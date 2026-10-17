
# 第 7 章 脚本与 Shell

```sh
ssh() {
  /usr/bin/ssh -p 7988 $*
}
```

在你的 `~/.bash_profile` 中确保 `ssh` 始终使用 `-p 7988` 选项运行。

与许多 Shell 一样，`bash` 有一种别名机制可以更简洁地实现这个有限示例，但函数更通用、更强大。

## 控制流

在本章中已经看到了 `if-then` 和 `if-then-else` 形式；它们的作用正如你预期的那样。`if` 语句的终止符是 `fi`。要更改子句，你可以使用 `elif` 关键字表示“else if”。例如：

```sh
if [ $base -eq 1 ] && [ $dm -eq 1 ]; then
  installDMBase
elif [ $base -ne 1 ] && [ $dm -eq 1 ]; then
  installDMBase
elif [ $base -eq 1 ] && [ $dm -ne 1 ]; then
  installDM
else
  echo '=='
fi
```

用于比较的奇特 `[ ]` 语法和整数比较操作符的类命令行名称（例如 `-eq`）都继承自原始 `/bin/test` 的 Bourne Shell 实现。中括号实际上是调用 `test` 的简写，并不是运算符本身。表 7.3 显示了数字的比较运算符。

| 字符串 | 数值 | 为真条件 |
| --- | --- | --- |
| `x = y` | `-eq` | x 等于 y |
| `x != y` | `-ne` | x 不等于 y |
| `x < y` | `-lt` | x 小于 y |
| `x > y` | `-gt` | x 大于 y |
| `x <= y` | `-le` | x 小于等于 y |
| `x >= y` | `-ge` | x 大于等于 y |
| `-n x` |  | x 不为空 |
| `-z x` |  | x 为空 |

`sh` 在评估文件属性的选项方面非常出色（再次归益于 `/bin/test`）。表 7.4 显示了 `sh` 操作符。

| 运算符 | 为真条件 |
| --- | --- |
| `-d file` | 存在且是目录 |
| `-e file` | 存在 |
| `-f file` | 存在且是普通文件 |
| `-r file` | 有读取权限 |
| `-s file` | 存在且不为空 |
| `-w file` | 有写入权限 |
| `file1 -nt file2` | file1 新于 file2 |
| `file1 -ot file2` | file1 老于 file2 |

尽管 `elif` 形式很有用，但 `case` 选择通常是更好的选择。它的语法在下面一个集中处理日志的脚本例中显示。特别注意的是每个条件后的右括号，以及在满足条件时执行的语句后的分号。`case` 语句以 `esac` 结束。

```sh
# 日志级别设置在全局变量 LOG_LEVEL 中。脚本的代码在许多细节上生成消息，但只有通过全局阈值 LOG_LEVEL 的部分会被记录或处理。为了明确每个消息重要性，消息文本之前有一个指示其关联日志级别的标签。
Msg() {
  message_level=$1
  message_itself=$2
  if [ $message_level -le $LOG_LEVEL ]; then
    case $message_level in
      0) message_level_text="Error"; ;;
      1) message_level_text="Warning"; ;;
      2) message_level_text="Info"; ;;
      3) message_level_text="Debug"; ;;
      *) message_level_text="Other"
    esac
    echo "${message_level_text}: $message_itself"
  fi
}
```

例程说明了许多应用程序使用的“日志级别”范式。脚本的代码在许多细节上生成消息，但只有通过全局阈值 `LOG_LEVEL` 的部分会被记录或处理。为了明确每个消息重要性，消息文本之前有一个指示其关联日志级别的标签。

某些系统具有操作系统层级的 `printf` 和 `echo` 命令，分别位于 `/usr/bin` 和 `/bin`。尽管这些命令与 Shell 内置命令相似，但它们在细节上可能有所不同，特别是在 `printf` 的情况下。请遵循 `sh` 的语法，或者使用完整路径调用外部 `printf`。

你可以使用 `read` 命令来提示输入。这里是一个示例：

```sh
#!/bin/sh
echo -n "Enter your name:
read user_name
```

```sh
if [ -n "$user_name" ]; then
    echo "Hello $user_name!"
    exit 0
else
    echo "Greetings, nameless one!"
    exit 1
fi
```

`echo` 命令抑制了通常的换行，但你也可以在这里使用 `printf`。我们很快会介绍 `if` 语句的语法，但其效果应该是显而易见的。`if` 语句中的 `-n` 在字符串参数不为空时评估为真。以下是该脚本运行时的样子：

```
$ sh readexample
Enter your name: Ron
Hello Ron!
```

## 文件名中的空格

文件和目录的命名基本上是不限制的，但名称有长度限制，且不能包含斜杠字符或空字符。特别是，允许包含空格。遗憾的是，UNIX 有一个使用空白字符分隔命令行参数的长传统，因此当文件名中出现空格时，旧软件往往会崩溃。

文件名中的空格曾经主要出现在 Mac 和 PC 的文件系统中，但现在它们已经渗透到 UNIX 文化中，并出现在标准软件包中。这是不争：管理脚本必须准备好处理文件名中的空格（更不用说单引号、星号和其他威胁性的标点符号）。

在 Shell 和脚本中，带空格的文件名可以用引号括起来以保持其整体性。例如，命令

```
$ less "My spacey file"
```

将 `My spacey file` 作为一个单一参数传递给 `less`。你也可以用反斜杠转义单个空格：

```
$ less My\ spacey\ file
```

## `sh` 脚本

大多数 Shell 的文件名完成功能（通常绑定到 `<Tab>` 键）通常会自动为你添加反斜杠。

当你编写脚本时，一个需要知道的有用武器是 `find -print0 opt`。与 `xargs -0` 结合，该选项使得 `find/xargs` 组合无论文件名中包含什么空白字符都能正常工作。例如命令

```
$ /home -type f -size +1M -print0 | xargs -0 ls -1
```

列出 `/home` 下所有大于 1MB 的文件的详细列表。

## 命令行参数与函数

脚本的命令行参数变成数字变量。`$1` 是第一个命令行参数，`$2` 是第二个，依此类推。`$0` 是调用脚本时的名称。这可能是像 `../bin/example.sh` 这样奇怪构造，因此每次运行脚本时的值并不相同。

变量 `$$` 包含提供的命令行参数数量，而变量 `$*` 同时包含所有的 `$`。这两个变量都不包含或计算 `$0`。以下是使用参数的示例：

```sh
#!/bin/sh
show_usage() {
    echo "Usage: $0 source_dir dest_dir" >&2
    exit 1
}

# 主程序从这里开始
if [ $# -ne 2 ]; then
    show_usage
else # 有两个参数
    if [ -d $1 ]; then
        source_dir=$1
    else
        echo "Invalid source directory" >&2
        show_usage
    fi
if [ -d $2 ]; then
    dest_dir=$2
    else
        echo "Invalid destination directory" >&2
        show_usage
    fi
fi

printf "Source directory is ${source_dir}\n"
printf "Destination directory is ${dest_dir}\n"
```
