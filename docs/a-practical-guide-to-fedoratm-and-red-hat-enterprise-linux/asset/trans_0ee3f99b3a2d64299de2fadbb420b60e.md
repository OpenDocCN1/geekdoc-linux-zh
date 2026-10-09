

## declare：列出并为变量设置属性

**declare** 内建命令用于列出 shell 变量并设置其属性和值。**type set** 内建命令（**declare** 的另一个名称）执行相同的功能，但已废弃。表 9-3 列出了这些属性中的五个。

| **属性** | **含义** |
| :--------- | :--------- |
| -a | 声明变量为数组（第 1038 页） |
| -f | 声明变量为函数名（第 396 页） |
| -i | 声明变量为整型（第 358 页） |
| -r | 使变量变为只读；等效于 **readonly**（前一页） |
| -x | 使变量成为环境变量；等效于 **export**（第 1032 页） |

以下命令声明了多个变量并设置了某些属性。第一行声明 **person1** 并将其初始化为 **max**。无论是否使用 **declare** 这个词，该命令的效果都相同。

```
$ declare person1=max 
$ declare -r person2=zach 
$ declare -rx person3=helen 
$ declare -x person4
```

**readonly** 和 **export** 内建命令分别是命令 **declare -r** 和 **declare -x** 的同义词。你可以声明变量而不对其进行初始化，如前面 **person4** 变量的声明所示。此声明使 **person4** 成为环境变量，因此它对所有子 shell 可用。在 **person4** 被初始化之前，它的值为空。

你可以单独按任意顺序列出 **declare** 的选项。以下命令等价于前面 **person3** 的声明：

```
$ declare -x -r person3=helen
```

当你想要从变量中移除某个属性时，使用 + 号代替 - 号。你无法移除只读属性。执行以下命令后，变量 **person3** 不再被导出，但它仍然是只读的：

```
$ declare +x person3
```

有关导出变量的更多信息，请参阅第 1032 页。

在没有参数或选项的情况下，**declare** 列出所有 shell 变量。当你运行不带任何参数的 **set** 时（第 1025 页），也会输出相同的列表。

如果你调用 **declare** 时带有选项但没有变量名，该命令将列出所有设置了指定属性的 shell 变量。例如，命令 **declare -r** 显示所有只读变量的列表。这个列表与不带任何参数的 readonly 命令产生的列表相同。在执行前例中的声明后，结果如下：

```
$ declare -p
declare -r BASHOPTS="checkwinsize:cmdhist:expand_aliases: ..."
declare -ir BASHPID
declare -ir BASH_VERSINFO=([0]="4" [1]="2" [2]="24" [3]="1" ...)
declare -ir EUID="500"
declare -ir PPID="1936"
declare -r SHELLOPTS="braceexpand:emacs:hashall:hists:hashall:histexpand: ..."
declare -ir UID="500"
declare -r person2="zack"
declare -rx person3="helen"
```

前七个条目是关键字变量，它们自动被声明为只读。其中一些变量以整数形式存储（-i）。-a 选项表明 `BASH_VERSINFO` 是一个数组变量；数组中每个元素的值列在等号右侧。

### 整数

默认情况下，变量的值以字符串形式存储。当你对字符串变量进行算术运算时，shell 会将变量转换为数字，对其进行操作，然后再将其转换回字符串。具有整数属性的变量以整数形式存储。按如下方式分配整数属性：

```
$ declare -i COUNT
```

你可以使用 `declare` 显示整型变量：

```
$ declare -i
declare -ir BASHPID
declare -i COUNT
declare -ir EUID=1000
declare -i HISTCMD
declare -i LINENO
declare -i MAILCHECK=60
declare -i OPTIND=1
...
```

## BASH 关键字变量

关键字变量要么是由 shell 在启动时继承或声明并初始化的。你可以从命令行或启动文件中为这些变量赋值。通常，这些变量是环境变量（已导出），因此它们不仅对登录 shell 可用，也对你启动的所有子 shell 可用。

### HOME：你的主目录

默认情况下，你的主目录是登录时的工作目录。你的主目录在你的账户建立时确定；其名称存储在 `/etc/passwd` 文件中。

```
$ grep sam /etc/passwd
sam:x:500:500:Sam the Great::/home/sam::/bin/bash
```

登录时，shell 继承你主目录的路径名，并将其分配给环境变量 **HOME**。当你执行不带参数的 `cd` 命令时，`cd` 将存储在 **HOME** 中的目录名称作为工作目录：

```
$ pwd
/home/max/laptop
$ echo $HOME
/home/max
$ cd
$ pwd
/home/max
```

此示例显示了 **HOME** 变量的值以及 `cd` 内建命令的效果。执行不带参数的 `cd` 后，工作目录的路径名与 **HOME** 的值相同：你的主目录。

## 波浪号 (~)

shell 使用 **HOME** 的值来展开使用简写波浪号 (~) 表示法（第 182 页）来表示用户主目录的路径名。以下示例使用 `echo` 显示此快捷方式的值，然后使用 `ls` 列出 Max 的笔记本电脑目录中的文件，该目录是其主目录的一个子目录。

```
$ echo ~
/home/max
$ ls ~/laptop
tester  count  lineup
```

## PATH：Shell 查找程序的地方

当你向 shell 提供绝对或相对路径名作为命令时，它会查找指定目录中具有指定文件名的可执行文件。如果指定路径名的文件不存在，shell 报告 **No such file or directory**（没有这样的文件或目录）。如果文件按指定存在，但你没有其执行权限，或者对于 shell 脚本你没有读和执行权限，shell 报告 **Permission denied**（权限被拒绝）。

当你提供一个简单的文件名作为命令时，shell 会搜索某些目录（你的搜索路径）以查找你要执行的程序。它在几个目录中查找与命令同名且你具有执行权限（编译后的程序）或读和执行权限（shell 脚本）的文件。**PATH** 变量控制此搜索。

**PATH** 的默认值在编译 `bash` 时确定。它不在启动文件中设置，尽管可能会在那里修改它。通常，默认值指定 shell 搜索几个用于存放常见命令的系统目录。这些系统目录包括 `/usr/bin` 和 `/usr/sbin` 以及适合本地系统的其他目录。当你发出命令时，如果 shell 在 **PATH** 中列出的任何目录中找不到可执行（对于 shell 脚本是可读）且名称与命令匹配的文件，shell 将生成上述错误消息之一。

工作目录
**PATH** 变量指定了目录的顺序，shell 应按此顺序搜索它们。每个目录必须用冒号与下一个目录分隔。以下命令设置 **PATH**，使得对可执行文件的搜索从 */usr/local/bin* 目录开始。如果它没有在此目录中找到文件，shell 接下来会在 */usr/bin* 中查找。如果在这些目录中搜索失败，shell 会在 *~bin* 目录中查找，这是用户主目录的一个子目录。最后，shell 会在工作目录中查找。导出 **PATH** 确保它是环境变量，因此它对子 shell 可用，尽管通常在其声明时已导出，因此再次导出并不必要：

```
$  export PATH=/usr/local/bin:/usr/bin:~/bin:
```

字符串中的空值表示工作目录。在前面的示例中，一个尾随冒号（冒号和行尾之间没有任何内容）作为字符串的最后一个元素出现。工作目录由前导冒号表示（不推荐；参见以下安全提示）、尾随冒号（如示例所示）或字符串中任意位置的两个相邻冒号表示。你也可以使用句点 (.) 显式表示工作目录。

因为 Linux 将许多可执行文件存储在名为 **bin**（*binary*）的目录中，用户通常将其可执行文件放在自己的 *~bin* 目录中。如果你将自己的 **bin** 目录放在 **PATH** 的末尾，如前面的示例所示，shell 会在 **PATH** 中前面列出的目录中找不到任何命令时，在此处查找。

如果你想向 **PATH** 添加目录，可以在将 **PATH** 设置为新值时引用 **PATH** 变量的旧值（但参见以下安全提示）。以下命令在当前的 **PATH** 开头加上 */usr/local/bin*，并在末尾加上用户主目录中的 **bin** 目录 (*~bin*)：

在 *~/bash_profile* 中设置 **PATH**；参见第 331 页的提示。

```
$  PATH=/usr/local/bin/:$PATH:~/bin
```

### PATH 与安全

在安全受关注时，不要在 **PATH** 中把*工作目录*放在首位。如果你以 **root** 身份工作，你*永远*不应把工作目录放在 **PATH** 的首位。**root** 的 **PATH** 通常会完全省略工作目录。你总是通过在名称前加 *./ 来执行工作目录中的文件：*./myprog*。

在工作目录中放置可执行文件会在 **PATH** 中把工作目录放在首位可能会创建安全漏洞。大多数人进入目录时输入的第一个命令是 **ls**。如果目录的所有者在该目录中放了一个名为 **ls** 的可执行文件，且工作目录出现在用户的 **PATH** 中首位，那么用户从该目录发出的 **ls** 命令将执行工作目录中的 **ls** 程序，而不是系统的 **ls** 实用程序，这可能会产生不良后果。

## MAIL：邮件存储位置

**MAIL** 变量通常包含保存你邮件的文件的路径名（你的*邮箱*，通常是 */var/mail/name*，其中 *name* 是你的用户名）。但是，你可以使用 **MAIL** 监控任何文件（包括目录）：将 **MAIL** 设置为你想要监控的文件名。

