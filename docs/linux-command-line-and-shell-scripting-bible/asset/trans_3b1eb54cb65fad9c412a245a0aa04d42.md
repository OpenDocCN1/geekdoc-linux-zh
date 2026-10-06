
正如你从输出所示，dash 版本的 `echo` 命令在不使用 `-e` 命令行参数的情况下也能正常识别行中的特殊字符，但对于包含 `-e` 命令行参数的行，它会产生混乱并将 `-e` 显示为普通文本。

命令行参数也是不可靠的。虽然 bash 支持使用 `-n` 来抑制行尾的换行符，但在所有的 ash shell 版本中都不支持它。dash shell 的 `echo` 语句支持 `-n` 参数，但并非所有的 ash shell 都支持它。

遗憾的是，这个问题没有简单的解决方案。如果你编写的既可以在 bash 可以在 dash ash 环境运行的脚本，最佳的解决方案是使用 `printf` 命令来显示文本。`ash` 命令在两个环境中的工作方式相同，并且可以正常显示特殊字符。

## function 命令

第 14 章展示了如何在 shell 脚本中定义自己的函数。bash shell 支持两种定义函数的方法。第一种方法是使用 `function` 语句：

```
function name {
  commands
}
```

`name` 属性定义了分配函数的唯一名称。你在脚本中定义的每个函数都必须分配一个唯一名称。

`commands` 是构成你函数的一个或多个 bash 命令。当你调用函数时，bash shell 会按照命令在函数中出现的顺序执行每条命令，就像执行普通脚本一样。

bash shell 脚本中定义函数的第二种格式更贴近其他编程语言中函数的定义方式：

```
name() {
  commands
}
```

函数名后的空括号表示你正在定义一个函数。这种格式下的命名规则与原始 shell 脚本函数格式相同。

ash 和 dash shell 不支持第一种定义方法（它们不支持 `function` 语句）。相反，在 ash 和 dash shell 中，你必须使用带括号的函数名来定义函数。如果你尝试在 ash 或 dash shell 中运行为 bash shell 设计的函数，将收到错误消息：

```
$ cat test9
#!/bin/bash
# testing functions

function func1() {
echo "This is an example of a function"
count=1
while [ $count -le 5 ]
do
  funccl
  count=$(( $ count + 1 ))
done
echo "This is the end of the loop"
funccl
echo "This is the end of the script"
$ ./test9
./.test9: 4: Syntax error: "( unexpected"
$
$
```

dash shell 并没有将代码分配给函数，而是执行了函数定义内部的代码，然后对 shell 脚本的格式表示抱怨。

如果你正在编写可能在 ash 或 dash 环境使用的脚本，请始终使用第二种定义函数的方法：

```
$ cat test10
#!/bin/dash
# testing functions

funccl() {
  echo "This is an example of a function"
  count=1
  while [ $count -le 5 ]
  do
    funccl
    count=$(( $ count + 1 ))
  done
echo "This is the end of the loop"
funccl
echo "This is the end of the script"
$ ./test10
This is an example of a function
This is an example of a function
This is an example of a function
This is an example of a function
This is an example of a function
This is the end of the loop
This is an example of a function
This is the end of the script
$
```

现在，dash shell 能够正常识别脚本中定义的函数，并在脚本内部使用它。

## 总结

本章讨论了在 ash shell 环境下的工作。ash shell 不是 Linux 发行版中常见的 shell，但它出现在 NetBSD 和 FreeBSD Unix 发行版中。ash shell 的衍生版本是 dash shell，它用于许多基于 Debian 的 Linux 发行版，尽管不是作为登录 shell。

ash 和 dash shell 是 Bourne shell 的简化版本，因此支持的功能没有 bash shell 那么多。如果你编写可能在 ash 或 dash shell 环境使用的 shell 脚本，需要考虑这一点。

下一章将讨论你可能会遇到的另一个 Linux shell 环境。C shell 是某些 Unix 环境中流行的 shell，并已以 `tcsh` shell 的形式进入了 Linux 世界。我们将查看 tcsh shell 与 bash shell 的区别，以及为了让脚本在 tcsh shell 环境中运行你需要了解的知识。

## 第 21 章

## tcsh Shell

Linux 世界中一种不太流行的替代性 shell 是 C shell。正如你可能猜的那样，C shell 在某种程度上尝试将 C 编程语言中的功能整合到 shell 脚本中。开源实现中最流行的 C shell 版本是 `tcsh` shell。本章将讨论 tcsh shell，描述如何为它编写 shell 脚本。

- 本章内容
- tcsh shell 的历史
- tcsh 的组成
- 使用 tcsh shell

## 什么是 tcsh shell？

C shell 是由 Bill Joy 在加州大学伯克利分校开发的，用于替代 AT&T 实验室创建的 Unix shell（Bourne shell 之前）。伯克利的开发人员当时拥有并构建了一个 Unix 系统来与 AT&T Unix 竞争，而 C shell 是他们的默认选择。20 世纪 70 年代后期，Ken Greer 创建了 C shell 的扩展，添加了 TENEX 操作系统中包含编辑功能。这就是 `tcsh` 名字的由来。tcsh shell 已经成为许多 Unix 系统的流行 shell（包括早期的 macOS）。

虽然 bash shell 已成为大多数 Linux 发行版的默认 shell，但 tcsh shell 是可选的，并且可以根据需要直接从源代码安装。如果你将 shell 脚本从 BSD 环境迁移到 Linux 环境，使用 tcsh shell 会非常有帮助。

由于 C shell 创建于 Bourne shell 之前，两者之间存在显著差异。由于 bash 基于 Bourne shell，tcsh 和 bash shell 之间也存在显著差异。对于所有非简单的应用程序，编写可以在两个环境中运行的脚本几乎是不可能的。

第四部分 替代性 Linux Shell

## tcsh Shell 组件

与 bash shell 一样，tcsh shell 使用命令行参数、默认文件、环境变量和内置命令来定义 shell 运行环境。本节将描述 tcsh shell 的这些特性。

## tcsh 命令行参数

tcsh shell 提供了若干命令行参数，允许你自定义 shell 的运行方式。这些命令行参数定义了哪些 shell 功能以及 shell 在交互环境中的行为。表 21-1 列出了 tcsh shell 可用的命令行参数。

tcsh shell 使用了一些与 bash 相同的命令行参数，但也有一些自己的。

`-v` 和 `-V` 参数在 tcsh shell 中进行故障排除时非常有用。它们会在 shell 执行命令时显示命令。

`-V` 参数从 shell 启动就开始显示命令，包括登录和启动 shell 文件（见“tcsh 文件”章节）。`-v` 参数在启动和登录完成后才开始显示命令。

这对于命令行没有用，但在处理 shell 脚本时非常酷：

```
$ cat test1
#!/bin/tcsh -v
# run a script
set testing=10
echo "This is a test"
echo "The value of testing is $testing"
./test1
```
