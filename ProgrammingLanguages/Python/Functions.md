## 内建函数

> **[Built-in Functions](https://docs.python.org/3/library/functions.html)**
>
> **[Built-in Types](https://docs.python.org/3/library/stdtypes.html)**

| 函数           | 描述                                                         | 函数定义                                                     |
| -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| `isinstance()` | 检查对象是否为特定类型的实例                                 | **isinstance**(*object*, *classinfo*)                        |
| `getattr()`    | 返回对象对应名称的属性或方法                                 | **getattr**(*object*, *name*)<br/>**getattr**(*object*, *name*, *default*) |
| `hasattr()`    | 名称对应的属性或方法在对象中是否存在                         | **hasattr**(*object*, *name*)                                |
| `setattr()`    | 为对象添加/修改名称对应的属性或方法的值                      | **setattr**(*object*, *name*, *value*)                       |
| `iter()`       | 返回一个迭代器(**iterator**)对象                             | **iter**(*object*)<br/>**iter**(*object*, *sentinel*)        |
| `range()`      | 生成一个不可变的均匀分布的整数序列，[build-in sequence type: range](https://docs.python.org/3/library/stdtypes.html#typesseq-range) | *class* **range**(*stop*)<br/>*class* **range**(*start*, *stop*, *step=1*) |
| `type()`       | 返回对象的类型                                               | *class* **type**(*object*)                                   |
| `type()`       | 返回一个新类型对象，这本质上是`class`语句的动态形式          | *class* **type**(*name*, *bases*, *dict*, ***kwds*)          |
| `bool()`       | 返回布尔值，使用标准真值测试程序转换参数，默认值`False`      | *class* **bool**(*object=False*, */*)                        |
| `float()`      | 返回由数字或字符串构造的浮点数对象，默认值`0.0`              | *class* **float**(*number=0.0*, */*)<br/>*class* **float**(*string*, */*) |
| `int()`        | 返回由数字或字符串构造的整数对象，默认值`0.0`                | *class* **int**(*number=0*, */*)<br/>*class* **int**(*string*, */*, *base=10*) |
|                |                                                              | *class* **str**(*object=''*)<br/>*class* **str**(*object=b''*, *encoding='utf-8'*, *errors='strict'*) |
|                |                                                              |                                                              |
|                |                                                              |                                                              |
|                |                                                              |                                                              |
|                |                                                              |                                                              |
|                |                                                              |                                                              |
|                |                                                              |                                                              |
|                |                                                              |                                                              |

