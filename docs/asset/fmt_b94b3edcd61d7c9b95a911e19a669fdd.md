
### EXPLANATION

- 1. `read` 命令接受一行用户输入并将输入分配给变量 `answer`。
- 2. `read` 命令从用户接受输入并将输入的第一个词分配给变量 `first`，第二个词分配给变量 `middle`，其余所有词直到行尾分配给变量 `last`。

# EXAMPLE 8.4

(The Script)

```
#!/bin/sh

# Scriptname: printer_check

# Script to clear a hung up printer for SVR4

1 if [ $LOGNAME != root ]
then
    echo "Must have root privileges to run this program"
    exit 1
fi

2 cat << EOF
Warning: All jobs in the printer queue will be removed.
Please turn off the printer now. Press Enter when you
are ready to continue. Otherwise press Ctrl-C.
EOF

3 read ANYTHING    # Wait until the user turns off the printer
echo

4 /etc/init.d/lp stop    # Stop the printer
```

```
5  rm -f /var/spool/lp/SCHEDLOCK /var/spool/lp/temp
   echo
   echo "Please turn the printer on now."

6  echo "Press Enter to continue"

7  read ANYTHING        # Stall until the user turns the printer back on
   echo                # A blank line is printed

8  /etc/init.d/lp start  # Start the printer
```

### EXPLANATION

- 1. 检查用户是否为 `root`。如果不是，则发送错误并退出。
- 2. 创建一个 here 文档。警告信息显示在屏幕上。
- 3. `read` 命令等待用户输入。当用户按下 Enter 时，变量 `ANYTHING` 接受所键入的内容。该变量未用于任何用途。此处的 `read` 用于等待用户关闭打印机，返回后按下 Enter。
- 4. `lp` 程序停止打印机守护进程。
- 5. 在调度程序重新启动之前，必须删除 `SCHEDLOCK` 文件，以及 `/var/spool/lp` 中的临时文件。
- 6. 提示用户在准备好时按下 Enter。
- 7. 用户键入的任何内容都被读入变量 `ANYTHING`，并在按下 Enter 后程序将恢复执行。
- 8. `lp` 程序启动打印守护进程。

# 8.3 算术

算术并未内置于 Bourne shell。如果需要执行简单的整数算术计算，UNIX `expr` 命令在 Bourne shell 脚本中最常用。对于浮点算术，可以使用 `awk` 或 `bc` 程序。由于算术未内置，shell 在循环迭代多次时的性能会下降。每次在循环机制中递增或递减计数器时，都需要 fork 另一个进程来处理算术。

### 8.3.1 整数算术和 expr 命令

`expr` 命令是一个表达式处理程序。当用于计算算术表达式时，它可以执行简单的整数运算（参见表 8.2）。其每个参数必须用空格分隔。支持 `+`、`−`、`*`、 `/`、和 `%` 运算符，并且正常的编程结合性和优先级规则适用。

# 表 8.2 expr 命令算术运算符

| 运算符 | 功能 |
|---|---|
| * | 乘法 |
| / | 除法 |
| % | 取模 |
| + | 加法 |
| - | 减法 |

### 示例 8.5

```
1 $ expr 1 + 4
5

2 $ expr 1+4
1+4

3 $ expr 5 + 9 / 3
8

4 $ expr 5 * 4
expr: syntax error

5 $ expr 5 \* 4 - 2
18

6 $ expr 11 % 3
2

7 $ num=1
$ num=`expr $num + 1`
$ echo $num
2
```

# 解释

+ 1 `expr` 命令计算表达式。两个数字相加。
+ 2 因为运算符之间没有空格，表达式被当作字符串求值。
+ 3 加法和除法组合使用。先执行除法，然后执行加法。
+ 4 星号 (`*`) 被 shell 当作其通配符之一进行求值，导致 `expr` 命令失败。
+ 5 星号 (`*`) 用反斜杠转义以防止 shell 解释。`expr` 命令执行算术运算。
+ 6 取模运算符 (`%`) 返回除法后的余数。
+ 7 变量 `num` 被赋值为 1。`expr` 命令将 1 加到变量的值上并将结果赋给 `num`。`num` 的值被回显到屏幕上。

### 8.3.2 浮点运算

如果需要执行更复杂的计算，`bc`、`awk` 和 `nawk` 工具很有用。

### 示例 8.6

```
(The Command Line)

1 $ n=`echo "scale=3; 13 / 2" | bc`
$ echo $n
6.500

2 $ n=`bc << EOF
scale=3
13/2
EOF`
$ echo $n
6.500

3 $ product=`nawk -v x=2.45 -v y=3.123 'BEGIN{printf "%.2f\n",x*y}'`
$ echo $product
7.65
```

# 解释

+ 1 `echo` 命令的输出被管道传输到 `bc` 程序。`scale` 被设置为 3，即小数点右侧将打印的有效数字位数。计算是 13 除以 2。整个管道被反引号括起来。命令替换将被执行并将输出赋给变量 `n`。
+ 2 此示例在反引号中使用 here 文档来执行与第一个示例相同的功能。命令的输出将被赋给变量 `n`，然后用 `echo` 命令显示。
+ 3 `nawk` 程序从命令行传入的参数列表获取其值，`x=2.45` `y=3.123`。(`-v` 开关适用于 `nawk`，不适用于 `awk`。) 在数字相乘后，`printf` 函数格式化并打印结果，小数点右侧的精度为两位。输出被赋给变量 `product`。

# 8.4 位置参数和命令行参数

信息可以通过命令行传递到脚本中。脚本名之后每个由空白分隔的单词称为一个参数。

命令行参数可以在脚本中使用位置参数引用；例如，`$1` 表示第一个参数，`$2` 表示第二个参数，`$3` 表示第三个参数，以此类推。`$#` 变量用于测试参数的数量，而 `$*` 用于

# 解释

+ 1. 在 `greetings` 脚本中，位置参数 `$0` 引用脚本名，`$1` 引用第一个命令行参数，`$2` 引用第二个命令行参数。
+ 2. `greetings` 脚本在未传递任何参数的情况下执行。输出说明脚本名为 `greetings`（脚本中的 `$0`），并且 `$1` 和 `$2` 从未被赋予任何值；因此它们的值为空，什么也不会打印。
+ 3. 这次传递了一个参数 `Tommy`。`Tommy` 被赋给位置参数 1。
+ 4. 输入了两个参数 `Tommy` 和 `Kimberly`。`Tommy` 被赋给 `$1`，`Kimberly` 被赋给 `$2`。

#### 8.4.1 set 命令和位置参数

带参数的 `set` 命令会重置位置参数。¹ 一旦重置，旧的参数列表就会丢失。要取消所有位置参数，请使用 `set --`。`$0` 始终是脚本的名称。

### 示例 8.8

```
(The Script)

#!/bin/sh

# Scriptname: args

# Script to test command-line arguments

1 echo The name of this script is $0.
2 echo The arguments are $*.
3 echo The first argument is $1.
4 echo The second argument is $2.
5 echo The number of arguments is $#.
6 oldargs=$*      # Save parameters passed in from the command line
7 set Jake Nicky Scott   # Reset the positional parameters
8 echo All the positional parameters are $*.
9 echo The number of positional parameters is $#.
10 echo "Good-bye for now, $1"
11 set `date`      # Reset the positional parameters
12 echo The date is $2 $3, $6.
```
