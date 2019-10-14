## 什么是ORM  
ORM（Object/Relationship Mapping）:对象/关系映射
## 什么是Hibernate  
Hibernate是Java领域的一款开源的ORM框架技术。  
Hibernate对JDBC进行了非常轻量级的对象封装。

## 基本类型  

	hibernate映射类型		java类型				标准SQL类型				描述
	-----------------------------------------------------------------------------------
		date			java.util.Date或				Date			代表日期：yyyy-MM-dd
						java.sql.Date
	-----------------------------------------------------------------------------------
		time			java.util.Date或
						java.sql.Date				TIME			代表时间：hh:mm:ss
	-----------------------------------------------------------------------------------
		timestamp		java.util.Date或								代表：时间和如期
						java.sql.Timestamp			TIMESTAMP		yyyy-MM-dd hh:mm:ss
	-----------------------------------------------------------------------------------
		calendar		java.util.Calendar			TIMESTAMP		同上
	-----------------------------------------------------------------------------------
		calendar_date	java.util.Calendar			DATE			代表日期：yyyy-MM-dd
	-----------------------------------------------------------------------------------

## Hibernate的开发步骤
1. 编写配置文档hibernate.cfg.xml  
2. 编写实体类
3. 生成对应的实体类的映射文件并添加到配置文档中
4. 进行测试
