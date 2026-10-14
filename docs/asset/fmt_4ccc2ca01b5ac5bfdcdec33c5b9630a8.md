
# 保护您的机器

```
sudo /etc/tripwire/twinstal.sh
```

Tripwire 站点和本地密码用于签名各种文件，如配置、策略和数据库文件。要初始化 Tripwire，使用其 `--init` 选项如下：

```
sudo tripwire --init
```

输出：

```
解析文件： /etc/tripwire.tw.pol
生成数据库...
*** 正在处理 Unix 文件系统 ***

...
写入数据库文件 /var/lib/tripwire/shuttle2.twd
数据库生成成功。
```

注意，并非所有输出都显示在此处。在 Tripwire 创建数据库（它是您文件系统的快照）后，它将使用此基线以及 `/etc/tripwire` 目录下的加密配置和策略设置来监控系统的状态。随后，您应该根据所需的选项以完整性检查模式启动 Tripwire。（详情请参阅 `tripwire` 手页。）例如，您可以在命令行让 Tripwire 检查您的系统并生成报告，如下：

```
# tripwire -m c
```

此处未显示输出，但示例中显示了报告。输出将重定向到文件中，但报告将保存为 `/var/lib/tripwire/report/hostname-YYYYMMDD-HHMMSS.tw`（换句话说，使用您的主机名、年、月、日、小时、分钟和秒）。可以使用 `twprint` 工具读取此报告，如下：

```
twprint --print-report -r \
/var/lib/tripwire/report/shuttle2-20020919-181049.tw | less
```

Tripwire 还支持其他选项，例如制作报告，这些应通过您系统的调度表 `/etc/crontab` 在非工作时间作为计划任务运行。Tripwire 软件包还包含一个 `twmin` 工具，您可以使用它来微调或更改设置、策略，或执行其他管理工作。

# 设备

永远不要宣称您已将网卡（NIC）设置为**混杂模式**。混杂模式（可以通过 `ifconfig promiscu` 在接口上设置）有助于监控跨网络流量，并且通常允许您监控可能已经入侵您网络的人的操作。`tcpdump` 命令在程序运行时也会将指定的接口设置为混杂模式；遗憾的是，当 `tcpdump` 运行时，`ifconfig` 命令不会报告这一事实！

不要忘记为正确的工作使用正确的工具。虽然可以使用网桥器将您的网络连接到互联网，但这不是一个好的选择。网桥器几乎已经过时，因为它们会转发任何经过的连接到互联网的数据包。而路由器允许您过滤被中继的数据包。

# 病毒

在得当的人手中，Linux 对病毒变得像 Windows 一样脆弱。这可能让你感到意外，特别是如果你是基于其安全记录切换到 Linux 的话。然而，Windows 和 Linux 的区别在于，在 Linux 上更容易防范病毒。事实上，只要你足够机灵，就永远不需要担心它们。原因如下：

- Linux 永远不会将当前目录放入可执行路径中，因此输入 `ls /bin/ls` 运行的是该程序而非当前目录下的任何 `ls`。
- 非 root 用户只会感染他有权访问，这通常只有他家目录下的文件。这就是为什么在不需要时绝不使用 `sudo` 的重要原因之一！
- Linux 强制你将文件标记为可执行，因此你不会误运行一个名为 `myfile.txt.exe` 的文件而认为它只是一个文本文件。
- 通过拥有多个常用的浏览器和电子邮件客户端，Linux 具有由于多样性带来的优势：病毒编写者无法针对一个平台并击中 90% 的用户。

尽管如此，Linux 仍然极易成为病毒的载体。如果您运行邮件服务器，您的 Linux 可能会向 Windows 机器发送病毒感染的邮件。基于 Linux 的服务器可能是安全的，但 Windows 客户端会被病毒击。

在这种情况下，您应该为您的机器考虑一个病毒扫描器。您有多个选择，包括免费和商业性的。最流行的免费套件是 Clam AV (http://www.clamav.net)，由 Central Command、BitDefender、F-Secure、Kaspersky 和 McAfee 开发，它们都在竞争提供商业解决方案——在决定之前多寻找最佳优惠。

# 配置您的防火墙

在连接到互联网的计算机上始终使用基于硬件或软件的防火墙。Ubuntu 包含一个名为 `gnome-lokkit` 的图形防火墙配置客户端，以及一个名为 `lokkit` 的控制台防火墙客户端。使用这些工具来实现选择性或限制性的策略，授权访问计算机或局域网。

从控制台或终端窗口启动 `lokkit` 命令。您必须以 root 身份运行此命令；否则您将看到如下错误消息：

```
$ /usr/sbin/lokkit

ERROR - You must be root to run lokkit.
```

使用 `sudo` 命令如下运行 `lokkit`：

```
$ sudo "/usr/sbin/lokkit"
```
