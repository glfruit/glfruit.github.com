---
title: '使用Spring开发微服务（一）：Hello, Microservices!'
tags: [Spring, 微服务]
categories: 技术研究
---
微服务是近几年开始流行起来的一种架构设计方式，我最近根据[《Spring Microservices in Action》](https://www.manning.com/books/spring-microservices-in-action)这本书认真学习了一下微服务和使用Spring来开发微服务应用的基本方法，这个系列就算是学习笔记吧，主要记录使用Spring及相关工具开发微服务的具体步骤和方法，关于微服务的概念、设计和思考在其它文章中再展开。
<!-- more -->

## 用到的框架和程序
- Spring Framework
- Spring Boot
- Maven
- POSTMAN
- SDKMAN!

## 项目配置与初始化
### 安装Spring Boot CLI
Spring为基于Spring Boot开发微服务应用提供了完善的支持，Spring Boot CLI是一个通过命令行来创建和运行使用Spring Boot创建的应用的工具，因此我们首先安装它，安装方式有多种，这里我们选择
使用SDKMAN!安装：
`````
sdk install springboot
`````

### 初始化项目
spring
Spring Boot is the core technology used in our microservice implementation. Spring Boot greatly simplifies microservice development by simplifying the core tasks of building REST-based microservices.

Spring Boot CLI的安装与基本使用

创建一个Spring Boot应用
{% codeblock lang:bash %}
spring init -g=me.glfruit -a=todos -d=web todos
{% endcodeblock %}

编辑TodoApplication.java
{% codeblock lang:java %}
package me.glfruit.todos;

import org.springframework.boot.SpringBootApplication;
import org.springframework.boot.SpringApplication;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.bind.annotation.RestController;

@SpringBootApplication
@RestController
@RequestMapping(value="/")
public class TodoApplication {
    public static void main(String[] args) {
        SpringApplication.run(TodoApplication.class, args);
    }
    @RequestMapping(value="/hello")
    public String hello() {
        return "{\"message\":\"Hello, Microservices!\"}";
    }
}
{% endcodeblock %}

### 运行项目
{% codeblock lang:bash %}
  mvn spring-boot:run
{% endcodeblock %}
