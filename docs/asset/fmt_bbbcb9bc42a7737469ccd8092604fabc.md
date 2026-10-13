
```
if [ expression ]
then
( body )
fi

if [ expression ]
then
( body )
else
( body )
fi

if [ expression ]
then
( body )
elif [ expression ]
then
( body )
else
( body )
fi
```

在这种类型的循环中，会对每个表达式进行测试。根据测试结果，执行随后采取的操作之一。

表 12-2 列出了在 `if` 语句中括号之间可能存在的测试表达式。左括号本身开始语句的“test”部分。实际上，前面的每个 `if` 语句都可以重写为不带括号的形式，如下所示：

```
if test expression
```

当表达式被评估时，结果要么是 0（表示“真”），要么是 1（表示“假”）。

### 表 12-2：测试表达式的运算符

| 运算符 | 测试的是什么？ |
|---|---|

| `-b file` | 文件是否是块特殊文件（例如块设备）？用于标识磁盘和磁带设备。 |
| `-c file` | 文件是否是字符特殊文件（例如字符设备）？用于标识串行线和终端设备。 |
| `-d file` | 文件是否是一个目录？ |
| `-e file` | 文件是否存在？ |
| `-f file` | 文件是否存在，并且它是一个常规文件（例如不是目录、套接字、管道、链接或设备文件）？ |
| `-g file` | 文件是否设置了 set-group-id 位？ |
| `-G file` | 文件是否存在且其组所有权与当前用户的主组相同？ |
| `-k file` | 文件是否设置了粘滞位？ |
| `-L file` | 文件是否是一个符号链接？ |
| `-n string` | 字符串长度是否大于 0 字节？ |
| `-O file` | 文件是否存在且当前用户拥有它？ |
| `-p file` | 文件是否是一个命名管道？ |
| `-r file` | 文件是否存在且可读？ |
| `-s file` | 文件是否存在且大小大于 0 字节？ |
| `-S file` | 文件是否存在且是一个套接字？ |
| `-t fd` | 文件描述符是否打开？ |
| `-u file` | 文件是否设置了 set-user-id 位？ |
| `-w file` | 文件是否存在且可写？ |
| `-x file` | 文件是否存在且可执行？ |
| `-z string` | 字符串长度是否为 0 字节？ |
| `expr1 -a expr2` | 第一个表达式和第二个表达式是否都为真？ |
| `expr1 -o expr2` | 两个表达式中是否有一个为真？ |
| `file1 -nt file2` | 第一个文件是否比第二个文件新（使用修改时间戳）？ |
| `file1 -ot file2` | 第一个文件是否比第二个文件旧（使用修改时间戳）？ |
| `file1 -ef file2` | 两个文件是否通过链接（硬链接或符号链接）关联？ |
| `var1 -eq var2` | 第一个变量是否等于第二个变量？ |
| `var1 -ge var2` | 第一个变量是否大于或等于第二个变量？ |
| `var1 -gt var2` | 第一个变量是否大于第二个变量？ |
| `var1 -le var2` | 第一个变量是否小于或等于第二个变量？ |
| `var1 -lt var2` | 第一个变量是否小于第二个变量？ |
| `var1 -ne var2` | 第一个变量是否不等于第二个变量？ |

以下是一些演示 `if` 语句和测试表达式用法的示例：

```
if [ -x /sbin/ifconfig ]
if [ $4 -eq "n1" ]
if [ $# -gt 2 ]
if [ -z $HOSTNAME ]
```

在之前的示例中，第一个语句检查 `/sbin/ifconfig` 程序是否可执行。第二个示例检查字符串值 `n1` 是否等于存储在 `$4`（第四个命令行参数）中的值。下一行检查命令行参数的数量（由 `$#` 变量表示）是否大于两个。最后一个示例判断变量 `$HOSTNAME` 是否为空。

## 用于嵌套 if 语句的 case 命令

另一个常用的结构是 `case` 命令。类似于编程语言中的 `switch` 语句，它可以取代多个嵌套的 `if` 语句。`case` 语句的一般形式如下：

```
case "VAR" in
    Result1)     { body }
        ;
    Result2)     { body }
        ;
    *)           { body }
        ;
esac
```

`case` 命令的示例如下。这段代码片段根据 `/etc/passwd` 文件中第七个（冒号分隔的）字段报告的用户默认 `shell` 来设置 `TYPE` 和 `RCFILE` 变量：

```
Shell=`grep "^$USER:" /etc/passwd | awk -F: '{ print $7 }'`
    case "$Shell" in
        /bin/sh)     TYPE=Bourne
            RCFILE=".profile"
            ;;
        /bin/csh)    TYPE=C
            RCFILE=".cshrc"
            ;;
        /bin/bash)    TYPE=Bourne
            RCFILE=".bashrc"
            ;;
        /bin/tcsh)    TYPE=C
            RCFILE=".tcshrc"
            ;;
        *)    TYPE=Other
            RCFILE="unknown"
            ;;
    esac
```

星号 (`*`) 用作万能匹配。如果在循环过程中没有匹配到其他任何条目，则匹配星号，并将值设置为 `unknown`。

## while . . . do 和 until . . . do 循环

另外两种可能的循环结构是 `while` . . . `do` 循环和 `until` . . . `do` 循环。每种结构的形式如下所示：

```
while condition    do
    ( body )
done

until condition    do
    { body }
done
```

在 `while` 循环中，条件通常是一个测试语句，但也可以用于读取输入，直到遇到文件结束符 (`<EOF>`)。如果使用测试条件，则循环体执行的条件评估为假（返回码为 1）时结束。这里包含一个示例：

```
while read COL1 COL2 COL3 COL4
do
     echo -n " |      X    $COL2     |     $COL3     " > /home/ben/DB
     echo " |    $COL4     |     $COL1     X | " >> /home/ben/DB
done
```

此循环从键盘读取值（每次四个一组），重新排列列顺序，并以特定格式输出到文件。

`until` 循环执行循环体中的代码，直到测试评估为真（返回码为 0）。此时，循环退出。

```
COUNT=1
until [ $COUNT -eq 34 ]
do
    DIR=/home/grd/proj/$COUNT
    if [ ! -d $DIR ]
    then
        mkdir $DIR
        cp /home/grd/proj/template $DIR/file_def
```

前面的循环会创建一个目录（如果该目录尚不存在），并将一个模板文件复制到其中。此过程会重复执行，直到 `COUNT` 变量的值等于 34（需要 33 次迭代）。

## 尝试一些简单的 shell 脚本

有时候，最简单的脚本反而最实用。如果你经常反复输入相同的命令序列，那么将这些命令（只需一次！）存储到文件中是合理的。以下是一些简单但实用的 shell 脚本示例。

### 一个简单的备份脚本

如果你过去两年一直在为某个研究项目收集数据，你希望保留工作的备份副本，以防原始文件发生不可预见的意外。与其每次想要备份时都手动输入完整的命令，不如将命令存储在一个 shell 脚本中：

```bash
#!/bin/bash
#
mt /dev/rft0 rew
cd /home/rp008a/data
tar cvf /dev/rft0
mt /dev/rft0 rewoffl
exit 0
```
