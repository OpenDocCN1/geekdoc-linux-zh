
# 在 shell 脚本中进行算术运算

Bash 使用变量，这意味着它通常将变量视为字符串或文本，但如果你愿意，可以随时更改它们。除非你用 `declare` 告诉它，否则你的变量对 bash 来说只是一堆字母。当你开始在 bash 中进行算术运算时，如果可以，shell 将将其转换为整数。这使得在 bash 中执行相当复杂的算术运算成为可能。

整数运算可以使用内置的 `let` 命令或外部的 `expr` 和 `bc` 命令完成。在将 `BIGNUM` 值设置为 1024 后，这些命令会将值 64 存储在 `RESULT` 变量中。最后一个命令获取 0 到 10 之间的随机数并交给 bash 执行。

```bash
BIGNUM=1024
RESULT=$BIGNUM/16
RESULT=`expr $BIGNUM / 16 | bc -1`
let foo=$RANDOM%10; echo $foo
```

> 注意：shell 脚本的大部分元素都是相对自由的（空白，如空格或制表符是不重要的），但 `let` 和 `expr` 对空格非常特殊。`let` 命令要求每个操作数和数学运算符之间不能有空格，而 `expr` 命令的语法则要求每个操作数与其运算符之间留有空格。相比之下，`bc` 对空格并不挑剔，但因为它执行浮点运算，所以可能会比较棘手。

要查看使用 `let` 命令可以执行的算术运算完整列表，请在 bash 提示符下输入 `help let`。

# 在 shell 脚本中使用编程结构

使 shell 脚本如此强大的特性之一是，其循环和条件执行结构的实现与在更复杂的脚本和编程语言中发现的相似。你可以根据需要使用不同类型的循环。

## “if...then”语句

最常用的编程结构是条件执行，或 `if` 语句。它用于仅在特定条件下执行操作。它有几种变体，取决于你是在测试一个条件，还是在条件为真时执行某件事、条件为假时执行另一件事，或者你想连续测试几件事。

这个 `if...then` 示例测试 `VARIABLE` 是否设置为数字 1。如果是，则使用 `echo` 命令表示它被设置为 1。`fi` 表示 `if` 语句完成，可以继续处理。

```bash
VARIABLE=1
if [ $VARIABLE -eq 1 ]; then
  echo "The variable is 1"
fi
```

```bash
STRING="Friday"
if [ $STRING = "Friday" ]; then
  echo "WhoHoo Friday."
else
  echo "Friday will get ever here?"
fi
```

你也可以用感叹号（`!`）进行反向测试。在下面的示例中，如果 `STRING` 不是 Monday，则输出 "At least it's not Monday"。

```bash
STRING="FRIDAY"
if [ "$STRING" != "Monday" ]; then
  echo "At least it's not Monday"
fi
```

在下面的示例中，`elif`（代表 "else if"）被用于测试额外的条件（是否为文件名或目录）。

```bash
filename="$HOME"
if [ -f $filename ]; then
  echo "$filename is a regular file"
elif [ -d $filename ]; then
  echo "$filename is a directory"
else
  echo "I have no idea what $filename is"
fi
```

正如从前面的示例所示，条件被放置在方括号 `[ ]` 内。当测试表达式被求值时，它将返回值 0（表示为真）或返回 1（表示为假）。注意 `echo` 行缩进了。这是可选的，仅为了使脚本更具可读性。

表格 12-2 列出了可以测试的条件，是一个非常实用的参考。（如果你赶时间，可以在命令行上使用 `help test` 获取相同的信息。）

## 表 12-2：测试表达式的运算符

| 运算符 | 正在测试什么？ |
| --- | --- |
| -a file | 文件是否存在？（与 -e 相同） |
| -b file | 文件是否为特殊设备？ |
| -c file | 文件是否为特殊字符（例如，字符设备）？用于识别串口和终端设备。 |
| -d file | 文件是否为目录？ |
| -e file | 文件是否存在？（与 -a 相同） |
| -f file | 文件是否存在且是普通文件（例如，不是目录、套接字、管道或设备）？ |
| -g file | 文件是否设置了 set-group-id 位？ |
| -h file | 文件是否为符号链接？（与 -L 相同） |
| -k file | 文件是否设置了粘滞位？ |
| -L file | 文件是否为符号链接？ |
| -n string | 字符串长度是否大于 0 字节？ |
| -o file | 你拥有它吗？ |
| -p file | 文件是否为命名管道？ |
| -r file | 你是否可读该文件？ |
| -s file | 文件是否存在且大于 0 字节？ |
| -S file | 文件是否存在且是一个套接字？ |
| -t fd | 文件描述符是否连接到终端？ |
| -u file | 文件是否设置了 set-user-id 位？ |
| -w file | 你是否可写该文件？ |
| -x file | 文件是否可执行？ |
| -z string | 字符串长度是否为 0？ |
| -a file | 两个表达式都为真吗？ |
| -o file | 至少有一个表达式为真吗？ |
| -nt file | 第一个文件比第二个文件新吗？ |
| -ot file | 第一个文件比第二个文件旧吗？ |
| -ef file | 两个文件相等吗？ |

# 第 12 章：自动化系统任务

## 第12 章：自动化系统任务

```bash
for FILE in /bin/ls
do
  echo $FILE
done
```

你可以这样写，这样稍微整洁一些。

```bash
for NAME in John Paul Ringo George ; do
  echo $NAME is my favorite Beetle
done
```

`LIST` 中的每个元素都通过空格与下一个元素隔开。如果你不小心，这可能会引起麻烦，因为某些命令（如 `ls -l`）每行输出多个字段，每个字段都用空格隔开。语句在该字符串结束。

如果你是一个习惯了 diff 的 C 语言程序员，bash 允许你使用 C 语言的语法来控制循环：

```bash
LIMIT=10
# 双括号，即使 LIMIT 是变量，也不加 $ 符号：
for ((a=1; a <= LIMIT; a++)); do
  echo "$a"
done
```

## “while...do” 和 “until...do”

另外两种可能的循环结构是 `while...do` 循环和 `until...do` 循环。它们的结构在此所示：

```
while condition    until condition
do               do
  { body }         { body }
done              done
```

`while` 语句在条件为真时执行。`until` 语句在条件为真时停止，换句话说，在条件为假时执行。

这是一个 `while` 循环的示例，将输出数字 0123456789：

```bash
N=0
while [ $N -lt 10 ] ; do
  echo -n $N
  let N=$N+1
done
```

输出数字 0123456789 的另一种方法是使用如下 `until` 循环：

```bash
N=0
until [ $N -eq 10 ] ; do
  echo -n $N
  let N=$N+1
done
```

## 一实用的外部程序

Bash 非常强大，有很多内置命令，但它通常需要一些帮助来完成有用的工作。你经常看到的常用的实用程序有 `grep`、`cut`、`tr`、`awk` 和 `sed`。有了这些 UNIX 工具，这些程序中的大多数都被设计为配合标准输入和标准输出工作，因此你可以轻松地结合管道和 shell 使用它们。

## 通用正则表达式解析器 (grep)

“正则表达式解析器”这个名字听起来很吓人，但 `grep` 只是在文件或文本中查找模式的方法。把它想象成搜索工具。精通正则表达式是一个挑战，但很多事情只需要最简单的形式就能完成。

例如，你可以使用 `grep` 搜索 `/etc/passwd` 文件中包含 `/home` 的行，以此来显示所有用户账户列表：

```bash
grep "/home" /etc/passwd
```
