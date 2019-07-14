
#标签
##路径
	./当前目录
	../上一级目录
	../../上两层
	相对路径：相对于html页面的路径
	绝对路径：真实路径（在带有服务器的项目中，不能直接访问绝对路径）
	/开头代表网站跟目录

#注释 
	<!-- 注释 -->
	
##`&nbsp;`空格
##font  字体标签
	<font color="red" face="楷体"></font>
	color字体颜色   face字体
## `<hr />`分割线
	<hr size="10px" width="100px" noshade align="center">
	size是线的厚度，width是宽度 ，noshade使hr的颜色为纯色，align是hr在父元素中的显示方式
## i 倾斜
	<i>倾斜</i>   倾斜
## b 加粗
	<b>加粗</b>   加粗
## u 下划线
	<u>下划线</u>  字体带下划线
##strong 加粗强调，加重语气
	<strong>加粗强调</strong>
	strong与b的区别：b只是字体的加粗，而strong是加重语气的强调
##em  斜体强调
	<em>斜体</em>
	em与i的区别：i只是单独的字体倾斜，而em表示强调
**注意：**在使用加粗和倾斜的时候，优先使用Strong和em
## a 超链接
	<a href="...." target="_black|_self|parent|_top|framName">超链接</a>
	_black在新窗口打开被连接的文档
	_self 默认。在当前窗口打开被链接的文件
	_parent 在父框架中打开被链接的文档
	_top 在整个窗口中打开被链接的文件
	frameName  在指定的框架中打开被链接的文档
**注意：**如果在target中是不存在的页面，则浏览器会在第一次点击超链接时打开一个新窗口，如果新窗口不关闭，再点击超链接，还会在之前的新窗口中打开，重新加载
##锚点
	<a name="top"></a>  设置一个锚点
	<a href="#top"></a>点击该链接就会返回到锚点的位置
##无序列表 ul
	<ul type="square|circle|disc">
		<li>one</li>
		<li>two</li>
		<li>three</li>
	</ul>
	square  实心正方形  circle空心圆  disc实心圆
##有序列表 ol
	<ol type="1|a|A" start="2">
		<li>one</li>
		<li>two</li>
		<li>three</li>
	</ol>
	type时序号类型 ，数字代表数字序号 a代表小写字母序号   A代表大写字母序号  start时序号开始位置，只能是数字
##列表 dl dt dd  块级元素
	<dl>
		<dt>标题1<dt>
		<dd>描述1</dd>
		<dt>标题2<dt>
		<dd>描述2</dd>
	</dl>
	dl定义一个列表，dt是标题，dd是对标题的描述
##表格table
	<table cellspacing="20px" cellpadding="50px" border="1" rules='none/rows/cols/all'>
		<tr>
			<th>1</th>
			<th>2</th>
		</tr>
		<tr>
			<td colspan="2" rowspan="2" align=""center>3</td>
		</tr>
		<tr></tr>
	</table>
	th加粗并居中  colspan 占几列，rowspan 占几行 border设置边框线的宽度,align设置单元格内容的显示方式：居中。。。
	cellspacing  单元格与单元格之间的距离
	cellpadding   是单元格与单元格内容的距离
	rules:规定内侧边框的哪部分时可见的 none:内测边框不可见，只有外边框 rows 只显示横着的线  cols :只显示竖线
##图片 img
	<img src="" alt="" height="100px" width="100px" title="" />
	一般图片不同时设宽高，只设一个，图片就会等比缩放
	alt是图片丢失时显示的文字，title是鼠标放在图片上的提示
#表单 form
	<form action="" method="get|post">
		
	</form>
	action是表单提交请求的地址，method是提交类型
	get：是默认的提交方式，在url中可以看到数据，请求地址?参数1=参数值1&参数2=参数值2。。。
**注意：**form表单不可以嵌套
##input文本框
	<input type="text" placeholder="请输入用户名" maxlength="10" size="50" value="123" autofocus />
	placeholder:提示
	maxlength:最大输入长度，汉字和所有字符都一样
	size：设置文本框的长度
	autofocus:在页面加载完自动获取焦点，直接可以输入
##隐藏文本框	不占位置
	<input type="hidden" name="n" id="n" value="1000" />
##重置按钮
	<input type="reset" name="" id="" value="重置按钮" />
**注意：**重置按钮不是清空内容，而是恢复到初始状态
##查询文本框
	<input type="search" />
	查询文本框与文本框的区别：查询文本框在输入之后会在文本框的最后显示一个用来清空文本框的小红叉
##列表提示 datalist
	<input type="text" list="searchList" />
	<datalist id="searchList">
		<option value="1">北京</option> 
		<option value="2">上海</option> 
	</datalist>
![](https://i.imgur.com/m7C0WOP.png)
	点击输入框后会给出提示，选取后文本框显示的是value值
##数字文本框
	<input type="number" min="1" max="10" step="2" />
	min：输入的最小值
	max：最大值
	step：每点击一次输入框的加减按钮的进度

##居中
	<center>居中</center>
##预编译
	<pre>
		静夜思
		--李白
		床前明月光，
		疑似地上霜。
		举头望明月，
		低头思故乡。
	</pre>
	保留代码中的原格式
##align:段落格式
	p标签设algin:center;p标签在父元素中居中
	div如果没设宽高，则align:center;使div在父元素中居中，如果设置了宽高，则是div中的元素在div中居中，div在父元素中不居中
	table设algin:center;table在父元素中居中
##小于号(<) `&lt;`  大于号(>) `&gt;`
##行级元素
	span a stong em lable  input  select  textarea img br
##块级元素
	div  form  table  p  pre H dl  ol  ul
##base标签。放在head里
	修改相对路径的相对位置
	<base href="http://localhost:63342/webStormWorkSpace/">
	<img src="img/1.jpg">
	相当于把两个地址拼在一起
	



