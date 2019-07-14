#html5
狭义：html4升级的新标签，新特性。
广义：随着终端的发展，为了适应终端产生的技术。  
	1手机直接访问网站，根据不同的大小显示不同的样式。响应式。：bootstrap响应式框架mui也是
	2.hybird：混合应用。通过html/css/js +打包技术cordovar直接打包成不同的终端应用（android/ios/黑莓/winphone）
#新增结构标签：(块状元素) 有意义的div
	<header>标记定义一个页面或一个区域的头部
	<main>主体
	<nav>标记定义导航链接
	<section>标记定义一个区域
	<aside>标记定义页面内容部分的侧边栏
	<article>标记定义一篇文章(一个分支，会存在并列)
	<footer>标记定义一个页面或一个区域的底部
	<hgroup>标记定义文件中一个区块的信息
	<figure>标记定义一组媒体内容以及它们的标题
	<figcaption>标记定义figure元素的标题
	<dialog>标记定义一个对话框（会话框）类似微信
	**注意**新的结构标签带来的是网页布局的改变及提升对搜索引擎的友好
#html5布局方式
![](https://i.imgur.com/BrHtui0.png)

###input 标签的form属性指向某个form的id。即使input标签不在form表单内，也可以参与该id的form表单的提交


###在form标签里加 novalidate="novalidate" ，取消H5标签自带的验证

### input的pattern属性，给这个输入框设置正则表达式,直接写正则表达式，不用/ /
#新增的表单属性
1. Required  必填
2. placeholder    提示文本
3. Autofocus  自动获取焦点
4. Pattern   正则表达式属性

###input 标签的autofocus属性，页面加载完，自动获取焦点

##Fieldset标记
	<fieldset style="color:red">
		<legend>健康信息</legend>
		身高
		<input type="text" name="" id="" value="" />
		体重
		<input type="text" name="" id="" value="" />
	</filedset>
![](https://i.imgur.com/4ZFRN5P.png)

##base标签。放在head里
	修改相对路径的相对位置
	<base href="http://localhost:63342/webStormWorkSpace/">
	<img src="img/1.jpg">
	相当于把两个地址拼在一起

#JS
-基础编程：js基础语法，常用对象Date、Math、Number。。。  
-DOM编程：document中获取对象：标签对应的js对象（HTMLDocument Object/Collection）
-BOM编程：浏览器对象。window
	window.screen
	window.alert/confirm
	window.history
	window.location
	window.navigator
###disabled 不参与表单提交
###readonly只读
disabled与readonly的区别：disabled不参与表单的提交



###`<input type="image" src="../img/2.jpg" />` 点击的时候会提交表单


#
			视口						初始缩放比例		是否允许用户缩放

`<meta name="viewport" content="initial-scale=1.0,user-scalalbe=no">`

###客户端存储
1.cookie:基于http://www.dnjsak.com:8080（网页关了就不存在了）  
2.localStorage:没有时间限制的数据存储  
3.sessionStorage:当前网页的数据存储(只存在当前页中，其它页无法访问)  

	window.localStorage.ename="tom";声明一个localStorage的对象ename,值是“tom”
	window.localStorage.ename;  获取localStorage的对象ename的值

#drop/drag
ondragstart:当元素开始拖拽时
ondragover:在何处被拖拽时触发
ondrag:拖拽事件
ondrop:拖放事件


preventDefault();终止事件默认的处理方式
dataTransfer.setData/getData.存放事件数据


#abbr 缩写。
如果有title属性，就是鼠标悬停显示的文字，默认样式text-decoration:underline dotted；行级元素
#address标签
地址，标注作者信息及地址信息，默认斜体：text-style:italic;块级元素

#area图片部分定位可以链接到别处
	<img src="../img/timg.jpg"  usemap="#map1" width="200" />
	<map id="map1" name="map1">
    	<area shape="rect" coords="0,0,100,100" href="http://www.baidu.com" title="hhh" />
	</map>
#article 文章，条目。。。一般用在section里   display:block
#bdo  dir:ltr/rtl  设置文本显示方向

#blockquote:长引用；引用一段话，或者来自网络的文字
#q :短引用

#`&copy;`&copy; `&quot`;&quot;

	<table border="1" style="border-collapse: collapse;width: 200px">
        <caption>这是表格的标题</caption>  //表格的标题
        <colgroup>						//定义列宽
            <col width="50px" />	
            <col width="auto" />
        </colgroup>
        <thead>								//表头
            <tr>
                <th>1</th>
                <th>2</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>123</td>
                <td>dasds</td>
            </tr>
            <tr>
                <td>123</td>
                <td>dasds</td>
            </tr>
        </tbody>



#`<city></city>`<city></city> :引入外部文献，比如书籍，杂志；斜体；行级元素
#`<dfn>`定义一个项目`</dfn>`；斜体
#`<code>`定义一段代码块`</code>`
#`<samp>`定义样本文本`</samp>`
#`<var>`定义变量`</var>`；斜体
#`<kbd>`定义键盘输入的文字`</kbd>`

#`<del>`删除线`</del>`
#`<ins>`下划线`</ins>`


#`<figure>``</figure>`;修饰多媒体样式，加个标题
	<figure>
        <figcaption>吃吃吃吃</figcaption>
        <img src="../img/2.jpg" width="100px" />
    </figure>
#`<hgroup>`修饰H1到H6的标题组`<hgroup>`

#img的algin属性，可以设置图片周围文字环绕

#`<mark>`标记：背景色变黄色`</mark>`

#button放在form中，相当于input submit

#`details`折叠内容`</details>`  `<sumary>`details标题`<sumary>`

#客户端存储
1.SQL：结构化查询语句。通用关系型数据库：Oracle/MSSQL-Server2000、2007/mysql/prossgrss/ibm DB2  
2.NOSQL:不仅仅是SQL，非关系型数据库。MongDB/hive/redis/indexedDB  
3.
##indexedDB
NOSQL
型数据库，存储是key/value结构。

1.打开数据库，获取request对象。

	var request=window.indexedDb.open("数据库实例名",版本号);
2.可以定义request相关的回调函数。

	onerror=function(event){} //发生错误时调用
	onsuccess=function(event){}   //成功的时候调用
	onupgradeneeded(event){}     //版本发生变更或者创建数据库时调用
	参数event.target.result  返回 数据库实例
	var db=event.target.result;
3. 通过db对象获取事务对象。


		var tran=db.transcation([objectstory名...],事务方式)；
		只读事务：查询
		读写事务：修改
4. 获取ObjectStroe(相当于数据库的表)


		var objectStore=tran.objectStore(objectstore名);
1. 调用objectStore响应方法：
	
		add(数据):添加数据

#JSON.stringify()能将对象变成字符串形式；JSON.parse();将字符串还原成对象

#事务的四大特性
1. 原子性（atomicity）
1. 一致性（Consistency）
2. 隔离性（Isolation）
3. 持久性（Durability）