
named 目录。如果文件存在，named 会查看文件时间，计算刷新间隔，然后决定是否重新加载文件。删除适当的数据库文件将保证下载到文件的全新副本。

如果你选择使用此方法来重启你的 DNS 从服务器，你可能想要将 db.cache 和 db.0.0.127.in-addr.arpa 文件重命名为唯一名称。例如，你可以将缓存文件更改为 named.cache，将 0.0.127.in-addr.arpa 文件更改为 named.loopback。要使此更改生效，你只需修改你的 named.boot 或 named.conf 文件。现在，你要重启 DNS 从服务器所需要做的就是杀掉 named 进程，删除数据库文件，然后重启 named，如图 6.6 所示。

## WINDOWS 2000 SERVER DNS

Windows 2000 Server 附带内置的 DNS 服务器。如果你没有在初始安装期间安装 DNS 服务器，可以通过控制面板中的添加/删除程序小程序添加。Microsoft DNS 服务器的功能与任何 UNIX DNS 服务器非常相似，虽然它是独立实现的，但与 BIND 版本 8 非常相似。有一种显著的例外：默认情况下，Windows 2000 DNS 服务器从注册表或 Active Directory 启动。但是，Windows 2000 DNS 服务器可以配置为像 UNIX DNS 服务器一样从文件启动。DNS 数据文件存储在 %SystemRoot%\System32\DNS 中。所有区域和反向查找文件格式与 UNIX DNS 服务器中使用的格式完全相同。启动文件（%SystemRoot%\System32\DNS\boot）格式也与 UNIX 下的 named.boot 相同。因此，对于熟悉 UNIX 上 DNS 的人来说，先简单地操作文件然后再学习 GUI。你会发现这种方式比双脚跳入要容易得多。最终，你会发现 GUI 可以帮助简化许多任务并防止你犯常见错误。

## Creating a DNS Zone in Windows 2000

如果你尚未在 Windows 2000 服务器上安装 DNS 服务器服务，请现在使用控制面板中的添加/删除程序小程序进行安装。你需要此服务来托管主 DNS 区域，我们将在此处创建。假设你已拥有网络所需的所有相关信息，例如域名、IP 范围等。如果你没有这些信息，现在是获取它们的最佳时机。假设你已准备就绪，让我们创建新的区域：

### Figure 6.7 DNS MMC snap-in.

Configure the DNS Server

域名系统（DNS）是一种用于在网络上定位计算机和其他资源的分层命名系统。DNS 主要以提供将友好 DNS 域名映射到网络资源和 IP 地址的服务而闻名。这允许配置为查询 DNS 的计算机通过主机名而不是 IP 地址指定远程系统。

此 DNS 服务器尚未配置。配置包括更新根提示，以及创建正向和反向查找区域。

要配置 DNS 服务器，请在操作菜单上单击配置服务器。

有关配置 DNS 服务器的更多信息，请参阅联机帮助中的“Checklist: Installing a DNS server”。

- 1. 从开始菜单打开的管理工具文件夹中打开 DNS MMC 管理单元。你将看到与图 6.7 相似的屏幕。
- 2. 选择服务器（应该只有一个列出），然后从操作菜单中选择配置 DNS 服务器... 将出现如图 6.8 所示的配置 DNS 服务器向导。

### Figure 6.8
Configure DNS
Server
Wizard.

Configure DNS Server Wizard

欢迎使用配置 DNS 服务器向导

此向导帮助你设置 DNS（域名系统）服务器并配置服务器区域。

区域是链接 DNS 名称和相关数据（如 IP 地址或网络服务）的数据库。

要继续，请单击下一步。

![](img/415c89a1ede71e11e5040a0038b6916c_236_0.png)

![](img/415c89a1ede71e11e5040a0038b6916c_236_1.png)

