
`systemctl status firewalld`

输出如下屏所示：

```bash
[root@ol8 ~]# systemctl status firewalld

* firewalld.service - firewall dynamic daemon

Loaded: loaded (/usr/lib/systemd/firewall.service; enabled; vendor preset: enabled)

Active: active (running) since Tue 2023-04-04 22:23:14 EDT; 1min 10s ago

Main PID: 841 (firewall20)

Tasks: 2 (limit: 4020)

Memory: 941.0M

CGGroup: /system.slice/firewall.service

-541 /usr/libexec/platform-python -s /usr/sbin/firewalld --nofork --nopid
```

Apr 04 22:23:13 ol8.m57.local systemd[1]: Starting firewall - dynamic daemon...

图 9.16 - 防火墙状态

## 如何操作...

你可以使用 `firewall-cmd` 的 `--list-all` 选项查看当前配置：

```bash
[root@ol8 ~]# firewall-cmd --list-all
```

这将向你显示信息：

```text
[root@ol8 ~]# firewall-cmd --list-all
public (active)
target: default
icmp-block-inversion: no
interfaces: enp0s3 enp0s8
sources:
services: cockpit dhcpv6-client ssh
ports:
protocols:
forward: no
masquerade: no
forward-ports:
source-ports:
icmp-blocks:
rich rules:
```

图 9.17 - `firewall-cmd --list-all`

上述命令的输出显示了 Linux 系统上由 `firewalld` 管理的活动防火墙规则和配置的全面摘要。输出分为几个部分：

- `public (active)`：此行显示活动防火墙区域的名称，在本例中，该区域为公用区域（public）。`Target: default` 存在，这表示这是默认区域且当前正处于激活状态。
- `interfaces`: enp0s3 enp0s8：此行显示分配给活动防火墙区域的网络接口。在本例中，enp0s3 和 enp0s8 接口都被分配到了公用区域。
- `sources`：此行显示允许访问防火墙区域的 IP 地址或网络范围。如果没有定义源，此行将为空。
- `services`: cockpit dhcpv6-client ssh：此行列出允许访问防火墙区域的服务。在本例中，允许进入 cockpit、dhcpv6-client 和 ssh 服务的入站流量。
- `ports`：此行显示允许访问防火墙区域的 TCP 和 UDP 端口。如果没有定义端口，此行将为空。
- `protocols`：此行显示在协议级别管理的协议，例如 TCP/UDP/ICMP。
- `forward`: no：此行指示防火墙区域是否启用了转发功能。
- `masquerade`: no：此行指示防火墙区域是否开启了伪装（masquerade）。伪装允许来自一个网络的数据包看起来像是来自另一个网络网络。
- `forward-ports`：此行显示为防火墙区域定义了哪些转发端口。转发端口允许特定端口的入站流量重定向到不同的端口或 IP 地址。
- `source-ports`：此行显示为防火墙区域定义的任何源端口。源端口允许来自特定端口的入站流量重定向到不同的端口或 IP 地址。
- `icmp-blocks`：此行显示防火墙拦截的任何互联网控制消息协议（ICMP）数据包。ICMP 数据包用于网络诊断和故障排除。
- `rich rules`：此行显示为防火墙区域定义的任何规则。富规则（Rich rules）允许使用类似于 iptables 语法来定义更复杂的规则。

添加新规则非常简单。可以使用服务名称（在 `/etc/services` 中找到）或端口号添加规则。最常见的任务是添加常用的用户服务，例如 mysql。这通过在命令中添加 `--add-service` 选项来实现。添加服务后，除非添加 `--permanent` 选项，否则配置在重启后不会生效。一些常见示例如下：

```bash
firewall-cmd --permanent --add-service=http
firewall-cmd --permanent --add-service=imap
firewall-cmd --permanent --add-service=pop
firewall-cmd --permanent --add-service=mysql
```

此外，你可以指定允许服务的协议和端口。以下是添加 TCP 或 UDP 端口的示例：

```bash
firewall-cmd --permanent --add-port=1521/TCP
firewall-cmd --permanent --add-port=6900/UDP
```

你也可以使用 `--remove-port` 或 `--remove-service` 选项移除端口或服务：

```bash
firewall-cmd --permanent --remove-service=pop
firewall-cmd --permanent --remove-port=6900/UDP
```

完成更改后，你需要重新加载防火墙规则。这通过 `--reload` 选项实现：

```bash
firewall-cmd --reload
```

# 工作原理...

`firewall` 基于 `netfilter` 框架，该框架是一组钩子（`hooks`），允许内核对网络包进行过滤。该框架用于在许多 Linux 系统上实现 `iptables` 防火墙。`firewall` 提供了更高层次的抽象，允许管理员通过服务、端口和协议定义规则，而不是直接操作 `iptables`。`firewall` 的优势之一是允许根据区域（`zones`）来定义规则，每个区域都有特定的安全级别。

## 保持 SELinux 激活

`SELinux`（Security-Enhanced Linux）是一个提供强制访问控制（MAC）策略的内核模块。它通过限制进程可以的操作增加了额外的安全层。本教程将介绍如何创建自定义 `SELinux` 策略而不是禁用它，以及如何允许服务绑定低端口（`<1024`）。

## 准备工作

与其他测试一样，我们需要一个 Linux 系统进行操作。系统默认启用。要查看 `SELinux` 状态，可以使用 `getenforce` 命令。该命令将返回当前状态：

- `enforcing`：`SELinux` 处于激活并拦截活动
- `permissive`：`SELinux` 已启用，但不拦截活动
- `disabled`：`SELinux` 已禁用

如果你通过 `dnf` 安装了 `setools`，则可以使用额外的命令：

```bash
dnf install setools-console
```

你还应该使用 `sestatus` 命令获取有关 `SELinux` 的更多信息：

```text
[root@localhost8]# sestatus
SELinux status: enabled
SELinux mount: /sys/fs/selinux
SELinux root directory: /etc/selinux
Loaded policy name: targeted
Mode: enforcing
Mode from config file: enforcing
Policy MLS unknown status: allowed
Memory protection checking: actual (secure)
Max kernel policy version: 31
```
