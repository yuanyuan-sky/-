#XML
一个基本的XML文档通常由序言和文档元素两部分组成。
###序言
XML文档的序言中可以包括XML声明，处理指令和注释。但这三项不是必须的

	<?xml version="version" encoding="value" standalone="value" ?>
	version:用于指定遵循XML规范的版本号，该属性必须放在XML声明中其它属性之前
	encoding:指定XML文档中字符使用的编码。
	standalone:指定XML文档是否和一个外部文档嵌套使用。取值为yes/no，yes说明是一个独立文档，与外部文件无关联；no说明XML文档不独立。
###文档元素


- XML文档中的元素是以树型分层结构排序的，一个元素可以嵌套在另一个元素中。XML文档中有且只有一个顶层元素称之为根元素。  

- XML文档元素由其实标记、元素内容和结束标记3部分组成。定义XML文档元素的语法格式如下

		<TagName>content</TagName>
		<TagName>：是XML文档元素的其实标记，TagName是元素的名字
		content:元素内容，可以包含其它元素。
		1、元素的名字可以包含字母，数字和其它字符
		2、元素只能以字母、下划线、：开头
		3、元素的名字不能是xml、XML、Xml。。。。
		4、元素的名字不能包含空格。
###XML语法要求
- XML文档必须有一个顶层元素，其它元素必须嵌套在顶层元素中
- 每个元素必须同时拥有起始标记和结束标记
- 起始标记中的元素类型名必须与相应的结束标记中的名称完全匹配
- XML元素类型名区分大小写。
- 元素可以包含属性，但属性必须用单引号或者双引号引起来，而且前后两个引号必须一致。

###XML文档中元素定义属性
- 在一个元素的起始标记中，可以自定义一个或多个属性

###处理字符数据
在XML文档中，有些字符会被XML解析器当作标记进行处理。如果希望把这些字符作为普通字符处理，就需要使用*实体引用*或*CDATA段*。

1. 使用实体引用

		   字符		<		>		&		'		"
		实体引用    &lt;	   &gt;	  &amp;	  &apos;	&quot;
1. 使用CDATA段

		CDATA段是一种用来包含文本的方法，它内部的所有内容都会被XML解析器当作普通文本。语法格式如下

		<![CDATA[文本内容]]>

		<placard version="2.0">
		    <info id="1">
		        <title>在servlet中弹出JavaScript</title>
		        <content>
		            <![CDATA[PrintWriter out = response.getWriter();
		            out.println("<script>alert('修改成功!');</script>");]]>
		        </content>
		        <pubDate>2012-06-15 16:12:06</pubDate>
		    </info>
		</placard>
		注意：CDATA不能进行嵌套，另外字符"]]>"之间不能有空格或换行符
#dom4j
引入两个jar包  
1、dom4j.jar  
2、jaxen.jar

1. 创建XML文档对象

		Document document = DocumentHelper.createDocumetn();
		或
		DocumentFactory factory = DocumentFactory.getInstance();
		Document document = factory.createDocument();
1. 创建根节点

		1、创建普通节点  
		Element root = DocumentHelper.createElement(String name);  
		2、将普通节点设置为根节点   
		document.setRootElement(普通节点对象);
1. 添加注释
		
		通过Element对象的addComment(String comment)方法
		
		Document document = DocumentHelper.createDocument();
		Element placard = DocumentHelper.createElement("placard");
		documen.setRoorElement(placard);
		placard.addComment("这是一个根节点");		
1. 添加属性

		通过Element对象的addAttribute(String name,String value);方法
		
		Documeen document = DocumentHelper.createDocument();
		Element placard = DocumentHelper.createElement("placard");
		document.setRootElement(placard);
		placard.addAttribute("version","2.0");
1. 创建子节点

		通过Element对象的addElement(String name)方法,返回一个Element对象
		Document document = DocumentHelper.createDocument();
		Element placard = DocumentHepler.createElement("placard");
		document.setRootElement(placard);
		Element description = placard.addElement("description");
1. 设置节点的内容

		1、将普通文本作为节点内容
		Element description = placard.addElement("description");
		description.setText("公告栏");
		2、将CDATA段设置为节点内容
		Element content_item = placard.addElement("content");
		content.addCDATA("人生自古两难全");
1. 设置编码

		在应用dom4j创建XML文档时，默认的编码集为UTF-8.但有时不一定要使用该编码集。
		OutputFormat format = new OutputFormat();
		format.setEncoding("UTF-8");
		
1. 设置输出格式

		在应用dom4j生成XML时，默认是采用紧凑的方式排版。
		OutputFormat format = OutputFormat.createPrettyPrint();//以缩进的方式输出XML。
1. 输出XML为文件

		1、未设置输出格式
		String fileURL = getServletContext().getRealPath("/")+"xml\\placard.xml";
		XMLWriter write = new XMLWriter(new FileWriter(fileURL));
		writer.write(document);
		writer.close();
		2、已经设置了输出格式或编码集
		OutputFormat format = new OutputFormat();
		format.setEncoding("UTF-8");
		String fileURL = getServletContext().getRealPath("/")+"xml\\placard.xml";
		XMLWriter writer = new XMLWriter(new File(fileURL),format);
		writer.write(document);
		writer.close();
		3、将XML输出到控制台
		XMLWriter writer =new XMLWriter(System.out,format);
		writer.write(document);
		**注意：输出到控制台不能调用XMLWriter的close()方法**
		4、将XML文档输出到浏览器
			//out是java.io.PrintWrite类的对象，也可以是response.getWriter()方法获得，也可以是JSP的内置对象out。
		XMLWriter writer = new XMLWrite(out,format);
		write.write(document);
	
##解析XML文档对象
1. 构建XML文件所对应的XML文档对象

		String fileURL = getServletContext().getRealPath("/")+"xml\\placard.xml";
		SAXReader reader = new SAXReader();
		Document document=reader.read(new File(fileURL));
		使用完后要释放document
		document.clearContent();
1. 获取根节点

		Element placard = document.getRootElement();
1. 获取子节点
		
		通过Element对象的element()方法和elements()方法实现
		1、element(String name)方法;获取指定节点名的子节点；返回Element
		2、elements(String name)方法;获取指定名称的全部子节点；返回List
		例子：
		Element root = document.getRootElement();
		Element description = root.element("description");
		-------------------------------------------------
		Element root = document.getRootElement();
		List list_item = root.elements("info");

##修改节点
1. 查询节点  
使用Element对象的selectSingleNode()方法和selectNodes()方法。
	
		1、selectSingleNode(String xpathExpression)方法;获取指定条件的唯一节点  
		xpathExpression:XPath表达式。使用反斜杠"/"隔开节点树中的父子节点，从而构成代表节点位置的路径。
		如果XPath表达式以反斜杠"/"开头，则表示使用的是绝对路径，否则使用的是相对路径。如果使用属性，则必须在属性名前加上@符号；
		*获取ID属性值等于1的info节点
		org.dom4j.Node item = placard.selectSingleNode("/placard/info[@id='1']");

		2、selectNodes(String xpathExpression)方法;获取符合指定条件的节点列表
		*获取根节点placard的子节点info的
		List list = placard.selectNodes("/placard/info");
1. 删除节点

		1、使用Element对象的remove(Element elemen)方法；返回值是boolean
		删除根节点placard的ID属性为1的子节点info
		Element item = (Element)placard.selectSingleNode("/placard/info[@id='1']")
		if(item != null){
			placard.remove(item);
		}
		2、批量删除
		document.getRootElement().elements("info").clear();
		
		
		
		
		