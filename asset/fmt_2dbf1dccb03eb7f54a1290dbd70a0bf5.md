
默认情况下，如果服务器请求，PPP 将进行身份验证，除非它没有可以共享的密钥。如果没有密钥，PPP（或更具体地说，PPP 守护进程 `pppd`）将拒绝身份验证。你可能会在设置 PPP 连接时在这些文件中找到提供的用户名和密码。

# 第 16 章：连接到 701

`chap-secrets` 和 `pap-secrets` 格式是相同的。每行认证信息都可以包含客户端名称、服务器名称和密钥。服务器名称可以用 `*` 表示（以允许此密钥用于验证任何服务器）。如果你不知道服务器名称将是什么，这非常有用。此外，请记住大小写是敏感的（即 `Mister` 不等于 `myserver`）。

> **提示：** 有关更多关于 Linux 下 CHAP 和 PPP 的信息，请参阅 `pppd` 手页（输入 `man pppd`）。

在任何情况下，这里有一个 `chap-secrets` 文件的示例：

```
# secrets for authentication CHAP IP addresses
# client server secret
###### redhat-config-network 将覆盖此部分!!! (begin) ######
"abusername" "pppd0" "MySecretPassword"
```

**注意：** `pap-secrets` 和 `chap-secrets` 文件不应允许除 root 用户以外的任何人访问。任何获取此信息的任何人都可以使用它来访问您的 Internet 账户。默认情况下，对 root 用户以外的所有权限都是关闭的。（要设置权限，请使用 `chmod 600 /etc/ppp/-secrets`。）

# 查看 ifcfg 文件

你的 PPP 连接的 `ifcfg` 文件存储在包含你输入的服务提供商名称的文件中（例如 `/etc/sysconfig/network-scripts/ifcfg-ATT`）。该文件包含了传递给 `pppd` 守护进程的选项，用于与远程 PPP 服务器协商的功能。你的 PPP 连接可能发生的大多数问题都是由于某些选项设置错误（特别是请求了服务器无法或不愿提供的功能）。

以下是一个用于连接到 Windows PPP 服务器的 `ifcfg-???` 文件示例（在本例中命名为 `ifcfg-ATT`）：

```
DEVICE=ppp0
PROVIDER=ATT
MODEMPORT=/dev/ttyS0
LINES=115200
PAPNAME=guest
ONBOOT=yes
DEFROUTE=yes
DEMAND=yes
```

# 702 第四部分：Fedora RHEL 网络和服务器设置

设备名称为 `ppp0`。`PROVIDER` 是你分配给连接的名称（它与配置文件相关，例如 `ifcfg-ATT`）。`MODEMPORT` 是调制解调器连接的端口的设备名称（在本例中为 COM1）。`SPEED` 设置电脑与调制解调器之间的速度，单位为 bps（而不是拨号速度，拨号速度通常较）。`PAPNAME` 是你登录时使用的名称，假设你正在使用 PAP 认证。

`ONBOOT` 设置为 `yes` 以在启动时启动 `ppp` 守护进程（但尚未拨出，因为设置了 `DEMAND`）。`DEFROUTE=yes` 将默认路由设置到 PPP 连接。`DEMAND=yes` 会导致链路仅在存在流量时才被初始化。

> 提示：如果你想查看这些每个参数的具体选项，请查看 `/etc/sysconfig/network-scripts/if0-ppp` 脚本的内容。例如，如果 `DEFROUTE=yes`，则 `default` 选项被设置为 `ppp` 守护进程。请参阅 `ppp` 手页以获取每个选项的描述（输入 `man ppp`）。

你可以添加 `PPOPTIONS` 来列出任何想要传递给 `ppp` 守护进程的额外选项。在某些情况下，连接到某些类型的服务器时，ISP 将需要此文件中未包含的其他值。以下是一些不应出现在此文件中或应该（在某些情况下）出现在某些 Windows NT 服务器中的值建议。有关这些选项的描述，请参阅 `ppp` 手页：

- `remotename=remotename` —— 你可能在 PAP 认证需要此值，但在 CHAP 认证中不应输入它。（对于 CHAP，远程服务器为你服务。）

- `require-chap`, `require-pap`, `auth`, `noauth` — 要求 Windows NT 服务器进行自我认证是一个好主意（`require-chap` 和 `require-pap` 对其各自的协议所做的）。`auth` 值要求服务器在发送或接收数据包之前进行自我认证。我从权威渠道获，Windows NT 不允许你进行任何此类操作。认证将失败，你将无法建立连接。你可能需要通过 `noauth` 选项显式指示服务器不需要进行认证。

- `defaultasync` — PAP 可能会因为“链路透明度问题”导致认证失败。如果认证失败且你确定认证是正确的，请尝试此值。

- `ipcp-accept-local`, `ipcp-accept-remote` — 有时服务器会请求你的 IP 地址，即使它想自己分配一个。远程地址也是如此。尝试在选项文件中添加这几行：

# 第 16 章：连接到 Internet 703

```
192.168.0.1:192.168.0.2
ipcp-accept-local
ipcp-accept-remote
demand
```

这提供了本地和远程地址，并告诉远程服务器它可以替换这些值。与其使用私有 IP 地址（如下所示），你可以使用 `0.0.0.0` 代替

- `bsdcomp`, `deflate` —— Windows NT PPP 服务器不支持某些种类的压缩。因此，你不应该请求 BSD 压缩 (`bsdcomp`) 或 Deflate 压缩 (`deflate`)。在某些情况下，你可能想禁止这些类型的压缩：`nobsdcomp`, `nodelate` 和 `noccp`（用于无压缩控制协议）。

如前所述，`pppd` 选项描述的最佳地方是 `pppd` 手页。

# 运行调试

如果你的调制解调器工作正常，但你没有连接，要要做的事情是开启日志。如果已连接但没有任何应用程序似乎可以工作，检查你的 PPP 接口是否设置为默认路由。如果是，检查 `/etc/resolv.conf` 是否正确指定了 DNS 服务器。

从桌面进行此类调试最好，因为打开多个窗口很有帮助（我建议至少三个）。从第一个窗口，启动一个显示我们定义的日志内容的命令，以便调试信息进入：

```
tail -f /var/log/ppp
```

在下一个窗口，启动 PPP 接口。假设它是 `ppp0`，使用以下命令：

```
ifup ppp0
```

检查输出是否有通过 `/dev/modem` 建立的消息。

要将调试重定向到单独的文件，请向 `/etc/rsyslog.conf` 中添加这些行：

```
daemon.* /var/log/ppp
local2.* /var/log/ppp
```

之后，通过输入以下命令以 root 身份重启：

```
service rsyslog restart
```

# 704 第四部分：Fedora RHEL 网络和服务器设置

# 将你的 LAN 连接到 Internet

LAN 用户对你让他们共享文件和打印机感到高兴。在用户连接到 LAN 后，下一步是建立一个大家共享的 Internet 连接。此方法的优点是：

- 节省调制解调器 —— 无需每台电脑都有自己的调制解调器，你可以使用一个高速设备（如 DSL 路由器或电缆调制解调器）路由所有流量到 Internet。

- 节省电话线 —— 无需为每个想要访问 Internet 的人使用电话线，而是为你的 ISP 使用一条（在 DSL 的情况下，电话公司允许你在同一条电话线上同时传输模拟和高速数字数据）。

- 集中维护 —— 如果与 Internet 连接相关的信息发生变化（例如拨号或服务器地址），你可以在一个位置管理更改，而不是在每台电脑上都进行。

- 集中安全 —— 你可以控制进出的 Internet 流量。

本部分的程序假设你已经建立了第 15 章描述的 LAN。还假设你的 Linux 系统有一个到 Internet 的外部连接，LAN 电脑与 Internet 之间的所有流量都可以通过。该外部连接可能是拨号的，也可以通过另一个连接（到 DSL 路由器）或其他 LAN 卡。

- **作为路由器** — 通过将 Linux 配置为路由器，它可以将来自局域网（LAN）客户端的 IP 数据包通过拨号连接路由到互联网。

- **作为代理服务器** — 你可以将 Linux 配置为代理服务器。通过这种方式，局域网上的客户端计算机可以访问互联网，就好像连接是来自 Linux 计算机一样。

## 将 Linux 设置为路由器

有多种不同的方法可以设置从局域网到互联网的路由。你可以拥有一个专用的路由器，或者使用一台已经连接到局域网的计算机作为路由器。本节将描述如何将 Linux 作为路由器使用。

计算机可能具有多个网络接口，例如环回接口（`loopback`）、以太网局域网、到另一台计算机的直连线或拨号接口。客户端要使用路由器访问互联网，它在局域网上可能被分配一个私有 IP 地址。到路由计算机的连接将作为所有其他地址的网关。
