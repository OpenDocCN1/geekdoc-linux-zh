
```bash
$ read2
Enter a command: xxx
./read2: line 2: xxx: command not found
Thanks
```

`read3` 脚本将值读入三个变量中。`read` 内置命令将每个单词（一个非空字符序列）分配给每个变量：

```bash
$ cat read3
read -p "Enter something: " word1 word2 word3
echo "Word 1 is: $word1"
echo "Word 2 is: $word2"
echo "Word 3 is: $word3"

$ read3
Enter something: this is something
Word 1 is: this
Word 2 is: is
Word 3 is: something
```

当你输入的单词比 `read` 指定的变量多时，`read` 会为每个变量分配一个单词，所有剩余单词都进入最后一个变量。`read` 和 `read2` 分别将第一个单词和所有剩余单词分配给它们各自处理的变量。在接下来的示例中，`read` 接受五个单词并进入三个变量，将第一个单词分配给第一个变量，第二个单词分配给第二个变量，剩下的三个单词分配给第三个变量：

```bash
$ read3
Enter something: this is something
Word 1 is: this
Word 2 is: is
Word 3 is: something
```

### 表 28-7：read 选项

| 选项 | 说明 |
| :--- | :--- |
| `a` | 将单词分配给数组变量 |
| `d` | 设置输入分隔符（默认为空格） |
| `e` | 如果到达 EOF 则退出状态为 0 |
| `n` | 读取的字符数 |
| `p` | 在读取前显示提示字符串 |
| `r` | 启用反斜杠转义解释 |
| `t` | 每行读取指定数量字符 |
| `u` | 从指定的文件描述读取 |

## exec: 执行命令

`exec` 主要有两个用途：在不创建进程的情况下运行命令，以及在脚本内重定向标准输入、输出或错误的文件描述（第 911 页）。当 shell 执行内置命令时，它会创建一个进程。新进程从父进程继承环境（全局或导出）变量，但不会继承父进程未导出的变量。（更多信息请参见第 916 页的“变量的局部性”。）相比之下，`exec` 替换（覆盖）当前进程执行命令。

### exec 与 . (dot)

由于 `exec` 在原始进程的环境中运行命令，它与 `. (dot)` 命令（第 269 页）相似。然而，与只能运行 shell 脚本的 `. (dot)` 命令不同，`exec` 可以运行脚本和编译后的程序。

### 可选

每当你重定向输入时，shell 都会打开输入文件并将读取指针置于开头：

```bash
$ read line1 < names; echo $line1; read line2 < names; echo $line2
```

Alice Jones

Alice Jones

这里每次 `read` 都打开 `names` 并从头开始。在接下来的示例中，`names` 被作为进程创建的子 shell 的标准输入打开。每个 `read` 读取连续的标准输入。

```bash
$ (read line1; echo $line1; read line2; echo $line2) < names
```

Alice Jones

Robert Smith

另一种获得相同效果的方法是通过 `exec` 打开输入文件并保持打开（参见第 911 页的“文件描述符”）：

```bash
$ exec 3-< names
$ read -u3 line1; echo $line1; read -u3 line2; echo $line2
```

Alice Jones

Robert Smith

`$ exec 3<&`

在运行完成后它会将控制权返回给原始脚本，而 `exec` 则不会。最后，该命令允许新程序访问本地变量，而 `exec` 则不会。

## exec 运行命令

用于运行命令的内置命令 `exec` 具有如下语法：

`exec command arguments`

## exec 不返回控制权

因为当你使用 `exec` 时 shell 不会创建新进程，所以命令运行得更快。但是，由于 `exec` 不会将控制权返回给原始程序，因此它只能作为脚本中想要运行的最后一个命令。下面的脚本显示了控制权没有返回给脚本：

```bash
$ cat exec_demo

who
date
echo "This line is never displayed."

$ exec_demo

jenny pts/7 May 30 7:05 (bravo.example.com)
hls pts/1 May 30 6:59 (0.0)
Mon May 30 11:42:56 PDT 2005
```

下一个示例是 `out` 脚本 (883) 的修改版本，它使用 `exec` 来执行最后的脚本运行。由于 `out` 运行 `cat` 或 `less` 并终止，新名为 `out2` 的版本同时使用 `exec` 配合 `cat` 和 `less`：

```bash
$ cat out2
if [ $ -eq 0 ]
then
    echo "Usage: out2 [-v] filenames" 1>&2
    exit 1
fi
if [ "$1" = "-" ]
then
    shift
    exec less "$@"
else
    exec cat -- "$@"
fi
```

## exec 重定向输入和输出

`exec` 的第二个主要用途是在脚本中重定向文件描述符（包括标准输入、输出或错误）。接下来的命令允许脚本后续所有本应来自标准输入的输入重定向到名为 `infile` 的文件：

```bash
exec < infile
```

同样，下面的命令分别将标准输出和标准错误重定向到 `outfile` 和 `errfile`：

```bash
exec > outfile 2> errfile
```

当你像这样使用 `exec` 时，当前进程不会被新进程替换，`exec` 后面可以跟在脚本中的其他命令。

```bash
/dev/tty
```

当你将脚本的输出重定向到文件时，必须确保用户能看到脚本显示的任何提示。`/dev/tty` 设备是用户正在工作的屏幕的别名；你可以使用此设备来引用用户的屏幕，而无需知道它是哪种设备。（`tty` 工具会显示你正在使用的设备名称。）通过将脚本的输出重定向到 `/dev/tty`，你可以确保提示和消息会发送到用户的终端，无论用户登录的是哪个终端。如果脚本的标准输出和标准错误被重定向，发送到 `/dev/tty` 的消息将不会被转移。

`to_screen1` 脚本将输出发送到三个地方：标准输出、标准错误和用户的屏幕。当它在标准输出和标准错误重定向的情况下运行时，`to_screen1` 将消息显示到用户屏幕上的 `/dev/tty`。`out` 和 `err` 文件保存发送到标准输出和标准错误的输出。

```bash
$ cat to_screen1
echo "message to standard output"
echo "message to standard error" 1>&2
echo "message to the user" > /dev/tty
```

```bash
$ to_screen1 > 2> err
$ cat out
message to the user
message to standard output
$ cat err
message to standard error
```

下面的命令将脚本的输出重定向到用户的屏幕：

```bash
exec > /dev/tty
```

将此命令放在之前脚本的开头会改变输出的去向。在 `to_screen2` 中，`exec` 将输出重定向到用户屏幕，因此 `/dev/tty` 是多余的。在执行 `exec` 命令后，所有发送到标准输出的输出都会进入 `/dev/tty`（屏幕）。标准错误不受影响。

```bash
$ cat to_screen2
exec < /dev/tty
echo "message to standard output"
echo "message to standard error" 1>&2
echo "message to the user" > /dev/tty

$ to_screen2 > out

message to standard output

message to the user
```

使用 `exec` 重定向输出到 `/dev/tty` 的缺点是后续输出会被重定向，除非你在脚本中再次使用 `exec`。你也可以重定向输入（标准输入），使其来自 `/dev/tty`（键盘）：

```bash
read name < /dev/tty
```

或者

```bash
exec < /dev/tty
```

## trap: 捕获信号

`信号`是向进程报告情况的机制。Linux 使用信号来报告用户生成的中断（例如按下中断键）以及错误的系统调用、断管道、非法指令和其他情况。`trap` 内置命令捕获（或拦截）一个或多个信号，允许你引导脚本在接收到特定信号时采取的操作。

本文讨论了编写 shell 脚本时重要的六种信号。表 28-5 列出了这些信号、系统通常分配给信号数字以及产生每个信号的条件。执行命令 `kill l`、`trap l` 或 `man 7 signal` 可以获取信号名称列表。

### 表 28-5. 信号

| 类型 | 名称 | 编号 | 生成条件 |
| :--- | :--- | :--- | :--- |
| 非信号 | `EXIT` | 0 | 脚本结束 |
| 挂断 | `HUP` | 1 | 断开 |
| 终端中断 | `INT` | 2 | 按下中断键 |
| 退出 | `QUIT` | 3 | 按下退出键 |
| 杀死 | `KILL` | 9 | 强制杀死 |
| 软件终止 | `TERM` | 15 | 软件终止 |
| 停止 | `STOP` | 20 | 按下暂停键 |
| 调试 | `DEBUG` | | 断点 |
| 错误 | `ERR` | | 命令返回非零状态 |

`done`

当传入一个或多个文件名时，`addbanner` 会遍历这些文件并在每个文件的头部添加一个横幅（`banner`）。当你需要在文档顶部使用标准格式（例如备忘录布局），或想为 shell 脚本添加标准头部时，此脚本非常有用。头部存储在名为 `~/banner` 的文件中。由于 `addbanner` 使用了 `HOME` 变量（该变量包含用户目录的路径），该脚本可以在无需修改的情况下供多个用户使用。如果 Alfred 使用 `/home/alex` 代替 `$HOME` 并将脚本交给 Jenny，那么 Jenny 将必须进行更改，否则当 Jenny 运行它时，`addbanner` 将使用 Alex 的 `~/banner`（假设对该文件有读取权限）。

`addbanner` 中的第一个陷获（`trap`）会导致它在接收到挂断、中断（终端中断或退出）或信号终止时以状态 1 退出。该脚本在 `signal-number` 处捕获一个 0，这导致它在退出时（无论是因为附加命令还是到达末尾）执行命令参数。这些操作使得无论脚本是正常终止还是提前终止，都能删除临时文件。第二个陷获的标准错误被发送到 `/dev/null`，用于处理尝试删除不存在的文件的情况。在某些情况下，`rm` 会向标准错误发送错误消息，但由于标准错误被重定向，用户看不到此消息。

请见第 899 页查看使用 `trap` 的另一个示例。

## kill: 终止进程

`kill` 向进程或作业发送信号。`kill` 命令的语法如下：

```bash
kill [signal] PID
```

其中 `signal` 是信号名称或数字（例如 `INT` 或 2），`PID` 是要接收信号的进程标识符。你也可以使用作业号 `%n`（例如 19）代替 `PID`。如果省略 `signal`，`kill` 将发送 `TERM`（软件终止，数字 15）信号。有关信号名称和数字的更多信息，请参见第 933 页的表 28-5。

以下命令向作业号 1 发送 `TERM` 信号：

```bash
kill -TERM %1
```

由于 `TERM` 是 `kill` 的默认信号，你也可以执行命令 `kill %1`。执行命令 `kill -l`（小写 "l"）来显示信号名称列表。

被中断的程序通常会留下处于不可预测的状态：临时文件可能被留下（通常它们会被删除），并且权限可能会被更改。编写良好的应用程序会在退出前捕获、检测并清理。大多数仔细的应用程序会捕获 `INT`、`QUIT` 和 `TERM` 信号。

要终止程序，请按 `INT`（如果作业在前台，则按 `CTRL-C`）。由于程序可以被写为忽略信号，你可能需要使用 `KILL` 信号，它是无法被捕获或忽略的；这是一个“强制杀死”。有关更多信息，请参阅第 395 页的“kill: 向进程发送信号”。

## getopts: 解析选项

内置命令 `getopts` 解析命令行参数，使得编写遵循 Linux 参数惯例的程序变得更容易。`getopts` 的语法为：

```bash
# getopts optstring varname [arg ...]
```

其中 `optstring` 是有效选项列表，`varname` 是每次接收一个选项的变量，`arg` 是要处理的可选参数列表。如果 `arg` 不存在，`getopts` 会生成一个参数；如果 `optstring` 以冒号 (:) 开头，它将负责生成错误消息；`getopts` 会生成错误消息。

`getopts` 使用 `OPTIND`（选项索引）和 `OPTARG`（选项参数）来存储选项关系值。当 shell 脚本运行时，`OPTIND` 的值为 1。每当 `getopts` 定位一个参数时，它就会将 `OPTIND` 增加到下一个选项的索引。如果选项未被选取，则将参数的值分配给 `OPTARG`。

要表示某个选项允许参数，请在 `optstring` 中相应的字母后跟一个冒号 (:)。选项字符串 `dx:it:r` 表示 `getopts` 应该搜索 `d`、`x`、`i`、`t` 和 `r` 选项，其中 `d` 和 `t` 选项需要参数。

在 `while` 控制结构中作为测试命令使用，允许你逐个遍历选项。该 `getopts` 会检查列表中是否存在于 `optstring` 中的选项。循环每次循环都会将找到的选项存储在 `varname` 中。

假设你想写一个可以接受三个选项的程序：

- 1. `ab` 选项，程序应该忽略输入行开头的空格。
- 2. `at` 选项，后面跟着目录名称，程序应使用该目录存放临时文件。否则，应使用 `/tmp`。
- 3. `u` 选项，表示程序应将其所有输出转换为大写。

此外，程序应该忽略所有其他选项，并在遇到两个连字符 (`--`) 时结束处理。

问题在于编写确定用户提供了哪些选项的程序部分。以下解决方案没有使用 `getopts`：

```bash
SKIPOPTS===
TMPDIR=/tmp
CASE=lower
while [ "$1" = "-" ] && [ "$1" != "" ]; do
    case $1 in
        b) SKIPOPTS=TRUE; ;;
        f) if [ -d "$2" ]; then
            TMPDIR="$2"
            shift
        else
            echo "$0: takes a directory argument." >&2
            exit 1
        fi
        ;;
        u) CASE=$upper ;;
        --) break ;;
        *) echo "$0: Invalid option $1." >&2; exit 1 ;;
    esac
    shift
done
```

此程序片段使用循环在参数不为空时检查 `shift` 参数。（注：此处原文存在大量重复和错误，已根据逻辑进行整合）。

## 表 28-6. bash 内置命令

| 内置命令 | 功能 |
|--- |--- |
| `:` | 返回 0 或 true（空内置命令）；第 935 页 |
| `. (dot)` | 作为当前进程的一部分执行脚本（第 269 页） |
| `bg` | 将挂起的任务放入后台（第 281 页） |
| `break` | 退出循环控制结构（第 900 页） |
| `cd` | 切换另一个工作目录（第 174 页） |
| `continue` | 从循环控制结构的下次迭代开始（第 800 页） |
| `echo` | 显示其参数（第 137 页） |
| `eval` | 扫描并评估命令行（第 823 页） |
| `exec` | 在当前进程中执行脚本或程序（第 830 页） |
| `exit` | 从交互式 shell 退出（通常通过 CONTROL-D）；第 820 页 |
| `export` | 将值置调用环境中（变为全局变量）；第 816 页 |
| `fg` | 将任务从后台带回前景（第 280 页） |
| `getopts` | 解析给 shell 的参数（第 936 页） |
| `jobs` | 显示后台任务列表（第 280 页） |
| `kill` | 向进程或任务发送信号（第 395 页） |
| `pwd` | 显示工作目录的名称（第 170 页） |
| `read` | 从标准输入读取一行（第 827 页） |
| `readonly` | 声明变量为只读（第 289 页） |
| `set` | 设置标记或命令行变量；不带参数时，列出所有变量（第 825 和 924 页） |
| `shift` | 提升每个命令行参数（第 923 页） |
| `test` | 比较参数（第 879 页） |
| `times` | 显示当前 shell 及其子进程的总运行时间 |
| `trap` | 捕获信号（第 933 页） |
| `type` | 显示参数将如何解释为命令（第 927 页） |
| `umask` | 返回文件创建掩码的值（第 420 页） |
