
Linux 2.6.10-1741_FC3 (desktop.andbhudson.co.uk) (2005年6月4日星期五 15:43)

```
login: andrew
```

输入用户名（在此例中为 `andrew`）后按回车，系统会提示你输入远程系统上的密码：

```
Password:

Last login: Fri Jun 4 17:12:35 from 192.168.2.2

andrew@desktop]$
```
输入密码后，你就可以在远程计算机上工作了。再次，你在与远程计算机通信时通过键盘输入的所有内容都是加密的。使用 `exit` 或 `logout` 命令退出会话并返回自己的计算机。

> 警告
下一个远程访问命令 `telnet` 被列为示例是因为包含在许多 Linux 发行版中，但不应该使用它：`telnet` 以明文形式跨网络传输你的用户名和密码，这将为你的系统带来巨大的安全风险。此外，请注意，此服务必须在远程计算机上显式开启并允许（通过编辑 `/etc/xinetd.d` 目录下名为 `telnet` 的文件并重启 `xinetd`；有关启动或重启服务的更多信息，请参阅第 15 章中的“手动启动和停止服务”部分）。

## 注意

旧版本的 Linux 操作系统限制用户名长度为 8 个字符。当前版本的 Ubuntu 用户限制为 32 个字符。良好的密码至少至少 8 个字符，并包含大小写字母和数字。可以使用 `mkpassword` 命令为用户生成随机密码。

你无法更改用户名，但可以更改用户信息，如地址、电话等。你使用 `chfn` 来进行这些更改。该命令将修改系统文件 `/etc/passwd` 中的条目，该文件供 `finger` 命令显示系统用户信息。例如，在命令行输入 `chfn` 并按回车：

```
$ chfn

Password:

正在更改 andrew 信息

输入新值，或按回车使用默认值

Full Name [None]: 17

Room Number Phone [0122544556]: 0122512223

Home Phone [0122512233]: 0122544556
```

你将被引导一系列提示输入新的或更新的信息。注意，`chfin` 命令不允许在输入信息时使用逗号。你可以通过两种方式验证这些信息，例如查看 `/etc/passwd` 的内容：

你也可以通过 `finger` 命令验证更新后的用户信息：

```
$ finger andrew

Login: andrew               Name: Andrew Hudson

Directory: /home/andrew      Shell: /bin/bash

Office: 17, +0-122-551-2233  Home Phone: +0-122-544-5566

On since Tue May 30 20:54 (BST) on :0 (messages off)

On since Tue May 30 20:55 (BST) on pts/0 from :1.0

No mail.

No Plan.
```

## 阅读文档

尽管你在本书书中学习了 Ubuntu 的基础知识，但你仍需要时间通过实践来掌握并解决 Linux 操作系统及其发行版中更复杂的问题。与任何操作系统一样，在你继续使用 Linux 时，你可能会遇到一些问题或困惑的问题。解决这些问题的首选地方是系统自带的文档；如果你在那里没有找到所需的信息，请检查 Ubuntu 网站。

注意

在 Ubuntu 网站检查安全更新和错误修复是一个好主意。请访问 `http://www.ubuntu.com`。或者，你也可以随时快速运行 `sudo apt-get update && sudo apt-get dist-upgrade` 来确保你的系统拥有最新的软件。

Linux 与 UNIX 不同，它是一个自文档化的系统，可以通过 `man` 命令访问 man 手页（帮助页）。Linux 还提供了许多其他有用命令来访问其文档。你可以使用 `apropos` 命令——例如使用如 `partition` 等关键字来查找与分区相关的命令，如下：

```
$ apropos partition
cfdisk (8)
- 基于 Curses 的 Linux 磁盘分区表操作器
fdisk (8)
- Linux 分区表操作器
jfs_mffs (8)
- 创建 JFS 格式的分区
mdrun (8)
- 自动检测并激活所有  分区
mkfs.jfs (8)
- 创建 JFS 格式的分区
parted (8)
- 分区操作程序
partprobe (8)
- 通知操作系统分区表更改
pcreate (8)
- 为 LVM 初始化磁盘或分区
presize (8)
- 调整 LVM2 使用的磁盘或分区的大小
sfdisk (8)
- Linux 分区表操作器
```

要查找某个命令及其文档，你可以使用 `where` 命令。例如，如果你正在寻找 `fdisk` 命令，可以这样做：

```
$ where fdisk

fdisk: /sbin/fdisk /usr/share/man/man8/fdisk.8.gz
```

# 使用 man 手页

要了解更多关于命令或程序的信息，请使用 `man` 命令后接命令名称。Linux 和 X Window 命令的 man 手页位于 `/usr/share/man` 和 `/usr/local/share/man` 目录下；例如，若要阅读 `rm` 的 man 手页，可以使用如下命令：

```
$ man rm
```

当你按下回车键时，`less` 命令（一种 Linux 分页器）会显示 man 手页。`less` 命令是一个文本浏览器，你可以用它向前向后（甚至是侧向）滚动文档，以学习更多关于命令的信息。输入字母 `h` 获取帮助，使用正斜杠 `/` 输入搜索字符串，或按 `q` 退出。

虽然 Linux 包含的数百个 GNU 命令中几乎每一个都有一个 man 手页，但关于使用 GNU 命令的详细信息必须使用 `info` 命令来阅读。例如，要学习关于 bash（它有一个相当详尽的手手册），可以使用如下 `info` 命令：

```
$ info bash
```

按 `n` 和 `p` 键在文档中导航，滚动到屏幕上的菜单项并按回车键阅读特定功能的介绍。按 `q` 退出阅读。

# 查找和阅读软件包文档

各种软件包的文档包含在 `/usr/share/doc` 目录下；该目录存储在另一个以相关包命名的目录中。你可以通过访问 `http://www.tldp.org/` 在线查找其他 Linux 文档，即 HOWTOs 和常见问题解答（FAQs）。HOWTOs 包含与特定主题相关的特定信息，如打印、设置网络、为串口编程或在 Linux 下使用 CD-ROM 驱动器。这些文档可以使用你的网络浏览器阅读。当然，你可以使用的最佳在线工具之一是搜索引擎，例如 Google。

你可以使用 `less` 或其他分页器/文本器阅读文档格式。例如，若要阅读 GNU 通用许可证（GPL）的副本（位于 `/usr/share/apps/LICENSES` 目录下的 GPL-V2 文件），可以使用如下 `less` 命令：

```
$ less /usr/share/common-licenses/GPL-2
```

当你按下回车键时，可以反复滚动文件。按 `q` 退出阅读。如果文档是压缩格式（以 `.gz` 结尾），请使用 `zless` 分页器，它会先解压文档：

```
$ zless /usr/share/man/man1/renice.gz
```

大多数用户在图形桌面中使用网络浏览器阅读 HTML 等文档格式。然而，Ubuntu 至少包含了两个通用的基于文本的网络浏览器，通过 `lynx` 命令访问。要在不使用 X11 的情况下浏览系统上的 HTML 文件，可以使用任一命令配合文件路径。例如，若要阅读带有链接的 GNU GPL 的 HTML 版本，使用如下命令：

```
$ links /usr/share/doc/HTML/en/common/gpl-license.html
```
