## 什么时Spring Data ##
## Spring Data 包含多个子项目
1. Spring Data JPA

		减少数据访问层的开发量
2. Spring Data Mongo DB
3. Spring Data Redis
4. Spring Data Solr

#Spring Data Jpa
##Repository
###1. Repository接口
Spring Data的核心接口，不提供任何方法。空接口，标记接口  
一个接口可以继承Repository，或者通过注解@RepositoryDefinition。同时该接口就会交给spring管理
**Repository中查询方法定义规则和使用**  
**使用Spring Data完成复杂查询方法名称的命名**  
![avatar](..\imgs\spring-data1.png)  
![avatar](..\imgs\spring-data2.png)  
###2. CrudRepository：继承了Repository，并且实现了基本的CURD操作

###3. PagingAndSortingRepository：继承了CrudRepository，实现了分页的操作
	1、该接口包含分页和排序功能
	2、带排序的查询
	3、带排序的分页查询：findAll(Pageable pageable)
###4. JpaRepository：继承了PagingAndSortingRepository接口。实现Jpa规范
###5. JpaSpecificationExecutor:
按照方法命名来使用的话，有弊端    
1. 方法名太长：约定大于配置    
2. 对于一些复杂的查询，是很难实现   
**Query注解的使用：只能查询用**  
1. 在Repository方法中使用，不需要遵循查询方法命名规则  
2. 只需要将@Query定义在Repository中的方法之上即可  
3. 命名参数及索引参数的使用    
4. 本地查询  
**Modifying注解的使用**  
1. Query注解和Modifying注解一起使用才能修改数据
2. 更新操作还必须配合事务
3. 才可以，否则就会报异常

###6. RepositoryDefinition
###7. Repository Query Specifications
###8. Query Annotation
###8. Update/Delete/Transcation