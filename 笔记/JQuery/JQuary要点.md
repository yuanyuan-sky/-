#JQuery：javaScript的函数库 2018/8/14 14:51:57 
    
##1
	1.JQuery对象：指的是$()选择后的的对象  
	2.对象对象:document.getElement***
##1.1 window.onload与$(document).ready()的区别
	1. window.onload写多个时，只有最后一个有用，$(document).ready()多个每个都有用
	2. $(document).ready()可以缩写为$(function(){});onload不能缩写
#1.2DOM与JQ的区别
	1. 语法格式不一样   
	   js:DOM.innerHTML=""  jq:$().html("");
	   js:DOM.innerText=""  jq:$().test("");
	
##2
	css()方法：参数可以是对象，也可以是两个字符串。用于设置样式  
	如果是一个参数是什么意思？
	>※ 双参数是 赋值   单参数是取值  
	>※ 设置是所有元素设置。取值只取第一个元素的值
###补充：rgb：三原色：红、绿、蓝  
	每一个颜色取值范围 0~255  0~FF  
	红色：red\rgb(255,0,0)\#FF0000  
	绿色：green\rgb(0,255,0)\#00FF00  
	蓝色：blue\rgb(0,0,255)\#0000FF  
	白色：white\rgb(255,255,255)\#FFFFFF  
	黑色：black\rgb(0,0,0)\#000000

#3转换
	JQuery对象与DOM对象的转换  
	$(this).*****  
	1.DOM --> JQuery  :用$(DOM对象)  
		$("选择器")。。。。
	或者 $(DOM对象)
	2.JQuery --> DOM :用$("选择器").get(0)
		$("选择器").get(0).innerHtml="";
		.get(0)转为DOM对象
		.get() 转为数组
#4操作文本
	> text() 设置或者返回所选元素的文本内容   
	> html() 设置或返回所选元素的内容（包括html标记）
	> val()  设置或返回【表单】字段的值
	
#5 属性相关
attr:单参数取值，双参数赋值。修改属性
removeAttr（）：删除属性
prop： checked/selected/disabled/readonly四个属性的修改
removeProp  :删除上面四个属性
#6 CSS相关
addClass:添加class属性
removeClass:删除class属性
toggleClass:添加或者删除属性（标签已有指定的class就删除，没有就就把指定的class添加上）

css：添加样式

html():相当于innerHTML;无参取值，有参赋值
text():相当于innerTEXT
val():相当于value

offset(): left\top组成，相对于浏览器窗口
position():left\top  相对于父元素

#7文档处理
parent.append(son):父加子，在最后加入
son.appendTo(parent);子加入父，在最后加入

parent.prepend(son):父加子，在第一个
son.prependTo(parent):子加入父，在第一个

after()： 前.after(后)
before()  后.before(前)
insertAfter(): == before()
insertBefore():  ==after()
##7.1
empty():清楚标签里的内容
	 $("div").empty()
remove（）：删除标签
#8参照
children(""): 获取一级子
find(""):获取所有后代

parent():获取父
parents():获取祖宗

#JQuery事件
on所有事件都可用。jqueyy1.7之后推荐使用  
	 $("选择器").on("事件",function(){
		
	});
off: 取消事件：
	$("p").off();取消所有事件
	$("p").off("click")取消点击事件

delegate(selector,[type],[data],fn):适用于当前元素和未来元素：（事件的委托机制）
（不是未来元素的）父.delegate（“选择器”，“click/change”,function(){
}）;

切换：hover:  一般是悬停处理
	hover(function(){   
		悬停事件
	},function(){
		离开事件
	})；
#2JQuery效果
	hide(): display:none
	show(): display:block;inline;inline-block
	toggle(): 显示变不显示，不显示变显示
#3JQuery方法和JQuery对象方法
	JQuery方法指的是$.方法（）
	JQuery对象方法指的是$().方法（）
#4 数组的循环
1.for循环：
for(var item in array3){
						/* 这里的item是索引 */
						document.write(array3[item]);
					}  
2.while  
3 for in  循环：循环的是属性（如果循环的是数组，则循环的是下标，如果循环的是对象，则循环的是属性）
JS的数组循环 forEach   a.forEach(function(item,index){
	})index是下标：循环标量
	
JQuery的each   $.each(a,function(index,item){

	})
JQuery对象的each  $().each(function(index,item)){
						在里面也可以用this代表item
				}
#5 标签存储数据
	通过标签加入data-变量="值"进行数据存储。
	获取数据：$().data("变量")
	设置数据：$().data("变量","值");
	<div data-name="tom" data-age="12"></div>
	console.log($("div").data("name"));
    console.log($("div").data("age"));
#6插件扩展
$.fn.extends();给JQuery对象加入方法
$.extends();给JQuery加入方法

补充：
权重  id:100  class:10    标签1


#小技巧
	a 标签的href属性默认点击会发生跳转。
	可以通过设置href="javascript:void(0)" 取消默认跳转或者href="javascript:语句"

	\转译符号   \"   就是一个"
## lable标签  
	修饰页面上的文字。for属性：指向某个标签的id
	当点击这个文字时，for对应的id标签获取焦点

##get（）与eq()的区别  get()获取到的是DOM对象，eq()获取的是JQuery（）对象
#如何区分JQuery对象和Dom对象
	 <p>1</p>
	 <p>2</p>
	 <p>3</p>
	console.log($("p").eq(1));
    console.log($("p").get(1));
![](https://i.imgur.com/WorCVck.png)  
	JQuery对象在控制台打印是init类型而Dom对象直接是html元素或者是array数组
##获取select标签中被选中的值，用的事件是 change


###对于form表单
	$("form").serializeArray(); 获取form表单所有提交的内容的数组（元素要有name）
	$("form").serialize();获取form表单所有提交的内容的字符串
![](https://i.imgur.com/86unneA.png)

	function abc(opt) {
	        //想当于继承，前面是父，后面是子，子会覆盖父
	        var settings = $.extend({sex: "男", likes: ["lol", "DNF"], ename: "jary"}, opt);
	        console.log(settings);
	    }
	    abc({ename:"tom", age: 13})


$(':focus').css('background', 'red'); //focus 过滤器，必须是网页初始状态的已经被激活焦点的元素才能实现元素获取。而不是鼠标点击或者Tab 键盘敲击激活的
