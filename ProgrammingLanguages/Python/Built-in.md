> 
>
> **[Built-in Types](https://docs.python.org/3/library/stdtypes.html)**

### 内建函数

> **[Built-in Functions](https://docs.python.org/3/library/functions.html)**

| 函数                                                         | 描述                                       |
| ------------------------------------------------------------ | ------------------------------------------ |
| `print(*objects, sep=' ', end='\n', file=None, flush=False)` | 将对象输出到文本流文件，默认输出到控制台。 |
| `input()`<br />`input(prompt)`                               | 从输入中读取一行，将其转换为字符串并返回。 |



| 函数                                                         | 描述                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| `class float(number=0.0, /)`<br/>`class float(string, /)`    | 返回由数字或字符串构造的浮点数对象，默认值`0.0`              |
| `class int(number=0, /)`<br/>`class int(string, /, base=10)` | 返回由数字或字符串构造的整数对象，默认值`0`                  |
| `class complex(number=0, /)`<br/>`class complex(string, /)`<br/>`class complex(real=0, imag=0)` | 将字符串或数字转换为复数，或根据实部（`real`）和虚部（`imag`）创建复数 |
| `class bool(object=False, /)`                                | 返回布尔值对象，使用标准真值测试程序转换参数，默认值`False`  |
| `class str(object='')`<br/>`class str(object=b'', encoding='utf-8', errors='strict')` | 返回字符串对象                                               |
|                                                              |                                                              |
|                                                              |                                                              |
|                                                              |                                                              |
| `class type(object)`                                         | 返回对象的类型                                               |
|                                                              |                                                              |



| 函数                                                       | 描述                                                         |
| ---------------------------------------------------------- | ------------------------------------------------------------ |
| `class range(stop)`<br/>`class range(start, stop, step=1)` | 生成一个不可变的均匀分布的整数序列：[`range`](https://docs.python.org/3/library/stdtypes.html#ranges) |
| `enumerate(iterable, start=0)`                             | 将一个可迭代对象转换为一个由索引和元素组成的枚举对象         |
| `zip(*iterables, strict=False)`                            | 返回元组的迭代器，其中第`i`个元组包含每个参数可迭代对象中的第`i`个元素<br />`strict=True`可迭代对象参数的长度不一致时返回错误 |
|                                                            |                                                              |
|                                                            |                                                              |
|                                                            |                                                              |
|                                                            |                                                              |
|                                                            |                                                              |
|                                                            |                                                              |
|                                                            |                                                              |
|                                                            |                                                              |

```python
names = ["Remilia", "Cirno", "Flandre"]
# 10: Remilia | 11: Cirno | 12: Flandre |
for index, name in enumerate(names, start=10):
    print(f"{index}: {name}", end=" | ")

x = [1, 2, 3, 4, 5]
y = [6, 7, 8, 9, 0]
dot_product = 0
for (x_i, y_i) in zip(x, y):
    dot_product += x_i * y_i
# x and y dot product is 80
print(f"x and y dot product is {dot_product}")
```











| 函数           | 描述                                                         | 函数定义                                                     |
| -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
|                |                                                              |                                                              |
|                |                                                              |                                                              |
|                |                                                              | |
| `abs()` | 返回数值的绝对值，参数可以是`int`、`float`和实现`__abs__()`的对象 | **abs**(*x*) |
| |  | |
| | | |
| `isinstance()` | 检查对象是否为特定类型的实例                                 | **isinstance**(*object*, *classinfo*)     |
| `getattr()`    | 返回对象对应名称的属性或方法                                 | **getattr**(*object*, *name*)<br/>**getattr**(*object*, *name*, *default*) |
| `hasattr()`    | 名称对应的属性或方法在对象中是否存在                         | **hasattr**(*object*, *name*)                                |
| `setattr()`    | 为对象添加/修改名称对应的属性或方法的值                      | **setattr**(*object*, *name*, *value*)                       |
| `iter()`       | 返回一个迭代器(**iterator**)对象                             | **iter**(*object*)<br/>**iter**(*object*, *sentinel*)        |
| `range()`      | 生成一个不可变的均匀分布的整数序列，[build-in sequence type: range](https://docs.python.org/3/library/stdtypes.html#typesseq-range) | *class* **range**(*stop*)<br/>*class* **range**(*start*, *stop*, *step=1*) |
| `type()`       | 返回对象的类型                                               | *class* **type**(*object*)                                   |
| `type()`       | 返回一个新类型对象，这本质上是`class`语句的动态形式          | *class* **type**(*name*, *bases*, *dict*, ***kwds*)          |
|        |                                                              |                                                              |
|                |                                                              |                                                              |
|                |                                                              |  |
|                |                                                              |                                                              |
| `len()`        | 返回对象的长度，即元素数量。参数可以是序列(`str`, `bytes`, `bytearray`, `memoryview`, `tuple`, `list`, `range`)或集合(`dict`, `set`, `frozenset`) | **len**(*s*)                                                 |
|                |                                                              |                                                              |
|                |                                                              |                                                              |
|                |                                                              |                                                              |
|                |                                                              |                                                              |
|                |                                                              |                                                              |
| `zip()` | 返回元组的迭代器，其中第`i`个元组包含每个参数可迭代对象中的第`i`个元素。`strict=True`参数可以在参数的长度不一致时返回错误， | **zip**(**iterables*, *strict=False*) |
|  |  |  |



```python
# zip()
zip_result = zip(range(3), ["a", "b", "c"], [True, False, True]) # <zip object at 0x7f98001e9d80>
print([x for x in zip_result]) # [(0, 'a', True), (1, 'b', False), (2, 'c', True)]
```





A
abs()
aiter()
all()
anext()
any()
ascii()

B
bin()

breakpoint()
bytearray()
bytes()

C
callable()
chr()
classmethod()
compile()

D
delattr()
dict()
dir()
divmod()

E
enumerate()
eval()
exec()

F
filter()

format()
frozenset()

G
getattr()
globals()

H
hasattr()
hash()
help()
hex()

I
id()


isinstance()
issubclass()
iter()

L
len()
list()
locals()

M
map()
max()
memoryview()
min()

N
next()

O
object()
oct()
open()
ord()

P
pow()

property()




R
range()
repr()
reversed()
round()

S
set()
setattr()
slice()
sorted()
staticmethod()

sum()
super()

T
tuple()
type()

V
vars()

Z
zip()

_
__import__()
