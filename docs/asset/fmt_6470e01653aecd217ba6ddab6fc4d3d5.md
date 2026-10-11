
```
Address Type Recv-Q Send-Q Inode Conn Refs Nexthref Addr
b8be00 stream 0 0 a19000 0 0 0 /tmp/.AgentSo*
red000 dgram 0 0 c99000 0 0 0 /opt/dcelocal
cebe00 dgram 0 0 d21000 0 0 0 /opt/dcelocal
bd2020 dgram 0 0 b87000 0 0 0 /opt/dcelocal
bd3700 dgram 0 0 b84800 0 0 0 /opt/dcelocal
b24e00 dgram 0 0 b84000 0 0 0 /opt/dcelocal
d54400 dgram 0 0 b84000 0 0 0 /var/tmp/gph_
d85c00 dgram 0 0 be7000 0 0 0 /var/tmp/gph_1
c8b200 dgram 0 0 b21000 0 0 0 /opt/dcelocal
c8c440 stream 0 0 b78400 0 0 0 /opt/dcelocal
b80300 dgram 0 0 b78000 0 0 0 /opt/dcelocal1
b5c090 dgram 0 0 d22400 0 0 0 /opt/dcelocal
cc8c00 dgram 0 0 ba1000 c4a180 c32e80 0 /opt/dcelocal
tbe190 dgram 0 0 9a4400 0 0 0 /opt/dcelocal
d6a100 stream 0 0 9a4800 0 0 0 /opt/dcelocal
bc5600 dgram 0 0 cc0000 d4d940 0 0 /opt/dcelocal1
c44200 dgram 0 0 cf8000 c32c80 0 0 /opt/dcelocal1
cfd800 dgram 0 0 d24000 c12000 0 0 /opt/dcelocal1
CE5e00 stream 0 0 c1b000 0 0 0 /opt/dcelocal
D1dd00 dgram 0 0 ca8400 0 0 0 /opt/dcelocal1
cf8c00 dgram 0 0 a92800 a15bc0 0 /opt/dcelocal7
d2d600 dgram 0 0 a93800 c13200 0 ddbb80 /opt/dcelocal
c98e00 dgram 0 0 a93800 0 0 0 /opt/dcelocal
06a800 stream 0 0 ba3000 0 0 0 /var/opt/GW/SI
```

此输出包含大量信息。你可以参考 HP-UX 系统上的在线手册页。

第一行显示 `Proto` 为 `tcp`，`Local Address` 为 `system1.telnet`，状态为 `ESTABLISHED`。这是我们要对该系统发起的连接。我们位于 `system1` 上，并且有一个到运行 `netstat` 命令的系统的 `telnet` 会话处于打开状态。

其余大部分 `tcp` 协议条目均处于监听状态。这意味着它们正在监听传入连接，如 `LISTEN` 所示。它们在 `Foreign Address` 字段中有一个通配符，一旦连接建立，该字段将包含对应的地址。如 `ESTABLISHED` 所示，我们是少数已建立连接的其中之一。

所有发送和接收队列（显示为 `Recv-Q` 和 `Send-Q`）均为空，如 `0` 所示。

输出末尾的 UNIX 域套接字是 NFS 等多种服务的流和报文连接。

此输出让你能够了解你的 UNIX 系统在网络视角下正在发生的巨大活动量。自 UNIX 诞生以来，网络与连接一直是其最先进的方面之一。

### route

`netstat` 显示的信息是你系统的路由表。其中一些是在系统启动或网络接口初始化时，通过 `ifconfig` 命令自动创建的。到未直接连接到你的系统的网络和主机的路由，是通过 `route` 命令输入的。

可以即时进行路由更改，就像我将标志从 `U` 更改为 `UG` 那样：

```
/usr/sbin/route add default 128.185.61.1 3
```

首先是 `route` 命令。其次，我们指定要添加一条路由；另一个选项是删除一条路由。第三，我们指定目标，在此例中是默认目标。这可能是一个特定的主机名、网络名、`IP` 地址，或者表示通配网关路由的 `default`（如我们的示例所示）。第四是到达目标所使用的网关。在上述示例中，使用的是 `IP` 地址，但也可以使用主机名。`3` 对应于用于指定网关是本地主机还是远程网关的计数。如果网关是本地主机，则使用计数 `0`。如果网关是远程主机（如示例中的情况），则使用计数 `>0`。这对应于 `Flags` 中的 `UG`。这通过添加具有适当 `Flags` 的默认路由，手动更改了网络路由表。执行此命令解决了我遇到的问题，即让 `system1` 与路由器另一侧的系统进行通信（回想图 13-11）。

在执行带有 `add` 选项的 `/usr/sbin/route` 之前，你可以先使用 `delete` 选项来移除现有的不工作的默认路由。

`route` 命令通常出现在系统的某个启动文件中，以便每次系统启动时都会发出 `route` 命令。这确保了每次系统启动时都有正确的连接信息就位。

### ifconfig

`ifconfig` 命令提供有关 LAN 接口的额外信息。

以下示例提供了网络接口的配置：

```
/etc/ifconfig lan0
lan0:	flags=863<UP,BROADCAST,NOTRAILERS,RUNNING>
	inet 128.185.61.2 netmask ffff0000 broadcast 128.185.61.255
```

从这个例子中，我们可以快速看出接口已启用，地址为 `128.185.61.2`，并且网掩码为 `ffff0000`。再次请注意，你的网络接口可能有不同的名称，例如 `leo`。

你可以使用 `ifconfig` 获取网络接口的状态，就像我在这里所做的那样，为网络接口分配地址，或配置网络接口参数。你拥有的网络地址属于“ A ”、“ B ”或“ C ”类，如前所述。在开始配置你的 LAN 接口之前，务必确定你的网络类别。此示例是一个“ B ”类网络，因此网掩码定义为 `ffff0000`（这是“ B ”类地址的典型值），而不是 `ffff00`（这是“ C ”类网络的典型值）。网掩码用于确定保留多少地址来将网络细分为较小的网络。网掩码可以表示为十六进制（如上所示）或十进制格式（如 `/etc/hosts` 文件中所示）。以下是我发出的用于配置接口的 `ifconfig` 命令：

```
/etc/ifconfig lan0 inet 128.185.61.2 netmask 255.255.0.0
```

- `255.255.0.0` 对应于前面针对“ B ”类子网掩码显示的十六进制 `ffff0000`。
- `lan0` 是正在配置的接口。
- `inet` 是地址族，目前是该系统唯一支持的地址族。
- `128.185.61.2` 是系统 1 的 LAN 接口地址。
- `netmask` 显示如何细分网络。
- `255.255.0.0` 等同于 `ffff0000`，这是“ B ”类地址的网掩码。

我很好地利用了 `netstat`、`ping` 和 `ifconfig` 来帮助获取网络状态。如果你需要识别任何需要进行的更改，可以使用 `ifconfig`、`route` 和 `/etc/hosts` 来配置网络。子网示例展示了在配置网络以满足当前和未来需求时，你可以多么灵活。在简单网络中，你可能不需要使用这些命令中的许多或复杂的子网划分。在复杂网络中，或者在遇到配置困难时，你可能必须广泛使用这些命令。在任何情况下，网络规划都是设置 UNIX 系统的重要组成部分。

本章中使用的大多数命令是每个系统管理员工具箱的一部分。然而，网络对于 UNIX 系统的使用至关重要，因此在该领域拥有背景知识有助于你更全面地理解系统以及如何更有效地使用它。

### rpcinfo

作为用户，你可能需要在另一系统上挂载 NFS 目录，或执行一些你以前未在你的系统上执行过的其他功能。你可以通过评估系统中正在运行的守护进程来确定各种功能是否已启用。`rpcinfo` 允许你通过在系统上（包括本地系统）发出命令 `rpc -p system_name` 来生成远程过程调用 (`RPC`)。

以下示例显示在我们的本地系统上发出 `rpcinfo -p`：
