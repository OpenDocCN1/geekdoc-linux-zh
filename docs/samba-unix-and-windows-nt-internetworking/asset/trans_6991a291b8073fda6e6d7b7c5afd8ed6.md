
![](img/7684008b1d7775727df27d44aed5b3f0_190_0.png)

图 14.4：SMB2WWW 网络邻域

## Smbconfool

Smbconfool 是另一个 smb.conf 编辑工具。与 SWAT 不同，smbconfool 会保留 smb.conf 中的注释。然而，你无法输入注释。该功能将在未来的版本中提供。你可以执行大多数常规配置任务，如创建、更新和删除共享部分。

Smbconfool 基于 Java，因此浏览器需要 Java 支持。你可以从以下地址获取 smbconfool 的副本：http://www.eatonweb.com/samba/

## Windows 工具

### bbSAT

HP 3000 渠道合作伙伴 B+B Unternehmensberatung 开发了一款名为 bbSAT（图 14.5）的基于 Windows 的 GUI 工具，用于维护 Samba 配置。此工作是在 Samba 移植到 MPE/iX 的过程中完成的。bbSAT 可免费获得，并且可与其他 Samba 平台一起使用。与 smbconfool 类似，bbSAT 会保留 smb.conf 注释。还有一个增强版的 bbSAT，名为“bbSAT (GE) Gold Edition”，提供额外功能。更多信息请访问 bbSAT 网站：http://jazz.external.hp.com/src/samba/bbsat_index.html.

![](img/7684008b1d7775727df27d44aed5b3f0_191_0.png)

图 14.5：bbSAT

### smbedit

smbedit 是另一款免费的 Win32 应用程序，可从 Windows 客户端编辑 smb.conf（图 14.6）。除了常规的 Samba 配置编辑外，你还可以调用 Samba 服务，如 testparm 和 smbstatus。更多信息请参阅 smbedit 网页：http://us3.samba.org/samba/smbedit/readme.htm.

![](img/7684008b1d7775727df27d44aed5b3f0_192_0.png)

图 14.6：smbedit

## 其他工具

### smb-mode.el

对于 Emacs 爱好者来说，有一个名为 smb-mode.el 的 Emacs 主模式可用于编辑 smb.conf。使用 smb-mode.el，你可以编辑单独的 smb.conf 部分，从 Samba 手册页查找参数信息，执行参数补全，并通过 Samba testparm 命令运行缓冲区。要获取 smb-mode.el 的副本，请访问以下网站：http://users.gtn.net/fraserm/smbmode.html.

### GSMB

在我们关注 smb.conf 编辑工具之外，我们注意到一个名为 gsmb（图 14.7）的 Gtk 工具，用于管理 Samba smbpasswd 加密密码支持。它由 Laurent Foucher 创建。gsmb 使用 Gtk 1.2.0 库。更多信息请访问 gsmb 网站：http://savage.iut-blagnac.fr/projets/developpement/gsmb/.

![](img/7684008b1d7775727df27d44aed5b3f0_193_0.png)

图 14.7：gsmb

## 摘要

- 有用的 Samba 管理命令行工具包括：`testparm`、`smbclient`、`smbstatus` 和 `testprns`。
- 有用的 Samba GUI 管理工具包括：
  - **Web 工具：** SWAT、Webmin、SMB2WWW 和 smbconfool。
  - **Windows 工具：** bbSAT 和 smbedit。
  - **其他工具：** smb-mode.el 和 gsmb。

## 第 15 章：故障排除

### 概述

> “政治就是寻找麻烦的艺术，找到它，误诊它，然后错误地应用错误的补救措施。”

**格鲁乔·马克斯**

计算机在某种程度上就像政治。迟早麻烦总会出现。它通常发生在你对生产服务进行一次深夜的小改动时。你知道那种情况。它总是某个预防性服务补丁，用于你从未见过的问题；供应商建议需要应用的补丁，保证它只是一个良性的软件更新。你应用补丁并梦想着第二天早上睡个懒觉。就在你准备收工时，问题症状开始从多个子系统出现。SNMP 监控警报到处弹出，宣布网络各地的服务器故障。在紧张的肾上腺素激增中，你迅速尝试在为时已晚之前回滚补丁。进行到一半时，卸载任务失败，你的屏幕变黑，电话开始响个不停。

残酷吧？无法避免计算机和网络问题，但可以限制灾难的范围。诀窍是始终手边有一套良好的诊断工具，并有一个可靠的回退计划。安装新系统时，先在隔离的测试环境中试用。当生产系统出现问题时，将其作为一系列验证阶段来处理。从最低级别的子系统开始。依次检查每个更高级别的服务，在进行过程中排除可能性。此过程有助于诊断根源于复杂子系统相互关系的事件。

### 追踪 Samba

Samba 是由紧密耦合的子系统组成的一个网络服务的典型例子。因此，通常很有帮助以上一段所述的分步方式处理 Samba 问题。首先验证从电路的服务器端和客户端的网络连接。接下来确认 smbd 和 nmbd 正在运行并监听连接请求。确保配置文件正确反映了 Samba 在工作组或域中扮演的角色。当其他方法都失败时，确保你知道去哪里寻求帮助。

在以下各节中，我们将仔细查看在网络、守护进程和配置级别验证 Samba 服务。表 15.1 列出了我们在分析系统的每个组件时将使用的工具集。

### 表 15.1 故障排除工具

#### Samba 工具

```
smbclient
nmblookup
testparm
testprns
```

#### UNIX 工具

- `ifconfig`
- `netstat`
- `ping`
- `ps`
- `iostat`

#### Windows 客户端工具

- `NET`
- `NBTSTAT`
- `WINIPCFG`

### 网络连接

开始故障排除时，先检查客户端和服务器之间的网络连接。

大家能否通过线路相互通信？每个人是否都配置为支持 NetBIOS over TCP/IP？分配的 IP 地址和子网是否正确？在每个 UNIX 客户端和服务器上使用 `ifconfig` 命令（示例 15.1），在 Windows 客户端和服务器上使用 `winipcfg` 命令（图 15.1）来验证网络接口配置。这些命令将显示网络适配器状态、分配的 IP 地址和子网掩码以及广播地址。

### 示例 15.1 ifconfig – UNIX 网络接口

```
# ifconfig en0
en0: flags=0x080863<UP,BROADCAST,NOTRAILERS,RUNNING,SIMPLEX,
    MULTICAST,GROUPRT>
inet 145.142.210.20 netmask 0xffffffff broadcast
    145.142.210.255
```

![](img/7684008b1d7775727df27d44aed5b3f0_196_0.png)

图 15.1：winipcfg – Windows 网络接口

一旦你确定每个系统的网络接口都正常运行，就使用 ping 命令在问题系统之间发送 ICMP 回显请求来检查可达性（示例 15.2）。显示回显往返时间和丢包率统计，指示参与系统之间通信路径的整体健康状况。

### 示例 15.2 ping – 验证通信路径

```
# ping foo.bar.com
PING foo.bar.com (130.111.58.1): 56 data bytes
64 bytes from 130.111.58.1: icmp_seq=0 ttl=252 time=8 ms
64 bytes from 130.111.58.1: icmp_seq=1 ttl=252 time=3 ms
64 bytes from 130.111.58.1: icmp_seq=2 ttl=252 time=8 ms
64 bytes from 130.111.58.1: icmp_seq=3 ttl=252 time=5 ms
--- foo.bar.com ping statistics ---
4 packets transmitted, 4 packets received, 0% packet loss
round-trip min/avg/max = 3/5/8 ms
```

在大多数情况下，可达性问题与路由配置或分配错误的子网掩码有关。使用 netstat 命令显示额外的接口统计信息（表 15.2），包括子网掩码和路由信息（示例 15.3）。可以使用 netstat 的间隔标志在一段时间内收集统计快照。

### 表 15.2 有用的 netstat 选项

| Option | Description |
| -i | 接口状态、数据包速率和错误。 |
| -a | 显示套接字连接状态。 |
| -R | 显示路由表信息。 |
| -m | 显示内存分配和使用情况（mbufs）。 |

### 示例 15.3 netstat – 显示路由

```
$ netstat -rn
Routing tables
Destination Gateway.Flags Refs Use If PMTU Exp Groups
Netmasks:
(0) 0 ff00
(0) 0 ffff ff00

Route Tree for Protocol Family 2:
default 145.142.210.100 UG 22 23884982 en0 - -
127 127.0.0.1 U 3 637989 lo0 - -
140.142.78 145.142.210.20 U 4 20262917 en0 - -
```

### 运行中的守护进程

如果你确信所有网络通信路径都正常工作，那么下一步就是确认 Samba smbd 和 nmbd 守护进程正在运行并监听连接。使用 ps 命令显示 smbd 和 nmbd 的进程状态（示例 15.4）。

查看 inetd 配置（参见“配置文件”部分），以验证在请求 SMB 服务时守护进程将被生成。检查 /usr/local/samba/var 中的 smb.log 和 nmb.log 文件，以获取指示任何启动或通信异常的诊断消息。

### 示例 15.4 'ps' 检查守护进程实例

```
# ps -ef | grep smbd
root 448 1 0 07:25 ? 00:00:00 /usr/local/samba/bin/smbd -D

# ps -ef | grep nmbd
root 446 1 0 07:25 ? 00:00:00 /usr/local/samba/bin/nmbd -D
```

假设 smbd 和 nmbd 守护进程已启动并运行，接下来查看它们是否正在监听传入连接请求。使用 -a 选项调用 netstat 以列出服务器上的端口监听服务集。你可以通过将命令通过管道传输到 grep 来将列表缩小到仅 NetBIOS 服务（示例 15.5）。

### 示例 15.5 Samba 列出 NetBIOS 端口

```
$ netstat -a | grep netbios
```
