# day25_ 

# 1.Log4J日志

## 1.1简介

## 1.2日志级别

​		分为五个级别：
​		DEBUG(人为调试信息)、INFO(普通信息)、WARN(警告)、ERROR(错误)和FATAL(系统错误)

​		Log4j有一个规则：只输出级别不低于设定级别的日志信息，假设Loggers级别设定为INFO，则INFO、WARN、ERROR和FATAL级别的日志信息都会输出，而级别比INFO低的DEBUG则不会输出。

## 1.3配置文件

```properties
# Set root category priority to INFO and its only appender to CONSOLE. 
# log4j.rootCategory=DEBUG, CONSOLE 
log4j.rootCategory=INFO, CONSOLE, LOGFILE

# 单独设置SQL语句的输出级别为DEBUG级别
# 方法级别
# log4j.logger.com.wse.mappers.EmpMapper.queryAll=DEBUG
# 类级别
# log4j.logger.com.wse.mappers.EmpMapper=DEBUG
# 包级别
log4j.logger.com.wse.mappers=DEBUG

# CONSOLE is set to be a ConsoleAppender using a PatternLayout. 
log4j.appender.CONSOLE=org.apache.log4j.ConsoleAppender 
log4j.appender.CONSOLE.layout=org.apache.log4j.PatternLayout 
log4j.appender.CONSOLE.layout.ConversionPattern=- %m %n

# LOGFILE is set to be a File appender using a PatternLayout. 
log4j.appender.LOGFILE=org.apache.log4j.FileAppender 
log4j.appender.LOGFILE.File=G:/java/shsxt/test.log
log4j.appender.LOGFILE.Append=false 
log4j.appender.LOGFILE.layout=org.apache.log4j.PatternLayout 
log4j.appender.LOGFILE.layout.ConversionPattern=- %m %n
```

## 1.3开启日志并调整日志级别

​		通过settings标签开启 log4j 的支持
​		settings用于设置 MyBatis 在运行时的行为方式, 例如:缓存, 延迟加载, 日志等.

```xml
<!-- settings标签 -->
<settings>
<!-- 设置MyBatis使用log4j日志支持 -->
<setting name="logImpl" value="LOG4J"/>
</settings>
```

## 1.4properties标签实现软编码

​		mybatis核心配置文件中添加properties标签,指定加载外部的properties文件,
注意定义位置

```xml
<!-- 加载外部的properties文件 -->
<properties resource="jdbc.properties" />
```

```xml
<environments default="development">
    <environment id="development">
        <transactionManager type="JDBC"/>
        <dataSource type="POOLED">
            <property name="driver" value="${driver}"/>
            <property name="url" value="${url}"/>
            <property name="username" value="${user}"/>
            <property name="password" value="${pwd}"/>
        </dataSource>
    </environment>
</environments>
```

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <!-- 加载外部的properties文件 -->
    <properties resource="jdbc.properties" />
    <!-- settings标签 -->
    <settings>
        <!-- 设置MyBatis使用log4j日志支持 -->
        <setting name="logImpl" value="LOG4J"/>
    </settings>
    <!-- 定义别名 -->
    <typeAliases>
        <!-- 为指定的一个 类型定义别名 -->
        <!-- <typeAlias type="com.xxxx.pojo.Emp" alias="e"/>
        <typeAlias type="com.xxxx.pojo.Dept" /> -->  <!-- alias 属性省略,默认类名为别名,不区分大小写 -->
        <!-- 为整个包下所有的类型定义别名,别名默认为 类名,不区分大小写 -->
        <package name="com.wse.pojo"/>
    </typeAliases>
    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="${driver}"/>
                <property name="url" value="${url}"/>
                <property name="username" value="${user}"/>
                <property name="password" value="${pwd}"/>
            </dataSource>
        </environment>
    </environments>
    <mappers>
<!--        <mapper resource="com/wse/mappers/EmpMapper.xml"/>-->
        <mapper resource="com/wse/mappers/DeptMapper.xml"/>  <!-- xml文件,指明路径要使用/ -->
<!--        <mapper resource="com/wse/mappers/EmpMapper1.xml"/>  &lt;!&ndash; xml文件,指明路径要使用/ &ndash;&gt;-->
    </mappers>
</configuration>
```

## 1.5通过package标签给整个包下的所有类定义别名,别名为类名

```xml
<typeAliases>
    <!-- 为指定的一个 类型定义别名 -->
    <!-- <typeAlias type="com.xxxx.pojo.Emp" alias="e"/>
    <typeAlias type="com.xxxx.pojo.Dept" /> -->  <!-- alias 属性省略,默认类名为别名,不区分大小写 -->
    <!-- 为整个包下所有的类型定义别名,别名默认为 类名,不区分大小写 -->
    <package name="com.wse.pojo"/>
</typeAliases>
```

## 1.6parameterType入参类型

### 1.6.1一个参数的查询

### 1.6.2多个参数查询

```java
package com.wse.test;

import com.wse.pojo.Emp;
import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;

import java.io.IOException;
import java.io.InputStream;
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.*;

/** 测试参数类型
 * @author wse
 * @version 1.0
 * @date 2020/7/24 0024 19:01
 */
public class EmpDemo02 {
    public static void main(String[] args) throws IOException, ParseException {
        //1.加载mybatis全局核心配置文件
        InputStream is = Resources.getResourceAsStream("mybatis1.xml");
        //2.构建SqlSessionFactory对象
        SqlSessionFactory factory = new SqlSessionFactoryBuilder().build(is);
        //3.通过工厂获取会话
        SqlSession session = factory.openSession();
        //4.通过session调用方法执行查询
        //selectList() 查到的数据返回一个list集合,没查到返回空的list
        //selectList 的第一个参数为statement: 命名空间+id
//        List<Emp> list = session.selectList("com.wse.mappers.EmpMapper.queryAll");
//        list.forEach(System.out::println);

        //通过name查询一个人的信息selectOne
//        Emp emp = session.selectOne("com.wse.mappers.EmpMapper.queryByName");
//        System.out.println(emp);

        //将查询结果放入Map
//        Map<Integer, Emp> map = session.selectMap("com.wse.mappers.EmpMapper.queryByDeptno", "deptno");
//        Set<Integer> deptno = map.keySet();
//        for (Integer i : deptno) {
//            System.out.println(i + "-->" + map.get(i));
//        }
        //只输入一条数据，因为map集合中key值不可重复，同一部门只能查出一人

        //基本数据类型|包装类 String Date JavaBean Map  List 数组
        Emp emp = session.selectOne("com.wse.mappers.EmpMapper.queryById", 7369);
        System.out.println(emp);

        //String
        List<Emp> list1 = session.selectList("com.wse.mappers.EmpMapper.queryByName", "KING");
        list1.forEach(System.out::println);

        //Date  1981/12/3
        Date date = new SimpleDateFormat("yyyy/MM/dd").parse("1981/12/3");
        List<Emp> list2 = session.selectList("com.wse.mappers.EmpMapper.queryByDate", date);
        list2.forEach(System.out::println);

        //JavaBean
        Emp emp1 = new Emp();
        emp1.setEname("SMITH");
        emp1.setSal(800.00);
        List<Emp> list3 = session.selectList("com.wse.mappers.EmpMapper.queryByEmp",emp1);
        list3.forEach(System.out::println);

        //Map  多个参数封装成为map集合,sql中根据key获取对象的value
        Map map = new HashMap();
        map.put("deptno",30);
        map.put("sal",1250.00);
        List<Emp> list4 = session.selectList("com.wse.mappers.EmpMapper.queryByMap",map);
        list4.forEach(System.out::println);

        List list = Arrays.asList(7369,7521,7900);
        List<Emp> list5 = session.selectList("com.wse.mappers.EmpMapper.queryByList",list);
        list5.forEach(System.out::println);


        //5.关闭会话资源
        session.close();
    }
}
```

## 1.7工具类的封装

```java
package com.wse.util;

import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;

import java.io.IOException;

/** 对sqlSession回话的封装
 * @author wse
 * @version 1.0
 * @date 2020/7/25 0025 12:16
 */
public class SessionUtil {
    private static SqlSessionFactory factory =null;
    static{
        try {
            factory = new SqlSessionFactoryBuilder().build(Resources.getResourceAsStream("com.wse.mybatis1.xml"));
        } catch (IOException e) {
            e.printStackTrace();
        }
    }


    public static SqlSession getSession() {
        SqlSession session = null;
        if(factory!=null) {
            //修改为自动提交事务
            session = factory.openSession(true);
        }
        return  session;
    }
}
```

## 1.8测试resultType结果类型

```java
package com.wse.test;

import com.wse.pojo.Emp;
import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;

import java.io.IOException;
import java.util.Date;
import java.util.List;
import java.util.Map;

/**
 * 测试结果类型
 * @author wse
 * @version 1.0
 * @date 2020/7/25 0025 14:43
 */
public class EmpDemo03 {
    public static void main(String[] args) throws IOException {
        SqlSession session = new SqlSessionFactoryBuilder().build(Resources.getResourceAsStream("mybatis1.xml")).openSession();
        //String    根据empno查询员工姓名
        String  name = session.selectOne("com.wse.mappers.EmpMapper1.queryNameById",7369);
        System.out.println(name);//SMITH

        //date  根据用户名查询入职日期
        Date date = session.selectOne("com.wse.mappers.EmpMapper1.queryDateByName", "SMITH");
        System.out.println(date);//Wed Dec 17 00:00:00 CST 1980

        //List  根据用户名模糊匹配包含
        List<Emp> list = session.selectList("com.wse.mappers.EmpMapper1.queryListByName", "A");
        list.forEach(System.out::println);

        //Map  -->链表查询或者没有对应java类型,无法转为对象的时候可以使用
        Map<String,Object> map = session.selectOne("com.wse.mappers.EmpMapper1.queryMapById", 7369);
        System.out.println(map);//{ENAME=SMITH, HIREDATE=1980-12-17 00:00:00.0, EMPNO=7369, MGR=7902, JOB=CLERK, DEPTNO=20, SAL=800}

        //List<Map> : list中每一个map就是记录一条数据(这个数据的所有字段名和字段值作为键值对数据存在这个map中)
        List<Map<String,Object>> list1 = session.selectList("com.wse.mappers.EmpMapper1.queryListMapById", 1250.00);
        list1.forEach(System.out::println);

        //关闭资源
        session.close();

    }
}
```

## 1.9接口绑定方案

​		Myabtis中,提供了一套接口绑定方案,程序员可以提供一个接口,然后提供一个与接口所对应的mapper.xml文件
​		Myabaits会自动讲接口与xml文件进行绑定,实际上就是Mybatis互根据接口和对应的xml文件创建一个接口的实现类,换言之,就是可以得到接口类型的一
个对象,方便方法的调用

- 定义接口

- ```java
  package com.wse.mappers;
  
  
  import com.wse.pojo.Dept;
  import org.apache.ibatis.annotations.Param;
  
  import java.util.List;
  
  /**
   * @author wse
   * @version 1.0
   * @date 2020/7/26 0026 8:36
   */
  public interface DeptMapper {
      //查询所有的员工信息并且返回List
      List<Dept> queryAll();
      //通过部门编号获取部门信息
      Dept querDeptByNo(int no);
      //通过部门编号及部门名称获取部门信息
      Dept querDeptByNoName(@Param("deptno") int deptno, @Param("dname") String dname);
      //新增一条部门数据
      int insertDept(Dept dept);
      //根据deptno修改loc
      int updateDept(@Param("deptno") int deptno, @Param("loc") String dname);
      //根据deptno删除数据
      int deleteDeptByNO(int deptno);
  }
  ```

- 映射文件

- ```xml
  <?xml version="1.0" encoding="UTF-8" ?>
  <!DOCTYPE mapper
          PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
          "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
  
  <!--
     根元素 namespace : 命名 空间
                 唯一的,不可重复,唯一标识sql映射文件
                 随意定义
                 建议: xml所在的包名.文件名
  -->
  <!--
     测试接口绑定方案的使用
     mapper文件名与对应的接口名保持一致
     namespace 与 对应的接口的权限定名保持一致
  -->
  <mapper namespace="com.wse.mappers.DeptMapper">
  
      <!-- 查询标签:
          id :  唯一 标识
          parameterType:  参数类型: javabean 基本数据类型  String List  Map  数组
          resultType: 结果类型 : javabean 基本数据类型  String List  Map  Date
              如果类型为容器,指明容器的泛型类型
              引用数据类型: 权限定名 包名.类名
      -->
  
  
      <!--    查询部门所有信息-->
      <select id="queryAll" resultType="dept">
          select * from dept
      </select>
  
      <!--    通过部门编号获取部门信息-->
      <select id="querDeptByNo" resultType="dept">
          select * from dept where deptno = #{deptno}
      </select>
  
      <!--    通过部门编号及部门名称获取部门信息-->
      <select id="querDeptByNoName" resultType="dept">
          select * from dept where deptno = #{deptno} and dname = #{dname}
      </select>
  
      <!--    新增一条用户数据-->
      <insert id="insertDept" parameterType="dept">
          insert into Dept values(seq_user_id.nextval,#{dname},#{loc})
      </insert>
      <!--    修改数据  根据deptno修改loc-->
      <update id="updateDept" >
          update Dept set loc = #{loc} where deptno = #{deptno}
      </update>
      <!--    根据deptno删除数据-->
      <delete id="deleteDeptByNO" parameterType="int">
          delete from dept where deptno = #{deptno}
      </delete>
  </mapper>
  ```

- 测试类

- ```java
  package com.wse.test;
  
  import com.wse.mappers.DeptMapper;
  import com.wse.pojo.Dept;
  import com.wse.util.SessionUtil;
  import org.apache.ibatis.session.SqlSession;
  
  import java.util.List;
  
  /**
   * @author wse
   * @version 1.0
   * @date 2020/7/26 0026 8:34
   */
  public class DeptDemo {
      public static void main(String[] args) {
          //工具类使用
          SqlSession session = SessionUtil.getSession();
          //获取接口实现类对象
          DeptMapper mapper = session.getMapper(DeptMapper.class);
          //调用方法，查询所有部门信息
          List<Dept> depts = mapper.queryAll();
          depts.forEach(System.out::println);
  
          //通过部门编号获取部门信息
          Dept dept = mapper.querDeptByNo(30);
          System.out.println(dept);//Dept{deptno=30, dname='SALES', loc='CHICAGO'}
  
          //通过部门编号及部门名称获取部门信息
          Dept dept1 = mapper.querDeptByNoName(30, "SALES");
          System.out.println(dept1);//Dept{deptno=30, dname='SALES', loc='CHICAGO'}
  
          //新增一条部门数据
          Dept dept2 = new Dept();
          dept2.setDname("销售部");
          dept2.setLoc("北京");
          int rows = mapper.insertDept(dept2);
          System.out.println(rows > 0 ? "插入成功" : "插入失败");
  
          //根据deptno修改loc
          int rows1 = mapper.updateDept(21, "上海");
          System.out.println(rows1 > 0 ? "修改成功" : "修改失败");
  
          int rows2 = mapper.deleteDeptByNO(22);
          System.out.println(rows2 > 0 ? "删除成功" : "删除失败");
  
  
      }
  }
  ```

注意点：

1. xml文件名要与接口名保持一致

2. namespace属性值 必须与接口的权限定名

3. id属性必须与抽象方法名保持一致

4. 返回值类型和参数类型与方法的返回值和参数保持一致

5. 多参时

    通过#{arg+数字}或#{param+数字}的方式.

    接口中定义方法, 参数中使用@Param 注解设定参数名用于在 SQL 语句中使用.

