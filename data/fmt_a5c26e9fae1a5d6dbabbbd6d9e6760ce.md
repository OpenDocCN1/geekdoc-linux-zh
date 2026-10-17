
如果你更喜欢手动操作而不是预配置 `pptp-command`，从命令行操作也足够简单。你必须使用 `pptp-command` 或手动方法配置 CHAP 密钥。

要启动会话，你需要 PPTP 服务器的外部 IP 地址和你的 PPTP VPN 名称（即 `/etc/ppp/peers/` 中的文件名）。然后如下调用 `pptp`：

```
wildcat# call bears.example.com
```
你必须手动添加网络路由并在需要时修改 `/etc/resolv.conf`，因为这些通常由 `pptp-command` 为你处理。

要停止 VPN，假设它使用设备 `ppp1`，你可以如下杀死 `pppd` 进程：

```
wildcat# kill /var/run/ppp1.pid
```

# 高级 pptp-command 选项

`pptp-command` 脚本有一些额外的功能，可以让你从菜单界面，让生活更轻松。

## 选择默认 PPTP 隧道

如果你想偷（所有的 Linux 管理员都应该是这样），你可以设置默认 PPTP 连接。这将允许你在不进入 `pptp-command` 管理系统的情况下启动和停止默认 PPTP 连接。

启动 `pptp-command` 并进入选择默认隧道菜单：

- 1.) Chicago

- 2.) Atlanta

- 3.) cancel

你想让哪个隧道成为默认?: 1

然后你可以如下从从命令行启动隧道：

```
wildcat# pptp-command start
```

或类似地停止它：

```
wildcat# pptp-command stop
```

## 创建通用的 `/etc/pptp.d` 配置文件

如果你是 PPTP 服务器管理员并且有许多想要连接的用户，你可以通过向他们提供 `pptp-command` 配置文件来让他们更容易配置 PPTP。该文件存放在 `/etc/pptp.d` 中将预加载用户配置。例如，如果在亚特兰大和芝加哥都有 PPTP 服务器，我们可以创建如下 `pptp-command` 配置文件：

```
# PPTP 连接定义。格式：
# PPTP_tunnel_name IP_ADDRESS
# route command
# route command
# ...
```

```
Chicago 208.8.8.8
add -net 192.168.1.0/24 TUNNEL_DEV
add -net 192.168.2.0/24 TUNNEL_DEV
```

```
Atlanta 270.7.7.7
add -net 192.168.1.0/24 TUNNEL_DEV
add -net 192.168.2.0/24 TUNNEL_DEV
```

```
# 你需要这一行来表示我们现在正在定义
# 名称服务器
# 名称服务器定义写在这里。
```

# 安装 pptpd

PPTP 服务器软件被称为 `pptpd`，这是一个我们由衷钦佩的机智双关语（pun）。它是为 Linux 构建的，但可以在 Solaris 等其他 Unix 类操作系统上运行。它本质上是一个守护进程，接受入站的 PPTP 连接并派生自身的副本来处理 TCP 控制通道和 GRE 数据包，同时将数据交给 PPP 以处理实际的点对点链路、身份验证和加密。

要安装 `pptpd`，请从 `http://poptop.lineo.com` 获取源码包并将其解压：

```bash
# root tar xzv pptpd-VERSION.tar.gz
# root cd pptpd-VERSION
```

`pptpd` 附带了一个配置脚本，用于选择编译时的设置。以下是一些比较实用的命令行选项：

- `--prefix=DIR` 将软件安装到 DIR 而不是 `/usr/local`

- `--with-libwrap` 包含对 TCP Wrapper 支持

- `--with-pppd-ip-alloc` 允许 `pppd` 分配固定 IP 地址

- `--with-slirp` 使用 SLIRp 代替 `pppd`（后文将详细介绍）

我们通常这样配置 `pptpd`：

```bash
#root /config --prefix=/opt/pkgs/pppd --with-libwrap \
--pppd-ip-alloc
```

这会将 `pptpd` 程序存放在 `/opt/pkgs/pppd` 并使用 TCP Wrappers。

遗憾的是，没有可以选的配置选项来更改 `pppd` 查找二进制文件的默认位置。如果你之前将其安装在非标准位置，则需要修改 `config.h` 文件中的以下行（该文件由你的 `./config` 命令生成），以反映正确的位置：

```c
/* 问的 pppd 在哪里？ */
#define PPP_BINARY "/usr/sbin/pppd"
```

在在本章稍前的安装示例中，我们将 `pppd` 安装在 `/opt/pkgs/pppd-mppe` 目录下，这意味着我们需要按所示修改前面的行：

```c
#define PPP_BINARY /opt/pkgs/ppp-mppe/usr/sbin/pppd
```

完成任何自定义后，只需编译并安装软件即可：

```bash
# root make
# root install
```

## 什么是 TCP Wrappers？

TCP Wrappers 允许你根据 `/etc/hosts.deny` 和 `/etc/hosts.allow` 中定义的规则，控制哪些机器允许连接你的 PPTP 服务器。TCP Wrappers 是大多数服务器软件的一个选项。更多信息请参阅 `hosts.allow` man 手页。

# 构建 PPTP VPN 服务器

## 为 pptpd 安装 ppp-mpe

`pptpd` 将经过 GRE 封装的 PPP 数据交给你本地的 `pppd` 命令。该程序必须支持用于身份验证和加密的微软扩展。

处理此问题的首选软件是 `ppp-mpe`。它是标准 PPP Linux 软件的补丁版本，包含了额外的位位，并与 OpenSSL 配合使用加密算法。在本章之前讨论 PPTP 客户端时，我们已经介绍过 `ppp-mpe` 的安装。请按照此处描述的方法安装 `ppp-mpe`。

## PPTPd 和 SLIRP

我们提到的 `pptpd` 配置选项之一是 `--slirp`。SLIRP 是一个 TCP/IP 模拟器，它本质上允许你将普通的 shell 账户转换为一个完整的 SLIP/PPP 账户。（在 PPP 流行之前，SLIP 是调制号器拨号的首选协议。）

你可以使用 SLIRP 代替使用 `ppp-mpe` 软件包中的 `pptpd` 程序。`ppp-mpe` 需要 Linux 内核模块，使其具有特定的 Linux 特性，而 SLIRP 更具跨平台性。因此，如果你想在 Solaris 上运行 PPTP 服务器，SLIRP 将是一个值得考虑的选择。

然而，我们建议你坚持使用 `ppp-mpe`，原因如下：

- SLIRP 不再维护了。

- `ppp-mpe` 的版本包含了微软的身份验证和加密扩展，而 SLIRP 则没有。

```bash
# 这些选项仅在您应用了
# 可选 pppd-mppe 补丁后可用
require-mppe
require-mppe-stateless
#chapms-strip-domain
```

```bash
# 帮助 Windows 查找其
# 网络设置的一些选项。根据需要替换 IP。
ms-dns IP.AD.DR.ES
ms-wins IP.AD.DR.ES
```

```bash
# 支持入站连接所需的
# 标准选项。参见我们在第 3 章中对 ppp 选项的讨论
proxyarp
lock
...
```

## 设置 chap-secrets 文件

PPTP VPN 远程用户的密码存储在服务器的 `/etc/ppp/chap-secrets` 中。该文件包含客户端名称（用户名）、服务器名称、密钥（密码）以及其他 IP 地址。`pptp` 程序通过参数 `pptp` 调用 `pppd`，`/etc/ppp/chap-secrets` 中的第二个字段必须是 `pptp`。一个示例文件可能如下：

| Client | Server | Secret | IP Address |

|---|---|---|---|

| reegen | pptp | littleWildc&7 | |

| bree | pptp | dämNc/t3 | 10.1.0.201 |

在此示例中，Reagen 将从 `/etc/ppptd.conf` 中设置的范围内获取一个 IP 地址。如果您在编译 `pptpd` 时使用了 `-with-pppd-ip-alloc` 选项，Bree 将始终获得静态地址 `10.1.0.201`；否则，她也将从 `/etc/ppptd.conf` 中的范围中获取一个随机 IP 地址。

> 不要忘记 NT 域名

如果您没有应用 `strip-Msdomain-patch`，则您需要将 NT 域名作为用户名的一部分提供。假设您的域以及 Reagen 使用的是发送域名的 Windows 机器，第一行应该读如下：

```
CHICAGO\rengen pptp 1!littleWildc&
```

## 启动 pptpd

启动 `pptpd` 只需要运行以下命令：

`bear-pppdserver pptpd`

`ppptd` 作为守护进程运行，这意味着它可以处理多个入站连接。对于每个成功的连接，有两个进程来处理 VPN：

```bash
bearS$ ps -ef | egrep pptpd|ppptd
root      23201 1 04:43 ?      00:00:00 /usr/sbin/ppptd
root      2024 23201 04:43 ?      00:00:00 pptpd [IP,AD.DR,ES]
root      2025 2024 04:43 ?      00:00:00 /usr/sbin/ppppd local file
/etc/pptp/ppptd-options ....
```

第一个进程仅仅是 `pptpd` 守护进程，它监听额外的连接。第二个 `pptpd` 进程是 GRE/PPP 封装/解封装器。最后，`pppd` 处理 VPN 的加密和网络层。如果您想杀死特定的 VPN 连接，只需杀掉相关的 `pppd` 进程即可。

您可以通过从 Linux 发行版中复制模板在 `/etc/init.d` 中创建一个启动/停止脚本。如果您想要一个极其通用的脚本，只需将以下内容保存为 `/etc/init.d/ppptd`：

```bash
#!/bin/sh

# 替换为您的 pptpd 程序的实际路径
PPTPD=/opt/pkgs/ppptd/sbin/ppptd

case "$1" in
start)
	echo "Starting PPTPD Daemon"
	PPTPD
	echo "ppptd."
	;
stop)
	echo "Stopping PPTPD Daemon"
	kill cat /var/run/ppptd.pid
	;
restart)
	echo "Restarting PPTPD Daemon"
	sh $0 stop; sh $0 start
	;
*)
	echo "Usage: /etc/init.d {start|stop|restart}"
	exit 1
	;
esac
```

然后简单地将其链接到启动时运行。例如，如果您启动到 init 状态 2，您可能想执行以下操作：

```bash
bears-ppptserver# ln -s .../init.d/ppptd /etc/rc2/S99ppptd
```

`ppptd` 服务器将在启动时始终启动，并在重启前停止。您可以使用以下两个命令手动启动或停止服务器：

```bash
bears-ppptserver# /etc/init.d/ppptd start
bears-ppptserver# /etc/init.d/ppptd stop
```

# 226 第 7 章 PPTP

此脚本在停止 `pptpd` 守护进程本身时会停止所有现有的 PPTP VPN 连接。如果您只想停止特定的 VPN，请杀死与其相关的 `pppd` 进程。

## 故障排除

由于 PPTP VPN 包含许多部分，您可能会发现自己陷入许多棘手的的境地。

### PPTP 模块未加载

PPP 和 PPTP 工作必须加载几个模块。尝试建立 PPTP 连接并检查可加载模块列表：

```bash
# lsmod
Module Size Used by
mppe 22240 0 (unused)
ppd_deflate 40180 2 (autoclean)
bsd_comp 3852 0 (autoclean)
ppp 21036 2 (autoclean) [mppe pppd_deflate bsd_comp]
slhc 4440 1 (autoclean) [ppp]
```

将会加载其他模块，但这些是 PPTP 作为 VPN 运行所需的。`mppe` 模块不是由您的 Linux 发行版提供的，但它在本章之前已编译。其余部分可能是预装的。如果您的内核在编译时支持 PPP 而不是作为可加载模块（这不太），您将会在 `lsmod` 输出中看到最后四个模块。

参考本章前面的“PPP 内核模块”部分以确保您正确安装了所需的模块。如果您未能更新 `/etc/modules.conf` 或运行 `depmod -a`，您可能会遇到加载新模块的问题。

### 启用调试

您可以通过将要修改的文件添加到 PPTP 程序的选项列表中来强制额外的调试。

```
/etc/ppp/options For pppd (client and/or server)
```

## 实现非标准 VPN 协议

- 8 VTun

- cIPe

- tinc

### 8 VTun

VTUN，或 VIRTUAL TUNNEL（虚拟隧道），是由 Maxim Krasnyansky 编写的一种 VPN 解决方案。使用 VTun 构建的 VPN 使用隧道接口，数据在进入隧道时被加密，在从隧道远端退出时解密。下一节将提供 VTun 的概述。关于 VTun 编译、配置、故障排除和兼容性的章节将完成本章的其他内容。

#### VTun 概述

隧道是一种逻辑连接，通过这种连接，两个设备似乎是直接连接的。隧道的工作原理是数据包封装。数据包封装是将数据包放入另一个数据包中的过程。在 VTun Case中，封装是对路由通过隧道接口的数据包执行的。VTun 将数据包封装在 IP 数据包中，并使用 IP 网络将这些封装后的数据包从隧道的一侧路由到另一侧。隧道接口是进入隧道连接的逻辑入口，在隧道连接的两侧创建。隧道的每侧都包含关于对端的信息，例如可达的网络地址以及其之外的网络。这样，当一个发往隧道远端之外网络的的数据包进入服务器时，它将通过本地隧道接口进行路由。如前所述，内核随后封装此数据包，并将此新数据包转发到隧道远端的已知地址。到达隧道远端后，数据包将经过检查、解封装，然后转发到其原始目的地。

图 8.1 展示了隧道传输的数据包封装过程。主机 `192.168.1.10` 向 VTun 机器 `280.8.8.8` 发送数据包。VTun 服务器将该数据包封装在另一个数据包中，以 `280.8.8.8` 为源 IP 地址，`270.7.7.7` 为目的 IP 地址。当 `270.7.7.7` 的客户端接收到数据包时，将对其进行检查和解封装。这将数据包恢复到原始状态——即源 IP 再次变为 `192.168.1.10`，目的 IP 回到 `192.168.2.15`。

VTun 允许两个服务器建立连接并协商隧道参数，VTun 允许两个服务器使用 TCP 或 UDP 作为底层传输来创建隧道。

除了正常的隧道行为外，VTun 还引入了新的增强功能。VTun 支持数据加密，使任何窃听者无法确定封装数据包的内容。VTun 还支持压缩，使数据包在进入隧道时被压缩，到达隧道端点时解压缩。最后，流量整形（traffic shaping）是 VTun 实现的一项功能，用于对隧道连接进行限流，以为优先级流量保留带宽。

VTun 支持多种类型的隧道。关于每个隧道类型特定配置任务的更多信息将在本章的“VTun 配置”部分进行讨论。

#### VTun 组件及其功能

VTun 有两个主要组件：Linux 内核 TUN/TAP 驱动程序和 `vtun` 守护进程。TUN/TAP 内核驱动用于创建隧道接口，而 `vtun` 用于本地到远程隧道连接的设置和维护。

##### TUN/TAP 驱动程序

TUN/TAP 驱动用作隧道的逻辑访问点。换句话说，路由到驱动程序的数据包被发送到隧对端。反之亦然；从驱动程序读取的数据包是从隧道对端发送到本地侧的。驱动程序包含两个部分：虚拟接口和设备文件。

虚拟接口充当隧道的入口。当数据包发送到 Linux 服务器时，根据每个数据包的节点字段做出路由决策。`vtund` 列出发送到这些接口的数据包，并根据需要封装或解封装数据包。如果数据包的目标是隧道远端，VTun 将将数据包封装在 IP 中并将其转发到隧道端点。如果数据包的目标是本地网络，数据包将被解封装并转发到相应的本地接口。TUN 驱动使用格式为 `xtun` 的 IP 接口命名，其中 X 是唯一标识该隧道接口的数字。在本章的其余部分，将约定将 IP 虚拟接口称为 `tun`。

为 TUN/TAP 接口配置的 IP 地址还允许路由将发往远程网络的流量指向该本地接口。本地接口在逻辑上连接到通往远程网络的下一跳。

为了为隧道远端的网络创建路由表项，必须为每个隧道接口配置 IP 地址。对于每个隧道连接，远程和本地隧道接口被配置在相同的网络中，就像点对点链路一样。这维持了跨隧道网络仅一跳之遥的幻。

此示例路由表显示了通过隧道接口发送数据包的路由情况。使用此路由表，我们将检查通过隧道接口路由数据包的过程。
