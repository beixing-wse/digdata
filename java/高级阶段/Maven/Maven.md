[toc]

# Maven

# 1、为什么使用Maven？【why】

- 添加第三方jar包
- jar包之间的依赖关系,Maven会自动将依赖的jar包导入进来。
- 处理jar包之间的冲突
- 获取第三方jar包
- 将项目拆分为多个工程模块
- 实现项目的分布式部署

# 2、Maven是什么？    【what】

## 2.1. 简介 		

​		Maven【[ˈmevən]】这个词可以翻译为"专家","内⾏"。 作为Apache组织中的⼀个颇为成功的开源项⽬，Maven主要服务于基于java平台的项⽬构建，依赖管理和项⽬信息管理。Maven是一款<font color = "red">服务于Java平台</font>的项目自动化构建工具。

## 2.2. 项目构建⼯具

### 2.2.1什么是构建？

​		构建并不是创建，创建一个工程并不等于构建一个项目。要了解构建的含义我们应该由浅入深的从以下三个层面来看：

①纯 Java 代码

​		大家都知道，我们 Java 是一门编译型语言，.java 扩展名的源文件需要编译成.class 扩展名的字节码文件才能够执行。所以编写任何 Java 代码想要执行的话就必须经过编译得到对应的.class 文件。

②Web 工程

​	当我们需要通过浏览器访问 Java 程序时就必须将包含 Java 程序的 Web 工程编译的结果“拿”到服务器上的指定目录下，并启动服务器才行。这个“拿”的过程我们叫部署。我们可以将未编译的 Web 工程比喻为一只生的鸡，编译好的 Web 工程是一只煮熟的鸡，编译部署的过程就是将鸡炖熟。

③实际项目

​		在实际项目中整合第三方框架，Web 工程中除了 Java 程序和 JSP 页面、图片等静态资源之外，还包括第三方框架的 jar 包以及各种各样的配置文件。所有这些资源都必须按照正确的目录结构部署到服务器上，项目才可以运行。
​		所以综上所述：构建就是以我们编写的 Java 代码、框架配置文件、国际化等其他资源文件、JSP 页面和图片等静态资源作为“原材料”，去“生产”出一个可以运行的项目的过程。

**Ant构建**

​		最早的构建⼯具，基于IDE, ⼤概是2000年有的，当时是最流⾏java构建⼯具，不过它的XML脚本编写格式让XML⽂件特别⼤。对⼯程构建过程中的过程控制特别好 .

**Maven【JAVA】**

​		项⽬对象模型，通过其描述信息来管理项⽬的构建，报告和⽂档的软件项⽬管理⼯具。它填补了Ant缺点，Maven第⼀次⽀持了从⽹络上下载的功能，仍然采⽤xml作为配置⽂件格式。Maven专注的是依赖管理，使⽤Java编写。

**Gradle**

​		属于结合以上两个的优点，它继承了Ant的灵活和Maven的⽣命周期管理，它最后被google作为了Android御⽤管理⼯具。它最⼤的区别是不⽤XML作为配置⽂件格式，采⽤了DSL格式，使得脚本更加简洁。 

​		⽬前市⾯上Ant⽐较⽼, 所以⼀般是⼀些⽐较传统的软件企业公司使⽤, Maven使⽤Java编写, 是当下⼤多数互联⽹公司会使⽤的⼀个构建⼯具, 中⽂⽂档也⽐较⻬全, gradle是⽤groovy编写, ⽬前⽐较新型的构建⼯具⼀些初创互联⽹公司会使⽤, 以后会有很⼤的使⽤空间.

### 2.2.2构建过程

​		①清理 清理：删除以前的编译结果，为重新编译做好准备。
​		②编译 编译：将 Java 源程序编译为字节码文件。
​		③测试 测试：针对项目中的关键点进行测试，确保项目在迭代开发过程中关键点的正确性。
​		④报告 报告：在每一次测试后以标准的格式记录和展示测试结果。
​		⑤打包 打包：将一个包含诸多文件的工程封装为一个压缩文件用于安装或部署。Java 工程对应 jar 包，Web工程对应 war 包。
​		⑥安装 安装：在 Maven 环境下特指将打包的结果——jar 包或 war 包安装到本地仓库中。
​		⑦部署 部署：将打包的结果部署到远程仓库或将 war 包部署到服务器上运行。

### 2.2.3Maven 核心概念

​		Maven 能够实现自动化构建是和它的内部原理分不开的，这里我们从 Maven 的九个核心概念入手，看看 Maven 是如何实现自动化构建的
​		①POM
​		②约定的目录结构
​		③坐标		
​		④依赖管理
​		⑤仓库管理
​		⑥生命周期
​		⑦插件和目标
​		⑧继承
​		⑨聚合

## 2.3. Maven的四⼤特性

### 2.3.1. 依赖管理系统

​		Maven为Java世界引⼊了⼀个新的依赖管理系统jar包管理 jar 升级时修改配置⽂件即可。在Java世界中，可以⽤groupId、artifactId、version组成的Coordination（坐标）唯⼀标识⼀个依赖。
​		任何基于Maven构建的项⽬⾃身也必须定义这三项属性，⽣成的包可以是Jar包，也可以是war包或者jar包。⼀个典型的依赖引⽤如下所示：

```xml
<dependency>
    <groupId>javax.servlet</groupId> com.baidu
    <artifactId>javax.servlet-api</artifactId> ueditor echarts
    <version>3.1.0</version>
</dependency>
```

**坐标属性的理解**

​		Maven坐标为各种组件引⼊了秩序，任何⼀个组件都必须明确定义⾃⼰的坐标。

**groupId**

​		定义当前Maven项⽬⾪属的实际项⽬-公司名称。（jar包所在仓库路径） 由于Maven中模块的概念，因此⼀个实际项⽬往往会被划分为很多模块。 ⽐如spring是⼀个实际项⽬，其对应的Maven模块会有很多，如spring-core,spring-webmvc等。

**artifactId**

​		该元素定义实际项⽬中的⼀个Maven模块-项⽬名， 推荐的做法是使⽤实际项⽬名称作为artifactId的前缀。 ⽐如： spring-bean, spring-webmvc等。

**version**

​		该元素定义Maven项⽬当前所处的版本。

### 2.3.2. 多模块构建

​		项⽬复查时 dao, service, controller 层分离将⼀个项⽬分解为多个模块已经是很通⽤的⼀种⽅式。
​		在Maven中需要定义⼀个parent POM作为⼀组module的聚合POM。在该POM中可以使⽤ 标签来定义⼀组⼦模块。parent POM不会有什么实际构建产出。⽽parent POM中的build配置以及依赖配置都会⾃动继承给⼦module。

### 2.3.3. ⼀致的项目结构

​		Ant时代⼤家创建Java项⽬⽬录时⽐较随意，然后通过Ant配置指定哪些属于source，那些属于testSource等。⽽<font color = "red">Maven在设计之初的理念就是Conversion over configuration（约定⼤于配置）</font>。其制定了⼀套项⽬⽬录结构作为标准的Java项⽬结构,解决不同ide 带来的⽂件⽬录不⼀致问题。

​		现在 JavaEE 开发领域普遍认同一个观点：<font color = "red">约定>配置>编码</font>。意思就是能用配置解决的问题就不编码，能基于约定的就不进行配置。而 Maven 正是因为指定了特定文件保存的目录才能够对我们的 Java 工程进行自动化构建。

### 2.3.4. ⼀致的构建模型和插件机制

```xml
<plugin>
    <groupId>org.mortbay.jetty</groupId>
    <artifactId>maven-jetty-plugin</artifactId>
    <version>6.1.25</version>
    <configuration>
        <scanIntervalSeconds>10</scanIntervalSeconds>
        <contextPath>/test</contextPath>
    </configuration>
</plugin>
```

# 3、Maven环境下构建多模块项目

​		使⽤maven 提供的多模块构建的特性完成maven 环境下多个模块的项⽬的管理与构建。

```
这⾥以四个模块为例来搭建项⽬,以达到通俗易懂的初衷

模块 maven_parent —– 基模块,就是常说的parent （pom）

模块 maven_dao —– 数据库的访问层，例如jdbc操作（jar）

模块 maven_service —– 项⽬的业务逻辑层 （jar）

模块 maven_controller —– ⽤来接收请求，响应数据 （war）
```

# 4、POM

Project Object Model：项目对象模型。将 Java 工程 工程的相关信息封装为 对象作为便于操作和管理的 模型。
Maven 工程的核心配置。可以说学习 Maven 就是学习 pom.xml 文件中的配置。

# 5、坐标

## 6.1 几何中的坐标

- 在一个平面中使用 x、y 两个向量可以唯一的确定平面中的一个点。
- 在空间中使用 x、y、z 三个向量可以唯一的确定空间中的一个点。

## 6.2 Maven 的坐标

​		使用如下三个向量在 Maven 的仓库中唯一的确定一个 Maven 工程。

- groupid：公司或组织的域名倒序+当前项目名称

- artifactId：当前项目的模块名称

- version：当前模块的版本

  ```xml
  <groupId>com.atguigu.maven</groupId>
  <artifactId>Hello</artifactId>
  <version>0.0.1-SNAPSHOT</version>
  ```

  

## 6.3 如何通过坐标到仓库中查找 jar 包？

- 将 gav 三个向量连起来
  com.atguigu.maven+Hello+0.0.1-SNAPSHOT
- 以连起来的字符串作为目录结构到仓库中查找
  com/atguigu/maven/Hello/0.0.1-SNAPSHOT/Hello-0.0.1-SNAPSHOT.jar
- ※注意：我们自己的 Maven 工程必须执行安装操作才会进入仓库。安装的命令是：mvn install

# 6、依赖

​		Maven 中最关键的部分，我们使用 Maven 最主要的就是使用它的依赖管理功能。要理解和掌握 Maven的依赖管理，我们只需要解决一下几个问题：

①依赖的目的是什么
		当 A jar 包用到了 B jar 包中的某些类时，A 就对 B 产生了依赖，这是概念上的描述。那么如何在项目中以依赖的方式引入一个我们需要的 jar 包呢？
答案非常简单，就是使用 dependency 标签指定被依赖 jar 包的坐标就可以了。

```xml
<dependency>
<groupId> com.atguigu.maven </groupId>
<artifactId> Hello </artifactId>
<version> 0.0.1- - SNAPSHOT </version>
<scope>compile</scope>
</dependency>
```

②依赖的范围

​		大家注意到上面的依赖信息中除了目标 jar 包的坐标还有一个 scope 设置，这是依赖的范围。依赖的范围有几个可选值，我们用得到的是：compile、test、provided 三个。

## 6.1. 依赖的基本配置

根元素project下的dependencies可以包含多个 dependence元素，以声明多个依赖。每个依赖都应该包
含以下元素：

1. groupId, artifactId, version : 依赖的基本坐标， 对于任何⼀个依赖来说，基本坐标是最重要的，Maven根据坐标才能找到需要的依赖。
2. Type： 依赖的类型，⼤部分情况下不需要声明。 默认值为jar
3. Scope： 依赖范围（compile,test,provided,runtime,system）

- compile: 编译依赖范围。
  如果没有指定，就会默认使⽤该依赖范围。使⽤此依赖范围的Maven依赖，对于编译、测
  试、运⾏三种classpath都有效。
- test: 测试依赖范围。
  使⽤此依赖范围的Maven依赖，只对于测试classpath有效，在编译主代码或者运⾏项⽬的使⽤时将⽆法使⽤此类依赖。典型的例⼦就是JUnit，它只有在编译测试代码及运⾏测试的时候才需要。
- provided: 已提供依赖范围。
  使⽤此依赖范围的Maven依赖，对于编译和测试classpath有效，但在运⾏时⽆效。典型的例⼦是servlet-api，编译和测试项⽬的时候需要该依赖，但在运⾏项⽬的时候，由于容器已经提供，就不需要Maven重复地引⼊⼀遍(如：servlet-api)。
- runtime: 运⾏时依赖范围。
  使⽤此依赖范围的Maven依赖，对于测试和运⾏classpath有效，但在编译主代码时⽆效。典型的例⼦是JDBC驱动实现，项⽬主代码的编译只需要JDK提供的JDBC接⼝，只有在执⾏测试或者运⾏项⽬的时候才需要实现上述接⼝的具体JDBC驱动。
- system: 系统依赖范围。
  该依赖与三种classpath的关系，和provided依赖范围完全⼀致。但是，使⽤system范围依赖时必须通过systemPath元素显式地指定依赖⽂件的路径。由于此类依赖不是通过Maven仓库解析的，⽽且往往与本机系统绑定，可能造成构建的不可移植，因此应该谨慎使⽤。

4. Optional：标记依赖是否可选
5. Exclusions： ⽤来排除传递性依赖。

## 6.2. 依赖范围

​		⾸先需要知道，Maven在编译项⽬主代码的时候需要使⽤⼀套classpath。 ⽐如：编译项⽬代码的时候需要⽤到spring-core, 该⽂件以依赖的⽅式被引⼊到classpath中。 其次， Maven在执⾏测试的时候会使⽤另外⼀套classpath。 如：junit。
​		最后在实际运⾏项⽬时，⼜会使⽤⼀套classpath， spring-core需要在该classpath中，⽽junit不需要。
​		那么依赖范围就是⽤来控制依赖与这三种classpath(编译classpath，测试classpath，运⾏时classpath)的关系， Maven有以下⼏种依赖范围：

- Compile 编译依赖范围。 如果没有指定，就会默认使⽤该依赖范围。 使⽤此依赖范围的Maven依
  赖， 对于编译，测试，运⾏都有效。
- Test： 测试依赖范围。 只在测试的时候需要。⽐如junit
- Provided： 已提供依赖范围。 使⽤此依赖范围的Maven依赖，对于编译和测试有效， 但在运⾏时⽆效。 典型的例⼦是servlet-API, 编译和测试项⽬的需要， 但在运⾏项⽬时， 由于容器已经提供，就不需要Maven重复地引⼊⼀遍。
- Runtime： 运⾏时依赖范围。 使⽤此依赖范围的Maven依赖，对于测试和运⾏有效， 但在编译代码时⽆效。 典型的例⼦是：jdbc驱动程序， 项⽬主代码的编译只需要jdk提供的jdbc接⼝，只有在执⾏测试或者运⾏项⽬的时候才需要实现上述接⼝的具体jdbc驱动。
- System： 系统依赖范围。 ⼀般不使⽤。

