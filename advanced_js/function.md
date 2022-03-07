# 函数
## 1.什么是函数？
+ 实现特定功能的封装体
+ 只有函数是可以执行的，其他都是不可以执行的
## 2.为什么使用函数
+ 提高代码复用效率
+ 容易阅读
```javascript
function showInfo (age) {
    if(age < 18) {
        console.log('未成年')
    } else if(age > 60) {
        console.log('退休')
    } else {
        console.log('上班')
    }
}
showInfo(18)
showInfo(65)
```
## 3.如何定义函数
+ 函数声明
+ 
```javascript
function fn1 (age) {
    console.log('函数声明')
}

var fn2 = function () {
    console.log('函数表达式')
}
```
## 4.如何调用函数？
+ test() 直接调用
+ obj.test() 通过对象调用
+ new test() new调用
+ test.call/apply(obj) 相当于obj.test()，临时让test成为obj的方法进行调用
+ call和apply可以让一个函数成为指定任意对象的方法进行调用，其他语言做不到
 ```javascript
var obj = {}
function test () {
    this.x = 'hh'
}
test.call(obj)
console.log(obj.x) // 'hh'
```
## 5.什么是回调函数？
+ 回调函数的特点
>+ 你定义的
>+ 你没有调用
>+ 但最后它执行了
 ```javascript
setTimeout(function () {
    alert('hh')
}, 2000)
```
## 6.常见的回调函数？
+ dom事件回调函数
+ 定时器回调函数
+ ajax请求回调函数
+ 生命周期回调函数

## 7.IIFE 立即调用函数表达式
+ immediately-invoked function expression
```javascript
(function () {  // 匿名函数自调用
    console.log('hh')  // 此方法可以避免污染全局变量
})()
```
+ 作用
>+ 隐藏实现
>+ 不会污染外部的命名空间
```javascript
(function () {  
    var a = 1
    function test () {
        console.log(++a)
    }
    window.$ = function() {
        return {
            test: test
        }
    }
})()
$().test()
```