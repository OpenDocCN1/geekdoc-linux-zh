
安装 ntp 软件包。如果没有该软件包，执行 chkconfig ntpd on 命令将会导致错误信息。

有时存在互斥的替代方案。例如，对于 SMTP 服务，RHEL 6 允许配置 Postfix 或 sendmail 二者之一。在第 13 章中，你将研究另一种确保只有一个服务被设置为运行的方法。

当然，在考试中，可能会要求你确保某个服务在启动过程中不启动。而且在生产环境中，由于安全风险，在单个系统上安装如此多的服务是很少见的。

## 通过安全层审查访问

检查服务的第一个地方是从本地系统。例如，如果你能从该系统连接到 FTP 服务器，这就证实了该服务的良好配置。一些问题与 SELinux 有关；其他问题与各种基于用户和主机的防火墙有关。对于超出 SELinux 的问题，第 2 章中安装的网络命令工具会非常有帮助。

## 排查 SELinux 问题

如果配置良好但仍然无法工作，这就表明存在 SELinux 问题。并非所有 SELinux 问题都很容易被发现。然而，你可以针对 SELinux 检查两个基本问题：

- 与所讨论的配置选项相关的布尔设置列表。例如，尝试通过 FTP 服务器连接到远程主目录的用户可以通过主 vsFTP 配置文件进行配置。但是问题并不总是出现在 SELinux 日志中。
- SELinux 文件上下文。目标目录的上下文应与默认目录的上下文匹配。换句话说，当你在共享 FTP 目录上运行 ls -Z 命令时，文件上下文应与默认共享 FTP 目录的上下文匹配。

下一步是从远程系统测试连接。以多种方式测试连接是合适的：

- 1. 远程客户端系统能否与远程服务器通信？这最容易通过 ping 命令确认。
- 2. 远程客户端能否通过分配的端口通信？这可以通过 telnet 命令确认。例如，以下命令尝试在 TCP/IP 端口 21 上建立连接：

```
$ telnet 192.168.122.50 21
```

如果连接成功，vsFTP 服务器将以名称标识。输入 quit 命令并按 ENTER 退出连接。
- 3. 如果 telnet 连接到适当端口无法工作，则可能存在防火墙问题。实际上存在细微差异
  - a. 防火墙存在于多个层面。第 4 章和第 10 章中讨论的 iptables 命令防火墙，按 /etc/sysconfig/iptables 配置，必须支持通过所记录的端口号访问，并且不能从期望的主机限制它。
  - b. TCP Wrappers 系统与与 libwrap.so.0 库关联的守护进程一起工作，允许并限制 /etc/hosts.allow 和 /etc/hosts.deny 中的访问。

如果所有防火墙都已清除，而服务仍然无法按预期工作，则服务器可能存在配置问题。一些服务器包含基于主机、IP地址和用户名的自身限制。

## 排查基于 iptables 的防火墙问题

总体而言，基于 iptables 的防火墙很直接。如果系统允许服务器通信访问，你会在 /etc/sysconfig/iptables 文件中记录的端口号以及 iptables -L 命令的输出中看到它。
具体来说，你应该期望在 /etc/sysconfig/iptables 中看到如下类似的行，以允许通过 SSH 服务器的标准端口进行通信：

```
-A INPUT -m state --state NEW -m tcp -p tcp --dport 22 -j ACCEPT
```

当使用 /etc/init.d/iptables start 命令启动 iptables 服务时，文件会被读入内存；你应该能够从 iptables -L 命令中看到有关该端口的以下摘录：

```
ACCEPT tcp -- anywhere anywhere state NEW tcp dpt:ssh
```

让我们将该行翻译成更接近英文的内容。此规则接受数据包。它检查数据包是否使用 TCP 协议。然后它检查头部的 IP 地址，但允许来自任何地址、目标为任何地址的数据包。数据包是新的，其 TCP 目标端口（dpt）与 ssh 相关联。/etc/services 文件将 ssh 翻译为标准的 SSH 端口 22。

当然，你可以使用第 4 章和第 10 章中描述的防火墙配置工具，但如果这些工具有缺陷怎么办？对于基于 iptables 的防火墙，其核心在于所记录的文件以及使用 iptables -L 命令实现的方式。

除非防火墙中打开了此端口，否则尝试连接到该服务器的尝试会以如下类似的消息被拒绝：

```
ssh: connect to host server1.example.com port 22: No route to host
```

相比之下，telnet server1.example.com 22 命令会导致类似的消息：

```
telnet: connect to address 192.168.122.50: No route to host
```

## 排查 TCP Wrappers 防火墙问题

相比之下，如果服务受 TCP wrappers 保护，错误消息行为会不同。对于本节，我在 server1.example.com 系统上配置了 /etc/hosts.allow 和 /etc/hosts.deny 文件，仅允许 192.168.122.0/24 网络上的 .example.com 系统访问。这意味着不允许来自 IP 地址为 192.168.100.100 的 outsider1.example.org 等系统访问。

在这种情况下，当我尝试使用 ssh 命令访问 server1.example.com 系统时，收到了以下错误消息：

```
ssh_exchange_identification: Connection closed by remote host
```

相比之下，从同一系统执行的 telnet server1.example.com 22 命令返回以下消息，稍作停顿：

```
Trying 192.168.122.50
Connected to server1.example.com.
Escape character is '^]'
```

短暂几秒钟后，系统似乎即将连接。但随后 TCP Wrappers 的阻止导致以下消息：

```
Connection closed by foreign host.
```

## EXERCISE 11-2

### 审查 iptables 和 TCP Wrappers 的不同效果

此练习假设有一个可操作的 vsFTP 服务器，类似于第 1 章安装时配置的服务器。假设你将在 server1.example.com 系统上配置该 vsFTP 服务器。然后你将确保防火墙阻止标准 vsFTP 端口 21 上的流量，然后从远程被阻止系统 outsider1.example.org 检查效果。回顾一下，这些系统按第 1 章和第 2 章配置的 IP 地址分别为 192.168.122.50 和 192.168.100.100。

然后你将打开端口 21 的防火墙，然后使用 TCP Wrappers 限制访问。此练习步骤很多；事实上，每个编号步骤都需要多个命令或操作。在某些情况下，所需命令是隐含的。例如，由于防火墙配置工具有两个版本，所需的确切步骤会有所不同。

- 1. 如果尚未安装，请按本章所述安装 vsFTP 服务器。确保该服务器已通过 `/etc/init.d/vsftpd start` 命令处于活动状态。
- 2. 使用 `system-config-firewall` 命令启动防火墙管理工具。确保受信任服务列表中未激活 FTP。确保应用更改然后退出防火墙管理工具。
- 3. 尝试使用类似 `lftp localhost` 的命令从本地系统连接到 vsFTP 服务器。它应该可以工作，你可以通过 `lftp localhost:/>` 提示符使用 `ls` 命令确认。退出 vsFTP 服务器时使用 `quit` 命令。
- 4. 移动到 outsider1.example.org 系统。通过 SSH 连接是可接受的；事实上，在考试中（以及现实生活中）这可能是连接到该系统的唯一方法。
- 5. 使用 `ping 192.168.122.50` 命令 ping 具有 vsFTP 服务器的系统。记得按 `CTRL-C` 停止进程。使用 `lftp 192.168.122.50` 命令尝试连接到 vsFTP 服务器。会发生什么？使用 `telnet 192.168.122.50 21` 命令尝试连接到该系统。会发生什么？
- 6. 返回 server1.example.com 系统。再次打开防火墙配置工具，这次将 FTP 设为受信任服务。不要忘记在退出防火墙配置工具之前应用更改。

