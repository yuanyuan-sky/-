#jdk安装
概念：java开发工具包。泛指javaSE：java标准版

#java语言的特点：
java是面向对象、编译+解释型语言、跨平台
安全、简单、动态、多线程、分布式等等
#java中没有指针
##java能做什么
winform 编程-gui 图形用户界面  
doc命令行方式工具 
终端、嵌入式  
大型服务端程序web方向
##按用途分支
javaSE:j2SE:javase  :java标准版  
javaEE:j2EE:javaee  javaWeb开发、Java企业级应用开发  
javaME：j2ME:javame:java嵌入式开发  

![](https://i.imgur.com/hfANwQs.png)

###字节码经过java运行变成机器码

#HelloWorld

	public class HelloWorld{
		//定义程序入口方法
		public static void main(String[] args){
	
			System.out.println("hello world");
			System.out.println("===========");
		}
	
	}
#命令
javac  文件   命令根据.java文件生成.class文件。编译  
java   类名   命令运行：解释.class文件成机器码运行
	
	.class叫做字节码文件。.java源码文件
#java程序类型分类
1. applet:内嵌在网页上的（已经淘汰了）
2. application:app应用程序

##JVM
java虚拟机。JVM是一种用于计算设备的规范。通过内存虚构出来的计算机。模拟计算机各种功能。


1. 跨平台：一次编写可以在不同的平台运行。原因是JVM。


1. 解释执行：jvm把字节码.class文件解释成机器码执行。


1. 面向对象：：3个特性：继承、多态、封装


1. 自动垃圾回收：通过垃圾回收的不同算法。实现内存（主要是堆内存）的自动清理。


1. 健壮性，2次验证：编译时，运行时。异常处理机制。


1. 多线程：多个线程做一件事。js是单线程。

2. 简单：没有指针，不直接操作内存

1. 分布式：

1. 安全性：java能够防范各种攻击

1. 体系结构中立

1. 高性能

1. 动态性：库中可以自由的添加新方法和实例变量

###JNI：java本地化接口，java代码调用c++/c

JDK:java开发工具包  
JRE：java运行时环境。jvm在jre中  
.jar --java打包文件，库文件。超级狗只需要jre就行了



#注释


1. //
2. /* */多行注释
3. /**   */  文档注释，放在类上和方法上的注释，用生产的javadoc  
**注释不能嵌套**
#标识符
由数字，字母，下划线，$(美元符)组成，不能以数字开头，不能是关键字

###java语言严格区分大小写

#定义一个类
	[public] class 类名{
		类体
	}
类名首字母要大写。  
public修饰的类名必须和文件名相同。文件中可以有很多个class，但是只有一个public  
**main方法必须为public且必须为静态**
#java语言的保留字
1. const
2. goto
#定义一个方法
[public/protected/private] static  void/类型  方法名（参数列表）

权限访问修饰符  static静态的   void 返回值方法/类型是返回的类型  方法名指标识符  
参数列表（类型1  参数名1，类型2  参数名2。。。）

#静态不能调用非静态。反过来则可以，即静态方法不能调用非静态方法，静态方法也不能调用类中非静态的变量
**静态是属于类的。非静态是属于对象的**

#定义变量、常量
类型  变量名；
变量名=值；
常量：final 类型  变量名=值；
变量名是标识符

#包的概念
classpath 根目录一般就是src，编译开始的根目录

src/java/util/Date.java 在不同包的情况下想引入Date

import java.util.Date;只引入Date.class
或者  java.util.*  ;引入java.util下的所有的类

**java.long是默认包：例如 String System 不需要import。处理默认包以外的都应该import**

#对象实例化
	类型  变量 =new 类型();    BigIntegrt  b=new BigIntrger();
	类型 对象  =new 构造方法();    Class  b=new Class([参数...]);

#类
1. java程序的基本组成单位是类

#类之间的关系
1. 依赖：参数
2. 关联：属性
3. 继承

###类的结构

- 属性：对象数据的描述  
- 方法：对象的行为
- 构造方法：用于实例化对象
- 内部类：在类中声明的类
- 块：分为静态块，实力块

###类的作用
类就是一个模板，定义多个对象共同的属性和方法
###方法
方法即对象的行为：实现具体的功能

###Java配置的环境变量是哪三个 _PATH_，_JAVAHOME_，_CLASSPATH_

    public static void main(String[] args) {

		boolean b = true;
		boolean d;
		if (b == true) {//做比较
			System.out.println("aaaa");
		}
		if (d = true) {//先赋值，再判断
			System.out.println("bbb");
		}
        两个if都是可以运行的，只是意义不一样，

	}

静态代码块在构造方法之前执行    


	   String a = "" + 5 + true;
		System.out.println(a);
        结果为5true
