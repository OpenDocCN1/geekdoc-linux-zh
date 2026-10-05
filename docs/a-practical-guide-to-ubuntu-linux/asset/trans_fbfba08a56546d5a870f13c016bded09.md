

# 654 第17章 配置与监控局域网 (LAN)

![](img/45ff4cd21497435daa35084a84b95d07_704_0.png)

图 17-9 使用屏幕右上边缘标签页的默认图表。

你可以使用屏幕右上边缘的标签页来控制图表。Settings（设置）标签页允许你设置图表显示的偏好；Tree View（树状视图）标签页显示图表的层级结构，允许你选择感兴趣的设备或图表；List View（列表视图）标签页显示所有可用图表的列表；List Preview（列表预览）标签页显示所有可用图表的小型预览。此外，List 和 Preview 标签页在屏幕顶部提供了一个过滤器，允许你显示图表的子集。

# CACTI CONSOLE 标签页

点击 Console（控制台）标签页会显示主控制台界面（图 17-8，上一页），你可以从这里管理 Cacti。主控制台界面左侧有一个菜单，并在 Console 标签页下方显示当前屏幕的路径。

屏幕右上角是用户名称（admin）和一个 Logout（注销）按钮。

# 设置远程数据源

你可以将任何运行 SNMP 的设备设置为 Cacti 可以监控和报告的数据源。本节将解释如何将本地网络上的远程系统设置为数据源，以及如何设置 Cacti 监控该数据源。设置本地数据源与设置远程数据源是的。

# 前提条件

在 Cacti 将监控的远程系统上安装以下包。如果你想监控本地系统，必须在本地系统上安装并配置此包；它不会随 cacti 包一起安装。

- * snmpd

snmpd.conf /etc/snmpd/snmpd.conf 控制 snmpd 守护进程。保存已安装的 snmpd.conf 文件以便以后参考。设置以下 snmpd.conf 文件，将 SNMP 团体设置为 public，并允许来自 localhost 和 10.10.4.98（运行 Cacti 的系统；请将此地址替换为本地 Cacti 服务器的地址）的查询：

```
$ cat /etc/snmpd/snmpd.conf
rocommunity public localhost
rocommunity public 10.10.4.98
```

/etc/default/snmpd 在 Ubuntu 和其他基于 Debian 的系统上，/etc/default/snmpd 文件控制 snmpd 守护进程的各个方面。例如，它指定了 snmpd 为查询列出哪些地址。Fedora 和 Red Hat 系统不使用此文件。如果你想让 snmpd 监听来自远程系统的查询，则必须编辑以下行，该行指定了 snmpd 运行的选项：

# $ cat /etc/default/snmpd

```
SNMPOPTS='-Lsd -Lf /dev/null -u snmp -g snmp -I -smux -p /var/run/snmpd.pid 127.0.0.1'
```

将 127.0.0.1 改为本地系统的 IP 地址，因为运行 Cacti 的系统将查询该本地系统。如果你不进行此更改，本地系统将不会响应来自远程系统的 snmpd 查询。

snmpd init 重启 snmpd 守护进程：

```
$ sudo service snmpd restart
* Restarting network management services:
```

你可以使用 status 参数来检查守护进程是否在运行（snmpd 的工作不需要 snmptrapd）：

```
$ sudo service snmpd status
* snmpd is running
* snmptrap is not running
```

# 656 第17章 配置与监控局域网 (LAN)

![](img/45ff4cd21497435daa35084a84b95d07_706_0.png)

图 17-10 添加设备

# 添加设备

在连接到 Cacti 的 Web 浏览器中，点击 Console 标签页，并选择 Configuration（配置）⇨ Settings（设置），然后点击 General（常规）标签页，并在名为 SNMP Version（SNMP 版本）的下拉列表中选择 Version 1（不是 SNMP Utility Version）。默认情况下，SNMP 运行时的团体设置为 public；除非你有相应理由，否则不要更改此设置。点击 Save（保存）。

接下来选择 Management（管理）⇨ Device（设备），点击屏幕右上角的 Add（添加，字很小）。或者，你可以选择 Create（创建）⇨ New Graphs（新图表），然后点击 Create New Host（新建主机）。Cacti 会显示一个允许你指定新设备的屏幕（图 17-10）。

如果你按照说明设置了 SNMP 版本（即 Version 1），则 SNMP 设置将如图 17-10 所示。在标记为 Description（描述）的文本框中填入对要监控系统的适当描述。在标记为 Host（主机）的文本框中输入 IP 地址或完全限定域名。

# 介绍 CACTI 657

![](img/45ff4cd21497435daa35084a84b95d07_707_0.png)

图 17-11 关于新系统

Cacti 使用 SNMP 收集信息。如果一切顺利，它将在屏幕顶部显示关于新系统的图表（图 17-11）。

创建图表 Cacti 会显示你要创建的图表。Cacti 会显示关于新节点的图源（图 17-12，下一页）。

创建图表 Cacti 会显示你要创建的图表。点击 Graphs（图表）标签页来添加图源。

将节点添加到树 Cacti 会显示你要创建的图表。点击 Management（管理）中的 Add（添加）来添加节点。

创建图表 Cacti 会显示你要创建的图表。点击 Settings（设置）来设置要创建的图源。

# 658 第17章 配置与监控局域网 (LAN)

![](img/45ff4cd21497435daa35084a84b95d07_708_0.png)

图 17-12 新节点的图表

现在你可以浏览生成的图表，选择感兴趣的时间段并了解更多。

# 更多信息

- 路由器操作系统：smoothwall.org, pfsense.com
- NdisWrapper：help.ubuntu.com/community/WifiDocs/Driver
- sourceforge.net/projects/ndiswrapper
- Cacti：cacti.net/additional_scripts
- 手册：cacti.net/downloads/html
- Cacti 论坛：forums.cacti.net
- RRDTool：oss.oteiker.net/rrdtool
- SNMP：www.net-snmp.org
- Linux 无线域网 HOWTO：https://www.hpl.com/personal/Jean_Tourril
- Linux 硬件兼容性 HOWTO

# 总结（注：根据页面，文中出现了两次 CHAPTER SUMMARY）

![](img/45ff4cd21497435daa35084a84b95d07_709_0.png)

图 17-13 新设备的图表

# 总结

局域网（LAN）连接一个地点的计算机，并允许连接的计算机共享互联网连接、文件和打印机。LAN上的每个系统或节点必须有一个网络接口卡（NIC）。NIC 可以通过线（有线）或无线波（无线）连接到网络。

基于以太网的 LAN 将计算机连接到集线器或交换机。集线器通常比交换机慢，对于小型 LAN 来说足够。无线接入点（WAP）将无线网络连接到有线网络。如果你设置的 LAN 连接到另一个网络（如互联网），则 LAN 需要路由器。路由器可以执行多种功能，最常见的是允许多个系统共享单个连接和 IP 地址；此功能称为 NAT。

在设置 LAN 时，许多工具非常有用。特别是网络连接窗口（nm-connection-editor）和 nm-applet 允许你配置 NIC（有线或无线）。

你可以配置 LAN 上的系统使用 NIS 作为登录服务器，这样你就不需要在每个系统上设置账户。你可以使用 NFS，它允许你

