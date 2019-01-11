Spring 学习笔记
====

一、Spring基于xml的IoC环境搭建
----
* 使用idea创建新项目,勾选Spring(4.3.18),这样会自动导入Spring中常用的jar包,或者手动下载：[下载地址](https://repo.spring.io/libs-release-local/org/springframework/spring/ "点击下载")<br>
Java类：
```Java
public class IAccountServiceImpl implements IAccountService {
}
public class AccountDaoImpl implements IAccountDao {
}
```
bean.xml：
```Xml
<?xml version="1.0" encoding="UTF-8" ?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd">
        
    <bean id="accountService" class="com.wangyu.service.impl.IAccountServiceImpl"/>
    <bean id="accountDao" class="com.wangyu.dao.impl.AccountDaoImpl"/>
```
Main:
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
输出结果
```Java
com.wangyu.service.impl.IAccountServiceImpl@48eff760
com.wangyu.dao.impl.AccountDaoImpl@402f32ff
```
