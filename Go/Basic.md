基本数据类型、复合数据类型、接口类型

### 1. 整型

- 平台无关整型
  - `int8` `int16` `int32` `int64`
  - `uint8` `uint16` `uint32` `uint64`
- 平台相关整型
  - `int` `uint` 
  - `uintptr`

```go
// `unsafe.Sizeof()`返回变量占用的字节长度
fmt.Println(unsafe.Sizeof(int(42)))  // 8
fmt.Println(unsafe.Sizeof(uint(42))) // 8
```

- 字面量&格式化输出





数值类型

整型、浮点型、复数类型

有符号整型

int8

int16

int32

int64

无符号整型，uint8，uint16,uint32,uint64

平台无关的

平台相关的，int uint uintptr

```go
unsafe.Sizeof(a) // 返回变量的字节数量
```

数值字面量

