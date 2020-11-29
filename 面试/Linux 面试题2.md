[TOC]

#### 01、Linux 常用的命令？

|                             描述                             |                             命令                             |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
|                   绝对路径用什么符号表示？                   |                       如 `/etc/init.d`                       |
|                当前目录、上层目录用什么表示？                |                         `./` 和`../`                         |
|                      主目录用什么表示?                       |                             `~/`                             |
|                     切换目录用什么命令？                     |                             `cd`                             |
| 复制文件用什么命令？<br />如果需要连同文件夹一块复制呢？<br />如果需要有提示功能呢？ |                    `cp`、`cp -r`、`cp -i`                    |
|                      怎么查看当前进程？                      |                             `ps`                             |
|                        怎么执行退出？                        |                            `exit`                            |
|                      怎么查看当前路径？                      |                            `pwd`                             |
|                     查看用过的命令列表?                      |                          `history`                           |
|                          怎么清屏？                          |                           `clear`                            |
|                     目录创建用什么命令？                     |                           `mkdir`                            |
|                     创建文件用什么命令？                     | 典型的如 `touch`，`vi` 及 `vim` 也可以创建文件，<br />其实只要向一个不存在的文件输出，都会创建文件 |
|             移动文件用哪个命令？改名用哪个命令？             |                             `mv`                             |
|                   删除空文件夹用什么命令？                   |                           `rmdir`                            |
|                      怎么退出当前命令？                      |                      `ctrl+c` 彻底退出                       |
|                        怎么执行睡眠？                        |             `ctrl+z` 挂起当前进程 `fg` 恢复后台              |
|                    怎么查看当前用户 id？                     |  `id `查看显示目前登陆账户的 ==uid== 和 ==gid== 及所属分组   |
|                   查看指定帮助用什么命令？                   | `man`查看指定帮助： 如 ==man adduser==<br />`--help`这个很全 而且有例子； ==adduser --help==<br />`info` 这个告诉你一些常用参数；==info adduesr== |
|            挂载用什么命令？<br />卸载用什么命令？            |    `mount 设备块 挂载目录`<br />`umount 设备块 挂载目录`     |
|             使用什么命令查看 ip 地址及接口信息？             |                          `ifconfig`                          |
|                一个给其他命令传递参数的过滤器                |                           `xargs`                            |
|                   linux 远程访问用哪个命令                   |                  `ssh 远程主机域名/IP地址`                   |

> **Linux 后台运行和关闭程序、查看后台任务**
>
> ​       `fg、bg、jobs、&、ctrl+z` 都是跟系统任务有关的，虽然现在基本上不怎么需要用到这些命令，但学会了也是很实用的。
>
> 1. ==&==：这个用在一个命令的最后，可以把这个命令放到后台执行；
> 2. ==ctrl + z==：可以将一个正在前台执行的命令放到后台，并且暂停；
> 3. ==jobs==：查看当前有多少在后台运行的命令；
>    * `-l`：显示进程号；
>    * `-p`：仅任务对应的显示进程号；
>    * `-n`：显示任务状态的变化；
>    * `-r`：仅输出运行状态（running）的任务；
>    * `-s`：仅输出停止状态（stoped）的任务。
> 4. ==fg==： 将后台中的命令调至前台继续运行，如果后台中有多个命令，可以用 `fg %jobnumber` 将选中的命令调出，`%jobnumber` 是通过 `jobs` 命令查到的后台正在执行的命令的序号（不是 pid）
> 5. ==bg==：将一个在后台暂停的命令，变成继续执行。如果后台中有多个命令，可以用 `bg %jobnumber `将选中的命令调出，`%jobnumber` 是通过 `jobs` 命令查到的后台正在执行的命令的序号（不是pid）



#### 02、Linux 常用的高级命令？

| 序号 |              命令               |                     命令解释                     |
| :--: | :-----------------------------: | :----------------------------------------------: |
|  1   |              `top`              | 用于实时显示 process 的动态，如内存使用、CPU占用 |
|  2   |             `df -h`             |                 查看磁盘存储情况                 |
|  3   |             `iotop`             |   查看磁盘IO读写（==yum install iotop安装==）    |
|  4   |           `iotop -o`            |           直接查看比较高的磁盘读写程序           |
|  5   | `netstat -tunlp \| grep 端口号` |              查看网络端口号占用情况              |
|  6   |            `uptime`             |          查看报告系统运行时长及平均负载          |
|  7   |            `ps -aux`            |                     查看进程                     |
|  8   |             `jobs`              |          查看当前有多少在后台运行的命令          |
|  9   |           `free -mh`            |         查看内存使用率，并用兆字节显示？         |
|  10  |           `fdisk -l`            |                列出磁盘分区表信息                |
|  11  |            `tail -f`            |             实时追踪该文档的所有更新             |
|  12  |             `lsblk`             |                  列出块设备信息                  |



#### 03、VI 常用命令

| 序号 |         描述         |                      命令                       |
| :--: | :------------------: | :---------------------------------------------: |
|  1   | vim 快捷键到最后一行 |                       `G`                       |
|  2   |       批量替换       | `: %s/old 字符/new` 字符 如 ==:%s /read/write== |
|  3   |       删除4行        |                      `4dd`                      |
|  4   |         粘贴         |                       `p`                       |



#### 04、netstat 可以查询哪两种状态，分别有什么不同？

查询出来的状态有==网络状态==以及==端口状态== 两种。

* `网络状态（netstat -ntulp）`：可以查看服务所采用的协议，以及时时监护服务的流量走向、网络速度，给用户准确的实时网络状态。
* `端口状态（netstat  -anp | grep  端口号）`： 查看所有的服务端口并显示对应的服务程序名。

> 　　在`linux`一般使用`netstat`来查看==系统端口使用情况==。`netstat`命令是一个监控==TCP/IP网络==的非常有用的工具，它可以显示==网络连接、路由表和网络接口信息==，可以让用户得知目前都有哪些网络连接正在运作。
>
> * `-t`：显示TCP协议的连接情况。
> * `-u`：显示UDP协议的连接情况。
> * `-n`：以网络 IP 地址代替名称，显示出网络连接情形。
> * `-l, --listening`：只显示正在侦听的套接字(这是默认的选项)
> * `-p, --program`：显示套接字所属进程的 PID 和名称。
> * `-a`： 显示所有socket，包括正在监听的。



#### 05、Ls 命令执行什么功能？ 可以带哪些参数，有什么区别？

ls 执行的功能： 列出指定目录中的目录，以及文件

哪些参数以及区别： 

| 选项  |                             功能                             |
| :---: | :----------------------------------------------------------: |
| `-a ` |  全部的文件，连同隐藏档( 开头为 . 的文件) 一起列出来(常用)   |
| `-A`  |                   不包含当前目录和上级目录                   |
| `-l`  | 详细信息，长数据串列出，包含文件的属性与权限等等数据； (常用) |
| `-i`  |   输出文件前先输出文件系列号（即 i 节点号: i-node number）   |



#### 06、建立软链接(快捷方式)，以及硬链接的命令。

软链接：`ln -s slinksource`

硬链接：`ln link source`

> [“软链接”和“硬链接”的区别](https://www.linuxprobe.com/soft-and-hard-links.html)



#### 07、文件权限修改用什么命令？格式是怎么样的？

文件权限修改： `chmod`

格式如下：

![chmode](I:\课程\1 笔记\1.4 Markdown\(1) 计算机科学与技术\【3】大数据\Linux\img\chmode.png)

`u`：所有者、`g`：所有组、`o`：其他人、`a`：所有人(u、 g、 o 的总和)

r=4 w=2 x=1 rwx=4+2+1=7

==第一种方式变更权限==：`chmod [{ugoa}{+-=}{rwx}] 文件或目录`

==第二种方式变更权限==：`chmod [mode=421 ] [文件或目录]  `



#### 08、查看文件内容有哪些命令可以使用？

1. `vi或vim 文件名`：编辑方式查看，可修改；
2. `cat 文件名`：显示全部文件内容；
3. `more 文件名`：分页显示文件内容；
4. `less 文件名`：与 more 相似，更好的是可以往前翻页；
5. `tail 文件名`：仅查看尾部，还可以指定行数；
6. `head 文件名`：仅查看头部,还可以指定行数；



#### 09、随意写文件命令？怎么向屏幕输出带空格的字符串，比如 hello world?

写文件命令：`vi 或 vim`

向屏幕输出带空格的字符串：`echo hello world`



#### 10、终端是哪个文件夹下的哪个文件？黑洞文件是哪个文件夹下的哪个文件？

终端文件：`/dev/tty`

黑洞文件：`/dev/null`

> ​		**黑洞文件**：在许多操作系统中， `/dev/null` 是一个空设备，是一个抛弃向该文件中写的所有数据并反馈写操作成功的设备文件。`/dev/null` 通常用来处理==进程中那些不想要的输出流==，或者作为一个方便的空文件输入流。这个通过用来做重定向。
>
> ​		`/dev/null` 设备是一个特殊的文件，而不是一个路径。因此不能通过 `mv` 命令来移动一个文件或路径进入这个设备文件，`rm` 命令是 `Unix` 系统中删除文件适当的方法。



#### 11、Linux 下命令有哪几种可使用的通配符？分别代表什么含义?

* **?**：可替代单个字符。
* **\\**：转义字符
* *****：可替代任意多个字符。
* **~**：表示当前用户的$HOME 目录
* **[]**：方括号可替代 charset 集中的任何单个字符，如 ==[a-z]，[abABC]==

> **[] 使用分析**
>
> ```shell
> [topcloud@hadoop101 teset]$ ll 
> 总用量 0
> -rw-rw-r--. 1 topcloud topcloud 0 10月 26 10:26 a
> -rw-rw-r--. 1 topcloud topcloud 0 10月 26 10:25 aa
> -rw-rw-r--. 1 topcloud topcloud 0 10月 26 10:26 ab
> -rw-rw-r--. 1 topcloud topcloud 0 10月 26 10:26 abc
> -rw-rw-r--. 1 topcloud topcloud 0 10月 26 10:26 ac
> -rw-rw-r--. 1 topcloud topcloud 0 10月 26 10:26 b
> -rw-rw-r--. 1 topcloud topcloud 0 10月 26 10:25 bb
> -rw-rw-r--. 1 topcloud topcloud 0 10月 26 10:26 bc
> -rw-rw-r--. 1 topcloud topcloud 0 10月 26 10:25 c
> -rw-rw-r--. 1 topcloud topcloud 0 10月 26 10:25 cc
> 
> [topcloud@hadoop101 teset]$ ll [a]
> -rw-rw-r--. 1 topcloud topcloud 0 10月 26 10:26 a
> 
> [topcloud@hadoop101 teset]$ ll [a]*
> -rw-rw-r--. 1 topcloud topcloud 0 10月 26 10:26 a
> -rw-rw-r--. 1 topcloud topcloud 0 10月 26 10:25 aa
> -rw-rw-r--. 1 topcloud topcloud 0 10月 26 10:26 ab
> -rw-rw-r--. 1 topcloud topcloud 0 10月 26 10:26 abc
> -rw-rw-r--. 1 topcloud topcloud 0 10月 26 10:26 ac
> 
> [topcloud@hadoop101 teset]$ ll [a]c
> -rw-rw-r--. 1 topcloud topcloud 0 10月 26 10:26 ac
> 
> [topcloud@hadoop101 teset]$ ll [a]??
> -rw-rw-r--. 1 topcloud topcloud 0 10月 26 10:26 abc
> ```



#### 12、用什么命令对一个文件的内容进行统计？(行号、单词数、字节数)

**命令**：`wc [参数] 文件名`

**参数**： `-c` 统计==字节数==，`-l` 统计==行数==，`-w` 统计==字数==。



#### 13、Grep 命令有什么用？ 如何忽略大小写？ 如何查找不含该串的行?

1. `Grep` 全称是 ==Global Regular Expression Print==，表示 ==全局正则表达式打印==，它的使用权限是所有用户，它是一种强大的文本搜索工具，它能使用正则表达式搜索文本，并把匹配的行打印出来。
2. `-i`：不区分大小写（只适用于单字符）；
3. `-v`：显示不包含匹配文本的所有行；



#### 14、Linux 中进程有哪几种状态？在 ps 显示出来的信息中，分别用什么符号表示的？

1. `R (TASK_RUNNING)`，==可执行状态==。只有在该状态的进程才可能在CPU上运行。而同一时刻可能有多个进程处于可执行状态，这些进程的task_struct结构（进程控制块）被放入对应CPU的可执行队列中（一个进程最多只能出现在一个CPU的可执行队列中）。进程调度器的任务就是从各个CPU的可执行队列中分别选择一个进程在该CPU上运行。
2. `T (TASK_STOPPED or TASK_TRACED)`，==暂停状态或跟踪状态==。向进程发送一个 SIGSTOP 信号，它就会因响应该信号 而进入 TASK_STOPPED 状态;当进程正在被跟踪时，它处于 TASK_TRACED 这个特殊的状态。正被跟踪”指的是进程暂停下来，等待跟踪它的进程对它进行操作。
3. `S (TASK_INTERRUPTIBLE)`，==可中断的睡眠状态==。处于这个状态的进程因为等待某某事件的发生（比如等待 socket 连接、等待信号量），而被挂起。
4. `D (TASK_UNINTERRUPTIBLE)`，==不可中断的睡眠状态==。进程处于睡眠状态，但是此刻进程是不可中断的。不可中断，指进程不响应异步信号。
5. `Z (TASK_DEAD - EXIT_ZOMBIE)`，==退出状态，进程成为僵尸进程==。在一个进程调用了exit之后，该进程 并非马上就消失掉，而是留下一个称为僵尸进程（Zombie）的数据结构。在Linux进程的5种状态中，僵尸进程是非常特殊的一种，它已经放弃了几乎所 有内存空间，没有任何可执行代码，也不能被调度，仅仅在进程列表中保留一个位置，记载该进程的退出状态等信息供其他进程收集，除此之外，僵尸进程不再占有 任何内存空间。
6. `X (TASK_DEAD - EXIT_DEAD)`，==退出状态，进程即将被销毁==。

> **补充：ps 信息中其他符号的含义**
>
> * `W`，进入内存交换（从内核 2.6 开始无效）
> * `s`，==包含子进程==
> * `+`，位于后台



#### 15、怎么使一个命令在后台运行?

1. 一般都是使用 ==&== 在命令结尾来让程序自动运行。(命令后可以不追加空格)
2. 先==ctrl + z==这样可以将一个正在前台执行的命令放到后台，并且暂停；再使用==bg==，将一个在后台暂停的命令，变成继续执行。



#### 16、利用 ps 怎么显示所有的进程? 怎么利用 ps 查看指定进程的信息？

`ps -aux | grep 进程号`（功能描述：查看系统中所有进程）

`ps -ef | grep 进程号`（功能描述： 可以查看子父进程之间的关系）

| 选项 |          功能          |
| :--: | :--------------------: |
|  -a  |      选择所有进程      |
|  -u  | 显示所有用户的所有进程 |
|  -x  |   显示没有终端的进程   |



#### 17、把后台任务调到前台执行使用什么命令?把停下的后台任务在后台执行起来用什么命令?

把后台任务调到前台执行 `fg`

把停下的后台任务在后台执行起来 `bg`



#### 18、终止进程用什么命令? 带什么参数?

kill 命令发送信号给进程

* `kill -9 pid`，是不顾后果的强制终止 （功能描述：通过进程号杀死进程）。
* `kill -15 pid`，是先关闭和其有关的程序，再将其关闭。
* `killall 进程名称`（功能描述：通过进程名称杀死进程，也支持通配符，这在系统因负载过大而变得很慢时很有用）。

> `ctrl+c` 通常是终止当前在终端窗口中运行的命令或脚本。



#### 19、怎么查看系统支持的所有信号？

`kill -l`

![kill-l](I:\课程\1 笔记\1.4 Markdown\(1) 计算机科学与技术\【3】大数据\Linux\img\kill-l.png)



#### 20、搜索文件用什么命令? 格式是怎么样的?

1. `find <指定目录> <指定条件> <指定动作>`：如 ==find / -name "string*"==，直接搜索磁盘，较慢。
   * `-name<查询方式>`：按照指定的文件名查找模式查找文件。
   * `-user<用户名>`：查找属于指定用户名所有文件。
   * `-size<文件大小>`：按照指定的文件大小查找文件。
2. `whereis`：加参数与文件名。该指令只能用于查找==二进制文件、源代码文件和man手册页==，一般文件的定位需使用 locate 命令。
3. `locate`：只加文件名。第一次运行前，必须使用 updatedb 指令创建 locate 数据库。



#### 21、查看当前谁在使用该主机用什么命令? 查找自己所在的终端信息用什么命令?

查看当前谁在使用该主机：`whoami`

查找自己所在的终端信息：`who`或者`who am i`

```shell
[topcloud@hadoop101 ~]$ whoami
topcloud

[topcloud@hadoop101 ~]$ who
topcloud pts/0        2020-10-26 15:48 (192.168.10.1)

[topcloud@hadoop101 ~]$ who am i
topcloud pts/0        2020-10-26 15:48 (192.168.10.1)
```



#### 22、使用什么命令查看磁盘的使用空间以及空闲空间呢?

`df -hl`

* `-h`：用常见的格式显示出大小（例如:1K 234M 2G）
* `-l`：只显示本地文件系统使用状况

```shell
[topcloud@hadoop101 ~]$ df -lh
文件系统                 容量  已用  可用 已用% 挂载点
/dev/mapper/centos-root   47G  6.3G   41G   14% /
devtmpfs                 975M     0  975M    0% /dev
tmpfs                    992M     0  992M    0% /dev/shm
tmpfs                    992M   10M  982M    2% /run
tmpfs                    992M     0  992M    0% /sys/fs/cgroup
/dev/sda1               1014M  157M  858M   16% /boot
tmpfs                    199M     0  199M    0% /run/user/1000
```



#### 23、使用什么命令查看网络是否连通?使用什么命令查看 ip 地址及接口信息？

1. `ping`
2. `ifconfig` 或者 `ip addr` 或者 `ip addr show`



#### 24、查看各类环境变量用什么命令?

查看所有环境变量信息 `env`

查看某个环境变量信息，如 ==home==，则为 `env $HOME`



#### 25、通过什么命令指定命令提示符?

通过该命令 `export PS1='[\u@\h \w]\$'`，可实现命令提示符的修改。

* `\u`：显示当前用户账号
* `\h`：显示当前主机名
* ` \W`：只显示当前路径最后一个目录
* `\w`：显示当前绝对路径（当前用户目录会以~代替）
* ` $PWD`：显示当前全路径
* `$`：显示命令行’$'或者’#'符号
* ` #`：下达的第几个命令
* ` \d`：代表日期，格式为 week day month date，例如："MonAug1"
* ` \t`：显示时间为 24 小时格式，如：HH：MM：SS
* ` \T`：显示时间为 12 小时格式
* ` \A`：显示时间为 24 小时格式：HH：MM
* `\v`：BASH 的版本信息 

> **案例补充**
>
> ```shell
> # 在 /etc/profile.d 中创建文件执行文件 myprofile.sh，并设为可执行
> [topcloud@hadoop101 profile.d]$ vim myprofile.sh
> # 写入该脚本后，命令行提示符显示完整工作目录，当前用户目录会以 ~代替：
> export PS1='[\u@\h \w]\$'
> 
> # 重新加载该配置文件
> [topcloud@hadoop101 profile.d]$ source myprofile.sh
> 
> # 设置完后可发现当前显示的目录已经发生改变
> [topcloud@hadoop101 /etc/profile.d]$cd
> 
> # 家目录还是 ~
> [topcloud@hadoop101 ~]$cd /
> ```



#### 26、查找命令的可执行文件是去哪查找命令的? 怎么对其进行设置及添加?

`whereis [-bfmsu][-B <目录>…][-M <目录>…][-S <目录>…][文件…]`

**补充说明**：`whereis` 指令会在==特定目录==中查找符合条件的文件。这些文件的烈性应属于原始代码，二进制文件，或是帮助文件。

```shell
-b   只查找二进制文件。
-B<目录> 只在设置的目录下查找二进制文件。 -f 不显示文件名前的路径名称。
-m   只查找说明文件。
-M<目录> 只在设置的目录下查找说明文件。 -s 只查找原始代码文件。
-S<目录> 只在设置的目录下查找原始代码文件。 -u 查找不包含指定类型的文件。
which 指令会在 PATH 变量指定的路径中，搜索某个系统命令的位置，并且返回第一个搜索结果。
-n 指定文件名长度，指定的长度必须大于或等于所有文件中最长的文件名。
-p 与-n 参数相同，但此处的包括了文件的路径。 -w 指定输出时栏位的宽度。
-V   显示版本信息
```

> **案例**
>
> ```shell
> # 查找 jps 命令
> [topcloud@hadoop101 /etc/profile.d]$whereis jps
> jps: /opt/module/jdk1.8.0_212/bin/jps
> 
> # 让它去指定目录 /etc 查找 jps 命令，则没找到
> [topcloud@hadoop101 /etc/profile.d]$whereis -B /etc jps
> ```



#### 27、通过什么命令可以查找执行命令?

`which` 只能查可执行文件。

`whereis` 只能查二进制文件、说明文档，源文件等。



#### 28、怎么对命令进行取别名？

```shell
[topcloud@hadoop101 ~]$ la
bash: la: 未找到命令...

# alias la='ls -a' 命令，可实现取别名
[topcloud@hadoop101 ~]$ alias la='ls -a'
[topcloud@hadoop101 ~]$ la
.              .bash_logout   bin     .config    .ICEauthority  .pki      模板  文档  桌面
..             .bash_profile  .cache  .dbus      .local         .viminfo  视频  下载
.bash_history  .bashrc        calc    .esd_auth  .mozilla       公共      图片  音乐
```



#### 29、du 和 df 的定义，以及区别？

* `du`：显示目录或文件的大小。

```shell
[topcloud@hadoop101 ~]$du -ch --max-depth=1 ~
0	/home/topcloud/.mozilla
3.5M	/home/topcloud/.cache
4.0K	/home/topcloud/.dbus
104K	/home/topcloud/.config
300K	/home/topcloud/.local
0	/home/topcloud/桌面
0	/home/topcloud/下载
0	/home/topcloud/模板
0	/home/topcloud/公共
0	/home/topcloud/文档
0	/home/topcloud/音乐
0	/home/topcloud/图片
0	/home/topcloud/视频
4.0K	/home/topcloud/bin
0	/home/topcloud/.pki
3.9M	/home/topcloud
3.9M	总用量
```

* `df`：显示每个 <文件> 所在的文件系统的信息，默认是显示所有文件系统。
  * `-m`：以指定块大小等于 1048576 字节（1M） 来显示使用状况。
  * `-h`：用常见的格式显示出大小（例如:1K 234M 2G）。
  * `-l`：只显示本地文件系统使用状况。

```shell
[topcloud@hadoop101 ~]$df -l
文件系统                   1K-块    已用     可用 已用% 挂载点
/dev/mapper/centos-root 49250820 6569384 42681436   14% /
devtmpfs                  997948       0   997948    0% /dev
tmpfs                    1015084       0  1015084    0% /dev/shm
tmpfs                    1015084   10120  1004964    1% /run
tmpfs                    1015084       0  1015084    0% /sys/fs/cgroup
/dev/sda1                1038336  160460   877876   16% /boot
tmpfs                     203020       0   203020    0% /run/user/1000
```

**区别**： `du` 命令只查看==文件系统的部分情况==，而`df` 命令获得真正的==文件系统数据==。



#### 30、当你需要给命令绑定一个宏或者按键的时候，应该怎么做呢？

​		可以使用 `bind` 命令，`bind` 可以很方便地在 shell 中实现宏或按键的绑定。在进行按键绑定的时候，我们需要先获取到==绑定按键对应的字符序列==。

​		比如获取 `F12` 的字符序列获取方法如下：先按下 `Ctrl+V`，然后按下 `F12`。我们就可以得到 `F12` 的字符序列 ==^[[24~==。接着使用 bind 进行绑定。

```shell
# echo 111 绑定到 ctrl + l 上
[deng@localhost ~]$  bind -x '"\C-l":echo 111'
111
111
```

> 【附】也可以使用 `showkey -a` 命令查看按键对应的字符序列。另外要注意，相同的按键在不同的终端或终端模拟器下可能会产生不同的字符序列。



#### 31、如果一个 linux 新手想要知道当前系统支持的所有命令的列表，他需要怎么做？

使用命令 `compgen -c`，可以打印出所有支持的命令列表。

```shell
# 查看前10条命令
[topcloud@hadoop101 ~]$ compgen -c | head
egrep
fgrep
grep
l.
ll
ls
vi
which
if
then
```



#### 32、如果你的助手想要打印出当前的目录栈，你会建议他怎么做？

使用 Linux 命令 `dirs` 可以将当前的目录栈打印出来。

```shell
# 进目录栈
[topcloud@hadoop101 /etc/profile.d]$pushd /
/ /etc/profile.d

# 进目录栈
[topcloud@hadoop101 /]$pushd /home
/home / /etc/profile.d

# 打印目录栈
[topcloud@hadoop101 /home]$dirs
/home / /etc/profile.d

# 出目录栈
[topcloud@hadoop101 /home]$popd
/ /etc/profile.d

# 出目录栈
[topcloud@hadoop101 /]$popd
/etc/profile.d

# 出目录栈
[topcloud@hadoop101 /etc/profile.d]$popd
-bash: popd: 目录栈为空
```

> 【附】：目录栈通过 `pushd` `popd` 来操作。



#### 33、你的系统目前有许多正在运行的任务，在不重启机器的条件下，有什么方法可以把所有正在运行的进程移除呢？

使用 linux 命令 `disown -r` 可以将所有正在运行的进程移除。

```shell
[topcloud@hadoop101 /home]$jobs
[1]+  已停止               sudo iotop

[topcloud@hadoop101 /home]$disown -r

[topcloud@hadoop101 /home]$jobs
[1]   已停止               sudo iotop

[topcloud@hadoop101 /home]$disown -a
-bash: 警告:删除进程组 2135 中已停止的任务 1

[topcloud@hadoop101 /home]$jobs
```



#### 34、bash shell 中的 hash 命令有什么作用？

​		linux 命令 `hash` 管理着一个内置的哈希表，记录了已执行过的命令的完整路径，用该命令可以打印出你所使用过的命令以及执行的次数。

```shell
[topcloud@hadoop101 /home]$hash
命中	命令
   1	/usr/sbin/iotop
   1	/usr/bin/sudo
   5	/usr/bin/ps
```



#### 35、哪一个 bash 内置命令能够进行数学运算。

`bash shell` 的内置命令 ==let== 可以进行整型数的数学运算。

```shell
# 写入脚本
[topcloud@hadoop101 ~]$ vim calc
#!/bin/bash
let a=5+4
let b=9-3
echo $a $b

# 运算
[topcloud@hadoop101 ~]$ bash calc 
9 6
```



#### 36、怎样一页一页地查看一个大文件的内容呢？

1. `less` 命令
2. `more` 命令

> **less 命令与 more 命令**
>
> ​		`less` 指令用来分屏查看文件内容，它的功能与 `more` 指令类似，但是比 `more` 指令更加强
> 大，支持各种显示终端。 `less` 指令在显示文件内容时，并不是一次将整个文件加载之后才显
> 示，而是==根据显示需要加载内容==，对于显示大型文件具有较高的效率。  



#### 37、怎样查看一个 linux 命令的概要与用法？假设你在/bin 目录中偶然看到一个你从没见过的的命令，怎样才能知道它的作用和用法呢？

使用命令 `whatis` 可以先出显示出这个命令的用法简要，若要详细用法可以使用 `man`、`--help` 或者 `info`

```shell
[topcloud@hadoop101 /etc/profile.d]$whatis cat
cat (1)              - 连接文件并在标准输出上输出
cat (1p)             - concatenate and print files
```



#### 38、Linux 查 CPU 和内存以及磁盘的命令

1. 查看 CPU 信息：
   * `cat /proc/cpuinfo`，相同 physical id 的记录是属于同一个 CPU 的，对应于多核的信息。
2. 查看内存的信息：
   * `cat /proc/meminfo`：它是了解 Linux 系统内存使用状况的主要接口,我们最常用的 free、vmstat 等命令就是通过它获取数据的。
   * `free -mh`：查看内存使用率，并用兆字节显示；
3. 查看硬盘的信息：
   * `cat /proc/scsi/scsi`
   * `fdisk -l`：磁盘的块设备信息；
   * `df -h`：查看磁盘存储情况；

>  **其他命令**
>
>  * `top`：查看进程的内存及 CPU 的信息。
>
>  * `ps aux --sort -rss`：ps命令可以实时的显示各个进程的内存使用情况。可以使用 “–sort”选项对进程进行排序，例如按RSS进行排序：
>
>  * `vmstat`：`vmstat` 是 ==Virtual Meomory Statistics（虚拟内存统计）==的缩写，可对操作系统的虚拟内存、进程、CPU活动进行监控。是对系统的整体情况进行统计，不足之处是无法对某个进程进行深入分析。`vmstat -s` 可以显示内存相关统计信息及多种系统活动数量。
>
>    ```shell
>    [topcloud@hadoop102 ~]$ vmstat
>    procs -----------memory---------- ---swap-- -----io---- -system-- ------cpu-----
>     r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st
>     1  0      0 3344108   2116 334688    0    0    11     2   34   31  0  0 100  0  0
>    [topcloud@hadoop102 ~]$ vmstat -s
>          4028432 K total memory
>           347668 K used memory
>           328628 K active memory
>           174464 K inactive memory
>          3343960 K free memory
>             2116 K buffer memory
>    ```



#### 39、查找文件名，cpu 负载情况的查看？

查找文件名：`find [搜索范围] [选项]`

cpu 负载：`top` 和 `uptime`



#### 40、linux 服务器的负载命令 top 通过哪些指标来看 cpu 状态，内存？

使用 `top` 命令查看负载：

1. `top下按“1”`：查看 CPU 核心数量
2. `shift+"c"`：按 cpu 使用率大小排序
3. `shif+"p"`：按内存使用率高低排序；



**CPU 状态指标**：查看 CPU 的平均负载状况、CPU的使用率、最耗CPU的进程有哪些。

```shell
# load average 数据是每隔5秒钟检查一次活跃的进程数，然后按特定算法计算出的数值。
# 如果这个数除以逻辑 CPU 的数量，结果高于 5 的时候就表明系统在超负荷运转了。
# 通过负载信息能够直观的了解到CPU的压力状况，linux会给出最近1分钟、5分钟、15分钟的平均负载值
top - 20:04:54 up  1:51,  2 users,  load average: 0.15, 0.05, 0.06
```

**内存状态指标**：查看进程占用内存的情况，可用内存大小等。

> ​		`Linux` 的负载高，主要是由于 ==CPU使用、内存使用、IO消耗==三部分构成。任意一项使用过多，都将导致服务器负载的急剧攀升。
>
> ​		查看服务器负载有多种命令，主要有 `uptime`、`w`、`top`、`iostat`，下面将一一展示。
>
> ```shell
> # w和uptime只是单纯的反映出负载，linux提供了更为强大，也更为实用的top命令来查看服务器负载。
> [topcloud@hadoop102 ~]$ w
> 19:44:13 up  1:31,  2 users,  load average: 0.00, 0.01, 0.04
> USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
> topcloud pts/0    192.168.10.1     17:46    1:44m  0.14s  0.14s -bash
> topcloud pts/1    192.168.10.1     18:35    5.00s  0.16s  0.00s w
> 
> [topcloud@hadoop102 ~]$ uptime
> 19:44:16 up  1:31,  2 users,  load average: 0.00, 0.01, 0.04
> 
> # top命令能够清晰的展现出系统的状态，而且它是实时的监控，按q退出。
> [topcloud@hadoop102 ~]$ top
> top - 19:47:44 up  1:34,  2 users,  load average: 0.00, 0.01, 0.04
> Tasks: 147 total,   1 running, 146 sleeping,   0 stopped,   0 zombie
> %Cpu(s):  0.0 us,  0.1 sy,  0.0 ni, 99.9 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
> KiB Mem :  4028432 total,  3343376 free,   348188 used,   336868 buff/cache
> KiB Swap:  2097148 total,  2097148 free,        0 used.  3393872 avail Mem 
> PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+ COMMAND                           
> 1762 topcloud  20   0  160908   2504   1128 S   0.3  0.1   0:00.19 sshd                                        
> 2583 topcloud  20   0  161972   2280   1584 R   0.3  0.1   0:00.01 top                                         
>   1 root      20   0  128372   6948   4180 S   0.0  0.2   0:02.36 systemd      
>   
> # 仅仅有top命令是不够的，因为它仅能展示CPU和内存的使用情况，对于负载升高的另一重要原因——IO没有清晰明确的展示。linux提供了iostat命令，可以了解io的开销。
> 
> # 使用iostat -x 命令来监控io的输入输出是否过大
> [topcloud@hadoop102 ~]$ sudo iotop
> Total DISK READ :	0.00 B/s | Total DISK WRITE :       0.00 B/s
> Actual DISK READ:	0.00 B/s | Actual DISK WRITE:       0.00 B/s
> TID  PRIO  USER     DISK READ  DISK WRITE  SWAPIN     IO>    COMMAND  
> ```
>
> **更多**：https://www.cnblogs.com/dragonsuc/p/5512797.html




#### 41、tail cat 之间的区别，说一下参数

`tail`：用于输出文件中尾部的内容， 默认情况下 tail 指令显示文件的后 10 行内容。  

* `-n`：输出文件尾部 n 行内容；
* `-f`：显示文件最新追加的内容，监视文件变化；

`cat`：全部重定向到标准输出，常用于查看比较小的文件内容，从第一行开始显示。  

* `-n`：显示所有行的行号，包括空行；
* `-b`：和 -n 相似，只不过对于空白行不编号；
* `-s`：当遇到有连续两行以上的空白行，就代换为一行的空白行；
* `-v`： 将不可见字符转变为可见字符；



#### 42、如何查看 Linux 中线程的内存、CPU占用、磁盘的消耗等？具体的参数讲一下

`ps` 命令即可查看当前系统进程状态，如内存、CPU占用、磁盘占用情况等。

* `-a`：选择所有进程
* `-u`：显示所有用户的所有进程
* `-x`：显示没有终端的进程
* `-e`： 列出程序时，显示每个程序所使用的环境变量。
* `-f`：用ASCII字符显示树状结构，表达程序间的相互关系。

> `ps -aux | grep 进程号`（==功能描述：查看系统中所有进程==）
>
> `ps -ef | grep 进程号`（==功能描述： 可以查看子父进程之间的关系==）



#### 43、linux 命令怎么查看 mr 任务的 jobid

`jobs -l`，`-l`是显示进程号。

> **Linux命令中 ps 和 jobs 区别**
>
> * `jobs`：该命令用于查看当前终端==后台运行的任务==。
> * `ps`：该命令用于查看瞬间进程的动态。
>
> ```shell
> # 开启 iotop，然后 ctrl + z 后台挂起
> [topcloud@hadoop101 /home]$sudo iotop
> 
> [topcloud@hadoop101 /home]$jobs -l
> [1]+  2771 停止 (tty 输出)     sudo iotop
> 
> [topcloud@hadoop101 /home]$ps -ef | grep 2771
> root       2771   1453  0 02:20 pts/0    00:00:00 sudo iotop
> root       2777   2771  1 02:20 pts/0    00:00:00 /usr/bin/python /sbin/iotop
> topcloud   2781   1453  0 02:20 pts/0    00:00:00 grep --color=auto 2771
> ```



#### 44、Linux 的 inode 干嘛用的

​		`inode` 又称==索引节点==，是用来存储文件元信息，如==文件的创建者，创建日期，文件大小==。，当系统创建文件系统的同时会创建大量的 `inode`，可以用 `stat` 命令，查看某个文件的 `inode` 信息：

```shell
[topcloud@hadoop102 bin]$ stat xsync
  文件："xsync"
  大小：576       	块：8          IO 块：4096   普通文件
设备：fd00h/64768d	Inode：105232118   硬链接：1
权限：(0764/-rwxrw-r--)  Uid：( 1000/topcloud)   Gid：( 1000/topcloud)
环境：unconfined_u:object_r:home_bin_t:s0
最近访问：2020-10-18 17:38:47.378282460 +0800
最近更改：2020-10-17 02:44:40.064446362 +0800
最近改动：2020-10-17 02:44:40.113446919 +0800
创建时间：-
```

> **详述 inode**
>
> ​		理解 `inode`，要从文件储存说起。文件存储在硬盘上，硬盘的最小存储单位叫做“扇区”（Sector）。每个扇区储存512字节（==相当于0.5KB==）。操作系统读取硬盘的时候，不会一个个扇区的读取，这样效率太低，而是一次性连续读取多个扇区，即一次性读取一个=="块"==（block）。这种由多个扇区组成的=="块"==，是文件存取的最小单位。=="块"==的大小，最常见的是==4KB==，即连续八个 sector 组成一个 block。
>
> ​		文件数据都储存在 =="块"== 中，那么很显然，我们还必须找到一个地方储存文件的=="元信息"==，比如==文件的创建者、文件的创建日期、文件的大小==等等。这种储存文件元信息的区域就叫做 `inode`，中文译名为 =="索引节点"==。每一个文件都有对应的 `inode`，里面包含了与该文件有关的一些信息。



#### 45、UNIX 中进程间通信的方法有哪些？

1. 管道（匿名管道）
2. FIFO（命名管道）
3. 消息队列
4. 信号量
5. 共享内存



#### 46、Linux下，查看 Java 进程的命令

```shell
# 方式一：jps 命令，jps 可以当前的 Java 进程的小工具。
[topcloud@hadoop101 ~]$jps
3265 Jps

# 方式二：ps 命令
[topcloud@hadoop101 /etc/profile.d]$ps -ef | grep java
```



#### 47、Linux下，配置 JDK 环境变量有几种方法，分别是什么？

**一、修改 /etc/profile 文件**

​		当本机仅仅作为开发使用时推荐使用这种方法，因为此种配置时所有用户的 `shell` 都有权使用这些环境变量，可能会给系统带来安全性问题。

​		只需用文本编辑器打开 ==/etc/profile==，在 ==profile== 文件末尾加入配置，然后重新登录或使用 `source` 重新加载配置文件即可。

```shell
JAVA_HOME=/usr/share/jdk1.5.0_05
PATH=$JAVA_HOME/bin:$PATH
CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
export JAVA_HOME
export PATH
export CLASSPATH
```

**二、修改 .bashrc 文件**

​		这种方法更为安全，它可以把使用这些环境变量的==权限控制到用户级别==，如果需要给某个用户权限使用这些环境变量，只需要修改其个人用户主目录下的.bashrc文件就可以了。

​		用文本编辑器打开用户目录下的 ==.bashrc== 文件，在 ==.bashrc== 文件末尾加入，完成后重新登录即可。

```shell
set JAVA_HOME=/usr/share/jdk1.5.0_05
export JAVA_HOME

set PATH=$JAVA_HOME/bin:$PATH
export PATH

set CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
export CLASSPATH
```

**三、直接在 shell 下设置变量**

​		不推荐使用这种方法，因为换个 `shell`，该设置就无效了。这种方法仅仅是临时使用，以后要使用的时候又要重新设置，比较麻烦。

​		只需在 `shell` 终端执行下列命令：

```shell
export JAVA_HOME=/usr/share/jdk1.5.0_05
export PATH=$JAVA_HOME/bin:$PATH
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
```

**注意事项**

1. 要将 ==/usr/share/jdk1.5.0_05== 改为 `jdk` 安装目录
2. linux 下用冒号 ==":"== 来分隔路径
3. `$PATH / $CLASSPATH / $JAVA_HOME` 是用来引用原来的环境变量的值，在设置环境变量时特别要注意不能把原来的值给覆盖掉了。
4. `CLASSPATH` 中当前目录 =="."== 不能丢掉。这个是告诉 `JDK`，搜索 `CLASS` 时先查找当前目录的 ==class 文件==。这是由于 ==LINUX== 的安全机制引起的。
5. `export` 是把这三个变量导出为==全局变量==。
6. 大小写必须严格区分。



#### 48、Linux下查找目录下的所有文件中是否含有某个字符串，并且只打印出文件名。

```shell
[topcloud@hadoop102 ~]$ sudo find . | grep -ril "hello world"
```

> **grep 参数详解**
>
> - `^t`：以 t 开头的行，如 ls / | grep ^t
> - `-i`：不区分大小写地搜索。默认情况区分大小写，
> - `-v`：反转查找。
> - `-l`：只列出匹配的文件名。
> - `-R -r`：递归地，读取每个资料夹下的所有档



#### 49、Linux中，如何调整文件最大打开数

​		Linux 会为每个用户登录系统打开最大文件数都有限制, 这个限制通过 `ulimit -n` 可以看到, 一般是 ==1024==。在一些并发或多线程情况下, 需要突破这个限制。

​		修改方式如下：

1. 编辑 `/etc/security/limits.conf` 并确保其包含下列行：

   ```shell
   # 这里 * 表示所有用户, 但有的系统不认, 需要具体的用户名, 比如: root
   [root@hadoop102 topcloud]# echo "* soft nofile 65535" >> /etc/security/limits.conf
   [root@hadoop102 topcloud]# echo "* hard nofile 65535" >> /etc/security/limits.conf
   ```

2. 编辑 `etc/pam.d/login` ，确保有如下行:

   ```shell
   session required pam_limits.so
   ```

3. 退出终端重新登录并验证

   ```shell
   # 使用 ulimit -Hn 和 ulimit -Sn 命令可以分别查看当前进程用户的 hard 和 soft 的限制数.
   [topcloud@hadoop102 ~]$ ulimit -Hn
   65535
   
   [topcloud@hadoop102 ~]$ ulimit -Sn
   65535
   ```

> **补充：**
>
> 通过命令`ulimit -a`可以查看当前进程可以打开的最大文件数，如下图所示，显示是 ==1024==。
>
> ![ulimit](I:\课程\1 笔记\1.4 Markdown\(1) 计算机科学与技术\【3】大数据\Linux\img\ulimit.png)
>
> ```shell
> # 输入ulimit -n`可以进行查看当前进程可以打开的最大文件数
> [topcloud@hadoop102 ~]$ ulimit -n
> 1024
> 
> # 查看系统最大文件数，它指的是所有进程可以打开的文件数量 
> [topcloud@hadoop102 ~]$ cat /proc/sys/fs/file-max
> 394617
> ```



####  50、Linux 怎么操作，能使一台服务器实时同步另一台服务器的数据

​		可以通过 `rsync + inotify-tools` 结合来实现，编写相关脚本后台运行，一旦文件有变化就执行 `rsync`，来实现服务器间的数据同步。

> * `rsync`：远程同步工具。主要用于备份和镜像。具有速度快、增量备份优点。
> * ` inotify-tools 工具`：该工具为文件实时监控工具，需要 ==linux== 操作系统内核支持，内核支持需要至少版本为 2.6.13。



#### 51、在 Linux 系统中每隔 10 天的 23 点 55 执行 test.sh 脚本的怎么实现？

```shell
# 1、给test.sh脚本执行赋权
[topcloud@hadoop102 ~]$ chmod u+x /home/test.sh

# 2、运行crontab –e，编写一条定时任务
[topcloud@hadoop102 ~]$ crontab -e
55 23 */10 * * /home/test.sh

# 3、centos7设置crond开机自动启动
[root@hadoop102 topcloud]# systemctl enable crond.service

# 4、查看是否自启
[root@hadoop102 topcloud]# systemctl is-enabled crond.service
enabled
```



#### 52、定时任务：脚本 start.sh 每月1日早六点执行

```shell
# 分 时 天 月 周
[topcloud@hadoop102 test]$ crontab -e
0 6 1 * *
```



#### 53、查看 PID 为 7724 的进程占用系统资源的情况，每 2 秒自动更新（命令带参数）

```shell
[topcloud@hadoop102 test]$ top -p 7724 -d 2
```

> **top的命令行使用方式**
>
> 1. `top -b`：批量处理模式，加上 `-b` 后，`top` 显示的时候，将每一次显示的结果都打印出来，不会将上一次的结果给冲掉。
> 2. `top -p pid`：显示某个进程的信息，如果是多个进程，只要如下：`$ top -p pid1,pid2,pid3`
> 3. ` top -u username`：显示某个用户的进程信息
> 4. `top -H`：显示线程的信息，而不是进程的信息
> 5. `top -d ntime`：设置刷屏的时间（单位为s） 



#### 54、查看当前目录下所有文件及目录，包括隐藏的（命令带参数）

```shell
# -R：递归遍历
[topcloud@hadoop102 test]$ ls -aR
.:
.  ..  test1  test2  test3  test4

./test1:
.  ..  test1-1  test1-2  test1-3  test2-1  test2-2  test2-3
```



#### 55、在/home 目录下查找以“.log”结尾的文件名（命令带参数）

`find /home -name *.log`

```shell
# 参考如下
[topcloud@hadoop102 hadoop-3.1.3]$ find logs/ -name *.log
logs/hadoop-topcloud-namenode-hadoop102.log
logs/hadoop-topcloud-datanode-hadoop102.log
logs/hadoop-topcloud-nodemanager-hadoop102.log
logs/hadoop-topcloud-historyserver-hadoop102.log
logs/hadoop-topcloud-timelineserver-hadoop102.log
```



#### 56、若你的程序或脚本运行在 Linux（RetHat 或 Centos）上，请至少列出两种方式将你的程序通过 SSH 运行在服务器后台。

1. 在程序运行时使用 `ctrl+z` 将程序放在后台队列中暂停，在使用 `bg % 序号` 命令，启动，这时如果将终端退出，在使用 `jobs` 查看，无法查看到刚刚放在后台的进程，是因为 `jobs` 只能看到其当前终端的后台程序，如果使用 `ps id` 就可以看到刚刚放在后台的程序了，比如项目端口在10702，我们使用 `lsof -t -i:10702` 获取进程 ==id==号，`ps id` 就能看到后台进程。
2. 使用 `screen` ，会开启一个新的回话，`screen -S name` ,在 `screen` 中启动程序，然后 `ctrl+ b +d` 退出，退出终端，打开一个新的终端，`screen -r name` ,程序依然运行。
3. 使用 `tmux`，`tmux -s name` 创建一个新的回话，在回话中创建程序，`ctrl+b+d`，退出，在退出终端，打开一个新的 使用 `tmux attach  -t name`，进入终端程序依然运行。
4. 使用`nohup command &`命令，在退出当前账户或是关闭终端的时候程序会收到 ==SIGHUP== 信号，这个信号会被使用了 `nohup` 的程序忽略，但是如果使用了 `CTRL + C` 结束命令，程序会收到 ==SIGINT==信号，这个信号还是会让程序终结，如果不想程序被结束，就在结尾加上一个 `&`, 让程序也忽略 ==SIGINT== 信号。



#### 57、Linux查找全磁盘过滤 20G 以上数据的方法

```shell
# -type  b/d/c/p/l/f	查是块设备、目录、字符设备、管道、符号链接、普通文件
find / -type f -size +20G
```



#### 58、Linux 下查看进程占用的 CPU 的百分比，使用工具（）

A、ps				B、cat				C、more				==D、top==



#### 59、解压 tar.gz 结尾的 HBase 压缩包使用的 Linux 命令是（）

==A、tar -zxvf==				B、tar -zx				C、tar -s				D、tar -nf



#### 60、在 Centos 6 中，查询本机 IP 地址的命令是（）

A、ipconfig				==B、ip addr==				C、ifconfig				D、ip

 

#### 61、在 Linux 系统中查询本机内存的命令是（）

==A、free -m==				B、df -h				C、fdisk -l				D、top

 

#### 62、在 Linxu 系统中 start.sh 文件的权限为：-rw-r--r--，下列哪条命令可使属主具有可执行权限（）

A、chmod  644  start.sh

==B、chmod  744  start.sh==

C、chmod  +X start.sh

D、chmod  U+X start.sh



#### 63、在 Linux 系统中的 w 编辑器，下列的命令表示强制保存的是（）

A、 :q				B、:wq				C、:q!				==D、:wq!==



#### 64、还有 linux kill -9 执行时会不会通知进程，如何优雅的关闭

1. **linux kill -9 执行时会不会通知进程?**

​		`kill -9 pid` 则是向进程号为 `pid` 的进程发送 ==SIGKILL==（该信号的编号为9），从文本上面的说明可知，*SIGKILL 既不能被应用程序捕获，也不能被阻塞或忽略，其动作是立即结束指定进程，通俗的说，应用程序捕获，也不能被阻塞或忽略，其动作是立即结束指定进程*。通俗的说，应用层序根本无法感知 ==SIGKILL== 信号，它在完全无准备的情况下，就被收到 ==SIGKILL== 信号的操作系统给干掉了，显然，在这种 “暴力” 情况下，应用程序完全没有释放当前占用资源的机会。事实上，==SIGKILL== 信号是直接发给 ==init== 进程的，它收到该信号后，负责终止 ==pid== 指定的进程。

​		关于 Linux init 进程的说明，可以参考这里。在某些情况下（如进程已经 hang 死，无法响应正常信号），就可以使用 `kill -9` 来结束进程若通过 `kill` 结束的进程是一个创建过子进程的父进程，则其子进程就会成为孤儿进程，这种情况下，子进程的退出系统就不能再被应用程序捕获（因为作为父进程的应用程序已经不存在了），不过应该不会对整个 ==Linux== 系统产生什么不利影响

2. **应用程序如何优雅退出**

​		==Linux Server== 端的应用程序经常会长时间运行，在运行过程中，可以申请了很多系统资源，也可能保存了很多状态，在这些场景下，我们希望进程在退出前，可以释放资源或将当前状态 `dump` 到磁盘上或打印一些重要的日志，也就是希望进程优雅退出（exit gracefully）

​		从这上面介绍不难看出，优雅退出可以通过捕获 ==SIGTERM==（通过 `kill pid` 命令可发送该信号） 

> **kill pid和kill -9 pid的区别**
>
> ​		`kill pid` 的作用是向进程号为 `pid` 的进程发送 ==SIGTERM==（这是 kill 默认发送的信号），该信号是一个结束进程的信号且可以被应用程序捕获。若应用程序没有捕获并响应该信号的逻辑代码，则该信号的默认动作是 `kill` 掉进程，这是终止指定进程的推荐做法。
>
> 
>
> **优雅退出具体来讲，通常只需要两步动作**
>
> 1. 注册 ==SIGTERM== 信号的处理函数，并在处理函数中做一些进程退出的准备。信号处理函数的注册可以通过 `signal()` 或 `sigaction()` 来实现，其中，推荐使用后者来实现信号响应函数的设置。信号处理函数的逻辑越简单越好，通常的做法是在该函数中设置一个 `bool` 型的 `flag` 变量以表明进程收到了 ==SIGTERM== 信号，准备退出
> 2. 在主进程的main()中，通过类似于while(!bQuit)的逻辑来检测哪个flag变量，一旦bQuit在signal handler function中被置为true，则主进程退出while()循环，接下去就是一些释放资源或dump进程当前状态或记录日志的动作，完成这些后，主进程退出



#### 65、还有如何通过 linux 一行指令找到 5 天内修改过的文件

```shell
[topcloud@node02 ~]$ find /opt/ -mtime -5
```

> **Linux下查找固定时间内被访问过的文件：**
>
> ```shell
> #查找最近1小时内访问的文件：
> [topcloud@node02 ~]$ sudo find /opt -amin -60
> ```
>
> 
>
> **Linux下查找固定时间内被更改过的文件：**
>
> ```shell
> # 在过去2天中（包括第二天）查找更改的文件
> [topcloud@node02 ~]$ find /etc/profile -ctime 2
> 
> # 在过去2天中（不包括第二天）查找更改的文件
> [topcloud@node02 ~]$ find /etc/profile -ctime -2
> 
> # 在1-3天更改的文件
> [topcloud@node02 ~]$ find /etc/profile -ctime +1 -ctime -3
> ```
>
> 
>
> **Linux下查找固定时间内被修改过的文件：**
>
> ```shell
> # 查找最近 30分钟内 修改过的文件
> [topcloud@node02 ~]$ find /opt/ -mmin -30
> 
> # 查找最近24小时内修改过的文件
> [topcloud@node02 ~]$ find /opt/ -mtime 0
> 
> # 查找最近24~48小时之间修改过的文件
> [topcloud@node02 ~]$ find /opt/ -mtime 1
> ```
>
> 更多：https://www.cnblogs.com/Ido-911/p/9638612.html