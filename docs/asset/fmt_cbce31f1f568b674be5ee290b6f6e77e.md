
# `/etc/tripwire/twinst.sh`

Tripwire 站点和本地口令用于签名各种文件，例如配置、策略和数据库文件。

口令长度应至少为 8 个字符，并包含字母和数字。

更多信息请参阅 Tripwire 手册。

正在创建密钥文件

（在选择口令时，请记住良好的口令通常包含大小写字母、数字和符号标记，且至少有 8 个字符。）

输入站点口令：

然后你需要输入密码。按照提示操作后，默认配置和策略文件（`tw.cfg` 和 `tw.pol`）将被加密。要初始化 Tripwire，使用其 `--init` 选项：

```bash
# tripwire --init
Please enter your local passphrase:
Parsing policy file: /etc/tripwire/tw.pol
Generating the database...
*** Processing System ***
Wrote database file: /var/lib/tripwire/shuttle2.twd
```

数据库已成功生成。

注意并非所有输出都会显示。在 Tripwire 创建数据库（系统的快照）后，使用此基准以及 `/etc/tripwire` 下的加密配置和策略设置来监控系统的状态。然后你应该使用所需的选项以完整性检查模式启动 Tripwire。（详情见 Tripwire 手册。）例如，你可以让 Tripwire 在命令行检查你的系统并生成报告，如下：

```bash
# tripwire -m c
```

此处未显示输出，但会显示报告。

Tripwire 还支持其他选项，例如通过电子邮件发送报告，这应该通过你的调度表 `/etc/crontab` 在非工作时段运行（它在性能较弱的计算机上可能会消耗资源）。Tripwire 软件包还包含一个 `twadmin` 工具，你可以用它微调或更改设置或策略，或执行其他管理任务。

## 设备

不要宣扬你已将网卡设置为混杂模式。混杂模式（可以使用 `ifconfig` 的 `prom` 选项在接口上设置）有利于监控跨网络流量，并允许你监控可能破入你网络的人的行为。`tcpdump` 命令在程序运行时也会设置一个指定的接口进行监控；不幸的是，当 `tcpdump` 运行时，`ifconfig` 命令不会报告这一事实！请记住，这是破解者用来监控你的网络以获取至关重要的 root 密码的方法之一。

# 第 35 章 保护您的机器

> 注意
>
> 访问 http://www.redhat.com/docs/manuals/ 了解如何检测未经授权的网络入侵或数据包嗅探（称为网络嗅探）。你可以利用这些信息来帮助保护系统。向下滚动页面并点击“安全指南”（Security guide）链接。

不要忘记为任务选择正确的工具。虽然可以使用网桥将您的网络连接到互联网，但这不是一个良好的选择。网桥几乎已经过时，因为它们会转发经过的所有数据包，当网桥连接到互联网时这并不是好事。路由器允许您过滤哪些数据包被中继。

## 病毒

在高手手中，Linux 和 Windows 一样容易受到病毒攻击。这可能会让你感到惊讶，特别是如果你是因为安全记录而切换到 Linux 的。然而，Windows 和 Linux 的区别在于，在 Linux 上更容易防御病毒。事实上，只要你足够聪明，就永远不必担心它们。原因如下：

- Linux 永远不会将当前目录放入可执行路径中，因此输入 `ls /bin` 会运行 `/bin/ls`，而不是当前目录下的 `ls`。
- 非 root 用户只能感染其具有写入权限的文件，这通常仅限于其家目录下的文件。这就是绝不长时间使用 root 账户的最重要原因之一！
- Linux 强制你将文件标记为可执行，这样你就不会无小心运行一个名为 `myfile.txt.exe` 的文件并以为它是一个文本文件。
- 通过拥有多个网络浏览器和电子邮件客户端，Linux 具有多样性带来的优势：病毒编写者无法针对某一个平台影响 90% 的用户。

尽管如此，Linux 仍然可能成为病毒的载体。如果你运行邮件服务器，你的 Linux 可能会向 Windows 机器发送感染病毒的邮件。基于 Linux 的服务器可能是安全的，但 Windows 客户端会被病毒破坏。

在这种情况下，你应该考虑为你的机器准备一个病毒扫描器。你有多种选择，包括免费和商业软件。最流行的免费套件是 Clam AV (http://www.clamav.net/)，但 Central Command、BitDefender、F-Secure、Kaspersky、McA 等都在提供商业解决方案——在决定之前寻找最优惠。

## 配置防火墙

在连接到互联网的计算机上，始终使用基于硬件或软件的防火墙。Fedora 包含一个名为 `system-config-securitylevel` 的图形防火墙配置客户端，以及一个名为 `lokkit` 的控制台防火墙客户端。使用这些工具针对您的计算机或局域网实施选择性或限制性策略。

从控制台或终端窗口启动 `lokkit` 命令。你必须以 root 身份运行此命令；否则你会看到这样的错误消息：

```
$ /usr/sbin/lokkit
ERROR - You must be root to run lokkit.
```

使用以下命令运行 `lokkit`：

```
$ su -c "/usr/sbin/lokkit"
```

按下回车后，你将看到如图 35.1 所示的对话框。按 Tab 键导航或禁用防火墙。你可以自定义防火墙设置，允许特定协议通过端口通过，并在安装了多个网卡的情况下指定以太网接口作为防火墙。你还可以在 X 会话期间运行 `gnome-lokkit` 客户端使用 `lokkit` 的图形界面版本。

![](img/d4ad9a7c85702c925b4288f587284a4f_917_0.png)

**图 35.1** Fedora `lokkit` 命令在 Linux 内存中快速生成防火墙规则。

使用 `system-config-securitylevel` 是一种快速且简单的实现数据包过滤规则的方法，通过过滤来启用或拒绝通过主机以太网或指定设备（如 `eth0` 或 `pp0`）流过的 TCP 和 UDP 数据包。规则是动态创建并使用 `iptables` 立即在内存中实现的。

从设置（Settings）菜单中的安全级别（Security level）项目启动 `system-config-securitylevel`。系统会提示输入 root 密码，客户端窗口将会出现。图 35.2 显示为 `eth0` 设备启用了防火墙，允许入站的安全 shell 和 HTTP 请求。

![](img/d4ad9a7c85702c925b4288f587284a4f_918_0.png)

**图 35.2** Fedora 的 `system-config-securitylevel` 客户端也可用于为 Linux 快速生成并实施简单的自定义防火墙规则。

## FEDORA 与防火墙

Fedora 还支持较旧但功能仍然强大的 `iptables` 数据包过滤软件，它可以用于在 Linux 关关、服务器和工作站上构建有效的防火墙规则。Linux 还支持功能更 `iptables` 或 NetFilter 系统，它添加了额外的控制和日志功能，用于构建过滤规则集或过滤指令。

遗憾的是，Fedora 不包含任何供你构建、共享和测试复杂规则集的命令行或图形界面实用（这些规则通常以 shell 脚本实现）。如果你想控制出站以及入站数据包，就需要手动操作。不过，你可以使用 `vi` 等文本编辑器编写自己的规则。许多经验丰富的 Linux 用户会在高级网络情况下（例如路由规则的开发）为特定应用程序手动调优规则。

要了解关于使用 `iptables` 各种网关和防火墙系统的良好概览及所有细节，请阅读 Robert L. Ziegler 写的《Linux Firewalls》。你也可以访问 http://www.linux-firewall.com/linux/index.html。

## 制定恢复计划

没有人喜欢为最坏的情况做计划。如果你被黑了，一切都会压力倍增。然而，如果你花时间提前准备，你至少可以避免这种情况。这里是一些入门技巧：

- 不要直接拔掉网线——这会提醒黑客他已被检测到。
- 只通知那些需要知道的人——你的老板和其他其他 IT 人员处于名单之首。
- 如果需要该机器且你不想追踪攻击，请安全地从网络中移除它。
- 复制系统上所有的日志文件并存储在其他处。
- 如果你之前与外部安全公司合作过，请他们他们进行一次新的审计——他们能够从日志中提取出所有可能的信息。
- 开始收集前几个月的备份磁带——你的系统可能在你发现很久以前就被黑了，所以你可能需要回滚系统多次。
- 从 http://www.rootkit.nl/projects/rootkit_hunter.html 下载并安装 Rootkit Hunter。

## 第 35 章 保护您的机器

### 跟进 Linux 安全问题

有许多与安全相关的网站。其中一个特定的网站是 Security Focus，其邮件列表被称为 BugTraq。BugTraq 以对安全漏洞进行无偏见的讨论而闻名。请注意：它的流量相对很大（每天超过 200 多条消息）。
