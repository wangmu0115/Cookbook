## 函数

### 1. First Class

> https://wiki.c2.com//?FirstClass
>
> A language construct is said to be a `FirstClass` value in that language when there are no restrictions on how it can be created and used: when the construct can be treated as a value without restrictions.

- Go函数可以存储在变量中

```go
var F2 = func(format string, args ...interface{}) (int, error) {
	return fmt.Printf(format, args...)
}
```

- 支持在函数内创建并通过返回值返回

```go
func Setup(task string) func() {
	fmt.Printf("1. do some setup stuff for %s.\n", task)
	return func() {
		fmt.Printf("3. do some teardown stuff for %s.\n", task)
	}
}
func main() {
	teardown := Setup("demo")
	defer teardown()
	fmt.Println("2. do some business stuff")
}
```

- 作为参数传入函数
- 拥有自己的类型









错误处理机制

