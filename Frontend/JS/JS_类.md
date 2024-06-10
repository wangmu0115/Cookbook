## 类(class)

定义类有两种主要方式：**类声明**和**类表达式**，类可以包含*构造函数*、*实例方法*、*获取函数*、*设置函数*和*静态类方法*。

```js
// 类声明
class Person {}
// 类表达式
const Animal = class {};

let person = new Person();
let animal = new Animal();
```

### 类构造函数

`constructor`关键字用于在类定义块内部创建类的构造函数，当使用`new`操作符创建类的新实例时，会调用该函数。

```js
class A {}
class B {
  constructor() {
    console.log('B constructor');
  }
}
class C {
  constructor() {
    this.color = 'red';
  }
}

let a = new A();
let b = new B(); // B constructor
let c = new C();
console.log(c.color); // red
```

- `new`操作符会在内存中创建一个新对象，构造函数中的`this`指向该对象。
- 如果构造函数返回非空对象，则`new`操作符就返回该非空对象，否则返回新创建的对象。
- 类实例化时传入的参数会用作构造函数的参数。

```js
class Foo {
  constructor(override) {
    console.log(`Arguments length: ${arguments.length}`);
    // 如果传入参数不为空，则使用传入的参数，否则默认为`false`
    this.override = override || false;
    if (override) {
      return {
        bar: 'bar',
      };
    }
  }
}
// 不传入参数
let f1 = new Foo();     // Arguments length: 0
let f2 = new Foo(true); // Arguments length: 1
// override为false，`new`操作符返回的是`this`
console.log(f1);                // Foo { override: false }
console.log(f1 instanceof Foo); // true
// override为true，构造函数返回非空对象，`new`操作符返回的是该非空对象
console.log(f2);                // { bar: 'bar' }
console.log(f2 instanceof Foo); // false
```

类构造函数与构造函数的主要区别是，调用类构造函数必须使用`new`操作符。

```js
function A1() {
  this.foo = 'foo';
}
class A2 {
  constructor() {
    this.bar = 'bar';
  }
}
// 构造函数如果不使用`new`，则会以全局的`this`作为内部对象
let v1 = A1();
// 浏览器环境是`window`，nodejs环境是`global`
console.log(global.foo); // foo
let v2 = new A1();
console.log(v2.foo); // foo
let v3 = new A2();
console.log(v3.bar); // bar
// 类构造函数必须使用`new`操作符
let v4 = A2(); // 报错
```

ECMAScript类就是一种特殊函数，`typeof`操作符返回的是`function`，`instanceof`操作符检查构造函数原型是否存在于实例的原型链中。

```js
class Foo {}
// `typeof`操作符
console.log(Foo); // class Foo {}
console.log(typeof Foo); // function
// 类标识符具有`prototype`属性，对象原型的`constructor`属性指向类本身
console.log(Foo.prototype); // {}
console.log(Foo.prototype.constructor); // class Foo {}
let foo = new Foo();
// `instanceof`操作符
console.log(foo instanceof Foo); // true
```

类是JS的一等公民，可以像其他对象或函数引用一样把类作为参数传递。与立即调用函数表达式类似，类也可以立即实例化。

```js
let classList = [
  class {
    constructor(id) {
      this.id = id;
      console.log(`instance ${this.id}`);
    }
  },
];
// 类可以作为参数传递
function createInstance(classDefinition, id) {
  return new classDefinition(id);
}
let foo = createInstance(classList[0], 9527); // instance 9527
// 立即实例化
let instance = new (class {
  constructor(val) {
    this.val = val;
  }
})('bar');
console.log(instance.val); // bar
```



