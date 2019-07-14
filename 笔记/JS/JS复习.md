#复习
	form标签的action是表单提交的请求。
	menthod属性：get默认值，url能够看到  请求?参数1=参数值1&参数2=参数值2。。。
	post请求：以数据流形式提交请求。没有参数列表
	<textarea></textarea>开始和结束标签之间不要有空格或回车
	重置按钮不是清空，是恢复到默认值
	NAN == NAN NAN===NAN   都是false
#javascript/ECMAScript	
	1.基于对象：封装、继承、没有多态
	面向对象三大特点：封装、继承、多态
	2.事件驱动:onclick=函数();
	3.弱类型：定义时没有类型。赋值之后有类型。

instanceof  判断一个变量是否是对象  
	d1 instanceof Date  判断d1是否是Date类型，返回true或false
	typeof（d1）获取d1的类型，返回值是小写的类型  number
#运算符优先级
> 1元运算符  + - （正负号） ++   --  ！
> 2元运算符  
> 算术运算符+ - * / %  
> 比较运算符  ==   ===  != !==  <  >   
> 逻辑运算符  &&    ||   ！
> 三元运算符：  ？  ：
> 赋值运算   =  +=  -=


#方法
	function abc(a,b,c) {
        console.log(arguments);
    }
	arguments可以获取传过来的参数

空格的keyCode是32   回车的是13

#XML：存储数据，网络传输用的一种数据格式
头信息<? 版本号    字符编码>
> 1.只有一个根（root）节点
> 2.标签必须合理嵌套
> 3.区分大小写
> 4.属性值必须有引号
 
标签：标记：元素：节点：<abc></abc>
属性：attribute、property   <abc a="1" b="tome" / >
内容： 

onload=a();也可以写在body里


#赋值问题：
- js中，除了5中基本类型的赋值时值引用，其它的都是地址引用
- 基本类型外的作为调用函数的参数，也是地址引用

##代码执行顺序
**注意：从上向下，要注意js代码的位置，可能加载js的时候html代码还未加载，会导致Js无法获取html对象**

##获取当前元素的父节点
	当前节点.parentNode;即可找到该节点的父节点，不会弄错
##对于table对象
- tableObj.rows.length可以回去table有多少行
###document.write()
向文档写入HTML表达式或者JS代码  
	`document.write("<input type="text" />");`
###null==undefined   返回true；null===undefined   返回false

###科学计数法
	
	5.167e7表示 5.167乘10的7次方
#Canvas与SVG的区别

	1、Canvas可以看作是一个画布，其绘制出来的是标量图，因此可以在Canvas中引入jpg，png等格式的图片；SVG绘制的矢量图，所以SVG不能引入普通的图片
	2、Canvas绘制的图片不能被引擎抓取，而SVG可以被抓取
	3、Canvas绘制图形是通过js实现的，而SVG更多是通过标签