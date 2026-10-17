
你可以使用 `chkconfig` 命令来开启或关闭服务器：
`chkconfig pop-3 on`

请确保 `pop-3` 服务列在 `/etc/services` 中，并包含其端口号 `110`：
`pop-3 110/tcp`

# IMAP

互联网邮件访问协议 (`IMAP`) 允许远程服务器为用户存储邮件，用户随后可以登录访问这些邮件。与 `POP` 服务器不同，`IMAP` 服务器会保留用户的邮件。用户甚至可以将邮件保存到 `IMAP` 邮件服务器上。这样做的处处是将用户的邮件保持在网络上的一个中央位置，可以在网络上的任何地方进行访问。用户可以从网络上的任何主机登录邮件服务器，并读取、发送和保存邮件。这种交互式连接比 `POP` 协议需要更多的连接时间，最适合用户始终处于连接状态的以太网 `LAN`，而不是通过媒介拨号接入。

与 `POP` 不同，`IMAP` 允许用户在邮件服务器上设置多个文件夹，并在其中组织邮件。`IMAP` 还支持使用共享文件夹，多个用户可以访问特定主题的邮件。

华盛顿大学的 `IMAP` 服务器包含在 `Red Hat` 发行版中。其他 `IMAP` 服务器也同样可用，例如 `Courier-IMAP` 服务器 (`www.courier-mta.org`) 和 `Cyrus IMAP` 服务器 (`asg.web.cmu.edu/cyrus`)。`Courier-IMAP` 是一个小型、快速的 `IMAP` 服务器，提供了广泛的身份验证支持，包括 `LDAP`；`Cyrus IMAP` 服务器具有安全控制和认证功能。华盛顿 `IMAP`、`Courier-IMAP` 和 `Cyrus IMAP` 服务器都支持如前述 `POP` 服务器那样的 `SSL`。华盛顿大学 `IMAP` 守护进程的名为 `imapd`。在 `Red Hat` 上，`/etc/xinetd.d` 目录下有一个名为 `imap` 的文件。你使用 `chkconfig` 命令将其开启或关闭。

# 第 25 章节：打印服务器

## 概述

尽管在大多数 `Linux` 发行版中打印机的安装几乎是自动的，但理解其底层原理是有帮助的。打印机曾被视为直接连接到系统的设备，而现在被视为由打印服务器管理的网络资源。对于直接连接到系统的单个打印机，其网络功能是透明的，打印机看起来就像是又一个设备。另一方面，你可以轻松地利用打印服务器的网络能力，让多个系统使用同一台打印机。你可以在 `www.linuxprinting.org` 找到更多关于 `Linux` 打印的信息。

## CUPS 和 LPRng

目前，`Red Hat Linux` 上有两种可用的打印服务器：行式打印机、下一代版本 (`LPRng`) 和通用 `Unix` 打印系统 (`CUPS`)。`LPRng` 曾是 `Linux` 和 `Unix` 系统的传统打印服务器，但后来已从 `Red Hat` 发行版中移除。此处对其进行简要描述。从 `Red Hat 9` 开始，`CUPS` 现在已成为 `Red Hat Linux` 的主要打印服务器，并由 `redhat-config-printer` 支持。然而，在 `Red Hat 8.0` 及之前的版本中，`LPRng` 仍被用作默认服务器，且 `redhat-config-printer` 支持它。一旦你安装了打印机并配置了打印服务器，就可以使用打印客户端打印并管理你的打印队列。`CUPS` 服务器有多种打印客户端可用，包括 `redhat-config-printer`、`GNOME` 打印管理器、`CUPS` 配置工具以及各种如 `lpq` 和 `lpc` 等行式打印工具，将在本章稍后部分详细介绍。`CUPS` 配置工具是一个基于 `Web` 的配置工具，还可以管理打印机和打印作业（打开浏览器并输入 `URL` `http://localhost:631`）。将显示一个网页，包含管理作业、管理打印机和管理任务的条目。选择“Manage Jobs”（管理作业）条目可以删除或重新排序你提交的任务。`LPRng` 服务器也有多种打印客户端可用，包括 `lpq` 以及各种如 `lpq` 和 `lpc` 等行式打印工具，它们的工作方式与 `CUPS` 的对应工具类似。

## 打印机设备与配置

在使用任何打印机之前，你必须先在网络中的某个 `Linux` 系统上安装它。本地打印机直接安装在你自己的系统上。这涉及在配置文件中为打印机创建一个条目，定义它的打印机类型，以及如设备文件和池化目录等功能。在 `CUPS` 上，打印机配置文件是 `etc/cups/printers.conf`。安装打印机非常简单：确定打印机使用哪个设备文件，在 `Red Hat` 上，你可以使用 `redhat-config` 配置工具来设置和配置你的打印机。根据你使用的界面，`redhat-config-printer` 会调用 `redhat-config-printer-gui`（一个 `GUI GNOME` 打印机配置工具）或 `redhat-config-printer-tui`（具有屏幕光标驱动界面的相同工具）。

> 提示
> 如果你找不到打印机的驱动程序，可能从 `www.linuxprinting.org` 下载。该网站维护了大量的驱动列表。

## 打印机设备文件

`Linux` 创建了三个设备文件：`lp0`、`lp1` 和 `lp2`。这些用于并行打印机。对于串口打印机，它使用 `ttyS0`、`ttyS1` 和 `ttyS2`。

## 池化目录

当你使用打印机时，它会使用称为池化目录（`spool directories`）的特殊目录。对于 `CUPS`，池化目录位于 `/var/spool/cups`。该目录包含用于管理作业和打印机文件。

## 使用 CUPS 管理打印机

通用 `Unix` 打印系统 (`CUPS`) 是提供打印服务的 `LPrng` 的替代方案。它在 `GNU` 许可证下免费提供。虽然它现在包含在大多数发行版中，但你也可以从 `cups.org` 下载最新的源码版本。该网站还提供了有关安装和管理打印机的文档。`LPrng` 源自伯克利守护进程 (`lpd`)，而 `CUPS` 基于互联网打印协议 (`IPP`)。互联网打印协议旨在为互联网建立一个标准（更多信息请参见 `www.pwg.org/ipp/`）。虽然基于 `LP` 的打印系统主要关注打印机，但基于 `IPP` 的系统则提供了网络、`PostScript` 和 `Web` 服务器。`CUPS` 的工作方式类似于互联网服务器，其配置设置非常类似于 `Apache Web` 服务器。

对于 `Red Hat` 使用的 `RPM` 版本，`/etc/rc.d/init.d` 目录下安装了 `cups` 启动脚本。你可以使用 `service` 命令和 `cups` 脚本来启动、停止和重启 `CUPS`。当你进行更改或安装打印机时，需要重启 `CUPS` 以使更改生效。在 `Red Hat` 上，可以使用以下命令：

```
service cups restart
```

## 使用 CUPS 安装打印机

使用 `CUPS` 配置和安装打印机最简单的方法是使用前面的章节介绍的 `redhat-config-printer`。你也可以使用 `CUPS` 配置工具，这是一个基于浏览器的配置工具。为了确保浏览器访问，请确保先在打印系统切换器中选择 `CUPS`，或者如果你使用 `xnetd` 用于 `CUPS`，则使用 `chkconfig cups` 命令开启。

在 `Red Hat` 上启动界面的方法是在浏览器中输入以下 `URL`：
`http://localhost:631`

这将打开一个管理界面，你可以在其中管理和添加打印机。你首先会被要求输入管理员用户名（通常为 `root`）和密码（通常为 `root` 密码）。

你通过一系列 `Web` 页面在 `CUPS` 中安装打印机，每个页面请求不同的信息。要安装打印机，点击“Add Printer”（添加打印机）按钮将显示一个输入打印机名称和位置的页面（见图 25-1）。位置是打印机连接的主机。

图 25-1: `CUPS` 添加打印机

后续页面将提示你输入打印机型号和驱动程序，你可以从可用列表中进行选择。一旦添加了打印机，就可以对其进行配置。在“管理”（Administration）页面点击“管理打印机”（Manage Printers）项将列出你已安装的打印机。然后你可以点击某个打印机，显示一个告诉你如何配置打印机的页面。你可以配置其打印设置、修改其安装，甚至删除该打印机。点击“配置打印机”（Configure Printer）按钮将显示一个页面，你可以通过指定分辨率或纸张大小来配置打印机的打印方式。

打印机的配置信息将存储在 `/etc/cups/printers.conf` 文件中。你可以直接检查此文件并进行修改。这里有一个打印机配置项的示例。注意，它是使用 `redhat-config-printer` 创建的。它目前处于空闲（Idle）状态，队列中为空。

```
<DefaultPrinter meyperson
Info Created by redhat-config-printer 0.6.x
DeviceURI parallel:/dev/lp0
Location:
State Idle
Accepting Yes
JobSheets none none
QuotaLimit 0
PageLimit 0
Klimit 0
</Printer>
```

`DeviceURI` 项指定了使用的设备，在本例中为 `lp0` 并设备。对于远程打印机，此项将包含一个 `Internet` 地址及其协议。例如，`CUPS` 服务器 (`ipp`) 上的远程打印机将如所示所示（`Windows` 打印机使用 `samb` 协议）：

```
DeviceURI ipp://mysuff.com/printers/queue
```

你可以使用 `lpadmin` 命令从命令行执行所有管理任务。更多详细信息请参阅 `CUPS` 文档。

注意

# 在 CUPS 上配置远程打印机

要安装连接到 `Windows` 系统或运行 `CUPS` 的其他 `Linux` 系统的远程打印机，你需要使用特殊的 `URL` 协议来指定其位置。对于 `Windows` 打印机，你首先需要安装、配置并运行 `Samba`。`CUPS` 使用 `Samba` 访问 `Windows` 打印机。当你在 `CUPS` 上安装 `Windows` 打印机时，你指定的其位置是使用未注册版本的 `CHM2PDF Pilot` 创建的。允许登录打印机的用户输入主机名，并用 `@` 符号与其隔开。在大多数配置中，这是访客用户（`guest`）。连接名为 `lizard` 的 `Windows` 主机的名为 `myhp` 的 `Windows` 打印机位置为。其共享引用为 `/lizard/myhp`。

`smb://guest@myhp`

要在 `Samba` 上启用 `PS`，你必须将 `/etc/samba/smb.conf` 文件中的打印选项设置为 `cups`，如下所示：
`printing = cups`
`printcap name = cups`

要让 `cups` 与 `Samba` 工作，你必须将 `smbpool` 链接到 `CUPS` 的 `smb` 目录：
`ln -s /usr/bin/smbpool /usr/cups/backend/smb`

要使用 `LPRng` 访问连接到 `Linux` 或 `Unix` 系统，使用 `lpd` 协议指定其位置。在以下示例中，打印机 `mylaser` 连接到 `Linux` 主机 `rabbit.mytrek.com`：
`lpd:rabbit.mytrek.com/mylaser`

# CUPS 打印机类

`CUPS` 提供了一种方法为作业选择一组打印机，而不是只选择一个。这样，如果其中一台打印机忙或宕机，就可以自动选择另一台打印机来执行作业。这种打印机分组被称为类（`classes`）。一旦安装了打印机，你可以将它们分成不同的类。例如，你可能将所有喷墨打印机分为一类，将激光打印机分入另一类，或者你可能想将连接到特定服务器的打印机分到自己的类。要创建一个类，在“管理”（Administration）页面选择“类”（Classes）并输入类的名称。然后你可以为其添加打印机。

# CUPS 配置

`CUPS` 配置文件放置在 `/etc/cups` 目录下。这些文件如表 25-1 所示。`classes.conf`、`printers.conf` 和 `client.conf` 可以通过 `Web` 界面进行管理。`printers.conf` 包含了你安装的不同打印机的配置信息。如果你愿意，可以手动编辑这些文件的任何一个。

# cupsd.conf

`CUPS` 服务器通过位于 `/etc/cups` 的 `cupsd.conf` 文件配置。你必须手动编辑配置选项；服务器无法通过 `Web` 界面进行配置。你安装 `CUPS` 时会为每个选项安装一个带有注释的 `cupsd.conf` 文件，大多数选项都会被注释掉。被注释的行以 `#` 符号开头。每个选项都有详细的说明。服务器配置使用 `Apache Web` 语法，由一组指令组成。像 `Apache` 一样，这些指令中的若干条可以组合其他的指令块。

表 25-1: `CUPS` 配置文件

| 文件名 | 描述 |
| --- | --- |
| `classes.conf` | 不同本地打印机类的配置 |
| `client.conf` | 为指定客户端列出特定选项 |
| `cupsd.conf` | 配置 `CUPS` 服务器 `cupsd` |
| `printers.conf` | 可用本地打印机的打印机配置 |

# CUPS 指令

某些指令允许你对特定位置设置访问控制。这些可以是打印机或资源，例如管理工具或溢空打印目录。位置控制通过 `Location` 指令实现。`Allow From` 和 `Deny From` 指令允许或拒绝来自特定主机的访问。`CUPS` 支持基本（Basic）和摘要（Digest）形式的认证，在 `AuthType` 指令中指定。认证使用用户名和密码。例如，要使用 `Web` 界面，系统会提示输入 `root` 用户和 `root` 密码。摘要认证使用 `MD5` 版本保存在 `CUPS` 中的用户名和密码信息。位置使用未注册版本的 `CHM2PDF Pilot` 创建... [后文继续] 每个选项都有详细的说明。服务器配置使用 `Apache Web` 语法，由一组指令组成。像 `Apache` 一样，这些指令中的若干条可以组合其他的指令块。

当作业被放入队列时，你可以使用任何命令行客户端来管理它。这些客户端包括 `lpr`、`lpc`、`lpq` 和 `lprm`（表 25-2）。通过这些客户端，你可以检查打印机状态、重新排序、删除打印作业。

# lpr

`lpr` 客户端提交作业，然后 `lpd` 获取并将其放入队列。如果没有指定打印机，则使用默认打印机。`-P` 选项允许你指定特定的打印机。在下一个示例中，用户首先打印文件，然后向名为 `myepson` 的打印机打印报告：

```
$ lpr preface
$ lpr -P myepson report
```
