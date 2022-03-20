# 变量提升
## 变量提升与函数提升

### 变量声明提升
+ 通过 var 定义（声明）的函数，在定义语句之前可以访问到
+ 值：undefined
```javascript
var a = 3
function fn (){  // 变量提升
    console.log(a) // 先从内部查找 a
    var a = 4  // 相当于在函数内部第一行声明 var a，然后在此处赋值
}
fn()  // undefined
var b = 4
function fn1 (){
    console.log(b)
}
fn1()  // 4
```
### 函数声明提升
+ 通过 function 声明的函数，在之前就可以直接调用
+ 值：函数定义（对象）
```javascript
fn2()  // 4 可调用，函数提升
var b = 4
function fn2 (){
    console.log(b)
}
fn2()  // 4
fn3()  // 不能调用

var fn3 = function (){
    console.log('fn3')
}
```

### 变量提升和函数提升是如何产生的？