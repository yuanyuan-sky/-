#1.DispacherServlet（调度员Servlet）
#2.Controller
#3.HandlerAdapter
#4.HandlerInterceptor(拦截器)
#5.HandlerMapping
#6.HandlerExecutionChan
#7.ModelAndView
#8.ViewResolver(视图解析器)
#9.View

![avatar](..\imgs\1033.jpg) 

#SpringMVC拦截器

- 什么是拦截器？  

	    通过统一拦截从浏览器发往服务器的请求来完成功能的增强
- domo,解决乱码的过滤器

		web.xml
		<filter>
	        <filter-name>encoding</filter-name>
	        <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
	    </filter>
	    <filter-mapping>
	        <filter-name>encoding</filter-name>
	        <url-pattern>/</url-pattern>
	    </filter-mapping>

- 实现拦截器

		1、实现HandlerInterceptor接口
			public class MyInterceptor implements HandlerInterceptor {
			    @Override
			    /*
			    * 请求响应之前调用
			    * */
			    //返回值：标识是否要将当前的请求拦截下来
			    //如果返回false，请求将被终止
			    //如果返回true，请求会被继续进行
			    //Object handler:表示被拦截请求的目标对象
			    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
			        System.out.println("执行到了preHandle");
			        return true;
			    }
			
			    @Override
			    /*
			    * 在请求响应但是还没到达视图的时候调用
			    * */
			    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {
			        //可以通过modelAndView参数来改变显示的视图，或修改发往视图的数据
			        System.out.println("执行到了postHandle");
			    }
			
			    @Override
			    /*
			    * 在请求响应了且视图也响应后进行调用
			    * 该方法在请求的最后调用，主要进行一些资源的销毁
			    * */
			    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
			        System.out.println("执行到了afterCompletion");
			    }
			}
			
		2、将拦截器注册进SpringMVC框架中
			mvc-dispatcher-servlet.xml
			<!--  注册拦截器  -->
		    <mvc:interceptors>
		        <mvc:interceptor>
		            <mvc:mapping path="/filter/login"/>
		            <bean class="com.study.springMVC.interceptor.MyInterceptor"/>
		        </mvc:interceptor>
		
		    </mvc:interceptors>
		3、配置拦截器的拦截规则
			步骤2的<mvc:mapping...
- 配置多个拦截器，即如果有多个拦截器拦截同一个请求,方法执行顺序  
![avatar](..\imgs\1044.jpg) 

#拦截器的其它实现方式
1. 实现WebRequestInterceptor接口
#拦截器的使用场景
使用原则：处理所有的共同问题  
1. 解决乱码问题
2. 权限验证问题
#拦截器与过滤器的对比
1. 过滤器Filter依赖于Servlet容器，基于回调函数，过滤范围大；拦截器interceptor依赖框架容器，基于反射机制，只过滤请求
