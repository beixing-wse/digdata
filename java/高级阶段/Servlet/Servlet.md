[TOC]



# Servlet

# 1.主要内容

![](G:\java\我的笔记\笔记图片\Servlet主要内容.png)

# 2.什么是Servlet

​		Servlet 是 Server 与 Applet 的缩写，是服务端小程序的意思。使用 Java 语言编写的服务器端程序，可以像生成动态的 WEB 页，Servlet 主要运行在服务器端，并由服务器调用执行， 是一种按照 Servlet 标准来开发的类。 是 SUN 公司提供的一门用于开发动态 Web 资源的技术。（言外之意：要实现 web 开发，需要实现 Servlet 标准）。

​		Servlet 本质上也是 Java 类，但要遵循 Servlet 规范进行编写，没有 main()方法，它的创建、使用、销毁都由 Servlet容器进行管理(如 Tomcat)。（言外之意：写自己的类，不用写 main 方法，别人自动调用）。
​		Servlet 是和 HTTP 协议是紧密联系的，其可以处理 HTTP 协议相关的所有内容。这也是 Servlet 应用广泛的原因之一。
​		提供了 Servlet 功能的服务器，叫做 Servlet 容器，其常见容器有很多，如 Tomcat, Jetty, WebLogic Server,WebSphere, JBoss 等等。

## 2.1Servlet的实现

```java
Servlet的实现
*      1. 新建web项目
*      2. 新建包，b并在包下新建普通java类
*      3. 集继承父类HttpServletRequest（需要web服务器）
*      4. 重写service方法
*      5. 接收请求，响应结果
*      6. 设置servlet的对外访问路径
```

### 2.1.1实现Servlet规范，继承HttpServlet

​		实现 Servlet 规范，即继承 HttpServlet 类，并到如响应的包，该类中已经完成了通信的规则，我们只需要进行业务的实现即可。

```java
package com.shsxt.servlet;
import javax.servlet.http.HttpServlet;
//继承HttpServlet 类
public class Servlet01 extends HttpServlet {
    
}
```



### 2.1.2重写service方法

​		满足 Servlet 规范只是让我们的类能够满足接收请求的要求，接收到请求后需要对请求进行分析，以及进行业务逻辑处理，计算出结果，则需要添加代码，在规范中有一个叫做 service的方法，专门用来做请求处理的操作，业务代码则可以写在该方法中。

### 2.1.3设置注解

​		在完成好了一切代码的编写后，还需要向服务器说明，特定请求对应特定资源。开发servlet项目，使用@WebServlet将一个继承于javax.servlet.http.HttpServlet 的类定义Servlet组件。在Servlet3.0中 可以使用@WebServlet注解将继承javaxjavax.servlet.http.HttpServlet的类标注为可以处理用户请求的Servlet。

### 2.1.4发布项目并启动服务

## 2.2doGet和doPost方法

```java
/**
 * doGet与doPost方法
 *
 * @author wse
 * @version 1.0
 * @date 2020/8/6 0006 14:34
 */
@WebServlet("/ser03")
public class Servlet03 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("get....");
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("post....");
    }
}
```



## 2.3Secvlet工作过程

1. 通过请求头获知浏览器访问的是哪个主机
2. 再通过请求行获取访问的是哪个一个web应用
3. 再通过请求行中的请求路径获知访问的是哪个资源
4. 通过获取的资源路径在配置中匹配到真实的路径，
5. 服务器会创建servlet对象，（如果是第一次访问时，创建servlet实例，并调用init方法进行初始化操作）
6. 调用service（request， response）方法来处理请求和响应的操作
7. 调用service完毕后返回服务器 由服务器讲response缓冲区的数据取出，以http响应的格式发送给浏览器

## 2.4生命周期

```java
生命周期
*      1. 创建及初始化阶段
*          init()
*          服务器自动调用，只会执行一次，在第一次访问Servlet时执行
*      2. 调用/服务阶段
*          service()
*          当有请求到达时，就会被执行。可以执行多次。
*      3. 销毁阶段
*          destory()
*          服务器自动调用，当Servlet被销毁（应用程序停止）时执行
```

​		Servlet没有 main()方法，不能独立运行，它的运行完全由 Servlet 引擎来控制和调度。 所谓生命周期，指的是servlet 容器何时创建 servlet 实例、何时调用其方法进行请求的处理、 何时并销毁其实例的整个过程。

- 实例和初始化时机

  请求到达容器时，容器查找该 servlet 对象是否存在，如果不存在，则会创建实例并进行初始化。HttpServlet 的 service()方法，会依据请求方式来调用 doGet()或者 doPost()方法。但是， 这两个 do 方法默认情况下，会抛出异常，需要子类去 override。

- 就绪/服务/调用阶段

  有请求到达容器，容器调用 servlet 对象的 service()方法，service()方法可多次调用

- 销毁时机

  容器关闭时（应用程序停止时），会将程序中的 Servlet 实例进行销毁。

```java
/**
 * 生命周期
 *  1、创建及初始化
 *      init()
 *      只会执行一次
 *  2、调用服务阶段
 *      service()
 *      请求到达时
 *  3、销毁阶段
 *      destory()
 *      服务器自动调用，当servle
 * @author wse
 * @version 1.0
 * @date 2020/8/6 0006 14:39
 */
@WebServlet("/ser04")
public class Servlet04  extends HttpServlet {
    /**
     * 服务方法
     * @param req
     * @param resp
     * @throws ServletException
     * @throws IOException
     */
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("Service....");
    }

    /**
     * 销毁方法
     */
    @Override
    public void destroy() {
        System.out.println("destroy....");

    }

    /**
     * 初始化方法
     * @throws ServletException
     */
    @Override
    public void init() throws ServletException {
        System.out.println("init....");
    }
}
```

 Tomcat 与 Servlet 的工作过程：

![image-20200806192407117](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200806192407117.png)

1. Web Client 向 Servlet 容器（Tomcat）发出 Http 请求
2. Servlet 容器接收 Web Client 的请求
3. Servlet 容器创建一个 HttpServletRequest 对象，将 Web Client 请求的信息封装到这个对象 中
4. Servlet 容器创建一个 HttpServletResponse 对象
5. Servlet 容器调HttpServlet 对象service 方法，把 Request 与 Response 作为参数，传给 HttpServlet
6. HttpServlet 调用 HttpServletRequest 对象的有关方法，获取 Http 请求信息
7. HttpServlet 调用 HttpServletResponse 对象的有关方法，生成响应数据
8. Servlet 容器把 HttpServlet 的响应结果传给 Web Client

# 3.HttpServletRequest对象

​		HttpServletRequest 对象：主要作用是用来接收客户端发送过来的请求信息，例如：请求的参数，发送的头信息等都属于客户端发来的信息，service()方法中形参接收的是 HttpServletRequest 接口的实例化对象，表示该对象主要应用在 HTTP 协议上，该对象是由 Tomcat 封装好传递过来。HttpServletRequest 是 ServletRequest 的子接口，ServletRequest 只有一个子接口，就是 HttpServletRequest。既然只有一个子接口为什么不将两个接口合并为一个？
​		从长远上讲：现在主要用的协议是 HTTP 协议，但以后可能出现更多新的协议。若以后想要支持这种新协议，只需要直接继承 ServletRequest 接口就行了。
在 HttpServletRequest 接口中，定义的方法很多，但都是围绕接收客户端参数的。但是怎么拿到该对象呢？不需要，直接在 Service 方法中由容器传入过来，而我们需要做的就是取出对象中的数据，进行分析、处理。

## 3.1. 接收请求

### 3.1.1常用方法

```java
/**
 * HttpServletRequest对象
 * 1、 常用方法
 *
 * @author wse
 * @version 1.0
 * @date 2020/8/6 0006 15:10
 */
@WebServlet("/ser01")
public class Servlet01 extends HttpServlet {
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //获取客户端请求的完整URL（从http开始，到?前面结束）
        StringBuffer requestURL = req.getRequestURL();
        System.out.println("获取客户端的完整URL = " + requestURL);//获取客户端的完整URL = http://localhost:8080/s02/ser01
        //获取客户端请求的部分URL(从站点名开始，到?前面结束）
        String requestURI = req.getRequestURI();
        System.out.println("获取客户端请求的部分URL = " + requestURI);//获取客户端请求的部分URL = /s02/ser01

        //获取请求行中的参数部分
        String queryString = req.getQueryString();
        System.out.println("获取请求行中的参数部分 = " + queryString);//获取请求行中的参数部分 = null
        //获取客户端的请求方式
        String method = req.getMethod();
        System.out.println("客户端的请求方式 = " + method);//客户端的请求方式 = GET

        //获取HTTP版本号
        String protocol = req.getProtocol();
        System.out.println("HTTP版本号 = " + protocol);//HTTP版本号 = HTTP/1.1

        //获取webapp名字（站点名）
        String contextPath = req.getContextPath();
        System.out.println("webapp名字（站点名） = " + contextPath);//webapp名字（站点名） = /s01

    }
}
```

### 3.1.2. 获取请求参数

- 通过参数名获取参数值  getParameter("参数名")，返回的是字符串
- 通过参数名获取请求的所有参数值 getParameterValues("参数名"),返回数组

```java
/**
 * HttpServletRequest对象
 *      获取请求参数
 *          通过参数名获取参数值  getParameter("参数名")，返回的是字符串
 *          通过参数名获取请求的所有参数值 getParameterValues("参数名"),返回数组
 *          http://localhost:8080/s02/ser01?name=admin&pwd=123456&hobby=sing&hobby=dance&hobby=rap
 * @author wse
 * @version 1.0
 * @date 2020/8/6 0006 20:05
 */
@WebServlet("/ser02")
public class Servlet02  extends HttpServlet{
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //获取请求参数
        String name = req.getParameter("name");
        //打印请求参数
        System.out.println("name = " + name);
        String pwd = req.getParameter("pwd");
        System.out.println("pwd = " + pwd);
    }
}
```

## 3.2. 请求乱码问题

```java
/**
 HttpServletRequest对象
 *      请求乱码问题
 *          Tomcat8及以上版本
 *              GET请求不乱码，POST会乱码
 *              处理请求乱码：设置请求的编码格式
 *                  request.setCharacterEncoding("UTF-8");
 *          Tomcat7及以下版本
 *              GET请求会乱码，POST会乱码
 * @author wse
 * @version 1.0
 * @date 2020/8/6 0006 20:05
 */
@WebServlet("/ser03")
public class Servlet03 extends HttpServlet{
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //设置编码格式
        req.setCharacterEncoding("UTF-8");
        String name = req.getParameter("name");
        System.out.println("name = " + name);
    }
}
```

## 3.3. 请求转发

​		请求转发，是一种服务器的行为，当客户端请求到达后，服务器进行转发，此时会将请求对象进行保存，地址栏中的 URL 地址不会改变，得到响应后，服务器端再将响应发送给客户端，从始至终只有一个请求发出。实现方式如下，达到多个资源协同响应的效果。

```java
request.getRequestDispatcher(url).forward(req,resp);
```

## 3.4. request作用域

通过该对象可以在一个请求中传递数据，作用范围：在一次请求中有效，即服务器跳转有效。

```java
// 设置域对象内容
request.setAttribute(String name, String value);
// 获取域对象内容
request.getAttribute(String name);
// 删除域对象内容
request.removeAttribute(String name);
```

request 域对象中的数据在一次请求中有效，则经过请求转发，request 域中的数据依然存在，则在请求转发的过程
中可以通过 request 来传输/共享数据。

# 4.HttpServletResponse对象

​		Web服务器收到客户端的http请求，会针对每一次请求，分别创建一个用于代表请求的 request 对象和代表响应的response 对象。

​		request 和 response 对象代表请求和响应：获取客户端数据，需要通过 request 对象；向客户端输出数据，需要通过 response 对象。
​		HttpServletResponse 的主要功能用于服务器对客户端的请求进行响应，将 Web 服务器处理后的结果返回给客户端。service()方法中形参接收的是 HttpServletResponse 接口的实例化对象，这个对象中封装了向客户端发送数据、发送响应头，发送响应状态码的方法。

## 4.1. 响应数据

- getWriter() 获取字符流(只能响应回字符)
- getOutputStream() 获取字节流(能响应一切数据)

## 4.2. 响应乱码问题

出现原因：这是因为服务器响应的数据也会经过网络传输，服务器端有一种编码方式，在客户端也存在一种编码方式，当两端使用的编码方式不同时则出现乱码。

解决方案：保证发送端和接收端的编码一致

```java
/**
 * HttpServletResponse对象
 *      向应数据
 *          getWriter() 字符输出流（只能响应字符）
 *          getOutputStream() 字节输出流（能响应一切数据）
 *
 *          两者不能同时使用
 *          响应乱码问题
 *          乱码原因
 *              服务器响应数据时，会通过网络传输，服务端有一种编码格式，客户端也有一种编码格式。
 *              当两种编码格式不一致或编码格式不支持中文时则出现乱码。
 *
 *              getWriter()的字符乱码
 *  	        对于 getWriter()获取到的字符流，响应中文必定出乱码，由于服务器端在进行编码时默认会使用 ISO-8859-1 格式的编码，
 *              该编码方式并不支持中文。
 *              getOutputStream()字节乱码
 *              对于 getOutputStream()方式获取到的字节流，响应中文时，由于本身就是传输的字节， 所以此时可能出现乱码，也可能正确显示。
 *
 *          解决方案
 *              设置服务端与客户端的编码格式一致，且支持中文。
 *                   同时设置服务端与客户端的编码格式
 *                   response.setContentType("text/html;charset=UTF-8");
 *
 * @author wse
 * @version 1.0
 * @date 2020/8/6 0006 16:30
 */
@WebServlet("/ser05")
public class Servlet05 extends HttpServlet {
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //设置服务端编码格式
//        resp.setCharacterEncoding("UTF-8");
//        //设置客户端编码格式
//        resp.setHeader("content-type","text/html;charset=UTF-8");

        //以上两句用一下这句代替
        resp.setContentType("text/html;charset=UTF-8");


        //字符输出流,没有标题效果
        PrintWriter writer = resp.getWriter();
        writer.write("<h2>Hello 中国</h2>");
        writer.flush();
        writer.close();


        //字节输出流，不可以输出字符串 两个只显示一个，不乱码
//        ServletOutputStream outputStream = resp.getOutputStream();
//        outputStream.write("<h2>Hello  中国</h2>".getBytes());
//        outputStream.flush();
//        outputStream.close();
    }
}
```

```java
// 总结设置客户端与服务端的编码
response.setContentType("text/html;charset=UTF-8");
```

​		总结：要想解决响应的乱码，只需要保证使用支持中文的编码格式。并且保证服务器端 和客户端使用相同的编码
方式即可。

## 4.3. 重定向

​		重定向是一种服务器指导，客户端的行为。客户端发出第一个请求，被服务器接收处理后，服务器会进行响应，在响应的同时，服务器会给客户端一个新的地址（下次请求的地址 response.sendRedirect(url);），当客户端接收到响应后，会立刻、马上、自动根据服务器给的新地址发起第二个请求，服务器接收请求并作出响应，重定向完成。从描述中可以看出重定向当中有两个请求存在，并且属于客户端行为。

## 4.4请求转发与重定向的区别

```
请求转发与重定向的区别
*      1. 请求转发是服务端跳转，重定向是客户端跳转。
*      2. 请求转发只有一次请求，从重定向存在两次请求。
*      3. 请求转发可以共享request作用域的数据，重定向不可以。
*      4. 请求转发地址栏不发生改变，重定向的地址会改变。
*      5. 请求转发只能转发到当前项目下的资源，重定向可以跳转到任意页面（可以跨域）。
```

```java
/**
 * 重定向
 *      服务端指导，客户端跳转行为
 *      地址栏发生改变，存在两次请求，request作用域不共享
 *
 *  请求转发与重定向的区别
 *      1. 请求转发是服务端跳转，重定向是客户端跳转。
 *      2. 请求转发只有一次请求，从重定向存在两次请求。
 *      3. 请求转发可以共享request作用域的数据，重定向不可以。
 *      4. 请求转发地址栏不发生改变，重定向的地址会改变。
 *      5. 请求转发只能转发到当前项目下的资源，重定向可以跳转到任意页面（可以跨域）。
 * @author wse
 * @version 1.0
 * @date 2020/8/6 0006 16:50
 */
@WebServlet("/ser06")
public class Servlet06 extends HttpServlet {
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("Servlet06...");

        //设置作用域
        System.out.println("获取作用域" + req.getAttribute("name"));

        //重定向到页面
//        resp.sendRedirect("login.jsp");
        //重定向到Servlet
        resp.sendRedirect("ser07");

    }
}
```

# 5、Cookie对象

​		Cookie是浏览器提供的一种技术，通过服务器的程序能将一些只须保存在客户端，或者在客户端进行处理的数据，放在本地的计算机上，不需要通过网络传输，因而提高网页处理的效率，并且能够减少服务器的负载，但是由于Cookie 是服务器端保存在客户端的信息， 所以其安全性也是很差的。例如常见的记住密码则可以通过 Cookie 来实现。

​		java中专门操作Cookie的类 javax.servlet.http.Cookie。

​		Cokkie的格式：键值对用“=”链接，多个键值对间通过“；”隔开。

## 5.1Cokkie的创建和发送

​		创建cokkie对象，要想将 Cookie 随响应发送到客户端，需要先添加到response 对象中，response.addCookie(cookie);此时该 cookie 对象则随着响应发送至了客户端。在浏览器上可以看见。

```java
//创建Cookie对象
Cookie cookie = new Cookie("username", "admin");
Cookie cookie02 = new Cookie("userpwd", "123456");
//发送，响应给浏览器
resp.addCookie(cookie);
resp.addCookie(cookie02);
```



## 5.2Cokkie的获取

​		在服务器端只提供了一个 getCookies()的方法用来获取客户端回传的所有 cookie 组成的一个数组，如果需要获取单个 cookie 则需要通过遍历，getName()获取 Cookie 的名称，getValue()获取 Cookie 的值。

```java
//获取cookie数组
Cookie[] cookies = req.getCookies();
//判断
if (cookies != null && cookies.length > 0) {
    //遍历
    for (Cookie cookie : cookies) {
        //System.out.println("键" + cookie.getName() + "," + "值" + cookie.getValue());
        //获取时通过URLDecoder.decode()解码
        String name = URLDecoder.decode(cookie.getName());
        String value = URLDecoder.decode(cookie.getValue());
        System.out.println("键：" + name  + "，值：" + value);

        //判断，获取指定的cookie对象
        if ("username".equals(cookie.getName())) {
            System.out.println("当前cookie的值为："+cookie.getName());
        }
    }
}
```

## 5.3. Cookie设置到期时间	

​		Cookie到期时间默认为当前浏览器关闭即失效。我们可以手动设定 cookie 的有效时间（通过到期时间计算），通过 setMaxAge(int time);方法设定 cookie 的最大有效时间，以秒为单位。

**到期时间的取值**

- 负整数

  若为负数，表示不存储该 cookie。

  cookie 的 maxAge 属性的默认值就是-1，表示只在浏览器内存中存活，一旦关闭浏览器窗口，那么 cookie 就会消失。

- 正整数

  若大于 0 的整数，表示存储的秒数。
  表示 cookie 对象可存活指定的秒数。当生命大于 0 时，浏览器会把 Cookie 保存到硬盘上，就算关闭浏览器，就算重启客户端电脑，cookie 也会存活相应的时间。

- 0

  若为 0，表示删除该 cookie。
  cookie 生命等于 0 是一个特殊的值，它表示 cookie 被作废！也就是说，如果原来浏览器已经保存了这个Cookie，那么可以通过 Cookie 的 setMaxAge(0)来删除这个 Cookie。 无论是在浏览器内存中，还是在客户端硬盘上都会删除这个 Cookie。

```java
//创建cookie
Cookie cookie = new Cookie("aa", "AA");
//设置cookie的有效期
//cookie.setMaxAge(-1);//关闭浏览器就失效
//设置有效期20秒
cookie.setMaxAge(20);
//响应cookie
resp.addCookie(cookie);

Cookie cookie1 = new Cookie("name", "zs");
//设置有效期一周
cookie1.setMaxAge(7*24*3600);
//响应cookie
resp.addCookie(cookie1);
```

## 5.4Cookie的注意点

- 不跨浏览器，不跨电脑.
- 不支持中文
   *          如果需要存储中文，如果有中文则通过 URLEncoder.encode()来进行编码，获取时通过URLDecoder.decode()来进行解码。

-  同名Cookie问题
  如果服务器端发送重复的Cookie那么会覆盖原有的Cookie。

- 浏览器存放Cookie的数量
  不同的浏览器对Cookie也有限定，Cookie的存储有是上限的。Cookie是存储在客户端（浏览器）的，而且一
  般是由服务器端创建和设定。后期结合Session来实现回话跟踪。

## 5.5Cookie的路径

​		Cookie的setPath设置cookie的路径，这个路径直接决定服务器的请求是否会从浏览器中加载某些cookie。

```java
//1、当前项目下的资源可获取Cookie对象 （默认不设置Cookie的path）
Cookie cookie1 = new Cookie("a1", "A1");
cookie1.setPath("/s03");
//2、指定项目下的资源可获取Cookie对象
Cookie cookie2 = new Cookie("a2", "A2");
cookie2.setPath("/s03/cook02");
//3、当前服务器下任何项目的任意资源都可获取Cookie对象
Cookie cookie3 = new Cookie("a3", "A3");
cookie3.setPath("/");
//4、指定目录下的资源可获取Cookie对象
Cookie cookie4 = new Cookie("a4", "A4");
cookie4.setPath("/s04");

//响应cookie
resp.addCookie(cookie1);
resp.addCookie(cookie2);
resp.addCookie(cookie3);
resp.addCookie(cookie4);
```

# 6.HttpSession对象

​		HttpSession对象是 javax.servlet.http.HttpSession 的实例，该接口并不像 HttpServletRequest 或 HttpServletResponse还存在一个父接口，该接口只是一个纯粹的接口。这因为 session 本身就属于 HTTP 协议的范畴。

​		对于服务器而言，每一个连接到它的客户端都是一个 session.

​		session 无论客户端还是服务器端都可以感知到，若重新打开一个新的浏览器，则无法取得之前设置的 session，因为每一个 session 只保存在当前的浏览器当中，并在相关的页面取得。

​		Session 的作用就是为了标识一次会话，或者说确认一个用户；并且在一次会话（一个用户的多次请求）期间共享数据。我们可以通过 request.getSession()方法，来获取当前会话的 session 对象。

```java
// 如果session对象存在，则获取；如果session对象不存在，则创建
HttpSession session = request.getSession();
```

## 6.1标识符JESSIONID

​		Session 既然是为了标识一次会话，那么此次会话就应该有一个唯一的标志，这个标志就是 sessionId。

​		每当一次请求到达服务器，如果开启了会话，服务器就会先查看是否从客户端回传一个名为JESSIONID的cookie，如果没有则认为这时一次新的会话，会创建一个新的session对象，并用唯一的sessionid作为此次会话的标识。如果有JESSIONID这个cookie回传，服务器就会根据JESSIONID去查看是否有id为JESSIONID的session对象，如果找到了session对象，则认为这不是一次新的会话，返回这个session对象。如果没有id为JESSIONID的session的对象，则重新创建一个session对象，返回session对象，数据共享。

​		这里提到一个叫做 JSESSIONID 的 cookie，这是一个比较特殊的 cookie，当用户请求服务器时，如果访问了session，则服务器会创建一个名为 JSESSIONID，值为获取到的 session（无论是获取到的还是新创建的）的sessionId 的 cookie 对象，并添加到 response 对象中，响应给客户端，有效时间为关闭浏览器。
​		所以 Session 的底层依赖 Cookie 来实现

```java
//获取session对象
HttpSession session = req.getSession();
//会话标识符
System.out.println("会话标识符 = " + session.getId());

System.out.println("会话创建时间：" +session.getCreationTime());

System.out.println("会话的最后一次访问时间" + session.getLastAccessedTime());

System.out.println("是否是新的会话"+ session);
```

## 6.2. session域对象

​		Session 用来表示一次会话，在一次会话中数据是可以共享的，这时 session 作为域对象存在，可以通过setAttribute(name,value) 方法向域对象中添加数据，通过 getAttribute(name) 从域对象中获取数据，通过removeAttribute(name) 从域对象中移除数据。

```java
//获取session对象
HttpSession session = req.getSession();
//设置session域对象
session.setAttribute("name","zhangsan");
//设置request作用域
req.setAttribute("name1","lisi");
//请求转发
req.getRequestDispatcher("sess03");
```

​		数据存储在 session 域对象中，当 session 对象不存在了，或者是两个不同的 session 对象时，数据也就不能共享了。这就不得不谈到 session 的生命周期。

## 6.3. session对象的销毁

### 6.3.1. 默认时间到期

​		当客户端第一次请求 servlet 并且操作 session 时，session 对象生成，Tomcat 中 session 默认的存活时间为 30min，即你不操作界面的时间，一旦有操作，session 会重新计时。那么 session 的默认时间可以改么？答案是肯定的。可以在 Tomcat 中的 conf 目录下的 web.xml 文件中进行修改。

```jsp
<!-- session 默认的最大不活动时间。单位：分钟。 -->
<session-config>
<session-timeout>30</session-timeout>
</session-config>
```

### 6.3.2. 自己设定到期时间

​		当然除了以上的修改方式外，我们也可以在程序中自己设定 session 的生命周期，通过session.setMaxInactiveInterval(int) 来设定 session 的最大不活动时间，单位为秒。

```java
// 获取session对象
HttpSession session = request.getSession();
// 设置session的最大不活动时间
session.setMaxInactiveInterval(15); // 15秒
```

通过 getMaxInactiveInterval() 方法来查看当前 Session 对象的最大不活动时间。

```java
// 获取session的最大不活动时间
int time = session.getMaxInactiveInterval();
```

### 6.3.3. 立刻失效

​		或者我们也可以通过 session.invalidate() 方法让 session 立刻失效

```java
// 销毁session对象
session.invalidate();
```

### 6.3.4. 关闭浏览器

​		从前面的 JESSIONID 可知道，session 的底层依赖 cookie 实现，并且该 cookie 的有效时间为关闭浏览器，从而session 在浏览器关闭时也相当于失效了（因为没有 JSESSION 再与之对应）。

### 6.3.5. 关闭服务器

​		当关闭服务器时，session 销毁。Session 失效则意味着此次会话结束，数据共享结束。

# 7.ServletContext对象

​		每一个 web 应用都有且仅有一个ServletContext 对象，又称 Application 对象，从名称中可知，该对象是与应用程序相关的。在 WEB 容器启动的时候，会为每一个 WEB 应用程序创建一个对应的 ServletContext 对象。该对象有两大作用，第一、作为域对象用来共享数据，此时数据在整个应用程序中共享； 第二、该对象中保存了当前应用程序相关信息。例如可以通过 getServerInfo() 方法获取当前服务器信息 ，getRealPath(String path) 获取资源的真实路径等。

## 7.1. ServletContext对象的获取

获取 ServletContext 对象的途径有很多。比如：

```java
package com.shsxt.servlet;

import javax.servlet.ServletContext;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

/**
 * ServletContext对象
 * 每一个 web 应用都有且仅有一个ServletContext 对象，又称 Application 对象，
 * <p>
 * ServletContext对象的获取
 *      1. 通过 request 对象获取
 *          getServletContext();
 *      2. 通过 session 对象获取
 *          getSession().getServletContext();   
 *      3. 通过 servletConfig 对象获取，在 Servlet 标准中提供了 ServletConfig 方法
 *      4. 直接获取，Servlet 类中提供了直接获取 ServletContext 对象的方法
 *
 *      常用方法
 *      获取项目存放的真实路径     .getRealPath("/")
 *      获取当前服务器的版本信息    getServerInfo();
 *
 *      Servlet的三大域对象
 *          1. request域对象
 *              在一次请求中有效。请求转发有效，重定向失效。
*           2. session域对象
 *              在一次会话中有效。请求转发和重定向都有效，session销毁后失效。
 *          3. servletContext域对象
 *              在整个应用程序中有效。服务器关闭后失效。
 *
 * @author wse
 * @version 1.0
 * @date 2020/8/7 0007 11:35
 */
@WebServlet("/sess05")
public class Servlet05 extends HttpServlet {
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

        //1. 通过 request 对象获取	常用
        ServletContext servletContext = req.getServletContext();
        //2、通过 session 对象获取
        ServletContext servletContext1 = req.getSession().getServletContext();
        //3、通过 servletConfig 对象获取，
        ServletContext servletContext2 = getServletConfig().getServletContext();
        //4、直接获取，Servlet 类中提供了直接获取 ServletContext 对象的方法
        ServletContext servletContext3 = getServletContext();

        //常用方法
        System.out.println("项目存放的真实路径:" + req.getServletContext().getRealPath("/"));
        System.out.println("当前服务器的版本信息:" + req.getServletContext().getServerInfo());

    }
}
```

**Servlet的三大域对象**

1. request域对象
在一次请求中有效。请求转发有效，重定向失效。
2. session域对象
在一次会话中有效。请求转发和重定向都有效，session销毁后失效。
3. servletContext域对象
在整个应用程序中有效。服务器关闭后失效。

# 8、文件上传和下载

在上网的时候我们常常遇到文件上传的情况，例如上传头像、上传资料等；当然除了上传，遇见下载的情况也很
多，接下来看看我们 servlet 中怎么实现文件的上传和下载。

## 8.1. 文件上传

​		文件上传涉及到前台页面的编写和后台服务器端代码的编写，前台发送文件，后台接收并保存文件，这才是一个完
整的文件上传。

### 8.1.1. 前台页面	

​		在做文件上传的时候，会有一个上传文件的界面，首先我们需要一个表单，并且表单的请求方式为 POST；其次我们的 form 表单的 enctype 必须设为"multipart/form-data"，即 <font color="red">enctype="multipart/form-data"</font>，意思是设置表单的类型为文件上传表单。默认情况下这个表单类型是 "application/x-www-form-urlencoded", 不能用于文件上传。只有使用了multipart/form-data 才能完整地传递文件数据。

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>文件上传</title>
</head>
<body>
    <form action="uploadServlet" method="post" enctype="multipart/form-data">
        姓名：<input type="text" name="uname">
        文件：<input type="file" name="myfile">
        <button type="submit">提交</button>
    </form>
</body>
</html>
```

### 8.1.2. 后台实现

​		使用注解 @MultipartConfig 将一个 Servlet 标识为支持文件上传。 Servlet 将 multipart/form-data 的 POST 请求封装成 Part，通过 Part 对上传的文件进行操作。

```java
/**
 * 文件上传
 * @author wse
 * @version 1.0
 * @date 2020/8/7 0007 12:30
 */
@MultipartConfig
@WebServlet("/uploadServlet")
public class UploadServlet extends HttpServlet {
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //设置编码格式
        req.setCharacterEncoding("UTF-8");
        //得到文件标签的name
        String uname = req.getParameter("uname");//uname代表表单元素input的name属性值
        System.out.println("uname = " + uname);
        //文件上传
        Part myfile = req.getPart("myfile");
        //通过Part对象，获取上传的文件名
        String fileName = myfile.getSubmittedFileName();
        //进行判断，可能没有上传文件
        if (fileName != null||"" !=fileName.trim()) {
            //获取上传文件需要存放的路径
            String realPath = req.getServletContext().getRealPath("/");
            //将文件上传的指定的位置
            myfile.write(realPath+fileName);

        }
    }
}
```

## 8.2. 文件下载

​		文件下载，即将服务器上的资源下载（拷贝）到本地，我们可以通过两种方式下载。第一种是通过超链接本身的特性来下载；第二种是通过代码下载。

### 8.2.1. 超链接下载

​		当我们在 HTML 或 JSP 页面中使用a标签时，原意是希望能够进行跳转，但当超链接遇到浏览器不识别的资源时会自动下载；当遇见浏览器能够直接显示的资源，浏览器就会默认显示出来，比如 txt、png、jpg 等。当然我们也可以通过 download 属性规定浏览器进行下载。但有些浏览器并不支持。
​		默认下载	

```jsp
<!-- 当超链接遇到浏览器不识别的资源时，会自动下载 -->
<a href="test.zip">超链接下载</a>
```

​		指定 download 属性下载

```jsp
<!-- 当超链接遇到浏览器识别的资源时，默认不会下载。通过download属性可进行下载 -->
<a href="test.txt" download>超链接下载</a>
```

​		download 属性可以不写任何信息，会自动使用默认文件名。如果设置了download属性的值，则使用设置的值做为文件名。当用户打开浏览器点击链接的时候就会直接下载文件。

### 8.2.2. 后台实现下载

实现步骤
1. 需要通过 response.setContentType 方法设置 Content-type 头字段的值， 为浏览器无法使用某种方式或激活某个程序来处理的 MIME 类型，例 如 "application/octet-stream" 或 "application/x-msdownload" 等。
2. 需要通过 response.setHeader 方法设置 Content-Disposition 头的值 为 "attachment;filename=文件名".
3. 读取下载文件，调用 response.getOutputStream 方法向客户端写入附件内容。

```java
/**
 * @author wse
 * @version 1.0
 * @date 2020/8/7 0007 14:50
 */
@WebServlet("/downServlet")
public class DownServlet extends HttpServlet {
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //设置编码格式
        req.setCharacterEncoding("UTF-8");
        String fileName = req.getParameter("fileName");
        if (fileName==null || "".equals(fileName.trim())){
            System.out.println("请输入文件名!");
            return;
        }

        String filePath = req.getServletContext().getRealPath("/");

        File file = new File(filePath + fileName);
        if (file.exists()&&file.isFile()){
            // 设置响应类型 (浏览器无法使用某种方式或激活某个程序来处理的类型)
            resp.setContentType("application/x-msdownload");
            // 设置头信息
            resp.setHeader("Content-Disposition", "attachment;filename=" + fileName);

            //输入流
            FileInputStream in = new FileInputStream(file);

            //输出流
            ServletOutputStream out = resp.getOutputStream();
            //字节数组
            byte[] bytes = new byte[1024];
            //定义长度
            int len = 0;
            //循环输出
            while(-1!=(len= in.read(bytes))){
                //写出
                out.write(bytes,0,len);
            }
            //关闭资源
            out.close();
            in.close();

        }else{
            System.out.println("文件不存在");
        }
    }
}
```

