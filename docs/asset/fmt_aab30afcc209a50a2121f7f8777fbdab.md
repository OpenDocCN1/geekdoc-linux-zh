
某些系统具有操作系统级别的 `echo` 和 `printf` 命令，分别位于 `/bin` 和 `/usr/bin` 中。尽管这些命令与 shell 内置命令相似，但它们在细节上可能会有细微差别，特别是在 `printf` 的情况下。要么遵循 `bash` 的语法，要么使用完整路径调用外部的 `printf`。

你可以使用 `read` 命令来提示输入。这里有一个用例：

```bash
#!/bin/bash

echo -n "Enter your name: "

read user_name
```

```bash
if [ -n "$user_name" ]; then
    echo "Hello $user_name!"
    exit 0
else
    echo "You did not tell me your name!"
    exit 1
fi
```

`echo` 命令中的 `-n` 抑制了通常的换行，但你可以使用 `printf`。我们很快会介绍 `if` 语句的语法，但它的效果在这里应该是显而易见的。这里 `if` 语句中的 `-n` 如果其字符串参数不为空则评估为真。当如下所示时脚本如下：

```
$ read example
Enter your name: Ron
Hello Ron!
```

### 命令行参数与函数

脚本的命令行参数变成名称为数字的变量 `变量1` 是第一个命令行参数，`$2` 是第二个，以此此类推 `变量0` 是调用脚本时的名称。这可能是某些奇怪的东西，例如 `../bin/example.sh`，因此它不是固定值。

变量 `$#` 包含提供的命令行参数数量，变量 `$@` 包含所有参数。这两个变量都不包含或计算 `$0`。

### 命令行参数与函数

如果你不带参数或使用不参数调用脚本，脚本应该打印一条简短的用法信息来提醒如何使用。下面的示例脚本接受两个参数，验证这两个参数都是目录并显示它们。如果参数无效，脚本将打印用法信息并以非零返回码退出。如果脚本的调用者检查返回码，它将知道该脚本执行不正确。

```bash
#!/bin/bash

function show_usage {
    echo "Usage: $0 source_dir dest_dir"
    exit 1
}

#### 主程序从这里开始

if [ $# -ne 2 ]; then
    show_usage
else # 有两个参数
    if [ -d $1 ]; then
        source_dir=$1
    else
        echo "Invalid source directory"
        show_usage
    fi
    if [ -d $2 ]; then
        dest_dir=$2
    else
        echo "Invalid destination directory"
        show_usage
    fi
fi

printf "Source directory is ${source_dir}\n"
printf "Destination directory is ${dest_dir}\n"
```

我们创建了一个 `show_usage` 函数来打印用法信息。如果脚本以后更新为接受额外的参数，则只需要在一个地方更改用法信息即可。⁵

```
$ mkdir aaa bbb
$ show_usage aaa bbb
Source directory is aaa
Destination directory is bbb
$ show_usage foo bar
Invalid source directory
Usage: show_usage source_dir dest_dir
```

- 注意，错误信息和用法信息输出到标准输出。它们不应该输出到标准错误吗？那样更正确，但由于这个脚本并不是设计用作过滤器，这种区别没那么重要。

## 第 2 章 脚本与 Shell

`bash` 函数的参数处理方式非常类似于命令行参数。第一个参数变成 `$1`，以此此类推。正如示例所示，`$0` 仍然是脚本的名称。

为了让之前的示例更健壮一些，我们可以将 `show_usage` 程序作为错误码参数参数。这样就可以为每种类型返回更确定的代码。

```bash
function show_usage {
    echo "Usage: $0 source_dir dest_dir"
    exit 1
}
```

在上面的示例中，我们打印了命令行并将其管道到子壳中执行。这种技术并非无处适用，但它通常很有帮助。或者，你也可以通过将输出重定向到文件来捕获输出。无论如何，在执行任何破坏性操作之前看到正确的内容。

### 变量作用域

变量在脚本范围内是全局的，但函数可以使用 `local` 声明创建自己的局部变量。考虑以下代码：

```bash
#!/bin/bash

function localizer {
  echo "In localizer, a starts as '$a'"
  local a
  echo "After local declaration, a is '$a'"
  a="localizer"
  echo "Leaving localizer, a is '$a'"
}
```

```bash
a="test"
echo "Before calling localizer, a is '$a'"
localizer
echo "After calling localizer, a is '$a'"
```

下面的日志显示了 `localizer` 内部的 `$a` 版本覆盖了全局变量 `$a`。全局 `$a` 在遇到 `local` 声明之前可见的；`local` 是一个在执行时创建局部变量的命令。

```
$ scopotest.sh
Before calling localizer, a is 'test'
In localizer, a starts as 'test'
After local declaration, a is ''
Leaving localizer, a is 'localizer'
After calling localizer, a is 'test'
```

### 控制流

我们在本章中已经见过几种 `if-then` 和 `if-then-else` 形式；它们的运作正如你预期的那样。语句的结束符是 `fi`。要连接你的子句，可以使用 `elif` 关键字表示“else if”。例如

```bash
if [ $base -eq 1 ] && [ $dm -eq 1 ]; then
  installDMBase
elif [ $base -ne 1 ] && [ $dm -eq 1 ]; then
  installBase
elif [ $base -eq 1 ] && [ $dm -ne 1 ]; then
  installDM
else
  echo 'Installing not'
fi
```
