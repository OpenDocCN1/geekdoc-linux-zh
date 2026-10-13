
为了让主机使用您网络上的 NIS，首先需要指定该主机上的 NIS 域名。此外，您的 NIS 客户端需要知道您的 NIS 服务器的名称。如果您安装 Linux 时网络已经在运行 NIS，您可能在安装过程中已经输入了此信息。

### 指定 NIS 域和服务器

在 Red Hat 上，您可以使用 `authconfig-gtk` 工具指定 NIS 域名和服务器，您可以从系统设置窗口访问该工具。在该窗口中，选择 Authentication。这将打开 Authentication Configuration 窗口。在 User Information 面板上，点击 Configure NIS 按钮打开一个对话框，您可以在其中输入 NIS 域名称以及 NIS 服务器。请务必也在 User Information 面板上启用 NIS。NIS 域将保存在 `/etc/sysconfig/network` 文件中，NIS 服务器则保存在 `/etc/yp.conf` 文件中。

### 访问服务器

每个 NIS 客户端主机然后在您的网络上必须运行 `ypbind` NIS 客户端以访问服务器。在客户端的 `/etc/yp.conf` 文件中，您需要指定它将使用的 NIS 服务器。以下条目将引用位于 `192.168.1.1` 的 NIS 服务器：

```
ypserver 192.168.1.1
```

或者，您可以指定 NIS 域名及其使用的服务器：

```
domain mydomain.nis server servername
```

`authconfig-gtk` 工具将在 `/etc/yp.conf` 中为使用 `turtle.mytrek.com` 服务器的 `myturtles.nis` NIS 域创建以下条目：

```
domain myturtles.nis server turtle.mytrek.com
```

要启动 NIS 客户端，请运行 `ypbind` 脚本：

```
service ypbind start
```

然后，为了检查一切正常，您可以使用 `ypcat` 尝试列出 NIS 密码文件：

```
ypcat passwd
```

您可以使用 `ypcat` 列出任何 NIS 配置文件。`ypwhich` 命令将显示您的客户端正在使用的 NIS 服务器名称。`ypmatch` 可用于在配置文件中查找特定条目。

```
ypmatch cecelia passwd
```

用户可以使用 `yppasswd` 命令更改 NIS `passwd` 文件中的密码。其工作方式与 `passwd` 命令相同。您还必须运行 `yppasswd` 守护进程。

### 使用 nsswitch.conf 指定配置文件

为了确保客户端访问特定配置文件的 NIS 服务器，您应在 `/etc/nsswitch.conf` 文件中指定该文件的 `nis` 条目。`nisplus` 选项指的是 Red Hat 当前使用的 NIS 版本 3。`nis` 选项用于指代较旧的 NIS 版本 2。`/etc/nsswitch.conf` 文件指定主机应查找某些类型信息的位置。例如，以下条目说明首先检查本地配置文件（`files`），然后从 NIS 服务器（`nisplus`）查找密码数据：

```
passwd: files nisplus
```

`files` 指定先使用系统自身的文件，即本地主机上的文件。`nis` 指定在 NIS 文件中查找条目，访问 NIS 服务器。`nisplus` 指定使用由 NIS+ 服务器维护的 NIS+ 文件。`dns` 指定执行 DNS 查找；它只能用于包含主机名的文件，如 `hosts`。以下是一些标准条目：

```
passwd:      files nisplus
shadow:      files nisplus
group:       files nisplus

hosts:       files nisplus dns
bootparams:  nisplus [NOTFOUND=return] files

ethers:      files
netmasks:    files
networks:    files
protocols:   files nisplus
rpc:         files
services:    files nisplus
netgroup:    files nisplus
publickey:   nisplus
automount:   files nisplus
aliases:     files nisplus
```

# 第 37 章：Samba

## 概述

通过 Samba，您可以将 Microsoft Windows 网络上的 Windows 客户端连接到由 Linux Samba 服务器控制的服务，如共享文件、系统和打印机，同时允许 Linux 系统访问 Windows 系统上的共享文件和打印机。Samba 是一组 Linux 工具，允许您通过 Windows 网络与 Windows 系统进行通信。实际上，Samba 使 Linux 系统或网络表现得像一个 Windows 服务器，使用与 Windows 网络相同的协议。虽然大多数 Unix 和 Linux 系统使用 TCP/IP 协议进行网络通信，但 Microsoft 的 Windows 网络使用一种不同的协议，称为服务器消息块（SMB）协议，该协议实现了运行 Windows 的个人电脑局域网（LAN）。SMB 使用一种称为网络基本输入输出系统（NetBIOS）的网络接口，允许 Windows 个人电脑共享资源，如打印机和磁盘空间。在这样的网络中，一台 Windows 个人电脑可以访问另一台 Windows 个人电脑磁盘驱动器的部分，就像它是自己的磁盘一样。SMB 最初是为小型局域网设计的。为了将其连接到更大的网络，包括那些有 Unix 系统的网络，Microsoft 开发了通用互联网文件系统（CIFS）。CIFS 仍然使用 SMB 和 NetBIOS 进行 Windows 网络通信。Andrew Tridgell 希望将他的 Linux 系统连接到 Windows 个人电脑，因此他编写了一个他称为 Samba 的 SMB 客户端和服务器。Samba 允许 Unix 和 Linux 系统连接到这样的 Windows 网络，就像它们是 Windows 个人电脑一样。Unix 系统可以共享 Windows 系统上的资源，就像它们是另一台 Windows 个人电脑一样。Windows 个人电脑也可以访问 Unix 系统上的资源，就像它们是 Windows 系统一样。Samba 实际上已经成为一个专业级别、开源且免费的 CIFS 版本。它也比 CIFS 运行得快得多。Samba 有效地使您能够使用 Linux 或 Unix 服务器作为运行在 Windows 网络上一组 Windows 机器的网络服务器。您还可以使用它在 Linux 系统上与其他 Windows 个人电脑共享文件，或者从 Linux 系统访问 Windows 个人电脑上的文件，以及 Windows 个人电脑之间也是如此。在 Linux 系统上，`smbfs` 文件系统使您能够实际上在您的文件系统中挂载远程 SMB 共享目录。然后您可以像访问本地系统上的目录一样访问它。

## Samba 文档

您可以从位于 [www.samba.org](http://www.samba.org) 和 [ftp.samba.org](http://ftp.samba.org) 的 Samba 网站和 FTP 站点获取广泛的文档和当前版本。Red Hat 的 RPM 软件包可从 Red Hat 及 RPM 存储库（参见第 1 章）获取。大多数 Linux 发行版也包含 Samba。还可以从 SMB 新闻组 `comp.protocols.smb` 获取其他信息。软件包附带了广泛的文档，并安装在您的系统中，通常位于带有 Samba 版本名称的子目录下，路径为 `/usr/share/doc` 目录。在这里，您可以找到广泛的 HTML 和文本格式文档，以及众多示例和当前的常见问题解答（FAQ）。Samba HOW-TO 文档也可在 [www.tldp.org](http://www.tldp.org) 上获取。示例包括针对不同配置类型的 `smb.conf` 文件示例。SWAT 配置工具的首页还提供基于 Web 页面的 Samba 文档，以及针对不同功能特性的上下文帮助。

## Samba 应用程序
