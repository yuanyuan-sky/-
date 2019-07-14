##css:层叠样式表
样式定义如何显示HTML元素  
多个样式定义可以层叠为一
#万维网联盟（w3c）
#字体的默认大小:16px=1em
##注释
	/*  注释*/
##css的4中引入方法
	1.内联样式：也叫内嵌式或行内式，直接在标签上写样式
	2.内部样式表：在网页上使用style标签包裹样式代码
	3.外部样式表：使用<link href="。。.css" rel="stylesheet" type="text/css" />
	4.导入式：<style>@import url("。。.css")</style>
	**优先级**内联式>嵌入式>外联式
	import和link的区别：页面加载时，link会同时被加载；inport引入的 css会等页面被加载完再加载
#多重样式表
	外表样式表
	h3{
		color:red;
		text-align;center;
		font-size:15px;
	}
	内部样式表
	h3{
		text-align:right;
		font-size:30px
	}
	如果一个页面同时用了这两个样式，那么h3拥有的样式是
	color:red;
	text-align:right;
	font-size:30px;
	**注意：**这两个样式同在一种样式表中也是同样的效果
##css基本语法
	1.忽略大小写（但在定义选择器的时候区分大小写）
	2.多重声明：使用多个属性以及取值同时渲染一组标签
#选择器
**注意：属性值与单位之间不要有空格**
##标签选择器
	标签{
		属性：属性值
	}
##id选择器
	`#`id{
	}
	区分大小写
	id的命名规范：数字、字母、下划线；数字不能开头
##多元素选择器
	选择器,选择器,...{
	
	}
##类选择器
	.类名{
	
	}
	也可以指定特定的HTML元素使用class
	p.aaa{
		color:red;
	}
	只有p标签使用了这个class字才会变成红色，其它标签使用没有效果
	<p class="aaa">哈哈哈</p>  红色
	<div class="aaa">div</div>	无效果
##属性选择器
	a[href]{

	}带有href的a标签
	a[href][title]{
	
	}带有href和title属性的a标签
	a[href='www.baidu.com']{
	
	}href属性等于www.baidu.com的a标签
	
##子元素选择器
	父选择器 > 子选择器{
	
	}获取父元素的所有一级子元素
##相邻元素选择器
	选择器1 + 选择器2{

	}选择器1【下方】的与选择器1相邻的选择器2
##后续兄弟选择器
	选择器1 ~ 选择器2{
	
	}选择器1后面的兄弟中的全部选择器2
##后代元素器
	父选择器 后代选择器{
	
	}获取父元素中所有指定的后代（全部子孙后代）

##选择器的优先级
	id选择器 > 类选择器 > 标签选择器
##伪类样式
	a:link{
		未被访问的链接
	}
	a:visited{
		已被访问的链接
	}
	a:active{
		正在点击的链接
	}
	a:hover{
		鼠标滑过的时候
	}
**注意：当设置多个状态时，hover必须跟在link和visited后面；active必须跟在hover后面**  
：first-child;选择父元素的第一个子元素
	  
	p:first-child{
		
	} 作为任何元素的第一个子元素的p标签（这个p必须时第一个子元素）
	p > i:first-child
	{
	    color:blue;
	}
	匹配作为p的第一个子元素的i标签
:checked 选择所有选中的表单元素  
:disabled 选择所有禁用的表单元素  
:empty 选择所有没有子标签的元素  
:enabled 选择所有启用的表单  
:required 选择有required属性的元素  
:focus 选择获得焦点的元素  
:first-letter 指定元素的第一个字母的样式  
	
	p:first-letter{} 每个p元素的第一个字母的样式  
:first-line  指定选择器的第一行的样式	

	p:first-line{}每个p的第一行的样式
:before 向指定的元素前插入内容
	
	p:before{
		content:"Read this:"	
		background-color:yellow;
		color:red;
		font-weight:bold;
	}
	<p>123</p>
	变为Read this:123,且只有Read this:有上面的样式

:after 向指定元素后面插入内容，同上，只是加在后面  
###用after给div加小箭头

	div {
        width: 100px;
        height: 100px;
        background-color: #5dd94e;
        top: 100px;
        left: 100px;
    }
    div:after {
        content: "";
        position: absolute;
        border-width: 5px;
        border-style: solid;
        border-color: red blue green yellow;
        top: 50px;
        left: 108px;
    }
	**注意after一定要用绝对定位（absolute/fixed），不然会有问题，问题如下**
![](https://i.imgur.com/rVNAem2.png)
![](https://i.imgur.com/77N214k.png)

##css样式
text-decoration:none/underline/overline/line-through无下划线/有下划线/下划线在上面/下划线在中间  
list-style:列表样式，是否有圆点  
color：字体颜色  
font-size：字体大小  
font-family：字体  
		
	如果字体系列的名称超过一个字，它必须用引号，如Font Family："宋体"。
	p{font-family:"Times New Roman", Times, serif;}
font-weight：字体加粗  
font：粗细 大小 字体  	
background-color:背景颜色  
background-image:url()背景图片  
background-repeat:repeat-x/repeat-y/no-repeat x轴平铺/y轴平铺/不平铺   
background：[ background-color ] || [ background-image ] || [ background-repeat ] || [ background-attachment ] || [ background-position ]  
background-attachment:fixed/srocll 背景图片是否随内容滚动，fixed不滚动，scroll滚动  
background-position:背景图片位置【用处：美工给的图集，设一个div，选取一个图标作背景图，通过background-position控制显示哪个图标】  
white-space：normal/pre/nowrap/pre-wrap/pre-line 默认。空白会被浏览器忽略/空白会被保留，类似`<pre>`标签/文本不会换行/保留空白符序列，但是进行正常的换行/合并空白符序列，但是保留换行符  
overflow:容器的内容超出宽度时怎么处理。visible显示hidden超出的内容不显示scroll出现滚动条  
letter-spacing:每个字符之间的距离，汉字也有效果  
word-space:每个单词之间的距离，对汉字没效果  
text-indent:文字缩进  
line-height:行高  
vertical-align:垂直方向对齐方式top/middle/bottom；使用vertical-align的条件：1.该元素必须是内联元素或者是table-cell元素。2.内联元素或table-cell元素的基线相对于该元素所在行的基线的垂直对齐。  
border-collapse：collapse;table使用此样式可以使相邻单元格的线变为一条  
text-align:center/right/left/justify;居中，右对齐，左对齐，两端对齐  
#文本转换属性
	text-transform:uppercase;全大写
	text-transform:lowercase;全小写
	text-transform:capitalize;首字母大写
#字体的样式
	font-style:normal/italic;正常/倾斜
	font-variant:normal/small-caps;正常/把段落设置为小型的大写字母字体：
##文字阴影
	text-shadow:水平阴影的位置(必须) 垂直阴影的位置(必须)  blur 模糊的距离(可选)  阴影的颜色(可选)
	如果后两个参数省略，则阴影就是原文字
![](https://i.imgur.com/zuQfWLo.png)
##div阴影（图片也可以）
	box-shadow:水平位置(必须)  垂直位置(必须) 模糊距离(可选)  阴影扩展的半径(可选)  阴影的颜色(可选)  inset(可选)变为内测阴影
	只有前两个参数则为黑色阴影
##尺寸属性
	min-width:最小宽度
	max-width:最大宽度
##定位属性 position
1.relative:相对定位，对象遵循普通流，当前元素参照正常位置的左上角进行位置偏移，移动相对定位的元素，但其原本所占的空间不会变  
2.absolute:绝对定位，以离其最近的设置了相对定位的父类元素的左上角为参考，如果没有。则以浏览器的左上角为参考。absolute 定位使元素的位置与文档流无关，因此不占据空间。  
3.fixed：以窗口为参考，出现滚动条时，不会滚动  
**注意：**只有设置了position属性才可以使用top，left，right，bottom属性  
4.static:默认值  
5.sticky:粘性定位 ;
	
	粘贴定位依赖于用户滚动条的滚动。指定 top, right, bottom 或 left 四个阈值其中之一，才可使粘性定位生效。否则其行为与相对定位相同。
	iv.sticky {
	    position: -webkit-sticky; /* Safari */
	    position: sticky;
	    top: 20px;
	    background-color: green;
	    border: 2px solid #4CAF50;
	} 
	意思是当的用户滚动滚动条时，当该元素距离浏览器顶部大于20px时，该元素随浏览器滚动，当该元素距离浏览器顶部20px时，该元素不再随滚动条滚动（此时的表现像fixed）
6.inherit:继承父元素的定位，父元素是什么定位，它就是什么定位  
※z-index:当两个元素发生覆盖时使用，值大的显示在上面
##display属性
	none;隐藏，不占空间
	block；此元素变为块级元素，元素前后有换行符
	inline；此元素被显示为内联元素，元素前后没有换行符
	list-item;此元素被作为列表显示
	table；此元素被作为块级表格显示出来，元素前后有换行符
	inline-table;元素被作为内联表格显示，元素前后没有换行符
	table-row|table-cell|table-column  作为表格行，表格单元格，表格列显示
##visibility
	hidden;隐藏，但是占空间
	visible;显示
##浮动布局float
	left;左浮动
	right；右浮动
	clear：both；清除浮动
**浮动会使一个元素变为块级元素，不论他本身是何种元素**
##margin
	四个值：上右下左
	三个值 上（左右） 下
	两个值   （上下）（左右）
##外边距属性的特殊说明：
内联块级元素和块级元素的可以设置外边距。
内联元素可以设置左、右两边的外边距；若要设置上、下两边的外边距，必须先使该元素变为块级元素或内联块级元素。
##内边距属性的特殊说明
	行内元素可以设置左、右两边的内边距；若要设置上、下两边的内边距，必须先使该元素变为块级或内联块级元素。
#去掉input文本框获取焦点时的边框
	outline:none;
#列表

- ul无序列表
- 有序列表

		list-style-type:设置列表项的标记类型，（点，方块，数字。。。）
		list-style-image: url("../img/w.png");设置图片为列表项的标记
		list-style-position:inside/outside
![](https://i.imgur.com/WIeDsM1.png)

#边框（border）
border-style:边框样式  

- dotted/dashed/solid/double/groove/ridge/inset/outset  
点线边框/虚线边框/实线/双边框/3D沟槽边框/3D脊边框/3D的嵌入边框/3D突出边框
**注意：double双线边框的宽度就是border-width的宽度**
#轮廓（outline）outline是不占空间的

#cursor:设定鼠标移动到该元素上的显示方式（小手、问好。。。）
#元素的浮动（float）
	1.浮动元素之后的元素将围绕它。
	2.浮动元素之前的元素将不会受到影响。
	3.如果图像是右浮动，下面的文本流将环绕在它左边：
	

