
```python
print("{0} {1} {2}".format(hello_dict["first_name"],
                            hello_dict["last_name"],
                            hello_dict["eye-colour"]))
```

![](img/f16311c48f0c39ab87b1836be5339b9e_13_0.png)

## 详细缩进

正如前面提到的，缩进级别决定了代码块属于哪个。在 Python 中缩进是强制的，而在其他语言中，使用大括号来组织块。由于这个原因，使用一致的缩进至关重要。你可以使用制表符，但如果在多个编辑器中打开文件，那么制表符的定义并不清晰。

![](img/f1836be5339b9e_14_0.png)

## 控制结构

在编程编程中，控制结构是指任何可以改变代码执行路径的语句。例如，一个如果数字小于 5 就结束程序的控制结构看起来像这样：

```python
#!/usr/bin/env python2
import sys
int_condition = 5
if int_condition < 6:
    sys.exit("int_condition must be >= 6")
else:
    print("int_condition was >= 6")
```

代码路径取决于整数 `int_condition` 的值。其他控制结构包括以下项目，你在使用 Python 时应该注意：

- For 语句：允许你遍历集合中的项，或按次数重复一段代码
- While 语句：当条件为真时持续的循环

我们将编写一个接受用户输入的程序，以演示控制结构的工作原理。我们将列表命名为 `construct.py`。`for` 循环使用当前值的局部副本，这意味着循环内部的任何更改都不会影响列表。另一方面，`while` 循环是直接访问列表中的元素，因此你会希望这样做。我们将在文章稍后部分更详细地讨论变量作用范围。程序如下：

```
$ liam@liam-laptop$ ./construct.py
How many integers? acd
You must enter an integer

$ liam@liam-laptop$ ./construct.py
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

![](img/f16311c48f0c39ab87b1836be5339b9e_15_0.png)

# Python 入门

## 入门

### 代码列表

```python
#!/usr/bin/env python2

# 我们将编写一个程序，要求用户
# 输入任意数量的整数，将它们存储在集合中，
# 然后演示如何使用各种控制
# 结构来使用该集合。

import sys # 用于 sys.exit 函数
target_int = raw_input("How many integers?")

# 此时，变量 target_int 包含了用户
# 输入的任何内容的字符串表示。我们需要尝试
# 将其转换为整数，但要准备好在如果它不是整数时
# 处理错误。
# 否则程序将
# 崩溃。
try:
    # 用于存储整数的列表
    target_int = int(target_int)
except ValueError:
    # sys.
    sys.exit("You must enter an integer")

ints = list()

count = 0
```

- 我们希望在列表中拥整数数量
- 用于存储整数的列表
- 这些用于跟踪我们目前拥有多少个整数

![](img/f16311c48f0c39ab87b1836be5339b9e_16_0.png)

## 入门

如果上述操作成功，则 `isint` 将被设置为 `true`：`isint=True`

```python
## 继续询问整数，直到我们达到
# 要求的数量
while count < target_int:
    line = raw_input("Please enter integer (): ".format(count + 1))
    isint = False
    try:
        new_int = int(line)
    except:
        print("You must enter an integer")
```

此时，用户已经放弃了，或者我们已经有一个满了整数的列表。我们可以通过两种方式遍历这些整数。第一是使用 `for` 循环

```python
## 只有当我们有一个整数时才继续。否则，
# 我们将再次循环
# 注意下面我使用了 ==，这与
# == 不同。单等号是
# 赋值运算符，而双等号是比较运算符。
```

```python
if isint == True:
    # 将整数添加到集合中
    ints.append(new_int)
    # 计数加 1
    count += 1
```

```python
print("Using a for loop")
for value in ints:
    print(str(value))
```

```python
# 或者使用 while 循环：
print("Using a while loop")
# 我们已经有了上面的总数，但知道
```

![](img/f16311c48f0c39ab87b1836be5339b9e_17_0.png)

## Python 列表

Python 列表类似于其他语言中的数组。Python 列表（或元组）可以包含不同的数据类型，这在其他语言的数组中通常是不可能的。由于这个原因，我们建议你只在列表中存储相同类型的数据。由于列表中数据处理方式的性质，几乎在所有情况下都是如此的。

![](img/f16311c48f0c39ab87b1836be5339b9e_18_0.png)

## 函数和变量作用域

编程中的函数用于将过程分解成更小的部分。这通常会让代码变得更易读。如果设计得当，函数还可以被复用。函数可以接收传递的变量。Python 中的变量始终通过值传递，这意味着变量的副本被传递给函数，该副本仅在函数作用域内有效。在函数内部对原始变量的任何更改都将被丢弃。然而，函数也可以返回值，所以这不是问题。函数使用关键字 `def` 定义，后面紧跟函数名。任何可以传递的变量都在函数名后的括号中。多个变量之间用逗号分隔。在这些括号中变量的名称就是它们在函数作用域内的名称，无论传递给函数的变量被称为什么。

让我们来看一下实际操作。对应的程序程序输出如下：

> “函数使用关键字 `def` 定义，然后是函数名”

![](img/f16311c48f0c39ab87b1836be5339b9e_18_1.png)

## 入门

```python
#!/usr/bin/env python2 # 下面是一个名为 modify_string 的函数，它接受一个变量
## 该变量在函数作用域内被称为 original。在函数定义下方缩进 4 个空格的内容都是
# 作用域：
def modify_string(original):
    original += " that has been
    modified."
# 目前，只有此字符串的本地副本被修改了

def modify_string_return(original):
    original += " that has been
    modified."
# 然而，我们可以将本地副本返回给调用者
```

此时，用户已经放弃了，或者我们已经有一个满了整数的列表。我们可以通过两种方式遍历这些整数。第一是使用 `for` 循环

```python
## 只有当我们有一个整数时才继续。否则，
# 我们将再次循环
# 注意下面我使用了 ==，这与
# == 不同。单等号是
# 赋值运算符，而双等号是比较运算符。
```

```python
if isint == True:
    # 将整数添加到集合中
    ints.append(new_int)
    # 计数加 1
    count += 1
```

```python
## len 函数非常
# 有用。
total = len(ints)
count = 0
while count < total:
    print(str(ints[count]))
    count += 1
```
