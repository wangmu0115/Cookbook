## 创建对象

通过`Object`构造函数或对象字面量可以很方便地创建对象，但是创建具有相同接口的多个对象需要编写很多重复的代码。

> 工厂模式，构造器模式，原型模式

### 工厂模式(Factory Pattern)

工厂模型可以解决创建多个类型对象重复代码的问题，但是没有解决对象表示问题，即新创建的对象是什么类型。

```js
// 工厂方法
function createPerson(name, age, job) {
  let person = new Object();
  person.name = name;
  person.age = age;
  person.job = job;
  person.sayName = function () {
    console.log(this.name);
  };
  return person;
}
let person1 = createPerson('Nicholas', 29, 'Software Engineer');
let person2 = createPerson('Greg', 27, 'Docker');
```

### 构造函数模式(Function Constructor Pattern)

自定义**构造函数**，通过`new`操作符创建对象实例，可以确保创建的对象实例都被标识为特定类型。

```js
// 自定义构造函数
// 构造函数也可以是函数表达式：let Person = function(name, age, job){/* do something*/}
function Person(name, age, job) {
  this.name = name;
  this.age = age;
  this.job = job;
  this.sayName = function () {
    console.log(this.name);
  };
}
// `new`操作符创建Person实例
let person = new Person('Nicholas', 29, 'Software Engineer');
```

创建的对象实例的`constructor`属性保存着对象的类型，也可以通过`instanceof`操作符确认对象类型。

```js
console.log(person.constructor); // [Function: Person]
console.log(person.constructor === Person); // true
console.log(person instanceof Object); // true
console.log(person instanceof Person); // true
```

**构造函数也是函数**

- `new`操作符创建的是一个新的对象实例，`this`指向新创建的对象。
- 直接调用构造函数，`this`会指向Global对象（浏览器环境是`window`，Nodejs环境是`global`）。
- 通过`call()`或`apply()`调用函数，`this`值会指向特定的对象。

```js
// 1.构造器创建新的实例对象，`this`指向新的实例对象。
let person = new Person('Nicholas', 29, 'Software Engineer');
person.sayName(); // Nicholas
// 2.直接调用函数，`this`指向Global对象.
Person('Greg', 27, 'Docker');
// [nodejs]运行环境
global.sayName(); // Greg
// [浏览器]运行环境
// window.sayName(); // Greg
// 3. `call()`或`apply()`，`this`指向特定的对象
let obj = new Object();
Person.call(obj, 'Kristen', 25, 'Nurse');
obj.sayName(); // Kristen
```

构造函数创建对象实例的缺点是**不同实例上的函数虽然同名，但是不相等**。
```js
// 对象中的方法是相同的，没必要创建一个实例时，都创建一个不同的`Function`实例。
let person1 = new Person('Nicholas', 29, 'Software Engineer');
let person2 = new Person('Kristen', 25, 'Nurse');
console.log(person1.sayName == person2.sayName); // false
```

### 原型模式(Prototype Pattern)

每个函数都会创建一个`prototype`属性，该属性值是一个对象，包含由特定引用类型的实例共享的**属性**和**方法**。`prototype`属性值对象就是通过调用构造函数创建的**对象的原型**。

```js
let Person = function () {};
// 将在构造函数中赋值给对象实例的值，赋值给原型，即Function的`prototype`属性
Person.prototype.name = 'Nicholas';
Person.prototype.age = 29;
Person.prototype.job = 'Software Engineer';
Person.prototype.sayName = function () {
  console.log(this.name);
};
let person1 = new Person();
let person2 = new Person();
console.log(person1.sayName === person2.sayName); // true
```

- 只要创建一个函数，就会按照特定的规则为这个函数创建一个`prototype`属性，指向**原型对象**。
- 原型对象有一个`constructor`属性，指向与之关联的**构造函数**。
- 自定义构造函数时，**原型对象**默认只会获得`constructor`属性，其他的方法都继承自Object。
- 调用构造函数创建对象新实例，实例的[[Prototype]]指针会被赋值为**构造函数的原型对象**。
- 实例与构造函数原型之间有直接的联系，但是实例与构造函数之间没有。

```js
function Person() {}
Person.prototype.name = 'Nicholas';
Person.prototype.age = 29;
Person.prototype.job = 'Software Engineer';
Person.prototype.sayName = function () {
  console.log(this.name);
};
let person1 = new Person();
let person2 = new Person();
// 函数的`prototype`属性，指向**原型对象**
// **原型对象**的`constructor`属性，指向与之关联的**构造函数**。
console.log(Person.prototype); // {name: 'Nicholas', ..., constructor: ƒ Person(), [[Prototype]]: Object}
console.log(typeof Person.prototype); // object
console.log(Person.prototype.constructor === Person); // true
// 实例的[[Prototype]]指针会被赋值为**构造函数的原型对象**，通过实例的`__proto__`属性暴露
console.log(person1.__proto__ === Person.prototype); // true
console.log(person1.__proto__ === person2.__proto__); // true
console.log(person1.__proto__.constructor == Person); // true
```
![](../_Resources/JS_Object_Prototype.png)

- 对象原型的`isPrototypeof()`方法，当参数的对象原型指向调用方时，返回`true`。
- 静态方法`Object.getPrototypeof()`，返回参数的对象原型，即[[Prototype]]的值。

```js
// `isPrototypeOf()`判断参数的对象原型是否指向调用者
console.log(Person.prototype.isPrototypeOf(person1)); // true
console.log(Person.prototype.isPrototypeOf(person2)); // true
// `Object.getPrototypeOf()`获取对象实例的内部[[Prototype]]指向的对象原型
console.log(Object.getPrototypeOf(person1) === Person.prototype); // true
console.log(Object.getPrototypeOf(person1).name); // Nicholas
```

- 静态方法`Object.setPrototypeof()`，可以向实例的[[Prototype]]写入一个新值，即为实例设置新的对象原型。
- 静态方法`Object.create()`创建新的对象，同时为其指定对象原型。

```js
let obj1 = { foo: 'hello' };
let obj2 = { bar: 42 };
// `Object.setPrototypeof()`将obj1的对象原型设置为obj2
Object.setPrototypeOf(obj1, obj2);
console.log(Object.getPrototypeOf(obj1)); // {bar: 42}
console.log(Object.getPrototypeOf(obj1) === obj2); // true
console.log(obj1.bar); // 42
// 也可以通过`Object.create()`方法创建对象的同时，设置对象原型
let obj3 = Object.create(obj2);
obj3.foo = 'hello';
console.log(Object.getPrototypeOf(obj3)); // {bar: 42}
console.log(Object.getPrototypeOf(obj3) === obj2); // true
console.log(obj3.bar); // 42
```

通过对象访问属性时，会依次从对象实例和原型对象中查找该属性对应的值。如果在对象实例中添加与原型对象同名的属性，即使赋值为`null`，也会遮蔽(shadow)原型对象的属性。使用`delete`操作符可以完全删除实例的属性。

```js
function Person() {}
Person.prototype.name = 'Nicholas';
let person = new Person();

console.log(person.name); // Nicholas
console.log(person.anotherName); // undefined
// 遮蔽原型对象中的同名属性`name`
person.name = 'Greg';
console.log(person.name); // Greg
// 赋值为`null`也会遮蔽
person.name = null;
console.log(person.name); // null
// `delete`操作符删除
delete person.name;
console.log(person.name); // Nicholas
```

- 对象实例的`hasOwnProperty()`方法，当入参的属性在对象实例存在时，返回`true`。
- `in`操作符会在通过对象访问指定属性时返回`true`，无论该属性在实例上还是原型上。

```js
function Person() {}
Person.prototype.name = 'Nicholas';
let person = new Person();

console.log(person.hasOwnProperty('name')); // false
console.log('name' in person); // true
// 实例中添加属性
person.name = 'Greg';
console.log(person.hasOwnProperty('name')); // true
console.log('name' in person); // true
// `delete`操作符删除
delete person.name;
console.log(person.hasOwnProperty('name')); // fasle
console.log('name' in person); // true
// Function: 判断某个属性是否只存在于原型对象中
function hasPrototypeProperty(object, name) {
  return name in object && !object.hasOwnProperty(name);
}
```

- `Object.keys()`返回参数传入对象的所有可枚举(`[[Enumerable]]=true`)属性名称的字符串数组。
- `Object.getOwnPropertyNames()`返回对象的所有非Symbol类型属性名的字符串数组，包括不可枚举的属性。
- `Object.getOwnPropertySymbols`返回对象的Symbol类型的属性名数组。

```js
function Person() {}
Person.prototype.name = 'Nicholas';
Person.prototype.age = 29;
Person.prototype.job = 'Software Engineer';
Person.prototype.sayName = function () {
  console.log(this.name);
};
let person1 = new Person();
person1.name = 'Greg';
Object.defineProperty(person1, 'age', {
  enumerable: false,
  value: 42,
});
let person2 = new Person();
let obj = {
  [Symbol()]: 42,
  [Symbol()]: 'hello',
};
// `Object.keys()`返回所有可枚举的属性名的字符串数组
console.log(Object.keys(Person)); // []
console.log(Object.keys(Person.prototype)); // [ 'name', 'age', 'job', 'sayName' ]
console.log(Object.keys(person1)); // ['name']
console.log(Object.keys(person2)); // []
console.log(Object.keys(obj)); // []
// `Object.getOwnPropertyNames()`返回对象的所有非Symbol类型属性名的字符串数组，包括不可枚举的属性
console.log(Object.getOwnPropertyNames(Person.prototype)); // [ 'constructor', 'name', 'age', 'job', 'sayName' ]
console.log(Object.getOwnPropertyNames(person1)); // ['name', 'age']
console.log(Object.getOwnPropertyNames(person2)); // []
console.log(Object.getOwnPropertyNames(obj)); // []
// `Object.getOwnPropertySymbols`返回对象的Symbol类型的属性名数组
console.log(Object.getOwnPropertySymbols(obj)); // [ Symbol(), Symbol() ]
```

> 属性枚举的顺序：Object.keys() 的枚举顺序是不确定的；Object.getOwnPropertyNames()、Object.getOwnPropertySymbols()和 Object.assign() 的枚举顺序是确定性的。先以升序枚举数值键，然后以插入顺序枚举字符串和符号键。在对象字面量中 定义的键以它们逗号分隔的顺序插入。
> 

对象内容序列化，`Object.values()`返回对象值的数组，`Object.entries()`返回键值对的二维数组。Symbol属性会被忽略。
```js
let obj = {
  x: 'foo',
  y: 42,
  z: {},
  [Symbol()]: true,
};
console.log(Object.values(obj)); // [ 'foo', 42, {} ]
console.log(Object.entries(obj)); // [ [ 'x', 'foo' ], [ 'y', 42 ], [ 'z', {} ] ]
```




