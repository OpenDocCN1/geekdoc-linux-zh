
## Windows 网络概念

Windows 网络使用服务器消息块（SMB）协议进行网络机器之间的通信。广而言之，SMB 协议提供以下功能：

- 打开和关闭文件
- 读取和写入数据
- 获取目录信息
- 维护共享资源的通用命名约定（UNC）名称（例如打印机、文件）
- 操作系统开销

SMB 协议大致类似于 Unix 和 lpd 守护进程的结合。注意：与 Unix 相比，SMB 更复杂且更容易出现 Bug，但同时，一个 SMB 命令就可以替代三个 NFS 命令。SMB 协议运行在 NetBIOS 网络接口之上。NetBIOS 代表网络基本输入输出系统。它是用于 Windows 网络的会话层接口（OSI 模型）。NetBIOS 提供以下基本服务：

| 名称 | 服务 |
| :--- | :--- |
| 服务 | 维护应用程序名称数据库 |
| 会话 | 处理连接/断开以及应用程序之间的通信 |
| 数据报 | 将数据报（基本数据包）发送到网络，接收 |

BEUI 是一种为 LocalManager 网络设计的可路由协议。它是 NetBIOS 的一种实现。

## 引言

通用命名约定（UNC）用于指定 Windows 机器上共享资源（“共享”）的语法。UNC 格式如下：

```
\\server\sharename\subdirectory\filename
```

`server` 和 `sharename` 是强制性的；`subdirectory` 和 `filename` 是可选的。例如，在本章开始的示例网络中，我的打印机共享为：

```
\Loki\My Documents\Linux Book
```

Windows 网络有两种类型：工作组（workgroups）和域（domains）。工作组可以在没有 NT 机器的情况下运行，是点对点网络，允许跨网络访问资源（打印机、目录）。工作组具有非常有限的安全功能，但为打印机或其他共享设置密码。域需要 NT 机器，实现集中式访问控制。存储账户信息的域机器被称为主域控制器。

> 注意：NT 域和域是完全不同的概念。

在 Windows 网络上查看可用资源被称为浏览（browsing）。为了方便浏览，Windows 网络要求网络上的一台机器维护浏览资源列表。维护该列表的计算机被称为主浏览器。

Windows 命名服务（WINS）是将域名解析为 IP 地址的客户端服务器机制。LMHOSTS 文件用于 Windows 系统将 BIOS 名称与 IP 地址关联（不像 Linux 的 `/etc/hosts` 文件）。它位于 `WINNT2\drivers\etc` 目录（Windows NT）或 `WINDOWS` 目录（Windows 95/98）。

Samba 是运行在 Linux 上的程序包。运行 Samba 的 Linux 机器可以作为 Windows 机器的文件和打印服务器。可以从此处获取 Samba：http://samba.anu.edu.au/pub/samba ![](img/3ac9b27762bf61e48d880d6f0f96f8b_520_0.png) Samba 配置文件 `smb.conf` 包含了 `smbd` 和 `nmbd` 的配置。

本节涵盖的命令包括：

| 命令 | 描述 |
| :--- | :--- |
| mattrib | 为 MS-DOS 文件设置属性 |
| mbadblocks | 扫描 MS-DOS 磁盘的坏道 |
| mcd | 切换目录 |
| mdel | 从目录删除文件 |
| mdeltree | 删除目录树 |
| mdir | 显示目录内容 |
| mdu | 显示 DOS 磁盘使用情况 |
| mformat | 格式化 DOS 磁盘 |
| mlabel | 为 DOS 磁盘标记 |
| mmd | 创建 DOS 目录 |
| mrd | 删除 DOS 目录 |
| mmove | 在 DOS 文件系统中移动文件 |
| mtype | 显示 DOS 文件内容 |
| xcopy | 递归复制 DOS 目录内容 |
| nmbd | 提供 NetBIOS 服务器 |
| smclient | 访问网络上的 Windows 机器 |
| smbount | 挂载 LanManager 文件系统 |
| smbstatus | SMB 连接的状态信息 |

`smbount` 卸载 LanManager 文件系统。

| /usr/local/samba | Samba Samba目录 |
| /etc/lmhosts | SMB 的 IP 到主机名映射 |

以下选项适用于所有 mtools 命令：

- `-o` 默认覆盖主名称。
- `-O` 默认覆盖次要名称。
- `-r` 默认重命名主名称。
- `-A` 默认重命名次要名称。
- `-a` 默认自动重命名主名称。
- `-A` 默认自动重命名次要名称。
- `-s` 默认跳过主名称。
- `-S` 默认跳过次要名称。
- `-m` 询问用户如何处理主名称。
- `-M` 询问用户如何处理次要名称。

```
mattrib [-a|+a] [-h|+h] [-r|+r] [-s|+s] [-i] [-X] MSDOSFILE [MSDOSFILES ...]
```

此命令用于为 MS-DOS 文件添加或删除属性标记。

示例：使软盘上的 MS-DOS 文件“secret.txt”对 dir 命令不可：

```
mattrib +h secret.txt
```
