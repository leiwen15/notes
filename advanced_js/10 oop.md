# 对象创建模式

## 方式一、Object 构造函数模式

- 套路：先创建空的 Object 对象，再动态添加属性、方法
- 适用场景：起始时不确定对象内部数据
- 问题：语句太多

```javascript
var p = new Object();
p.name = "tom";
p.age = 12;
p.setName = function (name) {
  this.name = name;
};
p.setName("marry");
console.log(p);
```

## 方式二、对象字面量模式

- 套路：使用 {} 创建对象，同时指定属性、方法
- 适用场景：起始时，对象内部数据是确定的
- 问题：如果创建多个对象，有重复代码

```javascript
var p = {
  name: "tom",
  age: 12,
  setName: function () {
    this.name = name;
  },
};
```

## 方式三、工厂模式

- 套路：通过工厂函数动态创建对象并返回
- 适用场景：需要创建多个对象
- 问题：对象没有一个具体的类型，都是 Object 类型

```javascript
function createPerson(name, age) {
  // 返回一个对象的函数 ===> 工厂函数
  var obj = {
    name: "tom",
    age: 12,
    setName: function () {
      this.name = name;
    },
  };
  return obj;
}
var p1 = createPerson("marry", 12);
var p2 = createPerson("tom", 12);
// 这种模式不太用
// 因为这种模式没有具体类型
// s 和 p1 都是 obj 类型
function createStudent(name, price) {
  var obj = {
    name: "tom",
    age: 12,
    setName: function () {
      this.name = name;
    },
  };
  return obj;
}
var s = createStudent("jack", 12000);
```

## 方式四、自定义构造函数模式

- 套路：自定义构造函数，通过 new 创建对象
- 适用场景：需要创建多个类型确定的对象
- 问题：每个对象都有相同的数据，浪费内存

```javascript
function Person(name, age) {
  this.name = name;
  this.age = age;
  this.setName = function (name) {
    this.name = name;
  };
}
var p1 = new Person("tom", 12);
var p2 = new Person("marry", 14);
p1.setName("Jack");
console.log(p1.name, p1.age);
console.log(p1 instanceof Person);
// 浪费空间
// p1 和 p2 都存储了 setName 这个方法
console.log(p1, p2);

function Student(name, age) {
  this.name = name;
  this.age = age;
  this.setName = function (name) {
    this.name = name;
  };
}
var s = new Student("jim", 13);
console.log(s instanceof Student);
```

## 方式五、构造函数 + 原型的组合模式

- 套路：自定义构造函数，属性在函数中初始化，方法添加到原型上
- 适用场景：需要创建多个类型确定的对象

```javascript
function Student(name, age) {
  this.name = name;
  this.age = age;
}
Student.prototype.setName = function (name) {
  this.name = name;
};
var s1 = new Student("jim", 12);
var s2 = new Student("marry", 13);
console.log(s1, s2);
```

- new 一个对象背后做了什么？
  > - 创建一个空对象
  > - 给对象设置 \_\_proto\_\_，值为构造函数对象的 prototype 属性值
  > - 执行构造函数体（给对象添加属性 / 方法）
