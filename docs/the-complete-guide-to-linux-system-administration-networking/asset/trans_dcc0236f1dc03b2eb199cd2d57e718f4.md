

你可以使用 (?) 来匹配单个字符，或使用 ( * ) 来匹配多个字符，就像你在 Microsoft Windows 中使用通配符一样。例如，如果你的当前工作目录是 /home/nwells/documents，则以下命令会将 /home/nwells/documents 中的所有文件复制到 /tmp/nwells：

```
$ cp * /tmp/nwells
```

你可以使用绝对路径和相对路径名与任何 Linux 命令一起使用。例如，如果你的当前工作目录是 /home/nwells/documents，则以下命令会将该目录中的所有文件复制到 /home/nwells（即你当前目录的父目录，用 .. 表示）：

```
$ cp * ..
```

> 在 Nautilus 窗口中，你可以通过在桌面上的另一个 Nautilus 窗口的文件夹中拖放来复制你用鼠标选择的一个或多个文件。你也可以右键单击文件并选择 Cut File 或 Copy File，然后更改目录，再次右键单击并选择 Paste Files。

要删除文件，请使用 rm 命令（意为 remove）。使用 rm 命令时要非常小心。当你使用 rm 删除文件时，该文件无法像图形桌面上的回收站或废纸篓中的文件那样恢复。Linux 图形桌面提供了一个 Trash 图标。当你在 Nautilus 窗口中选择一个项目并按下 Delete 键时，该项目会被删除并移动到 Trash。你可以双击桌面上的 Trash 图标来查看（如果需要可恢复）你使用 Nautilus 删除的任何项目。但是，rm 命令不使用回收站——它会永久删除文件。

在 Linux 中，移动和重命名文件这两个操作合并为一个命令，即 mv 命令。名称 mv 是 move 的缩写；本质上，重命名文件与将其移动到不同的文件名相同。例如，如果你在 /tmp 目录中有一个名为 report 的文件，你可以用以下命令将其移动到 /home/nwells 目录：

```
$ mv /tmp/report.doc /home/nwells
```

你可以在同一时间重命名文件，使用如下包含新文件名的命令：

```
$ mv /tmp/test.doc /home/nwells/test.backup
```

使用 mv 命令而不带目录名作为参数会将重命名的文件放在与原始文件相同的目录中。要将文件移动到不同的目录，请包含目录名，并可选择不同的文件名。

> 在 Nautilus 中，你可以通过从一个 Nautilus 窗口拖动文件或目录并将其放到另一个窗口中来将其移动到新位置。你也可以右键单击文件并选择 Cut File，然后更改目录，再次右键单击并选择 Paste Files。当使用 Nautilus 执行移动操作时，你必须单独通过右键单击并选择 Rename 选项来重命名文件。

## Viewing Files

Linux 提供了多种用于查看文件内容的实用程序。其中最简单的是 cat 命令，它将文件内容显示到屏幕上。例如，以下命令显示 test 文件的内容：

```
$ cat /etc/test
```

cat 命令还用于连接，或合并多个文件到一个更大的文件中——这就是该命令名称的由来。zcat 命令将压缩文本文件的内容显示到屏幕上。如果文件以字母 “.gz” 结尾，则它已使用 gzip 命令进行压缩。要在不先解压缩的情况下查看使用 gzip 压缩的文件的内容，请使用 zcat 命令。

大多数文件不适合一屏显示，在这种情况下 cat 命令工作太快——你只能看到文件中的最后 20 行左右的文本。要查看大文件，请使用 less 命令，它一次显示一个屏幕的文件内容。你可以使用箭头键或 Page Up 和 Page Down 在文件中的不同区域移动。要移动到下一屏文本，请按空格键。例如，以下命令一次一屏地显示一个大的配置文件：

```
$ less /etc/termcap
```

输入 q 以退出 less 命令。less 命令类似于 more 命令，也用于一次一屏地显示文件内容。less 命令比 more 命令具有更多功能，但你可以使用其中任何一个来查看文件内容。less 和 more 命令旨在显示文本文件（具有人类可读内容）。

你可以使用 file 命令来确定文件包含的内容。file 命令会告诉你文件中包含的数据类型。如果你不熟悉某个特定文件，请在使用 less 或 more 命令之前使用 file 命令查看其内容。例如，以下命令显示所指示文件的类型，结果出现在第二行：

```
$ file /etc/printcap
/etc/printcap: ASCII English text
```

如果你知道某个特定文件存在于你的 Linux 系统上，但记不起它在哪里，请使用 slocate 命令（意为 secure-locate）来查找它。例如，假设为了执行某项任务，你需要编辑一个名为 services 的配置文件，但你记不起它存储在哪个目录中。使用以下命令显示文件名或目录名中包含的所有 “services” 实例：

```
$ slocate services
```

另一个名为 locate 的命令提供与 slocate 相同的功能，但 slocate 更受青睐，因为它只显示你有权限访问的文件。

slocate 命令会显示包含你指定的文本字符串的任何内容的完整路径和文件名。你越精确，slocate 显示的列表就越短（因此越有帮助）。

在使用 slocate 之前，必须对文件和目录进行索引。如果你正在使用新安装的 Linux 系统，或一台不连续开机的系统，则可能尚未创建此索引。要创建它，你必须以 root 身份登录并执行 updatedb 命令。

本节介绍了你可以使用命令行管理文件和目录的几个 Linux 命令。这些命令和本章介绍的其他命令在章节末尾的 Command Summary 中进行了总结。在本章末尾的项目中，你可以练习使用这些命令。

## FINDING COMMAND HELP

本书向你介绍了作为 Linux 系统管理员工作所需了解的最重要主题和技能。你可以学习到比本书容纳的更多细节，并使用本节所述的资源探索额外的 Linux 主题。

### Reading Linux Documentation

由于 Linux 和其他自由软件项目的开发者完全通过互联网工作，他们通过电子或在线文档共享其软件的描述。这些文档通常在项目分发时被纳入其中，供大家使用。大多数 Linux 发行版都包含所有这些文档——数千页的材料，你可以使用几个简单的命令快速访问。

阅读 Linux 文档时，请记住其中许多是由软件开发者编写的。正因如此，Linux 软件的大量文档是假设你已经阅读了系统上的所有其他文档而编写的。你可以找到大量有用的细节，但作为 Linux 新手，你应该预期会读到许多最初不理解的内容。稍后重新阅读这些材料会使一切变得更清晰。

### The Linux Documentation Project

Linux Documentation Project（LDP）由 Matt Welsh 在 1990 年代初期创立，当时 Linux 刚刚在技术圈中为人所知。LDP 是最早记录 Linux 工作原理的努力之一，至今仍提供 Linux 文档

以多种格式提供。LDP 目前包含超过 6000 页的文档，所有文档均可在网上免费获取，采用适用于文档的 GPL 修改版本。LDP 由几种类型的文档组成。其中一些，例如 Network Administrator's Guide 和 Kernel Hacker's Guide，是完整的在线参考手册。

最初，你可能会发现 HOWTO 文档是 LDP 中最有用的部分。HOWTO 涵盖特定主题，例如在 Windows XP 和 Linux 之间共享系统，或维护网络安全。大多数文档由一位对该主题有专长的人撰写。称为 mini-HOWTO 的文档比常规 HOWTO 更专注于较窄的主题。HOWTO 文档通常由软件开发者撰写，但它们面向不熟悉所讨论主题的读者。

LDP 和所有 HOWTO 文档都包含在许多 Linux 发行版中，尽管由于其大小，通常默认不安装。你也可以在许多网站上阅读它们。

![](img/43f64015de86d989e30eff5bb284fb96_66_0.png)

> 开始研究作为 LDP 一部分提供的文档的一个好地方是 www.tldp.org。

### Linux on the Internet

Linux 在互联网上诞生，互联网仍然是了解更多关于 Linux 的好地方。每天，开发者发布新软件，公司发布关于 Linux 产品的公告，各种用户提供新的或修订的信息。当你遇到具有挑战性的问题时，一个有效的方法是访问 www.google.com 并输入问题的关键词。例如，假设你刚刚获得了一张新的无线网络卡，想知道 Linux 是否支持它。输入类似 “Linux driver D-Link DWL-2100AP” 的内容很可能会找到几条 Linux 管理员讨论如何使用该产品的消息。（如果你好奇的话，Linux 确实支持无线网络，并且新驱动程序定期可用。）表 1-3 列出了一些更通用的网站，在你探索 Linux 世界时可能会有用。

### Table 1-3 Linux-related Web Sites

| Web site | Description |
|---|---|
| www.linuxjournal.com | 与月刊印刷杂志配套的网站；包含额外的 Linux 链接和信息（大多偏技术） |
| www.linuxmagazine.com | 与月刊印刷杂志配套的网站；包含额外的 Linux 链接和信息，既有商业也有技术导向 |

