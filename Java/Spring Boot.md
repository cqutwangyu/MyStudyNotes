Spring Boot 学习笔记
====

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