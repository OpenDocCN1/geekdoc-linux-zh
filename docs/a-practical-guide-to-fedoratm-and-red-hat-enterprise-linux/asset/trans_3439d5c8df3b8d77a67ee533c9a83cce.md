

作为一个示例，假设你要编写一个程序，该程序可以接受三个选项：

1. `-b` 选项表示程序应忽略输入行开头的空白字符。
2. 如果 `-t` 选项后跟一个目录名，则表示程序应将该目录作为存储临时文件的位置。否则，它应使用 `/tmp`。
3. `-u` 选项表示程序应将所有输出转换为大写。

此外，程序应忽略所有其他选项，并在遇到两个连字符（`--`）时结束选项处理。

问题在于编写程序的那部分代码，该代码用于确定用户提供了哪些选项。下面的解决方案不使用 `getopts`：

```bash
SKIPBLANKS=
TMPDIR=/tmp
CASE=lower
while [ " $1 " = -* ] # [ ] does pattern match
do
    case $1 in
        -b)  SKIPBLANKS=TRUE ;;
        -t)  if [ -d "$2" ]
             then
                  TMPDIR=$2
                  shift
             else
                  echo "$0: -t takes a directory argument." >&2
                  exit 1
             fi ;;
        -u)  CASE=upper ;;
        --)  break ;; # Stop processing options
        *)    echo "$0: Invalid option $1 ignored." >&2 ;;
    esac
    shift
done
```

这个程序片段使用循环来检查并 `shift` 参数，只要参数不是 `--`。只要参数不是两个连字符，程序就会继续循环执行一个 `case` 语句，该语句检查可能的选项。`--` 的 case 标签会跳出 while 循环。`*` 的 case 标签识别任何选项；它作为最后一个 case 标签出现，以捕获任何未知选项，显示错误消息，并允许处理继续。在每次循环迭代中，程序使用 `shift`，以便在下次循环时访问下一个参数。如果一个选项需要参数，程序会使用额外的 `shift` 来跳过该参数。

下面的程序片段使用 `getopts` 处理相同的选项：

```bash
SKIPBLANKS=
TMPDIR=$tmp
CASE=lower

while getopts :bt:u arg
do
    case $arg in
        b)  SKIPBLANKS=TRUE ;;
        t)  if [ -d "$OPTARG" ]
            then
                TMPDIR=$OPTARG
            else
                echo "$0: $OPTARG is not a directory." >&2
                exit 1
            ;;
        u)  CASE=upper ;;
        :)  echo "$0: Must supply an argument to -$OPTARG." >&2
            exit 1 ;;
        \?)  echo "Invalid option -$OPTARG ignored." >&2 ;;
    esac
done
```

在这段代码的版本中，`while` 结构每次控制流转到循环顶部时都会评估 `getopts` 内置命令。`getopts` 内置命令使用 OPTIND 变量来跟踪它下次被调用时要处理的参数的索引。在这个示例中，不需要调用 `shift`。

在脚本的 `getopts` 版本中，case 模式不以连字符开头，因为 `arg` 的值仅为选项字母（`getopts` 去掉了连字符）。此外，`getopts` 识别 `--` 为选项的结束，因此你不需要显式指定它，如第一个示例中的 case 语句所示。

因为你告诉 `getopts` 哪些选项是有效的，哪些需要参数，所以它可以检测命令行中的错误并以两种方式处理它们。此示例在 `optstring` 中使用前置冒号来指定你在代码中检查并处理错误；当 `getopts` 发现无效选项时，它将 `varname` 设置为 ?，将 OPTARG 设置为该选项字母。当它发现缺少参数的选项时，`getopts` 将 `varname` 设置为 :，将 OPTARG 设置为缺少该参数的选项。

`\?` case 模式指定当 `getopts` 检测到无效选项时要采取的操作。`:` case 模式指定当 `getopts` 检测到缺少选项参数时要采取的操作。在这两种情况下，`getopts` 都不写入错误消息，而是将该任务留给你。

如果你从 `optstring` 中省略前置冒号，无效选项和缺少选项参数都会导致将字符串 `?` 分配给 `varname`；OPTARG 会被设置，`getopts` 会向标准错误写入其自己的诊断消息。通常，这种方法不太理想，因为你对用户看到的内容控制较少。

使用 `getopts` 并不一定会使你的程序更短。它的主要优势是提供统一的编程接口，并强制执行标准的选项处理。

## 内置命令的部分列表

表 27-6 列出了某些 `bash` 内置命令。你可以使用 `type`（第 1041 页）来查看某个命令是否运行内置命令。关于如何显示内置命令完整列表的说明，请参见第 170 页的“Listing `bash` builtins”。

**表 27-6: bash 内置命令**

| 内置命令 | 功能 |
| :--- | :--- |
| `:` | 返回 0 或 `true`（空内置命令；第 1037 和 1049 页） |
| `. (dot)` | 将 shell 脚本作为当前进程的一部分执行（第 332 页） |
| `bg` | 将挂起的任务放入后台（第 348 页） |
| `break` | 退出循环控制结构（第 1005 页） |
| `cd` | 更改到另一个工作目录（第 185 页） |
| `continue` | 开始循环控制结构的下一次迭代（第 1005 页） |
| `echo` | 显示其参数（第 219 页） |
| `eval` | 扫描并评估命令行（第 1051 页） |
| `exec` | 代替当前进程执行 shell 脚本或程序（第 1045 页） |
| `exit` | 退出当前 shell（通常与交互式 shell 中的 `CONTROL-D` 相同；第 1029 页） |
| `export` | 将变量设为环境变量（第 1032 页） |
| `fg` | 将任务从后台带到前台（第 347 页） |
| `getopts` | 解析 shell 脚本的参数（第 1052 页） |
| `jobs` | 显示后台任务列表（第 346 页） |
| `kill` | 向进程或任务发送信号（第 465 页） |
| `pwd` | 显示工作目录的名称（第 143 页） |
| `read` | 从标准输入读取一行（第 1041 页） |
| `readonly` | 声明变量为 `readonly`（第 356 页） |
| `set` | 设置 shell 标志或位置参数；如果没有参数，则列出所有变量（第 400 和 1024 页） |
| `shift` | 提升每个位置参数（第 1025 页） |
| `test` | 比较参数（第 983 页） |
| `times` | 显示当前 shell 及其子进程的总时间 |
| `trap` | 捕获信号（第 1047 页） |
| `type` | 显示每个参数将如何被解释为命令（第 1041 页） |
| `umask` | 设置并显示文件创建掩码（第 469 页） |
| `unset` | 移除变量或函数（第 356 页） |
| `wait` | 等待后台进程终止 |

## 表达式

表达式由常量、变量和 shell 可以处理以返回值的运算符组成。本节涵盖算术、逻辑和条件表达式以及运算符。第 1059 页的表 27-8 列出了 *bash* 运算符。

## 算术评估

Bourne Again Shell 可以执行算术赋值并评估许多不同类型的算术表达式，全部使用整数。shell 通过多种方式执行算术赋值。一种方式是使用 *let* 内置命令的参数：

```bash
$ let "VALUE=VALUE * 10 + NEW"
```

在前面的示例中，变量 **VALUE** 和 **NEW** 持有整数值。在 *let* 语句中，变量名称前不需要使用美元符号（$）。双引号必须包围单个参数或表达式，该表达式包含**空格**。由于大多数表达式包含**空格**且需要引号，*bash* 接受 `((expression))` 作为 `let ' expression '` 的同义词，从而消除了对引号和美元符号的需求：

```bash
$ ((VALUE=VALUE * 10 + NEW))
```

你可以在任何允许 `(( ))` 命令的地方使用任一形式，并且可以移除**空格**。在这些示例中，星号 `(*)` 不需要引号，因为 shell 不会对赋值右侧执行路径名扩展（第 354 页）：

```bash
$ let VALUE=VALUE*10+NEW
```

由于 *let* 的每个参数都被评估为单独的表达式，你可以在单行上为多个变量赋值：

```bash
$ let "COUNT = COUNT + 1" VALUE=VALUE*10+NEW
```

你必须使用逗号来分隔双括号内的多个赋值：

```bash
$ ((COUNT = COUNT + 1, VALUE=VALUE*10+NEW))
```

