# Spring-依赖注入

## 一、 产生的原因

​        在采用面向对象方法设计的软件系统中，底层实现都是由N个对象组成的，所有的对象通过彼此的合作，最终实现系统的业务逻辑。即软件系统中对象之间的耦合，对象A和对象B之间有关联，对象B又和对象C有依赖关系，这样对象和对象之间有着复杂的依赖关系，所以才有了控制反转这个理论

## 二、 什么是控制反转和依赖注入

二什么是控制反转?

1. IoC是Inversion of Control的缩写，有的翻译成“控制反转”，还有翻译成为“控制反向”或者“控制倒置”

2. 1996年，Michael Mattson在一篇有关探讨面向对象框架的文章中，首先提出了IoC 这个概念。简单来说就是把复杂系统分解成相互合作的对象，这些对象类通过封装以后，内部实现对外部是透明的，从而降低了解决问题的复杂度，而且可以灵活地被重用和扩展。IoC理论提出的观点大体是这样的：借助于“第三方”实现具有依赖关系的对象之间的解耦

3. 所谓控制反转就是应用本身不负责依赖对象的创建及维护，依赖对象的创建及维护是由外部容器负责的。 这样控制权就由应用转移到了外部容器，控制权的转移就是所谓反转

4. 依赖注入（DI）

   1. IoC的别名,2004年，Martin Fowler探讨了同一个问题，既然IoC是控制反转，那么到底是“哪些方面的控制被反转了呢？”，经过详细地分析和论证后，他得出了答案：“获得依赖对象的过程被反转了”。控制被反转之后，获得依赖对象的过程由自身管理对象变为由IoC容器主动注入。于是，他给“控制反转”取了一个更合适的名字叫做“依赖注入（Dependency Injection，DI）”。他的这个答案，实际上给出了实现IoC的方法：注入。

   2. 所谓依赖注入，就是由IoC容器在运行期间，动态地将某种依赖关系注入到对象之中。

   3. 所以，依赖注入（DI）和控制反转（IoC）是从不同的角度描述的同一件事情，就是指通过引入IoC容器，利用依赖关系注入的方式，实现对象之间的解耦

5. 依赖关系的四种情况

   1. 对象之间最弱的一种关联方式，是临时性的关联。代码中一般指由局部变量、函数参数、返回值建立的对于其他对象的调用关系

   2. 四种情况

      1. ClassA中某个方法的参数类型是ClassB； 这种情况成为耦合；

      2. ClassA中某个方法的参数类型是ClassB的一个属性； 这种情况成为紧耦合；

      3. ClassA中某个方法的实现实例化ClassB；

      4. ClassA中某个方法的返回值的类型是ClassB；

   3. 如果出现了上述四种情况之一，两个类很有可能就是“依赖”关系。 依赖关系（Dependency）：是类与类之间的连接，依赖总是单向的。依赖关系代表一个类依赖于另一个类的定义

6. 总结

   \(Dependency Injection\)和控制反转\(Inversion of Control\)是同一个概念。具体含义是:当某个角色\(可能是一个Java实例，调用者\)需要另一个角色\(另一个Java实例，被调用者\)的协助时，在 传统的程序设计过程中，通常由调用者来创建被调用者的实例。但在Spring里，创建被调用者的工作不再由调用者来完成，因此称为控制反转;创建被调用者 实例的工作通常由Spring容器来完成，然后注入调用者，因此也称为依赖注入

## 三 使用IoC的好处

1. 可维护性比较好，非常便于进行单元测试，便于调试程序和诊断故障。代码中的每一个Class都可以单独测试，彼此之间互不影响，只要保证自身的功能无误即可，这就是组件之间低耦合或者无耦合带来的好处。

2. 每个开发团队的成员都只需要关注自己要实现的业务逻辑，完全不用去关心其他人的工作进展，因为你的任务跟别人没有任何关系，你的任务可以单独测试，你的任务也不用依赖于别人的组件，再也不用扯不清责任了。所以，在一个大中型项目中，团队成员分工明确、责任明晰，很容易将一个大的任务划分为细小的任务，开发效率和产品质量必将得到大幅度的提高。

3. 可复用性好，我们可以把具有普遍性的常用组件独立出来，反复应用到项目中的其它部分，或者是其它项目，当然这也是面向对象的基本特征。显然，IoC更好地贯彻了这个原则，提高了模块的可复用性。符合接口标准的实现，都可以插接到支持此标准的模块中。

4. IoC生成对象的方式转为外置方式，也就是把对象生成放在配置文件里进行定义，这样，当我们更换一个实现子类将会变得很简单，只要修改配置文件就可以了，完全具有热插拨的特性

## 四 IoC的原理

控制反转是Spring框架的核心。其原理是基于面向对象\(OO\)设计原则的The Hollywood Principle：Don't call us, we'll call you（别找我，我会来找你的）。也就是说，所有的组件都是被动的，所有的组件初始化和调用都由容器负责。组件处在一个容器当中，由容器负责管理。简单的来讲，就是由容器控制程序之间的关系，而非传统实现中，由程序代码直接操控，即在一个类中调用另外一个类。这也就是所谓“控制反转”的概念所在：控制权由应用代码中转到了外部容器，控制权的转移，即所谓反

# 五 依赖注入的实现方式

### 5.1 构造函数注入

1. 示例代码

   ```java
   public class Person {
       private Hand hand;
       private Footer footer;
       private Head head;
       public Person(Hand hand, Footer footer, Head head) {
           this.hand = hand;
           this.footer = footer;
           this.head = head;
           }
    }
   ```

   ```java
   public class Person {
       private Hend hend;
        public Person() {
           head = new Head();
       }
   }
   ```

2. 说明

   ```
   通过Person 的构造函数，向Person 传递了一个Hand对象。
   这意味着两个对象之间的耦合变低了。
   Person类不需要知道 Hand 的具体实现，只要继承了原始 Hand 类，任何类型 Hand 都符合要求
   ```

### 5.2 setter注入

1. 示例代码

   ```java
    public class Person {
       private Hend hend;
        public Person() {
           head = new Head();
       }

       public void setHead(Head head) {
           this.head = head;
       }
   }
   }
   ```

### 5.3 接口注入

1. 示例代码

   ```java
   public class Person implements InjectFinder {
       private Head head;
   }
   ```

   ```java
   public interface InjectFinder {
       void injection(Head head);
   }
   ```

   ```
   @Test
   public void TestDo() {
      Person person = new Person();
      person.injection(new Head());
      person.doSomething();
   }
   ```

## 六、使用步骤

### 6.1、导入相应的jar包

1. 在pom.xml文件中添加

   ```xml
           <dependency>
               <groupId>org.springframework</groupId>
               <artifactId>spring-core</artifactId>
               <version>4.3.9.RELEASE</version>
           </dependency>
           <dependency>
               <groupId>org.springframework</groupId>
               <artifactId>spring-context</artifactId>
               <version>4.3.9.RELEASE</version>
           </dependency>

           <dependency>
               <groupId>org.springframework</groupId>
               <artifactId>spring-context-support</artifactId>
               <version>4.3.9.RELEASE</version>
           </dependency>
           <dependency>
               <groupId>org.springframework</groupId>
               <artifactId>spring-web</artifactId>
               <version>4.3.9.RELEASE</version>
           </dependency>

   ```

2. 相应的jar

   ![](http://opzv089nq.bkt.clouddn.com/17-7-16/66591711.jpg)

### 6.2、Spring Bean配置

#### 6.2.1、beans配置

##### 6.2.1.1、命名空间\(xmlns\)

1. 说明

   ```
   这一功能是在spring2之后引进来的，spring的容器启动时回去寻找jar包下面的META-INF，
   看里面是否有spring.schema或者是spring.handlers,
   这个handler文件里面就定义了命名空间以及处理这个命名空间的Java类
   ```

2. 完整结构图

   ![](http://opzv089nq.bkt.clouddn.com/17-7-16/34611456.jpg)

3. 说明

   1、beans

   ```
   支持声明Bean和装配Bean，是Spring最核心也是最原始的命名空间
   ```

   2、context

   ```
   为配置Spring应用上下文提供配置元素，包括自动检测和自动装配、注入非Spring直接管理的对象
   ```

   3、aop

   ```
   为声明切面以及@AspectJ注解切面提供配置元素
   ```

   4、tx

   ```
   提供声明式事务配置
   ```

   5、util

   ```
   提供各种各样的工具类，包括集合配置为Bean、支持属性占位符元素
   ```

   6、jee

   ```
   提供了与J2EE API的集成
   ```

   7、jms

   ```
   为声明了消息驱动bean提供配置元素
   ```

   8、lang

   ```
   支持配置由Groovy、JRuby或者BeanShell等脚本实现的Bean
   ```

   9、mvc

   ```
   启用Spring MVC能力，例如面向注解的控制器、视图控制和拦截器
   ```

   10、oxm

   ```
   支持由Java对象到XML的映射配置
   ```

   ​

##### 6.2.1.2 XML配置的结构

```
<beans>
    <import resource="xxx.xml"/>
    <bean id="" class=""></bean>
    <bean name="" class=""></bean>
    <alias alias="alias" name="alias" />
    <import resource="xxx.xml" />
</beans>
```

1. 说明

   1、&lt;bean&gt;标签

   ```
   主要用来进行Bean定义
   ```

   2、&lt;alias&gt;标签

   ```
   用于定义Bean别名
   ```

   3、import标签

   ```

   ```

#### 6.2.1、bean的xml配置

##### 6.2.2.1、说明

​ 在spring容器内拼凑bean叫作装配。装配bean的时候，你是在告诉容器，需要哪些bean，以及容器如何使用依赖注入将它们配合在一起

##### 6.2.2.2、配置方式

1. 通过全类名（反射）

2. 通过工厂方法（静态工厂方法 & 实例工厂方法）

3. FactoryBean

##### 6.2.2.3、IoC容器

1. BeanFactory

   ```
   IOC 容器的基本实现,BeanFactory 是 Spring 框架的基础设施，面向 Spring 本身
   ```

2. ApplicationContext

   ​ 提供了更多的高级特性. 是 BeanFactory 的子接口,ApplicationContext 面向使用 Spring 框架的开发者，几乎所有的应用场合都直接使用 ,ApplicationContext 而非底层的 BeanFactory,主要实现类

   1、ClassPathXmlApplicationContext：从 类路径下加载配置文件2、FileSystemXmlApplicationContext: 从文件系统中加载配置文件3、ConfigurableApplicationContext 扩展于 ApplicationContext，新增加两个主要方法：4、refresh\(\) 和 close\(\)， 让 ApplicationContext 具有启动、刷新和关闭上下文的能力5、ApplicationContext 在初始化上下文时就实例化所有单例的 Bean。

3. WebApplicationContext

   是专门为 WEB 应用而准备的，它允许从相对于 WEB 根目录的路径中完成初始化工作

##### 6.2.2.4、基本配置

```

```

##### 6.2.2.5、详细说明

1. id

   1、Bean 的名称,在 IOC 容器中必须是唯一的 ,代码中通过BeanFactory获取JavaBean实例时需以此作为索引名称

   2、若id没有指定，Spring 自动将权限定性类名作为 Bean 的名字

   3、id 可以指定多个名字，名字之间可用逗号、分号、或空格分隔

2. name

   1、同上，如果给bean增加别名，可以通过name属性指定一个或多个id。

3. class

   1、Java Bean 类名\(全路经\)。

4. singleton

   ```java
   用来配置 spring bean 的作用域。在spring2.0之前bean只有2种作用域即：
   singleton(单例)、non-singleton（也称 prototype）, 
   ​
   Spring2.0以后，增加了session、request、global session三种专用于Web应用程序上下文的Bean。
   因此，默认情况下Spring2.0现在有五种类型的Bean。当然，Spring2.0对 Bean的类型的设计进行了重构，
   并设计出灵活的Bean类型支持，理论上可以有无数多种类型的Bean，用户可以根据自己的需要，增加新的Bean类 型，满足实际应用需求
   ```

   1、singleton 可选值

   1. 说明

      当一个bean的 作用域设置为singleton, 那么Spring IOC容器中只会存在一个共享的bean实例，并且所有对bean的请求，只要id与该bean定义相匹配，则只会返回bean的同一实例。换言之，当把 一个bean定义设置为singleton作用域时，Spring IOC容器只会创建该bean定义的唯一实例。这个单一实例会被存储到单例缓存（singleton cache）中，并且所有针对该bean的后续请求和引用都 将返回被缓存的对象实例，这里要注意的是singleton作用域和GOF设计模式中的单例是完全不同的，单例设计模式表示一个ClassLoader中 只有一个class存在，而这里的singleton则表示一个容器对应一个bean，也就是说当一个bean被标识为singleton时 候，spring的IOC容器中只会存在一个该bean

   2. 示例代码

      ```
      <
      bean
      id
      =
      "user"
      class
      =
      "com.werner.di.bean.User"
      scope
      =
      "singleton"
      /
      >
      <
      bean
      id
      =
      "user"
      class
      =
      "com.werner.di.bean.User"
      singleton
      =
      "true"
      /
      >
      ```

   2、prototype 可选值

   1. 说明

      prototype作用域部署的bean，每一次请求（将其注入到另一个bean中，或者以程序的方式调用容器的 getBean\(\)方法）都会产生一个新的bean实例，相当与一个new的操作，对于prototype作用域的bean，有一点非常重要，那就是Spring不能对一个prototype bean的整个生命周期负责，容器在初始化、配置、装饰或者是装配完一个prototype实例后，将它交给客户端，随后就对该prototype实例不闻不问了。不管何种作用域，容器都会调用所有对象的初始化生命周期回调方法，而对prototype而言，任何配置好的析构生命周期回调方法都将不会被调用。 清除prototype作用域的对象并释放任何prototype bean所持有的昂贵资源，都是客户端代码的职责。（让Spring容器释放被singleton作用域bean占用资源的一种可行方式是，通过使用 bean的后置处理器，该处理器持有要被清除的bean的引用。）

   2. 示例代码

      ```
      <
      bean
      id
      =
      "user"
      class
      =
      "com.zw.api.bean.User"
      scope
      =
      "prototype"
      init-method
      =
      "init"
      destroy-method
      =
      "destroy"
      >
      ```

   3、request 可选值

   1. 说明

      ​ request表示该针对每一次HTTP请求都会产生一个新的bean，同时该bean仅在当前HTTP request内有效，配置实例：request、session、global session使用的时候首先要在初始化web的web.xml中做如下配置：如果你使用的是Servlet 2.4及以上的web容器，那么你仅需要在web应用的XML声明文件web.xml中增加下述ContextListener即可：

   2. 示例代码

      ```
      <
      web-app
      >
       ...
      <
      listener
      >
      <
      listener-class
      >
      org.springframework.web.context.request.RequestContextListener
      <
      /
      listener-class
      >
      <
      /
      listener
      >
       ...
      <
      /
      web-app
      >
      ```

      ```
      <
      bean
      id
      =
      "user"
      class
      =
      "com.zw.api.bean.User"
      scope
      =
      "request"
      init-method
      =
      "init"
      destroy-method
      =
      "destroy"
      >
      <
      /
      bean
      >
      ```

   4、session

   1. 说明

      session作用域表示该针对每一次HTTP请求都会产生一个新的bean，同时该bean仅在当前HTTP session内有效,和request配置实例的前提一样，配置好web启动文件就可以如下配置

   2. 示例代码

      ```
      <
      web-app
      >
       ...
      <
      listener
      >
      <
      listener-class
      >
      org.springframework.web.context.request.RequestContextListener
      <
      /
      listener-class
      >
      <
      /
      listener
      >
       ...
      <
      /
      web-app
      >
      <
      bean
      id
      =
      "user"
      class
      =
      "com.zw.api.bean.User"
      scope
      =
      "session"
      init-method
      =
      "init"
      destroy-method
      =
      "destroy"
      >
      <
      /
      bean
      >
      ```

   5、abstract

   1. 说明

      设定ApplicationContext是否对bean进行预先的初始化。

   2. 示例代码

      ```
      <
      bean
      id
      =
      "user1"
      class
      =
      "com.zw.api.bean.User"
      abstract
      =
      "true"
      scope
      =
      "session"
      init-method
      =
      "init"
      destroy-method
      =
      "destroy"
      >
      <
      /
      bean
      >
      ```

   6、parent

   7、autowire

   1. bean自动装配模式。可选5种模式

      ```
      1、no：不使用自动装配。Bean的引用必须通过ref元素定义。
      2、byName：通过属性名字进行自动装配。
      3、byType：如果BeanFactory中正好有一个同属性类型一样的bean，就自动装配这个属性。如果有多于一个这样的bean，就抛出一个致命异常，它指出你可能不能对那个bean使用byType的自动装配。如果没有匹配的bean，则什么都不会发生，属性不会被设置。如果这是你不想要的情况（什么都不发生），通过设置dependency-check="objects"属性值来指定在这种情况下应该抛出错误。
      4、constructor：这个同byType类似，不过是应用于构造函数的参数。如果在BeanFactory中不是恰好有一个bean与构造函数参数相同类型，则一个致命的错误会产生。
      5、autodetect： 通过对bean 检查类的内部来选择constructor或byType。如果找到一个缺省的构造函数，那么就会应用byType。
      ```

   2. 示例代码

      ```
      public
      class
      Application
       { 
      private
      User
      user
      ;
      public
      Application
      (
      User
      user
      ) {
      this
      .
      user
      =
      user
      ;
        }
      public
      User
      getUser
      () {
      return
      user
      ;
        }
      public
      void
      setUser
      (
      User
      user
      ) {
      this
      .
      user
      =
      user
      ;
        }
      }
      ​
      ​
      public
      class
      User
      implements
      Serializable
       {
      private
      String
      id
      ;
      private
      String
      name
      ;
      private
      String
      sex
      ;
      private
      Integer
      age
      ;
      public
      void
      destroy
      () {
      System
      .
      out
      .
      println
      (
      "销毁!"
      );
        }
      public
      void
      init
      () {
      System
      .
      out
      .
      println
      (
      "初始化!"
      );
        }
      ```

      ```
      1.根据属性名来加载
      private User user;
      <
      bean
      id
      =
      "application"
      class
      =
      " com.werner.di.Application"
      autowire
      =
      "byName"
      /
      >
      <
      bean
      id
      =
      "user_id"
      class
      =
      " com.werner.di.User"
      >
      <
      property
      name
      =
      "name"
      value
      =
      "user"
      /
      >
      <
      /
      bean
      >
      ​
      2. 根据构造类型来加载
      <
      bean
      id
      =
      "application"
      class
      =
      " com.werner.di.Application"
      autowire
      =
      "byType"
      /
      >
      <
      bean
      id
      =
      "user"
      class
      =
      " com.werner.di.User"
      >
      <
      property
      name
      =
      "name"
      value
      =
      "user"
      /
      >
      <
      /
      bean
      >
      ​
      3. 根据构造方法来加载
      public Application(User user) {
        this.user = user;
      }
      <
      bean
      id
      =
      "app"
      class
      =
      "com.werner.di.Application"
      autowire
      =
      "constructor"
      >
      <
      /
      bean
      >
      ```

   8、init-method

   1. 说明

      初始化方法,此方法将在BeanFactory创建JavaBean实例之后，在向应用层返回引用之前执行。一般用于一些资源的初始化工作。

   2. 示例代码

      ```
      public class User implements Serializable {
        public void init() {
        System.out.println("初始化");
        }
      }
      ```

      ```xml
      <
      bean
      class
      =
      "com.werner.di.User"
      name
      =
      "user"
      init-method
      =
      "init
      >
      ```

   9、destroy-method

   1. 说明:

      销毁方法,此方法将在BeanFactory销毁的时候执行，一般用于资源释放。

   2. 示例代码

      ```
      public
      class
      User
      implements
      Serializable
       {
      ​
      public
      void
      destroy
      () {
        }
      }
      ```

      ```
      <
      bean
      class
      =
      "com.werner.di.User"
      name
      =
      "user"
      init-method
      =
      "init"
      destroy-method
      =
      "destroy"
      >
      ```



