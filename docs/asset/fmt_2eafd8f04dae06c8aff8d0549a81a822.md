
`netstat` 命令用于显示网络状态。它有几个参数，可以显示你喜欢的尽可能多或尽可能少的信息。服务按套接字（两台计算机之间的应用对应用连接）列出。你可以使用 `netstat` 来显示表 18.2 中的信息。

| 选项 | 输出 |
|---|---|
| .g | 显示配置的多播组 |
| .i | 显示由 `ifconfig` 配置的接口 |
| .s | 列出每个协议的活动摘要 |
| .v | 提供详细输出，列出活动和非活动套接字 |
| .c | 每秒更新输出（适合测试和故障排除） |
| .e | 仅为活动连接提供详细输出 |
| .C | 显示路由缓存信息，适合查看过去的连接 |

此命令还有其他几个可用选项，但使用频率较低。与 `/sbin/route` 命令一样，`man` 页可以提供所有选项和参数的详细信息。

## 网络配置文件

如前所述，可以修改七个网络配置文件来更改系统的基本网络交互。这些文件是

- `/etc/hosts`——地址、主机名和别名的列表
- `/etc/services`——网络服务和端口连接
- `/etc/nsswitch.conf`——Linux 网络信息搜索配置
- `/etc/resolv.conf`——域名服务域（搜索）设置
- `/etc/host.conf`——网络信息搜索顺序（默认情况下，先是 `/etc/hosts`，然后是 DNS）
- `/etc/sysconfig/network`——主机名、IP 地址、启动激活控制和网关设置（以及可选的 IPv6 设置）
- `/etc/sysconfig/network-scripts/ifcfg-eth0`——`eth0` 网络设备设置；有关可选设置的详细信息，请参阅 `/usr/share/doc/initscripts/` 目录下的文件 `sysconfig.txt`

修改这六个文件中的前六个后，更改即可生效。与大多数配置文件一样，可以在注释前使用井号（`#`）添加注释。最后一个文件（`/etc/sysconfig/network`）要求在文件使用前重启网络守护进程。这七个文件都有一个 `man` 页提供更多信息。

## 将主机添加到 /etc/hosts

`/etc/hosts` 文件是 IP 到主机名的映射。如果你没有使用 DNS 或其他命名服务，并且连接到大型网络，该文件可能会变得非常大，管理起来非常麻烦。小型的 `/etc/hosts` 文件可能看起来像这样：

```
127.0.0.1     localhost.localdomain      localhost

128.112.50.69 myhost.mydomain.com        myhost

128.112.50.169 yourhost.mydomain.com     yourhost
```

第一个条目用于回环条目。第二个用于机器名称。第三个是网络上的另一台机器。如果网络上没有使用命名服务，`myhost` 能识别的唯一主机名是 `yourhost`。（网络上的 IP 地址仍然可以使用。）

如果你的网络使用命名服务，最后一行不需要，可以删除。但是，如果 `myhost` 经常连接到 `yourhost`，保留该条目可能更好，这样 `myhost` 每次就不需要查询命名服务。这可以节省时间并减轻网络或命名服务服务器的负担。如果你需要更改主机名或 IP 地址，或者你没有使用命名服务且网络中已添加主机，请编辑此文件。

## /etc/services 中的服务设置

`/etc/services` 文件将端口号映射到服务。前几行看起来类似于以下内容（`/etc/services` 文件可能相当长，超过 500 行）：

```
# 每一行描述一个服务，格式为：

#

# service-name port/protocol [aliases ...] [# comment]

tcpmux 1/tcp # TCP 端口服务多路复用器

tcpmux 1/udp # TCP 端口服务多路复用器

rje 5/tcp # 远程作业输入

rje 5/udp # 远程作业输入

echo 7/tcp

echo 7/udp

discard 9/tcp sink null

discard 9/udp sink null

systat 11/tcp users
```

通常，每个服务有两个条目，因为大多数服务可以使用 TCP 或 UDP 进行传输。通常，在 `/etc/services` 初始配置完成后，你不需要更改它。

## 更改命名服务后使用 /etc/nsswitch.conf

该文件最初由 Sun Microsystems 开发，用于指定系统中访问服务的顺序。`/etc/nsswitch.conf` 文件列出了许多服务，但最常修改的条目是 `hosts` 条目。文件的一部分可能看起来像这样：

```
passwd: files

shadow: files

group: files

#hosts: db files nisplus nis dns

hosts: files dns
```

这告诉服务系统应查询标准的 Unix/Linux 文件以进行 `passwd`、`shadow` 和 `group` 的查找（分别对应 `/etc/passwd`、`/etc/shadow` 和 `/etc/group`）。对于主机名查找，系统会检查 `/etc/hosts`，如果其中没有条目，则检查 DNS。被注释掉的 `hosts` 条目列出了主机查找的可能值。只有当你的命名服务发生变更时，才需要编辑此文件。

## 通过 `/etc/resolv.conf` 设置名称服务器

`/etc/resolv.conf` 被 DNS（域名服务）使用。（DNS 在章节 27 中有详细介绍。）以下是 `resolv.conf` 的一个示例：

```text
nameserver 192.172.3.8

nameserver 192.172.3.9

search mycorp.com
```

这设置了 DNS 使用的名称服务器及域名的顺序。如果你使用动态主机配置协议（Dynamic Host Configuration Protocol，即 DHCP），该文件的内容将自动设置（请参见本章稍后的“DHCP”部分）。

## 通过 `/etc/host.conf` 设置 DNS 搜索顺序

`/etc/host.conf` 文件列出了机器搜索主机名解析的顺序。以下是默认的 `/etc/host.conf` 文件：

```text
order hosts, bind
```

在此示例中，主机先检查 `/etc/hosts` 文件，然后执行 DNS 查找。还有几个选项控制命名服务的使用方式。修改此文件的唯一原因是你使用 NIS 作为命名服务，或者想要使用某种可选服务。`nosport` 选项对于系统安全可能是一个不错的选项。它将标准的 DNS 查找与反向查找（从主机到 IP，然后从 IP 到主机）进行比较，如果两者不匹配则失败。缺点是，当使用代理服务时，查找通常会失败，因此需谨慎使用此选项。

## 检查 `/etc/sysconfig/network` 中的主机网络设置

对 `/etc/sysconfig/network` 的更改将在重启网络守护进程或重启系统之前不会生效。如果你使用 Fedora 的图形化网络配置工具（在下一节中介绍），你不应该编辑此文件。该文件可能如下所示：

```text
NETWORKING=yes

HOSTNAME=myhost

GATEWAY=192.112.50.99
```

`GATEWAYDEV` 设置也可用于关联特定的网络设备（如 `eth0` 或 `eth1` 等）。`/etc/sysconfig/network` 中还有一个额外的可选条目，用于 NIS 域机器，如下所示：

```text
NISDOMAIN=rebel
```
