# Hive的优化

## Fetch抓取

​		Fetch是指*在Hive中对于某些情况的查询不必使用MR的计算*。如：`SELECT * FROM employees`；这种情况Hive能够简单地读取employees对应的存储目录下的文件，然后输出结果到控制台。

​		在hive-default.xml.template文件中hive.fetch.task.conversion默认是more，*老版本hive默认是minimal*，该属性修改为more以后，在全局查找、字段查找、limit查找等都不走mapreduce。

配置文件如下：

```xml
<property>
    <name>hive.fetch.task.conversion</name>
    <value>more</value>
    <description>
      Expects one of [none, minimal, more].
      Some select queries can be converted to single FETCH task minimizing latency.
      Currently the query should be single sourced not having any subquery and should not have any aggregations or distincts (which incurs RS), lateral views and joins.
      0. none : disable hive.fetch.task.conversion
      1. minimal : SELECT STAR, FILTER on partition columns, LIMIT only
      2. more  : SELECT, FILTER, LIMIT only (support TABLESAMPLE and virtual columns)
    </description>
</property>
```

## 表的优化

### 小表、大表Join

​		将key相对分散，并且数据量小的表放在join的左边，这样可以有效减少内存溢出错误发生的几率；再进一步，可以使用map join让小的维度表（1000条以下的记录条数）先进内存。在map端完成reduce。

​		新版Hive对小表和大表join进行了优化，小表放在左边右边已经没有什么区别了。默认开启。

**案例**

1. 需求

测试大表JOIN小表和小表JOIN大表的效率

2. 建大表、小表和JOIN后表的语句

    ```
    // 创建大表
    create table bigtable(id bigint, t bigint, uid string, keyword string, url_rank int, click_num int, click_url string) row format delimited fields terminated by '\t';
    ```

    ```
    // 创建小表
    create table smalltable(id bigint, t bigint, uid string, keyword string, url_rank int, click_num int, click_url string) row format delimited fields terminated by '\t';
    ```

    ```
    // 创建join后表的语句
    create table jointable(id bigint, t bigint, uid string, keyword string, url_rank int, click_num int, click_url string) row format delimited fields terminated by '\t';
    ```

3. 分别向大表和小表中导入数据

    ```
    hive (default)> load data local inpath '/opt/module/datas/bigtable' into table bigtable;
    hive (default)>load data local inpath '/opt/module/datas/smalltable' into table smalltable;
    ```

4. 关闭mapjoin功能（默认是打开的）

    ```
    set hive.auto.convert.join = false;
    ```

5. 执行小表JOIN大表语句

    ```
    insert overwrite table jointable
    select b.id, b.t, b.uid, b.keyword, b.url_rank, b.click_num, b.click_url
    from smalltable s
    join bigtable  b
    on b.id = s.id;
    
    Time taken: 35.921 seconds
    No rows affected (44.456 seconds)
    ```

6. 执行大表JOIN小表语句

    ```
    insert overwrite table jointable
    select b.id, b.t, b.uid, b.keyword, b.url_rank, b.click_num, b.click_url
    from bigtable  b
    join smalltable  s
    on s.id = b.id;
    
    Time taken: 34.196 seconds
    No rows affected (26.287 seconds)
    ```

    

### 大表Join大表

**空KEY过滤**

有时join超时是因为某些key对应的数据太多，而相同key对应的数据都会发送到相同的reducer上，从而导致内存不够。此时我们应该仔细分析这些异常的key，很多情况下，这些key对应的数据是异常数据，我们需要在SQL语句中进行过滤。例如key对应的字段为空，操作如下：

案例实操

1. 配置历史服务器

配置mapred-site.xml

```xml
<property>
    <name>mapreduce.jobhistory.address</name
    <value>hadoop102:10020</value>
</property>
<property>
    <name>mapreduce.jobhistory.webapp.address</name>
    <value>hadoop102:19888</value>
</property>
```

启动历史服务器

```
sbin/mr-jobhistory-daemon.sh start historyserver
```

查看jobhistory

http://hadoop102:19888/jobhistory

2. 创建原始数据表、空id表、合并后数据表

```
// 创建原始表
create table ori(id bigint, t bigint, uid string, keyword string, url_rank int, click_num int, click_url string) row format delimited fields terminated by '\t';
```

```
// 创建空id表
create table nullidtable(id bigint, t bigint, uid string, keyword string, url_rank int, click_num int, click_url string) row format delimited fields terminated by '\t';
```

```
// 创建join后表的语句
create table jointable(id bigint, t bigint, uid string, keyword string, url_rank int, click_num int, click_url string) row format delimited fields terminated by '\t';
```

3. 分别加载原始数据和空id数据到对应表中

```
hive (default)> load data local inpath '/opt/module/datas/ori' into table ori;
hive (default)> load data local inpath '/opt/module/datas/nullid' into table nullidtable;
```

4. 测试不过滤空id

```
hive (default)> insert overwrite table jointable select n.* from nullidtable n
				left join ori o on n.id = o.id;

Time taken: 37.284 seconds
```

5. 测试过滤空id

```
hive (default)> insert overwrite table jointable select n.* from (select * from 					nullidtable where id is not null ) n left join ori o on n.id = o.id;

Time taken: 28.876 seconds
```

**空key转换**

当key为空对应的数据很多，但是对应的数据不是异常数据，必须要包含join的结果中，此时我们可以表a中key为空的字段赋一个随机的值，使得数据随机均匀地分不到不同的reducer上。

如：

```
insert overwrite table jointable select n.* from nullidtable n full join ori o on 
nvl(n.id,rand()) = o.id;
```

### MapJoin（MR引擎）

​		如果不指定MapJoin或者不符合MapJoin的条件，那么Hive解析器会将Join操作转换成Common Join，即：在Reduce阶段完成join。容易发生数据倾斜。可以用MapJoin把小表全部加载到内存在map端进行join，避免reducer处理。

MapJoin默认开启，小表的大小为25M，当服务器内存大于128G时，可以适当增大。

1. 开启MapJoin参数设置

    （1）设置自动选择Mapjoin

    ```
    set hive.auto.convert.join = true; 默认为true
    ```

    （2）大表小表的阈值设置（默认25M一下认为是小表）：

    ```
    set hive.mapjoin.smalltable.filesize=25000000;
    ```

2. MapJoin工作机制

3. 案例实操： 
    （1）开启Mapjoin功能

    ```
    set hive.auto.convert.join = true; 默认为true
    ```

    （2）执行小表JOIN大表语句

    ```
    insert overwrite table jointable
    select b.id, b.t, b.uid, b.keyword, b.url_rank, b.click_num, b.click_url
    from smalltable s
    left join bigtable  b
    on s.id = b.id;
    Time taken: 24.594 seconds
    ```

    （3）执行大表JOIN小表语句

    ```
    insert overwrite table jointable
    select b.id, b.t, b.uid, b.keyword, b.url_rank, b.click_num, b.click_url
    from bigtable  b
    left join smalltable  s
    on s.id = b.id;
    Time taken: 24.315 seconds
    ```

    

### Group By

​		解决数据倾斜问题。

​		默认情况下，Map阶段同一Key数据分发给一个reduce，当一个key数据过大时就倾斜了。

​		并不是所有的聚合操作都需要在Reduce端完成，很多聚合操作都可以先在Map端进行部分聚合，最后在Reduce端得出最终结果。

1. 开启Map端聚合参数设置

    （1）是否在Map端进行聚合，默认为True

    ```
    set hive.map.aggr = true
    ```

    （2）在Map端进行聚合操作的条目数目

    ```
    set hive.groupby.mapaggr.checkinterval = 100000
    ```

    （3）有数据倾斜的时候进行*负载均衡*（默认是false）

    ```
    set hive.groupby.skewindata = true
    ```

    *当选项设定为 true，生成的查询计划会有两个MR Job*。第一个MR Job中，Map的输出结果会随机分布到Reduce中，每个Reduce做部分聚合操作，并输出结果，*这样处理的结果是相同的Group By Key有可能被分发到不同的Reduce中，从而达到负载均衡的目的*；第二个MR Job再根据预处理的数据结果按照Group By Key分布到Reduce中（这个过程可以保证相同的Group By Key被分布到同一个Reduce中），最后完成最终的聚合操作。

    ```
    hive (default)> select deptno from emp group by deptno;
    Stage-Stage-1: Map: 1  Reduce: 5   Cumulative CPU: 23.68 sec   HDFS Read: 19987 HDFS Write: 9 SUCCESS
    Total MapReduce CPU Time Spent: 23 seconds 680 msec
    OK
    deptno
    10
    20
    30
    ```

    优化以后

    ```
    hive (default)> set hive.groupby.skewindata = true;
    hive (default)> select deptno from emp group by deptno;
    Stage-Stage-1: Map: 1  Reduce: 5   Cumulative CPU: 28.53 sec   HDFS Read: 18209 HDFS Write: 534 SUCCESS
    Stage-Stage-2: Map: 1  Reduce: 5   Cumulative CPU: 38.32 sec   HDFS Read: 15014 HDFS Write: 9 SUCCESS
    Total MapReduce CPU Time Spent: 1 minutes 6 seconds 850 msec
    OK
    deptno
    10
    20
    30
    ```

### 笛卡尔积

​		尽量避免笛卡尔积，join的时候不加on条件，或者无效的on条件，Hive只能使用1个reducer来完成笛卡尔积。

### 行列过滤

​		列处理：在SELECT中，只拿需要的列，如果有，尽量使用分区过滤，少用SELECT *。
​		行处理：在分区剪裁中，当使用外关联时，如果将副表的过滤条件写在Where后面，那么就会先全表关联，之后再过滤，比如：

**案例实操：**

1. 测试先关联两张表，再用where条件过滤

    ```
    hive (default)> select o.id from bigtable b
    join ori o on o.id = b.id
    where o.id <= 10;
    Time taken: 34.406 seconds, Fetched: 100 row(s)
    ```

2. 通过子查询后，再关联表

    ```
    hive (default)> select b.id from bigtable b
    join (select id from ori where id <= 10 ) o on b.id = o.id;
    Time taken: 30.058 seconds, Fetched: 100 row(s)
    ```

    

### 动态分区



### 分桶

## 合理设置Map及Reduce数（MR引擎）

（1）通常情况下，作业会通过input的目录产生一个或者多个map任务。

主要的决定因素有：input的文件总个数，input的文件大小，集群设置的文件块大小。

（2）是不是map数越多越好？

答案是否定的。如果一个任务有很多小文件（远远小于块大小128m），则每个小文件也会被当做一个块，用一个map任务来完成，而一个map任务启动和初始化的时间远远大于逻辑处理的时间，就会造成很大的资源浪费。而且，同时可执行的map数是受限的。

（3）是不是保证每个map处理接近128m的文件块，就高枕无忧了？

答案也是不一定。比如有一个127m的文件，正常会用一个map去完成，但这个文件只有一个或者两个小字段，却有几千万的记录，如果map处理的逻辑比较复杂，用一个map任务去做，肯定也比较耗时。

针对上面的问题2和3，我们需要采取两种方式来解决：即减少map数和增加map数；

### 复杂文件增加Map数

​		当input的文件都很大，任务逻辑复杂，map执行非常慢的时候，可以考虑*增加Map数*，来使得每个map处理的数据量减少，从而提高任务的执行效率。

​		增加map的方法为：根据

```
computeSliteSize(Math.max(minSize,Math.min(maxSize,blocksize)))=blocksize=128M
```

公式，调整maxSize最大值。让maxSize最大值低于blocksize就可以增加map的个数。

案例实操：

1. 执行查询

```
hive (default)> select count(*) from emp;
Hadoop job information for Stage-1: number of mappers: 1; number of reducers: 1
```

2. 设置最大切片值为100个字节

```
hive (default)> set mapreduce.input.fileinputformat.split.maxsize=100;
hive (default)> select count(*) from emp;
Hadoop job information for Stage-1: number of mappers: 6; number of reducers: 1
```

### 小文件进行合并减少Map数

1. 在map执行前合并小文件，减少map数：CombineHiveInputFormat具有对小文件进行合并的功能（系统默认的格式）。HiveInputFormat没有对小文件合并功能。

```
set hive.input.format= org.apache.hadoop.hive.ql.io.CombineHiveInputFormat;
```

2. 在Map-Reduce的任务结束时合并小文件的设置：

    在*map-only任务*结束时合并小文件，默认true

```
SET hive.merge.mapfiles = true;
```

​		在*map-reduce任务*结束时合并小文件，默认false

```
SET hive.merge.mapredfiles = true;
```

​		合并文件的大小，默认256M

​		SET hive.merge.size.per.task = 268435456;

​		当输出文件的平均大小小于该值时，启动一个独立的map-reduce任务进行文件merge

```
SET hive.merge.smallfiles.avgsize = 16777216;
```

### 合理设置Reduce数

1. 调整reduce个数方法

    （1）每个Reduce处理的数据量默认是256MB

    ```
    hive.exec.reducers.bytes.per.reducer=256000000
    ```

    （2）每个任务最大的reduce数，默认为1009

    ```
    hive.exec.reducers.max=1009
    ```

    （3）计算reducer数的公式

    ```
    N=min(参数2，总输入数据量/参数1)
    ```

2. 调整reduce个数方法二

    在hadoop的mapred-default.xml文件中修改

    设置每个job的Reduce个数

    ```
    set mapreduce.job.reduces = 15;
    ```

3. reduce个数并不是越多越好

    （1）过多的启动和初始化reduce也会消耗时间和资源；

    （2）另外，有多少个reduce，就会有多少个输出文件，如果生成了很多个小文件，那么如果这些小文件作为下一个任务的输入，则也会出现小文件过多的问题；

    在设置reduce个数的时候也需要考虑这两个原则：处理大数据量利用合适的reduce数；使单个reduce任务处理数据量大小要合适；

## 并行执行

​		Hive会将一个查询转化成一个或者多个阶段。这样的阶段可以是MapReduce阶段、抽样阶段、合并阶段、limit阶段。或者Hive执行过程中可能需要的其他阶段。默认情况下，Hive一次只会执行一个阶段。不过，某个特定的job可能包含众多的阶段，而这些阶段可能并非完全互相依赖的，也就是说有些阶段是可以并行执行的，这样可能使得整个job的执行时间缩短。不过，如果有更多的阶段可以并行执行，那么job可能就越快完成。

​		通过设置参数hive.exec.parallel值为true，就可以开启并发执行。不过，在共享集群中，需要注意下，如果job中并行阶段增多，那么集群利用率就会增加。

```
	set hive.exec.parallel=true;       //打开任务并行执行
	set hive.exec.parallel.thread.number=16; //同一个sql允许最大并行度，默认为8。
```

*当然，得是在系统资源比较空闲的时候才有优势，否则，没资源，并行也起不来。*

## 严格模式

Hive可以通过设置防止一些危险操作：

（1）将hive.strict.checks.no.partition.filter设置为true时，对于分区表，除非where语句中含有分区字段过滤条件来限制范围，否则不允许执行。换句话说，就是用户不允许扫描所有分区。进行这个限制的原因是，通常分区表都拥有非常大的数据集，而且数据增加迅速。没有进行分区限制的查询可能会消耗令人不可接受的巨大资源来处理这个表。

（2）将hive.strict.checks.orderby.no.limit设置为true时，对于使用了order by语句的查询，要求必须使用limit语句。因为order by为了执行排序过程会将所有的结果数据分发到同一个Reducer中进行处理，强制要求用户增加这个LIMIT语句可以防止Reducer额外执行很长一段时间。

（3）将hive.strict.checks.cartesian.product设置为true时，会限制笛卡尔积的查询。对关系型数据库非常了解的用户可能期望在执行JOIN查询的时候不使用ON语句而是使用where语句，这样关系数据库的执行优化器就可以高效地将WHERE语句转化成那个ON语句。不幸的是，Hive并不会执行这种优化，因此，如果表足够大，那么这个查询就会出现不可控的情况。

## JVM重用

​		JVM重用是Hadoop调优参数的内容，其对Hive的性能具有非常大的影响，特别是对于很难避免小文件的场景或task特别多的场景，这类场景大多数执行时间都很短。

​		Hadoop的默认配置通常是使用派生JVM来执行map和Reduce任务的。这时JVM的启动过程可能会造成相当大的开销，尤其是执行的job包含有成百上千task任务的情况。JVM重用可以使得JVM实例在同一个job中重新使用N次。N的值可以在Hadoop的mapred-site.xml文件中进行配置。通常在10-20之间，具体多少需要根据具体业务场景测试得出。

```xml
<property>
    <name>mapreduce.job.jvm.numtasks</name>
    <value>10</value>
    <description>How many tasks to run per jvm. If set to -1, there is no limit. 
    </description>
</property>
```

​		这个功能的缺点是，开启JVM重用将一直占用使用到的task插槽，以便进行重用，直到任务完成后才能释放。如果某个“不平衡的”job中有某几个reduce task执行的时间要比其他Reduce task消耗的时间多的多的话，那么保留的插槽就会一直空闲着却无法被其他的job使用，直到所有的task都结束了才会释放。

## 压缩

## 执行计划（Explain）