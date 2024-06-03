使用大括号表示对象，在大括号内部声明每个属性和方法的类型
```ts
// `{}`表示对象
const obj: {
  name: string;
  age: number;
} = { name: 'cirno', age: 9 };

// `type`别名
type Person = {
  name: string;
  age: number;
};
let person1: Person = { name: 'remilia', age: 500 };
let person2: Person = { name: 'flandre', age: 495 };

type Point = {
  x: number;
  y: number;
  add(x: number, y: number): number;
};
let point: Point = {
  x: 3,
  y: 4,
  add(x, y) {
    return x + y;
  },
};
```