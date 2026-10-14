

#!/usr/bin/env python2

# 我们通过写下想要的变量名，后跟等号，再跟上想要存储在变量中的值来创建一个变量。例如，下面的行创建了一个名为
# hello_str 的变量，包含字符串 Hello World。
hello_str = "Hello World"

hello_int = 21

hello_bool = True

hello_tuple = (21, 32)

hello_list = ["Hello", "this", "is", "a", "list"]

# 这个列表现在包含 5 个字符串。注意这些字符串之间没有空格
# 如果你想把它们连起来组成一个句子
# 你需要在每个元素之间加上空格。

hello_list = list()
hello_list.append("Hello,")
hello_list.append("this")
hello_list.append("is")
hello_list.append("a")
hello_list.append("list")

# 第一行创建了一个空列表，随后的行使用列表类型的 append
# 函数向列表中添加元素。这种使用列表的方式在处理事先已知的字符串时并不是很有用，但在处理动态数据（如用户输入）时可能很有用。这个列表将用相同的变量名覆盖第一个列表，而不会有任何警告。

hello_dict = {"first_name":"Liam",
              "last_name":"Fraser",
              "eye_colour":"Blue"}

# 让我们访问集合中的一些元素
# 我们先从更改 hello_list 中最后一个字符串的值开始
# 并在末尾添加一个感叹号。"list" 字符串是列表中的第 5 个元素
# 然而，Python 中的索引是从零开始的，这意味着
# 第一个元素的索引是 0。

print(hello_list[4])
hello_list[4] += "!"
# 上一行等同于
# hello_list[4] = hello_list[4] + "!"
print(hello_list[4])

以下行创建了一个名为 hello_int 的整数变量，其值为 21。注意它不需要放在引号中

布尔值也是同样的原理

我们以如下方式创建一个元组

以及以这种方式创建一个列表

你也可以以如下方式创建相同的列表

我们不妨顺便创建一个字典。注意我们已将冒号对齐以使代码整洁

注意，当我们打印该元素时，现在会出现两个感叹号

## TIP
此时，值得解释的是，Python 文件中任何跟在 # 字符后面的文本都将被解释器忽略。这样你就可以在代码中写注释。

> "Python 文件中任何跟在 # 字符后面的文本都将被忽略"

## Get started with Python

记住元组是不可变的，虽然我们可以像这样访问它们的元素

让我们使用 hello_dict 中的数据创建一个句子

更整洁的做法是使用 Python 的字符串格式化

```
print(str(hello_tuple[0]))
# 我们不能像刚才对列表那样更改这些元素的值
# 注意上面使用 str 函数显式地将元组中的整数值转换为字符串后再打印它。
```

```
print(hello_dict["first_name"] + " " + hello_dict["last_name"] + " has " + hello_dict["eye_colour"] + " eyes.")
```

```
print("{0} {1} has {2} eyes.".format(hello_dict["first_name"], hello_dict["last_name"], hello_dict["eye_colour"]))
```

## Control structures

在编程中，控制结构是任何可以改变代码执行路径的语句。例如，一个决定如果数字小于 5 就结束程序的控制结构看起来会像这样：

```
#!/usr/bin/env python2

import sys # 用于 sys.exit 函数

int_condition = 5

if int_condition < 6:
    sys.exit("int_condition must be >= 6")
else:
    print("int_condition was >= 6 - continuing")
```

代码所走的路径取决于整数 int_condition 的值。'if' 块中的代码只有在条件为真时才会被执行。import 语句用于加载 Python 系统库；后者提供了 exit 函数，允许你退出程序并打印错误信息。注意缩进（在本例中每个缩进为四个空格）用于指示代码块属于哪个语句。

'If' 语句可能是使用最频繁的控制结构。其他控制结构包括：

- For 语句，允许你遍历集合中的项目，或重复执行一段代码特定次数；
- While 语句，只要条件为真就会继续的循环。

我们将编写一个程序，从用户接受输入来演示控制结构的工作方式。我们称它为 construct.py

'for' 循环使用当前值的本地副本，这意味着循环内部的任何更改都不会对列表产生影响。另一方面，'while' 循环直接访问列表中的元素，因此如果你想这样做，可以在其中更改列表。我们稍后会更详细地讨论变量作用域。上面程序的输出如下：

## Indentation in detail

如前所述，缩进级别决定了代码块属于哪个语句。缩进在 Python 中是强制性的，而在其他语言中，通常使用大括号集来组织代码块。因此，使用一致的缩进风格至关重要。在 Python 中，通常使用四个空格来表示一个缩进级别。你可以使用制表符，但制表符定义不明确，尤其是在你在一个以上编辑器中打开文件时。

> “‘for’ 循环使用本地副本，因此循环中的更改不会影响列表”

```
[liam@liam-laptop Python]$ ./construct.py
How many integers? acd
You must enter an integer

[liam@liam-laptop Python]$ ./construct.py
How many integers? 3
Please enter integer 1: t
You must enter an integer
Please enter integer 1: 5
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

## More about a Python list

Python 列表类似于其他语言中的数组。列表（或 Python 中的元组）可以包含多种类型的数据，而这在其他语言的数组中通常不是这种情况。因此，我们建议你只在列表中存储相同类型的数据。无论如何，由于列表中数据处理的性质，这几乎总是应该如此。

