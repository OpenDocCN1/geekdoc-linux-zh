
```
# /etc/host.conf
order hosts, bind
multion on
```

`/etc/resolv.conf`

首先，此文件指定名称服务器的 IP 地址（关键字 `nameserver`）。`domain` 关键字确保了不完整的互联网名称（例如 `jupiter`）通过其域名进行扩展（变为 `jupiter.galactic.network`）。这主要是为了提高易用性，因为它允许以简写格式指定本地互联网名称。

```
# /etc/resolv.conf
domain galactic.network
search galactic.network
nameserver 192.168.1.2
```

除了上述文件外，还有无数其他 `/etc` 下的文件控制着各种网络和 Internet 网服务。然而，对于基础配置来说，更重要的是一些额外的配置文件，遗憾的是，这些文件取决于具体的发行版。以下是一些示例。

## RedHat

本地网络配置通过 `/etc/sysconfig/network-scripts` 中的脚本文件执行（另见第 131 页）。

```
# /bin/sh
# /etc/sysconfig/network-scripts/ifcfg-eth0
>>>设备类型: ethernet
>>>变量声明:
DEVICE=eth0
IPADDR=192.168.1.5
NETMASK=255.255.255.0
```

## 网络配置 177

`NETWORK=192.168.1.0`

`BROADCAST=192.168.1.255`

`GATEWAY=none`

`ONBOOT=yes`

`#>>>变量声明结束`

## SuSE

配置通过中心文件 `/etc/rc.config` 完成。以下列表显示了片段：

```
# /etc/rc.config 的片段
IPADDR_0=192.168.1.5
NETDEV=eth0
IFCONFIG_0="=192.168.1.5 broadcast 192.168.1.255 \
netmask 255.255.255.0"
NETWORK_0="-net 192.168.1.0"
GATEWAY_0=""
FQHOSTNAME=jupiter.galactic.network
NAMESERVER=""
```

## 配置一个带有 ftp 和 NFS 的小型网络

在某种意义上，这违背了本书将网络主题限制在客户端视角的意图。但在实践中，经常会出现两台或更多 Linux 计算机连接到网络，以至于它们可以轻松交换文件，我们将简要处理一个相当简单的微型网络的设置。必要的配置非常简单且易于遵循。

前提条件是计算机已经连接网络并按照上述描述进行了配置。对于所有计算机，必须使用相同的域名和广播地址。主机名和 IP 号必须单独设置，例如（使用三台计算机）：

- IP 地址：`192.168.1.5`, `192.168.1.6`, `192.168.1.7`
- 主机名：`jupiter`, `uranus`, `saturn`
- 通用域名：`galactic.network`
- 通用掩码：`255.255.255.0`
- 通用广播地址：`192.168.1.0`

下一步是向 `/etc/hosts` 插入你的 IP 地址以及另外两台计算机的 IP 地址。因此，在所有三台计算机上，该文件看起来完全一样：

```
# /etc/hosts
127.0.0.1         localhost
192.168.1.5       jupiter.galactic.network jupiter
192.168.1.6       uranus.galactic.network uranus
192.168.1.7       saturn.galactic.network saturn
```

这确保了计算机在重启或重新启动网络程序后可以立即相互访问。在 `ping` 命令中，你可以指定 IP 地址、全名，或短形式（`/etc/hosts` 中的第三列）。如果不起作用，请检查布线是否正确、所有计算机的内核是否都识别了以太网卡、以太网卡接口是否激活（`ifconfig`）以及路由表中是否连接了本地网络（`route`）。

```
root# ping uranus
PING uranus.galactic.network(192.168.1.56): 64 bytes of data
64 bytes from 192.168.1.1: icmp_seq=0 ttl=255 time=2.0 ms
64 bytes from 192.168.1.1: icmp_seq=1 ttl=255 time=1.2 ms
64 bytes from 192.168.1.1: icmp_seq=2 ttl=255 time=1.2 ms
<Str><++++anus.galactic.network ping statistics ---
3 packets transmitted, 3 packets received, 0% packet loss
round-trip min/avg/max = 1.2/1.4/2.0 ms
```

## FTP 服务器配置

`ftp` 是一种允许在计算机之间传输文件的协议。（客户端侧 `ftp` 的使用方法请见第 335 页。）

在大多数发行版中，`FTP` 服务器是自动安装的（通常是 `wuftpd`）。此时 `ftp` 应该可以立即工作——尝试执行 `ftp localhost`。要传输特定用户的文件，你需要执行 `ftp hostname`。随后，你输入用户名和密码。

如果没有安装 `FTP` 服务器，你需要在你的发行版中查找相应的包并安装它。为了让匿名 `FTP` 工作，你需要创建目录 `/home/ftp` 并向其中填充数据。为此，最好遵循 `ftp` 的 `man` 手册，其中包含了许多关于安全方面的细节。

出于安全考虑，`ftp` 不能用于无密码的登录。（我们指的是服务器端的登录名。你自己可以在没有密码的情况下登录，但你无法访问不受保护的外国账户数据。）此外，在 `/etc/ftpususers` 文件中，可以列出不允许使用 `ftp` 的用户。通常，出于安全考虑，`root` 会列在该文件中。

除了 `ftp` 之外，其他一些网络服务也应该可以立即工作：尝试 `telnet` 或 `login`。出于安全考虑，通常无法直接以 `root` 登录。先用另一个名称登录，然后执行。

## 访问控制

如果你想精确控制谁允许以及不允许使用哪些网络服务，你可以修改 `/etc/hosts.allow` 和 `/etc/hosts.deny` 文件。这些文件的语法为 `用户:服务`。

通过 `in.ftp:192.168.1.1`，`hosts.allow` 允许网络成员使用 `ftp`。通过 `ALL:ALL` `hosts.deny`，你拒绝对任何服务的访问。（此示例设置非常严格，因为它只允许了一个 IP。）

## 网络配置 179

```
# /etc/hosts.allow
in.ftp:192.168.1.1
# /etc/hosts.deny
ALL
```

在内部，访问控制通过 `tcpd` 执行。当请求某项服务时，`tcpd` 评估 `hosts.allow`，如果请求与模式匹配，则允许访问。如果没有找到任何内容，`tcpd` 会检查 `hosts.deny` 文件，如果找到匹配行，则拒绝访问。

```
# 来自 /etc/inetd.conf 的行
ftp stream nowait /usr/bin/tcpd in.ftp 192.168.1.1
```

## NFS 服务器配置

如果计算机的整个文件系统（或只是一个目录）要供其他计算机使用，该计算机必须配置为 `NFS` 服务器。`NFS` 配置在很大程度上独立于网络服务的配置。

大多数发行版都经过预配置，使得计算机可以自动用作 `NFS` 服务器。（如果不是，则需要安装 `portmap` 和 `nfs-server` 包。）

为了让 `NFS` 工作，必须启动 `rpc.portmap`、`rpc.mountd` 和 `rpc.nfsd`。这三个 `rpc` 程序是守护进程，它们共同提供了 `NFS` 服务器的服务。通过 `ps -x | grep` 可以确保这些守护进程正在运行。（在某些系统上，更安全的 `portmap` 代替 `rpc.portmap`。）

`/etc/exports` 文件控制哪些用户允许哪些目录以及（只读还是读写）。以下文件（安装在 Jupiter 计算机上）允许所有网络用户访问 `cdrom` 目录，允许 `uranus` 用户读取 `/usr/local`，允许 `saturn` 用户读取和写入目录（这显然构成了安全风险！）。

```
# jupiter计算机的 /etc/exports
/cdrom (ro)
/usr/local uranus(ro)
saturn(rw)
```

在客户端，不需要特殊配置。要挂载 `NFS` 文件系统，简单的 `mount` 命令即可。也可以在 `/etc/fstab` 中准备相应的条目（带有 `noauto` 选项！）。以下指令使 `/usr/local` 中 `uranus` 的所有文件在本地计算机 `/usr/local` 可用。这可以节省空间（因为该目录下的程序只需要在一台计算机上安装）。

```
root# mount -t nfs jupiter:/usr/local /usr/local
```
