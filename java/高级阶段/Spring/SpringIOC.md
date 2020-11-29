# Spring

[TOC]

## 1、主要内容

![](G:\java\我的笔记\笔记图片\Spring主要内容.png)

## 2、Spring5框架

### 2.1Spring基本概念		

​		Spring 是众多开源java项⽬中的⼀员，<font color ="red">是基于分层的JavaEE应用的一站式轻量级开源框架</font>。使用Spring，JavaBean就可以实现许多以前要考EJB才能实现的功能。同样的功能，在EJB（EJB是sun的JavaEE服务器端组件模型，）中需要通过很多繁琐的配置和代码才能实现，而在Spring中却非常的优雅和简洁。

​		Spring的核心就是IOC（控制反转和依赖注入）和AOP（面向切面）两大技术。在项目的开发中能够轻松实现解耦，提高开发的效率。

​		<font color ="red">**Spring的优良特性**</font>

- **非侵入式**：基于Spring开发的应用中的对象可以不依赖于Spring的API

- **依赖注入**：DI——Dependency Injection，反转控制(IOC)最经典的实现。

- **面向切面编程**：Aspect Oriented Programming——AOP

- **容器**：Spring是一个容器，因为它包含并且管理应用对象的生命周期

- **组件化**：Spring实现了使用简单的组件配置组合成一个复杂的应用。在 Spring 中可以使用XML和Java注解组合这些对象。

  <font color ="red">**一站式**</font>

  在IOC和AOP的基础上可以整合各种企业应用的开源框架和优秀的第三方类库（实际上Spring 自身也提供了表述层的SpringMVC和持久层的Spring JDBC）。

  Spring模块

  ![](G:\java\我的笔记\笔记图片\Spring模块 .bmp)

### 2.2. Spring 源码架构

​		Spring 总共⼤约有20个模块，由1300多个不同的⽂件构成。⽽这些组件被分别整合在<font color="blue">核⼼容器（CoreContainer）、Aop（Aspect Oriented Programming）和设备⽀持（Instrmentation）、数据访问及集成Data Access/Integeration）、Web、报⽂发送（Messaging）、单元测试</font>6个模块<集合中。
1. <font color="red">核⼼容器</font>：<font color="red">Spring-beans</font> 和<font color="red">Spring-core</font> 模块是Spring 框架的核⼼模块，包含控制反转（Inversionof Control, IoC）和依赖注⼊（Dependency Injection, DI）,核⼼容器提供Spring 框架的基本功能。核⼼容器的主要组件是BeanFactory，⼯⼚模式的实现。<font color="red">BeanFactory 使⽤控制反转（IOC）思想将应⽤程序的配置和依赖性规范与实际的应⽤程序代码分开</font>。

   Spring 上下⽂Spring Context：Spring 上下⽂是⼀个配置⽂件，向Spring 框架提供上下⽂信息。
   Spring 上下⽂包括企业服务，例如JNDI、EJB、电⼦邮件、国际化、校验和调度功能。

   Spring-Expression 模块是统⼀表达式语⾔（unified EL）的扩展模块，可以查询、管理运⾏中的对象，同时也⽅便的可以调⽤对象⽅法、操作数组、集合等。它的语法类似于传统EL，但提供了额外的功能，最出⾊的要数函数调⽤和简单字符串的模板函数。

2. Spring-AOP：Spring-aop是Spring的另⼀个核⼼模块, 在Spring中，他是以JVM的动态代理技术为基础，然后设计出了⼀系列的Aop横切实现，⽐如前置通知、返回通知、异常通知等。通过其配置管理特性，Spring AOP 模块直接将⾯向切⾯的编程功能集成到了Spring 框架中。所以，可以很容易地使Spring 框架管理的任何对象⽀持AOP。

3. Spring Data Access(数据访问)：由Spring-jdbc、Spring-tx、Spring-orm、Spring-jms和Spring-oxm 5个模块组成，<font color="red">Spring-jdbc 模块是Spring 提供的JDBC抽象框架的主要实现模块，⽤于简化SpringJDBC</font>。

  Spring-tx 模块是<font color="red">SpringJDBC事务控制实现模块</font>。使⽤Spring框架，它对事务做了很好的封装，通过它的Aop配置，可以灵活的配置在任何⼀层。

  Spring-Orm 模块是ORM框架⽀持模块，主要集成hibernate, Java Persistence API (JPA) 和Java Data Objects (JDO) ⽤于资源管理、数据访问对象(DAO)的实现和事务策略。

  Spring-Jms 模块（Java Messaging Service）能够发送和接受信息。

  Spring-Oxm 模块主要提供⼀个抽象层以⽀撑OXM（OXM 是Object-to-XML-Mapping 的缩写，它是⼀个O/M-mapper，将java对象映射成XML 数据，或者将XML 数据映射成java 对象），例如：JAXB,Castor, XMLBeans, JiBX 和XStream 等。

4. Web 模块：由Spring-web、Spring-webmvc、Spring-websocket和Spring-webmvc-portlet 4个模块组成，Web 上下⽂模块建⽴在应⽤程序上下⽂模块之上，为基于Web 的应⽤程序提供了上下⽂。

  Web 模块还简化了处理多部分请求以及将请求参数绑定到域对象的⼯作。

5. 报⽂发送：即Spring-messaging模块。Spring-messaging是Spring4 新加⼊的⼀个模块，主要职责是为Spring 框架集成⼀些基础的报⽂传送应⽤。

6. 单元测试：即Spring-test模块。Spring-test模块主要为测试提供⽀持

### 2.3. Spring 框架环境搭建

#### 2.3.1. 环境要求

JDK 版本：
JDK 1.7 及以上版本
Spring版本：
Spring 5.x版本

#### 2.3.2. 新建Maven 项⽬

1. 创建Maven 的普通Java 项⽬

#### 2.3.3. 调整项⽬环境

1. 修改JDK 版本
2. 修改单元测试JUnit 版本
3. build标签中的pluginManagement标签

#### 2.3.4. 添加Spring 框架的依赖坐标

​		Maven仓库：https://mvnrepository.com/

```xml
<!-- 添加Spring框架的核⼼依赖-->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>5.2.4.RELEASE</version>
</dependency>

```



#### 2.3.5. 编写Bean 对象

#### 2.3.6. 添加Spring 配置⽂件

1. 在项⽬的src 下创建⽂件夹resources（Alt + insert）

2. . 将resources 标记为资源⽬录

3. 在src\main\resources ⽬录下新建spring.xml ⽂件，并拷⻉官⽹⽂档提供的模板内容到xml 中。
   配置bean 到xml 中，把对应bean 纳⼊到Spring 容器来管理
   spring.xml

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://www.springframework.org/schema/beans
                              https://www.springframework.org/schema/beans/spring-beans.xsd">
       <!--
           xmlns 即xml namespace xml使⽤的命名空间
           xmlns:xsi 即xml schema instance xml 遵守的具体规范
           xsi:schemaLocation 本⽂档xml遵守的规范官⽅指定
           -->
   <bean id="userService" class="com.xxxx.service.UserService"></bean>
   </beans>
   
   ```

4. 在spring.xml 中配置Bean 对象

   ```xml
   <!--
       id：bean对象的id，唯⼀标识。⼀般是Bean对象的名称的⾸字⺟⼩写
       class：bean对象的类路径
   -->
   <bean id="userService" class="com.xxxx.service.UserService"></bean>
   
   ```

#### 2.3.7. 加载配置⽂件，获取实例化对象

```java
package com.xxxx;
import com.xxxx.service.UserService;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;
public class App {
public static void main(String[] args) {
    // 获取Spring上下⽂环境(加载配置⽂件)
    ApplicationContext ac = new ClassPathXmlApplicationContext("spring.xml");
    // 通过getBean⽅法得到Spring容器中实例化好的Bean对象（实例化Bean对象）
    // userService代表的是配置⽂件中bean标签的id属性值
    UserService userService = (UserService) ac.getBean("userService");
    // 调⽤⽅法（使⽤实例化对象）
    userService.test();
    }
}

```



## 3、Spring IOC 容器Bean 对象实例化模拟

思路:
1. 定义Bean ⼯⼚接⼝，提供获取bean ⽅法
2. 定义Bean ⼯⼚接⼝实现类，解析配置⽂件，实例化Bean对象
3. 实现获取Bean ⽅法

### 3.1. 定义Bean 属性对象

```java
package com.xxxx.spring;
/**
* bean对象
* ⽤来接收配置⽂件中bean标签的id与class属性值
*/
public class MyBean {
    private String id; // bean对象的id属性值
    
    spring.xml
    private String clazz; // bean对象的类路径
    public MyBean() {
    }
    public MyBean(String id, String clazz) {
    this.id = id;
    this.clazz = clazz;
    }
    public String getId() {
    return id;
    }
    public void setId(String id) {
    this.id = id;
    }
    public String getClazz() {
    return clazz;
    }
    public void setClazz(String clazz) {
    this.clazz = clazz;
    }
}

```

### 3.2. 添加dom4j 坐标依赖

```xml
<!-- dom4j -->
<dependency>
    <groupId>dom4j</groupId>
    <artifactId>dom4j</artifactId>
    <version>1.6.1</version>
    </dependency>
    <!-- XPath -->
    <dependency>
    <groupId>jaxen</groupId>
    <artifactId>jaxen</artifactId>
    <version>1.1.6</version>
</dependency>

```



### 3.3. 准备⾃定义配置⽂件

spring.xml

```xml
<?xml version="1.0" encoding="utf-8" ?>
<beans>
<bean id="userService" class="com.xxxx.service.UserService"></bean>
<bean id="accountService" class="com.xxxx.service.AccountService"></bean>
</beans>
```



### 3.4. 定义Bean ⼯⼚接⼝

```java
package com.xxxx.spring;
/**
* Bean ⼯⼚接⼝定义
*/
public interface MyFactory {
    // 通过id值获取对象
    public Object getBean(String id);
}

```



### 3.5. 定义Bean 接⼝的实现类

```java
package com.xxxx.spring;
import org.dom4j.Document;
import org.dom4j.DocumentException;
import org.dom4j.Element;
import org.dom4j.XPath;
import org.dom4j.io.SAXReader;
import java.net.URL;
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
/**
* 模拟Spring的实现
* 1、通过构造器得到相关配置⽂件
* 2、通过dom4j解析xml⽂件，得到List 存放id和class
* 3、通过反射实例化得到对象Class.forName(类的全路径).newInstance(); 通过Map<id,Class>存
储
* 4、得到指定的实例化对象
*/
public class MyClassPathXmlApplicationContext implements BeanFactory {
    
    private Map beans = new HashMap(); // 实例化后的对象放⼊map
    private List<MyBean> myBeans; // 存放已读取bean 配置信息
    
    /* 1、通过构造器得到相关配置⽂件*/
    public MyClassPathXmlApplicationContext(String fileName) {
        
        /* 2、通过dom4j解析xml⽂件，得到List （存放id和class）*/
        this.parseXml(fileName);
        
        /* 3、通过反射实例化得到对象Class.forName(类路径).newInstance(); 通过Map存储*/
        this.instanceBean();
    }
    
    /**
    * 通过dom4j解析xml⽂件，得到List 存放id和class
    * 1、获取解析器
    * 2、得到配置⽂件的URL
    * 3、通过解析器解析xml⽂件（spring.xml）
    * 4、通过xpath语法，获取beans标签下的所有bean标签
    * 5、通过指定语法解析⽂档对象，返回集合
    * 6、判断集合是否为空，遍历集合
    * 7、获取标签元素中的属性
    * 8、得到Bean对象，将Bean对象设置到集合中
    * @param fileName
    */
    
    private void parseXml(String fileName) {
        // 1、获取解析器
        SAXReader reader = new SAXReader();
        // 2、得到配置⽂件的URL
        URL url = this.getClass().getClassLoader().getResource(fileName);
        try {
            // 3、通过解析器解析xml⽂件（spring.xml）
            Document document = reader.read(url);
            // 4、通过xpath语法，获取beans标签下的所有bean标签
            XPath xPath = document.createXPath("beans/bean");
            // 通过指定语法解析⽂档对象，返回集合
            List<Element> list = xPath.selectNodes(document);
            // 判断集合是否为空，遍历集合
            if (list != null && list.size() > 0) {
                    myBeans = new ArrayList<>();
                    for(Element el : list) {
                        // 获取标签元素中的属性
                        String id = el.attributeValue("id"); // id 属性值
                        String clazz = el.attributeValue("class"); // class 属性值
                        System.out.println(el.attributeValue("id"));
                        System.out.println(el.attributeValue("class"));
                        // 得到Bean对象
                        MyBean bean = new MyBean(id, clazz);
                        // 将Bean对象设置到集合中
                        myBeans.add(bean);
                    }
            	}
            } catch (DocumentException e) {
        		e.printStackTrace();
        	}
        }
    
        /**
        * 通过反射实例化得到对象
        * Class.forName(类的全路径).newInstance();
        * 通过Map<id,Class>存储
        */
        private void instanceBean() {
            // 判断bean集合是否为空，不为空遍历得到对应Bean对象
            if (myBeans != null && myBeans.size() > 0) {
                for (MyBean bean : myBeans){
                    try {
                    // 通过类的全路径实例化对象
                    Object object = Class.forName(bean.getClazz()).newInstance();
                    // 将id与实例化对象设置到map对象中
                    beans.put(bean.getId(), object);
                    } catch (Exception e) {
                    	e.printStackTrace();
                    }
                }
            }
        }
        /**
        * 通过key获取map中的指定value
        * @param id
        * @return
        */
        @Override
        public Object getBean(String id) {
            Object object = beans.get(id);
            return object;
        }
}

```



### 3.6. 测试⾃定义IOC 容器

1. 创建与配置⽂件中对应的Bean对象
UserService.java

```java
package com.xxxx.service;
public class UserService {
    public void test(){
    System.out.println("UserService Test...");
    }
}
```

AccountService.java

```java
package com.xxxx.service;
public class AccountService {
    public void test(){
    System.out.println("AccountService Test...");
    }
}

```

2. 测试是否可以获取实例化的Bean对象

```java
package com.xxxx;
import com.xxxx.spring.MyFactory;
import com.xxxx.spring.MyClassPathXmlApplicationContext;
import com.xxxx.service.AccountService;
import com.xxxx.service.UserService;
public class App {
    public static void main(String[] args) {
        MyFactory factory = new MyClassPathXmlApplicationContext("spring.xml");
        // 得到实例化对象
        UserService userService = (UserService) factory.getBean("userService");
        userService.test();
        
        UserService userService2 = (UserService) factory.getBean("userService");
        System.out.println(userService+"=====" + userService2);
        
        AccountService accountService =
        (AccountService)factory.getBean("accountService");
        accountService.test();
    }
}
```

Spring 容器在启动的时候读取xml配置信息，并对配置的bean 进⾏实例化（这⾥模拟的⽐较简单，仅⽤于帮助⼤家理解），同时通过上下⽂对象提供的getBean() ⽅法拿到我们配置的bean 对象，从⽽实现外部容器⾃动化维护并创建bean 的效果。

## 4、Spring IOC 配置⽂件加载

### 4.1 IOC和DI

#### 4.1.1 IOC(Inversion of Control)：控制反转

​		在应用程序中的组件需要获取资源时，传统的方式是组件主动的从容器中获取所需要的资源，在这样的模式下开发人员往往需要知道在具体容器中特定资源的获取方式，增加了学习成本，同时降低了开发效率。

​		反转控制的思想完全颠覆了应用程序组件获取资源的传统方式：<font color="red">反转了资源的获取方向——改由容器主动的将资源推送给需要的组件</font>，开发人员不需要知道容器是如何创建资源对象的，只需要提供接收资源的方式即可，极大的降低了学习成本，提高了开发的效率。这种行为也称为查找的<font color="red">被动形式</font>。

#### 4.1.2 DI(Dependency Injection)：依赖注入

​		IOC的另一种表述方式：即组件以一些预先定义好的方式(例如：setter 方法)接受来自于容器的资源注入。相对于IOC而言，这种表述更直接。

​		IOC 描述的是一种思想，而DI 是对IOC思想的具体实现. 

#### 4.1.3 IOC容器在Spring中的实现

​		1）在通过IOC容器读取Bean的实例之前，需要先将IOC容器本身实例化。

​		2）Spring提供了IOC容器的两种实现方式

​			① BeanFactory：IOC容器的基本实现，是Spring内部的基础设施，是面向Spring本身的，不是提供给开发人员使用的。

​			② <font color="red">ApplicationContext</font>：BeanFactory的子接口，提供了更多高级特性。面向Spring的使用者，几乎所有场合都使用ApplicationContext而不是底层的			BeanFactory。

### 4.2 Spring 配置⽂件加载

spring.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           https://www.springframework.org/schema/beans/spring-beans.xsd">
    <bean id="userService" class="com.xxxx.service.UserService"></bean>
</beans>

```



#### 4.2.1. 根据相对路径加载资源

```java
ApplicationContext ac = new ClassPathXmlApplicationContext("spring.xml");
```

#### 4.2.2. 根据绝对路径加载资源（了解）

```java
ApplicationContext ac = new
FileSystemXmlApplicationContext("C:/IdeaWorkspace/spring01/src/main/resources/spring.xml");
```

### 4.3 Spring 多配置⽂件加载

Spring 框架启动时可以加载多个配置⽂件到环境中。对于⽐较复杂的项⽬，可能对应的配置⽂件有多个，项⽬在启动部署时会将多个配置⽂件同时加载进来。

service.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           https://www.springframework.org/schema/beans/spring-beans.xsd">
    <bean id="userService" class="com.xxxx.service.UserService"></bean>
</beans>

```

dao.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           https://www.springframework.org/schema/beans/spring-beans.xsd">
    <bean id="userDao" class="com.xxxx.dao.UserDao"></bean>
</beans>

```

#### 4.3.1. 可变参数，传⼊多个⽂件名

```java
// 同时加载多个资源⽂件
ApplicationContext ac = new ClassPathXmlApplicationContext("spring.xml","dao.xml");
```

#### 4.3.2. 通过总的配置⽂件import其他配置⽂件

spring.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           https://www.springframework.org/schema/beans/spring-beans.xsd">
    <!--导⼊需要包含的资源⽂件-->
    <import resource="service.xml"/>
    <import resource="dao.xml"/>
</beans>
```

加载时只需加载总的配置⽂件即可

```java
// 加载总的资源⽂件
ApplicationContext ac = new ClassPathXmlApplicationContext("spring.xml");
```

## 5、Spring IOC 容器Bean 对象实例化

### 5.1. 构造器实例化

注：<font color="red">通过默认构造器创建空构造⽅法必须存在否则创建失败</font>

1. 设置配置⽂件spring.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           https://www.springframework.org/schema/beans/spring-beans.xsd">
    <bean id="userService" class="com.xxxx.service.UserService"></bean>
</beans>
```

### 5.2. 静态⼯⼚实例化（了解）

注：
		要有该⼯⼚类及⼯⼚⽅法
		⼯⼚⽅法为静态的

1. 定义静态⼯⼚类

```java
package com.xxxx.factory;
import com.xxxx.service.UserService;
/**
* 定义静态⼯⼚类
*/
public class StaticFactory {
    /**
    * 定义对应的静态⽅法，返回实例化对象
    * @return
    */
    public static UserService createUserService() {
        return new UserService();
    }
}
```

2. 设置配置⽂件spring.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           https://www.springframework.org/schema/beans/spring-beans.xsd">
    <!--静态⼯⼚-->
    <bean id="userService" class="com.xxxx.factory.StaticFactory" factorymethod="
                                                                                 createUserService"></bean>
</beans>
```

3. 获取实例化对象

```java
ApplicationContext ac = new ClassPathXmlApplicationContext("spring.xml");
UserService userService = (UserService) ac.getBean("userService");
userService.test();
```

当我们指定Spring使⽤静态⼯⼚⽅法来创建Bean实例时，Spring将先解析配置⽂件，并根据配置⽂件指定的信息，**通过反射调⽤静态⼯⼚类的静态⼯⼚⽅法，并将该静态⼯⼚⽅法的返回值作为Bean实例**，在这个过程中，<font color ="red">Spring不再负责创建Bean实例，Bean实例是由⽤户提供的静态⼯⼚⽅法提供的</font>。

### 5.3. 实例化⼯⼚实例化（了解）

注：
	⼯⼚⽅法为⾮静态⽅法
	需要配置⼯⼚bean，并在业务bean中配置factory-bean，factory-method属性

1. 定义⼯⼚类

   ```java
   package com.xxxx.factory;
   import com.xxxx.service.UserService;
   /**
   * 定义⼯⼚类
   */
   public class InstanceFactory {
   /**
   * 定义⽅法，返回实例化对象
   * @return
   */
       public UserService createUserService() {
           return new UserService();
       }
   }
   
   ```

2. 设置配置⽂件spring.xml

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://www.springframework.org/schema/beans
                              https://www.springframework.org/schema/beans/spring-beans.xsd">
       <!--
   实例化⼯⼚
   1.定义实例化⼯⼚bean
   2.引⽤⼯⼚bean 指定⼯⼚创建⽅法(⽅法为⾮静态)
   -->
       <bean id="instanceFactory" class="com.xxxx.factory.InstanceFactory"></bean>
       <bean id="userService" factory-bean="instanceFactory" factorymethod="
                                                                            createUserService"></bean>
   </beans>
   
   ```

3. 获取实例化对象

```java
ApplicationContext ac = new ClassPathXmlApplicationContext("spring.xml");
UserService userService = (UserService) ac.getBean("userService");
userService.test();
```

### 5.4. Spring三种实例化Bean的⽅式⽐较

- ⽅式⼀：通过bean的缺省构造函数创建，当各个bean的业务逻辑相互⽐较独⽴的时候或者和外界
  关联较少的时候可以使⽤。

- ⽅式⼆：利⽤静态factory⽅法创建，可以统⼀管理各个bean的创建，如各个bean在创建之前需要
  相同的初始化处理，则可⽤这个factory⽅法险进⾏统⼀的处理等等。

- ⽅式三：利⽤实例化factory⽅法创建，即将factory⽅法也作为了业务bean来控制，1可⽤于集成其
  他框架的bean创建管理⽅法，2能够使bean和factory的⻆⾊互换。

  **开发中项⽬⼀般使⽤⼀种⽅式实例化bean，项⽬开发基本采⽤第⼀种⽅式，交给Spring托管，使⽤时直接拿来使⽤即可。另外两种了解**

## 6、Spring IOC 注⼊

### 6.1. Spring IOC ⼿动装配（注⼊）

​		Spring ⽀持的注⼊⽅式共有四种：set 注⼊、构造器注⼊、静态⼯⼚注⼊、实例化⼯⼚注⼊。

#### 6.1.1. set⽅法注⼊

注：
		属性字段需要提供set⽅法
		四种⽅式，推荐使⽤set⽅法注⼊

##### 6.1.1.1. 业务对象JavaBean

1. 属性字段提供set⽅法

   ```java
   public class UserService {
       // 业务对象UserDao set注⼊（提供set⽅法）
       private UserDao userDao;
       public void setUserDao(UserDao userDao) {
           this.userDao = userDao;
       }
   }
   
   ```

2. 配置⽂件的bean标签设置property标签

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://www.springframework.org/schema/beans
                              https://www.springframework.org/schema/beans/spring-beans.xsd">
       <!--
           IOC通过property标签⼿动装配（注⼊）：
               Set⽅法注⼊
                   name：bean对象中属性字段的名称
                   ref：指定bean标签的id属性值
       -->
       <bean id="userDao" class="com.xxxx.dao.UserDao"></bean>
       <bean id="userService" class="com.xxxx.service.UserService">
           <!--业务对象注⼊-->
           <property name="userDao" ref="userDao"/>
       </bean>
   </beans>
   
   ```

   

##### 6.1.1.2. 常⽤对象和基本类型

1. 属性字段提供set ⽅法

   ```java
   public class UserService {
       // 常⽤对象String set注⼊（提供set⽅法）
       private String host;
       public void setHost(String host) {
           this.host = host;
       }
       // 基本类型Integer set注⼊（提供set⽅法）
       private Integer port;
       public void setPort(Integer port) {
           this.port = port;
       }
   }
   
   ```

2. 配置⽂件的bean 标签设置property 标签

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://www.springframework.org/schema/beans
                              https://www.springframework.org/schema/beans/spring-beans.xsd">
       <!--
   IOC通过property标签⼿动装配（注⼊）：
   Set⽅法注⼊
   name：bean对象中属性字段的名称
   value:具体的值（基本类型常⽤对象|⽇期集合）
   -->
       <bean id="userService" class="com.xxxx.service.UserService">
           <!-- 常⽤对象String 注⼊-->
           <property name="host" value="127.0.0.1"/>
           <!-- 基本类型注⼊-->
           <property name="port" value="8080"/>
       </bean>
   </beans>
   ```

   

##### 6.1.1.3. 集合类型和属性对象

1. 属性字段提供set⽅法

   ```java
   package com.beixing.service;
   
   import com.beixing.dao.UserDao;
   
   import java.util.Iterator;
   import java.util.List;
   import java.util.Map;
   import java.util.Set;
   
   /**
    * set方法注入
    *
    * @author wse
    * @version 1.0
    * @date 2020/8/12 0012 11:18
    */
   public class InjectService {
       private UserDao userDao;
       private String host;
       private Integer port;
   
       private List<String> list;
       private Set<String> set;
       private Map<Integer, String> map;
   
       public void setSet(Set<String> set) {
           this.set = set;
       }
   
       public void setList(List<String> list) {
           this.list = list;
       }
   
       public void setMap(Map<Integer, String> map) {
           this.map = map;
       }
   
       public void setHost(String host) {
           this.host = host;
       }
   
       public void setPort(Integer port) {
           this.port = port;
       }
   
       public void setUserDao(UserDao userDao) {
           this.userDao = userDao;
       }
   
       public void test() {
           System.out.println("InjectService");
           //打印字段
           System.out.println(this.host);
           System.out.println(this.port);
           //遍历list
           this.list.forEach(System.out::println);
           //遍历set
           this.set.forEach(System.out::println);
           //遍历map
           Iterator<Map.Entry<Integer, String>> iterator = map.entrySet().iterator();
           for (Map.Entry<Integer, String> entry : map.entrySet()) {
               System.out.println("key= " + entry.getKey() + " and value= " + entry.getValue());
           }
           //调用userDao的方法
           userDao.test();
       }
   }
   ```

2. 配置⽂件的bean标签设置property标签

   ```xml
   <?xml version="1.0" encoding="UTF-8" ?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:util="http://www.springframework.org/schema/util"
          xsi:schemaLocation="http://www.springframework.org/schema/beans
                              https://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/util https://www.springframework.org/schema/util/spring-util.xsd">
       <!--
          IOC通过property标签⼿动装配（注⼊）：
              Set⽅法注⼊
                  name：bean对象中属性字段的名称
                  value:具体的值（基本类型常⽤对象|⽇期集合）
      -->
       <bean id="userDao" class="com.beixing.dao.UserDao"></bean>
       <bean id="injectService" class="com.beixing.service.InjectService">
   <!--        业务对象-->
           <property name="userDao" ref="userDao"></property>
   <!--        基本类型-->
           <property name="host" value="localhost"></property>
           <property name="port" value="8080"></property>
           <!--
       IOC通过property标签⼿动装配（注⼊）：
           Set⽅法注⼊
               name：bean对象中属性字段的名称
               value:具体的值（基本类型常⽤对象|⽇期集合）
   -->
           <!--        List集合注入-->
           <property name="list">
               <list>
                   <value>上海</value>
                   <value>北京</value>
                   <value>深圳</value>
               </list>
           </property>
   <!--        set集合注入-->
           <property name="set">
               <set>
                   <value>上海set</value>
                   <value>北京set</value>
                   <value>深圳set</value>
               </set>
           </property>
   <!--        map集合注入-->
           <property name="map">
               <map>
                   <entry>
                       <key><value>1</value></key>
                       <value>邓紫棋</value>
                   </entry>
                   <entry>
                       <key><value>2</value></key>
                       <value>周杰伦</value>
                   </entry>
                   <entry>
                       <key><value>3</value></key>
                       <value>陈奕迅</value>
                   </entry>
               </map>
           </property>
       </bean>
   </beans>
   ```

##### 6.1.1.4. 测试代码

```java
public class UserInject {
    @Test
    public void test(){
        //获取Spring上下文环境（加载配置文件），
        ClassPathXmlApplicationContext ca = new ClassPathXmlApplicationContext("spring02.xml");
        //根据id获取容器中Bean对象
        InjectService injectService = (InjectService) ca.getBean("injectService");
        //调用方法
        injectService.test();
    }
}
```

#### 6.1.2. 构造器注⼊

注：
	提供带参构造器

6.1.2.1. 单个Bean对象作为参数

Java 代码

```java
package com.beixing.service;
import com.beixing.dao.UserDao;
/**
 * 构造器注入
 *
 * @author wse
 * @version 1.0
 * @date 2020/8/12 0012 10:45
 */
public class UserService02 {
    private UserDao userDao;
    public UserService02(UserDao userDao) {
        this.userDao = userDao;
    }
    public void test(){
        System.out.println("UserService");
    }
}
```

XML配置

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:util="http://www.springframework.org/schema/util"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           https://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/util https://www.springframework.org/schema/util/spring-util.xsd">
    <!--
    IOC通过构造器注⼊：
        通过constructor-arg标签进⾏注⼊
        name：属性名称
        ref：指定bean标签的id属性值
-->
    <bean id="userDao" class="com.beixing.dao.UserDao"></bean>
    <bean id="userService02" class="com.beixing.service.UserService02">
        <constructor-arg name="userDao" ref="userDao"></constructor-arg>
    </bean>

</beans>
```

##### 6.1.2.2. 多个Bean对象作为参数

##### 6.1.2.3. Bean对象和常⽤对象作为参数

##### 6.1.2.4. 循环依赖问题

循环问题产⽣的原因：

​		Bean 通过构造器注⼊，之间彼此相互依赖对⽅导致bean ⽆法实例化。

如何解决：将构造器注⼊改为set⽅法注⼊。

#### 6.1.3. 静态工厂注入

1. 定义静态⼯⼚类

   ```java
   public class StaticFactory {
       // 定义静态⽅法
       public static TypeDao createTypeDao() {
           return new TypeDao();
       }
   }
   ```

2. Java代码

   ```java
   public class TypeService {
       private TypeDao typeDao;
       public void setTypeDao(TypeDao typeDao) {
           this.typeDao = typeDao;
       }
       public void test() {
           System.out.println("TypeService Test...");
       }
   }
   ```

   

3. XML配置

   在配置⽂件中设置bean标签，指定⼯⼚对象并设置对应的⽅法

   ```java
   <bean id="typeService" class="com.xxxx.service.TypeService">
       <property name="typeDao" ref="typeDao"/>
       </bean>
       <!--
           静态⼯⼚注⼊：
           静态⼯⼚注⼊也是借助set⽅法注⼊，只是被注⼊的bean对象的实例化是通过静态⼯⼚实例化的
       -->
       <bean id="typeDao" class="com.xxxx.factory.StaticFactory" factorymethod="createTypeDao"></bean>
   ```

#### 6.1.4. 实例化工厂注⼊

1. 定义⼯⼚类

   ```java
   public class InstanceFactory {
       public TypeDao createTypeDao() {
           return new TypeDao();
       }
   }
   ```

   

2. Java代码

   ```java
   public class TypeService {
       private TypeDao typeDao;
       public void setTypeDao(TypeDao typeDao) {
           this.typeDao = typeDao;
       }
       public void test() {
           System.out.println("TypeService Test...");
       }
   }
   ```

   

3. XMl配置

   声明⼯⼚bean标签，声明bean对象，指明⼯⼚对象和⼯⼚⽅法

   ```java
   <bean id="typeService" class="com.xxxx.service.TypeService">
       <property name="typeDao" ref="typeDao"/>
       </bean>
       <!--
       实例化⼯⼚注⼊：
       实例化⼯⼚注⼊也是借助set⽅法注⼊，只是被注⼊的bean对象的实例化是通过实例化⼯⼚实例化的
       -->
       <bean id="instanceFactory" class="com.xxxx.factory.InstanceFactory"></bean>
       <bean id="typeDao" factory-bean="instanceFactory" factory-method="createTypeDao"></bean>
   
   ```

**重点掌握set注⼊和构造器注⼊，⼯⼚⽅式了解即可。实际开发中基本使⽤set⽅式注⼊bean。**

#### 6.1.5. 注⼊⽅式的选择

​		开发项⽬中set⽅式注⼊⾸选使⽤构造注⼊可以在构建对象的同时⼀并完成依赖关系的建⽴，对象⼀建⽴则所有的⼀切也就准备好
了，但如果要建⽴的对象关系很多，使⽤构造器注⼊会在构建函数上留下⼀⻓串的参数,且不易记忆,这时使⽤Set注⼊会是个不错的选择。
　　使⽤Set注⼊可以有明确的名称，可以了解注⼊的对象会是什么，像setXXX()这样的名称会⽐记忆Constructor上某个参数的位置代表某个对象更好。

**P名称空间的使⽤**

​		spring2.5以后，为了简化setter⽅法属性注⼊，引⽤p名称空间的概念，可以将⼦元素，简化为元素属性配置。

1. 属性字段提供set ⽅法

   ```java
   public class UserService {
       // 业务对象UserDao set注⼊（提供set⽅法）
       private UserDao userDao;
       public void setUserDao(UserDao userDao) {
           this.userDao = userDao;
       }
       // 常⽤对象String set注⼊（提供set⽅法）
       private String host;
       public void setHost(String host) {
           this.host = host;
       }
   }
   ```

2. 在配置⽂件spring.xml 引⼊p 名称空间

   ```xml
   xmlns:p="http://www.springframework.org/schema/p"
   ```

   ```xml
   ?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns:p="http://www.springframework.org/schema/p"
          xsi:schemaLocation="http://www.springframework.org/schema/beans
                              https://www.springframework.org/schema/beans/spring-beans.xsd">
       <bean id="userDao" class="com.xxxx.dao.UserDao"></bean>
       <!--
           p:属性名:="xxx" 引⼊常量值
           p:属性名-ref:="xxx" 引⼊其他Bean对象的id属性值
   -->
       <bean id="userService" class="com.xxxx.service.UserService"
             p:userDao-ref="userDao"
             p:host="127.0.0.1" /></beans>
   ```

### 6.2. Spring IOC ⾃动装配（注⼊）

​		注解⽅式注⼊Bean
​		对于bean 的注⼊，除了使⽤xml 配置以外，可以使⽤注解配置。注解的配置，可以简化配置⽂件，提⾼开发的速度，使程序看上去更简洁。对于注解的解释，Spring对于注解有专⻔的解释器，对定义的注解进⾏解析，实现对应bean对象的注⼊。<font color = "red">通过反射技术实现</font>。

#### 6.2.1. 准备环境

1. 修改配置⽂件

   ```xml
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns:context="http://www.springframework.org/schema/context"
          xsi:schemaLocation="http://www.springframework.org/schema/beans
                              https://www.springframework.org/schema/beans/spring-beans.xsd
                              http://www.springframework.org/schema/context
                              http://www.springframework.org/schema/context/spring-context.xsd">
   ```

2. 开启⾃动化注⼊

   ```xml
   !--开启⾃动化装配（注⼊）-->
   <context:annotation-config/>
   <bean id="userDao" class="com.xxxx.dao.UserDao"></bean>
   <bean id="userService" class="com.xxxx.service.UserService"></bean>
   ```

3. 给注⼊的bean对象添加注解

#### 6.2.2. @Resource注解

@Resource注解实现⾃动注⼊（反射）

- 默认根据属性字段名称查找对应的bean 对象（属性字段的名称与bean标签的id属性值相等）
- 如果属性字段名称未找到，则会通过类型（Class类型）查找
- 属性可以提供set⽅法，也可以不提供set⽅法
- 注解可以声明在属性级别或set⽅法级别
- 可以设置name属性，name属性值必须与bean标签的id属性值⼀致；如果设置了name属性值，就只
  会按照name属性值查找bean对象
- 当注⼊接⼝时，如果接⼝只有⼀个实现则正常实例化；如果接⼝存在多个实现，则需要使⽤name
  属性指定需要被实例化的bean对象

**代码示例**

1. 默认根据属性字段名称查找对应的bean对象（属性字段的名称与bean标签的id属性值相等）

   ```java
   /**
   * @Resource注解实现⾃动注⼊（反射）
   * 默认根据属性字段名称查找对应的bean对象（属性字段的名称与bean标签的id属性值相等）
   */
   public class UserService {
       @Resource
       private UserDao userDao; // 属性字段的名称与bean标签的id属性值相等
       public void setUserDao(UserDao userDao) {
           this.userDao = userDao;
       }
       public void test() {
           // 调⽤UserDao的⽅法
           userDao.test();
       }
   }
   ```

2. 如果属性字段名称未找到，则会通过类型（Class类型）查找

   ```java
   /**
   * @Resource注解实现⾃动注⼊（反射）
   * 如果属性字段名称未找到，则会通过类型（Class类型）查找
   */
   public class UserService {
       @Resource
       private UserDao ud; // 当在配置⽂件中属性字段名（ud）未找到，则会查找对应的class（UserDao类型）
           public void setUd(UserDao ud) {
           this.ud = ud;
       }
       public void test() {
           // 调⽤UserDao的⽅法
           ud.test();
       }
   }
   ```

3. 属性可以提供set⽅法，也可以不提供set⽅法

   ```java
   /**
   * @Resource注解实现⾃动注⼊（反射）
   * 属性可以提供set⽅法，也可以不提供set⽅法
   */
   public class UserService {
       @Resource
       private UserDao userDao; // 不提供set⽅法
       public void test() {
           // 调⽤UserDao的⽅法
           userDao.test();
       }
   }
   ```

4. 注解可以声明在属性级别或set⽅法级别

   ```java
   /**
   * @Resource注解实现⾃动注⼊（反射）
   * 注解可以声明在属性级别或set⽅法级别
   */
   public class UserService {
       private UserDao userDao;
       @Resource // 注解也可设置在set⽅法上
       public void setUserDao(UserDao userDao) {
           this.userDao = userDao;
       }
       public void test() {
           // 调⽤UserDao的⽅法
           userDao.test();
       }
   }
   ```

5. 可以设置name属性，name属性值必须与bean标签的id属性值⼀致；如果设置了name属性值，就只会按照name属性值查找bean对象

   ```java
   /**
   * @Resource注解实现⾃动注⼊（反射）
   * 可以设置name属性，name属性值必须与bean的id属性值⼀致；
   * 如果设置了name属性值，就只会按照name属性值查找bean对象
   */
   public class UserService {
       @Resource(name = "userDao") // name属性值与配置⽂件中bean标签的id属性值⼀致
       private UserDao ud;
       public void test() {
           // 调⽤UserDao的⽅法
           ud.test();
       }
   }
   ```

6. 当注⼊接⼝时，如果接⼝只有⼀个实现则正常实例化；如果接⼝存在多个实现，则需要使⽤name属性指定需要被实例化的bean对象

**定义接⼝类IUserDao.java**

```java
package com.xxxx.dao;
/**
* 定义接⼝类
*/
public interface IUserDao {
    public void test();
}
```

定义接⼝实现类UserDao01.java

```java
package com.xxxx.dao;
/**
* 接⼝实现类
*/
public class UserDao01 implements IUserDao {
    @Override
    public void test(){
        System.out.println("UserDao01...");
    }
}
```

定义接⼝实现类UserDao02.java

```java
package com.xxxx.dao;
/**
* 接⼝实现类
*/
public class UserDao02 implements IUserDao {
    @Override
    public void test(){
        System.out.println("UserDao02...");
    }
}
```

XML配置⽂件

```xml
<!--开启⾃动化装配（注⼊）-->
<context:annotation-config/>
<bean id="userService" class="com.xxxx.service.UserService"></bean>
<bean id="userDao01" class="com.xxxx.dao.UserDao01"></bean>
<bean id="userDao02" class="com.xxxx.dao.UserDao01"></bean>
```

使⽤注解UserService.java

```java
/**
* @Resource注解实现⾃动注⼊（反射）
* 当注⼊接⼝时，如果接⼝只有⼀个实现则正常实例化；如果接⼝存在多个实现，则需要使⽤name属性指
定需要被实例化的bean对象
*/
public class UserService {
    @Resource(name = "userDao01") // name属性值与其中⼀个实现类的bean标签的id属性值⼀致
    private IUserDao iUserDao; // 注⼊接⼝（接⼝存在多个实现）
    public void test() {
        iUserDao.test();
    }
}
```

#### 6.2.3. @Autowired注解

@Autowired注解实现⾃动化注⼊：

- 默认通过类型（Class类型）查找bean对象与属性字段的名称⽆关
- 属性可以提供set⽅法，也可以不提供set⽅法
- 注解可以声明在属性级别或set⽅法级别
- 可以添加@Qualifier结合使⽤，通过value属性值查找bean对象（value属性值必须要设置，且值要与bean标签的id属性值对应）

## 7.1. Spring IOC 扫描器的配置

```
Spring IOC 扫描器
	作⽤：bean对象统⼀进⾏管理，简化开发配置，提⾼开发效率
        1、设置⾃动化扫描的范围
        	如果bean对象未在指定包范围，即使声明了注解，也⽆法实例化
        2、使⽤指定的注解（声明在类级别）bean对象的id属性默认是类的⾸字⺟⼩写
        Dao层：
        	@Repository
        Service层：
        	@Service
        Controller层：
       	 	@Controller
        任意类：
        	@Component
注：开发过程中建议按照指定规则声明注解
```

1. 设置⾃动化扫描范围

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns:context="http://www.springframework.org/schema/context"
          xsi:schemaLocation="http://www.springframework.org/schema/beans
                              https://www.springframework.org/schema/beans/spring-beans.xsd
                              http://www.springframework.org/schema/context
                              http://www.springframework.org/schema/context/spring-context.xsd">
       <!-- 设置⾃动化扫描的范围-->
       <context:component-scan base-package="com.xxxx"/>
   </beans>
   
   ```

## 7.2. Spring 模拟用户登录流程

# 8、Bean的作用域与⽣命周期

## 8.1. Bean的作用域

默认情况下，我们从Spring容器中拿到的对象均是单例的，对于bean的作⽤域类型如下：

### 8.1.1. singleton 作用域

​		注意: lazy-init是懒加载, 如果等于true时作⽤是指Spring容器启动的时候不会去实例化这个bean, ⽽是在程序调⽤时才去实例化. 默认是false即Spring容器启动时实例化.默认情况下，被管理的bean只会IOC容器中存在⼀个实例，对于所有获取该Bean的操作Spring容器将只返回同⼀个Bean。
容器在启动的情况下就实例化所有singleton 的bean对象，并缓存与容器中。

​		lazy-init属性（懒加载）
​				如果为false，则在IOC容器启动时会实例化bean对象，默认false
​				如果为true，则IOC容器启动时不会实例化Bean对象，在使⽤bean对象时才会实例化

​		**lazy-init设置为false有什么好处？
​				1）可以提前发现潜在的配置问题
​				2）Bean 对象存在于缓存中，使⽤时不⽤再去实例化bean，加快程序运⾏效率**

​		**什么对象适合作为单例对象？
​				⼀般来说对于⽆状态或状态不可改变的对象适合使⽤单例模式。（不存在会改变对象状态的成员变量）**

⽐如：controller层、service层、dao层

​		什么是⽆状态或状态不可改变的对象？
​		实际上对象状态的变化往往均是由于属性值得变化⽽引起的，⽐如user类姓名属性会有变化，属性姓名的变化⼀般会引起user对象状态的变化。对于我们的程序来说，⽆状态对象没有实例变量的存在，保证了线程的安全性，service 层业务对象即是⽆状态对象。线程安全的。

### 8.1.2. prototype 作用域

​		通过scope="prototype" 设置bean的类型，每次向Spring容器请求获取Bean都返回⼀个全新的Bean，相对于"singleton"来说就是不缓存Bean，每次都是⼀个根据Bean定义创建的全新Bean。

### 8.1.3. Web应用中的作用域

1. request作⽤域
表示每个请求需要容器创建⼀个全新Bean。⽐如提交表单的数据必须是对每次请求新建⼀个Bean
来保持这些表单数据，请求结束释放这些数据。
2. session作⽤域
表示每个会话需要容器创建⼀个全新Bean。⽐如对于每个⽤户⼀般会有⼀个会话，该⽤户的⽤户
信息需要存储到会话中，此时可以将该Bean作⽤域配置为session级别。
3. globalSession作用域
类似于session作⽤域，其⽤于portlet(Portlet是基于Java的Web组件，由Portlet容器管理，并由容
器处理请求，⽣产动态内容)环境的web应⽤。如果在⾮portlet环境将视为session作⽤域。

​        配置⽅式和基本的作⽤域相同，只是必须要有web环境⽀持，并配置相应的容器监听器或拦截器从⽽能应⽤这些作⽤域，⽬前先熟悉概念，后续集成web时讲解具体使⽤，⼤家只需要知道有这些作⽤域就可以了。

## 8.2. Bean的生命周期

​		对⽐已经学过的servlet ⽣命周期（容器启动装载并实例化servlet类，初始化servlet，调⽤service⽅法，销毁servlet）。
​		同样对于Spring容器管理的bean也存在⽣命周期的概念在Spring中，Bean的⽣命周期包括Bean的定义、初始化、使⽤和销毁4个阶段。

### 8.2.1. Bean的定义

​		在Spring中，通常是通过配置⽂档的⽅式来定义Bean的。
​		在⼀个配置⽂档中，可以定义多个Bean。

### 8.2.2. Bean 的初始化

默认在IOC容器加载时，实例化对象。
Spring bean 初始化有两种⽅式：
⽅式⼀：在配置⽂档中通过指定init-method 属性来完成。

```java
public class RoleService {
    // 定义初始化时需要被调⽤的⽅法
    public void init() {
        System.out.println("RoleService init...");
    }
}
```

```xml
<!-- 通过init-method属性指定⽅法-->
<bean id="roleService" class="com.xxxx.service.RoleService" init-method="init"></bean=>
```

⽅式⼆：使⽤ApplicationContex

```java
public class RoleService implements InitializingBean {
    @Override
    public void afterPropertiesSet() throws Exception {
        System.out.println("RoleService init...");
    }
}
```

```xml
<bean id="roleService" class="com.xxxx.service.RoleService" ></bean>
```

​		Bean对象实例化过程是在Spring容器初始化时被实例化的，但也不是不可改变的，可以通过lazyinit="true" 属性延迟bean对象的初始化操作，此时再调⽤getBean ⽅法时才会进⾏bean的初始化操作

### 8.2.3. Bean 的使用

⽅式⼀：使⽤BeanFactory

⽅式⼆：使⽤ApplicationContext

### 8.2.4. Bean的销毁

​		实现销毁⽅式(Spring容器会维护bean对象的管理，可以指定bean对象的销毁所要执⾏的⽅法)。
​		步骤⼀：实现销毁⽅式(Spring容器会维护bean对象的管理，可以指定bean对象的销毁所要执⾏的⽅法)

```xml
<bean id="roleService" class="com.xxxx.service.RoleService" destroy-method="destroy">
</bean>
```

​		步骤⼆：通过AbstractApplicationContext 对象，调⽤其close⽅法实现bean的销毁过程

```java
AbstractApplicationContext ctx=new ClassPathXmlApplicationContext("spring.xml");
ctx.close();
```

​		<font color = "red">IOC/DI-控制反转和依赖注⼊</font>
​					<font color = "red">将对象实例化的创建过程转交给外部容器（IOC容器充当⼯⼚⻆⾊）去负责；属性赋值的操作</font>