
### 16.3.3 Functions

Python 提供了一种称为函数的编程构造，允许你定义自己的命名过程，并在代码中以模块化方式重用这些过程。你可以将函数视为一个黑盒机器，它将函数调用或调用前存在的命名对象作为输入，在黑盒内部使用只能在黑盒内部看到的名称进行处理，然后通过赋值语句将它们作为命名对象吐出，供 Python 程序使用。

函数定义的一般形式是：

```
def name (formal parameters):
    body of the function
    return (returned parameters)
```

TABLE 16.3 Python 2.7.X Keywords

| and | del | from | not | while |
| as | elif | global | or | with |
| assert | else | if | pass | yield |
| break | except | import | print | |
| class | exec | in | raise | |
| continue | finally | is | return | |
| def | for | lambda | try | |

其中 `name` 是你给函数的名字（确保你没有使用 Python 关键字），“形式参数”是传递给函数以便它对其执行某些操作的命名对象，并且可选地，“返回参数”是被你的程序使用的命名对象。

你可以使用三种基本方式执行函数：

- 1. 使用方式 1（交互模式），并在 Python 命令行提示符下的解释器中输入或复制粘贴函数定义中的每一行代码。
- 2. 使用方式 2（脚本模式），并在具有 `.py` 扩展名的文件中创建函数定义。然后在 shell 提示符下以函数定义文件名加扩展名作为 Python 命令的参数运行 Python。
- 3. 使用方式 3（导入脚本模式），并导入一个文件（有时称为模块），你已用文本编辑器创建并包含函数定义，将其导入到当前 Python 会话中。然后你可以在该文件中使用的函数定义和命名对象。

使用函数定义在 Python 中使用第一种方式的简单示例如下。在 Python 命令提示符下输入以下七行 Python 代码。省略号（`...`）是另一种形式的 Python 提示符，要求输入更多命令行。记住要缩进所示的行，并在每行后按键盘上的 `<Enter>`。

```
>>> w = 7
>>> x = 12
>>> def add(a, b):
...     c = a + b
...     return (c)
...
>>> z = add(w, x)
>>> z
19
>>>
```

从这个例子中，我们可以称 `w` 和 `x` 为传递给函数定义的实际参数，`a` 和 `b` 为函数定义体中使用的形式参数，`c` 为返回参数。请注意，为了使返回参数在函数定义后在你的 Python 会话的其余部分中使用，你必须将函数调用或调用的右侧的等号左侧分配一个命名变量。

使用方式 3（导入脚本模式）将函数定义带入 Python 的简单示例如下：

使用你选择的文本编辑器在你执行 Python 的当前工作目录中创建以下文件，命名为 `math1.py`：

`cond2` 是一个测试条件，其真值决定是否执行附加的语句块
`else` 是默认情况，执行最后的语句

使用 Way 1（交互模式）在 Python 中使用此结构的简单示例如下（请记住在输入每一行后按下键盘上的 `<Enter>`）。

## Example 16.2

```
>>> x = 1
>>> if x == 0: # the == is a logical, or Boolean operator
    print "x equal 0"
    elif x == 1: #one or more of these optional blocks are
    # allowed
        print "x equal 1"
    else:        #optional block
        print "x is something else"
x equal 1
>>>
```

## EXERCISE 16.3

- 1. 如果在 Example 16.2 中省略 `elif` 块，会打印出什么？
- 2. 如果将第一行改为 `x = 3`，并在 Example 16.2 中省略 `else` 行，会打印出什么？
- 3. 如果在 Example 16.2 中将第一行改为 `x = 1.8`，会打印出什么？

也可以将条件执行块嵌套在彼此内部。例如：

## Example 16.3

```
>>> w = 36
>>> y = 13
>>> z = 20
>>> if w < 37:
...     print "w is less than 37"
...     if y > 13:
...         print "y is greater than 13"
...     elif y == 13:
...         print "y is equal to 13"
...     else:
...         print "y is less than 13"
...     if z > 21:
...         print "z is greater than 21"
...     elif z == 21:
...     print "z is equal to 21"
...     else:
...         print "z is less than 21"
... else:
...     print "w is greater than or equal to 37"
...
w is less than 37
y is equal to 13
z is less than 21
>>>
```

### 16.3.5 Determinate and Indeterminate Repetition Structures and Recursion

Python 可以以两种基本方式重复程序或脚本文件结构的一部分：通过确定性重复结构或不确定性重复结构。传统上，确定性重复结构称为计数重复，而不确定性重复结构称为逻辑重复。这两种方法分别使用 `for` 过程语句和 `while` 过程语句实现。一般来说，如果你在编写代码时就提前知道想要执行代码块的重复次数，就使用 `for` 语句，如果不知道（例如，当你允许用户在脚本文件运行时输入重复次数时），就使用 `while` 语句。

当然，可以通过不使用特定的结构化编程方法来实现这两种重复方式；例如，通过使用条件执行和非结构化切换来获得相同的结果。但我们选择在 Python 中展示结构化的方法。

确保在 `while` 执行的不确定性重复块中包含的语句体中，继续执行的测试条件会变为假。否则，这将导致无限重复！要停止正在执行的脚本文件的无限重复，请按住键盘上的 `<Ctrl>` 和 `C` 键。

根据 Guido van Rossum 在 Python 语言参考中对 Pythonic 的定义，Python 中的常见技术是使用 `for` 语句遍历可迭代对象的全部元素。许多其他语言都没有这种构造，因此不熟悉 Python 的人有时会改用数值计数器：

```
>>>for i in range(len(money)):
...     print money[i]
```

Pythonic 的方式是：

```
>>>for bills in money:
...     print bills
```

Pythonic 的方式可以被描述为迭代，而传统的语言构造可以被描述为计数。

`for` 结构可以对任何可迭代序列重复执行一组操作，例如字符串、列表、元组或类中的用户定义的可迭代对象。

`for` 语句结构的一般形式是：

```
for a certain number of times
    repeat these statements
```

`while` 结构可以在测试条件为真时重复执行一组操作。

`while` 语句结构的一般形式是：

```
while a certain condition is true
    repeat these statements
```

对象 `K` 是可迭代的，如果它能成功运行以下代码。该代码还显示了传统 `for` 循环结构之类的计数迭代形式可以用 `while` 结构实现（请注意缩进，并在最后一个省略号 `...` 后按 `<Enter>`）：

```
>>>K = [22,33,44,55]                #Lists are iterable.
>>>c = K.__iter__()                #c is the counter
>>>while 1:
...     #execute while true
...     try:
...         item = c.next()            #get the next one
```
