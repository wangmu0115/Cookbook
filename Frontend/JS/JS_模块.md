## 模块模式

背后思想：把逻辑分块，各自封装，相互独立，每个块自行决定对外暴露什么，同时自行决定引入执行哪些外部代码。

### 模块标识符

模块系统本质上是键/值实体，其中每个模块都有个可用 于引用它的标识符。这个标识符在模拟模块的系统中可能是字符串，在原生实现的模块系统中可能是模 块文件的实际路径。

完善的模块系统一定不会存在模块标识冲突的问题，且系统中的任何模块都应该能够无歧义地 引用其他模块。

将模块标识符解析为实际模块的过程要根据模块系统对标识符的实现。原生浏览器模块标识符必须 提供实际 JavaScript 文件的路径。除了文件路径，Node.js 还会搜索 node_modules 目录，用标识符去匹配 包含 index.js 的目录。

### 模块依赖

模块系统的核心是管理依赖。指定依赖的模块与周围的环境会达成一种契约。本地模块向模块系统 声明一组外部模块(依赖)，这些外部模块对于当前模块正常运行是必需的。模块系统检视这些依赖， 进而保证这些外部模块能够被加载并在本地模块运行时初始化所有依赖。

每个模块都会与某个唯一的标识符关联，该标识符可用于检索模块。这个标识符通常是 JavaScript 文件的路径，但在某些模块系统中，这个标识符也可以是在模块本身内部声明的命名空间路径字符串。

### 模块加载





### CommonJS

CommonJS规范概述了**同步声明依赖**的模块定义，主要用于在**服务端**实现模块化代码组织：使用`require()`指定依赖，使用`module.exports`对象定义自己的公共API。

```js
// moduleA.js
console.log('moduleA');
function doStuff() {
  return 'hello world';
}
module.exports = { // 导出`moduleA`的公共API
  doStuff,
};

// 与`moduleA.js`同级目录下的`moduleB.js`文件
// 指定依赖`moduleA`
let moduleA = require('./moduleA'); // `./moduleA` = 相对路径的模块标识符
module.exports = { // 导出模块`moduleB`的公共API
  stuff: moduleA.doStuff(),
};
```

### 异步模块定义(AMD, Asynchronous Module Definition)

AMD的模块定义系统以**浏览器**为目标执行环境，实现的核心是用函数包装模块定义。包装模块的函数是全局`define`的参数，它是由AMD加载器库的实现定义的。

AMD模块可以使用字符串标识符指定自己的依赖，AMD加载器会在所有依赖模块加载完毕后立即调用模块工厂函数。

```js
// `moduleB`的模块定义，`moduleB`依赖`moduleA`，`moduleA`会异步加载
define('moduleB', ['moduleA'], function(moduleA) {
  return {
	stuff: moduleA.doStuff();
  }
})
// 也支持`require`和`exports`对象
define('moduleB', ['require', 'exports'], function(require, exports) { 
  let moduleA = require('moduleA');
  exports.stuff = moduleA.doStuff();
});
```

### 通用模块定义(UMD, Universal Module Definition)

为了统一CommonJS和AMD生态系统，UMD规范应运而生。UMD定义的模块会在启动时检测要使用哪个模块系统，然后进行适当配置，并把所有逻辑包装在一个立即调用的函数表达式(IIFE)中。

### ES6模块

#### 模块标签及定义

带有`type="module"`属性的`<script>`标签的相关代码会作为模块执行，模块可以嵌入到页面中，或作为外部文件引入，不过嵌入的模块定义代码不能使用`import`加载到其他模块。

```html
<script type="module">
  // 嵌入的模块代码
</script>
<!-- 外部文件引入 -->
<script type="module" src="path/to/module.js"></script>
```

- **立即下载，延迟执行**：解析到`<script type="module">`标签时，会立即下载模块文件，但是会延迟到文档解析完成后执行。
- **模块单例**：同一个模块无论在一个页面中被加载多少次，也不管是如何加载的，实际上都只会加载一次。

#### 模块加载

ES6模块既可以通过浏览器加载，也可以与第三方加载器和构造工具一起加载，从顶级模块异步加载整个依赖图。浏览器会解析入口模块，确定依赖，并发送对依赖模块的请求。这些文件通过网络返回后，浏览器就会解析它们的内容，确定它们的依赖，如果这些二级依赖还没有加载，则会发送更多请求。这个异步递归加载过程会持续到整个应用程序的依赖图都解析完成。解析完依赖图，应用程序就可以正式加载模块了。

#### 模块特性

- 模块代码只在加载后执行。
- 模块只能加载一次。
- 模块是单例。
- 模块可以定义公共接口，其他模块可以基于这个公共接口观察和交互。
- 模块可以请求加载其他模块。
- 支持循环依赖。
- 默认在严格模式下执行。
- 不共享全局命名空间。
- 模块顶级`this`的值是`undefined`(浏览器环境中是`window`)。
- 模块中的`var`声明不会添加到`window`对象中。
- ES6模块是异步加载和执行的。

与`<script type="module">`关联或者通过`import`语句加载的JavaScript文件会被认定为模块。

#### 模块导出

ES6模块控制哪些部分对外部可见是通过`export`关键字实现的，支持两种导出：命名导出和默认导出。导出语句必须在**模块顶级**，不能嵌套在某个块中。



























