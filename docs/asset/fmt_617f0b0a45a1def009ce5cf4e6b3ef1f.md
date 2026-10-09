
为了防止他人向你的系统发起任何访问，创建一个规则，使用 `state` 选项配合 `NEW` 来阻止外部通过 `SYN` 数据包进行的访问。任何丢弃

# 第14章：防火墙

`eth0` 接口上的连接（假设只有 `eth0` 连接到互联网或外部网络）。

## 防止并避免主动发起的连接

`iptables -A INPUT -m state --state NEW -i eth0 -j DROP`

`iptables -A FORWARD -m state --state NEW -i eth0 -j DROP`

## 本地网络访问

为了允许内部网络通过防火墙发起连接，你允许来自内部以以太网连接 `eth1` 的所有数据包的输入。有效的内部网络地址被指定为输入源：

`iptables -A INPUT ACCEPT -p all -i eth1 -s 192.168.0.0/24`

## 列出规则

这些 `iptables` 选项的列表显示了每个选项的不同规则，如下所示：

```
# iptables -L (policy DROP)
Chain INPUT (policy ACCEPT)
target prot opt source destination
LOC all -- !!192.168.0/24 anywhere LOG level warning
DROP all -- !!192.168.0/24 anywhere
DROP all -- !!192.168.0.24 anywhere
DROP all -- 127.0.0/8 anywhere
ACCEPT all -- anywhere tcp dpt:http
ACCEPT tcp -- 10.0.0.2 anywhere state RELATED, ESTABLISHED
ACCEPT tcp -- 192.168.0.0/24 state RELATED, ESTABLISHED tcp spt:http
ACCEPT icmp -- anywhere icmp echo-reply state RELATED, ESTABLISHED
DROP all -- anywhere state NEW
ACCEPT all -- 192.168.0/24 anywhere icmp echo-reply
ACCEPT icmp -- 10.0.0.1 icmp echo-request
ACCEPT icmp -- 10.0.0.1 icmp destination-unreachable
Chain FORWARD (policy ACCEPT)
target prot opt source destination
DROP all -- !!192.168.0/24 anywhere
DROP all -- !!192.168.0/24 anywhere
DROP all -- 127.0.0/8 anywhere
DROP all -- anywhere state NEW
```

```
Chain OUTPUT (policy ACCEPT)
target prot opt source destination
DROP tcp -- anywhere 192.168.0.0/24 state NEW tcp spt:http
```

```
# iptables -t nat -L
Chain PREROUTING (policy ACCEPT)
target prot opt source destination
Chain POSTROUTING (policy ACCEPT)
target prot opt source destination
MASQUERADE all -- anywhere
```

## 第二部分：安全

Chain OUTPUT (policy ACCEPT)

target prot opt source destination

## 用户定义规则

对于复杂的规则，你可能想要创建自己的链以减少重复。一种常用方法是为 `INPUT` 和 `FORWARD` 链都定义用户链，这样你就不需要为每个链重复 `DROP` 操作。相反，你将只有一个用户链，`FORWARD` 和 `INPUT` 链都会将其发送到该用户链进行 `DROP` 操作。请记住，除了共享的规则外，`FORWARD` 和 `INPUT` 操作都有各自的规则。在接下来的示例中，创建了一个名为 `arriving` 的用户定义链。该链在脚本顶部通过 `-N` 选项定义：

`iptables -N arriving`

用户链在被用作其他规则的目标之前必须先定义。你必须首先定义并添加该链的所有规则，然后将其用作目标。首先定义 `arriving` 链并添加其规则，在文件末尾，它被用作 `INPUT` 和 `FORWARD` 链的目标。`INPUT` 链列出了接受数据包的规则，而 `FORWARD` 链具有 `ACCEPT` 策略，默认将接受它们。

```
iptables -N arriving
iptables -F arriving
# IP 欺骗，拒绝内部网络上任何具有外部源地址的数据包
iptables -A arriving -j LOG -i eth0 ! -s 192.168.0.0/24
iptables -A arriving -j DROP -i eth0 ! -s 192.168.0.0/24
iptables -A arriving -j DROP ! -i eth0 -s 192.168.0.0/24
```

```
# 脚本结束目
iptables -A INPUT -j arriving
iptables -A FORWARD -j arriving
```

相应的规则列表显示在此：

Chain INPUT (policy DROP)

target prot opt source destination

arriving all -- 0.0.0.0/0 0.0.0.0/0

Chain FORWARD (policy ACCEPT)

target prot opt source destination

arriving all -- 0.0.0.0/0 0.0.0.0/0

Chain arriving (2 references)

target prot opt source destination

LOG all -- 192.168.0.0/24 0.0.0.0/0 LOG flags level 4

DROP all -- 192.168.0.0/24 0.0.0.0/0

DROP all -- 192.168.0.0/24 0.0.0.0/0

对于可能有所不同的规则，你仍然需要确保有独立的规则。在 `myfilter` 脚本中，`FORWARD` 链具有 `ACCEPT` 策略，允许所有转发到本地网络的数据包通过防火墙。如果 `FORWARD` 链具有 `DROP` 策略（像 `INPUT` 链一样），那么你可能需要定义单独的规则让 `FORWARD` 可以接受数据包。`INPUT` 链列出了接受数据包的规则，而 `FORWARD` 链具有 `ACCEPT` 策略，默认接受它们。

## 第14章：防火墙

在你的系统上进行伪装（masquerading）。在使用 IP 伪装之前，内核必须支持 IP 伪装。

在 Linux 系统上实现的 IP 伪装使得具有 Internet 地址的机器同时成为使用防火墙 Internet 地址连接互联网的局域网的防火墙和网关。实现 IP 伪装的防火墙有时被称为 `MASQ` 网。通过 IP 伪装，连接互联网的系统（防火墙）会监听来自其局域网主机的请求。当它收到请求时，它会将请求的本地主机 IP 地址替换为防火墙的 Internet IP 地址，然后将请求发送到互联网，就像是它自己一样。来自互联网的回复将发送到防火墙系统。防火墙的回复使用其 Internet 地址指向防火墙。然后防火墙确定响应的是哪个本地系统的请求。它剥离自己的 IP 地址并通过局域网将响应发送给本地主机。从本地机器的角度来看，这种连接是透明的。它们似乎是直接连接到互联网的。

### 局域网伪装

IP 伪装通常用于允许私有网络或小型局域网（例如小型企业）上的机器访问互联网。此类网络可能只有一台机器可以访问互联网，因此只有一个 Internet 地址。本地私有网络将从私有网络分配的范围内选择 IP 地址（10.、172.16. 或 192.168）。理想情况下，防火墙有两个网卡：一个用于连接局域网的接口（例如 `eth1`），另一个用于连接互联网的接口，例如 `eth0`（用于拨号上网 ISP）。用于互联网的网卡（`eth0`）将被分配 IP 地址。本地网络的以太网接口（`eth1`）——你的私有局域网将有一个网络地址 `192.168.0.0`。其以太网接口（`eth1`）将被分配 IP 地址 `192.168.0.1`。实际上，防火墙接口被配置为伪装所有来自私有网络的数据包。你的局域网需要有自己的域名服务器，用于识别你网络上的机器，包括你的防火墙。每台本地机器都需要将防火墙指定为其网关。不要在同一个物理接口上对防火墙和 Internet 地址使用 IP 别名（aliasing）。请为它们使用单独接口，例如两块以太网卡，或一块以太网卡和一个调制解调器（`ppp0`）。

### 伪装 NAT 规则

在 Netfilter 中，IP 伪装是一种 NAT 操作，不像 IP Chain 那样与数据包过滤集成。伪装命令放置在 NAT 表上，并与数据包过滤命令分开处理。使用 `iptables` 在 NAT 表上放置伪装规则。首先，使用 `-t nat` 选项引用 NAT 表。在 `POSTROUTING` 链上添加规则，使用 `-o` 选项指定输出设备，并使用 `-j` 选项配合 `MASQUERADE` 命令。

```bash
iptables -t nat POSTROUTING -o eth0 -j MASQUERADE
```

### IP 转发

下一步是开启 IP 转发，可以手动开启，也可以通过设置 `/etc/sysctl.conf` 文件中的 `net.ipv4.ip_forward` 变量并运行带有 `-p` 选项的 `sysctl`。

## 第二部分 安全

如果要默认启用转发。对于 IPv6，使用 `net.ipv6.conf.all.forwarding`。示例选项所示：

```bash
sysctl -w net.ipv4.ip_forward=1
sysctl -w net.ipv6.conf.all.forwarding=1
```

然后你运行带有 `-p` 选项的 `sysctl`：

```bash
sysctl -p
```

你可以使用所示的 `echo` 命令直接更改相应的转发文件：

```bash
echo 1 > /proc/sys/net/ipv4/ip_forward
echo 1 > /proc/sys/net/ipv6/conf/all/forwarding
```

对于 IPv6，你将使用对应 `/proc/sys/net/ipv6` 目录下的 `conf/forwarding` 转发文件：

```bash
echo 1 > /proc/sys/net/ipv6/conf/all/forwarding
```

### 伪装选定主机

与其将所有本地主机伪装成防火墙网关的单一 IP 地址，你可以使用 NAT 表为少数选定的主机重写地址。这种方法通常应用于多个本地主机作为 Internet 服务器的设置。使用 `DNAT` 和 `SNAT` 标记，你可以将数据包定向到特定的本地主机。你会使用 `PREROUTING` 和 `POSTROUTING` 链上的规则来重定向输入和输出数据包。

例如，上一个中的 Web 服务器可以配置为本地主机，`DNAT` 目标可以重定向任何原始从 `10.0.0.2` 接收的数据包。假设 Web 服务器设置在 `192.168.0.5` 上。它在互联网上显示的地址 `10.0.0.2` 将被 NAT 表重写并重定向到 `192.168.0.5`。你会使用带有 `-d` 选项的 `PREROUTING` 链处理入站连接，并使用带有 `-s` 选项的 `POSTROUTING` 链处理输出数据包。

```bash
iptables -t nat -A PREROUTING -d 10.0.0.2 --to-destination 192.168.0.5 -j DNAT
iptables -t nat -A POSTROUTING -s 192.168.0.5 --to-source 10.0.0.2 -j DNAT
```

# 第15章：文件系统 367

文件系统将其文件组织在自己的目录树中。你可以将其想象为一个必须挂载到主目录树的子树。在专门你连接它之前，该树与你系统的目录树保持分离状态。例如，一个带有 Linux 文件的软磁盘有它自己的目录树。你需要将此子树挂载到你硬盘分区的主树上。在挂载之前，你无法访问软磁盘上的文件。

| 目录 | 功能 |
| :--- | :--- |
| `/` | 文件系统结构的起点——称为根目录 (root) |
| `/boot` | 存放内核镜像文件以及相关的启动信息和文件 |
| `/home` | 包含用户的家目录 |
| `/sbin` | 存放管理级命令以及 root 用户使用的任何命令 |
| `/dev` | 存放用于如终端和打印机等设备的动态生成文件接口（参见第 17 章中的“udev：设备文件”） |
| `/etc` | 存放系统配置文件以及任何其他系统文件 |
| `/etc/opt` | 存放 `/opt` 中应用程序的系统配置文件 |
| `/etc/X11` | 存放 X Window 系统及其应用程序的系统配置文件 |
| `/bin` | 存放基本的用户命令和实用程序 |
| `/lib` | 存放基本的共享库和内核模块 |
| `/lib/modules` | 存放内核模块 |
| `/media` | 用于存放挂载基于介质的可移动式文件系统的目录，如 CD-ROM、软磁盘、USB 读卡器和数码相机 |
| `/mnt` | 用于存放额外文件系统（如硬盘）的目录 |
| `/opt` | 存放添加的软件应用程序（例如某些发行版中的 KDE） |
| `/proc` | 进程目录，一个内存驻留的目录，包含用于提供系统信息的文件 |
| `/sys` | 用于内核对象的 sysfs 文件系统，列出了支持的内核设备和模块 |
| `/tmp` | 存放临时文件 |
| `/usr` | 存放系统使用的文件和命令；此目录分为若干个子目录 |
| `/var` | 存放变化的文件，如邮件邮箱、Web 和 FTP 文件 |

表 15-1：Linux 文件系统目录

## 文件系统层次结构标准 (FHS)

Linux 将其文件和目录组织成一个整体的互连树，从根目录开始一直延伸到系统和用户目录。系统目录的组织和布局由文件系统层次结构标准 (FHS) 决定。`FHS` 提供了一个标准化的布局，所有 Linux 发行版在设置系统目录时都遵循该标准。

例如，必须有一个 `/etc` 目录来存放配置文件，以及一个 `/dev` 目录用于存放设备文件。你可以在 `http://www.pathname.com/fhs` 了解更多关于 `FHS` 的信息，包括官方文档。Linux 发行版、开发者和管理员遵循 `FHS`，以为 Linux 文件系统提供一致的组织结构。

Linux 使用了一系列具有特定名称的目录来执行专门的行政/管理任务。所有这些目录都位于你主 Linux 文件系统的顶层，即文件根目录，用单个斜杠 `/` 表示。例如，`/dev` 目录存放设备文件，`/home` 目录存放家目录以及你所有的用户文件。你只有在系统管理员身份下才能访问这些目录和文件（尽管用户通常只有读权限）。你需要以 root 身份登录（使用 `su` 命令，或在运行级别 3 下作为 root），将自己置于一个特殊的 root 管理目录 `/root/` 中。从这里，你可以访问 Linux 文件系统上的任何目录，无论是管理目录还是用户目录。

## 根目录：/

根目录 `/` 下的子目录列表 15-1所示，以及其他常用的子目录。你作为管理员经常访问的目录包括 `/etc` 目录（存放配置文件）、`/dev` 目录（存放动态生成的设备文件）以及 `/var` 目录（存放 DNS、Web、邮件和 FTP 服务器服务器数据，以及系统日志和计划任务）。为了管理不同版本的内核，你可能还需要访问 `/boot` 和 `/lib/modules` 目录以及 `/usr/src/`。`/boot` 目录存放你安装的新内核的内核镜像文件，而 `/lib/modules` 目录存放适用于你不同内核的模块。

> 提示：在 Linux 中，你可以挂载不同类型的文件系统，包括由其他操作系统（如 Windows、Unix 和 OSX）创建的文件系统。Linux 支持多种文件系统，包括 ReiserFS 和 ext3 等几种日志文件系统。

## 系统目录

你的 Linux 目录树包含某些目录，其中的文件被用于不同的系统功能。对于基本的系统管理，你应该熟悉存放应用程序的系统程序目录、存放大多数配置文件的系统配置目录 (`/etc`) 以及存放记录系统活动日志的系统日志目录 (`/var/log`)。表 15-2 列出了这些系统目录。

### 程序目录

名称中带有 `bin` 的目录用于存放程序。`/bin` 目录存放基本用户程序，如登录、shell (`BASH`、`TCSH` 和 `zsh`) 以及文件命令 (`cp`、`mv`、`rm`、`ln.` 等)。`/sbin` 目录存放用于此类任务的专门系统程序，如文件系统管理 (`fsck`、`fdisk`、`mkfs`) 以及关机和启动 (`init`) 等操作。`/usr/bin` 目录存放为用户任务设计的文件。`/usr/sbin` 目录存放相关的系统操作，例如用于添加新用户的 `useradd`。`/lib` 目录存放你用到的所有库，包括主 Linux 库 `libc` 以及 `modules` 等子目录（`modules` 存放了所有当前内核模块）。它还将存放一些系统控制的配置文件，如 `/lib/udev`。

| 目录 | 描述 |
| :--- | :--- |
| `/bin` | 系统相关程序 |
| `/sbin` | 用于专门任务的系统程序 |
| `/lib` | 库文件 |
| `/etc` | 配置文件，用于用户帐户、应用程序、服务器或网络连接 |
| `/home` | 用户目录 |
| `/media` | 可移动媒体文件系统 |
| `/var` | 变量文件 |
| `/usr` | 程序 |
| `/usr/bin` | 用户可用程序 |
| `/dev` | 设备文件 |
| `/sys` | sysfs 文件系统 |
