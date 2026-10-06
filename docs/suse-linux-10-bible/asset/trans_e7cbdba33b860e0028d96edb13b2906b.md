

```bash
#!/bin/bash
case $1 in
happy)
echo "What a nice day it is today"
;;
sad)
echo "What a gloomy day it is today"
;;
esac
```

该脚本根据变量的值（在本例中为给定的参数）决定其输出内容。这种条件分支是任何编程语言的核心特征。

```bash
$ ./case.sh happy
What a nice day it is today

$ ./case.sh sad
What a gloomy day it is today

$ ./case.sh mad
```

注意，备选项测试后面跟着一个换行符，整个条件块以分号结束。整组条件集由 `esac` 关闭。

## 从脚本中发送邮件

你可能希望获知进度或成功信息。实现这一点的方法之一是使用 `mail` 命令。它看起来如下：

```bash
echo "many returns" | mail -s "Happy Birthday" user@domain.net
```

这会向该地址发送封主题为“Happy Birthday”的邮件。邮件正文可以从系统上的某个文件中获取。当然，发送的消息类型可能是“complete”（已完成）之类的，但几乎肯定有系统管理员使用 cron 任务来避免忘记生日！

在脚本中使用块的一种更高级的方法是所谓的“在此文档”（here-document）。在脚本中，符号 `<<` 配合 `EOF` 定义了用于重定向到命令的块的结束标记。`EOF` 通常如下所示使用：

## 在 Linux 中使用命令行

例如：

```bash
#!/bin/bash
cat <<EOF
many returns
EOF
```

如果你运行此代码，你将看到以下内容：

```bash
many returns
EOF
```

要发送问候邮件，请执行以下操作：

```bash
#!/bin/bash
mail -s "Greetings" user@domain.net <<EOF
many returns
EOF
```

## Shell 脚本的局限性

系统的大部分基础设施都基于 shell 脚本。特别是整个初始化和运行级别（runlevel）系统依赖于许多相互依赖的 shell 脚本。这些脚本从 `/etc/sysconfig/` 等其他地方读取。它们可能大量使用 `awk`、`sed` 和 `grep` 等基本命令，因为这些命令运行非常高效。

然而，作为用户或系统管理员，你不一定认为 shell 脚本是执行某些逻辑任务最简单或最优雅的方法。通常，shell 脚本最适合它们通常执行的工作：在低层运行的较小脚本。对于更复杂的任务，人们通常会转向专门的脚本语言。在实践中，这意味着使用 Perl 或 Python（或 Ruby）。如果你对创建动态网页内容感兴趣，请也查看 PHP 脚本以及用 Perl 或 Python 编写的 CGI 脚本，并根据你的需求选择。

## Shell 资源

你可以找到许多关于 shell 脚本的好书，包括：

- Mastering UNIX Shell Scripting by Randal K. Michael (Wiley, 2023)
- Linux Shell Scripting with Bash by Ken Bertuch (Sams, 2004)
- Learning the Bash by Cameron Newham and Bill Rosenblatt (O'Reilly, 1998)
- Wicked Cool Shell Scripts by Dave Taylor (No Starch Press, 2004)

## 与系统交互

网络上可用的资源包括：

- Advanced Bash Scripting Guide (www.tld.org/LDP/abs/html/)
- Bash Guide for Beginners (http://linux.org/training/bash/)
- Henri's Shell Dojo (www.shelldojo.com/)

## 脚本语言

正如 vi 的追随者与 emacs 的信徒之间（正如我们在第 11 章中讨论过的）或 KDE 爱好者与真正的 GNOME 信徒之间存在“宗教战争”一样，在脚本语言领域，Perl 和 Python 用户之间也存在某种分歧。

- Perl 非常常见，并且可以说更通用，仅仅是因为为它编写了大量的模块。在 Perl 中可以编写更多的代码，它充满了缩写和特殊符号。
- Python 更新、更简洁，并且可以说更优雅。它无疑是最容易学习的语言，而且阅读他人的 Python 代码比阅读他人的 Perl 代码容易得多。

它们之间的区别或许用 Perl 的口号“不止一种实现方法”（There is more than one way to do it）以及 Python 对此的回应“应该只有一种——最好只有一种——明显的实现方法”（There should be one—and preferably only one—obvious way to do it）来总结最好。

这里不是简单介绍这些语言；两者都有许多资源（参见该章节的“注释与资源”部分获取某些资源选项）。

如果你了解它们并想快速完成实用的脚本，我们建议你学习 Python。然而，如果你可能在一个需要维护他人编写的脚本环境中工作，那么 Perl 可能是正确的首选。

这里我们提供用两种语言完成非常简单任务的微示例，以及一些进一步信息的提示。

## Squid 日志读取脚本示例

Squid Web 会产生一个不可读的日志文件。有很多工具可以将 Squid 日志输出转换为其他格式，包括良好的格式。

