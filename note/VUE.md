###  什么是VUE 

vue是一种渐进式的JavaScript框架

特点：易用、灵活、高效

------

### 面向对象

> - 面向对象是一父3种编程思想，通过把事物对象化
>
> - MVC编程思想：m：model 模型、v：view 视图、c：control 控制层
>
> - MVVM编程：m：model、v：view、vm：viewModel 视图模型（数据视图的响应式）

#### 面向对象的编程语言

	> JAVA、C++
	> JavaScript变向地实现面向对象

#### 面向对象编程语言的四大特征

> 抽象：把现实世界中的事物抽象成类
>
> 封装：（将对象的属性和方法封装成一个类）把需要封装的属性私有化，分别生成get、set方法，get方法用来读			 取属性、set方法用来设置属性
>
> 继承：子类继承父类的属性和方法
>
> 多态：子类可以重写父类的方法，有不同的行为方式

构造函数：在对象实例化时自动执行的一个特殊函数

#### 应用场景

------

jquery（一个轻量级的JS库）思想

1. 通过选择器选择元素
2. 操作元素（DOM操作，样式修改，事件绑定）

------

### VUE语法

#### 环境的配置

浏览器中使用vue：

- 导入vue的js文件：https://cdn.jsdelivr.net/npm/vue/dist/vue.js
- 通过npm下载vue文件：npm install vue

#### 模板语法

1. 插值：`<span>{{变量名}}</span>`

2. 显示文本：`<span v-text="变量名"></span>`

3. 显示html：`<span v-html="<a href="javascript:;">我是一个超链接</a>"></span>`

4. 绑定事件：①@事件名称 ②v-on:事件名称

5. 修改标签属性：①v-bind:属性名=‘表达式' ② :属性名='表达式' 

6. 特殊指令：

   - v-once：只渲染一次

   - v-pre：浏览器解析引擎遇到vue的插值符号时会自动解析，v-pre输出不被解析的纯文本

     `<span v-pre>{{msg}}</span>` //如果data中有msg，浏览器不会解析，直接输出{{msg}}

7. 条件渲染：v-if、v-else-if、v-else

8. 表单绑定：v-model

### VUE交互

#### 鼠标事件

#### 键盘事件

> 键盘事件：①@keydown.enter ②@keydown.37

#### 属性监听

~~~JS
    var app = new Vue({
            el: "#app",
            data: {
                index: 0
            },
            watch: {
                //当监听的值发生变化 时 ，该方法会被执行
                index: function(val) {
                    if (val > 2) {
                        this.index = 0;
                    }
                }
            },
            methods: {}
        })
~~~

#### 计算属性

> 只有当计算属性函数中用到的变量发生变化时，才会触发属性重新计算，其他情况都不变

~~~js
methods: {
            randomMsg() {
                return this.msg + Math.random();
            }
          },
 computed: {
                 rdmMsg: function() {
                     return this.msg + Math.random();
                 }
            }
~~~

#### 生命周期

什么是生命周期

> vue每个组件都是独立的，每个组件都有一个属于它的生命周期，从一个组件创建、数据初始化、挂载、更新、销毁，这就是一个组件所谓的生命周期。

vue组件生命周期

> 1. 初始化阶段
> 2. 渲染挂载阶段
> 3. 监听更新阶段
> 4. 销毁阶段
>
> 常用的生命周期方法：
>
> ​	mounted()：发送Ajax请求，启动定时器等异步任务
>
> ​	beforeMounted()：做收尾工作，如：清除定时器

生命周期图解：

<img src="file://E:/Desktop/%E4%B8%8A%E8%AF%BE%E7%AC%94%E8%AE%B0/vue-demo/readme.assets/clipboard.png?lastModify=1599221802" alt="img" style="zoom:33%;" />

~~~js
 el: "#app",
 data: {
        msg: 'Hello Vue',
        count: 0
 },
beforeCreate() {
    debugger
    console.log("vue初始data和方法之前被调用")
    console.log(this.count,this.foo); //undefined,undefined
},
created() {
    console.log("vue初始data和方法之后被调用")
    console.log(this.count,this.foo); //0 "Hello Vue"
},
beforeMount() {
	console.log('渲染模板挂载el节点之前');
},
mounted() {
	console.log('渲染模板挂载el节点之后');
},
beforeUpdate() {
	console.log('页面数据发生变化更新dom之前')
},
updated() {
	console.log('页面数据发生变化更新dom之后')
},
beforeDestroy() {
	console.log('vue实例被销毁之前');
},
destroyed() 
	console.log('bye bye!!');
}

~~~



### VUE样式

#### 绑定style修改样式

> 例：<input type="text" :style='{color:"red",textAlign:"center"}'>

#### 绑定class修改样式

> 例：...  .active{color:red};  ...
>
> ​		<input type="text" :class="active">

### VUE动画

入场动画：.v-enter、.v-enter-active、.v-enter-to

出场动画：.v-leave、.v-leave-active、.v-leave-to

~~~css
.v-enter {
    left: 10%;
}        
.v-enter-active {
    transition: all 1s;
}        
.v-enter-to {
    left: 50%;
}        
.v-leave {
    left: 50%;
}        
.v-leave-active {
    transition: all 2s;
}
.v-leave-to {
    left: 90%;
}
~~~



### VUE组件

#### 注册组件的步骤

> 1.创建组件构造器
>
> 2.注册组件
>
> 3.使用组件



#### 全局组件定义

~~~js
Vue.component('CountButton',{
            template:"<button @click='count++'>点击了按钮{{count}}次</button>",
            data:function(){
                return {
                    count:0
                }
            }
        })
~~~

注意事项

1. data必须返回的是一个函数

2. template可以是字符串，也可以

   `<script type='text/x-template'></script>`

3. 组件的名称可以采用横线分隔也可以驼峰式名称（浏览器上使用时有大小写的问题）

#### prop参数

> 父容器给子组件传送参数，通过prop传送

~~~js
 <script type="text/x-template" id="myBtn">
        <button v-if='lang=="zh"' @click="count++">click {{count}} times</button>
        <button v-else='lang=="en"' @click="count++">点击了按钮 {{count}} times</button>
 </script>
 <div id="app">
        <count-btn lang="en"></count-btn>
        <count-btn lang="zh"></count-btn>
        <count-btn :lang="currentLang"></count-btn>
        <button @click='currentLang=currentLang=="en"?"zh":"en"'>切换语言</button>
 </div>
 <script>
        Vue.component("CountBtn", {
            template: '#myBtn',
            data: function() {
                return {
                    count: 0
                }
            },
            props: ['lang']
        })
        var app = new Vue({
            el: "#app",
            data: {
                currentLang: 'en'
            },
            methods: {

            }
        })
 </script>
~~~

#### 监听事件

> 子组件给父容器传送参数，通过$emit()传送
>
> 有利于降低父子组件的耦合度

~~~js
<script type="text/x-template" id="countBtn">
        <button @click="countAdd">点击了{{count}}次</button>
        <!-- <button @click="count++">点击了{{count}}次</button> -->
</script>
<div id="app">
        <p>点击次数总和为：{{sum}}</p>
        <count-button @count-change="sum++"></count-button>
        <count-button @count-change="sum++"></count-button>
        <count-button @count-change="sum++"></count-button>
</div>
<script>
        Vue.component("CountButton", {
            template: "#countBtn",
            data: function() {
                return {
                    count: 0
                }
            },
            methods: {
                countAdd: function() {
                    this.count++;
                    // 向父容器抛送一个事件
                    this.$emit('count-change');
                }
            }
        })
        var app = new Vue({
            el: "#app",
            data: {
                sum: 0
            },
            methods: {
            }
        })
</script>
~~~

#### 在自定义组件（标签）上使用标签

> <input type="text" :value="currentValue" @input="currentValue=$event.target.value">

#### 动态组件

> 在一个节点上动态加载不同的组件         

##### 全部组件

~~~js
 // 全局组件
 Vue.component('button2', {
     template: '#myBtn'
 })
~~~

##### 局部组件

~~~ js
  	<button3></button3>
 	<button4></button4>

	var app = new Vue({
            el: "#app",
            data: {},
            methods: {},
            // 局部组件，只在app实例里面有效
            components: {
                // botton3是组件名
                "button3": {
                    template: "<span>span按钮</span>",
                    props: ["msg", "count"]
                },
                "button4": {
                    template: "<button>button组件</button>",
                }
            }
        })
~~~

##### props声明方式

~~~js
Vue.component("组件",{
    //常见用法
    props:["属性1","属性2"]
})
//更严谨的声明方式
Vue.component("组件",{
    props:{
        id:Number,
        sex:[String,Number],
        username:{
           	type:String,
            required:true
        },
        sal:{
            type:Number,
            default:1000
        }
        intro:{
        	type:Object,
        	default:function(){
   	 			return {message:"hi!"}
			}
    	}
		status:{
            validator:function(){
                return ['success','fail','error']
            }
        }
    }
})
~~~

##### vue单文件组件

1. 全局定义--组件名称不能重复
2. 字符串模板--没有代码提示，script
3. 不支持css
4. 没有构建过程（不能使用预处理技术babel[把es6版本转换成es5]，less）

##### *.vue文件

~~~js
<template></template>
<script>
    //交互
</script>
<style scoped>
	//样式，scoped表示该样式只作用于该组件
</style>
~~~

##### 安装vue-cli工具

~~~nginx
//安装命令行工具
npm install -g @vue/cli
//测试是否安装成功
vue -v
//创建项目
vue create 项目名
vue create ./  将当前项目作为要创建的项目
//
vue install -g @vue/cli-service-global
//运行项目
npm run serve
//测试组件
vue serve 要测试的组件目录
~~~

##### 通过vue-cli创建vue项目

> //1.全局安装vue-cli运行环境
>
> npm install -g vue-cli
>
> //2.初始化webpack打包工具
>
> vue init webpack vue_demo
>
> //3.定位到创建的项目
>
> cd  vue_demo
>
> //4.安装项目依赖
>
> npm install
>
> //5.运行项目
>
> npm run dev

模板项目的结构

> --build:webpack：相关的配置
>
> --dev-server.js：通过express启动后台服务器
>
> --config：webpack 相关的配置文件夹（基本不需要修改）
>
> --index.js：指定的后台服务的端口号和静态资源文件夹

组件：

> 一个局部的功能模块

#### 组件间通信

1. props

   父子组件间通信的基本方式

   属性值的两大类型：

   ​	一般：父组件-->子组件

   ​	函数：子组件-->父组件

   隔层组件间传递：必须逐层传递（麻烦）

   兄弟组件间传递：必须借助父组件（麻烦）

2. vue自定义事件

   - 子组件与父组件的通信方式，用来取代function props


   - 不适合隔层组件和兄弟组件间的通信

   - 父组件可以在使用子组件的地方直接用v-on来监听子组件触发的事件。即父组件中使用v-on绑定自定义事件，然后再子组件中使用$emit(eventName,data)触发事件。

3. 消息订阅与发布(PubSubJS库)

   适合任意关系的组件间通信

   安装：npm install --save pubsub-js

   订阅消息 PubSub.subscribe('msg',function(msg,data){})

   发布消息：PubSub.publish('msg',data)

   使用：

   ~~~vue
   父组件：
   import PubSub from 'pubsub-js'
   PubSub.subscribe('deleteTodo',(msg,index)=>{//msg必须要写
       this.deleteTodo(index)
   })
   子组件：
   import  PubSub from 'pubsub-js'
   PubSub.publish('deleteTodo');
   ~~~

   

4. slot插槽

   用于父组件向子组件传递标签数据

   ~~~html
   子组件：
   <template>
   	  <div>
          	  <slot name="xxx">不确定的标签结构</slot>
             <div>
                 组件确定的标签结构
             </div>
             <slot name="yyy">不确定的标签结构</slot>
          </div>  
   </template>
   父组件：
   <template>
   	<child>
       	<div slot="xxx">
               xxx对应的标签结构
           </div>
           <div slot="yyy">
               yy对应的标签结构
           </div>
    </child>
   </template>
   ~~~

5. 兄弟间通信：vuex

   

------

### vue-ajax

#### vue项目中常用的2个ajax库

1. vue-resource：vue插件，非官方库，vue1.x使用广泛

   > npm install vue-resource --save 

   

   ~~~
   //引入模板
   import VueResource fom "vue-resource"
   //使用插件
   Vue.use(VueResource)
   
   //通过vue/组件对象发送ajax请求
   this.$http.get('/someUrl').then((response)=>{
   	console.log(response.data)//返回结果数据
   },(response)=>{
   	//error callback
   })
   ~~~

   

2. axios：通用的ajax请求库，官方推荐，vue2.x使用广泛

   > npm install axios --save

   

   ~~~ 
   //引入模板
   import Axios fom "axios"
   //使用插件
   Vue.use(Axios)
   
   //通过vue/组件对象发送ajax请求
   axios.get('/someUrl').then((response)=>{
   	console.log(response.data)//返回结果数据
   }).catch(error=>{
   	alert('请求错误')
   })
   ~~~

   

### vue UI组件库

1. 常用

   1)Mint UI：

   ​		a.主页：http://mint-ui.github.io/#!/zh-cn

   ​		b.说明：饿了么开源的基于vue的移动端ui组件库

   2)Element：

   ​		a.主页：http://element-cn.io/#/zh-CN

   ​		b.说明：饿了么开源的基于vue的PC端UI组件库

2. 安装

   > npm install 

### 前端渲染和后端渲染

1. 后端渲染：
2. 前端渲染：浏览器中显示的网页中的大部分内容，都是由前端写的js代码，在浏览器中执行，最终渲染出来的网页

### vue官方路由插件

#### 安装

>  vue install vue-router --save

#### 配置

1. ​	创建路由配置文件：src/router/index.js

   ~~~ vue
   import Home from '@/views/Home'
   //1.导入路由对象
   import VueRouter from 'vue-router'
   
   // 调用路由插件
   Vue.use(VueRouter)
   
   方法1：
   export default new Router({
       routes: [{
           path: '/',
           name: 'HelloWorld',
           component: HelloWorld
       }, {
           path: '/Home',
           name: 'Home',
           component: Home
       }]
   })
   方法2：
   routes: [{
           path: '/Home',
           name: 'Home',
           component: Home
   	}]
   
   // 创建路由对象
   const router = new VueRouter({
       mode: 'history',
       routes
   })
   
   // 导出路由对象
   export default router;
   ~~~

2. 修改src/main.js文件

   ~~~
   import router from './router'
   new Vue({
       el: '#app',
       router,
       components: { App },
       template: '<App/>'
   })
   ~~~

3. 配置页面的显示

   ~~~ 
   <router-view></router-view>
   ~~~

4. 跳转

   1. 标签跳转： 

      **path跳转**

      `App.vue页面：<router-link to="/about">About</router-link>` 

      `<router-link :*to*="{path:'/Home',query:{id:111,age:18}}">用户详情(通过path跳转)</router-link>`

      `<router-link :*to*="{name:'Home',query:{id:111,age:18}}">用户详情(通过path跳转)</router-link>`

      **修改样式**

      .router-link-exact-active*, .router-link-active*

      **传参**

      普通传参：/User?id=1

      RESTful传参：/User/101/22  /user/:id/:age

   2. js跳转

      this.$router.push()

      ~~~ 
      //字符串
      // this.$router.push("about");
      //对象
      // this.$router.push({path:'/user',query:{id:111,age:18}});
      // RESTfull
      console.log(this.$router);
      this.$router.push({name:'User2',params:{id:111,age:18}});
      //-1 后退一页 1向前切换
      // history.go()
      // this.$router.go(-1);
      ~~~



#### 嵌套路由

```
{
    path: '/home',
    name: 'Home',
    component: Home,
    children: [{
        path: '/home/news',
        component: News
        },
        {
        path: '/home/message',
        component: Message
        }, {
        path: '',
        redirect: '/home/news'
        }
    ]
}
```

#### router-link属性

~~~js
//to属性：用于指定跳转的路径
<router-link to="/home"></router-link>
//tag:可以指定<router-link>之后渲染成什么组件
<router-link tag="button"></router-link>
//replace:不会留下history记录
<router-link tag="button" replace></router-link>
//active-class,修改linkActiveClass可以通过router实例进行
const router=new VueRouter({
    routes,
    mode:history,
    linkActiveClass:'active'
})
~~~



#### 向路由组件传递数据

1. 路由路径携带参数（params/query）

   ~~~
   配置路由：
   {
       path: '/home/message',
       component: Message,
       children: [{
               path: '/home/message/detail/:id',
               component: MessageDetail
   	}]
    }
    参数携带：
     <router-link :to="`/home/message/detail/${message.id}`">{{message.title}}</router-link>
   ~~~

2. <router-view></router-view>属性携带数据

   `<router-view :msg="abc"></router-view>`

#### 缓存路由组件

1. 理解：
   - 默认情况下，被切换的路由组件对象会死亡释放，再次回来时是重新创建的
   - 如果可以缓存路由组件对象，可以提高用户体验

2. 编码实现

   `<keep-alive><router-view></router-view></keep-alive>`

#### 编程式路由导航

##### 相关API

1. this.$router.push(path)：相当于点击路由链接（可以返回到当前路由界面）
2. this.$router.replace(path)：用新路由替换当前路由（不可以返回到当前路由界面）
3. this.$router.back()：请求（返回）上一个记录路由
4. this.$router.go(-1)：请求（返回）上一个记录路由

#### 模拟数据接口

json-server：快速搭建RESTful风格的数据接口

> npm install -D json-server

编写xxx.json

~~~ json
{
 "user":[
     {id:1,username:'zs',sex:'男'}
     {id:1,username:'zs',sex:'男'}
 	 {id:1,username:'zs',sex:'男'}
 ]   
}
~~~

#### URL模式

- history
- hash
- abstract

#### 命名视图

> 在一个页面显示多个视图

~~~~js
//在index.js文件扩展路由
routes = [{
    // 后台布局路由
    path: '/backend',
    component: Admain, //后台主页
    children: [{
            path: 'list',
            component: UserList,
        },
        {
            path: 'edit',
            component: UserEdit
        },
        {
            path: 'add',
            component: UserAdd
        }
    ]
}]
~~~~

------

前后端分离项目登录功能实现

1. 当用户请求一个需要授权的页面
2. 输入用户名和密码进行验证，验证通过后台生成令牌
3. 前端获取令牌，把令牌保存到localStorage
4. 前端向后端发送异步请求获取需要授权的数据

vue中实现登陆需要用到

1. 路由元信息：
2. 路由守卫（类似vue的生命周期方法，类似后台路由拦截器）

### VUEX

> vue官方的一个插件，用来解决多个界面间的共享问题
>
> 针对Vue的应用程序实现的状态管理模式
>
> 采用集中式方式来管理多个组件中的状态
>
> 采用固定的流程规则来实现一种可预见的状态管理

#### 基本概念

1. 单组件中的状态管理模式

   ![image-20200913192608441](C:\Users\张灵灵\AppData\Roaming\Typora\typora-user-images\image-20200913192608441.png)

2. 多组件状态模式

   ![image-20200913192651891](C:\Users\张灵灵\AppData\Roaming\Typora\typora-user-images\image-20200913192651891.png)

#### vuex安装配置

安装：

~~~
npm install --save vuex
~~~

配置：

~~~
// src/store/index.js
import Vue from 'vue'
import Vuex from 'vuex'
//安装插件
Vue.use(Vuex)

//vuex配置文件
const store = new Vuex.store()

//src/main.js
import store from './store'
...
new Vue({
	...
	store
}).mouted("#app")
~~~

#### vuex状态管理应用包含的部分

1. state：多组件的数据仓库

2. getters：Vuex中的compute属性，多次访问可以优化性能

3. Mutations：Vuex中数据改变的唯一方式

   - mutation主要包括两部分：

     - 字符串的事件类型(type)
     - 一个回调函数(handler)，该回调函数的第一个参数就是state

   - mutation代码

     ~~~
     //1.通过commit普通提交
     `mutation:{increment(state,count){state.counter+=count}}`
     `addCount:function(){this.$store.commit('increment')}`
     //2.特殊的提交封装
     `mutation:{increment(state,payload){state.counter+=payload.count}}`
     `addCount:function(){this.$store.commit({type:'increment',count})}`
     ~~~

   - Mutation传递参数
     
     - 通过mutation更新数据携带的额外参数被称为是mutation的载荷(Payload)
   - mutation响应规则
     - 提前在store中初始化好所需要的属性
     - 当给state中的对象添加新属性时，使用下面的方法
       - 方法一：使用Vue.set(obj,'newProp','123')
       - 方法二：用新对象给旧对象重新赋值
   - mutation类型常量
     
     - 用来解决项目过大，事件名称过多以防写错的情况
   - Mutation同步函数
     - Mutation中的方法必须是同步方法，这样可以在使用devtools时，可以捕捉mutation的快照
     - Action类似于Mutation，用来代替Mutation进行异步操作

4. Actions：用于封装某些功能的业务逻辑，并且支持异步操作

   ~~~js
   const store=new Vuex.Store({
   	mutations: {
           changeX(state, val) {
               state.x = val;
           }
      },
      actions: {
           drag(context, data) {
               context.commit("changeX", data.x)
           }     
           // 封装一个异步方法
           aUpdate(context,payload){
               return new Promise((resolve,reject)=>{
                   setTimeout(()=>{
                       context.commit('changeX');
                       console.log(payload);
                       resolve('2333');
                   },1000)
               })
           }
       }
   })
   methods:{
   	update(){
   		this.$store.dispatch('aUpdate','我是携带的信息').then(res=>{
   console.log('里面完成了提交');
   console.log(res)
   })
   	}
   }
   
   ~~~

   

5. Modules：如果存储中心中需要保存海量状态信息时，可以使用模块来划分，实现数据的独立性

#### vuex的使用情况

> vuex可以用来开发大型单页应用，可以帮助管理共享状态

### 网络模块封装

1. Vue中发送网络请求的方式

   1)传统的Ajax是基于XMLHTTPRequest(XHR)

   -  易解释，但配置和调用方式非常混乱，实际开发很少直接使用

    2)jQuery-Ajax

   -  相对于传统的ajax好用，但是在Vue的网络请求中特意引用重量级框架jQuery没有必要

    3)vue-resource

   - 官方在Vue1.x的时候推出，体积相对于jQuery小很多，但在Vue2.0退出后，Vue作者就在GitHub的Issues中说明去掉了vue-resource，并不再更新，若继续使用则这对以后的项目开发和维护存在很大的隐患

    4)axios（作者推荐）

   - 功能特点
     - 在浏览器中发送XMLHTTPRequest请求
     - 在node.js中发送http请求
     - 支持Promise API
     - 拦截请求和响应
     - 转换请求和响应数据
   - 支持多种请求方式
     - axios(config) ->默认为get请求
     - axios.request(config)
     - axios.get(url[,config])
     - axios.delete(url[,config])
     - axios.head(url[,config])
     - axios.post(url[,data[,config]])
     - axios.put(url[,data[,config]])
     - axios.patch(url[,data[,config]])
   - 发送并发请求
     - axios.all([])返回结果是一个数组，使用axios.spread可将数组[res1,res2]展开为res1，res2

   ~~~js
   axios.all([axios.get('http://127.0.0.1:3000/users'),axios.get('http://127.0.0.1:8080',{params:{type:'sell',page:1}})]).then(axios.spread((res1,res2)=>{
       console.log(res1);
       console.log(res2)
   }))
   ~~~

   - 常见的配置选项
     - 请求地址：url:'/user'
     - 请求类型：method: 'get '
     - 请求根路径：baseURL: 'http://www.mt.com/api'
     - 请求前的数据处理：transformRequest:[function(data){}]
     - 请求后的数据处理：transformResponse:[function(data){}]
     - 自定义的请求头：headers:{'x-Requested-With':'XMLhttpRequest'}
     - URL查询对象：param:{id:12}
     - 查询对象序列化函数：paramsSerializer: function(params){ }
     - request body：data:{key: 'aa'}
     - 超时设置：timeout:1000
     - 跨域是否带token：withCredentials：false
     - 自定义处理请求：adapter：function(resolve,reject,config){}
     - 身份验证信息：auth:{uname:'',pwd:''}
     - 响应的数据格式json/blob/document/arrayuffer/text/stream->responseType:'json'

### vue-devtools安装

1. 官网下载vue-devtools

> 方法1：git clone https://github.com/vuejs/vue-devtools/tree/master
>
> 方法2：下载压缩文件再解压 	

2. 安装依赖包

> 1. 定位到：E:\Downloads\chrome插件\vue-devtools-master\shells\chrome
>
> 2. 命令行输入npm install下载依赖

3. 修改文件

   > 打开chrome下的manifest.json将“persistent”:false改为true

4. 编译代码

   > npm run build

5. 运行插件

   > 打开chrome浏览器的扩展程序，以开发者模式运行，添加vue-devtools-master\shells\chrome安装包



