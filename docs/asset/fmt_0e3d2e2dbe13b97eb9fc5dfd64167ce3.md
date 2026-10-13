
```
$ chfn
Changing finger information for bhudson.
Password:
Name []: Bernice Hudson
Office []: Suite 56 N. Centennial Blvd.
Office Phone []: 919 555-1212
Home Phone []: 919 555-1213
Finger information changed.
```

系统将引导你完成一系列提示以输入新的或更新的信息。请注意，`chfn`命令不允许你在输入信息时使用任何逗号。你可以通过几种方式来验证此信息，例如查看`/etc/passwd`的内容：

```
$ grep bhudson /etc/passwd
bhudson:x:501:501:Bernice Hudson,Suite 56 N. Centennial Blvd.,\
919 555-1212,919 555-1213:/home/bhudson:/bin/bash
```

你还可以通过使用`finger`命令来验证更新的用户信息：

```
$ finger bhudson
Login: bhudson
    Name: Bernice Hudson
Directory: /home/bhudson
    Shell: /bin/bash
Office: Suite 56 N. Centennial Blvd.
    Office Phone: 919 555-1212
Home Phone: 919 555-1213
Never logged in.
No mail.
No Plan.
```

## 阅读文档

虽然你在本书中学习了使用 Fedora 的基础知识，但你需要时间和练习来掌握并排除 Linux 操作系统和你的发行版中更复杂方面的故障。与任何操作系统一样，随着你继续使用 Linux，你预计会遇到一些问题或令人困惑的问题。解决这些问题的第一个求助对象是随系统提供的文档；如果你无法在那里找到所需信息，请查看 Fedora 的网站。

> **注意**
>
> 检查 Fedora 网站以获取安全更新和 bug 修复是个好主意。浏览到 http://fedoraredhat.com/download/。或者，你随时可以运行一次快速的`yum update`以确保你的系统拥有最新可用的软件。

Linux 与 Unix 一样，是一个自文档化系统，可以通过`man`命令访问手册页。Linux 提供许多其他有用的命令来访问其文档。你可以使用`apropos`命令——例如，使用诸如`partition`之类的关键词——来查找与分区相关的命令，如下所示：

```
$ apropos partition
GNU Parted [parted]     (8) - a partition manipulation program
fdisk                   (8) - Partition table manipulator for Linux
jfs_mkfs                (8) - create a JFS formatted partition
jfs_mkfs [mkfs]         (8) - create a JFS formatted partition
lvmdiskscan             (8) - scan for all disks / multiple devices / partitions
➜ available
mpartition              (1) - partition an MSDOS hard disk
partprobe               (8) - inform the OS of partition table changes
pvcreate                (8) - initialize a disk or partition for use by LVM
sfdisk                  (8) - Partition table manipulator for Linux
```

若要查找命令及其文档，你可以使用`whereis`命令。例如，如果你在寻找`fdisk`命令，可以这样做：

```
$ whereis fdisk
fdisk: /sbin/fdisk /usr/share/man/man8/fdisk.8.gz
```

### 使用 man 手册页

若要了解有关命令或程序的更多信息，请使用`man`命令，后跟命令的名称。Linux 和 X Window 命令的手册页位于`/usr/share/man`、`/usr/local/share/man`和`/usr/X11R6/man`目录中；因此，例如，若要阅读`rm`命令的手册页，请像这样使用`man`命令：

```
$ man rm
```

在你按下**Enter**后，`less`命令（一个被称为分页器的 Linux 命令）显示手册页。`less`命令是一个文本浏览器，你可以使用它在文档中前后（甚至左右）滚动以了解有关该命令的更多信息。键入字母**h**获取帮助，使用前斜杠输入搜索字符串，或按**q**退出。

**注意**

虽然随 Linux 提供的数百个 GNU 命令中几乎每一个都有手册页，但有关使用 GNU 命令的详细信息必须使用`info`命令阅读。例如，若要进一步了解`bash`（它有一个相当详尽的手册页），请像这样使用`info`命令：

```
$ info bash
```

按下**n**和**p**键以在文档中导航，或向下滚动到屏幕上的菜单项并按下**Enter**以阅读关于特定功能的内容。按**q**退出阅读。

## 查找和阅读软件包文档

各种软件包的文档包含在`/usr/share/doc`目录中；该目录存储在一个用关联软件包名称标记的另一个目录中。你可以通过浏览`http://www.tldp.org`在线找到其他 Linux 文档，这些文档被称为 HOWTO 和常见问题解答（FAQs）。HOWTO 文档包含与特定主题相关的特定信息，例如打印、设置网络、编程串行端口或在 Linux 上使用 CD-ROM 驱动器。这些文档可以使用你的网络浏览器阅读。当然，你可以使用的最佳在线工具之一是好的搜索引擎，例如 Google。

你可以使用`less`或其他分页器或文本阅读器阅读文本等文档格式。例如，若要阅读 GNU 通用公共许可证（GPL）的副本，即`/usr/share/apps/LICENSES`目录下名为`GPL_V2`的文件，请像这样使用`less`：

```
$ less /usr/share/apps/LICENSES/GPL_V2
```

在你按下**Enter**后，你可以前后滚动该文件。按**q**退出阅读。如果文档处于压缩形式（以`.gz`结尾），请使用`zless`分页器，它会先解压文档：

```
$ zless /usr/share/man/es/man1/README.gz
```

大多数用户使用图形桌面中的网络浏览器阅读 HTML 等文档格式。然而，Fedora 至少包含两个通用的基于文本的网络浏览器，可以通过`lynx`和`links`命令访问。要在不使用 X11 的情况下浏览系统上的 HTML 文件，请使用任一命令以及该文件的路径。例如，若要使用`links`阅读 GNU GPL 的 HTML 版本，请像这样使用命令：

```
$ links /usr/share/doc/HTML/en/common/gpl-1icense.html
```

在你按下 Enter 后，使用你的**Up**和**Down**光标键前后滚动文件。按**q**退出阅读。如果你已配置了鼠标，点击屏幕顶部附近的左键，`links`将显示其菜单。

## 使用 Shell

Shell 是一个具有许多不同特性的交互式命令提示符：

- 输入和输出重定向
- 后台处理
- 作业控制
- 历史编辑
- 内置帮助
- 命令行补全
- 命令行编辑

Shell 解释键盘命令，并通常使用 Shell 的解释器语言（称为*shell 脚本*）来启动其他命令或程序。

> **注意**
>
> Shell 脚本在第 14 章中讨论。

你使用的 Shell 由系统`/etc/passwd`文件中你的条目的最后一个字段指定。此示例针对名为`andrew`的用户，显示登录 shell 是`bash`：

```
andrew:x:502:502::/home/andrew:/bin/bash
```

大多数 Linux 发行版（包括 Fedora）的默认 shell 是 GNU `bash`或 Bourne Again Shell，但其他 shell，如`tsh`、`ksh`和`zsh`也可用。你可以在命令行中键入其名称来使用不同的 shell。或者，root 操作员在创建该用户帐户时可能将用户分配给另一个 shell（参见本章后面的“作为 Root 工作”）。
