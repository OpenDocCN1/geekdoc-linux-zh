
或者

```zsh
zsh % ls ./
-
```

这些是约定而非硬性，许多工具并不遵循它们（例如 `find`）。遵循此类约定是一个好主意；它让用户更容易学习使用你的程序。当你编写需要选项的程序时，请遵循 GNU/Linux 约定。

# GNU --help 选项

大多数 GNU 工具遵循的约定是，当你带有 `--help` 参数调用它们时，会显示（有时是详细的）帮助信息：

```zsh
zsh % gzip --help

gzip 1.2.4 (18 Aug 93)

usage: gzip [-cdfhlnrttV19] [-S suffix] [file ...]

  -stdout write on standard output, keep original ...

  -d decompress decompress

  -f force overwrite of output file and ...

  -h help give this help

  -l list compressed file contents

  -L license display software license

......
```

# getopts: 解析选项

`getopts` 内置命令让你更容易编写遵循 UNIX/Linux（包括红帽）参数约定的程序。`getopts` 的语法为：

```
getopts optstring varname [arg ...]
```

`optstring` 是有效选项字母的列表。要指示某个选项需要参数，请在该字母后加上冒号 `(:)`。选项字符串

`getopts -t` 表示 `getopts` 应该查找 `-d`, `-x`, `-o`, `-l`, `-t` 和 `-r` 选项，并且 `-o` 和 `-t` 选项需要参数。

在控制结构中将 `getopts` 作为测试命令使用，可以让你一次循环处理一个选项。`getopts` 会检查选项列表，查找存在于 `optstring` 中的选项。在每次循环中，`getopts` 会将它找到的选项存储在 `varname` 中。默认情况下，`getopts` 使用命令行选项。如果你在 `varname` 之后提供了一个参数列表 `arg`，它将改用该列表。

`getopts` 内置命令使用 `OPTIND`（选项索引）和 `OPTARG`（选项参数）来存储选项相关的值。当 shell 脚本运行时，`OPTIND` 的值用于定位参数，它会将 `OPTIND` 增加到下一个要处理的选项索引。如果选项需要参数，zsh 会将参数的值赋给 `OPTARG`。

假设你编写了一个可以接受三个选项的程序。

1. `-b` 表示你的程序应该忽略输入行开头的空白字符。
2. `-u` 后跟目录名称表示你的程序应该使用该目录作为临时文件。否则，它应该使用 `/tmp`。
3. `-u` 选项表示你的程序应该将其所有输出转换为大写字母。

此外，程序应该忽略所有其他选项，并在遇到 `--` 时结束选项处理。

问题在于编写程序中确定用户提供了哪些选项的部分。以下解决方案没有使用 `getopts`：

```
SKIPBLANKS=

TMPDIR=/tmp

CASE=$1

while [[ "$1" = -* ]] # 记住，[[ = ]] 是模式匹配
do
  case $1 in
    -b)
      SKIPBLANKS=TRUE;
      if [ -d "$2" ]
        then
          TMPDIR=$2
          shift
        else
          print "$0: -t takes a directory argument." >&2
          exit 1
      fi;
    -u)
      CASE=upper;
      break ;; # 停止处理选项
    *)
      print "$0: Invalid option $1 ignored." >&2;
  esac
done
```

这个程序片段使用循环来检查并移动参数，只要参数不是两个双连字符 `--`。只要参数不是两个双连字符，程序就会继续通过 `case` 语句循环，检查所有可能的选项。`case` 标签跳出 `while` 循环。`*` `case` 标签识别任何选项；它作为最后一个 `case` 标签出现，以捕获任何未知选项，打印错误消息并允许处理继续。在循环的每次迭代中，程序都会执行一次 `shift` 来获取下一个参数。如果选项需要参数，程序会执行一次额外的 `shift` 来跳过该参数。

以下程序片段使用 `getopts` 处理相同的选项：

在代码的这个版本中，`while` 结构在每次回到循环顶部时都会评估 `getopts` 内置命令。`getopts` 内置命令使用 `OPTIND` 变量来跟踪它下一次调用时要处理的参数索引。第二个示例仅在结束时调用了一次 `shift`，而第一个示例使用 `shift` 来获取每个新参数。当 `getopts` 内置命令处理完所有参数时，它会返回非零（假）状态并将控制传递给 `done` 语句。

由于你告诉了 `getopts` 哪些选项是有效的以及哪些是参数，它可以检测命令行中的错误并以两种方式处理它们。此示例在 `optstring` 中使用前导冒号来指定你在代码中设置并处理错误；当 `getopts` 发现无效选项时，它会将 `varname` 设置为 `?` 并 `OPTARG` 设置为该选项字母。当它发现缺少参数的选项时，`getopts` 将 `varname` 设置为 `?` 并将 `OPTARG` 设置为缺少参数的选项。

`?` `case` 指定了当 `getopts` 检测到无效选项时要执行的操作。`:` 模式指定了当 `getopts` 检测到缺失选项参数时要的操作的操作。两种情况下，`getopts` 都不写入任何错误消息；它将该任务留给你。

如果你省略了 `optstring` 中的前导冒号，无效选项和缺失选项参数会导致 `varname` 被赋值字符串 `?`。`OPTARG` 不会被设置，且 `getopts` 会将其自己的诊断消息写入标准错误。通常这种方法不那么如人，因为当发生错误时，你对用户看到的内容控制较少。

使用 `getopts` 不一定会让你的程序变得更短。它的主要优势是提供了一个统一的编程接口，并强制执行标准的选项处理。

## 输入与输出

编程语言需要输入和输出命令。在 Z Shell 中，输入命令是 `read`，输出命令是 `print`。

### read: 接受用户输入

`read` 的语法与 Bourne Again Shell 的 `read`（第 573 页）类似，但 Z Shell 的 `read` 提供了额外功能：

```
read [-prs] [-un] [varname?prompt] [varname...]
```

变量名是可选的。以下命令是有效的，如下：

```zsh
zsh read
```

它从标准输入读取一整行输入到变量 `REPLY` 中。当你在命令行上提供参数时，`read` 假设它们是变量名并拆分输入行（使用 `IFS` 中的字符作为分隔符），将每个单词按顺序分配给 `varname` 参数。如果变量不足，最后一个变量将被赋值为等于输入行剩余部分的字符串。如果单词不足，剩余的变量将被设置为空（第 575 页）。

Z Shell 允许你通过使用 `varname?prompt` 语法为第一个输入名称指定输入提示。下面的示例显示了一个 `read` 命令及其生成的提示：

```sh
sh % read MON month, day and year separated by spaces: " DAY YEAR "

month, day and year separated by spaces:
```
