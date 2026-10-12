
## E.7 运行闪存管理工具

`run` 命令用于运行闪存管理工具。在开始之前，你需要准备一个 Milo 可用的设备，其中包含 `updateflash` 程序。该文件（如同 `vminux` 一样）可以经过 gzip 压缩。你需要使用 `(run)` 命令从 Milo 中运行闪存管理工具程序：

```
MILO> run fd0:fmuz.gz
```

一旦加载并初始化完成，闪存管理工具将提供一些关于闪存设备的信息，并显示命令提示符。同样，`help` 命令最为有用。

```
Linux Milo Flash Management Utility V1.0
Flash device is an Intel 28F008SA
16 segments, each of 0x10000 (65536) bytes
Scanning Flash blocks for usage
Block 12 contains the environment variables
FMU>
```

请注意，在环境变量可能存储且存在多个闪存块（例如 AlphaPC64）的系统中，闪存管理工具会寻找一个用于存放 Milo 环境变量的块。如果已存在这样的块，闪存管理工具会告知其位置。否则，你必须使用 `environment` 命令设置并初始化一个块。在上述示例中，闪存块 12 包含 Milo 的环境变量。

### E.7.1 "help" 命令

```
FMU> help
FMU command summary:

list - List the contents of flash
program - program an image into flash
quit - Quit
environment - Set which block should contain the environment variables
bootopt num - Select firmware type to use on next power up
help - Print this help text
FMU>
```

请注意，`environment` 和 `bootopt` 命令仅在 EB66+、AlphaPC64 和 EB164 系统（及其克隆机型）上可用。

### E.7.2 "list" 命令

"list" 命令显示闪存存储器的当前使用情况。当存在多个闪存块时，将显示每个闪存块的使用情况。在下面的示例中，可以看到 Windows NT ARC 使用了 4:7 块和第 15 块。

```
FMU> list

 Flash blocks:  0:DBM  1:DBM  2:DBM  3:WNT  4:WNT  5:WNT  6:WNT  7:WNT  8:Milo
 9:Milo  10:Milo  11:Milo  12:Milo  13:0  14:0  15:WNT
 Listing flash Images

 Flash image starting at block 0:
    Firmware Id:   0 (Alpha Evaluation Board Debug Monitor)
    Image size is 191248 bytes (3 blocks)
    Executing at 0x300000

 Flash image starting at block 3:
    Firmware Id:   1 (Windows NT ARC)
    Image size is 277664 bytes (5 blocks)
    Executing at 0x300000

 Flash image starting at block 8:
    Firmware Id:   7 (Milo/Linux)
    Image size is 217896 bytes (4 blocks)
    Executing at 0x200000

 FMU>
```

### E.7.3 "program" 命令

闪存管理工具中包含一份 Milo 闪存映像的压缩副本。"program" 命令允许你将此映像写入闪存。该命令允许你取消操作，但在运行之前，你应该使用 "list" 命令查看 Milo 应放置的位置。如果 Milo 已在闪存中，闪存管理工具将询问是否覆盖它。

```
FMU> program
Image is:
Firmware Id: 7 (Milo/Linux)
Image size is 217896 bytes (4 blocks)
Executing at 0x200000
Found existing image at block 8
Overwrite existing image? (N/y)? y
Do you really want to do this (y/N)? y
Deleting blocks ready to program: 8 9 10 11
Programming image into flash
Scanning Flash blocks for usage
FMU>
```

请等待操作完成后再关闭系统电源。

注意：我必须强调，在这里你必须非常小心，不要覆盖你可能需要的现有闪存映像，否则会导致系统无法使用。一条很好的规则是永远不要覆盖调试监视器（Debug Monitor）。

### E.7.4 "environment" 命令

此命令选择一个闪存块来包含 Milo 的环境变量。

### E.7.5 "bootopt" 命令

这与 Milo 的 "bootopt" 命令完全相同，请参阅第 E.6.4 节 "bootopt" 命令。

### E.7.6 "quit" 命令

这个命令实际上意义不大。一旦闪存管理工具运行完毕，返回 Milo（或其他状态）的唯一方法是重启系统。

## E.8 限制

不幸的是，世界并不完美，因此总有一些需要注意的限制。

Milo 的设计初衷并非用于加载 Linux 以外的操作系统，尽管它可以加载那些链接到与 Linux 相同内存位置（即 `0xFFFFFC0000310000`）执行的映像。这就是闪存管理工具能够运行的原因。

包含在 `trmniniboot/palcode/t/ttlah` 中的 PALCode 源代码是正确的，但是在使用最新的 gas 构建时存在问题。如果使用 Alpha 评估板工具包中提供的古老的 a.out gas，则可以成功构建（它们就是这样构建的）。我正在试图让有人修复新的 gas。在此期间，作为一个变通方案，我已为支持的板卡提供了预编译的 PALCode，David Mosberger-Tang 在他的 ftp 站点上有一个修复后的 gas。

## E.9 问题解决

以下是一些常见的问题及其解决方案。

**从评估板调试监视器读取 MS-DOS 软盘。** 多人报告在使用 Digital Alpha 评估板（如 AlphaPC64）附带的评估板调试监视器从软盘读取文件时遇到问题。通常，调试监视器可以正确加载前几个扇区，但随后会进入无限循环并抱怨“坏扇区”。显然，调试监视器预期的 DOS 文件系统与 Linux 实现的 DOSFS 之间存在不兼容性问题。长话短说：如果遇到此问题，请尝试使用 DOS 写入软盘。例如，如果加载文件 `milo.cab` 不起作用，请使用 DOS 机器，插入软盘，然后执行：

```
copy a:milo.cab c:
copy c:milo.cab a:
del c:milo.cab
```

然后再次尝试从该软盘启动。这通常可以解决问题。

**Milo 显示一长串 0 且不接受输入。** 这通常发生在 Milo 被构建为使用 COM1 作为辅助控制台设备的情况下。在这种情况下，Milo 会将输出回显到 COM1 并从中接受输入。这对于调试非常有用，但如果连接的设备不是终端，则不太好。如果发生这种情况，请断开设备或断电，直到 Linux 内核启动完成。一旦 Linux 正常运行，一切都会如预期般工作。

## E.10 致谢

我要感谢：

- Eric Rasmussen 和 Eilteen Samberg，PALcode 的作者；
- Jim Paradis，因其键盘驱动器和最初的 MILO 界面；
- Jay Estabrook，因其帮助和 bug 修复；
- David Mosberger-Tang，因其共享软件 BIOS 模拟以及他的支持和鼓励；
- 最后（且*绝非*次要地），感谢 Linus Torvalds，因其定时器代码及其内核。

Milo 还有很多事情需要完成，如果你想要自己添加某些内容，请告知我 david.rusling@reo.mts.dec.com，以便我们不重复劳动。

最后，向 Digital 表示巨大感谢，感谢他们生产出如此出色的芯片（并支付费用让我做这件事）。

# 附录 F

# Red Hat Linux 常见问题解答

## F.1 引言

这是 Red Hat Linux 官方常见问题解答（FAQ）的第二版。它由 redhat@redhat.com 维护，关于此 FAQ 的所有评论或建议请发送至该地址。要获取此 FAQ 的更新，请发送电子邮件至 faq@redhat.com 以获取自动回复，或在任何 Red Hat 镜像的 docs 目录中查看。

如果你拥有此文档的印刷版本（例如来自 Red Hat 用户指南）并希望获取最新版本，请参阅 http://www.redhat.com 或发送电子邮件至 faq@redhat.com。

## F.2 一般性问题

### F.2.1 我可以在哪里获取关于 Red Hat Linux 的信息？

联系 Red Hat Software 获取订购信息。最好的方式是访问 http://www.redhat.com。获取其他信息，请发送电子邮件至 info@redhat.com 以获取自动回复（非常有用……真的）。你也可以浏览

ftp://ftp.redhat.com 和 http://www.redhat.com 以获取新公告和产品信息。

### F.2.2 Red Hat Linux 提供哪些媒体？

目前，它可以通过 CD 和 FTP 获取。要了解从哪里 FTP 获取，请参阅关于 Red Hat 镜像的问题。

### F.2.3 Red Hat FTP 站点速度较慢。有没有镜像？

Red Hat FTP 站点有几个镜像：

- 英国
  - sunsite.doc.ic.ac.uk /packages/linux/redhat
  - nfs-uxsup.cox.cam.ac.uk /pub/redhat/
  - ftp.ox.ac.uk /pub/linux/redhat
- 欧洲
  - ftp.pk.edu.pl /pub/linux/redhat
  - ftp.arch.pwr.wroc.pl /mirror/linux/redhat/
  - ftp.ras.ru /pub/Linux/redhat
  - ftp.u-bordeaux.fr /pub/Linux/redhat
  - ftp.ibp.fr /pub/linux/distributions/redhat
  - redhat.netvision.net.il /pub/mirrors/redhat
  - ftp.sorosis.ro /pub/mirrors/ftp.redhat.com
  - ftp.mp1-sb.mpg.de /pub/linux/mirror/ftp.redhat.com
  - ftp.jate.u-szeged.hu /pub/linux/redhat
  - ftp.ibp.fr /pub/linux/distributions/redhat
  - ftp.gwdg.de /pub/linux/install/redhat
  - ftp.msu.ru /pub/Linux/RedHat
  - ftp.sgg.ru /mirror/redhat
  - sunsite.mff.cuni.cz /OS/Linux/Distributions/RedHat
  - ftp.ton.tut.fi /pub/Linux/RedHat
  - garbo.uwasa.fi /pub/mirror/RedHat
  - ftp.funet.fi /pub/Linux/images/RedHat

