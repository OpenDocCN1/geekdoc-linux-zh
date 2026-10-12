
# iptables 规则

```
iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT

iptables -A FORWARD -m state --state ESTABLISHED,RELATED -j ACCEPT

# 允许 SSH
iptables -A INPUT -p tcp --dport 22 -j ACCEPT

# 允许 DNS
iptables -A INPUT -p udp --dport 53 -j ACCEPT
iptables -A OUTPUT -p udp --sport 53 -j ACCEPT
```

因此，这些规则开放了这些端口以双向访问，但有一个特殊之处：这些规则使用状态检测包检测（stateful packet inspection）来确保只有出站连接允许 `NEW` 数据包。在 `INPUT` 链中省略 `NEW` 状态，意味着运行在高端口上的服务器（普通用户可能会尝试这样做以绕过你的系统安全设置）将无法接受连接。这两条规则还限制了 `INVALID` 状态，这可以减少拦截和“劫持”已建立连接的概率。

本地 `SSH` 服务器流量：最后两次 `iptables` 的调用在防火墙上打开了一个缺口，允许本地计算机连接到 `SSH` 服务器。该服务器运行在端口 `22` 上，因此源自或发往本地（`172.24.1.0/24`）网络且针对该端口的流量将会被接受。结合客户端流量规则，这些规则首先采用首次包检查作为额外的预防措施。`INVALID` 数据包在两个方向都会被拒绝，而 `NEW` 数据包仅在输入数据包上被接受。

许多脚本定义了包含主机 IP 地址和本地网络地址的变量，然后它们会引用这些变量而不是直接使用它们，如列表 20.2 所示。这种做法在你的 IP 地址发生或脚本需要在多台计算机上运行时，极大地简化了脚本的修改。

## 使用 TCP Wrappers 拦截 IP 地址

包过滤防火墙基于 IP 地址和端口拦截访问非常有效，但它们并不是实现此目的的唯一工具。TCP Wrappers（在本节介绍）和 `xinet`（在接下来的章节“增强 `xinet` 限制”中介绍）是另外两种可以根据 IP 地址阻止访问的工具。在许多方面，TCP Wrappers 和 `xinet` 比包过滤防火墙不灵活。例如，它们可以阻止访问并非超级服务器启动或未设计为使用超级服务器的服务器，并且无法拦截针对客户端或由客户端发送的流量。尽管如此，TCP Wrappers 和 `xinet` 可以完成一些包过滤防火墙无法做的事情，例如根据远程用户的用户名进行记录和限制（如果远程系统运行 `inetd` 或等效服务器）。出于这些原因，并且由于安全性是分层实现的，你可能想要使用 TCP Wrappers 或 `xinet` 代替或 `iptables` 使用。

TCP Wrappers 最常用的用法是结合 `inetd` 超级服务器使用，这在第 22 节中有描述。极少数独立服务器（如 NFS 服务器）可以直接按现状使用它。虽然可以将 TCP Wrappers 与 `xinet` 超级服务器配合使用，但大多数不需要这样做，因为 `inetd` 包含了与 TCP Wrappers 类似的功能。默认使用 `inetd` 且因此对 TCP Wrappers 最为关键的发行版包括 `Debian`、`Slackware` 和 `Suisse`。

## TCP Wrappers 基础

TCP Wrappers 最常见的用法是结合 `inetd` 使用。`inetd` 不直接调用服务器程序，而是调用 TCP Wrappers（通过其 `tcpd` 可执行文件）并向其传递最终服务器程序的名称以及它所需的任何参数。TCP Wrappers 可以检查入站连接并决定是否接受它。如果连接被拒绝，TCP Wrappers 不会调用服务器，而是丢弃连接。如果 TCP Wrappers 接受连接，它会启动服务器并将连接交给它。

为了配置 TCP Wrappers，你需要在两个文件中提供接受或拒绝连接的依据：`/etc/hosts.allow` 和 `/etc/hosts.deny`。第一个文件定义了应该被授予访问服务器的计算机；第二个文件指定了不应连接的系统。如果一个系统同时列在两个文件中，则 `hosts.allow` 具有优先级。如果两个文件都没有列出某个系统，TCP Wrappers 将允许其连接。

提示：要运行具有最严格 TCP Wrappers 安全性的系统，请在 `/etc/hosts.deny` 中包含一行 `: ALL`。此行会阻止所有由 TCP Wrappers 处理的入站连接。然后你可以在 `/etc/hosts.allow` 中为特定的客户端系统开放单独的服务。

使用 TCP Wrappers 时，你通过文件名引用服务器，该文件名可能与其在 `/etc/services` 中的服务名不同。例如，FTP 服务器可能被引用为 `.ftp`、`vsftpd`、`proftpd` 或其他名称。当你结合 `inetd` 使用 TCP Wrappers 时，服务器名称会紧接着 `/etc/inetd.conf` 中该服务器行里对 `tcpd` 的调用出现。通常情况下，服务器必须位于 `tcpd` 路径上的某处。如果你需要在 `/etc/inetd.conf` 文件中包含服务器的路径，TCP Wrappers 的限制可能无法正常工作。如有必要，你可以从路径上的某个目录到实际执行文件创建一个符号链接。

## 使用 TCP Wrappers 限制访问

`/etc/hosts.allow` 和 `/etc/hosts.deny` 的格式相同，尽管相同的内容在两个控制文件中产生相反的效果。这些条目的通用格式如下：

`service-names : client-list : shell-command`

`service-names` 可以是一个服务器名称，如 `ftp` 或 `inetd`；也可以是多个名称，并用逗号或空格分隔。你还可以使用 `ALL` 关键字，它代表所有服务。可选的 `shell-command` 是你在尝试访问时运行的命令。你可以使用此功能向地址发送邮件通知、在端口上显示失败消息或采取任何其他操作。

`client-list` 比 `service-names` 复杂得多。与 `service-names` 类似，`client-list` 可以是单个条目或多个，用逗号或空格分隔。你可以以任何不同方式指定客户端：

- **IP 地址**：你可以提供单个 IP 地址（例如 `172.24.45.102`），以阻止或允许来自该 IP 的访问。
- **IP 范围**：如果你想根据 IP 范围阻止或允许整个网络的访问，可以这样做。最简单的方法是提供部分 IP 地址（以点结尾），例如 `172.24.45.*`，它会匹配 `172.24.45.0/24` 子网中的所有系统。你也可以提供完整的网络地址并使用斜杠添加位数或网络掩码，例如 `172.24.45.0/24` 或 `172.24.45.0/255.255.255.0`。
- **主机名**：如果你不想使用 IP 地址，可以通过提供主机名（如 `trex.pangaea.edu`）来阻止或授权单个计算机。然而，这种方法比使用 IP 地址风险更大，因为它依赖于成功且准确的 DNS 查找。
- **域名**：要根据域名阻止或授权访问，请列出名前加点的域名。例如，`.pangaea.edu` 阻止或授权 `pangaea.edu` 域中的所有计算机。对于主机名，这种方法依赖于可靠的 DNS。
- **NIS 网组名称**：如果你的网络运行网络信息服务 (NIS) 网组服务器，可以通过在名称前加 `@` 来指定网组名称。结合主机名和域名指定，这会让你的系统受控于他人。
- **通配符**：你可以使用几种通配符来匹配特定的计算机组。通配符的示例包括 `ALL`（所有计算机）、`LOCAL`（所有主机名解析到服务器相同域的计算机）、`UNKNOWN`（主机名或 IP 地址未知，或无法通过身份验证名的计算机）、`KNOWN`（主机名和 IP 地址已知且由客户端返回名的计算机）以及 `PARANO`（主机名和 IP 地址匹配的系统）。除了 `ALL` 之外，所有这些选项都有一定风险，因为它们依赖于适当的 DNS。
- **用户名**：你可以通过在主机名或 IP 地址前加上用户名和 `@` 符号来匹配单个用户，例如 `sue@pangaea.edu`。

除了这些规则外，你可能还可以使用 `EXCEPT` 关键字创建一个带有异常的列表。例如，`172.24.45.0/24 EXCEPT 172.24.45.72` 将 `172.24.45.72` 从列表中排除。

作为这些规则运行的示例，请考虑列表 20.3，它显示了一个 `/etc/hosts.allow` 示例。该文件应配合 `/etc/hosts.deny` 文件使用，后者限制部分或所有服务器的访问。如果配合空的 `hosts.deny` 文件使用列表 20.3，它将没有任何效果，因为没有系统会被拒绝访问。

列表 20.3: 示例 `/etc/hosts.allow` 文件

```
in.telnetd : 172.24.45.2 trex.pangaea.edu

vftpd : 172.24.45.1 EXCEPT 172.24.45.72

imap : .pangaea.edu EXCEPT router,pangaea.edu
```
