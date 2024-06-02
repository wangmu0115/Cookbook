## TS的类型系统

> JS运行环境无法识别TS代码，TS代码需要先编译成JS代码，在编译时，与类型相关的代码会被删除，只保留可运行的JS代码。TS的类型检查只是**编译时**的类型检查。

- **类型声明**：在标识符后添加“冒号+类型”，变量的值应该与声明的类型一致，声明的变量必须被赋值后才可以使用。
- **类型推断**：类型声明不是必须的，如果没有类型声明，TS会自行推断类型。

```ts
let num: number = 42;
let str: string = 'Hello World';
// 类型推断
let x = 42; // number
```

- 每一个值在TS中都是有类型的。例如，`42`是一个值，它的类型是`number`。
- TS只涉及类型，不涉及值，与值相关的处理，都由JS完成。
- TS项目中，存在两种代码，使用JS语法的**值代码**和使用TS类型语法的**类型代码**。TS的编译过程，就是将类型代码删除，只保留值代码。

### `any`类型

> `any`类型表示没有任何限制，该类型的变量可以被赋予任意类型的值。

- TS会关闭对`any`类型变量的类型检查。
- `any`类型是其他类型的全集，称为**顶层类型(top type)**。
- TS举行类型推断时，如果无法推断出类型，就会认为该变量类型是`any`。

```ts
let x: any;
x = 42;
x = 'hello world';
x = true;
// 类型推断无法识别类型，推断为`any`
let x; // any
```

尽量避免使用`any`类型，否则就失去了使用TS的意义了：

- 可以通过打开编译选项`noImplicitAny`，只要推断出是`any`类型就报错。
- 使用`let`和`var`声明变量时，如果不赋值，就应该显式声明类型。

### `unknown`类型

> 严格版的`any`类型，需要使用`any`类型的地方，应该优先考虑`unknown`类型。

- `unknown`类型是**顶层类型(top type)**
- 任何类型的值都可以赋值给`unknown`类型；`unknown`类型的变量不能赋值给除`any`和`unknown`以外的其他类型。
- 不能直接调用`unknown`类型变量的方法和属性。
- `unknown`类型支持的运算符：比较运算符(`==`、`===`、`!=`、`!==`、`||`、`&&`、`?`)，取反运算符(`!`)，`typeof`和`instanceof`。

```ts
// 任意类型都可以赋值给`unknown`
let x: unknown;
x = 42;
x = 'hello';
// `unknown`不能赋值给其他类型
let y: unknown = 42;
let v1: boolean = y; // 报错
let v2: string = y;  // 报错
// 不能调用`unknown`变量的方法和属性
let v3: unknown = { name: 'remilia' };
let v4: unknown = 'hello';
console.log(v3.name); // 报错
v4.trim();            // 报错
```

通过**类型缩小**使用`unknown`类型变量：

```ts
// 类型缩小，即将一个不确定的类型缩小为更明确的类型
function fn(x: unknown): void {
  if (typeof x === 'number') {
    console.log(`x is ${x}, type is number`);
  } else if (typeof x === 'string') {
    console.log(`x is ${x}, type is string`);
  } else {
    console.log(`unknown types: ${typeof x}`);
  }
}
fn(42);      // x is 42, type is number
fn('hello'); // x is hello, type is string
fn(true);    // unknown types: boolean
```

### `never`类型

- `never`类型即**空类型**，不包含任何值，无法为它赋任何值。
- `never`类型是**底层类型(bottom type)**，任何类型都包含`never`类型。
- `never`类型可以赋值给其他任意类型。

```ts
// `never`类型无法赋值
let x: never;
// `never`类型用来处理可能类型之后剩余的情况
function fn1(x: number | string) {
  if (typeof x === 'number') {
    // do something
  } else if (typeof x === 'string') {
    // do something
  } else {
    throw new Error('x should be `number` or `string`.');
  }
}
let n: any = true;
fn1(n); // Error: x should be `number` or `string`.
// `never`类型可以赋值给任意类型
function fn2(): never {
  throw new Error('Error: return never');
}
const num: number = fn2();
const str: string = fn2();
const bool: boolean = fn2();
```

### 基本类型

> `boolean`, `string`, `number`, `bigint`, `symbol`, `object`, `undefined`, `null`

#### `boolean`

```ts
let v1: boolean = true;
let v2: boolean = false;
```

#### `string`

```ts
let v1: string = 'Hello';
let v2: string = "World"
let v3: string = `${v1} ${v2}!`;
```

#### `number`

```ts
let v1: number = 42;
let v2: number = 3.14;
let v3: number = 0xff;
```

#### `bigint`

- ES2020标准引入的**大整数**，`bigint`和`number`类型不兼容。

```ts
let v1: bigint = 42n;
let v2: bigint = 0xffn;
let v3: bigint = 42;   // 报错
let v4: bigint = 3.14; // 报错
```

#### `symbol`

- ES2015标准引入的**原始类型**。
- `Symbol()`方法返回的Symbol值都是独一无二的。
- `Symbol.for()`方法可以返回相同的Symbol值。

```ts
// Symbol()
let v1: symbol = Symbol();
let v2: symbol = Symbol();
console.log(v1 == v2);  // false
console.log(v1 === v2); // false
// Symbol.for()
let v3: symbol = Symbol.for('foo');
let v4: symbol = Symbol.for('foo');
console.log(v3 == v4);  // true
console.log(v3 === v4); // true
```

##### `unique symbol`

- `symbol`类型没有字面量，只能通过变量引用，所以它**没有值类型**。
- `unique symbol`是`symbol`的子类型，表示单个的、某个具体的Symbol值，所以它实际上就是**值类型**。
- `unique symbol`只能通过`const`声明，`const`命令为变量赋值时，默认类型是`unique symbol`。

```ts
const v1: symbol = Symbol();        // symbol
const v2: unique symbol = Symbol(); // typeof v2 (unique symbol)
const v3 = Symbol();                // typeof v3 (unique symbol)
```

- `unique symbol`类型的变量是**不同的值类型**，不能相互运算。
- `unique symbol`类型的变量之间不能赋值，只能通过`typeof x`的方式声明另外一个变量的`unique symbol`类型。

```ts
const us1 = Symbol.for('foo'); // typeof us1
const us2 = Symbol.for('foo'); // typeof us2
console.log(us1 === us2); // 报错: typeof us1' and 'typeof us2' have no overlap.

const us3: unique symbol = Symbol();
const us4: unique symbol = us3; // 报错
const us5: typeof us3 = us3;    // typeof us3类型
```

- `unique symbol`类型可以作为属性名，`symbol`类型不可以。

```ts
const x: unique symbol = Symbol.for('x');
const y: symbol = Symbol.for('y');

interface Foo {
  [x]: string; // 正确
  [y]: string; // 报错
}
```

##### 类型推断

- `let`命令声明的变量，推断类型是`symbol`。
- `const`命令声明的变量，推断类型是`unique symbol`。
- `const`命令声明的变量，赋值来源于`let`命令声明的变量，推断类型是`symbol`。

```ts
let v1 = Symbol();   // symbol
const v2 = Symbol(); // typeof v2(unique symbol)
let v3 = v2;         // symbol
const v4 = v1;       // symbol
```

#### `object`

```ts
let v2: object = [1, 2, 3];            // 数组
let v3: object = (n: number) => n + 1; // 函数
let v1: object = { name: 'remilia' };  // 对象
```

#### `undefined`, `null`

- `undefined`类型只有一个值`undefined`，表示未定义。
- `null`类型只有一个值`null`，表示为空。
- 未显式类型声明的`undefined`和`null`值，在关闭编译选项`strictNullChecks`时会被推断为`any`，打开编译选项`strictNullChecks`时会被推断为`undefined`和`null`。

```ts
let v1: undefined = undefined;
let v2: null = null;

// 类型推断，关闭编译选项`strictNullChecks`会被推断为`any`
let v3 = undefined;
let v4 = null;
```

### 包装对象类型

> **包装对象(wrapper object)**：字面值在需要使用对象的场景，会自动产生的对象。

| 基本类型  | 包装对象类型 |
| --------- | ------------ |
| `boolean` | `Boolean`    |
| `string`  | `String`     |
| `number`  | `Number`     |
| `bigint`  | `BigInt`     |
| `symbol`  | `Symbol`     |

- `new`命令调用构造函数，可以获取某个基本类型值的包装对象。`bigint`和`symbol`无法直接获取包装对象。

```ts
let v1 = Number(42);          // number
let v2 = new Number(42);      // Number
let v3 = Boolean(true);       // boolean
let v4 = new Boolean(true);   // Boolean
let v5 = String('Hello');     // string
let v6 = new String('Hello'); // String
```

- 包装对象可以赋值包装对象和字面量，基本类型只能赋值字面量。
- **最佳实践**：只使用基本类型，不使用包装对象类型。TS很多内置方法的参数都是基本类型，使用包装对象类型会报错。

```ts
let v1: string = 'hello';                // 正确
let v2: String = 'hello';                // 正确

let v3: string = new String('hello');    // 错误
let v4: String = new String('hello');    // 正确
```

### `Object`

- `Object`类型代表JS语言中的广义对象，除了`undefined`和`null`，其他任何值都可以赋值给`Object`类型。
- `{}`是`Object`类型的简写形式。

```ts
let o1: Object;
// 等同于Object
let o2: {};
o1 = 42;
o1 = { foo: 42 };
o2 = 'hello';
o2 = [2, 4, 6];
```

- `object`类型代表JS语言中的狭义对象，即可以用字面量表示的对象，只包含数组、函数和对象。
- 对于显式声明为`object`和`Object`类型，只能使用JS内置对象原生的属性和方法，用户自定义的属性和方法不能使用。

```ts
let obj: object;
obj = { foo: 42 };
obj = 42;          // 出错

let obj1: Object = { foo: 42 }; // Object
let obj2: object = { foo: 42 }; // object
let obj3 = { foo: 42 }; // 声明的对象类型

console.log(obj1.toString()); // 正确，JS对象的原生方法
console.log(obj2.toString()); // 正确，JS对象的原生方法
console.log(obj3.toString()); // 正确，JS对象的原生方法

console.log(obj1.foo); // 出错
console.log(obj2.foo); // 出错
console.log(obj3.foo); // 42
```

### 值类型

> 单个值也是一种类型

- 值类型只能赋值为该值，赋值为其他值则会报错。
- `const`命令声明的基本类型变量，如果没有显式类型声明，则会推断为值类型。

```ts
let v1: 'hello';
v1 = 'hello';
v1 = 'world'; // 错误：v1是值类型(`hello`)，只能赋值'hello'。

const v2 = 42; // type: 42
const v3 = true; // type: true

const person = { name: 'remilia' }; // type: {name: string}
person.name = 'cirno'; // JS中对象虽然是常量，但是可以修改对象中的属性
```

### 联合类型

> `|`

- `A|B`，任何一个类型属于`A`或`B`。
- 可以与值类型相结合，表示一个变量值的若干种可能。
- 联合类型可以看成是声明时**类型放大(type widening)**，在处理时就需要**类型缩小(type narrowing)**。

```ts
// `类型放大`
let x: string | number;
x = 42;
x = 'hello';
// 声明为值类型的联合
let color: 'red' | 'green' | 'blue';

function fn(x: string | number): void {
  // 处理时，需要对x进行`类型缩小`
  if (typeof x === 'string') {
  } else if (typeof x === 'number') {
  } else {
  }
}
```

### 交叉类型

> `&`

- `A&B`，任何一个类型必须同时属于`A`和`B`。
- 主要用于表示对象的合成。

```ts
// 不存在值的类型既是`string`又是`number`，x的实际类型是`never`
let x: string & number;

// y的值需要同时具有`name`和`age`属性
let y: { name: string } & { age: number };
y = { name: 'remilia', age: 500 };

// 为对象添加新的属性，T2在T1的基础上增加`newProp`属性
type T1 = { prop: string };
type T2 = T1 & { newProp: number };
```

### `type`命令

> type T_Alias = T;

- `type`命令用来定义一个类型的别名。
- `type`命令属于类型代码，编译成JS代码的时候，会被全部删除。

```ts
type Age = number;
let age: Age = 42;

type Person = { name: string; age: number };
let person: Person = { name: 'Remilia', age: 500 };
```

### `typeof`运算符

> typeof $value;

- `typeof`运算符是一元运算符，返回一个字符串，代表操作数的类型。
- `typeof`运算符有两种作用：用于TS类型代码和用于JS的值代码。

```ts
let a: string = 'hello';
// typeof用于类型代码，返回的是值在TS类型系统中的类型
let b: typeof a;
// typeof用于值代码，返回的是值在运行时的类型，即JS中的类型，以下8中可能值的一种
// `undefined`, `boolean`, `number`, `string`, `object`, `function`, `symbol`, `bigint`
if (typeof a === 'string') {
  b = a;
}
```
