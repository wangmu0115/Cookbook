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