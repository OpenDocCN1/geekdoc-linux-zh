
现在假设我们想要遍历 /usr/sbin 目录树中的所有文件，并找出设置了 setuid 位且由 root 拥有的文件。为此，我们使用 find 命令并指定 -user 和 -perm 测试。但与默认的 -print 操作不同，我们将指定 -ls 选项以获取类似 ls 的列表。

```
[tschenk@nomad /usr]$ find sbin -user root -perm -4000 -ls
143415  6 -rwsr-xr-x 1 root root 5736 Apr 19 14:39 sbin/usernetctl
143500 293 -rwsr-xr-x 1 root root 299364 Apr 19 15:38 sbin/sendmail
143537 17 -rwxr-xr-x 1 root bin 16488 Mar 22 14:53 sbin/traceroute
143541 11 -rwsr-xr-x 1 root root 10708 Apr 12 10:29 sbin/userhelper
143566 19 -rwsr-xr-x 1 root root 18576 Apr 1 06:52 sbin/fping
```

除了像 -print 和 -ls 这样的简单操作外，还有其他操作，其中最强大的就是 -exec 操作。通过此操作，你可以指定对找到的每个文件执行任意操作。稍加思考即可看出，这可以成为一个极其强大的工具。例如，假设你想要运行一个每日脚本，对系统上所有 setuid root 程序执行 md5sum，以便将其与前一天记录的内容进行比较以检测更改。这样的脚本可能如下所示：

```
#!/bin/sh

# Start by running the find command to locate the setuid programs and
# execute the md5sum program against them.

if [ -f /var/local/setuid.log ]; then
    FIRSTTIME=false
    mv /var/local/setuid.log /var/local/setuid.log.OLD
else
    FIRSTTIME=true
fi

find / -perm -4000 -exec md5sum {} \; > /var/local/setuid.log

if [ "$FIRSTTIME" = "false" ]; then
    cd /var/local
    diff -u setuid.log.OLD setuid.log | mail -s "Setuid Report" root
fi

exit 0
```

### 警告

这只是 find 可以做到的事情的一个示例，而随着这种能力的增强，也伴随着一些警告。首先，在按下回车键之前，务必反复检查你的语法。这在你使用 -exec 操作并执行破坏性操作，例如删除文件时尤其重要。其次，find 命令可能非常消耗资源，应谨慎使用。这有几个原因。首先，find 的本质是必须检查指定起始目录下的每个文件，并可选地对其执行某些测试。其次，使用 -exec 操作时，你可以指定对找到的任何文件运行任意命令或脚本。因此，你必须考虑正在运行的命令或脚本的资源使用情况。没有比格式错误的 find 命令配合资源占用型操作更危险的了。

## awk

另一个你作为高级用户会发现有用的命令是 awk 命令。该命令实际上是一种功能强大的脚本语言，其主要功能是生成报告。事实上，awk 的许多报告生成功能影响了 perl 中的类似功能。许多管理员发现 awk 在简单的单行命令或作为简单 shell 脚本的一部分时最有用。例如，以下命令行：

```
ps auxw | awk 'NR > 1 { print $1 }' | sort | uniq
```

此命令行执行以下操作：

- 取 ps 的输出
- 跳过第一行
- 截取用户名
- 对用户名进行排序
- 对排序后的列表运行 uniq

这将生成当前系统上正在运行进程的所有用户 ID 的列表。

这只是 awk 的一个非常简单的用法，但正如所说，awk 主要是一个文本处理和报告生成工具。以下命令序列演示了这种能力。此命令从 passwd 文件的第 5 个字段获取 GECOS 信息，并生成用户名、办公室号码和办公室电话的报告。

```
[tschenk@nomad redhat]$ awk -F ':' \
'BEGIN { printf "%-15s%-15s%-10s\n\n", "FULL NAME", "OFFICE NO.", "PHONE" }
{ split($5, f, ","); 
printf "%-15s%-15s%-10s\n", f[1], f[2], f[3] }' passwd
```

| 全名 | 办公室号码 | 电话 |
|---|---|---|
| Thomas Schenk | Rm 164 | 502-2603 |
| E.J. Schenk | Rm 503 | 503-1467 |
| Nick Schenk | Rm 503 | 503-1465 |
| Nia Schenk | Rm 104 | 502-6514 |
| Robert Smith | Rm 504 | 503-1465 |
| Bob Reed | Rm 504 | 503-1467 |
| Charles Brown | Rm 104 | 502-4158 |
| Chuck Jones | Rm 504 | 503-1465 |
| Diane Wilson | Rm 104 | 502-4156 |
| Dwight Wilson | Rm 504 | 503-1466 |
| Ashley Waters | Rm 504 | 503-1468 |
| Bill Ashton | Rm 100 | 502-6195 |

现在，你可能认为 perl 可以更轻松地完成此操作。但请考虑以下几点：在这种情况下，awk 有时是更好的选择，因为它是一个更轻量级的进程，没有 perl 的启动开销。这种开销差异是熟悉 awk 成为有用技能的原因之一。awk 脚本语言允许你生成报告、进行计算并执行其他任务，就像 perl 一样。另一方面，perl 是一种更通用的脚本语言。由于其对扩展模块的支持，perl 可用于构建超出 awk 能力范围的非常复杂的系统。然而，即使 perl 是一种功能更丰富的脚本语言，对于小型任务，awk 可能是更好的选择。如果你把 awk 和 perl 想象成锤子，awk 是木匠的钢丝钳锤，perl 是五磅重的铁锤；你使用哪一个取决于钉子的大小。

## sed

我们接下来要介绍的命令是流编辑器 sed。该命令主要用于快速的搜索和替换操作。通过为 sed 编写简单的脚本文件，你可以对文件执行多次更改。这种能力在脚本文件中非常有用。

这里有一个 sed 用得上的例子，可以节省与公司名称和标志更改相关的大量输入。此示例利用 sed 命令以及 find 命令的文件定位功能。将两者结合使用可以让你做两件事：

- 1. 替换旧的公司名称。
- 2. 将对旧标志文件名的引用替换为对新标志文件名的引用。

```
[root@nomad html]# cat /tmp/sedscript
s/Widget Makers/Widget.com/g
s/widgetlogo.gif/widgetlogo2.gif/g
[root@nomad html]# cat /tmp/rename.sh
#!/bin/bash

FNAME=$1

mv ${FNAME} ${FNAME}.OLD

sed -f /tmp/sedscript ${FNAME}.OLD > ${FNAME}
[root@nomad html]# find . -name "*.html" -exec /tmp/rename.sh {} ;
```

这只是 sed 的众多用途之一，但正如你所见，这个简单的脚本为某人节省了大量输入。无需使用编辑器访问公司网站上的每个 HTML 文件来更改公司名称和标志，脚本为我们完成了工作。这意味着可能需要花费数小时的人工任务可以更快地完成。有关 sed 命令可用选项的更详细描述，请参阅手册页。

我们刚刚介绍的几个命令并不是你在担任 Linux 系统管理员角色时唯一会发现有用的命令，但将这三个命令与你选择的 shell 的掌握相结合使用，你可以完成他人无法完成的任务。

## Linuxconf、Control-Panel 和配置实用程序

除了 find、awk 和 sed 等工具，你可以用它们构建其他工具来使系统管理更轻松外，Red Hat Linux 发行版还提供了一些工具来帮助你作为系统管理员。其中包括 Linuxconf、control_panel 程序以及用于配置诸如声音支持、网络等内容的多个配置实用程序。本节简要讨论这些工具中的每一个，并描述如何启动它们。它还讨论了一些功能，但不会深入其功能，因为这在本书的其他部分有介绍。

### Linuxconf 系统

Linuxconf 系统是一个功能强大的管理工具，可在文本和图形模式下使用。它可用于执行 Linux 系统上的许多配置任务。

- 网络配置
- 用户账户管理
- 文件系统管理
- 启动加载器管理

除了这些任务外，Linuxconf 还可用于归档配置信息，创建可在此后在它们之间切换的配置配置文件。例如，这些配置文件在笔记本系统上可能很有用，该系统必须能够在工作网络上工作，但你也希望它在家庭网络上工作。通过存储与每个网络交互所需的网络配置的配置文件，你可以通过更改配置文件轻松地从一个环境移动到另一个环境。它还可以管理文件系统的挂载和卸载，关闭 Linux 系统，并控制 PPP、SLIP 和 PLIP 链接。图 2.1 是 Linuxconf 图形版本的屏幕截图，显示了顶级菜单选项。

图 2.1
Linuxconf 图形模式。

![](img/4886c42c7629f445c7f7f3011ffbf3c3_65_0.png)
