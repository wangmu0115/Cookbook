https://go.dev/blog/json

标准库：encoding/json，https://pkg.go.dev/encoding/json@go1.23.0

JSON标准：https://www.rfc-editor.org/rfc/rfc7159.html

json.Marshal 将Go Values序列化成JSON

json.Unmarshal 将JSON反序列化成Go Values



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