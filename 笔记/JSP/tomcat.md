#1发布
1. 把项目export成***.war
2. copy到tomcat下的webapps下
3. 启动comcat,***.war自动解压

#2tomcat的目录
1. bin:启动、工具;里面最常用的是starup.bat,如果是linux或mac系统，启动文件是stratup.sh
2. conf：配置tomcat;里面最核心的是server.xml。例如端口什么的
3. lib:库文件，tomcat依赖jar
4. log：日志
5. temp：放临时文件
6. webapps：放程序的。可以放war，也可以直接是目录形式
7. work：编译以后的class文件

#tomcatweb容器：可以运行jsp的
weblogic:超大型的web容器  
tomcat：中型  
jetty：小型web容器  
jboss：中型，比tomcat好一些  
webSphere：IBM的web容器  

/php/asp/aspx...     
支持以上的web容器：   
IIS：ms window自带的web容器   
apache2：web容器  