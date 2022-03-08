# 原型与原型链
+ 函数的 prototype 属性
>+ 每个函数都有一个 prototype 属性，默认指向一个 object 空对象
>+ 原型对象中有一个属性 constructor，指向函数对象
+ 给原型对象添加属性（一般是方法），实例对象可以访问
>+ 作用：函数的所有实例对象，自动拥有原型中的属性（方法） 
```javascript
console.log(Date.prototype, typeof Date.prototype)

console.log(Date.prototype.constructor === Date) // 原型对象中有一个属性 constructor，指向函数对象
function fun () {

}

console.log(fun.prototype)  // 默认指向一个空的 Object 空对象
console.log(fun.prototype.constructor === test)
fun.prototype.test = function() { // 给原型对象添加方法
    console.log('test')
}
``` 