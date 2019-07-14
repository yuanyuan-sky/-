#1 id选择器
	$("#id")   例：$("#div1")
#2元素选择器
	$("标签")  例：$("span")   返回一个数组
#3 类选择器
	$(".类名")  例：$(".aaa")  查找所有使用了aaa类的标签   返回数组
#4 *选择器
	匹配所有元素
#5 多选择器
	$("div,p,span")  返回数组
#6 派生选择器
	$("div  span")  div内的所有span标签    数组
#7 1级子选择器
	$("div > span")  div【子代】的所有span标签，只是子代，不含孙子代
#8 相邻选择器
	$("div + span")  所有紧跟在div后面的span标签
#9同辈选择器（本身后面的同辈选择器）
	$("div ~ input") 所有div后面的与div【同级】的input标签
#10 伪类选择器（以：分割）
	
> ##10.1 :first
	<ul>
        <li>1</li>
        <li>2</li>
        <li>3</li>
        <li>4</li>
    </ul>
	$("li:first")获取第一个li    

> ##10.2 :not() 去除所有与给定选择器匹配的元素
	<input type="checkbox">
    <input type="checkbox" checked>
	$("input:not(:checked)");  获取没有选中的input标签
> ##10.3 :even匹配所有索引值为偶数的元素，从 0 开始计数
> ##10.4 :odd 匹配所有索引值为奇数的元素，从 0 开始计数
> ##10.5 :eq(index)匹配一个给定索引值的元素
> ##10.6 :gt(index)匹配所有大于给定索引值的元素
> ##10.7 :lt(index)匹配所有小于给定索引值的元素
> ##10.8 :last  获取最后一个
	<table border="1">
        <tr>
            <td>0</td>
            <td>1</td>
        </tr>
        <tr>
            <td>2</td>
            <td>3</td>
        </tr>
        <tr>
            <td>4</td>
            <td>5</td>
        </tr>
        <tr>
            <td>6</td>
            <td>7</td>
        </tr>
    </table>
	$("td:even")选中索引为偶数的td，也就是例中内容为偶数的td
	$("td:odd")选中索引为奇数的td，也就是例中内容为奇数的td
	$("td:eq(3)")选中索引为3的td，也就是例中内容为3的td
	$("td:gt(3)")选中所有索引大于3的td，也就是例中的4567td
	$("td:lt(3)")选中所有索引小于3的td，就就是例中的012
	$("td:last")获取最后一个td，也就是例中的7
> ##10.9 :contains(text) 匹配包含给定文本的元素（子类包含text也可以）
	<div><p><span>123</span></p></div>
    <div>abc</div>
    <div>cdr</div>
	$("div:contains('123')")  获得第一个div
> ##10.10 :empty   匹配所有【不含】【子元素】或者【文本】的空元素
	<div><p><span></span></p></div>
    <div>abc</div>
    <div>cdr</div>
    <div></div>
	$("div:empty")   后去最后一个div
>##10.11 :has(选择器) 匹配【子元素】中含有选择器所匹配的元素的元素（不能是文本）
	<div>abc</div>  $("div:has('abc')")   无法获取
	<div><p class="aaa"><span>123</span></p></div> $("div:has(.aaa)") 可以获取div
	<div><p></p></div>  $("div:has(p)")  可以获取div
>##10.12 :parent 匹配所有含有【子元素】或者【文本】的元素
	<div><span></span></div>
    <div>1232</div>
    <div></div>
	$("div:parent")  获取前两个div
> ##10.13 :hidden 匹配所有不可见或者type为hidden的元素 :visible 匹配所有可见的元素
	<table>
        <tr style="display: none">1</tr>
        <tr>2</tr>
        <tr>3</tr>
    </table>
#11属性选择器
> ##11.1 [attribute]  匹配包含给定属性的元素
	<div>
        <p>hello</p>
    </div>
    <div id="test"></div>
	$("div[id]") 匹配【所有】含有id属性的div
> ##11.2  [attribute = value] 匹配给定的属性是某个特定值的元素；[attribute != value] 匹配所有属性不等value的元素	
	<input type="text" name="test1">
	<input type="text" name="test2">
	<input type="text" name="test3">
	$("input[name ='test1']") 匹配name等于test1的input标签
	$("input[name ！='test1']")匹配所有name不等于test1的input标签
**注意：当一个元素有多个class，当用属性选择器的class的时候，用其中一个class是无法获得这个元素的，必须把所有的class都写上**
	
	<div class="aaa bbb">
	
	</div>'
	$("[class='aaa']")是无法获取这个div的
	$("[class='aaa bbb']");可以获取
> ##11.3 [attribute ^=value] [arrtibute $=value] [attribute *= value]分别是属性以value开头；以value结束；含有value
	<input type="text" name="newsletter">
	<input type="text" name="milkemannews">
	<input type="text" name="aaanewsboy">
	$("input[name ^= 'news']")匹配name以news字符串开头的input标签
	$("input[name $= 'news']")匹配name以news字符串结束的input标签
	$("input[name *= 'news'])匹配name中含有news字符串的标签
> ##11.4 [attribute][attribute]...复合属性选择器
	<input type="text" name="newsletter" id="t1">
	<input type="text" name="newsletter" id="t2" >
	$("input[name='newsletter'][id='t1']")匹配name=newsletter且id=t1的input标签
#12 子元素选择器
> ##12.1  :first-child 每一个父元素中，作为第一个子元素的标签
	<ul>
       <li>1</li>
       <li>2</li>
       <li>3</li>
       <li>4</li>
	</ul>
	<ul>
       <li>5</li>
       <li>6</li>
       <li>7</li>
       <li>8</li>
	</ul>
	$("li:first-child") 匹配每个ul中的li元素  获得1和5
	$("li:first")只匹配第一个li  获得1

> ##12.3 :last-child 每一个父元素中，作为最后一个子元素的标签
	<ul>
       <li>1</li>
       <li>2</li>
       <li>3</li>
       <li>4</li>
	</ul>
	<ul>
       <li>5</li>
       <li>6</li>
       <li>7</li>
       <li>8</li>
	</ul>
	$("li:last-child")  匹配每个ul中的最后一个子元素li 获得4和8
	$("li:last")  只匹配最后一个li 获得8

> ##12.4 :nth-of-type(n|even|odd)

	<div>
	    <span>John</span>   1
	    <b>Kim</b>
	    <span>Adam</span>   2
	    <b>Rafael</b>
	    <span>Oleg</span>   3
	</div>
	<div>
	    <b>Dave</b>
	    <span>Ann</span>    1
	</div>
	<div>
	    <i>
	        <span>Maurice</span>  1
	        <span>12321</span>    2
	    </i>
	    <div>dasd</div>
	    <div>sasx</div>
	    <span>Richard</span>     1
	    <span>Ralph</span>       2
	    <span>Jason</span>       3
	</div>
	【下标从1开始】
	$("span:nth-of-type(2)") 获取【同一个父元素】里的第二个span标签（只数span）
	$("span:nth-of-typy(odd|even)") 获取同一个父元素里下标为奇数或偶数的span标签
#13 表单


> ##13.1  ：input 匹配所有 input, textarea, select 和 button 元素
	<form>
	    <input type="button" value="Input Button"/>
	    <input type="checkbox" />
	    <input type="file" />
	    <input type="hidden" />
	    <input type="image" />
	    <input type="password" />
	    <input type="radio" />
	    <input type="reset" />
	    <input type="submit" />
	    <input type="text" />
	    <select
			<option>Option</option>
		</select>
	    <textarea></textarea>
	    <button>Button</button>
	</form>
	<input type="submit" />
	$(":input") 获取上面除了form的所有标签，
> ##13.2 :text  匹配所有的单行文本框  :radio 匹配所有单选按钮  :password  匹配所有的密码框 :checkbox 匹配所有的复选框  :submit 匹配所有的提交按钮 :image 匹配所有的type为image的标签  :reset 匹配所有的重置按钮 ：button匹配所有的按钮（包括type=button）:file匹配所有文件域  
	<form>
	    <input type="text" />                  1
	    <input type="password" />              2
	    <input type="checkbox" />              3
	    <input type="radio" />                 4
	    <input type="image" />                 5
	    <input type="file" />                  6
	    <input type="submit" />                7
	    <input type="reset" />                 8
		<button type="reset"></button> 			13
	    <input type="button" />                9
	    <select><option/></select>             10
	    <textarea></textarea>				   11
	    <button></button>                      11
		<button type="submit"></button>        12
	</form>
	$(":text")  获取1
	$(":radio") 获取4
	$(":password")获取2
	$(":checkbox")获取3
	$(":submit")获取7、12
	$(":image")获取 5
	$(":reset")获取 8、13
	$(":button")获取 11、9
	$(":file")获取6
#14 表单对象属性
> ##14.1 :enable 匹配所有可用元素
	<form>
		<input name="email" disabled="disabled" />
		<input name="id" />
	</form>
	$("input:enabled")获取第二个input
> ##14.2 :disabled  匹配所有不可用元素
	<form>
		<input name="email" disabled="disabled" />
		<input name="id" />
	</form>
	$("input:disabled") 获取第一个元素
> ##14.3 :checked 匹配所有被选中的元素（复选框、单选框等，不包含select中的option）
	<form>
		<input type="checkbox" name="newsletter" checked="checked" value="Daily" />
		<input type="checkbox" name="newsletter" value="Weekly" />
		<input type="checkbox" name="newsletter" checked="checked" value="Monthly" />
	</form>
	$("input:checked")获取1、3input
> ##14.4 ：selected 匹配所有选中的option元素
	<select>
		<option value="1">Flowers</option>
		<option value="2" selected="selected">Gardens</option>
		<option value="3">Trees</option>
	</select>
	$("option:selected") 获取2
	

	


	
