# Hadoop开发重点

## 1完全分布式运行模式（<font color= "red">开发重点</font>）

分析：
		1）准备3 台客户机（关闭防火墙、静态ip、主机名称）
		2）安装JDK
		3）配置环境变量
		4）安装Hadoop
		5）配置环境变量
		6）配置集群
		7）单点启动
		8）配置ssh
		9）群起并测试集群

### 1.1虚拟机准备

### 1.2编写集群分发脚本xsync

1. scp（secure copy）安全拷贝

（1）scp 定义：scp 可以实现服务器与服务器之间的数据拷贝。（from server1 to server2）

（2）基本语法
scp 		-r		$pdir/$fname	 				$user@hadoop$host:$pdir/$fname
命令	递归		要拷贝的文件路径/名称	目的用户@主机:目的路径/名称

（3）实操案例

- 在hadoop101 上，将hadoop101 中/opt/module 目录下的软件拷贝到hadoop102
  上。

  `[atguigu@hadoop101 /]$ scp -r /opt/module root@hadoop102:/opt/module`

- 在hadoop103 上，将hadoop101 服务器上的/opt/module 目录下的软件拷贝到
  hadoop103 上。

  `[atguigu@hadoop103 opt]$ sudo scp -r atguigu@hadoop101:/opt/module root@hadoop103:/opt/module`

- 在hadoop103 上操作将hadoop101 中/opt/module 目录下的软件拷贝到
  hadoop104 上。

  `[atguigu@hadoop103 opt]$ scp -r atguigu@hadoop101:/opt/module root@hadoop104:/opt/module `

<font color="red">注意：拷贝过来的/opt/module 目录，别忘了在hadoop102、hadoop103、hadoop104
上修改所有文件的，所有者和所有者组</font>。`sudo chown atguigu:atguigu -R /opt/module`

- 将hadoop101 中/etc/profile 文件拷贝到hadoop102 的/etc/profile 上。
  `[atguigu@hadoop101 ~]$ sudo scp /etc/profile root@hadoop102:/etc/profile`
- 将hadoop101 中/etc/profile 文件拷贝到hadoop103 的/etc/profile 上。
  `[atguigu@hadoop101 ~]$ sudo scp /etc/profile
  root@hadoop103:/etc/profile`
- 将hadoop101 中/etc/profile 文件拷贝到hadoop104 的/etc/profile 上。
  `[atguigu@hadoop101 ~]$ sudo scp /etc/profile
  root@hadoop104:/etc/profile`
  <font color="red">注意：拷贝过来的配置文件别忘了source 一下/etc/profile.</font>

2. rsync 远程同步工具
     		rsync 主要用于备份和镜像。具有速度快、避免复制相同内容和支持符号链接的优点。
     		rsync 和scp 区别：用rsync 做文件的复制要比scp 的速度快，rsync 只对差异文件做更新。scp 是把所有文件都复制过去。

  - 基本语法
    rsync    -rvl    		$pdir/$fname		 		$user@hadoop$host:$pdir/$fname
    命令    选项参数	要拷贝的文件路径/名称	目的用户@主机:目的路径/名称
  - 案例实操
    （a）把hadoop101 机器上的/opt/software 目录同步到hadoop102 服务器的root 用户下的/opt/目录
    `[atguigu@hadoop101 opt]$ rsync -rvl /opt/software/
    root@hadoop102:/opt/software`

3. xsync 集群分发脚本

（1）需求：循环复制文件到所有节点的相同目录下

（2）需求分析：

（a）rsync 命令原始拷贝：

`rsync -rvl /opt/module root@hadoop103:/opt/`
（b）期望脚本：
xsync 要同步的文件名称
（c）说明：在/home/atguigu/bin 这个目录下存放的脚本，atguigu 用户可以在系统
任何地方直接执行。
（3）脚本实现

- （a）在/home/atguigu 目录下创建bin 目录，并在bin 目录下xsync 创建文件，文件
  内容如下：

`[atguigu@hadoop102 ~]$ vim bin xsync.sh`

在该文件中编写如下代码

```shell
#!/bin/bash
#1 获取输入参数个数，如果没有参数，直接退出
pcount=$#
if((pcount==0)); then
echo no args;
exit;
fi
#2 获取文件名称
p1=$1
fname=`basename $p1`
echo fname=$fname
#3 获取上级目录到绝对路径
pdir=`cd -P $(dirname $p1); pwd`
echo pdir=$pdir
#4 获取当前用户名称
user=`whoami`
#5 循环
for((host=103; host<105; host++)); do
	echo ------------------- hadoop$host --------------
	rsync -rvl $pdir/$fname $user@hadoop$host:$pdir
done
```

- （b）修改脚本xsync 具有执行权限
  `[atguigu@hadoop102 bin]$ chmod 777 xsync`

- （c）调用脚本形式：xsync 文件名称
  `[atguigu@hadoop102 bin]$ xsync /home/atguigu/bin`

  注意：如果将xsync放到/home/atguigu/bin目录下仍然不能实现全局使用，可以将xsync移动到/usr/local/bin 目录下。

### 1.3集群配置

1. 集群部署规划

|      | hadoop101               | hadoop102                       | hadoop103                     |
| ---- | ----------------------- | ------------------------------- | ----------------------------- |
| HDFS | Namenode  <br> Datanode | <br>Datanode                    | SecondaryNamenode<br>Datanode |
| YARn | <br>NodeManager         | ResourceManager<br/>NodeManager | <br>NodeManager               |

2. 配置集群

（1）核心配置文件
配置core-site.xml
`[atguigu@hadoop102 hadoop]$ vi core-site.xml`
在该文件中编写如下配置

```
<!-- 指定HDFS 中NameNode 的地址-->
<property>
	<name>fs.defaultFS</name>
	<value>hdfs://hadoop102:9000</value>
</property>
	<!-- 指定Hadoop 运行时产生文件的存储目录-->
<property>
	<name>hadoop.tmp.dir</name>
	<value>/opt/module/hadoop-2.7.2/data/tmp</value>
</property>
```

（2）HDFS 配置文件
配置hadoop-env.sh
`[atguigu@hadoop102 hadoop]$ vi hadoop-env.sh`
`export JAVA_HOME=/opt/module/jdk1.8.0_144`
配置hdfs-site.xml
`[atguigu@hadoop102 hadoop]$ vi hdfs-site.xml`
在该文件中编写如下配置

```
<property>
	<name>dfs.replication</name>
	<value>3</value>
</property>
<!-- 指定Hadoop 辅助名称节点主机配置-->
<property>
	<name>dfs.namenode.secondary.http-address</name>
	<value>hadoop104:50090</value>
</property>
```

（3）YARN 配置文件
配置yarn-env.sh
`[atguigu@hadoop102 hadoop]$ vi yarn-env.sh`
`export JAVA_HOME=/opt/module/jdk1.8.0_144`
配置yarn-site.xml
`[atguigu@hadoop102 hadoop]$ vi yarn-site.xml`
在该文件中增加如下配置

```
<!-- Reducer 获取数据的方式-->
<property>
	<name>yarn.nodemanager.aux-services</name>
	<value>mapreduce_shuffle</value>
</property>
<!-- 指定YARN 的ResourceManager 的地址-->
<property>
	<name>yarn.resourcemanager.hostname</name>
	<value>hadoop103</value>
</property>
```

（4）MapReduce 配置文件
配置mapred-env.sh
`[atguigu@hadoop102 hadoop]$ vi mapred-env.sh`
`export JAVA_HOME=/opt/module/jdk1.8.0_144`
配置mapred-site.xml
`[atguigu@hadoop102 hadoop]$ cp mapred-site.xml.template
mapred-site.xml`
`[atguigu@hadoop102 hadoop]$ vi mapred-site.xml`

在该文件中增加如下配置

```
<!-- 指定MR 运行在Yarn 上-->
<property>
	<name>mapreduce.framework.name</name>
	<value>yarn</value>
</property>
```

3．在集群上分发配置好的Hadoop 配置文件 <font color = "red">(这里同步hadoop文件夹就可以)</font>
`[atguigu@hadoop102 hadoop]$ xsync /opt/module/hadoop-2.7.2/`
4．查看文件分发情况
`[atguigu@hadoop103 hadoop]$ cat /opt/module/hadoop-
2.7.2/etc/hadoop/core-site.xml`

### 1.4 集群单点启动

### 1.5 SSH 无密登录配置

1. 配置ssh
   （1）基本语法
   ssh 另一台电脑的ip 地址

2. 无密钥配置

   在hadoop102上生成私钥和公钥

   `[atguigu@hadoop102 .ssh]$ ssh-keygen -t rsa`

   然后敲（三个回车），就会生成两个文件id_rsa（私钥）、id_rsa.pub（公钥）

   将公钥拷贝到要免密登录的目标机器上

   `[atguigu@hadoop102 .ssh]$ ssh-copy-id hadoop102
   [atguigu@hadoop102 .ssh]$ ssh-copy-id hadoop103
   [atguigu@hadoop102 .ssh]$ ssh-copy-id hadoop104`

   <font color = "red">注意：这里生成的秘钥文件是存在atguigu用户下的bin目录下的（.ssh是隐藏文件）。
   还需要在hadoop102 上采用root 账号，配置一下无密登录到hadoop102、hadoop103、hadoop104；
   还需要在hadoop103 上采用atguigu账号配置一下无密登录到hadoop102、hadoop103、hadoop104 服务器上。</font>

3. .ssh 文件夹下（~/.ssh）的文件功能解释

   | 文件            | 解释                               |
   | --------------- | ---------------------------------- |
   | known_hosts     | 记录素数访问过计算机的公钥         |
   | id_rsa          | 生成的私钥                         |
   | id_rsa.pub      | 生成的公钥                         |
   | authorized_keys | 存放授权过的无秘登入服务器端的秘钥 |

### 1.6群起集群

1. 配置slaves

   `/opt/module/hadoop-2.7.2/etc/hadoop/slaves
   [atguigu@hadoop102 hadoop]$ vi slaves`

   在该文件中增加如下内容：
   `hadoop102
   hadoop103
   hadoop104`

   <font color = "red">注意：该文件中添加的内容结尾不允许有空格，文件中不允许有空行。</font>

   同步所有节点配置文件

   `[atguigu@hadoop102 hadoop]$ xsync slaves`

2. 启动集群

   （1）如果集群是第一次启动，需要格式化NameNode（<font color = "red">注意格式化之前，一定要先停
   止上次启动的所有namenode 和datanode 进程，然后再删除data 和log 数据</font>）

   `[atguigu@hadoop102 hadoop-2.7.2]$ bin/hdfs namenode -format`

   `[atguigu@hadoop102 hadoop-2.7.2]$ sbin/start-dfs.sh`

   （2）启动HDFS

   `[atguigu@hadoop102 hadoop-2.7.2]$ sbin/start-dfs.sh`

   （3）启动YARN

   `[atguigu@hadoop103 hadoop-2.7.2]$ sbin/start-yarn.sh`

   （4）Web 端查看SecondaryNameNode

3. 集群基本测试

   （1）上传文件到集群

   （2）上传文件后查看文件存放在什么位置

   ​		/opt/module/hadoop-2.7.2/data/tmp/dfs/data/current/BP-938951106-192.168.10.107-1495462844069/current/finalized/subdir0/subdir0

### 1.7 集群启动/停止方式总结

1. 各个服务组件逐一启动/停止
   （1）分别启动/停止HDFS 组件
   `hadoop-daemon.sh start / stop namenode / datanode / secondarynamenode`
   （2）启动/停止YARN
   `yarn-daemon.sh start / stop resourcemanager / nodemanager`
2. 各个模块分开启动/停止（配置ssh 是前提）常用
   （1）整体启动/停止HDFS
   `start-dfs.sh / stop-dfs.sh`
   （2）整体启动/停止YARN
   `start-yarn.sh / stop-yarn.sh`