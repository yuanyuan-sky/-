#1. NoSQL的概述   

- NoSQL = not only SQL 不仅仅是SQL
- 非关系型数据库
- C语言开发出来的

#2.为什么需要NoSQL

1. High performance - 高并发读写。
2. Huge Storage - 海量数据的高效率存储和访问。
3. High Scalability && High Availability - 高可扩展性和高可用行。

#3.NoSQL数据库的四大分类
1. 键值（Key-Value）存储。redis

		优点：快速查询。
		缺点：存储的数据缺少结构化。
		应用：内容缓存，主要用于处理大量数据的高访问负载。
2. 列存储。HBase

		优点：查找速度比较快、扩展性比较强，更容易进行分布式扩展。
		缺点：功能相对局限。
		应用：分布式的文件系统。
3. 文档数据库。MongDB

		优点：数据结构要求不是很严格。
		缺点：查询性能不是很高且缺少统一的查询语法。
		应用：Web应用。
4. 图形数据库。

#4.NoSQL的特点

1. 易扩展
2. 灵活的数据模型
3. 大数据量，高性能
4. 高可用