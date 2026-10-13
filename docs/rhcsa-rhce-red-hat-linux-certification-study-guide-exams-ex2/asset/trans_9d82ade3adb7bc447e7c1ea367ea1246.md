

![](img/9139201cfcaf4292284a0eed074928e5_981_0.png)

## 术语表

## 2 术语表

**访问控制列表 (ACL)**  访问控制列表 (ACLs) 为文件和目录提供额外的访问控制层；与 `setfacl` 和 `getfacl` 命令相关。

**地址解析协议 (ARP)**  一种将 IP 地址映射到网卡上的硬件地址的协议。

**替代方案**  alternatives 命令支持默认配置的更改；例如，`alternatives --config mta` 命令支持管理员在 sendmail 和 Postfix 之间切换当前 SMTP 服务器。

**anacron**  anacron 服务旨在运行服务器断电期间无法运行的 `cron` 作业；现已通过 `/etc/anacrontab` 文件集成到周期性作业管理中。

**apachectl**  `apachectl` 命令是启动、停止和重新加载 Apache 服务器的首选方法；`apachectl graceful` 命令在不中断已连接用户的情况下重新加载修订后的配置文件。

**Apache Web 服务器**  Apache Web 服务器提供普通和安全 Web 服务，由 `httpd` 守护进程控制。

**arp（地址解析协议）**  `arp` 命令用于查看或修改内核的 ARP 表。使用 `arp`，您可以检测网络上重复地址等问题。或者，您可以使用 `arp` 添加来自本地局域网所需的条目。

**at**  `at` 命令类似于 `cron`，但允许您一次性运行作业。

**自动挂载器**  自动挂载器可配置为按需挂载本地和网络目录。它在 `/etc` 目录中的 `auto.master`、`auto.net`、`auto.misc` 和 `auto.smb` 文件中进行配置。

**bash**  Linux 用户的默认 shell 是 bash，也称为 Bourne-Again Shell。

**BIND（伯克利因特网名称域）**  BIND 是用于设置域名系统 (DNS) 服务的软件。关联的守护进程是 *named*。

**BIOS**  BIOS 是基本输入/输出系统，在您开机时运行基本命令。在大多数现代系统中，它已被 UEFI 取代。BIOS 菜单允许您自定义许多选项，包括启动介质的顺序。

**/boot**  包含启动 Linux 所需主要文件的目录，包括 Linux 内核和初始 RAM 磁盘。默认情况下，/boot 挂载在单独的分区上。

**仅缓存名称服务器**  一种仅缓存名称服务器，执行 DNS 服务器的许多功能。它存储最近名称搜索关联的 IP 地址，供本地局域网上的其他计算机使用。

**CentOS**  社区企业操作系统，是基于 Red Hat 源代码的 RHEL “重建” 版本。

**chage**  *chage* 命令管理密码的过期日期。

**chattr**  *chattr* 命令允许您更改文件属性。

**chgrp**  *chgrp* 命令更改文件所属的组。

**chkconfig**  *chkconfig* 命令管理运行级服务信息。它可以激活或停用服务。它还可以自定义特定运行级下的服务。

**chmod**  *chmod* 命令更改文件的权限。

**chown**  *chown* 命令更改文件的所有权。

**CIFS（通用互联网文件系统）**  CIFS 是微软对其网络软件改进的名称。它也包含在 Samba 的最新版本 3.5.4 中，该版本随 RHEL 6 提供。

## 4 术语表

**cron**  一种按周期运行作业的服务。它在 /etc/crontab 中配置；默认情况下，它在 /etc/cron.hourly、/etc/cron.daily、/etc/cron.weekly 和 /etc/cron.monthly 目录中执行作业。

**crontab**  单个用户可以运行 **crontab** 命令来配置定期运行的作业。

**cryptsetup**  **cryptsetup** 命令可用于配置带有 LUKS 加密的卷。

**/dev**  包含设备文件的目录，用于表示硬件和软件组件。

**DHCP（动态主机配置协议）**  DHCP 客户端从本地网络上的 DHCP 服务器租用固定时间段的 IP 地址。

**Disk Druid**  Anaconda 的硬盘管理程序。虽然其功能类似于 **fdisk** 和 **parted**，但 Disk Druid 更易于使用。然而，它仅在 Linux 安装过程中可用。

**dmesg**  **dmesg** 命令列出内核环形缓冲区和初始启动消息。如果系统成功启动，/var/log/dmesg 是查找消息的地点之一。

**DNS（域名系统）**  DNS 服务维护一个完全限定域名（如 www.mcgraw-hill.com）和 IP 地址（如 198.45.24.143）的数据库。如果域名不在本地数据库中，DNS 通常配置为查询其他更权威的 DNS 服务器。关联的守护进程是 **named**。

**dumpe2fs**  **dumpe2fs** 命令提供有关分区格式的大量信息。

**e2label**  **e2label** 命令将设备与标签关联，通常是文件系统目录。

**edquota**  **edquota** 命令编辑用户或组的配额。

**环境**  每个用户的环境指定默认设置，如登录提示、终端、PATH、邮件目录等。

**/etc/fstab**  /etc/fstab 配置文件定义默认挂载目录。

**/etc/inittab**  /etc/inittab 配置文件设置默认运行级并启动关键进程，如终端 gettys。

**exportfs**  **exportfs** 命令允许将共享的 NFS 目录与网络共享。

**ext2/ext3/ext4**  第二、第三和第四扩展文件系统（ext2、ext3、ext4）是 RHEL 6 的标准。ext3 和 ext4 文件系统包含日志功能。ext4 文件系统可处理高达 1 艾字节（1,000,000 TB）的文件。

**fdisk**  一个标准磁盘分区命令实用程序，允许您修改物理和逻辑磁盘分区布局。

**Fedora Linux**  自由可用的 Red Hat Linux 版本的继任者；有关此 Linux 发行版的更多信息可在网上 www.fedoraproject.org 获取。

**文件系统**  在 Linux 中，文件系统有多重含义。它指挂载的目录；根目录（/）的文件系统格式化在其自己的分区上。它也指文件格式；RHEL 6 卷通常格式化为 ext4 文件系统。

**防火墙**  防止未经授权访问网络的硬件或软件系统。

**fsck**  fsck 命令检查 Linux 分区上的文件系统一致性。针对特定文件系统有此命令的变体，如 **fsck.ext2**、**fsck.ext3**、**fsck.ext4**，甚至 **fsck.vfat**。

**FTP（文件传输协议）**  FTP 协议是专为最佳文件传输速度设计的 TCP/IP 协议。

**网关**  在 Linux 中，网关一词有多重含义。网关可以是从一台计算机或网络到另一网络的路由。默认网关地址是连接局域网与另一网络（如互联网）的计算机或路由器的 IP 地址。网关也可以是网络之间的路由器。

**genkey**  `genkey` 命令支持为安全网站生成 SSL 密钥。

**getfacl**  `getfacl` 命令允许您读取文件和目录上的访问控制列表 (ACL)。

**getsebool**  `getsebool` 命令允许您读取 SELinux 布尔值的当前状态。

**getty**  getty 是一个终端程序，包含登录和密码提示。虚拟控制台 gettys 通过 `/etc/init` 目录中的 start-ttys.conf 文件进行配置。

**GNOME（GNU 网络对象模型环境）**  GNOME 是 Red Hat Enterprise Linux 的默认 GUI 桌面。

**GPG（GNU 隐私保护）**  GPG 是随 Red Hat Enterprise Linux 提供的 OpenPGP 标准实现。您可以使用 `gpg2` 命令在 RHEL 6 上实现此功能。

**GPL**  GPL 是 Linux 通用公共许可证，大多数 Linux 软件均在此许可证下发布。

**组 ID**  每个 Linux 组都有一个组 ID，如 `/etc/group` 中所定义。

**GRUB（大统一引导加载程序）**  RHEL 的默认引导加载程序。

**grub-install**  `grub-install` 命令从 MBR 添加指向 GRUB 引导加载程序配置文件 `/boot/grub/grub.conf` 的指针。

**主目录**  主目录是 Linux 用户的登录目录。通常为 `/home/user`，其中 *用户* 是用户的登录名。它在任何 Linux 命令中也由波浪号（\~）表示。

