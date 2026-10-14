

![](img/7aaa8e4f2209bf9f2fb443905096e94c_336_0.png)

图 13.5 GRUB 启动加载器为启动甚至不熟悉的系统提供了极大的灵活性。

## 使用恢复功能

在计算机启动时，Ubuntu 会显示一条提示，按 Escape 键以查看 GRUB 菜单的提示。如果你这样做，你会看到可启动操作系统的列表，其中将包括 Ubuntu 安装的恢复模式选项。如果你启动到恢复模式，你将获得对机器的自动 root 访问权限，可以在其中安全地修复你的问题。

另外，你可以插入 Ubuntu 安装光盘并从那里使用恢复模式。请记住，这些恢复模式旨在成为仅文本的系统，用于严肃的系统恢复目的；不要期望它们是手把手的，也不要期望它们易于使用！

## 相关 Ubuntu 命令

以下命令在 Ubuntu 中执行备份、恢复和还原操作时很有用：

- amdump—Amanda 是一个基于网络的备份系统，由 18 个独立命令组成，用于 Linux。
- ark—KDE 桌面 GUI 归档实用程序。
- cp—复制命令。
- scp—安全 shell 复制命令。
- cpio—数据归档实用程序。
- dd—数据复制和转换实用程序。
- gzip—GNU 压缩实用程序。
- tar—GNU 磁带归档实用程序。

## 参考

- http://www.tldp.org/LDP/solrhe/Securing-Optimizing-Linux-RH-Edition-v1.3/whywhen.html—使用 dump 和 restore 进行备份的彻底讨论，附带示例。
- http://en.tldp.org/LDP/solrhe/Securing-Optimizing-Linux-RH-Edition-v1.3/chap29sec306.html—使用 cron 用 tar 进行自动备份。
- http://kmself.home.netcom.com/Linux/FAQs/backups.html—Linux Backups 小型 FAQ 包含了一些关于备份介质、压缩、加密和安全性的有用但简短的评论。
- http://www.tldp.org/—Linux 文档项目提供了几份有用的 HOWTO 文档，讨论备份和磁盘恢复。
- http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Bootdisk-HOWTO.html#EAN1483—这里是 LILO 启动错误代码列表，可帮助你调试无法启动的挑剔系统。
- http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Ftape-HOWTO.html—这是软盘磁带设备驱动程序的 HOWTO。
- http://www.linux-usb.org/USB-guide/x498.html—用于大容量存储设备的 USB 指南。如果你有 USB 设备并需要知道它是否受支持，请在此处查看。
- http://www.backupcentral.com/amanda.html—这是《Unix Backup and Recovery》的 Amanda 章节（由 John R. Jackson 撰写，由 O’Reilly and Associates 出版）。该章节可在网上获取，涵盖了使用 Amanda 的各个方面。该网站为该章节提供了一个方便的搜索工具。
- http://twiki.org/cgi-bin/view/Wikilean/RsyncingALargeFileBeginner—Rsyncing 一个大文件以“修复”不通过 md5sum 检查的本地 ISO 映像。
- http://www.lycoris.org/sections.php?op=viewarticle&artid=8—Lycoris ISO rsync 小型 HOWTO。关于使用 rsync 同步文件的逐步教程。
- http://www.mikerubel.org/computers/rsync_snapshots/—使用 rsync 进行自动快照式备份。
- http://www.mondorescue.org/—Mondo Rescue 是一个独立于 Ubuntu 的裸机备份/救援工具，使用 CD、DVD、磁带或 NFS；它可以生成可启动 CD 以恢复系统。
- http://www.ccp14.ac.uk/ccp14admin/linux-server/mondorescue/dvd_mondo.html—使用 MondoRescue 在 DVD 上备份的 HOWTO。
- http://www.linuxorbit.com/modules.php?op=modload&name=Sections&file=index&req=review&catid=222&pager=1—使用 split 和 mkisofs 手动将大型归档备份到 CD 的 HOWTO。

本页 intentionally left blank

## 第 14 章

## 网络

开源技术总体上以及 Linux 特别的优势之一是，它现在已经成熟到可以在多种不同的网络环境以及互联网上轻松使用。Linux 对标准互联网协议 TCP/IP 具有强大的支持，还可以与所有 UNIX 变体通信，包括 Mac OS X、Windows（借助 Samba 的帮助）、NetWare（IPX）甚至像 DECNET 和 Banyan Vines 这样较旧的协议。许多组织使用 Linux 作为互联网网关，允许许多不同的客户端通过 Linux 访问互联网，以及通过电子邮件和即时消息进行通信。本章涵盖网络和互联网连接，因为大多数网络最终都会以某种形式连接到互联网。你将学习如何做好基础工作，包括使用 Ubuntu 配置和管理网卡（NIC）和其他网络服务。你还将了解如何从命令行管理网络服务——这在你被限制在命令行提示符下时又是一项重要课程。我们还将研究连接选项，既针对入站网络流量也针对出站网络流量，以及 PPP（点对点协议）的重要性。还包括对 Ubuntu 图形管理客户端的概述，这些客户端变得越来越受欢迎。

### 奠定基础：`localhost` 接口

在你成功连接到网络甚至互联网之前需要发生的第一件事是创建 localhost 接口，有时也称为 *loopback interface*，但更常被称为 *lo*。TCP/IP 协议（参见后面的“使用 TCP/IP 进行网络”）

本章内容

- 奠定基础：The `localhost` Interface
- Networking with TCP/IP
- Network Organization
- Hardware Devices for Networking
- Using Network Configuration Tools
- Dynamic Host Configuration Protocol
- Wireless Networking
- Beyond the Network and onto the Internet
- Common Configuration Information
- Configuring Digital Subscriber Line Access
- Configuring Dial-Up Internet Access
- Troubleshooting Connection Problems
- Reference

