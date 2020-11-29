# 作业

## 简答题

1. Spring 是什么？

   Spring是一个轻型的容器，是J2EE规范的轻量级实现，是企业应用的“一站式”解决方案。其中的核心就是bean工厂，用以构造我们需要的Model，spring是非侵入式的，Spring的应用中的对象不依赖于Spring的特定类。Spring是一款开源的，基于分层的JavaEE应用一站式轻量化的框架，主要核心是IOC（控制反转和依赖注入）和AOP（面向切面）技术。实现项⽬在开发过程中的轻松解耦，提⾼项⽬的开发效率。

2. 谈谈你对IOC的理解

   IOC即Inversion of Control，IOC：控制反转，把创建对象过程交给Spring 进行管理。

3. 简述Spring IOC的启动过程

   - 先获取spring的上下文环境（加载配置文件）
   - 通过getBean方法得到spring已经实例化好的Bean对象

4. 说出bean工厂创建bean的三种方式？

   - 构造器实例化
   - 静态工厂实例化
   - 实例化工厂实例化

5. 在Spring中，bean的注入有几种方式，各是什么？

   4种

   - set方法注入
   - 构造器注入
   - 静态工厂注入
   - 实例化工厂注入

6. 请叙述构造注入的优点？

   （1）可以在构造器中决定依赖关系的注入顺序，优先依赖的优先注入。

   （2）对于依赖关系无须变化的bean，构造注入更加有用处。因为没有setter方法，所有的依赖关系全部在构造器内设定，因此，无须担心后续的代码对依赖关系产生破坏。

   （3）依赖关系只能在构造器中设定，则只有组建的创建者才能改变组建的依赖关系。对组建的调用者而言，组建内部的依赖关系完全透明，更符合高内聚的原则。

7. 列举Spring中使用到的注解，并解释其作用

   @Resource，实现自动注入（反射）

   @Autowired，实现自动注入（反射）

   @Repository,Dao层自动扫描

   @Service，Service层自动扫描

   @Controller，Controller层自动扫描

   @Component，任意层自动扫描。

8. @Resource与@Autowried的使用及区别

   ##### 相同点：

    @resource和@autowried都是用来装配bean，都可以写在字段上或者setter方法上。

   ##### 区别：

   ###### @autowried：

    1.是默认按照类型进行装配（属于spring），默认情况是要求依赖的对象必须存在，如果允许null值，则需要将required属性设置为false。如：@autowried（required=false）

    2.如果需要按照名称装配需要用到另一个注解@qualifier(“value”）和@autowried组合使用。value属性值必须要设置，且值要与bean标签的id属性值对应。

   ###### @resource

    装配时会先根据名称进行装配，当找不到名称与之匹配的bean时才按照类型进行装配，**如果写了name的属性则只会根据name的名称去装配**：

   1. 如果同时指定了name和type，则从Spring上下文中找到唯一匹配的bean进行装配，找不到则抛出异常

   　　2. 如果指定了name，则从上下文中查找名称（id）匹配的bean进行装配，找不到则抛出异常
   　　3. 如果指定了type，则从上下文中找到类型匹配的唯一bean进行装配，找不到或者找到多个，都会抛出 异常
   　　4. 如果既没有指定name，又没有指定type，则自动按照byName方式进行装配；如果没有匹配，则回退为一个原始类型进行匹配，如果匹配则自动装配。

   <font color = "red">**推荐使⽤@Resource 注解是属于J2EE的，减少了与Spring的耦合。**</font>

9. Spring中Bean 的生命周期是怎么样的？

   在Spring中，Bean的⽣命周期包括Bean的定义、初始化、使⽤和销毁4个阶段.

   - Bean的定义：在Spring中，通常是通过配置⽂档的⽅式来定义Bean的。

   - Bean的初始化：默认在IOC容器加载时，实例化对象。

     - ⽅式⼀：在配置⽂档中通过指定init-method 属性来完成。
     - ⽅式⼆：实现org.springframework.beans.factory.InitializingBean 接⼝。

     ​        Bean对象实例化过程是在Spring容器初始化时被实例化的，但也不是不可改变的，可以通过lazy-init="true" 属性延迟bean对象的初始化操作，此时再调⽤getBean ⽅法时才会进⾏bean的初始化操作。

   - Bean的使⽤：使⽤BeanFactory和使用ApplicationContext。

   - Bean的销毁：实现销毁⽅式(Spring容器会维护bean对象的管理，可以指定bean对象的销毁所要执⾏的⽅法)。

     - 实现销毁⽅式(Spring容器会维护bean对象的管理，可以指定bean对象的销毁所要执⾏的⽅法)

       - ```xml
         <bean id="roleService" class="com.xxxx.service.RoleService" destroy-method="destroy">
         </bean>
         ```

     - 通过AbstractApplicationContext 对象，调⽤其close⽅法实现bean的销毁过程

       - ```java
         AbstractApplicationContext ctx=new ClassPathXmlApplicationContext("spring.xml");
         ctx.close();
         ```

         





## 选择题

1. 下面关于Spring的说话正确的是 （C）

   A）Spring是一个重量级的框架 

   B）Spring是一个轻量级的框架

   C）Spring是一个IOC和AOP容器 

   D）Spring是一个入侵式的框架



2. 下面关于IOC的理解，正确的是（A）

   A）控制反转 
   B）对象被动的接受依赖类 

   C）对象主动的去找依赖类 

   D）一定要用接口

   

3. Spring各模块之间关系（A）

   A）Spring 各模块之间是紧密联系的，相关依赖的

   B）Spring 各模块之间可以单独存在

   C）Spring 的核心模块是必须的，其他模板是基于核心模板

   D）Spring 的核心模板不是必须的，可以不要

   

4. 下面是Spring依赖注入方式的是 （A,B）

   A) set方法注入

   B) 构造方法注入

   C) get方法注入

   D) 接口的注入

   

5. 下面关于在Spring中配置Bean的id属性的说法正确的是 （）

   A) id属性是必须，没有id水泥杆就会报错

   B) id属性不是必须的，可以没有

   C) id属性的值不可重复

   D) id属性的值不可以重复

   

6. 下面关于在Spring中配置Bean的id属性的说法正确的是 （B）

   A) 那么属性是必须，没有name属性就会报错

   B) name属性不是必须的，可以没有

   C) name属性的值可以重复

   D) name属性的值不可以重复



7. 下面关于在Spring中配置Bean的id属性的说法正确的是 （C）

   A) init-method 是在最前面执行的

   B) init-method 在构造方法后，依赖注入前执行

   C) init-method在依赖注入之后执行

   D) init-method在依赖注入之后，构造函数之前执行



8. 下面关于Spring配置文件说话正确的是 （C）

   A) Spring配置文件必须叫applicationContext.xml

   B) Spring配置文件可以不叫applicationContext.xml

   C) Spring配置文件可以有多个

   D) Spring配置文件只能有一个

9. 看下面的代码，说法正确的是 （A）

   ```xml
   <bean id="userTable" class="com.xfaccp.bean.UserTable"> 
     	<property name="userName" value="admin"/>
   </bean>
   ```

   A) 其中<property name="userName">的userName是UserTable中属性，可以不要get、set方法

   B) 其中<property name="userName">的userName是UserTable中属性，可以不要get方法，但是一定要有set方法

   C) 其中<property name="userName">的userName是UserTable中属性，可以不要set方法，但是一定有get方法

   D) 其中<property name="userName">的userName是UserTable中属性，一定要有get、set方法



10. Spring 以 Bean的方式管理所有的组件，此处的Bean指的是 （A）

    A) 必须符合JavaBean

    B) 任何Java对象以及Java组件都视为bean

    C) 必须要有getter方法和setter方法

    D) EJB组件











