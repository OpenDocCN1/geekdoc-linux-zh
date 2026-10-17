
# Shell 编程

## check_test 脚本示例

```bash
$ cat -n check_test
1  #
2  # check_test
3  # A sample program using the test command
4  #
5  echo # skip a line
6  echo "Are you OK?" # prompt user
7  echo "Input Y for yes and N for no:" # store response in answer
8  read answer
9  if test "$answer" = Y # test user entered Y
10 then
11 echo "Glad to hear that!" # display the message
12 else # user entered N
13 echo "Go home!" # display the message
14 fi
15 echo # skip a line
16 exit 0 # end of the program, exit
```

1. `check_test` 脚本提示用户输入 (Y)es 或 (N)o，然后读取用户的回答。
2. 如果用户的回答是字母 Y，`test` 命令返回 0，如果条件为真，则执行 `if` 的体。显示消息 "Glad to hear that!"，并跳过 `else` 体。
3. 用户输入的除字母 Y 以外的任何输入都会导致条件失败；因此，跳过 `if` 的体并执行 `else`。显示消息 "Go home!"。

### 使用括号调用

Shell 为你提供了另一种调用 `test` 命令的方法。你可以使用方括号 (`[` 和 `]`) 来代替单词 `test`。因此，`if` 语句可以写成：

```bash
if test "$Variable" = value
# 或
if [ "$Variable" = value ]
```

## 测试不同类别

通过使用 `test` 命令，你可以测试不同类别的内容，包括以下内容：数值值、字符串值和文件。这些类别中的每一个将在后续章节进行解释。

## 数值值

你可以使用 `test` 命令以代数方式测试（比较）两个整数。你还可以将比较数字的表达式与逻辑运算符结合使用。格式如下：

```bash
test expression_1 logical_operator expression_2
```

逻辑运算符如下：

- **逻辑与运算符 (`-a`)**：如果两个表达式都为真，`test` 命令返回 0（条件码为真）。
- **逻辑或运算符 (`-o`)**：如果一个或两个表达式为真，`test` 命令返回 0（条件码为真）。
- **逻辑非运算符 (`!`)**：如果表达式为假，`test` 命令返回 0（条件码为真）。

用于比较数值变量的运算符总结在表 12.5 中。

### 表 12.5 test 命令数值运算符

| 运算符 | 示例 | 含义 |
| :--- | :--- | :--- |
| `-eq` | `number1 -eq number2` | number1 是否等于 number2? |
| `-ne` | `number1 -ne number2` | number1 是否不等于 number2? |
| `-gt` | `number1 -gt number2` | number1 是否大于 number2? |
| `-ge` | `number1 -ge number2` | number1 是否大于或等于 number2? |
| `-lt` | `number1 -lt number2` | number1 是否小于 number2? |
| `-le` | `number1 -le number2` | number1 是否小于或等于 number2? |

假设你想编写一个脚本接受三个数字作为输入（命令行参数）并显示三个中最大的一个。使用 `cat` 命令，图 12.16 显示了编写此程序的方法，名为 `largest`。

1. 当你运行 `largest` 程序时，它会等待你输入三个数字。然后你的输入将通过 `if-then-elif` 结构找到最大的那个。
2. 如果前两个数字都不是最大的，则第一个语句失败，下一个 `elif` 失败，你的程序将到达 `else` 语句。不再进行检查。如果最大的既不是第一个也不是第二个，它必须是第三个。

尝试运行 `largest` 的示例：

```bash
$ chmod +x largest  # Change it into executable file.
$ largest           # Run the program.
Enter three numbers and I will show you the largest of them.
10 20 30
The largest number is: 30
Done!
```

### 图 12.16 一个名为 largest 的 Shell 程序

```bash
$ cat -n largest
1  #
2  # largest.
3  # A sample program using test command
4  # This program accepts three numbers and shows the largest of them
5  #
6  echo # skip a line
7  echo "Enter three numbers and I will show you the largest of them:"
8  read num1 num2 num3
9  if [ "$num1" -gt "$num2" -a "$num1" -gt "$num3" ]
10 then
11 echo "The largest number is: $num1"
12 elif [ "$num2" -gt "$num1" -a "$num2" -gt "$num3" ]
13 echo "The largest number is: $num2"
14 else
15 echo "The largest number is: $num3"
16 # end of program message
17 echo "Done!"
18 # skip a line
19 exit 0
```

> **思考**：如何改进 `largest` 程序？例如，你可以使用更少的代码行吗？（例如，你必须在 `if`、`elif` 和 `else` 的体中重复 `echo` 命令吗？）你可以进行错误检查吗？（如果你输入两个数字会怎样？）

## 字符串值

你也可以用 `test` 命令比较（测试）字符串。`test` 命令为字符串比较提供了一套不同的运算符。这些运算符总结在表 12.6 中。以下示例显示了带参数的 `test` 命令。

### 表 12.6 test 命令字符串运算符

| 运算符 | 示例 | 含义 |
| :--- | :--- | :--- |
| `=` | `string1 = string2` | string1 是否匹配 string2? |
| `!=` | `string1 != string2` | string1 是否不匹配 string2? |
| `-n` | `-n string` | 字符串包含字符（非零长度）吗? |
| `-z` | `-z string` | 字符串为空字符串（零长度）吗? |

首先测试空变量：

```bash
$ STRING=          # Declare a null variable.
$ test -z $STRING  # Test for zero length.
test: Argument expected  # Error message.
$                  # The prompt reappears.
```

1. Shell 用一个空字符串替换了 `$STRING`，因此产生了错误消息。
2. 将字符串变量括在引号内可以确保正确的测试，即使变量包含空格或制表符。

尝试带引号的 `$STRING`：

```bash
$ test -z "$STRING"  # Test for zero length.
```

此测试命令返回 0（真），这意味着变量 `$STRING` 包含空字符串。

在另一个示例中，命令在 `$` 提示符处输入。如果命令未完成，Shell 显示二级提示符 (`>`) 并等待你完成命令：

```bash
$ DATE1=date  # Initialize DATE1.
$ DATE2=date  # Initialize DATE2.
$ if test "$DATE1" = "$DATE2"  # Test for equality.
> then         # 如果代码尚未完成，shell 显示第二个提示符。
> echo "STOP! The computer clock is dead!"
> else         # 开始执行 else 体.
> fi
```

这个测试的结果为假。因此，执行 `else` 体并显示消息。存储在 `DATE1` 和 `DATE2` 中的值可能相等吗？

## 文件

你可以使用 `test` 命令测试文件特性，例如文件大小、文件类型和文件权限。可以检查超过 10 种文件属性；这里介绍了其中几个。表 12.7 总结了文件测试运算符。以下示例显示了与文件结合的 `test` 命令的使用。命令直接在 `$` 提示符处输入。

### 表 12.7 测试命令文件测试操作符

| 操作符 | 示例 | 含义 |
| :--- | :--- | :--- |
| `-r` | `-r filename` | 文件是否存在且可读？ |
| `-w` | `-w filename` | 文件是否存在且可写？ |
| `-s` | `-s filename` | 文件是否存在且长度不为零？ |
| `-f` | `-f filename` | 文件是否存在且不是目录文件？ |
| `-d` | `-d filename` | 文件是否存在且是一个目录文件？ |

假设你有一个名为 `myfile` 的文件，且对该文件只有读取权限。让我们输入以下命令并查看输出：

```bash
$ FILE=myfile                    # 初始化 FILE 变量。
$ if -r "$FILE"                  # 检查文件是否可读。
> then                           # 次级提示符。
> echo "READABLE"                # 显示消息。
> elif test -w "$FILE"           # 检查文件是否可写。
> then                           # 次级提示符。
> echo "WRITABLE"                # 显示消息。
> else                           # 次级提示符。
> echo "Read and Write Access Denied"
$ fi                             # 结束 if 结构。
READABLE
$                                # 回到主提示符。
```

1. 一旦你输入 `fi`（`if` 结构的结束标志），Shell 就会执行命令、产生输出并显示 `$` 提示符。
2. 第一个测试检查对 `myfile` 的读取权限。由于你有读取权限，`test` 命令返回 0（真），条件成立。因此只执行了第一个 `if` 的体，并显示消息 READABLE。
3. 如果你对 `myfile` 只有写入权限，则回显消息 WRITABLE。
4. 如果你对 `myfile` 没有写入或读取权限，且 `if` 和 `elif` 条件均失败，则会显示消息 Read and Write Access Denied.

图 12.17 显示了 `svi` 脚本文件的另一个版本（svi4），它会检查指定文件是否存在，只有当文件存在时才会执行 `cp` 和 `vi` 命令。

运行这个版本的 `svi` 程序 `svi4`：

```bash
$ svi4 xyz        # 运行，指定一个不存在的文件 xyz。
File not found. Try again.
$ svi4            # 运行；未指定文件。
You must specify a filename. Try again.
$                 # 回到提示符。
```

### 图 12.17 svi 脚本文件的另一个版本：svi4

```bash
$ cat -n svi4
1  #
2  # svi4
3  # 保存并调用 vi
4  # 使用 test 命令和文件测试操作符的示例程序
5  # 版本 4：此版本检查文件是否存在
6  #
7  DIR=$HOME/keep      # 将 keep 路径赋值给 DIR
8  if test $# -eq 1    # 检查命令行参数的数量
9  then
10 if test -f "$1"     # 检查文件是否存在
11 then
12 cp "$1" "$DIR"      # 将指定的文件复制到 keep
13 vi "$1"             # 使用指定的文件调用 vi
14 else
15 echo "File not found. Try again"
16 fi
17 else
18 echo "You must specify a filename. Try again."
19 fi                  # if 语句的结束
20 exit 0              # 程序的结束，退出
```

1. 为了检查 `if` 条件，使用了 `test` 单词而不是方括号。
2. 该程序使用了嵌套 `if` 结构（`if` 内部嵌套另一个 `if`）。
3. 如果未找到指定的文件，则会显示 `File not found. Try again.`。
4. 如果找到了指定的文件，会将文件复制到 `keep` 目录并调用 `vi` 编辑器。
5. 如果命令行上没有指定文件名，第一个条件失败，会显示 `You must specify a filename. Try again.`。

## 12.3.6 参数替换

Shell 提供了参数替换功能，允许你测试参数的值并根据指定的选项更改其值。这在 Shell 编程中非常有用，当你想要检查变量是否已赋值时。例如，当你在文件中执行命令时，确保用户已输入了内容。美元符号 (`$`)、大括号 (`{}`)、冒号 (`:`)、选项和单词的格式如下：

```bash
${parameter:option word}
```

选项字符决定了你打算对单词执行的操作。选项字符由 `-`、`=`、`+`、`?` 指定。这些选项的执行方式取决于变量是否为空。

### 空变量定义

如果变量为空（空值），则是一个空变量：

- `EMPTY=`：这是一个空变量。
- `EMPTY=""`：这是一个空变量。
- `EMPTY=''`：这是一个空变量。

要创建一个空变量，在引号之间留空。

### 表 12.8 变量选项

| 变量选项 | 含义 |
| :--- | :--- |
| `$variable` | 变量中的值。 |
| `${variable}` | 变量中的值。 |
| `${variable:-string}` | 如果未设置或为空，使用 string。 |
| `${variable:+string}` | 如果设置且不为空，使用 string。 |
| `${variable:=string}` | 如果未设置或为空，赋值为 string。 |
| `${variable:?string}` | 如果为空，则打印 string 并退出。 |

将变量（参数）放在大括号内可以防止后续变量名字符引起的任何冲突。以下示例说明了这一点。假设你想更改名为 `FILE` 的变量名为 `memo`。

```bash
$ echo $FILE        # 检查 FILE 中的内容。
$ mv $FILE          # 更改为 memo。
Usage: mv
$                   # 回到提示符。
```

该命令没有执行，因为 Shell 认为 `$FILE` 变量不存在（此处原文逻辑可能指变量名拼接歧义，加大括号可避免）。

```bash
$ mv ${FILE} memo   # 更改为 memo。
$                   # 完成；提示符返回。
```

该命令执行了，因为 Shell 在这种情况下替换了变量名为 `memo`。

### `${parameter:-word}` - 连字符选项

连字符选项意味着如果变量（参数）已设置且**不为空**，则使用其值。否则，如果变量为空（空值）或未设置，则替换为 word。例如：

```bash
$ FILE=                      # 这是一个空变量。
$ echo ${FILE:-/usr/dev/xfile}  # 显示 FILE 值。
/usr/dev/xfile
$ echo "$FILE"               # 检查 FILE 变量。
                             # 它是空的。
$                            # 回到提示符。
```

1. Shell 解析 `FILE`；它是空的，因此选项替换为 `/usr/dev/xfile` 字符串，并传递给 `echo` 命令显示。
2. `FILE` 仍然是一个空变量。
