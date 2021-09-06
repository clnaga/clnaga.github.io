---
layout: mypost
title: Java Spring
categories: [Java]
---



### 为什么要使用 Spring？

**1.简介**

- 目的：解决企业应用开发的复杂性
- 功能：使用基本的JavaBean代替EJB，并提供了更多的企业应用功能
- 范围：任何Java应用

简单来说，Spring是一个轻量级的控制反转(IoC)和面向切面(AOP)的容器框架。

**2.轻量**　　

从大小与开销两方面而言Spring都是轻量的。完整的Spring框架可以在一个大小只有1MB多的JAR文件里发布。并且Spring所需的处理开销也是微不足道的。此外，Spring是非侵入式的：典型地，Spring应用中的对象不依赖于Spring的特定类。

**3.控制反转**　　

Spring通过一种称作控制反转（IoC）的技术促进了松耦合。当应用了IoC，一个对象依赖的其它对象会通过被动的方式传递进来，而不是这个对象自己创建或者查找依赖对象。你可以认为IoC与JNDI相反——不是对象从容器中查找依赖，而是容器在对象初始化时不等对象请求就主动将依赖传递给它。

**4.面向切面**　　

Spring提供了面向切面编程的丰富支持，允许通过分离应用的业务逻辑与系统级服务（例如审计（auditing）和事务（transaction）管理）进行内聚性的开发。应用对象只实现它们应该做的——完成业务逻辑——仅此而已。它们并不负责（甚至是意识）其它的系统级关注点，例如日志或事务支持。

**5.容器**

Spring包含并管理应用对象的配置和生命周期，在这个意义上它是一种容器，你可以配置你的每个bean如何被创建——基于一个可配置原型（prototype），你的bean可以创建一个单独的实例或者每次需要时都生成一个新的实例——以及它们是如何相互关联的。然而，Spring不应该被混同于传统的重量级的EJB容器，它们经常是庞大与笨重的，难以使用。

**6.框架**

Spring可以将简单的组件配置、组合成为复杂的应用。在Spring中，应用对象被声明式地组合，典型地是在一个XML文件里。Spring也提供了很多基础功能（事务管理、持久化框架集成等等），将应用逻辑的开发留给了你。

所有Spring的这些特征使你能够编写更干净、更可管理、并且更易于测试的代码。它们也为Spring中的各种模块提供了基础支持。

> [接近8000字的Spring/SpringBoot常用注解总结](https://segmentfault.com/a/1190000022521844){:target="_blank"}

### 解释一下什么是 AOP？

AOP（Aspect-Oriented Programming，面向切面编程），可以说是OOP（Object-Oriented Programing，面向对象编程）的补充和完善。OOP引入封装、继承和多态性等概念来建立一种对象层次结构，用以模拟公共行为的一个集合。当我们需要为分散的对象引入公共行为的时候，OOP则显得无能为力。也就是说，OOP允许你定义从上到下的关系，但并不适合定义从左到右的关系。例如日志功能。日志代码往往水平地散布在所有对象层次中，而与它所散布到的对象的核心功能毫无关系。对于其他类型的代码，如安全性、异常处理和透明的持续性也是如此。这种散布在各处的无关的代码被称为横切（cross-cutting）代码，在OOP设计中，它导致了大量代码的重复，而不利于各个模块的重用。

而AOP技术则恰恰相反，它利用一种称为“横切”的技术，剖解开封装的对象内部，并将那些影响了多个类的公共行为封装到一个可重用模块，并将其名为“Aspect”，即切面。所谓“切面”，简单地说，就是将那些与业务无关，却为业务模块所共同调用的逻辑或责任封装起来，便于减少系统的重复代码，降低模块间的耦合度，并有利于未来的可操作性和可维护性。AOP代表的是一个横向的关系，如果说“对象”是一个空心的圆柱体，其中封装的是对象的属性和行为；那么面向方面编程的方法，就仿佛一把利刃，将这些空心圆柱体剖开，以获得其内部的消息。而剖开的切面，也就是所谓的“方面”了。然后它又以巧夺天功的妙手将这些剖开的切面复原，不留痕迹。

使用“横切”技术，AOP把软件系统分为两个部分：核心关注点和横切关注点。业务处理的主要流程是核心关注点，与之关系不大的部分是横切关注点。横切关注点的一个特点是，他们经常发生在核心关注点的多处，而各处都基本相似。比如权限认证、日志、事务处理。Aop 的作用在于分离系统中的各种关注点，将核心关注点和横切关注点分离开来。正如Avanade公司的高级方案构架师Adam Magee所说，AOP的核心思想就是“将应用程序中的商业逻辑同对其提供支持的通用服务进行分离。”

> [Spring AOP的底层原理](https://www.jianshu.com/p/f8ed74827d71)

### 解释一下什么是 IoC？

IoC是Inversion of Control的缩写，多数书籍翻译成“控制反转”。

1996年，Michael Mattson在一篇有关探讨面向对象框架的文章中，首先提出了IoC 这个概念。对于面向对象设计及编程的基本思想，前面我们已经讲了很多了，不再赘述，简单来说就是把复杂系统分解成相互合作的对象，这些对象类通过封装以后，内部实现对外部是透明的，从而降低了解决问题的复杂度，而且可以灵活地被重用和扩展。　

IoC理论提出的观点大体是这样的：借助于“第三方”实现具有依赖关系的对象之间的解耦。如下图：

![IoC1](IoC1.jpg)

由于引进了中间位置的“第三方”，也就是IoC容器，使得A、B、C、D这4个对象没有了耦合关系，齿轮之间的传动全部依靠“第三方”了，全部对象的控制权全部上缴给“第三方”IoC容器，所以，IoC容器成了整个系统的关键核心，它起到了一种类似“粘合剂”的作用，把系统中的所有对象粘合在一起发挥作用，如果没有这个“粘合剂”，对象与对象之间会彼此失去联系，这就是有人把IoC容器比喻成“粘合剂”的由来。

我们再来做个试验：把上图中间的IoC容器拿掉，然后再来看看这套系统：

![IoC2](IoC2.jpg)

我们现在看到的画面，就是我们要实现整个系统所需要完成的全部内容。这时候，A、B、C、D这4个对象之间已经没有了耦合关系，彼此毫无联系，这样的话，当你在实现A的时候，根本无须再去考虑B、C和D了，对象之间的依赖关系已经降低到了最低程度。所以，如果真能实现IoC容器，对于系统开发而言，这将是一件多么美好的事情，参与开发的每一成员只要实现自己的类就可以了，跟别人没有任何关系！

我们再来看看，控制反转(IoC)到底为什么要起这么个名字？我们来对比一下：

软件系统在没有引入IoC容器之前，如图1所示，对象A依赖于对象B，那么对象A在初始化或者运行到某一点的时候，自己必须主动去创建对象B或者使用已经创建的对象B。无论是创建还是使用对象B，控制权都在自己手上。

软件系统在引入IoC容器之后，这种情形就完全改变了，如图3所示，由于IoC容器的加入，对象A与对象B之间失去了直接联系，所以，当对象A运行到需要对象B的时候，IoC容器会主动创建一个对象B注入到对象A需要的地方。

通过前后的对比，我们不难看出来：对象A获得依赖对象B的过程,由主动行为变为了被动行为，控制权颠倒过来了，这就是“控制反转”这个名称的由来。

### Spring Bean 生命周期

Spring 框架中的 Bean 经过四个阶段：实例化 -> 属性赋值 -> 初始化 -> 销毁

1. 实例化：new xxx(); 

   两个时机：当客户端向容器申请一个 Bean 时；当容器在初始化一个 Bean 时发现还需要依赖另一个 Bean（利用 BeanDefinition 反射实例化一个对象）

2. 设置对象属性（依赖注入）：Spring 通过 BeanDefinition 找到对象依赖的其他对象，并将这些对象赋予当前对象

3. 处理 Aware 接口：Spring 会检测对象是否实现了 xxxAware 接口，如果实现了，就会调用对应的方法：BeanNameAware、BeanClassLoaderAware、BeanFactoryAware、ApplicationContextAware

   > Aware 是一个具有标识作用的超级接口，实现该接口的 Bean 是具有被Spring 容器通知的能力的，而被通知的方式就是通过回调。也就是说：直接或间接实现了这个接口的类，都具有被 Spring 容器通知的能力。Spring Aware 的目的是为了让 Bean 获得 Spring 容器的服务。

4. BeanPostProcessor 前置处理

5. InitializingBean：Spring 检测对象如果实现了这个接口，会执行它的 afterPropertiesSet() 方法，定制初始化逻辑

6. init-method：<bean init-method=xxx> 如果 Spring 发现 Bean 配置了这个属性，会调用它的配置方法，执行初始化逻辑。注解 @PostConstruct

7. BeanPostProcessor 后置处理

   > 到这里 Bean 的创建过程就完成了，Bean 可用正常使用了

8. DisposableBean：当 Bean 实现了这个接口，在对象销毁时会调用 destroy() 方法

9. destroy-method：<bean destroy-method=xxx> @PreDestroy 如果这个 Bean 的 Spring 配置中配置了 destroy-method 属性，会自动调用其配置的销毁方法

### Spring 常用的注入方式有哪些？

Spring通过DI（依赖注入）实现IoC（控制反转），常用的注入方式主要有三种：

1. 构造方法注入
2. setter注入
3. 基于注解的注入

### Spring 自动装配 bean 有哪些方式？

Spring容器负责创建应用程序中的bean同时通过ID来协调这些对象之间的关系。作为开发人员，我们需要告诉Spring要创建哪些bean并且如何将其装配到一起。

Spring中bean装配有两种方式：

- 隐式的bean发现机制和自动装配
- 在java代码或者XML中进行显示配置

当然这些方式也可以配合使用。

### Spring 中的 bean 是线程安全的吗？

Spring容器中的Bean是否线程安全，容器本身并没有提供Bean的线程安全策略，因此可以说Spring容器中的Bean本身不具备线程安全的特性，但是具体还是要结合具体scope的Bean去研究。

### Spring 支持几种 bean 的作用域？

当通过Spring容器创建一个Bean实例时，不仅可以完成Bean实例的实例化，还可以为Bean指定特定的作用域。Spring支持如下5种作用域：

- singleton：单例模式，在整个Spring IoC容器中，使用singleton定义的Bean将只有一个实例
- prototype：原型模式，每次通过容器的getBean方法获取prototype定义的Bean时，都将产生一个新的Bean实例
- request：对于每次HTTP请求，使用request定义的Bean都将产生一个新实例，即每次HTTP请求将会产生不同的Bean实例。只有在Web应用中使用Spring时，该作用域才有效
- session：对于每次HTTP Session，使用session定义的Bean都将产生一个新实例。同样只有在Web应用中使用Spring时，该作用域才有效
- globalsession：每个全局的HTTP Session，使用session定义的Bean都将产生一个新实例。典型情况下，仅在使用portlet context的时候有效。同样只有在Web应用中使用Spring时，该作用域才有效

其中比较常用的是singleton和prototype两种作用域。对于singleton作用域的Bean，每次请求该Bean都将获得相同的实例。容器负责跟踪Bean实例的状态，负责维护Bean实例的生命周期行为；如果一个Bean被设置成prototype作用域，程序每次请求该id的Bean，Spring都会新建一个Bean实例，然后返回给程序。在这种情况下，Spring容器仅仅使用new 关键字创建Bean实例，一旦创建成功，容器不在跟踪实例，也不会维护Bean实例的状态。

如果不指定Bean的作用域，Spring默认使用singleton作用域。Java在创建Java实例时，需要进行内存申请；销毁实例时，需要完成垃圾回收，这些工作都会导致系统开销的增加。因此，prototype作用域Bean的创建、销毁代价比较大。而singleton作用域的Bean实例一旦创建成功，可以重复使用。因此，除非必要，否则尽量避免将Bean被设置成prototype作用域。

### Spring 事务实现方式有哪些？

1. 编程式事务管理对基于 POJO 的应用来说是唯一选择。我们需要在代码中调用beginTransaction()、commit()、rollback()等事务管理相关的方法，这就是编程式事务管理。
2. 基于 TransactionProxyFactoryBean 的声明式事务管理
3. 基于 @Transactional 的声明式事务管理
4. 基于 Aspectj AOP 配置事务

### 说一下 Spring 的事务隔离？

事务隔离级别指的是一个事务对数据的修改与另一个并行的事务的隔离程度，当多个事务同时访问相同数据时，如果没有采取必要的隔离机制，就可能发生以下问题：

- 脏读：一个事务读到另一个事务未提交的更新数据。
- 幻读：例如第一个事务对一个表中的数据进行了修改，比如这种修改涉及到表中的“全部数据行”。同时，第二个事务也修改这个表中的数据，这种修改是向表中插入“一行新数据”。那么，以后就会发生操作第一个事务的用户发现表中还存在没有修改的数据行，就好象发生了幻觉一样。
- 不可重复读：比方说在同一个事务中先后执行两条一模一样的select语句，期间在此次事务中没有执行过任何DDL语句，但先后得到的结果不一致，这就是不可重复读。

### Spring MVC 介绍

SpringMVC 是 Spring 对 Web 框架的一个解决方案。Spring 的模型-视图-控制器（MVC）提供了一个总的前端控制器 Servlet，用来接受请求，然后定义了一套路由策略（url 到 handler 的映射）及适配执行 handler，将 handler 结果使用视图解析技术生成视图展示给前端

### Spring MVC 工作流程

1. 用户请求：用户发送请求到前端控制器 DispatcherServlet
2. 寻找处理器：DispatcherServlet 收到请求调用 HandlerMapping 处理器映射器
3. 调用处理器：DispatcherServlet 调用 HandlerAdapter 处理器适配器
4. 处理请求：HandlerAdapter 经过适配器调用具体的处理器处理请求（Controller，也叫后端控制器）
5. 返回 ModelAndView：Controller 执行完成返回 ModelAndView
6. 处理视图映射：DispatcherServlet 将 ModelAndView 传给 ViewReslover 视图解析器，找到ModelAndView指定的视图
7. 响应用户：DispatcherServlet 根据 View 进行渲染视图（将模型数据填充到视图中），并响应用户

![SpringMVC流程](SpringMVC流程.png)

待补充：https://mp.weixin.qq.com/s/eHK5wqAv5UgYoYUnpFCxzA

### 什么是 Spring boot？

在Spring框架这个大家族中，产生了很多衍生框架，比如 Spring、SpringMMC框架等，Spring的核心内容在于控制反转(IoC)和依赖注入(DI),所谓控制反转并非是一种技术，而是一种思想，在操作方面是指在Spring配置文件中创建<bean>，依赖注入即为由Spring容器为应用程序的某个对象提供资源，比如 引用对象、常量数据等。

SpringBoot是一个框架，一种全新的编程规范，他的产生简化了框架的使用，所谓简化是指简化了Spring众多框架中所需的大量且繁琐的配置文件，所以 SpringBoot是一个服务于框架的框架，服务范围是简化配置文件。

### 为什么要用 Spring boot？

- Spring Boot使编码变简单
- Spring Boot使配置变简单
- Spring Boot使部署变简单
- Spring Boot使监控变简单
- Spring的不足

### Spring boot 核心配置文件是什么？

Spring Boot提供了两种常用的配置文件：

- properties文件
- yml文件

### Spring Boot 自动装配原理

**什么是 Spring Boot 自动装配**

SpringBoot 定义了一套接口规范，在 SpringBoot 启动时会扫描外部引用 jar 包中的 spring.factories 文件，将文件中配置的类型信息加载到 Spring 容器中，并执行类中定义的各种操作。对于外部 jar 包来说，只需要按照 SpringBoot 定义的标准，就能将自己的功能装置进SpringBoot 中

**SpringBoot 是如何实现自动装配**

通过注解或者一些简单的配置就能在 Spring Boot 的帮助下实现某块功能

> 1. [面试常问：“讲述一下 SpringBoot 自动装配原理？”](https://www.cnblogs.com/javaguide/p/springboot-auto-config.html){:target="_blank"}

### Spring / SpringBoot 常用注解

1. `@SpringBootApplication`

   > 这个注解是 SpringBoot 项目的基石，创建 SpringBoot 项目之后会默认在主类上
   >
   > 可以看作是 `@Configuration`、`@EnableAutoConfiguration`、`@ComponentScan` 注解的集合
   >
   > - `@Configuration`：允许在 Spring 上下文中注册额外的 bean 或导入其他配置类
   >
   > - `@EnableAutoConfiguration`：启用 SpringBoot 的自动配置机制
   > - `@ComponentScan`： 扫描被`@Component` (`@Service`,`@Controller`)注解的 bean，注解默认会扫描该类所在的包下所有的类。

2. Spring Bean 相关

   1. `@Autowired`

      > 自动导入对象到类中，被注入进的类同样要被 Spring 容器管理比如：Service 类注入到 Controller 类中
      >
      > ```java
      > @Service
      > public class UserService {
      >   ......
      > }
      > 
      > @RestController
      > @RequestMapping("/users")
      > public class UserController {
      >    @Autowired
      >    private UserService userService;
      >    ......
      > }
      > ```

   2. `@Component`,`@Repository`,`@Service`, `@Controller`

      > 我们一般使用 `@Autowired` 注解让 Spring 容器帮我们自动装配 bean。要想把类标识成可用于 `@Autowired` 注解自动装配的 bean 的类,可以采用以下注解实现
      >
      > - `@Component` ：通用的注解，可标注任意类为 `Spring` 组件。如果一个 Bean 不知道属于哪个层，可以使用`@Component` 注解标注。
      > - `@Repository` : 对应持久层即 Dao 层，主要用于数据库相关操作。
      > - `@Service` : 对应服务层，主要涉及一些复杂的逻辑，需要用到 Dao 层。
      > - `@Controller` : 对应 Spring MVC 控制层，主要用于接受用户请求并调用 Service 层返回数据给前端页面

   3. `@RestController`

      > `@RestController`注解是`@Controller和`@`ResponseBody`的合集,表示这是个控制器 bean,并且是将函数的返回值直 接填入 HTTP 响应体中,是 REST 风格的控制器

   4. `@Scope`

      > ```java
      > @Bean
      > @Scope("singleton")
      > public Person personSingleton() {
      >     return new Person();
      > }
      > ```
      >
      > **常见的 Spring Bean 的作用域：**
      >
      > - singleton : 唯一 bean 实例，Spring 中的 bean 默认都是单例的。
      > - prototype : 每次请求都会创建一个新的 bean 实例。
      > - request : 每一次 HTTP 请求都会产生一个新的 bean，该 bean 仅在当前 HTTP request 内有效。
      > - session : 每一次 HTTP 请求都会产生一个新的 bean，该 bean 仅在当前 HTTP session 内有效。

   5. `@Configuration`

      > 一般用来声明配置类，可以使用 `@Component`注解替代，不过使用`@Configuration`注解声明配置类更加语义化
      >
      > ```java
      > @Configuration
      > public class AppConfig {
      >     @Bean
      >     public TransferService transferService() {
      >         return new TransferServiceImpl();
      >     }
      > 
      > }
      > ```

3.  处理常见的 HTTP 请求类型

   **5 种常见的请求类型:**

   - **GET** ：请求从服务器获取特定资源。举个例子：`GET /users`（获取所有学生）

     ```java
     @GetMapping("/users")
     public ResponseEntity<List<User>> getAllUsers() {
     	return userRepository.findAll();
     }
     ```

   - **POST** ：在服务器上创建一个新的资源。举个例子：`POST /users`（创建学生）

     ```java
     @PostMapping("/users")
     public ResponseEntity<User> createUser(@Valid @RequestBody UserCreateRequest userCreateRequest) {
      	return userRespository.save(user);
     }
     ```

   - **PUT** ：更新服务器上的资源（客户端提供更新后的整个资源）。举个例子：`PUT /users/12`（更新编号为 12 的学生）

     ```java
     @PutMapping("/users/{userId}")
     public ResponseEntity<User> updateUser(@PathVariable(value = "userId") Long userId,
       @Valid @RequestBody UserUpdateRequest userUpdateRequest) {
       	......
     }
     ```

   - **DELETE** ：从服务器删除特定的资源。举个例子：`DELETE /users/12`（删除编号为 12 的学生）

     ```java
     @DeleteMapping("/users/{userId}")
     public ResponseEntity deleteUser(@PathVariable(value = "userId") Long userId){
       	......
     }
     ```

   - **PATCH** ：更新服务器上的资源（客户端提供更改的属性，可以看做作是部分更新），使用的比较少，这里就不举例子了。

     ```java
     @PatchMapping("/profile")
       public ResponseEntity updateStudent(@RequestBody StudentUpdateRequest studentUpdateRequest){
           studentRepository.updateDetail(studentUpdateRequest);
           return ResponseEntity.ok().build();
       }
     ```

4. 前后端传值

   1. `@PathVariable` 和 `@RequestParam`
   2. `@RequestBody`

5. 读取配置信息

   数据源 `application.yml`:

   ```yaml
   wuhan2020: 2020年初武汉爆发了新型冠状病毒，疫情严重，但是，我相信一切都会过去！武汉加油！中国加油！
   
   my-profile:
     name: Guide哥
     email: koushuangbwcx@163.com
   
   library:
     location: 湖北武汉加油中国加油
     books:
       - name: 天才基本法
         description: 二十二岁的林朝夕在父亲确诊阿尔茨海默病这天
       - name: 时间的秩序
         description: 为什么我们记得过去，而非未来？时间“流逝”意味着什么？
       - name: 了不起的我
         description: 如何养成一个新习惯？如何让心智变得更成熟？
   ```

   1. `@value`

      ```java
      @Value("${wuhan2020}")
      String wuhan2020;
      ```

   2. `@ConfigurationProperties`

      ```java
      @Component
      @ConfigurationProperties(prefix = "library")
      class LibraryProperties {
          @NotEmpty
          private String location;
          private List<Book> books;
      
          @Setter
          @Getter
          @ToString
          static class Book {
              String name;
              String description;
          }
        省略getter/setter
        ......
      }
      ```

> [Spring/Spring Boot 常用注解总结！安排！](https://github.com/Snailclimb/JavaGuide/blob/master/docs/system-design/framework/spring/SpringBoot+Spring常用注解总结.md){:target="_blank"}

### Spring Cloud 待补充

https://mp.weixin.qq.com/s/UscOEtOBq5qjy1-SJLYtaw

> Reference:
>
> + https://mp.weixin.qq.com/s/UscOEtOBq5qjy1-SJLYtaw