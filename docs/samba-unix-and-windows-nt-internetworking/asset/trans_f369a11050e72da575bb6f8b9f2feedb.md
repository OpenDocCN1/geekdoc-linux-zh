
来自多个不同操作系统环境的应用程序（图 3.1）。与上一章自下而上讨论 UNIX 操作系统层不同，我们将从上到下查看 Windows NT。NT 架构堆栈的顶层驻留着用户模式服务。其中包括用于运行传统 DOS 应用程序的虚拟 DOS 机器（VDM）、用于 Windows 3.x 程序的 16 位 Windows 子系统、POSIX 子系统、OS/2 子系统以及 Win32 子系统。在特定子系统内执行的应用程序作为独立的受保护虚拟内存空间进行管理。用户模式服务通过执行服务缓冲区与较低级别的内核模式服务交互。该缓冲区是一个代码段，用于划分和保护用户模式和内核模式操作。紧邻该缓冲区下方的是 NT 执行管理器，它们调节对象和进程生命周期；虚拟内存；过程调用；I/O 功能；并监控访问安全。一个小型固定微内核位于执行管理器层下方。微内核的角色仅限于调度和同步线程以及管理系统中断。操作系统的基础由硬件抽象层（HAL）组成，其工作是隐藏硬件和设备驱动程序依赖性，使其对操作系统其余部分不可见。这简化了、安全化并通用化了用于开发使用硬件服务的应用程序的 API。

| 层 |
|---|
| VDM, Win 3.x, OS/2, POSIX, Win32 |
| 执行服务缓冲区 |
| 执行服务管理器 |
| NT 微内核 |
| 硬件抽象层 |
| 物理硬件 |

图 3.1：Windows NT 分层架构

## 网络
Windows NT 几乎配备了所有可要求的网络协议和接口（图 3.2）。通常的嫌疑对象包括 TCP/IP、NetBIOS/NetBEUI 和 IPX/SPX。基础协议和接口通过额外的通信服务得到增强，以支持虚拟专用网络（VPN）和路由与远程访问服务（RRAS），以及 Microsoft LAN Manager、OS/2 LAN Manager、Banyan Vines、Novell 和 Internet 之间的网关支持。就我们的目的而言，我们将范围缩小到 NetBIOS 和 TCP/IP，它们为 Samba 与 Windows 客户端和服务器之间的服务器消息块（SMB）协议提供传输。

![](img/7684008b1d7775727df27d44aed5b3f0_36_0.png)

图 3.2：Windows NT 网络架构

### NetBIOS
很久以前，在遥远的 LAN 中，开发了一种 API，用于扩展个人计算机的基本输入/输出系统（BIOS）服务，以包括通过网络在计算机之间共享信息的支持。由此产生的 NetBIOS API 记录在 IBM PC Network Technical Reference Manual 中，（1994 年 9 月）。NetBIOS API 定义了三种服务类型：会话服务、数据报服务和名称服务。

NetBIOS 应用程序之间的对话由 NetBIOS 会话和数据报服务促进。NetBIOS 会话服务在两个已知方之间传递消息需要可靠的虚拟电路并保证交付时使用。会话型连接的示例是访问文件共享。相比之下，当目标接收方事先未知时，NetBIOS 数据报服务用于无连接通信且不保证交付。数据报，或在 Microsoft 用语中称为 Mailslots，通常作为网络广播或多播传输到一组机器。数据报服务在客户端请求主浏览器的标识时使用。

### NetBT
NetBIOS 本身不是通信协议，而是一种用于建立和管理基于网络服务的编程接口。NetBIOS 应用程序之间的消息必须由传输层协议在网络上传输。流行的传输协议包括 NetBEUI、IPX、DECnet 和 TCP/IP。Samba 使用 RFC 1001 和 1002 中定义的 NetBIOS over TCP/IP（NetBT）作为其传输服务。正如本章后面将看到的，在大型网络中扩展 NetBIOS 服务时，使用 NetBT 作为传输至关重要。

### 名称服务
NetBIOS 名称服务表示为扁平的、非层次化的命名空间。每个服务条目由一个 16 字节的字符串标识，该字符串构成服务的唯一名称或其所属的组名（图 3.3）。字符串的前 15 个字节表示字母数字的机器名或组名。第 16 个字节是一个十六进制数字，表示机器或组的资源类型（表 3.1）。

![](img/7684008b1d7775727df27d44aed5b3f0_37_0.png)

图 3.3：设置 NetBIOS 名称和工作组

### 表 3.1 NetBIOS 名称
| 字符 1-15： | 机器或组名 |
|---|---|
| <a-z, A-Z, 0-9, !, @, #, $, %, ^, &, (, ), *, ', {, }, .-> | |
| 字符 16： | 唯一资源类型 |

| 代码 | 名称 |
|---|---|
| <00> | 工作站服务名称 |
| <03> | 信使服务名称 |
| <06> | RAS 服务器 |
| <1B> | 域主浏览器 |
| <1F> | NetDDE 服务 |
| <20> | 服务器服务 |
| <21> | RAS 客户端 |
| <BE> | 网络监视器代理 |
| <BF> | 网络监视器实用程序 |

### 组资源类型
| 代码 | 名称 |
|---|---|
| <1C> | 域组名称 |
| <1D> | 主浏览器名称 |
| <1E> | 选举组名称 |
| <20> | Internet 组 |

同一逻辑子网或工作组内资源名称之间的冲突可以通过使用 NetBIOS *作用域* 标识符对命名空间进行分区来解决（图 3.4）。这是一个字符字符串，与 NetBIOS 名称一起使用以在命名空间中强制唯一性。NetBIOS 作用域加上 NetBIOS 名称的总长度不能超过 256 个字符。请注意，使用 NetBIOS 作用域有效地将资源彼此隔离，无法通信。

![](img/7684008b1d7775727df27d44aed5b3f0_39_0.png)

图 3.4：设置 NetBIOS 作用域

每个应用程序通过发出 NetBIOS Add Name 或 Add Group Name 调用在命名空间中注册其存在。服务或组名随后在命名空间中保留，直到通过 Delete 调用明确释放或托管该服务的机器关闭。已注册的名称和资源类型可以通过调用 Windows nbtstat 命令进行查询。在示例 3.1 中，nbtstat 用于显示名为 Wizard 的机器的已注册 NetBIOS 资源表。该列表表明 Wizard 是 Eyrie 组的成员，并且有一个已连接用户 DeRoest。保留名称 __MSBROWSE__ 将 Wizard 标识为该组已注册的主浏览器。

### 示例 3.1 NetBIOS 机器列表
```
C:\nbtstat -a Wizard
NetBIOS Remote Machine Name Table

Name                Type          Status
--------------------------------------------
WIZARD              <00> UNIQUE   Registered
EYRIE                <00> GROUP    Registered
WIZARD               <03> UNIQUE   Registered
WIZARD      <20> UNIQUE      Registered
EYRIE        <1E> GROUP       Registered
DEROEST      <03> UNIQUE      Registered
EYRIE        <1D> UNIQUE      Registered
..__MSBROWSE__.. <01> GROUP   Registered
```

NetBIOS 名称服务使用两种方法注册、解析和释放 NetBIOS 名称、组和地址。第一种方法使用网络广播管理命名空间。客户端机器以广播形式在网络上查询或宣布名称，然后等待对请求的响应。由于交付无法保证，客户端可能需要在请求得到解决前多次重传请求。这种方法在小型网络中有效，但在大型网络中由于广播流量过重而迅速失效。

管理命名空间的第二种方法使用点对点通信。名称注册和 IP 地址解析请求以类似于 Internet 动态 DNS 的方式定向到 NetBIOS 名称服务器（NBNS）。NetBIOS 点对点名称服务在 RFC 1001 和 RFC 1002 中定义，并作为 Microsoft 的 Windows Internet Name Service（WINS）实现（图 3.5）。

![](img/7684008b1d7775727df27d44aed5b3f0_40_0.png)

图 3.5：WINS 配置
