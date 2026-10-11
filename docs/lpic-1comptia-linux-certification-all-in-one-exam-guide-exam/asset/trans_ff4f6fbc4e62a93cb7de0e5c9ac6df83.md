

## 从用户读取输入

到目前为止，我们的脚本都是非交互式的，这意味着用户只需在 shell 提示符下输入命令，而脚本则执行其预设的任务。

然而，你可以通过使脚本具备交互性来增加其灵活性，这意味着脚本可以询问用户问题，并捕获他们的输入进行处理。这是通过将之前讨论过的 `echo` 命令与 `read *变量*` 命令结合使用来实现的。`echo` 命令用于向用户展示问题。`read *变量*` 命令用于暂停脚本，在屏幕上显示提示符，并将用户提供的信息读取到你定义的一个变量中。请考虑以下示例：

```bash
#!/bin/bash
#A script for adding a directory to the PATH environment variable
echo "What directory do you want to add to the PATH?"
read MYNEWPATH
echo "You want to add " $MYNEWPATH
exit 0
```

在这个脚本中，用户会被提示输入他或她想添加到 PATH 环境变量中的目录名称。`read` 命令向用户提供了输入目录名称的提示符。当用户按下回车键时，他或她输入的值会被赋名为 MYNEWPATH 的变量。

一旦变量被存储到内存中，`echo` 命令被第二次使用以在屏幕上显示 MYNEWPATH 的值。现在，我们实际上还没有修改 PATH 变量。为了做到这一点，我们需要向 shell 脚本添加更多命令。解决这个问题的最佳方式是问自己：“如果我从 shell 提示符开始做这件事，我需要哪些命令？”然后在脚本中输入这些命令并尝试运行。

在这个例子中，我们需要将用户指定的目录添加到 PATH 中，然后导出 PATH。这可以通过使用本示例中显示的命令来完成：

```bash
#!/bin/bash
#A script for adding a directory to the PATH environment variable
echo "What directory do you want to add to the PATH?"
read MYNEWPATH
echo "Adding the " $MYNEWPATH " directory to PATH."
PATH=$PATH:$MYNEWPATH
export PATH
echo "Your PATH environment variable is now:"
echo $PATH
exit 0
```

如果你做过任何编程，你可能已经注意到我们在脚本的任何地方都没有声明 MYNEWPATH 变量。在许多脚本和编程语言中，你必须先声明变量，设置其大小，并指定它将包含什么类型的信息（文本字符串、实数、整数、布尔值等）。bash shell 稍微宽容一些。bash shell 会通过 `read` 命令动态地在内存中为你创建变量，并将用户的输入分配为其值。

当然，如果你愿意，bash 允许你声明和定义变量类型。这是通过脚本中的 `declare` 命令完成的。如果你希望用户在 `read` 命令中输入数字，这会很有用。这里的问题是，bash shell 将 `read` 命令输入的任何内容都解释为文本，即使用户输入的是数字。请考虑以下脚本：

```bash
#!/bin/bash
#A script that adds variables together.
echo "Enter a number:"
read NUM1
echo "Enter a second number:"
read NUM2
TOT=$NUM1+$NUM2
echo "The sum of these numbers is " $TOT
exit 0
```

运行时，此脚本要求用户输入两个数字，将它们相加并将结果赋名为 TOT 的变量，并在屏幕上回显 TOT 的值。注意图 14-3 中脚本运行时会发生什么。

因为我们没有声明 NUM1、NUM2 或 TOT 变量，bash 将它们都视为简单文本。没有进行算术运算；每个变量的文本值被连接成一个单一的文本字符串。然而，如果我们声明这些变量并将它们定义为整数，情况将大不相同。请看下面这个修订版的脚本：

```bash
#!/bin/bash
#A script that adds variables together.
declare -i NUM1
declare -i NUM2
declare -i TOT
echo "Enter a number:"
read NUM1
echo "Enter a second number:"
read NUM2
TOT=$NUM1+$NUM2
echo "The sum of these numbers is " $TOT
exit 0
```

注意 NUM1、NUM2 和 TOT 在脚本开头使用 `-i`（整数）选项进行了声明。现在 bash shell 会将用户的输入解释为整数，而不是文本。当我们在脚本中变量上使用 `+` 运算符时，它们实际上被相加，而不仅仅是连接，如图 14-4 所示。

### 图 14-3

未声明变量的结果

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_565_0.png)
![](img/fb5404b3ce1e1e1d707f5abc39814a4a_566_0.png)

你做得很好！我们已经从相对简单的脚本过渡到稍微复杂一点的脚本。让我们再进一步，为我们的脚本添加一些控制结构。

## 在脚本中使用控制结构

除了交互性之外，在 shell 脚本中添加控制结构也非常有益。到目前为止，我们的脚本一直是从头到尾顺序执行。这没问题，但如果我们需要脚本做出一些决定呢？基于用户输入或命令输出，你可能希望脚本确定一个行动方向。这是通过在脚本中实现控制结构来完成的。我们将讨论这种脚本元素的以下内容：

- 使用 if/then/else 结构
- 使用 case 结构
- 使用循环结构

让我们从复习 if/then 语句开始。

### 使用 if/then 结构

在 shell 脚本中使用 if/then/else 结构赋予脚本根据特定条件是真还是假来执行不同命令的能力。其结构如下所示：

```bash
if condition then
    commands
else
    commands
fi
```

`if` 部分告诉 shell 确定指定条件是评估为真还是假。如果为真，则执行 `then` 部分下的命令。如果条件评估为假，则执行 `else` 部分下的命令。

例如，在本章的这一部分中，我们一直在处理的脚本中，我们要求用户输入他或她想添加到 PATH 环境变量的目录名称。当我们把目录添加到 PATH 时，shell 并不检查用户输入的目录是否实际存在。运行一个快速测试以验证指定目录是否存在将是有益的。如果存在，我们应该继续将其添加到 PATH 变量中。如果不存在，我们应该在屏幕上发布错误消息，告诉用户发生了什么。下一个示例中显示的脚本正好做了这件事：

```bash
#!/bin/bash
#A script for adding a directory to the PATH environment variable
echo "What directory do you want to add to the PATH?"
read MYNEWPATH
if [ -e "$MYNEWPATH" ]; then
    echo "The $MYNEWPATH" directory exists.
    echo "Adding the "$MYNEWPATH" directory to PATH."
    PATH=$PATH:$MYNEWPATH
    export PATH
    echo "Your PATH environment variable is now:"
    echo $PATH
else
    echo "$MYNEWPATH" doesn't exist."
fi
exit 0
```

在这个例子中，`[ -e "$MYNEWPATH" ]` 条件调用了一个名为 `test` 的实用程序，并指示它检查 MYNEWPATH 变量中包含的目录是否存在（由 `-e` 选项指定）。如果 `test` 返回 TRUE 值，则立即执行 `if` 语句下的步骤。然而，如果 `test` 程序返回 FALSE 值，则执行结构 `else` 部分下的语句。在这种情况下，将显示一条错误消息，指出该目录不存在。当我们运行此脚本并提供一个有效目录时，将显示图 14-5 中的输出。

除了在 if/then/else 结构中使用 `-e` 选项来测试条件外，你还可以直接使用 `test` 命令本身。你可以将以下选项与 `test` 一起使用：

- `-d` 检查指定目录是否存在。
- `-e` 检查指定文件是否存在。
- `-f` 检查指定文件是否存在且是否为常规文件。
- `-G` 检查指定文件是否存在且是否由指定的组拥有。
- `-h` 或 `-L` 检查指定文件是否存在且是否为符号链接。

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_567_0.png)
![](img/fb5404b3ce1e1e1d707f5abc39814a4a_567_1.png)

