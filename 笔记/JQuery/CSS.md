#1CSS
##css()访问匹配元素的样式属性。
	单参数取值，双参数赋值
	$("p").css({ "color": "#ff0011", "background": "blue" });
	$("p").css("color","ff0011").css("background","blue")
	两种方式都可以
##offset()  获取匹配元素在【当前视口】的相对偏移	
	var offset = $("p").offset();
	offset.left  获取左偏移
	offset.top   获取上偏移
##pisotion()  获取匹配元素相对【父元素】的偏移。
	var offset = $("p").offset();
	offset.left  获取左偏移
	offset.top   获取上偏移


 