
这个命令词是 `ls`，它不包含斜杠。因此，shell 检查 PATH 中的第一个目录（在本例中是 `/bin`）。如果 `/bin/ls` 是可执行文件，shell 将尝试运行该程序且不再检查 PATH 中的任何其他目录。如果 `/bin/ls` 不存在或不是普通文件或可执行文件，shell 然后将移动到下一个目录（在本例中是 `/usr/bin`）。如果 `/usr/bin/ls` 是可执行文件，shell 将尝试运行它且不再检查 PATH 中的任何其他目录。当 shell 尝试了 PATH 中的所有目录都未找到可执行文件时，它将放弃并返回“命令未找到”的错误。

# 将当前目录添加到 PATH

如果你的 UNIX 命令不包含斜杠，则只会检查 PATH 中的目录。有些人还希望检查当前目录。这通常只在你编写自己的 shell 脚本，并希望在脚本所在的目录中能够运行它们时才有用用。

要在 PATH 变量中包含当前目录，请添加点目录 `.` 或空目录。我更倾向于添加点目录，因为那是指示当前目录的常用方法。然而，你应该能够识别 PATH 中的空目录，因为这涉及到安全影响（后文将介绍）。

这是一个在 Bourne shell 或 Korn shell 中使用点 `.` 将当前目录添加到 PATH 的示例。

```
PATH=/usr/bin:.:../usr/local/bin
```

在这里，PATH 设置为在 `/bin` 和 `/usr/bin` 之后、`/usr/local/bin` 之前搜索当前目录。这里是更多使用点的示例：

```
PATH=/bin:/usr/bin:/local/bin:. # 情况 1
```

```
PATH=.:usr/bin:/local/bin # 情况 2
```

```
PATH=$PATH:. # 情况 3
```

在情况 1 中，当前目录在 `/bin` 和 `/usr/bin` 之后搜索。在情况 2 中，它在其他目录之前搜索。在情况 3 中，它在原有的 `$PATH` 之后搜索。

作为一种简便方法，你可以使用空目录来指示当前目录。空目录就像点一样，但多了一个冒号。看以下示例：

```
PATH=/usr/bin:/local/bin:: # 情况 1
```

```
PATH=:/usr/bin:/local/bin # 情况 2
```

```
PATH=/bin:/usr/bin:/local/bin: # 情况 3
```

```
PATH=$PATH:: # 情况 4
```

在情况 1 中，当前目录在 `/local/bin` 之后搜索。在情况 2 中，它在其他目录之前搜索。在情况 3 和 4 中，它在最后搜索。

# PATH 的安全影响

通常，你不应该将当前目录指定在 PATH 的开头。出于安全考虑，如果你要把当前目录添加到 PATH，请将其放在最后。否则，黑客可以在目录下创建与常用命令同名的文件。如果你在陷阱目录执行系统命令，运行的是黑客的程序而不是系统命令。

出于同样的原因，root PATH 中的任何目录都不应对普通用户具有写权限。

# PATH 与附加包

如果你为系统添加了新的软件包，该包可能要求你将其可执行目录添加到 PATH 变量。软件包的安装脚本可能会自动修改 `/etc/profile`。修改 `/etc/profile` 需要 root 权限。在你以 root 身份添加包后，请登录并检查你的 PATH 变量。确保目录顺序是合理的，特别是当它被包修改过时。

# 命令在哪里？

有时知道你运行的命令的完整路径是有用的，特别是当它们运行不正常且你想调查原因时。PATH 可能包含许多目录，因此幸运的是某些命令可以为你检查 PATH 并告诉你命令的完整路径。

这些命令中最用用 `type`，它在 Bourne shell 和 Korn shell 中都有效：

```
$ type ls # 来自 Bourne shell
ls /usr/bin/ls
$ exec ksh 切换到 Korn shell
$ type ls
ls is a tracked alias for /usr/bin/ls
$
```

在这里，`type` 获取你提供的命令并确定该命令的完整路径名。

如果你的系统不支持 `type` 命令，请使用 `which` 命令或 `whence` 来获取命令的完整路径：

```
$ which ls
$ whence ls
```

# 用户输入 UNIX 命令时常见的错误

通常该命令只在 Bourne shell 中有效，而 `whence` 命令仅在 Korn shell 中有效。

对于初学者来说，UNIX 可能会令人沮丧。起初，UNIX 似乎非常挑剔，会对你输入的每一个内容都反对意见。接下来的章节将介绍学者常犯错误，帮助你避免它们。

## 错误的大小写

> UNIX 是区分大小写的

区分大小写意味着你在文件名或命令中必须使用相同的大写和小写字母。如果你使用了错误的大小，将无法访问该文件或命令。

在 UNIX 下，以下文件名将指向不同的文件：

- acme acMe acMe acmeE
- ACME acME acMe AcME
- Acme Acme aCME AcME

所有这些文件可能同时在一个目录中被使用，在 UNIX 中，字母是大写还是小写至关重要。起初，你的眼睛可能甚至注意到本该是小写却误写大写的字母，反之亦然。

要警小心手写的 UNIX 命令指令，因为人们在书写时往往不注意大小写。

## 错误的空格

正如本章前面提到的，命令、选项和参数不能连在一起；它们必须用空格隔开。在命令或路径中间插入空格也是无效的。

## 误用方向键、插入键、翻页键和其他特殊键

避免使用键盘上的特殊键，如箭头键、Insert键、Home键、End键以及Page Up 和 Page Down键。Linux 是唯一良好整合了这些键的 UNIX 变。对于其他类型的 UNIX 系统，使用这些特殊键只会向文件、电子邮件和文件名中插入转义序列。一旦你插入了这些垃圾内容，将其删除会非常困难。

Windows 用户习惯 PC 风格键盘和 PC 编辑键。Windows 程序使用这些特殊键是有的，因为它们一直触手可及。UNIX 运行在各种系统中，许多系统的键盘并没有这些键。如果一个 UNIX 系统有 100 个工作站，可能只有控制台有这些键，而控制台可能被锁在机房里。UNIX 通常在图形工作站上支持这些键，但在许多字符工作站上不支持。

如果你在文本文档、电子邮件或文件名中发现如下垃圾内容：
`^[A]`|`^[B]`|`^[C]`|`^[D]`

这是用户试图使用方向键重新移动光标来纠正拼写错误导致的。

要在文件名中显示控制字符，请使用 `ls -b`：

```bash
$ ls
acme
acme
$ ls -b
acme
abm*'|[0^]|\0acme
$
```

起初 `ls` 似乎显示同一个目录下有两个名为 acme 的文件，这绝是不可能的。通过给 `ls` 添加 `-b` 选项，我们可以看到第二个文件名中的控制字符。该文件名是由一个用户创建的，他本想将输出重定向到 acme 但误打成了 `abm`。他按了两次左箭头键并在 `bn` 之上输入了 `cm`，以便命令行显示为 `acme`。用户从未意识到自己犯了这个错误，因为一切看起来都很正常。

你应该如何备份和纠正输入错误？嗯，这取决于情况。备份和纠正错误有两种主要方法：

# 第一部分 UNIX 基础

# 第四章 输入 UNIX 命令的规则

- 使用 Backspace 键或按 `Ctrl+H`
- 使用 delete 键或按 `Ctrl+?`

这之所以变得复杂，是因为在某些键盘上，Delete 键发送的是 ASCII DEL `127` 字符。在其他键盘上，它发送的是 ESC 序列。Backspace 键会发送 `Ctrl+H` 或 ASCII DEL。有时 Backspace 是可编程的，特别是当你使用 PC 登录 UNIX 时。有时 Backspace 会发送 `Ctrl+H`，而 `Shift+Backspace` 会发送 DEL，反之亦然。

为了消除疑惑，请输入以下：

```bash
$ stty -a
speed 38400 baud;
eucw 1:0:0:0; scrow 1:0:0:0
intr = ^c; quit = ^; erase; kill = ^u
eof = ^d; eol = <undef>; eol2 = <undef>; swtch = <undef>
start = ^q; stop = ^s; z = ^z; dsupup = ^y
prnt = ^r; flush = ^o; werase = ^w; lnext = ^v
parenb -parodd cs8 -cstopb -hubpc own create istrip -loblk -clocal -crtscts -crtssoff -
ibrnk brinkxl ingnar -parmark -inpck istrip -lncr icrnl -iuclcixon
ixany -ixoff imoxal
isig isican -xcase echo echo echok -echon -nflsh
```
