
在获取所需的命令后，你可以简单地在不带 `-k` 选项的情况下运行 `man` 命令来查找该命令的详细信息。

> 你也可以使用 `apropos usb` 命令来执行与 `-k usb` 命令相同的功能。这两个命令在终端屏幕上产生完全相同的输出。

> 如果在安装 Linux 后没有看到 `-k` 或 `apropos` 命令的任何输出，你可能需要运行 `makewais-command` 命令来对手册页数据库建立索引。

另一种原本旨在替换 Linux 中 `man` 命令的工具是 GNU info 页面。你可以通过输入相关命令名称后跟 `info` 命令来访问此工具。`info` 命令返回每个命令的易于读的描述，并包含指向其他信息页的链接（称为超链接）。今天，info 页面和手册页都被用于查找文档，因为手册页自 Linux 诞生以来就一直在使用，在过去的二十多年 UNIX 系统中也是如此。以下是使用 `info` 工具查找关于 `whoami` 信息的示例：

```
[root@server1]# info whoami
```

info 页面以交互方式显示：

```
File: coreutils.info, Node: whoami invocation, Next:
groups invocation, Prev: logname invocation, Up:
User information
'whoami': Print effective user id
==================
```

## Linux 基础用法

'whoami' 打印与有效用户 ID 关联的。它等同于命令 'id -un'。

唯一的选项是 '--help' 和 '--version'。

注意选项：

退出状态为零表示成功，非零值表示失败。

欢迎使用 info 版本 4.6。输入 `?` 获取帮助，输入 `m` 访问菜单项。

root@server1 root]#

在 info 工具中时，按下 `?` 或 `Ctrl+h` 组合键可以显示描述 info 用法的帮助屏幕。与 `man` 命令一样，你可以使用 `q` 退出。

![](img/8fe037bf1ed016dccb79dbd1a27184f2_126_0.png)

某些命令没有手册页或 info 页面。这些命令通常是内置于 BASH shell 的函数。要查找这些命令的帮助，你必须按照如下方式使用命令：

```
[root@server1]# help echo
echo: echo [-ne] [arg ...]
输出 ARGs。如果指定了 n，则抑制末尾的换行符。如果给了 -e 选项，则开启对后续反斜杠转义字符的解释：
\a (铃声)
\b退格
\c抑制末尾换行符
\e转义字符
\ff页符
\n换行
\rc返回
\t水平制表符
\v垂直制表符
\\\反斜杠
\num ASCII 码为 NUM（八进制）的字符。
```

你可以通过 `[root@server1 root]#` 显式关闭对 -E 字符的解释

## 关闭 Linux 系统

操作系统处理从计算机内存写入磁盘驱动器的数据，简单地关闭计算机电源可能会导致用户和系统文件损坏。因此，在关闭计算机硬件组件电源之前为操作系统做好关机准备是重要的。为了做到这一点，你可以发出 `shutdown` 命令，它可以在一段时间后停止或重启（重新启动）你的计算机。例如，要在 15 分钟后停止系统，你可以输入：

```
[root@server1 root] # shutdown -h +15
```

这将产生类似于下面的输出：

来自 root (tty2) 的广播消息 (2005年3月29日周二 04:08:18): 系统将在 15 分钟后准备关机！

注意前面的输出，在 `shutdown` 命令启动后，你不会再次收到命令提示符。因此，要停止关机，只需组合按下 `Ctrl` 和 `c` 键来取消命令。或者，你可以登录另一个终端并发出 `shutdown -c` 命令来取消关机。

要立即停止系统，你可以输入：

```
[root@server1 root] # shutdown -h now
```

此命令将产生类似于下面的输出：

来自 root (tty2) 的广播消息 (2005年3月29日周二 04:08:18): 系统将现在立即关机！

`shutdown` 命令的其他示例及其描述如表 3-6 所示。

| 表 3-6 停止和重启 Linux 操作系统的命令 |
| --- | --- |
| 命令 |  |
| shutdown -h +4 | 在四分钟后停止系统 |
| shutdown -r +4 | 在四分钟后重启系统 |
| shutdown -h now | 立即停止系统 |
| shutdown -r now | 立即重启系统 |
| shutdown -c | 取消计划的关机 |
| halt | 立即停止系统 |
| reboot | 立即重启系统 |

## 章节总结

- 大多数软件可以在安装时指定；然而，网络配置和软件包选择需要仔细规划。
- 虽然有许多安装方法，基于 CD-ROM 安装是最简单的。
- 典型的安装会提示用户选择语言、引导加载程序、硬盘分区、网络配置、防火墙配置、时区、用户账户、软件包选择并登录终端。

# 术语

无论你使用哪种终端（图形或命令行），你都可以输入命令、选项或关闭 Linux 系统。

## 术语表

`arguments` —— 命令名称后的文本，不以 "-"开头，指定命令所需的信息。

`authentication` —— 用户必须使用有效的用户名和密码才能访问系统的过程。

`BASH shell` —— Bourne Again Shell；它是 Linux 的默认命令行界面。

`boot loader` —— 由 ROM 启动的小型程序，用于执行 Linux 内核。

`command` —— 存在于硬盘并在命令行输入执行的程序。

`Disk Druid` —— 一种易于使用的图形程序，用于分区或修改硬盘上的分区。

`dual booting` —— 在计算机上安装多个操作系统的过程。用户随后可以在系统启动时选择加载哪个操作系统。

`ext2` —— 非日志 Linux 文件系统。

`ext3` —— 一种日志 Linux 文件系统。

`first wizard` —— 在 Red Fedora 安装后立即运行的配置工具。

`framebuffer` —— 视频硬件的抽象表示，程序无需直接与视频硬件通信。

`GRand Bootloader (GRUB)` —— Linux 中常用的引导加载程序。

`info pages` —— 一组通过输入 `info` 命令获取的本地、易于读的命令语法文档。

`journaling` —— 一种跟踪需要写入硬盘信息的文件系统类型；常见的日志文件系统包括 ext3 和 REISER。

`kernel parameters` —— 可以传递给 Linux 内核以更改工作方式的特定信息。

`large block addressing 32-bit (LBA32)` —— 一个可以在引导加载程序中指定的启用大块寻址的参数；只有在使用系统 BIOS 不完全支持的大硬盘时才需要。

`manual pages` —— 最常见的本地命令语法文档，通过输入 `man` 命令获取。也称为 man pages。

`metacharacters` —— Linux 操作系统中具有特殊含义的键组合。

# 第 3 章 Linux 安装与使用

`options` — 选项：以 "-" 或两个连字符开头的特定字母出现在命令名之后，用于更改命令的工作方式。

冗余磁盘磁盘阵列 (`RAID`) — 一种存储类型，可以将硬盘组合在一起以实现容错。

`REISER` — Linux 中使用的一种日志文件系统。

`shell` — 壳 —— 一种接受用户输入并将输入传递给内核进行处理的用户界面。

`swap memory` — 交换内存 —— 另见虚拟内存。

`terminal` — 终端 —— 允许特定用户登录并通过用户界面与内核通信的通道。

`VFAT`（虚拟文件分配表） — Linux 中可能使用的非日志文件系统。

`virtual memory` — 虚拟内存 —— 硬盘上的一个区域（交换分区），当物理内存（RAM）被过度使用时，该区域可用于存储通常驻留在物理内存中的信息。

## 复习习题

+ 1. Linux 中的默认 shell 叫什么名字？
  a. SH
  b. BSH
  c. CSH
  d. BASH

+ 2. 哪个命令相当于 `man` 命令，通常为被查询的命令提供更易读的描述，并包含指向其他相关信息的链接？
  a. who
  b. man help
  c. man -descriptive
  d. info

+ 3. 使用什么命令可以立即安全关闭 Linux 系统？
  a. shutdown -c
  b. shutdown -r
  c. down
  d. halt

+ 4. 什么命令相当于 `man -k` 关键字命令？
  a. find keyword
