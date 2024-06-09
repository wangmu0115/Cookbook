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




