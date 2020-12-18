# Spring5

## 一、IOC

### 1.1 概念和原理

#### 1.1.1 什么是 IOC 

- 控制反转，把对象创建和对象之间的调用过程，交给 Spring 进行管理
- 使用 IOC 目的：为了耦合度降低
- 做入门案例就是 IOC 实现



#### 1.1.2 底层原理

- xml 解析、工厂模式、反射

  ![image-20201120094422098](C:\Users\魏汉鹏\AppData\Roaming\Typora\typora-user-images\image-20201120094422098.png)



### 1.2 Bean管理

#### 1.2.1 Bean管理

​	**Bean 管理指的是两个操作** ：

- Spring 创建对象
- Spirng 注入属性

​    **Bean 管理操作有两种方：** 

- 基于 xml 配置文件方式实现
- 基于注解方式实现



#### 1.2.2 基于xml方式实现Bean管理

##### 1.2.2.1 基于xml创建对象

```xml
<!--配置User对象的创建-->
<bean id="user" class="com.weihp.spring5.User"></bean>
```

1、在 spring 配置文件中，使用 bean 标签，标签里面添加对应属性，就可以实现对象创建

2、在 bean 标签有很多属性，介绍常用的属性：

* id 属性：唯一标识
* class 属性：类全路径（包类路径）

3、创建对象时候，默认也是执行无参数构造方法完成对象创建



##### 1.2.2.2 属性注入

**1、使用 set 方法注入**

```java
/**
* 演示使用 set 方法进行注入属性
*/
public class Book { 
    //创建属性 
    private String bname; 
    private String bauthor; 
    //创建属性对应的 set 方法 
    public void setBname(String bname) { 
        this.bname = bname; 
    } 
    public void setBauthor(String bauthor) { 
        this.bauthor = bauthor; 
    } 
}
```

```xml
<!-- set 方法注入属性-->
<bean id="book" class="com.atguigu.spring5.Book">
    <!--使用 property 完成属性注入
     name：类里面属性名称
     value：向属性注入的值
     -->
    <property name="bname" value="易筋经"></property>
    <property name="bauthor" value="达摩老祖"></property>
</bean>
```

**2、使用 有参构造 进行注入**

```java
/**
* 使用 有参构造 注入
*/
public class Orders {
    //属性
    private String oname;
    private String address;
    //有参数构造
    public Orders(String oname,String address) {
        this.oname = oname;
        this.address = address;
    }
}
```

```xml
<!-- 有参数构造注入属性-->
<bean id="orders" class="com.atguigu.spring5.Orders">
    <constructor-arg name="oname" value="电脑"></constructor-arg>
    <constructor-arg name="address" value="China"></constructor-arg>
</bean>
```



##### 1.2.2.3 字面量（注入特殊的值）

**1、null值**

```xml
<!--null 值-->
<property name="address">
    <null/>
</property>
```

**2、属性值包含特殊符号**

```xml
<!--属性值包含特殊符号
 1 把<>进行转义 &lt; &gt;
 2 把带特殊符号内容写到 CDATA
-->
<property name="address">
    <value><![CDATA[<<南京>>]]></value>
</property>
```



##### 1.2.2.4 注入外部bean

```java
/**
*（1）创建两个类 service 类和 dao 类
*（2）在 service 调用 dao 里面的方法
*（3）在 spring 配置文件中进行配置
*/
public class UserService {
    //创建 UserDao 类型属性，生成 set 方法
    private UserDao userDao;
    public void setUserDao(UserDao userDao) {
        this.userDao = userDao;
    }
    public void add() {
        System.out.println("service add...............");
        userDao.update();
    }
}

```

```xml
<!--1 service 和 dao 对象创建-->
<bean id="userService" class="com.atguigu.spring5.service.UserService">
    <!--注入 userDao 对象
     name 属性：类里面属性名称
     ref 属性：创建 userDao 对象 bean 标签 id 值
    -->
    <property name="userDao" ref="userDaoImpl"></property>
</bean>

<bean id="userDaoImpl" class="com.atguigu.spring5.dao.UserDaoImpl"></bean>
```



##### 1.2.2.5 注入内部bean

```java
/**
*（1）一对多关系：部门和员工
*	一个部门有多个员工，一个员工属于一个部门
*	部门是一，员工是多
*（2）在实体类之间表示一对多关系，员工表示所属部门，使用对象类型属性进行表示
*/
//部门类
public class Dept {
    private String dname;
    public void setDname(String dname) {
        this.dname = dname;
    }
}
//员工类
public class Emp {
    private String ename;
    private String gender;
    //员工属于某一个部门，使用对象形式表示
    private Dept dept;
    public void setDept(Dept dept) {
        this.dept = dept;
    }
    public void setEname(String ename) {
        this.ename = ename;
    }
    public void setGender(String gender) {
        this.gender = gender;
    }
}
```

```xml
<!--内部 bean-->
<bean id="emp" class="com.atguigu.spring5.bean.Emp">
    <!--设置两个普通属性-->
    <property name="ename" value="lucy"></property>
    <property name="gender" value="女"></property>
    <!--设置对象类型属性-->
    <property name="dept">
        <bean id="dept" class="com.atguigu.spring5.bean.Dept">
            <property name="dname" value="安保部"></property>
        </bean>
    </property>
</bean>
```

或者

```xml
<!--级联赋值-->
<bean id="emp" class="com.atguigu.spring5.bean.Emp">
    <!--设置两个普通属性-->
    <property name="ename" value="lucy"></property>
    <property name="gender" value="女"></property>
    <!--级联赋值-->
    <property name="dept" ref="dept"></property>
</bean>

<bean id="dept" class="com.atguigu.spring5.bean.Dept">
    <property name="dname" value="财务部"></property>
</bean>
```



##### 1.2.2.6 注入集合属性

```java
//（1）创建类，定义数组、list、map、set 类型属性，生成对应 set 方法
public class Stu {
    //1 数组类型属性
    private String[] courses;
    //2 list 集合类型属性
    private List<String> list;
    //3 map 集合类型属性
    private Map<String,String> maps;
    //4 set 集合类型属性
    private Set<String> sets;
    public void setSets(Set<String> sets) {
        this.sets = sets;
    }
    public void setCourses(String[] courses) {
        this.courses = courses;
    }
    public void setList(List<String> list) {
        this.list = list;
    }
    public void setMaps(Map<String, String> maps) {
        this.maps = maps;
    }
}
```

```xml
<!--1 集合类型属性注入-->
<bean id="stu" class="com.atguigu.spring5.collectiontype.Stu">
    <!--数组类型属性注入-->
    <property name="courses">
        <array>
            <value>java 课程</value>
            <value>数据库课程</value>
        </array>
    </property>
    
    <!--list 类型属性注入-->
    <property name="list">
        <list>
            <value>张三</value>
            <value>小三</value>
        </list>
    </property>
    
    <!--map 类型属性注入-->
    <property name="maps">
        <map>
            <entry key="JAVA" value="java"></entry>
            <entry key="PHP" value="php"></entry>
        </map>
    </property>
    
    <!--set 类型属性注入-->
    <property name="sets">
        <set>
            <value>MySQL</value>
            <value>Redis</value>
        </set>
    </property>
</bean>
```

**在集合中设置对象属性：**

```xml
<!--创建多个 course 对象-->
<bean id="course1" class="com.atguigu.spring5.collectiontype.Course">
    <property name="cname" value="Spring5 框架"></property>
</bean>
<bean id="course2" class="com.atguigu.spring5.collectiontype.Course">
    <property name="cname" value="MyBatis 框架"></property>
</bean>

<!--注入 list 集合类型，值是对象-->
<property name="courseList">
    <list>
        <ref bean="course1"></ref>
        <ref bean="course2"></ref>
    </list>
</property>
```



##### 1.2.2.7 bean的作用域

- 在 Spring 里面，默认情况下，**bean 是单实例对象**

- 在 spring 配置文件 bean 标签里面有属性（scope）用于设置单实例还是多实例

  scope 属性值 ：

  - 第一个值 默认值，singleton，表示是单实例对象 
  - 第二个值 prototype，表示是多实例对象

  ```xml
  <bean id="course1" class="com.atguigu.spring5.collectiontype.Course" scope="prototype">
      <property name="cname" value="Spring5 框架"></property>
  </bean>
  ```



##### 1.2.2.8 bean生命周期

- 通过构造器创建 bean 实例（无参数构造）
- 为 bean 的属性设置值和对其他 bean 引用（调用 set 方法）
- 调用 bean 的初始化的方法（需要进行配置初始化的方法）
- bean 可以使用了（对象获取到了）
- 当容器关闭时候，调用 bean 的销毁的方法（需要进行配置销毁的方法）



##### 1.2.2.9 自动装配

根据指定装配规则（属性名称或者属性类型），Spring 自动将匹配的属性值进行注入

```xml
<!--实现自动装配
 bean 标签属性 autowire，配置自动装配
 autowire 属性常用两个值：
 	byName 根据属性名称注入 ，注入值 bean 的 id 值和类属性名称一样
 	byType 根据属性类型注入
-->
<!--根据属性名称自动注入-->
<bean id="emp" class="com.atguigu.spring5.autowire.Emp" autowire="byName">
    <!--<property name="dept" ref="dept"></property>-->
</bean>
<bean id="dept" class="com.atguigu.spring5.autowire.Dept"></bean>

<!--根据属性类型自动注入-->
<bean id="emp" class="com.atguigu.spring5.autowire.Emp" autowire="byType">
    <!--<property name="dept" ref="dept"></property>-->
</bean>
<bean id="dept" class="com.atguigu.spring5.autowire.Dept"></bean>
```



##### 1.2.2.10 外部属性文件

```xml
<!--引入 context 名称空间-->
<beans xmlns="http://www.springframework.org/schema/beans" 
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/context
                           http://www.springframework.org/schema/context/spring-context.xsd">
    
    <!--引入外部属性文件-->
    <context:property-placeholder location="classpath:jdbc.properties"/>
    <!--配置连接池-->
    <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
        <property name="driverClassName" value="${prop.driverClass}"></property>
        <property name="url" value="${prop.url}"></property>
        <property name="username" value="${prop.userName}"></property>
        <property name="password" value="${prop.password}"></property>
    </bean>
```



#### 1.2.3 基于注解方式实现Bean管理

##### 1.2.3.1 注解的含义

- 注解是代码特殊标记，格式：@注解名称(属性名称=属性值, 属性名称=属性值..)
- 使用注解，注解作用在类上面，方法上面，属性上面
- 使用注解目的：简化 xml 配置



##### 1.2.3.2 Spring 针对 Bean 管理中创建对象提供注解

- @Component

- @Service

- @Controller

- @Repository

  上面四个注解功能是一样的，都可以用来创建 bean 实例



##### 1.2.3.3 基于注解方式实现对象创建

-  开启组件扫描

  ```xml
  <!--开启组件扫描
   1 如果扫描多个包，多个包使用逗号隔开
   2 扫描包上层目录
  -->
  <context:component-scan base-package="com.atguigu"></context:component-scan>
  ```

- 创建类

  ```java
  //在注解里面 value 属性值可以省略不写，
  //默认值是类名称，首字母小写
  //UserService -- userService
  @Component(value = "userService") //<bean id="userService" class=".."/>
  public class UserService {
      public void add() {
          System.out.println("service add.......");
      }
  }
  ```

- 基于注解方式实现属性注入

  ```java
  /**
  * (1) @Autowired：根据属性类型进行自动装配
  * 	第一步 把 service 和 dao 对象创建，在 service 和 dao 类添加创建对象注解
  * 	第二步 在 service 注入 dao 对象，在 service 类添加 dao 类型属性，在属性上面使用注解
  */
  @Service
  public class UserService {
      //定义 dao 类型属性
      //不需要添加 set 方法
      //添加注入属性注解
      @Autowired
      private UserDao userDao;
      public void add() {
          System.out.println("service add.......");
          userDao.add();
      }
  }
  
  /**
  *（2）@Qualifier：根据名称进行注入
  *	这个@Qualifier 注解的使用，和上面@Autowired 一起使用
  */
      //定义 dao 类型属性
      //不需要添加 set 方法
      //添加注入属性注解
      @Autowired //根据类型进行注入
      @Qualifier(value = "userDaoImpl1") //根据名称进行注入
      private UserDao userDao;
  
  /**
  *（3）@Resource：可以根据类型注入，可以根据名称注入
  */
      // @Resource //根据类型进行注入
      @Resource(name = "userDaoImpl1") //根据名称进行注入
      private UserDao userDao;
  
  /**
  *（4）@Value：注入普通类型属性
  */
      @Value(value = "abc")
      private String name;
  ```

- 开启组件扫描细节配置

  ```xml
  <!--示例 1
   use-default-filters="false" 表示现在不使用默认 filter，自己配置 filter
   context:include-filter ，设置扫描哪些内容
  -->
  <context:component-scan base-package="com.atguigu" use-defaultfilters="false">
      <!--只扫描带 @Controller 的类-->
      <context:include-filter type="annotation"
                              expression="org.springframework.stereotype.Controller"/>
  </context:component-scan>
  
  <!--示例 2
   下面配置扫描包所有内容
   context:exclude-filter： 设置哪些内容不进行扫描
  -->
  <context:component-scan base-package="com.atguigu">
       <!--不扫描带 @Controller 的类-->
      <context:exclude-filter type="annotation"
                              expression="org.springframework.stereotype.Controller"/>
  </context:component-scan>
  ```



##### 1.2.3.4 完全注解开发 

```java
/**
*（1）创建配置类，替代 xml 配置文件
*/
@Configuration //作为配置类，替代 xml 配置文件
@ComponentScan(basePackages = {"com.atguigu"})
public class SpringConfig {
}

/**
*（2）编写测试类
*/
@Test
public void testService2() {
    //加载配置类
    ApplicationContext context
        = new AnnotationConfigApplicationContext(SpringConfig.class);
    UserService userService = context.getBean("userService",UserService.class);
    System.out.println(userService);
    userService.add();
}
```



## 二、AOP

### 2.1 概念

- 面向切面编程（方面），利用 AOP 可以对业务逻辑的各个部分进行隔离，从而使得业务逻辑各部分之间的耦合度降低，提高程序的可重用性，同时提高了开发的效率。
- 通俗描述：不通过修改源代码方式，在主干功能里面添加新功能
- 使用登录例子说明 AOP

![image-20201120104359982](C:\Users\魏汉鹏\AppData\Roaming\Typora\typora-user-images\image-20201120104359982.png)

### 2.2 底层原理

- 使用 **JDK 动态代理**，使用 Proxy 类里面的方法创建代理对象

- 调用 newProxyInstance 方法 方法有三个参数：

  - 第一参数，类加载器 

  - 第二参数，增强方法所在的类，这个类实现的接口，支持多个接口

  - 第三参数，实现这个接口 InvocationHandler，创建代理对象，写增强的部分



### 2.3 Aop的基本实现

#### 2.3.1 切入点表达式

```
（1）切入点表达式作用：知道对哪个类里面的哪个方法进行增强
（2）语法结构： execution([权限修饰符] [返回类型] [类全路径] [方法名称]([参数列表]) )
	举例 1：对 com.atguigu.dao.BookDao 类里面的 add 进行增强
		execution(* com.atguigu.dao.BookDao.add(..))
	举例 2：对 com.atguigu.dao.BookDao 类里面的所有的方法进行增强
		execution(* com.atguigu.dao.BookDao.* (..))
	举例 3：对 com.atguigu.dao 包里面所有类，类里面所有方法进行增强
		execution(* com.atguigu.dao.*.* (..))
```



#### 2.3.2 Aop实现

```xml
<!--（1）在 spring 配置文件中，开启注解扫描 -->
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           http://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/context
                           http://www.springframework.org/schema/context/spring-context.xsd
                           http://www.springframework.org/schema/aop
                           http://www.springframework.org/schema/aop/spring-aop.xsd">
    
    <!-- 开启注解扫描 -->
    <context:component-scan basepackage="com.weihp.spring5.proxy"></context:component-scan>
    
    <!-- 开启 Aspect 生成代理对象-->
    <aop:aspectj-autoproxy></aop:aspectj-autoproxy>
```

```java
//被增强的类
@Component
public class User {
    public void add() {
        System.out.println("add.......");
    }
}

//增强的类
@Component
@Aspect //生成代理对象
public class UserProxy {
    //前置通知
    //@Before 注解表示作为前置通知
    @Before(value = "execution(* com.weihp.spring5.proxy.User.add(..))")
    public void before() {
        System.out.println("before.........");
    }
    //后置通知（返回通知）
    @AfterReturning(value = "execution(* com.weihp.spring5.proxy.User.add(..))")
        public void afterReturning() {
        System.out.println("afterReturning.........");
    }
    //最终通知
    @After(value = "execution(* com.weihp.spring5.proxy.User.add(..))")
    public void after() {
        System.out.println("after.........");
    }
    //异常通知
    @AfterThrowing(value = "execution(* com.weihp.spring5.proxy.User.add(..))")
        public void afterThrowing() {
        System.out.println("afterThrowing.........");
    }
    //环绕通知
    @Around(value = "execution(* com.weihp.spring5.proxy.User.add(..))")
    public void around(ProceedingJoinPoint proceedingJoinPoint) throws
        Throwable {
        System.out.println("环绕之前.........");
        //被增强的方法执行
        proceedingJoinPoint.proceed();
        System.out.println("环绕之后.........");
    }
}

//相同切入点的抽取
@Component
@Aspect //生成代理对象
@Pointcut(value = "execution(* com.weihp.spring5.proxy.User.add(..))")
public void UserProxy() {
    //前置通知
    //@Before 注解表示作为前置通知
    @Before(value = "pointdemo()")
    public void before() {
        System.out.println("before.........");
    }
}

//在增强类上面添加注解 @Order(数字类型值)，数字类型值越小优先级越高
@Component
@Aspect
@Order(1)
public class PersonProxy
```



#### 2.3.3 完全注解开发

```java
//创建配置类，不需要创建 xml 配置文件
    @Configuration
    @ComponentScan(basePackages = {"com.atguigu"})
    @EnableAspectJAutoProxy(proxyTargetClass = true)
    public class ConfigAop {
    }
```



#### 2.3.4 xml开发

```xml
<!--创建对象-->
<bean id="user" class="com.weihp.spring5.proxy.User"></bean>
<bean id="userProxy" class="com.weihp.spring5.proxy.UserProxy"></bean>

<!--配置 aop 增强-->
<aop:config>
    <!--切入点-->
    <aop:pointcut id="p" expression="execution(*
                                     com.weihp.spring5.proxy.User.add(..))"/>
    <!--配置切面-->
    <aop:aspect ref="userProxy">
        <!--增强作用在具体的方法上-->
        <aop:before method="before" pointcut-ref="p"/>
    </aop:aspect>
</aop:config>
```



## 三、JdbcTemplate

### 3.1 定义

​	Spring 框架对 JDBC 进行封装，使用 JdbcTemplate 方便实现对数据库操作

### 3.2 实现流程

#### 3.2.1 xml配置

```xml
<!-- 数据库连接池 -->
<bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource"
      destroy-method="close">
    <property name="url" value="jdbc:mysql:///user_db" />
    <property name="username" value="root" />
    <property name="password" value="root" />
    <property name="driverClassName" value="com.mysql.jdbc.Driver" />
</bean>

<!-- JdbcTemplate 对象 -->
<bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
    <!--注入 dataSource-->
    <property name="dataSource" ref="dataSource"></property>
</bean>

<!-- 组件扫描 -->
<context:component-scan base-package="com.atguigu"></context:component-scan>
```

#### 3.2.2 具体操作

```java
@Repository
public class BookDaoImpl implements BookDao {
    //注入 JdbcTemplate
    @Autowired
    private JdbcTemplate jdbcTemplate;
    //添加的方法
    @Override
    public void add(Book book) {
        //1 创建 sql 语句
        String sql = "insert into t_book values(?,?,?)";
        //2 调用方法实现
        Object[] args = {book.getUserId(), book.getUsername(),
                         book.getUstatus()};
        int update = jdbcTemplate.update(sql,args);
        System.out.println(update);
    }
    
    //修改的方法
    @Override
    public void updateBook(Book book) {
        String sql = "update t_book set username=?,ustatus=? where user_id=?";
        Object[] args = {book.getUsername(), book.getUstatus(),book.getUserId()};
        int update = jdbcTemplate.update(sql, args);
        System.out.println(update);
    }
    
    //删除的方法
    @Override
    public void delete(String id) {
        String sql = "delete from t_book where user_id=?";
        int update = jdbcTemplate.update(sql, id);
        System.out.println(update);
    }

    //查询表记录数
    @Override
    public int selectCount() {
        String sql = "select count(*) from t_book";
        Integer count = jdbcTemplate.queryForObject(sql, Integer.class);
        return count;
    }
    
    //查询返回对象
    @Override
    public Book findBookInfo(String id) {
        String sql = "select * from t_book where user_id=?";
        //调用方法
        Book book = jdbcTemplate.queryForObject(sql, new
                                                BeanPropertyRowMapper<Book>(Book.class), id);
        return book;
    }

    //查询返回集合
    @Override
    public List<Book> findAllBook() {
        String sql = "select * from t_book";
        //调用方法
        List<Book> bookList = jdbcTemplate.query(sql, new
                                                 BeanPropertyRowMapper<Book>(Book.class));
        return bookList;
    }

}
```



## 四、事务操作

### 4.1 事务的定义及特点

#### 4.1.1 定义

​	事务，就是一组操作数据库的动作集合。事务是现代数据库理论中的核心概念之一。如果一组处理步骤或者全部发生或者一步也不执行，我们称该组处理步骤为一个事务。当所有的步骤像一个操作一样被完整地执行，我们称该事务被提交。由于其中的一部分或多步执行失败，导致没有步骤被提交，则事务必须回滚到最初的系统状态。

#### 4.1.2 四个特点

- 原子性：一个事务中所有对数据库的操作是一个不可分割的操作序列，要么全做要么全不做

- 一致性：数据不会因为事务的执行而遭到破坏

- 隔离性：一个事物的执行，不受其他事务的干扰，即并发执行的事物之间互不干扰

- 持久性：一个事物一旦提交，它对数据库的改变就是永久的。



### 4.2 实现机制

​	Spring 为事务管理提供了丰富的功能支持。**Spring 事务管理分为编码式和声明式的两种方式**：

- 编程式事务指的是通过编码方式实现事务；

- 声明式事务基于 AOP,将具体业务逻辑与事务处理解耦。

​    **声明式事务有两种方式：**

- 一种是在配置文件（xml）中做相关的事务规则声明，

- 另一种是基于@Transactional 注解的方式。

#### 4.2.1 开启事务管理

- **xml方式：**

  ```xml
  <!--在 spring 配置文件引入名称空间 tx-->
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns:context="http://www.springframework.org/schema/context"
         xmlns:aop="http://www.springframework.org/schema/aop"
         xmlns:tx="http://www.springframework.org/schema/tx"
         xsi:schemaLocation="http://www.springframework.org/schema/beans
                             http://www.springframework.org/schema/beans/spring-beans.xsd
                             http://www.springframework.org/schema/context
                             http://www.springframework.org/schema/context/spring-context.xsd
                             http://www.springframework.org/schema/aop
                             http://www.springframework.org/schema/aop/spring-aop.xsd 
                             http://www.springframework.org/schema/tx
                             http://www.springframework.org/schema/tx/spring-tx.xsd">
      <!--创建事务管理器-->
      <bean id="transactionManager"
            class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
          <!--注入数据源-->
          <property name="dataSource" ref="dataSource"></property>
      </bean>
      <!--开启事务注解-->
      <tx:annotation-driven transactionmanager="transactionManager"></tx:annotation-driven>
  ```

- **注解方式：**

  ```java
  @Configuration //配置类
  @ComponentScan(basePackages = "com.atguigu") //组件扫描
  @EnableTransactionManagement //开启事务
  public class TxConfig {
      //创建数据库连接池
      @Bean
      public DruidDataSource getDruidDataSource() {
          DruidDataSource dataSource = new DruidDataSource();
          dataSource.setDriverClassName("com.mysql.jdbc.Driver");
          dataSource.setUrl("jdbc:mysql:///user_db");
          dataSource.setUsername("root");
          dataSource.setPassword("root");
          return dataSource;
      }
      //创建 JdbcTemplate 对象
      @Bean
      public JdbcTemplate getJdbcTemplate(DataSource dataSource) {
          //到 ioc 容器中根据类型找到 dataSource
          JdbcTemplate jdbcTemplate = new JdbcTemplate();
          //注入 dataSource
          jdbcTemplate.setDataSource(dataSource);
          return jdbcTemplate;
      }
      //创建事务管理器
      @Bean
      public DataSourceTransactionManager
          getDataSourceTransactionManager(DataSource dataSource) {
          DataSourceTransactionManager transactionManager = new
              DataSourceTransactionManager();
          transactionManager.setDataSource(dataSource);
          return transactionManager;
      }
  }
  ```

#### 4.2.2 声明事务

- **xml方式：**

  ```xml
  <!--1 创建事务管理器-->
  <bean id="transactionManager"
        class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
      <!--注入数据源-->
      <property name="dataSource" ref="dataSource"></property>
  </bean>
  <!--2 配置通知-->
  <tx:advice id="txadvice">
      <!--配置事务参数-->
      <tx:attributes>
          <!--指定哪种规则的方法上面添加事务-->
          <tx:method name="accountMoney" propagation="REQUIRED"/>
          <!--<tx:method name="account*"/>-->
      </tx:attributes>
  </tx:advice>
  <!--3 配置切入点和切面-->
  <aop:config>
      <!--配置切入点-->
      <aop:pointcut id="pt" expression="execution(*
                                        com.atguigu.spring5.service.UserService.*(..))"/>
      <!--配置切面-->
      <aop:advisor advice-ref="txadvice" pointcut-ref="pt"/>
  </aop:config>
  ```

- **注解方式：**

  ```java
  （1）@Transactional，这个注解添加到类上面，也可以添加方法上面
  （2）如果把这个注解添加类上面，这个类里面所有的方法都添加事务
  （3）如果把这个注解添加方法上面，为这个方法添加事务
      @Service
      @Transactional
      public class UserService {
          
      }
  ```

  

#### 4.2.3 事务回滚

- 自动回滚

  ```java 
  @Override
  @Transactional(rollbackFor = Exception.class)
  public Object submitOrder() throws Exception {  
       success();  
       //假如exception这个操作数据库的方法会抛出异常，方法success()对数据库的操作会回滚。 
       exception(); 
       return ApiReturnUtil.success();
  }
  ```

- 手动回滚

  ```java
  @Override
  @Transactional(rollbackFor = Exception.class)
  public Object submitOrder (){  
      success();  
      try {  
          exception(); 
       } catch (Exception e) {  
          e.printStackTrace();     
          //手工回滚异常
          TransactionAspectSupport.currentTransactionStatus().setRollbackOnly();
          return ApiReturnUtil.error();
       }  
      return ApiReturnUtil.success();
  ```

- 不会回滚的情况

  ```java
  @GetMapping("delete")
  @ResponseBody
  @Transactional    
  public void delete(@RequestParam("id") int id) {       
      try {          
          //delete country
          this.repository.delete(id);         
          if(id == 1){              
              throw Exception("测试事务");
          }           
          //delete city
          this.repository.deleteByCountryId(id);
      }catch (Exception e){
          logger.error("delete false:" + e.getMessage());        
          return new MessageBean(101,"delete false");
      }
  }
  //发现事务不回滚，即 this.repository.delete(id); 成功把数据删除了。
  ```

- **总结：**

  ​	**默认spring事务只在发生未被捕获的 RuntimeException 时才回滚。**

  ​	spring aop  异常捕获原理：**被拦截的方法需显式抛出异常，并不能经任何处理，这样aop代理才能捕获到方法的异常，才能进行回滚，默认情况下aop只捕获 RuntimeException 的异常，但可以通过配置来捕获特定的异常并回滚。**

  ​	换句话说**在service的方法中不使用try catch** 或者**在catch中最后加上throw new runtimeexcetpion（）**，这样程序异常时才能被aop捕获进而回滚。



#### 4.2.4 自调用问题

```java
@Service
public class OrderService {
    //没有事务管理
    private void insert() {
        //调用下面带有事务的方法
        insertOrder();
    }

    @Transactional
    public void insertOrder() {
        //insert log info
        //insertOrder
        //updateAccount
    }
}
```

**insertOrder 尽管有@Transactional 注解，但它被内部方法 insert()调用，事务被忽略，出现异常事务不会发生回滚**

**自调用导致@Transactional 失效。**

出现这个问题的根本原因 ：**在于AOP的实现原理。由于@Transactional 的实现原理是AOP，AOP的实现原理是动态代理，换句话说，自调用时不存在代理对象的调用，这时不会产生我们注解@Transactional 配置的参数，自然无效了。**



#### 4.2.5 @Transactional注解的使用

- **Spring团队的建议是你在具体的类（或类的方法）上使用 @Transactional 注解，而不要使用在类所要实现的任何接口上**。你当然可以在接口上使用 @Transactional 注解，但是这将只能当你设置了基于接口的代理时它才生效。因为注解是不能继承的，这就意味着如果你正在使用基于类的代理时，那么事务的设置将不能被基于类的代理所识别，而且对象也将不会被事务代理所包装（将被确认为严重的）。因此，请接受Spring团队的建议并且在具体的类上使用 @Transactional 注解。
- **@Transactional 注解应该只被应用到 public 修饰的方法上**。 如果你在 protected、private 或者 package-visible 的方法上使用 @Transactional 注解，它也不会报错， 但是这个被注解的方法将不会展示已配置的事务设置。
- Spring的AOP即声明式事务管理默认是针对unchecked exception回滚。也就是默认对RuntimeException()异常或是其子类进行事务回滚。checked异常,即Exception可try{}捕获的不会回滚，因此对于我们自定义异常，通过rollbackFor进行设定。
- 如果我们需要捕获异常后，同时进行回滚，通过TransactionAspectSupport.currentTransactionStatus().setRollbackOnly();进行手动回滚操作。
- 使用Object savePoint = TransactionAspectSupport.currentTransactionStatus().createSavepoint(); 设置回滚点，使用TransactionAspectSupport.currentTransactionStatus().rollbackToSavepoint(savePoint);回滚到savePoint。



#### 4.2.6 @Transactional常用配置

| 参 数 名 称            | 功 能 描 述                                                  |
| :--------------------- | :----------------------------------------------------------- |
| readOnly               | 该属性用于设置当前事务是否为只读事务，设置为true表示只读，false则表示可读写，默认值为false。例如：@Transactional(readOnly=true) |
| **rollbackFor**        | **rollbackFor   该属性用于设置需要进行回滚的异常类数组**，当方法中抛出指定异常数组中的异常时，则进行事务回滚。<br/>例如：指定单一异常类：@Transactional(rollbackFor=RuntimeException.class)<br/>指定多个异常类：@Transactional(rollbackFor={RuntimeException.class, Exception.class}) |
| rollbackForClassName   | 该属性用于设置需要进行回滚的异常类名称数组，当方法中抛出指定异常名称数组中的异常时，则进行事务回滚。<br/>例如：指定单一异常类名称@Transactional(rollbackForClassName=”RuntimeException”)<br/>指定多个异常类名称：@Transactional(rollbackForClassName={“RuntimeException”,”Exception”}) |
| **noRollbackFor**      | 该属性用于设置不需要进行回滚的异常类数组，当方法中抛出指定异常数组中的异常时，不进行事务回滚。<br/>例如：指定单一异常类：@Transactional(noRollbackFor=RuntimeException.class)<br/>指定多个异常类：@Transactional(noRollbackFor={RuntimeException.class, Exception.class}) |
| noRollbackForClassName | 该属性用于设置不需要进行回滚的异常类名称数组，当方法中抛出指定异常名称数组中的异常时，不进行事务回滚。<br/>例如：指定单一异常类名称：@Transactional(noRollbackForClassName=”RuntimeException”)<br/>指定多个异常类名称：@Transactional(noRollbackForClassName{“RuntimeException”,”Exception”}) |
| **propagation**        | 该属性用于设置事务的传播行为。<br/>例如：@Transactional(propagation=Propagation.NOT_SUPPORTED,readOnly=true) |
| **isolation**          | 该属性用于设置底层数据库的事务隔离级别，事务隔离级别用于处理多事务并发的情况，通常使用数据库的默认隔离级别即可，基本不需要进行设置 |
| timeout                | 该属性用于设置事务的超时秒数，默认值为-1表示永不超时事物超时设置: @Transactional(timeout=30) //默认是30秒 |



#### 4.2.7 事务5种隔离级别

例如：@Transactional(isolation = Isolation.READ_COMMITTED)

| 隔离级别         | 含义                                                         |
| :--------------- | :----------------------------------------------------------- |
| DEFAULT          | 这是一个PlatfromTransactionManager默认的隔离级别，使用数据库默认的事务隔离级别. 另外四个与JDBC的隔离级别相对应； |
| READ_UNCOMMITTED | 最低的隔离级别。事实上我们不应该称其为隔离级别，因为在事务完成前，其他事务可以看到该事务所修改的数据。而在其他事务提交前，该事务也可以看到其他事务所做的修改。可能导致脏，幻，不可重复读 |
| READ_COMMITTED   | 大多数数据库的默认级别。在事务完成前，其他事务无法看到该事务所修改的数据。遗憾的是，在该事务提交后，你就可以查看其他事务插入或更新的数据。这意味着在事务的不同点上，如果其他事务修改了数据，你就会看到不同的数据。可防止脏读，但幻读和不可重复读仍可以发生。 |
| REPEATABLE_READ  | 比ISOLATION_READ_COMMITTED更严格，该隔离级别确保如果在事务中查询了某个数据集，你至少还能再次查询到相同的数据集，即使其他事务修改了所查询的数据。然而如果其他事务插入了新数据，你就可以查询到该新插入的数据。可防止脏读，不可重复读，但幻读仍可能发生。 |
| SERIALIZABLE     | 完全服从ACID的隔离级别，**确保不发生脏读、不可重复读和幻读**。这在所有隔离级别中也是最慢的，因为它通常是通过完全锁定当前事务所涉及的数据表来完成的。代价最大、可靠性最高的隔离级别，所有的事务都是按顺序一个接一个地执行。避免所有不安全读取。 |



#### 4.2.8 脏读、不可重复读和幻读

| 术语       | 含义                                                         |
| :--------- | :----------------------------------------------------------- |
| 脏读       | **A事务读取到了B事务还未提交的数据，如果B未提交的事务回滚了，那么A事务读取的数据就是无效的，这就是数据脏读** |
| 不可重复读 | **在同一个事务中，多次读取同一数据返回的结果不一致，这是由于读取事务在进行操作的过程中，如果出现更新事务，它必须等待更新事务执行成功提交完成后才能继续读取数据，这就导致读取事务在前后读取的数据不一致的状况出现** |
| 幻读       | **A事务读取了几行记录后，B事务插入了新数据，并且提交了插入操作，在后续操作中A事务就会多出几行原本不存在的数据，就像A事务出现幻觉，这就是幻读** |

**提醒：**
  不可重复读的重点是修改，同样的条件，你读取过的数据，再次读取出来发现值不一样了
  幻读的重点在于新增或者删除，同样的条件，第 1 次和第 2 次读出来的记录数不一样



### 4.3 注意事项

1. 要根据实际的需求来决定是否要使用事物，最好是在编码之前就考虑好，不然到以后就难以维护；
2. 如果使用了事物，请务必进行事物测试，因为很多情况下以为事物是生效的，但是实际上可能未生效！
3. 事物@Transactional的使用要放再类的**公共(public)方法**中，需要注意的是在 protected、private 方法上使用 @Transactional 注解，它也不会报错(IDEA会有提示)，但事务无效。
4. **事物@Transactional是不会对该方法里面的子方法生效！**也就是你在公共方法A声明的事物@Transactional，但是在A方法中有个子方法B和C，其中方法B进行了数据操作，但是该异常被B自己处理了，这样的话事物是不会生效的！反之B方法声明的事物@Transactional，但是公共方法A却未声明事物的话，也是不会生效的！如果想事物生效，需要将子方法的事务控制交给调用的方法，在子方法中使用rollbackFor注解指定需要回滚的异常或者将异常抛出交给调用的方法处理。一句话就是在使用事物的时候子方法最好将异常抛出！
5. 事物@Transactional由spring控制的时候，它**会在抛出异常的时候进行回滚**。如果自己**使用catch捕获了处理了，是不生效的**，**如果想生效可以进行手动回滚或者在catch里面将异常抛出，比如throw new RuntimeException();**。
6. **@Transactional可以放在Controller下面直接起作用，看到网上好多同学说要放到@Component下面或者@Service下面，经过试验，可以不用放在这两个下面也起作用。**
7. @Transactional引入包问题，她有两个包：import javax.transaction.Transactional; 和 import **org.springframework.transaction.annotation.Transactional**; 这两个都可以用，对比了一下他们两个的方法和属性，发现后面的比前面的**强大。建议后面的**。
8. PlatformTransactionManager 这个接口中定义了三个方法 getTransaction创建事务，commit 提交事务，rollback 回滚事务。她的实现类是 AbstractPlatformTransactionManager这个。



## 五、原理

### 5.1 注解驱动开发

#### 5.1.1 向IOC容器中注册组件的方式：

- 包扫描+组件标注注解（@Controller/@Service/@Repository/@Component）
- @Bean 导入第三方包里面的组件
- @Import 快速给容器导入一个组件
  - @Import(要导入到容器中的组件) ；容器中就会自动注册这个组件，id默认是全类名
  - ImportSelector ：返回需要导入的组件的**全类名**数组
  - ImportBeanDefinitionRegistrar 手动注册bean到容器中

- 使用 Spring 提供的 FactoryBean（工厂Bean）
  - 默认获取到的是工厂Bean调用getObject创建的对象
  - 要获取工厂Bean本身，我们需要给id前面加一个 &

#### 5.1.2 Bean的生命周期

- 构造（对象创建）：

  - 单实例：在容器每次启动时创建对象
  - 多实例：在每次获取时创建对象

  BeanPostProcessor.postProcessBeforeInitialization

- 初始化：

  - 对象创建完成，并赋值好，调用初始化方法

  BeanPostProcessor.postProcessAfterInitialization

- 销毁：
  - 单实例：容器关闭时
  - 多实例：容器不会管理这个Bean；容器不会调用销毁方法

