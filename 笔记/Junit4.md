#Junit4
1. 测试方法上必须使用@Test修饰
2. 测试方法必须使用public void修饰，不能带任何修饰
3. 测试单元中的每个方法必须可以独立测试，测试方法间不能有任何依赖

		@Test
	    public void add() {
	        assertEquals(6, new Calculate().add(4, 2));
	    }

**注意：使用assertEquals必须import static org.junit.Assert.*;**


#Junit4测试流程
1. @BeforeClass修饰的方法会在所有的测试方法执行前被调用，且该方法是静态的，所以当测试类被加载后接着就会运行这个方法，而且内存中只会存在一份实例，它比较适合加载配置文件
2. @AfterClass同@BeforeClass，只是它修饰的方法会在最后执行，通常用来对资源进行清理
3. @Before和@After会在每个测试方法的前后各执行一次

#常用注解
1. @Test:将普通方法修饰为测试方法

		@Test(expected = XXX.class)捕获某种异常
		@Test(timeout = 毫秒)测试方法在指定时间内运行完，则不会报错，超过指定时间就会报错
1. @Before
2. @After
3. @BeforeClass
4. @AfterClass
5. @Ignore:所修饰的测试方法会被测试运行器忽略
6. @RunWith：可以更改测试运行器，继承org.junit.runner.Runner即可

#Junit4测试套件
测试套件就是组织测试类一起运行的  
1. 写一个作为测试套件的入口类，这个类里不包含其它方法  
2. 更改测试运行器Suit.class   
3. 将要测试的类作为数组传入到Suit.SuitClasses({})  

		@RunWith(Suite.class)
		@Suite.SuiteClasses({TaskTest1.class,TaskTest2.class,TaskTest3.class})
		public class SuiteClass {
		
		}

#Junit4的参数化设置
1. 更改默认的测试运行器为RunWith(Parameterized.class)
2. 声明变量来存放预期值和结果值
3. 声明一个返回值为Collection的公共静态方法，并使用@Parameters进行修饰
4. 为测试类声明一个带有参数的公共构造函数，并为变量赋值

		@RunWith(Parameterized.class)
		public class ParameterTest {
		    int expected = 0;
		    int input1 = 0;
		    int input2 = 0;
		
		    @Parameterized.Parameters
		    public static Collection<Object[]> t() {
		        return Arrays.asList(new Object[][]{
		                {3, 1, 2},
		                {4, 2, 2}
		        });
		    }
		
		    public ParameterTest(int expected, int input1, int input2) {
		        this.expected = expected;
		        this.input1 = input1;
		        this.input2 = input2;
		    }
		
		    @Test
		    public void addTest() {
		        assertEquals(expected, new Calculate().add(input1, input2));
		    }
		}