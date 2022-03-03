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

