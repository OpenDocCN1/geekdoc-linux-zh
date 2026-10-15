
```
23:17:16.938256 IP 20.101.240.13.microsoft_tcp.local.(443) > 192.168.1.156.54382: length 54, flags [ACK]

23:17:17.018648 IP 192.168.1.156.54382 > 20.101.240.13.microsoft_tcp.local.(443): length 54, flags [ACK]

23:17:17.019198 IP 20.101.240.13.microsoft_tcp.local.(443) > 192.168.1.156.54382: length 54, flags [PSH, ACK]

23:17:17.022289 IP 192.168.1.156.54382 > 20.101.240.13.microsoft_tcp.local.(443): length 54, flags [ACK]

23:17:17.022289 IP 20.101.240.13.microsoft_tcp.local.(443) > 192.168.1.156.54400: length 54, flags [ACK]

23:17:17.011863 IP 192.168.1.156.54400 > 20.101.240.13.microsoft_tcp.local.(443): length 54, flags [ACK]

23:17:17.113795 IP 20.101.240.13.microsoft_tcp.local.(443) > 192.168.1.156.54400: length 54, flags [PSH, ACK]

23:17:17.113795 IP 192.168.1.156.54400 > 20.101.240.13.microsoft_tcp.local.(443): length 54, flags [ACK]

23:17:17.113795 IP 20.101.240.13.microsoft_tcp.local.(443) > 192.168.1.156.54412: length 54, flags [ACK]

23:17:22.394649 IP 192.168.1.156.54412 > 20.101.240.13.microsoft_tcp.local.(443): length 54, flags [ACK]

23:17:22.394649 IP 20.101.240.13.microsoft_tcp.local.(443) > 192.168.1.156.54412: length 54, flags [PSH, ACK]

- 捕获了 10 个包
- 系统丢弃了 0 个包
- cesarmer@localhost$ ~
```

图 5：网络包捕获

此图展示了捕获，这是监控和分析网络流量的关键技术。通过记录网络传输的数据，管理员可以检查协议、源和目的地址以及包内容。包捕获对于诊断连接问题、识别安全威胁和调整性能至关重要。在 Rocky Linux 9 中，`tcpdump` 和 `Wireshark` 等工具提供了捕获和分析流量的强大能力。

## 管理网络工具

在本节中，我们探索了构成有效系统管理的一系列网络工具。这些工具对于 Rocky Linux 9 中的配置、管理和网络连接排除至关重要。基础命令如 `ping` 允许管理员验证基本连接，而 `ip` 为接口配置和路由提供了强大的选项。对于深入检查，`tcpdump` 等工具能够实现详细的流量分析和包级诊断。维护安全稳定的网络环境不仅需要反应性措施，定期检查和更新网络设置、审计防火墙规则有助于整体可靠性和性能。通过持续使用这些工具，管理员可以确保各种环境下的网络操作运行。

## 防火墙与 `Firewalld`

`firewalld` 是 Rocky Linux 9 中的默认防火墙管理工具，提供了对流量的动态和灵活控制。与静态防火墙不同，`firewalld` 允许在不需要重启服务的情况下实时更改，这在可用性性环境中特别有用。它利用基于区域的方法，允许管理员为网络连接定义不同的信任级别。将接口分配到 public、home 或 internal 等区域，可以满足每个环境的安全需求，提供精确的入站和出站流量控制。其关键功能包括支持 IPv4 和 IPv6、运行时和永久配置以及定义高级自定义规则的能力。在 Rocky Linux 9 中安装和配置 `firewalld` 非常简单，涉及与系统工具的集成以及对 DBus 的支持。通过利用防火墙的能力，管理员可以实施结构化的流量管理方法，确保系统防护。

### `firewalld` 的初始设置与配置

在 Rocky Linux 上使用 `firewalld`，请确保它已安装并运行。首先，我们将使用以下命令验证安装：`sudo dnf install firewalld`。

```bash
$ sudo dnf install firewalld

上次元数据过期时间：2025年5月3日 星期六 06:24:36 CST 前。

已解析依赖：

Package                Version             Repository      Size

安装:             firewalld           1.3.4-9.el9    base            452 k

升级:              0

删除依赖项: 0

总下载大小:      404 k

正在安装依赖项:

  firewall-filesystem   1.3.4-9.el9_5    base            8.6 k

  libfirewalld           x86_64             7.111-3.el9     base            41 k

  system-libs             7.111-3.el9     base            68 k

  dbus-libs             7.111-3.el9     base            35 k

  policy-core          x86_64             1.1.0-3.el9      base            201 k

安装弱依赖项:

  firewalld               0.8.2-79           appstream       29 k

事务摘要:

安装                7 个包

升级                0 个包

下载              1 个包

总下载大小:1.4 M

(1/1) firewall-filesystem-1.3.4-9.el9_5.rpm   70 kB/s / 8.6 kB  00:00
```

> 图 5.19：防火墙安装

这展示了如何使用 `firewalld` 在 Rocky Linux 上安装和激活防火墙。该过程首先验证防火墙包是否已安装，如果没有，则通过 TNF 包管理器安装。安装完成后，使用 `systemctl` 命令启用并启动服务。

激活后，`firewalld` 提供了一种动态且高效的方法来管理防火墙规则、服务和网络区域——允许在不重启服务的情况下进行实时更改。此外，启用防火墙自动启动可以确保持续且持久的网络保护。

### 1. 启动并启用 `firewalld`：

```bash
sudo systemctl start firewall
sudo systemctl enable firewall
```

在 Rocky Linux 上启动并启用防火墙的过程。安装完成后，启动防火墙服务以激活它并开始管理流量至关重要。启用防火墙确保它在每次系统启动时自动运行，维护一致的网络安全。该过程通常涉及使用 `systemctl` 命令，例如 `systemctl start firewall` 启动服务，`systemctl enable firewall` 确保其在启动时启用。这些步骤确保防火墙始终运行，保护系统免受未经授权的访问。

### 2. 检查防火墙状态：

```bash
sudo systemctl status firewall
```

```
[asmerver@local ~]$ sudo systemctl status firewall

firewall.service - dynamic firewall daemon

Loaded: loaded (/lib/systemd/system/firewall.service; enabled; preset: enabled)

Active: active (running) since 2023-03-03 18:51:21 UTC; 45s ago

Duration:0min

Docs: firewall(1)

Main PID: 4893 (code, status=SUCCESS)

CPU: 1.152s
```
