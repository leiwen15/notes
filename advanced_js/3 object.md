# 对象
## 1.什么是对象？
+ 多个数据的封装体
+ 用于保存多个数据的容器
+ 一个对象代表现实中的一个事物

## 2.为什么要用对象？
+ 统一管理多个数据
## 3.对象的组成？
```javascript
var persion = {
    name: 'tom',
    age: 12,
    setAge: function (age) {
        this.age = age
    },
    setName: function (name) {
        this.name = name
    }
}
persion.setName('sam')
persion['setAge'](13)

```
+ 属性：由属性名（字符串）和属性值组成
+ 方法：一个特殊的属性（属性值是函数）
## 4.如何访问对象内部的数据？
+ .属性名: 编码简单，有时候不能用
+ [字符串]：通用
>+ 什么时候只能用中括号的方式？
>>+ 属性名包含特殊字符：- 空格
>>+ 变量名不确定