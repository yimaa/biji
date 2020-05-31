# VUE基础知识点 #
## 1.VUE介绍
vue.js是一个MVVM框架库，优势如下：

* 1.非常容易上手的API
* 2.轻巧、高性能、可组件化
 
#### 资料
* 1.vue文档地址：https://vuejs.bootcss.com/v2/guide/
* 2.vue.js文件地址：https://cdn.jsdelivr.net/npm/vue/dist/vue.js 

#### MVVM模式
* Model：负责数据，例如从服务器请求到的数据
* View：负责页面展示，一般指的是html页面
* View Model：负责业务逻辑处理，对model的数据进行加工后交给view展示，就是一个桥梁作用将view和model给联系到一起 

#### vue使用步骤

* 1.使用script标签引入vue.js文件
* 2.书写js代码：

	  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js "></script>
	  new Vue({
	    	el:'#id值', 
	    	data:{
	    		message:'hello Vue!',
	    	}  
	   })

* 3.在html页面中，如果想要使用data里面的变量，直接 {{变量名字就可以使用}}
	
		<h1>{{message}}</h1>


## 2.常用指令
#### 绑定数据
* 1.直接使用 {{message}} => 输出message对应的内容  
* 2.在{{}}里面可以进行数学运算 
    * {{num + 1}}=>输出num+1的结果   
    * {{m + n}}=>输出num+n的结果
* 3.在{{}}里面进行三元运算： 
    * {{条件?值1：值2 }}=>条件成立，输出值1，否则输出值2 
    * {{score > 60 ?'及格':'不及格'}}

#### v-text
* v-text：类似于dom的innerText属性

    	var str = '<h1>大标题</h1>'
    	{{str}}  将str原样输出


#### v-html
* v-html：类似于dom的innerHtml属性

	    var str = '<h1>大标题</h1>'
    	{{str}}  将str里面的标签解析成标签输出


#### v-bind动态的绑定标签属性
* a.基本用法: v-bind：属性名="变量名" 
	
		v-bind:class=""   v-bind:value=""  v-bind:src=""等

* b.简写:将v-bind简写为 冒号(:)，即v-bind：属性名="变量名" 简写为 ：属性名="变量名"

		v-bind:class=""  简写为  :class=""
		v-bind:value=""  简写为  :value=""   
		v-bind:src=""    简写为  :src=""


* c.同时绑定静态class: 如果使用v-bind:class绑定一个动态的class，还可以在通过class来绑定一个静态的class 

		<div v-bind:class="className" class="wrap divbox"></div>


#### v-on：监听dom事件
* 1.常用的事件有：v-on:click 、 v-on:keyup等
* 2.事件对象的方法是自定义方法，所以需要写在methods里面
* 3.v-on: 可以简写为 @ v-on:click 等同于@click ，v-on:keyup等同于@keyup
* 4.在方法里面可以通过this.变量名字获取到data里面的数据

		<button v-on:click="changeTitle">按钮</button> 
		data:{ 
			message:'hello',
		},
		 methods:{
		    changeTitle(){
			    console.log(this.message); 
		    },
		 },


#### v-if：条件渲染
如果条件不成立，该元素根本不会被渲染

* v-if   
* v-else-if  
* v-else 	

		<div v-if="sex == 1">男</div>
		<div v-else-if="sex == 2">女</div>
		<div v-else>秘密</div>


#### v-for：列表渲染
* v-for="item in 对象变量名"
* v-for="(item,index) in Array"
* v-for="(value,key) in Object"
    * item表示遍历的当前项，index表示遍历的当前索引
    * 如果不需要索引用第一种写法，需要索引第二种写法
    * item/value和index/key是自定义变量名，可以用任意变量名替代

			<ul>
			    <li v-for="(item,index) in array">{{item}}</li>
			</ul>
			data:{ 
				array:['北京','上海','郑州','西安','深圳'],
			},


#### v-model表单数据双向绑定
* 1.在表单控件或者组件上创建数据双向绑定
* 2.v-model仅能在如下元素中使用： 	input、    select、    textarea
* 3.使用方式：在input，select，textare标签身上加v-model=”变量名”，该变量名需要在data里面定义好

		<input type="text" v-model="username">
		<textarea v-model="description"></textarea>
		<select name="" id="" v-model="sex"></select>

#### v-bind:class绑定class
* 1.基础语法    <div v-bind:class="变量名"></div>

		<div v-bind:class="variableName"></div>
		渲染为<div class="current"></div>	 
		new Vue({
		    data:{
		        variableName:'current',
		    }
		}）

* 2.对象语法    <div v-bind:class="{ class名字: 布尔值 }"></div>

		<div v-bind:class="{ first：isFirst，'v-last'：1==10 }"></div>
		渲染为<div class="first"></div>
		data:{
		    isFirst:true,
		}

* 3.数组语法    <div v-bind:class="[变量名1, 变量名2]"></div>

		<div v-bind:class="[classStr1,classStr2]"></div>
		渲染为<div class="current red"></div>
		data:{
			classStr1:'current',
			classStr2:'red',
		}

* 注意：如果class名字有连接符，可以用引号包裹起来

## 3.修饰符
#### v-on 事件修饰符
* .stop - 阻止向上冒泡。@click.stop

		<button @click.stop="clickFn4">按钮</button>

* .prevent - 阻止元素发生默认的行为，例如，当点击提交按钮时阻止对表单的提交@sbumit.prevent

		<form action="##" method="post" @submit.prevent></form>


#### keyup修饰符
* .enter
* .tab
* .delete ("删除"和"退格"键)
* .esc
* .space
* .up
* .down
* .left
* .right

		 <input type="text" 
		    placeholder="用户名" 
		    @keyup.left="onLeft"  
		    @keyup.right="onRIght"
		    @keyup.up="onUp"
		    @keyup.down="onDown"
		    @keyup.space="onSpace"
		    @keyup.esc="onEsc"
		    @keyup.delete="onDelete"
		    @keyup.tab="onTab"
		    @keyup.enter="onEnter"
		>


#### v-model修饰符
* .lazy  :  v-model 在每次 input 将输入框的值与数据进行同步，如果添加 lazy 修饰符，可以转变为使用 change 事件进行同步
* .number : 正常情况下，即使用户输入的是数字，通过js取出来的还是字符串类型，但是.number能够保证取出来的就是number类型
* .trim : 去除首尾空白字符

		<input type="text" placeholder="用户名" v-model.trim="username" />


## 4.获取dom对象
* 1.在标签里面加入 ref=”自定义名字”
* 2.在js里面，通过this.$refs 获取到所有的定义过ref的dom对象
* 3.通过this.$refs.自定义名字，可以获取到具体的dom对象

## 5.生命周期
* beforeCreate：此时还不能获取到data
* created：此时可以获取到data的数据，但是获取不到dom元素
* beforeMount：同created一样
* mounted：可以获取到data数据和dom元素
* beforeUpdate
* updated：页面元素或者数据发生改变时触发
* beforeDestroy
* destroyed：vue实例销毁时触发

## 6.axios实现http请求

#### axios.get()
语法：

	axios.get('url地址?key=value').then((res)=>{   
	  res.data //服务器返回的数据   
	})
例子：

	axios.get('/getGoodLists.php?pagenum=2').then((res)=>{
	    console.log(res.data);
		this.cardList = res.data.result;
	})


#### axios.post()
语法：

	axios.post('url地址',{ 传递给服务器的数据 }).then((res)=>{  
	    res.data //服务器返回的数据  
	})

例子：

	axios.post('/postGoodLists.php',{
	    pagenum:3,
	}).then((res)=>{
	    console.log(res.data);
	    this.cardList = res.data.result;
	})


#### axios.config()
get配置：

	axios({  
	    url:' ', //请求的接口地址  
	    method:'get',  //默认值 get是默认值  
	    baseURL:'http://地址',  //baseURL和url拼接结果才是真正的请求地址  
	    params:{  //替代了 ?key=value  
	        key:value, //传递给服务器的参数  
	    },  
	    responseType:'json', // 默认值是json，还可以取值text, 一般情况下，有经验的后台开发者给我们的数据都是json，所以这里基本上可以省略  
	}).then((res)=>{  
	     res.data  //服务器返回的数据    
	})

post配置：

	axios({
	        url:' ', //请求的接口地址
	        method:'post',  //默认值 get是默认值
	        baseURL:'http://地址',  //baseURL和url拼接结果才是真正的请求地址
	       data:{ //method为get时不可用
	            key:value, //传递给服务器的参数
	        },
	       responseType:'json', // 默认值是json，还可以取值text
	 }).then((res)=>{
	        res.data  //服务器返回的数据                                    
	 })


#### axios all

	axios.all([
	    this.getOrderData(-1), 
	    this.getOrderData(0), 
	    this.getOrderData(1),
	    this.getOrderData(2),
	    this.getOrderData(3),
	]).then(axios.spread(function (arg1,arg2) {
	    console.log('两个请求都完成了')
	    console.log(arg1,arg2)
	}));

## 7.自定义指令
#### 定义：全局指令和局部指令
* 1.全局
	* Vue.directive() 此方式定义的指令为全局指令，该页面所有的vue都可以使用：
	* 定义全局的任何代码，必须写在创建 Vue 实例之前

			Vue.directive（'自定义指令的名字',{
				inserted(el，binding){
					el：//指令所绑定的元素
					binding:{}  //指令信息对象
			  	}, 	
			}）
			<div v-自定义指令名字="值"></div>
 
* 2.局部（建议局部）  

		new Vue({
			el:'#app',
			directives:{  //这个里面的指令，只对id为app的区域有效
				自定义指令名字：{
					钩子函数：（el，binding）{  函数体}
				}	
			}
		})

#### 自定义指令的生命周期
* bind() 只调用一次，指令第一次绑定到元素时调用
* inserted() 被绑定元素插入父节点时调用

#### 自定义指令的生命周期
* el  指令所绑定的元素
* binding  一个对象
    * name：指令名，不包括 v- 前缀。
    * value：指令的绑定值，例如：v-mydirective="2" 中，绑定值为 2。
    * arg：传给指令的参数，可选。例如 v-mydirective:foo 中，参数为 "foo"。


## 8.过滤器

#### 过滤器的使用方式
* {{ 变量名字 | 过滤器名字(参数) }}
* v-bind:属性名="值 | 过滤器名字"
* 参数可以省略 {{ 变量名字 | 过滤器名字 }}

		{{number | foFixed}}  {{number | foFixed(2)}}
		v-bind:id=”idName | captial”


#### 过滤器定义方式
局部：

	new Vue({
	    el:'#app',
	     filters:{
	        过滤器名字(value,arg){
	              return 过滤的结果；
	        },
	    }
	})


全局：

	Vue.filter(过滤器名字，(value,arg)=>{
	   return 过滤的结果;
	})


#### 过滤器的参数
* 1.value:要过滤的数据  
比如 {{message  |  captial}} 那么message就是value的参数值
* 2.arg参数：过滤器（）里面传递的参数，和正常的fuction调用类似  
比如{{number | toFixed(2) }}  2就是arg参数

## 9.自定义组件
#### 组件定义方法
* 第一步：将公用的html代码放在tempate标签里面，然后写在body标签里面

		<body>
		    <template id="id值">
		   这个template标签里面的内容必须有一个标签包裹起来才可以
		    </template>
		</body>


* 第二步：通过vue注册一下

		Vue.component('自定义组件名字',{
		    template:'#id值'，
			data:function(){ //data里面的数据，是供组件使用的
		        return { // data在这里是一个方法，而且必须配合return{}使用
		            key:value,		
		        }	    
		    },
		    methods:{//methods里面的方法，供组的方法
		        自定义方法(){},
		    }
		});


#### 父组件给子组件传值

* 1.在父组件中调用子组件的标签里面，通过v-bind:变量名字="要给子组件传递的值"来传值  
<组件名字 v-bind:变量名="要给子组件传递的值"></组件名字>
* 2.在组件的js代码里面，通过props属性来接收传过来的值：props:['变量名字']	  

		Vue.component('组件名字',{
		    template:'#,
		    props:["变量名"],//这里的变量名要和上面的变量名一模一样
		}）

* 3.使用：直接将props里面的变量当做正常的组件变量使用即可  

 		{{变量名}}   v-if=”变量名” v-for=”item in 变量名”


#### 子组件给父组件传值
* 1.在子组件中通过this.$emit('方法名字',值)来给父组件传值

		this.$emit('eventFromChild',value);


* 2.在父组件中，在调用子组件的时候通过v-on:eventFromChild=“fn”来接收值，在父组件中定义fn()方法，参数就是传递过来的值

		<navmenu v-on:'eventFromChild'="getValueFromChild"></navmenu>
		getValueFromChild（value）{  }


## 10.transition动画
#### vue过渡动画的使用步骤
* 1.想要那个标签有动画效果，就需要在该标签的外面，包裹一个transition标签
* 2.由于要给动画写css样式，所以需要给transition标签加一个name属性
* 3.由于vue的过渡动画是在元素插入和移除时触发，所以一般会在想要有动画效果的元素身上加上v-if 或者 v-show
* 4.通过修改v-if的值来达到让元素显示隐藏的目的

		<transition  name="fade">
		    <div  class="box" v-show="isShow"></div>
		</transition>


#### vue过渡动画的过渡的类名
* 1.元素在由隐藏状态到显示状态的类名：
    * v-enter：用来定义元素显示的那一瞬间的css状态，查看视频
    * v-enter-active：整个过渡一直存在的类名，可以用来定义transition属性
* 2.元素在由显示状态到隐藏状态的类名
    * v-leave-active：整个过渡一直存在的类名，可以用来定义transition属性
    * v-leave-to：用来定义元素隐藏的最终css状态
* 3.v-是class类名的前缀，需要使用transition的name属性值来替换

#### transition结合animate动画库使用
自定义过渡类名的主要优点就是，可以使用市面上比较优秀的C3动画库  
animate.css库的地址：https://daneden.github.io/animate.css/?  
在transition标签身上加以下属性：
* enter-active-class=”显示的动画类名”
* leave-active-class=”显示的动画类名”
* :duration="{ enter: 500, leave: 800 }" 
* enter定义显示的动画时间，leave定义隐藏的动画时间  
提示：一定不要忘记给动画的标签身上加animated类名

		<button @click="isShow = !isShow">切换显示隐藏div</button>
		<transition  name="slide" 
		enter-active-class="bounceInRight" 
		leave-active-class="bounceOutRight" 
		:duration="{ enter: 500, leave: 4800 }">
		   <div v-show="isShow" class="animated"></div>
		 </transition>


## 11.watch
watch用来监控数据，如果我们需要在数据发生变化的时候，进行操作，就需要用到watch 

deep默认是false，加deep：true是为了深度监听

	data:{},
	methods:{},
	watch:{
	    要监控的变量：{ //这个变量必须是已经定义过的
	        handler:function(newVal,oldVal){
	            newVal 最新值  oldVal  之前的值
	            这里面书写数据变化之后的逻辑
	        },
	        deep:true,
	    }	
	},


## 12.computed
computed 用来做数据计算，computed里面的变量不能在data里面定义，这一步就相当于是在定义变量，并且计算变量的值，并且可以充当watch的监听功能

	data:{},
	methods:{},
	computed:{
	    要计算的变量：function(){
	        return '结果';
	    }	
	},



## 13.快速删除nde_modules的方法

* 1.全局安装rimraf：

		npm install rimraf -g

* 2.到你的项目根目录下（即有node_modules的目录），执行命令：
	
		rimraf node_modules

# vue组件页面

## 1.vue文件介绍
三个元素组成：template，script，style，

	<template>
	</template>
	<script>
	export default {
	 	
	}
	</script>
	<style >
	</style>

#### (1)template标签
* template标签里面书写的html代码，可以使用任何vue的指令
* tempalte里面必须有一个大标签包裹起来，否则报错
 
#### (2)script标签
* 1.必须使用 export default{} 导出一个 Vue的实例 
* 2.在export default{}里面可以定义data，methods，生命周期等

		export default {
		    data(){
		        return {   }
		    },
		    methods:{   },
		    beforeCreate(){  },
		    created(){},
		    beforeMount(){},
		    mounted(){ },
		}


#### (3)style标签
* 1.style标签可以添加一个属性scoped，表示该style里面的样式是私有的，只有该组件可以使用
* 2.如果该组件不需要写css样式的话，最好把该组件的style标签删掉


		<template>
		   <div> 
		       <h3>{{title}}</h3>
		       <h3>{{title}}</h3>
		       <h2>{{title}}</h2>
		       <h2>{{title}}</h2>
		      <ul>
		          <li v-for="(item,index) in list" :key="index" >{{item}}</li>
		      </ul>
		       <ul>
		          <li v-for="(item,index) in list" :key="index" >{{item}}</li>
		       </ul>
		   </div>
		</template>
		
		<script>
		export default {
		    data(){
		        return {
		            list:['喜羊羊','美羊羊','灰太狼','小灰灰','红太狼','暖羊羊'],
		            title:'羊村成员'
		        }
		    },
		    methods:{
		
		    },
		    created(){},
		}
		</script>
		<style scoped>
		   h3{font-weight: normal;font-size:20px;}
		   li{list-style: none;font-size:18px;color:#333;}
		</style>

#### 4.vscode安装插件

vscode默认不识别vue文件，所以没有任何提示代码， 我们找到扩展工具安装vue插件：

在VSCODE软件里面，打开扩展，搜索vetur，点击安装，时间比较长，需耐心等待，安装完成之后，可以看到vue页面的代码就有了色彩

## 2.父访问子childre-refs
我们可以通过属性绑定和props实现父组件给子组件传参，那么如果想要在父组件访问子组件的属性和方法，就需要使用chilren或者refs来解决

#### children
通过 this.$children 可以获取当前组件引用的所有子组件，返回值是一个数组

* this.$children[index].属性名字  可以获取子组件的属性
* this.$chilren[index].方法名字()   可以调用子组件的方法

#### parent
通过 this.$parent 可以获取当前组件父组件

* this.$parent.属性名字  可以获取子组件的属性
* this.$parent.方法名字()   可以调用子组件的方法

#### refs
给子组件加ref="名字" 属性，然后通过 this.$refs.名字 可以获取对应的子组件

* this.$refs.ref属性值.属性名字  可以获取子组件的属性
* this.$refs.ref属性值.方法名字()   可以调用子组件的方法

注意：this.$chilren 和 this.$refs 在created阶段是获取不到的

## 3.slot插槽
slot插槽：用于决定将所携带的内容，插入到指定的某个位置，从而使模板分块，具有模块化的特质和更大的重用性

#### 基础使用
1.在子组件中使用`<slot></slot>`标签，可以定义一个插槽
2.在父组件中，引用子组件的那个标签中，可以放入一些其他标签，这些标签将会替代子组件的slot标签

	子组件
	<template>
	    <div>
	      <slot></slot>
	      <h1>哈哈</h1>
	    </div>
	</template>
	父组件中引用：
	<comp>
      <h2>嘻嘻嘻嘻</h2>
      <p>哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈</p>
    </comp>

#### slot默认标签
我们可以在slot标签中加入一些标签，当做默认标签，这样的话，所有引用该组件的父组件，都会渲染slot里面的默认标签 

	<slot><h1>哈哈</h1></slot>

#### 具名slot插槽
* 1.给slot标签加name属性
* 2.在引用的时候，使用template标签包裹，并且给template标签加v-slot:slot的name属性值

		<slot name="left"></slot>
	    <slot name="center"></slot>
	    <slot name="right"></slot>

		<comp :navs="navs" ref="hello">
	      <template v-slot:left>
	       	<a href="#">返回</a>
	      </template>
	      <template v-slot:center>
	        <span>标题</span>
	      </template>
	      <template v-slot:right>
	        <button>更多</button>
	      </template>
	    </comp>

#### 插槽子组件给父组件传值
* 1.给slot加一个自定义属性，属性值是我们要传递的值
* 2.子引用的时候通过给tempalte的v-slot加参数来接收

		<slot name="test" scope="小明"></slot>
		<template v-slot:test="data">
	        <h1>{{data.scope}}</h1>
	    </template>

## 4.a.vue页面引用b.vue组件
* 1.在a.vue页面使用import引入b.vue
	
		import ym_nav from '../components/b.vue'
* 2.在js中注册
		
		export default {
		   components:{
		      ym_nav,
		   },
		   data(){
		      return {
		
		      }
		   },
		}


# 路由
## 1.vue-router安装使用
vue-router 是vue官方的路由管理器
* 1.安装  	
		
		npm install vue-router --save
* 2.引入插件：
    * (1) 在main.js里面引入vue
    * (2) 在main.js里面引入vue-router
    * (3) 需要user一下vue-fouter

			import Vue from 'vue'
			import VueRouter from 'vue-router'
			Vue.use(VueRouter);
		
* 3.定义router：routes 用来规定路由规则，属性值是一个数组，有一个路由，就写多少项		
		
		const router = new VueRouter({
		    routes:[
        		{
            		path:'/login'，路径，这里的属性值和router-link的属性值必须保持一致
            		component:Login，属性值是组件的名字
        		},
			],
		});

注意：网站首页的路径是'/'


* 4.在vue实例中引用上一步定义的router

		new Vue({
		    el:'#app',
		    router,
		});


## 2.vue-link
* 1.使用router-link标签来替代之前 a标签
* 2.router-link的属性：
	* to 用来定义路由的跳转地址
	* tag 默认router-link会被选渲染成a标签，我们可以通过tag属性配置成其他标签

		<router-link  to="/login" tag="li"></router-link> 

注意：

* 1.router-link标签必须有to属性
* 2.to的属性值必须通过vuerouter配置过才可以成功跳转


## 3.router-view
router-view标签就是一个占位符，路由配置让显示什么，他就显示什么。根据路由切换显示不同的内容

	<template>
	   <div> 
	        <router-link to="/login">登录</router-link>
	        <router-link to="/register">注册</router-link>
	        <router-view></router-view>
	   </div>
	</template>


## 4.redirect重定向
 
	 {
	    path:'/',
	     redirect:'/login',
	 }, 
 
这段代码的含义是：
* 当浏览器加载根目录（首页）的时候，router-view自动显示到login组件
* 路径是'/'表示处于网站首页

## 5.路由嵌套
router-view加载的组件里面，还有一个router-view标签，这种关系就形成一种路由嵌套关系

在子路由里面通过chidren来配置子路由

	 {
	      path: '/home',  //主路由路径
	      component: Home, //主路由加载的组件
	      children:[ //子路由集合
	        {path: '',redirect: 'order'},//嵌套的子路由不要加/了
        	{path: 'order',component: order},
	     ]
	 }

在vue-link的to属性里面，我们书写地址的时候加上父路由的名字

	<router-link to="/home/order" >首页</router-link>




## 6.动态路由
#### 传参方式1：params

在配置动态路由的时候，path是这种格式： 

	path: '/路径/:属性名' 
	path: '/user/:id/:name/:age',

在router-link中to里面这么写

	<router-link :to="'/路径/'+属性名">用户</router-link>
	<router-link :to="'/test/'+id+'/'+name+'/'+age">测试</router-link>

或者 在js里面这么写

	 this.$router.push({
	    name:'atest',
	    params:{
	        id:'12',
	        age:18,
	        name:'哈哈'
	    }
	});

可以通过以下语句获取动态路由的参数

	this.$route.params.属性名

例子

	路由配置：
	{
	  path: '/user/:userid',
	  component: User
	},

	路由使用：
	<router-link :to="'/user/'+userid">用户</router-link>

	获取参数:
	computed:{
	    userid(){
	        return this.$route.params.userid;;
	    }
	}

#### 传参方式2：params

路由正常写法

	{
      path: '/user',
      component: User
    },

在route-link中to的属性值为：

	<router-link :to="touser" >用户</router-link>

	touser:{
        name:'路由名字',
        params:{
           username:'xiaoming',
           age:18,
           height:188
        }
     }


#### 传参方式3：query

路由正常写法

	{
      path: '/user',
      component: User
    },

在route-link中to的属性值为：

	<router-link :to="touser" >用户</router-link>

	touser:{
        path:'路由path',
        query:{
           username:'xiaoming',
           age:18,
           height:188
        }
     }


	

## 7.路由懒加载

假设你有一个庞大的管理系统，没有做懒加载，当用户首次访问的时候，js 文件加载时间过长，页面上会显示为白屏，用户体验极差。

1.使用方式：在router文件里面的index.js中，修改组件的引用方式

将 `import Login from '@/view/login'` 改为 `const Login = ()=> import('@/view/login');` 

用这种方式打包的文件，会多很多js文件，做到了将js分包处理

2.代码示例：

	const Login = ()=> import('@/view/login');
	const Home = ()=> import('@/view/home');
	routes: [
	    {
	      path:'/',
	      redirect:'/login',
	    }, 
	    {
	      path: '/login',
	      component: Login
	    }
	]

## 8.在方法里面跳转路由

this.$router.push('/路径名字'); 就可以实现路由跳转

实现点击跳转路由：

* 1.在标签身上加@click=””
* 2.在方法中书写  this.$router.push('/路径名字');

		<button @click="jumpRouter('order')"></button>
	 	methods:{
	        jumpRouter(routerName){
	            this.$router.push('/'+routerName);
	        },
	    }


## 9.全局导航守卫

* 1.可以监听路由跳转
* 2.可以在不满足要求的时候，禁止路由跳转

		router.beforeEach((to,from,next)=>{
		  console.log(to);//to指的是当前所处于的路由
		  next();
		})

案例1：监听路由跳转，修改网页的title

	导航守卫的代码：
	router.beforeEach((to,from,next)=>{
	  document.title = to.matched[0].meta.title;
	  next();
	})
	需要router里面配置一个meta作为参数配置：
	{
    	path: '/login',
	    name: 'Login',
	    component: Login,
	    meta:{
	      title:'登录',
	    },
	},

案例2：如果用户没有登录，直接进入首页，我们需要强制将路由跳转到登录页

用户登录成功之后，可以将用户的userid存入到本地设备，当用户进入其他页面时，判断本地存不存在该字段，如果存在那么继续跳转路由，如果不存在，就直接将路由跳转到登录页

	router.beforeEach((to,from,next)=>{
	  var userid = sessionStorage.getItem('userid');
	  if(to.name != 'Login'){
	    userid ? next(): next('/login');
	  }else{
	    next();
	  }
	})

## 10.keep-alive 组件缓存
当我们由一个路由跳转到另一个路由的时候，组件会跟随着创建和销毁，如果用户频繁切换会造成频繁创建和销毁，所以，我们可以将打开过得组件缓存下来

只需要在router-vie外面套一个keep-alive标签即可

	<keep-alive >
	  <router-view/>
	</keep-alive>

如果我们想要某个组件不缓存，可以使用exclude属性去排除，属性值是需要排除的组件的name属性值，可以排除多个，中间用逗号隔开即可

	<keep-alive exclude="user,login">
	    <router-view/>
	</keep-alive>

	login组件：
	export default {
	  name:'login',
	}

# element-ui
## 安装和引用
* 1.安装命令	npm i element-ui -s
* 2.引用:element-ui是依赖vue的，所以必须先引入vue，在引入element-ui,需要单独引入css文件

		import Vue from 'vue';
		import ElementUI from 'element-ui'
		import 'element-ui/lib/theme-chalk/index.css';
		Vue.use(ElementUI)


# vue-cli脚手架

* 1.vue-cli就是vue的脚手架，用来一键生成vue+webpack的项目模板，包括vue-router，vue-loader等各种必须的依赖库，免去你手动安装各种插件的麻烦
* 2.以后我们开发vue项目，都是用这一套脚手架即可
* 3.现在用的最多是3版本

## 1.安装使用

#### vue-cli2版本的安装使用

* 1.安装命令：	npm install  vue-cli  -g
* 2.查看是否安装成功：  vue --version 如果正确输出版本号表示成功   
* 3.创建项目命令： vue init webpack 项目名字

	* Project name：项目名称，默认 回车 即可
	* Project description：项目描述，默认 回车 即可
	* vAuthor：项目作者，默认 回车 即可
	* Install vue-router：是否安装 vue-router，默认 回车 即可
	* Use ESLint to lint your code：是否使用 ESLint 做代码检查，选择 n 不安装
	* Set up unit * tests：单元测试相关，选择 n 不安装
	* Setup e2e tests with Nightwatch：单元测试相关，选择 n 不安装
* 4.在终端运行npm  run dev
* 5.在浏览器输入localhost:8080，就可以看到画面

#### vue-cli3,4版本的安装使用
* 1.安装：如果电脑上已经安装了2版本，那么需要执行这两个命令安装3,4版本：
	* npm uninstall -g vue-cli
	* npm install -g @vue/cli
* 2.查看是否安装成功：  vue --version 如果正确输出版本号表示成功 
* 3.创建项目命令： vue create 项目名字

	* Please pick a preset: 选择 Manually select features 回车之后通过空格键来控制该选项是否选中配置，自己根据需求进行配置，下面几项可以选中
	
		* Babel
		* Router
		* Vuex
		* CSS Pre-processors
	* Use history mode for router? 可以选择no，后期再手动更改
	* Pick a CSS pre-processor ：选择less
	* Where do you prefer placing config for Babel, ESLint, etc：默认即可
	* Save this as a preset for future projects? 是否将改配置保存
	* 将自己的配置保存成一个名字，便于下次直接选择
* 4.在终端运行 npm  run serve
* 5.在浏览器输入localhost:8080，就可以看到画面
* 6.在任意很窗口输入命令：vue ui  可以打开一个vue-cli的ui管理界面


## 2.安装和引入element-ui
* 1.安装命令	
	
		npm i element-ui -s
* 2.在main.js中引用 

		import Vue from 'vue';
		import ElementUI from 'element-ui'
		import 'element-ui/lib/theme-chalk/index.css';
		Vue.use(ElementUI)


## 3.使用npm安装axios
* 1.安装

		npm install axios

* 2.在main.js里面

		import Axios from 'axios'
		Vue.prototype.axios = Axios;

* 3.使用：只需要 this.axios.post() 或者  this.axios.get()即可

## 4.打包项目
执行命令：

	npm run build

然后可以发现多了个dist文件夹，里面的文件就是我们生成的文件

## 5.默认配置打包之后，可能会产生路径问题，我们这么解决：

#### 1.vue-cli2这么解决

* 1.打开config/index.js文件，修改build里面的assetsPublicPath为空字符串，其他项不用修改
	
		build: {
	    	assetsPublicPath: '',
		}

* 2.打开build/utils.js文件夹，找到这个代码，然后publicPath为'../../'即可解决

		return ExtractTextPlugin.extract({
	        use: loaders,
	        publicPath:'../../',
	        fallback: 'vue-style-loader'
	     })

#### 2.vue-cli3这么解决
新建一个vue.config.js文件，然后这么写
	    
	module.exports = {
	    publicPath: '',//用来修改打包之后的静态资源的引入地址   
	}

# VUEX
vuex用来储存全局变量，在任何位置都可以访问和改变

## 1.安装和引用vuex
* 1.安装VUEX	

		npm install vuex --save

* 2.在src里面新建一个store文件夹,里面新建一个index.js，用来书写vuex的代码
* 3.在index.js里面：
	
		import Vue from 'vue'
		import Vuex from 'vuex'
		
		Vue.use(Vuex)
		
		export default new Vuex.Store({
		  state: {
		    属性名：属性值，
		  },
		  mutations: {
		    setData(state,data){
		      state[data.key] = data.value;
		    },
		  },
		  actions: {
		  },
		  modules: {
		  }
		})




## 2.全局注册vuex

在main.js里面引入store，然后在vue里面全局注册

	import  store  from './store/index.js'
	new Vue({
	  el: '#app',
	  router,
	  store，
	}
		

## 3.vue组件获取和设置vuex的值

* 1.设置state的值：

	this.$store.commit('setData',{
        key:'属性名',value:属性值
    });

* 2.获取state的值，一般都写在computed里面：this.$store.state.属性名	

		computed：{
			变量(){
				return this.$store.state.属性名;
			 },
		}


# 将请求数据分离
#### 1.新建一个js文件
新建一个http.js文件，然后书写以下代码

	import Axios from 'axios';
	import qs from 'qs'
	var http = Axios.create({
	    baseURL: '自己的ip地址'，
	});
	
	export default {
	    get(url,params={}){
	       params = qs.stringify(params);
	       return http({
	           url,
	           params,
	           method:'get',
	       });
	   },
	   post(url,data={}){
	       data = qs.stringify(data);
	       return http({
	           url,
	           data,
	           method:'post',
	       });
	   }
	};


#### 2.在main.js中引用
	
	import http from '@/lib/http.js'
	Vue.prototype.http = http;


#### 3.在对应的地方直接使用

	this.http.get('url地址',{参数}).then(res=>{
        
    });


# 其他知识点
## 1.prop的另一种用法
可以将props写成一个json，属性名是我们接收的变量名，属性值接收的数据类型

* String  字符串
* Number   数值
* Boolean   布尔
* Function   函数
* Object	对象型
* Array		数组
 
		export default {
			props:{
				navs:Array,
				curIndex:Number,
				num:[String,Number],//表示该数据可以是两种数据类型
			}
		}

## 2.prop默认值写法

		export default {
			props:{
				curIndex:{
					type:Number,
					default:0,
				},
				isDisabled:{
					type:Boolean,
					default:true,
				},
			}
		}


## 3.修改没有暴露出来的标签的样式
两种做法：

* 1.写在全局css里面
* 2.在组件暴露出来的选择器  和 组件没有暴露出来的选择器 之间加上 >>> 
	
		例如：
		.car >>> .van-nav-bar__title{color:yellow;}


## 4.强制刷新数据
vue  属于 浅层次的监听，如果数据是基础类型，那么vue可以快速获取到数据改变，并且改变页面中的数据和样式，但是如果是引用型数据类型，的数据发生改变，可能会检测不到，所以这个时候需要强制刷新数
 
* this.$set(json名字,'key',value);
* this.$forceUpdate(); //最干脆的一个解决方法



## 5.forEach

array.forEach(function(item, index))

* item	必需。当前元素
* index	可选。当前元素的索引值

		  var arr = ['大乔','小乔','妲己','亚瑟','甄姬','后裔'];
		  arr.forEach(function(item,index){
		      console.log(item,index)
		  })


## 6...操作符
...操作符 表示可以穿不定数的参数

	function fn(...arg){
		console.log(arg);//arg的结果是个数组
	}
	fn(1);
	fn(2,3,4);
	fn(4,5,6);


## 7.vue.config.js

vue-cli3用来做一些配置

	const path = require('path')
	const chain = (config)=>{
	    config.resolve.alias
	    .set('@assets',path.join(__dirname,'./src/assets'))
	    .set('@comp',path.join(__dirname,'./src/components'))
	}
	    
	module.exports = {
	    publicPath: '',//用来修改打包之后的静态资源的引入地址
	    chainWebpack:chain,//用来修改开发环境sr根目录下的引入路径
	}

## 8.后台无法接受到post数据时解决方案

1.让后台修改代码

2.我们修改代码

安装	

	npm i qs 

引入	

	import qs from 'qs'

然后使用qs.stringify()将需要传递的数据转换一下格式即可

	qs.stringify(data);

## 9.@import 导入css时使用简写报错

	<style scoped>
		@import url('@css/login.css');//这么写报错，正确写法前面加~
		@import url('~@css/login.css');
	</style>

## 10.style里面使用@import引入的css文件是全局的

ue单页开发中，style上的scoped表示样式是局部作用域，只有当前页面起作用，可是如果内部有@import，引用外部文件的，那么引用的外部文件将是全局作用域。

这样的引用会导致其他页面的样式受到干扰，同时从js中利用import或者require引用的话也是全局的作用域，如果想引用一个局部作用域的css文件，用带有scoped的style去引用

	<style scoped src='@css/login.css'></style>

## 11.修改滚动条样式

	::-webkit-scrollbar {
		width: 2px; /*对垂直流动条有效*/
	}
	/*定义滚动条的轨道颜色、内阴影及圆角*/
	::-webkit-scrollbar-track{
		background-color: #fff;
	}
	
	
	/*定义滑块颜色、内阴影及圆角*/
	::-webkit-scrollbar-thumb{
		background-color: #ccc;
	}



## 12.element-ui表格数据过滤
scope.row 表示改行的数据

	<el-table-column   label="状态" align="center">
    	 <template slot-scope="scope">
           {{scope.row.status | statusToText}}
     	</template>
	</el-table-column>
	filters:{
        //0-未完成,1-已取消,2-已完成,3-已评价
        statusToText(value){
           var arr = ['未完成','已取消','已完成','已评价'];
           return arr[value];
        }
    }

## 13.el-table中给每一行数据加属性
通过table的属性row-class-name 实现

	<el-table :data="currentOrderLists"  :row-class-name="rowAddAttr">		
		<el-table-column label="操作"  align="center">
            <template slot-scope="scope">
                <i class="el-icon-circle-check" @click="completeTheItem(scope.row)"></i>
            </template>
        </el-table-column>
	</el-table>
	rowAddAttr(data){
		data.row.isClicked = true;
    }


## 14.github使用
* 1.从github下载代码：

	* git clone http地址

* 2.上传代码到github
 
	* git init
	* git add *
	* git commit -m "first commit"
	* git remote add origin http地址
	* git push -u origin master

* 3.更新代码

	* git pull
	
* 4.往上推代码
	
	* git push
