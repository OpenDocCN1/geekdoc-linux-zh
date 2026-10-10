
## 第 33 章：与 Microsoft Windows 共享文件和打印

NFS 是 Unix 机器之间文件共享的绝佳解决方案，它必须跨机器保留 Unix 权限和文件元数据（例如修改时间）。然而，NFS 在许多消费级操作系统中并未得到广泛支持。Windows 和经典 Mac OS 仅通过第三方应用程序支持它，而且在企业环境中，NFS 没有内置任何“发现”机制来允许客户端浏览可用服务器列表，这一点更为重要。

当你将 FreeBSD 机器放入现有网络中时，那里的大多数计算机很可能都在运行 Windows。与这些客户端以及现有 Windows 文件服务器进行真正的互操作，要求 FreeBSD 以与 Windows 相同的方式共享文件。这种方法涉及 SMB（*Server Message Block*，服务器消息块）协议，以及逐渐取代它的 *Common Internet File System*（CIFS，通用 Internet 文件系统）。

通过 SMB/CIFS 进行文件共享不是 FreeBSD 的内置功能。然而，一个名为 *Samba* 的附加软件包赋予了 FreeBSD 机器充当 Windows 文件服务器的能力，并使其能够参与与真正的 Windows 客户端相同的所有文件共享活动。

Samba 是一个开源的志愿者项目，最初由 Andrew Tridgell 发起，现在由通用 Unix 社区协作开发。它为 Unix 机器（如 FreeBSD）提供了执行 Windows 文件共享所能执行的所有功能的能力，包括出现在网络浏览列表中、基于 NT 域和用户名登录来保护连接，以及提供网络打印服务。Samba 还包含许多提供 Windows NT/2000 服务器管理功能的工具。通过添加 smbfs 内核模块，使 FreeBSD 能够作为 Windows 文件共享客户端运行（你将在本章后面了解更多关于 smbfs 的信息），你可以在 Windows 网络环境中使用 FreeBSD 机器，其功能性与本机 Windows 机器一样强大。

本章将指导你配置 Samba。在这里，你将学习如何为 FreeBSD 系统添加类似 Windows 的文件共享和打印机管理功能，包括集成到 Windows 工作组和域中，使得你的系统在网络上与本机 Windows PC 难以区分。

> **注意**
> Samba 的官方网站是 www.samba.org，你可以从中选择多个不同的地理镜像站点。

### 本章内容
- SMB/CIFS 和 Samba
- 安装和配置 Samba
- 其他 Samba 组件
- 未来的 Samba 开发
- 访问 Windows 系统上的共享文件（*smbfs* 文件系统）

### SMB/CIFS 和 Samba

SMB 可追溯至 IBM 在 1985 年发布的文档，后来由 Microsoft 和 Intel 进一步扩展，它是一种用于通过本地网络共享各种系统资源的通用系统。此类资源包括文件、打印机、串行端口以及命名管道等软件抽象。即使在表面上 Windows 文件共享看起来是点对点结构，它也是一个以客户端/服务器方式运行的协议。SMB 是许多操作系统的重要组成部分，包括 MS-DOS、Windows、OS/2 和 Linux——尽管如今 SMB 的主要用途是在 Windows 中，并由 Microsoft 推广。

SMB 和 CIFS 命令通过诸如 IPX、NetBEUI、Banyan VINES 和 DECnet 等网络协议发送。这些协议在堆栈的“网络”层运行，与 IP（如你在第 21 章“使用 FreeBSD 进行网络通信”中所见）处于同一层，因此不受限于 TCP/IP 传输。然而，SMB 最常用的传输协议是运行在 IP 上的 NetBIOS（Network Basic Input/Output System，网络基本输入/输出系统，描述在 RFC 1001 和 1002 中），它使用 TCP 和 UDP 组件运行。这是 Windows 文件使用中使用的协议。

#### 浏览

SMB 相对于 NFS 等协议的一个优势是，它支持自动服务器发现，或*浏览*。在 Windows 中，如果你打开“网络邻域”或“我的网络位置”窗口，它将显示本地网络上所有可用 SMB 服务器的名称。此列表是动态构建的，每台机器都会发送周期性的广播包以寻找网络的“主浏览器”（一台拥有本地和远程 SMB 主机确定性列表的计算机）并宣告其自身的存在。网络上的其他每台机器都根据这些广播构建其“浏览列表”。

每台机器在网络浏览器窗口中显示的名称（如图 33.1 所示）是其 *NetBIOS 名称*，这是 Windows 允许长达 15 个字符的指定。尽管 Windows 要求你输入大写的 NetBIOS 名称，但它在网络浏览器窗口中仅首字母大写显示。在其他操作系统（如 FreeBSD）下，NetBIOS 名称与机器的主机名相同，如有必要则截断为 15 个字符。

![](img/48eec858cce7dfb89da36a4d40b7daf3_812_0.png)

**图 33.1** Windows 网络浏览器窗口，显示一台运行 Samba 的 FreeBSD 机器。

NetBIOS 名称由一种名称服务处理，有点像 DNS 名称，但除了 IP 地址外，还基于其他标准将显示的 NetBIOS 机器名称映射到特定的机器（因为 NetBIOS 不受限于 IP）。Samba 的名称服务器组件与实际 SMB 数据服务器是分开的。

NetBIOS 的一个缺点是它仅在局域网（LAN）上运行；NetBIOS 数据包基于广播，因此不会被路由器转发。Windows Internet 名称服务（WINS）协议的存在是为了连接不同网络上的 Windows 共享区域，从而在一定程度上缓解此问题。

#### 安全、工作组和域

对 SMB 共享的访问在各个层级受到控制。最高层级基于主机 IP 地址或密码验证来限制访问文件服务器内容的查看。在此之下，每个单独的共享（目录、打印机或其他资源）都有其自身的访问权限以及可选的主机/密码限制。最后，在共享内部，单个文件受到基于已验证访问该共享的用户或主机的访问权限的限制。

使用密码进行用户身份验证可以以分布式方式（由每个单独的共享主机）或以集中方式（由中央网络登录服务器）处理。这是 Windows 中“工作组”和“域”之间的区别。*工作组*是一组同意出现在彼此网络浏览器窗口中的机器，每台机器各自处理其自身的身份验证和安全。*域*是一组机器，其安全职责由所有成员机器必须订阅的中央服务器处理。

Samba 提供了在所有这些层级上限制访问的能力，并且还可以充当“主浏览器”（在工作组上下文中）或域控制器（在域环境中的中央登录权威）。你很快就会看到这是如何实现的。

### 使用 AppleTalk 与 Macintosh 客户端进行文件和打印共享

Samba 不会提供与 Macintosh 客户端通信的 SMB/CIFS 功能。对于该任务，请考虑 AppleTalk。这个局域网级别的协议套件通过其自身的传输层或 IP 运行，并被许多企业和大学网络使用。

为 Unix 平台提供 AppleTalk 功能的软件包称为 netatalk，它可以在 ports 集合中找到。要安装 AppleTalk 支持，请从 /usr/ports/net/netatalk 构建 netatalk。（忽略 netatalk-asun port，只安装基本的 netatalk port；如果你同时安装这两个 ports，AppleTalk 将无法工作。）

在你的内核配置中启用 NETATALK 选项。有关构建自定义内核的信息，请参见第 16 章“内核配置”。netatalk port 安装了一系列配置文件——每个必要的守护进程一个——以及 /dist（或 distribution）参考副本。守护进程在默认安装配置中运行；你可以修改某些配置文件来调整其行为。网络上的每台 Macintosh 将在其 AppleShare 区域中的 Chooser（或 Mac OS X 中的“连接服务器”窗口）中看到这台机器。

有关 netatalk 软件包中各种工具的更完整描述以及指向其他文档的链接，请参见 netatalk 的官方网站 `http://netatalk.sourceforge.net/`。

### 安装和配置 Samba

Samba 可在 `/usr/ports/net/samba` 的 ports 中或 packages 中找到。有关安装软件包或 port 的详细信息，请参阅第 14 章“安装附加软件”。

一旦你安装了 Samba 软件包，各种新项目将被安装，包括守护进程可执行文件（在 `/usr/local/sbin` 中）、管理工具（在 `/usr/local/bin` 中）、文档和示例（在 `/usr/local/share` 中）以及放入 `/usr/local/etc` 的配置文件。一些可能的配置文件在默认安装中不存在；如果你想利用它们的功能，必须从头创建它们。还有代码页（在 `/usr/local/etc/codepages` 中）将 Windows 字符集映射到 Unix 字符集。

软件包中唯一存在的配置文件是 `smb.conf.default`，你必须将其重命名为 `smb.conf` 才能使其工作。同样，`/usr/local/etc/rc.d/samba.sh.sample` 启动脚本必须重命名为 `smb.sh`。以最简单的方式让 Samba 运行，你只需要编辑 `smb.conf` 并修改 workgroup 行，以反映你的机器所属的工作组或域：

```
# workgroup = NT-Domain-Name or Workgroup-Name, eg: REDHAT4
workgroup = MYGROUP
```

