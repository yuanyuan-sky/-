#1. VUE
1、注重数据（json）和视图（模板、标签）的绑定。  
2、响应式【双向绑定】。   

	OGNL---对象导航语言---根就是stu
	root----stu{ename:"tom",age:10}
	{{ename}}
3、MVVM模型  
 
	M:model 模型：数据模型、业务模型  
	V:view  视图：模板、标签，<div id="app">...</div>
	VM:viewmodel:视图和模型的封装，双向处理等。vue对象
#2.vue数据绑定
## 文本插值
		
	<div id="app">  
        <h1>{{message}} is interesting!</h1> 
    </div>  
    <script>  
        new Vue({  
            el:"#app",  **※el是element的缩写**不要忘了 **#**  
            data:{  
                message: "hello vue"  
            }  
        });  
    </script>
##html（v-html=""）

	<div id="app_8">
    	<div v-html="message"></div>
	</div>
	new Vue({
        el:"#app_8",
        data:{
            message:'<h1>啦啦啦</h1>'
        }
    });
##text (v-text="")同上，只是插入的是文本
**html标签的属性不用{{}} 而是用v:bind:**

#指令、指令带有前缀v-（条件与循环）
##条件（v-if=""）
	<div id="app_3">
        <p v-if="seen">你看见我了吗</p>
    </div>
	new Vue({
            el:"#app_3",
            data:{
                seen: false
            }
        });
	seen为true时显示，false时不现实
<h1 v-show="ok">Hello!</h1> 显示或者不显示
##v-else:
可以用 v-else 指令给 v-if 添加一个 "else" 块：

	<div id="app">
	    <div v-if="Math.random() > 0.5">
	      Sorry
	    </div>
	    <div v-else>
	      Not sorry
	    </div>
	</div>
##v-else-if
	
	<div id="app">
	    <div v-if="type === 'A'">
	      A
	    </div>
	    <div v-else-if="type === 'B'">
	      B
	    </div>
	    <div v-else-if="type === 'C'">
	      C
	    </div>
	    <div v-else>
	      Not A/B/C
	    </div>
	</div>

##循环（v-for="item in data"）
	<div id="app_4">
	    <ol>
	        <li v-for="item in todo">
	            {{item.text}}
	        </li>
	    </ol>
	</div>
	
	data: {
            todo: [{text: "学习"},{text: "只爱学习"}]
        }
###v-for迭代【对象】
	<ul>
        <li v-for="value in object"> //这里的value可以随便写，代表的是第一个参数，就是对象的值
            {{value}}
        </li>
    </ul>
	new Vue({
        el:"#app_12",
        data:{
            object:{
                name:"tom",
                url:"wwwww",
                slogan: "哈哈哈"
            }
        }
    });
	输出：·tom  ·wwwww    ·哈哈哈  
	-----------------------------
	<div id="app">
	  <ul>
	    <li v-for="(value, key) in object"> 第一个为值，第二个是键
	    {{ key }} : {{ value }}
	    </li>
	  </ul>
	</div>  
	-------------------------------
	<div id="app">
	  <ul>
	    <li v-for="(value, key, index) in object"> //第一个为值，第二个是键，第三个是索引
	     {{ index }}. {{ key }} : {{ value }}
	    </li>
	  </ul>
	</div>
### v-for迭代【整数】
	<div id="app_14">
	    <ul>
	        <li v-for="n in 10">
	            {{n}}
	        </li>
	    </ul>
	</div>
	new Vue({
        el: "#app_14"
    });
循环的嵌套（九九乘法表）
	<div id="app_15">
	    <div v-for="n in 9">
	        <b v-for="m in n">
	            {{m}}*{{n}}={{m*n}}
	        </b>
	    </div>
	</div>



**注意：通过代码在data里添加的属性，是不能实现响应式的，所有如果一个属性要实现响应式而开始又不用，最好提前声明，赋予初始值空值即可**
##Object.freeze,阻止修改现有属性，无法跟随响应
	<div id="app_7">
	    <p>{{foo}}</p>
	    <button v-on:click="aa">change</button>
	</div>
	var obj={
        foo:'bar'
    }
    Object.freeze(obj);  //这个obj对象将无法实现响应
	new Vue({
        el:"#app_7",
        data: obj,
        methods: {
            aa: function () {
                this.foo = "bbb";   //因为foo无法实现响应，所以不会改变

            }
        }
    });
#获取VOE属性
在VOE对象外面获取VOE属性  

		var data = { a: 1 }  
		var vm = new Vue({  
		  el: '#example',  
		  data: data  
		})
	
	vm.$data === data // => true
	vm.$el === document.getElementById('example') // => true

#使用js表达式
	<div id="app_10">
	    {{5+5}}<br>  
	    {{ok ? 'YES' : 'NO'}}<br>   //三元表达式
	    {{message.split('').reverse().join('')}}  //字符串反转
	    <div v-bind:id="'list'+id">啦啦啦</div>   //字符串的拼接
	</div>
	new Vue({
        el:"#app_10",
        data:{
            ok: true,
            message: "abcde",
            id: 1
        }
    });
**注意：每个绑定只能包含单个表达式**  
	
	{{var a=1}}
	{{if(ok){return message}}} 
	这两个都不会生效
#修饰符 
修饰符是以半角句号 . 指明的特殊后缀，用于指出一个指定应该以特殊方式绑定。 
 
	<form v-on:submit.prevent="onSubmit"></form>
	.prevent 修饰符告诉 v-on 指令对于触发的事件调用 event.preventDefault()：
#缩写
1.v-bind:    ------------   :

	v-bind:url="ttt"----------------:url="ttt"

2.v-on:       --------------  @

	v-on:click="todo"------------  @click="todo"
#过滤器
	<div id="app">
		{{ message | capitalize }}
	</div>
	new Vue({
	el: '#app',
	data: {
    	message: 'runoob'
	},
	filters: {
	    capitalize: function (value) {   value代表原来的值
	      if (!value) return ''
	      value = value.toString()
	      return value.charAt(0).toUpperCase() + value.slice(1)
	    }
		}
	})
过滤器可以串联
	
	{{ message | filterA | filterB }}先执行filterA，再执行filterB
#计算属性
1. getter 获取值，有返回值的
2. setter 设置值，有参数的

		<div id="app">
	        <p>{{message}}</p>
	        <p>{{remessage}}</p>
	    </div>
		new Vue({
	        el:"#app",
	        data:{
	            message: "hello"
	        },
	        computed:{
	            remessage: function () {       //默认的getter方法
	                return this.message.split("").reverse().join("");
	
	            }
	        }

    	});

	-----------------------------------------------
		<div id="app_16">
	    <p>{{ site }}</p>
		</div>
		<script>
		    var vm = new Vue({
		        el: '#app_16',
		        data: {
		            name: 'Google',
		            url: 'http://www.google.com'
		        },
		        computed: {
		            site: {
		                // getter方法
		                get: function () {
		                    return this.name + ' ' + this.url
		                },
		                // setter
		                set: function (newValue) {
		                    var names = newValue.split(' ')
		                    this.name = names[0]
		                    this.url = names[names.length - 1]
		                }
		            }
		        }
		    })
			// 调用 setter， vm.name 和 vm.url 也会被对应更新
		    vm.site = '菜鸟教程 https://www.runoob.com';//调用setter方法；先调用setter方法设置值，然后再调用getter方法返回值

#watch 响应数据的变化
当见监听的数据发生变化的时候，就会自动调用响应的方法
		   
	<div id = "app">
		    <p style = "font-size:25px;">计数器: {{ counter }}</p>
		    <button @click = "counter++" style = "font-size:25px;">点我</button>
		</div>
		var vm = new Vue({
	    el: '#app',
	    data: {
	        counter: 1
	    }
	});
	vm.$watch('counter', function(nval, oval) { //当counter发生变化时，自动调用次方法
	    alert('计数器值的变化 :' + oval + ' 变为 ' + nval + '!');
	});
	------------------------------	--------------------
	<div id = "computed_props">
	    千米 : <input type = "text" v-model = "kilometers">
	    米 : <input type = "text" v-model = "meters">
	</div>
	var vm = new Vue({
    el: '#computed_props',
    data: {
        kilometers : 0,
        meters:0
    },
	watch : {
        kilometers:function(val) { //当kilometers发生变化时，调用此方法
            this.kilometers = val;
            this.meters = val * 1000;
        },
        meters : function (val) { //当meters发生变化时，调用此方法
            this.kilometers = val/ 1000;
            this.meters = val;
        }
    }
    });


#样式绑定
## 绑定元素属性(v-bind:)

	<div id="app_2">
        <span v-bind:title="message"> **绑定属性不用{{}}**
            鼠标悬停
        </span>
    </div>
	v-bind 特性被称为指令，
##样式绑定
	
	.active {
		width: 100px;
		height: 100px;
		background: green;
	}
	<div id="app">
		//当isActive为true时，应用active，false不应用
	  <div v-bind:class="{ active: isActive }"></div>
	</div>
	new Vue({
	  el: '#app',
	  data: {
	    isActive: true
	  }
	})
	----------------------------------------------------------
	<div id="app">
	  <div class="static" v-bind:class="{ active: isActive, 'text-danger': hasError }">
	  </div>
	</div>
	上面的例子相当于给div加了三个class，只不过后两个class受变量控制
	**注意：绑定多个class时，后面的class要用 单引 引入**
	----------------------------------------------------------
可以把一个数组传给 v-bind:class

	<div id="app">
		<div v-bind:class="[activeClass, errorClass]"></div>
	</div>
	new Vue({
	  el: '#app',
	  data: {
	    activeClass: 'active',
	    errorClass: 'text-danger'
	  }
	})
也可以直接绑定到一个对象上

	<div id="app">
	  <div v-bind:style="styleObject">菜鸟教程</div>
	</div>
	new Vue({
	  el: '#app',
	  data: {
	    styleObject: {
	      color: 'green',
	      fontSize: '30px'
	    }
	  }
	})
也可以使用数组，将多个样式对象应用到一个元素上

	<div id="app">
	  <div v-bind:style="[baseStyles, overridingStyles]">菜鸟教程</div>
	</div>
	new Vue({
	  el: '#app',
	  data: {
	    baseStyles: {
	      color: 'green',
	      fontSize: '30px'
	    },
		overridingStyles: {
	      'font-weight': 'bold'
	    }
	  }
	})
**注意：给元素绑定href属性时，也可以绑定一个target**

	new Vue({
		el: '#app',
	 	data: {
	    url: 'http://www.runoob.com',
	    target:'_blank'
		}
	})

#事件处理（v-on:）
逆转消息

	<div id="app_5">
	    <p>{{message}}</p>
	    <button v-on:click="reverseMessage">逆转消息</button>  //添加绑定事件
	</div>
	new Vue({
	        el:"#app_5",
	        data:{
	            message: "hello vue!"
	        },
	        methods:{   //里面放绑定的方法
	            reverseMessage: function () {
	                this.message = this.message.split("").reverse().join("");
					//this.message获取data里的message
	            }
	        }
	    });
##事件修饰符
1. .stop  阻止事件冒泡

	<a v-on:click.stop="aaa"></>

1. .prevent  阻止默认提交

	<form v-on:submit.prevent="onsubmit"></form>

1. .capture  添加事件侦听器时使用事件捕获模式，就是发生冒泡事件的时候，有该修饰符的先发生事件，然后没有该修饰符的元素按冒泡顺序执行

	<div v-on:click.capture="doThis">...</div>

1. .once   只能点击一次

	<a v-on:click.once="doThis"></a>

1. .self  只当事件在该元素本身（而不是子元素）触发时触发回调，即通过冒泡传过来的事件不会触发函数

	<div v-on:click.self="doThat">...</div>

**注意：修饰符可以串联**<a v-on:click.stop.prevent="doThat"></a>
##按键修饰符
	
	<button v-on:keyup.enter="aaa">点击</button>
	当按下回车键触发函数，**注意：只有该按钮获得焦点的时候，按下回车才会触发**
#表单
用 v-model 指令在表单控件元素上创建双向数据绑定。
##v-model:"" 实现【表单】输入和应用状态之间的双向绑定
	<div id="app_6">
	    <p>{{message}}</p>
	    <input v-model="message">
	</div> 
	new Vue({
        el:"#app_6",
        data:{
            message: "哈哈"
        }
    });
	//p里的内容随着输入框内容的改变同步改变
##对于复选款	

1. 当v-model对应的是字符串时，v-model:"" 绑定的是checked属性

		tt为true时选中，false不选中
		<input type="checkbox" id="aaa" v-model="tt">
	    <label for="aaa">{{tt}}</label>
		new Vue({
	        el: "#app",
	        data:{
	            tt: false
	        }
	    });
1. 当v-model对应的是数组时

		<div id="app">
		    <input type="checkbox"  v-model="tt" value="aaa" />aaa
		    <input type="checkbox"  v-model="tt" value="bbb" />bbb
		    <input type="checkbox"  v-model="tt" value="ccc" />ccc
		    <input type="checkbox"  v-model="tt" value="ddd" />ddd
		    <input type="checkbox"  v-model="tt" value="eee" />eee
		    {{tt}}
		</div>
		new Vue({
	        el: "#app",
	        data:{
	            tt: ['ccc']
	        }
	    });
		当选中一个时，会把选中的value值放进tt这个数组中，同时，如果在tt的数组中放上默认的value值，则对应value值的checkbox将被选中
###select（单选下拉框）
	**注意：v-model写在select标签上**
	如果option没写value，则v-model绑定的是option之间的值，如果写了value，则绑定的是value值
	<div id="app">
        <select v-model="se">
            <option value="">----请选择-----</option>
            <option value="11111111">aaaaaaaaa</option>
            <option value="22222222">bbbbbbbbb</option>
            <option value="33333333">ccccccccc</option>
        </select>
        {{se}}
    </div>
	new Vue({
        el:"#app",
        data: {
            se: ''
        }
    });
###多选下拉框
	
	<div id="example-6">
	    <select v-model="selected" multiple style="width: 50px;">
	        <option>A</option>
	        <option>B</option>
	        <option>C</option>
	    </select>
	    <br>
	    <span>Selected: {{ selected }}</span>
	</div>
	new Vue({
        el: '#example-6',
        data: {
            selected: []
        }
    })
	如果option没有value，则绑定的是选中option标签之间元素的数组【A,B,C】,如果有value值，则绑定的是选中的option的value值得数组
###单选按钮
	<div id="example-4">
	    <input type="radio" id="one" value="One" v-model="picked">
	    <label for="one">One</label>
	    <br>
	    <input type="radio" id="two" value="Two" v-model="picked">
	    <label for="two">Two</label>
	    <br>
	    <span>Picked: {{ picked }}</span>
	</div>
	<script>
	    new Vue({
	        el: '#example-4',
	        data: {
	            picked: ''
	        }
	    })
	</script>
	v-model绑定的是value
###修饰符
	
1. .lazy  

		<div id="app">
		    <span>{{message}}</span><br>
		    <input type="text" v-model.lazy="message">
		</div>
		new Vue({
	        el: "#app",
	        data:{
	            message: "hello"
	
	        }
	    });
		正常v-model在文本框中，同步输入框与数据的值，即随着文本框的输入，message同步在变，而加上.lazy后，文本框在输入的时候，message不在同步，只有当按下【回车键】或者输入框失去焦点时，message才会去同步
1. .number
		
		<div id="app">
		    <span>{{message}}</span><br>
		    <input type="text" v-model.number="message" />
		</div>
		会将输入的值转换为number类型，如果输入的不是字符，则会保留最后一次是字符的状态，如果给message添加watch，则输入非数字时不会触发函数。正常情况下，即使input的type为number，获取的值也是string类型
		**注意：**即使这样，通过js获取的value值依旧为string类型，但是vue对象中的message为number类型
1. .trim

		自动过滤掉输入的收尾空格
#组件

##全局组件
在注册之后可以用在任何新创建的 Vue 【根实例】 (new Vue) 的模板中。比如：
	
	Vue.component('component-a', { /* ... */ })
	Vue.component('component-b', { /* ... */ })
	new Vue({ el: '#app' })
	<div id="app">
	  <component-a></component-a>
	  <component-b></component-b>
	</div>
	
	<script>
		//注册
	    Vue.component('runoob',    //组件名
		{
	        template: "<h1>自定义组件</h1>"
	    });
	</script>
	<div id="app">
	    <runoob></runoob>          //相当于上面的h1
	</div>
	<script>
	    new Vue({
	        el: "#app"
	    });
	</script>
##局部组件
这样的组件只能在当前的实例中使用

	<div id="app">
    	<runoob></runoob>
	</div>
	<script>
	   var child={
	       template:'<h1>自定义局部组件</h1>'
	   }
	   new Vue({
	       el: "#app",
	       components:{
	           'runoob': child
	       }
	   });
	</script>
##prop

	<div id="app">
	    <child message="hello"></child>
	</div>
	<script>
	    Vue.component('child', {
	        template: '<span>{{message}}</span>',
	        props: ['message']
	    });
	    new Vue({
	        el: "#app",
	    });
	</script>
结果如下  
![](https://i.imgur.com/FKwlimh.png)
###动态Prop
	<div id="app">
	    <div>
	        <input type="text" v-model="parentMsg">
	        <br>
	        <child :message="parentMsg"></child>   
	    </div>
	</div>
	<script>
	    Vue.component('child', {
	        template: '<span>{{message}}</span>',//这里的message就是prop的值
	        props: ['message']
	    });
	    new Vue({
	        el: "#app",
	        data:{
	            parentMsg: "父组件的内容"
	        }
	    });
	</script>
	父组件就是#app这个div，里面的就是子组件
**注意：prop是单向绑定的：当父组件的属性变化时，将传导给子组件，但是不会反过来**
###自定义事件
如果子组件要把数据传给父组件，就需要使用自定义事件


#路由
在页面不刷新得情况下，通过url指向不同的模板。
通常要配置一个路由对象，包含
