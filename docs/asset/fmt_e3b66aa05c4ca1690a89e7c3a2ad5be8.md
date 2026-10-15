
```bash
$ find . -name "*.log"
```

哦，你发现需要包含点在模式中，并排除目录。通过以下方式找回命令并然后修改它：

```bash
$ find . -name "*.log"
```

OK，这看起来好多了。但 `do-not-touch` 目录看起来很危险；你可能应该在那里捣乱：

```bash
$ find . -name "*.log" | grep -v "do-not-touch"
```

好了，这就是需要重命名的文件列表。尝试生成新名称：

```bash
$ find . -name "*.log" | grep -v "do-not-touch" | while read fname;
do
  echo mv $fname '$(fname | sed '.log$/LOG)'
done
```

是的，这些是执行重命名的命令。那么如何真正执行它？你可以回溯命令并删掉 `echo`，这将让 `sh` 执行命令而不只是打印它们。然而，将命令管道到独立的 `sh` 实例更不容易出错，且不需要编辑之前的命令。当你这样做时，你会发现 `bash` 将你的微脚本压缩成了单行。对于这行压缩的命令行，只需添加一个将输出发送到 `sh -x` 的管道即可：

```bash
$ find . -name "*.log" | grep -v "do-not-touch" | while read fname; do mv $fname $(fname | sed '.log$/LOG'); done | sh -x
```

`sh` 的 `-x` 选项在执行每个命令之前打印它。这完成了实际的重命名，但保存脚本以供以后使用。`bash` 的内置命令 `fc` 就像那样，但它不是将最后的命令返回到命令行，而是将其传输到你选择的编辑器。添加 `shebang` 行和用法注释，将文件写入合理的位置（可能是 `~/bin` 或 `/usr/local/bin`），使文件可执行，你就有一个脚本。

## 输入与输出

`echo` 命令粗糙但简单。为了对输出有更多控制，请使用 `printf`。它稍微不方便，因为你必须在需要换行的地方显式放入 `"\n"`，但它提供了使用制表符和增强数字格式化输出的选项。比较以下两个命令的输出：

```bash
$ echo "\t\tbb\tcc\n"
\t\tbb\tcc\n
$ printf "\t\tbb\tcc\n\n"
  aa bb cc
```

# 第 7 章 脚本与 Shell

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

# 文件名中的空格

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

# sh 脚本

大多数 Shell 的文件名完成功能（通常绑定到 `<Tab>` 键）通常会自动为你添加反斜杠。

当你编写脚本时，一个需要知道的有用武器是 `find -print0 opt`。与 `xargs -0` 结合，该选项使得 `find/xargs` 组合无论文件名中包含什么空白字符都能正常工作。例如命令

```
$ /home -type f -size +1M -print0 | xargs -0 ls -1
```

列出 `/home` 下所有大于 1MB 的文件的详细列表。

# 命令行参数与函数

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

# 第 7 章 脚本与 Shell

如果你调用脚本时不带参数或提供的参数不当，脚本应该打印简短的用法消息提醒你如何使用它。上面的示例脚本接受两个参数，验证这两个参数都是目录，并打印它们的名称。如果参数无效，脚本将打印用法消息并以非零返回码退出。如果脚本的调用者检查返回码，它将知道该脚本执行不正确。

我们创建了一个独立的用法函数来打印用法消息。如果以后更新脚本以接受更多参数，则只需要在一个地方更改用法消息。打印错误信息的行的 `1>&2` 符号将输出重定向到 STDERR。

```
$ mkdir aaa bbb
$ sh showusage aaa bbb
Source directory is aaa
Destination directory is bbb
$ sh showusage foo bar
Invalid source directory
Usage: showusage source_dir dest_dir
```

`sh` 函数的参数处理方式类似于命令行参数。第一个参数变成 `$1`，依此类推。如你所见，`$0` 保持为脚本名称。

为了使示例更健壮，我们可以让 `show_usage` 例程接受一个错误码作为参数。这将允许为每种失败返回更确定的代码。下一个代码片段显示了如何实现：

```sh
show_usage() {
  echo "$0 source_dir dest_dir" 1>&2
  if [ $# -ne 0 ]; then
    exit 99 # 以任意非零返回码退出
  else
    exit 1
  fi
}
```

在这个版本的例中，参数是可选的。在函数内部，`$#` 告诉传递了多少参数。如果没有指定特定代码，脚本以代码 99 退出。但特定值，例如，

`show_usage 5`

会让脚本在打印用法消息后以该代码退出。（Shell 变量 `$?` 包含最后执行命令的退出状态，无论是在脚本内部还是命令行。）

函数与命令之间的类比在 `sh` 中是非常强烈的。你可以在你的 `~/.bash_profile` 文件中（原生 `sh` 使用 `~/.profile`）中定义完整的函数，然后在命令行中使用，像使用命令一样使用它们。例如，如果你的站点通过网络端口 7988 对 SSH 协议进行了标准化（一种“通过隐性实现安全”的形式），你可以定义

# sh 脚本
