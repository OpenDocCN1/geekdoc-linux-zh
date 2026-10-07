

```bash
$ smbclient //server/share
```

输入此命令后，smbclient 会提示你输入密码，该密码必须与你在服务器上用户名关联的密码相匹配。（如果你在服务端的用户名与客户端不同，可以使用 `-U username` 参数来指定你在服务器上的用户名。）smbclient 中可用的命令与文本模式下的 ftp 程序或 Linux shell 中的命令类似——例如，查看可用文件；分别使用 put 和 get 在共享资源中传输文件；使用 cd 移动到新的目录；等等。你可以输入 `?` 或 `help` 来查看命令摘要。

虽然 smbclient 可能是快速传输少量文件的好方法，但如果你希望直接修改服务器上的文件，smbmount 会更加灵活。例如，你可能会使用此工具调用 Linux 程序来编辑存储在服务器上的文件。要使用 smbmount，请以以下形式发出命令：

```bash
$ smbmount //server/share mountpoint
```

**注意** 如果你没有以 root 身份发出 smbmount 命令，则必须将两个程序设置为 user ID (suid) root 才能正常工作：smbmnt（smbmount 的辅助程序）和 smbmount（用于卸载 SMB/CIFS 共享资源）。你可以发出命令 `chmod a+s /usr/bin/smbmnt /usr/bin/smbmount` 来完成此任务。

与 smbclient 类似，smbmount 在挂载共享资源之前会要求你输入密码。一旦共享资源被挂载，你就可以像访问本地磁盘上的文件一样访问其中的文件，但需注意某些事项。某些文件系统可能是只读共享的，因此你可能无法向这些共享资源写入文件。SMB/CIFS 不支持 Linux 式的拥有权和权限，因此默认情况下，所有文件都属于发出 smbmount 命令的该个人。当你用完某个共享资源后，可以使用 smbmount 命令卸载它；输入格式如下

```bash
$ smbmount mountpoint
```

如前所述，在 Samba 2.0.6 及更高版本中，你可以使用 mount 代替 smbmount。这样做时，你调用 mount 时使用 smbfs 文件系统类型，如下所示：

```bash
# mount -t smbfs //server/share mountpoint
```

除非你创建一个 /etc/fstab 条目，允许普通用户发出 mount 命令（如第 6 章所述），否则当调用者是 root 时，此流程效果最好。在这种情况下，你在发出 mount 命令时应省略文件系统类型、服务器名称和共享资源名称（例如 `mount mountpoint`）。

有几种用于 smbmount 的 GUI 前端。操作细节因程序而异，但作为一个总体规则，这些工具提供了一个本地网络的 GUI 视图，正如 LinNeighborhood（http://www.bnr.o.de/~schmidjo/）所展示的那样，如图 12.4 所示。当你双击一个共享资源以打开它时，一个对话框会询问你的用户名和密码，然后该程序将使用你在配置程序时指定的文件管理器在该共享资源上打开一个窗口。GUI 前端并没有真正为 Linux 的 SMB/CIFS 功能增加根本性的新功能，但它们确实使这些网络对不熟悉 Samba 文本模式工具的人来说更容易访问。因此，你可能希望安装 LinNeighborhood 或类似的软件包，如 Kruiser（http://devel-home.kde.org/~kruiser/）或 xSMBrowser（http://www.public.iastate.edu/~chadspen/）。

![](img/10371fe30b7fdac23ef2ef30d5ffe738_326_0.png)

图 12.4：LinNeighborhood 和其他 GUI SMB/CIFS 浏览器提供类似于 Windows 中网络邻居的用户界面。

## Internet 服务器

如果你希望在你离开计算机时仍能使用它，你必须在该计算机上安装某种类型的服务器。同样，如果你希望其他人能够使用计算机，也需要服务器。然而，合适的服务器取决于你的具体需求。虽然配置服务器有一些共同点，但每种配置都至少有一些独特的方面，因此你应该查阅相应的文档。

## 可用的服务器

Linux 支持各种各样的 Internet 服务器软件包。虽然这些软件包可以单独用于本地网络，但它们更常用于为 Internet 上的各种计算机提供服务。书中其他部分在较大或较小的程度上讨论了一些这些服务器。其中许多足够复杂，以至于整个书都是关于它们的。通常你可以在随服务器提供的文档文件中或专门介绍这些服务器的 Web 页面上找到更多信息。Linux 可用服务器的完整列表太长，无法在此复述；但一些最重要的服务器类型包括：

- **FTP 服务器**：*文件传输协议*（*FTP*）是 Internet 上最重要的协议之一，尽管它是不太显眼的。FTP 允许个人向 FTP 服务器传输文件或从 FTP 服务器传输文件。Web 页面上指向程序文件的链接通常是 FTP 链接。Linux 有多种可用的 FTP 服务器，例如 *华盛顿大学 FTP*（*WU–FTP*；http://www.wu-ftpd.org/）和 *ProFTP*（http://www.proftpd.net/）。Red Hat 随附 *WU–FTP*，但如果你愿意，可以为 Linux 安装任何其他 FTP 服务器。

- **邮件服务器**：如果你希望你的计算机直接接收发给它的邮件，你必须运行一个*邮件服务器*——也称为*邮件传输代理*（*MTA*）。（如果你的*ISP* 为你收集和保存邮件，你可能不需要一个 *MTA*；相反，你可以使用使用诸如*邮局协议*（*POP*）等协议的邮件程序来检索邮件。）所有主要的 Linux 发行版都随附一个 *MTA*，通常默认以合理的方式配置用于标准工作站。Red Hat 随附 *sendmail*（http://www.sendmail.org/），但存在各种替代方案，且被其他一些发行版使用。第 14 章涵盖 *sendmail*，但如果你的系统要专门用作邮件服务器，你应该考虑购买一本专门讨论该主题的书，例如 Craig Hunt 的 *Linux SendMail Administration*（Sybex, 2000）。

- **新闻服务器**：*网络新闻传输协议*（*NNTP*）控制*Usenet 新闻*的传输——这是一个全球性的讨论论坛，用户在其中发布关于各种主题（从素食烹饪到 Linux 再到国际空间站）的查询、解决方案和其他讨论。新闻服务器通常存在于 ISP 和大型组织（如大学）中。它们相互交换文章，从而实现了 *Usenet 新闻* 的全球范围。你可以自己运行一个新闻服务器，无论你是负责大型组织的新闻服务器，还是希望为一个内部使用或维护你感兴趣的新闻组本地副本的小型新闻服务器。Red Hat 随附 *Internet News*（*INN*），这是更受欢迎的新闻服务器软件包之一。对于一个仅维护少数新闻组的小型新闻服务器，*Leafnode*（http://www.leafnode.org/）可能更合适。请注意，如果你只是想*阅读 Usenet 新闻*，你不需要新闻服务器。为此，你需要一个*新闻阅读器*，如 *tin*（http://www.tin.org/）、*Knews*（http://www.matematik.su.se/~kij/）或 Netscape 的新闻阅读器组件。你还需要访问一个新闻服务器，例如由你的*ISP*维护的一个。

- **远程登录服务器**：如果你希望远程运行程序，你必须运行某种*远程登录服务器*。这是一种接受远程位置登录的程序。*Getty* 程序（在第 11 章中讨论）是用于拨号连接的登录服务器。对大多数人来说最熟悉的登录服务器是 *Telnet*，它接受来自整个 Internet 的登录。（此服务器随所有主要 Linux 发行版一起提供。）不幸的是，*Telnet* 以明文发送所有信息（包括密码），因此从安全角度来看并不是很好。在此方面更好的替代方案是 *安全外壳*（*SSH*），它对所有数据进行加密。*SSH* 的一个实现是 *OpenSSH*（http://www.openssh.com/），它成为 Red Hat 发行版 7.0 版的标准部分。

- **Web 服务器**：最可见的 Internet 服务器类型之一是 Web 服务器，它实现了*超文本传输协议*（*HTTP*）。在 Linux 上，*Apache*（http://www.apache.org/）是迄今为止最流行的 Web 服务器。*Apache* 足够复杂，以至于除了基本配置之外，你应该阅读一本关于它的书

317

