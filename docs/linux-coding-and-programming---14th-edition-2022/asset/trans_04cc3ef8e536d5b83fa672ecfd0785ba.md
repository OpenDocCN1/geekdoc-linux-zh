

## 用户输入

在之前的一些示例中，我们已经看到了一些基本的用户交互代码，所以现在是一个很好的时机，让我们专门关注如何从用户那里获取信息，然后存储并展示这些信息。

### 用户友好

你需要从用户那里获取的输入类型，很大程度上取决于你正在编写的程序类型。例如，游戏可能会询问角色的名字，而数据库可能会询问个人详细信息。

#### 步骤 1

如果尚未打开，请打开 Python 3 IDLE Shell，并在编辑器中开始一个新文件。让我们从非常简单的事情开始，输入：

```python
print("Hello")
firstname=input("What is your first name? ")
print("Thanks.")
surname=input("And what is your surname? ")
```

![](img/d501697c83491ed0bb4b382b0d28ef0a_107_0.png)

#### 步骤 2

保存并执行代码，正如你可能已经猜测的那样，在 IDLE Shell 中，程序会询问你的名（first name），并将其存储在变量 `firstname` 中，然后询问你的姓（surname）；同样存储在另一个变量（`surname`）中。

![](img/d501697c83491ed0bb4b382b0d28ef0a_107_1.png)

#### 步骤 3

既然我们已经将用户的名字存储在几个变量中，我们可以在任何时候调用它们：

```python
print("Welcome", firstname, surname, ". I hope you're well today.")
```

![](img/d501697c83491ed0bb4b382b0d28ef0a_107_2.png)

#### 步骤 4

运行代码后，你会发现一个小问题：姓氏后面的句号前面多了一个空格。为了消除这个问题，我们可以在代码中用加号代替逗号：

```python
print("Welcome", firstname, surname + ". I hope you're well today.")
```

![](img/d501697c83491ed0bb4b382b0d28ef0a_107_3.png)

#### 步骤 5

你并不总是需要在 input 命令中包含带引号的文本。例如，你可以询问用户姓名，并在下一行接收输入：

```python
print("Hello. What's your name?")
name=input()
```

![](img/d501697c83491ed0bb4b382b0d28ef0a_108_0.png)

#### 步骤 6

前一步骤中的代码通常被认为比在 input 命令中包含大量文本更整洁，但这并不是一条固定的规则，因此在这些情况下，你可以随心所欲。扩展该代码，尝试以下内容：

```python
print("Hello! Who goes there?")
name=input()
```

#### 步骤 7

这可能是文字冒险游戏的一个很好的开始，也许？现在你可以进一步扩展，使用用户的原始输入来丰富游戏内容：

```python
if name == "David":
    print("Welcome, good sir. You may pass.")
else:
    print("I know you not. Prepare for battle!")
```

![](img/d501697c83491ed0bb4b382b0d28ef0a_108_1.png)

#### 步骤 8

你在这里创建的是一个条件语句，我们稍后会详细介绍。简而言之，我们正在使用用户的输入并将其与条件进行比较。因此，如果用户输入 David 作为他们的名字，守卫将允许他们通过。否则，如果他们输入的不是 David 的名字，守卫就会向他们发起战斗挑战。

![](img/d501697c83491ed0bb4b382b0d28ef0a_108_1.png)

#### 步骤 9

正如你之前所学，用户的任何输入自动都是字符串，因此你需要应用类型转换（TypeCast）才能将其转换为其他类型。这为 input 命令带来了一些有趣的扩展。例如：

```python
# Code to calculate rate and distance
print("Input a rate and a distance")
rate = float(input("Rate: "))
```

![](img/d501697c83491ed0bb4b382b0d28ef0a_108_2.png)
![](img/d501697c83491ed0bb4b382b0d28ef0a_108_3.png)

#### 步骤 10

为了完成速率和距离的代码，我们可以添加：

```python
distance = float(input("Distance: "))
print("Time: ", (distance / rate))
```

保存并执行代码，然后输入一些数字。使用 `float(input` 元素，我们告诉 Python 输入的任何内容都是浮点数，而不是字符串。

![](img/d501697c83491ed0bb4b382b0d28ef0a_108_4.png)
![](img/d501697c83491ed0bb4b382b0d28ef0a_108_5.png)

## 创建函数

既然你掌握了变量和用户输入的使用，下一步就是处理函数。你已经使用过一些函数，如 `print` 命令，但 Python 允许你定义自己的函数。

### 花哨的函数

函数是你输入到 Python 中执行某项任务的命令。它是一小块独立的代码，接收数据，对其进行处理，然后返回结果。

#### 步骤 1

函数处理的不仅仅是数据。它们在 Python 中可以执行各种有用的操作，例如对数据进行排序、将项目从一种格式更改为另一种格式，以及检查项目的长度或类型。基本上，函数是一个后面跟着括号的简短单词。例如，`len()`、`list()` 或 `type()`。

![](img/d501697c83491ed0bb4b382b0d28ef0a_109_0.png)

#### 步骤 2

函数接收数据（通常是一个变量），对其进行处理并返回最终值。正在处理的数据位于括号内，因此如果你想知道单词 *antidisestablishmentarianism* 中有多少个字母，那么你可以输入：`len("antidisestablishmentarianism")`，数字 28 将作为结果返回。

![](img/d501697c83491ed0bb4b382b0d28ef0a_109_1.png)

#### 步骤 3

你可以以类似的方式通过函数传递变量。假设你想要知道一个人姓氏的字母数，你可以使用以下代码（在此示例中请输入文本编辑器）：

```python
name = input("Enter your surname: ")
count = len(name)
print("Your surname has", count, "letters in it.")
```

按 F5 保存并执行代码。

![](img/d501697c83491ed0bb4b382b0d28ef0a_109_2.png)

#### 步骤 4

Python 内置了数十个函数，由于这里空间有限，无法详尽介绍。然而，要查看 Python 3 可用的内置函数列表，请访问 [www.docs.python.org/3/library/functions.html](https://www.docs.python.org/3/library/functions.html)。这些是预定义的函数，但由于用户创建了许多其他函数，它们并不是唯一可用的函数。

![](img/d501697c83491ed0bb4b382b0d28ef0a_109_3.png)

#### 步骤 5

可以通过模块向 Python 添加更多函数。Python 拥有大量可用的模块，可以涵盖许多编程任务。它们添加函数，并可根据需要随时导入。例如，要使用高级数学函数，请输入：

```python
import math
```

输入后，你可以访问所有 Math 模块函数。

![](img/d501697c83491ed0bb4b382b0d28ef0a_110_0.png)

#### 步骤 6

要使用模块中的函数，请输入模块名称，后跟一个句点，然后是函数名称。例如，使用 Math 模块，由于你刚刚将其导入 Python，你可以利用平方根函数。为此，请输入：

```python
math.sqrt(16)
```

你可以看到代码的格式是 `module.function(data)`。

![](img/d501697c83491ed0bb4b382b0d28ef0a_110_1.png)

### 打造函数

有许多不同的函数可以由其他 Python 程序员创建并供你导入，你无疑在未来会遇到一些优秀的例子；你也可以使用 `def` 命令创建自己的函数。

#### 步骤 1

选择 文件 > 新文件 进入编辑器，让我们创建一个名为 `Hello` 的函数，用于问候用户。输入：

```python
def Hello():
  print("Hello")
Hello()
```

按 F5 保存并运行脚本。你可以在 Shell 中看到 `Hello`，输入 `Hello()` 即可返回新的函数。

![](img/d501697c83491ed0bb4b382b0d28ef0a_110_2.png)

#### 步骤 2

现在让我们扩展该函数以接受一个变量，例如用户的名字。编辑你的脚本使其读取：

```python
def Hello(name):
  print("Hello", name)
Hello("David")
```

现在它将接受变量 `name`，否则它将打印 `Hello David`。在 Shell 中，输入 `name="Bob"` 然后：`Hello(name)`。你的函数现在可以通过它传递变量。

![](img/d501697c83491ed0bb4b382b0d28ef0a_110_4.png)

#### 步骤 3

为了进一步修改，删除 `Hello('David')` 行，即脚本中的最后一行，并按 Ctrl+S 保存新脚本。关闭编辑器并创建新文件（文件 > 新文件）。输入以下内容：

```python
from Hello import Hello
Hello("David")
```

按 F5 保存并执行代码。

![](img/d501697c83491ed0bb4b382b0d28ef0a_110_3.png)

#### 步骤 4

你刚才所做的就是从已保存的 `Hello.py` 程序中导入 `Hello` 函数，然后使用它向 David 打招呼。这就是模块和函数的工作方式：你导入模块，然后使用函数。尝试这个，并修改它以获取额外学分：

```python
def add(a, b):
  result = a + b
  return result
```

![](img/d501697c83491ed0bb4b382b0d28ef0a_110_5.png)

