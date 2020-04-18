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


# webpack打包 #

## webpack安装
#### 1.安装node和npm
* 1.下载并且安装node
http://nodejs.cn/download/ 

* 2.安装完毕之后，摁电脑的“win+R”键，在输入框输入“cmd”，打开终端
	* 输入 node -v，如果正确输出版本号，则表明node安装正确
	* 输入 npm -v，如果正确输出版本号，则表明npm安装正确

#### 2.安装nrm
* 1.命令 ：npm install -g nrm 
* 2.命令：nrm ls  查看可选的源，带*的是当前使用的源
* 3.命令：nrm use taobao 可以切换下载源到taobao

#### 3.webpack安装
* 命令：npm install webpack@4.29.6  -g 

	输出 + webpack@4.29.6 ，继续下一步
* 命令：npm install webpack-cli@3.3.0  -g

	输出 + webpack@3.3.0，继续下一步
* 命令：webpack -v  ；查看版本号，版本号无误，那么webpack安装成功

## webpack构建vue项目
#### 1.新建项目文件 
在项目文件中新建

* dist 文件夹
* src 文件夹
	* main.js 
	* App.vue  
* static 文件夹
	* images 文件夹
* index.html
	* 书写`<div id="app"></div>`
* webpack.config.js

#### 2.修改webpack.config代码 

    const HtmlWebpackPlugin = require('html-webpack-plugin');
	const VueLoaderPlugin = require('vue-loader/lib/plugin');

	module.exports={
	    mode:'development',
	    entry:'./src/main.js',  
	    output:{ 
	       path : __dirname+'/dist',
	       filename:'build.js',  
	    },
	    plugins:[
 			new VueLoaderPlugin(),
	        new HtmlWebpackPlugin({
	            filename: 'index.html',
	            template: 'index.html',
	        }),
	    ],
	}


#### 3.生成package.json 

在项目根目录，打开黑窗口，输入 npm init 输入 package name：项目名字，其他的直接回车即可

#### 4.安装依赖
* 安装vue

	npm install vue  --save

* 安装vue-router
 	
	npm install vue-router --save

#### 5.npm安装loader
* 安装css loader:

	npm install css-loader style-loader --save-dev

*  安装less loader（可以不安装）
 
	npm install less less-loader style-loader css-loader --save-dev

*  安装vue loader
 
	npm install vue-loader vue-template-compiler  --save-dev

* 安装url-loader
	
	npm install url-loader -d

#### 6.webpack配置loader
在webpack.config.js文件里面，加入

     module:{
    	rules:[{ //css loaer
		    test:/\.css$/,
		    loader:'style-loader!css-loader'            
		 },{//less loader
       		test:/\.less$/,
        	loader:'style-loader!css-loader!less-loader'            
 		 },{//vue loader
       		test:/\.vue$/,          				
			loader:'vue-loader'           
		},{
        	test: /\.(woff2?|eot|ttf|otf)(\?.*)?$/,
        	loader: 'url-loader',
 		},
    ]},

#### 7.配置热刷新
* 1.安装
	* npm install webpack@4.29.6   -d
	* npm install  webpack-cli@3.3.0 -d
	* npm install webpack-dev-server html-webpack-plugin  -d

* 2.配置paskage.json里面的script
    
		"scripts": {
	    	"dev": "webpack-dev-server --inline --hot --open --port 3000"
	    },

#### 8.main.js中不能少的代码

	import Vue from 'vue';
	import App from './App.vue';
	import VueRouter from 'vue-router';
	import Login from './components/login.vue';

	Vue.use(VueRouter);

	const router = new VueRouter({
	    routes:[
		  	{
            	path:'/',
            	redirect:'/login'
        	},
			{
          		path:'/login',
          		component:Login
        	},
	    ],
	});
	new Vue({
	    el:'#app', 
	    router,
	    render (c){ 
	        return c(App);
	    },
	});

根据以上代码的配置：

* 不要忘记在index.html中书写id为app的div
* 主页面必须为App.vue

## 9.快速删除nde_modules的方法

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

## 2.路由
#### (1)vue-loader安装使用
vue-loader 是vue官方的路由管理器
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


#### (2)vue-link
* 1.使用router-link标签来替代之前 a标签
* 2.使用to属性来替代之前的href属性

		<router-link  to=””></router-link> 

注意：
* 1.router-link标签必须有to属性
* 2.to的属性值必须通过vuerouter配置过才可以成功跳转

#### (3)router-view
router-view标签就是一个占位符，路由配置让显示什么，他就显示什么。根据路由切换显示不同的内容

	<template>
	   <div> 
	        <router-link to="/login">登录</router-link>
	        <router-link to="/register">注册</router-link>
	        <router-view></router-view>
	   </div>
	</template>


#### (4)redirect重定向
 
	 {
	    path:'/',
	     redirect:'/login',
	 }, 
 
这段代码的含义是：
* 当浏览器加载根目录（首页）的时候，router-view自动显示到login组件
* 路径是'/'表示处于网站首页


# element-ui
## 1.安装和引用
* 1.安装命令	npm i element-ui -s
* 2.引用:element-ui是依赖vue的，所以必须先引入vue，在引入element-ui,需要单独引入css文件

		import Vue from 'vue';
		import ElementUI from 'element-ui'
		import 'element-ui/lib/theme-chalk/index.css';
		Vue.use(ElementUI)

## 2.常用组件介绍
#### 1.el-button按钮

	  <el-button>默认按钮</el-button>
	  <el-button type="primary">主要按钮</el-button>
	  <el-button type="success">成功按钮</el-button>
	  <el-button type="info">信息按钮</el-button>
	  <el-button type="warning">警告按钮</el-button>
	  <el-button type="danger">危险按钮</el-button>

#### 2.Message 消息框

	this.$message({
	    message:'提示内容',
	    type:'success,warning,info,error',
	    duration:'显示时间，设置为0则不小时，单位毫秒',
	    showClose:'是否显示关闭按钮，默认false',
	    center:'文字是否居中，默认false',
	    onClose:'fn,点击关闭按钮时触发的方法'
	});

#### 3.MessageBox 弹框

	<el-button type="text" @click="open">打开对话框</el-button>
	open() {
	    this.$alert('对话框的内容', '对话框的标题', {
	        confirmButtonText: '确定',
	        callback: action => {
	        //点击确定或者关闭之后的回调函数，可以省略
	        }
	    })
	},

#### 4.确认消息

	<el-button type="text" @click="open">打开对话框</el-button>
	open() {
	    this.$confirm('此操作将永久删除该文件, 是否继续?', '提示', {
	       confirmButtonText: '确定',
	        cancelButtonText: '取消',
	        type: 'warning'
	    }).then(() => {
		//点击确定之后的回调事件，可以省略
	     }).catch(() => {
	         //点击取消之后的回调事件，可以省略
	    });      
	},


## 5.Notification 通知

	 <el-button type="text" @click="open">打开对话框</el-button>
	 open() {
	    this.$notify({
	        title: '提示', 
	        message: '这是一条不会自动关闭的消息',
	        duration: 1200,//通知框显示时间
	        type: 'success'
	    });
	},

## 6.走马灯/轮播图

	<div class="bannerwrap">
	    <el-carousel trigger="click" height="轮播图的高度">
	        <el-carousel-item v-for="item in bannerArr" :key="item">
	        <img :src="'/static/images/'+item" alt="">
	        </el-carousel-item>
	    </el-carousel>
	</div>
	.bannerwrap{width:轮播图的宽度；}


## 7.InputNumber 计数器

	<el-input-number 
	    v-model="num" //绑定值
	    :min="1"   //设置计数器允许的最小值
		:max="10" //设置计数器允许的最大值
	></el-input-number>
	data(){
		return {
			num:1,
		}
	}


## 8.评分
* 1.评分：

		<el-rate   v-model="score"  show-text>  </el-rate>

* 2.如果只是想要显示分数，并不想要用户修改，只需要加一个disabled属性即可

		<el-rate  v-model="score"  show-score  disabled>  </el-rate>


## 9.tab标签页

	<el-tabs v-model="activeName">
	    <el-tab-pane label="用户管理"  name="first">用户管理</el-tab-pane>
	    <el-tab-pane label="配置管理" name="second">配置管理</el-tab-pane>
	</el-tabs>

* v-model  选中选项卡的 name
* label 选项卡标题

## 10.分页

	<el-pagination
	    :current-page="2" //当前处于第几页
	    :page-sizes="[10, 20, 50, 100]" //每页显示个数,选择列表
	    :page-size="20" //当前每页显示多少条，只能是page-sizes里面的某一项
	    layout="total, sizes, prev, pager, next, jumper"
	    :total="400"//总共多少条数据
	    @size-change="handleSizeChange"//pageSize 改变时会触发
	    @current-change="handleCurrentChange"//currentPage 改变时会触发
	></el-pagination>


## 11.icon图标
直接在想要设置突变的地方设置类名为 el-icon-iconName 来使用即可

	<i class="el-icon-edit"></i>
	<el-button type="primary" icon="el-icon-search">搜索</el-button>


## 12.导航菜单
* 1、el-menu  是导航菜单的总标签
* 2、el-menu-item表示每一项菜单，可以有多个
* 3、菜单可以通过属性来设置为横向菜单或者竖向菜单

#### 普通导航菜单

	<el-menu
	    default-active="2" //当前激活菜单的 index
	    mode="vertical"//菜单模式，取值：horizontal / vertical，默认vertical
	    background-color="#545c64"//菜单的背景色，仅支持16进制写法
	    text-color="#fff"//菜单的文字颜色，仅支持16进制写法
	    active-text-color="#ffd04b" //当前激活菜单的文字颜色，仅支持16进制写法>
	    <el-menu-item //每一项菜单
	    index="1" //当前菜单的索引值>
	        <i class="el-icon-menu"></i>  <span slot="title">导航一</span>
	    </el-menu-item>
	</el-menu>


#### 包含子菜单的导航菜单

	 <el-menu>
	    <el-submenu index="1"> 如果主菜单有子菜单的话，需要使用el-submenu标签
	        <template slot="title">导航一</template> 主菜单的标题内容
	        <el-menu-item index="1-1">选项1</el-menu-item>子菜单的每一项
	        <el-menu-item index="1-2">选项2</el-menu-item>
	        <el-menu-item index="1-3">选项3</el-menu-item>
	        //index="1-1" 第一个数字是父菜单的index值，第二个数字自己的索引值
	    </el-submenu>
	    <el-menu-item index="2">导航二 </el-menu-item>         
	 </el-menu>


## 13.form表单
#### Checkbox 多选框
v-model属性值：数组，选中的每一项的label属性值 

	<el-checkbox-group  v-model="checkList">  
	    <el-checkbox label="复选框 A"></el-checkbox>
	    <el-checkbox label="复选框 B"></el-checkbox>
	    <el-checkbox label="复选框 C"></el-checkbox>
	</el-checkbox-group>
	data(){
	    return(){
	        checkList:['复选框 A'],
	    }
	},


#### Select 选择器
v-model ：当前选中的那一项的value值

	<el-select v-model="currentSelect" placeholder="请选择">
	    <el-option value="中国"> </el-option>
	    <el-option value="美国"> </el-option>
	    <el-option value="俄罗斯"> </el-option>
	</el-select>
	data(){
	    return(){
	        currentSelect:'中国',
	    }
	},


#### Switch 开关

	<el-switch
	    v-model="isAnonymous"  当前是打开还是关闭，true/false
	    active-color="#13ce66"  打开时的背景色
	    inactive-color="#ccc" 关闭时的背景色
	    active-text="公开" 打开时的值
	    inactive-text="匿名" 关闭时的值>
	</el-switch>
	data(){
	    return(){
	        isAnonymous:'true
	    }
	},

## 14.upload上传

#### 1.属性
* action	必选参数，上传的地址,ip/yima/element/upload.php
* multiple 是否支持多选文件，默认false
* show-file-list	是否显示已上传文件列表，默认true
* drag	是否启用拖拽上传，默认false
* list-type	文件列表的类型，取值有text，picture，picture-card
* :limit='2'  最大允许上传个数，数值型
* :on-exceed='fn'	文件超出个数限制时触发的函数

		
		<el-upload
			:action="必选参数，上传的地址"
			multiple drag>
			    <el-button>上传</el-button>
		</el-upload>

#### 2.钩子函数
* :on-success  文件上传成功时的钩子,参数是response,file，fileList
* :on-error  文件上传失败时的钩子，参数是err, file, fileList
* :before-upload：往上传文件之前的钩子，参数为file，可以在这个阶段判断文件的大小和格式是否满足要求，如果不满足要求，我们return false，就可以终止图片上传
	* file.size  上传的文件大小，单位是B
	* file.type 上传的文件类型


			<el-upload
	            action='http://192.168.0.116/yima/element/upload.php'
	            multiple
	            :limit='3'
	            drag
	            list-type="picture-card"
	            :on-exceed='multipleErrFn'
	            :on-success="uploadSuccess"
	            :on-error="uploadError"
	            :before-upload="uploadBeforeFn"
            	><el-button type="primary">点击上传</el-button>
        	</el-upload>
			multipleErrFn(){
                this.$message({
                    message:'最多上传3张图片',
                    type:'error',
                })
            },
            uploadBeforeFn(file){
                console.log(file)
                console.log(this.maxSize)
                let isSizeok = file.size < this.maxSize;
                let isImg = file.type == 'image/jpeg' || file.type=='image/png';
                if(isSizeok && isImg){
                    return true;
                }else{
                    this.$message({
                        message:'图片不能超过2M',
                        type:'error',
                    })
                    return false;
                }
            },
            uploadSuccess(response,file,filelist){
                console.log(response)
                if(response.status==1){
                    this.$message({
                        message:'上传成功',
                        type:'success',
                    })
                }else{
                    this.$message({
                        message:response.message,
                        type:'error',
                    })
                }
               
            },
            uploadError(){
                this.$message({
                    message:'上传失败',
                    type:'error',
                })
            },


##  15.日期选择器
format：yyyy-MM-dd 或者 yyyy年MM月dd日

注意：MM是大写的

	<el-date-picker
	 v-model="绑定值"
	 type="year|month|date"
	 format="显示在输入框中的格式"
	 value-format="最好和format保持一致"
	 placeholder="选择日期">
	</el-date-picker>



##  16.form表单
#### 表单标签
* el-form标签表示form表单
* :model   表单的数据对象
* label-width：px  每一项描述文字label的宽度
* el-form-item表示表单的每一项
* label属性表示该项的描述文字

		<el-form  :model="ruleForm" label-width="80px">
			<el-form-item  label="描述文字"> 
			    <el-input v-model="ruleForm.name"></el-input>	
		    </el-form-item>
		</el-form>


#### 表单验证
Form 组件提供了表单验证的功能，步骤：
* 1.给 form-Item 标签增加 prop 属性，属性值为需校验的字段名即可。
* 2.给el-form标签增加 rules 属性，属性值为规则，例如v-bind:rules=”rules”
* 3.给data(){}增加 rules 属性，属性值为{}，传入约定的验证规则

#### rules验证关键字
* required：此项不能为空
* message：不满足要求是的错误提示文字
* trigger：什么时候有错误提示，blur|change
* min：最少几个字符
* max：最多几个字符
* type：该项的数据类型， array | date | number

#### rules验证规则
* 1.一条规则：json即可      变量名字：{  }

		name: { required: true, message: '请输入活动名称', trigger: 'blur' },

* 2.多条规则：数组即可,	变量名字：[{ }，{ }]

		salary:[
		    {type:'number',message: '只能是数字', trigger: 'blur'},
		    { required: true, message: '请输入活动名称', trigger: 'blur' },
		],

## 5.数字验证规则
* 1.在v-model后面加个number，即 v-model.number
* 2.在rules规则里面，规则type：“number”

		<el-input v-model.number="ruleForm.salary"></el-input> 
		{type:'number',message: '只能是数字', trigger: 'blur'},


# vue-cli脚手架

* 1.vue-cli就是vue的脚手架，用来一键生成vue+webpack的项目模板，包括vue-router，vue-loader等各种必须的依赖库，免去你手动安装各种插件的麻烦
* 2.以后我们开发vue项目，都是用这一套脚手架即可

## 1.安装：
* 1.安装脚手架：	npm install  vue-cli  -g
* 2.查看是否安装成功：  vue --version 如果正确输出版本号表示成功
    
## 2.使用vue-cli创建项目
创建项目 	

	vue init webpack 项目名字

* Project name：项目名称，默认 回车 即可
* Project description：项目描述，默认 回车 即可
* vAuthor：项目作者，默认 回车 即可
* Install vue-router：是否安装 vue-router，默认 回车 即可
* Use ESLint to lint your code：是否使用 ESLint 做代码检查，选择 n 不安装Set up unit * tests：单元测试相关，选择 n 不安装
* Setup e2e tests with Nightwatch：单元测试相关，选择 n 不安装

## 3.运行  
* 在终端运行npm  run dev
* 在浏览器输入localhost:8080，就可以看到画面

## 4.安装和引入element-ui
* 1.安装命令	
	
		npm i element-ui -s
* 2.引用 

		import Vue from 'vue';
		import ElementUI from 'element-ui'
		import 'element-ui/lib/theme-chalk/index.css';
		Vue.use(ElementUI)


## 5.使用npm安装axios
* 1.安装

		npm install axios

* 2.在main.js里面

		import Axios from 'axios'
		Vue.prototype.axios = Axios;

* 3.使用：只需要 this.axios.post() 或者  this.axios.get()即可

## 6.配置proxy
配置proxy可以解决跨域问题  
步骤：

* 1.打开build文件夹里面的webpack.dev.conf.js文件
* 2.在devServer属性里面添加：

		proxy: {
		      "/api": {
		        target: "http://ip地址:80",
		        pathRewrite: {"^/api" : ""}
		      }
		},

然后，重启服务器

	proxy: {
      "/hairShop": {
        target: "http://localhost:80",
        pathRewrite: {"^/hairShop" : "/hairShop"}//使用'/hairShop' 替代 'http://localhost:80/hairShop'
      },
	"/api": {
        target: "http://localhost:80",
        pathRewrite: {"^/api" : "/api"}//使用'/api' 替代 'http://localhost:80/api'
      },
	},


# VUEX
vuex用来储存全局变量，在任何位置都可以访问和改变

## 1.安装和引用vuex
* 1.安装VUEX	

		npm install vuex --save
* 2.在src里面新建一个store文件夹,里面新建一个index.js，用来书写vuex的代码
* 3.在index.js里面：
	
		import Vue from 'vue' 	
		import Vuex from 'vuex'	Vue.use(Vuex);
		const store= new Vuex.Store({
		    state:{//数据
		    
			},
		    getters:{ //可以让组件通过这里的方法来获取到state的数据
		    
			},
		    mutations:{ //这里的方法修改state的数据
		    
			},
		    actions:{
		        //可以让vue组件传递需要更改的数据给这里的方法，
		        //然后这里在把数据提交给mutations,
		        //mutations在更改state
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

## 3.代码例子
 
	export default new Vuex.Store({
	    state:{
	        username:'11',
	    },
	    getters:{ 
	        getUsername(state){
	            console.log(state.username);
	            return state.username;
	        }
	    },
	    mutations:{ //这里的方法修改state的数据
	        setUsername(state,data){
	            state.username = data;
	        },
	    },
	    actions:{    //可以让vue组件传递需要更改的数据给这里的方法，
	        	//然后这里在把数据提交给mutations,
	            //mutations在更改state
	        setUsername(context,data){
	            context.commit('setUsername',data);
	        },
	    }
	})

## 4.vue组件获取和设置vuex的值

* 1.设置state的值：

	this.$store.dispatch('actions里面对应的方法',值)
		
		this.$store.dispatch('setTitle','学习vuex');

* 2.获取state的值，一般都写在computed里面：

	this.$store.getters.getters里面的方法

		computed：{
			变量(){
				var title = this.$store.getters.getTitle;
			 },
		}

# 项目知识点
## 1.在方法里面跳转路由
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

## 2.路由嵌套
router-view加载的组件里面，还有一个router-view标签，这种关系就形成一种路由嵌套关系

在子路由里面通过chidren来配置子路由

	 {
	      path: '/home',  //主路由路径
	      component: Home, //主路由加载的组件
	      redirect:'/order',//将router-view默认显示order
	      children:[ //子路由集合
	        {
	          path: '/order', //子路由路径
	          component: Order //子路由组件
	        },
	     ]
	 }