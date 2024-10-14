组合设计哲学

```go
// net/http/server.go
func (srv *Server) ListenAndServeTLS(certFile, keyFile string) error {}
```

相比函数，多了receiver参数

receiver参数是方法与类型之间的纽带

- Go中的方法必须归属于一个类型，对应receiver参数的类型

receiver参数类型可以是T或者*T，无论是那种，T是receiver参数t的基类型。

每个方法只能有一个receiver参数

方法接收器（receiver）参数、函数 / 方法参数，以及返回值变量对应的作用域范围，都是函数 / 方法体对应的显式代码块。

receiver 参数的基类型本身不能为指针类型或接口类型。

方法声明要与 receiver 参数的基类型声明放在同一个包内。

- 不能为原生类型（诸如 int、float64、map 等）添加方法。
- 不能跨越 Go 包为其他包的类型声明新方法。

如果 receiver 参数的基类型为 T，那么我们说 receiver 参数绑定在 T 上，我们可以通过 *T 或 T 的变量实例调用该方法

我们是将 receiver 参数以第一个参数的身份并入到方法的参数列表中。

**方法表达式（Method Expression）**

以类型名 T 调用方法的表达方式，被称为 Method Expression。

 Go 语言的 Method Expression 在使用时，同样以 receiver 参数所代表的类型实例作为第一个参数。

Go 语言中的方法的本质就是，一个以方法的 receiver 参数作为第一个参数的普通函数。





GO函数的参数采用的是值拷贝传递

选择receiver参数的原则：

- 如果 Go 方法要把对 receiver 参数代表的类型实例的修改，反映到原类型实例上，那么我们应该选择 *T 作为 receiver 参数的类型。

无论是 T 类型实例，还是 *T 类型实例，都既可以调用 receiver 为 T 类型的方法，也可以调用 receiver 为 *T 类型的方法。

- 如果我们不需要在方法中对类型实例进行修改呢？这个时候我们是为 receiver 参数选择 T 类型还是 *T 类型呢？这也得分情况。一般情况下，我们通常会为 receiver 参数选择 T 类型，因为这样可以缩窄外部修改类型实例内部状态的“接触面”，也就是尽量少暴露可以修改类型内部状态的方法。不过也有一个例外需要你特别注意。考虑到 Go 方法调用时，receiver 参数是以值拷贝的形式传入方法中的。那么，如果 receiver 参数类型的 size 较大，以值拷贝形式传入就会导致较大的性能开销，这时我们选择 *T 作为 receiver 类型可能更好些。

方法集合也是用来判断一个类型是否实现了某接口类型的唯一手段，可以说，“方法集合决定了接口实现”。

Go 语言规定，*T 类型的方法集合包含所有以 *T 为 receiver 参数类型的方法，以及所有以 T 为 receiver 参数类型的方法。





类型嵌入（Type Embedding），在一个类型的定义中嵌入其他类型，**接口类型的类型嵌入**和**结构体类型的类型嵌入**







