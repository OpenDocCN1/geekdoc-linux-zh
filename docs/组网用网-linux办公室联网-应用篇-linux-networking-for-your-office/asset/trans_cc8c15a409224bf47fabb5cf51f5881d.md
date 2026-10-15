

如果打印机是 PostScript 型号，当然，无论它托管在 Linux 还是 Windows 系统上。

> NOTE
> 
> 你可能会发现将打印服务器配置为接受 UNIX 风格的打印作业更容易。Linux 当然可以做到这一点，Windows NT 也可以。

## Summary

在你配置了 Linux 打印机队列并为文件共享设置了 Samba 之后，与 DOS、Windows 和 OS/2 机器共享打印机，只需在 /etc/smb.conf 文件中为打印机添加一个条目即可。该条目与文件共享条目非常相似，这是有原因的：Samba 打印机共享的工作方式与文件共享非常相似。客户端计算机打开一个共享并向其写入文件，Samba 随后将该共享定向到标准的 Linux 打印机队列。

在此场景中最大的复杂性来自于需要选择合适的打印机驱动程序集，既在 Linux 中（如果打印到非 PostScript 打印机，则用于 Ghostscript），也在客户端操作系统中（以匹配 Ghostscript 以及通过 Ghostscript 的打印机功能）。因此，在某些情况下，使用原生客户端操作系统驱动程序和原始队列进行打印可能更简单易配置。

也可以反向进行此过程，从 Linux 打印到 Windows 打印机。然而，你应该意识到这样做的安全影响，因为此配置要求服务器的密码以未加密的形式存储在客户端硬盘上，可供所有用户读取。

## Netatalk: Sharing Printers with Macintoshes

### CHAPTER
17

### IN THIS CHAPTER

- An Overview of Macintosh-Style Printer Sharing 408
- Setting Up Remote Access 411
- Configuring MacOS for Printing 415
- Printing from Linux to Macintosh Printers 419
- Summary 422

Linux 的打印机共享功能如果没有对 Macintosh 的支持就不算完整，而 Linux 在这方面也不令人失望。然而，Red Hat 6.0 并未随附必要的软件 Netatalk，因此它包含在本書附带的 CD-ROM 的 sams-extras/netatalk 目录中。Netatalk 结合 Linux 内核中对 Apple Datagram Delivery Protocol (DDP; p. 293) 的支持，使 Linux 能够参与 Apple 原生的网络“对话”。

本章不讨论 Netatalk 的基本配置。关于这一点，你应该阅读第 12 章“Netatalk: Sharing Files with Macintoshes”，尤其是标题为“Compiling AppleTalk Support into Your Kernel”和“The atalkd Daemon”的部分。在你启动了基本的 Netatalk 服务后，你可以阅读本章学习如何使你的打印机可供 Macintosh 使用。

Linux 可以成为 Macintosh 的出色打印服务器，部分原因在于 Macintosh 与网络 PostScript 打印机配合良好，但与大多数廉价喷墨打印机配合不佳，而使用 Linux 你可以将 PostScript 转换为喷墨打印机可理解的格式。你可以通过在 Linux 中配置 Ghostscript 程序自动作为打印过滤器的一部分来做到这一点。因此，你可以设置一台 Linux 计算机为一组 Macintosh 工作组提供两到三台廉价彩色喷墨打印机。即使包括 Linux 服务器的成本（它可以做的不止是提供打印机），你也可能比购买更昂贵的网络 PostScript 彩色打印机节省资金。Macintosh 也能自行共享其非 PostScript 彩色打印机，但这会占用服务器计算机，意味着你必须将计算机专用于服务器（在这种情况下，Linux 计算机和 PC 硬件更便宜），或者服务器计算机的用户在任何人想要打印作业时必须忍受性能下降。

### An Overview of Macintosh-Style Printer Sharing

一些最早的 Macintosh 使用 AppleTalk over LocalTalk 网络打印到最早的 LaserWriter（随后是其他 PostScript 打印机）。事实上，共享昂贵的 LaserWriter 打印机是大多数早期 AppleTalk 网络的主要功能。

由于早期的 Apple 激光打印机是 PostScript 型号，Apple 的网络打印模型高度以 PostScript 为中心。如今 PostScript 打印机种类繁多，因此 Apple 的 PostScript 驱动程序使用一个描述 PostScript 打印机功能的文件。这种方法允许单个 Macintosh 打印机驱动程序处理功能各异的各种打印机。

了解协议和打印机描述两者将有助于你处理 Macintosh 打印并配置 Netatalk 以服务 Macintosh，因此相关信息在此呈现。

