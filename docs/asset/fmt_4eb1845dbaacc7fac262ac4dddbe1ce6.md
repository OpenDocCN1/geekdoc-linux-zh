
`$ who | grep 'root' | sort | tee root.txt`

```bash
$ who | grep 'root' | sort | tee root.txt
```

通过结合过滤器，你可以使用简单的工具执行复杂的数据处理任务。每个过滤器执行一个特定的任务，它们共同可以解决许多问题。

## 在后台运行程序

### 前台 (Foreground)

在之前的示例中，命令都是在前台运行的。当你在前台运行命令时，Shell 会等待它完成，给你另一个提示符并允许你继续。当你在后台运行命令时，你不需要等待它完成。

### 任务 (Jobs)

任务是可以通过管道连接的一个或多个命令的序列。你可以在窗口或屏幕上只有一个前台任务，但你可以有多个后台任务。通过同时运行多个任务，你正在使用 Linux 的重要功能之一：多任务处理。

### 任务号、PID 号

要在后台运行命令，在结束命令行的回车键之前输入与符号 (`&`)。Shell 会为任务分配一个较小的数字并在括号中显示该任务号。在任务号之后，Shell 显示由操作系统分配的较大的进程标识 (PID) 号。这些每一个都标识了正在后台运行的命令。然后 Shell 显示另一个提示符，你可以输入另一个命令。当后台任务完成时，Shell 会显示一条包含任务号和运行该命令的消息。

下一个示例在后台运行并将其输出通过管道发送到 `lpr`，将其发送到打印机。

```bash
$ ls -l | lpr &
[1] 2092
```

`[1]` 跟随命令行表示 Shell 为此任务分配了任务号 1。`2092` 是该的 PID 号。

作业中的命令。当此后台任务执行完毕时，你会看到消息：

`[1]+ Done ls -l | lpr`

（相对于 `ls -l`，shell 可能会显示类似于 `ls --color=tty` 的内容。这种差异是因为 `ls` 被别名为 `ls --color=tty`。）

# 将作业从前台移动到后台

### CONTROL-Z

你可以通过按下暂停键（通常为 `CONTROL-Z`）来挂起作业（停止其运行）。shell 会停止该进程并断开标准输入与键盘的连接。你可以使用 `bg` 命令加上作业号将挂起的作业置于运行并重新启动它。当只有一个停止的作业时，不需要使用作业号。

只有前台作业可以从键盘获取输入。要将键盘连接到后台运行的程序，你必须将其带回前台。当后台只有一个作业时，不带任何参数直接输入 `fg`。当后台有多个作业时，输入 `fg` 或百分号 (`%`)，后跟你想带回前台的作业号。shell 会显示你用于启动该作业的命令（在下面的示例中为 `promptme`），你可以在提示符中输入任何内容以继续：

```bash
bash $ fg 1
promptme
```

重定向你在后台运行的作业输出，以防止它干扰你在屏幕上正在进行的任何操作。有关后台任务的更多细节，请参阅“命令的分离与分组”第276页。

# kill：终止后台作业

中断键（通常为 `CONTROL-C`）无法终止你在后台运行的进程；你必须使用 `kill` 来实现此目的。在命令行中使用 `kill` 后，加上想要终止的进程 PID 或百分号 (`%`) 以及作业号。

### 使用 ps 确定 PID

如果你忘记了 PID 号，可以使用 `ps`（进程状态）工具来显示。下面的示例作为后台作业运行 `tail -f outline`（`f` 选项调用 `tail` 监控 `outline` 并在写入文件时显示新行），使用 `ps` 显示该进程的 PID 及其作业控制信息（jobctrl）：

```bash
$ tail -f outline &
[1] 18228
$ ps | grep tail
18228 pts/4 00:00:00 tail
$ kill 18228
[1]- Terminated tail -f outline
$
```

如果你忘记了作业号，可以使用 `jobs` 命令显示作业号列表。下一个示例与上一个类似，但使用作业号而非 PID 来终止作业。有时，提示作业已终止的消息直到你按下回车键以结束 `kill` 命令时才会出现：

```bash
$ tail -f outline &
[1] 18236
$ bigjob &
[2] 18237
$ jobs
[1]- Running tail -f outline &
[2]+ Running bigjob & 
$ kill %1
$ RETURN
[1]- Terminated tail -f outline
$
```

# 文件名生成/路径扩展

## 通配符，通配 (globbing)

当你给 shell 提供包含特殊字符（称为元字符）的缩写文件名时，shell 可以生成与现有文件名匹配的文件名。这些特殊字符也被称为通符，因为它们的作用就像扑牌中的万能牌。当这些字符之一出现在命令行中时，shell 会按排序顺序将参数扩展为文件名列表，并将列表传递给命令行。包含这些特殊字符的文件名被称为模糊文件引用，它们不指向任何特定文件。shell 对这些文件名执行的操作称为路径扩展或通配 (globbing)。

模糊文件引用可以快速引用一组名称相似的文件，节省了你逐个输入名称的精力。它还可以帮助你找到你不完整记得的文件名。如果没有文件名匹配模糊文件引用，shell 通常会将未扩展的引用字符直接传递给命令。

# 特殊字符

## 问号 (?) 特殊字符

问号 (`?`) 是一个特殊字符，导致 shell 在现有文件的名称中生成任意单个字符。下面的命令在 `lpr` 工具的参数中使用此特殊字符：

```bash
$ lpr memo?
```

shell 扩展 `memo?` 参数，并生成工作目录下所有由任意单个字符组成的文件列表。然后 shell 将此传递给 `lpr`。`lpr` 永远“不知道” shell 是生成了它所调用的文件名。如果没有文件名匹配模糊文件引用，shell 将将字符串本身 (`?`) 传递给 `lpr`，或者如果设置了如此，则传递使用第327页中 `nullglob` 的字符串。

下面的示例使用 `ls` 列出工作目录下所有文件的名称，然后显示与 `memo?` 匹配的文件名。

```bash
$ ls
memo memo12 memo9 memoalex newmemo5
memo memo5 memoa memos
```

```bash
$ ls memo?
memo5 memo9 memoa memos
```

`memo?` 模糊文件引用不匹配 `mem`、`memo`、`memo12`、`memoalex` 或 `newmemo5`。你也可以在模糊引用的中间使用问号：

```bash
$ ls
7may4report may4report may_report
may14report may4report.79 mayreport may_report
```

```bash
$ ls may*?report
may.report may4report may_report mayreport
```

练习生成文件名，可以使用 `echo`。`echo` 工具显示 shell 传递给它的参数：

```bash
$ echo may?report
may.report may4report may_report mayreport
```

shell 首先将引用 `may?report` 扩展为工作目录下所有文件的列表，然后将其传递给 `echo`，就像你输入了文件名列表作为参数一样。问号不匹配开头的点（表示隐藏文件；见第170页）。当你想要匹配以点开头的文件名时，必须在模糊文件引用中显式包含点。

## 星号 (*) 特殊字符

星号 (`*`) 的功能与问号类似，但它可以匹配任意数量的字符。下面的示例显示了 `*` 如何匹配任意数量的字符：

```bash
$ ls
7may4report may4report may_report
may14report may4report.79 mayreport may_report
```

（注：由于 OCR 原文中存在大量重复，已根据逻辑结构进行清理，以下为核心内容的后续翻译及特殊字符说明）

## 方括号 [ ] 特殊字符

一对括号括起字符列表，用于匹配包含这些单个字符的文件名。由于 `memo[17a]` 限制更严格，仅匹配 `memo1`、`memo7` 和 `memoa`；而 `memo*` 则匹配 memo 后面跟随任意字符。括号定义了一个包含括号内所有字符的字符类（character class）。

```bash
$ echo [aeiou]*
```

```bash
$ less page[2468].txt
```

以下命令显示了三种打印名为 part0、part1、part2、part3 和 part5 的文件名的方法。这些命令中的每一个都会导致 shell 带有 lpr，并传入文件名：

```bash
$ lpr part0 part1 part2 part3 part5
```

```bash
$ lpr part(0-1235)
```

```bash
$ lpr part(0-35)
```

第一条命令显式指定了五个文件名。第二个和第三条命令使用了无歧义的文件引用，结合了字符类定义。shell 会扩展第二条命令行的参数，以包含所有以 part 开头并以字符类中的任意字符结尾的文件。该字符类被显式定义为 a, 1, 2, 3 和 5。第三条命令也使用了字符类定义，但将字符类定义为 3-5 范围内的所有字符。

以下命令打印 39 个文件，从 part0 到 part38：

```bash
$ lpr part(0-9) part[12][0-9]part3[0-8]
```

接下来的两个示例列出了工作目录中的文件名。第一个列出了名称以 a 到 m 开头的文件。第二个列出了以 x、y 或 z 结尾的文件。

```bash
$ echo [a-m]*
```

```bash
$ echo [x-z]*
```

## 可选内容

当感叹号 (`!`) 或脱字符符号 (`^`) 紧跟在定义字符类的左括号 { 之后时，括号内的字符串匹配不在括号之间的任意字符。因此，`[^ab]` 匹配任何不以 a 或 b 开头的文件名。

以下示例显示 `[*b]` 匹配不以字母 a 或 b 结尾的文件名，而 `[b-d]*` 匹配以 b、c 或 d 开头的文件名。

```bash
$ ls
```

```bash
aa ab ac ad ba bc bd cc dd
```

```bash
$ ls [*ab]
```

```bash
ac ad bc bd cc dd dd
```

```bash
$ ls [b-d]*
```

```bash
ba bb bc bd cc dd
```

你可以通过将连字符 `-` 或右括号 `}` 放在最后一个右括号之前之前来匹配它们。

下一个示例演示了该实用程序无法解释歧义的文件引用。首先是 `?old`。shell 将 `?old` 扩展为文件名 `.hold`，并将该名称传递给 shell。第二条命令与第一条相同，只是给 `?` 加上了引号（见第 126 页的“特殊字符”）。shell 不将问号识别为特殊字符，并将其传递给 `ls`。实用程序生成一条错误信息，说找不到名为 `?old` 的文件（因为没有名为 `?old` 的文件）。

```bash
$ ls ?old
```

```bash
hold
```

```bash
$ ls ?old: No such file or directory
```
