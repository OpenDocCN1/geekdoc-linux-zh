
- 19.6 一个用户属于 `student` 组，但 `/etc/group` 没有在组旁边显示他的名字。这代表什么？
- 19.7 用户如何通过 `passwd` 更新 `/etc/shadow`，尽管该文件受限制？
- 19.8 你将如何安排一组用户向同一个目录写入，且无法删除其他的文件？
- 19.9 `init` 的两个重要功能是什么？解释 shell 进程是如何创建的。
- 19.10 你如何确定默认运行级别？运行级别 0 和 6 之间有什么区别？
- 19.12 `start` 和 `kill` 脚本的意义是什么？它们是...
- 19.13 你将如何使用 `shutdown` 立即关闭系统？Linux 提供了什么快捷？
- 19.14 提到启动文件系统和交换文件系统的重要性。
- 19.15 哪些文件系统可以卸载？为什么？
- 19.16 `fsck` 命令用于什么？
- 19.17 `find` 选项 `-perm 1000` 和 `-perm -1000` 之间的区别是什么？
- 19.18 管理员如何安排在工作日的上午 9 点和晚上 10 点监控空闲磁盘空间？
- 19.19 你将如何找出当前目录树的总使用量？
- 19.20 你如何在 (i) SVR4 和 (ii) Linux 中将 HTML 文件复制到 DOS 软盘中？
- 19.21 命令 `tar xvf /dev/fd *.c` 显示了错误信息，尽管软盘中包含多个 `.c` 文件。解释导致此消息的两种情况。
- 19.22 `rpm` 命令只能从 root 用户账户使用。对或错？
- 19.23 尽管你正确指定了包名，`rpm` 仍拒绝卸载软件包。可能的原因是什么？

（注：原文后续存在大量重复题目，已按要求不重复输出）

# 附录 A：C Shell——编程结构

`set` 语句也可以填充数组；值必须用括号括。`shift` 语句也可以作用于数组：

```
$ set num = ( 9876 2345 6213 )
% echo $num[1]
9876
% echo $'num
3
% shift num
% echo $num[1]
2345
```

存储在 `$num[*]` 中的完整列表

需要数组名

## 比较和逻辑运算符

数值比较与 awk 相同，它使用了 `<`、`!=`、`==` 和 `>=` 运算符。完整列表见表 12.3。字符串比较也使用 `==` 和 `!=` 运算符，但 C shell 优于 Bourne shell，因为它支持另外两个匹配通配符表达式的运算符：

- `**` 匹配通配符表达式
- `?*` 不匹配通配符表达式

perl 使用这些运算符的含义相同，不同在于 perl 使用它们来匹配正则表达式。你也可以像在 Bourne shell 中一样使用 `&&` 和 `||` 运算符。

## if 语句

在 Bourne shell 中，`if` 条件判断有第 13 章所示的三形式。然而，存在以下差异：

- `then` 必须与 `if` 在同一行。
- 结构以 `endif` 结束，而不是 `fi`。
- 命令被包含在括号内（除非它是 UNIX 命令）。

让我们查看这三种形式，但仅看示例。第一形式展示了数值比较的使用，但注意第二种形式，它匹配 `$response` 与任何以 y 或 Y 开头的字符串：

| if ($argv != 2 ) then | if ($response = [yY]*) then |
| :--- | :--- |
| echo Two parameters required | echo You answered yes |
| endif | else |
| | echo You answered no |
| | endif |
| 形式 1 | 形式 2 |

第三种形式使用了 `if-else` 子句（根据需要可以使用多次），但仅有一个 `endif`。这里是脚本 `emp3a.sh`（第 13 章）的核心部分，此处已修改为在 C shell 中运行：

```
if ($ # == 0 ) then
echo "Usage: $0 pattern file" >/dev/tty
else if ($ # == 2 ) then
grep "$1" $2 || echo "$1 not found in $2" >/dev/tty
else
echo "You didn't enter two arguments" >/dev/tty
endif
```

### 形式 3

作为形式 1 的变体，当没有 `else` 子句时，可以使用单条件判断。不使用 `then` 和 `endif` 关键字：

```
if ($ #argv == 2 ) @ size = $1 * 512; echo Size of $2 is $size bytes
```

当你使用 UNIX 命令作为控制命令时，命令本身应该用一对匹配的大括号括起来，而不是括号：

```
if ( grep "director" emp.lst ) then
```

注意，与 `if` 使用控制命令时必须提供 `( )` 或 `{ }` 封装。

## 测试文件属性

尽管 C shell 没有 `test` 语句，你仍然可以测试文件属性。该 shell 支持有限的运算符，其中大部分在 Bourne shell 中的用法如下：

- `-f file` 如果是普通文件则为真。
- `-d file` 如果是目录则为真。
- `-r file` 如果可读则为真。
- `-w file` 如果可写则为真。
- `-x file` 如果可执行则为真。
- `-e file` 如果存在则为真。
- `-z file` 如果文件存在且大小为零则为真。

以下代码展示了部分运算符的使用：

```
if ( -f $1 ) then
if ( ! -r $1 ) then
echo "File exists but is not readable"
else
echo "File is readable"
endif
else
echo "File doesn't exist"
endif
```

## switch 语句

`switch` 语句基于 C 语言中的同名结构。与 `case` 类似，该结构语句根据多个替代方案匹配表达式。使用的关键字有 `ends`、`case`、`default` 和 `breaksw`。在第 13 章开发的 `menu.sh` 代码在此处修改为使用 `switch` 代替 `case`：

```
cat << END
MENU
1. List of files
2. Processes of user
3. Exit
Enter your option:
set choice = $<
switch ($choice)
case 1:
ls -1 ; breaksw
case 2:
ps -f ; breaksw
case 3:
exit
echo "Invalid option"
END
```

`breaksw` 关键字在找到成功匹配后将控制移到结构之后。如果没有使用此词，则会产生“穿透”（fall through）行为，执行所有剩余的 `case` 。`default` 关键字通常作为最后一个选项。

## while 和 foreach 循环

有两种循环——`while` 和 `foreach`（代替 `for`）。这两种循环与 Bourne 中的对应物有三个主要区别：

- `foreach` 使用的控制命令或列表封装在括号内。
- 不使用 `do` 关键字。
- 循环以 `end` 结束而不是 `done`。

让我们先考虑 `while` 循环。在提示符处输入的简单序列将运行四次 `ps` 命令：

```
set x = 1
while ($x < 5)
  ps -f
  sleep 5
  @++
end
```

`foreach` 循环用于迭代单词列表。例如：

```
foreach file (a b c)
  echo $file
end
```

# 附录 B：Korn 和 Bash Shell——独有的编程结构

```
$ -p "Enter y or n: " -nl
Enter y or n: y
$ No[Enter] pressed
returns without [Enter]
```

Korn shell 使用在协进程（coprocess）中的 `read` 来从父进程接受标准输入。（Bash 中的 `read` 并不具备此功能）。Korn Shell '93 还支持超时功能。

## 访问所有位置参数

在 Bourne shell 中，你无法通过 `$10` 访问第 10 个位置参数；你必须使用 `shift` 然后访问 `$9`。在 Korn 和 Bash 中，你可以通过大括号包裹参数来访问任何位置参数：

```
echo ${15}
```

这会打印传递给脚本的第 15 个参数。然而，我们通常不需要处理许多参数的脚本，但如果我们使用 `set` 来分配位置参数，可以打印它来获取代码：

```
$ ls -ls /etc/passwd
289906 4 -rw-r--r-- 1 root root 639 Oct 2 23:09 /etc/passwd
$ set --($ls -ls /etc/passwd)
$ echo "the ${11} has the number $1"
The file /etc/passwd has the number 289906
```

回想一下，我们在这些 中中使用 `$(command)` 形式执行命令替换。

## select 语句

`select` 语句显示一个菜单，读取选定的选项并将其供使用。这种不特殊的结构语法与 `for` 循环相似：

```
select var stg1 stg2 ...
do
  action
done
```

字符串 `stg1`、`stg2` 等会被显示为编号的菜单选项。`select` 显示一个由 `PS3` 求值的提示符（默认值为 `--#`）。你输入的数字存储在变量 `REPLY` 中，而代表该数字的字符串保存在 `var` 中。`select` 的体必须包含根据 `REPLY` 的每个值确定执行操作的代码。在执行操作或用户按下 `[Enter]` 后，菜单会重复显示。要终止循环，必须在体中使用 `break` 语句。

第 13 章中使用 `case` 语句的脚本可以使用 `select` 重新实现：

```bash
#!/usr/bin/ksh
#
PS3="Choice: "
select task in "List of files" "Processes of user" \
  "Today's Date" "Users of system" "Quit" \
do
  case $REPLY in
    1) ls -l ;;
    2) ps -f ;;
    3) date ;;
    4) who ;;
    5) break ;;
    *) echo "Invalid option" ;;
  esac
done
```

我们首先将 `PS3` 设置为一个有意义的字符串。脚本呈现了一个五选项的菜单，每当输入 1 到 4 之间的选项时，它就会重复显示。选项 5 因为 `break` 语句终止了循环：

- 1) List of files
- 2) Processes of user

Choice: 3

Tue Jun 29 11:29:09 EST 2004

Choice: 6

Invalid option

3) Today's Date

4) Users of system

5) Quit

由 PS3 设置的提示符

在 `for` 循环中，列表可以作为命令行传递给 `select`。`select task` 等同于 `select task in "$@"`

## `[[ ]]` 结构

为了配合 `if` 和 `while` 语句进行测试，Korn 和 Bash 支持额外的结构——`[[ ]]` 和 `(( ))`。`[[` 实际上是一个需要 `]]` 作为结束符的内置命令。它是 `test` 语句的超集；你可以用它进行数值和字符串比较，还可以测试文件属性：

```bash
if [[ $answer = y ]]
if [[ $# -ne 2 ]]
if [[ -f file ]]
```

### Bourne shell 特性

让我们学习为什么要使用 `[[` 结构。在单个 `[[ ]]` 内部使用 `&&` 和 `||` 运算符：

```bash
if [[ $answer = y || $answer = Y ]]
```

与仅匹配字符串的 `test`（或 `[ ]`）不同，`[[` 允许使用 shell 通配符（类似于 `case`）。考虑以下示例，第一个与之前的示例等效。第二个示例匹配至少四个字符的字符串。第三个示例匹配 C 或 Java 程序的文件名：

```bash
if [[ $Answer = [yz] ]]
if [[ $Answer = ???* ]]
if [[ $filename = *.c || $filename = *.java ]]
```

注意，即使模式没有加引号，shell 也不会尝试将它们与当前目录下的文件名匹配。由于 Korn 和 Bash 中的通配符支持一些额外的字符（第 6 章——进阶），我们可以缩短上面第三示例中的命令：

```bash
if [[ $file = @(*c,.java) ]]
```

如果你在 Bash 中使用了如 `(` 等出现在通配符表达式中的字符，别忘记在脚本开头使用 `shopt -s extglob`。要对前面的测试进行取反，在两种 shell 中均使用 `!` 代替 `@`。

使用全套通配符进行模式匹配的功能确实非常方便。

## `(( ))` 结构

（注：原文此部分存在大量重复和 OCR 错误，已根据逻辑要求清理）

在评估元素时，注意使用大括号。尽管 `month[1]` 看起来像被处理为一个变量，但它可以与一个命名的月份共存。要填充元素组，请使用以下两种形式之一：

```
set -A month 0 31 28 31 30 31 30 31 31 30 31 30 31
month=(0 31 28 31 30 31 30 31 31 30 31 30 31)
```

此数组存储了 12 个月中的每个月的天数。第一个元素被设置为零，因为否则 `month[0]` 没有任何意义。你可以使用 `@` 或 `*` 作为下标显示所有已定义的元素。如果你添加了 `#` 前缀，则只显示计数：

```
$ echo ${month[@]}
0 31 28 31 30 31 30 31 31 30 31 30 31
$ echo ${#month[@]}
13
```

已分配元素的数量...

当你选择性地分配单个元素时会发生什么？例如，如果你只设置了 `x[0]` 和 `x[100]`，则只会为这两个元素分配内存，而 `x[99]` 的求值为 `null`：

```
$ x[0]=1; x[100]=10
$ echo ${x[0]}
1
$ echo ${#x[@]}
2
```

而不是数组的大小

本附录中讨论许多特性都没有包含在 POSIX 中，因此大问题是是否应该使用所有它们。今天，Bash 越来越多地随 UNIX 系统（包括 Solaris）一起分发，但现在的每个系统都支持 Korn Shell。因此，即使你的应用程序不符合 POSIX 标准，只要你使用了至少在 1993 年之前的 Korn Shell 版本中可用的功能，就可以实现相当程度的可移植性。无论如何，POSIX 的下次修订还需要一段时间。

# 附录 C

## GNU emacs 编辑器

除了 vi 之外，许多 UNIX 系统还提供 emacs 全屏编辑器。它由 Richard Stallman（GNU 的创始人）创建，现在是自由软件基金会。正如你预期的那样，所有的 Linux 发行版都提供 emacs。它的起源于一组宏，但如今的 emacs 不仅仅是一个编辑器。它提供了一个完整的环境，你可以在其中使用合适的插件处理和浏览 Web 网。在本附录中，我们将局限于编辑功能。

## 一个 emacs 会话

与 vi 不同，emacs 可能没有安装在你的系统上。确保你已经安装了 emacs，然后用文件名调用它：

```
emacs emfile
```

在全屏模式下（图 C.1），顶行有一个反显色显示的菜单。底部的模式行（mode line）也以反显色显示。这一行显示了文件名（emfile）和光标所在的当前行；L7 是第 7 行。注意 F1 左侧的两个星号；表示缓冲区已修改。起初，你应该在该位置看到三个连字符。

最后一行被称为最小缓冲区（minbuffer），显示由 emacs 生成的消息。该行用于用户输入 emacs 命令，并用于 emacs 显示系统消息。由于 emacs 占用了三行供其内部使用，因此 22 行可用于编辑。

你现在可以直接输入文本，使用 `[Enter]` 分隔行。要擦除文本，你使用 `[Backspace]` 键而不是 `[Ctrl-h]`。后者是用于调用其帮助辅助设施的 emacs 快捷键。你也可以使用 `[Ctrl-d]` 或 `[Delete]` 删除光标下方的字符。我们将使用这个阴影框来表示

当你键入文本后，光标将位于文本的最后一行。你现在可以沿着当前行水平移动。按下 `[Ctrl-b]` 将光标向后移动，按下 `[Ctrl-f]` 向移动。你也可以使用 `[Ctrl-n]` 移动到上一行。此外，还有更快的导航方法；将在稍后讨论。

657

# 图 C.1 插入一些文本

| 文件 | 编辑 | 选项 | 缓冲区 | 工具 | 帮助 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 按下的任何键都会显示为输入。[Enter] | | | | | |
| 除非你使用控制键和元键。[Enter] | | | | | |
| 这些键用于导航和文本编辑。[Enter] | | | | | |
| 同样使用 [Ctrl-n] 和 [Ctrl-p] 向上和向下移动。[Enter] | | | | | |
| 我们将它们称为 C-n 和 C-p。 | | | | | |
