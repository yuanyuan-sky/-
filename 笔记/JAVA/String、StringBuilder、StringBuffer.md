#java.lang包
java内置得一个基础包，不用import

#构建字符串 
目的：是为了提高字符串操作的效率，比如拼接
	StringBuilder builder=new StringBuilder();//构建一个空的字符串构建器  
	builder.append("123");//想构造器中添加字符串  
	String s=builder.toString();//将StringBuilder对象转为字符串对象  
**注意**

	上面的代码用System.out.println(builder)也能输出构造器里的字符，但是，其输出的是StringBuilder对象，而不是字符串，如果想得到字符串，
	要使用.toString()方法或者+一个空字符串也行。
###StringBuilder重要的方法


1. .length(); 返回构造器中的字符数
2. .append(char | String);想构造器中追加一个字符串或者一个字符，并返回这个Stringbuilder对象
3. .setCharAt(int i,char c);将构造器中第i个字符替换为字符c（位置从0开始），无返回值
4. .insert(int i,String s | char c);在构造器的i位置上插入字符串s或者字符c，并返回这个Stringbuilder对象
5. .delete(int start ,int end);从构造器中删除从i位置到end位置（左闭右开）,并返回这个Stringbuilder对象
6. .deleteCharAt(int i);从构造器中删除i位置上的字符,并返回这个Stringbuilder对象
1. .toString();返回一个与构造器内容相同的字符串
2. .reverse();将构造器里的字符串反转
3. .charAt(i); 返回下标为i的字符
4. .replace(int start,int end ,String s);将从start开始到end的字符，替换为字符串s（不包含end）
5. .indexOf(String s);如果s是其字串，则返回s的首字母在其内的最小的下标，否则返回-1
6. .lastIndexOf(String s);如果s是其字串，则返回s的首字母在其内的最大的下标，否则返回-1
7. substring(int start,int end);截取其子串，从start到end（不包含end），如果没有end，则从start截到最后，注意：返回值是String

**注释：**在JDK5.0中引入StringBuilder类，这个类的前身是StringBuffer，其效率稍微有些低，但允许采用多线程的方式添加或删除字符串字符的操作，线程安全，如果所有字符串在一个单线程中编辑（通常都是这样），则应该用StringBuilder（线程不安全）。这两个类的API是相同的。
###StringBuffer和StringBuilder的区别
1. StringBuffer  支持并发操作，线性安全的，适合多线程中使用。
2. StringBuilder  不支持并发操作，线性不安全的，不适合多线程中使用。线程不安全，但其在单线程中的性能比 StringBuffer高。

#StringBuffer
字符串缓冲对象

#String 类

- java中字符串是String类的对象
- 构造方法
	
		1、String();创建一个空字符串
		2、String(String);新建一个字符串，作为指定字符串的副本
		3、String(char[] value);将根据字符数组，构建一个新字符串
		4、String(byte[] types);将通过转换指定的字节数组新建一个字符串
	
#字符串
###获取字符串的长度
	s.length();后面有（）；【注意与数组获取长度的区别】
	“中国”.length();  返回2
1. .substring(index1,index2);字符串截取，左闭右开

		一个参数时 substring(beginIndex);
		从beginIndex开始，到最后
**任何一个java对象都可以转变为字符串**
1. String.join("a","b","c",...)

		将b和c字符串以a字符串为分界符，连接起来
		String all=String.join("/", "a","b","c");
		结果：        a/b/c
1. s.charAt(n);获取字符串s下标为n的字符，返回值为char，当n>=s.length时，会报空指令异常  
**java中将String字符串称为不可变字符串，因为无法修改一个字符串中的字符，只能用截取、复制等生成新串操作**
 
1. .equals() 检测两个字符串是否相等

		不要使用==判断字符串是否相等，==只能判断两个字符串是否在一个位置上（String 是引用对象类型，==是比较栈里的值）
		String e="123";
		if (e.substring(0,2)=="12") {
			System.out.println("666");
		}
		这种情况，不会输出666
1. .equalsIgnoreCase();

		比较两个字符串是否相等，忽略大小写，返回true或false
1. int  .compareTo(String s);判断两个字符串是否相等

		如果相等就返回0，不相等的话，就比较两个字符串第一个不相同的字符的ASCII码的差值
		String a="ab";
		String b="ac";
		a.compareTo(b);返回  -1；因为b的ASCII码值减去a的ASCII值等于-1；
1. boolean  .startWith("b") ;.endWith("b");

		如果字符串是以b字符串开头或者结束的，返回true，否则false


1. int   .indexOf("s") ;  .lastIndexOf("s") 
	
		如果s是字符串的字串，则返回s的首字母在字符串中的位置，否则返回-1


1. String    .replace(char old,char new); 

		用new字符替换字符串中所有的old字符串
1. String     .replaceAll(Regex,new);

		接收一个正则表达式，换成new字符串
1. String     .trim();

		返回一个新串，将原始字符串首位的空格删除
1. concat();

		字符串拼接，返回一个新串
1. .contains(string s);

		判断字符串中是否含有字符串s,返回true或者false
		一个字符串.contains("");返回true
1. .isEmpty();

		判断一个字符串是否是空串，返回boolean
		String a="";
		a.isEmpty();  返回true
		-------------------------
		String b="         ";
		b.isEmpty();   返回false
		-------------------------
		String c=null
		c.isEmpty();    空指令异常
1. String[] .split(Regex);

		根据提供的正则表达式为分界符，将字符串转为数组
		注意有些符号需要转译，例如 .    //.

1. boolean   .matches(Regex);

		判断字符串是否与正则表达式匹配
1. String.valueOf(s)

		将s转变成字符串
		int i=10；
		String a=String.valueOf(i);  将i转变为字符串
1. .toCharArray();

		将字符串转为字符数组
		String a = "dmasjkndsa";
		
		char[] b=a.toCharArray();
		for (char c : b) {
			System.out.println(c);
		}
1. toUpperCase()/toLowerCase()

		小写转大写/大写转小写
1.String   .substring(start,end)

		截取字符串（左闭右开）
		substring(start) 从start截到最后
		
### 空串与Null串的区别

	String a="";
	String b=null;
	a是一个java对象，有自己的长度（0）和内容（空）
	b相当于没有new出对象，就是还没开辟出空间；
	null可以赋值给引用类型对象，不能赋给基本类型变量
	输入b  是null，但输入b.length();报空指令异常
**java中对null进行操作，会报空指令异常错误**


#字符串比较
- 基本类型比较：用==   0==0.0   1==1.0
- 对象类型比较

		==比较地址
		equals()比较两个对象的内容

		String a1="abc";//常量池
		String a2="abc";//常量池
		System.out.println(a1==a2); //true
		System.out.println(a1.equals(a2));//true
		
		String a3=new String("abc");//new  在堆中新开一个空间，空间的内容是abc
		System.out.println(a1==a3);  //false
		System.out.println(a1.equals(a3));//true

- 字符串中的+是concat（）方法的重载

**常量+常量还是常量**

		public static void main(String[] args) {

		/*while (true) {
			//后面的代码会报错，因为在编译的时候，true是常量，编译器会认为后面的代码永远不会执行
			
		}*/
		
		boolean flg=true;
		while (flg) {
			//不会报错
			
		}
		String a = "a" + "b"; // 常量计算
		String b = "ab";
		System.out.println(a == b);  //true

		String m = "a";
		String n = m + "b";//表达式运算ab ，计算的结果是一个新对象
		String k = m + "b";
		System.out.println(n == k);//false
	}
#=赋值与new对字符串赋值的区别
=赋值是从实例池中查找，如果有相同内容的，即引用使用，否则就初始化并存储到实例池；而new赋值，不管内容是否相同，都初始化一个新的字符串
