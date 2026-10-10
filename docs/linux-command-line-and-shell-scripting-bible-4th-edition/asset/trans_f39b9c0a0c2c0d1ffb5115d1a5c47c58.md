

Barbara Blum,team1,110,115,100
Christine Bresnahon,team2,120,115,118
Tim Bresnahon,team2,125,112,116

每个玩家在数据文件中都有来自三场独立比赛的分数，并且每个玩家通过第二列中的队名来标识。以下是用于整理每个团队的数据并计算总分和平均值的 shell 脚本：

```sh
#!/bin/sh

for team in $(gawk -F, '{print $2}' scores.txt | uniq)
do
gawk -v team=$team 'BEGIN{FS=","; total=0}
{
    if ($2==team)
    {
        total += $3 + $4 + $5;
    }
}
END {
    avg = total / 6;
    print "Total for", team, "is", total, ",the average is",avg
}' scores.txt
done
```

for 循环内部的第一个 gawk 语句从数据文件中过滤出队名，然后使用 uniq 函数为每个独立的队名返回一个值。随后，for 循环对每个独立的队名进行迭代。

for 循环内部的 gawk 语句负责执行计算。对于每条数据记录，它首先判断队名是否与当前循环迭代中的团队值匹配。这是通过使用 gawk 的 -v 选项来实现的，该选项允许我们将 shell 变量传递到 gawk 程序内部。如果队名匹配，代码会保持对数据记录中三个分数的累加总和，只要该数据记录与队名匹配，就添加每条数据记录的值。

在每次循环迭代结束时，gawk 代码会显示分数总和以及分数的平均值。输出结果应该如下所示：

```sh
$ ./bowling.sh
    Total for team1 is 635, the average is 105.833
    Total for team2 is 706, the average is 117.667
    $
```

现在你拥有了一个方便的 shell 脚本来计算所有保龄球锦标赛的结果；你只需将每位玩家的数据填入数据文本文件并运行该脚本即可！

## 摘要

本章带你了解了 *gawk* 编程语言更高级的功能。每种编程语言都需要使用变量，*gawk* 也不例外。*gawk* 编程语言包含一些内置变量，你可以使用它们来引用特定的数据字段值，并获取有关处理的数据字段和记录数的信息。你还可以创建自己的变量供脚本使用。

*gawk* 编程语言还提供了你从编程语言中期望的许多标准结构化命令。你可以轻松使用 *if*-then 逻辑、*while*、*do*-while 和 *for* 循环来创建复杂的程序。这些命令中的每一个都允许你更改 *gawk* 程序脚本的流程，以遍历数据字段值，从而创建详细的数据报告。

如果你需要自定义报告输出，*printf* 命令是一个非常强大的工具。它允许你指定显示 *gawk* 程序脚本中数据的精确格式。你可以轻松创建格式化报告，将数据元素放置在完全正确的位置。

最后，本章讨论了 *gawk* 编程语言中可用的许多内置函数，并展示了如何创建自己的函数。*gawk* 程序包含许多用于处理数学功能的有用函数，例如标准平方根和对数，以及三角函数。还有一些字符串相关函数，使从较大的字符串中提取子字符串变得轻而易举。

在 *gawk* 程序中，你并不局限于内置函数。如果你正在开发一个使用大量专用算法的应用程序，你可以创建自己的函数来处理这些算法，然后在自己的代码中使用这些函数。你还可以设置一个包含你在 *gawk* 程序中使用的所有函数的库文件，从而节省所有编码中的时间和精力。

下一章会稍微转换一下话题。它将考察你在 Linux shell 脚本开发中可能会遇到的其他几种 shell 环境。尽管 Bash shell 是 Linux 中最常用的 shell，但它并非唯一的 shell。了解一些其他可用 shell 及其与 Bash shell 的差异会有所帮助。

# 第 23 章
使用替代 Shell

## 本章内容

- 理解 Dash shell
- 在 Dash shell 中编程
- 介绍 zsh shell
- 为 zsh 编写脚本

尽管 Bash shell 是 Linux 发行版中使用最广泛的 shell，但它并不是唯一的。既然你已经了解了标准 Linux Bash shell 的方方面面以及你能用它做什么，现在是时候考察 Linux 世界中可用的其他几种 shell 了。本章描述了你在 Linux 之旅中可能遇到的另外两种流行 shell，并展示了它们与 Bash shell 的区别。

## 考虑 Dash Shell

Debian Linux 发行版，以及其许多衍生版本（如 Ubuntu），使用 Dash shell 作为标准 Linux Bash shell 的替代品。Dash shell 有一段有趣的过往。它是 ash shell 的直接后代，而 ash shell 是 Unix 系统上可用的 Bourne shell 的一个简单副本（参见 [第 1 章](chapter1)，“Linux Shell 入门”）。Kenneth Almquist 为 Unix 系统创建了一个小规模的 Bourne shell 版本，并将其命名为 Almquist shell，随后简称为 ash。这个原始的 ash shell 版本极其小巧且快速，但缺乏许多高级功能，如命令行编辑和历史记录功能，这使得它很难作为交互式 shell 使用。

NetBSD Unix 操作系统采用了 ash shell，直到今天仍将其用作默认 shell。NetBSD 开发者通过添加几个新功能来定制 ash shell，使其更接近 Bourne shell。这些新功能包括使用 Emacs 和 vi 编辑器命令进行命令行编辑，以及用于回忆之前输入命令的 history 命令。FreeBSD 操作系统也使用这个版本的 ash shell 作为默认的登录 shell。

Debian Linux 发行版创建了自己版本的 ash shell（称为 Debian ash，或 *Dash*）并将其包含在其 Linux 版本中。在大多数情况下，Dash 复制了 NetBSD 版本 ash shell 的功能，提供了高级的命令行编辑能力。然而，为了增加 shell 的混乱程度，Dash shell 在许多基于 Debian 的 Linux 发行版中实际上并不是默认的用户 shell。由于 Bash shell 在 Linux 中的流行程度，大多数基于 Debian 的 Linux 发行版使用 Bash shell 作为常规登录 shell，并且仅将 Dash shell 用作安装脚本的快速启动 shell 以安装发行版文件。

要在你的系统上检查这一点，只需查看你的用户账户在 `/etc/passwd` 文件中的条目；你可以看到分配给你的账户的默认交互式 shell。以下是一个示例：

```sh
$ cat /etc/passwd | grep rich
rich:x:1000:1000:Rich,,,:/home/rich:/bin/bash
$
```

这个 Ubuntu 系统使用 Bash shell 作为交互式用户 shell 的默认 shell。要检查默认系统 shell，请使用 `ls` 命令查看 `/bin` 目录中的 `sh` 文件：

```sh
$ ls -al /bin/sh
lrwxrwxrwx 1 root root 4 Jul 21 08:10 /bin/sh -> dash
$
```

果然，这个 Ubuntu 系统使用 Dash shell 作为默认系统 shell。问题可能就出在这里。

正如你在 [第 11 章] “基本脚本构建” 中所看到的，每个 shell 脚本必须以一行声明脚本所使用的 shell 开头。在我们的 Bash shell 脚本中，我们一直使用以下行：

```sh
#!/bin/bash
```

这告诉 shell 使用位于 `/bin/bash` 的 shell 程序来执行脚本。在 Unix 世界中，默认 shell 始终位于 `/bin/sh`。熟悉 Unix 环境的许多 shell 脚本程序员在 Linux shell 脚本中使用以下内容：

```sh
#!/bin/sh
```

在大多数 Linux 发行版中，`/bin/sh` 文件是一个符号链接（参见第 3 章，“基本 Bash Shell 命令”），指向 `/bin/bash` shell 程序。这使得你能够轻松地将为 Unix Bourne shell 设计的 shell 脚本移植到 Linux 环境，而无需修改它们。

但正如你在示例中所看到的，Ubuntu Linux 发行版将 `/bin/sh` 文件链接到 `/bin/dash` shell 程序。由于 Dash shell 仅包含原始 Bourne shell 中可用命令的一个子集，这（并且经常确实）会导致某些 shell 脚本无法正常工作。

下一节将带你了解 Dash shell 的基础知识以及它与 Bash shell 的区别。如果你编写了可能在 Ubuntu 环境中需要运行的 Bash shell 脚本，知道这一点尤为重要。

## 查看 Dash Shell 功能

尽管 Bash shell 和 Dash shell 都以 Bourne shell 为模型，但它们存在一些差异。本节将带你了解 Dash shell 中的功能，以便在我们深入 shell 脚本功能之前，熟悉其工作原理。

## Dash 命令行参数

Dash shell 使用命令行参数来控制其行为。表 23.1 列出了这些参数，并描述了每个参数的作用。

### 表 23.1 Dash 命令行参数

| 参数 | 描述 |
| :-------- | :---------- |
| -a | 导出分配给 shell 的所有变量。 |
| -c | 从指定的命令字符串中读取命令。 |

