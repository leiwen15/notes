# 数据类型
## 一、分类：基本类型、对象（引用）类型
### 1. 基本：
>+ String: 任意字符串
>+ Number: 任意数字
>+ boolean: true/ false
>+ null: null
>+ undefined: undefined
### 2. 引用：
>+ object：任意对象
>+ function: 一种特殊的对象，可执行
>+ array: 一种特殊的对象，有下标，有序
### 二、判断
>+ typeof( 返回字符串类型 )
>>+ 可以判断 udefined 数值 字符串 布尔值 function
>>+ 不能判断: null与object  object与array
>+ instanceof( 判断对象的具体类型 )
>+ ===( 可以用来判断undefined, null )
#### 基本类型
```javascript
var a
console.log(a, typeof a === 'undefined')

var b = 4
console.log(typeof b === 'number')

var c = 's'
console.log(typeof c === 'string')

var d = true
console.log(typeof d === 'boolean')

var e = null
console.log(typeof e, e === null)
```
#### 引用类型
```javascript
var b1 = {
    b2: [1, 'abs', console.log],
    b3: funtion() {
        console.log(b3)
        return function() {
            return 'hhhh'
        }
    }
}

console.log(b1 instanceof Object, b1 instanceof Array) // true false;
console.log(b1.b2 instanceof Object, b1.b2 instanceof Array) // true true;
console.log(b1.b3 instanceof Object, b1.b3 instanceof Function) // true true;

console.log(typeof b1.b3 === "function") // true;
console.log(typeof b1.b2[2] === 'function') // true
b1.b2[2](4)
console.log(b1.b3()())

console.log(typeof b1.b2) // object

```
### 三、相关问题
#### 1.实例：实例对象
#### 2.类型：类型对象
```javascript
function Persion (name, age){ // 构造函数
    this.name = name
    this.age = age
}

var p = new Persion('Tom', 12) // 根据类型创建的实例对象
```
#### 3.undefined与null的区别
>+ undefiened 未赋值
>+ null 赋值了，但值为null
```javascript
var a
console.log(a) // undefiend

a = null
console.log(a) // null
```

#### 4. 什么时候给变量赋值为null
>+ 表明将要赋值为对象
>+ 结束前赋值，让对象成为垃圾对象，进而被回收
```javascript
var b = null
console.log(a) // undefiend

b = ['hello', 12] // 确定对象，便赋值

b = null // 切断数组与b的联系，垃圾回收数组
```

#### 5. 严格区别变量类型与数据类型
>+ 数据的类型：
>>+ 基本类型
>>+ 对象类型
>+ 变量的类型（变量内存值的类型，js是弱类型语言）：
>>+ 基本类型：保存的基本类型的数据
>>+ 引用类型：保存的是一个地址值
```javascript
var c = function () {

} // c 保存的是对象类型的地址值

console.log(typeof c) // 'function'
```