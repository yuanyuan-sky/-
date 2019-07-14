项目管理工具有哪些？  
- Maven
- Ant
- gradle

#Maven
什么是maven？  
Maven是基于项目对象模型（POM），可以通过一小段描述信息来管理项目的构建、报告和文档的软件项目管理工具。
#Maven的目录结构

	src
		-main
			-java
				-package
		-test
			-java
				-package
		resources

#Maven中常用得构建命令
1. mvn -v 查看maven版本
2. mvn compile 编译
3. mvn test 测试
4. mvn package 打包
5. mvn clean 删除target文件
6. mvn install将打包得本地文件jar包发布到本地仓库中

#自动创建目录骨架
两种方式

1. mvn archetype:genarate

		这种方式按照提示进行选择
2. mvn archetype:genarate -DgroupId=组织名,公司网址的反写+项目名 -DartifactId=项目名-模块名 -Dversion=版本号 -Dpackage=代码所存在的包名

#Maven中的坐标和仓库
####坐标

	groupId
	arcifactId
	version
#####仓库  
本地仓库和远程仓库 

	远程仓库
	E:\apache-maven-3.6.0\lib\maven-model-builder-3.6.0.jar\org\apache\maven\model\pom.xml里有地址
#####镜像仓库
	E:\apache-maven-3.6.0\conf\settings.xml
	配置
	<mirrors>
		<mirror>
		  <id>maven.net.cn</id>
		  <mirrorOf>central</mirrorOf>
		  <name>central mirror in china</name>
		  <url>http://maven.net.cn/content/groups/public</url>
		</mirror>
	</mirrors>
	就可以使用国内的镜像仓库

#更改本地仓库位置

	<settings ...>
		<localRepository>F:\maven\repository</localRepository>
	</settings>

#在Eclipse中创建maven项目
Maven有些东西是运行在jdk上的，而eclipse是运行在jre上的，所以要修改eclipse的jre。
![avatar](..\imgs\1010.jpg)

jre home选择内带jre的jdk
####创建maven项目
file->new->other->Maven Project

####运行pom.xml文件
在pom.xml上右键->run as ->Maven build...
![avatar](..\imgs\1011.jpg)

红线处可以输入compile、package等命令，然后Run

#Maven的生命周期和插件
#####完整的项目构建过程包括
清理、编译、测试、打包、集成测试、验证、部署
#####maven生命周期
1. clean：清理项目

		分为三个阶段
		1、pre-clean 执行清理前的工作
		2、clean 清理上一次构建生成的所有文件
		3、post-clean 执行清理后的文件
2. default：构建项目（最核心）

		常用的阶段
		1、compile
		2、test
		3、package
		4、install
3. site：生成项目站点

		1、pre-site 在生成项目站点前要完成的工作
		2、site 生成项目的站点文档
		3、post-site 在生成项目站点后要完成的工作
		4、site-deploy 发布生成的站点到服务器上

这三个生命周期是相互独立的

#pom.xml解析



#依赖的传递

A依赖于B，B依赖于C，则默认情况下，A就会依赖于B和C

	<dependency>
			<!-- 当前maven项目依赖于hongxing-ng，hongxing-ng依赖于hongxing-bg -->
    	  <groupId>com.hongxing</groupId>
		  <artifactId>hongxing-ng</artifactId>
		  <version>0.0.1-SNAPSHOT</version>
			<!-- 只想依赖hongxing-ng，可以把hongxing-bg屏蔽掉 -->
		  <exclusions>
		  	<exclusion>
		  		<groupId>com.hongxing</groupId>
			    <artifactId>hongxing-bge</artifactId>
		  	</exclusion>
		  </exclusions>
    </dependency>

#maven依赖冲突
1. 短路优先

		优先解析路径短的版本
		A->B->C->X
		A->D->X;优先解析这个
1. 先声明先优先

		如果路径长度相同，则谁先声明，先解析谁（谁在pom的前面，就依赖谁）

#Maven中的聚合和继承
1. 聚合

		将多个Maven项目一起执行install

		<modules>
		  	<module>../hongxing-bge</module>
		  	<module>../hongxing-ng</module>
		  	<module>../hongxing-shanji</module>
	    </modules>
		将这三Maven放在该Maven项目里，然后将该Maven项目的<packaging>pom</packaging>改为pom，然后执行clean install
1. 继承
		以Junit为例  
		1、建一个Maven项目作为父项目，将父项目的pom中的packaging改为pom  
		2、将公共依赖放于父项目的pom中的dependencyManagement中  
			`<dependencyManagement> `  
			  `<dependencies>`  
			    `<dependency>`   
			      `<groupId>junit</groupId>`  
			      `<artifactId>junit</artifactId>`  
			      `<version>3.8.1</version>`  
			      `<scope>test</scope>`  
			    `</dependency>`  
			  `</dependencies>`  
		    `</dependencyManagement>`  
		3、在子项目中的pom.xml中，加入parent标签,并给出父项目的坐标      
			`<parent>`  
				`<groupId>com.hongxing</groupId>`  
				`<artifactId>hongxing-parent</artifactId>`  
				`<version>0.0.1-SNAPSHOT</version>`  
			`</parent> `   
		则子项目中只需要  
		`<dependency>`  
	      `<groupId>junit</groupId>`   
	      `<artifactId>junit</artifactId>`   
	    `</dependency>`
		即可


#使用maven构建web项目