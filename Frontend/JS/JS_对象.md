## 对象

ECMA-262将对象定义为**一组属性的无序集合**，对象的每个属性都由唯一的名称标识，名称映射到一个数据或者函数。我们可以将ECMAScript的对象想象成一张散列表，其中的内容就是一组名/值对。

创建自定义对象有两种方式：创建`Object`的一个新实例，再给它添加属性和方法；对象字面量。
```js
// `new Object()`
let person1 = new Object();
person1.name = 'Nicholas';
person1.age = 29;
person1.sayName = function () {
  console.log(this.name);
};
// 对象字面量
let person2 = {
  name: 'Nicholas',
  age: 29,
  sayName() {
    console.log(this.name);
  },
};
```

### 属性的类型

> `Object.defineProperty()`

对象的属性分为两种：**数据属性**和**访问器属性**。

#### 数据属性

数据属性包含一个保存数据值的位置，值会从这个位置读取，也会写入到这个位置。数据属性有4个特性描述它们的行为：

- `[[Configurable]]`：属性是否可以通过`delete`删除并重新定义，是否可以修改它的特性，是否可以把它改为访问器属性。直接定义在对象上的属性的这个特性是`true`。
- `[[Enumerable]]`：属性是否可以通过`for-in`循环返回。直接定义在对象上的属性的这个特性是`true`。
- `[[Writable]]`：属性的值是否可以被修改。直接定义在对象上的属性的这个特性是`true`。
- `[[Value]]`：属性实际的值。默认值是`undefined`。

```js
let person = {
  // `name`是数据属性，[[Configurable]]、[[Enumerable]]和 [[Writable]]都被设置为`true`，[[Value]]被设置为'Nicholas'。
  name: 'Nicholas',
};
```

`Object.defineProperty()`方法可以创建或修改数据属性。

```js
let person = {
  // `name`是数据属性，[[Configurable]]、[[Enumerable]]和[[Writable]]都被设置为`true`，[[Value]]被设置为'Nicholas'。
  name: 'Nicholas',
};
// 修改`name`属性
Object.defineProperty(person, 'name', {
  configurable: false, // [[Configurable]]
  enumerable: true, // [[Enumerable]]
  writable: false, // [[Writable]]
  value: 'Greg', // [[Value]]
});
// 创建`age`属性
Object.defineProperty(person, 'age', {
  configurable: true, // 新定义的属性特性默认为`false`
  enumerable: true, // 可以将这行注释，`console.log()`方法打印的对象将不再包含`age`属性
  writable: true,
  value: 29,
});
console.log(person); // { name: 'Greg', age: 29 }
```




