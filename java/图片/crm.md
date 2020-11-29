CRM - ⽤户管理

# 1、学习⽬标

![](G:\java\我的笔记\java\项目1\笔记图片\01-CRM用户管理.bmp)

# 2、CRM 系统概念与项⽬开发流程

## 2.1. CRM 基本概念

​		圈内存在这么⼀句话：“世上本来没有CRM，⼤家的⽣意越来越难做了，才有了CRM。” 在同质化竞争时代，顾客资产尤为重要，新时代在呼唤CRM。

​		<font color = "red">CRM 系统即客户关系管理系统，顾名思义就是管理公司与客户之间的关系</font>。是⼀种以"客户关系⼀对⼀理论"为基础，旨在改善企业与客户之间关系的新型管理机制。客户关系管理的定义是：企业为提⾼核⼼竞争⼒，利⽤相应的信息技术以及互联⽹技术来协调企业与顾客间在销售、营销和服务上的交互，从⽽提升其管理⽅式，向客户提供创新式的个性化的客户交互和服务的过程。<font color = "red">其最终⽬标是吸引新客户、保留⽼客户以及将已有客户转为忠实客户，增加公司市场份额</font>。

​		CRM 的实施⽬标就是通过全⾯提升企业业务流程的管理来降低企业成本，通过提供更快速和周到的优质服务来吸引和保持更多的客户。作为⼀种新型管理机制，CRM 极⼤地改善了企业与客户之间的关系，应⽤于企业的市场营销、销售、服务与技术⽀持等与客户相关的领域。

## 2.2. CRM 分类

​		根据客户的类型不同，CRM 可以分为<font color = "red">B to B CRM 及B to C CRM</font>。BtoB CRM 中管理的客户是企业客户，⽽B to C CRM 管理的客户则是个⼈客户。提供企业产品销售和服务的企业需要的B to B 的CRM，也就是市⾯上⼤部分CRM 的内容。⽽提供个⼈及家庭消费的企业需要的是B to C 的CRM。

​		根据CRM 管理侧重点不同⼜分为操作性和分析型CRM。<font color = "red">⼤部分CRM 为操作型CRM</font>，⽀持CRM的⽇常作业流程的每个环节，⽽分析型CRM 则偏重于数据分析。

## 2.3. 企业项⽬开发流程

![](G:\java\我的笔记\java\项目1\笔记图片\crm-2企业项目开发流程.bmp)

1. 产品组根据市场调研或商户同事的反馈提出idea，设计出原型然后跟市场, 商户同事进⾏确认
2. UI 设计组和开发组⼀起讨论，确定⽅案是否可⾏
3. UI 组根据产品组提供的原型稿做出设计稿，与产品和开发确认
4. 开发组根据产品的原型稿(看逻辑)和UI组的设计稿(看界⾯)编写代码其中当然也会来回跟设计, 产品
  同学进⾏确认和沟通
5. 代码编写完毕后提交给测试组. 然后再提交上线
6. 后期的数据跟踪和优化
  这就是⼀个产品研发的⼤致流程。其中开发的责任就是选⽤合适的框架技术来完成产品所提供的需求
  以及设计所提供的效果。
# 3、CRM 系统模块划分

## 3.1. 系统功能模块图

![](G:\java\我的笔记\java\项目1\笔记图片\CRM-3CRM核心模块.bmp)

## 3.2. 模块功能描述

### 3.2.1. 基础模块

​		包含系统基本的<font color = "red">⽤户登录，退出，记住我，密码修改</font>等基本操作。

### 3.2.2. 营销管理

​		营销机会管理：企业客户的质询需求所建⽴的信息录⼊功能，⽅便销售⼈员进⾏后续的客户需求跟踪。

​		营销开发计划：开发计划是根据营销机会⽽来，对于企业质询的客户，会有相应的销售⼈员对于该客户进⾏具体的沟通交流，此时对于整个Crm 系统⽽⾔，通过营销开发计划来进⾏相应的信息管理，提⾼客户的购买企业产品的可能性。

### 3.2.3. 客户管理

​		客户信息管理：Crm 系统中完整记录客户信息来源的数据、企业与客户交往、客户订单查询等信息录⼊功能，⽅便企业与客户进⾏相应的信息交流与后续合作。

​		客户流失管理：Crm 通过⼀定规则机制所定义的流失客户（⽆效客户），通过该规则可以有效管理客户信息资源，提⾼营销开发的效率。

### 3.2.4. 服务管理

​		服务管理是针对客户⽽开发的功能，针对<font color = "red">客户要求</font>，Crm 提供客户相应的信息质询，反馈与投诉功能，提⾼企业对于客户的服务质量。

### 3.2.5. 数据报表

​		Crm 提供的数据报表功能能够帮助企业了解客户整体分布，了解客户开发结果整体信息，从⽽帮助企业整体调整客户开发计划，提⾼企业的在市场中的竞争⼒度。

### 3.2.6. 系统管理

​		系统管理包含常量字典维护⼯作，以及权限管理模块，Crm 权限管理是基于⻆⾊的⼀种权限控制，基于RBAC 实现基于⻆⾊的权限控制，通过不同⻆⾊的⽤户登录该系统后展示系统不同的操作功能，从⽽达到对不同⻆⾊完成不同操作功能。

# 4、CRM 系统数据库设计

​		CRM 系统根据产品的原型稿以及UI组的设计稿，接下来就要设计数据库，⼀般在⼤公司通常会有专⻔的DBA，这时我们可以不要考虑数据库表设计，但是也要能够读懂或者了解DBA的设计思路⽅便在程序开发阶段不会出现问题，<font color = "red">⼀般关系型数据库表设计满⾜三范式的设计即可，表名设计做到⻅名知意最好</font>。

## 4.1. E-R图表简介

### 4.1.1. 营销管理模块

![](G:\java\我的笔记\java\项目1\笔记图片\CRM-4营销管理模块.bmp)

### 4.1.2. 客户管理模块

#### 4.1.2.1. 客户信息管理

![](G:\java\我的笔记\java\项目1\笔记图片\CRM-5客户管理模块.bmp)

#### 4.1.2.2. 客户流失管理

![](G:\java\我的笔记\java\项目1\笔记图片\CRM-6客户流失管理.bmp)

### 4.1.3. 服务管理

![](G:\java\我的笔记\java\项目1\笔记图片\CRM-7服务管理.bmp)

### 4.1.4. 系统管理

#### 4.1.4.1. 权限模块E-R 模型

![](G:\java\我的笔记\java\项目1\笔记图片\CRM-8 权限模块E-R 模型.bmp)

#### 4.1.4.2. 字典&⽇志管理

![](G:\java\我的笔记\java\项目1\笔记图片\CRM-9字典&⽇志管理.bmp)

## 4.2. 表结构详情

| t_sale_chance | 营销机会表    |                |          |          |
| ------------- | ------------- | -------------- | -------- | -------- |
|               | 字段          | 字段类型       | 字段限制 | 字段描述 |
| 主键          | id            | int(11)        | 自增     | id主键   |
|               | chance_source | varchar(300)   | 可空     | 机会来源 |
|               | customer_name | varchar(100)   | 可空     | 客户名称 |
|               | cgil          | int(11)        | 可空     | 成功⼏率 |
|               | overview      | varchar（300） | 可空     | 概要     |
|               | link_man      | varchar(100)   | 可空     | 联系⼈   |
|               | link_phone    | varchar(100)   | 可空     | ⼿机号   |
|               | description   | varchar(1000)  | 可空     | 描述     |
|               | create_man    | varchar(100)   | 可空     | 创建⼈   |
|               | assign_man    | varchar(100)   | 可空     | 分配⼈   |
|               | assign_time   | datetime       | 可空     | 分配时间 |
|               | state         | int(11)        | 可空     | 分配状态 |
|               | dev_result    | int(11)        | 可空     | 开发结果 |
|               | is_valid      | int(4)         | 可空     | 有效状态 |
|               | create_date   | datetime       | 可空     | 创建时间 |
|               | update_date   | datetime       | 可空     | 更新时间 |

| t_cus_dev_plan | 客户开发计划表 |              |          |            |
| -------------- | -------------- | ------------ | -------- | ---------- |
|                | 字段           | 字段类型     | 字段限制 | 字段描述   |
| 主键           | id             | int(11)      | ⾃增     | id         |
|                | sale_chance_id | int(11       | 可空     | 营销机会id |
|                | plan_item      | varchar(100) | 可空     | 计划内容   |
|                | plan_date      | datetime     | 可空     | 计划⽇期   |
|                | exe_affect     | varchar(100) | 可空     | 执⾏效果   |
|                | create_date    | datetime     | 可空     | 创建时间   |
|                | update_date    | datetime     | 可空     | 更新时间   |
|                | is_valid       | int(4)       | 可空     | 有效状态   |

t_sale_chance 营销机会表
字段字段类型字段限制字段描述
主键id int(11) ⾃增id主键
chance_source varchar(300) 可空机会来源
customer_name varchar(100) 可空客户名称
cgjl int(11) 可空成功⼏率
overview varchar(300) 可空概要
link_man varchar(100) 可空联系⼈
link_phone varchar(100) 可空⼿机号
description varchar(1000) 可空描述
create_man varchar(100) 可空创建⼈
assign_man varchar(100) 可空分配⼈
assign_time datetime 可空分配时间
state int(11) 可空分配状态
dev_result int(11) 可空开发结果
is_valid int(4) 可空有效状态
create_date datetime 可空创建时间
update_date datetime 可空更新时间
t_cus_dev_plan 客户开发计划表
字段字段类型字段限制字段描述
主键id int(11) ⾃增id
sale_chance_id int(11) 可空营销机会id
plan_item varchar(100) 可空计划内容
plan_date datetime 可空计划⽇期
exe_affect varchar(100) 可空执⾏效果
create_date datetime 可空创建时间
update_date datetime 可空更新时间
is_valid int(4) 可空有效状态
t_customer 客户信息表
字段字段类型字段限制字段描述
主键id int(11) ⾃增id主键
khno varchar(20) 可空客户编号
name varchar(20) 可空客户姓名
area varchar(20) 可空客户所属地区
cus_manager varchar(20) 可空客户经理
level varchar(30) 可空客户级别
myd varchar(30) 可空客户满意度
xyd varchar(30) 可空客户信⽤度
address varchar(500) 可空客户地址
post_code varchar(50) 可空邮编
phone varchar(20) 可空联系电话
fax varchar(20) 可空传真
web_site varchar(20) 可空⽹址
yyzzzch varchar(50) 可空营业执照注册号
fr varchar(20) 可空法⼈代表
zczj varchar(20) 可空注册资⾦
nyye varchar(20) 可空年营业额
khyh varchar(50) 可空开户银⾏
khzh varchar(50) 可空开户账号
dsdjh varchar(50) 可空地税登记号
gsdjh varchar(50) 可空国税登记号
state int(11) 可空流失状态
is_valid int(4) 可空有效状态
create_date datetime 可空创建时间
update_date datetime 可空更新时间
t_customer_contact 客户交往记录表
字段字段类型字段限制字段描述
主键id int(11) ⾃增id主键
cus_id int(11) 可空客户id
contact_time datetime 可空交往时间
address varchar(500) 可空交往地址
overview varchar(100) 可空概要
create_date datetime 可空创建时间
update_date datetime 可空更新时间
is_valid int(4) 可空有效状态
t_customer_linkman 客户联系⼈表
字段字段类型字段限制字段描述
主键id int(11) ⾃增id主键
cus_id int(11) 可空客户id
link_name varchar(20) 可空联系⼈姓名
sex varchar(20) 可空性别
zhiwei varchar(50) 可空职位
office_phone varchar(50) 可空办公电话
phone varchar(20) 可空⼿机号
is_valid int(4) 可空有效状态
create_date datetime 可空创建时间
update_date datetime 可空更新时间
t_customer_loss 客户流失表
字段字段类型字段限制字段描述
主键id int(11) ⾃增id主键
cus_no varchar(40) 可空客户编号
cus_name varchar(20) 可空客户姓名
cus_manager varchar(20) 可空客户经理
last_order_time date 可空最后下单时间
confirm_loss_time date 可空确认流失时间
state int(11) 可空流失状态
loss_reason varchar(1000) 可空流失原因
is_valid tinyint(4) 可空有效状态
create_date datetime 可空创建时间
update_date datetime 可空更新时间
t_customer_order 客户订单
字段字段类型字段限制字段描述
主键id int(11) ⾃增id主键
cus_id int(11) 可空客户id
order_no varchar(40) 可空订单编号
order_date datetime 可空下单时间
address varchar(200) 可空地址
state int(11) 可空状态
create_date datetime 可空创建时间
update_date datetime 可空更新时间
is_valid int(4) 可空有效状态
t_order_details 订单详情表
字段字段类型字段限制字段描述
主键id int(11) ⾃增id主键
order_id int(11) 可空订单id
goods_name varchar(100) 可空商品名称
goods_num int(11) 可空商品数量
unit varchar(20) 可空商品单位
price float 可空单价
sum float 可空总⾦额
is_valid int(4) 可空有效状态
create_date datetime 可空创建时间
update_date datetime 可空更新时间
t_customer_reprieve 客户流失暂缓表
字段字段类型字段限制字段描述
主键id int(11) ⾃增id主键
loss_id int(11) 可空流失id
measure varchar(500) 可空措施
is_valid tinyint(4) 可空有效状态
create_date datetime 可空创建时间
update_date datetime 可空更新时间
t_customer_serve 客户服务表
字段字段类型字段限制字段描述
主键id int(11) ⾃增id主键
serve_type varchar(30) 可空服务类型
overview varchar(500) 可空概要
customer varchar(30) 可空客户
state varchar(20) 可空服务状态
service_request varchar(500) 可空服务请求
create_people varchar(100) 可空服务创建⼈
assigner varchar(100) 可空服务分配⼈
assign_time datetime 可空分配时间
service_proce varchar(500) 可空服务处理
service_proce_people varchar(20) 可空服务处理⼈
service_proce_time datetime 可空服务处理时间
service_proce_result varchar(500) 可空处理结果
myd varchar(50) 可空满意度
is_valid int(4) 可空是否有效
update_date datetime 可空更新时间
create_date datetime 可空创建时间
t_datadic 字典表
字段字段类型字段限制字段描述
主键id int(11) ⾃增id主键
data_dic_name varchar(50) 可空字典名
data_dic_value varchar(50) 可空字典值
is_valid tinyint(4) 可空是否有效
create_date datetime 可空创建时间
update_date datetime 可空更新时间
t_user ⽤户表
字段字段类型字段限制字段描述
主键id int(11) ⾃增字段描述
user_name varchar(20) 可空⽤户名
user_pwd varchar(100) 可空⽤户密码
true_name varchar(20) 可空真实姓名
email varchar(30) 可空邮箱
phone varchar(20) 可空电话
is_valid int(4) 可空有效状态
create_date datetime 可空创建时间
update_date datetime 可空更新时间
t_role ⻆⾊表
字段字段类型字段限制字段描述
主键id int(11) ⾃增
role_name varchar(255) 可空⻆⾊名
role_remarker varchar(255) 可空⻆⾊备注
create_date datetime 可空创建时间
update_date datetime 更新时间
is_valid int(11) ⾮空是否有效

1. 项⽬环境搭建与测试
   5.1. 项⽬技术栈
   5.2. 环境搭建与测试
   5.2.1. 新建项⽬
   在IDEA 中，新建SpringBoot 项⽬，项⽬名设置为crm
   5.2.2. 引⼊坐标& 插件
   在pom.xml ⽂件中，添加项⽬集成环境所需要的依赖坐标与插件
   <properties>
   <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
   <maven.compiler.source>1.8</maven.compiler.source>
   <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   <parent>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-parent</artifactId>
   <version>2.2.2.RELEASE</version>
   </parent>
   <dependencies>
   <!-- web 环境-->
   <dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-web</artifactId>
   </dependency>
   <!-- aop -->
   <dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-aop</artifactId>
   </dependency>
   <!-- freemarker -->
   <dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-freemarker</artifactId>
   </dependency>
   <!-- 测试环境-->
   <dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-test</artifactId>
   <scope>test</scope>
   </dependency>
   <!-- mybatis -->
   <dependency>
   <groupId>org.mybatis.spring.boot</groupId>
   <artifactId>mybatis-spring-boot-starter</artifactId>
   <version>2.1.1</version>
   </dependency>
   <!-- 分⻚插件-->
   <dependency>
   <groupId>com.github.pagehelper</groupId>
   <artifactId>pagehelper-spring-boot-starter</artifactId>
   <version>1.2.13</version>
   </dependency>
   <!-- mysql -->
   <dependency>
   <groupId>mysql</groupId>
   <artifactId>mysql-connector-java</artifactId>
   <scope>runtime</scope>
   </dependency>
   <!-- c3p0 -->
   <dependency>
   <groupId>com.mchange</groupId>
   <artifactId>c3p0</artifactId>
   <version>0.9.5.5</version>
   </dependency>
   <!-- commons-lang3 -->
   <dependency>
   <groupId>org.apache.commons</groupId>
   <artifactId>commons-lang3</artifactId>
   <version>3.5</version>
   </dependency>
   <!-- json -->
   <dependency>
   <groupId>com.alibaba</groupId>
   <artifactId>fastjson</artifactId>
   <version>1.2.47</version>
   5.2.3. 添加配置⽂件
   src/main/resources ⽬录下新建application.yml 配置⽂件，内容如下：
   </dependency>
   <!-- DevTools 热部署-->
   <dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-devtools</artifactId>
   <optional>true</optional>
   </dependency>
   </dependencies>
   <build>
   <plugins>
   <plugin>
   <groupId>org.apache.maven.plugins</groupId>
   <artifactId>maven-compiler-plugin</artifactId>
   <version>2.3.2</version>
   <configuration>
   <source>1.8</source>
   <target>1.8</target>
   <encoding>UTF-8</encoding>
   </configuration>
   </plugin>
   <plugin>
   <groupId>org.mybatis.generator</groupId>
   <artifactId>mybatis-generator-maven-plugin</artifactId>
   <version>1.3.2</version>
   <configuration>
   <configurationFile>src/main/resources/generatorConfig.xml</configurationFile>
   <verbose>true</verbose>
   <overwrite>true</overwrite>
   </configuration>
   </plugin>
   <plugin>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-maven-plugin</artifactId>
   <configuration>
   <!-- 如果没有该配置，热部署的devtools不⽣效-->
   <fork>true</fork>
   </configuration>
   </plugin>
   </plugins>
   </build>

## 端下⽂路径

server:
port: 8080
servlet:
5.2.4. 添加视图转发
新建com.xxxx.crm.controller 包，添加系统登录，主⻚⾯转发代码。(这⾥先引⼊base 包，具体⽂件⻅
相关⽬录)
context-path: /crm

## 数据源配置

spring:
datasource:
type: com.mchange.v2.c3p0.ComboPooledDataSource
driver-class-name: com.mysql.cj.jdbc.Driver
url: jdbc:mysql://127.0.0.1:3306/crm?
useUnicode=true&characterEncoding=utf8&serverTimezone=GMT%2B8
username: root
password: root

## freemarker

freemarker:
suffix: .ftl
content-type: text/html
charset: UTF-8
template-loader-path: classpath:/views/

## 启⽤热部署

devtools:
restart:
enabled: true
additional-paths: src/main/java

## mybatis 配置

mybatis:
mapper-locations: classpath:/mappers/*.xml
type-aliases-package: com.xxxx.crm.vo;com.xxxx.crm.query;com.xxxx.crm.dto
configuration:
map-underscore-to-camel-case: true

## pageHelper 分⻚

pagehelper:
helper-dialect: mysql

## 设置dao ⽇志打印级别

logging:
level:
com:
xxxx:
crm:
dao: debug
package com.xxxx.crm.controller;
import com.xxxx.crm.base.BaseController;
5.2.5. 添加静态资源
在src/main/resources ⽬录下新建public ⽬录，存放系统相关静态资源⽂件，拷⻉静态⽂件内容到
public ⽬录。
5.2.6. 添加视图模板
在src/main/resources ⽬录下新建views ⽬录，添加index.ftl、main.ftl 等⽂件。(具体视图⽂件详⻅相关
⽬录)
5.2.7. 添加应⽤启动类
在com.xxxx.crm 包下新建Starter.java ，添加启动项⽬相关代码如下：
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
@Controller
public class IndexController extends BaseController {
/**

* 系统登录⻚
* @return
  */
  @RequestMapping("index")
  public String index(){
  return "index";
  }
  // 系统界⾯欢迎⻚
  @RequestMapping("welcome")
  public String welcome(){
  return "welcome";
  }
  /**
* 后端管理主⻚⾯
* @return
  */
  @RequestMapping("main")
  public String main(){
  return "main";
  }
  }
  5.2.8. 项⽬⽬录结构
  5.2.9. 浏览器访问
  package com.xxxx.crm;
  import org.springframework.boot.SpringApplication;
  import org.springframework.boot.autoconfigure.SpringBootApplication;
  @SpringBootApplication
  public class Starter {
  public static void main(String[] args) {
  SpringApplication.run(Starter.class);
  }
  }
  Chrome浏览器访问登录⻚地址：http://localhost:8080/crm/index
  Chrome浏览器访问系统主⻚地址：http://localhost:8080/crm/main

6. ⽤户登录功能实现
   6.1. 准备⼯作
   6.1.1. ⼯具类与⾃定义异常类
   将⼯具类与⾃定义异常类，拷⻉到项⽬中。(这⾥拷⻉utils 包和exceptions 包，具体⽂件⻅相关⽬录)
   6.1.2. ⾃动⽣成代码
   6.1.2.1. generatorConfig.xml
   在src/main/resources ⽬录下，添加generatorConfig.xml 配置⽂件。（需要修改数据库驱动路径、数据
   库账号密码等信息。）
   <?xml version="1.0" encoding="UTF-8"?>

<!DOCTYPE generatorConfiguration
PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"
"http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">
<generatorConfiguration>
<!-- 数据库驱动路径：在左侧project边栏的External Libraries中找到mysql的驱动，右键选择copy
path -->
<classPathEntry
location="C:/java/m2/repository/mysql/mysql-connector-java/5.1.39/mysqlconnector-
java-5.1.39.jar"/>
<!-- context 是逆向⼯程的主要配置信息，id：起个名字，targetRuntime：设置⽣成的⽂件适⽤于哪个
mybatis版本-->
<context id="DB2Tables" targetRuntime="MyBatis3">
<!--optional,指在创建class时，对注释进⾏控制-->
<commentGenerator>
<!-- 是否去除⽇期那⾏注释-->
<property name="suppressDate" value="true"/>
<!-- 是否去除⾃动⽣成的注释true：是：false:否-->
<property name="suppressAllComments" value="true"/>
</commentGenerator>
<!-- 数据库链接地址账号密码-->
<jdbcConnection
driverClass="com.mysql.cj.jdbc.Driver"
connectionURL="jdbc:mysql://127.0.0.1:3306/crm?serverTimezone=GMT%2B8"
userId="root"
password="root">
</jdbcConnection>
<!--
java类型处理器
⽤于处理DB中的类型到Java中的类型，默认使⽤JavaTypeResolverDefaultImpl；
6.1.2.2. 执⾏命令
使⽤mybatis-generator⽣成Mybatis代码。能够⽣成vo 类、能⽣成mapper 映射⽂件（其中包括基本的
增删改查功能）、能⽣成mapper 接⼝。
命令：mybatis-generator:generate -e
注意⼀点，默认会先尝试使⽤Integer，Long，Short等来对应DECIMAL和NUMERIC数据类
型；
true：使⽤BigDecimal对应DECIMAL和NUMERIC数据类型
false：默认，把JDBC DECIMAL和NUMERIC类型解析为Integer
-->
<javaTypeResolver>
<property name="forceBigDecimals" value="false"/>
</javaTypeResolver>
<!-- ⽣成Model类存放位置-->
<javaModelGenerator targetPackage="com.xxxx.crm.vo"
targetProject="src/main/java">
<!-- 在targetPackage的基础上，根据数据库的schema再⽣成⼀层package，⽣成的类放在这个
package下，默认为false -->
<property name="enableSubPackages" value="true"/>
<!-- 设置是否在getter⽅法中，对String类型字段调⽤trim()⽅法-->
<property name="trimStrings" value="true"/>
</javaModelGenerator>
<!--⽣成映射⽂件存放位置-->
<sqlMapGenerator targetPackage="mappers" targetProject="src/main/resources">
<property name="enableSubPackages" value="true"/>
</sqlMapGenerator>
<!--⽣成Dao类存放位置-->
<javaClientGenerator type="XMLMAPPER" targetPackage="com.xxxx.crm.dao"
targetProject="src/main/java">
<property name="enableSubPackages" value="true"/>
</javaClientGenerator>
<!-- 数据库的表名与对应的实体类的名称，tableName是数据库中的表名，domainObjectName是⽣成
的JAVA模型名-->
<table tableName="t_user" domainObjectName="User"
enableCountByExample="false" enableUpdateByExample="false"
enableDeleteByExample="false" enableSelectByExample="false"
selectByExampleQueryId="false">
</table>
</context>
</generatorConfiguration>
6.2. 核⼼思路分析
6.3. 核⼼代码实现
6.3.1. UserModel
定义UserModel 实体类，⽤来返回登录成功后的⽤户信息
/**
* ⽤户登录
* 1. 验证参数
* 姓名⾮空判断
* 密码⾮空判断
* 2. 根据⽤户名，查询⽤户对象
* 3. 判断⽤户是否存在
* ⽤户对象为空，记录不存在，⽅法结束
* 4. ⽤户对象不为空
* ⽤户存在，校验密码
* 密码不正确，⽅法结束
* 5. 密码正确
* ⽤户登录成功，返回⽤户的相关信息（定义UserModel类，返回⽤户某些信息）
*/
package com.xxxx.crm.model;
public class UserModel {
private Integer userId;
6.3.2. UserService
⽤户登录具体的业务逻辑的实现
private String userName;
private String trueName;
public Integer getUserId() {
return userId;
}
public void setUserId(Integer userId) {
this.userId = userId;
}
public String getUserName() {
return userName;
}
public void setUserName(String userName) {
this.userName = userName;
}
public String getTrueName() {
return trueName;
}
public void setTrueName(String trueName) {
this.trueName = trueName;
}
}
package com.xxxx.crm.service;
import com.xxxx.crm.base.BaseService;
import com.xxxx.crm.dao.UserMapper;
import com.xxxx.crm.model.UserModel;
import com.xxxx.crm.utils.AssertUtil;
import com.xxxx.crm.utils.Md5Util;
import com.xxxx.crm.vo.User;
import org.apache.commons.lang3.StringUtils;
import org.springframework.stereotype.Service;
import javax.annotation.Resource;
@Service
public class UserService extends BaseService<User, Integer> {
@Resource
private UserMapper userMapper;
/**
* ⽤户登录
* @param userName
* @param userPwd
* @return
*/
public UserModel userLogin(String userName, String userPwd) {
// 1. 验证参数
checkLoginParams(userName, userPwd);
// 2. 根据⽤户名，查询⽤户对象
User user = userMapper.queryUserByUserName(userName);
// 3. 判断⽤户是否存在(⽤户对象为空，记录不存在，⽅法结束)
AssertUtil.isTrue(null == user, "⽤户不存在或已注销！");
// 4. ⽤户对象不为空（⽤户存在，校验密码。密码不正确，⽅法结束）
checkLoginPwd(userPwd, user.getUserPwd());
// 5. 密码正确（⽤户登录成功，返回⽤户的相关信息）
return buildUserInfo(user);
}
/**
* 构建返回的⽤户信息
* @param user
* @return
*/
private UserModel buildUserInfo(User user) {
UserModel userModel = new UserModel();
// 设置⽤户信息
userModel.setUserId(user.getId());
userModel.setUserName(user.getUserName());
userModel.setTrueName(user.getTrueName());
return userModel;
}
/**
* 验证登录密码
* @param userPwd 前台传递的密码
* @param upwd 数据库中查询到的密码
* @return
*/
private void checkLoginPwd(String userPwd, String upwd) {
// 数据库中的密码是经过加密的，将前台传递的密码先加密，再与数据库中的密码作⽐较
userPwd = Md5Util.encode(userPwd);
// ⽐较密码
AssertUtil.isTrue(!userPwd.equals(upwd), "⽤户密码不正确！");
}
/**
* 验证⽤户登录参数
* @param userName
* @param userPwd
*/
private void checkLoginParams(String userName, String userPwd) {
6.3.3. UserMapper
在UserMapper 接⼝类中定义对应的查询⽅法
6.3.4. UserMapper.xml
配置查询对应的SQL 语句
6.3.5. UserController
控制层定义接⼝，对接前台。Controller 层调⽤Service 层userLogin ⽅法，捕获service ⽅法的异常，获
取登录结果，并将ResultInfo 对象通过JSON 格式响应给客户端。
// 判断姓名
AssertUtil.isTrue(StringUtils.isBlank(userName), "⽤户姓名不能为空！");
// 判断密码
AssertUtil.isTrue(StringUtils.isBlank(userPwd), "⽤户密码不能为空！");
}
}
package com.xxxx.crm.dao;
import com.xxxx.crm.base.BaseMapper;
import com.xxxx.crm.vo.User;
public interface UserMapper extends BaseMapper<User,Integer> {
// 根据⽤户名查询⽤户对象
User queryUserByUserName(String userName);
}
<!-- 根据⽤户名查询⽤户对象-->
<select id="queryUserByUserName" parameterType="string"
resultType="com.xxxx.crm.vo.User">
select
<include refid="Base_Column_List" />
from
t_user
where
user_name = #{userName}
</select>
package com.xxxx.crm.controller;
import com.xxxx.crm.base.BaseController;
import com.xxxx.crm.base.ResultInfo;
import com.xxxx.crm.exceptions.ParamsException;
import com.xxxx.crm.model.UserModel;
import com.xxxx.crm.service.UserService;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.ResponseBody;
import javax.annotation.Resource;
@Controller
public class UserController extends BaseController {
@Resource
private UserService userService;
/**
* ⽤户登录
* @param userName
* @param userPwd
* @return
*/
@PostMapping("user/login")
@ResponseBody
public ResultInfo userLogin (String userName, String userPwd) {
ResultInfo resultInfo = new ResultInfo();
// 通过try catch 捕获Service 层抛出的异常
try {
// 调⽤Service层的登录⽅法，得到返回的⽤户对象
UserModel userModel = userService.userLogin(userName, userPwd);
/**
* 登录成功后，有两种处理：
* 1. 将⽤户的登录信息存⼊Session （问题：重启服务器，Session 失效，客户端需要重
复登录）
* 2. 将⽤户信息返回给客户端，由客户端（Cookie）保存
*/
// 将返回的UserModel对象设置到ResultInfo 对象中
resultInfo.setResult(userModel);
} catch (ParamsException e) { // ⾃定义异常
e.printStackTrace();
// 设置状态码和提示信息
resultInfo.setCode(e.getCode());
resultInfo.setMsg(e.getMsg());
} catch (Exception e) {
e.printStackTrace();
resultInfo.setCode(500);
resultInfo.setMsg("操作失败！");
}
return resultInfo;
}
}
6.3.6. Starter
修改启动类，在启动类上添加@MapperScan 注解，设置扫描包范围。
6.3.7. PostMan 测试
利⽤Postman ⼯具，对⽤户登录的接⼝进⾏测试。
6.3.8. 前端登录功能实现
index.ftl 添加对应index.js，使⽤layui 表单组件实现表单提交操作。登录成功后，如果
参考API：https://www.layui.com/doc/modules/form.html#onsubmit
package com.xxxx.crm;
import org.mybatis.spring.annotation.MapperScan;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
@SpringBootApplication
@MapperScan("com.xxxx.crm.dao")
public class Starter {
public static void main(String[] args) {
SpringApplication.run(Starter.class);
}
}
layui.use(['form','jquery','jquery_cookie'], function () {
var form = layui.form,
layer = layui.layer,
$ = layui.jquery,
$ = layui.jquery_cookie($);
/**
* ⽤户登录表单提交
*/
form.on("submit(login)", function(data){
// 获取表单元素的值（⽤户名+ 密码）
var fieldData = data.field;
// 判断参数是否为空
if (fieldData.username == "undefined" || fieldData.username.trim() == "") {
layer.msg("⽤户名称不能为空！");
return false;
}
if (fieldData.password == "undefined" || fieldData.password.trim() == "") {
layer.msg("⽤户密码不能为空！");
return false;
}
// 发送ajax 请求，请求⽤户登录
$.ajax({
type:"post",
url:ctx + "/user/login",
data:{
userName:fieldData.username,
userPwd:fieldData.password
},
dataType:"json",
success:function(data){
// 判断是否登录成功
if (data.code == 200) {
layer.msg("登录成功！", function () {
// 将⽤户信息存到cookie中
var result = data.result;
$.cookie("userId", result.userId);
$.cookie("userName", result.userName);
$.cookie("trueName", result.trueName);
// 登录成功后，跳转到⾸⻚
window.location.href = ctx + "/main";
});
} else {
// 提示信息
layer.msg(data.msg);
}
}
});
// 阻⽌表单跳转
6.3.9. 修改Cookie 的数据
将Cookie 中的userId 的值加密存储。未加密前效果如下：
修改UserModel 中的属性字段，将Integer 类型的userId 属性改为String 类型的userIdStr
修改UserService 中对应的⽅法，将userId 的值加密
修改index.js 中存储cookie 的值
加密后效果如下：
return false;
});
});
public class UserModel {
private String userIdStr;
private String userName;
private String trueName;
/* 省略get 和set ⽅法*/
}
/**
* 构建返回的⽤户信息
* @param user
* @return
*/
private UserModel buildUserInfo(User user) {
UserModel userModel = new UserModel();
// 设置⽤户信息（将userId 加密）
userModel.setUserIdStr(UserIDBase64.encoderUserID(user.getId()));
userModel.setUserName(user.getUserName());
userModel.setTrueName(user.getTrueName());
return userModel;
}
$.cookie("userIdStr", result.userIdStr);
6.3.10. 主⻚⾯显示⽤户名信息
在IndexController控制器中，main ⽅法转发时，查询登录⽤户信息并放置到request 域。
在main.ftl 中获取作⽤域中的user 对象，显示登录⽤户信息
6.3.11. 启动程序测试登录效果
使⽤测试账号执⾏登录操作。（⽤户名：admin ，密码：123）
7. 密码修改功能实现
7.1. 核⼼思路分析
/**
* 后端管理主⻚⾯
* @return
*/
@RequestMapping("main")
public String main(HttpServletRequest request) {
// 通过⼯具类，从cookie中获取userId
Integer userId = LoginUserUtil.releaseUserIdFromCookie(request);
// 调⽤对应Service层的⽅法，通过userId主键查询⽤户对象
User user = userService.selectByPrimaryKey(userId);
// 将⽤户对象设置到request作⽤域中
request.setAttribute("user", user);
return "main";
}
7.2. UserService
updateUserPassword ⽅法实现
/**
* ⽤户密码修改
* 1. 参数校验
* userId ⾮空⽤户对象必须存在
* oldPassword ⾮空与数据库中密⽂密码保持⼀致
* newPassword ⾮空与原始密码不能相同
* confirmPassword ⾮空与新密码保持⼀致
* 2. 设置⽤户新密码
* 新密码进⾏加密处理
* 3. 执⾏更新操作
* 受影响的⾏数⼩于1，则表示修改失败
*/
/**
* ⽤户密码修改
* 1. 参数校验
* ⽤户ID：userId ⾮空⽤户对象必须存在
* 原始密码：oldPassword ⾮空与数据库中密⽂密码保持⼀致
* 新密码：newPassword ⾮空与原始密码不能相同
* 确认密码：confirmPassword ⾮空与新密码保持⼀致
* 2. 设置⽤户新密码
* 新密码进⾏加密处理
* 3. 执⾏更新操作
* 受影响的⾏数⼩于1，则表示修改失败
*
* 注：在对应的更新⽅法上，添加事务控制
*/
@Transactional(propagation = Propagation.REQUIRED)
public void updateUserPassword (Integer userId, String oldPassword,
String newPassword, String confirmPassword ) {
// 通过userId获取⽤户对象
User user = userMapper.selectByPrimaryKey(userId);
// 1. 参数校验
checkPasswordParams(user, oldPassword, newPassword, confirmPassword);
// 2. 设置⽤户新密码
user.setUserPwd(Md5Util.encode(newPassword));
// 3. 执⾏更新操作
AssertUtil.isTrue(userMapper.updateByPrimaryKeySelective(user) < 1, "⽤户密码更新失
败！");
}
/**
* 验证⽤户密码修改参数
* ⽤户ID：userId ⾮空⽤户对象必须存在
* 原始密码：oldPassword ⾮空与数据库中密⽂密码保持⼀致
* 新密码：newPassword ⾮空与原始密码不能相同
* 确认密码：confirmPassword ⾮空与新密码保持⼀致
7.3. UserController
updateUserPassword ⽅法实现
* @param user
* @param oldPassword
* @param newPassword
* @param confirmPassword
*/
private void checkPasswordParams(User user, String oldPassword,
String newPassword, String confirmPassword) {
// user对象⾮空验证
AssertUtil.isTrue(null == user, "⽤户未登录或不存在！");
// 原始密码⾮空验证
AssertUtil.isTrue(StringUtils.isBlank(oldPassword), "请输⼊原始密码！");
// 原始密码要与数据库中的密⽂密码保持⼀致
AssertUtil.isTrue(!(user.getUserPwd().equals(Md5Util.encode(oldPassword))), "原始密
码不正确！");
// 新密码⾮空校验
AssertUtil.isTrue(StringUtils.isBlank(newPassword), "请输⼊新密码！");
// 新密码与原始密码不能相同
AssertUtil.isTrue(oldPassword.equals(newPassword), "新密码不能与原始密码相同！");
// 确认密码⾮空校验
AssertUtil.isTrue(StringUtils.isBlank(confirmPassword), "请输⼊确认密码！");
// 新密码要与确认密码保持⼀致
AssertUtil.isTrue(!(newPassword.equals(confirmPassword)), "新密码与确认密码不⼀致！");
}
/**
* ⽤户密码修改
* @param request
* @param oldPassword
* @param newPassword
* @param confirmPassword
* @return
*/
@PostMapping("user/updatePassword")
@ResponseBody
public ResultInfo updateUserPassword (HttpServletRequest request,
String oldPassword, String newPassword, String
confirmPassword) {
ResultInfo resultInfo = new ResultInfo();
// 通过try catch 捕获Service 层抛出的异常
try {
// 获取userId
Integer userId = LoginUserUtil.releaseUserIdFromCookie(request);
// 调⽤Service层的密码修改⽅法
userService.updateUserPassword(userId, oldPassword, newPassword,
confirmPassword);
} catch (ParamsException e) { // ⾃定义异常
7.4. PostMan 测试
7.4.1. 在Postman 中添加Cookie
点击右侧"Cookies "，打开Cookie 管理窗⼝
e.printStackTrace();
// 设置状态码和提示信息
resultInfo.setCode(e.getCode());
resultInfo.setMsg(e.getMsg());
} catch (Exception e) {
e.printStackTrace();
resultInfo.setCode(500);
resultInfo.setMsg("操作失败！");
}
return resultInfo;
}
输⼊域名，点击"Add"
点击"Add Cookie"，添加对应的Cookie
修改Cookie 对应的名称和值，以及路径，点击"Save" 保存
关闭Cookie 窗⼝，重新发送请求测试
7.5. 前端核⼼代码
7.5.1. 添加视图⻚⾯
在src/main/resources ⽬录的views ⽬录下，新建user ⽬录，将password.ftl ⽂件拷⻉进去
7.5.2. 添加⻚⾯转发
在layuimini 布局⻚⾯，通过点击"修改密码" ，请求后端的user/toPasswordPage 接⼝
在UserController 控制层，添加对应的视图转发⽅法
进⼊⽤户密码修改⻚⾯
7.5.3. 前端核⼼JS
准备密码修改⻚对应JS ⽂件。添加表单提交代码，使⽤ajax 对接后端密码修改接⼝实现密码修改操
作，当密码修改后清除客户端cookie 信息并跳转⾄登录⻚⾯。
在src/main/resources/public/ js ⽬录中，新建user ⽬录，添加password.js ⽂件
@RequestMapping("user/toPasswordPage")
public String toPasswordPage(){
return "user/password";
}
layui.use(['form','jquery','jquery_cookie'], function () {
var form = layui.form,
layer = layui.layer,
$ = layui.jquery,
$ = layui.jquery_cookie($);
/**
* ⽤户密码修改表单提交
*/
form.on("submit(saveBtn)", function(data) {
// 获取表单元素的内容
var fieldData = data.field;
// 发送ajax请求，修改⽤户密码
7.5.4. 测试操作
原始密码：123，修改后密码：123456，点击保存按钮
$.ajax({
type:"post",
url:ctx + "/user/updatePassword",
data:{
oldPassword:fieldData.old_password,
newPassword:fieldData.new_password,
confirmPassword:fieldData.again_password
},
dataType:"json",
success:function (data) {
// 判断是否成功
if (data.code == 200) {
// 修改成功后，⽤户⾃动退出系统
layer.msg("⽤户密码修改成功，系统将在3秒钟后退出...", function () {
// 退出系统后，删除对应的cookie
$.removeCookie("userIdStr", {domain:"localhost",path:"/crm"});
$.removeCookie("userName", {domain:"localhost",path:"/crm"});
$.removeCookie("trueName", {domain:"localhost",path:"/crm"});
// 跳转到登录⻚⾯(⽗窗⼝跳转)
window.parent.location.href = ctx + "/index";
});
} else {
layer.msg(data.msg);
}
}
});
});
});
8. ⽤户退出功能实现
8.1. 退出登录
找到"退出登录" 的元素，并绑定点击事件。当⽤户点击退出时，清空cookie信息
在main.js 中，通过类选择器绑定元素的点击事件
/**
* ⽤户退出
* 删除cookie
*/
$(".login-out").click(function () {
// 删除cookie
$.removeCookie("userIdStr", {domain:"localhost",path:"/crm"});
$.removeCookie("userName", {domain:"localhost",path:"/crm"});
$.removeCookie("trueName", {domain:"localhost",path:"/crm"});
// 跳转到登录⻚⾯(⽗窗⼝跳转)
window.parent.location.href = ctx + "/index";
});
9. 全局异常统⼀处理
9.1. 全局异常实现思路
9.2. 全局异常拦截器实现
实现HandlerExceptionResolver 接⼝，处理应⽤程序异常信息
控制层的⽅法返回的内容两种情况
1. 视图:视图异常
2. Json:⽅法执⾏错误返回错误json信息
package com.xxxx.crm;
import com.alibaba.fastjson.JSON;
import com.xxxx.crm.base.ResultInfo;
import com.xxxx.crm.exceptions.ParamsException;
import org.springframework.stereotype.Component;
import org.springframework.web.bind.annotation.ResponseBody;
import org.springframework.web.method.HandlerMethod;
import org.springframework.web.servlet.HandlerExceptionResolver;
import org.springframework.web.servlet.ModelAndView;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.PrintWriter;
/**
* 全局异常统⼀处理
*/
@Component
public class GlobalExceptionResolver implements HandlerExceptionResolver {
/**
* ⽅法返回值类型
* 视图
* JSON
* 如何判断⽅法的返回类型：
* 如果⽅法级别配置了@ResponseBody 注解，表示⽅法返回的是JSON；
* 反之，返回的是视图⻚⾯
* @param request
* @param response
* @param handler
* @param ex
* @return
*/
@Override
public ModelAndView resolveException(HttpServletRequest request,
HttpServletResponse response,
Object handler, Exception ex) {
// 设置默认异常处理
ModelAndView mv = new ModelAndView();
mv.setViewName("");
mv.addObject("code", 400);
mv.addObject("msg", "系统异常，请稍后再试...");
// 判断HandlerMethod
if (handler instanceof HandlerMethod) {
// 类型转换
HandlerMethod handlerMethod = (HandlerMethod) handler;
// 获取⽅法上的ResponseBody 注解
ResponseBody responseBody =
handlerMethod.getMethod().getDeclaredAnnotation(ResponseBody.class);
// 判断ResponseBody 注解是否存在(如果不存在，表示返回的是视图;如果存在，表示返回的
是JSON)
if (null == responseBody) {
/**
* ⽅法返回视图
*/
if (ex instanceof ParamsException) {
ParamsException pe = (ParamsException) ex;
mv.addObject("code", pe.getCode());
mv.addObject("msg", pe.getMsg());
}
return mv;
} else {
/**
* ⽅法上返回JSON
*/
ResultInfo resultInfo = new ResultInfo();
resultInfo.setCode(300);
resultInfo.setMsg("系统异常，请重试！");
// 如果捕获的是⾃定义异常
if (ex instanceof ParamsException) {
ParamsException pe = (ParamsException) ex;
resultInfo.setCode(pe.getCode());
resultInfo.setMsg(pe.getMsg());
}
// 设置响应类型和编码格式（响应JSON格式）
response.setContentType("application/json;charset=utf-8");
// 得到输出流
PrintWriter out = null;
try {
out = response.getWriter();
// 将对象转换成JSON格式，通过输出流输出
out.write(JSON.toJSONString(resultInfo));
out.flush();
} catch (Exception e) {
9.3. 消除try-catch 代码
系统引⼊全局异常，简化控制层try-catch 代码
e.printStackTrace();
} finally {
if (out != null) {
out.close();
}
}
return null;
}
}
return mv;
}
}
/**
* ⽤户登录
* @param userName
* @param userPwd
* @return
*/
@PostMapping("user/login")
@ResponseBody
public ResultInfo userLogin (String userName, String userPwd) {
ResultInfo resultInfo = new ResultInfo();
// 调⽤Service层的登录⽅法，得到返回的⽤户对象
UserModel userModel = userService.userLogin(userName, userPwd);
// 将返回的UserModel对象设置到ResultInfo 对象中
resultInfo.setResult(userModel);
return resultInfo;
}
/**
* ⽤户密码修改
* @param request
* @param oldPassword
* @param newPassword
* @param confirmPassword
* @return
*/
@PostMapping("user/updatePassword")
@ResponseBody
public ResultInfo updateUserPassword (HttpServletRequest request,
String oldPassword, String newPassword, String
confirmPassword) {
ResultInfo resultInfo = new ResultInfo();
10. ⾮法请求拦截
对于后端菜单资源，这⾥要求⽤户必须进⾏登录来保护web 资源的安全性，此时引⼊⾮法请求拦截功
能。
10.1. 实现思路
10.2. 定义拦截器
在新建interceptors 包，创建NoLoginInterceptor 类，并继承HandlerInterceptorAdapter 适配器，实现拦
截器功能。
// 获取userId
Integer userId = LoginUserUtil.releaseUserIdFromCookie(request);
// 调⽤Service层的密码修改⽅法
userService.updateUserPassword(userId, oldPassword, newPassword, confirmPassword);
return resultInfo;
}
/**
* 判断⽤户是否是登录状态
* 获取Cookie对象，解析⽤户ID的值
* 如果⽤户ID不为空，且在数据库中存在对应的⽤户记录，表示请求合法
* 否则，请求不合法，进⾏拦截，重定向到登录⻚⾯
*/
package com.xxxx.crm.interceptors;
import com.xxxx.crm.exceptions.NoLoginException;
import com.xxxx.crm.service.UserService;
import com.xxxx.crm.utils.LoginUserUtil;
import org.springframework.web.servlet.handler.HandlerInterceptorAdapter;
import javax.annotation.Resource;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
/**
* ⾮法访问拦截
*/
public class NoLoginInterceptor extends HandlerInterceptorAdapter {
@Resource
private UserService userService;
/**
10.3. 全局异常类配置
在全局异常处理类中引⼊未登录异常判断
* 判断⽤户是否是登录状态
* 获取Cookie对象，解析⽤户ID的值
* 如果⽤户ID不为空，且在数据库中存在对应的⽤户记录，表示请求合法
* 否则，请求不合法，进⾏拦截，重定向到登录⻚⾯
* @param request
* @param response
* @param handler
* @return
* @throws Exception
*/
@Override
public boolean preHandle(HttpServletRequest request, HttpServletResponse response,
Object handler) throws Exception {
// 获取Cookie中的⽤户ID
Integer userId = LoginUserUtil.releaseUserIdFromCookie(request);
// 判断⽤户ID是否不为空，且数据库中存在对应的⽤户记录
if (null == userId || null == userService.selectByPrimaryKey(userId)) {
// 抛出未登录异常
throw new NoLoginException();
}
return true;
}
}
/**
* 全局异常统⼀处理
*/
@Component
public class GlobalExceptionResolver implements HandlerExceptionResolver {
@Override
public ModelAndView resolveException(HttpServletRequest request,
HttpServletResponse response,
Object handler, Exception ex) {
/**
* 判断异常类型
* 如果是未登录异常，则先执⾏相关的拦截操作
*/
if (ex instanceof NoLoginException) {
// 如果捕获的是未登录异常，则重定向到登录⻚⾯
ModelAndView mv = new ModelAndView("redirect:/index");
return mv;
}
// 设置默认异常处理
ModelAndView mv = new ModelAndView();
10.4. 拦截器⽣效配置
新建config 包，添加拦截器⽣效的配置类
10.5. 拦截测试
10.6. 测试拦截效果
当Cookie 中的⽤户ID不存在时，访问main ⻚⾯，会⾃动跳转到登录⻚⾯
/* 后续代码省略*/
return mv;
}
}
package com.xxxx.crm.config;
import com.xxxx.crm.interceptors.NoLoginInterceptor;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.config.annotation.InterceptorRegistry;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurerAdapter;
@Configuration
public class MvcConfig extends WebMvcConfigurerAdapter {
@Bean
public NoLoginInterceptor noLoginInterceptor() {
return new NoLoginInterceptor();
}
/**
* 添加拦截器
* @param registry
*/
@Override
public void addInterceptors(InterceptorRegistry registry) {
// 需要⼀个实现HandlerInterceptor接⼝的拦截器实例，这⾥使⽤的是NoLoginInterceptor
registry.addInterceptor(noLoginInterceptor())
// ⽤于设置拦截器的过滤路径规则
.addPathPatterns("/**")
// ⽤于设置不需要拦截的过滤规则
.excludePathPatterns("/index","/user/login","/css/**","/images/**","/js/**","/lib/**")
;
}
}
11. 记住我功能实现
记住我功能核⼼在于当⽤户上次登录时如果点击了记住我，下次在重新打开浏览器时可以不⽤选择登
录，此时可以借助拦截器+ cookie 来实现，当⽤户在登录时，如果⽤户点击了记住我功能，默认设置
cookie存储时间为7天即可。
11.1. 修改index.ftl
在⽤户登录表单中添加记住密码的复选框
11.2. 修改index.js
如果⽤户在登录时，勾选了"记住我" 的复选框，则在登录成功之后，设置cookie 的有效期
<#-- 记住我-->
<div class="layui-form-item">
<input type="checkbox" name="rememberMe" id="rememberMe" value="true" layskin="
primary" title="记住密码">
</div>
layui.use(['form','jquery','jquery_cookie'], function () {
var form = layui.form,
layer = layui.layer,
$ = layui.jquery,
$ = layui.jquery_cookie($);
/**
* ⽤户登录表单提交
*/
form.on("submit(login)", function(data){
// 获取表单元素的值（⽤户名+ 密码）
var fieldData = data.field;
// 判断参数是否为空
if (fieldData.username == "undefined" || fieldData.username.trim() == "") {
layer.msg("⽤户名称不能为空！");
return false;
}
if (fieldData.password == "undefined" || fieldData.password.trim() == "") {
layer.msg("⽤户密码不能为空！");
return false;
}
// 发送ajax 请求，请求⽤户登录
$.ajax({
type:"post",
url:ctx + "/user/login",
data:{
userName:fieldData.username,
userPwd:fieldData.password
},
dataType:"json",
success:function(data){
// 判断是否登录成功
if (data.code == 200) {
layer.msg("登录成功！", function () {
// 将⽤户信息存到cookie中
var result = data.result;
$.cookie("userIdStr", result.userIdStr);
$.cookie("userName", result.userName);
$.cookie("trueName", result.trueName);
// 如果⽤户选择"记住我"，则设置cookie的有效期为7天
if($("input[type='checkbox']").is(":checked")){
$.cookie("userIdStr", result.userIdStr, { expires: 7 });
$.cookie("userName", result.userName, { expires: 7 });
$.cookie("trueName", result.trueName, { expires: 7 });
}
// 登录成功后，跳转到⾸⻚
window.location.href = ctx + "/main";
});
} else {
// 提示信息
layer.msg(data.msg);
}
}
});
// 阻⽌表单跳转
return false;
});
});