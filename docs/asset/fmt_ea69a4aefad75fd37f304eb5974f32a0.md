
如果你回到 `Security Configuration` 窗口并点击 `SELinux` 标签，然后展开到 `Modify SELinux Policy`，你将看到一组用于切换各种 `SELinux` 设置的选项。这些选项只是用于在 `SELinux` 策略文件中切换设置的有限预配置选择。对于任何严肃的配置，你将需要手动编辑文件。你也可以从 `SELinux Policy Editor Project` (`http://seedit.sourceforge.org/index.html`) 下载第三方的 `SELinux` 策略编辑器。该包包含了一组简化的工具，比普通策略工具稍微少一点点。然而，你可以在两者之间切换。

通过通过审查日志，你可以看到哪些操作被拒绝了。如果你发现合法的活动被阻止，可以调整策略以允许它。这是微调 `SELinux` 策略的关键部分。

## TCP/IP 栈加固

通过配置 `TCP/IP` 栈，你可以加固系统以防止各种网络攻击。这通常使用 `sysctl` 命令完成，允许你在运行时修改内核参数。要使这些更改持久化，你必须将它们添加到 `/etc/sysctl.conf` 文件。以下是你可能考虑调整的一些常用参数：

- `net.ipv4.tcp_synack_retries`: 尝试完成三次握手时的重传次数；数字越小抗攻击能力越强。
- `net.ipv4.tcp_max_syn_backlog`: 队列中可以存在的半打开连接数；数字越大抗攻击能力越强，但会消耗内存。
- `net.ipv4.icmp_echo_ignore_broadcasts=1`: 告诉系统不要响应广播地址的 ping。此值本身就是默认值。
- `net.ipv4.conf.all.accept_redirects=0` & `net.ipv4.conf.all.send_redirects=0`: 告诉系统不要监听 `ICMP` 重定向，这可能被更改路由表。
- `net.ipv4.conf.all.accept_source_route=0`, `net.ipv4.conf.all.forwarding=0` and `net.ipv4.conf.all.me_forwarding=0`: 这些设置共同禁用了源路由，源路由除了攻击尝试很少使用。
- `net.ipv4.conf.rp_filter=1`: 告诉系统当源和目的与进入接口不符时丢弃数据包。
- `net.ipv4.conf.tcp_syncookies=1`: 启用 `SYN` cookie，允许在不使用监听队列的情况下建立。如果启用了此设置，`net.ipv4.tcp_max_syn_backlog` 设置将无效。

要立即应用这些更改，你可以使用以下命令：

```bash
sysctl -w net.ipv4.tcp_synack_retries=3
```

默认值为 5，将其设置为 3 只会导致更少的超时。其他值也是可能的，但请谨慎使用。

## 自动化加固脚本

由于有许多设置需要调整和配置，很容易漏掉步骤。因此，许多人开发了半自动脚本来帮助加固 Linux 系统。

![](img/33fc180c04c8f96c022bce6e62ae12fd_376_0.png)

# Linux 堡垒机 • 第 10 章

`Cadillac` 加固脚本即是 `Bastille-Linux`。它已经从一个粗糙的基础脚本演变成一个带有 `GUI` 界面的经过完善的加固系统。`Bastille` 目前支持 `Red Enterprise Linux`、`Fedora Core`、`SuSE`、`Debian`、`Gentoo` 和 `HP-UX`，并正在开发 `Mac OS` 版本。你可以在 `www.bastille-linux.org` 读取关于 `Bastille` 的信息并下载。

你可以向 `Bastille` 传递三个选项，每个选项都会告诉它在不同的模式下运行。如果你使用 `bastille-report`，系统将为你的主机当前的“加固”状态生成一个 `Web` 报告。`-c` 选项将在文本模式下运行实际的加固脚本，而 `-x` 将在图形模式下运行，如图 10.9 所示。

## 图 10.9 Bastille 图形配置

![](img/33fc180c04c8f96c022bce6e62ae12fd_377_0.png)

你对 `Bastille` 要做的就是启动它，它将提出一系列你必须用“是”或“否”回答的问题。根据你的选择，`Bastille` 将自动配置各种安全设置。这些设置包括从某些程序（例如 `shell`）中移除 `SUID` 位、更改用户账户等。脚本通常会将最安全的选项作为默认选择，除非某些选择对影响正常功能具有高风险的情况下。当你回答完这些问题后，系统会提示你选择是否保存生成的 `Bastille` 配置。然后，系统会提示你选择是否想要应用该配置。

`www.syngress`

### 控制对资源的访问

到目前为止，的大多数步骤都集中在控制用户如何与堡垒机交互上。到目前为止的大多数步骤都是假设用户已经有了到堡垒机的连接，从该连接开始，程序的 `SUID` 位被设置到它们所使用的安全上下文，以及可用的服务。遵循深度防御的哲学，接下来的步骤是限制谁可以与堡垒机交互。通过限制谁可以与堡垒机进行通信，除了限制他们在建立通信后能做什么之外，我们更接近于一个防黑客攻击的系统。

## 基于地址的访问控制

从网络角度来看，限制访问的最方法是基于外部系统的 `IP` 地址。传统的防火墙属于这一类。在本节中，我们将讨论一些可以根据相关系统的 `IP` 地址限制访问的方法。

## 配置 TCP Wrappers

`TCP Wrappers` 的功能与防火墙类似，不同之处防火墙是根据数据包 `IP` 头中包含的数据来允许或拒绝流量，而 `TCP Wrappers` 则是过滤对其运行的主机上服务的访问。针对 `libwrap` 库编译的服务将使用 `TCP Wrappers`。当启用 `TCP Wrappers` 时，`TCP Wrappers` 尝试访问给定的服务的行为将与 `/etc/hosts.allow` 文件和 `/etc/hosts.deny` 文件进行比较。规则将按顺序检查，并在找到匹配项时停止处理规则。例如，如果你只想允许来自 `Synergy.com` 的连接到堡垒机的 `SSH`，同时拒绝所有其他尝试，那么在你的 `hosts.allow` 和 `deny` 文件中将如下所示：

```text
/etc/hosts.allow
sshd :synergy.com
```

```
/etc/hosts.deny
sshd : ALL
```

这两个文件接受几个通配符，例如 `ALL`、`LOCAL`、`KNOWN`、`UNKNOWN` 和 `PARANOID`。你也可以在规则文件中启用日志记录，并配置日志条目的设施（facility）和严重性（severity）。由于 `TCP Wrappers` 功能有限且语法简单，你可能会奇怪为什么不直接使用 Linux 防火墙 `IPTables` 而要用它。因为 `IPTables` 在数据包级别工作，如果你想拒绝对进程（如 `HTTP`）的访问，你必须基于端口号。所以如果你使用 `IPTables` 显式阻塞对 80 端口的尝试，而 `Web` 服务器告诉它监听 8080 端口，则连接将被允许。而在 `TCP Wrappers` 中，你允许或拒绝对一个进程的访问。如果你有一个服务使用了大量的监听端口，或者某种根据需要而创建的服务类型，并且如果数据包被封装在另一种协议中，导致无法通过端口号进行识别，这种区别可能证明是无价的。

![](img/33fc180c04c8f96c022bce6e62ae12fd_378_0.png)

## 配置 IPTables

`IPTables` 几乎每一个 Linux 发行版。它是一个功能非常强大的防火墙，具有一系列令人深刻的功能和选项。要启用 `IPTables` 防火墙，只需导航到 `System | Administration | Security Level and Firewall`。在 `Firewall Options` 选项卡上，确保它是 `Enabled`，如图 10.10 所示。

## 图 10.10 启用 IPTables 防火墙

![](img/33fc180c04c8f96c022bce6e62ae12fd_379_0.png)

取决于你选择的发行版，`IPTables` 的默认规则集可能会不同。在 `Fedora Core 5` 的情况下，默认规则集是允许所有出站流量并允许作为建立会话部分的入站流量。正如图 14.10 所示，`SSH`了 `SSH`。由于默认配置阻止了所有入站连接尝试，勾选该框将创建一个规则来允许 `SSH` (`TCP 22`) 的入站连接。除了预配置的端口（服务）之外，你可以在 `Other ports` 部分添加你的自定义端口。

# 图 10.12 主启动器控制台

![](img/33fc180c04c8f96c022bce6e62ae12fd_382_0.png)

### 审计资源访问

审计在网络安全中起着重要作用。它不仅能让你实时了解系统上发生了什么，还允许你在事件发生后对其进行追溯，这在发生成功攻破后尤为重要。你基本上有两种类型的审计：一种是*内核*（kernel）审计，它会记录系统调用；另一种是*syslog*，它可以记录其他所有内容。

## 启用审计守护进程
