

- **\*** — 匹配任意字符。例如，要查找当前目录下所有以 .txt 结尾的文件，可以使用：
  ```
  $ ls *.txt
  ```
- **?** — 匹配单个字符。例如，要查找当前目录下所有扩展名为 .dtc 的文件（其中 ? 可以是 0–9、a–z 或 A–Z）：
  ```
  $ ls *.dtc
  ```
- **[xX*] 或 [x-x]** — 匹配字符范围。例如，要列出目录中名称包含数字的所有文件：
  ```
  $ ls *[0-9]*
  ```
- **\x** — 匹配或转义字符，例如 ? 或制表符。例如，要创建一个名称中包含问号的文件：
  ```
  $ touch foo?\?
  ```

请注意，Shell 可能不会像 Linux 命令那样解释某些字符或正则表达式，除非小心谨慎，否则在 Shell 脚本中混用通配符和正则表达式可能会导致问题。例如，查找文本中的模式最好留给与 `grep` 等命令配合使用的正则表达式；简单的通配符应用于在命令行上过滤或匹配文件名。并且，尽管 Linux 命令表达式和 Shell 脚本都可以识别反斜杠作为模式中的转义字符，但美元符号 ($) 具有两种截然不同的含义（在表达式中用于单字符模式匹配，在脚本中用于变量赋值）。

> **注意**
> 使用通配符时，请务必仔细阅读您的命令；一个非常常见的错误是输入类似 `rm -rf *.txt` 的命令，但在 * 和 .txt 之间多输入了一个空格。当您发现命令运行时间过长并疑惑原因时，bash 可能已经删除了您的大部分文件。问题在于它将 * 和 .txt 视为两个独立的对象。* 匹配所有内容，因此 bash 会删除您的所有文件。

## 管道数据传输

许多 Linux 命令可以在单一的、相互连接的命令行中协同工作，将数据从一种形式转换为另一种形式。以这种方式串联 Linux 命令被称为使用或创建管道。管道通过竖线运算符（`|`）在命令行上创建。例如，可以使用管道通过单条命令行执行复杂任务，如下所示：

```
$ find /d2 -name '*.txt' -print | xargs cat | \
tr ' ' '\n' | sort | uniq > output.txt
```

这个示例获取 `find` 命令的输出，并通过 `xargs` 将 `/d2` 目录下所有文本文件的名称提供给 `cat` 命令。然后，所有匹配文件的内容通过 `tr` 命令处理，将数据流中的每个空格转换为回车。接着，单词流被排序，并使用 `uniq` 命令去除相邻的相同行。输出结果是一个原始单词列表，随后保存在名为 `output.txt` 的文件中。

## 后台处理

Shell 允许您启动一个命令，然后通过在命令行末尾使用 ampersand（`&`）将其作为进程放到后台运行。这种技术在 X 终端窗口中常用于启动客户端并返回命令行。例如，使用 `xterm` 客户端启动另一个终端窗口：

```
$ xterm &
[3] 1437
```

回显的数字显示了一个数字（本例中为 3），这是 *作业编号*，即 Shell 进程的引用编号，以及 *进程 ID* 编号，或 PID（本例中为 1437）。您可以使用 Shell 内置的 `kill` 命令配合作业编号来终止 `xterm` 窗口会话，如下所示：

```
$ kill %3
```

或者，可以使用 `kill` 命令配合 PID 来终止进程，如下所示：

```
$ kill 1437
```

后台处理可用于 Shell 脚本中启动耗时较长的命令，例如备份：

```
# tar -czf /backup/home.tgz /home &
```

## 相关的 Fedora 和 Linux 命令

在使用 Shell 或编写 Shell 脚本时，可以使用以下命令和工具：

- `csh` — 用于更改登录 Shell 的命令
- `kibitz` — 允许两人通过单个 Shell 进行交互
- `mc` — 名为 GNU Midnight Commander 的可视化 Shell
- `nano` — 控制台简易文本编辑器
- `system-config-users` — 用于更改一个或多个用户登录 Shell 的图形用户管理工具
- `shar` — 用于创建 Shell 归档的命令
- `vi` — `vi`（实际上是 `vim`）文本编辑器

## 参考

- [http://www.linuxgazette.com/issue70/ghosh.html](http://www.linuxgazette.com/issue70/ghosh.html) — 《Linux Gazette》上一篇关于“引导 Linux”的文章，其中详细介绍了引导过程中的 BIOS 和 MBR 方面。
- [http://www.lostcircuits.com/advice/bios2/l.shtml](http://www.lostcircuits.com/advice/bios2/l.shtml) — LostCircuits BIOS 指南；详细介绍了所有 BIOS 设置的含义。
- [http://www.rojakpot.com/default.aspx?location=1](http://www.rojakpot.com/default.aspx?location=1) — BIOS 优化指南；详细说明了如何尽情调整这些 BIOS 设置。
- [http://www-106.ibm.com/developerworks/linux/library/l-slack.html](http://www-106.ibm.com/developerworks/linux/library/l-slack.html) — 通过 IBM 网站链接到一篇关于启动 Slackware Linux 的文章，并附有关于 System V 与 BSD 初始化脚本历史的侧边栏。
- `/usr/src/linux/init/main.c` — Linux 源代码中的此文件是了解 Linux 如何启动的最佳场所。阅读起来非常引人入胜。从源代码获取它！
- [http://sunsite.dk/linux-newbie/](http://sunsite.dk/linux-newbie/) — Linux 新手管理员指南的主页——这是一篇关于 Linux 系统管理的温和介绍。
- [http://www.gnu.org/software/grub/manual/](http://www.gnu.org/software/grub/manual/) — 尚未完成的 GRUB 手册。在您的 Fedora 系统中，`info grub` 提供了大量信息，并且可以在 `/usr/doc/grub` 中找到一个示例 `grub.conf` 文件（`/boot/grub/menu.lst` 是 `/boot/grub/grub.conf` 的符号链接；可以使用任一名称）。
- Lilo 用户指南——Werner Almesberger 关于 Linux LILOoader（或 LILO）及其在基于 Intel 的 PC 上如何工作的权威技术巨著。在 `/usr/share/doc/lilo*/doc` 目录下查找文件 `User_Guide.ps`，该文件可以通过 `gv` 客户端查看。LILO 已从 Fedora 中移除；GRUB 现在是发行版支持的默认启动加载器。
- “Managing Liscritpts with Red Hat's chkconfig” — 作者 Jimmy Ball，《*Linux Journal*》，2001 年 4 月；第 128–132 页。
- “Grub, Glorious Grub” — 作者 Hoyt Duff，《*Linux Format*》，2001 年 8 月；第 58–61 页。关于 GRUB 启动加载器的教程。
- [http://www.redhat.com/docs/manuals/linux/RHL-9-Manual/custom-guide/s1-services-serviceconf.html](http://www.redhat.com/docs/manuals/linux/RHL-9-Manual/custom-guide/s1-services-serviceconf.html) — Red Hat 关于使用 `system-config-service` 客户端（当时称为 `redhat-config-services`）的指南。
- [http://www.linuxbase.org/spec/refspecs/LSB_1.0.0/LSB/lsb/init.html](http://www.linuxbase.org/spec/refspecs/LSB_1.0.0/LSB/lsb/init.html) — Linux 标准基关于系统初始化的描述；这是标准。

*此页故意留白*

# 第 12 章
## 系统监控工具

为了保持系统处于最佳状态，您需要密切关注它。在企事业单位环境中，这种监控至关重要，因为正常运行时间至关重要，任何系统故障都可能造成实际经济损失。无论是检查进程是否存在异常的守护程序，还是密切监视 CPU 和内存使用率，Fedora 都提供了丰富的实用程序，可以根据您的需求提供少量或大量的反馈。本章介绍了一些基本的监控工具，以及一些旨在让系统运行更长时间的技术。一些监控工具涵盖网络连接、内存和硬盘使用情况，但它们都应成为系统管理工具包中的一部分。最后，您将学习如何使用图形工具和命令行工具的组合来操作活跃的系统进程。

## 基于控制台的监控

熟悉 UNIX 系统管理的人员已经知道在大多数 UNIX 变体中常见的 `ps` 或进程显示命令。由于 Linux 与 UNIX 关系密切，它也从该命令中受益，允许您快速查看系统上当前运行的进程，以及谁拥有它们以及它们资源消耗如何。

虽然 Linux 内核具有自己独特的体系结构和内存管理，但它也从增强使用 `/proc` 文件系统中受益，这是在许多 UNIX 变体中找到的虚拟文件系统。通过 `/proc` 文件系统，您可以直接与内核通信，以深入了解当前正在发生的事情。开发人员倾向于使用 `/proc` 文件系统作为一种获取信息的方式

### 本章内容

- 基于控制台的监控
- 使用 `kill` 命令控制进程
- 使用优先级调度与控制
- 使用 `free` 显示空闲和已用内存
- 图形进程和系统管理工具
- KDE 进程和系统监控工具
- 参考

