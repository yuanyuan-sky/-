#SqlSession的作用
1. 向SQL语句传入参数
2. 执行SQL语句
3. 获取执行SQL语句的结果
4. 事务控制

###如何获取SqlSession
1. 通过配置文件获取数据库连接信息
		读取配置文件  
		Reader reader = Resources.getResourceAsReader("com/imooc/config/Configuration.xml");
2. 通过配置信息构建SqlSessionFactory

		SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(reader);
3. 通过SqlSessionFactory打开数据库会话

		SqlSession session = sqlSessionFactory.openSession();
1. 执行XML中的方法

		messageList =  session.selectList("Message.queryMessageList",message);
		第一个参数：XML的namespace.标签的id
		第二个参数：参数。只能传一个参数，所以多个的时候需要进行封装
**注意：mybatis默认是不会自动提交的**

#核心配置文件
	<?xml version="1.0" encoding="UTF-8" ?>
	<!DOCTYPE configuration
	    PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
	    "http://mybatis.org/dtd/mybatis-3-config.dtd">
	
	<configuration>
	  <environments default="development">
	    <environment id="development">
	      <transactionManager type="JDBC">
	        <property name="" value=""/>
	      </transactionManager>
	      <dataSource type="UNPOOLED">
	        <property name="driver" value="com.mysql.jdbc.Driver"/>
	        <property name="url" value="jdbc:mysql://127.0.0.1:3306/micro_message"/>
	        <property name="username" value="root"/>
	        <property name="password" value="123456"/>
	      </dataSource>
	    </environment>
	  </environments>
	
	  <mappers>
	    <mapper resource="com/imooc/config/sqlxml/Message.xml"/>
	  </mappers>
		<!-子XML的位置-->
	
	</configuration>


#ONGL表达式
![avatar](..\imgs\666.jpg)   
![avatar](..\imgs\777.jpg)

	传的是一个常量，直接使用${_parameter}
	<delete id="deleteOne" parameterType="int">
    	delete from message where ID = #{_parameter}
  	</delete>
	注意：#{}里，当传的是String和基本类型的时候，写什么都可以，但是最好是_parameter。
	------------------------------------------------------------------
	传的是一个List，无论传的list参数名叫什么，collection里都是list
	<delete id="deleteBatch" parameterType="java.util.List">
        delete from message where  ID in (
            <foreach collection="list" item="item" separator=",">
                #{item}
            </foreach>
        )
    </delete>
	separator:以什么为间隔，把集合里的元素拼接起来
	
OGNL中支持java方法

	<if test="description !=null and !&quot;&quot;.equals(description.trim())">
        and DESCRIPTION = #{description}
    </if> 


#Mybatis中常用的标签
1. where标签

		select *
        from command 
        <where>
            <if test="name != null and !&quot;&quot;.equals(name.trim())">
                and Name = #{name}
            </if>
            <if test="description !=null and !&quot;&quot;.equals(description.trim())">
                and DESCRIPTION like '%' #{description} '%'
            </if>
        </where>
		where标签的作用：
		1、如果where标签里的条件都不满足，则不在原sql后面加上where关键字
		2、如果where里的多个条件满足，则把第一个and关键字去掉
1. sql标签

		<sql id="columns">name,age,sex</sql>//该标签与select等标签同级
		在使用的时候
		select <include refid="columns"> from user
1. set标签

		set标签用于update标签内
		update  user
		<set>
			<if test="name != null" >
				set name=#{name},
			</if>
			<if test="age != null">
				set ang = #{age},
			</if>
		</set>
		作用：
		1、set标签内的条件如果都不满足的话，则不在原sql后加上set关键字。
		2、如果set内的多个条件都满足，则去掉最后一个逗号。
1. trim标签

		<trim prefix="(" suffix=")" prefixOverrides="," suffixOverrides=",">

		</trim>
		作用：如果trim中有内容，则在最前面加上( 最后面加 ),还能解决最前面或者最后面多的逗号问题
		prefix:前缀
		suffix:后缀
		prefixOverrides:解决最前面多出来的符号；如果想解决前面多出的两种符号之一：prefixOverrides="and/or/,"
		suffixOverrides:解决最后面多出来的符号;同上
1. choose标签

		<choose>
			<when test="">
	
			</when>
			<when test="">

			</when>
			<when test="">

			</when>
			<otherwise>
				
			</otherwise>
		</choose>
		
		类似于java的swith标签；
		第一个when里的满足，则输出第一个第一个when里的内容，后面的不输出；依次往下推。
		如果都不能满足，则输出otherwise里的内容
1. collection标签

		一对多时使用
		<resultMap type="com.imooc.bean.Command" id="Command">
	        <id column="C_ID" jdbcType="INTEGER" property="id"/>
	        <result column="NAME" jdbcType="VARCHAR" property="name"/>
	        <result column="DESCRIPTION" jdbcType="VARCHAR" property="description"/>
	        <collection property="list" resultMap="CommandContent.CommandContent">
	
	        </collection>
	    </resultMap>
		collection中的resultMap是辅表xml的namespace点resultMap的id

1. association标签 

		与collection标签相反，collection是一对多时，在主表中指向辅表的
		association则是在辅表中指向主表的

![avatar](..\imgs\888.jpg)

#`#`{}和${}的区别

	select * from user where username = #{name}
	select * from user where username = ${name}
	#{}有个预编译的过程，会将#{}编译成 ?,然后再对其赋值
	${}没有预编译过程，会直接将值拼在相应的位置。
	${}的应用场景：order by ${column} ;根据前台传的参数，按不同的列排序

#mybatis怎么取自增主键值
	
	<insert parameterType="com.User" useGeneratedKeys="true" keyProperty="id">
		insert into user(name,age) values(#{name},#{age})
	</insert>
	在传进来的对象中，id是没有值的，但是在执行插入成功后，传进来的参数user的id上，会存入生成的主键值。


#log4j
properties文件：里面放的都是key=value这种形式
	
	#输出的级别和位置，输出大于等于dubug级别的都输出
	log4j.rootLogger=DEBUG,Console
	log4j.appender.Console=org.apache.log4j.ConsoleAppender
	log4j.appender.Console.layout=org.apache.log4j.PatternLayout
	#定义日志输出格式
	log4j.appender.Console.layout.ConversionPattern=%d [%t] %-5p [%c] - %m%n
	log4j.logger.org.apache=INFO
	------------------------------------------
	debug->info->warn->error;级别由低到高
	日志格式：%d 产生日志的时间；%t产生日志的线程名称；%-5p:输出日志的级别，最少占5个空格，负号说明空格在左边；%c输出日志所处的类全名；%m输出日志时的附加信息；%n换行

#mybatis接口式编程
1. 子XML的namespace变为接口的类全名
2. 子XML中的sql的id与接口中的方法相对应
3. sql的返回值与接口中方法的返回值对应，sql的参数与接口中方法的参数对应

		//获取SqlSession
		SqlSession session = new SqlSessionFactoryBuilder().build(reader);
		//获取接口的反射
		ICommand icommand = session.getMapper(ICommand.class);
		//执行接口中的方法，获取结果
		List list = icommand.queryMessageList(参数);

#mybatis的拦截器

