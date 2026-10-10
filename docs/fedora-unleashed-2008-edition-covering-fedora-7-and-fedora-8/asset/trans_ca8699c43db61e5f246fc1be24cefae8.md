

最后，请注意物理安全。如果潜在的攻击者能够获得你系统的物理访问权限，获取完全访问权限就变得轻而易举。将所有服务器存放在上锁的房间里，并确保只有授权人员才能访问客户端。

## 配置和使用 Tripwire

Tripwire 是一种安全工具，用于检查正常系统二进制文件的完整性，并通过 syslog 或电子邮件报告任何更改。Tripwire 是一个确保你的二进制文件未被木马程序替换的好工具。*木马*是恶意程序，由于与分发（预期）程序的文件名相同而被意外安装，它们可能在被入侵的系统上造成严重破坏。

Fedora 不包含 Tripwire 的免费版，但可以使用它来监控系统。要首次设置 Tripwire，请访问 *http://www.tripwire.org/*，然后下载并安装该软件的一个开源版本。安装后，以 root 身份运行位于 `/etc/tripwire` 目录下的 `twinstall.sh` 脚本，如下所示：

```
# /etc/tripwire/twinstall.sh
=============================================
The Tripwire site and local passphrases are used to
sign a variety of files, such as the configuration,
policy, and database files.

Passphrases should be at least 8 characters in length
and contain both letters and numbers.

See the Tripwire manual for more information.

=============================================
Creating key files...

(When selecting a passphrase, keep in mind that good passphrases typically
have upper- and lowercase letters, digits, and punctuation marks, and are
at least 8 characters in length.)

Enter the site keyfile passphrase:
```

然后你需要输入一个至少八位字符的密码（也许最好是一个随机字符串，如 *5fwwc4lm*）至少两次。脚本生成你的站点（主机）的密钥，然后要求你输入一个本地使用的密码（两次）。随后，你会被要求输入新的站点密码。按照提示操作后，（相当庞大的）默认配置文件和策略文件（`tw.cfg` 和 `tw.pol`）会被加密。然后你应该备份并删除由 Fedora RPM 包安装的原始纯文本文件。

接着，要初始化 Tripwire，请像这样使用其 `--init` 选项：

```
# tripwire --init

Please enter your local passphrase:

Parsing policy file: /etc/tripwire/tw.pol

Generating the database...

*** Processing Unix File System ***

.....

Wrote database file: /var/lib/tripwire/shuttle2.twd

The database was successfully generated.
```

请注意，这里没有显示所有输出。在 Tripwire 创建其数据库（这是你文件系统的快照）之后，它使用此基线以及 `/etc/tripwire` 目录下的加密配置和策略设置来监控系统的状态。然后你应该在完整性检查模式下启动 Tripwire，并使用所需的选项。（有关详细信息，请参阅 `tripwire` 手册页。）例如，你可以让 Tripwire 检查你的系统，然后在命令行上生成报告，如下所示：

```
# tripwire -m c
```

这里没有显示输出，但在此示例中显示了报告。输出可以重定向到文件，但报告会保存为 `/var/lib/tripwire/report/hostname-YYYYMMDD-HHMMSS.twr`（换句话说，使用你的主机名、年、月、日、时、分和秒）。使用 `twprint` 实用程序读取此报告，如下所示：

```
# twprint --print-report -r \
/var/lib/tripwire/report/shuttle2-20020919-181049.twr | less
```

Tripwire 支持其他选项，如通过电子邮件发送报告，这些任务应由系统的调度表 `/etc/crontab` 在非工作时间作为计划任务运行。（在性能较弱的计算机上，这可能非常消耗资源。）Tripwire 软件包还包括一个 `twadmin` 实用程序，你可以使用它来微调或更改设置或策略，或执行其他管理任务。

## 设备

切勿宣传你已将 NIC 设置为混杂模式。混杂模式（可以通过使用 `ifconfig` 的 `promisc` 选项在接口上设置）适用于监控跨网络的流量，并且通常允许你监控可能已入侵你网络的人的行动。`tcpdump` 命令在程序运行期间也会将指定接口设置为混杂模式；不幸的是，当 `tcpdump` 运行时，`ifconfig` 命令不会报告这一事实！请记住，这是黑客监控你的网络以获取极其重要的 root 密码的一种方式。

> **注意**
> 
> 浏览 `http://www.redhat.com/docs/manuals/` 阅读关于如何检测未经授权的入侵或数据包浏览（称为 *网络嗅探*）的信息。你可以使用这些信息来帮助保护你的系统。向下滚动页面并点击安全指南链接。

不要忘记在合适的工作中使用合适的工具。虽然网络桥接器可用于将你的网络连接到互联网，但这样做并不是一个好的选择。桥接器几乎已经过时，因为它们会转发任何到达它们的数据包，当桥接器连接到互联网时，这并不是好事。路由器允许你过滤哪些数据包被中继。

## 病毒

即使在使用得当的情况下，Linux 与 Windows 一样容易受到病毒的侵害。这可能会让你感到惊讶，特别是如果你是基于 Linux 的安全记录才切换到 Linux 的话。然而，Windows 和 Linux 之间的区别在于，在 Linux 上防范病毒要容易得多。事实上，只要你足够聪明，你就不必为此担心。原因如下：

- Linux 从不将当前目录放入你的可执行文件路径中，因此输入 `ls` 会运行 `/bin/ls`，而不是当前目录中的任何 `ls`。
- 非 root 用户只能感染他具有写权限的文件，这通常仅限于其主目录中的文件。这是永远不要使用 root 账户超过必要时间的最重要原因之一！
- Linux 强制你将文件标记为可执行文件，因此你不会意外运行名为 `myfile.txt.exe` 的文件，误以为它只是一个文本文件。
- 通过拥有多个常见的 web 浏览器和电子邮件客户端，Linux 通过多样性获得优势：病毒编写者无法瞄准一个平台并击中 90% 的用户。

尽管说了这么多，Linux 仍然有成为病毒载体的风险。如果你运行邮件服务器，你的 Linux 机器可以将受病毒感染的电子邮件发送给 Windows 机器。基于 Linux 的服务器本身可能没问题，但 Windows 客户端会被病毒击倒。

在这种情况下，你应该考虑为你的机器配备病毒扫描器。你可以从免费和商业软件中进行多种选择。最流行的免费套件是 Clam AV（`http://www.clamav.net/`），但 Central Command、BitDefender、F-Secure、Kaspersky、McAfee 等都在争相提供商业解决方案——在承诺之前请四处寻找最划算的方案。

## 配置防火墙

始终在连接到互联网的计算上使用基于硬件或基于软件的防火墙。Fedora 包含一个名为 `system-config-securitylevel` 的图形化防火墙配置客户端，以及一个名为 `lokkit` 的控制台防火墙客户端。使用这些工具实施关于访问你的计算机或 LAN 的选择性或限制性策略。

从控制台或终端窗口启动 `lokkit` 命令。你必须以 root 身份运行此命令；否则，你会看到类似这样的错误消息：

```
$ su /usr/sbin/lokkit
ERROR · You must be root to run lokkit.
```

使用 `su` 命令像这样运行 `lokkit`：

```
$ su -c "/usr/sbin/lokkit"
```

按下回车键后，你会看到图 30.1 中所示的对话框。按 Tab 键导航以启用或禁用防火墙。你还可以自定义防火墙设置，允许特定协议通过端口访问，如果安装了多个 NIC，还可以指定用于防火墙的以太网接口。请注意，你还可以在 X 会话期间运行 `gnome-lokkit` 客户端来使用 `lokkit` 的图形界面版本。

![](img/34e72348d53ca54c2a1d9c871316691b_692_0.png)

使用 `system-config-securitylevel` 是实现简单数据包过滤规则集的快速而简单的方法，该规则集使用过滤规则来接受或拒绝流经你的主机以太网或指定设备（如 `eth0` 或 `ppp0`）的 TCP 和 UDP 数据包。这些规则是即时创建并立即在内存中通过 `iptables` 实施的。

从管理菜单的“防火墙”菜单项启动 `system-config-securitylevel`。系统会提示你输入 root 密码，然后客户端窗口出现。图 30.2 显示已为 `eth0` 以太网设备启用防火墙，允许传入的 secure shell 和 HTTP 请求。

