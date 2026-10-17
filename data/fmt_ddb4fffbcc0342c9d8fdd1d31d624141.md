
总而言，`dump` 和 `tar` 的使用非常简单且直观。虽然 Windows 在运行时会锁定文件，但备份根系统就像备份目录一样简单。这是 Windows 不具备的能力。`dump` 支持远程备份，但只有在适当的分区或文件系统共享到网络后才能进行。完成后，机器上的脚本每晚可以监控文件系统、对其备份并卸载它。唯一的限制是网络带宽。Elutions 预计每晚大约有 100 GB。在 100 Mb/sec（每秒 10 兆字节）的速度下，需要 10,000 秒，即三小时的网络带宽。如果数据量增长，我们可能需要考虑多个网络通道或更高速度的网络。

## 调度

备份可以在 Linux 和 Windows 上进行调度。Windows 上的调度服务和 Linux 上的 `cron` 程序允许任务在特定时间运行。`dump` 和 `ntbackup` 都可以从命令行运行，因此都易于编写脚本，生成的脚本可以被保护。为了不需要让人在场进行备份，Elutions 将购买足够的 DVD-RAM 光盘以供每晚使用。此外，DVD-RAM 光盘也将每周备份。DVD-RAM 介质将存储在本地。定期会将一套完整的备份异地存储。由于 Elutions 是一家小公司，备份介质的安全将通过储存在锁好的房间来。

## 总结

我们检查了 Windows 和 Linux 自带的一些备份工具。通常，`ntbackup` 和 `dump` 都能完成系统备份或简单文件备份的任务。对于 Windows 2000，由于两个原因，问题变得有些复杂：

- Windows 会锁定许多文件，这些文件无法复制。为了解决这个问题，Windows 有特殊的 API 可以从锁定文件的服务直接请求内容。`ntbackup` 知晓并使用这些 API，而其他自定义程序（如 Cygwin 中的 `tar` 和 `cpio`）则并不支持。结果是它们都无法完全备份系统分区中的文件。
- Windows 无法将系统恢复到未格式化的磁盘。系统恢复操作需要分区中有一个运行的 Windows 操作系统。这意味着对于完整恢复，需要完整的安装。

Windows 操作系统必须在恢复操作之前安装。在我们正在使用的 ThinkPad 770X 上以及 2-GB 的分区大小下，整个恢复操作大约需要两个小时。

Windows 2000 和 Linux 都可以备份文件。恢复文件非常简单，但恢复文件的安全性就没那么简单了。Windows 提供的用于保存和恢复文件及其安全上下文的唯一工具是 `ntbackup`。其他文件复制工具（例如 Cygwin 的 `tar` 命令）并未尝试完全处理安全信息。第三方产品可以做到。

Linux 拥有更简单的安全模型，Linux 上大多数归档和转储工具都能正确处理安全性和启动分区。

最后，在 Linux 上执行备份和恢复操作所需的唯一权限是 `root` 账户。在 Windows 上，必须拥有备份权限或用户必须是 `Administrators` 组的成员。

Elutions 将在 Linux 上使用 `dump` 并在 Windows 上使用 `ntbackup`。此外，还将实施相关程序，让个人将自己的文件备份到共享文件系统。使用该 `at` 命令（Linux 和 Windows 上均可用），将编写脚本定期将用户数据完全备份到共享文件系统中。共享文件系统将定期备份到其他介质上。我们目前的选择是 DVD-RAM，单个磁盘可以容纳 9 GB 以上。

## 拨号

### 本章主题

- 点对点连接
- Windows 和 Linux 客户端配置
- 点对点协议
- 互操作性

当永久连接成本过高时，交换式数据连接非常有用。大多数家庭接入的连接都是拨号客户端连接。最近 DSL 和电缆调制解调器的出现开始侵蚀家庭拨号用户群。串行链路接口协议 (SLIP) 和点对点协议 (PPP) 是两种常见的拨号 IP 协议。Windows 和 Linux 都支持 SLIP 和 PPP，它们可以使用这些连接协议相互通信。当需要特定于安装的动作时，可以使用脚本来扩展 SLIP 和 PPP。出差的旅客和居家通勤者将使用 Windows 或 Linux 拨号技术来访问 ISP，或访问 Elutions 办公室配置用于入站拨号访问的机器。在本章中，我们将讨论拨号连接和协议。我们还将讨论如何设置 Linux 和 Windows 的入站和出站连接。我们的目的是介绍这些可用技术。Linux 和 Windows 中的拨号技术和配置可以写满一本书。我们在本章中仅介绍表面的细节并建立基础连接。

## 拨号连接

到目前为止我们的网络讨论是从全连接的角度来看的。我们的系统永久连接到网络并具有全天候访问权限。像电话那样的拨号连接没有寿命。拨号连接可以通过调制解调器、使用两台计算机上的串行、并行或红外端口的直接连接，甚至是无线连接来实现。我们将关注电话拨号连接。表 1-1 列出了 Linux 和 Windows 提供的支持。每个功能都有一个字母等级，这是我们对该功能质量的评价。

### 表 17-1 支持的拨号协议

| 协议 | Linux | Windows |
| :--- | :--- | :--- |
| Telnet 客户端 | B | B+ |
| Telnet 服务器 | A | B- |
| SLIP 客户端 | B | B |
| SLIP 服务器 | B | |
| PPP 客户端 | C | A |
| PPP 服务器 | C | A |
| VPN | | A |
| L2TP | | A |

> **注意：** Windows telnet 客户端获得 B+ 是因为 Windows 版本的 telnet 支持 Windows 认证，这意味着密码不会通过连接传输。Windows telnet 服务器获得 B- 是基于我们对 Windows telnet 服务器低可靠性的经验。Windows 2000 和 Windows XP 的 Telnet Server 比之前的版本有了很大改进。然而，微软仍然至少有两个 telnet 服务器。一个随 Windows 2000 和 Windows XP 基础产品提供，并支持最多两个同时连接。另一个随 Services for Unix 产品提供并支持更多。Windows 没有 SLIP 服务器。Linux 的 PPP 能力需要使用脚本。Linux 没有通用策略，且不与 Windows Active Directory 集成。

我们将逐一介绍这些功能。然而，必须早早指出，Windows 对 PPP、虚拟专用网络 (VPN) 和二层隧道协议 (L2TP) 协议的支持要优越得多。Windows 功能的增加伴随着设置复杂性的随之增加。Windows 中的这些拨号连接完全值得写一本书。我们不会详细讨论 Windows 拨号服务的配置问题。我们将展示如何设置和配置入站和出站连接，但对于高级功能，我们将推迟到其他著作。关于 Windows 2000 拨号管理的极佳参考，请参阅 William Boswell 的 *Inside Windows 2000 Server* (New Riders Publishing, 2000, ISBN 1-5605-929-7)。

## 拨号连接

在讨论协议之前，我们需要了解如何将每个拨号连接接入网络。SLIP、PPP、VPN 和 L2TP 都是点对点连接协议。它们在两台计算机之间建立了最低级别的连接。一旦建立连接，就必须将 TCP/IP 协议栈绑定到连接上。连接的每个端必须看起来像一个网络适配器：媒体访问控制 (MAC)。连接建立后，所有协议都定义两个 IP 地址（每个端一个），并要求每端将这些地址添加到其路由表中。Linux 和 Windows 是如何实现的？只有在连接绑定到 TCP/IP 栈后，连接才建立。步骤 1 提供了最有趣的部分。某些 ISP 配置为用户登录时启动协议。在何种情况下，检查连接都需要一个通信程序。图 17-1 显示了最简单的步骤。

### 图 17-1 点对点连接并绑定到 TCP/IP

| 步骤 | 动作 | 备注 |
| :--- | :--- | :--- |
| 步骤 1 | | C2 |
| 步骤 2 | | C2 |
| 步骤 3 | | C2 |
| 步骤 4 | | C2 |

通信程序经常需要。表 17-2 列出了这些程序。

### 表 17-2 Windows 和 Linux 中的通信程序

| | Linux | Windows |
| :--- | :--- | :--- |
| 程序 | `cu`, `dip`, `minicom` | `hyperterminal` |

AT 命令（适用于所有 Hayes 兼容调制解调器）返回 OK，说明软件已找到硬件。连接 telnet 线并输入以下内容将线路正在拨号：

```
ATDT555
```

你应该听到拨号音和调制音。注意我输入了一个不完整的号码。这意味着你并没有拨给任何人。这个简单的测试并不意味着电话已接通——只是计算机及其软件可以直接与调制解调器通信。我们不会详细讨论如何设置和诊断串行连接。

## Telnet

我们对 telnet 的讨论顺序有点乱，因为在使用 telnet 服务之前必须存在 TCP/IP 连接。先提到 telnet 是它是几乎所有启用 TCP/IP 的计算机都支持的最简单互操作连接。它可以在本章描述的拨号连接和局域网上使用。

telnet 是一种在两台机器之间建立 ASCII 终端会话的协议。不支持图形界面；只能执行命令行程序，所有输出都到终端屏幕。telnet 由一个服务器和一个客户端程序组成。服务器在 Windows 中是一个服务，在 Linux 上是一个守护进程。表 17-3 显示了如何在 Linux 和 Windows 上启动和停止 telnet 服务。

### 表 17-3 启动和停止 Telnet 服务

| | Linux | Windows |
| :--- | :--- | :--- |
| **命令行** | | |
| 启动 | `chkconfig --level 345 telnet on` | `net start tlntsvr` |
| 停止 | `chkconfig --level 345 telnet off` | `net stop tlntsvr` |
| **GUI** | | |
| 启动 | System V Init Editor | `services.msc` and `tlntadmn` |
| 停止 | System V Init Editor | `services.msc` and `tlntadmn` |

Telnet 托管在 TCP/IP 上。客户端连接到远程计算机的 23 端口。一旦连接，远程计算机将启动终端会话，用户即可获得远程系统的命令行访问。要建立连接，需执行 telnet 客户端。在 Windows 或 Linux 上输入以下任一命令均可启动 telnet 客户端：

```
telnet <IP address>
telnet hostname
```

如果远程系统运行着 telnet 服务，用户将被要求使用远程系统账户数据库中的用户名和密码进行登录。Windows 中的 Telnet 具有使用 Windows 身份验证算法的额外功能。其优势是用户名和密码不会以明文形式通过网络传输，并且在域内不需要登录。

## SLIP

SLIP 在两台计算机之间建立拨号连接，TCP/IP 可通过其流动。SLIP 是一种简单的协议（RFC 1055）。SLIP 仅传输 IP 数据包并用 `0xC0` 字节结束传输。如果数据包中出现 `0xC0` 字节，则将其替换为 `0xDB, 0xDC` 序列。如果流中出现 `0xDB` 字节，则将其替换为 `0xDB, 0xDD` 序列。这就是该协议的内容。SLIP 需要配置串口以传输 8 位数据、无奇偶校验，并带有硬件或 XON/XOFF 流控。在高速传输速度下，选择硬件流控至关重要。

SLIP 是一个过时的协议，因为 SLIP 帧不包含错误检查。它依赖高层协议来提供错误检测。Linux 支持 SLIP 客户端和服务器，但 Windows 不支持入站 SLIP 连接（Windows 没有 SLIP 服务）。在互操作解决方案中，SLIP 主要被 PPP 取代；在仅限 Windows 的环境中则被 VPN 和 L2TP 取代。压缩 SLIP (CSLIP) 通过移除对端机器已知的冗余信息来压缩数据头，从而增加串口的带宽。Windows 客户端支持 SLIP 和 CSLIP。

### Linux

在尝试建立 SLIP 连接之前，我们必须确保有一个运行中的 Linux SLIP 模块。Linux 通常以模块形式随附 SLIP。我们使用 `lsmod` 来检查 `slip` 模块是否已加载。如果列表中没有 `slip`，我们（以 `root` 身份）输入：

```
sbin/modprobe slip
```

随后的 `lsmod` 将显示 `slip` 已加载。如果需要一直加载，则应在系统启动时加载 `slip`。将前述命令行添加到 `/etc/rc.d/rc.local` 中即可实现启动时加载的需求。

以下是从 Linux 系统设置 SLIP 连接所需的步骤。使用 `dip` 程序完成这些操作最为容易，本描述假设我们正在使用 `dip`。

1. 输入本地和远程 IP 地址、要使用的通信端口以及连接速度。

```
get slip 206.45.34.2      # 从 ISP 获取
get srtip 206.45.34.19     # 从 ISP 获取
speed 38400
port ttyS0
```

2. 拨号远程系统并登录。如果远程系统上的 SLIP 软件没有启动，请在远程系统上启动。

```
term                       # 设置 dip 进入与调制解调器通信模式
ATX                        # 等待 "OK"
ATDT 5555 5555 # 拨号 ISP，等待 "CONNECTED"
                             # 以及 "login prompt"
egb                        # 输入用户名；等待 "password:"
\*\***                       # 输入密码；等待登录
```

此时，要么 ISP 已经启动了 SLIP 服务，要么你必须输入 ISP 推荐的命令。

在远程端启动 SLIP 后，通过 CNTL-]（同时按下 Control 键和右括号）进入 `dip` 命令模式。

3. 使用 `default` `dip` 命令设置到远程系统的路由。在这里，我们告诉本地路由发送那些我们不识别的该 SLIP 连接远端 IP 地址的数据包。

```
default
```
