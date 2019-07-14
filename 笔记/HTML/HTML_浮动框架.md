#浮动框架frameset:要去掉body

    `<frameset cols="30%,*" border="0">
		<frame src="" name="" scrolling="no" noresize="noresize" />
	</frameset>`
	cols:要分成的列，*代表余下的
	frame 中设置noresize 布局不可改变，不能进行拖拉
	frame中设置scrolling 是否使用滚动条
	border:设置边框线
#iframe
		<iframe  src="index.html" width="100%" height="200px" frameborder="0" marginheight="10px" marginwidth="10px" scrolling="yes">哈哈哈哈</iframe>
	frameborder：(0|1)设置是否显示边框；0不显示，1显示;
	marginheight:框架的上下边距；marginwidth:框架的左右边距
	scrolling:是否显示滚动条；yes|no;上下的滚动条
	**注意：**两个iframe要左右排列要用浮动
	
#嵌套框架
	<frameset rows="200px,*">
		<frame src="1.html" >
		<frameset cols="200px,*">
			<frame src="2.html" >
			<frame src="3.html" >
		</frameset>
	</frameset>

![](https://i.imgur.com/SwmH4Vr.png)