
如果你的机器作为一个或多个子网络的路由器运行，路由守护进程将为你省去在所有机器上设置所有子网络路由的繁琐任务。它的作用是向其他机器发送路由表条目。

如果你想发送路由表条目，你需要禁用“不发送任何路由”（`Do not send out any routes`）选项。如果你的机器同时也作为默认网关运行，你可以选择发送默认路由表。例如，如果你使用这台机器连接 Internet 并希望向所有其他机器发送路由时就是如此。

## 机器名的搜索路径

![](img/b8bd4b587c4dd67fa1a0b81ef3d39692_122_0.png)

将 IP 地址解析为机器名有三种不同的方式：

1. `hosts`：系统在 `/etc/hosts` 文件中查找与 IP 地址或相应名称对应的条目，并返回所需的结果。这是最简单的方法，对于小型网络通常足够；
2. `DNS`：系统查询远程名称服务器。系统查询服务器的方法之前已解释过；
3. `NIS`（网络信息系统）：参见下段落

你可以使用或不使用任何你需要的服务，并指定查询服务的顺序。如果第一个失败，第二个将接管，依此类推。`hosts DNS` 是最好的折中方案，至少你不需要使用 `NIS`，就像在某些大型 Unix 网络中那样。

### NIS

![](img/b8bd4b587c4dd67fa1a0b81ef3d39692_123_0.png)

`NIS` 是由太阳微系统（Sun Microsystems）发明的一种协议。它避免了信息冗余，例如在“导出”用户账户、服务等方面。如果你想查询现有的 `NIS` 域，需要在相关字段中输入域名以及服务器的名称或地址。如果你想创建一个 `NIS` 服务，请咨询 `NIS-HOWTO`。

### PPP/SLIP/PLIP

![](img/b8bd4b587c4dd67fa1a0b81ef3d39692_124_0.png)

`PPP`、`SLIP` 和 `PLIP` 是三种类似于以太网卡的网络接口，但区别在于它们不是永久激活的。这就是为什么它们被分配了专门的章节。不会讨论 `SLIP` 和 `PLIP` 接口的配置，部分因为它们是两个不常用的接口，部分因为它们的配置相对简单。另一方面，`PPP` 接口非常常见：

![](img/b8bd4b587c4dd67fa1a0b81ef3d39692_125_0.png)

如果你想通过调制解调器建立 Internet 连接，你需要选择这种类型的接口。对应调制解调器的串口端口由文件 `/dev/ttySx` 指定，其中 `x` 代表串口号，`/dev/ttyS0` 对应于第一个并行端口（`COM1`）等。

你需要从你所选择的 Internet 服务提供商处查询你是否使用 `PAP`，如果是的话，你应该激活相应的选项，并且在此处填写连接名称和密码。然后你需要点击“自定义”（`Customize`），它包含四个个标签页。你只需要修改的选项如下：

1. `PAP` 标签页（如果你使用 `PAP`）；
2. 在“硬件”（`Hardware`）标签页中，你可以允许每个用户激活或禁用接口。

### 用户账户

![](img/b8bd4b587c4dd67fa1a0b81ef3d39692_126_0.png)

`linuxconf` 的此模块允许你在设置普通用户账户之外，设置特殊账户，如 `PPP` 账户（如果你的机器作为 `PPP` 服务器运行）、邮件别名和密码验证规则。即使你是一个重要网络的管理员，可能也不需要第一个标签页。

用户账户：

![](img/b8bd4b587c4dd67fa1a0b81ef3d39692_127_0.png)

## 5.5. 使用 LINUXCONF

用户列表将如下所示。用户有一个标识其身份的数字（`uid`）。最好保留所有数字小于 500 的账户原样，它们具有。添加用户的对话框如下：

![](img/b8bd4b587c4dd67fa1a0b81ef3d39692_128_0.png)

`Passwd` 按钮允许更改用户的密码。`Tasks` 按钮允许你按固定间隔执行任务（使用 `cron` 守护进程）。要执行的任务必须写在一行。这样，该任务将

![](img/b8bd4b587c4dd67fa1a0b81ef3d39692_129_0.png)

你可以激活和禁用所有条目。

用户组：原理与添加或删除用户非常相似。创建专用组可以帮助该组成员访问某些文件，前提是权限设置适当。用户可以属于一个或多个组。

## 8.5. 使用 LINUXCONF

你可以编辑、添加或删除组 选择 `[添加]` 来添加新定义

| 组 | ID | 备成员 |
|---|---|---|
| `nobody` | `yy` | |
| `nogrp` | `100` | `games` |
| `popusers` | `231` | |
| `postfix` | `233` | |
| `postgres` | `234` | |
| `pppusers` | `230` | |
| `root` | `0` | `root` |
| `slipusers` | `232` | |
| `slocate` | `21` | |
| `squid` | `16` | |
| `sys` | `3` | `root bin adm` |
| `tty` | `5` | |
| `users` | `500` | `desdemona` |
| `utmp` | `101` | |
| `uucp` | `14` | `uucp` |
| `wheel` | `10` | `root` |
| `xfs` | `102` | |

![](img/b8bd4b587c4dd67fa1a0b81ef3d39692_130_0.png)

### 文件系统

![](img/b8bd4b587c4dd67fa1a0b81ef3d39692_131_0.png)

此模块允许你从繁琐的挂载命令中解放出来。你可以处理三种分区，即通过添加、删除或修改挂载选项。这里只处理本地磁盘，你可以选择“访问本地磁盘”标签页来访问它们。你将看到本地存储设备的列表（硬盘分区、磁盘、光驱、其他）。

添加分区需要填写不同的字段：

## 8.5 使用 LINUXCONF

你可以编辑、添加或删除挂载项
选择 `[Add]` 添加新定义

| 来源 | 挂载点 | 文件系统类型 | 大小 | 分区类型 | 状态 |
|---|---|---|---|---|---|
| `/dev/sda1` | `/` | `ext2` | `2055M` | `Linux(83)` | 已挂载 |
| `/dev/hdb1` | `/home` | `ext2` | `2051M` | `Linux(83)` | 已挂载 |
| `/dev/hda2` | `/usr` | `ext2` | `4094M` | `Linux(83)` | 已挂载 |
| `/dev/hdb3` | `/usr/local` | `ext2` | `1527M` | `Linux(83)` | 已挂载 |
| `/dev/hdc1` | `/opt` | `ext2` | `3098M` | `Linux(83)` | 已挂载 |
| `/dev/fd0` | `/mnt/floppy` | `vfat` | | | |
| `/dev/cdrom` | `/mnt/cdrom` | `iso9660` | | | |
| `none` | `/dev/ptspts` | `devpts` | | | 已挂载 |

![](img/b8bd4b587c4dd67fa1a0b81ef3d39692_132_0.png)

## 基础

在本节中，你指定要挂载的分区（这里是次主 IDE 磁盘的第一分区）、该分区上可能的文件系统类型以及将作为挂载点的目录。

## 第 8 章 系统管理

你必须输入卷或分区的规格，以及你希望在该工作站的目录结构中安装该卷的位置（挂载点）

| 基础 | 选项 | Dos 选项 | 杂项 |
| --- | --- | --- | --- |
| 分区 | `/dev/hdc1` | | | |
| 类型 | `ext2` | | | |
| 挂载点 | `/opt` | | | |

![](img/b8bd4b587c4dd67fa1a0b81ef3d39692_133_0.png)

### 选项

本节介绍了一系列可能的挂载选项。注意，某些文件系统对应的某些选项没有实际意义。例如，`FAT` 分区（12, 16 或 32）不支持特殊文件或配额。

如果目标分区对于系统的运行至关重要，你应该将 `dump` 频率（`dump frequency`）字段设置为 1，否则该分区在启动时永远不会被检查，并且

## 8.5. 使用 LINUXCONF

你可能会面临糟糕的意外。根分区的 `fsck` 优先级（`fsck priority`）字段必须为 1，其他系统分区为 2 或更多。对于任何其他分区或非必需外设，这两个字段必须留为 0。

![](img/b8bd4b587c4dd67fa1a0b81ef3d39692_134_0.png)

### DOS 选项

你必须输入卷或分区的规格，以及你希望在该工作站的目录结构中安装该卷的位置（挂载点）

![](img/b8bd4b587c4dd67fa1a0b81efd39692_135_0.png)

正如名称所示，本节用于配置特定于 `DOS` 文件系统（`msdos` 和 `FAT`）的选项。如果指定了用户或组，则挂载目录的所有文件将属于该用户或组。默认权限（`default permission`）字段的格式与 `umask` 命令的格式相同。例如，`027` 赋予所有用户 (0) 所有权限，剥夺所有组的写入权限 (2)，并剥夺其他用户的所有权限 (7)。翻译模式（`translation mode`）可以留为 `auto`。

### 其他

正如名称所示，本节允许你指定前几节中提供的其他选项。查看 `mount` 手页以获取可用选项列表。

### 更多...

`linuxconf` 显然还有很多功能，而且你会发现这里没有讨论过的模块。如果你对网络服务（`NFS`, `NIS`, `Samba` 等）的配置感兴趣，我强烈建议你在尝试之前阅读相关的 `HOWTOs`。

## 第 9 章 文档

### 9.1 "HOWTOs"

`HOWTOs` 文档对于给定的主题非常详尽。例如，关于在 Linux 下刻录 CD，请参考 `CD-Writing HOWTO`。要设置防火墙，请参考 `firewall HOWTO`。

你也可以在 `/usr/doc/howto/` 目录下查看这些文档，格式有：`text`、`HTML`（使用 `kfm` 或 `netscape` 查看）或 `dvi`（使用 `xdvi` 查看）。`/usr/doc/howto/mini/` 包含了 `mini-HOWTO`。

以下是可用的 `HOWTO` 列表：

- `3Button-Mouse`
- `ADSL Linux-FreeBSD-mini-HOWTO`
- `ADSM-Backup Linux-NT-Loader`
- `Alife Linux-Win95`
- `Advocacy Load-Win95`
- `Apache-SSL-PHP-Loopback-Root-FS`
- `Back-With-MSDOS Mac-Terminal`
- `Battery-Powered Mail-Queue`
- `Boca Mail2News`
- `BogoMips Man-Page`
- `Bridge Modules`
- `Bridge-Firewall Multiboot-with-LILO`
- `Bzip2 NCD-X-Terminal`
- `Cable-Modem NFS-Root`
- `Clock NFS-Root-Client`
- `Coffee Netscape-Proxy`
- `Colour-ls News-Leafsite`
- `Cyrus-IMAP Offline-Mailing`
- `DHCP Partition`
- `DHCPcd Partition-Rescue`
- `DPT-Hardware-RAID Path`
- `Diald Pre-Installation-Checklist`
- `Diskless Process-Accounting`
- `Ext2fs-Undletion Proxy-ARP-Subnet`
- `Fax-Server Public-Web-Browser`
- `Firewall-Piercing Qmail-MH`
- `GIS-GRASS Quota`
- `GTEK-BBS-550 RCS`
- `Hard-Disk-Upgrade README`
- `INDEX RPM-Slack`
- `INDEX.html Remote-Boot`
- `IO-Port-Programming Remote-X-Apps`
- `IP-Alias SLIP-PPP-Emulator`
- `IP-Masquerade Sendmail-UUCP`
- `IP-Subnetworking Small-Memory`
- `ISP-Connectivity Software-Building`
- `Install-From-ZIP Software-RAID`
- `Kerneld Soundblaster-AWE`
- `LBX StarOffice`
- `LILO Term-Firewall`
- `Large-Disk TkRat`
- `Leased-Line Token-Ring`
- `Linux-DOS-Win95-OS2 Ultra-DMA`

### 第 9 章文档

- `DNS-HOWTO`
- `DOS-Win-Linux-HOWTO`
- `DOS-to-Linux-HOWTO`
- `Danish-HOWTO`
- `Distribution-HOWTO`
- `ELF-HOWTO`
- `Emacspeak-HOWTO`
- `Esperanto-HOWTO`
- `Ethernet-HOWTO`
- `Finnish-HOWTO`
- `Firewall-HOWTO`
- `French-HOWTO`
- `FTP-HOWTO`
- `GCC-HOWTO`
- `German-HOWTO`
- `Glib-HOWTO`
- `GRASS-Quota`
- `Hardware-HOWTO`
- `Hebrew-HOWTO`
- `INFO-SHEET`
- `IP-Alias-HOWTO`
- `IP-Chains-HOWTO`
- `IP-Hookup-HOWTO`
- `IP-Masquerade-HOWTO`
- `IP-Subnetworking-HOWTO`
- `IPX-HOWTO`
- `Installation-HOWTO`
- `Intranet-Server-HOWTO`
- `Italian-HOWTO`
- `Java-CGI-HOWTO`
- `Kernel-HOWTO`
- `Keyboard-and-Console-HOWTO`
- `KickStart-HOWTO`
- `Linux-Doc-HOWTO`
- `Linux-HOWTO`
- `Mail-HOWTO`
- `Mail2News-HOWTO`
- `Multi-Disk-HOWTO`
- `Multicast-HOWTO`
- `NET-3-HOWTO`
- `NFS-HOWTO`
- `NIS-HOWTO`
- `Networking-Overview-HOWTO`
- `Optical-Disk-HOWTO`
- `Oracle-HOWTO`
- `PCI-HOWTO`
- `PCMIA-HOWTO`
- `PPP-HOWTO`
- `Parallel-Processing-HOWTO`
- `Pilot-HOWTO`
- `Polish-HOWTO`
- `PostgreSQL-HOWTO`
- `Printing-HOWTO`
- `Printing-Usage-HOWTO`
- `Quake-HOWTO`
- `README`
- `Reading-List-HOWTO`
- `Root-RAID-HOWTO`
- `SMB-HOWTO`
- `Security-HOWTO`
- `Serial-Programming-HOWTO`
- `Shadow-Password-HOWTO`
- `Slovenian-HOWTO`
- `Sound-HOWTO`
- `Sound-Playing-HOWTO`
- `Spanish-HOWTO`
- `Text-Terminal-HOWTO`
- `Thai-HOWTO`
- `Tips-HOWTO`
- `UPS-HOWTO`
- `UUCP-HOWTO`
- `User-Group-HOWTO`
- `VAR-HOWTO`
- `VMS-to-Linux-HOWTO`
- `Virtual-Services-HOWTO`
- `WWW-HOWTO`
- `WWW-SQL-HOWTO`
- `XFree86-HOWTO`
- `Free86-Video-Timings-HOWTO`

### 9.1. "HOWTOS"

`Mini-HOWTOS`:

- `3Button-Mouse Linux-FreeBSD`
- `ADSL Linux-FreeBSD-mini-HOWTO`
- `ADSM-Backup Linux-NT-Loader`
- `Alife Linux-Win95`
- `Advocacy Load-Win95`
- `Apache-SSL-PHP-Loopback-Root-FS`
- `Back-With-MSDOS Mac-Terminal`
- `Battery-Powered Mail-Queue`
- `Boca Mail2News`
- `BogoMips Man-Page`
- `Bridge Modules`
- `Bridge-Firewall Multiboot-with-LILO`
- `Bzip2 NCD-X-Terminal`
- `Cable-Modem NFS-Root`
- `Clock NFS-Root-Client`
- `Coffee Netscape-Proxy`
- `Colour-ls News-Leafsite`
- `Cyrus-IMAP Offline-Mailing`
- `DHCP Partition`
- `DHCPcd Partition-Rescue`
- `DPT-Hardware-RAID Path`
- `Diald Pre-Installation-Checklist`
- `Diskless Process-Accounting`
- `Ext2fs-Undletion Proxy-ARP-Subnet`
- `Fax-Server Public-Web-Browser`
- `Firewall-Piercing Qmail-MH`
- `GIS-GRASS Quota`
- `GTEK-BBS-550 RCS`
- `Hard-Disk-Upgrade README`
- `INDEX RPM-Slack`

## 第 10 章

## 附录

### 10.1 常见问题 (FAQ)

以下是一些常见的 Linux-Mandrake 错误信息及其相应的解释。此 `FAQ` 在 Linux-Mandrake 网上定期更新。

“无法显示目录 `xxx` 的内容”

您没有读取该目录内容的权限。请检查目录权限。

“无法读取 `xxx`。文件不存在或访问被拒绝。”

通常，此的原因是您没有读取该文件的权限。请检查文件权限。

### "KFM 无法连接到 'localhost'"

您修改了环回配置。
输入：`localhost`

```
localhost
```
