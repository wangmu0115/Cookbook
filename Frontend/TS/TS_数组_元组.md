## 数组类型

> JS数组在TS中分成两种类型，即`数组(Array)`和`元组(Tuple)`。

### Array

> 所有成员的**数据类型必须相同**，成员数量不固定，可以是零或无限数量成员。

#### 数组声明

```TS
// 数组Item的类型是`number`
let arr1: number[] = [0, 2, 4, 6, 8];
// 数组Item的类型是`number`或`string`
let arr2: (number | string)[] = ['a', 1, 'b', 3, 5];

// 数组泛型写法声明：
// 数组Item的类型是`number`
let arr3: Array<number> = [1, 3, 5, 7, 9];
// 数组Item的类型是`number`或`string`
let arr4: Array<number | string> = ['a', 'b', 'c', 42];
```

#### 类型推断

如果数组变量没有声明类型，TS会根据初始值推断数组的类型：
```ts
let arr1 = [];             // any[]
let arr2 = [42];           // number[]
let arr3 = ['hello'];      // string[]
let arr4 = [42, 'hello'];  // (number | string)[]
```

#### 只读数组

- `readonly`关键字声明只读数组，增加、删除、修改数组成员都会报错。
- `readonly`**不能**与数组泛型写法一起使用，泛型只读数组：`ReadonlyArray<T>`和`Readonly<T[]>`
- `as const`(**const断言**)也可以声明只读数组。

```ts
// `readonly`
const arr1: readonly number[] = [1, 3, 5, 7, 9];
// `number[]`是`readonly number[]`的子类型，因为它比只读数组多了`pop()`、`push()`等方法
const arr2: number[] = [2, 4, 42];
const arr3: readonly number[] = arr2;
// 泛型声明数组
const arr4: ReadonlyArray<number> = [2, 4, 42];
const arr5: Readonly<number[]> = [2, 4, 42];
// `as const`断言
const arr6 = [2, 4];          // number[]
const arr7 = [2, 4] as const; // readonly [2, 4]
```

#### 多维数组

TS使用`T[][]`格式声明二维数组，`T`是底层数组成员的类型：
```ts
const mdArray: number[][] = [
  [1, 3, 5],
  [2, 4, 6],
];
```

### Tuple

> **成员类型可以自由设置**的数组，元组中的成员类型可以各不相同。使用元组是，必须明确给出类型声明。

```ts
// 声明Tuple
const tup1: [string, boolean, number] = ['hello', true, 42];
// 如果省略类型声明，TS会推断为数组
const tup2 = [42, 'remilia', true]; // (string | number | boolean)[]
```

- 元组成员类型声明时添加`?`后缀，表示该成员是**可选的**，可选成员在必选成员之后。
- 使用扩展运算符(`...`)，可以表示不限成员数量的元组，扩展运算符可以在元组的任意位置。

```ts
// `?`可选成员
let tup1: [string, number?, string?];
tup1 = ['hello'];
tup1 = ['hello', 42];
tup1 = ['hello', 42, 'world'];
// `...`扩展运算符
let tup2: [string, ...number[]];
tup2 = ['remilia', 2, 4, 6];
let tup3: [...boolean[], string, number];
let tup4: [string, ...boolean[], number];
let tup5: [string, number, ...boolean[]];
```

#### 只读元组

- `readonly`关键字或使用`Readonly<[T1, T2, ...]>`声明只读元组。
- `as const`(**const断言**)生成的是一个只读的值类型，既可以解读为只读数组也可以解读为只读元组。

```ts
// 只读Tuple，普通Tuple是只读Tuple的子类型
const tup1: readonly [string, number] = ['remilia', 500];
const tup2: Readonly<[string, number]> = ['cirno', 9];
// `as const`
const tup3 = ['flandre', 495] as const; // readonly ["flandre", 495]

function fn(params: [string, number]): void {
  console.log(params[0] + "'s age is " + params[1] + '.');
}
fn(tup1 as [string, number]);
fn(tup2 as [string, number]);
fn(tup3 as [string, number]);
```

### Array/Tuple成员的类型

TS运行使用方括号`[]`读取数组或元组成员的类型：
```ts
// `[]`读取数组成员的类型
type arrType = string[];
type arrItemType = arrType[0]; // string
// `[]`读取元组成员的类型
type tupType = [string, string, boolean];
type tupItemType0 = tupType[0]; // string
type tupItemType2 = tupType[2]; // boolean

// 数组/元组的成员是数值索引，可以通过`number`读取成员类型
type arrItemTypeByIdx = arrType[number]; // string
type tupItemTypeByIdx = tupType[number]; // string | boolean
```