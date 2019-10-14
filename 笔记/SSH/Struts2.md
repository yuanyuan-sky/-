## Struts2的环境要求
1. Servlet API 2.4
2. JSP API 2.0
3. Java 5

## Structs2 的工作原理以及文件结构 
### 工作原理  
![avatar](..\imgs\6688.png)  

1. 客户端初始化一个指向Servlet容器（例如Tomcat）的请求
2. 这个请求经过一系列的过滤器（Filter）（这些过滤器中有一个叫做ActionContextCleanUp的可选过滤器，这个过滤器对于Struts2和其他框架的集成很有帮助，例如：SiteMesh Plugin）
3. 接着FilterDispatcher（现已过时）被调用，FilterDispatcher询问ActionMapper来决定这个请是否需要调用某个Action
4. 如果ActionMapper决定需要调用某个Action，FilterDispatcher把请求的处理交给ActionProxy
5. ActionProxy通过Configuration Manager询问框架的配置文件，找到需要调用的Action类
6. ActionProxy创建一个ActionInvocation的实例。
7. ActionInvocation实例使用命名模式来调用，在调用Action的过程前后，涉及到相关拦截器（Intercepter）的调用。
8. 一旦Action执行完毕，ActionInvocation负责根据struts.xml中的配置找到对应的返回结果。返回结果通常是（但不总是，也可 能是另外的一个Action链）一个需要被表示的JSP或者FreeMarker的模版。在表示的过程中可以使用Struts2 框架中继承的标签。在这个过程中需要涉及到ActionMapper  

### 文件结构
1. web.xml
		
		配置dispatcher
		引入struts
2. struts.xml

		struts2的核心配置文件。自动加载
		该文件主要负责管理应用中的Action映射，以及该Action包含的Result定义等
		1、全局属性
		2、用户请求和响应Action之间的对应关系
		3、Action可能用到的参数和返回结果
		4、各种拦截器的配置
3. struts.properties

		struts2框架的全局属性文件，自动加载
		该文件包含很多key-value对

### Action搜索顺序  
Http://localhost:8080/struts2/path1/path2/path3/student.action

	第一步：判断package是否存在，如 path1/path2/path3/
			如果package存在，判断action是否存在，如果action不存在则去默认的namespace的package里面寻找action，如果没有action，则报错
			
			如果package不存在，检查上一级路径的package是否存在，直到默认的namespace，如果一直没找到则报错

### 动态方法调用
解决一个Action对应多个请求的处理  
3种方式  

1. 指定method属性（不推荐使用） 

		在action标签中指定请求对应的方法
2. 感叹号方式（不推荐使用）

		在struts.xml中开启一个功能
		<constant name="struts.enable.DynamicMethodInvocation" value="true"/>

		在action中指定多个result，并指定name属性
			<result name="add">/add.jsp</result>
		在相应的方法中指定返回到result的name
			return "add";
		
		请求：
		http://localhost:8080/struts2/helloworld!add.action
3. 通配符的方式
			
		struts.xml中
		<!-- {1}就是和*对应的 -->
		 <action name="helloworld_*" method="{1}" class="com.ssh.action.HelloWorldAction">
            <result>/result.jsp</result>
            <result name="add">/{1}.jsp</result>
            <result name="update">/{1}.jsp</result>
        </action>

		Action中
		public String add() {
	        System.out.println("add");
	        return "add";
	    }

		访问
		http://localhost:8080/struts2/helloworld_add

		第二种

		<package name="default" namespace="/" extends="struts-default">
	        <action name="*_*" method="{2}" class="com.ssh.action.{1}Action">
	            <result>/result.jsp</result>
	            <result name="add">/{2}.jsp</result>
	            <result name="update">/{2}.jsp</result>
		     </action>
	    </package>

		Action类中

		public String add() {
	        System.out.println("add");
	        return "add";
	    }


		访问：
		http://localhost:8080/struts2/HelloWorld_add

		_ 前面的*对应的是{1}
		_ 后面的*对应的是{2}

		注意：请求地址中，_前面应该和你的Action类名一致

### 指定多个配置文件

	<include file="xxx.xml" />

### struts2 的后缀
两种配置方式  

	一、在struts.properties文件中
			struts.action.extension = action,do,asd,
	二、在struts.xml中
			<constant name="struts.action.extension" value="action,aa,ad"/>

### 接受参数
三种方式  

1. 直接在Action中添加全局属性，并且给这个属性添加get、set方法

		前端传过来的数据，就会对应到相应的属性上
2. 使用对象

		在Action中添加要传入的对象的全局属性（不用实例化）
		给该对象属性添加get、set方法
			
		前端传数据的时候要指定是哪个全局对象的属性

		 private User user；
		前端
		用户名:<input type="text" name="user.username">
3. 使用ModelDriven

		Action需要实现接口ModelDriven<T>,并实现其方法
		@Override
	    public User getModel() {
	        return user;
	    }

		这种方式全局属性需要实例化
		 private User user=new user()；
		不需要为user添加get、set方法

		前端
		用户名:<input type="text" name="username">

		如果User中有个List类型的sort属性，前端怎么向sort传值
		
		类别1:<input type="text" name="sort[0]">
		类别2:<input type="text" name="sort[1]">
			
			  
	
	

		
		
