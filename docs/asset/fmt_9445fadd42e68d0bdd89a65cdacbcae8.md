
网关地址是连接到另一个网络（如 Internet）的计算机的 IP 地址。在典型的局域网中，只有 一台计算机直接连接到另一个网络。该计算机通常有两个网卡：一个连接到局域网，另一个连接到其他网络。每个网卡分配一个 IP 地址。网关地址是局域网上网卡的 IP 地址。

请看图 12.1，它显示了一个由五台计算机组成的局域网。图中位于集线器和 Internet 之间的计算机是网关计算机。此局域网上所有其他计算机的网关地址是 192.168.1.3，这是网关计算机在局域网上使用的地址。

![](img/7a908c965299f9cdfda2a4ea3cd98bf4_254_0.png)

图 12.1 具有网关的典型局域网。

IP 地址 192.168.2.208

网络掩码 255.255.255.0

广播 192.168.2.255

默认路由器 192.168.2.254

![](img/7a908c965299f9cdfda2a4ea3cd98bf4_255_0.png)

> 网关 IP 地址与分配在网络上的其他地址处于同一主机 IP 地址范围。

## 访问控制

在网关计算机上，有多种限制访问的方法。你可以在两个方向设置限制：防止不受欢迎的用户进入，以及防止网络上的用户访问其他网络，如 Internet。你可以通过 IP 地址或计算机名称在 `/etc/hosts.allow` 和 `/etc/hosts.deny` 文件中控制访问。至少，你希望拒绝访问其他私有 IP 地址以及你不希望外界使用的任何服务，例如电子邮件或内部网站。

> 注意：控制进出网络的主要方式是通过防火墙实用程序，例如 `iptables` 或 `ipchains`。

## 其他网络服务

当你安装 Linux 时，可能需要配置 DNS 服务器、DHCP 服务器、NFS 和 Samba 连接。

在 Linux 上可以设置的网络服务中包括 `sendmail` 和 `Apache`。`Sendmail` 让你在 Linux 计算机上设置邮件服务器。`Apache` 让你在 Linux 计算机上设置 Web 服务器。虽然你不需要详细了解这些服务，但了解一些基础知识是有帮助的。

## 域名系统 (DNS)

DNS 服务器将类似 `www.mommabears.com` 的名称翻译为类似 `199.93.70.2` 的 IP 地址。如果你为任何计算机设置 Internet 访问，你需要访问 DNS 服务器。当你为 Linux 配置 Internet 或其他网络访问时，你需要一些 DNS 服务器的 IP 地址。如果你通过 ISP 访问 Internet，请向 ISP 询问其 DNS 服务器的 IP 地址。

Linux 在 `/etc/resolv.conf` 文件中查找 DNS 服务器 IP 地址。如果你的 ISP 告诉你应使用的 DNS 服务器是 24.1.80.33，请将以下行添加到该文件：

```
nameserver 24.1.80.33
```

使用类似以下示例的列表，在 `/etc/hosts` 文件中建立主机名和 IP 地址的数据库：

```
192.168.16.1    linux1.mommabears.com    linux1
192.168.16.2    windows1.mommabears.com    windows1
192.168.16.3    laptop1.mommabears.com    laptop1
192.168.16.4    linux2.mommabears.com    linux2
192.168.16.5    examcram.mommabears.com    examcram
```

正如你所见，此示例列出了每个 IP 地址关联的主机名和完全限定域名。缺点是你需要在网络中的每台计算机上都有此文件的相同副本。如果你网络中有大量计算机，这可能会难以维护。在这种情况下，设置自己的 DNS 服务器可能更容易。

## 动态主机配置协议 (DHCP)

计算机从 DHCP 服务器“租用” IP 地址一段时间。如果在租用的 IP 地址到期时计算机仍处于活动状态，它可以续租一段时间。当来自非活动计算机的租约到期时，DHCP 服务器可以将该地址重新分配给另一台计算机。

你可能想要使用 DHCP 有两个原因。如果你没有足够的 IP 地址供网络使用，DHCP 可以帮助管理可用地址。如果你网络中有大量计算机，DHCP 可以帮助你避免为每台计算机分配 IP 地址的麻烦。DHCP 需要一个名为 `dhcpd` 的服务器守护进程。你可以在网络上的任何 Linux 计算机上设置此守护进程。

如前所述，当你连接到 Internet 时，你需要一个公共 IP 地址。分配给 ISP 的 IP 地址数量有限。ISP 使用 DHCP 在其成员之间分配 IP 地址。如果你 ISP 使用 DHCP 为你分配 IP 地址，你可以通过 `/etc/dhcpd.conf` 配置文件设置 Linux 从 ISP 的 DHCP 服务器接收此地址。

## 网络文件系统 (NFS)

一旦两台计算机建立连接，它们需要一种共同的语言来共享文件和打印机。NFS 是 Linux 计算机之间共享信息的主要语言。NFS 由网络文件系统守护进程 `nfsd` 运行。设置后，你可以像挂载本地软盘驱动器和 CD-ROM 驱动器一样轻松地挂载远程目录。

你选择共享的目录在 `/etc/exports` 配置文件中设置。准备就绪后，你可以设置 `/etc/fstab` 文件，以便每次启动 Linux 时挂载 NFS 目录。

## Samba

Microsoft Windows 计算机通过使用服务器消息块（SMB）的语言相互通信。Linux 通过 Samba 系统模拟这种语言。运行 Samba 需要两个守护进程：`smbd` 和 `nmbd`。`smb` 守护进程是通用语言；`nmb` 守护进程允许 Linux 识别和使用基于 Microsoft 的计算机名称。设置 Samba 后，你可以像浏览 Windows 网络邻居中的任何其他 Microsoft Windows 计算机一样浏览 Linux 计算机。并且你可以同样轻松地从 Linux 浏览 Microsoft Windows 系统。

目录和打印机的共享在 `/etc/samba/smb.conf` 或 `/etc/smb.conf` 配置文件中设置。你可以设置 Samba 在由 Windows NT/2000 服务器或工作站管理的 Microsoft Windows 域中共享，或设置 Samba 在与 Windows 95/98/ME 系统的工作组中共享。

## sendmail

当你为用户设置电子邮件时，你可以通过 ISP 分配地址，或设置自己的邮件服务器。如果你的用户有大量电子邮件，你可能希望设置自己的邮件服务器。根据发行版，`sendmail` 或 `smail` 是首选邮件服务器。你可以设置 `sendmail` 通过常见的接收协议传输消息，例如 `POP`（邮局协议）或 `IMAP`（Internet 消息访问协议）。你也可以设置 `sendmail` 通过其他邮件协议传输消息，例如 `SMTP`（简单邮件传输协议）。

*注意：使用 POP 的邮件服务器通常使用名为 `POP3` 的更新版本。同样，IMAP 的当前版本称为 `IMAP4`。*

`Sendmail` 被称为邮件传输代理。`Sendmail` 用户账户基于 `/var/spool/mail` 目录中的文件。

## Apache

Linux Web 服务器被称为 `Apache`。当你在 Linux 上设置 `Apache` 时，你安装 `http` 守护进程 `httpd`。你可以根据 `/etc/httpd/conf` 目录中的三个文件配置 `Apache`：

- `access.conf`—为浏览器设置目录。你在此文件中指定的目录将成为你的主页文件的家。
- `httpd.conf`—是主要的 Apache 配置文件。你可以通过此文件在一台计算机上设置多个网站（虚拟主机）。
- `srm.conf`—定义在完全限定域名之后出现的目录名称。

在某些发行版中，此配置信息合并在 `/etc/httpd/conf/access.conf` 文件中。你也可能在 `/etc/apache` 目录中找到这些配置文件。

## 网络应用程序

网络守护进程，例如 NFS 和 Samba，允许你与网络上的其他计算机共享文件和打印机。网络应用程序允许你使用其他服务，例如 `Apache` 和 `sendmail`。虽然你不能直接访问共享的网页，但你可以用名为 `Netscape Communicator` 的网络应用程序浏览它。虽然你不能直接访问邮件服务器的共享，但你可以用诸如 `Netscape Messenger` 之类的应用程序访问单个邮件。使用 `FTP`（文件传输协议），你可以在远程服务器上共享文件。使用 `Telnet`，你可以登录并管理远程 Linux 计算机。

## 网页浏览器

`Netscape` 和 `Internet Explorer` 并不是浏览互联网的唯一方式（Microsoft Internet Explorer 现在可以为 Linux 设置）。KDE 和 GNOME 包都有自己的浏览器。另一种流行的 Linux 替代方案是 `Opera` 浏览器。这些是图形浏览器。
