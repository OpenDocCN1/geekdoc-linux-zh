
```bash
# cat /etc/rc.config.d/netconf
# netconf: 核心网络子系统的配置值

# @(#)B.11.11_LR $Revision: 1.6.119.6 $ $Date: 97/09/10 15:56:01 $

# HOSTNAME: 用于 uname -s 和 hostname 的系统名称
# OPERATING_SYSTEM: uname -s 返回的操作系统名称
# ---- 请勿更改此值 ----
# LOOPBACK_ADDRESS: 回环地址
# ---- 请勿更改此值 ----
#
# 重要提示：在 9.x 到 10.0 的迁移过程中，不要在
# 下一组语句之间插入空行

HOSTNAME="cvhdcn4"
OPERATING_SYSTEM=HP-UX
LOOPBACK_ADDRESS=127.0.0.1

# 互联网配置参数。参见 ifconfig(1m), autopush(1m)
#
#INTERFACE_NAME:  网络接口名称（参见 lanscan(1m)）
#
#IP_ADDRESS:
       主机名（在 /etc/hosts 中）或点分十进制
       表示的 IP 地址（例如，192.1.2.3）
#
#SUBNET_MASK:     点分十进制表示的子网掩码，如果与默认值不同
                  则使用此值
#
#BROADCAST_ADDRESS: 点分十进制表示的广播地址，如果
                    与默认值不同则使用此值
#
#INTERFACE_STATE: 启动时所需的接口状态。
                  可以是 up 或 down，默认为 up。
#
#DHCP_ENABLE:
       决定是否在网络接口上启用 DHCP 客户端功能
       （参见 auto_parms(1M), dhclient(1M)）。DHCP 客户端
       从 DHCP 服务器获取 IP 地址分配。
       1 启用 DHCP 客户端功能，0 禁用它。
#
# 对于每个额外的网络接口，添加一组类似下面的变量赋值，
# 将索引更改为 [1]、[2] 等。
#
# 重要提示：在 9.x 到 10.0 的迁移过程中，不要在
# 下一组语句之间插入空行

INTERFACE_NAME[0]=lan1                <--  lan1
IP_ADDRESS[0]=172.16.14.44
SUBNET_MASK[0]=255.255.255.0
BROADCAST_ADDRESS[0]=255.255.255.255
INTERFACE_STATE[0]=""
DHCP_ENABLE[0]=0

# 互联网路由配置。参见 route(1m), routing(7)
#
#ROUTE_DESTINATION: 目标主机名（在 /etc/hosts 中）或主机或网络
                   点分十进制 IP 地址，前面加上单词
                   "host" 或 "net"，或者简单地使用单词 "default"。
#
#ROUTE_MASK:      点分十进制表示的子网掩码，或 0（C 语言
                  十六进制表示）。这是一个可选字段。
                  IP 地址和子网掩码对能唯一标识
                  要到达的子网。如果未给出子网掩码，
                  则系统将为该路由分配已配置网络接口中
                  最长的子网掩码。
                  如果没有匹配的子网掩码，则系统
                  将分配默认网络掩码作为该路由的
                  子网掩码。
#
#ROUTE_GATEWAY:   网关主机名（在 /etc/hosts 中）或点分
                  十进制 IP 地址。本地接口必须使用
                  上述 IP 地址所使用的相同格式（localhost 或
                  点分十进制表示）。如果是回环接口，即
                  127.0.0.1，则必须将 ROUTE_COUNT 设置为零。
#
#ROUTE_COUNT:     一个整数，表示网关是
                  远程接口（1）还是本地接口（0）
                  或回环接口（例如 127.*）。
#
#ROUTE_ARGS:      路由命令的参数和选项。此变量
                  可以包含以下参数的组合：
                  "-r", "-n" 和 "-p "per"。
#
# 对于每条额外的路由，添加一组类似下面的变量赋值，
# 将索引更改为 [1]、[2] 等。
#
# 重要提示：在 9.x 到 10.0 的迁移过程中，不要在
# 下一组语句之间插入空行

# ROUTE_DESTINATION[0]=default
# ROUTE_MASK[0]=0.0.0.0
# ROUTE_GATEWAY[0]="172.16.14.1"
# ROUTE_COUNT[0]="1"
```

# 虚拟分区主机相关信息

```
# ROUTE_ARGS[0]=""

# 动态路由守护进程配置。参见 gated(1m)
# GATED: 设置为 1 以启动 gated 守护进程。
# GATED_ARGS: 传递给 gated 守护进程的参数。

GATED=0
GATED_ARGS=""

# 路由器发现协议守护进程配置。参见 rdpd(1m)
# RDPD: 设置为 1 以启动 rdpd 守护进程

RDPD=0

# 逆 ARP 守护进程配置。参见 rarpd(1m)
# RARP: 设置为 1 以启动 rarpd 守护进程

RARP=0

ROUTE_GATEWAY[0]=172.16.14.1
ROUTE_COUNT[0]=1
ROUTE_DESTINATION[0]=default
```

我们也可以在 SAM 中查看和配置与网络相关的信息。图 13-1 展示了 SAM 中第二个 vPar（*cable2*）上 *lan1* 的与网络相关的信息：

![](img/eff8b9287a5f38c5adf538f24aacf29e_857_0.png)

这些窗口显示了我们之前在各个文件和命令行中查看到的信息。一些系统管理员更喜欢在 SAM 中修改和查看信息，而另一些则更喜欢在命令行中操作。

### 使用两张网卡配合 Telnet

分配给虚拟分区的局域网卡可以像在非 vPar 系统上那样用于多种用途。当两个不同 vPar 中的用户或应用程序进行通信时，它们是通过局域网进行的。在正常操作中，vPar 并没有为通信提供任何特殊的机制。（然而，vPar 之间确实存在特殊的系统管理通信，例如虚拟分区数据库的同步，这是以特殊方式进行的。）当在两个 vPar 之间建立通信会话时，即使它们位于同一台服务器上，也会使用两个 vPar 上的局域网接口。这包括 `telnet`、`ftp` 以及 Berkeley 的“r”命令，如 `rlogin`。以下示例展示了书中许多示例中使用的两个 vPar 之间的 `telnet` 会话。在此示例中，vPar `cable1`（主机名 `cvhdcon3`）发起与 vPar `cable2`（主机名 `cvhdcon4`）的 `telnet` 会话：
