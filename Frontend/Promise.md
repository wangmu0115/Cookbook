## Promise

**`Promise`**对象表示异步操作最终完成（或失败）以及异步操作的结果值。本质上`Promise`是一个函数返回的对象，我们可以在它上面绑定回调函数，而不需要在一开始把回调函数作为参数传入这个函数了。

```js
getFileContentAsync("fileName.txt", function(error, result) {
  if(error) {
    throw error;
  }
});
// 回调函数可能出现回调地狱，而且编码规范是通过约定实现，Promise可以将复杂的异步处理轻松地进行规范化
const p = getFileContentAsyncPromise("fileName.txt");
p.then((result) => {}).catch((error) => {})
```



### Promise的生命周期

Promise是个**有状态**的对象，可能的状态包括：`pending`、`fulfilled`和`rejected`。Promise的生命周期对应着这三个状态：`pending`是Promise的初始状态，处于`pending`状态的Promise最终会落定为代表成功的`fulfilled`，或者代表失败的`rejected`。Promise的状态是不可逆的，落定到具体确认状态后将不再改变。

Promise具有两个私有属性[[PromiseState]]和[[PromiseResult]]，[[PromiseState]]用以表示Promise的状态，[[PromiseResult]]表示当Promise状态落定到确定状态时的值(`fulfilled`)或原因(`rejected`)。

|                   pending Promise                    |                    fulfilled Promise                    |                rejcted Promise                 |
| :--------------------------------------------------: | :-----------------------------------------------------: | :--------------------------------------------: |
| ![pending](./_Resources/Promise/promise_pending.png) | ![fulfilled](./_Resources/Promise/promise_resolved.png) | ![](./_Resources/Promise/promise_rejected.png) |








每个Promise对象都会经历一个短暂的生命周期，Promise是个有状态的对象，可能的状态包括：`pending`是Promise的初始状态，处于`pending`状态的Promise，最终会落定为代表成功的`fulfilled`，或者代表失败的`rejected`。






Promise是异步操作结果的“临时占位符”，这个结果会在未来的某个时间点提供给当前程序。Promise是ES6新增的引用类型，异步函数可以返回一个Promise，而不用通过订阅一个事件或者传递一个回调给该函数。

```js
// fetch()函数发送网络请求，并等待结果，p的类型是Promise。
const p = fetch('https://dog.ceo/api/breeds/image/random');
```


我们无法通过[[PromiseState]]来确定Promise当前所处的状态，但是可以在Promise改变状态时，通过`then()`方法来制定具体的行为。

### `Promise.prototype.then()`

`then()`方法具有两个参数，分别是当Promise落定到`fulfilled`状态时的履行处理器函数(fulfillment handler)，任何与履行相关的额外数据都会被传给这个函数
和落定到`rejected`状态的拒绝处理器(rejection handler)，任何与异步操作被拒绝相关的额外数据都会被传给这个拒绝处理器。

```ts
then<TResult1 = T, TResult2 = never>(onfulfilled?: ((value: T) => TResult1 | PromiseLike<TResult1>) | undefined | null, onrejected?: ((reason: any) => TResult2 | PromiseLike<TResult2>) | undefined | null): Promise<TResult1 | TResult2>;
```

两个handler都是可选的，可以任意选用了两种的组合

```js
const promise = fetch('https://dog.ceo/api/breeds/list/all');
// 添加处理落定到`fulfilled`和`rejcted`状态的处理器
promise.then(
  (resp) => console.log(resp.json()), // fulfillment handler
  (reason) => console.error(reason) // rejection handler
);
// 只添加落定到`fulfilled`状态的处理器
promise.then(
  (resp) => console.log(resp.json()) // fulfillment handler
);
// 只添加落定到`rejcted`状态的处理器
promise.then(
  null,
  (reason) => console.error(reason) // rejection handler
);
```



### `Promise.prototype.catch()`

`catch()`方法的行为与只传入拒绝handler的行为类似，可以将它理解为then(null, rejected_handler)的语法糖。

```ts
catch<TResult = never>(onrejected?: ((reason: any) => TResult | PromiseLike<TResult>) | undefined | null): Promise<T | TResult>;
```

### `Promise.prototype.finally()`

无论异步操作是否成功或者失败，只要操作完成，那么传给finally()的回调函数，传给finally的回调函数不接受任何参数

```ts
finally(onfinally?: (() => void) | undefined | null): Promise<T>;
```

finally和catch更清晰地表现你的意图

当你希望知道一个操作已经完成且并不关系结果时，解决处理器就很有用。


### 创建Promise

Promise的对象构造器构建，构造器函数接受一个被称作执行器（executor）的函数作为参数，该执行器函被作为参数传递给两个分别名为resolve()和reject()的函数。
当执行器执行完成之后，调用resolve()函数表示Promise操作成功完成，reject()表示Promise操作失败。

```ts
    new <T>(executor: (resolve: (value: T | PromiseLike<T>) => void, reject: (reason?: any) => void) => void): Promise<T>;
```









# 参考资料





