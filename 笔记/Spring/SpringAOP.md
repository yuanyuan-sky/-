#AOP
- 什么是AOP？

		Aspect Oriented Programming;面向切面编程
		通过预编译方式和运行期动态代理实现程序功能的统一维护的一种技术
####只要功能
		
		日志记录、性能统计、安全控制、事务处理、异常处理等等
#AOP实现方式
1. 预编译

		AspectJ
2. 运行期动态代理（JDK动态代理、CGLIB动态代理）

		Spring AOP 、JbossAOP

#AOP几个相关概念
1. 切面（Aspect）：一个关注点的模块化，这个关注点可能会横切多个对象
2. 连接点（Joinpoint）:程序执行过程中的某个特定的点
3. 通知（Advice）：在切面的某个特定的连接点上执行的操作
4. 切入点（Pointcut）:匹配连接点的断言，在AOP中通知和一个切入点表达式关联
5. 引入（Introduction）：在不修改类代码的前提下，为类添加新的属性和方法
6. 目标对象（Target Object）：被一个多个切面通知的对象
7. AOP代理（AOP Proxy）：AOP框架创建的对象，用来实现切面契约（aspect contract）(包括通知方法执行等功能)
8. 织入（Weaving）：把切面连接到其它的应用程序类型或者对象上，并创建一个被通知的对象，分为编译时织入、类加载时织入、执行时织入

#Advice（通知）的类型
1. 前置通知：在某连接点（join point）之前执行的通知，但不能阻止连接点前的执行，除非它抛出一个异常
2. 返回后通知：在某连接点正常执行后执行的通知
3. 抛出异常后通知：在方法抛出异常推出时执行的通知
4. 后通知：在某连接点退出的时候执行的通知
5. 环绕通知：包围一个连接点的通知

#基于配置的AOP（Schema——based AOP）
Spring所有的切面和通知器都必须放在一个<aop:config>内，可以有多个，每一个<aop:config>可以包含pointcut、advisor和aspect元素  
**它们必须按照这个顺序进行声明**

#pointcut

1. execution(public * *(..));切入点为执行所有public方法时
2. execution(*set*(..));切入点为执行所有set开始的方法时
3. execution(* com.xyz.service.AccountService.*(..))切入点为执行AccountService类中所有的方法时
4. execution(* com.xyz.service..(..))切入点为执行com.xyz.service包下的所有方法时
5. execution(* com.xyz.service...(..))切入点为执行com.xyz.service包及其子包下的所有方法时

**以上的在springAOP和aspectJ中都支持，下面的只有spring支持**
1. within(com.xyz.service.*)
2. within(com.xyz.service..*)
3. this(com.xyz.service.AccountService)

	within用于匹配指定类型内的方法执行
	this用于匹配当前AOP代理对象类型的执行方法
**pointcut有很多，使用时再查找吧**


#Advice的使用

	public class AspectBiz {

	    public void  biz() {
	        System.out.println("AspectBiz");
	        throw new RuntimeException("");
	    }

		public void init(String bizName, int times) {
	        System.out.println("AspectBiz:init=" + bizName + " " + times);
	    }
	}
	--------------------------------------------
	public class MoocAspect {

	    public void before() {
	        System.out.println("MoocAspect:before:");
	    }
	    public void afterReturning() {
	        System.out.println("MoocAspect:afterReturning");
	    }
	
	    public void afterThrowing() {
	        System.out.println("MoocAspect:afterThrowing");
	    }
	
	    public void after() {
	        System.out.println("MoocAspect:after");
	    }

		public Object around(ProceedingJoinPoint pjp) {
	        Object o = null;
	        try {
				//这句输出会在切点中的方法执行之前执行
	            System.out.println("MoocAspect:around 1");
	            o = pjp.proceed();
				//这句输出会在切点中的方法执行之后执行
	            System.out.println("MoocAspect:around 2");
	        } catch (Throwable throwable) {
	            throwable.printStackTrace();
	        }
	        return o;
	    }

		public Object aroundInit(ProceedingJoinPoint pjp,String bizName,int times) {
	        System.out.println("bizName = " + bizName + "and times = " + times);
	        Object o = null;
	        try {
	            System.out.println("MoocAspect:aroundInit 1");
	            o = pjp.proceed();
	            System.out.println("MoocAspect:aroundInit 2");
	        } catch (Throwable throwable) {
	            throwable.printStackTrace();
	        }
	        return o;
	    }
	}
	
	---------------------------------------------------------
	spring.xml
	<bean class="com.spring.aop.advice.MoocAspect" id="moocAspect"/>
    <bean class="com.spring.aop.advice.AspectBiz" id="aspectBiz"/>

    <aop:config>
        <aop:aspect id="moocAspectAOP" ref="moocAspect">
			<!--切点：AspectBiz类中的所有方法-->
            <aop:pointcut id="moocPiontcut" expression="execution(* com.spring.aop.advice.AspectBiz.*(..))"/>
			**注意：execution中第一个*号后有一个空格**

			<!--当切点的方法执行之前，会先执行切面中的before方法-->
            <aop:before method="before" pointcut-ref="moocPiontcut"/>

			<!--当切点的方法执行return之后，执行切面中的afterReturning方法-->
            <aop:after-returning method="afterReturning" pointcut-ref="moocPiontcut"/>
			
			<!--当切点中的方法抛出异常之后，执行切面中的afterThrowing方法-->
            <aop:after-throwing method="afterThrowing" pointcut-ref="moocPiontcut"/>

			<!--当切点中的方法执行之后，执行切面中的after方法-->
            <aop:after method="after" pointcut-ref="moocPiontcut"/>
			<!--环绕通知，当切点中的方法执行之后，执行切面中的around方法-->
			<aop:around method="around" pointcut-ref="moocPiontcut"/>
			**注意：around方法的第一个参数的类型必须是ProceedingJoinPoint，且方法要返回ProceedingJoinPoint对象的proceed()方法的返回值**
			
			<!--带参环绕通知-->
			<!--当AspectBiz类中的init(string,int)方法执行时,会执行切面中的aroundInit方法，且aroundInit方法要有bizName和times参数，且类型顺序要和init方法的参数顺序一样-->
			<aop:around method="aroundInit" pointcut="execution(* com.spring.aop.advice.AspectBiz.init(String,int))
                and args(bizName,times)"/>
        </aop:aspect>
    </aop:config>

	**需要aspectjrt、aspectjweaver的jar**

###Introductions
在不改变类的代码的前提下，给类增加一个方法

	public interface Fit {
	    void filter();
	}
	-------------------------------
	public class FitImpl implements Fit {

	    @Override
	    public void filter() {
	        System.out.println("FitImpl.filter");
	    }
	}
	--------------------------------------
	spring.xml
	<bean class="com.spring.aop.advice.MoocAspect" id="moocAspect"/>
    <bean class="com.spring.aop.advice.AspectBiz" id="aspectBiz"/>
	 <aop:config>
        <aop:aspect id="moocAspectAOP" ref="moocAspect">
			<!--给advice包下的所有类增加一个FitImpl父类，改父类实现Fit接口-->
            <aop:declare-parents types-matching="com.spring.aop.advice.*"
                                 implement-interface="com.spring.aop.advice.Fit"
                                    default-impl="com.spring.aop.advice.FitImpl"/>
        </aop:aspect>
    </aop:config>
	-------------------------------------
	测试
	@Test
    public void test() {
        ApplicationContext context = new ClassPathXmlApplicationContext("spring.xml");
        Fit fit = (Fit) context.getBean("aspectBiz", AspectBiz.class);
        fit.filter();
    }

**注意：配置文件中的aspect只支持单例模式的Bean**


#Spring中配置AspectJ

1. XML配置文件的方式

		<aop:aspectj-autoproxy />

1. java风格的配置

		@Configuration
		@EnableAspectJAutoProxy
		public class ....{}

一个类中的@Aspect注解标识它为一个切面，并且将自己从自动代理中排除 
 
**注意：@Aspect注解是不能够通过类路径自动检测发现的，所有需要配合使用@Component注解或者在xml配置bean**

####pointcut
一个切入点通过一个普通的方法定义来提供，并且切入点表达式使用@Pointcut注解，方法返回类型必须为void

		@Component
		@Aspect
		public class MoocAspect {
			//定义一个切点
		    @Pointcut("execution(* com.spring.aop.aspectj.*Biz.*(..))")
		    public void pointcut(){
		        
		    }

			//Advice
			@Before("pointcut()")
		    public void before1(){
		        System.out.println("Before....");
		    }

			//Advice，不使用切点，直接在advice上的注解上声明什么时候调用该advice
			@Before(""execution(* com.spring.aop.aspectj.*Biz.*(..))"")
		    public void before2(){
		        System.out.println("Before....");
		    }

			//advice，returnValue是真正的方法执行的返回值，该例中为"Save success"
			@AfterReturning(pointcut ="pointcut()",returning = "returnValue")
		    public  void afterReturning(Object returnValue) {
		        System.out.println("AfterReturning"+returnValue);
		    }

		}

		-------------------------------------------------------------
		@Service
		public class MoocBiz {
		
		    public  String save(String arg){
		        System.out.println("MoocBiz save:" + arg);
		        return "Save success";
		    }
		}

		-------------------------------------------------------------
		spring.xml

		<context:component-scan base-package="com.spring.aop.aspectj"/>

    	<aop:aspectj-autoproxy></aop:aspectj-autoproxy>


##向advice传递参数

		其它代码同上

		@Before("pointcut() && args(arg)")
	    public void before(String arg){
	        System.out.println("Before...." + arg);
	    }
		arg在本例中即为"Save success"
