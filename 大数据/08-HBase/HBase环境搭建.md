# HBase环境搭建

1. 文件上传解压

2. 修改环境变量

3. 修改配置文件==conf==目录下

    - ==hbase-env.sh==添加如下内容，作用不使用HBase自带的ZK

        ```
        export HBASE_MANAGES_ZK=false
        ```

    - ==hbase-site.xml==`<configuration>`标签内添加如下内容：

        ```xml
        <property>
            <name>hbase.rootdir</name>
            <value>hdfs://hadoop102:8020/hbase</value>
        </property>
        <property>
            <name>hbase.cluster.distributed</name>
            <value>true</value>
        </property>
        <property>
            <name>hbase.zookeeper.quorum</name>
            <value>hadoop102,hadoop103,hadoop104</value>
        </property>
        <property>
            <name>hbase.unsafe.stream.capability.enforce</name>
            <value>false</value>
        </property>
        <property>
            <name>hbase.wal.provider</name>
            <value>filesystem</value>
        </property>
        
        ```

    - ==regionservers==添加从机节点

        ```
        hadoop102
        hadoop103
        hadoop104
        ```

4. 软连接hadoop配置文件到HBase（*可以不配置*）：

    ```
    [atguigu@hadoop102 module]$ ln -s /opt/module/hadoop-3.1.3/etc/hadoop/core-site.xml /opt/module/hbase/conf/core-site.xml
    [atguigu@hadoop102 module]$ ln -s /opt/module/hadoop-3.1.3/etc/hadoop/hdfs-site.xml /opt/module/hbase/conf/hdfs-site.xml
    ```

5. HBase远程发送到其他集群

    ```
    [atguigu@hadoop102 module]$ xsync hbase/
    ```

6. HBase服务的启动

    - ```
        [atguigu@hadoop102 hbase]$ bin/hbase-daemon.sh start master
        [atguigu@hadoop102 hbase]$ bin/hbase-daemon.sh start regionserver
        ```

    - 群起群关：

        ```
        start-hbase.sh
        stop-hbase.sh
        ```

7. 解决jar包冲突

    在103,104上删除jar包

    ```
    [atguigu@hadoop103 ~]$ rm -rf /opt/module/hbase/logs/hbase-atguigu-master-hadoop102.out
    [atguigu@hadoop104 ~]$ rm -rf /opt/module/hbase/logs/hbase-atguigu-master-hadoop102.out
    ```

**注意**

- 集群间时间必须同步，否则会启动报错
- 依赖ZK和HDFS,且HDFS不能处于安全模式

8. 高可用(可选)

    - 关闭HBase集群（如果没有开启则跳过此步）

    ```
    [atguigu@hadoop102 hbase]$ bin/stop-hbase.sh
    ```

    - 在conf目录下创建backup-masters文件

    ```
    [atguigu@hadoop102 hbase]$ touch conf/backup-masters
    ```

    - 在backup-masters文件中配置高可用HMaster节点

    ```
    [atguigu@hadoop102 hbase]$ echo hadoop103 > conf/backup-masters
    ```

    - 将整个conf目录scp到其他节点

    ```
    [atguigu@hadoop102 hbase]$ scp -r conf/ hadoop103:/opt/module/hbase/
    
    [atguigu@hadoop102 hbase]$ scp -r conf/ hadoop104:/opt/module/hbase/
    ```

    - 打开页面测试查看

    [http://hadooo102:16010](http://linux01:16010) 

