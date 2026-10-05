

```
[global]
printing = bsd
printcap name = /etc/printcap
load printers = yes
guest account = nobody
log file = /usr/local/samba/log.%m
admin users=ricks markk
read prediction = yes
dead time = 15
workgroup=AURAGROUP
mangled map=(*.html,*.htm)
lock directory = /usr/local/samba/var/locks
share modes = yes
os level = 33
domain master = yes
```

```
[homes]
comment = Home Directories
browseable = no
read only = no
create mode = 0750
read size = 8192
max xmit = 8192
```

```
[printers]
comment = All Printers
browseable = no
printable = yes
public = yes
writable = no
create mode = 0700
```

```
[pcsoft]
comment = PC Software
path = /vol/repository
public = no
only guest = no
writable = yes
printable = no
create mode = 0666
```

```
[accounting]
path = /home/bob/shared
valid users = fred bob
public = no
only guest = no
browseable = no
writable = yes
create mask = 0777
```

## 9.3 在 Windows 上安装 Linux 打印机

与 Windows 系统的 system.ini 一，文件被分为以括号中的单词开头的节；`smb.conf` 文件也是如此。`[global]`、`[printers]` 和 `[homes]` 是三个保留的节头。所有其他节都被假设为可用的共享名称。`[global]` 部分适用于整个程序。例如，`mangled map` 选项表示所有以 .htm 结尾的 Samba 文件都应该以 .html 格式写入 Linux 服务器。这使得在 Windows 中写入文件并将其发送到 Web 器上变得更加容易。

其他值得注意的选项还包括：

- log file——当 `smbd` 启动时，它将在这里写入其日志文件。在上面的情况下，日志文件的名为“log.”加上机器名称。这提供了唯一的日志文件。
- dead time——在没有活动超过`<dead time>` 分钟后，smb 连接将断开。这不仅有助于节省 Linux 服务器上的资源，还能允许 Samba 在 Windows 机器崩溃时恢复。一个好的选择是 15 分钟左右。
- admin users——这些用户的权限等同于 root。事实上，他们对所有共享都有 root 权限。这里应该只有你或管理 Samba 的人员。
- workgroup——要连接的工作组。这应该与你早些在 Windows 中设置的名称相同。

这些节将放在用户 Windows 主目录的“浏览网络”部分。用户随后可以点击或挂载该目录，它就是他们在 Linux 上的主目录。

一旦在网络上安装了 Samba，你可以通过启动 `smbd` 和 `nmbd`（它们处理类似于 DNS 的功能）并进行网络浏览来测试。你应该能在机器列表中看到你的 Linux 机器（见图 9–1）。

Samba 足够了解（通过 `printing = bsd` 和 `printcap name = /etc/printcap`），可以加载 `/etc/printcap` 中所有可用打印机并让 SMB 客户端可以使用。Linux 侧不需要任何更改，但你可能需要确保 `/etc/printcap` 文件已成功设置并且你可以打印。Samba 还会处理任何远程打印机

## 第 9 章 • Samba

![](img/cd7585e53abd949068548271c07fcdd8_135_0.png)

**图 9–1** Dingle 和 Galaxy 是运行 Samba 的 UNIX 服务器

你从从 Linux 获取的任何打印机都应该可以通过 Samba 使用（见图 9–2）。

Windows 侧可能会稍微复杂一些。直接与打印机通信的更复杂的打印驱动程序可能会给你带来一些问题。我的第一个建议是获取一个支持 PCL 或 Post-Script 的打印机。这样，你至少可以将数据发送到打印机。请注意，现在出的更多打印机可能使用“Windows 打印系统”，它除了 Windows 之外的任何系统无法工作。如果你有一个接受 PCL 或 PostScript 的打印机，你可以在 Windows 中安装通用驱动程序来打印 Samba 打印机。我在使用 Apple LaserWriter 作为 PostScript 打印机以及 HP LaserJet 4 作为 PCL 打印机方面获得过成功。

一旦配置了打印机和共享，你就可以让用户使用了。务必密切关注日志文件，以便在出现问题时进行监控。

> ⁴你的实际情况可能会有所。尝试在 Windows 下使用其他打印驱动程序看看它们的效果如何。

## 9.4 总结

![](img/cd7585e53abd949068548271c07fcdd8_136_0.png)

**图 9–2** Galaxy 可用的打印机和共享驱动器列表。

## 9.4 总结

- Samba 是与 Windows、Windows 95 和 NT 机器共享磁盘空间和打印机的简单方法。

# NetNews 10

# 在你的 Linux 机器上安装 INN 程序。

Usenet News 是一个全球分发的讨论系统，支持许多被称为新闻组（newsgroups）的不同主题论坛。

几乎所有可以想象的主题都涵盖在 Usenet 范围内，而且每天都会添加新的新闻组以跟上流行需求。Usenet 可用于研究、娱乐或仅仅寻找有共同兴趣的人。有关从用户和历史角度对 Usenet 的更深入的描述，请参考位于以下位置的“什么是 Usenet”FAQ（常见问题解答）：

```
ftp://rtfm.mit.edu/pub/usenet-by-group/news.answers/usenet/what-is/part1
```

以及

```
ftp://rtfm.mit.edu/pub/usenet-by-group/news.answers/usenet/what-is/part2.
```

# 第 10 章 · NetNews

Usenet 的历史始于 1979 年，当时两个研究生学生 Tom Truscott 和 Jim Ellis 考虑使用 UNIX 复制软件（UUCP）来连接机器，用以便在用户之间进行信息交换。起初，流量由许多 shell 脚本处理，但第一个公共软件是 Anews。Anews 规模很小，设计时每天每个组处理处理超过几篇文章。当读者数量增加时，Anews 被重写并于 1982 年作为 Bnews 发布，随后在 1987 年再次重写为 Cnews。RFC 850 和 1036 标题为《USENET 消息交换标准》，详细说明了 USENET 主机之间进行网络新闻消息交换的格式，定义了新闻消息的格式、传输方法和传播方法。

在 Cnews 之前的所有新闻服务器版本主要都以 UUCP 网络为目标，尽管它们也可以在不同的协议上使用。

随着 TCP/IP 和 DEC-Net 等其他网络的日益普及，必须开发更高效的新闻传输方法，因此网络新闻传输协议（NNTP）于 1986 年诞生。NNTP 被设计为一种“存储和转发”技术，这意味着新闻文章存储在中央数据库中，读者从中拉取单篇文章。关于 RFC 977《一种基于流的新闻传输建议标准》的更多技术细节如下。

起初，NNTP 仅作为 Cnews 的一个附加包可用，但开发了互联网新闻程序，更广为人知的名称是 ANN。ANN 将 NNTP 部分与新闻服务器本身相结合，使得安装和配置比以前更容易。最初，ANN 软件由 Rich Salz 编写和维护，直到 1993 年年中发布的 ANN1.4sec。那时，Rich 没有时间维护分发版，Dave Barr uno 介入并接管了维护，编写了软件的 1.4off 版本。1996 年，Rich 将 ANN 分发版交给了互联网软件协会（ISC），并约定他们将接管未来 ANN 版本的维护和开发。ISC（主要是 James Brister）合并了在非官方 off 版本中发生的更改，然后添加了更多功能并修复了错误，产生了 1.5 及以上版本。

今天，互联网上的大多数站点使用 ANN 作为它们的新闻服务器，但各种新开发的服务器，如 Cyclone、Dnews、Diablo 等。本章主要介绍 ANN 软件以及如何在 Linux 系统上对其进行安装、配置和故障排除。

## 10.1 INN 安装前的考虑

# 10.1 INN 安装前的考虑

在实际安装 INN 并开始接收新闻之前，有几点需要考虑。INN 是一项内存密集型和磁盘密集型软件，特别是当机器接收并存储大量文章时。提前确定所需的内存和磁盘空间，并规划文件系统的布局，可以为将来省去很多麻烦。

## 空间考虑

Usenet 会消耗大量的磁盘空间，取决于你运行多少新闻组以及新闻组属于什么层级。提前估计日志、实际新闻存储区域和新闻二进制文件需要多少磁盘空间。目前，完整的新闻流每天产生 3 到 4 GB 的侵入新闻。其中大部分被 alt.* 层级占据，其中最大的部分是 alt.binaries 层级。

如果你想接收部分新闻但没有太多可用空间，请考虑只获取部分新闻。你可以根据层级或指定组名限制保留的内容。如果你对某些主题感兴趣，接受讨论这些主题的小组。通常，除非运行 ISP 或服务，大多数人选择只接受部分新闻，因为有许多你无法理解的语言的组。

对于较大的安装，将日志、二进制文件和配置文件放在不同的分区上通常是一个好主意。新闻二进制文件和配置文件占用的空间基本不变，可以与其他二进制文件放在同一个分区上（通常在 /usr 或 /usr/local）。剧烈变化的片段是大小和日志文件分区。日志文件分区必须至少是正常使用空间的两倍，因为当 expire（清理程序）运行时，INN 会创建历史文件的多个副本。池区域必须容纳你希望保留的几天新闻，并能够处理本地机器或上游新闻提供商宕一段时间后发送大量积压新闻的偶发情况。

