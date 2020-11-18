1.点击vue-link报错![image-20200916161213855](C:\Users\张灵灵\AppData\Roaming\Typora\typora-user-images\image-20200916161213855.png)

解决方法：

在main.js文件添加以下代码

~~~
import Router from 'vue-router'
const originPush = Router.prototype.push
Router.prototype.push = function push(location) {
    return originPush.call(this, location).catch(err => err)
}
~~~

2.通过插槽、path跳转报错

![image-20200919112421452](C:\Users\张灵灵\AppData\Roaming\Typora\typora-user-images\image-20200919112421452.png)

App.vue页面path跳转代码

![image-20200919112548695](C:\Users\张灵灵\AppData\Roaming\Typora\typora-user-images\image-20200919112548695.png)

错误原因：不能给插槽绑定path跳转请求，将跳转请求设置在tab-bar-item上可以实现跳转

![image-20200919112723939](C:\Users\张灵灵\AppData\Roaming\Typora\typora-user-images\image-20200919112723939.png)

3. 使用vuex报错

   ![image-20200923150133811](C:\Users\张灵灵\AppData\Roaming\Typora\typora-user-images\image-20200923150133811.png)

造成错误原因是store小写，将Vuex.store({})的store改为Store即可