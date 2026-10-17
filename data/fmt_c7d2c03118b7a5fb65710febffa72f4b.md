
**图 41.** Linux 上的 Samba 日志。

### 主日志文件

如果 Samba 出现问题，且`smb.conf`文件的语法检查通过，下一步是检查日志。存储在`/var/log`中的主日志文件会告诉你有关 Samba、NetBIOS 和 Winbind 守护进程的信息。以下是关于这些日志文件的详细信息：

- `log.smbd.` 每当 Samba 进程启动时，文件中都会有一个记录，包含日期和时间。
- `log.nmbd.` 在 Linux PDC 上，此文件包含浏览器数据。每当 NetBIOS 守护进程`nmbd`启动时，文件中都会有一个记录（更多信息请参见第 3 章“设置服务器系统”）。
- `log.winbind.` 在 Linux/Samba 域成员服务器上，此文件记录与 Microsoft 计算机连接的问题。
- `smbd:` 任何与 Samba 守护的问题都会记录在此文件中。
  > 在 Red Linux 9 中，由`glibc`包定义的标准库存在 bug。使用第 2 章介绍的 Red Hat 更新程序更新你的系统。确保下载的`glibc`版本不低于`2.3.2`。如果不升级，到 Samba 的连接可能是间歇性的。更多信息请访问`bugzilla.redhat.com/bugzilla/show_bug.cgi?id=90036`。
- `smbd:` 此文件存储 NetBIOS 查询和主选举。

- 确保网络配置恰当。
- 建立与域的连接。在 Microsoft Windows 9x/ME 上，你可以通过工作站的网络属性进行此操作。在 Microsoft Windows NT/2000/XP 上，步骤各不相同。
- 一旦连接到域，即可根据需要设置漫游配置（roaming profiles）。
- 根据需要连接到共享。
- 与域中的其他用户共享你选择的目录。

你可以从 MS-DOS 命令行界面执行这些中的许多功能。例如，你可以使用`net view`命令浏览域和工作组。你可以使用适当的`net use`命令连接到共享目录。

你会在对点网络中设置 Microsoft 和 Linux 计算机。当你连接到对点网络中的共享目录时，步骤取决于源端是 Windows 9x/ME、Windows NT/2000/XP 还是 Linux 成员服务器。

> 本章节的更新和更正可以在 Hentzenwerke 网站`www.hentzenwerke.com`。点击“Catalog”（目录）并导航到该书的页面。

## 第 7 章：配置打印机

### 第 7 章 配置打印机

就像 Bogart 和 Bacall、Sonny 和 Cher 或 Spike 和 Buffy 一样，在计算机网络世界中，文件服务器和打印总是形影相随。正如你可以配置 Samba 在 Microsoft Windows 风格的网络中共享目录一样，你也可以配置 Samba 和 Linux 打印服务器在同一网络上共享打印机。

可能你已经知道如何从 Microsoft Windows 计算机配置和共享打印机。在本章中，我将向你展示如何从 Linux 计算机配置和共享打印机。你可以从网络上的 Windows 或 Linux 工作站连接到共享打印机。

在编写本文时，Red Hat 有时会在你安装操作系统时自动安装打印机。Red Hat 假设任何安装了打印机的计算机都是打印服务器。如果你想从你的计算机或网络打印，在安装 Linux 之后可能需要配置本地或网络打印机。

两种打印服务与通用 Unix 打印系统（CUPS）和行打印守护进程（LPD）关联最紧密。在你计算机上安装 Red Hat Linux 9 时，这两者都是选项。它们是互斥的；虽然你可以在网络上运行 CUPS 或 LPD，但在任何情况下，你都可以使用 Red Hat 打印机配置工具来管理 Linux 工作站上的本地或远程打印机。

CUPS 还包含一个用于 SWAT（在第 3 章描述）的 Web 界面，允许你将多个不同的打印机连接为一个组。这组打印机在 CUPS 中被称为类（class）。LPD 有它自己的 Web 工具。与其他 GUI 工具一样，CUPS 和 Red Hat 打印机配置器是“前端”，可以帮助你编辑关键文本配置。

一旦你配置了 CUPS 或 LPD 打印机，你就可以通过 Samba 与你 Microsoft Windows 风格的网络上的其他计算机共享它。我将向你展示如何从 Microsoft Windows 和 Linux 工作站连接到这些打印机。

本章仅对 CUPS 和 LPD 提供了最简短的介绍。有关 CUPS 的详细书籍级信息，请参见`www.cups.org/documentation.php`上的文档。有关 LPD 的详细信息，请参考 Printing HOWTO，地址为`www.tldg.org/HOWTO/Printing-HOWTO/index.html`。

> 在编写本文时，Red Hat Linux 的继任者 Fedora Linux 将不包含 LPD 软件。

![](img/6ee4859e736a0839007ea9afb576c195_219_0.png)

### 软件包

如果你正在使用 Red Hat Linux 9，你可能安装了第 2 章“安装 Linux 作为文件服务器”中描述的打印支持组。如果你安装了该组中的默认包，你应该已经拥有在计算机上设置 CUPS 打印机所需的包。或者，如果你升级了或正在使用旧版本的 Linux，那么你的计算机上已经安装了 LPD 系统。例如，如果你已升级到 Red Hat Linux 7.x，LPD 应该仍然安装在计算机上。

无论你选择 CUPS 还是 LPD，请确保在网络上的每个 Linux 打印服务器和 Linux 工作站上安装了相同的 RPM。

在情况下，Red Hat 在`/etc/printcap`文件中列出配置的打印机。由于 Linux 打印服务器上`smb.conf`文件中的`printcap`命名变量，它连接到了 Microsoft Windows 风格的网络。

### CUPS 软件包

与 Red Linux 中的其他软件一样，CUPS 经过组织，并可以从 Red Hat 包管理器 (RPM) 软件包安装。这些软件包是以`.rpm`扩展名的文件组织在你的 Red Hat 安装光盘上的。记住，你可以使用`rpm -q packagename`命令检查包是否已安装。例如，以下命令检查主 CU 是否已安装：

```bash
$ rpm -q cups
```
