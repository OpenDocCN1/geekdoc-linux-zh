
# 实例演示

如果你必须处理数据文件中的数据值（例如统计销售额或计算保龄得分），那么高级 `gawk` 特性将非常有用。当你处理数据文件时，关键是将相关的数据记录分组，然后对相关数据执行任何所需的计算。

例如，让我们处理一个包含两支队伍比赛保龄得分的文件，每支队伍有两个球员：

```text
$ cat scores.txt
Rich Blum,team1,100,115,95
Barbara Blum, team1,110,100
Christine Bresnahan, team2,120,115,118
Tim Bresnahan, team2,125,112,116
$
```

每个球员在数据文件中都有三场独立比赛的得分，每个球员通过第二列中的团队名称来标识。以下是用于对每个团队排序并计算总和和平均值的 Shell 脚本：

```bash
$ cat bowling.sh
#!/bin/bash
for team in $(gawk -F, '{print $2}' scores.txt | uniq)
do
  gawk -v team=$team 'BEGIN{FS=","; total=0
  {
    if ($2==team)
    {
      total += $3 + $4 + $5;
    }
  }
  END {avg = total / 6; print "Total for", team, "is", total, "the average is", avg}
}' scores.txt
done
```

循环内部第一个 `gawk` 语句过滤数据文件中的团队名称，并使用 `uniq` 函数为每个不同的团队名称返回一个值。`for` 循环处理每个团队。

```bash
$ ./bowling.sh
Total for team1 is 420 the average is 70
Total for team2 is 751 the average is 125.16666666667
```

# 什么是 dash Shell？

Debian 的 `dash` shell 有着有趣的历史。它是 `ash` shell 的直接后代，而 `ash` 是 Unix 系统上原始 Bourne shell 的简单拷贝版本（见第 1 章）。Kenneth Almquist 为 Unix 系统创建了一个小规模的 Bourne shell 版本，并命名为 Almquist shell，后缩写为 `ash`。这个原始版本的 `ash` shell 极其精简且运行速度快，但缺少许多高级功能，例如命令行编辑或历史记录功能，这使得它很难作为交互式 shell 使用。

NetBSD Unix 操作系统采用了 `ash` shell，并且直到今天仍将其作为默认 shell。NetBSD 开发者通过添加若干个新功能对 `ash` shell 进行了定制，使其更接近 Bourne shell。这些新功能包括使用 emacs 和 vi 编辑器命令进行命令行编辑，以及一个用于召回之前输入过的命令的 `history` 命令。这个版本的 `ash` shell 也被 FreeBSD 操作系统用作默认登录 shell。

Debian Linux 发行版创建了它自己的 `ash` shell 版本（称为 Debian ash，或 `dash`），以将其包含在自己的 Linux 版本中。在大多数情况下，`dash` 复制了 NetBSD 版本 `ash` shell 的功能，提供了高级的命令行编辑能力。

然而，为了增加 shell 的混淆性，`dash` shell 实际上是 Linux 中的默认 shell，但大多数基于 Debian 的发行版使用 `bash` shell 作为普通登录 shell，而仅将 `dash` 作为安装脚本的快速启动 shell，用于安装发行版文件。

例外是流行的 Ubuntu 发行版。这让 shell 程序员感到困惑，并在 Linux 环境下运行脚本时引起大量问题。Ubuntu Linux 发行版使用 `bash` shell 作为默认交互式 shell，但将 `dash` 作为默认的 `/bin/bash` shell。这种“特性”真的困了 shell 程序员。

正如你在第 11 章看到的，每个脚本必须以一行声明脚本所使用的 shell 作为开头。在我们的 `bash` shell 脚本中，我们一直使用：

```
#!/bin/bash
```

这告诉 shell 使用位于 `/bin/bash` 的 shell 程序来执行脚本。在 Unix 世界中，默认 shell 始终是 `/bin/bash`。许多 shell 程序员会将此复制到他们的 Linux shell 脚本中：

```
#!/bin/sh
```

在大多数 Linux 发行版中，`/bin/sh` 文件是指向 `/bin/bash` 程序的符号链接（见第 3 章）。这允许你轻松地将为 Unix Bourne shell 设计的脚本移植到 Linux 环境，而无需进行修改。

遗憾的是，Ubuntu Linux 发行版将 `/bin/sh` 文件链接到 `/bin/dash` 程序。因为 `dash` shell 只包含了原始 Bourne shell 命令的子集，这可能会——而且通常会——导致某些脚本无法正常工作。

下一节将带你了解 `dash` shell 的基础及其与 `bash` shell 的区别。如果你编写可能需要在 Ubuntu 环境下运行的 `bash` shell 脚本，了解这一点尤为重要。

# dash Shell 特性

尽管 `bash` shell 和 `dash` shell 都模仿 Bourne shell 建模，但它们之间存在一些差异。本节将带你了解 Debian shell 中的功能，以便在我们深入研究 shell 脚本特性之前，熟悉 `dash` shell 的工作原理。

# dash 命令行参数

`dash` shell 使用命令行参数来控制其行为。表 23.1 列出了命令行参数并描述了每个参数的作用。

表 23.1 `dash` 命令行参数

| 参数 | 描述 |
| :--- | :--- |
| `-a` | 导出所有分配给 shell 的变量 |
| `-c` | 从指定的命令字符串读取命令 |
| `-e` | 如果不是交互式的，若任何未测试的命令失败则立即退出 |
| `-f` | 显示路径通配符字符 |
| `-n` | 如果不是交互式的，读取命令但不执行 |
| `-u` | 当尝试展开未设置的变量时，向 STDERR 写入错误消息 |
| `-v` | 在读取时将输入写入 STDERR |
| `-x` | 在执行每个命令时将该命令写入 STDERR |
| `-I` | 在交互模式下忽略输入中的 EOF 字符 |
| `-i` | 强制 shell 在交互模式下运行 |
| `-m` | 开启作业控制（在交互模式下默认启用） |
| `-s` | 从 STDIN 读取命令（在无命令行参数时的默认行为） |
| `-E` | 启用 emacs 命令行编辑器 |
| `-V` | 启用 vi 命令行编辑器 |

Debian 在原始 shell 命令命令行列表中添加了几个额外的命令行参数。`-E` 和 `-v` 命令行参数启用了 `dash` shell 的特殊命令行编辑功能。

`-E` 命令行参数允许你使用 `emacs` 编辑器编辑命令行文本（见第 10 章）。你可以使用 Ctrl 和 Meta 键组合使用所有的 `emacs` 命令来操作单行文本。

`-v` 命令行参数允许你使用 `vi` 编辑器编辑命令行文本（再次，见第 10 章）。此功能允许你使用 Esc 键在命令行的普通模式和 `vi` 编辑器模式之间切换。在 `vi` 模式下，你可以使用所有标准的 `vi` 命令（如用 `x` 删除字符，用 `i` 插入文本）。完成命令行编辑后，必须再次按下 Esc 键以退出 `vi` 编辑器模式。

# dash 环境变量

`dash` shell 使用了非常少的默认环境变量来跟踪信息，你也可以创建自己的环境变量。本节描述了这些环境变量以及 `dash` 如何处理它们。

## 默认环境变量

`dash` 环境变量与 `bash` 中使用的环境变量非常相似。`dash` shell 包含的变量远少于 `bash`。

`dash` shell 使用 `set` 命令显示环境变量：

```
$ set
COLOR=0
DESKTOP_SESSION=true
DISPLAY=0.0
HOME=/home/atest
IFS=
LANG=en_US
LANGUAGE=en_US
LC_ALL=en_US
NAME=atest
OPTIND=1
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/bin
PPID=5293
PS1=$
PS2=> 
PS4=+
PWD=/home/atest
SHELL=/bin/dash
TERM=xterm
USER=atest
XCURSOR_THEME=default
```

你的默认 `dash` shell 环境可能会不同，因为不同的 Linux 发行版在登录时会分配不同的环境变量。

## 位置参数

除了默认环境变量，`dash` 还为命令行中定义的任何参数分配特殊变量。以下是 `dash` shell 可用的位置参数：

- `$$` shell 的名称
- `$n`: 第 `n` 位置参数
