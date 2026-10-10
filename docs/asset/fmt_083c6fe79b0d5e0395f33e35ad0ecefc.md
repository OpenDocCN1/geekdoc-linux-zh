
```
MYFILENAME="/home/digby/myfile.txt"
FILE=${MYFILENAME##*/}             #FILE becomes "myfile.txt"
DIR=${MYFILENAME%/*}              #DIR becomes "/home/digby"
NAME=${FILE%.*}                   #NAME becomes "myfile"
EXTENSION=${FILE#*.}              #EXTENSION becomes "txt"
```

### 在 Shell 脚本中执行算术运算

Bash 使用无类型变量，这意味着它通常将变量视为字符串或文本，但如果你希望的话，它可以即时更改它们。除非你通过 `declare` 告诉它否则，你的变量对 bash 来说只是一堆字母。但是，当你开始尝试对它们进行算术运算时，bash 会在可能的情况下将它们转换为整数。这使得在 bash 中执行一些相当复杂的算术运算成为可能。

可以使用内置的 `let` 命令或通过外部的 `expr` 或 `bc` 命令执行整数算术。在将变量 `BIGNUM` 设置为 1024 之后，接下来的三个命令都将把值 64 存储在 `RESULT` 变量中。（使用 `bc` 的命令会将 `RESULT` 变量设置为 64.00000000000000000000。）

最后一个命令获取 0 到 10 之间的一个随机数，并将结果回显给你。

```
BIGNUM=1024
let RESULT=$BIGNUM/16
RESULT=`expr $BIGNUM / 16` 
RESULT=`echo "$BIGNUM / 16" | bc -l` 
let foo=$RANDOM%10; echo $foo
```

你还可以使用以下双括号语法进行行内算术运算：

```
$ RESULT=$( (10*20) )
$ echo $RESULT
200
```

> **注意：** 虽然 shell 脚本的大多数元素形式较为自由（即空格、制表符等空白字符通常无关紧要），但 `let` 和 `expr` 对空格的使用有着严格的要求。`let` 命令坚持在每个操作数与数学运算符之间不能有空格，而 `expr` 命令的语法则要求每个操作数与其运算符之间必须有空格。与它们相比，`bc` 对空格并不挑剔，但由于它执行的是浮点算术，使用起来可能更具挑战性。

要查看使用 `let` 命令可以执行的算术运算的完整列表，请在 bash 提示符下键入 `help let`。

### 在 shell 脚本中使用编程结构

shell 脚本之所以强大，其中一个特性是其对循环和条件执行结构的实现类似于更复杂的脚本和编程语言中常见的结构。你可以根据需要使用多种不同类型的循环。

#### “if...then” 语句

最常用的编程结构是条件执行，也就是 `if` 语句。它用于仅在满足特定条件时执行操作。根据你是测试单一项目，还是希望在条件为真时执行一个操作、在条件为假时执行另一个操作，或者希望依次测试多个项目，存在几种变体。

第一个 `if`...`then` 示例测试 `VARIABLE` 是否设置为数字 1。如果是，则使用 `echo` 命令说明它被设置为 1。`fi`（即 if 的反写）随后表示 `if` 语句已完成，可以继续处理后续内容。

```bash
VARIABLE=1
if [ $VARIABLE -eq 1 ] ; then
    echo "The variable is 1"
fi
```

你可以使用等号（`=`）代替 `-eq`，如下面的示例所示。`=` 最适合用于比较字符串值，而 `-eq` 通常更适合比较数字。使用 `else` 语句，如果未满足 `if` 语句的条件（即 `STRING = "Friday"`），可以输出不同的单词。请记住，将字符串放在双引号中是一个好习惯。

```bash
STRING="Friday"
if [ $STRING = "Friday" ] ; then
    echo "WhoooHoo. Friday,"
else
    echo "Will Friday ever get here?"
fi
```

你还可以使用感叹号（`!`）反转测试。在以下示例中，如果 `STRING` 不是 Monday，则输出 "At least it's not Monday"。

```bash
STRING="FRIDAY"
if [ "$STRING" != "Monday" ] ; then
     echo "At least it's not Monday"
fi
```

> **提示：** 在方括号前后各保留一个空格，因为 `[` 实际上是一个位于 `/usr/bin` 中的 Linux 命令（同时也内置于 bash shell 中）。

在以下示例中，`elif`（意为“否则如果”）用于测试额外的条件（`filename` 是文件还是目录）。

```bash
filename="$HOME"

if [ -f "$filename" ] ; then
     echo "$filename is a regular file"
elif [ -d "$filename" ] ; then
     echo "$filename is a directory"
else
     echo "I have no idea what $filename is"
fi
```

从上述示例中可以看出，你要测试的条件放在方括号 `[ ]` 之间。当测试表达式被评估时，它会返回 0（表示真）或 1（表示假）。注意 `echo` 行是缩进的。这是可选的，仅仅是为了使脚本更具可读性。

表 11-2 列出了可测试的条件，这是一个非常实用的参考。（如果你赶时间，可以在命令行键入 `help test` 获取相同的信息。）

#### 表 11-2: 测试表达式的运算符

| 运算符 | 测试内容 |
| :--- | :--- |
| `-a file` | 文件是否存在？（等同于 `-e`） |
| `-b file` | 文件是否为特殊的块设备？ |
| `-c file` | 文件是否为字符特殊文件（例如字符设备）？用于识别串行线路和终端设备。 |
| `-d file` | 文件是否为目录？ |
| `-e file` | 文件是否存在？（等同于 `-a`） |
| `-f file` | 文件是否存在，且是否为常规文件（例如，不是目录、套接字、管道、链接或设备文件）？ |
| `-g file` | 文件是否设置了 set-group-id 位？ |
| `-G file` | 你的组是否拥有该文件？ |
| `-h file` | 文件是否为符号链接？（等同于 `-L`） |
| `-k file` | 文件是否设置了 sticky 位？ |
| `-L file` | 文件是否为符号链接？ |
| `-n string` | 字符串长度是否大于 0 字节？ |
| `-N file` | 文件自上次读取以来是否已被修改？ |
| `-O file` | 你是否拥有该文件？ |
| `-p file` | 文件是否为命名管道？ |
| `-r file` | 你是否可读该文件？ |
| `-s file` | 文件是否存在，且大于 0 字节？ |
| `-S file` | 文件是否存在，且是否为套接字？ |
| `-t fd` | 文件描述符是否连接到终端？ |
| `-u file` | 文件是否设置了 set-user-id 位？ |
| `-w file` | 你是否可写该文件？ |
| `-x file` | 你是否可执行该文件？ |
| `-z string` | 字符串长度是否为 0 字节？ |
| `expr1 -a expr2` | 第一个表达式和第二个表达式是否都为真？ |
| `expr1 -o expr2` | 两个表达式中是否有任一为真？ |
| `file1 -nt file2` | 第一个文件是否比第二个文件新（使用修改时间戳）？ |
| `file1 -ot file2` | 第一个文件是否比第二个文件旧（使用修改时间戳）？ |
| `file1 -ef file2` | 两个文件是否通过硬链接相关联？ |
| `var1 = var2` | 第一个变量是否等于第二个变量？ |
| `var1 -eq var2` | 第一个变量是否等于第二个变量？ |
| `var1 -ge var2` | 第一个变量是否大于或等于第二个变量？ |
| `var1 -gt var2` | 第一个变量是否大于第二个变量？ |
| `var1 > var2` | 第一个变量是否在排序中位于第二个变量之后？ |
| `var1 -le var2` | 第一个变量是否小于或等于第二个变量？ |
| `var1 -lt var2` | 第一个变量是否小于第二个变量？ |
| `var1 < var2` | 第一个变量是否在排序中位于第二个变量之前？ |
| `var1 != var2` | 第一个变量是否不等于第二个变量？ |
| `var1 -ne var2` | 第一个变量是否不等于第二个变量？ |
