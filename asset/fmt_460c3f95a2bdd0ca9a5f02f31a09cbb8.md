
![](img/92a94ba94656919835b7a50a27c9d9ba_401_3.png)

![](img/92a94ba94656919835b7a50a27c9d9ba_401_4.png)

![](img/92a94ba94656919835b7a50a27c9d9ba_401_5.png)

`xeyes`

`xload`

`xmag`

`xcalc`

# 图 16.8

`xman`应用程序在易于滚动的应用程序窗口中读取手册页。

```
$ @workstation20~$ man
$ 
@workstation20~$ ls
```

![](img/92a94ba94656919835b7a50a27c9d9ba_401_6.png)

# 第 16 小时

在帮助页（Manual Page）窗口中，点击窗口顶部的“Section”按钮来选择帮助页章节，然后从生成的列表中选择你想阅读的帮助页。

# 在 Shell 脚本中与用户交互

在第 9 小“利用 Shell 的力量”中，你学习了如何编写 shell 脚本来在没有用户干预的情况下执行一系列命令。但有时，在 shell 脚本运行时能够获取用户输入也是很有帮助的——例如，允许脚本用户对任务的执行方式做出选择。

在 shell 脚本可以使用 `xmessage` 命令，使脚本通过鼠标与你进行交互。

# 在 Shell 脚本中使用 xmessage

要在脚本中使用 `xmessage`，必须从脚本内部调用它，并带有 `-buttons` 选项和两个参数——一个用逗号分隔的按钮列表，以及应该在按钮上方显示给用户的消息。其格式如下：

```
xmessage -buttons button1,button2,button3 "My Message"
```

这将会在消息下方出现一个带有标记为 `button1`、`button2` 和 `button3` 按钮的对话框。例如，以下对 `xmessage` 的调用将显示图 16.9 所示的对话框：

```
xmessage -buttons "Yes,No" "Would you like some ice cream?"
```

图 16.9

通过调用 `xmessage` 命令创建的对话框。

![](img/92a94ba94656919835b7a50a27c9d9ba_402_0.png)

当用户点击消息下方的按钮之一时，对话框向脚本返回一个值，该值被赋值给特殊变量 `$?`。如果点击了第一个按钮，变量被赋值为 101。如果点击了第二个按钮，变量被赋值为 102，以此此类推。

# xmessage 示例脚本

为了说明 `xmessage` 的用法，学习一些 shell 脚本可能会帮助。这些示例使用了第 9 小学的技术，如果你发现对解释感到困惑，应该在继续之前复习第 9 小时。

# 高级 Linux 桌面使用

假设你想为 `rm` 命令（用于删除文件）创建一个自己的替代方案，在实际删除文件之前通过确认对话框提示用户。列表 16.1 显示了一个名为 `myrm` 的脚本可能的样子，它正是执行此操作。从编辑器开始创建一个 `~/bin/myrm` 文件。输入列表，查看列表，然后逐行检查以它是如何工作的。

# 列表 16.1 myrm 命令的示例脚本

```
#!/bin/sh
xmessage -buttons Yes,No "Remove file $1?"
RESULT=$?

if [ $RESULT -eq 101 ]; then
  rm "$1"
fi
```

这是一个短脚本，执行简单的功能，因此非常容易拆解：

- 第 1 行以 shell 脚本文件的标准头开头。这是 shell 脚本运行所必需的。

- 第 3 行使用 `xmessage` 显示一个带有 Yes 和 No 按钮的对话框。消息简单地词汇化为“Remove file”，后面跟着用户提供的第一个参数，该参数会被替换为 `$1`。

- 第 4 行将特殊变量 `$?` 的值（它包含 `xmessage` 的退出状态）保存到变量 `RESULT` 中。如果点击了第一个按钮，`RESULT` 的值为 101。如果点击了第二个按钮，其值为 102。

- 第 6-8 行检查 `RESULT` 的值是否为 101。如果是，意味着用户点击了按钮，文件被删除。如果不是，则不执行任何操作——脚本直接结束并退出。

要尝试此操作，使用 `chmod` 命令使 `myrm` 可执行：

```
@station$ chmod +x ~/bin/myrm
```

然后，使用该脚本删除文件 `myfile.txt`。输入以下命令将显示图 16.10 所示的对话框：

```
@station$ myrm myfile.txt
```

此时点击 Yes 按钮将导致文件删除。点击 No 按钮将保持文件完好。

第 16 小时

图 16.10

`myrm` 命令显示一个对话框，询问你是否真的想删除提供的作为参数的文件。

![](img/92a94ba94656919835b7a50a27c9d9ba_404_0.png)

# 第二 x xmessage脚本

一个示例可能有助于说明 `xmessage` 更动态的用法。假设你的目录中有一组 `.tex` 文件。如果没有，现在使用 `touch` 命令创建空的 tex 文件以备后用：

```
@station$ touch myfile.txt newfile.txt
```

现在假设你想创建一个脚本，让你通过输入 `texedit` 并使用 `xmessage` 对话框选择文件名来编辑你的任何 tex 文件。启动文本编辑器，并将列表 16.2 输入为 `~/bin/texedit`，然后你来逐行检查它。

# 列表 16.2 texedit 命令的示例脚本

```
#!/bin/sh
xmessage -buttons $(ls -m *.tex) "Which file?"
RESULT=$?
INDEX=100
for TEXFILE in *.tex; do
  INDEX=$(expr $INDEX + 1)
  if [ $RESULT -eq $INDEX ]; then
    emacs $TEXFILE
  fi
done
```

此脚本也相对短，但它的操作比之前的脚本要复杂一些：

- 第 1 行使用 shell 脚本的标准头。再次，这是 shell 脚本运行所必需的。

- 第 3 行使用 `xmessage` 和命令替换来显示工作目录中的所有 tex 文件。这是通过 `ls` 命令使用 `-m` 选项实现的。

- 第 4 行将特殊变量 `$?` 的值（它包含 `xmessage` 的退出状态）保存到变量 `RESULT` 中。如果点击第一个按钮，其值为 101。

- 第 6 行创建一个用于计数的变量。因为点击第一个按钮的结果是 101，我们的计数器从 100 开始。

- 第 7-12 行创建 `for..do` 循环；对于工作目录中的每个 tex 文件执行一次命令；每次 `TEXFILE` 变量都包含一个文件名。

- 第 8 行每次循环时将 `INDEX` 的值加 1；对于第一个 `TEXFILE` 值，`INDEX` 的值为 101；当 `TEXFILE` 再次变化时，`INDEX` 变为 102，以此此类推。

- 第 9-11 行检查 `INDEX` 的值。当它与 `RESULT` 的值相同时，意味着 `TEXFILE` 是用户点击的文件，`emacs` 编辑器使用 `TEXFILE` 作为参数。

让我们看看 16.2 中的脚本。在你保存 `~/bin/texedit` 之后，记得使用 `chmod` 命令使其可执行，以便你可以在命令行调用它：

```
@station$ chmod +x ~/bin/texedit
@station$ texedit
```

当用户在命令行提示符输入 `texedit` 时，将显示 16.2 中的对话框：

```
@station$ texedit
```

图 16.11

`xmessage` 对话框允许用户在工作目录所有的 `.tex` 文件之间进行选择。

![](img/92a94ba94656919835b7a50a27c9d9ba_405_0.png)

点击文件名按钮之一会将文件加载到新的 `emacs` 编辑器窗口。

# Nautilus 文件管理器

你可以通过 Nautilus 文件管理器访问脚本并让它们对选定文件操作。要这样做，在 Nautilus 中选择文件并右键点击以产生你编写的 shell 脚本列表；然后从列表中选择处理选定文件的脚本。在本节中，如果你在跟随示例脚本时遇到困难，可能需要参考第 9 小时。

# 使用 Nautilus 创建和使用 Shell 脚本

要创建供 Nautilus 使用的脚本，请将任何用于 Nautilus 的脚本创建并保存到 `~/.gnome/nautilus-scripts` 目录。

当从 Nautilus 文件管理器调用脚本时，该脚本的行为就像是从命令行调用的一样。

# 高级 Linux 桌面使用

此脚本相当短，也相当简单，但它的运行符合预期。以下是它的工作原理：

- 第 1 行提供了标准的 shell 头部。
