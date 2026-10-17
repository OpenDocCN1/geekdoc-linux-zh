
如果 `ping` 命令显示网络上的可用，你就可以继续。

## 使用 TCP/IP 配置文件

网络配置工具可以帮助你，但你可能想直接编辑配置文件。例如，`/etc/hosts` 文件包含主机名。

### /etc/hosts

`/etc/hosts` 文件包含 IP 地址和名称的列表。以下是 `/etc/hosts` 示例：

```
# 这样的行是注释。

127.0.0.1       localhost

192.168.0.1     localhost933

192.168.0.2     localhost200

192.168.0.3     localhost60

192.168.0.4     localhost40

192.168.0.5     localhost25
```

### /etc/networks

另一个包含网络名称和 IP 地址的文本文件是 `/etc/networks`。这些网络名称被。

### /etc/host.conf

Linux 使用解析库获取主机名的 IP 地址。`/etc/host.conf` 指定了如何解析名称。典型的 `/etc/host.conf` 可能包含以下行：

- `order hosts, bind`
- `multi`

`order` 选项指示了顺序。示例条目指定解析库应首先检查 `/etc/hosts` 文件，然后检查名称服务器。

`multi` 选项决定 `/etc/hosts` 中的主机是否可以有多个 IP 地址。

### /etc/hosts.allow

此文件指定了哪些主机允许使用运行在你系统上的 Internet 服务（如 Telnet）。正如“理解 xinetd 配置文件”章节所解释的，TCP wrapper 在启动 Internet 服务之前会查询 `/etc/hosts.allow` 文件。只有当 `hosts.allow` 中的条目表明请求主机允许使用服务时，它才会启动该服务。

`/etc/hosts.allow` 中的条目采用 `server:IP address` 格式，其中 `server` 指提供特定 Internet 服务的程序名称，`IP address` 指标识允许在本地网络（C 类网络 192.168.0.0）访问 Telnet 服务（由 `in.telnetd` 程序提供）的主机。请在 `/etc/hosts.allow` 中添加以下行：

```
in.telnetd:192.168.0.0.
```

如果您想允许所有主机访问所有 Internet 服务，可以使用 `ALL` 关键字并将该行重写为：

```
ALL:ALL.
```

最后，若要向所有主机开放所有 Internet 服务，您可以将 IP 地址替换为 `ALL`，如下：

```
ALL:ALL
```

您也可以使用主机名代替 IP 地址。

要学习 `/etc/hosts.allow` 文件条目的详细语法，可以在 Linux 提示符下输入 `hosts.allow`。

### /etc/hosts.deny

此文件是 `/etc/hosts.allow` 的相反——`hosts.allow` 指定哪些主机可以访问系统上的 Internet 服务（如 TELNET 和 FTP），而 `hosts.deny` 文件则标识必须被拒绝的主机。正如“理解 xinetd 配置文件”章节所解释的，如果 TCP wrapper 在 `/etc/hosts.allow` 文件中没有找到请求主机的规则，将查询 `/etc/hosts.deny` 文件。如果 TCP wrapper 在 `hosts.deny` 文件中找到适用于主机的规则，将拒绝服务。

`/etc/hosts.deny` 中的条目与 `/etc/hosts.allow` 文件格式相同——均采用 `server:IP address` 格式，其中 `server` 指提供特定 Internet 服务的程序名称，`IP address` 指允许使用该服务的主机。

如果您已经在 `/etc/hosts.allow` 文件中设置了条目以允许访问特定主机，则可以在 `/etc/hosts.deny` 中放置以下行，以拒绝所有其他主机访问系统上的任何服务：

```
ALL:ALL
```

## 第6章：网络设置

要学习 `/etc/hosts.deny` 文件条目的详细语法，请在 Linux 提示符下输入 `man hosts.deny`。

### /etc/nsswitch.conf

此文件称为名称服务切换（NSS）文件，指定了服务（如名称解析库、NIS、NIS+ 以及本地配置文件如 `/etc/hosts` 和 `/etc/shadow`）如何相互作用。GNU C Library 版本 2 (`glibc 2`) 或更新版本的 Linux 依赖 `/etc/nsswitch.conf` 文件来确定优先级：是本地配置文件还是 DNS 或 NIS 等服务（参见第18章了解更多关于 DNS 和 NIS）。

例如，`/etc/nsswitch.conf` 文件中的 `hosts` 条目指定解析库应首先尝试 `/etc/hosts` 文件，然后尝试 NIS+，最后是 DNS：

```
hosts: files dns
```

您可以在终端窗口中输入 `info "Name Switch@dp"` 来了解更多关于 `/etc/nsswitch.conf` 的信息。

### 启动时配置网络

您希望在每次启动系统时自动启动网络。为了实现这一点，您必须将相应的命令放在一个或多个启动脚本。该过程在 Linux 启动后立即运行。该过程查询 `/etc/init.ab` 并根据当前的运行级别执行各种命令（通常是 shell 脚本）。例如，在运行级别 3（多用户级别）中，`etc/init.ab` 指定应运行参数为 3 的脚本文件 `/etc/rc.d/`。

> 在运行级别 3 和 5 中，启动脚本会执行 `/etc/rc.d/init/network` 脚本来激活所有网络接口。如果您查看 `/etc/rc.d/init/network` 文件，会发现网络初始化使用的是 `/etc/sysconfig` 目录下的另一组文件。网络激活脚本需要 `/etc/sysconfig/network` 文件中定义的变量来决定是否激活网络。在 `/etc/sysconfig/network` 中，您将看到如下行：
> `NETWORKING=yes` 只有当 `NETWORKING` 变量设置为 `yes` 时，网络才会被激活。`/etc/sysconfig/network` 文件中的另一个变量——`HOSTNAME`——定义了系统主机名。`HOSTNAME` 的默认设置为如下：
> `HOSTNAME=localhost.localdomain`

## 第一部分：安装 Linux

`/etc/rc.init.d/network` 脚本反而执行 `/etc/sysconfig/network/scripts` 目录中的若干脚本来激活特定的网络接口。例如，要激活太网接口 `eth0`，将执行 `/etc/sysconfig/network-scripts/ifup` 脚本并使用 `/etc/sysconfig/network-scripts/ifcfg-eth0` 文件。以下是一个典型的 `/etc/sysconfig/network-scripts/ifcfg-eth0` 文件内容：

```
DEVICE=eth0

BOOTPROTO=dhcp

HWADDR=00:2C:76:F4:38:B3

ONBOOT=yes

TYPE=Ethernet
```

如您所示，此文件包含网络设备名称以及太网卡的硬件地址。`BOOTPROTO=dhcp` 行指定应通过动态主机配置协议 (DHCP) 获取网络接口的 IP 地址。`ONBOOT` 变量表示 Linux 启动时是否激活此接口。

要激活接口 `eth0`，将执行 `/etc/sysconfig/network-scripts/ifup` 脚本并使用 `/etc/sysconfig/network-scripts/ifcfg-eth0` 文件。以下是一个典型的 `/etc/sysconfig/network-scripts/ifcfg-eth0` 文件内容：

```
DEVICE=eth0

BOOTPROTO=dhcp

HWADDR=00:2C:76:F4:38:B3

ONBOOT=yes

TYPE=Ethernet
```
