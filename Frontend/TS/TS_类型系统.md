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

> ES2020标准引入的**大整数**，`bigint`和`number`类型不兼容。

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

- 











#### `object`类型
```ts
let v1: object = { name: 'remilia' };  // 对象
let v2: object = [1, 2, 3];            // 数组
let v3: object = (n: number) => n + 1; // 函数
```

#### `undefined`和`null`类型
> `undefined`类型只有一个值`undefined`，表示未定义
>
> `null`类型只有一个值`null`，表示为空
>
> `noImplicitAny`, `strictNullChecks` 关闭时，推断是any，否则推断是具体的类型
```ts
// 第一个是类型，第二个是值
let v1: undefined = undefined; 
let v2: null = null;
```

### 包装对象类型
> `boolean`, `string`, `number`, `bigint`, `symbol`


#### 数组类型










