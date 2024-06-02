## 函数

> 声明函数时，给出参数的类型和返回值的类型。

```ts
// 声明参数类型和返回值类型
function getFullName(firstName: string, lastName: string): string {
  return `${firstName} ${lastName}`;
}
console.log(getFullName('Remilia', 'Scarlet')); // Remilia Scarlet
```

### 函数类型声明

- 通过**箭头函数**格式定义函数类型，形式参数的参数名不能省略。
- 函数的实际参数可以少于定义的形式参数，但是不能比形式参数多。

```ts
// 箭头函数格式
// 形式参数的名称不能省略
type MyFunc = (x: string, y: number) => void;
// 函数的实际参数可以少于定义的形式参数
let myFunc1: MyFunc = (x: string) => console.log(x);
let myFunc2: MyFunc = (a: string, b: number) => console.log(a, b);
```

### Function

- `Function`类型标识任何函数

```ts
type AddFn = (x: number, y: number) => number;
function invokeFn(func: Function, ...params: unknown[]): unknown {
  return func(...params);
}
let add: AddFn = (a: number, b: number): number => {
  return a + b;
};
console.log(invokeFn(add, 3, 4)); // 7
```

### 可选参数

### 参数默认值

### 参数解构

### rest参数

### 函数重载

> 函数名相同，参数类型或数量不同

- 逐一定义每种情况的类型
- 对重载的函数给予完整的类型声明
- 在一个实现中，处理不同的参数






函数的类型声明，需要在声明函数时，给出参数的类型和返回值的类型。
不指定参数或返回值类型，TS会自行推断
将函数赋值给变量
函数的实际参数个数，可以少于类型指定的参数个数
如果一个变量要套用另一个函数类型，有一个小技巧，就是使用typeof运算符。
> 这是一个很有用的技巧，任何需要类型的地方，都可以使用typeof运算符从一个值获取类型。

函数类型还可以采用对象的写法。
这种写法平时很少用，但是非常合适用在一个场合：函数本身存在属性。

`Function`类型

 Function 类型表示函数，任何函数都属于这个类型。
 Function 类型的函数可以接受任意数量的参数，每个参数的类型都是any，返回值的类型也是any，代表没有任何约束，所以不建议使用这个类型，给出函数详细的类型声明会更好

 如果函数的某个参数可以省略，则在参数名后面加问号表示。
 函数的可选参数只能在参数列表的尾部，跟在必选参数的后面。
如果前部参数有可能为空，这时只能显式注明该参数类型可能为undefined。

设置了默认值的参数，就是可选的。如果不传入该参数，它就会等于默认值。

可选参数与默认值不能同时使用。
具有默认值的参数，不传或者传入undefined都会使用设置的默认值。
具有默认值的参数如果不位于参数列表的末尾，调用时不能省略，如果要触发默认值，必须显式传入undefined。


参数解构


