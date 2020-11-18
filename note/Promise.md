### Promise

1. 一种异步编程方式

2. ES6封装的一个类

3. 可以解决回调地狱的问题

4. 使用方法

   new ->构造函数(1.保存了一些状态信息  2.执行传入的函数)

   ~~~js
   new promise((resolve,reject)=>{
       //第一次执行的代码
       setTimeout((data)=>{
           //成功的时候，调用resolve方法,执行then
          // resolve(data)
           
           //失败的时候调用reject方法，执行catch
           reject('error')
       },1000)
   }).then((data)=>{
       return new Promise((resolve,reject)=>{
           //第二次执行的代码
       })
   }).then(()=>{
           
       })
   }).then(()=>{
           
       })
   }).catch((err)=>{
       console.log(err)
   })
   ~~~

5. promise的使用情况
   - 一般情况下有异步操作时，使用Promise对这个异步操作进行封装

6. Promise的三种状态
   - pending：等待状态，比如正在进行网络请求，或者定时器没有到时间
   - fulfill：满足状态，当我们主动调用了resolve时，就处于该状态，并且会回调.then()方法
   - reject：拒绝状态，当我们主动调用了reject时，就处于该状态，并且会调用.catch()方法

7. Promise的all方法使用

   ~~~js
   Promise.all([
       new Promise((resolve,reject)=>{
           $ajax({
               url:"url1",
               success:function(data){
                   resolve(data)
               }
           })
       }),
       new Promise((resolve,reject)=>{
           $ajax({
               url:'url2',
               success:function(data){
                   resolve(data)
               }
           })
       })
   ]).then(results=>{
       results[0]
       results[1]
   })
   ~~~

   