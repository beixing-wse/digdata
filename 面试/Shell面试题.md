[TOC]

#### 01、Shell常用工具及写过的脚本

1）awk、sed、cut、sort

2）用Shell写过哪些脚本

​    （1）集群启动，分发脚本

​    （2）数仓与mysql的导入导出

​	（3）数仓层级内部的导入



#### 02、Shell中提交了一个脚本，进程号已经不知道，但是需要kill掉这个进程，怎么操作?

```shell
ssh $i "ps -ef | grep file-flume-kafka | grep -v grep |awk '{print \$2}' | xargs kill"
```



####  03、Shell中单引号和双引号区别

1）在/home/atguigu/bin创建一个test.sh文件

```shell
[atguigu@hadoop102 bin]$ vim test.sh 
```

在文件中添加如下内容

```shell
#!/bin/bash
do_date=$1

echo '$do_date'
echo "$do_date"
echo "'$do_date'"
echo '"$do_date"'
echo `date`
```

2）查看执行结果

```shell
[atguigu@hadoop102 bin]$ test.sh 2019-02-10
$do_date
2019-02-10
'2019-02-10'
"$do_date"
2019年 05月 02日 星期四 21:02:08 CST
```

3）总结：

（1）单引号不取变量值

（2）双引号取变量值

（3）反引号`，执行引号中命令

（4）双引号内部嵌套单引号，取出变量值

（5）单引号内部嵌套双引号，不取出变量值

---

1. 新建测试脚本test.sh

   ```
   #!/bin/bash
   val=22
   echo $val
   echo "$val"
   echo '$val'
   echo "'$val'"
   echo '"$val"'
   1234567
   ```

2. 修改执行权限
   `chmod 777 test.sh`

3. 执行结果

   ```
   [root@cdh01 ~]# ./test.sh
   22
   22
   $val
   '22'
   "$val"
   123456
   ```

4. 结论

   - 当单独使用单引号时，不能取出变量值
   - 当单独使用双引号时，可以取出变量值
   - 当外层使用双引号时，输出内层的单引号和变量值
   - 当外层使用单引号时，输出内层的双引号和双引号中的内容。



#### 04、用一条shell命令找出一个文件中出现次数最多的userid的top10



#### 05、linux 中工具命令 cut 使用命令

获取当前机器IP地址

`ifconfig eth0 | grep "inet addr" | cut -d":" -f 2 | cut -d" " -f 1`

-f 列号，提取第几列

-d 分隔符，按照指定分隔符分割列



```shell
指定输出一行中的选取部分。

输出每一行的第二个字节内容：cut -b 2 cut.txt

输出每一行的第二个字符内容：cut -c 2 cut.txt

输出每一行第一列内容：cut -d , -f 1 cut.txt

输出每一行第一、二列内容：cut -d , -f 1,2 cut.txt 

选取字节的列表，即选取每行的第N个字节。：-b,--bytes

选取字符的列表，即选取每个的第N个字符。(英文字符下与-b没有区别，中文字符下，一个中文占据2-3个字节，所以存在中文的时候更倾向于用-c)。：-c,--characters

分隔符，默认为TAB。：-d,--delimiter

选取列的列表，即选取每行的第N列。：-f,--field
```





#### 06、常用的Linux命令，Shell的awk、sed、sort、cut是用来处理什么问题的？

cut的工作就是“剪”，具体的说就是在文件中负责剪切数据用的。cut 命令从文件的每一行剪切字节、字符和字段并将这些字节、字符和字段输出。

sed是一种流编辑器，它一次处理一行内容。处理时，把当前处理的行存储在临时缓冲区中，称为“模式空间”，接着用sed命令处理缓冲区中的内容，处理完成后，把缓冲区的内容送往屏幕。接着处理下一行，这样不断重复，直到文件末尾。文件内容并没有改变，除非你使用重定向存储输出。

awk一个强大的文本分析工具，把文件逐行的读入，以空格为默认分隔符将每行切片，切开的部分再进行分析处理。

sort命令是在Linux里非常有用，它将文件进行排序，并将排序结果标准输出。



#### 07、使用Linux命令查询file1里面空行的所在行号

```shell
1，sed -n '/[a-zA-Z0-9@#$%^&*]/!=' file1
2，grep -n ^$ file1
3，awk '/^$/{print NR}' file1
4，sed -n '/^$/=' file1
```



#### 08、有文件chengji.txt内容如下:

```tex
张三 40

李四 50

王五 60
```

请使用Linux命令计算第二列的和并输出

```shell
awk -F " " '{sum+=$2} END{print sum}'
```



#### 09、awk -F的作用

```shell
指定分隔符

- awk -F: '{print $1}'  /etc/passwd ==  awk -F ":" '{print $1}' /etc/passwd
- awk -F: '{print $1 $2}'                         输入字段1,2，中间不分隔
- awk -F: '{print $1,$3,$6}' OFS="\t" /etc/passwd     输出字段1,3,6， 以制表符作为分隔符
- awk -F: '{print $1; print $2}'  /etc/passwd          输入字段1,2，分行输出
- awk -F: '{print $1 "**" print $2}'  /etc/passwd        输入字段1,2，中间以**分隔
- awk -F: '{print "name:"$1"\tid:"$3}' /etc/passwd      自定义格式输出字段1,2
- awk -F: '{print NF}' /etc/passwd                   显示每行有多少字段
- awk -F: 'NF>2{print }' /etc/passwd                 将每行字段数大于2的打印出来
- awk -F: 'NR==5{print}' /etc/passwd                打印出/etc/passwd文件中的第5行
- awk -F: 'NR==5|NR==6{print}' /etc/passwd          打印出/etc/passwd文件中的第5行和第6行
- awk -F: 'NR!=1{print}' /etc/passwd                不显示第一行
- awk -F: '{print > "1.txt"}' /etc/passwd              输出到文件中
- awk -F: '{print}' /etc/passwd > 2.txt                使用重定向输出到文件中
```





#### 10、在CentOS 7中，/home/centos/txt的方容如下:

```tex
  aaa bbb abc

  ccc aaa ddd

  aab eee fff

  aaa ggg hhh
```



(1)查找以aaa开头的行，要求一行命令

(2)将以aaa开头的那一行中的全部a换成大写A，要求一行命令。

```shell
find . -name "txt" -exec grep '^aaa' {} \; |wc -l
```





#### 11、awk用过吗

awk 自成一门编程语言，语句的分隔是有特点的。涉及到`''`，`{}`，`,`这些符号，我们总结出特点有以下三点：

- 1.被 `{}`包裹的是 awk 的 action 动作，也就是说下面 awk 的各种语法放在`{}`才能被 awk 语法编译执行，`{}`中被识别为 awk 的语法

- 2.`{}`中，awk 的脚本语句之间需要用`;`隔开，这一点与其他编程语言类似

- 3.`{}`外，单引号内的空间是模式语句，模式可以直接做真假值的判定，不用加 if 语句，比如`NR==1`，awk 会逐行进行的判定，当 awk 遍历到该行的时候，若此条件判定为真，就会输出该行相应的数据，否则不输出

  基础操作：

  ```shell
  *# 打印第一列* awk '{print $1}' test.log 
  
  *# 格式化打印第一列第二列* awk '{print $1,\t,$2}' test.log 
  
  *# 打印第一行* awk 'NR==1 {print $0}' test.log 
  
  *# 打印匹配到数字的行的行号和第一列* awk '/[0-9]/ {print NR,$1}' test.log 
  
  *# 打印第一列匹配到数字的行* awk '$1~/[0-9]/ {print $0}' test.log 
  
  *# 不匹配数字的行* awk '!/[0-9]/ {print $0}' test.log 
  
  *# 设置 : 为分隔符* awk -F ':' '{print $1}' test.log awk 'BEGIN{FS==":"} {print $1}' test.log 
  
  *# 多重分割，用空格和逗号做分给，逻辑上是先用空格分隔，之后空格里在用逗号分隔* awk -F '[ ,]' '{print $1,$2}' test.log 
  
  *# 不区分大小写匹配* awk 'BEGIN{IGNORECASE=1} /aaa/' test.log 
  
  *# 输出 0-1 的随机数* echo | awk '{srand(); print rand()}'
  ```

  



#### 12、linux命令 磁盘 内存 剩余内存free 定时任务

```shell
创建一个文件 aa.sh 文件名不重要要以 .sh 结尾

free -m：在aa.sh文件夹中输入查询命令

chmod +x *.sh：给所有sh结尾的文件赋予执行的权限

crontab -e：创建定时任务

 */1 * * * * //var/spool/mail/ds.sh：输入定时时间以及要运行的脚本文件要绝对路径

:wq：保存并退出
```





#### 13、AWK、sort等用过把，讲讲呗



**AWK**

有三种方式调用awk

1.命令行方式
awk [-F  field-separator]  'commands'  input-file(s)
其中，commands 是真正awk命令，[-F域分隔符]是可选的。 input-file(s) 是待处理的文件。
在awk中，文件的每一行中，由域分隔符分开的每一项称为一个域。通常，在不指名-F域分隔符的情况下，默认的域分隔符是空格。

2.shell脚本方式
将所有的awk命令插入一个文件，并使awk程序可执行，然后awk命令解释器作为脚本的首行，一遍通过键入脚本名称来调用。
相当于shell脚本首行的：#!/bin/sh
可以换成：#!/bin/awk

3.将所有的awk命令插入一个单独文件，然后调用：
awk -f awk-script-file input-file(s)
其中，-f选项加载awk-script-file中的awk脚本，input-file(s)跟上面的是一样的。

 基本用法：

awk [选项参数] ‘pattern1{action1} pattern2{action2}...’ filename

pattern：表示AWK在数据中查找的内容，就是匹配模式

action：在找到匹配内容时所执行的一系列命令

**sort命令：**

用法：sort [选项]... [文件]...
串联排序所有指定文件并将结果写到标准输出。

排序选项：

-b, --ignore-leading-blanks 忽略前导的空白区域
-d, --dictionary-order 只考虑空白区域和字母字符
-f, --ignore-case 忽略字母大小写
-g, --general-numeric-sort 按照常规数值排序
-i, --ignore-nonprinting 只排序可打印字符
-n, --numeric-sort 根据字符串数值比较
-r, --reverse 逆序输出排序结果

其他选项：

-c, --check, --check=diagnose-first 检查输入是否已排序，若已有序则不进行操作
-k, --key=位置1[,位置2] 在位置1 开始一个key，在位置2 终止(默认为行尾)
-m, --merge 合并已排序的文件，不再进行排序
-o, --output=文件 将结果写入到文件而非标准输出
-t, --field-separator=分隔符 使用指定的分隔符代替非空格到空格的转换
-u, --unique 配合-c，严格校验排序；不配合-c，则只输出一次排序结果



#### 14、awk 详解。

答案：

```shell
awk '{pattern + action}' {filenames}

\#cat /etc/passwd |awk -F ':' '{print 1"\t"7}' //-F 的意思是以':'分隔 root

/bin/bash

daemon /bin/sh 搜索/etc/passwd 有 root 关键字的所有行

\#awk -F: '/root/' /etc/passwd root:x:0:0:root:/root:/bin/bash
```





#### 15、如何查找某个文件里的重复行

```shell
sort aa.txt | uniq -d：aa.txt为文件名
```





#### 16、用到哪些linux命令，如果一个文件夹占了很大的存储空间，比如文件夹下有几千个文件，怎么用命令找到这个文件夹

```shell
find . -type f -size +100M #查找100M以上的文件

find . -type f -size +100M  -print0 | xargs -0 du -h | sort -nr#对查找结果按照文件大小做一个排序

sudo du -hm --max-depth=2 | sort -nr | head -20#查找当前目录下前20的大目录
```







#### 17、使用过类似awk之类的函数

1. 概述
   1. 简述 shell 命令行工具 cut
2. 背景
   1. 偶尔需要用 awk 来筛选特定的列
      1. awk 很是强大
      2. 但是强大的背后, 却伴随着复杂
         1. 其实同样的功能, awk 也没有复杂多少
   2. 如果是 简单的任务, cut 工具完全是可以胜任的
      1. 切割行内的特定位置
      2. 切割行内的特定字段
      3. 描述可能不是很准确, 下面会有例子

**1. 准备**

1. os

   1. centos7

2. 文件

   1. cutdemo01

      ```
      1:2:3:4:5
      1:2:3:4:5
      1:2:3:4:5
      ```

   2. cutdemo02

      ```
      1	2	3	4	5
      1	2	3	4	5
      1	2	3	4	5
      ```

**2. 场景1: 切割行内的特定位置**

1. 概述

   1. 想切割行内的特定字符

2. 命令

   1. 命令1: 切割单个字符

      ```
      # -c 表示切割行内的 特定字符
      # 下标从 1 开始
      # 如果超出范围, 会返回 空内容
      > cut -c1 cutdemo01
      1
      1
      1
      ```

   2. 命令2: 切割连续字符

      ```
      # 下标从 1 开始, 3 结束
      > cut -c1-3 cutdemo01
      1:2
      1:2
      1:2
      ```

   3. 命令3: 切割不连续字符

      ```
      # 下标从 1 开始, 3 结束, 外加第 5 个字符
      > cut -c1-3,5 cutdemo01
      1:23
      1:23
      1:23
      ```

**3. 场景2: 切分行内特定字段**

1. 概述

   1. 类似 awk 的切割方式

2. 命令

   1. 命令1: 切割特定分隔符下的字段

      ```
      -d 指定分隔符
      -f 指定字段
      > cut -d':' -f 1 cutdemo01
      1
      1
      1
      ```

   2. 命令2: 切割特定分隔符下的连续字段

      ```
      # -f 类似 之前的 -c
      # 结果中, 每个字段, 会用 -d 指定的分隔符隔开
      > cut -d':' -f 1-3 cutdemo01
      1:2:3
      1:2:3
      1:2:3
      ```

   3. 命令3: 切割特定分隔符下的不连续字段

      ```
      > cut -d':' -f1-3,5 cutdemo01
      1:2:3:5
      1:2:3:5
      1:2:3:5
      ```

3. 疑问

   1. 如果要用 tab 分列, 命令行打不出 tab, 用 \t 转义也不好使, 该怎么办
      1. 可以看看 man 命令
         1. 不带 -d, 默认就是用 tab 来分

4. 坑

   1. cut 只能以 一个字符 作为分隔符
      1. 所以可能会有 两种可能会坑
         1. 需要 连续多个字符, 做分隔符
         2. 同时使用 多种字符, 做分隔符
      2. 解决
         1. 使用 awk







#### 19、Linux 基本命令，shell 语法，写了哪些 shell，里面如何写的，具体过程



#### 20、test.log日志中内容如下左列所示，使用awk输出右列4行数据

```shell
10-3-jd-dv

2-4-jd-dv	10-4-jd-dv

5-7-pv-click	5-7-pv-click

36-24-pv-uv

37-24-pv-uv	37-24-pv-uv

24-3-uv-mq	24-3-uv-mq
```



#### 21、常用的linux命令，shell的awk、sed、sort、cut是用来处理什么问题的？

作用：--- 截取文本字符串，获取某些内容

   --- 写脚本



#### 22、awk -F的作用



#### 23、写过哪些 shell脚本？

1. 启动停止脚本

   ```shell
   #!/bin/bash 
   case $1 in 
   "start"){
   for i in hadoop102 hadoop103
   do
   
   done
   };; 
   "stop"){
   for i in hadoop102 hadoop103
   do
   
   done
   };; 
   easc
   ```

   

2. 数仓层级内部的导入

3. 与MySQL的导入导出

 

#### 24、单引号和双引号区别

        双引号：解析变量
        单引号：不解析变量
        
        嵌套问题： 看谁在最外面  
        在文件中添加如下内容
        echo '$do_date'
        echo "$do_date"
        echo "'$do_date'"
        echo '"$do_date"'
        echo `date`
        2）查看执行结果
        $do_date
        2019-02-10
        '2019-02-10'
        "$do_date"
        2019年 05月 02日 星期四 21:02:08 CST


#### 25、让我用Shell写一个脚本，对文本中无序的一列数字排序

我说Shell简单的我可以，比如说写个脚本，Crontab周期性调度一下，复杂的我得查下资料，也就没写

`awk -F ' '  '{print $1}' test.txt |sort -n`

`sort -n test.txt|awk '{a+=$0;print $0}END{print "SUM="a}'`

#### 26、Shell脚本实际上是什么（问的应该是shell底层调用了什么）

默认：/bin/bash

#### 27、Shell脚本里如何检查文件是否存在，如果不存在该如何处理？Shell里如何检查一个变量是否是空？

判断一个文件是否存在？不存在则创建该文件。

脚本 isFileExist.sh，注意[  ]的右边和左边要有空格（条件判断式与[]之间必须有空格）

`./isFileExist.sh /root/passwd` 测试，

```shell
#! /bin/bash
if [ ! -f "$1" ];then
        touch "$1"
fi
```

判断变量是否为空：

```shell
# -n 判断一个变量是否有值
var=1
if [ ! -n "$var" ]; then
 echo "$var is empty"
 exit 0
fi
if [ -n "$var" ]; then
 echo "$var"
 exit 0
fi
```



#### 28、Shell脚本里如何统计一个目录下（包含子目录）有多少个Java文件？如何取得每一个文件的名称（不包含路径）

获取当前文件夹（包含子目录）有多少个.java文件：

`ls -lR|grep "^-"|grep ".java"| wc -l`

统计当前文件夹下文件的个数：

`ls -l |grep "^-"|wc -l`

统计当前文件夹下目录的个数:

`ls -l |grep "^d"|wc -l`

统计当前文件夹下文件的个数，包括子文件夹里的:

`ls -lR|grep "^-"|wc -l`

统计文件夹下目录的个数，包括子文件夹里的

`ls -lR|grep "^d"|wc -l`

#### 29、Shell脚本，bash的含义，以及简单的说自己写过的脚本

Shell脚本是一个命令解释器，操作系统是看不懂用户所输入的指令，通过shell解释器，能够将用户输入的指令传递给操作系统内核。

bash是CentOS的默认Shell解析器。bash能够直接在命令行直接执行用户输入的指令，也能够在文件中读取命令，所以通常在脚本文件的首行我们会输入`#! /bin/bash`，这就是在指定Shell解析器。

#### 30、请用shell脚本写出查找当前文件夹（/home）下所有的文本文件内容中包含有字符”a”的文件名称

`grep -r "a" /home | cut -d ":" -f 1  `

#### 31、常用的shell语法

```shell
if [ 条件 ];then
	程序
fi
```

注意：if后有空格，[]和条件之间有空格

```shell
case $var in
	"值1")
	程序
	;;
	
	"值1")
	程序
	;;
	
	*)
	程序
	;; 
esac
```

#### 32、shell脚本用kill -9 停止正在运行的hadoop和spark。



#### 33、shell脚本呢 是定时任务还是人工

shell脚本可以放到定时任务中执行，也可以手动执行

#### 34、shell脚本遍历文件夹

遍历某目录下所有文件夹，参数1为文件夹

```shell
#!/bin/bash
for file in `ls $1`
	do
		echo $1"/"$file
	done
```

遍历目录及其子目录中的所有文件方法，参数1为文件夹

```shell
#! /bin/bash
function read_dir(){
for file in `ls $1` #注意此处这是两个反引号，表示运行系统命令
do
 ``if [ -d $1"/"$file ] #注意此处之间一定要加上空格，否则会报错
 ``then
 ``read_dir $1"/"$file
 ``else
 ``echo $1"/"$file #在此处处理文件即可
 ``fi
done
} 
#读取第一个参数
read_dir $1
```

#### 35、shell：统计每个ip个数（应该问的是如何统计日志文件中ip的个数）

日志内容：

```
112.111.12.248 – [25/Sep/2013:16:08:31 +0800]formula-x.haotui.com“/seccode.php?update=0.5593
110133088248″ 200″http://formula�x.haotui.com/registerbbs.php” “Mozilla/4.0 (compatible; MSI
E 6.0; Windows NT 5.1;SV1;)”61.147.76.51 – [25/Sep/2013:16:08:31 +0800]xyzdiy.5d6d.com“/atta
chment.php?aid=4554&k=9ce51e2c376bc861603c7689d97c04a1&t=1334564048&fid=9&sid=zgohwYoLZq2qPW
233ZIRsJiUeu22XqE8f49jY9mouRSoE71″301″http://xyzdiy.5d6d.com/thread-1435-1-23.html” “Mozilla
/4.0 (compatible; MSIE 6.0;Windows NT 5.1; SV1; .NET CLR 1.1.4322; .NET CLR 2.0.50727)”
```

`awk -F' ' '{print $1}' 1.log |sort -n |uniq -c |sort -n`：1.log为文件名

#### 36、用一条shell命令找出一个文件中出现次数最多的userid的top10

文件userid.log内容如下：

userid:zs
userid:li
userid:zs
userid:li
userid:zs1
userid:zs2
userid:zs3
userid:zs4
userid:aa1
userid:aa2
userid:aa2
userid:aa3
userid:aa4
userid:aa5
userid:aa6
userid:aa7
userid:aa8

`awk -F: '{print $2}' userid.log | sort -n | uniq -c |sort -rn | head 10`

#### 37、shell命令说几个

常用的查看文件的命令

cut,awk,sed,sort

#### 38、shell语法，写了哪些shell，里面如何写的，具体过程

统计日志文件中每个ip的访问次数，

`awk -F' ' '{print $1}' 1.log |sort -n |uniq -c |sort -n`

查看日志中访问次数最多的前10个IP

`cat access_log |cut -d ' ' -f 1 | sort |uniq -c | sort -nr | awk '{print $0 }' | head -n 10 | less`

查看最近访问量最高的文件

`cat access_log | tail -10000 | awk '{print $7}' | sort | uniq -c | sort -nr | less`

#### 39、shell语言掌握怎么样 crontab各指的是什么单位  ls -l 想得到文件属主和文件名 

第一个*表示第几分钟

第一个*表示第几小时

第一个*表示第几天

第一个*表示第几月

第一个*表示星期几

