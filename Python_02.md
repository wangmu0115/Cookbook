```python
def greeting(first_name, second_name, gender="Male"): 
	"""
	first_name:  姓, string
	second_name: 名, string
	"""
	name = first_name + " " + second_name
	print("Hello, " + name.title() + ".")
	print(name.title + " is " + gender.title() + ".")
```
- **函数**: 带有名字的代码块，用于完成具体的工作
	- 定义: `def $func_name($parameters... #形参): $func_body`
	- 调用: `$func_name($arguments... #实参)`
	- 传递实参
		- *位置实参*: 实参的顺序与形参的顺序相同；`greeting("wang", "mu") # Hello, Wang Mu.`
		- *关键字实参*: 传递给函数的名称—值对，传递顺序无关紧要；`greeting(second_name="mu", first_name="wang") # Hello, Wang Mu.`
		- *形参默认值*: 编写函数时，可以为形参指定默认值，在调用函数中给形参提供了实参时，Python将使用指定的实参值；否则，将使用形参的默认值。
	- 返回值: `return`语句返回一个简单值、列表/元组、字典等
	- 传递任意数量的实参: 