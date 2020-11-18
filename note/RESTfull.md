RESTfull

- rest(Representational State Transfer,表征性状态转移)指的是一组架构约束条件和规则，提供了一个新的架构设计思路，满足这些约束条件 和原则的应用程序或设计就是restfull。

- RESTfull是一种数据接口规范，RESTfull通过提供一套统一的接口为所有客户端提供web服务，实现前后端分离和全栈开发方式


RESTfull特点

1.每一个地址就是一个资源

```
/user 用户
/dept 部门
/emp  员工
```

2.采用不同的请求方式交互

```
get /user:id //获取数据	router.get('/:id',function(req,res){})
post /user //创建数据	router.post('/',function(req,res){})
put /user //修改数据	router.put('/',function(req,res){})
delete /user:id //删除数据  router.delete('/:id',function(req,res){})
```

POSTMAN：专门用来测试数据接口

axios：是一个基于promise的HTTP库，可以用在浏览器和node.js中

axios是通过promise实现对ajax技术的一种封装，就像jQuery实现ajax封装一样。

```
axios安装：npm install axios -D   //安装在开发环境
```



------

axios和ajax的区别：

- 共同点：都可以实现异步响应

- 区别：ajax技术实现了局部数据的刷新，axios实现了对ajax的封装，axios有的ajax都有，ajax有的axios不一定有，总结一句话就是axios是ajax，ajax不止axios

- 优缺点：

  ajax：

  ​	1、本身是针对MVC编程，不符合前端MVVM的浪潮

  ​	2、基于原生XHR开发，XHR本身的架构不清晰，已经有了fetch的替代方案，jquery整个项目太	大，单纯使用ajax却要引入整个jquery非常不合理（采取个性化打包方案又不能享受cdn服务）

  ​	3、ajax不支持浏览器的back按钮

  ​	4、安全问题ajax暴露了与服务器交互的细节

  ​	5、对搜索引擎的支持比较弱

  ​	6、破坏程序的异常机制

  ​	7、不容易调试

  axios：

  ​	1、从node.js创建http请求

  ​	2、支持Promise API

  ​	3、客户端防止CSRF（网站恶意利用）

  ​	4、提供了一些并发请求的接口

------

网页状态管理

cookie：存储在浏览器，以key=value形式存储，大小在4k左右，cookie默认不加密

session：存储在服务器，服务器关闭，session失效，大小没有限制，session默认加密(签名)

------

cookie-parser:

安装：npm install cookie-parser

配置：在app.vue文件添加 

```
var cookieParser=require('cookie-parser');
app.use(cookieParser());
```

------

session使用：

安装 ：npm install express-session --save

配置：配置一个拦截器

```
const session=require('express-session');
app.use(session({
    resave: false,
    secret: 'xxxx',
    saveUninitialized: true,
    cookie: {
        maxAge: 6000
    }
}))
```

获取session地址：

安装uuid模块：npm install  uuid

配置模块：

------

文件上传功能实现

安装模块：npm install express-fileupload

配置：

```javascript
var fileupload = require('express-fileupload');
app.use(fileupload({
    limits: {
        fileSize: 50 * 1024 * 1024
    }
}))
```
