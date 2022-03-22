# 闭包

```javascript
for (var i = 0, length = btns.length; i < length; i++) {
  var btn = btn[i];
  btn.onclick = function () {
    alert("第" + (i + 1) + "个"); // 第4个， 第4个， 第4个
  };
}
```

```javascript
for (var i = 0, length = btns.length; i < length; i++) {
  var btn = btn[i];
  btn.index = i;
  btn.onclick = function () {
    alert("第" + (this.index + 1) + "个"); // 第1个， 第2个， 第3个
  };
}
```

```javascript
// 利用闭包
for (var i = 0, length = btns.length; i < length; i++) {
  (function (i) {
    var btn = btns[i];
    btn.onclick = function () {
      alert("第" + (i + 1) + "个"); // 第1个， 第2个， 第3个
    };
  })(i);
}
```

## 如何产生闭包？

- 当一个嵌套的内部（子）函数引用了嵌套的外部（父）函数的变量（函数）时，就产生了闭包

## 闭包到底是什么？

- 使用 chrome 浏览器查看
  > - 闭包是嵌套的内部函数（大部分人）
  > - 包含被引用变量（函数）的对象（极少数人）
  > - ps：闭包存在于嵌套的内部函数中

## 闭包产生的条件？

- 函数嵌套
- 内部函数引用了外部函数的数据（变量）

```javascript
function fn1() {
  var a = 2; // 此时就产生了闭包
  var b = "abc";
  function fn2() {
    // 执行函数定义，就会产生闭包
    console.log(a);
  }
}
fn1(); // 不需要调用内部函数，就可以产生闭包
```

```javascript
function fn1() {
  var a = 2; // 还没产生闭包
  var b = "abc";
  var fn2 = function () {
    // 此时是函数表达式
    console.log(a);
  };
}
fn1();
```

## 常用的闭包？

- 将函数作为另一个函数的返回值
- 将函数作为实参传递给另一个函数调用
  > - 产生了几个闭包？

```javascript
// 将函数作为另一个函数的返回值
function fn1() {
  var a = 2; // 其实此时就已经产生闭包了，因为函数提升
  function fn2() {
    // 执行函数定义，就会产生闭包
    a++;
    console.log(a);
  }
  return fn2;
}
var f = fn1(); // 产生了 1 个闭包
f(); // 3
f(); // 4
fn1(); // 产生了第 2 个闭包， 与执行内部的 fn2  无关
```

```javascript
// 将函数作为实参传递给另一个函数调用
function showDelay(msg, time) {
  setTimeout(function () {
    alert(msg);
  }, time);
}
showDelay("hello", 2000);
```

## 闭包的应用一

- 使用函数内部的变量在函数执行完之后，仍然存活在内存中（延长了局部变量的生命周期）
- 让函数外部可以操作（读写）到函数内部的数据（变量/函数）

### 问题

- 函数执行完之后，函数内部声明的局部变量是否还存在？
  > - 一般时候不存在
  > - 存在闭包里的变量，还是存在的
- 在函数外部能直接访问函数内部的局部变量吗？
  > - 不能
  > - 但可以通过闭包让外部操作它

```javascript
function fn1() {
  var a = 2; // 只有 a 在闭包中
  function fn2() {
    // 执行完被释放，被回收
    a++;
    console.log(a);
  }
  function fn3() {
    a--;
    console.log(a);
  }
  return fn3; // 返回 fn3 的地址值， 但是 fn3 不在了
}
var f = fn1(); // f 指向 fn3，因此 fn3 不会成为垃圾对象
f();
f();
```

## 闭包的生命周期

- 产生：在嵌套内部函数定义执行结束时，就产生了（不是在调用）
- 死亡：在嵌套的内部函数成为垃圾对象时

```javascript
function fn1() {
  // 此时闭包就已经产生了（函数提升，内部函数对象已经创建了）
  var a = 2; // 只有 a 在闭包中
  function fn2() {
    // 执行完被释放，被回收
    a++;
    console.log(a);
  }
  return fn2; // 返回 fn2 的地址值， 但是 fn2 不在了
}
var f = fn1(); // f 指向 fn2，因此 fn2 不会成为垃圾对象
f(); // 3
f(); // 4
f = null; // 闭包死亡，因为包含闭包的函数对象成为垃圾对象
```

## 闭包的应用二

- 定义 JS 模块
  > - 具有特定功能的 js 文件
  > - 将所有的数据和功能都封装到一个函数内部（私有的）
  > - 只向外暴露一个包含 n 个方法的对象或函数
  > - 模块的使用者，只需要通过模块暴露的对象调用方法，来实现对应的功能

```javascript
function myModule() {
  // msg 是私有数据，外部看不到
  var msg = "hello, world";
  function doSomething() {
    console.log("doSomething() " + msg.toUpperCase());
  }
  function doOtherthing() {
    console.log("doOtherthing() " + msg.toLowerCaes());
  }
  // 向外暴露对象（给外部使用的方法）
  return {
    doSomething: doSomething,
    doOtherthing: doOtherthing,
  };
}
var module = myModule();
module.doSomething();
module.doOtherthing();
```

```javascript
// 这种方法使用起来更加方便
(function myModule() {
  // msg 是私有数据，外部看不到
  var msg = "hello, world";
  function doSomething() {
    console.log("doSomething() " + msg.toUpperCase());
  }
  function doOtherthing() {
    console.log("doOtherthing() " + msg.toLowerCaes());
  }

  window.myModule2 = {
    doSomething: doSomething,
    doOtherthing: doOtherthing,
  };
})();
// 可以直接调用
myModule2.doSomething();
myModule2.doOtherthing();
```

```javascript
// 这么写也可以
(function myModule(window) {
  // msg 是私有数据，外部看不到
  var msg = "hello, world";
  function doSomething() {
    console.log("doSomething() " + msg.toUpperCase());
  }
  function doOtherthing() {
    console.log("doOtherthing() " + msg.toLowerCaes());
  }

  window.myModule2 = {
    doSomething: doSomething,
    doOtherthing: doOtherthing,
  };
})(window);
// 可以直接调用
myModule2.doSomething();
myModule2.doOtherthing();
```

## 闭包的缺点

- 缺点
  > - 函数执行完后，函数的局部变量没有释放，占用内存时间会变长
  > - 容易造成内存泄露
- 解决
  > - 能不用就不用
  > - 及时释放

```javascript
// 这么写也可以
function fn1() {
  var arr = new Array[1000000]();
  function fn2() {
    console.log(arr.length);
  }
  return fn2;
}
var f = fn1();
f();
f = null; // 让内部函数成为垃圾对象，进而回收闭包
```

## 内存溢出和内存泄露

- 内存溢出
  > - 一种程序运行时出现的错误
  > - 当程序运行需要的内存超过了剩余的内存时，就会抛出内存溢出的错误
- 内存泄漏
  > - 占用的内存没有及时释放
  > - 内存泄露累积多了，容易导致内存溢出
  > - 常见的内存泄露：
  >   > - 意外的全局变量
  >   > - 没有及时清理的计时器或回调函数
  >   > - 闭包

```javascript
var obj = {};
for (var i = 0; i < 1000; i++) {
  obj[i] = new Array(10000000);
}
```

```javascript
function fn() {
  // 意外的全局变量
  a = 3;
  console.log(a);
}
fn();
```

```javascript
// 忘记关闭的定时器
setInterval(function () {
  console.log("========");
}, 1000);
```

```javascript
// 应该记得关闭
var intervalId = setInterval(function () {
  console.log("========");
}, 1000);

clearInterval(intervalId);
```

```javascript
// 这么写也可以
function fn1() {
  var arr = new Array[1000000]();
  function fn2() {
    console.log(arr.length);
  }
  return fn2;
}
var f = fn1();
f();
// 如果没有 f = null，则不会释放，可能会导致内存泄露
```

## 面试题

```javascript
// 题一
var name = "window";
var object = {
  name: "my object",
  getNameFunc: function () {
    return function () {
      // 不存在闭包
      return this.name; // 虽然存在函数嵌套，但没有内部函数引用外部变量
    };
  },
};
alert(object.getNameFunc()()); // window
```

```javascript
// 题二
var name2 = "window";
var object = {
  name2: "my object",
  getNameFunc: function () {
    var that = this;
    return function () {
      // 存在闭包
      return that.name2;
    };
  },
};
alert(object.getNameFunc()()); // my object
```

```javascript
// 题三
function fun(n, o) {
  console.log(o);
  return {
    fun: function (m) {
      return fun(m, n);
    },
  };
}
var a = fun(0);
a.fun(1);
a.fun(2);
a.fun(3);
var b = fun(0).fun(1).fun(2).fun(3);
var c = fun(0).fun(1);
c.fun(2);
c.fun(3);
```
