#Java Web的发展史
- 第一阶段：javaBean+Servlet+JSP
- 第二阶段：面对EJB重量级框架带来的麻烦
- 第三阶段：SpringMVC/Struts+Spring+Hibernate+myBatis
- 第四阶段：SpringBoot
- 第五阶段：以Dubbo为代表的SOA微服务体系
- 第六阶段：SpringCloud微服务架构技术生态圈

#IOC
什么是IOC?

	Inversion of Control,控制反转
1. 控制什么？

		控制对象的创建及销毁（声明周期）
1. 反转什么？

		将对象的控制权交给IOC容器
#DI

	依赖注入
###把一个javaBean交由spring管理
1. 创建xml配置文件

		<?xml version="1.0" encoding="UTF-8" ?>
		<beans xmlns="http://www.springframework.org/schema/beans"
		       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
		       xsi:schemaLocation="http://www.springframework.org/schema/beans
		                     http://www.springframework.org/schema/beans/spring-beans-4.2.xsd
		                     ">
		        <!--  将一个Bean交由Spring创建并管理  -->
		        <bean id="bean" class="com.demo.Bean"></bean>
		</beans>
1. 获取spring上下文

		//获取spring上下文
        ApplicationContext context = new ClassPathXmlApplicationContext("spring.xml");
1. 获取Bean

		//获取一个bean
        Bean bean = context.getBean("bean", Bean.class);

#使用spring实例化Bean
	public class Bean {
	    public Bean() {
	        System.out.println("bean实例化了");
	    }
	}
	----------------------------------------
	public class Bean2 {
	    public Bean2() {
	        System.out.println("bean2实例化了");
	    }
	}
	------------------------------------------
	public class Bean2Factory {
	    public static Bean2 getBean2(){
	        return new Bean2();
	    }
	}
	-------------------------------------------
	public class Bean3 {
	    public Bean3() {
	        System.out.println("bean3 实例化了");
	    }
	}
	---------------------------------------------
	public class Bean3Factory {
	    public Bean3 getBean3(){
	        return new Bean3();
	    }
	
	}

		
1. 通过构造方法实例化Bean

		<bean id="bean" class="com.SpringIOC.bean.Bean" name="bean1_1,bean1_2"/>


2. 通过静态方法实例化Bean

		<!--  通过静态方法实例化bean  -->
    	<bean id="bean2" class="com.SpringIOC.bean.Bean2Factory" factory-method="getBean2"/>


3. 通过实例方法实例化Bean 

		<bean id="bean3Factory" class="com.SpringIOC.bean.Bean3Factory"/>
    	<bean class="com.SpringIOC.bean.Bean3" factory-bean="bean3Factory" factory-method="getBean3" id="bean3"/>

####Bean起别名
两种方式  
一、
	
	<bean id="bean" class="com.SpringIOC.bean.Bean" name="bean1_1,bean1_2"/>
	可以在name属性中起多个别名，用逗号隔开

二、

	<bean id="bean" class="com.SpringIOC.bean.Bean" name="bean1_1,bean1_2"/>
	<alias name="bean" alias="bean1_3"/>
	给bean起一个别名，name属性是bean的id


#注入Bean
		实例化一个bean
		<bean class="com.SpringIOC.lesson2.AnotherBean" id="anotherBean"/>
1. 构造方法注入

		<bean class="com.SpringIOC.lesson2.Bean" id="bean4">
			<!--index；构造方法中的第几个参数 name：参数名，type：参数类型
	            这三个参数不一定都得写，只要能标识出是第几个参数即可，参数类型都不相同，只是用type也可以
	            value:给基本类型赋值，ref：给自定义对象类型赋值
	        -->
	        <!--通过构造方法注入bean-->
	        <constructor-arg index="0" name="anotherBean" type="com.SpringIOC.lesson2.AnotherBean"
	                         ref="anotherBean"/>
	        <constructor-arg index="1" name="string" type="java.lang.String" value="aaa"/>
		</bean>
2. 通过set方法注入

		ref是关联另一个bean的id
		<bean class="com.SpringIOC.lesson2.Bean" id="bean4">
			<!--通过set方法注入bean-->
	        <property name="anotherBean1" ref="anotherBean"/>
			<property name="string1" value="bbbbb"/>
		</bean>


3. 给List属性注入

		<bean class="com.SpringIOC.lesson2.Bean" id="bean4">
			<property name="stringList">
	            <list>
	                <value>aaaa</value>
	                <value>bbbb</value>
	                <value>cccc</value>
	            </list>
	        </property>
		</bean>
		如果list的类型不是基本类型，把value标签换位ref标签
		<ref bean="beanId"/>
4. 给set属性注入

		<bean class="com.SpringIOC.lesson2.Bean" id="bean4">
			<property name="stringSet">
	            <set>
	                <value>11111</value>
	                <value>22222</value>
	            </set>
	        </property>
		</bean>
		如果set的类型不是基本类型，把value标签换位ref标签
		<ref bean="beanId"/>
5. 给Map属性注入


		<bean class="com.SpringIOC.lesson2.Bean" id="bean4">
			<property name="stringMap">
	            <map>
	                <entry key="ccccc" value="ddddddd"/>
	                <entry key="dddddd" value="ffffff"/>
	            </map>
	        </property>
		</bean>
		如果map的键或值不是基本类型，只要将相应的的key或value改为key-ref或value-ref
6. 给Properties属性赋值

		<bean class="com.SpringIOC.lesson2.Bean" id="bean4">
			<property name="properties">
	            <props>
	                <prop key="aaaaa">bbbbbbb</prop>
	            </props>
	        </property>
		</bean>
7. 赋NULL值

		<bean class="com.SpringIOC.lesson2.Bean" id="bean4">
			<property name="anotherBean2">
	            <null/>
	        </property>
		</bean>

#####构造注入和set注入的简便写法
	c:构造注入 p:set注入 
	<bean class="com.SpringIOC.lesson2.Bean" id="bean5"
    c:anotherBean-ref="anotherBean" c:string="ccccc"
    p:anotherBean1-ref="anotherBean" p:string1="dddddd"
    />

#Bean的自动装配
1. No：不做任何操作
2. byName：根据属性名自动装配，此选项将检测容器并根据名字查找与属性名完全一致的Bean，并将其与属性自动装配;调用的是set方法
3. byType：如果容器中存在一个与指定属性类型相同的Bean，那么将与该属性自动装配；如果存在多个该类型的bean，则抛出异常;调用set方法
4. constructor：与ByType方式类似，不同之处在于它应用于构造器参数

		public class AutowiringDao {

		}
		----------------------------------------
		public class AutowiringService {

    		private AutowiringDao autowiringDao;

		}
		---------------------------------------
		spring.xml
		<beans xmlns="http://www.springframework.org/schema/beans"
	       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	       xsi:schemaLocation="http://www.springframework.org/schema/beans
	                     http://www.springframework.org/schema/beans/spring-beans-4.2.xsd"

	                    default-autowire="byName">
					//byType、No、constructor、byType

		<bean class="com.spring.face.to.autowiring.AutowiringService" id="autowiringService"/>

    	<bean class="com.spring.face.to.autowiring.AutowiringDao" id="autowiringDao"/>
#####Spring Bean 的作用域
scop的默认值是单例模式  
1. Singleton作用域（单例模式）

		<bean class="com.SpringIOC.lesson3.Bean2" id="bean22" scope="singleton"/>		
		在同一个spring上下文中，多次请求同一个bean的实例，spring返回的都是同一个
2. prototype作用域（多例模式）

		<bean class="com.SpringIOC.lesson3.Bean2" id="bean22" scope="prototype"/>	
		每次想spring上下文请求这个实例，拿到的都是不同的实例

结论：如果 Bean1依赖于Bean2

		1、
		<bean class="com.SpringIOC.lesson3.Bean2" id="bean22" scope="prototype"/>
	    <bean class="com.SpringIOC.lesson3.Bean1" id="bean11" scope="prototype" >
	        <property name="bean2" ref="bean22"/>
	    </bean>
		Bean1和Bean2都是多实例的。则每次拿到的bean1都不相同，且它的属性bean2也都不相同；每次单独拿到的bean2也不相同
		2、
		<bean class="com.SpringIOC.lesson3.Bean2" id="bean22" scope="singleton"/>
	    <bean class="com.SpringIOC.lesson3.Bean1" id="bean11" scope="singleton" >
	        <property name="bean2" ref="bean22"/>
	    </bean>
		Bean1和Bean2都是单实例的。则每次拿到的bean1都是一样的，且它里面的属性bean2也都是一样的，每次拿的bean2也是一样的
		4、
		<bean class="com.SpringIOC.lesson3.Bean2" id="bean22" scope="singleton"/>
	    <bean class="com.SpringIOC.lesson3.Bean1" id="bean11" scope="prototype" >
	        <property name="bean2" ref="bean22"/>
	    </bean>
		Bean1是多例的，Bean2是单例的，则每次拿到的bean1都是不同的，且它的属性bean2是同一个；单独拿bean2也都是相同的
		3、
		<bean class="com.SpringIOC.lesson3.Bean2" id="bean22" scope="prototype"/>
	    <bean class="com.SpringIOC.lesson3.Bean1" id="bean11" scope="singleton" >
	        <property name="bean2" ref="bean22"/>
	    </bean>
		Bean1是单实例的，Bean2是多实例的，则每次拿到的bean1都是同一个，且它的属性bean2也是同一个；每次单独拿bean2都是一个新的实例
		
问题：如果Bean1是单实例的，Bean2是多实例的，但我想每次从bean1中拿到的bean2是不同的，怎么办的？  
######方法注入
	将Bean1进行改造
	public abstract class Bean1 {

	    protected abstract Bean2 createBean2();
	
	    public String printBean2() {
	       return createBean2().toString();
	    }
	}
	spring.xml
	<bean class="com.SpringIOC.lesson3.Bean2" id="bean22" scope="prototype"/>
    <bean class="com.SpringIOC.lesson3.Bean1" id="bean11" scope="singleton">
        <lookup-method name="createBean2" bean="bean22"/>
    </bean>
	则每次拿到的bean1都是相同的，但每个bean1里得到的bean2却不相同

	
		

3. Web环境作用域

		1、request作用域
			每个request请求都会创建一个单独的实例
		2、session作用域
			每个session都会创建一个单独的实例
		3、application作用域
			每个servletContext都会创建一个单独的实例
		4、websocket
			每个websocket连接都会创建一个单独的实例
4. 自定义作用域

		一：
		1、自定义一个Class，实现org.springframework.beans.factory.config.Scope接口
		2、在里面实现逻辑
		3、在spring.xml里先注册自己定义的class
			<bean class="com.SpringIOC.lession4.MyScope" id="myScope"/>
		4、将自己定义的Scope添加到spring的作用域了
		<bean class="org.springframework.beans.factory.config.CustomScopeConfigurer">
	        <property name="scopes">
	            <map>
	                <entry key="myScop" value-ref="myScope"/>
	            </map>
	        </property>
	    </bean>
		5、即可使用
		<bean class="com.SpringIOC.lession4.Bean" scope="myScop" id="bean66"/>
		二：spring还内置了一个自定义的作用域SimpleThreadScope
		<bean class="org.springframework.context.support.SimpleThreadScope" id="simpleThreadScope"/>

		<bean class="org.springframework.beans.factory.config.CustomScopeConfigurer">
	        <property name="scopes">
	            <map>
	               <entry key="simpleThreadScope" value-ref="simpleThreadScope"/>
	            </map>
	        </property>
	    </bean>
		这个作用域在在每个线程里创建一个新的实例，同意个线程只创建一个实例

#Bean的懒加载
- 默认情况下，Spring容器会在创建容器时提前初始化Singleton作用域的bean，即Spring在创建容器时，就会把所有的单例bean实例化。但是如果bean被标注了lazy-init="true"，则改bean只在其被需要的时候才会创建
- **只在singleton作用域有效**
- 该方法适用于为某个单例的Bean设定懒加载

为该配置文件里所有的单例的Bean设懒加载
		
		在beans标签里加上 
		default-lazy-init="true"

		<beans .....
		default-lazy-init="true" />
			.......
		</beans>

#Bean初始化及销毁逻辑处理
#####如果需要在Bean实例化后之后执行一些逻辑，有两种方法

1. init-method指定要执行的方法

		<bean class="com.SpringIOC.lession6.Bean" id="bean6_1" init-method="onInit" destroy-method="destroy"/>
2. 让Bean实现InitializingBean接口，实现其方法

####如果需要Bean在销毁之前执行一些逻辑，有两种方法
1. 使用destroy-method指定要执行的方法

		<bean class="com.SpringIOC.lession6.Bean" id="bean6_1" init-method="onInit" destroy-method="destroy"/>
2. 让Bean实现DisposableBean接口，实现其方法

**如果该配置文件中的每个Bean都需要在实例化之后执行一个方法，且方法名都相同；如果该配置文件中的每个Bean都需要在销毁之前执行一个方法，且方法名都相同；有个简便写法**

	<beans .....
		default-init-method="onInit"
		default-destroy-method="destroy" />
			.......
		</beans>

**以上三种初始化以及销毁逻辑，继承接口的优先级最高，如果三种都存在，先执行接口的，在执行bean的，beans的不会执行；**  
**beans里指定的方法不一定要存在；但是bean里指定的方法一定要存在**
#Bean属性继承
两种场景  
####场景1
Class1 和Class2有相同的父类ParentClass，且Class1和Class2都各自有自己的属性

	class parentClass{
		attribute1;
		attribute2;
	}
	------------------
	class 1 extent ParentClass{
		attribute4；
		attribute5；
	}
	----------------------------
	class 2 extent ParentClass{
		attribute7；
		attribute8；
	}

	如果class1和class2的公共属性的值相同，我们怎么给class1和class2的所有属性注入值呢？
	<bean class="class1" ...>
		<property name = "attribute1" value="..."/>
		...
		一个一个赋值
	</bean>
	class2的赋值同上
	---------------------------------------------
	现在有简便写法
	<bean class="ParentClass" id="parentClass" abstract="true">
        <property name="attribute1" value="..."/>
        <property name="attribute2" value="..."/>
    </bean>
	<bean class="class1" ... parent="parentClass">
		<property name = "attribute4" value="..."/>
		<property name = "attribute5" value="..."/>
	</bean>
	<bean class="class2" ... parent="parentClass">
		<property name = "attribute7" value="..."/>
		<property name = "attribute8" value="..."/>
	</bean>
#####场景2
Class1 和 Class2含有公共属性，且公共属性的值相同
	
	class Class1{
		attribute1;
		attribute2;
		attribute3;
	}
	class Class2{
		attribute1;
		attribute2;
		attribute4;
	}
	不用一个一个赋值
	<bean abstract="true" id="parentClass">
		<property name="attribute1" value="..."/>
		<property name="attribute2" value="..."/>
	</bean>
	----------------------------
	<bean class="Class1" parent="parentClass">
		<property name="attribute3" value="..."/>
	</bean>
	------------------------------
	<bean class="Class2" parent="parentClass">
		<property name="attribute4" value="..."/>
	</bean>

#springIoc注解得基本使用
#####实例化bean
1. 创建一个class配置文件，并添加注解Configuration

		class Bean1{
		
		}

		----------------------------------------
		@Configuration
		public class MyConfigration {
		
		    //将一个bean交由Spring创建并管理
		    //Bean(value="bean2") 起别名
		    @Bean
		    public Bean1 bean1() {
		        return new Bean1();
		    }
		}
		
		获取spring上下文
		ApplicationContext content = new AnnotationConfigApplicationContext(MyConfigration.class);
		//获取bean1  如果bean没有起别名，id默认是MyConfigration里的方法名
		Bean1 bean1 = context.getBean("bean1",Bean1.class);
		
		但是上面的方法太繁琐，下面是简便写法
		
		//将该class文件变为spring的配置文件
		@Configuration
		//扫描指定路径下，所有注解为Componet的Class，并将其实例化
		@ComponentScan(value = "com.springIoc4.two")
		public class Myconfigration {
			
		}
		----------------------------
		//@Conponent(value="bean2")起别名
		@Component
		public class Bean1 {

		}
		-----------------------------
		ApplicationContext content = new AnnotationConfigApplicationContext(MyConfigration.class);
		//获取bean1  如果bean没有起别名，id默认是类名首字母小写
		Bean1 bean1 = context.getBean("bean1",Bean1.class);

		以上两种都不需要spring.xml配置文件，下面这种需要spring的配置问价

		@Component
		public class Bean1 {
		    
		}
		-------------------------
		spring.xml
		<beans xmlns="http://www.springframework.org/schema/beans"
	       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	       xmlns:context="http://www.springframework.org/schema/context"
	       xsi:schemaLocation="http://www.springframework.org/schema/beans
	                     http://www.springframework.org/schema/beans/spring-beans-4.2.xsd
	                     http://www.springframework.org/schema/context
	                    http://www.springframework.org/schema/context/spring-context.xsd">
			扫描指定包下的所有注解为componte的Class，并将其实例化
		    <context:component-scan base-package="com.springIoc4.three"/>
		</beans>
		------------------------------------
		获取bean
		 ApplicationContext context = new AnnotationConfigApplicationContext(Myconfigration.class);
        Bean1 bean1 = context.getBean("bean1", Bean1.class);
        System.out.println("bean1 = " + bean1);

**component-scan和componteScan不只能扫描被注解为componte的class，还能扫描以下的注解**  
1. @Controller ：被标注在Controller层  
2. @Service：被标注在Service层  
3. @Repository:被标注在Dao层  
4. @Componetnt：通用型注解



#通过注解注入bean

@Autowired  
@AuAutowired(required = false):require的值默认是true，如果找不到能注入的类则会抛异常，等于false后则不会，找到相应的bean则注入，找不到则不注入  
每个类只能有一个构造器被标记为  required = true  
1. 通过方法注入Bean

		1、通过构造方法注入Bean
			@Component
			public class MyBean {
			    private AnotherBean anotherBean1;

				//将AnotherBean类型的bean自动注入进来
				@Autowired
			    public MyBean(AnotherBean anotherBean1) {
			        this.anotherBean1 = anotherBean1;
			    }
			}
			-----------------------------------------------------
			@Component
			public class AnotherBean {
			
			}
			----------------------------------------------------
			Configuration
			@ComponentScan("com.springIoc4")
			public class MyConfigruation {

			}
			
		2、通过set方法注入Bean
			@Component
			public class MyBean {

			    private AnotherBean anotherBean2;

				public AnotherBean getAnotherBean2() {
			        return anotherBean2;
			    }
			
				//将AnotherBean类型的bean自动注入进来
			    @Autowired
			    public void setAnotherBean2(AnotherBean anotherBean2) {
			        this.anotherBean2 = anotherBean2;
			    }
				
			}
			-------------------------------------------
			@Component
			public class AnotherBean {
			
			}
			----------------------------------------------------
			Configuration
			@ComponentScan("com.springIoc4")
			public class MyConfigruation {

			}

		3、通过属性直接注入
		
			@Component
			public class MyBean {

				@Autowired
			    private AnotherBean anotherBean2;
				
			}
			-------------------------------------------
			@Component
			public class AnotherBean {
			
			}
			----------------------------------------------------
			Configuration
			@ComponentScan("com.springIoc4")
			public class MyConfigruation {

			}
1. 给List注入值
		
			1、通过set方法注入
			@Component
			public class MyBean {
				private	List<String> stringList；
				
				@Autowired
			    //注入指定id的Bean
			    //@Qualifier("abc")
			    public void setStringList(List<String> stringList) {
			        this.stringList = stringList;
			    }
			}
		-------------------------------------------
		@Configuration
		@ComponentScan("com.springIoc4")
		public class MyConfigruation {
		
			//交由spring管理的一个List<String>类型的bean
		    @Bean
			//@Bean("abc")起别名
		    public List<String> stringList() {
		        List<String> list = new ArrayList<>();
		        list.add("111");
		        list.add("222");
		        return list;
	    }
			
	 	2、通过泛型注入
		@Component
		public class MyBean {
			
			//将string类型的bean自动注入进来
			@Autowired
			private	List<String> stringList；
		}
		------------------------------------
		@Configuration
		@ComponentScan("com.springIoc4")
		public class MyConfigruation {
		
		   @Bean
		   @Order(12)
		   public String string1(){
		       return "333";
		   }
		    @Bean
		    //order是指定注入顺序，值小的在前面
		    @Order(10)
		    public String string2(){
		        return "444";
		    }
	    }

		**上面list的两种注入方式中，下面的植入方式优先级高**
1. 给Map注入值

		1、通过set方法
			同list
		2、通过键值中的值
			@Component
			public class MyBean {

				@Autowired
				private Map<String, Integer> integerMap;
			}
			-----------------------------------------
			@Configuration
			@ComponentScan("com.springIoc4")
			public class MyConfigruation {
			
				//如果没有别名，键默认是方法名，有别名，键即为别名，值为返回值
			   @Bean("int1")
			    public Integer integer1() {
			        return 333;
			    }
			    @Bean("int2")
			    public Integer integer2() {
			        return 444;
			    }
		    }

1. 给简单类型注入值

		1、通过set方法
		@Component
		public class MyBean {

			private String string;
			@Value("555")
		    public void setString(String string) {
		        this.string = string;
		    }

		}

		
		2、直接注入
		@Component
		public class MyBean {

			@value("6666")
			private String string2;
		}
1. 给int类型注入

		同String，会将字符串转为int  


#@Resource注解
和@autowired注解一样，负责bean的自动注入，但是该注解有个name属性，可以指定注入bean的id，如果使用@autowired，则需要搭配@qualifier一起使用  
如果不指定那么属性，则注解在属性上，name的默认值为属性名，注解在set方法上，name的值为方法名


#通过注解设定Bean的作用域

	1、单例、多例、web作用域
	@Component("testBean2")
	@Scope("prototype")
	public class TestBean {
	
	}
	2、自定义作用域
		2.1自定义一个class实现Scope接口
		public class MyScope implements Scope {	
			....
		}
		2.2
		@Configuration
		public class TestConfiguration {
			//将MyScope交由Spring管理
			@Bean
		    public MyScope myScope() {
		        return new MyScope();
		    }
		
			//将MyScope添加到自CustomScopeConfigurer中，并交由spring管理
			@Bean
		    public CustomScopeConfigurer customScopeConfigurer() {
		        CustomScopeConfigurer configurer = new CustomScopeConfigurer();
		        configurer.addScope("myScope", myScope());
		        return configurer;
		    }
		}
		
	3.class1单例，内部属性多例，默认情况获取class1的实例，其属性都是一样的。使用方法注入，即可实现获取class1的实例都是单例的，但每一个class1里的属性都不一样
		
		@Component
		@Scope("singleton")
		public abstract class Bean {
		
		    @Lookup
		    public abstract AnotherBean anotherBean();
		
		    public void print() {
		        System.out.println("anotherBean = " + anotherBean());
		    }
		}
		-----------------------------
		@Component
		@Scope("prototype")
		public class AnotherBean {
		
		}
		

#通过注解实现Bean的懒加载

		第一种
		@Component
		@Lazy
		public class TestBean {
			
		}
		第二种
		@Configuration
		@ComponentScan("com.springIoc4")
		@Lazy //该配置文件实例化的所有bean都是懒加载
		public class TestConfiguration {
		
		    @Bean
		    @Lazy
		    public TestBean testBean() {
		        return new TestBean();
		    }
		}

#通过注解编写Bean初始化及销毁
两种方式
  
	1、实现InitializingBean和DisposableBean接口
	@Component
	public class TestBean implements InitializingBean, DisposableBean {
	
	    @Override
	    public void destroy() throws Exception {
	
	    }
	
	    @Override
	    public void afterPropertiesSet() throws Exception {
	
	    }
	    
	}
	2、@PostConstruct和@PreDestory
	
	@Component
	public class TestBean{

		@PostConstruct
	    public void Init() {
			
	    }
	    @PreDestroy
	    public void Destory() {
	
	    }

	}
	
	3、
	public class TestBean2 {

	    public void init() {
	
	    }
	
	    public void destroy() {
	
	    }
	
	}
	--------------------------------------
	@Configuration
	@ComponentScan("com.springIoc4")
	public class TestConfiguration {
	
	
	    @Bean(initMethod = "init",destroyMethod = "destroy")
	    public TestBean2 testBean2() {
	        return new TestBean2();
	    }
	}


#@importResources注解
1. 不使用注解读取properties文件

		properties文件；键=value的形式
		url = www.baidu.com
		password = 123456
		------------------------------------------
		public class PropertiesBean {
		    private String url;
		    private String password;
		    public String getUrl() {
		        return url;
		    }
		    public void setUrl(String url) {
		        this.url = url;
		    }
		    public String getPassword() {
		        return password;
		    }
		    public void setPassword(String password) {
		        this.password = password;
		    }
		}
		---------------------------------------------
		xml中；需要context命名空间
		<context:property-placeholder location="classpath:jdbc.properties"/>
	    <bean class="com.spring.face.to.properties.PropertiesBean" id="bean">
	        <property name="url" value="${url}"/>
	        <property name="password" value="${password}"/>
	    </bean>
1. 使用@ImportResources

		public class MyDriverManager {

		    public MyDriverManager(String url, String password) {
		        System.out.println("url = " + url);
		        System.out.println("password = " + password);
		    }
		}
		--------------------------------------------
		@Configuration
		@ImportResource(value = "classpath:spring.xml")
		public class Config {
		
		    @Value("${jdbc.url}")
		    private String url;
		
		    @Value("${jdbc.password}")
		    private String password;
		
		    @Bean
		    public MyDriverManager myDriverManager() {
		        return new MyDriverManager(url , password);
		    }
		}
		---------------------------------------------
		spring.xml
		<context:property-placeholder location="classpath:jdbc.properties"/>
		
**注意：properties中不要使用username作为键**  
@Value("${username}")
    private String username;//获取的操作系统当前登录的用户，不是properties文件中的username值
		




#Spring中的Aware接口

1. ApplicationContextAware接口

		获取Spring上下文
		public class MoocApplicationContext implements ApplicationContextAware {
			ApplicationContext context；
		    @Override
		    public void setApplicationContext(ApplicationContext applicationContext) throws BeansException {
				context = applicationContext；
		        System.out.println("applicationContext:"+applicationContext.getBean("moocApplicationContext"));
		    }
		}
		实例化这个bean即可获取spring上下文，方法会自动调用
1. BeanNameAware接口

		获取当前Bean的name
		public class MoocBeanName implements BeanNameAware {
    
		    @Override
		    public void setBeanName(String s) {
		        System.out.println("BeanName = " + s);
		    }
		}
		实例化这个Bean即可获取这个bean的name，方法会自动调用

#Resource
1. classpath:从classpath中加载
2. file:从文件系统中加载
3. url:网址中加载

		public class MoocResource implements ApplicationContextAware {

		    private ApplicationContext context;
		
		    @Override
		    public void setApplicationContext(ApplicationContext applicationContext) throws BeansException {
		        context = applicationContext;
		    }
		
		    public void resource() {
		        //Resource resource = context.getResource("classpath:config.txt");
		        //Resource resource = context.getResource("file:F:\\MyWorkSpace\\FaceToInterface\\src\\main\\resources\\config.txt");
		        Resource resource = context.getResource("url:http://www.nipic.com/show/8601959.html");
		        System.out.println("resource = " + resource.getFilename());
		
		    }
		}
		**不写前缀默认是从classpath中加载**