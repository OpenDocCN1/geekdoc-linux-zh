
这条 ipchains 规则将拒绝（换句话说，丢弃）来自远程计算机的所有数据包。为了使此操作永久化，你可以将 ipchains 选项（从 -I 到行尾）添加到 /etc/sysconfig/ipchains 文件中，将 $TARGETS 替换为你要拒绝访问的计算机的实际 IP 地址。

- **KILL_HOSTS_DENY**：此选项用于拒绝由 TCP 封装保护的请求任何网络服务的请求。此选项的默认设置如下：

```
KILL_HOSTS_DENY="ALL: $TARGETS"
```

设置上述选项后，$TARGETS 将被入侵远程计算机的 IP 地址替换，并且引号内的行将被添加到 /etc/hosts.deny 文件中。例如，如果远程计算机的 IP 地址是 10.0.0.59，则出现在 /etc/hosts.deny 中的行将是：

```
ALL: 10.0.0.59
```

- **KILL_RUN_CMD**：除了使用防火墙、重路由或 TCP 封装来拒绝入侵计算机访问你的计算机外，你还可以选择任意你喜欢的命令作为响应。当 BLOCK_TCP 和 BLOCK_UDP 选项设置为 "2" 时，KILL_RUN_CMD 的值将在扫描你的受监控端口时运行。

KILL_RUN_CMD 的值应为你想要运行的脚本的完整路径，加上任何选项。若要包含远程计算机的 IP 地址或被扫描的端口号，可以分别包含 $TARGET$ 或 $PORT$ 变量。以下是你想要修改的示例外观：

```
KILL_RUN_CMD="/some/path/here/script $TARGET$ $PORT$"
```

> **注意**：不要使用任何 KILL_RUN_CMD 来报复入侵的远程主机。首先，扫描你端口的计算机本身可能已被破解，因此不是报复的有效目标；其次，报复可能只会激怒黑客对你发动进一步的攻击。

- **PORT_BANNER**：通过设置 PORT_BANNER 选项，你可以向触发 PortSentry 监视器的人发送消息。默认情况下，未定义任何消息。但是，你可以取消注释以下行以使用该消息。（不建议使用侮辱性消息。）

```
PORT_BANNER="*** 未经授权禁止访问 ***
你的连接尝试已被记录。请离开。"
```

PortSentry 在接受上述描述的响应之前可接受的来自入侵计算机的扫描次数，可以通过使用 SCAN_TRIGGER 选项进行设置。默认情况下，该选项设置如下：

```
SCAN_TRIGGER="0"
```

"0" 值表示你不容忍来自入侵系统的任何扫描。换句话说，第一次扫描就会触发 PortSentry 监视器。你可以增加此值以容忍一次或多次误扫描（尽管你可能不想这样做）。

## 修改 portsentry.modes 文件

`/etc/portsentry/portsentry.modes` 文件定义了启动时运行 PortSentry 命令的模式。该文件默认外观如下：

```
tcp
udp
#stcp
#sudp
#atcp
#audp
```

`tcp` 和 `udp` 选项分别是 TCP 和 UDP 服务的基本 PortSentry 模式。你的其他选项选择包括 *隐匿 TCP*（`stcp`）和 *高级隐匿 TCP*（`atcp`）以及 *隐匿 UDP*（`sudp`）和 *高级隐匿 UDP*（`audp`）。只运行一个 TCP 服务和一个 UDP 服务。因此，如果你取消隐匿或高级隐匿服务的注释，请确保在相应的基本服务前添加注释。

为了激活新服务，你随后需要执行以下命令：

```bash
# /etc/init.d/portsentry restart
```

新的 PortSentry 模式将立即生效。当你的计算机重新启动时，这些新模式也将生效。

## 测试 PortSentry

你可以通过不同的方式测试你的端口是否正确受保护。你需要运行潜在入侵者会运行的程序，看看它是否触发了 PortSentry 的相应响应。例如，你可以使用端口扫描器查看你的端口在外部世界中的外观。你还可以使用 `telnet` 等命令来尝试触发特定端口，以查看 PortSentry 是否捕获到它。

`nmap` 是扫描 TCP 和 UDP 端口的流行工具。你可以给 `nmap` 命令一个主机名或 IP 地址，它会扫描计算机上的约 1500 个端口，查看哪些端口是开放的（并假设这些端口提供可能被破解的服务）。

`nmap` 的 RPM 包也可用。你可以下载包含简单图形界面的 `nmap` 调用 `xnmap` 的 `nmap-frontend` 包。我建议你在运行 PortSentry 的系统上安装这些包，同时在你的局域网（LAN）上的另一个系统（如果可用）上也安装。然后在 PortSentry 系统上运行以下程序以进行测试：

1. 如果 PortSentry 正在运行，通过输入以下内容将其关闭：

```bash
# /etc/init.d/portsentry stop
```

2. 输入以下 `nmap` 命令以查看本地系统上哪些端口是开放的：

```bash
# nmap -sS -O 127.0.0.1
# nmap -sU -O 127.0.0.1
```

输出将显示你的计算机当前为 TCP 和 UDP 协议提供服务的端口。

3. 如果你不希望某些服务保持开放，你应该使用 `chkconfig service off`（将 *service* 替换为服务名称）关闭这些服务，或者编辑 `/etc/xinetd.d` 目录中代表该服务的配置文件，并将 `disable = no` 更改为 `disable = yes`。

4. 如果你希望某些服务可从你的计算机访问，请确保代表这些服务的端口号未被 PortSentry 监控。从 `/etc/portsentry/portsentry.conf` 文件中的 `TCP_PORTS` 和/或 `UDP_PORTS` 选项中移除端口号，否则 PortSentry 将报告该端口存在可能的隐匿扫描。

5. 如下重新启动 PortSentry：

```
# /etc/init.d/portsentry start
```

6. 按照前述描述再次运行 nmap。提供合法服务的端口以及被 PortSentry 监控的端口，都应该显示为开放状态。

7. 检查 `/var/log/messages` 文件，确保 PortSentry 没有尝试监控你正在提供服务的任何端口。

当你确定 PortSentry 已按你的喜好设置完毕后，从网络上的另一台计算机运行 nmap 命令。这次，将 127.0.0.1 替换为 PortSentry 计算机的名称或 IP 地址。如果一切正常，远程计算机在你的 PortSentry 计算机上扫描的第一个端口应阻止所有后续扫描。

## 跟踪 PortSentry 入侵

除了对入侵者采取行动外，PortSentry 还使用 syslog 工具记录其活动。PortSentry 的启动、关闭和扫描检测活动会被记录到你的 `/var/log/messages` 文件中。以下是该文件中 PortSentry 输出的示例。

```
portsentry[13259]: adminalert: Psionic PortSentry 1.0 is starting.
portsentry[13260]: adminalert: Going into listen mode on TCP port: 1
portsentry[13260]: adminalert: Going into listen mode on TCP port: 11
.
.
.
portsentry[13260]: adminalert: PortSentry is active and listening.
portsentry[]: attackalert: Connect from host:10.0.0.4 to TCP port: 31337
portsentry[]: attackalert: Connect from host: 10.0.0.4 to TCP port: 11
portsentry[]: attackalert: Host: 10.0.0.4 is already blocked. Ignoring
.
.
.
portsentry[13371]: securityalert: Psionic PortSentry is shutting down
portsentry[13371]: adminalert: Psionic PortSentry is shutting down
```

输出的第一部分显示 PortSentry 正在启动。随着 PortSentry 开始监听每个端口，该端口会在单独的日志消息中被记录。接下来的消息显示计算机正在被扫描。来自 10.0.0.4 主机的某人运行了 `nmap` 来扫描计算机上的端口。PortSentry 捕获了对端口 31337 的扫描并阻止了对其他端口的扫描尝试。

最后，最后一组消息显示 PortSentry 正在关闭。这是一个安全警报，因为除了你之外，其他人可能关闭 PortSentry 以掩盖他们已入侵的事实。

> **注意**：如果你一直在运行 Logcheck 包（前文所述），这些消息会显示在你每小时从 Logcheck 接收的电子邮件消息中。

## 恢复访问

如果对你希望拥有访问权限的计算机切断了访问，你可以检查以下几件事来纠正该问题：

- `/etc/hosts.deny`：查看该计算机的 IP 地址是否被错误地添加到此文件中。这将导致该 IP 地址的主机的网络服务被拒绝。
- `/var/portsentry/portsentry.blocked`：检查是否在该计算机的 IP 地址条目被添加到 `portsentry.blocked.udp` 或 `portsentry.blocked.tcp` 文件中。
- `route`：运行 `/sbin/route` 命令，查看来自该计算机的消息是否被重新路由到无响应的主机（可能是本地主机）。
- `ipchains`：运行 `ipchains -L` 命令，查看是否创建了新的防火墙来阻止来自该计算机的访问。

> **提示**：为了确保访问不会再次被切断，你可以将远程计算机的 IP 地址添加到 `/etc/portsentry/portsentry.ignore` 文件中。未来的不当扫描或服务请求将不会导致远程计算机被阻止。

## 摘要

随着互联网的兴起，安全已成为几乎所有计算机用户的关键问题。正确使用密码、安全配置网络服务以及监控日志文件是保持计算机安全的关键方式。

定期运行 Crack、Tiger 和 Tripwire 等应用程序，以确保你的系统保持安全。防火墙可以保护你的本地局域网（LAN）和公共互联网之间的边界。Logcheck 和 PortSentry 可以保护你的 Red Hat Linux 系统免受入侵。

