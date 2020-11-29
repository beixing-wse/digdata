# JVM架构和GC垃圾回收机制详解

# JVM架构图分析

![img](https://img-blog.csdn.net/20170610165140237?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvYWlqaXVkdQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

JVM被分为三个主要的子系统

**（1）类加载器子系统（2)运行时数据区（3）执行引擎**

## 1. 类加载器子系统

​		Java的动态类加载功能是由类加载器子系统处理。当它在运行时（不是编译时）首次引用一个类时，它加载、链接并初始化该类文件。

**类加载的时机 :** 

   	类从加载到虚拟机到被卸载出内存为止, 整个生命周期包括: 加载, 验证, 准备, 解析, 初始化, 使用, 卸载, 其中 加载,验证,准备,初始化和卸载这5个阶段的顺序是确定的, 类在加载过程必须按照这种**顺序开始**, 而解析阶段不一定: 它在某些情况下可以在初始化后再开始, 之所以强调按顺序开始, 而不是按顺序进行或完成, 是因为这些阶段通常是互相交叉的混合式进行的, 通常会在一个阶段执行的过程中调用另外一个阶段, 而解析阶段则例外, 可能在初始化之后再开始(支持动态绑定)

**类加载的过程 :** 

  1). 加载 : JVM规范没有明确规定时机, 各JVM实现自己决定加载时机

​       类加载是整个类装载的第一个阶段, 此阶段需完成三件事情

​       ①: 通过一个类的全限定名来获取此类的二进制字节流

​       ②: 将这个字节流所代表的静态存储结构转化为方法区的运行时数据结构

​       ③: 在内存中生成一个代表这个类的java.lang.Class对象, 作为方法区这个类的各种数据访问入口

​        \* 数组类本身并不通过类加载器创建,而是通过Java虚拟机直接创建 

  2). 验证 : 

​        ①: 文件格式验证

​        ②: 元数据验证(语义分析)

​        ③: 字节码验证

​        ④: 符号引用验证

  3). 准备 : 为类变量分配内存并设置类变量初始值(零值)的阶段

  4). 解析 : 将符号引用转会为直接引用

  5). 初始化 : 有且只有几种情况下当虚拟机没有对类进行初始化时必须进行初始化动作, 

​        ①: 遇到new, getstatic, putstatic, invokestatic这四个字节码指令时, 落到代码的场景通常是: new关键字对对象进行实例化时, 读取或者设置一个类的静态字段时, 以及调用一个类的静态方法时;

​        ②: 当对类进行反射时

​        ③: 当初始化一个类时, 如果发现其父类还没初始化, 先触发其父类的初始化

​        ④: 虚拟机启动时, 用户需要制定一个执行的主类

​        ⑤: 当Method实例最后解析结果REF_getStatic, REF_putStatic, REF_invokeStatic的方法句柄, 并且这个方法句柄所对应的类没有进行初始化

​		类由此组件加载。启动类加载器 (BootStrap class Loader)、扩展类加载器(Extension class Loader)和应用程序类加载器(Application class Loader) 这三种类加载器帮助完成类的加载。

### 1.1 加载

​		①: 启动类加载器 : BootstrapClassLoader，负责加载存放在 JDK\jre\lib(JDK代表JDK的安装目录，下同)下，或被 -Xbootclasspath参数指定的路径中的，并且能被虚拟机识别的类库（如rt.jar，所有的java.开头的类均被 BootstrapClassLoader加载）。启动类加载器是无法被Java程序直接引用的。

​        ②: 扩展类加载器 : ExtensionClassLoader，该加载器由 sun.misc.Launcher$ExtClassLoader实现，它负责加载 JDK\jre\lib\ext目录中，或者由 java.ext.dirs系统变量指定的路径中的所有类库（如javax.开头的类），开发者可以直接使用扩展类加载器。

​        ③: 应用类加载器 : ApplicationClassLoader，该类加载器由 sun.misc.Launcher$AppClassLoader来实现，它负责加载用户类路径（ClassPath）所指定的类，开发者可以直接使用该类加载器，如果应用程序中没有自定义过自己的类加载器，一般情况下这个就是程序中默认的类加载器。

-  **启动类加载器** – 负责从启动类路径中加载类，无非就是**rt.jar**。这个加载器会被赋予最高优先级。

- **扩展类加载器** – 负责加载**ext** 目录**(jre\lib)**内的类。

- **应用程序类加载器** – 负责加载**应用程序级别类路径**，涉及到路径的环境变量等etc.

  ​	上述的**类加载器**会遵循**委托层次算法（Delegation Hierarchy Algorithm）**加载类文件**。**

### 1.2 链接

- **校验** – 字节码校验器会校验生成的字节码是否正确，如果校验失败，我们会得到**校验错误**。

- **准备** – 分配内存并初始化**默认值**给所有的静态变量。

- **解析** – 所有**符号内存引用**被**方法区(Method Area)**的**原始引用**所替代。

### 1.3 初始化

​		这是类加载的最后阶段，这里所有的**静态变量**会被赋初始值**,** 并且**静态块**将被执行。

## 2. 运行时数据区（Runtime Data Area）

​		 运行时数据区域被划分为5个主要组件：方法区，堆区，栈区，PC寄存器，本地方法栈。

### 2.1 方法区（Method Area）

​		所有**类级别数据**将被存储在这里，包括**静态变量**。每个JVM只有一个方法区，它是一个共享的资源。

### 2.2 堆区（Heap Area）

​		所有的**对象**和它们相应的**实例变量**以及**数组**将被存储在这里。每个JVM同样只有一个堆区。由于**方法区**和**堆区**的内存由多个线程共享，所以存储的数据**不是线程安全的**。

### 2.3 栈区（Stack Area）

​		对每个线程会单独创建一个**运行时栈**。对每个**函数呼叫**会在栈内存生成一个**栈帧(Stack Frame)**。所有的**局部变量**将在栈内存中创建。栈区是线程安全的，因为它不是一个共享资源。栈帧被分为三个子实体：

**a 局部变量数组** – 包含多少个与方法相关的**局部变量**并且相应的值将被存储在这里。

**b 操作数栈** – 如果需要执行任何中间操作，**操作数栈**作为运行时工作区去执行指令。

**c 帧数据** – 方法的所有符号都保存在这里。在任意**异常**的情况下，catch块的信息将会被保存在帧数据里面。



**如图是JVM三大核心区域：**

![img](https://img-blog.csdn.net/20180617161343935?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2Fpaml1ZHU=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

### 2.4 PC寄存器

​		每个线程都有一个单独的**PC寄存器**来保存**当前执行指令**的地址，一旦该指令被执行，pc寄存器会被**更新**至下条指令的地址。

### 2.5 本地方法栈

​		本地方法栈保存本地方法信息。对每一个线程，将创建一个单独的本地方法栈。



## 3. 执行引擎

​		分配给**运行时数据区**的字节码将由执行引擎执行。执行引擎读取字节码并逐段执行。

### 3.1 解释器

​		 解释器能快速的解释字节码，但执行却很慢。 解释器的缺点就是,当一个方法被调用多次，每次都需要重新解释。

### 3.2编译器

​		JIT编译器消除了解释器的缺点。执行引擎利用解释器转换字节码，但如果是重复的代码则使用JIT编译器将全部字节码编译成本机代码。本机代码将直接用于重复的方法调用，这提高了系统的性能。

a. **中间代码生成器** – 生成中间代码

b. **代码优化器** – 负责优化上面生成的中间代码

c. **目标代码生成器** – 负责生成机器代码或本机代码

d. **探测器(Profiler)** – 一个特殊的组件，负责寻找被多次调用的方法。

### 3.3 垃圾回收器:

​		收集并删除未引用的对象。可以通过调用*"System.gc()"*来触发垃圾回收，但并不保证会确实进行垃圾回收。JVM的垃圾回收只收集哪些由**new**关键字创建的对象。所以，如果不是用**new**创建的对象，你可以使用**finalize函数**来执行清理。



## **4、Java本地接口 (JNI)**

​		**JNI** 会与**本地方法库**进行交互并提供执行引擎所需的本地库。



## **5、本地方法库**

​		本地方法库是一个执行引擎所需的本地库的集合。



## 6、通过一个小程序认识JVM

```java
package com.spark.jvm;
/**
 * 从JVM调用的角度分析java程序堆内存空间的使用：
 *
 * 当JVM进程启动的时候，会从类加载路径中找到包含main方法的入口类HelloJVM
 * 找到HelloJVM会直接读取该文件中的二进制数据，并且把该类的信息放到运行时的Method内存区域中。
 * 然后会定位到HelloJVM中的main方法的字节码中，并开始执行Main方法中的指令
 * 此时会创建Student实例对象，并且使用student来引用该对象（或者说给该对象命名），其内幕如下：
 * 		第一步：JVM会直接到Method区域中去查找Student类的信息，此时发现没有Student类，就通过类加载器加载该Student类文件；
 * 		第二步：在JVM的Method区域中加载并找到了Student类之后会在Heap区域中为Student实例对象分配内存，
 * 			并且在Student的实例对象中持有指向方法区域中的Student类的引用（内存地址）；
 * 		第三步：JVM实例化完成后会在当前线程中为Stack中的reference建立实际的应用关系，此时会赋值给student
 * 			接下来就是调用方法。
 * 			在JVM中方法的调用一定是属于线程的行为，也就是说方法调用本身会发生在线程的方法调用栈：
 * 				线程的方法调用栈（Method Stack Frames），每一个方法的调用就是方法调用栈中的一个Frame，
 * 				该Frame包含了方法的参数，局部变量，临时数据等 student.sayHello();
 */
public class HelloJVM {
	//在JVM运行的时候会通过反射的方式到Method区域找到入口方法main
	public static void main(String[] args) {//main方法也是放在Method方法区域中的
		/**
		 * student(小写的)是放在主线程中的Stack区域中的
		 * Student对象实例是放在所有线程共享的Heap区域中的
		 */
		Student student = new Student("spark");
		/**
		 * 首先会通过student指针（或句柄）（指针就直接指向堆中的对象，句柄表明有一个中间的,student指向句柄，句柄指向对象
		 * 找Student对象，当找到该对象后会通过对象内部指向方法区域中的指针来调用具体的方法去执行任务
		 */
		student.sayHello();
	}
}
class Student {
	// name本身作为成员是放在stack区域的但是name指向的String对象是放在Heap中
	private String name;
	public Student(String name) {
		this.name = name;
	}
	//sayHello这个方法是放在方法区中的
	public void sayHello() {
	System.out.println("Hello, this is " + this.name);
	}
}
```

**JVM三大性能调优参数：-Xms –Xmx –Xss**

-Xms –Xmx是对堆的性能调优参数，一般两个设置是一样的，如果不一样，当Heap不够用，会发生内存抖动。一般都调大这两个参数，并且两个大小一样。

-Xss是对每一个线程栈的性能调优参数,影响堆栈调用的深度

**实战演示从OOM推导出JVM GC时候基于的内存结构：新生代Young Generation（Eden、From、To）、老生代OldGeneration、Permanent Generation**

**![img](https://img-blog.csdn.net/20170610165614684?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvYWlqaXVkdQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)**



**JVMHeap区域(年轻代、老年代)和方法区(永久代)结构图：**



![img](https://img-blog.csdn.net/20170610165636450?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvYWlqaXVkdQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

​		从Java GC的角度解读代码：程序20行new的Person对象会首先会进入年轻代的Eden中（如果对象太大可能直接进入年老代）。在GC之前对象是存在Eden和from中的，进行GC的时候Eden中的对象被拷贝到To这样一个survive空间（survive（幸存）空间：包括from和to，他们的空间大小是一样的，又叫s1和s2）中（有一个拷贝算法），From中的对象（算法会考虑经过GC幸存的次数）到一定次数  |（阈值（如果说每次GC之后这个对象依旧在Survive中存在，GC一次他的Age就会加1，默认15就会放到OldGeneration。但是实际情况比较复杂，有可能没有到阈值就从Survive区域直接到Old Generation区域。在进行GC的时候会对Survive中的对象进行判断，Survive空间中有一些对象Age是一样的，也就是经过的GC次数一样，年龄相同的这样一批对象的总和大于等于Survive空间一半的话，这组对象就会进入old Generation中，（是一种动态的调整））），| 会被复制到OldGeneration，如果没到次数From中的对象会被复制到To中，复制完成后To中保存的是有效的对象，Eden和From中剩下的都是无效的对象，这个时候就把Eden和From中所有的对象清空。在复制的时候Eden中的对象进入To中，To可能已经满了，这个时候Eden中的对象就会被直接复制到Old Generation中，From中的对象也会直接进入Old Generation中。就是存在这样一种情况，To比较小，第一次复制的时候空间就满了，直接进入old Generation中。复制完成后，To和From的名字会对调一下，因为Eden和From都是空的，对调后Eden和To都是空的，下次分配就会分配到Eden。一直循环这个流程。好处：使用对象最多和效率最高的就是在Young Generation中，通过From to就避免过于频繁的产生FullGC（Old Generation满了一般都会产生FullGC

​		虚拟机在进行MinorGC（新生代的GC）的时候，会判断要进入OldGeneration区域对象的大小，是否大于Old Generation剩余空间大小，如果大于就会发生Full GC。

​		刚分配对象在Eden中，如果空间不足尝试进行GC，回收空间，如果进行了MinorGC空间依旧不够就放入Old Generation，如果OldGeneration空间还不够就OOM了。

​		比较大的对象，数组等，大于某值（可配置）就直接分配到老年代，（避免频繁内存拷贝）

​		**年轻代和年老代属于Heap空间的**

​		**Permanent Generatio**（永久代）可以理解成方法区，（它属于方法区）也有可能发生GC，例如类的实例对象全部被GC了，同时它的类加载器也被GC掉了，这个时候就会触发永久代中对象的GC。

​		如果OldGeneration满了就会产生FullGC。

​		满原因：1，from survive中对象的生命周期到一定阈值

​						2，分配的对象直接是大对象

​						3、由于To 空间不够，进行GC直接把对象拷贝到年老代（年老代GC时候采用不同的算法）

​		如果Young Generation大小分配不合理或空间比较小，这个时候导致对象很容易进入Old Generation中，而Old Generation中回收具体对象的时候速度是远远低于Young Generation回收速度。

​		因此实际分配要考虑年老代和新生代的比例，考虑Eden和survives的比例

​		Permanent Generation中发生GC的时候也对性能影响非常大，也是Full GC。

# JVM GC时候核心参数

**-XX：NewRatio –XX:SurvivorRatio –XX:NewSize –XX:MaxNewSize**

**–XX:NewSize–XX:MaxNewSize指定新生代初始大小和最大大小。**

1，-XX:NewRatio  是年老代 新生代相对的比例，比如NewRatio=2，表明年老代是新生代的2倍。老年代占了heap的2/3，新生代占了1/3

2，-XX:SurvivorRatio 配置的是在新生代里面Eden和一个Servive的比例

如果指定NewRatio还可以指定NewSizeMaxNewSize，如果同时指定了会如何？？？

NewRatio=2，这个时候新生代会尝试分配整个Heap大小的1/3的大小，但是分配的空间不会小于-XX:NewSize也不会大于 –XX:MaxNewSize

3，-XX:NewSize –XX:MaxNewSize

实际设置比例还是设置固定大小，固定大小理论上速度更高。

-XX:NewSize –XX:MaxNewSize理论越大越好，但是整个Heap大小是有限的，一般年轻代的设置大小不要超过年老代。

-XX:SurvivorRatio新生代里面Eden和一个Servive的比例，如果SurvivorRatio是5的话，也就是Eden区域是SurviveTo区域的5倍。Survive由From和To构成。结果就是整个Eden占用了新生代5/7，From和To分别占用了1/7,如果分配不合理，Eden太大，这样产生对象很顺利，但是进行GC有一部分对象幸存下来，拷贝到To，空间小，就没有足够的空间，对象会被放在old Generation中。如果Survive空间大，会有足够的空间容纳GC后存活的对象，但是Eden区域小，会被很快消耗完，这就增加了GC的次数。

# JVM的GC日志解读

**一、 JVM YoungGeneration下MinorGC日志详解**

[GC (Allocation Failure) [PSYoungGen:2336K->288K(2560K)] 8274K->6418K(9728K), 0.0112926 secs] [Times:user=0.06 sys=0.00, real=0.01 secs]

PSYoungGen（是新生代类型，新生代日志收集器），2336K表示使用新生代GC前，占用的内存，->288K表示GC后占用的内存，(2560K)代表整个新生代总共大小

8274K（GC前整个JVM Heap对内存的占用）->6418K（MinorGC后内存占用总量）(9728K)（整个堆的大小）0.0112926 secs（Minor GC消耗的时间）] [Times: user=0.06 sys=0.00, real=0.01 secs] 用户空间，内核空间时间的消耗，real整个的消耗

**二、 JVM的GC日志Full GC日志每个字段彻底详解**

[Full GC (Ergonomics) [PSYoungGen: 984K->425K(2048K)] [ParOldGen:7129K->7129K(7168K)] 8114K->7555K(9216K), [Metaspace:2613K->2613K(1056768K)], 0.1022588 secs] [Times: user=0.56 sys=0.02,real=0.10 secs]

[Full GC (Allocation Failure) [PSYoungGen: 425K->425K(2048K)][ParOldGen: 7129K->7129K(7168K)] 7555K->7555K(9216K), [Metaspace:2613K->2613K(1056768K)], 0.1003696 secs] [Times: user=0.64 sys=0.03,real=0.10 secs]

***\*[Full GC\****（表明是Full GC） ***\*(Ergonomics) [PSYoungGen:\****FullGC会导致新生代Minor GC产生]***\*984K->425K(2048K)][ParOldGen:\****（老年代GC）***\*7129K\****（GC前多大）***\*->7129K\****（GC后，并没有降低内存占用，因为写的程序不断循环一直有引用）***\*(7168K)\**** （老年代总容量）***\*] 8114K\****（GC前占用整个Heap空间大小）***\*->7555K\**** （GC后占用整个Heap空间大小） ***\*(9216K)\**** （整个Heap大小，JVM堆的大小）***\*, [Metaspace:\**** （java6 7是permanentspace，java8改成Metaspace，类相关的一些信息） ***\*2613K->2613K(1056768K)\**** （GC前后基本没变，空间很大）***\*], 0.1022588 secs\****（GC的耗时，秒为单位）***\*] [Times: user=0.56 sys=0.02, real=0.10 secs]\****（用户空间耗时，内核空间耗时，真正的耗时时间）

三、 **Java8中的JVM的MetaSpace**

Metaspace的使用C语言实现的，使用的是OS的空间，Native Memory Space可动态的伸缩，可以根据类加载的信息的情况，在进行GC的时候进行调整自身的大小，来延缓下一次GC的到来。

可以设置Metaspace的大小，如果超过最大大小就会OOM，不设置如果把整个操作系统的内存耗尽了出现OOM，一般会设置一个足够大的初始值，安全其间会设置最大值。

永久代发生GC有两种情况，类的所有的实例被GC掉，且class load不存。

对于元数据空间 简化了GC， class load不存在了就需要进行GC。

# 三种基本的GC算法基石

**一、 标记／清除算法**

内存中的对象构成一棵树，当有效的内存被耗尽的时候，程序就会停止，做两件事，第一：标记，标记从树根可达的对象（途中水红色），第二：清除（清楚不可达的对象）。标记清除的时候有停止程序运行，如果不停止，此时如果存在新产生的对象，这个对象是树根可达的，但是没有被标记（标记已经完成了），会清除掉。

缺点：递归效率低性能低；释放空间不连续容易导致内存碎片；会停止整个程序运行；

![img](https://img-blog.csdn.net/20170610165906970?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvYWlqaXVkdQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

**二、 复制算法**

把内存分成两块区域：空闲区域和活动区域，第一还是标记（标记谁是可达的对象），标记之后把可达的对象复制到空闲区，将空闲区变成活动区，同时把以前活动区对象1，4清除掉，变成空闲区。

速度快但耗费空间，假定活动区域全部是活动对象，这个时候进行交换的时候就相当于多占用了一倍空间，但是没啥用。

![img](https://img-blog.csdn.net/20170610165923256?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvYWlqaXVkdQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

**三、 标记整理算法**

平衡点

标记谁是活跃对象，整理，会把内存对象整理成一课树一个连续的空间，

![img](https://img-blog.csdn.net/20170610165941100?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvYWlqaXVkdQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

**JVM垃圾回收分代收集算法**

综合了上述算法优略

1， 分代GC在新生代的算法：采用了GC的复制算法，速度快，因为新生代一般是新对象，都是瞬态的用了可能很快被释放的对象。

2， 分代GC在年老代的算法 标记／整理算法，GC后会执行压缩，整理到一个连续的空间，这样就维护着下一次分配对象的指针，下一次对象分配就可以采用碰撞指针技术，将新对象分配在第一个空闲的区域。

# JVM垃圾回收器串行、并行、并发垃圾回收器概述

1， JVM中不同的垃圾回收器

2， 串行，并行，并发垃圾回收器（和JVM历史有关系，刚开始串行）

[***\*Java\****](http://lib.csdn.net/base/javase)中Stop-The-World机制简称STW，是在执行垃圾收集[***\*算法\****](http://lib.csdn.net/base/datastructure)时，Java应用程序的其他所有线程都被挂起（除了垃圾收集帮助器之外）。Java中一种全局暂停现象，全局停顿，所有Java代码停止，native代码可以执行，但不能与JVM交互；这些现象多半是由于gc引起。

**JVM中Serial收集器、ParNew收集器、Parallel收集器解析**

Serial收集器 单线程方式（没有线程切换开销，如果受限物理机器单线程可采用）串行且采用stop the world在工作的时候程序会停止

**Serial**和serial old

ParNew收集器：多线程（多CPU和多Core的环境中高效），生产环境对低延时要求高的话，就采用ParNew和CMS组合来进行server端的垃圾回收

Parallel 收集器：多线程，并行， 它可以控制JVM吞吐量的大小，吞吐量优先的收集器，一般设置1%，可设置程序暂停的时间，会通过把新生代空间变小，来完成回收，频繁的小规模垃圾回收，会影响程序吞吐量大小

**JVM中CMS收集器解密**

低延迟进行垃圾回收，在线服务和处理速度要求高的情况下很重要

配置：XX:UseConcMarkSweepGC

***\*concurrence\**\**（并发） Mark\**（标记）Sweep（清理）**

***\*低延时\****

***\*把垃圾回收分成四个阶段\****

***\*CMS-initial-mark\**\**初始标记阶段会stop the world\**，短暂的暂停程序根据跟对象标记的对象所连接的对象是否可达来标记出哪些可到达**

***\*CMS-concurrent-mark\**\**并发标记，根据上一次标记的结果确定哪些不可到达，线程并发或交替之行，基本不会出现程序暂停。\****

***\*CMS-remark\**\**再次标记，会出现程序暂停，所有内存那一时刻静止，确保被全部标记，有可能第二阶段之前有可能被标记为垃圾的对象有可能被引用，在此标记确认。\****

***\*CMS-concurrent-sweep\**\**并发清理垃圾，把标记的垃圾清理掉了，没有压缩，有可能产生内存碎片，不连续的内存块，这时候就不能更好的使用内存，可以通过一个参数配置，根据内存的情况执行压缩。\****

**JVM中G1收集器**

可以像CMS收集器一样，GC操作与应用的现场一起并发执行

紧凑的空闲内存区域且没有很长的GC停顿时间

需要可预测的GC暂停耗时

不想牺牲太多吞吐量性能

启动后不需要请求更大的Java堆

通过案例瞬间理解JVM中PSYoungGen、ParOldGen、MetaSpace

```java
Heap
 PSYoungGen      total 2560K, used 321K[0x00000007bfd00000, 0x00000007c0000000, 0x00000007c0000000)
  eden space 2048K, 15% used[0x00000007bfd00000,0x00000007bfd50568,0x00000007bff00000)
  from space 512K, 0% used[0x00000007bff00000,0x00000007bff00000,0x00000007bff80000)
  to   space 512K, 0% used[0x00000007bff80000,0x00000007bff80000,0x00000007c0000000)
 ParOldGen       total 7168K, used 7097K[0x00000007bf600000, 0x00000007bfd00000, 0x00000007bfd00000)
 object space 7168K, 99%used [0x00000007bf600000,0x00000007bfcee7b8,0x00000007bfd00000)
 Metaspace       used 2647K, capacity 4486K, committed4864K, reserved 1056768
 class space    used 289K, capacity 386K, committed 512K,reserved 1048576K
```

PSYoungGen是eden + from

使用MAT对Dump文件进行分析实战

导出Dump文件

 