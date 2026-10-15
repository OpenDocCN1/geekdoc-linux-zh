
如你所见，通过 `finger` 可以获得大量信息（这也是建议关闭 `in.fingerd` 的原因之一）。由于 `spawn` 允许任意 shell 命令，因此可以根据提供的规则采取多种操作。例如，我们可能会将示例 10-17 中的 `/bin/mail` 调用替换为其他命令，例如一个记录特定用户未授权连接尝试次数的脚本，当达到阈值（如三次此类尝试）时，执行某个操作，如向管理员发送寻呼或关闭特定服务。事实上，公共领域中确实存在这样一个脚本——它被称为 `spawch`——我们将在第 17 章中探索其功能。

### 使用 twist

`twist` 选项会导致调用指定的守护进程或命令，而不是 `/etc/inetd.conf` 中指示的守护进程。例如，如果 `/etc/inetd.conf` 中有如下条目

```
ftp  stream  tcp     nowait  root  /usr/sbin/inetpd  in.ftpd  -a -l
```

那么，通常，每当遇到成功的 `ftp` 请求时，将调用 `/usr/sbin/in.ftpd -l -a`。假设您已为内部使用配置了匿名 `ftp` 环境（有关匿名 `ftp` 服务器的更多信息，请参阅第 255 页 *Internet Services Resources* 中引用的资源）。进一步假设，您的内部安全策略要求所有系统运行 `identd`，但它也指定内部对 `ftp` 服务器（如上述示例中的服务器）的访问对生产力至关重要。为了满足此标准，您可以实现 `TCP_wrappers` 根据给定用户是否可识别而采取不同的操作；您还可以如示例 10-19 所示，根据特定用户身份的可可用性调用不同的守护进程。正如第 206 页的表 10.5 中所述，如果用户身份已知，`tcpd` 将报告 `KNOWN`；如果未知，则报告 `UNKNOWN`。请注意示例 10-19 中两个 `in.ftpd` 规则中 `@KNOWN` 的使用。回顾第 206 页的表 10.5，对于客户端列表，只有当主机名和 IP 地址都已知时才会匹配。因此，主机名的结果为 `UNKNOWN` 可能意味着主机名解析服务没有正常工作。该选项的存在强制进行反向查找（无论编译时选项如何；参见第 196 页的 *Building TCP_Wrappers*）。此外，在示例 10-19 中，我们看到了 `/etc/hosts.allow` 文件中的条目，它以以下方式区分已知和未知用户。由于条目 `KNOWN@UNKNOWN` 的存在，每当发生传入的 `ftp` 请求时，`tcpd` 将生成一个 `RFC931` 调用（无论编译时选项如何）以获取传入的用户名。如果成功，则规则匹配，并从编译时守护进程源目录（在 Red Hat 5.2/6.0 的情况下为 `/usr/sbin`）调用 `in.ftpd -a -l`。请注意，`in.ftpd` 的 `-l` 标志导致 `in.ftpd` 记录连接，而 `-a` 标志导致 `in.ftpd` 检查 `/etc/ftpaccess` 文件。有关更多信息，请参见第 255 页 *Internet Services Resources* 中引用的参考文献和 `ftpd(8)` 手册页。

### 示例 10-19 使用 twist 的样本 /etc/hosts.allow

```
# hosts.allow

KNOWN@UNKNOWN

in.ftpd: UNKNOWN@KNOWN: banners \
	/bin/echo "Policy Violation!" \
	| /bin/mail -s "$(h isn't running ident)" root@$(h),root@$(h); \
	twist PATH=/usr/sbin/extra/exec in.ftpd -l -o -1

in.ftpd: PARANOID: banners /etc/security/banners/paranoid; \
	spawn (/bin/echo "$(h reported being %$(h connected using '$)" | \
	/bin/mail -s "Alert! Hostname Lookup Failure!" root@&h); deny

in.ftpd: ALL: deny
```

另一方面，如果对客户端的用户名请求失败，用户名将解析为 `UNKNOWN`。在这种情况下，连接仍被允许，但会显示一个特殊的横幅（可能通知用户客户端上未运行 `identd`），并向服务器上的 `root`（`root@$(h)`）和客户端上的 `root`（`root@$(h)`）发送电子邮件，通知管理员已发生安全策略违规。最后，我们可以看到 `twist` 选项的使用，它导致调用 `/usr/sbin/extra/exec in.ftpd -l -o -1` 而不是 `/usr/sbin/in.ftpd -a -l`。使用 `/usr/sbin/extra`（它是

...此处仅用于举例说明其功能）会导致目录路径的变化，并且仅当您要调用的守护进程不在 `/usr/sbin` 中时才需要该路径（Red Hat 5.2/6.0 的默认情况）。请注意，`in.ftpd` 的 `-l` 和 `-o` 标志分别会导致上传和下载的文件默认记录到 `/var/log/xferlog`。

接下来，在示例 10-19 中，如果客户端在服务器上解析为 `PARANOID`（IP 地址的反向查找与主机名的正向查找不一致），`tcpd` 会向客户端显示一条特殊消息，发送电子邮件通知管理员此问题，然后使用 `deny` 关键字拒绝访问。在内部环境中，如本例所示，`PARANOID` 报告很可能表明存在网络故障；尽管如此，此类报告仍应始终进行彻底调查。在这些文件中使用 `PARANOID` 假设在编译时未选择 `-D PARANOID` 选项（Red Hat 5.2/6.0 的情况即是如此）。最后，示例的最后一行在其他任何情况下都拒绝 `ftp` 访问。

## 将 TCP Wrappers 规则压缩到一个文件中

在前一节中，我们看到了 `/etc/hosts.allow` 文件中 `deny` 选项的使用。使用此选项以及 `allow` 选项，允许您构建一个用于访问控制的单一文件。在规则相对简单的情况下，这种方法可能是一种便利。对于更长的规则集，例如为主要服务器系统配置的规则，使用典型的两个文件系统进行组织可能更容易。

示例 10-20 展示了一个单文件访问控制列表的简单示例。在这种情况下，使用的是 `/etc/hosts.allow`。注意关键字 `LOCAL` 的使用。这将匹配名称中不包含“.”的任何主机。由于这是一个允许文件，其行为是允许匹配的条目。最后一个条目通过 `deny` 关键字覆盖了此行为。您可以在拒绝文件中实现相同的效果，使用适当的 `allow` 关键字。无论您使用 `deny` 还是 `allow` 关键字，它必须出现在规则的最后。

### 示例 10-20 单文件访问控制列表

```
# hosts.allow file
# Internal systems only allow telnet and ftp
in.ftpd: LOCAL: banners /etc/security/banners/allow
in.telnetd: LOCAL: banners /etc/security/banners/allow
ALL: ALL: banners /etc/security/banners/deny: deny
```

这些关键字的另一个用途是在一个文件中保持复杂的规则集，如第 212 页的示例 10-19 所示。在这种情况下，所有关于 `in.ftpd` 的规则都在一个位置维护，使其更容易理解和故障排除。

## 区分多宿主服务器的源接口

您可能正在组建一个具有多个网络接口的单一 `ftp` 服务器。在这种情况下，您可以使用 `TCP_wrappers` 根据请求数据包中使用的目的 IP 地址（在 `TCP_wrappers` 文档中称为服务器端点模式）来定向守护进程调用。示例 10-21 给出了一个非常简单的例子。在此示例中，我们使用 `daemon@address` 形式；然而，可以使用第 203 页表 10.2 中描述的任何客户端形式来替代 IP 地址。这是使传入的 `ftp` 请求基于目的 IP 地址获得服务的一种方式。

### 示例 10-21 使用服务器端点模式的示例允许条目

```
# hosts.allow
# ftp server entries
in.ftp@24.1.11.113: ALL EXCEPT .evill.com: twist in.ftpd
in.ftpd@24.2.8.118: ALL EXCEPT .evill.com: twist in.wuftpd
```

> **注意**

> 您不能在客户端列表中的网络编号使用 `EXCEPT`。例如，`172.17.1.1 EXCEPT 172.17.1.3` 将不会产生预期的行为。

### 综合应用

构建 `hosts.allow` 和 `hosts.deny` 文件需要一些考虑。您最终可能会根据特定系统的用途获得多种配置——典型的桌面系统可能具有非常简单的访问控制列表；服务器系统将具有稍微复杂的列表；暴露于不受信任网络（如互联网）的系统可能具有高度专业化的列表。
