

## 入门

## 从 Python 入门

提示

此时，值得解释的是，Python 文件中任何跟在 # 字符后面的文本都会被解释器忽略。这样做是为了让你代码中编写注释。

除了这些主要数据类型，还有序列类型（从技术上讲，字符串是一种序列类型，但由于它非常常用，我们将其归为主要数据类型）；

| 类型 | 说明 |
| :--- | :--- |
| List (列表) | 包含特定顺序的数据集合 |
| Tuple (元组) | 包含特定顺序的不可变数据集合 |

元组通常用于坐标之类内容，包含存储为单个变量的 x 和 y 值，而列表通常用于存储更大的集合。存储在元组中的数据是不可变的，因为你无法更改元组中单个元素的值。然而，在列表中你可以做到这一点。

了解 Python 的字典（dictionary）类型也会很有用。字典是一种映射数据类型。这意味着你使用该值对应的键（key）来访问字典中存储的值，这与你使用列表的方式不同。在列表中，你使用元素的索引（表示该元素在列表中位置的数字）来访问列表的元素。

让我们编写一个程序，用来演示如何使用变量和不同的数据类型。此时值得注意的是，在 Python 中你并不总是需要指定数据类型。请在任何你喜欢的编辑器中创建此文件。只要你记得让文件具有可执行性，一切都能正常工作。我们将该文件命名为 variables.py。

![](img/c72194f2c3aec198936695a665a5167c_11_0.png)

## 解释型与编译型语言

| 像 Python 这样的解释型语言是指源代码每次程序运行时都会转换为机器码并执行的语言。 | 这与 C 等编译型语言不同，编译型语言源代码只会被转换为一次机器码——生成的机器码会在每次程序运行时执行。 |

## 从 Python 入门

## 入门

## 完整代码列表

```python
#!/usr/bin/env python2
# 我们通过编写变量名后跟一个等号来创建变量，等号后面跟的是我们想要存储在 # 变量中的值。例如，下面这一行创建了一个名为 hello_str 的变量，包含字符串 Hello World。
hello_str = "Hello World"
hello_int = 21
hello_bool = True
hello_tuple = (21, 32)
```

下一行创建了一个整数变量 hello_int，值为 21。注意它不需要被放在引号中。

同样的原理也适用于元组。我们以如下方式创建元组。

并以这种方式创建列表：

```python
hello_list = ["Hello", "this", "is", "a", "list"]
# 现在这个列表包含 5 个字符串。注意这些字符串之间没有空格，所以如果你想将它们连接成一个句子，你必须在每个元素之间添加空格。
hello_list = list()
hello_list.append("Hello")
hello_list.append("this")
hello_list.append("is")
hello_list.append("a")
hello_list.append("list")
```

也可以通过以下方式创建相同的列表：第一行创建一个空列表，接下来的行使用列表类型的 append 函数向列表中添加元素。在处理高级字符串时，这种使用 # 列表的方法并不真的那么有用，但在处理动态数据（如用户 # 输入）时可能很有用。这个列表将在无任何警告的情况下覆盖第一个列表。

![](img/c72194f2c3aec198936695a665a5167c_12_0.png)

## 入门

## 从 Python 入门

顺便我们也创建一个字典。注意我们对齐下面的冒号以使代码整洁，因为我们使用了之前列表相同的变量名。

```python
hello_dict = { "first_name": "Liam", "last_name": "Fraser", "eye_colour": "Blue" }
```

## 访问集合内部的一些元素

获取 hello_list 中的最后一个字符串并在末尾添加一个感叹号。“list”字符串是列表中的第 5 个元素。然而，Python 中的索引是从0 开始的，这意味着第一个元素的索引为 0。

注意当我们打印该元素时，会有两个感叹号：

```python
print(hello_list[4])
hello_list[4] += "!"
# 上述行等于
hello_list[4] + "!"
print(hello_list[4])
```

记得元组是不可变的，尽管我们可以像这样访问它们的元素：

```python
print(str(hello_tuple[0]))
```

# 我们无法像刚才对列表那样更改这些元素的值
# 注意在上方使用 str 函数是为了在打印之前显式地将元组内部的整数值转换为字符串。

让我们使用 hello_dict 中的数据创建一个句子：

```python
print(hello_dict["first_name"] + " " + hello_dict["last_name"] + " " + hello_dict["eye_colour"])
```

一个更整洁的方法是使用字符串格式化：

```python
print("{0} {1} has {2} eyes".format(hello_dict["first_name"],
  hello_dict["last_name"],
  hello_dict["eye_colour"]))
```

![](img/c72194f2c3aec198936695a665a5167c_13_0)

## 从 Python Python

## 入门

## 缩进详解

如前所述，缩进决定了语句属于哪个块。在 Python 中缩进是强制的，而在其他语言中则使用大括号来组织代码块。通常使用四个空格表示缩进。你可以使用制表符，但制表符并没有很好的定义，尤其是当你打开多个编辑器时。

![](img/c72194f2c3aec198936695a665a5167c_14_0)

## 控制结构

在程序编程中，控制结构是指任何可以改变代码执行路径的语句。例如，一个在数字小于5时结束程序的控制结构看起来如下：

```python
#!/usr/bin/env python2
import sys # 用于 sys.exit 函数
int_condition = 5
if int_condition < 6:
    sys.exit("int_condition must be >= 6")
else:
    print("int_condition was >= 6")
```

代码路径将取决于整数 int_condition 的值。if 块中的代码只有在条件为真时执行。import 语句用于加载系统库；后者提供了 exit 函数，允许退出程序。注意缩进（在这种情况下为每层四个空格）用于指示代码块属于语句。if 语句可能是最常用的结构。其他结构包括你在使用 Python 时应该注意的以下项：

- For 语句，允许你遍历集合中的项，或重复执行某些代码
- While 语句，在条件为真时持续运行的循环

我们将编写一个接受用户输入的程序，以演示控制结构是如何工作的。将其命名为 construct.py。for 循环使用的是当前值的本地副本，这意味着循环内部的任何更改都不会对列表产生影响。然而，while 循环直接访问列表元素，因此如果你需要，可以在那里更改列表。我们将在文章后面的部分更详细讨论变量作用范围。程序如下：

```bash
$liam@liam-laptop Python$ ./construct.py
How many integers? acd
You must enter an integer
$liam@liam-laptop Python$ ./construct.py
How many integers? 3 t
Please enter integer 1: t
You must enter an integer 1: 5
Please enter integer 2: 2
Please enter integer 3: 6
Using a for loop
5
2
6
Using a while loop
5
2
6
```

![](img/c72194f2c3aec198936695a665a5167c_15_0.png)

