## JSON

### 1. 概览

JSON(JavaScript Object Notation)是一种简单的数据交换格式。

- JSON标准 [RFC 7159](https://www.rfc-editor.org/rfc/rfc7159.html)
- Go序列化/反序列化JSON标准库：[encoding/json](https://pkg.go.dev/encoding/json)

```go
func Marshal(v any) ([]byte, error) // 将Go值序列化成JSON

func Unmarshal(data []byte, v any) error // 反序列化JSON数据并将结果保存在`v`中
```

### 2. 序列化/Encoding

```go
type Variable struct {
	Name  string  `json:"name"`
	Label *string `json:"label,omitempty"`
	Type  int     `json:"type"`
}
type CustomVariable struct {
	Variable
	Multi   bool     `json:"multi"`
	Options []string `json:"options"`
}

func main() {
	v := Variable{Name: "gender", Type: 1}
	cv := CustomVariable{Variable: v, Multi: false, Options: []string{"male", "female", "unknow"}}
	b, err := json.Marshal(cv)
	if err != nil {
		fmt.Println(err)
    return
	}
	// {"name":"gender","type":1,"multi":false,"options":["male","female","unknow"]}
	fmt.Println(string(b))
}
```

只有能够表示为有效JSON的数据结构才会被序列化，否则会返回`error`：

- JSON对象**只支持string类型**的键，如果序列化map类型的Go值，则map类型的格式必须是`map[string]T`。
- `channel`、`complex`、`function`类型无法被序列化。
- **不支持循环数据结构**，会导致`Marshal`陷入无限循环。
- 指针会被序列化为其指向的值，如果指针为`nil`则为`null`。
- 只有**导出字段（大写字母开头的字段）**会被序列化在JSON对象中。

### 3. 反序列化

```go
func main() {
	vJson := `{"Name":"gender","type":null,"multi":false,"options":["male","female","unknow"]}`
	var cv CustomVariable
	err := json.Unmarshal([]byte(vJson), &cv)
	if err != nil {
		fmt.Println(err)
		return
	}
	// {{gender <nil> 0} false [male female unknow]}
	fmt.Println(cv)
}
```

- 如果JSON对象的字段值为空，则反序列化的Go值对应的字段值为**字段类型默认空值**，如果不希望将`null`反序列化类型空值，则可以声明为指针类型，例如`Label`和`Type`字段。













```json
```











### 4. References

- [JSON and Go](https://go.dev/blog/json)





序列化 Encoding

```go
func Marshal(v interface{}) ([]byte, error)
```

Only data structures that can be represented as valid JSON will be encoded:

- JSON objects only support strings as keys; to encode a Go map type it must be of the form `map[string]T` (where `T` is any Go type supported by the json package).
- Channel, complex, and function types cannot be encoded.
- Cyclic data structures are not supported; they will cause `Marshal` to go into an infinite loop.
- Pointers will be encoded as the values they point to (or ’null’ if the pointer is `nil`).

The json package only accesses the exported fields of struct types (those that begin with an uppercase letter). Therefore only the exported fields of a struct will be present in the JSON output.

反序列化 Decoding

```go
func Unmarshal(data []byte, v interface{}) error
```

How does `Unmarshal` identify the fields in which to store the decoded data? For a given JSON key `"Foo"`, `Unmarshal` will look through the destination struct’s fields to find (in order of preference):

- An exported field with a tag of `"Foo"` (see the [Go spec](https://go.dev/ref/spec#Struct_types) for more on struct tags),
- An exported field named `"Foo"`, or
- An exported field named `"FOO"` or `"FoO"` or some other case-insensitive match of `"Foo"`.

以上是在明确知道JSON格式的前提下，有可能存在不知道JSON格式的情况，我们反序列化成`interface{}`

空接口是通用容器类型，interface{}

类型断言

The json package uses `map[string]interface{}` and `[]interface{}` values to store arbitrary JSON objects and arrays