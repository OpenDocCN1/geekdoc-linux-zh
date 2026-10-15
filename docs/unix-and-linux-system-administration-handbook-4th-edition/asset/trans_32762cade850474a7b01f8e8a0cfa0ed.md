

## 输入与输出

echo 命令很粗糙但简单易用。若想对输出有更多控制，可使用 **printf**。它稍显不便，因为你必须在想要换行处显式加上换行符（使用 “\n”），但它能让你在输出中使用制表符和增强的数字格式。比较下面两个命令的输出。

```sh
$ echo "\taa\tbb\tcc\n"
\taa\tbb\tcc\n
$ printf "aa\tbb\tcc\n"
    aa  bb  cc
```

某些系统在操作系统层面提供 **echo** 和 **printf** 命令，通常分别位于 **/bin** 和 **/usr/bin**。尽管命令和 shell 内置命令相似，但在细节上可能存在细微差异，尤其是在 **printf** 的情况下。最好遵循 **bash** 的语法，或使用完整路径调用外部 **printf**。

你可以使用 **read** 命令来提示输入。以下是一个示例：

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

**echo** 命令中的 **-n** 会抑制通常的换行，但你也可以在这里使用 **printf**。我们稍后会介绍 if 语句的语法，但其作用在这里应该很明显。if 语句中的 **-n** 在其字符串参数非空时求值为真。脚本运行时的样子如下：

```text
$ sh readexample
Enter your name: Ron
Hello Ron!
```

## 命令行参数和函数

传递给脚本的命令行参数会变成名称为数字的变量。$1 是第一个命令行参数，$2 是第二个，以此类推。$0 是脚本被调用时的名称。这可能是诸如 **../bin/example.sh** 之类的奇怪名称，因此它不是固定值。

变量 $# 包含提供的命令行参数数量，而变量 $* 则一次性包含所有参数。这两个变量都不包括或计数 $0。

如果你在没有参数或参数不适当的情况下调用脚本，脚本应打印简短的用法消息以提醒你如何使用它。下面示例脚本接受两个参数，验证这两个参数都是目录，并显示它们。如果参数无效，脚本会打印用法消息并以非零返回码退出。如果脚本的调用者检查返回码，它就会知道该脚本未能正确执行。

```bash
#!/bin/bash

function show_usage {
  echo "Usage: $0 source_dir dest_dir"
  exit 1
}

# Main program starts here
if [ $# -ne 2 ]; then
  show_usage
else # There are two arguments
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

printf "Source directory is ${source_dir}\n"
printf "Destination directory is ${dest_dir}\n"
```

我们创建了一个单独的 show_usage 函数来打印用法消息。如果脚本后来更新为接受额外参数，用法消息只需在一个地方更改即可。

```text
$ mkdir aaa bbb
$ sh showusage aaa bbb
Source directory is aaa
Destination directory is bbb
$ sh showusage foo bar
Invalid source directory
Usage: showusage source_dir dest_dir
```

5. 注意错误消息和用法消息都输出到标准输出。它们不应该输出到标准错误吗？事实上那样会更正确，但由于此脚本并非打算用作过滤器，这种区别就不那么重要了。

传递给 **bash functions** 的参数与命令行参数的处理方式非常相似。第一个参数变为 $1，以此类推。如上例所示，$0 仍然是脚本的名称。

为了使前面的示例更健壮，我们可以让 `show_usage` 例程接受一个错误代码作为参数。这样就可以为每种不同的失败类型返回更明确的代码。下面的代码片段展示了它可能的样子。

```bash
function show_usage {
    echo "Usage: $0 source_dir dest_dir"
    if [ $# -eq 0 ]; then
        exit 99 # Exit with arbitrary nonzero return code
    else
        exit $1
    fi
}
```

在这个版本的例程中，参数是可选的。在函数内部，$# 告诉你传入了多少个参数。如果没有提供更具体的代码，脚本将以 99 代码退出。但一个特定的值，例如

```text
show_usage 5
```

会使脚本在打印用法消息后以该代码退出。（shell 变量 $? 包含最后执行的命令的退出状态，无论是在脚本内部还是在命令行中使用。）

在 **bash** 中，函数与命令之间的类比很强。你可以在 `~/.bash_profile` 文件中定义有用的函数，然后像使用命令一样在命令行中使用它们。例如，如果你的站点已将网络端口 7988 标准化为 SSH 协议（一种“通过模糊实现安全”的形式），你可能会在 `~/.bash_profile` 中定义

```bash
function ssh {
    /usr/bin/ssh -p 7988 $*
}
```

以确保 ssh 总是以选项 **-p 7988** 运行。

像许多 shell 一样，bash 也有别名机制，可以更简洁地重现这个有限的示例，但函数更通用、更强大。放弃别名，使用函数。

## 变量作用域

变量在脚本内部是全局的，但函数可以通过 local 声明创建自己的局部变量。考虑以下代码。

