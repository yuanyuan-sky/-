
#三个div第一个左浮动，第二个右浮动，第三个不浮动时。且第三个div大时
第三个div会在第一个div下面  

	<div id="div1" style="width: 100px;height: 100px; border: 1px solid red;float: left;">

    </div>
    <div id="div2" style="width: 100px;height: 100px; border: 1px solid yellow;float: right;">

    </div>
    <div id="div3" style="width: 150px;height: 150px; border: 1px solid green;">
            
    </div>
![](https://i.imgur.com/Lzd7DdX.png)


----------


当第三个div中的内容比较多时  
![](https://i.imgur.com/ecjN10X.png)  

----------

第三个div跟其它的一样大时  
第三个div被第一个div遮住  
![](https://i.imgur.com/ip34Ukp.png)

----------


第三个div跟其它的一样大，且里面有内容时  
第三个div虽然被第一个完全遮住，但内容被第一个div挤下来了

![](https://i.imgur.com/GAMqvwN.png)

----------

#四个div，第一个右浮动，后面三个不浮动
![](https://i.imgur.com/7Q9zkYe.png)

一个div浮动，会对其后面的div产生影响





----------

#三个div，前两个右浮动，第三个不浮动
![](https://i.imgur.com/9IFtzBR.png)

----------
#三个div都右浮动，再清除掉第二个div的浮动
	<style>
        #div2{
            clear: both;
        }
    </style>

	<div id="div1" style="width: 100px;height: 100px; border: 1px solid red;float: right;">
        div1
    </div>
    <div id="div2" style="width: 100px;height: 100px; border: 1px solid yellow;float: right">
        div2
    </div>
    <div id="div3" style="width: 100px;height: 100px; border: 1px solid green;float: right">
        div3
    </div>
![](https://i.imgur.com/OZdzKLR.png)  
这个存在选择器优先级问题，这个div2其实还是右浮动，只是因为清楚了与div1浮动的联系，所以才到下一行了