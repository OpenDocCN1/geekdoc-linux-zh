
# 高级 Bash 脚本指南：Shell 脚本艺术的深度探索

本教程假设读者对脚本或编程没有基础知识，但会快速向中高级教学水平进阶（……其中穿插了许多 UNIX 智慧和技巧）。它可以作为教科书、自学手册，以及脚本技术的参考资料和知识源。练习题和注释良好的示例邀请读者积极参与，其前提是学习脚本的唯一方法就是编写脚本。

本文档的最新更新是一个包含 SGML 源码和渲染后 HTML 的归档“tarball”，可以从[作者主页]()() 下载。请查看[变更日志](_) 获取修订历史。

## 献辞

献给 Anita，所有魔法的源泉

## 第 1 章 为什么要学习 Shell 编程？

对于每个希望精通系统管理的人来说，掌握 Shell 脚本的使用知识都是至关重要的，即使他们预计自己永远不需要编写脚本。想象一下当 Linux 机器启动时，它会执行 `/etc/rc.d` 中的脚本来恢复系统配置并设置服务。深入理解这些启动脚本对于分析系统行为以及可能对其进行修改非常重要。

编写脚本并不难学，因为脚本可以拆分成较小的系统来构建，而且只需要学习一小部分 Shell 特有的操作符和操作。其语法简单直观，类似于在命令行中调用和链式组合实用程序，并且只有少数“规则”需要学习。大多数脚本在第一次运行时就能成功，而较长脚本的调试也十分直观。

Shell 脚本是复杂应用程序的一种“快速且粗暴”的原型方法。即使给 Shell 脚本提供有限的功能子集，即使速度缓慢，通常也是开发过程中用的用的阶段。然后就可以对应用程序的结构进行测试和尝试，并在进行 C、C++、Java 或 Perl 最终编码之前发现主要的陷阱。

Shell 脚本回归了 Unix 的方式，即将复杂项目拆分为子任务，并将组件和实用程序链在一起。许多人认为，这种解决问题的方法（或至少在审美上更优）优于使用那种一代强大的全能语言（如 Perl），这些语言试图满足所有人的需求，但代价是迫使你改变自己的思维模式来适应工具。

### 何时不该使用 Shell 脚本

- 资源密集型任务，且速度是因素时（排序、哈希处理等）
- 涉及重度操作的过程，特别是浮点运算、任意精度计算或复数（请改用 C++ 或 FORTRAN）
- 需要跨平台可移植性（请改用 C）
- 复杂应用程序，结构化编程是必须的（需要变量类型检查、函数原型等）
- 任务关键型应用，尤其是当你处于开发一线或关乎公司未来时
- 安全性重要的场合，你需要保证系统的完整性并防止入侵、破解和破坏
- 项目由具有相互依赖关系的子系统组成
- 需要大量的文件操作（Bash 仅限于顺序文件访问，而且仅是以一种特别笨拙低效的逐行方式进行）
- 需要多维数组
- 需要数据结构，如链表或树
- 需要生成或处理图形或 GUI
- 需要直接访问系统硬件
- 需要端口或套接字 I/O
- 需要使用库或与旧代码接口
- 专有的、闭源应用程序（Shell 脚本本质上是开源的）

如果上述任何情况，请考虑使用更强大的脚本语言，可能是 Perl、Tcl、Python，或者可能是高级编译型语言（如 C、C++ 或 Java）。即便如此，将 Shell 脚本作为应用程序原型可能也是一个有用的开发步骤。

# 高级 Bash 脚本指南

我们将使用 Bash，它是“Bourne–Again Shell”（再次 Bourne 的 Shell）的缩写，也是对 Stephen Bourne 的经典 Bourne Shell 的一个双关语。Bash 已成为所有变体 UNIX 上 shell 脚本的事实标准。本书涉及的大多数原则也同样适用于其他 shell 脚本，例如 Korn Shell（Bash 从其继承了某些功能，[2]）以及 C Shell 及其变体。（请注意，由于某些固有问题，不建议使用 C Shell 编程，正如 Tom Christensen 在 1993 年 10 月在某个新闻组帖子中所指出的那样）。

以下是一个 shell 脚本教程。它高度依赖示例来说明 shell 的功能。在尽可能的情况下，示例脚本都经过了测试，其中一些在现实生活中实际上是很有用的。读者理应当使用源归包中的实际示例（通过 `chmod u+rx something-or-other.sh`，[3] 赋予它们执行权限），然后运行它们查看会发生什么。如果没有源归包，则可以从 HTML、pdf 或文本渲染版本中剪粘贴。请注意，下面的某些脚本在解释之前就引入了特性，这可能要求读者临时跳读以获得启示。

除非另有说明，后续的示例脚本均由作者编写。

## 第 1 章。为什么要进行 shell 编程？

## 第 2 章。从 Sha-Bang 开始

在最简单的情况下，脚本无非是存储在文件中的系统命令列表。至少，这节省了每次调用时都重新输入该特定序列命令的精力。

### 示例 2–1. cleanup：一个清理 /var/log 中日志文件的脚本

```bash
# cleanup
# 当然，要以 root 身份运行。

cd /var/log
cat /dev/null > messages
cat /dev/null > wtmp
echo "Logs cleaned up."
```

这里没什么特别的，只是一组可以从控制台或 xterm 中的命令行轻松调用的命令。将命令放置在脚本中的优势在于不再需要反复输入。此外，脚本可以针对特定应用程序方便地修改、定制或通用化。

### 示例 2–2. cleanup：上述脚本的增强和通用化版本。

```bash
#!/bin/bash
# cleanup, version 2
# 当然，要以 root 身份运行。

LOG_DIR=/var/log
ROOT_UID=0          # 只有 UID 0 的用户拥有 root 权限。
LINES=50            # 默认保存行数。
E_XCD=66             # 无法更改目录？
E_NOTROOT=67         # 非 root 退出错误。

if [ -ne "$ROOT_UID" ];
then
    echo "Must be root to run this script."
    exit $E_NOTROOT
fi

if [ -n "$1" ];
    # 测试是否存在命令行参数（非空）。
then
    lines=$1
else
    lines=$LINES # 如果未在命令行指定，则使用默认值。
fi

# Stephanie Chazelas 遵循以下方法
# 作为检查命令行参数的更好方法，
# 但对于教程的这个阶段来说仍然有点高级。

    E_WRONGARGS=65     # 非数值参数（参数格式错误）
    case "$1" in
```

## 高级 Bash 脚本指南

```bash
# == lines=50;
# *[!0-9]*) echo "Usage: $basename $0" file-to-cleanup"; exit $E_WRONGARGS;
# # lines=$1;
esac
```

跳到“循环”章节以理解。

```bash
$LOG_DIR
if [ 'pwd' != "$LOG_DIR" ] # 或者如果 [ "$PWD" != "$LOG_DIR" ]
# 不在 /var/log 中？
then
echo "Can't change to $LOG_DIR"
exit $E_XCD
fi # 在处理日志文件之前，双检查是否在正确的目录。
```

```bash
# 更好的是：
#
# cd /var/log || {
  echo "Cannot change to necessary directory." >&2
  exit $E_XCD
}
```

```bash
tail -$lines messages > mesg.tmp # 保存日志文件的最后一部分。
mv mesg.tmp messages # 成为新文件。
```

```bash
# cat /dev/null messages
# 不再需要，因为上面的方法更安全。
```

```bash
cat /dev/null ~wtmp # ~wtmp 的效果相同。
echo "Logs cleaned up."
```

```bash
exit 0
# 脚本退出时返回零值
# 向 shell 表示成功。
```

由于你可能不想擦除整个系统，第一个脚本的这个变体保留了日志文件的最后部分。你将不断发现完善脚本以提高效率的方法。

脚本开头的 `sha-bang` (#) 告诉你的系统这是一组要传递给命令解释器的命令。# 实际上是一个双字节的“魔术数字”，一种用于指定文件类型的特殊标记，或者在可执行 shell 的情况下（关于这一迷人主题的详情，请参见 `man magic`）。紧随 `sha-bang` 之后是一个路径名。这是解释命令的程序路径，无论它是 shell、编程语言还是工具。该命令解释器执行脚本顶部的命令（脚本的第 1 行），[5]

```bash
#!/bin/sh
#!//bin/bash
#!//usr/bin/perl
#!//usr/bin/tcl
#!//bin/sed -f
#!//usr/awk -f
```

## 第 2 章。从 Sha–Bang 开始

# 高级 Bash 脚本指南

脚本头部的每一行都会调用不同的命令解释器，或者 `/bin/sh`（大多数商业变体 UNIX 的默认值，Linux 系统中为 bash）或其他。[6] 使用 `#!/bin/sh`（大多数商业变体 UNIX 的默认 Bourne Shell）可以将脚本移植到非 Linux ，尽管你可能需要牺牲一些 Bash 特性（脚本将符合 POSIX [7] 标准）。

请注意，“sha-bang”处给出的路径必须正确，否则运行脚本的唯一结果将是错误信息，通常为“找不到命令”。

如果脚本只包含通用系统命令且不使用内部指令，则可以省略 `#!`。上面的示例 2 需要初始的 `#!`，变量赋值行 `line=50` 使用了 shell 特有的结构。请注意 `#!/bin/sh` 调用的是默认解释器，它在 Linux 机器上默认为 `/bin/bash`。

![](img/1ce1edffaa36e4f698a85430e71c6d3b_10_0.png)

本教程鼓励使用模块化方法构建脚本。注意并收集未来脚本中可能有用的“样板”代码段。最终，你可以建立一个相当实用的例程库。例如，下面的脚本引导测试了脚本是否用正确数量的参数调用。

```bash
if [ $# -ne Number_of_expected_args ]
then
    echo "Usage: basename $0 whatever"
    exit WRONG_ARGS
fi
```

### 2.1. 调用脚本

编写脚本后，你可以通过 `sh scriptname` [18] 调用它，或者改为使用 `bash scriptname`。（不建议使用 `sh <scriptname`，因为这实际上禁用了脚本内部从标准输入读取。）更方便的方法是使用 `chmod` 使脚本本身直接执行。

可以使用：

```bash
chmod 555 scriptname（赋予所有人读/执行权限） [9]

chmod +rx scriptname（赋予所有人读/执行权限）

chmod u+ scriptname（仅赋予所有者读/执行权限）
```

或者

赋予执行执行后，你现在可以通过 `./scriptname` 测试它。[10] 如果它以“sha-bang”行开头，脚本将调用正确的解释器来运行。

作为最后一步，在测试和调试之后，你可能想将其移动到 `/usr/local/bin`（当然要以 root 身份），以便你自己和其他所有用户都能作为系统级执行文件使用。这样只需从命令行输入 `scriptname` [回车] 即可调用脚本。

### 2.1. 调用脚本

* 这

### 2.2. 预练习

+   1. 系统管理员编写脚本来自动化常见任务。给出此类脚本有实例。
2. 编写一个脚本，在调用时显示日期、列出所有登录用户并提供系统运行时间。脚本将这些信息保存到日志文件中。

## 第二部分 基础知识

+   目录
3. 退出与退出状态
4. 特殊字符
5. 变量与参数介绍
   5.1 变量替换
   5.2 变量赋值
   5.3 Bash 变量是无类型的
   5.4 特殊变量类型
6. 引用
7. 测试
   7.1 测试结构
   7.2 文件测试操作符
   7.3 比较运算符（二进制）
   7.4 嵌套 if/then 条件测试
   7.5 测试你的测试知识
8. 操作与相关主题
   8.1 操作符
   8.2 数值常量

## 第 3 章 退出与退出状态

...Bourne shell 中有很多阴暗的角落，人们利用了其中所有的角落。

Bret Ramey

`exit` 命令可以终止脚本，就像在 C 语言中一样。它还可以返回一个值，该值对脚本的父进程是的。

每个命令都会返回一个退出状态（有时称为返回状态）。执行成功的命令返回 0，而失败的命令返回一个非零值，该值通常可以被解释为错误代码。良好的 UNIX 命令、程序和实用程序在完成后会返回 0 退出码，尽管存在一些例外情况。

同样，脚本内部的函数和脚本本身也会返回退出状态。函数或脚本中最后执行的命令决定了退出状态。在脚本中，可以使用 `exit` 向 shell传递一个 `nnn` 退出状态（`nnn` 必须是 0–255 范围内的数字）。

![](img/1ce1edffaa36e4f698a85430e71c6d3b_12_0.png)

当脚本以一个不带参数的 `exit` 结束时，脚本的退出状态是脚本中最后执行的命令的退出状态（不计 `exit` 本身）。

`$?` 读取最后执行命令的退出状态。在函数执行之后，`$?` 给出最后执行命令的退出状态。这是 Bash 给函数提供“返回值”的方法。在脚本终止后，从命令行输入的 `$?` 提供脚本的退出状态，即脚本中最后执行的命令，按照习惯，成功返回 0，错误返回 1–255 范围内的整数。

### 示例 3–1. exit / 退出状态

```bash
#!/bin/bash
echo hello
echo $? # 因为命令执行成功，返回退出状态 0。
lsdkf # 无法识别的命令。
echo $? # 因为命令执行失败，返回非零退出状态。
echo
exit 113 # 将向 shell 返回 113。
# 要验证这一点，在脚本终止后输入 "echo $?"。

# 习惯，'exit 0' 表示成功，
# 而非零退出值意味着错误或异常情况。
```

`$?` 特别适用于测试脚本中命令的结果（示例 12–8 和示例 12–13）。

![](img/1ce1edffaa36e4f698a85430e71c6d3b_12_1.png)

逻辑“非”限定符会反转测试或命令的结果，这会影响它的[退出状态](exit status)。

### 示例 3–2. 使用 ! 取反条件

```bash
true # 内置命令 "true"。 
echo "exit status of \"true\" = $?  # 0

! true
echo "exit status of !true\" = $?  # 1
# 注意 "!" 后面需要一个空格。
# !true 会导致“command not found”错误
# 感谢，S.C.
```

某些退出状态代码有[保留的含义](reserved meanings)，不应在脚本中由用户指定。

## 第 4 章 特殊字符

位于脚本及其他地方的特殊字符

**注释。** 以 # 开头的行（#! 除外）都是注释。

```bash
# 这一行是一条注释。
```

注释也可以出现在命令的末尾。

```bash
echo "A comment will follow." # 这里是注释。
```

注释也可以出现在行首的空白之后。

```bash
# 此注释前有一个制表符。
```

![](img/1ce1edffaa36e4f698a85430e71c6d3b_14_0.png)

命令不能紧跟在同一行的注释之后。没有什么方法可以在同一行内终止注释。使用新行来让“代码”开始。

在某些情况下，转义的 `#` 不会开始注释。

```bash
echo "The # does not begin a comment."
echo 'The # does not begin a comment.'
echo The # here does not begin a comment.
echo The # here begins a comment.
```

```bash
echo ${PATH*:} # 参数替换，不是注释。
echo $((2*1011)) # 转换，不是注释。
```

感谢，S.C.

转义字符 `\"` 会转义 `#`。

某些模式匹配操作也使用 `#`。

**命令分隔符。** [分号] `;` 允许在同一行内放置两个或多个命令。

```bash
echo hello; echo there
```

注意 `:` 有时需要转义。

`case` 选项中的终止符。

```bash
case "$variable" in
abc)    echo "$variable";;;
xyz)    echo "$variable";;;
esac
```

“点”命令。[点] `.` 等于 1–14。在不同的上下文中，作为正则表达式的一部分，`.` 匹配单个字符。在另一个上下文中，`.` 是文件名前缀，`ls` 通常会显示。



# 高级 Bash 脚本指南

## 第 4 章 特殊字符

```bash
$ touch .hidden-file
$ ls -al
total 10
--rw-r-- 1 user 0 18 22 .addressfile
--rw-r-- 1 group 0 25 13 .addressbook
--rw-r-- 1 group 0 17 00 .addressbook.bak
--rw-r-- 1 user 0 29 54 .hidden-file
drwxr-xr-x 3 group 4096 18 22 ..
drwx------ 2 group 0 25 13 .
--rw-r-- 1 group 0 17 00 .addressbook.bak
drwxr-xr-x 3 user 4096 18 22 .addressfile
--rw-r-- 1 user 0 29 54 .hidden-file
```

部分引用。`"` 保留了字符串中的大部分特殊字符。见第 6 章。

全引用。`'` 保留了字符串中的所有特殊字符。这是使用第 6 章的一种强引用形式。

逗号运算符。逗号运算符连接一系列算术操作。所有操作都会求值，但只有最后一个会被赋值。

```bash
let a = 9, b = 10
```

转义。`\` 转义字符 `X`。这具有引用 `X` 的效果。`\'` 用于字面量引用。

### 文件名分隔符

`/` 分隔文件名的组成部分（如 `/home/projects/`）。这也是除法运算符。

### 命令替换

`` `command` `` 使 `command` 的输出可用于设置变量。也被称为反引号。

### 空命令

`:` 在 shell 中相当于 `NOP`（无操作）。`:` 命令是 `Bash` 内置命令，它的退出状态为 `0`。

```bash
echo $? # 0
```

无限循环：

```bash
while true
do
  operation-1
  operation-2
  ...
  operation-n
done
```

`if/then` 测试中的占位符：

```bash
if condition
then
    : # 什么都不做
else
  take-some-action
fi
```

在期望二进制的地方占位符，见示例 8–2 和默认参数。

```bash
$ $(username=whoami) 没有前导符会报错
# 除非 "username" 是命令或内置命令...
```

在此文档（here document）中期望命令的地方提供占位符。见示例 1–8。

使用参数替换求值变量字符串（如示例 9–12）。

```bash
${HOSTNAME} ${USER} ${MAIL}
# 如果一个或多个基本环境变量未设置，则打印错误信息。
```

变量扩展。结合 `>` 运算符使用，可以将文件截断为零长度而不改变其属性。如果文件之前不存在，则创建它。

```bash
> data.xxx # 文件 "data.xxx" 现在为空。
# 效果等同于 cat /dev/null >data.xxx
```

结合 `>>` 运算符使用，更新文件的访问/修改时间。这等同于 `touch`。

![](img/1ce1edffaa36e4f698a85430e71c6d3b_17_0.png)

这适用于普通文件、管道、符号链接和特殊文件。

可以用来开始注释行，但不建议这样做。使用 `#` 作为注释会关闭对该行剩余部分的检查，因此任何内容都可以位于注释中。然而，`:` 并非如此：

```bash
> : 这是一个会产生错误的注释（如果 $ x -eq 3 ）。
```

`:` 作为字段分隔符存在于 `/etc/passwd` 中以及 `PATH` 变量中。

```bash
echo $PATH
/usr/local/bin:/usr/bin:/usr/X11R/bin:/bin:/usr/sbin:/sbin:/usr/games
```

反转（或否定）测试或退出状态的意义。`!` 运算符反转其应用的命令的退出状态（示例 3–2），意味着一个测试运算符。这可以将“等于” (`=`) 的意义变为“不等于” (`!`)。`!` 也是 `Bash` 的一个关键字。

在另一个上下文中，`!` 也出现在间接变量引用中。

![](img/1ce1edffaa36e4f698a85430e71c6d3b_17_1.png)

### 通配符

`*` 字符在文件名扩展（globbing）中用作“通配符”，在正则表达式中表示任意数量（或零）字符。

双星号 `**` 是幂运算符。

`?` 字符在通配符（globbing）中作为单字符“文件名通配符”，在扩展正则表达式中也表示一个字符。

在双括号内，`?` 作为 C 风格的三元运算符使用。示例 9–25。

### 变量替换

`$` 是变量替换前缀。

```bash
var1=5
var2=23skidoo
echo $var1    # 5
echo $var2    # 23skidoo
```

在正则表达式中，`$` 匹配行尾。

### 参数替换

`${*}` 和 `${@}`

### 位置参数

`()`, `()`, `[ ]`, `[[ ... ]]`, `(( ... ))`, `>`, `>>`, `<`

### 命令组

```bash
(a=hello; echo $a)
```

![](img/1ce1edffaa36e4f698a85430e71c6d3b_18_0.png)

圆括号内的命令列表会启动一个子 shell（subshell）。

子 shell 内括号内的变量对脚本的其他部分不可见。父进程（脚本）无法读取在子进程（子 shell）中创建的变量。

```bash
a=123
( a=321; "$a")
echo "$a"    # a = 123
      # "$a"   在括号内的作用类似于局部变量。
```

### 数组初始化

```bash
Array={element1 element2 element3}
{xxx,yyy,zzz,...}
```

### 大括号扩展

```bash
grep Linux file.*{txt,htm}
# 在 fileA.txt, "file2.txt", "fileR.html", "file-87.htm" 等文件中
# 单词 "Linux" 的所有实例
```

命令可以接受大括号之间用逗号分隔的文件规格列表。文件名扩展（通配符）适用于大括号之间的文件空间。

![](img/1ce1edffaa36e4f698a85430e71c6d3b_19_0.png)

大括号内不允许有空格，除非空格被引用或转义。

```bash
echo {file1,file2}\: \A, "B", 'C'
file1 : A file1 : B file : C file2
: A file2 : B file2 : C
```

### 代码块

也称为“内联组”（inline group），这种结构实际上创建了一个匿名函数。与函数不同，代码块中的变量将持续到脚本的剩余部分。

```bash
bash { local a; a=123; }
bash: local: can only be used in a function
```

```bash
a=123
{ a=321; }
echo "a = $a"    # a = 321    (代码块内部的值)

# 感谢 S.C.
```

大括号包裹的代码块可以对其进行 I/O 重定向。

#### 示例 4–1. 代码块和 I/O 重定向

```bash
#!/bin/bash
# 读取 /etc/fstab 中的行

File=/etc/fstab
{
read line1
read line2
} <$File
echo "First line in $File is:"
echo "$line1"
echo
echo "Second line in $File is:"
echo "$line2"

exit 0
```

与上述圆括号内的命令组不同，由花括号 `{}` 包围的代码块**不**通常会启动一个子 shell。

### 路径（pathname）

最常用于 `find` 结构。这不是一个 shell 内置命令。

`\\` 结束 `-exec` 命令序列。它需要转义以防止被 shell 解释。

```bash
{\\:
```

`test` 命令。`[ ]` 之间的表达式。它是 shell 内置命令 `test` 的同义词，而不是外部命令 `/usr/bin/test`。

```bash
[]
```

`test` 命令。`[[ ... ]]` 之间的表达式。参见 `[[ ... ]]` 结构。

```bash
[]
```

整数扩展。`(( ... ))` 之间的表达式。参见 `(( ... ))` 结构。

```bash
()
```

重定向。

`>`, `>>`, `<`

`scriptname > filename` 将 `scriptname` 的输出重定向到 `filename`。如果文件已存在则会覆盖。

`scriptname >> filename` 将 `scriptname` 的输出追加到 `filename`。如果文件不存在，则会创建。

```bash
command >
```

进程替换。`<(command)`

```bash
<(command)>
```

在不同的上下文中，`<` 和 `>` 字符作为字符串比较运算符。在另一个上下文中，`<` 和 `>` 字符作为整数比较运算符。

在此文档（here document）中使用重定向 `<<`。

### 管道

将上一个命令的输出传递给下一个命令，或 shell。这是一种链接命令的方法。

```bash
echo ls -1 | sh
# 将 "echo ls -1" 的输出传递给 shell
# 结果与简单的 "ls -1" 相同。
```

```bash
cat *.lst | sort
# 合并并排序所有 ".lst" 文件，然后删除重复行。
```

管道作为进程通信的经典方法将一个进程的 `stdout` 发送到另一个进程的 `stdin`。在通常情况下，如 `cat` 或 `echo` 等命令会将数据流管道到过滤器。

```bash
cat $filename | grep $search_word
```

命令或命令的输出可以管道到脚本。

```bash
#!/bin/bash

# uppercase.sh : 将输入转换为大写

tr 'a-z' 'A-Z' # 范围必须加引号以防止生成单个字符的文件。
```

现在，将 `ls -1` 的输出管道到 `uppercase.sh`。

```bash
bash ls -1 | /uppercase.sh
```

```bash
variable="initial_value"

echo "new_value" | read variable

echo "$variable" = initial_value
```

管道中每个进程的 `stdout` 必须作为下一个进程的 `stdin` 读取。如果不是这种情况，数据流将被阻塞，管道将无法按预期工作。

```bash
file2

# "cat file2" 的输出出现
```

管道运行子进程，因此无法更改变量。

### 强制重定向（即使设置了 `noclobber` 选项）

这将覆盖现有文件。在后台运行作业。命令后跟 `&` 将后台运行。在脚本内部，命令和循环可以在后台运行。

```bash
sleep 10 &
```

#### 示例 4–3. 在后台运行循环

```bash
#!/bin/bash

# background-loop.sh

for i in 2 3 4 5 6 7 8 9 10
do
    echo -n "$i"
done & # 在后台运行。有时会在第二个循环后执行。

echo

# 这个 'echo' 有时不会显示。
```

### 按键

坦率说，这有解决办法。从 `stdin` 到 `stdout` 的重定向。

```bash
cd /source/directory && tar cf - | (cd /dest/directory && tar xpvf -)

# 将整个文件树从一个目录移动到另一个 [感谢 Alan Cox <a.cox@swansea.ac.uk>]，这是一个重大变化
```

要移动的文件所在的源目录。“列表：如果 `cd` 操作成功，则执行。`c` 选项 `tar` 归档命令创建一个归包，`f` 文件选项后的 `-` 指定目标及其当前目录树 (`.`)。

1. `cd /source/directory`
2. `&&`
3. `tar cf -`
4. `|`
5. `(...)`
6. `cd /dest/directory`
7. `&&`
8. `tar xpvf -`

切换到目标目录。“列表”：同上。解压缩 (`x`)，保留所有权和文件权限 (`p` 并向 `stdout` 发送详细信息 (`v`)），从 `stdin` 读取数据 (`f` 后跟 `-`)。

管道到。注意 `x` 是一个命令，而 `p`、`v`、`f` 是选项。

一个子 shell

呼！

更优雅，但等同于：

```bash
cd source-directory
tar cf - | (cd ../target-directory; tar xf -)
cp -a /source/directory /dest 也有效果。
```

```bash
bunzip2-linux-2.4.3.tar.bz | tar xvf-

--压缩文件-- | --将其传递给 "tar"---

如果 `tar` 没有修补以处理 `bunzip2`，则需要使用管道分两个离散步骤完成。练习的目的是解压缩“压缩过的”内核源码。

注意在这种情况下，`-` 本身不是 Bash 运算符，而是 Unix 写入 stdout 时识别的选项，如 `tar`、`cal`、`cat`。
```

```bash
bash echo "whatever" | cat
whatever
```

这一次，它接受来自标准输入的输入并进行过滤。

`-` 可以将标准输出管道到其他命令。这允许进行一些技巧操作，例如在文件开头添加行。

使用 `diff` 比较文件与另一个文件的部分：

```bash
grep bash file1 | diff file2 -
```

最后，是一个使用 `tar` 的真实示例。

#### 示例 4–4. 备份昨天更改的所有文件

```bash
#!/bin/bash

# 将当前目录下在过去 24 小时内修改过的文件
# 备份到“tar 包”（tar 压缩并 gzip 文件）。

NOARGS=0
E_BADARGS=65

if [ $# == $NOARGS ]
then
  echo "Usage: basename $0 filename"
  exit $E_BADARGS
fi

find . -mtime -1 -type f -print > $1.tar
gzip $1.tar

# Stephanie Chalaz 指出，如果找到的文件过多
# 上述代码将会失败
# 如果任何文件名包含空白字符。

# 他建议了以下替代方案：
# find -mtime -1 -type f -print | xargs -0 tar rvf "$1.tar"
# 使用 GNU 版本的 "find"
# find -mtime -1 -type f -exec tar rvf "$1.tar" '{}' \; 
# 可移植到其他 UNIX 变体，但慢得多。

exit 0
```

以 `--` 开头的文件名与重定向运算符配合时会导致问题。脚本应该检查此并将此类文件名作为变量或 `$PWD` 传递。如果变量的值以 `--` 开头，可能也会创建类似的问题。

### 上一个工作目录

`cd` 切换到上一个目录。这使用了 `$PWD`。不要与 `-` 重定向混淆。`-` 取决于它出现的上下文。

重定向方向：

- `>` 将标准输出重定向到文件。
- `<` 将标准输入从文件重定向。
- `>>` 将标准输出追加到文件。
- `2>` 将标准错误重定向到文件。
- `2>&1` 将标准错误重定向到标准输出。
- `> /dev/null` 将标准输出重定向到空设备。
- `&> /dev/null` 将标准输出和标准错误都重定向。

### 减号（Minus）

算术运算中的减号。

### 等号（Equals）

赋值运算符

```bash
a=28
echo $a
```

在不同的上下文中，`=` 是字符串比较。

### 加号（Plus）

加法运算。

在不同的上下文中，`+` 是正则表达式运算符。

### 取模（Modulo）

除法的余数算术运算。

在不同的上下文中，`%` 是模式匹配运算符。

### 主目录（Home）

`~` 这对应于内部变量 `$HOME`。`~` 是用户的主目录，`ls` 列出内容。`~/` 是当前目录，`ls` 列出内容。

```bash
echo $HOME
echo ~
```

### 控制字符

- `Ctrl+C` 终止前台作业。
- `Ctrl+D` 退出 shell（类似于 `exit`）。它发送 `EOF`（文件结束符）。
- `Ctrl+J` 回车。
- `Ctrl+L` 清除终端屏幕。
- `Ctrl+M` 换行。
- `Ctrl+U` 擦除输入行。
- `Ctrl+Z` 暂停前台作业。
- `Ctrl+A` 行首。
- `Ctrl+G` 蜂鸣。
- `Ctrl+H` 退格。

```bash
#!/bin/bash
# 在字符串中嵌入 Ctrl+H。
a="*H" # 两个 Ctrl+H（退格）。
echo -n "abcdef" # 末尾有两个空格。
echo -n "abcdef$a" # abcdef
# 末尾没有空格时不退格（为什么？）。
echo; echo # 结果可能不符合预期。
```

### 空白字符（Whitespace）



空白字符由空格或制表符组成。在某些上下文中，空格是不允许的。空行没有影响。

内部字段分隔符（`IFS`）：`IFS` 是分隔字段的特殊变量。在某些命令中，它是允许的，有默认值。

## 第 5 章 变量介绍

变量是编程的核心。它们出现在脚本的各个部分，出现在算术运算和字符串解析中，是不可或缺的。变量的赋值、导出、取消设置、引用和操作。

变量的赋值。赋值出现在脚本的各个位置。语法错误。变量可以出现在双引号、单引号或不加引号的范围内。引用变量值。使用大括号 `${}` 引用变量。

# 高级 Bash 脚本指南

```bash
# 在 'read' 语句中（也是一种赋值类型）
echo -n "Enter \a\"
read a
echo "The value of \a\" is now $a"
echo
exit 0
```

### 示例 5–3. 变量赋值，普通与花哨

```bash
#!/bin/bash

a=23            # 简单情况
echo $a
b=$a
echo $b

# 现在，来点花哨的（命令替换）。

a=$(echo Hello!)   # 将 'echo' 命令的结果赋值给 'a'
echo $a
# 注意，在命令行中使用感叹号 (!) 
# 在命令行中将无法不起作用，
# 因为这会触发 Bash 的“历史机制”。
a=is -1         # 将 '-1' 命令赋值给 'a'
echo $a        # 然而，如果不加引号，会移除制表符和换行符。
echo
echo "$a"    # 带引号的变量会保留空格。
# （请参见“引用”章节。）

exit 0
```

使用 `$(..)` 机制进行变量赋值（比反引号更新的方法）

```bash
# 来自自 /etc/rc.d/rc.local
R=$(cat /etc/redhat-release)
arch=$(uname -m)
```

## 5.3. Bash 变量是无类型的

与其他编程语言不同，Bash 不按“类型”区分其变量。本质上，Bash 变量是字符字符串，但根据上下文，Bash 允许对变量进行整数操作和比较。决定因素是变量的值是否只包含数字。

### 示例 5–4. 整数还是字符串？

```bash
#!/bin/bash
# int-or-string.sh
# 整数还是字符串？

a=2334            # 整数。
let "a += 1"

echo "a = $a " 
echo
# 仍然是整数。
b=$(a/23)
# 转换为字符串。
echo "b = $b"
declare -i b
# 声明为整数没有帮助。
echo "b = $b"
# 仍然如此。

let b="+ 1"
echo "b = $b"
# 1
echo

c=2334
echo "c = $c"
d=$((c/23))
# 转换为整数。
echo "d = $d"
# 101
let d+=" 1"
# 101 + 1 =
echo "d = $d"
# 102

exit 0
```

无类型变量既是福也是诅咒。它们在脚本编写中提供了更大的灵活性（给你足够的绳子让你勒死自己），并且更容易写出代码行。然而，它们允许错误渗入，并鼓励了草率的编程习惯。

跟踪脚本变量的类型是程序员的负担。Bash 不会为你做这件事。

## 5.4. 特殊变量类型

### 局部变量 (local variables)
- 仅在代码块或函数内部可见的变量（参见函数中的局部变量）

### 环境变量 (environmental variables)
- 影响 `shell` 行为和用户界面的变量

![](img/1ce1edffaa36e4f698a85430e71c6d3b_33_0.png)

在更通用的背景下，每个进程都有一个“环境”，即一组包含进程可能引用的信息的变量。从这个意义上说，`shell` 的行为与其他进程一样。

每次 `shell` 启动，都会创建一个与其环境变量对应的变量。更新或添加新的 `shell` 变量会导致 `shell` 更新其环境，所有的 `shell` 进程（它执行的命令）都会继承这个环境。

分配给环境的空间是有限的。创建过多的环境变量或占用过多空间的变量会导致问题。

```bash
bash eval `seq 10000 | sed -e 's/.*/export var=ZZZZZZZZZZZZZZZ'`

bash du

bash: /usr/bin/du: Argument list too long
```

（感谢 S. C. 的说明，以及提供上面的示例。）

如果脚本设置了环境变量，它们需要被“导出”（`export`），这会报告给脚本本地的环境。这就是 `export` 命令的功能。

![](img/1ce1edffaa36e4f698a85430e71c6d3b_34_0.png)

脚本只能将变量导出到子进程，即只导出到该脚本启动的命令或进程。从命令行调用的脚本无法将变量导出回命令行环境。子进程无法将变量导出回产生它们的父进程。

![](img/1ce1edffaa36e4f698a85430e71c6d3b_34_1.png)

### 位置参数 (positional parameters)
- 从命令行传递给脚本的参数 – `$0`, `$1`, `$2`, `$3`... `$0` 是脚本本身的名字，`$1` 是第一个参数，`$2` 是第二个，`$3` 是第三个，依此类推。在 `$9` 之后，参数必须括在括号中。

### 示例 5–5. 位置参数

```bash
#!/bin/bash

# 调用此脚本时至少传入 10 个参数

./scriptname 1 2 3 4 5 6 7 8 9 10

echo "The name of this script is $(basename $0)"

if [ -z "$1" ]; then
    echo "The first argument is missing"
fi

if [ -z "$2" ]; then
    echo "The second argument is missing"
fi

if [ -z "$3" ]; then
    echo "The third argument is missing"
fi

if [ -z "$4" ]; then
    echo "The fourth argument is missing"
fi

if [ -z "$5" ]; then
    echo "The fifth argument is missing"
fi

if [ -z "$6" ]; then
    echo "The sixth argument is missing"
fi

if [ -z "$7" ]; then
    echo "The seventh argument is missing"
fi

if [ -z "$8" ]; then
    echo "The eighth argument is missing"
fi

if [ -z "$9" ]; then
    echo "The ninth argument is missing"
fi

if [ -z "${10}" ]; then
    echo "The tenth argument is missing"
fi
```

无类型变量是福也是诅咒。它们在脚本编写中提供了更大的灵活性（给你足够的绳子让你勒死自己），并且更容易写出代码行。然而，它们允许错误渗入，并鼓励了草率的编程习惯。

跟踪脚本变量的类型是程序员的负担。Bash 不会为你做这件事。

## 第 6 章 引用 (Quoting)

引用意味着对字符串加引号。这可以防止 `shell` 对特殊字符进行重新解释或扩展。

### 示例 6–1. 打印特殊变量

```bash
#!/bin/bash

# weirdvars.sh: 打印特殊变量。

var="\\(\$\\\\\$\

echo

IFS=''

echo $Svar       # 将 '${Svar}' 转换为空格。

echo "$Svar"    # 输出 '${Svar}'

exit 0
```

单引号（`''`）的操作方式与双引号（`""`）类似，但它不允许引用变量，`$` 的特殊含义会被关闭。在单引号内，除了 `\` 之外的每一个特殊字符都会被字面量解释。可以将单引号（“全引用”）视为一种比双引号（“部分引用”）更严格的引用方法。

由于即使是转义字符（`\`）在单引号内也会被字面解释，因此尝试在单引号内嵌套单引号将无法得到预期的结果。

![](img/1ce1edffaa36e4f698a85430e71c6d3b_39_0.png)

```bash
echo "Why can't I write 's between single quotes"

echo

# 变通方法。

echo "Why can't I write ''''s between single quotes"

# ---------- ------------------------------------------------------

# 三个单引号字符串，带有转义和带引号的单引号

# 本示例由 Stephane Chazelas 提供。
```

转义是一种对单个字符的引用方法。位于字符前的转义字符（`\`）告诉 `shell` 对该字符进行字面量解释。

![](img/1ce1edffaa36e4f698a85430e71c6d3b_39_1.png)

对于某些命令和实用程序（如 `echo`、`sed`），转义一个字符可能会产生相反的效果——它可以开启或关闭该字符的特殊含义。

#### 用于 `echo` 和 `sed` 时的某些转义字符的特殊含义

| 字符 | 含义 |
| :--- | :--- |
| `\n` | 意味着换行 |
| `\v` | 意味着回车 |
| `\t` | 意味着制表符 |
| `\w` | 意味着垂直制表符 |
| `\b` | 意味着退格 |
| `\a` | 意味着“警报”（鸣响或闪烁） |
| `\07xx` | 翻译为 `\07xx` 的八进制 ASCII 等效值 |

### 示例 6–2. 转义字符

```bash
#!/bin/bash

# escaped.sh: 转义字符

echo echo

echo "\v\v\v\v"      # 打印 \v\v\v\v

# 使用 'echo' 的 -e 选项来打印转义字符。

echo -e "\v\v\v\v"    # 打印 4 个垂直制表符。

echo -e "\042"         # 打印 " （引号，ASCII 字符42）。

# '$X' 结构使得 -e 选项不再必要。

echo '$\n'               # 换行。

echo '$\a'               # 警报（鸣响）。

# Bash 2 及更高版本允许使用 '\xxx' 结构。

echo '$\t \042 \\t'     # 由制表符包围的引号 (")。

# 将 ASCII 字符赋值给变量。

------------------------------------------------------

quote='\042'             # 将 " 赋值给变量。

echo "\$quote This is a quoted string, \$quote and this lies outside the quotes"

echo

# 在变量中拼接 ASCII 字符。

triple_underscore='\137\137\137'  # # \137 是 '_' 的八进制 ASCII 码。

echo "\$triple_underline UNDERLINE \$triple_underline"
```

```bash
ABC=$'101\102\103\010' # 101, 102, 103 是 A, B, C 的八进制。

echo $ABC

echo; echo

escape=$'\033' # 033 是 escape 的八进制。

echo \"escape\" echoes as \$escape" 无可见输出。

echo; echo

exit 0
```

查看 [示例 35–1](#) 获取关于 `$'` 字符串扩展结构的另一个示例。

`\"` 赋予引号以字面含义

```bash
echo "Hello" # Hello

echo \"Hello\", he said. # \"Hello", he said.
```

`\$` 赋予美元符号以字面含义（`$` 后的变量名不会被引用）

```bash
echo "$variable01" # 结果为 \$variable01
```

`\\` 赋予反斜杠以字面含义

> `\\` 的转义和引用行为取决于其本身是否被转义、引用，或者出现在[命令替换](#substitution) 或[在此文档](#document) 之中。

```bash
echo \z # 简单的转义引用

echo \z # \z

echo \'z' # \z

echo \"z\' # \\z

echo \"z" # \z

echo \"z" # \z
```

```bash
echo \'z\' # 命令替换

echo \'z\' # \z

echo \\\"z\\\' # \\z

echo \\\\\"z\\\' # \\\\\z

echo \\\\\\\\\"z\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\z

echo echo \"z" # \z

echo echo \"z" # \z
```

```bash
cat <<EOF # 在此文档

\z

EOF
```

# 这些示例由 Stephen Chazelas 提供。

此详细的“`if`-`test`”解释由 Stephane Chazelas 提供。

### 示例 7–1. 什么是真？

```bash
#!/bin/bash

echo

echo "Testing \"0\"

if [ 0 ] # 0

then

echo "0 is true."

else

echo "0 is false."

fi # 0 is true.

echo

echo "Testing \"1\"

if [ 1 ] # 1

then

echo "1 is true."

else

echo "1 is false."

fi # 1 is true.

echo

echo "Testing \"-1\"

if [ -1 ] # 负1

then

echo "-1 is true."

else

echo "-1 is false."

fi # -1 is true.

echo

echo "Testing \"NULL\"

if [ ] # 空条件（空条件）

then

echo "NULL is true."

else
```



```bash
echo "NULL is false."
fi # NULL is false.
echo
echo "Testing \"xyz\"
if [ xyz ] # 字符串
then
echo "Random string is true."
else
echo "Random string is false."
fi # Random string is true.
echo
echo "Testing \"\$xyz\"
if [ $xyz ] # 测试 $xyz 是否为空，但是...
# 它只是一个未初始化的变量。
then
echo "Uninitialized variable is true."
else
echo "Uninitialized variable is false."
fi
# Uninitialized variable is false.
echo
echo "Testing \-n \$xyz\"
if [ -n "$xyz" ]
# 更符合规范的写法。
then
echo "Uninitialized variable is true."
else
echo "Uninitialized variable is false."
fi
# Uninitialized variable is false.
echo
xyz=
# 已初始化，但被设置为空值。
echo "Testing \-n \$xyz\"
if [ -n "$xyz" ]
then
echo "Null variable is true."
else
echo "Null variable is false."
fi
echo
# 什么时候 "false" 是真的？
echo "Testing \$false\"
if [ "false" ]
# 看起来 "false" 仅仅是一个字符串。
then
echo "\$false\" is true." # 并且它测试为真。
else
echo "\$false\" is false.
fi
# "false" is true.
echo
echo "Testing \$false\" # 再次，未初始化的变量。
if [ "$false" ]
then
echo "\$false\" is true.
else
echo "\$false\" is false.
fi
# "false" is false.
# 现在，我们得到了预期的结果。
echo
0
```

练习。解释上述示例 7–1 的行为。

# 第 7 章. 测试

```bash
if [ condition-true ]
then
  command 1
  command 2
else
  # 可选（如果不需要可以省略）
  # 添加默认代码块，当原始条件测试为假时执行。
  command 3
  command 4
fi
```

在条件测试中，如果 `if` 和 `then` 位于同一行，必须用分号 `;` 结束 `if` 语句。`if` 和 `then` 都是关键字。关键字（或命令）开始语句，如果同一行有新语句，旧语句必须结束。

```bash
if [ -x "filename" ]; then
```

# Else if 和 elif

`elif` 是 `else if` 的缩写。其效果是在外部 `if` 内部嵌套一个 `if`。

```bash
if [ condition1 ]
then
  command1
  command2
elif [ condition2 ]
# 等同于 else if
then
  command4
else
  default
fi
```

`test condition-true` 结构与 `if [ condition-true ]` 完全等价。恰好，左括号 `[` 是一个调用 `test` 命令的标记。右括号 `]` 并不严格 way，但较新版本的 Bash 要求使用。`test` 是一个用于填充和比较字符串的 Bash 内置命令。因此，在 Bash 脚本中，`test` 不调用外部的 `/bin/test` 二进制文件（后者链接到 `/bin/[`）。

```bash
test is a shell builtin
[ is a shell builtin
[[ is a shell keyword
]] is not found
```

# 示例 7–2. [ ] 和 test 的等价性

```bash
#!/bin/bash
echo
if test -z "$1"
then
    echo "No command-line arguments."
else
    echo "First command-line argument is $1"
fi
exit 0
```

`([ ])` 结构是 `[ ]` 的 shell 等价物。这是采用自 ksh 的扩展命令。在 `[` 和 `]` 之间不会发生文件名扩展或单词分割，但存在参数扩展和命令替换。使用 `[[ ]]` 结构而不是 `[ ]` 可以防止脚本中的许多逻辑错误。例如，`&&`、`||` 和 `>` 运算符在 `[[ ]]` 测试中可以工作，尽管它们在 `[ ]` 结构中会报错。

```bash
file=/etc/passwd
if [ -e $file ]
then
    echo "Password file exists."
fi
```

# 测试

在 `if` 之后，测试命令或测试括号 `[ ]` 或 `[[ ))` 并不是严格必要的。

```bash
dir=/home/bozo
if cd "$dir" 2>/dev/null; then
    echo "Now in $dir."
else
    echo "Can't change to $dir."
fi
```

“if COMMAND” 结构返回 `COMMAND` 的退出状态。同样，测试括号内的条件可以脱离 `if` 独立存在，与列表结构结合使用。

```bash
var=20
var=22
[ "$var" -ne "$var" ] && echo "$var"
home=/home
[ -d "$home" ] || echo "home not exist."
```

`(( ))` 展开并评估算术表达式。如果表达式为零，则返回退出状态 1（假）；非零表达式返回退出状态 0（真）。这与之前讨论的 `test` 和 `[ ]` 形成对比。

# 示例 7–3. 使用 (( )) 进行算术测试

```bash
#!/bin/bash
# 算术测试。
# (( )) 结构评估数值表达式。
# 状态与 [ ] 结构相反！
(( 0 )) && echo "Exit status of ((0 ))" is $?" # 1
(( 1 )) && echo "Exit status of ((1 ))" is $?" # 0
(( 5 > 4 ))              # true
echo $?               # 0
(( 5 > 9 ))              # false
echo $?               # 1
```

## 7.2. 文件运算符

如果满足以下条件返回真：

- `-e`: 文件存在
- `-f`: 是普通文件（不是目录或设备文件）
- `-s`: 文件大小不为零
- `-d`: 是目录
- `-b`: 是块设备（软磁盘、光驱等）
- `-c`: 是字符设备（键盘、调制解调器、声卡等）
- `-p`: 是管道
- `-h`: 是符号链接
- `-L`: 是符号链接
- `-S`: 是套接字
- `-t`: 文件（描述符）与终端设备关联。此选项用于检查给定脚本的 `stdin` (`[-t 0]`) 或 `stdout` (`[-t 1]`) 是否为终端。
- `-r`: 具有读取权限（对于运行测试的用户）
- `-w`: 文件具有写入权限（对于运行测试的用户）
- `-x`: 文件具有执行权限（对于运行测试的用户）
- `-g`: 文件或目录设置组 ID (`sgid`) 标志。如果目录设置了 `sgid` 标志，则在该其中创建的文件属于该目录的组，而不是创建用户的组。这对于工作组共享的目录可能有用。
- `-u`: 文件设置用户 ID (`suid`) 标志。带有 `suid` 标志的 `root` 二进制文件即使由普通用户调用也会以 `root` 权限运行。这对于需要访问系统硬件的可执行文件（如 `pppt` 和 `cdrecord`）非常有用。缺少 `suid` 标志会导致这些二进制文件无法被非 `root` 用户调用。带有 `suid` 标志的文件在权限中显示 `s`。
- `-k`: 设置了粘位。通常被称为“粘位”，是一种特殊的文件权限。如果文件设置了此标志，该文件将保留在缓存内存中以便快速访问。如果在目录上设置，它将限制写入权限。设置粘位会在文件或目录列表上添加 `t`。
- `-O`: 你是文件的所有者
- `-G`: 文件的组 ID 与你的相同
- `-m`: 文件自上次读取以来被修改过

```
f1 -nt f2
文件 $f1 比 $f2 新

f1 -ot f2
文件 $f1 比 $f2 旧

f1 -ef f2
文件 $f1 和 $f2 是指向同一个文件的硬链接

!
"not" — 反转上述测试的含义（如果条件不存在则返回真）。
```

示例 29-1、示例 10-7、示例 10-3、示例 29-3 和示例 A-2 释了文件操作符的使用。

## 7.3. 比较运算符（二元）

### 整数比较

- `-eq`
  等于
  ```bash
  if [ "$a" -eq "$b" ]
  ```
- `-ne`
  不等于
  ```bash
  if [ "$a" -ne "$b" ]
  ```
- `-gt`
  大于
  ```bash
  if [ "$a" -gt "$b" ]
  ```
- `-ge`
  大于等于
  ```bash
  if [ "$a" -ge "$b" ]
  ```
- `-lt`
  小于
  ```bash
  if [ "$a" -lt "$b" ]
  ```
- `-le`
  小于等于
  ```bash
  if [ "$a" -le "$b" ]
  ```
- `<`
  小于（在双括号内）
  ```bash
  (( "$a" < "$b" ))
  ```
- `<=`
  小于等于（在双括号内）
  ```bash
  (( "$a" <= "$b" ))
  ```
- `>`
  大于（在双括号内）
  ```bash
  (( "$a" > "$b" ))
  ```
- `>=`
  大于等于（在双括号内）
  ```bash
  (( "$a" >= "$b" ))
  ```

### 字符串比较

- `=`
  等于
  ```bash
  if [ "$a" = "$b" ]
  ```
- `==`
  等于
  ```bash
  if [ "$a" == "$b" ]
  ```
  这是 `=` 的同义词。
  ```bash
  [[ $a == z* ]] # 如果 $a 以 "z" 开头则为真（模式匹配）
  [[ $a == z* ]] # 如果 $a 等于 z* 则为真
  [ $a == z* ]   # 会发生通配符展开和单词分割
  [ "$a" == z* ] # 如果 $a 等于 z* 则为真
  ```
- `!=`
  不等于
  ```bash
  if [ "$a" != "$b" ]
  ```
  此运算符在 `[ ]` 结构内部使用模式匹配。
- `<`
  小于，按照 ASCII 字母顺序
  ```bash
  if [ "$a" < "$b" ]
  ```
  ```bash
  if [ "$a" \< "$b" ]
  ```
  注意在 `[ ]` 结构内对 `<` 需要进行转义。
- `>`
  大于，按照 ASCII 字母顺序
  ```bash
  if [ "$a" > "$b" ]
  ```
  ```bash
  if [ "$a" \> "$b" ]
  ```
  注意在 `[ ]` 结构内对 `>` 需要进行转义。
  参见示例 26–4 关于此比较运算符的应用。
- `-z`
  字符串为 "null"，即长度为 0
- `-n`
  字符串不为 "null"。

`-n` 测试绝对要求字符串在测试括号内加引号。虽然像 `-z` 那样使用不引号的字符串，或者仅在测试括号内使用不引号字符串（示例 7–5）通常可以运行，但这是一种不安全的做法。始终对测试的字符串加引号。

### 示例 7–4 算术与字符串比较

```bash
#!/bin/bash
a=4
b=5
# 这里 "a" 和 "b" 可以被视为整数或字符串。
# 算术和字符串比较之间存在某些模糊，
# 因为 Bash 变量不是强类型的。
# Bash 允许对由全整数字符组成的变量进行算术运算和比较。
# 请注意。
if [ "$a" -ne "$b" ]
then
    echo "$a is not equal to $b"
    echo "(arithmetic comparison)"
fi
if [ "$a" != "$b" ]
then
    echo "$a is not equal to $b."
    echo "(string comparison)"
fi
```
在此情况下，`-ne` 和 `!=` 均有效。

### 示例 7–5 检查字符串是否为空

```bash
#!/bin/bash
# str-test.sh: 测试空字符串和未加引号字符串，
# 但不测试空字符串以及...
# 使用 if [ ... ]
# 如果字符串没有初始化，则没有值。
# 这种状态被称为 "null"不同于零）。
if [ -n "$1" ]
then
    echo "$1 is not null."
else
    echo "$1 is null."
fi
# 结果错误。
# 显示 $1 不空，尽管它没有被初始化。
```

### 示例 7–6 zmost

```bash
#!/bin/bash
# 使用 'most' 查看压缩文件
NOARGS=65
NOTFOUND=66
NOTZIP=67
if [ $# -eq 0 ]; # 效果等于：if -z "$1" ]
  # $1 可以存在，但为空
then
  echo "Usage: basename $0 filename" >&2
  # 错误信息输出到 stderr
  exit NOARGS
  # 返回 65 作为脚本的退出状态（错误代码）。
fi
filename=$1
if [ ! -f "$filename" ]; # 为 $filename 加引号允许可能存在空格。
then
  echo "File $filename not found!" >&2
  # 错误信息输出到 stderr
  exit NOTFOUND
fi
if [ "${filename#*.}" != "gz" ]; # 在变量替换中使用括号。
then
  echo "File $1 is not a zipped file!"
  exit NOTZIP
fi
zcat $1 | most
# 使用文件查看器 'most'（类似于 'less'）。
# 后版本的 'most' 具有文件解压功能。
# 根据需要可以替代 'more' 或 'less'。
exit $? # 脚本返回管道的退出状态。
# 实际上返回 $? 没有必要的，因为脚本无论如何
#都会返回最后一个执行命令的退出状态。
```

## 复合比较

- `-a`
  逻辑与
  如果 `exp1` 和 `exp2` 都为真则 `exp1 -a exp2` 返回真。
- `-o`
  逻辑或
  如果 `exp1` 或 `exp2` 为任一真则 `exp1 -o exp2` 返回真。

这些与在双括号内使用的 Bash 比较运算符 `&&`、`||` 相似

```bash
[[ condition1 && condition2 ]]
```
`-a` 运算符与 `test` 命令配合工作或在单括号内使用。

```bash
if [ "$exp1" -a "$exp2" ]
```
参见示例 8–3 和示例 26–8 查看比较运算符的实际应用。

## 7.4. 嵌套 if/then 条件测试

使用 `if/then` 结构的条件测试可以嵌套。其最终结果与使用上述的 `&&`、`||` 比较运算符相同。

```bash
if [ condition1 ]
then
  if [ condition2 ]
  then
    do-something # 但仅当 "condition1" 和 "condition2" 有效时执行。
  fi
fi
```
参见示例 35–4 关于嵌套 `if/then` 条件测试的示例。

## 7.5. 测试对测试的理解

系统级 `xinitrc` 文件可用于启动 X 服务器。该文件包含许多 `if/then` 测试，如下所示所示。

```bash
if [ -f $HOME/.Xclients ]; then
  exec $HOME/.Xclients
elif [ -f /etc/X11/xinit/Xclients ]; then
  exec /etc/X11/xinit/Xclients
else
  # 故障设置。虽然我们在 Xclients 中也提供了备用方案，但无无益。
  xclock -geometry 100x50+5 &
  xterm -geometry 800x50+150 &
  if [ -f /usr/bin/netscape -a f /usr/share/doc/HTML/index.html ]; then
    netscape /usr/share/doc/HTML/index.html &
  fi
fi
```
解释上述摘录中的 "test" ，然后检查整个文件 `/etc/X11/xinitrc` 并分析 `if/then` 测试。你可能需要参考 `grep`、`sed` 和正则表达式的讨论。

# 8. 操作与相关主题

## 8.1. 运算符

### 赋值

初始化或更改变量的值

`=`

通用赋值运算符，适用于算术和字符串赋值。

```bash
var=27
category=minerals # "=" 后面不允许空格
```



# 高级 Bash 脚本指南

## 赋值运算符与测试运算符

不要将 `=` 赋值运算符与 `=` 测试运算符混淆。

```bash
# = 作为测试运算符

if [ "$string1" = "$string2" ]; then
    # [ "X$string1" = "X$string2" ]
    # 防止其中一个变量为空时出现错误消息。
    #（前置的 "X" 字符会抵消。）
    command
fi
```

## 算术运算符

*   `+`：加
*   `-`：减
*   `*`：乘
*   `/`：除
*   `**`：幂

Bash 版本 2.02 引入了 `**` 幂运算符。

```bash
# Bash 版本 2.02 引入了 """ 幂运算符。

let z=5**3

echo "z = $z" # z = 125
```

### 取模（modulo）

取模（modulo），或返回整数除法操作的余数。

```bash
bash$ echo `expr 5 % 3'

2
```

该运算符常用于许多场景，例如：生成特定范围内的数字（参见示例 9–21 和示例 9–22）以及格式化程序输出（参见示例 26–7 和示例 A–6）。它甚至可以用于生成质数（参见示例 A–14）。取模在各种数值配方中出现的频率异常地高。

### 示例 8–1. 最大公约数

```bash
#!/bin/bash

# gcd.sh 最大公约数
# 使用欧几里得算法
# 两个整数的“最大公约数”(gcd)
+# 是能整除这两个数且无余数的最大整数。
# 欧几里得算法使用连续除法。
# 在每次循环中，
## 被除数 < 除数
## 除数 <- 余数
## 直到 余数 = 0。
# 最后一次通过后，gcd = 极佳结果。
# 关于欧几里得算法的优秀讨论，请访问
# Jim Loy 的网站：http://www.jimloy.com/number/euclids.html

# 参数检查
ARGS=2
E_BADARGES=65

if [ "$#" -ne "$ARGS" ];
then
    echo "用法: `basename` 第一个数字 第二个数字"
    exit $E_BADARGES
fi
```

```bash
gcd () {
    # 任意赋值。
    # 并不重要
    dividend=$1
    divisor=$2
    +# 两个中哪个较大。
    # 为什么？
}
```

第 8 章。操作与相关主题

# 高级 Bash 脚本指南

```bash
remainder=1              # 如果在循环中使用未初始化的变量，
# ++ 它会导致错误信息
# + 在循环第一次通过时。

until [ "$remainder" -eq 0 ]
do
    let remainder = $dividend % $divisor
    dividend=$divisor      # 现在对两个最小数重复。
    divisor=$remainder      # 欧几里得算法
done

# 最后的 $dividend 是 gcd。
```

```bash
gcd $1 $2
echo; " $1 和 $2 的最大公约数 = $dividend"; echo

+   练习题：
-------
# 检查命令行参数以确保它们是整数，
+# 如果不是，则带有相应的错误信息退出脚本。

exit 0
```

### 复合赋值运算符

*   **加等号**（通过常量增加变量）：`let var += 5` 结果 `var` 增加了 5。
*   **减等号**（通过常量减少变量）
*   **乘等号**（通过常量乘以变量）：`let var *= 4` 结果 `var` 被乘以了 4。
*   **除等号**（通过常量除以变量）
*   **模等号**（变量除以常数的余数）

算术运算符通常出现在 `expr` 或 `let` 表达式中。

### 示例 8–2. 使用算术运算

```bash
#!/bin/bash
```

#### 以 5 种不同方式 6 计数

```bash
n=1; echo -n "$n"

let n = $n + 1  # let n = n + 1 也有效。

echo -n "$n"

$((($n + 1)))

# "$(" 是必要的，否则 Bash 会尝试
#+ 将 "$(n = $n + 1)" 解释为命令。

echo -n "$n"

n=$($n + 1)

echo -n "$n"

$: n = $n + 1

# "$" 是必要的，否则 Bash 会尝试
#+ 将 "$(n = $n + 1)" 解释为命令。
# 即使 "n" 被初始化为字符串也有效。

echo -n "$n"

s={ $n + 1 }

# 即使 "n" 被初始化为字符串也有效。
# 避免这种构造类型，因为它是过时且不可移植的。

echo -n "$n"; echo
```

# 感谢 Stephanie Chazelas。

```bash
exit 0
```

![图示](img/1ce1edffaa36e4f698a85430e716d3b_62.png)

Bash 中的整数变量实际上是长整型（32位整数），范围在 `-2147483648` 到 `2147483647` 之间。超出这些限制的运算将报错。

### 位运算符

| 运算符 | 描述 |
| :--- | :--- |
| `<<` | 位位左移（每次移位乘以 2） |
| `>>` | 位位右移（每次移位除以 2） |
| `&` | 位位与 |
| `\|` | 位位或 |
| `~` | 位位取反 |
| `^` | 位位异或 |
| `<<=` | 位位左移-赋值 |
| `>>=` | 位位右移-赋值 |
| `&=` | 位位与-赋值 |
| `\|=` | 位位或-赋值 |
| `^=` | 位位异或-赋值 |

Bash 不理解浮点运算。它将包含小数点的数字视为字符串。

```bash
a=1.5

let b = $a + 1.3 # 表达式错误（标记为 ".5 + 1.3"）

echo $b
```

在需要浮点计算或数学函数的脚本中使用 `bc`。位运算符在 shell 脚本中很少出现。它们的主要用途似乎是动态处理和测试值，就像 C 和 C++ 中一样。

# 第 8 章。操作与相关主题

# 逻辑运算符

#### 与运算符 `&&`（逻辑）

```bash
if [ $condition1 ] && [ $condition2 ];
# 等于：if [ $condition1 -a $condition2 ]
# 如果两个条件都为真则返回真...

if [[ $condition1 && $condition2 ]]; # 同样有效。

# 注意在 [ ] 结构中不允许使用 &&。
```

![图示](img/1ce1edffaa36e4f698a85430e716d3b_62.png)

`&&` 不允许在 `[ ]` 结构中使用。

```bash
# numbers.sh: let oct = 081: value too great for base (error token "081")

# 进制数只使用 0 - 7 范围内的数字。

exit 0

# 感谢 Rich Bartell 和 Stephane Chazelas 的解释。
```

# 第 3 部分：超越基础

## 目录

*   9 变量回顾
    *   9.1. 字符串处理
    *   9.2. 参数替换
    *   9.3. 变量类型：`declare` 或 `typeset`
    *   9.4. 变量的间接引用
    *   9.5. `SRAND`：生成随机整数
    *   9.6. 双括号结构
*   10. 循环与分支
    *   10.1. 循环
    *   10.2. 嵌套循环
    *   10.3. 循环控制
    *   10.4. 测试与分支
*   11. 内部命令与内置命令
    *   11.1. 作业控制
*   12. 外部过滤器、程序和命令
    *   12.1. 基础命令
    *   12.2. 复杂命令
    *   12.3. 时间 / 命令
    *   12.4. 文本处理命令
    *   12.5. 文件与归档命令
    *   12.6. 通信命令
    *   12.7. 终端命令
    *   12.8. 数学命令
    *   12.9. 杂命令
*   13. 系统与管理命令
*   14. 命令替换
*   15. 算术扩展
*   16. I/O 重定向
    *   16.1. 使用 `exec`
    *   16.2. 重定向代码块
    *   16.3. 应用程序
*   17. Here Documents
*   18. 时间

# 第 9 章：变量回顾

变量如果使用得当，变量可以增加脚本的力量和灵活性。这需要学习它们的细微差别和特性。

### 9.1. 内部变量

影响 `bash` 行为的内置变量：

#### `$BASH`

```bash
$BASH

# Bash 二进制文件的路径，通常为 /bin/bash
```

#### `$BASH_ENV`

```bash
$BASH_ENV

# 一个环境变量，指向在调用脚本时要读取的 Bash 启动文件
```

#### `$BASH_VERSINFO[n]`

```bash
$BASH_VERSINFO[n]

# 一个包含关于安装的 Bash 版本信息的数组。这与下方的 $BASH_VERSION 类似，但更详细。
```

```bash
# Bash 版本：
for n in 0 1 2 3 4 5; do
  echo "${BASH_VERSINFO[$n]}"
done

# BASH_VERSINFO[0] = 2 # 主版本号
# BASH_VERSINFO[1] = 0 # 小版本号
# BASH_VERSINFO[2] = 1 # 补丁级别。
# BASH_VERSINFO[3] = 1 # 构建版本。
# BASH_VERSINFO[4] = release # 发布状态。
# BASH_VERSINFO[5] = 13-redhat-gnu # 架构（与 $HOSTNAME 相同）。
```

#### `$BASH_VERSION`

```bash
$BASH_VERSION

# 系统中安装的 Bash 版本
```

```bash
bash$ echo $BASH_VERSION
2.0.4
```

```bash
tcsh% echo $BASH_VERSION
BASH_VERSION: Undefined variable.
```



# 高级 Bash 脚本指南

## 变量说明

检查 `$BASH_VERSION` 是确定正在运行哪个 shell 的好方法。shell 不一定会给出正确答案。

### $DIRSTACK
目录栈中的顶端值。`pushd` 和 `popd` 对应 `dirs` 命令，但 `dirs` 会显示目录栈的所有内容。

### $EDITOR
脚本调用的默认编辑器，通常为 `vi` 或 `emacs`。

### $EUID
当前用户所假设的（可能通过 `su` 获取）的“有效”用户 ID 数字。`$EUID` 不一定等同于 `$SUID`。

### $FUNCN
当前函数的名称

```bash
xyz2 () {

  echo "$FUNCN now executing."

}

xyz2

echo "$FUNCN" # 函数外为空值。

xyz2

echo "$FUNCN" # 函数名。
```

### $GLOBIGNORE
在 `glob`（通配符）匹配中被排除在外的的文件名模式列表。

### $GROUPS
当前用户所属的组，是当前用户组 ID 的列表（数组），记录在 `/etc/passwd` 中。

```bash
root$ echo $GROUPS

0

root$ echo ${GROUPS[1]}

1

root$ echo ${GROUPS[5]}

6
```

### $HOME
用户的家目录，通常为 `/home/username`（参见示例 9–12）。

### $HOSTNAME
主机会在初始化脚本在启动时分配系统名称。然而，`hostname()` 函数会设置 Bash 变量 `$HOSTNAME`。另请参见示例 9–12。

### $HOSTTYPE
主机类型，类似于 `$MACHTYPE`，用于识别系统硬件。

```bash
bash$ echo $HOSTTYPE
```

### $IFS
输入字段分隔符。默认是空白符（空格、制表符和换行符），但可以更改，例如用于解析逗号分隔的数据文件。注意 `$*` 使用 `$IFS` 中的第一个字符。参见示例 6–1。

```bash
bash$ echo $IFS | cat -v

bash$ bash -c 'set w y z; IFS=";"; echo "$*"'

w:y:z
```

`$IFS` 处理空白的方式与处理字符的方式不同。示例 9，`$IFS` 和空白符

```bash
#!/bin/bash

# $IFS 对空白的处理与其它字符不同。

output_args_per_line() {

  for arg; do

    echo "[$arg]"

  done

}

echo; echo "$IFS=$*"

echo "----------------"

IFS=" "

var=" a b c "

output_args_per_line $var # 输出 output_args_per_line "echo a b c ""

# [a]

# [b]

# [c]

echo; echo IFS=:

echo ""

IFS=:

var=:a::b:: # 与上面相同，用 ":" 替换 " "

output_args_per_line $var

# [a]

# [b]

# [c]

# 在 awk 的 "FS" 字段分隔符中也会发生同样的情况。

# 感谢 Stephane Chazelas。

# exit 0
```

（感谢 S. C. 提供的解释和示例。）

### $IGNOREEOF
忽略 `EOF`：shell 在注销之前会忽略多少个文件结束符（control–D）。

### $LC_COLLATE
通常设置在 `.bashrc` 或 `/etc/profile` 文件中，该变量控制文件名扩展和模式匹配中的排序顺序。如果处理不当，`LC_COLLATE` 可能会导致文件名通配符匹配出现意想不到的结果。

![](img/1ce11aa34f698a85430e71c6d3b_71.png)

从 Bash 2.0 版本开始，文件名通配符不再区分括号范围内的大小写字母。例如，`b [A-M]*` 会匹配 `File1.txt` 和 `file1.txt`。要恢复自定义行为，请在 `/etc/profile` 或 `~/.bashrc` 中设置 `LC_COLLATE=C`。

### $LC_CTYPE
此内部变量控制通配符和模式匹配中的字符解释。

### $LINENO
该变量是所在 shell 脚本的行号。它仅在脚本内部有意义，主要用于调试。

```bash
last_cmd_arg=$# 保存它

echo "At line number $LINENO, v1 = $v1"

echo "Last command processed = $last_cmd_arg"
```

### $MACHTYPE
机器类型，识别系统硬件。

```bash
bash$ echo $MACHTYPE
```

### $OLDPWD
旧工作目录（之前所在的目录）

### $OSTYPE
操作系统类型

```bash
bash$ echo $OSTYPE
```

### $PATH
二进制文件路径，通常为 `/bin/`, `/usr/local/bin/` 等。当给定命令时，shell 会在 `$PATH` 列出的目录中自动搜索。系统将 `$PATH` 定义存储在 `/etc/profile` 或 `~/.bashrc` 中。这种方法临时将目录添加到路径可能是方便的。当脚本退出时，它会恢复原始的 `$PATH`（子进程如脚本可能更改父进程的环境）。

![](img/1ce11aa34f698a85430e71c6d3b_72.png)

出于安全考虑，当前“工作目录”从 `$PATH` 中排除。

### $PIPETYPE
上一次执行管道的退出状态。有趣的是，这与上一次执行命令的退出状态并不相同。

```bash
bash$ echo $PIPSTATUS

0

bash$ ls -al | bogus_command

bash: bogus_command: command not found

bash$ echo $PIPSTATUS

141

bash$ ls -al | bogus_command

bash: bogus_command: command not found

bash$ echo $?

127
```

### $REPLY
当未向 `read` 命令提供变量时的默认值。这也适用于 `select` 菜单，但仅提供所选变量的索引，而不是变量本身的值。

```bash
#!/bin/bash

echo

echo -n "What is your favorite vegetable? "

read

echo "Your favorite vegetable is $REPLY."

# 只有在没有提供变量时，REPLY 才会持有上一次 "read" 的值

echo

echo -n "What is your favorite fruit? "

read fruit

echo "Your favorite fruit is $fruit"

echo "but..."

echo "Value of \REPLY is still $REPLY"

# REPLY 仍然保持其之前的值，因为

# 变量 $fruit 吸收了新的 "read" 值。

echo

exit 0
```

### $SECONDS
脚本已运行的秒数。

```bash
#!/bin/bash

ENDLESS_LOOP=1

INTERVAL=1

echo "Hit Control-C to exit this script."

echo

while [ "$ENDLESS_LOOP" ]

do

    if [ "$SECONDS" -eq 1 ];

    then

        units=second

    else

        units=seconds

    fi

    echo "This script has been running $SECONDS $units"

    sleep $INTERVAL

done

exit 0
```

### $SHELLOPTS
已启用 shell 选项列表，一个只读变量

### $SHLVL
Shell 层级，Bash 的嵌套深度。如果从命令行执行 `SHLVL` 为 1，在脚本中它将递增到 2。

### $TMOUT
如果将环境变量 `$TMOUT` 设置为非零时间值，则 shell 提示符将在该秒数后超时。这会导致注销。

![](img/1ce1edffaa36e4f698a85430e71c6d3b_75_0.png)

遗憾的是，这只在 shell 提示符或 `xterm` 中等待输入时有效。虽然推测此内部变量用于定时输入的用处会很棒，但它与 `read` 结合使用时，`$TMOUT` 在该上下文中不起作用，对于 shell 脚本编写几乎没有用处。（据报道 `ksh` 版本的定时 `read` 是有效的。）

在脚本中实现定时输入是完全可能的

## 9–2. 定时输入

```bash
#!/bin/bash

# timed-input.sh

# TIMELIMIT=3 在脚本中是没用的

TIMELIMIT=3 # 此例中为三秒，可以设置为不同的值。

PrintAnswer()

{

    if [ "$answer" = $TIMEOUT ]

    then

        echo $answer

    else

        echo # 不混淆实例

        echo "Your favorite veggie is $answer"

        kill $! # 杀死后台运行且持续需要的 TimerOn 函数。$! 是最后一个后台运行作业的 PID。

}

TimerOn()

{

    sleep $TIMELIMIT && kill -s 14 $$ &

    # 等待3 秒，然后向脚本发送 sigalarm。

}

Intl4Vector()

{

    answer="TIMEOUT"

    PrintAnswer

    exit 14

}

trap Intl4Vector 14 # 定时中断 (14) 被我们的目的所劫持。

echo "What is your favorite vegetable "

TimerOn

read answer

PrintAnswer
```

- 诚然，`-t` 选项是定时输入的一种笨拙实现，
- 然而，“`read`” 选项简化了这项任务。
- 参见下文的 `t-out.sh`。
- 如果你需要真正优雅的方法...
- 考虑使用 `C` 或 `C++` 编写应用程序，
- 使用适当的库函数，如 `alarm` 和 `setitimer`。

`exit 0`

替代方法是使用 `stty`。

## 示例 9–3. 再次定时输入

```bash
#!/bin/bash

# timeout.sh

# 由 Stephane Chazelas 编写

# 由文档作者修改

INTERVAL=5

# 超时间隔

timed_read() {

timeout=$1

varname=$2

old_tty_settings='tty -g'

stty -icanon 0 time ${timeout}0

eval read $varname or just read $varname

stty "$old_tty_settings"

# 查看关于 "stty" 的页面

}

echo -n "What is your favorite vegetable "

TimerOn

read answer

PrintAnswer
```

## 示例 9–4. 使用 IFS 处理参数

```bash
echo

echo 'IFS unchanged, using "$*"'

c=0

for i in "$*"    # 加了引号

doo echo "$((c+1)): [$i]" # 这行在每个实例中都保持不变。

                                     # 输出参数。

done

d

echo ---

echo 'IFS unchanged, using $*'

c=0

for i in $*       # 未加引号

doo echo "$((c+1)): [$i]"

done

echo ---

echo 'IFS unchanged, using "$@"'

c=0

for i in "$@"

doo echo "$((c+1)): [$i]"

done

echo ---

echo 'IFS unchanged, using $0'

c=0

for i in "$0"

doo echo "$((c+1)): [$i]"

done

echo ---

IFS=

echo 'IFS=":", using "$*"'

c=0

for i in "$*"

doo echo "$((c+1)): [$i]"

done

echo ---

echo 'IFS=":", using $*'

c=0

for i in *

doo echo "$((c+1)): [$i]"

done

echo ---

var=$* 

echo 'IFS=":", using "$var" (var=$*)'

c=0

for i in "$var"

doo echo "$((c+1)): [$i]"

done

echo ---

echo 'IFS=":", using $var (var=$*)'

c=0

for i in $var

doo echo "$((c+1)): [$i]"

done

echo ---

exit 0

```

## 示例 9–5. 更多 IFS 行为

```bash
var="$*"

echo IFS=":", using var(var="$*")

c=0

for i in $var

doo echo "$((c+=1)): [$i]"

done

echo ---

echo IFS=":", using \$var(var="$*")

c=0

for i in "\$var"

doo echo "$((c+=1)): [$i]"

done

echo ---

echo IFS=":", using \$\$@"

c=0

for i in "\$@"

doo echo "$((c+=1)): [$i]"

done

echo ---

echo IFS=":", using \$@'

c=0

for i in \$@$

doo echo "$((c+=1)): [$i]"

done

echo ---

var="\$@"

echo IFS=":", using var(var="\$@")

c=0

for i in $var

doo echo "$((c+=1)): [$i]"

done

echo ---

echo IFS=":", using \$var(var="\$@")

c=0

for i in \$var

doo echo "$((c+=1)): [$i]"

done

echo ---

echo IFS=":", using \$var(var="\$@")

c=0

for i in $var

doo echo "$((c+=1)): [$i]"

done

echo ---

# 尝试用 ksh 或 zsh 运行此脚本。

exit 0

```

`$$` 和 `\$` 参数仅在双引号之间时有所不同。

## 示例 9–8. 当 $IFS 为空时的 $* 和 @@

```bash
#!/bin/bash

# 如果 IFS 设置为空为空，

那么 "$*" 和 "@@" 不会如预期输出位置参数。

# 输出位置参数。

mecho () {

  echo "$1,$2,$3"

}

IFS="" # 设置了但为空。

set a b c  # 位置参数。

mecho "$*" # abc,

mecho $* # a,bc

mecho @@ # a,b,c

mecho "@@" # a,b,c

# 当 $IFS 为空时，$* 和 @@ 的行为取决于正在运行的 Bash 或 sh 版本。

# 因此，在脚本中依赖这种“特性”是不可接受的。

# 感谢 S.C.

exit 0

```

# 特殊参数

- `$-`: 传递给脚本的标志。这最初是 `ksh` 的结构并引入 `Bash`，遗憾的是它在 `Bash` 脚本中似乎并不可靠。一种可能的用途是让脚本自测它是否为交互式。
- `$!`: 上一个后台作业的 `PID`（进程 ID）。
- `$_`: 特殊变量，设置为上一个执行命令的最后一个参数。

## 示例 9–9. 下划线变量

```bash
#!/bin/bash
```



```bash
echo $_          # 只是调用 /bin/bash 来运行脚本。

du >/dev/null      # 所以命令没有输出。

ls -al             # 所以命令没有输出。

echo $_           #: 命令、函数或脚本本身的状态（参见示例 23–24 和 12–23）
```

## 9.2. 字符串处理

- `${string}`: 长度
```bash
string=abc123ABCc
echo ${#string}      # 11
```

- `${string:length}`: 字符串开头子串长度
```bash
string=abc123ABCc
echo ${string:0}      # 11
```

- `${string#pattern}`: 字符串开头匹配子串的长度（$substring 是正则表达式）。
```bash
string=abc123ABCc
echo ${string#abc}  # 8
```

- `${string%%pattern}`: 索引（匹配子串第一个字符的数字位置）。
```bash
string=abc123ABCc
echo ${string%%ABC*}  # 6
```

- `${string##pattern}`: 索引（'1' 之前的数字位置）。
```bash
string=abc123ABCc
echo ${string##abc*}  # 3
```

- `${string:position}`: 子串提取（如果字符串参数是 `*` 或 `@`，则从该位置开始提取位置参数）。
```bash
string=abc123ABCc
echo ${string:7}      # 23ABC（等等，OCR 文本说逻辑是 23ABC）
```

- `${string:position:length}`: 子串提取（如果字符串参数是 `*` 或 `@`，则从该位置开始提取最多长度参数）。
```bash
string=abc123ABCc
echo ${string:2:3}    # bc
```

- `${string%pattern}`: 子串移除（从 $string 尾部移除 'b' 和 'c' 之间最短匹配项）。
```bash
string=abc123ABCc
echo ${string%b*c}    # abc123ABCa
```

- `${string%%pattern}`: 子串移除（从 $string 尾部移除 'b' 和 'c' 之间最长匹配项）。
```bash
string=abc123ABCc
echo ${string%%b*c}    # a
```

- `${string#pattern}`: 子串移除（移除 'a' 和 'C' 之间最短匹配项）。
```bash
string=abc123ABCc
echo ${string#aC}    # 123
```

- `${string##pattern}`: 子串移除（移除 'a' 和 'C' 之间最长匹配项）。
```bash
string=abc123ABCc
echo ${string##a*}   # abc
```

- `${string##pattern}`: 子串移除（从 $string 尾部移除最长的 $substring）。
- `${string%%pattern}`: 子串移除（从 $string 尾部移除最长的 $substring）。

## 9–10. 转换图形文件并修改文件名

```bash
#!/bin/bash
cvt.sh
# 将目录下所有的 MacPaint 图像转换为 "pbm" 格式。
# 使用来自 netpbm 软件包的 "macptopbm" 二进制文件，
# 由 Brian Henderson (bryanh@giraffe-data.com) 维护。
# Netpbm 是大多数 Linux 发行版的标准部分。
```

```bash
OPERATION=macptopbm
SUFFIX=pbm
# 新文件名后缀。
if [ -n "$1" ]
then
  directory=$1
  # 如果脚本参数传递了目录名
else
  directory=$PWD
  # 否则使用工作目录。
## 假设目标目录中的所有文件都是带有 ".mac" 后缀的 MacPaint 图像文件。
for file in $directory/*  # 文件名通配。
do
  filename=${file%.*c}
  # 去掉文件名中的 .mac 后缀
  $OPERATION file > $filename.$SUFFIX  # 将转换重定向到新文件名。
  rm -f "$file"  # 转换后删除原始文件。
  echo "$filename.$SUFFIX"  # 将正在的操作输出到 stdout。
done
exit 0
```

# 高级 Bash 脚本指南

```
# 将所有匹配 'abc' 的部分替换为 'wyz'
${string//substring/replacement}
```

如果 $substring 匹配 $string 的开头，则将 $substring 替换为 $replacement。
`${string%substring/replacement}`

如果 $substring 匹配 $string 的结尾，则将 $substring 替换为 $replacement。

```
stringZ=abc123ABCabc
echo ${stringZ/#abc/XYZ}
# XYZABC123ABCabc
# 将开头匹配的 'abc' 替换为 'xyz'
echo ${stringZ/%abc/XYZ}
# abc123ACXYZ
# 将结尾匹配的 'abc' 替换为 'xyz'
```

## 9.2.1 使用 awk 处理字符串

Bash 脚本可以调用 `awk` 的字符串处理功能作为内置操作的替代。

**示例 9–11. 提取子字符串的替代方法**

```bash
#!/bin/bash
# substring-extraction.sh
String=23skidoodle
# 0123456789  Bash
# 123456789 awk
# 索引系统：
# 注意 awk 将字符串的第一个字符标记为 '0'
# Bash 将字符串的第一个字符标记为 '1'
echo ${String:2:4} # 位置 3 (0-1)，长度 4 个字符
# skid
# ${string:pos:length} 的 awk 等效等式是 substr(string,pos,len)。
echo '' | awk '{ print substr($String,3,4) }'
# skid
# 向 awk 管道传递一个空的 "echo" 可以提供伪输入，
# 并使得无需提供文件名。
exit 0
```

### 9.2.2. 进一步讨论

有关脚本中更多字符串处理操作，请参考第 9.3 节和 `expr` 命令列表的相关部分。脚本示例请参阅：

9.2.1. 使用 `awk` 处理字符串

- 示例 12–6
- 示例 9–13
- 示例 9–14
- 示例 9–15
- 示例 9–17

## 9.3. 参数替换

变量的处理和/或扩展

`$(parameter)`

相当于 `$parameter`，即变量参数的值。在某些上下文中，只有这种无歧义的 `$(parameter)` 形式有效。

可用于将变量与字符串拼接。

```bash
your_id=$(USER)-on-$(HOSTNAME)
echo "$your_id"
echo "Old $PATH = $PATH"
PATH=$(PATH):/opt/bin # 在脚本运行期间向 $PATH 添加 /opt/bin。
echo "New $PATH = $PATH"
```

`$(parameter-default)`

如果参数未设置，则使用默认值。

```bash
echo ${username-`whoami`}
# 如果变量 $username 仍未设置，则输出 `whoami` 的结果。
```

这与 `$(parameter:-default)` 几乎等效。额外的 `:-` 仅在参数已声明但为空时才会产生区别。

```bash
#!/bin/bash
username0=
# username0 已声明，但被设置为空值。
echo "username0=${username0-`whoami`}"
# 不输出。
echo username1=${username1-`whoami`}
# username1 未声明。
# 将输出。
username2=
# username2 已声明，但被设置为空值。
echo "username2=${username2:-`whoami`}"
# 将输出，因为使用了 :- 而不仅仅是在条件测试中。
exit 0
```

`${parameter=default}` , `${parameter:=default}`

如果参数未设置，则将其设置为默认值。

两种形式几乎等效。仅当 `$parameter` 已声明且为空时（如上文 [21]），才会产生区别。

```bash
echo ${username=whoami}
# 变量 `username` 现在设置为 `whoami`
```

`${parameter+alt_value}` , `${parameter:+alt_value}`

如果参数设置，则使用 `alt_value`，否则使用空字符串。

两种形式几乎等效。仅在参数已声明且为空时才会产生区别，见下文。

```bash
######## $(parameter+alt_value) #######
echo
a=$(param1+xyz)
echo "a = $a"  # a =
param2=
a=$(param2+xyz)
echo "a = $a"  # a =
param3=123
a=$(param3+xyz)
echo "a = $a"  # a =
######## $(parameter+alt_value) #######
echo
a=$(param4+xyz)
echo "a = $a"  # a =
param5=
a=$(param5+xyz)
echo "a = $a"  # a =
# 结果与 a=${param5+xyz} 不同
param6=123
a=$(param6+xyz)
echo "a = $a"  # a =
```

`${parameter?err_msg}`

如果参数设置，则使用它，否则打印 `err_msg`。两种形式几乎等效。仅在参数已声明且为空时（如上文所示）才会产生区别。

## 9.3. 参数替换

字符串长度（`$var` 中的字符数）。

`${var%pattern}` , `${var##pattern}` 从 `$var` 中删除匹配 `$pattern` 开头的最短/最长部分。来自示例 A–7 的用法说明：

```bash
# 来自 "days-between.sh" 示例的函数。
# 从传递的参数中删除前导零。
strip_leading_zero () {
    # 最好删除日期或月份可能的前导零
    val=${1#0} # 否则 Bash 将其解释为八进制值 (POSIX.2, 9.2.1 节)。
    return $val
}
```

另一个用法说明：

```bash
echo "basename $PWD" # 当前工作目录。
echo "$PWD##*/" # 当前工作目录。
echo "basename $0" # 脚本名。
echo $0 # 脚本名。
echo "${0##*/}"      # 脚本名。
filename=test.data          # data
echo "${filename##*.}"    # 文件扩展名。
```

`$varpattern` 从 `var` 中删除匹配 `$pattern` 结尾的最短/最长部分。Bash 版本 2 增加了选项。

# 示例 9–14. 参数替换中的模式匹配

```bash
#!/bin/bash
# 使用 # 和 % 参数替换运算符进行模式匹配。
var1=abcd12345abc6789
pattern1=*c # (通配符) 匹配 a 到 c 之间的所有内容。

echo var="$var1" # abcd12345abc6789
echo "$var1" (另一种形式) abcd12345abc6789
echo "Number of characters in ${var1}" = ${#var1}
echo pattern1=$*c ('a' 和 'c' 之间的所有内容)
echo

echo "${var1$pattern1}" = '${var1$pattern1}' # dcd12345abc6789
# 短匹配，删除前 3 个字符 abcd12345abc6789
^^^^
echo '${var1#$pattern1}' = '${var1#$pattern1}' # 6789
# 最长匹配，删除前 12 个字符 abcd12345abc6789
^^^^^^^^^^^^
```

```bash
echo;
pattern2=b*9 # 'b' 和 '9' 之间的所有内容
echo var="$var1" # 仍为 abcd12345abc6789
echo pattern2=$pattern2
echo

echo "${var1%pattern2}" = '${var1%pattern2}' # abcd12345a
# 短匹配，删除 6 个字符 abcd12345abc6789
^^^^^^
echo '${var1%%pattern2}' = '${var1%%pattern2}' #
# 最长匹配，删除最后 12 个字符 abcd12345abc6789
^^^^^^^^^^^^
```

# 记住，# 和 ## 从字符串左端开始工作，
# % 和 %% 从右端开始工作。

# 示例 9–15. 重命名文件扩展名：

```bash
#!/bin/bash
```

# 高级 Bash 脚本指南

```bash
# rfe
# ---
# 重命名文件后缀。
# rfe old_extension new_extension
# 示例:
# 将工作目录下的所有 *.gif 文件重命名为 *.jpg，
# rfe gif jpg

ARGS=2
E_BADARGES=65

if [ $# -ne "$ARGS" ];
then
    echo "Usage: basename $0' old_file_suffix new_file_suffix"
    exit $E_BADARGES
fi

for filename in $*.1
  # 遍历以第一个参数结尾的文件列表。
do
    mv $filename${filename%%$1} $2
    # 去掉文件名中匹配第一个参数的部分，
    # 然后追加第二个参数。
done
exit 0
```

# 变量扩展 / 字符串替换

这些构造体纳自 `ksh`。

### `${var:pos}`

对变量 `var` 进行扩展，从偏移量 `pos` 开始。

### `${var:pos:len}`

从偏移量 `pos` 开始，扩展变量 `var` 最多 `len` 个字符。请参见示例 A–12 以了解此操作符的创意用法。

### `${var/pat/replacement}`

将 `var` 中第一个匹配 `pat` 的项替换为 `replacement`。

如果省略了 `replacement`，则 `pat` 的第一个匹配项将被替换为空，即被删除。

### `${var//pat/replacement}`

全局替换。将 `var` 中所有匹配 `pat` 的项都替换为 `replacement`。

同上，如果省略了 `replacement`，则 `pat` 的所有出现之处将被替换为空，即被删除。

## 9.3. 参数替换

示例 9–16. 使用模式匹配解析任意字符串



## 9.3. 参数替换

```bash
#!/bin/bash

var=abcd-1234-def
echo "var = $var"

t=${var#*}
echo "var (已删除从第一个 - 开始并包含在内的所有内容) = $t"
# t=${var#*-} 的效果完全相同，
# 因为 * 匹配第一个字符串，
# 且 * 匹配其之前的所有内容，包括空字符串。
#（感谢 S. C. 指出这一点。）

t=${var%*}}
echo "如果 var 包含 \", 则返回空字符串..." var = $t"

t=${var#-*}
echo "var (已删除从最后一个 - 开始的所有内容) = $t"
echo

path_name=/home/bozo/ideas/thoughts.for.today
# path_name="$path_name"
echo "path_name = $path_name"
t=${path_name#*/} 去掉前缀 = $t
# 在这种特定情况下与 t=$basename 效果相同。
# t=${path_name*:}; t=${t##*/} 是一个更通用的解决方案，
# 但有时仍然失败。
# 如果 path_name 以换行符结尾，则 $path_name 将不起，
# 但上面的表达式可以工作。
#（感谢 S.C.）

t=${path_name##/*}
# 与 t=dirname $path_name 效果相同
echo "path_name, 去掉后缀 = $t"
# 这些在某些情况下会失败，例如 "../////", # "foo/", "/*"
# 删除后缀，尤其是当 basename 没有后缀但 dirname 有后缀时，也会会让问题变得复杂。
#（感谢 S.C.）
echo

t=${path_name:11}
echo "path_name, 去掉前 11 个字符 = $t"
t=${path_name:11:5}
echo "path_name, 去掉前 11 个字符后，长度为 5 = $t"
echo

t=${path_name//bozo/clown}
echo "$ 将 \"bozo\" 替换为 \"clown\" 后 = $t"
t=${path_name#*/today/}
echo "删除了 \"today\" 的 path_name = $t"
t=${path_name//o/O}
echo "所有 o 都已大写的 path_name = $t"
t=${path_name//o/(o)}
echo "删除了所有 o 的 path_name = $t"
```

### 示例 9–17. 在字符串的前缀或后缀匹配模式

```bash
exit 0
${var/##patt/replacement}
```

如果 `var` 的前缀匹配 `replacement`，则将 `patt` 替换为 `replacement`。

```bash
${var/*#patt/replacement}
```

如果 `var` 的后缀匹配 `replacement`，则将 `patt` 替换为 `replacement`。

```bash
#!/bin/bash
# 字符串前缀/后缀的模式替换。

v0=abc1234zip1234abc # 原始变量。
echo v0 = $v0 # abc1234zip1234abc
echo

# 在字符串的开头（beginning）匹配。
v1=$(v0/##ABCDEF) # abc1234zip1234abc
echo v1 = $v1 # ABCDE1234zip1234abc
||

# 在字符串的结尾（end）匹配。
v2=$(v0%#ABCDEF) # abc1234zip123abc
echo v2 = $v2 # abc1234zip1234ABCDEF
|----|

echo
echo

# 必须在字符串的开头/结尾匹配，
# 否则没有替换结果。
v3=$(v0#/12300) # 匹配，但不在开头。
echo v3 = $v3 # abc1234zip1234abc
# 无替换。
v4=$(v0%#12300) # 匹配，但不在结尾。
echo v4 = $v4 # abc1234zip1234abc
# 无替换。
```

```bash
exit 0
${!varprefix*}, ${!varprefix@}
```

匹配所有以 `varprefix` 开头的已声明变量。

```bash
xyz23=whatever
xyz24=

a=${!xyz*} # 扩展以 "xyz" 开头的声明变量名
echo "a = $a@" # a = xyz23 xyz24
a=${!xyz24} # 同上。
echo "a = $a@" # a = xyz23 xyz24
```

## 9.4. 变量类型：declare 或 typeset

`declare` 或 `typeset` 内置命令（它们是同义词）允许限制变量的属性。这是一种弱类型检查。

```bash
exit 0
${var/##patt/replacement}
```

如果 `var` 的前缀匹配 `replacement`，则将 `patt` 替换为 `replacement`。

```bash
${var/*#patt/replacement}
```

如果 `var` 的后缀匹配 `replacement`，则将 `patt` 替换为 `replacement`。

### 示例 9–17. 在字符串的前缀或后缀匹配模式

```bash
#!/bin/bash
# 字符串前缀/后缀的模式替换。

v0=abc1234zip1234abc # 原始变量。
echo v0 = $v0 # abc1234zip1234abc
echo

# 在字符串开头（beginning）匹配。
v1=$(v0/##ABCDEF) # abc1234zip1234abc
echo v1 = $v1 # ABCDE1234zip1234abc
||

# 在字符串结尾（end）匹配。
v2=$(v0%#ABCDEF) # abc1234zip123abc
echo v2 = $v2 # abc1234zip1234ABCDEF
|----|

echo
echo

# 必须在字符串的开头/结尾匹配，
# 否则没有替换结果。
v3=$(v0#/12300) # 匹配，但不在开头。
echo v3 = $v3 # abc1234zip1234abc
# 无替换。
v4=$(v0%#12300) # 匹配，但不在结尾。
echo v4 = $v4 # abc1234zip1234abc
# 无替换。
```

```bash
exit 0
${!varprefix*}, ${!varprefix@}
```

匹配所有以 `varprefix` 开头的已声明变量。

```bash
xyz23=whatever
xyz24=

a=${!xyz*} # 扩展以 "xyz" 开头的声明变量名
echo "a = $a@" # a = xyz23 xyz24
```

# 高级 Bash 脚本指南

## 9.5. 生成随机整数

```bash
MAXCOUNT=10
count=1
echo "$MAXCOUNT random numbers:"
echo "------------------"
while [ "$count -le $MAXCOUNT ]; do
  # 生成 10 ($MAXCOUNT) 个随机整数。
  number=$RANDOM
  echo $number
  let count += 1  # 计数加
done
echo "------------------"
```

如果你需要一个特定范围内的随机整数，请使用“取模”运算符。

它返回除法运算的余数。

```bash
RANGE=500
echo
number=$RANDOM
let "number %= $RANGE"
echo "Random number less than $RANGE  --- $number"
echo
```

如果你需要一个大于下限的随机整数，请设置一个测试来丢弃所有低于下限的数字。

```bash
FLOOR=200
number=0  # 初始化
while [ "$number" -le $FLOOR ];
do
  number=$RANDOM
done
echo "Random number greater than $FLOOR  --- $number"
echo
```

可以结合上述两种技术来获取两个数字之间的随机数。

```bash
number=0  # 初始化
while [ "$number" -le $FLOOR ];
do
  number=$RANDOM
  let "number %= $RANGE"  # 将数字缩小到 $RANGE 范围内。
done
echo "Random number between $FLOOR and $RANGE  --- $number"
echo
```

生成二选一，即“真”或“假”值。

```bash
BINARY=2
number=$RANDOM
T=1
let "number >= 14"  可以提供更好的随机分布
# (右) 移出除了最后一个二进制位以外的所有内容。
if [ "$number" -eq $T ];
then
```

## 9.6. $RANDOM: 生成随机整数

```bash
echo "TRUE"
else
echo "FALSE"
fi

echo

# 可以模拟掷骰子。
SPOTS=7 # 取模 7 范围 0 - 6。
DICE=2
ZERO=0
diel=0
diel2=0

# 分别投掷，这样就能获得正确的概率。

while [ "$diel" -eq $ZERO ]; # 不能出现零。
do
    let diel = $RANDOM % $SPOTS # 掷第一个骰。
done

while [ "$diel2" -eq $ZERO ];
do
    let die2 = $RANDOM % $SPOTS # 掷第二个骰。
done

let throw = $diel + $die2
echo "Throw of the dice $throw"
echo
```

`RANDOM` 到底有多随机？测试此点的最佳方法是编写一个脚本，跟踪 `RANDOM` 生成的“随机”数的分布。让我们投掷几次 `RANDOM` 吧……

### 示例 9–22. 使用 RANDOM 掷骰子

```bash
#!/bin/bash
# RANDOM 到底有多随机

RANDOM=$RANDOM # 使用脚本进程 ID 重新种子随机数生成器。

PIPS=6 # 骰子有 6 个点。
MAXTHROWS=600 # 如果你没别的事要做，可以增加这个值。
throw=0 # 投掷次数。

zeros=0 # 必须将计数初始化零。
ones=0 # 因为未初始化的变量是空，而不是零。
twos=0
trees=0
fours=0
fives=0
sixes=0

print_result ()
{
echo
echo "ones" = $ones
echo "twos" = $twos
echo "threes" = $threes
echo "fours" = $fours
echo "fives" = $fives
echo "sixes" = $sixes
echo
}
```

```bash
update_count() {
  case $1 in
    0) let "ones" += 1;; # 因为没有“零”，这对应于 1
    1) let "twos" += 1;; # 对应于 2，以此类推。
    2) let "threes" += 1;;
    3) let "fours" += 1;;
    4) let "fives" += 1;;
    5) let "sixes" += 1;;
  esac
}
```

```bash
while [ "$throw" -lt "$MAXTHROWS" ]
do
  let "diel" = RANDOM % $PIPS
  update_count $diel
  let "throw" += 1
done
```

假设 `RANDOM` 是相当随机的，得分分布应该均匀。

当 `MAXTHROWS` 为 600 时，所有结果都应该集中在 100 左右，正负 20。

请记住 `RANDOM` 是一个伪随机生成器，而且它并不是特别特别优秀。

练习（简单）：重写此脚本来抛掷 1000 次硬币。选择是“HEADS”（正面）或“TAILS”（反面）。

正如我们在上一个示例中看到的，每次调用 `RANDOM` 时都“重新种子” `RANDOM` 生成器是最好的。对 `RANDOM` 使用相同的种子会重复相同的数字序列。（这反映了 C 语言中 `random()` 函数的行为。）

### 示例 9-23. 为 RANDOM 种子

```bash
#!/bin/bash
# seeding-random.sh: 为 RANDOM 变量设置种子。

MAXCOUNT=25
# 生成多少数字。
random_numbers() {
  count=0
  while [ "$count" -lt "$MAXCOUNT" ]
  do
    number=$RANDOM
  echo -n "$number "
    let count += 1
  done
  echo
}
```

```bash
RANDOM=1
random_numbers
```

设置 `RANDOM` 会种子随机数生成器。

```bash
RANDOM=1
random_numbers
```

对 `RANDOM` 使用相同的种子……会复制相同的数字序列。

什么时候需要重复同一个“随机”数字序列？

```bash
RANDOM=2
random_numbers
```

再次尝试，但使用不同的种子……会产生不同的数字序列。

```bash
# RANDOM=$$ 根据脚本 ID 为 RANDOM 设置种子。
# 也可以从 'time' 为 RANDOM 设置种子。
```

# 第 10 章 循环与分支

## 高级 Bash 脚本指南

```bash
echo # 用引号括起整个“列表”将创建一个单个变量。
for planet in "Mercury Venus Earth Mars Jupiter Saturn Uranus Neptune Pluto"
do
  echo $planet
done
exit 0
```

每个 `[list]` 元素可以包含多个参数。这在分组处理参数时非常有用。在这种情况下，请使用 `set` 命令（参见示例 11-10）来强制解析每个 `[list]` 元素，并将每个组件赋值给位置参数。

### 示例 10-2. 每个 [list] 元素中包含两个参数的 for 循环

```bash
#!/bin/bash
# 重新回顾行星。

# 将每个行星的名称与其到太阳的距离关联。
for planet in "Mercury 36" "Venus 67" "Earth 93" "Mars 142" "Jupiter 483"
do
  set --"$planet" 解析并设置位置参数。
  # "-" 可以防止在 $planet 为空或以连字符开头时出现意外情况。

  # 可能需要保存原始的位置参数，因为它们会被覆盖。
  # 这种方法的一种是使用数组
  original_params=("$@")

  echo "$1" $2,000,000 miles from the sun
  # --two 在参数 $2 后面拼接了两个零
done

# （感谢 S.C. 提供的额外说明。）
exit 0
```

变量可以为 `for` 循环提供 `[list]`。

### 示例 10-3. Fileinfo：对变量中包含的文件列表进行操作

```bash
#!/bin/bash
# fileinfo.sh

FILES="/usr/sbin/privatepw
/usr/sbin/pwck
/usr/sbin/go500gw
/usr/bin/fakefile
/sbin/mkreiserfs
  # 你感兴趣的文件列表。
  /sbin/ypbins
  # 顺便加入了一个虚拟文件 /usr/bin/fakefile。"
```

```bash
echo
for file in $FILES
do
  if [ ! -e "$file" ]; then    # 检查文件是否存在。
    echo "$file does not exist."; echo
    continue
    # 继续处理下一个。
  fi

  ls -l $file | awk '{print $9}'    file size: "$5" # 打印两个文件。
  whatis basename $file    # 文件信息。
  echo
done
```

`for` 循环中的 `[list]` 可以包含通配符（globbing），即使用通配符进行文件名扩展。

### 示例 10–4. 使用 for 循环操作文件

```bash
#!/bin/bash
# list-glob.sh: 使用“globbing”在 for 循环中生成 [list]
echo
for file *
do
  ls -l "$file" # 列出 $PWD（当前目录）中的文件。
  # 回想通配符 "*" 匹配一切
  # 但在“globbing”中，它不匹配隐藏文件（点文件）。

  # 如果模式没有匹配到文件，它将扩展为。
  # 为了防止这种情况，请设置 nullglob 选项
  # (shopt nullglob)
  # 感谢 S.C.
done
echo
for file in []*
do
  rm -f "$file" # 删除 $PWD 中以 "j" 或 "x" 开头的文件。
  echo "Removed file \$file"
done
echo
```

在 `for` 循环中省略 `[list]` 会导致循环对 `$@` 操作，即传递给脚本的命令行参数列表。示例 A–14 是此这一点特别巧妙的说明。



# 示例 10–5. for 循环中缺失 [list]

第 10 章 循环与分支 104

# 高级 Bash 脚本指南

```bash
#!/bin/bash

# 分别带参数和不带参数调用，查看会发生什么

for a
do
  echo -n "$a "
done

# 缺少 'in list'，因此循环对 '$@' 操作
#（命令行参数列表，包括空格）

echo

exit 0
```

可以使用命令替换来生成 for 循环中的 [list]。请参见另示例 12–34、示例 10–10 以及示例 12–31。

# 示例 10–6. 使用命令替换在 for 循环中生成 [list]

```bash
#!/bin/bash
# 使用命令替换生成 [list] 的 for 循环。

NUMBERS="9 7 3 8 37.53"

for number in `echo $NUMBERS` # for number in 9 7 3 8 37.53
do
  echo -n "$number "
done
echo
exit 0
```

这是一个使用命令替换创建 [list] 的较复杂的示例。

# 示例 10–7. 针对二进制文件的 grep 替换

```bash
#!/bin/bash
# bin-grep.sh 在二进制文件中查找匹配的字符串。

# 针对二进制文件的 "grep" 替换方案。
# 效果与 "grep -a" 相似。

E_BADARGS=65
E_NOFILE=66

if [ $# -ne 2 ]
then
  echo "Usage: `basename $0` string filename"
  exit $E_BADARGS
fi

if [ ! -f "$2" ]
then
  echo "File \$2" does not exist."
  exit $E_BADARGS
fi

# 第 10 章 循环与分支 109

# 高级 Bash 脚本指南
```

# 高级 Bash 脚本指南

请参见示例 26–7、示例 26–8 和示例 A–6。

现在，我们在“真实生活”场景中使用 `for-loop`（for 循环）。

# 示例 10–13. 使用批量模式下的 efax

```bash
#!/bin/bash

EXPECTED_ARGS=2
E_BADARGS=65

if [ $# -ne $EXPECTED_ARGS ]
  # 检查命令行参数是否正确。
then
  echo "Usage: $basename $0# phone text-file"
  exit $E_BADARGS
fi

if [ ! -f "$2" ]
then
  echo "File $2 is not a text file"
  exit $E_BADARGS
fi

fax make $2                     # 从文本文件创建传真格式的文件。

for file in $(ls $2.0*) # 合并转换后的文件。
  # 在变量列表中通配符。
do
  file="$file$file"
done

efax -d /dev/ttyS3 -ol -t "T1" $file # 执行工作。

# 正如 S.C 指出的，for-loop 可以被消除
# efax -d /dev/ttyS3 -ol -t "T1" $2.0
# 但这样并不十分具有启发性 [笑]。

exit 0
```

## while

这在循环顶部构建了一个测试，只要条件为真（返回退出状态 0），它就会继续循环。与 for 循环相比，`while loop`（while 循环）用于预先未知循环重复次数的情况。

```bash
while [condition]
do
  command...
done
```

与 for/in 循环一样，将 `do` 置于条件测试放在同一行需要一个分号（;）。

```bash
while [condition] ; do
```

注意，某些特殊的变量循环（例如 `getopts` 结构）在 particular 处与标准模板有所不同。

### 示例 10–14. 简单的 while 循环

```bash
#!/bin/bash
var0=0
LIMIT=10

while [ "$var0" -lt "$LIMIT" ];
do
    echo -n "$var0 "      # -n 抑制换行。
    var0=$(expr $var0 + 1)  var0=$((var0+1)) 同样有效。
done
echo
exit 0
```

### 示例 10–15. 另一个 while 循环

```bash
#!/bin/bash
echo
while [ "$varl" != "end" ];  # while 测试 "$varl" != "end"
do
    # 同样有效。
    echo "Input variable #1 (end to exit)"
    read varl                        # 没有读取 '$varl'（为什么？）。
    echo "variable #1 $varl"         # 因为 "#" 需要引号
    # 如果输入是 'end'，则在此处回显它。
    # 在循环顶部之前不会测试终止条件。
echo
done
exit 0
```

一个 while 循环可以有多个条件。只有最后一个条件决定循环是否终止。然而，这需要略有不同的循环语法。

### 示例 10–16. 带有多个条件的 while 循环

```bash
#!/bin/bash
varl=unset
previous=$varl

while echo "previous-variable = $previous"
do
    echo
    previous=$varl
    [ $varl != ] # 记录 $varl 之前的值。
    # 针对 "while" 的条件，但只有最后一个控制循环。
    # *最后一个*退出状态才是起作用。
    echo "Input variable #1 (end to exit)"
    read var
    echo "variable #1 = $varl"
done

# 尝试弄清楚这这一切是如何工作的。
# 这有点复杂。
exit 0
```

与 for 循环一样，while 循环可能通过使用双括号采用类似 C 的语法。

# 10–17. while 循环中的类似 C 的语法

```bash
#!/bin/bash
echo
while [ "$varl" != "end" ];  # while 测试 "$varl" != "end"
do
    # 同样有效。
    echo "Input variable #1 (end to exit)"
    read varl                        # 没有读取 '$varl'（为什么？）。
    echo "variable #1 $varl"         # 因为 "#" 需要引号
    echo "variable #1 = $varl"
    # 如果输入是 'end'，则在此处回显它。
    # 在循环顶部之前不会测试终止条件。
echo
done
exit 0
```

## until

这种结构在循环顶部进行测试，并且只要条件为假（与 while 循环相反），就会继续循环。

```bash
until [condition]
do
  command...
done
```

注意，until 循环在循环顶部测试终止条件。与 for 循环一样，将 `do` 置于条件放在同一行需要一个分号。

```bash
until [condition] ; do
```

### 示例 10–18. until 循环

```bash
#!/bin/bash
until [ "$var" = end ] # 在此处测试条件。
do
  echo "Input variable #1 (end to exit)"
  read var
  echo "variable #1 $var"
done
exit 0
```

## 10.2. 嵌套循环

嵌套循环是循环中的循环，即外部循环体内部的循环。发生的情况是外部循环的第一次通过触发内部循环并执行完毕。外部循环的第二次通过再次触发内部循环。这会重复直到外部循环结束。当然，内部或外部循环中的 `break` 可能会中断这一过程。

### 示例 10–19. 嵌套循环

```bash
#!/bin/bash
# 嵌套的 "for" 循环。

outer=1      # 设置外部循环计数。
# 外部循环开始。
for a in 1 2 3 4 5
do
  echo "Pass $outer in outer loop."
  echo "----------------------"
  inner=1      # 重置内部循环计数。
  # 内部循环开始。
  for b in 1 2 3 4 5
  do
    echo "Pass $inner in inner loop."
    inner+=1 # 增加内部循环计数。
  done
  # 内部循环结束。
  outer+=1 # 增加外部循环计数。
  # 外部循环通过之间的输出。
done
# 外部循环结束。
```

请参见示例 26–4 关于嵌套 "while" 循环的说明，以及示例 26–5 查看嵌套在 "until" 循环内部的 "while" 循环。

## 10.3. 循环控制

### 影响循环的命令

`break` 和 `continue` 循环命令与其编程语言中的对应物完全对应。`break` 终止循环（跳出），而 `continue` 导致跳转到循环的下次迭代，跳过该特定循环中的剩余命令。

### 示例 10–20. 循环中 break 和 continue 的影响

```bash
#!/bin/bash
LIMIT=19 # 上限
echo
echo "Printing Numbers 1 through 20 (but 3 and 11)."

a=0
while [ "$a" -le $LIMIT ]
do
  a=$((a+1))

  if [ "$a" -eq 3 ] || [ "$a" -eq 11 ] # 排除 3 和 11
  then
    continue # 跳过本次迭代的剩余部分。
  fi

  echo -n "$a "
done

# 练习：
# 为什么循环打印到 20？
```

```bash
echo; echo
echo Printing Numbers 1 through 20, but something happens after 2.
######################################################
# 相同的循环，但将 'continue' 替换为 'break'
a=0
while [ "$a" -le "$LIMIT ]
do
  a=$((a+1))
  if [ "$a" -gt 2 ];
  then
    break # 跳过整个循环剩余部分。
  fi
  echo -n "$a "
done
echo; echo; echo
exit 0
```

`break` 命令可以可选地接受一个参数。普通的 `break` 只终止其嵌入的最内层循环，但 `break N` 会跳出 N 层循环。

### 示例 10–21. 跳出多层循环

```bash
#!/bin/bash
# break-levels.sh: 跳出循环。

# "break N" 跳出 N 层的循环。
for outerloop in 1 2 3 4 5
do
  echo -n "Group $outerloop: "
  for innerloop in 1 2 3 4 5
  do
    echo -n "$innerloop"
    if [ "$innerloop" -eq 3 ];
    then
      break # 尝试 break 2 看看发生什么。
      # （跳出内部和外部循环）。
    fi
  done
  echo
done
echo
exit 0
```

`continue` 命令与 `break` 类似，可选地接受一个参数。普通的 `continue` 结束循环内的当前迭代并开始下次迭代。`continue N` 则终止该循环的所有剩余迭代，并继续上方 N 层循环的下次迭代。

### 示例 10–22. 在更高层循环中继续

```bash
#!/bin/bash
# "continue N" 命令，在第 N 层循环继续。

for outer in I II III IV V # 外部循环
  do
    echo; echo -n "Group $outer:"

    for inner in 1 2 3 4 5 6 7 8 9 10 # 内部循环
    do
      if [ "$inner" -eq 7 ];
      then
        continue 2 # 在第二层继续，即“外部循环”
        # 将上述行替换为简单的 "continue"
        # 查看正常的循环行为。
      fi
      echo -n "$inner "  # 8 9 10 永远不会回显。
    done
done
echo; echo

# 练习：
# 在脚本中为 "continue N" 想出一个有意义的用法。

exit 0
```

# 高级 Bash 脚本指南

```bash
case "$variable" in
  "$condition1"
    command...
    ;;
  "$condition2"
    command...
    ;;
esac
```

![](img/1ce1edffaa36e4f698a85430e71c6d3b_121_0.png)

- 给变量加引号不是强制的，因为不会发生单词拆分。

- 每个行测试行以右括号 `)` 结束。

- 每个条件块以双分号 `;;` 结束。

- 整个 case 块以 `esac` 结束（case 的反向拼写）。

# 示例 10–23. 使用 case

```bash
#!/bin/bash

echo "按下一个键，然后回车。"
read Keypress

case "$Keypress" in
  [a-z]) echo "小写字母";
  [A-Z]) echo "大写字母";
  [0-9]) echo "数字";
  *) echo "标点、空格或其他";
# 允许在 [方括号] 中使用字符范围
esac

# 练习：

# 目前脚本目前是，它接受单个按键，然后退出。
# 修改脚本使其接受连续输入，
# 报告每次按键的输入，并仅在按下 "X" 时才退出。
# 提示：将所有内容封装在 "while" 循环中。
exit 0
```

# 示例 10–24. 使用 case 创建菜单

```bash
#!/bin/bash

# 简单的地址数据库

clear # 清空屏幕。

echo "联系列表*"
echo "      ------ ---"
echo "选择以下人员之一："
echo
```

## 10.4. 测试与分支

# 高级 Bash 脚本指南

```bash
echo "[E]vans, Roland"
echo "[J]ones, Mildred"
echo "[S]mith, Julie"
echo "[Z]ane, Morris"
echo
```

read person

```bash
case "person" in
  # 注意变量加了引号。
  "E" | "e"
    # 接受大写或小写输入。
    echo
    echo "Roland Evans"
    echo "4321 Floppy Dr."
    echo "Hardscrabble, CO 80753"
    echo "(033) 734-3874"
    echo "(303) 734-9892 fax"
    echo "revans@zy.net"
    echo "业务伙伴 & 老朋友"
  # 注意用双分号结束
  # 每个选项。
  "J" | "j"
    echo
    echo "Mildred Jones"
    echo "249 E. 7th St., Apt. 19"
    echo "New York, NY 10009"
    echo "(212) 533-2912"
    echo "(213) 533-9972 fax"
    echo "milliej@loisaida.com"
    echo "女朋友"
    echo "生日: 2月11日"
  # 稍后添加 Smith & Zane 的信息。
  *)
    # 默认选项。
    # 空输入（按回车）也符合这里。
    echo
    echo "数据库中尚。"
esac
```

echo

# 练习：

# 修改脚本使其接受连续输入，

# 而在显示一个地址后就退出。

exit 0

case 的一种非常巧妙的用法是测试命令行参数。

```bash
#! /bin/bash
```

# 高级 Bash 脚本指南

```bash
case "$1" in
")") echo "用法: $0* <filename>"; exit 65; # 无命令行参数，
  # 或者第一个参数为空。
# 注意 $0#*) 是 ${var#pattern} 参数替换。结果是 $0。

-*) FILENAME=$1;
  # 如果作为参数 ($1) 传递的文件名以横杠开头，
  # 将其替换为 /$1
  # 这样后续命令就不会将其解释为选项。

*) FILENAME=$1;
  # 否则，使用 $1。
esac
```

# 示例 10-25. 使用常用替换生成 case 变量



```bash
#!/bin/bash
# 使用命令替换生成 "case" 变量

case $(arch) in
"arch") returns architecture.
echo "arch-based machine";
echo "arch-based machine";
echo "arch-based machine";
esac
```

`case` 结构可以过滤字符串。

### 示例 10-26. 字符串匹配

```bash
#!/bin/bash
# 简单的字符串匹配

match_string ()
{
  MATCH=0
  NOMATCH=1
  # 匹配逻辑
  case "$1" in
    apple)
      MATCH=1
      ;;
    orange)
      MATCH=1
      ;;
  esac

  if [ $MATCH -eq 1 ]; then
    echo "匹配 $1"
  else
    echo "不匹配 $1"
  fi
}

match_string "apple"
match_string "orange"
```

### 示例 10-27. 检查字母

```bash
#!/bin/bash
# 检查字母

case "$1" in
  [apple)
    echo "匹配 $1"
  *)
    echo "不匹配 $1"
  es
```

### 示例 10-28. 使用 select 创建菜单

```bash
#!/bin/bash
# 使用 select 创建菜单

PS3="请选择一个: "

select fruit in "apple" "banana" "cherry" "quit"; do

  case $fruit in

    apple) echo "你选择了苹果" ;;

    banana) echo "你选择了香蕉" ;;

    cherry) echo "你选择了樱桃" ;;

    quit) break ;;

    *) echo "无效选项 $REPLY" ;;

  esac

done
```

```bash
PS3="请选择一个: "

select fruit in "apple" "banana" "cherry" "quit"; do

  case $fruit in

    apple)

      echo "你选择了苹果"

      ;;

    banana)

      echo "你选择了香蕉"

      ;;

    cherry)

      echo "你选择了樱桃"

      ;;

    quit)

      echo "正在退出..."

      break

      ;;

    *)

      echo "无效选项 $REPLY"

      ;;

  esac

done
```

### 示例 10-29. 使用 select 循环输入

```bash
#!/bin/bash
# 使用 select 循环输入

PS3="请选择一个: "

select fruit in "apple" "banana" "cherry" "quit"; do

  case $fruit in

    apple)

      echo "你选择了苹果"

      ;;

    banana)

      echo "你选择了香蕉"

      ;;

    cherry)

      echo "你选择了樱桃"

      ;;

    quit)

      echo "正在退出..."

      break

      ;;

    *)

      echo "无效选项 $REPLY"

      ;;

  esac

done
```

### 示例 10-30. 使用 select 处理文件数组

```bash
#!/bin/bash
# 使用 select 处理文件数组

files=("config.txt" "data.csv" "log.log")

PS3="请选择一个文件: "

select file in "${files[@]}" "quit"; do

  echo "正在处理 $file"

  [[ "$file" == "quit" ]] && break

done
```

### 示例 10-31. 使用 select 处理动态列表

```bash
#!/bin/bash
# 使用 select 处理动态列表

items=$(ls *.txt)

PS3="请选择一个文本文件: "

select item in $items "quit"; do

  echo "你选择了 $item"

  [[ "$item" == "quit" ]] && break

done
```

# 高级 Bash 脚本指南

```bash
bash$ ls -l /usr/share/apps/kjezr/sounds/
total 40 -rw-r--r-- 1 root root 716 Nov 7 2000 reflect.au -rw-r--r-- 1 root 362 Nov 7
```

此命令是一个 `shell` 内置命令，与 `/bin/echo` 不同，尽管它的行为与之相似。

```bash
bash$ type -a echo
echo is a shell builtin
echo is /bin/echo
```

### printf

`printf`（格式化打印），该命令是 `echo` 的增强版。它是 C 语言 `printf` 的一个限制变体，语法略有不同。

`printf 格式字符串... 参数...`

这是 `/bin/printf` 或 `/usr/bin/printf` 命令的 `Bash` 内置版本。请参阅 `printf` 手页（系统命令的）以获取更深入的介绍。

> 旧版本的 `Bash` 可能不支持 `printf`。

## 示例 11-1. printf 的用法

```bash
#!/bin/bash
# printf 演示

PI=3.14159265358979

DecimalConstant=31733

Message1="Greetings,"

Message2="Earthling."

echo

printf "Pi to 2 decimal places = %1.2f" $PI

echo

printf "Pi to 9 decimal places = %1.9f" $PI  # 它甚至可以正确四舍五入。

printf "\n"

  # 打印换行符，
  # 等同于 'echo'

printf "Constant = \t%d\n" $DecimalConstant  # 插入制表符 (\t)

printf "%% %s \n" $Message1 $Message2

echo

------------------------------------

# 模拟 C 函数 'sprintf'。

# 使用格式化字符串加载变量。
```

第 11 章 内内部命令与内置命令 123

# 高级 Bash 脚本指南

```bash
echo

PI12=$(printf "%1.12f" $PI)

echo "Pi to 12 decimal places = $PI12"

Msg=$(printf "%s \n" $Message1 $Message2)

echo $Msg; echo $Msg

# 恰好，'printf' 函数现在可以作为可加载模块被到 Bash 访问，但这没有可移植性。

exit 0
```

格式化错误消息是 `printf` 的一个有用应用

```bash
E_BADDIR=65

var=nonexistent_directory

error() {

    printf "%s" >&2

    # 格式化传递的参数并将其发送到标准错误 stderr。

    echo

    exit $E_BADDIR

}
```

`cd $var || error "Can't cd to %s" "$var"`

# 感谢 S.C.

`"read"` 从标准输入读取变量值，交互式地从键盘获取输入。`-a` 选项允许读取数组变量（参见示例 26–2）。

## 示例 11-2. 变量赋值，使用 read

```bash
#!/bin/bash

echo -n "Enter the value of variable 'var1':"

# echo 的 -n 选项抑制换行符。

read var1

# 注意 var1 前没有 '$'，因为它正在被赋值。

echo "var1 = $var1"

echo

# 单个 'read' 语句可以设置多个变量。

echo -n "Enter the values of variables 'var2' and 'var3' (separated by a space or tab):"

read var2 var3

echo "var2 = $var2 var3 = $var3"

# 如果你只输入一个值，另一个变量将保持未设置状态（空）。

exit 0
```

第 11 章 内部命令与内置命令

# 高级 Bash 脚本指南

通常情况下，在 `read` 的输入期间输入 `\` 会抑制换行符。`-r` 选项导致输入的 `\` 被视为字面量解释。

## 示例 11–3. read 的多行输入

```bash
#!/bin/bash

echo

echo "Enter a string terminated by a \,, then press <ENTER>"

echo "Enter, enter a second string, and again press <ENTER>"

read -d var1

    # 在读取 "var1" 时，\ 抑制了换行符
    # 第一行
    # 第二行

echo "var1 = $var1"

    # var1 = 第一行 第二行

# 对于每一行以 \ 结尾的行
# 你会在下一行获得提示，以继续向 var1 输入字符。

echo;

echo "Another string terminated by a \,, then press <ENTER>"

read -r var2

    # -r 选项导致 \ 被字面量读取。
    # 第一行 \

echo "var2 = $var2"

    # var2 = 第一行 \

# 数据输入在第一个 <ENTER> 结束。

echo

exit 0
```

`read` 命令有一些有趣的选项，允许回显提示符甚至在不按回车的情况下回显按键。

```bash
# read 命令 允许回显提示符甚至在不按回车的情况下回显。

read -p "提示: "

# -s 选项会隐藏输入（静默）。
# -r 选项防止反斜杠被作为转义符。
# -n 选项在读取指定字符数后停止。
# -p 选项允许在输入前显示提示符。
# -t 选项设置超时。
# -d 选项指定结束分隔符。
# -a 选项允许读取到数组。
# -u 选项允许从文件描述符读取。
```

`read` 命令具有一些有趣的选项，允许回显提示符甚至在不按回车的情况下回显按键。

```bash
# read 示例

read -p "请输入姓名: " name

echo "你好， $name"

read -s -p "请输入密码: " password

echo -e "\n密码已设置"

read -n 5 char

echo "你输入了前 5 个字符: $char"

read -t 5 timeout || echo "在 5 秒内未输入内容"

read -d "" line

echo "你读取了整个输入：$line"
```

`read` 命令具有一些有趣的选项，允许回显提示符甚至在不按回车的情况下回显按键。

```bash
# read 选项说明

-s 选项会隐藏输入。

-r 选项防止反斜杠被作为转义符。

-p 选项允许显示提示符。

-d 选项指定指定结束符符

--a 选项允许读取到数组。

-u 选项允许从文件描述符读取。
```

`read` 命令具有一些有趣的选项，允许回显提示符甚至在不按回车的情况下回显按键。

```bash
# 使用 read 的示例

read -p "请输入用户名: " username

echo "欢迎, $username"

read -s -p "请输入密码: " password

echo -e "\n密码已保存"

read -n 1 char

echo -e "\n你输入了字符: $char"
```

`read` 命令具有一些有趣的选项，允许回显提示符甚至在不按回车的情况下回显按键。

```bash
# read 常用用法

read [变量名]
```

`read` 是一个 `shell` 内置命令，用于从标准输入读取行。

- `-a`：将读取的内容存储到数组。
- `-d`：指定分隔符（默认为 `\n`）。
- `-e`：使用 `readline` 编辑器功能。
- `-f`：指定文件名。
- `-i`：忽略大小写模式。
- `-n`：读取指定字符数后停止。
- `-p`：显示提示符。
- `-r`：禁用反斜杠转义功能。
- `-s`：静默模式。
- `-t`：设置超时（秒）。
- `-u`：从指定的文件描述符读取。

## 示例 11-2. 变量赋值，使用 read

```bash
#!/bin/bash

echo -n "Enter the value of variable 'var1':"

# echo 的 -n 选项抑制换行符。

read var1

# 注意 var1 前没有 '$'，因为它正在被赋值。

echo "var1 = $var1"

echo

# 单个 'read' 语句可以设置多个变量。

echo -n "Enter the values of variables 'var2' and 'var3' (用空格或制表符分隔):"

read var2 var3

echo "var2 = $var2 var3 = $var3"

# 如果你只输入一个值，另一个变量将保持未设置状态（空）。

exit 0
```

第 11 章 内部命令与内置命令

# 高级 Bash 脚本指南

通常情况下，在 `read` 的输入期间输入 `\` 会抑制换行符。`-r` 选项导致输入的 `\` 被视为字面量解释。

## 示例 11–3. read 的多行输入

```bash
#!/bin/bash

echo

echo "输入一个以 \ 结尾的字符串，然后按 <ENTER>"

echo "输入，再输入第二个字符串，再次按 <ENTER>"

read -d '' var1

    # 在读取 "var1" 时，\ 抑制了换行符
    # 第一行
    # 第二行

echo "var1 = $var1"

    # var1 = 第一行 第二行

# 对于每一行以 \ 结尾的行
# 你会在下一行获得提示，以继续向 var1 输入字符。

echo;

echo "输入另一个以 \ 结尾的字符串，然后按 <ENTER>"

read -r var2

    # -r 选项导致 \ 被字面量读取。
    # 第一行 \

echo "var2 = $var2"

    # var2 = 第一行 \

# 数据输入在第一个 <ENTER> 结束。

echo

exit 0
```

`read` 命令具有一些有趣的选项，允许回显提示符甚至在不按回车的情况下回显按键。

`read` 命令具有一些有趣的选项，允许回显提示符甚至在不按回车的情况下回显按键。

```bash
# 使用 read 的示例

read -p "请输入用户名: " username

echo "你好， $username"

read -s -p "请输入密码: " password

echo -e "\n密码已保存"
```

`read` 命令具有一些有趣的选项，允许回显提示符甚至在不按回车的情况下回显按键。

```bash
# read 常用用法

read [变量名]
```

`read` 是一个 `shell` 内置命令，用于从标准输入读取行。

- `-a`：将读取的内容存储到数组。
- `-d`：指定分隔符（默认为 `\n`）。
- `-e`：使用 `readline` 编辑器功能。
- `-f`：指定文件名。
- `-i`：忽略大小写模式。
- `-n`：读取指定字符数后停止。
- `-p`：显示提示符。
- `-r`：禁用反斜杠转义功能。
- `-s`：静默模式。
- `-t`：设置超时（秒）。
- `-u`：从指定的文件描述符读取。

# 高级 Bash 脚本指南

### 示例 11–6. 使用 `let` 进行算术运算。

```bash
#!/bin/bash

echo

let a=11      # 等同于 'a=11'

let a=a+5     # 等同于 let 'a = a + 5'

              # (引号和空格使其更具可读性)

echo 11 + 5   $a

let a <<=3    # 等同于 let 'a = << 3'

echo "$a"    # (16) 左移 3 位 $a

let a /=4     # 等同于 let 'a = a / 4'

echo 128 / 4  $a

let a -=5     # 等同于 let 'a = a - 5'

echo 32 - 5   $a

let a *=10    # 等同于 let 'a = a * 10'

echo 27 * 10  $a

let a %=8      # 等同于 let 'a = a % 8'

echo 270 modulo 8 = $a (270 / 8 = 33, 余数为 $a)

echo

exit 0
```



`eval`

`eval arg1 [arg2] ... [argN]`
翻译列表中的命令（用于在脚本内部生成代码）。

### 示例 11–7. 显示 `eval` 的效果

```bash
#!/bin/bash

y='eval ls -1'  # 类似于 y='ls -1'

echo $y        # 但由于 'echoed' 变量未加引号，换行符被移除

echo

echo "$y"     # 变量加引号时保留了换行符

echo; echo

y=eval df       # 类似于 y=df

echo $y       # 但换行符被移除。

# 当 LF 未被保留时，它可能更容易解析输出，

# 使用诸如 "awk" 等工具。

exit 0
```

### 示例 11–8. 强制退出

```bash
#!/bin/bash

# 高级 Bash 脚本指南
y='eval ps ax | sed -n '/ppp/p' | awk '{ print $1 }'

# 查找 'ppp' 的进程号。

kill -9 sy      # 杀死它

# 上述行可以替换为

# kill -9 ps ax | awk /ppp/ { print $1 }
```

```bash
chmod 666 /dev/tty3

# 执行 SIGKILL 会改变串口的

# 权限。将它们恢复到之前的状态。

rm /var/lock/LCK..tty3      # 移除串口锁文件。

exit 0
```

### 示例 11–9. "rot13" 的版本

```bash
#!/bin/bash

# 使用 'eval' 的 "rot13" 版本。

# 与 "rot13.sh" 示例对比。

setvar_rot13() {

    "rot13" 乱

    local varname=$1 value=$2

    eval varname=$(echo "$value" | tr a-z n-a-m)

}

setvar_rot_13 var "foobar"      # 通过 rot13 执行 "foobar"。

echo $var                      # sbone

echo $var | tr a-z n-a-m      # 回到原始变量。

# 此示例由 Stephane Chazelais 编写。

exit 0
```

`eval` 命令可能具有风险性，当存在合理的替代方案时通常应避免使用。`eval $COMMANDS` 执行 `COMMANDS` 的内容，其中可能包含令人讨厌的操作，如 `rm -rf *`。对他人编写的未知代码运行 `eval` 是危险的。

### `set`

`set` 命令更改内部脚本变量的值。此命令用于帮助确定脚本的行为。它的另一个应用是重置脚本视为命令结果的位置参数（`set` 命令）。然后脚本可以解析命令输出的字段。

#### 示例 11–10. 将 `set` 用于位置参数

```bash
#!/bin/bash

# 脚本 "set-test"

# 使用三个命令行参数调用此脚本，

# 例如 ./set-test one two three。

echo "set 之前的位置参数:"

echo "命令行参数 = $1"

echo "命令行参数 = $2"

echo "命令行参数 = $3"

echo "set 之后的位置参数:"

# $1, $2, $3 重新初始化为命令的结果

echo "字段 #1 = $1"

echo "字段 #2 = $2"

echo "字段 #3 = $3"

exit 0
```

参见示例 10–2。`unset` 命令删除变量，实际上是将其设置为空。注意，此命令不影响位置参数。

```bash
unset PATH

echo $PATH
```

#### 示例 11–11. “取消设置”变量

```bash
#!/bin/bash

# unset.sh

variable=hello # 初始化

echo "variable = $variable"

unset variable # 取消设置。

echo "variable = $variable" # variable 为空。

exit 0
```

`export` 命令使变量在运行的脚本或 shell 的所有子进程中可用。遗憾的是，没有方法可以将变量导出回调用或唤起该脚本的父进程。`export` 命令的一个重要用途是在启动文件中，用于初始化变量并让后续进程可以访问。

#### 示例 11–12. 使用 `export` 将变量传递给嵌入式 `awk`

```bash
#!/bin/bash

# getopts 的另一个版本 "gettotal" 脚本

# 传递选项和参数到 awk。

# 使用环境变量传递列号。

ARGS=2

if [ $# -ne "$ARGS" ]; then # 检查参数数量

    echo "用法: $0"

    exit 1

fi

filename=$1

column_number=$2

# 到此为止

export column_number

# 将列号导出到环境变量，以便获取。

# 开始 awk 脚本。

awk '{ total += ENV["column_number"] } END { print total }' $filename

# awk 脚本结束。

# 感谢 Stephanie。

exit 0
```

可以在同一操作中初始化并导出变量，如 `export var=xxx`。

### `declare`, `typeset`

`declare` 和 `typeset` 命令指定并或限制变量的属性。

### `readonly`

`readonly` 将变量设置为只读，实际上将其视为常量。尝试更改变量将报错。这是 shell 对 C 语言 `const` 修饰符的功能。

### `getopts`

这个强大的工具解析命令行参数到脚本。这是 C 程序员熟悉的 `getopt` 函数。它允许将多个选项和关联参数传递给脚本（例如 `scriptname -abc -e`）。

`getopts` 构建两个隐式变量。`$OPTIND` 是选项索引，`$OPTARG`（OptionArgument）是附加到选项的（可选）参数。声明选项名称后的冒号标记该选项具有关联参数。

`getopts` 通常封装在 `while` 循环中，一次处理一个选项和参数，递减隐式的 `$OPTIND` 变量以进入下一个。

1. 参数必须带有减号 (`-`) 或加号 (`+`) 前缀从命令行传递给脚本。前缀 `+` 让 `getopt` 识别命令行参数作为选项。事实上，`getopts` 在遇到第一个缺少这些前缀的参数时将停止选项处理。
2. `getopts` 与标准的 `while` 循环略有不同，它缺少条件括号。
3. `getopts` 取代了过时的 `getopt` 命令。

```bash
while getopts ":abc:fg" opt

# 初始化。

# a, b, c, d, e, f 和 g 是预期的选项（标志）。

# 选项 e 后面的冒号显示它将有一个参数。

do

  case $opt in

    a) 对变量 'a' 执行操作。

    b) 对变量 'b' 执行操作。

    e) 对 'e' 执行操作，并对 $OPTARG 执行操作

        # 它是选项 'e' 传递的关联参数。

    g) 对变量 'g' 执行操作。

  esac

done

shift $((OPTIND - 1))

# 移动参数指针到下一个。

# 这些内容看起来并不那么复杂 <grin>
```

```bash
# 尝试用以下方式调用脚本

# 'scriptname -mn'

# 'scriptname -oqQOption' (qOption 可以是任意字符串。)

# 'scriptname -qXXX -r'

# 'scriptname -qr-' 意外结果，将 "r" 作为选项 "q" 的参数

# 'scriptname -qr-' 意外结果，与上述相同

# 如果选项需要一个参数（"flag"），它将捕获

# 命令行上的下一个内容。

NO_ARGS=0

OPTERROR=0

if [ $# -eq "$NO_ARGS" ]; # 脚本调用时没有命令行参数？

then

    echo "Usage: $(basename $0) options (-mnopqrs)"

    exit $OPTERROR # 如果给了任何参数(s)，则退出并解释用法。

fi

# 用法：scriptname -options

# 注意：横字符 (-) 是必要的

while getopts ":mnopqrs" opt

do

    case "$opt" in

        m) echo "Scenario #1: option -m-"

        n | o) echo "Scenario #2: option -Option-";

        p) echo "Scenario #3: option -p-"

        q) echo "Scenario #4: option -q- with argument \$OPTARG\"\n            # 注意 'q' 必须有一个关联参数，

            # 否则它将回退到默认值。

        r | ) echo "Scenario #5: option -Option'";

        *ac) echo "Unimplemented option chosen."" # 默认

    esac

done

shift $((OPTIND - 1))

# 减少参数指针使其指向下一个参数。

exit 0
```

#### 脚本行为

### `source .` (点命令)

此命令从命令行调用，执行一个脚本。在脚本内部，`source file-name` 加载该文件名。这在 shell 脚本中相当于 C/C++ 的 `#include` 指令。在多个脚本使用公共数据文件或函数库的情况下它非常有用。

#### 示例 11-14。“包含”一个数据文件

```bash
#!/bin/bash

# 加载数据文件。

data-file # 与 "source data-file" 相同，但更具可移植性。

# 文件 "data-file" 必须在当前工作目录下，

# 因为它是通过其 'basename' 引用的。

# 现在，从该文件中引用一些数据。

echo variable1 (from data-file) = $variable1

echo variable3 = $variable3

let sum = $variable2 + $variable4

echo "sum" of variable2 + variable4 (from data-file) = $sum"

echo "message" (from data-file) = \$message1\"

# 注意：

    转义引号

print_message This is the message-print function in the data-file.

exit 0
```

上述示例 11-14 的数据文件。必须存在于相同目录。

```bash
# 这是一个由脚本加载的数据文件。

# 此类型的文件包含变量、函数等。

# 它可能被 shell 脚本通过 'source' 或 '.' 命令加载。

# 我们来初始化一些变量。

variable1=22

variable2=47

variable3=5

variable4=97

message="Hello, how are you?"

message2="Enough for now. Goodbye."

print_message ()

{

# 回显传递给它的任何消息。

if [ -z "$1" ];

then

    return 1

    # 如果缺少参数，则报错。

fi

echo

until [ -z "$1" ];

do

    # 遍历传递给函数的参数。

    echo -n "$1"

    # 一次显示参数，抑制换行。

    echo -n ""

    # 在单词间插入空格。

    shift

    # 下一个。

done

echo

return 0

}
```

### `exit`

无条件地终止脚本。`exit` 命令可以可选地接受一个整数参数，该参数将作为脚本的退出状态返回给 shell。让所有简单的脚本以 `exit 0` 结尾是一种良好的习惯，表示运行成功。

如果脚本在缺少参数的情况下通过 `exit` 退出，则退出状态为脚本中执行的最后一个命令的退出状态（不包括 `exit` 本身）。

### `exec`

这个内置命令用当前进程替换指定的命令。通常情况下，当 shell 遇到 `exec` 时，会创建一个子进程来实际执行。使用 `exec` 内置命令，它不会 `fork`，而是替换 shell。在脚本中使用时，它会强制从脚本终止。对于 `exit`，如果 `exit` 后面没有参数，则退出状态是脚本中执行的最后一个命令的退出状态。

#### 示例 11–15. `exec` 的影响

![](img/1ce1edffaa36e4f698a85430e71c6db_140_0.png)

```bash
#!/bin/bash

exec echo "Exiting\"" # 退出脚本。

# 以下行不会执行。

echo "This will never echo."

exit 0 # 在此处不退出。
```

`--exec` 选项 `find` 并不是 shell 内置命令。

### `shopt`

这个命令允许动态更改 shell 选项（参见示例 24–1 和 24–2）。它经常出现在 Bash 启动文件中，但需要 Bash 2 或更高版本。

```bash
shopt -s cd

# 允许对 'cd' 的拼写错误。

command.
```

### `command`

### `true`

一个返回成功（零）退出状态但不执行其他操作命令。

```bash
# 无限循环

while true alias for ":"

do

  operation-1

  operation-2

  ...

  operation-n

  # 需要一种退出循环的方法。
```

### `false`

一个返回不成功退出状态但不执行其他操作命令。

```bash
# 空循环

while false

do

  # 以下代码不会执行。
```

### `exit`

`exit` 命令终止脚本。退出状态的最后一个命令。

```bash
ls -l &

echo "Done."

wait

bash$ ./test.sh

Done.

[bozo@localhost-test-scripts]$ total 1

-rwxr-xr-x 1 bozo bozo 34 Oct 11 15:09 test.sh
```

将命令输出重定向到文件甚至 `/dev/null`。

### `suspend`

这与 `Control-Z` 的效果类似，但它会暂停 shell（shell 的父进程）。你可以在适当的时间恢复它。

### `logout`

退出登录 shell，可以选择指定退出状态。

### `times`

给出执行命令时使用的系统时间统计，格式如下：

```
0m0.020s 0m0.020s
```



这种能力价值有限，因为对 shell 脚本进行分析和基准测试并不常见。

## `kill`

通过向进程发送适当的终止信号来强制终止进程（参见示例 13–4）。

![](img/1ce1edffaa36e4f698a85430e71c6d3b_144_0.png)

`kill -1` 列出所有信号。`kill -9` 是“强杀”，通常会终止顽固拒绝普通 `kill` 杀死的进程。有时 `kill -15` 有效。“僵尸进程”是指父进程已终止（你无法杀死它），且无法被杀死（已经死亡），但系统通常迟晚会清理它。

## `command`

`command COMMAND` 会禁用命令 "COMMAND" 的所有别名和函数。

![](img/1ce1edffaa36e4f698a85430e71c6d3b_144_1.png)

这是影响脚本命令处理的三个 shell 指令之一。另外两个是 `builtin` 和 `enable`。

## `builtin`

# 11.1. 作业控制命令

# 高级 Bash 脚本指南

调用 `builtin` `BUILTIN_COMMAND` 会作为 shell 内置命令运行命令 "BUILTIN_COMMAND"，临时禁用同名的函数和外部系统命令。

## `enable`

这用于启用或禁用 shell 内置命令。例如，`enable -n` 会禁用 shell 内置的 `kill`，因此当 Bash 随后遇到 `kill` 时，它会调用 `/bin/kill`。

`enable` 的 `-a` 选项列出所有 shell 内置命令，并指示它们是否已启用。`-f` 文件选项允许从编译的对象的文件作为共享库（DLL）模块加载。[127]

## `autoload`

这是 `ksh` 自动加载器在 Bash 中的移植。使用 `autoload` 后，带有 "autoload" 声明的函数将在首次调用时从外部文件加载。[28] 这节省了系统资源。

注意 `autoload` 不是 Bash 核心安装的一部分。它需要通过 `enable -f` 加载。

# 表 11–1 作业标识符

| 符号 | 含义 |
|--- |--- |
| `%N` | 作业号 `[N]` |
| `%S` | 作业启动（命令行）以字符串 `S` 开头 |
| `?S` | 作业启动（命令行）包含字符串 `S` |
| `%#` | “当前”作业（上一个在前台停止或在后台启动的作业） |
| `%+` | “当前”作业（上一个在前台停止或在后台启动的作业） |
| `%-` | 上一个作业 |
| `%!` | 上一个后台进程 |

# 11.1. 作业控制命令

# 第 12 章. 外部过滤器、程序和命令

标准的 UNIX 命令让 shell 脚本更加灵活。脚本的威力源于系统命令、shell 指令与简单编程构造的结合。

## 12.1 基础命令

### 命令列表

基础的文件“列出” (`list`) 命令。人们很容易低估这个谦逊命令的力量。例如，使用递归选项 `-R`，`ls` 可以提供目录结构的树形列出。其他风趣的选项还有 `-s`（按文件大小排序）、`-t`（按修改时间排序）和 `-i`（显示文件 `inode`，参见示例 12-3）。

#### 示例 12-1. 使用其为刻录 CDR 创建目录

```bash
#!/bin/bash

SPEED=2                # 如果你的硬件支持，可以使用更高速度
IMAGEFILE=cdimage.iso
CONTENTSFILE=contents
DEFAULTDIR=/opt       # 确保此目录存在。

# 自动化刻录 CDR 的脚本。
# 使用 Josef Schilling 的 "cdrecord" 包。
# (http://www.fokus.de/ntyp/employees/schilling/cdrecord.html)

# 如果以普通用户调用此脚本，需要以 root 身份执行
# sudo cdrecord
# chmod u+s /usr/bin/cdrecord

if [ -z "$1" ];
then
    IMAGE_DIRECTORY=$DEFAULTDIR
    # 如果命令行未指定，则使用默认目录。
else
    IMAGE_DIRECTORY=$1
fi

ls -lRF $IMAGE_DIRECTORY

# ... (此处省略脚本后续逻辑，原文存在重复且逻辑混乱)
```

# 高级 Bash 脚本指南

```bash
do
badname=`echo -n "$filename" | sed -n '/\+\([^\\\"\(\()\\&*\\]/p'`
# 包含这些讨厌字符的文件:      + \; " = ? - <>& * |
rm $badname>/dev/null #这样错误信息会被深度切分。
done
```

```bash
# 现在，处理包含各种空白字符的文件。
find -name "*" -exec rm -f {} \;
# find 替换 "{}" 的文件路径。
# \; 确保了 '{}' 被视为字面量，即作为命令的结束。
```

```bash
exit 0
# 此行之后的命令将不会因为 "exit" 而执行：
```

```bash
# 上述脚本的替代方案：
find -name "*[^\"\\?\\<>&\\$*]*" -exec rm -f '{}' \;
exit 0
# (感谢 S.C.)
```

#### 示例 12-3. 通过节点号删除文件

```bash
#!/bin/bash
# idelete.sh: 通过节点号删除文件
# 当文件名以非法字符开头时这非常有用
# 例如 ? 或 -
```

```bash
ARGCOUNT=1      # 文件名参数必须传递给脚本。
E_WRONGARGS=70
E_FILE_NOT_EXIST=71
E_CHANGED_MIND=72
```

```bash
if [ $# -ne "$ARGCOUNT" ];
then
  echo "Usage: basename $0 filename"
  exit $E_WRONGARGS
fi
if [ ! -e "$1" ];
then
  echo "File \"$1\" does not exist."
  exit $E_FILE_NOT_EXIST
fi
```

```bash
inum=`ls -i | grep "$1" | awk '{print $1}'`
# inum =文件的索引（inode）号。
# 每个文件都是一条索引记录，记录包含其物理地址。
echo; echo -n "Are you absolutely sure you want to delete \"$1\" (y/n)? "
read answer
case "$answer" in
[nN]) echo "Changed your mind, huh?"
    exit $E_CHANGED_MIND
    ;;
*) echo "Deleting file \"$1\"."
esac
find -inum $inum -exec rm {} \;
echo "File \"$1\" deleted!"
```

## 12.2. 复杂命令

使用 `find` 的脚本请参见 [示例 12–22]、[示例 4–4] 和 [示例 10–9]。其手册页提供了此复杂且强大的命令的更多细节。

### `xargs`

一个向命令提供参数的过滤器，也是一个构建命令本身的工具。它将数据流拆分成小块供过滤器和命令处理。将其视为反引号的强大替代品。在反引号因参数过多而失败的情况下，替换为 `xargs` 是行之有效的。通常情况下，`xargs` 从 `stdin` 或管道读取，也可以从文件的输出中读取。

`xargs` 的默认命令是 `echo`。这意味着管道到 `xargs` 的输入可能会被删除换行符和其他空白字符。

```bash
bash$ ls -l
total 0
-rw-rw--      1 bozo bozo 0 Jan 29 23:58 file1
-rw-rw--      1 bozo bozo 0 Jan 29 23:58 file2
```

```bash
bash$ ls -1 | xargs
total 0 -rw-rw-- 1 bozo 0 Jan 29 23:58 file1 -rw-rw-- 1 bozo 0 Jan 29 23:58
```

`ls | xargs -p -I gzip gzip {}` 一次处理当前目录下的每个文件，并对每次操作都进行提示。

![](img/1ce1edffaa36e4f698a85430e71c6d3b_151_0.png)

一个有趣的 `xargs` 选项是 `-n NN`，它限制传递的参数数为 `NN`。

`ls | xargs -n 8 echo` 以 8 列列出当前目录下的文件。

![](img/1ce1edffaa36e4f698a85430e71c6d3b_151_0.png)

另一个实用的选项是 `-0`，与 `find -print0` 结合使用可以处理包含空格或引号的参数。

```bash
find ... -print0 | xargs -0 rm
```

上述命令将删除任何包含 "GUI" 的文件。（感谢 S.C.）

# 12.2. 复杂命令（注：由于提供的原始文本存在大量 OCR 识别错误和重复，此处译文已根据核心逻辑进行了清理和整合翻译）

# 高级 Bash 脚本指南

```bash
#!/bin/bash
# 练习 'date' 命令
echo "从今年年初开始的天数是 `date +j`"
# 需要用 '+' 来调用格式化。
# %j 表示一年中的天数。

echo "从 1970/01/01 至今经过的秒数是 `date +s`"
# % 产生自 'UNIX 纪'开始以来的秒数，
# 这有什么用呢？

prefix=temp
suffix=date+%s # 'date' 的 '%s' 选项是 GNU 特有的。
filename=$prefix.$suffix
echo $filename

# 它非常适合创建“唯一”的临时文件名，
# 比 $$ 更好。

查看 'date' 手页以获取格式化选项。
exit 0
```

```bash
$ bash date
Fri Mar 29 21:07:39 MST 2002
$ date -u
Sat Mar 30 04:07:42 UTC 2002
```

- `-u` 选项提供 `UTC`（世界协调时间）。

### `dump`

在指定的时区输出时间。

```bash
$ dump EST
EST Tue Sep 18 22:09:22 2001 EST
```

### `time`

输出执行命令时非常详细的计时统计信息。

```
0.00user 0.01system 0:00:05elapsed 16CPU (0avgtext+0avgdata 0maxresident) 0inits+0ncswitch (149major+27minor)pagefaults 0swaps
```

参见上一节中非常类似的 `times` 命令。

![](img/1ce1edffaa36e4f698a85430e71c6d3b_156_0.png)

从 Bash 2.0 版本开始，`time` 变成了一个 shell 保留字，在管道中的行为略有不同。

## 12.3 时间 / 日期命令

### `touch`

用于将文件的访问/修改时间更新为当前系统时间或其他指定时间的工具，对于创建新文件也用。`touch zzz` 命令将创建一个长度为零、名为 `zzz` 的新文件，因为 `zzz` 之前不存在。以这种方式对空文件进行时间标记对于存储数据信息、跟踪项目修改时间很有用。

`touch` 命令等同于：`touch new`（对于普通文件）。

### `at`

`at` 作业控制在指定时间执行一组命令。表面上，它类似于 `crond`，然而，`at` 主要用于一次性执行一组命令。

`at 2pm January 15` 用于在 11 月 15 日下午 2 点执行的一组命令。这些命令应该是与 shell 兼容的，从所有实际角度考虑，用户是在一次一行地输入一个可执行的脚本。输入以 `Ctrl-D` 结束。

使用 `-f` 选项或重定向 (`<>`)，`at` 从文件中读取命令列表。该文件是一个可执行脚本，尽管它，当然，是非交互的。特别聪明的做法是在文件中包含 `run-parts` 命令来执行不同的脚本集。

```bash
$ bash at 2:30 am Friday < at-jobs.list
job 2 at 2000-10-27 02:30
```

### `batch`

`batch` 作业控制命令与 `at` 类似，但在当系统负载低于 8 时运行命令列表。和 `at` 一样，它可以使用 `-f` 选项从文件中读取命令。

### `cal`

向 `stdout` 打印格式化良好的每月日历。将处理当前年份或过去及未来的大范围年份。

### `sleep`

这是 shell 等同于等待循环。它暂停指定的秒数，什么都不做。这对于计时或在运行的进程中很有用。这可以用于计时或在运行的进程中。这可以用于计时或很有用。

```bash
sleep 3
# 暂停3 秒。
```

![](img/1ce1edffaa36e4f698a85430e71c6d3b_156_0.png)

从 Bash 2.0 版本开始，`time` 变成了一个 shell 保留字，在管道中的行为略有不同。

`sleep` 命令默认是分钟、小时，或可以指定。

```bash
sleep h
# 暂停小时。
```

### `usleep`

微秒级睡眠（"u" 是 `sleep` 的微秒版）。这和 `sleep` 相同，但在微秒间隔。

```bash
usleep 30
# 暂停30 微秒。
```

`usleep` 命令不提供精确的计时，因此不适用于关键循环。

### `hwclock`, `clock`

`hwclock` 命令访问或调整机器的时钟。某些选项需要 `root` 权限。`clock` 命令是 `hwclock` 的同义词。

## 12.4 文本命令

### 命令列表

#### `sort`

文件排序器，经常作为管道的过滤器。使用 `-m` 选项，它合并已排序的文件。它的信息页列出了许多功能。

#### `tsort`

拓扑排序。

`tsort` 拓扑排序，根据空格分隔的字符串进行拓扑排序。

#### `diff`, `patch`

`diff`：灵活的文件比较工具。它按行比较目标文件。在某些应用程序中，作为比较字典，可能先通过 `sort` 和 `uniq` 过滤文件再传递给 `diff`。

```bash
diff --y
# side-by-side 选项到 diff 会输出每个比较的文件，并标记不匹配的行。
```

`diff` 有各种漂亮的前端，如 `spiff`, `wdiff`, `xdiff` 和 `mgdiff`。

### 12.4 文本命令

#### `diff`

如果比较的文件相同，`diff` 命令返回退出状态 0，如果不同则返回 1。

#### `sdiff`

比较两个文件并将它们合并到输出文件中。由于其交互性，此命令在脚本中用处不大。

#### `cmp`

`cmp` 命令是上面 `diff` 的简单版本。`diff` 报告两个文件之间的差异，`cmp` 仅显示它们差异的地方。

![](img/1ce1edffaa36e4f698a85430e71c6d3b_160_0.png)

和 `diff` 一样，如果比较的文件相同，`cmp` 返回退出状态 0，如果不同则返回 1。这允许在脚本中使用测试结构。

#### 示例 12–8. 在脚本中使用 `cmp` 比较两个文件。

```bash
#!/bin/bash
# 脚本预期两个参数。
ARGS=2 E_BADARGS=65

if [ $# -ne "$ARGS" ];
then
    echo "Usage: basename $0 file1 file2"
    exit $E_BADARGS
fi
```

```bash
cmp $1 > /dev/null # /dev/null 掩盖了 "cmp" 命令的输出。
# 同样适用于 'diff'即 diff $1 $2 > /dev/null
if [ $? -eq 0 ];
then
    echo "文件 \$1 与文件 \$2 相同。"
else
    echo "文件 \$1 与文件 \$2 不同。"
fi
exit 0
```

# 高级 Bash 脚本指南

◆ `column 3` = 两者共有的行。

这些选项允许隐藏一或多列的输出。

- ◆ `-1` 隐藏第 1 列
- ◆ `-2` 隐藏第 2 列
- ◆ `-3` 隐藏第 3 列
- ◆ `-12` 隐藏第 1 列和第 2 列，以此类推

#### `uniq`

此过滤器从排序后的文件中删除重复行。它通常与 `sort` 配合管道使用。

```bash
cat list-1 list-2 list-3 | sort | uniq > final.list
# 合并列表文件，
# 对它们进行排序，
# 移除重复行，
# 最后将结果写入输出文件。
```

有用的 `-c` 选项会在输入文件的每行前加上该行出现的次数。

```bash
bash$ cat testfile

这一行只出现一次。
这一行出现了两次。
这一行出现了两次。
这一行出现了三次。
这一行出现了三次。
这一行出现了三次。
```

```bash
bash$ uniq -c testfile

1 这一行只出现一次。
2 这一行出现了两次。
3 这一行出现了三次。
```

```bash
bash$ sort testfile | uniq -c | sort -nr

3 这一行出现了三次。
2 这一行出现了两次。
1 这一行只出现一次。
```

`sort INPUTFILE | uniq -c | sort -nr` 命令会生成 `INPUTFILE` 文件的出现频率列表（`-nr` 选项导致反向数值排序）。该模板用于日志文件和字典列表的分析，适用于任何需要检查文档词法结构的地方。

##### 示例 12–9. 词频分析

```bash
#!/bin/bash
# wf.sh: 对文本文件进行粗略词频分析。
```



# 检查命令行是否存在输入文件。

```bash
ARGS=$1

E_BADARGS=65

## 12.4 文本处理命令

E_NOFILE=66

if [ $# -ne "$ARGS" ]; then # 传递脚本的参数数量是否正确？
    echo "用法: `basename $0 filename`"
    exit $E_BADARGS
fi

if [ ! -f "$1" ]; then # 检查文件是否存在。
    echo "文件 \$1 不存在。\n"
    exit $E_NOFILE
fi
```

```bash
############################################################
# main ()
sed -e 's/\.'//g' -e 's/ | -c/g' "$1" | tr 'A-Z-a-z' | sort | uniq | sort -nr
############################################################
    出现频率
# 过滤掉句号并
+# 将单词之间的空格替换为行符，
+# 然后将字符转换为小写，
+# 最后前加上出现计数并进行数值排序。
############################################################
# 练习：
# 1) 添加 'sed' 命令来过滤其他标点符号，如逗号。
# 2) 修改以过滤多个空格和其他空白字符。
# 3) 添加次要排序键，使得出现次数相同的实例
+# 按字母顺序排序。
```

```bash
bash$ cat testfile
这一行出现一次。
这一行出现两次。
这一行出现两次。
这一行出现三次。
这一行出现三次。
这一行出现三次。
```

```bash
bash$. ./wf.sh testfile
6 this
6 occurs
6 line
3 times
3 three
2 twice
1 only
1 once
```

### `expand`, `unexpand`

`expand` 过滤器将制表符转换为空格。它通常用于管道中。

## 12.4 文本处理命令

`unexpand` 过滤器将空格转换为制表符。这与 `expand` 的效果相反。

### `cut`

一个用于从文件中提取字段的工具。它类似于 `awk` 中的 `print $N` 命令，但功能更具局限。在脚本中使用 `cut` 可能会比使用 `awk` 更简单。特别重要的是 `-d`（分隔符）和 `-f`（字段指定符）选项。

使用 `cut` 获取已挂载的文件系统列表：

```bash
cat /etc/mtab | cut -d ' ' -f1,2
```

使用 `cut` 列出操作系统和内核版本：

```bash
uname -a | cut -d" " -f1,3,11,12
```

使用 `cut` 从邮件文件夹中提取标题头：

```bash
bash$ grep '^Subject:' messages | cut -c10-80
Subject: Linux for mission-critical apps
Subject: Spam
```

使用 `cut` 解析文件：

```bash
# 列出 /etc/passwd 中的所有用户
FILENAME=/etc/passwd
for user in $(cut -d: -f1 $FILENAME)
do
    echo $user
done
# 感谢提供这个建议。
```

`cut -d ' ' -f2,3` 等同于 `awk -F' ' '{print $2,3}'`。

### `join`

将不同文件合并为单个多列文件的工具。与 `cut` 结合使用时，适用于创建系统文件。将其视为 `paste` 的特殊用途亲戚。这个强大的工具允许以有意义的方式合并两个文件，创建一个关系数据库的简单版本。`join` 命令精确地在两个文件上操作，它将具有共同标记字段（通常是数值）的行拼接在一起，并将结果写入标准输出。

| range | action |
|---|---|
| 1.data | 2.data |
| 100 | Shoes |
| 200 | Laces |
| 300 | Socks |

```bash
bash$ join 1.data 2.data
100 Shoes
200 Laces
300 Socks
```

# 高级 Bash 脚本指南

```bash
bash$ grep -n Linux osinfo.txt
2:这是一个包含 Linux 信息的文件。
6:GPL 规定了 Linux 系统的分发。
```

`-v`（或 `--invert-match`）选项会过滤掉匹配项。

```bash
grep pattern1 *.txt | grep -v pattern2
# 匹配 "*.txt" 中所有包含 "pattern1" 的行，
# 但不包含 "pattern2"。
```

`-c` (`--count`) 选项提供匹配项的数字计数，而不是实际列出匹配项。

```bash
grep -c txt *.sgml  # ("txt" 在 "*.sgml" 文件中出现的次数)

grep -cz ^ dot
# 意味着计数 (-c) 以零分隔 (-z) 分隔且匹配 " 的项，
# 即非空项（至少包含 1 个字符）。

printf 'a bnc' d\n\n\n\n\n\n\000\000\nf' | grep -cz # 4
printf 'a bnc' d\n\n\n\n\n\n\000\000\nf' | grep -cz '\$' # 5
printf 'a bnc' d\n\n\n\n\n\n\000\000\nf' | grep -cz '^' # 5
printf 'a bnc' d\n\n\n\n\n\n\000\000\nf' | grep -c '$' # 9
# 默认情况下，换行符 \n 用作匹配项的分隔符。
```

```bash
# 注意 -z 选项是 GNU "grep" 特有的。
```

```bash
# 感谢，S.C.
```

当给出多个目标文件时，`grep` 会指定哪一个文件包含匹配项。

```bash
bash$ grep Linux osinfo.txt misc.txt
osinfo.txt:这是一个包含 Linux 信息的文件。
osinfo.txt:GPL 规定了 Linux 系统的分发。
misc.txt:Linux 操作系统正在流行。
```

> 若要强制 `grep` 在仅搜索单个目标文件时显示文件名，只需将 `/dev/null` 作为源即可。

```bash
bash$ grep Linux osinfo.txt /dev/null
osinfo.txt:这是一个包含 Linux 信息的文件。
osinfo.txt:GPL 规定了 Linux 系统的分发。
```

如果有成功匹配，`grep` 返回退出状态 `0`，这使得它在脚本的条件测试中非常有用，特别是配合使用 `-q` 选项抑制输出时。

```bash
SUCCESS=0 # 如果 grep 查找成功
word=Linux
```

## 12.4. 文本处理命令

```bash
filename=data.file
grep -q "$word" "$filename"    # "-q" 选项导致没有任何输出到标准输出
if [ $? -eq $SUCCESS ]
then
    echo "$filename 中找到了 $word"
else
    echo "在 $filename 中未找到 $word"
fi
```

示例 30-5 展示了如何使用 `grep` 在系统日志文件中搜索单词模式。

# 示例 12-12. 在脚本中模拟 "grep"

```bash
#!/bin/bash
# grep.sh: 'grep' 的非常粗糙的实现
E_BADARGS=65
if [ -z "$1" ]    # 检查脚本参数。
then
    echo "用法: basename $0 pattern"
    exit $E_BADARGS
fi
for file in *      # 遍历 $PWD 下的所有文件。
do
    output=$(sed -n "/$1/p" $file)  # 命令替换。
    if [ ! -z "$output" ];    # 如果 "$output" 没有加引号会怎样？
    then
        echo -n "$file"
        echo "$output"  # sed -ne "/$1/|^|${file}:|p" 等于上述操作。
    fi
done
exit 0
```

# 练习：
# 1) 如果任何给定文件中有多个匹配项，则在输出中添加换行。
# 2) 添加功能。

`egrep` 等于 `grep -E`。它使用了一套稍不同的扩展正则表达式，可以使搜索更灵活。

`fgrep` 等于 `grep -F`。它执行字面字符串搜索（不使用正则表达式），据称

# 12.4. 文本处理命令

可以稍微提高速度。

`agrep` 扩展了 `grep` 的功能以实现近似匹配。搜索字符串与结果匹配项之间允许指定数量的差异。该工具不是 Linux 发行版的核心。

![](img/1ce1edffaa36e4f698a85430e71c6d3b_169_0.png)

要搜索压缩文件，使用 `zgrep`、`zegrep` 或 `zfgrep`。它们也可以用于非压缩文件，尽管速度比普通的 `grep`、`egrep`、`fgrep` 慢。对于搜索混合文件非常方便。

要搜索 `bzipped` 文件，使用 `bgrep`。

`look` 命令的作用类似于 `grep`，但它对“字典”（排序后的列表）进行查找。默认情况下，`look` 在 `/usr/dict/words` 中搜索匹配，但可以指定不同的字典文件。

# 示例 12–13. 检查列表中单词的有效性

```bash
#!/bin/bash
# look: 对数据文件中的每个单词进行字典查找。
file=words.data # 用于测试的单词数据文件。
while [ "$word" != "end" ] # 数据文件中的最后一个单词。
do
    read word < /dev/null # 不显示字典文件中的行。
    lookup=$? # 'look' 命令的退出状态。
    if [ "$lookup" -eq 0 ];
    then
        echo "$word 是有效的。"
    else
        echo "$word 是无效的。"
    fi
done <"$file" # 将 stdin 重定向到 $file，因此“读取”来自那里。
exit 0
------------------------------------------------------------
# 下方的代码将因为 "exit" 命令而不会执行。
```

Stephane Chaselas 提出了以下更简洁的替代方案：

```bash
while read word && [[ $word != "end" ]]
do
    if [ "$word" != "end" ];
    then
        echo "$word 是有效的。"
    else
        echo "$word 是无效的。"
    fi
done
```

（注：OCR 文本在后半部分包含严重的损坏和碎片化的句子。我已根据标准的 Bash 使用法和提供的上下文片段重构了逻辑流。）

```bash
for filename in * # 没有必要使用 basename，
  # 因为 "*" 不会返回包含 "/" 的文件
do
    lower=$(echo "$filename" | tr '[:upper:]' '[:lower:]')
  # POSIX 字符集表示法。
  # 添加末尾的斜杠是为了确保它们
  # 不被命令替换移除。
  # 变量替换：
    n=${filename%/} # 从 filename 中移除上面添加末尾斜杠。
    [[ $filename == $n ]] || mv "$filename" "$n"
  # 检查文件名是否已经是小写。
done
exit 0
```

# 示例 12-16. DOS 到 UNIX 文本文件转换。

```bash
#!/bin/bash
# du.sh: DOS 到 UNIX 文本文件转换
E_WRONGARGS=65
if [ -z "$1" ];
then
    echo "Usage: basename $0 filename-to-convert"
    exit $E_WRONGARGS
fi
NEWFILENAME=$1.unx
CR=$'\x15' # 回车符。
# DOS 文本文件以 CR-LF 结尾。
tr -d $CR < $1 > $NEWFILENAME
# 删除 CR 并写入新文件。
echo "Original DOS text file is \"$1\""
echo "Converted UNIX text file is \"$NEWFILENAME\""
exit 0
```

# 示例 12-17. rot13, rot13，极弱加密。

```bash
#!/bin/bash
# rot13.sh: 经典的 rot13 算法，足以欺骗 3 岁小孩的加密。
# 使用: ./rot13.sh filename
# 或 ./rot13.sh $filename
# 或 ./rot13.sh 并提供键盘输入 (stdin)
cat "$@" | tr 'a-zA-Z' 'n-za-MN-ZA-M' # "a" 变成 "n", "b" 变成 "o", 以此类推。
# "cat @@" 结构
# 允许从 stdin 或文件获取输入。
exit 0
```

# 示例 12-18. 生成“加密引言”谜题

```bash
#!/bin/bash
# crypto-quote.sh: 加密引言

# 将使用简单的单字母替换法加密引言。
# 结果类似于在日报评论版中
# 看到的“加密引言”谜题。

key=ETAOINSHRDULBCFGJMPVW2XYK
# "key" 仅仅是一个乱序的字母表。
# 改变 "key" 就会改变加密。
# 'cat $@' 结构从 stdin 或文件获取输入。
# 如果使用 stdin，用 Control-D 结束输入。
# 否则，指定文件名作为命令参数。

cat "$@" | tr "a-z" "A-Z" | tr "A-Z" "$key"
             # to uppercase             # encrypt
# 支持小写、大写或混合大小写的引言。
# 非字母字符保持不变。

# 输出是：
# "CPHFRCS QF CIIQ MINFERCS EQ FPHIM GIFGUI'Q HETPQ."
# BEEML PZERC

# 要反转加密：
# cat "$@" | tr "A-Z"

exit 0
```

这种简单的密码可以被平均水平的 12 岁孩子仅用铅笔和纸就能破解。

## `tr` 变体

`tr` 工具有两个历史变体。BSD 版本不使用括号（`tr a-z A-Z`），但 SysV 版本使用 `tr '[a-z]' '[A-Z]'`。GNU 版本与 BSD 相似，因此括号内的范围是强制性的。

`fold` 过滤器会将行文本折行到指定的宽度。配合 `-s` 选项使用时特别有用，它会在空格处折行（参见示例 12–19 和示例 A–2）。

这是一个简单的格式化器，用于在管道中“折行”长文本输出。

# 示例 12–19. 格式化列表。

```bash
#!/bin/bash
WIDTH=40                # 40 列宽。
b=$(ls /local/bin)      # 获取文件列表...
echo $b | fmt -w $WIDTH # 也可以通过 echo $b | fold -w 完成。
exit 0
```

`fmt` 的强大替代方案是 Kamil 的 `col` 工具，从 `http://berkeley.edu/~kamil/col/` 获取。它输出文件的置换索引（交叉列表），在必要时可以在管道中进一步过滤和格式化。

`col` 过滤器从输入流中移除行。它还尝试用空格替换制表符。`col` 的主要功能是过滤某些文本处理工具的输出，例如 `groff` 和 `tbl`。

```bash
# 这是对 "column" 手页中文件的微调。
printf "%PERMISSIONS OWNER SIZE HH:MM PROG-NAME\n" \
# -t 选项删除了输出的第一行
ls -l | sed 1d | column -t
# 其中 "N" 是通过 "ls -l" 找到的文件数。
exit 0
```



列移除器。它从文件中移除列（字符），并将每行的第二到第四字符写回`stdout`。

如果文件包含制表符或不可打印字符，可能会导致不可预测的行为。在这种情况下，考虑在`col`之前使用`expand`和`unexpand`。

`nl`将文件名列表到`stdout`，但在每个非空行开头插入连续数字。默认情况下如此。

# 12–21. `nl`: 自动编号脚本。

```bash
#!/bin/bash

# 此脚本将自身回显到 `stdout` 并带有行号。

# 'nl' 将上述行视为第 3，因为它不列出空行。

# 'cat -n' 将上述行视为第 5。

nl 'basename $0'

# 注意 'nl -ba' 也会做到这一点。

exit 0
```

列格式化器。它将文件(`stdout`)分页，用于硬拷贝打印或在屏幕上查看。各种选项允许行和列的操作、合并行、添加页眉以及合并文件等。`pr`命令结合了`nl`、`paste`和`expand`的许多功能。

```bash
pr -o 5 --widths=65 file | # 给出一个 5 和 65 列的精美分页输出。
```

一个特别用的选项是`-d`，强制双倍间距（效果相当于`sed -G`）。一个用于本地化并将程序输出翻译成外语的 GNU 工具。主要用于 C 程序，并在 shell 脚本中使用。一个将文件转换为不同编码（字符集）的工具。它的主要用途是本地化。考虑这个高级版本的`iconv`。这个将文件转换为不同编码的通用工具不是标准 Linux 安装的一部分。

## TeX, gs

- `TeX` 和 `Postscript` 是用于准备打印或格式化视频显示的文本标记语言。

`TeX`是 Donald Knuth 复杂的排版系统。通常编写一个 shell 脚本来封装给这些标记语言之一的所有选项和参数是非常方便的。

`Ghostscript`(`gs`)是一个 GPL Postscript 解释器。

## groff, tbl, eqn

另一种文本标记和显示格式语言是`groff`。它是古老的 UNIX `roff`/`tbl`显示和排版包的增强 GNU 版本。Manpages 使用`groff`（参见示例 A–1）。

`tbl`处理工具被认为是`groff`的一部分，其功能是将表格标记转换为`groff`命令。`eqn`方程处理工具同样是`groff`的一部分，其功能是将方程标记转换为`groff`命令。

## lex, yacc

`lex`词法分析器产生用于模式匹配的程序。在 Linux 系统上已被非专利的`flex`代替`yacc`工具根据一组规范创建解析器。在 Linux 系统上已被非专利的`bison`代替。

## 12.5. 文件和归档命令

### 归档

### tar

标准的 UNIX 归档工具。最初是一个磁带归档（Tape Archiving）程序，它已发展成为一个通用软件包，可以处理所有类型的目标设备，从磁带驱动器到除`stdout`外的所有文件（参见示例 4–4）。GNU `tar`早已修复以接受`gzip`压缩选项，如`tar czvf archive-name.tar.gz *`，它递归地归档并压缩目录树中的所有文件，当前工作目录(`$PWD`)中的隐藏文件。

一些常用的`tar`选项：

1. `-c`（创建新归档）
2. `--delete`（从归档中删除文件）
3. `-r`追加（文件到归档）
4. `-t`列出（归档内容）
5. `-u`更新归档
6. `-x`提取（从归档提取文件）
7. `-z` `gzip`归档

从损坏的 gzipped `tar`归文件中恢复数据可能困难。在归档文件时，请制作多个备份。

### shar

Shell 归档工具。shell 归档中的文件是在不压缩的情况下连接的，生成的归档本质上是一个 shell 脚本，包含`#!/bin/sh`头，并包含所有必要的解包命令。`shar`归档出现在互联网新闻组中，但除此之外`shar`已经被`tar`/`gzip`充分取代。`unshar`命令用于解`shar`归档。

### ar

广泛用于二进制对象文件的归档创建和处理工具。

### cpio

这种专门的归档复制命令（复制输入和输出）已经很少见到，因为它已被`tar`/`gzip`取代。它仍然有其用处，例如移动目录树。

# 示例 12–22. 使用 `cpio` 移动到目录树

```bash
#!/bin/bash

# 使用 cpio 复制目录树

ARGS=2

E_BADARGS=65

if [ $# -ne "$ARGS" ];

then

    echo "Usage: basename $0 destination"

    exit $E_BADARGS

fi

source=$1

destination=$2

find "$source" -depth | cpio -admv "$destination"

# 读取 man 页以解读这些 cpio 选项。

exit 0
```

# 示例 12–23. 解包 `rpm` 归档

```bash
#!/bin/bash

# de-rpm.sh: 解包一个 'rpm'

E_NO_ARGS=65

TEMPFILE=$$.cpio # 带有“唯一”名称的临时文件。
                 # $$ 是脚本的进程 ID。

if [ -z "$1" ]

then

    echo "Usage: basename $0 filename"

    exit $E_NO_ARGS

fi

rpm2cpio < $1 $TEMPFILE # 将 rpm 归档转换为 cpio 归档。

cpio --make-directories -F $TEMPFILE -i # 解包 cpio 归档。

rm -f $TEMPFILE # 删除 cpio 归档。
```

### gzip

标准的 GNU/UNIX 压缩工具，取代了劣质且专有的`compress`。相应的解压缩命令是`gzip -d`。

`zcat`将 gzipped 文件解压到`stdout`，作为管道或重定向的可能输入。这实际上是一个作用于压缩文件的`cat`命令（包括用旧版`compress`工具处理的文件）。`zcat`命令等于`gzip -dc`。

![](img/1ce1edffaa36e4f698a85430e71c6d3b_179_0.png)

> 在某些商业 UNIX 系统上，`zcat`是`uncompress -c`的别名，将无法作用于 gzipped 文件。

另参阅[示例 7–6](#)。

### bzip2

另一种压缩工具，通常比`gzip`更有效率，特别是在处理大文件时。相应的解压缩命令是`bzip2`。

### compress, uncompress

这是在商业 UNIX 发行版中找到的旧专用压缩工具。更有效的`gzip`已在很大程度上取代了它。Linux 发行版通常包含一个兼容的`compress`模拟，尽管`gunzip`可以解包用`compress`处理的文件。

![](img/1ce1edffaa36e4f698a85430e71c6d3b_179_1.png)

> `znew`命令将`compressed`文件转换为 gzipped 文件。

### sq

另一种压缩工具，一个仅作用于排序后的 ASCII 单词列表的过滤器。它使用过滤器的标准调用语法`sq < input-file > output-file`。速度快，但远没有`gzip`高效。相应的解压缩过滤器是`unsq`，调用方式与`sq`一样。

`sq`的输出可以管道到`gzip`进行进一步压缩。

跨平台文件归档和压缩工具，兼容 DOS `PKZIP`。“Zipped”归档在互联网上似乎比“tarballs”（`tar`包）是更易接受的交换媒介。

# 文件信息

### file

一种用于识别文件类型的工具。命令`file file-name`将返回文件的文件的规格，例如 ascii 文本或数据。它引用`/usr/share/magic`、`/etc/magic`或`/usr/lib/magic`中的魔数数，取决于 Linux/Unix 发行版。

`-f`选项导致`file`以批模式运行，读取一个文件名列表进行分析。`-z`选项用于压缩目标文件，强制其分析解压缩后的文件类型。

```bash
$ bash file test.tar.gz

test.tar.gz: gzip compressed data, deflated, last modified: Sun Sep 16 13:34:51 2001, os:

$ bash file -z test.tar.gz

test.tar.gz: GNU archive (gzip compressed data, deflated, last modified: Sun Sep 13
```

# 示例 12–24. 从 C 程序文件中剥离注释

```bash
#!/bin/bash

# strip-comment.sh: 去除 C 程序中的注释 (* COMMENT *)。

E_NOARGS=65

E_ERROR=66

E_WRONG_FILE_TYPE=67

if [ $# -eq "$E_NOARGS" ]

then

    echo "Usage: basename $0" >&2 # 错误消息。

    exit $E_ERROR

fi

# 检查文件类型。

type=$(file $1 | awk '{ print $2,3,4 }') # "file" 删除了这里的第一个字段...

# 然后将结果放入变量 "type"。

if [ "$type" != "ASCII" ]

then

    echo "此脚本仅作用于 ASCII 文件。"

    exit $E_WRONG_FILE_TYPE

fi

# 相当晦涩的 sed:

# 如果你花几个小时学习基础知识，就会很容易理解。

# 需要在 sed 中增加增加行来处理同一行后面紧跟注释的情况。

# 此外，上面的删除了带有“/*”的行。由于 'exit 0'，此行代码不会执行。

# Stephane Chazelas 建议了以下替代方案：

usage() {
    echo "Usage: $0" >&2
    exit 1
}
WEIRD=$(echo $1)
[[ $# -eq 1 ]] && usage
case "$WEIRD" in
    *)
        sed -e "s/\/\*///g;s/\*\///g" "$1"
        )
esac

# 这仍然内容欺骗：
# printf("/*");
# *
# 为了处理特殊情况（行中的注释）...
exit 0
```

`which`提供`command-xxx`的完整路径。这有助于确定特定的命令或工具是否安装在系统中。

```bash
$ bash which rm
/usr/bin/rm
```

### whereis

与`which`，`whereis`提供`command-xxx`的完整路径，但也提供了其 man 页。

```bash
$ bash whereis rm
/bin/rm /usr/share/man/man1/rm.bz2
```

### whatis

`whatis`在 whatis 数据库中查找“file”。这有助于识别系统命令和重要的配置文件。将其视为简化的`man`命令。

```bash
$ bash whatis whatis
whatis (1) search the whatis database for complete words
```

# 示例 12–25. 探索 `/usr/X11R6/bin`

```bash
#!/bin/bash

# /usr/X11R6/bin 中那些神秘的二进制文件是什么？
DIRECTORY="/usr/X11R6/bin"
# 尝试 "/bin", "/usr", "/local/bin" 等。

for file in $DIRECTORY
do
    whatis basename '$file' # 输出二进制信息。
done

exit 0
# 你可能希望重定向 whatis 的输出，如下：
# whatis.sh >>whatis.db
# 或者在标准输出上一页查看，
# whatis.sh | less
```

另参阅示例 10–3。

### vdir

显示详细的目录列表。效果类似于`ls -l`。这是 GNU 文件工具之一。

```bash
$ vdir
total 10
-rw-r--r 1 bozo bozo 4034 Jul 18 22:04 datal.xrolo
-rw-r--r 1 bozo bozo 4602 May 25 13:58 datal.xrolo.bak
-rw-r--r 1 bozo bozo 877 Dec 17 2000 employment.xrolo
```

# 高级 Bash 脚本指南

```bash
exit $E_BADGARS
fi
if [ -f "$1" ]; # 检查文件是否存在
then
    file_name=$1
else
    echo "File \$1\" 不存在。"
    exit $E_NOFILE
fi
```

```bash
MINSTRLEN=3 # 最小字符串长度。
WORDFILE=/usr/share/dict/linux.words # 字典文件。
# 可以指定不同的
# 列表文件
# 格式为每行单词。
```

```bash
wlist=$(strings "$1" | tr A-Z a-z | tr '[:space:]' Z | \
tr -cs ' ' | tr -s '\173-\377' Z | tr Z ' \
')
```

```bash
# 使用多次 'tr' 命令对 'strings' 命令的输出进行翻译。
# 'tr A-Z a-z' 将转换为小写。
# 'tr '[:space:]' Z' 将空白转换为 Z。
# 'tr '[:alpha:]' 将非字母字符转换为 Z，
# 并压缩多个连续的
# 'tr -s '\173-\377' Z' 将所有 'z' 之后的字符转换为 Z
# 并压缩多个连续的 Z，
# 'tr Z ' '' 移除掉之前的翻译 
# 未能处理的所有特殊字符。
# 最后，'tr Z ' ''' 将所有 Z 转换为空格，
# 这些空格在下面的循环中将被视为单词分隔符。

# 注意这种技术：将 'tr' 的输出回传给自身，

# 但在每一页都使用不同的参数。

for word in $wlist
# 重要：
# $wlist 不能加引号。
# "$wlist" 是不起作用的。
# 为什么？
```

```bash
do
    strlen=${#word} # 字符串长度。
    if [ "$strlen" -lt "$MINSTR" ]; # 跳过短字符串。
then
        continue
fi
    grep -Fw "$word" "$WORDFILE" # 仅匹配整个单词。
done
```

# 实用工具

## basename

## 12.5. 文件与归档命令

从文件名中删除路径信息，仅打印名称。构造`basename $0`可以脚本获取自身的名称，即它被调用的名称。这可以用于“用法”消息，例如，当调用脚本时缺少参数的情况下：

```bash
echo "Usage: basename $0 arg1 arg2 ... argn"
```

## dirname

从文件名中删除基名，仅打印路径信息。

`basename`和`dirname`可以作用于任意字符串。参数不需要指向一个存在的文件，甚至不需要是一个文件名（示例 A–7）。

## 示例 12–27. `basename` 和 `dirname`

```bash
#!/bin/bash
a=/home/bozo/daily-journal.txt
echo "Basename of /home/bozo/daily-journal.txt = $(basename $a)"
echo "Dirname of /home/bozo/daily-journal.txt = $(dirname $a)"
echo "My own home is $(basename ~)" # 仅用 . 同样有效
echo "The home of my home is $(dirname ~)" # 仅用 . 同样有效
exit 0
```

## sum, cksum, md5sum

这些是生成校验和的实用工具。`cksum`是根据文件内容数学计算出的数字，用于检查其完整性。脚本可能会出于安全目的引用校验和列表，例如检查关键系统文件的内容是否未被修改或损坏。`md5sum`命令在这些安全应用中是最合适的。

注意`cksum`还会显示目标文件的字节（字节字节）。

```bash
bash cksum /boot/mlinuz
1670054224 804083 /boot/mlinuz

bash md5sum /boot/mlinuz
0f43eceea8f09e0a2b5c1cdf333ba /boot/mlinuz
```

# 编码与加密

## uuencode

此工具将二进制文件编码为 ASCII 字符，使其适用于在邮件正文或新闻组帖子中传输。

## uudecode

该命令反转编码，将`uudencode`编码的文件解码回原始二进制文件。

## 示例 12–28. `uucoding` 编码的文件



```bash
#!/bin/bash
lines=35 # 为头文件留出 35 行（非常慷慨）。
for File in * # 测试当前工作目录下的所有文件...
do
  search1='head "$File" | grep begin | wc -w'
  search2='tail "$File" | grep end | wc -w'
  # Uucoded 文件在开头附近有一个 "begin"，
  # 在结尾附近有一个 "end"。
  if [ "$search1" -gt 0 ];
  then
    if [ "$search2" -gt 0 ];
    then
      echo decoding $File
      uudecode "$File"
    fi
  fi
done
# 注意运行此脚本会让它认为自己是一个 uudencode 文件，
# 因为包含了 "begin" 和 "end"。

# 练习：
# 修改此脚本以检查新闻组头。
exit 0
```

`fold -s` 命令可能有用（可能在管道中），用于从 `Usenet` 下载的长长度文本消息。

## mmencode, mmencode

`mmencode` 和 `mmencode` 命令处理多媒体邮件附件。虽然邮件用户代理（如 `pine` 或 `km`）通常会自动处理这些，但特定的实用工具允许从命令行或通过脚本手动操作附件。

## crypt

曾几何时是标准的 `UNIX` 文件加密工具。出于政治考虑的政府加密软件出口规定导致 `crypt` 在许多 `UNIX` 世界中消失，它在大多数 `Linux` 发行版中仍然缺失。

幸运的是，程序员们已经提出了许多不错的替代方案，其中包括作者自己的 `cruft`（参见示例 A–7）。

## 杂杂

## cp

将文件分成较小块的实用工具。通常用于分割大文件以便备份到软盘，或为电子邮件或上传做准备。

## install

特殊用途的复制，类似于 `cp`，但能够设置权限。

## more, less

分页器，一次显示一个屏幕的文件或流。

## 12.6. 通信命令

## host

查找有关 `Internet` 主机的信息。

## nslookup

执行 `DNS`（域名系统）查询。

## dig

类似于 `nslookup`，执行 `Internet` 查询。

## traceroute

追踪发送到远程主机的数据包路径。

## 远程主机访问

## sx, rx

`sx` 和 `rx` 命令集用于通过 `xmodem` 协议与远程主机之间传输文件。通常是通信包（如 `minicom`）的一部分。

## sz, rz

# 高级 Bash 脚本编写指南

`sz` 和 `rz` 命令集用于通过 `zmodem` 协议在远程主机之间传输文件。`Zmodem` 相比 `xmodem` 具有某些优势，例如更高的传输速率和支持中断传输的恢复。与 `sx` 和 `rx` 一样，这些命令通常是通信包的一部分。

# ftp

用于向远程主机上传/下载文件的工具和协议。`ftp` 会话可以在脚本中实现自动化（参见示例 17–7、示例 A–4 和示例 A–11）。

# cu

调用远程系统并作为简单终端进行连接。这是 `telnet` 的一种精简版本。

# uucp

`UNIX` 到 `UNIX` 拷贝（`UNIX to UNIX copy`）。这是一个用于在 `UNIX` 服务器之间传输文件的通信包。使用 shell 脚本处理 `uucp` 命令序列的有效方法。

自从互联网和电子邮件出现以来，`uucp` 似乎已经淡出舞台，但在没有互联网连接或不便连接互联网的情况下，它仍然存在并可以完美运行。

# telnet

用于连接远程主机的工具和协议。

![](img/1ce1edffaa36e4f698a85430e71c6d3b_189_0.png)

`telnet` 协议包含安全漏洞，因此应避免使用。

# rlogin

远程登录，在远程主机上启动会话。此命令存在安全问题，请改用 `ssh`。

# rsh

远程 shell（Remote shell），在远程主机上执行命令。此存在安全问题，请改用 `ssh`。

# rcp

远程拷贝（Remote copy），在两个不同的网络机器之间拷贝文件。在脚本中使用具有安全影响的 `rcp` 及类似工具可能并不明智。相反，请考虑使用 `ssh` 或 `expect` 脚本。

# ssh

安全 shell（Secure shell），登录远程主机并在上面执行命令。作为 `telnet`、`login`、`rcp`、`rsh` 的安全替代方案，它使用身份验证和加密。详情请参其 man 手。

## 12.6. 通信命令

# write

`write`

这是一个终端与终端之间通信的工具。它允许从你的终端（控制台或 `xterm`）向另一个用户的终端发送行。当然，可以使用 `msg` 命令来禁用对终端的写访问。

由于 `write` 是交互式的，它通常不会在脚本中使用。

# mail

`mail`

向用户发送电子邮件。

这个精简的命令行邮件客户端可以作为脚本中的命令工作。

## 示例 1–29. 一个给自己发邮件的脚本

```bash
#!/bin/sh
# self-mailer.sh: 自发邮件脚本
ARGCOUNT=1      # 需要收件人姓名。
E_WRONGARGS=6
if [ $# -ne $ARGCOUNT ];
then
  echo "Usage: `basename $0` addressee"
  exit $E_WRONGARGS
fi

cat $0 | mail -s "Script `basename $0` has mailed itself to you." "$1"

# 来自自发邮件脚本的问候。
# 一个调皮的人运行了这个脚本，
# 导致它将自己邮件给了你。
# 显然，有些人时间空闲得没正事做了。
#
exit 0
```

此工具会自动回复那些收件人正在休假且暂时不可用的电子邮件。它在网络上结合 `sendmail` 运行，不适用于拨号 `POP` 账户。

## 12.7. 终端控制命令

### 命令列表

### tput

初始化终端并/或从 `terminfo` 数据中获取信息。各种选项允许某些终端操作。`tput clear` 等同于下方的 `clear`。`tput reset` 等同于下方的 `reset`。

```bash
bash$ tput longterm
xterm terminal emulator (XFree86 4.0 Window System)
```

注意 `stty` 提供了更强大的命令集来控制终端。

### reset

重置终端参数并清除文本屏幕。与 `clear` 一样，光标和提示符会重新出现在终端的左上角。

### clear

`clear` 命令只需清除控制台或 `xterm` 中的文本屏幕。提示符和光标重新出现在屏幕或 `xterm` 窗口的左上角。此命令既可以在命令行中使用，也可以在脚本中使用。参见示例 10–24。

### script

此工具记录（保存到文件）控制台或 `xterm` 窗口命令行中的所有用户按键。这在实际上创建了一个会话记录。

## 12.8. 数学命令

### 命令列表

### factor

将整数分解为质因数。

```bash
bash$ factor 27417
27417: 3 13 19 37
```

### bc, dc

这些是灵活的任意精度计算工具。

`bc` 的语法模糊类似于 `C` 语言。

`dc` 使用 `RPN`（逆波兰表示法）。

在两者中，`bc` 在脚本中似乎更有用。它是一个非常良好的 `UNIX` 工具，可以在管道中使用。

`Bash` 无法处理浮点数计算，并且缺乏某些重要数学函数的运算符。幸运的是，`bc` 出现来救了救场。

这里有一个使用 `bc` 计算脚本变量的简单模板。它使用了命令替换。

```bash
variable=$(echo "OPTIONS; OPERATIONS" | bc)
```

## 高级 Bash 脚本指南

```bash
for i in [list] missing...
  do ==> 所以是对命令行参数进行操作
  case "$i" in
    0*) ibase=2; # 二进制
    0x*[a-f]*[A-F]*) ibase=16; # 十六进制
    ibase=8; # 八进制
    [1-9]*) ibase=10; # 十进制
    *)
      echo "illegal number $i - ignored"
      continue;
  esac

  # 前缀，将十六进制数字转换为大写 (bc 需要此)
  number=$(echo "$i" | sed -e 's:0x:[0-9a-fA-F]//' | tr '[a-f]' '[A-F]')
  # 使用 \ 作为分隔符，而不是 ""
  # 将数字转换为十进制
  dec=$(echo "ibase=$ibase;$number" | bc) # 计算器工具
  case "$dec" in
    [0-9]*) # 数字正常
      continue;
    *) ) # 错误：忽略
  esac

  # 在同一行打印所有转换结果。
  # == 'here document' 命令列表输入到 'bc'
  bc <<EOF
    obase=16; "hex": $dec
    obase=10; "dec": $dec
    obase=8; "oct": $dec
    obase=2; "bin": $dec
EOF | sed -e 's/"//g'
done

while [ $# -gt 0 ];
  do
    case "$1" in
      -\) shift; break;
      -h) Usage; ==> 帮助信息。
         Usage;
         break;
      *) ) # 第一个数字
    esac
    ==> 对非法输入进行错误检查将会很有用。
  shift
done

if [ $# -gt 0 ];
  then
    PrintBases "$@" # 从标准 读取
  else
    while read line
      do
        PrintBases $line
      done
  fi
```

一种使用嵌入在 `[command substitution]` 块中的 `[here document]` 来调用 `bc` 的替代方法。当脚本需要向 `bc` 传递一组选项和命令时，这种方法特别适用。

## 12.7. 终端控制命令

```bash
variable=`bc << LIMIT_STRING
options
statements
operations
LIMIT_STRING

...或者...

variable=$(bc << LIMIT_STRING
options
statements
operations
LIMIT_STRING
)
```

## 示例 12–32. 调用 bc 的另一种方法

```bash
#!/bin/bash
# 使用命令替换
# 结合 'here document' 来调用 'bc'

var1=$(bc << EOF
18.33 * 19.78
EOF)
echo $var1      # 362.56

# $(...) 记法同样有效。
v1=23.53
v2=17.881
v3=83.501
v4=171.63

var2=$(bc << EOF
scale = 4
a = ($v1 + $v2)
b = ($v3 + $v4)
a * b + 15.35
EOF)
echo $var2      # 593847.8452

var3=$(bc -1 << EOF
scale = 9
s ( 1.7 )
EOF)
# 返回 1.7 弧度的正弦值。
# "-1" 选项调用 'bc' 数学库。
echo $var3      # .991664810
```

## 现在，在函数中尝试一下...

```bash
hyp # 声明全局变量。
hypotenuse () # 计算直角角的斜边。
{
hyp=$(bc -1 << EOF
scale = 9
sqrt ( $1 * $1 + $2 * $2 )
EOF
# 遗憾的是，Bash 函数无法返回浮点数值。
)
hypotenuse 3.68 7.31
echo "hypotenuse = $hyp"      # 8.18403934

exit 0
```

在脚本中进行浮点数运算的另一种方法是在 shell 包装器中使用 `awk` 的内置数学函数。

## 示例 12–33. 计算三角形的斜边

```bash
#!/bin/bash
# hypotenuse.sh: 返回直角三角形的“斜边”。
# “直角边”平方的根

ARGS=2      # 脚本需要传递三角形的边。
E_BADARGS=65  # 参数数量错误。

if [ $# -ne "$ARGS" ]; then  # 测试脚本的参数数量。
then
    echo "Usage: $0 side_1 side_2"
    exit $E_BADARGS
fi

AWKSCRIPT='printf("%3.3f\n", sqrt($1 + $2*$2))' 
  # 传递给 awk 的参数
  # command(s)

echo -n "Hypotenuse of $1 and $2 = "
echo $1 $2 | awk "$AWKSCRIPT"

exit 0
```

## 12.9. 杂命令

### 命令列表

这些工具输出整数序列。每个整数之间正常的分隔符是...

# 高级 Bash 脚本指南

```bash
#!/bin/bash
# 在无需按回车键的情况下捕获按键。

keypresses=4                              # 要捕获的按键次数。

old_tty_setting=$(tty -g)                # 保存旧终端设置。
echo "Press $keypresses keys."         # 禁用规范模式。
stty -icanon -echo                       # 禁用本地回显。
keys=$(dd bs=1 count=$keypresses 2>/dev/null)    # 如果未指定 "if"，'dd' 使用标准输入。

stty "$old_tty_setting"               # 恢复旧终端设置。
echo "You pressed the $keys"

# 感谢 S.C. 的指明道路。
exit 0
```

`dd` 命令可以从数据流上读取原始数据。

```bash
echo -n | dd bs=1 seek=4 of=file conv=noctrunc
# "conv=noctrunc" 选项意味着输出文件不会被截断

# 感谢 S.C.
```

`dd` 命令可以在设备（如软磁盘和磁带驱动器）之间拷贝原始数据和磁盘镜像（示例 A-5）。常见的用途是创建启动软磁盘。

```bash
dd if=kernel-image of=/dev/fd0H1440
```

同样，`dd` 可以将软磁盘的所有内容（即使是带有“异类”系统的磁盘）作为镜像拷贝到原始硬盘。

```bash
dd if=/dev/fd0 of=...img
```

`dd` 的其他应用包括初始化临时交换文件（示例 29–2）和内存磁盘（示例 29–3）。它可以对整个硬盘分区进行低级复制，尽管这并不一定被推荐。

那些闲无正事事（打发时间）的人不断在思考 `dd` 的有趣应用。

# 示例 12–36. 安全删除文件

```bash
#!/bin/bash
# blotout.sh: 擦除文件的所有痕迹。
# 此脚本交替使用随机字节和零字节覆盖目标文件，
## 最后将其删除。
# 在此之后，即使是检查原始磁盘扇区
## 也无法发现原始文件数据。

PASSES=7
# 文件粉碎的次数。
BLOCKSIZE=1
# 与 /dev/urandom 进行 I/O 需要单位块大小，
# 否则你会得到奇怪的结果。
E_BADARGS=70
E_NOT_FOUND=71
E_CHANGED_MIND=72

if [ -z "$1" ]; then  # 未指定文件名。
then
    echo "Usage: basename $0 filename"
    exit $E_BADARGS
fi

file=1

if [ ! -e "$file" ]; 
then
    echo "File $file not found."
    exit $E_NOT_FOUND
fi

echo; echo -n "Are you absolutely sure you want to blot out $file? (y/n) "
read answer
case "$answer" in
[nN]) echo "Changed CHANGED_MIND, huh?"
    exit $E_CHANGED_MIND
    ;
*) echo "Blotting out $file.";
    break
esac

flength=$(ls -1 "$PASSES") | awk '{print $5}'  # 第 5 列是文件长度。

pass_count=1

echo

while [ "$pass_count" -le "$PASSES" ];
do
    echo "$pass_count"

    # 刷新缓冲区。
    sync

    dd if=/dev/urandom of=$file bs=$BLOCKSIZE count=$flength

    # 填充随机字节。

    sync

    # 再次刷新缓冲区。

    dd if=/dev/zero of=$file bs=$BLOCKSIZE count=$flength

    # 填充零。

    sync

    # 再次刷新缓冲区。

    let "$pass_count += 1"
done

rm -f $file  # 最后，删除乱码且粉碎的文件。

sync

# 最后刷新一次缓冲区。
```



```bash
echo "File $file blotted out and deleted."; echo

# # 这是一种相当安全、尽管效率低下且速度缓慢的
# 彻底“粉碎”文件的方法。'shred' 命令
## 是 GNU "fileutils" 软件包的一部分，执行相同的操作，
# 但效率更高。

# 文件无法通过正常方法被“恢复”或检索。
# 然而……
# 这种简单的方法可能*无法*经受法医分析。

## Tom Vier 的 "wipe" 文件删除包在文件粉碎方面
# 比这个简单的脚本做得要彻底得多。
# http://www.ibibio.org/pub/Linux/utils/file/wipe-2.0.0.tar.bz2

# 关于文件删除和安全主题的深入分析，
## 请参考 Peter Gutmann 的论文，
# "从磁性和固态存储器中安全删除数据"
# http://www.cs.auckland.ac.nz/~-pgut01/secure_del.html

exit 0
```

## 12.9. 杂项命令

`od` 八进制转储文件将文件转换为文本（八进制）或其他基进制。这对于查看或处理二进制数据文件或其他基进制非常有用。

### 高级 Bash 脚本指南

... 运行脚本的用户。

```bash
#!/bin/bash

# 一些命令。
sudo cp /root/secretfile /home/bozo/secret
# 更多命令。
```

文件 `/etc/sudoers` 存储允许调用 `sudo` 的用户名称。

`users`

显示所有登录的用户。这与 `who -q` 大致等效。

`ac`

显示从 `/var/log/wtmp` 中读取的用户的登录时间。这是 GNU 记账工具之一。

```bash
bash$ ac
total      68.08
```

`last`

列出从 `/var/log/wtmp` 读取的最后登录的用户。此命令也可以显示远程登录。

`groups`

列出当前用户及其所属的组。这与内部变量 `$GROUPS` 对应，但它提供的是组名，而不是组 ID。

```bash
bash$ groups
bozita cdwriter audio xgrp

bash$ echo $GROUPS
501
```

`newgrp`

在不注销登录的情况下更改用户的组 ID。这允许访问新组的文件。由于用户可能同时属于多个组，此命令用处不大。

## 终端

`tty`

显示当前用户终端的名称。注意，每个独立的 `xterm` 窗口都被视为不同的终端。

```bash
bash$ tty
/dev/pts/1
```

`stty`

第 13 章。系统和管理命令

显示并更改终端设置。这个复杂的命令在脚本中使用，可以控制终端行为和输出显示。请参阅 `info` 页面并仔细研究。

### 示例 13–1. 设置删除字符

```bash
#!/bin/bash
# erase.sh: 使用 "stty" 在读取输入时设置一个删除字符。

echo -n "What is your name? "
read name
# 尝试删除输入的字符。
# 将不起作用。
echo "Your name is $name".

stty erase '#'
# 将“井号标记” (\#) 设置为删除字符。
echo -n "What is your name? "
read name
# 使用 # 删除上一次输入的字符。
echo "Your name is $name".

exit 0
```

### 示例 13–2. 秘密密码：关闭终端回显

```bash
#!/bin/bash
echo -n "Enter password "
read passwd
echo "password is $passwd"
echo -n "If someone had been looking over your shoulder, "
echo "your password would have been compromised."

echo -e \n # “与列表”中的两个换行符。
stty -echo # 关闭屏幕回显。
echo -n "Enter password again "
read passwd
echo "password is $passwd"
echo

stty echo # 恢复屏幕回显。
exit 0
```

`stty` 的一种创意用法是检测用户按键（无需按下回车键）。

### 示例 13–3. 按键检测

```bash
#!/bin/bash
# keypress.sh: 检测用户按键（“热键盘”）
echo
old_tty_settings=$(stty -g) # 保存旧设置。
stty -icanon

| Keypress=$(head -c1) | # $=$(dd bs=1 count=1 2 > /dev/null) |
| | 在非 GNU 系统上 |

echo
echo "Key pressed was \"$Keypress\""
echo

stty $old_tty_settings # 恢复旧设置。

# 感谢 Stephane Chazelas。

exit 0
```

另见 [示例 9–3]。

## 终端与模式

通常，终端以规范模式（canonical mode）工作。当用户按下键时，产生的字符不会立即发送到在该终端运行的程序。终端本地的缓冲区存储按键。当用户按下 `ENTER` 键时，会将所有按键发送给程序。终端内部有一个基础编辑器。

```bash
bash$ tty -a
speed 9600; rows 36; columns 96; line = 0;
intr = ^C; quit = ^I; erase = ^H; kill = ^U; eof = ^E; deol = ^D; <undefined>; ed2 = <undefined>
start = ^Q; stop = ^S; susp = ^Z; rprnt = ^R; werase = ^W; lnext = ^V; flush = ^O

使用规范模式重新定义本地终端的特殊键。

```bash

bash$ cat file

a<ctl-W-I-ctl-Uhello world<ENTER>

bash$ cat file

hello world

bash$ wc -c

```

控制终端的进程只接收 13 个字符（包括换行符）。在非规范（raw）模式下，每个按键（包括特殊键 `ctrl-H`）都会立即将字符发送给控制进程。终端禁用了 `icanon` 和 `echo`。

`tset`

显示或初始化终端设置。这是 `stty` 的功能较少版本。

```bash

bash$ tset -r

Terminal type is xterm-86.

Kill = ^U).

Interrupt = ^C).

```

`setserial`

设置或显示串口端口。此命令必须由 `root` 用户运行，通常位于系统设置脚本：

```bash

# From /etc/pcmia/dev/$DEVICE | sed -e 's/\.*/'

setserial /dev/$DEVICE irq 0

```

`getty, agetty`

初始化终端使用 `getty` 或 `agetty`。对应的脚本是 `stty`。

`mesg`

启用或禁用当前用户终端的写入权限。禁用访问将防止网络上的其他用户写入终端。在编辑的文本文件中突然出现关于订披萨的消息可能会非常烦人。在多用户网络中，你可能需要禁用你的终端访问以避免干扰。

`wall`

这是 "write all" 的缩写，即向连接到每个终端的用户发送消息。它主要是系统管理员的工具，例如用于警告大家系统由于问题即将关闭（见示例 17–2）。

```bash

bash$ System down for maintenance in 5 minutes!

Broadcast message from bozo (pts/1) Sun Jun 8 13:53:27 2001...

System down for maintenance in 5 minutes!

```

如果通过 `mesg` 禁用了特定终端，`wall` 就无法对其发送消息。

`dmesg`

将所有系统启动消息列到 `stdout`。用于调试安装了哪些驱动程序。`dmesg` 的输出可以通过管道交给 `grep`。

`uname`

输出系统规格（操作系统、内核等）。`-a` 选项显示所有信息。

```bash

bash$ uname -a

Linux

```

`arch`

显示架构。

```bash

bash$ arch

686

```

`lastcomm`

提供以前登录的信息，存储在 `/var/log/wct` 中。这是 GNU 记账工具之一。

`last`

显示从 `/var/log/wtmp` 读取的用户的最后登录时间。这是 GNU 记账工具之一。

```bash

bash$ last

total      68.08

```

`lastlog`

显示从 `/var/log/wtmp` 读取的所有登录的用户。此命令也可以显示远程登录。

```bash

bash$ lastlog

username                               

bozo                               pts/1         Sun Jun 8 13:53:27 2001

```

`mesg`

启用或禁用当前用户终端的写入权限。禁用访问将防止网络上的其他用户写入终端。

`lsof`

列出打开的文件。此命令输出所有打开文件的详细表格，并提供所有者、大小以及关联进程的信息。当然，`lsof` 可以交给 `grep`。

| COMMAND | PID | FD | TYPE | SIZE | NAME |
|---|---|---|---|---|---|
| init | 1 | root | REG | 30748 | 30303 /sbin/init |
| init | 1 | root | REG | 73120 | 8069 /lib/ld-2.3.so |
| init | 1 | root | REG | 93168 | 8075 /lib/libc-2.3.so |
| cardmgr | 213 | root | REG | 36956 | 30357 /sbin/cardmgr |

`strace`

用于跟踪系统调用和信号的诊断和调试。最简单的方法是 `strace COMMAND`。

```bash

bash strace df

execve("/bin/df", ["/* 45 vars */]) = 0

uname("sys="Linux", node="bozo.localdomain", ...)) = 0x804f5e4

brk(0)

```

`free`

以表格形式显示内存和缓存使用。此命令的输出适用于 `grep`、`awk` 解析。`procinfo` 命令显示 `free` 显示的所有信息以及更多。

| total | used | free | shared | buffers | cached |
|---|---|---|---|---|---|
| Mem: | 30504 | 28624 | 1880 | 15820 | 1608 | 16176 |
| -/+ buffers/cache: | 68540 | 10640 | 19864 | | |
| Swap: | 3128 | 65412 | | | |

要显示未使用的内存：

```bash

bash free grep Mem | awk '{ print $4 }'

1880

```

`procinfo`

从 `/proc` 文件系统提取并列出信息和统计。这提供了一个非常详细的列表。

`lsdev`

列出设备，即已安装的硬件。

### 高级 Bash 脚本指南

| 设备 | DMA | IRQ | I/O 端口 |
| --- | --- | --- | --- |
| cascade | 4 | | |
| dma | | | 0080-008f |
| dmal | | | 0000-001f |
| dma2 | | | 00c0-00df |
| fpu | | | 00f0-00ff |
| ide0 | 14 | | 01f0-01f7 03f6-03f6 |

递归地显示磁盘文件使用情况。除非有指定，否则默认为当前工作目录。

```bash

bash du -ach

1.0k /wi.sh

1.0k /tst.sh

1.0k /random.file

6.0k

6.0k total

```

以表格格式显示文件系统使用情况。

| 文件系统 | 1k-块 | 已用 | 可用 使用率 | 挂载点 |
| --- | --- | --- | --- | --- |
| /dev/hda5 | 273262 | 92607 | 166547 | 36% | / |
| /dev/hda8 | 222525 | 123951 | 87085 | 59% | /home |
| /dev/hda7 | 1408796 | 1075744 | 261488 | 80% | /usr |

对给文件（设备或设备文件）或一组文件提供详细的统计信息。

```bash

bash stat test.cru

File: "test.cru"

Size: 49970 Allocated Blocks: 100 Filetype: Regular File

Mode: (0664/-rw-rw--) Uid: (501/bozo) Gid: (501/bozo)

Device: 3,8 Inode: 18185 Links: 1

Access: Sat Jun 2 16:40:24 2001

Modify: Sat Jun 2 16:40:24 2001

Change: Sat Jun 2 16:40:24 2001

```

如果目标文件不存在，`stat` 会返回错误消息。

```bash

bash stat nonexistent-file

nonexistent-file: No such file or directory

```

显示虚拟内存统计信息。

```bash

bash vmstat

procs memory swap io system cpu

r b w swpd free buff cache si so bo in cs us sy id

```

第 13 章。系统与管理命令

### 高级 Bash 脚本指南

显示当前的网络统计和信息，例如路由表和活动连接。此实用程序访问 `/proc/net`（第 28 章）。请参见示例 28–2。

`netstat -r` 等同于 `route`。

显示系统运行的时间以及相关的统计数据。

```bash

bash uptime

10:28pm up 1:57, 3 users, load average: 0.17, 0.34, 0.27

```

列出系统的主机名。此命令在 `/etc/rc.d` 设置脚本中（`/etc/rc.d/rc.sysinit` 或类似文件）设置主机名。它等同于 `uname -n`，是内部变量 `HOSTNAME` 的对应项。

```bash

bash hostname

localhost.localdomain

bash echo $HOSTNAME

localhost.localdomain

```

输出主机的 32 位十六进制标识符。

```bash

bash hostid

7f0100

```

该命令据称为特定系统获取“唯一的”序列号。某些产品注册程序使用此数字来标记特定的用户许可。遗憾的是，`hostid` 仅以十六进制返回网络地址，且字节对发生了转置。

典型的非网络化 Linux 机器的网络地址可以在 `/etc/hosts` 中找到。

```bash

$ cat /etc/hosts             localhost.localdomain localhost

127.0.0.1

```

转置 127.0.0.1 的字节时，我们得到 0.127.1.0.，这在十六进制中翻译为 007f0100，与上述 `hostid` 返回的结果完全相同。具有此相同 `hostid` 的 Linux 机器仅存几百万。

第 13 章。系统与管理命令

### 调用 sar–脚本指南

`sar`（系统活动报告）提供了系统统计的详详细概述。此命令于某些商用 UNIX 系统，但不是 Linux 发行版的一部分。它包含在 Sebastian Goddard 编写的 `sysstat` 包中。

```bash

$ sar

Linux 2.4.7-10 (localhost.localdomain)   12/31/2001

10:30:01 AM    CPU     %user    %nice    %system  %idle

10:40:00 AM    all     1.39    0.00     0.77    97.84

10:50:00 AM    all     76.83   0.00     1.45    21.72

11:00:00 AM    all     1.32    0.00     0.69    97.99

11:10:00 AM    all     1.17    0.00     0.30    98.53

11:20:00 AM    all     1.51    0.00     0.30    99.19

06:30:00 PM    all     100.00  0.00    100.01   0.09

Average:               1.39    0.00     0.66    97.95

```

## 系统日志

`logger`

将用户生成的消息添加到系统日志（`/var/log/messages`）。调用 `logger` 不需要 `root` 权限。

```bash

logger Experiencing instability in network connection at 23:10, 05/21.

# No, do a 'tail /var/log/messages'.
```



在脚本中嵌入`logger`可以向`/var/log/messages`写入调试信息。

```bash
logger Experiencing instability in network connection at 23:10, 05/21.
# No, do a 'tail /var/log/messages'.
```

# 高级 Bash 脚本指南

模式 (1)，在多用户模式 (2 或 3) 下，在 X Windows (5) 下或重启时 (6)。此命令访问`/var/run/utmp`文件。

`halt`, `shutdown`, `reboot`

用于关闭系统的命令，通常在关机之前执行。

# 网络

## `ifconfig`

网络接口配置和调优工具。它最常用于启动时设置接口，或在重启时关闭接口。

```bash
# 摘自 /etc/rc.d/init.d/network 代码片段
# 检查网络是否已启动。
$ [ $(NETWORKING) = "no" ] && exit 0
[ -x /sbin/ifconfig ] || exit 0
for i in $Interfaces; do
  if ifconfig $i 2>/dev/null | grep -q "UP" >/dev/null 2>&1; then
    action "Shutting down interface $i: /sbin/ifconfig"
    # grep 的 GNU 特有 "-q" 选项意味着“静默”，即不产生输出。
    # 因此，将输出重定向到 /dev/null 并不是绝对必要的。
  fi
done
```

```bash
echo "Currently active devices:"
echo /sbin/ifconfig | grep '[a-z]*' | awk '{print $1}'
# 以下方法同样有效。
echo $(sbin/ifconfig) | awk '/[a-z]*/ { print $1 }'
echo $(sbin/ifconfig) | sed -e 's/.*//'
# 感谢 S.C. 的额外注释。
```

另见[示例 3-5](#)。

# `route`

显示或修改内核路由表信息。

| `bash$ route` | 网关 | Genmask | Flags | MSS | Wtt | Inace |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| pm3-67.bosozisip | | 255.255.255.255 | UH | 40 | 0 | eth0 |
| 127.0.0.0 | | 255.0.0.0 | U | 40 | 0 | lo |
| default | | pm3-67.bosozisip | 0.0.0.0 | | 40 | 0 | eth0 |

# `chkconfig`

检查网络配置。此命令列出并管理`/etc/rc.d`中启动时启动的网络服务。

13. 系统和管理命令

`chkconfig`原本是从`IRIX`移植到`Red Hat Linux`的，某些`Linux`发行版可能不是核心安装的一部分。

| `bash$ chkconfig --list` | 1:off | 2:off | 3:on | 4:on | 5:on | 6:off |
| `atd` | 0:off | 1:off | 2:off | 3:off | 4:off | 5:off | 6:off |
| `rwhod` | 0:off | 1:off | 2:off | 3:off | 4:off | 5:off | 6:off |

## `tcpdump`

网络数据包“嗅探器”。该工具通过转储符合特定标准的数据包头，来分析和排查网络流量。

转储主机`bozoville`和`caduceus`之间的包流量：

```bash
bash$ tcpdump ip host bozoville and caduceus
```

当然，`tcpdump`的输出可以使用之前讨论过的某些文本处理工具进行解析。

# 文件系统

## `mount`

挂载文件系统，通常在外部设备上，如软盘或`CD-ROM`。文件`/etc/fstab`提供了可用文件系统、分区和设备的列表，包括可能自动或手动挂载的选项。`/etc/mtab`文件显示当前已挂载的文件系统和分区（包括虚拟分区，如`/proc`）。

`mount -a`挂载`/etc/fstab`中列出的所有文件系统和分区，但带有`auto`选项的除外。在启动时，`/etc/rc.d`中的启动脚本（`rcsysinit`或类似脚本）会调用此命令以完成所有挂载。

```bash
mount -t iso9660 /dev/cdrom /mnt/cdrom
# 挂载 CD-ROM
/mnt/cdrom
# 快捷方式，如果 /mnt/cdrom 已在 /etc/fstab 中
```

这个多功能命令可以在块设备上创建一个普通条，该文件将表现像文件系统一样。`mount`配合回环设备对该文件进行组装。其应用之一是在将`ISO9660`镜像刻录到`CDR`之前，对其进行挂载和检查。[40]

# 示例 13–5。检查 CD 镜像

```bash
# 作为 root 用户...
# 准备挂载点，如果尚不存在。
mdir -r -t iso9660 -o loop cd-image.iso /mnt/cdtest # 挂载镜像
# -o loop "loop" 选项等于 "losetup /dev/loop0"
cd /mnt/cdtest # 现在检查镜像。
```

第 13 章 系统和管理命令

```bash
ls -alR               # 列出该目录树中的文件。
                      # 以此类推。
```

卸载当前挂载的文件系统。在物理移除之前挂载的软盘或`CD-ROM`驱动器之前，必须先卸载设备，否则可能会发生文件系统损坏。

```bash
umount /mnt/cdrom
# 现在你可以可以操作了。
```

## 高级 Bash 脚本指南

更改`ROOT`目录。通常命令是从`$PATH`中获取的，相对于`/`（即默认根目录）。此命令会将根目录更改为另一个（同时也会更改工作目录）。这对于安全目的非常有用，例如当管理员希望限制用户（如使用`telnet`）访问文件系统的安全部分时；它有时通过将用户限制在“`chroot`监狱”中来实现限制。请注意，在执行`chroot`之后，系统二进制文件的执行路径将不再有效。

`chroot /opt`会创建对`/usr/bin`的引用并转换为`/opt/usr/bin`。同样，`chroot /aaa/bbb /bin/ls`将限制未来的`ls`实例以`/aaa/bbb`为基础目录（这是通常的情况）。在用户的`~/.bashrc`中设置`alias xx='chroot /aaa/bbb'`可以有效限制其运行命令`xx`时可以操作的文件系统部分。

`chroot`命令还用于从空软磁盘运行（`chroot`到`/dev/fd0`），或在从系统崩溃中恢复时作为`l`的选项。其他人使用从不同的文件系统进行安装（一个`rmp`选项）或从`CD-ROM`运行只读文件系统。仅以`root`身份调用，并谨慎使用。

![](img/1ce1edffaa36e4f698a85430e71c6d3b_221_0.png)

可能需要将系统文件复制到`chrooted`目录，在其中无法再依赖标准的`$PATH`。

此实用程序是`procmail`软件包（`www.procmail.org`）的一部分。它会创建一个锁文件。

锁文件用于此类应用程序，例如保护系统邮件文件夹不被多个用户同时修改、指示调制解调器正在访问，以及显示`Netscape`实例正在使用其缓存。脚本通过检查进程创建的锁文件是否存在来检查该进程是否正在运行。请注意，如果脚本尝试创建一个已存在的锁文件，脚本可能会挂起。

通常，应用程序在`/var/lock`目录中创建并检查锁文件。脚本可以通过类似内容来测试锁文件是否存在。

```bash
appname=xyzip
# Application "xyzip" 创建了锁文件 "/var/lock/xyzip.lock"
if [ -e "/var/lock/$appname.lock" ]; then
```

创建块或字符设备文件（在系统上安装新硬件时可能是必要的）。

自动删除在指定时间内未被访问的文件。通常由`crond`调用以删除过期的日志文件。

## `MAKEDEV`

用于创建设备文件的实用程序。必须以`root`身份运行，并在`/dev`目录下执行。

```bash
root# ./MAKEDEV
```

这是`mknod`的一种高级版本。

## 备份

`dump`, `restore`

`dump`命令是一个精细文件系统备份工具，通常用于较大的安装和网络环境。[42]。它读取原始分区并以二进制格式写入备份文件。要备份的文件可以使用多种存储媒体，包括磁盘和磁带驱动器。`restore`命令恢复用`dump`创建的备份。

## `fdformat`

在软磁盘上执行低级格式化。

## 系统资源

### `ulimit`

设置系统资源的上限。通常带有`-f`选项调用，该选项设置文件大小限制（`ulimit -f 1000`将文件限制为最大`1MB`）。`-t`选项限制核心转储大小（`ulimit -c 0`消除核心文件）。通常，`ulimit`的值设置在`/etc/profile`和或`~/.bash_profile`中（见第 27 章）。

### `umask`

用户文件创建掩码。限制特定用户的默认文件属性。该用户创建的所有文件都使用由`umask`指定的属性。（传递给`umask`的八进制值定义了禁用的文件权限）。当然，`umask 002`确保新文件的权限最多为`755`。通常做法是在`/etc/profile`和`~/.bash_profile`中设置`umask`值（见第 27 章）。

### `rdev`

获取或更改根设备、交换空间或视频模式。`rdev`的功能已被`lilo`取代，但`rdev`仍用于设置内存磁盘。这是另一个危险命令。

## 模块

### `lsmod`

列出已安装的内核模块。

| 模块 | 大小 | 使用者 |
|---|---|---|
| autofs | 9456 | 2 (autoclean) |
| opli3 | 11376 | 0 |
| serial_cs | 5456 | 0 (unused) |
| sb | 34752 | 0 [sb] |
| uart401 | 6384 | 0 [opli3 sb uart401] |
| sound | 58368 | 0 [sound] |
| soundlow | 464 | 0 [sb, sound] |
| soundcore | 2800 | 2 [serial_cs] |
| ds | 6448 | 0 |
| i28365 | 22928 | 2 |
| pcmia_core | 45984 | 0 [serial_cs ds i28365] |

`insmod`

强制安装内核模块。必须以`root`身份调用。

`rmmod`

强制卸载内核模块。必须以`root`身份调用。

`modprobe`

模块加载器，通常在启动脚本中自动调用。

`depmod`

创建模块依赖文件，通常从启动脚本调用。

## 杂项

`env`

在设置或更改某些环境变量的情况下运行程序或`shell`（而不更改整体系统环境）。`[varname=xxx]`允许在脚本运行期间更改环境变量名称。在未指定选项的情况下，此命令会列出所有环境变量。

> 在`Bash`和其他`Bourne`衍生版本中，可以在单个命令的环境中设置变量。

```bash
var1=value var2=value2 commandXXX
# $var1 和 $var2 仅在 'commandXXX' 的环境中设置
```

> 脚本的第一行（"`sha-bang`"行）在`shell`或解释器路径未知时可以使用`env`。

```bash
#!/usr/bin/env perl
print "This Perl script will..."
```

# 第 14 章. 命令替换

命令替换重新赋值一个命令 [44] 甚至多个命令的输出；它字面上将命令输出插入到另一个上下文中。

命令替换的经典形式使用反引号（`...`）。反引号（`backticks`）内的命令会生成命令行文本。

```bash
script_name=$(basename $0)
echo "The name of this script is $script_name."
```

命令的输出可以作为另一个命令，用于设置变量，甚至用于在循环中生成参数。

```bash
rm `cat filename` # "filename" 要删除的文件列表。
# S. C. 指出了 "arg too long" 错误结果。
# 更好的方法是
# xargs rm < filename
# (处理了 "filename" 以 "-" 开头的情况)
```

```bash
textfile_listing=$(ls *.txt)
# 当前目录下所有 *.txt 文件的文件名。
echo "$textfile_listing"
```

```bash
textfile_listing=$(*.txt) # 命令替换的另一种形式。
echo "$textfile_listing"
# 结果相同
```

```bash
# 将文件列表放入单个字符串的一个可能问题
# 是可能会引入换行符。
```

```bash
# 将文件列表赋值给参数更安全的方法是使用数组。
shopt -s nullglob # 如果没有匹配项，filename 扩展为空。
textfile_listing=( *.txt)
```

```bash
# 感谢 S.C.
```

命令替换可能会导致单词拆分（`word splitting`）。

```bash
COMMAND "echo a" # 2 个参数: a 和 b
COMMAND "echo a b" # 1 个参数: "a b"
COMMAND `echo` # 无参数
COMMAND `echo*` # 一个空参数
```

```bash
# 感谢 S.C.
```

在没有单词拆分的情况下，命令替换可以移除尾部的换行符。

```bash
# cd "$pwd" # 这应该始终有效。
# 然而...
```

# 高级 Bash 脚本指南

```bash
mkdir 'dir with trailing newline'
cd 'dir with trailing newline'
cd "$pwd" # 错误消息：
# bash: cd /tmp/file with trailing newline: No such file or directory
cd "$PWD" # 正常工作
```

```bash
old_tty_setting=$($stty) # 保存旧终端设置。
echo "Hit a key " # 为终端禁用*规范（canonical）*模式。
stty -icanon -echo # 同时，禁用*本地（local）*回显。
key=$(dd bs=1 count=1 2>/dev/null) # 使用 'dd' 获取按键。
stty $old_tty_setting # 恢复旧设置。
echo "You hit ${key}" # ${(variable)} =变量中的字符数
# 按除 RETURN 外的任何键，输出是 "You hit 1 key."
# 按 RETURN，输出是 "You hit 0 key."
# 换行符进入了命令替换。
```

感谢`S.C.`。

使用`echo`输出带有命令替换的未引号变量会从重新赋值的命令（`$s`）输出中移除尾部字符。这可能会导致令人意外的惊喜。

```bash
dir_listing=`ls -l`
echo $dir_listing # 未引号
# 期望得到一个排序良好的目录列表。
# 然而，你得到：
# total 3 -rw-rw-r-- 1 bozo 30 May 13 13:17 1.txt -rw-rw-r-- 1 bozo 51 May 15 20:57 t2.sh -rwxr-xr-x 1 bozo 21 Mar 5 21:23 wi.sh
```

```bash
echo "$dir_listing" # 带引号
# -rw-rw-r-- 1 bozo 30 May 13 13:17 1.txt
# -rw-rw-r-- 1 bozo 51 May 15 20:57 t2.sh
# -rwxr-xr-x 1 bozo 21 Mar 5 21:23 wi.sh
```

```bash
# 换行符消失了。
```

命令替换使用重定向或`cat`命令将文件内容赋值给变量。

```bash
variable1=$(cat file) # 将 "variable1" 设置为 "file" 的内容
variable2=$(cat file2) # 将 "variable2" 设置为 "file2" 的内容
```

```bash
# 注意，你的变量可能包含空格，
# 甚至包含（可怕的）控制字符。
```

# 第 14 章. 命令替换

# 高级 Bash 脚本指南

```bash
# 系统文件片段，/etc/rc.d/rc.sysinit
#+ (在 Red Hat Linux 安装上)
if [ -f /fsckoptions ]; then
    fsckoptions=$(cat /fsckoptions)
...
if [ -e /proc/ide/$disk[$device]/media ]; then
    hdmedia=$(cat /proc/ide/$disk[$device]/media)
...
```



```
if [ ! -n uname -r | grep "-*" ]; then

    ktag=cat /proc/version"

...

if [ $usb = "1" ]; then

    sleep 5

    mouseoutput=cat /proc/bus/devices 2>/dev/null|grep -E "^I.*Cls=03.Prot=02"

    kbdoutput=cat /proc/bus/usb/devices 2>/dev/null|grep -E "^I.*Cls=03.Prot=01"

...
```

不要将变量赋值给长文本，除非你有非常好的理由。不要将变量赋值给二进制文件，即使是玩笑。

### 示例 14–1. 愚蠢技巧

```bash
#!/bin/bash

# stupid-tricks.sh: 不要在家里尝试这个。

dangerous_variable=cat /boot/vmlinuz # 压缩的 Linux 内核本身。

echo "string-tricks" $dangerous_variable
```

# 高级 Bash 脚本指南

```
ERRORFILE-script.errors

bad_command1 2>$ERRORFILE      # 错误消息发送到 $ERRORFILE。

bad_command2 2>>$ERRORFILE # 错误消息追加到 $ERRORFILE。

bad_command3                # 错误消息输出到 stderr，

+#不会出现在 $ERRORFILE。

# 这些重定向命令在每行之后会自动“重置”。

==================================================================================
```

```
2>&1

# 将 stderr 重定向到 stdout。

# 错误消息将发送到标准输出相同的地方
```

```
i>j

# 将文件描述符 i 重定向到 j。

# i 指向的文件的所有输出都发送 j 指向的文件。
```

```
>j

# 默认将文件描述符 1 (stdout) 重定向到 j。

# 所有 stdout 都发送 j 指向的文件。
```

```
0<

# 从文件接受输入。

# 是 ">" 的配套命令，通常与它结合使用。

# grep search-word <filename
```

```
[j]<filename

# 以读写模式打开文件 "filename"，并将文件描述符 "j" 分配给它。

# 如果 "filename" 不存在，则创建。

# 如果未指定文件描述符 "j"，默认为 fd 0, stdin。

# 此方法的应用是在文件的指定位置写入。

echo 1234567890 > File # 将字符串写入 "File"。

exec 3<4 File # 打开 "File" 并为其分配 fd 3。

read -n 4 <3 # 仅读取 4 个字符。

echo -n . >&3 # 在那处写入一个小数点。

exec 3->4 # 关闭 fd 3。

cat File == 1234.67890

# 天哪，随机访问。
```

```
|# 管道 (Pipe)。

# 通用进程和命令链工具。

# 与 ">" ，但效果更通用。

# 用于将命令、脚本、文件和程序链在一起。

cat .txt | sort | uniq result-file

# 所有 .txt 文件的输出并删除重复行

# 最后将结果保存到 "result-file"
```

单行命令行中可以组合多个输入和输出重定向/或管道。

```
command <input-file >output-file

command1|command2|command3 >output-file
```

# 第 16 章. I/O 重定向

参见示例 12–23 和 示例 A–13。

多个输出流可以重定向到一个文件。

```
ls -yz >> command.log 2>&1

# 将 'ls' 的非法选项 'yz' 的结果捕捉到文件 'command.log'

# 因为 stderr 重定向到了文件，任何错误信息也会在那里。
```

## 关闭文件描述符

`n<&-`

关闭输入文件描述符 `n`。

`0<&-, <&-`

# 关闭 stdin。

`n>&-`

关闭输出文件描述符 `n`。

`1>&-, >&-`

# 关闭 stdout。

子进程会继承打开的文件描述符。这就是管道的工作原理。为了防止 fd 被继承，请关闭它。

```
# 仅将 stderr 重定向到管道

exec 3>&1                               # 保存 stdout 的当前“值”。

ls -l 2>&1 >3 3<&- | grep bad 3>&-  # 为 'grep' 关闭 fd 3（但不关闭 'ls'）。

----                                     

exec 3>&                               # 现在在脚本剩余部分关闭它。
```

# 感谢，S.C.

有关 I/O 重定向的详细介绍见附录 D。

## 16.1. 使用 exec

`exec <filename>` 将 stdin 重定向到文件。从该点开始，所有的 stdin 都来自文件，而不是其正常来源（通常是键盘输入）。这提供了一种通过 `sed` 或 `awk` 按行读取文件的方法。

### 示例 16–1. 使用 exec 重定向 stdin

```bash
#!/bin/bash

exec 6>&0               # 将 stdin 保存到文件描述符 6。

exec 6<data-file      # stdin 被 "data-file" 替换

read a1               # 读取 "data-file" 的第一行

read a2               # 读取 "data-file" 的第二行

echo "从文件读取后续行。"

echo $a1

echo $a2

echo "--------------------"

exec 0<&6 6&- # 从 fd 6 恢复 stdin，并关闭 fd 6 以供其他进程使用。
```

## 16.2. 重定向代码块

代码块如 `while`、`until` 和 `for` 循环，甚至 `if/then` 块也可以包含 stdin 的重定向（见示例 16–7）。在代码块末尾使用 `<` 运算符实现了这一点。

### 示例 16–2. 重定向 while 循环

```bash
#!/bin/bash

if [ -z "$1" ]

then

  Filename=names.data   # 未指定文件名时的默认值。

else

  Filename=${1:-names.data} # 替换上述测试

fi

count=0

while [ "$name" != "" ] # 为什么变量 $name 要加引号？

do

  read name                # 从重定向的 stdin ($Filename)

  echo $name

  let "count" += 1

done <"$Filename" # 重定向 stdin 到文件。

# 在旧的 shell 语言中，重定向循环会作为子 shell 运行。

因此，$count 会返回 0，它是在循环外初始化的。# 尽可能避免启动子 shell，这样这个脚本（例如 for 循环）就能正确运行。
```

### 示例 16–3. while 循环的变体

```bash
#!/bin/bash

# 这是前述脚本的变体。

# Steven 在循环作为子 shell 运行时建议这样做，因此循环内部的变量不会保留值。

if [ -z "$1" ]

then

  Filename=names.data      # 未指定文件名时的默认值。

else

  Filename=$1

fi

exec 3>&      # 保存 stdin 到文件描述符 3。

exec 0<"$Filename" # 标准输入。

count=0

while [ "$name" != "" ]

do

  read name                # 从文件读取

  echo $name

  let "count" += 1

done <"$Filename" # 循环从文件读取。

exec 0<&      # 恢复旧 stdin。

exec 3>&      # 关闭临时 fd 3。
```

### 示例 16–4. 重定向 until 循环

```bash
#!/bin/bash

# 与示例相同，但使用了 "until" 循环。

if [ -z "$1" ]

then

  Filename=names.data      # 未指定文件名时的默认值。

else

  Filename=$1

fi

while [ "$name" != "" ]

until [ "$name" = "" ]

do

  read name

  echo $name

done "$Filename"        # 重定向 stdin 到文件
```
与之前示例中的 "while" 循环结果相同。

### 示例 16–5. 重定向 for 循环

```bash
#!/bin/bash

if [ -z "$1" ]

then

  Filename=names.data      # 未指定文件名时的默认值。

else

  Filename=$1

fi

line_count=$(wc < "$Filename" | awk '{ print $1 }') # 文件的行数。虽然非常复杂且拙劣，但表明在 "for" 循环内部重定向 stdin 是可能的……如果你足够聪明。更简洁的方法是 `line_count=$(wc < "$Filename")`。

for name in $(seq $line_count)

# 

# # 回想一下 "seq" 是数字序列。比 "while" 循环复杂 --

do

  read name

  echo $name

  if [ "$name" = "" ]

    # 这里需要这些这些性工作。

    break

  fi

  done <"$Filename"        # 重定向 stdin 到文件

exit
```
我们可以修改上一个示例也重定向循环的输出。

### 示例 16-6. 重定向 for 循环（stdin 和 stdout 都重定向）

```bash
#!/bin/bash

if [ -z "$1" ]

then

  Filename=names.data      # 未指定文件名时的默认值。

else

  Filename=$1

fi

SaveFile=$Filename.new  # 保存结果的文件名。

FinalName=Jonah           # 用于终止 "read" 的名称。

line_count=$(wc $Filename | awk '{ print $1 }') # 文件的行数。

for name in $(seq $line_count)

do

  echo "$name"

  if [ "$name" = "$FinalName" ]

  then

    break

  fi

done < "$Filename" > "$Savefile"

# 重定向 stdin 到文件 $Filename，并保存到备份文件。

exit
```

### 示例 16-7. 重定向 if/then 测试

```bash
#!/bin/bash

if [ -z "$1" ]

then

  Filename=names.data      # 未指定文件名时的默认值。

else

  Filename=$1

fi

TRUE=1

if [ "$TRUE" ] # true 和 if : 也可以工作。

then

  read name

  echo $name

fi <"$Filename"
```
# 只读取文件的第一行。
# "if/then" 测试在不嵌入循环的情况下没有迭代方法。

exit

## 示例 16-8. 上述示例的数据文件 "names.data"

```
Aristotle
Belisarius
Capablanca
Euler
Goethe
Hamurabi
Jonah
Laplace
Maroczy
Furcell
Schmidt
Semmelweiss
Smith
Turing
Venn
Wilson
Znosko-Borowski
```

# 这是一个数据文件
#+ "redir2.sh", "redir3.sh", "redir4.sh", "redir4a.sh", "redir5.sh".

重定向代码块的标准输出（stdout）具有将其输出保存到文件的效果。参见 [示例 4–2]。

[在此文档 (Here documents)] 是重定向代码块的一种特殊情况。

## 16.3. 应用

巧妙地使用 I/O 重定向可以对命令输出片段进行解析和拼接 ([示例 11–4]）。这允许生成报告和日志文件。

## 示例 16–9. 记录事件

```bash
#!/bin/bash

# logevants.sh, 由 Stephanie Chazelas 

将事件记录到文件中。

# 必须以 root 身份运行（为了获得 /var/log 的写入权限）。

ROOT_UID=0          # UID 为 0 的用户具有 root 权限。

E_NOTROOT=67       # 非 root 退出错误。

if [ "$UID" -ne "$ROOT_UID" ];

then

    echo "必须以 root 运行此脚本。"

    exit $E_NOTROOT

fi

FD_DEBUG1=3

FD_DEBUG2=4

FD_DEBUG3=5

# 取消下面两行中的一个来激活脚本。

# LOG_EVENTS=1

# LOG_VARS=1

log() # 将运行时间和日期写入日志文件。

{
  echo "$(date)  $*&7  # 这将日期追加到文件中。
  # 见下文。
}

case $LOG_LEVEL in
1) exec $3&2 4> /dev/null 5 >/dev/null;
2) exec $3&2 5 >/dev/null;
3) exec $3&2 4>& 5>&2;
*) exec $3 >/dev/null 4> /dev/null 5 >/dev/null;
esac

FD_LOGARS=6

if [[ $LOG_VARS ]]
then exec 6 >/var/log/vars.log
else exec 6 >/dev/null
# 隐藏输出。
fi

FD_LOGEVENTS=7

if [[ $LOG_EVENTS ]]
then
# ... (省略重复逻辑)
```

## 17. 在此文档 (Here Documents)

在此文档使用 I/O 重定向的一种特殊形式，将命令脚本传递给交互式程序，例如 `telnet` 或 `ex`。通常，该脚本由一组由限制字符串分隔的命令列表组成。特殊符号 `<<` 位于限制字符串之前。这具有将文件输出重定向到程序的效果，类似于 `interactive-program < command-file`，其中 `command-file` 包含：

```
command #1

command #2

...
```

“在此文档”的写法如下：

```bash
#!/bin/bash

interactive-program <<LimitString

command #1

command #2

...

LimitString
```

选择一个特殊的限制字符串，使其不会在命令列表中任何地方出现并引起混淆。注意，在此文档有时与非交互式工具和命令结合良好。

### 示例 17–1. dummyfile：创建一个 2 行的伪文件

```bash
#!/bin/bash

# 非交互式使用 'vi' 编辑文件。

# 模拟 'sed'。

E_BADARGS=65

if [ -z "$1" ]

then

  echo "用法: $0 <filename>"

  exit $E_BADARGS

fi

TARGETFILE=$1

# 在文件中插入 2 行并保存。

#------在此文档开始------

vi $TARGETFILE <<LimitString

i

这是示例文件的第 1 行。

这是示例文件的第 2 行。

ZZ

LimitString

#------在此文档结束------
```

```bash
# 注意上面的 ^$ 是一个字面转义符

# 通过 Control-V <Esc> 输入。

# Bram Moolenaar 指出这在 'vim' 中可能不起作用，

# 因为存在终端交互问题。

exit 0
```

上述内容完全可以使用 `ex` 同样有效地实现。

# 高级 Bash 脚本指南

```
Filename=$basename $1

# 从文件名中剥离出路径名。

Server="metalab.unc.edu"

Directory="incoming/Linux"

# 这些内容不需要硬编码在脚本中，

# 而是可以使用命令行参数。

Password="your.e.mail.address" # 根据需要修改上方内容。

ftp -n $Server <<End-Of-Session

# -n 选项禁用自动登录

user anonymous "$Password"

binary

cd $Directory

# 在每个文件传输后响一下“铃”
```



```
put "$Filename.lsm"
put "$Filename.tar.gz"
bye
End-Of-Session
exit 0
```

可以使用 `:` 作为占位命令来接收来自“在此处文档”（here document）的输出。这在实际上创建了一个“匿名”在此处文档。

# 示例 17–8. “匿名”在此处文档

```bash
#!/bin/bash

# <<TESTVARIABLES
$(HOSTNAME)?($USER)?($MAIL)?)\ # 如果其中一个变量未设置，则打印错误消息。
TESTVARIABLES

exit 0
```



在此处文档创建临时文件，但这些文件在打开后会被删除，并且任何其他进程都可以访问。

```bash
bash -c 'lsof -a p $$ -d0' << EOF
lsof | 1213 bozo | 0 | REG | 3,5 | 03386 /tmp/t1213-0-sh (deleted)
EOF
```

某些工具在此处文档内部无法工作。

对于那些对于“在此处文档”来说过于复杂的任务，请考虑使用`expect`脚本语言，它专门为向交互式程序提供输入而设计。

第 17 章 在此处文档 | 240

# 第 18 章 休息时间

这个奇怪的小间歇让读者有机会放松，也许还能大笑一下。

爱的 Linux 用户，你好！你正在阅读的内容将带给你好运。只需将此文档的副本通过电子邮件发送给 10 个朋友。在复制之前，向此信底部提供的列表中的第一个人发送一个 100 行的 Bash 脚本。删除他们的名字，并将你的名字添加到列表末尾。

不要打破链条！请在 48 小时内完成复制。布鲁克林的 Wilfred P. 未能发送出他的十份副本，第二天早上醒来发现自己的工作变成了“COBOL 程序员”。纽波特纽斯的 Howard L. 发送了他的十份副本，在一个月内他获得了足够的硬件来构建一个拥有 100 个节点的 Beowulf 集群，用于运行 `xbill`。芝加哥的 Amelia V. 对这封信笑了并打破了链条。不久后，她的终端起火了，现在她每天都在为 MS Windows 编写文档。

不要打破链条！今天就寄出你的十份副本吧！

感谢 'NIX' 的“幸运饼”，包含了一些修改和许多深表歉意。

# 第 4 部分 高级主题

- 19. 正则表达式
    - 19.1. 正则表达式简述
    - 19.2. 通配符 (Globbing)
- 20. 子壳
- 21. 限制性 Shell
- 22. 进程替换
- 23. 函数
    - 23.1. 复杂函数与函数复杂度
    - 23.2. 本地变量
- 24. 别名 (Aliases)
- 25. 列表构造
- 26. 数组
- 27. 文件
- 28. Idev/proc
    - 28.1. `/dev`
    - 28.2. `/proc`
- 29. 关于零与空
- 30. 调试
- 31. 选项
- 32. 陷阱 (Gotchas)
- 33. 风格写作
    - 33.1 非官方 Shell 脚本样式表
- 34. 杂项
    - 34.1 交互式与非交互式 Shell 及脚本
    - 34.2. Shell Wrapper
    - 34.3. 测试与比较：替代方案
    - 34.4. 优化
    - 34.5. 各类技巧
    - 34.6. 奇异之处
    - 34.7. 可移植性问题
    - 34.8 Windows 下的 Shell 脚本
- 35. Bash 版本 2

# 第 19 章 正则表达式

为了充分利用 Shell 脚本的力量，你需要精通正则表达式。脚本中常用的某些命令和工具，如`expr`、`sed`和`awk`，都会解释并使用正则表达式（RE）。

## 19.1. 正则表达式简述

表达式是一个字符字符串。那些具有超出字面意义的解释含义的字符被称为元字符。引号符号可能表示人的言语，也可能表示字符的含义。UNIX 使用时具有特殊特性。正则表达式（RE）的主要用途是文本搜索和字符串处理。

- 星号 `*` 匹配字符字符串或前置字符的任意次数，包括零次。
- 点号 `.` 匹配除换行符外的任何字符。
- 加号 `+` 匹配至少一个任意字符（包括空格）。
- 插入符号 `^` 匹配行首，但有时取决于上下文，它会否定字符集的含义。
- 正则表达式末尾的美元符号 `$` 匹配行尾。
- 方括号 `[...]` 包含在一个单一 RE 中匹配的字符集。
- `"xyz"` 匹配字符 x、y 或 z。
- `[c-n]` 匹配 c 到 n 范围内的任意字符。
- `[B-y]` 匹配 B 到 y 范围内的任意字符。

# 高级 Bash 脚本指南

```bash
```



## 高级 Bash 脚本指南

```bash
ls -l

total 2

-rw-rw-r-- 1 bozo bozo 0 Aug 6 18:42 a.1
-rw-rw-r-- 1 bozo bozo 0 Aug 6 18:42 b.1
-rw-rw-r-- 1 bozo bozo 0 Aug 6 18:42 c.1
-rw-rw-r-- 1 bozo bozo 466 6 17:48 t2.sh
-rw-rw-r-- 1 bozo bozo 758 Jul 30 09:02 test1.txt

bash ls -l t?.sh

-rw-rw-r-- 1 bozo bozo 466 6 17:48 t2.sh

bash ls -l [ab]*

-rw-rw-r-- 1 bozo bozo 0 Aug 6 18:42 a.1
-rw-rw-r-- 1 bozo bozo 0 Aug 6 18:42 b.1

bash ls -l [a-c]*

-rw-rw-r-- 1 bozo bozo 0 Aug 6 18:42 a.1
-rw-rw-r-- 1 bozo bozo 0 Aug 6 18:42 b.1
-rw-rw-r-- 1 bozo bozo 0 Aug 6 18:42 c.1

bash ls -l -1 [b*,c*,*est]

-rw-rw-r-- 1 bozo bozo 0 Aug 6 18:42 b.1
-rw-rw-r-- 1 bozo bozo 466 6 17:48 t2.sh
-rw-rw-r-- 1 bozo bozo 758 Jul 30 09:02 test1.txt

bash ls -l 11 bozo bozo 0 Aug 6 18:42 b.1

-rw-rw-r-- 1 bozo bozo 0 Aug 6 18:42 c.1
-rw-rw-r-- 1 bozo bozo 758 Jul 30 09:02 test1.txt

bash echo *

a.1 b.1 c.1 t2.sh test1.txt

bash echo t*

t2.sh test1.txt
```

即使是 `echo` 命令也会在文件名中执行通配符扩展。

请参见示例 10–4。

# 第 20 章 子 shell

运行 shell 脚本会启动命令处理器的另一个实例。正如你的命令在命令行提示符处被解释一样，脚本也会类似的批量处理文件中的命令列表。每个运行的 shell 脚本实际上都是父 shell 的子进程，即那个在控制台或 x 窗口中为你提供提示符的 shell。

shell 脚本也可以启动子进程。这些子 shell 让 shell 执行并行处理，同时执行多个子任务。

## 括号中的命令列表

```bash
( command1; command2; command3; )
```

> 嵌入在括号之间的命令列表将作为子 shell 运行。

子 shell 中的变量在子 shell 代码块外部是不可见的。它们对于父进程（即启动子 shell 的 shell）不可访问。这些实际上是局部变量。

# 示例 20–1. 子 shell 中的变量作用范围

```bash
#!/bin/bash

# subshell.sh

echo
outer_variable=Outer

{
inner_variable=Inner
echo From subshell, "inner_variable" = $inner_variable
echo From subshell, "outer" = $outer_variable
}

echo

if [ -z "$inner_variable" ]
then
echo "inner_variable undefined in main body of shell"
else
echo "inner_variable defined in main body of shell"
fi

echo "From main body of shell, "inner_variable" = $inner_variable

# $inner_variable 将显示为未初始化，因为
# 定义在子 shell 中的变量是“局部变量”。

echo
exit 0
```

# 高级 Bash 脚本指南

请参见示例 32–1。

在子 shell 中进行的目录更改不会传递到父 shell。

# 示例 20–2. 列出用户配置文件

```bash
#!/bin/bash

# allprofs.sh: 输出所有用户配置文件

# 此脚本由 Heiner Steven 编写，由文档作者修改。

FILE=.bashrc # 包含用户配置文件的文件，
# 原脚本中是 ".profile"。

for home in awk -F: '$(print $6)' /etc/passwd
do
    [ -d "$home"] || continue # 如果没有家目录，跳到下一个。
    [ -r "$home"] || continue # 如果不可读，跳到下一个。

    cd $home; [ -e $FILE ] && $FILE
done

# 当脚本终止时，不需要 'cd' 回原始目录，
# 因为 'cd $home' 在子 shell 中执行的。

exit 0
```

可以使用子 shell 为一组命令设置一个“专用环境”。

```bash
COMMAND1
COMMAND2
COMMAND3

(
IFS=-/bin
PATH=-C
unset TERMINFO
set -C
shift
COMMAND4
COMMAND5
exit 3 # 只退出子 shell。
```

父 shell 未受到影响，环境得以保留。

```bash
COMMAND6
COMMAND7
```

这种方法的一个应用是测试一个变量是否已定义。

```bash
if [ -z "$variable" ] 2>/dev/null
then
echo "Variable is set."
fi
```

# 也可以写成

```bash
[[ -z "$variable" ]] && echo "Variable is set."

# 或者

[[ "$variable" != "" ]]

# 或者

[[ ${ ${variable+x} -eq 0 ]]
```

另一个应用是检查锁文件：

```bash
if set -C; > lock_file 2>/dev/null
then
echo "Another user is already running that script."
exit 1
fi
```

# 第 20 章 子 shell

感谢，S.C.。进程可以在不同的子 shell 中并行执行。这允许将复杂任务拆分为多个组件。

# 示例 20–3. 在子 shell 中运行并行进程

```bash
(cat list1 list2 list3 > list23) &
```



(cat list4 list5 list6 > list456) & # 同时合并两组列表

## 高级 Bash 脚本指南

### `or`

```
exec 3>&1

tar cf /dev/fd/4 dir 4>&1 3>&3 | bzip2 -c file.tar.bz2 3&-

exec 3>&
```

### 感谢 S.C.

本文的一位读者发送了以下关于进程替换的有趣示例。

### 取自 SuSE 发行版的脚本片段：

```
while read des what mask iface; do

# Some commands...

done < (route -n)
```

```
# 为了测试它，让它执行一些操作。

while read des what mask iface; do

echo $des $what $mask $iface

done < (route -n)
```

### 输出：
```
# 内内核 IP 路由表
# Destination Gateway Genmask Flags Metric Ref Use Iface
# 127.0.0.0 0.0.0.0 255.0.0.0 U 0 0 0 lo
```

正如 S.C. 指出的，更容易理解的等效写法是：

```
route -n |

while read des what mask iface; do # 变量来自管道的输出。

echo $des $what $mask $iface

done # 输出与上面相同。
```

## 第 22 章 进程替换

## 第 23 章 函数

像“真正的”编程语言一样，Bash 也拥有函数，尽管实现方式有些有限。函数是一个子程序，是一个实现一组操作的代码块，是一个执行指定任务的“黑盒”。在任何有重复代码的地方，当一个任务以只有细微差异重复出现时，可以考虑使用函数。

```
function function_name {

  command...

}
```

或者

```
function_name() {

  command...

}
```

这第二种形式会让 C 语言程序员感到高兴（并且可移植性更好）。

与 C 语言一样，函数的左括号可以可选地出现在第二行。

```
function_name() {

  command...

}
```

函数的调用只需通过调用它们的名称即可触发。

### 示例 23–1. 简单函数

```
#!/bin/bash

funky {

  echo "This is a funky function."

  echo "Now exiting funky function."

} # 函数定义必须在调用之前。

# 现在，调用函数。

funky

exit 0
```

函数的定义必须在第一次调用它之前。没有像 C 语言那样的“声明”函数的方法。

```
# f1

# 将产生一个错误信息，因为函数 "f1" 尚未定义。

# 然而...

f1 ()

{

    echo "Calling function \"F2\" from within function \"F1.\."

    f2

}

f2 ()

{

    echo "Function \"f2.\."

}

f1 # 直到这一步，函数 \"f2\" 还没有真正被调用

    # 尽管它在定义之前就被引用了

    # 这是被允许的。
```

### 感谢 S.C.

甚至可以在函数内部嵌套另一个函数，尽管这并不好用。

```
f1 ()

{

    f2 () # 嵌套

{

        echo "Function \"f2\", inside \"f1.\."

    }

}

f2 # 产生错误信息

f1 # 什么也不做，因为调用 \"f1" 不会自动调用 \"f2"

f2 # 现在，调用 \"f2" 可以的

    # 因为它的定义通过调用 \"f1" 变得可见了。
```

### 感谢 S.C.

函数声明可以出现在意想不到的地方，甚至在原本应该放置命令的地方。

```
ls -1 | foo() ( echo "foo"; ) # 允许，但没用。

if [ $USER = bozo ]

then

    bozo_greet () # 嵌入在 if/then 结构中。

    {

        echo "Hello, Bozo."

bozo_greet # 只对 Bozo 有效，其他用户会报错。
```

```
这种做法在某些上下文中可能是用的。

NO_EXIT=1 # 将启用下面的定义。
```

## 第 23 章 函数

```
[[ $NO_EXIT -eq 1 ]] && exit () { true; } # “与”列表中的定义

# 如果 $NO_EXIT 为 1，则声明 "exit()"。

# 通过将其别命名为 "true" 来禁用内置命令 "exit"。

exit # 调用 "exit()" 函数，而不是内置的 "exit"。

# 感谢 S.C.
```

### 23.1. 复杂函数

函数可以处理传递给它们的参数并返回退出状态。函数通过位置引用参数（就像位置参数一样），即 `$1`, `$2` 等。

```
function_name $arg1 $arg2
```

#### 示例 23–2. 接收参数

```
#!/bin/bash

func2 () {

  if [ -z "$1" ]; # 检查参数 #1 是否为空。

  then

    echo "-1 is zero length."

  else

    echo "-1 is not."

  fi

  if [ "$2" ];

    echo "-2 is not."

  fi

  return 0

}

echo "Nothing passed."

func2 # 无参数调用

echo "Zero-length parameter passed."

func2 "" # 空长度参数调用

echo "Null parameter passed."

func2 "$initialized_param" # 未初始化的参数调用

echo "One parameter passed."

func2 first # 有一个参数调用

echo "Two parameters passed."

func2 first # 有两个参数调用
```

`shift` 命令处理传递给函数的参数（见示例 3–6）。与其他语言不同，shell 脚本通常向函数传递值。变量名（实际上是指针）如果作为参数传递，将被视为字面量且无法解引用。函数字面上解释它们的参数。

#### 退出与返回

函数返回一个被称为退出状态的值。`return` 语句可以显式指定退出状态（成功为 0，失败为非 0）。此退出状态可以在脚本中通过引用 `$?` 使用。`return` 终止函数。`return` 命令可选地接收一个整数参数，作为调用脚本的“退出状态”。该状态赋值给变量 `$?`。

##### 示例 23–3. 两个数的最大值

```
#!/bin/bash

# max.sh 两个整数的最大值。

max2() # 返回两个数中较大的一个

  if [ -z "$2" ]; # 注意：参数必须少于 2。

  then

    return $E_PARAM_ERR

  fi

if [ "$1" -eq "$2" ]

then

  return $EQUAL

else

  if [ "$1" -gt "$2" ]

  then

    return $1

  else

  return $2

  fi

fi

max2 3 4

return_val=$?

if [ "$return_val" -eq $E_PARAM_ERR ]

then

  echo "Need to pass two parameters to the function."

elif [ "$return_val" -eq $EQUAL ]

then

  echo "The two numbers are equal."

else

  echo "The larger of the two numbers is $return_val."

fi

exit 0

# 练习（简单）：

# 将此转换为交互式脚本，

# 即脚本请求输入（两个数字）。
```

为了让函数返回字符串或数组，请使用专门的变量。

```
count_lines_in_etc_passwd() {
  [[ -r /etc/passwd ]] && REPLY=$(echo $(wc -l < /etc/passwd))
  # 如果 /etc/passwd 可读，设置 REPLY 为行数。
  # 返回值和状态信息。
}

count_lines_in_etc_passwd
then
  echo "There are $REPLY lines in /etc/passwd"
else
  echo "Cannot count lines in /etc/passwd"
fi
```

### 感谢 S.C.

#### 示例 23–4. 将数字转换为罗马数字

```
#!/bin/bash

# 阿拉伯数字到罗马数字转换
# 范围：0 - 200
# 它很粗糙，但有效。
```

扩展范围以及其他脚本改进留作作为练习。

##### 使用方法：`roman` `number-to-convert`

```
LIMIT=200
E_ARG_ERR=65
E_OUT_OF_RANGE=66

if [ -z "$1" ];
then
    echo "Usage: basename $0 number-to-convert"
    exit $E_ARG_ERR
fi

num=$1
if [ "$num" -gt $LIMIT ]
then
    echo "Out of range!"
    exit $E_OUT_OF_RANGE
fi

to_roman () {
    number=$1
    factor=$2
    rchar=3
    let "remainder" = number - factor
    while [ "$remainder" -ge 0 ];
    do
        echo -n $rchar
        let "number" = "factor"
        let "remainder" = number - factor
    done
    return $number
    # 练习：
    # -----
    # 解释这个函数是如何工作的。
    # 提示：连续减除法。
}
n
to_roman $num 100 C
num=$?
to_roman $num 90 LXXXX
num=$?
to_roman $num 50 L
num=$?
to_roman $num 40 XL
num=$?
to_roman $num 10 X
num=$?
to_roman $num 9 IX
num=$?
to_roman $num 5 V
num=$?
to_roman $num 4 IV
num=$?
to_roman $num 1 I

echo
```

## 进阶 Bash 脚本指南

```bash
exit 0
```

另请参见示例 10–27。

函数返回的最大正整数是 256。`return` 命令与退出状态（exit status）的概念紧密相关，而这一概念导致了这种特定的限制性。坦率地说，对于那些需要函数返回大整数值的情况，有多种变通方法。

### 23–5. 在函数中测试大返回值

```bash
#!/bin/bash
# return-test.sh

# 函数可以返回的最大正值是 256。

return_test ()      # 返回传递给它的任何值（作为退出状态）。
{
    return $1
}

return_test 27      # o.k.
echo $?               # 返回 27。

return_test 256     # 仍然 o.k.
echo $?               # 返回 256。

return_test 257     # 错误！
echo $?               # 返回 1（各种错误的返回代码）。

return_test -151896  # 然而，大的负数可以工作。
echo $?               # 返回 -151896。

exit 0
```

正如我们所见，函数可以返回一个大的负值。通过一些技巧，这同时也允许返回大的正整数。

实现此点的另一种方法是简单地将“返回值”赋值给全局变量。

```bash
Return_Val=      # 用于保存函数超范围返回值的全局变量。

alt_return_test ()
{
    fvar=$1
    Return_Val=$fvar
    return              # 返回 0（成功）。
}

alt_return_test 1   # 0
echo $?               
echo "return value = $Return_Val"  # 1
```

### 23.1. 复杂函数与函数复杂度

#### 进阶 Bash 脚本指南

```bash
alt_return_test 256
echo "return value = $Return_Val"    # 256

alt_return_test 257
echo "return value = $Return_Val"    # 257

alt_return_test 25701
echo "return value = $Return_Val"    # 25701
```

##### 示例 2-6. 比较两个大整数

```bash
#!/bin/bash
# 大整数的最大值
# max2.sh: 两个大整数的最大值

# 这是之前的 "max.sh" 示例，
# 经过修改允许比较大整数。

EQUAL=0                              # 两个参数都相等。
MAXRETVAL=256                      # 函数返回的最大正值。
E_PARAM_ERR=-99999                  # 参数错误。
E_NPARAM_ERR=-9999999              # “归一化”的参数错误。

max2()\                              # 返回两个数中较大的。
if [ -z "$2" ]
then
    return $E_PARAM_ERR
fi

if [ "$1" -eq "$2" ]
then
    return $EQUAL
else
    if [ "$1" -gt "$2" ]
then
    retval=$1
else
    retval=$2
fi

# 这是一个允许从此函数返回大整数的变通方法。
if [ "$retval" -gt "$MAXRETVAL" ]    # 如果超出范围，
then
    let retval=$(( 0 - $retval ))     # 调整为负值。
    # (( 0 - $VALUE )) 改变值的符号。
fi

# 幸运的是，允许大的“负”返回值。
#
    return $retval
}

max2 33001 33997
return_val=$?

#
if [ "$retval" -lt 0 ]              # 如果是“调整过的”负数，
then
    # then
```

### 23.1. 复杂函数与函数复杂度

#### 进阶 Bash 脚本指南

```bash
let "return_val = (( 0 - $return_val ))" # 归一化为正数。
fi # $return_val 的“绝对值”。

if [ "$return_val" -eq $E_PARAM_ERR ]; # 参数错误“标记”也会被改变。
then
echo "Error: 参数太少。"
elif [ "$return_val" -eq $EQUAL ];
then
echo "两个数字相等。"
else
echo "两个数字中较大的是 $return_val。"
fi

exit 0
```

另请参见示例 A–7。

**练习：** 使用我们刚刚学到的知识，扩展之前的罗马数字示例以接受任意大小的输入。

### 重定向

*重定向函数的标准输入*

函数本质上是一个代码块，这意味着它的标准输入可以重定向（如示例 4–1）。

#### **示例 23–7. 从用户名获取真实名**

```bash
#!/bin/bash

# 从用户名从 /etc/passwd 获取“真实名”。
ARGCOUNT=1  # 期望一个参数。
EWRONGARGS=65

file=/etc/passwd
pattern=$$

if [ $# -ne "$ARGCOUNT" ];
then
    echo "用法: `basename $0` USERNAME"
    exit $E_WRONGARGS
fi

file_excerpt () {
    # 扫描文件中的模式，打印行的相关部分。
    while read line; do # while line 并不一定需要 "[condition"
        echo "$line" | grep "$pattern" | awk -F":" '{print $5}' # 让 awk 使用 ":" 分隔符
    done < "$file" # 文件重定向到标准输入。
}

file_excerpt $pattern

# 是的，整个脚本可以简化
```

### 23.1. 复杂函数与函数复杂度

#### 进阶 Bash 脚本指南



# 第 23 章 函数 (Functions)

```bash
# grep PATTERN /etc/passwd | awk -F:"' '{ print $5 )
# or awk -F:/PATTERN/ (print $5 )
# or or awk -F:{$1 == "username" { print $5 } # 从用户名
# 然而，它可能没有那么有意义。

exit 0
```

另一种可能不那么混乱的重定向函数输入的方法是将标准输入重定向到函数内部嵌入的括号代码块。

```bash
# 代替：
Function ()
{
  ...
} < file

# 尝试这个：
Function ()
{
  ...
} < file

# 同样，
Function () # 这可以工作。
{
  ...
} <
```

## 23.1. 复杂函数与函数复杂度

## 进阶 Bash 脚本指南

## 23.2. 局部变量

什么让变量变为局部？

声明为局部的变量仅在它所在的块中可见。在调用函数之前，函数内部声明的所有变量在函数体外部都是不可见的。

## 进阶 Bash 脚本指南

```bash
func ()
{
  local_var=37      # 声明为局部。
  echo $local_var   # 在函数内部可见
}
func
echo $local_var       # 此处可见
```

### 23.2.1. 局部变量

局部变量使得递归可能，但这种做法通常涉及大量的开销且执行缓慢，因此通常不适合在脚本中使用。

#### 示例 23–9. 使用局部变量的递归

```bash
#!/bin/bash
factorial
--------
```

# 第 24 章 别名 (Aliases)

`Bash` 别名本质上只是键盘快捷键、缩写，是避免输入长命令序列的方法。例如，如果我们在 `~/.bashrc` 文件中包含 `alias im="ls -l | more"`，那么命令行中的每个 `im` 都会被自动替换为 `ls -l | more`。这在命令行中节省了大量时间，并避免了记忆复杂的命令和选项组合。设置 `alias rm="rm -i"`（交互模式）可能会避免很多麻烦，防止无意中丢失重要文件。

在脚本中，别名的通用性非常有限。如果别名能够承担一些 C 语言预处理器的功能（例如宏展开），那就太好了，但遗憾的是 `Bash` 不会在别名内部进行求值[55]。此外，脚本无法在“复合结构”（如 `if/then` 语句、循环和函数）内部展开别名。另一个限制是，别名不会进行递归展开。几乎在任何情况下，我们希望让别名执行的任何操作，都可以通过函数更好地实现。

#### 示例 24-1. 脚本中的别名

```bash
#!/bin/bash
# 在旧系统上可能需要用 #!/bin/bash2 调用。

set -s expand_aliases
# 必须设置此选项，否则脚本不会展开别名。

# 首先，来点有趣的。
alias Jesse_James=echo "*Alias Jesse\" was a 1952 comedy starring Bob Hope."
Jesse_James

echo; echo;

alias ll1="ls -l"
# 可以使用转义的 \" (单斜 \') 或双引号 (") 来定义别名。
echo "Trying aliased \"*\""
ll1 /usr/X11R6/mk* # 别名有效。

echo

directory=/usr/X11R6/bin/
prefix=* # 查看通配符是否引起问题。
echo "Variables \"directory\" + \"prefix\" = $directoryprefix"
echo

alias ll1="ls -l $directoryprefix"
echo "Trying listing \"*\"" in /usr/X11R6/bin starting with mk.
ll1 # 列出 /usr/X11R6/bin 中所有以 mk 开头的文件。
# 别名处理连接变量，包括通配符，可行。

TRUE=1

echo

if [ TRUE ]
then
  alias rr="ls -l"
  echo "Trying aliased \"rr\" if/then statement"
  rr /usr/X11R6/bin/mk* # 结果为错误！
  # 复合语句未展开别名
  echo "However, previously expanded alias still recognized"
  ll /usr/X11R6/bin/mk*
fi

echo

count=0
while [ $count -lt 3 ]
do
  alias rr="ls -l"
  echo "Trying aliased \"rr\" within \"while\" loop"
  rr /usr/X11R6/bin/mk* # 别名在这里也不会展开。
  ((count+=1))
done

echo;
alias xyz="$$1" # 尝试在别名中使用位置参数。
xyz # 如果你用文件名作为参数调用脚本。
# 这似乎有效，
# 尽管 Bash 文档建议它不应该有效。

exit 0
```

`unalias` 命令用于删除之前设置别名。

#### 示例 24–2. `unalias`：设置和取消别名

```bash
#!/bin/bash

set -s expand_aliases # 启用别名展开

alias ll='ls -al | more'
ll

echo

unalias ll # 取消别名。
ll
# 结果为错误，因为 'll' 不再被识别。

exit 0
./unalias.sh
```

```
total 6
drwx-xr-x 2 bozo 3072 Feb 6 14:04
drwxr-xr-x 40 bozo 2048 Feb 6 14:04 ..
-rwxr-xr-x 1 bozo 199 Feb 6 14:04 unalias.sh
```

```
./unalias.sh: ll: command not found
```

# 第 25 章 列表结构 (List Constructs)

“与”和“或”结构提供了连续处理命令的方法。

它们有效地替换了复杂的嵌套 `if/then` 或 `case` 语句。

## 链式命令

```bash
command-1 && command-2 && command-3 ... command-n
每个命令按顺序执行，前提是上一个命令的返回值为
（零）。当遇到第一个假（非零）返回值时，命令链终止（第一个返回假结果的命令是最后一个执行执行的命令）。
```

#### 示例 25–1. 使用“与列表”测试命令行参数

```bash
#!/bin/bash
# "and list"

if [ ! -z "$1" ] && echo "Argument $1 = $1" && [ ! -z "$2" ] && echo "Argument $2 = $2"
then
    echo "传递给脚本的至少有两个参数。"
    # 所有链式命令都返回真。
else
    echo "传递给脚本的参数少于 2 个。"
    # 至少有一个链式命令返回假。
fi
# 注意 "if [ -n $1 ]" 有效，但它所谓的等价写法
# "if [ -z $1 ]" 无效。然而，加上引号可以修复此。
# "if [ -n $1 ]" 有效。注意！
# 最好始终为变量加上引号。

# 使用“纯”的 if/then 语句实现相同的功能。

if [ ! -z "$1" ]
then
    echo "Argument $1 = $1"
fi

if [ ! -z "$2" ]
then
    echo "Argument $2 = $2"
else
    echo "传递给脚本的参数少于 2 个。"
fi

# 它比“与列表”长且不优雅。

exit 0
```

```bash
#!/bin/bash
ARGS=$#
if [ ! -z "$ARGS" ] # 表示了参数的数量。

BADARGS=6 # 如果传递的参数数量错误时的退出值
test $# -ne $ARGS && echo "Usage: $0 (arguments)" && exit $BADARGS
# 如果条件为真（传递的参数数量错误），
# 则执行行的剩余部分，脚本终止。

echo "传递给此脚本的参数数量正确。"

# 要检查退出值，在脚本结束后执行 "echo $?"。
```

```bash
file=$1 # 设置文件名

[ -f "$1" ] && echo "File $1 not found."
# 胆怯拒绝删除不存在的文件。
# 与列表（AND LIST），在文件不存在时提供错误信息。
# 注意 echo 消息通过转义符在第二行继续显示。

[ -f "$1" ] || (rm -f $1; echo "File $file deleted")
# 或列表（OR LIST），如果存在则删除。
# ( command1 ; command2 ) 实际上是与列表的变体。

# 注意上述逻辑反转。
# 与列表在为真时执行，或列表在为假时执行。

false && true || echo false    # false

# 与以下结果相同

( false && true ) || echo false    # false

# 但不是

false && ( true || echo false )      # (无输出)

# 注意语句的从左到右分组和评估，

# 因为逻辑运算符 "&&" 和 "||" 具有相同的优先级。

# 最好避免这种复杂性，除非你清楚自己在做什么。

# 感谢，S.C.
```

参见示例 A–7 以获取使用与/或列表测试变量的插图。

# 第 26 章 数组 (Arrays)

较新版本的 `Bash` 支持一维数组。数组元素可以使用 `variable[xx]` 符号进行初始化。或者，脚本也可以通过显式的 `declare -a variable` 语句引入整个数组。要解引用（查找）数组元素的内容，使用 `${variable[xx]}` 表示法。

#### 示例 26–1. 简单数组用法

```bash
#!/bin/bash

area[11]=23

area[13]=37

area[51]=UFOs

# 数组成员不需要是连续或相邻的。

# 数组的某些成员可以不初始化。

# 数组中的间隙是可以接受的。

echo -n "area[11]" = ""

echo ${area[11]}      # 需要（大括号）

echo -n "area[13]" = ""

echo ${area[13]}

echo "Contents of area[51] is ${area[51]}"

# 未初始化数组变量的内容为空。

echo -n "area[43]" = ""

echo ${area[43]}

echo "${area[43]} unassigned"

echo

# 将两个数组变量的和赋值给第三

area[5]=expr ${area[11]} + ${area[13]}

echo "area[5] = area[11] + area[13]"

echo -n "area[5]" = ""

echo ${area[5]}

area[6]=expr ${area[11]} + ${area[5]}

echo "area[6] = area[11] + area[5]*"

echo -n "area[6]" = ""

echo ${area[6]}

# 这失败了，因为不允许对字符串加整数。

echo; echo; echo

#------------------------------------------------------

# 另一个数组，“area2"

# 分配数组变量另一种方法...

# array_name=( XXX YYY ZZZ ... )

area2=( zero one two three four )

echo -n "area2[0] = "

echo ${area2[0]}

# 哦，从零开始索引（数组的第一个元素是 [0]，而不是 [1]）。

echo -n "area2[1] = "

echo ${area2[1]} # [1] 是数组的第二个元素。

----------------------------------------------------------------------

echo; echo; echo

# 另一个数组, "area3"

# 另一个赋值数组变量的数组...

# array_name=([xx]=XX [yy]=YYY ...)

area3=([17]=seventeen [24]=twenty-four)

echo -n "area3[17] = "

echo ${area3[17]}

echo -n "area3[24] = "

echo ${area3[24]}

exit 0
```

数组有特定的语法，即使是标准的 `Bash` 命令和运算符也针对数组的使用进行了特殊适配。

```bash
array=( zero one two three four )
echo ${array[0]}      # zero
echo ${array:0}       # 第一个元素的参数扩展。
echo ${array:1}       # one
# 第一个元素的参数扩展，从位置 1 开始（第二个字符）。

echo ${#array}          # 5
# 在数组上下文中表示元素的长度。Bash 内置命令的含义略有不同。例如，unset 会删除数组元素或整个数组。

# 示例 26-2. 数组的一些特殊属性

#!/bin/bash

declare -a colors
# 允许在不指定大小的情况下声明数组。

echo "输入你喜欢的颜色（用空格分隔）。"
read -a colors      # 输入至少 3 种颜色以演示下文。
# 'read' 命令的特殊选项，允许向数组元素赋值。

element_count=${#colors[@]}
# 提取数组元素数量的特殊语法。
element_count=${#colors[*]} 同样有效。
# 该变量允许在引号内进行单词拆分（提取由空格分隔的变量）。

index=0
while [ "$index" -lt "$element_count" ]; do
    echo ${colors[$index]}
    # 列出数组中的所有元素。
    let index=$((index + 1))
done
# 每个元素单独行列出。
# 如果不需要这样，请使用 echo -n "${colors[$index]}"

# 使用 "for" 循环来实现：
for i in "${colors[@]}"; do
    echo "$i"
done
# （感谢，C.）

# 再次列出数组中的所有元素，但使用更优雅的方法。
echo ${colors[@]}      ${colors[*]} 同样有效。

# "unset" 命令删除数组的元素或整个数组。
unset colors[1]      # 移除数组的第二个元素。
# 与 unset colors[1]= 效果相同。再次列出数组，元素将缺失。

unset colors
    # 删除整个数组。
# unset colors[*] 和 unset colors[@] 同样有效。
echo; echo -n "颜色已消失。"
echo ${colors[@]}      # 再次列出数组，现在为空。

exit 0
```

如前面的示例所示，如果 `${array_name[@]}` 或 `${array_name[*]}` 指的是数组的所有元素。要获取数组元素的计数，请使用 `${#array_name[@]}` 或 `${#array_name[*]}`。`${#array_name}` 是 `${array_name[0]}`（数组的第一个元素）的长度（字符数）。

#### 示例 26-3. 空数组和空元素

```bash
#!/bin/bash
# empty-array.sh

# 空数组不等同于包含空元素的数组。
```



## 高级 Bash 脚本指南

### 第 26 章 数组

**数组基础**

```bash
array0=( first second third )
array1=( ' ') # "array1" 有一个空元素
array2=() # 没有元素... "array2" 是空的。

echo "Elements in array0: ${array0[0]}"
echo "Elements in array1: ${array1[0]}"
echo "Elements in array2: ${array2[0]}"

echo "Length of first element in array0: ${array0[0]}"
echo "Length of first element in array1: ${array1[1]}"
echo "Length of first element in array2: ${array2[2]}"

echo "Number of elements in array0: ${array0[@]}" # 3
echo "Number of elements in array1: ${array1[*]}" # 1 (意外！)
echo "Number of elements in array2: ${array2[*]}" # 0

exit 0 # 感谢，C.
```

`$array_name[@]` 和 `$array_name[*]` 之间的关系类似于 `@@` 和 `$*` 之间。这种强大的数组表示法有很多用途。

**数组操作**

```bash
# 复制数组。
array2=("array1[@]}")
# 或者
array2="${array1[*]}"

# 向数组添加元素。
array=("${array[0]}) "new element"
# 或者
array[${#array[*]*}="new element"

# 感谢，C.
```

`array=element1 element2 ... elementN` 初始化操作，通过命令替换的帮助，使得将文本内容加载到数组中成为可能。

**示例 26-4. 冒泡排序**

```bash
#!/bin/bash

filename=sample_file

# cat sample_file
# 1 a b c
# 2 d e f g

declare -a array1

array1=$(cat "$filename" | tr '\n' ' ') # 将文件名的内容加载到 array1。
# 输出文件到标准输出。
# 将文件中的换行符更改为空格。

echo ${array1[@]} # 列出数组。
```

**示例 26-5. 质数筛**

```bash
# ... (逻辑继续)

initialize ()
{
# 初始化数组。

i=$LOWER_LIMIT
until [ "$i" -gt "$UPPER_LIMIT" ]
do
  Primes[i]=$PRIME
  let i += 1
done
  # 假设所有数组元素都是有罪的（质数）
  # 直到被证明无罪。
}

print_primes ()
{
# 打印 Primes[] 数组中标记为质数的元素。

i=$LOWER_LIMIT
until [ "$i" -gt "$UPPER_LIMIT" ]
do

  if [ "${Primes[i]}" -eq "$PRIME" ]
then
    printf "%8d" "$i"
    # 每个数字留出 8 个空格可以形成整齐的列。
  fi
done

let i += 1
}

sift ()
{
# 筛选掉非质数。

let i=$LOWER_LIMIT+1
# 我们知道 1 是质，所以从 2 开始。

until [ "$i" -gt "$UPPER_LIMIT" ]
do

  if [ "${Primes[i]}" -eq "$PRIME" ]
# 不要去处理已经筛选过的数字（已标记为非质数）。
then

    t=$i
    while [ "$t" -le "$UPPER_LIMIT" ]
do
      let t += $i
      Primes[t]=$NON_PRIME
      # 将所有倍数标记为非质数。
done
  fi
done
}

let "i += 1"
)

# 顺序调用函数。
initialize
sift
print_primes
# 这就是他们说的结构化编程。

echo

exit 0

#------------------------------------
# 下以下代码将不会执行。

# 这个由 Stephanie Chazelas 改进的筛法版本
# 执行速度较快。

# 必须带有命令行参数调用（质数范围）。
UPPER_LIMIT=$1    # 来自命令行。
let SPLIT=UPPER_LIMIT/2    # 到最大数字的一半。

Primes=(' $(seq $UPPER_LIMIT) )

i=1
until [[ ((i += 1) > SPLIT ]]; # 只需检查到一半。
do
  if [[ -n ${Primes[$i]} ]]];
  then
    t=$i
    until (( ((t += i) > UPPER_LIMIT ))
    do
      Primes[t]=
    done
  fi
done
echo ${Primes[*]}
exit 0
```

将此基于数组的质数生成器与不使用数组的替代方案进行比较。参见示例 A-14。

---

数组在某种程度上可以模拟 Bash 无原生支持的数据结构。

**示例 26–6. 模拟推入栈**

```bash
#!/bin/bash
# stack.sh: 推入栈模拟

# 类似于 CPU 栈，推入栈按顺序存储数据项
# 但按反序释放它们，即后进先出。

BP=100            # 栈数组的基指针。
                   # 从元素 100 开始。
SP=$BP           # 栈指针。
                   # 将其初始化为栈的“基底”（底部）。
Data=             # 栈位置的内容。
                   # 必须使用局部变量，
                   # 因为函数返回范围有限制。
declare -a stack

push() {
  if [ -z "$1" ]  # 将项目推入栈。
  then
    return
  fi

  let SP --= 1      # 增加栈指针。
  stack[$SP]=$1
  return
}

pop() {           # 从栈中弹出项目。
  Data=            # 清空数据项。
  if [ "$SP" -eq "$BP" ]  # 栈为空？
  then
    return
  fi
  # 这也防止了 SP 超过 100，
  # 防止栈溢出。
  Data=${stack[$SP]}
  let SP += 1       # 增加栈指针。
  return
}

status_report() {
  # 找出正在发生什么。
  echo "------------------------------------------------"
  echo "报告"
  echo "栈指针 = $SP"
  echo "刚刚从栈中弹出 \"$Data\"。"
  echo "------------------------------------------------"
  echo
}

# ==================================================
# 现在，来玩点点。
echo

# 看看是否能从空栈弹出任何东西。
pop
status_report

echo

push garbage
pop
status_report # 垃圾进，垃圾出。
value1=23; push $value1
value2=skidoo; push $value2
value3=FINAL; push $value3

pop # FINAL
status_report
pop # skidoo
status_report
pop # 23
status_report # 后进先出！

echo

# 注意栈指针如何每次 push 都会递减
# + 每次 pop 都会增加。

====================================================
```

**练习：**

- 1) 修改 `push()` 函数，允许在单次调用中向栈推入多个元素。
- 2) 修改 `pop()` 函数，允许在单次调用中从栈弹出多个元素。
- 3) 以此脚本为起点，编写一个基于栈的计算器。

对数组“脚本”进行精妙操作可能需要中间变量。对于涉及这些的项目，再次考虑更强大的语言，例如 `Perl` 或 `C`。

**示例 26–7. 复杂的数组应用：探索一个奇特的序列**

```bash
#!/bin/bash

# Hofstadter 著名的“Q-序列”:
# Q(1) = 1
# Q(2) = 1
# Q(n) = Q(n-1) + Q(n-2), 对于 n>2
# 这是一个“混沌”序列，具有奇异且不可预测的行为。
# 该序列的前 20 项为：
# 1 2 3 4 5 6 8 8 9 10 11 12

LIMIT=100 # 要计算的项数
LINEWIDTH=20 # 每行的项数

Q[1]=1 # 序列的第一项。
Q[2]=1 # 序列的第二项。

for ((n=3; n<LIMIT; n++))
do
  Q[n]=$(( Q[n-1] + Q[n-2] ))
  echo -n "${Q[n]} "
  if [ $((n % LINEWIDTH)) -eq 0 ]; # 格式化输出。
  then
    echo
  fi
done

# 迭代实现 Q-序列作为练习。
警告：递归实现此序列非常耗时。
```

`Bash` 仅支持一维数组，但通过小技巧允许模拟多维数组。

**示例 26–8. 模拟二维数组，然后倾斜它**

```bash
#!/bin/bash

# 模拟二维数组

# 二维数组按顺序存储。

Rows=5

Columns=5

declare -a alpha      # 无必要的声明。

load_alpha ()
{
    local rc=0
    local index
    local row=0
}while [ "$row" -lt "$Rows" ];
do
    # 按行输出
    # 列在变化
    local column=0
    while [ "$column" -lt "$Columns" ];
    do
        let index=$(row * Rows + column)
        echo -n "${alpha[$index]}"  # alpha[row][column]
        let "column += 1"
    done
    let "row += 1"
done

# 更简单的等价方法
# echo ${alpha[*]} | xargs -n $Columns

filter () {
    echo -n ""      # 过滤负数组索引。
    #               提供了倾斜。
}

if [[ "$1" -ge 0 && "$1" -lt "$Rows" && "$2" -ge 0 && "$2" -lt "$Columns" ]];
then
let index=$1 * Rows + "$2"
# 现在，打印旋转后的。
echo -n "${alpha[$index]}"  # alpha[row][column]
fi

rotate () # 将数组绕其左下角旋转。
local row
local column
for ((row = Rows; row > -Rows; row-- ))  # 反向遍历数组
  for ((column = 0; column < Columns; column++))
  do
    if [ "$row" -ge 0 ]
    then
      let t1=$column $row
      let t2=$column
    else
      let t1=$column
      let t2=$column + $row
    fi
    filter $t1 $t2  # 过滤掉负数组索引。
  done
  echo; echo
done

# 数组旋转灵感来自《哥德尔、埃舍尔、巴赫：永恒的金织》中的示例（第 143-146 页）。
#（参见参考文献）。

--------------------------------------

load_alpha      # 加载数组。

print_alpha     # 打印它。

rotate          # 逆时针旋转 45 度。

--------------------------------------

exit 0
```

二维数组本质上等同于一维数组，但具有额外的地址模式，可以通过“行”和“列”位置来引用和操作单个元素。

欲了解模拟二维数组的更详尽的示例，请参见示例 A–8。

### 第 27 章：文件

#### 启动文件

这些文件包含了作为用户 `shell` 运行的 `Bash` 以及在系统初始化后调用的所有 `Bash` 脚本可用的别名和环境变量。

| 文件路径 | 说明 |
| :--- | :--- |
| `/etc/profile` | 系统级默认设置，主要设置环境（所有 `Bourne` 类型的 `shell`，不包括 `Bash` [56]） |
| `/etc/bashrc` | `Bash` 的系统级函数和别名 |
| `$HOME/.bash_profile` | 用户特定的 `Bash` 环境变量默认设置，位于每个用户的家目录中（是 `/etc/profile` 的本地对应项） |
| `$HOME/.bashrc` | 用户特定的 `Bash` 初始化文件，位于每个用户的家目录中（是 `/etc/bashrc` 的本地对应项）。只有交互式 `shell` 和用户脚本会读取此文件。请参见附录 G 中的示例 `.bashrc` 文件。 |

#### 注销文件

| 文件路径 | 说明 |
| :--- | :--- |
| `$HOME/.bash_logout` | 用户特定的指令文件，位于每个用户的家目录中。当退出登录 (`Bash`) `shell` 时，将执行此文件中的命令。 |

### 第 28 章：/dev 和 /proc

`Linux` 或 `UNIX` 机器通常有两个特殊用途目录：`/dev` 和 `/proc`。

#### 28.1. /dev

`/dev` 目录包含了硬件中可能存在也可能不存在物理设备的条目。[57]。如简单的 `df` 命令所示，包含挂载文件系统的硬设备分区在 `/dev` 中有相应条目。

```bash
bash$ df
```

| Filesystem | 1k-blocks | Used | Available | Use% | Mounted on |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `/dev/sda` | 495876 | 222748 | 247527 | 48% | `/` |
| `/dev/hdb1` | 50755 | 3887 | 44248 | 9% | `/boot` |
| `/dev/hda8` | 367013 | 13262 | 334803 | 4% | `/home` |
| `/dev/hda5` | 171416 | 112624 | 503704 | 70% | `/usr` |

其中，`/dev` 目录还包含回环设备（loopback devices），例如 `/dev/loop0`。回环设备是一种技巧，允许普通文件像块设备一样被访问。[158] 这允许在一个大文件中挂载整个文件系统。请参见示例 13-6 和示例 13-5。

`/dev` 中的一些伪设备具有其他特殊用途，例如 `/dev/null`、`/dev/zero` 和 `/dev/urandom`。

#### 28.2. /proc

`/proc` 目录实际上是一个伪文件系统，`/proc` 目录中的文件镜像了运行中的系统和内核进程，并包含了关于它们的信息和统计数据。

```bash
bash$ cat /proc/devices

Character devices:

1 mem
2 pty
3 ttyp
4 tty
5 cua
7 vcs
10 misc
14 sound
29 fb
36 netlink
128 ptm
136 pts
162 raw
254 pcmcia

Block devices:

1 ramdisk
```

```bash
bash$ cat /proc/interrupts

CPU0
0: 84505 XT-PIC timer
1: 3375 XT-PIC keyboard
2: 0 XT-PIC cascade
5: 1 XT-PIC soundblaster
8: 1 XT-PIC rtc
12: 4231 XT-PIC PS/2 Mouse
14: 109373 XT-PIC ide0
NMI: 0
ERR: 0
```

```bash
bash$ cat /proc/partitions

major | #blocks | name | rio | rmerge | rest | ruse | wo | wmerge | wsect | using | run | aveq |
```




| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 3 | 0 | 300782 | `hda` | 472 | 22260 | 114520 | 942 | 3351 | 18703 | 50384 | 549710 | 0 | 111550 | 64430 |
| 3 | 1 | 52416 | `hdl` | 27 | 395 | 844 | 960 | 4 | 21 | 180 | 0 | 800 | 1140 |
| 3 | 2 | 1 | `hda` | 2 | 0 | 0 | 0 | 0 | 0 | |
| 3 | 4 | 165280 | `hda` | 10 | 0 | 20 | 210 | 0 | 0 | 0 | 210 | |
| ... |

```bash
bash$ cat /proc/loadavg
0.13 0.42 0.27 2/44 119
```

可以从 `/proc` 中的某些文件中提取数据。[59]

```bash
kernel_version=$( awk '{ print $3 }' < /proc/version )

CPU=$( awk '/model/ { print $4 }' < /proc/cpuinfo)

if [ $CPU == Pentium ]
then
    run_some_commands
else
    run_different_commands
fi
```

`/proc` 目录包含以异常命名的子目录。每一个对应一个运行中进程的 ID。这些子目录中包含了有关进程的有用信息。`stat` 文件保存运行统计，`cmdline` 文件包含了调用进程时的参数，而 `exe` 文件是指向进程完整路径的符号链接。还有一些这样的文件，但从脚本的角度来看这些是最有趣的。

## 第 28. `/dev` 和 `/proc`

### 示例 28–1. 与 PID 关联进程

```bash
#!/bin/bash
# pid-identifier.sh: 获取关联 PID 的路径

ARGNO=$# 脚本期望的参数数量。
E_WRONGARGS=65
E_BADPID=66
E_NOSUCHPROCESS=67
E_OPERMISSION=68
PROFILE=$

if [ $ARGNO -ne 1 ]; then
    echo "Usage: $0 PID" >&2 # 输出到标准错误
    exit $E_WRONGARGS
fi

pidno=$(ps ax | awk '{ print $1 }' | grep $1) # 在 "ps" 列表中查找 pid。
# 然后 grep 过滤掉脚本自身的进程。
if [ -z "$pidno" ];
then
    # 如果过滤后结果为空字符串，
    echo "No process running."
    # 进程对应给定的 PID。
    exit $E_NOSUCHPROCESS
fi

或者：
if ! kill -0 $1 /dev/null 2>&1; then # 测试是否向进程发送信号。
    echo "No process running."
    exit $E_NOSUCHPROCESS

# 为了简化整个过程，使用 "pidof"

if [ -r "/proc/$PROFILE" ]; then # 检查读取权限。
    echo "Process $1 running, ..."
    echo "Can't read permission on /proc/$PROFILE." # 普通用户无法访问 /proc 中的某些文件。
fi
if ! kill -0 $1 /dev/null 2>&1; # '0' 不是信号，但它可以测试是否可以向进程发送信号。
then
    echo "PID does not exist or you're not its owner" >&2
    exit $E_BADPID
fi

exe_file=$(ls -1 /proc/$1 | grep "exe" | awk '{ print $1 }')
# 或者 file=$(ls -l /proc/$1/exe | awk '{print $1 }')

# /proc/$1/exe 是指向调用进程完整路径的符号链接。
if [ -e "$exe_file" ]; # 如果 /proc/$1/exe 存在...
then
    # 对应的进程存在。
    echo "Process $1 invoked by $exe_file."
else
    echo "No such process running."

# 这个复杂的脚本几乎可以替换为
# ps ax | grep $1 | awk '{ print $5 }'
# 但这行不通，因为 'ps' 的第五字段是进程的 argv[0]而不是可执行文件路径。
# 然而，以下任一方法可行：
# find /proc/$1/exe -printf '%l\n'
# lsof -afn -p $1 -d txt -ne 's//p'

# Stephane Chazelas 的额外注释。

exit 0
```

### 示例 28–2. 在线状态

```bash
#!/bin/bash
PROCNAME=pppd #守护进程
PROCFILENAME=status # 查看的位置
NOTCONNECTED=65
INTERVAL=2

# 每2秒更新一次。
pidno=$(ps ax | grep -v "ps ax" | grep -v grep | grep $PROCNAME | awk '{ print $1 }')
# 查找 'pppd' 的进程号，守护进程
# 必须过滤掉搜索本身生成的进程行。
# 然而，如 Oleg Philon 所出，使用 "pidof" 可以大大简化此。
# pidno=$(pidof $PROCNAME)

# 故事的：
# 当命令序列变得太复杂时，寻找捷径。
if [ -z $pidno ]; # 如果没有 pid，则进程未运行。
then
    echo "$NOTCONNECTED"
    exit $NOTCONNECTED
else
    echo "Connected."; echo
fi

while [ true ]; # 无限循环，脚本此处可以改进。
do
    if [ ! -e /proc/$pidno/$PROCFILENAME ]; # 当进程运行时，则 "status" 文件存在。
    then
        echo "Disconnected."
        exit $NOTCONNECTED
    fi

    netstat -s grep "packets received" # 获取一些连接统计数据。
    netstat -s grep "packets delivered"

    sleep $INTERVAL
    echo; echo
done
exit 0
```

# 按照目前，此脚本必须通过 `Control-C` 终止

+ # 练习：

------

+ # 改进脚本在按下 `q` 键时退出。

# 以其他方式让脚本更对用户友好。

> 通常情况下，写入 `/proc` 中的文件是危险的，因为这可能会损坏文件系统或导致机器崩溃。

# 第 29 章 零与空值

`/dev/zero` 和 `/dev/null`

### `/dev/null` 的用途

将 `/dev/null` 视为一个“黑洞”。它是最接近只写文件的设备。所有写入它的内容都会永久消失。尝试从其读取或向其输出都不会产生任何结果。尽管如此，`/dev/null` 在命令行和脚本中非常有用。

抑制 `stdout` 或 `stderr`（示例 12-2）：

```bash
rm $badname 2>/dev/null
# 错误消息 [stderr] 不会显示。
```

在保留文件本身及其所有相关权限的情况下删除文件内容（参考示例 2-1 和 示例 2-2）：

```bash
cat /dev/null > /var/log/messages
# : > /var/log/messages 效果相同，但不会产生新进程。
cat /dev/null > /var/log/tmp
```

自动清空日志文件的内容（特别适用于处理网站发送的讨厌“cookies”）：

### 示例 29-1. 隐藏 cookie 罐

```bash
[ -f ~/.netscape/cookies ] # 如果存在，则删除。
then
  rm -f ~/.netscape/cookies
  ln -s /dev/null ~/.netscape/cookies
fi
# 所有 cookies 现在都被发送到黑洞，而不是保存到设备。
```

### `/dev/zero` 的用途

与 `/dev/null` 一，`dev/zero` 是一个伪文件，但它实际上包含空字符（零，而不是 ASCII 字符）。写入它时，内容会消失，且很难从 `/dev/zero` 中读取空字符，尽管可以使用 `od` 或十六进制编辑器来实现。`/dev/zero` 的主要用途是创建一个用作临时交换文件的初始化虚拟文件。

### 示例 29-2. 使用 `/dev/zero` 设置交换文件

```bash
#!/bin/bash

# 创建交换文件。
# 此脚本必须以 root 身份运行。
ROOT_UID=0 # root 用户的 $UID 为 0。

高级 Bash 脚本指南

E_WRONG_USER=65    # 不是 root？

FILE=~/swap
BLOCKSIZE=1024
MINBLOCKS=40
SUCCESS=0

if [ "$UID" -ne "$ROOT_UID" ]
then
    echo; echo "你必须是 root 才能运行此脚本..."; echo
    exit E_WRONG_USER
fi

if [ -n "1" ]
then
    blocks=$1
else
    blocks=$MINBLOCKS    # 如果命令行未指定，则设置为默认的 40 块。
fi

if [ "$blocks" -lt $MINBLOCKS ]
then
    # 必须至少有 40 块长。
fi
```

`/dev/zero` 的另一个应用是为了特殊目的“清零指定大小的文件”，例如在回环设备上挂载文件系统（参见示例 13–6）或安全地删除文件（参见示例 12–36）。

### 示例 29–3. 创建内存盘 (ramdisk)

```bash
#!/bin/bash
# ramdisk.sh

# "ramdisk" 是系统内存的一段
# 就像文件系统一样工作。
# 它的优点是访问速度极快（读写时间）。
# 缺点：易失性，重启或断电后数据丢失。
#                 会减少系统的可用内存。

# 什么是好的内存盘？
# 在内存盘上保留大型数据集（如表格或字典）
# 可以加快数据查找速度，因为内存访问远快于磁盘访问。

E_NON_ROOT_USER=70                # 必须以 root 身份运行。
ROOTUSER_NAME=root

高级 Bash 脚本指南

MOUNTTP=/mnt/ramdisk
SIZE=2000                          # 2K 块（根据需要更改）
BLOCKSIZE=1024                      # 1K (1024 字节) 块大小
DEVICE=/dev/ram0                    # 第一个内存设备

username=$(id -nu)
if [ "$username" != "$ROOTUSER_NAME" ]
then
    echo "必须以 \"$(basename $0)\" 运行。"
    exit $E_NON_ROOT_USER
fi

if [ ! -d "$MOUNTTP" ];               # 测试挂载点是否存在，
then
    mkdir $MOUNTTP                    # 这样即使多次运行此脚本
                                     # 也报错。
fi

dd if=/dev/zero of=$DEVICE count=$SIZE bs=$BLOCKSIZE  # 清空内存设备。
mke2exts $DEVICE                     # 在上面创建 ext2 文件系统。
mount $DEVICE $MOUNTTP                # 挂载。
chmod 777 $MOUNTTP                   # 让普通用户可以访问内存盘。
                                     # 然而，必须是 root 才能卸载它。

echo "\"$MOUNTTP\" 现在可用。"
# 普通用户现在也可以访问内存盘来存储文件。

# 注意，内存盘是易失的，其内容将在重启或断电时消失。
# 请将保存的任何内容复制到普通目录。

# 重启后，再次运行此脚本以设置内存盘。
# 在没有其他步骤的情况下重新挂载 /mnt/ramdisk 将不起。

exit 0
```

# 第 30 章. 调试

`Bash` shell 不包含调试器，也没有任何用于调试的命令或结构。脚本中的语法错误或明显的拼写错误产生晦涩的错误信息，这些信息对于调试无法运行的脚本通常没有帮助。

### 示例 30–1. 一个有错误的脚本

```bash
#!/bin/bash
# ex74.sh

# 这是一个错误的脚本。

a=37

if [ $a -gt 27 ]
then
  echo $a
fi

exit 0
```

脚本的输出：

```
./ex74.sh: [37]: command not found
```

上面的脚本哪里有问题？（提示：`if` 语句）

如果脚本执行了，但结果不符合预期呢？这是一个非常熟悉的逻辑错误。

### 示例 30–2. test24, 另一个错误的脚本

```bash
#!/bin/bash
# 这个脚本本应该删除当前目录下所有
# 包含空格的文件名。
# 它不起作用。为什么？

badname=$(ls | grep ' ')
# echo "$badname"
```

## 示例 30–4. 退出时的陷获

```bash
#!/bin/bash

trap 'echo Variable Listing --- a = $sa b = $sb' EXIT
# EXIT 是脚本退出时生成的信号名称。

a=39

b=36

exit 0
```

# 请注意，注释掉 `exit` 命令会产生影响，

# 因为脚本在运行完所有命令后无论如何退出。

# 示例 30–5. Control–C 后的清理

```bash
#!/bin/bash
# logon.sh: 一个快速且粗略的脚本，用于检查你是否在线。

TRUE=1
LOGFILE=/var/log/messages
# 注意 LOGFILE 必须是可读的 (chmod 644 /var/log/messages)。
TEMPFILE=tmp.\$
# 创建一个“唯一”的临时文件名，使用脚本的进程 ID。
KEYWORD=address
# 在登录时，行 "remote IP address xxx.xxx.xxx.xxx"
# 会追加到 /var/log/messages。

ONLINE=22
USER_INTERRUPT=13

trap 'rm -f $TEMPFILE; exit $USER_INTERRUPT' TERM INT
# 如果脚本被 control-c 中断，则清理文件。

echo

while [ $TRUE ]; do # 无限循环。

  tail -1 $LOGFILE > $TEMPFILE
  # 将系统日志文件的最后一行保存为临时文件。
  search=$(grep $KEYWORD $TEMPFILE)
  # 检查是否存在 "IP address" 短语，
  # 表示登录成功。

  if [ -z "$search" ]; # 因为可能存在空格，需要引号。
  then
    echo "On-line"
    rm -f $TEMPFILE # 清理临时文件。
    exit $ONLINE
  else
    echo -n "." # -n 选项抑制 echo 的换行，
    # 这样你会得到连续的一行点。
  fi

  sleep 1
done
```

# 注意：如果你将 `KEYWORD` 变量更改为 "Exit"

# 该脚本可以在在线时使用，以检查意外的注销。

# 第 30 章 调试

# 高级 Bash 脚本编写指南

# 练习：根据上面的说明修改脚本，

# 并将其美化。

```bash
exit 0
```

# Nick Drage 建议另一种替代方法：

```bash
while true
do
  ifconfig ppp0 | grep UP 1 > /dev/null && echo "connected" && exit 0
  echo - "." # 打印点（.... 直到连接）。
  sleep 2
done
```

# 问题：通过 `Control-C` 终止此进程可能是不够的。

# （可能会持续输出。）

# 练习：修复此。

# Stéphane Chaselas 还有另一种替代方案：

```bash
CHECK_INTERVAL=1
while ! tail -1 "$LOGFILE" | grep -q "$KEYWORD"
do
  sleep $CHECK_INTERVAL
  echo "On-line"
```

# 练习：讨论这些各种方法的优缺点。

> `trap` 的 `DEBUG` 参数会导致脚本中的每条命令执行时都执行指定的动作。这允许对变量进行追踪等。

## 示例 30– 跟踪变量



```bash
#!/bin/bash
trap 'echo "VARIABLE-TRACE = \"$variable\"*' DEBUG
# 在每个命令执行后回显 $variable 的值。

variable=29
echo "Just initialized \"$variable\" to $variable."

let variable *= 3
echo "Just multiplied \"$variable\" by 3."
```

`trap` 命令的 `'commands'` 结构在复杂脚本中会更有用，

在那种情况下，放置多个 `echo $variable` 语句可能会

变得笨拙且耗时。

感谢 `Stéphane Chaselas` 的指点。

```bash
exit 0
```

## 第 30 章 调试

`trap '' SIGNAL`（两个相邻的单引号）在脚本剩余时间内禁用 `SIGNAL`。`trap SIGNAL` 再次恢复 `SIGNAL` 的功能。

这对于保护脚本的关键部分免受意外中断很有用。

```bash
trap '' 2 # 信号 2 是 Control-C，现在已禁用。
command
command
trap 2 # 重新启用 Control-C
```

## 第 31 章 选项

选项是改变 shell 和/或脚本行为的设置。

`set` 命令启用脚本中的选项。在脚本中你希望选项生效的地方，使用 `set -option-name` 或简写形式 `set -option-abbrev`。这两种形式是等价的。

```bash
#!/bin/bash
set -o Echo all commands before executing. # 在执行前回显所有命令。
```

```bash
#!/bin/bash
set -v
# 与上述效果相同。
```

要禁用脚本中的选项，使用 `set +option-name` 或 `set +option-abbrev`。

```bash
#!/bin/bash
set -o verbose
# 命令回显开启。
command
...
command
set +o verbose
# 命令回显关闭。
command
# 不回显。
set -v
# 命令回显开启。
command
...
command
set +v
# 命令回显关闭。
command
exit 0
```

在脚本中启用选项的另一种方法是在紧接 `#!` 脚本头部之后指定它们。

```bash
#!/bin/bash -x
#
```

# 高级 Bash 脚本编写指南

脚本正文如下。

也可以从命令行启用脚本选项。某些无法与 `set` 使用的选项可以通过这种方式可用。其中包含 `-i`，强制脚本以交互模式运行。

```bash
bash -v script-name
```

```bash
bash -o verbose script-name
```

以下是一些常用选项的列表。可以使用缩写形式或全称指定。

### 表 31–1. bash 选项

| 缩写 | 名称 | 效果 |
| :--- | :--- | :--- |
| `-C` | `noclobber` | 防止通过重定向覆盖文件（可能会被 `>` 覆盖） |
| `-D` | (none) | 列出以 `$` 为前缀的双引号字符串，但不执行脚本中的命令 |
| `-a` | `allexport` | 导出所有定义的变量 |
| `-b` | `notify` | 在后台运行的任务结束时通知（在脚本中用处不大） |
| `-c ...` | (none) | 从 `...` 读取命令 |
| `-f` | `noglob` | 禁用文件名扩展（通配符） |
| `-i` | `interactive` | 脚本在交互模式下运行 |
| `-p` | `privileged` | 脚本作为 `suid` 运行（注意！） |
| `-r` | `restricted` | 脚本在限制模式下运行（见第 21 章）。 |
| `-u` | `nounset` | 遇到未定义变量时报错 |
| `-v` | `verbose` | 在执行前回显命令 |
| `-x` | `xtrace` | 与 `-v` 类似，但展开命令 |
| `-e` | `errexit` | 命令以非零状态退出时终止脚本 |
| `-n` | `noexec` | 从标准输入读取命令 |
| `-s` | `size` | 检查文件是否为空 |
| `-t` | `terminal` | 检查是否为终端 |
| `-` | (none) | 选项结束。 |
| `--` | (none) | 选项结束。 |

## 第 31 章 选项

## 第 32 章 陷阱 (Gotchas)

> Turandot: Gli enigmi sono tre, la morte!
>
> Caleph: No! Gli enigmi sono tre, una vita!

混用整数字符串比较运算符。记住，`=` 用于字面量，`-eq` 用于整数。

```bash
if [ "$sa" = 273 ]   # $sa 是一个整数吗？
if [ "$sa" -eq 273 ]   # $sa 是整数吗？
```

有时你可以混用 `-eq` 和 `=` 而不产生不利后果。

然而...

`a=273.0` # 不是整数。

```bash
if [ "$sa" = 273 ]
then
  echo "比较有效。"
else
  echo "比较无效。"
fi   # 比较无效。
```

对于 `a="273"` 和 `a="0273"` 也是如此。

同样，在非整数值上使用 `-eq` 会产生问题。

```bash
if [ "$sa" -eq 273.0 ]
then
  echo "a = $sa"
fi   # 报错
# test.sh: [273.0: integer expression expected
```

混淆整数字符串比较运算符。

```bash
#!/bin/bash
# bad-op.sh
```

```bash
number=1
```

```bash
while [ "$number" < 5 ]   # 错误！应该是 [ "$number" -lt 5 ]
do
  echo -n "$number"
  let "$number" += 1
done
```

```bash
# 尝试运行此会报错
# bad-op.sh: 5: No such file or directory
```

有时“括号” `[ ]` 内的变量需要引用（双引号）。不这样做会导致意外行为。参见示例 7-5、示例 16-2 和示例 9-6。

从脚本发出的命令可能无法执行，因为脚本所有者缺乏这些命令的执行权限。如果用户无法从命令行调用命令

尝试将其用作重定向运算符（它并不是）会导致令人不快的意外。

```bash
command1 2-> | command2 # 尝试将 command1 的错误输出重定向到管道...
#   ...将无法工作。
```

## 高级 Bash 脚本指南

```
command1 2>& | command2 # 这样做也是徒劳的。

感谢，S.C.
```

使用 Bash 2+ 版本的功能可能会导致带有错误信息的强制退出。较旧的 Linux 机器默认安装的是 1.XX 版本的 Bash。

```bash
#!/bin/bash

minimum_version=2
# 由于 Chet Ramey 不断向 Bash 添加新功能，
# 你可以将 $minimum_version 设置为 2.XX，或任何合适的值。
SE_BAD_VERSION=80

if [ "$BASH_VERSION" -lt "$minimum_version" ];
then
  echo "此脚本仅在 Bash $minimum_version 或更高版本下运行。
  echo "强烈建议升级。"
  exit $SE_BAD_VERSION
fi
```

在非 Linux 机器上在 Bourne 脚本 (`/bin/sh`) 中使用 Bash 特有功能可能会导致意外行为。Linux 系统通常将 `sh` 别名为 `bash`，这在通用的 UNIX 机器上并不一定。

具有 DOS 类型换行符 (`\r`) 的脚本将无法执行，因为 `/bin/bash\r` 不被识别，它不同于 `/bin/bash`。修复方法是将脚本转换为 UNIX 风格的换行符。

以 `#!/bin/sh` 开头的脚本可能不在 Bash 兼容模式下运行。Bash 特有的函数可能会被禁用。需要完全访问所有 Bash 特有扩展的脚本应该以 `#!/bin/bash` 开头。

脚本可能无法将其变量导出到父进程（shell）或环境中。正如生物学中学到的，子进程可以继承父进程，但反之则不然。

```
WHATEVER=/home/bozo
export WHATEVER
exit 0
bash$WHATEVER
bash$
```

不出意外，回到命令行提示符后，`$WHATEVER` 仍然未设置。

在 shell 中设置和操作变量，尝试在 shell 范围之外使用这些变量将导致一个不快的惊喜。

### 示例 32–1. 子壳陷阱

```bash
#!/bin/bash
# 子壳中变量的陷阱。
```

`outer_variable=outer`

## 第 32 章. 注意事项 (Gotchas)

## 高级 Bash 脚本指南

```bash
echo
echo "outer_variable = $outer_variable"
echo
(
# 开始子壳
echo "outer_variable inside subshell = $outer_variable"
inner_variable=inner # 设置
echo "inner_variable inside subshell = $inner_variable"
out_variable=inner # 值会全局变化吗？
echo "outer_variable inside subshell = $outer_variable"
# 结束子壳
)
echo
echo "inner_variable outside subshell = $inner_variable" # 未设置
echo "outer_variable outside subshell = $outer_variable" # 未改变。
echo
```

在脚本中使用 `suid` 命令是有风险的，因为它可能会危及系统安全。[61]

使用 shell 脚本进行 CGI 编程可能会出现问题。shell 脚本变量不是“类型安全的”，这对于 CGI 而言可能会导致不可预的行为。此外，很难对 shell 脚本进行“防破解处理”。

> 危险近在咫尺 --
>
> 小心，小心，小心，小心。
>
> 许多勇敢的心灵睡在深渊之中。
>
> 所以要留心 --
> > 小心。
>
> AJ. Lamb 和 H.W. Petrie

## 第 33 章. 风格化脚本

养成结构化和系统化编写 shell 脚本的习惯。即使是“即时”和“写在信封背面”的脚本，如果你在坐下编码之前花几分钟规划和组织思路，也会受益匪浅。

以下是一些风格指南。这并不打算作为官方的 Shell 脚本样式表。

### 33.1. 非官方 Shell 脚本样式表

- 为你的代码添加注释。这使得代码更易于理解（以及欣赏），并且更易于你进行维护。
- `PASS="$PASSES(MATRIX:$($RANDOM$(#MATRIX))):):1"`
- 当你去年写它时它非常有道理，但现在它完全是一个谜团。
- （来自 Anton Sawicki 的 `"pw.sh"` 脚本。）

为你的脚本和函数添加描述性的头部。

```bash
#!/bin/bash

****************************************************
# xyz.sh
# 作者：Bozo Bozman
# 2001年7月5日

# 清理项目文件。
****************************************************

BADDIR=65      # 无此类目录。
projectdir=/home/bozo/projects  # 要清理的目录。

####################################################
cleanup_files() {
# 删除指定目录下的所有文件
# 参数：$target_directory
# 返回：成功返回 0，出错时返回 $BADDIR。
####################################################
cleanup_files() {
  if [ ! -d "$1" ]; # 测试目标目录是否存在。
  then
    echo "$1 不是一个目录。"
    return $BADDIR
  fi

  rm -f "$1"*      # 成功。
  return 0
}

cleanup_files $projectdir

exit 0
```

确保将 `#!/bin/bash` 放在脚本第一行的开头，位于任何注释头部之前。

- 避免使用“魔数”，[62]，即“硬编码”的字面量常量。使用具有意义的变量名代替。这使得脚本更易编辑，并允许在不破坏应用程序的情况下进行更改和更新。

```bash
if [ -f /var/log/messages ]
then
fi
# 一年后，
```

- 具有 DOS 类型换行符 (`\r`) 的脚本将无法执行...
- 修复方法是将脚本转换为 UNIX 风格的换行符。
- 以 `#!/bin/sh` 开头的脚本可能不在 Bash 兼容模式下运行。Bash 特有的函数可能会被禁用。需要完全访问所有 Bash 特有扩展的脚本应该以 `#!/bin/bash` 开头。
- 脚本可能无法将其变量导出到父进程（shell）或环境中。

## 高级 Bash 脚本指南

```bash
# 非交互式
...
else
  # 交互式
fi
或者，脚本可以检查是否存在 `i` 选项。
case "$*" in
  i*) # 交互式
    ;;
  *) # 非交互式
    ;;
# (感谢你，Unix 1993)
```

脚本可能会通过 `-i` 选项强制在交互模式运行。注意，这会导致异常行为或在没有错误时显示错误信息。

## 34.2. 封装器

“封装器”（wrapper）是一个封装系统命令或工具的脚本，它保存了传递给命令的一组参数。对于 `sed` 或 `awk` 特别有用。

`sed` 或 `awk` 通常从命令行调用。将此类脚本嵌入 Bash 脚本中可以简单地调用它，使其变得“可重用”。这允许组合 `sed` 和 `awk` 的功能，例如将 `sed` 的输出管道至 `awk`。

### 示例 34–1. 封装器

```bash
#!/bin/bash
# 这是一个删除文件中空行的简单脚本。
```

```bash
# 无参数检查。
# 与 `sed -e '^$/d' filename` 从命令行调用的方式相同。
sed -e '/$/d' "$"
# `-e` 意味着后面的“编辑”命令（此处）。`^` 是行开头，`$` 是行尾。匹配开头和结尾之间的空行。
引号命令允许文件名包含空格和特殊字符。
exit 0
```

### 示例 34–2. 稍微复杂的封装器

```bash
#!/bin/bash
# 在目标文件中添加指定的列。

ARGS=2
E_BADARGS=65

if [ $# -ne "$ARGS" ]; # 检查命令行参数是否正确
then
    echo "用法: $0 filename列数"
    exit $E_BADARGS
fi

old_pattern=$1
new_pattern=$2

if [ -f "$3" ]; then
    file_name="$3"
else
    echo "文件 $3 不存在。"
    exit $E_BADARGS
fi

# 这里是执行大量工作的地方。
sed -e "s/$old_pattern/$new_pattern/g" "$file_name"
# 's' 显然是 `sed` 中的替换命令，`/pattern/` 触发对 $old_pattern 的替换。
# "g" 全局标志会对每行的每一个出现处进行替换，而不只是第一个。
查阅 `sed` 文献以获取更深入的解释。

exit 0 # 脚本成功执行返回 0。
```

### 示例 34–3. awk 脚本的封装器

```bash
#!/bin/bash
# 在文件中添加指定的列（数字）。

ARGS=2
E_WRONGARGS=65

if [ $# -ne "$ARGS" ]; # 检查命令行参数数量
then
    echo "用法: $0 filename 列数"
    exit $E_WRONGARGS
fi

filename=$1
column_number=$2
```

```bash
# 将变量传递给脚本的 awk 部分有点复杂。
# 更多信息请查看 awk 文档。

# 多行 awk 脚本通过 awk ' . . ' 调用。

# 开始 awk 脚本。
# ----------------------
awk '
{
sum += $1
}
END {
    print sum
}'
```

（注：由于原文中存在大量完全重复的代码块和注释，根据“注意一定不要重复输出原文”的原则，此处译文仅保留并翻译了核心逻辑结构及代表性说明。）

```bash
# 将变量传递给脚本的 awk 部分有点复杂。
# 更多信息请查看 awk 文档。
```

## 高级 Bash 脚本指南

- 存放包含你最喜欢和最实用的定义和函数的文件。根据需要，使用点运算符 (`.`) 或 `source` 命令在脚本中“包含”一个或多个此类“库文件”。



# 脚本库

> **注意**
> * 这里没有 "!" 符号。
> * 也没有“实时代码 (live code)”。

## 有用的变量定义

```bash
ROOT_UID=0      # Root 用户的 UID 为 0。
E_NOTROOT=101 # 非 root 用户错误。
MAXRETVAL=256 # 函数的最大（正数）返回值。
SUCCESS=0
FAILURE=-1
```

## 函数

### `Usage()`

# "Usage:" 消息。

```bash
Usage ()       # "Usage:" 消息。
{
  if [ -z "$1" ] # 未传递参数。
  then
    msg=filename
  else
    msg=$0
  fi
}
echo "Usage: $(basename $0)\" \"$msg\""
```

### `Check_if_root()`

检查是否以 root 身份运行脚本。

```bash
Check_if_root () # 检查是否以 root 身份运行脚本。
if [ "$UID" -ne "$ROOT_UID" ] # 取自 "ex39.sh" 示例。
then
  echo "必须以 root 身份运行此脚本"
  exit E_NOTROOT
fi
```

### `CreateTempFileName()`

创建一个“唯一的”临时文件名。

```bash
CreateTempFileName () # 创建一个“唯一的”临时文件名。
{
  prefix=temp
  suffix=$(date +%s)
  Tempfilename=$prefix.$suffix
}
```

### `isalpha2()`

测试“整个字符串”是否为字母。

```bash
isalpha2 () # 测试“整个字符串”是否为字母。
{
  # 取自 "isalpha.sh" 示例。
  if [ $1 -eq 1 ] || return $FAILURE
}
case $1 in
  "*[a-zA-Z]*") return $FAILURE;
  *) return $SUCCESS;
esac                                # 感谢 S.C.。
```

### `abs()`

计算绝对值。

```bash
abs ()
{
  E_ARGERR=-999999                             # 绝对值。
                              # 注意：最大返回值 = 256。

  if [ -z "$1" ]                               # 需要传递参数。
  then
    return $E_ARGERR                        # 返回明显的错误值。
  fi

  if [ "$1" -ge 0 ]                            # 如果是非负数
  then
    absval=$1                                # 保持不变。
  else
    let absval=$(( 0 - $1 ))               # 否则，
                               # 改变符号。
  fi

  return $absval
}
```

### `tolower()`

将作为参数传递的字符串转换为小写。

```bash
tolower (                               # 将作为参数($)传递的字符串
{
                              # 转换为小写。

  if [ -z "$1" ]                                # 如果未传递参数 ($s)，
  then
    echo "null"                          # 发送错误消息
    return                                # (C 风格空指针错误消息)
                               # 从函数返回。
  fi

echo "$#" | tr -A a-z
# 转换所有传递的参数 ($@)。

return

# 使用注释替换将函数的输出赋值给变量。
# 例如：
# oldvar=$(tolower of mixed-caSeLeterS)
# newvar=$(tolower "$oldvar")
# echo "$newvar"                          # 一组混合大小字母
# 练习：重写此函数以将传递的小写参数($)
# 转换为大写 .... toupper($) [简单]。
```

* 使用特殊用途的注释头部来增加脚本的清晰性和合法性。

## 警告

```bash
## 警告。
rm -rf ./*                               # "rm" 的 "-rf" 非常危险，
                               # 尤其是使用通配符时。
```

## 换行符

```bash
## 换行符。
# 这是多行注释的
# 第 1 行，
# 这是最后最后一行。
```

## 注意

```bash
## 注意。
```

* O 列表项。

```bash
# 另一种观点。
while [ "$varl" = "end" ]
  while test "$varl" != "end"
```

使用 `$?` 状态变量，脚本可以测试参数是否仅包含数字，从而可以将其视为整数。

```bash
#!/bin/bash

SUCCESS=0
E_BADINPUT=65

test "$1" -ne -o "$1" -eq 0 2>/null
# 整数要么等于 0，要么不等于 0。
# 2>/null 抑制错误消息。

if [ "$1" -ne "$SUCCESS" ]; then
  echo "Usage: $0 <input>"
  exit $E_BADINPUT
fi
```

```bash
let sum=$1 + $2  # 如果 $1 不是整数则会报错。
echo "sum = $sum"
```

任何变量（而不只是命令行）都可以用任何 0 范围的返回值进行测试，这是一个严重的限制。全局变量的变通方法通常有问题。函数向主体返回值的另一种方法是让函数写入标准输出 (`stdout`)，并将其给变量。

## 34.6. 返回值

```bash
#!/bin/bash
# 乘法

multiply () { # 乘以参数。
  local product=1
  until [ -n "$1" ]; do # 直到参数为空。
    let product *= $1
    shift # 移动位。
  done
  echo "$product" # 输出结果。
}

result=$(multiply 2 3 4) # 将函数输出赋值给变量。
echo "Result: $result"
```

## 34.7. 多个返回值

```bash
#!/bin/bash
# 多个返回值

get_stats () { # 获取统计。
  local sum=$1
  local count=$2
  local avg=$(( sum / count ))
  echo "$sum"   # 输出总和。
  echo "$count" # 输出计数。
  echo "$avg"   # 输出平均值。
}

# 使用 read 接收多个返回值。
read s c a < <(get_stats 100 5)
echo "Sum: $s, Count: $c, Avg: $a"
```

## 34.8. 数组返回

```bash
#!/bin/bash
# 数组返回

get_array () { # 获取数组。
  local arr=("$@")
  echo "${arr[@]}" # 输出数组元素。
}

my_array=($(get_array "apple" "banana" "cherry"))
echo "Array: ${my_array[@]}"
```

# 高级 Bash 脚本指南

关于将数组传递给函数的更详细示例，请参见示例 A–8。

* 使用双括号 `()` 结构，可以使用 C 语言语法来设置和增加变量，以及在 `for` 和 `while` 循环中使用。请参见示例 10–12 和示例 10–17。
* 一种实用的脚本技术是反复将过滤器的输出（通过管道）传递给同一个过滤器，并使用不同的参数集和/或选项。如果这是 `tr` 命令，这种方法尤为适用。

```bash
# 来自 "wstrings.sh" 示例。
wlist="strings "$* | tr A-Z a-z | tr '[:space:]' Z | |
tr -cs '[[:alpha:]]' Z tr -s '\1\37\37' Z tr Z ' '
```

* `run-parts` 命令非常适合顺序执行一组命令脚本，特别是与 `cron` 或 `at` 结合使用时。
* 如果能从 shell 脚本中调用 X–Windows 组件就太好了。目前已经几个实现此功能的包，即 `Xscript`、`Xmenu` 和 `widtools`。其中前两个似乎较难维护。幸运的是，在这里仍然可以扩展 `widtools`。

![](img/1ce1edffaa36e4f698a8543e71cd3b_327_0.png)

`widtools` 软件包需要安装 `XForms`。此外，在典型的 Linux 系统上需要对 `Makefile` 进行一些编辑。最后，提供的六个包中有三个无法工作（实际上它们已经失效了）。

为了更有效地编写脚本，请尝试 `wish`（Tcl 的衍生品）、`PerlTk`（Perl 的 Tk ）、`ksh`（ksh 扩展）、`XForms4l`（Perl 的 XForms ）或 `PyQt`（Python 的 Qt ）。

## 34.6. 递归

脚本可以递归地调用自己。

**示例 34–9.** 一个递归调用自己的脚本。

```bash
#!/bin/bash
# recurse.sh

# 脚本可以递归地调用自己吗？
# 是的，但这只是“概念验证”。

RANGE=10
MAXVAL=9
i=$RANDOM  # 在 0 到 $MAXVAL 之间生成一个随机数。
```

```bash
if [ "$i" -lt "$MAXVAL" ]
then
  echo "$i = $i"
# 脚本递归地生成自身的另一个实例。
# 每个子进程执行相同的操作，直到 $i 等于 $MAXVAL
# 使用 "while" 循环代替 "if/then" 测试会导致问题。
# 解释原因。

exit 0
```

![](img/1ce1edffaa36e4f698a8543e71cd3b_328_0.png)

递归深度会耗尽脚本的栈空间，导致段错误（`segfault`）。

## 34.7. 可移植性问题

本书专门涉及 GNU/Linux 系统上的脚本编写。同样，`sh` 和 `ksh` 的用户将从这里获得很多价值。

事实上，许多 shell 和脚本语言似乎都在向 POSIX 1003.2 标准收敛。使用 `--posix` 选项调用 `Bash` 或在脚本头部插入 `-o posix` 会使 `Bash` 严格遵循该标准。缺乏这一措施，大多数 `Bash` 脚本在 `ksh` 下无法运行，反之亦然。由于 Chet Ratney 已将 `ksh` 特性推向最新的 `Bash` 版本，这种趋势只会加速。

## 34.8. 在 Windows 下编写脚本

运行其他操作系统的用户也可以编写类 Unix 脚本，并从本书的许多课程中受益。`Cygwin` 软件包和 Mortice Associates 的 `MKS` 工具为 Windows 增加了脚本能力。

# 35. Bash 版本 2

你机器上运行的 `Bash` 版本实际上是 2.XX。

```bash
bash$ echo $BASH_VERSION
2.04(1)-release
```

经典 `Bash` 脚本语言的这次更新增加了数组变量、以及更好的间接变量引用方法。

## 35–1. 字符串扩展

```bash
#!/bin/bash

# 字符串扩展。
# 在 Bash 版本 2 中引入。

# 形式为 $'xxx' 的字符串会解释转义字符。

echo '$Ringing bell 3 times \a \a'
echo '$Three feeds \f \f'
echo '$10 newlines \n\n\n\n\n\n\n'

exit 0
```

## 35–2. 间接引用——新方法

```bash
#!/bin/bash

# 间接变量引用。
# 这具有 C++ 引用的一些属性。

a=letter_of_alphabet
letter_of_alphabet=z

echo "a = $a"      # 直接引用。
echo "Now a = ${!a}" # 间接引用。
echo "$(variable) 表示法远优于旧方法"
t=table_cell_3
table_cell_3=387
echo "t = ${!t}"    # t = 387
echo "Value of t to ${!t}"

# 这对于引用数组成员或模拟多维数组很有用。
# 如果有索引选项就更好了 ()。
exit 0
```

## 35–3. 使用间接引用的简单数据库

```bash
#!/bin/bash
# resistor-inventory.sh
# 使用间接引用的简单数据库应用程序。

############################################
# 数据
B123_value=470                          # 欧姆
B123_powerdissip=.25                   # 瓦特
B123_colorcode="yellow-violet-brown"  # 色带
B123_loc=17                           # 位置
B123_inventory=78                      # 数量

B124_value=1000
B124_powerdissip=.25
B124_colorcode="brown-black-red"
B124_loc=24
B124_inventory=43

B125_value=10000
B125_powerdissip=.25

############################################
echo "Inventory:"
# 这里的逻辑只是为了演示间接引用
# 实际应用中会遍历变量
for i in B123 B124 B125; do
  echo "Item $i: ${!i_value} ohms, ${!i_powerdissip}W"
done
```

# 高级 Bash 脚本指南

```bash
return 0
}

# 结构化编程：
# 整个程序逻辑模块化在函数中。

=================
seed_random
initialize_Deck
initialize_Suits
initialize_Cards
deal_cards

exit 0
====================
```

# 练习 1：

* 添加注释以详细说明脚本。

# 练习 2：

* 修改脚本以按花色打印每个手牌。

* 如果你喜欢，可以添加其他额外功能。

# 练习 3：

* 简化并优化脚本的逻辑。

第 35 章.Bash，版本 2 328

# 第 36 章 终记

## 36.1. 作者序

我是如何开始写一本 Bash 脚本书的？这是一个奇怪的故事。似乎几年前，我需要学习 shell 脚本，而没有什么方法比读一本关于该主题的好书更好了了。我当时正想写一份涵盖脚本各个方面的教程和参考书。事实上，我找的正是这本书，或者类似的书。遗憾的是，它并不存在，所以如果我想要，就得自己写。于是，伙计们，我们就在这里。

这让我想起那个关于疯狂教授的传闻故事。那家伙像小丑一样疯狂。只要看到书（任何一本书，在图书馆、书店或任何地方），他就会完全痴迷于这样一个想法：他本可以写这本书，本该写这本书，而且还可以做得更好。随后他会冲回家，在同一时间写出一本书。几年后当他真的做到了时，他已经拥有了几部著作，可能甚至让阿西莫都感到逊色。那些书可能并不好，谁知道呢，但这真的重要吗？这是一个实现了梦想的人，尽管他是被梦想所驱动的，我不禁佩服这位老酷范儿……

## 36.2. 关于作者

这个哥们到底是谁？

作者声称自己没有任何资历或特殊资格，除了写作的冲动。[64] 这本书与他的另一部主要作品《如何与女性交往：害羞男人的关系指南》有所不同。他写写过《软件构建指南》（`HOWTO`）。

作为自 1995 年以来的 Linux 用户（`Shellack 2.2`，内核 `1.2.1`），作者发布过几款“软件松露”，包括 `cruft` 一次性密码加密工具、`makes` 房贷贷款计算器、`judge` Scrabble® 评判器，以及 `yaw` 单词列表包。他最初是在 CDC 3800 机器上使用 FORTRAN IV 开始编程的，对于那些日子来说，这并不让人怀旧。

他与妻子和狗生活在一个偏远的沙漠社区，他珍视人类的脆弱性。

## 36.3 制作本书时使用的工具

### 36.3.1. 硬件

一台二手的 IBM Thinkpad 760XL 型号笔记本电脑（`P166`，`80MB` 内存），运行 Red Hat 7.1/7.2。诚然，它很慢，键盘也很古怪，但它比 2 号铅笔和大型写字板好得多。

### 36.3.2. 软件和打印设备

* i. `Bram Molenaar` 强大的支持 `SGML` 的 `vim` 编辑器。
* ii. `OpenJade`，一种将 `SGML` 文档转换为其他格式的 `DSSSL` 渲染引擎。
* iii. `Norman Walsh` 的 `DSSSL` 样式表。
* iv. 《`DocBook` 权威指南》，`Norman Walsh` 和 `Leonard Muellner` 编写（`O'Reilly` 出版），`ISBN 1-56592-587`。这是尝试以 `Docbook SGML` 格式编写文档的标准参考书。

## 36.4. 致谢

社区的参与使得本项目成为可能。作者衷感谢，如果没有各位的帮助和反馈，编写这本书将是一项无法完成的任务。

Philippe Martin 将本文翻译成 DocBook/SGML。虽然他不是法国某小公司的软件开发人员，但他喜欢从事 GNU/Linux 文档和软件、文学创作、演奏音乐以及与朋友聚乐。你可能在法国或巴斯克地区遇到他，或者通过邮件 `feloy@free.free` 与他联系。



Philippe Martin 还指出位置参数 `$9` 使用了 `[]` 符号表示，参见示例 5–5。

Stéphane Chazelas 提供了长长的修正、补充和示例脚本列表。除了贡献者，他实际上承担了本书的编辑工作。非常感谢！

我要感谢 Patrick Callahan、Mike Novak 和 Pal Domicos 发现 Bug、指出歧义并建议澄清和修改。他们对 shell 脚本和通用文档问题的讨论启发了我让文档易读。

感谢 Jim Van Zandt 指出 0.2 版本的错误和遗漏，他还贡献了一个直观的示例脚本。

非常感谢 Jordi Sanfeliu 允许使用他的自由树脚本（示例 A–15）。

感谢 Noah Friedman 允许使用他的字符串脚本（示例 A–16）。

Emmanuel Rougat 对命令替换和别名提出了修正和补充。他还贡献了一个非常好的示例 `.bashrc` 文件（附录 G）。

Heiner Steven 慷慨允许使用他的进制转换脚本（示例 12–3）。

Florian Wisser 让我了解了一些 Bash，并提供了许多建议。

Oleg Knoop 指出了一些错误。

# 高级 Bash 脚本指南

Arnold Robbins, *Effective Awk Programming*, Free Software Foundation / O'Reilly and Associates, 2000, 1–882114–26–4.

最棒的 **awk** 教程和参考资料。这本书的免费电子版是 **awk** 文档的一部分，最新版本的纸质版可通过 O'Reilly and Associates 购买。

这本书为作者编写本文的文档提供了灵感。

Bill Rosenberg, *Learning the Korn Shell*, O'Reilly and Associates, 1993, 1–56592–054–6.

这本编写良好的书包含了关于 shell 脚本的一些优秀见解。

Paul Sheer, *LINUX: Route User's Tutorial and Exposition*, 第 1 版, 2002, 0–13–033351–4。

对 Linux 系统管理非常详尽且易读的介绍。

这本书有纸质版，也可以[在线阅读](on-line)。

Ellen Siever 和 O'Reilly and Associates 的员工, *Linux in a Nutshell*, 第 2 版, O'Reilly and Associates, 1999, 1–56592–585–8.

最全的 Linux 命令参考，甚至包含一个 Bash 部分。

*The UNIX CD Bookshelf*, 第 2 版, O'Reilly and Associates, 2000, 1–56592–815–6.

一套包含在 CD 上的六本 UNIX 书籍，包括 **UNIX Power Tools**、**Sed** 和 **Awk** 以及 **Learning the Korn Shell**。这是一套你可能需要的所有 UNIX 参考和教程，价格约为 70 美元。即使这意味着要负债不交房租，也买它吧。

遗憾的是，已经过时了。

O'Reilly 关于 Perl 的书籍。（实际上是任何 O'Reilly 的书籍。）

---

## 参考文献

# 高级 Bash 脚本指南

Ben Okopnik 在 [Linux Gazette](link) 第 53, 54, 55, 57 和 59 期发表了编写良好的 Bash 脚本入门文章，以及他在第 56 期中对“Bash 的深层、黑暗秘密”的解释。

Chet Ramey 的 *bash – The GNU Shell*，是一个发表在 1994 年 7 月至 8 月 [Linux Journal](link) 第 3 和 4 期的作品。

Mike G 的 [Bash–Programming–Intro HOWTO](link)。

Richard 的 [UNIX Scripting Universe](link)。

Chet Ramey 的 [Bash F.A.Q.](link)。

[Lucc’s Shell Scripts](link) 中的示例 shell 脚本。

[SHELLorado](link) 中的示例 shell 脚本。

[Noah Friedman’s script site](link) 中的示例 shell 脚本。

[SourceForge Snippet Library – shell scripts](link) 中的示例 shell 脚本。

Giles Orr 的 [Bash–Prompt HOWTO](link)。

[sed F.A.Q.](link)。

Carlos Duarte 具有指导意义的 ["Do It With Sed"](link) 教程。

GNU gawk [参考手册](link)（gawk 是 awk 的扩展 GNU 版本，适用于 Linux 和 BSD 系统）。

Trent Fisher 的 [groff 教程](link)。

Mark Komarinski 的 [Printing–HOWTO](link)。

在[阿尔伯塔大学网站](link) 的 [textutils 文档第 10 章](link) 中有一些关于 [I/O 重定向](link) 的材料。

# 参考文献

# 高级 Bash 脚本指南

Rick Hohenhesee 完全用 bash 脚本编写了 osimpa i386 汇编器。

由 Chet Ramey 和 Brian Fox 编写的优秀“Bash 参考手册”，作为 `bash–2–doc package` 的一部分（可通过 rpm 获取）。请特别注意该程序包中具有指导意义的示例脚本。

`comp.os.unix.shell` 新组。

`bash` 和 `bash2`, `date`, `expect`, `expr`, `find`, `grep`, `gzip`, `ln`, `patch`, `tar`, `bc`, `xargs` 的 manpages。关于 `bash`, `ddd`, `m4`, `awk`, `sed` 的 texinfo 文档。

## 附录 A. 贡献的脚本

这些脚本没有放入本文正文，但它们展示了一些有趣的编程技术。它们很有用。祝你分析和运行它们时愉快。

### 示例 A–1. manview: 查看格式化的 manpages

### 示例 A–2. mailformat: 格式化电子邮件消息

```bash
#!/bin/bash
# mailformat.sh: Format e-mail messages.

# 移除脱号、制表符，并折叠过长的行。
# 脚本参数的标准检查
ARGS=1
E_BADARGS=65
E_NOFILE=66

if [ $# -ne $ARGS ]; # 传递给脚本的参数数量是否正确？
then
    echo "Usage: $0 filename"
    exit $E_BADARGS
fi

if [ -f "$1" ]; # 检查文件是否存在。
then
    file_name=$1
else
    echo "File $1 does not exist."
    exit $E_NOFILE
fi

MAXWIDTH=70 # 折叠行的宽度。
# 删除行开头的脱号和制表符，
# 然后将行折叠为 $MAXWIDTH 个字符。
sed '/\s*//d' # 删除脱号和制表符
sed 's/^\s//'
# 将行折叠为 $MAXWIDTH 个字符。
fold -w $MAXWIDTH

# 此脚本受文章启发。
```

# 示例 A-5. copy-cd: 拷贝数据 CD

```bash
#!/bin/bash
# copy-cd.sh: copying a data CD
CDROM=/dev/cdrom # CD ROM 设备
OF=/home/bozo/projects/cdimage.iso # 输出文件
BLOCKSIZE=2048
SPEED=2 # 如果支持，可以使用更高的速度。

echo; echo "插入源 CD，但*不要*挂载它。"
echo; echo "准备好后按回车键。"
read ready # 等待输入，ready 不可用
echo; echo "正在将源 CD 拷贝到 $OF。"
echo; echo "这可能需要一段时间。请耐心等待。"

dd if=$CDROM of=$OF bs=$BLOCKSIZE # 原始设备拷贝。
echo; echo "移除数据 CD。"
echo; echo "插入空白 CDR。"
echo; echo "准备好后按回车键。"
read ready # 等待输入，ready 不可用

echo; echo "正在将 $OF 拷贝到 CDR。"
cdrecord -v -isosize speed=$SPEED dev=0 $OF
# 使用了 Joeschilling 的 "cdrecord" 包（参见其文档）。
# http://www.fokus.GMD.de/nthp/employees/schilling/cdrecord.html

case "$answer" in
[yY]) rm -f $OF
    echo "$OF erased."
*)
    echo "$OF not erased.";
esac

echo

# 练习：

# 修改上面的 "case" 语句使其也接受 "yes" 和 "Yes" 作为输入。

exit 0
```

# 示例 A-6. Collatz 序列（碰撞猜想）

```bash
#!/bin/bash
# collatz.sh
# --------------------------------------------------
# 臭名的“hallstone”或 Collatz 序列。
# --------------------------------------------------
# 1) 从命令行获取整数“种子”。
# 2) NUMBER <-- 种子
# 3) 打印 NUMBER：
# 4) 如果 NUMBER 是偶数，除以 2；或者
# 5) 如果是奇数，乘以 3 并加 1。
# 6) NUMBER <-- 结果
# 7) 回到 3（循环指定的迭代次数）。

# 该理论是：每一个序列，
# 无论初始值有多大，
# 最终都会稳定在循环“4,2,1...”周期中，
# 即使在经历了大范围数值的波动之后。

# 这是“迭代”的一个实例，
# 这种操作将输出反馈回输入中。
# 有时结果是一个“混沌”序列。

ARGS=1
E_BADARGS=65

if [ $# -ne $ARGS ];    # 需要一个种子数字。
then
    echo "Usage: $0 NUMBER"
    exit $E_BADARGS
fi

MAX_ITERATIONS=200
# 对于较大的种子数字 (>32000)，请增加 MAX_ITERATIONS。

h=$1
# 种子
echo
echo "C($1) --- $MAX_ITERATIONS 次迭代"
echo

for ((i=1; i<=MAX_ITERATIONS; i++))
do
    echo -n "$h"
    #
    let remainder = h % 2
    if [ "$remainder" -eq 0 ]; then # 是偶数吗？
        let "h /= 2"          # 除以 2。
    else
        let "h = h*3 + 1"    # 乘以 3 并加 1
    fi

    COLUMNS=10 # 每行输出 10 个值。
    let "line_break = i % $COLUMNS"
    if [ "$line_break" -eq 0 ]; then
        echo
    fi

done
echo

# 关于此数学函数的更多信息，
# 请参阅 Pickover 的《Computers, Pattern, Chaos, and Beauty》，第 185 页及以后，
# 见参考文献列表。

exit 0
```

# 示例 A-7.-: 计算两个日期之间的天数

```bash
#!/bin/bash

# days-between.sh: 计算两个日期之间的天数。

# 用法：./days-between.sh [M/M][D/YYYY] [M/M][D/YYYY]

ARGS=2 # 两个命令行参数。

E_PARAM_ERR=65 # 参数错误。

REFYEAR=1600 # 参考年份。

CENTURY=100
DIY=365
ADJ_DAY=366 # 针对闰年+分数调整。

MIY=12
DIM=31
LEAPC=4

MAXRETVAL=256 # 函数允许的最大
# 正数返回值。

diff= # 声明日期值的全局变量。
value= # 声明绝对值的全局变量。
day= # 日、月、年的全局变量。
month= # 日、月、年的全局变量。
year= # 日、月、年的全局变量。

Param_Error () # 命令行参数错误。
{
echo "Usage: $0 [M/M][D/YYYY] [M/M][D/YYYY]"
echo "(日期必须在 1600/1/3 之后)"
exit $E_PARAM_ERR
}

ParseDate () {
  # 从命令行参数解析日期。
  month=${1%%/*}
  # 日和月。
  day=${1#*/}
  let year = `basename $1`  # 不是文件名，但工作原理一样。
}

check_date () {
  # 检查传递的无效日期。
  [ "$day" -gt "$DIM" ] || [ "$month" -gt "$MIY" ] || [ "$year" -lt "$REFYEAR" ] && Param_Error "数值无效时退出脚本"
  # 使用“或-与列表”
  # 练习：实现更严谨的日期检查。
}

strip_leading_zero () {
  # 最好去掉日/或或月中可能的前导零(s)
  val=${1#0}
  # 否则 Bash 将它们解释为
  return $val  # 八进制值 (POSIX.2, sect.2.9.2.1)。
}

day_index () {
  # 斯斯公式：
  # 从 1600 年 1 月 3 日到传入参数的日的天数。
  day=$1
  month=$2
  year=$3

  let "month = $month - 2"

  if [ "$month" -le 0 ]; then
    let "month += 12"
    let "year -= 1"
  fi

  let "year -= $REFYEAR"
  let "index = $year + $year / $CENTURY"
}

let Days = $DAY*$year + $year/LEAPC - $index + $year/$LEAPC + $ADJ_DAY*$month/$month/

# 有关此算法的深度解释，请参见
# http://today-t-online.de/home/berndt.schwerdtfeger/cal.htm

if [ "$Days" -gt "$MAXRETVAL" ]; then
  # 则改为负值
  let "dindex = 0 - $Days"
else
  let "dindex = $Days"
  # 该值可以从函数返回。
fi

return $dindex
}

calculate_difference () {
# 天数之间的差异。
{
var= # 存储当前代数。
generation=0 # 初始化代数。
let "cells" = $ROWS * $COLS
# 单元格数量。

declare -a initial ## 包含单元格的数组。

declare -a current
```

# 附录 A. 贡献脚本

```bash
display ()
{
alive=0    # 活跃单元格数量。
# 初始为零。

  declare -a arr
  arr=(echo "$1")    # 将传递的参数转换为数组。
  element_count=${#arr[@]}
  local i
```



# 高级 Bash 脚本指南

## 代码片段 1

```bash
  local rowcheck

  for (i=0; i<element_count; i++))

  do

    # 每行插入换行

    let rowcheck = $i % ROWS

    if [ "$rowcheck" -eq 0 ];

    then

      echo

      echo -n " "    # 缩进。

    fi

  cell=${arr[i]}

  if [ "$cell" = . ]

  then

    let alive = 1

  fi

  echo -n "$cell" | sed -e 's/_/ /g'

  # 数组并将下划线替换为空格。

  done

  return

}

IsValid ()    # 测试单元坐标是否有效。

{

  if [ -z "$1" -o -z "$2" ]    # 缺少强制参数？

  then

    return FALSE

  fi

  local row

  local lower_limit=0

  local upper_limit

  local left

  local right

  let "upper_limit" = $ROWS * $COLS - 1  # 单元格总数。

  if [ "$1" -lt "$lower_limit" -o "$1" -gt "$upper_limit" ]

  then

    return FALSE    # 越数组边界。

  fi

}
```

## 代码片段 2

```bash
row=$(( $row * $ROWS ))

let $left = $row + $COLS # 左边界。

let $right = $left + $COLS - 1 # 右边界。

if [ "$1" -lt "$left" -o "$1" -gt "$right" ]

then

    return $FALSE # 越了行边界。

fi

return $TRUE # 有效坐标。

}

nIsAlive () # 测试单元格是否存活。

{

    # 接收数组、单元格编号、单元状态作为参数。

    GetCount "$1" $2 # 获取邻域内的存活单元数量。

    local nhbd=$

    if [ "$nhbd" -eq "$BIRTH" ] # 在任何情况下存活。

then

        return $ALIVE

    fi

    if [ "$3" = "." -a "$nhbd" -eq "$SURVIVE" ]

then

        return $ALIVE # 仅在之前存活时存活。

    fi

    return $DEAD # 默认。

}

Count () # 统计通过单元格邻域内的存活单元。

{

    # 两个参数

    # $1 存放数组的变量

    # $2) 单元格编号

    local cell_number=$2

    local array

    local top

    local center

    local bottom

    local r

    local row

    local i

    local t_top

    local t_cen

    local t_bot

    local count=0

    local ROW_NHBD=3

    array=( `echo "$1"` )

    let $top = $cell_number - $COLS - 1 # 设置单元编号。

    let $center = $cell_number - 1

    let $bottom = $cell_number + $COLS - 1

    let $r = $cell_number / $ROWS
```

## 代码片段 3

```bash
for ((i=0; i<$ROW_NHBD; i++)) {

  # 从左到右遍历。

  let t_top = $top + $i

  let t_cen = $center + $i

  let t_bot = $bottom + $i

  let row = $r # 统计邻域中心行。

  IsValid $st_row # 有效单元格位置？

  if [ $? -eq "TRUE" ]

then

    if [ ${array[$st_cen]} = "$ALIVE1" ] # 存活吗？

    then

      let count += 1 # 是？

      增加计数器。

    fi

  fi

  fi

  let row = $r - 1 # 统计顶行。

  IsValid $st_top $row

  if [ $? -eq "TRUE" ]

then

    if [ ${array[$st_top]} = "$ALIVE1" ]

    then

      let count += 1

    fi

  fi

  let row = $r + 1 # 统计底行。

  IsValid $st_bot $row

  if [ $? -eq "TRUE" ]

then

    if [ ${array[$st_bot]} = "$ALIVE1" ]

    then

      let count += 1

    fi

  fi

if [ ${array[$cell_number]} = "$ALIVE1" ]

then

  let count -- 1 # 确保测试对象本身

  # 不被计数。

fi

return $count

}

next_gen () # 更新代数数组。

local array

local i=0

array=( "$1" ) # 将传递参数转换为数组。

while [ $i -lt ${#array[@]} ]

do

  IsAlive "$1" ${array[$i]} # 存活吗？

  if [ $? -eq "TRUE" ]

then

    # 如果存活，则

    array[$i]=. # 用点表示单元格。

  else

    array[$i]="" # 否则用下划线

    #（稍后会被空格）

  fi

  let i += 1

done

# generation += 1 # 增加代数计数

# 设置传递给 "display" 的变量。

avar="${array[@]}" # 将数组转换回字符串。

display "$avar" # 显示它。

echo; echo

echo "Generation --$generation"

if [ $generation -eq 0 ];

then

    echo "提前退出：没有更多存活单元了！"

    exit $ALIVE # 没必要继续

fi

# 如果有存活单元。

}
```

## 主程序流程

====================================

```bash
# main()
# 使用启动文件加载初始数组。
initial=$(cat "$startfile" | sed -e '#.*d' | tr -d '\n' |
sed -e 's/\./g' -e 's/_/g') # 删除包含 # 注释的行。
# 移除换行并在元素间插入空格。

clear # 清屏。

echo # 标题
echo "=================="
echo "$GENERATIONS generations of"
echo "\"Life in the Lane\""
echo "=================="

# 显示第一代。
Gen0="${initial[0]}"
display "$Gen0" # 显示。
echo
echo "Generation --$generation"
```

--------------------------------

```bash
let generation += 1 # 增加代数计数。
# 显示下一代。
Cur="${initial[@]}"
next_gen "$Cur" # 显示。

# 后续代数的循环。
while [ $generation -le $GENERATIONS ]
do
  Cur="$avar"
  next_gen "$Cur" # 显示。
  let generation += 1
done
==================

exit 0

# 如果有存活单元。
```

## 示例脚本

```bash
SITE=`domainname`.toronto.edu
# ==> `domainname` 类似于 'hostname'
# ==> 可能会将其重写为参数以供通用用途。

usage="Usage: $0 [-h remotehost] [-d remotirectory]... [-f remfile:localfile] ... \
  [-c localdirectory] [-m filename] [-v]"
ftpflags="i -n*"
varflag=""
set x="# 所以我们在 -m* 中使用了通配符"
set x 'getopts d:ic:f:'
if [ $? -ne 0 ]; then
    echo "$usage"
    exit 65
fi
shift
trap 'rm -f "$TMPFILE"; exit 0 1 2 3 15' EXIT
echo "user anonymous ${USER-gnu}@${SITE}" > ${TMPFILE}
# ==> 添加引号（在复杂的 echo 中建议使用）
echo binary >> ${TMPFILE}
for i in $@
do
    case $i in
        -v) varflag=-v; echo hash >> ${TMPFILE}; shift;
        -h) remothost=$2; shift 2;
        -d) echo cd $2 >> ${TMPFILE};
            if [ "$varflag" != "$x" ]; then
                echo passwd >> ${TMPFILE};
            fi;
            shift 2;
        -c) echo cd $2 "$2" >> ${TMPFILE}; shift 2;
        -f) fi-expr="$2" = "([^[::]]**"; f2="$2" = "[[::]]*(:.+)"
            echo get $($f2) >> ${TMPFILE}; shift 2;
        *) break;
    esac
done
if [ $# -ne 0 ]; then
    echo $usage
    exit 65 # ==> 改为 "exit 2" 以符合标准。
fi
if [ "$varflag" != "$x" ]; then
    ftpflags="${ftpflags}-v"
fi
if [ "$remhost" = "" ]; then
    remotep=prep.ai.mit.edu
    # ==> 重写为你喜爱的 ftp 站点。
fi
echo quit >> ${TMPFILE}
# ==> 所有命令已保存在模板中。

tftp ${ftpflags} ${remhost} < ${TMPFILE}
# ==> 现在，临时文件由 ftp 批量处理。

rm -f ${TMPFILE}
# ==> 最后，删除模板（你可能希望将其复制到日志文件中）。

# ==> 练习：
# ==> 1) 添加错误检查。
# ==> 2) 添加功能（bells & whistles）。
```

## 附录 A 贡献脚本

### 示例 A–12. 密码：生成随机 8 字符密码

`Antek Sawicki` 创建了以下脚本，该脚本非常巧妙地使用了第 9.3 节讨论的参数替换操作符。

```bash
#!/bin/bash
# !/bin/bash2 在旧版机器上使用。
# 可能需要这样调用：
# bash 2.x 随机密码生成器，由 Antek Sawicki 提供 <tenox@tenox.tc,
# 他慷慨地允许文档作者在此处使用。
# --> 文档作者添加的注释 -->

MATRIX="0123456789ABCDEFGHIJKQRSTUVWXYZabcdefghijklmmnopqrstuvwxyz"
LENGTH=${#MATRIX}

while [ $n -le 1 ]; do
# - 是“默认替换”操作符。
# 记住如果 'n' 尚未初始化，则将其设置为 1。
do
  PASS=$SPASS${($RANDOM%${#MATRIX})):1}
  # --> 非常聪明，但很复杂。

  # --> 从最内层嵌套开始...
  # --> ${#MATRIX} 返回数组 MATRIX 的长度。
  # --> ${RANDOM%${#MATRIX}} 返回 1 到
  # 以及 MATRIX 长度 - 1 之间的随机数。

  PASS=$SPASS{($RANDOM%${#MATRIX})):1}
  # --> 返回随机位置的 MATRIX ，长度为 1。
  # --> 查看第 3.3 节中的 (pos:len) 参数替换。
  # 以及后续示例。
  PASS=$PASS... 仅仅将剩余部分接到之前的 PASS（拼接）。
  # --> 为了更清晰地可视化，取消下面注释
  # --> echo "$SPASS"
  # --> 看到 PASS 的构建，
  # 每次循环处理一个字符。
  let n+=1
  # --> 增加 'n' 以进行下次。
done

echo "$SPASS"

# --> 或者，重定向到文件，根据需要。
```

`James R. Vanandt` 贡献了此脚本，它使用了引号和转义。

### 示例 A–13. 使用命名管道进行每日备份

```bash
#!/bin/bash
# ==> 由 James R. Vanandt 创建，并获得了许可。

# ==> 文档作者添加的注释。

HERE=$(uname -n)  ==> hostname
THERE-bilbo
echo "开始备份到 $(date +%r)"
# ==> date +r 返回 12 小时格式，例如 "08:34 PM"。
# 确保 /pipe 是管道而不是文件
rm -f /pipe
mkfifo /pipe
# ==> 创建“命名管道”，名为 "pipe"

# ==> 'ssh' 执行命令（远程登录）。
su uyz -c "ssh $HERE <home/uyz/$HERE.tar.gz>" /pipe
# ==> 使用命名管道在进程之间进行通信：
# ==> 'tar' 写入 /pipe，'ssh' 从 /pipe 读取。

# 结果备份了主目录，
# 向下。
# ==> 在这种情况下使用“命名管道”的优势是什么？
# 相比于“匿名管道”，带有
# ==> 匿名管道在这里有效吗？

exit 0
```

`Stephane Chelas` 贡献了以下脚本以演示生成数字（这需要数组）。

### 示例 A–14. 使用取模操作符生成质数

```bash
#!/bin/bash

# primes.sh: 生成质数，不使用数组。

# 由 Stephane Chelas 贡献。

# 这个没有使用经典的埃拉托尼筛（Eratosthenes）算法，

# 而是使用更直观的方法测试每个候选数（因数），使用取模操作符。

# 过滤掉非质数。

LIMIT=1000

Primes()

  (( n = $1 + 1 ))

  # 增加到下一个整数。

  shift

  # 列表中的下一个参数。

  echo -n=$n

  if (( n == LIMIT ))

  then

    echo $*

    return

  fi

  for i; do

    echo -n=$n $i

    (( n % i == 0 )) && continue

    Primes $n

  return

done

Primes 1

# "i" 被设置为之前的 n 值

# 优化。

# 循环内部递归。

# 循环外部递归。

# 连续累积位置参数。

# 是质数的积累列表。

# 取消第 17 和第 25 行看看发生了。

#比较此生成质数的算法速度与 primes.sh。

# 练习：不使用递归重写此脚本以提高执行速度。
```

`Jordi Sanelas` 允许使用他的优雅 `tree` 脚本。

### 示例 A–15. 显示目录树



```bash
#!/bin/sh
# tree 由 Jordi Sanelas 创建，邮箱：mikaku@arrakis.es
# 版本：1.0
# 下一个版本：1.1

search () {
  for dir in $(echo *
  # 'echo *' 列出工作目录下的所有文件，不换行。
  # 效果类似于 for dir in *
  # 但 dir in 'echo *' 将无法处理带空格的文件名。
  do
    if [ -d "$dir" ]; then # 如果是目录 (-d)
      zz=0 # 变量，跟踪目录级别。
      while [ $zz -le $depth ]; do # 嵌套循环。
        echo -n "| " # 显示垂直连接符，
        zz=$((zz+1)) # 增加2 个空格且不留空行以便缩进。
      done
      if [ -L "$dir" ]; then # 如果是符号链接...
        echo "---$dir" | ls -ld "$dir" | sed 's/^/  /'
        # 显示头部和目录名，但... 显示详细列表的日期/时间。
      else
        echo "---$dir" # 显示水平连接符...
        # 并打印目录名。
        if cd "$dir"; then # 如果进入子目录...
          depth=$((depth+1)) # 增加深度。
          search # 函数递归。
          numdirs=$((numdirs+1)) # 增加计数。
        fi
      fi
    fi
  done
    cd .. # 返回上一级目录。
    if [ $depth -eq 0 ]; then # 如果 depth = 0（返回 TRUE)...
      swfi1=1 # 设置标记显示搜索完成。
    fi
    depth=$((depth-1)) # 减少深度。
  done
}
# - 主 -
if [ $# -eq 0 ]; then
  cd "$PWD"
  cd "$PWD" # 脚本无参数，使用当前工作目录。
else
  cd $1 # == 否则，进入指定的目录。
fi
echo "初始目录 = $PWD"
swfi0=0 # 搜索结束标记。
deep0=0 # 列表深度。
numdirs0=0
zz0=0
while [ $swfi0 -ne 1 ]; # 当标记未设置...
  search # 在初始化变量后调用函数。
done
echo "目录目录 = $numdirs"

exit 0

# ==> 挑战：尝试弄清楚脚本是如何工作的。

Noah Friedman 允许使用此字符串脚本，它基本上实现了一些 C 库的字符串处理函数。

## 附录 A–16. 字符串函数：C 风格字符串函数

```bash
#!/bin/bash
# string.bash -- bash 模拟 string(3) 库程序

# 作者: Noah Friedman <friedman@prep.ai.mit.edu>
# => 在此文档中使用已获得本人许可。
# 创建于: 1992-07-01
# 最后修改: 1993-09-29
# 公有领域

# 由 Chet Rame 转换为 bash v2 语法

# 注释：
# 代码：

#:doc strcat:
# 用方法：strcat s1 s2

# strcat 将变量 s2 的值追加到变量 s1 之后。

# 示例：
# a="foo"
# b="bar"
# strcat a b
# echo $a
# > foobar

#end docstring
###;;autoload --> 函数的自动加载已注释。
function strcat () {
    local s1_val s2_val

    s1_val=${1} # 间接变量扩展
    s2_val=${2}
    eval "$s1='${s1_val}\${s2_val}'*"
    # => eval s1='${s1_val}\${s2_val}' 避免了问题，
    # => 如果其中一个变量包含单引号。
}

#:doc strcat
# 用方法：strcat s1 s2 n

# 行结构，strcat 从变量 s2 的值中最多追加 n 个字符。
# 如果变量 s2 的值少于 n 个字符，则全部复制。在标准输出上显示结果。

# 示例：
# a=foo
# b=barbaz
# strcat a b 3
# echo $a
# > foobar

#end docstring:
###;;autoload
function strcat {
    local s1="$1"
    local s2="$2"
    local -i n="$3"
    local s1_val s2_val

    s1_val=${!s1} --> 间接变量扩展
}
```

### 附录 A. 贡献脚本

355

# 高级 Bash 脚本指南

```bash
:docstring strcmp
# 方法：strcmp s1 s2
# strcmp 比较其参数并返回一个小于、等于或大于零的整数，
# 取决于字符串 s1 在字典序上是小于、等于还是大于字符串 s2。
#:end docstring
```

```bash
###;autoload
function strcmp() {
    [ "$1" = "$2" ] && return 0

    [ "$1" != "$2" ] > /dev/null || return -1
    return 0
}
```

```bash
:docstring strcmp
# 方法：strcmp s1 s2 n
# 类似于 strcmp，但它通过检查最多 n 个字符来做比较
# (n 小于或等于 0 时视为相等）。
#:end docstring
```

```bash
###;autoload
function strcmp() {
    if [ -z "$3" -o "$3" -le "0" ]; then
        return 0
    fi

    if [ ${3} -ge ${#1} -a $3 -ge ${#2} ]; then
        strcmp "$1" "$2"
        return $?
    else
        s1=${1:0:$3}
        s2=${2:0:$3}
        strcmp $s1 $s2
        return $?
    fi
}
```

```bash
:docstring strlen
# 方法：strlen s
# strlen 返回字符串字面量 s 中的字符数量。
#:end docstring
```

```bash
###;autoload
function strlen ()
```

```bash
eval echo "\${$(1)}"

# 返回作为参数传递的变量名
 对应的值的长度
```

```bash
:docstring strcspn
# 方法：strcspn s1 $s2
#
# Strcsp 返回字符串 s1 的最大前缀段的长度，
# 该段落完全由字符串 s2 中的字符组成。
#:enddocstring
###;autoload
function strcspn ()
{
    # 取消 IFS 允许允许空白符被视为普通字符处理。
    local IFS=
    local result="${1%%[!${2}]*"
    echo "$result"
}
```

```bash
:docstring strcspn
# 方法：strcspn s1 $s2
#
# Strcsp 返回字符串 s1 的最大前缀段的长度，
# 该段落完全由不在字符串 s2 中的字符组成。
#:enddocstring
###;autoload
function strcspn ()
{
    # 取消 IFS 允许空白符被视为普通字符处理。
    local IFS=
    local result="${1%%[!${2}]*"
    echo "$result"
}
```

```bash
:docstring strstr
# 方法：strstr s1 s2
#
# Strstr 返回从 s1 中字符串 s2 第一次出现开始的子字符串，
# 如果 s2 不在字符串中出现，则返回空。如果 s2 指向
# 长度为零的字符串，strstr 输出空。
#:enddocstring
```

```bash
###;autoload
function strstr ()
{
    # 如果 s2 指向长度为零的字符串，strstr 输出
    [ $2 -eq 0 ] && { echo "$1"; return 0; }

    # 如果 s2 不在 s1 中出现，strstr 不输出内容
    case "$1" in
        *) return 1;
    esac

    # 使用模式匹配代码剥离匹配项
    # 之后的部分
```

357

# 高级 Bash 脚本指南

```bash
first=$(1/$2*)
# 然后剥离字符串中不匹配的部分
echo "${1#first}"

:docstrtok:
# 方法：strtok s1 s2
# strtok 将字符串 s1 转换为由一个或多个 token 组成
# 由来自 s2 的更多字符分隔。第一次调用
#（带有非空字符串 s1）会将由第一个 token 组成的字符串
# 输出到标准输出。函数在调用之间跟踪其在字符串
# 中的位置，因此使用第一个参数进行的后续调用
# 将处理该 token 之后的字符串。通过这种方式，
# 后续调用将处理字符串直到没有剩余 token。
# 分隔符字符串可能与调用不同。当 s1 中没有剩余 token 时，，向标准输出输出空值。
#:endstrtok;
```

```bash
###;;autoload
function strtrunc() {
:docstrunc:
# 方法：strtrunc n s1 ($s2) (...)
# 用于 strcmp 等许多函数以截断参数进行比较。
# 在标准输出上输出每个字符串 s1 ... 的前 n 个字符。
#:endstrunc;
```

```bash
###;autoload
function strtrunc() {
    local n="$1"
    local s1="$2"
    local s2="$3"
    local s1_val s2_val
    s1_val=${s1:0:$n}
    if [ -n "$s2" ]; then
        s1_val="${s1_val}${s2}"
    fi
    echo "$s1_val"
}
```

```bash
# 这是一个演示面向对象编程的脚本
# 类似于 C++ 的类声明
#!/bin/bash
# obj-oriented.sh: 脚本中的面向对象编程。

person.new()
{
    local obj_name=$1 name=$2 firstname=$3 birthdate=$4
    # 模拟方法
    # 构造
    eval "$obj_name.set_name() {
        eval \$obj_name.get_name() {
            echo \"\$name\"
        }
    }"
    eval "$obj_name.set_firstname() {
        eval \$obj_name.get_firstname() {
            echo \"\$firstname\"
        }
    }"
    eval "$obj_name.set_birthdate() {
        eval \$obj_name.get_birthdate() {
            echo \"\$birthdate\"
        }
    }"
    eval "$obj_name.get_age() {
        echo \$(( \$(date +%s) - \$birthdate )) / 3600 / 24 / 365
    }"
    eval "$obj_name.show_birthdate() {
        echo -d \"1/1970 0:0:\$1 GMT\"
    }"
}

# 示例：创建 "person.new" 的实例（实际上是向函数传递参数）。

person.new self Bozeman Bozo 1012743

# 测试所有方法
self.get_firstname    # Bozo
self.get_name         # Bozeman
self.get_age          # 28
self.get_birthdate    # 1012743
self.show_birthdate   # Sat Mar 17 20:13:33 MST 1973
```

```bash
echo
# typeset -f
# 查看创建的函数（小心，它会超出屏幕）。
exit 0
```

## 附录 B. Sed 和 Awk 快速入门

这是对 `sed` 和 `awk` 文本处理工具的非常な介绍。在这里我们只处理基础知识，但对于理解 shell 脚本中简单的 `sed` 和 `awk` 构造已经足够。

- `sed`：非交互式文本编辑器
- `awk`：具有类似 C 语法的字段型模式处理语言

尽管有许多差异，这两个工具具有相似的调用语法，都使用正则表达式，但默认都从 `stdin` 读取输入，并都输出到 `stdout`。这些是良好的 UNIX 工具，它们协作良好。一个工具的输出可以管道到另一个工具，它们的结合能力赋予了 shell 一些类似于 Perl 的功能。

# 高级 Bash 脚本指南

`Sed` 通过传递给它的地址范围来确定对输入内容中的哪些行进行操作。
[65] 你可以通过行号或匹配模式来指定此地址范围。例如，`3d` 表示删除输入的第 3 行，而 `/windows/d` 则告诉你想删除输入中所有包含 "windows" 匹配项的行。

在 `sed` 工具集的所有操作中，我们将主要关注三个最常用的操作。这些是打印（`stdout`）、删除（deletion）和替换（substitution）。

### 表 B–1. 基础 sed 运算符

| 运算符 | 名称 | 效果 |
|---|---|---|
| `[address-range]/p` | 打印 | 打印[指定的地址范围] |
| `[address-range]/d` | 删除 | 删除[指定的地址范围] |
| `s/pattern1/pattern2/` | 替换 | 将行中第一个 `pattern1` 替换为 `pattern2` |
| `[address-range]/s/pattern1/pattern2/` | 替换 | 在地址范围内，将行中第一个 `pattern1` 替换为 `pattern2` |
| `[address-range]/y/pattern1/pattern2/` | 转换 | 将 `pattern1` 中的任何字符替换为 `pattern2` 中对应的字符，地址范围（等同于 `tr`） |
| `g` | 全局 | 对输入中每个匹配行的每一个模式匹配项进行操作 |

![](img/1ce1edffaa36e4f698a85430e71c6d3b_366_0.png)

除非在替换命令后附加 `g`（全局）运算符，否则替换仅作用于每行中模式匹配的第一个实例。

在命令行 `-e` 和在 shell 脚本中，`sed` 操作可能需要引号和某些选项。

```bash
sed -e '^$/d' $filename

# -e 选项导致下一个字符串被解释为编辑指令。
# (如果只向 "sed" 传递单个指令，则 "-e" 是可选的)。
# 字符串引号 (''') 保护了指令中的正则表达式（RE）字符，
# 防止被脚本主体重新解释为特殊字符。
# (这为指令的 RE 扩展留给 sed 使用。)
# 对文件 $filename 的文本进行操作。
```

# 高级 Bash 脚本指南

`Sed` 使用 `-e` 选项来指定后续字符串是一个指令或一组指令。如果字符串中只包含一个指令，可以省略此选项。

```bash
sed -n '/xzy/p' $filename

# -n 选项告诉 sed 仅打印匹配模式的行。
# 否则，所有输入行都会被打印。
# 这里不需要 -e 选项，因为只有一个编辑指令。
```



## 表 B–2. 示例

| 记法 | 效果 |
|---|---|
| `8d` | 删除输入的第 8 行。 |
| `/^$/` | 删除所有空行。 |
| `1,/` | 从输入开始到第一个空行（包含空行）。 |
| `/Jones/p` | 仅打印包含 "Jones" 的行（使用 `-n` 选项）。 |
| `s/Windows/Linux/` | 将每行输入中找到的 "Windows" 替换为 "Linux"。 |
| `s/BSOD/stability/g` | 将每行输入中找到的 "BSOD" 替换为 "stability"。 |
| `s/ */` | 删除每行末尾的所有空格。 |
| `s/00*/0g` | 将所有连续的零序列压缩为单个零。 |
| `/GUI/d` | 删除所有包含 "GUI" 的行。 |
| `s/GUI//` | 删除所有 "GUI" 实例，保持每行的其余部分完整。 |

将一个零长度字符串替换为另一个，等同于删除输入行中的该字符串。这会保持行的其余部分完整。对以下行应用 `s/GUI//`：

> The most important parts of any application are its GUI and sound effects results in
> The most important parts of any application are its and sound effects

反斜杠作为替换字符时表示换行符。在一种特殊情况下，替换表达式在下一行继续。

```
s/^ *//g
```

此替换将行首空格替换为换行符。最终结果是将段落缩进替换为段落之间的空行。

### 附录 B. Sed 和 Awk 快速入门

# 高级 Bash 脚本指南

地址范围后跟一个或多个操作可能需要开合花括号，并带有适当的换行。

```
/[0-9A-Za-z],/^$\{

  $/d

}
```

这只删除第一组连续的空行。这可能对于使文本文件单行间距有用，但保留段落之间的行。

![](img/1ce1edffaa36e4f698a85430e71c6d3b_368_0.png)

使文本文件双倍行行的快速方法是 `sed G filename`。

关于 shell 脚本内部的演示示例，请参见：

1. 示例 34–1
2. 示例 34–2
3. 示例 12–2
4. 示例 A–3
5. 示例 12–12
6. 示例 12–20
7. 示例 A–10
8. 示例 A–15
9. 示例 12–24
10. 示例 10–9
11. 示例 12–31
12. 示例 A–2
13. 示例 12–7
14. 示例 12–9
15. 示例 A–8

对于 `sed` 的更广泛处理，请参考[参考文献]。

## B. Awk

`Awk` 是一种功能完备的语言，受到 C 语言的启发。它使用字段分隔符来处理数据。`Awk` 使用模式-动作对来处理数据，当模式匹配成功时，执行相应的动作。`Awk` 具有许多内置变量，如 `$0`（当前行）、`NR`（行数）、`NF`（字段数）和 `FS`（字段分隔符）。`Awk` 是一个强大的文本处理工具，非常适合数据分析和报告生成。

`Awk` 脚本通常具有以下结构：

```awk
BEGIN { ... }
...
END { ... }
```

其中 `BEGIN` 块在处理任何行之前执行一次，`END` 块在处理完所有行后执行一次。中间的部分在每行匹配到模式时执行。

```awk
awk '{ print $0 }' file
```

这会打印文件的每一行。

```awk
awk '{ print $1 }' file
```

这会打印每行的第一个字段。

```awk
awk '/pattern/ { print $0 }' file
```

这会打印包含 "pattern" 的行。

```awk
awk '$3 > 10 { print $0 }' file
```

这会打印第三字段大于 10 的行。

```awk
awk -F: '{ print $2 }' file
```

这使用冒号作为字段分隔符，并打印第二个字段。

`Awk` 还可以执行数学运算，例如：

```awk
awk '{ sum += $1 } END { print sum }' file
```

这会计算第一列之和并在最后输出。

`Awk` 是处理结构化数据的强大力器，其灵活的语法胜任复杂的文本处理任务。

# 高级 Bash 脚本指南

按照习惯，命令从 `fd 0 (stdin)` 读取输入，将正常输出打印到 `fd 1 (stdout)`，并将错误输出打印到 `fd 2 (stderr)`。如果这些文件描述符 (`fd`) 中的一个没有打开，你可能会遇到问题：

```bash
bash cat /etc/passwd >&-
cat: standard output: bad file descriptor
```

例如，当 `xterm` 运行时，它会先进行初始化。在运行用户的 shell 之前，`xterm` 会打开终端设备（`/dev/pts/n` 或类似设备）三次。

此时，`Bash` 继承了这三个文件描述符，而由 `Bash` 运行的命令（子进程）也会按继继承这些符，除非你对命令进行了重定向。重定向意味着将其中一个文件描述符重新分配给另一个（通过管道或任何类似机制）。文件描述符可以针对某个命令、子 shell、`while` 或 `if` 循环进行局部重新分配，也可以全局地在 shell 的剩余运行时间内进行重新分配（使用 `exec`）。

`ls > /dev/null` 意味着运行 `ls` 时将 `fd 1` 连接到 `/dev/null`。

```bash
bash exec 2>/dev/null

bash lsof -a p -- -d0,1
COMMAND PID USER FD TYPE DEVICE SIZE NAME
lsof 3621 0u CH 136,1 3 /dev/pts/1
lsof 3620 1u CH 136,1 3 /dev/pts/1
lsof 3620 2w CH 136,1 120 /dev/null
```

```bash
bash bash -c 'lsof -a p -- -d0,1,2' | cat
COMMAND PID USER FD TYPE DEVICE SIZE NAME
lsof 3709 0u CH 136,1 3 /dev/pts/1
lsof 3709 1u CH 136,1 3 /dev/pts/1
lsof 3709 2w CH 136,1 3 /dev/pts/1
```

```bash
bash echo "$(lsof -a p -- -d0,1,2)" >&6
COMMAND PID USER FD TYPE DEVICE SIZE NAME
lsof 4226 0u CH 136,1 3 /dev/pts/1
lsof 4226 1w FIFO 0,0 7520 pipe
lsof 4226 2w FIFO 0,0 7520 pipe
```

这种方法适用于各种类型的重定向。

# 练习：分析以下脚本。

```bash
#! /usr/bin/env bash
mkfifo /tmp/fifo1 /tmp/fifo2
while read a; do echo "FIFO1: $a"; done < /tmp/fifo1 &
? exec 7 > /tmp/fifo1
exec 8>(while read a; do echo "FD8: $a, to fd7"; done >&7)
```

## 附录 A.I/O 和 I/O 重定向详细介绍

```bash
exec 3>&1
(
  while read a; do echo "FIFO2: $a"; done < /tmp/fifo2 | tee /stderr | tee /dev/4 | tee |
  exec 3> /tmp/fifo2
)
echo 1st, to stdout
sleep 1
echo 2nd, to stderr >&2
sleep 1
echo 3rd, to fd 3 >&3
sleep 1
echo 4th, to fd 4 <&4
sleep 1
echo 5th, to fd 5 >&5
sleep 1
echo 6th, through a pipe | sed 's/.*/PIPE: &, to fd 5/' >&5
sleep 1
echo 7th, to fd 6 <&6
sleep 1
echo 8th, to fd 7 >&7
sleep 1
echo 9th, to fd 8 >&8
) 4>&1 3<-\ | while read a; do echo "FD4: $a"; done 1>&3 5<&- 6<&-
) 5>&1 >3 | while read a; do echo "FD5: $a"; done 1>&3 6<&-
) 6>&1 >3 | while read a; do echo "FD6: $a"; done 3>&-
rm -f /tmp/fifo1 /tmp/fifo2
```

```bash
# 对于每个命令和子 shell，找出哪个 fd 指向什么。
exit 0
```

# 附录 E. 本地化

本地化是一个未文档说明的 `Bash` 特性。

本地化的 shell 脚本将根据系统区域设置（`locale`）定义的语言导出其文本。位于德国柏林的 `Linux` 用户将获得德语脚本输出，而他位于美国马里兰州柏林的表哥将获得来自同一份脚本的英语输出。

要创建一个本地化脚本，请使用以下模板向用户写入所有消息（错误信息、提示信息等）。

```bash
#!/bin/bash
# localized.sh
E_CERROR=65
error() {
  printf "%s" $@ >&2
  exit $E_CERROR
}
```

```bash
cd $var || error "Can't cd to %s." "$var"
read -p $"Enter the value: " var
#
```

```bash
bash -D localized.sh
"Can't cd to %s."
"Enter the value: "
```

这列出了所有本地化文本。`-D` 选项可以在不执行脚本的情况下列出带有 `$` 前缀的双引号字符串。

# 高级 Bash 脚本指南

```bash
# Shell 提示符
#-----------
function fastprompt() {
  unset PROMPT_COMMAND
  case $TERM in
    *term | rxvt)
      PS1="[#h] \W > \u033[0;\u007[h] \w\u007";
    )
    *)
      PS1="[#h] \W > "
  esac
}
```

```bash
function powerprompt() {
  _powerprompt() {
    LOAD=$($uptime | sed -e "s/.*([^^*]*).\1/" -e "s //g")
    TIME=$(date +%H:%M)
  }
  PROMPT_COMMAND=_powerprompt
  case $TERM in
    *term | rxvt)
      PS1="$(cyan)[\TIME]NC\u033[0;\u007[h] \w\u007";
    linux)
      PS1="$(cyan)[\TIME]NC\u033[0;\u007[h] \w\u007";
    *)
      PS1="$(cyan)[\TIME]NC\u033[0;\u007[h] \w\u007";
  esac
}
powerprompt # 这是默认设置 - 可能会慢
# 如果慢，请改用 fastprompt。
```

## 别名（ALIASES）与函数

# 可以认为，这里的某些函数非常占用内存，所以
# 如果你想让它更小量，可以将这些函数转换为脚本。许多函数取自 bash-2 示例。

### 个人别名

```
alias rm='rm -i'
alias cp='cp -i'
alias mv='mv -i'
alias h='history'
alias j='jobs'
alias r='login'
```

## 附录 G. 示例 .bashrc

```bash
alias ..='type -all'
alias .='cd'
alias path='echo -e ${PATH}'
alias background='- -d &'
alias vi='vim'
alias du='du -h'
alias df='df -kh'
# 'ls' 系列（假设你使用的是 GNU ls）
alias ls='--color' # 为文件类型添加颜色
alias lr='sort -r' # 按扩展名排序
alias ks='-S' # 按大小排序
alias la='-Al' # 显示隐藏文件
alias lm='-ai' # 按日期排序
alias tree='tree -Cs' # 'ls' 的良好替代方案
# 定制 'less'
alias more='less'
export PAGER='less'
export LESSOPEN='|usr/bin/lesspipe.sh' # 如果存在 lesspipe.sh 则使用
export LESS='-i -N -Z -g -e -M -X -F -P -t'
# 拼写错误 - 高度个人化
alias xs='cd'
alias vf='cd'
alias moor='more'
alias moew='more'
alias kk='less'
function {
  case $term in
    *rxvt)
      echo -ne "\033];0*"
    *)
  esac
}
# 别名...
alias top='top on $HOST &'
alias make='make $(basename $PWD)'
alias nftp='nftp'
# 函数
function man () {
  man $(basename $PWD) |tr -d .[:digit:]
  man -a "*"
}
function ll() { ls -1 "$*" | grep "^d"; ls -l "$@" 2>&1 | grep -v "^d|total"; }
function emacs() { command emacs -private 2>&1 && disown }
function te() { # emacs/gnuuser 的封装
{
  if [ "$(gnuclient -eval t 2>&1)" == "t" ]; then
    gnuclient -q "$@"
  else
    emacs "$@" &
  fi
}
```

## 文件与字符串相关函数

```bash
function ff() { find -name '*$1*' ; } # 查找文件
function fe() { find -name '*$1*' -exec $2 \; \; } # 查找文件并在其上运行 $2
function fstr() { 在一组文件中查找字符串
if [ "@" -gt 2 ]; then
  echo "Usage: fsstr \"pattern\" [files]"
  return;
fi
SMS=$(tput rmso)
RMS=$(tput smso)
find . -type f -name "${2:-*}" -print | xargs grep -sin "$1" | \
sed "s/$1/$SMS$RMS/g"
}
function cutall() # 剪切文件中最后 n 行，默认 10 行
{
lines=${2:-10}
sed -n -e "1,\${lines}p"
}
function lowercase() { # 将文件名转换为小写
{
  for file; do
    filename=${file##*/}
    case "$filename" in
      *)
        dirname="$filename"
        if [ "$file" != "$dirname" ]; then
          echo "lowercase: $file"
        fi
    esac
  done
}
function swap() { # 交换
{
  local TMPFILE=$1
  mv $1 $2
  mv $2 $TMPFILE
}
```

## 进程/系统相关函数

```bash
function my_ps() { ps -u -o cpu,$mem,command; }
function pp() { ps f; }
function kills() { # 该函数与 'kill' 大致相同，但没有等效对应
local pid=$1
if [ "$#" -lt 1 ] || [#" -gt 2 ]; then
return;
fi
kill $pid
}
function my_ip() { # 获取 IP 地址
{
MY_IP=$(sbin/ifconfig | awk '/inet/ {print $2}')
echo "$MY_IP"
}
function ii() { # 获取当前主机信息
{
MY_IP=$(sbin/ifconfig | awk '/inet/ {print $2}')
echo "$MY_IP"
}
```

## 杂项工具



## 高级 Bash 脚本指南

### 可编程补全 - 从 BASH-2.04 起

```bash
function repeat() { # 重复 n 次命令
  local i max
  max=$1; shift;
  for ((i=1; i<=max; i++)); do
    echo "$2"
  done
}

function ask() {
  echo -n "$@" [y/n]
  read ans
  case "$ans" in
    y*|Y*) return 0 ;;
    *) return 1 ;;
  esac
}
```

如果实际上需要 `bash-2.05` 的某些功能：

```bash
if [ "$BASH_VERSION*" != "2.05" ]; then
  echo 你需要升级到 2.05 版本使用可编程补全
  return
fi

shopt -s extglob
set -o nounset # 否则补全将失败

complete -A hostname rsh telnet rmdir ping
complete -A command nohup exec trace g gdb
complete -A type which
printenv
complete -A export local unset
complete -A variable builtin
complete -A alias unalias
complete -A function function
complete -A user su
complete -A help # 目前与 builtin 相同
complete -A short shopt
complete -A stopped -P '\%%' bg
complete -A job -P '\%%' fg jobs disown
complete -A directory mkdir rmdir
complete -A directory -o default cd
complete -f -d -X '*.gz' gzip
complete -f -o default -X '*.bz2' bzip2
complete -f -o default -X '*.gz' gunzip
complete -f -o default -X '*.bz2' bunzip2
complete -f -o default -X '*.pl*' perl perls1
complete -f -o default -X '*.ps*' gs ghostview ps2pdf ps2ascii
complete -f -o default -X '*.vi*' dvipid select dvitype
complete -f -o default -X '*.+.*' pdf2ps
complete -f -o default -X '*.+(ps)*' gv
complete -f -o default -X '*.txt*' makeinfo texi2divi texi2html texi2pdf
complete -f -o default -X '*.tex*' latex slitex
complete -f -o default -X '*.lyx*'
complete -f -o default -X '*.*(jpg|gif|png|bmp)*' xv image
complete -f -o default -X '*.mp3*' mp3123
complete -f -o default -X '*.ogg*' ogg123
```

#### 通用补全示例

```bash
case "$1" in
  *)
    eval cmd=$1;
    cmd="$1";
esac
```

```bash
COMPRELY=$($cmd --help | sed -e '//|d' -e 's/.*\-\([^*]*\).*/\1/' | \
  grep "$2" | sort -u)
complete -o default -F _universal_func ldd wget bash inc cur
```

#### 自定义 Make 补全

```bash
_make_targets () {
  local mdef make gcmd prev i
  COMPRELY=$($COMP_WORDS[COMP_CWORD])
  prev=$($COMP_WORDS[COMP_CWORD-1])
}
```

# 如果上一个参数是 -f，则返回文件名补全。
# 我们可以在这里变得聪明一点，返回匹配
# * makefile "$prev" Makefile *.mk，取决于任何存在的文件

# 如果我们想要一个选项，则返回可能的 posix 选项
```bash
case "$cur" in
  COMPRELY=$(-e -f -i -k -n -p -q -r -S -t); return 0;
esac
```

# make 在读取 'makefile' 之前会读取 'Makefile'
```bash
if [ -f makefile ]; then
  mdef=makefile
elif [ -f Makefile ]; then
  mdef=Makefile
else
  mdef="*.mk"
fi
```

# 在扫描目标之前，检查是否通过 -f
# 指定了 make 名称
```bash
for ((i=0;i<${COMP_WORDS[$0]}; i++)); do
  if [[ ${COMP_WORDS[$i]} == -*f ]]; then
    eval makefile=$${COMP_WORDS[$i+1]} # 使用 eval 进行波浪扩展
    break
  fi
done
[ -z "$makefile" ] && make=$mdef
```

# 如果我们必须使用 *，我们可以去掉 cut，并使用
# 该单词的匹配项
# 限制为
```bash
if [ -n "$2" ]; then gcmd='grep "$2*"; else gcmd=cat; fi
```

# 测试 -f $makefile 和输入重定向
```bash
COMPRELY=$($cat $makefile 2>/dev/null | awk 'FS=":"' /^\#.*][^]*:/ {print $1} | tr)
```

```bash
complete -F _make_targets -X+'*[.cho]' make pmake
```

### 附录 G. 示例 `.bashrc`

# 高级 Bash 脚本指南

```bash
_configure_func ()
{
    case "$2" in
        *) ;;
        *) return ;;
    esac
    case "$1" in
        \*) eval cmd=$1 ;;;
        *) cmd="$1";;
    esac
}

COMPRELY=$( "$cmd" --help | awk '{if ($1 ~ -.*/) print $1}' | grep "^$2" | sort -u)
complete -F _configure_func configure
```

# cvs (1) 补全
```bash
_cvs ()
{
    local cur prev
    COMPRELY=()
    cur=$(COMP_WORDS[COMP_CWORD])
    prev=$(COMP_WORDS[COMP_CWORD-1])
    if [ $COMP_CWORD -eq 1 ] || [ "${prev:0:1}" = "-" ]; then
        COMPRELY=($0 compgen -w addin commit diff \
            export history import log diff release rtag status \
            tag update' $cur)
    else
        COMPRELY=($0 compgen -f $cur)
    fi
    return 0
}
complete -F _cvs cvs
```

```bash
_killall ()
{
    local cur prev
    COMPRELY=()
    cur=$(COMP_WORDS[COMP_CWORD])
    # 获取进程列表（第一个 sed 求值
    # 处理了已交换的进程，第二个
    # 处理获取进程的基名）
    COMPRELY=($0 /usr/bin/ps -u $USER -o comm | \
        sed -e '1,d' -e 's/[#][]//@' -e 's/.*$##' | \
        awk 'if ($0 ~ /^$cur\/) print $0')
    return 0
}
complete -F _killall killall killps
```

# 本局变量：
# mode:shell-script
# sh-shell:bash
# 结束。

### 附录 G. 示例 `.bashrc` 文件

### 附录 H. 将 DOS 批处理转换为脚本

许多程序员在运行 `DOS` 的 `PC` 上学习脚本的。即使是功能有限的批处理语言也允许编写一些相当强大的脚本和应用程序，尽管它们通常需要大量的补丁和变通方法。偶尔，仍然会有将旧 `DOS` 批处理文件转换为 `shell` 脚本的需求。这通常并不困难，因为 `DOS` 处理文件运算符只是对应 `shell` 脚本选项的有限子集。

#### 表 H–1. 处理文件关键字/变量/运算符及其对应的 shell 等价项

| 处理文件运算符 | Shell 脚本等价项 | 含义 |
|---|---|---|
| `%` | `$` | 命令行参数前缀 |
| `/` | `-` | 命令选项标志 |
| `\` | `/` | 目录路径分隔符 |
| `==` | `=` | (等于)字符串比较测试 |
| `! ==` | `!=` | (不等于)字符串比较测试 |
| `|` | `|` | 管道 |
| `@` | `set +v` | 不回显当前命令 |
| `*` | `*` | 文件名“通配符” |
| `>` | `>` | 文件重定向（覆盖） |
| `>>` | `>>` | 文件重定向（追加） |
| `<` | `<` | 重定向 `stdin` |
| `%VAR%` | `$VAR` | 环境变量 |
| `REM` | `#` | 注释 |
| `NOT` | `!` | 否定后续内容 |
| `NUL` | `/dev/null` | 用于丢弃输出的“黑洞” |
| `ECHO` | `echo` | 回显（`Bash` 中有许多选项） |
| `ECHO.` | `echo` | 空行 |
| `ECHO OFF` | `set +v` | 不回显随后的命令 |
| `FOR %VAR IN (LIST)` | `var in [list];` | "for" 循环 |
| `:LABEL` | `none` (无必要) | 标签 |
| `GOTO` | `none` (使用函数) | 跳转到脚本中的另一个位置 |
| `PAUSE` | `sleep` | 暂停或等待间隔 |
| `CHOICE` | `case` or `select` | 菜单选择 |
| `IF` | `if` | `if`–测试 |
| `IF EXIST FILENAME` | `if -e filename` | 测试文件是否存在 |
| `IF !N` | `if -z "$N"` | 可替换参数 "N" 不存在 |
| `CALL` | `source` (`.dot` operator) | “包含”另一个脚本 |
| `COMMAND /C` | `source` (`.dot` operator) | 包含另一个脚本 |
| `SET` | `export` | 环境变量 |
| `SHIFT` | `shift` | 左移列表 |
| `SGN` | `-lt` `-gt` | 符号 |
| `ERRORLEVEL` | `exit` | 状态 |
| `CON` | `/dev/null` | (标准输入) |
| `PRN` | `/dev0` | 打印设备 |
| `LPT1` | `tty` | 打印设备 |

批处理文件通常包含。转换为 `UNIX` 命令。

#### 表 H–2. DOS 命令及其等价项

| DOS 命令 | UNIX 等价项 | 含义 |
|---|---|---|
| `ASSIGN` | | 赋值 |
| `ATTRIB` | `chmod` | 修改权限 |
| `CD` | `cd` | 切换目录 |
| `CLS` | `clear` | 清屏 |
| `CMP` | `cmp` | 比较 |
| `COPY` | `cp` | 复制 |
| `DEL` | `rm` | 删除 |
| `DIR` | `ls` | 列表 |
| `ERASE` | | 删除 |
| `FIND` | `grep` | 查找 |
| `MD` | | 移动 |
| `MKDIR` | `mkdir` | 创建目录 |
| `MORE` | `less` | 分页 |
| `MOVE` | `mv` | 移动 |
| `PATH` | `$PATH` | 路径 |
| `REN` | | 重命名 |
| `RENAME` | | 重命名 |
| `RD` | | 删除 |
| `RMDIR` | `rmdir` | 删除目录 |
| `SORT` | `sort` | 排序 |
| `TIME` | `date` | 时间 |
| `TYPE` | `cat` | 类型 |
| `XCOPY` | | |
| `CON` | `/dev/null` | (标准输入) |
| `PRN` | `/dev0` | 打印设备 |
| `LPT1` | `tty` | 打印设备 |

批处理文件通常包含。转换为 `UNIX` 命令。

处理文件通常。

### 附录 I. 练习

#### I.1. 分析脚本

检查以下脚本。运行它，然后解释它做了什么。对脚本进行注释，然后用更紧凑、优雅的方式重写。

```bash
#!/bin/bash
MAX=10000
for((nr=1;nr<$MAX; nr++))
do
    let t1 = nr % 5
    if [ "$t1" -ne 3 ];
then
        continue
fi
    let "t2 = nr % 7"
    if [ "$t2" -ne 4 ]
then
      continue
fi
    let "t3 = nr % 9"
    if [ "$t3" -ne 5 ]
then
      continue
fi
    break # 如果你注释掉这一行会发生什么？为什么？
done
echo "Number = $nr"
```

读者发送了以下代码片段。

```bash
while read LINE
do
  echo $LINE
done < "tail -f /var/log/messages"
```



他希望写一个脚本来跟踪系统日志文件 `/var/log/messages` 的变化。遗憾的是，上面的代码块会挂起且没有任何用处。修复它的工作方式（提示：不要重定向循环的 `stdin`），尝试使用管道。

分析示例 A-8，并以更简单、更具逻辑性的风格重新组织它。看看可以消除多少变量，并尝试优化速度以缩短其执行时间。

修改脚本使其接受任何普通的 `ASCII` 文件作为初始“生成”的输入。脚本将首先读取 `$ROW` 个字符，并将元音出现的次数设置为“存活”单元。提示：务必将输入文件中的空格转换为下划字符。

## I.2. 编写脚本

编写脚本来执行以下每项任务。

### 简单

#### 主目录列表

对用户的家目录执行递归目录列表操作，并将信息保存到文件中。压缩该文件，让保存提示插入软磁盘，然后按回车。最后，将文件保存到软磁盘。

#### 将 for 循环转换为 while 和 until 循环

将示例 10–1 中的 `for` 循环转换为 `while` 循环。将数据存储在数组中并遍历数组元素。

在已经完成“重体力工作”之后，现在将示例中的循环转换为 `until` 循环。

#### 修改测试行的间距

编写一个脚本读取目标文件的每一行，然后将行写回标准输出，但在每行后面多加一个空行。这具有文件双倍间距的效果。

包含所有必要的代码以检查脚本是否获取了必要的命令行参数（文件名），以及指定的文件是否存在。

当脚本正常运行时，修改它以使目标文件变为三倍间距。

最后，编写一个脚本从目标文件中删除所有空行，使其变为单倍间距。

#### 反向列表

编写一个脚本将自身反向输出到标准输出。

#### 质数

打印（到标准输出） 60000 到 63000 之间的所有质数。输出应以列的格式整齐排列（提示：使用 `print`）。

#### 唯一系统 ID

为你的计算机生成一个“唯一的”6 位十六进制标识符。不要使用有缺陷的 `hostid` 命令。提示：`md5sum /etc/passwd`，然后选择输出的前 6 位。

#### 备份

将家目录树（`/home/user-name`）中在过去 24 小时内修改过的所有文件归为“tar 包”（`tar.gz` 文件）。提示：`find`。

#### 安全删除

编写一个脚本“安全”删除命令 `rm.sh`。作为命令行参数传递给此脚本的文件不会被删除，而是被 `gzip` 压缩并移动到 `/home/username/trash` 目录。在调用时，脚本检查“trash”目录中超过 48 小时的文件并删除它们。

### 中等

#### 管理磁盘空间

逐列出 `/home/username` 目录树中所有大于 100K 的文件。给用户删除或压缩文件的选项，然后继续显示下一个。将所有已删除的文件及其删除时间写入日志文件。

#### 找零

使用普通流通中的硬币（最高到 25 分币）为 $1.68 找零最有效的方法是什么？是 6 枚硬币、1 枚十分美币、1 枚镍美币和 3 个分币。

给定以美元和分表示的任意命令行输入（`$??`），使用最少数量的硬币计算找零。如果你的国家不是美国，可以使用你的货币单位。脚本需要解析命令行输入，然后将其转换为最小货币单位（分或或其他）的倍数。提示：查看 23–4。

#### 二次方程

求解形式为 $Ax^2 + Bx + C = 0$ 的“二次”方程。让脚本接受系数 `A`、`B` 和 `C` 作为参数，并返回带小数的解。

提示：将输出管道到 `bc`，使用著名的公式 $x = (-B \pm \sqrt{B^2 - 4AC}) / 2$。

#### 幸运数

“幸运数”是指其各个数字通过连续相加结果为 7 的数。例如，`62431` 是一个“幸运数”（`6+2+4+4+3+1=16`, `1+6=7`）。找到 1000 到 10000 之间所有的“幸运数”。

#### 字符串字母排序

对从命令行读取的任意字符串进行（`ASCII`）字母排序。

#### 解析

解析 `/etc/passwd`，并以美观易读的表格形式输出其内容。

#### 数据文件的格式化打印

某些数据库和表格软件包使用逗号分隔值（`CSV`）的保存文件。其他应用程序通常需要解析。给定一个逗号分隔值的数据文件：

```
CODES S

A B F G H

I K L M N

P Q R T U

V W Y Z
```

字母表中的每个字母出现一次，“I”也代表“J”。任意选择的关键词，“CODES”首先出现，然后是字母表的其余。加密时，将明文分成二分组（两个字母一组）。如果一组有两个相同的字母，删除第二个。如果最后剩下一个字母，插入一个“空”字符，通常为“X”。

```
THIS IS A TOP SECRET MESSAGE

TH AS OF SE GE
```

----------------------------------------------------------------

1) 两个字母都在密钥矩阵的同一行
将每个字母替换为右侧的字母。如果有需要，绕回行的开头。
2) 两个字母都在密钥矩阵的同一列
将每个字母替换为正下方的字母。如果有需要，绕回列的顶部。
3) 两个字母形成密钥矩阵内矩形的两个角。将每个字母替换为矩形所在行的另一个角。

或

----------------------------------------------------------------

```
"TH" 元组属于第三种情况。

GH

MN

T

（T 和 H 为角的矩形）
```

```
T -> U
```

### 困难

#### 访问记录

记录 `/etc` 的所有访问，包括文件名、用户时间和。

#### 删除注释

删除脚本中的所有注释。

#### HTML 转换

将文本文件转换为 `HTML`。

#### 指定文件中删除所有标签。

#### 摩斯密码

将文本文件转换为摩斯密码。每个字符将由点和线表示。

#### XML 转换

将 `XML` 文件转换并格式化为行。

#### 十进制转储

对文件进行二进制转储。每个字段显示地址。

#### 模拟移位器

使用 26 位示例，编写一个脚本模拟寄存器。实现加载寄存器、左移和右移的功能。

#### 行列式

求解 4x4 行列式。

#### 隐藏单词

编写一个“单词查找”游戏生成器，该脚本在 10x10 的随机字母矩阵中隐藏 10 个单词。单词可以水平、垂直或对角线方向隐藏。

# 高级 Bash 脚本指南

```
H --> G

"SE" 散列属于情况 #1。

C O D E S (包含 "S" 和 "E" 的行)

S --> C (向左回绕到行开头)

E --> S
```

要解密加密后的文本，请反向执行情况 #1 和 #2 中的上述步骤（替换时方向相反）。在情况 #3 下，只需取矩形的两个对角顶点即可。

`Helen Fouche Gaines` 的经典著作《要素级密码分析》（1939）对普莱费尔密码（`Playfair Cipher`）及其解决方案进行了相当详细的阐述。

此脚本将包含三个主要部分：

- I. 基于用户输入的关键词生成“密钥矩阵”。
- II. 加密“明文”消息。
- III. 解密加密后的文本。

该脚本将大量使用数组和函数。

请不要向作者发送这些练习题的答案。有更好的方式向他展示你的才华，例如提交 `Bug` 修复和改进本书的建议。

# 附录 J. 版权

《高级 Bash 脚本指南》版权所有，(c) 2000，作者 `Mendel Cooper`。本文可根据 `LDP` 许可规定的条款和条件进行分发。这些是非常宽松的条款，不应阻碍对本书的任何合法分发或使用。作者鼓励出于教学目的使用本书。

基本上，你可以自由分发未经修改的电子版本书。分发修改后的版本或派生作品必须获得作者的许可。此限制的目的是保护本文档的艺术完整性并防止“分叉”。

本书的商业权利现已出售。感兴趣请通知作者。

`Hyun Jin Cha` 完成了该书 1.0.1 版本的韩语翻译。西班牙语、葡萄牙语、法语和中文翻译正在进行中。如果你希望将本文档翻译成其他语言，请在遵守上述条款的前提下尽管进行。作者希望获得此类操作的通知。

附录 J. 版权

# 高级 Bash 脚本指南

# 笔记

- [1] 这些被称为内置命令（`builtins`），是 shell 内部的功能。

- [2] `ksh88` 的许多功能，甚至更新后的 `ksh93` 的部分功能已合并到 `Bash` 中。

- [3] 根据惯例，用户编写的通常符合 `Bourne shell` 标准的 shell 脚本通常以 `.sh` 扩展名命名。系统脚本（如位于 `/etc/rc.d` 中的脚本）不遵循这一指南。

- [4] 某些种的 `UNIX`（基于 `4.2BSD` 的）采用四字节的魔数名称，在 `!` 之后需要一个空格。`#!/bin/sh`。

- [5] shell 脚本中的 `#` 行将是命令解释器（`sh` 或 `bash`）看到的第一个命令。由于该行以 `#` 开头，当命令解释器最终执行脚本时，它会被正确解释为注释。该行已经完成了它的使命——调用命令解释器。

- [6] 这允许进行一些有趣的小技巧。

```bash
#!/bin/rm

# 自删除脚本。

# 运行此脚本时似乎没有发生什么……除了文件消失。

WHATEVER=65

echo "这一行永远不会打印（我敢赌！）。"

exit $WHATEVER # 无所谓。脚本不会在此退出。
```

此外，尝试用 `#!/bin/more` 编写一个 `README` 文件并使其可执行。结果是一个自列出的文档文件。（等等，我漏掉了一些文字）

- [7] 可移植操作系统接口（`POSIX`），一种试图标准化类 `Unix` 操作系统的尝试。

- [8] 警告：通过 `sh` 调用 `Bash` 脚本会关闭 `Bash` 特有的扩展，导致脚本可能执行失败。

- [9] 脚本需要读取权限以及执行权限才能运行，因为 shell 需要能够读取它。

- [10] 为什么不直接用 `scriptname` 调用脚本？如果你所在的目录（`$PWD`）是 `scriptname` 所在的位置，为什么这样做有效？出于安全考虑，目录 `.` 不包含在用户的 `$PATH` 中。因此，有必要在当前目录下通过 `./scriptname` 显式地调用脚本。

- [11] shell 执行括号扩展（`brace expansion`）。命令本身作用于扩展的结果。

- [12] 异常：作为管道一部分的大括号代码块可能会作为子 shell 运行。

# 附录 J. 版权

# 高级 Bash 脚本指南

```bash
ls | read firstline; read secondline; }

# 错误。括号中的代码块作为子 shell 运行，

# 因此 "ls" 的输出无法传递给块内的变量。

echo "First line is $firstline; second line is $secondline" # 将不起作用。
```

# 感谢，S.C.。

调用进程设置了 `$0` 参数。根据惯例，该参数是脚本名称。参见 `execv` 的映射。

在此语境下，“单词拆”（`Word splitting`）是指将字符字符串分成若干个独立的离散参数。

请注意，`suid` 二进制文件可能会打开安全漏洞，`suid` 标记对 shell 脚本无效。

在现代 `UNIX` 系统上，粘滞位（`sticky bit`）不用于文件，仅用于目录。

正如 S.C. 指出的，在复合测试中，即使对引用……

# 高级 Bash 脚本指南

内置命令的源码通常位于 `/usr/share/doc/bash`

注意 `-f` 选项并非所有系统都可移植。

- [28] `autoload` 的相同效果可以通过 `typeset` 实现。

- [29] 这些是以点命名的文件，例如 `.` 文件。它们不会在列表中显示，且无法通过 `rm -rf *` 删除。

- [30] `tar cvzf` 会包含当前目录下的目录。这是一个未文档的功能

- [31] 这是一个对称块密码，用于加密单个系统或本地网络上的文件，与“公钥”密码类相比，`pgp` 是著名的例子。

- [32] 守护进程（`daemon`）是不连接到终端会话的后台进程。守护进程在触发或通过特定事件时执行指定的服务。

“daemon”一词在希腊语中意味着幽灵，`Unix` 守护进程在后台默默执行任务的方式确实带有一种神秘的、超自然的色彩。

- [33] 这实际上是一个自 `Debian` 发行版的脚本。

- [34] 打印队列是等待打印的任务组。

- [35] 关于此主题的极佳概述，请参阅 `Andy Vaught` 在 1997 年 9 月《Linux Journal》上的文章《命名管道》。

- [36] `EBCDIC`（读作 "ebcd-sid-ic"）是扩展二进制编码交换的缩写。它是一种不再使用的 `IBM` 数据格式。应用 `dd` 的 `conv_ebcdic` 选项是一种快速但并不实用的文本文件编码器。

```bash
cat $file dd=swab,ebcdic > $file_encrypted

# 编码（看起来像乱码）

# 也可以交换字节（swab），增加一点效果

$file_encrypted dd=swab,ascii > $file_plaintext

# 解码。
```

- [37] 宏（`macro`）是一个符号常量，展开为命令字符串或对参数的操作集。

- [38] 这在 `Linux` 机器或带有磁盘配额的 `UNIX` 系统上是如此。

- [39] 如果被删除的用户仍登录，`userdel` 命令将失败。

# 高级 Bash 脚本指南

- 有关刻录 `CDR` 的更多信息，请参阅 1999 年 10 月份 [Linux Journal] 中 `Alex Withers` 写的文章《创建 CD》。

- `mke2fs` 的 `-c` 选项也会调用坏块检查。

- 单用户 `Linux` 系统的操作员通常倾向于使用更简单的备份工具，例如 `tar`。

- `NAND` 是逻辑“非与”运算符。它的效果与减法有些相似。

- 出于命令替换的考虑，命令可以是外部系统命令、内部脚本内置命令，甚至是脚本函数。

- 描述符（descriptor）仅仅是操作系统分配给打开文件的数字，用于跟踪它。或者可以将其看作简化版的文件指针。它类似于 `C` 语言中的文件句柄（`file handle`）。

- 使用文件描述符 5 可能导致问题。当 `Bash` 创建子进程（如 `exec`）时，子进程会继承 `fd 5`（参见 `Chet Cheney` 的邮件，主题为：RE: File descriptor 5 is held open）。最好让特定的 `fd` 保持原样。

- 最简单的正则表达式类型是保留其字面含义的字符字符串，不包含任何元字符。

- 由于 `sed`、`awk`、`grep` 处理单行，通常不会匹配换行符。在多行表达式存在换行符的情况下，点号 `.` 将匹配换行符。

```bash
#!/bin/bash

sed -e 'N;s/\n/\n/ ' << EOF # Here Document

line1

line2

EOF

# OUTPUT:

# [line1]

# line2

echo

awk '{ $0~"\n" $2; if (./line.1/) (print)' << EOF

line 1

line 2

EOF

# OUTPUT:

# line

#

 Thanks, S.C.

exit 0
```

- 文件名扩展可以匹配点文件（`dotfiles`），但只有当模式显式包含点时才。

## 附录 J 版权

```
~/[.bashrc      # 不展开为 ~/.bashrc

~/.bashrc       # 同样

               # 通配符和元字符在全局匹配（globbing）中不会展开为点。

~/.[b]ashrc      # 会展开为 ~/.bashrc

~/.ba7rc       # 同样

~/.bash*       # 同样
```

# 设置 "globopt" 可以关闭此功能。

# 感谢，S.C.。

- 这具有类似于命名管道（临时文件）的效果，事实上，命名管道当时被用于进程替换。

- 间接变量引用（参见示例 35–2）提供了一种笨拙的机制，将变量指针传递给函数。

# 感谢 Stephanie Chazelas 提供的启发性示例。

exit 0

- `return` 命令是 `Bash` 内置命令。

- `Herbert Mayer` 将递归定义为“……使用相同算法的简化版本来表达算法……”。递归函数是指调用它自身的函数。

## 附录 J 版权

- 递归层过多可能导致脚本因段错误（`segfault`）崩溃。

```bash
#!/bin/bash

recursive_function ()

{

  (( $1 < $2 )) && f $(( $1 + 1 )) $2;

  # 只要第一个参数小于第二个参数，

  # 增加 1 并递归。

}

recursive_function 1 50000 # 递归深度达 50,000 层！

# 自然会发生段错误。

# 如此深度的递归可能会由于耗尽分配给栈的所有内存而导致 C 程序发生段错误。

# 感谢，S.C.。

exit 0 # 此脚本将不会正常退出。
```



- 然而，别名（`aliases`）似乎会展开位置参数。
- 这不适用于`csh`、`tsh` 以及其他与经典的 Bourne shell (`sh`) 无关或后代的 shell。
- `/dev` 中的条目提供了物理和虚拟设备的挂载点。这些条目占用极少的磁盘空间。
- 某些设备如`/dev/null`、`/dev/zero` 和`/dev/urandom`是虚拟的。它们不是真实的物理设备，仅存在于软件中。
- 块设备（block device）以块为单位读取和或写入数据，而字符设备（character device）则以字符为单位访问数据。块设备的示例是硬盘和 CD ROM 驱动器。字符设备的示例是键盘。
- 某些系统命令如`procinfo`、`free`、`vmstat`、`lsdev` 和`uptime`也是这样做的。
- 根据习惯，信号 `0` 被分配给退出（`exit`）。
- 在脚本上设置`su`权限没有作用。
- 在此语境下，“魔数”（magic numbers）与用于指定文件类型的魔数完全不同的含义。
- Chet Ramey 承诺在未来的 Bash 版本中支持数组（Perl 的特性）。
- 能做的就去做；不能做的的……去考个 MCSE。
- 如果没有指定地址范围，默认为所有行。
- *

## 附录 J 版权

# 高级 Bash 脚本指南

- 越范围的退出值可能导致不可预测的退出状态。例如，`exit 3809` 给出的退出码为 `225`。
