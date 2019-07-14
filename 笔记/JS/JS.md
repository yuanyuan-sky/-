#变量
##变量的声明
	
1. 先声明后
8.    var a;   a=11；
2. 同时声明和赋值   var b=11；
3. 不声明直接赋值     c=20；
4. 同时多个赋值   var t,n,m=20;   **注意：**这个时候只有m为20，t和n都为undefiend；（undefiend:是变量的默认类型，代表未定义值，var a;  a就是undefiend类型） 
   
		变量的重名规则：如果重名的变量都有赋值表达式，则后面的会覆盖前面的变量，如果前面的有赋值表达式，而后面的没有则后面的无效；
		**注意：**变量名对大小写敏感，大小写是不同的变量
		起名规范：必须以【字母】、【下划线】、【美元符号】开头，后面可以跟数字，字母，下划线，美元符号；不能使用js的关键字和保留字作变量名
		
##变量的生命周期
###全局变量的声明	
1. 显式声明：在方法外面使用var 声明的变量都是全局变量
2. 隐式声明：不用var，直接给变量赋值，即使该变量在一个方法内部，当该方法执行后，该变量就会变为全局变量；这种方式相当于window.test;test就是全局变量  
4.方法里使用var声明的变量，只在方法里有效，方法外无法访问  
**注意：**在循环表达式中或者循环表达式的{}中定义的变量，在{}外也可以访问  

		for (var i=0;i<5;i++){
		    var a = i;
		}
		console.log(i);
		console.log(a);
		i和a在循环外部都可以访问
5.变量的提升
	
		var a2 = 1;
    	function abc() {
	        console.log(a2);
	        var a2 = 10;
	        console.log(a2);
    	}
    	abc();
		打印的结果：undefined   10;
为什么会有这种结果：js的【方法中】，用var生明的变量，无论在哪个地方声明，都会把变量提升到方法的最上面进行声明，然后在具体的位置赋值;所以在上面的例子中，相当于在方法最开始声明了a2，然后在下面赋值，所有第一次打印的是undefined

#数组
###数组：一组相同或不同数据类型的容器
###js数组与java数组的区别
	
1. js数组对象是由js编写的本地容器
2. js数组的长度可以变化
3. js数组的存储类型可以为不同的数据类型
###js数组与java数组的相同点
	
1. 功能相同，都是存储介质
2. 操作相同，都需要遍历数组的内容，同时提供了许多修改数组内容的方法
###数组的重名规则
- 如果两个数组都进行了赋值，则后面的会覆盖前面的，如果前一个赋值而后面的没有赋值，则后面的无效
###数组的声明方式
1. var array=new Array();声明一个数组   array[0]=1;array[1]=2;
2. var array=new Array(1,2,3,4);
3. var array=[1,2,3,4];
###数组的方法
1. .reverse();颠倒数组的顺序，数组本身发生变化
2. .sort();对数组进行升序或者降序排序，数组本身发生变化  
		
		var a=[1,2,100,3,,200];  a.sort();  得到的是[1,100,2,200,3];
		sort()方法如果想进行升序排序，必须提供一个参考函数
		var a=[1,2,100,3,200];
		    console.log(a.sort(function (a,b) {
		        return a - b;
		    }));
			这个时候返回的是[1,2,3,100,200]
		var a=[1,2,100,3,200];
		    console.log(a.sort(function (a,b) {
		        return b - a;
		    }));
			这个时候返回的是[200,100,3,2,1]
1. join();将数组元素通过指定字符连接，返回一个字符串，原数组不变
		
		var a=[1,2,3]; a.join("-");返回一个字符串 "1-2-3"
1. toString();将数字转换为字符串

		var a=[1,2,3]; a.toString();  1,2,3   **注意：**会保留数组的分隔符  ,
1. concat();用于连接两个或多个数组，也可以在数组中追加元素
	
		var a=[1,2,3];a.concat(4,5); [1,2,3,4,5]
		b=[4,5,6];var c=[7,8,9];
		a.concat(b,c);    [1,2,3,4,5,6,7,8,9]
1. pop();删除并返回数组的最后一个元素，改变原数组
	
		var a=[1,2,3];  a.pop();   返回3  a=[1,2]
1. shift();删除并返回数组的第一个元素，其它同pop()

2. push();向数组的末尾添加一个或多个元素，返回添加后数组的长度	
		
		var a=[1,2,3]; a.push(6,7);  返回 5   a=[1,2,3,6,7]
1. unshift();在数组的头部添加一个或者多个元素,返回添加后数组的长度，同push（）
2. slice(start,end);返回一个新的数组，包含从数组的start位置开始，到end（不包含end，左闭右开），如果参数为负值，则代表从后向前数，-1代表最后一个位置，该方法不会改变原数组
	
		var a=[1,2,3,4,5,6];
		a.slice(2,4);    返回[3,4]
1. splice(index,howmany,element1,element2....)用于插入、删除或者替换数组中的元素，从index位置开始（包含index位置），删除howmany个元素，再从index位置开始，插入element(可选参数)元素，可以插入多个，原数组发生变化，返回的是一个含有元素组中被删除的元素的新数组
	
		var a = [0,1, 2, 3, 4, 5, 6, 7];
    	console.log(a.splice(2,2,66));返回[2,3]  a=[0,1,66,4,5,6,7]
		var a = [0,1, 2, 3, 4, 5, 6, 7];
		console.log(a.splice(2,2));返回[2,3]  a=[0,1,4,5,6,7]
#字符串的方法
**字符串的所有方法都不会改变字符串本身**  
1. length；获取字符串长度，**注意：**后面没有（）   
2. indexOf()/lastIndexOf();第一次/最后一次字符出现的位置

		var a="abcde"; a.indexOf("b");  返回1
		若果查找的为多个字符，以第一个字符为准
		a.indexOf("bcd"); 返回1 
		a.indexOf("5bc");返回-1
1. toUpperCase()  小写变大写
2. toLowerCase()  大写变小写
3. replace("old","new");替换字符串中的字符,把old字符换为new字符，原字符串不变，返回替换后的字符串，如果要替换的字符串在原字符串中不存在，则返回原字符串

		var a="abcd";
		a.replace("bc","5");返回"a5d";   a="abcd"；
		a.replace("kk","5");返回"abcd"	a="abcd";
1. substr(start,number);从start位置开始截number个，返回截取的字符串，原字符串不变
	
		var a="abcde";
		a.sunstr(2,2); 返回cd   a="abcde"
1. substring(index1,index2)；从index1位置截到index2位置，不包括index（左闭右开）返回截取的字符串，原字符串不变
2. concat()连接多个字符串，返回连接后的新字符串，原字符串不变**注意：**跟+一样
3. search（）在字符串中查找指定字符串，如果找到，返回匹配的第一个字符在原字符串中的位置，找不到返回-1
4. split（）去掉字符串中指定的字符，然后转变为数组，转变的数组元素以去掉的字符为间隔，转变为数组的元素，原字符串不变，返回一个数组,
	
		var a="a-b-c-d-e";
		a.split("-");   返回["a","b","c","d","e"]  a不变
		var b="abcdef";
		b.split("c");  返回["ab","def"];
		**注意：**只能去掉一类型的元素，可以去掉【连着】的字符串
		var r="abcdefg";
		r.split("cdef"); 返回["ab","g"]
1. eval()把字符串转换为表达式进行计算，根据四则运算法则进行计算

		var a="1+2*3";   eval(a);   得7


1. charAt(index)返回在指定位置的字符  
2.slice（start,end）;字符串截取 
**字符串反转**s.split("").reverse().join("");
		
#Math 方法
	
1. Math.abs(x);  返回x的绝对值
2. Math.ceil(x);  对x进行上舍入，返回一个大于或等于x的整数  5.1  返回6
3. Math.floor（x）;对x进行下舍入 ，返回一个小于会等于x的整数  5.6  返回5
4. Math.min(x,y,z);返回最小的参数（只能用于数字），如果没有值返回infinity,如果存在NAN，返回NAN   
5. Math.max();  返回参数中的最大数
6. Math.pow(x,y) 返回x的y次幂
7. Math.random();返回0~1之间的随机数  [0,1) 不包含1，左闭右开
8. Math.round(x);对x进行四舍五入，不影响原数字(四舍五入只算小数点后第一位，大于5进1，小于5不变)


		
#运算符
	**注意：** js的除法不自动取整
	算术运算符：+ - * / %  ++   --   
	赋值运算符：=  +=  -=  *=   /=   %=   
	比较运算符： ==  ===  !=  >   <   >=   <=   (===比较的是值和类型，==只比较值)
	逻辑运算符：&&   ||   ！
	条件运算符：元素符  ？ :     2>1?"a":"b";
	**注意：**逻辑运算符也可以连接其他类型的数据，运算前js引擎会对运算双方执行new Boolean(data)的数据转型，转型后执行逻辑比较
	**注意：**在进行逻辑&&运算时，只要前面的为假，就不会去判断&&符号后面的表达式，在逻辑||中，只要前面的为真，就不对后面的表达式进行运算
#循环
###for
	1. for(var i=0;i<10;i++){}
### forEach
	2. array.forEach(function(value,[index],[array]){
			value 是值，index是下标，array是原数组，（不会变）
		});
	**缺点：**不能使用break语句终端循环，也不能使用reture语句返回到外层函数
###for   in
	
	3. for (var index in myArray) { 			// 千万别这样做
  			console.log(myArray[index]);	
		}  
         这里的下标不是整数下标0，1，2，而是字符串“0”，“1”，“2”；for in可以遍历对象的属性，所有通常用来遍历对象
		for…in会遍历到自定义属性甚至原型属性、index是字符串而不是数值、某些情况下甚至不按顺序遍历
###for   of
	4.for(var value  of  array){
	
	}
	**优点：**1.这是最简洁、最直接的遍历数组元素的语法
				2.这个方法避开了for-in循环的所有缺陷
				与forEach()不同的是，它可以正确响应break、continue和return语句
			3.for-of循环也可以遍历其它的集合
			  for-of循环不仅支持数组，还支持大多数类数组对象，例如DOM NodeList对象。
			  for-of循环也支持字符串遍历，它将字符串视为一系列的Unicode字符来进行遍历：
#数据类型
###5种基本类型，除了5种基本类型外，其它都是对象（Object）
###string，number，boolean，undifiend,null
	string:单引，双引都是字符串，空格也是字符串，字符串中有几个空格就是几个空格
	number：整数和浮点数   NaN和Infinity
	boolean:true/false
	undefined:变量声明后没有赋值，变量的默认赋值；**注意：**一个没有声明的变量，使用typeof，返回的类型也是undefined。
	null：使用typeof,返回的结果是object
###object类型
	js中的对象，数组，null
###function类型
###null和undefined的区别
	undefined定义了没赋值，null占空间，undefined不占空间，null可以参与运算，undefined不可以
###对象数据类型：
	非基本类型的都是对象数据类型
###注意
		NaN  ==  NaN  false
		null ==  object   true
		null ===  object   false
		undefiend和not defiend不一样，前者是声明了变量没有赋值，后者是变量不存在
#日期对象
	
1. 创建日期对象
	
		var date=new Data();
1. 当前是几号
	
		var day=data.getDate();
1. 几天星期几

		var day=date.getDay();  
		(0~6) 星期日是 0
1. 获取当前的月份
	
		var day=date.getMonth();
		获取当前的月份，从0开始
1. 获取当前的年 

		var day=date.getFullYear();
1. 获取当前的年份减去1900

		var day=date.getYear();
1. 获取当前的毫秒

		var day=date.getMilliseconds();

1. 获取1970年1月1日到现在的毫秒数

		var day=data.getTime();
1. 获取当前的小时

		var day=date.getHours();24小时制
1. 获取当前的分钟

		var day=date.getMinutes();
1. 获取当前的秒

		var day=date.getSeconds();
#自定义对象
	
		var person={
			name:"Tom",
			age:"20",
			eat:function(){
				alert("吃菜")；
			}
		}
**注意：对象的赋值是地址引用，即使作为函数参数，也是地址引用**
#函数
##系统函数


1. parseInt(string , [radix]);  转为Int

		string:要被解析的字符串
		radix:可选，要被解析的数字的基数。该值介于2~36之间。如果省略该参数或该参数为0，则数字将以10为基础来解析。如果它以0X或0x开头，将以16为基数。如果该参数小于2或者大于36，则parseInt将返回NAN；
		parseInt允许字符串开头和结尾有空格
		如果string的第一个字符不能转换为数字（正负号除外），将返回NaN，否则直到第一个不能转换为数字的字符之前的字符将转换为整数

		var a= parseInt("12px"); 返回12
		var b=parseInt("px12");  返回NaN
		若果字符串是以0x或0X,则后面的数字会当成16进制数
		var c=parseInt("0X14");  返回20；  16进制的14==十进制的20
		

		
2. parseFloat(); 转为浮点数

		parseFloat("1.1.1")  返回1.1
		parseFloat（"a1.1"）  NaN
		parseFloat("1.1a")   1.1
3. isNaN();判断是否【不是】数字 ，不是数字返回true，是数字返回false
4. typeof();获取变量的类型;可能的返回值：undefined,boolean,number,string,object
5. instanceof  判断一个变量是否是对象  

		d1 instanceof Date  判断d1是否是Date类型，返回true或false
		typeof（d1）获取d1的类型，返回值是小写的类型  number
##自定义函数
	
1. 普通函数

		function fname(parameter1,parameter2..){
			要执行的代码
		}
1. 匿名函数（没有名字）

		类似window.onload=function(){
			要执行的代码
		}
1. 函数表达式

		var a=function(){
			要执行的代码
		}
1. 内部函数

		function(){
			function(){
			
			}
		}
1. Function对象
	
		var b=new Function('a','b','return a+b');



1. 函数的重名规则

	如果一个网页中出现多个同名函数（不区分参数），则后定义的函数覆盖前面定义的函数

**注意：js无法用参数区分函数，只要函数名正确就行，不传参数也可以调用有参函数**
#JS的引入方式
1. 嵌入式引入

		<script type="text/javascript">
	
		</script>
1. 外部文件方式引入

		<script src="js/test.js" type="text/javascript" >
		</script>
1. 事件方式引入，例如onclick事件

		<button onclick="alert("aa");">点击</button>
#计时器
	
1. setInterval("function",time);
	
		time是毫秒，一秒等于1000毫秒
		每隔time毫秒执行一次function函数
		如果想停止setInterval,需要将setInterval赋给一个变量，使该变量成为setInterval得持有者然后调用clearInterval(mm);即可停止mm定时器
1. setTimeout(function,time);

		隔time毫秒执行一次function方法，只执行一次
#document访问基本元素DOM对象的方式
1. document.documentElement:获取整个网页的dom对象 即`<html>...</html>`  
2. document.doctype:取HTML文档的文档头字符 网页最开头的 <!DOCTYPE html>
3. document.body:获取body的dom对象
4. document.head:获取head标签的dom对象
5. document.title:获取title的文字标题
#document访问文档内子节点DOM对象的方式
1. 根据id获取符合DOM第一个对象，获取不到返回null

		document.getElementById('id');
1. 根据标签名（忽略大小写）获取全部该标签对象的【数组】

		doument.getElementsByTagName("tagName");
1. 根据name属性获取全部该标签的对象数组

		document.getElementsByName("name");
1. 根据类名属性获取全部使用了该类的标签


		document.getElementsByClassaName("className");
1. 根据选择器获取，只能获取第一个

		document.querySelector(".类名")；
1. 对于form表单（如下即可获得表单内标签的DOM对象）

		document.formName.input标签的Name;获取form表单中的标签	
		document.forms[0];获取第一个form对象
		document.all

#节点（node）对象        
- Node对象是其它节点对象的父类，因此其它节点类型对象都具备Node对象的属性和方法
- 基本属性

	
		1.nodeType:节点类型
		2.nodeName：节点标签名（大写）
		3.nodeValue：节点值
##父子关系属性：用于访问当前节点的祖辈或后代元素的属性
1. parentNode:当前元素的父DOM节点
2. firstChild：当前元素的第一个子节点对象（如果后面有回车或者空格，则获取的是回车和空格）
3. lastChild:当前元素的最后一个字节点对象，如果最后面有空格或者回车，则获取的是空格和回车
4. childNodes:当前元素的【子节点】对象（伪数组），只获取一级子标签，跟孙子没关系
5. children:当前元素的所有【子节点】（数组），只获取一级子标签，跟孙子没关系

**注意：childNodes、lastChild、firstChild会连空格和回车都获取，children不会获取空格和回车**
##window对象
**window是js层级中得最顶层对象**  
1. alert("");提示框，标准写法是window.alert();  
2. confirm("");确认框，返回true或者false  
3. prompt();输入框，返回一个输入的值  
4. screen();获取屏幕的信息  

		availHeight:680  有效高度（实际高度-任务栏高度）
		availLeft:0
		availTop:0
		availWidth:1280
		colorDepth:24
		height:720			实际高度
		orientation:ScreenOrientation {angle: 0, type: "landscape-primary",onchange: null}
		pixelDepth:24
		width:1280
#window的尺寸
1.window.innerHeight;浏览器窗口的内部高度
![](https://i.imgur.com/SoNukAQ.png)
![](https://i.imgur.com/xYHmoDj.png)  

2.window.innerWidth;浏览器窗口的内部宽度(不包括滚动条的宽度)


###会有兼容行问题
※对于Internet Explorer、Chrome、Firefox、Opera 以及 Safari：

window.innerHeight - 浏览器窗口的内部高度  
window.innerWidth - 浏览器窗口的内部宽度
※对于 Internet Explorer 8、7、6、5：

document.documentElement.clientHeight  
document.documentElement.clientWidth  
或者  
document.body.clientHeight  
document.body.clientWidth  
**实用的JS方案，涵盖所有浏览器**  
var w=window.innerWidth
|| document.documentElement.clientWidth
|| document.body.clientWidth;（所有的浏览器获取宽度）

var h=window.innerHeight
|| document.documentElement.clientHeight
|| document.body.clientHeight;（所有的浏览器获取高度）
3.document.body.scrollHeight;||document.documentElement.scrollHeight.获取整个网页的高度  
4。document.documentElement.scrollTop;获取页面滚动条滚上去的高度
##window树

![](https://i.imgur.com/rQBZxak.png)


	
##获取和设定css属性
	document.getElementById("#div1").style.color="red";
##查看和修改节点属性
1. 查看属性

		document.getElementById("#div1").getArrtribute("src");
1. 修改属性

		document.getElementById("#div1").setAttribute("src","../img/1/png");
**注意：**
			
		※对于checkbox的selected属性，不使用getArrtribute和setAttribute，而是使用.checked
		checkedboxObj.checked; 选中的返回true，没选中的返回false
		使checkedbox被选中checkedboxObj.checked=true；不选中checkedboxObj.checked=false；
		※ 单选按钮和checkbox一样
		※ 对于下拉列表框select
			selecteObj.selectedIndex； 回去当前选中项的索引
			selectObj.options[index].value() 即可获取当前选中项的值

#注释
1. 单行注释   //
2. 多行注释   /* */
#JS事件类型
### 常用的窗口事件
1. onload:window对象、document对象、图片对象、外部文件完全加载事件
		
		window.onload=function(){
			在文档内内容全部加载后调用响应函数
		}
		window.addEventListener("load",function(){
				在文档内内容全部加载后调用响应函数
		});
		上面两个方法是一样的
1.onunload 用户退出界面
###常用的焦点事件
1. focusout:失去焦点事件
2. focusin:获得焦点事件
3. blur：老版本的失去焦点的事件  ==   focusout
4. focus：老版本的获得焦点的事件 ==focusin
###鼠标事件
1. click：鼠标点击后抬起事件
2. dblclick：鼠标双击事件
3. mousedown:鼠标左键被按下事件
4. mouseup:鼠标左键被抬起事件
5. mouseover:鼠标移动到某对象身上时触发的事件
6. mouseout：鼠标离开某对象时触发的事件
7. mousemove：鼠标在某对象上面移动时触发的对象
### 键盘事件
1. keydown：当键盘按下时调用，如不松手则反复调用（非输入按键只调用一次），输入中文时，每次都会调用
2. keyup：当键盘松开时调用
3. keypress：与keydown相同，但对于非字符输入不调用

#事件流
	
	事件流：浏览器在执行事件相应程序的顺序
#HTMl代码\文本\值
	
1. .innerHTML
	
		获取闭合标签的值或者html代码
		赋值使用.innerHTML="";
1. .innerText();
1. .value

		获取标签的value值
		赋值使用value="";
#DOM和BOM
DOM是文档对象类型；BOM浏览器对象模型
#BOM
###location对象
	window.location.href：浏览器当前地址，也可以进行跳转
	window.location.href="http://www.baidu.com"; 跳转到百度
###navigator:浏览器对象，用于获取当前浏览器信息。还能获取定位对象，获取经纬度
###history:历史
	history.go(0);刷新当前页面
	history.go(-1)后退一步 = history.back()
	history.go(1)前进一步
##open 打开一个网址，参数太多，百度吧

###DOM对象的类型
1. 文档类型：文档全局对象document
2. 节点类型：也称为元素类型
3. 文本类型：节点类型下的文字内容对象
#绑定事件流
###html级别绑定事件流
	
	<button onclick="aaa()">点击</button>
	在html中内嵌js程序，不符合DOM标准

###DOM0级别绑定事件流
- 将响应程序直接赋给DOM元素的事件类型
	
		document.getElementById("div1").onclick=function(){}
		同一个事件类型只能绑定一个响应函数，无法传递参数，无法设定事件流
		domObj.onXXX=null  可以解除绑定
###DOM2级别绑定事件流
- 使用事件绑定函数

								※这里的事件需要将正常的事件去掉on   ：  onclick-----click
		domObj.addEventlistener("事件"，function(){},true/false);第三个参数代表是否捕获，true代表捕获，false代表不捕获
		解除绑定：domObj.romoveEventLinterner("事件"，function)
		同一个事件类型可以绑定多个响应函数，按照绑定顺序执行

		domObj.addEventlistener("click",function(event){
			响应函数在调用时，JS会传给它一个event事件，event.stopPropagation();可以阻止事件传播
		});
#Event事件
- 事件触发后将会产生一个event对象，event对象记录事件发生时鼠标的位置，键盘按键的状态和触发对象等信息
		
		event.stopPropagation();阻止事件进一步传播
		event.preventDefault();阻止默认方式，表单提交可以阻止默认提交数据
		event.srcElement;触发该事件的对象，后面可以点出该对象的属性，如id、name
		event.button；鼠标按下的键（1左键、2中键、4右键）
#this
	方法里的this，谁调用就是指谁
	事件方法里的this，谁触发就是谁
	a标签添加click事件，如果不传参数，在方法里的this是window对象，因为href其实是window的属性；如果想在方法里获取被点击的a标签，a标签调用方法的地方传this过去
#事件流的流动方式
	
1. 冒泡方式：事件相应函数从最具体的函数开始执行，执行后向上层父节点传播，直到根节点
2. 捕获流：事件响应函数从最上层元素开始执行，执行后向下层子节点传播，直到最精确的触发元素
3. DOM2中的事件流标准：先按照捕获方式进行传播，再按照冒泡流进行传播，但在事件绑定时要说明响应函数的事件流方式
#节点的创建，添加，替换和删除
1. 创建节点(只是创建，没有添加到页面中)
		
		var image= document.createElement("img");
		image.setAttribute("src","img.1.png");
1. 将一个节点插到一个父元素的最后位置
	
		document.getElementById("div1").appendChild(image);
		把image标签插到div1的子元素中的最后位置
1. 将一个节点插入到某个节点前面

		parentObj.insertBefore(newObj,某个节点)；
		var old=document.getElementsByTagName("img")[0];
		document.body.insertBefore(image,old);
		把image节点插入到old节点前面
1. 克隆节点

		obj.cloneNode(boolean);
		克隆obj节点，boolean是指是否克隆子节点，true克隆子节点，false不克隆子节点
1. table对象

		tableObj.rows.length;获取table的行数
		tableObj.insertRow(n);在table的第n行插入一行
		trObj.insertCell(n);在tr的n位置插入一个td
1. 删除节点
		
		parentObj.removeChild(obj);
		var m=document.getElementsByTagName("div")[0];	
		document.body.removeChild(m);从body中删除m节点


1. 替换节点
		
		parentObj.replaceChild(newObj,oldObj);
		var n=document.createElement("div");
		n.innerHTML="kkkkkkk";
		var old=document.getElementsByTagName("p")[0];
		document.body.replaceChild(n,old);
		把body中的old标签替换为n标签

#JS面向对象
##给类添加属性
	function Car() {
        this.name = "BENZ";
        this.color = "red";
    }定义了一个类，含有name和color两个属性
	1.通过类的对象给类添加属性,这种添加属性，只有这个变量有这个属性，其它的变量没有
	var a=new Car();
	var b=new Car();
	a.leg=3;
	2.通过原型添加属性，这样每个变量都会有这个属性
	Car.prototype.leg=3;
##try catch
	document.forms["fff1"].onsubmit = function () {
        var age=document.querySelector("#age").value;
        try {
            checkage(age);
        }catch (e) {
            alert(e);
            return false;
        }
    };
    function checkage(age) {
        if (!age){
            throw "age不能为空";
        } else if (age>100){
            throw "年龄太大啦";
        } else if (age < 10) {
            throw "年龄太小了";
        }
    }
	catch会捕获try代码块里抛出的异常
###Number类型的toString方法

	var a = 10.0;
    var b = 10;
    var c = 1.234e7;
    console.log(a.toString() + "-" + b.toString() + "-" + c.toString());
	结果：10-10-12340000
1.默认模式：在默认模式中，无论最初采用什么表示法声明数字，Number 类型的 toString() 方法返回的都是数字的十进制表示。因此，以八进制或十六进制字面量形式声明的数字输出的都是十进制形式的。先把数字转为10进制，在转换为字符串
2.采用 Number 类型的 toString() 方法的基模式
	
	var a = 10;
    console.log(a.toString(2));
    console.log(a.toString(8));
    console.log(a.toString(16));
	结果："1010"  "12"   "A"     
#对象
	
	object.hasOwnProperty("属性");判断某个对象是否含有某个对象;返回true或者false



		
	