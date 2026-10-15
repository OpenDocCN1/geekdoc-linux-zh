
## 第 6 步
本质上，带有注释的新代码可以是：

```python
# 将 A 的初始值设置为 10
a=10
# 打印 A 的当前值
print("The value of A is,", a)
```

## 第 7 步
你可以用不同的方式使用注释：解释代码部分发生了什么，例如告诉读者你正在做什么：

> # 这是最棒的游戏，它是一群没有睡了几周的 Python 专家创建的。尽管代码非常糟糕，但它至少运行得良好。

## 第 8 步
行内注释是跟在代码行后面的注释。例如，如果你想移除第一条语句，使用：

```python
## print("The value of A is,", a)
```

## 第 9 步
注释，哈希符号也可以用于注释掉你不想执行的代码段。

## 第 10 步
你还可以使用三个单引号在你想注释的区域前后注释掉一个块注释或多行部分：

> # 这是最棒的游戏，它是一群没有睡了几周的 Python 专家创建的。尽管代码非常糟糕，但它至少运行得良好。

# 变量操作

我们在 Python 代码中已经看到了一些变量的示例，但回顾一下它们的运行方式，以及 Python 如何创建并为变量分配特定值，总是值得的。

## 各种变量

在本教程中，你将使用 Python 3 ID Shell。如果你还没有打开，请打开 Python 3 或关闭之前的 IDLE Shell 以清理任何代码。

### 步骤 1
在某些编程语言中，你被要求使用美元符号（`$`）来表示字符串，字符串是由多个字符组成的变量，例如人的姓名。在 Python 中，这并不是必要的。例如，在 Shell 中输入 `name="David Howard"`（或使用你自己的名字，除非你也叫 David Howard）。

```
Python 3.4.2 Shell
File Edit Shell Debug Windows Help
>>> Type "credit" or "license" for more information.
Oct 19 2014, 13:31:11
>>> [GCC 4.8.1] on linux
>>> name="David Howard"
>>> print(name)
David Howard
>>>
```

### 步骤 3
你之前已经看到，可以在变量名之间使用加号符号来连接变量。在我们的示例中，可以使用 `print(name + ":" + title)`。引号之间的中间部分允许我们添加一个冒号和一个空格，因为变量连接是不带空格的，所以我们需要手动添加它们。

```
Python 3.4.2 Shell
File Edit Shell Debug Windows Help
>>> Type "credit" or "license" for more information.
Oct 19 2014, 13:31:11
>>> [GCC 4.8.1] on linux
>>> name="David Howard"
>>> title="Descended from Vikings"
>>> print(name + ":" + title)
David Howard:Descended from Vikings
>>>
```

### 步骤 2
你可以通过发布 `type()` 命令来更改变量的类型，在括号内放置变量名。在示例中，这将是：`type(name)`。添加一个新的字符串变量：`title="Descended from Vikings"`。

```
Python 3.4.2 Shell
File Edit Shell Debug Windows Help
>>> Type "credit" or "license" for more information.
Oct 19 2014, 13:31:11
>>> [GCC 4.8.1] on linux
>>> name="David Howard"
>>> print(name)
David Howard
>>> class str
>>> name="Descended from Vikings"
>>> type(name)
>>>
```

### 步骤 4
你还可以将变量组合在另一个变量中。例如，要将 `name` 和 `title` 组合为一个新变量，我们使用：

```python
character_name = ":" + title
```

然后输出新变量的内容：

```python
print(character)
```

数字以不同的变量形式存储：

`age=44`

`type(age)`

正如我们所知，它们是整数。

![](img/b810837b9059fc96b3c0bd60b035eb13_105_0.png)

### 步骤 5
然而，你不能在同一个命令中组合字符串和整数变量，因为你需要将其中一个转换为另一个，反之亦然。当你尝试组合两者时，你会得到一个错误消息：

```python
print (name + age)
```

```
Python 3.4.2 (default, Oct 19 2014, 13:31:11)
[GCC 4.8.0] Linux
> type "credits" or "license" for more information.
name = "Vikings"
age = 44
print(name)
print(age)
print(type(name))
class 'str'>
print(type(age))
class 'int'>
David Howard Descended from Vikings is 44 years old.
print(name + age)
Traceback (most recent call last):
File "test", line 1, in <module>
    print(name + age)
TypeError: Can't convert 'int' to object str
```

### 步骤 8
当你想要处理用户输入的任务（作为字符串变量和整数）时，这会带来一些问题。例如，你需要：

```python
int(age) + 10
```

这将 `age` 强制转换（TypeCast）为一个可以处理的整数。

```
Edit Shell Debug Options Windows help
Python 3.4.2 (default, Oct 19 2014, 13:31:11)
[GCC 4.8.0] Linux
> type "credits" or "license" for more information.
age = 44
age = input("How old are you?")
print(age + 10)
class 'str
Traceback (most recent call last):
File "test", line 1, in <module>
    print(age + 10)
TypeError: Can't convert 'str' to object int
age = 10
```

### 步骤 6
这种过程被称为类型转换（Typecasting）。代码是：

```python
print ("is " + str(age) + " years old.")
```

或者你可以使用：

```python
print ("is ", age, " years old.")
```

注意，在这种情况下，你不需要在引号单词之间留空格，因为逗号单独处理每个参数。

### 步骤 9
这是在处理带有小数点的数字时使用类型转换的方法。例如，输入：

```python
age=19.99
```

现在输入 `type(age)`，你会发现 Python 将其分配为 'float'，因为包含小数。

```
Edit Shell Debug Options Windows help
Python 3.4.2 (default, Oct 19 2014, 13:31:11)
[GCC 4.8.0] Linux
> type "credits" or "license" for more information.
age = 19.99
print(type(age))
class 'float'
```

### 步骤 7
另一个类型转换示例是提供用户输入的字符串。所有数据都存储为字符串。

### 步骤 10
组合整数和浮点数通常会将整数转换为浮点数，但反过来不是。将浮点数转换为整数时，Python 总是向下取整到最近整数；在 19.99 的情况下，它变成了 19。

```
Edit Shell Debug Options Windows help
Python 3.4.2 (default, Oct 19 2014, 13:31:11)
[GCC 4.8.0] Linux
> type "credits" or "license" for more information.
age = 19.99
print(int(age))
class 'int'
```

## 用户输入

我们之前已经通过代码看到了一些基础的用户交互，所以现在是时候专注于如何从用户那里获取信息并将其展示了。

## 用户友好

你从用户那里获取输入的类型很大程度上取决于你编写的程序类型。例如，游戏可能会询问名字，数据库可能会询问个人详情。

### 步骤 1
如果还没有打开，打开 Python 3 Shell 并在编辑器中新建一个文件。让我们从非常简单的开始，输入：

```python
print("Hello")
firstname=input("What is your first name?")
print("Thanks")
surname=input("And what is your surname?")
```

![](img/b810837b9059fc96b3c0bd60b035eb13_107_0.png)

### 步骤 2
保存并执行代码，正如怀疑，IDLE 程序将询问你的名字并存储为 `firstname`，然后询问你的姓；将其存储在变量 (`surname`) 中：

### 步骤 3
现在我们已经将姓名存储在两个变量中，我们可以随时调用它们：

```python
print("Welcome", firstname, ". I hope you're well today.")
```

![](img/b810837b9059fc96b3c0bd60b035eb13_107_1.png)

### 步骤 4
运行代码你会发现一个小问题，姓氏后面跟着一个空格。为了消除这个问题，你可以在代码末尾添加加号：

```python
print("Welcome", firstname, surname+". I hope you're well today.")
```

![](img/b810837b9059fc96b3c0bd60b035eb13_107_2.png)

![](img/b810837b9059fc96b3c0bd60b035eb13_107_3.png)

## 用户输入

### 步骤 5
你不总是要在 `input` 命令中包含引号文本。例如，你可以询问姓名，并在下面的行中使用输入：

### 步骤 8
你在这里创建一个条件，我们将使用它。简而言之，我们使用用户的输入并对其条件进行衡量。因此，如果用户输入 David 作为名字，卫兵将允许他们不受惩罚地通过。否则，如果他们输入任何非 David 的名字，卫兵将挑战他们战斗。

```python
print("Hello. What is your name?")
name=input()
```

![](img/b810837b9059fc96b3c0bd60b035eb13_108_0.png)

上一步的代码通常被认为比在 `input` 命令中有大量文本要好一点，但这不是铁成不变的规则，所以在此情况下请随你的意愿操作。扩展这段代码如下：

### 步骤 9
正如你之前学到的，来自用户的任何输入都是字符串，所以你需要应用类型转换将其转换为其他形式。这为 `input` 命令创建了有趣的添加。例如：

```python
print("Hail! Who goes there?")
name=input()
```

# 计算速度和距离

```python
print("Input a rate and a distance")
```

```python
rate=float(input("Rate: "))
```

![](img/b810837b9059fc96b3c0bd60b035eb13_108_1.png)

### 步骤 7
这也许是文字冒险游戏的良好开始，不是吗？现在你可以扩展它并使用原始输入来稍微丰富游戏：

### 步骤 10
要完成速度和距离，我们可以：
`distance=float(input("Time: "))`
`rate=(distance / rate)`

```python
if name=="David":
    print("Welcome, good sir. You may pass.")
else:
    print("I know you not. Prepare for battle!")
```

保存并执行并输入一些数字。使用 `float` 元素，我们将告诉 Python 输入的内容是浮点数而不是字符串。

![](img/b810837b9059fc96b3c0bd60b035eb13_108_2.png)

Linux 编码与编程 109

## 创建函数

现在你已经掌握了变量和用户输入的使用，下一步是攻克函数。你已经使用过一些函数，例如 `print` 命令，但 Python 允许你定义自己的函数。

## 奇妙函数

函数是你输入到 Python 中执行某些操作的命令。它是一段自成体系的代码，接收数据、对其进行处理，然后返回结果。

### 步骤 1
函数处理的不仅仅是数据。它们可以执行从一种格式到另一种格式的各种操作，并检查项目的长度或类型。例如，函数是一个后面跟着括号的短单词。例如，`len()` 或 `type()`。

### 步骤 2
函数接收数据（使用变量），根据函数的程序编写方式对其进行处理，并返回值。被处理的数据位于括号内，因此，如果你想知道 `disestablishmentarianism` 这个单词中有多少个字母，你可以使用：`len("disestablishmentarianism")`，它将返回数字 28。

### 步骤 3
你可以以类似的方式通过函数传递变量。假设你想知道一个人姓氏的字母数量，可以使用以下代码（请为此示例进入文本编辑器）：

```python
name=input("Enter your surname: ")
print("Your surname has", count, "letters in it.")
```

### 步骤 4
Python 内置了数十个函数，由于此处空间有限，无法全部列出。然而，要查看 Python 3 可用的内置函数列表，请导航至 `docs.python.org/3/library/functions.html`。这些是预定义函数，但用户创建了更多，它们并不是唯一的可用函数。

## 创建函数

### 步骤 5
可以通过模块（`modules`）向 Python 添加额外的函数。Python 拥有一系列编程任务。它们添加函数并可以在需要时导入。例如，要使用数学函数：

### 步骤 6
要使用模块中的函数，输入模块名称后跟一个点号，例如，使用 Math 模块，你刚刚将其导入 Python，你就可以利用平方根函数。操作如下：

```python
import math
```

输入后，你就可以使用 Math 模块的所有函数了。

```python
math.sqrt(16)
```

当你看到代码呈现为：`function(data):` 时：

## 锻造函数

你可以导入其他 Python 程序员导入许多不同的函数，未来会有更多优秀的示例：你也可以用 `def` 命令创建一个。

### 步骤 1
选择 `File -> New File` 进入编辑器，创建一个名为 `Hello` 的函数，它会问候用户。

### 步骤 3
要修改它，删除 `Hello("David")` 这一行（脚本的最后一行），并按 `Ctrl+S` 保存新脚本。选择 Editor 并创建一个新文件（`File -> New File`）。输入：

```python
def Hello():
    print("Hello")
```

从 Hello 导入：

```python
Hello("David")
```

按 `F5` 保存并运行脚本。你将在 Shell 中看到 Hello，输入 `Hello()`，它会返回该函数。

按 `F5` 保存并执行代码。

### 步骤 2
让我们扩展函数以接受一个变量，例如用户的名字。编辑你的脚本为：

### 步骤 4
你所做的是从已保存的 `Hello` 程序中导入该函数，然后使用它来说 Hello。这就是函数和函数的工作方式；尝试一个，并修改它以获得额外积分：

```python
def Hello(name):
    print("Hello", + name)
```

```python
def add(a, b):
    result = a + b
    return result
```

`Hello("David")`
这将接受变量名，否则它将打印 Hello David。在 Shell 中，输入 `name=("Bob")`，然后输入 `Hello(name)`。你可以通过函数传递参数。

## Python 中的条件与循环

条件和循环让程序变得有趣；它们可以是简单的也可以是复杂的，如何使用它们很大程度上取决于程序试图实现的目标；它们可能是游戏中剩余的生命值，或者仅仅是显示倒计时。

## 条件

开始时保持条件简单会让学习编程变得更加愉快。让我们从检查某事是否为真开始，如果是执行其他操作。

### 步骤 1
让我们创建一个新程序，要求用户输入一个单词，然后检查它是否是四字母单词。从 `File > New` 开始，并开始输入变量：

```python
word=input("Please enter a four-letter word: ")
```
