# SpringBoot入门

## 什么是SpringBoot

- javaweb的开发框架
- 简化开发，**约定大于配置**
- 开箱即用



## 微服务

一种架构风格



## 单体应用架构

一个应用中的所有服务都封装在一个应用中



## 微服务架构

让服务独立。把独立出来的功能元素动态组合，需要的功能元素才组合，需要多一些时间以整合多个功能元素。

微服务架构是对功能元素进行复制，而没有对整个应用进行复制。

好处：

- 节省了调用资源
- 每个功能元素都是一个可替换的、可独立升级的软件代码

[MartinFowler关于微服务架构论文（中文版）](https://www.cnblogs.com/liuning8023/p/4493156.html)



# 第一个程序

## 创建

- 官方提供了一个快速生成的网站

- IDEA提供



## 初始文件说明

- xxxxApplication --->程序主入口 本身就是Spring的一个组件

- application.properties --->springboot核心配置文件

- xxxxApplicationTests --->单元测试

- pom.xml文件

![image-20210526152046600](image-20210526152046600.png)



## 测试

在xxxApplication**同级目录**下创建controller\service\dao\pojo等包



## Skills

- 更改端口号

  在application.properties中添加如下代码

```java
server.port=8081
```

- 修改banner

  在网络上寻找banner自动生成器，将生成好的banner复制

  在application.properties同级目录下创建banner.txt，将刚才复制的banner文本放入

  重启spring



# 原理初探*

pom.xml

- spring-boot-dependencies：核心依赖在父工程中
- 不需要指定版本就是因为有依赖



启动器



主程序

```java
//@SpringBootApplication:标注这个类是一个springboot的应用
@SpringBootApplication
public class Springboot01HelloworldApplication {
    public static void main(String[] args) {
        //将springboot应用启动
        SpringApplication.run(Springboot01HelloworldApplication.class, args);
    }
}
```

- 注解

  - ```java
    @SpringBootConfiguration：springboot 的配置
    	@Configuration：spring配置类
    @EnableAutoConfiguration：自动配置
        @AutoConfigurationPackage：自动配置包
        @Import(AutoConfigurationImportSelector.class)：导入了选择器
    ```

- run



# 配置文件

## yaml配置文件

### 语法结构

key: 空格value

**对空格的要求十分高**

可以注入到配置类

```java
# 普通的key-value
server:
  port: 8081

# 对象
student1:
  name: fourteen
  age: 3

#行内写法
student2: {name: fourteen,age: 3}

#数组
pets:
  - cat
  - dog
  - pig

#数组行内写法
pets:[cat,dao,pig]
```



## 配置文件给实体类赋值

### 使用yaml文件

```java
//可以使用配置文件中的属性给加了此注解的类赋值
//将配置文件中配置的每一个属性的值，映射到这个组件中
//告诉SpringBoot将本类中所有的属性和配置文件中相关的配置进行绑定
//只有这个组件是容器中的组件，才能使用容器提供的@ConfigurationProperties功能
@ConfigurationProperties(prefix = "配置类中配置的前缀")
```

添加以下依赖可以解决该问题

![image-20210526165003250](image-20210526165003250.png)

```java
<dependency
	<groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-configuration-processor</artifactId>
    <optional>true</optional>
</dependency>
```

### 使用properties文件

```
//类上使用
//使用该注解进行配置文件导入 同时该注解导入的配置文件可以自定义名
@PropertySource(value = "classpath:fourteen.properties")

//该注解放在需要导入值的属性上 使用EL表达式即可获取值
@Value("${name}")
```



## 占位符

```xml
person:
  name: ${random.uuid}
  age: ${random.int%80}
  happy: true
  birth: 2019/11/02
  maps: {k1: v1,k2: v2}
  lists:
    - code
    - music
    - girl
  dog:
    name: ${person.happy:hello}_旺财
    age: 1
```



## 松散绑定

配置文件中的属性值和类中定义的属性名称可以不一样

firstName ---> first-name



## 多环境配置及配置文件位置

### 配置文件优先级

file:./config/

file:./

classpath:./config

classpath:./

### 多环境配置

#### properties文件下

另外两个文件命名为

application-dev.properties

application-test.properties

```properties
# springboot的多环境配置，可以选择激活哪一个配置文件
spring-profiles-active=dev
spring-profiles-active=test
```

#### yaml文件下

```yaml
# springboot的多环境配置，可以选择激活哪一个配置文件
server:
  port: 8080
spring:
  profiles:
    active: test
---
server:
  port: 8081
spring:
  config:
    activate:
      on-profile: dev

---
server:
  port: 8083
spring:
  config:
    activate:
      on-profile: test
```



# JSR303校验

**Bean Validation 中内置的 constraint**

![img](webp)

 **Hibernate Validator 附加的 constraint**

![img](webp2)

### 邮箱验证

引入依赖

```xml
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-validation</artifactId>
</dependency>
```

使用

```java
@Validated //数据校验 放在类上
@Email()	//放在需要验证的属性上
```



# Web开发

## 静态资源

在springboot中，我们可以使用以下方法处理静态资源

- webjars
- public,static,/**,resoures     localhost：8080

优先级

resoures  >  static（默认）>  public



## 首页

放在resoures  、  static、  public目录下的index.html页面可以直接访问

而在templates目录下的所有页面，只能使用controller操作



## SpringMVC自动配置

在springboot中有非常多的xxxConfiguration帮我们进行扩展配置