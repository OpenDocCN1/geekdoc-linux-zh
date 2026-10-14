

## Zabbix：监控

*Zabbix* 是一款网络监控应用，它监视一切——我们说的就是一切。我们不禁怀疑它是不是索伦之眼的化身。

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_117_0.png)

隐藏在他的堡垒中，系统管理员一览无余。他的目光穿透不同的发行版、不同的设备、磁盘和应用程序。你知道我在说什么，曾花费大量精力绘制出火焰中的巨眼。嗯，并不是那么无眼皮且缠绕着火焰，因为这不是小说，对吧！

*Zabbix* 是一款网络监控应用，可让你跟踪网络上发生的一切。无论网络规模大小，无论不同机器上安装的操作系统如何，*Zabbix* 都能密切关注这些机器的各个方面。使用 *Zabbix*，你可以监控可用磁盘空间、CPU 负载、网络流量统计、内存消耗、应用程序状态、文件的

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_117_1.png)

校验和，以及更多。所有收集的信息都存储在数据库中，你可以使用 *MySQL*、*Oracle* 或 *PostgreSQL*，因为 *Zabbix* 都支持它们。

### 超越竞争对手

但为什么你应该使用 *Zabbix*，当大多数人总是挂在嘴边的是 *Cacti* 和 *Nagios* 呢？

*Zabbix* 就像其更受欢迎的兄弟一样，支持简单网络管理协议（SNMP）。这意味着这些应用可以监控网络上几乎任何设备，例如路由器、打印机、交换机、调制解调器等。

虽然 *Nagios* 是监控本地和远程机器及 IT 基础设施的行业标准，但它几乎总是与其它监控工具一起使用。这是因为 *Nagios* 没有可视化功能，无法将记录的数据简化为易于理解的图表。话虽如此，*Nagios* 具有出色的告警功能，可让系统管理员随时了解其跟踪的所有设备。

相比之下，*Cacti* 没有告警机制，但它可以创建精美且详细的图表，表示其在网络设备上收集的所有数据。

我们选择的工具，在发送告警和创建图表方面非常方便。除了通过电子邮件、短信和 Jabber 发送告警外，它还允许你设置自动操作。也就是说，你可以配置 *Zabbix* 在发生某些定义事件时自行对远程机器采取行动。

在可视化方面，*Zabbix* 支持监控项的实时绘图，并提供图表、网络地图、屏幕，甚至幻灯片，使其适用于复杂的网络，其系统管理员更喜欢以图形方式查看数据。

### 了解 Zabbix

监控应用主要执行两个功能。它收集网络上所有设备的数据并将其报告给中央控制机构。*Zabbix* 依靠两个关键组件来执行这些功能——**zabbix-server** 和 **zabbix-agent**。

顾名思义，你需要在网络上希望监控的所有机器上安装 **zabbix-agent**。代理可以监控硬件资源以及应用程序，并将所有收集的信息推送到 **zabbix-server**。目前，**zabbix-agent** 可用于 Linux、FreeBSD、OpenBSD、NetBSD、HP-UX、MacOS X、Solaris 和各种 Windows 版本。

另一部分 **zabbix-server** 负责数据的轮询和捕获。在出现问题或停机时，服务器会向配置的账户发送通知。你只需在网络上安装一个 **zabbix-server** 实例即可。使用 *Zabbix*，你将获得一个集中的 Web 界面，可用于控制网络上监控哪些事件。由于其功能众多，以及它希望实现的目标，界面有时对许多用户来说似乎过于复杂和繁琐。尽管你有所保留和初步印象，我们还是建议你继续你的 Zabbix 之旅。

> 所有的绿色 OK 都证明了我在这里知道自己在做什么。

*你的网络*

### 当事情出错时

尽管该项目提供了出色的文档，如果你从未使用过 Zabbix 等网络监控应用，可能会出现许多问题。这就是为什么你不应在不先熟悉该应用的情况下将其安装到生产服务器上的原因。

配置不当的网络监控器如 Zabbix 可能会极大地消耗你的资源。如果不配置其删除旧数据，数据库可能会占用相当多的磁盘空间。也可能有其它原因让你想要避开 Zabbix。例如，你可能会发现 Zabbix 对于你的需求来说不是最优的，例如当它对你的目的来说过于庞大时。

文档本身并未提供卸载 Zabbix 的任何说明，那该怎么办？嗯，继续阅读，当然！

最明智的解决方案是禁用 Zabbix。但首先，前往 配置 > 主机 并禁用所有已配置的主机。接下来，从网络上的所有机器上卸载 zabbix-agent 并停止 zabbix-server。

红色意味着“你不能再往前”，但幸运的是 Zabbix 在鼠标悬停时提供了更多详细信息。

### 安装 Zabbix

该项目为少数发行版提供了二进制文件，例如 Debian 和 CentOS，而大多数发行版在其仓库中都提供 Zabbix。但与许多管理工具一样，仓库并不总是提供最新版本。

我们使用 CentOS 作为安装 zabbix-server 的基础。网络上还有其它运行其它 Linux 发行版的机器，例如 Linux Mint。

你应该已经在机器上安装了所有必需的 PHP 和 MySQL 包，但如果你在全新系统上安装 Zabbix，以下命令将安装依赖项：

```
su - "yum -y install mysql-server php5-mysql php5-gd"
```

在 CentOS 上安装 Zabbix 的最佳方式是通过 EPEL 仓库，因为官方仓库不提供最新版本。如果它尚未在你的机器上配置，你将必须先设置 EPEL 仓库：

```
su - "yum -y localinstall http://dl.fedoraproject.org/pub/epel/6/i386/epel-release-6-8.noarch.rpm"
su - "yum -y install zabbix20-server-mysql zabbix20-web-mysql"
```

上面的第一个命令将配置并启用仓库。在第二个命令中，我们指定要安装的包，在本例中为 Zabbix 2.0.x

Zabbix 支持 MySQL、PostgreSQL 和 Oracle 数据库，并可以将收集的数据存储在其中任何一个中。默认配置期望一个名为 zabbix 的数据库。此数据库的默认用户名为 zabbix，且未配置密码。你可以编辑 /etc/zabbix/zabbix_server.conf 文件以更改这些预定义设置。

如果你决定更改数据库设置，请确保将其记下，因为我们稍后在为 Zabbix 创建数据库时需要它们。你需要从终端运行以下命令：

```
mysql -u root -e "create database zabbix"
mysql -u root -e "create user 'zabbix'@'localhost' identified by 'ChangeMe'"
mysql -u root -e "grant all on zabbix.* to 'zabbix'@'localhost'"
mysql -u root -e "flush privileges"
```

上面的命令都很容易理解。我们在第一个命令中创建数据库，在第二个命令中创建用户。请确保指定你在 /etc/zabbix/zabbix_server.conf 文件中定义的确切用户名和密码。有关 MySQL 管理的更多详细信息，请参阅框。

现在数据库已就位，我们准备对其进行填充：

```
mysql -uzabbix -p'ChangeMe' zabbix < /usr/share/zabbix/mysql/schema.sql
mysql -uzabbix -p'ChangeMe' zabbix < /usr/share/zabbix/mysql/images.sql
mysql -uzabbix -p'ChangeMe' zabbix < /usr/share/zabbix/mysql/data.sql
```

### 快速提示

由于所有数据都记录在数据库中，内存越多，数据库访问速度越快。

你可以使用图表右上角的栏来指定时间段。

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_118_0.png)

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_118_1.png)

订阅 Linux Format http://myfavouritemagazines.co.uk/LINsubs

