
现在你已经使用了 Python 中大部分实用的功能，下一步是处理函数。你已经用过一些函数，例如 `print` 命令，但 Python 允许你定义自己的函数。

- **步骤 1** 函数处理的不仅仅是数据。它们可以做事情：排序数据、将项目从一种格式转换为另一种格式，以及检查项目的长度或类型。基本上，函数是一个紧跟在括号后面的短单词。例如，`len()`、`list()` 或 `type()`。

- **步骤 3** 你可以用同样的方式通过函数传递变量。假设你想知道一个人姓氏的字母数量，你可以使用以下代码（为此示例进入文本编辑器）：

```python
name=input("Enter your surname: ")
count=len(name)
print("Your surname has", count, "letters in it.")
```

## 创建函数

现在你已经使用了 Python 中大部分实用的功能，下一步是处理函数。你已经用过一些函数，例如 `print` 命令，但 Python 允许你定义自己的函数。

**修订后的逻辑流：**
1. 用户输入
2. 创建函数
3. 奇妙函数
4. 创建函数（重复）
5. 锻造函数
6. 条件与循环

# 第 5 章

按下 `F5` 并保存代码以执行。在 Shell 中输入一个四个字母的单词开始，你应该会收到返回消息，该单词是四个字母。现在再次按 `F5` 运行程序，这次输入五个字母的单词。Shell 将显示它不是四个字母单词。

```python
import random

word = random.choice('abcdefghijklmnopqrstuvwxyz')

print("copyright" or "liceless" for more information.")

if len(word) == 4:
    print("word is a four-letter word.")
    print(word)
elif len(word) == 3:
    print("word is a three-letter word. Try again.")
else:
    print("is not a four-letter.")
```

# 第 6 章

现在扩展代码以包含另一个条件。最终它可能会变得非常复杂。我们添加了一个三个字母单词的条件：

```python
word=input("Please enter a four-letter word: ")
if len(word) == 4:
    print("is a four-letter word. Well done.")
elif len(word) == 3:
    print("is a three-letter word. Try again.")
else:
    print("is not a four-letter word.")
```

# 循环

循环看起来和条件非常相似，但它们在操作上有所不同。循环会运行相同的代码块多次，通常在条件的支持下。

# 第 1 章

让我们从简单的 `while` 语句开始。如果，这将检查某内容是否为真（TRUE），那么缩进的代码：

```python
x = 0
while x < 10:
    print(x)
    x = x + 1
```

# 第 3 章

`for` 循环是另一个例子。`for` 用于遍历一组范围内的数据，变量列在方括号中。

```python
words=["Cat", "Dog", "Unicorn"]
for word in words:
    print(word)
```

# 第 2 章

`if` 和 `while` 的区别在于 `while` 的缩进代码它会返回并检查语句是否仍然为真。在示例中，如果 `x`，则打印 `x` 的当前值，然后将值加 1。当 `x` 等于 10 时，它会循环。

# 第 4 章

`for` 循环也可以在倒计时示例中使用 `range` 函数。

```python
for x in range(10, 0, -1):
    print(x)
```

这里不需要 `x+=1`，因为 `range` 函数在第一个数字和最后一个数字之间创建了一个列表。

# Python 模块

我们之前提到过模块（`Math` 模块），但由于模块是充分利用 Python 优势的重要组成部分，值得花更多一点时间在它们上。

## 精通模块

将模块想象成你 Python 代码的扩展，以增强其功能。正如我们所见，有无数模块可用，你也可以编写自己的模块。虽然 Python 内置函数是有限的，但使用模块允许我们编写更复杂的程序。如你所知，模块是会被导入的 Python 脚本，例如 `math`。要安装模块，我们可以使用 `PIP`。关闭 IDLE Shell 进入命令提示符，输入：

```bash
pip install pygame
```

某些模块（特别是在树莓派上）是默认包含的，其他模块并不可用。非树莓派平台上的很好的例子是 `Pygame` 模块，它包含许多创建游戏的函数。尝试：

```bash
pip install pygame
```

结果是 IDLE 中的一个错误：

```python
>>> import pygame
>>> import traceback
>>> traceback.print_exc()
File line 1, in <module>
ModuleNotFoundError: No module named 'pygame'
```

```bash
Administrator: Command Prompt
Microsoft Windows [Version 10.0.15063]
(c) Microsoft Corporation. All rights reserved.
C:\Users\david>pip install pygame
Collecting pygame
  Downloading pygame-1.9.6-cp36-win32.whl
Installing collected packages: pygame-1.9.6-cp36-win32.whl
Successfully installed pygame-1.9.6
C:\WINDOWS\system32>
```

关闭命令提示符并重新启动 IDLE Shell。现在当你输入 `pygame`，模块将无问题地导入到代码中。你会发现，大多数从网上复制的代码都会包含一个模块，缩进的缺失通常是执行时错误的根源。

你的代码中可以导入多个模块。为了扩展我们的示例，使用：

```python
import random
import math
for i in range(5):
    print(random.randint(1, 25))
print(math.pi)
```

模块包含了在你自己的代码中实现某些结果所需的额外代码，正如我们之前实验的那样。例如：

```python
import random
```

引入了来自随机数生成器的代码。你可以用它创建类似这样的：

```python
for i in range(10):
    print(random.randint(1, 25))
```

结果是一串数字，随后是从 `Math` 模块中提取的 Pi 值。你也可以使用 `import` 和 `from` 命令从模块中提取函数，例如：

```python
from random import randint
for i in range(5):
    print(randint(1, 25))
```

这段代码在保存并执行时将显示 1 到 25 之间的随机数。你可以尝试显示更多，或者来自更大或更小的范围。例如：

```python
import random
for i in range(25):
    print(random.randint(1, 100))
```

这有助于创建更精简的编程方法。你也可以导入模块 `*`，这将导入该模块中的所有内容。

```python
import math as m
print(m.pi)
```
