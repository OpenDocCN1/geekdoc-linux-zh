
```
[root@hel -]# firewall-cmd --state
running
[root@hel -]# systemctl status firewall
● firewall.service - active (dynamic, daemon)
  Loaded: loaded (/usr/lib/system/firewall.service; enabled; vendor preset)
  Active: active (running) since 2022-08-28 16:59:22 CEST; 7h ago
  Docs: manfirewall(1)
  Main PID: 802 (firewall)
  Tasks: 2 (limit: 7757)
  Memory: 28M
  CPU: 2.24s
Group: system.slice/firewall.service
```

`Aug 27 15:59:28 rhel.example.com systemd[1]: Starting firewall - dynamic firewall`

`Aug 27 15:59:28 rhel.example.com systemd[1]: Started firewall - dynamic firewall`

> 图 8.3: 检查防火墙服务状态的输出示例

默认情况下，防火墙针对不同用途有一些预定义的区域。表 8.1 显示了名称和描述：

| Zone | 描述 |
|---|---|
| `drop` | 丢弃所有入站数据包，且不作响应。仅允许站网络连接。 |
| `block` | 拒绝所有入站网络连接，IPv4 发送 `icmp-host-prohibited` 消息，IPv6 发送 `icmp6-adm-prohibited` 消息。仅允许在该系统内部发起的连接。 |
| `public` | 用于公共区域。你不信任网络上的其他计算机不会损害你的计算机。只接受选定的入站连接。 |
| `external` | 用于启用了伪装的外部网络，特别是对于路由器。你不信任网络上的其他计算机不会损害 你的计算机。 |
| `dmz` | 用于你的非军事化区域内的计算机，这些计算机可以公开访问，但对内部网络的访问有限。只接受选定的入站连接。 |
| `work` | 用于工作区域。你必须信任网络上的其他计算机不会损害你的计算机。只接受选定的入站连接。 |
| `home` | 用于家庭区域。你必须信任网络上的其他计算机不会损害你的计算机。只接受选定的入站连接。 |
| `internal` | 用于内部网络。你必须信任网络上的其他计算机不会损害你的计算机。只接受选定的入站连接。 |
| `trusted` | 接受所有网络连接。 |

表 8.1: `firewalld` 中的预定义区域

可以使用 `--get-zones` 选项列出所有可用区域。`--get-active-zones` 列出活动区域，包括分配给这些区域的接口。`--get-default-zone` 选项打印连接和接口的默认区域。图 8.4 显示了上述选项的输出示例：

```
[root@rhel]# firewall-cmd --get-zones
block dmz drop external home internal nm-shared public trusted work
[root@rhel]# firewall-cmd --get-active-zones
public
interfaces: enp1s0 bond0 enp7s0 enp8s0 vlan10
[root@rhel]# firewall-cmd --get-default-zone
public
```

图 8.4: 使用 `firewall-cmd` 命令获取区域的输出示例

`--list-all` 选项列出与默认区域（默认为 `public`）相关的信息，包括允许的服务和分配的接口。

```bash
root@ubuntu:~# ufw status
Status: inactive
root@ubuntu:~# ufw enable
Command may disrupt existing ssh connections. Proceed with operation (y|n)?
Firewall is active and enabled on system startup
```

图 8.10：使用 `ufw` 状态并启用防火墙

可以使用 `allow` 参数并指定允许的端口来允许新连接。`deny` 参数则拒绝该连接。可以指定协议（参数 `proto`）、源地址（参数 `from`）、目标 IP（`to`）以及目标端口（`port`）。图 8.11 显示了允许所有人访问 22 端口以及允许特定 IP 访问 80 端口的示例：

```bash
root@ubuntu:~# ufw allow 22
Rule added
Rule added (v6)
root@ubuntu:~# ufw allow proto tcp from 192.168.122.145 to any port 22
Rule added
```

图 8.11：使用 `ufw` 允许访问系统

当 `ufw` 配置了规则时，使用 `status` 参数可以列出这些规则。可以添加 `verbose` 作为第二个参数以获取关于默认操作的信息，如图 8.12 所示：

```bash
root@ubuntu:~# ufw status verbose
Status: active
Logging: on (low)
Default: deny (incoming), allow (outgoing), disabled (routed)
New profiles: skip
```

| | Action | From |
|---|---|---|
| 22 | `ALLOW IN` | `Anywhere` |
| 22/tcp | `ALLOW IN` | `192.168.122.145` |
| 22 (v6) | `ALLOW IN` | `Anywhere (v6)` |

图 8.12：列出 `ufw` 中的规则

某些应用程序在目录 `/etc/ufw/applications/` 下创建了使用的端口定义。以下代码显示了 `openssh-server` 应用程序的定义：

```ini
[OpenSSH]
title=Secure shell server, an rshd replacement
description=OpenSSH is a free implementation of the Secure Shell protocol.
ports=22/tcp
```

可以使用 `app list` 参数列出定义的应用程序，并使用 `app info` 获取信息。图 8.13 显示了用法示例：

```bash
root@ubuntu:~# ufw app list
Available applications:
OpenSSH
root@ubuntu:~# ufw info OpenSSH
Profile: OpenSSH
Title: Secure shell server, a rshd replacement
Description: OpenSSH is a free implementation of the Secure Shell.
Port:
22/tcp
```

图 8.13：使用 `ufw` 列出应用程序并获取信息

## 伪装地址 (Masquerading)

在第 7 章“网络配置”中，我们学习了如何配置 Linux 服务器充当路由器。通过 IP 转发（IP Forwarding），我们可以访问其他网络。只有在不涉及网络地址转换 (NAT) 的情况下，这才是可能的。例如，当节点 IP 为 `192.168.122.10` 且网关为 `192.168.122.1`，且网络 `192.168.122.0/24` 的节点使用网关 `192.168.122.10` 且启用了 IP 转发时，这种通信是可能的。

如果涉及一对多网络地址转换，意味着从一个网络的连接被重定向到另一个网络，则就需要伪装地址（masquerading）来执行该连接。图 8.14 展示了流量流和 IP 伪装过程：

![](img/bcd1b6709d1a6bc46b09b8587284794e_251_0.png)

# 图 8.14：IP 伪装图

所描述的两种防火墙解决方案（`firewalld` 和 `ufw`）都允许为区域或接口启用伪装。图 8.15 显示了如何使用 `firewall-cmd` 命令通过 `--add-masquerade` 启用它：
