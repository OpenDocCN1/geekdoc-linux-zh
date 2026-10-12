
| 此函数 | 执行以下操作 |
|---|---|
| fc -s [pat=rep] [cmd] | 在将模式 pat 替换为 rep 后重新执行命令。 |
| fg [jobspec] | 将指定的作业置于前台。如果未指定作业，则将最近的作业置于前台。 |
| getopts optstring name [args] | 获取可选参数（在 shell 脚本中调用以从命令行提取参数）。 |
| hash [-r] [name] | 记住指定命令的完整路径名。 |
| help [cmd ...] | 显示指定内置命令的帮助信息。 |
| history [n] | 显示过去的命令，或如果指定数字 n，则显示过去的 n 条命令。 |
| jobs [-lnp] [ jobspec ... ] | 列出当前活动的作业。 |
| kill [-s sigspec \| -sigspec] [pid \| jobspec] ... | 评估每个参数，如果最后一个参数为 0 则返回 1。 |
| let arg [arg ...] | 创建具有指定名称和值的局部变量（用于 shell 函数）。 |
| local [name=value] ... | 退出登录 shell。 |
| logout | 从目录堆栈中删除条目。 |
| popd [+/-n] | 将指定目录添加到目录堆栈顶部。 |
| pushd [dir] | 打印当前工作目录的完整路径名。 |
| pwd | 从标准输入读取一行并解析它。 |
| read [-r] [name ...] | 将指定变量标记为只读，以便以后无法更改这些变量。 |
| readonly [-f] [name ...] | 使用返回值 n 退出 shell 函数。 |
| return [n] | 设置各种标志。 |
| set [-abefhkmnptuvx] [ -o option] [arg ...] | 使第 n+1 个参数成为 $1，第 n+2 个参数成为 $2，以此类推。 |
| shift [n] | 从文件读取并执行命令。 |
| source filename [arguments] | 直到收到 SIGCONT 信号为止停止执行。 |
| suspend [-f] | 评估表达式 expr，如果 expr 为真则返回零。 |
| test expr | 打印从 shell 运行的进程的累计用户时间和系统时间。 |
| times |  |

表 3-1（续）

| 此函数 | 执行以下操作 |
|---|---|
| `trap [-l] [cmd] [sigspec]` | 当收到信号 `sigspec` 时执行 `cmd`。 |
| `type [-all] [-type \| -path] name [name ...]` | 指示 shell 如何解释每个名称。 |
| `ulimit [-SHacdfmstpnuv] [limit]` | 控制 shell 可用的资源。 |
| `umask [-S] [mode]` | 设置文件创建掩码——文件的默认权限。 |
| `unalias [-a] [name ...]` | 取消定义指定的别名。 |
| `unset [-fv] [name ...]` | 删除指定变量的定义。 |
| `wait [n]` | 等待指定进程终止。 |

## 第 4 章：在 Perl 中编程

### 本章内容

- ✓ 编写你的第一个 Perl 程序
- ✓ 获取 Perl 的概览
- ✓ 理解 Perl 包和模块
- ✓ 在 Perl 中使用对象

在编写脚本方面，Perl 语言在系统管理员中非常流行，尤其是在 UNIX 和 Linux 系统上。系统管理员使用 Perl 来自动化例行系统管理任务，例如查找可以归档并删除以释放磁盘空间的旧文件。

Perl 是一种脚本语言，这意味着你不必编译和链接 Perl 脚本（包含 Perl 命令的文本文件）。相反，解释器执行 Perl 脚本。这使得编写和测试 Perl 脚本变得容易，因为你不必经历典型的编辑-编译-链接周期来编写 Perl 程序。

除了编程的简易性之外，Perl 流行的另一个原因是 Perl 可自由分发，并且可在各种计算机系统上使用，包括 Red Hat Linux 以及许多其他系统，如 UNIX、Windows 95/98/NT/2000/XP 和 Apple Macintosh。

在本章中，我向你介绍 Perl 脚本编程。

### 了解 Perl

正式来说，Perl 代表 Practical Extraction Report Language（实用提取报告语言），但 Perl 的创建者 Larry Wall 说人们经常将 Perl 称为 Pathologically Eclectic Rubbish Lister（病态折衷垃圾列表器）。从这些名称可以看出，Perl 最初是为从文本文件中提取信息并生成报告而设计的。

Perl 于 1986 年诞生，最初是由 Larry Wall 创建的系统管理工具。随着时间的推移，Perl 通过不断增加许多新特性和功能而发展。最新版本——Perl 5.8——支持面向对象编程，并允许任何人通过以指定格式添加新模块来扩展 Perl。

Perl 忠实于其作为系统管理工具的起源，多年来一直深受 UNIX 系统管理员的欢迎。最近，当万维网（或简称为 Web）变得流行并出现对通用网关接口（CGI）程序的需求时，Perl 成为那些已熟悉该语言的人的自然选择。Perl 人气最近的飙升主要归功于在 Web 上编写 CGI 程序中使用 Perl。当然，随着人们对 Perl 的关注度提高，他们发现 Perl 的用途远不止 CGI 编程。这反过来又使 Perl 在用户中变得更加流行。

Perl 可在各种计算机系统上使用，因为与 Linux 操作系统一样，Perl 可以自由分发。

如果你熟悉 shell 编程或 C 编程语言，你可以快速掌握 Perl。如果你从未编程过，熟练掌握 Perl 可能需要一段时间。我鼓励你从 Perl 的一小部分功能开始，并忽略你不立即理解的内容。然后，慢慢将 Perl 功能添加到你的技能库中。

### 确定是否已安装 Perl

在继续 Perl 教程之前，请检查你的 Red Hat Linux 系统上是否已安装 perl 程序。输入以下命令：

```
which perl
```

which 命令会告诉你它是否在 PATH 环境变量列出的目录中找到指定的程序。如果已安装 perl，你应该会看到以下输出：

```
/usr/bin/perl
```

如果 which 命令抱怨在当前 PATH 中不存在此类程序，这并不一定意味着你没有安装 perl；它可能只是意味着你没有在 PATH 中包含 /usr/bin 目录。确保 /usr/bin 在 PATH 中；通过输入以下命令进行检查：

```
echo $PATH
```

查看输出是否列出 /usr/bin 目录。如果 /usr/bin 不在 PATH 中，使用以下命令重新定义 PATH：

```
export PATH=$PATH:/usr/bin
```

现在，再次尝试 which perl 命令。如果仍然出现错误，你可能尚未安装 Perl。你可以从随附的 DVD 中安装 Perl，按以下步骤操作：

- 1. 以 **root** 身份登录。
- 2. 将随附的 DVD-ROM 插入 DVD-ROM 驱动器。如果你正在 GNOME 或 KDE 图形环境中工作，DVD-ROM 应该会自动挂载。否则，通过输入以下命令挂载 DVD-ROM：
```
mount /mnt/cdrom
```
- 3. 输入以下命令将目录更改为 Red Hat 软件包的位置：
```
cd /mnt/cdrom/RedHat/RPMS
```
- 4. 输入以下 **rpm**（Red Hat 软件包管理器）命令来安装 Perl：
```
rpm -ivh perl*
```

在系统上安装 Perl 后，输入以下命令查看其版本号：

```
perl -v
```

这是该命令的典型输出：

```
This is perl, v5.8.1 built for i386-linux-thread-multi
(with 1 registered patch, see perl -V for more detail)

Copyright 1987-2003, Larry Wall

Perl may be copied only under the terms of either the Artistic License or the
GNU General Public License, which may be found in the Perl 5 source kit.

Complete documentation for Perl, including FAQ lists, should be found on
this system using "man perl" or "perldoc perl". If you have access to the
Internet, point your browser at http://www.perl.com/, the Perl Home Page.
```

此输出告诉你你拥有 Perl 版本 5.8，补丁级别 1，并且 Perl 的创始人 Larry Wall 拥有版权。（不过请记住，Perl 是在 GNU 通用公共许可证下自由分发的。）

你可以通过将万维网浏览器指向 Comprehensive Perl Archive Network（CPAN）来获取最新版本的 Perl。以下地址会将你连接到离你最近的 CPAN 站点：
http://www.perl.com/CPAN/

![](img/a7eec43a54473e95dc5ea333fecf1bd7_810_0.png)
