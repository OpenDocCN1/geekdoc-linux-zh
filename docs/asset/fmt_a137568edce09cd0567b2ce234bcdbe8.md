
```bash
$ echo $person
max
$ echo "$person"
max
$ echo '$person'
$person
$ echo \$person
$person
```

## 空格（SPACES）

双引号不会阻止变量替换，但会关闭大多数其他字符的特殊含义。因此，在将值分配给变量以及使用这些值时，双引号非常有用。要为包含空格或制表符的变量分配值，请在使用双引号将值括起来。虽然并非所有情况都需要双引号，但使用它们是一个良好的习惯。

```bash
$ person="max and zach"
$ echo $person
max and zach
$ person=max and zach
bash: and: command not found
```

当你引用一个值包含制表符或多个相邻空格的变量时，你需要使用引号来保留空格。如果你没有给变量加引号，Shell 会在将变量传递给实用程序之前，将每串空白字符压缩为一个空格：

```bash
$ person="max    and    zach"
$ echo $person
max and zach
$ echo "$person"
max and zach
```

### 赋值中的路径名扩展

当你使用变量作为参数执行命令时，Shell 会用变量的值替换变量名，并将该值传递给正在执行的程序。如果变量的值包含特殊字符，如 `*` 或 `?`，Shell *可能* 会扩展该变量。

下面这一系列命令的第一行将字符串 `max*` 分配给变量 `memo`。Bourne Again Shell *不会扩展该字符串*，因为 bash 在将值分配给变量时不执行路径名扩展（第 256 页）。所有 Shell 都按照特定顺序处理命令行。在此顺序中，bash 在解释命令之前先扩展变量。在下面的 echo 命令行中，双引号对扩展后的 `$memo` 值中的星号（`*`）进行了引用，防止 bash 在将 memo 变量的扩展值传递给 echo 命令之前对其执行路径名扩展：

```bash
$ memo=max*
$ echo "$memo"
max*
```

当你引用一个包含未加引号的特殊字符的变量时，所有 Shell 都会将这些特殊字符解释为特殊字符。在下面的例子中，因为该值未加引号，所以 Shell 扩展了 `memo` 变量的值：

```bash
$ ls
max.report
max.summary
$ echo $memo
max.report max.summary
```

在这里，Shell 将 `$memo` 变量扩展为 `max*`，将 `max*` 扩展为 `max.report` 和 `max.summary`，并将这两个值传递给 `echo`。

## 可选：花括号

`$VARIABLE` 语法是更通用的语法 `${VARIABLE}` 的特例，在后者中，变量名被 `{}` 包围。花括号将变量名与相邻字符隔离开来。在将变量值与字符串拼接时，必须使用花括号：

```bash
$ PREF=counter
$ WAY=$PREclockwise
$ FAKE=$PREfeit
$ echo $WAY $FAKE
```

上述示例未按预期工作。因为尽管符号 `PREclockwise` 和 `PREfeit` 是有效的变量名，但它们并未被设置，所以只输出了一行空白。默认情况下，*bash* 将未设置的变量评估为空（null）字符串并显示该值。为了实现这些语句的意图，请使用花括号引用 `PRE` 变量：

```bash
$ PREF=counter
$ WAY=${PRE}clockwise
$ FAKE=${PRE}feit
$ echo $WAY $FAKE
counterclockwise_counterfeit
```

Bourne Again Shell 通过位置引用其命令行上的参数，使用特殊变量 `$1`、`$2`、`$3` 等，直到 `$9`。如果你想引用第九个参数之后的参数，必须使用花括号：`${10}`。命令名称保存在 `$0` 中（第 997 页）。

## unset：移除变量

除非你移除一个变量，否则只要创建它的 Shell 存在，该变量就会一直存在。要移除变量的*值*但保留变量本身，请为该变量分配一个空值：

```bash
$ person=
$ echo $person
```

你可以使用 *unset* 内建命令移除变量。以下命令移除了变量 *person*：

```bash
$ unset person
```

## 变量属性

本节讨论属性以及如何为变量分配它们。

### readonly：使变量的值永久化

你可以使用 *readonly* 内建命令来确保变量的值不能被更改。下一个例子声明变量 *person* 为只读。你必须在将变量声明为只读*之前*为其分配值；声明后你不能更改其值。当你尝试取消设置或更改只读变量的值时，Shell 会显示一条错误消息：

```bash
$ person=zach
$ echo $person
zach
$ readonly person
$ person=helen
bash: person: readonly variable
```

如果你在没有参数的情况下使用 *readonly* 内建命令，它会显示所有只读 Shell 变量的列表。该列表包括自动设置为只读的关键词变量，以及你声明为只读的关键词或用户创建的变量。请参阅第 318 页的示例（*readonly* 和 *declare -r* 产生相同的输出）。

### declare 和 typeset：为变量分配属性

*declare* 和 *typeset* 内建命令（同一命令的两个名称）为 Shell 变量设置属性和值。表 9-3 列出了其中的五个属性。

**表 9-3** 变量属性（typeset 或 declare）

| 属性 | 含义 |
| :--- | :--- |
| `-a` | 声明变量为数组（第 990 页） |
| `-f` | 声明变量为函数名（第 349 页） |
| `-i` | 声明变量为整数类型（第 318 页） |
| `-r` | 使变量*只读*；也是 *readonly*（第 317 页） |
| `-x` | 导出变量（使其变为全局变量）；也是 *export*（第 992 页） |

以下命令声明了几个变量并设置了一些属性。第一行声明 *person1* 并为其分配值 *max*。无论是否带有 *declare* 一词，该命令的效果相同。

```bash
$ declare person1=max
$ declare -r person2=zach
$ declare -rx person3=helen
$ declare -x person4
```

readonly 和 export 内建命令分别是命令 `declare -r` 和 `declare -x` 的同义词。你可以声明变量而不为其分配值，正如前面变量 `person4` 的声明所示。此声明使 `person4` 对所有子 Shell 可用（即使其变为全局变量）。在对变量进行分配之前，它具有空值。

你可以将 `declare` 的选项以任何顺序单独列出。以下命令与前面 `person3` 的声明等效：

```bash
$ declare -x -r person3=helen
```

当你想要从变量中移除某个属性时，请用 `+` 字符替代 `-`。你无法移除只读属性。在给出以下命令后，变量 `person3` 不再被导出，但它仍然是只读的。

```bash
$ declare +x person3
```

你可以使用 `typeset` 代替 `declare`。

不带任何参数或选项时，`declare` 列出所有 Shell 变量。当你不带任何参数运行 `set`（第 998 页）时，也会输出相同的列表。

- **列出变量属性**

如果你使用带有选项但没有变量名作为参数的 `declare` 内建命令，该命令将列出所有具有指定属性设置的 Shell 变量。例如，命令 `declare -r` 显示所有只读 Shell 变量的列表。该列表与不带任何参数的 `readonly` 命令生成的列表相同。在给出前面示例中的声明后，结果如下：

```bash
$ declare -r
declare -ar BASH_VERSIONINFO=([0]='3' [1]='2' [2]='39' [3]='1' ... )
declare -ir EUID='500'
declare -ir PPID='936'
declare -r SHELLOPTS="braceexpand:emacs:hashall:histexpand:history:..."
declare -ir UID='500'
declare -r person2='zach'
declare -rx person3='helen'
```

前五个条目是自动声明为只读的关键词变量。其中一些变量以整数形式存储（`-i`）。`-a` 选项表明 `BASH_VERSIONINFO` 是一个数组变量；数组每个元素的值列在等号的右侧。

- **整数**

默认情况下，变量的值以字符串形式存储。当你对字符串变量执行算术运算时，Shell 将变量转换为数字，对其进行操作，然后转换回字符串。具有整数属性的变量以整数形式存储。按以下方式分配整数属性：

```bash
$ declare -i COUNT
```

## 关键词变量

关键词变量要么被继承，要么是 Shell 启动时声明和初始化的。你可以从命令行或这些变量来自启动文件。通常，你希望这些变量同样适用于你启动的所有子 shell 以及你的登录 shell。对于 shell 未自动导出的那些变量，你必须使用 export（第 992 页）使其在子 shell 中可用。

## HOME：你的主目录

默认情况下，你的主目录是你登录时的工作目录。你的主目录在设置账户时建立；其名称存储在 `/etc/passwd` 文件中。

```bash
$ grep sam /etc/passwd
sam:x:501:501:Sam S .x301::/home/sam:/bin/bash
```

当你登录时，shell 会继承你主目录的路径名，并将其分配给变量 `HOME`。当你给出一个不带参数的 `cd` 命令时，`cd` 会将存储在 `HOME` 中的目录名作为工作目录：

```bash
$ pwd
/home/max/laptop
$ echo $HOME
/home/max
$ cd
$ pwd
/home/max
```

此示例展示了 `HOME` 变量的值以及 `cd` 内建命令的效果。在你执行不带参数的 `cd` 之后，工作目录的路径名与 `HOME` 的值相同：你的主目录。

波浪号 (~) shell 使用 `HOME` 的值来扩展使用波浪号（~）简写表示法（第 206 页）表示用户主目录的路径名。以下示例使用 `echo` 显示此快捷方式的值，然后使用 `ls` 列出 Max 的 laptop 目录中的文件，该目录是其主目录的一个子目录：

```bash
$ echo ~
/home/max
$ ls ~/laptop
tester count lineup
```

## PATH：Shell 查找程序的目录

当你给 shell 一个绝对或相对路径名，而不是简单的文件名作为命令时，它会在指定的目录中查找具有指定文件名的可执行文件。如果你指定的路径名的文件不存在，shell 会报告 command not found。如果文件如指定存在，但你没有对它的执行权限，或者对于 shell 脚本你没有读取和执行权限，shell 会报告 Permission denied。

如果你给出一个简单的文件名作为命令，shell 会在某些目录（你的搜索路径）中搜索你要执行的程序。它会在几个目录中查找一个与命令同名且你拥有执行权限（编译后的程序）或读取和执行权限（shell 脚本）的文件。`PATH` shell 变量控制此搜索。

### 320 第 9 章 Bourne Again Shell

- 工作目录

`PATH` 的默认值在编译 bash 时确定。它不在启动文件中设置，尽管可能会在那里进行修改。通常，默认值指定 shell 搜索几个用于存放常用命令的系统目录。这些系统目录包括 `/bin` 和 `/usr/bin` 以及适合本地系统的其他目录。当你发出一个命令时，如果 shell 没有在 `PATH` 列出的任何目录中找到由命令命名的可执行——并且在 shell 脚本情况下是可读的——文件，shell 会生成上述错误消息之一。

`PATH` 变量指定了 shell 应该按顺序搜索的目录。每个目录必须用冒号与下一个目录分隔。以下命令设置 `PATH`，使得对可执行文件的搜索从 `/usr/local/bin` 目录开始。如果在此目录中未找到文件，shell 接下来在 `/bin` 中查找，然后在 `/usr/bin` 中查找。如果在这些目录中的搜索失败，shell 会在 `~/bin` 目录中查找，这是用户主目录的一个子目录。最后，shell 会在工作目录中查找。导出 `PATH` 使其值对子 shell 可访问：

```bash
$ export PATH=/usr/local/bin:/bin:/usr/bin:~/bin:
```

字符串中的空值表示工作目录。在上面的示例中，空值（冒号与行尾之间没有内容）出现在字符串的最后一个元素中。工作目录由前导冒号（不推荐；参见以下安全提示）、尾随冒号（如示例中所示）或字符串中任意位置相邻的两个冒号表示。你也可以用点（`.`）显式表示工作目录。

由于 Linux 将许多可执行文件存储在名为 `bin`（binary）的目录中，用户通常将自己可执行文件放在自己的 `~/bin` 目录中。如果你将自己 bin 目录放在 `PATH` 的末尾，如前面的示例所示，shell 将在 `PATH` 中列出的较早目录中找不到任何命令时，在该目录中查找。

## PATH 与安全性

- 安全性

当安全性是一个问题时，不要将工作目录放在 `PATH` 的第一位。如果你以 root 身份工作，绝对不要将工作目录放在 `PATH` 的第一位。root 的 `PATH` 通常完全省略工作目录。你总是可以通过在名称前添加 `./` 来执行工作目录中的文件：`./myprog`。

将工作目录放在 `PATH` 的第一位可能会创建一个安全漏洞。大多数人进入目录时输入的第一个命令是 `ls`。如果目录的所有者在该目录中放置了一个名为 `ls` 的可执行文件，并且工作目录出现在用户 `PATH` 的第一位，那么用户从该目录发出 `ls` 命令时，将执行工作目录中的 `ls` 程序，而不是系统 `ls` 实用程序，这可能产生不良结果。

如果你想向 `PATH` 添加目录，你可以在设置 `PATH` 为新值时引用 `PATH` 变量的旧值（但参见前面的安全提示）。以下命令将 `/usr/local/bin` 添加到当前 `PATH` 的开头，并将用户主目录中的 bin 目录（`~/bin`）添加到末尾：

```bash
$ PATH=/usr/local/bin:$PATH:~/bin
```

## MAIL：邮件存储位置

`MAIL` 变量包含保存你邮件的文件（你的 *邮箱*，通常是 `/var/mail/name`，其中 *name* 是你的用户名）的路径名。如果设置了 `MAIL` 且未设置 `MAILPATH`（下一节），shell 会在 `MAIL` 指定的文件中有邮件到达时通知你。在图形环境中，你可以取消设置 `MAIL`，以便 shell 不在终端模拟器窗口中显示邮件提醒（假设你使用的是图形化邮件程序）。

`MAILPATH` 变量包含一个用冒号分隔的文件名列表。如果设置了此变量，当列表中任何一个文件被修改时（例如，当邮件到达时），shell 会通知你。你可以跟随列表中任何文件名的后面加上问号（`?`），然后跟随一条消息。当你登录状态下收到邮件时，该消息会替换 `you have mail` 消息。

`MAILCHECK` 变量指定 shell 检查新邮件的频率（以秒为单位）。默认值为 60 秒。如果你将此变量设置为零，shell 会在每个提示符之前检查。

## PS1：用户提示符（主要）

Bourne Again Shell 的默认提示符是美元符号（`$`）。当你以 **root** 权限运行 **bash** 时，**bash** 通常显示井号（`#`）提示符。**PS1** 变量保存 shell 用于告知你它正在等待命令的提示字符串。当你改变 **PS1** 的值时，你就改变了提示符的外观。

你可以自定义 **PS1** 显示的提示符。例如，赋值语句

```bash
$ PS1="[\u@\h \W \]$ "
```

显示以下提示符：

`[user@host directory event]$`

其中 *user* 是用户名，*host* 是直到第一个点止的主机名，*directory* 是工作目录的基名，*event* 是当前命令的事件号（第 331 页）。

如果你正在多个系统上工作，将系统名称合并到提示符中可能会有帮助。例如，你可能会将提示符更改为你正在使用的系统名称，后面跟一个冒号和空格（提示符末尾的空格使你输入的命令更容易阅读）。此命令在分配给 **PS1** 的字符串中使用命令替换（第 362 页）：

```bash
$ PS1="$(hostname): "
bravo.example.com: echo test
test
bravo.example.com:
```

以下第一个示例将提示符更改为主机名称、一个 `SPACE`（空格）以及一个美元符号（或者，如果用户以 **root** 权限运行，则为井号）。第二个示例将提示符更改为时间后跟用户名称。第三个示例将提示符更改为本书中使用的样式（root 使用井号，其他情况使用美元符号）：

```bash
$ PS1='\h \$ '
bravo $
$ PS1='\@ \u $ '
09:44 PM max $
$ PS1='\$ '
$
```

表 9-4 描述了一些你可以用在 `PS1` 中的符号。要查看提示字符串中可使用的特殊字符完整列表，请打开 `bash` 手册页并搜索第二次出现的 PROMPTING（输入命令 `/PROMPTING` 然后按 n）。

### 表 9-4 PS1 符号

| **符号** | **在提示符中的显示** |
| :--- | :--- |
| `\$` | 如果用户以 **root** 权限运行，显示 `#`；否则显示 `$` |
| `\w` | 工作目录的路径名 |
