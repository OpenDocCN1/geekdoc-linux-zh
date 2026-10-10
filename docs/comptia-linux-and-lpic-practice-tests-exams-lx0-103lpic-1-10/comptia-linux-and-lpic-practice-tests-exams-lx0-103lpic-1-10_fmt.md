
# CompTIA Linux+ 和 LPIC 实践指南：考试 LX0-103／LPIC-1 101-400, LX0-104／LPIC-1 102-400, LPIC-2 201, 以及 LPIC-2 202

提供了超过 1,200 道题，包括 4 份模拟考试，涵盖了 CompTIA Linux+、LPIC-1 和 LPIC-2 的所有目标领域。

是《CompTIA Linux+ Study Guide: Exam LX0-103 and Exam LX0-104》、《LPIC-1 Study Guide: Exam 101-400 and Exam 102-400》以及《LPIC-2 Study Guide: Exam 201 and Exam 202》的补充。

- 考试 LX0-103/LPIC-1 101-400
- LX0-104/LPIC-1 102-400
- LPIC-2 201, 以及 LPIC-2 202

Steven Suehring

在加拿大同步出版

341

## 致谢

到某一点，写致谢比写书本身变得困难。我在这一点上比写书其他部分花费了更长时间。感谢每一位直接或间接贡献的人。感谢 UWSP 的全体成员，对我的欢迎和帮助。感谢 Ken Brown 和 Gary Schwartz，与你们共同工作非常荣幸。当然，如果没有 Patti、Jess、Rob 和 Tim，致谢部分将是不完整的。感谢 Kent 一直的支持。期待未来。

## 关于作者

Steve Sueh 是威斯康星大学史文点分校计算与新媒体技术助理教授。在 2015 年加入教职之前，Steve 在技术工程、系统和网络管理以及系统架构领域拥有 20 年的领域经验。Steve 曾担任 LinuxWorld 杂志编辑。

## 引言

CompTIA Linux+ and LPIC Practice Tests 是《CompTIA Linux+ 学习指南》的配套读物。本书通过测试你对考试中所用概念和术语的理解，帮助你准备认证考试。书中包含 1,201 个问题、答案和解释，涵盖了考试所需的各个主题。

书中的每个章节都包含针对考试特定部分的题目。此外还有四个较长的模拟考试，涵盖了特定领域的问题。本书旨在与相关的认证书籍配合使用，并可帮助你发现可能需要进一步学习的领域。

## Linux+ 认证

CompTIA 认证以其持有者可以获得的额外收益而闻名。Linux+ 认证是证明你具备履行 Linux 管理相关职责所需知识的一种。它可以帮助你准备在 Linux 服务器上需要执行的工作。测试区域包括安装、服务器软件的编译与安装以及安全性。这些主题对于 Linux 管理员的日常工作至关重要。

重要的是，该认证并不绑定于特定的发行版，而是针对整个 Linux 生态系统。这能让你更好地应对在特定雇主或工作中遇到的各种 Linux 变体。

## 本书结构

本书由两个部分组成，每个部分基于 Linux+ 和 LPIC 认证系列中的一项考试。书中每个相关领域都有一个专门的章节。在书末，有四个对应一组特定领域的长模拟考试。

每个章节的开头都列出了该章节涵盖的目标领域。虽然题目本身源自这些目标，但你可以预计会涉及到其他与作为 Linux 管理员相关的知识。

## 引言

书中包含的复习题和最终复习测试并非源自真实的 Linux+ 考试题。它们的作用是让你接触底层内容，并提供一个类比的测试工具供你准备考试。背诵这些问题的答案并认为这样做就能通过考试，将不是一项有用的练习。基础科目是你学习的重点，这样你才能通过考试。

祝贺你决定通过这项认证来展示你的 Linux 管理技能。

## 如何使用本书以及交互在线学习环境和题库

本书包含 1200 道模拟测试题，将帮助你准备通过 Linux+ 和 LPIC 考试。与《CompTIA Linux+ and LPIC Practice Tests》配套的交互在线学习环境提供了一个强大的题库，帮助你准备认证考试并增加首次通过的概率！通过使用此题库，你可以提前识别薄弱环节，然后利用这些强大的测试功能制定稳固的学习策略。

题库还提供四个模拟考试。请像实际考试一样参加这些模拟考试（不使用任何参考资料）。完成第一场考试后，继续进行下一个，以巩固你的应试技巧。如果你的正确率超过 90%，就可以准备好参加认证考试了。

可以通过以下地址访问 Syex 交互在线题库：`http://www.wiley.com/Sybextestprep`。

## CompTIA Linux+ 练习：目标映射

### 目标映射表

| 目标 | 章节编号 |
|--- |--- |
| 101 系统架构 | 1 |
| 101.1 确定并配置硬件设置。 | 1 |
| 启用和禁用集成外设 | 1 |
| 配置带有或不带键盘等外部外设的系统 | 1 |
| 区分不同类型的质存储设备 | 1 |
| 了解冷插拔和热插拔设备的区别 | 1 |
| 确定设备的硬件资源 | 1 |
| 列出各种硬件信息的工具和程序（例如 `lsusb`, `lspci`） | 1 |
| 操作 USB 设备的工具和程序 | 1 |
| 对 `sysfs`, `udev`, `dbus` 的概念理解 | 1 |
| 101.2 启动系统。 | 1 |
| 在启动时为引导加载程序提供常用命令并在内核提供选项 | 1 |
| 展示从 `BIOS` 到启动完成的启动序列知识 | 1 |
| 理解 `SysVinit` 和 `systemd` | 1 |
| 对 `Upstart` 的了解 | 1 |

*(注：由于后续表格内容高度重复，此处省略重复部分的翻译，保持格式一致即可)*

### 103.8 使用 `vi` 执行基本文件编辑操作 3

- 使用 `vi` 导航文档 3
- 使用 `vi` 的基本模式 3
- 插入、编辑、删除、复制和查找文本 3

### 104.1 创建分区和文件系统。 4

- 管理 MBR 分区表 4
- 使用各种 `mkfs` 命令创建各种文件系统，例如：
    - `ext2/ext3/ext4`
    - `XFS`
    - `VFAT`
- 了解 `ReiserFS` 和 `Btrfs` 4
- 了解在 GPT 分区表下使用 `gdisk` 和 `parted` 的基本知识 4

### 104.2 维护文件系统的完整性 4

- 验证文件系统的完整性 4
- 监控剩余空间和 `inode` 4
- 修复简单的文件系统问题 4

### 104.3 控制文件系统的挂载和卸载。 4

- 手动挂载和卸载文件系统 4
- 配置启动时的文件系统自动挂载 4
- 配置用户可挂载的移除式文件系统 4

### 104.4 管理磁盘配额。 4

- 为文件系统设置磁盘配额 4
- 编辑、检查并生成用户配额报告 4

### 104.5 管理文件权限和所有权。 4

- 管理普通文件、特殊文件以及目录的访问权限 4
- 使用 `suid`、`sgid` 和粘滞位 (`sticky bit`) 等访问模式维护安全性 4
- 如何更改文件创建掩码 (`umask`) 4
- 使用组字段向组成员授予文件访问 4

### 104.6 创建并更改硬链接和符号链接。 4

- 创建链接 4
- 识别硬链接和/软链接 4
- 复制与链接文件 4
- 使用链接支持系统管理任务 4

### 104.7 查找系统文件并将文件放置在正确位置。 4

- 理解 FHS 标准下文件的正确位置 4
- 在 Linux 系统上查找文件和命令 4
- 了解 FHS 中定义的重要文件和目录的位置及用途 4

### 105 Shell、脚本和数据管理 5

#### 105.1 定制和使用 shell 环境。 5

- 在登录或启动新 `shell` 时设置环境变量（例如 `PATH`） 5
- 为频繁使用的命令序列编写 BASH 函数 5
- 为新用户账户维护用户骨架目录 (`skeleton directories`) 5
- 使用正确的目录设置命令搜索路径 5

#### 105.2 定制或编写简单脚本。 5

- 使用标准 `sh` 语法（循环、测试） 5
- 使用命令替换 5
- 测试命令返回的返回值以判断成功、失败或其他信息 5
- 向超级用户执行条件邮件发送 5
- 通过 `shebang` (`#!`) 行正确选择脚本解释器 5
- 管理脚本的位置、所有权、执行权限和 `SUID` 权限 5

#### 105.3 SQL 数据管理 5

- 使用基础 `SQL` 命令 5
- 执行基础数据操作 5

### 106 用户界面和桌面 6

#### 106.1 安装并配置 X11。 6

- 验证显卡和显示器是否受 `X server` 支持 6
- 了解 X 字体服务器 6
- 对 X Window 配置文件的基本理解和知识 6
- `LightDM` 的基本配置 6
- 开启或关闭显示管理器 6
- 修改显示管理器欢迎界面 6
- 了解 `XDM`、`KDM` 和 `GDM` 6

#### 106.3 辅助功能 (Accessibility)。 6

- 键盘辅助功能设置 (`AccessX`) 6
- 视觉设置和主题的基础知识 6
- 辅助技术 (`AT`) 的基础知识 6

### 用户和组管理 7

- 添加、修改和删除用户和组 7
- 管理密码/组数据库中的用户/组信息 7
- 创建特殊用途和限制账户 7

### 计划任务 7

- 管理 `cron` 和 `at` 任务 7
- 配置 `cron` 和 `at` 服务 7
- 配置 `anacron` 7

### 时间和日期 8

- 配置本地设置和环境变量 7
- 配置时区设置和环境变量 7
- 设置系统日期时间 8
- 将硬件时设置为 `UTC` 时间 8
- 配置正确的时区 8
- 基础 `NTP` 配置 8
- 使用 `pool.ntp.org` 服务的知识 8
- `ntpq` 命令的知识 8

### 108.2 系统日志。 8

- `syslog` 守护进程配置 8
- 理解标准设施 (`facilities`)、优先级和动作 (`actions`) 8
- `logrotate` 配置 8
- 了解 `rsyslog` 和 `syslog-ng` 8

### 108.3 邮件传输代理 (MTA) 基础。 8

- 创建邮件别名 (`aliases`) 8
- 配置邮件转发 8
- 常用 MTA 程序（`postfix`, `sendmail`, `qmail`, `exim`） 8

### 108.4 管理打印机和打印。 8

- 基础 `CUPS` 配置（本地和远程打印机） 8
- 管理用户打印队列 8
- 排除通用打印问题 8
- 从配置的打印队列中添加和删除任务 8

### 网络基础 9

- 演示互联网协议 9
- 掩码和 `CIDR` 表示法知识 9
- 私有和公共 `IP` 地址知识 9
- `TCP` 和 `UDP` 端口（20, 21, 22, 23, 25, 53, 80, 110, 123, 139, 143, 161, 162, 389, 443, 465, 514, 636, 993, 995 以及 `ICMP` 知识） 9
- `IPv4` 和 `IPv6` 之间的差异知识 9
- `IPv6` 的主要特性知识 9

### 109.2 基础网络配置。 9

- 手动和自动配置网络接口 9
- 基础 `TCP/IP` 主配置 9
- 设置默认路由 9
- 手动和自动配置网络接口和路由表（添加、停止、重启、重新配置网络接口） 9
- 修改、查看路由表并纠正设置错误的默认路由 9
- 调试与网络配置相关的问题 9
- 查询远程 `DNS` 服务器 9
- 配置本地名称解析并使用远程 `DNS` 服务器 9
- 修改名称解析的顺序 9

### 安全管理 10

- 审计系统以查找带有 `suid/sgid` 位的文件 10
- 设置或更改用户密码和年龄信息 10
- 能够使用 `nmap` 和 `netstat` 发现系统上的开放端口 10
- 设置用户登录、进程和内存使用的限制 10
- 确定哪些用户已登录系统或当前正在登录 10
- 基础 `sudo` 配置和使用 10

# 导言

# xxvii

### 110.2 设置主机安全。 10

- 了解 `shadow` 密码及其工作原理 10
- 关闭未使用的网络服务 10
- 理解 `TCP wrappers` 的作用 10

### 110.3 使用加密保护数据。 10

- 执行基础 `OpenSSH 2` 客户端配置和使用 10
- 理解 `OpenSSH 2` 服务器主机密钥的作用 10
- 执行基础 `GnuPG` 配置、使用和撤销 10
- 理解 `SSH` 端口隧道（包括 `X11` 隧道） 11

### 性能监控 11

- 测量 `CPU` 使用 11
- 测量内存使用 11
- 测量磁盘 `I/O` 11
- 测量网络 `I/O` 11
- 测量防火墙和路由吞吐量 11
- 映射客户端带宽使用 11
- 匹配/关联系统症状与可能的问题 11
- 估算吞吐量并识别包括网络的系统瓶颈 11
- 使用监控和测量工具监控 `IT` 基础设施的使用 11
- 预测配置的容量突破点 11

### 容量管理 11

- 观察容量使用率的增长率。11
- 绘制容量使用率趋势图。11
- 了解 `Icing`、`Nagios`、`collect`、`MRTG` 和 `Cacti` 等监控解决方案。11

### 内核管理 12

- 内核 `2.6.x`、`3.x` 和 `4.x` 文档 12
- `/usr/src/linux/` 12
- 内核 `Makefiles` 12
- 内核 `2.6.x`、`3.x` 和 `4.x` 的 `make` targets 12
- 自定义当前内核配置。12
- 构建新内核和相应的内核模块。12
- 安装新内核及任何模块。12
- 确保引导程序能够定位新内核及关联文件。12
- 模块配置文件 12
- 使用 `DKMS` 编译内核模块。12
- 了解 `dracut` 12
- 使用命令行工具获取当前内核和内核模块的信息。12
- 手动加载和卸载内核模块。12
- 确定何时可以卸载模块。12

### 模块管理 12

- 确定模块接受的参数。
- 配置系统通过文件名以外的名称加载模块。12
- `/proc` 文件系统 12
- `/boot/` 和 `/lib/modules/` 的内容 12
- 分析可用硬件信息的工具和实用程序 12
- `udev` 规则 12

### 启动管理 13

- `Systemd` 13
- `SysV` init 13
- Linux 基础规范 (`LSB`) 13
- `BIOS` 和 `UEFI` 13
- `GRUB` 版本 2 和 Legacy 13
- `grub` shell 13
- 引导加载程序的启动以及移交给内核加载的过程 13
- 守护进程/服务的初始化与设置 13
- 了解硬盘或可移动设备上不同的引导加载程序位置。13
- 覆盖标准引导加载程序选项并使用 loader shell。13
- 使用 `systemd` 救援模式和紧急模式。13

### 202.3 备引导加载程序 13

- `SYLINUX`, `ISOLINUX`, `PXELINUX` 13
- 理解适用于 `BIOS` 和 `UEFI` 的 `PXE` 13
- 了解 `systemd-boot` 和 `U-Boot` 13

### 文件系统管理 14

- `fstab` 配置的概念 14
- 处理交换分区和文件的工具与实用程序 14
- 使用 `UUID` 识别和挂载文件系统 14
- 操作 `ext2`、`ext3` 和 `ext4` 的工具和实用程序 14
- 执行基本 `Btrfs` 操作（包括子卷和快照）的工具和实用程序 14
- 操作 `XFS` 的工具和实用程序 14
- 了解 `ZFS` 14
- `autofs` 14
- 理解自动挂载单元 (`automount units`) 14
- `UDF` 和 `ISO9660` 工具与实用程序 14
- 了解其他 CD-ROM 文件系统 (`HFS`) 14
- 了解 CD-ROM 文件系统扩展 (`Joliet`, `Rock Ridge`, `El Torito`) 14
- 数据加密的基本功能知识 (`dm-crypt` / `LUKS`) 14

### 存储管理 15

- 软件 RAID 配置文件和工具 15
- 为包括 `ATAPI` 和 `SATA` 在内的 `IDE` 设备配置 `DMA` 的工具和实用程序 15
- 配置包括 `AHCI` 和 `NVMe` 在内的固态硬盘 (`SSD`) 的工具和实用程序 15
- 操作或分析系统资源（例如中断）的工具和实用程序 15
- 了解 `sdparam` 命令及其用途 15
- 用于 `iSCSI` 的工具和实用程序 15
- 了解 `SAN`，包括相关协议 (`AoE`, `FCoE`) 15
- `LVM` 工具集中的工具 15
- 调整、重命名、创建和删除逻辑卷、卷组和物理卷 15
- 创建和维护快照 15
- 激活卷组 15

### 网络配置 16

- 配置和操作以太网网络接口的工具 16
- 配置无线网络的基础访问 16

### 205.2 高级网络配置 16

- 操作路由表的工具 16
- 配置和操作以太网网络接口的工具 16
- 分析网络状态的工具 16



## 系统基础与网络工具

- 监控 `TCP/IP` 流量的工具
- 访问限制文件的位置和内容
- 配置以太网网络接口的工具
- 管理路由表的工具
- 列出网络状态
- 获取网络配置
- 关于使用的硬件设备信息
- 系统初始化文件及其内容 (`Systemd`, `SysV init`)
- `NetworkManager` 及其的影响
- 使用常用的压缩和存档工具解包源码
- 了解编译的基本知识
- 应用参数到配置脚本
- 了解源码默认存储位置
- 了解包含的目录
- 磁带或其他备份介质的知识
- 执行部分或完整备份
- 通过登录消息与用户通信
- 系统维护问题

## 207.1 基础 DNS 服务器

- `BIND 9.x` 配置文件、术语和工具
- `BIND` 配置中区文件的位置
- 重新加载修改后的配置和区文件
- 了解 `dnsmasq`, `dnssq`, `djbindns` 和作为备用服务器 `PowerDNS`
- `BIND 9` 配置文件、术语和工具
- 从 `DNS` 服务器请求信息的工具
- `BIND` 区文件的布局、内容和文件位置
- 在区文件中添加新主机（包括反向区）的各种方法
- `BIND 9` 配置文件
- 配置 `BIND` 在 `chroot` 环境中运行
- 使用 `forwarders` 语句对 `BIND` 进行拆分配置
- 配置和使用事务签名 (`TSIG`)
- 了解 `DNSSEC` 和基础工具
- 了解 `DANE` 和相关记录

## Apache 与 SSL 配置

- `Apache 2.4` 配置文件、术语和内容
- `Apache` 日志文件配置和内容
- 访问限制方法和文件
- `mod_perl` 和 `PHP` 配置
- 客户端用户身份验证文件和工具
- 最大请求、最小及最大服务器和客户端配置
- `Apache 2.4` 虚拟主机实现（带有或不专用 `IP` 地址）
- 使用 `Apache` 配置文件中的重定向语句自定义文件访问
- `SSL` 配置文件、工具和实用程序
- 为商业 `CA` 生成服务器私钥和 `CSR`
- 生成自签名证书
- 安装密钥和证书（包括中间 `CA`）
- 使用 `SNI` 配置虚拟主机
- 了解虚拟主机和使用 `SSL` 的问题
- `SSL` 使用中的安全问题，禁用不安全的协议和加密算法

## 208.3 实现 Squid 作为缓存代理

- `Squid 3.x` 配置文件、术语和工具
- 访问限制方法
- 客户端用户身份验证方法
- `Squid` 配置文件 `ACL` 的布局和内容

## 208.4 实现 Nginx 作为 Web 服务器和反向代理

- `Nginx`
- 反向代理
- 基础 `Web` 服务器

## Samba 4 配置

- `Samba 4` 文档
- `Samba 4` 配置文件
- `Samba 4` 工具、工具和守护进程
- 在 `Linux` 上挂载 `CIFS` 共享
- 将 `Windows` 用户映射到 `Linux` 用户
- 用户级、共享级和 `AD` 安全

## NFS 配置

- `NFS` 版本 3 配置文件
- `NFS` 工具和工具
- 对特定主机或子网的访问限制
- 服务器和客户端上的挂载选项
- `TCP Wrappers`
- `NFSv4` 概述

## DHCP 与 LDAP

- `DHCP` 配置文件、术语和工具
- 子网和动态分配范围设置
- `DHCP6` 和 `IPv6` 路由器公告
- `PAM` 配置文件、术语和工具
- `passwd` 和 `shadow`
- 使用 `sssd` 进行 `LDAP` 认证
- 用于数据管理和查询的 `LDAP` 工具
- 修改用户密码
- 查询 `LDAP` 目录
- `OpenLDAP`
- 基于目录的配置
- 访问控制
- 区分名 (Distinguished Names)
- 模式 (Schemas) 和网页
- 目录
- 对象 ID、属性和类

## 简介与邮件服务

### 邮件服务

- `postfix` 配置文件
- `postfix` `TLS` 配置
- `SMTP` 协议基础知识
- `sendmail` 和 `exim` 概述
- `Sieve` 功能、语法和操作符
- 使用 `Sieve` 根据发件者、收件者(s)、头部和大小对邮件进行过滤
- `procmail` 概述
- `Dovecot` `IMAP` 和 `POP3` 配置和管理
- `Dovecot` 基础 `TLS` 配置
- `Courier` 概述

### 网络安全与防火墙

- `iptables` 和 `ip6tables` 配置文件、工具和工具
- 管理路由表的命令和工具
- 私有地址范围 (`IPv4`) 以及链路本地地址 (`IPv6`)
- 端口重定向和 `IP` 转发
- 根据源或目的协议、端口和地址允许或拦截 `IP` 包
- 保存并重载过滤配置

### FTP 与 SSH

- `Pure-FTPD` 和 `vsftpd` 配置文件、工具和工具
- `ProFTPD` 概述
- 理解被动与主动 `FTP`
- `OpenSSH` 配置文件、工具和工具
- 超级用户和普通用户的登录限制
- 管理和使用服务器和客户端密钥免登录
- 使用多个主机防止配置更改后连接丢失
- 在服务器上扫描和测试端口的工具和工具
- 以日志或其他来源报告安全告警的位置
- 实现入侵检测系统 (`IDS`) 的工具和工具
- `OpenVAS` 和 `Snort` 概述

## 硬件管理

- `CompTIA Linux+/LPIC-1`
- 启用和禁用集成外设
- 配置带有或带有键盘等外部外设的系统
- 区分不同类型的存储设备
- 确定设备的硬件资源
- 列出硬件信息的工具和工具（例如 `lsusb`, `lspci` 等）
- 操作 `USB` 设备的工具和工具
- 对 `sysfs`, `udev`, `hal`, `dbus` 的概念性理解
- 以下是使用的文件、术语和工具的部分列表：
    - `/sys`
    - `/proc`
    - `/dev`
    - `modprobe`
    - `lsmod`
    - `lspci`
- 在启动时为内核提供常用命令

## 启动与初始化

- 从 `BIOS` 到完成的启动序列
- 理解 `SysVinit` 和 `systemd`
- 对 `Upstart` 的了解
- 在日志文件中检查启动事件
- 以下是使用的文件、术语和工具的部分列表：
    - `dmesg`
    - `BIOS`
    - `bootloader`
    - `kernel`
    - `initramfs`
    - `init`
    - `SysVinit`
    - `system`
- 设置默认运行级别或启动目标
- 在运行级别/启动目标之间切换（包括单用户模式）
- 从命令行关机和重启
- 在切换运行级别/启动目标或主要系统事件之前提醒用户
- 正常终止进程
- 以下是使用的文件、术语和工具的部分列表：
    - `/etc/inittab`
    - `shutdown`
    - `init`
    - `/etc/init.d`
    - `telinit`
    - `system`
    - `systemctl`
    - `/etc/systemd/`
    - `/usr/lib/systemd/`
    - `wall`

## 练习题

A. `/dev/hdx`  
B. `/dev/sataX`  
C. `/dev/sdX`  
D. `/disk/sataX`  

A. `view /proc/irq`  
B. `cat /proc/interrupts`  
C. `cat /dev/irq`  

A. `/dev/hd0`  
B. `/dev/flo0`  
C. `/dev/fd0`  
D. `/dev/sda`  

A. `/udev/`  
B. `/devices/`  
C. `/udev/config`  
D. `/udev`  

A. `modprobe`  
B. `lsmod`  
C. `insmod`  
D. `rmmod`  

A. `usb-list`  
B. `lsusb`  
C. `ls-usb`  
D. `--usb`  

A. `/etc/usb`  
B. `/etc/usb-dev`  
C. `/dev/usb`  
D. `/etc/hotplug/usb`  

8. `GRUB` 配置中提供的启动选项会将系统引导单用户模式？  
A. `single-user`  
B. `su`  
C. `single`  
D. `root`  

A. `Shift`  
B. `E`  
C. `V`  
D. `H`  

10. 使用哪个命令查看内核环缓冲区以诊断启动过程？  
A. `lsboot`  
B. `boot-log`  
C. `krblogger`  
D. `dmesg`  

A. `Runlevel 5`  
B. `Runlevel SU`  
C. `Runlevel 1`  
D. `Runlevel 6`  

A. `/etc/init-d`  
B. `/etc/init`  
C. `/etc/sysV`  
D. `/etc/init.d`  

A. `init 6`  
B. `shutdown -h -t now`  
C. `init 1`  
D. `refresh-system`  

A. `init-refresh`  
B. `init 6`  
C. `telinit`  
D. `reload-inittab`  

A. `show-level`  
B. `init --level`  
C. `sudo init`  
D. `runlevel`  

A. `/etc/system.conf.d`  
B. `/lib/system.conf.d`  
C. `/lib/systemd/system`  
D. `/etc/sysconfd`  

```
lrwxr-xr-x. 1 root 35 Jul 8 2014 .fetchmailrc -> .configs/fetchmail/.fetchmailrc
```

A. 这是一个名为 `.fetchmailrc` 的文件，使用符号链接链接。  
B. 这是一个名为 `.configs/fetchmail/.fetchmailrc` 的文件，所有者为 `lrwxr-xr-x`。  
C. 这是一个名为 `.fetchmailrc` 的目录，所有者为 `Jul`。  
D. 这是一个本地目录 `.configs/fetchmail/.fetchmailrc`。  

A. `systemd list-units`  
B. `systemctl list-units`  
C. `systemd unit-list`  
D. `systemctl show-units`  

A. `-numdev`  
B. `-n`  
C. `-nn`  
D. `-devnum`  

A. `insmod`  
B. `modlist`  
C. `ls --modules`  
D. `lsmod`  

A. `--show-options`  
B. `--list-deps`  
C. `--show-depends`  
D. `--list-all`  

A. `cat`  
B. `wall`  
C. `tee`  
D. `ssh`  

A. 拔掉磁盘。  
B. 检查系统 `BIOS`。  
C. 重启 `Web` 服务器服务。  
D. 运行 `disk-detect` 命令。  

A. `/etc/usbdevices`  
B. `/var/usb`  
C. `/lib/sys/usb`  
D. `/proc/bus/usb`  

A. `rootpartition={hd0,2}`  
B. `root={dev/sda2}`  
C. `root={hd0,3}`  
D. `rootpartition=/dev/sda2`  

A. 按 `ESC` 编辑，按 `Return` 启动  
B. 按 `V` 编辑，按 `Return` 启动  
C. 按 `E` 编辑，按 `B` 启动  
D. 按 `V` 编辑，按 `B` 启动  

A. `ls`  
B. `showPart`  
C. `partitionlist`  
D. `ps`  

A. `/var/log/bootmessages`  
B. `/var/log/mail.info`  
C. `/var/adm/log/boot.info`  
D. `/var/log/dmesg`  

A. `systemctl --ls`  
B. `telinit`  
C. `systemctl status`  
D. `sysctl -a`  

30. 在受 `systemd` 控制的系统上，哪个命令会将系统置于单用户模式？  
A. `systemctl one`  
B. `systemctl isolate resue.`  
C. `systemctl single-user`  
D. `systemctl runlevel one`  

31. 在由 `Upstart` 控制的系统中，哪个命令将重新加载配置文件？  
A. `initctl reload`  
B. `systemd reload`  
C. `upstart --reload`  
D. `ups -reload`  

32. 在 `SysV` 系统上工作时，`chkconfig` 哪个选项显示所有服务及其运行级别？  
A. `--reload`  
B. `--list`  
C. `--all`  
D. `--ls`  

33. 连接到 `USB` 的驱动器被视为哪种类型的设备？  
A. 介质 (`Medium`)  
B. 冷插拔 (`Coldplug`)  
C. 热插拔 (`Hotplug`)  
D. 侧插拔 (`Sideplug`)  

34. 在启动过程中，内核接管初始化过程并初始化设备后，下一步是什么？  
A. 系统 `BIOS` 初始化设备。  
B. 系统被置于多用户模式。  
C. 引导程序初始化内核。  
D. 挂载根分区。  

35. 使用一个旧式 `PATA` 磁盘启动系统。你最近为电脑添加了一个内部 `DVD` 驱器，系统将不再启动。最可能的原因是什么？  
A. `BIOS` 将 `DVD` 驱器识别为第一块磁盘，因此系统无法找到 `Linux` 分区。  
B. 在安装 `DVD` 驱器时，硬盘损坏了。  
C. `BIOS` 中未启用热插拔选项。  
D. 电脑未检测到 `DVD` 驱器，在安装之前需要先在 `BIOS` 和 `Linux` 中启用它。  

36. 系统使用临时闪存 `USB` 磁盘将数据挂载在 `/dev/sda1`。你需要移除该磁盘。以下哪个命令将允许磁盘安全地从系统中移除？  
A. `usstop /dev/sda`  
B. `umount /dev/sda1`  
C. `ummount /dev/sda1`  
D. `dev-eject /dev/sda`  

37. `EFI` 将挂载在哪个分区中？  
A. `/etc`  
B. `/root`  
C. `/sys`  
D. `/boot`  

## 第 1 章 系统架构 (领域 101)

38. 你已向系统连接了一个 `USB` 磁盘并需要查找它的连接情况。以下哪种方法是最好的？  
A. 查看 `/var/log` 的内容  
B. 运行 `dmesg` 并查找系统信息  
C. 重启系统  

39. 以下哪个命令将立即关闭系统？  
A. `shutdown -c`  
B. `halt`  
C. `systemd stop`  
D. `stop`  

40. `systemd` 文件中的哪个选项指示要执行的程序？  
A. `StartProgram`  
B. `ShortCut`  
C. `ExecStart`  
D. `Startup`  

41. `systemd` 上的哪个命令显示默认目标（`target`）？  
A. `systemctl defaults`  
B. `update-rc.d`  
C. `systemctl runlevel`  
D. `systemctl get-default`  

42. `systemctl` 命令的哪个选项可以更改服务以便在启动时运行？  
A. `enable`  
B. `starton`  
C. `loadboot`  
D. `start`  

43. 下哪项最符合 `/proc` 文件系统？  
- `/proc` 包含待处理的文件。  
- `/proc` 包含进程的配置文件。  
- `/proc` 包含当前运行的信息，包括内核。  
- `/proc` 包含邮件和网络等变量数据。  

44. 哪个命令将以树状格式检索计算机上的 `USB` 连接信息？  
- `lsusb -tree`  
- `lsusb --tree`  
- `lsusb -t`  
- `usblist --tree`  

45. 每个总线支持多少个 `SCSI` 设备？  
- 7 到 15  
- 2 到 4  
- 12  
- 4  

46. 即使设备已加载且运行正常，设备驱动程序未出现在 `lsmod` 输出中的原因可能是？  
- 使用 `systemd` 意味着大多数设备不需要驱动。  
- 使用 `initramfs` 意味着默认启用。  
- 系统不需要设备驱动程序。  
- 设备支持直接编译到内核中。  

47. `rmod` 命令的哪个选项将等待模块不再被使用时再卸载？  
- `-test`  
- `-f`  
- `-w`  
- `-unload`  

## 第 2 章 Linux 安装与包管理 (领域 102)

本章涵盖了以下 `CompTIA LINUX+/LPIC-1` 考试目标：

### 102.1 设计磁盘布局

- 将文件系统和交换空间分配到单独分区或磁盘
- 根据系统的预定用途进行定制设计
- 确保 `/boot` 分区符合启动的硬件架构要求
- `LVM` 基本功能的知识
- 以下是所用文件、术语和工具的部分列表：
    - `/(root)` 文件系统
    - `/var` 文件系统
    - `/home` 文件系统
    - `/boot` 文件系统



*   交换空间
*   挂载点
*   分区

### 102.2 安装引导管理器

*   提供备启动位置和备份启动选项
*   安装并配置如 `GRUB Legacy` 等类的引导程序
*   为 `GRUB2` 执行基本配置更改
*   与引导程序进行交互
*   以下是使用的文件、术语和工具的部分列表
    *   `menu.list`, `grub.cfg` 和 `grub.conf`
    *   `grub-install`
    *   `grub-mkconfig`
    *   `MBR`

### 102.3 管理共享库

*   识别共享库
*   识别系统库的典型位置
*   加载共享库
*   以下是使用的文件、术语和工具的部分列表
    *   `ld`
    *   `ldconfig`
    *   `/etc/ld.so.conf`
    *   `LD_LIBRARY_PATH`

### 102.4 使用 Debian 软件包管理

*   安装、升级和卸载 Debian 二进制包
*   查找包含特定文件或库的软件包（无论是否已安装）
*   获取包信息，如版本、内容、依赖关系、包完整性和安装状态（包是否安装）
*   以下是使用的文件、术语和工具的部分列表：
    *   `/etc/apt/sources.list`
    *   `dpkg`
    *   `dpkg-reconfigure`
    *   `apt-get`
    *   `apt-cache`
    *   `aptitude`

![](img/84990579543ce21a46ac6dc507fcde32_53_0.png)

### 102.5 使用 RPM 和 YUM 软件包管理

*   使用 `RPM` 和 `YUM` 安装、重装、升级和删除包
*   获取 `RPM` 包的信息，如版本、状态、依赖关系、完整性和签名
*   确定包提供了哪些文件，并查找特定文件来自哪个包
*   以下是使用的文件、术语和工具的部分列表：
    *   `rpm`
    *   `rpm2cpio`
    *   `/etc/yum.conf`
    *   `/etc/yum.repos.d/`
    *   `yum`
    *   `yumdownloader`

![](img/84990579543ce21a46ac6dc507fcde32_54_0.png)

#### 练习题

1.  在为邮件服务器 `Postfix` 分区磁盘时，哪一个分区/挂载目录应该是最大的，以便允许邮件存储？
    *   A. `/etc`
    *   B. `/usr/bin`
    *   C. `/mail`
    *   D. `/var`

2.  `GRUB Legacy` 中的哪个选项用于指示根分区包含非 Linux 内核？
    *   A. `initrd`
    *   B. `non-linux`
    *   C. `rootnofify`
    *   D. `root-win`

3.  分区挂载命令中的哪个选项会导致分区以防止执行程序的方式进行挂载？
    *   A. `execless`
    *   B. `stoprun`
    *   C. `noexec`
    *   D. `durun`

4.  哪个命令会输出新的 `GRUB 2` 配置文件并将输出发送到启动的正确位置？
    *   A. `update-grub > /boot/grub/grub.cfg`
    *   B. `update-grub boot > /boot/grub/grub.cfg`
    *   C. `grub-rc.d`
    *   D. `grub-boot`

5.  `MBR` 分区系统中可用的主分区数量是多少？
    *   A. 两个
    *   B. 四
    *   C. 一个
    *   D. 五

6.  哪个命令用于更新系统上共享库的链接和缓存？
    *   A. `ldcache`
    *   B. `cache-update`
    *   C. `link-update`
    *   D. `ldconfig`

## 第 2 章 ■ 安装与软件包管理 (领域 102)

7.  使用哪个命令和选项将 Debian 系统更新到最新软件？
    *   A. `apt-update`
    *   B. `apt-get upgrade`
    *   C. `dpkg -U`
    *   D. `apt-cache clean`

8.  `yum` 命令提供的哪个选项会安装给定的包？
    *   A. `update`
    *   B. `configure`
    *   C. `install`
    *   D. `get`

9.  `root` 用户的家目录位置在哪里？
    *   A. `/home/root`
    *   B. `/home/su`
    *   C. `/root`
    *   D. `/`

10. 使用 `rpm2pio` 时，默认输出到哪个位置？
    *   A. `STDOUT`
    *   B. `cpio.out` 文件
    *   C. `a.out` 文件
    *   D. `/tmp/pio.out`

11. 在处理磁盘分区时，看到 `swap`。这是哪种分区？
    *   A. `Linux`
    *   B. `swap`
    *   C. `NTFS`
    *   D. `FAT32`

12. 哪个分区或目录结构持有大部分 Linux 程序？
    *   A. `/etc`
    *   B. `/usr`
    *   C. `/home`
    *   D. `/var`

13. 你的 `GRUB Legacy` 配置列出了 Linux，然后列出了另一个系统。以下哪个选项将默认启动 Linux？
    *   A. `default=linux`
    *   B. `default=0`
    *   C. `default=1`
    *   D. `default=other`

14. 使用 `GRUB 2` 设置超时等项时应该编辑哪个文件？
    *   A. `/etc/default/grub`
    *   B. `/etc/grub/boot`
    *   C. `/etc/grub.d`
    *   D. `/grub/boot`

15. `yum` 选项显示包的依赖关系？
    *   A. `list`
    *   B. `deplist`
    *   C. `dependencies`
    *   D. `listdeps`

16. `rpm` 命令的哪个选项会显示安装过程的详细输出？
    *   A. `-ivh`
    *   B. `-vh`
    *   C. `--av`
    *   D. `--ins-verbose`

17. 以下哪个命令使用 `Bash Shell` 将 `/usr/local/lib` 添加到 `LD_LIBRARY_PATH`？
    *   A. `export LD_LIBRARY_PATH=/usr/local/lib`
    *   B. `export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/lib`
    *   C. `LD_LIBRARY_PATH=/usr/local/lib`
    *   D. `set LD_LIBRARY_PATH=/lib`

18. 哪个命令可以在不安装的情况下下载 `RPM` 包？
    *   A. `yum`
    *   B. `yumdownloadonly`
    *   C. `yumdown`
    *   D. `yumdownloader`

19. 哪个命令会在 Debian 系统上搜索名为 `zsh` 的包？
    *   A. `apt-cache search zsh`
    *   B. `apt-get search zsh`
    *   C. `apt-cache locate zsh`
    *   D. `apt search zsh`

20. `/etc/default/grub` 中的哪个选项用于配置引导操作系统？
    *   A. `GRUB_OS`
    *   B. `GRUB_ON`
    *   C. `GRUB_DEFAULT`
    *   D. `DEFAULT_OS`

21. 在 `GRUB` 配置文件中找到 `ro` 选项表示什么？
    *   A. 最初将根分区挂载为只读
    *   B. 将内核挂载为只读
    *   C. 单次启动 `init` 程序
    *   D. 以只读模式挂载分区

22. 在哪个目录下会找到 `YUM` 使用的仓库？
    *   A. `/etc/yum.conf`
    *   B. `/etc/repos`
    *   C. `/etc/yum.conf.d`
    *   D. `/etc/yum.repos.d`

23. 哪个 `rpm` 选项可以验证自安装以来文件是否被更改？
    *   A. `-v`
    *   B. `-V`
    *   C. `--verbose`
    *   D. `--filesum`

24. `grub-mkconfig` 命令的哪个选项将输出发送到文件而不是 `STDOUT`？
    *   A. `-stdout`
    *   B. `--fileout`
    *   C. `-o`
    *   D. `-f`

25. 文件系统中存在 `menu.lst` 通常表示哪种情况？
    *   A. 系统上正在使用 `GRUB Legacy`。
    *   B. 输出到 `menu.lst` 时发生错误。
    *   D. 救援启动选项已更改。

26. 哪个命令用于确定给定命令依赖的库？
    *   A. `ldconfig`
    *   B. `librarylist`
    *   C. `listdeps`
    *   D. `ldd`

27. 关于 Linux `swap` 空间，以下哪个正确？
    *   A. `Swap` 用于存储临时数据库表。
    *   B. 当 `RAM` 不足时，`Swap` 作为额外内存。
    *   C. 邮件服务器为了安全使用 `Swap`。
    *   D. `Swap` 用于清除网络数据。

28. 以下哪项通常用于存储库？
    *   A. `/lib`
    *   B. `/etc/lib`
    *   C. `/usr/lib`
    *   D. `/usr/local/lib`

29. 以下哪个命令更新 Debian 系统的软件包缓存？
    *   A. `apt-get cache-update`
    *   B. `apt-cache update`
    *   C. `apt-get update`
    *   D. `apt-get upgrade`

30. Debian 系统上当前软件包仓库的详情存储在哪个文件中？
    *   A. `/etc/apt.list`
    *   B. `/etc/sources.list`
    *   C. `/etc/apt/sources.list`
    *   D. `/etc/apt.d/sources.list`

31. 在以下选项中，什么大小对于 Linux 系统的 `/boot` 分区最合适？
    *   A. 100 MB 到 500 MB 之间
    *   B. 1 GB 到 10 GB 之间
    *   C. `/boot` 不应该分区。
    *   D. 小于 5 MB

32. 以下哪个命令初始化用于 `LVM` 的物理分区？
    *   A. `lvcreate`
    *   B. `pvcreate`
    *   C. `fcreate`
    *   D. `lvinit`

33. 以下哪个命令将 `GRUB` 安装到第二个 `SATA` 磁盘的 `MBR` 中？
    *   A. `grub-install /dev/db2`
    *   B. `grub-install /dev/sda2`
    *   C. `grub-config /dev/sda`
    *   D. `grub-install /dev/sdb`

34. 对安装 Debian 包时做出的更改应该使用哪个命令？
    *   A. `dpkg-reconfigure`
    *   B. `dpkg -r`
    *   C. `dpkg --reconf`
    *   D. `apt-get reinstall`

35. 哪个命令用于 `LVM` 创建逻辑卷？
    *   A. `pvcreate`
    *   B. `lvcreate`
    *   C. `vgcreate`
    *   D. `volcreate`

36. 创建 `LVM` 逻辑卷的逻辑顺序是？
    *   A. 物理卷创建、卷组创建、逻辑卷创建
    *   B. 物理卷创建、逻辑卷创建、卷组创建
    *   C. 逻辑卷创建、物理卷创建、卷组创建
    *   D. `LVM` 创建、格式化、分区

37. Debian 软件包管理工具中的哪一个提供了管理的终端界面？
    *   A. `apt-get`
    *   B. `dpkg`
    *   C. `apt-cache`
    *   D. `aptitude`

38. `yum` 的哪个选项执行软件包缓存的搜索？
    *   A. `seek`
    *   B. `query --search`
    *   D. `search`

39. 哪个 `rpm` 命令选项可以用于显示内核版本？
    *   A. `rpm kernel`
    *   B. `rpm -q kernel`
    *   C. `rpm search kernel`
    *   D. `rpm --list kernel`

40. 假设你的 `GRUB` 配置中有一个名为“Debian”的菜单项，`/etc/default/grub` 中的哪个选项将将其设置为默认启动的操作系统？
    *   A. `GRUB_OS`
    *   B. `GRUB_OS_DEF`
    *   C. `GRUB_DEFAULT`
    *   D. `GRUB_CONF`

41. `/etc/yum.conf` 中的哪个选项用于确保在系统更新时不更新内核？
    *   A. `exclude=kernel*`
    *   B. `exclude-kernel`
    *   C. `updatekernel=false`
    *   D. `include-except=kernel`

42. Linux 系统的非交换分区应该创建什么种类型的分区？
    *   A. `82`
    *   B. `83`
    *   C. `84`
    *   D. `L`

43. 在修改 `/etc/default/grub` 文件后，应该运行哪个命令？
    *   A. `grub`
    *   B. `grub-mkconfig`
    *   C. `grub-inst`
    *   D. `reboot`

44. 哪个命令在 Debian 系统上搜索并提供给定包的信息，包括该包当前是否已安装？
    *   A. `dpkg -i`
    *   B. `dpkg -s`
    *   C. `apt-cache`
    *   D. `apt-info`

45. 哪个命令用于搜索用于 `LVM` 的物理卷？
    *   A. `svmcreate`
    *   B. `pvcreate`
    *   C. `lvdiskscan`
    *   D. `lvscan`

46. 添加到 `yumdownloader` 的哪个选项也会下载依赖项？
    *   A. `--deps`
    *   B. `--resolve`
    *   C. `--resdeps`
    *   D. `-d`

47. 下列哪个命令可以安装之前下载的 Debian 包？
    *   A. `dpkg -i <package name>`
    *   B. `apt-install <package name>`
    *   C. `apt-slash <package name>`
    *   D. `dpkg -U <package name>`

48. `GRUB` 配置文件报告硬盘为 `hd(0,0)`。这对应于以下哪个磁盘和分区？
    *   A. `/dev/hdb2`
    *   B. `/dev/hda0`
    *   C. `/dev/disk1`
    *   D. `/dev/sda1`

# GNU 和 Unix 命令

(领域 103)

本章涵盖了以下 CompTIA LINUX+/LPIC-1 考试目标：

## 103.1 在命令行上工作

*   使用单个 shell 命令和单行命令序列在命令行上执行基本任务
*   使用和修改 shell 环境，包括定义、引用和导出环境变量
*   使用和编辑命令历史
*   在定义路径内外调用命令
*   以下是所用文件、术语和工具的部分列表：
    *   `bash`
    *   `echo`
    *   `env`
    *   `export`
    *   `pwd`
    *   `set`
    *   `unset`
    *   `man`
    *   `uname`
    *   `history`
    *   `.bash_history`

### 103.2 使用过滤器处理文本流

*   将文本文件和输出流通过文本实用程序过滤器，使用 `GNU textutils` 包中的标准 UNIX 命令修改输出
*   以下是所用文件、术语和工具的部分列表：
    *   `cat`
    *   `cut`
    *   `expand`
    *   `fmt`
    *   `head`
    *   `od`
    *   `join`
    *   `nl`
    *   `paste`
    *   `pr`
    *   `sed`
    *   `sort`
    *   `split`
    *   `tail`
    *   `tr`
    *   `unexpand`
    *   `wc`

### 103.3 执行基本文件管理。

*   分别复制、移动和删除文件和目录
*   递归复制多个文件和目录
*   递归删除文件和目录
*   在命令中使用简单和高级通配配符规范
*   使用 `find` 根据类型、大小或时间定位并处理文件
*   `tar`, `cpio` 和 `dd` 的用法
*   以下是所用文件、术语和工具的部分列表：
    *   `cp`
    *   `find`
    *   `mkdir`
    *   `mv`
    *   `ls`
    *   `rm`
    *   `rmdir`
    *   `touch`
    *   `tar`
    *   `cpio`
    *   `dd`
    *   `file`
    *   `gzip`
    *   `gunzip`
    *   `bzip2`
    *   `xz`
    *   `file globbing`

![](img/84990579543ce21a46ac6dc507fcde32_65_0.png)

### 103.4 使用流、管道和重定向

*   重定向标准输入、标准输出和标准错误
*   将一个命令的输出通过管道到另一个命令的输入
*   将一个命令的输出作为另一个命令的参数
*   将输出同时发送到 `stdout` 和文件
*   以下是所用文件、术语和工具的部分列表：
    *   `tee`
    *   `xargs`

![](img/84990579543ce21a46ac6dc507fcde32_66_0.png)

### 103.5 创建、监控和杀死进程

*   在前台和后台运行作业
*   信号程序在注销后继续
*   监控活动进程
*   选择并排序进程以便显示
*   向进程发送信号
*   以下是所用文件、术语和工具的部分列表：
    *   `bg`
    *   `fg`
    *   `jobs`
    *   `kill`
    *   `nohup`
    *   `ps`
    *   `top`
    *   `free`
    *   `uptime`
    *   `pgrep`
    *   `killall`
    *   `screen`

![](img/84990579543ce21a46ac6dc507fcde32_67_0.png)

### 103.6 修改进程执行

*   了解创建的任务的默认优先级
*   以比默认更高或更低的优先级运行程序
*   修改正在运行进程的优先级
*   以下是所用文件、术语和工具的部分列表：
    *   `nice`
    *   `ps`
    *   `renice`
    *   `top`

### 103.7 使用正则表达式搜索文本文件

*   创建包含几个元素的简单正则表达式
*   使用正则表达式工具对文件系统或内容进行搜索
*   以下是所用文件、术语和工具的列表：
    *   `grep`
    *   `egrep`
    *   `fgrep`
    *   `regex`

### 103.8 使用 vi 执行基本文件编辑

*   使用 `vi` 导航文档
*   使用基础 `vi` 模式
*   插入、编辑、删除、复制文本
*   以下是所用文件、术语和工具的列表：
    *   `vi`
    *   `/`
    *   `h`, `j`, `k`, `l`
    *   `i`, `o`, `a`
    *   `c`, `d`, `p`, `y`
    *   `z`, `w`, `q`

![](img/84990579543ce21a46acdc507fcde32_68_0.png)

第30 部分 CompTIA Linux+/LPIC-1

#### 练习题

1.  使用什么 shell 命令可以查看环境变量设置？
    *   A. `environment`
    *   B. `env`
    *   C. `listenv`
    *   D. `set`

2.  假设你在使用 shell 并想要防止覆盖文件。哪个命令和选项可以实现这种行为？
    *   A. `set -f`
    *   B. `overwrite=`
    *   C. `set -n`
    *   D. `overwrite`

3.  哪个命令用于访问文档？
    *   A. `doc`
    *   B. `heredoc`
    *   C. `man`
    *   D. `manual`

4.  下列哪个命令将打印关于内核和架构的其他信息？
    *   A. `info --`
    *   B. `man`
    *   C. `sys`
    *   D. `-a`

5.  使用 `sed` 进行替换操作时，包含哪个选项可以适用于整行而非仅第一个实例？
    *   A. `g`
    *   B. `a`
    *   C. `r`
    *   D. `y`

6.  `wc` 命令的哪个选项打印输入行数？
    *   A. `-f`



- B. `-a`

- C. `-l`

- D. `-o`

# 第3章 GNU 和 Unix 命令 (领域 103)

7. `head` 和 `tail` 命令默认打印的行数分别是？

- A. `head` 为 10，`tail` 为 5

- B. `head` 为 5，`tail` 为 10

- C. 均为 10

- D. 均为 30

8. 你正尝试使用 `rm` 删除目录，但内部仍有文件和其他目录。假设你确定要删除该目录及其所有内容，需要什么命令和参数？

- A. `rm -f`

- B. `rm -rf`

- C. `rm -a`

- D. `rm -m`

9. 哪个命令将查找当前目录下以 2014 开头的目录？

- A. `find ./ -name "2014"`

- B. `find . -type d -name "2014"`

- C. `find / -type d -name "2014"`

- D. `find ./ -type d -name "2014*"`

10. 下列哪个命令可以从 `/etc/passwd` 获取排序后的用户名列表？

- A. `cat /etc/passwd | awk -F':' '{print $1}' | sort`

- B. `sort /etc/passwd | cut`

- C. `echo /etc/passwd`

- D. `cat /etc/passwd | awk '{print $1}' | sort`

11. `ls` 的哪些选项可以产生包含隐藏（点）文件的输出，并按最新文件在输出末尾进行排序？

- A. `-la`

- B. `-lat`

- C. `-ltr`

- D. `-altr`

12. 对已存在的文件执行 `touch` 命令，结果是什么？

- A. 文件的访问时间将在执行 `touch` 命令时更改为当前时间。

- B. 文件将被覆盖。

- C. 没有变化。

- D. 文件将被追加。

13. `mv` 和 `cp` 命令的哪个选项项会导致命令在覆盖已存在的文件之前进行提示？

- A. `-f`

- B. `-Z`

- C. `-r`

- D. `-i`

14. 下列哪个命令会将 `/etc/passwd` 的内容发送到标准输出（`stdout`）以及一个名为 `passwordfile` 的文件中？

- A. `cat /etc/passwd > passwordfile`

- B. `var /etc/passwd | tee passwordfile`

- C. `cat /etc/passwd | tee passwordfile`

- D. `echo /etc/passwd | stdout > passwordfile`

15. 服务器当前的层次结构包含一个名为 `/usr/local` 的目录。你需要在下方创建一个名为 `/usr/local/test/october` 的额外目录。哪个命令可以完成此任务？

- A. `mkdir -p /usr/local/test/october`

- B. `mkdir /usr/local/test/october`

- C. `mkdir -r /usr/local/test/october`

- D. `mkdir -f /usr/local/test/october`

16. `cp` 命令的哪个选项会以递归方式拷贝目录？

- A. `-v`

- B. `-R`

- C. `-Z`

- D. `-i`

17. 你收到了一个没有文件扩展名的文件。你可以运行哪个命令来帮助确定它可能是什么类型的文件？

- A. `grep`

- B. `telnet`

- C. `file`

- D. `export`

18. 哪个命令将创建 `/dev/sda` 磁盘分区的镜像并将该镜像放入名为 `output.img` 的文件中？

- A. `dd if=/sda of=/dev/sda`

- B. `dd if=output.img of=/dev/sda`

- C. `dd if=/dev/sda of=output.img`

- D. `echo /dev/sda > output.img`

# 第 3 章 • GNU 和 Unix 命令 (领域 103)

19. `cut` 命令默认使用的分分隔符是什么？

- A. 冒号 (Colon)

- B. 制表符 (Tab)

- C. 空格 (Space)

- D. 逗号 (Comma)

20. 下列哪项将解压并提取经过 `tar` 压缩和 `gzip` 压缩的文件内容？

- A. `tar -zxf <file.tgz>`

- B. `tar -xf <file.tgz>`

- C. `tar -vz <file.tgz>`

- D. `tar -fd <file.tgz>`

21. 在命令通过 `&` 放入后台运行后，使用哪个命令将其带前台处理？

- A. `bg`

- B. `fore`

- C. `4g`

- D. `fg`

22. 你需要编写一个脚本，收集系统中运行的所有 `Apache` 实例的进程 ID（PIDs）。下列哪个命令可以完成此任务？

- A. `ps auxw | grep apache`

- B. `pgrep apache`

- C. `processlist apache`

- D. `ls -p apache`

23. 下列哪个命令行会持续地监控一个名为 `nagios` 的单进程？

- A. `top -n 1`

- B. `ps -p 23`

- C. `top -nagios`

- D. `top -p pidof nagios`

24. 用户报告服务器上的各种程序正在崩溃。在检查日志时，你看到某些进程报告了内存溢出（out-of-memory）状况。你可以使用哪个命令查看整体内存使用情况，包括可用交换空间（`swap space`）？

- A. `tree`

- B. `pgrep`

- C. `uptime`

- D. `free`

25. 你正在使用 `vi` 编辑器修改文件并需要退出。你收到一条提示：“No write since last change.”假设你想保存工作，下列哪个命令将保存工作并退出？

- A. `:wq`

- B. `:ql`

- C. `dd`

- D. `x`

26. 使用哪个选项来更改 `head` 和 `tail` 命令的输出行数？

- A. `-l`

- B. `-f`

- C. `-g`

- D. `-n`

27. 哪个命令可以用于确定当前的负载平均值，以及自系统上次启动以来运行时间的信息？

- A. `uptime`

- B. `sysinfo`

- C. `bash`

- D. `-u`

28. 你需要启动一个需要终端和前台处理的长时间运行进程。但是，由于安全限制，你无法保持终端窗口打开。哪个命令将让你启动该进程并在稍后返回会话？

- A. `fg`

- B. `bg`

- C. `kill`

- D. `screen`

29. 你已尝试使用服务命令停止进程，并使用了 `kill` 命令。可以使用 `kill` 命令向进程发送什么种信号来强制进程结束？

- A. `-15`

- B. `-f`

- C. `-9`

- D. `-stop`

30. 在 `Bash shell` 中工作时，你需要重定向标准输出（`stdout`）和标准错误（`stderr`）。下列哪个命令会重定向标准输出和标准错误？

- A. `1>2`

- B. `>2`

- C. `2>&1`

- D. `>>`

31. 运行哪个命令可以确定当前用户创建进程的默认优先级？

- A. `prio`

- B. `nice`

- C. `renice`

- D. `defpriority`

32. 下列哪个 `egrep` 命令将检查 `/etc/passwd` 以寻找使用 `/bin/bash` 或 `/bin/zsh` 作为其 `shell` 的用户？

- A. `grep /etc/passwd`

- B. `egrep '*/sh$' /etc/passwd`

- C. `grep '*/*.sh$' /etc/passwd`

- D. `egrep '*/\.sh$' /etc/passwd`

33. `man` 命令的哪个选项可以访问不同级别的文档，例如，系统调用文档？

- A. `man 2 <argument>`

- B. `prog <argument>`

- C. `man --sys <argument>`

- D. `man --list`

34. 使用 `vi` 进行编辑时，哪个命令会切换到插入模式并在光标位置下方打开一个新行？

- A. `f`

- B. `a`

- C. `o`

- D. `i`

35. 可以发送哪个 `kill` 信号来重启进程？

- A. `-HUP`

- B. `-RESTART`

- C. `-9`

- D. `-SIG`

36. 下列哪个命令将显示你 `Bash` 历史记录的最后 50 行，包括当前会话的命令？

- A. `bash 50`

- B. `history 50`

- C. `cat .bash_history`

- D. `tail -f .bash_history`

# 第 4 章

# 设备、Linux 文件系统和文件标准 (领域 104)

以下 `CompTIA LINUX+/LPIC-1` 考试目标在本章中涵盖：

- 104.1 创建分区和文件系统

    - 管理 `MBR` 分区表
    - 使用各种 `mkfs` 命令创建各种文件系统，如
        - `ext2`
        - `ext3`
        - `ext4`
        - `XFS`
        - `VFAT`
    - 对 `ReiserFS` 和 `Btrfs` 的了解



# 104.2 维护文件系统的完整性

- 验证文件系统的完整性
- 监控剩余空间和节点（`inodes`）
- 修复简单的文件系统问题

**以下是部分文件、术语和工具：**

- `du`
- `df`
- `fsck`
- `e2fsck`
- `mke2fs`
- `debugfs`
- `dumpe2fs`
- `tune2fs`
- `xfs tools`（如 `xfs_metadump` 和 `xfs_info`）

# 104.3 控制文件的挂载和卸载

- 手动挂载和卸载文件系统
- 配置启动时挂载文件系统
- 配置用户可挂载的可移动式文件系统

**以下是部分文件、术语和工具：**

- `/etc/fstab`
- `/media`
- `mount`
- `ummount`

# 104.4 管理磁盘配额

- 为文件系统设置磁盘配额
- 编辑、检查并生成用户配额报告

**以下是使用的文件、术语和工具的部分列表：**

- `quota`
- `edquota`
- `repquota`
- `quotaun`

# 104.5 管理文件权限和所有权

- 管理普通文件、特殊文件以及目录的访问权限
- 使用 `suid`、`sgid` 和粘位（`sticky bit`）等访问模式维护安全性
- 了解如何更改文件创建掩码（`umask`）
- 使用组字段为组成员授予文件访问权限

**以下是使用的文件、术语和工具的部分列表：**

- `chmod`
- `umask`
- `chown`
- `chgrp`

# 104.6 创建和更改硬链接和符号链接

- 创建链接
- 识别硬链接和/软链接
- 复制文件与链接文件
- 使用链接支持系统管理任务

**以下是使用的文件、术语和工具的部分列表：**

- `ln`
- `ls`

# 104.7 查找系统文件并将文件放置在正确位置

- 理解 `FHS`（文件系统层次结构标准）下文件的正确位置
- 在 Linux 系统上查找文件和命令

![](img/84990579543ce21a46ac6dc507fcde32_80_0.png)

- 了解 `FHS` 定义的重要文件和目录的位置及其用途

**以下是使用的文件、术语和工具的部分列表：**

- `find`
- `locate`
- `updatedb`
- `whereis`
- `which`
- `type`
- `/etc/updatedb.conf`

![](img/84990579543ce21a46ac6dc507fcde32_81_0.png)

# 第 4 章 • 设备、Linux 文件系统和文件系统层次结构标准

1. 哪个命令可以用于确定在当前环境和位置输入时将运行的可执行文件的位置？
   A. `which`
   B. `what`
   C. `which`
   D. `when`

2. 下列哪个命令可以正确将名为 `a.out` 的文件的组所有更改更改 `users`？
   A. `chgrp users a.out`
   B. `chgrp a.out users`
   C. `groupchg a.out users`
   D. `grpchg users a.out`

3. 另一位管理员对用于管理目的的本地脚本之一进行了更改。该更改也立即反映在你的脚本副本中。然而，当用 `ls` 检查文件时，它看起来是一个普通文件。这种情况下可能的原因是什么？
   A. 文件在编辑后被执行。
   B. 管理员将文件复制给了你。
   C. 你的文件是原始文件的硬链接。
   D. 文件已从备份中恢复。

4. 下列哪个命令显示所有文件系统的节点（`inodes`）使用情况？
   A. `df -i`
   B. `ls -i`
   C. `du -i`
   D. `dm -i`

5. 在 `ext3` 文件系统上运行 `fsck` 时，过程比预期的要长，需要管理员输入以修复问题。下次执行该命令时可以添加哪个选项以便在无需干预的情况下自动尝试修复错误？
   A. `-o`
   B. `-v`
   C. `-y`
   D. `-f`

6. 在系统中插入新的硬盘后，让该硬盘准备好供 Linux 的正确顺序是什么？
   A. 使用 `fdisk` 创建分区，然后挂载分区。
   B. 挂载分区。
   C. 使用 `fdisk` 创建分区并使用 `-a` 挂载所有新创建的分区。
   D. 使用 `fdisk` 创建分区，然后使用类似 `mkfs` 的工具格式化分区，然后挂载分区。

7. 你正在使用 `SAN`（存储区域网络），由于 `SAN` 供应商创建的不适当内核模块，你的 Linux 系统经常报错。当 `SAN` 发送更新时，会导致文件系统被挂载为只读。你可以使用哪个命令和选项更改文件系统的行为以考虑 `SAN` bug？
   A. `mount--continue`
   B. `tune2fs -e continue`
   C. `mkfs --no-remount`
   D. `mount -o remount`

7. 下列哪个描述了 `ext2` 和 `ext3` 文件系统之间的主要区别？
   A. `ext3` 主要是 `ext2` 的错误修复更新。
   B. `ext3` 包含了文件系统的日志功能。
   C. `ext3` 完全改变了管理磁盘所需的工具。
   D. `ext3` 没有显著差异。

9. `umask` 的哪个选项将以 `POSIX` 格式显示将要使用的权限？
   A. `-p`
   B. `-p`
   C. `-s`
   D. `-v`

10. `ln` 的哪个选项可以创建指向另一个文件的符号链接？
    A. `-sl`
    B. `-s`
    C. `-l`
    D. `--ln`

11. 如果你需要定位给定命令的各种元素（例如其二进制文件和帮助页），可以使用下述哪个命令？
    A. `whatis`
    B. `find`
    C. `whereis`
    D. `ls`

12. `/etc/updatedb.conf` 中的哪个选项会将路径从结果包含中移除？
    A. `PRUNPATHS`
    B. `EXCLUDEDEPATH`
    C. `INCLUDEEXCLUDE`
    D. `SEPARATEPATH`

# 第 4 章 ■ 设备、Linux 文件系统和文件系统层次结构标准

13. 根据 `FHS`，服务器特定数据的正确位置是哪里？
    A. `/etc`
    B. `/var`
    C. `/tmp`
    D. `/srv`

14. 下列哪个命令可以为名为 `homescript.sh` 的文件用户启用粘位？
    A. `chmod +sticky homescript.sh`
    B. `chmod 755 homescript.sh`
    C. `chmod u+s homescript.sh`
    D. `u+sticky homescript.sh`

15. `mount` 命令的哪个选项将挂载 `/etc/fstab` 中当前可所有文件系统？
    A. `-f`
    B. `-d`
    C. `-a`
    D. `-m`

16. 哪个命令用于格式化交换分区？
    A. `fdisk`
    B. `mkswap`
    C. `formatswap`
    D. `format -s`

17. 哪个命令和选项用于显示文件系统挂载的次数？
    A. `tune2fs -h`
    B. `cat /etc/fstab`
    C. `mount -a`
    D. `less /etc`

18. `xfs_metadata` 的哪个选项显示进度指示？
    A. `-g`
    B. `-p`
    C. `-f`
    D. `-v`

19. 哪个命令用于执行文件系统的配额检查？
    A. `quota -u`
    B. `runquota -u`
    C. `qcheck -u`
    D. `quotacheck -u`

20. 目录空间不足且未启用配额。可以使用哪个命令来确定包含大文件的目录？
    A. `du`
    B. `df`
    C. `ls`
    D. `locate`

21. 哪个文件包含要挂载的文件系统、其分区以及应该用于挂载它们的选项？
    A. `/etc/filesystems`
    B. `/etc/mounts`
    C. `/etc/fstab`
    D. `/srv/media`

22. 根据 `FHS`，可移动媒体的适当挂载点是？
    A. `/etc`
    B. `/srv`
    C. `/tmp`
    D. `/media`

23. 哪个文件包含当前挂载文件系统的信息及其挂载选项？
    A. `/etc/mtab`
    B. `/etc/fstab`
    C. `/tmp/files`
    D. `/etc/filesystems`

24. `unmount` 命令的哪个选项会在卸载失败时导致文件系统重新挂载为只读模式？
    A. `-o`
    B. `-r`
    C. `-f`
    D. `-v`

# 第 4 章 ■ 设备、文件系统和层次结构标准

25. `umask` 命令报告掩码为 `022`。对于新的非执行文件的权限是什么？
    A. `u+rw, g+r, w+r`
    B. `755`
    C. `022`
    D. `a+r`

26. 使用 `ls -la` 获取目录列表时，看到一个权限为 `lrwxrwxrwx` 的对象。这是什么类型的对象？
    A. 它是一个目录。
    B. 它是一个符号链接。
    C. 它是一个临时文件。
    D. 它是一个本地文件。

27. 哪个命令和选项将输出当前读写且启用配额的文件系统的配额使用摘要？
    A. `repqa -a`
    B. `repquota -a`
    C. `quotaran -a`
    D. `quota -u`

28. `locate` 命令报告信息过期。应该运行哪个命令让 `locate` 命令更新数据库？
    A. `locateddb -u`
    B. `locate -u`
    C. `updatedb`
    D. `locate`

29. 哪个 shell 内置命令可以确定将运行哪个命令？
    A. `type`
    B. `when`
    C. `find`
    D. `help`

30. `chown` 的哪个选项递归地更改所有权？
    A. `-f`
    B. `-R`
    C. `-a`
    D. `-m`

# 第一部分 - CompTIA Linux+/LPIC-1

31. 下列哪个代表了 `/etc/fstab` 文件的正确格式？
    A. `<directory> <device> <type> <options>`
    B. `<device> <type> <options>`
    C. `<device> <type> <options> <directory> <dump> <fsck>`
    D. `<device> <directory> <type> <options> <dump> <fsck>`

32. 下列哪个命令用于识别分区的 `UUID`？
    A. `blkid`
    B. `ls`
    C. `find`
    D. `cat`

33. `xfs_info` 命令在功能上等同于哪个命令和选项？
    A. `xfs_test -n`
    B. `xfs_list`
    C. `tunexfs -i`
    D. `xfs_growfs -n`

34. 下列哪个命令将在第一个 `SATA` 器上创建 `btrfs` 文件系统？
    A. `mkfs /dev/sda`
    B. `mkfs.btrfs /dev/sda`
    C. `mkfs.btrfs /dev/sda`
    D. `mkfs -b /dev/sda`

35. 文件系统上设置了哪个选项以启用用户级配额？
    A. `quotaon`
    B. `enquota=user`
    C. `usrquota`
    D. `userquota`

36. 你需要允许 Web 服务器（以 `www-data` 用户和组运行）写入名为 `/home/webfiles/` 的目录。哪些命令能以最安全的方式完成此任务？
    A. `chgrp www-data /home/webfiles; chmod 775 /home/webfiles`
    B. `chmod 777 /home/webfiles`
    C. `chgrp www-data /home/webfiles; chmod 711 /home/webfiles`
    D. `chmod 707 /home/webfiles`

# 第 4 章 ■ 设备、Linux 文件系统和文件系统层级标准 49

37. 使用哪个命令和选项来设置文件系统在两次运行 `fsck` 之间允许挂载的最大次数？
    A. `tune2fs -c`
    B. `tune2fs -f`
    C. `tune2fs -m`
    D. `setmount`

38. 哪个命令可以更改磁盘的分区方案，例如在不删除现有分区的情况下更改其分区的大小？
    A. `resize2fs`
    B. `parted`
    C. `mkfs`
    D. `fdisk`

39. 假设 USB 驱动器使用 `VFAT` 文件系统，使用哪个命令可以将 USB 设备 `/dev/sdb1` 挂载到 `/media/usb` 目录？
    A. `mount -t vfat /dev/sdb1 /mnt`
    B. `usbmount /dev/sdb1 /mnt/usb`
    C. `mount -t vfat /dev/sdb1 /media/usb`
    D. `mount -t usb /dev/sdb1 /mnt/usb`

40. `gdisk` 的哪个选项可以更改分区名称？
    A. `n`
    B. `b`
    C. `v`
    D. `c`

41. `dump2fs` 命令的哪个选项可以显示因被标记为坏块而被保留的块？
    A. `-v`
    B. `-f`
    C. `-b`
    D. `-m`

42. `fsck` 的哪些选项可以检查 `/etc/fstab` 中列出的除根分区以外的所有文件系统？
    A. `-NR`
    B. `-AM`
    C. `-X`
    D. `-C`

# 50 第一部分 CompTIA Linux+/LPIC-1

43. 哪个命令用于在之前已设置过配额使用的文件系统上启用配额？
    A. `quotaenable`
    B. `quotaon`
    C. `quotau`
    D. `enquota`

44. `/etc/fstab` 中的哪个选项设置了设备在启动时检查的顺序？
    A. `options`
    B. `dump`
    C. `fsck`
    D. `checkorder`

45. `quotacheck` 的哪个选项用于首次创建文件？
    A. `-f`
    B. `-u`
    C. `-m`
    D. `-c`

46. `SAN` 崩溃了，导致 Linux 服务器上的一个文件系统严重损坏。使用哪个命令和选项可以检查驱动器内容而不造成更多损坏？
    A. `fdisk`
    B. `mke2fs -c`
    C. `debugfs -c`
    D. `ls -a`

47. `find` 命令的哪个选项将根据 `inode` 节点搜索文件？
    A. `-inode`
    B. `-type`
    C. `-in`
    D. `-inum`

48. `chgrp` 的哪个选项可以更改给定目录内所有文件的组所有权？
    A. `-directory`
    B. `-d`
    C. `-R`
    D. `-V`

# 第 5 章

# 使用 Shell、脚本和数据管理 (领域 105)

本章涵盖了以下 `COMPTIA LINUX+/LPIC-1` 考试目标：

## 105.1 自定义和使用 shell 环境

- 在登录时或启动新 shell 时设置环境变量（例如 `PATH`）
- 为频繁使用的命令序列编写 `Bash` 函数
- 为新用户账户维护骨架目录
- 使用正确的目录设置命令搜索路径

**以下是所用文件、术语和工具的部分列表：**

- `source`
- `/etc/bash.bashrc`
- `/etc/profile`
- `env`
- `export`
- `set`
- `unset`
- `~/.bash_profile`
- `~/.bash_login`
- `~/.profile`
- `~/.bashrc`
- `~/.bash_logout`
- `function`
- `alias`
- `lists`

![](img/84990579543ce21a46ac6dc507fcde32_90_0.png)

## 105.2 自定义或编写简单脚本

- 使用标准 `sh` 语法（循环、测试）
- 使用命令替换
- 测试命令提供的成功失败或其他信息
- 向超级用户执行条件邮件发送
- 通过 `shebang` (`#!`) 行正确选择脚本解释器
- 管理脚本的位置、所有权、执行权限和 `suid` 权限

**以下是所用文件、术语和工具的部分列表：**

- `for`
- `while`
- `test`
- `if`
- `read`
- `seq`
- `exec`

## 105.3 SQL 数据管理

- 使用基础 `SQL` 命令
- 执行基础数据操作

**以下是所用文件、术语和工具的部分列表：**

- `insert`
- `update`
- `select`
- `delete`
- `from`
- `where`
- `group by`
- `order by`
- `join`

![](img/84990579543ce21a46ac6dc507fcde32_91_0.png)
![](img/84990579543ce21a46ac6dc507fcde32_92_0.png)

1. 哪个命令用于在 `Bash` shell 中读取并执行文件？
   A. `run`
   B. `execute`
   C. `source`
   D. `func`

2. 假设所有用户都使用 `Bash`。此命令应该放在哪个文件中？
   A. `~/.bash_logout`
   B. `/etc/bash_logout`
   C. `/home/.bash_logout`
   D. `/etc/bashlogout`

3. 以下哪个命令移除已设置的环境变量？
   A. `unset`
   B. `env`
   C. `set`
   D. `import`

4. 设置 脚本的 `shebang` 行时，哪个命令将自动确定解释器的位置？
   A. `#!usr/bin/env`
   B. `#!bin/bash`
   C. `#!env`
   D. `#!bin/bash`



5. 查询数据库时，以下语句从名为 `users` 的表中检索所有数据？

-   A. `SELECT ALL FROM users;`
-   B. `QUERY ALL FROM users;`
-   C. `SELECT * FROM Users;`
-   D. `SELECT * FROM users;`

6. 以下哪项对 `PS1` 变量的描述最准确？

-   A. `PS1` 用于设置命令的位置。
-   B. `PS1` 用于定义 `Bash` 的默认 shell提示符。
-   C. `PS1` 作为系统变量使用。
-   D. `PS1` 是用户定义的没有默认值。

7. 以下哪个命令在执行 `ls` 命令时不带选项时确保使用了 `-la` 选项？

-   A. `alias ls="ls -la"`
-   B. `ln -s ls -la`
-   C. `alias "ls -la"=ls`
-   D. `set ls`

8. 登录 `Bash` shell 时配置文件的顺序是什么？

-   A. `.bash_login`, `.profile`, `/etc/profile`
-   B. `.bash_profile`, `.profile`, `.bash_login`
-   C. `.profile`, `.bash_login`, `.bash_profile`
-   D. `.bash_login`, `.bash_profile`, `.profile`

9. `Bash` 脚本中的哪个变量用于访问第一个参数？

-   A. `$ARG`
-   B. `$0`
-   C. `$1`
-   D. `$@`

10. 以下哪个符号为 `Bash` 脚本中的 `if` 条件提供结束标志？

-   A. `ex`
-   B. `}`
-   C. `]`
-   D. `fi`

11. 以下哪个命令将删除 `MySQL` 中名为 `virtualusers` 的表的所有数据？

-   A. `DELETE FROM VIRTUAL;`
-   B. `DELETE FROM virtualusers;`
-   C. `DELETE * FROM virtualusers;`
-   D. `DELETE ALL FROM virtualusers;`

12. 以下哪个命令显示指定表的列和列类型？

-   A. `DESC`
-   B. `ASK`
-   C. `SELECT`
-   D. `DISPLAY`

# 第一部分 CompTIA Linux+/LPIC-1

13. 以下哪个命令将打印从 0 开始的六个数列表？

-   A. `list 0-5`
-   B. `seq 1 5`
-   C. `echo 0-5`
-   D. `seq 1 6`

14. 创建脚本时，使用哪个命令显示变量的内容？

-   A. `var_dump`
-   B. `echo`
-   C. `ls`
-   D. `env`

15. 一个命令通过 `ls -la` 获取了如下列表：

```
-rwsr-xr-x 1 user user 21 Nov 2 13:53 script.sh
```

列表中用户权限中的 `s` 表示什么？

-   A. 该程序设置了 `SUID` 标志位。
-   B. 这是一个符号链接。
-   C. 该文件将不可执行。
-   D. 该文件是一个特殊的系统文件。

16. 以下哪个命令将在执行脚本后退出 shell？

-   A. `run`
-   B. `source`
-   C. `./`
-   D. `exec`

17. 哪种字符序列只有在第一个命令成功退出时执行两个命令？

-   A. `&*`
-   B. `&&`
-   C. `;`
-   D. `&`

18. Shell 脚本中的哪个命令等待用户输入并将输入放入变量中？

-   A. `exec`
-   B. `get`
-   C. `read`
-   D. `prompt`

# 第 5 章 使用 Shell、脚本和数据管理 (领域 105)

19. 使用什么字符在 shell 脚本中将命令序列标记为函数？

-   A. 使用括号声明函数（可选），使用花括号包含命令
-   B. 使用花括号声明函数，使用括号包含命令
-   C. 使用方括号声明函数，使用花括号包含命令
-   D. 使用引号表示函数

20. 假设你从 `MySQL` 数据库检索数据，并根据名为“`id`”的列按数字升序显示。在 `SELECT` 语句中添加以下哪个命令可以完成任务？

-   A. `ORDER BY id ASC;`
-   B. `ORDER BY id;`
-   C. `GROUP BY id;`
-   D. `GROUP BY ASC;`

21. 字符字符表示在前一个命令未成功退出时执行替代命令？

-   A. `&&`
-   B. `--`
-   C. `||`
-   D. `EL`

22. 哪个关键词用于启动 `Bash` 脚本中的备选条件？

-   A. `if`
-   B. `else if`
-   C. `elif`
-   D. `elsif`

23. 以下哪个命令移除当前定义的别名命令？

-   A. `remove`
-   B. `rm`
-   C. `unalias`
-   D. `delete`

24. 在 `Bash` 中 `source` 文件时，假设你的当前用户拥有该文件，哪个 `chmod` 命令将提供最小权限以确保文件被正确 `source`？

-   A. `chmod 600`
-   B. `chmod 755`
-   C. `chmod 777`
-   D. `chmod 400`

25. 假设一个用空格分隔的数值列表定义为 `LIST="one two three four"`，以下哪种 `for` 循环结构将遍历列表中的元素？

-   A. `for LIST`
-   B. `for VAR in LIST`
-   C. `for VAR in $LIST`
-   D. `for $LIST -> $VAR`

26. 在 `SQL` 中看到类似 `table1.id = table2.id` 的语句时，将使用哪种类型的连接（`join`）？

-   A. 内连接 (Inner)
-   B. 外连接 (Outer)
-   C. 左外连接 (Left outer)
-   D. 右外连接 (Right outer)

27. Shell 脚本循环中的哪种测试将检查一个值是否小于另一个值？

-   A. `-less`
-   B. `-lessThan`
-   C. `-lt`
-   D. `-than`

28. 下列哪个测试可以判断 shell 脚本上下文中文件是否存在？

-   A. `-a`
-   B. `-e`
-   C. `-m`
-   D. `-i`

29. 应该将文件放在哪个目录下，以便在创建用户时将这些文件自动复制到用户的家目录？

-   A. `/etc/userhome`
-   B. `/etc/templateuser`
-   C. `/etc/skel`
-   D. `/home/skel`

30. 下列哪项代表 `SQL` `UPDATE` 语句的正确语法？

-   A. `UPDATE <table> SET <column> = <newvalue> WHERE <column> = <value>`
-   B. `UPDATE <table> WHERE <column> = <newvalue>`
-   C. `UPDATE WHERE <column> = <newvalue>`
-   D. `UPDATE FROM <table> VALUE (<value>)`

# 第 5 章 使用 Shell、脚本编写和数据管理（领域 105）

31. 假设一个名为 `AUTHENTICATION` 的 `MySQL` 表有三列（`id`, `username`, `password`）。下列哪条语句向表中插入一行数据？

-   A. `INSERT id,username,password INTO AUTHENTICATION;`
-   B. `INSERT INTO AUTHENTICATION VALUES ('user','pass');`
-   C. `INSERT INTO AUTHENTICATION ('','user','pass');`
-   D. `INSERT INTO AUTHENTICATION (username,password) VALUES ('user','pass');`

32. `Bash` 的哪个选项将导致 shell 在不读取初始化文件的情况下执行？

-   A. `--no-rc`
-   B. `--no-init`
-   C. `--norc`
-   D. `--rc-none`

33. 下列哪项在 `bash` 脚本中用于创建一个数组？

-   A. `ARRAY=(val1 val2)`
-   B. `ARRAY="val1 val2"`
-   C. `ARRAY_PUSH($ARRAY,"val1","val2");`
-   D. `ARRAY{} = "val1"`

34. `declare` 语句的哪个选项以一种可以作为另一个命令输入的方式显示输出？

-   A. `-o`
-   B. `-n`
-   C. `-p`
-   D. `-m`

35. 你需要创建一个函数，该函数在每次登录系统时都可用。该函数应该放在哪个文件中？

-   A. `.bash_profile`
-   B. `.rc`
-   C. `/etc/profile`
-   D. `.bash_run`

36. 哪个 shell 内置命令用于显示只读变量列表？

-   A. `ro`
-   B. `readonly`
-   C. `env-ro`
-   D. `ro-env`

37. 下列哪个 `SQL` 关键字可以与 `GROUP BY` 子句一起使用？

-   A. `SELECT`
-   B. `INSERT`
-   C. `UPDATE`
-   D. `DELETE`

38. 使用哪些字符来表示 shell 脚本中 `while` 循环测试部分的开始和结束？

-   A. 括号 `( )`
-   B. 花括号 `{ }`
-   C. 方括号 `[ ]`
-   D. 双引号 `""`

39. 当使用带有一个参数的 `test` 内置命令时，如果其参数不为空，则返回值将是什么？

-   A. `false`
-   B. `true`
-   C. `unknown`
-   D. `-1`

40. 当使用波浪号字符切换目录（如 `cd ~`）时，使用的是哪个环境变量？

-   A. `HOMEDIR`
-   B. `HOMEPATH`
-   C. `HOME`
-   D. `MAILPATH`

41. 如果你想在用户一段时间未活动后自动将其注销 shell，可以设置哪个环境变量？

-   A. `TIMEOUT`
-   B. `TMOUT`
-   C. `TO`
-   D. `IDLETIME`

42. 在 shell 脚本中使用 `case` 语句时，哪种序列表示 `case/switch` 语句的结束？

-   A. `caseend`
-   B. `esac`
-   C. `endcase`
-   D. `}`



# 第 5 章 • 使用 Shell、脚本编写和数据管理（领域 105）

31. 假设一个名为 `AUTHENTICATION` 的 MySQL 表有三列（`id`, `username`, `password`）。下列哪条语句向表中插入一行数据？

- A. `INSERT id,username,password INTO AUTHENTICATION;`
- B. `INSERT INTO AUTHENTICATION VALUES ('user','pass');`
- C. `INSERT INTO AUTHENTICATION ('','user','pass');`
- D. `INSERT INTO AUTHENTICATION (username,password) VALUES ('user','pass');`

32. `Bash` 的哪个选项将导致 shell 在不读取初始化文件的情况下执行？

- A. `--no-rc`
- B. `--no-init`
- C. `--norc`
- D. `--rc-none`

33. 下列哪项在 `bash` 脚本中用于创建一个数组？

- A. `ARRAY=(val1 val2)`
- B. `ARRAY="val1 val2"`
- C. `ARRAY_PUSH($ARRAY,"val1","val2");`
- D. `ARRAY{} = "val1"`

34. `declare` 语句的哪个选项以一种可以作为另一个命令输入的方式显示输出？

- A. `-o`
- B. `-n`
- C. `-p`
- D. `-m`

35. 你需要创建一个函数，该函数在每次登录系统时都可用。该函数应该放在哪个文件中？

- A. `.bash_profile`
- B. `.rc`
- C. `/etc/profile`
- D. `.bash_run`

36. 哪个 shell 内置命令用于显示只读变量列表？

- A. `ro`
- B. `readonly`
- C. `env-ro`
- D. `ro-env`

37. 下列哪个 SQL 关键字可以与 `GROUP BY` 子句一起使用？

- A. `SELECT`
- B. `INSERT`
- C. `UPDATE`
- D. `DELETE`

38. 使用哪些字符来表示 shell 脚本中 `while` 循环测试部分的开始和结束？

- A. 括号 `( )`
- B. 花括号 `{ }`
- C. 方括号 `[ ]`
- D. 双引号 `""`

39. 当使用带有一个参数的 `test` 内置命令时，如果其参数不为空，则返回值将是什么？

- A. `false`
- B. `true`
- C. `unknown`
- D. `-1`

40. 当使用波浪号字符切换目录（如 `cd ~`）时，使用的是哪个环境变量？

- A. `HOMEDIR`
- B. `HOMEPATH`
- C. `HOME`
- D. `MAILPATH`

41. 如果你想在用户一段时间未活动后自动将其注销 shell，可以设置哪个环境变量？

- A. `TIMEOUT`
- B. `TMOUT`
- C. `TO`
- D. `IDLETIME`

42. 在 shell 脚本中使用 `case` 语句时，哪种序列表示 `case/switch` 语句的结束？

- A. `caseend`
- B. `esac`
- C. `endcase`
- D. `}`

# 第 5 章 • 使用 Shell、脚本编写和数据管理（领域 105）

25. 假设一个用空格分隔的数值列表定义为 `LIST="one two three four"`，以下哪种 `for` 循环结构将遍历列表中的元素？

- A. `for LIST`
- B. `for VAR in LIST`
- C. `for VAR in $LIST`
- D. `for $LIST -> $VAR`

26. 在 SQL 中看到类似 `table1.id = table2.id` 的语句时，将使用哪种类型的连接（join）？

- A. 内连接 (Inner)
- B. 外连接 (Outer)
- C. 左外连接 (Left outer)
- D. 右外连接 (Right outer)

27. Shell 脚本循环中的哪种测试将检查一个值是否小于另一个值？

- A. `-less`
- B. `-lessThan`
- C. `-lt`
- D. `-than`

28. 下列哪个测试可以判断 shell 脚本上下文中文件是否存在？

- A. `-a`
- B. `-e`
- C. `-m`
- D. `-i`

29. 应该将文件放在哪个目录下，以便在创建用户时将这些文件自动复制到用户的家目录？

- A. `/etc/userhome`
- B. `/etc/templateuser`
- C. `/etc/skel`
- D. `/home/skel`

30. 下列哪项代表 SQL `UPDATE` 语句的正确语法？

- A. `UPDATE <table> SET <column> = <newvalue> WHERE <column> = <value>`
- B. `UPDATE <table> WHERE <column> = <newvalue>`
- C. `UPDATE WHERE <column> = <newvalue>`
- D. `UPDATE FROM <table> VALUE (<value>)`

# 第 6 章 ■ 理解用户界面和桌面（领域 106）

13. `X` 的哪种配置选项用于配置键盘模型？

- A. `XkbLayout`
- B. `XkbModel`
- C. `XkbType`
- D. `XkbInput`

14. `X` 服务器配置文件中 `Monitor` 部分内部的哪行配置行会将垂直刷新率设置在 55 到 75 赫兹之间？

- A. `Vert 55-75`
- B. `VertRefresh 55.0–75.0`
- C. `VertSync 55.0–75.0`
- D. `RefreshMode 55.0–75.0`

15. 在 `X` 会话中，以下哪个命令显示显示器信息，包括分辨率和色彩深度？

- A. `xrandinfo`
- B. `xterm`
- C. `xwin`
- D. `xdpyminfo`

16. 对于鼠标等输入设备，哪种 `AccelerationProfile`（加速配置文件）可以启用线性加速（更快的速度更大的加速度）？

- A. `0`
- B. `-1`
- C. `6`
- D. `7`

17. 基于 `X.org` 的服务器使用哪个目录来存储字体？

- A. `/usr/share/fonts`
- B. `/usr/X11/fonts`
- C. `/etc/fonts`
- D. `/var/font/xorg`

18. 盲文显示器（Braille display）的原生支持至少哪个版本的内核？

- A. `2.2.0`
- B. `2.4.22`
- C. `2.6.26`
- D. `3.2.1`

19. `xorg.conf` 文件中的哪种配置选项可以设置为防止用户使用 `Ctrl+Alt+小键盘加` 和 `Ctrl+Alt+小键盘减` 更改视频模式？

- A. `DontZoom`
- B. `Modes=No`
- C. `NoModeSwitch`
- D. `DontZap`

20. `GNOME` 包含原生的屏幕键盘功能。以下哪个命令可以启动屏幕键盘？

- A. `gok`
- B. `osk`
- C. `kb`
- D. `oskb`

21. 当使用 `GDM` 作为显示管理器时，可以使用哪个 GUI 程序设置登录窗口的选项？

- A. `gdmlogin`
- B. `gdmconfig`
- C. `gdmsetup`
- D. `ddm`

22. 使用 `KDE` 时，哪一个程序提供放大功能？

- A. `xmag`
- B. `mag`
- C. `pmag`
- D. `kmag`

23. `lightdm.conf` 文件中 `SeatDefaults` 部分的哪种选项用于禁用登录时的用户名显示？

- A. `greeter-disable-user`
- B. `greeter-enable-login`
- C. `greeter-show-manual-login`
- D. `greeter-disable-auto-login`

24. 在 `GNOME` 中，`GNOME 控制中心`（`GNOME Control Center`）的哪个部分用于选择高对比度主题？

- A. `Display`（显示）
- B. `Appearance`（外观）
- C. `Locale`（语言区域）
- D. `Contrast`（对比度）

25. 以下哪项最能描述鼠标手势（mouse gesture）的概念？

- A. 鼠标手势允许特殊点击，例如右键上下文菜单。
- B. 鼠标手势通过以特定方式移动鼠标来方便程序的使用。
- C. 鼠标手势用于登录。
- D. 鼠标手势用于截屏。

26. 在 `GNOME 3.9` 或更高版本中，哪个键盘快捷键可激活屏幕阅读器？

- A. `Super+R`
- B. `Super+S`
- C. `Ctrl+Super+S`
- D. `Alt+Super+S`

27. 假设启动时已禁用了显示管理器。登录后可以使用哪个命令启动 `X` 服务器？

- A. `xs`
- B. `xstart`
- C. `X -start`
- D. `startx`

28. `xorg.conf` 配置文件中的哪种选项配置了屏幕进入空闲模式但但不进入待机模式的时间，并且在不支持 `DPMS` 的显示器上可用？

- A. `StandbyTime`
- B. `BlankTime`
- C. `SuspendTime`
- D. `OffTime`

29. 以下哪个命令可以帮助你确定 `X` 会话中给定窗口的信息，包括窗口大小和位置信息？

- A. `xkbinfo`
- B. `xdxpy`
- C. `xwininfo`
- D. `xver`

30. `GOK` 内部的哪个选项/按钮用于显示替代鼠标的按键？

- A. `Mouse`
- B. `MouseKeys`
- C. `Movement`
- D. `Compose`

31. 以下哪个命令允许名为 `cwa` 的主机连接到 `X` 服务器？

- A. `xconnect cwa`
- B. `xterm +cwa`
- C. `xhost +cwa`
- D. `xf cwa`

32. `ssh` 配置文件中的以下哪项选项需要启用，以便会话可以通过 `ssh` 连接发送？

- A. `X11Connect yes`
- B. `ForwardX11 yes`
- C. `ForwardX yes`
- D. `XForward yes`

33. `xorg.conf` 配置文件中 `Files` 部分的哪种配置选项可以添加服务器搜索字体的路径？



### A. FontSection

- B. Fonts
- C. FontLoc
- D. FontPath

34. 使用哪种辅助技术为无法使用指针（如鼠标）的用户提供输入法？

- A. Keyboard（键盘）
- B. Sticky keys（粘滞）
- C. Mouse keys（鼠标键）
- D. On-screen keyboard（屏幕键盘）

35. 哪种辅助技术会忽略连续按下或按住的键？

- A. Sticky keys（粘滞）
- B. Mouse keys（鼠标键）
- C. Bounce keys（弹跳键）
- D. On-screen keyboard（屏幕键盘）

36. 使用 `LightDM` 时，使用哪个组合键返回终端？

- A. `Alt+Ctrl+F2`
- B. `Alt+Ctrl+F1`
- C. `Ctrl+F1`
- D. `Ctrl+Esc`

37. `LightDM` 配置中的哪种选项启用了特定用户的自动登录？

- A. `auto login`
- B. `auto user`
- C. `login auto`
- D. `user auto`

38. 哪种辅助技术会忽略连续按下或按住的键？

- A. Sticky keys（粘滞）
- B. Mouse keys（鼠标键）
- C. Bounce keys（弹跳键）
- D. On-screen keyboard（屏幕键盘）

39. 使用 `LightDM` 时，使用哪个组合键返回终端？

- A. `Alt+Ctrl+F2`
- B. `Alt+Ctrl+F1`
- C. `Ctrl+F1`
- D. `Ctrl+Esc`

40. `LightDM` 配置中的哪种选项启用了特定特定自动自动登录？

- A. `auto login`
- B. `auto user`
- C. `login auto`
- D. `user auto`

41. 假设启动时已禁用了显示管理器。登录后可以使用哪个命令启动 `X` 服务器？

- A. `xs`
- B. `xstart`
- C. `X -start`
- D. `startx`

42. `xorg.conf` 配置文件中的哪种选项配置了屏幕进入空闲模式但但不进入待机模式，并且在不支持 `DPMS` 的显示器上可用？

- A. `StandbyTime`
- B. `BlankTime`
- C. `SuspendTime`
- D. `OffTime`

43. 以下哪个命令可以帮助你确定 `X` 会话中给定窗口的信息，包括窗口大小和位置信息？

- A. `xkbinfo`
- B. `xdxpy`
- C. `xwininfo`
- D. `xver`

44. `GOK` 内部的哪个选项/按钮用于显示替代鼠标的按键？

- A. `Mouse`
- B. `MouseKeys`
- C. `Movement`
- D. `Compose`

45. 以下哪个命令允许名为 `cwa` 的主机连接到 `X` 服务器？

- A. `xconnect cwa`
- B. `xterm +cwa`
- C. `xhost +cwa`
- D. `xf cwa`

46. `ssh` 配置文件中的以下哪项选项需要启用，以便会话可以通过 `ssh` 连接发送？

- A. `X11Connect yes`
- B. `ForwardX11 yes`
- C. `ForwardX yes`
- D. `XForward yes`

47. `xorg.conf` 配置文件中 `Files` 部分的哪种配置选项可以添加服务器搜索字体的路径？

- A. `FontSection`
- B. `Fonts`
- C. `FontLoc`
- D. `FontPath`

48. 使用哪种辅助技术为无法使用指针（如鼠标）的用户提供输入法？

- A. Keyboard（键盘）
- B. Sticky keys（粘滞）
- C. Mouse keys（鼠标键）
- D. On-screen keyboard（屏幕键盘）

49. 哪种辅助技术会忽略连续按下或按住的键？

- A. Sticky keys（粘滞）
- B. Mouse keys（鼠标键）
- C. Bounce keys（弹跳键）
- D. On-screen keyboard（屏幕键盘）

# 第 7 章

# 管理任务（领域 107）

本章涵盖以下 `CompTIA LINUX+`/`LPIC-1` 考试目标：

- `107.1` 管理用户账户和相关文件
    - 添加、修改和删除用户和组
    - 管理密码/组数据库中的用户信息
    - 创建特殊目的和受限账户
    - 以下是使用的文件和工具列表：
        - `/etc/passwd`
        - `/etc/shadow`
        - `/etc/group`
        - `/etc/skel`
        - `chage`
        - `getent`
        - `groupadd`
        - `groupdel`
        - `groupmod`
        - `passwd`
        - `useradd`
        - `userdel`
        - `usermod`

- `107.2` 通过调度任务自动化管理任务
    - 管理 `cron` 和 `at` 任务
    - 配置用户对 `cron` 和 `at` 服务的访问
    - 配置 `anacron`
    - `/etc/cron.{d,daily,hourly,monthly,weekly}`
    - `/etc/at.deny`
    - `/etc/at.allow`
    - `/etc/crontab`
    - `/etc/cron.allow`
    - `/etc/cron.deny`
    - `/var/spool/cron/*`
    - `crontab`
    - `at`
    - `atq`
    - `atrm`
    - `anacron`
    - `/etc/anacrontab`

- `107.3` 本地化和国际化
    - 配置本地设置和环境变量
    - 配置时区设置和环境变量
    - 以下是使用的文件和工具列表：
        - `/etc/timezone`
        - `/etc/localtime`
        - `/usr/share/zoneinfo`
        - `LC_*`
        - `LC_ALL`
        - `LANG`
        - `TZ`
        - `/usr/bin/locale`
        - `tzselect`
    - `tzconfig`
    - `date`
    - `iconv`
    - `UTF-8`
    - `ISO-8859`
    - `ASCII`
    - `Unicode`

![](img/84990579543ce21a46ac6dc5014.png)

1. 哪个文件包含用户信息（如用户名和真实姓名），并对所有用户可见？

- A. `/etc/pass`
- B. `/etc/shadow`
- C. `/etc/passwd`
- D. `/etc/user-info`

2. 下列哪个命令会在每天上午12:15 和 下午12:15 通过 `cron` 执行任务？

- A. `0,12 * *`
- B. `15 0,12 * *`
- C. `15 * * 0/12`
- D. `*/12 * * 15`

3. 哪个文件用于指示服务器的本地时区？

- A. `/etc/time`
- B. `/etc/timezoneconfig`
- C. `/etc/localtime`
- D. `/etc/localtz`

4. 哪个文件用于提供可以添加和删除 `cron` 任务的用户列表？

- A. `/etc/cron.job`
- B. `/etc/cron.allow`
- C. `/etc/cron.users`
- D. `/etc/crontab`

5. 下列哪个命令移除账户过期时间？

- A. `sudo chage -l username`
- B. `sudo chage -E -1`
- C. `sudo chage -E username`
- D. `sudo chage --noexpire username`

6. 在哪个目录下找到不同地区的时区文件？

- A. `/etc/timezoneinfo`
- B. `/etc/zoneinfo`
- C. `/var/zoneinfo`
- D. `/usr/share/zoneinfo`

## 第 7 章 管理任务 (Domain 107)

7. 下列哪个命令从现在开始调度一系列命令？

- A. `at +1hr`
- B. `at now + 1 hour`
- C. `atq`
- D. `at -1`

8. 你需要从系统中删除一个用户，包括其家目录。下列哪个命令可以完成此任务？

- A. `userdel`
- B. `userdel -r`
- C. `userdel -R`
- D. `deluser`

9. 在创建用户时，应该在哪个目录下放置文件以便将其复制到用户的家目录？

- A. `/etc/skel`
- B. `/etc/homedir`
- C. `/home/useplate`
- D. `/etc/template`

10. 如果你需要的计算机在不同时间关机，应该使用哪种任务调度器？

- A. `cron.d`
- B. `cron.hourly`
- C. `anacron`
- D. `at`

11. 下列哪个命令以自 `epoch` 秒的格式提供当前日期和时间？

- A. `date %+seconds`
- B. `date +%s`
- C. `date --seconds`
- D. `date --now`

12. `iconv` 命令的哪个选项显示特定系统中可用的字符集？

- A. `--show-char`
- B. `--show`
- C. `--list`
- D. `--all`

13. 哪个环境变量控制日期时间的格式（例如 12 小时或 24 小时时钟）？

- A. `LOCALE_DATE`
- B. `DATE_FORMAT`
- C. `LC_TIME`
- D. `LC_DATE`

14. 哪个命令显示当前通过 `at` 调度的任务列表？

- A. `atlist`
- B. `atq`
- C. `atl`
- D. `at --jobs`

15. 如果用户不允许交互式地登录计算机，应该将用户设置为哪个 shell？

- A. `/bin/bash`
- B. `/bin/tcsh`
- C. `/bin/zsh`
- D. `/bin/false`

16. 下列哪种编码提供了字符的多字节表示？

- A. `ISO-8859`
- B. `UTF-8`
- C. `ISO-L`
- D. `UFTMulti`

17. 下列哪个命令将名为 `DomainAdmins` 的组改为 `DomainUsers`？

- A. `groupmod -n DomainAdmins DomainUsers`
- B. `groupch DomainAdmins DomainUsers`
- C. `chgroup DomainAdmins DomainUsers`
- D. `group -N DomainAdmins DomainUsers`

18. 在哪个目录下你会找到对应于系统中当前 `cron` 任务的用户文件列表？

- A. `/var/spool/cron/crontabs`
- B. `/var/spool/jobs`
- C. `/etc/cron`
- D. `/etc/cron.users`

19. 哪个命令删除 `ID` 为 3 的 `at` 任务？

- A. `atq`
- B. `at -l`
- C. `atm 3`
- D. `rmat`

20. 哪个命令可以查看系统上可用的时区并获取可用于脚本设置时区的输出？

- A. `tzd`
- B. `/etc/locale`
- C. `tzdata`
- D. `tzselect`

21. 你需要确定 `LDAP` 集成是否工作。为了实现这一点，你想通过 `/etc/nconf` 获取用户列表？

- A. `get`
- B. `getent`
- C. `usermod`
- D. `userlist`

22. 在添加用户和组时，哪个文件的名称包含最大和最小用户 `ID` 信息？

- A. `/etc/groupinfo`
- B. `/etc/login.defs`
- C. `/etc/login.info`
- D. `/etc/loginlist`

23. 下列哪个被用作全局 `cron` 文件？

- A. `/etc/cron.d`
- B. `/etc/cron.sys`
- C. `/etc/crontab`
- D. `/etc/cron.tab`

24. 添加到用户家目录下的 `.profile` 中的下列哪行会将时区设置为 `America/Chicago`？

- A. `TZ=/Central; export TZ`
- B. `TIMEZONE='America/Chicago'; export TIMEZONE`
- C. `set TZ=/Central`
- D. `TZ='America/Chicago'; export TZ`

25. 在哪个目录下你会找到每 24 小时通过 `cron` 的脚本？

- A. `/etc/cron.daily`
- B. `/etc/cron.weekly`
- C. `/etc/cron.hourly`
- D. `/etc/crontab`

26. 下列 `LANG` 变量的哪个会让系统跳过本地化（locale）？

- A. `LANG=COMPAT`
- B. `LANG=NONE`
- C. `LANG=C`
- D. `LANG=END`

27. 运行 `useradd` 时，需要指定哪个选项以创建家目录？

- A. `-h`
- B. `-m`
- C. `-x`
- D. `-a`

28. 下列哪个命令锁定用户的密码登录，但不阻止其他形式的登录？

- A. `usermod L`
- B. `userdel -r`
- C. `useradd -h`
- D. `userlock`

29. 如果你需要重新配置特定会话的所有本地变量和设置，可以使用哪个环境变量？

- A. `LC_LIST`
- B. `LC_GLOBAL`
- C. `LC_ALL`
- D. `ALL_LOCALE`

30. 下列哪个项在放在 `/etc/crontab` 中会以 `www-data` 用户身份运行名为 `/usr/local/bin/changehome.sh` 的命令？

- A. `1 1 * * www-data /usr/local/bin/change.sh`
- B. `www-data changehome.sh`
- C. `*/1 www-data changehome.sh`
- D. `* * */www-data /usr/local/bin/changehome.sh`

31. 下列哪个命令产生列系统中所有用户最后密码更改时间的报告？

- `passwd -a`
- `passwd -S`
- `passwd a -S`
- `passwd --all`

32. 假设密码每 60 天必须更改一次。哪个命令会更改用户的最后密码更改日期，而不实际用户更改账户？

- `chage -f`
- `chage -w`
- `chage -l`
- `chage -d`

33. 下列哪个文件被 `anacron` 用于读取任务相关的配置信息？

- `/etc/anacron.d`
- `/etc/anacrontab`
- `/etc/anacron.config`
- `/etc/anacron.conf`

34. 下列哪个命令将系统级时区设置为 `America/Los_Angeles`？

- `-sf /usr/share/zoneinfo/America/Los_Angeles /etc/localtime`
- `-sf America/Los_Angeles; /etc/localtime`
- `-sd /etc/localtime /usr/share/timezone/America/Los_Angeles`
- `-sf /etc/localtime /usr/share/zoneinfo/America/Los_Angeles`

35. 哪个文件包含不允许创建 `cron` 调度任务的用户列表？

- `/etc/cron.users`
- `/etc/cron.deny`
- `/etc/cron.allow`
- `/etc/cron.userlist`

36. 哪个文件包含用户名、`UID` 和加密密码的列表？

- `/etc/passwd`
- `/etc/shadow`
- `/etc/encpass`
- `/etc/grouppass`

37. 下列哪项最符合 Linux 系统上 `UID` 和 `GID` 之间的关系？

- A. 对于特定用户，`UID` 和 `GID` 在系统中是相同的。
- B. 每个用户都有相同的 `UID` 和 `GID`，并且在用户创建时创建。
- C. `UID` 代表用户，而 `GID` 是一个全局唯一的用户 ID。
- D. `UID` 和 `GID` 之间没有直接关系。

38. 在基于 Debian 的系统中，哪个命令可以使用包的工具更改时区？

- A. `dpkg-reconfigure time`
- B. `dpkg-reconfigure tzdata`
- C. `apt-select tzdata`
- D. `apt-config timezone`



## 39. 哪个命令用于将用户的家目录更改为 `/srv/data/username` 并同时移动内容？

A. `usermod -d /srv/data/username -m`

B. `homedir -m /srv/data/username`

C. `userex -m /srv/data/username`

D. `userchg -m /srv/data/username -d`

## 40. `useradd` 的哪个选项为用户添加额外的组？

A. `-g`

B. `-x`

C. `-l`

D. `-G`

## 41. 哪个命令会列出由 `<username>` 指定 cron 条目？

A. `crontab -l <username>`

B. `crontab -u <username>`

C. `cron -u <username>`

D. `cronent -u <username>`

## 42. `useradd` 的哪个选项创建的是系统用户而不是普通用户？

A. `-r`

B. `-s`

C. `-a`

D. `-S`

# 第 7 章 ■ 管理任务（领域 107） 83

## 43. 哪个文件包含组的加密密码信息？

A. `/etc/group`

B. `/etc/gshadow`

C. `/etc/gsecure`

D. `/etc/group.conf`

## 44. 哪个与 locale 相关的变量用于货币相关的本地化？

A. `LC_MONE`

B. `LC_CURRENCY`

C. `LC_MONETARY`

D. `LC_CURR`

## 45. 下列哪项最准确描述了 `groupdel` 命令的用法？

A. 你可以使用 `-f` 选项强制删除组。

B. 如果要删除用户的主组，则必须先删除该用户或更改其主组。

C. `groupdel` 可以在任何时间运行，无论组成员身份关系如何。

D. `groupdel` 的 `-r` 选项会在删除组后递归地更改用户的 GID。

## 46. 下列哪个命令显示给定的用户的 UID、主组和补充组？

A. `id`

B. `getid`

C. `passwd`

D. `chage`

## 47. `usermod` 命令的哪个选项用于更改给定用户的真实名称？

A. `-R`

B. `-n`

C. `-d`

D. `-c`

## 48. 假设你删除了一个 UID 为 1501 的用户账户，并使用了 `-r` 选项。你还应该运行哪个命令来查找可能由该用户拥的其他文件？

A. `find -id 1501`

B. `grep 1501 *`

C. `grep -u 1501 *`

D. `find / -uid 1501`

# 第 8 章

## 核心系统服务（领域 108）

本章涵盖以下 COMPTIA LINUX+/LPIC-1 考试目标：

### 108.1 维护系统时间

- 设置系统日期和时间
- 将硬件时钟设置为正确的 UTC 时间
- 配置正确的时区
- 基础 NTP 配置
- 了解 `pool.ntp.org` 服务的知识
- 对 `ntpq` 命令的了解

以下是所用文件、术语和工具的部分列表：

- `/usr/share/zoneinfo`
- `/etc/timezone`
- `/etc/localtime`
- `/etc/ntp.conf`
- `date`
- `hwclock`
- `ntpd`
- `ntpdate`
- `pool.ntp.org`

### 108.2 系统日志

- `syslog` 守护进程的配置
- 理解标准设施、优先级和操作
- `logrotate` 的配置

![](img/84990579543ce21a46ac6dc507fcde32_124_0.png)

- 对 `rsyslog` 和 `syslog-ng` 的了解
- 以下是所用文件、术语和工具的部分列表：
  - `syslog.conf`
  - `syslogd`
  - `klogd`
  - `/var/log/`
  - `logger`
  - `logrotate`
  - `/etc/logrotate.conf`
  - `/etc/logrotate.d/`
  - `journalctl`
  - `/etc/systemd/journald.conf`
  - `/var/log/journal/`

### 108.3 邮件传输代理 (MTA) 基础

- 创建邮件别名
- 配置邮件转发
- 常用 MTA 程序（`postfix`, `sendmail`, `qmail`, `exim`）的知识（不涉及配置）
- 以下是所用文件、术语和工具的部分列表：
  - `~/.forward`
  - `sendmail` 仿真层命令
  - `newaliases`
  - `mail`
  - `mailq`
  - `postfix`
  - `sendmail`
  - `exim`
  - `qmail`

![](img/84990579543ce21a46ac6dc507fcde32_125_0.png)

### 108.4 管理打印机和打印

- 基础 CUPS 配置（用于本地和远程打印机）
- 管理用户打印队列
- 排除一般的打印问题
- 从已配置的打印机队列中添加和删除作业
- 以下是所用文件、术语和工具的部分列表：
  - CUPS 配置文件、工具和程序
  - `/etc/cups`
  - `lpd` legacy接口 (`lpr`, `iprm`, `lpq`)

![](img/84990579543ce21a46ac6dc507fcde32_126_0.png)

## 49. 下列哪个命令用于检查 `systemd` journal 或日志文件？

A. `journallist`

B. `ctlj`

C. `journalctl`

D. `jctl`

## 50. 哪个系统日志设施用于来自内核的消息？

A. `syslog`

B. `kernel`

C. `kern`

D. `system`

## 51. 你可以向哪个服务器地址设置 NTP 客户端以便从区域本地服务器接收时间？

A. `127.0.0.1`

B. `192.168.1.100`

C. `ntp.example.com`

D. `pool.ntp.org`

## 52. 提供日志设施的 `systemd` 服务名称是什么？

A. `systemd-journal`

B. `systemd-loggingd`

C. `systemd-syslog`

D. `systemd-logger`

## 53. 在运行 `Postfix` 的服务器上更改邮件别名后，必须运行哪个命令？

A. `service postfix restart`

B. `newaliases`

C. `alias -n`

D. `postfix`

## 54. 在哪个目录层次结构中找到与 CUPS 打印相关的配置文件？

A. `/etc/cupsd`

B. `/etc/cups.d`

C. `/etc/CUPS`

D. `/etc/cups`

# 第 8 章 ■ 核心服务（领域 108）

## 55. CUPS 配置文件中哪个控制指令允许系统接受来自 192.168.1.1 到 192.168.1.27 的本地网络连接？

A. `Allow 192.168.1.0/25`

B. `Allow 192.168.1.0/24`

C. `Allow 127.0.0.0/8`

D. `AllowHosts 192.168.1.10`

## 56. 下列哪个命令可以在脚本中立即设置日期？

A. `ntpd`

B. `ntpdate pool.ntp.org`

C. `setime`

D. `time`

## 57. 执行 `ntp` 命令时收到“Connection refused.”通常表示什么？

A. 网络已断。

B. NTP 守护进程未运行。

C. 禁止使用 NTP。

D. 当前用户没有执行 `ntp` 的权限。

## 58. 哪个命令用于查询和操作系统上的硬件时钟？

A. `hwc`

B. `ntpdate`

C. `systime`

D. `hwclock`

## 59. 在哪个目录中找到 `qmail` 服务器上的邮件队列？

A. `/var/sp/qmail`

B. `/var/qmail/queue`

C. `/var/sp/mailq`

D. `/var/sp/qmail/queue`

## 60. 哪个 syslog 级别用于提供信息消息？

A. `kern`

B. `emerg`

C. `debug`

D. `info`

## 61. 在 `/etc/ntp.conf` 中，以下哪行设置 drift 文件的位置？

A. `drift /var/lib/ntp/drift`

B. `driftfile /var/lib/ntp/drift`

C. `drift-file /var/lib/ntp/drift`

D. `driftconfig /var/lib/ntp/drift`

## 62. `/etc/logrotate.conf` 中的哪个选项会在选定日志运行时将日志通过邮件到 `admin@example.com`？

A. `mail @example.com`

B. `sendmail @example.com`

C. `maillog @example.com`

D. `logmail @example.com`

## 63. 下列哪个命令用于确定日志文件使用的磁盘空间？

A. `journalctl --disk`

B. `journalctl --du`

C. `journalctl --usage`

D. `journalctl -ls`

## 64. 下列哪个命令显示 `Postfix` 服务器上的当前邮件队列？

A. `qmail`

B. `mailqueue`

C. `mail -q`

D. `mailq`

## 65. 运行 NTP 守护进程时，执行哪个命令可以交互模式与 NTP 服务器交互？

A. `ntpd`

B. `ntpdate`

C. `ntpq`

D. `ntp-interactive`

## 66. 假设你想将发送给 `root` 用户的邮件发送 `admin@example.com`。`/etc/aliases` 中的以下哪行可以实现此？

A. `admin@example.com -> root`

B. `root -> admin@example.com`

C. `root, admin@example.com`

D. `root: admin@example.com`

## 67. 使用 `klogd` 时，可以使用哪个选项控制记录消息的文件？

A. `-d`

B. `-f`

C. `-v`

D. `-l`

## 68. 在哪个目录中找到要用 `logrotate` 轮的各种日志配置文件？

A. `/etc/logrotate`

B. `/etc/logs`

C. `/etc/logrotate.d`

D. `/var/spool/logrotate`

## 69. 下列哪个命令将文件放入打印队列？

A. `lpr`

B. `lpd`

C. `lpq`

D. `lpx`

## 70. `sendmail` 命令的以下哪个选项会打印关于邮件队列的信息？

A. `-bi`

B. `-queue`

C. `-bp`

D. `-f`

## 71. `hwclock` 命令的哪个功能将硬件时钟设置为当前系统时间？

A. `-w`

B. `-s`

C. `-a`

D. `-m`

## 72. CUPS 管理 Web 界面的默认端口是什么？

A. `tcp/53`

B. `tcp/8080`

C. `udp/456`

D. `tcp/631`

## 73. 下列哪个命令导致 `sendmail` 尝试递送队列中的消息？

A. `sendmail -q`

B. `sendmail -b`

C. `sendmail -f`

D. `sendmail -v`

## 74. 你需要创建一个邮件地址来接收 `abuse@example.com` 的邮件。然而，你希望将垃圾报告发送到组织内的多个邮件地址。以下哪项会将发往 `abuse` 账户的邮件发送 `admin@example.com` 和 `security@example.com`？

A. 为 `abuse` 用户家目录创建转发文件并准确地转发邮件。

B. 在 `/etc/aliases` 中添加此：`admin@example.com,security@example.com`。

C. 为 `root` 创建转发文件并准确地转发邮件。

D. 在 `/etc/aliases` 中添加此：`admin@example.com\security@example.com`。

## 75. 下列哪个命令根据当前系统时间将硬件时钟设置为 UTC？

A. `hwclock --systohc --utc`

B. `hwclock --systohc --localtime`

C. `hwclock --systohc`

D. `hwclock --systoutc`

## 76. 你需要删除 `postfix` 服务器上队列中的所有消息。以下哪个命令将执行此操作？

A. `postqueue -remove`

B. `rm -rf`

C. `postfix -f`

D. `postuper -d ALL`

## 77. 下列哪个 URL 用于查看 CUPS 中已完成打印任务的列表？

A. `http://localhost:631/jobs?which_jobs=completed`

B. `http://localhost:631/completed`

C. `http://localhost:631/?completed`

D. `http://cups/jobs=completed`

## 78. `journalctl` 命令的哪个选项会在创建新条目时持续更新显示？

A. `-tail`

B. `-t`

C. `-f`

D. `-l`

# 第 8 章 ■ 核心系统服务 (领域 108)

## 79. 假设在 `rsyslog` 的配置中设置了 `$ModLoad imdup` 配置选项，那么以下哪个额外选项对于配置服务器将监听的端口是必要的？

A. `$Port 514`

B. `$UDServerRun 514`

C. `$Listen 514`

D. `$UDListen 514`

## 80. 下列哪个命令会导致在 `Postfix` 服务器上处理邮件队列？

A. `postfix -f`

B. `postfix -D`

C. `postfix -q`

D. `postuper -q`

## 81. 运行 `ntpd` 时，如果时间相对于 NTP 服务器存在偏差，服务器将不会调整或同步时间。`ntpd` 的哪个选项可以禁用此功能，并确保在存在较大偏差时也继续同步过程？

A. `ntpd -noskew`

B. `ntpd -skewcheck-off`

C. `ntpd -g 0`

D. `ntpd -s 0`

## 82. `journal.conf` 中的哪个选项控制单个日志日志的最大文件大小？

A. `SystemMaxSize`

B. `MaxFile`

C. `LogFileSize`

D. `LogSize`

## 83. 执行哪个命令可以查看已完成的打印作业？

A. `lpstat -q`

B. `lpq`

C. `lpstat -W completed`

D. `lpqueue -c`

## 84. 在配置日志轮转时，你需要执行一个命令在日志轮转后运行脚本。配置中的哪个选项可以实现这一行为？

A. `after-rotate`

B. `run-script`

C. `rotatecomplete`

D. `postrotate`

## 85. 你正在部署一个 `Exim` 服务器，并需要配合防火墙确保打开了正确的入站端口。对于正常的 SMTP 流量，你应该允许入站哪个协议和端口？

A. `TCP/23`

B. `TCP/25`

C. `TCP/110`

D. `TCP/143`

## 86. 在修改 `sendmail` 访问数据库 `/etc/access` 后，应该执行哪个命令？

A. `makemap`

B. `makeddb`

C. `newaccess`

D. `rebuilddb`

## 87. 使用 `syslog-ng` 工作时，以下哪个主配置文件的正确路径和文件名？

A. `/etc/syslog-ng/syslog-ng.conf`

B. `/etc/syslog/syslog-ng.conf`

C. `/etc/syslog-ng/syslog-ng.conf`

D. `/etc/syslog-ng/ngd.conf`

## 88. 开发者创建了一个应用程序，并希望利用 `syslog` 将日志记录到自定义日志文件中。这样的应用程序应该使用哪个设施（facility）？

A. `syslog`

B. `kern`

C. `local0`

D. `user`

## 89. 用户需要处理与打印相关的项目。下列哪个命令可以将用户（选项中称为 `username`）添加到用于此目的的组中？

A. `usermod -aG printerusers username`

B. `usermod -aG lpadmin username`

C. `usermod -gA lpadmin username`

D. `usermod -a lpadmin username`

## 90. `logrotate` 配置文件中的哪个选项会禁用日志文件的压缩？

A. `compressoff`

B. `limitcompress`

C. `nocompress`

D. `ncompress`

## 91. `date` 命令的哪个选项可以设置日期和时间？

A. `date -f`

B. `date -t`

C. `date --change`

D. `date -s`

## 92. 使用哪个命令可以收集并显示运行 `sendmail` 的服务器上处理的邮件统计信息？

A. `mailq`

B. `mailstats`

C. `statmail`

D. `sendmailstats`

## 93. 从 shell 脚本运行时，哪个命令可以启用记录到 `syslog`？

A. `logd`

B. `login`

C. `logit`

D. `logger`

## 94. 下列哪个命令可以重启运行 `systemd` 的服务器上的 CUPS？

A. `systemctl restart cups.service`

B. `systemctl restart cups`

C. `systemctl reboot cups.target`

D. `systemctl restart cups.target`



47. 在查看 `syslog` 配置时，你注意到几个日志文件前面有一个减号 (`-`)。配置中的减号有什么什么意义？

- A. 使用 `-` 表示日志可能在任何时间进行轮转。
- B. 使用 `-` 表示系统在适当时可以使用其他日志设施。
- C. 使用 `-` 省略了每个条目进入日志的同步过程。
- D. 使用 `-` 注释掉该行。

48. `CUPS` 配置文件中的哪个选项会导致守护进程在端口 `631` 上监听所有接口上？

- A. `Port 631`
- B. `Listen All:631`
- C. `Listen 127.0.0.1:631`
- D. `Port All:631`

# 第 9 章 网络基础知识

(领域 109)

本章涵盖了以下 CompTIA LINUX+/LPIC-1 考试目标：

## 109.1 互联网协议基础

- 演示网络掩码和 `CIDR` 表示法
- 了解私有地址和公共“点分点”地址的区别
- 了解常用的 `TCP` 和 `UDP` 端口（`20, 21, 22, 23, 25, 53, 80, 110, 123, 139, 143, 161, 162, 389, 443, 465, 514, 636, 993`）
- 了解 `TCP`, `ICMP`, `IPv4` 和 `IPv6` 的区别
- 了解 `IPv6` 的基本特征
- 使用的文件和工具列表：`/etc/services`, `IPv4`, `IPv6`, `子netting`, `TCP`, `UDP`

## 109.2 网络配置

- 手动和自动配置接口
- `TCP/IP` 配置
- 设置默认路由
- 使用的文件和工具列表：`/etc/hostname`, `/etc/hosts`, `/etc/nsswitch.conf`, `ifconfig`, `ip`, `ping`

## 109.3 网络故障排除

- 手动和自动配置接口和路由表，包括添加、停止或重新配置接口
- 查看或配置路由表并纠正不正确的默认路由
- 与网络配置相关的问题
- 使用的文件和工具列表：`ifconfig`, `ip`, `ifup`, `ifdown`, `route`, `host`, `hostname`, `dig`, `netstat`, `ping`, `ping6`, `traceroute`, `traceroute6`, `netcat`

## 109.4 配置 DNS

- 查询远程 `DNS` 服务器
- 配置本地解析并使用远程 `DNS` 服务器
- 修改解析的顺序
- 使用的文件和工具列表：`/etc/hosts`, `/etc/resolv.conf`, `/etc/nsswitch.conf`, `host`, `dig`, `getent`

1. 下列哪个命令在不执行 `IP` 地址查询的情况下显示当前默认路由？

   - A. `netstat -rn`
   - B. `netstat -n`
   - C. `netstat -r`
   - D. `netstat -f`

2. 你的服务器接口出现故障，且目前处于关闭状态。假设设备没有硬件故障，可以使用哪个命令和选项显示有关接口的信息？

   - A. `ifconfig -a`
   - B. `ifup`
   - C. `netstat -n`
   - D. `ifconfig`

3. 下列哪一个不作为内部、非互联网的私有地址？

   - A. `172.16.4.2`
   - B. `192.168.40.3`
   - C. `10.74.5.244`
   - D. `143.236.32.231`

4. 下列哪个命令为 `eth0` 接口添加 `192.168.1.1` 的默认网关？

   - A. `route add default gateway 192.168.1.1 eth0`
   - B. `eth0 --dg 192.168.1.1`
   - C. `route add default gw 192.168.1.1 eth0`
   - D. `route define eth0 192.168.1.1`

5. `host` 命令的哪个选项将查询特定域名的权威服务器？

   - A. `-t ns`
   - B. `-t all`
   - C. `-ns`
   - D. `-named`

6. 为了让主备名称服务器为特定域名通信，防火墙中应该开启哪些端口？

   - A. `UDP/53`
   - B. 同时 `TCP/53` 和 `UDP/53`
   - C. `TCP/53`
   - D. `UDP/53` 和 `TCP/503`

7. `ping` 命令的哪个选项允许你选择生成 `ICMP` 包的接口？

   - A. `-i`
   - B. `-I`
   - C. `-t`
   - D. `-a`

8. 你需要划分一个子网以启用四个每个最多 `30` 个主机的子网。哪种 `CIDR` 表示法的子网掩码适用于此场景？

   - A. `/25`
   - B. `/24`
   - C. `/32`
   - D. `/27`

9. 下列哪个命令查询 `example.com` 域的邮件服务器？

   - A. `dig.example.com mx`
   - B. `dig example.com`
   - C. `host -t smtp example.com`
   - D. `dig example.com smtp`

10. 下列地址代表 `IPv6` 中的 `localhost`？

    - A. `0:1`
    - B. `::1`
    - C. `127:0:1`
    - D. `:127:0:0:1`

11. `traceroute` 命令的哪个选项将使用 `TCP SYN` 包进行路径追踪？

    - A. `-T`
    - B. `-t`
    - C. `-s`
    - D. `-i`

12. 下列哪个命令将尝试开启网络配置中所有标记为自动的接口？

    - A. `ifconfig -a`
    - B. `ifup auto`
    - C. `ifup -a`
    - D. `ifstat`

13. 在脚本场景中，哪条命令将返回为服务器配置的域名？

    - A. `dnsname`
    - B. `fqdn`
    - C. `hostname`
    - D. `hostname -d`

14. 哪条命令可以监听网络上的 `netlink` 消息？

    - A. `ip monitor`
    - B. `netlink -a`
    - C. `ip netlink`
    - D. `route`

15. 如果 `traceroute6` 命令不可用，`traceroute` 命令的哪个选项可以用于 `IPv6` 跟踪路由？

    - A. `-ipv6`
    - B. `-net6`
    - C. `-v6`
    - D. `-6`

16. `/etc/nsswitch.conf` 中的以下配置行中，哪一个会导致组信息查找首先使用本地文件，然后使用 `LDAP`？

    - A. `group: files ldap`
    - B. `lookup: group [local ldap]`
    - C. `group: [local ldap]`
    - D. `group: localfiles ldap`

17. 下列哪条 `dig` 命令将 `example.com` 的查询直接发送到 `192.168.2.5` 服务器，而不是发送到本地配置的解析器？

    - A. `dig example.com @192.168.2.5`
    - B. `dig -t 192.168.2.5 example.com`
    - C. `dig -s 192.168.2.5 example.com`
    - D. `dig server=192.168.2.5 example.com`

18. `SNMP` 流量需要通过防火墙允许哪些端口？

    - A. 端口 `23` 和 `25`
    - B. 端口 `110` 和 `143`
    - C. 端口 `80` 和 `443`
    - D. 端口 `161` 和 `162`

# 第 9 章 网络基础 (领域 109)

19. 下列哪条命令将列出主机数据库？

    - A. `getent hosts`
    - B. `ghosts`
    - C. `nslookup`
    - D. `host`

20. 下列哪个子网掩码用于用 `/25` `CIDR` 表示法描述的子网？

    - A. `255.255.255.0`
    - B. `255.255.0.0`
    - C. `255.255.255.192`
    - D. `255.255.255.128`

21. 下列哪行配置将使用 `/etc/resolv.conf` 将 `DNS` 服务器设置为 `192.168.1.4`？

    - A. `dns=192.168.1.4`
    - B. `dns-server 192.168.1.4`
    - C. `nameserver 192.168.1.4`
    - D. `name-server 192.168.1.4`

22. 在检查服务器上的开放端口时，你看到 `TCP` 端口 `3000` 被列出，但没有对应的协议名称（如 `smtp`、`imaps` 等）。在哪个文件中可以找到端口到协议的转换列表，该列表可以自定义来添加此新端口？

    - A. `/etc/ports`
    - B. `/etc/p2p`
    - C. `/etc/ppp`
    - D. `/etc/services`

23. 下列哪条命令为服务器添加到 `192.168.51.0/24` 的路由，网关为 `192.168.51.1`？

    - A. `route add -net 192.168.51.0 netmask 255.255.255.0 gw 192.168.51.1`
    - B. `route add -net 192.168.51/24 gw 192.168.51.1`
    - C. `route -net 192.168.51.0/24 192.168.51.1`
    - D. `route add 192.168.51.1 -n 192.168.51.0//255.255.255.0`

24. 下列哪条命令显示当前的网络服务或套接字，以及未监听的套接字？

    - A. `netstat -a`
    - B. `netlink -a`
    - C. `sockets -f`
    - D. `opensock -l`

25. 下列哪行是 `/etc/hosts` 的正确配置行？

    - A. `192.168.1.4 cwa.braingia.org cwa`
    - B. `cwa.braingia.org cwa 192.168.1.4`
    - C. `cwa.braingia.org 192.168.1.8 alias cwa`
    - D. `alias cwa.braingia.org cwa 192.168.1.4`

26. 下列哪条命令将 `eth0` 设备配置为 `/24` 网络中的 `IP` 地址 `192.168.1.1`？

    - A. `ifconfig eth0 192.168.1.1/24`
    - B. `ifconfig eth0 192.168.1.1/255.255.255.0`
    - C. `ifconfig eth0 192.168.1.1 netmask 255.255.255.0`
    - D. `ifconfig 192.168.1.1 netmask 255.255.255.0 eth0`

27. 下列哪项描述了 `IPv4` 和 `IPv6` 之间的主要区别？

    - A. `IPv4` 用于内部网络，而 `IPv6` 用于公网。
    - B. `IPv4` 用于公网网络，而 `IPv6` 用于内部网络。
    - C. `IPv4` 使用 `32` 位地址，而 `IPv6` 使用 `128` 位地址。
    - D. 在 `IPv6` 中没有子网划分。

28. `ICMP` 在哪个端口运行？

    - A. `TCP/43`
    - B. `UDP/11`
    - C. `UDP/69`
    - D. `ICMP` 不使用端口。

29. 下列哪条命令使用 `eth0` 将默认网关设置为 `192.168.1.1`？

    - A. `ip route default 192.168.1.1`
    - B. `ip route change 192.168.1.1 dev0`
    - C. `ip route update 192.168.1.1`
    - D. `ip route default 192.168.1.1 eth0`

30. 下列哪个端口用于 `Secure Shell`？

    - A. `TCP/23`
    - B. `TCP/25`
    - C. `TCP/22`
    - D. `TCP/20`

31. 下列哪个 `netcat` 选项将在端口 `8080` 上创建一个监听服务器？

    - A. `netcat -p 8080`
    - B. `nc -l -p 8080`
    - C. `nc -p 8080`
    - D. `nc -s 8080`

32. 下列哪条命令显示 `example.com` 的起始权限（Start of Authority）？

    - A. `dig example.com soa`
    - B. `dig example.com authority`
    - C. `dig example.com -auth`
    - D. `dig -t auth example.com`

33. 假设你想通过添加 `example.com` 或 `example.org` 域名，让本地客户端完全限定网络上的主机。`/etc/resolv.conf` 中的哪个选项可以提供这一点？

    - A. `search`
    - B. `domain`
    - C. `local-domain`
    - D. `local-order`

34. 下列哪条命令向本地地址发送 `IPv6` `ping`？

    - A. `ping -6 127.0.0.1`
    - B. `ping6 /128`
    - C. `ping6 fd6:551:b0f::`
    - D. `ping -6 fd6:551:b0f:`

35. 下列哪条命令防止流量到达主机 `192.168.1.3`？

    - A. `route add -host 192.168.1.3 reject`
    - B. `route -nullroute 192.168.1.3`
    - C. `route add -null 192.168.1.3`
    - D. `route add -block 192.168.1.3`

36. 下列描述描述了 `traceroute` 和 `tracepath` 之间的主要区别？

    - A. `traceroute` 命令需要 `root` 权限。
    - B. `tracepath` 命令提供每个跳点的 `MTU`，而 `traceroute` 不提供。
    - C. `tracepath` 命令无法用于跟踪外部网络的路径。
    - D. `traceroute` 命令与 `IPv6` 不兼容。

37. 下列哪条命令将模拟 Microsoft Windows 中的 `ping` 命令，即发送四个数据包后退出？

    - A. `ping -n 4`
    - B. `ping -t 4`
    - C. `ping -p 4`
    - D. `ping -c 4`

38. 你正在使用 `dig` 命令排查 `DNS` 问题，并收到“`status: NXDOMAIN`”消息。下列哪项最能描述 `NXDOMAIN` 的含义？

    - A. `NXDOMAIN` 意味着你收到了查询的非权威回答。
    - B. `NXDOMAIN` 表示未找到域名或主机。
    - C. `NXDOMAIN` 表示查询成功。
    - D. `NXDOMAIN` 表示添加了新的记录。

39. 下列哪条命令为 `eth1` 配置 `IPv6` 地址 `fd6:551:b0e::`？

    - A. `ifconfig eth1 inet6 add fd6:551:b0e::/128`
    - B. `ifconfig add fd6:551:b0e::`
    - C. `ifconfig fd6:551:b0e::: eth1`
    - D. `ifconfig eth1 fd6:551:b0e`

40. `LDAP over SSL` 在哪个端口运行？

    - A. `Port 53`
    - B. `Port 389`
    - C. `Port 636`
    - D. `Port 443`

41. 当你需要防止本地客户端访问特定主机 `www.example.com`，而是将其重定向到本地主机时，下列哪种方法？

    - A. 为 `www.example.com` 的 `IP` 地址添加防火墙条目。
    - B. 从路由表中删除 `www.example.com`。
    - C. 为 `www.example.com` 添加空路由（null route）。
    - D. 在 `/etc/hosts` 中添加条目。

42. 在执行 `ip route change` 之后应该执行下列哪条命令？

    - A. `ip route flush`
    - B. `ip route reload`
    - C. `ip route cache`
    - D. `ip route restart`

43. 使用 `dig` 发送 `SPF` 记录查询时应该使用哪个选项？

    - A. `-t txt`
    - B. `-t spf`
    - C. `-t mx`
    - D. `-t mailspf`

44. 下列哪种协议使用三次握手？

    - A. `ICMP`
    - B. `TCP`
    - C. `UDP`
    - D. `IP`

45. `IPv4` 中 `172.16.0.0` 私有范围有多少个 `IP` 地址？

    - A. `/32`
    - B. `16,777,216`
    - C. `65,536`
    - D. `1,048,576`

46. 在排查连接问题时，你发现可以通过网页访问服务器但无法 `ping` 它。下列哪项最能描述这种场景可能的原因？

    - A. `TCP` 流量被防火墙拦截。
    - B. `DNS` 查找失败。
    - C. `ICMP` 流量被拦截。
    - D. 存在拒绝路由（reject route）。

47. 使用 `route` 命令查看可用路由时，一条路由包含标志 `UG`，而其他路由只包含 `U`。路由表中的字母 `U` 表示什么？

    - A. `G` 表示路由是良好的（good）。
    - B. `G` 表示路由不可用。
    - C. `G` 表示这是一个网关（gateway）。
    - D. `G` 表示该路由是聚合的（aggregate）。

48. 下列哪条命令从从 `192.168.1.4` 服务器请求 `example.org` 的区域传输（zone transfer）？

    - A. `dig example.org @192.168.1.4 axfr`
    - B. `dig example.org @192.168.1.4`
    - C. `dig example.org @192.168.1.4 xfer`
    - D. `dig example.org #192.168.1.4 xfer`

# 第 10 章：安全（领域 110）

本章涵盖了以下 CompTIA LINUX+/LPIC-1 考试目标：

## 110.1 执行安全管理任务

- 审计系统以设置了 `suid/sgid` 位的文件
- 设置或更改用户密码及密码有效期信息
- 能够使用 `nmap` 和 `netstat` 发现系统上的开放端口
- 对用户登录、进程和内存使用设置限制
- 确定哪些用户已登录系统或当前正在登录
- 基础的 `sudo` 配置和使用
- 以下是所用文件、术语和工具的部分列表：
  - `find`
  - `passwd`
  - `fuser`
  - `lsof`
  - `nmap`
  - `chage`
  - `netstat`
  - `sudo`
  - `/etc/sudoers`
  - `su`



* `usermod`
* `ulimit`
* `who`, `w`, `last`

### 110.2 设置主机安全

* 了解影子密码（shadow passwords）及其工作原理
* 关闭未使用的网络服务
* 理解 TCP Wrappers 的作用
* 以下是所用文件、术语和工具的部分列表：
  * `/etc/nologin`
  * `/etc/passwd`
  * `/etc/shadow`
  * `/etc/xinetd.d/*`
  * `/etc/xinetd.conf`
  * `/etc/inetd.d/*`
  * `/etc/inetd.conf`
  * `/etc/inittab`
  * `/etc/init.d/*`
  * `/etc/hosts.allow`
  * `/etc/hosts.deny`

## 110.3 使用加密保护数据

* 执行基础的 OpenSSH 2 客户端配置和使用
* 理解 OpenSSH 2 服务器主机密钥的作用
* 执行基础的 GnuPG 配置、使用和撤销
* 理解 SSH 端口隧道（包括 X11 隧道）
* 以下是所用文件、术语和工具的部分列表：
  * `ssh`
  * `ssh-keygen`
  * `ssh-agent`
  * `ssh-add`
  * `~/.ssh/id_rsa` and `id_rsa.pub`
  * `~/.ssh/id_dsa` and `id_dsa.pub`
  * `/etc/ssh/ssh_host_rsa_key` and `ssh_host_rsa_key.pub`
  * `/etc/ssh/ssh_host_dsa_key` and `ssh_host_dsa_key.pub`
  * `~/.ssh/authorized_keys`
  * `/etc/ssh/known_hosts`
  * `gpg`
  * `~/.gnupg/*`

![](img/84990579543ce21a46ac6dc507fcde32_149_0.png)

1. 你需要防止用户临时通过 `ssh` 或或其他方式登录系统。下列哪项描述了实现此任务的方法？
   A. 使用命令 `touch /etc/login`。
   B. 禁用 `sshd`。
   C. 删除 `/etc/login`。
   D. 添加影子文件。

2. 下列哪个命令在整个文件系统中查找设置了 setuid 位的文件？
   A. `find / -perm suid`
   B. `find / -perm 4000`
   C. `find / -type suid`
   D. `find / -type f -perm setuid`

3. 下列哪个命令显示当前开放的端口以及使用该端口的进程？
   A. `netstat -a`
   B. `lsof -i`
   C. `ps auxw`
   D. `netlist`

4. 你正尝试使用 `umount` 命令卸载文件系统。然而，当你执行时，收到一条消息显示文件系统正在使用。下列哪个命令可以确定哪个进程一直占用文件系统？
   A. `fuser`
   B. `ls`
   C. `find`
   D. `ps`

5. 下列哪个命令显示账户信息，如过期日期、最后更改密码日期和其他相关细节？
   A. `usermod -`
   B. `userinfo -a`
   C. `chageuser -l`
   D. `chage -l`

6. 下列哪个命令扫描 IP 地址 `192.168.1.154` 的开放端口？
   A. `nmap 192.168.1.154`
   B. `lsof 192.168.1.154`
   C. `netstat 192.168.1.154`
   D. `netmap 192.168.1.154`

7. 哪个命令用于创建供 `ssh` 使用的公/私钥对？
   A. `ssh -k`
   B. `ssh-keygen`
   C. `ssh-genkey`
   D. `ssh -key`

8. 下列哪个配置选项在 `/etc/security/limits.conf` 中为名为 `suehr` 的用户设置 25 个进程的硬限制？
   A. `suehr hard proc 25`
   B. `suehr hard proc 25 hard`
   C. `suehr hard proc-25`
   D. `proc 25 hard`

9. 你应该在哪个文件中放置你将接受密钥认证的服务器的公钥？
   A. `~/.ssh/authorized_keys`
   B. `~/.ssh/keys`
   C. `~/.ssh/key`
   D. `~/.ssh/auth`

10. 你正在工作的系统没有安装 `lsof` 命令，而且你不允许经过层层审批并提前计划安装的情况下安装软件。`netstat` 的哪个选项将显示给定端口连接的进程 ID？
    A. `-a`
    B. `-n`
    C. `-p`
    D. `-l`

11. 你需要查看 `log` 文件记录之外的登录信息。`last` 命令的哪个选项可以加载另一个文件？
    A. `-a`
    B. `-t`
    C. `-e`
    D. `-f`

12. 你需要检查谁当前登录了系统。下列哪个命令会显示这一点？
    A. `listuser`
    B. `fuser`
    C. `ls -u`
    D. `w`

13. 你需要以特定用户执行命令。下列哪个命令可以实现这一点？
    A. `sudo -u`
    B. `sudo -U`
    C. `sudo -s`
    D. `sudo -H`

14. `/etc/sudoers` 中的哪个选项会导致指定的命令不提示密码？
    A. `PASSWORD=NO`
    B. `NOPASSWD`
    C. `NOPASSWD`
    D. `NOPMPT`

15. 下列哪个命令将显示当前登录用户的运行时间、内存和其他限制？
    A. `reslimit`
    B. `limit -a`
    C. `ulimit -a`
    D. `proclimit -n`

16. `/etc/hosts.deny` 文件中的哪行将防止 `192.168.1.0/24` 内的主机访问由 `xinetd` 运行的服务？
    A. `BLOCK:192.168.1.0/24`
    B. `REJECT:192.168.1.0/24`
    C. `ALL:192.168.1.0/24`
    D. `NONE:192.168.1.0/24`

17. 使用 `usermod -e` 使账户过期时，下列哪项代表正确的日期格式？
    A. `YYYY-MM-DD`
    B. `MM/DD/YYYY`
    C. `DD/MM/YY`
    D. `MM/DD/YY HH:MM:SS`

18. `/etc/xinetd.d` 内的配置文件的哪个指令将阻止服务启动？
    A. `enable no`
    B. `start no`
    C. `disable yes`
    D. `boot no`

19. 你对 SSH 使用基于 RSA 的密钥对。默认情况下，`~/.ssh` 中的私钥文件名是什么？
    A. `id_rsa`
    B. `id_rsa.priv`
    C. `id_rsa.key`
    D. `rsa_key.priv`

20. `su` 命令的哪个选项将非交互式会话执行命令？
    A. `-s`
    B. `-u`
    C. `-c`
    D. `-e`

21. 在指定密钥服务器后，`gpg` 的哪个选项用于指定服务器密钥？
    A. `key-name`
    B. `keyname`
    C. `send-key`
    D. `sendkey`

22. 下列哪项最好描述了使用 `ssh` 在远程服务器上执行单个命令的方法？
    A. 使用 `-e` 选项跟随命令。
    B. 在命令行中作为选项之后发送命令。
    C. 使用 `--execute` 选项跟随命令。
    D. 使用 `-s` 选项跟随命令。

23. 使用 `ssh-agent` 时，哪个命令和选项列出加载的密钥？
    A. `ssh-agent -l`
    B. `ssh -l`
    C. `ssh-list-keys`
    D. `ssh-add -l`

24. 应该使用下列哪个命令编辑 `/etc/sudoers` 文件？
    A. `editsudo`
    B. `visudo`
    D. `visudo`

25. 下列哪个命令可用于基于 `systemd` 的系统防止 `httpd.service` 等服务在启动时运行？
    A. `systemctl disable httpd2service`
    B. `systemctl stop httpd.service`
    C. `systemd disable httpd.service`
    D. `systemd enable httpd.service boot=no`

26. 下列哪个命令将根据自 1970 年 1 月 1 日以来的天数设置账户过期？
    A. `passwd -e`
    B. `chage -E`
    C. `usermod -l`
    D. `chguser`

27. 你正在使用 `nmap` 扫描主机的开放端口。但服务器阻止了 ICMP 回显请求。你可以设置 `nmap` 的哪个选项来继续扫描？
    A. `-P0`
    B. `-no-ping`
    C. `-s0`
    D. `-ping-0`

28. `/etc/security/limits.conf` 中的哪个选项用于控制给定账户同时登录次数？
    A. `nlogins`
    B. `loginmax`
    C. `maxlogins`
    D. `loginlimit`

29. 哪个文件可以存储已知 ssh 密钥的服务器端缓存？
    A. `/etc/ssh_known_hosts`
    B. `/etc/ssh_known_hosts`
    C. `~/.ssh/known_hosts`
    D. `/root/ssh_known_hosts`

30. 在 `/etc/shadow` 的以下条目中，数字 15853 指什么？

```
mail:*:15853:0:99999:7:
```

    A. `mail` 用户的 UID
    B. `mail` 拥有的文件数量
    C. 最后更改密码的日期（自1970/1/1起）
    D. 账户过期的剩余天数

31. 哪一个命令设置了从本地端口 5150 到 `www.example.com` 远程端口 80 的本地端口转发会？
    - A. `ssh -L 5150:www.example.com:80`
    - B. `ssh 5150:www.example.com`
    - C. `ssh -p 5150 www.example.com`
    - D. `ssh -e 5150 www.example.com:80`

32. 为了让 X11 转发工作，目标服务器上的 `/etc/sshd_config` 必须启用哪个选项？
    - A. `XForwardward yes`
    - B. `Xenable yes`
    - C. `X11Forwarding yes`
    - D. `Xconnection yes`

33. 哪一个命令生成 GnuPG 密钥对？
    - A. `gpg --gen-key`
    - B. `gpg --key`
    - C. `gpg --send-key`
    - D. `gpg --create-key`

34. 在 `/etc/sudoers` 中，哪一个代表一个名为 `admins` 的组？
    - A. `@admins`
    - B. `admins`
    - C. `-admins`
    - D. `%admins`

35. `ssh` 的哪个选项用于设置远程主机的端口？
    - A. `-p`
    - B. `-P`
    - C. `-l`
    - D. `@`

36. `nmap` 的哪个选项设置扫描使用 TCP SYN 包来查找开放的端口？
    - A. `-sS`
    - B. `-sT`
    - C. `-sY`
    - D. `-type SYN`

37. 上一个命令使用以下哪一个日志来详细说明最近的登录情况？
    - A. `/var/log/last`
    - B. `/var/log/all.log`
    - C. `/var/log/wtmp`
    - D. `/var/log/logins`

38. `ssh` 的哪个选项启用使用密钥进行认证？
    - A. `-i`
    - B. `-k`
    - C. `-f`
    - D. `--key`

39. 在脚本场景中，你需要阻止 `sudo` 提示凭据或出于任何其他原因。`sudo` 的哪个选项用于指示这一点？
    - A. `-n`
    - B. `--noprompt`
    - C. `-i`
    - D. `-q`

40. 以下哪一个命令生成一个用于 `ssh` 的 RSA 密钥？
    - A. `ssh -key rsa`
    - B. `ssh --gen-key rsa`
    - C. `ssh-keygen -t rsa`
    - D. `ssh-keygen rsa`

41. 你需要禁用 `/etc/inetd.conf` 中找到的一个服务。在文件中，哪一个被用作注释字符？
    - A. `-`
    - B. `#`
    - C. `/`
    - D. `%`

42. 以下哪一个命令可以用于锁定账户？
    - A. `usermod -L`
    - B. `usermod -l`
    - C. `passwdlock`
    - D. `lockacct`

43. 哪一个文件被用作 `gpg` 公钥环的默认存储？
    A. `publickeys.gpg`
    B. `pubring.gpg`
    C. `public.gpg`
    D. `pubkeys.gpg`

44. `~/.gnupg` 中的哪一个文件存在时表示文件已迁移到 `gpg` 2.1 或更高版本？
    A. `.gpg-v21`
    B. `.gpg-updated`
    C. `.gpg-v21-migrated`
    D. `.gpg-files-v21`

45. 以下哪一个命令在服务器上搜索启用了 setgid 位的文件？
    A. `find / -perm 4000`
    B. `find ./ -perm setgid`
    C. `grep setgid *`
    D. `find / -perm 2000`

46. 以下哪一个命令在 Debian 系统上创建 `/etc/rc.d/*` 内的链接，用于启动和停止服务？
    A. `createsym`
    B. `startstop-service`
    C. `update-rc.d`
    D. `createateconfig`

47. 根据 `/etc/inittab` 的指示，通常用于单用户模式的运行级别是哪一个？
    A. `1`
    B. `2`
    C. `5`
    D. `6`

48. `su` 命令的哪个选项用于获取正常的登录环境？
    A. `-u`
    B. `-U`
    C. `-`
    D. `-login`

![](img/84990579543ce21a46ac6dc507fcde32_158_0.png)

## 第 11 章

## 容量规划 (主题 200)

本章涵盖了以下 LPIC-2 考试考点：

* **200.1 测量和排错资源使用**
  * 测量 CPU 使用率。
  * 测量内存使用率。
  * 测量磁盘 I/O。
  * 测量网络 I/O。
  * 测量防火墙和路由吞吐量。
  * 映射客户端带宽使用。
  * 将系统症状与可能的问题匹配/关联。
  * 估计吞吐量并识别包括网络在内的系统瓶颈。
  * 以下使用的文件、术语和工具的部分列表：
    * `iostat`
    * `iotop`
    * `vmstat`
    * `netstat`
    * `ss`
    * `iptraf`
    * `pstree`
    * `ps`
    * `lsof`
    * `top`
    * `htop`
    * `sar`
    * `swap`
    * 被 I/O 阻塞的进程
    * 输入块
    * 输出块

* **200.2 预测需求**
  * 使用监控和测量工具监控基础设施使用情况。
  * 预测容量断点。
  * 观察容量使用的增长率。
  * 绘制容量使用的趋势图。
  * 了解如 Icinga2、Nagios、collectd 和 Cacti 等监控解决方案。
  * 以下使用的文件、术语和工具的部分列表：
    * 诊断
    * 预测增长
    * 资源耗尽

![](img/84990579543ce21a46ac6dc507fcde32_160_0.png)

当使用 `iostat` 评估性能时，哪个选项显示基于分区的设备信息？
* A. `-a`
* B. `-c`
* C. `-d`
* D. `-p`

当使用 `iptraf` 通过 `ssh` 连接进行监控时，显示你的会话中所有流量的是哪一个？
* A. 区域
* B. 过滤器
* C. 排除
* D. 选择

以下哪一个用于排除/包含 `iptraf` 流量？
* A. 区域
* B. 过滤器
* C. 排除
* D. 选择

以下哪一个命令显示与 I/O 相关的输入和输出块？
* A. `ioprt`
* B. `iptraf`
* C. `vmswap`
* D. `vmstat`

以下哪一个命令可以显示基于进程的磁盘使用实时信息？
* A. `iostat`
* B. `top`
* C. `iotop`
* D. `free`

你需要部署一种能够根据可配置性能条件启用告警以及脚本响应的监控解决方案。以下哪个软件包执行这些任务？
* A. `MySQL`
* B. `ntop`
* C. `mrtg`
* D. `Nagios`

以下哪一个命令可以显示当前登录用户列表，以及平均负载和自重启以来的时间？
* A. `uptime`
* B. `w`
* C. `swap`
* D. `sysinfo`

7. 以下哪一个命令提供了当前内存使用以及交换空间及其利用率的概述？
   * A. `mem`
   * B. `free`
   * C. `pstat`
   * D. `swap`

8. 在使用 `top` 命令时，以下哪种方法排序方法使内存使用率最高的显示在列表顶部？
   * A. 在 `top` 中，按 `o` 然后选择 `mem`。
   * B. 在 `top` 中，按 `Shift+E`，滚动到 `%MEM`，按 `s` 选择并 `q`。
   * C. 在 `top` 中，按 `S` 然后选择 `mem`。
   * D. 在 `top` 中，按 `Shift+S`，选择 `%MEM`，按 `q`。

9. 以下哪一个命令可以用于显示？
   * A. `df`
   * B. `du`
   * C. `diskutil`
   * D. `diskuse`

10. 以下哪个工具可以使用 SNMP 和脚本收集用于性能绘图的数据？
    * A. `ptop`
    * B. `pstree`
    * C. `Cacti`
    * D. `Grafr`



11. 哪一个工具可以测量单个进程的内存使用率以帮助容量规划？

-   A. `ps`
-   B. `iotop`
-   C. `iostat`
-   D. `ifconfig`

12. `htop` 的哪个选项启用监控进程 ID？

-   A. `-p`
-   B. `-a`
-   C. `-e`
-   D. `-s`

13. 以下哪一个 `netstat` 选项显示每个 socket 的发送和接收队列？

-   A. `-r`
-   B. `-M`
-   C. `-a`
-   D. `-v`

14. 以下哪一个提供了一个可在 `ssh` 连接上使用的 `ncurses` 的网络监控图形工具？

-   A. `ipmon`
-   B. `iptraf`
-   C. `ipconfig`
-   D. `netmon`

15. 以下哪一个命令启用排序和分组的进程列表，并分为父/子显示？

-   A. `ps`
-   B. `psdisp`
-   C. `pstree`
-   D. `ptree`

16. 以下哪一个命令每两秒采集一次、总共 10 次 CPU 相关的性能信息？

-   A. `sar -u 2 10`
-   B. `sar -u 10 2`
-   C. `sar -u 2`
-   D. `uptime -t`

17. 以下哪一个工具提供了一个基于 `ncurses` 的进程界面，包括查看、更改优先级和杀死进程？

-   A. `htop`
-   B. `ptop`
-   C. `libtop`
-   D. `restop`

18. 使用 `vmstat` 查看统计数据时，哪一个统计量代表 CPU 等待 I/O 的时间？

-   A. `sy`
-   B. `us`
-   C. `wa`
-   D. `io`

19. `pstree` 命令的哪个选项在显示正常输出的同时显示进程 ID？

-   A. `-i`
-   B. `-b`
-   C. `-p`
-   D. `-a`

![](img/84990579543ce21a46ac6dc507fcde32_161_0.png)

20. 使用 `ps` 查看信息时，`RSS` 列表示什么？

- A. 实际交换大小 (Real Swap Size)
- B. 剩余交换空间 (Remaining Swap Space)
- C. 驻存大小 (Resident Set Size)
- D. 推荐集合大小 (Recommended Set Size)

21. 下列哪个命令可以显示当前打开的文件列表及其大小？

- A. `ls`
- B. `lsof`
- C. `lsio`
- D. `ls -o`

22. 使用 `htop` 交互式监控进程时，可以使用哪个键来显示所选进程的打开文件？

- A. `L`
- B. `j`
- C. `f`
- D. `o`

23. 在虚拟服务器环境中工作，`iostat` 中的哪一列显示了由于虚拟化程序导致的非自愿等待时间（百分比）？

- A. `proc`
- B. `wait`
- C. `user`
- D. `steal`

24. 下列哪个性能监控命令在现代安装中默认可用，且不需要作为单独包安装？

- A. `i`
- B. `top`
- C. `sar`
- D. `uptime`

25. `uptime` 命令中的三个数字代表什么时间间隔？

- A. 1, 5 和 15 分钟
- B. 5, 10 和 15 分钟
- C. 10, 30 和 60 秒
- D. 1, 3 和 5 分钟

## 第 11 章 容量规划 (Topic 200)

26. 下列哪个文件包含关于交换空间的信息，包括当前使用的量以及用于交换的磁盘分区？

- A. `/proc/swapinfo`
- B. `/proc/swaps`
- C. `/proc/swap`
- D. `/etc/swap.conf`

27. 下列哪个工具为网络相关统计数据（如每个主机的带宽占用）提供了 Web 界面？

- A. `mrt`
- B. `nag`
- C. `ntop`
- D. `htop`

28. `ps` 命令的哪个选项以宽格式显示信息？

- A. `-`
- B. `w`
- C. `a`
- D. `o`

29. 当为 `sar` 命令未提供间隔或计数时，输出显示什么信息？

- A. 自自启动以来收集的统计数据
- B. 当前负载平均值
- C. 当前利用率统计数据
- D. 平均 I/O

30. 下列哪个 `lsof` 命令将显示端口 80 的所有连接？

- A. `lsof -i 80`
- B. `lsof 80`
- C. `lsof -i :80`
- D. `lsof -i -80`

31. `iostat` 的哪个选项会导致显示以兆字节输出？

- A. `-k`
- B. `-l`
- C. `-m`
- D. `-o`

32. 使用 `vmstat` 查看信息时，你注意到 `b` 列中有两个进程指示不可中断睡眠。你如何找到哪些进程正处于不可中断睡眠模式？

- A. 为 `vmstat` 添加 `-n` 选项。
- B. 使用 `ps` 并在 `Stat` 列中查找 `D`。
- C. 使用 `ps` 并在 `Stat` 列中查找 `Sl`。
- D. 重启服务器。

33. 使用 `htop` 工作时，下列哪个选项将更新之间的延迟设置为 10 秒？

- A. `-d 10`
- B. `-d 100`
- C. `-f 10`
- D. `-f 100`

34. 下列哪个命令和选项每秒显示一次内存和 CPU 使用的性能信息，持续 10 秒？

- A. `vmstat 1 10`
- B. `iostat 10 1`
- C. `vmstat 10 1`
- D. `iostat 1 10`

35. 下列哪个命令显示内核转发的数据包数量？

- A. `ls`
- B. `ipstat`
- C. `ifconfig -a`
- D. `netstat -s`

36. 你正在使用双处理器系统，并注意到一分钟负载平均值为 1.00。这对于性能意味着什么？

- A. 其中一个处理器空闲了 50% 的时间。
- B. 系统受到 CPU 限制，因为它已达到 100% 的容量。
- C. 无法从该信息中确定 CPU 利用率。
- D. 其中一个处理器空闲了 25% 的时间。

37. 在不提供计数值的情况下向 `sar` 命令提供 0 增量值，预期输出是什么？

- A. 从很久开始的统计数据
- B. 自启动以来的平均利用率
- C. 持续更新的统计数据
- D. 会发生错误。

## 第 12 章 Linux 内核 (Topic 201)

本章涵盖了以下 LPIC-2 考试主题：

### 201.1 内核组件

- 内核 2.6.x, 3.x 和 4.x 文档
- 以下是使用的文件、术语和工具的部分列表：
    - `/usr/src/linux/`
    - `/usr/src/linux/Documentation/`
    - `zimage`
    - `bzimage`
    - `x` 压缩

### 201.2 编译 Linux 内核

- `/usr/src/linux/`
- 内核 `Makefiles`
- 内核 2.6.x, 3.x 和 4.x `make` 目标
- 定制化当前内核配置。
- 构建内核。
- 安装内核及其模块。
- 启动文件。
- 配置。
- 使用 `DKMS` 编译模块。

13. 下列哪个命令可以创建模块及其依赖项列表？

-   A. `lsmod`
-   B. `depmod`
-   C. `modlist`
-   D. `listmod`

14. 下列哪个命令用于实时查看与内核相关的 `udev` 事件？

-   A. `udevls all`
-   B. `lsudev -f`
-   C. `udevmon -a`
-   D. `udevadm monitor`

15. 下列哪个命令以树形结构显示来自内核的 USB 相关信息？

-   A. `lsusb -t`
-   B. `usblist --tree`
-   C. `usbtree`
-   D. `usblist -t`

16. `sysctl` 的哪个选项显示所有值及其当前设置？

-   A. `-a`
-   B. `-b`
-   C. `-d`
-   D. `-c`

17. 下列哪个命令可以安装内核模块，包括依赖项？

-   A. `lsmod`
-   B. `modprobe`
-   C. `modinst`
-   D. `instmod`

18. 下列哪些 `make` 目标可以创建内核镜像和相关文件的 Debian 包？

-   A. `kpkgk`
-   B. `deb-pkg`
-   C. `bin-deb`
-   D. `deb-bin`

19. 下列哪个命令用于显示当前内核版本？

-   A. `kver`
-   B. `uname -r`
-   C. `uptime -k`
-   D. `kerver`

20. `sysctl` 的名称和值存储在哪个目录层级结构中？

-   A. `/sysctl`
-   B. `/etc/sysctl.info`
-   C. `/proc/sys`
-   D. `/proc/sysctl`

21. 与 `udev` 规则存储在哪个目录层级结构中？

-   A. `/etc/udev.conf`
-   B. `/etc/udev.conf.d`
-   C. `/etc/udev/rules.d`
-   D. `/etc/udev.d`

22. 使用哪个命令来确定另一个模块所依赖的模块？

-   A. `modinfo`
-   B. `modlist`
-   C. `modprobe`
-   D. `tracemod`

23. 在哪个目录中通常可以找到与内核相关的文档？

-   A. `/usr/src/Documentation`
-   B. `/usr/share/kerneldocs`
-   C. `/usr/src/linux/Documentation`
-   D. `/usr/share/kernel/Documentation`

24. `lspci` 的哪个选项显示用于给定 PCI 设备的内核驱动程序？

-   A. `-t`
-   B. `-k`
-   C. `-n`
-   D. `-a`

25. 下列哪个命令将模块插入到运行的内核中但不解析依赖关系？

-   A. `lsmod`
-   B. `modinstall`
-   C. `insmod`
-   D. `moduleinst`

26. `modprobe` 的哪个选项会移除模块并尝试移除其依赖的任何未使用的模块？

-   A. `-v`
-   B. `-r`
-   C. `-d`
-   D. `-f`

27. 下列哪些 `make` 目标用于安装以前编译的模块？

-   A. `modules`
-   B. `modules_install`
-   C. `instmod`
-   D. `modinst`

28. 在以下哪个目录中可以找到通过 `modprobe` 加载的模块的名单信息？

-   A. `/etc/blacklist`
-   B. `/etc/modprobe.d`
-   C. `/etc/blacklist.mod`
-   D. `/etc/modprobe`

29. 下列哪个命令显示当前已加载的模块列表？

-   A. `depmod`
-   B. `depmod -a`
-   C. `lsmod`
-   D. `listmod`

30. 在 CentOS 6 系统工作时，使用哪个命令创建初始 RAM 磁盘？

-   A. `mkinit`
-   B. `dracut`
-   C. `mkraminit`
-   D. `mkinitfs`

31. 使用哪个命令从运行的系统中移除内核模块？

-   A. `modrm`
-   B. `rmmod`
-   C. `modremove`
-   D. `removemod`

32. 如果你想让通过 `sysctl` 命令设置的值在启动时生效，应该将变量及其取值放在哪个文件中？

-   A. `/etc/sysctl.cfg`
-   B. `/etc/sysctl.conf`
-   C. `/lib/sysctl`
-   D. `/var/sysctl.conf`

33. 在哪个文件中可以找到当前可用内核符号的列表？

-   A. `/proc/kernelsyms`
-   B. `/etc/kernel.conf`
-   C. `/etc/lsyms`
-   D. `/proc/kallsyms`

34. `modprobe` 的以下哪个选项将显示模块的依赖关系？

-   A. `--show-deps`
-   B. `--show-depends`
-   C. `--deps`
-   D. `--list-deps`

35. 下列哪个命令可以显示与当前加载模块相关的各种信息，包括核心大小和选项设置？

-   A. `sysctl -v -m <module>`
-   B. `modinfo -r <module>`
-   C. `lsmod <module>`
-   D. `dinf <module>`

36. 哪个目录包含关于内核的各种元素和配置信息，例如发行号、域名、`modprobe` 位置以及其他设置？

-   A. `/proc/sys/kmod`
-   B. `/proc/sys/kernel`
-   C. `/proc/kernel`
-   D. `/proc/kernel/sys`

37. 下列哪个命令显示内核缓冲区的消息？

-   A. `kring`
-   B. `ringbuf`
-   C. `dmesg`
-   D. `kmesg`

# 第 13 章 系统启动 (202)

本章涵盖以下 LPIC-2 考试主题：

### 202.1 自定义系统启动

* `Systemd`
* `SysV init`
* `Linux 规范 (LSB)`
* 以下是使用的文件、术语和工具：
    * `/usr/lib/systemd/`
    * `/etc/systemd/`
    * `/run/systemd/`
    * `systemctl`
    * `systemd-delta`
    * `/etc/inittab`
    * `/etc/init.d/`
    * `/etc/rc.d/`
    * `chkconfig`
    * `update-rc.d`
    * `init`

### 202.2 系统恢复

* `BIOS` 和 `UEFI`
* `NVMe` 启动
* `GRUB` 版本 2 和传统模式 (Legacy)
* 硬盘或可移动设备上不同的启动加载程序安装位置。
* 标准启动加载程序选项和启动加载程序 `shell`。
* 使用 `systemd` 救援和紧急模式。
* 以下是使用的文件、术语和工具：
    * `mount`
    * `fsck`
    * `initab`, `telinit` 和 `SysV init`
    * `/boot/`，`/boot/grub/` 和 `/boot/efi/`
    * `EFI` 系统分区 (ESP)
    * `GRUB`
    * `grub shell`
    * 启动加载程序的启动并交给内核
    * 内核加载
    * 硬件初始化和设置
    * `daemon`/`service` initialization and setup

### 202.3 替代启动加载程序

* `syslinux`, `PXE`
* 理解 `BIOS` 和 `UEFI`
* 以下是使用的文件、术语：
    * `syslinux`
    * `pxelinux`
    * `efiboot`
    * `systemd`

1. 创建的 `systemd` unit 文件应该存储在哪个目录中？

-   A. `/etc`
-   B. `/systemd`
-   C. `/usr/share`
-   D. `/share/system`

2. 在修改 `systemd` 后，应该执行以下哪个命令使更改生效？

-   A. `systemd`
-   B. `reboot`
-   C. `systemctl`
-   D. `systemctl`

3. 下列哪个文件包含系统的运行级别（runlevels）？

-   A. `/etc/runlevels`
-   B. `/etc/inittab`
-   C. `/etc/rc`
-   D. `runlevels`

4. 哪个启动加载程序可以用于 FAT 系统？

-   A. `SYSBOOT`
-   B. `SYLINUX`
-   C. `TIELINUX`
-   D. `FATLINUX`

5. `EFI` 系统分区 (ESP) 使用什么文件系统类型？

-   A. `FAT`
-   B. `EXT`
-   C. `NTFS`
-   D. `EXT3`

6. 下列哪个用于为继续启动过程所需的内核驱动程序提供早期文件系统加载？

-   A. `bootrd`
-   B. `driverload`
-   C. `initrd`
-   D. `initdrv`

7. 启动系统时，收到类似于“未找到 init”的错误，然后进入 `initramfs` 提示符。你需要检查硬盘是否有错误。下列哪个命令对硬盘分区执行错误检查？

-   A. `defrag`
-   B. `fsck`
-   C. `checkfs`
-   D. `chkfs`

8. 下列哪个命令将系统置于单用户模式？

-   A. `telinit 1`
-   B. `chgin 1`
-   C. `telinit 1`
-   D. `telinit 1`

9. 下列哪个命令将 `extlinux` 安装到 `/boot` 分区？

-   A. `extlinux --install /boot`
-   B. `extlinux --inst /boot`
-   C. `extlinux -boot`
-   D. `extlinux /boot install`

10. 下列哪个命令在 `/boot` 分区中挂载 `/dev/sda1`？

-   A. `mount /dev/sda /boot`
-   B. `mount /boot /dev/sda1`
-   C. `mount /dev/sda1 /boot`
-   D. `mount -dev sda1 /boot`

11. 下列哪个命令将 `GRUB` 安装到第一块 SATA 硬盘的主引导记录 (MBR) 中？

-   A. `grub-install /dev/hda`
-   B. `grub-install /dev/sda`
-   C. `grub-install /dev/hd0,0`



# 144 Part II • LPIC-2

-   D. `grub -i /dev/hda`

12. 下列哪个命令更改下次启动的启动顺序？

-   A. `efibootmgr -c`
-   B. `efibootmgr -b -B`
-   C. `efibootmgr -o`
-   D. `efibootmgr -n`

13. 哪种引导程序可以用于 `ISO9660` `CD-ROM`？

-   A. `ISOLINUX`
-   B. `EFIBOOT`
-   C. `ISOFS`
-   D. `BOOTISO`

14. 安装的软件包将 `systemd` 文件放置在哪个目录下？

-   A. `/usr/lib/systemd/user`
-   B. `/usr/lib/systemd/system`
-   C. `/etc/systemd`
-   D. `/etc/system`

15. 使用 `UEFI` 时，下列哪个文件可以作为引导程序？

-   A. `shim.efi`
-   B. `shim.efi`
-   C. `shim.fx`
-   D. `efi.shim`

16. 下列哪项描述了 `systemd` 配置文件的优先级顺序？

-   A. `/etc` 中的文件、`/run` 中的文件，然后是 `/lib` 中的文件
-   B. `/run` 中的文件、`/etc` 中的文件，然后是 `/lib` 中的文件
-   C. `/lib` 中的文件、`/run` 中的文件，然后是 `/etc` 中的文件
-   D. `/lib` 中的文件、`/etc` 中的文件，然后是 `/run` 中的文件

17. 在基于 `SysV init` 的系统中，哪个目录包含用于启动和停止服务的脚本？

-   A. `/etc/rc.int`
-   B. `/etc/boot`
-   C. `/etc/bootscripts`
-   D. `/etc/init.d`

18. 下列哪个命令用于在基于 `systemd` 的系统中查找覆盖的配置文件？

-   A. `diff systemctl -diff`
-   B. `systemd-delta`
-   C. `systemctl configoverride`

19. 在 Red Hat 系统级上，下列哪个命令列出了所有设置为在启动时执行的文件以及它们在每个运行级别下的设置？

-   A. `rlevel`
-   B. `chkconfig --list`
-   C. `bootldr --list`
-   D. `init --bootlist`

# 第13章 ■ 系统启动 (主题 202)

20. 在 `UEFI shell` 中执行的下列哪个命令控制引导配置？

-   A. `bootcfg`
-   B. `bcfg`
-   C. `grub-install`
-   D. `grcfg`

21. 下列哪个项被识别为磁盘上存储磁盘分区和操作系统位置信息的初始区？

-   A. 最小引导记录 (MBR)
-   B. 主引导记录 (MBR)
-   C. 扇区
-   D. 主分区表 (MPT)

22. 启动后，`EFI` 引导程序挂载在哪个目录下？

-   A. `/boot/efi`
-   B. `/etc/boot/efi`
-   C. `/etc/efi`
-   D. `/boot/loader`

23. 基于 `systemd` 的系统可以设置为哪个目标以辅助帮助恢复？

-   A. `recovery.target`
-   B. `recover.target`
-   C. `target.recover`
-   D. `rescue.target`

24. 下列哪个配置文件用于 `ISOLINUX`？

-   A. `isolinux.cfg`
-   B. `isolinux.conf`
-   C. `isolin.cfg`
-   D. `isolinux.conf.d`

25. 对于使用 `PXELUX` 作为引导程序的系统，`TFTP` 服务器上的 `/tftpboot` 必须存在哪个文件？

-   A. `pxelinux.tftp`
-   B. `pxelinux.boot`
-   C. `pxelinux.conf`
-   D. `pxelinux.0`

26. 在 Debian 或 Ubuntu 系统上可以使用哪个工具来管理 `SysV init` 脚本，例如将它们设置为在启动时运行？

-   A. `bootordder`
-   B. `bootloader`
-   C. `configchk`
-   D. `update-rc-d`

27. 在操作系统选择菜单期间按下哪个键可以启用编辑与 `GRUB` 启动相关的参数？

-   A. `v`
-   B. `e`
-   C. `r`
-   D. `y`

28. 下列哪个命令显示基于 `systemd` 系统的默认目标？

-   A. `systemctl list-unit-default`
-   B. `systemctl get-unit-default`
-   C. `systemctl get-unit-default`
-   D. `systemctl get-default-unit`

29. `fsck` 命令的哪些选项会查找错误并自动假设它应该修复发现的错误？

-   A. `-ry`
-   B. `-vy`
-   C. `-my`
-   D. `-xy`

30. `grub-install` 的哪个选项会将 `GRUB` 镜像放在备用目录中？

-   A. `--boot-dir`
-   B. `-b`
-   C. `--boot`
-   D. `--boot-directory`

31. `systemctl` 子命令用于切换运行级别？

-   A. `switch`
-   B. `move`
-   C. `runlevel`
-   D. `isolate`

# 第13章 ■ 系统启动 (主题 202)

32. 检查 `/etc/inittab` 文件时，哪个选项表示系统启动的默认运行级别？

-   A. `default`
-   B. `defaultboot`
-   C. `initdefault`
-   D. `defaultit`

33. 下列哪项替代 `initrd` 为关键驱动程序提供早期文件系统？

-   A. `initnext`
-   B. `initramfs`
-   C. `initialize`
-   D. `initfs`

34. 下列哪个命令将默认 `systemd` 目标设置为多用户（`multi-user`）？

-   A. `systemctl set-default multi-user.target`
-   B. `systemd set-default multi-user.target`
-   C. `systemctl set-def muser.target`
-   D. `systemd set-def muser.target`

35. 使用 `shim` 引导基于 `UEFI` 的系统，下列文件在 `shim.efi` 之后加载？

-   A. `grubx64.cfg`
-   B. `grub.conf`
-   C. `grubx64.efi`
-   D. `efi.boot`

36. `/etc/init.d` 中的文件在哪个层次结构中链接，以便在 `SysV` 系统的各个运行级别执行这些文件？

-   A. `/etc/rc.S`
-   B. `/etc/rc`
-   D. `/etc/init.d`

37. `systemd` 系统启动的目标名称是什么？

-   A. `recovery.target`
-   B. `recover.target`
-   C. `target.recover`
-   D. `rescue.target`

# 第 14 章 ■ 文件系统与设备（主题 203）

14. `ummount` 命令的哪种选项会导致它仅卸载指定类型的文件系统？

-   A. `-v`
-   B. `-f`
-   C. `-t`
-   D. `-a`

15. 哪个命令会促使未写入的数据立即写入磁盘？

-   A. `write`
-   B. `wrnow`
-   C. `connwrite`
-   D. `sync`

16. 哪个命令用于用于激活系统上的交换空间（`swap space`）？

-   A. `mkswap`
-   B. `swapon`
-   C. `swapact`
-   D. `actswap`

17. `xfs_check` 命令的哪个选项用于验证存储在文件中的文件系统？

-   A. `-v`
-   B. `-a`
-   C. `-f`
-   D. `-d`

18. `debugfs` 的哪个选项会导致文件系统以读写模式打开而非默认的只读模式？

-   A. `-rw`
-   B. `-w`
-   C. `-r`
-   D. `-n`

19. 哪个守护进程负责监控与自监控、分析和报告技术（`SMART`）兼容的硬盘？

-   A. `smartmon`
-   B. `smarty`
-   C. `sartd`
-   D. `smartd`

20. `fsck` 命令的哪个选项会导致即使在文件系统明显被标记为“已清理”（`clean`）的情况下运行检查？

-   A. `-f`
-   B. `-m`
-   C. `-a`
-   D. `-c`

21. 你正在执行 `xfsrestore`。该 `xfsdump` 是以 `4M` 的块大小执行的。你需要在 `xfsrestore` 中调用哪个选项以便使其成功地使用该转储文件？

-   A. `-b 4M`
-   B. `-g 1M`
-   C. `-i 1M`
-   D. `-k 1024K`

22. 你在 `/etc/fstab` 中使用了 `defaults` 单词。哪些选项包含在 `defaults` 中？

-   A. `ro, exec, auto`
-   B. `rw, suid, dev, dev, auto, nouser, async`
-   C. `rw, exec, auto, nouser, async`
-   D. `rw, exec, nouser, async, noauto, suid`

23. 下列哪个命令用于管理和配置 `SMART` 监控的执行？

-   A. `smartmon`
-   B. `smartd`
-   C. `smartctl`
-   D. `smartctl`

24. 下列 `/etc/fstab` 中文件系统的正确格式是？

-   A. `<filesystem> <mountpoint> <type> <options> <dump> <pass>`
-   B. `<mountpoint> <filesystem> <type> <options> <dump> <pass>`
-   C. `<mountpoint> <filesystem> <type> <options> <pass> <dump>`
-   D. `<filesystem> <mountpoint> <type> <dump> <pass> <options>`

25. `LUKS` 使用哪种密钥派生函数？

-   A. `PBKDF2`
-   B. `SSL`
-   C. `RSA`
-   D. `DSA`

26. 下列哪个命令创建 `btrfs` 子卷（`subvolume`）？

-   A. `btrfs create subvolume`
-   B. `btrfs subvolume create`
-   C. `btrfs sv create`
-   D. `btrfs svcreate`

27. 下列 `xfsdump` 的哪个选项设置了包含在转储文件中最大大小？

-   A. `-p`
-   B. `-s`
-   C. `-z`
-   D. `-b`

28. `tune2fs` 命令的哪个选项设置了发生文件系统错误时的行为？

-   A. `-f`
-   B. `-d ''`
-   C. `-e`
-   D. `-k`

29. `/etc` 文件系统已挂载为只读以进行恢复过程。你需要挂载另一个分区。`mount` 命令的哪个选项会导致它不写入 `/etc/mtab`？

-   A. `-a`
-   B. `-m`
-   C. `-b`
-   D. `-n`

30. 下列哪个命令禁用交换空间？

-   A. `swapoff`
-   B. `swap -off`
-   C. `unmountswap`
-   D. `uswap`

31. 在 `systemd` 挂载单元（`mount unit`）的 `[mount]` 部分，哪个指令指定了所选文件系统的挂载位置？

-   A. `Where=`
-   B. `Location=`
-   C. `List=`
-   D. `Dest=`

32. 下列哪个交换选项显示交换空间大小及其已用空间的信息？

-   A. `--list`
-   B. `-a`
-   C. `--show`
-   D. `-h`

33. 下列哪个命令可以格式化 `FAT` 文件系统？

-   A. `mkfs.fat`
-   B. `mkfs -f`
-   C. `mkfs --fat`
-   D. `mkfat`

34. 下列哪个命令为现有的 `ext3` 文件系统添加日志（`journal`）？

-   A. `tune2fs -jrn`
-   B. `e2fs -x`
-   C. `tune3fs`
-   D. `tune2fs -j`

35. 下列哪个命令创建 `btrfs` 子卷快照？

-   A. `btrfs subvolume snapshot`
-   B. `btrfs snapshot --create`
-   C. `btrfs snapshot`
-   D. `btrfs --create`

36. `xfs_repair` 的哪个选项将强制清零日志，即使日志中存在元数据？

-   A. `-L`
-   B. `-v`
-   C. `-d`
-   D. `-V`

37. 下列哪个命令以只读模式挂载文件系统？

-   A. `mount read-only`
-   B. `mount`
-   C. `-ro`
-   D. `mount`

19. 下列哪个层次结构包含光纤通道（`Fibre Channel`）的 `WWN` 等信息？

-   A. `/sys/class/wwn`
-   B. `/sys/class/fc_host`
-   C. `/sys/class/fclist`
-   D. `/sys/class/wwn`

20. `mdadm` 的哪个选项用于创建新数组？

-   A. `--create`
-   B. `--start`
-   C. `--begin`
-   D. `--construct`

21. 下列哪个文件被用作 `iscsid` 的配置文件？

-   A. `iscsid.cfg`
-   B. `iscsid.conf`
-   C. `iscsidaemon.conf`
-   D. `iscsi.cfg`

22. 在下列哪个目录中可以找到逻辑卷的信息？

-   A. `/dev/lvinfo`
-   B. `/dev/map`
-   C. `/dev/mapper`
-   D. `/dev/lvmap`

23. `mdadm` 的哪个选项监控 `RAID` 阵列的异常情况？

-   A. `--mon`
-   B. `--watch`
-   C. `--monitor`
-   D. `--examine`

24. 在排查故障的 `md RAID` 阵列时，你需要以只读模式挂载其中一个驱动器。哪个选项会将驱动器映射为只读？

-   A. `-o ro`
-   B. `read-only`
-   C. `-o rw`
-   D. `-op ro`

25. 下列哪个命令使用 `LVM` 创建逻辑卷？

-   A. `lvc`
-   B. `lvcreate`
-   C. `lvlist`
-   D. `lvmake`

26. 在监控模式下运行 `mdadm` 时，`/etc/mdadm.conf` 中的哪个选项用于在发现问题时设置邮件接收地址？

-   A. `MAILTO`
-   B. `MAILADDR`
-   C. `MAILFROM`
-   D. `MAILDEST`

27. 下列哪个命令用于查找参与 `LVM` 配置的物理卷和卷组？

-   A. `vgscan`
-   B. `lvscan`
-   C. `lvlist`
-   D. `pvlist`

28. 使用哪种分区类型来表示软件 `RAID` 阵列（例如用 `mdadm` 构建的阵列）？

-   A. `0xmd`
-   B. `-x-`
-   C. `0xRD`
-   D. `0xFD`

29. 下列哪个命令用于显示参与 `LVM` 的物理卷列表？

-   A. `pvdisp`
-   B. `pvlist`
-   C. `pvscan`
-   D. `pvmm`

30. `multipathd` 命令的哪个选项将进入交互式控制台？

-   A. `-c`
-   B. `-k`
-   C. `-f`
-   D. `-n`

31. `lvchname` 的哪个选项设置逻辑卷是否可用？

-   A. `-a`
-   B. `-b`
-   C. `-c`
-   D. `-d`

32. 在使用 `vgscan` 时，可以在哪个文件中为设备配置过滤器？

-   A. `lvm.conf`
-   B. `vg.conf`
-   C. `vgscan.conf`
-   D. `lv.cfg`

33. `lvcreate` 的哪个选项会创建逻辑卷的快照？

-   A. `snap`
-   B. `snapshot`
-   C. `ss`
-   D. 快照不通过 `lvcreate` 创建。

34. 给 `sysctl` 的哪个选项用于更改其中一个内核参数？

-   A. `-a`
-   B. `-k`
-   C. `-w`
-   D. `-A`

35. 下列哪个命令用于访问和更改 `SCSI` 设备的值？

-   A. `scsiparm`
-   B. `scsiparam`
-   C. `sdlist`
-   D. `sdparm`

36. 下列哪个目录包含 Linux 上光纤以太网（`FCoE`）的配置信息？

-   A. `/etc/fcoe`
-   B. `/etc/fc`
-   C. `/etc/fibredev`
-   D. `/fc`

37. 下列哪个命令将检查基于 `NVMe` 的设备的 `PCI` 子系统？

-   A. `psnvme`
-   B. `lsnvme`
-   C. `lspci | grep scsi`
-   D. `lspci | grep -i nvme`

# 第16 章

## 网络配置 (Topic205)

LPIC-2 考试涵盖以下主题：

### 205.1 基础网络配置

-   配置和操作以太网接口的工具
-   配置无线网络访问
-   以下是使用的文件、术语和工具的部分列表：
    -   `ip`
    -   `ifconfig`
    -   `route`
    -   `arp`
    -   `iw`
    -   `iwconfig`
    -   `iwlist`

### 205.2 高级网络配置

-   管理路由表的工具
-   配置和操作以太网接口的工具
-   分析网络设备状态的工具 `img/84990579543ce21a466dc507fcde32_204_0.png`
-   监控和分析 `TCP/IP` 流量的工具



以下是使用的文件、术语和工具的部分列表：

- `ip`
- `ifconfig`
- `route`
- `ss`
- `netstat`
- `lsof`
- `ping`, `ping6`
- `nc`
- `tcpdump`
- `nmap`

### 205.3 网络故障排除

- 访问限制
- 配置和操作以太网接口的工具
- 管理路由表的工具
- 列出网络状态的工具
- 获取网络配置信息的工具
- 已识别设备
- 系统初始化文件（`Systemd` 和 `SysV init`）
- `NetworkManager` 及其对网络配置的影响

![](img/84990579543ce21a466dc507fcde32_205_0.png)

以下是使用的文件、术语和工具的部分列表：

- `ip`
- `ifconfig`
- `route`
- `ss`
- `netstat`
- `/etc/network/`, `/etc/sysconfig/network-scripts/`
- `ping`, `ping6`
- `traceroute`, `traceroute6`
- `mtr`
- `hostname`
- 如 `/var/log/syslog`, `/var/log/messages` 等系统日志
- `dmesg`
- `/etc/resolv.conf`
- `/etc/hosts`
- `/etc/hostname`
- `/etc/hosts.allow`, `/etc/hosts.deny`

![](img/84990579543ce21a466dc507fcde32_206_0.png)

1. 使用 `ip` 命令时，如果没有指定，默认使用哪种协议族？
    - A. `TCPIP`
    - B. `IP`
    - C. `INET`
    - D. `ARP`

2. 下列哪个命令更改 `eth0` 的 MAC 地址？
    - A. `ifmac eth`
    - B. `ifconfig eth0 ether`
    - C. `ifconfig eth0 mac`
    - D. `ifconfig eth0 hw`

3. 你正在使用 `route` 命令查看路由。但名称解析花费了很时间导致命令延迟。应该添加哪个选项使其不执行名称解析？
    - A. `-d`
    - B. `-e`
    - C. `-f`
    - D. `-n`

4. 你替换了网络上的设备但使用了另一个设备的 IP 地址。运行哪个命令可以从计算机中删除 MAC 条目以便重新进行地址解析？
    - A. `arp -d`
    - B. `netstat -rn`
    - C. `hostname.dig`

5. 下列哪个命令显示无线设备 `wlan0` 的链路状态等信息？
    - A. `iw dev wlan0`
    - B. `wlan0 list`
    - C. `iw wlan0 -l`
    - D. `iw dev link`

6. 哪个命令用于设置无线设备的 `ssid`、通道和其他选项？
    - A. `ifconfig`
    - B. `iwconfig`
    - C. `wlancfg`
    - D. `ifconf`

# 第 16 章 · 网络配置 (Topic 205)

7. 下列哪个命令可以扫描可用的无线网络？
    - A. `iwlist get`
    - B. `iwconfig scan`
    - C. `iwlist scan`
    - D. `iw-scan`

8. 在解析 `ip` 命令的输出时，设置哪个选项可以移除换行符以便将输出传递给 `grep` 命令？
    - A. `-n`
    - B. `-o`
    - C. `-l`
    - D. `-f`

9. 你需要为网络接口设置特定的 MTU 值。`ifconfig` 的哪个选项可以实现此功能？
    - A. `-mtu`
    - B. `mtu`
    - C. `metric`
    - D. `addrmtu`

10. 下列哪个命令为网络 `172.16.3.0/24` 创建拒绝（reject）路由？
    - A. `route del 172.16.3.0/24`
    - B. `route add -net 172.16.3.0 netmask 255.255.255.0 reject`
    - C. `route del -net 172.16.3.0 netmask 255.255.255.0`
    - D. `route del default`

11. 使用 `arp` 命令时，为给定的 IP 地址和 MAC 地址创建新条目？
    - A. `-s`
    - B. `-c`
    - C. `-d`
    - D. `--add`

12. 下列哪个命令显示网络套接及其分配内存？
    - A. `ss -m`
    - B. `mpas`
    - C. `mem`
    - D. `free`

13. `netstat` 的哪些选项显示活动和监听的 TCP 套接及连接？
    - A. `-tu`
    - B. `-f`
    - C. `-an`
    - D. `-ta`

14. 下列哪个命令列出所有非 bind 用户的文件？
    - A. `lssof -i`
    - B. `lssof -u bind`
    - C. `lssof -u ^bind`
    - D. `lssof | grep bind`

15. 在排查潜在硬件问题时，你需要确定哪个物理接口用于地址。一种方法是使用 `ping` 命令监控设备的指示灯。`ping` 的哪个选项会向接口泛发 `ECHO_REQUEST` 数据包？
    - A. `-e`
    - B. `-a`
    - C. `-c`
    - D. `-f`

16. 下列哪个命令可以用于在 TCP 层而不是 Telnet 测试网络连接性？
    - A. `netstat`
    - B. `nc`
    - C. `nettest`
    - D. `ping`

17. `tcpdump` 的哪个选项显示供 `tcpdump` 操作的可用接口列表？
    - A. `-a`
    - B. `-d`
    - C. `-D`
    - D. `-i`

18. `nmap` 的哪个选项会使其始终执行名称解析？
    - A. `-n`
    - B. `-R`
    - C. `-b`
    - D. `-a`

19. 哪种命令提供了为 IPv6 发 ICMP 请求的方法？
    - A. `ping6`
    - B. `pingv6`
    - C. `tracert`
    - D. `6ping`

20. 下列哪个命令显示计算机当前使用的地址信息（特别是 IPv6 地址）？
    - A. `ip addr`
    - B. `ip -6 addr`
    - C. `ip6add`
    - D. `ipv6addr`

21. 下列哪个命令会禁用 `eth0` 接口上的 ARP？
    - A. `ifconfig eth0 -arp`
    - B. `ip -eth0 no-arp`
    - C. `ifconfig eth0 noarp`
    - D. `if eth0 disable arp`

22. `route` 命令的哪个选项会强制内核使用指定的设备进行路由，而不是尝试确定正确的设备？
    - A. `inet`
    - B. `addr`
    - C. `dev`
    - D. `device`

23. `ss` 命令的哪个选项会显示与套接相关的进程 ID (`PID`)？
    - A. `-l`
    - B. `-a`
    - C. `-p`
    - D. `-f`

24. `netstat` 的哪个选项以类表格格式显示接口信息，这可能适用于脚本编写？
    - A. `-i`
    - B. `-r`
    - C. `-t`
    - D. `-l`

25. 在 Debian 系统中，在哪个目录结构下可以找到配置信息以及用于在接口启动或关闭时运行脚本的目录？
    - A. `/etc/netconf`
    - B. `/etc/netconfig`
    - C. `/etc/net.conf.d`
    - D. `/etc/network`

26. `traceroute` 的哪个选项会导致命令使用 ICMP 进行请求？
    - A. `-T`
    - B. `-A`
    - C. `-I`
    - D. `-i`

27. 下列哪个命令提供了主机之间路由的实时追踪，近近实时地更新每个跳数的信息？
    - A. `traceroute --live`
    - B. `mtr`
    - C. `route -update`
    - D. `liveroute`

28. `hostname` 命令内部使用了哪个程序化函数？
    - A. `getaddr`
    - B. `gethost`
    - C. `gethostname`
    - D. `getname`

29. 下列哪个命令会检查系统日志以获取 DHCP 活动的信息？
    - A. `grep -i dhcp /var/log/syslog`
    - B. `grep -v dhcp /var/log/syslog`
    - C. `grep -vi dhcp /var/log/kern.log`
    - D. `dmesg | grep dhcp`

30. 下列哪些字符对于 `/etc/hosts` 中的主机名是有效的？
    - A. 数字字母、减号、下划线和点
    - B. 数字字母、减号和点
    - C. 数字字母和点
    - D. 数字字母

31. `/etc/resolv.conf` 中的下列哪行配置可以启用调试功能？
    - A. `debug`
    - B. `options debug`
    - C. `option debug`
    - D. `enable-debug`

32. `dmesg` 的哪个选项在读取一次后清除内容？
    - A. `-C`
    - B. `-c`
    - C. `-a`
    - D. `-e`

33. 下列哪个命令查看 `NetworkManager` 单元的 systemd 日志？
    - A. `systemd NetworkManager`
    - B. `systemd NetworkCtl`
    - C. `systemctl NetworkManager`
    - D. `systemctl -u NetworkManager`

34. 启动时读取哪个文件来设置本地计算机的主机名？
    - A. `/etc/hostname`
    - B. `/etc/hosts`
    - C. `/etc/localhost`
    - D. `/etc/networkhost`

35. Red Hat 系统上的下列哪个目录包含网络接口配置信息？
    - A. `/etc/network-scripts`
    - B. `/etc/system/network`
    - C. `/etc/sysconfig/network-scripts`
    - D. `/etc/sysconfig/net.d`

36. 哪个 `traceroute` 命令专门用于 IPv6 路由追踪？
    - A. `trace6`
    - B. `traceroute6`
    - C. `tracert6`
    - D. `trace`

37. 在 `/etc/hosts.allow` 中可以使用哪个通配符来指定名称与其 IP 地址不匹配的主机？
    - A. `*`
    - B. `ALL`
    - C. `PARANOID`
    - D. `NAMEMATCH`

# 第 17 章

# 系统维护 (主题 206)

本章涵盖了以下 LPIC-2 考试主题：

- 206.1 使用常用的压缩和归档工具解包源码。
- 理解调用 `make` 编译程序的基础知识。
- 向配置 脚本应用参数。
- 了解源代码默认的存储位置。
- 以下是所用文件、术语和工具的部分列表：
    - `/usr/src/`
    - `gunzip`
    - `gzip`
    - `bzip2`
    - `xz`
    - `tar`
    - `configure`
    - `make`
    - `uname`
    - `install`
    - `patch`

![](img/84990579543ce21a466dc507fcde32_214_0.png)

## 206.2 备份操作

- 了解必须包含在备份中的目录。
- 了解 `Amanda`、`Bacula`、`Bareos` 和 `BackupPC` 等网络备份解决方案。
- 了解磁带、光、磁盘或其他备份介的优缺点。
- 执行部分备份和手动备份。
- 验证备份文件的完整性。
- 部分或完全恢复备份。
- 以下是所用文件、术语和工具的部分列表：
    - `/bin/sh`
    - `dd`
    - `tar`
    - `/dev/st*` 和 `/dev/nst*`
    - `mt`
    - `rsync`

## 206.3 通知用户系统相关问题

- 通过登录消息与用户自动通信。
- 通知活动用户系统维护工作。
- 以下是所用文件、术语和工具的部分列表：
    - `/etc/issue`
    - `/etc/issue.net`
    - `/etc/motd`
    - `wall`
    - `shutdown`
    - `systemctl`

![](img/84990579543ce21a466dc507fcde32_215_0.png)

# 第 17 章 ■ 系统维护 (主题 206)

25. `rsync` 命令的哪个选项更改了确定文件修改的精度？
    - A. `--mod-time`
    - B. `--modify-time`
    - C. `--mod-res`
    - D. `--modify-window`

26. `patch` 命令的哪个选项会为正在补丁的文件创建备份？
    - A. `-r`
    - B. `-b`
    - C. `-l`
    - D. `-a`

27. `make` 命令的哪个目标（通常在大多数项目的 `Makefile` 中）会将编译后的文件放置到最终位置，并执行其他操作（如使适当的文件具有可执行权限）？
    - A. `list`
    - B. `distclean`
    - C. `run`
    - D. `install`

28. `tar` 命令的哪个选项表示 `xz` 压缩？
    - A. `-x`
    - B. `-c`
    - C. `-J`
    - D. `-j`

29. `rsync` 命令的哪个选项仅检查文件大小作为确定文件是否应该同步的手段？
    - A. `--filesize`
    - B. `--size-only`
    - C. `--list-size`
    - D. `--file-size`

30. 以下 `xz` 选项中用于解压文件并将解压内容发送到 `STDOUT` 的哪个？
    - A. `--decompress --stdout`
    - B. `--deout`
    - C. `--uncomp --stdout`
    - D. `-out -u`

# 182 第二部分 • LPIC-2

31. `bzip2` 的以下选项中哪个将输出发送到 `STDOUT`？
    - A. `-s`
    - B. `-c`
    - C. `-d`
    - D. `-f`

32. 下列哪个文件通常用作 `Bacula Director` 配置文件？
    - A. `/etc/bacula/bacula.cfg`
    - B. `/etc/bacula.cfg`
    - C. `/etc/bacula-dir.conf`
    - D. `/etc/bacula/bacula-dir.conf`

33. 使用 `mt` 命令时，下列哪个命令可以回退磁带？
    - A. `mt reverse`
    - B. `mt rewind`
    - C. `mt goback`
    - D. `mt operation=back`

34. 下列关机命令会在 15 分钟后重启系统？
    - A. `shutdown -r +15`
    - B. `shutdown +15`
    - C. `shutdown -15`
    - D. `shutdown -r 00:15`

35. `gzip` 命令的哪个选项将抑制所有警告信息，并且在输出不合适的情况下可能很有用？
    - A. `-v`
    - B. `-q`
    - C. `-L`
    - D. `-r`

36. `rsync` 的哪个选项指定同步过程的远程外壳或传输应使用 `SSH`？
    - A. `-t ssh`
    - B. `--overssh`
    - C. `-e ssh`
    - D. `-F ssh`

37. `configure` 脚本的哪个选项通常会生成命令的可用选项列表？
    - A. `--list`
    - B. `--help`
    - C. `--show`
    - D. `--get`

# 第 18 章

# 域名服务器

(主题 207)

本章涵盖了以下 LPIC-2 考试主题：

- 207.1 基础 DNS 服务器配置
    - `BIND 9.x` 配置文件、术语和实用程序
    - 在 `BIND` 配置文件中定义 `BIND` 区域文件的位置
    - 重新加载修改后的配置和区域文件
    - 了解 `dnsmasq`、`djbdns` 和 `PowerDNS` 作为备名服务器
    - 以下是使用的文件、术语和实用程序的部分列表：
        - `/etc/named.conf`
        - `/var/named/`
        - `rndc`
        - `named-checkconf`
        - `kill`
        - `host`
        - `dig`

- 207.2 创建和维护 DNS 区域
    - `BIND 9` 配置文件、术语和实用程序
    - 从 DNS 服务器请求信息的实用程序
    - `BIND` 区域文件的布局、内容和文件位置
    - 在区域文件中添加新主机的各种方法，包括反向区域

![](img/84990579543ce21a46ac6dc507fcde32_222_0.png)

![](img/84990579543ce21a46ac6dc507fcde32_223_0.png)

- 以下是使用的文件、术语和实用程序的部分列表：
    - `/var/named/`
    - 区域文件语法
    - 资源记录格式
    - `named-checkzone`
    - `named-compilezone`
    - `masterfile-format`
    - `dig`
    - `nslookup`
    - `host`

### 207.3 保护 DNS 服务器

- `BIND 9` 配置文件
- 配置 `BIND` 运行在 `chroot` 监狱中
- 使用 `forwarders` 语句对 `BIND` 进行拆分配置
- 配置和使用事务签名 (`TSIG`)
- 了解 `DNSSEC` 和基础工具
- 了解 `DANE` 和相关记录
- 以下是使用的文件、术语和实用程序的部分列表：
    - `/etc/named.conf/`
    - `/etc/named.conf`



`/etc/passwd`

`DNSSEC`

`dnssec-keygen`

`dnssec-signzone`

# 第 18 章 ■ 域名服务器 (主题 207) 185

1. 哪个配置文件用作 `BIND` 服务器的默认配置？

   A. `named.conf`
   B. `named.cfg`
   C. `bind.cfg`
   D. `bind.conf`

2. `BIND` 配置中的哪个指令指定允许查询的地址或网络？

   A. `query-addresses`
   B. `allow-query`
   C. `query-allow`
   D. `query-auth`

3. `kill` 命令的哪个信号可以用于指示 `BIND` 应该重新加载配置？

   A. `-15`
   B. `-1`
   C. `-9`
   D. `-2`

4. `dnssec-keygen` 的哪个选项指定密钥使用的算法？

   A. `-a`
   B. `-n`
   C. `-d`
   D. `-e`

5. 下列哪项描述了 `named-compilezone` 和 `named-checkzone` 的基本区别？

   A. `named-checkzone` 和 `named-compilezone` 事情。
   B. `named-checkzone` 检查区域错误，并将输出发送到文件。
   C. `named-checkzone` 执行语法检查，而 `named-compilezone` 将区域转换为不同的格式。
   D. `named-checkzone` 执行语法检查，而 `named-compilezone` 为使用 `BIND` 准备区域。

6. 在创建 `MX` 记录时，下列哪个优先级最高？

   A. `0`
   B. `10`
   C. `20`
   D. `100`

# 第二部分 ■ LPIC-2

7. 区域传输请求在哪个协议和端口上发送？

   A. `UDP/53`
   B. `ICMP/53`
   C. `TCP/143`
   D. `TCP/53`

8. `BIND` 的区域文件存储在下列哪个目录中？

   A. `/var/named`
   B. `/etc/named`
   C. `/var/cache`
   D. `/var/namedzones`

9. 下列哪个命令用于控制 `BIND` 服务器？

   A. `bind-config`
   B. `named-config`
   C. `rndc`
   D. `rdmc`

10. `dig` 命令可以使用哪种类型来测试区域传输？

    A. `xfr`
    B. `transfer`
    C. `zxfr`
    D. `axfr`

11. `BIND` 配置中的哪个指令设置守护进程监听的 IP 地址？

    A. `listeners`
    B. `listen-on`
    C. `listen-in`
    D. `ip-listeners`

12. 在为 `chroot` 场景配置 `BIND` 时，应该在下列哪个文件中为 `chroot` 用户设置主目录？

    A. `/etc/bind.home`
    B. `/etc/bind.user`
    C. `/etc/passwd`
    D. `/etc/bindauth`

13. 哪个命令用于为 `DNSSEC` 签名区域？

    A. `dnssec-signzone`
    B. `signzone`
    C. `bind-signzone`
    D. `dnssec-sign`

# 第 18 章 ■ 域名服务器 (主题 207) 187

14. `host` 命令的哪个选项将查询类型设置为 `ANY`？

    A. `-a`
    B. `-b`
    C. `-c`
    D. `-d`

15. 下列哪项正确地在主机名和 `host web.example.com` 之间创建了 `CNAME` 记录？

    A. `www CNAME web.example.com`
    B. `web.example.com CNAME www`
    C. `www IN CNAME web.example.com.`
    D. `www IN CNAME web.example.com`

16. `BIND forward` 指令的哪个选项将服务器设置为转发服务器？

    A. `only`
    B. `first`
    C. `now`
    D. `required`

17. 当运行递归名称服务器时，下列哪个选项拒绝提供来自给定地址的回答？

    A. `deny-hosts`
    B. `blackhole`
    C. `deny-query`
    D. `deny-answer`

18. 下列哪个是安装 `djbdns` 的先决条件？

    A. `bind9`
    B. `daemontools`
    C. `qmail`
    D. `bind-tools`

19. 哪个命令可以验证 `BIND` 配置文件有效？

    A. `bind9-ver`
    B. `bind-check`
    C. `config-check`
    D. `named-checkconf`

20. 下列哪个 `TTL` 值代表八小时？

    A. `8`
    B. `480`
    C. `28800`
    D. `86400`

21. 假设有以下 `BIND` 区域文件部分，值 `1800` 代表什么？

```
@ IN SOA cwa.example.org. root.example.org. (
201607400
3600
1800
604800
86400
)
```

    A. `Refresh`
    B. `Retry`
    C. `Default TTL`
    D. `Serial`

22. 哪种资源记录类型用于 `SPF` 记录？

    A. `SPF`
    B. `MX`
    C. `TXT`
    D. `MAIL`

23. 下列哪项定义了一个优先级为 `10` 的 `MX` 记录？

    A. `MX 10 mail.example.com.`
    B. `10 MX mail.example.com.`
    C. `mail.example.com 10 MX`
    D. `mail.example.com MX 10`

24. 在哪个哪个文件中可以为 `dig` 命令创建每个用户的默认设置？

    A. `/etc/dig.cfg`
    B. `/etc/dig.conf`
    C. `~/.digrc`
    D. `~/.dig.conf`

25. `mount` 命令的哪个选项有助于方便在 `chroot` 环境中运行 `BIND`？

    A. `--bind`
    B. `--chroot`
    C. `--lift`
    D. `--secure`

26. 在设置递归名称服务器时，根根提示文件（root hints file）设置的是哪种类型的区域？

    - A. 主节点 (Master)
    - B. 从节点 (Slave)
    - C. 递归 (Recurse)
    - D. 提示 (Hint)

27. 对 `DNS` 区域进行更改后，可以使用以下哪个命令重新加载区域使更改生效？

    - A. `rndc reload`
    - B. `rndc restart-zones`
    - C. `rndc zone-reload`
    - D. `rndc-rel`

28. `BIND` 区域配置中的哪个配置选项指定了允许请求区域传输的主机？

    - A. `allow-axfr`
    - B. `allow-xfr`
    - C. `allow-trans`
    - D. `allow-record`

29. 哪种 `DNS` 记录用于指定 `POP3` 服务器？

    - A. `POP`
    - B. `PO`
    - C. `MX`
    - D. 没有针对 `POP3` 服务器的特定类型。

30. `BIND` 配置中的哪个指令允许指定允许使用服务器进行递归查询的主机或网络？

    - A. `allow-recurs`
    - B. `allow-recursive`
    - C. `allow-recursion`
    - D. `allow-rec`

31. 下列哪项是 `named-checkzone` 命令的正确格式？

    - A. `named-checkzone <zone> <zonefile>`
    - B. `named-checkzone -z <zone>`
    - C. `named-checkzone -f <zonefile>`
    - D. `named-checkzone <zonefile> <zone>`

## 190 第二部分 ■ LPIC-2

32. 使用 `dnssec-keygen` 生成密钥时，`rndc` 认证 必须使用哪种算法？

    - A. `sha1`
    - B. `sha256`
    - C. `md5`
    - D. `hmac-md5`

33. 下列哪条配置指令告诉 `BIND` 不要公布其版本号？

    - A. `allow-version { none }`
    - B. `version none;`
    - C. `allow-query-version { none; }`
    - D. `query-version no;`

34. `named-checkconf` 的哪个选项用于对配置文件中列出的所有主区域进行测试？

    - A. `-l`
    - B. `-f`
    - C. `-z`
    - D. `-d`

35. 你在区域中的一个单独记录中指定 `TTL` 为 `300`，而区域本身具有 `86400` 的默认 `TTL`。当你在重启 `BIND` 后，对该单独记录进行更改，需要多长时间更改才能传播到外部解析器？

    - A. 最长 `86400` 秒
    - B. 最长 `300` 秒
    - C. 重启后更改立即生效。
    - D. 从所提供的信息无法判断。

36. 下列哪个包分别在 `Debian` 和 `Red Hat` 上安装 `PowerDNS` 权威名称服务器？

    - A. `Debian` 上的 `pdns-server` 和 `Red Hat` 上的 `pdns`
    - B. `Debian` 上的 `pdns` 和 `Red Hat` 上的 `pdns-server`
    - C. `Debian` 和 `Red Hat` 上均使用 `pdns`
    - D. `Debian` 和 `Red Hat` 上均使用 `pdns-server`

37. 下列哪个命令可以重启 `BIND` 服务器，使 `named.conf` 文件的更改生效？

    - A. `rndc reload`
    - B. `rndc reconfig`
    - C. `named reboot`
    - D. `restart bind`

# HTTP 服务

## (主题 208)

本章涵盖了以下 `LPIC-2` 考试主题：

- 208.1 基础 `Apache` 配置
  - `Apache` 2.4 配置、术语和工具
  - `Apache` 日志文件配置和内容
  - 访问限制方法和文件
  - `mod_perl` 和 `PHP` 配置
  - 客户端用户身份认证文件和工具
  - 最大请求数、最小和最大服务器及客户端的配置
  - `Apache` 2.4 虚拟主机实现（带和不带专用 IP 地址）
  - 在 `Apache` 配置中使用重定向语句（`redirect`）来自定义文件访问
  - 以下是所用文件、术语和工具的部分列表：
    - 访问日志和错误日志
    - `.htaccess`
    - `httpd.conf`
    - `mod_auth_basic`, `mod_authz_host` 和 `mod_access_compat`
    - `htpasswd`
    - `AuthUserFile`, `AuthGroupFile`
    - `apachectl`, `apache2`
    - `httpd`, `apache2`

- 208.2 `HTTPS` 的 `Apache` 配置
  - `SSL` 配置、工具和实用
  - 为商业 `CA` 生成服务器私钥和 `CSR`
  ![](img/84990579543ce21a46ac6dc507fcde32_230_0.png)
  - 生成自签名证书
  - 安装密钥和证书，包括中间 `CA`
  - 使用 `SNI` 配置虚拟主机
  - 了解虚拟主机和 `SSL` 使用中的问题
  - `SSL` 使用过程中的安全问题，禁用不安全的协议和加密算法
  - 以下是所用文件、术语和工具的部分列表：
    - `Apache2` 配置文件
    - `/etc/ssl/`, `/etc/pki/`
    - `openssl`, `CA.pl`
    - `SSLEngine`, `SSLCertificateKeyFile`, `SSLCertificateFile`, `SSLCertificatePath`
    - `SSLProtocol`, `SSLCipherSuite`, `ServerTokens`, `TraceEnable`

- 208.3 `Squid` 的配置
  - `SSL` 配置文件、工具和实用
  - 为商业 `CA` 生成服务器私钥和 `CSR`
  - 生成自签名证书
  - 安装密钥和证书，包括中间 `CA`
  - 使用 `SNI` 配置虚拟主机
  - 了解虚拟主机和 `SSL` 使用中的问题
  - `SSL` 使用过程中的安全问题，禁用不安全的协议和加密算法
  - 以下是所用文件、术语和工具的部分列表：
    - `Apache2` 配置文件
    - `/etc/ssl/`, `/etc/pki/`
    - `openssl`, `CA.pl`
    - `SSLEngine`, `SSLCertificateKeyFile`, `SSLCertificateFile`, `SSLCertificatePath`
    - `SSLProtocol`, `SSLCipherSuite`, `ServerTokens`, `TraceEnable`

- 208.4 作为反代理的 `Squid`
  - `SSL` 配置文件、工具和实用
  - 为商业 `CA` 生成服务器私钥和 `CSR`
  - 生成自签名证书
  - 安装密钥和证书，包括中间 `CA`
  - 使用 `SNI` 配置虚拟主机
  - 了解虚拟主机和 `SSL` 使用中的问题
  - `SSL` 使用过程中的安全问题，禁用不安全的协议和加密算法
  - 以下是所用文件、术语和工具的部分列表：
    - `Apache2` 配置文件
    - `/etc/ssl/`, `/etc/pki/`
    - `openssl`, `CA.pl`
    - `SSLEngine`, `SSLCertificateKeyFile`, `SSLCertificateFile`, `SSLCertificatePath`
    - `SSLProtocol`, `SSLCipherSuite`, `ServerTokens`, `TraceEnable`

- 208.5 作为反代理的 `Nginx`
  - `Nginx` 配置
  - `SSL` 配置文件、工具和实用
  - 为商业 `CA` 生成服务器私钥和 `CSR`
  - 生成自签名证书
  - 安装密钥和证书，包括中间 `CA`
  - 使用 `SNI` 配置虚拟主机
  - 了解虚拟主机和 `SSL` 使用中的问题
  - `SSL` 使用过程中的安全问题，禁用不安全的协议和加密算法
  - 以下是所用文件、术语和工具的部分列表：
    - `Apache2` 配置文件
    - `/etc/ssl/`, `/etc/pki/`
    - `openssl`, `CA.pl`
    - `SSLEngine`, `SSLCertificateKeyFile`, `SSLCertificateFile`, `SSLCertificatePath`
    - `SSLProtocol`, `SSLCipherSuite`, `ServerTokens`, `TraceEnable`

# 域名解析服务器 (主题 207)

1. 在设置递归名称服务器时，根根提示文件（root hints file）设置的是哪种类型的区域？
   - A. 主节点
   - B. 从节点
   - C. 递归
   - D. 提示

2. 对 `DNS` 区域进行更改后，可以使用以下哪个命令重新加载区域使更改生效？
   - A. `rndc reload`
   - B. `rndc restart-zones`
   - C. `rndc zone-reload`
   - D. `rndc-rel`

3. `BIND` 区域配置中的哪个配置选项指定了允许请求区域传输（`zone transfer`）的主机？
   - A. `allow-axfr`
   - B. `allow-xfr`
   - C. `allow-trans`
   - D. `allow-record`

4. 哪种 `DNS` 记录用于指定 `POP3` 服务器？
   - A. `POP`
   - B. `PO`
   - C. `MX`
   - D. 没有针对 `POP3` 服务器的特定类型。

5. `BIND` 配置中的哪个指令允许指定允许使用服务器进行递归查询的主机或网络？
   - A. `allow-recurs`
   - B. `allow-recursive`
   - C. `allow-recursion`
   - D. `allow-rec`

6. 下列哪项是 `named-checkzone` 命令的正确格式？
   - A. `named-checkzone <zone> <zonefile>`
   - B. `named-checkzone -z <zone>`
   - C. `named-checkzone -f <zonefile>`
   - D. `named-checkzone <zonefile> <zone>`

7. 使用 `dnssec-keygen` 生成密钥时，`rndc` 认证 必须使用哪种算法？
   - A. `sha1`
   - B. `sha256`
   - C. `md5`
   - D. `hmac-md5`

8. 下列哪条配置指令告诉 `BIND` 不要公布其版本号？
   - A. `allow-version { none }`
   - B. `version none;`
   - C. `allow-query-version { none; }`
   - D. `query-version no;`

9. `named-checkconf` 的哪个选项用于对配置文件中列出的所有主区域进行测试？
   - A. `-l`
   - B. `-f`
   - C. `-z`
   - D. `-d`

10. 你在区域中的一个单独记录中指定 `TTL` 为 `300`，而区域本身具有 `86400` 的默认 `TTL`。当你在重启 `BIND` 后，对该单独记录进行更改，需要多长时间更改才能传播到外部解析器？
    - A. 最长 `86400` 秒
    - B. 最长 `300` 秒
    - C. 重启后更改立即生效。
    - D. 从所提供的信息无法判断。

11. 下列哪个包分别在 `Debian` 和 `Red Hat` 上安装 `PowerDNS` 权威名称服务器？
    - A. `Debian` 上的 `pdns-server` 和 `Red Hat` 上的 `pdns`
    - B. `Debian` 上的 `pdns` 和 `Red Hat` 上的 `pdns-server`



- C. Debian 和 Red Hat 上均使用 `pdns`

- D. Debian 和 Red Hat 上均使用 `pdns-server`

12. 下列哪个命令可以重启 `BIND` 服务器，使 `named.conf` 文件的更改生效？

- A. `rndc reload`

- B. `rndc reconfig`

- C. `named reboot`

- D. `restart bind`

## HTTP 服务

（主题 208）

本章涵盖了以下 LPIC-2 考试主题：

- 208.1 基础 Apache 配置

  - Apache 2.4 配置文件、术语和工具

  - Apache 日志文件配置和内容

  - 访问限制方法和文件

  - `mod_perl` 和 PHP 配置

  - 客户端用户身份认证文件和工具

  - 最大请求数、最小和最大服务器及客户端的配置

  - Apache 2.4 虚拟主机实现（带和不带专用 IP 地址）

  - 在 Apache 配置中使用重定向语句来自定义文件访问

  - 以下是所用文件、术语和工具的部分列表：

    - 访问日志和错误日志

    - `.htaccess`

    - `httpd.conf`

    - `mod_auth_basic`, `mod_authz_host` 和 `mod_access_compat`

    - `htpasswd`

    - `AuthUserFile`, `AuthGroupFile`

    - `apachectl`, `apache2`

    - `httpd`, `apache2`

- 208.2 HTTPS 的 Apache 配置

  - SSL 配置文件、工具和实用

  - 为商业 CA 生成服务器私钥和 CSR

  ![](img/84990579543ce21a46ac6dc507fcde32_230_0.png)

  - 生成自签名证书

  - 安装密钥和证书，包括中间 CA

  - 使用 SNI 配置虚拟主机

  - 了解虚拟主机和 SSL 使用中的问题

  - SSL 使用过程中的安全问题，禁用不安全的协议和加密算法

  - 以下是所用文件、术语和工具的部分列表：

  - Apache2 配置文件

  - `/etc/ssl/`, `/etc/pki/`

  - `openssl`, `CA.pl`

  - `SSLEngine`, `SSLCertificateKeyFile`, `SSLCertificateFile`, `SSLCertificatePath`

  - `SSLProtocol`, `SSLCipherSuite`, `ServerTokens`, `TraceEnable`

- 208.3 Squid 的配置

  - SSL 配置配置文件、工具和实用

  - 为商业 CA 生成服务器私钥和 CSR

  - 生成自签名证书

  - 安装密钥和证书，包括中间 CA

  - 使用 SNI 配置虚拟主机

  - 了解虚拟主机和 SSL 使用中的问题

  - SSL 使用过程中的安全问题，禁用不安全的协议和加密算法

  - 以下是所用文件、术语和工具的部分列表：

  - Apache2 配置文件

  - `/etc/ssl/`, `/etc/pki/`

  - `openssl`, `CA.pl`

  - `SSLEngine`, `SSLCertificateKeyFile`, `SSLCertificateFile`, `SSLCertificatePath`

  - `SSLProtocol`, `SSLCipherSuite`, `ServerTokens`, `TraceEnable`

- 208.4 作为反代理的 Squid

  - SSL 配置配置文件、工具和实用

  - 为商业 CA 生成服务器私钥和 CSR

  - 生成自签名证书

  - 安装密钥和证书，包括中间 CA

  - 使用 SNI 配置虚拟主机

  - 了解虚拟主机和 SSL 使用中的问题

  - SSL 使用过程中的安全问题，禁用不安全的协议和加密算法

  - 以下是所用文件、术语和工具的部分列表：

  - Apache2 配置文件

  - `/etc/ssl/`, `/etc/pki/`

  - `openssl`, `CA.pl`

  - `SSLEngine`, `SSLCertificateKeyFile`, `SSLCertificateFile`, `SSLCertificatePath`

  - `SSLProtocol`, `SSLCipherSuite`, `ServerTokens`, `TraceEnable`

- 208.5 作为反代理的 Nginx

  - Nginx 配置

  - SSL 配置配置文件、工具和实用

  - 为商业 CA 生成服务器私钥和 CSR

  - 生成自签名证书

  - 安装密钥和证书，包括中间 CA

  - 使用 SNI 配置虚拟主机

  - 了解虚拟主机和 SSL 使用中的问题

  - SSL 使用过程中的安全问题，禁用不安全的协议和加密算法

  - 以下是所用文件、术语和工具的部分列表：

  - Apache2 配置文件

  - `/etc/ssl/`, `/etc/pki/`

  - `openssl`, `CA.pl`

  - `SSLEngine`, `SSLCertificateKeyFile`, `SSLCertificateFile`, `SSLCertificatePath`

  - `SSLProtocol`, `SSLCipherSuite`, `ServerTokens`, `TraceEnable`

## 域名解析服务器（主题 207）

1. 在设置递归名称服务器时，根根提示文件（root hints file）设置的是哪种类型的区域？

- A. 主节点

- B. 从节点

- C. 递归

- D. 提示

2. 对 DNS 区域进行更改后，可以使用以下哪个命令重新加载区域使更改生效？

- A. `rndc reload`

- B. `rndc restart-zones`

- C. `rndc zone-reload`

- D. `rndc-rel`

3. `BIND` 区域配置中的哪个配置选项指定了允许请求区域传输（zone transfer）的主机？

- A. `allow-axfr`

- B. `allow-xfr`

- C. `allow-trans`

- D. `allow-record`

4. 哪种 DNS 记录用于指定 POP3 服务器？

- A. `POP`

- B. `PO`

- C. `MX`

- D. 没有针对 POP3 服务器的特定类型。

5. `BIND` 配置中的哪个指令允许指定允许使用服务器进行递归查询的主机或网络？

- A. `allow-recurs`

- B. `allow-recursive`

- C. `allow-recursion`

- D. `allow-rec`

6. 下列哪项是 `named-checkzone` 命令的正确格式？

- A. `named-checkzone <zone> <zonefile>`

- B. `named-checkzone -z <zone>`

- C. `named-checkzone -f <zonefile>`

- D. `named-checkzone <zonefile> <zone>`

7. 使用 `dnssec-keygen` 生成密钥时，`rndc` 认证必须使用哪种算法？

- A. `sha1`

- B. `sha256`

- C. `md5`

- D. `hmac-md5`

8. 下列哪条配置指令告诉 `BIND` 不要公布其版本号？

- A. `allow-version { none }`

- B. `version none;`

- C. `allow-query-version { none; }`

- D. `query-version no;`

9. `named-checkconf` 的哪个选项用于对配置文件中列出的所有主区域进行测试？

- A. `-l`

- B. `-f`

- C. `-z`

- D. `-d`

10. 你在区域中的一个单独记录中指定 `TTL` 为 300，而区域本身具有 86400 的默认 `TTL`。当你在重启 `BIND` 后，对该单独记录进行更改，需要多长时间更改才能传播到外部解析器？

- A. 最长 86400 秒

- B. 最长 300 秒

- C. 重启后更改立即生效。

- D. 从所提供的信息无法判断。

11. 下列哪个包分别在 Debian 和 Red Hat 上安装 `PowerDNS` 权威名称服务器？

- A. Debian 上的 `pdns-server` 和 Red Hat 上的 `pdns`

- B. Debian 上的 `pdns` 和 Red Hat 上的 `pdns-server`

- C. Debian 和 Red Hat 上均使用 `pdns`

- D. Debian 和 Red Hat 上均使用 `pdns-server`

12. 下列哪个命令可以重启 `BIND` 服务器，使 `named.conf` 文件的更改生效？

- A. `rndc reload`

- B. `rndc reconfig`

- C. `named reboot`

- D. `restart bind`

19. 以下哪一个 `RedirectMatch` 指令会在用户尝试查看 `.git` 目录时向用户提供“页面未找到”（Page Not Found）错误？

- A. `RedirectMatch 404 /\.git(/|$)`

- B. `RedirectMatch PageNotFound /.git/`

- C. `RedirectMatch 404 .git`

- D. `RedirectMatch .git 404`

20. Apache 配置中的以下哪一个指令告诉服务器 SSL 私钥的路径？



- A. `SSLKeyFile`

- B. `SSLCertificatePrivateKey`

- C. `SSLCertificateKeyFile`

- D. `SSLPrivateKey`

21. Squid 默认在哪个端口上监听？

- A. `3000`

- B. `3128`

- C. `5150`

- D. `10300`

22. 以下哪一个模块提供了根据主机名或 IP 地址为 Apache 授权？

- A. `mod_auth_ipaddress`

- B. `mod_auth_host`

- C. `mod_authz_host`

- D. `mod_auth_dns`

23. Apache 在哪一个日志文件中记录对服务器的请求？

- A. `access_log`

- B. `access-log`

- C. `access.txt`

- D. `syslog`

24. Squid 配置中的哪一个指令决定了给定的 ACL 是否可以使用代理？

- A. `access_allow`

- B. `http_access`

- C. `proxy_access`

- D. `enable_access`

25. 以下哪行 Apache 配置将 `.htaccess` 文件的名称更改为 `.htaccesslist`？

- A. `Access .accesslist`

- B. `AccessFile .accesslist`

- C. `AccessFileName ".accesslist"`

- D. `AuthFile ".accesslist"`

# 第 19 章 HTTP 服务 (主题 208)

26. 根据 Apache 文档，与用户认证相关的指令的优选位置是：

A. 在 `.htaccess` 文件内

B. 在主服务器配置内

C. 在 `mod_rewrite` 块内

D. 在用户认证的专用模块中

27. 哪一个 Apache 配置指令还启用了基于组的授权？

A. `AuthGroups`

B. `AuthGroupList`

C. `AuthGrouping`

D. `AuthGroupFile`

28. 以下哪一个命令显示 Apache 服务器的当前状态，包括正在处理的请求数和服务器运行时间？

A. `apachectl status`

B. `apachectl status`

C. `apachectl faststatus`

D. `apachectl stats`

29. 当 Apache 内的 `TraceEnable` 设置为 `off` 时，返回哪种 HTTP 状态码？

A. `405`

B. `100`

C. `302`

D. `200`

30. `htpasswd` 的哪一个选项会创建凭据文件并在其中添加一个新条目？

A. `-f`

B. `-b`

C. `-c`

D. `-e`

31. 使用哪一个 Apache 服务器日志格式序列来记录处理请求所花费的时间（以微秒为单位）？

A. `%D`

B. `%T`

C. `%t`

D. `-m`

32. 以下哪行配置行使目录 `/home/web/docs` 可以在服务器的 `/documentation/` 路径下可用？

- A. `Connect /documentation /home/web/docs`

- B. `Alias /documentation/ /home/web/docs/`

- C. `Connect /home/web/docs /documentation/`

- D. `Alias ~docs/ <Location> stanza`

33. 在 `<location>` 块中，Apache 中的哪一个指令表示 `mod_perl` 将用于该位置的资源？

- A. `Handler mod_perl`

- B. `SetHandler perl-script`

- C. `SetHandler mod_perl`

- D. `LoadModule perl-script`

34. nginx 配置中哪一个指令用于为给定位置设置透传代理（pass-through proxy）？

- A. `pass-through`

- B. `proxy`

- C. `proxy_pass`

- D. `proxypass`

35. 哪一个配置指令决定了初始启动 Apache 子服务器进程的数量？

- A. `Servers`

- B. `MaxServers`

- C. `StartServers`

- D. `ServerStarts`

36. 哪一个 Apache 指令设置日志文件的格式，包括日志文件中记录了哪些元素？

- A. `LogFile`

- B. `Format`

- C. `LoggingDirective`

- D. `LogFormat`

37. `.htaccess` 文件中的哪一个选项仅允许共享组的用户访问？

- A. `Require sharing`

- B. `RequireUser sharing`

- C. `Require user sharing`

- D. `AllowOnly sharing`

# 第 20 章 文件共享

(主题 209)

本章涵盖了以下 LPIC-2 考试主题：

## 209.1 Samba 服务器配置

- Samba 4 文档
- Samba 4 配置文件
- Samba 4 工具、实用程序和守护进程
- 在 Linux 上挂载 CIFS 共享
- 将 Windows 用户名映射到 Linux 用户名
- 用户级、共享级和 AD 安全
- 以下是所用文件、术语和实用程序的部分列表：
  - `smbd`, `nmbd`, `winbindd`
  - `smbcontrol`, `smbstatus`, `testparm`, `smbpasswd`, `nmblookup`
  - `samba-tool`
  - `net`
  - `smbclient`
  - `mount.cifs`
  - `mount.cifs`

## 209.2 NFS 配置

- NFS 服务器配置
- NFS 配置文件
- NFS 工具和实用程序
- 在 Linux 上挂载 NFS 共享
- 将主机名映射到 Linux 用户名
- 用户级、共享级和安全性
- 以下是所用文件、术语和实用程序的部分列表：
  - `exports`
  - `showmount`
  - `rpcinfo`
  - `fstab`

# 第 20 章 文件共享 (主题 209)

1. 在哪一个文件中可以找到 Samba 4 的配置？

A. `/etc/`

B. `/var/`

C. `/home/`

D. `/root/`

2. 哪一个守护进程负责响应 NetBIOS 请求？

A. `smbd`

B. `nmbd`

C. `winbindd`

D. `samba`

3. 在 `samba.conf` 中修改了配置后，使用哪一个命令可以重新加载？

A. `service restart`

B. `service restart`

C. `service reload`

D. `service restart all`

4. Squid 配置中的哪一个指令决定特定的 ACL 是否可以使用代理？

A. `access_allow`

B. `http_access`

C. `proxy_access`

D. `enable_access`

5. 以下哪行 Apache 配置将 `.htaccess` 文件的名称更改为 `.htaccesslist`？

A. `Access .accesslist`

B. `AccessFile .accesslist`

C. `AccessFileName ".accesslist"`

D. `AuthFile ".accesslist"`

6. 根据 Apache 文档，与用户认证相关的指令的优选位置是：

A. 在 `.htaccess` 文件内

B. 在主服务器配置内

C. 在 `mod_rewrite` 块内

D. 在用户认证的专用模块中

7. 哪一个 Apache 配置指令还启用了基于组的授权？

A. `AuthGroups`

B. `AuthGroupList`

C. `AuthGrouping`

D. `AuthGroupFile`

8. 以下哪一个命令显示 Apache 服务器的当前状态，包括正在处理的请求数和服务器运行时间？

A. `apachectl status`

B. `apachectl status`

C. `apachectl faststatus`

D. `apachectl stats`

9. 当 Apache 内的 `TraceEnable` 设置为 `off` 时，返回哪种 HTTP 状态码？

A. `405`

B. `100`

C. `302`

D. `200`

10. `htpasswd` 的哪一个选项会创建凭据文件并在其中添加一个新条目？

A. `-f`

B. `-b`

C. `-c`

D. `-e`

11. 使用哪一个 Apache 服务器日志格式序列来记录处理请求所花费的时间（以微秒为单位）？

A. `%D`

B. `%T`

C. `%t`

D. `-m`

12. 以下哪行配置行使目录 `/home/web/docs` 可以在服务器的 `/documentation/` 路径下可用？

- A. `Connect /documentation /home/web/docs`

- B. `Alias /documentation/ /home/web/docs/`

- C. `Connect /home/web/docs /documentation/`

- D. `Alias ~docs/ <Location> stanza`

13. 在 `<location>` 块中，Apache 中的哪一个指令表示 `mod_perl` 将用于该位置的资源？

- A. `Handler mod_perl`

- B. `SetHandler perl-script`

- C. `SetHandler mod_perl`

- D. `LoadModule perl-script`

14. nginx 配置中哪一个指令用于为给定位置设置透传代理（pass-through proxy）？

- A. `pass-through`

- B. `proxy`

- C. `proxy_pass`

- D. `proxypass`

15. 哪一个配置指令决定了初始启动 Apache 子服务器进程的数量？

- A. `Servers`

- B. `MaxServers`

- C. `StartServers`

- D. `ServerStarts`

16. 哪一个 Apache 指令设置日志文件的格式，包括日志文件中记录了哪些元素？

- A. `LogFile`

- B. `Format`

- C. `LoggingDirective`

- D. `LogFormat`

17. `.htaccess` 文件中的哪一个选项仅允许共享组的用户访问？

- A. `Require sharing`

- B. `RequireUser sharing`

- C. `Require user sharing`

- D. `AllowOnly sharing`

19. 以下哪一个 `RedirectMatch` 指令会在用户尝试查看 `.git` 目录时向用户提供“页面未找到”错误？

- A. `RedirectMatch 404 /\.git(/|$)`

- B. `RedirectMatch PageNotFound /.git/`

- C. `RedirectMatch 404 .git`

- D. `RedirectMatch .git 404`

20. Apache 配置中的以下哪一个指令告诉服务器 SSL 私钥的路径？

- A. `SSLKeyFile`

- B. `SSLCertificatePrivateKey`

- C. `SSLCertificateKeyFile`

- D. `SSLPrivateKey`

21. Squid 默认在哪个端口上监听？

- A. `3000`

- B. `3128`

- C. `5150`

- D. `10300`

22. 以下哪一个模块提供了根据主机名或 IP 地址为 Apache 授权？

- A. `mod_auth_ipaddress`

- B. `mod_auth_host`

- C. `mod_authz_host`

- D. `mod_auth_dns`

23. Apache 在哪一个日志文件中记录对服务器的请求？

- A. `access_log`

- B. `access-log`

- C. `access.txt`

- D. `syslog`

24. Squid 配置中的哪一个指令决定了给定的 ACL 是否可以使用代理？

- A. `access_allow`

- B. `http_access`

- C. `proxy_access`

- D. `enable_access`

25. 以下哪行 Apache 配置将 `.htaccess` 文件的名称更改为 `.htaccesslist`？

- A. `Access .accesslist`

- B. `AccessFile .accesslist`

- C. `AccessFileName ".accesslist"`

- D. `AuthFile ".accesslist"`

19. `smbstatus` 的哪个选项可以显示锁列表？

- A. `-l`

B. `-L`

C. `-o`

D. `-m`

20. 下列哪个命令可以在 Samba 密码数据库中创建新用户？

- A. `passwd -samba`

B. `smbpasswd -a`

C. `smbpass`

D. `smbuser -c`

21. Samba 配置文件中共享（share）内定义的哪个选项指定了浏览网络共享的用户是否能够看到该共享？

- A. `browseable`

B. `shareconnect`

C. `sharepoint`

D. `browseenable`

22. `samba-tool` 命令中的哪一个被用于验证本地 Active Directory 数据库以确保其无错误？

- A. `dbverify`

B. `dblist`

C. `verifydb`

D. `dbcheck`

23. Samba 文件中哪个部分指定了日志文件？

- A. `[server]`

B. `[logging]`

C. `[global]`

D. `[debug]`

24. 下列哪个命令可以用于验证 Samba 配置文件的语法？

- A. `testsmb`

B. `smbest`

C. `testparm`

D. `smbver`

25. 下列哪个命令通过重新加载文件来导出 `/etc/exports` 中的所有文件系统？

- A. `export -a`

B. `exportfs -ra`

C. `exportnfs -a`

D. `exportnfs -r`

## 第 20 章 文件共享（主题 209） 205

26. `smbclient` 的哪个选项允许指定名称解析的顺序？

A. `-R`

B. `-r`

C. `-d`

D. `-o`

27. `mountd` 的哪个选项会记录所有的成功的请求？

A. `-n`

B. `-b`

C. `-l`

D. `-r`

28. Samba 共享配置中的哪个选项配置了该共享是否允许读写访问？

A. `read write`

B. `read only`

C. `read/write`

D. `read-write`

29. `smbd` 默认在哪些端口上监听？

A. `139`

B. `443`

C. `139` 和 `445`

D. `161` 和 `162`

30. `/etc/exports` 中的哪个选项防止远程 `root` 用户在 NFS 服务器共享的文件系统上拥有 `root` 权限？

A. `no_root`

B. `deny_root`

C. `root_squash`

D. `disallow_root`

31. 下列哪个命令显示 Windows 到 Linux 的组映射？

A. `groupmap list`

B. `net groupmap list`

C. `netgroup list`

D. `net list groupmapping`

32. `rpcinfo` 的哪个选项显示当前的端口映射？

A. `-p`

B. `-c`

C. `-m`

D. `-f`

33. `smbpasswd` 命令的下列哪个选项可以删除指定的用户？

A. `-d`

B. `-x`

C. `-o`

D. `-e`

34. 下列哪个命令可以列出名为 `fs.example.com` 的主机上可用的共享？

A. `smblist`

B. `smblist -list`

C. `smbclient -L`

D. `smbshare -L`

35. 下列哪个日志文件指令会为每个共享创建一个单独日志文件？

A. `log file = <share>.log`

B. `log file = %<share>.log`

C. `log file = %S.log`

D. `log file = [share].log`

36. 下列哪个命令可以用于测试 Windows NetBIOS 相关的名称服务和浏览状态？

A. `mblookup`

B. `adlookup`

C. `browser`

D. `nmblookup`

37. 下列哪个命令停止共享所有 NFS 文件共享？

A. `nfs stop -a`

B. `nfs-stopshare`

C. `stopnfs -a`

D. `exportfs -ua`

# 第 21 章 网络客户端管理（主题 210）

本章涵盖了以下 LPIC-2 考试主题：

## 210.1 DHCP 配置

- DHCP 配置文件、术语和实用工具
- 子网网和动态分配的范围
- 对 DHCP6 和路由器通告（Router Advertisements）的了解
- 以下是所用文件、术语和实用工具的部分列表：
  - `dhcpd.conf`
  - `dhcpcd.leases`
  - `syslog` 或 `systemd journal` 中的 DHCP 消息
  - `arp`
  - `dhcpcd`
  - `radvd`
  - `radvd.conf`



# 第 21 章 网络客户端管理（主题 210）

本章涵盖了以下 LPIC-2 考试主题：

## 210.1 DHCP 配置

- `DHCP` 配置文件、术语和实用工具
- 子网网和动态分配的范围
- 对 `DHCP6` 和路由器通告（`Router Advertisements`）的了解
- 以下是所用文件、术语和实用工具的部分列表：
  - `dhcpd.conf`
  - `dhcpcd.leases`
  - `syslog` 或 `systemd journal` 中的 `DHCP` 消息
  - `arp`
  - `dhcpcd`
  - `radvd`
  - `radvd.conf`

## 210.2 PAM 认证

- `PAM` 配置文件、术语和实用工具
- `passwd` 和 `shadow`
- 使用 `sssd` 进行认证
- 以下是所用文件和实用工具的部分列表：
  - `/etc/pam.d/`
  - `pam.conf`
  - `nsswitch.conf`
  - `pam_unix`, `pam_limits`, `sssd.conf`

## 210.3 LDAP 客户端用法

- 用于数据管理和查询的 `LDAP` 实用工具
- 修改用户密码
- 查询 `LDAP` 目录
- 以下是所用文件、术语和实用工具的部分列表：
  - `ldapsearch`
  - `ldappasswd`
  - `ldapadd`
  - `ldapdelete`

## 210.4 配置 OpenLDAP 服务器

- `OpenLDAP`
- 基于目录的配置
- 访问控制
- 属性（`Distinguished Names`）
- `LDAP` 操作
- 模式（`Schemas`）和白页（`Whitepages`）
- 目录
- 对象
- 以下是所用文件的部分列表：
  - `slapd`
  - `slapconfig`
  - `LDIF`
  - `slapadd`
  - `slapindex`
  - `/var/lib/`

## 练习题

1. `/etc/exports` 中的哪个选项通过重新加载文件来导出 `/etc/exports` 中的所有文件系统？
   A. `export -a`
   B. `exportfs -ra`
   C. `exportnfs -a`
   D. `exportnfs -r`

2. `smclient` 的哪个选项允许指定名称解析的顺序？
   A. `-R`
   B. `-r`
   C. `-d`
   D. `-o`

3. `mountd` 的哪个选项会记录所有成功的请求？
   A. `-n`
   B. `-b`
   C. `-l`
   D. `-r`

4. `Samba` 共享配置中的哪个选项配置了该共享是否允许读写访问？
   A. `read write`
   B. `read only`
   C. `read/write`
   D. `read-write`

5. `smbd` 默认在哪些端口上监听？
   A. `139`
   B. `443`
   C. `139` 和 `445`
   D. `161` 和 `162`

6. `/etc/exports` 中的哪个选项防止远程 `root` 用户在 `NFS` 服务器共享的文件系统上拥有 `root` 权限？
   A. `no_root`
   B. `deny_root`
   C. `root_squash`
   D. `disallow_root`

7. 下列哪个命令显示 `Windows` 到 `Linux` 的组映射？
   A. `groupmap list`
   B. `net groupmap list`
   C. `netgroup list`
   D. `net list groupmapping`

8. `rpcinfo` 的哪个选项显示当前的端口映射？
   A. `-p`
   B. `-c`
   C. `-m`
   D. `-f`

9. `smbpasswd` 命令的下列哪个选项可以删除指定的用户？
   A. `-d`
   B. `-x`
   C. `-o`
   D. `-e`

10. 下列哪个命令可以列出名为 `fs.example.com` 的主机上可用的共享？
    A. `smblist`
    B. `smblist -list`
    C. `smbclient -L`
    D. `smbshare -L`

11. 下列哪个日志文件指令会为每个共享创建一个单独日志文件？
    A. `log file = <share>.log`
    B. `log file = %<share>.log`
    C. `log file = %S.log`
    D. `log file = [share].log`

12. 下列哪个命令可以用于测试 `Windows NetBIOS` 相关的名称服务和浏览状态？
    A. `mblookup`
    B. `adlookup`
    C. `browser`
    D. `nmblookup`

13. 下列哪个命令停止共享所有 `NFS` 文件共享？
    A. `nfs stop -a`
    B. `nfs-stopshare`
    C. `stopnfs -a`
    D. `exportfs -ua`

14. 哪个 `PAM` 模块提供了检查和强制密码强度的机制？
    A. `pam_passwdstr.so`
    B. `pam_cracklib.so`
    C. `pam_libpassword.so`
    D. `pam_strpass.so`

15. 你需要为 `sssd` 指定一个备用配置文件。在 `sssd` 命令行可以使用哪个选项来指向新的配置文件？
    A. `-f`
    B. `-c`
    C. `-a`
    D. `-m`

16. `DHCP` 故障转移在哪个端口进行通信？
    A. `67`
    B. `68`
    C. `647`
    D. `389`

17. `dhcpcd.conf` 中的哪个选项定义了将随 `DHCP` 租约发送的默认网关？
    A. `default-gw`
    B. `default-gateway`
    C. `routers`
    D. `default-route`

18. 哪个命令从当前的 `LDAP` 数据库创建 `LDIF` 文件？
    A. `slapdump`
    B. `ldapdump`
    C. `slapcat`
    D. `catldap`

19. 哪个 `PAM` 模块负责执行限制条件，例如最大登录数和使用的 `CPU` 时间？
    A. `pam_enforce.so`
    B. `pam_limittest.so`
    C. `pam_max.so`
    D. `pam_limits.so`

20. 下哪个命令用于根据现有的 `slapd` 数据库重新创建索引？
    A. `ldapind`
    B. `ldapindex`
    C. `slapindex`
    D. `indexldap`

21. 在 `slapd.conf` 配置文件中将日志级别设置为 `0x10` 时，会记录什么？
    A. 无调试信息
    B. 跟踪调试
    C. 统计日志
    D. 发送和接收的数据包

22. 在使用 `slapapd` 进行大型导入时，在完成完成 90% 处发生错误。`slapapd` 的哪个选项可以指定从哪行开始重新导入？
    A. `-l`
    B. `-f`
    C. `-q`
    D. `-j`

23. 对于 `OpenLDAP 2.3` 及更高版本，推荐使用哪个命令配置 `slapd`？
    A. `slapd-conf`
    B. `config-slapd`
    C. `openldap-config`
    D. `slapd-config`

24. 在使用 `LDIF` 文件更改 `LDAP` 数据库时，使用哪个 `changetype` 来创建新的数据库条目？
    A. `create`
    B. `add`
    C. `addmod`
    D. `insert`

25. 使用 `ldapsearch` 时，以下哪个选项可以创建不带注释或版本信息的 `LDIFv1` 格式输出？
    A. `-L`
    B. `-LLL`
    C. `-cal`
    D. `-e`

26. `LDAP SSL` 在哪个端口监听连接？
    A. `389`
    B. `443`
    C. `636`
    D. `3128`

27. 以下哪个 `PAM` 模块可以用于使用外部文件的授权和认证场景？
    A. `pam_authfiles.so`
    B. `pam_listfiles.so`
    C. `pam_filesauth.so`
    D. `pam_fileauth.so`

28. `ldapmodify` 的哪个选项用于执行空运行，即不对对数据库进行任何更改？
    A. `-n`
    B. `-d`
    C. `-l`
    D. `-e`

29. 当未提供过滤器时，`ldapsearch` 的默认过滤器是什么？
    A. `(*)`
    B. `(objectClass=*)`
    C. `(class=*)`
    D. `(list*)`

30. 哪个 `PAM` 模块用于与 `SSSD` 系统集成？
    A. `pam_sss.so`
    B. `pam_sssd.so`
    C. `pam_sssd_config.so`
    D. `pam_sss_mod.so`

31. `sssd.conf` 中的哪个选项设置了 `LDAP` 服务器的 `URI`？
    A. `ldap_server`
    B. `ldap_uri`
    C. `ldap_connect`
    D. `ldap_use`

32. 以下哪行配置会导致 `DHCP` 服务器拒绝来自服务器未知客户端的地址请求？
    A. `unknown-clients: deny;`
    B. `deny unknown-clients;`
    C. `clients-deny: unknown`
    D. `list-clients-deny`

# 电子邮件服务

(主题 211)

本章涵盖以下 `LPIC-2` 考试主题：

## 211.1 使用邮件服务器



# 第 22 章 ■ 电子邮件服务 (主题 211)

- `postfix` 的配置文件
- `postfix` 的基础 `TLS` 配置
- `SMTP` 协议的基础知识
- 对 `sendmail` 和 `exim` 的了解

以下是所用文件、术语和工具的列表：
  - `postfix` 的配置文件和命令
  - `/etc/postfix/`
  - `/var/spool/postfix/`
  - `sendmail` 模拟层命令
  - `/etc/aliases`
  - `/var/log/` 中的邮件日志

### 211.2 管理邮件投递

- 对 `Sieve` 功能、语法和操作符的理解
- 使用 `Sieve` 根据发送者、收件者、头部和大小对邮件进行过滤和排序
- 对 `procmail` 的了解

以下是所用文件、术语和工具的列表：
  - 条件和比较操作符
  - `keep`, `fileinto`, `redirect`, `discard`, `stop`
  - `Dovecot` 扩展

### 211.3 管理信箱

- `Dovecot` `IMAP` 和 `POP3` 配置
- `Dovecot` 的基础 `TLS`
- 对 `Courier` 的了解

以下是所用文件、术语和工具的列表：
  - `/etc/dovecot/`
  - `dovecot.conf`
  - `doveconf`
  - `doveadm`

# 第 22 章 ■ 电子邮件服务 (主题 211)

2. `Postfix` 的队列消息存储在哪个目录？
   A. `/var/queue`
   B. `/var/spool/mailq`
   C. `/var/spool/postfix`
   D. `/postfix`

3. `Postfix` 的证书和密钥应该是什么格式？
   A. `PKCS`
   B. `PEM`
   C. `TLS`
   D. `SSL`

4. `Sieve` 的哪个配置关键字负责将邮件移动到指定的信箱？
   A. `filein`
   B. `moveinto`
   C. `mailmover`
   D. `fileinto`

5. `postfix` 服务器的配置文件存储在哪个目录？
   A. `/etc/postfix.d`
   B. `/etc/postfix.conf.d`
   C. `/var/mail/postfix`
   D. `/postfix`

6. 以下哪个文件作为 `Procmail` 的用户配置？
   A. `/home/procmail.conf`
   B. `~/.procmailrc`
   C. `/etc/procmail.conf`
   D. `~/procmail.conf`

7. `/etc/aliases` 中的以下哪个定义会将邮件投递到 `admin@example.com` 和 `webmaster@example.com`？
   A. `root = admin@example.com, webmaster.com`
   B. `root: admin webmaster`
   C. `root: admin`
   D. `root: admin@example.com,master.com`

8. 以下哪个命令显示 `Postfix` 服务器的邮件队列？
   A. `mailqueue`
   B. `qmail`
   C. `mailq`
   D. `mail-queue`

9. 以下哪个命令会导致 `Postfix` 立即处理邮件队列？
   A. `postqueue -f`
   B. `mailq -f`
   C. `postqueue -a`
   D. `mailq -process`

10. 以下哪个命令删除 `Postfix` 邮件队列中的所有消息？
    A. `postsuper -d`
    B. `postsuper - ALL`
    C. `postsuper delete-all`
    D. `postsuper -D`

11. 执行哪个命令可以重建 `/etc/aliases` 数据库？
    A. `newaliases`
    B. `realaliases`
    C. `rebuildaliases`
    D. `aliases`

12. 哪个 `Sieve` 动作将邮件保留在信箱中？
    A. `remain`
    B. `keep`
    C. `store`

13. 以下哪个命令查看存在于 `Postfix` 队列中的邮件内容？
    A. `postshow`
    B. `postless`
    C. `postmore`
    D. `postcat`

14. 使用哪个命令可以查看 `Dovecot` 服务器当前登录的用户？
    A. `doveadm list`
    B. `dovecot list`
    C. `dovecot users`
    D. `doveadm who`

15. 以下哪个命令删除符合 `Sieve` 条件的邮件？
    A. `delete`
    B. `discard`
    C. `remove`
    D. `kill`

16. 以下哪个命令用于查看 `Postfix` 服务器上的待处理（`pending`）队列？
    A. `postqueue -p`
    B. `postconf -pending`
    C. `postqueue -f`
    D. `postsuper pending`

17. `Sieve` 配置中的以下哪个动作行将邮件拷贝到 `admin@example.com` 并保留一份供后续处理？
    A. `redirect "admin@example.com"`
    B. `forward "admin@example.com"`
    C. `redirect :copy "admin@example.com"`
    D. `forward :duplicate "admin@example.com"`

18. `vacation` `Sieve` 功能中的哪个配置参数指定向同一发送者发送 `vacation` 回复的频率？
    A. `:freq`
    B. `:days`
    C. `:often`
    D. `:replyfrequency`

19. 使用哪个 `Postfix` 相关命令按时间提供输入和活动队列中邮件数量概述？
    A. `queuelist`
    B. `postq`
    C. `qshape`
    D. `queueshow`

20. 以下哪个命令显示当前的 `Dovecot` 配置？
    A. `doveconf`
    B. `doveconfig`
    C. `dovecot --list`
    D. `doveadm conf`

21. 在使用 `Sieve` 时，当没有其他动作优先时，隐式执行哪个动作？
    A. `keep`
    B. `discard`
    C. `shred`
    D. `forward`

22. `Postfix` 的哪个配置参数设置允许通过服务器中继的网络？
    A. `relaynet`
    B. `mynetworks`
    C. `networkrelay`
    D. `relnet`

23. 以下哪个命令测试 `Dovecot` 服务器用户的身份验证？
    A. `dovecot -testauth`
    B. `doveadm testauth`
    C. `dovecot auth`
    D. `doveadm auth`

24. 以下哪个命令编译原生语言的 `Sendmail` 配置文件以生成 `/etc/sendmail.cf` 的标准 `Sendmail` 配置文件？
    A. `makemap sendmail.mc > /etc/sendmail.cf`
    B. `m1 sendmail.mc > /etc/sendmail.cf`
    C. `gcc sendmail.mc > /etc/sendmail.cf`
    D. `m4 sendmail.mc > /etc/sendmail.cf`

25. 以下哪个命令查看所有与 `Postfix` 配置相关的参数？
    A. `postconf -d`
    B. `postmaster -config`
    C. `postfix -c`
    D. `postc -a`

26. 在哪个文件中可以找到与 `Postfix` 服务器邮件投递相关的错误？
    A. `/var/log/mail`
    B. `/var/log/postfix.log`
    C. `/var/log/mail.err`
    D. `/var/log/postfix.err`

27. 使用哪种选项在 `Dovecot` 配置中创建一个监听端口的段落（`stanza`）？
    A. `inet_port`
    B. `inet_listener`
    C. `listening_port`
    D. `listener`

28. `SMTP` 默认在哪个端口上运行？
    A. `25`
    B. `2525`
    C. `110`
    D. `143`

29. 你需要在 `Postfix` 服务器上找到邮件队列路径。你正在使用 `postconf -d` 查看所有参数。以下哪行包含 `Postfix` 服务器上的邮件队列路径？
    A. `mqueue_dir`
    B. `queue_dir`
    C. `mailq_path`
    D. `mqueue_path`

30. 在测试客户端与服务器（`mail.example.com`）之间的 `SMTP` 通信时，你需要使用扩展问候（`Extended Hello`）语法开始对话，来自 `mail.example.com`？
    A. `BEGIN mail.example.com`
    B. `SMTP mail.example.com`
    C. `HELO mail.example.com`
    D. `EHLO mail.example.com`

31. 在 `Sieve` 中，以下哪个关键字用于在原始条件失败时定义备选条件？
    A. `else if`
    B. `elsif`
    C. `elseif`
    D. `alt`

32. 哪种 `Sieve` 测试通过将对象视为地址来检查，以判断其中是否存在字符串？
    A. `:grep`
    B. `:contains`
    C. `:has`
    D. `:lookin`

33. 哪种配置选项指定了 `Dovecot` 服务器内活动身份验证进程的最大数量？
    A. `process_limit`
    B. `max_proc`
    C. `proc_max`
    D. `auth_proc_max`

34. 在 `Sieve` 中检查地址时，使用哪个关键字尝试仅查看地址的域名部分？
    A. `:domainname`
    B. `:afterat`
    C. `:last`
    D. `:domain`

35. `Dovecot` 在哪个端口上监听基于 `SSL/TLS` 的 `IMAP` 或 `IMAPS`？
    A. `143`
    B. `993`
    C. `995`
    D. `110`

36. 以下哪个文件用作 `Debian` 系统上 `Exim 4` 的默认配置文件？
    A. `/etc/exim/exim4.conf`
    B. `/etc/exim/exim.conf`
    C. `/etc/exim/exim.configure`
    D. `/etc/exim/exim/configure`

37. 使用哪种 `Postfix` 配置选项配合 `postscreen` 服务器来设置 `TLS` 安全级别？
    A. `postscreen_tls`
    B. `postscreen_tls_security_level`
    C. `postscreen_security_level`
    D. `post_tls_sec_level`

# 第 23 章 系统安全 (主题 212)

本章涵盖了以下 `LPIC-2` 考试主题：

### 212.1 配置路由器

- `iptables` 和 `ip6tables` 配置文件、工具和实用程序
- 管理路由表的工具、命令和实用程序。
- 私有地址范围 (`IPv4`) 和唯一本地地址 (`Unique Local Addresses`) 以及链路本地地址 (`Link Local Addresses` `IPv6`)
- 端口重定向和 `IP` 转发
- 编写过滤规则，根据源或目的协议、端口和地址接受或阻止 `IP` 数据包
- 保存和重载过滤配置

以下是使用的文件、术语和实用程序的部分列表：
  - `/proc/sys/net/ipv4/`
  - `/proc/sys/net/ipv6/`
  - `/etc/services`
  - `iptables`
  - `ip6tables`

### 212.2 管理 FTP 服务器

- `Pure-FTPd` 和 `vsftpd` 的配置文件、工具和实用程序
- 对 `ProFTPd` 的了解
- 理解被动与主动 `FTP` 连接

以下是使用的文件、术语和实用程序的部分列表：
  - `vsftpd.conf`
  - 重要的 `Pure-FTPd` 命令行选项

### 212.3 安全外 (SSH)

- `OpenSSH` 配置文件、工具和实用程序
- 超级用户和普通用户的登录限制
- 管理和使用服务器及客户端密钥进行有密码或无密码登录
- 从多个主机使用多个连接，以防止配置更改后丢失与远程主机的连接

以下是使用的文件、术语和实用程序的部分列表：
  - `ssh`
  - `sshd`
  - `/etc/ssh/sshd_config`
  - `/etc/ssh/`
  - 私钥和公钥文件
  - `PermitRootLogin`, `PubKeyAuthentication`, `AllowUsers`, `PasswordAuthentication`, `Protocol`

### 212.4 安全任务

- 用于扫描和测试服务器端口的工具和实用程序
- 报告安全警报的位置和机构，如 `Bugtraq`、`CERT` 或其他来源
- 实现入侵检测系统 (`IDS`) 的工具和实用程序
- 对 `OpenVAS` 和 `Snort` 的了解

以下是使用的文件、术语和实用程序的部分列表：
  - `telnet`
  - `nmap`
  - `fail2ban`
  - `nc`
  - `iptables`

### 212.5 OpenVPN

- `OpenVPN`

以下是使用的文件、术语和实用程序的部分列表：
  - `/etc/openvpn/`
  - `openvpn`



![](img/84990579543ce21a46ac6dc507fcde32_262_0.png)

### 212.3 安全外 (SSH)

- `OpenSSH` 配置文件、工具和实用程序
- 超级用户和普通用户的登录限制
- 管理和使用服务器及客户端密钥进行有密码或无密码登录
- 从多个主机使用多个连接，以防止配置更改后丢失与远程主机的连接

以下是使用的文件、术语和实用程序的部分列表：

- `ssh`
- `sshd`
- `/etc/ssh/sshd_config`
- `/etc/ssh/`
- 私钥和公钥文件
- `PermitRootLogin`, `PubKeyAuthentication`, `AllowUsers`, `PasswordAuthentication`, `Protocol`

### 212.4 安全任务

- 用于扫描和测试服务器端口的工具和实用程序
- 报告安全警报的位置和机构，如 `Bugtrap`、`CERT` 或其他来源
- 实现入侵检测系统 (`IDS`) 的工具和实用程序
- 对 `OpenVAS` 和 `Snort` 的了解

以下是使用的文件、术语和实用程序的部分列表：

- `telnet`
- `nmap`
- `fail2ban`
- `nc`
- `iptables`

### 212.5 OpenVPN

- `OpenVPN`

以下是使用的文件、术语和实用程序的部分列表：

- `/etc/openvpn/`
- `openvpn`

![](img/84990579543ce21a46ac6dc507fcde32_263_0.png)

## 23 章 系统安全 (主题 212) 225

27. 使用哪种选项在 `Dovecot` 配置中创建一个监听端口的段落（stanza）？

- A. `inet_port`
- B. `inet_listener`
- C. `listening_port`
- D. `listener`

28. `SMTP` 默认在哪个端口上运行？

- A. 25
- B. 2525
- C. 110
- D. 143

29. 你需要在 `Postfix` 服务器上找到邮件队列路径。你正在使用 `postconf -d` 查看所有参数。以下哪行包含 `Postfix` 服务器上的邮件队列路径？

- A. `mqueue_dir`
- B. `queue_dir`
- C. `mailq_path`
- D. `mqueue_path`

30. 在测试客户端与服务器（`mail.example.com`）之间的 `SMTP` 通信时，你需要使用扩展问候（Extended Hello）语法开始对话，来自 `mail.example.com`？

- A. `BEGIN mail.example.com`
- B. `SMTP mail.example.com`
- C. `HELO mail.example.com`
- D. `EHLO mail.example.com`

31. 在 `Sieve` 中，以下哪个关键字用于在原始条件失败时定义备选条件？

- A. `else if`
- B. `elsif`
- C. `elseif`
- D. `alt`

32. 哪种 `Sieve` 测试通过将对象视为地址来检查，以判断其中是否存在字符串？

- A. `:grep`
- B. `:contains`
- C. `:has`
- D. `:lookin`

## 222 第二部分 ■ LPIC-2

33. 哪种配置选项指定了 `Dovecot` 服务器内活动身份验证进程的最大数量？

- A. `process_limit`
- B. `max_proc`
- C. `proc_max`
- D. `auth_proc_max`

34. 在 `Sieve` 中检查地址时，使用哪个关键字尝试仅查看地址的域名部分？

- A. `:domainname`
- B. `:afterat`
- C. `:last`
- D. `:domain`

35. `Dovecot` 在哪个端口上监听基于 `SSL/TLS` 的 `IMAP` 或 `IMAPS`？

- A. 143
- B. 993
- C. 995
- D. 110

36. 以下哪个文件用作 `Debian` 系统上 `Exim 4` 的默认配置文件？

- A. `/etc/exim/exim4.conf`
- B. `/etc/exim/exim.conf`
- C. `/etc/exim/exim.configure`
- D. `/etc/exim/exim/configure`

37. 使用哪种 `Postfix` 配置选项配合 `postscreen` 服务器来设置 `TLS` 安全级别？

- A. `postscreen_tls`
- B. `postscreen_tls_security_level`
- C. `postscreen_security_level`
- D. `post_tls_sec_level`

## 第 23 章

## 系统安全

(主题 212)

本章涵盖了以下 `LPIC-2` 考试主题：

+ 212.1 配置路由器

- `iptables` 和 `ip6tables` 配置文件、工具和实用程序
- 管理路由表的工具、命令和实用程序。
- 私有地址范围 (`IPv4`) 和唯一本地地址 (`Unique Local Addresses`) 以及链路本地地址 (`Link Local Addresses IPv6`)
- 端口重定向和 `IP` 转发
- 列表写过滤规则，根据源或目的协议、端口和地址接受或阻止 `IP` 数据包
- 保存和重载过滤配置

- 以下是使用的文件、术语和实用程序的部分列表：
  - `/proc/sys/net/ipv4/`
  - `/proc/sys/net/ipv6/`
  - `/etc/services`
  - `iptables`
  - `ip6tables`

+ 212.2 管理 FTP 服务器

- `Pure-FTPd` 和 `vsftpd` 的配置文件、工具和实用程序
- 对 `ProFTPd` 的了解
- 理解被动与主动 `FTP` 连接

- 以下是使用的文件、术语和实用程序的部分列表：
  - `vsftpd.conf`
  - 重要的 `Pure-FTPd` 命令行选项

![](img/84990579543ce21a46ac6dc507fcde32_262_0.png)

### 212.3 安全外 (SSH)

- `OpenSSH` 配置文件、工具和实用程序
- 超级用户和普通用户的登录限制
- 管理和使用服务器及客户端密钥进行有密码或无密码登录
- 从多个主机使用多个连接，以防止配置更改后丢失与远程主机的连接

以下是使用的文件、术语和实用程序的部分列表：

- `ssh`
- `sshd`
- `/etc/ssh/sshd_config`
- `/etc/ssh/`
- 私钥和公钥文件
- `PermitRootLogin`, `PubKeyAuthentication`, `AllowUsers`, `PasswordAuthentication`, `Protocol`

### 212.4 安全任务

- 用于扫描和测试服务器端口的工具和实用程序
- 报告安全警报的位置和机构，如 `Bugtrap`、`CERT` 或其他来源
- 实现入侵检测系统 (`IDS`) 的工具和实用程序
- 对 `OpenVAS` 和 `Snort` 的了解

以下是使用的文件、术语和实用程序的部分列表：

- `telnet`
- `nmap`
- `fail2ban`
- `nc`
- `iptables`

### 212.5 OpenVPN

- `OpenVPN`

以下是使用的文件、术语和实用程序的部分列表：

- `/etc/openvpn/`
- `openvpn`

![](img/84990579543ce21a46ac6dc507fcde32_263_0.png)

## 23 章 系统安全 (主题 212) 227

27. 使用哪种选项在 `Dovecot` 配置中创建一个监听端口的段落（stanza）？

- A. `inet_port`
- B. `inet_listener`
- C. `listening_port`
- D. `listener`

28. `SMTP` 默认在哪个端口上运行？

- A. 25
- B. 2525
- C. 110
- D. 143

29. 你需要在 `Postfix` 服务器上找到邮件队列路径。你正在使用 `postconf -d` 查看所有参数。以下哪行包含 `Postfix` 服务器上的邮件队列路径？

- A. `mqueue_dir`
- B. `queue_dir`
- C. `mailq_path`
- D. `mqueue_path`

30. 在测试客户端与服务器（`mail.example.com`）之间的 `SMTP` 通信时，你需要使用扩展问候（Extended Hello）语法开始对话，来自 `mail.example.com`？

- A. `BEGIN mail.example.com`
- B. `SMTP mail.example.com`
- C. `HELO mail.example.com`
- D. `EHLO mail.example.com`

31. 在 `Sieve` 中，以下哪个关键字用于在原始条件失败时定义备选条件？

- A. `else if`
- B. `elsif`
- C. `elseif`
- D. `alt`

32. 哪种 `Sieve` 测试通过将对象视为地址来检查，以判断其中是否存在字符串？

- A. `:grep`
- B. `:contains`
- C. `:has`
- D. `:lookin`

## 222 第二部分 ■ LPIC-2

33. 哪种配置选项指定了 `Dovecot` 服务器内活动身份验证进程的最大数量？

- A. `process_limit`
- B. `max_proc`
- C. `proc_max`
- D. `auth_proc_max`

34. 在 `Sieve` 中检查地址时，使用哪个关键字尝试仅查看地址的域名部分？

- A. `:domainname`
- B. `:afterat`
- C. `:last`
- D. `:domain`

35. `Dovecot` 在哪个端口上监听基于 `SSL/TLS` 的 `IMAP` 或 `IMAPS`？

- A. 143
- B. 993
- C. 995
- D. 110

36. 以下哪个文件用作 `Debian` 系统上 `Exim 4` 的默认配置文件？

- A. `/etc/exim/exim4.conf`
- B. `/etc/exim/exim.conf`
- C. `/etc/exim/exim.configure`
- D. `/etc/exim/exim/configure`

37. 使用哪种 `Postfix` 配置选项配合 `postscreen` 服务器来设置 `TLS` 安全级别？

- A. `postscreen_tls`
- B. `postscreen_tls_security_level`
- C. `postscreen_security_level`
- D. `post_tls_sec_level`

## 第 23 章

## 系统安全

(主题 212)

本章涵盖了以下 `LPIC-2` 考试主题：

+ 212.1 配置路由器

- `iptables` 和 `ip6tables` 配置文件、工具和实用程序
- 管理路由表的工具、命令和实用程序。
- 私有地址范围 (`IPv4`) 和唯一本地地址 (`Unique Local Addresses`) 以及链路本地地址 (`Link Local Addresses IPv6`)
- 端口重定向和 `IP` 转发
- 列表写过滤规则，根据源或目的协议、端口和地址接受或阻止 `IP` 数据包
- 保存和重载过滤配置

- 以下是使用的文件、术语和实用程序的部分列表：
  - `/proc/sys/net/ipv4/`
  - `/proc/sys/net/ipv6/`
  - `/etc/services`
  - `iptables`
  - `ip6tables`

+ 212.2 管理 FTP 服务器

- `Pure-FTPd` 和 `vsftpd` 的配置文件、工具和实用程序
- 对 `ProFTPd` 的了解
- 理解被动与主动 `FTP` 连接

- 以下是使用的文件、术语和实用程序的部分列表：
  - `vsftpd.conf`
  - 重要的 `Pure-FTPd` 命令行选项

![](img/84990579543ce21a46ac6dc507fcde32_262_0.png)

### 212.3 安全外 (SSH)



# 第 23 章 系统安全 (主题 212)

本章涵盖了以下 LPIC-2 考试主题：

### 212.1 配置路由器

- `iptables` 和 `ip6tables` 配置文件、工具和实用程序
- 管理路由表的工具、命令和实用程序
- 私有地址范围 (`IPv4`) 和唯一本地地址 (`Unique Local Addresses`) 以及链路本地地址 (`Link Local Addresses IPv6`)
- 端口重定向和 `IP` 转发
- 列表写过滤规则，根据源或目的协议、端口和地址接受或阻止 `IP` 数据包
- 保存和重载过滤配置

以下是使用的文件、术语和实用程序的部分列表：

- `/proc/sys/net/ipv4/`
- `/proc/sys/net/ipv6/`
- `/etc/services`
- `iptables`
- `ip6tables`

### 212.2 管理 FTP 服务器

- `Pure-FTPd` 和 `vsftpd` 的配置文件、工具和实用程序
- 对 `ProFTPd` 的了解
- 理解被动与主动 `FTP` 连接

以下是使用的文件、术语和实用程序的部分列表：

- `vsftpd.conf`
- 重要的 `Pure-FTPd` 命令行选项

### 212.3 安全外 (SSH)

- `OpenSSH` 配置文件、工具和实用程序
- 超级用户和普通用户的登录限制
- 管理和使用服务器及客户端密钥进行有密码或无密码登录
- 从多个主机使用多个连接，以防止配置更改后丢失与远程主机的连接

以下是使用的文件、术语和实用程序的部分列表：

- `ssh`
- `sshd`
- `/etc/ssh/sshd_config`
- `/etc/ssh/`
- 私钥和公钥文件
- `PermitRootLogin`, `PubKeyAuthentication`, `AllowUsers`, `PasswordAuthentication`, `Protocol`

### 212.4 安全任务

- 用于扫描和测试服务器端口的工具和实用程序
- 报告安全警报的位置和机构，如 `Bugtrap`、`CERT` 或其他来源
- 实现入侵检测系统 (`IDS`) 的工具和实用程序
- 对 `OpenVAS` 和 `Snort` 的了解

以下是使用的文件、术语和实用程序的部分列表：

- `telnet`
- `nmap`
- `fail2ban`
- `nc`
- `iptables`

### 212.5 OpenVPN

- `OpenVPN`

以下是使用的文件、术语和实用程序的部分列表：

- `/etc/openvpn/`
- `openvpn`

![img/84990579543ce21a46ac6dc507fcde32_262_0.png](img/84990579543ce21a46ac6dc507fcde32_262_0.png)

## 练习测试

以下是 `COMPTIA LINUX+` 考试 103 的练习测试

20. `OpenSSH` 配置中的哪一个指令用于使用的 `SSH` 协议版本？

- A. `Proto`
- B. `Protocol`
- C. `ProtoVer`
- D. `Version`

21. 下列哪项最准确描述了 `iptables` 中 `DROP` 和 `REJECT` 目标之间的区别？

- A. `DROP` 和 `REJECT` 的作用相同。
- B. `DROP` 静默丢弃数据包，而 `REJECT` 发回 `ICMP` 确认包。
- C. `REJECT` 静默丢弃数据包，而 `DROP` 发回 `ICMP` 确认包。
- D. `DROP` 返回直接消息，而 `REJECT` 返回重定向。

22. 哪个文件包含了允许特定用户认证的密钥列表？

- A. `~/ssh/keys`
- B. `~/ssh/pubkeys`
- C. `~/.ssh/keyauth`
- D. `~/.ssh/authorized_keys`

23. 下列哪个部分 `iptables` 规则设置了每分钟限制记录三条日志的配置？

- A. `-m limit 3 -j LOG`
- B. `-m limit --limit 3/minute --limit-burst 3 -j LOG`
- C. `-m limit --limit 3`
- D. `-m limit --limit-minute 3 --burst 3 -j LOG`

24. `ssh` 命令的哪个选项用于 `X11` 应用转发？

- A. `-X11`
- B. `-A`
- C. `-X`
- D. `-F`

25. 命令 `netstat -a` 报告服务器上的端口 `80` 正在使用中。下列哪个命令可以确定到底是什么在用该端口？

- A. `listPorts`
- B. `portlist -a`
- C. `lsof -i`
- D. `tcpdump`

26. 下列哪个 `iptables` 规则允许入的 `ICMP` 流量？

- A. `-A INPUT -p ICMP -j ACCEPT`
- B. `-A IN -P ICMP`
- C. `-A INPUT -P ACCEPT-ICMP`
- D. `-A IN -P ICMP -j ACCEPT`

27. `OpenSSH` 配置中的哪个选项用于确定是否启用端口转发？

- A. `AllowPortForwarding`
- B. `PortPort`
- C. `ForwardPort`
- D. `AllowTcpForwarding`

28. 下列哪个 `iptables` 规则阻止了来自 `192.168.51.50` 的所有流量？

- A. `-A INPUT -p ALL 192.168.51.50 -j ACCEPT`
- B. `-A INPUT -p ALL -s 192.168.51.50 -j DROP`
- C. `-A INPUT -p ALL -s 192.168.51.50 -j BLOCK`
- D. `-A INPUT -p ALL 192.168.51.50 -j DISCARD`

29. 下列哪个 `iptables` 规则允许所有主机连接到 `TCP` 端口 `2222`？

- A. `-A INPUT -p TCP -s 0/0 --destination-port 2222 -j ACCEPT`
- B. `-A TCP -s ALL -p 2222 -j ACCEPT`
- C. `-A INPUT -p TCP -s *. --destination-port 2222 -j ALLOW`
- D. `-A INPUT --destination-port /* * -j ACCEPT`

30. 下列哪个命令启用了用于 `NAT` 的转发功能？

- A. `echo "1" > /proc/sys/net/ipv4/nat`
- B. `echo "1" > /proc/sys/net/ipv4/ip_forward`
- C. `iptables --enable-forwarding`
- D. `ip-forward --enable`

31. 在 `vsftpd.conf` 文件中，哪个指令启用了 `IPv6`？

- A. `ipv6_enable`
- B. `ipv6`
- C. `ipv6_listen`
- D. `listen_ipv6`

32. `OpenSSH` 的哪个配置指令决定是否使用基于密钥的认证？

- A. `KeyAuth`
- B. `PubKeyAuth`
- C. `PubkeyAuthentication`
- D. `AuthenticationKey`

33. 在 `fail2ban` 的 `jail` 配置中，哪个配置选项设置了监控失败的日志文件名称和位置？

- A. `logpath`
- B. `monitor`
- C. `logfile_mon`
- D. `monitor_log`

34. 哪个命令将公钥身份副本发送到另一个服务器以供 `SSH` 使用？

- A. `ssh-key`
- B. `ssh-copy-key`
- C. `ssh-sendkey`
- D. `ssh-copy-id`

35. 哪个命令用于创建和维护 `IPv6` 的防火墙规则？

- A. `iptables`
- B. `ip6tables`
- C. `ipv6tables`
- D. `ipfw6`

36. 下列哪个 `OpenVPN` 配置项向客户端发送 `DHCP` 选项，以指示客户端使用的 `DNS` 服务器（`192.168.2.1`）？

- A. `push "dhcp-option ns 192.168.2.1"`
- B. `push "dhcp-nameserver 192.168.2.1"`
- C. `push "dhcp-option DNS 192.168.2.1"`
- D. `push "dhcp-dns 192.168.2.1"`

37. `vsftpd.conf` 中的哪个选项指定用户是否能够认证服务器？

- A. `local_enable`
- B. `users_login`
- C. `user_login`
- D. `local_users`

# 第 24 章 练习测试

以下是 `COMPTIA LINUX+` 考试 103 的练习测试

7. 你一直在排除与系统中 `PCI` 设备驱动程序相关的系统问题。哪个命令和选项将显示 `PCI` 设备及其使用的驱动程序？

- A. `lus -v`
- B. `ls -p`
- C. `lspci`
- D. `showci`

8. `telinit` 命令的哪个选项会导致操作不向登录用户发送通知？

- A. `-q`
- B. `-v`
- C. `--noall`
- D. `-l`

9. 查看 `sysfs` 文件系统中的哪个文件可以查看 `eth0` 的 `MAC` 地址？

- A. `/sys/class/eth0/address`
- B. `/sys/devices/eth0`
- C. `/sysfs/devices/eth0`
- D. `/sys/net/eth0`

10. 新添加的 `SATA` 磁盘在启动过程中没有显示。可以在哪里检查以排除此故障？

- A. 系统日志
- B. `Debugfs`
- C. 在 `fdisk` 工具中
- D. `BIOS` 中

11. 哪个命令可以监控与 `dbus` 的通信？

- A. `dbus-mon`
- B. `dbus -m`
- C. `dbus-monitor`
- D. `dbus-debug`

12. 在 `systemd` 环境中，哪个服务管理 `udev`？

- A. `systemd-udevd.service`
- B. `systemd-udev.service`
- C. `udev-service`
- D. `systemd.udevd-service`

13. 表示系统应在 `pm` 点关机的正确语法是什么？

- A. `shutdown +0`
- B. `shutdown pm`
- C. `shutdown +2`
- D. `halt +`

14. `systemctl kill` 命令的哪个选项将更改发送给进程的信号？

- A. `-k`
- B. `-f`
- C. `-s`
- D. `-d`

15. 在 `SysV` 环境中，哪个 `systemctl` 命令和选项等同于 `config --list`？

- A. `systemctl list-unit-files`
- B. `systemctl list-service`
- C. `systemctl --list`
- D. `systemctl list-unit-files --type=service`

16. `ldconfig` 的哪个选项用于更新缓存的位置？

- A. `-C`
- B. `-c`
- C. `-f`
- D. `-v`

17. 下列哪个命令会删除 `Debian` 中包的所有文件，包括配置文件？

- A. `apt-get remove`
- B. `apt-cache clean`
- C. `dpkg -P`
- D. `apt-get conf-remove`

18. `/etc/apt/sources.list` 中表示 `Debian` 源仓库的前缀是什么？

- A. `deb`
- B. `source`
- C. `deb-src`
- D. `debsrc`

19. `rpm` 的哪个选项在升级包的同时显示进度和其他关于操作的额外信息？

- A. `-Iv`
- B. `-Uvh`
- C. `-U`
- D. `-vh`

20. `yum install` 命令的哪个选项会让 `yum` 认为是，因此在执行认为关键的操作时不提示验证？

- A. `-y`
- B. `-f`
- C. `-p`
- D. `-m`

21. 在使用基于 `yum` 的系统时，你需要创建一个配置以确保某些包不升级或安装。可以在 `/etc/yum.conf` 中设置哪个选项来实现此行为？

- A. `exclude`
- B. `noupdate`
- C. `assumeupdate`
- D. `clearupdate`

22. 你在系统的共享库上遇到了困难。下列哪个命令会打印缓存中的当前目录和库？

- A. `ldconfig -C`
- B. `ldd -f`
- C. `ldconfig -p`
- D. `ldd -b`

23. `/etc/yum.repos.d/` `.repo` 文件中的哪个选项用于设置仓库的 `URL`？

- A. `url`
- B. `repourl`
- C. `httpurl`
- D. `baseurl`

24. 哪个命令和选项用于显示 `Debian` 系统上每个包及其依赖关系的基本信息？

- A. `apt-get list`
- B. `apt-cache dump`
- C. `apt-get list`
- D. `apt-cache`



### 第 24 章 ■ 测试卷 1

**25. 运行 `lsblk` 命令时，没有列出 `/boot` 的独立分区。系统可能从哪个分区启动的？**

- A. 在 `/` 分区下有一个 `/boot` 目录。
- B. `/boot` 分区被隐藏了。
- C. 系统尚未构建 `/boot` 分区。
- D. `/boot` 未通过 `lsblk` 显示。

**26. 在哪个层级中存储 `yum` 和 `apt` 缓存数据？**

- A. `/etc`
- B. `/var/cache`
- C. `/usr/lib`
- D. `/tmp`

**27. 在 BIOS 系统中，引导程序通常安装在磁盘的哪个区域？**

- A. `MBR`
- B. `/boot`
- C. 扇区 `8192`
- D. `Front`

**28. 下列哪项最准确描述 Linux 中 `/` 文件系统的内容？**

- A. `/` 文件系统是根文件并包含临时文件。
- B. `/` 文件系统是根的家目录。
- C. `/` 文件系统用于存储设备和交换信息。
- D. `/` 文件系统是根文件系统以及 Linux 层级的逻辑根。

**29. 下列哪个命令将 `grub2-mkconfig` 命令的输出发送到启动的正确位置？**

- A. `grub2-mkconfig --output=/boot/grub2/grub.cfg`
- B. `grub2-mkconfig --file=/boot/grub.menu`
- C. `grub2-mkconfig --file=/boot/grub.lst`
- D. `grub2-mkconfig --output=/boot/menu.lst`

**30. 哪个命令将进入当前用户的家目录？**

- A. `cd !`
- B. `cd home`
- C. `cd ~`
- D. `cd /home`

- C. `imgw raspbian.img | cat /dev/sdc`
- D. `dd raspbian.img > /dev/sdc`

**32. 在排查故障时，你通过 `.bash_history` 确定你最近执行的命令。然而，该文件不包含当前会话的信息。你可以使用哪个命令来查看当前会话期间执行的命令？**

- A. `cmdhist`
- B. `cmds`
- C. `pwd`
- D. `history`

**33. 如果你想在 `/boot` 以外的目录中安装启动镜像，应该向 `grub-install` 传递哪个选项？**

- A. `--boot`
- B. `--image`
- C. `--boot-directory`
- D. `-b`

**34. 应该运行哪个命令来使 `GRUB2` 配置的更改生效？**

- A. `update-grub`
- B. `grub-update`
- C. `grub-config`
- D. `grub-ins`

**35. 在使用 `Bash` shell 时，以下哪个命令将环境变量 `JAVA_PATH` 设置为 `/home/user/java2`？**

- A. `invoke JAVA_PATH=/home/user/java2`
- B. `export JAVA_PATH=/home/user/java2`
- C. `envvar JAVA_PATH=/home/user/java2`
- D. `echo JAVA_PATH=/home/user/java2`

**36. `.bashrc` 中的哪个选项设置了在 `.bash_history` 文件中保留的命令数？**

- A. `HISTLIMIT`
- B. `HISTORYFILE`
- C. `HISTFILESIZES`
- D. `HISTNUM`

**37. 以下哪个命令会使 `nl` 对名为 `code.php` 的文件的所有行（包括空行）进行编号？**

- A. `nl code.php`
- B. `nl -a code.php`
- C. `nl -n code.php`
- D. `nl -b code.php`

**38. 哪个命令可以创建给定明文文件的八进制表示？**

- A. `oct`
- B. `cat`
- C. `list`
- D. `od`

**39. 哪个命令和选项可以以双倍行距格式分页格式文本，并包含页码？**

- A. `pr -d`
- B. `pag -db`
- C. `cat -pd`
- D. `print -d`

**40. 在 `tail` 命令的以下选项中，哪个选项输出从文件开始第 `30` 行开始的最后几行，而不是文件末尾？**

- A. `-n +30`
- B. `-n 30`
- C. `-30`
- D. `+30`

**41. `uniq` 命令的哪个选项会导致匹配不区分大小写？**

- A. `-c`
- B. `-f`
- C. `-i`
- D. `-n`

**42. 以下哪个命令以制表符分隔的格式打印 `/etc/passwd` 中所有用户的用户名和真实姓名？**

- A. `cut -f 1,6 /etc/passwd`
- B. `sed 's/:/:/\' /etc/passwd`
- C. `awk -F: '{print $1,$5}' OFS="\t" /etc/passwd`
- D. `cat -o "\t" /etc/passwd`

**43. `cp` 命令的哪个选项将在递归复制时保留符号链接？**

- A. `-f`
- B. `-d`
- C. `-a`
- D. `-b`

**44. 以下哪个键组合是在 `Vi` 中移动到文件第 `23` 行的技巧？**

- A. `23G`
- B. `/23`
- C. `i23`
- D. `ZZ`

**45. `top` 命令的哪个选项可以更改更新间隔？**

- A. `-d`
- B. `-t`
- C. `-n`
- D. `-f`

**46. 以下哪个命令将显示系统进程的进程 ID、真实用户 ID、文件系统访问用户 ID 和命令？**

- A. `listproc -uf`
- B. `ps -e pid,user,comm`
- C. `ps -e pid,user,comm`
- D. `Ps -fa`

**47. 哪个命令可以搜索当前位置以下包含 `DB` 字符的文件内容？**

- A. `grep -r "DB" *`
- B. `grep -ri "DB" *`
- C. `cat * | less`

**48. 以下哪个命令和选项可以从当前目录开始查找所有以 `DB` 开头的文件？**

- A. `locate "DB*"`
- B. `find ./ -name "DB*"`
- C. `whereis "DB*"`
- D. `find "DB*"`

**49. 以下哪个文件用于 `uptime` 命令收集平均负载信息？**

- A. `/proc/uptime`
- B. `/proc/loadavg`
- C. `/proc/load`
- D. `/proc/utime`

**50. 系统包含一个无法访问的 `NFS` 挂载文件系统。应该传递哪个选项给 `unmount` 以强制卸载？**

- A. `-nfs`
- B. `--fake`
- C. `-f`
- D. `-n`

**51. `fsck` 命令的哪个选项会在尝试修复时提示？**

- A. `-y`
- B. `-f`
- C. `-r`
- D. `-a`

**52. 以下哪个文件动态更新关于已挂载文件系统的信息？**

- A. `/etc/fstab`
- B. `/etc/files`
- C. `/boot/fstab`
- D. `/etc/mtab`

**53. `repquota` 命令的哪个选项以人类可读格式输出？**

- A. `-h`
- B. `-s`
- C. `-p`
- D. `-f`

**54. 运行 `df` 命令时，需要更改 `scale` 使报告显示 `TB` 而不是字节。哪个选项可以实现？**

- A. `-S`
- B. `-B`
- C. `-j`
- D. `-T`

**55. 哪个命令可以创建 `ext3` 文件系统的重要元数据映像？**

- A. `e2image`
- B. `e3image`
- C. `dumpefs`
- D. `dumpe3fs`

**56. `mk2fs` 的哪个选项用于创建期间检查坏块？**

- A. `-a`
- B. `-b`
- C. `-c`
- D. `-d`

**57. 以下哪个命令将 `file.java` 的所有者更改为 `steve`，组为 `developers`？**

- A. `chgrp steve:developers file.java`
- B. `chown developers.file.java`
- C. `chown developers file.java`
- D. `chown file.java developers`

**58. 以下哪个描述描述了 `Bash` 中 `HISTSIZE` 和 `HISTFILESIZE` 的区别？**

- A. `HISTSIZE` 是 `.bash_history` 中保留的历史条目数，而 `HISTFILESIZE` 设置当前会话的命令数。
- B. `HISTFILESIZE` 是 `.bash_history` 中保留的历史条目数，而 `HISTSIZE` 设置当前会话的命令数。
- C. `HISTSIZE` 是 `root` 的历史大小，而 `HISTFILESIZE` 设置总历史。
- D. `HISTSIZE` 和 `HISTFILESIZE` 相同的。

**59. 在 `/etc/default/grub` 中设置哪个配置选项可以影响启动失败后的系统行为？**

- A. `GRUB_RECOVER`
- B. `GRUB_NOFAIL`
- C. `GRUB_RECORD_TIMEOUT`
- D. `GRUB_TIMEOUT`

**60. `du` 命令的哪个选项以人类可读格式打印摘要信息？**

- A. `-sh`
- B. `-h`
- C. `-s`
- D. `-su`

**61. `find` 命令的哪个选项会导致它跟随符号链接？**

- A. `-S`
- B. `-H`
- C. `-P`
- D. `-L`

### 第 25 章 ■ 测试卷 2

以下是 CompTIA LINUX+ 考试 `104` 的测试卷

![](img/84990579543ce21a46dc507fcde32_282_0.png)

# 第二部分 • LPIC-2

**1. 为了使用 `TCP Wrappers` 阻塞主机，你应该在文件中添加条目？**

A. `/etc/hosts.deny`
B. `/etc/wrappers`
C. `/etc/wrap.config`
D. `/etc/tcpwrap.conf`

**2. 以下哪个最好描述 `SQL` `WHERE` 关键字？**

A. `WHERE` 可以用于 `SELECT`、`INSERT` 和 `DELETE` 操作。
B. `WHERE` 可以用于 `SELECT` 和 `DELETE` 操作。
C. `WHERE` 是一个允许选择特定标准的的独立语句。
D. `WHERE` 用于 `GROUP BY` 子句中。

**3. 以下哪个命令为 `ps` 命令创建别名，使得当用户输入 `psa` 时会包含 `auwx`？**

A. `alias "ps auwx" = "psa"`
B. `alias psa=ps auwx`
C. `alias psa="ps auwx"`
D. `psa="=ps auwx"`

**4. `Bash` 脚本中的以下哪个条件判断将测试变量 `DAY` 是否等于 `SUNDAY`？**

A. `if ($DAY == "SUNDAY")`
B. `if ($DAY -eq "SUNDAY")`
C. `if [[ $DAY == "SUNDAY" ]]`
D. `if [ $DAY = "SUNDAY" ]`

**5. 以下哪个命令对于使当前 shell 中定义的变量对子进程可用是必要的？**

- A. `export`
- B. `source`
- C. `let`
- D. `def`

**6. 你正在观察另一个管理员在服务器上执行工作。作为工作的一部分，管理员使用了以下命令：`.variables.sh`。以下哪个等同于 `.variables.sh`？**

A. `let variables.sh`
B. `set variables.sh`
C. `source variables.sh`
D. `var variables.sh`

**7. 以下哪个命令将 `~/code/bin` 添加到路径？**

A. `PATH=~/code/bin:$PATH`
B. `PATH=/code/bin:$PATH`
C. `PATH=/home/code/bin:$PATH`
D. `PATH=${PATH:-~/code/bin}`

**8. 以下哪个显示了一个有效的 `Bash` 函数可以调用 `sayHello`？**

A. `function sayHello() { echo "hello"; }`
B. `function sayHello{}`
C. `function sayHello() { echo Hello }`
D. `function sayHello() { echo Hello }; };`

**9. 以下哪个命令向 `root` 发送邮件，主题为 `Update`，内容为 `/etc/hostname` 文件的内容？**

（注：原文选项 B 和 C 相同，此处保留原样逻辑翻译）

**10. `fsck` 命令的哪个选项会在尝试修复时提示？**

A. `-y`
B. `-f`
C. `-r`
D. `-a`

**51. 以下哪个文件动态更新关于当前已挂载文件系统的信息？**

A. `/etc/fstab`
B. `/etc/files`
C. `/boot/fstab`
D. `/etc/mtab`

**52. `repquota` 命令的哪个选项以人类可读格式输出？**

A. `-h`
B. `-s`
C. `-p`
D. `-f`

**53. 运行 `df` 命令时，需要更改 `scale` 使报告显示 `TB` 而不是字节。哪个选项可以实现？**

A. `-S`
B. `-B`
C. `-j`
D. `-T`

**54. 哪个命令可以创建 `ext3` 文件系统的重要元数据映像？**

A. `e2image`
B. `e3image`
C. `dumpefs`
D. `dumpe3fs`

**55. `mk2fs` 的哪个选项用于创建期间检查坏块？**

A. `-a`
B. `-b`
C. `-c`
D. `-d`

**56. 以下哪个命令将 `file.java` 的所有者更改为 `steve`，组为 `developers`？**

A. `chgrp steve:developers file.java`
B. `chown developers.file.java`
C. `chown developers file.java`
D. `chown file.java developers`

**57. 以下哪个描述最好描述了 `Bash` 中 `HISTSIZE` 和 `HISTFILESIZE` 的区别？**

A. `HISTSIZE` 是 `.bash_history` 中保留的历史条目数，而 `HISTFILESIZE` 设置当前会话的命令数。
B. `HISTFILESIZE` 是 `.bash_history` 中保留的历史条目数，而 `HISTSIZE` 设置当前会话的命令数。
C. `HISTSIZE` 是 `root` 的历史大小，而 `HISTFILESIZE` 设置总历史。
D. `HISTSIZE` 和 `HISTFILESIZE` 相同的。

**59. 在 `/etc/default/grub` 中设置哪个配置选项可以影响启动失败后的系统行为？**

A. `GRUB_RECOVER`
B. `GRUB_NOFAIL`
C. `GRUB_RECORD_TIMEOUT`
D. `GRUB_TIMEOUT`

**60. `du` 命令的哪个选项以人类可读格式打印摘要信息？**

A. `-sh`
B. `-h`
C. `-s`
D. `-su`

**61. `find` 命令的哪个选项会导致它跟随符号链接？**

A. `-S`
B. `-H`
C. `-P`
D. `-L`

**13. `Ubuntu` 系统中的以下哪个区域包含辅助功能信息和设置？**

A. 辅助功能 (`Accessibility`)
B. 访问与帮助 (`Access and Help`)
C. 通用使用 (`Universal Use`)
D. 通用访问 (`Universal Access`)

**14. 使用哪个命令可以设置键盘的延迟和重复率？**

A. `keyboard`
B. `kbdrate`
C. `kbd`
D. `keyrate`

**15. 以下哪个位置存储了 `LightDM` 的配置？**

A. `/etc/lightdm/`
B. `/etc/lightdm.conf`
C. `/etc/lightdm-conf`
D. `/etc/lightdm.d`

**16. 哪个变量用于指示 `GUI` 应用程序将显示的屏幕？**

A. `DISPLAY`
B. `SCREEN`
C. `LIST`
D. `XWIN`

**17. 以下哪个命令显示 `X` 窗口中窗口的统计数据和信息？**

A. `xinfo`
B. `xstats`
C. `xwin`
D. `xwininfo`

**18. 用户可以添加或删除以访问 `X` 器。哪个命令可以方便这一操作？**

A. `authorization`
B. `xhost`
C. `xwin`
D. `xconnect`

**19. `useradd` 的哪个选项设置了密码过期与账户被禁用之间的天数？**

A. `-n`
B. `-f`
C. `-e`
D. `-g`

**20. 以下哪个命令显示服务器上已当前的邮件别名？**

- A. `getent aliases`
- B. `getaliases`
- C. `listaliases`
- D. `mail aliases`

**21. `/etc/hosts.deny` 中的以下哪行配置创建了默认拒绝的策略，客户端需要在 `/etc/hosts.allow` 中被特定允许？**

- A. `*.*`
- B. `ALL: ALL`
- C. `ALL: ALL`
- D. `LOC: ALL`

**22. 以下哪个描述了以 `root` 身份运行 `atq` 命令的结果？**

- A. 列出所有用户的当前 `cron` 任务。
- B. 列出所有用户的当前 `cron` `at` 任务。
- C. 列出所有用户的当前 `cron` 和任务。
- D. 显示日志中的最后 `10` 条目。

**23. 以下哪个命令可以用于在 `Debian` 服务器设置时区？**

- A. `tzconfig`
- B. `/etc/timeconfig`
- C. `timeconfig`
- D. `timecfg`

**24. 使用 `crontab` 命令的哪个选项可以删除指定用户的所有 `cron` 任务？**

- A. `-d`
- B. `-e`
- C. `-r`
- D. `-l`

**25. `crontab` 命令的哪个选项允许你处理不同用户的任务？**

- A. `-u`
- B. `-m`
- C. `-d`
- D. `-e`

**26. 以下哪个命令显示可用的字符映射？**

- A. `charmap`
- B. `charmap -l`
- C. `locale -m`
- D. `mapinfo`

**27. 在哪个目录层次结构中可以找到有关服务器可用时区的信息？**

- A. `/usr/zoneinfo`
- B. `/usr/share/zoneinfo`
- C. `/etc/zoneinfo`
- D. `/etc/tz.conf.d`

**28. 从服务器上删除用户时，你需要保留其家目录而不是删除它。以下命令的哪个选项可以删除用户 `<username>` 但保留其家目录？**

- A. `userdel <username>`



## 第 26 章

### 练习题 3

以下是针对 CompTIA LINUX+ 考试 201 的练习题

![](img/84990579543ce21a46ac6dc507fcde32_294_0.png)

1. 在监控模式下使用 `mdadm` 时，哪个选项用于设置轮询间隔？

- A. `--delay`
- B. `--internal`

- B. `userdel -r <username>`

- C. `userdel -h <username>`

- D. `userdel -p <username>`

29. 删除组后，你需要搜索文件系统中属于该组（组 ID）的文件。`find` 命令的哪个选项将使用组 ID 进行搜索？

- A. `-user`

- B. `-group`

- C. `-groupid`

- D. `-gid`

30. 以下哪个命令将组名从 `admins` 改为 `serveradmins`？

- A. `groupmod -g admins serveradmins`

- B. `groupmod -n serveradmins admins`

- C. `groupch -n serveradmins admins`

- D. `groupch admins -n serveradmins`

31. 哪个命令用于解析基于 `systemd` 的系统的日志文件条目？

- A. `logger`

- B. `journalentry`

- C. `journctl`

- D. `journalctl`

32. 在 Red Hat 系统上，`etc/ntp.conf` 中指定的漂移文件默认存储在哪个位置？

- A. `/var/lib/ntp/drift`

- B. `/var/ntp/drift`

- C. `/usr/share/ntpdrift`

- D. `/usr/share/lib/ntpdrift`

33. `ntpdate` 命令的哪个选项配置了使用的版本，以便查询较旧的 NTP 服务器？

- A. `-o`

- B. `-v`

- C. `-e`

- D. `-r`

34. `systemd` journals 默认存储在哪个目录？

- A. `/var/log/systemd`

- B. `/var/systemd/journal`

- C. `/var/log/journald`

- D. `/var/log/journal`

35. `logrotate` 命令的哪个选项指定了使用的邮件程序？

- A. `-o`

- B. `-s`

- C. `-m`

- D. `-v`

36. `date` 命令的哪个选项将输出改为 UTC，无论当前时区如何？

- A. `-u`

- B. `-t`

- C. `-s`

- D. `-v`

37. 以下哪个命令可以用于在 `lp` 打印服务的系统中删除任务？

- A. `lpdel`

- B. `rmprint`

- C. `rm -print`

- D. `lprm`

38. 使用 `mail` 命令时，哪个字符组合将消息正文设置为 STDIN？

- A. `<`

- B. `>`

- C. `<<<`

- D. `|`

39. 以下哪个命令从 Linux 系统中删除一个组？

- A. `groupdm`

- B. `grouprm`

- C. `groupdel`

- D. `group`

40. 以下哪个 syslog 记录来自打印设施的消息？

- A. `auth`

- B. `messages`

- C. `lpr`

- D. `root`

41. 以下哪个子网掩码代表 /23？

- A. `255.255.255.0`

- B. `255.255.254.0`

- C. `255.255.255.0`

- D. `255.255.255.0`

42. `/etc/hosts.deny` 中的以下哪行配置创建了默认拒绝的策略，客户端需要在 `/etc/hosts.allow` 中被特定允许？ 以下哪个描述了以 `root` 身份运行 `atq` 命令的结果？

- A. 列出所有用户的当前 `cron` 任务。

- B. 列出所有用户的当前 `cron` `at` 任务。

- C. 列出所有用户的当前 `cron` 和 任务。

- D. 显示日志中的最后 10 条目。

43. 以下哪个命令可以用于在 Debian 服务器设置时区？

- A. `tzconfig`

- B. `/etc/timeconfig`

- C. `timeconfig`

- D. `timecfg`

44. 使用 `crontab` 命令的哪个选项可以删除指定用户的所有 `cron` 任务？

- A. `-d`

- B. `-e`

- C. `-r`

- D. `-l`

45. `crontab` 命令的哪个选项允许你处理不同用户的任务？

- A. `-u`

- B. `-m`

- C. `-d`

- D. `-e`

46. 以下哪个命令显示可用的字符映射？

- A. `charmap`

- B. `charmap -l`

- C. `locale -m`

- D. `mapinfo`

47. 在哪个目录层次结构中可以找到有关服务器可用时区的信息？

- A. `/usr/zoneinfo`

- B. `/usr/share/zoneinfo`

- C. `/etc/zoneinfo`

- D. `/etc/tz.conf.d`

48. 从服务器上删除用户时，你需要保留其家目录而不是删除它。以下命令的哪个选项可以删除用户 `<username>` 但保留其家目录？

- A. `userdel <username>`

- B. `userdel -r <username>`

- C. `userdel -h <username>`

- D. `userdel -p <username>`

49. 删除组后，你需要搜索文件系统中属于该组（组 ID）的文件。`find` 命令的哪个选项将使用组 ID 进行搜索？

- A. `-user`

- B. `-group`

- C. `-groupid`

- D. `-gid`

50. 以下哪个命令将组名从 `admins` 改为 `serveradmins`？

- A. `groupmod -g admins serveradmins`

- B. `groupmod -n serveradmins admins`

- C. `groupch -n serveradmins admins`

- D. `groupch admins -n serveradmins`

51. 哪个命令用于解析基于 `systemd` 的系统的日志文件条目？

- A. `logger`

- B. `journalentry`

- C. `journctl`

- D. `journalctl`

52. 在 Red Hat 系统上，`etc/ntp.conf` 中指定的漂移文件默认存储在哪个位置？

- A. `/var/lib/ntp/drift`

- B. `/var/ntp/drift`

- C. `/usr/share/ntpdrift`

- D. `/usr/share/lib/ntpdrift`

53. `ntpdate` 命令的哪个选项配置了使用的版本，以便查询较旧的 NTP 服务器？

- A. `-o`

- B. `-v`

- C. `-e`

- D. `-r`

54. `systemd` journals 默认存储在哪个目录？

- A. `/var/log/systemd`

- B. `/var/systemd/journal`

- C. `/var/log/journald`

- D. `/var/log/journal`

55. `logrotate` 命令的哪个选项指定了使用的邮件程序？

- A. `-o`

- B. `-s`

- C. `-m`

- D. `-v`

56. `date` 命令的哪个选项将输出改为 UTC，无论当前时区如何？

- A. `-u`

- B. `-t`

- C. `-s`

- D. `-v`

57. 以下哪个命令可以用于在 `lp` 打印服务的系统中删除任务？

- A. `lpdel`

- B. `rmprint`

- C. `rm -print`

- D. `lprm`

58. 使用 `mail` 命令时，哪个字符组合将消息正文设置为 STDIN？

- A. `<`

- B. `>`

- C. `<<<`

- D. `|`

59. 以下哪个命令从 Linux 系统中删除一个组？

- A. `groupdm`

- B. `grouprm`

- C. `groupdel`

- D. `group`

60. 以下哪个 syslog 记录来自打印设施的消息？

- A. `auth`

- B. `messages`

- C. `lpr`

- D. `root`

61. 以下哪个子网掩码代表 /23？

- A. `255.255.255.0`

- B. `255.255.254.0`

- C. `255.255.255.0`

- D. `255.255.255.0`

62. `/etc/hosts.deny` 中的以下哪行配置创建了默认拒绝的策略，客户端需要在 `/etc/hosts.allow` 中被特定允许？ 以下哪个描述了以 `root` 身份运行 `atq` 命令的结果？

- A. 列出所有用户的当前 `cron` 任务。

- B. 列出所有用户的当前 `cron` `at` 任务。

- C. 列出所有用户的当前 `cron` 和 任务。

- D. 显示日志中的最后 10 条目。

63. 以下哪个命令可以用于在 Debian 服务器设置时区？

- A. `tzconfig`

- B. `/etc/timeconfig`

- C. `timeconfig`

- D. `timecfg`

64. 使用 `crontab` 命令的哪个选项可以删除指定用户的所有 `cron` 任务？

- A. `-d`

- B. `-e`

- C. `-r`

- D. `-l`

65. `crontab` 命令的哪个选项允许你处理不同用户的任务？

- A. `-u`

- B. `-m`

- C. `-d`

- D. `-e`

66. 以下哪个命令显示可用的字符映射？

- A. `charmap`

- B. `charmap -l`

- C. `locale -m`

- D. `mapinfo`

67. 在哪个目录层次结构中可以找到有关服务器可用时区的信息？

- A. `/usr/zoneinfo`

- B. `/usr/share/zoneinfo`

- C. `/etc/zoneinfo`

- D. `/etc/tz.conf.d`

68. 从服务器上删除用户时，你需要保留其家目录而不是删除它。以下命令的哪个选项可以删除用户 `<username>` 但保留其家目录？

- A. `userdel <username>`

- B. `userdel -r <username>`

- C. `userdel -h <username>`

- D. `userdel -p <username>`

69. 删除组后，你需要搜索文件系统中属于该组（组 ID）的文件。`find` 命令的哪个选项将使用组 ID 进行搜索？

- A. `-user`

- B. `-group`

- C. `-groupid`

- D. `-gid`

70. 以下哪个命令将组名从 `admins` 改为 `serveradmins`？

- A. `groupmod -g admins serveradmins`

- B. `groupmod -n serveradmins admins`

- C. `groupch -n serveradmins admins`

- D. `groupch admins -n serveradmins`

71. 哪个命令用于解析基于 `systemd` 的系统的日志文件条目？

- A. `logger`

- B. `journalentry`

- C. `journctl`

- D. `journalctl`

72. 在 Red Hat 系统上，`etc/ntp.conf` 中指定的漂移文件默认存储在哪个位置？

- A. `/var/lib/ntp/drift`

- B. `/var/ntp/drift`

- C. `/usr/share/ntpdrift`

- D. `/usr/share/lib/ntpdrift`

73. `ntpdate` 命令的哪个选项配置了使用的版本，以便查询较旧的 NTP 服务器？

- A. `-o`

- B. `-v`

- C. `-e`

- D. `-r`

74. `systemd` journals 默认存储在哪个目录？

- A. `/var/log/systemd`

- B. `/var/systemd/journal`

- C. `/var/log/journald`

- D. `/var/log/journal`

75. `logrotate` 命令的哪个选项指定了使用的邮件程序？

- A. `-o`

- B. `-s`

- C. `-m`

- D. `-v`

76. `date` 命令的哪个选项将输出改为 UTC，无论当前时区如何？

- A. `-u`

- B. `-t`

- C. `-s`

- D. `-v`

77. 以下哪个命令可以用于在 `lp` 打印服务的系统中删除任务？

- A. `lpdel`

- B. `rmprint`

- C. `rm -print`

- D. `lprm`

78. 使用 `mail` 命令时，哪个字符组合将消息正文设置为 STDIN？

- A. `<`

- B. `>`

- C. `<<<`

- D. `|`

79. 以下哪个命令从 Linux 系统中删除一个组？

- A. `groupdm`

- B. `grouprm`

- C. `groupdel`

- D. `group`

80. 以下哪个 syslog 记录来自打印设施的消息？

- A. `auth`

- B. `messages`

- C. `lpr`

- D. `root`

81. 以下哪个子网掩码代表 /23？

- A. `255.255.255.0`

- B. `255.255.254.0`

- C. `255.255.255.0`

- D. `255.255.255.0`

82. `/etc/hosts.deny` 中的以下哪行配置创建了默认拒绝的策略，客户端需要在 `/etc/hosts.allow` 中被特定允许？ 以下哪个描述了以 `root` 身份运行 `atq` 命令的结果？

- A. 列出所有用户的当前 `cron` 任务。

- B. 列出所有用户的当前 `cron` `at` 任务。

- C. 列出所有用户的当前 `cron` 和 任务。

- D. 显示日志中的最后 10 条目。

83. 以下哪个命令可以用于在 Debian 服务器设置时区？

- A. `tzconfig`

- B. `/etc/timeconfig`

- C. `timeconfig`

- D. `timecfg`

84. 使用 `crontab` 命令的哪个选项可以删除指定用户的所有 `cron` 任务？

- A. `-d`

- B. `-e`

- C. `-r`

- D. `-l`

85. `crontab` 命令的哪个选项允许你处理不同用户的任务？

- A. `-u`

- B. `-m`

- C. `-d`

- D. `-e`

86. 以下哪个命令显示可用的字符映射？

- A. `charmap`

- B. `charmap -l`

- C. `locale -m`

- D. `mapinfo`

87. 在哪个目录层次结构中可以找到有关服务器可用时区的信息？

- A. `/usr/zoneinfo`

- B. `/usr/share/zoneinfo`

- C. `/etc/zoneinfo`

- D. `/etc/tz.conf.d`

88. 从服务器上删除用户时，你需要保留其家目录而不是删除它。以下命令的哪个选项可以删除用户 `<username>` 但保留其家目录？

- A. `userdel <username>`

- B. `userdel -r <username>`

- C. `userdel -h <username>`

- D. `userdel -p <username>`

89. 删除组后，你需要搜索文件系统中属于该组（组 ID）的文件。`find` 命令的哪个选项将使用组 ID 进行搜索？

- A. `-user`

- B. `-group`

- C. `-groupid`

- D. `-gid`

90. 以下哪个命令将组名从 `admins` 改为 `serveradmins`？

- A. `groupmod -g admins serveradmins`

- B. `groupmod -n serveradmins admins`

- C. `groupch -n serveradmins admins`

- D. `groupch admins -n serveradmins`

91. 哪个命令用于解析基于 `systemd` 的系统的日志文件条目？

- A. `logger`

- B. `journalentry`

- C. `journctl`

- D. `journalctl`

92. 在 Red Hat 系统上，`etc/ntp.conf` 中指定的漂移文件默认存储在哪个位置？

- A. `/var/lib/ntp/drift`

- B. `/var/ntp/drift`

- C. `/usr/share/ntpdrift`

- D. `/usr/share/lib/ntpdrift`

93. `ntpdate` 命令的哪个选项配置了使用的版本，以便查询较旧的 NTP 服务器？

- A. `-o`

- B. `-v`

- C. `-e`

- D. `-r`

94. `systemd` journals 默认存储在哪个目录？

- A. `/var/log/systemd`

- B. `/var/systemd/journal`

- C. `/var/log/journald`

- D. `/var/log/journal`

95. `logrotate` 命令的哪个选项指定了使用的邮件程序？

- A. `-o`

- B. `-s`

- C. `-m`

- D. `-v`

96. `date` 命令的哪个选项将输出改为 UTC，无论当前时区如何？

- A. `-u`

- B. `-t`

- C. `-s`

- D. `-v`

97. 以下哪个命令可以用于在 `lp` 打印服务的系统中删除任务？

- A. `lpdel`

- B. `rmprint`

- C. `rm -print`

- D. `lprm`

98. 使用 `mail` 命令时，哪个字符组合将消息正文设置为 STDIN？

- A. `<`

- B. `>`

- C. `<<<`

- D. `|`

99. 以下哪个命令从 Linux 系统中删除一个组？

- A. `groupdm`

- B. `grouprm`

- C. `groupdel`

- D. `group`

100. 以下哪个 syslog 记录来自打印设施的消息？

- A. `auth`

- B. `messages`

- C. `lpr`

- D. `root`



## 练习题 3

2. 假设服务器上有一个 RAID 设备，哪个 `mdadm` 选项可以启动阵列？

- A. `--assemble`
- B. `--start`
- C. `--get`
- D. `--begin`

3. 哪个命令可以将第一个 SATA 设备的第一个分区设置为 RAID 类型？

- A. `sfdisk /dev/sda fd`
- B. `sfdisk --id /dev/sda 1 fd`
- C. `sfdisk /dev/sda 1 fd`
- D. `sfdisk --list 1 fd`

4. 下哪项是用于跨系统标识 SCSI 设备的持久性名称？

- A. `iSCSIIID`
- B. `/dev/sd`
- C. `iLUN`
- D. `WWID`

5. 下哪项代表了 `iscsiadm` 用于发现 iSCSI 目标的有效模式？

- A. `discovery`
- B. `discover`
- C. `find`
- D. `list`

6. 哪个命令用于构建 LVM 缓存文件？

- A. `lvmcache`
- B. `lvcache`
- C. `vgscan`
- D. `vgcache`

7. 哪个命令显示内核已知的当前主机名？

- A. `cat /etc/passwd`
- B. `sysctl -n kernel.hostname`
- C. `sysctl -n net.host`
- D. `less /etc/hosts`

8. `/etc/ssh/sshd_config` 中的哪个选项用于提供在通过 `ssh` 登录之前显示的文件名：

- A. `Banner`
- B. `LoginBanner`
- C. `MOTD`
- D. `Message`

9. 配置脚本的哪个选项用于设置编译后代码安装的位置？

- A. `--location`
- B. `--dest`
- C. `--last`
- D. `--prefix`

10. 调用 `rsync` 的 `-a` 选项时包含了哪些选项？

- A. `-rlpt`
- B. `-rlptgo`
- C. `-rpfsxl`
- D. `-rlptgod`

11. 从控制台排排除问题时，内核消息不断打印，导致难以进行排排除。`dmesg` 的哪个选项可以停止向控制台发送消息？

- A. `-D`
- B. `-off`
- C. `-E`
- D. `-O`

12. `netstat` 的哪个选项显示有关多播组成员关系的信息？

- A. `-m`
- B. `-g`
- C. `-r`
- D. `-a`

13. `ip` 命令的哪个选项显示 DNS 名称而非仅是 IP 地址？

- A. `-n`
- B. `-f`
- C. `-r`
- D. `-a`

14. 下面哪个命令和选项允许你检查与监听套接字相关的计时信息？

- A. `ss -o`
- B. `netstat -rn`
- C. `ping -f`
- D. `ls -l`

15. 下面哪个 `dd` 命令写入 `linux.img > /dev/sdb1`？

- A. `dd if=/linux.img > /dev/sdb1`
- B. `dd of=/dev/sdb1 > linux.img`
- C. `dd if=/dev/sdb1 of=linux.img`
- D. `dd if=/linux.img of=/dev/sdb1`

16. 下哪一组 IP 地址和子网掩码对表示 /24 大小的私有网络？

- A. `192.168.3.0/255.255.255.128`
- B. `172.16.19.128/255.255.255.0`
- C. `192.168.2.0/255.255.255.0`
- D. `10.168.1.0/0.0.0.255`

17. `rsync` 的哪个选项为每个传输的目标文件创建备份？

- A. `-a`
- B. `-b`
- C. `-c`
- D. `-d`

18. `tar` 命令的哪个选项保留权限？

- A. `-x`
- B. `-v`
- C. `-z`
- D. `-p`

19. 在查看 `traceroute` 结果时，你看到 `!H`。`!H` 指代什么？

- A. Network unreachable（网络不可达）
- B. Host available（主机可用）
- C. Host unreachable（主机不可达）
- D. High length（长度）

20. 假设内核已启用策略路由，`ping` 命令的哪个选项可以适当标记发出的请求，以指示数据包应根据特定策略进行处理？

- A. `-m`
- B. `-a`
- C. `-p`
- D. `-k`

21. 哪个环境变量可以用于指定 `mount` 命令操作的默认设备？

- A. `TAPDEVICE`
- B. `MTDEVICE`
- C. `MTTAPE`
- D. `TAPE`

22. 为系统创建备份时，应该包含哪个目录以确保大多数配置文件被备份？

- A. `/var`
- B. `/opt`
- C. `/etc`
- D. `/bin`

23. 在处理 `mount` 文件时，使用哪个选项可以使进程忽略空白符？

- A. `-w`
- B. `-i`
- C. `-e`
- D. `-p`

24. 在发现模式下工作，`iscsadm` 的哪个选项设置请求之间的延迟？

- A. `-a`
- B. `-e`
- C. `-i`
- D. `-o`

25. `hdparm` 的哪个选项检查驱动器的当前电源？

- A. `-a`
- B. `-c`
- C. `-d`
- D. `-f`

26. 哪个文件包含有关交换空间和设备的信息？

- A. `/proc/swapspace`
- B. `/proc/swap`
- C. `/etc/swap`
- D. `/proc/swaps`

27. 哪个 `systemd` target 将引导到救援模式？

- A. `init`
- B. `rescue`
- C. `recovery`
- D. `recover`

28. `fsck` 的哪个选项将报告完成 `fsck` 操作所用的时间等统计信息？

- A. `-s`
- B. `-r`
- C. `-l`
- D. `-f`

29. 内核哪个 target 用于在创建配置文件时回答每一个问题？

- A. `allconfig`
- B. `config`
- C. `alloconfig`
- D. `menoconfig`

30. 下面哪个文件提供了内存利用率信息，包括缓冲区、缓存使用和若干额外项目？

- A. `/proc/meminfo`
- B. `/proc/mem`
- C. `/etc/mem`
- D. `/proc/mem_`

31. `lsblk` 的哪个选项可以显示分区的挂载点？

- A. `-n`
- B. `-f`
- C. `-r`
- D. `-a`

32. `netstat` 的哪个选项显示有关多播组成员关系的信息？

- A. `-m`
- B. `-g`
- C. `-r`
- D. `-a`

33. `ip` 命令的哪个选项显示 DNS 名称而非仅是 IP 地址？

- A. `-n`
- B. `-f`
- C. `-r`
- D. `-a`

34. 下面哪个命令和选项允许你检查与监听套接字相关的计时信息？

- A. `ss -o`
- B. `netstat -rn`
- C. `ping -f`
- D. `ls -l`

35. 下面哪个 `dd` 命令写入 `linux.img > /dev/sdb1`？

- A. `dd if=/linux.img > /dev/sdb1`
- B. `dd of=/dev/sdb1 > linux.img`
- C. `dd if=/dev/sdb1 of=linux.img`
- D. `dd if=/linux.img of=/dev/sdb1`

36. 下哪一组 IP 地址和子网掩码对表示 /24 大小的私有网络？

- A. `192.168.3.0/255.255.255.128`
- B. `172.16.19.128/255.255.255.0`
- C. `192.168.2.0/255.255.255.0`
- D. `10.168.1.0/0.0.0.255`

37. `rsync` 的哪个选项为每个传输的目标文件创建备份？

- A. `-a`
- B. `-b`
- C. `-c`
- D. `-d`

38. `tar` 命令的哪个选项保留权限？

- A. `-x`
- B. `-v`
- C. `-z`
- D. `-p`

39. 在查看 `traceroute` 结果时，你看到 `!H`。`!H` 指代什么？

- A. Network unreachable（网络不可达）
- B. Host available（主机可用）
- C. Host unreachable（主机不可达）
- D. High length（高长度）

40. 假设内核已启用策略路由，`ping` 命令的哪个选项可以适当标记发出的请求，以指示数据包应根据特定策略进行处理？

- A. `-m`
- B. `-a`
- C. `-p`
- D. `-k`

41. 哪个环境变量可以用于指定 `mount` 命令操作的默认设备？

- A. `TAPDEVICE`
- B. `MTDEVICE`
- C. `MTTAPE`
- D. `TAPE`

42. 为系统创建备份时，应该包含哪个目录以确保大多数配置文件被备份？

- A. `/var`
- B. `/opt`
- C. `/etc`
- D. `/bin`

43. 在处理 `mount` 文件时，使用哪个选项可以使进程忽略空白符？

- A. `-w`
- B. `-i`
- C. `-e`
- D. `-p`

44. 在发现模式下工作，`iscsadm` 的哪个选项设置请求之间的延迟？

- A. `-a`
- B. `-e`
- C. `-i`
- D. `-o`

45. `hdparm` 的哪个选项检查驱动器的当前电源？

- A. `-a`
- B. `-c`
- C. `-d`
- D. `-f`

46. 哪个文件包含有关交换空间和设备的信息？

- A. `/proc/swapspace`
- B. `/proc/swap`
- C. `/etc/swap`
- D. `/proc/swaps`

47. 哪个 `systemd` target 将引导到救援模式？

- A. `init`
- B. `rescue`
- C. `recovery`
- D. `recover`

48. `fsck` 的哪个选项将报告完成 `fsck` 操作所用的时间等统计信息？

- A. `-s`
- B. `-r`
- C. `-l`
- D. `-f`

49. 内核哪个 target 用于在创建配置文件时回答每一个问题？

- A. `allconfig`
- B. `config`
- C. `alloconfig`
- D. `menoconfig`

50. 下面哪个文件提供了内存利用率信息，包括缓冲区、缓存使用和若干额外项目？

- A. `/proc/meminfo`
- B. `/proc/mem`
- C. `/etc/mem`
- D. `/proc/mem_`

51. 在与磁带设备工作时，以下哪个设备名称通常表示系统上的第一个非循环 SCSI 磁带设备？

- A. `/dev/st0`
- B. `/dev/tape0`
- C. `/dev/nst0`
- D. `/dev/tape/st0`

52. 在选择要备份的目录时，应该包含哪个目录层次结构以确保邮件文件（例如包含邮件的用户邮件存留文件）被备份？

- A. `/var`
- B. `/mail`
- C. `/etc`
- D. `/usr`

53. `patch` 命令的哪个选项可以创建文件的备份？

- A. `-d`
- B. `-b`
- C. `-s`
- D. `-c`

54. `hdpar` 命令的哪个选项可以显示驱动器的扇区大小和起始偏移量等信息？

- A. `-e`
- B. `-w`
- C. `-h`
- D. `-g`

55. 使用 `systemd` 进入救援模式时，系统会向所有登录用户发送消息通知他们即将进行重启。`systemctl` 的哪个选项可以防止此消息的显示？

- A. `--suppress`
- B. `--no-wall`
- C. `--quiet-mesg`
- D. `--no-mesg`

56. 使用 `fsck` 检查 ext4 文件系统时，可以使用哪个选项显示进度指示器？

- A. `-p`
- B. `-f`
- C. `-C`
- D. `-d`

### 第 26 章 ■ 练习题 3

57. 使用哪个内核目标（target）来提供最小的内核配置？

- A. `minconfig`
- B. `min`
- C. `tinyconfig`
- D. `configsmall`

58. 以下哪个文件包含 udev 硬件数据库？

- A. `/etc/udev/hwdb.cfg`
- B. `/etc/udev/d/hwdb.txt`
- C. `/etc/udev/hwdb.db`
- D. `/etc/udev/hwdb.bin`

59. `systemd-delta mount` 的哪个选项可以用于在文件被覆盖的实例中显示文件之间的差异？

- A. `--show-diff`
- B. `--diff`
- C. `-s`
- D. `-d`

60. `mount` 命令的哪个选项可以使用 UUID 挂载分区？

- A. `-u`
- B. `-U`
- C. `-t`
- D. `-i`

## 第 27 章

# 练习题 4

以下是针对 CompTIA LINUX+ 考试 202 的练习题

![](img/84990579543ce21a46ac6dc507fcde32_306_0.png)

1. 在 BIND 主区域的区域配置语句（stanza）中，哪个选项用于指定当区域发生变化时，是否应该通知从用服务器？

- A. `slave-notify`
- B. `notify-slave`
- C. `notify`
- D. `a-notify`

2. `dnssec-keygen` 命令的哪个选项允许指定要使用的密钥大小？

- A. `-b`
- B. `-f`
- C. `-e`
- D. `-a`

3. `named-checkzone` 命令的哪个选项除了退出码外外抑制输出？

- A. `-s`
- B. `-q`
- C. `-p`
- D. `-f`

4. 创建区域文件时，一条记录包含：`www IN A 192.168.1.1.`。记录中的 `IN` 指什么？

- A. Internal（内部）
- B. Internet（互联网）
- C. Inner（内部）
- D. IN Priority

5. `rndc` 默认监听哪个端口？

- A. 53
- B. 1053
- C. 953
- D. 530

6. 哪种类型的 DNS 记录表示“起始起始”？

- A. A
- B. IN
- C. SOA
- D. NS

7. `dig` 命令的哪个选项可以将查询发送到的服务器设置为 192.168.3.2？

- A. `@192.168.3.2`
- B. `server=192.168.3.2`
- C. `server=non-default`
- D. `--query-dest=192.168.3.2`

### 第 27 章 • 练习题

8. BIND 的哪个配置指令设置了查询发送到的转发器？

- A. `forward-dest`
- B. `forward-ip`
- C. `forwarding`
- D. `forwarders`

9. 哪条 BIND 配置指令设置了发送查询的 IP 地址？

- A. `query-source`
- B. `query-ip`
- C. `query-origination`
- D. `source-ip`

10. `named-checkzone` 的哪个选项允许以规范格式（canonical format）转储区域？

- A. `-D`
- B. `-d`
- C. `-c`
- D. `-o`

11. 使用 `named-checkconf` 时，如果 BIND 运行在 chroot 环境下，应该使用哪个选项？

- A. `-c`
- B. `-t`
- C. `-f`
- D. `-r`

12. `httppasswd` 命令的哪个选项指定使用 bcrypt 加密？

- A. `-B`
- B. `-b`
- C. `-m`
- D. `-C`

13. Apache 的哪个配置选项更改了服务器为生成的文档返回版本信息的方式？

- A. `Version`
- B. `ServerVersion`
- C. `-ServerTokens`
- D. `Token`

## 第二部分 LPIC-2

14. 以下哪一个是 Apache 服务器的主主配置文件？

- A. `apache2.conf`
- B. `apache.conf`
- C. `http.cfg`
- D. `httpd.conf`

15. Squid 配置中的哪个指令允许设置 Squid 监听连接的端口？

- A. `tcp_port`
- B. `http_port`
- C. `listen_host`
- D. `ip_listener`

16. 哪个指令设置了基于 SSL 的虚拟主机公钥的路径？

- A. `SSLCertificateKey`
- B. `SSLCertificateFile`
- C. `SSLCertificatePublicKey`
- D. `File`



## 第 17 题
哪个 SSL 相关的指令设置了 Apache 服务器上可用的加密套件列表？

A. `SSLCipherList`

B. `SSLCiphers`

C. `SSLCipherSuite`

D. `LCryptoList`

## 第 18 题
在 Apache 中使用 `AuthGroupFile` 时，对于成员为 `tim` 的组 `steve`，以下哪种格式是正确的？

A. `Group: steve, tim`

B. `Group: steve tim`

C. `AdminGroup: steve tim`

D.

## 第 19 题
使用哪种 Web 服务器日志格式来记录响应中的字节数（包括 HTTP Header）？

A. `%b`

B. `%B`

C. `-b`

D.

## 第 20 题
`ca` 辅助脚本的哪个参数可以创建新的证书颁发机构？

A. `-ca`

B. `-g`

C. `-newca`

D. `-ew`

## 第 21 题
你正在寻找与服务器 SSL 配置相关的文件。在查看 `/etc/ssl` 之后，文件可能还位于哪个其他目录？

A. `/etc/sslconfig`

B. `/usr/share/ssl`

C. `/etc/pki`

D. `/etc/private`

## 第 22 题
`nmbd` 守护进程监听哪个端口？

A. 139

B. 445

C. 137

D.

## 第 23 题
`nmbd` 的哪种消息类型可以用于 Samba 广播？

A. `force-election`

B. `new-election`

C. `send-election`

D. `notify`

## 第 24 题
`net` 命令的哪个模式用于操作 Active Directory？

A. `rpc`

B. `ads`

C. `ad`

D. `activated`

## 第 25 题
以下哪个 NFS 配置选项使用了名为 `admins` 的组？

A. `-admins`

B. `group=admins`

C. `@admins`

D. `rw`

## 第 26 题
对于指定用户名 `Steve` 和密码 `Boo`，以下哪种格式是正确的？

A. `-username=Steve,password=Boo`

B. `-username password`

C. `-credentials=Steve,Boo`

D.

## 第 27 题
为了使用 Active Directory，应该设置哪个级别的安全设置？

A. `ads`

B. `ad`

C. `domain`

D. `control`

## 第 28 题
`showmount` 命令的哪个选项显示挂载的目录信息？

A. `-a`

B. `-b`

C. `-c`

D. `-d`

## 第 29 题
以下哪条命令列出当前的 Samba 共享？

A. `smbstats`

B. `smbstatus -S`

C. `smbshares`

D. `smbd`

## 第 30 题
你需要为 Samba 创建新用户。但是当你执行 `smbpasswd -a` 时发现该用户已存在。该操作的结果是什么？

A. 用户信息将被覆盖。

B. 密码将被更改。

C. 将发生错误。

D. 将创建一个重复项。

## 第 31 题
Samba 配置没有使用标准端口。`smbclient` 命令的哪个选项允许设置端口？

A. `-a`

B. `-p`

C. `-b`

D.

## 第 32 题
`dhcpd.conf` 中主机语句内部的哪个选项用于指定 DHCP 预留 IP 地址？

A. `ip-address`

B. `address`

C. `ethernet address`

D. `fixed-address`

## 第 33 题
以下哪项描述了 `slapadd` 和 `ldap` 之间的主要区别？

A. `ldap` 命令在服务器运行时使用，而 `sladd` 在离线状态下工作。

B. `ldap` 命令用于向本地数据库添加项，而 `sladd` 用于向远程数据库添加项。

C. `ldap` 命令已被废弃，改为使用 `sladd`。

D. `ldap` 命令用于 OpenLDAP，而 `sladd` 用于 Active Directory。

## 第 34 题
当 `ravdv` 启动时，如果指定的接口不存在它将退出。哪个接口选项可以改变这种行为？

A. `StartAlways`

B. `StartIfMissing`

C. `IgnoreIfMissing`

D. `MissingOK`

## 第 35 题
`dhcpd.conf` 中的哪个选项设置了池的默认租用时间？

A. `lease-duration`

B. `default-lease-time`

C. `default-time`

D. `lease-time`

## 第 36 题
`/etc/nsswitch.conf` 中的以下哪条配置行从本地文件和 LDAP 提供组成员信息？

A. `groupmembers: files ldap`

B. `groups: files ldap`

C. `group: files ldap`

D. `group [files ldap]`

## 第 37 题
`sssd.conf` 文件分为若干部分。`sssd.conf` 中的哪个部分指定守护程序的整体或通用参数？

A. `[general]`

B. `[service]`

C. `[sssd]`

D. `[main]`

### 274 第二部分 - LPIC-2

## 第 38 题
`pam_limits.so` 模块相关的配置存储哪个文件中？

A. `limits.conf`

B. `pam_limits.conf`

C. `pmlimit.conf`

D. `limitproc.cfg`

## 第 39 题
`slapcat` 的哪个选项指定了输出写入的文件？

A. `-f`

B. `-l`

C. `-o`

D. `-d`

## 第 40 题
LDIF 文件中的哪种更改类型（changetype）用于表示某条条目应该被修改？

A. `change`

B. `modify`

C. `mod`

D. `update`

## 第 41 题
LDAP 属性 `mail` 存在于哪种对象类（objectClass）中？

A. `inetOrgPerson`

B. `mailOrg`

C. `orgMail`

D. `organization`

## 第 42 题
使用 Sieve 时，哪个运算符用于测试一个值是否大于另一个值？

A. `>`

B. `greater-than`

C. `ge`

D. `gt`

## 第 43 题
Dovecot 的配置文件存储在哪个目录下？

A. `/usr/dvecot`

B. `/etc/dvecot`

C. `/etc/dovecot.conf.d`

D. `/etc/dove.cfg.d`

## 第 44 题
以下哪个命令是打印邮件队列的 `sendmail` 命令？

A. `sendmail -q`

B. `sendmail -bp`

C. `sendmail -bq`

D. `sendmail -mailq`

## 第 45 题
以下哪个命令删除了 Postfix 延迟队列（deferred queue）中的所有消息？

A. `postsuper -d DEFERRED`

B. `postqueue -d DEF`

C. `postsuper -d ALL deferred`

D. `postqueue -d ALL`

## 第 46 题
以下哪个选项可以与 `postcat` 使用以仅显示消息正文？

A. `-m`

B. `-e`

C. `-h`

D. `-b`

## 第 47 题
以下哪个 Sieve 测试会匹配大于 500 KB 的消息？

A. `if message > 500`

B. `if size :over 500K`

C. `if messagesize > 500K`

D. `if size :morethan 500`

## 第 48 题
以下哪个命令产生适用于 Dovecot 的密码？

A. `dovepass`

B. `doveadm pw`

C. `dovepasswd`

D. `doveadm pass`

## 第 49 题
Postfix 配置中的哪个参数设置了单条消息的限制？

A. `message_size_limit`

B. `message_max`

C. `message_size`

D. `max_message_size`

## 第 50 题
在 Sieve 中，哪种地址部分结构用于表示整个电子邮件地址？

A. `:email`

B. `:address`

C. `:all`

D. `:full`

## 第 51 题
使用 Telnet 等工具测试 SMTP 协议时，以下哪行指定了作为 SMTP 会话一部分的目的地址？

A. `RCPT TO`

B. `MAILTO`

C. `DEST`

D. `TO`

## 第 52 题
以下哪个 `iptables` 目标（target）用于创建端口重定向？

A. `PORTDIR`

B. `PORTREDIR`

C. `REDIR`

D. `REDIRECT`

## 第 53 题
哪个 Pure-FTPd 指令用于限制认证用户的带宽？

A. `-T`

B. `-B`

C. `-b`

D. `-t`

## 第 54 题
以下哪个命令通过标准 HTTP 端口连接到 `www.example.com`？

A. `nc www.example.com`

B. `nc www.example.com 80`

C. `nc www.example.com:80`

D. `nc www.example.com:http`

## 第 55 题
以下哪个命令清除给定链（chain）的规则？

A. `iptables -P`

B. `iptables -C`

C. `iptables -F`

D. `iptables -N`

## 第 56 题
哪个 OpenSSH 配置指令用于指定允许使用 SSH 登录的用户？

A. `AllowUsers`

B. `PermitUsers`

C. `UsersAllowed`

D. `AllowedUsers`

# 第 27 章 ■ 练习测试 4 277

## 第 57 题
以下哪个命令防止数据包从与接收数据包接口不同的接口发出？

A. `iptables --no-redirect`

B. `echo "1" > /proc/sys/net/ipv4/conf/all/rp_filter`

C. `echo "1" > /proc/sys/net/ipv4/conf/all/redirect_filter`

D. `echo "1" > /proc/sys/net/ipv4/conf/all/pf`

## 第 58 题
以下哪个命令创建了一个本地端口转发场景，其中到端口 `8080` 的连接将通过 `ssh.example.com` 服务器发送到 `www.example.com` 的 `80` 端口？

A. `ssh --forward 80:www.example.com:8080 ssh.example.com`

B. `ssh -p 8080:www.example.com:80 ssh.example.com`

C. `echo ssh.example.com -F 8080`

D. `ssh -L 8080:www.example.com:80 ssh.example.com`

## 第 59 题
使用 `netstat -a` 时，查询哪个文件用于端口号到名的转换？

A. `/etc/portnum`

B. `/etc/services`

C. `/etc/portnames`

D. `/proc/sys/net/ipv4/ports`

## 第 60 题
`iptables` 的 `LOG` 目标中的哪个选项用于设置附加在日志项前的字符串？

A. `--log-prefix`

B. `--prepend`

C. `--log-prepend`

D. `--log-str`

# 附录

# 复习题

![](img/8490579543ce21a46dc507fcde321_0.png)

# 第一章：系统架构（领域101）

1. 1. C SATA 磁盘的地址为 `/dev/sdx`，就像 SCSI 磁盘一样。
2. 14. B SATA 磁盘的地址为 `/dev/sdx`，就像 SCSI 磁盘一样。
3. 15. C SATA 磁盘的地址为 `/dev/sdx`，就像 SCSI 磁盘一样。
4. 16. D SATA 磁盘的地址为 `/dev/sdx`，就像 SCSI 磁盘一样。
5. 17. A SATA 磁盘的地址为 `/dev/sdx`，就像 SCSI 磁盘一样。
6. 18. B SATA 磁盘的地址为 `/dev/sdx`，就像 SCSI 磁盘一样。
7. 19. C SATA 磁盘的地址为 `/dev/sdx`，就像 SCSI 磁盘一样。
8. 20. D SATA 磁盘的地址为 `/dev/sdx`，就像 SCSI 磁盘一样。
9. 21. A SATA 磁盘的地址为 `/dev/sdx`，就像 SCSI 磁盘一样。
10. 22. B SATA 磁盘的地址为 `/dev/sdx`，就像 SCSI 磁盘一样。
11. 23. C SATA 磁盘的地址为 `/dev/sdx`，就像 SCSI 磁盘一样。
12. 24. D SATA 磁盘的地址为 `/dev/sdx`，就像 SCSI 磁盘一样。
13. 25. A SATA 磁盘的地址为 `/dev/sdx`，就像 SCSI 磁盘一样。
14. 26. B SATA 磁盘的地址为 `/dev/sdx`，就像 SCSI 磁盘一样。

（注：原文中答案部分的 OCR 文本似乎存在重复/损坏；已根据提供的结构进行了格式清理。）

# 第一章：系统架构（领域101）

（此处重复上方内容以保持格式）

1. 1. C SATA 磁盘的地址为 `/dev/sdx`，就像 SCSI 磁盘一样。
2. 14. B SATA 磁盘的地址为 `/dev/sdx`，就像 SCSI 磁盘一样。
3. 15. C SATA 磁盘的地址为 `/dev/sdx`，就像 SCSI 磁盘一样。
4. 16. D SATA 磁盘的地址为 `/dev/sdx`，就像 SCSI 磁盘一样。
5. 17. A SATA 磁盘的地址为 `/dev/sdx`，就像 SCSI 磁盘一样。
6. 18. B SATA 磁盘的地址为 `/dev/sdx`，就像 SCSI 磁盘一样。
7. 19. C SATA 磁盘的地址为 `/dev/sdx`，就像 SCSI 磁盘一样。
8. 20. D SATA 磁盘的地址为 `/dev/sdx`，就像 SCSI 磁盘一样。
9. 21. A SATA 磁盘的地址为 `/dev/sdx`，就像 SCSI 磁盘一样。
10. 22. B SATA 磁盘的地址为 `/dev/sdx`，就像 SCSI 磁盘一样。
11. 23. C SATA 磁盘的地址为 `/dev/sdx`，就像 SCSI 磁盘一样。
12. 24. D SATA 磁盘的地址为 `/dev/sdx`，就像 SCSI 磁盘一样。
13. 25. A SATA 磁盘的地址为 `/dev/sdx`，就像 SCSI 磁盘一样。
14. 26. B SATA 磁盘的地址为 `/dev/sdx`，就像 SCSI 磁盘一样。

# 附录 ■ 复习题答案

26. C. 当启动选项被高亮时，按 `E` 进入编辑会话。你可以进行更改，完成后完成后按 `B` 启动系统。
27. A. 在 `grub >` 提示符下执行 `ls` 命令将以类似于 `(hd0,1)` 的格式显示可用的分区。
28. D. 文件 `/var/log/dmesg` 通常包含来自系统当前启动的历史性消息。在某些 Linux 发行版中，这些信息也位于 `/var/log/boot.log` 中。
29. C. 在给出的选项中，`systemctl status` 命令是最合适的。`telinit` 和 `systemctl` 命令不用于此目的。同样，`--ls` 选项对 `systemctl` 来说是无效。
30. B. `isolate` 选项用于将系统移动到指定的目标，因此选项 B 是正确答案。其他选项不存在。
31. A. `initctl reload` 命令会导致 Upstart 重新读取其配置文件。
32. B. `--list` 选项将显示系统中所有的服务及其在每个运行级别下的状态。
33. C. USB 设备通常被认为是热插拔设备。热插拔设备指的是那些在系统“热运行”（即开机）时可以插入和移除的设备，而冷插拔设备是指必须在系统关机时插入和移除的设备。
34. D. 根分区在设备初始化后挂载。系统服务（包括多用户模式）在根分区挂载后启动。另外两个选项 A 和 C 发生在内核初始化设备驱动程序之前。
35. A. 使用电缆选择（cable select），ATA 驱动器将按照它们从主板连接电缆的顺序被检测。可能需要通过电缆物理上交换驱动器。
36. B. `umount` 命令用于在运行的系统中卸载驱动器。其他命令不存在。
37. D. ESP 通常挂载在 `/boot/efi`。
38. A. `mount` 命令用于在 Linux 中挂载驱动器。源和挂载点作为参数指定。驱动分区从数字 1 开始，使得第一个分区为 1。
39. D. 在给出的选项中，运行 `dmesg` 是查找内核为驱动器分配位置的常用方法。重启系统不是一个好的选择，尽管它有效。并没有像 `/var/log/usb.log` 这样的文件，且驱动器位置可能会随端口而变化，取决于系统如何检测驱动器。
40. 在这些选项中，只有 B 会立即关闭系统。答案 A 将取消关机。

# 第 2 章：Linux 安装与包管理（领域 102）

- 41. C. `ExecStart` 选项表示在 systemd 服务启动时执行的命令。
- 42. D. `systemctl get-default` 命令将显示默认目标（target）。其他命令和选项均无效。
- 43. A. `enable` 选项配置服务在启动机时启动。`start` 选项（答案 D）用于立即启动服务。其他选项对该命令无效。
- 44. C. `/proc` 文件系统包含当前正在运行进程的信息，以及关于内核和系统当前启动的其他信息。
- 45. C. `lsusb` 的 `-t` 选项将以树状格式打印输出，你可以看到哪些设备连接到哪个总线。`lsusb` 的其他参数无效，且 `usblist` 命令并不存在。
- 46. A. 根据 SCSI 类型，每个 SCSI 总线支持 7 到 15 个设备。
- 47. D. 如果设备没有出现在 `lsmod` 中，通常意味着驱动程序已经编译到内核中，而不是通过模块加载。使用 `systemd`（答案 A）或 `initfs`（答案 B）没有影响。



48. C. `-w` 选项导致模块在卸载前等待直到它不再被需要。`-f` 选项强制立即移除，应谨慎使用。其他选项对 `rmmod` 无效。

# 第 2 章：Linux 安装与包管理（领域 102）

1. D. 包含 `/var` 的分区对于邮件服务器应该是最大的，因为邮件池（mail pools）存储在这个层次结构中。`/etc` 目录通常很小，`/usr/bin` 也是如此。邮件目录默认不存在。

2. C. `rootnofexec` 选项用于指定 GRUB 应尝试加载的非 Linux 内核。`initrd` 选项用于指定 init RAM 磁盘，因此选项 A 是正确的。其余选项 B 和 D 不是 GRUB 的有效选项。

3. C. `noexec` 选项将防止位于该分区上的程序被执行。`noexec` 选项用于频繁挂载 `/tmp` 分区。

4. A. `update-grub` 命令将其输出发送到标准输出（STDOUT）。因此，你必须使用 `>` 重定向并将输出发送正确的文件。其他选项对该目的无效。答案 C 和 D 不是有效命令，而 B 包含无效选项和无效的目标文件位置。

5. B. 基于 MBR 的磁盘可以被划分为四个主分区，其中一个可以被进一步分区或扩展为逻辑分区。

6. D. `ldconfig` 命令更新当前的共享库缓存并读取 `/etc/ld.so.conf`，合并其中发现的任何更改。其他选项无效。

7. B. `upgrade` 选项用于 `apt-get` 将更新系统。

8. C. `yum install` 将安装软件包。

9. C. 邮件目录默认不存在。

10. A. 根目录是 `/root`。

11. B. `ext4` 是文件系统。

12. `/sbin` 目录包含系统命令。

13. B. GRUB 默认值从 0 开始计数。

14. A. `/etc/default/grub` 文件用于此目的。

15. B. `dpkg` 选项显示已安装的软件包。

16. A. `rpm -V` 将检查软件包中的文件。

17. B. `export` 命令用于设置环境变量。

18. D. `yumdownloader` 将下载软件包，而不是安装。

19. A. `apt-cache` 命令用于软件包缓存。

20. C. `/etc/default/grub` 文件用于配置系统。

# 第 2 章：Linux 安装与包管理（领域 102）

21. A. `ro` 选项将根挂载为只读。

22. D. `/etc/yum.repos.d` 包含存储库文件。

23. B. `yum.conf` 是一个文件。

24. C. `-o` 选项可以将输出重定向到文件而不是标准输出。

25. A. `.menu` 文件用于 GRUB。

26. D. `ldd` 命令将列出命令所依赖的库。

27. B. 当内存不足时使用交换空间。

28. B. `/etc/lib` 目录通常与库文件相关，在手动创建的 Linux 系统不存在。

29. C. `apt-get update` 命令通过从源更新软件包缓存。

30. C. `/etc/apt/sources.list` 包含 Debian 软件包源列表。

31. A. `/boot` 分区将远小于 500 MB，但不应这样使用。

32. B. `pvcreate` 命令初始化物理分区以便将来作为逻辑卷使用。

33. D. `grub-install` 命令用于将 GRUB 安装到磁盘上，SATA 磁盘将是 `/dev/sdb`，使得答案 D 是正确选项。你可以在不同的磁盘上使用 `grub-install` 以提供备用或备份启动选项。

34. A. `dpkg-reconfigure` 程序会导致已安装的软件包被重新配置或更改。`dpkg` 的 `-r` 选项用于移除软件包，使得 B 错误。

35. C. `lvcreate` 命令用于使用 LVM 创建逻辑卷。

36. A. 首先初始化物理卷，然后创建卷组，最后创建逻辑卷。

37. D. `aptitude` 提供的是基于终端的界面，而不是此问题中列出的其他工具的标准命令行界面。

38. D. `-search` 选项会对包名和描述等各种字段进行搜索。

39. B. `rpm -q kernel` 命令将显示内核版本。你也可以使用 `uname -r` 同样的目的。

40. C. `/etc/default/grub` 中的 `GRUB_DEFAULT` 选项将设置默认启动的操作系统。

41. A. 排除 (exclude) 选项可以用于排除某些软件包。该参数接受通配符，排除所有 `kernel*` 将产生所需的行为。

42. B. 新的 Linux 分区应创建类型为 0x83 的分区。类型 82 用于交换分区（swap），而 84 用于 OS/2 分区。

43. B. 修改 `/etc/default/grub` 文件后，应该运行 `grub-mkconfig` 命令，以便使用更改后的选项创建新配置。

44. B. `dpkg` 的 `-s` 选项搜索指定的软件包并提供其在系统上当前状态的信息。`apt-cache` 命令不用于此目的，`dpkg` 的 `-i` 选项用于安装软件包。`apt-info` 命令不存在。

45. C. `lvdmscan` 命令查找已初始化用于 LVM 的物理卷。

46. B. `--resolve` 选项将下载已下载包的依赖项。此问题中显示的其他选项对 `yumdownloader` 命令无效。

47. A. `dpkg` 的 `-i` 选项将安装之前下载的软件包。其他命令不存在，`dpkg` 的 `-u` 选项也不存在。

48. D. GRUB Legacy 从 0 开始计数并用逗号分隔磁盘字母和分区，从而使得 0,0 成为第一块磁盘上的第一个分区。答案 A 不是系统上的第一个磁盘，答案 B 和 C 包含不存在的分区或设备。

## 第 3 章：GNU 和 Unix 命令（领域 103）

1. B. `env` 命令将打印 Bash 的当前环境变量。`printenv` 命令也将执行相同的操作。此问题中列出的其他命令不存在。

2. `set` 命令可以用于多种用途来更改 shell 环境。其中一个选项是 `-C`，它可以防止输出重定向（如使用 `>`）在文件已存在时覆盖文件。

3. `man` 命令显示作为参数给出的命令的文档。此答案中列出的其他选项不存在。

4. `uname` 命令用于打印系统信息，`-a` 选项打印 `uname` 可用的所有信息。

5. `g` 选项（也称为贪婪模式 greedy）将匹配匹配的选项应用于整行，而不仅仅是匹配的第一个实例。其他选项应为 Perl 兼容正则表达式（PCRE）的选项。

6. `-l` 选项提供输入的行数。`wc -l /etc/passwd` 打印 `/etc/passwd` 文件的行数。此问题中提供的其他选项对 `wc` 命令无效。

7. `head` 和 `tail` 默认都打印 10 行输出。

8. `rm` 的 `-rf` 选项将递归删除目录的内容，包括目录本身。由于存在额外的目录，`-f` 选项在此情况下也不起作用。`rmdir` 提供的其他选项不存在。

9. `find` 命令的 `-type` 选项将其搜索限制为目录，而 `-name` 选项返回重命名项的名称。注意由于问题的表述，使用了通配符。还要注意使用 `./` 表示在当前目录中搜索。

10. `cat` 命令将显示 `/etc/passwd` 文件的内容并将该输出传递给 `awk` 命令。`awk` 命令解析其输入，并根据 `/etc/passwd` 指定的分符（即冒号 `:`）进行分割。输出被打印并传递给 `sort` 命令。B 中的 `sort` 命令将无法工作，因为 `cat` 命令需要一个参数。同样，C 中的 `echo` 命令也可以用于分割输入，但它是基于固定宽度的，这在处理密码文件输入时是不可行的。`tr` 命令是 `awk` 命令的典型伙伴，有助于构建 `awk` 输出的字符。

11. `ls` 的 `-l` 选项按时间戳产生列表输出。`-r` 选项反转顺序，需要 `-a` 来包含隐藏（点）文件，使得答案 C 正确。

12. 在已存在的文件上运行 `touch`，文件时间戳将会更改。

13. `-i` 选项会导致 `cp` 和 `mv` 都变为交互式模式，即在覆盖之前提示。`-f` 选项将允许命令运行，而 `-r` 是递归的。

14. `tee` 命令将输出发送到标准输出 (stdout) 和指定的文件，因此答案 C 正确。选项 A 将输出重定向到正确的文件，但不会同时重定向到标准输出。其他答案对此问题无效。应该注意 `cat` 或 `tee` 没有特定的格式。如果文本处理需要格式，可以使用 `fmt` 命令。

15. `-p` 选项将导致 `mkdir` 创建额外的目录层级而不报错。不带选项运行 `mkdir` 将不起作用。`mkdir` 的 `-r` 和 `-f` 选项不存在。

16. `-R` 选项将递归复制目录。`-v` 选项增加详细性但不会导致递归。`-z` 选项不存在。

17. `file` 命令可以确定正在使用的文件类型。选项 A `grep` 在文件内部查找。`telnet` 和 `export` 命令不用于此目的。

18. `dd` 命令用于创建磁盘镜像等。在此情况下，输入文件是 `/dev/sda1`，输出文件是 `output`。通常使用 `bs` 参数添加块大小，如 `bs=1M`。

19. `cut` 命令使用制表符作为默认分隔符。可以通过 `-d` 选项更改。必须使用 `cut` 命令对或多个文件应用过滤器，以便可以使用 `join` 或 `paste` 命令连接。如果需要将空格转换为制表符，可以使用 `unexpand` 命令以及 `expand` 命令。然而，你也可以更改 `cut` 使用的分隔符。

20. A. `-z` 选项将解压缩文件，`-x` 从存档提取，`-f` 用于指定执行上述操作的文件。通常还会添加 `-v` 以获得详细输出。

21. `fg` 命令将通过 `&` 或 `bg` 命令后台运行的命令带回前台。你可能将命令或进程放入后台，以便在注销后继续运行。

22. 虽然带有 `grep` 的 `ps aux` 命令可以提供运行中的 Apache 实例的信息，但它提供的信息比问题需要的多。`grep` 命令提供了进程 ID，因此符合问题提出的标准。

23. D. `top` 命令用于持续监控 CPU 和内存使用等情况，`-p` 选项监控单个进程。通过对 `pidof` 命令使用引号，可以将进程 ID 作为输入提供给 `-p` 选项。

24. D. `free` 命令显示内存和交换内存总体使用情况，并可确定何时需要额外内存。

# 第 3 章：GNU 和 Unix 命令 (领域 103)

27. A. `uptime` 命令显示基本信息，如问题中所描述的内容，以及登录系统的用户数和当前时间。`bash` 命令是一个 shell 环境，而 `ls` 命令不会显示所需信息。

28. D. `screen` 命令启动一个新的终端，可以根据需要断开并重新连接。在 `screen` 会话中运行的进程不知道自己正在运行于 `screen` 会话，因此这符合该题所需的标准。`fg` 或 `bg` 命令不符合标准，而 `kill` 命令会停止进程。

29. C. `-9` 选项调用 SIGKILL，这将强制终止进程。`-f` 和 `-stop` 选项不存在。某些命令可能是使用 `nohup` 启动的，这意味着它们对其他信号可能引起的挂起。注意，你可以使用 `pkill` 命令杀死一组命令，而不是逐个 `kill`。

30. C. 在 Bash 中，数字 1 代表 stdout，2 代表 stderr。同时重定向两者意味着以 C 所示的方式对它们进行重定向。

31. B. `nice` 命令在不带参数运行时，将输出登录用户的优先级，正常情况下为 0。`renice` 命令可更改运行进程的优先级。此题的另外两个选项不存在。

32. D. 在正则表达式中，`*` 代表零或多个字符，在这种情况下，问题不在于用户是否在使用 `/bin/bash` 还是 `/usr/bin/zsh`。同样，`.` 匹配单个字符，但在 bash 和 zsh 的情况下，我们需要查看第一个以及可选的第二个字符。最后，`$` 将模式锚定在字符串结尾，这也是该正则表达式的关键。`grep` 命令等同于 `grep -e`，`fgrep` 等同于 `grep -F`，两者都已弃用。更多信息请参阅 `regex(7)`。

33. A. 通过在参数前加上所需的级别来访问菜单的不同层级。其他选项（如 `~list`）在此上下文中不存在。

34. C. `o` 命令在当前光标位置下方打开一个新行。该命令在字符之后开始插入模式，而不是在行之后。`i` 命令在当前光标位置开始插入模式。

35. A. 在 `kill` 命令中发送 `-HUP` 将重启进程。在其他答案中，`-9` 将完全杀死进程。另外两个答案并不是杀死进程的有效手段。

36. B. `history` 命令将显示你的命令历史，包括当前会话的命令。你可以指定显示多少行历史，如该题的答案所示。`.bash_history` 不显示当前会话的历史。

37. C. `jobs` 内置命令显示后台运行的作业列表。它的输出包括作业编号和作业状态。

38. B. `find` 命令以路径开头，然后是 `-name` 参数，将定位所有名为 `.bash_history` 的文件。`find` 命令的输出应该通过管道给 `xargs`，`xargs` 然后可以从标准输入构建命令。注意，此题和答案假设所有用户都使用 Bash shell 并保留历史。

39. C. `tail` 命令提供作为参数的文件末尾部分。添加 `-f` 选项将导致输出在有新行添加到文件尾部时进行更新。

40. D. `nl` 命令将在作为参数的文件前加上行号。输出随后发送到 stdout。在其他答案中，`wc -l` 将打印文件的行数，但不会在每行上加上数字，正如本题要求的那样。

41. A. `xz` 命令可以压缩和解压多种格式的文件，其中一种是独特的。

42. `find` 命令用于此目的。添加 `-type f` 将搜索限制为仅文件，`-mtime` 选项将限制为修改时间（天）。

43. C. `mv` 命令用于移动文件，`*.txt` 将查找所有扩展名为 `.txt` 的文件。注意带有 `/` 的完整目标路径。

44. D. `pwd` 命令显示当前工作目录。`cd` 命令更改目录。

45. A. 文件首先需要排序以将邮政编码分组在一起。之后，将输出管道到 `uniq` 将显示唯一的邮政编码，`-c` 选项提供计数。

46. A. 在命令前加上 `!` 将搜索历史并执行指定的命令。例如，`!vi` 将启动你上一次的 vi 会话。

47. C. `killall` 用于通过名称终止进程。

48. C. `?` 将会在文件中反向搜索。`/` 用于正向搜索。`h` 键将光标向左移动一个字符，`x` 键将删除一个字符。

# 第 4 章：设备、Linux 文件系统和文件系统层次结构 (领域 104)

1. A. `which` 命令返回给定命令的完整路径，它对于判断给定命令是否可用以及命令从何处运行很有用。

2. B. `chgrp` 命令可更改文件的组所有权。顺序为 `chgrp <groupname> <target>`。

3. C. 该文件几乎是原始脚本的所有硬链接。虽然 `ls` 不会显示此信息，但 `stat` 命令将显示它是一个链接，并显示文件链接的 inode。

4. A. `df` 的 `-i` 选项产生跨所有文件系统的 inode 信息。`ls -i` 选项将产生 inode 列表，但仅针对当前目录。`-i` 选项对 `du` 无效，且 `dm` 不是一个命令。

5. C. `-y` 选项将尝试自动重复，本质是回答 `y` 或 `yes`，而不是提示。在其他选项中，只有 `-V` 是有效的且会产生详细输出。

# 第 4 章：设备、Linux 文件系统和文件系统层次结构 291

6. 第一步是使用 `fdisk` 创建一个或多个分区，然后格式化分区。`fdisk` 命令用于各种类型的磁盘，包括基于 MBR 的分区。

7. `tune2fs` 命令可用于此，但应谨慎使用，因为它可能导致数据损坏。

8. `ext3` 中增加日志功能提高了文件系统的可靠性和性能。

9. `-s` 选项以 `u=frwx,g=rx,o=rx` 等格式显示输出。该问题列出的其他选项不存在。

10. `-s` 选项用于创建符号链接（symlink）。

11. `whereis` 命令显示关于参数命令的相关信息。例如，Debian 系统上的 `whereis apache2` 将显示二进制文件、配置文件和其他相关细节。

12. `PRUNEPATH` 选项接受空格分隔的路径列表，以便从结果中移除。此题列出的其他选项不存在。

13. `/srv` 层次结构用于服务器程序。`/etc` 层次结构用于配置，而 `/var` 也用于变量，例如邮件文件。`/tmp` 目录用于临时文件。

14. `chmod` 命令用于此目的，`u+s` 选项为用户设置粘滞位。

15. `-a` 选项挂载 `/etc/fstab` 中当前可用的文件系统。在列出的其他选项中，只有 `-f` 选项在使用，它是“fake”选项的快捷方式，除了运行外什么都不做。

16. `mkswap` 命令格式化交换分区。`fdisk` 命令用于创建分区但不格式化。另外两个选项不存在。

17. `tune2fs` 命令显示关于文件系统的大量信息，包括文件挂载次数。

18. `-g` 选项显示 `dump` 的进度。其他选项列表不存在。

19. `quota` 命令用于更新文件系统的配额。`quota -u` 命令将显示给定用户的当前配额。其他命令不存在。

20. `du` 命令将递归地报告磁盘使用情况，与此处显示的其他命令不同。



- 21. `/etc/fstab` 文件用于存储系统内挂载的文件系统信息。

- 22. `/media` 挂载点用于可移动介质。关于 FHS 的更多信息请参阅 `https://wiki.linuxfoundation.org/en/FHS`。

- 23. `/etc/mtab` 文件包含当前挂载的文件系统。注意 `/etc/fstab` 包含文件系统信息，但不包含哪些文件系统当前挂载的信息。

# 附录 ■ 复习题答案

24. B. `-r` 选项使 `mount` 尝试以只读模式重新挂载。`-v` 选项是详细模式，`-f` 选项强制执行操作。`-o` 选项不存在。

25. C. `022` 掩码会将新的不可执行文件转换为 `644` 权限。

26. B. 列表中的 `l` 表示符号链接（symlink）。目录将显示 `d` 而不是 `l`。符号链接不是文件的拷贝，类似于快捷方式。对符号链接内容的更改也会影响到源文件。

27. B. `repquota` 命令用于此目的，`-a` 选项将显示所有文件系统的信息。

28. C. `updatedb` 命令将使用 `locate` 命令更新数据库。

29. A. `type` 内建命令返回 shell 运行给定命令时将使用的位置，其他命令均不存在。

30. B. `-R` 选项将以递归方式执行所有权更改。

31. D. 正确的顺序是设备（UUID 或分区），随后是挂载该设备的目录，然后是其选项，最后是 `dump` 和 `fsck` 命令。

32. A. `blkid` 命令将显示分区 UUID。你也可以通过 `lsblk -no UUID <partition>` 命令获取此信息。问题中显示的其他命令无法完成所需任务。

33. D. `xfs_info` 命令等于 `xfs_growfs -n`。

34. B. `mkfs.btrfs` 用于创建 `btrfs` 文件系统，且不需要对驱动器进行分区。

35. C. `usquota` 将在指定的挂载点上启用用户级配额。这通常在 `/etc/fstab` 中设置。

36. A. 这些选项中最佳选项是将组更改为 `www-data` 并更改权限，使组能够写入该目录。不应使用选项 B，因为它允许所有人对该目录进行写入。其他选项将不允许 Web 服务器写入该目录。

37. A. `tune2fs` 命令用于此目的，`-c` 选项设置指定分区的挂载计数。

38. B. 可以使用 `parted` 命令以这种方式调整分区大小。`mkfs` 命令不用于此目的，另外两个选项不存在。

39. C. VFAT 文件系统在 `mount` 命令中称为 `vfat`，且 `mount` 命令的所有元素都是标准的。

40. D. `gdisk` 中的 `c` 选项用于更改分区名称。`n` 选项创建新分区，`v` 选项验证磁盘，`b` 选项将 GPT 数据备份到文件中。

41. C. `-b` 选项打印已知的坏块。`-f` 选项用于强制显示信息，其他选项不存在。

# 第 5 章：使用 Shell、脚本编写和数据管理（领域 105）

- 42. B. `-A` 选项检查 `/etc/fstab` 中的所有文件系统，而 `-M` 选项排除根文件系统。将运行的 `fsck` 取决于文件系统的类型。例如，对于 `ext2` 分区将执行 `efsck`。

- 43. B. `quotaman` 表示应该对给定的文件系统启用配额。这意味着已经创建了配额文件。可以使用 `edquota` 命令编辑配额。

- 44. C. `fsck` 选项在 `/etc/fstab` 文件中以数字表示，设置了启动时检查设备的顺序。

- 45. D. `-c` 选项首次创建文件。`-f` 选项用于强制检查，`-u` 用于不尝试以只读模式重新挂载。

- 46. C. 可以使用 `debugfs` 命令此目的。当使用 `-c` 打开时，文件系统将以只读模式打开，且打开时不会读取 inode。

- 47. D. `-inum` 选项通过 inode 号搜索文件。这在搜索涉及硬链接的文件时非常有用。

- 48. C. `-R` 选项设置递归选项，这意味着 `chgrp` 将遍历给定目录并在指定的层级中执行组所有权更改操作。

- 1. C. `source` 命令用于从文件执行命令。一个典型的用例是创建函数或变量，然后在当前会话中使用这些内容。列出的其他命令不存在。

- 2. 虽然每个用户都有 `.bash_logout`，但该文件存在于他们的家目录中并可以由用户编辑。因此，为了确保在注销时执行所需的命令，必须使用 `/etc/bash.bash_logout` 文件。

- 3. B. `env -u` 命令用于取消当前会话的环境变量。`unset` 命令也可用于此。

- 4. A. `env` 命令当用作 `#!/usr/bin/env bash` 时，将自动确定 Bash 解释器的位置。这使得脚本对于 Bash 可能不在 `/bin/` 下的系统更具可移植性。你可以使用此命令作为为跨平台使用自定义 shell 的方法。可以按顺序为大部分中的命令创建小型脚本。

- 5. `SELECT` 命令用于检索数据，而 `*` 获取所有数据。`SELECT` 语句包括查询部分，随后是 `FROM`，然后是源。

- 6. `alias` 命令用于此目的，其格式为 `name=value`，因此答案是 A。

- 7. 用户配置文件的顺序为 `.bash_profile`、`.bash_login` 和 `.profile`。只执行第一个文件，其他的会被忽略。

- 8. `$1` 变量在 Bash 脚本中自动可用并代表第一个命令行参数。`$0` 变量是脚本本身。问题中的变量不存在。

- 9. `fi` 结构用于表示条件的结束。在许多语言中，条件由大括号 `{ }` 限定，但在 shell 脚本中，使用 `fi` 来表示结束。

- 10. `DELETE FROM` 命令删除表中的所有数据。注意 MySQL 通常对大小写敏感，因此需要遵循大小写。

- 11. `DESCRIBE` 命令用于提供表的列和列类型描述。在所示的选项命令中，只有 `SELECT` 是有效的 SQL 命令，且它用于检索数据而不是表本身的描述。

- 12. `seq` 命令用于以各种格式提供数字序列。问题的答案提供了一个起点（0）、一个增量（1）和一个结束数字（5），导致输出六个数字。

- 13. `echo` 命令用于显示其参数，无论该命令是在 shell 脚本内部还是从命令行使用。`env` 命令用于显示环境变量，因此不符合问题需求。

- 14. SUID 位允许程序以用户所有者的身份运行，无论谁执行该程序。出于安全考虑，通常不建议 SUID。

- 15. `exec` 命令执行作为其参数的脚本并退出 shell。`source` 命令不会退出 shell。

- 16. `&&` 序列仅当行内的上一个命令正常退出时才执行后续命令。

# 第 5 章：使用 Shell、脚本与数据管理（领域 105） 295

19. A 括号用于表示函数，例如 `myFunction()`。括号是可选的，但后面紧跟一个大括号，其中包含调用函数时要执行的命令。

20. 使用 `ORDER BY` 子句用于此目的，需要添加 `ASC` 关键字以按升序显示。

21. C `||` 序列表示如果初始的前一个命令没有正常退出，则运行一个备用命令。`&&` 序列仅在前面的一个命令正常退出时执行，因此它与问题要求的相反。

22. C `elif` 关键字用于在 shell 脚本中创建备用执行路径。其他结构（如 `else` 和 `elseif`）被用于其他语言。

23. A `unalias` 命令用于删除之前定义的别名。`rm` 命令将删除普通文件，而不是别名。其他命令均不存在。

24. D 你至少需要读取被源的文件；因此，`chmod 400` 将正确设置权限。任何赋予额外权限的 `chmod` 都是没有必要的。

25. C 在这种情况下，循环结构要求变量 `LIST` 前面有一个美元符号 (`$`)，使得选项 C 是正确的。其他选项无法实现所述目的。

26. A 内连接（inner join）是 SQL 在按指定方式连接列时形成的默认连接类型。外连接（outer join），无论是左连接、右连接还是全外连接，都用于返回不在适当表中的行。

27. C `-lt` 运算符用于在脚本中测试“小于”条件。其他运算符在 shell 脚本中无效。

28. B `-e` 选项用于检查文件是否存在，它通常用于 shell 中的条件语句中。其他选项可能在 shell 脚本中工作，但它们不是文件存在性测试。

29. C `/etc/skel` 目录包含要复制到用户主目录的文件。此问题列出的其他目录默认不存在。

30. A `UPDATE` 语句使用 `SET` 关键字指示要更改的列。`WHERE` 子句是可选的。

31. D 语法以 `INSERT INTO <table>` 开始。该语法之后可选地跟随要插入值的列名，然后是 `VALUES` 关键字，最后是要插入的值。

32. C `-norc` 选项允许 Bash 在不读取 `/etc/bash.bashrc` 或本地的 `~/.bashrc` 文件的情况下执行。其他选项并不是 Bash 的有效选项。

33. A shell 脚本中的数组在此种方式使用时涉及括号。你也可以使用方括号来定义单个元素，例如 `ARRAY[] = "val1"`。

34. C `-p` 选项以全限定名的方式显示语句，这些命令是完全限定的，并且可以通过管道或重定向作为另一个命令的输入。

35. 如果 `.bash_profile` 文件存在于你的主目录中，它将在登录时执行。请注意，将函数放在 `/etc/profile` 在技术上是行的，但该函数将对所有用户可用，这并不是问题所要求的。

36. `readonly` 命令显示在当前会话中定义的只读变量列表。为此列出的其他命令均不存在。

37. 唯一可以使用 `GROUP BY` 的 SQL 语句是 `SELECT` 语句。列出的其他命令是有效的，但不能与 `GROUP BY` 使用。

38. 方括号用于表示 shell 中 `while` 循环的开始和结束。其他语言通常为此目的使用圆括号。

39. 内置命令 `true` 用于测试变量的值是否非空。请注意，`test` 内置命令的行为取决于参数的数量。

40. 当输入命令 `cd` 时，会查询自动设置为用户主目录的 `HOME` 环境变量。其他列作为 `HOME` 的路径默认不存在，而显示的 `MAILPATH` 环境变量包含了当 shell 进行交互式交互时检查邮件的路径列表。

41. `TMOUT` 变量可以在用户的 shell 中设置，用户将在闲置达到该值（以秒为单位）后被登出。列出的其他环境变量均不存在。

42. 就像 `if` 语句以 `fi` 结尾一样，`case` 语句也以倒拼的单词结尾。选项 D 所示的大括号在许多语言中用于关闭 `case` 语句，但不用于 shell 脚本。

43. 提供的答案执行了命令替换，并将结果命令的值放入变量中。问题指定对日期使用 `%s` 格式，将输出格式化为自 Unix 纪元以来的时间。选项 C 将提供 `DATE` 变量，但不会按指定格式格式化。

44. 将变量封装在大括号中 `${FILENAME}` 将确保变量被正确地插值或扩展，即使是在通常不会扩展的地方（例如在带引号的字符串中）。

45. 在 shell 脚本中，执行的命令从 `do` 关键字开始，到 `done` 关键字结束。其他语言通常使用大括号或制表符。

46. `-r` 测试确定给定文件是否存在并可被当前用户读取。`-e` 测试仅检查文件是否存在，而 `-s` 确定文件是否存在且大小大于 0。没有 `-a` 文件测试。

47. `-r` 选项用于声明创建或将变量标记为只读。`-p` 选项以可以重用的格式打印输出。`-x` 选项声明该变量用于导出。

48. `*` 序列用于表示在没有匹配项时执行的默认语句集。

## 第 6 章：理解用户界面与桌面（领域 106）

1. A greeter 通过 `/etc/lightdm/lightdm.conf` 配置。提供的其他答案无效。

2. B `xorg.conf` 的 `Section` 部分用于逻辑上绑定显卡和显示器，每个设备都在自己的部分中定义。

3. A 频率选项为 `Hz`、`kHz`、`M` 或 `MHz`，因此 `uHz` 是无效选项。

4. C `systemctl default-command` 用于此目的，`multiuser` target 用于进入命令行。你还需要从 `/etc/default/grub` 中移除 `splash` 并运行 `update-grub`。

5. A `DISPLAY` 变量可以通过 ssh 将 X 会话的窗口发送到另一台计算机。没有 `XTERMINAL` 或 `XDISP` 环境变量，且 `XTERM` 是终端窗口而不是环境变量。

6. D `Welcome` 选项设置用户登录时在显示管理器显示的消息。用户可以使用 `RemoteWelcome` 信息。

7. C Shift 用于用于 GNOME 和其他操作系统启用和禁用粘滞键。

8. A `Disable` 键用于确保不加载来模块。请注意，相同模块的 `Load` 语句于 `Disable` 语句，但 `Disable` 可用于卸载默认加载的模块。

9. A Orca 项目为 GNOME 提供了辅助屏幕阅读功能。对于给出的其他选项，`screen` 命令是有效的，但不是用于此目的。

10. C `xrandr` 命令可更改分辨率，将分辨率更改为如 800x600 会让图标和其他项目变。

11. D `allowguest` 选项更改 LightDM 的客体登录行为，禁止客体登录通常会让计算机更安全，尽管如果有人拥有物理访问权限，他们可能通过其他方式获得访问。

# 复习题答案附录

13. `XkModel` 配置选项用于设置使用的键盘类型，例如 pc105-key 键盘。`XkBlayout` 选项定义键盘的布局，例如用于美国样式键盘的 US。

14. `VertRefresh` 选项用于此目的，它接受如所示形式的值范围。该问题的其他选项对于所述目的均无效。

15. `Xdpyminfo` 命令显示当前显示(器)的各种元素以及关于 X 本身的信息。

16. 通过在 `xorg.conf` 中将 `AccelerationProfile` 设置为 6 来启用线性加速配置。设置为 0 被称为 classic（经典），-1 防止恒定加速（无配置），7 被称为 limit（限制），其执行功能与线性加速相同，但设置了最大速度和加速度限制。

17. `/usr/share/fonts` 层次结构用于存储字体。另一个可能包含字体信息的路径是 `/usr/share/X11/fonts`，但它不在本题的选项中。

18. 2.6.26 版本的内核在 Linux 中包含了对盲文显示器的原生支持。

19. `DontZoom` 选项防止指定的组合键更改视频模式。在其他选项中，`DontZap` 了 `Ctrl+Alt+Backspace` 组合键的行为。其他选项没有任何影响，且在 `xorg.conf` 中无效。

20. `gok` 命令是 GNOME On-screen Keyboard 的缩写，是启动软键盘的程序。Caribou 将作为 `gok` 的继任者。

21. `gdmsetup` 程序用于配置登录窗口和环境的各种选项，包括针对本地和远程用户的选项。本题显示的其他选项未用于此目的或不存在。

22. `kmag` 管理桌面上的项目并用作辅助技术。通常，`kmag` 也可以与其他窗口管理器一起使用。

23. `greeter-manual-login` 选项

24. GNOME 控制中心的“外观”（Appearance）部分用于管理桌面显示和行为的许多方面，包括高对比度主题的选择。

25. 鼠标手势通常与辅助技术相关，通过以特定方式移动鼠标来帮助使用程序。鼠标手势可以用于登录和截屏，但这些并不能充分或通用地描述它们。

26. `Alt+Super+S` 快捷键在 GNOME 3.9 或更高版本中激活屏幕阅读器。`Super+S` 快捷键进入概览模式。其他快捷键默认没有特殊含义。

# 第6章：理解用户界面和桌面（领域 106）

27. D. `start` 命令在登录到本地终端后启动显示管理器。其他命令不存在，或无法实现所述目的。

28. B. `BlankTime` 选项默认设置为 10 分钟，会导致显示器变黑，但实际上不会进入进入待机或其他节能模式。

29. C. `xwininfo` 命令显示 X 会话中给定窗口的信息。答案中列出的其他命令无效。

30. A. `Mouse` 按钮显示移动鼠标的按键。`Compose` 按钮显示键盘，其他选项无效。

31. C. `xhost` 命令用于控制对 X 服务器的访问。使用 `+` 添加主机，通过在命令前加 `-` 移除主机。

32. B. 必须启用 `ForwardX11` 选项，来自 X 服务器生成的连接或窗口才能通过 ssh 连接进行传输。

33. D. `FontPath` 指令提供了服务器可以找到字体的另一个位置。其他选项在 `xorg.conf` 配置文件的上下文中不存在。

34. D. 使用软键盘，用户可以使用指针作为鼠标来选择键盘上的按键。

35. C. `Bounce keys`（粘滞键）会导致在不小心连续按下或按住键时界面不做出反应。

36. B. `Alt+Ctrl+F1` 组合键用于获取终端提示符，这在 X 服务器无法正常启动的情况下很有帮助。

37. A. `accesslogin` 选项用于定义一个将自动登录系统的单一用户。本题中的其他选项不存在。

38. C. `Access` 工具用于在旧系统或较旧系统上设置许多辅助功能选项。`AccessX` 提供的功能可以在原生 X 窗口管理器提供的工具之一找到，取决于用户使用的窗口管理器。

39. A. `export` shell 命令设置环境变量。在这种情况下，需要设置 `DISPLAY` 环境变量。`env` 命令不会设置该变量。

40. A. `Mens` 命令显示给定选项的菜单，可以通过键盘对这些选项操作。`Activate` 选项有助于操作桌面和其他应用程序。本题显示的其他选项无效。



41. B. `/etc/lightdm/lightdm.conf.d` 目录包含各种设置的配置文件，它通常会与 `/etc/lightdm/lightdm.conf` 文件一起解析。

42. 在通过 `telnet` 命令访问的运行级别（runlevel）3 中，通常不执行 X 服务器。runlevel 6 将关闭系统。runlevel 1 切换到单用户模式，而 runlevel 5 是多用户模式，此时 X 通常正在运行。

# 复习题答案附录

43. C. `VideoRam` 选项可以以字节表示，用于配置显卡可用 RAM 的量。

44. A. `ColorDepth` 选项设置给定显示器的颜色深度。此项的典型值可能是 24。

45. B. `Identifier` 选项为 X 配置中的每个布局提供唯一描述。其他选项不存在。

46. A. `mkfontscale` 命令创建一个描述系统上轮廓字体的文件，用于配置手动添加到系统的字体。

47. A. 显示器电源管理（DPMS）启用额外的节能模式，例如全睡眠模式，从而进一步提高显示器的能量效率。

48. B. `Emacspeak` 程序提供了作为 `Orca` 替代方案的辅助技术。这里列出的其他技术与之无关。

# 第 7 章：管理任务（领域 107）

1. C. `/etc/passwd` 文件包含关于系统上用户的各种信息，如用户名和真实姓名、用户 ID (UID) 和登录 shell。该文件是全局可读的。

2. B. `cron` 的格式为 `[分钟 小时]`，默认设置为 10 分钟，会导致显示器变黑但实际上不会进入待机或其他节能模式。

3. C. `xwininfo` 命令显示 X 会话中给定窗口的信息。答案中列出的其他命令无效。

4. B. `/etc/cron.allow` 文件是允许创建任务的用户列表。`crontab` 文件用于存储任务。

5. B. `chage` 命令用于设置账户过期时间。

6. D. 在 `/usr/share/zoneinfo` 层次结构中，你可以找到区域和时区的信息。

7. B. `at` 命令用于调度命令。与 `cron` 不同，它可以指定具体时间执行。

8. B. `userdel` 命令用于此目的，`-r` 选项会删除主目录。

9. A. `/etc/group` 包含拥有一个或多个 cron 任务或条目的用户信息。

10. 当计算机关闭时，使用 `anacron` 来调度任务。

11. B. `+s` 选项将日期格式化为自 1970 年以来的整数。该选项在脚本和其他地方经常使用。

12. C. `--list` 选项显示可用的字符集。本题给出的选项存在。

13. C. `LC_TIME` 环境变量用于控制时间的显示和行为，可以通过更改不同的 locale 来实现所需的显示格式。

14. B. `atq` 命令显示已调度的任务列表。其他命令不存在，选项 D 使用了无效选项 `--jobs`。

15. D. 将用户的 shell 设置为 `/bin/sh` 将阻止其登录系统（如 `ssh`）。本题显示的其他选项都是有效的交互式 shell。

16. B. `UTF-8` 提供多字节字符编码，并被广泛接受作为未来的标准。其他答案无效。`UTF-8` 能够编码 `Unicode` 定义的所有字符。另一种流行但过时的编码是 `ASCII`。

17. A. `groupmod` 命令用于此目的，`-n` 选项用于更改组名。

18. A. `/var/spool/cron/crontabs` 目录为每个拥有一个或多个任务的用户包含文件。

19. C. `atrm` 命令根据任务 ID。可以通过 `atq` 命令获取 ID。`atq` 和 `-l` 命令将显示列表但不会删除。

20. D. `tzselect` 命令将显示一个分步菜单以选择时区。最终输出将包含一个区域/时区行，例如 `America/Chicago`。

# 附录 ■ 复习题答案

`LDAP` 服务用于检查是否连接到 `LDAP` 服务器。`usermod` 命令是有效的，但它不用于此目的，且此题中显示的其他命令都是无效的。

- 22. `/etc/login.defs` 文件包含各种配置项，例如系统上使用的最小和最大用户 ID 以及组 ID。

- 23. `/etc/crontab` 文件是一个纯文本文件，被视为系统级 `cron` 文件。因此，该文件通常不与任何单一用户关联，编辑此文件后没有必要运行特殊命令。

- 24. `TZ` 环境变量用于此目的，通用格式如所示，因此选项 D 是正确答案。

- 25. `/etc/cron.daily` 目录包含作为脚本的文件，它们每天执行一次。还有 `cron.hourly`、`cron.weekly` 和 `cron.monthly` 目录，它们按照目录名称所示的各自的计划运行。

- 26. 设置 `LANG=C` 是 `POSIX` 兼容的别名，将导致程序跳过本地化翻译。为 `LANG` 显示的其他选项都是无效的。

- 27. `-m` 允许创建用户的家目录。默认情况下，如果没有指定此选项且未设置 `CREATE_HOME`，则不创建家目录。`-h` 显示帮助文本，其他选项均无效。

- 28. `usermod -l` 命令通过在加密密码开头放置 `!` 来锁定账户。如果用户有其他登录方式（例如 `ssh` 密钥），使用 `usermod -l` 将无法阻止其登录。此选项在创建专用账户时经常被使用。

- 29. `LC_ALL` 变量用于将环境变量设置为本地化，且该变量将覆盖其他变量。这可以在需要临时更改时使用。此地列出的其他变量不用于此目的，且默认不创建。

- 30. 添加用户名时的格式将用户名放在计划任务和要运行的命令之间，因此选项 A 正确。此题中显示的其他选项均无效。在选项 B 的情况下，没有计划。在选项 C 和 D 的情况下，计划格式错误。

- 31. `passwd` 命令用于此目的。`-a` 选项显示所有用户，需要使用 `-s` 指明状态。单用 `-s` 选项不会为所有用户生成报告，而 `--all` 是 `-a` 的别名。

- 32. `date` 命令用于此目的。`-d` 选项设置自上次更改密码以来的天数，以自 1970 年 1 月 1 日起的数计算。`-W` 选项是更改密码的警告天数，`-l` 选项显示与账户相关的各种设置列表。

- 33. `/etc/anacontab` 文件包含有关任务的信息，例如任务名称和延迟等。列出的其他文件不包含与 `anacron` 相关的任务信息。

# 第 7 章：管理任务（领域 107） 303

- 34. A. `ln` 命令用于此目的，`-s` 选项创建符号链接，而 `-f` 强制覆盖目标。其他选项或命令顺序均无效。

- 35. B. `/etc/cron.deny` 文件包含一个不能创建 `cron` 计划任务的用户列表。`/etc/cron.allow` 文件被用于提供一个允许创建 `cron` 任务的用户列表。另外两个文件默认不存在。

- 36. B. `/etc/shadow` 文件包含用户名、UID 和加密密码，由于加密密码的敏感性，系统上的任何非 `root` 用户都无法读取。`/etc/passwd` 文件包含用户名和 UID，但不包含加密密码。此地列出的另外两个文件不存在。

- 37. D. 系统上的 UID 和 GID 之间没有直接关系。UID 代表用户，而 GID 代表组 ID。在某些系统上，普通用户的 UID 和 GID 数字会匹配，但这并非强制要求，更多像是一个巧合。

- 38. B. `dpkg-reconfigure` 命令用于触发询问配置设置。`tzdata` 包是基于 `Debian` 的系统上的包名。`apt-get` 命令无效的。

- 39. A. `usermod` 命令用于此目的。`-d` 选项更改家目录，其中 `-m` 移动内容。用于此目的的其他命令均无效。

- 40. D. `-s` 选项是用户将被添加的附加组列表。较小写的 `-g` 选项提供主 ID。`-l` 选项导致用户不会被添加到 `logfail` 和登录数据库中。没有 `-x` 选项。

- 41. A. `crontab` 命令可用于此目的，`-l` 选项用于列出 `crontab`。需要 `-u` 选项来指定当前用户以外的用户。

- 42. A. `-r` 选项创建一个系统用户，这通常不包含家目录，且 UID 低于 1000。`-s` 选项定义 shell，通常不用于此目的。`-a` 和 `-S` 选项不存在。

- 43. B. `/etc/shadow` 文件包含用户名、UID 和加密密码，系统上的任何非 `root` 用户无法读取。

- 44. C. `LC_ALL` 变量用于将环境变量设置为本地化，且该变量将覆盖其他。这可以在需要临时更改时使用。

- 45. B. `groupdel` 命令删除组。没有 `-f` 选项。`groupadd` 命令用于添加组。

- 46. A. `id` 命令显示用户名、UID、主组。`passwd` 和 `chage` 命令不用于此目的。

- 47. D. `-c` 选项更改 `/passwd` 中的注释字段。`-R` 选项表示 `chroot`，而 `-d` 表示目录。没有 `-n` 选项。

- 48. D. `find` 命令应用于此目的。正确语法在 D。`grep` 命令仅在指定文件中查找 `-u`。

# 第 8 章：基本系统服务（领域 108）

- 1. C. `journalctl` 命令用于处理 `systemd` journal。在基于 `systemd` 的系统上，`journalctl` 是调试和故障排除的核心工具。

- 2. C. `kernel` 设施接收来自内核的消息用于日志。在其他选项中，`syslog` 用于日志本身。

- 3. D. `ntp.org` 提供免费的时间同步服务。当你使用 `ntp.org` 作为目标时，通常会收到一个地理位置的 NTP 服务器，或尽可能靠近。将地址设置为 `127.0.0.1` 或 `192.168.1.100` 使用本地服务器，但前提是该服务器拥有 NTP 服务。

- 4. A. `systemd` 管理的计算机日志服务是 `journald`。你使用 `journalctl` 而标准的 `syslog` 工具。

- 5. B. `newaliases` 命令在运行 `Postfix`、`sendmail` 和 `qmail` 的服务器上重建数据库。运行 `newaliases` 后不需要重启邮件服务器。选项 C 中的 `alias` 命令为 shell 创建别名，但与 `Postfix` 无关。

- 6. D. `CUPS` 的配置文件位于 `/etc/cups`。然而，通常通过其 Web 界面管理 `CUPS`。其他目录均无效。

- 7. A. `Allow` 目录用于此目的，且地址 `192.168.1.1` 到 `192.168.1.127` 在 CIDR 表示法中代表 `/25`，因此答案正确。注意选项 B 使用 `/24` 掩码也会允许这些地址，但也会允许 `192.168.1.128` 到 `192.168.1.255`，范围比允许的要大。

- 8. B. `ntpdate` 命令提供命令行界面，根据作为参数的 NTP 服务器立即更改或设置时间。选项 A 提供的 `ntpdate` 答案将运行 NTP 守护进程，不适合脚本。

## 第 8 章：核心系统服务 (领域 108)

- 9. 通常，来自 NTP 相关命令的“Connection refused”（拒绝连接）消息意味着守护进程未运行。没有迹象 `ntpq` 命令正在查询不同的服务器；因此，网络启动或关闭无关。根据所指示的错误信息，基于权限的选项是的。

- 10. `hwclock` 用于查询和设置硬件时钟，即由系统固件或 BIOS 维护的时钟。`ntpdate` 命令用于设置本地系统时间，但对硬件时钟无效。其他命令均无效。

- 11. Qmail 默认包含在 `/var/qmail/` 中。查询目录是 `/var/qmail/queue`。在 qmail 的默认配置中，其他目录均无效。

- 12. `info` 严重级别为指定的设施（facility）提供消息。给出的选项中 `emerg` 用于紧急消息且通常不被应用程序使用，而 `debug` 是通过 `syslog` 可用的最高或最详细的日志级别。`syslog` 的配置通常位于 `/etc/` 层次结构下的 `syslog.conf` 或 `syslog.conf` 中。

- 13. `driftfile` 选项设置 `ntppd` 漂移文件的位置。漂移文件有助于保持准确。该位置在 Red Hat Enterprise Linux 中显示。

- 14. `mail` 选项用于在 `logrotate` 进程完成后将日志发送到指定的电子邮件地址。其他选项在 `/etc/logrotate.conf` 中不存在。

- 15. `journalctl` 命令用于此目的，`--usage` 选项显示 journal 日志文件空间，这些文件通常存储在 `/var/log/journal`。与 journal 相关的配置位于 `/etc/systemd/journal.conf`。

- 16. `mailq` 命令用于 Postfix 服务器，提供当前邮件队列的摘要。队列详情包括正在发送的邮件 ID 以及事务中的一个或多个电子邮件地址。`mailq` 命令也适用于较新版本的 sendmail。

- 17. `ntpq` 命令为 NTP 服务器提供了一个交互式的、菜单式的界面。你可以使用 `ntpdate` 命令作为选项 B，作为一种设置时间的命令行手段。选项 A 所示的 `ntppd` 命令将执行 NTP 守护进程本身。

- 18. 别 文件的格式为 `user: destination`，因此选项 D 是正确的。其他选项不是 aliases 文件的有效语法。

- 19. `-f` 选项标识将要记录日志的文件。`-d` 选项用于调试，而 `-v` 打印 `klogd` 的版本。`klogd` 没有 `-l` 选项。

- 20. 各种日志轮转策略的单独配置文件位于 `/etc/logrotate.conf`。该目录从主配置文件 `/etc/logrotate.conf` 引入。

- 21. `lpr` 命令将文件（或标准输入）放入打印队列供 `lpd` 使用。`lpq` 命令打印当前队列。没有 `lpx` 命令。

## 附录：复习题答案

22. C. `sendmail` 命令的 `-bp` 选项打印有关当前队列的信息。没有与此问题相关的 `-q` 或 `-f` 选项。`-bi` 选项用于与别名数据库配合工作。

23. A. `-w` 选项将硬件时钟设置为当前系统时间。`-s` 选项设置相反的操作，将系统时间设置为硬件时钟。`hwclock` 没有 `-a` 或 `-m` 功能。

24. D. TCP 端口 631 用于进入 CUPS 的管理接口。访问该端口上的活动 CUPS 服务器将显示打印队列和其他与 CUPS 相关的配置项的管理网站。

25. A. `-q` 选项导致 `sendmail` 尝试交付队列中的消息。添加 `-v` 选项显示详细输出。

26. B. 多个电子邮件地址阻止了使用 `.forward`；因此，需要在 `/etc/aliases` 中完成。多个电子邮件地址的格式是用逗号分隔，使得选项 B 是正确的。

27. A. `-ssutc` 将硬件时钟设置为当前系统时间。需要使用 `-utc` 以确保时间被设置为 UTC。如果未设置 `-utc`，时间将默认为上一次运行命令的时间，那可能是 UTC 但也可能是本地时间。因此，最佳选项是 A。

28. D. `postqueue -d` 命令删除队列中的消息。`ALL` 关键字会导致所有消息被删除。执行此操作时是不可逆的。`postqueue` 没有 `-remove` 选项，且 postfix 的 `-f` 选项与之无关。所示的 `-rf` 命令不够具体，且通常不会手动从邮件队列中删除文件。

29. A. URL 将显示本地 CUPS 服务器的作业区域，查询字符串名称为 `_jobs` 值为 `completed`。其他 URL 均无效。

30. C. 正如 `tail -f` 命令会在添加新内容时持续更新显示一样，`-f` 选项也会为指定的 syslog 标识符显示 journal 的新条目。没有 `-tail` 或 `-l` 选项。

31. B. `SDPServerRun` 选项用于描述的端口。服务器应监听的端口应作为此选项的值提供。其他选项不是 syslog 的有效配置项。

32. A. `-f` 命令用于刷新队列。

33. C. `-g` 选项用于设置日期。

34. A. `driftfile` 选项设置漂移文件的位置。

35. C. `lpstat` 命令用于所述。

36. D. 配置中的 `postrotate` 选项用于执行。

37. B. SMTP 运行在 TCP 端口 25。

38. A. `makemap` 命令用于创建哈数据库。

39. A. `syslog-ng` 的配置文件存储在 `/etc/syslog-ng` 并命名为 `syslog-ng.conf`。

40. C. 理论上可以使用任何日志函数，取决于应用程序类型。然而，记录自定义日志意味着日志具有不同的名称和位置，使得 `local0` 到 `local7` 是合适的。

41. B. `usermod` 命令用于将组添加到用户列表中。

42. D. `nocompress` 选项用于防止日志文件在轮转过程中被压缩或封压缩。

43. D. `-s` 选项设置命令中指定的日期和时间。

44. B. `mailstats` 命令用于所述。

45. D. `logger` 命令用于向 syslog 发送消息。

46. A. `systemctl` 命令用于控制服务。

47. C. 使用 `-` 表示 syslog 不为每条日志条目同步到磁盘。

48. A. Port 配置选项用于此目的，并被作为 `Listen` 指令的替代方案。使用 `Listen` 指令时，你将指定地址:端口。然而，选项 C 虽然在语法上有效，但它只会监听 127.0.0.1 的本地主机 IP 地址，而不是监听所有接口。

## 第 9 章：网络基础（领域 109）

- 1. A. `netstat` 命令可用于此目的，`-r` 选项显示当前路由。添加 `-n` 可以防止 DNS 查询，这有助于性能。

- 2. A. `ifconfig` 命令可用于此目的，它需要添加 `-a` 选项，因为适配器目前处于关闭状态。`ifup` 命令可以启动接口，但它默认不显示信息。`netstat` 命令可以显示网络信息，但带带 `-n` 选项。



- 3. D. 私有 IP 地址位于 `10.0.0.0/8`、`172.16.0.0/12` 和 `192.168.0.0/16` 范围内，因此 `143` 范围内的地址是公 IP 地址。

- 4. C. `route` 命令用于此目的，通过 `add` 选项添加路由。使用 `default gw` 关键字后跟网关 IP 和适配器 IP 来添加默认网关。

- 5. A. `host` 命令通过 `-t` 选项启用更改查询类型。使用 `ns` 类型将查询给定域名的名称服务器。没有 `all` 类型，其他选项也是无效的。

- 6. B. 传统上，`UDP/53` 用于 DNS 查询，但由于存在主、备用服务器，假设可能会发生区域传输。DNS 区域传输通常接管 `TCP/53`。

- 7. B. `-i` 选项允许选择接口。小写的 `-i` 选项设置间隔，而 `-a` 表示审计性 ping（audit ping）。最后，`-t` 仅启用基于 TTL 的 ping。

- 8. D. 掩码为 `255.255.255.224` 的 `/27` 将子网分为四个每个 `32` 个地址的段，从而产生 `30` 个可用地址。

- 9. A. 可以通过将类型设置为 `mx` 使用 `host` 或 `dig` 命令用于此目的。`mx` 将查询给定域的邮件交换器。没有 `smtp`。

- 10. B. IPv6 的本地主机地址可以写为 `::1`。显示的类似 `127` 的地址代表 IPv4 本地主机范围，但格式不适用于 IPv4 或 IPv6。

- 11. A. `-t` 选项导致 `traceroute` 使用 TCP 包。此选项需要 root 权限，在防火墙拦截 traceroute 流量的情况下可能有用。`-i` 选项选择接口，而 `-s` 选项选择源地址。小写的 `-t` 选项设置服务类型 (`ToS`) 标志。

- 12. C. `ifup` 命令用于启动网络接口，`-a` 选项启动标记为 `auto` 的接口。`ifconfig -a` 显示所有接口的信息，且没有 `ifstat`。`ifdown` 命令可用于关闭或离线接口。

- 13. D. `hostname` 命令用于返回主机名和域名。当给定 `-d` 选项时，仅将域名返回到 `STDOUT`，适合在脚本中使用。

- 14. A. `ip` 命令配合 `monitor` 选项/子命令将显示到达的 `netlink` 消息。`ip` 命令没有 `netlink` 子命令，`route` 命令可以用于此目的。

- 15. D. `traceroute -6` 中的 `-6` 选项执行 IPv6 traceroute。此问题所示其他选项均无效。如果 `traceroute6` 命令不可用但 `traceroute -6` 可，将是非常罕见的。

- 16. A. 语法为 `database:database`，并带有用空格分隔的额外数据库名，如本题正确选项所示。

- 17. A. 使用 `@` 符号标识直接向其发送查询的服务器。对于通过将查询直接发送到域名的权威服务器来排除解析问题非常有用。在其他选项中，`-t` 设置类型，其他选择无效。

- 18. D. `SNMP` 流量发生在端口 `161` 和 `162`。虽然流量通常是 `UDP`，但 `TCP` 端口也用于 `SNMP`。端口 `110` 和 `143` 分别用于 `POP3` 和 `IMAP`，而 `23` 和 `25` 用于 `Telnet` 和 `SMTP`。最后，端口 `80` 和 `443` 用于 `HTTP` 和 `HTTPS`。

- 19. A. `get` 命令用于处理 `NSS` 数据库，`get hosts` 将显示使用 `/etc/resolv.conf` 配置的数据库的可用主机。

- 20. A. `CIDR` 表示法中的 `/24` 代表地址空间中 `/23` 的一半，使掩码位为 `255.255.255.0`。`255.255.0` 的答案是 `/16`，而 `255.255.192` 则对应 `/25`。

- 21. C. `netmask` 选项用于此目的，可以提供多个域名。在 IPv6 中，`fc00::/7` 是唯一本地地址空间。

- 22. D. `route` 命令用于此目的，在描述的情况下，使用 `reject` 目标用于路由。其他选项无效，因为对 `route` 命令使用了无效选项。

- 23. A. `route` 命令可用于此目的，通过 `add` 选项添加路由。使用 `default gw` 关键字后跟网关 IP 和适配器 IP 来添加。

- 24. A. `netstat` 命令可用于此目的，`-r` 选项显示当前路由。添加 `-n` 可以防止 DNS 查询，这有助于性能。

- 25. A. `ip` 命令配合 `monitor` 选项/子命令将显示到达的 `netlink` 消息。`ip` 命令没有 `netlink` 子命令，`route` 命令可以用于此目的。

- 26. `ifconfig -a` 选项启动标记为 `auto` 的接口。`ifconfig -a` 显示所有接口的信息，且没有 `ifstat`。`ifdown` 命令可关闭离线接口。

- 27. IPv4 地址长度为 `32` 位，IPv6 地址长度为 `128` 位。两者都用于内部和外部网络。

- 28. D. `ICMP` 是一种网络层协议，意味着它不使用端口通信。`UDP/69` 用于 `TFTP`，`111` 用于 `sunrpc`。

- 29. B. `ip route` 命令可用于此目的，在描述的情况下，需要先删除现有网关并重新添加网关。

- 30. C. `Secure Shell`（即 `ssh`）默认使用 `TCP` 端口 `22`。`TCP/23` 用于 `Telnet`；`TCP/25` 用于 `SMTP`，其他无效。

- 31. B. `nc` 命令用于启动 `netcat`，`-l` 选项使其监听。`-p` 选项用于指定 `netcat` 监听的端口。`-s` 选项指定本地源地址，用于此场景。

- 32. A. `so` 类型用于查询域的权威记录。注意，在许多情况下，`dig` 会尝试在给定命令中查找域名并看起来没有错误。例如，运行选项 D (`dig -t auth example.com,`) 你将收到关于 `example.com` 的信息，输出中有一行显示 `dig` 忽略了无效地址类型。

- 33. A. `search` 选项用于此目的，可以提供多个域名，每个域名由空格或制表符分隔。`domain` 选项在 `/etc/resolv.conf` 中有效，但它不适用于多个域名。

- 34. `ping6` 命令用于 ping IPv6 地址。唯一本地地址是 IPv4 中 `RFC 1918` 私有地址的 IPv6 等效物。在 IPv6 中，`fc00::/7` 是唯一本地地址空间。注意普通 `ping` 命令没有 `-6` 选项。

- 35. A. `route` 命令可用于此目的，在描述的情况下，路由使用了 `reject` 目标。其他选项无效，因为对 `route` 命令使用了无效选项。

## 附录：问题答案

### 第9章：网络基础 (领域 109)

36. B. `tracepath` 命令提供跳数的最大传输单元 (`MTU`)，`traceroute` 和 `tracepath` 均可在内部或外部使用，且都支持 IPv6。`traceroute` 命令的某些选项需要 root 权限，但题目中没有足够的信息使其成为正确选项。`tracepath` 命令具有原生 IPv6 功能。

37. D. `-c` 选项提供发送的 ping 计数。`-n` 选项仅指定数字输出，而 `-p` 选项指定数据包内容的模式。最后，`-t` 选项设置 `TTL`（生存时间）。

38. B. `NXDOMAIN` 是不存在的域名或主机状态，基本上意味着查询的主机不存在。当没有错误时，正常状态为 `"NOERROR"`。

39. A. 为了便于描述的场景，`ifconfig` 的语法使用设备名后跟协议，在本例中为 `inet6`。下一个键用于指示正在添加 IP 地址。最后，后面是地址本身。

40. C. 基于 `SSL` 的 `LDAP`（或 `LDAPS`）运行在端口 `636`。端口 `53` 用于 `DNS`，端口 `389` 用于普通的非 `SSL` `LDAP`，端口 `443` 用于 `HTTP` `SSL`。

41. D. 此题的最佳选项是在 `/etc/hosts` 中为主机添加条目。这样做将导致 `DNS` 查询解析到 `127.0.0.1`。其他选项并不健壮，因为它们依赖于 `www.example.com` 具有相同的 IP 地址，或者解决方案需要额外的维护，以不断向 `www.example.com` 的 IP 地址更改添加新 IP。

42. A. 在更改路由后，应执行 `ip route flush cache` 命令。此题所示其他命令均无效。

43. A. `SPF` 记录存储在 `DNS` 的 `txt` 记录类型中，因此 `-t txt` 是此题的正确选项。在其他选项中，只有 `-t mx` 是有效的，它会返回给定域的邮件交换器。

44. B. `TCP` 是一种面向连接的协议，使用三次握手建立连接。`ICMP` 不使用端口进行通信，`UDP` 是无连接的。它是核心互联网协议，且不使用握手。

45. D. `172.16.0.0` 私有范围内有 `1,048,576` 个 IP 地址。`10.0.0.0` 范围有 `16,777,216` 个，`192.168.0.0` 范围有 `65,536` 个。

46. C. 列出的选项中唯一可能的可能是 `ICMP` 流量被阻止了。由于可以通过 `HTTP` 到达，因此 `TCP` 流量显然是通过的，且 `DNS` 也一定在工作。

47. C. `G` 表示路由表中的网关。

48. A. `axfr` 是区域传输，`@` 符号表示查询发送到的服务器。没有 `xfer` 类型，选项 B 只是发送到指定服务器的域名的普通查询。

### 第10章：安全 (领域 110)

- 1. 如果存在 `/etc/nologin`，则用户将被阻止登录系统。假设 `ssh` 配置中启用了 root 登录，root 用户可以登录。

- 2. `find` 命令用于此目的，权限可以描述为 `4000` 以表示存在 `setuid` 位。`-type` 选项可用于更改返回对象的类型，但它与描述的场景无关。

- 3. `lsof` 命令可用于此目的，配合 `-i` 选项将显示网络端口及其对应的进程。`netstat` 命令使用 `-a` 选项会显示网络端口但不显示进程。`ps` 命令用于进程而非网络端口。最后，没有 `list` 命令。

- 4. `fuser` 命令可用于确定哪个进程正在使用给定文件。`ls` 命令显示文件，`find` 可用于文件但不是专门用于此目的。`ps` 命令显示进程如何，但不一定绑定到特定文件。

- 5. `chage` 命令用于处理账户老化信息，如过期日期、密码更改、密码更改之间的天数等。`-l` 选项列出给定账户的信息。`userm` 命令用于修改账户，另外两个命令无效。

- 6. `nmap` 命令用于扫描开放端口。`nmap` 命令将扫描指定地址或地址的开放 `TCP` 端口。其他命令不扫描外部（离主机）IP 地址的开放端口。

- 7. `ssh-keygen` 命令用于创建密钥对以供 `ssh` 代替密码。其他选项中，`ssh` 命令确实存在，但 `-k` 选项用于禁用 `G` 凭据转发，而非所述目的。

- 8. 格式为用户名（或其他标识符）后跟 `hard` 或 `soft`（取决于限制类型），然后是关键字，最后是给定关键字的值。

- 9. 文件 `authorized_keys` 存储在主目录的 `.ssh` 目录，包含了允许使用相应私钥登录服务器的公钥。

- 10. `-p` 选项显示给定进程的进程 ID。`netstat` 命令使用 `-a` 选项会显示网络端口但不显示进程。`ps` 命令用于进程而非网络端口。最后，没有 `list` 命令。

# 附录 ■ 复习题答案

26. B. `change` 命令可用于此目的，`-E` 选项接受自 `1970/1/1` 以来的天数。`passwd` 没有 `-e` 选项，而 `usermod` 的 `-U` 不会执行描述的操作。没有 `hgouser` 命令。

27. A. 设置 `-p8` 将导致扫描之前不发送任何 ping 请求，它对于描述的场景非常有用。虽然有一个 `-s` 选项，但它不是用于此目的。其他选项无效。

28. C. `maxlogs` 参数用于控制给定账户的并发登录数。

29. B. `ssh_known_hosts` 文件通常保存在 `/etc/` 中，用于描述的目的。注意在某些系统上，此文件和其他 `ssh` 相关的配置可能位于 `/etc/ssh/`。`*` 表示 `-` 或 `/root` 是错误的，因为问题指定的是全服务器范围的列表。

30. C. 上次修改密码的日期（自 `1970` 年 `1` 月 `1` 日起的天数）包含在 `shadow` 条目的第三字段中。过期日期将是第八字段，并用冒号分隔。

31. A. 前向使用的格式是 `-L` 选项，后跟本地端口，然后是远程:端口的组合。这通常后面跟着用于 `ssh` 连接的 `user@host` 凭据。

32. C. 该选项是 `ForwardForward`，它必须被设置，以便让目标服务器将基于 `X` 的窗口转发到本地客户端计算机。其他选项无效。

33. A. `--gen-key` 子命令用于描述的目的。其他选项不存在。

34. D. `%` 用于表示 `/etc/sudoers` 中的组。它提供了一种管理特权组的 `l`。

35. A. `-p` 选项设置端口用于登录，它无法使用 `host:port` 语法。`ssh` 没有 `-P` 或 `@` 选项。

36. A. `-s` 选项设置类型，当后跟大写 `S` 时，将其设置为 `SYN`。`T` 选项用于 `Connect` 扫描。`nmap` 没有 `-type` 选项。

37. C. `wtmp` 文件存储在 `/var/log` 中，用于存储最近登录信息，由于其使用，可以配合 `w` 命令。其他列出的日志不存在。

38. A. `-i` 选项用于 `ssh` 用于身份验证。这表示公钥位于远程主机的 `authorized_keys` 文件中。`-k` 选项禁用了 `GSSAPI` 凭据的发送，而 `-f` 用于后台运行 `ssh`。没有 `--key` 选项。

39. A. `-n` 选项有助于描述的场景，它将退出而不是提示。`-i` 选项指定登录名，该场景场景无效。`-q` 和 `--prompt` 选项不存在。

40. C. `ssh-keygen` 命令用于此目的，`-t` 选项指定要生成的密钥类型。`ssh` 命令没有相关的生成选项。主机密钥存储在 `/etc/ssh/ssh_host_rsa_key`（`RSA` 密钥）和 `/etc/ssh/ssh_host_dsa_key`（`DSA` 密钥）。

41. B. 井号 (`#`) 可以注释掉 `/inetd.conf` 中的行。在对 `/inetd.conf` 做出更改后，应该重启服务。许多系统利用 `/inetd.conf` 存储与特定服务相关的配置文件。

42. A. `-l` 选项用于锁定账户。小写版本的 `-l` 用于更改用户名。其他命令不存在。

43. B. 位于 `~/.gnupg/` 的 `publishing.gpg` 文件包含公钥。

44. C. 存在的 `.gpg-v21-migrated` 表示 `gpg` 版本为 `2.1` 或更高，文件已迁移。

45. D. `find` 命令用于此目的，需要 `-perm` 选项，具体用于指示 `setgid`。使用 `/~` 将搜索整个服务器。`grep` 命令无法用于此目的，因为它在当前目录的文件查找 `setgid` 字符串。

46. C. `update-rc.d` 命令从 `/etc/init.d/` 中的服务文件到 `/etc/rc.d/*` 中每个运行级别（runlevel）的相应位置创建符号链接。其他命令无效。

48. C. 单横杠 `-` 是用于 `su` 的典型选项。没有 `-u` 或 `-U` 选项，`-login` 选项不存在。有一个 `--login` 选项（两个横杠），但图中显示的。

### 第 11 章：容量规划（主题 200）

- 1. D. `iostat` 的 `-p` 选项显示设备和分区的信息。`-c` 选项显示 `CPU` 利用率，`-d` 显示设备利用率。没有 `-a` 选项。

- 2. B. `iptraf` 中的过滤器用于定义应该包含或排除的流量。对于此场景，将源地址定义为自身，目的地定义为监控的接口。

- 3. `vmstat` 命令用于显示性能的扩展信息，包括输入块。`iptraf` 命令用于提供网络级监控，其他命令无效。

- 4. `iotop` 命令用于按进程监控磁盘使用情况（如读取和写入）。`top` 命令不提供磁盘使用，`iostat` 不按进程提供信息。最后，`free` 提供内存的聚合信息。

- 5. `Nagios` 提供了适用于场景的监控功能，使用各种插件监控设备和系统的许多方面。

- 6. `w` 命令显示各种有用信息，包括平均负载、登录用户和运行时间。`uptime` 命令不显示谁登录。

- 7. `free` 命令显示 `RAM` 和交换区的当前内存使用情况，包括总计和空闲。作为选项显示的其他命令不存在。

- 8. 在 `top` 中按下 `Shift+F` 允许你选择显示的列以及排序顺序。在描述的场景中，你可以查看使用内存最多的进程。

- 9. `df` 命令显示磁盘使用情况信息，它可以帮助随时间进行规划。例如，如果你知道磁盘利用率正在显著增加，你可以准备增加磁盘使用或释放空间。

- 10. C. `Cacti` 是一种图表工具，同时使用脚本和 `SNMP` 收集数据，帮助可视化网络和系统的性能。`pstree` 命令用于显示进程的树结构。

- 11. `ps` 命令提供单个进程的处理器和内存使用信息。你可以使用这些信息来预测容量。

- 12. `pstree` 的 `-p` 选项显示一个或多个进程的 ID。`-s` 选项设置排序。`vmstat` 没有这些选项。

- 13. `iptraf` 的 `-a` 选项显示监听和非监听套接字的统计信息。这可以用于发现性能瓶颈。

- 14. `iptraf` 工具用于实时监控流量，提供发送和接收队列的统计。它是图形化的。

30. 这种情况需要使用 `-i` 选项，且端口格式前有一个冒号。

31. `-m` 选项将磁盘相关的统计数据以兆字节（`MB`）为单位，而不是默认的千字节（`KB`）。



32. 如果 `ps` 命令输出中的 `Stat` 列显示为 `D`，则表示有一个进程处于不可中断睡眠状态，这意味着它无法被杀死，并且通常正在等待 I/O。处于 `SI` 状态的进程是多线程进程的正常睡眠状态。重启服务器是清除不可中断睡眠进程的唯一方法，假设它们不会自动唤醒。最后，`vmstat` 的 `-n` 选项用于选择表头的显示方式。

33. `-d` 选项用于设置延迟，间隔单位为秒分之一，因此需要 100 个这样的间隔才等于 10 秒。

34. `vmstat` 命令同时显示内存和 CPU 使用信息。`iostat` 命令不显示内存信息。一旦熟悉了该命令，只需使用正确的语法来实现每秒更新并持续 10 秒即可。

35. `-s` 命令显示网络部分的聚合统计信息，包括接收的数据包总数和转发的数据包数量。`ifconfig` 命令不显示转发的数据包。`ls` 命令不用于网络，且 `ipstat` 命令不存在。

36. 在只有一个处理器的系统上，`1.00` 的平均负载表示高利用率。然而，在两个处理器的系统上，平均负载约等于 `50%` 的容量。即使在 `50%` 的容量下，使用 `top` 或 `ps` 命令检查导致利用率的原因可能也是一个好主意。

37. 当向 `sar` 发送计数为 `0` 的零间隔作为参数时，将显示自上次重启以来的平均值，然后程序退出。

## 第 12 章：Linux 内核（主题 201）

- 1. `make oldconfig` 命令将现有的配置文件集成到内核的新配置中。你仍然需要注意新内核中移动或更改的项目，以确保配置正确。

- 2. 内核源码通常保留在 `/usr/src/linux` 中。

- 3. `xz` 命令用于压缩和解压缩文件。当配合 `-d` 选项使用时，作为参数提供的文件将被解压缩。

- 4. 传统的 `zimage` 格式大小限制为 `512 KB`，而 `bzimage` 没有此类限制。

- 5. `menuconfig` 目标提供了一个用于选择内核选项的图形化界面，适合在 `ssh` 连接上使用。不过，在 `ssh` 上编译内核时要小心。如果你选择了错误的选项，服务器可能无法成功启动。因此，请确保你有其他访问控制台的方法。

- 6. A. `mkinitrd` 命令在其他系统中用于创建初始 RAM 磁盘。初始 RAM 磁盘用于加载（某些可能会预加载）磁盘的关键模块以及启动所需的关键组件。

- 7. C. 在可用时，使用 `bzip2` 压缩 `bImage`。`bImage` 描述了压缩内核镜像的另一种格式，它可以超过通常作用于 `zimage` 的 `512 KB` 限制。

- 8. B. 内核配置放置在 `/usr/src/linux/.config` 中。如果你将来需要从源码重新创建内核或为了参考，制作该文件的备份是一个好主意。

- 9. B. `lsmod` 命令用于显示当前加载的模块。这对于从标准内核或发行版提供的内核迁移到自定义内核的场景非常有用，并可以知道哪些模块需要编译到新内核中。

- 10. B. `clean` 目标移除大部分编译文件，但可能会留下一些，例如与内核编译相关的文件。`mrproper` 目标移除之前内核副本的编译文件，同时也移除 `.config` 文件。`config` 目标用于配置内核选项，但在执行 `mrproper` 之前不应使用它。

- 11. B. 在“General Setup”区域找到 `LOCALVERSION` 选项可以根据你的本地节点附加自定义版本号。

- 12. C. 动态内核模块支持 (`dkms`) 用于在内核源码树之外构建模块。

- 13. B. `depmod` 命令用于创建模块列表。列表保留在名为 `modules.dep` 的文件中，其位置取决于 Linux 的发行版。

- 14. D. `udevadm` 命令用于处理内核的 `udev` 接口，监控器（`monitor`）实时显示内核事件和 `udev` 事件。

- 15. A. `lsusb` 命令显示有关 USB 内核接口的信息。`-t` 选项以树状结构格式化输出，这有助于可视化设备是如何连接到计算机的。

- 16. A. `-a` 选项显示 `sysctl` 的所有值及其当前设置。`-b` 选项为二进制，并显示不带换行的值。`-d` 选项是 `-h` 的别名，用于显示帮助。没有 `-c` 选项。

- 17. B. `modprobe` 命令检查给定模块的依赖关系，并加载依赖项和请求的模块。

- 18. B. `deb-pkg` 目标创建适用于 Debian 软件包管理系统的 `.deb` 文件。其他系统上也有类似的目标。

- 19. B. `uname` 命令用于此目的，`-r` 选项显示内核版本。

- 20. C. `dracut` 命令用于在新系统中创建初始 RAM 磁盘，并取代了旧的 `mkinitrd` 命令。

- 21. C. 与 `udev` 规则存储在 `/etc/udev/rules`。`/etc/udev/rules.d` 目录用于存储模块相关的配置。

- 22. A. `modinfo` 命令提供给定模块的信息。

- 23. C. 在 `/usr/src/linux/Documentation` 中可以找到关于内核的详细文档。

- 24. B. `-k` 选项显示与给定设备相关的内核驱动程序，`-t` 以树状结构显示，`-n` 使用数字代替设备名称。没有 `-a` 选项。

- 25. C. `insmod` 命令将模块插入运行的内核。然而，它不会尝试解析依赖关系，如果不存在依赖模块或内核符号，则会报错。

- 26. B. `-r` 选项从运行的系统中移除模块，并尝试移除该模块依赖的任何模块；`-d` 选项设置模块的根目录，`v` 为详细模式，`f` 强制加载模块。

- 27. B. `modules_install` 目标用于安装通过 `modules` 目标编译的模块。

- 28. B. `/etc/modprobe.d` 目录用于存储与模块相关的配置信息，例如黑名单。

- 29. C. `lsmod` 命令显示当前加载的模块列表。列表中包含了模块的大小以及正在使用该模块的内容（如果有）。

- 30. B. `rmmod` 命令从运行的系统中移除模块。为了使用 `rmod`，该模块不能被使用或被其他当前加载的模块依赖。

- 31. B. 放置在 `/etc/sysctl.conf` 中的变量和值将在启动时生效。

- 32. D. `/proc/kallsyms` 文件提供了查看当前内核符号的方法。注意，在旧系统中，该文件可能被称为 `/proc/ksyms`。

- 34. B. `--show-depends` 选项显示给定模块的依赖关系。其他选项对于 `modprobe` 命令无效。

- 35. A. `modinfo` 工具可用于显示当前加载模块的选项。`modinfo -r` 命令无效，且 `modinfo` 显示的是关于模块的信息，它不包含核心大小和其他设置。`lsmod` 命令无法用于此目的，且没有 `infmod` 命令。

- 36. B. `/proc/sys/kernel` 层次结构包含内核的至关重要的配置信息。这些设置可以在运行中的系统上更改。

- 37. C. 内核环形缓冲区（或与内核相关的日志消息）可以使用 `dmesg` 命令进行查看。消息通常会轮换，只显示最新的消息，但可以通过配置选项进行更改。

# 第 13 章：系统启动

（主题 202）

- 1. B. `/etc/systemd/system` 目录是存储系统 单元文件（`unit files`）的推荐位置。其他位置无效。

- 2. C. `systemctl` 命令用于此类目的，使用 `daemon-reload` 子命令可以重新加载系统配置，但 `reboot` 选项是不正确的，因为它会确保服务器重启，这并不是题目所问的。

- 3. B. `/etc/inittab` 文件包含各种运行级别以及在给定运行级别要运行的内容。例如，运行级别 `1` 是单用户模式，运行级别 `6` 是重启，依此类推。其他文件不存在。

- 4. B. `SYLINUX` 引导加载器用于 `FAT` 文件系统创建救援磁盘，并协助 Linux 的通用安装。`Syslinux` 还描述了一个包含其他特殊引导加载程序的项目。此问题列出的其他选项不是有效的加载器。

- 5. A. `ESP` 使用旧的 `FAT` 文件系统作为其底层格式。有一项规范规定了如何在 `FAT` 格式之上创建 `ESP` 分区，以用于引导加载程序和内核镜像。注意，该分区通常是 `FAT32`，但如果驱动器上只运行 Linux 系统，则可以是 `FAT16`。

- 6. C. `initrd` 用于早期磁盘的初始根文件系统。`initrd` 配置为在特定操作系统的 `grub` 配置文件中加载。

- 7. B. `fsck` 命令用于在 Linux 中诊断和修复硬硬盘。Linux 中没有 `defrag` 命令。

- 8. D. `init` 命令可用于此目的，传递 `1` 作为参数将系统切换到单用户模式。所示其他命令均无效。

# 附录复习题答案

- 9. `--install` 选项后接使用 `extlinux` 的分区，将被安装用于启动。

- 10. `mount` 命令的格式为 `[partition] [target]`，因此选项 `C` 是确的。其他选项无效，因为参数顺序错误。

- 11. 安装 `GRUB` 的命令是 `grub-install`，第一个 `SATA` 硬盘是 `/dev/sda`。列为 `hda` 的设备是 `PATA` 硬盘，使得这些选项是错误的。

- 12. `-n` 选项更改下次启动的启动顺序并从分区启动。`-b` 配合 `-M` 修改并删除选项。`-o` 选项设置启动顺序。`-c` 选项创建启动菜单。

- 13. `ISOLINUX` 提供了一种将 `CD-ROM` 格式化为 `ISO 9660` 的方法。使用 `ISOLINUX` 启动的活动 `CD` 或使用/恢复 `CD` 非常常见。引导加载程序对于此目的无效或不存在。

- 14. `/usr/lib/systemd` 层次结构包含与 `systemd` 配置相关文件。该层次结构内的用户目录用于用户单元文件，系统文件存储在 `/usr/lib/systemd/system` 中。

- 15. 由于微软 `UEFI` 设计中做出的不安全决策，在带有 `UEFI` 的系统上启动通常需要一个 `shim`。`.efi` 文件可以作为此目的的初始引导加载程序。

- 16. 系统配置文件的优先级顺序是 `/etc` 层次结构内的，其次是 `/run` 层次结构中的，然后是 `/lib` 层次结构中的。

- 17. 在基于 `SysV init` 的系统中，启动和停止服务的脚本位于 `/etc/init.d`。此选项中的其他目录均无效。

- 18. `systemd-diff` 命令用于覆盖配置文件。在其他命令中，`diff` 是有效的，但不是用于此目的。`systemctl` 命令也是有效的，但同样不是用于所述目的。

- 19. `hkconfig --list` 命令显示所有启动时将执行的服务以及每个运行时的的设置。在其他命令中，`init` 是有效的，但它没有 `--bootlist` 选项。其他命令均无效。

- 20. `UEFI shell` 中的 `becfg` 命令用于配置基于 `UEFI` 的系统上的引导加载程序。该命令可以接受各种参数来配置引导加载程序并在启动时加载内核。在所示的其他命令中，`grub-install` 是有效的，但不在 `UEFI shell` 内。

- 21. 主引导记录（`MBR`）是磁盘上的第一个扇区，包含关于磁盘结构的信息。如果 `MBR` 损坏，磁盘上的所有数据可能会丢失。此问题列出的其他选项均无效。

- 22. 引导加载器被挂载到 `/boot/efi`。其他目录不存在。

- 23. D. 救援目标（`rescue target`）用于加载最小化系统来协助恢复。

- 24. A. 配置文件是 `isolinux.cfg`，通常位于 `/boot/isolinux`。其他选项无效。

- 25. D. `pxelinux.0` 文件必须存在于 `/tftpboot` 中，系统才能使用 `PXELUX`。

- 26. D. `update-rc.d` 工具可用于管理 `SysV` 脚本。使用 `update-rc.d` 时，你提供脚本名称，该工具将负责创建符号链接。

- 27. B. 键在启动过程中正确时机按下时将你送入 `GRUB shell`，在其中你可以更改诸如内核选项之类的参数。

- 28. B. `systemctl` 命令用于此目的，`get-default` 子命令将显示默认目标。在许多发行版中，默认目标是 `graphical.target`。

- 29. A. `-r` 选项修复文件系统，`-y` 选项导致 `fsck` 回答“`yes`”而不是提示。`-v` 选项是详细模式。`fsck` 没有 `-m` 或 `-x` 选项。

- 30. D. `--boot-directory` 允许你指定 `GRUB` 镜像的替代位置而非 `/boot`。此问题的其他选项无效。

- 31. D. `isolate` 命令后接所需的目标用于在基于 `systemd` 的系统中切换运行级别。所示的其他子命令无效。

- 32. C. 定义为 `initdefault` 的运行级别是系统的默认运行级别。其他选项不存在。

- 33. B. 使用 `initramfs` 系统代替 `initrd` 来创建启动所需的内核驱动程序的文件系统加载过程。

- 34. A. `systemctl` 命令用于此目的，`set-default` 子命令对于影响所需的行为是必要的。目标文件名为 `multi-user.target`。

- 35. C. `shim.efi` 引导加载程序加载另一个引导加载程序，默认是 `grub64.efi`。其他选项不是所述目的的有效文件名。

- 36. D. `/etc/rc.d` 层次结构包含指向 `/etc/init.d` 中文件的符号链接。这些符号链接用于在适当的运行级别执行脚本。例如，在启动时，系统将在每次启动时执行运行级别目录中的脚本。

- 37. A. `default.target` 是 `systemd` 在启动时激活的默认目标单元。默认目标随后根据依赖关系启动其他服务。

# 第 14 章：文件系统与设备 (主题 203)

- 1. `/etc/mtab` 列出了当前挂载的文件系统。`/etc/fstab` 文件列出了计算机的整体文件系统，但它不区分已挂载或未挂载的文件系统。问题列出的其他选项不存在。

- 2. `-t` 选项将文件系统类型设置为 `ext2`、`ext3` 或 `ext4`。`mke2fs` 命令通常是来自 `/sbin/mkfs.ext2`、`/sbin/mkfs.ext3` 和 `/sbin/mkfs.ext4` 的软链接。`-f` 选项强制 `mke2fs` 创建文件系统。`-a` 和 `-o` 选项不存在。

- 3. `/etc/auto.master` 文件包含 `autofofs` 的配置。其他选项均无效。

- 4. `mkiso` 命令创建一个 `ISO` 文件系统，然后可以将其写入 `CD` 或 `DVD`。其他命令是无效的。

- 5. `cryptsetup` 命令用于设置和配置 `dm-crypt` 卷。其他命令均无效。

- 6. `mkswap` 命令用于格式化交换分区。其他命令均无效。

- 7. `-c` 选项设置最大挂载次数。`-b` 选项设置挂载数量。`-a` 选项不存在。

- 8. `-f` 选项（也称为 `f`）对于需要调试挂载过程或为之前挂载的文件系统向 `/etc/mtab` 添加条目的情况很有帮助。`-l` 选项显示标签，`-v` 是详细模式。

- 9. 字母 `r` 表示文件系统已以只读模式挂载，这意味着无法对文件系统执行写入操作。另一个选项是 `w`，表示文件系统已以读写模式挂载。

- 10. 使用 `-b` 选项显示坏块。另一个命令是 `f`。

- 11. `D` 基于写时复制（`copy-on-write`）原则，通常认为比 `ext4` 及其之前的更先进。`FAT` 是一种遗留文件系统，主要用于 `DOS` 和 `Windows`。

- 12. `xfs_info` 命令功能上等同于 `xfs_grow -n`，用于显示 `XFS` 格式文件系统的信息。

- 13. `blblk` 命令显示分区信息，包括它们的类型、`UUID` 和其他基本信息。

- 14. `-t` 选项可以接受逗号分隔的类型列表，指定仅卸载列出的类型的文件系统。这与 `-a` 选项结合使用非常有用，可以卸载除 `/proc` 之外的所有文件系统。`-v` 选项是详细模式，`-f` 强制执行操作。

- 15. `sync` 命令立即将未写入的数据写入磁盘，适用于在尝试卸载操作之前运行。

- 16. B. `swap` 命令启用交换空间，使其可以作为虚拟内存。`mkswap` 命令格式化该空间。其他命令是有效的。

- 17. C. `-f` 选项指示 `fsck` 应该检查指定文件内容的一致性。`-v` 选项设置详细程度，且没有 `-d` 或 `-a` 选项。

- 18. B. `-w` 选项允许 `debugfs` 以读写模式打开文件系统。还有一个 `-c` 选项用于对受损严重的文件系统以灾难模式（`catastrophic mode`）打开。`-rw`、`-r` 和 `-n` 选项无效。

- 19. D. `smart` 守护进程监控兼容 `SMART` 的磁盘的重大事件，并可以配置在事件发生时发送警报。其他命令在此场景下均无效。

- 20. A. `-f` 选项在原本干净的文件系统上强制运行 `fsck`。这在你怀疑文件系统存在错误并需要验证故障排除过程中的这部分时很有帮助。这也有助于为文件系统进行转换做准备，转换可以使用 `btrfs-convert` 等工具完成。

- 21. A. 导入或恢复的块大小必须与导出或转储使用的块大小匹配。块大小通过 `-b` 选项指定，因此选项 `A` 是确的。其他选项对 `xfsstore` 均无效。

- 22. B. 使用默认挂载选项的文件系统将以读写(`rw`)模式挂载，并具有执行程序的能力(`exec`)。文件系统将自动挂载(`auto`)，但用户将无法手动挂载(`ouser`)。字符和块设备将被解释(`dev`)，磁盘操作将以异步方式(`async`)进行。

- 23. D. `smartctl` 命令控制对给定设备的 `SMART` 监控，假设已安装了 `smart` 工具包。`smartd` 选项代表监控 `SMART` 事件的整体守护进程。

- 24. A. 在 `/etc/fstab` 中，首先找到要挂载的文件系统（如 `/dev/sda1`），然后是文件系统将挂载的目标位置。接下来是文件系统类型，以及文件系统所需的任何选项。`dump` 工具指示符位于选项之后，最后是 `pass` 或 `fs` 顺序。最后一个字段决定了在启动时由 `fsck` 检查文件系统的顺序。

- 25. A. 基于密码的密钥派生函数 2 (`PBKDF2`) 用于 `LUKS` 中基于密码加密的密钥派生。`SSL` 是安全套接层，通常用于 `HTTP` 流量加密。`RSA` 和 `DSA` 都是加密算法，但它们与此问题无关。

- 26. B. `btrfs subvolume create` 命令创建一个 `btrfs` 子卷。其他命令无效。



# 第 15 章：高级存储设备管理 (主题 204)

3. C. `/dev/disk/by-id` 目录包含指向 `/dev/sd` 的符号链接，例如 `/dev/sda`。由于 WWID 可跨系统识别设备，它们通常用于存储区域网络（SAN）环境。选项列出的其他目录并不存在。

4. A. `iscsadm` 命令用于管理 Linux 系统上的 iSCSI 设备。此问题显示的其他选项均无效。

5. C. `pvdisplay` 命令显示物理卷（PV）的信息。你可以使用 `pvdisplay` 查看构建 PV 的设备以及该 PV 的区大小（extent size）。显示的其他命令无效。

6. D. `DEVICE` 配置行包含一个可用于阵列的设备列表。关键字 `DEVICE` 之后是一个由空格分隔的设备列表。

7. B. 包含字符 `fc` 的逻辑单元号（LUN）通过光纤通道（Fibre Channel）找到。这就是选项 B 和 C 之间的区别，选项 C 包含字母 `scsi`，而这通常代表本地磁盘。其他选项无效。

8. C. `multipath` 命令用于管理 LUN 等设备，并可为服务器查找 LUN 的路径，例如在 SAN 配置中。其他命令均无效，`lsblk` 除外，`lsblk` 是有效的；但该选项与 LUN 无关，而是 `lsblk` 命令中各种标志的组合。

9. C. `ftrim` 命令用于删除未使用的数据块。`ftrim` 命令在 SAN 配置中被频繁使用，以便将未使用的存储归给 SAN。`ftrim` 命令也可以用于固态硬盘以达到相同目的。显示的其他命令无效。

10. 支持 NVMe 的设备命名为 `/dev/nvme*`。除了现代系统原生内核中找到的驱动外，不需要特殊驱动。其他答案中的路径默认并不存在。

11. A. `scsi_id` 命令在设备上虚拟产品设备的 0x80 或 0x83 页面上生成 SCSI 标识符。其他命令无效。

12. D. AOE（或称 over Ethernet）直接通过以太网发送 ATA。AOE 命令在 OSI 中较低层（TCP/IP 甚至 IP 层）发送，但它们不可路由。显示的其他缩写是有效的，但不是用于此目的。PXE 是启动协议，POE 用于以太网供电，iSI 是一种存储协议，但与 ATA 无关。

13. B. `hdparm` 命令用于获取或设置 IDE 和 SATA 设备驱动器设置的底层配置值。此问题显示的其他命令无效。

14. A. 下一步通常是使用 `vgcreate` 创建一个卷组（或多个卷组）。`-f` 选项指示一个操作，但是基于新创建的物理卷。

15. B. `-E` 选项表示扩展选项关注，例如 `stripe_width`。对于此解决方案来说这并不是必要的，而 `-e` 选项设置错误时的行为。没有 `-extend` 选项。

# 附录 ■ 复习题答案

16. 文件 `/proc/mdstat` 包含系统中发现的 RAID 阵列类型信息、组成阵列的设备以及其他相关信息。显示的其他文件无效。

17. `iscsid` 守护进程创建并维护到 iSCSI 目标的连接，使其在 Linux 中可用。`iscsiad` 命令用于管理目的，其他命令无效。

18. `nvmme` 模块在现代系统中可用，作为 Linux 上 NVMe 设备的驱动。你可以使用 `modinfo` 命令检查 `nvmme` 模块。

19. 目录 `/sys/class/fe_host` 光纤连接的其他目录。在这些目录中，可以在名为 `port_md` 的文件中找到 WWN（全球标识符）。其他目录结构无效。

20. `--create` 选项启用创建一个使用 `md` 的 RAID 阵列。典型参数是 `/dev/mdn` 设备。其他选项对 `mdadm` 无效。

21. `iscsid.conf` 文件通常位于 `/etc` 或 `/etc/iscsid/`，用于与 `iscsid` 守护进程相关的配置。其他配置文件对 `iscsid` 无效。

22. `/dev/multipath` 目录包含作为逻辑卷的多路径设备信息。其他目录无效。

23. C. `--monitor` 选项用于主动监控阵列是否存在磁盘故障等问题。监控作为后台守护进程进行，从而在出现问题时发出警报。

24. `-ro` 选项以只读模式挂载驱动器。`rw` 模式为读写。如果你需要在访问驱动器而不可能破坏驱动器上的任何信息，则以只读挂载是有用的。其他选项无效。

25. `lvcreate` 命令用于从之前创建的物理设备和卷组创建逻辑卷。使用 `lvcreate` 是 LVM 在实际使用逻辑卷之前三个步骤之一。

26. `MDADD` 选项设置 `mdadm` 在监控模式下记录的 RAID 事件邮件目标地址。

27. `vgscan` 命令查找与 LVM 相关的物理卷和卷组。其他选项无效。

28. A. `-d` 选项设置 `mdadm` 在监控模式下记录的 RAID 事件的邮件目标地址。

5. `iw` 命令用于此目的。当你配合特定设备使用 `iw` 时，会出现 `dev` 关键字，后面跟着设备名称。最后，使用用于在该设备上执行的命令（在本例中为 `link` 命令）。

6. `iwconfig` 命令与 `ifconfig` 命令类似，它作用于单个接口以设置和显示参数。在其他命令中，`ifconfig` 命令是有效的，但不是用于无线网络的。其他命令均无效。

7. `iwlist` 命令可以用于此目的，其 `scan` 子命令用于查找本地访问点和无线网络。`iwconfig` 命令没有 `scan` 子命令。同样，`iwlist` 也没有名为 `for` 的子命令，也没有 `iw-scan` 命令。

8. `-o` 选项移除输出中的换行符，从而使输出更适合 `grep` 命令。`-l` 选项指定 `ip addr flush` 命令的循环次数`-f` 选项指定协议族。没有 `-n` 选项。

9. `mtu` 选项可设置给定接口的最大传输单元（MTU）值。`metric` 选项设置接口度量。其他选项无效。

10. 为了利用 `reject` 目标，需要添加一条路由，因此选项 B 是正确的。选项 C 删除路由但不创建 `reject` 路由。选项 D 删除默认路由，而选项 A 无效。

11. `-s` 选项创建一个 ARP 表条目。`-d` 选项移除条目。`-c` 和 `--address` 选项不存在。

12. `ss` 命令提供了与 `netstat` 许多相同的功能，但它可以显示某些扩展信息，例如给定套接字的内存分配。`free` 命令显示按套接字的内存使用情况。这两个命令不存在。

13. `-t` 选项打开 TCP 连接，而 `-a` 显示活动套字。`-n` 选项禁用域名解析。

14. 此解决方案需要一种过滤掉 `bind` 用户的方法；因此，`grep` 搜索 `bind` 或将 `bind` 指定为用户的答案都是错误的。然而，`lsof` 命令允许使用脱字符字符 `^` 进行取反。列出除 `bind` 外的所有文件需要特定的语法。

15. `-f` 选项是洪水泛型 ping（flood ping）。这实际上会导致接口发送和接收大量流量，使其在交换机上更容易被发现。`-a` 选项是有声 ping，在 ping 时发出声音。`-c` 选项设置特定的 ping 计数。没有 `-e` 选项。

16. `netcat` 命令提供了一种在 TCP 连接双方（服务器和客户端）打开并进行通信的方法。`netcat` 命令避免了 Telnet 捕捉 Telnet 协议特定字符的一些问题。`netstat` 命令不测试连接性，而 `ping` 不在 TCP 层级进行。没有 `nettest` 命令。

## 第 16 章：网络配置 (主题 205)

17. C. `-d` 选项列出给定计算机上的接口。`-d` 选项转储编译后的匹配代码，`-i` 选择接口。没有 `-a` 选项。

18. B. `-R` 选项要求尝试进行域名解析。`-n` 选项的作用相反；即禁用域名解析。没有 `-b` 或 `-a` 选项。

19. A. `ping6` 命令的操作与 IPv4 的 `ping` 命令相同，但它是针对 IPv6 的。其他命令在 Linux 上无效。

20. B. `ip` 命令可用于此目的。当配合 `addr` 对象和 `-6` 选项使用时，将仅显示有关 IPv6 地址的信息。第一个选项简单的 `ip addr` 将显示包括 IPv4 在内的所有地址。其他命令无效。

21. A. `ifconfig` 命令用于此目的，可以通过在单词 `arp` 前加一个减号来禁用 ARP，如所示。如果没有减号，ARP 将被启用。其他命令在该场景下将不起作用。

22. C. `dev` 选项指定所指定路由的设备。这是许多路由的典型用例，以减少内核错误增长的概率。此问题所示其他选项均无效。

23. C. `-p` 选项在 `s` 输出中显示给定套接字拥有的 ID。`-a` 选项用于所有套接字，`-l` 用于监听套接字。`-f` 选项用于指定协议族。

24. A. `-i` 选项以表格格式显示接口信息。将显示如接口的发送和接收字节数以及 MTU 等其他信息。`-r` 选项显示路由，而 `-l` 显示监听套接字。没有 `-t` 选项。

25. D. `/etc/network` 目录包含网络接口的信息，并包含在接口启动或关闭时执行的进一步脚本。其他目录不存在。

26. C. `-I` 选项告诉 `traceroute` 使用 ICMP 进行请求。`-T` 选项是 TCP SYN。`-A` 选项执行路径查找，`-i` 选项配置 `traceroute` 使用指定的接口。

27. B. `mtr` 命令提供查看主机间路由每跳实时信息的独特方法。`traceroute` 和 `route` 命令都是有效的，但各自显示的选项无效。没有 `live` 命令。

28. C. `hostname` 命令获取主机名。当在排查地址解析问题时，这非常有用，因为主机命名可能会产生冲突的结果。其他功能无效。

29. A. 应该使用 `grep` 命令和 `-i` 选项来实现忽略大小写。`-v` 排除参数，因此操作与所需的相反。`-p` 选项指定了在补丁时从路径开头删除的斜杠数量。`-p1` 和 `-p8` 选项都很常见。`-s` 选项指定静默操作。没有 `-strip` 选项。

### 332 附录复习题答案

30. C. 只有字母数字、减号/连字符和点是有效的。

31. `/etc/resolv.conf` 内的选项以关键字开头，后跟一个或多个选项。

32. C. `-c` 选项清除第一次读取。

33. `systemctl` 命令用于此目的。添加 `-u` 选项指定所需的日志条目的单元（unit）。

34. A. `/etc/hostname` 文件通常只包含主机名而不是域名。这在启动时读取以设置计算机的主机名。`/etc/hosts` 文件包含用于名称解析的各种主机信息。其他文件不存在。

35. C. `/etc/sysconfig/network-scripts` 目录包含 Red Hat 系统的信息。其他目录不存在。

36. B. `tracer6` 命令用于跟踪 IPv6 路由。其他命令不存在。

37. C. `PARANOID` 通配符指定主机名和 IP 匹配。`ALL` 关键字也是 TCP Wrappers 中的通配符，可用于 `/etc/hosts.allow` 和 `/etc/hosts.deny`。

## 第 17 章：系统维护 (主题 206)

1. C. 内核源码使用 `xz` 压缩。以前这些源码曾使用 `bzip2`，在此之前使用 `gzip`。没有压缩算法。

2. C. `-a` 选项提供存档模式，它是多个选项的替代。`-r` 选项是递归，`-o` 选项指示保留所有权，`-f` 选项启用过滤器。

3. A. `-c` 选项表示创建 `tar` 文件。`-d` 选项用于对比两个 `tar` 文件，`-b` 选项提供块大小，`-f` 选项指定使用的文件。

4. C. `--remove-files` 选项在将文件添加到存档后从文件系统中删除。`-r` 选项将文件追加到存档末尾，`-d` 选项提供文件系统与存档之间的差异，`-f` 选项指定文件。

6. 根据 `make` 命令的 `man(1)` 页面，大写字母 M 的 `Makefile` 是推荐的文件名。`makefile` 作为默认名是有效的，但它不是推荐的选项。其他文件名作为默认无效。

7. `clean` 目标通常包含在项目的 `Makefile` 中，用于删除上一次编译遗留的文件。其他目标均无效。

8. `configure` 脚本通常包含在源码包中，用于根据本地环境对软件进行自定义配置。显示的其他脚本名称通常不被使用。

9. 根据文件系统层次结构标准（FHS），`/usr/src` 目录是源代码的推荐位置。许多管理员转而使用 `/usr/local/src`，但 FHS 中并未规定这一点。

10. `gzip` 命令用于解压缩使用 `gzip` 压缩的文件。

11. `-b` 选项用于指定块大小。可以使用各种后缀，例如 `M` 等于兆字节（megabytes），`K` 等于千字节（kilobytes）。

12. `tapype` 指令为目标定义一个友好名称。随后在相应的 `define` 指令中进一步配置目标。其他指令对 Amanda 均无效。

13. 使用 `/dev/st*` 查找磁带设备。

14. `/etc/issue` 文件用于在本地登录前向用户提供消息（例如登录幅）。显示的其他文件对于所述用途无效。

15. A. 在 `rsync` 归档模式同步时，`--delete` 选项会删除宿主机系统中已不存在的文件。其他选项对 `rsync` 均无效。

16. D. `wall` 命令向所有登录的用户显示消息。该命令有时用于通知服务器即将到来的重启或关机。其他命令无效。

17. B. `--exclude` 选项从存档中排除匹配模式的文件。该选项通过排除存档中的不必要文件可以极大地减小存档的大小。`-x` 选项是从存档中提取文件的唯一有效选项。

18. C. 当用户成功登录时，会显示 `motd` 文件（`Message of the Day` 的缩写）的内容。在其他选项中，`/etc/issue` 的内容会在本地登录前显示。其他文件名对于此用途无效。

19. B. `-f` 选项指定文件名，`-v` 是详细模式，根据场景，这两个选项都是要求的。`-x` 选项从存档中提取。

20. C. 直接从当前目录执行 `configure` 脚本意味着在脚本名前加上 `./`，如正确选项所示。

# 附录习题答案

21. `-z` 选项将解压缩用 `gzip` 压缩的 `tar` 文件。`-x` 选项用于提取，而 `-c` 用于创建 `tar` 文件。最后，`-f` 指定要操作的文件。

22. `/etc/issue.net` 文件用于远程登录（如 `Telnet`）提供消息。列出的其他文件对于所述用途无效。

23. 使用 `systemctl` 命令访问的系统 `poweroff` 重启用于停止系统并在兼容的系统上尝试移除电源。`halt` 停止系统但不尝试移除电源，而 `reboot` 重新启动系统。没有 `stop` 目标。

24. `uname` 命令显示关于内核、处理器类型以及在编译软件时可能有帮助的相关组件的信息。

25. `--modify-window` 选项修改确定同步的方式。默认行为是匹配到最接近的秒。该选项对于同步文件系统类型非常有用，例如 Microsoft FAT，因为它没有 Linux 文件系统样的精度。

26. `-b` 选项指定在补丁过程中应进行备份。`-l` 选项告诉 `patch` 忽略空格。`-r` 选项指定拒绝文件。没有 `-a` 选项。

27. `install` 目标将最终编译的文件安装到适当的位置，并在适用的情况下将它们设为可执行。在其他选项中，`distclean` 作为一个目标用于将源文件恢复到原始状态。其他目标无效。

29. `--size-only` 选项检查正在同步的文件大小是否相同。这对于可能存在严重时间偏差或阻止正常差异机制正常工作的情况很有帮助。其他选项对 `rsync` 均无效。

30. `--decompress` 选项解压缩 `xz` 文件，而 `--stdout` 选项将输出发送到标准输出。其他选项无效。

31. `-c` 选项将输出发送到 `STDOUT`。`-d` 选项用于解压缩，而 `-f` 强制操作。最后，`-s` 减少了 `bzip2` 的内存占用。

32. Bacula Director 配置文件默认位于 `/etc/bacula/bacula-dir.conf`。其他文件通常不作为 Bacula 配置的一部分。

33. `mt` 命令的 `rewind` 子命令将磁带回到开头。该子命令可以缩写为 `we` 而不是 `rewind`。其他子命令不适用于 `mt`。

34. `-r` 选项指示指定重启以及从现在开始计算时间的格式。它带有加号 (`+`) 前缀，因此选项 A 是正确的。在其他命令中，在不指定 `-r` 选项的情况下指定 `+15` 仅会在 15 分后关闭电脑，而将时间指定为 `00:15`（如选项 D）将在凌晨 12:15 重启电脑。

35. B. `-q` 选项抑制所有警告。`-v` 是详细模式，而 `-L` 显示许可证。`-r` 选项是递归的。

36. C. `-e` 选项（也可用 `--ssh`）使用 `ssh` 作为传输手段，确保同步过程通过加密隧道。其他选项无效。

37. B. `--help` 选项通常包含在 `configure` 脚本中，用于列出其他选项。由于每个 `configure` 脚本都是定制的，其他选项可能会有所不同。即使是 `--help` 也不总是可用。

# 第 18 章：域名服务器

1. A. `named.conf` 文件位于 `/etc/` 或 `/etc/bind/`，是 BIND 服务器的默认配置文件。该文件通常加载或包含其他特定配置的文件。

2. B. `allow-query` 指令设置允许进行 DNS 查询的主机。这对于可能存在不可信客户端的情况很有帮助。



3. B. `-1` 或 `-HUP` 信号重新加载指定的进程。`-15` 是默认终止信号，而 `-2` 用于强制杀死，在进程不响应正常信号的紧急情况下才会被这种做法。

4. A. `-a` 选项允许指定使用的算法，而 `-n` 指定名称类型为 `zone`、`host` 或其他。没有 `-d` 或 `-e` 选项。

5. B. `named-checkzone` 命令检查区域文件是否存在会导致 BIND 使用该文件的明显语法错误。`named-checkzone file` 功能与 `named-checkzone` 相同，但它直接将输出到文件。

6. A. 对于 MX 记录，数字越小优先级越高，因此 `0` 是该域名的优先级 MX 记录。

7. D. DNS 通常使用 UDP `53` 端口，区域传输外由于大多数区域请求的大小使用了 TCP `53` 端口。

8. A. `/var/named` 目录存储区域。在 Debian 上，此目录是 `/var/cache/bind`。`/etc/named` 目录被某些发行版用作配置的位置。

9. C. `rndc` 命令用于控制 BIND 服务器，包括通过远程连接控制。显示的其他命令无效。

10. D. `axfr` 类型可以配合 `dig` 请求区域传输。请求区域传输的客户端需要获得授权才能发起传输。

11. B. `listen-on` 指令设置了守护进程运行的 IP 地址或地址。其他指令无效。

12. C. 主目录应该在 `/etc/passwd` 中设置，并且它应该设置为 `chroot` 目录。列出的其他文件无效。

13. A. `dnssec-signzone` 命令用于在使用 DNSSEC 时对 DNS 区域进行签名。其他命令不存在。

14. A. 在 `host` 命令中将 `-a` 设置为选项会将查询类型设置为 `ANY`。`-c` 选项设置类，`-d` 选项开启调试。没有 `-b` 选项。

15. C. `CNAME` 的正确格式要求末尾有一个点，这是答案 C 和 D 之间的唯一区别。

16. A. 唯一的选项 `forward only`（仅转发）被用于指示服务器应只转发查询，而不尝试直接回答。第一个选项转发查询，如果没有收到响应，它将尝试自己执行查询。其他选项无效。

17. B. `blackhole` 选项提供了一份地址列表，出于安全考虑，这些地址将不允许接收查询。这在某些情况下很有帮助。其他选项无效。

18. B. 安装 `bind9` 需要 `daemontools` 包。当使用 `bind9` 时通常不使用 `BIND9`，且不需要 `qmail`。

19. D. `named-checkconf` 命令用于验证 BIND 的配置。在未提供配置文件的情况下，假设 `/etc/named.conf` 代表配置文件。

20. C. TTL（生存时间）值默认以秒提供，因此 `28800` 等于八小时。

21. B. 数值 `1800` 代表区域的重试值。刷新（refresh）为 `3600`，而默认 TTL 为 `86400`。最后，序列号（serial）为 `2016070400`。

22. C. `TXT` 记录用于创建支持 SPF 的资源记录。`MX` 用于 SMTP 记录。

23. B. 邮件服务器（mailer）在格式中定义为 `Priority MX Hostname`。

24. C. 位于用户主目录下的 `.digrc` 文件可用于设置 `dig` 命令的默认值。在 `/etc` 中没有找到 dig 配置。

25. A. `mount` 命令的 `--bind` 选项与 BIND 守护进程本身无关，用于在另一个位置挂载或重新挂载文件系统的部分。这对于在 `chroot` 环境下处理 BIND 配置文件很有帮助。

26. D. `hint` 区域类型用于根区域文件。在设置服务器具有权威性的区域时，类型为 `master` 或 `slave`。没有 `recurse` 类型。

## 第 19 章：HTTP 服务（主题 208）

27. A. `rndc` 命令可用于此目的，当给于 `reload` 子命令时，它将重新加载服务器的区域。

28. D. `allow-transfer` 指令指定了允许请求区域传输的主机。其他选项无效。

29. D. POP3 服务器在 DNS 中没有特定类型。MX 类型表示邮件交换器或 SMTP 服务器。

30. C. `allow-recursion` 选项适用于某些情况：某些客户端可以查询域名服务器的权威名称，但不能请求递归。

31. A. 正确格式是 `named-zone <zone> <zonefile>`。不需要其他选项。

32. D. `rndc` 唯一的可用算法是 `hmac-md5`，密钥可以使用 `dnssec-keygen` 生成。其他选项是加密或哈希算法，但不用于所描述的场景。

33. B. BIND 配置文件中的 `version none;` 指令告诉 BIND 不要返回版本信息。其他指令无效。

34. C. `-z` 选项告诉 `named-checkconf` 在验证过程中验证主区域。其他选项无效。

35. B. 记录上的单个 TTL 意味着更改需要许多秒时间才能传播。新请求在重启后将立即看到更改，但外部解析器在请求下一次解析之前可能会缓存 TTL 值。

36. A. Debian 上提供 `pdns-server` 包，Red Hat 上提供 `pdns`。Red Hat 需要从 EPEL 安装。

37. B. `rndc` 命令可以配合 `reconfig` 子命令用于此目的。由于该场景涉及对 `named.conf` 配置配置文件的更改，简单的 `rndc reload` 并不合适。

## 第 19 章：HTTP 服务（主题 208）

1. B. `<VirtualHost>` 指令开始的一个段落有助于使用虚拟服务器提供网站。其他指令对 Apache 无效。

2. D. `htpasswd` 命令使用 `htpass` 创建或更新原生 Apache 身份验证的凭据。`passwd` 命令是有效的，但它不能与 `htpass` 配合。其他命令无效。

3. C. `configtest` 选项验证配置文件的语法，这对于防止由于配置致命错误导致服务器无法重启非常有帮助。对于 `apachectl` 命令来说，其他选项无效。

4. `openssl` 命令配合 `gens` 选项用于此目的。使用 `-out` 指定输出文件。其他包含 `-out` 的命令无效。

5. `AuthFile` 指令指定密码文件的路径。

6. `ServerName` 指令设置服务器的主机。

7. `Options` 指令指定目录中允许的选项。

8. `allow_access` 指令定义基于 IP 地址的访问规则。

9. `http_access` 指令结合 ACL 指令定义访问。

10. 当 `TraceEnable` 关闭时，将发送 `405 Method not allowed` 响应。

11. `SSLCertificateFile` 指定证书文件的路径。

12. `SSLCertificateKeyFile` 指向私密钥。

13. `AuthGroupFile` 指定用于身份验证的组文件。

14. `LoadModule` 指令用于加载 Apache 模块。

15. 此场景未使用 `-z` 选项。

16. `DocumentRoot` 指令设置网站根目录。

17. `directory` 指令对特定目录进行设置。

18. `Options` 指令指定哪些功能被启用或禁用。

19. 当 `TraceEnable` 关闭时，将发送 `405 Method not allowed` 响应。

20. B. `SSLCertificateKeyFile` 指令指向私密钥。

21. B. Squid 默认监听端口 `3128`。

22. C. `mod_authz_host` 模块用于基于 IP 的授权。

23. A. 日志默认名称是 `access_log`。

24. B. `http_access` 指令结合 ACL 指令定义访问。

25. C. `AccessFile` 指令可设置文件名。

26. B. Apache 解释说通过将与身份验证相关的指令存储在主服务器配置中来实现高性能。

# 第 20 章：文件共享 (主题 209)

33. B. `SetHandler` 指令用于此目的。为了让 `mod_perl` 工作，`SetHandler` 应设置为 `perl-script`。`mod_perl` 需要 `LoadModule`，但其参数包含了 `mod_perl` 和 `mod_perl` 模块的路径。

34. C. 在 `nginx` 的 `location` 块中，`proxy_pass` 指令允许将请求代理到指定的 URL。其他指令对 `nginx` 无效。

35. C. `StartServers` 指令决定初始启动的子进程数量。该数量会随着请求的变化的变化，特别是并发请求。在繁忙的服务器上，可能需要增加 `StartServers` 以及其他所有相关指令以确保足够的性能。

36. D. `LogFormat` 指令设置要存储的参数。`LogFormat` 指令设置一个可以在配置其他地方使用的日志配置文件。其他选项无效。

37. C. `Require` 指令用于此操作，当需要特定用户时，该指令后跟 `user` 关键字和允许的用户名。显示的其他指令对 Apache 无效。

38. B. Samba 的配置文件位于 `/etc/samba`。该目录并未针对特定的 Samba 版本命名。其他目录默认不存在。

39. B. `nmbd` 守护进程负责 NetBIOS 名称服务的处理。`smbd` 守护进程负责文件和打印，`winbind` 提供用户和组信息。没有名为 `samba` 的守护进程。

40. D. `smbcontrol` 命令可以向 `smbd`、`nmbd` 或 `winbind` 发送消息。当使用目标 `all` 时，消息将发送给所有三个守护进程。`smbcontrol` 可以发送多种消息类型，其中之一是 `reload-config`。有一个 `shutdown` 消息，会对用户造成干扰并在重启之前不会重新加载配置。

41. D. `/etc/exports` 文件包含使用 NFS 共享的文件系统定义。其他文件对 NFS 无效。

42. A. 在 NFS 导出配置中，空格非常重要。选项 A 和选项 C 之间的主要区别在于主机与 `(rw)` 配置指令之间是否存在空格。在选项 A 中，没有空格，`www.example.com` 允许对共享进行读写访问。在选项 C 中，由于存在空格 `.example.com` 仅允许读取访问，而其他人均允许读写。

43. B. `-k` 选项为 `net` 命令启用 Kerberos 认证。`-k` 选项表示应使用非交互模式，`-l` 设置日志目录。没有 `-b` 选项。

44. D. `username map` 选项被设置为一个包含用户名映射的文件，用于为每个用户提供 Windows 用户名与 Linux 用户名之间的翻译。显示的其他选项在 Samba 配置中无效。

45. C. 使用百分号 (`%`) 来分隔用户名和密码，例如此示例，用户为 `Administrator`，密码为 `adminpass`：`-U Administrator@adminpass`。

46. C. NFS 使用 `*` 或 `?` 指定通配符；因此 `*.example.org` 表示 `*.example.org` 直接下方的所有主机都可以连接。注意，通配符映射不是分级的，`*.example.org` 下的子域名不包含在内（例如 `www.example.org`）。

47. D. `cifs` 文件系统类型用于挂载 Samba 共享。`vfat` 文件系统用于挂载 Windows 文件系统，而 `ext4` 是原生 Linux 文件系统。没有 `win` 类型。

48. C. `mount` 命令可用于此目的，当给定 `-t cifs` 参数时，它不会显示 `bfs` 文件系统类型，而带有 `-cifs` 选项的 `ls` 命令将显示并非特定于 CIFS 文件系统的各种文件列表。

49. D. 将安全参数设置为 `share` 表示将保护共享级安全。参数设置为 `security=share`。此问题的其他选项无效。

50. B. `rpcinfo` 的 `-m` 选项显示 `rpcbind` 的统计信息。`-s` 和 `-l` 选项用于显示程序列表和特定程序的条目。`rpcinfo` 没有 `-e` 选项。

51. B. `showmount` 命令用于此目的，当给定 `-e` 选项时，它显示服务器的导出情况。在其他选项中，`mount` 命令是有效的，但使用的给定的选项无效。

52. C. `/etc/fstab` 文件利用特定格式，要求文件系统设备（在此处为 `src.example.com:/source`），随后是挂载目标（在此处为 `/srv/source`），然后是文件系统类型。对于此场景，文件系统类型是 `nfs`。文件系统选项以及默认挂载选项通常包含在 `/etc/fstab` 中。

53. A. `-3` 选项仅显示 NFSv3 统计信息。还有相应的 `-2` 和 `-4` 选项分别对应 NFSv2 和 NFSv4。其他选项均不存在。

54. B. `/proc/mounts` 显示当前已挂载的文件系统。`/etc/fstab` 文件显示可以挂载但当前未挂载的系统。显示的其他文件无效。

55. A. 与 TCP Wrappers 使用时（如 `hosts.allow` 和 `hosts.deny`），`portmap` 服务必须使用 IP 地址。因此，选项 A 是正确的。

# 附录 ■ 复习题答案

50. `-L` 选项显示锁列表。`-l` 选项设置日志的基础目录。`smbstatus` 没有 `-o` 或 `-m` 选项。

51. `smbpasswd` 命令用于管理 Samba 凭据。当给定 `-a` 选项时，会创建一个新用户。在其他命令中，`passwd` 命令有效但没有 `-samba` 选项。其他命令无效。

52. `browsable` 选项设置为 `yes` 或 `no`，用于配置给定共享是否可以通过浏览看到。当设置为 `no` 时，用户必须知道名称才能与之交互。

53. `samba-tool` 的 `dbcheck` 命令用于验证活动目录数据库的位置。其他命令不与 `samba-tool` 使用。

54. Samba 配置文件的 `[global]` 部分允许设置日志文件的设置。显示的其他部分无效。

55. `testpar` 命令可用于验证 Samba 配置文件中的语法。其他命令无效。

56. `exportfs` 命令用于与 NFS 相关的若干管理任务。当使用 `-ra` 选项时，会重新读取 `/etc/exports` 文件，创建新列表并创建共享。

57. `-R` 选项指定 `smbclient` 的名称解析顺序。例如，设置 `-R` 选项的值决定了应使用哪个 WINS 服务器进行名称解析。`-d` 选项指定调试级别。

58. `-l` 选项记录所有成功的挂载请求。在其他选项中，`-n` 允许非 root 请求，`-r` 允许通过 RPC 请求提供硬文件。

59. `read only` 选项设置为 `yes` 或 `no`，定义连接到给定共享的用户是否对共享执行读写操作。其他选项对 Samba 有效。

60. `smbd` 守护进程监听 TCP 端口 `139` 和 `445`。端口 `443` 用于 HTTPS，端口 `161` 和 `162` 用于 SNMP。

61. `root_squash` 选项更改了从远程客户端使用 NFS 共享时 root 的权限。root 将具有最低的可能权限。其他选项对 NFS 无效。

62. `net` 命令用于此解决方案，当给定 `groupmap list` 子命令和选项时，将显示 Windows 组到 Linux 组的映射。其他命令无效。

63. `-p` 选项显示主机各种 RPC 相关服务的当前端口映射。`-m` 选项显示统计信息。`rpcinfo` 没有 `-c` 或 `-f` 选项。

64. `-x` 选项从 Samba 用户数据库中删除用户。`-d` 选项禁用账户。`-e` 选项启用账户。没有 `-o` 选项。

65. C. `smbclient` 命令可用于此目的，当给定 `-L` 选项时，命令将显示该主机上可的服务。显示的其他命令都是无效的。

66. C. 显示的配置带有 `%S.log` 将为每个共享创建一个单独的日志文件。其他选项都包含语法错误，导致它们对于 Samba 配置无效。

67. D. `nmblookup` 命令可用于测试网络上与 NetBIOS 相关的服务。

68. D. 带有 `-u` 和 `-a` 选项的 `export` 命令会导出所有目录。完成此任务的另一种方法是停止 NFS 守护进程，但在选项中没有提供该选项。

## 第 21 章：网络客户端管理（主题 210）

1. A. `ddns-update-style` 选项配置服务器在租约创建或确认时是否执行 DNS 更新。其他选项不适用于 DHCP。

2. A. `subnet` 关键字也用于此目的，此外还有 `netmask` 参数。显示的子掩码将提供 `126` 个可用地址。

3. B. `hardware ethernet` 指令用于指定特定主机的 MAC 地址，该预留将绑定到该主机。其他选项未用于 DHCP。

4. C. 目录 `/etc/pam.d` 存储各个 PAM 感知服务的配置文件。每个服务都有自己的文件，根据其对 PAM 的使用对该服务进行管理。在其他选项中，没有目录是用于 PAM 的默认目录。

5. A. LDAP 的标准端口是 `389`，也是 `slapd` 监听连接的端口。端口 `3389` 是 RDP，而 `3306` 是 MySQL。最后，`110` 是 POP3。

6. D. `ldapadd` 命令用于向 OpenLDAP 数据库添加条目。



### 网络与安全（续）

7. C. 使用 UDP 的 DHCP 流量在端口 67 和 68 上通信。在其他端口中，只有 143 被广泛用作 IMAP 端口，且与 UDP 无关。

9. C. 域名搜索顺序可以通过 DHCP 选项设置。选项名称为 `domain-search`，值之间用逗号分隔。

10. 目录 `/var/lib/ldap` 存储与特定服务器上的 `OpenLDAP` 部署相关的数据库文件。显示的其他目录对于此目的无效。

11. C. `pam_nologin.so` 模块有助于在当 `/etc/login` 存在时防止非 `root` 登录的场景。该模块必须在特定服务的配置文件中指定。例如，使用 `sshd` PAM 配置文件，以下行为 `ssh` 创建了此配置：

```
account required pam_nologin.so
```

12. D. `LDAP` 数据交换格式 (LDIF) 是一种开放格式，定义在 RFC 2849 中，能够启用 `LDAP` 条目的导入和导出。文件格式 `TXT` 和 `CSV` 是有效的，但不是用于所描述的目的。没有名为“`LDAP`”的特定文件格式。

13. C. `pam_unix.so` 模块用于标准登录。`pam_unix` 的主页表明它用于“传统的密码认证”。列出的其他模块不是标准的 PAM 模块，尽管对于 `Squid` 有类似的 `pam_auth` 或 `squid_pam_auth`。

14. B. `radv.conf` 中的 `clients` 是一个接口，允许配置将路由公告发送的特定客户端。此问题列出的其他选项在 `radv.conf` 中无效。

15. B. 调试级别 64 提供配置处理的调试信息。调试级别 1 跟踪函数调用，而级别 8 显示连接管理。调试级别 0 为无调试。

16. B. `max-lease-time` 指令后跟秒数，指定了特定主机在被清除之前可以拥有租约的时间。显示的其他选项在 `dhcpd.conf` 配置文件中无效。

17. B. 被记录的 `DHCPDISCOVER` 消息来自客户端。客户端正在开始从 DHCP 服务器获取 IP 地址的过程。

18. A. 在 `nsswitch.conf` 中，`passwd` 包含有关认证的信息。格式在正确答案中。本地认证通过密码文件的关键字完成。通常还有一行名为 `shadow` 的行，假设服务器使用 shadow 密码。`shadow` 行遵循类似的格式。

19. B. `pam_cracklib.so` 模块强制执行密码强度选项。列出的其他文件对于 PAM 模块无效。

20. B. `-c` 选项指定 `sssd` 的备用配置文件。`-f` 选项将输出到文件。`sssd` 没有 `-a` 或 `m` 选项。

21. C. DHCP failover 在端口 647 上通信。DHCP failover 有助于为此重要服务提供冗余。端口 67 和 68 用于正常的 DHCP 流量，而 389 用于 `LDAP`。

22. C. `routers` 选项定义特定 DHCP 租约的默认网关。与其他选项一样，`routers` 可以在子网级别或针对单个主机指定。其他选项对于描述的目的无效。

23. C. `slapcat` 命令以 LDIF 格式转储 `slapd` 数据库。其他命令无效。

24. D. `pam_limits.so` 模块负责执行问题中提到的限制以及其他如文件最大大小、内存使用等限制。列出的其他模块无效。

25. C. `slapindex` 命令根据 `slapd` 数据库生成索引。其他命令无效。

26. 调试级别可以通过关键字、整数或十六进制等多种方式指定 `slapd`。显示的所有选项都是有效的。调试 0，跟踪 256 或 512，以及 `0x10`。

27. D. `-j` 选项指定从此处开始导入。

28. 从 `OpenLDAP` 2.3 版本开始，配置见 <http://www.ldap.org/doc>。

29. `changetype` 用于条目。

30. B. `-j` 选项显示输出。

31. C. 443 用于 SSL。

32. B. `pam_nologin.so` 模块有助于在当 `/etc/login` 存在时防止非 `root` 登录。

33. A. 格式在正确答案。

34. B. `pam_unix.so` 模块用于标准登录。

35. B. `-f` 选项将输出到文件。

36. B. `-c` 选项指定 `sssd` 的备用配置文件。

37. B. 被记录的 `DHCPDISCOVER` 消息来自客户端。

## 第 22 章：电子邮件服务（主题 211）

1. A. `ddns-update-style` 选项配置服务器在租约创建或确认时执行 DNS 更新。

2. `/var/spool/postfix` 目录包含邮件队列相关文件。显示的其他目录无效。

3. B. PEM 格式用于公钥和私钥。其他方法无效。

4. 关键字用于定义 `Sieve` 中匹配一个或多个条件的邮件的去地。

5. `/etc/postfix` 目录包含与 `Postfix` 配置相关的文件。

6. 位于用户主目录下的 `.procmailrc` 文件被 `Procmail` 用于处理消息。

7. 格式为 `本地地址:目的地址`。

8. `mailq` 命令显示 `Postfix` 服务器的当前邮件队列。

9. A. `postqueue` 命令用于此目的，给定 `-f` 选项时，它将清空队列。

10. `postuper` 命令用于此目的，特别是带有 `-d` 选项。

11. `newaliases` 命令将重新加载 `/etc/aliases` 数据库。

12. `keep` 动作导致消息保留在邮件箱中。

13. `postcat` 命令显示来自 `Postfix` 队列的消息内容。

14. D. 该解决方案使用了 `doveadm` 命令。`-l` 选项会生成当前登录用户的列表、其 PID 和 IP 地址。`doveadm` 或 `dovecot` 没有 `list` 选项，同样，`doccot` 命令也没有 `users` 选项。

15. B. 使用 `discard` 关键字来确保消息被删除。它通常后面跟着 `stop` 关键字，表示不再需要对该消息进行进一步处理。

16. A. `-p` 命令和选项查看待处理队列。`postqueue -f` 命令和选项会刷新队列。显示的其他命令是有效的，但它们的选项无效。

17. C. 将使用重定向（redirect）操作，但不会配合 `:copy` 关键字来保留消息副本。`Sieve` 中没有 `forward` 或 `:duplicate` 关键字。

18. B. `:days` 关键字设置了假期自动回复回复发送者的频率。例如，设置 `:days=1` 意味着相同的消息每天收到一次假期自动回复。其他关键字均无效。

19. C. `qshape` 命令显示有关 `Postfix` 邮件入队列和活动队列中消息数量和年龄的信息。也可以使用该命令查看其他队列。作为此题选项显示的其他命令是无效的。

20. A. `doveconf` 命令显示与 `Dovecot` 相关的配置参数，包括设置名称及其值。`dovecot` 命令是有效的，`doveadm` 命令也是有效的。然而，这些命令中为 `dovecot` 显示的选项是无效。并没有 `doveconf` 命令。

21. A. 如果一组操作中没有其他操作处理电子邮件，则 `keep` 操作具有优先。有一个 `discard` 命令，但它不是默认的。没有名为 `shred` 或 `forward` 的操作。

22. B. `networks` 参数设置允许通过 `Postfix` 服务器中继的网络或主机。其他选项无效。注意，有与 `relayhost` 相关的参数，但那些通常用于设置中继的目的地，而不是允许。

23. D. `doveadm` 命令在配合 `auth` 选项使用时，会为给定用户进行身份验证。有一个 `dovecot` 命令，但该命令没有 `auth` 选项。同样，`doveadm` 没有 `testauth`。

24. D. `m4` 命令将原生的 `Sendmail` 配置编译为最终文件。使用标准重定向将输出发送到最终目的地。

25. A. `postconf` 命令用于此目的，当给定 `-d` 选项时，它会显示当前 `Postfix` 配置中的所有参数。注意，显示的另一个有效命令是 `postfix`，但它使用 `-c` 来实现问题所述的目的。

# 复习题附录

26. `/var/log/mail.err` 文件包含与邮件投递相关的错误。然而，在某些系统上，邮件错误可能会进入不同的日志，例如 `/var/log/mail.info` 或类似文件。

27. `inet_listener` 指令在 `Dovecot` 中创建一个用于监听端口的段（stanza）。可以指定与给定监听器相关的可选参数。

28. A. `SMTP` TCP 端口默认是 25。110 端口是 `POP3`，143 是 `IMAP`。993 端口不是常用端口。

29. `mailq_path` 参数包含 `Postfix` 邮件队列的路径。你可以用它来诊断队列目录的问题。显示的其他参数无效。

30. `EHLO` 命令表示扩展欢迎（Extended Hello）语法，后面是发起通信的主机。在其他选项中，`HELO` 选项是有效的，但此处是无效的。

31. B. `Sieve` 使用 `elsif` 作为替代条件。该关键字的其他形式在许多语言中是有效的，但对 `Sieve` 不适用。没有 `alt` 关键字。

32. `:contains` 关键字查找地址以查看其中是否存在匹配的字符串。其他关键字无效。

33. `:process_limit` 选项指定了 `Dovecot` 的最大登录进程。该参数按服务单独设置。

34. `:domain` 关键字匹配 `Sieve` 中地址的域名部分。其他关键字无效。

35. `IMAPS` 的默认端口是 993。`POP3` 使用 110 端口进行非加密通信，使用 995 进行加密通信。加密 `IMAP` 的默认端口是 143。

36. A. 在 `Debian` 上，`Exim` 配置文件默认为 `/etc/exim/exim4.conf`，但在使用其他 Linux 发行版时，其名称可能不同。

37. `postscreen_tls_security_level` 选项设置了 `postscreen` 服务器的安全级别。应该使用此选项代替 `postscreen_use_tls` 和 `smtpd_use_tls` 选项。

## 第 23 章：系统安全（主题 212）

1. A. `PermitRootLogin` 指令设置为 `yes` 或 `no`，决定 `root` 用户是否可以直接登录。其他选项无效。

2. B. `vsftpd.conf` 文件包含 `vsftpd` 的配置。可以在 `/etc` 或如 `/etc/vsftpd` 等子目录下找到该文件。

3. B. `PREROUTING` 链是 `nat` 表的一部分，包含了在数据包到达时应用的规则。该链的常用用途是重定向（`REDIRECT`）。`REDIRECT` 看起来是，，但实际上是一个目标（target），而不是链（chain）。显示的其他选项无效。

4. A. `OpenSSH` 的主配置文件是 `/etc/ssh/sshd_config`。显示的其他选项无效。

5. C. `iptables-save` 命令创建一个包含当前运行的 `iptables` 规则的文件。该文件可以在下次服务器重启时应用。显示的其他命令无效。

6. B. `-H` 选项允许 `Pure FTP` 不解析主机名。`-n` 选项用于强制执行配额，`-r` 选项用于指示不应覆盖现有文件。`-z` 选项允许匿名用户读取以点开头的目录和文件。

7. D. `ssh-keygen` 命令生成一对公私钥，可用于客户端和服务器之间的用户身份验证。其他命令无效。

8. B. `telnet` 命令用于此目的，对于 `SMTP`，需要像本题正确答案所示使用端口。没有 `smtpt` 命令，且通过名称指定端口或直接指定端口均无效。

9. D. `iptables -n` 选项允许 `iptables` 不解析主机名或端口名。`-L` 选项列出当前规则。没有 `-a`。

10. C. `-i` 选项启用匿名用户上传。`-a` 选项让用户保留在主目录，除非他们是指定组的成员。`-m` 选项在服务器 CPU 负载高于阈值时防止下载。`-n` 选项用于强制执行配额。

11. A. `Port` 选项指定了 `OpenSSH` 服务守护进程监听的端口。客户端需要使用 `-p` 或冒号表示法指定端口以连接服务器。其他选项无效。

12. B. `push` 指令用于在连接时向客户端发送路由。在这种情况下，设置了网络和掩码，255.255.255.0 适用于 /24。其他选项无效。

13. B. `nmap` 命令用于此目的，`-sT` 对指定的宿主机或网络执行 TCP 连接。其他命令无效。

14. D. `/etc/fail2ban` 目录包含与 `fail2ban` 相关的配置文件。其他目录无效。

15. `ip6tables-save` 命令保存当前运行的 IPv6 `iptables` 配置。图中显示的其他命令均无效。大多数与 `iptables` 相关的 IPv6 命令都采用 `ip6tables` 的形式。

16. `PermitEmptyPasswords` 指令设置为 `yes` 或 `no` 时，指定是否可以使用空密码进行身份验证。启用空密码是一个特殊用例，通常不建议这样做。其他选项无效。

17. `-P` 选项设置 `iptables` 中给定链（chain）的策略。在这种情况下，链是 `INPUT`，所需的策略是 `DROP`。

18. `OpenVPN` 默认监听在 UDP 端口 1194 上。其他组合并不是有效的 `OpenVPN` 配置。

19. `Protocol` 指令指定了应该使用的 SSH 协议版本。目前建议使用版本 2。其他选项无效。

20. `DROP` 目标会静默丢弃匹配规则的数据包。`REJECT` 则会发送 ICMP 消息。通常情况下，优先使用 `DROP` 以减少拒绝服务 (DoS) 或信息收集技术的机会。

21. `authorized_keys` 文件包含密钥，当发送相应的私钥时可以使用这些密钥进行身份验证。客户端无效的。

22. `-m match limit` 选项配合所示配置选项创建了所描述的场景。每分钟将产生三条日志记录。这可以防止在攻击进行期间通过填充日志文件或压垮服务器 I/O 来导致拒绝服务。

23. `-X` 选项允许通过 SSH 连接转发 X11。`-A` 选项用于身份验证代理转发（authentication agent forwarding），`-F` 表示用户配置文件。没有 `-X11` 选项。

24. `lsof` 命令和选项可用于此目的。它将显示进程和端口列表，然后用于确定哪个实际进程正在监听该端口。对于其他命令，`tcpdump` 是有效的，但不是解决问题所需的信息。其他命令无效。

25. 使用了 `INPUT` 链，当配合 `-A` 选项时，它向链中追加一条规则。`-p` 选项指定协议（在此情况下为 ICMP），`-j` 选项指定目标（在此情况下为 `ACCEPT`）。`-P` 选项指定策略，未用于此场景。

26. `AllowTcpForwarding` 配置指令决定了是否允许通过 SSH 服务器进行端口转发。启用后，客户端可以通过 SSH 连接转发端口。其他指令无效。

27. 使用了 `INPUT` 链，需要用 `-A` 追加一条规则。指定协议的 `ALL` 选项意味着规则中包含了所有协议。`-s` 选项指定源，在此情况下为单一 IP 地址。最后，`DROP` 目标静默丢弃数据包。没有 `BLOCK` 或 `DISCARD` 目标，且 `ACCEPT` 目标不会接受所有流量。

## 第 24 章：单元测试 1

28. 规则将通过 `-A` 追加到 `INPUT` 链中。在这种情况下，协议将通过 `-p TCP` 指定，目标端口为 2222。指定的源地址 `0/0` 适用于所有规则。将使用 `ACCEPT` 目标。

29. B. 向 `/proc/sys/net/ipv4/ip_forward` 文件写入 `echo 1` 以启用 IP 包转发。这对于利用 NAT 和其他用户是必要的。不存在 `/proc/sys/net/ipv4/nat` 文件。

30. D. `listen_ipv6` 指令用于指示为 `vsftpd` 启用 IPv6。其他指令无效。

31. C. `PubkeyAuthentication` 指令决定是否可以与服务器使用基于密钥的身份验证。其他指令无效。

32. A. `logpath` 指令决定 `fail2ban` 监控失败的日志文件。该文件被作为特定监狱（jail）较大配置的一部分。其他指令对 `fail2ban` 无效。

33. D. `ssh-copy-id` 命令将身份发送到远程服务器，然后用于基于密钥的身份验证。其他命令无效。

34. B. `iptables` 命令用于创建和维护 IPv6 防火墙。`ip6tables` 命令的形式与 `iptables` 命令相似。

35. C. 使用了 `push` 指令，它要求使用 `dhcp-option`，在此情况下为 DNS 192.168.2.1。其他格式和选项无效。

36. A. `local_enable` 指令指定用户是否能够登录服务器。在 FTP 服务器仅匿名的情况下，不会使用此选项。

1. B. `/proc` 文件系统存储了系统上运行进程的信息。`/etc` 文件系统用于配置信息，`/dev` 用于设备信息。默认 Linux 系统上不存在 `/environment` 文件系统。

2. C. `/etc/modprobe.d` 目录包含与 `modprobe` 配置相关的信息。可以通过命令行上的 `-C` 选项进行覆盖。

3. A. `-g` 选项将输入发送到指定的组。答案 B 将输出发送给所有用户，而答案 C 和 D 将不起作用。

4. B. `SIGTERM` 信号是 `systemctl kill` 命令发送的默认信号。



## 第 24 章：测试卷 1

- 5. B. `dmesg` 的 `-e` 选项以通常更易读的格式显示本地时间的增量。

### 附录 = 答案

6. `init` 进程通常与 PID 1 关联。调用 `systemd-udev` 服务关闭系统。

7. `lci` 命令显示设备，`-k` 选项显示正在使用的内核驱动。没有 `showpci` 命令。

8. `--no-wall` 选项不会调用 `telnet` 向登录用户显示状态。

9. `/sys/class/net` 层级结构包含网络配置信息。它是设备的符号链接，按地址而非 `eth0` 名称列出。

10. 系统内故障的逻辑位置是日志文件。

11. `dbus-monitor` 程序需要 X 显示，可用于监控 dbus。

12. 系统可以调度在特定时间关机，该时间应以 24 小时格式输入，如答案所示。

13. `-s` 选项将发送的信号更改为 `SIGTERM`。新信号必须是主信号类型之一，例如 `SIGINT` 或 `SIGSTOP`。

14. `list-unit-files` 命令显示可用文件，而 `--type=service` 将这些文件限制为服务，就像 `hckconfig` 返回服务列表一样。

15. `-c` 选项更改更新的缓存位置而不是默认的 `/etc/ld.so.cache`。小写选项 `-c` 更改缓存格式，而 `-v` 设置详细模式。`-f` 选项不存在。

16. `dpkg` 的 `-P` 选项将从系统中彻底删除（purge）软件包及其与包相关的配置文件。`apt-cache clean` 命令将清理缓存而不是删除单个软件包，`apt-get remove` 命令将删除软件包但不删除关联的配置文件。

17. `deb-src` 前缀用于指示给定存储库包含软件包。选项 A 中的 `deb` 前缀表示普通软件包。

18. `-U` 选项用于升级软件包。添加 `-v` 详细模式和 `-h` 哈希标记可以按照题目要求打印额外信息和进度。

19. `-y` 或 `--assume-yes` 选项将如其名，即假设你将回答是，因此不再提示。其他选项不存在。

21. A. `/etc/yum.conf` 中的 `exclude` 选项是一个由空格分隔的软件包列表，接受通配符，且这些包无法安装或升级。问题中列出的其他选项不存在。

22. C. `ldconfig` 命令用于处理库缓存，`-p` 选项打印缓存中的目录和库。`-C` 告知 `ldconfig` 使用不同的缓存。`ldd` 命令打印指定命令的库依赖，但给出的选项并不适用于 `ldd`。

23. D. `baseurl` 选项用于设置 URL 且必须是完全限定的，这意味着它必须包含 `http://` 或 `file://` 协议。

24. B. `apt-cache dump` 命令将显示可用软件包及其相应的依赖。问题中列出的其他命令和选项不能显示。

25. A. `/boot` 目录几乎存在，但没有被分区到独立空间。如果 `/boot` 分区确实是独立的，它不会被 `lsblk` 隐藏。

26. B. `/var/cache` 层次结构包含两种包管理工具的缓存数据。对于 `yum`，缓存数据存储在 `/var/cache/yum` 中；对于基于 Debian 的系统，缓存数据存储在 `/var/cache/apt` 中。

27. A. 主引导记录 (MBR) 是基于 BIOS 的系统上存储加载程序的典型位置。

28. D. `/filesystem` 是根文件系统。如果没有创建单独的分，`/filesystem` 将是层次结构的起点，并包含同一分区中的所有其他目录。

29. A. `-output` 选项配置命令的输出位置而不是 `STDOUT`。

30. C. 波浪号键 (`~`) 用作用户主目录的替代符号。此处显示的其他选项将无法实现所描述的目的。

31. A. `dd` 命令用于此目的，在 particular 情况下，它通过 `if` 选项接收输入文件，通过 `of` 选项接收输出目标。`-bs` 选项显示块大小为 1 兆字节。

32. D. `history` 命令显示当前会话的历史，可以用于描述的目的。默认情况下，`.bash_history` 文件在会话关闭时写入。

33. C. `--boot-directory` 选项将引导镜像安装到指定的目录中。这对于非标准安装或有时需要单独挂载引导分区的情况可能有所帮助。问题中列出的其他选项不存在。

34. A. 在对 GRUB 配置进行更改后，应执行 `update-grub` 命令以使更改在菜单中生效。问题中列出的其他命令不存在。

35. B. `export` 命令用于此目的，并接受答案所示的 `name=value` 键对。其他命令都是无效的，`echo` 命令除外，`echo` 只会将参数回到控制台。

36. C. `HISTFILESIZE` 选项配置在历史文件中保留的命令数量。其他变量在 Bash 中无效的。

37. D. `-b` 选项配置 `nl` 的正文编号，默认情况下不会对空行进行编号。`-a` 格式选项会对包括空行在内的所有行编号。`-a` 选项不用于 `nl` 命令，`-n` 选项配置编号格式需要额外的参数才能有效。

38. D. `od` 命令用于创建八进制输出。`cat` 命令将显示文件在磁盘上的原始状态。另外两个命令无效。

39. A. `pr` 命令为打印格式化文本，包括每页顶部的日期和页码。添加 `-n` 选项会导致输出双倍行距。`cat` 会显示输出，但不会以这种分页方式显示。另外两个命令无效。

40. A. `-n` 选项用于更改行数。添加 `-N` 选项将从第 N 行开始 `tail` 进程。

41. C. `-i` 选项导致在忽略匹配元素大小的情况下进行唯一性测试。

42. C. 所示的 `awk` 命令可用于此目的。`-F` 选项设置字段分隔符，`OFS` 选项设置输出字段分隔符。

43. C. `-a` 选项等同于 `-d` 和 `-n` 选项，分别保留行递归复制。`-b` 选项创建备份，`-f` 强制复制。

44. A. 在命令模式下，输入数字后跟大写 `G` 会立即将光标移动到该行。`/23` 选项在文件中搜索数字 23。`i23` 选项将插入数字 23，最后 `ZZ` 将退出 Vi。

45. A. `-d` 选项更改更新间隔，在可能影响性能的繁忙系统上可能有所帮助。`-n` 选项设置运行的迭代次数。此项没有 `-t` 或 `-f` 选项。

46. B. `ps -e` 命令用于显示所有进程，而 `-o` 选项配置要显示的列。

47. A. `grep` 命令可用于此目的。注意 `grep -r` 和 `grep -ri` 的区别。问题没有要求区分大小写，因此选项 B 中使用 `-i` 导致它是错误的。

48. B. `find` 命令将用于此目的。需要设置开始查找的目录以及表达式。

49. A. `pr` 命令为打印格式化文本，包括每页顶部的日期和页码。添加 `-n` 选项会导致输出双倍行距。`cat` 会显示输出，但不会以这种方式分页。另外两个命令无效。

50. A. `-n` 选项用于更改行数。添加 `-N` 选项将从第 N 行开始 `tail` 进程。

51. C. `-i` 选项导致在忽略匹配元素大小的情况下进行唯一性测试。

52. C. 所示的 `awk` 命令可用于此目的。`-F` 选项设置字段分隔符，`OFS` 选项设置输出字段分隔符。

53. C. `-a` 选项等同于 `-d` 和 `-n` 选项，分别保留行递归复制。`-b` 选项创建备份，`-f` 强制复制。

54. A. 在命令模式下，输入数字后跟大写 `G` 会立即将光标移动到该行。`/23` 选项在文件中搜索数字 23。`i23` 选项将插入数字 23，最后 `ZZ` 将退出 Vi。

55. A. `-d` 选项更改更新间隔，在可能影响性能的繁忙系统上可能有所帮助。`-n` 选项设置运行的迭代次数。此项没有 `-t` 或 `-f` 选项。

56. B. `ps -e` 命令用于显示所有进程，而 `-o` 选项配置要显示的列。

57. A. `grep` 命令可用于此目的。注意 `grep -r` 和 `grep -ri` 的区别。问题没有要求区分大小写，因此选项 B 中使用 `-i` 导致它是错误的。

58. B. `find` 命令将用于此目的。需要设置开始查找的目录以及表达式。

59. C. `GRUB_TIMEOUT` 变量用于设置。

60. A. 设置路径的语法使用冒号分隔新路径。

61. D. `-L` 选项告诉跟随。

## 第 25 章：测试卷 2

1. A. `/etc/yum.conf` 中的 `exclude` 选项是一个由空格分隔的软件包列表，接受通配符，且这些包无法安装或升级。问题中列出的其他选项不存在。

22. C. `ldconfig` 命令用于处理库缓存，`-p` 选项打印缓存中的目录和库。`-C` 告知 `ldconfig` 使用不同的缓存。`ldd` 命令打印指定命令的库依赖，但给出的选项并不适用于 `ldd`。

23. D. `baseurl` 选项用于设置 URL 且必须是完全限定的，这意味着它必须包含 `http://` 或 `file://` 协议。

24. B. `apt-cache dump` 命令将显示可用软件包及其相应的依赖。问题中列出的其他命令和选项不能显示。

25. A. `/boot` 目录几乎存在，但没有被分区到独立空间。如果 `/boot` 分区确实是独立的，它不会被 `lsblk` 隐藏。

26. B. `/var/cache` 层次结构包含两种包管理工具的缓存数据。对于 `yum`，缓存数据存储在 `/var/cache/yum` 中；对于基于 Debian 的系统，缓存数据存储在 `/var/cache/apt` 中。

27. A. 主引导记录 (MBR) 是基于 BIOS 的系统上存储加载程序的典型位置。

28. D. `/filesystem` 是根文件系统。如果没有创建单独的分，`/filesystem` 将是层次结构的起点，并包含同一分区中的所有其他目录。

29. A. `-output` 选项配置命令的输出位置而不是 `STDOUT`。

30. C. 波浪号键 (`~`) 用作用户主目录的替代符号。此处显示的其他选项将无法实现所描述的目的。

31. A. `dd` 命令用于此目的，在 particular 情况下，它通过 `if` 选项接收输入文件，通过 `of` 选项接收输出目标。`-bs` 选项显示块大小为 1 兆字节。

32. D. `history` 命令显示当前会话的历史，可以用于描述的目的。默认情况下，`.bash_history` 文件在会话关闭时写入。

33. C. `--boot-directory` 选项将引导镜像安装到指定的目录中。这对于非标准安装或有时需要单独挂载引导分区的情况可能有所帮助。问题中列出的其他选项不存在。

34. A. 在对 GRUB 配置进行更改后，应执行 `update-grub` 命令以使更改在菜单中生效。问题中列出的其他命令不存在。

35. B. `export` 命令用于此目的，并接受答案所示的 `name=value` 键对。其他命令都是无效的，`echo` 命令除外，`echo` 只会将参数回到控制台。

36. C. `HISTFILESIZE` 选项配置在历史文件中保留的命令数量。其他变量在 Bash 中无效的。

37. D. `-b` 选项配置 `nl` 的正文编号，默认情况下不会对空行进行编号。`-a` 格式选项会对包括空行在内的所有行编号。`-a` 选项不用于 `nl` 命令，`-n` 选项配置编号格式需要额外的参数才能有效。

38. D. `od` 命令用于创建八进制输出。`cat` 命令将显示文件在磁盘上的原始状态。另外两个命令无效。

39. A. `pr` 命令为打印格式化文本，包括每页顶部的日期和页码。添加 `-n` 选项会导致输出双倍行距。`cat` 会显示输出，但不会以这种分页方式显示。另外两个命令无效。

40. A. `-n` 选项用于更改行数。添加 `-N` 选项将从第 N 行开始 `tail` 进程。

41. C. `-i` 选项导致在忽略匹配元素大小的情况下进行唯一性测试。

42. C. 所示的 `awk` 命令可用于此目的。`-F` 选项设置字段分隔符，`OFS` 选项设置输出字段分隔符。

43. C. `-a` 选项等同于 `-d` 和 `-n` 选项，分别保留行递归复制。`-b` 选项创建备份，`-f` 强制复制。

44. A. 在命令模式下，输入数字后跟大写 `G` 会立即将光标移动到该行。`/23` 选项在文件中搜索数字 23。`i23` 选项将插入数字 23，最后 `ZZ` 将退出 Vi。

45. A. `-d` 选项更改更新间隔，在可能影响性能的繁忙系统上可能有所帮助。`-n` 选项设置运行的迭代次数。此项没有 `-t` 或 `-f` 选项。

46. B. `ps -e` 命令用于显示所有进程，而 `-o` 选项配置要显示的列。

47. A. `grep` 命令可用于此目的。注意 `grep -r` 和 `grep -ri` 的区别。问题没有要求区分大小写，因此选项 B 中使用 `-i` 导致它是错误的。

48. B. `find` 命令将用于此目的。需要设置开始查找的目录以及表达式。

49. A. `pr` 命令为打印格式化文本，包括每页顶部的日期和页码。添加 `-n` 选项会导致输出双倍行距。`cat` 会显示输出，但不会以这种方式分页。另外两个命令无效。

50. A. `-n` 选项用于更改行数。添加 `-N` 选项将从第 N 行开始 `tail` 进程。

51. C. `-i` 选项导致在忽略匹配元素大小的情况下进行唯一性测试。

52. C. 所示的 `awk` 命令可用于此目的。`-F` 选项设置字段分隔符，`OFS` 选项设置输出字段分隔符。

53. C. `-a` 选项等同于 `-d` 和 `-n` 选项，分别保留行递归复制。`-b` 选项创建备份，`-f` 强制复制。

54. A. 在命令模式下，输入数字后跟大写 `G` 会立即将光标移动到该行。`/23` 选项在文件中搜索数字 23。`i23` 选项将插入数字 23，最后 `ZZ` 将退出 Vi。

55. A. `-d` 选项更改更新间隔，在可能影响性能的繁忙系统上可能有所帮助。`-n` 选项设置运行的迭代次数。此项没有 `-t` 或 `-f` 选项。

56. B. `ps -e` 命令用于显示所有进程，而 `-o` 选项配置要显示的列。

57. A. `grep` 命令可用于此目的。注意 `grep -r` 和 `grep -ri` 的区别。问题没有要求区分大小写，因此选项 B 中使用 `-i` 导致它是错误的。

58. B. `find` 命令将用于此目的。需要设置开始查找的目录以及表达式。

59. C. `GRUB_TIMEOUT` 变量用于设置。

60. A. 设置路径的语法使用冒号分隔新路径。

61. D. `-L` 选项告诉跟随。

## 第 25 章：测试题

19. B. `-f` 选项设置账户从过期到禁用之间的天数。`-g` 选项用于设置组 ID，而 `-e` 用于设置总过期日期。

20. A. `get` 命令可以用于描述的目的，它将通过检查别名数据库来显示别名（aliases）。其他命令都是无效的，在所示的 `mail` 命令情况下，它将仅仅尝试向一个名为 aliases 的地址发送邮件。

21. C. `ALL: ALL` 语法将拒绝主机。这意味着你必须使用 `/etc/hosts.allow` 显式授权主机和网络。

22. B. 当以超级用户身份执行 `atq` 时，会显示所有用户的作业。

23. A. `tzconfig` 命令可以在 Debian 系统上用于设置时区。列出的其他命令不存在。

24. C. `crontab` 命令的 `-r` 选项删除指定用户的所有 cron 条目。`-l` 选项列出 cron 任务，而 `-e` 则编辑 crontab。没有 `-d` 选项。

25. A. `-u` 选项指定用户。`-l` 选项列出 cron 任务，`-e` 编辑它们。没有 `-d` 或 `-m` 选项。

26. C. `locale` 命令用于此目的，`-m` 选项显示可用的字符映射。没有 `chapmap` 或 `mapinfo` 命令。

27. B. 时区信息位于 `/usr/share/zoneinfo` 层次中。列出的其他目录通常默认不存在。

28. A. `userdel` 命令在没有其他选项的情况下不会删除其家目录。当给定 `-r` 选项时，该命令将删除家目录和邮件池文件。`userdel` 命令没有 `-h` 或 `-p` 选项。

29. D. `-g` 选项用于为 `find` 命令指定组所有权。`-group` 选项存在，但由于题目指定该组已被删除，因此必须使用 `-gid`。有 `-user` 选项，但它是按名称搜索而非按组 ID 搜索。

30. B. `groupmod` 命令用于此目的，`-n` 选项后跟新组名用于更改名称。没有 `groupcommand`。

31. D. `journalctl` 命令用于在基于 systemd 的系统上查看和解析以特殊格式维护日志的日志条目。`logger` 命令可以创建日志条目，其他命令不存在。

32. A. Red Hat 上的默认位置是 `/var/lib/ntp/drift`。其他位置默认不存在。在 `/etc/ntp.conf` 中，可以使用 `driftfile` 选项更改漂移文件的位置。

33. A. `-o` 选项后跟 1 或 2 可使 `ntpdate` 与旧版 NTP 服务器 兼容。在未指定 `-o` 选项时，默认版本为 3。`-v` 选项告诉 `ntpdate` 输出详细信息，而 `-e` 选项设置身份验证超时。

### 附录 ■ 复习题答案

34. D. 目录 `/var/log/journal` 用于存储基于 systemd 系统的 journal 日志文件。其他目录默认不存在。

35. C. `-m` 选项设置发送邮件日志时使用的邮件程序。默认设置为 `/usr/bin/mail -s`。没有 `-o` 选项，且 `-v` 是详细模式。`-s rotate` 命令设置要使用的状态文件。

36. A. `-u` 选项无论时区如何都将输出配置为 UTC。`-s` 选项设置时间，没有 `-v` 或 `-t` 选项。



## 练习题解答（续）

37. D. `lprm` 命令用于从使用 `lp` 系统打印的系统中删除作业。没有 `lpdel` 或 `rprint` 命令。有 `rm` 命令，但它不用于打印队列。

38. C. `<<<` 字符组合从 `STDIN` 或标准输入读取输入并将其作为 `mail` 命令的消息体。

39. C. `groupdel` 命令用于从系统中删除组。该组不能留任何成员，否则命令将失败。

40. C. `lp` 设施将消息从 `lp` 子系统发送到 `syslog`。`auth` 设施用于安全相关消息。列出的其他选项不是 `syslog` 设施。

41. D. `255.255.255.0` 子网掩码等于 `/24`。`255.255.255.0` 子网掩码是 `/23`。子网掩码 `255.255.255` 是 `/32`，而 `255.255.255.0` 是 `/16`。（注：此处原文逻辑似乎存在数值对应错误，如掩码与位数的不符，翻译已按原文字面意思）

42. A. 将首先识别 `/etc/hosts` 文件，并根据所示配置发送 `DNS` 查询。

43. 标准 `LDAP` 是服务器上的 `TCP` 端口 `389`。`TCP` 端口 `25` 是 `SMTP`，`443` 是 `HTTPS`，`143` 是 `IMAP`。

44. C. `-l` 选项更改身份验证的用户名。这对于不使用 `@` 符号的脚本场景非常有用。`-v` 选项是详细模式，`-i` 是要使用的身份标识文件。没有 `-u` 选项。

45. D. `-n` 选项禁用 `ping` 请求/响应中地址的名称解析。`-D` 选项返回时间戳，而 `-d` 设置 `SO_DEBUG`。最后，`-f` 是。

46. A. `ifconfig` 命令显示接口的开启或关闭状态，包括数据包数。

47. B. `dig` 允许 `IPv6`。

48. B. `/etc/hosts` 中的 `-6`。

49. C. `dig` 选项显示 `SOA`。

50. A. `/etc/resolv.conf` 中的 `-n`。

# 第 26 章：测试题

51. C. `/etc/hosts.allow` 中的 `-w`。

52. C. `/etc/cron.deny` 中的 `-u`。

53. C. `/etc/cron.allow` 中的 `-s`。

54. A. 默认是秒。

55. B. 选项用于输出。

56. B. 选项显示用户。

57. C. `sysctl` 命令查看内核参数。

58. `ssh_config` 文件中的 `Banner` 选项。

59. `-prefix` 选项设置编译代码将安装的目标目录。

60. `rsync` 的归档选项 `-a` 等同于多个其他选项。

61. `-D` 选项禁用向控制台打印。

62. `-g` 选项显示组播信息。

63. `ip` 命令使用 `-r` 解析 IP 地址。

64. `ss` 命令被使用，当使用 `-o` 选项时显示计时器信息。

65. A. `--delay` 设置检查间隔。

66. A. `--assemble` 选项启动停止的阵列。

67. A. `sfdisk` 命令用于此目的，指定操作的磁盘分区。

68. `WWID`（宽标识符）识别独立的 `SCSI` 设备。

69. `iscsiadm` 的发现模式发现 `iSCSI` 目标。

70. `vgscan` 命令用于构建 `LVM` 缓存。

71. `sysctl` 命令可以查看当前主机名。

## 第 26 章：测试题 361

72. C. `-m` 序列表示主机不可达（host unreachable）。网络不可达（Network unreachable）是 `-N`。

73. A. `-m` 选项指定数据包如何标记或标签。`-a` 选项是音频 ping（audible ping），而 `-p` 启用指定自定义填充。没有 `-k` 选项。

74. D. 环境变量 `TAPE` 可用于指定 `mt` 操作的设备。其他环境变量不被 `mt` 命令使用。

75. C. `/etc` 目录及其子目录包含配置文件，这些文件在恢复场景中重新创建系统是必要的。`/var` 目录包含变量信息，而 `/opt` 可能用于其他几种用途。`/bin` 目录包含可以重新安装的二进制文件。

76. B. `-i` 选项告诉 `patch` 忽略空格。当补丁文件与所需的内容不完全匹配时，这可能是必要的。`-p` 选项设置补丁的目录层级，而 `-e` 告知 `patch` 解释为 `ed` 脚本。`patch` 没有 `-w` 选项。

77. C. `-i` 选项设置 `isciadm` 中 `ping` 请求之间的间隔。`-a` 选项设置 `ping` 模式下的 IP 地址，`-s` 设置数据库操作，且没有 `-e` 选项。

78. B. `-C` 选项检查支持该操作的驱动器的电源模式。`-a` 选项获取或设置扇区计数，`-d` 通过使用 `-adm` 选项获取或设置，而 `-f` 选项在退出时同步并冲刷驱动器的缓冲区缓存。

79. D. 文件 `/proc/swaps` 包含给定计算机上可用交换空间的信息。其他文件默认不存在。

80. B. `rescue` 从救援模式启动系统，可以在模式下执行系统恢复。其他目标（targets）均无效。

81. B. `-r` 选项显示一份报告，包括 `CPU` 时间和退出状态，内容针对刚完成的 `fsck` 操作。`-f` 选项强制执行任何请求，`-s` 将 `fsck` 操作序列化，而 `-l` 创建一个排他的 `flock`。

82. C. `noconfig` 目标在为内核编译创建新配置时对每个问题都回答是。在其他选项中，只有 `config` 目标有效，用于创建普通配置，并提示包含哪些内核部分。

83. D. 文件 `/proc/meminfo` 提供了关于内存使用和利用的大量信息。这些信息大部分由各种命令显示，但这些命令的规范来源通常在该文件中找到。在其他选项中，只有 `/proc/cpuinfo` 有效，并为计算机的 `CPU` 提供信息。

84. B. `-p` 选项显示给定模块的参数。其他选项对 `modinfo` 命令无效。

85. C. `-k` 选项显示给定 `PCI` 设备的内核驱动程序。`-d` 选项从指定的供应商中选择设备。其他选项无效。

86. D. 此目的应使用 `uudev` 命令，`hwdb` 模式与硬件数据库配合。`-u` 选项更新数据库。

# 附录 ■ 复习题答案

87. A. `systemd-delta` 命令通过显示覆盖（overrides）、屏蔽（masked）和其他文件冲突和排序来帮助整理描述的场景。其他命令和选项无效。

88. B. `grub-install` 命令用于此场景。`SCSI` 磁盘位于 `/dev/sd*`，第一个磁盘是 `/dev/sda`，第二个是 `/dev/sdb`。选项 D 是错误的，因为它同时列出了 `/dev/sdb` 和分区号 2。

89. D. `blkid` 命令显示适当设备的 `UUID` 和其他相关信息。其他命令无效。

90. C. `LUKS` 加密是 `dm-crypt` 命令的默认模式。其他模式包括 `plain`、`loopyes` 和 `lrypt`。

91. B. `-b` 选项接受一个包含 El Torito 启动镜像的文件参数。启动镜像的大小必须为 `1200`、`1440` 或 `2880 KB`。其他选项在 `mkisofs` 中无效。

92. A. 退出代码 `64` 表示某些磁盘失败了 `trim` 过程。退出代码 `0` 表示成功，`1` 表示失败，`32` 表示全部失败。

93. D. `arp` 命令的正确选项是 `-s`，格式为地址后跟硬件地址。`-d` 选项删除条目，`-a` 显示所有条目。

94. B. `txpower` 选项显示接口可用的发射功率。`power` 选项可用，并列出接口的电源管理模式。另外两个无效。

95. D. 使用 `nmap` 的 `-sX` 模式可以进行 Xmas 扫描。`-sT` 是 `TCP` 连接，`-sS` 是 `TCP SYN`。没有 `-sP` 选项。

96. A. `-s` 选项设置捕获的快照长度（snaplen），而不是其默认的 `65535` 字节。`-l` 选项提供行缓冲，`-c` 在接收指定数量的数据包后停止，`-d` 将编译后的数据包匹配代码转储为可读的格式。

97. B. `-r` 选项反转日志，先显示最新的条目。`-n` 选项显示最近的 N 个事件，`-f` 是跟踪（follow），`-b` 告诉 `journalctl` 显示来自特定 ID 的消息。

98. B. 文件 `/etc/lvm/.cache` 使用 `vgscan` 构建，是 `LVM` 设备的所在地。

99. D. `hdparam` 没有 `-e` 选项。

100. D. `emergency` 目标可以恢复系统。其他目标无效。

101. A. `-i` 选项告诉 `patch` 忽略空格；因此需要 `-g` 和 `-o`。

102. B. `-f` 选项绕过路由表并直接发送数据包。`-A` 选项是自适应 `ping`，而 `-b` 启用广播。

103. A. `tracer` 命令默认使用 `UDP` 并选择任何端口。

104. C. `/nst*` 设备是非卷带；因此，索引 `0` 是第一个设备。`/dev/sd*` 设备是普通的 `SCSI` 设备。

105. A. `/var` 目录通常包含变量信息。但邮件池文件通常存储在 `/var/mail` 或 `/var/spool`。`/etc` 目录包含配置信息，`/usr` 包含可以重新安装的文件。`mail` 目录不存在。

106. B. `-b` 选项在补丁之前备份文件。这在顺序执行多个补丁的场景中特别有用。`-d` 选项导致目录更改，而 `-c` 告诉 `patch` 将补丁文件解释为普通文件。`-s` 选项允许 `patch` 在静音模式下工作。

107. D. `-g` 选项显示包含指定信息的几何结构。`-h` 选项显示帮助，`-w` 选项重启设备。挂载没有 `-e` 选项。

108. B. `--no-wall` 选项抑制警告发送给登录用户。其他选项无效。

109. C. `-C` 选项可用于在 `fsck` 操作显示进度指示。`-f` 选项强制执行，而 `-p` 和 `-d` 不退出。

110. C. `tinyconfig` 目标针对最小可能的内核配置。其他目标对内核无效。

## 第 27 章：测试题 4

1. C. `notify` 指令设置为 `yes` 或 `no`，用于指定是否通知从服务器服务器区域的变化。其他选项均无效。

2. A. `-b` 选项允许指定密钥长度。`-a` 选项指定算法。`-f` 选项在 `key/dnskey` 记录中设置标志位。通常没有 `-e` 选项，但在某些版本的 `Linux` 中，它可能与大指数有关。

3. B. `-q` 选项完全抑制输出，从而使命令在成功时不打印任何内容。然而，它会返回退出代码 `0` 表示成功，因此该命令可以用于脚本场景。`-f` 选项指定区域格式。`-s` 选项对 `named-checkzone` 无效，且没有 `-p` 选项。

4. B. 大多数 `BIND` 区域的记录类型为 `IN`，意味着 Internet（互联网类）。其他选项不是有效的类型。

5. C. `rndc` 命令默认在端口 `953` 上监听。端口 `53` 用于 `DNS` 但不用于 `rndc`。端口 `530` 是 `Rpc`，端口 `1053` 并不是定义的已知端口之一。

6. C. 权威起始记录被称为 `SOA` 记录。`NS` 记录是名称服务器，`A` 记录是普通地址记录。`IN` 是记录的类型，并不直接回答所提的问题。

7. A. `@` 符号可以作为设置 `dig` 命令查询服务器的方法。所示其他选项均无效。

8. D. `forwarders` 指令是一个地址列表，请求将从该服务器转发到这些地址。其他选项均无效。

9. A. `query-source` 指令设置查询看似源自的 IP 地址。这在多网服务器中非常有用，因为服务器可能无法正确选择使用哪种接口。其他选项均无效。

10. A. `-D` 选项以规范化格式（canonical format）转储区域文件。其他选项对此目的均无效。

11. B. `-t` 选项后接目录，允许 `named-checkconf` 读取指定目录下的文件。

12. A. `-B` 选项指定程序应对密码使用 `bcrypt`。`-C` 选项设置 `bcrypt` 使用的计算时间。`-b` 选项设置批模式，`-m` 选项对密码使用 `md5`。

13. C. `Server Tokens` 指令影响服务器生成的文档如何返回版本号，甚至决定是否返回版本号。所示其他指令均无效。

14. D. `httpd.conf` 是 `Apache2` 服务器的主配置文件。`httpd.conf` 通常包含一个或多个包含进一步配置信息的文件和目录。`httpd.conf` 文件通常位于 `/etc/` 层级下，但其具体的子目录很大取决于 `Linux` 发行版。

## 第 27 章：测试题 365

15. B. `http_port` 指令设置 `Squid` 监听连接的端口。默认情况下，`Squid` 监听端口 `3128`。所示其他选项均无效。

16. B. `SSLCertificateFile` 定义 SSL 托管场景下公钥的位置。`SSLCertificateKeyFile` 设置私钥的位置。其他指令无效。

17. C. `SSLCipherSuite` 允许选择服务器上可用的加密密码算法。这对于将密码算法限制为认为在任何时候都是安全的算法非常有帮助。

18. C. 格式为 `GroupName: name1 name2 name3`，因此选项 C 是正确答案。

19. A. `%B` 序列用于记录包括 `HTTP Header` 在内的字节数。`%B` 序列紧跟使用 `HTTP Header` 的字节数。日志序列以百分号开头，使得其他选项错误。

20. C. `-newca` 选项开始通过 `ca.pl` 脚本创建新的证书颁发机构，该脚本是 `openssl` 命令的助手，用于关联证书的生成和管理。

21. C. 用于 `Samba` 的文件通常存储在 `/etc/pki` 层级下的 `/etc/samba`（或其子目录）中。不存在 `/etc/private` 或 `/usr/share/samba` 目录。

22. D. `nmbd` 守护进程监听 `UDP` 端口 `139`，`445` 端口由 `smbd` 守护进程使用，端口 `143` 是 `IMAP`，与 `Samba` 无关。

23. A. `force-election` 消息类型发送到 `smbd`，用于强制进行浏览器主选举。其他消息类型在 `smcontrol` 中无效。

24. B. `ads` 模式启用在 `Active Directory` 环境中的集成。`rpc` 模式适用于远程过程调用环境。另外两种模式无效。

25. C. `@` 字符用于指定在使用导出的 `NFS` 文件系统时使用的 `NIS` 网组。其他语法示例均无效。

26. A. 凭据（Credentials）作为选项包含。选项通过 `-o` 指定。可以按所示指定用户名和密码。没有 `credentials` 命令行参数。

27. C. `domain` 的安全级别用于基于 `Active Directory` 的域安全模式。在域控制器和域之间建立了信任。

28. A. `-a` 选项显示主机名或 IP 地址。其他选项无效。

29. B. `-S` 选项显示共享列表。其他选项均无效。

30. 如果用户已存在，`smpasswd` 将更改密码。

31. 端口可以通过 `-p` 设置。`-d` 选项设置调试级别，其他选项无效。

32. D. `fixed-address` 指令为主机保留地址。当主机请求地址时，将获得指定的地址。

33. A. `ldapadd` 添加条目需要 `LDAP` 服务器在线。`slapd` 无此要求。两者作用于本地数据库。

34. C. `radvd` 接口中的 `Ignoremissing` 选项在接口不存在时改变其行为。

35. B. `default-lease-time` 选项后接租约数，用于指定客户端请求新租约之前的时间。

36. C. `/etc/nswitch.conf` 包含名称服务开关（`NSS`）的信息。格式如答案所示。本地文件被称为 `files`，在 `/etc/nswitch.conf` 中称为 `ldap`。

37. C. `[sssd]` 部分定义了用于 `SSSD` 系统的通用参数。部分用括号括起。

38. A. `limits.conf` 位于 `/etc` 或 `/etc/security`，提供了与 `pam_limits.so` 模块相关的基本配置。在某些发行版中也可以在 `/etc/security/limits.d` 找到相关文件。

39. B. `-l` 选项允许指定输出文件而非 `stdout`。`-f` 选项允许命令指向 `sldap` 配置文件。`-d` 选项指定调试，`-o` 允许指定扩展选项。

40. `modify` 更改类型指定条目将被更改。其他更改类型无效。

41. A. `mail` 属性位于 `inetOrgPerson` 中。`inetOrgPerson` 的其他属性包括 `homePhone`、`gn` (`givenName`) 等。在其他选项中，只有 `organization` 是有效的 `objectClass`。

42. D. `gt` 运算符用于在 `Sieve` 中测试大于条件。`ge` 测试值是否大于或等于。其他运算符不用于 `Sieve`。

43. B. `/etc/dovecot` 目录用于与 `Dovecot` 邮件守护进程相关的配置文件。其他目录默认不用于 `Dovecot`。

## 第 27 章：练习题 367

44. B. 查看队列的 `sendmail` 命令使用 `-bp` 选项。对于 `Postfix` 等邮件服务器，为了兼容性，提供了模拟的 `sendmail -bp`。

45. C. `postsuper` 命令用于此目的。当给定 `-d ALL` 参数时，所有消息都将被删除。但由于问题指定指定延迟队列（deferred queue），因此添加了关键字 `deferred` 以限制删除范围。

46. D. `-b` 选项使用 `postcat` 只显示消息正文，而不是信封 (`-e`) 和头部 (`-h`)，后者是该命令的默认选项 (`-beh`)。没有 `-m` 选项。



- 47. 一个 `if` 语句将使用 Sieve 执行条件测试。在这种情况下，需要大小测试，我们将使用 `:structure` 进行比较。`messagesize` 消息不起作用，但值得注意的是，Sieve 可以使用大于号。

- 48. B. 使用 `doveadm` 命令，特别是带有 `pw` 参数。该命令将提示输入密码（两次），并将生成的加密密码作为输出显示。

- 49. `message_size_limit` 参数用于设置发送至或发自 Postfix 服务器的任何单条消息的默认大小。默认值为 10,240,000 字节。

- 50. C. `:all address-part` 是互联网地址，且在没有指定其他地址部分时，它是默认值。其他选项不是有效的地址部分。

- 51. A. SMTP 会话中的 `RCP TO` 是指定目标地址的地方。显示的其他选项不是邮件投递的 SMTP 会话部分的一部分。

- 52. D. `REDIRECT` 目标用于在 iptables 中创建重定向。它通常在 `PREROUTING` 链中使用。其他目标是无效的。

- 53. A. `-t` 选项限制认证用户的带宽。`-t` 选项的作用相同，但对于 `-b`，它是在后台启动 Pure-FTPD，而 `-b` 表示 Pure-FTPD 将忽略 RFC 标准，以便与不符合标准的 FTP 客户端配合。

- 54. B. `nc` 命令可用于此目的，并需要指定端口，在这种情况下为 80。`nc` 命令的其他格式将不起作用。

- 55. C. `-F` 选项刷新或清除任何 iptables 链中的规则。该选项在 iptables 脚本的开头非常有用，用于清除现有规则以准备新的重置。`-P` 选项设置链的默认策略。

- 56. A. `AllowUsers` 指令用于指定允许登录服务器的用户。其他选项均无效。

- 57. 向 `/proc/sys/net/ipv4/conf/all/rp_filter` 写入 1 可以防止数据包从与其到达时接口不同的接口进入。`rp_filter` 中的 `rp` 是反向路径（reverse path）的缩写。

- 58. D. `-L` 选项设置本地端口转发，因此在该场景下是必需。它后面跟着本地端口，然后是连接将转发的主机/端口。其他选项对于该场景描述的目的无效。`-p` 选项连接到特定端口，但不会创建端口转发。

- 59. B. `/etc/services` 文件包含给定服务器的端口到名称的翻译。该文件包含已知端口，并可以根据每个服务器进行自定义。

- 60. A. `--log-prefix` 选项指定了 iptables 创建日志条目时的前缀字符串。显示的其他选项不可用于 iptables。

## 访问 (Access)

- 邮件滥用账户, 92

- `AccelerationProfile` 选项, 67

- 访问控制列表 (ACLs) 位于

    - Suid, 194

    - `access_log` 文件, 196

    - `AccessFileName` 指令, 196–197

- 可访问性

    - `AccessX` 选项, 71

    - Ubuntu, 246

    - `AccessX` 工具, 71

    - 过期, 76, 115

    - 信息, 111

    - 锁定, 117

    - 解锁, 252

- `acl` 条件指令, 194

- ACLs (访问控制列表) 位于

    - Suid, 194

- Active Directory 安全, 272

    - `@admins` 选项, 271

    - `net` 命令的 `das` 模式, 271

    - 广告，节点限制, 211

    - 告警监控, 123

- `alias` 命令, 55, 244

- `Alias` 指令, 198

- 别名命令，删除, 57

- 别名命令, 244

- 邮件, 88, 247

- 所有 `address-part` 结构, 275

- `/etc/hosts` 中的 `ALL:` 选项。拒绝, 113

- `alloconfig` 目标, 260

- CUPS 打印系统 `Allow` 指令, 89

- `allow-guest` 选项, 66

- `allow-query` 指令, 185

- `allow-recursion` 选项, 189

- `allowTcpForwarding` 指令, 229

- `AllowUsers` 指令, 276

- LightDM 中的 `Alt+Ctrl+F` 键, 70

- 读者的 `Alt+Super+S` 键, 69

- 修改的文件，检查, 19

- 条件执行, 56

- `anacron` 命令, 77, 81

- `ANY` 查询类型, 188

- Apache 访问

    - 文件名, 196–197

    - 认证设备, 193, 195

    - `AuthGroupFile`, 270

    - 授权, 196–197

    - 子进程, 198

    - 密算法, 270

    - 目录, 195

    - 文件显示, 195

    - 日志文件, 396

    - 模块启用, 195

    - 进程 ID, 33

    - 服务时间, 197

    - SSL 配置, 194

    - SSL 私钥, 196, 270

    - SSL 版本, 194

    - SSL 版本信息, 269

    - `<VirtualHost>` 指令, 193

    - Web 服务器格式, 270

    - Apache 服务器配置, 270

    - `systemctl config`, 193

    - `systemctl status`, 197

    - GNOME 中的外观部分, 68

    - 转发, 228

    - `apt-get update` 命令, 20

    - `apt-get upgrade` 命令, 17

    - apt 风格系统缓存, 236

    - 架构，信息, 30

    - 存档, 177, 179

    - 禁用, 171

    - 格式, 262

    - `apt -d` 命令, 168

    - `apt -s` 命令, 169, 262

    - `ARRAY` 命令, 59

    - 辅助技术

    - 边界键, 70

    - 屏幕键盘, 78

    - 星号 (`*`)

    - `case` 语句, 61

    - 主机, 202

    - 正则表达式, 35

    - `at` 命令, 77–78

    - `dig` 中的 `#` 符号, 268–269

    - 以太网 ATA (AE), 160

    - `atq` 命令, 288, 247

    - `atrm` 命令, 79

## 认证 (Authentication) - 缓存

- Apache 指令, 197

- Apache coverlet, 220, 222

- 外部文件, 214

- Kerberos, 201

- 密钥, 117, 228

- LDAP, 211

- OpenSSH, 230

- PAM 模块, 210

- 弹出窗口, 195

- `rnd`, 230

- SSH, 222

- `vsftpd.conf`, 230

- `AuthGroupFile` 指令, 197, 270

- `AuthName` 指令, 195

- `Banner` 选项, 257

- `baseurl` 选项, 235

- Bash

    - 命令历史, 35, 37, 241

    - 命令行参数, 55

    - 条件, 55, 57, 244

    - 配置文件, 55

    - 环境设置, 30, 61, 237

    - 文件命令, 54

    - 函数, 245

    - 初始化文件, 59

    - 输出重定向, 30, 34-35

    - 源文件, 57

- `blkid` 命令, 48, 152, 261

- 块

    - 坏, 49, 241

    - 显示, 123

    - 大, 154, 178

- `/boot` 分区

    - `/dev/sda1`, 143

    - `extlinux`, 143

    - 大, 20

- `/boot/efi` 分区, 10, 145

- 启动过程

    - `/boot` 镜像, 237, 261

    - 配置, 145

    - GUI, 6

    - 消息, 9

    - 顺序, 50, 143

    - 分区, 236

    - 救援模式, 260

    - 根分区挂载, 100

- 引导加载程序

    - Apache - 196

    - 外部文件, 214

    - `authorized_keys` 文件, 112, 228

    - `AuthUserFile` 指令, 193

    - 用户界面, 101

- `autofmusters`, 151

- `autologin-user` 选项, 70-71

- 自动登录

    - LightDM, 70–71

    - 可用字符集，显示, 77

- `awk` 命令, 238

- CD-ROM, 144

- GRUB, 261

- `grubx64.efi`, 147

- `MBBRs`, 236

- UEFI, 144

- 边界键, 70

- 盲显示器, 67

- 广播消息, 179

- Samba 中的 `browsable` 选项, 204

- 浏览主选举, 271

- `trfs` 文件系统

    - 写时复制功能, 152

    - 子卷, 155–156

- `trfs volume` 创建命令, 155

- `trfs volume` 快照命令, 136

- 绕过路由表, 263

### Cacti 工具 — CPU 371

- 库, 16, 235

- 位置, 234

- LVM, 256, 263

- 软件包, 20–21

- `yum` 和 `apt` 风格, 236

- Cacti 工具, 124

- `case` 语句 (case statements)

    - 默认情况 (default case), 61

    - 结束, 32

    - `cat` 命令, 32

    - `cat /passwd` 文件, 31

    - `cat /proc/interrupts`

    - 命令, 5

    - `cd --` 命令, 236

- CD-ROMS, 引导加载程序 (bootloader), 用于, 146

- 证书签名请求 (CSRs), 125

- 证书 (certificates)

    - 证书授权机构 (CA), 271

    - TLS 配置, 217

- `change -d` 命令, 81

- `change -E` 命令, 76, 115

- `change -l` 命令, 111

- 修改密码日期, 81

- `type add` 命令, 213

- 字符映射 (character maps), 248

- 字符多字节表示, 78

- 字符集 (character sets), 77

- `chgrp` 命令, 48

- `chgrp -R` 命令, 50

- `chgrp users` 命令, 43

- Apache 中的子服务器进程, 192

- `chkconfig --list` 命令

    - 启动文件, 144–145

    - 服务与运行级别 (runlevels), 10

    - systemd 等效项, 234

- `chmod` 命令

    - 权限, 57

    - 粘滞位 (sticky bits), 45

- `chown` 命令, 241

- `chown -R` 命令, 47

- chroot 环境

    - BIND, 188–189

    - 家目录目录, 186

    - `named-checkconf`, 269

- 子网掩码的 CIDR 表示法, 101, 103

- `cifs` 文件系统, 202

- 清理目标 (clean target), 133, 178

- 清除 iptables 规则, 276

- 节点限制的 `clients` 选项, 211

- 时钟 (clock)

    - 设置, 91–92

    - 操作, 89

- `CNAME` 记录, 187

- `ColorDepth` 选项, 270

- 表格中的列, 55

- Bash 中的命令行参数, 55

- 别名 (aliases), 244

- 感叹号, 37

- 日志执行时间, 54

- 历史 (history), 35, 237

- 信息, 44

- 管道与重定向, 59

- 读取与执行, 54

- 调度, 77, 80

- 注释 (comments), 117

- 通信, 监控, 239

- 编译代码位置, 257

- 已完成打印任务的显示, 92–93

- 压缩 (compression)

    - `bzip2`, 133

    - 日志文件, 94

    - 源代码, 174

- 计算机，关机, 180

- 条件执行, 56–57

- 配置文件 (configuration files)

    - Apache2 服务器, 270

    - `autofs` 自动挂载器, 151

    - 备份, 259

    - ACPI 描述符 (ACPI Descriptor), 182

    - BIND, 185, 187

    - 调试, 211

    - Dovecat, 274

    - Exim 4, 222

    - `fail2ban`, 227

    - `FCo`, 14

    - 问候, 65

    - `isicid` 守护进程, 126

    - ISOLINUX, 145

    - LightDM, 71, 246

    - 日志文件, 91

    - `modprobe` 命令, 232

    - 网络接口, 173

    - OpenLDAP, 213

    - OpenSSH, 225

    - 顺序, 55

    - 覆盖, 144

    - PAM 模块, 209, 274

    - PHP, 195

    - Postfix, 217

    - 优先级, 144

    - Proxmox, 217

    - RAID 设备, 159

    - 重新加载, 9

    - Samba, 201, 204

    - Sendmail, 220

    - SSL, 271

    - `ssd`, 252

    - `syslog-ng`, 94

    - 更新, 16

    - 验证, 193

    - `vsftpd`, 225

    - `/configure` 命令, 180

    - 配置脚本 (configure script)

        - 描述, 178

        - `--help` 选项, 182

    - USB 连接, 11–12

    - 连通性规则 (connectivity rules)

        - 网络, 170

        - SMTP, 226

        - `:contains` 关键字, 221

        - SMTP 会话, 221

    - 写时复制文件系统 (copy-on-write filesystems), 152

    - 拷贝 (copying)

        - 目录, 32

        - 文件, 275

        - 符号链接 (symlinks), 238

    - 损坏的系统, 50

    - `cp -i` 命令, 32

    - `cp -R` 命令, 32

    - CPU

        - I/O 等待时间, 125

        - 性能, 125

        - 时间信息, 260

        - 时间限制, 113, 212

        - 使用, 128

### 凭据 (Credentials) - DHCP

- 凭据 (credentials)

    - 文件, 197

    - `.htaccess` 场景, 193

    - 提示, 117

    - Samba, 272

- 定 `cron` 任务 (cron jobs)

    - 执行, 76

    - 移除, 247

    - 调度, 77

    - 全局文件, 79

    - 用户, 76, 78, 82, 247

    - 被拒绝的用户, 81, 252

    - `crontab -` 命令, 82

    - `crontab -` 命令, 247

    - `crontab -` 命令, 247

- 加密密码 (cryptographic ciphers), 270

- CUPS 打印, 195

- 已完成打印任务, 92

- 配置文件, 88

- 大括号 (`{}`), 37

- 货币相关本地化, 83

- 当前目录，打印, 37

- 当前日志, 112, 123

- 当前数量, 9

- 自定义日志文件, 94

- `date -s` 命令, 95

- `date -u` 命令, 249

- 日期 (dates)

    - 环境变量, 78

    - 过期账户, 113

    - 已登录用户, 253

    - 密码修改, 115

    - 设置, 88, 95

    - UTC, 249

    - 回复, 219

    - `decheck` 命令, 204

    - `debs-monitor` 命令, 233

    - `debs base` 命令, 178

    - `debs-activating` 交换空间, 155

    - `debs-pgk` 选项, 134

    - `debs-sec` 前缀, 234

    - `debug -c` 命令, 50

    - `debug -w` 命令, 153

    - 调试 (debugging)

        - 配置文件, 211

        - 启用, 172–173

        - 只读变量, 61

        - 解压缩文件, 36

        - `debs-lease-time` 选项, 273

        - `debs-target`, 147

        - `debs=o` 选项, 18

        - `case` 语句, 61

        - CUPS 端口, 91

        - `delay` 虚拟主机目录, 195

        - `delay` 速率, 246

        - `delays in ping` 请求, 259

        - `DELETE` 语句, 55



- 分隔符 (`delimiters`), 33
- `deny-by-default` 策略, 247
- `deny-owned-clients` 行, 214
- 依赖 (`dependencies`)
    - 检查, 178
    - 下载, 23
    - 模块, 5
    - 软件包, 18, 235
    - `deplist` 选项, 18
- 仓库 (`repositories`), 19
- `depool` 命令, 134
- `de-script`, `de-ESC` 命令, 55
- `/dev/disk/by-id` 目录, 159
- `/dev/disk/by-path` 文件, 160
- `/dev/idv0` 设备, 262
- `/dev/mapper` 目录, 162
- `/dev/nst0` 设备, 264
- `/dev/nvme*`, 160
- `/dev/sda1` 磁盘, 243
- `/dev/sdX` 标识符, 5
- `/dev/sd0` 设备, 179
- `DEVICE` 配置行, 159

## 设备 (`devices`)

- 启动顺序, 50
- 显示, 7
- 过滤器 (`filters`), 164

# D

- `%D` 日志格式, 197

## 数据库 (`databases`)

- 硬编码 (`hardcode`), 261
- 主机, 103
- `LDAP`, 210, 213
- 查找, 47
- `OpenLDAP`, 210
- `sendmail` 更改, 94
- `slapcat`, 213
- 排序, 57
- `date` 命令, 61
- 双端口接口, 18
- `/etc/fstab`, 154
- 网关, 100, 104
- 操作系统, 19, 22
- 进程优先级, 35
- 路由, 100
- 运行级别, 147
- `shell` 提示符, 54
- 目标, 11
- 地址请求, 214

## 域名后缀搜索 (`domain suffix search`)

- 顺序, 210
- 故障转移 (`failover`), 212
- 租约 (`leases`), 211
- 消息, 211
- `OpenVPN`, 230
- 端口, 212
- `IP` 地址, 104
- `UUIDs`, 261
- `df` 命令, 124
- `df -BT` 命令, 43
- `df -1` 命令

## `dhcpcd.conf` 文件 – 内核模块支持 (`dkms`)

- 预留 (`reservations`), 209, 273
- 子网 (`subnets`), 209
- 系统日志, 172

## `dhcpcd.conf` 文件

- 动态 `DNS` 更新, 209
- 未检测到, 8
- 模式, 259
- 准备顺序, 43
- 用户使用, 123
- 利用率, 124
- 域名安全级别, 72
- 不存在的域名, 106
- 完成工作 (`donework`), 61
- `IP` 地址, 273
- 租约 (`leases`), 211–272
- `DHCPDISCOVER` 消息, 211
- 写入数据, 153
- 显示信息, 67
- `DISPLAY` 事件变量, 65, 246
- 显示电源管理信号 (`DPMS`), 72
- 正则表达式 (`regular expressions`), 35

## `source` 命令

- 等效性 (`equivalence`), 244
- `debs auth` 命令, 220
- `debs pw` 命令, 275

## `dkms` 动态内核模块支持

- `dkms` 动态内核模块支持, 133

## `dmp-crypt`

- `dmp-crypt` 命令, 263
- `dmp-crypt` 列表, 101

## `Dovecat`

- 认证, 222
- 配置文件, 272

## `dig`

- `dig` 命令, 186
- `dig -g` 命令, 251
- `dig` 文件, 188

## `dmesg`

- `dmesg` 命令, 6
- `dmesg` 内核环缓冲区, 137
- `dmesg -c` 命令, 173
- `dmesg -c` 命令, 232

## `dpk`

- `dpk -i` 命令, 23
- `dpk -P` 命令, 234
- `dpk-reconfigure` 命令, 212
- 别名, 198
- 缓存, 235
- 拷贝, 232
- 查找, 311
- 大文件, 46
- 已挂载, 272
- `DNS` 更新, 209
- 名称显示, 257
- 服务器地址, 103
- 覆盖查看, 106
- 服务器请求, 138

## `DPMS` (显示电源管理)

- `DPMS` (显示电源管理), 72

## `dracut` 命令

- `dracut` 命令, 136
- 漂移文件位置, 90, 249
- 只读变量, 61
- 实例 (`instances`), 250

## 驱动 (`drivers`)

- 文件系统, 144
- 内核, 135
- 使用, 260
- 磁盘, 243
- 移除, 271
- 挂, 144
- 写入, 153

## `/etc/mtlab` 文件

- `/etc/mtlab` 文件
- 系统信息, 46
- `mount` 命令, 155
- 已挂载的系统, 151, 240
- `/etc/network` 目录, 172
- `/etc/nologin` 文件, 111, 210
- `/etc/nwitch.conf` 文件
    - 认证, 211
    - 组组成信息, 273
    - 主机名查找, 250
    - 本地文件, 102
    - 用户, 79
- `/etc/ntp.conf` 文件, 90, 249
- `/etc/passwd` 文件, 209
- `/etc/passwd`
    - `root` 用户, 186
    - 目录列表, 361
    - 用户信息, 76, 238
- `/etc/pki` 目录, 271
- `/etc/posix` 目录, 217
- `/etc/rc.d`
    - 链接, 178
    - 级别, 147
- `/etc/resolv.conf` 文件
    - 调试状态, 172–173
    - `DNS` 服务器, 103
    - 搜索选项, 105
- `/etc/samba` 目录, 201
- `/etc/limits.conf` 文件, 112, 115
- `/etc/sendmail.conf` 文件, 220
- `/etc/services` 文件
    - 端口号到名称转换, 277
    - 端口, 103
- `/etc/shadow`
    - 信息, 81
    - 密码更改日期, 115
- `/etc/skel` 目录, 58, 275
- `/etc/ssh_hosts_hosts`, 115
- `/etc/ssh/sshd_config` 文件, 225, 257
- `/etc/sshd_config` 文件, 116
- `/etc/sudoers` 文件
    - 编辑, 114
    - 邮件目标, 252
    - 组, 116
    - 密码提示, 113
- `/etc/sysconfig/network-scripts` 目录, 173
- `/etc/sysctl.conf` 文件, 137
- `/etc/syslog-ng/syslog-conf` 文件, 94
- `/etc/systemd/` 目录, 142
- `/etc/udev` 目录, 5
- `/etc/udev/hwdbdb.bin` 文件, 265
- `/etc/rules.d` 目录, 135
- `/etc/updatedb.conf` 文件, 44
- `/etc/X11/xorg.conf` 文件, 65
- `/etc/xinerd.d` 目录, 113
- `/etc/yum.conf` 文件
    - 更改, 22
    - 内内核更新, 22
    - 包更改, 235
- `/etc/yum` 目录, 19, 235
- `cuda` 中的事件, 134
- 命令的感叹号 (`!`), 37
- `exclude` 选项, 22, 235
- `exec` 命令, 56
- `ExecStart` 选项, 可执行文件位置, 43
- 执行命令, 54
- `Exim` 配置文件, 222
- 文件存在性, 58, 61
- 过期账户, 76, 115
- 密码, 246–247
- `export` 命令, 18, 237, 244
- `export DISPLAY` 命令, 71
- `NFS` 服务器的导出列表, 203
- `exports -ra` 命令, 204–205
- `exports -ua` 命令, 206
- 导出文件系统, 204–215
- 变量, 18, 237, 244
- `ext2` 文件系统, 44
- `ext3` 文件系统, 44
- `ext4` 文件系统, 264
- 内部文件安全, 214
- `nextlinux --install` 命令, 143

## F

- `fail2ban` 系统配置文件, 227
    - 日志, 230
- `FAT` 文件系统
    - `ESP`, 142
    - 格式化, 156
    - `LINUX` 引导器, 142
- `FCoE` (以太网光纤通道), 164
- `idisk` 命令, 43
- `fg` 命令, 33
- `FHS` (文件层级标准) 源码, 178
- `fi` 结构, 155
- 以太网光纤通道 (`FCOE`), 164
- `file` 命令, 32
- `fileento` 关键字, 217
- 启动镜像, 261
- 拷贝, 77, 245
- 创建, 50
- 解压, 36
- 存在性, 58, 61
- `gpg`, 118
- 组所有权, 43
- 硬链接, 43
- `inode` 号, 50
- 列出, 31
- 移动, 77
- 开放实例, 253
- 打开, 170
- 输出到, 19
- 覆盖, 261
- 写入, 32, 241, 263
- 所有权, 83, 241, 263
- 补丁备份, 181
- 权限, 47
- 移除, 179, 234
- 级别, 144–145
- 查找, 36, 111, 118, 239
- 查找内容, 239
- 大小, 126
- 排序, 37
- 粘位, 45
- 时间戳, 31
- 类型, 32
- 解压缩, 178, 180
- 用户信息, 76

## 防火墙

- `IPv6` 规则, 230
- `LDAP` 流量, 250
- `NTP` 流量, 253
- 端口, 100
- `SMTP` 流量, 94
- `SNMP` 流量, 102

## 第一块磁盘

- 识别, 10

## 函数

- `Bash`, 245
- `in.bash_profile`, 59
- 脚本, 37

## 文件层级标准 (`FHS`) 源码

- 178

![img/84990579543ce21a46ac6dc507fcde32_415_0.png](img/84990579543ce21a46ac6dc507fcde32_415_0.png)

## 文件系统

- 检查, 49
- 写时复制, 152
- 损坏, 50
- 创建, 48, 151
- 驱动程序, 147
- 错误, 155
- `/etc/stab`
- 导出, 204–205
- 格式化, 156
- 信息, 46
- 日志, 44, 156
- 位置, 151
- 已挂载, 151
- 挂载, 45, 49
- 配额, 50
- 只读, 46, 152, 156
- 读写模式, 153
- 共享, 201
- 挂载次数, 245
- 卸载, 240

## 阻塞块

- 闪存磁盘, 移除, 10

## 洪水测试

- 170

## 软盘设备

- 5

## `FontPath` 指令

- 70

## 字体

- 路径, 70
- 存储, 67
- `fonts.scale` 定义, 72

## 循环

- `for VAR` 结构, 53
- 前台进程, 33

## 日期和时间

- 76

## 日志文件

- 198

## 密码

- 272

## 格式化

## 网关

- 默认, 100, 104
- `DHCP`, 22

## 磁盘命令

- 49

## `gdmsetup` 程序

- 69

## 几何 `XFS` 文件系统

- 152

## 手势

- 69

## `get` 命令

- 70, 193

## 别名

- 247

## `gethostname`

- 172

## 关系

- 82

## `Gnome`

- 高对比度主题, 68
- 屏幕键盘, 68
- 屏幕阅读器, 66
- 粘滞键, 69

## `GPG` 密钥对

- 116

## `GRUB` 设备

- 164

## 流量

- 123

## `find` 命令

- 36, 111, 239
- 文件所有权, 83
- `find -gid` 命令, 248
- `find -L` 命令, 241
- `find -type` 命令, 36
- 查找目录, 31
- 开放端口, 116
- 指纹, 83

## `FAT` 文件系统

- 156

## 交换分区

- 45

## 仅转发指令

- 187

## 转发的包

- 128

## 转发应用

- 228

## 邮件

- 219

## 数据数据包

- 229

## 端口

- 116, 229, 277
- `X11`, 116

## `free` 命令

- 334

## 频率选项

- 监控, 65

## `fsck` 命令

- 143
- `fsck -a` 命令, 49
- `fsck -c` 命令, 264
- `fsck -f` 命令, 154
- `fsck -r` 命令, 146, 240, 260
- `fsck -y` 命令, 43
- `fsck` 在 `/etc/stab`, 50

## 菜单

- 71

## 鼠标键

- 69

## 迁移文件

- 118

## 公钥环

- 118

## `gpg-gen` 命令

- 114

## `gpg-v2-迁移文件`

- 18

## 图形命令

- 65

## 大于 (`>`)

## `greeter-show-manual`

- 68

## `greeters`

- 65

## `grep -i` 命令

- 172

## `grep -r` 命令

- 239

## `group: ldap` 选项

- 102

## 组所有权

- 43, 50, 79, 248

## `groupdel` 命令

- 83, 250

## `groupmod` 命令

- 78, 248
- `groupmod -n` 命令, 206

## 组

- 116
- `Apache` 授权, 197
- 删除, 83, 250
- `/etc/sudoers`, 116
- 成员信息, 273
- 组播组, 257
- 密码, 83
- 打印, 94
- 重命名, 78, 248
- 用户, 82
- `Windows` 到 `Linux` 映射, 205

## `GRUB` 引导器

- 1
- 安装, 6, 146
- 镜像, 146
- `MBR`, 143
- 参数, 146
- 根分区, 8
- 单用户模式, 6

## `GRUB_DEFAULT` 选项

- 19

## `GRUB-install` 命令

- 21, 143, 261
- `GRUB-install --boot-directory`, 146, 237

## `GRUB-mkconfig` 命令

- 22, 172

## `GRUB_64_efi` 引导器

- 147

## `LightDM` 中的登录

- 66

## `gunzip` 命令

- 182

## H

## `halt` 命令

- 11

## 硬磁盘

- 91

## 硬链接

- 43

## 硬时钟

- 89

## 硬件数据库

- 265

## 硬件指令

- 209

## 硬件查询

- 66

## `hdparam` 命令

- 161, 169, 259, 264
- `hdparam -C` 命令, 259
- `hdparam -g` 命令, 264

## `head` 命令

- 33
- `head -n` 命令, 34

## 隐藏文件

- 31

## `Hint` 区域

- 189

## `HISTORYSIZE`

- 237, 241

## `hmac-md5` 算法

- 190

## 主目录

- 236
- `chroot` 用户, 186
- 留, 17

## `host -a` 命令

- 187

## `host -C` 命令

- 251

## `host -t ns` 命令

- 272

## `hostname` 举举

- 103
- 名称查找, 250
- 不存在, 106
- 不可到达, 258
- 热插拔设备, 5

## `hostname` 域名

- 102
- `getost` 函数, 172
- 主机名, 256–257
- `Pure FTPD`, 225
- 有效字符, 172
- `host` 阻塞, 244
- 缓存, 115

## I

## `ICMP`

- 阻塞流量, 107
- `iptables` 规则, 229
- `IPv6` 请求, 171
- 包生成, 101
- 端口, 104
- `traceroute` 请求, 172

## `iconv–list` 命令

- 77

## `id` 命令

- 83

## `id_rsa` 文件

- 114

## `IDE` 设备参数

- 161

## `Identifier` 选项

- 772

## `htpasswd` 凭据

- 193

## `.htaccess` 文件

- 重命名, 196–197
- `Require` 指令, 198

## `top` 命令

- 开放文件, 126
- 进程, 125
- `top -d` 命令, 128



## T

- `top -p` 命令, 124

- `htop passwd` 命令, 193

- `htop passwd -B` 命令, 269

- `htop passwd -c` 命令, 197

- HTTP

- 头部, 270

- 端口, 276

- `TraceEnable` 中的状态码, 197

- `http_directory` 指令, 196

- `httpd.conf` 文件, 270

- `hclock` 命令, 899

- `hclock–syslogopt–utc`

- `hclock -w` 命令, 91

## I

### `if` statement

- `iwlist txpower` 命令

- `if statement`

- `fi` 结构, 55

- `Sieve`, 275

- `ifconfig` 命令

- IP 地址, 104

- IPv6 地址, 106

- MAC 地址, 168

- 网络接口, 251

- `ifconfig -a` 命令, 100

- `ifconfig -arp` 命令, 101

- `ifconfig -mtu` 命令, 169

- `ifup -a` 命令, 101

- `ifup --ignore errors` 命令, 252

- `IgnoreMissingOption`

### `images`

- 创建, 240

- GRUB, 146

- 位置, 237

- 分区, 32

- 写入, 236, 237

- IMAP 端口, 222

- IMAPS 端口, 226

- `slcap` 数据库, 213

- 有效, 194

- INET 族, 168

- `inet_listener_directory`, 226

- `inetPerson`, 168

- 信息消息, 89

- 严重级别, 89

- 信息, 111

- 初始化, 111

- 进程, 54

- `inramfs`, 127

- `init` 命令, 58

- inode 号, 50

- inodes 使用, 43

### `INPUT` 链

- 阻塞流量, 229

- host 连接, 229

- ICMP 流量, 226

- 列表, 226

- 保存, 225

- `iptables-save` 命令, 225

- `iptraf` 工具, 123, 125

- IPv6 地址, 227

- 启用, 229

- 防火墙规则, 230

- ICMP 请求, 171

- 信息, 171

- 主机, 101

- `ping` 命令, 105

- 路由追踪, 173

- `traceroute` 命令, 102

- `ip` 命令, 118

- `ip -6` 命令, 172

- `ip - monitor` 命令, 102

- `ip -o` 命令, 169

- `ip -r` 命令, 257

- `ip route` 更改, 106

- `ip route默认`, 104

- `ip route flush cache`, 106

- `ip6tables` 命令, 230

- `ip6tables-save` 命令, 227

## J

- 监狱锁配置 - 链接 379

- 监狱锁配置, 230 个任务

- `cron。查看删除的 cron 任务`, 79

- 执行, 81

- 信息, 计划, 78

- `jobs` 命令, 36

- 合并, 58

### `journalctl`

- 磁盘空间, 90

- 日志文件, 284

- `journalctl -f` 命令, 92

- `journalctl -conf` 文件, 93

- 显示, 173

- 文件系统, 44, 156

- systemd, 249

- 源目录, 132

- 符号, 137

- 解压, 132

- 更新, 22

- 升级, 132

- 版本, 22, 135, 180

### LDAP

- 数据库, 213

- 防火墙, 250

- 邮件属性, 274

- 服务器 URIs, 214

### 内核环形缓冲区

- 消息, 137

- 查看, 6

### 密钥对

- GnuPG, 116

- ssh, 223

### 键盘模型

- 配置, 67

- 键盘

### LDAP 数据交换格式 (LDIF)

- 类型, 274

- 创建, 212

- 数据库, 210

- `ldapsearch`, 213

- SSL 上的 LDAP, 106, 214

- `ldap-uri` 选项, 214

- `ldapadd` 命令, 273

- `ldapadd -f` 命令, 210

- `ldapmodify -n` 命令, 214

- `ldapsearch`, 214

- `ldapsearch -L` 命令, 213

- `ldconfig` 命令, 116

- `ldconfig -C` 命令, 234

- `ldconfig -p` 命令, 235

- 延迟和重复率, 246

- 屏幕上, 68, 70

### 键

- 算法, 185

- 认证, 117, 228

- OpenSSH, 236

- PBKDF2, 154

- RSA, 117

- 尺寸, 268

- SSH, 227

- SSL, 193

- TLS 配置, 217

- `kill` 命令, 185

- `kill -9` 命令, 34

- `kill -UP` 命令, 335

- `killall` 命令, 233

- 杀死进程, 37-232, 234

- `ldd` 命令, 205

- LDIF。查看 LDAP 数据交换格式 (LDIF)

- 路径前的斜杠移除, 177

- DHCP 中的租约, 211–213

- STDIN 消息的小于号 (`<`), 250

- `/lib/systemd/system` 文件夹, 7

### 库

- LightDM

## K

- `kbdb` 命令, 246

- 邮件箱的保留操作, 218

- Kerberos 身份认证, 201

- 内核功能, 88

### 内核

- 盲显示器, 67

- `dkms`, 133

- 文档, 135

- 驱动程序, 260

- 最终配置位置, 133

- 开启, 137

- 已加载模块, 8

- 消息, 88

- 最小配置, 265

- 选项, 9

- 参数, 164

- 打印信息, 30

- SAN 模块, 44

- 源压缩, 174

## L

- `htop` 的 1 键, 126

- `Lang+C` 选项, 80

- 大文件, 目录, 46

- 上一个命令, 117

- `last -f` 命令, 112

- 服务器的布局选项, 72

- `LC_ALL` 变量, 80

- `LC_MONETARY` 变量, 83

- `LC_TIME` 变量, 58

- 自动登录, 70–71

- 配置文件, 71, 246

- 客客登录, 66

- 恢复到, 70

- `lightdm.conf` 文件, 68

- `limits.conf` 文件, 274

- 前行号, 36

- 线性加速, 67

- 行，编号, 237

- `/etc/rc.d/*`, 118

- 文件, 43

- 共享库, 16

- 无线设备, 168

### `list-unit-files` 命令

- `list-unit-files` 命令, 234

- `listen-ipv6` 指令, 229

- `listen-on` 指令, 186

### 监听端口和套字

- `dovecot`, 221

- 计时, 258

- `in -s` 命令, 44

- `in -sf` 命令, 81

### 负载平均

- 确定, 34

- 信息, 239

- 性能, 128

- `uptime` 命令, 126

### 已加载模块

- 显示, 133, 136–137

- 列出, 8

### 加载服务

- 驱动程序, 124

- 模块, 5

- `LoadModule` 行, 195

- `local_enable` 指令, 230

- `local-reality`, 94

- 信息本地组, 102

- 本地时间设备, 232

- 本地时区, 76

- `local -mc` 命令, 248

- 本地翻译，跳过, 80

- 本地变量，重新配置, 80

- IPv6 中的 `localhost`, 101

- 局部性，货币相关, 88

- `locate` 命令, 47

- 锁定命令, 117

- 锁定日志, 80

- 显示锁, 204

### 日志文件

- 压缩, 94

- 配置文件, 91

- 自定义, 94

- 显示, 88, 92

- 限制, 228

- `fail2ban`, 230

- 格式, 198

- 邮件选项, 90

- 消息, 91

- 减号, 95

- 监控, 36

- 解析, 248

- 轮, 93

- Samba, 204

- 服务器请求, 196

- 服务时间, 197

- 共享, 206

- 尺寸, 93

- syslog, 88

- 归零, 156

- `--prefix` 选项, 277

- `LOG` 目标, 277

- `LogFormat` 指令, 198

- 登录用户, 218, 253

- `logger` 命令, 95

### 逻辑数字 (UNs)

- 160

### 逻辑卷 (LVM)

- 缓存, 256, 263

- 逻辑值, 21, 163

- 分区, 20–21

- 物理卷, 159

- 卷搜索, 23

#### 逻辑变量

- 可用, 164

- 创建, 21, 163

- 显示, 162

- 快照, 164

### 登录环境

- 118

- 窗口选项, 68

### 登录

- 自动, 70–71

- 当前, 112, 123

- 客户, 66

- 交互式, 78

- 上一个命令, 117

- 限制, 212

- 锁定, 179–180

- `root` 用户, 225

- 同时, 115

### `logouts` 命令

- 执行, 54

- 空闲, 60

- `logpath` 指令, 230

- `logrotate` 配置文件, 94

- `logrotate -m` 命令, 249

- `logprcm` 命令, 214

- 消息捕获, 250

- 打印队列, 91

- `lpstat -W` 命令, 93

- `ls` 命令, 9

- `ls la` 命令, 7

- `lsblk` 命令, 236

- `lsmod` 命令, 12

- 已加载模块, 133, 136

- `lsmod --depends`, 8

- `lsof` 命令, 111, 126

- `lsof -i` 命令, 127, 228

- `lsof -u` 命令, 170

- `lspci` 命令, 164

- `lspci -k` 命令, 260

- `lspci -t` 命令, 12

- PCI 设备, 135, 233

- `lvchange -a` 命令, 381

- `lvcreate` 命令, 21, 163

- `lvcreate` 快照, 164

- `lvm.conf` 文件, 164

- `lvmdiskscan` 命令, 23

### `m4 sendmail.mc` 文件

- `mount -a` 命令, 381

## M

- `m4 sendmail.mc` 文件, 220

- MAC 地址, 169

- 放大功能, 68

- 主机, 209

- LDAP 中的邮件属性, 274

- 邮件备份, 264

- 日志文件的邮件选项, 90

- 邮件队列, 90, 93

- Postfix 服务器, 90, 274, 275

- 邮件打印信息, 91

- `mail -s` 命令, 245

- 邮件分区, 16

- 邮件查询, 217–219

- 邮件发送器, 249

- `mailq` 命令, 90, 218

- `mailq` 参数, 221

- `mailto sente`, 252

- `make offend` 命令, 132

- `make allconf`, 133, 178

- `deb-pkg`, 134

- 额外文件, 178

- 安装, 181

- `makefig`, 132

- `modules_install`, 136

### `Makefile`

- 依赖关系, 178

- `makemap` 命令, 94

- `man` 命令, 30

- `man 2` 命令, 35

- 映射端口, 206

### 主引导记录 (MBRs)

- 引导加载程序, 236

- 区域，测试, 190

- `max-lease-time` 指令, 221

- 最大传输单元 (MTU), 169

- `maxins` 选项, 115

### MBRs (主引导记录)

- 引导加载程序, 236

- 描述, 145

- `mdam--assemble` 命令, 256

- `mdam --create` 命令, 162

- `mdam --delay` 命令, 256

- `mdam --monitor` 命令, 162

- `/media` 挂载点, 46

- 信息, 260

- 进程, 124

- 套接字, 169

- 使用, 32, 128

- 用户限制, 113

- 显卡, 71

- `menu.list` 文件, 19

- `menufig` 目标, 132

- GOK 菜单选项, 71

- `message_size_limit` 参数, 275

- 消息广播, 179

- 删除, 92

- DHCP, 211

- 显示, 179, 275

- 内核, 88

- 内核环形缓冲区, 137

- 日志文件, 191

- 登录, 179–180

- `netlink`, 102

- 发送, 8

- `sendmail`, 92

- syslog 级别, 89

- `wall`, 232

- `gpg` 中的迁移文件, 118

- 日志文件的减号, 95

- `mkdir -p` 命令, 32

- `mk2fs -c` 命令, 241

- `mk2fs-s` 命令, 151

- `mkfontscale` 命令, 72

- `mkfs.btrs` 命令, 48

- `mkinitrd` 命令, 132

- `mkisofs` 命令, 151

- `mkisofs -b` 命令, 261

- `mkswap` 命令, 45, 151

- `mod_auth_basic` 模块, 193

- `mod_authn_file` 模块, 193

- `mod_authz_host_模块`, 196

- 修改文件, 36

- 修改类型, 274

- `modinfo`, 271

- 模块依赖关系, 135

- NVM 模块, 261

- `modinfo -p` 命令, 260

### `modprobe` 命令

- 配置文件, 232

- 描述, 5

- 模块依赖关系, 8, 134, 137

- `modprobe -r` 命令, 136

- `modprobe --show-depends` 命令, 137

- `xorg.conf` 中的模块部分, 66

### 模块

- 黑列表信息, 136

- 依赖关系, 8, 134–137

- 安装, 135

- 已加载, 136–137

- 加载, 5

- 选项的, 260

- PAM。查看 Pguide

### 身份认证 (PAMs)

- 移除, 12, 16

### `modules_install` 选项 make target

- monitoring

- 警报, 123

- 通信, 233

## N

### 非交换交换分区

- 非交换交换分区, 22

- 分区

### `NOPASSWD` 选项

- 113

### `--norc` 选项

- 59

- 通知设备, 268

- `top` 命令, 127

### NTP

- 客户端, 88

- 与防火墙的通信, 253

#### NTP 服务器

- 容量, 249

- 交互式模式, 90

- `tpt-g` 命令, 93

- `tpdate` 命令, 89

- `tpdate -o` 命令, 249

- `tptq` 命令, 89

### `head` 和 `tail` 的行数

- 34

- 打印, 30–31

- 编号: (`#`) 用于注释, 117

- 编号列表, 237

- 代码显示, 79

### NVMe

- PCI 子系统中的设备, 164

- 驱动程序, 161

- 驱动器, 160

- `vme` 模块, 161

### `NXDDOMAIN`

- 106

- 打开文件, 170

### OpenLDAP

- 配置文件, 213

- 数据库, 210

### OpenSSH

- 允许的用户, 276

- 配置文件, 225

- 空分区, 227

- 基于密钥认证, 230

- 端口转发, 229

- 端口, 226

- `root` 用户登录, 225

- SSH 版本, 228

- `openssl ctl` 命令, 193

- `openssl req` 命令, 195

### OpenVPN

- DHCP, 230

- 端口, 227

- `push` 指令, 226

- 操作系统, 默认 19, 22

### `domain-search` 选项

- 210

### `/etc/resolv.conf` 中的 `options debug` 行

- 172–173

### `Options-Indexes` 指令

- 195

## P

### `-p` 选项

- 59

### 包

- 缓存搜索, 21

- 缓存更新, 20

- 依赖, 18, 235

- 从中删除文件, 234

- 信息, 22

- 安装, 17, 21, 23



## 包

- 缓存搜索, 21
- 缓存更新, 20
- 依赖, 18, 235
- 从中删除文件, 234
- 信息, 22
- 安装, 17, 21, 23
- 仓库, 20, 234
- 搜索, 19
- 基于热的接口工具, 21
- 升级, 235

## 控制

- 控制, 277
- 转发的, 128
- 转发, 229
- 日志文件, 213
- 页面未找到错误, 196
- 分页, 238

## Sam. 参见可插式认证模块 (PAMs)

- `pam_cracklib.so` 模块, 212
- `pam_limits.so` 模块, 214
- `pam_listfiles.so` 模块, 214
- `pam_nlogin.so` 模块, 210
- `pam_ss.so` 模块, 214
- `pam_unix.so` 模块, 211

## PARANOID 通配符

- `PARANOID` 通配符, 173

## 括号

- 纯文本中的八进制表示, 238
- `od` 命令, 238

## 非屏幕键盘

- 描述, 70
- `GNOME`, 6

## $1 命令行参数

- `$1` 命令行参数, 55

## 文件操作

- 显示打开的文件, 126
- 搜索打开的实例, 253

## 开放端口

- 连接, 127
- 显示, 111
- 查找, 116
- 扫描, 121

## ORDER BY 子句

- `SELECT` 语句, 57

## 内存溢出情况

- 内存溢出情况, 33

## 输出

- 到文件, 19
- 重定向, 30
- 输出到 `stdout`, 32

## 网络配置

- 覆盖 `DNS` 查找, 106
- 覆盖文件, 144, 261
- 覆盖文件时的提示, 32

## Orca 船运

- 修改, 47
- 文件, 83, 241, 263
- 组, 43

![](img/84990579543ce21a46ac6dc507fcde32_422_0.png)

## 透传代理 - Postfix

- 非交换, 22
- `RAID` 阵列, 159, 163, 256
- 重命名, 49
- 交换, 151
- `UUIDs`, 48, 152
- 透传代理, 198
- `passwd -s` 命令, 81
- `passwd -d file ldap` 行, 211
- `passwd -u` 命令, 252

## 基于密码的性能

- `CPU`, 125
- 平均负载, 128
- 性能图表工具, 124

## 权限

- `chmod`, 57
- 文件, 47
- 组, 48
- `POSIX` 格式, 44
- `SUID` 位, 56
- 符号链接, 47

## 其他指令与服务

- `PermEmptyPasswords`
- `POP3` 服务器, 189
- 端口到名称翻译, 277
- `OpenSSH` 中的 `Port` 选项, 226
- `portmap` 服务，访问, 203

## 端口

- 添加, 103
- `CUPS`, 95
- `DHCP`, 210, 212
- `Dovecot`, 221–222
- 防火墙, 100
- 转发, 116, 229, 277

## 派生函数

- 派生函数 2 (`PBKDF2`), 154

## 密码

- 修改日期, 115
- 修改, 272
- `Dovecot`, 275
- 空，加密, 269
- `/etc/shadow`, 81
- 过期, 246–247
- 格式, 272
- 组, 83
- `PAM` 模块, 211
- 提示, 113
- `Samba`, 202, 204
- 强度, 212
- `tar`, 258
- `patch -b` 命令, 181, 264
- `patch -i` 命令, 259
- `patch -pl` 命令, 177

## 路径

- 添加到, 245
- 邮件, 221
- 字体, 70
- 前导斜杠, 177
- `LUNs`, 160
- 删除, 44

## PCI 设备

- 驱动程序, 233
- `NVMe`, 164

## 包与模块

- `pdns-server` 包, 190

## PEM 文件

- 指令, 227

## 持久化

- `PermRootLogin` 指令, 225
- 持久化主从 `SCSI` 设备, 256

## 进程与工具

- `pgrep` 命令, 33

## PHP

- `PHP` 配置文件, 195
- `php.ini` 文件, 195
- `php7` 模块, 195

## ping 命令

- 延迟, 259
- 端口, 263
- `-c` 命令, 105
- `-f` 命令, 170
- `-i` 命令, 201
- `-m` 命令, 258
- `-n` 命令, 251
- `-r` 命令, 263
- `-6` 命令, 101

## 管道

- 管道, 59

## 纯文本文件

- 八进制表示, 238
- `HTTP`, 276
- `ICMP`, 104
- `LDAP`, 250
- `LDAP over SSL`, 214
- `nmb` 守护进程, 271
- 流量, 253

## 其他条目

- 打开的, 127
- `OpenSSH`, 226
- `OpenVPN`, 227
- 显示, 111
- 查找, 116
- 扫描, 121
- 密码, 115
- 密码修改, 272
- 密码 `Dovecot`, 275
- 密码空加密, 269
- 密码 `/etc/shadow`, 81
- 密码过期, 246–247
- 密码格式, 272
- 密码组, 83
- 密码 `PAM` 模块, 211
- 密码提示, 113
- 密码 `Samba`, 202, 204
- 密码强度, 212
- 密码 `tar`, 258
- 密码 `patch -b` 命令, 181, 264
- 密码 `patch -i` 命令, 259
- 密码 `patch -pl` 命令, 177

## 路由表

- 路由表，绕过，263

## RPC

- `rpcbind` 操作，203

## rcinfo 命令

- `rcinfo -m` 命令, 203
- `rcinfo -p` 命令, 206

## rm 命令

- `rm -ivh` 命令, 18

## RPM 包

- `RPM` 包
- 下载，18
- `rpm -q kernel` 命令, 22

## 其他 rm 命令

- `rm -Uvh` 命令, 235
- `rm -V` 命令, 19
- `rm2cpio` 输出, 17

## RSA

- `RSA` 密钥, 117

## rsync 命令

- `rsync -a` 命令, 177
- `rsync -b` 命令, 258
- `rsync -delete` 命令, 179
- `rsync -e` 命令, 182
- `rsync -go` 命令, 263
- `rsync -modify-command` 命令, 181
- `rsync-size-only` 命令, 181

## 服务

- `rsyslog` 端口, 93

## iptables

- `iptables`。参见 `iptables` 规则
- `dev`, 135

## 运行级别

- 单用户模式下的运行级别 1, 6
- `runlevel` 命令, 7

### 运行级别详解

- 默认值，147
- 显示，7, 10
- `/etc/inittab`, 142
- `/etc/rc`, 147
- 文件，144-153
- 单用户模式，118
- 切换，146

## 进程与任务

- 运行进程，12, 232
- 运行任务，显示，36

## 网络共享

- 端口，271-272
- 读写共享，205
- 安全级别，272
- 安全参数，202
- 共享挂载，202
- 从 `Windows` 到 `Linux`/用户名，202
- `samba-tool` 命令，204

## 存储与硬件

- `SANS`（存储区域网络），44

## sar 命令

- `sar` 命令
- 平均利用率
- 最后一次重启，128
- 自上次重启以来收集的统计数据，127
- `sar -um` 命令, 125

## SATA

- `SATA`（串行 `ATA`）设备



# S

## 标识符
*   5
*   161

## 参数
*   161

## 保存
*   保存 `vi` 编辑的文件，34

## 无线网络
*   扫描，169

## 计划任务
*   显示，78

## 调度
*   命令，77, 80
*   任务，77

## `screen` 命令
*   34

## 屏幕阅读器
*   激活，69
*   `Gnome`, 66
*   `/etc/X11/xorg.conf` 中的 `Screen` 部分，65
*   `GUI` 应用程序的屏幕，246

## 脚本
*   命令，57
*   `/etc/network`, 172
*   执行，56
*   查找，80
*   热插拔设备，5
*   服务，144
*   `SysVinit`, 6
*   `update-rc.d` 工具，144

## SCSI 设备
*   `ID`，160
*   持久性名称，256
*   磁带，179
*   值，164
*   `scsi_id` 命令, 160
*   `sdmp` 命令, 164

## 搜索选项
*   `/etc/resolv.conf`, 105
*   `yum`, 21

## 搜索
*   文件内容，239
*   文件，366, 118, 239
*   开放实例，253
*   软件包缓存，21
*   包信息，22

## 页面
*   19

## `vi` 差异器
*   37

## 卷
*   23

## `SeatDefaults` 部分
*   68

## 日期和时间的秒格式
*   77

## 扇区大小
*   264

## Secure Shell (SSL)
*   配置，194
*   基于名称的虚拟主机，194
*   端口，193, 196

## 安全
*   `Active Directory`, 272
*   `Samba` 参数，202
*   `s deg` 命令, 30
*   `SELECT * FROM` 语句，54
*   `SELECT GROUP BY` 语句，60
*   `SELECT ORDER BY` 语句, 57

## 自主监控、分析和报告技术 (SMART)
*   兼容硬盘，153
*   监控，154
*   发送，245
*   消息，8

## `sendmail`
*   访问数据库更改，94
*   配置文件，220
*   统计数据，95
*   `sendmail -bp` 命令, 91
*   `sendmail -q` 命令, 92

## Samba
*   配置文件，201, 204
*   凭据，272
*   日志文件，204
*   `NetBIOS` 名称服务请求，201
*   密码，204, 252

## seq command — sockets
*   `seq` 命令, 56

## 串行 ATA (SATA) 设备
*   标识符，5
*   参数，161

## 服务器生成的文档版本
*   269

## `showmount -e` 命令
*   203

## 启动关闭
*   11

## 系统
*   234

## `slapd_db_recover` 命令
*   210

## `slapindex` 命令
*   213

## `/` (斜杠) 文件系统
*   227

## 从用服务器
*   268

## 进程的睡眠模式
*   127

## SMART (自我监控、分析和报告
*   `SNI` 技术，194
*   `ServerName` 指令, 182

## 服务器
*   创建，104
*   域名，102
*   布局选项，72
*   日志文件请求，196
*   `NTP` 客户端地址，88
*   特定站点数据，45
*   状态，197
*   `SysVInit` 脚本，6

## Sieve
*   条件，221
*   删除操作，220
*   域名，222
*   电子邮件地址，217
*   转发消息，219
*   `if` 语句，274
*   邮箱箱，245

## Signature
*   指令，194
*   令牌，269

## 服务
*   禁用，117
*   脚本，144
*   启动和运行，118
*   启动时停止，115

## 单用户模式
*   运行级别，6, 118

## 特定站点数据服务器
*   45

## `smart` 守护进程
*   135

## 兼容硬盘
*   153

## 监控
*   154

## `smbclient -L` 命令
*   206

## `smbclient -R` 命令
*   272

## `smbcontrol force-election`
*   271

## `smbbd reload` 命令
*   201

## `SetHandler`
*   198

## 共享文件系统
*   201
*   列出，272
*   `Samba`，202
*   共享，206

## `shelbang` 行
*   34

## `shell` 提示符
*   54

## 尺寸
*   178

## 密钥
*   268
*   已打开的文件，126
*   恢复块，154
*   扇区，264
*   交换空间，156
*   窗口，69
*   `zimage` 镜像，132

## `slapd -j` 命令
*   213

## `slapd-l` 命令
*   274

## `slapd-config` 文件
*   212
*   213
*   数据集，213
*   调试级别，211
*   连接性测试，226
*   会话，221
*   防火墙，94
*   快照，156
*   长度，262
*   逻辑值，164

## SNI (服务器名称索引)
*   技术，194
*   `SNMP` 流量和防火墙，202

## SOA (区域起始记录)
*   显示，105, 251

## 套接字
*   130, 170
*   内存，169
*   进程 ID，171
*   队列，124–125
*   计时，258
*   粘滞，66

## `top` 的 `Shift+F` 键
*   124

## `shim.efi` 文件
*   144, 177

## `mount -a` 命令
*   272

# software updates - syslog

## 软件更新
*   17

## `sort` 命令
*   33

## 数据库数据
*   57

## 文件
*   37

## 压缩
*   174

## 内核
*   132

## 位置
*   178

## 源命令
*   54

## 等效性
*   244
*   `Orca`，254

## `DNS` 查询
*   106

## SQL 语句
*   `GROUP BY` 子句，60
*   内部连接，58
*   `SELECT * FROM`, 54
*   `UPDATE`, 58, 244
*   `WHERE` 关键字，244
*   方括号 `]` 在 `while` 循环中，60

## Squid 访问列表
*   194

## `ACL`
*   196
*   端口，270
*   目录，45

## `ssh` 命令
*   169

## `ssh -p` 命令
*   258

## `SSH` 连接
*   171
*   密钥指纹，252
*   密钥对，225
*   私钥，114
*   公钥，230
*   远程服务器，114
*   同步，182
*   版本，228
*   `X` 会话，70

## `ssh-add` 命令
*   114

## `ssh-agent`
*   14

## `ssh-copy-id` 命令
*   230

## `ssh-keygen` 命令
*   112, 277

## `ssh -i` 命令
*   117, 225

## `ssh -L` 命令
*   116, 251

## `ssh`
*   316

## Secure Shell (SSL)
*   `SSLCertificate` 指令，194
*   `SSLKey` 指令,270
*   `SSLCipherSuite` 指令,270
*   `SSLEngine` 选项，194

## `sshd.conf` 文件
*   214, 273

## `SSSD` 集成
*   69

## start of authority (SOA) 记录
*   268
*   描述，105, 251

## `StartServers` 指令
*   198, 214

## 启动脚本
*   `SysVinit`, 6
*   `startx` 命令, 69

## `STDIN`
*   32

## `STDOUT`
*   45

## `stty` 输出
*   115

## sticky keys
*   66

## storage area network (SAN)
*   44

## `su` 命令
*   114

## `su -c`
*   212

## `su -u` 命令
*   117

## `su -s` 命令
*   114

## subnets
*   209

## subnet masks
*   101

## swap space
*   156

## swap partitions
*   144, 155

## SUID bit
*   56

## volumes
*   23
*   volumes in `btrfs`, 155

# TTL 值 – UUID

## TTL 值
*   更改, 190
*   时间单位, 188

## `tune2fs` 命令
*   44
*   `tune2fs -c` 命令, 49, 151
*   `tune2fs -E` 命令, 16
*   `tune2fs - e` command, 155
*   `tune2fs - h` command, 45
*   `tune2fs - j` command, 156

## TXT 资源记录
*   188

## `type` 命令
*   47

## `TZ` 环境变量
*   79

## `tzconfig` 命令
*   74

## `tzselect` 命令
*   79

## 卸载系统
*   240

## 未使用的数据块
*   160

## 解压
*   内核, 132
*   压缩文件, 33

## `update-grub` 命令
*   16, 237

## `update-rc.d` 命令
*   118, 146

## `UPDATE` 语句
*   245

## `UPDATE SET` 语句
*   58

## `updatedb` 命令
*   47

## 更新
*   配置文件, 16
*   动态 `DNS`, 209
*   硬件数据库索引, 261
*   内核, 226
*   包缓存, 20
*   共享库链接和缓存, 16

## `usermod` 命令
*   `usermod -aG` 命令, 94
*   `usermod -c` 命令, 83
*   `usermod -e` 命令, 113
*   `usermod -L` 命令, 80, 117
*   用户名映射命令, 201

## 用户名
*   更改, 251
*   显示, 68
*   格式, 272
*   关于信息, 81
*   列出, 31
*   `Samba`, 202
*   `Windows` 到 `Linux` 翻译, 201

# U

## Ubuntu 系统可访问性
*   信息, 246

## udev
*   配置文件, 5
*   硬件数据库, 265
*   规则, 135
*   服务管理, 233

## 命令
*   `devadm hw -u` 命令, 261
*   `uudev monitor` 命令, 134

## UDP 扫描
*   253

## `$UDPServerRun` 选项
*   93

## 路由 UG 标记
*   107

## 显示
*   83
*   `GID` 关系, 82
*   列表, 81

## `ulimit -a` 命令
*   113

## `umask` 命令
*   47
*   `umask -s` 命令, 44

## `umount` 命令
*   10
*   `umount -f` 命令, 240
*   `umount -r` 命令, 46
*   `umount -t` 命令, 153
*   `umannal` 命令, 57

## `uname` 命令
*   `uname -a` 命令, 30, 180
*   `uname -r` 命令, 135

## 解压文件
*   178

## `uniq -i` 命令
*   238

## 通用访问部分
*   246

## 解锁账户
*   252

## 升级
*   内核, 132
*   软件包, 235
*   匿名上传, 226

## `uptime` 命令
*   描述, 34
*   负载负载, 239
*   负载负载输出, 126

## LDAP 服务器的 URIs
*   214

## USB 设备
*   连接点, 11
*   连接, 12
*   热插设备, 10
*   关于信息, 134
*   列出, 5
*   挂载, 41
*   存储位置, 8

## 用户输入
*   56

## 用户配额
*   检查, 46
*   启用, 48

## `useradd` 命令
*   `useradd -r` 命令, 246-247
*   `useradd -G` 命令, 82
*   `useradd -m` 命令, 80
*   `useradd -r` 命令, 82

## `userdel`
*   248
*   `userdel -r` 命令, 77

## 用户
*   `cron` 任务, 76, 78
*   81–82, 247
*   删除, 70, 206
*   磁盘占用, 123
*   组, 82
*   家目录, 236
*   关于信息, 76, 79, 113, 238
*   列表, 79
*   已登录的, 218
*   `OpenSSH`, 276
*   进程限制, 112
*   重命名, 83
*   `XServer`, 246

## `#!/usr/bin/env bash`
*   设置, 54

## 目录与文件
*   `usr/` 目录, 177
*   `usr/lib/systemd/user` 目录, 144
*   `usr/share/fonts` 目录, 67
*   `usr/share/zoneinfo` 文件, 76, 248
*   `usr/src` 目录, 178
*   `usr/src/linux/config` 文件, 133
*   `usr/src/linux/` 目录, 135

## `usrequota` 选项
*   48

## UTC 日期
*   249

## UTF-8 编码
*   78

## UUID
*   显示, 152
*   列出, 261
*   分区, 48, 265

# V

## 邮件假期回复 - xfsrestore-b 命令
*   邮件假期回复, 219

## 目录与文件
*   `var` 目录, 264
*   `var/cache` 目录, 236
*   `var/lib/ldap` 目录, 210
*   `var/lib/btp/rt` 文件, 249
*   `var/log/dmesg`, 210
*   `var/log/journal` 目录, 249
*   `var/mail/err` 文件, 220
*   `var/log/wtmp` 日文件, 117
*   `var/named` 目录, 186
*   `var/spool/cron/crabs`, 78
*   `var/spool/postfix` 目录, 217

## Shell 变量
*   更改影响, 137
*   大括号, 61
*   显示, 56
*   相等性测试, 244
*   导出, 244
*   只读, 61
*   用户输入, 56
*   `rpm` 中的输出, 18
*   验证配置文件, 187, 193
*   文件系统, 153

## 版本
*   `Apache`, 194
*   服务器生成的的文档, 269
*   `SSH`, 228
*   无版本, 190

## 备用命令
*   57
*   监控器, 67
*   刷新选项, 67

## `vgcreate` 命令
*   161

## `vgscan` 命令
*   163–164, 256

## `vi` 编辑器
*   插入模式, 35
*   在其中移动行, 239
*   使用, 37
*   `wi` 命令, 33

## 显卡 RAM
*   71

## 视频模式
*   更改, 68
*   基于名称, 94
*   虚拟主机, 195
*   虚拟服务器, 193
*   视觉障碍, 72

## `visudo` 命令
*   114

## 等待时间
*   125

## 睡眠模式
*   127

## 卷
*   159
*   `RAID` 数组, 161
*   身份认证, 230

## `vsfpd conf` 文件
*   225

## 启用 IPv6
*   229

# W

## `w` 命令
*   112, 123

## wa 统计

## `wall` 命令
*   8, 179
*   `wall -g` 命令, 232

## `wc` 命令
*   30

## 欢迎部分
*   65

## Where
*   SQL 中的 `WHERE`, 244

## `whichis` 命令
*   43

## `while` 循环运算符
*   58
*   方括号, 60

## 补丁文件空白
*   259

## `whois` 命令
*   253

## 宽格式
*   127

## 正则表达式
*   话信息, 69
*   `Windows-Linux` 组, 205
*   `Windows` 到 `Linux` 用户名翻译, 201

## 无线设备
*   168
*   扫描无线网络, 169

## 世界标识符 (WWID)
*   256

## 世界通用名称 (WWN)
*   162

# X

## X 程序
*   显示, 71
*   连接到 `X` 服务器, 70
*   启动, 69
*   `X` 会话，`ssh` 连接, 70
*   窗口信息, 69, 244
*   `X11` 转发, 116, 228

## 配置选项
*   `X11Forward` 选项, 116
*   `XFree86-config`, 66
*   `XkbModel` 选项, 67

## 扫描与命令
*   `Xmas` 扫描, 262
*   `xhost` 命令 –递归 DNS类型, 246
*   `xhost +wa` 命令, 70
*   `xorg.conf` 文件空白模式, 69
*   字体, 70
*   模块, 66
*   视频模式, 68

## `xrandr` 命令
*   `xrandr -s` 命令, 66

## `xwininfo` 命令
*   69, 246

## `xz` 命令
*   内核源码, 177
*   `lzma` 文件, 36
*   与 `tar` 使用, 181
*   `xz -d` 命令, 132
*   `xz --decompress -stdout` 命令, 181

## `yum` 命令
*   `nyum` 命令, 17–18
*   `yum install -y` 命令, 235
*   `yum` 系统缓存, 21, 26
*   存储库, 19
*   `yndownloader` 命令依赖, 23
*   `RPM` 软件包, 18
