
```
$((expression))
```

表达式将根据 C 编程语言的规则进行求值，并替换结果。例如：

```bash
foo=$(( ((5 + 3*2) - 4 ) / 2 ))
```

将把 `foo` 的值设置为 3（而不是 3.5），因为这是整数算术；或者由于操作符优先级设为 6。

引号去除在所有其他扩展完成后执行，`\`（反斜杠）、`'`（单引号）和 `"`（双引号）会移除所有剩余的未加引号的字符：

`bash` 执行两种类型的扩展。这些是大括号扩展和路径名扩展。它们主要用于在命令行发出的字符。大括号扩展用于创建多个具有共同元素的字符串。其通用形式为：

```
stringx{string1, string2, ..., stringn}
```

`bash` 展开这些 `[item]` 字符串，每个字符串包含括号中列出的字符串之一，并以 `stringx` 为头并由后缀替换。前缀或末尾字符串会被省略，但大括号内字符串的少数量为一，且括号内的项必须用逗号分隔。

| 模式 | 描述 |
| :--- | :--- |
| * | 匹配任何字符串 |
| ? | 匹配任何单个字符 |
| [abc] | 匹配括号中的任意一个字符 |
| [a-z] | 匹配范围内的任何字符 |
| [!abc] | 匹配不在括号内的任何字符 |

## 列表

除了管道外，命令可以在列表中执行，其中多个管道使用 `;`、`&` 或 `|` 运算符连接。列表可用于按顺序执行命令：

```
command1; command2; command3 ...
command1 | command2; command3 | command4 ...
```

列表通常用于此类任务：

```
lpr foo; lpq;
ps -ael | head -1; ps -ael | grep "$UID"
```

这些任务无法在单个命令中执行。

如果给出逻辑 AND 或 OR 运算符，列表还可以根据上一个命令的退出状态来执行命令：

```
command1 && command2
command1 || command2
```

如果使用了逻辑 AND 运算符（如第一种情况），只有当 `command1` 返回的退出状态为 0 时，才会执行 `command2`。如果使用了逻辑 OR 运算符（如第二种情况），只有当 `command1` 返回非零退出状态时，才会执行 `command2`。逻辑运算符经常被用来代替 `if` 语句；这种形式对于熟悉 C 编程语言及其“短路””逻辑运算符的人来说是直观的。

任何列表都可以在当前 shell 环境中或在子 shell 中执行。使用大括号包裹列表：

- `list ; }`

会导致列表在当前 shell 中执行，而使用圆括号包裹列表：

- `list ; )`

会导致列表在子 shell 中执行。例如：

```
ps -ael | head -1; ps -ael | grep "$UID " ; }
```

在当前 shell 中运行列表 `ps -ael | head -1; ps -ael | grep "$UID"`，并将其输出传递给 `more`。相同的列表可以在子 shell 中运行：

```
ps -ael | head -1; ps -ael | grep "$UID " ; )
```

但这可能不是一个好主意，因为每个子壳（`subshell`）都会占用更多的系统资源。在当前 shell 中运行所有程序会更高效。在子壳中运行列表是有用的，因为子壳可以有效地让所有变量变为局部的，且子壳拥有它们自己的工作目录。如下示例所示：

```
pwd; ( cd /tmp ; pwd ) ; pwd;
```

当前工作目录仅在子壳中发生了更改。

# 重定向

列表可以使用 `< >` 运算符包含输入和输出的重定向。默认情况下，`<` 重定向标准输入 `>` 重定向标准输出，但重定向操作符也可以用于打开和关闭文件。通常，输出重定向为：

```bash
command > file
list > file
```

第一种形式将命令的输出重定向到文件，而第二种将列表的输出重定向到文件。例如：

```bash
date > now
```

将 `date` 命令的输出重定向到文件 `now`。列表的输出也可以被重定向：

```bash
{ date; uptime; who; } > myylog
```

将 `date`、`uptime` 和 `who` 所有命令的输出都重定向到文件 `myylog`。除了这种覆盖输出文件的输出重定向外，还有追加输出重定向。如果使用 `>>` 运算符，输出将追加到文件中，如果文件不存在则会创建文件。通常，追加输出重定向为：

```bash
command >> file
list >> file
```

如果文件 `myylog`（上文）不应在每次添加数据时删除，可以写为：

```bash
{ date; uptime; who; } >> myylog
```

`Bash` 还允许将标准输出和错误合并重定向。通常，其实现方式为：

```bash
&& file
>& file
> file 2>&1
```

手册页显示第一种形式是优的，但所有形式都是等价的。第三种通过使用标准输出（文件描述符 1）和标准错误（文件描述符 2）的文件描述符工作；它实际上与C语言库函数 `dup()` 的作用相同。需要重定向输出标准错误的常用场景是：

```bash
if type emacs &> /dev/null ; then
  EDITOR=emacs
else
  EDITOR=vi
fi
```

在这里，只关心 `type` 内置命令的返回值，它的输出或打印的任何错误信息都被忽略，因此被重定向到 `/dev/null`。

输入也可以以类似的方式重定向。通常，输入重定向为：

```bash
command < file
```

在这里，文件的内容将成为 `command` 的输入。例如，以下是重定向的一种用法：

```bash
Mail ranga@soda.berkeley.edu < Final_Exam_Answers
```

其中 `Mail` 的输入（即邮件正文）将是文件 `Final_Exam_Answers`。

输入重定向另一个用途是创建 Here documents（在此文档）。Here document 的通用形式为：

```bash
command << delimiter
document
delimiter
```

`shell` 将 `<<` 运算符解释为读取输入的指令，直到找到包含分隔符的行。所有在包含分隔符的行之前的输入都会传递到命令的标准输入中。`Bash` 不对分隔符进行任何形式的扩展，但 `bash` 会对 Here document 中的行进行扩展。例如，为了打印一个 URL 列表，可以使用以下 Here document：

```
lpr << MYURLS
http://www.csua.berkeley.edu/~ranga/
http://www.macintouch.com/
http://www.marathon.org/story/
http://www.gnu.org/
MYURLS
```

这提供了创建临时文件的方便替代方案。为了删除此示例中的制表符，`<<` 运算符可以是选项——

# 流程控制

`Bash` 提供了两种强大的控制机制：`if-fi` 块和 `case-esac` 块。`if` 语句通常用于命令的条件执行，而 `case` 语句允许根据多个模式中第一个匹配变量的一个来执行任意数量的命令序列。如果涉及将变量与模式匹配，写成 `case` 语句通常更简单。

基本语法是 `if list ; then list; [elif list; then list; ] ... [else list]; fi`，写法如下：

```bash
if list1 ; then
  list2
elif list3 ; then
  list4
else
  list5
fi
```

`elif` 和 `else` 语句都是可选的。一个 `if` 语句可以带有任意数量的 `elif` 语句，且 `if` 语句可以只包含 `if` 和 `elif` 语句。`if` 语句中的列表可以是上一节讨论的列表。

在上述通用 `if` 语句中，首先评估 `list1`，如果 `list1` 代码为真，则执行 `list2` 和 `if` 语句。否则，评估 `list3` 并检查其退出码。如果 `list3` 返回 0，则执行 `list4` 并退出 `if` 语句。如果 `list3` 不返回 0，则执行 `list5`。`if` 语句的一个简单用法：

```bash
if uencode koala.gif koala.gif > koala.uu ; then
  echo "Encoded koala.gif to koala.uu"
else
  echo "Error encoding koala.gif"
fi
```

如果 `uencode` 命令的退出码表示成功，将回显 "Encoded koala.gif to koala.uu"。否则，将报告错误。

大多数情况下，列表是 `test`，用于评估条件。以下是常用的 `test` 操作符：

| 操作符 | 描述 |
| :--- | :--- |
| -d | 是目录 |
| -f | 是普通文件 |
| -k | 设置了粘滞位 |
| -L | 是符号链接 |
| -r | 可读的 |
| -s | 大小非零 |
| -t | 针对终端打开 |
| -w | 可写的 |
| -x | 可执行的 |
| -O | 属于有效用户 |
| -nt | file1 新于 file2 |
| -ot | file1 旧于 file2 |
| -z | 字符串长度为零 |
| -n | 字符串长度非零 |
| = | 等于 |
| != | 不等于 |
| ! | 为假 |
| -a | expr1 且 expr2 真 |
| -o | expr1 或 expr2 真 |
| -eq, -lt, -le, -gt, -ge | 算术比较 |

算术操作符分别返回等于、不等于、小于、小于等于、大于或大于真。`Arg1` 和 `arg2` 可以是正整数。

简单 `if` 结合的用法示例：

```bash
if [ -d $HOME/bin ]; then PATH=$HOME/bin; fi
if [ -s $HOME/.bashias ]; then . $HOME/.bashias; fi
```

在第一个示例中，`test` 用于判断目录是否存在并执行某些操作。第二个示例中，`test` 在执行任何操作之前判断文件是否存在且大小非零。

这里是两个等效的示例，展示了如何组合：

```bash
if [ -z "$HOME" && -d /usr/dt ]; then DHOME=/usr/dt; fi
if [ -z "$HOME" -a -d /usr/dt ]; then DHOME=/usr/dt; fi
```

某些用户喜欢第一种，因为逻辑了然。其他用户喜欢第二种，因为它只调用一次命令，可能更高效。

另一种流程控制形式是 `case-esac` 块。语法为 `case word in [ | pattern ... ] list ;; esac`，但通常写为：

```bash
case word in
pattern)
  list
;;
pattern2)
  list2
;;
esac
```

在这种形式中，`word` 是字符串或变量，其值与每个模式进行比较直到找到匹配。一旦执行了 `list`，程序将跳转到整个 `case` 语句的结束。如果没有找到匹配，`bash` 将退出 `case` 语句。可以使用 `*` 模式来执行某些默认操作。模式可以使用与路径匹配相同的特殊字符，并加上“或”运算符。`| ;;` 向 `bash` 表示列表已结束，类似于 C 语言中的 `break`。一个简单 `case` 语句的示例：

```bash
case "$TERM" in
term)
  TERM=xterm
;;
network|dialup|unknown|vt[0-9]*)
  TERM=vt10
;;
esac
```

`esac`

# 循环

`Bash` 支持三种类型的循环：`for`、`while` 和 `select` 循环。当需要重复执行一组命令时，使用 `for` 循环。当需要在特定条件成立时执行一组命令时，使用 `while` 循环。`select` 循环的一个用途是提供方便的选择界面。

基础的 `for` 循环语法为 `for name in list1; do list2; done;`，通常写成：

```
for name in list1
do
list2
done
```

在 `for` 循环中，变量 `name` 被设置为 `list1` 中的每个元素，并为 `list1` 的每个元素执行 `list2`。如果未给出 `list1`，`bash` 将遍历所有参数。如果 `list1` 以单词形式提供，则会对其进行展开。一个简单的 `for` 循环示例是：

```
for i in 1 2 3 4 5 6 7 8 9 10
do
echo $i
done
```

`for` 循环的一个常见用途是：

```bash
for files in ~/.bash_*
do
echo "<HEAD><TITLE>${files}.html</TITLE></HEAD>" >> ${files}.html
echo "<BODY><PRE>" >> ${files}.html
cat ${files} >> ${files}.html
echo "</PRE></BODY>" >> ${files}.html
echo "</html>" >> ${files}.html
chmod go+${files}.html
done
```

基础的 `while` 循环语法为 `list1; do list2; done.`。这通常写成：

```
while list1
do
list2
done
```

在 `while` 循环中，每次都会评估 `list1`，只要为真，就会执行 `list2`。这允许使用 `/bin/true` 作为 `list1` 来编写无限循环。一个简单的 `while` 循环示例是：

```bash
x=1
while [ $x -lt 10 ]
do
echo $x
x=$((x+1))
done
```

这个 `while` 循环将输入复制到其输出，类似于 `cat` 程序：

```bash
while read
do
  echo $REPLY;
done
```

如果使用了重定向，此循环将输入文件的内容写入标准输出，类似于 `cat`。

`while` 循环的变体是 `until` 循环：

```
until list1
do
  list2
done
```

在 `until` 循环中，一直执行 `list2` 直到 `list1` 为真。`until` 循环与 `while` 循环相同，`until` 后面的 `!` 是等效的：

```bash
x=1; while ! [ $x -ge 10 ]
do
  echo $x
  x=$((x+1))
done
x=1; until [ $x -ge 10 ]
do
  echo $x
  x=$((x+1))
done
```

`select` 循环是一种创建编号菜单的简单方法，用户从中可以选择选项。基础语法为 `select name in list1; do list2; done;`，通常写成：

```
select name in list1
do
  list2
done
```

在 `select` 循环中，`list1` 中的项会被打印到标准错误，前面带有一个数字。然后会显示提示符并读取一行。如果 `$REPLY` 变量（包含该列表行的变量）包含一个显示项的数字，则执行 `list2`。会再次显示 `list1` 中的项列表。如果读取到 EOF（文件结束），`select` 循环结束。

以下 `select` 循环显示 `/tmp` 目录下的文件列表，并对存在的文件运行 `ls -1`：

```bash
select file in /tmp/*
do
  if [ -e $file ]; then
    ls -l $file
  else
    break
  fi
done
```

输出将类似于：

+ 1) /tmp/. 6) /tmp/job.control.ms

2) /tmp/. 7) /tmp/job.control.ps

3) /tmp/.X11-unix 8) /tmp/ps_data

4) /tmp/intro7.html 9) /tmp/sunpro.c.1.157.3.000

5) /tmp/java 10) QUIT

#

其中 `#` 是用户输入数字的提示符。

`Bash` 中的所有循环都可以通过提供内置的 `break` 命令立即退出。该命令还接受一个大于或等于 1 的参数，指示要跳出的层数。当使用嵌套循环时此功能非常有用。

# 注释

`Bash` 命令以 `#` 字符开始。`#` 和换行符之间的每个字符都被视为命令的一部分，并被 `bash` 忽略。默认情况下，交互式 shell 和非交互式 shell 都是如此。交互式 shell 可以通过 `shift` 内置函数来更改此设置。

## 初始化文件

交互式登录 `bash` 会读取 `~/.bash_profile`、`~/.bash_login`、`~/.profile`，而非登录交互式 `bash` 会读取 `~/.bashrc` 文件。`bash` 尝试读取的初始化文件数量让许多用户感到困惑。

### 初始化文件注意事项

`Bash` 新手面临的主要问题之一是要创建哪些初始化文件以及在文件中放入什么内容。最简单的解决方案（许多 `bash` 用户都在使用）是创建一个初始化文件，并让其他文件成为该文件的符号链接。
