

## 附录：术语表

- **单播** 指发送给单台计算机的 TCP/IP 通信。
- **不间断电源 (UPS)** 一种包含电池存储的设备，用于在停电时为计算机供电。
- **通用访问实用程序** Fedora 20 中用于配置辅助技术的图形实用程序。
- **UNIX** 第一个真正的多任务、多用户操作系统，由 Ken Thompson 和 Dennis Ritchie 开发，Linux 即源于此。
- **UNIX SysV** 一种 UNIX 标准，用于提供 Linux 系统上系统初始化进程的结构。
- **update-rc.d 命令** 一条命令，可用于在 Ubuntu Linux 系统上按运行级别配置 UNIX SysV 守护进程的启动。
- **upstart** 用于现代 Linux 发行版上的 UNIX SysV 系统初始化进程的最新版本。
- **用户** 使用计算机的人。
- **用户** 当用于特定文件或目录的模式时，指该文件或目录的所有者。
- **用户账户** 存储在系统数据库（`/etc/passwd` 和 `/etc/shadow`）中的用户信息，可用于登录系统并获取系统资源的访问权限。
- **用户数据报协议/互联网协议 (UDP/IP)** TCP/IP 的一种速度更快但不可靠的版本。
- **用户标识符 (UID)** 分配给每个用户账户的唯一数字。
- **用户界面** 用户看到并用于与操作系统和应用程序交互的界面。
- **用户进程** 由用户启动并在终端上运行的进程。
- **useradd 命令** 用于向系统添加用户账户的命令。
- **用户定义变量** 由用户创建且不被系统使用的变量。这些变量通常导出到子 shell。
- **userdel 命令** 用于从系统中删除用户账户的命令。
- **usermod 命令** 用于修改系统中用户账户属性的命令。
- **变量** 用于存储信息的内存区域。变量在登录后首次创建 shell 时由环境文件中的条目创建，并在注销时销毁 shell 时被销毁。
- **变量标识符** 变量的名称。
- **Very Secure FTP 守护进程 (vsftpd)** 现代 Linux 发行版中使用的默认 FTP 服务器程序。
- **VFAT (Virtual File Allocation Table，虚拟文件分配表)** 一种非日志记录文件系统，可能用于 Linux。
- **vgcreate 命令** 用于创建 LVM VG 的命令。
- **vgdisplay 命令** 用于查看 LVM VG 的命令。
- **vgextend 命令** 用于向 LVM VG 添加额外物理卷的命令。
- **vgscan 命令** 用于查看 LVM VG 的命令。
- **vi 编辑器** 大多数 UNIX 和 Linux 系统上可用的强大命令行文本编辑器。
- **虚拟机** 在虚拟化软件中运行的操作系统。
- **虚拟机宿主** 运行虚拟化软件的操作系统。
- **虚拟内存** 位于硬盘或 SSD 上的区域（交换分区），如果物理内存 (RAM) 使用过量，可用来存储通常驻留在物理内存中的信息。
- **虚拟网络计算 (VNC)** 一种跨平台技术，允许用户通过网络连接到图形桌面。
- **虚拟化软件** 一组可用于在现有操作系统中并发运行操作系统的程序。
- **vmstat 命令** 用于显示内存、CPU 和交换统计信息的命令。
- **VNC 查看器** 用于连接到 VNC 服务器并获取图形桌面的程序。
- **vncpasswd 命令** 用于为用户设置 VNC 密码的命令。
- **卷组 (VG)** LVM 使用的一组 PV。
- **Web 页面命中** 从 Web 浏览器发送到 Web 服务器的单个 HTTP 请求。
- **知名端口** 在 65,535 个可能的端口中，0 到 1024 的端口，由常见网络服务使用。
- **which 命令** 用于定位 PATH 变量中列出的目录中存在的文件的命令。
- **whois 命令** 用于获取维护 DNS 域的组织信息的命令。
- **广域网 (WANs)** 计算机在地理上相距甚远的网络。
- **通配符元字符** 用于匹配文件或目录名称中特定字符的元字符；它们常用于指定多个文件。
- **窗口管理器** 负责确定 X Windows 在屏幕上绘制的窗口外观的 GUI 组件。
- **无线保真 (Wi-Fi)** 一种使用以太网通过空中传输数据的 LAN 技术。
- **工作站** 用于连接到服务器上的服务的计算机。
- **工作站服务** 用于访问网络服务器上共享资源的服务。
- **X 客户端** X Windows 的组件，从 X 服务器请求绘制图形并在终端屏幕上显示它们。
- **X 显示管理器 (xdm)** 图形登录屏幕。
- **X 服务器** X Windows 的组件，在终端屏幕上的窗口上绘制图形。
- **X Windows** Linux GUI 中在终端屏幕上的窗口上显示图形的组件。
- **X.org** Linux 发行版中常用的 X Windows 实现。
- **XFree86** Linux 发行版中常用的 X Windows 实现。
- **xvfb** 一个用于微调 X Windows 中视频卡的 sync 和 hsync 设置以便使用的程序。
- **xwininfo 命令** 用于显示 X Windows 状态信息的命令。
- **yum (Yellowdog Updater Modified) 命令** 用于从软件仓库安装和升级 RPM 软件包，以及管理和删除已安装的 RPM 软件包的命令。
- **zcat 命令** 用于将使用 **compress** 或 **gzip** 创建的归档内容查看到标准输出的命令。
- **Zettabyte 文件系统 (ZFS)** 一种高性能文件系统和卷管理软件，常用于在 Linux 和 UNIX 系统上从多个存储设备创建卷。
- **zfs 命令** 用于配置 ZFS 文件系统特性的命令。
- **ZFS 池** 由 **ZFS** 管理的一系列存储设备。
- **ZFS 子系统** ZFS 卷上的一个子目录，可由 ZFS 作为独立单元进行管理。
- **ZFS 卷** 从 ZFS 池内的空间创建的包含 ZFS 文件系统的卷。
- **zless 命令** 用于以逐页方式将使用 **compress** 或 **gzip** 创建的归档内容查看到标准输出的命令。
- **zmore 命令** 用于以逐页方式将使用 **compress** 或 **gzip** 创建的归档内容查看到标准输出的命令。
- **僵尸进程** 一个已执行完但其父进程尚未释放其 PID 的进程；僵尸仍在内核进程表中保留一个位置。
- **区域** 由一个或多个 DNS 服务器管理的域名空间的一部分。
- **区域传送** 将某个区域的资源记录从主 DNS 服务器复制到从 DNS 服务器的过程。
- **zpool 命令** 用于配置 ZFS 池和卷的命令。

Copyright 2016 Cengage Learning. All Rights Reserved. May not be copied, scanned, or duplicated, in whole or in part. Due to electronic rights, some third party content may be suppressed from the eBook and/or eChapter(s).

Editorial review has deemed that any suppressed content does not materially affect the overall learning experience. Cengage Learning reserves the right to remove additional content at any time if subsequent rights restrictions require it.

## 索引

- h (主机名), 314
- u (用户名), 314
- w (当前目录名称), 314
- 元字符, 85
- 3DES (三重数据加密标准), 560

### A

- aa-complain 命令, 655
- aa-enforce 命令, 655
- ab (Apache 基准测试) 命令, 590
- 绝对路径名, 84, 484, 486
- 接受打印作业, 426
- 访问控制列表 (ACL), 165–166
- 活动分区, 350
- add-apt-repository 命令, 511
- 管理
  - 文件, 474
  - 日志文件, 434–443
  - 打印机, 426–434
  - 远程, 556–562
  - 软件相关, 474
  - 用户和组, 443–454
- ADSL (非对称数字用户线路), 541
- 高级加密标准 (AES), 560
- 高级存储配置
  - iSCSI 配置, 261
  - 并行 SCSI 配置, 258–260
  - RAID 配置, 262–265
  - SCSI 硬盘驱动器配置, 258
  - 串行连接 SCSI 配置, 260
- AIX UNIX, 16
- alias 命令, 318
- 别名
  - 创建, 318–319
  - 列出, 140
  - 覆盖, 140
  - 查看, 318
- ANDing, 529
- Android, 32–33
- –a 选项, 93, 94
- apachectl 命令, 590
- Apache 开源开发者组, 588
- Apache Web 服务器, 554
  - 配置, 588
  - 管理, 588–589
  - 监控, 588–589
  - 安全性, 632, 646
  - 查看错误, 647
  - Web 页面命中, 589
- APIPA (自动专用 IP 编址), 534, 576
- AppArmor
  - 配置, 653–655
  - 配置文件, 654
- apparmor_status 命令, 654
- AppleTalk, 526
- 应用程序 (apps), 2–3
- 应用程序服务器, 28–29
- apt-cache 命令, 511
- apt-get (高级包工具) 命令, 510
- aptitude 命令, 511
- Aptitude 实用程序, 511
- ARCfour, 560
- 归档
  - 刻录软件, 492–493
  - crio 实用程序, 486–488
  - dump/restore 实用程序, 488–492
  - 系统备份, 481–493
  - tar (磁带归档) 实用程序, 482–486

