
充分利用 KDE。第三组链接提供了对手册页和 GNU info 页面的访问，就像 GNOME 帮助浏览器一样。第三组中的一个链接使您能够使用一个或多个关键字搜索在线帮助。

要查找手册页，请单击标记为 **系统手册页内容** 的链接。这会显示在线手册页的目录，按用户命令、文件格式和系统管理等部分组织。单击某个部分标题即可查看该部分中的项目列表。然后可以单击特定项目以阅读该项目的手册页。例如，要了解有关 `xinetd` 配置文件的更多信息，请选择标记为 **文件格式** 的部分。然后单击标记为 `xinetd.conf` 的链接。KDE 帮助随后会显示有关 `xinetd` 配置文件的信息的手册页。

您还可以通过单击 KDE 桌面上标记为 `www.redhat.com`、`Red Hat Errata` 和 `Red Hat Support` 的三个 Red Hat 图标之一，直接访问 Red Hat 的网站。这些图标中的每一个都是指向特定 Red Hat 网站的链接。例如，单击 `Red Hat Support` 会带您进入 `support.redhat.com` 网站。

## 使用 Linux 命令获取帮助

通过图形帮助浏览器浏览帮助信息很方便，但在终端窗口中输入 Linux 命令时您经常需要帮助。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_366_0.png)

您还应知道的另一个技巧是大多数 Linux 命令都有帮助选项。通常，如果您使用 `--help` 选项调用命令，命令会打印一些帮助信息。至少，此信息包括命令接受的命令行选项。通常帮助信息可能跨越多个屏幕，因此您应该将输出通过管道传输到 `more`，如下例所示：

```
ls --help | more
```

## man 命令

您可能隐约记得命令的名称，但记不起应该输入的确切语法。这正是 `man` 命令可以为您提供帮助的情况。使用 `man` 命令，您可以查看 Linux 命令的手册页，然后正确使用该命令。

您需要记住要查找在线帮助的命令。例如，要查看 `modprobe` 命令的手册页，请在终端窗口中输入以下命令：

```
man modprobe
```

`man` 命令随后逐页显示帮助信息。按 **空格键** 移动到下一页。按 `b` 向后移动一页。要在手册页中查找特定单词，请按正斜杠 `/`，输入该单词，然后按 **回车键**。例如，要搜索单词 `debug`，请输入 `/debug` 并按 **回车键**。阅读完手册页后，按 `q` 返回 Linux 命令提示符。

## whatis 命令

如果您不想阅读完整的手册页，可以使用 `whatis` 读取命令的一行摘要。例如，以下是如何使用 `whatis` 查看 `modprobe` 命令的简要描述：

```
whatis modprobe
modprobe          (8) - high level handling of loadable module
```

数字 `(8)` 表示 `modprobe` 命令列出的手册页部分。您应该尝试 `whatis` 命令来查看其他几个命令的一行描述。

您可以使用 shell 的通配符功能和 `whatis` 命令来探索 `/bin`、`/sbin`、`/usr/sbin`、`/usr/bin` 等各种系统目录中的文件。只需更改到感兴趣的目录，然后输入 `whatis *` 即可查看该目录中程序的一行描述。 （`whatis` 会为有此类信息的程序显示信息。）例如，以下是如何探索 `/sbin` 目录：

```
cd /sbin; whatis * | more
arp               (7) - Linux ARP kernel module
arp               (8) - manipulate the system ARP cache
askrunlevel: nothing appropriate
badblocks         (8) - search a device for bad blocks
cardctl           (8) - PCMCIA card control utility
cardmgr           (8) - PCMCIA device manager
... rest of the output not shown ...
```

如您所见，输出是当前目录中所有程序的字母顺序列表，以及可用的单行描述。如果程序没有可用信息，`whatis` 命令会显示 `nothing appropriate` 消息。

## apropos 命令

当您知道命令的名称时，`man` 和 `whatis` 命令很有用。如果您不知道命令的确切名称，可以使用 `apropos` 命令通过关键字（甚至是单词的一部分）搜索命令。例如，如果您记得命令包含单词 `probe`，请键入以下 `apropos` 命令进行搜索：

```
apropos probe
modprobe          (8)  - high level handling of loadable modules
pnpprobe          (8)  - scan ISA bus for PnP sound cards
SuperProbe        (1x) - probe for and identify installed video hardware
```

在这种情况下，搜索结果显示了三个候选命令，每个命令都有简要描述。然后您可以选择执行所需操作的命令。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_368_0.png)

如果 `apropos` 显示的命令列表过长，滚动速度过快而无法阅读，您可以键入 `apropos keyword | more` 来一次查看一个屏幕的输出。

## 查阅在线 HOWTO 文件

您可以参考的另一种在线文档形式是 HOWTO 文件列表，您可以通过在 Netscape Communicator 中打开 URL `http://www.redhat.com/mirrors/LDP/` 来访问。该 URL 中的 LDP 指的是 Linux 文档项目，在该网页上，您可以找到指向常见问题解答（FAQs）和 HOWTO 的链接。您可以单击 HOWTOs 链接并以多种格式下载（或阅读）HOWTO 文档，包括文本和 HTML 格式。例如，如果您单击查看文本格式的 HOWTO，Web 浏览器会显示超过 170 个 HOWTO 文件的列表（见图 30-1）。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_369_0.png)

**图 30-1**

通过 GNOME 桌面的 LDP 图标可访问的 HOWTO 文件部分列表

每个 HOWTO 文件都包含有关 Linux 某个方面的信息，例如如何在 Linux 中配置硬件或如何创建启动磁盘。要查看这些 HOWTO 文件中的任何一个，请单击名称，Web 浏览器将加载完整文本文件。例如，图 30-2 显示了单击 CD-Writing HOWTO 的结果，该 HOWTO 解释了如何使用安装在 Linux 系统中的 CD-ROM 可记录（CD-R）设备刻录 CD。

您应该浏览 HOWTO 文件列表（见图 30-1），并查看一个或多个感兴趣的文件。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_369_1.png)

在 HOWTO 文件列表的最后，您会看到一个名为 `mini` 的文件夹。单击该链接即可查看 mini-HOWTO 列表，这些 HOWTO 涵盖了更多更 narrowly focused 主题。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_370_0.png)

**图 30-2**

浏览 CD-Writing HOWTO 文件的纯文本版本

## 访问其他 Linux 资源

除了我刚刚描述的在线帮助之外，还有几个其他资源可以提供有关特定主题的更多信息。大多数资源都在互联网上，因为您可以在那里获得有关 Red Hat Linux 和 Linux 的最新信息。本节的其余部分将向您介绍其中一些 Linux 资源。不是提供冗长的 URL 列表，我展示了几个关键网站，您可以用它们作为搜索的起点。

### 网页

如果您浏览互联网，您可能会注意到有相当多的网页包含 Linux 相关信息。一个好的起点是以下 Linux 页面：

```
http://www.linux.org/
```

此页面提供了查找有关 Linux 信息的起点。您可以单击按钮以访问该按钮标签标识的主题的更多信息。在此页面上，您还可以找到 Linux 相关网站的有组织的链接集合。

要浏览有关 Linux 的最新新闻，请访问位于以下位置的 Linux Resources 页面：

```
http://www.linuxresources.com/
```

Specialized Systems Consultants (SSC), Inc.，*Linux Journal* 的出版商，维护此页面。您可以浏览 *Linux Journal* 最新一期的文章，并了解其他信息，例如内核的最新版本以及指向其他 Linux 资源的链接。

另一个流行且权威的 Linux 信息来源是 Linux 文档项目（LDP）的主页，其 URL 如下：

```
http://www.linuxdoc.org/
```

在此网站上，您可以找到指向互联网上其他 Linux 资源的更多指针。特别是，您可以从 `http://metalab.unc.edu/pub/Linux/docs/HOWTO/` 浏览和下载最新的 HOWTO 文档。

对于 Red Hat Linux 特定问题，您可以访问 Red Hat 的支持网站：

```
http://www.redhat.com/apps/support/
```

此网站提供诸如 *产品更新和勘误*、*硬件兼容性列表* 和 *安装指南和手册* 等链接。特别是，您可以在 `http://www.redhat.com/support/docs/howto/` 找到手册和常见问题解答（Frequently Asked Questions）。

### Internet 新闻组

要跟上 Linux 的发展，您确实需要访问互联网，特别是新闻组。您可以在表 30-1 所列的新闻组中找到有关特定 Linux 相关主题的讨论。
