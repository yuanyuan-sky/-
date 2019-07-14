
#json
json:数据格式、xml也是数据格式
	
	{}对象
	[]数组
	，分隔对象中属性和数组中每一个元素
	：分隔对象中属性名和属性值
 
#AJAX
1. Asynchronous JavaScript and XML：异步的 JavaScript 和 XML
2. 页面不刷新，可以进行异步提交
3. 基于javascript中的XMLHttpRequest对象

##请求：get/post
http://...........?ename=tom&age=10    ?前是请求，？后是参数列表  
1. 以前提交请求：form表单和a的链接，页面会刷新

#jsonp
ajax不允许跨域  
跨域：域名和端口不一样就认为是跨域  
	
	http://127.0.0.1:8080
	http://localhost:8080
	http://192.168.41.254:8080

##jsonp原理
	利用<script src="">发送跨域请求
	服务端调用客户端的方法，将数据以参数的方式返回来


#Ajax跨域请求成功，却进error方法的解决方法
1. 检查返回的数据是否是严格的json格式（有没有回车空格什么的）
2. 指定callBack名称（不指定ajax默认生成，容易出问题）
    
        客户端：
        dataType:"json",

        jsonp:"callback",//指定参数名称

        jsonpCallback:"successCallback"//指定回调函数名称

        服务端：
        String callback=req.getParameter("callback");
      
        PrintWriter pw = resp.getWriter();
		pw.write(json);
        json=callback + "(" +json + ")";  //一定要和前端的回调函数名称对应上对应上

        
        变化
        请求地址
        http://127.0.0.1:8080/jee_ServletCRUD2/search3.do?callback=successCallback&_=1541305816619

        successCallback([{"syno":"X001","bzqdw":"","typelist":[{"fname":"消炎","id":1}],"pdate":null,"bzq":0,"id":0,"mname":"头孢","zxflg":0,"cfflg":0},{"syno":"X002","bzqdw":"","typelist":[{"fname":"消炎","id":1},{"fname":"保健","id":2}],"pdate":null,"bzq":0,"id":0,"mname":"肾宝片","zxflg":0,"cfflg":0}])

        默认的

        http://127.0.0.1:8080/jee_ServletCRUD2/search3.do?callback=jQuery1101049561611191319055_1541306649252&_=1541306649253//ajax默认参数名称是callback，回调函数名称随机生成


#AJAX的几种写法
##js

        <script>
        var abc = new XMLHttpRequest();
        function callback(data) {

            //将JSON字符串转为JSON对象,加[]最外层是数组
            var all = eval("(" + data + ")");
            console.log(all);

            all.rows.forEach(element => {
                var tr=`<tr>
                    <td>${element.productid}</td>
                    <td>${element.unitcost}</td>
                </tr>`;
                document.getElementById('table').innerHTML+=tr;
            });
            


        }
        function add() {
            //对象的打开方法
            /*
               第一个参数：请求方式；get/post
                第二个参数：请求地址
                第三个参数：false：同步   true：异步
                第四、第五参数：用户名、密码 
            */
            abc.open("get", "../data/datagrid_data1.json", true);
            /*
                对象发送ajax请求
                参数：post请求时，所需要带的参数列表数据
            */
            abc.send(null);
            /*
                状态变化回调
                对象状态：0、1、2、3、4
                0服务器未初始化   1服务器连接已建立  2请求已接受   3请求处理中  4请求已完成且响应已就绪
                http状态：200~600       200  404   500   505   403  
                200 成功状态  404找不到资源  500服务器代码报错
            */
            abc.onreadystatechange = function () {

                if (abc.status == 200 && abc.readyState == 4) {
                    //abc.responseText 是响应回来的数据
                    callback(abc.responseText);
                }
            }
        }
    </script>

##JQ1

        $.ajax({
            url: "../data/datagrid_data1.json",//请求
            type: 'get',  //get或post方式
            data: { "ename": 'tom' },//请求参数常用两种 1、js对象 2、参数名=参数值&参数名=参数值。。。
            async: true,  //true 默认值 异步请求     false：异步的同步(虽然本身是异步，但线程会等待其回来)
            dataType: 'json',//返回的数据类型
            cache:false,//是否启用浏览器缓存
            success: function (data) { //4和200 即成功时触发，data就是响应数据
                console.log(data);
            },
            error: function (data) {
                console.log(data)
            }
        })

##JQ2

     $.get("../data/datagrid_data1.json", { ename: 'tom' }, function (data) {
            console.log(data);
        },"json");

##load

    <script>
        //load把ajax返回的文本放入选择器的元素中
        //$("#div1").load('../data/datagrid_data1.json');
        //还可以用来加载其它页面
        $("#div2").load('../html/aaa.html');
    </script>
        
