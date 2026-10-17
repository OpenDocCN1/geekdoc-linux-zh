
各种默认 UFW 策略存储在 `/etc/default/ufw` 配置文件中。首次安装时，这些设置允许所有传出连接并阻止所有传入连接。您可以使用 `ufw` 命令及其各种参数根据需要修改防火墙。表 18.5 展示了一些常用参数。

### 表 18.5 ufw 命令的常用参数

| 参数 | 描述 |
| :--- | :--- |
| `allow <Identifiers>` | 将 `<Identifiers>` 标识的规则设置为允许数据包 |
| `deny <Identifiers>` | 将 `<Identifiers>` 标识的规则设置为拒绝（丢弃）数据包 |
| `reject <Identifiers>` | 将 `<Identifiers>` 标识的规则设置为拒绝数据包 |
| `delete RULE \| NUM` | 删除由 `RULE` 或 `NUM` 标识的规则 |
| `insert NUM RULE` | 在索引 `NUM` 处插入规则 |
| `default POLICY DIRECTION` | 修改默认 `DIRECTION` 策略，其中 `POLICY` 为 `allow`、`deny` 或 `reject`，`direction` 为 `incoming`、`outgoing` 或 `routed` |
| `logging LEVEL` | 设置日志记录级别，其中 `LEVEL` 为 `on`、`off`、`low`（默认）、`medium`、`high` 或 `full` |

在创建新的 UFW 规则时，您可以使用简单或完整语法。简单语法涉及仅使用端口号或其服务名称来指定规则。您还可以将协议添加到端口号中，如清单 18.15 所示。

## 列表 18.15：使用 ufw 简单语法添加 ACL 规则

```bash
$ sudo ufw allow 22/tcp
Rule added
Rule added (v6)
$
$ sudo ufw status
Status: active
To   Action   From
--   ------   ----
22/tcp   ALLOW   Anywhere
22/tcp (v6)   ALLOW   Anywhere (v6)
```

请注意，当添加规则时，应用了两条规则——一条用于 IPv4 数据包，另一条用于 IPv6 数据包。使用完整语法时，有很多选项可用。例如，你可以采用表格 18.6 中列出的设置。

### 表格 18.6：ufw 命令完整语法的常用设置

| 设置 | 描述 |
| :--- | :--- |
| `comment "字符串"` | 对于被拒绝的流量显示此注释 |
| `in` | 规则仅应用于入站流量 |
| `out` | 规则仅应用于出站流量 |
| `proto 协议` | 规则应用于此 `协议` |
| `port 端口号` | 规则应用于此 `端口号` |
| `from 源` | 规则来自此 `源` 的流量，该源可以是单个 IP 地址、子网或任意流量 |
| `on 接口` | 规则应用于此网络 `接口` 上的流量 |
| `to 目的` | 规则应用于去往此 `目的` 的流量，该目的可以是单个 IP 地址、子网或任意流量 |

> **注意**
>
> 在添加、删除或修改规则后，无需发出 `ufw reload` 命令。更改会自动生效。

你可以通过服务名称（例如 `telnet`）使用 `ufw` 命令来指定规则。这样做时，`ufw` 会检查 `/etc/services` 文件以确定该服务的适当端口和协议信息。

使用 UFW 完整语法的示例在列表 18.16 中显示。在这种情况下，来自 `192.168.0.0` C 类子网中任何系统的数据包将被拒绝访问此系统的 `80` 端口。

### 列表 18.16：使用 ufw 完整语法添加 ACL 规则

```bash
$ sudo ufw deny from 192.168.0.0/24 to any port 80
Rule added
$
$ sudo ufw show added
Added user rules (see 'ufw status' for running firewall):
ufw allow 22/tcp
ufw deny from 192.168.0.0/24 to any port 80
$
```

可以使用 `ufw show added` 命令查看任何用户添加的规则，如列表 18.16 所示。UFW 规则存储在 `/etc/ufw/` 目录中，用户添加的规则被放置在该目录内的 `user.rules` 文件中，如列表 18.17 所示。

### 列表 18.17：显示 `/etc/ufw/` 目录的内容

```bash
$ ls /etc/ufw/
after6.rules applications.d before.rules user6.rules
after.init before6.rules sysctl.conf user.rules
after.rules before.init ufw.conf
$
```

如果需要删除规则，最简单的方法是通过规则编号进行。首先通过编号查看规则，然后使用 `ufw delete` 命令，如列表 18.18 所示。

### 列表 18.18：通过编号删除规则

```bash
$ sudo ufw status numbered
Status: active

  To                 Action     From
  --                 ------     ----
  [ 1] 22/tcp         ALLOW IN   Anywhere
  [ 2] 80             DENY IN    192.168.0.0/24
  [ 3] 22/tcp (v6)    ALLOW IN   Anywhere (v6)

$ sudo ufw delete 2
Deleting:
deny from 192.168.0.0/24 to any port 80
Proceed with operation (y/n)? y
Rule deleted
$
```

UFW 为常见应用程序和守护程序使用 `配置`。这些配置存储在 `/etc/ufw/applications.d/` 目录中。使用 `ufw app list` 命令查看当前可用的 UFW 应用程序配置。示例在列表 18.19 中显示。

### 列表 18.19：查看可用的 UFW 应用程序配置

```bash
$ sudo ufw app list
Available applications:
  CUPS
  OpenSSH
$ sudo ufw app info OpenSSH
Profile: OpenSSH
Title: Secure shell server, an rshd replacement
Description: OpenSSH is a free implementation[...]
Port:
  22/tcp
$
```

你还可以查看这些配置的详细信息，如列表 18.19 中也可所见。配置不仅提供应用程序文档，还允许你修改应用程序使用的端口和协议，以及为系统需求创建非典型的应用程序配置。

![](img/c0a399aca0d18f8822d714ad0a173123_603_0.png)

> 不要修改 `/etc/ufw/applications.d/` 目录中的配置。相反，在该目录下创建一个子目录并命名为 `custom.d`。这将防止你的自定义配置在 UFW 软件包更新期间被覆盖。有关配置规范的更多细节，请参见 `ufw` 手册页。

一旦你创建了新的配置或更新了旧配置，请使用 `ufw app update all` 命令来更新 UFW 以适应配置更改。此外，当使用配置指定规则的端口和协议时，在创建新规则的语法中，你必须使用 `app` 而不是 `port`。

## 转发 IP 数据包

Linux 中有一个数据包转发功能。此功能用于各种目的，例如允许 Linux 将数据包转发到远程主机，或用于 IP 伪装。在使用该功能之前，必须在内核中启用数据包转发。要启用该功能，只需为 IPv4 设置 `ip_forward` 项，或为 IPv6 设置 `forwarding` 项。你可以使用 `sysctl` 命令做到这一点：

```bash
sudo sysctl -w net.ipv4.ip_forward=1
sudo sysctl -w net.ipv6.conf.all.forwarding=1
```

你可以使用 `cat` 命令在 `/proc` 文件系统条目中检查当前的内核值。如果文件包含数字 `1`，则表示该功能已启用，如列表 18.20 所示；如果禁用，则文件将包含数字 `0`。

### 列表 18.20：查看数据包转发文件

```bash
$ cat /proc/sys/net/ipv4/ip_forward
1
$ cat /proc/sys/net/ipv6/conf/all/forwarding
1
$
```

一旦设置了这些内核值，你的 Linux 系统就能够将一个网络接口的流量转发到另一个网络接口。如果 Linux 系统上有多个网络接口，它会通过路由表知道使用哪个接口将流量发送到远程主机。路由表在第 7 章“配置网络连接”中已涉及。

## 动态设置规则

在保护系统时，拥有监控网络和系统上运行应用程序的软件有助于发现可疑行为。这些应用程序称为 `入侵检测系统`（IDS）。一些 IDS 应用程序允许你动态更改规则，以阻止这些攻击。DenyHosts 和 Fail2Ban 是两个这样的 IDS 程序。

防火墙工具箱中另一个有用的工具是允许你快速更改规则而无需反复输入长 IP 地址或 MAC 地址的工具。IPset 可以帮助解决此问题。

### DenyHosts

DenyHosts 应用程序是一个 Python 脚本，有助于保护系统免受通过 OpenSSH 进行的暴力破解攻击。该脚本可以作为服务运行，也可以作为 `cron` 任务运行。

它监控发行版认证日志文件中的 `sshd` 日志消息，例如 `/var/log/secure` 和 `/var/log/auth.log`。如果发现来自同一主机的重复认证失败尝试，它通过 `/etc/hosts.deny` 文件阻止该 IP 地址。

要配置 DenyHosts，你需要修改其 `/etc/denyhosts.conf` 文件。你还需要准备好 TCP Wrappers 文件 `/etc/hosts.allow` 和 `/etc/hosts.deny`。

![](img/c0a399aca0d18f8822d714ad0a173123_605_0.png)

> DenyHosts 仅适用于 IPv4 OpenSSH 流量。对于其他流量，你需要使用不同的工具。此外，请注意，一些发行版软件包仓库声称 DenyHosts 不再被开发。因此，请谨慎安装和使用。

### Fail2Ban

Fail2Ban 服务也监控系统日志，查找来自同一主机的重复失败。如果检测到问题，Fail2Ban 可以阻止违规主机的 IP 地址访问你的系统。虽然 DenyHosts 仅支持 TCP Wrappers，但 Fail2Ban 可以支持 TCP Wrappers、`iptables`、`firewalld` 等。

`fail2ban-client` 程序监控系统和应用程序日志，查找问题。它监控常见的系统日志文件，如 `/var/log/pwdfail` 和 `/var/log/auth.log` 日志文件，查找多次登录失败。当检测到某个用户账户有太多登录失败尝试时，它会阻止该用户账户尝试登录的主机访问。

Fail2Ban 的一个很棒功能是可以监控单个应用程序日志文件，例如 Apache Web 服务器的 `/var/log/apache/error.log` 日志文件。就像系统日志文件一样，如果 Fail2Ban 检测到来自同一远程主机的连接尝试或错误过多，它将阻止该主机的访问。

`/etc/fail2ban/jail.conf` 文件包含 Fail2Ban 配置。它定义要监控的应用程序、它们的日志文件位置以及在检测到问题时采取的操作。

![](img/c0a399aca0d18f8822d714ad0a173123_605_1.png)

> 使用 Fail2Ban 的缺点是它可能会出现误报，即在真正没有问题的情况下检测到问题。这可能导致它阻止合法客户端访问系统。幸运的是，Fail2Ban 足够强大，你可以配置它在设定时间后解除阻止，以允许客户端正确重新连接。

### IPset

IPset 是 IP 地址、网络接口、端口、MAC 地址或子集的命名集合。通过创建这些集合，你可以轻松管理通过防火墙和其他支持 IPset 的应用程序进行分组。

`ipset` 实用程序用于管理 IPset（IP 集合），并需要超级用户权限。创建 IPset 时，你需要先确定要为其赋予的名称。之后，决定你希望如何存储该 IPset。你的存储选项包括 `bitmap`（位图）、`hash`（哈希）或 `list`（列表）。通过 `ipset` 命令创建 IPset 有两种方式：

```bash
ipset create IPset-Name storage-method:set-type
ipset -N IPset-Name storage-method:set-type
```

清单 18.21 展示了在 Rocky Linux 发行版上创建子网 IPset 并向其中添加成员的示例。

### 清单 18.21：创建并填充子网 IPset

```bash
# ipset create BadGuyNets hash:net
#
# ipset add BadGuyNets 1.1.1.0/24
# ipset -A BadGuyNets 2.2.0.0/15
#
```

一旦你完成了 IPset 的成员填充，你就可以检查你的成果。只需使用 `ipset list` 命令，如清单 18.22 中的片段所示。

### 清单 18.22：查看子网 IPset

```bash
# ipset list
Name: BadGuyNets
Type: hash:net
[...]
Members:
1.1.1.0/24
2.2.0.0/15
```

创建并填充 IPset 后，在 `iptables` 或 `firewalld` ACL 规则中阻止该 IPset。为了使 IPset 持久化，你可以通过 `ipset save` 命令保存它，并将其 STDOUT（标准输出）重定向到 `/etc/ipset.conf` 文件，或者使用 `-f` 选项。

![](img/c0a399aca0d18f8822d714ad0a173123_606_0.png)

创建 IPset 后，你需要启动 `ipset` 服务。然而，在 systemd 系统上，你可能找不到用于启动或启用的服务文件。因此，如果你的发行版使用 systemd，你需要创建 `ipset.service` 文件，或者从可靠来源获取该文件。

你可以使用 `ipset del` 命令从命名 IPset 中删除单个条目。要删除整个 IPset，你需要销毁它，如清单 18.23 所示。

### 清单 18.23：删除子网 IPset

```bash
# ipset destroy BadGuyNets
#
# ipset list
#
```

![](img/c0a399aca0d18f8822d714ad0a173123_607_0.png)

只有 `firewalld` 和 `iptables` 服务命令直接支持 IPset。然而，你可以将 IPset 与 UFW 配合使用，但这需要多做一点工作。你必须修改 `/etc/ufw/` 目录中的 `before.init` 和 `after.init` 脚本。请查阅 `ufw-framework` 的手册页以了解有关这些脚本的更多信息。

## 摘要

正确管理系统的防火墙应用程序及其数据包过滤 ACL（访问控制列表）对于保障系统安全至关重要。为此，你必须了解防火墙软件的底层框架、如何修改其 ACL 规则，以及可以与该软件一起使用哪些附加应用程序来阻止恶意网络流量。使用正确的产品并正确配置它们不仅有助于保持系统安全，还能使你的工作变得更加轻松。

## 考试要点

**总结各种防火墙功能。** 防火墙 ACL 识别允许进入或离开网络的哪些数据包。无状态防火墙查看每个数据包的控制信息，并根据定义的 ACL 规则决定如何处理该数据包。有状态防火墙跟踪活动的网络连接，例如 `TCP` 和 `UDP`；监控网络状态；并可以判断数据包是否已分片。防火墙采用 `/etc/services` 文件，该文件记录了不同的标准应用程序服务名称及其对应的端口号、协议和别名。

**描述 firewalld 及其命令。** 对于 `firewalld` 服务，网络流量被分组到一个区域（zone）中，该区域是一组预定义的规则集。每个区域都有一个配置文件来定义此规则集，也称为信任级别。`firewalld` 区域配置文件存储在 `/usr/lib/firewalld/zones/` 目录中。自定义或用户创建的区域配置文件存储在 `/etc/firewalld/zones/` 目录中。对于 `firewalld`，服务是为特定服务（如 DNS）预定义的配置集。当你修改 `firewalld` 配置时，默认情况下你修改的是运行时环境，即当前活动状态。永久环境是配置文件中的防火墙设置。`firewall-cmd` 实用程序允许你查看并与 `firewalld` 进行交互。

**描述 iptables 及其命令。** `iptables` 防火墙服务使用称为 `链`（chains）的一系列过程来处理进入系统的网络数据包。这些链决定了每个数据包在进入 Linux 系统时到达相应应用程序所经过的路径。每个链都有一个策略值，并包含定义处理数据包规则的表。`iptables` 中的 ACL 规则为识别出的数据包提供了目标值，这些值决定了对它们采取的操作。`iptables` 命令允许你查看和交互各种 `iptables` 配置设置。
