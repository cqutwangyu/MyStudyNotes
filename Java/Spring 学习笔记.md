Spring 学习笔记
====

一、Spring基于xml的IoC环境搭建
----
### 1、Spring入门
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
        ApplicationContext ac = new ClassPathXmlApplicationContext("bean.xml");//由于我的bean.xml位于src下，直接写入即可。
        //2.根据bean的id获取对象
        IAccountService as = (IAccountService) ac.getBean("accountService");//返回一个object，需要强转为IAccountService
        IAccountDao adao = ac.getBean("accountDao", IAccountDao.class);//传入IAccountDao类的字节码，返回一个IAccountDao
        System.out.println(as);
        System.out.println(adao);
    }
```
输出结果：
```Java
com.wangyu.service.impl.AccountServiceImpl@48eff760
com.wangyu.dao.impl.AccountDaoImpl@402f32ff
```
### 2、bean对象的三种创建方式：
##### 第一种：通过调用构造函数来创建bean对象
* 在默认情况下，当我们在spring的配置文件中写了一个bean标签，并提供了class属性，spring就会调用默认构造函数创建对象。
* 如果没有默认构造函数，则对象创建失败。
bean.xml
```Xml
<bean id="accountService" class="com.wangyu.service.impl.AccountServiceImpl"/>
```
Main:
```
       ApplicationContext ac = new ClassPathXmlApplicationContext("bean.xml");//由于我的bean.xml位于src下，直接写入即可。
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
       ApplicationContext ac = new ClassPathXmlApplicationContext("bean.xml");//由于我的bean.xml位于src下，直接写入即可。
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
