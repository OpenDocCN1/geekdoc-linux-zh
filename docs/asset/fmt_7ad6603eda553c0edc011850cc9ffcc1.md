
`/etc/resolv.conf`

```
search mytrek.com mytrain.com

nameserver 192.168.0.1

nameserver 192.168.0.3
```

## `/etc/sysconfig/network-scripts`

`/etc/sysconfig/network-scripts` 目录存储不同网络连接设备的配置信息，例如所使用的 IP 地址和网络地址。详细讨论，请参阅本章节后续的“网络接口和路由：`ifconfig` 和 `route`”部分。

## `/etc/sysconfig/networking`

`/etc/sysconfig/networking` 目录存储通过 `system-config-network`（系统设置菜单和窗口中的“网络”）设置的配置信息。这些文件不应手动编辑。`profiles` 目录存储你设置的不同配置文件的配置。不同的配置将包含列出域名和 IP 地址的主机文件、持有系统主机名的 `network` 文件，以及包含你的域名服务器的 `resolv.conf` 文件。将列出你为该配置所用连接的设备配置文件，例如第一个以太网设备的 `ifcfg-eth0`。这些都是可能根据你使用的配置而改变的设置。例如，在办公室里，你可能使用公司网络上的以太网连接，该网络有自己的 DNS 服务器；而在家里，你可能使用连接到 ISP 的现代连接，ISP 也有它自己的 DNS 服务器。你的主机名和域名可能会根据你不同配置所连接的网络有所不同。

## `/etc/services`

`/etc/services` 文件列出了系统上可用的网络服务（如 FTP 和 Telnet），并将每个服务与特定端口关联。在这里，你可以发现是哪个 Web 服务器正在检查，或者哪个端口用于你的 FTP 服务器。你可以为服务指定一个别名，指定在端口号之后。然后你可以使用别名引用该服务。

## `/etc/protocols`

`/etc/protocols` 文件列出了你的系统当前支持的 TCP/IP 协议。每个条目显示协议号、其关键字标识符和简要描述。完整列表请参见 `www.iana.org/assignments/protocol-numbers`。

## `/etc/sysconfig/network`

`/etc/sysconfig/network` 文件包含了你网络配置的系统定义。这些包括了对域名、主机名和网关的定义，如下所示：

```
NETWORKING=yes

HOSTNAME=turtle.mytrek.com

GATEWAY=192.168.0.1
```

## 域名系统 (DNS)

每个连接到 TCP/IP 网络（如互联网）的计算机都通过其自己的 IP 地址进行标识。IP 地址很难记忆，因此也使用每个 IP 地址的域名版本来标识主机。如第 38 节所述，域名由两部分组成：主机名 (`hostname`) 和域名 (`domain`)。主机名是计算机的特定名称，而域名标识计算机所属的网络。用于美国的域名通常具有标识主机类型的扩展。

例如，`.edu` 用于教育机构，`.com` 用于商业机构。国际域名通常具有指示其所在地国家的扩展，例如德国的 `.de` 或澳大利亚的 `.au`。主机名、域名和扩展的组合形成了一个唯一名称，计算机可以通过该名称进行引用。域名可以进一步细分为多个子域名。

如你所知，网络上的计算机只能通过其 IP 地址进行标识，即使它有主机名。你可以使用主机名来引用网络上的计算机，但这涉及使用主机名在数据库中查找对应的 IP 地址。然后网络使用 IP 地址而非主机名来访问计算机。

# 766 第七：网络管理

| 文件 | 说明 |
| --- | --- |
| aliases | 邮件别名，由 Sendmail 使用 |
| ethers | 以太网编号 |
| group | 用户组 |
| hosts | 主机名和编号 |
| netgroup | 全网络范围的主机和用户列表，用于访问规则；在 glob:2.1 之前的 C 库仅支持通过 NIS 使用 netgroups |
| network | 网络名称和编号 |
| passwd | 用户密码 |
| protocols | 网络协议 |
| publicKey | 用于 NFS 和 NIS+ 中 SecureRPC 的公钥和密钥 |
| rpc | 远程过程调用名称和编号 |
| services | 网络服务 |
| shadow | 影子用户密码 |

表 37-8 NSS 支持的文件

操作项（action item）指定了针对特定服务要执行的操作。操作项放置在服务后的括号内。配置规范可以列出多个服务，每个服务都有其自己的操作项。在接下来的示例中，网络文件的条目具有一个配置规范，指示检查 NIS 服务，如果未找到，则检查 `/etc/protocols` 文件： `protocols: nisplus [NOTFOUND=return] files`

操作项由状态和一个动作组成。状态持有服务查找的可能结果，而动作是在状态为真时要采取的操作。目前，可能的状态值为 `SUCCESS`、`NOTFOUND`、`UNAVAIL` 和 `TRYAGAIN`（服务临时不可用）。可能的动作有 `return` 和 `continue`：`return` 停止配置文件的查找过程，而 `continue` 则继续到下一个列表服务。在上述的示例中，如果在 NIS 中未找到记录，则查找过程将结束。

| 服务 | 说明 |
| --- | --- |
| files | 检查 `/etc` 文件的顺序进行配置（例如用于 hosts 的 `/etc/hosts`）；此服务适用于所有文件 |
| db | 检查 `/var/db` 数据库的顺序进行配置；除 netgroup 外的所有文件均有效 |
| compat | 仅适用于 passwd、group 和 shadow 文件 |
| dns | 检查 DNS 服务；仅适用于 hosts 文件 |
| nis | 检查 NIS 服务；适用于所有文件 |
| nisplus | NIS 版本 3 |
| hesiod | 使用 Hesiod 进行查找 |

表 37-9 NSS 配置服务

# 第 37 章：管理 TCP/IP 网络

此处显示当前 `/etc/nswitch.conf` 文件的副本，它列出了常用的条目。注释和被注释的条目以 `#` 号开头：

```
/etc/nswitch.conf

# /etc/nswitch.conf

# # 一个示例名称服务切换配置文件。

passwd:      db files nplus nis

shadow:      db files nplus nis

group:       db files nplus nis

hosts:       files nplus dns

bootparams:  nisplus [NOTFOUND=return] files

ethers:     files

netmasks:    files

networks:    files

protocols:   files

rpc:         files

services:    files

netgroup:    nisplus

publickey:   nisplus

automount:   files

aliases:     files nisplus
```

## 网络接口与路由：`ifconfig` 和 `route`

你的系统通过特定的硬件接口（如以太网卡或调制解调器）连接到网络。通过该接口传输的数据会被路由到你的网络。`ifconfig` 命令配置你的网络接口，而 `route` 命令据此设置网络连接。如果你使用网络配置工具（如 `system-config-network`）配置接口，则不需要使用 config 或 route。然而，你可以直接使用 `ifconfig` 和 `route` 配置接口，每次启动系统时，都必须建立网络接口及其路由。这在你启动系统时，由 `/etc/rc.d/init.d/network` 初始化文件为每个接口执行的 `ifconfig` 和 `route` 命令自动完成的，该文件在系统启动时执行。如果你是手动添加接口，则必须设置网络脚本来为你的新接口执行 `ifconfig` 和 `route` 操作。

# 网络启动脚本：`/etc/rc.d/init.d/network`

在 Fedora Core 上，你的网络接口是由 `/etc/rc.d/init.d/` 中的网络脚本启动的。当你实现网关、主机和名称服务器标识等配置信息时，该脚本将激活你的网卡（NIC）。你可以使用此脚本以及 `restart`、`start` 或 `stop` 选项以及 `system-config-services` 手动关闭和启动网络接口。你可以使用 `service` 命令运行 Fedora Core 的脚本。以下命令关闭并启动你的网络接口：

```
