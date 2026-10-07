
双击文件夹查看该文件夹的内容。此时，你可能会收到输入密码的请求。输入密码并确定。现在你可以查看该文件夹及其子文件夹的内容。

> **提示：** 如果你计划经常使用该目录，可能想为其分配一个驱动器号。右键点击文件夹图标，选择“映射网络驱动器”。从列表中选择一个驱动器，如果需要，勾选“登录时重新连接”以便在登录时可用。然后点击确定。

你正在寻找的文件服务器没有出现在你的“网络邻域”中，你可以搜索它：选择开始 -> 查找 -> 计算机。输入要搜索的计算机名称，然后选择“现在”。如果出现了计算机名称，双击它。应该会打开一个窗口，显示来自服务器的共享目录和打印机。

或者，你可以创建一个 hosts 文件来帮助你的 Windows 95 计算机找到你的 Linux Samba 服务器。将示例文件 `C:\windows\hosts.sam` 复制到 `C:\windows\hosts`。然后编辑该文件，添加网络服务器的主机名和 IP 地址。

## 排除你的 Samba 服务器

Samba 服务器可能会出现很多问题。如果你的 Samba 服务器无法正常工作，本节中的描述应该帮助你定位问题。

### 基础网络已就绪？

在计算机能够通过 Samba 共享目录和打印机之前，它们必须能够在你的局域网（LAN）上通信。有关设置 LAN 的信息，请参考第 15 章。

在 Samba 中，你的 Samba 服务器可以使用 TCP/IP 名称作为 NetBIOS 名称（Windows 网络用于文件和打印机共享），也可以在 `smb.conf` 文件中设置独立的 NetBIOS 名称。至关重要的是，广播地址必须与与你 Samba 服务器通信的所有客户端相同。要查看你的广播地址，请输入以下命令（使用 root 用户）：

```bash
# ifconfig -a
eth0 Link encap:Ethernet Hwadd:00:D1:B3:75:A5:1B
inet addr:10.0.0.1 Bcast:10.0.0.255 Mask:255.255.255
```

重要信息是广播地址（`Bcast:10.0.0.255`）。这由子网掩码（`Mask:255.255.255`）决定。如果 Samba 服务器和 LAN 客户端的广播地址不同，客户端将无法看到 Samba 服务器有共享目录或打印机。

### Samba 服务正在运行？

首先，尝试从你的 Linux 系统使用 `smbclient` 命令检查一切是否运行正常并按你的预期共享。`smbclient` 命令是获取 Samba 服务器信息的绝工具，甚至可以从 Linux 和 Windows 计算机访问共享目录。以 root 或任何拥有你 Samba 服务器权限的用户登录时，输入以下内容：

```bash
$ smbclient -L localhost
Password: ********
Domain=[ESTREET] OS=[Unix] Server=[Samba 3.0.3-4]
```

## 第 18 章：设置文件服务器

| 共享名 | 类型 | 注释 |
| --- | --- | --- |
| homes | 磁盘 | 目录 |
| IPC$ | IPC | IPC 服务 (Samba 服务器) |
| ADMIN$ | 磁盘 | IPC 服务 (Samba 服务器) |
| hp-nsl | 打印机 |  |
| Domain=[ESTREET] | OS=+Windows | Server=[Samba 3.0.3-4] |
| PINE | | Samba 服务器 |
| MAPLE | | Windows XP |
| NS1 | | Samba 服务器 |
| Workgroup | Master |  |
| ESTREET | | PINE |

这显示 Samba 服务器正在运行在本地计算机上。共享目录、打印机以及工作组中的服务器都会显示在这里。如果 Samba 服务器没有运行，你将看到“拒绝连接”的消息。你需要按照前文“Samba 服务”中描述的方法启动 Samba 服务。

### 防火墙已开启？

如果 Samba 服务器正在运行，它应该开始在你的 LAN 上广播其可用性。如果你尝试从 LAN 上的 Windows 或 Linux 客户端访问服务器但得到“拒绝连接”错误，问题可能是 Samba 服务器上的防火墙拒绝了对 NetBIOS 服务的访问。如果你有一个安全的 LAN，可以输入以下命令（使用 root 用户）刷新防火墙：

```bash
# iptables
```

然后，尝试从 Windows 或 Linux 客户端连接到 Samba 服务器。如果你发现无法连接到服务器，请重新开启防火墙：

```bash
# service iptables restart
```

你仍然需要在防火墙中开启端口 137、138 和 139，以便 Samba 服务器能够能够接受连接（有关修改防火墙的信息，请参见第 14 章）。

### 用户密码是否有效？

尝试作为特定用户（从 LAN 上的主机或其他 Linux 系统）访问共享目录。你可以使用 `smbclient` 命令执行此操作。这里有一个示例：

```bash
# smbclient //localhost/shared -U chris
Password: ********
Domain=[ESTREET] OS=[Unix] Server=[Samba 2.2.7]
```

在此示例中，`smbclient` 连接到名为 `shared` 的目录。如果密码通过，你将看到有关服务器的信息和 smb 提示符。如果你无法从 Windows 客户端访问同一个共享目录，可能是客户端传递了不正确的用户名密码。对于某些 Windows 客户端，你可能需要更改 Windows 注册表。更改注册表的一种方法是使用 `regedit` 命令。不同 Windows 系统的注册表更改包含在 `/usr/share/doc/samba-*/` 目录下。

提示：在此处用于列出服务器信息的 `smbclient` 命令也可以连接后浏览共享目录并复制文件。在看到 smb 提示符后，输入 `help` 查看可用命令。该接口与任何客户端（如 ftp）类似。

## 在 Linux 中设置 NetWare 服务器

NetWare（来自 Novell, Inc.）曾是 LAN 中通过 PC 共享文件和打印机最流行的软件。NetWare 被称为网络操作系统。虽然 NetWare 不像客户端操作系统（如 Windows 2000 或 XP）那样可以放在办公桌上进行处理工作，但它是一个非常高效的文件和打印服务器。

Linux 提供了提供了从你的 Linux 系统模拟 NetWare 服务器的软件。与 Fedora Linux 一起使用的包是 NetWare 模拟器（nw 包）。虽然该包不再随 Fedora 分发，但你仍然可以各种 RPM 仓库获取 nw 包。

- 文件服务 — 你可以使用 NetWare 模拟器从 Linux 共享目录结构（称为卷）。
- 打印服务 — 你可以使用 NetWare 模拟器共享与 NetWare 服务关联打印机。
- RIP/SAP 守护进程 — 该守护进程允许你的 Linux 计算机作为 IPX 路由器。（IPX 是与 NetWare 系统通信使用的原生协议。）

在客户端，如果你想让你的 Fedora 系统利用来自 NetWare 服务器的服务，你需要安装一个额外的包 `ncpfs`（它在光盘 #3 上）。该包提供了一系列完整的客户端命令用于访问 NetWare 服务。这些命令允许你挂载卷、显示服务信息以及处理 NetWare 二进制对象。

### 创建 NetWare 文件服务器

要从你的 Linux 服务器共享 NetWare 服务，你需要使用 IPX 协议与 NetWare 客户端通信。常见情况是在以太网 LAN 上使用 IPX（本节所述）。

交叉引用：有关设置以太网 LAN 的信息，请参第 15 章。

大部分 Linux NetWare 服务器的配置在 `/etc/nwserv.conf` 文件中完成。随 nw 提供的 `nwserv.conf` 文件包含大量注释信息，描述了如何配置 NetWare 服务。有关在 Fedora Linux 中配置 NetWare 服务器的详细信息，请参考 `nwserv.conf` 文件中的注释文本。

### 配置 /etc/nwserv.conf

- 卷 (1) — 你想要共享的卷（Linux 目录）。
- 服务器名称 (2) — 服务器的标识。
- 内部网络号 (3) — 唯一标识服务器的数字。该地址必须是十六进制数，或包含单词 auto 以使用当前的 IP 地址作为网络号。
- IPX 设备 (4) —  IPX 网络的信息。包括网络号、接口设备（如 eth0）、帧类型（ethernet_i、802.2、802.3 或 SNAP）以及刻数（刻是确定数据包在特定接口上传输时间的增量）。如果你的 IP 网络已设置，则不需要执行此。
- 密码处理 (7) — 定义是否以及如何加密客户端密码。默认值为 0，强制加密所有客户端密码。
- 最小 UID/GID 权限 (10) — 为从 Linux 服务器共享的卷分配最小用户权限。默认情况下，分配 nobody 用户权限（UID=99）。同样默认情况下，分配 nobody 组权限（GID=99）。
- 管理员登录 (12) — 将 NetWare 管理员登录分配给你 Linux 系统上的特定登录。建议分配一个特殊的登录而不是使用 root（以限制安全影响）。默认情况下，管理员登录分配给 Linux 登录 (UID=0)。此条目是只读的，服务器首次运行时设置。该条目还应包含登录的初始密码。
- 用户登录 (13) — 将计算机上的普通 Linux 登录映射到 Linux NetWare 服务器登录。你也可以添加默认密码，尽管不是必须。
- 自动登录映射 (15) — 定义是否自动将你的 Linux 用户登录（`/etc/passwd` 中的用户）映射到你的 NetWare 服务器。对于常用的映射登录，将分配相同的密码。默认情况下，登录会从 `/etc/passwd` 重新读取并分配密码 `top-secret`（顶级）。
- 启动测试 (16) — 在启动时运行检查，此值设置为 1（默认值）。

你可以通过阅读 `/etc/nwserver.conf` 文件中的描述，找到关于其他用于设置打印、调试和计时的值的信息。以下是我设置的用于从 Linux 系统共享 NetWare 卷的值示例。其中某些值是 `/nwserver.conf` 文件中设置的默认值（条目分布在 `/etc/nwserver.conf` 文件中）。

| 索引 | 类型 | 路径 | 选项 | 权限 | 模式 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | SYS | /var/mars_nwe/sys | rk | 711 | 600 |
| 2 | CDROM | /mnt/cdrom | kr | auto | 1 |
| 3 | maple1 | | | | |
| 4 | 0x0 | eth0 | 802.3 | 1 | |
| 7 | | | | 1 | |
| 9 | | | | 99 | |
| 11 | | | | 99 | |
| 12 | SUPERVISOR | root | | secret | |
| 15 | | | | 99 | top-secret |

在此示例中，共享了 SYS (`/var/mars_nwe/sys` 目录）和 CDROM (`/mnt/cdrom`) 卷。服务器名称分配为 `maple1`。地址从本地计算机的 IP 地址自动选择 (`auto`)。通过 `0x0`，Linux 内核可以为你选择一个网络号。网络接口是 `eth0`（计算机上的第一个以太网网络），使用的帧类型为 `802.3`。UID 99 (用户 nobody) 被分配了最小的用户和组权限。SUPERVISOR 权限分配给 root 用户（初始密码为 `secret`）。UID 99 的密码为 `top-secret`。

### 启动 NetWare 守护进程

此时，你只需要启动你的 NetWare 服务器进程即可。你可以通过输入 `nwserver` 来实现。你的另一种选择（长期来看更好）是从系统初始化脚本启动服务器。`mars-nwe` 软件包提供了这样一个脚本，但它可能没有配置为在系统上自动启动。要设置脚本自动启动 NetWare 服务器进程，请输入以下内容：

```
# ckconfig mars-nwe on
```

## 第 18 章：设置文件服务器

此命令集设置 `mars-nwe` 在运行级别 3、4 和 5 启动。下一次你重启 Linux 系统时，`nwserv` 守护进程将提供你的 NetWare 服务。或者，你也可以输入以下命令立即启动服务：

```
# service mars-nwe start
```

### 使用 NetWare 客户端

`ncofs` 软件包包含一组与 NetWare 文件和打印服务工作的工具。以下是这些命令中的几个：

- **nsend** — 向用户的工作站发送消息。`nsend` 命令在主目录下的 `.nwclient` 文件中查找有关文件服务器、用户名以及可选密码的信息。例如，要向系统管理员发送消息，你可以输入 `nsend supervisor 'Hello, how is your day?'`。
- **nwauth** — 验证到 NetWare 服务器。你可以指定要验证的服务器 (`-S servername`)。否则，`nwauth` 将在你的 `$HOME/.nwclient` 文件中查找该信息。如果你在 shell 中运行此命令，服务器将提示你输入密码。
- **nbols** — 列出你指定的 NetWare bindery 对象。
- **nwbrops** — 列出与指定的 NetWare bindery 对象相关的属性。
- **nwpset** — 设置 NetWare bindery 属性值或创建 bindery 属性。
- **nwfinsfo** — 显示文件服务器的信息，无需登录服务器。
- **nwpasswd** — 在 NetWare 服务器上更改你的密码。
- **nwpurge** — 清理一个之前删除的文件目录。
- **nwrights** — 显示与特定文件或目录相关的 NetWare 权限。
- **nwfsind** — 搜索 NetWare 服务器并显示通往服务器的路由（网络地址）。
- **nwtrustee** — 显示与 NetWare 服务器相关的 trustee 目录分配列表。
- **nwuserlist** — 显示当前登录 NetWare 服务器的用户列表。
- **nwvolinfo** — 显示 NetWare 服务器卷的信息。
- **slist** — 显示所有可用 NetWare 服务器的列表。
- **ncpmount** — 从 NetWare 文件服务器挂载卷。
- **ncpmount** — 从 NetWare 文件服务器卸载卷（此处重复）。
- **nwbocreate** — 为 NetWare 文件服务器创建 bindery 对象。
- **nwbornorm** — 为 NetWare 文件服务器删除 bindery 对象。
- **nwfsctl** — 在 NetWare 文件服务器上运行命令。
- **nwgrant** — 向服务器添加 bindery 对象及其相关的 trustee 权限。
- **nwmsg** — 发送消息。
- **nwrevoke** — 撤销 NetWare 权限。

此命令集设置 `mars-nwe` 在运行级别 3、4 和 5 启动。下一次你重启 Linux 系统时，`nwserv` 守护进程将提供你的 NetWare 服务。或者，你也可以通过输入以下命令立即启动服务：

（此处省略了重复的乱码部分...）

## 第 19 章：设置邮件服务器

**本章内容**

- 介绍 SMTP 和 Sendmail
- 安装和运行 Sendmail
- 配置 sendmail
- 介绍 Postfix
- 使用 SpamAssassin 阻止垃圾邮件
- 从服务器获取邮件 (IMAP 和 POP3)
- 配置 SquirrelMail
- 管理 mailman 邮件列表

今天，电子消息传递是通信骨干的一部分，是各种规模公司信息传播的核心。从邮件室到实验室到 CEO办公室，每个人都在使用电子邮件。如果你负责组织的邮件服务器，当它停止工作时，你会收到通知。

本章解释了如何在 Fedora 中设置邮件服务器以发送和接收消息。特别是，它重点于配置邮件服务器，同时也介绍了如何配置 Postfix 邮件服务器（它也在 Fedora 发行版中）。一旦配置好邮件服务器，Fedora 为你的邮件服务器用户提供了从服务器获取电子邮件的不同方法，例如下载到邮件客户端（使用 IMAP 或 POP3）或通过 Web 浏览器读取（使用 SquirrelMail）。

本章还讨论了邮件列表的配置和管理（使用 mailman 软件包），详细介绍了 mailman 邮件列表软件如何与邮件服务器集成和交互。

> 注意：尽管本章讨论了邮件服务器配置的主要方面，但许多配置方面超出了其范围，因此未予以讨论。由于在连接到互联网时安全性是一个重要问题，因此我们在此给予了大量的关注。

### 介绍 SMTP

即使今天的电子邮件中已经包含了多媒体附件和 HTML 编码，但邮件传输背后的技术自 20 世纪 80 年初并没有并没有变化。简单邮件传输协议 (SMTP) 框架最初在 1982 年的 RFC 821 中引入。协议本身在 1993 年进行了扩展 (RFC 1425)，产生了扩展邮件传输协议 (ESMTP)，它提供了更多的命令和新的投递模式。
