#1属性
##1.1 属性
> ### attr()  设置或返回被选元素的属性值(一个参数是取值，两个参数是赋值)
	$("img").attr("src");  获取img标签的src属性
	$("img").attr("src","aa.jpg");将img标签的src属性修改为aa.jpg
> ### removeAttr(name) 从匹配的元素中删除一个属性
	$("img").removeAttr("src");删除img标签的src属性  结果<img />
> ### prop()  跟attr()一样，但往往用于checked、selected、disabled、readonly四个属性的修改
	$("#s1 option").prop("selected","selected");
	将s1中的option全选
> ### removeProp("")  删除指定的属性
#2CSS类
> ### addClass()  为每个匹配的元素添加指定的类名。
> ### removeClass()  从所有匹配的元素中删除全部或者指定的类。(如果没有参数，则删除指定元素的所有class)
> ### toggleClass("className")  若果指定的元素已经用了该则删除，没有则加上

#3 HTML代码/文本/值
	html()  text()   val()




