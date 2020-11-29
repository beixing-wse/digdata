# Spark Bug合集

## jar包提交集群

报错信息：

```
Exception in thread "main" java.lang.RuntimeException: Error in configuring object

............

Caused by: java.lang.reflect.InvocationTargetException
at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
at java.lang.reflect.Method.invoke(Method.java:498)
at org.apache.hadoop.util.ReflectionUtils.setJobConf(ReflectionUtils.java:109)
... 48 more
Caused by: java.lang.IllegalArgumentException: Compression codec com.hadoop.compression.lzo.LzoCodec not found.

...............
```

**原因：**

在hadoop的core-site.xml 和mapred-site.xml中开启了压缩，并且压缩式lzo的。这就导致写入/上传到hdfs的文件自动被压缩为lzo了

**解决：**

spark-env.sh中

配置SPARK_LIBRARY_PATH添加hadoop的native

配置SPARK_CLASSPATH添加Hadoop的lzo

```
export SPARK_LIBRARY_PATH=$SPARK_LIBRARY_PATH:/opt/module/hadoop-3.1.3/lib/native
export SPARK_CLASSPATH=$SPARK_CLASSPATH:/opt/module/hadoop-3.1.3/share/hadoop/common/hadoop-lzo-0.4.20.jar
```

