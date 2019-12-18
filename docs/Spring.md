# Spring

## 1、Spring概述

### 1.1 Spring是什么

Spring是分层的Java SE/EE应用full-stack轻量级开源框架，以IoC（Inverse Of Control：反转控制）和AOP（Aspect Oriented Programming：面向切面编程）为内核，提供了展现层Spring MWC和持久层Spring JDBC以及业务层事务管理等众多的企业级应用技术，还能整合开源世界众多著名的第三方框架和类库，逐渐成为使用最多的JavaEE企业应用开源框架。

### 1.2 Spring两大核心

Ioc和AOP

### 1.3 Spring发展历程和优势

1997年IBM提出了EJB的思想

1998年，SUN制定开袋标准规范EJB1.0

1999年，EJB1.1发布

2001年，EJB2.0发布

2003年，EJB2.1发布

2006年，EJB3.0发布

Rod Johnson（spring之父）

Expert One-to-One J2EE Design and Devflopment（2002）

阐述了J2EE使用EJB开发设计的优点及解决方案

Expert One-to-One J2EE Development without EJB（2004）

阐述了J2EE开发不使用EJB的解决方式（Spring雏形）

**2017年9月份发布了spring的最新版本spring 5.0通用版（GA）**

### 1.4 Spring架构图

![截图-1576460847](https://wimg.misiyu.cn/images/my_images/2019-12-16-1576460846801.png?x-oss-process=style/common)

## 2、程序的耦合和解耦

耦合性（Coupling），也叫耦合度，是对模块间关联程度的度量。耦合的强弱取决于模块间接口的复杂性、调用模块的方式以及通过界面传送数据的多少。模块间的耦合度是指模块之间的依赖关系，包括控制关系、调用关系、数据传递关系。模块间联系越多，其满合性越强，同时表明其独立性越差（降低耦合性，可以提高其独立性）。耦合性存在于各个领域，而非软件设计中独有的，但是我们只讨论软件工程中的耦合。
在软件工程中，耦合指的就是就是对象之间的依赖性。对象之间的耦合越高，维护成本越高。因此对象的设计应使类和构件之间的糊合最小。软件设计中通常用耦合度和内聚度作为衡量模块独立程度的标准，划分模块的一个准则就是高内聚低糊合。 

## 3、Spring中的IOC

### 3.1 基于XML的IOC环境搭建

1、`src/main/resources/bean.xml`

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

</beans>
```

## 4、依赖注入（DI）

Dependency Injection



