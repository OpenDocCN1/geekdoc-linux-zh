
# 介绍一个全球科技品牌
它承诺改变
你消费科技的方式

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_88_0.png)

# 报道
最新的
科技

- 深入
- 详细
- 经过全面测试的设备

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_88_1.png)

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_88_2.png)

# 黑客手册
2015年

# 网络

真正的 Linux 大师的标志是在桌面、命令行以及最重要的网络方面的专业能力。将多台机器（甚至运行不同操作系统的机器）连接在一起的技能至关重要——在当今时代，孤立的 PC 是极为罕见的。

- Samba：与 Windows 共舞 ........................................................ 92
- 网络：基础知识 ................................................................. 98
- Wireshark：分析流量 .......................................................... 102
- 网络：构建路由器 ........................................................ 106
- Deluge：搭建 Torrent 服务器 .................................................. 110
- Docker：构建容器 ........................................................... 114
- Zabbix：监控你的网络 .................................................... 118

# Samba

# 与 Windows 共舞

这是一个面向 Linux 的 Windows 互操作套件，拥有 Active Directory 支持。让我们来体验一下。

我们都喜欢我们的 Linux 机器，但大多数人在某个时候都需要与 Windows 机器在网络中共存，并知道 Samba 是能够在 Linux 和 Windows 之间共享文件系统的东西。但它能做的远不止这些，而且从第 4 版开始，它与微软的 Active Directory 完全兼容。这是一件大事——Samba 长期以来一直能够充当 Windows NT 4.0 域控制器，或者

> “Samba 4 完全实现了 Active Directory 域控制器功能”

加入现有的 Windows NT 4.0 域，但随着 Windows 2000 的发布，微软

开始从 NT 域控制器转向其新的 Active Directory，拉大了 Linux 和 Windows 生态系统之间的差距。Samba 4 及更高版本通过完全兼容 Active Directory，为这一问题提供了期待已久的补救措施。它完全实现了 Active Directory 域控制器功能，从而有效

取代 Microsoft 的 Windows Server 产品线中的相应功能。

Samba 是服务器消息块（Server Message Block，SMB）协议的开源实现。这是一种应用层网络协议，最初由 IBM 开发，用于提供对文件和打印机的共享访问。微软扩展了其对 SMB 的实现，以支持使用其自身的 NT LAN Manager（NTLM）以及后来的 NTLMv2 协议进行身份验证。微软称这一实现为通用互联网文件系统（Common Internet File System，CIFS）。包括支持符号链接在内的进一步扩展，以 SMB2 的形式随 Windows Vista 发布。

Samba 从 3.6 版本开始支持 SMB2。微软随 Windows 7 推出了 SMB2.1，随 Windows 8 推出了 SMB3。它将这些不同版本的协议称为方言，因此 CIFS 和 SMB2 都是 SMB 协议的方言。虽然这些方言是专有的，但其规范是公开可用的。

微软在 2004 年与欧洲法院和解的成果之一是发布了使用 Active Directory 进行网络身份验证的完整文档。这促使了 Samba 第 4 版的开发，微软本身也参与了测试。

（LDAP）版本 2 和 3。Kerberos 和 DNS。Samba 使用自己的 LDAP 实现，称为 ldb；它不支持将 OpenLDAP 用于 Active Directory。

因此，现在有两种使用 Samba 的方式——一种是像以前那样使用它（经典 Samba），它可以作为域成员或独立运行，这也是设置基本共享所需的全部内容。另一种方式是将 Samba 用作功能完备的 ADDC。你使用 Samba 的方式将取决于你的需求，但首先要做的是安装它。大多数发行版都应在软件仓库中包含它。另一种选择是从 www.samba. 下载源代码来构建。

> “使用 Samba 的方式取决于你的需求”

org/samba/download。安装后，Samba 的配置文件名为 smb.conf，通常位于子目录中，例如 /etc/samba。最简单的配置是使用一个独立的公共共享：

```
[global]

server string = Samba Server Version

%v

# Treat unknown users as a guest
(where permitted)
security = user
map to guest = Bad User

[tmp]
path = /tmp
read only = No
browseable = Yes
guest ok = Yes
force user = nobody
force group = nobody
create mask = 0755
directory mask = 0755
```

这会使服务器上的 /tmp 通过 TCP/IP 作为 Samba 共享提供。使用 security = user 和 map to guest 可以让来宾共享以类似于现有的 Samba 管理员所熟悉的已弃用的 security = share 模式的方式运行。拥有 Samba 无法识别的 Windows 用户名的用户将无需提供凭据即可访问共享，并且他们将被认证为来宾用户。

他们在那里写入的任何文件，其用户 ID 和组 ID 都将设置为 'nobody'。然而，如果 Samba 知道该用户名，则会提示用户输入其密码。这可能看起来很奇怪，但与 Windows 的工作方式一致。启动 Samba 守护进程 smbd，即可让该共享在 Windows 上被访问。要访问它，只需使用 Windows 资源管理器浏览到 Samba 服务器（你可以使用其名称或 IP 地址）。

# 添加/移除 NetBIOS

有一种长期以来一直与 Windows 网络关联的网络协议，因此它是 Samba 套件中不可或缺的一部分：NetBIOS。如今，NetBIOS 通常指基于 TCP/IP 的 NetBIOS 协议，它被认为是一种传统协议。它为没有 DNS 功能的设备提供名称解析、文件和打印机共享。

它曾经在 Windows 网络中必不可少，但现在除了涉及旧版 Windows 之外，已不再必要。如果你希望运行 Windows 2000 之前的操作系统的客户端能够访问你的共享，你仍然需要它。如果你不想包含 NetBIOS，可以在 smb.conf 的 [global] 部分添加以下内容来明确示意：

```
[global]
# disable NetBIOS
 disable netbios = yes
 smb ports = 445
```

不过，如果你需要启用 NetBIOS，则需要对 smb.conf 进行其他更改：
[global]

```
# NetBIOS identification
workgroup = WORKGROUP
netbios name = MYHOST
wins support = Yes
```

这告诉 Samba 使用 NetBIOS 让其在默认工作组中向 Windows 网络宣传自己（Windows 机器默认使用名为 WORKGROUP 的工作组），并充当 WINS 服务器。NetBIOS 名称相当于主机名——不必与主机名相同，但通常如此。WINS 是 Windows Internet

# 快速提示

修改 smb.conf 时，你无需重启或向 Samba 发送信号，因为它会自动检测更改。

# SMBFS 和 CIFS

Linux 上有两个虚拟文件系统实现允许挂载 SMB 共享：SMBFS 和 CIFS。后者是较新的实现，已内置在内核中。使用 CIFS 所需的用户空间工具最初是 Samba 的一部分，但现在已经是一个名为 cifs-utils 的独立包。

最初也是 Samba 套件一部分的 SMBFS 已被弃用——你应该使用 CIFS 来挂载 Samba 文件系统。其结果是，如果你只想在 Linux 机器上挂载 Windows 共享，你不需要 Samba。挂载 Windows 共享非常简单：

mount -t cifs -o username=myuser,password=mypass //myserver/myshare /mnt

CIFS 和 SMB 之间的区别可能有点令人困惑，因为 CIFS 方言比 SMB 新，但比 SMB2 旧，而

CIFS 比 SMBFS 新，支持 SMB、CIFS 以及更新的 SMB2 和 SMB3 方言。更多详情，请参阅客户端指南。http://pserver.samba.org/samba/ftp/cifs-cvs/linux-cifs-client-guide.pdf

SMB 和 CIFS 协议规范发布于 http://msdn.microsoft.com/en-us/library/cc246482.aspx 和 http://msdn.microsoft.com/en-us/library/ee442092.aspx。
