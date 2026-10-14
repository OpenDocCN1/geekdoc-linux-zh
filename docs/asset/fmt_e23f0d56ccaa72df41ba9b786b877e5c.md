
进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

```
matthew@seour~$ sudo tripwire -init
请输入本地口令：
解析策略文件: /etc/tripwire/tw.pol
生成数据库...
*** 处理 Unix 文件 ***
写入数据库文件: /var/lib/tripwire/shuttle2.twd
数据库生成成功。
```

注意，并非显示所有输出。在 Tripwire 创建数据库（文件系统的快照）后，使用此基线以及`/etc/tripwire`目录下的加密配置和策略设置来监控系统状态。然后你应该以完整性检查模式启动 Tripwire，并带有所需的选项。（详情请参 Tripwire 手页。）例如，你可以通过命令行让 Tripwire 检查你的系统并生成报告，如下：

```
matthew@seour~$ sudo tripwire -c m
```

# 病毒 435

此处未显示输出，但示例中显示了一个报告。输出可以重定向到文件，但报告会保存为`/var/lib/tripwire/report/hostname-YYYYMMDD-HHMMSS.t`（换句话说，使用您主机的名称、年、月、日、小时、分和秒）。可以使用`tripwire`工具读取此报告，例如：

```bash
matthew@seymour~\$ sudo tripwire --print-report -r /var/lib/tripwire/report/shuttle2-20020919-181049.t | less
```

Tripwire 还支持其他选项，例如通过电子邮件发送报告，这应该由您系统的调度表`/etc/crontab`在非空闲段作为计划任务运行（在性能较差的计算机上，它可能会消耗大量资源）。Tripwire 软件包还包含`twadmin`工具，您可以使用它来精调或更改设置和策略，或执行其他管理工作。

如果您想使用 Tripwire，请花些时间阅读文档。它很强大，但并不简单。我们建议从主页开始并使用`tripwire.com`。

# 设备

不要宣称您已将网卡（NIC）设为混杂模式。混杂模式（可以使用`ifconfig prom`选项在接口上设置）有助于监控跨网络的流量，并能让您能够监控可能侵入您网络的人的操作。`tcpdump`命令在程序运行时也会将指定的接口设置为混杂模式；遗憾的是，当`tcpdump`运行时，`ifconfig`命令并不会报告这一事实！

记住为特定的工作使用正确的工具。虽然您可以使用网络桥接器将网络连接到互联网，但这并不是好的选择。桥接器几乎已经过时，因为它们会转发经过它们的任何数据包，当桥接器连接到互联网时这不利。路由器允许您过滤被中继的数据包。

# 病毒

在正确的人手中，Linux 像 Windows 一样容易受到病毒攻击。这可能会让你感到意外，特别是如果你是因为它的安全记录而切换到 Linux 的。然而，Windows 和 Linux 的区别在于，在 Linux 上防御病毒容易得多。事实上，只要你聪明且勤奋，就永远不必担心它们。原因如下：

- Linux 永远不会将当前目录放在可执行路径中，因此输入`/bin/ls`而不是任何与当前目录下同名的程序来执行它。
- 非 root 用户只能感染该用户有权访问的文件，通常只有用户家目录下的文件。这是在不需要时绝不使用`sudo`的最重要的原因之一。

# 436 第 19 章 保护您的机器

- Linux 强制您手动标记文件为可执行，因此您不会不小心运行一个名为`myfile.txt.exe`的文件而误以为它只是一个文本文件。
- 通过拥有多个常用的网络浏览器和电子邮件客户端，Linux 在多样性方面具有优势：病毒无法针对某一个平台并击中 90% 的用户。

尽管如此，Linux 也很容易成为病毒的载体。如果您运行邮件服务器，您的 Linux 机器可以向 Windows 机器发送受病毒感染的邮件。基于 Linux 的服务器可能是安全的，但 Windows 客户端会被病毒击倒。

在这种情况下，请为您的机器考虑一个病毒扫描器。您有几个选择，既有免费的，也有商业的。最流行的免费套件是 Clam AV (`www.clam.net`)，但 Central Command、BitDefender、F-Secure、Kaspersky、McAfee 等都在竞争商业解决方案。在决定之前，请寻找最佳优惠。

# 配置您的防火墙

在连接到互联网的计算机上，请始终使用基于硬件或软件的防火墙。Ubuntu 默认安装了一个名为 Uncomplicated Firewall (`UFW`) 的防火墙应用程序。该工具允许您针对访问您的计算机或局域网实施选择性或限制性策略。

`UFW`从终端运行，您必须具有管理员权限才能使用它。命令格式如下：

```bash
mathew@semour:- sudo ufw status
```

最常用的命令列在表 19.1 中。其他命令请参考 UFW 的 man页。许多命令在表格之后有更详细的描述。

默认情况下，`UFW`或防火墙是禁用的。要启用防火墙，请运行：

| 表 19.1 UFW 有用命令 | 执行的操作 |
| :--- | :--- |
| enable | 启用防火墙 |
| disable | 禁用防火墙 |
| reload | 重新加载防火墙 |
| default | 设置默认策略 |
| allow | 允许流量 |
| deny | 拒绝流量 |
| reject | 拒绝流量 |
| limit | 限制流量 |
| on | 切换日志记录 |
| off | 切换日志记录 |
| status | 显示防火墙状态 |
| numbered | 显示编号的防火墙状态 |
| verbose | 显示详细的防火墙状态 |
| version | 显示版本 |

## 配置您的防火墙 # 437

| 命令 | 执行的操作 |
| :--- | :--- |
| on | 切换日志记录 |
| allow | 允许流量 |
| deny | 拒绝流量 |
| reject | 拒绝流量 |
| limit | 限制流量 |
| delete | 删除规则 |
| status | 显示防火墙状态 |
| numbered | 显示编号的防火墙状态 |
| verbose | 显示详细的防火墙状态 |
| version | 显示版本 |

接下来，您想启用日志记录。与`enable`命令类似，您运行：

```bash
matthew@seour:- sudo ufw on
```

若要在防火墙上启用特定端口，可以运行`ufw`命令并跟上要打开的端口号。例如，如果您想允许 80 (`HTTP`) 连接到您的服务器，只需输入：

```bash
matthew@seour:- sudo ufw allow 80
```

要删除允许 80 端口的防火墙规则，运行：

```bash
matthew@seour:- sudo ufw delete 80
```

许多服务已经定义在`ufw`中了。这意味着您不需要记住它们使用的标准端口，例如：

```bash
matthew@seour:- sudo ufw allow ssh
```

您还可以允许来自特定 IP 地址的入站连接。例如，如果您想使用`192.168.0.1`连接到您的机器，只需输入：

```bash
matthew@seour:- sudo ufw allow from 192.168.0.1
```

要删除允许上述 IP 地址的防火墙规则，运行：

```bash
matthew@seour:- sudo ufw delete allow from 192.168.0.1
```
