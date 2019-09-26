#SpringBoot
SpringBoot是SpringMVC的升级版，但是二者之间又没有什么联系
## SpringBoot的特点 ##
1. 简化配置
2. 备受关注，是下一代框架
3. 微服务的入门级的框架

## 微服务 ##
Spring为微服务提供了一整套组件  
微服务——》SpringCloud——》SpringBoot  
学习SpringCloud就要先学习SpringBoot  

## SpringBoot的启动方式 ##
方式一：

	直接在项目里运行Application文件
方式二：

	通过命令行进入到项目文件里
	输入命令：mvn spring-boot:run
方式三：

	通过命令行进入到项目文件里
	先通过命令mvn install将项目添加到本地仓库里
	然后进入到项目的target文件夹下
	然后使用java命令运行target下的.jar文件：java -jar ***.jar
## SpringBoot的配置文件 ##
**有两种格式**  
1. .properties文件

	# 修改端口号
	server.port=8081
	# 修改上下文路径，这样在访问controller时，就要在路径的前面加上/girl
	server.servlet.context-path=/girl
2. .yml文件

		server:
		  port: 8082
		  servlet:
		    context-path: /girl
		注意：如果冒号后面有内容的话，需要在冒号与内容之间要有空格
### 在不同环境使用不同配置文件 ###
1. 在生产环境中，可以使用application配置文件指定使用哪个配置文件
2. 在用maven的启动方式时，如启动方式3，可以在启动的时候选择使用哪个配置文件

		java -jar .\target\demo-0.0.1-SNAPSHOT.jar --spring.profiles.active=prod

## Spring-Data-Jpa ##
### JPA ###
	JAP定义了一系列对象持久化标准，目前实现这一规范的产品有Hibername、TopLink等
### Spring-Data-Jap ###
	就是Spring对Hibernate的整合