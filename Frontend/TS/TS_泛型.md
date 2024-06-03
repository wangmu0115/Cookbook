## 泛型

> **泛型**，即使用**类型参数`<T>`**在输入类型和输出类型之间建立一一对应关系。
>
> 常用场景：类型别名、函数、接口和类。
>
> **尽量少用泛型**。

### 类型别名

```ts
type Nullable<T> = T | null | undefined;
type Container<T> = { value: T };
type Tree<T> = {
  value: T;
  left: Tree<T> | null;
  right: Tree<T> | null;
};

let v1: Nullable<number> = 12;
v1 = null;
let v2: Container<string> = { value: 'hello' };
let v3: Container<number> = { value: 42 };
let v4: Tree<symbol> = {
  value: Symbol.for('root'),
  left: {
    value: Symbol.for('hello'),
    left: null,
    right: null,
  },
  right: null,
};
```

### 函数

```ts
// 具名函数
function getFirstElement<T>(arr: T[]) {
  return arr[0];
}
// 函数表达式
const fn1 = function <T>(arr: T[]): T {
  return arr[0];
};
// 箭头函数表达式
const fn2: <T>(arr: T[]) => T = <T>(arr: T[]): T => {
  return arr[0];
};
// 对象方式声明函数
const fn3: { <T>(arr: T[]): T } = getFirstElement;
```

### 接口

```ts
interface Box<T> {
  contents: T;
}
let textBox: Box<string> = {
  contents: 'Hello World',
};
// 泛型接口
interface Comparator<T> {
  compareTo(v: T): number;
}
class Rectangle implements Comparator<Rectangle> {
  compareTo(v: Rectangle): number {
    let result = 0;
    // do compare...
    return result;
  }
}
// 泛型接口
interface Fn {
  <T>(arg: T): T;
}
function id<T>(arg: T): T {
  return arg;
}
let fn: Fn = id;
```

### 类

```ts
class Pair<K, V> {
  key: K;
  value: V;
}
// 继承
class A<T> {}
class B1<T> extends A<T> {}
class B2 extends A<any> {}
// 类表达式
const C = class<T> {
  constructor(private readonly data: T) {}
};
let vc1 = new C<string | number>('hello'); // C<string | number>
vc1 = new C(42);

class D<T> {
  value!: T;
  add!: (x: T, y: T) => T;
}
let d = new D<number>();
d.value = 0;
d.add = (x, y) => x + y;
console.log(d.add(3, 4));

// 泛型类写成构造函数
type E1<T> = new (...args: any[]) => T;
interface E2<T> {
  new (...args: any[]): T;
}
function createInstance<T>(AnyClass: E1<T>, ...args: any[]) {
  return new AnyClass(args);
}
```

### 类型参数设置默认值

```ts
function getFirst<T = string>(arr: T[]) {
  return arr[0];
}
console.log(getFirst(['a', 'b', 'c']));
console.log(getFirst(['42', 42])); // 自动推导为 <string | number>

class Generic<T = string> {
  list: T[];
  add(t: T) {
    this.list.push(t);
  }
}
let v1 = new Generic();
v1.add('a');
let v2 = new Generic<number>(); // 非`string`类型，则需要显式指定
v2.add(42);
```

### 类型参数约束条件

> <TypeParameter extends ConstraintType>
>
> 上面语法中，TypeParameter表示类型参数，extends是关键字，这是必须的，ConstraintType表示类型参数要满足的条件，即类型参数应该是ConstraintType的子类型。

```ts
// 泛型类型必须有`length`属性
function compAndReturnLong<T extends { length: number }>(x: T, y: T): T {
  if (x.length >= y.length) {
    return x;
  } else {
    return y;
  }
}
let str = compAndReturnLong('cirno', 'remilia'); // `string`
console.log(str); // remilia

type Fn<A extends string, B extends string = 'world'> = [A, B];
let v1: Fn<'hello'> = ['hello', 'world'];
console.log(v1); // [ 'hello', 'world' ]
```