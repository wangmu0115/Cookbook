- `*.py`

- `print()`
- `input($tip_string_message)`, 函数返回值是字符串

- 变量声明: `message = "Hello World"`

- **字符串**: 一组使用双引号或者单引号括起来的字符，例如: `"Hello World"`, `'Hello World'`
	- *`+`*: 字符串拼接，每一项必须都是字符串，例如: `"Hello" + " World"`
	- 方法
		- *`title()`*: 字符串的首字符大写，其余都小写
		- *`upper()`* , *`lower()`*: 字符串中字符都大写/小写
		- *`rstrip()`* , *`lstrip()`*, *`strip()`*: 删除空白字符 
	- 函数
		- *`len($string)`*: 字符串的长度，即字符的数量
		- *`str($object)`*: 将非字符串值表示为字符串

- **数字**: 整数和浮点数
	- 运算符：`+`, `-`, `*`, `/`, `**`(乘方), `%`(模)
	- 函数*`int()`*: 将数字的字符串表示转换为数值表示

- **注释**: 
  - `# 单行注释`

  - *文档字符串（docstring）注释*:  `""" 多行注释 """`, `''' 多行注释 '''`

- **列表**: 由一系列按特定顺序排列的元素组成，例如: `items = ["Remilia", "Hello World", 3.1415926, 42, True]`
  - *索引*访问和修改元素: `items[0]`, `items[1] = "Flandre"`
  - 增
  	- 方法*`append($item)`*: 列表尾部添加元素
  	- 方法*`insert($index, $item)`*: 指定索引位置添加元素
  - 删
  	- 语句*`del $list[$index]`*: 删除列表中指定索引位置的元素
  	- 方法*`pop($index)`*: 删除指定索引位置的元素，并返回该元素
  	- 方法*`remove($value)`*: 从列表中删除*第一个值相等*的元素，结合循环删除所有
  - 排序
  	- 方法*`sort(reverse=$BooleanValue)`*: 永久排序，`reverse=True`是倒序
  	- 函数*`sorted($list, reverse=$BooleanValue)`*: 临时排序，不改变`$list`中元素顺序，`reverse=True`是倒序
  - 函数*`len($list)`*: 返回列表的长度，即列表中元素的数量
  - 方法*`reverse()`*: 反转列表
  - 遍历列表
  	- `for $item in $list:`
  - 函数*`range($from_include, $to_exclude, $step)`*: 生成数字序列
  - 函数*`list($seq)`*: 将一个序列变成列表
  - 函数*`set($seq/$list)`*: 变成一个去重后的无序列表
  - 函数*`max($list)`*, *`min($list)`*, *`sum($list)`*: 列表最大值/最小值/总和
  - **列表解析**: `[$func($value) for $value in $seq]`，示例获取[1,10]的平方列表: `[value ** 2 for value in range(1, 11)]`
  - **切片**: 获取列表的一部分，`$list[$from_index_include, $to_index_exclude]`
  	- 复制列表: `$list[:]`
  - **元组**: 不可变的列表，使用`()`表示，例如：`dimensions = (1, 4, 9)`

- **字典**: 一系列键-值对组成，每个键都有一个值相关联，例如: `dic = {"name": "Remilia", "age": 18}`
  - *键*访问和修改值: `dic["name"]`, `dic["name"] = "Flandre"`
  - 增
  	- *添加键-值对*: 依次指定字典名、用方括号括起的键和相关联的值；例如: `dic["address"] = "ScarletDevilMansion"`
  - 删
  	- 语句*`del $dic[$key]`*: 删除字典中的某个键-值对
  - 遍历字典
  	- 遍历所有的键值对: `for key, value in $dic.items():`
  	- 遍历所有的键: `for key in $dic.keys():`
  	- 遍历所有的值: `for value in $dic.values():`
  - 函数*`len($dic)`*: 返回字典中键-值对的数量
  - *列表*和*字典*的嵌套使用


- **if语句**: `if $cond_expression: $do_something`
	- *布尔值*: `True`, `False`
	- *比较运算符*: `==`, `!=`, `>`, `<`, `>=`, `<=`
	- *逻辑运算符*: `and`, `or` 
	- *判断元素是否在列表中`in`, `not in`*: `if $item in $list:`, `if $item not in $list:`
	- `if $string: $do_something`: 如果字符串非空，则为True，执行后续操作
	- `if`, `if-else`, `if-elif-else`
- **while语句**: 循环运行，直到指定的条件不满足为止，`while $cond_expression: $loop_do_something`
	- *`break`语句*: 退出整个循环
	- *`continue`语句*: 跳过此次循环
