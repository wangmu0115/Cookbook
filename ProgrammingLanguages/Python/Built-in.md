> **[Built-in Functions](https://docs.python.org/3/library/functions.html)**
>
> **[Built-in Types](https://docs.python.org/3/library/stdtypes.html)**

### 内建函数

| 函数           | 描述                                                         | 函数定义                                                     |
| -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| `print()` | 将对象打印到文本流文件，以`sep`分隔并后跟`end`，`sep`、`end`、`file`和`flush`必须作为关键字参数给出。默认情况下，输出到控制台 | **print**(**objects*, *sep=' '*, *end='\n'*, *file=None*, *flush=False*) |
| `input()` | 该函数从输入中读取一行，将其转换为字符串并返回（删除尾随换行符） | **input**()<br/>**input**(*prompt*) |
| `isinstance()` | 检查对象是否为特定类型的实例                                 | **isinstance**(*object*, *classinfo*)     |
| `getattr()`    | 返回对象对应名称的属性或方法                                 | **getattr**(*object*, *name*)<br/>**getattr**(*object*, *name*, *default*) |
| `hasattr()`    | 名称对应的属性或方法在对象中是否存在                         | **hasattr**(*object*, *name*)                                |
| `setattr()`    | 为对象添加/修改名称对应的属性或方法的值                      | **setattr**(*object*, *name*, *value*)                       |
| `iter()`       | 返回一个迭代器(**iterator**)对象                             | **iter**(*object*)<br/>**iter**(*object*, *sentinel*)        |
| `range()`      | 生成一个不可变的均匀分布的整数序列，[build-in sequence type: range](https://docs.python.org/3/library/stdtypes.html#typesseq-range) | *class* **range**(*stop*)<br/>*class* **range**(*start*, *stop*, *step=1*) |
| `type()`       | 返回对象的类型                                               | *class* **type**(*object*)                                   |
| `type()`       | 返回一个新类型对象，这本质上是`class`语句的动态形式          | *class* **type**(*name*, *bases*, *dict*, ***kwds*)          |
| `bool()`       | 返回布尔值，使用标准真值测试程序转换参数，默认值`False`      | *class* **bool**(*object=False*, */*)                        |
| `float()`      | 返回由数字或字符串构造的浮点数对象，默认值`0.0`              | *class* **float**(*number=0.0*, */*)<br/>*class* **float**(*string*, */*) |
| `int()`        | 返回由数字或字符串构造的整数对象，默认值`0`                  | *class* **int**(*number=0*, */*)<br/>*class* **int**(*string*, */*, *base=10*) |
| `str()`        | 返回字符串对象，即对象的[build-in text sequence type: str](https://docs.python.org/3/library/stdtypes.html#str)版本 | *class* **str**(*object=''*)<br/>*class* **str**(*object=b''*, *encoding='utf-8'*, *errors='strict'*) |
| `len()`        | 返回对象的长度，即项目数量。参数可以是序列(`str`, `bytes`, `bytearray`, `memoryview`, `tuple`, `list`, `range`)或集合(`dict`, `set`, `frozenset`) | **len**(*s*)                                                 |
|                |                                                              |                                                              |
|                |                                                              |                                                              |
|                |                                                              |                                                              |
|                |                                                              |                                                              |
|                |                                                              |                                                              |
|                |                                                              |                                                              |

