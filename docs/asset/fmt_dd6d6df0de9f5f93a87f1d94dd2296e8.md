
## UDP

`tcp_conn_request_max`. 最大连接请求数。默认值为 10。

`tcp_notify_interval`. 连接的第一优先级阈值。默认值为 1000ms。

`tcp_notify_interval`. 已建立连接的第一优先级阈值。默认值为 10 秒。

`tcp_ttl`. 插入 IP 标部的生存时间（TTL）值。默认值为 64。

`udp_port`. 最大端口号。默认值为 65535。

`tcp_remxit_initial`. 与 TCP 相同，但用于 UDP。默认值为 5 秒。

`tcp_remxit_max`. 往返时间的上限。默认值为 1 分钟。

`tcp_remxit_min`. 往返时间的下限。默认值为 500ms。

`tcp_synvd_max`. 最大 SYN 请求数。默认值为 5。

`tcp_sync_hiwat`. 如果不为零，则设置流量控制高水位。默认值为 10。

`tcp_sync_low`. 如果不为零，则设置流量控制低水位。默认值为 5。

`tcp_status`. 获取类似于 `netstat` 的完整报告。

`tcp_keepalive_interval`. TCP/IP 时间。默认值为 32000ms。

`tcp_keepalive_lfp`. 长管道的 TCP/IP 时间。默认值为 64000ms。

`tcp_keepalive_inp`. 窄管道的 TCP/IP 时间。默认值为 4000ms。

`tcp_keepalive_time`. TCP/IP 时间。默认值为 3600s。

# 网络应用接口

![](img/1c1e7552b53cca888836b6c6895bdb48_84_0.png)

> 图 5-1 Windows 2000 应用程序接口。两个 API 都使用 TCP 和 UDP。自《Microsoft Windows 2000 Server TCP/IP Core Networking Guide》，第 17 页。

NetBT 使用了不同的名称解析方案，利用广播、`LMHOSTS` 文件以及 Windows 内部命名服务（WINS）。因此，在基于 Windows 的网络中，你需要同时管理 WinSock 和 NetBIOS 名称解析。然而，如第 2 章所述，Windows 2000 工作站和服务器服务支持直接主机托管——但仅适用于运行 Windows 2000 的计算机。通过直接托管，客户端使用 DNS 解析名称并将通信发送到 TCP 端口 445（通常是 NetBIOS 会话通信发生发生的地方）。

## 5.3.2 HP-UX

直到 10.20 版本，HP-UX TCP/IP 都是基于 Berkeley sockets 的。在 11 版本中，它现在是基于 STEAMS 的。Uresh Vahalia 在《UNIX Internals: The Frontiers》（Prentice Hall, 1996）第 548 页中描述道：“流是内核空间中的驱动程序与用户空间中的进程之间的全双工处理和数据传输路径。STEAMS 是系统调用、内核资源和内核实用例程的集合，它们负责创建、使用和拆毁流。”

基于 STREAMS 的网络应用使用 `HOSTS` 文件、DNS、网络信息服务（NIS）或三者的组合来解析主机名和 IP 地址。除非你安装了如惠普的 Advanced Server/9000 这种会将 NetBIOS 安装到内核中的产品，否则不需要使用 WINS 或等同 `LMHOSTS` 文件。

## 5.4 结论

我们查看了 TCP/IP 协议族传输层中的两种协议：面向连接的 TCP 和无连接的 UDP。你可以在 HP-UX 和 Windows 2000 中调整 TCP 参数，尽管具体调整哪些参数取决于操作系统。NFS 和 NetBIOS 多年来广泛使用 UDP，尽管趋势正转向 TCP。Windows 2000 的网络 API 包括 WinSock 和 NetBIOS。HP-UX 已经从 Berkeley sockets 转换为 STREAMS。

# 参考文献

- 1. Thomas Lee and Joseph Davies, Microsoft Windows 2000 TCP/IP Protocols and Services Technical Reference. (Microsoft Press, 2000).
- 2. Microsoft Corporation, Microsoft Windows 2000 Server TCP/IP Core Networking Guide. (Microsoft Press, 2000).
- 3. Uresh Vahalia, UNIX Internals: The New Frontiers. (Prentice Hall, 1996).

# 名称解析

如第 5 章“传输层”所述。Windows 2000 网络服务是基于 NetBIOS 的。传统上，这需要使用 NetBIOS 缓存、`LMHOSTS` 文件和 WINS 将 NetBIOS 计算机和服务名称解析为 IP 地址。从 Windows 2000 开始，只要你的网络中有 Windows 2000 系统，这些实体就不是必须的。然而，在本文写作期间，纯 Windows 2000 网络是不可能的，更不用说这本书假设你的企业中运行着基于 UNIX 的客户端和服务器。预 Windows 2000 系统以及使 UNIX 与 Windows 系统互操作的工具目前仍使用 NetBIOS。因此，你极可能仍然需要管理 NetBIOS 名称解析和 TCP/IP 主机解析。

## 6.1 Windows 2000

### 6.1.1 计算机名称

Windows 2000 完整计算机名称与完全限定域名名（FQDN）是一个东西。FQDN 由主机名加主 DNS 后缀组成。这些内容可以在安装系统时设置，也可以通过右键点击“我的计算机”，选择“属性”，然后点击“网络标识”选项卡设置。点击“属性”按钮，你将看到“标识更改”框，如图 6–1 所示。

# 标识更改

![](img/1c1e7552b53cca888836b6c6895bdb48_87_0.png)

图 6–1 设置主机名。在此示例中，完整计算机名称是主机名后跟一个点。主 DNS 后缀尚未设置。点击“更多...”按钮允许你设置它。

填写“计算机名称：”框可设置主机名。如果你想设置主 DNS 后缀，请点击“更多...”按钮。你将得到“DNS 后缀和 NetBIOS 计算机名称”框。见图 6–2。

![](img/1c1e7552b53cca888836b6c6895bdb48_87_1.png)

图 6–2 设置主 DNS 后缀。此框允许你设置主 DNS 后缀，它与主机名结合创建完整计算机名称。NetBIOS 计算机名称默认为主机名，提供用于与预 Windows 2000 系统的通信。

# Windows 2000

然而，你可以为一个系统拥有多个 FQDN，因为 Windows 2000 允许为每个域名设置不同的 DNS 后缀。

### 6.1.2 查询 DNS

Windows 2000 背离了通过 NetBIOS 的传统。相反，它的工作相反：它首先检查 DNS。

当用户使用 Ping 等应用程序时，它调用 `gethostaddr()` 函数，该函数会：

1. 检查本地 `HOSTS` 文件。
2. 查询 DNS。
3. 如果所有尝试都失败，则使用 NetBIOS。

《Server TCP/IP Core Networking Guide》，第 338–339 页。

Windows 2000 解析器缓存从 DNS 查询中接收的信息，无论是正面的（找到主机）还是否面的（未找到主机名）。在经过前述的名称转换后，如果需要，所有查询都会首先通过此缓存。DNS 缓存还包含 `HOSTS` 文件中的项，这些项在系统启动时自动加载。

### 6.1.3 Windows 2000 解析器

Windows 2000 解析器采取的第一步是确定提交的是什么类型的名称。名称类型包括：

- FQDNs：这些以点结尾的名称（例如，`mysystem.com`）。这些名称会立即提交给 DNS。
- 多标签、未限定域名：这些名称要么看起来像没有终止点的 FQDN（例如，`mysystem`），要么是不完全的 FQDN（例如，`mysystem`）。对于前者，解析器附加一个点以创建 FQDN 然后提交它。对于后者，它附加 DNS 后缀（由用户指定）并将每个项提交给 DNS。
- 单标签、未限定域名：这些仅仅是主机名（例如，`mysystem`）。在这种情况下，解析器将按照前述点的方式附加 DNS 后缀，直到解析成功。

对于这两两种未限定域名，DHCP 服务器都可以设置主 DNS 后缀和连接特定的 DNS 后缀。DNS 名称解析过程可能非常复杂。有关更多信息，包括一些说明该过程的优秀流程图，请参见《Microsoft Windows 2000 Server TCP/IP Core Networking Guide》，第 344–354 页。

# Windows 2000

![](img/1c1e7552b53cca888836b6c6895bdb48_90_0.png)

图 6–3 高级 TCP/IP 设置对话框中的 DNS 选项卡。右键点击“我的网络位置”→“属性”，右键点击“局域网”→“属性。（这假设你只有一个网络适配器。）然后，选择“Internet协议 (TCP/IP)”并选择“属性”。

## 6.1.4 DNS 名称注册

微软的 DNS 和最新版本的 BIND 现在支持 DNS 数据库的动态更新。传统上，DNS 条目是手动更新的。但现在你实际上拥有了一种长期以来一直是 WINS 功能的名称注册形式。我们将在本章稍后部分回到这个话题。现在，让我们继续学习 NetBIOS 名称注册和解析。

### 6.1.5 NetBIOS

NetBT 是微软在 TCP/IP 之上的 NetBIOS 实现，但我们将假设你使用的是 TCP/IP 和更常用的术语 NetBIOS。基于 NetBIOS 的应用程序使用 NetBIOS 来定位资源、建立连接、接收数据并终止连接。这些服务是名称服务、会话服务和数据报服务。由于 NetBIOS 使用名称来识别网络资源，因此名称服务特别重要，因为它管理着名称的注册和解析。名称服务使用 UDP 端口 137。会话服务在 NetBIOS 应用程序之间建立、维护和终止可靠的对点连接。在进行任何 SMB（服务器消息块，文件共享协议）事务之前，必须建立 NetBIOS 会话。会话服务使用 TCP 端口 139。数据报服务使用 UDP 端口 138 处理不需要会话的消息。

NetBIOS 通过名称而非地址识别网络资源。这些名称长度为 16 个字符，通常包含计算机名、用户名或域名。你可以指定这些名称的前 15 个字符，第 16 个字符保留用于指定所针对特定网络组件。例如，计算机 `JETHRO<00>` 服务的 NetBIOS 名称（由十六进制 00 标识）。域 `CLAMPETT` 的域主浏览器（由十六进制 1B 标识）NetBIOS 名称为 `CLAM-PET<1B>`。在 Windows 2000 系统上，你可以通过在命令提示符输入 `nbtstat -n` 来查看计算机注册了哪些名称。

## 6.1.6 NetBIOS 名称注册

名称是如何创建的？通常，它们在服务启动时创建，例如在系统启动和服务开始启动时，其关联名称通过网络广播或咨询 NetBIOS 名称服务器（通常是 WINS）进行注册。如果客户端未配置向名称服务器注册其名称，它将在启动时在本地子网上发送名为“名称注册请求”的名称广播。在尝试几次后，如果没有其他客户端竞争该名称，客户端的名称将在子网上被正式注册（可以通过运行 `nbtstat -n` 命令查看）。如果系统是 WINS 客户端，它将直接向 WINS 服务器发送名称注册请求，由 WINS 服务器在将其输入数据库之前完成确保名称唯一性的工作。由于广播通常局限于子网，因此使用 WINS 来启用跨网段注册是明智的。

## 6.1.7 NetBIOS 名称解析

系统如何将 NetBIOS 名称解析为 IP 地址取决于节点类型。系统有五种节点类型之一：

| 节点类型 | 描述 |
| :--- | :--- |
| B-节点 | 通过广播解析名称。 |
| P-节点 | 查询 WINS 解析名称。 |
| M-节点 | 先广播，如果失败则查询 WINS。 |
| H-节点 | 先查询 WINS，如果失败则广播。 |
| 增强型 (Enhanced) | 除其他类型外，还使用本地 `LMHOSTS` 文件 DNS。 |

默认情况下，Windows 2000 系统被配置为 B 节点，除非你指定了 WINS 服务器，在这种情况下它们变为 H 节点。Windows DHCP 客户端可以从 DHCP 服务器获取其节点类型。与名称注册一样，在环境中使用 WINS 将极大地有助于名称解析。

如果你将 Windows 2000 系统配置为 WINS 客户端且它变为 H 节点，则将执行以下名称解析过程：

1. 客户端检查 NetBIOS 缓存，查看是否存在目标系统的匹配条目。缓存可以预加载 `LMHOSTS` 文件的内容。请查看该文件中的注释以获取更多信息。
2. 如果失败，它将通过定向数据报（直接发送到 WINS 服务器的可路由消息）联系 WINS 服务器。
3. 如果失败，它将诉诸在本地网络上进行广播。
4. 如果失败，它将检查 `LMHOSTS` 文件（如果启用）。

此过程通常减少了广播流量以及维护 `LMHOSTS` 文件的需求。请记住，从 Windows 2000 开始，此过程仅在 DNS 名称解析失败后发生。

## 6.2 HP-UX

### 6.2.1 计算机名称

你可以在安装时或运行 `/sbin/set_parms hostname` 命令设置 HP-UX 系统的名称。此主机名可以是最多 64 个字符的简单计算机名，也可以 FQDN。如果不是 FQDN，你必须在 `/etc/resol.conf` 文件中提供域名选项（参见下一节“查找过程”）。UNIX 系统没有 NetBIOS 计算机名，除非它们安装了文件共享包，并非所有包如此，某些包允许你让 UNIX 系统成为 WINS 客户端。在某些包中，可以让你让 UNIX 系统成为 WINS 客户端。

### 6.2.2 查找过程

HP-UX 如何将名称解析为 IP 地址取决于其配置。系统可以查询以下源来解析名称和 IP 地址：`/hosts` 文件、NIS 或 DNS。

- `/hosts` 文件：首先查询本地文件。
- NIS：如果 `/hosts` 失败，则查询 NIS。
- DNS：如果 NIS 失败，则查询 DNS。

### 6.2.3 BIND 解析器

`/etc/resolv.conf` 文件用于配置 BIND 解析器，它可以包含以下四个选项之一：

| domain default_domain | 你需要指定的主机名不是完全限定域名名（FQDN），且你尚未配置搜索（search）选项。 |
| :--- | :--- |
| 例如： | 你可以列出最多六个域名，用空格或制表符分隔。如果名称请求不以点结尾，解析器将在向 DNS 提交查询之前，按顺序逐个追加这些域名名。 |
| domain dev.emc.com | |
| | |
| search domain | 你可以指定最多三个名称服务器的 IP 地址，每个地址单独占一行，并以 `nameserver` 选项名称开头。 |
| 例如： | |
| search dev.emc.com it.emc.com | |
| nameserver name_server_IP_address | |
| nameserver 132.22.0.4 | |
| options ndots:n | 设置一个在进行初始 FQDN 查询之前，名称中必须出现的点的数量阈值。 |
| 例如： | 默认值为 1。 |
| options ndots:2 | |

解析器以以下方式向 DNS 提交名称（摘自惠尔特-普的《Installing and Administering Internet Services》，第 65–67 页）。

- 如果目标名称以点结尾，BIND 将直接进行查找，不向其追加任何域名。
- 如果要查询的名称包含至少由 `/etc/resolv.conf` 文件中 `ndots` 选项指定的数量的点，则BIND 将在追加任何域名之前对其进行查找。（`ndots` 的默认值为 1，因此，如果目标名称包含至少一个点，将在追加任何域名之前对其进行查找。）
- 如果目标名称由单个组件组成（不含点），且你设置了主机别名文件（host aliases file），BIND 将会在你的别名文件中进行查找，以将别名转换为完全限定的主机名。你可以为频繁输入的主机名创建一个主机别名文件，如下所示：
```
