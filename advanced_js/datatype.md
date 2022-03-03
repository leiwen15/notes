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

```
