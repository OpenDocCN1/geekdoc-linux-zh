
# 网络管理：ifconfig

| 选项 | 说明 |
| - | - |
| `-a` | 显示所有接口的状态，即使是关闭（down）的接口。 |
| `ADDRESS` | 要配配给 `INTERFACE` 的 IP 地址。 |
| `allmulti` 或 `-allmulti` | 启用或禁用“全组播”模式。如果选择，`INTERFACE` 将接收网络上的所有组播数据包。 |
| `arp` 或 `-arp` | 启用或禁用 `INTERFACE` 上的 ARP 协议。 |
| `[-]broadcast [ADDRESS]` | 如果提供了 `ADDRESS` 参数，则设置此接口的广播地址。否则，设置或清除接口的 `IFF_BROADCAST` 标志。 |
| `down` | 禁用 `INTERFACE`。 |

## 227

| 选项 | 说明 |
| --- | --- |
| `-dstaddr ADDRESS` | 设置点对点链路的远程 IP 地址。此关键字已过，已被 `pointopoint`（点对点）取代。 |
| `hw CLASS ADDRESS` | 如果设备驱动支持此操作，则设置接口的硬件地址。`CLASS` 是硬件类的名称。目前支持的硬件类包括 `ether`（以太网）、`ax25`（AMPR AX.25）、`ARCnet` 和 `netrom`（AMPR/ROM）。`ADDRESS` 是硬件地址的可打印 ASCII 等效值。 |
| `io_addr ADDRESS` | 设置设备 I/O 空间的起始地址。 |
| `irq ADDRESS` | 设置设备使用的中断线。 |
| `media TYPE` | 设置设备使用的物理端口或介质。并非所有设备都能更改此设置，且其支持的值也因设备而异。`TYPE` 的典型值为 `10base2`（细以太网）、`10baseT`（双绞线 10Mbps 以太网）、`AUI`（电子收发器）等。`auto` 特殊介质类型可指示驱动程序自动感介质。 |
| `mem_start ADDRESS` | 设置设备使用的共享内存的起始地址。 |
| `metric N` | 设置 `INTERFACE` 的度量（Metric）。此参数未实现，但为了兼容性仍被接受。 |
| `mtu N` | 设置 `INTERFACE` 的最大传输单元（MTU）。 |
| `multicast` | 设置接口上的组播标志。通常不需要，因为驱动程序会正确地设置该标志。 |
| `netmask ADDRESS` | 设置 `INTERFACE` 的 IP 网络掩码。此值默认为常用的 A 类、B 类或 C 类网络掩码（派生自接口 IP 地址），但可以设置为任何值。 |
| `[-]pointoint [ADDRESS]` | 启用接口的点对点模式，这意味着它是两台机器之间的直接链路，没有人在监听。如果还提供了 `ADDRESS` 参数，则设置链路另一侧的协议地址。否则，它将清除接口的 `IFF_POINTPOINT` 标志。 |
| `promis` 或 `-promisc` | 启用或禁用 `INTERFACE` 的“混杂”模式。如果选择，接口将接收网络上的所有数据包。 |
| `txqueelen LENGTH` | 设置设备的发送队列长度。对于高延迟设备（调制解调器链路和 ISDN 链路），设置较小的值很有用，可以防止快速批量传输减慢 telnet 会话和其他交互流量。 |
| `up` | 激活 `INTERFACE`。如果为接口分配了地址，则此操作是隐含。 |

# 网络管理：ripquery

## 228

### ripquery

`ripquery [-n] HOST`

`ripquery` 可以从远程 `HOST` 请求内核路由表的列表。远程主机必须运行 RIP 服务器才能处理请求。`-n` 选项可抑制 IP 地址到名称的解析。

## route

```
route [-CFvnee]
route [-v] [-A FAMILY] add OPTION ...
route [-v] [-A FAMILY] del
route [-version] [-help]
```

`route` 用于管理内核路由表。它可以为特定的主机或网络添加或删除路由。它通过显示路由表来管理路由。

| 选项 | 说明 |
| --- | --- |
| `-A FAMILY` | 指定路由地址族。目前有效的族值包括 `inet`、`ddp`、`ipx`、`netrom` 和 `ax25`。 |
| `-C` | 显示路由表。 |
| `-F` | 显示 FIB。 |
| `-h` | 显示帮助信息。 |
| `-n` | 抑制 IP 地址到名称的解析。 |
| `-v` | 详细输出。 |
| `add OPTION ...` | 添加路由。 |
| `del` | 删除路由。 |

# 网络管理：mount 和 rpc.mount

| 选项 | 说明 |
| :--- | :--- |
| `-d` or `--debug` | 将每个事务详细地记录到标准错误输出。默认情况下，除非 `mount` 在前台运行，否则日志输出将发送到 `syslog`。 |
| `-F` or `--foreground` | 给定此选项时，`mount` 将从终端运行。如果请求了调试，输出将发送到标准错误。 |
| `-f FILE` or `--exports-file FILE` | 使用 `FILE` 代替 `/etc/exports`。 |
| `-h` or `--help` | 提供帮助总结。 |
| `-n` or `--allow-non-root` | 允许传入的挂载请求，即使它们并非源于 root IP 端口也能被处理。 |
| `-P PORTNUM` or `--port PORTNUM` | 监听端口 `PORTNUM`。默认情况下，`mount` 将监听 `/etc/services` 中的 `mount/udp` 端口。如果未定义，它将使用某些随机端口 1024。 |
| `-p` or `--promiscuous` | 为网络上的任何主机提供服务。 |
| `-r` or `--re-export` | 允许导入的 NFS 或 SMB 文件系统被导出。 |
| `-v` or `--version` | 当前版本号。 |

# nfsd 和 rpc.nfsd

`rpc.nfsd OPTION ... [ NUMPIES ]`

`nfsd` 是一个 NFS 服务守护进程，用于处理客户端文件系统请求。与某些其他系统不同，`nfsd` 作为普通的用户级进程运行。该服务器与其他 NFS 服务器实现不同之处在于，它挂载了整个文件层次结构，不受物理文件系统边界的限制。该实现允许客户端对服务器的文件层次结构具有只读或读写访问。

`nfsd` 通常在启动时启动。它也可以由 `inetd` 调用。通过在 `/etc/inetd.conf` 中添加以下两行可以启用：

```
nfs/2 dgram rpc/udp wait root /usr/sbin/rpc.nfsd rpc.nfsd
nfs/2 stream rpc/tcp wait root /usr/sbin/rpc.nfsd rpc.nfsd
```

`NUMPIES` 允许并行运行多个 `nfsd` 实例。如果 `NUMPIES` 大于 1，`nfsd` 将派生（fork） `NUMPIES - 1` 次。由于服务器不共享共同的文件句缓存，当使用此选项调用时，`nfsd` 将禁止所有操作。

`nfsd` 还支持 WebNFS 协议。WebNFS 是 NFS 的扩展，允许通过 Web 浏览器检索文件。为了支持此功能，`-R` 或 `--public-root` 选项是相对的。公共根目录也必须在 `/etc/exports` 中命名。

# 网络管理：showmount

## 23

| 选项 | 说明 |
| :--- | :--- |
| `-d FACILITY` or `--debug FACILITY` | 详细地记录操作。`FACILITY` 的当前合法值为：`call` 用于 RPC 调用和参数，`fcache` 用于文件句柄操作，`auth` 用于身份验证程序，以及 `uid` 用于 UID 映射代码。除非守护进程在前台运行，否则调试消息将记录到 `syslog`。 |
| `-F` or `--foreground` | 使用此选项时，`nfsd` 不会脱离终端。 |
| `-f FILE` or `--exports-file` | 从 `FILE` 而不是从 `/etc/exports` 读取访问权限。 |
| `-h` or `--help` | 提供简要总结。 |
| `-l` or `--log-transfers` | 对于每个文件的存储或检索，都会向系统日志守护进程写入一行，包含客户端的 IP 地址和文件名。这些传输记录的日志级别为 `daemon.info`。 |
| `-n` or `--allow-no-root` | 允许 NFS 请求即使并非源于 IP 端口也能被处理。某些 NFS 客户端实现需要此项。某些较新的 NFS 客户端实现不使用端口检查。可以通过在 `/exports` 中指定 `insecure` 导出选项来为单个主机关闭此检查。 |
| `-P PORTNAME` or `--port PORTNAME` | 让 NFS 监听端口 `PORTNAME` 而不是默认端口 2049 或 `/etc/services` 中指定的 `nfs/udp` 端口。 |
| `-p` or `--promiscuous` | 将服务器处于混杂模式，它将为网络上的任何主机提供服务。 |
