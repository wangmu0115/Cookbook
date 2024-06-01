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

### **值(value)**和**类型(type)**

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

- `unknown`类型是**顶层类型(top type)**，任何类型的值都可以赋值给`unknown`类型；`unknown`类型的变量不能赋值给除`any`和`unknown`以外的其他类型。
- 不能直接调用`unknown`类型变量的方法和属性。
- `unknown`类型支持的运算符：比较运算符(`==`、`===`、`!=`、`!==`、`||`、`&&`、`?`)，取反运算符(`!`)，`typeof`和`instanceof`。
```ts
// 1. 任意类型都可以赋值给`unknown`
let x: unknown;
x = 42;
x = 'hello';
x = false;
// 2. `unknown`不能赋值给其他类型
let y: unknown = 42;
let v1: boolean = y; // 报错：Type 'unknown' is not assignable to type 'boolean'.
let v2: string = y; // 报错：Type 'unknown' is not assignable to type 'string'.
// 3. 不能调用`unknown`变量的方法和属性
let v3: unknown = { name: 'remilia' };
console.log(v3.name); // 报错：'v3' is of type 'unknown'.
let v4: unknown = 'hello';
v4.trim(); // 报错：'v4' is of type 'unknown'.
let v5: unknown = (n: number) => n + 1;
console.log(v5(42)); // 报错：'v5' is of type 'unknown'.
```


- `unknown`类型支持的运算符：`==`、`===`、`!=`、`!==`、`||`、`&&`、`?`、`!`、`typeof`、`instanceof`，其他运算符会直接报错
- 通过“类型缩小”，`unknown`类型变量才可以使用。

### `never`类型

- `never`类型即**空类型**，不包含任何值，无法为它赋任何值。
- `never`类型是**底层类型(bottom type)**，任何类型都包含`never`类型。
- `never`类型可以赋值给其他任意类型。

```ts
// 1. `never`类型无法赋值
let x: never;
// 2. `never`类型
function fn(x: number | string) {
  if (typeof x === 'number') {
    // do something
  } else if (typeof x === 'string') {
    // do something
  } else {
    throw new Error('x should be `number` or `string`.');
  }
}
let n: any = true;
fn(n); // Error: x should be `number` or `string`.
// 3. `never`类型可以赋值给任意类型
function fn2(): never {
  throw new Error('Error: return never');
}
const num: number = fn2();
const str: string = fn2();
const bool: boolean = fn2();
```













