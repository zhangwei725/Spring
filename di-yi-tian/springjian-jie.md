# 一、简介

​ Spring 是个java企业级应用的开源开发框架。Spring主要用来开发Java应用，但是有些扩展是针对构建J2EE平台的web应用。Spring 框架目标是简化Java企业级应用开发，并通过POJO为基础的编程模型促进良好的编程习惯。

## 二、为什么要使用Spring?

* **轻量：**Spring 是轻量的，基本的版本大约2MB。

* **控制反转：**Spring通过控制反转实现了松散耦合，对象们给出它们的依赖，而不是创建或查找依赖的对象们。

* **面向切面的编程\(AOP\)：**Spring支持面向切面的编程，并且把应用业务逻辑和系统服务分开。

* **容器：**Spring 包含并管理应用中对象的生命周期和配置。

* **MVC框架**：Spring的WEB框架是个精心设计的框架，是Web框架的一个很好的替代品。

* **事务管理：**Spring 提供一个持续的事务管理接口，可以扩展到上至本地事务下至全局事务（JTA）。

* **异常处理：**Spring 提供方便的API把具体技术相关的异常（比如由JDBC，Hibernate or JDO抛出的）转化为一致的unchecked 异常。

## 三 、核心模块

### 3.1、 说明

​ Spring框架包含的功能大约由20个模块组成。这些模块按组可分为核心容器、数据访问/集成，Web，AOP\(面向切面编程\)、设备、消息和测试

### 3.2、结构图

![](http://opzv089nq.bkt.clouddn.com/17-7-15/64723358.jpg)

### 3.3、模块介绍

| GroupId | ArtifactId | 说明 |
| :--- | :--- | :--- |
| org.springframework | spring-beans | Beans 支持，包含 Groovy |
| org.springframework | spring-aop | 基于代理的AOP支持 |
| org.springframework | spring-aspects | 基于AspectJ 的切面 |
| org.springframework | spring-context | 应用上下文运行时，包括调度和远程抽象 |
| org.springframework | spring-context-support | 支持将常见的第三方类库集成到 Spring 应用上下文 |
| org.springframework | spring-core | 其他模块所依赖的核心模块 |
| org.springframework | spring-expression | Spring 表达式语言，SpEL |
| org.springframework | spring-instrument | JVM 引导的仪表（监测器）代理 |
| org.springframework | spring-instrument-tomcat | Tomcat 的仪表（监测器）代理 |
| org.springframework | spring-jdbc | 支持包括数据源设置和 JDBC 访问支持 |
| org.springframework | spring-jms | 支持包括发送/接收JMS消息的助手类 |
| org.springframework | spring-messaging | 对消息架构和协议的支持 |
| org.springframework | spring-orm | 对象/关系映射，包括对 JPA 和 Hibernate 的支持 |
| org.springframework | spring-oxm | 对象/XML 映射（Object/XML Mapping，OXM） |
| org.springframework | spring-test | 单元测试和集成测试支持组件 |
| org.springframework | spring-tx | 事务基础组件，包括对 DAO 的支持及 JCA 的集成 |
| org.springframework | spring-web | web支持包，包括客户端及web远程调用 |
| org.springframework | spring-webmvc | REST web 服务及 web 应用的 MVC 实现 |
| org.springframework | spring-webmvc-portlet | 用于 Portlet 环境的MVC实现 |
| org.springframework | spring-websocket | WebSocket 和 SockJS 实现，包括对 STOMP 的支持 |

### 3.4、 模块详解

#### 3.4.1 核心模块（core）

1. spring-core：依赖注入IoC与DI的最基本实现

2. spring-beans：Bean工厂与bean的装配

3. spring-context：spring的context上下文即IoC容器

4. spring-context-support

5. spring-expression：spring表达式语言

#### 3.4.2 核心模块说明

1. spring-core

   ```
   这个jar文件包含Spring框架基本的核心工具类，Spring其它组件要都要使用到这个包里的类，是其它组件的基本核心，
   当然你也可以在自己的应用系统中使用这些工具类
   ```

2. spring-beans 模块

   ```
   这个jar文件是所有应用都要用到的，它包含访问配置文件、创建和管理bean以及
   进行Inversion of Control / Dependency Injection（IoC/DI）操作相关的所有类。
   如果应用只需基本的IoC/DI支持，引入spring-core.jar及spring- beans.jar文件就可以了
   ```

3. spring-context 模块

   ```
   Spring核心提供了大量扩展，这样使得由 Core 和 Beans 提供的基础功能增强：
   这意味着Spring 工程能以框架模式访问对象。Context 模块继承了Beans 模块的特性并增加了对国际化（例如资源绑定）、
   事件传播、资源加载和context 透明化（例如 Servlet container）。
   同时，也支持JAVA EE 特性，例如 EJB、 JMX 和 基本的远程访问。Context 模块的关键是 ApplicationContext 接口。
   spring-context-support 则提供了对第三方库集成到 Spring-context 的支持，
   比如缓存（EhCache, Guava, JCache）、邮件（JavaMail）、调度（CommonJ, Quartz）、
   模板引擎（FreeMarker, JasperReports, Velocity）等。
   ```

4. spring-expression 模块

   ```
   为在运行时查询和操作对象图提供了强大的表达式语言。
   它是JSP2.1规范中定义的统一表达式语言的扩展，支持 set 和 get 属性值、属性赋值、方法调用、
   访问数组集合及索引的内容、逻辑算术运算、命名变量、通过名字从Spring IoC容器检索对象，还支持列表的投影、
   选择以及聚合等。
   ```

### 3.5 Data Access/Integration - 数据访问与集成

#### 3.5.1 概要

​ 数据访问与集成层包含 JDBC、ORM、OXM、JMS和事务模块。

#### 3.5.2 详细说明

1. spring-jdbc 模块

   ```
   提供了 JDBC抽象层，它消除了冗长的 JDBC 编码和对数据库供应商特定错误代码的解析。
   ```

2. spring-tx 模块

   ```
   支持编程式事务和声明式事务，可用于实现了特定接口的类和所有的 POJO 对象。
   编程式事务需要自己写beginTransaction()、commit()、rollback()等事务管理方法，
   声明式事务是通过注解或配置由 spring 自动处理，编程式事务粒度更细。
   ```

3. spring-orm 模块

   ```
   提供了对流行的对象关系映射 API的集成，包括 JPA、JDO 和 Hibernate 等。
   通过此模块可以让这些 ORM 框架和 spring 的其它功能整合，比如前面提及的事务管理。
   ```

4. spring-oxm

   ```
   模块提供了对 OXM 实现的支持，比如JAXB、Castor、XML Beans、JiBX、XStream等。
   ```

5. spring-jms

   ```
    模块包含生产（produce）和消费（consume）消息的功能。从Spring 4.1开始，集成了 spring-messaging 模块
   ```

### 3.6 AOP

1. spring-aop 模块

   ```
   提供了面向切面编程（AOP）的实现，可以定义诸如方法拦截器和切入点等，从而使实现功能的代码彻底的解耦。
   使用源码级的元数据。
   ```

2. spring-aspects 模块

   ```
   提供了对 AspectJ 的集成
   ```

### 3.7 Instrumentation

1. spring-instrument

   ```
   模块提供了对检测类的支持和用于特定的应用服务器的类加载器的实现。
   ```

2. spring-instrument-tomcat

   ```
    模块包含了用于 Tomcat 的Spring 检测代理。
   ```

### 3.8 Messaging - 消息处理

1. spring-messaging 模块

```
从 Spring 4 开始集成,从一些 Spring 集成项目的关键抽象中提取出来的，
这些项目包括 Message、MessageChannel、MessageHandler 
和其它服务于消息处理的项目。这个模块也包含一系列的注解用于映射消息到方法
```

### 3.9 Web

#### 3.9.1 概要

​ Web 层包括 spring-web、spring-webmvc、spring-websocket、spring-webmvc-portlet 等模块。

#### 3.9.2 详细说明

1. spring-web 模块

   ```
   提供面向 web 的基本功能和面向 web 的应用上下文，比如 multipart 文件上传功能、
   使用 Servlet 监听器初始化 IoC 容器等。
   它还包括 HTTP 客户端以及 Spring 远程调用中与 web 相关的部分
   ```

2. spring-webmvc 模块

   ```
   为 web 应用提供了模型视图控制（MVC）和 REST Web 服务的实现。
   Spring 的 MVC 框架可以使领域模型代码和 web 表单完全地分离，且可以与 Spring 框架的其它所有功能进行集成
   ```

3. spring-webmvc-portlet 模块

   ```
   （即Web-Portlet模块）提供了用于 Portlet 环境的 MVC 实现，并反映了 pring-webmvc 模块的功能
   ```

### 3.10 Test

1. spring-test 模块

   ```
   通过 JUnit 和 TestNG 组件支持单元测试和集成测试。
   它提供了一致性地加载和缓存 Spring 上下文，也提供了用于单独测试代码的模拟对象（mock object）
   ```

Spring包依赖说明:

1. spring-core.jar依赖commons-collections.jar，spring-core.jar。

2. spring-beans.jar依赖 spring-core.jar，cglib-nodep.jar

3. spring-aop.jar依赖spring-core.jar，spring-beans.jar，cglib-nodep.jar，aopalliance.jar

4. spring-context.jar依赖spring-core.jar，spring-beans.jar，spring-aop.jar，commons-collections.jar，aopalliance.jar

5. spring-dao.jar依赖spring-core.jar，spring-beans.jar，spring-aop.jar，spring-context.jar

6. spring-jdbc.jar依赖spring-core.jar，spring-beans.jar，spring-dao.jar

7. spring-web.jar依赖spring-core.jar，spring-beans.jar，spring-context.jar

8. spring-webmvc.jar依赖spring-core.jar/spring-beans.jar/spring-context.jar/spring-web.jar

9. spring -hibernate.jar依赖spring-core.jar，spring-beans.jar，spring-aop.jar，spring- dao.jar，spring-jdbc.jar，spring-orm.jar，spring-web.jar，spring-webmvc.jar

10. spring-orm.jar依赖spring-core.jar，spring-beans.jar，spring-aop.jar，spring- dao.jar，spring-jdbc.jar，spring-web.jar，spring-webmvc.jar

11. spring -remoting.jar依赖spring-core.jar，spring-beans.jar，spring-aop.jar，spring- dao.jar，spring-context.jar，spring-web.jar，spring-webmvc.jar

12. spring-support.jar依赖spring-core.jar，spring-beans.jar，spring-aop.jar，spring-dao.jar，spring-context.jar，spring-jdbc.jar

13. spring-mock.jar依赖spring-core.jar，spring-beans.jar，spring-dao.jar，spring-context.jar，spring-jdbc.jar

[下载地址](http://repo.spring.io/release/org/springframework/spring)

