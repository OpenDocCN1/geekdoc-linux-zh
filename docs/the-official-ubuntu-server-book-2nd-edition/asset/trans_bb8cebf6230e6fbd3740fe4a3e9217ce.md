

![](img/304f637afcecc491b152ee8ac5afadee_67_0.png)

## Figure 1-3 File system settings for manual partitioning

同样来自 Ubuntu 安装程序，以及如何在已运行的服务器上使用命令行工具创建 RAID 卷。

手动安装程序甚至对于常规的 ext4 分区也不会隐藏太多设置。以下是每个选项的基本介绍以及你可能想要更改它们的原因：

- Mount point
如果你超出了标准的根分区和交换分区，就需要更改此选项，以指向系统启动时希望挂载此分区的位置。

- Mount options
你可以向文件系统传递许多高级选项以供挂载。当你选择此选项时，安装程序会向你显示可供选择的选项列表，并附带每个选项的简要说明。我的建议是，除非有充分理由将其禁用，否则请坚持使用默认的 relatime 选项。

在 Linux 下的网站，甚至 Ubuntu 已经将所有必要的软件包组合在一起。如果你选择 LAMP 服务器软件包组，Ubuntu 将添加 apache2、apache2-mpm-prefork、mysql-server-5.0、mysql-client-5.0 和 php5-mysql 软件包以及它们所有的库和其他依赖项。除了额外的软件包之外，当你选择此组时，安装程序会提示你为 MySQL root 用户选择一个可选密码（这是个好主意，因为默认密码为空）。

## Mail server

此选项安装 Postfix 邮件服务器软件包。当你启用此选项时，安装程序会启动初始 Postfix 配置脚本。这是一个交互式脚本，它为你提供几种常见的邮件服务器配置类型，并且根据你的选择，它会问你一些额外的问题，这样当你完成时，至少应该有一个可用的邮件服务器。需要记住的是，虽然邮件服务器可以运行，但如果你想添加垃圾邮件检查、灰名单、POP 或 IMAP 服务器或其他更高级的选项，就必须执行额外的配置。有关邮件服务器配置类型的列表，请参阅第 5 章《Guide to Common Ubuntu Servers》。

## OpenSSH server

此选项安装 openssh-server 软件包。如果你想使用 SSH 远程管理服务器，请选择此项。请注意，即使你不选择此选项，你仍然可以从主机 ssh；你只是无法 ssh 进入主机。

## PostgreSQL database

如果你想要一个 PostgreSQL 数据库服务器，请选择此选项。它将安装 postgresql 软件包以及其文档和任何必要的库和依赖项。

## Print server

此选项选择 cupsys、cupsys-bsd（为 cups 提供 lpr 服务）、defoma、foomatic-db、foomatic-filters 以及许多其他打印机驱动程序和库——所有你需要将服务器连接到一个或多个打印机（本地或通过网络）然后与你的局域网共享所需的东西。

- Samba file server
此选项添加 samba、samba-doc、smbfs 和 winbind 软件包以及依赖项和库。如果你想设置一个文件服务器来与 Windows、Linux 和 Mac 主机共享文件，但不想使用 NFS，请选择此选项。

- Tomcat Java server
如果你计划安装 Tomcat Java 服务器，此选项将安装你所需的所有 Java 软件包。

- Virtual machine host
如果你计划将此机器用作其他虚拟机的主机，此选项将安装你所需的全部 KVM 软件包。有关虚拟机的更多信息，请参阅第 9 章。

如果你选择其中任何一个选项，在某些情况下服务器就可以使用，但在许多情况下你仍需在自己的方面进行一些配置，以便服务器最终对你有用。在第 5 章中，我讨论了一些你可能想要配置的常见 Ubuntu 服务器，并为每种类型提供一些示例配置。顺便说一下，如果你完成安装后意识到你想再次查看此软件包列表，只需从终端运行 sudo tasksel 即可。请注意，本地版本的 tasksel 会显示一个更大的组列表，其中包括许多可能更适合桌面安装的选项。你也可以运行 sudo tasksel -s，以便只获取服务器任务列表。

## Installer Console

在大多数情况下，你将与默认的安装程序屏幕交互。在此屏幕中你基本上只能回答问题和选择一些选项。有时，安装并不会完全按照你的计划进行，特别是如果你使用的是特殊硬件或正在尝试新的 Kickstart 脚本。Ubuntu 安装程序通过可访问的其他控制台提供了多种诊断途径。例如，如果你按 Alt-F4，你将看到 Ubuntu 安装程序正在进行的操作的运行日志。或者，如果你似乎在网络上无法获得 DHCP 租约，你可以按 Alt-F4 切换到此控制台，查看主机上出现的错误。

