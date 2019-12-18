# Mybatis

> 新手，也可以先使用以下Maven，Windows如何安装，请参考：https://www.misiyu.cn/article/131.html



## ORM

ORM可以解决数据库与程序间的异构性，比如在Java中我们使用String表示字符串，而Oracle中可使用varchar2，MySQL中可使用varchar，SQLServer可使用nvarchar。

对象关系映射（英语：Object Relational Mapping，简称ORM，或O/RM，或O/R mapping），用于实现面向对象编程语言里不同类型系统的数据之间的转换。简单的说，ORM是通过使用描述对象和数据库之间映射的元数据，将程序中的对象与关系数据库相互映射。



ORM（O/R Mapping：对象关系映射）：一种将内存中的对象保存到关系型数据库中的技术负责实体域对象的持久化，封装数据库访问细节ORM提供了实现持久化层的另一种模式，采用映射元数据（XML）来描述对象-关系的映射细节，使得ORM中间件能在任何一个Java应用的业务逻辑层和数据库之间充当桥梁。

ORM提供了实现持久化层的另一种模式，它采用映射元数据来描述对象关系的映射，使得ORM中间件能在任何一个应用的业务逻辑层和数据库层之间充当桥梁。



### Java典型的ORM

**hibernate：**全自动的框架，强大、复杂、笨重、学习成本较高

**Mybatis：**半自动的框架（懂数据库的人才能操作）必须要自己写sql

**JPA：**JPA全称Java Persistence API、JPA通过JDK5.0注解或XML描述对象-关系表的映射关系，是Java自带的框架

### ORM三个核心原则

·简单：以最基本的形式建模数据。
·传达性：数据库结构被任何人都能理解的语言文档化。
·精确性：基于数据模型创建正确标准化了的结构。

### ORM的优缺点

**优点：**

1.提高了开发效率。由于ORM可以自动对Entity对象与数据库中的Table进行字段与属性的映射，所以我们实际可能已经不需要一个专用的、庞大的数据访问层。

2.ORM提供了对数据库的映射，不用sql直接编码，能够像操作对象一样从数据库获取数据。

**缺点：**

牺牲程序的执行效率和会固定思维模式，降低了开发的灵活性。

从系统结构上来看，采用ORM的系统一般都是多层系统，系统的层次多了，效率就会降低。ORM是一种完全的面向对象的做法，而面向对象的做法也会对性能产生一定的影



## IDEA配置

两个配置xml文件：

**MyBatis主配置文件：**

```ini
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
  PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
  "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
  <environments default="development">
    <environment id="development">
      <transactionManager type="JDBC"/>
      <dataSource type="POOLED">
        <property name="driver" value="${driver}"/>
        <property name="url" value="${url}"/>
        <property name="username" value="${username}"/>
        <property name="password" value="${password}"/>
      </dataSource>
    </environment>
  </environments>
  <mappers>
    <mapper resource="org/mybatis/example/BlogMapper.xml"/>
  </mappers>
</configuration>
```

**Mapper文件：**

```ini
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
  PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
  "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="org.mybatis.example.BlogMapper">
  <select id="selectBlog" resultType="Blog">
    select * from Blog where id = #{id}
  </select>
</mapper>
```



## Mybatis

MyBatis 本是apache的一个开源项目iBatis，2010年这个项目由apache software foundation 迁移到了google code，并且改名为MyBatis。2013年11月迁移到Github。

iBATIS一词来源于“internet"和“abatis”的组合，是一个基于Java的持久层框架。

iBATIS提供的持久层框架包括SQL Maps和Data Access Objects（DAOs）



**MyBatis 是一款优秀的持久层框架**，它支持定制化SQL、存储过程以及高级映射。

MyBatis 避免了几乎所有的JDBC代码和手动设置参数以及获取结果集。MyBatis 可以使用简单的XML 或注解来配置和映射原生信息，将接口和Java的**POJOs**（Plain Old Java Objects，普通的Java对象）映射成数据库中的记录。

### Mybatis 特点

**简单易学：**本身就很小且简单。没有任何第三方依赖，最简单安装只要两个jar文件+配置几个sql映射文件易于学习，易于使用，通过文档和源代码，可以比较完全的掌握它的设计思路和实现。

**灵活：**mybatis不会对应用程序或者数据库的现有设计强加任何影响。sql写在xm里，便于统一管理和优化。通过sql基本上可以实现我们不使用数据访问框架可以实现的所有功能，或许更多。



**解除sql与程序代码的耦合：**通过提供DAO层，将业务逻辑和数据访问逻辑分离，使系统的设计更清晰，更易维护，更易单元测试。sql和代码的分离，提高了可维护性。

提供映射标签，支持对象与数据库的ORM字段关系映射提供对象关系映射标签，支持对象关系组建维护提供XML标签，支持编写动态sql。



### Mybatis 工作流程

**（1）、加载配置并初始化触发条件：**

加载配置文件配置来源于两个地方，一处是配置文件，一处是Java代码的注解，将SQL的配置信息加载成为一个个MappedStatement对象（包括了传入参数映射配置、执行的SQL语句、结果映射配置），存储在内存中。

**（2）、接收调用请求触发条件：**

调用Mybatis提供的API传入参数：为SQL的ID和传入参数对象处理过程：将请求传递给下层的请求处理层进行处理。

**（3）、处理操作请求触发条件：API接口层传递请求过来**

传入参数：为SQL的ID和传入参数对象

处理过程：

（A）根据SQL的ID查找对应的MappedStatement对象。

（B）根据传入参数对象解析MappedStatement对象，得到最终要执行的SQL和执行传入参数。

（C）获取数据库连接，根据得到的最终SQL语句和执行传入参数到数据库执行，并得到执行结果。

**（4）、返回处理结果将最终的处理结果返回。**



无论是用过的hibernate，mybatis，你都可以法相他们有一个共同点：

在java对象和数据库之间有做mapping的配置文件，也通常是xml文件从配置文件（通常是XML配置文件中）得到SessionFactory由SessionFactory 产生Session在Session中完成对数据的增删改查和事务提交等在用完之后关闭Session



### Mybatis 架构

Mybatis的功能架构分为三层：

**API接口层：**提供给外部使用的接口API，开发人员通过这些本地API来操纵数据库。接口层一接收到调用请求就会调用数据处理层来完成具体的数据处理。

**数据处理层：**负责具体的SQL查找、SQL解析、SQL执行和执行结果映射处理等。它主要的目的是根据调用的请求完成一次数据库操作。

**基础支撑层：**负责最基础的功能支撑，包括连接管理、事务管理、配置加载和缓存处理，这些都是共用的东西，将他们抽取出来作为最基础的组件。为上层的数据处理层提供最基础的支撑。



### Mybatis 成员 层次结构

**主要成员：**

Configuration: MyBatis所有的配置信息都保存在Configuration对象之中，配置文件中的大部分配置都会存储到该类中。

SqlSession：作为MyBatis工作的主要顶层API，表示和数据库交互时的会话，完成必要数据库增删改查功能。

Executor:MyBatis执行器，是MyBatis调度的核心，负责SQL语句的生成和查询缓存的维护。

StatementHandler：封装了JDBC Statement操作，负责对JDBC statement的操作，如设置参数等。

ParameterHandler：负责对用户传递的参数转换成JDBC Statement 所对应的数据类型。

ResultSetHandler：负责将JDBC返回的ResultSet结果集对象转换成List类型的集合

TypeHandler：负责ava数据类型和jdbc数据类型（也可以说是数据表列类型）之间的映射和转换

MappedStatement:MappedStatement维护一条`<selectlupdateldeletelinsert>`节点的封装

SqlSource：负责根据用户传递的parameterObject，动态地生成SQL语句，将信息封装到BoundSql对象中，并返回

BoundSql：表示动态生成的SQL语句以及相应的参数信息



**层次结构**

....

## 创建Mybatis项目

### Maven

总体步骤：

1. 创建maven工程并导入坐标。
2. 创建实体类和dao的接口。
3. 创建Mybatis的主配置文件。
4. 创建mapper映射文件。

#### 新建

通过maven创建项目比较简单。

IDEA中创建Maven选择即可，

![截图-1573201666](https://wimg.misiyu.cn/images/20191108/1573201666_9f417a947ba8aa1.png?x-oss-process=style/common)

#### 配置

**pom.xml**

```ini
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.misiai</groupId>
    <artifactId>test01</artifactId>
    <version>1.0-SNAPSHOT</version>

    <dependencies>
<!--        mybatis-->
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.5.2</version>
        </dependency>
<!--        mysql-->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.45</version>
        </dependency>
<!--        junit-->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
        </dependency>
<!--        log-->
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-log4j12</artifactId>
            <version>1.6.1</version>
        </dependency>
    </dependencies>

</project>
```



**项目目录**

![截图-1573216948](https://wimg.misiyu.cn/images/20191108/1573216949_1714bbe83662077.png?x-oss-process=style/common)

**resources/mybatis-config.xml文件**

该文件主要设置数据库配置以及映射文件(mapper)

```ini
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<!-- mybatis 的主配置 文件-->
<configuration>
    <!--配置环境-->
    <environments default="development">
        <environment id="development">
            <!--配置事务环境-->
            <transactionManager type="JDBC"/>
            <!--配置数据源（连接池）-->
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.jdbc.Driver"/>
                <property name="url"
                          value="jdbc:mysql://localhost:3306/my_blog?characterEncoding=UTF-8&amp;useSSL=false"/>
                <property name="username" value="root"/>
                <property name="password" value="root"/>
            </dataSource>
        </environment>
    </environments>
    <!--指定映射文件配置的位置，-->
    <mappers>
        <!-- 路径要对，不然报错，以/分割
            该文件和mapper/*Mapper.xml文件都位于resources目录下
            注意要把.xml加上
            =======================
            如果使用注解方式，此处应该使用class属性指定被注解的dao全限定名
            然后此处分隔符就不是/而是.了
        -->
        <!--<mapper resource="com/misiai/dao/IArticleDao"/>-->
        <mapper class="com.misiai.dao.IArticleDao"/>
    </mappers>
</configuration>
```

**resources/mapper/StudentMapper.xml文件**

该文件是映射文件，主要设置一些底层sql语句

```ini
<?xml version="1.0" encoding="UTF-8" ?>
<!--映射文件-->
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<!-- 
	namespace命名空间需要全局唯一，该命名空间和下面的id="createStudent"会在下面java类中调用时指定
-->
<mapper namespace="com.misiai.dao.studentMapper">
<!--       parameterType 就是你要传入的参数类型，可以是pojo里面的对象类型，然后会自动getter其中的成员变量（也即数据库的字段）
除了是对象类型，还可以是String，int,long,double,boolean等普通类型。
keyProperty="主键"
useGeneratedKeys="true" // 是否自增
-->
    <insert id="createStudent" parameterType="com.misiai.pojo.Student"
            keyProperty="id" useGeneratedKeys="true">
        insert into tb_student(sname,sno,gender,age)
        values(#{sname},#{sno},#{gender},#{age})
    </insert>
</mapper>
```

**新建测试类**

```java
import com.misiai.pojo.Student;
import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;
import org.junit.Test;

import java.io.IOException;
import java.io.Reader;

public class TestMybatis {
    @Test
    public void insert() {
        String resource = "mybatis-config.xml";
        Reader reader = null;
        SqlSession session = null;
        try {
            reader = Resources.getResourceAsReader(resource);
            SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(reader);
            session = sqlSessionFactory.openSession();

            // 创建一个学生对象
            Student student = new Student("无小道", "171494124", 22);
            // 这里的com.misiai.dao.studentMapper和之前编写studentMapper.xml填入的命名空间是对应的，createStudent是定义的id值。
            session.insert("com.misiai.dao.studentMapper.createStudent", student);
            session.commit();

        } catch (IOException e) {
            e.printStackTrace();
            session.rollback();
        } finally {
            try {
                reader.close();

            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}
```

**其他：log4j.properties**

在resources目录下新建该文件【可选，选择打印日志格式等】

```ini
### 设置###
log4j.rootLogger = debug,stdout,D,E

### 输出信息到控制抬 ###
log4j.appender.stdout = org.apache.log4j.ConsoleAppender
log4j.appender.stdout.Target = System.out
log4j.appender.stdout.layout = org.apache.log4j.PatternLayout
log4j.appender.stdout.layout.ConversionPattern = [%-5p] %d{yyyy-MM-dd HH:mm:ss,SSS} method:%l%n%m%n

### 输出DEBUG 级别以上的日志到=E://logs/error.log ###
log4j.appender.D = org.apache.log4j.DailyRollingFileAppender
log4j.appender.D.File = F://logs/log.log
log4j.appender.D.Append = true
log4j.appender.D.Threshold = DEBUG
log4j.appender.D.layout = org.apache.log4j.PatternLayout
log4j.appender.D.layout.ConversionPattern = %-d{yyyy-MM-dd HH:mm:ss}  [ %t:%r ] - [ %p ]  %m%n

### 输出ERROR 级别以上的日志到=E://logs/error.log ###
log4j.appender.E = org.apache.log4j.DailyRollingFileAppender
log4j.appender.E.File =E://logs/error.log
log4j.appender.E.Append = true
log4j.appender.E.Threshold = ERROR
log4j.appender.E.layout = org.apache.log4j.PatternLayout
log4j.appender.E.layout.ConversionPattern = %-d{yyyy-MM-dd HH:mm:ss}  [ %t:%r ] - [ %p ]  %m%n
```

添加以上参数后，就会打印调试日志：

```ini
Created connection 660879561.
[DEBUG] 2019-11-09 09:36:27,275 method:org.apache.ibatis.transaction.jdbc.JdbcTransaction.setDesiredAutoCommit(JdbcTransaction.java:100)
Setting autocommit to false on JDBC Connection [com.mysql.jdbc.JDBC4Connection@276438c9]
[DEBUG] 2019-11-09 09:36:27,286 method:org.apache.ibatis.logging.jdbc.BaseJdbcLogger.debug(BaseJdbcLogger.java:143)
==>  Preparing: insert into tb_student(sname,sno,gender,age) values(?,?,?,?) 
[DEBUG] 2019-11-09 09:36:27,388 method:org.apache.ibatis.logging.jdbc.BaseJdbcLogger.debug(BaseJdbcLogger.java:143)
==> Parameters: 无小道(String), 171494124(String), 0(Integer), 22(Integer)
[DEBUG] 2019-11-09 09:36:27,625 method:org.apache.ibatis.logging.jdbc.BaseJdbcLogger.debug(BaseJdbcLogger.java:143)
<==    Updates: 1
```

#### 测试

`src\test\java\TestMybatis.java`

```java
import com.misiai.dao.IArticleDao;
import com.misiai.domain.Article;
import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;

import java.io.IOException;
import java.io.InputStream;
import java.util.List;

public class TestMybatis {
    public static void main(String[] args) throws IOException {
        //    1.读取配置文件
        InputStream in = Resources.getResourceAsStream("mybatis-config.xml");
        //    2.创建SqlSessionFactory工厂
        SqlSessionFactoryBuilder builder = new SqlSessionFactoryBuilder();
        SqlSessionFactory sqlSessionFactory = builder.build(in);
        //    3.使用工厂生产SqlSession
        SqlSession session = sqlSessionFactory.openSession();
        //    4.使用SqlSession创建Dao的代理对象
        IArticleDao articleDao = session.getMapper(IArticleDao.class);
        //    5.使用代理对象执行
        List<Article> articles = articleDao.findAll();
        for (Article article : articles) {
            System.out.println(article);
        }
        //    6.释放资源
        session.close();
        in.close();
    }
}
```

> 以上是第一个案例写法，之前还有另外一种写法。
>
> 这种方法需要遵循：
>
> - mybatis的映射配置文件位置必须和dao接口的包结构位置相同。
> - 映射配置文件的mapper标签的namespace属性的值必须是dao接口的 全限定类名。
> - 映射配置文件的的操作配置（select），id属性必须是dao接口的方法名。
>
> 遵循以上后，我们就不用写dao接口的实现类

## 通过注解使用

首先就不需要`src\main\resources\com\misiai\dao`目录及以下的配置文件了

```java
package com.misiai.dao;

import com.misiai.domain.Article;
import org.apache.ibatis.annotations.Select;

import java.util.List;

public interface IArticleDao {
    @Select("select * from blog_articles")
    List<Article> findAll();
}
```

## 编写dao实现类方式

...

## 分析

![截图-1573288481](https://wimg.misiyu.cn/images/20191109/1573288481_5eb0eb178afc2bf.png?x-oss-process=style/common)



![截图-1573288894](https://wimg.misiyu.cn/images/20191109/1573288894_b1715af8c8c6eb3.png?x-oss-process=style/common)

## 常用CURD文件

`IArticleDao.xml`

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.misiai.dao.IArticleDao">
    <!--配置查询所有的操作-->
    <select id="findAll" resultType="com.misiai.domain.Article">
        select * from blog_articles;
    </select>

    <insert id="saveArticle" parameterType="com.misiai.domain.Article">
        insert into blog_articles (title,content,author_id,category_id,tags)
        values (#{title},#{content},#{author_id},#{category_id},#{tags});
    </insert>
    <update id="updateArticle" parameterType="com.misiai.domain.Article">
        update blog_articles set title = #{title},content=#{content},tags=#{tags} where id=#{id};
    </update>
    <!--查询一个时，其中的aid随意即可-->
    <delete id="deleteById" parameterType="java.lang.Integer">
        delete from blog_articles where id=#{aid}
    </delete>

    <select id="findById" parameterType="java.lang.Integer" resultType="com.misiai.domain.Article">
        select * from blog_articles where id=#{id};
    </select>

    <select id="findByTitle" parameterType="java.lang.String" resultType="com.misiai.domain.Article">
        select * from blog_articles where title like #{title};
    </select>

    <!--    获取总记录条数-->
    <select id="findTotal" resultType="int">
        select count(*) from blog_articles;
    </select>
</mapper>
```

`MybatisTest.java`

```java
package com.misiai.test;

import com.misiai.dao.IArticleDao;
import com.misiai.domain.Article;
import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;
import org.junit.After;
import org.junit.Before;
import org.junit.Test;

import java.io.IOException;
import java.io.InputStream;
import java.util.List;

public class MybatisTest {

    //    1.读取配置文件
    InputStream in = null;
    //    2.创建SqlSessionFactory工厂
    SqlSessionFactoryBuilder builder = null;
    SqlSessionFactory sqlSessionFactory = null;
    //    3.使用工厂生产SqlSession
    SqlSession session = null;
    //    4.使用SqlSession创建Dao的代理对象
    IArticleDao articleDao = null;

    @Before
    public void before() throws IOException {
        in = Resources.getResourceAsStream("mybatis-config.xml");
        builder = new SqlSessionFactoryBuilder();
        sqlSessionFactory = builder.build(in);
        session = sqlSessionFactory.openSession();
        articleDao = session.getMapper(IArticleDao.class);
    }

    @After
    public void after() throws IOException {
        // 提交事务
        session.commit();
        in.close();
        session.close();
    }

    @Test
    public void testSave() {
        Article article = new Article();
        article.setAuthor_id(1);
        article.setCategory_id(1);
        article.setContent("hello world");
        article.setTags("title,article,tags");
        article.setTitle("Fisrt save in java");

        session.insert("com.misiai.dao.IArticleDao.saveArticle", article);
        System.out.println("ok");
    }

    @Test
    public void testUpdate() {
        Article article = new Article();
        article.setAuthor_id(1);
        article.setCategory_id(1);
        article.setId(61);
        article.setContent("hello 222 world");
        article.setTags("title,article,tags");
        article.setTitle("Fisrt save in java");

        session.update("com.misiai.dao.IArticleDao.updateArticle", article);
        System.out.println("ok");
    }

    @Test
    public void testDelete() {
        Article article = new Article();
        article.setId(61);

        session.delete("com.misiai.dao.IArticleDao.deleteById", 61);
        System.out.println("ok");
    }

    @Test
    public void testFindById() {

        Article article = session.selectOne("com.misiai.dao.IArticleDao.findById", 59);
        System.out.println(article);
        System.out.println("ok");
    }

    @Test
    public void testFindByTitle() {
        String title = "%子%";
        List<Article> articles = session.selectList("com.misiai.dao.IArticleDao.findByTitle", title);
        for (Article article :
                articles) {
            System.out.println(article);
        }
        System.out.println("ok");
    }
    @Test
    public void testFindTotal() {
        int count = articleDao.findTotal();
        System.out.println("count = " + count);
    }
}
```

`IArticleDao.java`

```java
package com.misiai.dao;

import com.misiai.domain.Article;

import java.util.List;

public interface IArticleDao {
    List<Article> findAll();

    void saveArticle(Article article);

    void updateArticle(Article article);

    void deleteById(Integer id);

    Article findById(Integer id);

    List<Article> findByTitle(String title);

    int findTotal();
}
```

**其中模糊查询有两种方式：**

**xml**

```xml
<select id="findByTitle" parameterType="java.lang.String" resultType="com.misiai.domain.Article">
    <!---select * from blog_articles where title like #{title};-->
    select * from blog_articles where title like '%${value}%';
</select>
```

**java**

```java
@Test
public void testFindByTitle() {
    // String title = "%子%";
    String title = "子";
    List<Article> articles = session.selectList("com.misiai.dao.IArticleDao.findByTitle", title);
    for (Article article :
            articles) {
        System.out.println(article);
    }
    System.out.println("ok");
}
```

> 有些人更推荐注释掉的那种方式。

## Mybatis参数深入

### Mybatis的参数

Mybatis：parameterType

**OGNL表达式：**

Object Graphic Navigation Language   对象图导航语言
它是通过对象的取值方法来获取数据。在写法上把get给省略了。
比如：我们获取用户的名称
类中的写法：user.getUsername();
OGNL表达式写法：user.username

#### 传递pojo对象

Mybatis使用ognl表达式解析对象字段的值，#{}或者${}括号中的值为pojo属性名称。

#### 传递pojo包装对象

开发中通过pojo传递查询条件，查询条件是综合的查询条件，不仅包括用户查询条件还包括其它的查询条件（比如将用户购买商品信息也作为查询条件），这时可以使用包装对象传递输入参数。
Pojo类中包含pojo。
需求：根据文章标题查询文章信息，查询条件放到QueryVo的article属性中。

`QueryVo.java`

```java
package com.misiai.domain;

public class QueryVo {
    private Article article;

    public Article getArticle() {
        return article;
    }

    public void setArticle(Article article) {
        this.article = article;
    }
}

```

`IArticleDao.xml`

```xml
<select id="findByVo" parameterType="com.misiai.domain.QueryVo" resultType="com.misiai.domain.Article">
    <!---select * from blog_articles where title like #{title};-->
    select * from blog_articles where title like '%${article.title}%';

</select>
```

`IArticleDao.java`

```java
List<Article> findByVo(QueryVo vo);
```

`MybatisTest.java`

```java
@Test
public void testFindByVo() {
    String title = "%子%";
    Article article = new Article();
    QueryVo queryVo = new QueryVo();
    article.setTitle(title);
    queryVo.setArticle(article);
    List<Article> articles = articleDao.findByVo(queryVo);
    for (Article article1 :
            articles) {
        System.out.println(article1);
    }
    System.out.println("ok");
}
```

### Mybatis商户处结果封装

Mybatis：resultType

**以上所有的例子都是pojo类中的成员变量和xml配置文件和数据库字段名都是一样的，那如果pojo的成员变量和其他不一样呢？**

```java
package com.misiai.domain;

public class Article {
    private Integer ID;
    private String Title;
    private String Content;
    private Integer Author_id;
    private Integer Category_id;
    private String Tags;
	// .....
}

```

那在xml配置里面也修改即可

```xml
<insert id="saveArticle" parameterType="com.misiai.domain.Article">
    insert into blog_articles (Title,Content,Author_id,Category_id,Tags)
    values (#{Title},#{Content},#{Author_id},#{Category_id},#{Tags});
</insert>
```

**或在其中sql语句中起别名，也可。**

```xml
<!--配置查询所有的操作-->
<select id="findAll" resultMap="articleMap" resultType="com.misiai.domain.Article">
    select author_id as Author_id,category_id as Category_id,title as title,content as Content from blog_articles;
</select>
```

> 以上，author_id是数据库中的字段名，而Author_id是pojo类中的成员变量

或者使用resultMap

#### 输出pojo对象

#### 输出pojo列表



#### resultMap

```xml
<resultMap id="articleMap" type="com.misiai.domain.Article">
    <!--首先：配置主键-->
    <id property="ID" column="id"/>
    <!--  非主键的对应  -->
    <result property="articleTitle" column="title"/>
    <result property="articleContent" column="content"/>
    <result property="articleAuthor_id" column="author_id"/>
</resultMap>
```

> 以上只是定义
>
> articleTitle 是之前pojo对象定义的成员变量（有setter和getter），而后面column的值则是数据库中的字段名

```xml
<!--配置查询所有的操作-->
<select id="findAll" resultMap="articleMap">
    select * from blog_articles;
</select>
```

> 以上需要增加一个属性resultMap="articleMap"

## Mybatis配置文件

### properties

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<!-- mybatis 的主配置 文件-->
<configuration>
    <properties>
        <property name="driver" value="com.mysql.jdbc.Driver"/>
        <property name="url" value="jdbc:mysql://localhost:3306/my_blog?characterEncoding=UTF-8&amp;useSSL=false"/>
        <property name="username" value="root"/>
        <property name="password" value="root"/>
    </properties>
    <!--配置环境-->
    <environments default="development">
        <environment id="development">
            <!--配置事务环境-->
            <transactionManager type="JDBC"/>
            <!--配置数据源（连接池）-->
            <dataSource type="POOLED">
                <property name="driver" value="${driver}"/>
                <property name="url"
                          value="${url}"/>
                <property name="username" value="${username}"/>
                <property name="password" value="${password}"/>
            </dataSource>
        </environment>
    </environments>
    <!--指定映射文件配置的位置，-->
    <mappers>
        <!-- 路径要对，不然报错，以/分割
            该文件和mapper/*Mapper.xml文件都位于resources目录下
            注意要把.xml加上
        -->
        <mapper resource="com/misiai/dao/IArticleDao.xml"/>
    </mappers>
</configuration>
```

> 如上，增加了
>
> ```xml
> <properties>
>     <property name="driver" value="com.mysql.jdbc.Driver"/>
>     <property name="url" value="jdbc:mysql://localhost:3306/my_blog?characterEncoding=UTF-8&amp;useSSL=false"/>
>     <property name="username" value="root"/>
>     <property name="password" value="root"/>
> </properties>
> ```
>
> 然后下面使用${property name}来引用
>
> 当然，还可以：
>
> ```xml
> <properties resource="jdbc.conf"/>
> ```
>
> 但是，你就得在mybatis-config.xml的同级下，新建jdbc.conf文件
>
> 内容如下：
>
> ```ini
> driver=com.mysql.jdbc.Driver
> url=jdbc:mysql://localhost:3306/my_blog?characterEncoding=UTF-8&amp;useSSL=false
> username=root
> password=root
> ```
>
> 配置properties可以在标签内部配置连接数据库的信息。
>
> 也可以通过属性引用外部配置文件信息
>
> resource属性：常用的
>
> 用于指定配置文件的位置，是按照类路径的写法来写，并且必须存在于类路径下。
>
> url属性：
>
> 是要求按照Ur1的写法来写地址
>
> URL:Uniform Resource Locator 统一资源定位符。它是可以唯一标识一个资源的位置。
>
> 它的写法：
>
> http://localhost:8080/mybatisserver/demo1Servlet 
>
> 协议主机端口URI URI:Uniform Resource Identifier 统一资源标识符。
>
> 它是在应用中可以唯一定位一个资源的。

### typeAliases

使用typeAliases配置别名，它只能配置domain中类的别名

typeAlias用于配置别名，type属性指定的是实体类全限定类名，alias属性指定别名。

当指定了别名，就不再区分大小写。

```xml
<typeAliases>
    <typeAlias type="com.misiai.domain.Article" alias="Article"/>
</typeAliases>
```

*使用*

```xml
<select id="findById" parameterType="java.lang.Integer" resultType="Article">
    select * from blog_articles where id=#{id};
</select>
```



**package**

用于指定要配置别名的包，当指定之后，该包下的**实体类**都会注册别名，**并且类名就是别名**，不再区分大小写

```xml
<typeAliases>
    <package name="com.misiai.domain"/>
</typeAliases>
```



**mapper下的package**

```xml
<mappers>
    <!--<mapper resource="com/misiai/dao/IArticleDao.xml"/>-->
    <!--package标签是用于指定dao接口所在的包，当指定了之后就不需要在写resource或者class了-->
    <package name="com.misiai.dao"/>
</mappers>
```





> 1、mybatis中的难按池以及争务控利mybatis中连接池使用及分析mybatis事务控制的分析
> 2、mybatis基于XL配置的动态SQL语句使用
> mappers配置文件中的几个标签：
> <if>
> <where>
> <foreach>
> <sql>
> 3、mybatis中的多表操作
> 一对多
> 一对一（？）
> 多对多

## Mybatis连接池

**配置的位置：**

主配置文件mybatis-config.xml中的dataSource标签，type属性就是表示采用何种连接池方式。

**type属性的取值：**

POOLED采用传统的javax.sql.DataSource规范中的连接池，mybatis中有针对规范的实现。

UNPOOLED采用传统的获取连接的方式，虽然也实现Javax.sql.DataSource接口，但是并没有使用池的思想。

JNDI采用服务器提供的JNDI技术实现，来获取DataSource对象，不同的服务器所能拿到DataSource是不一样。

## Mybatis 标签

**IF**

```xml
<select id="findByCondition" resultType="Article" parameterType="ArticleMap">
    select * from blog_articles where 1= 1
    <if test="title!=null">
        and title = #{title}
    </if>
    <!-- 多个条件，中间用and 而不是&& -->
    <if test="author_id!=null and category_id!=null">
        and author_id = #{author_id} and category_id=#{category_id}            
    </if>
</select>
```

> 当然，上面是我们手动加了where 1=1，然后里面有`<if>`标签
>
> 我们还可以使用`<where>`标签，就不用加`where 1=1`，并且`<if>`标签里面也不用加and

**提取重复**

```xml
<sql id="select1">
    select * from blog_articles
</sql>
```

> 注意后面要不要分号的问题，要看后面有没有拼接

使用的时候，用include引入即可，refid填取定义时的id

```xml
<select id="findAll" resultType="Article">
    <include refid="select1"/>
</select>
```