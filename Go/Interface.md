接口类型是由`type`和`interface`关键字定义的一组方法集合。

```go
type MyInterface interface {
	M1(int) error
	M2(io.Writer, ...string)
}
```

接口类型的方法集合中声明的方法，它的参数列表不需要写出形参名字，返回值列表也是如此。即，方法的参数列表中形参名字与返回值列表中的具名返回值，都不作为区分两个方法的凭据。

Go语言要求接口类型中声明的方法必须是具名的，且唯一。

类型嵌入，接口类型嵌入，必须保证同名方法的参数签名和返回值列表必须相同

Tip：接口类型也可以声明非导出的方法，但是不建议使用

```go
// $GOROOT/src/context/context.go
type canceler interface {
	cancel(removeFromParent bool, err error)
	Done() <-chan struct{}
}
```

**空接口类型** `interface{}` `any`

接口类型定义中没有一个方法，方法集合为空

```go
type EmptyInterface interface{}
```

接口类型定义之后，就可以用于声明变量，**接口类型变量**

接口类型变量的默认空值为nil

**如果一个类型`T`的方法集合是某接口类型`I`的方法集合的等价集合或超集，那么我们就说类型`T`实现了接口类型`I`，那么类型`T`的变量就可以作为合法的右值赋值给接口类型`I`的变量**

