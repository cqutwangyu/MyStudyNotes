Spring Boot 学习笔记
====

# 什么是Spring Boot？

Spring Boot 是 Spring 开源组织下的子项目，是 Spring 组件一站式解决方案，主要是简化了使用 Spring 的难度，简省了繁重的配置，提供了各种启动器，开发者能快速上手。

Spring Boot 的优点：

- 独立运行
- 简化配置
- 自动配置
- 无代码生成和XML配置
- 应用监控
- 上手容易
- …

# **Spring Boot 的核心配置文件**

Spring Boot 的核心配置文件是 application 和 bootstrap 配置文件。

application 配置文件这个容易理解，主要用于 Spring Boot 项目的自动化配置。

bootstrap 配置文件有以下几个应用场景。

- 使用 Spring Cloud Config 配置中心时，这时需要在 bootstrap 配置文件中添加连接到配置中心的配置属性来加载外部配置中心的配置信息；
- 一些固定的不能被覆盖的属性；
- 一些加密/解密的场景；

# **Spring Boot 的核心注解**

启动类注解是@SpringBootApplication，它也是 Spring Boot 的核心注解，主要组合包含了以下 3 个注解：

- @SpringBootConfiguration：组合了 @Configuration 注解，实现配置文件的功能。
- @EnableAutoConfiguration：打开自动配置的功能，也可以关闭某个自动配置的选项，如关闭数据源自动配置功能：             @SpringBootApplication(exclude = { DataSourceAutoConfiguration.class })。
- @ComponentScan：Spring组件扫描。

# 难题解决

## 一、Spring Boot正常启动访问url返回404
* `问题描述：`在浏览器中访问:`http://localhost:8081/rest/hello`返回`error (type=Not Found, status=404)`。
* 相关代码如下：
```Java
@RestController
@RequestMapping("/rest")
public class LoginController {

    @RequestMapping(value = "/hello",method = RequestMethod.GET)
    public String hello() {
        return "Hello!";
    }

}
```
`pom.xml`
```xml
    <groupId>com.example</groupId>
    <artifactId>demo</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <name>demo</name>
```
* `问题原因：`Controller与DemoApplication的层级关系错误。<br>
`DemoApplication.java`
```Java
package com.example.demo;

@SpringBootApplication
public class DemoApplication{}
```
`LoginController.java`
```Java
package com.jobms.controller;

@RestController
@RequestMapping("/rest")
public class LoginController {}
```
* `解决方法:`将DemoApplication.java置于LoginController.java的上级目录或同级目录。
* `得出结论:`SpringBootApplication启动类必须位于Controller控制类的同目录或父目录，如果放在子目录或者Controller类的兄弟目录下，都会在访问url时出现404错误。

## 二、Spring Boot连接MySql (jdbc+DruidDataSource)
* 错误信息如下：
```Java
java.sql.SQLException: The server time zone value 'ÖÐ¹ú±ê×¼Ê±¼ä' is unrecognized or represents more than one time zone. You must configure either the server or JDBC driver (via the serverTimezone configuration property) to use a more specifc time zone value if you want to utilize time zone support.
```
* `错误原因`The server time zone value 'ÖÐ¹ú±ê×¼Ê±¼ä' is unrecognized or represents more than one time zone.<br>
* `解决方法1`url:jdbc:mysql://localhost:port/databasename?`加上` serverTimezone=UTC,如果有多个参数需要用`&`连接
* `解决方法2`控制台登录mysql用户，输入命令`set global time_zone='+8:00';`
