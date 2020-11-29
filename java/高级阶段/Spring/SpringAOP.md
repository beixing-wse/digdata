# Spring AOP

# 1、主要内容

# 2、代理模式

代理模式在Java 开发中是⼀种⽐较常⻅的设计模式。设计⽬的旨在为服务类与客户类之间插⼊其他功
能，插⼊的功能对于调⽤者是透明的，起到伪装控制的作⽤。如租房的例⼦：房客、中介、房东。对应
于代理模式中即：客户类、代理类、委托类（被代理类）。
为某⼀个对象（委托类）提供⼀个代理（代理类），⽤来控制对这个对象的访问。委托类和代理类有
⼀个共同的⽗类或⽗接⼝。代理类会对请求做预处理、过滤，将请求分配给指定对象。
⽣活中常⻅的代理情况：
租房中介、婚庆公司等
代理模式的两个设计原则：

1. 代理类与委托类具有相似的⾏为（共同）
2. 代理类增强委托类的⾏为
常⽤的代理模式：
1. 静态代理
2. 动态代理
3. 静态代理
某个对象提供⼀个代理，代理⻆⾊固定，以控制对这个对象的访问。代理类和委托类有共同的⽗类或
⽗接⼝，这样在任何使⽤委托类对象的地⽅都可以⽤代理对象替代。代理类负责请求的预处理、过滤、
将请求分派给委托类处理、以及委托类执⾏完请求后的后续处理。
3.1. 代理的三要素
a、有共同的⾏为（结婚）- 接⼝
b、⽬标⻆⾊（新⼈）- 实现⾏为
c、代理⻆⾊（婚庆公司）- 实现⾏为增强⽬标对象⾏为
3.2. 静态代理的特点
1、⽬标⻆⾊固定
2、在应⽤程序执⾏前就得到⽬标⻆⾊
3、代理对象会增强⽬标对象的⾏为
4、有可能存在多个代理引起"类爆炸"（缺点）
3.3. 静态代理的实现
3.3.1. 定义⾏为（共同）定义接⼝
3.3.2. ⽬标对象（实现⾏为）
3.3.3. 代理对象（实现⾏为、增强⽬标对象的⾏为）
/**
* 定义⾏为
*/
public interface Marry {
public void toMarry();
}
/**
* 静态代理——> ⽬标对象
*/
public class You implements Marry {
// 实现⾏为
@Override
public void toMarry() {
System.out.println("我要结婚了...");
}
}
/**
* 静态代理——> 代理对象
*/
public class MarryCompanyProxy implements Marry {
// ⽬标对象
private Marry marry;
// 通过构造器将⽬标对象传⼊
public MarryCompanyProxy(Marry marry) {
this.marry = marry;
}
// 实现⾏为
@Override
public void toMarry() {
// 增强⾏为
before();
// 执⾏⽬标对象中的⽅法
marry.toMarry();
3.3.4. 通过代理对象实现⽬标对象的功能
静态代理对于代理的⻆⾊是固定的，如dao层有20个dao类，如果要对⽅法的访问权限进⾏代理，此时
需要创建20个静态代理⻆⾊，引起类爆炸，⽆法满⾜⽣产上的需要，于是就催⽣了动态代理的思想。
4. 动态代理
相⽐于静态代理，动态代理在创建代理对象上更加的灵活，动态代理类的字节码在程序运⾏时，由
Java反射机制动态产⽣。它会根据需要，通过反射机制在程序运⾏期，动态的为⽬标对象创建代理对
象，⽆需程序员⼿动编写它的源代码。动态代理不仅简化了编程⼯作，⽽且提⾼了软件系统的可扩展
性，因为反射机制可以⽣成任意类型的动态代理类。代理的⾏为可以代理多个⽅法，即满⾜⽣产需要的
同时⼜达到代码通⽤的⽬的。
动态代理的两种实现⽅式：
1. JDK 动态代理
2. CGLIB动态代理
// 增强⾏为
after();
}
/**
* 增强⾏为
*/
private void after() {
System.out.println("新婚快乐，早⽣贵⼦！");
}
/**
* 增强⾏为
*/
private void before() {
System.out.println("场地正在布置中...");
}
}
// ⽬标对象
You you = new You();
// 构造代理⻆⾊同时传⼊真实⻆⾊
MarryCompanyProxy marryCompanyProxy = new MarryCompanyProxy(you);
// 通过代理对象调⽤⽬标对象中的⽅法
marryCompanyProxy.toMarry();
4.1. 动态代理的特点
1. ⽬标对象不固定
2. 在应⽤程序执⾏时动态创建⽬标对象
3. 代理对象会增强⽬标对象的⾏为
4.2. JDK动态代理
注：JDK动态代理的⽬标对象必须有接⼝实现
4.2.1. newProxyInstance
Proxy类：
Proxy类是专⻔完成代理的操作类，可以通过此类为⼀个或多个接⼝动态地⽣成实现类，此类提供了如
下操作⽅法：
4.2.2. 获取代理对象
/*
返回⼀个指定接⼝的代理类的实例⽅法调⽤分派到指定的调⽤处理程序。(返回代理对象)
loader：⼀个ClassLoader对象，定义了由哪个ClassLoader对象来对⽣成的代理对象进⾏加载
interfaces：⼀个Interface对象的数组，表示的是我将要给我需要代理的对象提供⼀组什么接⼝，如果
我提供了⼀组接⼝给它，那么这个代理对象就宣称实现了该接⼝(多态)，这样我就能调⽤这组接⼝中的⽅法了
h：⼀个InvocationHandler接⼝，表示代理实例的调⽤处理程序实现的接⼝。每个代理实例都具有⼀个关联
的调⽤处理程序。对代理实例调⽤⽅法时，将对⽅法调⽤进⾏编码并将其指派到它的调⽤处理程序的invoke ⽅法
（传⼊InvocationHandler接⼝的⼦类）
*/
public static Object newProxyInstance(ClassLoader loader,
Class<?>[] interfaces,
InvocationHandler h)
public class JdkHandler implements InvocationHandler {
// ⽬标对象
private Object target; // ⽬标对象的类型不固定，创建时动态⽣成
// 通过构造器将⽬标对象赋值
public JdkHandler(Object target) {
this.target = target;
}
/**
* 1、调⽤⽬标对象的⽅法（返回Object）
* 2、增强⽬标对象的⾏为
* @param proxy 调⽤该⽅法的代理实例
* @param method ⽬标对象的⽅法
* @param args ⽬标对象的⽅法形参
* @return
* @throws Throwable
4.2.3. 通过代理对象实现⽬标对象的功能
*/
@Override
public Object invoke(Object proxy, Method method, Object[] args) throws Throwable
{
// 增强⾏为
System.out.println("==============⽅法前执⾏");
// 调⽤⽬标对象的⽅法（返回Object）
Object result = method.invoke(target,args);
// 增强⾏为
System.out.println("⽅法后执⾏==============");
return result;
}
/**
* 得到代理对象
* public static Object newProxyInstance(ClassLoader loader,
* Class<?>[] interfaces,
* InvocationHandler h)
* loader：类加载器
* interfaces：接⼝数组
* h：InvocationHandler接⼝(传⼊InvocationHandler接⼝的实现类)
*
*
* @return
*/
public Object getProxy() {
return
Proxy.newProxyInstance(this.getClass().getClassLoader(),target.getClass().getInterface
s(),this);
}
}
// ⽬标对象
You you = new You();
// 获取代理对象
JdkHandler jdkHandler = new JdkHandler(you);
Marry marry = (Marry) jdkHandler.getProxy();
// 通过代理对象调⽤⽬标对象中的⽅法
marry.toMarry();
注：JDK的动态代理依靠接⼝实现，如果有些类并没有接⼝实现，则不能使⽤JDK代理。
4.3. CGLIB 动态代理
JDK的动态代理机制只能代理实现了接⼝的类，⽽不能实现接⼝的类就不能使⽤JDK的动态代理，cglib
是针对类来实现代理的，它的原理是对指定的⽬标类⽣成⼀个⼦类，并覆盖其中⽅法实现增强，但因为
采⽤的是继承，所以不能对final修饰的类进⾏代理。
4.3.1. 添加依赖
在pom.xml⽂件中引⼊cglib的相关依赖
4.3.2. 定义类
实现MethodInterceptor接⼝
问：Java动态代理类中的invoke是怎么调⽤的？
答：在⽣成的动态代理类$Proxy0.class中，构造⽅法调⽤了⽗类Proxy.class的构造⽅法，给成员变量
invocationHandler赋值，$Proxy0.class的static模块中创建了被代理类的⽅法，调⽤相应⽅法时⽅法体中调
⽤了⽗类中的成员变量InvocationHandler的invoke()⽅法。
<!-- https://mvnrepository.com/artifact/cglib/cglib -->
<dependency>
<groupId>cglib</groupId>
<artifactId>cglib</artifactId>
<version>2.2.2</version>
</dependency>
public class CglibInterceptor implements MethodInterceptor {
// ⽬标对象
private Object target;
// 通过构造器传⼊⽬标对象
public CglibInterceptor(Object target) {
this.target = target;
}
/**
* 获取代理对象
* @return
*/
public Object getProxy() {
// 通过Enhancer对象的create()⽅法可以⽣成⼀个类，⽤于⽣成代理对象
Enhancer enhancer = new Enhancer();
// 设置⽗类(将⽬标类作为其⽗类)
enhancer.setSuperclass(target.getClass());
// 设置拦截器回调对象为本身对象
4.3.3. 调⽤⽅法
4.4. JDK代理与CGLIB代理的区别
JDK动态代理实现接⼝，Cglib动态代理继承思想
enhancer.setCallback(this);
// ⽣成⼀个代理类对象，并返回
return enhancer.create();
}
/**
* 拦截器
* 1、⽬标对象的⽅法调⽤
* 2、增强⾏为
* @param object 由CGLib动态⽣成的代理类实例
* @param method 实体类所调⽤的被代理的⽅法引⽤
* @param objects 参数值列表
* @param methodProxy ⽣成的代理类对⽅法的代理引⽤
* @return
* @throws Throwable
*/
@Override
public Object intercept(Object object, Method method, Object[] objects,
MethodProxy methodProxy) throws Throwable {
// 增强⾏为
System.out.println("==============⽅法前执⾏");
// 调⽤⽬标对象的⽅法（返回Object）
Object result = methodProxy.invoke(target,objects);
// 增强⾏为
System.out.println("⽅法后执⾏==============");
return result;
}
}
// ⽬标对象
You you = new You();
CglibInterceptor cglibInterceptor = new CglibInterceptor(you);
Marry marry = (Marry) cglibInterceptor.getProxy();
marry.toMarry();
User user = new User();
CglibInterceptor cglibInterceptor = new CglibInterceptor(user);
User u = (User) cglibInterceptor.getProxy();
u.test();
JDK动态代理（⽬标对象存在接⼝时）执⾏效率⾼于Ciglib
如果⽬标对象有接⼝实现，选择JDK代理，如果没有接⼝实现选择Cglib代理
5. Spring AOP
5.1. ⽇志处理带来的问题
我们有⼀个Pay(接⼝) 然后两个实现类DollarPay和RmbPay，都需要重写pay()⽅法, 这时我们需要对pay
⽅法进⾏性能监控，⽇志的添加等等怎么做？
5.1.1. 最容易想到的⽅法
对每个字符⽅法均做⽇志代码的编写处理，如下⾯⽅式
缺点: 代码重复太多, 添加的⽇志代码耦合度太⾼（如果需要更改⽇志记录代码功能需求，类中⽅法需
要全部改动，⼯程量浩⼤）
5.1.2. 使⽤装饰器模式/代理模式改进解决⽅案
装饰器模式：动态地给⼀个对象添加⼀些额外的职责。
代理模式：以上刚讲过。于是得出以下结构：
仔细考虑过后发现虽然对原有内部代码没有进⾏改动，对于每个类做⽇志处理，并引⽤⽬标类，但是
如果待添加⽇志的业务类的数量很多，此时⼿动为每个业务类实现⼀个装饰器或创建对应的代理类，同
时代码的耦合度也加⼤，需求⼀旦改变，改动的⼯程量也是可想⽽知的。
有没有更好的解决⽅案，只要写⼀次代码，对想要添加⽇志记录的地⽅能够实现代码的复⽤，达到松耦
合的同时，⼜能够完美完成功能？
答案是肯定的，存在这样的技术，aop已经对其提供了完美的实现！
5.2. 什么是AOP？
Aspect Oriented Programing ⾯向切⾯编程，相⽐较oop ⾯向对象编程来说，Aop关注的不再是程序代
码中某个类，某些⽅法，⽽aop考虑的更多的是⼀种⾯到⾯的切⼊，即层与层之间的⼀种切⼊，所以称
之为切⾯。联想⼤家吃的汉堡（中间夹⾁）。那么aop是怎么做到拦截整个⾯的功能呢？考虑前⾯学到
的servlet filter /* 的配置，实际上也是aop 的实现。
5.3. AOP能做什么？
AOP主要应⽤于⽇志记录，性能统计，安全控制，事务处理等⽅⾯，实现公共功能性的重复使⽤。
5.4. AOP的特点
1. 降低模块与模块之间的耦合度，提⾼业务代码的聚合度。（⾼内聚低耦合）
2. 提⾼了代码的复⽤性。
3. 提⾼系统的扩展性。（⾼版本兼容低版本）
4. 可以在不影响原有的功能基础上添加新的功能
5.4.1. AOP的底层实现
动态代理（JDK + CGLIB）
5.5. AOP基本概念
5.5.1. Joinpoint（连接点）
被拦截到的每个点，spring中指被拦截到的每⼀个⽅法，spring aop⼀个连接点即代表⼀个⽅法的执
⾏。
5.5.2. Pointcut（切⼊点）
对连接点进⾏拦截的定义（匹配规则定义规定拦截哪些⽅法，对哪些⽅法进⾏处理），spring 有专⻔
的表达式语⾔定义。
5.5.3. Advice（通知）
拦截到每⼀个连接点即（每⼀个⽅法）后所要做的操作
1. 前置通知（前置增强）— before() 执⾏⽅法前通知
2. 返回通知（返回增强）— afterReturn ⽅法正常结束返回后的通知
3. 异常抛出通知（异常抛出增强）— afetrThrow()
4. 最终通知— after ⽆论⽅法是否发⽣异常，均会执⾏该通知。
5. 环绕通知— around 包围⼀个连接点（join point）的通知，如⽅法调
⽤。这是最强⼤的⼀种通知类型。环绕通知可以在⽅法调⽤前后完成⾃
定义的⾏为。它也会选择是否继续执⾏连接点或直接返回它们⾃⼰的返
回值或抛出异常来结束执⾏。
5.5.4. Aspect（切⾯）
切⼊点与通知的结合，决定了切⾯的定义，切⼊点定义了要拦截哪些类的哪些⽅法，通知则定义了拦
截过⽅法后要做什么，切⾯则是横切关注点的抽象，与类相似，类是对物体特征的抽象，切⾯则是横切
关注点抽象。
5.5.5. Target（⽬标对象）
被代理的⽬标对象
5.5.6. Weave（织⼊）
将切⾯应⽤到⽬标对象并⽣成代理对象的这个过程即为织⼊
5.5.7. Introduction（引⼊）
在不修改原有应⽤程序代码的情况下，在程序运⾏期为类动态添加⽅法或者字段的过程称为引⼊
6. Spring AOP的实现
6.1. Spring AOP环境搭建
6.1.1. 坐标依赖引⼊
6.1.2. 添加spring.xml的配置
添加命名空间
6.2. 注解实现
6.2.1. 定义切⾯
<!--Spring AOP-->
<dependency>
<groupId>org.aspectj</groupId>
<artifactId>aspectjweaver</artifactId>
<version>1.8.9</version>
</dependency>
xmlns:aop="http://www.springframework.org/schema/aop"
http://www.springframework.org/schema/aop
http://www.springframework.org/schema/aop/spring-aop.xsd
/**
* 切⾯
* 切⼊点和通知的抽象（与⾯向对象中的类相似）
* 定义切⼊点和通知（切⼊点定义了要拦截哪些类的哪些⽅法，通知则定义了拦截过⽅法后要做什么）
*/
@Component // 将对象交给IOC容器去实例化
@Aspect // 声明当前类是⼀个切⾯
public class LogCut {
/**
* 切⼊点：
* 匹配规则。规定什么⽅法被拦截、需要处理什么⽅法
* 定义切⼊点
* @Pointcut("匹配规则")
*
* Aop 切⼊点表达式简介
* 1. 执⾏任意公共⽅法：
* execution(public *(..))
* 2. 执⾏任意的set⽅法
* execution(* set*(..))
* 3. 执⾏com.xxxx.service包下任意类的任意⽅法
* execution(* com.xxxx.service.*.*(..))
* 4. 执⾏com.xxxx.service 包以及⼦包下任意类的任意⽅法
* execution(* com.xxxx.service..*.*(..))
*
* 注：表达式中的第⼀个* 代表的是⽅法的修饰范围
* 可选值：private、protected、public （* 表示所有范围）
*/
@Pointcut("execution (* com.xxxx.service..*.*(..) )")
public void cut(){}
/**
* 声明前置通知并将通知应⽤到定义的切⼊点上
* ⽬标类⽅法执⾏前执⾏该通知
*
*/
@Before(value = "cut()")
public void before() {
System.out.println("前置通知.....");
}
/**
* 声明返回通知并将通知应⽤到定义的切⼊点上
* ⽬标类⽅法（⽆异常）执⾏后执⾏该通知
*
*/
@AfterReturning(value = "cut()")
public void afterReturn() {
System.out.println("返回通知.....");
}
/**
* 声明最终通知并将通知应⽤到定义的切⼊点上
* ⽬标类⽅法（⽆异常或有异常）执⾏后执⾏该通知
*
*/
@After(value = "cut()")
public void after() {
System.out.println("最终通知.....");
}
/**
* 声明异常通知并将通知应⽤到定义的切⼊点上
* ⽬标类⽅法出现异常时执⾏该通知
*/
@AfterThrowing(value="cut()",throwing = "e")
public void afterThrow(Exception e) {
System.out.println("异常通知....." + " 异常原因：" + e.getCause());
}
6.2.2. 配置⽂件（spring.xml）
6.3. XML实现
6.3.1. 定义切⾯
/**
* 声明环绕通知并将通知应⽤到切⼊点上
* ⽅法执⾏前后通过环绕通知定义相应处理
* 需要通过显式调⽤对应的⽅法，否则⽆法访问指定⽅法(pjp.proceed();)
* @param pjp
* @return
*/
@Around(value = "cut()")
public Object around(ProceedingJoinPoint pjp) {
System.out.println("前置通知...");
Object object = null;
try {
object = pjp.proceed();
System.out.println(pjp.getTarget() + "======" + pjp.getSignature());
// System.out.println("返回通知...");
} catch (Throwable throwable) {
throwable.printStackTrace();
System.out.println("异常通知...");
}
System.out.println("最终通知...");
return object;
}
}
<!--配置AOP代理-->
<aop:aspectj-autoproxy/>
**
* 切⾯
* 切⼊点和通知的抽象（与⾯向对象中的类相似）
* 定义切⼊点和通知（切⼊点定义了要拦截哪些类的哪些⽅法，通知则定义了拦截过⽅法后要做什么）
*/
@Component // 将对象交给IOC容器去实例化
public class LogCut02 {
public void cut(){}
/**
* 声明前置通知并将通知应⽤到定义的切⼊点上
* ⽬标类⽅法执⾏前执⾏该通知
*
*/
public void before() {
System.out.println("前置通知.....");
}
/**
* 声明返回通知并将通知应⽤到定义的切⼊点上
* ⽬标类⽅法（⽆异常）执⾏后执⾏该通知
*
*/
public void afterReturn() {
System.out.println("返回通知.....");
}
/**
* 声明最终通知并将通知应⽤到定义的切⼊点上
* ⽬标类⽅法（⽆异常或有异常）执⾏后执⾏该通知
*
*/
public void after() {
System.out.println("最终通知.....");
}
/**
* 声明异常通知并将通知应⽤到定义的切⼊点上
* ⽬标类⽅法出现异常时执⾏该通知
*/
public void afterThrow(Exception e) {
System.out.println("异常通知....." + " 异常原因：" + e.getCause());
}
/**
* 声明环绕通知并将通知应⽤到切⼊点上
* ⽅法执⾏前后通过环绕通知定义相应处理
* 需要通过显式调⽤对应的⽅法，否则⽆法访问指定⽅法(pjp.proceed();)
* @param pjp
* @return
*/
public Object around(ProceedingJoinPoint pjp) {
System.out.println("前置通知...");
Object object = null;
6.3.2. 配置⽂件（spring.xml）
7. Spring AOP总结
7.1. 代理模式实现三要素
1. 接⼝定义
2. ⽬标对象与代理对象必须实现统⼀接⼝
3. 代理对象持有⽬标对象的引⽤增强⽬标对象⾏为
7.2. 代理模式实现分类以及对应区别
1. 静态代理：⼿动为⽬标对象制作代理对象，即在程序编译阶段完成代理对象的创建
try {
object = pjp.proceed();
System.out.println(pjp.getTarget() + "======" + pjp.getSignature());
// System.out.println("返回通知...");
} catch (Throwable throwable) {
throwable.printStackTrace();
System.out.println("异常通知...");
}
System.out.println("最终通知...");
return object;
}
}
<!--aop相关配置-->
<aop:config>
<!--aop切⾯-->
<aop:aspect ref="logCut02">
<!-- 定义aop 切⼊点-->
<aop:pointcut id="cut" expression="execution(* com.xxxx.service..*.*(..))"/>
<!-- 配置前置通知指定前置通知⽅法名并引⽤切⼊点定义-->
<aop:before method="before" pointcut-ref="cut"/>
<!-- 配置返回通知指定返回通知⽅法名并引⽤切⼊点定义-->
<aop:after-returning method="afterReturn" pointcut-ref="cut"/>
<!-- 配置异常通知指定异常通知⽅法名并引⽤切⼊点定义-->
<aop:after-throwing method="afterThrow" throwing="e" pointcut-ref="cut"/>
<!-- 配置最终通知指定最终通知⽅法名并引⽤切⼊点定义-->
<aop:after method="after" pointcut-ref="cut"/>
<!-- 配置环绕通知指定环绕通知⽅法名并引⽤切⼊点定义-->
<aop:around method="around" pointcut-ref="cut"/>
</aop:aspect>
</aop:config>
2. 动态代理：在程序运⾏期动态创建⽬标对象对应代理对象。
3. jdk动态代理：被代理⽬标对象必须实现某⼀或某⼀组接⼝实现⽅式通过回调创建代理对象。
4. cglib 动态代理：被代理⽬标对象可以不必实现接⼝，继承的⽅式实现。
动态代理相⽐较静态代理，提⾼开发效率，可以批量化创建代理，提⾼代码复⽤率。
7.3. Aop 理解
1. ⾯向切⾯，相⽐oop 关注的是代码中的层或⾯
2. 解耦，提⾼系统扩展性
3. 提⾼代码复⽤
7.4. Aop 关键词
1. 连接点：每⼀个⽅法
2. 切⼊点：匹配的⽅法集合
3. 切⾯：连接点与切⼊点的集合决定了切⾯，横切关注点的抽象
4. 通知：⼏种通知
5. ⽬标对象：被代理对象
6. 织⼊：程序运⾏期将切⾯应⽤到⽬标对象并⽣成代理对象的过程
7. 引⼊：在不修改原始代码情况下，在程序运⾏期为程序动态引⼊⽅法或字段的过程