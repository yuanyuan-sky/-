	#div1{
            height: 100px;
            width: 100px;
            background-color: pink;
            border-style: solid;
            border-width: 100px 100px 100px 100px;
            border-color: red forestgreen blue cyan;
        }
##代码渲染效果
![](https://i.imgur.com/tfrtRh2.png)
##将div的 height设为0px

![](https://i.imgur.com/Q9t8nqq.png)

##将div的width设为0px  
![](https://i.imgur.com/Nq4NLhk.png)
##将div的宽高都设为0
![](https://i.imgur.com/RYyORRl.png)
##4个三角形取一个
	#div1{
		width:0;
		height:0
		border-left:100px solid cyan;
		border-top:100px solid transparent;
		border-bottom:100px solid transparent;
	}
![](https://i.imgur.com/ofEqkQo.png)
##下的三角形取一半
	#div5 {
            width: 0;
            height: 0;
            border-left: 100px solid transparent;
            border-bottom: 100px solid blue;
        }
![](https://i.imgur.com/c25ryOm.png)