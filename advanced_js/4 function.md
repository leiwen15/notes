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
## 8. this 是什么？
+ 任何函数本质上都是通过某个对象来调用的，如果没有指定，就是window
+ 所有函数内部都有一个变量：this
+ 其值为调用该函数的当前对象
```javascript
function Persion(color) {
    console.log(this)
    this.color = color
    this.getColor = function () {
        console.log(this)
        return this.color
    }
    this.setColor = function () {
        console.log(this)
        this.color = color
    }
}
Persion('red') // this 是 window
var p = new Persion('yellow') // this 是 p
var obj = {}
p.setColor.call(obj, 'black') // this 是 obj
var test = p.setColor
test()  // this 是 window

function func1() {
    function func2() {
        console.log(this)
    }
    func2() // this 是 window
}
func1() // this 是 window
```
## 9. 如何确定this的值？
+ test(): window
+ p.test()： p
+ new test()：新创建的对象
+ p.call(obj)：obj