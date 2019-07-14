#clip 裁剪 通过对元素进行剪切来控制元素的可显示区域
	

- **注意**clip属性只能在元素设置了position:absolute或者position:fixed属性时才能起作用
	
- clip:rect(top,right,bottom,left);

- top和bottom指定的偏移量是从元素盒子顶部边缘算起，left和right指定的偏移量是从元素盒子左边边缘算起的	

- **注意**rect()不支持百分比
- rect()中的bottom值小于top值，或者right值小于left值时，整个剪切区域不会显示
- 当top或者left取值为auto时，相当于取值为0
- 当bottom和right取值为auto时，相当于元素的100%宽度  
![](https://i.imgur.com/YLr5RCD.png)


##补充：
1.-moz代表firefox浏览器私有
2.-ms代表ie浏览器私有
3.-webkit代表safari、chrome私有属性
##技巧

1. 超出的文字变省略号
	overflow-x:hidden;white-space:nowrap;text-overflow:ellipsis;同时使用


1. 	多个半角空格浏览器只认识一个半角空格	,全角空格可以识别多个

##text-overflow:规定当文本溢出时，怎么处理溢出的文本
##overflow:内容超出宽度时应该怎么处理
	overflow-x/overflow-y超出时x，y轴处理
	属性：hidden  超出时隐藏  scroll 超出时显示滚动条
##圆角
	border-top-left-radius:左上角圆度
	border-top-right-radius:右上角圆度
	border-bottom-left-radius:坐下角圆度
	border-bottom-right-radius:右下角圆度
	border-radius:复合写法  左上 右上  右下  左下
**椭圆边角**
![](https://i.imgur.com/BQVh85d.png)

	#div1 {
            width: 100px;
            height: 100px;
            border: 1px solid red;
            border-radius: 50px/30px;
        }
斜杠前面的为第一组值为水平半径，后面的为垂直半径。也分别是四个值

##边框图片：border-image


##background-origin:设置背景图片左上开始的位置
	border-box:从边框开始
	padding-box:从内边距开始
	content-box：从内容开始
##background-clicp:截取背景图片
	border-box:
	padding-box:只保留内边距开始的范围，边框上的图片会被截掉
	content-box：只保留内容范围的图片，其它范围被截掉
##background-size:设置背景图片大小
	1.可以设置宽高，值或者比例
	2.cover：按照容器的宽度进行等比缩放，会导致高度有问题
	3.contain:按照容器的高度进行缩放，会导致宽度有问题
	4.auto：默认值，图片大小不变
##多背景图片
	background-image:url("1.jpg"),url("2.jpg"),url("3.jpg");
	background-repeat: no-repeat, no-repeat, no-repeat;  
	background-position: 0 0, 200px 0, 400px 201px;  
	
##透明度
	opacity:取值范围0~1	默认值是1，不透明
##tab-size:tab制表符
	数字：一个制表符代表多少个空格
	宽度：一个制表符代表多少px
	※必须用在pre里
##word-wrap:break-word   允许文本强制换行
正常情况下，如果单词与单词之间有空格的话，在宽度不够的情况下，文本会自动换行，但是当一个单词特别长的时候，这一个宽度可能就会超出宽度，那么在下一个空格带来之前，不会换行，那么，那个特别长的单词就会超出宽度范围，word-wrap:break-word就是可以强制那个特别长的单词进行断开换行  
![](https://i.imgur.com/ZDWlcKY.png)
![](https://i.imgur.com/uwK1kL0.png)
##overflow-wrap:默认情况下，按单词或句子进行断行
	强制断行：break-word;
##word-break:break-all;强制换行
##text-align:
	start:左对齐
	end：右对齐
	justify:两端对齐
##outline:边框的外边框
	outline:3个参数
	1.outline-width:线宽
	2.outline-style:线样式
	3.outline-color:颜色
	4.outline-offset：外边框的偏移量
##zoom 缩放

##box-sizing:设置盒子大小
	1.默认情况下，内容+边框*2+内边距*2=真实宽度，设的width就是内容的宽度
	box-sizing：border-box;设的width不是内容的宽度，而是内容+内边距+边框的宽度
	2.box-sizing：content-box 设的width就是内容的宽度
	**注意：**没有padding-box


##文字的多列显示
	column-width:指定列宽
	column-count:列数
	column-gap:列与列之间的宽度
	复合写法：column:column-width column-count;
	column-rule:设置每列之间的分割线，和border的属性一样
	column-span:列中的子标签占几列，none默认，all横跨所有列（只能有这两个值）
#引入外部字体
@font-face

	@font-face {
            font-family: myFirstFont;      //给引用的字体起个别名
            src: url("FZSuXSMZTJW.TTF");   //引入的字体路径
        }
        div {
            font-family: myFirstFont;      //应用引入的字体
        }
	如果这种字体还有粗体，引进其


# @media:用于响应式布局。根据不同的终端设备大小，设置不同的样式
	@media  [选择符not/only]  设备类型(screen屏幕，print打印环境,all所有) and   （查询表达式）{
		样式
	}
	查询表达式可以写多个，用and连接  max-width:800px;  min-width:300px
#!important 样式最高优先级
# @import :根据终端大小导入外部样式库
	语法：@impotr url('文件地址') [选择符not/only]  设备类型 [and  (查询表达式)]


#@supports:用于判断浏览器是否支持某个属性
	语法：@support (not (属性：属性值)) and/or( not （属性：属性值）)	

#关系选择器
	>  一级子（不含孙子）
	+ 下面相邻的一个（同辈）
	~ 后面的同辈里的指定元素
#属性选择器
	1.[attribute]  匹配包含给定属性的元素
	2.[attribute = value] 匹配给定的属性是某个特定值的元素；[attribute != value] 匹配所有属性不等value的元素	
	3.[attribute ^=value] [arrtibute $=value] [attribute *= value]分别是属性以value开头；以value结束；含有value
	4.[attribute][attribute]...复合属性选择器
#伪类选择器
	:nth-child(n):第n个子元素
	:nth-of-type;按类型  第n个子元素
#新增单位

1. rem:font-size默认值（一般16px）的倍数


2. vw: 视口宽度。视口宽度均分100份
3. vh:视口高度。视口高度被均分100份

#initial：恢复默认样式
	display:none/display:initial

#calc();可以进行单位的运算，加减乘除 
	width:(16px * 2);
#渐变(Gradients)
##线性渐变(Linear Gradients)：向上/向下/向左/向右/对角方向
为了创建一个线性渐变，你必须至少定义两种颜色结点。颜色结点即你想要呈现平稳过渡的颜色。同时，你也可以设置一个起点和一个方向（或一个角度）。
###语法
background:linear-gradient(direction,color1,color2,...);  

	默认是从上到下
	.div{
		background:-webkit-linear-gradient(blue,red...);
	}
	从左到右
	.div{
		background:-webkit-linear-gradient(left,blue,red...);
	}
	对角
	从左上角到右下角
	.div{
		background:-webkit-linear-gradient(left top,blue,red...);
	}
###使用角度
####语法:background:linear-gradient(angle,color1,color2);
角度是指水平线和渐变线之间的角度，逆时针方向计算。换句话说，0deg 将创建一个从下到上的渐变，90deg 将创建一个从左到右的渐变。
![](https://i.imgur.com/foBa5U7.png)  
**请注意很多浏览器(Chrome,Safari,fiefox等)的使用了旧的标准，即 0deg 将创建一个从左到右的渐变，90deg 将创建一个从下到上的渐变。换算公式 90 - x = y 其中 x 为标准角度，y为非标准角度。**
###使用透明度
	background: -webkit-linear-gradient(left,rgba(255,0,0,0),rgba(255,0,0,1));同一个颜色透明度从0—1
![](https://i.imgur.com/s2VdzFL.png)
###重复的线性渐变
	background: -webkit-repeating-linear-gradient(left,red, yellow 10%, green 20%);
##径向渐变(Radial Gradients)
为了创建一个径向渐变，你也必须至少定义两种颜色结点。颜色结点即你想要呈现平稳过渡的颜色。同时，你也可以指定渐变的中心、形状（圆形或椭圆形）、大小。默认情况下，渐变的中心是 center（表示在中心点），渐变的形状是 ellipse（表示椭圆形），渐变的大小是 farthest-corner（表示到最远的角落）  
###语法
	background:radial-gradient(center,shape size,start-color,...,last-color);
###颜色节点均匀分布的径向渐变
	background: -webkit-radial-gradient(red, green, yellow);
###颜色节点不均匀分布的径向渐变
	background: -webkit-radial-gradient(red 5%, green 15%, blue 60%); 
###设置形状
	background: -webkit-radial-gradient(ellipse,red, green, yellow);椭圆，圆形circle
###不同尺寸大小关键字的使用
1.closest-side  
2.farthest-side  
3.closest-corner  
4.farthest-corner  

	background: -webkit-radial-gradient(center,closest-side,red,yellow,blue);
###重复的径向渐变
	background: -webkit-repeating-radial-gradient(red, yellow 10%, green 15%);
#2D转换
	
1. translate(左，右)；根据左(X轴)和顶部(Y轴)位置给定的参数，从当前元素位置移动。
2. rotate();在一个给定度数顺时针旋转的元素，允许负值，是逆时针旋转。

		transform:rotate(50deg);顺时针旋转50度
3.scale();该元素增大或者减小
	
		transform:scale(2);变为原来的2倍
		transform:scale(2,3);宽度为原来的2倍，高度为原来的3倍
	
4.skew（）

		transform:skew(30deg,20deg);在X轴上旋转30度，在Y轴上旋转20度
**注意：一个标签同时应用多个转换：transform:translate()  rotate()  scale()...**
#3D转换
1.rotateX();定义3D旋转，只使用X旋转顺着X轴旋转指定的度数；rotateY();，只使用Y轴旋转顺着Y轴旋转指定的度数；totateZ();定义3D旋转，只使用Z轴;rotate3d(x,y,z,angle);定义3D旋转，x、y、z取值1或0，1代表沿该轴旋转，0代表不旋转，angle是旋转的角度。
2. scaleX();定义3D缩放，只使用X；scaleY();只使用Y，scaleZ();只使用Z轴；scale3d(x,y,z);定义3D缩放
3. translateX();定义3D转换，仅使用X轴；translateY();只使用Y轴；translateZ();只使用Z轴；translatesd(x,y,z);定义3D转换
2.transform-origin:设置转化的基点
	
	对于2D转换
	#div2:hover{
            transform: rotate(360deg);
            transform-origin: 0 0;
            transition: all 5s ease;
        }
	div2绕着自己本身位置的左上叫进行旋转360度，原位置的左上角为0 0 点
3.transform-style:flat/preserve-3d（给父元素设置）
	
	flat:子元素不保留其3D位置。即如果子元素进行3D装换，旋转了一个角度，当其父元素进行转换时，对子元素无影响，即子元素一致保持那个状态
	preserve-3d:子元素将保留其3D位置，即如果子元素旋转了一定角度，与父元素垂直，当父元素进行旋转时，子元素也会跟着动，且始终保持与父元素垂直的角度
4.backface-visibility: hidden；/visible;不可见/可见
元素的背面在旋转以后是否可见，正常在旋转后是可见的，只不过内容会反过来，而如果背面不可见，则旋转到背面时，就会消失
##过渡
	transition(属性(width/height/all),时间,过渡效果 ,延迟时间)；
	过渡效果：linear，ease，ease-in,ease-out,ease-in-out
	cubic-bezier(n,n,n,n);在 cubic-bezier 函数中定义自己的值。可能的值是 0 至 1 之间的数值。
#动画：  关键帧   动画
	@keyframes 动画名{
		0%{样式}
		50%{样式}
		100{样式}
	}
	元素{
		animation:动画名 几秒内完成  过渡效果（ease,linear） 延迟时间  循环次数（infinite是无限）  动画反向(alternate)
	}
animation-play-state:paused;可以暂停动画

#用户界面
1.resize:none/both/horizontal/vertical  用户无法调整/用户可调整元素的宽度和高度/可调整宽度/可调整高度  
**注意：如果希望此属性生效，需要设置元素的 overflow 属性，值可以是 auto、hidden 或 scroll。**  
2.outline-offset：设置元素轮廓与元素之间的距离