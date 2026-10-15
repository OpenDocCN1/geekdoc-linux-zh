
在前面的示例中，shell 在后台作业启动时会立即通过提示符显示该作业的作业号和 PID 号。为了演示此时可以输入命令，用户输入了 `date` 命令，其输出显示在屏幕上。shell 一直到发出提示符（在 `date` 完成后）才会通知你作业 1 已停止。当你输入 `fg` 命令时，shell 将作业置于前台，你就可以输入命令正在等待的数据。在这种情况下，输入需要用 CTRL-D 终止，这会向 shell 发送一个 EOF（文件结束）信号。shell 随后会显示另一个提示符。

shell 会随时向你通报作业状态，在后台作业启动、完成或停止时通知你，因为它正在等待终端的输入。shell 也会在前台作业被挂起时通知你。因为后台运行作业的通知可能会干扰你的工作，shell 会推迟显示这些通知，直到显示提示符之前。你可以设置 `notify`（第 355 页）来调用 shell 无延迟显示这些通知。

# 310 第 9 章 BOURNE AGAIN SHELL

![](img/c8ae2cd4d550a81142a3ed64b0f61f6a_360_0.png)

图 9-2 示例中的目录结构

如果你在作业停止时尝试退出 shell，shell 会发出警告且不允许你退出。此时如果你使用 `jobs` 查看作业列表，或立即再次尝试退出 shell，shell 将允许你退出。如果没有设置 `hupon`（第 355 页）（默认值），停止的后台作业将继续在后台运行。如果设置了该项，shell 将终止这些作业。

## 操作目录栈

Bourne Again Shell 允许你存储一个正在工作的目录列表，使你能够在它们之间轻松移动。这个列表被称为栈（stack）。它类似于一叠盘子：你通常从栈的顶部添加和移除盘子，因此这种类型的栈被称为后进先出（LIFO）栈。

### dirs：显示栈

`dirs` 内置命令显示目录栈的内容。如果你在目录栈为空时调用 `dirs`，它会显示工作目录的：

```bash
dirs
~/literature
```

![](img/c8ae2cd4d550a81142a3ed64b0f61f6a_360_1.png)

图 9-3 创建目录栈

## shell 基础 31

![](img/c8ae2cd4d550a81142a3ed64b0f61f6a_361_0.png)

**图 9-4** 使用 `pushd` 切换工作目录

`dirs` 内置命令使用波浪号 (-) 表示用户目录的名字。后续章节中的示例假设你指的是图 9-2 所示的目录结构。

### pushd 栈上的目录

当你带一个参数使用 `pushd`（推入目录）内置命令时，它会将参数指定的目录推入栈中，切换到指定的目录并显示栈。接下来的示例如图 9-3 所示：

```bash
$ pushd ..demo
~/demo ~literature
$ pwd
/home/sam/demo
$ pushd ..names
~names ~demo ~literature
$ pwd
/home/sam/names
```

当你不带参数使用 `pushd` 时，它会交换栈顶部的两个目录，将新目录（原来的第二个目录）变为当前目录，并显示栈（图 9-4）：

```bash
$ pushd
~/demo ~names ~literature
$ pwd
/home/sam/demo
```

通过这种方式使用 `pushd`，你可以轻松地在目录之间来回移动。（注：原文此处存在大量重复性错误，已根据逻辑清理翻译）。

通过在名称前加上美元符号（$、$? 和 #）来引用变量（所有变量都是如此的）。这些参数的值反映了你与 shell 之间持续交互的不同方面。

每当你输入一个命令时，命令行上的每个参数都会成为一个位置参数的值（第 996 页）。位置参数允许你访问命令行参数，你在编写 shell 脚本时经常会用到这种功能。`set` 内置命令（第 998 页）允许你为位置参数赋值。

其他频繁需要的 shell 脚本变量，例如上一次执行的命令名称、命令行参数的个数以及最近执行命令的状态，都可以以特殊参数的形式提供（第 994 页）。你不能为特殊参数赋值。

## 用户创建的变量

以下示例的第一行声明了名为 `person` 的变量，并将其初始化为值 `max`：

```bash
$ person=max
$ echo person
person
$ echo $Person
max
```

由于 `echo` 将其参数复制到标准输出，因此可以使用它来显示变量的值。上一个示例的第二行显示 `person` 并不代表 `max`。相反，字符串 `person` 被回显为 `person`。只有在名称前加上美元符号（$）时，shell 才会替换变量的值。因此，`echo Person` 显示变量 `person` 的值；它没有显示 `Person`，因为 shell 不会将 `$Person` 作为参数显示。由于开头的 `$`，shell 识别出 `Person` 是变量名，替换变量的值，并将该值传递给 `echo`。`echo` 内置命令显示变量的值——它永远不会“知道”你是通过变量调用它的。

引用 $ 符号

你可以通过对开头的 `$` 加引号来防止 shell 替换变量的值。双引号不能阻止替换；单引号或反斜杠（\）可以。

```bash
$ echo $Person
$ echo "Person"
max
$ echo 'Person'
$Person
$ echo \Person
$Person
```

### 空格

由于双引号不会阻止变量替换，但会关闭大多数其他字符的特殊功能，因此在为变量赋值以及使用这些值时，双引号非常有用。要给变量赋值一个包含空格（SPACES）或制表符（TABs）的值，请在值周围使用双引号。虽然并非所有情况下都需要双引号，但使用它们是一个好习惯。

```bash
$ person="max and zach"
$ echo $person
max and zach
$ person=max and zach
bash: and: command not found
```

当你引用一个值包含制表符或多个相邻空格的变量时，你需要使用引号来保留间距。如果你不对变量加引号，shell 在将变量传递给实用程序之前，会将每个空白字符字符串合并为单个空格（SPACE）：

```bash
$ person="max and zach"
$ echo $person
max and zach
$ echo "$person"
max and zach
```

### 路径名

当你使用变量作为参数执行命令时，shell 会将变量扩展名称替换为变量的值，并将该值传递给正在执行的程序。如果变量包含特殊字符（例如 `*` 或 `?`），shell 可能会扩展该变量。

在以下命令序列的第一行将 `max*` 赋值给变量 `memo`。Bourne Again Shell (bash) 不会扩展该字符串，因为 bash 在给变量赋值时不会执行路径名扩展（第 256 页）。所有 shell 都按照特定的顺序处理命令行。在这个顺序中，bash 在解释变量之前会扩展变量。在接下来的双引号中，引用了扩展后的 `echo` 命令中的星号（*），防止 bash 在将值传递给 `echo` 命令之前对扩展后的 `memo` 变量执行路径名扩展：

```bash
$ memo=*
$ echo "$memo"
max*
```

当你引用一个包含未引号特殊字符的变量时，所有 shell 都会将特殊字符视为特殊的。在下面的示例中，shell 扩展了 `memo` 变量的值，因为它没有加引号：

```bash
$ ls $memo
max.report
max.summary
$ echo $memo
max*
```

在这里，shell 将变量 `$memo` 扩展为 `max*`，将 `max*` 扩展为 `max.report` 和 `max.summary`，并将这两个值传递给 `echo`。

`$VARIABLE` 语法是通用语法 `${VARIABLE}` 的特例，其中变量名被括在 `{}` 中。大括号将变量名与相邻字符隔离开。在将变量值与字符串拼接时，大括号是必要的：

```bash
$ PREF=counter
$ WAY=$PREFclockwise
$ FAKE=$PREFeit
$ echo SWAY $FAKE
```

上面的示例并没有按预期工作。只输出了一个空行，因为虽然符号 `PREclockwise` 和 `PREfeit` 是有效的变量名，但它们没有被设置。默认情况下，bash 将未设置的变量评估为空字符串（null）并显示该值。为了实现这些语句的意图，请使用如下引用 `PREF` 变量：

```bash
$ PREF=counter
$ WAY=${PREF}clockwise
$ FAKE=${PREF}feit
$ echo SWAY $FAKE
counterclockwise counterfeit
```

Bourne Again Shell 通过位置引用命令行上的参数，使用特殊变量 `$1`、`$2`、`$3` 直到 `$9`。如果你想引用参数参数，必须使用大括号：`${10}`。命令名称存储在 `$0` 中（第 997 页）。

## unset: 删除变量

`unset` 内置命令删除变量。除非给出参数，否则它会随着 shell 的存在而一直存在。要删除变量，使用以下命令：

```bash
$ unset person
```

## readonly: 使变量永久

`readonly` 内置命令确保变量的值无法更改。以下示例将 `person` 设置为只读：

```bash
$ readonly person
```

如果你尝试更改只读变量，shell 会显示错误：

```bash
$ person=new
bash: person: readonly variable
```

## 变量属性

本节讨论了属性以及如何设置它们。

### 为变量分配属性

| 属性 | 含义 |
| :--- | :--- |
| -a | 声明数组 |
| -f | 声明函数 |
| -i | 变量为整数 |
| -r | 使变量只读 |
| -x | 导出变量 |

可以使用 `typeset` 代替 `declare`。在不带参数的情况下，`declare` 列出所有变量。在不带参数运行 `set`（第 998 页）时也会输出相同的列表。如果你带有选项但没有提供变量名，命令将列出所有设置了指定属性的变量。例如，`declare -r` 命令列出所有只读变量。这与不带参数的 `readonly` 命令产生的列表相同：

```bash
$ declare -r
- ar BASH_VERSINFO='([0]=3" [1]=2" [3]=39" [1]=1" )'
- ir EUID="500"
- ir PPID="936"
- r SHELLOPS=braceexpand:hash:histexpand:history:..."
- ir emacs="500"
- r person2="zach"
- rx person3="helen"
```

前五个项目是自动只读的关键字变量。只有部分这些变量被存储为整数 (-i)。-a 选项表示 `BASH_VERSINFO` 是数组；数组每个元素的值在等号右侧。

## 关键字变量

关键字变量要么继承，要么在 shell 启动时声明并初始化。你可以从命令行为这些变量赋值或

源自启动文件。通常，你希望这些变量适用于所有启动的子 shell 以及你的登录 shell。对于那些 shell 没有自动导出的变量，你必须使用 `export`（第 992 页）使它们子 shell 可用。

## HOME: 你的主目录

默认情况下，你的主目录是你登录时的工作目录。你的主目录在创建账户时建立；名称存储在 `/etc/passwd` 文件中。

```bash
$ grep sam /etc/passwd
sam:x:501:501:Sam x301:/home/sam:/bin/bash
```

当你登录时，shell 会继承你主目录的路径并将其赋值给变量 `HOME`。当你给出一个不带参数的 `cd` 命令时，`cd` 将存储在 `HOME` 中的目录设置为工作目录：

```bash
$pwd
/home/max/laptop
$ echo HOME
/home/max
$ cd
$pwd
/home/max
```

这个示例展示了 `HOME` 变量的值以及 `cd` 内置命令的效果。当你执行不带参数的 `cd` 时，工作目录的路径与 `HOME` 的值相同：即你的主目录。

波浪号 (-) 使用 `HOME` 的值来展开使用简写波浪号 (~) 符号（第 206 页）表示用户目录的路径。下面的示例使用波浪号显示此快捷方式的值，然后使用 `ls` 列出 Max laptop 目录中的文件，该目录是其主目录的子目录：

```bash
$ echo
/home/max
$ ls -~/laptop  count lineup
```

## PATH: shell 在哪里查找程序

当你给 shell 提供一个绝对或相对路径而不是简单的文件名作为命令时，它会在指定的目录中查找具有指定文件名的可执行文件。如果该路径的文件不存在，shell 会报告“未找到命令”（command not found）。如果文件按指定存在但你对其没有执行权限，或者在 shell 脚本的情况下，你对其没有读取和执行权限，shell 会报告“拒绝访问”（Permission denied）。

如果你给出一个简单的文件名作为命令，shell 会在某些目录（你的搜索路径）中搜索你想要执行的程序。它会在几个目录中查找与命令同名且你拥有执行权限（编译后的程序）或读取和执行权限（shell 脚本）的文件。`PATH` 变量控制这种搜索。

## 320 第 9 章 BOURNE SHELL

`PATH` 的默认值是在 bash 编译时确定的。它没有在启动文件中设置，尽管可以被修改。通常，默认值指定 shell 搜索用于查找常用命令的系统目录。这些系统目录包括 `/bin` 和 `/usr/bin` 以及其他适用于本地系统的目录。当你给出一个命令时，如果 shell 在 `PATH` 中的任何目录中都没有找到由命令命名的可执行文件（在 shell 脚本的情况下，为可读文件），shell 将生成上述错误消息之一。

工作目录：`PATH` 变量指定了 shell 应该搜索目录的顺序。每个目录之间必须用冒号隔开。下面的命令设置 `PATH`，使得对可执行文件的搜索从 `/usr/local/bin` 开始。如果在该目录中没有找到该文件，shell 将在查找 `/bin`，而不是 `/usr/bin`。如果在这些目录中搜索失败，shell 将查找 `~/bin`，它是用户主目录的一个子目录。导出 `PATH` 使其值对子 shell 可用：

```bash
$ export PATH=/usr/local/bin:$bin:/usr/bin:-
```

字符串中的空值表示工作目录。在前面的示例中，空值（冒号和行尾之间没有任何）作为字符串的最后一个元素出现。工作目录由开头的冒号（不建议；见安全提示）、结尾的冒号（如示例所示）或字符串中相邻冒号表示。你也可以用点 (.) 显式表示工作目录。

由于 Linux 将许多可执行文件存储在名为 bin（二进制）的目录中，用户通常将可执行文件放在自己的 `~/bin` 目录中。如果你将 bin 目录放在 `PATH` 的末尾（如前面的示例所示），shell 将查找在 `PATH` 之前的目录中无法找到的命令。

## PATH 与安全

安全：当考虑安全性时，不要将工作目录放在 `PATH` 中。如果你正在使用 root，永远不要将工作目录放在 `PATH` 中。root 的 `PATH` 完全省略工作目录是常见的情况。你始终可以通过在名称前加上 `./` 来执行工作目录中的文件：`./myfile`。

将工作目录放在 `PATH` 中可能会创建一个安全漏洞。大多数人在进入目录时输入的第一个命令是 `ls`。如果所有者在该目录下放置了一个名为 `ls` 的可执行文件，且工作目录出现在用户的 `PATH` 中，那么在该目录下执行命令的用户将执行工作目录中的 `ls` 程序，而不是系统的 `ls`，这可能导致意外的结果。

如果你想将目录添加到 `PATH`，可以在设置新值时引用 `PATH` 变量的旧值（但注意安全提示）。下面的命令将 `/usr/local/bin` 添加到当前 `PATH` 的开头，并将用户主目录下的 bin 目录 (~/bin) 添加到：

```bash
$ PATH=/usr/local/bin:$PATH:~/bin
```
