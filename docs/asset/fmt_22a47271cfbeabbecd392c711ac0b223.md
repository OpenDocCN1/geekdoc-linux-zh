
`listbox .list_yscroll .scroll set -relief sunken -width 15 -height 15 -setgrid yes`

这两个组件通过 `pack` 命令创建并放置在窗口中。它们放置在窗口的左侧，并将始终扩展以填充窗口。锚点（anchor）位于窗口的西侧（`w`）。首先放置列表框 `.list`，然后是滚动条 `.scroll`。

```
pack .scroll -side left -fill -anchor w
```

`if then` 检查在调用程序时用户是否输入了参数。测试检查 `argv` 列表中在启用参数的情况下是否存在第一个元素。如果没有参数，则使用由点 `.` 表示的当前目录。该目录被分配给变量 `dir`。然后使用 Tcl 的 `foreach` 操作来填充列表框。通过 `exec` 命令执行 shell 的 `ls` 命令获取文件和目录列表。然后使用 Tk 的 `insert` 操作将每个项目放入 `.list` 组件的列表框中。`insert` 命令接收位置值。在这里，值是存储在 `i` 中的文件名，被放置在列表末尾。

```
.list insert end $i
```

随后将 `CTRL-C` 字符绑定到 `exit` 命令，以便你轻松地关闭窗口。以下是 `mydir1` 程序的列表。

`mydir1`

```bash
#!/usr/bin/wish -f

# 创建滚动条和列表框

scrollbar .scroll -command ".list yview"

listbox .list -yscroll "scroll" -relief sunken -width 15 -height 15 -setgrid yes

pack .list .scroll -side left -fill x -expand -anchor w

# 如果用户输入了目录参数则使用该参数，否则使用当前目录。

if {$argc > 0} then {

    set dir [index $argv 0]

} else {

    set dir ""

}

# 使用从 ls 获取的文件和目录列表填充列表框 (.list)

cd $dir

foreach i [exec ls -a ] {

  if {[file is $i]} {

    .list insert end $i

  }

}

# 为文件管理器设置绑定。Control-C 关闭窗口。

bind all <Control-c> {destroy .}

```

要运行 `mydir1` 程序，首先使用 `chmod` 命令设置执行权限以使其可执行，如下所示：

```bash
chmod 755 mydir1
```

然后，在桌面或窗口管理器的终端窗口中，只需在提示符处输入 `mydir1` 命令即可。你可能需要在它前面加 `./` 以指明当前目录。

```bash
./mydir1
```

将打开一个窗口，其中包含一个 `listbox`，显示了你当前工作目录下的文件列表（见图 1）。使用滚动条显示任何未显示的文件。点击窗口的关闭框即可退出程序。

## 事件与绑定

Tk 程序是事件驱动的。运行时，它会等待事件发生，例如鼠标事件或键盘事件。鼠标事件可以是鼠标点击或双击，或者是鼠标按下或释放。键盘事件可以是 `CTRL` 键或元键（meta key），甚至是输入数据时的回车键。当程序检测到特定事件时，它会采取相应的操作。该操作可以是另一个图形操作（例如显示另一个菜单），也可以是一个 Tcl、Perl 或 shell 程序。

绑定（Bindings）是 Tk 程序的关键运行组件。绑定用于检测驱动 Tk 程序的事件。你可以将 Tk 程序想象成一个无限循环，不断扫描指定事件（绑定）的发生。当它检测到此类事件（如鼠标点击或控制键）时，它会执行绑定到该事件的动作。这些操作可以是任何 T/Tk 命令或系列命令。通常，它们可以执行复杂的操作。完成后，程序将恢复扫描，寻找其他事件，直到被 `exit` 或 `destroy` 强制中断（如通过 `CTRL-C` 绑定执行的那样）。

在文件 `grep` 命令中，甚至是在用 `wc` 统计文件字数时。在每种情况下，你都可以添加自定义的过滤功能。你可以显示每行的部分内容，或者在特定字段中搜索模式，或者只统计大写的单词。这种灵活性允许你使用 Gawk 生成报告、检测数据中的模式并对其进行计算。

你可以直接在 shell 命令行中使用 Gawk，也可以将 Gawk 放置在 shell 脚本中然后执行。实际上，通过 Gawk，你可以定义自己的过滤器。过滤器的名称可以这样理解，因为看待 Gawk 有两种方式：Gawk 本身就是一个过滤器，你可以像调用其他过滤器一样在命令行中调用它；而 Gawk 是一个可编程的过滤器，你可以用它创建自己的过滤器。本节将介绍 Gawk 的这两个方面。我们将首先研究作为过滤器的 Gawk 以及它所有不同的功能。然后，我们将看到如何使用 Gawk 定义你自己的过滤器。

`awk` 工具具有编程语言的所有灵活性和复杂性。Gawk 拥有一组运算符，使其能够进行决策和计算。你还可以声明变量并在结构中使用它们来控制处理行的方式。许多编程特性源自 C 语言语言，并共享相同的语法。这一切使得它成为一个非常强大的工具。

Gawk 是 Unix Awk 的 GNU 版本。Awk 最初被创建为 Unix 操作系统的标准工具。它的创建者之一是 Brian Kernigh，他开发了 Unix 操作系统。后来开发了名为 Nawk 的 Awk 增强版本，包含了文件处理。通过 Nawk，你可以在同一个程序中访问多个文件。Gawk 有进一步的增强，包含了 Nawk 的功能以及 Awk 的标准功能。

Gawk 拥有全套算术运算符。你可以执行除、加、减和取模运算。算术运算符与 C 语言和 Perl 中使用的相同。Gawk 还支持标量数组和关联数组，以及类似于 Perl 和 Tcl/Tk 的模式匹配和字符串函数。你可以在 `www.gnu.org/software/gawk` 了解更多关于 Gawk 信息。

# Gawk 命令

`awk` 命令的参数是一个 `awk` 指令和文件名列表。`gawk` 指令包含在单引号中并被视为一个参数。`awk` 指令由两个部分组成：模式（pattern）和动作（action）。动作包含在括号中。“模式”一词可能具有误导性。将模式部分视为条件（condition）或许更清晰。模式可以是一个搜索条件，也可以是编程语言中类型的测试条件。Gawk 工具有一全套运算符，用于构建复杂的条件。用户不再是像 `grep` 那样简单地匹配模式，而是指定一个条件。匹配该条件的记录将被提取。脚本中的动作随后将应用到该记录上。下一个示例显示了 `gawk` 指令的语法，你可以将其视为 `condition {action}`：

`pattern {action}`

Gawk 工具在文件或标准输入上操作。你可以在指令之后在命令行上列出文件名。如果没有列出文件，则从标准输入获取输入。下面的示例显示了整个 Gawk 指令的结构。调用 Gawk 由 `gawk` 关键字、Gawk 指令和文件名组成。使用 `sed` 命令时，指令应该放在单引号内以避免被 shell 解释。由于条件和动作不是 Gawk 的独立参数，你需要将它们封装在一组引号中。下一个示例显示了 `gawk` 命令的语法：

```bash
$ awk 'pattern { print }' filenames
```

你可以将 Gawk 指令中的模式视为对某行的引用。Gawk 动作在单行上执行。接下来的两个示例将打印所有包含模式 "Penguin" 的行。模式段是一个模式搜索。模式搜索由包含在斜线中的模式表示。使用此模式，所有符合该模式的记录都将被检索。第一个示例中的动作段包含 `print` 命令。`print` 命令将输出到标准输出。

| books | | | |
| :--- | :--- | :--- | :--- |
| Penguin | | | |
| Tempest | Shakespeare | 15.75 | Penguin |
| Christmas | Dickens | 3.50 | Academic |
| Iliad | Homer | 10.25 | Random |
| Raven | Poe | 2.50 | Penguin |

```bash
$ awk '/Penguin/{print}' books

Tempest Shakespeare 15.75 Penguin

Raven Poe 2.50 Penguin
```

你可以将 Gawk 指令中的模式理解为对某行的引用。Gawk 动作在单行上执行。（注：原文此处似乎有逻辑重复*）

> 提示：动作和模式在 Gawk 中都允许你省略其中任何一个。

```bash
$ awk '/Penguin/{print}' books

Tempest Shakespeare 15.75 Penguin

Raven Poe 2.50 Penguin
```
