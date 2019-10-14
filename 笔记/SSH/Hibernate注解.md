## JPA与Hibernate的关系  
## 什么是JPA？
Java Persistence API(java 持久化 API)  
## JPA与hibernate的关系  
JPA是标准接口，Hibernate是实现。但是其功能是JPA的超集。
## JPA 与 Hibernate 的关系
通过hibernate-annotation、Hibernate-entitymanager和hibenate-core三个组件来实现  

## Hibernate 注解的分类  
### 类级别注解
1. @Entity：映射实体类，一个实体类对应数据库中的一张表

		@Entity(name="tableName")
		name:可选，对应数据库中的一个表。若表明与实体类相同，则可以省略

	**注意：使用@Entity时必须指定实体类的主键属性**  
2. @Table

		@Table(name="",catalog="",schema="")
		配合@Entity使用，只能标注在实体的class定义处，表示实体对应的数据库表的信息
	  	name：可选，映射表的名称，默认表明与实体名称一致，只有在不一致的情况下才需要指定表明,与Entity的name属性，指定一个即可  
		catalog:可选，表示Catalog名称，默认为Catalog("")，mysql不支持catalog
		schema:可选，表示Schema名称，默认为Schema("")。在mysql中是指数据库的名称  
3. @Embeddable

		@Embeddable 表示一个非Entity类，即不会生成数据库表，但是可以嵌入到另一个Entity类中作为属性
### 属性级别注解
添加到属性上，可以直接写在属性上面，也可以写在属性的getter方法上
  
1. @Id  

		必须，定义了映射到数据库表的主键的属性，一个实体可以有一个或者多个属性被映射为主键
**注意：如果有多个属性被定义为主键，该实体必须实现serializable接口**
2. @SequenceGenerator  
3. @GeneratedValue

		@GeneratedValue(strategy=GenerationType,generator="")
		可选，用于定义主键生成策略
		strategy表示主键生成策略，取值有：
			1、GenerationType.AUTO:根据底层数据库自动选择（默认）
			2、GenerationType.IDENTITY:根据数据库的Identity字段生成
			3、GenerationType.SEQUENCE:使用Sequence来决定主键的取值
			4、GenerationType.TABLE:使用指定表来决定主键取值，结合@TableGenerator使用
		例如：定义自增主键
		@Id
		@GeneratedValue(strategy=GenerationType.AUTO)
		generator表示主键生成器
		定义主键手工填写
		@Id
		@GeneratedValue(generator="aaa")
		@GenericGenerator(name="aaa",strategy="assigned")
4. @Column

		@Column描述了数据库表中该字段的详细定义
		常用属性
			1、name：可选，表示数据库中该字段的名称。默认与属性名称一致
			2、nullable：表示该字段是否可以为null，默认为true
			3、unique：可选，表示该字段是否是唯一标识，默认false
			4、length：可选，表示该字段的大小，仅对String类型有效
			5、insertable:可选，表示在ORM框架进行插入操作时，该字段是否应该出现INSERT语句中，默认为true
			6、updateable：可选，表示更新操作时，该字段是否出现在UPDATE语句中
5. @Embeddedd

		表示该属性的类是嵌入类
		同时，嵌入类也必须标注@Embeddable注解
6. @Lob
7. @EmbeddedId

		使用嵌入式主键类实现复合主键
		注意：嵌入式主键类必须实现Serializable接口，必须有默认的public无参数的构造方法，必须覆盖equals和hashCode方法
		
8. @Version
9. @Basic
10. @Transient

		可选，表示该属性并非一个到数据库表的字段的映射，ORM框架将忽略该属性。
		如果一个属性并非数据库表的字段映射，就务必将其标示为@Transient,否则ORM框架默认将其注解为@Basic
### 映射关系注解
1. 一对一单向外键关联

				该注解添加在副表中，默认级联关系，全级联。所以级联也是相对于副表的，
				如果是全级联，则删除副表数据，对应的主表数据也删除。反之则不然。
		@oneToOne(cascadType.All)
				指定外键，name的值是主表的主键
		@JoinColumn(name="",unique="true")

		只需要在副表对应的类中加入主表类型的属性，然后在该属性上添加如上两个注解。
		结果是在副表中有外键，参考主表的主键

		保存的时候必须先保存主表
2. 一对一双向外键关联

		副表对应的类配置同一对一单向外键关联。
		主表中添加副表类型的属性，然后在该属性上加
		@OneToOne(mappedBy = "person") 注解
		mappedBy的值是 副表中主表类型属性的属性值

	跟一对一单向外键关联的区别：
	无论查哪一方，都可以把对方的信息也查出来
3. 一对一单向外键联合主键

		大部分同一对一单向外键关联
		在联合主键类上添加注解@Embeddedd
		在主表类中引入联合主键类属性作为主键@Id
		同时在添加注解@EmbeddedId
4. 多对一单向外键关联

		多方持有外键，即多方持有一方的引用
		在多方添加一方类型属性，然后在该属性上添加注解
		@ManyToOne(cascade = CascadeType.ALL,fetch = FetchType.EAGER)
		@JoinColumn(name="外键")
		name就是一方的主键
		cascade是级联关系，fetch是抓取策略

		添加数据的时候要先添加一方，在添加多方
5. 一对多单向外键关联

		一方持有多方的集合
		在集合上添加注解
		@OneToMany(cascade = CascadeType.ALL,fetch = FetchType.LAZY)
		@JoinColumn(name="外键")
		name是一方的主键

		添加数据的时候要先添加多方，再添加一方
6. 一对多或多对一 双向外键关联

		即将多对一和一会多结合起来
		多方持有一方的引用，同时一方持有多方的集合  
		注意：多方配置积极加载，一方配置懒加载
7. 多对多单向外键

		只需要其中一方持有另一方的集合
		然后在该集合上添加注解

		@ManyToMany
		@JoinTable(name="中间表的名字",
		joinCloumns={@JoinCloumn(name="当前类的主键")},
		inverseJoinColumns={@JoinCloumn(name="另一个类的主键")})
8. 多对多双向外键关联
		
		（以学生跟老师为例）
		双方持有对方的集合对象
		其中一方设置
		//教师方，mappedBy的值是学生中教师集合的属性名
		@ManyToMany(mappedBy="teachers")  //交给学生方来控制
		另一方设置
		//学生方
		@ManyToMany
		@JoinTable(
		name="中间表的名字",
		joinCloumns={@JoinCloumn(name="当前类的主键")},
		inverseJoinColumns={@JoinCloumn(name="另一个类的主键")}
		)
		