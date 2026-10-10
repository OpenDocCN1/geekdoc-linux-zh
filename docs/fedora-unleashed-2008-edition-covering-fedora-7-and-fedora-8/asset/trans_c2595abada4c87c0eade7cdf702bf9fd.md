

- [http://www.linux-usb.org/USB-guide/x498.html](http://www.linux-usb.org/USB-guide/x498.html)—用于大容量存储设备的 USB 指南。如果您有 USB 设备并且需要知道它是否受支持，请在此处查看。

- [http://www.backupcentral.com/amanda.html](http://www.backupcentral.com/amanda.html)—这是《Unix 备份与恢复》一书中关于 Amanda 的章节（由 John R. Jackson 撰写，O’Reilly and Associates 出版）。该章节在线可用，涵盖了使用 Amanda 的方方面面。该网站提供了针对该章节的便捷搜索工具。

- [http://twiki.org/cgi-bin/view/WikiLearn/RsyncingALargeFileBeginner](http://twiki.org/cgi-bin/view/WikiLearn/RsyncingALargeFileBeginner)—使用 rsync 传输一个大文件以“修复”未通过 md5sum 检查的本地 ISO 镜像。

- [http://www.lycoris.org/sections.php?op=viewarticle&artid=8](http://www.lycoris.org/sections.php?op=viewarticle&artid=8)—Lycoris ISO rsync 迷你 HOWTO。使用 rsync 同步文件的分步教程。

- [http://www.mikerubel.org/computers/rsync_snapshots/](http://www.mikerubel.org/computers/rsync_snapshots/)—使用 rsync 进行自动化快照式备份。

- [http://www.mondorescue.org/](http://www.mondorescue.org/)—Mondo Rescue 是一个独立于 Fedora 的裸机备份/救援工具，使用 CD、DVD、磁带或 NFS；它可以生成可启动 CD 来恢复系统。

- [http://www.ccp14.ac.uk/ccp14admin/linux-server/mondorescue/dvd_mondo.html](http://www.ccp14.ac.uk/ccp14admin/linux-server/mondorescue/dvd_mondo.html)—一个使用 MondoRescue 在 DVD 上进行备份的 HOWTO。

- [http://www.linuxorbit.com/modules.php?op=modload&name=Sections&file=index&req=viewarticle&artid=222&Page=1](http://www.linuxorbit.com/modules.php?op=modload&name=Sections&file=index&req=viewarticle&artid=222&Page=1)—使用 split 和 mkisofs 手动将大型存档备份到 CD 的 HOWTO。

*此页故意留白*

## 第 14 章
### 网络

#### 本章内容

- 使用网络配置工具
- 奠定基础：localhost 接口
- 基于 TCP/IP 的网络连接
- 高级无线网络
- 动态主机配置协议 (DHCP)
- 超越局域网走向互联网
- 配置拨号互联网访问
- 故障排除：连接问题
- 参考

开源技术（特别是 Linux）的一大优势在于它现在已经足够成熟，可以毫不费力地在多种不同的网络环境以及互联网中使用。凭借对标准互联网协议 TCP/IP 的强大支持，Linux 还可以与所有版本的 UNIX、Mac OS X、Windows（借助 Samba）、NetWare（IPX）以及甚至 DECnet 和 Banyan Vines 等较旧的协议进行通信。许多组织使用 Linux 作为互联网网关，允许许多不同的客户端通过 Linux 访问互联网，并经由电子邮件和即时通讯进行通信。本章涵盖网络和互联网连接，因为大多数网络最终都会以某种方式连接到互联网。您将学习如何正确掌握基础知识，包括使用 Fedora 配置和管理网络接口卡（NIC）以及其他网络服务。您还将了解如何从命令行管理网络服务——如果您曾经被困在命令行提示符下，这又是一个重要的一课。我们还探讨了连接选项，包括入站和出站网络流量，以及 PPP（点对点协议）的重要性。此外，还包括 Fedora 图形化管理客户端概览，它们正变得越来越流行。

### 使用网络配置工具

如果在初始安装后添加或更换网络硬件，您必须配置新硬件。您可以使用命令行或图形配置工具来执行此操作。要使用命令行配置网络客户端主机，您可以使用一系列命令的组合，或编辑 /etc/sysconfig 目录下的特定文件。要通过图形界面配置硬件，您可以使用 Fedora 提供的名为 system-config-network 的图形工具。本节介绍了您可以用来在 Fedora 系统上配置网络接口和网络设置的命令行和图形软件工具。您将看到如何控制您的 NIC 并管理系统与您网络的交互方式。

对于 Linux 新手来说，使用命令行配置工具可能看起来很难。对于任何网络新手来说，system-config-network 图形工具是首选方案。手动和图形方法都需要 root 访问权限才能工作。如果您没有 root 访问权限，请在尝试这些操作之前获取它。您不应编辑系统中用于图形网络管理工具的任何脚本或设置文件。下次运行该工具（如 system-config-network）时，您的更改将丢失！要么使用手动方法并编写自己的网络设置脚本，要么坚持使用图形配置实用程序。

> **注意**
> 本节描述的网络配置过程适用于客户端主机。在安装期间无法执行服务器网络配置，如域名系统 (DNS) 和 DHCP。（有关配置 DNS 的更多信息，请参见第 23 章“管理 DNS”；有关该项的更多信息，请参见本章后面的“DHCP”部分。）

#### 使用图形配置工具

如果您是网络新手，或者命令行使用尚未熟练，图形配置工具是您在 Fedora 中配置新硬件的最佳方法。与大多数图形工具一样，system-config-network 允许您填写空白；按下正确的按钮，该工具就会修改所需的文件并发出正确的命令。请记住，您必须是 root 才能运行 system-config-network。

您可以通过转到“系统”、“管理”菜单并选择“网络”来访问 system-config-network。由于您可以使用此工具进行系统范围的更改，因此系统会要求您输入 root 密码。

启动后，system-config-network 将显示图 14.1 中所示的屏幕。单击 DNS 选项卡以配置系统的 DNS 设置、主机名或 DNS 搜索路径。单击 Hosts 选项卡，然后单击“新建”或“编辑”按钮（选择主机后）以创建或编辑系统中的 /etc/hosts 文件中的条目——例如，添加网络上主机的 IP 地址、主机名和别名。有关编辑主机条目的示例，请参见图 14.2。

![](img/34e72348d53ca54c2a1d9c871316691b_328_0.png)

图 14.1 使用初始 *system-config-network* 网络屏幕开始配置您的网络客户端主机。

![](img/34e72348d53ca54c2a1d9c871316691b_328_1.png)

图 14.2 高亮显示现有条目，然后单击“编辑”按钮以更改网络配置屏幕中 Hosts 选项卡下的 */etc/hosts* 条目。

单击 Devices 选项卡，然后单击“新建”或选择现有设置并单击“编辑”，以自动或手动设置以太网设备。图 14.3 显示了以太网设备对话框，其中包含为 *静态* 或固定 IP 地址分配所需的所有必要信息。选择网卡获取配置的方式：手动、通过 *动态主机配置协议 (DHCP)*（参见下一节）或通过 Bootp。只需根据需要填写空白即可。

![](img/34e72348d53ca54c2a1d9c871316691b_329_0.png)

图 14.3 通过双击设备来配置以太网设备以使用静态 IP 地址。

> **注意**
> Bootp 是构建 DHCP 的初始协议，并且基本上已被 DHCP 取代。

完成 NIC 配置或编辑 NIC 的 IP 地址或分配方案后，使用文件菜单中的“保存”菜单项保存您的更改。请注意，您还可以使用配置文件菜单（如图 14.1 中先前所示）为您的已安装 NIC 创建不同的网络配置和 IP 地址分配。例如，如果您想在运行 Fedora 的笔记本电脑上为家庭或工作创建不同的网络设置，这非常有用。

#### 命令行网络接口配置

您可以使用基本的 Linux 网络实用程序从命令行配置网络接口。您通过使用命令更改当前设置或编辑一系列系统文件来使用命令行配置网络客户端主机。两个命令，`ifconfig` 和 `route`，用于网络配置。`netstat` 命令显示有关网络连接的信息。

