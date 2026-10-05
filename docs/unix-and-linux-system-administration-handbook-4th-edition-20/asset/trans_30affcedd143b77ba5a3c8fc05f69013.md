

# 从命令到脚本

是的，这些就是我们要执行重命名操作的命令。但实际上该如何操作呢？我们可以调回命令并删掉 `echo`，这样 bash 就会执行 `mv` 命令而不仅仅是打印它们。然而，将命令管道到另一个 bash 实例更不容易出错，且对之前的命令修改也较少。

当我们输入 <Control-P> 时，发现 bash 贴心地地将我们的微脚本合并成了一行。在这个精简的命令行中，我们只需添加一个管道，将输出发送给 `bash -x`。

```
$ find -type f name '*.log' | grep -v .do-not-touch | while read fname; do
echo mv $fname ${fname%.log}/.LOG}; done | bash -x
+ mv foo.log foo.LOG
+ mv genius/genius.log genius.LOG
```

-x 选项会在执行前打印每条命令。

我们已经完成了实际的重命名，但仍然想保留这个脚本以便以后可以使用。bash 的内置命令 `fc` 允许不将上一个命令返回到命令行，而是将命令传输到一个可能的位置（可能是 `~bin` 或 `/usr/local/bin`），使文件变为可执行，这样你就了一个脚本。

总结这种方法：

- 以流水线的形式开发脚本（或脚本组件），一步一步进行，完全在命令行中完成。
- 将输出发送到标准输出并检查以确保看起来正确。
- 在每个阶段，使用 shell 的命令历史调回管道，并使用 shell 的编辑功能对其进行微调。
- 在输出看起来正确之前，你实际上什么都没做，因此如果命令错误，也没有需要撤销。
- 一旦输出正确，就执行实际命令并验证它们是否按预期工作。
- 使用 `fc` 捕获你的工作、清理并保存。

在上面的示例中，我们打印了命令行然后将它们管道到子壳执行。这种技术并非无处不在，但通常很有帮助。或者，你也可以通过输出重定向到文件来捕获。无论如何，在预览中看到正确的内容之前，不要进行任何破坏性的操作。

# 第 2 章脚本与 Shell

## 输入与输出

`echo` 命令非常简单。若要对输出进行更多控制：

```
$ echo "\taa\tbb\tcc\n"
\taa\tbb\tcc\n
$ printf "\taa\tbb\tcc\n"
  aa bb cc
```

某些系统具有操作系统层级的 `echo` 和 `printf` 命令，分别位于 `/bin` 和 `/usr/bin`。虽然这些命令与内置命令相似，但它们在细节上可能会略有不同，特别是 `printf`。要么坚持 bash 语法，要么使用完整路径名调用外部的 `printf`。

你可以使用 `read` 命令提示输入。这里有一个示例：

```bash
#!/bin/bash

echo -n "Enter your name: "
read user_name

if [ -n "$user_name" ]; then
  echo "Hello $user_name!"
  exit 0
else
  echo "You did not tell me your name!"
  exit 1
fi
```

`echo` 命令中的 `-n` 抑制了通常换行，但你可以使用 `printf`。我们很快会介绍 `if` 语句的语法，但在这里效果应该是显而易见的。在这里，`if` 语句中的 `-n` 如果字符串参数不为空则求值为真。以下是脚本运行时的样子：

```
$ readexample
Enter your name: Ron
Hello Ron!
```

## 命令行参数与函数

脚本的命令行参数变为名称为数字的变量。`$1` 是第一个参数，`$2` 是第二个，以此此类推。`$0` 是调用脚本时的名称。它可能是 `../bin/example.sh` 这样奇怪的名字，所以它不是固定的值。

变量 `$#` 统计提供的命令行参数数量，变量 `$@` 则包含所有参数。这两个变量都不包含 `$0`。

如果你不带参数或带错误的参数调用脚本，脚本应该打印用法信息来提醒如何使用。下面的示例接受两个参数，验证它们是否都是目录并显示它们。如果参数无效，脚本将打印消息并以非零返回码退出。如果脚本的调用者检查返回码，就会知道该脚本执行失败。

```bash
#!/bin/bash

function show_usage {
    echo 'Usage: $0 source_dir dest_dir'
    exit 1
}

# 主程序开始
if [ -ne 2 ]; then
    show_usage
else # 有两个参数
    if [ -d $1 ]; then
        source_dir=$1
    else
        echo 'Invalid source directory'
        show_usage
    fi
    if [ -d $2 ]; then
        dest_dir=$2
    else
        echo 'Invalid destination directory'
        show_usage
    fi
fi
```

我们创建了一个 `show_usage` 函数来打印用法信息。如果以后更新脚本接受更多参数，用法信息只需要更改一处。

```
$ mkdir aaa bbb
$ sh showusage aaa bbb
Source directory is aaa
Destination directory is bbb
$ sh showusage foo bar
Invalid source directory
Usage: showusage source_dir dest_dir
```

- 注意错误消息和用法信息输出到了标准输出。它们难道应该输出到错误流吗？那样实际上会更正确，但由于这个脚本并不是……

## 变量作用域

变量在脚本中是全局的，但函数可以创建自己的局部变量。考虑以下代码：

```bash
#!/bin/bash

function localizer {
    echo ==> In localizer, a starts as '$a'
    local a
    echo ==> After local declaration, a is '$a'
    a="localizer version"
    echo ==> Leaving localizer, a is '$a'
}
```

```
a="test"
echo ==> Before calling localizer, a is '$a'
localizer
echo ==> After calling localizer, a is '$a'
```

下面的日志（等等，是上面的示例输出）演示了局部函数内部的 `$a` 版本遮蔽了全局 `$a`。全局 `$a` 在遇到局部声明之前是可见的；`local` 是一个在执行时创建局部变量的命令。

## 控制流

在本章中我们已经见过几种 `if-then` 和 `if-then-else` 形式；它们完全如你预期的那样。`if` 语句的结束符是 `fi`。要连接你的子句，可以使用 `elif` 关键字表示“否则如果”。例如：

```bash
if [ $base -eq 1 ] && [ $dm -eq 1 ]; then
    installDMBase
elif [ $base -ne 1 ] && [ $dm -eq 1 ]; then
    installBase
elif [ $base -eq 1 ] && [ $dm -ne 1 ]; then
    installDM
else
    echo 'Installing nothing'
fi
```

