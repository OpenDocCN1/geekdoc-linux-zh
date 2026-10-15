

host rabbit {
    option host-name "rabbit.mytrek.com"
    hardware ethernet 00:80:AD:30:17:2A;
    fixed-address rabbit.mytrek.com;
}
host lizard {
    option host-name "lizard.mytrek.com"
    hardware ethernet 00:70:2b:4b:29:14;
    fixed-address 192.168.0.3;
}

主机声明也可以放置在子网声明内，以提供有关该子网中特定主机的信息。

固定地址的常见候选是网络的 DNS 服务器。通常，您希望 DNS 服务器位于同一 IP 地址，以便可以直接访问。DHCP 服务器然后可以将其 IP 地址提供给其客户端。

| 条目 | 描述 |
|---|---|
| 声明 | |
| shared-network name | 用于指示某些子网是否共享同一物理网络 |
| subnet subnet-number netmask | 引用整个子网地址 |
| range [ dynamic-bootp ] low-address [ high-address ]; | 提供最高和最低动态分配的 IP 地址 |
| host hostname | 引用特定主机 |
| group | 允许您为一组参数和声明命名标签，然后使用该标签将它们应用于子网和主机 |
| allow unknown-clients; deny unknown-clients; | 不向未知客户端动态分配地址 |
| allow bootp; deny bootp; | 确定是否响应 bootp 查询 |
| allow booting; deny booting; | 确定是否响应客户端查询 |
| 参数 | |
| default-lease-time time; | 分配给租约的长度（以秒为单位） |
| max-lease-time time; | 租约的最大长度 |
| hardware hardware-type hardware-address; | 网络硬件类型（以太网或令牌环）和地址 |
| filename "filename"; | 初始引导文件的名称 |
| server-name "name"; | 客户端引导的服务器名称 |
| next-server server-name; | 加载 filename 中指定的初始引导文件的服务器 |
| TABLE 35-1 DHCP Declarations, Parameters, and Options |

| 条目 | 描述 |
|---|---|
| **条目** | |
| `fixed-address address [, address ...];` | 为客户端分配固定地址 |
| `get-lease-hostnames flag;` | 确定是否查找并使用客户端的 IP 地址 |
| `authoritative; not authoritative;` | 拒绝无效地址请求 |
| `server-identifier hostname;` | 指定服务器 |
| **选项** | |
| `option subnet-mask ip-address;` | 客户端的子网掩码 |
| `option routers ip-address [, ipaddress...];` | 客户端子网上的路由器 IP 地址列表 |
| `option domain-name-servers ip-address [, ip-address...];` | 客户端使用的域名服务器列表 |
| `option log-servers ip-address [, ip-address...];` | 客户端使用的日志服务器列表 |
| `option host-name string;` | 客户端的主机名 |
| `option domain-name string;` | 客户端的域名 |
| `option broadcast-address ip-address;` | 客户端的广播地址 |
| `option nis-domain string;` | 客户端的网络信息服务域 |
| `option nis-servers ip-address [, ip-address...];` | 客户端可使用的 NIS 服务器 |
| `option smtp-server ip-address [, ip-address...];` | 客户端使用的 SMTP 服务器列表 |
| `option pop-server ip-address [, ip-address...];` | 客户端使用的 POP 服务器列表 |
| `option nntp-server ip-address [, ip-address...];` | 客户端使用的 NNTP 服务器列表 |
| `option www-server ip-address [, ip-address...];` | 客户端使用的 Web 服务器列表 |

## CHAPTER
NFS 和 NIS

Linux 提供了多种工具，用于访问连接到网络的远程系统上的文件。网络文件系统 Network File System (NFS) 使您能够连接到并直接访问驻留在另一台机器上的资源，例如文件或 CD-ROM 等设备。网络信息服务 Network Information Service (NIS) 维护网络上所有系统的配置文件。通过 Samba，您可以将 Windows 客户端连接到 Microsoft Windows 网络上的服务，例如由 Linux Samba 服务器控制的共享文件、系统和打印机（请参阅第 37 章）。

## 网络文件系统：NFS 和 /etc/exports

NFS 使您能够将远程计算机上的文件系统挂载到自己的系统上，就像它是本地的一样。然后您可以直接访问该远程文件系统上的任何文件。这具有这样的优势：网络上的不同系统可以直接访问相同的文件，而无需各自保留自己的副本。只有一个副本位于远程文件系统上，每个计算机都可以访问它。您可以在其网站 nfs.sourceforge.net 上了解更多关于 NFS 的信息。

> NOTE 基于 BSD Unix 的 Macintosh 计算机的 Mac OS X 现在支持 NFS 用于文件共享。要使用旧版 Apple 操作系统访问 Apple 文件系统和打印机，可以使用 Netatalk。Netatalk 在 Unix 和 Linux 系统上实现了经典的 AppleTalk 和 AppleShare IP 网络协议。当前的 Netatalk 网站是 netatalk.sourceforge.net，提供了指向 FAQ 和 HOW-TO 部分的链接。

## NFS Daemons

NFS 在 TCP/IP 网络上运行。保存文件系统的远程计算机将其提供给网络上的其他计算机。它通过在名为 /etc/exports 的 NFS 配置文件中进行条目，以及运行多个守护进程来支持其他系统的访问来实现这一点。其中包括 rpc.mountd、rpc.nfsd 和

