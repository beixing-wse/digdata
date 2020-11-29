[TOC]



# JSP/JSTL

## 1、主要内容

![](G:\java\我的笔记\笔记图片\jsp主要内容.png)

## 2、JSP

### 2.1JSP基础语法

#### 2.1.1JSP简介

​		jsp 的全称是<font color ="red"> java server pages</font>。Java 的服务器页面。

​		jsp 页面本质上是一个 Servlet 程序。

​		JSP：Java Server Page SUN 公司提供的动态网页编程技术，是 Java Web 服务器端的<font color ="red">动态资源</font>。

#### 2.1.2. 注释

​		在 JSP 中支持两种注释的语法操作：
​		一种是显示注释，这种注释是允许客户端看见的； 另一种是隐式注释，此种注释是客户端无法看见的
​		① 显示注释语法：从 HTML 风格继承而来
​		② 隐式注释语法：从 JAVA 风格继承；JSP 自己的注释
​		JSP 的三种注释方式：

```
1） // 注释，单行注释 /* 多行注释*/
2）<!-- HTML风格的注释 -->
3）<%--  JSP注释  --%>
```

#### 2.1.3jsp 中的常用脚本

- 第一种，声明脚本：
  声明脚本格式如下：

  ```
  <%!
  	java 代码
  %>
  ```

  在声明脚本块中，我们可以干 4 件事情
  	1.我们可以定义全局变量。
  	2.定义 static 静态代码块
  	3.定义方法
  	4.定义内部类
  几乎可以写在类的内部写的代码，都可以通过声明脚本来实现

-   <font color = red>第二种，表达式脚本（*** 重点，使用很多）：</font>

  表达式脚本格式如下：

  <%=表达式	 %>

  表达式脚本 用于向页面输出内容。
  表达式脚本 翻译到 Servlet 程序的 service 方法中 以 out.print() 打印输出
  out 是 jsp 的一个内置对象，用于生成 html 的源代码
  <font color = "red">注意：表达式不要以分号结尾，否则会报错</font>
  <font color = "red">表达式脚本可以输出任意类型。</font>

- <font color = "red">第三种，代码脚本（***** 重点，使用最多 ）</font> 

  代码脚本如下：

  <% java 代码 	 %>

  代码脚本里可以书写任意的 java 语句。
  代码脚本的内容都会被翻译到 service 方法中。
  所以 service 方法中可以写的 java 代码，都可以书写到代码脚本中

### 2.2. JSP的指令标签

​		使用包含操作，可以将一些重复的代码包含进来继续使用，从正常的页面组成来看，有时可能分为几个区域。而其中的一些区域可能是一直不需要改变的，改变的就其中的一个具体内容区域。现在有两种方法可以实现上述功能。
​		方法一：在每个 JSP 页面（HTML）都包含工具栏、头部信息、尾部信息、具体内容
​		方法二：将工具栏、头部信息、尾部信息都分成各个独立的文件，使用的时候直接导入
​		很明显，第二种方法比第一种更好，第一种会存在很多重复的代码，并且修改很不方便，在 JSP 中如果要想实现包含的操作，有两种做法：**静态包含**、**动态包含**，静态包含使用 include 指令即可，动态包含则需要使用 include 动作标签。

#### 2.2.1. include 静态包含

```
<%@ include file="要包含的文件路径" %>  <!-- 相对路径 -->
```

​		静态包含的特点：
​      		  1 、静态包含不会翻译被包含的 jsp 页面。
​      		  2 、静态包含其实是把被包含的 jsp 页面的代码拷贝到包含的位置执行输出。
​      		  3、相当于直接内容的复制，不能出现同名变量
​      		  4、运行效率高一点点，耦合性较高，不够灵活。

```jsp
<head>
    <title>include静态包含</title>
</head>
<body>
<%--
    <%@ include file=""%> 就是静态包含
        file 属性指定你要包含的 jsp 页面的路径
        地址中第一个斜杠 / 表示为 http://ip:port/ 工程路径 / 映射到代码的 web 目录
        静态包含的特点：
        1 、静态包含不会翻译被包含的 jsp 页面。
        2 、静态包含其实是把被包含的 jsp 页面的代码拷贝到包含的位置执行输出。
        3、相当于直接内容的复制，不能出现同名变量
        4、运行效率高一点点，耦合度高，不够灵活
--%>
    <%@ include file="02-静态包含01.jsp"%>
    <h2>body内容</h2>
    <%@ include file="02-静态包含02.jsp"%>
</body>
```

#### 2.2.2. include 动态包含

​		动态包含在代码的编译阶段，包含和被包含部分是两个独立的部分，只有当运行时，才会动态包含进来，好比方法的调用。

```
格式：
    <jsp:include page="路径"></jsp:include>
特点：
    相当于方法的调用，会生成多个源码文件，可以出现同名变量。

注：
    1. inculue动态包含是双标签
    2. inculue动态包含可以传递参数
        <jsp:param name="参数名" value="参数值"/> name不支持任何表达式，value支持表达式
        参数的接收：request.getParameter(name);
    3. 如果没有参数传递，include双标签之间不能有任何内容，包括空格和换行
```

```jsp
<jsp:include page="03-include动态包含01.jsp"></jsp:include>
<h2>主体内容</h2>
<%
    String str = "Hello";
%>
<%-- 传递参数 --%>
<jsp:include page="03-include动态包含02.jsp">
    <jsp:param name="uname" value="admin"/>
    <jsp:param name="str" value="<%=str%>"/>
</jsp:include>
```

### 2.3. JSP的四大域对象

#### 2.3.1. 四种属性范围

在JSP中提供了四种属性的保存范围，所谓的属性保存范围，指的就是一个设置的对象，可以再多少个页面中保存
并可以继续使用

1. page范围
pageContext : 只在一个页面中保存属性，跳转之后无效
2. request范围
request : 只在一次请求中保存，服务器跳转后依然有效
3. session范围

   session : 在一次会话范围中，无论何种跳转都可以使用

4. application范围
    application : 在整个服务器上保存

| 方法                                            | 类型 | 描述                 |
| ----------------------------------------------- | ---- | -------------------- |
| public void setAttribute(String name, Object o) | 普通 | 设置属性的名称及内容 |
| public Object getAttribute(String name)         | 普通 | 根据属性名称取属性   |
| public void removeAttribute(String name)        | 普通 | 删除指定的属性       |

#### 2.3.2. 验证属性范围的特点

1. page
本页面取得，服务器端跳转（ <jsp :forward> ）后无效
1. request
服务器跳转有效，客户端跳转无效
如果是客户端跳转，则相当于发出了两次请求，那么第一次的请求将不存在了；如果希望不管是客户端还是服务器跳转，都能保存的话，就需要继续扩大范围。
1. session
无论客户端还是服务器端都可以取得，但是现在重新开启一个新的浏览器，则无法取得之前设置的session了，因为每一个session只保存在当前的浏览器当中，并在相关的页面取得。
对于服务器而言，每一个连接到它的客户端都是一个session如果想要让属性设置一次之后，不管是否是新的浏览器打开都能取得则可以使用application
1. application
所有的application属性直接保存在服务器上，所有的用户(每一个session)都可以直接访问取得
只要是通过application设置的属性，则所有的session都可以取得，表示公共的内容，但是如果此时服务器重启了，则无法取得了，因为关闭服务器后，所有的属性都消失了，所以需要重新设置。
问：使用哪个范围呢？
答：<font color = "red">在合理范围尽可能小</font>

### 2.4jsp 九大内置对象

- <font color = "red">request 对象 请求对象，可以获取请求信息</font>
- <font color = "red">response 对象 响应对象。可以设置响应信息</font>
- pageContext 对象 当前页面上下文对象。可以在当前上下文保存属性信息
- <font color = "red">session 对象 会话对象。可以获取会话信息。</font>
- exception 对象 异常对象只有在 jsp 页面的 page 指令中设置 isErrorPage="true" 的时候才会存在
- application 对象 ServletContext 对象实例，可以获取整个工程的一些信息。
- config 对象 ServletConfig 对象实例，可以获取 Servlet 的配置信息
- out 对象 输出流。
- page 对象 表示当前 Servlet 对象实例（无用，用它不如使用 this 对象）。

### 2.5. EL表达式的使用

#### 2.5.1. EL表达式的语法

​		EL（Expression Language） 是为了使 JSP 写起来更加简单。表达式语言的灵感来自ECMAScript 和 XPath 表达式语言，它提供了在 JSP 中简化表达式的方法，让 Jsp 的代码更加简化。

```
语法结构非常简单： ${expression}
```

​		EL 表达式一般操作的都是<font color = "red">域对象中的数据</font>，操作不了局部变量。

​		域对象的概念在 JSP 中一共有四个：pageContext, request, session, application；范围依次是，本页面，一次请求， 一次会话，整个应用程序。
当需要指定从某个特定的域对象中查找数据时可以使用四个域对象对应的空间对象，分别是：pageScope,requestScope, sessionScope, applicationScope。而 EL 默认的查找方式为从小到大查找，找到即可。当域对象全找完了还未找到则返回空字符串""。

#### 2.5.2. EL表达式的使用

##### 2.5.2.1. 获取数据

**设置域对象中的数据**

```jsp
<%
  pageContext.setAttribute("uname","zhangsan"); // page作用域
  request.setAttribute("uname","lisi"); // request作用域
  session.setAttribute("uname","wangwu"); // session作用域
  application.setAttribute("uname","zaholiu"); // application
%>
```

**获取域对象的值**

```jsp
<%-- 获取域对象中的数据：默认查找方式为从小到大，找到即止。若四个范围都未找到，则返回空字符串。--%>
${uname} <!-- 输出结果为：zhangsan -->
```

**获取指定域对象的值**

```jsp
${pageScope.uname} <!-- page作用域 -->
${requestScope.uname} <!-- request作用域 -->
${sessionScope.uname} <!-- session作用域 -->
${applicationScope.uname} <!-- application作用域 -->
```

**获取List**

```jsp
<%
List<String> list = new ArrayList<String>();
list.add("aaa");
list.add("bbb");
list.add("ccc");
request.setAttribute("list", list);
%>
<%--
  获取List中指定下标的数据
    	${list[下标] }
    获取集合的长度
    	${list.size()}
    注：
       list代表的是存在域对象中的变量名（限域变量名）
--%>
${list[1] } 
```

**获取Map**

```jsp
<%
  Map map = new HashMap();
  map.put("aaa", "111");
  map.put("bbb", 2222);
  map.put("ccc-a", 333);
  request.setAttribute("map", map);
%>
<%--
  获取Map中指定值
  	 ${map["key"] } 或 ${map.key }
	注：
		map代表的是存在域对象中的变量名（限域变量名）
--%>	
${map.aaa }
${map["bbb"]}
```

**获取JavaBean对象**
User.java

```java
public class User {
  private Integer userId;
  private String uname;
  private String upwd;
  public Integer getUserId() {
    return userId;
 }
  public void setUserId(Integer userId) {
    this.userId = userId;
 }
  public String getUname() {
    return uname;
 }
  public void setUname(String uname) {
    this.uname = uname;
 }
    public String getUpwd() {
    return upwd;
 }
  public void setUpwd(String upwd) {
    this.upwd = upwd;
 }
}
```

```jsp
<%
  User user = new User();
  user.setUserId(1);
  user.setUname("zhangsan");
  user.setUpwd("123456");
  request.setAttribute("user",user);
%>
<%-- JavBean中的属性字段需要提供get方法 --%>
${user} <%-- 获取对象 --%>
${user.uname} 或 ${user.getUname()} <%--获取对象中的属性--%>
```

##### 2.5.2.2. empty

```jsp
<%--
  empty
 	判断域对象是否为空。为空，返回true；不为空返回false；
 		${empty 限域变量名 }
	判断对象是否不为空。
		${!empty 限域变量名 }
--%>
${empty uname}
${empty list}
${empty map}
${empty user}
```

## 3. JSTL

### 3.1. 标签的使用

```jsp
<%--
    JSTL的使用
        1. 拷贝jar包
        2. 通过taglib指令，引入标签库
--%>
<%-- 核心标签库 --%>
<%@taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%>
<%-- 格式化标签库 --%>
<%@taglib uri="http://java.sun.com/jsp/jstl/fmt" prefix="fmt"%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
```

### 3.2. 条件动作标签

#### 3.2.1. if 标签

##### 3.2.1.1. 语法格式

```jsp
<c:if test="<boolean>" var="<string>" scope="<string>">
 ...
</c:if>
```

##### 3.2.1.2. 属性

​		if 标签有如下属性：

| 属性  | 描述                                                       | 是否必要 | 默认值 |
| ----- | ---------------------------------------------------------- | -------- | ------ |
| test  | 条件                                                       | 是       | 无     |
| var   | 用于存储条件结果的变量（限域变量名）                       | 否       | 无     |
| scope | var属性的作用域
可取值：page\|request\|session\|application | 否       | page   |

```jsp
%
    int num = 10;
    request.setAttribute("num",num);
    int score = 59;
    request.setAttribute("score",score);
%>
<c:if test = "${num>1}">
    <p>大于1</p>
</c:if>

<c:if test = "${score<60}">
    <p>不及格</p>
</c:if>
<c:if test = "${score>90}">
    <p>牛XXX</p>
</c:if>
```

注： JSTL中没有else标签，为了模拟 else 的情景，需要使用两个 if 标签，并且这两个标签为相反的条件。

#### 3.2.2. choose、when 和 otherwise 标签

​		choose 和 when 标签的作用与 Java 中的 switch 和 case 关键字相似，用于在众多选项中做出选择。也就是说：他们为相互排斥的条件式执行提供相关内容。
​		switch语句中有case，而choose标签中对应有when，switch语句中有default，而choose标签中有otherwise。

##### 3.2.2.1. 语法格式

```jsp
<c:choose>
  <c:when test="<boolean>">
   ...
  </c:when>
  <c:when test="<boolean>">
   ...
  </c:when>
 ...
 ...
  <c:otherwise>
   ...
  </c:otherwise>
</c:choose>
```

##### 3.2.2.2. 属性

- choose标签没有属性。
- when标签只有一个test属性。
- otherwise标签没有属性。

```jsp
<%--
    choose、when、otherwise标签
        1. choose标签与otherwise标签没有属性，when标签必须有test属性
        2. choose标签中至少有一个when标签
        3. otherwise标签必须放在最后一个when标签之后
        4. otherwise标签在所有的when标签不执行时才会执行
        5. choose标签只能包含when和otherwise标签，when和otherwise标签中可以嵌套其他标签

--%>
<c:choose>
    <c:when test="${score<60}">
        <p>不及格</p>
    </c:when>
    <c:when test="${score>=60 && score<=100}">
        <p>及格</p>
    </c:when>
    <c:otherwise>
        <p>成绩不合法</p>
    </c:otherwise>
</c:choose>
```

### 3.3. 迭代标签

forEach 是将一个主体内容迭代多次，或者迭代一个对象集合。可以迭代的对象包括所有的 java.util.Collection 和
java.util.Map 接口的实现，以及对象或者基本类型的数组。他还可 以迭代 java.util.Iterator 和 java.util.Enumeration,
但不能在多个动作指令中使用 Iterator 或者 Enumeration,因为 Iterator 或者 Enumeration 都不能重置（reset）。 各
属性含义如下：

#### 3.3.1. forEach标签

##### 3.3.1.1. 语法格式

```
<c:forEach
  items="<object>"
  begin="<int>"
  end="<int>"
  step="<int>"
  var="<string>"
  varStatus="<string>">
</c:forEach> 
```

##### 3.3.1.2. 属性

| 属性      | 描述                                       | 是否必要 | 默认值       |
| --------- | ------------------------------------------ | -------- | ------------ |
| items     | 要被循环的数据                             | 否       | 无           |
| begin     | 开始的元素（0=第一个元素，1=第二个元素）   | 否       | 0            |
| end       | 最后一个元素（0=第一个元素，1=第二个元素） | 否       | Last element |
| step      | 每一次迭代的步长                           | 否       | 1            |
| var       | 代表当前条目的变量名称                     | 否       | 无           |
| varStatus | 代表循环状态的变量名称                     | 否       | 无           |

forEach varStatus 属性

- index: 当前这次迭代从 0 开始的迭代索引
- count: 当前这次迭代从 1 开始的迭代计数
- first: 用来表明当前这轮迭代是否为第一次迭代的标志
- last: 用来表明当前这轮迭代是否为最后一次迭代的标志

```jsp
<c:forEach begin="开始数" end="结束数" step="迭代数" var="限域变量名">
    
</c:forEach>
<c:forEach  var = "i" begin = "1" end = "10">
    ${i}
</c:forEach>
<!-- 遍历主体内容多次 -->
<c:forEach begin="0" end="10" var="i" >
 标题${i }<br>
</c:forEach>
```

​		循环集合

```jsp
<%
    List<String> strings = new ArrayList<>();
    strings.add("aaa");
    strings.add("bbb");
    strings.add("ccc");
    request.setAttribute("list",strings);
%>
<c:forEach var="str" items="${strings}">
    ${str}
</c:forEach>
<!-- 遍历Map -->
<%
  Map<String,Object> map = new HashMap<String,Object>();
  map.put("map1", "aaa");
  map.put("map2", "bbb");
  map.put("map3", "ccc");
  pageContext.setAttribute("map", map);
%>
<c:forEach items="${map }" var="mymap">
 键：${mymap.key }-值：${mymap.value } <br>
</c:forEach>
```

### 3.4. 格式化动作标签

​		STL 提供了格式化和解析数字和日期的标签,我们讨论里面有：formatNumber、formatDate、parseNumber及parseDate。

#### 3.4.1. formatNumber标签

#### 3.4.2. formatDate标签

​		formatDate标签用于使用不同的方式格式化日期。（将Date型数据转换成指定格式的字符串类型。）

##### 3.4.2.1. 语法格式

```jsp
<fmt:formatDate
 value="<string>"
 type="<string>"
 dateStyle="<string>"
 timeStyle="<string>"
 pattern="<string>"
 timeZone="<string>"
 var="<string>"
 scope="<string>"/>
```

##### 3.4.2.2. 属性

| 属性      | 描述                                  | 是否必要 | 默认值     |
| --------- | ------------------------------------- | -------- | ---------- |
| value     | 要显示的日期                          | 是       | 无         |
| type      | DATE, TIME, 或 BOTH                   | 否       | date       |
| dateStyle | FULL, LONG, MEDIUM, SHORT, 或 DEFAULT | 否       | default    |
| timeStyle | FULL, LONG, MEDIUM, SHORT, 或 DEFAULT | 否       | default    |
| pattern   | 自定义格式模式                        | 否       | 无         |
| timeZone  | 显示日期的时区                        | 否       | 默认时区   |
| var       | 存储格式化日期的变量名                | 否       | 显示在页面 |
| scope     | 存储格式化日志变量的范围              | 否       | 页面       |

```jsp
<%
request.setAttribute("myDate", new Date());
%>
${myDate } <br/>
<fmt:formatDate value="${myDate }" /><br/>
<fmt:formatDate value="${myDate }" type="date"/><br/>
<fmt:formatDate value="${myDate }" type="time"/><br/>
<fmt:formatDate value="${myDate }" type="both"/><br/>
<fmt:formatDate value="${myDate }" type="both" dateStyle="full"/><br/>
<fmt:formatDate value="${myDate }" type="both" dateStyle="long"/><br/>
<fmt:formatDate value="${myDate }" type="both" dateStyle="short"/><br/>
<fmt:formatDate value="${myDate }" type="both" timeStyle="full"/><br/>
<fmt:formatDate value="${myDate }" type="both" timeStyle="long"/><br/>
<fmt:formatDate value="${myDate }" pattern="HH:mm yyyy/MM/dd"/><br/>
```



#### 3.4.3. parseNumber标签

#### 3.4.4. parseDate标签