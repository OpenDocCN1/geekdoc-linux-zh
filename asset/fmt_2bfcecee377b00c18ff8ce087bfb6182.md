
- `DONGLE=value`，`value` 指定用于红外通信的适配器（Dongle）的类型。此设置适用于使用适配器而非真实红外端口的用户。适配器是连接到传统串口上通过红外通信的设备。此行默认被注释掉，因为带有真实红外端口的笔记本电脑比带有额外适配器的电脑常见得多。

- `DISCOVERY=value`，`value` 为以下布尔值之一：

  - `yes` — 以发现模式启动 `irattack`，意味着它会主动检查其他红外设备。需要开启此项以便机器能够主动寻找红外连接（即不主动发起连接的一端）。
  - `no` — 不以发现模式启动 `irattack`。

## `/etc/sysconfig/kernel`

`/etc/sysconfig/kernel` 文件包含内核参数。这些参数在启动时传递给内核。

## `/etc/sysconfig/keyboard`

`/etc/sysconfig/keyboard` 文件控制键盘行为。可以使用以下值：

- `X3=value`，其中 `value` 为以下布尔值之一：

  - `yes` — 键盘只有两个键，但必须模拟第三个键。
  - `no` — 键盘已有三个键。
- `MOUSETYPE=value`，其中 `value` 指 X 运行时使用的鼠标类型。选项与此文件中 `MOUSETYPE` 设置相同。
- `DEVICE=value`，其中 `value` 是设备。此外，`/dev/mouse` 是指向实际设备的符号链接。

## `/etc/sysconfig/named`

`/etc/sysconfig/named` 文件用于在启动时向 `named` 进程传递参数。`named` 进程是一个域名系统 (DNS) 服务器，实现了伯克利互联网域名 (BIND) 版本 9。该服务器维护网络上主机名与 IP 地址关联的表。目前，可以使用：

- `ROOTDIR=some/where`，其中 `/some/where` 指向配置好的 chroot 环境的直接路径。必须配置 chroot 环境。有关如何配置的信息请输入 `info chroot`。
- `OPTIONS="value"`，其中 `value` 是 `named` 手页中列出的除 `-t` 以外的任何选项。在 `-t` 处使用之前的 `ROOTDIR` 行。

有关在此文件中使用的参数的更多信息，请参阅 `named`。默认情况下，文件不包含任何参数。

## `/etc/sysconfig/netdump`

`/etc/sysconfig/netdump` 文件是 `/etc/init.d/netdump` 配置文件。`netdump` 服务通过网络发送 oops 数据和内存转储。通常情况下，`netdump` 不是必需的服务，因此只有在绝对需要时才运行它。有关在此文件中可以使用哪些参数的更多信息，请参阅 `man netdump`。

# `/etc/sysconfig/network`

`/etc/sysconfig/network` 文件用于指定所需的网络配置信息。可以使用以下值：

- `NETWORKING=value`，其中 `value` 为以下布尔值值之一：

    - `yes` — 应该配置网络功能。
    - `no` — 不应该配置网络功能。
- `HOSTNAME=value`，其中 `value` 应该是完全限定域名名 (FQDN)，例如 `hostname.domain.com`，但也可以是你想要的任何内容。

> **注意：** 为了兼容人们可能安装的旧软件，`/etc/hostname` 文件和 `/etc/sysconfig/network` 文件应该包含相同的值。

- `GATEWAY=value`，其中 `value` 是网络网关的 IP 地址。
- `GATEWAYDEV=value`，其中 `value` 是网关设备，例如 `eth0`。
- `NISDOMAIN=value`，其中 `value` 是 NIS 域名。

# `/etc/sysconfig/ntpd`

`/etc/sysconfig/ntpd` 文件用于向 `ntpd` 守护进程传递参数，并指定是否在启动时使用。`ntpd` 守护进程设置并维护系统时钟以与互联网标准时间服务器同步。它实现了第 4 版网络时间协议 (NTP)。有关可以在此文件中使用的参数的更多信息，请浏览器访问以下文件：`/usr/share/doc/ntp-version/ntpd.htm`（其中 `version` 是 `ntpd` 的版本号）。默认情况下，此文件将 `ntpd` 进程的所有者设置为用户 `ntp`。

# `/etc/sysconfig/pcmcia`

`/etc/sysconfig/pcmcia` 文件用于指定 PCMCIA 配置信息。可以使用以下值：

- `PCMCIA=value`，其中 `value` 为以下值之一：

    - `yes` — 应该启用 PCMCIA 支持。
    - `no` — 不应该启用 PCMCIA 支持。

# 查看系统配置文件

`PCIC=value`，其中 `value` 为以下值之一：

    - `i82365` — 计算机拥有 `i82365` 式的 PCMCIA 插槽芯片组。
    - `tcic` — 计算机拥有 `tcic` 式的 PCMCIA 插槽芯片组。

- `PCIC_OPTS=value`，其中 `value` 是插槽驱动程序 (`i82365` 或 `tcic`) 的定时参数。
- `CORE_OPTS=value`，其中 `value` 是 `pcmia_core` 选项列表。
- `CARD_MGR_OPTS=value`，其中 `value` 是 PCMCIA `cardmgr` 的选项列表（例如用于静默模式的 `-q`，用于在指定目录查找可加载内核模块的 `-m` 等）。更多信息请参阅 `cardmgr` 页面。

# `/etc/sysconfig/selinux`

此文件链接到 `/etc/selinux/config`，用于控制系统上的 `selinux`。它有两个控制 `selinux` 状态的设置——强制（`enforcing`）、许可（`permissive`）或禁用（`disabled`），以及策略类型——目标（`targeted`）或严格（`strict`）。此文件的示例所示：

```
# 此文件控制系统上 SELinux 的状态。
# SELINUX= 可以取以下三个值之一：
# enforcing 强制执行 SELinux 安全策略。
# permissive SELinux 打印警告而不是执行。
# disabled 禁用禁用 SELinux。
SELINUX=permissive
# SELINUXTYPE = 策略的类型。可能的值有：
# targeted - 仅保护目标网络守护进程。
# strict - 全方位的 SELinux 保护。
SELINUXTYPE=targeted
```

# `/etc/sysconfig/system-config-users`

`/etc/sysconfig/system-config-users` 文件是图形化应用程序用户管理器（User Manager）的配置文件。此文件用于过滤系统用户，如 `root`、`daemon` 和 `lp`。此文件通过用户管理器应用程序中的首选项过滤器用户和组下拉菜单进行编辑，不应手动编辑。

# `/etc/sysconfig/system-logviewer`

`/etc/sysconfig/system-logviewer` 文件是图形化交互式日志查看器（Log Viewer）的配置文件。此文件通过系统日志（System Logs）应用程序中的编辑首选项下拉菜单进行编辑，不应手动编辑。

# `/etc/sysconfig/samba`

`/etc/sysconfig/samba` 文件用于启动时向 `smbd` 和 `nmbd` 守护进程传递参数。`smbd` 守护进程为网络上的 Windows 客户端提供文件共享连接。`nmbd` 守护进程提供 NetBIOS-over-IP 命名服务。有关在此文件中使用的参数的更多信息，请输入 `man smbd`。默认情况下，此文件将 `smbd` 和 `nmbd` 设置为以守护进程模式运行。

# `/etc/sysconfig/sendmail`

`/etc/sysconfig/sendmail` 文件允许将消息发送给一个或多个接收者，通过任何必要的网络路由消息。该文件设置了 Sendmail 运行的默认值。其默认值为作为后台守护进程运行，并每小时检查一次队列，且已备份并挂起进程。可以使用以下值：

- `DAEMON=value`，其中 `value` 为以下布尔值之一：

    - `yes` — 应该配置 Sendmail 监听端口 25 以接收邮件。`yes` 意味着使用 Sendmail 的 `-bd` 选项。
    - `no` — 不应该配置 Sendmail 监听端口 25 以接收邮件。
    - `QUEUE=1h`，传递给 Sendmail 的 `-$QUEUE`。如果 `/etc/sysconfig/sendmail` 存在且 `QUEUE` 为空或未定义，则不将该选项传递给 Sendmail。

# `/etc/sysconfig/vncservers`

`/etc/sysconfig/vncservers` 文件用于配置 `vnc` 服务器启动。它可能包含以下针对不同架构的内容：

- `VNCSVERS=value`，将值设置为类似于 `1`，表示 `vnc` 服务器应该启动。注意，当你使用 `vnc` 服务器时，通信是未加密的。有关 SSH 的具体说明，请查看第 28 章。

# `/etc/sysconfig/xinetd`

`/etc/sysconfig/xinetd` 文件用于启动时向 `xinetd` 守护进程传递参数。`xinetd` 守护进程在接收到请求时启动程序。有关可以在此文件中使用的参数的更多信息，请输入 `man xinetd`。有关 `xinetd`，请查看第 25 章。

# `/etc/sysconfig` 中的目录

`/etc/sysconfig` 下通常包含目录：

# `apm-scripts`

包含 Red Hat APM 暂停/恢复脚本。你不应直接编辑它。如果你需要自定义，只需创建一个 `/etc/sysconfig/apm/control` 文件，它会被调用。

# `daemons`

此目录在系统安装后为空。用于存放用户可能安装的程序的配置。例如，`webmin` 程序的配置文件在安装时放置在此目录。

# `networking`

此目录供网络配置工具（`system-config-network`）使用，其内容不应手动编辑。

> **交叉引用：** 有关使用网络配置工具配置接口的更多信息，请参见第十一章。

# `network-scripts`

此目录包含网络配置文件。

- 每个配置的网络接口的配置文件，例如用于 `eth0` 以太网接口的 `ifcfg-eth0`。
- 用于启动网络接口的脚本，例如 `ifup` 和 `ifdown`。
- 用于启动关闭 ISDN 接口的脚本，例如 `ifup-isdn` 和 `ifdown-isdn`。
- 不应直接编辑的各种共享网络脚本。

# `rhn`

此目录包含 Red Hat Network 的配置文件和 GPG 密钥。此目录中的任何文件都不应手动编辑。有关 Red Hat Network 的更多信息，请访问 Red Hat Network 网站：`https://rhn.redhat.com`。

## 检查系统配置文件 189

- 设置你主机的主机名。修改以下文件：

  `/etc/sysconfig/network`

  `/etc/hosts`

- 设置要引用的 DNS 服务器。修改以下文件：

  `/etc/resolve.conf`

- 创建主机名到 IP 地址映射的本地文件。修改以下文件：

  `/etc/hosts`

- 设置查找主机名的设备顺序。修改以下文件：

  `/etc/nsswitch.conf`

**交叉引用** 第 20 章解释了域名系统 (DNS) 以及如何如何在你的网络上设置它。

> **提示** Fedora Core 和红帽企业级 Linux 提供了一个名为“网络配置”工具的便捷图形化工具，用于配置你的网络设置。在 X-Window 环境下启动网络配置工具，可以使用一个与 Windows 网络控制面板非常类似的界面。如果你不需要按照后续章节所述手动编辑文件，请参考第 11 章关于使用网络配置工具的说明。此外，如果你使用 DHCP 获取 IP 信息，则不需要进行任何手动配置，可以跳过与手动配置网络设置相关的的章节。

## 设置 IP 地址

你应该做的第一件事是在网络接口上设置 IP 地址。这一步为你的计算机在网络上提供了一个身份。如果你尚未在安装过程中设置 IP 地址，则需要手动编辑配置文件。

要在你的第一个以太网接口 `eth0` 上设置 IP 地址，请使用 `/etc/sysconfig/network-scripts/ifcfg-eth0` 文件。该文件的副本如列表 8-7 所示。

在显示如下内容的行插入你接口的 IP 地址：

```
IPADDR=**
```

你还应该检查其他行的内容是否正确，特别注意以下两行：

```
BROADCAST=192.168.1.255
NETMASK="255.255.255.0"
```

```
DEVICE="eth0"
BOOTPROTO="static"
BROADCAST=192.168.1.255
IPADDR=192.168.1.10
NETMASK="255.255.255.0"
NETWORK=192.168.1.0
ONBOOT="yes"
USERCTL=no
```

**列表 8-7** `/etc/sysconfig/network-scripts/ifcfg-eth0` 文件。

## 设置主机名

一旦你选定了主机名，你就需要将其放入两个不同的地方：`/etc/sysconfig/network` 和 `/etc/hosts`。

在下所示的 `/etc/sysconfig/network` 中，修改显示如下内容的行：

`HOSTNAME="terry"`

这是 `/etc/sysconfig/network` 文件：

```
NETWORKING=yes
HOSTNAME="terry"
GATEWAY=192.168.1.1
GATEWAYDEV="eth0"
FORWARD_IPV4="yes"
```

你还需要修改 `/etc/hosts` 文件。修改文件中的第一行，通过添加你想要的主机名，它看起来可能如下所示：

```
127.0.0.1      terry      hostname.localdomain localhost local localeb
```

## 设置 DNS 域名解析

现在你应该能够与网络上的其他主机通信了。然而，如果你不知道它们的 IP 地址，你将无法与它们通信，因为你还没有设置应该引用的 DNS 服务器来将主机名映射到 IP 地址。

## 检查系统配置文件 191

将主机名解析为 IP 地址的程序读取一个名为 `resolv.conf` 的文件，因此你需要将 DNS 服务器的 IP 地址放在那里。通常情况下，你需要一个名称服务器，但如果你愿意，可以包含最多三个。指定多个名称服务器是非常重要的。如果列表中的第一个服务器没有响应，你的计算机将尝试向下一个进行解析，依此类推，直到找到一个有响应的服务器。

编辑 `/etc/resolv.conf` 以包含名称服务器列表，如下：

```
nameserver 1.2.3.4
nameserver 1.2.3.5
nameserver 1.2.3.6
```

## 创建主机名到 IP 地址映射的本地文件

Linux 允许你在 `/etc/hosts` 中存储主机名列表及其对应的 IP 地址，这样你就不需要每次使用它们时都去 DNS 中查找了。虽然你不应该对使用的每个主机名都这样做，但这样做的优点之一是通过这种方式配置常用主机名，可以将完全限定主机名别名为其更短的版本。你不需要在每次想 SSH 连接到那台机器时s都输入 `ssh foo.xena`，只需输入 `foo.xena.edu` 即可连接到同一个主机。

另一个有用的例子发生在你从监控主机监控多台服务器的网络时。例如，如果你正在监控到某些服务器的 SSH 连接情况，而你的 DNS 服务器停止了响应，监控软件可能会报告你的所有主机都离线了。这种情况是因为监控软件尝试通过主机名连接到服务器，但由于 DNS 未提供用于连接的 IP 地址，它没有得到任何响应。在这种情况下，看起来是你的网络崩溃了，但实际问题是你的 DNS 服务没有正常响应。

为了防止此类场景发生，你应该将主机名和 IP 地址放入 `/etc/hosts` 中。这样，系统在询问 DNS 服务器之前之前会先检查本地文件。如果 DNS 服务器宕机了，系统仍然能够解析 `/etc/hosts` 文件中列出的主机名。

```
127.0.0.1      terry      hostname.localdomain localhost local localeb
192.168.1.10   server1    server1.local
```

# 194 第 8 章

连接。当建立新连接时，`xinetd` 会启动相应的网络服务。

你应该禁用从 `xinetd` 启动的不必要服务，以增强你机器的安全性。此此的方法是编辑 `xinetd` 的配置文件 `/etc/xinetd.conf`。在 `xinetd.conf` 文件的末尾有一行指示表明 `/etc/xinetd.d` 下中的所有文件都已包含在此配置中。这意味着你还需要检查该目录下的文件，以关闭任何你不需要的服务。

因此，要禁用 Telnet，你需要在 `/etc/xinetd.d` 中查找一个名为 `telnet` 的文件。该文件如图 8-9 所示。编辑配置文件中显示 `disable = no` 的行，将其更改为 `disable = yes`，如列表 8-9 所示。在将该行设置为 `disable = yes` 后，该服务将被禁用，并在下次启动系统时不会启动。

```
/etc/xinetd.d/telnet

# default: on
# description: The telnet server serves telnet sessions; it uses \
# unrestricted username/password for for authentication.
{
    flags       = REUSE
    socket_type = stream
    wait        = no
    user        = root
    server      = /usr/sbin/in.telinetd
    log_on_failure = USERID
    disable     = yes
}
```
