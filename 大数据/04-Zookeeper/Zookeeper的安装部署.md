# Zookeeper的安装部署

1. **集群规划**

    在hadoop102、hadoop103和hadoop104三个节点上部署Zookeeper。

2. **解压安装**

（1）解压Zookeeper安装包到/opt/module/目录下

```
[atguigu@hadoop102 software]$ tar -zxvf zookeeper-3.5.7.tar.gz -C /opt/module/
```

（2）修改/opt/module/apache-zookeeper-3.5.7-bin名称为zookeeper-3.5.7

```
[atguigu@hadoop102 module]$ mv apache-zookeeper-3.5.7-bin/ zookeeper-3.5.7
```

（3）同步/opt/module/zookeeper-3.5.7目录内容到hadoop103、hadoop104

```
[atguigu@hadoop102 module]$ xsync zookeeper-3.5.7/
```

3. **配置服务器编号**

（1）在/opt/module/zookeeper-3.5.7/这个目录下创建zkData

```
[atguigu@hadoop102 zookeeper-3.5.7]$ mkdir zkData
```

（2）在/opt/module/zookeeper-3.5.7/zkData目录下创建一个myid的文件

```
[atguigu@hadoop102 zkData]$ vi myid
```

添加myid文件，注意一定要在linux里面创建，在notepad++里面很可能乱码

在文件中添加与server对应的编号：

```
2
```

（3）拷贝配置好的zookeeper到其他机器上

```
[atguigu@hadoop102 zkData]$ xsync myid
```

并分别在hadoop103、hadoop104上修改myid文件中内容为3、4

4. **配置zoo.cfg文件**

（1）重命名/opt/module/zookeeper-3.5.7/conf这个目录下的zoo_sample.cfg为zoo.cfg

```
[atguigu@hadoop102 conf]$ mv zoo_sample.cfg zoo.cfg
```

（2）打开zoo.cfg文件

```
[atguigu@hadoop102 conf]$ vim zoo.cfg
```

​	修改数据存储路径配置

```
dataDir=/opt/module/zookeeper-3.5.7/zkData
```

​	增加如下配置

```
#######################cluster##########################
server.2=hadoop102:2888:3888
server.3=hadoop103:2888:3888
server.4=hadoop104:2888:3888
```

（3）同步zoo.cfg配置文件

```
[atguigu@hadoop102 conf]$ xsync zoo.cfg
```

（4）配置参数解读

```
server.A=B:C:D。
A是一个数字，表示这个是第几号服务器；
集群模式下配置一个文件myid，这个文件在dataDir目录下，这个文件里面有一个数据就是A的值，Zookeeper启动时读取此文件，拿到里面的数据与zoo.cfg里面的配置信息比较从而判断到底是哪个server。
B是这个服务器的地址；
C是这个服务器Follower与集群中的Leader服务器交换信息的端口；
D是万一集群中的Leader服务器挂了，需要一个端口来重新进行选举，选出一个新的Leader，而这个端口就是用来执行选举时服务器相互通信的端口。
```

5. **ZK集群启动停止脚本**

（1）在hadoop102的/home/atguigu/bin目录下创建脚本

**[atguigu@hadoop102 bin]$ vim zk.sh**

​    在脚本中编写如下内容

```shell
#!/bin/bash

case $1 in
"start"){
    for i in hadoop102 hadoop103 hadoop104
    do
        echo "------------- $i -------------"
        ssh $i "/opt/module/zookeeper-3.5.7/bin/zkServer.sh start"
    done 
};;
"stop"){
    for i in hadoop102 hadoop103 hadoop104
    do
        echo "------------- $i -------------"
        ssh $i "/opt/module/zookeeper-3.5.7/bin/zkServer.sh stop"
    done
};;
"status"){
    for i in hadoop102 hadoop103 hadoop104
    do
        echo "------------- $i -------------"
        ssh $i "/opt/module/zookeeper-3.5.7/bin/zkServer.sh status"
	done
};;
esac
```

（2）增加脚本执行权限

```
[atguigu@hadoop102 bin]$ chmod 777 zk.sh
```

（3）Zookeeper集群启动脚本

```
[atguigu@hadoop102 module]$ zk.sh start
```

（4）Zookeeper集群停止脚本

```
[atguigu@hadoop102 module]$ zk.sh stop
```

