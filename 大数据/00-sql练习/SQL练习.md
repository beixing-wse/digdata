# SQL习题

## 案例1（求月累计销售总额）

求如下 报表：

店铺,月份,月总销售额,截止到当月的总累计销售额

| name | month | day  | money |
| ---- | ----- | ---- | ----- |
| a    | 1     | 2    | 100   |
| a    | 1     | 5    | 200   |
| a    | 2     | 1    | 500   |
| a    | 2     | 3    | 600   |
| a    | 2     | 7    | 400   |
| a    | 3     | 3    | 100   |
| a    | 3     | 6    | 200   |
| a    | 3     | 8    | 400   |
| b    | 1     | 3    | 100   |
| b    | 1     | 7    | 220   |
| b    | 2     | 8    | 500   |
| b    | 2     | 13   | 300   |
| b    | 2     | 27   | 460   |
| b    | 3     | 5    | 100   |
| b    | 3     | 16   | 250   |
| b    | 3     | 18   | 450   |

参考示例：

| name | month | amt  | money |
| ---- | ----- | ---- | ----- |
| a    | 1     | 300  | 300   |
| a    | 2     | 1500 | 1800  |
| a    | 3     | 700  | 2500  |
| b    | 1     | 320  | 320   |
| b    | 2     | 1260 | 1580  |
| b    | 3     | 800  | 2380  |

- 建表语句

```sql
CREATE table baobiao(
	name String,
	month int,
	day int,
	money int
)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ',';
```

1. 将原表按店铺名和月份联合分组求销售额（t1）

```sql
SELECT name,month,sum(money) sum_money from baobiao group by name, month;
```

2. 对上表进行开窗（按店铺名分区，月份排序进行开窗）

```sql
SELECT 
	t.name,t.month ,t.sum_money ,sum(sum_money) over (PARTITION  by t.name  ORDER by t.month)
from 
(SELECT name,month,sum(money) sum_money from baobiao group by name, month) t;
```

## 案例2（打地鼠连续命中）

--beat  1 代表击中  0 代表未击中

| uid  | seq  | beat |
| ---- | ---- | ---- |
| u01  | 1    | 1    |
| u01  | 2    | 0    |
| u01  | 3    | 1    |
| u01  | 4    | 1    |
| u01  | 5    | 0    |
| u01  | 6    | 1    |
| u02  | 1    | 1    |
| u02  | 2    | 1    |
| u02  | 3    | 0    |
| u02  | 4    | 1    |
| u02  | 5    | 1    |
| u02  | 6    | 0    |
| u02  | 7    | 0    |
| u02  | 8    | 1    |
| u02  | 9    | 1    |
| u03  | 1    | 1    |
| u03  | 2    | 1    |
| u03  | 3    | 1    |
| u03  | 4    | 1    |
| u03  | 5    | 1    |
| u03  | 6    | 0    |

建表语句

```sql
CREATE table dishu(
	uid String,
	seq int,
	beat int
)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ',';
```

1. 过滤出命中的数据  t1

```sql
select 
* 
from 
dishu 
where  beat = 1;
```

2. 按照 id 和 seq 分组累加命中次数 t2

```sql
SELECT 
t1.uid,
t1.seq,
sum(t1.beat) over(partition by t1.uid order by t1.seq) n
from (select 
* 
from 
dishu 
where  beat = 1) t1;
```

3. 将 t2 表的命中次数 n 和 seq 相减

```sql
SELECT 
t2.*,
t2.seq-t2.n x
from (SELECT 
t1.uid,
t1.seq,
sum(t1.beat) over(partition by t1.uid order by t1.seq) n
from (select 
* 
from 
dishu 
where  beat = 1) t1) t2;
```

4. 将 t3 表按 id 和 x 分组求组内成员个数（即连续命中次数）

```sql
SELECT t3.uid uid ,COUNT(*) y
FROM (SELECT 
t2.*,
t2.seq-t2.n x
from (SELECT 
t1.uid,
t1.seq,
sum(t1.beat) over(partition by t1.uid order by t1.seq) n
from (select 
* 
from 
dishu 
where  beat = 1) t1) t2) t3
GROUP by t3.uid,t3.x;
```

5. 过滤出连续命中次数大于 3 次的uid

```sql
select
*
from
(SELECT t3.uid uid ,COUNT(*) y
FROM (SELECT 
t2.*,
t2.seq-t2.n x
from (SELECT 
t1.uid,
t1.seq,
sum(t1.beat) over(partition by t1.uid order by t1.seq) n
from (select 
* 
from 
dishu 
where  beat = 1) t1) t2) t3
GROUP by t3.uid,t3.x) t4
where t4.x>3
```

## 案例3（列转行）

数据如下：

| uid  | event     |
| ---- | --------- |
| u01  | ad_click  |
| u01  | ad_show   |
| u01  | favor_sku |
| u01  | ad_click  |
| u01  | pageview  |
| u01  | searchs   |
| u02  | ad_click  |
| u02  | ad_show   |
| u02  | favor_sku |
| u02  | addcart   |
| u02  | pageview  |
| u02  | pageview  |

要求：
需求1：假如数据中的事件类型是已知且固定的，求如下报表：

| uid  | ad_click | ad_show | favor_sku | pageview | searchs | addcart |
| ---- | -------- | ------- | --------- | -------- | ------- | ------- |
| u01  | 2        | 1       | 1         | 1        | 1       | 0       |
| u02  | 1        | 1       | 1         | 2        | 0       | 1       |

```sql
SELECT 
uid,
sum (case event when 'ad_click' then 1 else 0 end) ad_click,
sum (case event when 'ad_show' then 1 else 0 end) ad_show,
sum (case event when 'favor_sku' then 1 else 0 end) favor_sku,
sum (case event when 'pageview' then 1 else 0 end) pageview,
sum (case event when 'searchs' then 1 else 0 end) searchs,
sum (case event when 'addcart' then 1 else 0 end) addcart
from anli_three 
group by uid;
```

## 案例4（销售天数的最大记录）

-- 求： 每家店铺连续销售天数的最大记录 （针对以下数据作答就好）

| id   | time       | sale |
| ---- | ---------- | ---- |
| a    | 2019-02-01 | 300  |
| a    | 2019-02-02 | 500  |
| a    | 2019-02-03 | 550  |
| a    | 2019-02-05 | 400  |
| a    | 2019-02-06 | 500  |
| b    | 2019-02-01 | 300  |
| b    | 2019-02-02 | 500  |
| b    | 2019-02-03 | 550  |
| b    | 2019-02-04 | 400  |
| b    | 2019-02-05 | 500  |

参考示例：

| id   | _c1  |
| ---- | ---- |
| a    | 3    |
| b    | 5    |

1. 开窗

```sql
SELECT 
id,
tim,sql
ROW_NUMBER() over(partition by id ORDER BY tim) n
from anli_four ;
```

2. 

```sql
SELECT 
t1.id,
t1.tim,
t1.n,
date_sub(t1.tim,t1.n) tim2
from (SELECT 
id,
tim,
ROW_NUMBER() over(partition by id ORDER BY tim) n
from anli_four) t1 ;
```

3. 

```sql
SELECT 
t2.id,
COUNT(*)
from (SELECT 
t1.id,
t1.tim,
t1.n,
date_sub(t1.tim,t1.n) tim2
from (SELECT 
id,
tim,
ROW_NUMBER() over(partition by id ORDER BY tim) n
from anli_four) t1)t2
group by t2.id,t2.tim2;
```

--借助于emp表和dept表

--1.找出各月倒数第3天受雇的所有员工.
示例：
+---------+-------------+
|  ename  |  hiredate   |
+---------+-------------+
| MARTIN  | 1981-09-28  |
+---------+-------------+

```sql
SELECT 
	ename,hiredate
FROM 
	emp
where
	2 = datediff(last_day(hiredate),hiredate); 
```



--2.找出早于12年前受雇的员工.
示例：
+---------+-------------+
|  ename  |  hiredate   |
+---------+-------------+
| SMITH   | 1980-12-17  |
| ALLEN   | 1981-02-20  |
| WARD    | 1981-02-22  |
| JONES   | 1981-04-02  |
| MARTIN  | 1981-09-28  |
| BLAKE   | 1981-05-01  |
| CLARK   | 1981-06-09  |
| SCOTT   | 1987-07-13  |
| KING    | 1981-11-17  |
| TURNER  | 1981-09-08  |
| ADAMS   | 1987-07-13  |
| JAMES   | 1981-12-03  |
| FORD    | 1981-12-03  |
| MILLER  | 1982-01-23  |
+---------+-------------+

```

```

--3.以首字母大写的方式显示所有员工的姓名.
示例：
Smith
Allen
Ward
Jones
Martin
Blake
Clark
Scott
King
Turner
Adams
James
Ford
Miller


--4.显示正好为5个字符的员工的姓名.
示例：
SMITH
ALLEN
JONES
BLAKE
CLARK
SCOTT
ADAMS
JAMES


--5.显示不带有"R"的员工的姓名
示例：
SMITH
ALLEN
JONES
BLAKE
SCOTT
KING
ADAMS
JAMES



--6.显示所有员工姓名的前三个字符.
示例：
SMI
ALL
WAR
JON
MAR
BLA
CLA
SCO
KIN
TUR
ADA
JAM
FOR
MIL


--7.显示所有员工的姓名,用a替换所有"A"
示例：
SMITH
aLLEN
WaRD
JONES
MaRTIN
BLaKE
CLaRK
SCOTT
KING
TURNER
aDaMS
JaMES
FORDM
ILLER

-<7.显示所有员工的姓名,如果不足位的，前边补0；
lpad


--8.显示满10年服务年限的员工的姓名和受雇日期.:
示例：
+---------+-------------+
|  ename  |  hiredate   |
+---------+-------------+
| SMITH   | 1980-12-17  |
| ALLEN   | 1981-02-20  |
| WARD    | 1981-02-22  |
| JONES   | 1981-04-02  |
| MARTIN  | 1981-09-28  |
| BLAKE   | 1981-05-01  |
| CLARK   | 1981-06-09  |
| SCOTT   | 1987-07-13  |
| KING    | 1981-11-17  |
| TURNER  | 1981-09-08  |
| ADAMS   | 1987-07-13  |
| JAMES   | 1981-12-03  |
| FORD    | 1981-12-03  |
| MILLER  | 1982-01-23  |
+---------+-------------+



--9.显示员工的详细资料,按姓名排序.
示例：
+------------+------------+------------+----------+---------------+----------+-----------+-------------+
| emp.empno  | emp.ename  |  emp.job   | emp.mgr  | emp.hiredate  | emp.sal  | emp.comm  | emp.deptno  |
+------------+------------+------------+----------+---------------+----------+-----------+-------------+
| 7876       | ADAMS      | CLERK      | 7788     | 1987-07-13    | 1100     | NULL      | 20          |
| 7499       | ALLEN      | SALESMAN   | 7698     | 1981-02-20    | 1600     | 300       | 30          |
| 7698       | BLAKE      | MANAGER    | 7839     | 1981-05-01    | 2850     | NULL      | 30          |
| 7782       | CLARK      | MANAGER    | 7839     | 1981-06-09    | 2450     | NULL      | 10          |
| 7902       | FORD       | ANALYST    | 7566     | 1981-12-03    | 3000     | NULL      | 20          |
| 7900       | JAMES      | CLERK      | 7698     | 1981-12-03    | 950      | NULL      | 30          |
| 7566       | JONES      | MANAGER    | 7839     | 1981-04-02    | 2975     | NULL      | 20          |
| 7839       | KING       | PRESIDENT  | NULL     | 1981-11-17    | 5000     | NULL      | 10          |
| 7654       | MARTIN     | SALESMAN   | 7698     | 1981-09-28    | 1250     | 1400      | 30          |
| 7934       | MILLER     | CLERK      | 7782     | 1982-01-23    | 1300     | NULL      | 10          |
| 7788       | SCOTT      | ANALYST    | 7566     | 1987-07-13    | 3000     | NULL      | 20          |
| 7369       | SMITH      | CLERK      | 7902     | 1980-12-17    | 800      | NULL      | 20          |
| 7844       | TURNER     | SALESMAN   | 7698     | 1981-09-08    | 1500     | 0         | 30          |
| 7521       | WARD       | SALESMAN   | 7698     | 1981-02-22    | 1250     | 500       | 30          |
+------------+------------+------------+----------+---------------+----------+-----------+-------------+

--10.显示员工的姓名和受雇日期,根据其服务年限,将最老的员工排在最前面.
示例：
+---------+-------------+
|  ename  |  hiredate   |
+---------+-------------+
| SMITH   | 1980-12-17  |
| ALLEN   | 1981-02-20  |
| WARD    | 1981-02-22  |
| JONES   | 1981-04-02  |
| BLAKE   | 1981-05-01  |
| CLARK   | 1981-06-09  |
| TURNER  | 1981-09-08  |
| MARTIN  | 1981-09-28  |
| KING    | 1981-11-17  |
| JAMES   | 1981-12-03  |
| FORD    | 1981-12-03  |
| MILLER  | 1982-01-23  |
| SCOTT   | 1987-07-13  |
| ADAMS   | 1987-07-13  |
+---------+-------------+



--11.显示所有员工的姓名、工作和薪金,按工作的降序排序,若工作相同则按薪金排序.
示例：
+---------+------------+-------+
|  ename  |    job     |  sal  |
+---------+------------+-------+
| WARD    | SALESMAN   | 1250  |
| MARTIN  | SALESMAN   | 1250  |
| TURNER  | SALESMAN   | 1500  |
| ALLEN   | SALESMAN   | 1600  |
| KING    | PRESIDENT  | 5000  |
| CLARK   | MANAGER    | 2450  |
| BLAKE   | MANAGER    | 2850  |
| JONES   | MANAGER    | 2975  |
| SMITH   | CLERK      | 800   |
| JAMES   | CLERK      | 950   |
| ADAMS   | CLERK      | 1100  |
| MILLER  | CLERK      | 1300  |
| SCOTT   | ANALYST    | 3000  |
| FORD    | ANALYST    | 3000  |
+---------+------------+-------+


--12.显示所有员工的姓名、加入公司的年份和月份,按受雇日期所在月排序,若月份相同则将最早年份的员工排在最前面.
示例：
+---------+-------+-----+
|  ename  |   y   |  m  |
+---------+-------+-----+
| MILLER  | 1982  | 1   |
| ALLEN   | 1981  | 2   |
| WARD    | 1981  | 2   |
| JONES   | 1981  | 4   |
| BLAKE   | 1981  | 5   |
| CLARK   | 1981  | 6   |
| SCOTT   | 1987  | 7   |
| ADAMS   | 1987  | 7   |
| TURNER  | 1981  | 9   |
| MARTIN  | 1981  | 9   |
| KING    | 1981  | 11  |
| SMITH   | 1980  | 12  |
| JAMES   | 1981  | 12  |
| FORD    | 1981  | 12  |
+---------+-------+-----+


--14.找出在(任何年份的)2月受聘的所有员工。
示例：
+--------+-------------+
| ename  |  hiredate   |
+--------+-------------+
| ALLEN  | 1981-02-20  |
| WARD   | 1981-02-22  |
+--------+-------------+


--15.对于每个员工,显示其加入公司的天数.
示例：

+---------+---------------------+
|  ename  |          d          |
+---------+---------------------+
| SMITH   | 14569.382407407407  |
| ALLEN   | 14504.382407407407  |
| WARD    | 14502.382407407407  |
| JONES   | 14463.382407407407  |
| MARTIN  | 14284.382407407407  |
| BLAKE   | 14434.382407407407  |
| CLARK   | 14395.382407407407  |
| SCOTT   | 12170.424074074073  |
| KING    | 14234.382407407407  |
| TURNER  | 14304.382407407407  |
| ADAMS   | 12170.424074074073  |
| JAMES   | 14218.382407407407  |
| FORD    | 14218.382407407407  |
| MILLER  | 14167.382407407407  |
+---------+---------------------+


--16.显示姓名字段的任何位置包含"A"的所有员工的姓名.
示例：


--17.列出所有job=‘CLERK’ 的员工平均薪资
示例：
+------------+
|   avgsal   |
+------------+
| 1037.5000  |
+------------+


--18.列出job=‘CLERK’员工的平均薪资 按照部门分组 
示例：
+---------+------------+
| deptno  |   avgsal   |
+---------+------------+
| 10      | 1300.0000  |
| 20      | 950.0000   |
| 30      | 950.0000   |
+---------+------------+



--19.列出job=‘CLERK’员工的平均薪资 按照部门分组 并且部门编号 in(10,30) 按照平均薪资 降序排列
示例：
+---------+------------+
| deptno  |   avgsal   |
+---------+------------+
| 30      | 950.0000   |
| 10      | 1300.0000  |
+---------+------------+


--20.列出job=‘CLERK’员工的平均薪资 按照部门分组 并且部门编号 in(20,30) 并且部门员工数量>=2人 按照平均薪资 降序排列
示例：
 +---------+-----------+-------+
| deptno  |  avgsal   | cemp  |
+---------+-----------+-------+
| 20      | 950.0000  | 2     |
+---------+-----------+-------+





1、列出至少有一个员工的所有部门。

示例：
+-------------+------+
|    name     | cou  |
+-------------+------+
| ACCOUNTING  | 3    |
| RESEARCH    | 5    |
| SALES       | 6    |
+-------------+------+
		
2、列出薪金比“SMITH”多的所有员工。（大于最大薪水SMITH员工）


示例：
+---------+-------+
|  ename  |  sal  |
+---------+-------+
| ALLEN   | 1600  |
| WARD    | 1250  |
| JONES   | 2975  |
| MARTIN  | 1250  |
| BLAKE   | 2850  |
| CLARK   | 2450  |
| SCOTT   | 3000  |
| KING    | 5000  |
| TURNER  | 1500  |
| ADAMS   | 1100  |
| JAMES   | 950   |
| FORD    | 3000  |
| MILLER  | 1300  |
+---------+-------+


3、列出所有员工的姓名及其直接上级的姓名。

示例：
+---------+---------+
|  ename  | mgname  |
+---------+---------+
| SMITH   | FORD    |
| ALLEN   | BLAKE   |
| WARD    | BLAKE   |
| JONES   | KING    |
| MARTIN  | BLAKE   |
| BLAKE   | KING    |
| CLARK   | KING    |
| SCOTT   | JONES   |
| TURNER  | BLAKE   |
| ADAMS   | SCOTT   |
| JAMES   | BLAKE   |
| FORD    | JONES   |
| MILLER  | CLARK   |
+---------+---------+


4、列出受雇日期早于其直接上级的所有员工。

示例：
+--------+-------------+---------+-------------+
| ename  |   hirdate   | mgname  |   hirdate   |
+--------+-------------+---------+-------------+
| SMITH  | 1980-12-17  | FORD    | 1981-12-03  |
| ALLEN  | 1981-02-20  | BLAKE   | 1981-05-01  |
| WARD   | 1981-02-22  | BLAKE   | 1981-05-01  |
| JONES  | 1981-04-02  | KING    | 1981-11-17  |
| BLAKE  | 1981-05-01  | KING    | 1981-11-17  |
| CLARK  | 1981-06-09  | KING    | 1981-11-17  |
+--------+-------------+---------+-------------+


5、列出部门名称和这些部门的员工信息，包括那些没有员工的部门。


示例：
+------------+-------------+-----------+-----------+-----------+------------+---------+--------------+---------+----------+------------+
| t1.deptno  |  t1.dname   |  t1.loc   | t2.empno  | t2.ename  |   t2.job   | t2.mgr  | t2.hiredate  | t2.sal  | t2.comm  | t2.deptno  |
+------------+-------------+-----------+-----------+-----------+------------+---------+--------------+---------+----------+------------+
| 10         | ACCOUNTING  | NEW YORK  | 7934      | MILLER    | CLERK      | 7782    | 1982-01-23   | 1300    | NULL     | 10         |
| 10         | ACCOUNTING  | NEW YORK  | 7839      | KING      | PRESIDENT  | NULL    | 1981-11-17   | 5000    | NULL     | 10         |
| 10         | ACCOUNTING  | NEW YORK  | 7782      | CLARK     | MANAGER    | 7839    | 1981-06-09   | 2450    | NULL     | 10         |
| 20         | RESEARCH    | DALLAS    | 7876      | ADAMS     | CLERK      | 7788    | 1987-07-13   | 1100    | NULL     | 20         |
| 20         | RESEARCH    | DALLAS    | 7788      | SCOTT     | ANALYST    | 7566    | 1987-07-13   | 3000    | NULL     | 20         |
| 20         | RESEARCH    | DALLAS    | 7369      | SMITH     | CLERK      | 7902    | 1980-12-17   | 800     | NULL     | 20         |
| 20         | RESEARCH    | DALLAS    | 7566      | JONES     | MANAGER    | 7839    | 1981-04-02   | 2975    | NULL     | 20         |
| 20         | RESEARCH    | DALLAS    | 7902      | FORD      | ANALYST    | 7566    | 1981-12-03   | 3000    | NULL     | 20         |
| 30         | SALES       | CHICAGO   | 7844      | TURNER    | SALESMAN   | 7698    | 1981-09-08   | 1500    | 0        | 30         |
| 30         | SALES       | CHICAGO   | 7499      | ALLEN     | SALESMAN   | 7698    | 1981-02-20   | 1600    | 300      | 30         |
| 30         | SALES       | CHICAGO   | 7698      | BLAKE     | MANAGER    | 7839    | 1981-05-01   | 2850    | NULL     | 30         |
| 30         | SALES       | CHICAGO   | 7654      | MARTIN    | SALESMAN   | 7698    | 1981-09-28   | 1250    | 1400     | 30         |
| 30         | SALES       | CHICAGO   | 7521      | WARD      | SALESMAN   | 7698    | 1981-02-22   | 1250    | 500      | 30         |
| 30         | SALES       | CHICAGO   | 7900      | JAMES     | CLERK      | 7698    | 1981-12-03   | 950     | NULL     | 30         |
| 40         | OPERATIONS  | BOSTON    | NULL      | NULL      | NULL       | NULL    | NULL         | NULL    | NULL     | NULL       |
+------------+-------------+-----------+-----------+-----------+------------+---------+--------------+---------+----------+------------+


​	
6、列出所有job为“CLERK”（办事员）的姓名及其部门名称。


示例：
+---------+-------------+
|  ename  |    dname    |
+---------+-------------+
| SMITH   | RESEARCH    |
| ADAMS   | RESEARCH    |
| JAMES   | SALES       |
| MILLER  | ACCOUNTING  |
+---------+-------------+


​	
7、列出最低薪金大于1500的各种工作。


示例：
+------------+-------+
|    job     |  sal  |
+------------+-------+
| ANALYST    | 3000  |
| MANAGER    | 2450  |
| PRESIDENT  | 5000  |
+------------+-------+




8、列出在部门“SALES”（销售部）工作的员工的姓名，假定不知道销售部的部门编号。

示例：
+---------+
|  ename  |
+---------+
| ALLEN   |
| WARD    |
| MARTIN  |
| BLAKE   |
| TURNER  |
| JAMES   |
+---------+


​	
9、列出薪金高于公司平均薪金的所有员工。

示例：
+--------+-------+
| ename  |  sal  |
+--------+-------+
| JONES  | 2975  |
| BLAKE  | 2850  |
| CLARK  | 2450  |
| SCOTT  | 3000  |
| KING   | 5000  |
| FORD   | 3000  |
+--------+-------+




10、列出与“SCOTT”从事相同工作的所有员工。

示例：
+-----------+
| ename  |
+-----------+
| SCOTT     |
| FORD      |
+-----------+




​	
11、列出薪金等于部门30中员工的薪金的所有员工的姓名和薪金。

示例：
+---------+-------+---------+
|  ename  |  sal  | deptno  |
+---------+-------+---------+
| ALLEN   | 1600  | 30      |
| WARD    | 1250  | 30      |
| MARTIN  | 1250  | 30      |
| BLAKE   | 2850  | 30      |
| TURNER  | 1500  | 30      |
| JAMES   | 950   | 30      |
+---------+-------+---------+




12、列出薪金高于在部门30工作的所有员工的薪金的员工姓名和薪金。


示例：
+----------+--------+
| e.ename  | e.sal  |
+----------+--------+
| JONES    | 2975   |
| SCOTT    | 3000   |
| KING     | 5000   |
| FORD     | 3000   |
+----------+--------+


​	
13、列出在每个部门工作的员工数量、平均工资和平均服务期限。

示例：
+---------+-------------+-------+------------+--------------------+
| deptno  |    dname    | cemp  |   avgsal   |        fwqx        |
+---------+-------------+-------+------------+--------------------+
| 10      | ACCOUNTING  | 3     | 2916.6667  | 39.08204962582445  |
| 20      | RESEARCH    | 5     | 2175.0000  | 37.03460670345003  |
| 30      | SALES       | 6     | 1566.6667  | 39.38067976281076  |
| 40      | OPERATIONS  | NULL  | NULL       | NULL               |
+---------+-------------+-------+------------+--------------------+




14、列出所有员工的姓名、部门名称和工资。

示例：
+---------+-------------+-------+
|  ename  |    dname    |  sal  |
+---------+-------------+-------+
| SMITH   | RESEARCH    | 800   |
| ALLEN   | SALES       | 1900  |
| WARD    | SALES       | 1750  |
| JONES   | RESEARCH    | 2975  |
| MARTIN  | SALES       | 2650  |
| BLAKE   | SALES       | 2850  |
| CLARK   | ACCOUNTING  | 2450  |
| SCOTT   | RESEARCH    | 3000  |
| KING    | ACCOUNTING  | 5000  |
| TURNER  | SALES       | 1500  |
| ADAMS   | RESEARCH    | 1100  |
| JAMES   | SALES       | 950   |
| FORD    | RESEARCH    | 3000  |
| MILLER  | ACCOUNTING  | 1300  |
+---------+-------------+-------+


​	
15、列出从事同一种工作但属于不同部门的员工的一种组合。

示例：
+-----------+-----------+------------+------------+----------+
| t1.ename  | t2.ename  | t1.deptno  | t2.deptno  |   job    |
+-----------+-----------+------------+------------+----------+
| JAMES     | SMITH     | 30         | 20         | CLERK    |
| MILLER    | SMITH     | 10         | 20         | CLERK    |
| BLAKE     | JONES     | 30         | 20         | MANAGER  |
| CLARK     | JONES     | 10         | 20         | MANAGER  |
| JONES     | BLAKE     | 20         | 30         | MANAGER  |
| CLARK     | BLAKE     | 10         | 30         | MANAGER  |
| JONES     | CLARK     | 20         | 10         | MANAGER  |
| BLAKE     | CLARK     | 30         | 10         | MANAGER  |
| JAMES     | ADAMS     | 30         | 20         | CLERK    |
| MILLER    | ADAMS     | 10         | 20         | CLERK    |
| SMITH     | JAMES     | 20         | 30         | CLERK    |
| ADAMS     | JAMES     | 20         | 30         | CLERK    |
| MILLER    | JAMES     | 10         | 30         | CLERK    |
| SMITH     | MILLER    | 20         | 10         | CLERK    |
| ADAMS     | MILLER    | 20         | 10         | CLERK    |
| JAMES     | MILLER    | 30         | 10         | CLERK    |
+-----------+-----------+------------+------------+----------+


​	
16、列出所有部门的详细信息和部门人数。

示例：
+--------------+-------------+-----------+-----+
| deptno         | dname      | loc      | cp  |
+--------------+-------------+-----------+-----+
| 10           | ACCOUNTING  | NEW YORK  | 3   |
| 20           | RESEARCH    | DALLAS    | 5   |
| 30           | SALES       | CHICAGO   | 6   |
| 40           | OPERATIONS  | BOSTON    | 0   |
+--------------+-------------+-----------+-----+


​	
17、列出各种工作的最低工资。

示例：
+------------+-------+
|    job     |  sal  |
+------------+-------+
| ANALYST    | 3000  |
| CLERK      | 800   |
| MANAGER    | 2450  |
| PRESIDENT  | 5000  |
| SALESMAN   | 1500  |
+------------+-------+


​	
18、列出各个部门的MANAGER（经理）的最低薪金（job为MANAGER）。

示例：

+--------+---------+-------+
| ename  | deptno  |  sal  |
+--------+---------+-------+
| CLARK  | 10      | 2450  |
| JONES  | 20      | 2975  |
| BLAKE  | 30      | 2850  |
+--------+---------+-------+


19、列出所有员工的年工资，按年薪从低到高排序。

+---------+----------+
|  ename  | yearsal  |
+---------+----------+
| SMITH   | 9600     |
| JAMES   | 11400    |
| ADAMS   | 13200    |
| MILLER  | 15600    |
| TURNER  | 18000    |
| WARD    | 21000    |
| ALLEN   | 22800    |
| CLARK   | 29400    |
| MARTIN  | 31800    |
| BLAKE   | 34200    |
| JONES   | 35700    |
| SCOTT   | 36000    |
| FORD    | 36000    |
| KING    | 60000    |
+---------+----------+