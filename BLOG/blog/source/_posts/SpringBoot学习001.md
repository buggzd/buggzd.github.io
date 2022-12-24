---
title: SpringBoot学习001
date: 2022-12-24 22:10:47
categories:
- 学习笔记
tags: 
- 后端
- SpringBoot
- Java
---
# Spring基础
# 控制器

@Controller和@RestController用于接受和处理HTTP请求。

请求页面和数据使用@Controller，如果只请求数据使用@RestController

# 路由映射
@RequestMapping进行路由映射

``` java
// 所有json格式请求都会调用test方法
@RequestMapping("/*.json")
public String test(){return "get json";}
```

使用@RequestMapping获取参数
常规域名后用？[参数名]=[参数值] 表示，多个参数用&分隔。
例如：
``` Java
//前往http://localhost:8080/hello页面并且给一个参数name=rick
//链接应该是http://localhost:8080/hello?name=rick
@RestController
public class HelloController {
//传入参数名必须和方法变量名一样。不填或者填错则获取到null
	@RequestMapping(value ="/hello",method=RequestMethod.GET)
	public String hello(String name){
		return name;
	}
//如果传入参数不一样可以使用@RequestParam解释
//但是如果加上注解，默认意味着该参数为必填，不填参数为非法
//可以添加required = false设置为非必选
	@RequestMapping(value ="/hello",method=RequestMethod.GET)
	public String hello(@RequestParam("name",required = false) String nickname){
		return name;
	}
}
```
# StringBoot 文件
默认会在项目目录下生成一个static文件存放静态资源。
src/main/resources/static
在这个static文件中放置图片，可以直接通过文件名访问。例如存放了一张名为test.jpg的图片。可以通过访问http://localhost:8080/test.jpg 访问图片。

可以在src/main/resources/application.properties这里配置访问路径，使用spring.mvc.static-path-pattern修改路径。
例如：
```java 
// "src/main/resources/application.properties"
//默认是=/**
spring.mvc.static-path-pattern=/upload/**
```
也可以修改static文件夹路径，也是在src/main/resources/application.properties这里，使用spring.web.resources.static-locations修改。
例如：
```
// "src/main/resources/application.properties"
//默认是=classpath:/static/
spring.web.resources.static-locations=classpath:/static/
```
# 接收文件：
src/main/java/com/example/springbootlearning/Controller/fileUploadController.java

springboot中的文件类型使用MultipartFile

