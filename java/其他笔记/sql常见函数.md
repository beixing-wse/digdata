[toc]



# 随笔记录

## 1、MySQL常用函数

## 1.1概念

​		类似于java中的方法，将一组逻辑语句封装在方法体中，对外暴露方法名

## 1.2好处

-  隐藏内部细节
- 提高代码重用性

## 1.3调用

​		select 函数名（实参列表） from 表；

## 1.4 分类

- 单行函数 （cencat、length、ifnull）
- 分组函数

### 1.4.1字符函数

- length

  select length('join');返回4

  select length（"王寿恩"）;返回15

- concat字符串拼接

  select concat(last_name,'_',first_name) from emplyess;

- upper，lower，大写，与小写

  select concat(upper(last_name),'_',lower(first_name)) from emplyess;

- substr,截取字符串

  select substr('abcdefgh',4,3);返回def；开始索引(为1vcc)和长度

- instr(str1,str2) 返回str2第一次出现在str1中的索引

  select instr('abcdef','de');返回4

- trim   去除前后空格.trim('str','str1')   去除str1中的前后str 

  select length(trim('      abc        '));返回3

- replace('str','str1','str2')   用str2替换str 中的str1

### 1.4.2数学函数

- round(num，num1) 四舍五入，保留num1为小数

- ceil(num)   向上取整，返回>=num的最小整数

- floor(num)   向下取整,返回<=num的最大整数

- truncate(num,num1)   截断

  truncate(1.1111,1) 返回1.1 

- mod(num1.num2)取余 返回 a-a/b*b

### 1.4.3日期函数

- now()返回当前日期时间

- curdate() 返回当前时间，不包含时间

- cuitime() 返回当前时间，不包含日期

- 可以获取指定的部分，年，月，日，时，分，秒

  select year(now()) 年;

  select month(now()) 月;

  select day(now()) 日;

- str_to_date将日期通过指定格式转换为日期

  select str_to_date('1998-3-3','%Y-%c-%d');

  select str_to_date('3-3 1998','%d-%c %Y');

- data_format(data,''format)将日期转换为字符串

   select data_format(now(),'%y年%m月%d日');

### 1.4.4其他函数

- select version();
- select database();
- select user();

### 1.4.5流程控制函数

- if函数
- case函数
- 

