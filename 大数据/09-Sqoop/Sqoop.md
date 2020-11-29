# Sqoop

# 1 Sqoop简介

​		Sqoop是一个数据的导入导出的工具，可以将一个关系型数据库（例如：MySQL ,Oracle ,Postgres 等）中的数据导进到Hadoop 的HDFS 中，也可以将HDFS 的数据导进到关系型数据库中。

​		导入导出的概念是基于大数据集群的，从大数据集群（HDFS，Hive，HBase）中导出数据叫导出（export），从非大数据集群（RDBMS）导入数据到大数据集群称为导入（import）。

# 2 Sqoop原理

​		将导入或导出命令翻译成mapreduce 程序来实现。
​		在翻译出的mapreduce 中主要是对inputformat 和outputformat 进行定制。

# 3 Sqoop 安装

# 4 Sqoop 的简单使用案例

## 4.1 导入数据

### 4.1.1 RDBMS 到HDFS

​		import，将数据从非大数据集群导入到大数据集群中，

- 将mysql数据库中的某个表中的全部数据导入到hdfs文件中
- 通过查询将表中的部分数据导入到hdfs文件中
- 指定列将数据到入hdfs文件中

### 4.1.2 RDBMS 到Hive

​		提示：该过程分为两步，第一步将数据导入到HDFS，第二步将导入到HDFS 的数据迁移到Hive 仓库，第一步默认的临时目录是/user/atguigu/表名

### 4.1.3 RDBMS 到Hbase

​		sqoop1.4.6 只支持HBase1.0.1 之前的版本的自动创建HBase 表的功能

## 4.2 导出数据

### 4.2.1 HIVE/HDFS 到RDBMS

提示：Mysql 中如果表不存在，不会自动创建

## 4.3 脚本打包

# 5 Sqoop 一些常用命令及参数