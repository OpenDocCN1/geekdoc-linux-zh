

## STEP 5

你在这里所做的是给字母 a 和 b 分别赋值为 2 和 2。它们现在是变量，可以被 Python 调用以输出、相加、相减、相除等，只要它们的数值保持不变即可。试试这个：

```
print(a)
print(b)
```

![](img/f80199d101da92d953f18eaa6205b48e_94_0.png)

## STEP 6

上一步的输出分别显示了 a 和 b 当前的值，就像你要求分别打印它们一样。如果你想把它们加起来，可以使用以下代码：

```
print(a+b)
```

这段代码只是取出 a 和 b 的值，将它们相加并输出结果。

![](img/f80199d101da92d953f18eaa6205b48e_94_1.png)

## STEP 7

你可以尝试不同种类的变量和 Print 函数。例如，你可以为某人的名字分配变量：

```
name="David"
print(name)
```

![](img/f80199d101da92d953f18eaa6205b48e_94_2.png)

## STEP 8

现在让我们加上姓氏：

```
surname="Hayward"
print(surname)
```

你现在有两个变量，分别包含名字和姓氏，可以独立打印它们。

![](img/f80199d101da92d953f18eaa6205b48e_94_3.png)

## STEP 9

如果我们像之前那样使用 + 符号应用同样的流程，名字在 Shell 中的输出将不会正确显示。试试看：

```
print(name+surname)
```

你需要在两者之间加一个空格，将它们定义为两个独立的值，而不是数学上可以随意操作的。

![](img/f80199d101da92d953f18eaa6205b48e_94_4.png)

## STEP 10

在 Python 3 中，你可以使用逗号在两个变量之间分隔出一个空格：

```
print(name, surname)
```

或者，你也可以自己加上空格：

```
print(name+" "+surname)
```

使用逗号的方式要简洁得多，如你所见。恭喜你，你已经迈出了进入 Python 广阔世界的第一步。

![](img/f80199d101da92d953f18eaa6205b48e_94_5.png)

## Saving and Executing Your Code

虽然在 IDLE Shell 中工作对于小段代码片段来说完全没问题，但它并不适合输入更长的程序列表。在本节中，你将[content]

## STEP 5

你在这里所做的是给字母 a 和 b 分别赋值为 2 和 2。它们现在是变量，可以被 Python 调用以输出、相加、相减、相除等，只要它们的数值保持不变即可。试试这个：

```
print(a)
print(b)
```

![](img/f80199d101da92d953f18eaa6205b48e_94_0.png)

## STEP 6

上一步的输出分别显示了 a 和 b 当前的值，就像你要求分别打印它们一样。如果你想把它们加起来，可以使用以下代码：

```
print(a+b)
```

这段代码只是取出 a 和 b 的值，将它们相加并输出结果。

![](img/f80199d101da92d953f18eaa6205b48e_94_1.png)

## STEP 7

你可以尝试不同种类的变量和 Print 函数。例如，你可以为某人的名字分配变量：

```
name="David"
print(name)
```

![](img/f80199d101da92d953f18eaa6205b48e_94_2.png)

## STEP 8

现在让我们加上姓氏：

```
surname="Hayward"
print(surname)
```

你现在有两个变量，分别包含名字和姓氏，可以独立打印它们。

![](img/f80199d101da92d953f18eaa6205b48e_94_3.png)

## STEP 9

如果我们像之前那样使用 + 符号应用同样的流程，名字在 Shell 中的输出将不会正确显示。试试看：

```
print(name+surname)
```

你需要在两者之间加一个空格，将它们定义为两个独立的值，而不是数学上可以随意操作的。

![](img/f80199d101da92d953f18eaa6205b48e_94_4.png)

## STEP 10

在 Python 3 中，你可以使用逗号在两个变量之间分隔出一个空格：

```
print(name, surname)
```

或者，你也可以自己加上空格：

```
print(name+" "+surname)
```

使用逗号的方式要简洁得多，如你所见。恭喜你，你已经迈出了进入 Python 广阔世界的第一步。

![](img/f80199d101da92d953f18eaa6205b48e_94_5.png)

## Saving and Executing Your Code

虽然在 IDLE Shell 中工作对于小段代码片段来说完全没问题，但它并不适合输入更长的程序列表。在本节中，你将了解到 IDLE 编辑器，从现在开始你将在其中工作。

## EDITING CODE

你最终会达到必须停止向 Shell 输入单行代码的阶段。相反，IDLE 编辑器将允许你保存和执行 Python 代码。

## STEP 1

首先，打开 Python IDLE Shell，打开后点击 File > New File。这将打开一个名为 Untitled 的新窗口。这就是 Python IDLE 编辑器，你可以在其中输入创建未来程序所需的代码。

![](img/f80199d101da92d953f18eaa6205b48e_95_0.png)

## STEP 3

你可以看到 IDLE 编辑器中的颜色编码与 Shell 中的相同，有助于你更好地理解代码的运行情况。然而，要执行代码，你需要先保存它。按下 F5 就会弹出一个 Save... 对话框。

![](img/f80199d101da92d953f18eaa6205b48e_95_1.png)

## STEP 2

IDLE 编辑器本质上是一个简单的文本编辑器，具有 Python 功能、颜色编码等；与 Sublime 类似。你可以像在 Shell 中一样输入代码，例如，取自上一教程的示例，输入：

```
print("Hello everyone!")
```

![](img/f80199d101da92d953f18eaa6205b48e_95_2.png)

## STEP 4

点击 Save 对话框中的 OK 按钮并选择保存所有 Python 代码的目的地。目的地可以是一个名为 Python 的专用文件夹，也可以随意放置。记住要保持磁盘整洁，以方便日后使用。

![](img/f80199d101da92d953f18eaa6205b48e_95_3.png)

## STEP 5

为你的代码输入一个名称，例如 'print hello'，然后点击 Save 按钮。一旦 Python 代码保存，它就会被执行，输出将显示在 IDLE Shell 中。在本例中，就是 'Hello everyone!'。

![](img/f80199d101da92d953f18eaa6205b48e_96_0.png)

## STEP 6

这就是绝大多数 Python 代码的执行方式。将其输入编辑器，按下 F5，保存代码，然后在 Shell 中查看输出。有时情况会有所不同，取决于你是否请求单独的窗口，但本质上这就是流程。除非另有说明，否则本书中将使用此流程。

![](img/f80199d101da92d953f18eaa6205b48e_96_1.png)

## STEP 7

如果打开保存的 Python 代码的文件位置，你会看到它以 .py 扩展名结尾。这是默认的 Python 文件名。你创建的任何代码都将是 whatever.py，从众多互联网 Python 资源站点下载的代码也将是 .py。只需确保代码是为 Python 3 编写的。

![](img/f80199d101da92d953f18eaa6205b48e_96_2.png)

## STEP 8

让我们扩展代码并输入一些来自上一教程的示例：

```
a=2
b=2
name="David"
surname="Hayward"
print(name, surname)
print(a+b)
```

现在按下 F5，你会被要求再次保存文件，因为它与之前不同。

![](img/f80199d101da92d953f18eaa6205b48e_96_3.png)

## STEP 9

如果点击 OK 按钮，文件将使用新的代码条目覆盖并执行，输出显示在 Shell 中。对于这几行来说不是问题，但如果你编辑的是更大的文件，覆盖可能会成为问题。相反，使用编辑器中的 File > Save As 来创建备份。

![](img/f80199d101da92d953f18eaa6205b48e_96_4.png)

## STEP 10

现在创建一个新文件。关闭编辑器，并从 Shell 打开一个新实例（File > New File）。输入以下内容并保存为 hello.py：

```
a="Python"
b="is"
c="cool!"
print(a, b, c)
```

你将在下一教程中使用这段代码。

![](img/f80199d101da92d953f18eaa6205b48e_96_5.png)

## Executing Code from the Terminal

虽然我们全书都使用 GUI IDLE 工作，但值得了解一下 Python 的命令行处理。我们已经知道有 Python 的命令行版本，但它也用于执行代码。

## COMMAND THE CODE

使用我们在上一教程中创建的代码，即我们命名的 hello.py，让我们看看如何从命令行级别运行在 GUI 中制作的代码。

## STEP 1

在 Linux 中，Python 提供了两种通过命令行执行代码的方式。其中一种使用 Python 2，另一种使用 Python 3 库等。首先，切换到操作系统的命令行或终端。

![](img/f80199d101da92d953f18eaa6205b48e_97_0.png)

## STEP 3

现在你在命令行中，我们可以启动 Python。对于 Python 3，你需要输入命令 python3 并按 Enter。这会将你带入命令行版本的 Shell，光标为熟悉的三个右向箭头（>>>）。

![](img/f80199d101da92d953f18eaa6205b48e_97_1.png)

## STEP 2

正如之前一样，我们使用的是 Raspberry Pi。Windows 用户需要点击开始按钮并搜索 CMD，然后点击搜索返回的命令行；macOS 用户可以通过点击 Go > Utilities > Terminal 来访问命令行。

![](img/f80199d101da92d953f18eaa6205b48e_97_2.png)

## STEP 4

从这里你可以输入之前查看过的代码，例如：
a=2
print(a)

你可以看到它工作得完全一样。

![](img/f80199d101da92d953f18eaa6205b48e_97_3.png)

## Executing Code from the Terminal

## STEP 5

现在输入：exit() 以离开命令行 Python 会话并返回到命令提示符。进入保存上一教程代码的文件夹并列出其中的可用文件；你应该能看到 hello.py 文件。

![](img/f80199d101da92d953f18eaa6205b48e_98_0.png)

## STEP 8

从 Python 2 命令行运行 Python 3 代码的结果是显而易见的。虽然不会以任何方式报错，但由于 Python 3 与 Python 2 处理 Print 命令的方式不同，结果与我们预期不符。暂时使用 Sublime 打开 hello.py 文件。

![](img/f80199d101da92d953f18eaa6205b48e_98_1.png)

## STEP 6

在你要运行代码的同一文件夹中，在命令行输入以下内容：
python3 hello.py
这将执行我们创建的代码，提醒你一下，它是：

```
a="Python"
b="is"
c="cool!"
print(a, b, c)
```

![](img/f80199d101da92d953f18eaa6205b48e_98_2.png)

## STEP 9

由于 Sublime Text 不适用于 Raspberry Pi，你将暂时离开 Pi，使用 Sublime 作为示例，说明你不一定需要使用 Python IDLE。使用 hello.py 文件将其修改为包含以下内容：

```
name=input("What is your name? ")
print("Hello,", name)
```

![](img/f80199d101da92d953f18eaa6205b48e_98_3.png)

## STEP 7

自然地，由于这是 Python 3 代码，使用 Python 3 独有的语法和布局，它只有在使用 python3 命令时才有效。如果你愿意，可以尝试用 Python 2 输入：
python hello.py

![](img/f80199d101da92d953f18eaa6205b48e_98_4.png)

## STEP 10

保存 hello.py 文件并返回到命令行。现在使用以下命令执行新保存的代码：
python3 hello.py
结果将是原来的 Python is cool! 语句，加上新增的 input 命令，要求你输入名字，并在命令行窗口中显示它。

![](img/f80199d101da92d953f18eaa6205b48e_98_5.png)

