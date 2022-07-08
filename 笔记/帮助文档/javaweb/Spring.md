# MyBatis

## pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.zhamao</groupId>
    <artifactId>mybatis</artifactId>
    <version>1.0-SNAPSHOT</version>


<dependencies>
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>5.1.47</version>
    </dependency>
    <!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis</artifactId>
        <version>3.5.6</version>
    </dependency>

    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.12</version>
    </dependency>
    <!-- https://mvnrepository.com/artifact/org.projectlombok/lombok -->
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.22</version>
    <scope>provided</scope>
</dependency>


</dependencies>

    <!--读取该路径下 指定文件名-->
    <!--我们用这样的形式来约束maven 让他读取资源目录下的 该后缀文件. -->
<build>
    <resources>
        <resource>
            <directory>src/main/java</directory>
            <includes>
                <include>**/*.xml</include>
                <include>**/*.properties</include>
            </includes>
        </resource>

        <resource>
            <directory>src/main/resources</directory>
            <includes>
                <include>**/*.xml</include>
                <include>**/*.properties</include>
            </includes>
        </resource>

    </resources>
    <!--maven约束JDK版本  此处为 jdk11-->
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.7.0</version>
            <configuration>
                <release>11</release>
            </configuration>
        </plugin>
    </plugins>
</build>



</project>
```



## 练习数据

```sql
CREATE DATABASE yggl
use yggl
CREATE TABLE `departments` (
`DepartmentID`  char(3) NOT NULL COMMENT '部门编号' ,
`DepartmentName`  char(20) NOT NULL COMMENT '部门名' ,
`Note`  text NULL DEFAULT NULL COMMENT '备注' ,
PRIMARY KEY (`DepartmentID`)
)ENGINE=INNODB DEFAULT CHARSET=utf8;


INSERT INTO departments VALUES ('1', '财务部', null),
('2', '人力资源部', null),
('3', '经理办公室', null),
('4', '研发部', null),
('5', '市场部', null);



CREATE TABLE `employees` (
`EmployeeID`  char(6) NOT NULL ,
`Name`  char(10) NOT NULL ,
`Education`  char(4) NOT NULL ,
`Birthday`  date NOT NULL ,
`Sex`  char(2) NOT NULL ,
`WorkYear`  tinyint(1) NULL DEFAULT NULL ,
`Address`  varchar(20) NULL DEFAULT NULL ,
`PhoneNumber`  char(12) NULL DEFAULT NULL ,
`DepartmentID`  char(3) NOT NULL ,
PRIMARY KEY (`EmployeeID`)
)ENGINE=INNODB DEFAULT CHARSET=utf8;


INSERT INTO employees 
VALUES ('000001', '王林', '大专', '1966-01-23', '1', '8', '中山路32-1-508', '83355668', '2'),
('010008', '伍容华', '本科', '1976-03-28', '1', '3', '北京东路100-2', '83321321', '1'),
('020010', '王向容', '硕士', '1982-12-09', '1', '2', '四牌楼10-0-108', '83792361', '1'),
('020018', '李丽', '大专', '1960-07-30', '0', '6', '中山东路102-2', '83413301', '1'),
('102201', '刘明', '本科', '1972-10-18', '1', '3', '虎距路100-2', '83606608', '5'), 
('102208', '朱俊', '硕士', '1965-09-28', '1', '2', '牌楼巷5-3-106', '84708817', '5'),
('108991', '钟敏', '硕士', '1979-08-10', '0', '4', '中山路10-3-105', '83346722', '3'),
('111006', '张石兵', '本科', '1974-10-01', '1', '1', '解放路34-1-203', '84563418', '5'), 
('210678', '林涛', '大专', '1977-04-02', '1', '2', '中山北路24-35', '83467336', '3'),
('302566', '李玉珉', '本科', '1968-09-20', '1', '3', '热和路209-3', '58765991', '4'),
('308759', '叶凡', '本科', '1978-11-18', '1', '2', '北京西路3-7-52', '83308901', '4'), 
('504209', '陈林琳', '大专', '1969-09-03', '0', '5', '汉中路120-4-12', '84468158', '4');



CREATE TABLE `salary` (
`EmployeeID`  char(6) NOT NULL COMMENT '员工编号' ,
`InCome`  float NOT NULL COMMENT '收入' ,
`OutCome`  float NOT NULL COMMENT '支出' ,
PRIMARY KEY (`EmployeeID`)
)ENGINE=INNODB DEFAULT CHARSET=utf8;


INSERT INTO salary 
VALUES ('000001', '2100.8', '123.09'),
('010008', '1582.62', '88.03'),
('020010', '2860', '198'),
('020018', '2347.68', '180'),
('102201', '2569.88', '185.65'),
('102208', '1980', '100'),
('108991', '3259.98', '281.52'),
('111006', '1987.01', '79.58'),
('210678', '2240', '121'),
('302566', '2980.7', '210.2'),
('308759', '2531.98', '199.08'),
('504209', '2066.15', '108');

```



## 结构

### 结构图

![image-20211211232952495](F:/图像/typora图像保存位置/image-20211211232952495.png)

### 结构思想

与javaweb中的结构相似, 但是在mybatis中  用 mapper 取代了dao层.   从返回结果来看二者功能一致,不过是过程不同.  总而言之,mybatis确实避免了大量的重复的 jdbc代码 使的jdbc的使用更加便捷 实用.  

同样的我们用 接口来定义方法,  **不过我们不需要再写实现接口的实现类** 这一切将由 MyBatis来进行.  我们只需要 配置好 mapper.xml.   将对应的 类路径给对,  方法名给对 sql 语句写对就行了. 





## 配置文件

### mybatis-config.xml(含解析)

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<!-- 根标签 -->
<configuration>
    !-- 读取properties文件  在下面的事务管理器中 可以获取文件中的键值对 下面只是其中一种写法 peroperties标签内 还有更多的功能 如果只是读取文件的话 做到这一部就可以了 -->
<!--    <properties resource="db.properties"/>-->
<!--其内部的标签可以当做一个键值对来看待 name属性 对标  事务管理器中的 value属性-->
    <properties resource="db.properties">
        <property name="aaa" value="123456"/>
    </properties>

<!--
    <typeAlias>
    类型别名可为 Java 类型设置一个缩写名字。 它仅用于 XML 配置，意在降低冗余的全限定类名书写。
    这里的别名只可以使用在  <mapper>下的CRDB子标签中的 resultType="employees" 中.
    mapper映射路径 是不可以使用别名来代替的
    <package>
    我们也可以给 包 起别名  然后 在mapper 中 就可以直接使用 实体类名 来封装  一般我们在实体类多的时候这么用.
    我们也可以用 注解@Alias("")来给实体类起别名.

    每一个在包 domain.blog 中的 Java Bean，在没有注解的情况下，会使用 Bean 的首字母小写的非限定类名来作为它的别名。
    比如 domain.blog.Author 的别名为 author；若有注解，则别名为其注解值。

    例如：
-->
    <typeAliases>
<!--        <typeAlias alias="departments" type="com.zhamao.pojo.departments"/>-->
<!--        <typeAlias alias="employees" type="com.zhamao.pojo.employees"/>-->
<!--        <typeAlias alias="salary" type="com.zhamao.pojo.salary"/>-->
<!--        <typeAlias alias="employeesMapper" type="com.zhamao.mapper.employeesMapper"/>-->
        <package name="com.zhamao.pojo"/>
    </typeAliases>
    
    
    <!-- 环境，可以配置多个，default：指定采用哪个环境 -->
    <environments default="test">
        <!-- id：唯一标识 -->
        <environment id="test">
            <!-- 事务管理器，JDBC类型的事务管理器
 				还有另一个 MANAGED 这种类型的管理器 不会有提交或回滚的操作 默认情况下它会关闭连接 如果想要阻止
                    <property name="closeConnection" value="false"/>
                请这么设置

			-->
            <transactionManager type="JDBC" />
            <!-- 数据源，池类型的数据源  有三种内建的数据源类型（也就是 type="[ UNPOOLED | POOLED | JNDI ]"） -->
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.jdbc.Driver" />
                                <!--在这里我们仍要注意,SSL安全认证设置为false,除非我们做了相关配置. 否则就会爆出org.apache.ibatis.exceptions.PersistenceException: 
### Error querying database  导致我们的sql语句无法正常执行 -->
                <property name="url" value="jdbc:mysql://127.0.0.1:3306/yggl?useSSL=false&amp;useUnicode=true&amp;characterEncoding=utf-8&amp;" />

                <property name="username" value="root" />
                <property name="password" value="123456" />
            </dataSource>
        </environment>

    </environments>
    <!--注册Mapper文件,-->
    <mappers>
        <mapper resource="com/zhamao/mapper/employeesMapper.xml"/>
        <mapper resource="com/zhamao/mapper/departmentsMapper.xml"/>
        <mapper resource="com/zhamao/mapper/salaryMapper.xml"/>
    </mappers>
</configuration>
```



### mapper.xml(CRUD)

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<!-- mapper:根标签，namespace：这里要写接口的路径,文件中sql语句 执行的主体类是在项目中的哪个位置.-->
<mapper namespace="com.zhamao.mapper.salaryMapper">
    <!-- statement，内容：sql语句。id：主体类方法名
       resultType：sql查询结果返回值,
     -->
    <select id="getSalary" resultType="com.zhamao.pojo.salary">
        select EmployeeID,inCome,OutCome from yggl.salary
    </select>
    <!--parameterType: 传参类型 -->
    <select id="getEmployeesByID" parameterType="String" resultType="com.zhamao.pojo.employees" >
        select * from yggl.employees where EmployeeID = #{EmployeeID}
    </select>
	<!--要注意的点: 这里传参类型为实体类, 所以我们在接口中传的参数也应该为对应的实体类
		int addEmployee(employees emp);
		如果我们的参数类型为一个实体类的话,
		我们可以直接使用 实体类中的参数,  只要名字与属性名相匹配就行.
	-->
    <!--最最应该注意的是, 在mybatis中 所有的增删改 都是在事务中进行的, 所以我们在执行完 sql语句后 要记得在java代码中提交事务,
        //提交事务
        sqlSession.commit();
    -->
    <insert id="addEmployee" parameterType="com.zhamao.pojo.employees">
        INSERT INTO employees
            value (#{EmployeeID},#{Name},#{Education},#{Birthday},#{Sex},#{WorkYear},#{Address},#{PhoneNumber},#{DepartmentID});
    </insert>

</mapper>
```



### db.properties

```properties
driver=com.mysql.jdbc.Driver
url=jdbc:mysql://127.0.0.1:3306/yggl?useSSL=false&useUnicode=true&characterEncoding=utf-8
username=root
password=123456
```

















## ***构建项目流程

1.导包   pxm.xml

2.配置 jdbc链接  db.properties      

3.配置文件 , mybatis-config.xml  并配置  **事务管理器** 

4.编写工具类.mybatisUtils.java

```java
package com.zhamao.utils;

import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;

import java.io.IOException;
import java.io.InputStream;

public class MybatisUtils{
    private static SqlSessionFactory sqlSessionFactory;
    static{
        try {
            String resource = "mybatis-config.xml";
            InputStream inputStream =  Resources.getResourceAsStream(resource);
            sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
        }catch (IOException e) {
            e.printStackTrace();
        }
    }

    public static SqlSession getSqlSession(){
        return sqlSessionFactory.openSession();
    }


}
```



5.编写实体类, 实体类与表对标

6.编写 mapper接口,

7.编写Mapper.xml, 并将 Mapper.xml与对应的mapper绑定

8.在 config中 映射 Mapper.xml文件

9.编写测试类.

```java
public void testGetStudent(){
    SqlSession sqlSession = MyBatisUtils.getSqlSession();//获取sqlsession
    System.out.println(sqlSession.getMapper(StudentMapper.class).getStudent(1)); //通过sqlsession.getMapper()来获取Mapper接口中的信息.
}
```

















## 一些技巧及设计思想

### 传参对象与map的区别

```xml
<!--传参为对象, 好处是 我们可以 从对象属性中 获取想要的值,不需要传递一大堆不同类型的对象.
	
	坏处是, 我们在做修改或者别的操作时,  很多时候我们只修改 一个字段,  如果这个实体类有一百个属性 而我们又只需要一个或者几个
	时就会非常棘手.
-->
	<insert id="addEmployee" parameterType="com.zhamao.pojo.employees">
        INSERT INTO employees
            value (#{EmployeeID},#{Name},#{Education},#{Birthday},#{Sex},#{WorkYear},#{Address},#{PhoneNumber},#{DepartmentID});
    </insert> 

<!-----------------------分割线----------------------------------------->
<!--map就是为了解决这个比较棘手的问题,  避免我们必须要传递对象的尴尬之处.   通过键值对 我们可以模拟出 对象中  属性:值  的
	情况.  key为 属性名,value为 值.  有了这个我们甚至可以不需要实体类. 	
-->
	<insert id="addEmployee" parameterType="map">
        INSERT INTO employees
            value (#{EmployeeID},#{Name},#{Education},#{Birthday},#{Sex},#{WorkYear},#{Address},#{PhoneNumber},#{DepartmentID});
    </insert>
```





### 为什么实体类属性名要与表字段名一致

MyBatis中有一个类型处理器. 这个处理器会自动把 select 后面的字段    当做实体类中的属性名  来赋值.

比如

```java
class user{
	id;
	name;
	password;
}

select id,name,pwd from user
我们可以这么想象  类加载器  调用了 user的构造器  来给 user的id属性 name属性 以及 pwd属性赋值.  
但是我们的实体类中 并没有pwd属性,我们有的是password属性   所以最后构建出来的 user类 的password值为null
```

我们可以通过 给字段起别名的 方法来解决该问题  

```sql
select id,name,pwd as password from user
```

但我们可以想象到 这么做会很麻烦,应该存在更加牛逼的方案才对.

### resultMap(接上文)

```xml
 <resultMap id="起map名" type="映射对象(实体类)">
      <result column="字段名" property="实体类属性名"/>
</resultMap>
```









### 分页( limit )

为什么使用分页?		加快查找速度,减少一次性处理的数据量.   例如 电商网站 商品有**页一样.

```sql
select * from employees limit 0,5;        (第一个参数起始下标,第二个参数查找容量)
```

与增删改查的思维逻辑是一样的 不过是sql语句不一样罢了.   

同样的我们需要给这个select标签两个参数.    使用 map类型.       











下面两种 原理还是 limit 不过是使用方式不同 ,了解即可

![image-20211213142048374](F:/图像/typora图像保存位置/image-20211213142048374.png)

![image-20211213142103523](F:/图像/typora图像保存位置/image-20211213142103523.png)



![image-20211213141956573](F:/图像/typora图像保存位置/image-20211213141956573.png)















### 使用注解来代替xml

```java
public interface employeesMapper {
    @Select("select * from employees")
    List<employees> getEmployees();
//当我们只需要使用一些简单的sql时, 我们可以使用注解来进行开发,  可以节省开发时间.    使用注解开发的一大好处就是,不需要在配置mapper.xml文件.  这一切都会由注解类来进行配置.      
    /**当然注解开发也有他的弊端,  在mapper中 我们有各种各样的 数据类型 传参类型,以及起别名等等操作来 让我们的结构逻辑更清晰.   当 实体类属性名 与 表字段名不一致时 也可以顺利获取想要的数据.     这是 注解开发所做不到的.
    */
    
}

```

最重要的我们是要了解  注解是如何做到  在不配置xml 的情况下  , 清楚地知道 我们的方法名, 返回值类型. 传参,  已经类的路径的.   

答案是  通过反射机制.     

```java
        SqlSession sqlSession = MyBatisUtils.getSqlSession();
        //读取mapper的class文件
        employeesMapper employeesMapper = sqlSession.getMapper(employeesMapper.class);
		//这里我们通过反射  把mapper类 返回给了 sqlSession.  sqlSession通过强大的反射机制, 来获取 这个类的一系列信息.  包括我们的 类路径,方法名,返回值,传参等等.
        List<employees> arrayList = employeesMapper.getEmployees();
```

教学老师 提到了  这个注解开发 的本质是  **动态代理**     动态代理我还没学,**静态代理请移步**  java高级  设计模式来复习.    



动态代理是一种设计模式,  而注解开发 则是  用反射机制 来实现了 这一种设计模式.









#### **CRUD**以及@Param("")

![image-20211213152935935](F:/图像/typora图像保存位置/image-20211213152935935.png)

![image-20211213153054127](F:/图像/typora图像保存位置/image-20211213153054127.png)

#### #{}  和${}的区别

#{}是预编译的  可以预防 sql注入

${}是字符串拼接的可以被 sql注入















## 一些对象的生命周期

### SqlSessionFactoryBuilder

创建SqlSessionFactory后就不再使用了.

### SqlSessionFactory

创建后 理应一直存在  是一个生产sqlSession的工厂.

### SqlSession

每一个线程 都应有一个 sqlsession    会话嘛  想想javaweb中的session.   







## 日志

### 环境搭建

```xml
<!--mybatis-config.xml-->

<!--设置 用来设置一些功能 比如日志的版本  这里设定日志系统为 log4j    
	2021年12月13日13:56:13
	近期log4j2  也就是 log4j的升级版 出现了巨大漏洞. 可以通过sql注入来远程连接服务器  被部分 mc服务器服主们发现并上传b站.
	SLF4J | LOG4J | LOG4J2(bug) | JDK_LOGGING | COMMONS_LOGGING | STDOUT_LOGGING(mybatis自带) | NO_LOGGING(不选择日志)
-->

    <settings>
        <setting name="logImpl" value="LOG4J"/>
    </settings>


<!--pom.xml-->
<!--导入jar包  日志系统有很多 有的是mybatis自带的. 这种的不需要导包 在setting中配置一下即可使用. 但是一些外来的日志系统需要进行导包.-->

    <!-- https://mvnrepository.com/artifact/log4j/log4j -->
    <dependency>
        <groupId>log4j</groupId>
        <artifactId>log4j</artifactId>
        <version>1.2.17</version>
    </dependency>

```



### 配置文件    log4j.properties

```properties
log4j.rootLogger=DEBUG,console,file

#控制台输出的相关设置

log4j.appender.console = org.apache.log4j.ConsoleAppender
log4j.appender.console.Target = System.out			
log4j.appender.console.Threshold=DEBUG
log4j.appender.console.layout = org.apache.log4j.PatternLayout
log4j.appender.console.layout.ConversionPattern=[%c]-%m%n

#文件输出的相关设置
log4j.appender.file = org.apache.log4j.RollingFileAppender
log4j.appender.file.File=./log/sqllog.log
log4j.appender.file.MaxFileSize=10mb
log4j.appender.file.Threshold=DEBUG
log4j.appender.file.layout=org.apache.log4j.PatternLayout
log4j.appender.file.layout.ConversionPattern=[%p][%d{yy-MM-dd}][%c]%m%n

#日志输出级别
log4j.logger.org.mybatis=DEBUG
log4j.logger.java.sql=DEBUG
log4j.logger.java.sql.Statement=DEBUG
log4j.logger.java.sql.ResultSet=DEBUG
log4j.logger.java.sql.PreparedStatement=DEBUG
```





























## 一对多查询

### 按照结果嵌套处理(多表查询)

```xml
  <!--按照结果嵌套处理-->
    <select id="getAllStudent" resultMap="getAllStudent2">
        select s.id sid,s.name sname,t.name tname from student s,teacher t where s.tid = t.id
    </select>

    <resultMap id="getAllStudent2" type="Student">
        <!--property代表在实体类中属性名    column 在sql语句中的字段对应的 名字       -->
        <result property="id" column="sid"/>
        <result property="name" column="sname"/>
<!--    association  代表这个属性是一个对象类型     javaType 它在java代码中的 数据类型  该实例为  Teacher类
        association  可以进行子标签嵌套.
     -->
        <association property="teacher" javaType="Teacher">
            <result property="name" column="tname"/>
        </association>
    </resultMap>
```





### 按照查询嵌套处理(子查询)

```xml
<!--根据查询嵌套处理,   子查询    查询结果中的对象的信息, 其实是通过另一条 简单查询语句查到的信息来获取的.
    两条查询语句属于从属关系,   子语句中的 where判定条件  可以从父语句中返回的信息中获取
    拿本实例来讲  select * from student   的第三个字段为 tid   是老师的id
    而 select * from teacher where id = #{tid} 中  where的 id = ?    这个?  就是 上面那条查询语句中获取的 tid 的值.
-->
    <select id="getAllStudent2" resultMap="getAllStudent1">
        select id,name,tid from student
    </select>
    <select id="getTeacher" resultType="Teacher">
        select id,name from teacher where id = #{id}
    </select>
    <resultMap id="getAllStudent1" type="Student">
<!--            property代表在实体类中属性名    column 在sql语句中的字段对应的 名字       -->
        <result property="id" column="id"/>
        <result property="name" column="name"/>
        <!--    association 当association作为一个闭合标签时,其内部的property="" column="" 代表的是 父sql    select="" 该属性才代表 子sql
             -->
        <association property="teacher" column="tid" javaType="Teacher"  select="getTeacher"/>
    </resultMap>
```

为了方便理解 多配一张图

![image-20220108235341906](F:\图像\typora图像保存位置\image-20220108235341906.png)	确实符合猜想

![image-20220108235450508](F:/图像/typora图像保存位置/image-20220108235450508.png)















## 多对一查询

### java

```java
public class Teacher {
    private int id;
    private String name;
    private List<Student> students;
}
-----------------------------------------------------------------------------------------
public interface TeacherMapper {
    public Teacher getTeacherAllStudent(@Param("id") int id);
}
```

### xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.zhamao.dao.TeacherMapper">

    <select id="getTeacherAllStudent" resultMap="getTeacherAllStudent">
        select t.id tid,t.name tname,s.name sname from teacher t,student s where t.id = #{id} and s.tid = t.id
    </select>

    <resultMap id="getTeacherAllStudent" type="Teacher">
        <result property="id" column="tid"/>
        <result property="name" column="tname"/>
<!--    当查询结果集中 包含 集合 这一数据结构时  ,我们用collection 来设置集合信息   collection标签 规范类型 不使用 javaType=""属性
        使用 ofType=""来设置  集合中 泛型的规范.    比如当前实例collection标签  代表实体类 teacher中的  List<Student>类型.
        按照往常的理解 我们可能会用javaType="Student" , 甚至javaType="List<Student>"来表达.    但是 ofType="Student" 才是正确的表达方式.
-->     <collection property="students" ofType="Student">
            <result property="name" column="sname"/>
        </collection>
        
    </resultMap>
</mapper>
```









































## 动态sql拼接

### 什么是动态sql

动态 SQL 是 MyBatis 的强大特性之一。如果你使用过 JDBC 或其它类似的框架，你应该能理解根据不同条件拼接 SQL 语句有多痛苦，例如拼接时要确保不能忘记添加必要的空格，还要注意去掉列表最后一个列名的逗号。利用动态 SQL，可以彻底摆脱这种痛苦。

使用动态 SQL 并非一件易事，但借助可用于任何 SQL 映射语句中的强大的动态 SQL 语言，MyBatis 显著地提升了这一特性的易用性。

如果你之前用过 JSTL 或任何基于类 XML 语言的文本处理器，你对动态 SQL 元素可能会感觉似曾相识。在 MyBatis 之前的版本中，需要花时间了解大量的元素。借助功能强大的基于 OGNL 的表达式，MyBatis 3 替换了之前的大部分元素，大大精简了元素种类，现在要学习的元素种类比原来的一半还要少。

- if
- choose (when, otherwise)
- trim (where, set)
- foreach







### 环境搭建

1.表

```sql
CREATE TABLE `blog`(
`id` VARCHAR(50) NOT NULL COMMENT '博客id',
`title` VARCHAR(100) NOT NULL COMMENT '博客标题',
`author` VARCHAR(30) NOT NULL COMMENT '博客作者',
`create_time` DATETIME NOT NULL COMMENT '创建时间',
`views` INT(30) NOT NULL COMMENT '浏览量'
)ENGINE=INNODB DEFAULT CHARSET=utf8
```

2.新的工具类(id生成器)

```java
public class IdUtils {
    public static String getId(){
        return UUID.randomUUID().toString().replace("-","");
    }

}
```

3.插入数据

```java
@Test
public void test(){
    SqlSession sqlSession = MybatisUtils.getSqlSession();
    BlogMapper mapper = sqlSession.getMapper(BlogMapper.class);

    mapper.addBlog(new Blog(IdUtils.getId(),"我的教导主任","炸毛",new Date(),2000));
    mapper.addBlog(new Blog(IdUtils.getId(),"我是扩阴器","炸毛",new Date(),2000));
    mapper.addBlog(new Blog(IdUtils.getId(),"哼,想逃?闪电旋风劈","尻比",new Date(),2000));
    mapper.addBlog(new Blog(IdUtils.getId(),"啊对对对","王喜顺",new Date(),2000));
    mapper.addBlog(new Blog(IdUtils.getId(),"我最后一瓶甜水","梁潇",new Date(),2000));

    sqlSession.commit();
    sqlSession.close();
}
```





### 动态sql的好处

可以减少创建重复的sql语句, 我们可以像在 jsp中使用 动作一样.  在xml中 使用标签 来达到 动态拼接sql语句的效果, 这样可以达到 一条sql语句, 实现多种查询,     通俗来讲 就是    把    重写sql    给智能化了

里面的 <if></if>  标签的语法 一看就能明白 就不解释了.

```xml
<select id="getBlog" parameterType="map" resultType="Blog">
    select title,author,create_time,views from blog where 1=1
    <if test="title != null">
        and title = #{title}
    </if>
    <if test="author != null">
        and author = #{author}
    </if>
</select>
```



着重解释一下 该sql语句中的    where 1=1   .    

![image-20220109195739321](F:\图像\typora图像保存位置\image-20220109195739321.png)



### <  where> 结合上文 对 where的理解

原来   where 1=1 只是缓兵之计.  开发者们早已想到并解决了这个问题

where标签 会  识别拼接条件 是否是 第一个   如果是的话   会自动把 句首的 and去掉. 

```xml
<select id="getBlog" parameterType="map" resultType="Blog">
    select title,author,create_time,views from blog
    <where>
        <if test="title != null">
            and title = #{title}
        </if>
        <if test="author != null">
            and author = #{author}
        </if>
    </where>
</select>
```

### 一些动态sql标签

1.choose、when、otherwise  (switch ) 

​	选择语句   when条件 .   无符合条件时执行otherwise  

```xml
<select id="findActiveBlogLike"
     resultType="Blog">
  SELECT * FROM BLOG
  <where>
    <if test="state != null">
         state = #{state}
    </if>
    <if test="title != null">
        AND title like #{title}
    </if>
    <if test="author != null and author.name != null">
        AND author_name like #{author.name}
    </if>
  </where>
</select>
```

2.set   (updata set  (sql语句))    会自动去除最后一条语句中的  ,   所以放心大胆的写.

```xml
<update id="updateAuthorIfNecessary">
  update Author
    <set>
      <if test="username != null">username=#{username},</if>
      <if test="password != null">password=#{password},</if>
      <if test="email != null">email=#{email},</if>
      <if test="bio != null">bio=#{bio}</if>
    </set>
  where id=#{id}
</update>
```





3.foreach

![image-20220111141543156](F:/图像/typora图像保存位置/image-20220111141543156.png)













## Sql 片段

在 Mapper.xml中 使用使用 < sql>标签

![image-20220111134434998](F:/图像/typora图像保存位置/image-20220111134434998.png)









## 缓存

缓存的作用就是,将查到的数据,暂时存放到内存中,以减少连接数据库对资源的消耗. 

一般我们只有哪些,经常需要查询, 并且不经常修改的数据才会放到缓存中. 

**注意** 缓存不存在于数据库.

缓存分为一级缓存和二级缓存.





基本上就是这样。这个简单语句的效果如下:

- 映射语句文件中的所有 select 语句的结果将会被缓存。
- 映射语句文件中的所有 insert、update 和 delete 语句会刷新缓存。
- 缓存会使用最近最少使用算法（LRU, Least Recently Used）算法来清除不需要的缓存。
- 缓存不会定时进行刷新（也就是说，没有刷新间隔）。
- 缓存会保存列表或对象（无论查询方法返回哪种）的 1024 个引用。
- 缓存会被视为读/写缓存，这意味着获取到的对象并不是共享的，可以安全地被调用者修改，而不干扰其他调用者或线程所做的潜在修改。





![image-20220111173740620](F:/图像/typora图像保存位置/image-20220111173740620.png)





### 一级缓存

一级缓存是默认开启的, 也关闭不掉.      

当我们的两次查询中 穿插了 增删改 等操作时,缓存也会被清理. 

![image-20220111151556564](F:/图像/typora图像保存位置/image-20220111151556564.png)









### 二级缓存

![image-20220111172900532](F:/图像/typora图像保存位置/image-20220111172900532.png)

### 自定义缓存(Ehcache)

















# Spring5

## 一些名字理论解释

**bean**: 在Spring中, 我们在.xml中 配置beans    这里面的 一个个bean其实就是 我们在java中说的对象.  只不过我们在Spring中叫它bean

所以此文档中, 将会使用bean这个名词来代替对象.





![image-20220111182850592](F:/图像/typora图像保存位置/image-20220111182850592.png)





![image-20220111183312594](F:/图像/typora图像保存位置/image-20220111183312594.png)



控制反转(IOC)思想:![image-20220111194511612](F:/图像/typora图像保存位置/image-20220111194511612.png)

现在假设我们的项目 有三层架构.     dao,service,用户.

现在我们的 dao是我们的核心层,最开始它只有 一个类 One,  我们也在service中实现了 One的业务逻辑.    最后 用户点击就能获取到数据.  

随着项目的发展, 现在我们需要在 dao层多加 Two,Three,Fore.三个类,  那么同样的我们可能也需要在 service中更改源代码,或者多加几个类 ,才能使得用户获取到想要的东西.          这是由  程序员来主导程序,  我们怎么实现 service成为了 用户能不能获取到数据关键.  

而IOC 就是把身份调换.   产品是为用户服务的, 主动权交由到用户手中,  我们给用户提供选择, 由用户选择它想要获取的类.  这个更改是由用户来作,而不再是程序员在后台更改代码.  



这就是 IOC 思想,想要达到的效果(初学根据理解 试着去解释IOC  没有权威性.....参考者请注意)



   









面向切面(AOP)思想:

说白了就是代理模式,让我们可以的动态的为自己的代码 增加 一些功能.    其内部也主要使用 动态代理模式 来实现  用到了反射技术.



AOP能让我们 在不改动 原有源代码文件的情况下,  仅通过 添加新的文件,就可以为之前的 业务增加一些新功能  

可以参考 本笔记中 使用的 黄段子demo.   原本 我们只有插入 和射击 两个功能.  但是写好之后 我们发现  插入之前我们忘记做了 防护措施,   那么 现在我们必须要 添加一个 在插入之前 戴套 的功能.          我们的 插入 和射击 封装在 文件1里.     如果我们在构建代码时 ,使用了 AOP这样一种模式, 我就可以 通过 新建文件2  来给 文件1的 插入功能 之前 添加一个 戴套功能.    

这样就达到了 插入之前戴套, 而完全不用再去修改之前的源文件. 

大大节省了维护精力.







## 准备工作

本次学习使用版本: 5.3.14

官网下载地址: https://repo.spring.io/ui/native/release/org/springframework/spring

GetHub: https://github.com/spring-projects/spring-framework/releases





### Maven依赖

```xml
spring-webmvc包含了许多依赖 总之导它

<!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-webmvc</artifactId>
    <version>5.3.14</version>
</dependency>

<!-- https://mvnrepository.com/artifact/org.springframework/spring-jdbc -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-jdbc</artifactId>
    <version>5.3.14</version>
</dependency>

```













## 入门

1.导包

2.创建实体类

```java
package com.zhamao.pojo;

import lombok.Data;

@Data
public class User {
    private String name;

}
```

3.beans.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd">

<bean id="user1" class="com.zhamao.pojo.User">
    <property name="name" value="炸毛"></property>
</bean>


</beans>
```

4.测试类

```java
import com.zhamao.pojo.User;
import org.junit.Test;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class MyTest {
    @Test
    public void test1(){
        ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
        User user1 = (User) context.getBean("user1");
        System.out.println(user1.toString());
    }
}

//-----------输出为----
//User(name=炸毛)
    
```







## xml开发

### 基础知识

bean是Spring容器 生成对象的关键,  容器从bean中获取属性和值, 调用无参构造方法来生成对象

```java
User user1 = new User();//参照物,方便理解 bean
```



```xml
<bean id="tools1" class="com.zhamao.pojo.Tools"/><!--为了假设临时写的-->

<bean id="user1" class="com.zhamao.pojo.User">
    <property name="name" value="炸毛"></property>
    <property name="tools" ref="tools1"><!--假设user类内有一个 Tools对象 -->
</bean>
```

**id** 实例化变量名

**class** 要实例化的对象位置

<property name="对象内的属性名" value="对象内属性的值" ref="引用在Spring中创建的类.(引用在beans中注册的类)"> 要注意这个设置值是通过 set方法来完成的. 而不是构造函数. 



### 构造bean

```xml
<!--通过参数顺序来 构造bean    -->
    <bean id="user1" class="com.zhamao.pojo.User">
        <constructor-arg index="0" value="炸毛"></constructor-arg>
    </bean>
<!--    通过参数类型来 构造bean-->
    <bean id="user1" class="com.zhamao.pojo.User">
        <constructor-arg type="java.lang.String" value="炸毛"></constructor-arg>
    </bean>
<!--    通过参数名,来构造bean-->
    <bean id="user1" class="com.zhamao.pojo.User">
        <constructor-arg name="name" value="炸毛"></constructor-arg>
    </bean>
```

当bean的属性中含有另一个bean时, 我们该如何操作.

```java
public class User {
    private String name;
    private Tools tools;
}
//----------------
public class Tools {
    private String name;
}
//-----------------
@Test
    public void test1(){
        ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
        User user1 = (User) context.getBean("user1");
        System.out.println(user1.getName()+"有"+user1.getTools().getName());
    }

//输出为: 炸毛有扩阴器
```



```xml
    <bean id="tool1" class="com.zhamao.pojo.Tools">
        <constructor-arg name="name" value="扩阴器"/>
    </bean>

    <bean id="user1" class="com.zhamao.pojo.User">
        <constructor-arg name="name" value="炸毛"/>
        <constructor-arg name="tools" ref="tool1"/>
    </bean>
```

利用 ref 属性,直接调用就好. 



在容器加载配置文件的时候, 所有的bean都会被创造出来.

容器中的每一个 bean 都只会有一个. 

我们从容器中取bean,不管取几次,取出来的都是那一个. 

看下图,两个对象的地址都一模一样. 因为取得都是 容器中的 "user"对象.

![image-20220111220150189](F:/图像/typora图像保存位置/image-20220111220150189.png)







### 起别名

```xml
<alias name="user1" alias="user"/>
<bean id="user1" class="com.zhamao.pojo.User">
```

通过alias标签可以给 bean起别名, 这样我们在容器中 get时,通过别名也可以get到.

```xml
<bean id="user1" class="com.zhamao.pojo.User" name="user,u">
```

通过name属性也可以起别名 而且还可以通过 逗号  空格  分号   间隔来同时起多个别名

注意!当我们 起了重复的名称后, 容器get() bean时 会报错





### 合并配置文件

一般用于多人合作开发,  我们用一个 applicationContext.xml最为最后配置文件, 通过import 标签 将多个 xml合并为一个xml. 

在创建容器时只需要加载最终的就可以了.

```xml
<import resource="beans.xml"/>
```









### 注入各种数据类型

```xml
    <bean id="user1" class="com.zhamao.pojo.User">

<!--    基本数据类型    -->
        <property name="name" value="炸毛"/>
<!--    引用数据类型    -->
        <property name="tools" ref="tool1"/>


<!--    数组    -->
        <property name="address">
            <array>
                <value>河南</value>
            </array>
        </property>
<!--    List    -->
        <property name="hobby">
            <list>
                <value>这次想不冲都不行了</value>
            </list>
        </property>
<!--    map-->
        <property name="map">
            <map>
                <entry key="第一个数" value="5"/>
                <entry key="第二个数" value="10"/>
                <entry key="第三个数" value="15"/>
            </map>
        </property>
<!--        set-->
        <property name="set">
            <set>
                <value>啊哈哈哈</value>
            </set>
        </property>
<!--    赋予空值     -->
        <property name="NULL">
            <null/>
        </property>

    </bean>
```





### p命名和c命名

在头文件加入规范开启 p命名和c命名的使用

p命名空间和c命名空间    p:<property>标签    set注入;    c: 构造器注入

```xml
xmlns:p="http://www.springframework.org/schema/p"
xmlns:c="http://www.springframework.org/schema/c"

------完整头部
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:c="http://www.springframework.org/schema/c"
    xmlns:p="http://www.springframework.org/schema/p"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">
    
    
    
    ----------c命名实例
    <bean id="beanOne" class="x.y.ThingOne">
        <constructor-arg name="thingTwo" ref="beanTwo"/>
        <constructor-arg name="thingThree" ref="beanThree"/>
        <constructor-arg name="email" value="something@somewhere.com"/>
    </bean>

    <!-- c-namespace declaration with argument names -->
    <bean id="beanOne" class="x.y.ThingOne" c:thingTwo-ref="beanTwo"
        c:thingThree-ref="beanThree" c:email="something@somewhere.com"/>
    
    
    ---------p命名实例
    <bean name="john-classic" class="com.example.Person">
        <property name="name" value="John Doe"/>
        <property name="spouse" ref="jane"/>
    </bean>

    <bean name="john-modern"
        class="com.example.Person"
        p:name="John Doe"
        p:spouse-ref="jane"/>

```







### bean作用域

Spring容器默认使用单例模式,创建的bean都是同一个, 

```xml
<bean id="tool1" class="com.zhamao.pojo.Tools" scope="singleton(单例) || prototpe(原形) || ">
```

scope关键词 设置bean的作用域

singleton 单例模式 创造的bean在内存中只有一个.

prototpe 原形模式 每获取一次bean 都会在内存中重新建立一个新的bean

![image-20220112145334620](F:/图像/typora图像保存位置/image-20220112145334620.png)





### bean自动装配

![image-20220112151806947](F:/图像/typora图像保存位置/image-20220112151806947.png)

byName,根据类的set方法后跟的名字  来匹配  bean的id,   当id与set不一样的时候就会达不到预期效果

byType根据类的set方法的参数类型  来匹配  bean的class类型,   当类型与set不一样的时候就会达不到预期效果(如果有两个bean来自同一个类型,也会报错.)









## IOC注解开发

1.xml开启头文件约束  ----->  开启注解开发

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd">

    <context:annotation-config/>

</beans>
```

### 注解自动装配bean





```java

@Qualifier(value = "tools1")
private Tools tools;
//标注在字段上,表明这个字段会装载该id的bean

@Autowired(required = false || true)
//标注在属性上即可,   标注之后可以不在实体类中写set方法,但必须在IOC容器中存在,该注解会默认使用byType的方式实现装载,如果没有符合要求的再使用byName.		当repuired为 false是   该属性不存在于IOC容器.

@Resource(name="")  //该注解会默认使用byName的方式实现装载,如果没有符合要求的再使用byType.  而且也可以装载指定id   不属于Spring包
```



@Nullable 该注解标注在属性上,也表示该属性可以为空, 不过,它没有@Autowired(required = false)来的方便  标注了该注解的属性,在每个方法和参数前 都要再标一次,  而@Autowired 只需要标一次.

```java
public class User {
    @Autowired(required = false)
    private String name;
    @Nullable
    private Tools tools;

    public String getName() {
        return name;
    }

    @Nullable
    public Tools getTools() {
        return tools;
    }

    public User() {
    }

    public User(String name, @Nullable Tools tools) {
        this.name = name;
        this.tools = tools;
    }

    @Override
    public String toString() {
        return "User{" +
                "name='" + name + '\'' +
                ", tools=" + tools +
                '}';
    }
}
```





### 注解注入

```java
@Component//等价于 <bean id="person" class="com.zhamao.pojo.Person"/>
@Scope("prototype")  //设置bean范围
public class Person {
    @Value("炸毛")//等价于<property name="name" value="炸毛"/>
    private String name;
    @Value("15")
    private int age;
}
```



![image-20220112173443666](F:/图像/typora图像保存位置/image-20220112173443666.png)







### 注解生成xml,bean

完全使用java代码来开发.

```java
@Configuration   
// 配置了这个注解的类, 就相当于一个config.xml配置文件. 容器加载 该类的.class 文件来获取信息.
// 在该类中 写一些获取bean的方法 
@Bean   //该注解会将该方法注册成 bean     这个bean的id是方法名, class是return的类.
public User User(){
    return new User();
}
```









## AOP 面向切面 



### 依赖

```xml
<dependency>
    <groupId>org.aspectj</groupId>
    <artifactId>aspectjweaver</artifactId>
    <version>1.9.4</version>
</dependency>
```



### .xml 开启配置

```xml
	xmlns:aop="http://www.springframework.org/schema/aop"
	http://www.springframework.org/schema/aop
	http://www.springframework.org/schema/aop/spring-aop.xsd
```



### 入门(H段子演示demo)

1.java代码

```java
//继承 MethodBeforeAdvice 类  重写before 方法       
public class Info implements MethodBeforeAdvice {
    @Override
    public void before(Method method, Object[] args, Object target) throws Throwable {
        System.out.println(target.getClass().getName()+"类执行了"+method.getName()+"方法");
    }
}
-------------------------------------------------------------------------
public class Caca implements AfterReturningAdvice {

    @Override
    public void afterReturning(Object returnValue, Method method, Object[] args, Object target) throws Throwable {
        System.out.println(target.getClass().getName()+"在"+method.getName()+"之后给"+(String) args[0]+"擦了擦");
    }

}

====================================================
public interface service {//接口
    public void charu();
    public void sheji(String name);
}
--------------------------
public class serviceimpl implements service {//重写接口方法
    @Override
    public void charu() {
        System.out.println("开始插入");
    }

    @Override
    public void sheji(String name) {
        System.out.println("开始射击"+name);
    }
}
```

2.spring配置

环绕的类 只能选择 继承了 MethodBeforeAdvice等类 的方法 .  

在运行代码时,  当我们执行 切入点时,  会执行  环绕类中重写的方法.

就算是环绕类  也是要在 <bean> 中注册 ,才能够使用的.  这里本人好久没写 当时忘记注册了结果代码不提示.

```xml
    
<aop:config>
<!--    pointcut 切入点.    id  切入点编号  expression 表达    execution(* com.zhamao.service.serviceimpl.*(..))  代表切入点的位置 -->
        <aop:pointcut id="pointcut1" expression="execution(* com.zhamao.service.serviceimpl.charu(..))"/>
        <aop:pointcut id="pointcut2" expression="execution(* com.zhamao.service.serviceimpl.sheji(..))"/>
<!--    advisor 顾问,参事,环绕  advice-ref 选择环绕的类,  选择切入点id    -->
        <aop:advisor advice-ref="info" pointcut-ref="pointcut1"/>
        <aop:advisor advice-ref="Caca" pointcut-ref="pointcut2"/>
    </aop:config>
```

3.不得不提的 一些切入接口的功能及作用

```java
MethodBeforeAdvice接口   需要我们重写 before(...)方法,  该接口 会在我们 调用执行切入点 之前   优先执行本方法.
AfterReturningAdvice接口 需要我们重写 afterReturning(....)方法.  该方法 会在我们 调用执行切入点之后   再执行本方法  本方法比相较于 befor(...)多了一个参数 ,该参数代表切入点函数的返回值.
```

4.测试

```java
public class Test {
    @org.junit.Test
    public void test(){
        ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
        //这里要注意一点,  AOP的核心原理是动态代理模式,  而动态代理代理的是接口,  所以我们再获取 Bean 时 不要错误的去 获取实体类.
        service serviceImpl = (service) context.getBean("serviceImpl");

        serviceImpl.charu();

        serviceImpl.sheji("梦中女神");
    }
}
```







### 自定义切入类

```xml
<!--ref 切入类-->
        <aop:aspect ref="类">
<!--            设置切入点和其id-->
            <aop:pointcut id="1" expression="execution( * * * )"/>
<!--            after 在切入点执行后开始切入   method  填写切入类中的方法, pointcut-ref 选择切入点 -->
            <aop:after method="类.方法名"  pointcut-ref="1"/>
<!--            before 在切入点执行之前切入-->
            <aop:before method="类.方法名" pointcut-ref="1"/>
        </aop:aspect>
```







### 注解开发

```XML
<aop:aspectj-autoproxy/>   //开启注解支持[
```



```java
@Aspect   //表明 这是一个切面类
public class Section {
    @After("execution(* com.zhamao.demo.ServiceImpl.eat(..))")  //切入点之后执行
    public void cazui(){
        System.out.println("擦擦嘴");
    }

    @Before("execution(* com.zhamao.demo.ServiceImpl.drink(..))")   //切入点之前 执行
    public void daoshui(){
        System.out.println("倒水");
    }
    
    /*	如果使用了 @Around注解后, 如果我们不使用 pj.proceed();执行方法时    @After和@Before会失效 , 如果我们使用了
    那么 双方会同时进行,并且 @Around 内代码的优先级 要高于@After和@Before
    
    
    	
    */
    
    @Around("execution(* com.zhamao.demo.ServiceImpl.*(..))")   //还没搞明白  算是一种总和性的 , 而ProceedingJoinPoint 这个类 则提供了需多辅助功能.
    public void test(ProceedingJoinPoint pj) throws Throwable {
        Signature signature = pj.getSignature();
        System.out.println(signature+"之前先擦擦嘴");
        pj.proceed();//执行方法
    }


}
```









## Spring-MyBatis

### 依赖

```xml
<!--spring链接数据库 需要导这两个包-->	  
剩下的就是一些mybatis的包  在mybatis笔记里
	<dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-jdbc</artifactId>
        <version>5.3.14</version>
    </dependency>

    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis-spring</artifactId>
        <version>2.0.2</version>
    </dependency>
```



### 入门

1.配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/aop
       http://www.springframework.org/schema/aop/spring-aop.xsd">

<!-- 在Spring中 注册 jdbc的配置信息类   -->
    <bean id="DataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
        <property name="driverClassName" value="com.mysql.jdbc.Driver"/>
        <property name="url" value="jdbc:mysql://127.0.0.1:3306/yggl?useSSL=false&amp;useUnicode=true&amp;characterEncoding=utf-8"/>
        <property name="username" value="root"/>
        <property name="password" value="123456"/>
    </bean>
<!--    注册sqlSessionFactory 来加载配置信息类-->
    <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
        <property name="dataSource" ref="DataSource" />
<!--        加载配置文件 这里选择 Mybatis的xml文件 classpath 可以直接加载同级目录下的文件,  不同目录下的 需要标注路径,文件夹之前用"/"分级-->
        <property name="configLocation" value="classpath:Mybatis-config.xml"/>
        <property name="mapperLocations" value="classpath:com/zhamao/Mapper/*.xml"/>
    </bean>
<!--固定格式 注册sqlSession   但是在spring中他叫做sqlSessionTemplate  只是功能相似 并不代表实现技术一样  犹豫该类 中不存在set方法 所以只能通过构造器注入-->
    <bean id="sqlSessionTemplate" class="org.mybatis.spring.SqlSessionTemplate">
        <constructor-arg index="0" ref="sqlSessionFactory"/>
    </bean>
<!--在spring中, 我们还需要注册一个实体类, 该实体类中会在每一次CUDR操作中 加载对应的 Mapper文件. -->
    <bean id="blogMapper" class="com.zhamao.Mapper.BlogMapperImpl">
        <property name="sqlSessionTemplate" ref="sqlSessionTemplate"/>
    </bean>
<!--注册实体类-->
    <bean id="blog" class="com.zhamao.pojo.Blog"/>
</beans>
```

2.生成实体类和Mapper

```java
public class Blog {
    private String id;
    private String title;
    private String author;
    private Date create_time;
    private int views;
}
public interface BlogMapper {

    public List<Blog> selectByauthor(String author);
}
```



```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.zhamao.Mapper.BlogMapper">
    <select id="selectByauthor" parameterType="String" resultType="com.zhamao.pojo.Blog">
        select * from blog where author=#{author}
    </select>

</mapper>
```

3.生成映射器

该类必须是一个java实现类

```java
//该实现类要实现对应的 Mapper接口
//该类内部要有一个 SqlSessionTemplate属性,  通过该属性来加载 Mapper文件,代替sqlsession所做的工作
public class BlogMapperImpl implements BlogMapper{
    private SqlSessionTemplate sqlSessionTemplate;
	//要提供一个 set方法 来让spring注入SqlSessionTemplate
    public void setSqlSessionTemplate(SqlSessionTemplate sqlSessionTemplate) {
        this.sqlSessionTemplate = sqlSessionTemplate;
    }
	//获取mapper,调用方法,返回操作结果
    @Override
    public List<Blog> selectByauthor(String author) {
        BlogMapper mapper = sqlSessionTemplate.getMapper(BlogMapper.class);
        return mapper.selectByauthor(author);
    }
}
```

4.测试

```java
//Test
public class Test {

    @org.junit.Test
    public void test(){
        ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
        BlogMapper blogMapper = context.getBean("blogMapper",BlogMapper.class);

        System.out.println(blogMapper.selectByauthor("炸毛").toString());

    }
}

/**输出结果
[Blog(id=c4817fded41c4ab6812bf5e048a40d84, title=我的教导主任, author=炸毛, create_time=Sun Jan 09 19:31:08 CST 2022, views=2000), 

Blog(id=2fa55e31fe2c4ebe86d135c31c0d7065, title=我是扩阴器, author=炸毛, create_time=Sun Jan 09 19:43:24 CST 2022, views=2000)]
*/
```

### 第二种方式

更为简便

![image-20220313132349185](F:\图像\typora图像保存位置\image-20220313132349185.png)



### 事务 (逃课)

















# Spring-MVC

## 1.依赖

```xml
        <!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>5.3.14</version>
        </dependency>

        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>5.3.14</version>
        </dependency>

        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-web</artifactId>
            <version>5.3.14</version>
        </dependency>
<!--servlet依赖-->
        <!-- https://mvnrepository.com/artifact/javax.servlet/javax.servlet-api -->
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>4.0.1</version>
            <scope>provided</scope>
        </dependency>
<!--        jsp依赖-->
        <!-- https://mvnrepository.com/artifact/javax.servlet.jsp/javax.servlet.jsp-api -->
        <dependency>
            <groupId>javax.servlet.jsp</groupId>
            <artifactId>javax.servlet.jsp-api</artifactId>
            <version>2.3.3</version>
            <scope>provided</scope>
        </dependency>



        <!-- https://mvnrepository.com/artifact/org.projectlombok/lombok -->
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <version>1.18.22</version>
            <scope>provided</scope>
        </dependency>

        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
        </dependency>

```







## 入门

### web.xml

```xml
<!--配置DispatcherServlet(servlet管理器)-->
    <servlet>
        <servlet-name>SpringMVC</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <!--配置spring-mvc.xml的路径-->
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:springmvc-servlet.xml</param-value>
        </init-param>
    </servlet>
    <servlet-mapping>
        <servlet-name>SpringMVC</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>
```



### spring-mvc.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
    
<!--bean的name映射成URL    然后再自动补全InternalResourceViewResolver里配置的 前缀和后缀
	HandlerMapping   : 处理器映射器
	HandlerAdapter   : 处理器适配器
-->
    <bean class="org.springframework.web.servlet.handler.BeanNameUrlHandlerMapping"/>
    <bean class="org.springframework.web.servlet.handler.SimpleServletHandlerAdapter"/>



    <bean id="viewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <!-- 前缀,我们的视图文件应该放到/WEB-INF/jsp/目录下,这里我们需要在WEB-INF下面创建jsp文件夹 -->
        <property name="prefix" value="/WEB-INF/jsp/"/>
        <!-- 设置后缀为.jsp -->
        <property name="suffix" value=".jsp"/>
    </bean>
<!--注意!!! 注大意  他娘了个   可别写 \hello   网址上分隔的符号是这个"/"  妈了个逼的 浪费我两个半小时艹-->
    <bean name="/hello" class="com.zhamao.test.OneHandler"/>




</beans
```



### java

```java
public class OneHandler implements Controller {
    @Override
    public ModelAndView handleRequest(HttpServletRequest request, HttpServletResponse response) throws Exception {
        ModelAndView mv = new ModelAndView();
//        添加一个对象
        mv.addObject("test","我是一个对象");
//        添加一个视图
        mv.setViewName("hello");

        return mv;

    }
}
```







### 	BeanNameUrlHandlerMapping

博客:https://www.cnblogs.com/kendoziyu/p/SpingMvc-BeanNameUrlHandlerMapping.html

```java
protected String[] determineUrlsForHandler(String beanName) {
      List urls = new ArrayList<>();
      // bean 的名称以 “/” 开头
      if (beanName.startsWith("/")) {
            urls.add(beanName);
      }
      String[] aliases = obtainApplicationContext().getAliases(beanName);
      for (String alias : aliases) {
            // bean 的别名以 “/” 开头
            if (alias.startsWith("/")) {
                  urls.add(alias);
            }
      }
      return StringUtils.toStringArray(urls);
}
```

第一种：单独指定 **id** 或者 **name**

```xml
<bean id="/welcome" class="coderead.springframework.mvc.WelcomeController" />
<bean name="/hello" class="coderead.springframework.mvc.HelloGuestController" />
```

此时，容器把 <bean> 唯一的 **name** 或者 **id** 作为 beanName。

第二种：即指定 **id** 又指定 **name**

```xml
<bean id="welcomeController" name="/welcome" class="coderead.springframework.mvc.WelcomeController" />
```

此时，容器把 "welcomeController" 作为 beanName，把 "/welcome" 作为别名，就会走到下面的循环中。











## springmvc 执行流程(需要加深理解)



![image-20220321144456350](F:\图像\typora图像保存位置\image-20220321144456350.png)





![preview](https://pic3.zhimg.com/v2-3ffbf11cbb82dbdfa846b407d491b28e_r.jpg)

1. 用户向服务器发送请求，请求被Spring 前端控制Servelt DispatcherServlet捕获；

2. DispatcherServlet对请求URL进行解析，得到请求资源标识符（URI）。然后根据该URI，调用HandlerMapping获得该Handler配置的所有相关的对象（包括Handler对象以及Handler对象对应的拦截器），最后以HandlerExecutionChain对象的形式返回；

3. DispatcherServlet 根据获得的Handler，选择一个合适的HandlerAdapter。（**附注**：如果成功获得HandlerAdapter后，此时将开始执行拦截器的preHandler(...)方法）

4. 提取Request中的模型数据，填充Handler入参，开始执行Handler（Controller)。 在填充Handler的入参过程中，根据你的配置，Spring将帮你做一些额外的工作：

	​	HttpMessageConveter： 将请求消息（如Json、xml等数据）转换成一个对象，将对象转换为指定的响应信息

	​	数据转换：对请求消息进行数据转换。如String转换成Integer、Double等

	​	数据根式化：对请求消息进行数据格式化。 如将字符串转换成格式化数字或格式化日期等

	​	数据验证： 验证数据的有效性（长度、格式等），验证结果存储到BindingResult或Error中

5. Handler执行完成后，向DispatcherServlet 返回一个ModelAndView对象；

6. 根据返回的ModelAndView，选择一个适合的ViewResolver（必须是已经注册到Spring容器中的ViewResolver)返回给DispatcherServlet ；

7. ViewResolver 结合Model和View，来渲染视图

8. 将渲染结果返回给客户端。





## 注解开发基础流程

```xml
<!--固定格式以后将不在写-->
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">

    <servlet>
        <servlet-name>springmvc</servlet-name>
        <servlet-class>
            org.springframework.web.servlet.DispatcherServlet
        </servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:springmvc-servlet.xml</param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>

    <servlet-mapping>
        <servlet-name>springmvc</servlet-name>  <!-- 需要和上面的servlet-name保持一致 -->
        <url-pattern>/</url-pattern> <!-- url的匹配规则，/ 就是匹配所有 -->
    </servlet-mapping>
</web-app>
```





### 1.springmvc-servlet.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd http://www.springframework.org/schema/mvc https://www.springframework.org/schema/mvc/spring-mvc.xsd">

    <!-- 自动扫描包，让指定包下的注解生效,由IOC容器统一管理 -->
    <context:component-scan base-package="com.zhamao.controllers"/>
    <!-- 让Spring MVC不处理静态资源 -->
    <mvc:default-servlet-handler />
    <!--
    支持mvc注解驱动
        在spring中一般采用@RequestMapping注解来完成映射关系
        要想使@RequestMapping注解生效
        必须向上下文中注册DefaultAnnotationHandlerMapping
        和一个AnnotationMethodHandlerAdapter实例
        这两个实例分别在类级别和方法级别处理。
        而annotation-driven配置帮助我们自动完成上述两个实例的注入。
     -->
    <mvc:annotation-driven />

    <bean id="viewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <!-- 前缀,我们的视图文件应该放到/WEB-INF/jsp/目录下,这里我们需要在WEB-INF下面创建jsp文件夹 -->
        <property name="prefix" value="/WEB-INF/jsp/"/>
        <!-- 设置后缀为.jsp -->
        <property name="suffix" value=".jsp"/>
    </bean>



</beans>
```

### 2.java文件

```java
package com.zhamao.controllers;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
@RequestMapping("/index")//如果我们在类上做了这个注释, 该类下所有方法上的映射都会被加上这样一个父级关系 
public class HelloController {
	//对应的请求映射
    @RequestMapping("/index")//比如这里将会变成(localhost:8080/index/index)才可以请求到.
    public String helloController(Model model){
        model.addAttribute("test","我是大傻逼");
		//返回的字符串会拼接在 InternalResourceViewResolver(视图解析器)里配置的前缀后缀来确定返回视图.
        return "hello";

    }

}
```







## RestFul风格

是一种请求风格,  就是本来要这样子发送请求     localhost:8080/1.jsp?a=xx   用了之后就可以这样了  localhost:8080/a.jsp/xx



### 实现方式    

给传参添加 注解

```java
    @RequestMapping("/index/{username}/{psw}")
    public String helloController(@PathVariable String username, @PathVariable String psw, Model model){
//        System.out.println(username.toString()+"\n"+psw);
        model.addAttribute("test","我是大傻逼");
        return "hello";

    }
```



从前端传递一个对象

```java
  //  url:http://localhost:4396/index/?username="123"&password="123456"
	//其实还是传递一些字段参数 然后由容器自动封装.     老套路, 字段名要与实体类中的属性名匹配才可以 自动封装
	@GetMapping("/index")
    public String helloController(User user, Model model){
//        System.out.println(username.toString()+"\n"+psw);

        model.addAttribute("user",user);
        model.addAttribute("test","我是大傻逼");
        return "hello";

    }
```



## Filter

在web.xml中配置

```XML

<!--    文件过滤器-->
    <filter>
        <filter-name>encodingFilter</filter-name>
        <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
        <init-param>
            <param-name>encoding</param-name>
            <param-value>utf-8</param-value>
        </init-param>
    </filter>
    
    <filter-mapping>
        <filter-name>encodingFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>
```





## json

### 导包

```xml
<!-- https://mvnrepository.com/artifact/com.fasterxml.jackson.core/jackson-databind -->
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.13.2</version>
</dependency>
//二选一即可 下面那个是 阿里巴巴的   一堆静态方法.new都不用new了挺方便
<!-- https://mvnrepository.com/artifact/com.alibaba/fastjson -->
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>fastjson</artifactId>
    <version>1.2.79</version>
</dependency>


```

### xml配置解决乱码

```xml
<!--    json乱码配置-->
    <mvc:annotation-driven>
        <mvc:message-converters register-defaults="true">
            <bean class="org.springframework.http.converter.StringHttpMessageConverter">
                <constructor-arg value="UTF-8"/>
            </bean>
            <bean class="org.springframework.http.converter.json.MappingJackson2HttpMessageConverter">
                <property name="objectMapper">
                    <bean class="org.springframework.http.converter.json.Jackson2ObjectMapperFactoryBean">
                        <property name="failOnEmptyBeans" value="false"/>
                    </bean>
                </property>
            </bean>
        </mvc:message-converters>
    </mvc:annotation-driven>
```

### 注解

```java
@RestController//注册在类上  表示这个类下面的方法返回的全是json字符串
@ResponseBody//注册在方法上 表示这个映射返回的是一个 json字符串

```

### 方法

https://www.jianshu.com/p/67b6da565f81

介绍的挺多样的上面这篇博客

```java
//json转java     参数可以是
objectMapper.readValue(参数,xx.class)
//java转json
    //写到文件中
objectMapper.writeValue( new FileOutputStream("data/output-2.json"), car);
	//写到字符串中
String json = objectMapper.writeValueAsString(car);

//去掉默认的时间戳格式     
objectMapper.configure(SerializationFeature.WRITE_DATES_AS_TIMESTAMPS, false);
//设置为东八区
objectMapper.setTimeZone(TimeZone.getTimeZone("GMT+8"));
// 设置输入:禁止把POJO中值为null的字段映射到json字符串中
objectMapper.configure(SerializationFeature.WRITE_NULL_MAP_VALUES, false);
 //空值不序列化
objectMapper.setSerializationInclusion(JsonInclude.Include.NON_NULL);
//反序列化时，属性不存在的兼容处理
objectMapper.getDeserializationConfig().withoutFeatures(DeserializationFeature.FAIL_ON_UNKNOWN_PROPERTIES);
//序列化时，日期的统一格式
objectMapper.setDateFormat(new SimpleDateFormat("yyyy-MM-dd HH:mm:ss"));
//序列化日期时以timestamps输出，默认true
objectMapper.configure(SerializationFeature.WRITE_DATES_AS_TIMESTAMPS, false);
//序列化枚举是以toString()来输出，默认false，即默认以name()来输出
objectMapper.configure(SerializationFeature.WRITE_ENUMS_USING_TO_STRING,true);
//序列化枚举是以ordinal()来输出，默认false
objectMapper.configure(SerializationFeature.WRITE_ENUMS_USING_INDEX,false);
//类为空时，不要抛异常
objectMapper.configure(SerializationFeature.FAIL_ON_EMPTY_BEANS, false);
//反序列化时,遇到未知属性时是否引起结果失败
objectMapper.configure(DeserializationFeature.FAIL_ON_UNKNOWN_PROPERTIES, false);
 //单引号处理
objectMapper.configure(JsonParser.Feature.ALLOW_SINGLE_QUOTES, true);
//解析器支持解析结束符
objectMapper.configure(JsonParser.Feature.ALLOW_UNQUOTED_CONTROL_CHARS, true);
```



## 方法重载思想

节省代码量,更高限度的实现代码复用

![image-20220323194648046](F:\图像\typora图像保存位置\image-20220323194648046.png)





