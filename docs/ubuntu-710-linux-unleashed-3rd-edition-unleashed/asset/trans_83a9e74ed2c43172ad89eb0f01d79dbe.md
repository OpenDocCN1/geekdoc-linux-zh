

```
Parsing policy file: /etc/tripwire/tw.pol
Generating the database...
*** Processing Unix File System ***
...
Wrote database file: /var/lib/tripwire/shuttle2.twd
The database was successfully generated.
```

请注意，这里并未显示全部输出。Tripwire 在创建其数据库（即文件系统的快照）后，会使用该基线以及 /etc/tripwire 目录下的加密配置和策略设置来监控系统的状态。然后你应以完整性检查模式启动 Tripwire，并使用所需的选项。有关详细信息，请参阅 tripwire 手册页。例如，你可以在命令行让 Tripwire 检查系统并生成报告，如下所示：

```
# tripwire -m c
```

在此示例中未显示输出，但会显示报告。输出可以重定向到文件，但报告会保存为 /var/lib/tripwire/report/hostname-YYYYMMDD-HHMMSS.twr（换句话说，使用主机名、年份、月份、日期、小时、分钟和秒）。该报告可使用 twprint 实用程序读取，如下所示：

```
# twprint --print-report -r \
/var/lib/tripwire/report/shuttle2-20020919-181049.twr | less
```

Tripwire 还支持其他选项，例如通过电子邮件发送报告，应由系统调度表 /etc/crontab 在非高峰时段作为计划任务运行 Tripwire。（在性能较弱的计算机上它可能占用大量资源。）Tripwire 软件包还包含 twadmin 实用程序，可用于微调或更改设置或策略，或执行其他管理任务。

## 设备

切勿宣称你已将网卡设置为混杂模式。混杂模式（可通过使用 ifconfig 的 promisc 选项在接口上设置）对于监控网络流量很有用，并且通常可以让你监控可能已入侵你网络的人的行为。tcpdump 命令在程序运行期间也会将指定接口设置为混杂模式；不幸的是，在 tcpdump 运行期间，ifconfig 命令不会报告这一事实！

## 病毒

在正确的使用下，Linux 与 Windows 一样容易受到病毒攻击。这可能会让你感到惊讶，特别是如果你正是基于其安全记录而转向 Linux 的话。然而，Windows 和 Linux 之间的区别在于，在 Linux 上防范病毒要容易得多。事实上，只要你足够聪明，就永远不必担心它们。原因如下：

- Linux 从不在你的可执行路径中放置当前目录，因此输入 `ls` 会运行 `/bin/ls`，而不是当前目录中的任何 `ls`。
- 非 root 用户只能感染他有写权限的文件，通常只有他主目录中的文件。这是永远不要在不需要时使用 `sudo` 的最重要原因之一！
- Linux 强制你将文件标记为可执行，因此你不会意外运行名为 `myfile.txt.exe` 的文件，以为它只是文本文件。
- 由于 Linux 有多种常见的网页浏览器和电子邮件客户端，因此具有多样性优势：病毒编写者无法针对一个平台就击中 90% 的用户。

尽管说了这么多，Linux 仍可能成为病毒的携带者。如果你运行邮件服务器，你的 Linux 机器可能会向 Windows 机器发送感染病毒的邮件。基于 Linux 的服务器本身会没事，但 Windows 客户端会被病毒击垮。

在这种情况下，你应考虑为你的机器安装病毒扫描程序。你有多个选择，既有免费的也有商业的。最受欢迎的免费套件是 Clam AV（http://www.clamav.net），但 Central Command、BitDefender、F-Secure、Kaspersky、McAfee 等公司也在竞争提供商业解决方案——在承诺之前请四处寻找最优惠的交易。

## 配置你的防火墙

始终在连接到互联网的计算机上使用基于硬件或基于软件的防火墙。Ubuntu 有一个名为 `gnome-lokkit` 的图形防火墙配置客户端，以及一个名为 `lokkit` 的基于控制台的防火墙客户端。使用这些工具来实现对你的计算机或 LAN 访问的选择性或限制性策略。注意：与往常一样，请确保启用 Universe 和 Multiverse 以获得计算机可用的全部软件范围。

从控制台或终端窗口启动 `lokkit` 命令。你必须以 root 身份运行此命令；否则，你会看到类似这样的错误信息：

```
```text
$ /usr/sbin/lokkit
ERROR - You must be root to run lokkit.
```
```

使用 sudo 命令以如下方式运行 lokkit：

```
```text
$ sudo "/usr/sbin/lokkit"
```
```

