#1 Servlet:
HttpServletRequest、HttpServletResponse  

Servlet。有两个参数，request、response  
用于编写逻辑的地方

Servelet 接收请求，返回响应

###1 配置URL ，映射一个servlet

###2 自定义的Servelet类要继承HttpServlet
###3覆盖doGet和doPost
	当get请求时调用doGet
	当post请求时调用doPost

**servlet获取session**

		HttpSession session= HttpServletRequest对象.getSession();

**获取字符输出流**

        PrintWrite  aa= HttpServletResponse对象.getWrite();
**字节输出流**
        
        OutputStream  bb = HttpServletResponse对象.getOutputStream();






在定义servlet的时候，可以配置初始化参数<init-param>...   
还可以定义load-on-start> 值是正数，web容器初始化调用

web容器：tomcat：web.xml   

**JSP就是Servlet**
	