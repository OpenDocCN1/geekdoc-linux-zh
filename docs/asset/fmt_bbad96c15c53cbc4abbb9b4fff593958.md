
片刻之后，你将看到许多关于进程正在停止的消息。在较旧的系统中，你会看到一条关于系统正在停机的消息。此时你可以关闭电源。在较新的系统上，关机过程也会关闭电源。

如果你想重启系统而不是停止它，可以使用带有 `-r` 选项的 `shutdown` 命令，如下：

```
/sbin/shutdown -r now
```

另一方面，你也可以简单地输入 `reboot` 来重启系统。

## 查找在线文档

你应该熟悉红帽 Linux 中的一个重要信息源。每隔一段时间，你就会看到要求你输入 Linux 命令的指令。一段时间后，你不可避免会遇到这种情况：你模糊地记得某个命令的名字，但想不起它应该使用的确切语法。在这种情况下，Linux 手册页（manual pages）可以为你提供帮助。

要尝试本节节中的命令，你需要在 GNOME 中打开一个终端。选择“主菜单” -> “系统工具” -> “终端”（参考图 7-2）。这会打开一个你可以在其中输入 Linux 命令的窗口。

你可以使用 `man` 命令来查看命令的手册页——通常称为 man page。（你需要记住这个命令以访问在线帮助）。例如，要查看 `modprobe` 的手册页，请在终端窗口中输入以下命令：

```
man modprobe
```

该命令将逐页显示帮助信息。按**空格键**移动到下一页。按 **b** 向上移动一页。若要在手册页中查找特定单词，按正斜杠 `/`，输入单词，然后按**回车**。例如，搜索 "debug"，输入 `/debug`，当你读完手册页后，按 **q** 返回 Linux 命令行提示符。

## 第 7 章：红帽 Linux 基础

在介绍了在线帮助页的用途之后，我必须指出，“Linux 命令”指的是任何可执行文件，从包含其他 Linux 命令的脚本文件到标准的 Linux 可执行程序不等。尽管大多数标准程序都有页面，但许多程序并没有在线帮助。尽管如此，每当你难以回想起某个命令时，使用 `man` 命令查看该命令是否存在任何在线帮助都是值得的。

如果你不想阅读整个页面，可以使用 `whatis` 读取命令的单行摘要。例如，这里是如何使用 `whatis` 查看 `modprobe` 命令的简要描述：

```
whatis modprobe
```

`modprobe (8) - high level handling of loadable module`

数字 `(8)` 表示 `modprobe` 命令列出的章节。你应该尝试使用 `whatis` 命令来查看其他几个命令的命令行描述。

你可以利用 shell 的通配符功能和 `whatis` 命令来探索各种目录中的文件，如 `/bin`、`/sbin`、`/usr/sbin`、`/usr/bin` 等。只需切换到感兴趣感兴趣的目录并使用 `whatis` 查看该目录下程序的单行描述即可。例如，这里是你是如何探索 `/sbin` 目录的：

```
cd /sbin; whatis * | more
```

`addpart: nothing appropriate`

`adsl-connect (8) - Shell script to manage a PPPoe link`

`adsl-setup (8) - Shell script to configure Roaring Penguin PPPoe client`

`adsl-start (8) - Shell script to bring up a PPPoe link`

`adsl-status (8) - Shell script to report on status of PPPoe link`

`adsl-stop (8) - Shell script to shut down a PPPoe link`

`agegetty - alternative Linux getty`

`arp (7) - Linux ARP kernel module`

`arp (8) - manipulate the system ARP cache`

`arping (8) - send ARP REQUEST to a neighbour host`

`aryst: nothing appropriate`

`avmcapitrl (8) - Add, reset or remove AVM cards and load firmware`

`are`

`badblocks (8) - search for device for bad blocks`

`blockdev (8) - call block ioctls from the command line`

`capinit: nothing appropriate`

`cardctl (8) - PCMIA card control utility`

`cardmgr (8) - PCMIA device manager`

`chconfig (8) - updates and queries information for system services`

`clock (3) - Determine processor time`

... rest of the output not shown

如你所见，输出是当前目录下所有程序的字母顺序列表，以及可用的单行描述。如果某个程序没有可用信息，`whatis` 命令会显示“nothing appropriate”的消息。当你知道命令名称时，`man` 和 `whatis` 命令非常有用。如果你不知道命令的确切名称，可以使用 `apropos` 命令通过关键词（甚至是其部分内容）来搜索命令。例如，如果你搜索单词 "probe"，请输入：

```
apropos probe
```

`probe (8) - high level handling of loadable module`

`modprobe (8) - high level handling`
