# Markdown分享



## 标题



　　`ctrl + 1 ~ 6`



## 代码



　　两个反点中间的部分，数字键1旁边那个



## 代码块



　　三个反点 + 语言

```java
package com.shsxt.day03;

public class ForDemo {

    public static void main(String[] args) {
        /*
            语法格式：
            for (起始变量; 条件表达式; 对起始变量的操作) {
                语句体;
            }

            解释：
                第一步：初始化变量，比如 int i = 0;
                第二步：执行条件表达式，比如 i <= 5;
                第三步：第二步执行如果为 true，执行语句体；如果为 false 结束循环
                第四步：语句体执行结束，执行对起始变量的操作，然后执行第二步。比如 i++;
         */

        // 需求：打印 0 ~ 5
        for (int i = 0; i <= 5; i++) {
            System.out.println("i = " + i);// 打印变量
        }

        System.out.println("后续代码");
    }

}
```



## 引用



大于号`>`

> 这里是引用的内容



## 链接



`[这里写链接的名称](链接的地址)`

[百度](https://www.baidu.com)

[图壳免费图床](https://imgkr.com/)

[sm.ms免费图床](https://sm.ms/)



## 图片



`![图片描述](图片地址)`



![99乘法表](https://static01.imgkr.com/temp/5faa075462084b01a02b41004d130955.jpg)



## 表格



`ctrl + t`



| 编号 | 姓名 | 年龄 |
| ---- | ---- | ---- |
| 001  | 张三 | 18   |
|      |      |      |
|      |      |      |



## 列表



`-` 短横杠



- 我是列表1
- 我是列表2
- 我是列表3



`数字`



1. 我是1
2. 我是2
3. 我是3



