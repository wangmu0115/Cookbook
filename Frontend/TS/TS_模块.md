## 模块

> **模块(module)**：任何包含`import`或`export`语句的文件。

- 模块内部的变量、函数、类只在内部可见，对于模块外部是不可见的。
- 暴露给外部的接口，使用`export`命令；外部其他文件使用模块的接口，使用`import`命令。

```ts
// 位于文件moduleA.ts中
type Bool = true | false;
export { Bool };
// 在同级目录下文件moduleB.ts中引用模块moduleA中的类型`Bool`
import { Bool } from './moduleA';
let x: Bool = true;
```

### `import type`



任何包含 import 或 export 语句的文件，就是一个模块（module）。相应地，如果文件不包含 export 语句，就是一个全局的脚本文件。

模块本身就是一个作用域，不属于全局作用域。模块内部的变量、函数、类只在内部可见，对于模块外部是不可见的。

```ts
export {};
```

import type
