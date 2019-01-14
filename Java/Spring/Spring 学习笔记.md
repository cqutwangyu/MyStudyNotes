Spring 学习笔记
====
目录
----
* [一、Spring基于xml](#一spring基于xml)
    * [1、Spring的IoC入门案例](#1spring的IoC入门案例)
    * [2、bean对象的三种创建方式](#2bean对象的三种创建方式)
    * [3、bean对象的作用范围与生命周期](#3bean对象的作用范围与生命周期)
    * [4、xml方式依赖注入](#4xml方式依赖注入)
* [二、Spring基于注解](#二spring基于注解)<br>

一、Spring基于xml
----
### 1、Spring的IoC入门案例
* 使用idea创建新项目，勾选Spring(4.3.18)，这样会自动导入Spring中常用的jar包，或者手动下载：[下载地址](https://repo.spring.io/libs-release-local/org/springframework/spring/ "点击下载")<br>
* Spring提供了核心容器，可以将配置好的bean对象存放在容器中。当程序需要时，根据需要的对象类型到容器中查找。若找到唯一匹配类型的对象则直接返回对，若没找到则报异常。若找到多个相同类型的对象则根据变量名来继续查找，若找到则返回对象，若没有找到则报异常。
* 以下程序中通过`ClassPathXmlApplicationContext`读取`bean.xml`配置文件，并通过根据`xml`中定义的`bean`对象的`id`来进行查找。<br>
Java类：<br>
```Java
public class AccountServiceImpl implements IAccountService {
}
public class AccountDaoImpl implements IAccountDao {
}
```
bean.xml：<br>
```Xml
<?xml version="1.0" encoding="UTF-8" ?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd">
        
    <bean id="accountService" class="com.wangyu.service.impl.AccountServiceImpl"/>
    <bean id="accountDao" class="com.wangyu.dao.impl.AccountDaoImpl"/>
</beans>
```
Main:<br>
```Java
    public static void main(String[] args) {
        //1.获取Spring的核心容器
        //由于我的bean.xml位于src下，直接写入即可。
        ApplicationContext ac = new ClassPathXmlApplicationContext("bean.xml");
        //2.根据bean的id获取对象
        //返回一个object，需要强转为IAccountService
        IAccountService as = (IAccountService) ac.getBean("accountService");
        //传入IAccountDao类的字节码，返回一个IAccountDao
        IAccountDao adao = ac.getBean("accountDao", IAccountDao.class);
        System.out.println(as);
        System.out.println(adao);
    }
```
输出结果：
```Java
com.wangyu.service.impl.AccountServiceImpl@48eff760
com.wangyu.dao.impl.AccountDaoImpl@402f32ff
```
### 2、bean对象的三种创建方式
##### 第一种：通过调用构造函数来创建bean对象
* 在默认情况下，当我们在spring的配置文件中写了一个bean标签，并提供了class属性，spring就会调用默认构造函数创建对象。
* 如果没有默认构造函数，则对象创建失败。
bean.xml
```Xml
<bean id="accountService" class="com.wangyu.service.impl.AccountServiceImpl"/>
```
Main:
```    //由于我的bean.xml位于src下，直接写入即可。
       ApplicationContext ac = new ClassPathXmlApplicationContext("bean.xml");
       IAccountService as = (IAccountService) ac.getBean("accountService");
```
##### 第二种：通过静态工厂创建bean对象
* 工厂类中提供一个静态方法，可以返回要用的bean对象。
StaticBeanFactory.java
```Java
public class StaticBeanFactory {
    public static IAccountService getBean() {
        return new AccountServiceImpl();
    }
}
```
bean.xml
```Xml
<bean id="staticAccountService" class="com.wangyu.factory.StaticBeanFactory" factory-method="getBean"/>
```
Main:
```Java
       //由于我的bean.xml位于src下，直接写入即可。
       ApplicationContext ac = new ClassPathXmlApplicationContext("bean.xml");
       IAccountService as = (IAccountService) ac.getBean("staticAccountService");
```
##### 第三种：通过实例工厂创建bean对象
* 工厂类中提供一个普通方法，可以返回要用的bean对象。
InstanceBeanFactory.java
```Java
public class InstanceBeanFactory {
    public IAccountService getBean() {
        return new AccountServiceImpl();
    }
}
```
bean.xml
```Xml
<bean id="instanceFactory" class="com.wangyu.factory.InstanceBeanFactory"/>
<bean id="instanceAccountService" factory-bean="instanceFactory" factory-method="getBean"/>
```
### 3、bean对象的作用范围与生命周期
##### 作用范围：
* 它是可以通过配置的方式来指定的。
```xml
<bean id="accountService" class="com.wangyu.service.impl.AccountServiceImpl" scope="prototype"/>
<!--
配置的属性：
       bean标签的scope属性属性的取值：
              singleton：单例的。默认值 最常用的
              prototype：多例的。
              request：请求范围。
              session：会话范围。
              global-session：全局会话范围
!-->
```

##### 生命周期
```
单例对象:
       出生：容器创建对象出生。
       活着：只要容器存在，对象就一直可用。
       死亡：容器销毁，对象消亡。
多例对象:
       出生：每次使用时，容器会为我们创建对象。活着：只要对象在使用过程中，就一直活着。
       死亡:当对象长时间不用，并且也没有其他对象引用时，由java的垃圾回收器回收。
```

### 4、xml方式依赖注入
```xml
<!-- 
Spring的依赖注入注入的方式：
       第一种方式：通过构造函数注入
       第二种方式：通过set方法注入
注入的内容：
       第一类：基本类型和String类型
       第二类：其他的bean类型
       第三类：复杂类型（集合类型）
第一种：使用构造函数注入
       涉及的标签：
              constructor-arg该标签是写在bean标签内部的子标签
              标签的属性：
              type：指定要注入的参数在构造函数中的类型
              index：指定要注入的参数在构造函数的索引位置
              name：指定参数在构造函数的中的名称
              value：指定注入的数据内容，他只能指定基本类型数据和String类型数据
              ref：指定其他bean类型数据。写的是其他bean的id。其他bean指的是存在于spring容器中的bean。
-->
<bean id="accountService"class="com.itheima.service.impl.AccountServiceImpl">
       <constructor-arg name="name"value="赛新待"></constructor-arg>
       <constructor-arg name="age"value="18"></constructor-arg>
       <constructor-arg name="birthday"ref="now"></constructor-arg>
</bean>

<!-- 
第二种：使用set方法注入常用
       涉及的标签：property该标签也是要写在bean标签内部的子标签
              标签的属性：
              name：指定的是set方法的名称。匹配的是类中set后面的部分。
              value：指定注入的数据内容，他只能指定基本类型数据和String类型数据
              ref：指定其他bean类型数据。写的是其他bean的id。其他bean指的是存在于spring容器中的bean。 
-->
<bean id="accountService2"class="com.itheima.service.impl.AccountServiceImpl2">
       <property name="name"value="test"></property>
       <property name="age"value="21"></property>
       <property name="birthday"ref="now"></property>r
</bean>
<bean id="now"class="java.util.Date"></bean>

<!-- 
使用p名称空间注入
的本质仍然是需要类中提供set方法，同时在配置文件中要导入p名称空间 
-->
<bean id="accountService3"class="com.itheima.service.impl.AccountServiceImpl3"
       p:name="张三">
</bean>
```
二、Spring基于注解
----
### 1、用于创建bean对象的注解
* 用于创建对象的基础注解：<br>
    * `@Component`<br>
     * 作用：就相当于在spring的xml配置文件中写了一个bean标签。<br>
     * 属性：<br>
         * value:用于指定bean的id，当不写时默认值是当前类名，首字母改小写，例如：accountServiceImpl<br>
* 由`@Component`衍生的三个注解：<br>
    * `@Controller`一般用于表现层（控制层）<br>
    * `@Service`一般用于业务层<br>
    * `@Repository`一般用于持久层<br>
   * 他们的作用以及属性和@Component的作用是一模一样的，他们的出现是spring框架为我们提供更明确的语义来指定不同层的bean对象。
```Java
//业务层
@Component("accountService1")//若不定义id，则默认为accountServiceImpl
public class AccountServiceImpl implements IAccountService {}
@Service("accountService2")
public class AccountServiceImpl_old implements IAccountService {}
//持久层
@Repository("accountDao")
public class AccountDaoImpl implements IAccountDao {}
//表现层（控制层）
@Controller
public class AccountControllerImpl implements IAccountController {}
```
### 2、用于注入数据的注解
* 用于注入其他bean类型的注解：
    * `@Autowired`
        * 作用：自动按照类型注入。只要容器中有唯一的类型匹配，则可以直接注入成功。如果有多个类型匹配时，会先按照类型找到符合条件的对象，然后再用变量名称作为bean的id，从里面继续查找，如果找到仍然可以注入成功，如果没有匹配的id，则报错。
        * 细节：当使用此注解注入时，set方法可以省略。
        * 属性：
            * required：是否必须注入成功，取值是true（默认组）/false，当取值是true时，没有匹配的对象就报错。
    * `@Qualifier`
        * 作用：在自动按照类型注入的基础之上，再按照bean的id注入。在给类成员注入时，它不能够独立使用。
        * 属性：
            * value：用于指定bean的id。
    * `@Resource`
        * 作用：直接按照bean的id注入。
        * 属性：
            * name：用于指定bean的id。
    * 以上3个注解，都只能用于注入其他bean类型，而不能注入基本类型和String。
    
* 用于注入基本类型和String类型的数据：
    * `@Value`
        * 作用：用于注入基本类型和string类型的数据。
        * 属性：
            * value：用于指定要注入的数据。它支持使用spring的el表达式,spring的el表达式写法：${表达式}
[回到顶部](#spring-学习笔记)
