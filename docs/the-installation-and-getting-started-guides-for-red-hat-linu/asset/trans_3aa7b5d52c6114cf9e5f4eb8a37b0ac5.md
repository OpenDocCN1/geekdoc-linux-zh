

- √ none — 不应使用任何启动时协议。
- √ bootp — 应使用 bootp 协议。
- √ dhcp — 应使用 dhcp 协议。

以下值适用于所有 PPP 和 SLIP 文件：

- **PERSIST**=*answer*，其中 *answer* 为以下值之一：
  - √ yes — 此设备应始终保持活动状态，即使在调制解调器挂断后被停用也是如此。
  - √ no — 此设备不应始终保持活动状态。
- **MODEMPORT**=*port*，其中 *port* 是调制解调器端口的设备名称（例如，`"/dev/modem"`）。
- **LINESPEED**=*baud*，其中 *baud* 是调制解调器的线路速度（例如，`"115200"`）。
- **DEFABORT**=*answer*，其中 *answer* 为以下值之一：
  - √ yes — 在创建/编辑此接口的脚本时插入默认中止字符串。
  - √ no — 在创建/编辑此接口的脚本时不插入默认中止字符串。

以下值适用于所有 PPP 文件：

- **DEFROUTE**=*answer*，其中 *answer* 为以下值之一：
  - √ yes — 将此接口设置为默认路由。
  - √ no — 不将此接口设置为默认路由。
- **ESCAPECHARS**=*answer*，其中 *answer* 为以下值之一：
  - √ yes — 使用预定义的 asyncmap。
  - √ no — 不使用预定义的 asyncmap。

（这表示一个简化接口；它不允许人们指定要转义的字符。不过，几乎任何人都可以使用 00000000 的 asyncmap，而且如果需要，也可以通过设置 PPPOPTIONS 来使用任意的 asyncmap。）

- **HARDFLOWCTL**=*answer*，其中 *answer* 为以下值之一：
  - √ *yes* — 使用硬件流控。
  - √ *no* — 不使用硬件流控。
- **PPPOPTIONS**=*options*，其中 *options* 是任意的选项字符串。它被放在命令行末尾，以便覆盖先前指定的其他选项（如 *asyncmap*）。
- **PAPNAME**=*name*，其中 *name* 用作 pppd 命令行中 `"name $PAPNAME"` 的一部分。请注意，`"remotename"` 选项总是被指定为逻辑 PPP 设备名称，例如 `"ppp0"`（如果之前启动了其他 PPP 设备，它可能实际上是物理设备 ppp1...），这使得管理 pap/chap 文件变得容易——名称/密码对与逻辑 PPP 设备名称关联，以便可以一起管理。原则上，不应该有任何东西阻止逻辑 PPP 设备名称使用 `"worldnet"` 或 `"myISP"` 而不是 `"ppp0"` — `"pppN"`。
- **REMIP**=*addr*，其中 *addr* 是远程 IP 地址（通常未指定）。
- **MTU**=*value*，其中 *value* 是用作 MTU 的值。
- **MRU**=*value*，其中 *value* 是用作 MRU 的值。
- **DISCONNECTTIMEOUT**=*value*，其中 *value* 表示在成功连接的会话终止后、重新建立连接之前等待的秒数。
- **RETRYTIMEOUT**=*value*，其中 *value* 表示在一次尝试失败后、再次尝试建立连接之前等待的秒数。

`/etc/sysconfig/network-scripts/chat-<interface-name>` — 此文件是用于 PPP 或 SLIP 连接的聊天脚本（chat script），旨在建立连接。对于 SLIP 设备，会根据聊天脚本编写一个 DIP 脚本；对于 PPP 设备，则直接使用聊天脚本。

`/etc/sysconfig/network-scripts/dip-<interface-name>` — 这个只写脚本由 netcfg 根据聊天脚本创建。不要修改此文件。将来，此文件可能消失，而是会根据聊天脚本即时创建。

## /etc/sysconfig/network-scripts/ifup-post

当任何网络设备（SLIP 设备除外）启动时，会调用此文件。它会调用 /etc/sysconfig/network-scripts/ifup-routes 来启动依赖于该设备的静态路由。为该设备启用别名。如果尚未设置主机名，并且可以找到该设备 IP 对应的主机名，则设置主机名。向任何请求网络事件通知的程序发送 SIGIO。可以根据需要扩展此文件，以修复名称服务配置、调用任意脚本等。

## /etc/sysconfig/network-scripts/ifdhcpcd-done

一旦 dhcp 配置完成，dhcpcd 就会调用此文件；它根据 dhcpcd 放置在 /etc/dhcpcd/resolv.conf 中的版本来设置 /etc/resolv.conf。

## System V 初始化

本节简要描述启动过程的内部机制。它详细介绍了机器如何使用 SysV init 启动，以及旧版 Linux 发行版中使用的 init 与 SysV init 之间的差异。init 是内核在启动时运行的程序。它负责启动所有需要在启动时运行的常规进程。这些进程包括允许你登录的 getty 进程、NFS 守护进程、FTP 守护进程，以及你希望在机器启动时运行的任何其他程序。SysV init 正迅速成为 Linux 世界中控制启动时软件启动的标准。这是因为它比传统的 BSD init 更易于使用，而且更强大、更灵活。SysV init 与 BSD init 的不同之处还在于，配置文件位于 /etc 的子目录中，而不是直接位于 /etc 中。这个目录称为 rc.d。在那里你会找到 rc.sysinit 和以下目录：

- init.d
- rc0.d
- rc1.d
- rc2.d
- rc3.d
- rc4.d
- rc5.d
- rc6.d

