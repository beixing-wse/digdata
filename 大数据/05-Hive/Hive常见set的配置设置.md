# Hive常见set的配置设置

设置reduce数量（默认值-1）

`set mapred.reduce.tasks=100;`

`set mapreduce.job.reduces=3;`



修改表为内部表

`set tblproperties('EXTERNAL'='FALSE');`



开启分桶表（默认false）

`set hive.enforce.bucketing=true;`



开启Hive中间传输数据压缩功能

`set hive.exec.cmpress.intermediate=true;`

开启mapreduce 中map 输出压缩功能

`set mapreduce.map.output.compress=true;`

设置mapreduce 中map 输出数据的压缩方式

`set mapreduce.map.output.compress.codec=
org.apache.hadoop.io.compress.SnappyCodec;`

开启hive 最终输出数据压缩功能

`set hive.exec.compress.output=true;`

开启mapreduce 最终输出数据压缩

`set mapreduce.output.fileoutputformat.compress=true;`

设置mapreduce 最终数据输出压缩方式

`set mapreduce.output.fileoutputformat.compress.codec =
org.apache.hadoop.io.compress.SnappyCodec;`

设置mapreduce 最终数据输出压缩为块压缩

`set mapreduce.output.fileoutputformat.compress.type=BLOCK;`



设置Fetch抓取为more（默认为more）

`set hive.fetch.task.conversion=more;`



开启本地模式（默认关闭）

`set hive.exec.mode.local.auto=true; `

设置local mr 的最大输入数据量，当输入数据量小于这个值时采用local mr 的
方式，默认为134217728，即128M
`set hive.exec.mode.local.auto.inputbytes.max=50000000;`
设置local mr 的最大输入文件个数，当输入文件个数小于这个值时采用local mr
的方式，默认为4
`set hive.exec.mode.local.auto.input.files.max=10;`



打开mapjoin 功能（默认是打开的）

`set hive.auto.convert.join = true;`



开启Map 端聚合参数设置

`set hive.map.aggr = true;`

在Map 端进行聚合操作的条目数目

`set hive.groupby.mapaggr.checkinterval = 100000;`

有数据倾斜的时候进行负载均衡（默认是false）

`set hive.groupby.skewindata = true;`



开启动态分区功能（默认开启）

`set hive.exec.dynamic.partition=true;`



设置为非严格模式（默认严格strict）

`set hive.exec.dynamic.partition.mode=nonstrict;`



在所有执行MR 的节点上，最大一共可以创建多少个动态分区。（1000）

`set hive.exec.max.dynamic.partitions=1000;`

在每个执行MR 的节点上，最大可以创建多少个动态分区（100）

`set hive.exec.max.dynamic.partitions.pernode=100;`

整个MR Job 中，最大可以创建多少个HDFS 文件。（100000）

`set hive.exec.max.created.files=100000;`



开启小文件合并（HiveInputFormat ）

`set hive.input.formatorg.apache.hadoop.hive.ql.io.CombineHiveInputFormat;`

每个Reduce 处理的数据量默认是256MB256000000）

`set mapreduce.input.fileinputformat.split.maxsize=256000000;`

每个任务最大的reduce 数，默认为1009

`set hive.exec.reducers.max=1009;`



开启并行执行（默认关闭）

`set hive.exec.parallel=true; `

同一个sql 允许最大并行度，默认为8。

`set hive.exec.parallel.thread.number=16; `