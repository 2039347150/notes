模块化管理

import、export

导出

1. 声明赋值的同时导出

   > //导出变量
   >
   > export var firstName = '三';
   >
   > export var lastName = '张';
   >
   > //导出函数
   >
   > export function sayLoveMe() {
   >
   >   console.log('I love you!!');
   >
   > }

   

2. 声明赋值之后导出

> var sex = '男';
>
> var age = 18;
>
> export { sex, age };
>
> //设置别名导出
>
> export {sex as gender}
>
> //导出默认值，默认值只能设置一个
>
> export default '启用';
>
> //导出函数
>
> function sayLoveMe100Times() {
>
>   console.log('I love you * 100');
>
> }
>
> export { sayLoveMe100Times }

3. 运行

> node --experimental-modules 运行的文件名

导入

> import { firstName, lastName } from './m1.mjs';