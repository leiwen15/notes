# 闭包

```javascript
for(var i = 0, length = btns.length; i < length; i++) {
    var btn = btn[i]
    btn.onclick = function () {
        alert('第' + (i + 1) + '个')  // 第4个， 第4个， 第4个
    }
}
```
```javascript
for(var i = 0, length = btns.length; i < length; i++) {
    var btn = btn[i]
    btn.index = i
    btn.onclick = function () {
        alert('第' + (this.index + 1) + '个')  // 第1个， 第2个， 第3个
    }
}
```
```javascript
// 利用闭包
for(var i = 0, length = btns.length; i < length; i++) {
    (function(i) {
        var btn = btns[i]
        btn.onclick = function () {
            alert('第' + (i + 1) + '个')  // 第1个， 第2个， 第3个
        }
    }
    )(i)
}
```
## 如何产生闭包？
+ 当一个嵌套的内部（子）函数引用了嵌套的外部（父）函数的变量（函数）时，就产生了闭包
## 闭包到底是什么？
+ 使用chrome 浏览器查看
>+ 闭包是嵌套的内部函数（大部分人）
>+ 包含被引用变量（函数）的对象（极少数人）
>+ ps：闭包存在于嵌套的内部函数中
## 闭包产生的条件？
+ 函数嵌套
+ 内部函数引用了外部函数的数据（变量）
```javascript
function fn1 () {
    var a = 2  // 此时就产生了闭包
    var b = 'abc'
    function fn2 () {  // 执行函数定义，就会产生闭包
        console.log(a)
    }
}
fn1()  // 不需要调用内部函数，就可以产生闭包
```
```javascript
function fn1 () {
    var a = 2  // 还没产生闭包
    var b = 'abc'
    var fn2 = function () {  // 执行函数定义，就会产生闭包
        console.log(a)
    }
}
fn1()  // 不需要调用内部函数，就可以产生闭包
```
## 常用的闭包？
+ 将函数作为另一个函数的返回值
+ 将函数作为实参传递给另一个函数调用
>+ 产生了几个闭包？
```javascript
// 将函数作为另一个函数的返回值
function fn1 () {
    var a = 2  // 其实此时就已经产生闭包了，因为函数提升
    function fn2 () {  // 执行函数定义，就会产生闭包
        a ++
        console.log(a)
    }
    return fn2
}
var f = fn1()  // 产生了 1 个闭包
f() // 3
f() // 4
fn1() // 产生了第 2 个闭包， 与执行内部的 fn2  无关
```
```javascript
// 将函数作为实参传递给另一个函数调用
function showDelay (msg, time) {
    setTimeout(function () {
        alert(msg)
    }, time)
}
showDelay('hello', 2000)
```