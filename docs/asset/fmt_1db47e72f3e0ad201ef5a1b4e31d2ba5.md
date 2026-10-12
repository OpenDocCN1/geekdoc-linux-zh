
`eth0`: `0x3509` tag `1`, BNC port, address `00 20 38 6a aa`

总结来说，OSI 模型在逻辑上划分了信息（以数据包的形式）从一台计算机到另一台计算机以及在计算机内部传输的路径。该模型中的抽象让你能够忽略为了你创建或使用的任何过程而必须发生的混乱细节。无论你在哪个层级工作，该模型都能让你理解你的局域网（LAN）以及整个互联网是如何运作的。

## Samba

Samba 的存在是我写这本书的首要原因。它提供了 NFS 所欠缺的直接且安全的接口，而且价格比 Novell NetWare 便宜得多。由于 Samba “说”微软原生协议 SMB，你的 Microsoft Windows PC 不需要再像使用 NFS 那样安装任何额外的、昂贵的或难以安装的软件。Samba 将你的 Linux PC 变成了一个强大的 Microsoft Windows 文件和打印服务器。

![](img/29df11d9c5c608cff7b4fa65d0c78e37_163_0.png)

NFS 的设置比 Samba 复杂。它并不是特别困难，但你需要更多的耐心。真正的问题在于购买和配置让你的 Windows 客户端使用 NFS 协议的软件。如果你想使用 Windows 3.x 或 MS-DOS 作为客户端，你必须从 SunSoft, Inc. (http://www.sunsoft.com) 购买如 PC-NFS 等软件；Windows 95 则需要来自 Intergraphics Corp. (http://www.intergraphics.com) 的 DiskAccess 等软件。

## 第3章：内部原理是什么？

当你开箱安装 Windows 95 时，它配备了 Microsoft Client 和 Microsoft TCP/IP。你必须选择将 TCP/IP 作为 Windows 95 软件包的部分进行安装。Microsoft Client 默认使用服务消息块（SMB）协议。该协议被近乎通用的互联网协议（IP）或 TCP/IP 称为。TCP/IP 是 Linux 的默认协议，因此 Windows 和 Linux 机器可以对话。（此前，使用 UNIX/NFS 服务器时，你必须购买额外的软件并安装在 Microsoft Windows PC 上使其支持 NFS 协议。这种购买是非常昂贵的，因为每个 PC 客户端都需要该软件。现在，单台 Linux PC 已经通晓微软原生语言。）

### Samba 协议

SMB 协议负责协商远程文件和打印机等资源的使用。图 3-2 显示了物理存在于 Linux 服务器上的文件 A——在 SMB 术语中，它持有共享。当 Windows 客户端想要使用此文件时，客户端必须告诉服务器将 A 交给它，然后跨网络传输文件内容。SMB 负责处理事务协商的细节。

![](img/29df11d9c5c608cff7b4fa65d0c78e37_164_0.png)

图 3-2：服务器持有客户端所需的文件。

例如，假设我想打开 Microsoft Word 文件 `A.DOC`，它物理存储在我的 Linux 服务器的硬盘上。我将包含 `A.DOC` 的 Linux 目录映射为网络 `E:` 驱动器。当我在 Word 中选择“文件→打开”并选择 `E:\A.DOC` 时，Windows 95 会向 Linux 服务器发送一个 SMB 请求。图 3-3 显示了客户端向服务器请求文件访问权限时发生的过程图。

![](img/29df11d9c5c608cff7b4fa65d0c78e37_165_0.png)

图 3-3：客户端与服务器协商以获取文件的权限。

在服务器接收到有效的 SMB 请求后，它会访问自己的文件系统来获取信息。Samba 充当到达内部的 SMB 数据包与 Linux 操作系统之间的接口。

## 第3章：内部原理

### Samba 守护进程（Daemons）

Samba 的核心是程序 `smbd` 和 `nmbd`。它们通常作为守护进程运行，即一直运行的进程。Red Hat 默认将它们作为守护进程运行。你可以选择从 `inetd` 启动它们（一种类似于超级守护进程，它寻找其控制的任何程序——由 `inetd.conf` 定义并根据需要启动它们）。那种方法会减慢 Samba 的速度，而将 `smbd` 和 `nmbd` 作为守护进程运行的开销较低，因此守护进程方法效果最好。

`nmbd` 进程允许 Linux 服务器被其他机器浏览。`smbd` 守护进程是到达网络的 SMB 数据包与 Linux 操作系统之间的接口。

## 第 3 章：内部原理

```
[homes]
comment = 家目录目录
browseable = no
read only = no
preserve case = yes
short preserve case = yes
create mode = 0750
```

```
; 注意：没有必要专门定义每一个单独的打印机
[printers]
comment = 所有打印机
path = /var/spool/samba
browseable = no
printable = yes
; 设置 public = yes 以允许用户 'guest account' 打印
public = no
writable = no
create mode = 0700
```
