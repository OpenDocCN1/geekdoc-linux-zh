

拖动文件时会创建链接而不是复制（或移动）文件。在 KDE 中，文件被放置时会出现一个小菜单，提供复制、移动或链接文件的选项。

## 总结

我们在这里涵盖了很多内容，完全消化需要一段时间。反复进行游乐场练习，直到它变得有意义。了解基本的文件操作命令和通配符非常重要。您可以自由地通过添加更多文件和目录来扩展游乐场练习，使用通配符为各种操作指定文件。链接的概念起初有点令人困惑，但花时间学习它们的工作原理。它们可以成为真正的救星。

## 进一步阅读

- 关于符号链接的讨论：http://en.wikipedia.org/wiki/Symbolic_link

## 5 – 使用命令

到目前为止，我们看到了一系列神秘的命令，每个命令都有其自己的神秘选项和参数。在本章中，我们将尝试消除其中一些神秘感，甚至创建一些自己的命令。本章介绍的命令有：

- type – 指示如何解释命令名称
- which – 显示将要执行的哪个可执行程序
- help – 获取 shell 内建的帮助
- man – 显示命令的手册页
- apropos – 显示适当的命令列表
- info – 显示命令的 info 条目
- whatis – 显示命令的非常简短的描述
- alias – 为命令创建别名

## 命令到底是什么？

命令可以是四种不同的东西之一：

1. 一个可执行程序，如我们在 /usr/bin 中看到的那些文件。在此类别中，程序可以是编译后的二进制文件，例如用 C 和 C++ 编写的程序，也可以是用脚本语言编写的程序，例如 shell、perl、python、ruby 等。
2. 内置于 shell 本身的命令。bash 支持一些称为 shell 内建的内部命令。例如，cd 命令就是一个 shell 内建。
3. 一个 shell 函数。这些是融入环境中的微型 shell 脚本。我们将在后面的章节中介绍配置环境和编写 shell 函数，但现在，只需知道它们存在即可。
4. 一个别名。我们可以自己定义的、由其他命令组成的命令。

## 识别命令

经常很有用的是知道正在使用的是四种命令中的哪一种，而 Linux 提供了几种方法来找出。

## type – 显示命令的类型

type 命令是 shell 内建，用于显示 shell 将执行给定命令名称的哪种类型的命令。它的用法如下：

```
type command
```

其中“command”是您想要检查的命令的名称。以下是一些示例：

```
[me@linuxbox ~]$ type type
type is a shell builtin
[me@linuxbox ~]$ type ls
ls is aliased to `ls --color=tty'
[me@linuxbox ~]$ type cp
cp is /bin/cp
```

这里我们看到了三个不同命令的结果。注意 ls 的结果（取自 Fedora 系统），ls 命令实际上是带有“--color=tty”选项的 ls 命令的别名。现在我们知道为什么 ls 的输出会显示颜色了！

## which – 显示可执行文件的[content]

拖动文件时会创建链接而不是复制（或移动）文件。在 KDE 中，文件被放置时会出现一个小菜单，提供复制、移动或链接文件的选项。

## 总结

我们在这里涵盖了很多内容，完全消化需要一段时间。反复进行游乐场练习，直到它变得有意义。了解基本的文件操作命令和通配符非常重要。您可以自由地通过添加更多文件和目录来扩展游乐场练习，使用通配符为各种操作指定文件。链接的概念起初有点令人困惑，但花时间学习它们的工作原理。它们可以成为真正的救星。

## 进一步阅读

- 关于符号链接的讨论：http://en.wikipedia.org/wiki/Symbolic_link

## 5 – 使用命令

到目前为止，我们看到了一系列神秘的命令，每个命令都有其自己的神秘选项和参数。在本章中，我们将尝试消除其中一些神秘感，甚至创建一些自己的命令。本章介绍的命令有：

- type – 指示如何解释命令名称
- which – 显示将要执行的哪个可执行程序
- help – 获取 shell 内建的帮助
- man – 显示命令的手册页
- apropos – 显示适当的命令列表
- info – 显示命令的 info 条目
- whatis – 显示命令的非常简短的描述
- alias – 为命令创建别名

## 命令到底是什么？

命令可以是四种不同的东西之一：

1. 一个可执行程序，如我们在 /usr/bin 中看到的那些文件。在此类别中，程序可以是编译后的二进制文件，例如用 C 和 C++ 编写的程序，也可以是用脚本语言编写的程序，例如 shell、perl、python、ruby 等。
2. 内置于 shell 本身的命令。bash 支持一些称为 shell 内建的内部命令。例如，cd 命令就是一个 shell 内建。
3. 一个 shell 函数。这些是融入环境中的微型 shell 脚本。我们将在后面的章节中介绍配置环境和编写 shell 函数，但现在，只需知道它们存在即可。
4. 一个别名。我们可以自己定义的、由其他命令组成的命令。

## 识别命令

经常很有用的是知道正在使用的是四种命令中的哪一种，而 Linux 提供了几种方法来找出。

## type – 显示命令的类型

type 命令是 shell 内建，用于显示 shell 将执行给定命令名称的哪种类型的命令。它的用法如下：

```
type command
```

其中“command”是您想要检查的命令的名称。以下是一些示例：

```
[me@linuxbox ~]$ type type
type is a shell builtin
[me@linuxbox ~]$ type ls
ls is aliased to `ls --color=tty'
[me@linuxbox ~]$ type cp
cp is /bin/cp
```

这里我们看到了三个不同命令的结果。注意 ls 的结果（取自 Fedora 系统），ls 命令实际上是带有“--color=tty”选项的 ls 命令的别名。现在我们知道为什么 ls 的输出会显示颜色了！

## which – 显示可执行文件的位置

有时系统上安装了不止一个版本的某个可执行程序。虽然在桌面系统上这种情况并不常见，但在大型服务器上并不罕见。要确定给定可执行程序的确切位置，使用 which 命令：

```
[me@linuxbox ~]$ which ls
/bin/ls
```

which 仅适用于可执行程序，不适用于内建命令或作为实际可执行程序替代的别名。当我们尝试对 shell 内建命令，例如 cd，使用 which 时，我们要么得不到响应，要么收到错误消息：

```
[me@linuxbox ~]$ which cd
/usr/bin/which: no cd in (/opt/jre1.6.0_03/bin:/usr/lib/qt-3.3/bin:/usr/kerberos/bin:/opt/jre1.6.0_03/bin:/usr/lib/ccache:/usr/local/bin:/usr/bin:/bin:/home/me/bin)
```

这是一种花哨的说法，意思是“命令未找到”。

## 获取命令的文档

有了这种关于命令是什么的知识，我们现在可以为每种类型的命令搜索可用的文档。

## help – 获取 shell 内建的帮助

bash 为每个 shell 内建提供了一个内置的帮助设施。要使用它，输入“help”后跟 shell 内建的名称。例如：

```
[me@linuxbox ~]$ help cd
cd: cd [-L|-P [-e]] [dir]
Change the shell working directory.

Change the current directory to DIR. The default DIR is the value of the HOME shell variable.

The variable CDPATH defines the search path for the directory containing DIR. Alternative directory names in CDPATH are separated by a colon (:). A null directory name is the same as the current directory. If DIR begins with a slash (/), then CDPATH is not used.

If the directory is not found, and the shell option `cdable_vars' is set, the word is assumed to be a variable name. If that variable has a value, its value is used for DIR.

Options:
-L  force symbolic links to be followed
-P  use the physical directory structure without following symbolic links
-e  if the -P option is supplied, and the current working directory cannot be determined successfully, exit with a non-zero status

The default is to follow symbolic links, as if `-L' were specified.

Exit Status:
Returns 0 if the directory is changed, and if $PWD is set successfully when -P is used; non-zero otherwise.
```
