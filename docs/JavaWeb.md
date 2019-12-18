# Java Web

## 基础

### 目录

![截图-1573133140](https://wimg.misiyu.cn/images/20191107/1573133140_e3f537f8dc2a960.png?x-oss-process=style/common)



## IDEA与Tomcat

- IDEA会为每一个tomcat部署的项目单独建立一份配置文件。

  > C:\Users\Kuan\.IntelliJIdea2019.2\system\tomcat

- 工作空间项目和tomcat部署的web项目

  - tomcat真正访问的是“tomcat部署的web项目”，“tomcat部署的web项目“对应着”工作空间项目”的web目录下的所有资源
  - **WEB-INF目录下的资源不能被浏览器直接访问**
  - 断点调试

## Servelet

Servelet：server applet

需要用到的包：

### 概念

- Servlet就是一个接口，定义了Java类被浏览器访问到（tomcat识别）的规则。
- 捋来我们自定义一个类，I实现Servlet接口，复写方法。

### 快速入门

**实现接口**

A. 新建类

```java
public class FirstServlet implements Servlet {
    @Override
    public void init(ServletConfig servletConfig) throws ServletException {
        
    }

    @Override
    public ServletConfig getServletConfig() {
        return null;
    }
	
    // 主要在此方法内打印一句话
    @Override
    public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws ServletException, IOException {

    }

    @Override
    public String getServletInfo() {
        return null;
    }

    @Override
    public void destroy() {

    }
}
```

B. 在web.xml 配置

```xml
<!--    配置servlet-->
<servlet>
    <servlet-name>demo</servlet-name>
    <servlet-class>com.misiai.demo.FirstServlet</servlet-class>
    <!--    tomcat将全类名对应的字节码文件加成进内存。-->
</servlet>
<servlet-mapping>
    <servlet-name>demo</servlet-name>
    <url-pattern>/demo</url-pattern>
</servlet-mapping>
```

![截图-1573134032](https://wimg.misiyu.cn/images/20191107/1573134023_efa8bd776036d59.png?x-oss-process=style/common)

![截图-1573135472](https://wimg.misiyu.cn/images/20191107/1573135472_cbf62ab7f48a560.png?x-oss-process=style/common)

C. 执行原理

1.当服务器接受到客户端浏览器的请求后，会解析请求URL路径，获取访问的Servlet的资源路径
2.查找web.xml文件，是否有对应的`<url-pattern>`标签体内容。
3.如果有，则在找到对应的`<servlet-class>`全类名
4.tomcat会捋字节码文件加载进内存，并且创建其对象
5.调用其方法



**生命周期方法**

1. init 初始化方法 【**服务器**创建时执行 一次，和destroy对应】

   - 什么时候被创建？

     - 默认情况下，第一次被访问时，Servlet被创建

     - 可以配置执行Servlet的创建时机。

       ```xml
       <servlet>
           <servlet-name>demo02</servlet-name>
           <servlet-class>com.misiai.demo.ServletDemo2</servlet-class>
               <!--        指定Servlet创建时期
                   1.第一次被访问时，创建
                       <1oad-on-startup>的值为负数
                   2.在服务器启动时，创建
                       <1oad-on-startup>的值为0或正整数
               -->
           <load-on-startup>1</load-on-startup>
       </servlet>
       ```

   - servlet的init方法，只执行一次，说明一个servlet在内存中只存在一个对象，servlet是单例的。

     - 多个用户同时访问时，可能存在线程安全问题。
     - 解决：尽量不要在servlet中定义成员变量。即使定义了成员变量，也不要对修改值。

   

2. service 提供服务的方法 【每一次servlet被访问执行】

   - 每次访问servlet时，service方法都会被调用一次。

3. destroy 销毁方法 【**服务器**关闭时执行一次】

   - Servlet被销毁时执行。服务器关闭时，Servlet被销毁。
   - 只有**服务器正常关闭**时，才会执行destroy方法。
   - destroy方法在Servlet被销毁之前执行，一般用于释放资源。

   

### 注解方式

**步骤：**

- 定义一个类，在类上实现Servlet接口

- 复写方法

- 在类上使用@WebServlet注解，进行配置。

  ```java
  // 在下面注解
  @WebServlet(urlPatterns = "/demo03")
  public class ServletDemo03 implements Servlet {
  }
  ```

### 体系结构

| 说明           | 接口   |
| -------------- | ------ |
| GenericServlet | 抽象类 |
| HttpServlet    | 抽象类 |

**GenericServlet：**将sprvlet接口中其他的方法做了默认空实现，只将service()方法作为抽象，特来定义servlet类时，可以继承Genericservlet，实现service())方法即可

```java
@WebServlet(urlPatterns = "/demo04")
public class ServletDemo04 extends GenericServlet {
    @Override
    public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws ServletException, IOException {
        System.out.println("service demo04");
    }
}
```

**HttpServlet：**对http协议的一种封装，简化操作

1.定义类继承HttpServlet
2.复写doGet/doPost方法

```java
@WebServlet(urlPatterns = "/demo05")
public class ServletDemo05 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // super.doGet(req, resp);
        System.out.println("echo Hello HttpServlet");
    }
}
```

### 相关配置

1. urlpartten:servlet访问路径
   - 一个servlet可以定义多个访问路径：@uebservlet（{"/d4"，"/dd4"，"/ddd4"}）
2. 路径定义规则：
   - /xxxx
   - /xxxx.xxx
   - *.do

## Request

**request对象和response对象的原理**

1. request和response对象是由服务器创建的。我们来使用它们
2. request对象是来获取请求消息，response对象是来设i响应消息



**request：对象继承体系结构**

ServletRequest - 接口

HttpServletRequest - 接口

org.apache.catalina.connector.RequestFacade - 类（tomcat）

**request：功能**

1. 获取请求信息功能
   1. 获取请求行数据
   2. 获取请求头数据
   3. 获取请求体数据
2. 其他功能