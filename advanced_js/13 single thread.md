# js 是单线程执行的
## 如何证明 js 执行是单线程的？
+ setTimeout()的回调函数是在主线程中执行的
+ 定时器回调函数只有在运行栈中的代码全部执行完后，才有可能执行
## 为什么 js 要用单线程模式，而不用多线程模式？
+ js 使用单线程，与它的用途有关
+ 作为浏览器脚本语言，js的主要用途是与用户互动，以及操作DOM
+ 这决定了它只能是单线程，否则会带来很复杂的同步问题
## 代码的分类
+ 初始化代码
+ 回调代码
## js 引擎执行代码的基本流程
+ 先执行初始化代码：包含一些特别的代码
>+ 设置定时器
>+ 绑定监听
>+ 发送 ajax 请求
+ 后面会在某个时刻才会执行回调代码
```javascript
// 先执行初始化代码，再执行回调代码
// alert 之前
// alert 之后
// timeout 0
// timeout 111
// timeout 555
setTimeout(function(){
    console.log("timeout 555")
    alert("55555555")
}, 5000)

setTimeout(function(){
    console.log("timeout 111")
    alert("11111111")
}, 1000)

setTimeout(function(){
    console.log("timeout 0")
    alert("00000000")
}, 0)

function fn() {
    console.log("fn()")
}

console.log("alert 之前")
alert("dddd")  // 暂停当前主线程的执行，同时暂停计时，点击确定后，恢复程序执行和计时
console.log("alert 之后")
```