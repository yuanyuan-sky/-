#ES6
##let
1. let定义变量，相当于var，但是它所声明的变量只在let命令所在的代码块内生效。

		{
	        let a = 10;
	        var b = 20;
	    }
	    console.log(b);   
	    console.log(a);   会报错
		for (let j=0;j<10;j++){

	    }
	    console.log(j);		会报错，j只在for循环中可用  

2.同一个作用域内，let声明的变量不能重名

	{
		let i=8;
		let i="123"; 报错
	}

------------

	{
		let i=8;
		{
			let i="123"; 不会报错，但两个i不是同一个变量
		}
	}
	外层代码块的变量不会受内层代码块影响，内部代码块可以获得外不代码块的变量，反之不行

--------------
		for(let i=0;i<10；i++){
			let i="abc";   不会报错，但两个i不是同一个变量
		}

----------------

		for(let i=0;i<10;i++){
				每轮循环的i都是一个新的变量
		}
	
-----------

		var a = [];
		for (var i = 0; i < 10; i++) {
		  a[i] = function () {
		    console.log(i);
		  };
		}
		a[6](); // 10          每轮的循环都是在上一轮的变量i的值加一，所以最后是10

		var a = [];
		for (let i = 0; i < 10; i++) {
		  a[i] = function () {
		    console.log(i);
		  };
		}
		a[6](); // 6  a[1]();// 1   每轮的循环都是一个新的i变量，所以最后是每个i的值
3.let声明的变量不会发生变量提升

	var a = 10;
    function f() {
        console.log(a);    undefiend
        var a = 15;
        console.log(a);   15
    }
    f();    这是因为var声明的变量会发生变量提升，即把变量的声明提升到所在代码块的最上面，然后在具体的位置赋值。
4.暂时性死区
	
	var temp = 123;
    if (true) {
        temp = "123";     报错
        let temp;  
    }
	ES6规定，如果一个区域中存在let和const命令，这个区块对这两个命令声明的变量，从一开始就形成了封闭作用域。凡是在声明【前】使用这些变量的，就会报错；在变量声明之后就没问题

---

	function aaa(x = y, y = 5) {   报错，因为声明x的时候，y还没声明，如果反过来就不会有事
        console.log(x, y);

    }
    aaa();
暂时性死区的本质就是，只要一进入当前作用域，所要使用的变量就已经存在了，但是不可获取，只有等到声明变量的那一行代码出现，才可以获取和使用该变量。
##const 声明一个只读的常量。一旦声明，常量的值就不能改变。
1.作用域：与let命令相同：只在声明所在的块级作用域内有效。  
2.const命令声明的常量也是不提升，同样存在暂时性死区，只能在声明的位置后面使用。
3.const声明的常量，也与let一样不可重复声明。

	const a1 = 3.141593;
    const a2={ename:"tom"}
    a1 = 123;--------------------报错
    a2.ename = "kk";-------------正常
	a2里放的是对象的地址，a2修改的时候，没有修改栈里地址值，修改的是地址对应的属性
	a2={}       报错，修改了地址
![](https://i.imgur.com/FVkSdNR.png)
	
##变量的解构
	老版：var a=1;var b=2;var c=3;
	ES6：var [a,b,c]=[1,2,3];
##方法参数问题
	//ES6
	//如果调用这个参数时没有传参数，则参数默认值为‘哈哈’
	function aaa(p = "哈哈" ) {

    }
    //ES6之前的写法
    function f(p) {
        var a= p  || "哈哈";
    }
##map循环
	var a = [1, 2, 3, 4, 5, 6];
	    a.map(function (value,index) {
	        console.log(index + ":" + value);
	    });
map与forech的区别
map不会修改原数组，而是创建一个新数组执行操作，forech会修改原数组
##数据结构set类型：去重数组
add(元素)：返回值是数组本身，相同的元素只能添加一次
	var a = new Set();
    console.log(a.add(1));
    console.log(a.add(2));
    console.log(a.add(1));
	a[1,2];
	var b=[1,2,3,4,1,2];
	var m=new Set(b);直接去重
##Map对象:键值对的集合
	var a=new Map();
Map对象的方法   
1. set


	添加一个新元素 
	m.set("a", 1);
    m.set("b", 2);
1. clear()
	
		移除所有元素  
		a.clear();
1. delete(key)  

		移除指定的元素
1. forEach
	
		遍历  
		m.forEach(function (item,key) {
	
	       console.log(item + ":" + key);  
	    });
2. get(key)

	返回指定元素
	m.get("a")     1
1. has(key)

		判断是否包含指定元素  
		console.log(m.has("a"));有返回true，没有返回false


	
	