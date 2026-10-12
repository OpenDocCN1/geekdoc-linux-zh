
- `IPADDR`—代表 PVC 的点对点链路中你侧的 IP 地址。

- `NETMASK`—两个路由器之间网络的子网掩码。（更多信息请参阅第 5.3.4 节。）

- `POINTPOINT`—你 PVC 另一端路由器的 IP 地址。你的对方应该具有相同但反转的值。

- `GATEWAY`—如果指定，则将用于配置默认路由的网关地址。

## 5.3.4 使用零节点网络节省时间

当我开始部署帧中继时，链路几乎已完全配置，但仍然存在为接口配置 IP 地址以实现与 PVC 另一端点对点连接的问题。如果你习惯其他帧中继路由器的配置，可能会认为这一步是可选的。从理论上讲，你不需要为每个帧中继接口分配 IP 地址——帧中继云知道如何路由你的数据包（基于 DLC 和 PVC）。然而，当你使用 `WANPIPE` 时，你需要为每个 PVC 的末端分配 IP 地址。这是因为内核在路由方面将这些接口视为任何其他点对点接口，并用 `ifconfig` 显示其属性。

每个 PVC 都会被分配一个 IP 地址，而 PVC 本身可以被视为一个只有两个节点的网络。（事实上，你可以通过指定 255.255.255 的子网掩码来配置点对点链路。请参阅第 5.3.4 节关于 `/etc/wanpipe/interfaces/` 中的名称，或者查看非 Debian 系统的 `/usr/lib/router/interfaces/`。这里有一个示例文件，这意味着 `/etc/wanpipe/interfaces/wan0` 和 `/etc/wanpipe/interfaces/wan1`。

通过查看文件，你会发现：

```
DEVICE=wan0
ONBOOT=yes
IPADDR=192.168.20.2
NETMASK=255.255.255
POINTOPOINT=192.168.20.3
GATEWAY=
```

该文件由启动脚本加载，这意味着文件必须遵循基本的 Bourne 语法。（实际上你不需要太担心语法，因为 `wancfg` 会为你创建文件）。参数如下：

- `DEVICE`—设备名称。

- `ONBOOT` [yes 或 no]—这可以在启动时临时禁用接口，而无需将其从 `wanpipe1.conf` 中删除。否则，它应该为 yes。

- `IPADDR`—代表 PVC 的点对点链路中你侧的 IP 地址。

- `NETMASK`—两个路由器之间网络的子网掩码。（更多信息请参阅第 5.3.4 节。）

- `POINTPOINT`—你 PVC 另一端路由器的 IP 地址。你的对方应该具有相同但反转的值。

- `GATEWAY`—如果指定，则将用于配置默认路由的网关地址。

(c) 在 `$WAN_DRIVERS` 中加载模块。检查该模块是否已经加载（失败）。`$modprobe` 的结果会在日志文件中记录为 ok（成功）或 fail（失败）。如果 `$WAN_DRIVERS` 为空字符串，脚本将自动失败。

(d) 调用 `ifconfig` 并将 `wanpipe1.conf`（以及其他文件）作为参数。这是 `$interfaces` 中的接口被创建的节点。

(e) 查找 `$IFCONF_DIR` 以提取每个接口的配置。当 `wanconfig` 创建接口并成功地向内核注册它时，在 `/proc/net/dev` 中会创建一个条目。脚本会检查 `$IFCONF_DIR` 下的每个接口文件；当它在 `/proc/net/dev` 中找到匹配项时，它会调用该接口的 `interface.up`。

(f) `interface.up` 读取接口文件（前文第 5.3.3 节讨论过），并使用其中的值通过 `$IPADDR`、`$NETMASK` 和 `$POINPOINT` 地址来配置接口。

(g) 使用 `route.5` 为 `$POINPOINT` 接口向内核路由表添加一条主机路由。

(h) 通过 `$GATEWAY` 添加一个默认网络路由（如果其已设置）。

## WANPIPE—加载模块

现在我们已经知道了应该发生什么，我们可以谈谈可能出现问题的地方。驱动模块的加载必须进行。如果模块不在 `/lib/modules/version/net` (2.2 内核) 或 `/lib/modules/version/kernel/net` (2.4 内核) 中，或者不是为正确内核编译的，你就必须采取一些纠正措施。

- 在第一种情况下，也许你忘记了执行内核修正的最后一步 `modules_install`。可能是因为你构建了内核，但自内核编译以来没有运行 `depmod`。`depmod` 通常在系统启动时运行，确保其运行的一种方法是重启系统。这也会纠正第二个问题，只要你从 `lilo` 写入内核的同一个地方启动系统即可（你是在使用 `make zlilo` 编译内核吗？）。当模块加载时，`lsmod` 的输出应该看起来像适用于 2.2.x 内核的 `WANPIPE` 模块：
