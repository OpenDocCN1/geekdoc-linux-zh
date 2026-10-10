
管理实用程序会寻找一个块来存放 MILO 的环境变量。如果这样的块已经存在，闪存管理实用程序会告诉你它的位置。否则，你必须使用 `environment` 命令来设置并初始化一个块。在上面的示例中，闪存块 12 包含了 MILO 的环境变量。

### D.7.1 “help” 命令

```
FWU> help

FWU 命令摘要：

list				- 列出闪存的内容
program			- 将映像编程到闪存中
quit				- 退出
environment		- 设置哪个块应包含环境变量
bootopt num		- 选择下次开机时使用的固件类型
help				- 打印此帮助文本
FWU>
```

*请注意，`environment` 和 `bootopt` 命令仅适用于 EB66+、AlphaPC64、EB164 和 PC164 系统（及其克隆系统）。*

### D.7.2 “list” 命令

“list” 命令显示当前闪存的使用情况。如果有多个闪存块，将显示每个闪存块的使用情况。在下例中，你可以看到 Windows NT ARC 正在使用块 4:7 和块 15。

```
FWU> list
Flash blocks:  0:DBM 1:DBM 2:WNT 4:WNT 5:WNT 6:WNT
			7:WNT 8:MILO 9:MILO 10:MILO 11:MILO 12:MILO 13:U 14:U 15:WNT
Listing flash Images
	Flash image starting at block 0:
	Firmware Id:	0 (Alpha Evaluation Board Debug Monitor)
	Image size is 191248 bytes (3 blocks)
	Executing at 0x300000
Flash image starting at block 3:
FMU> program
Image is:
Firmware Id: 7 (MILO/Linux)
Image size is 217896 bytes (4 blocks)
Executing at 0x200000
Found existing image at block 8
Overwrite existing image? (N/Y)? Y
Do you really want to do this (Y/N)? Y
Deleting blocks ready to program: 8 9 10 11
Programming image into flash
Scanning Flash blocks for usage
FMU>
```

### D.7.3 “program” 命令

闪存管理实用程序包含 MILO 闪存映像的一个压缩副本。“program” 命令允许你将此映像吹写到闪存中。该命令允许你退出操作，但在运行它之前，你应该使用 “list” 命令查看 MILO 应放在哪里。如果 MILO 已经在闪存中，闪存管理实用程序将提供覆盖它的选项。

请在系统断电前等待其完成。

注意：我无法过分强调你在这里必须多么小心，以免覆盖你可能需要存在的闪存映像或使你的系统变得无用。一个很好的规则是永远不要覆盖 Debug Monitor。

### D.7.4 “environment” 命令

这将选择一个闪存块来包含 MILO 的环境变量。

### D.7.5 “bootopt” 命令

这仅仅与 MILO 的 “bootopt” 命令相同，参见（第 D.6.4 节）。

### D.7.6 “quit” 命令

这实际上相当无意义。一旦闪存管理实用程序运行后，回到 MILO（或其他任何程序）的唯一方法是重启系统。

## D.8 限制。

不幸的是，这不是一个完美的世界，而且总有你需要了解的一些限制。

MILO 并非设计用于加载除 Linux 以外的操作系统，尽管它可以加载链接到与 Linux 在内存中相同位置（即 0xFFFFC0000310000）运行的映像。这就是闪存管理实用程序可以运行的原因。

miniboot/palcode/blah 中包含的 PALCode 源代码是正确的，但在使用最新的 gas 构建时存在问题。如果你使用 Alpha 评估板工具包中提供的古老的 a.out gas，它们 *确实* 能构建（它们就是这样构建的）。我正在试图找人修复新的 gas。在此期间，作为一种变通方法，我为支持的板卡提供了预构建的 PALCode，并且 David Mosberger-Tang 在他的 ftp 站点上有一个修复版的 gas。

## D.9 问题排查。

以下是一些常见的问题及其解决方案。

**从评估板调试监视器读取 MS-DOS 软盘。**

一些较旧版本的评估板调试监视器（2.0 版之前）存在与 Linux 生成的 DOS 格式软盘有关的问题。

通常，调试监视器可以正常加载前几个扇区，但随后会陷入无休止的循环，抱怨“坏扇区”。显然，调试监视器预期的 DOS 文件系统与 Linux 实现的 DOSFS 之间存在不兼容性。简而言之：如果你遇到这个问题，请尝试使用 DOS 写入软盘。例如，如果加载文件 MILO.cab 不起作用，请使用一台 DOS 机器，插入软盘，然后执行以下操作：

```
copy a:MILO.cab c:
copy c:MILO.cab a:
del c:MILO.cab
```

然后再次尝试从该软盘启动。这通常能解决问题。

**MILO 显示一长串 0> 并且不接受输入。**

这通常发生在 MILO 被构建为使用 COM1 作为次要控制台设备时。在这种情况下，MILO 会向 COM1 回显输出，并从那里接受输入。这对调试很有用，但如果连接的设备不是终端，那就不是很方便了。如果发生这种情况，请在 Linux 内核启动之前断开该设备或将其断电。一旦 Linux 正常运行，一切都会按预期工作。

**MILO 抱怨内核映像的魔术数字不正确**

旧版本的 MILO 不支持 ELF 对象文件格式，因此无法识别 ELF 映像，这可能是你的问题。如果报告此问题，请升级到你能找到的最新 MILO。所有 2.0.20 及更高版本的 MILO 都支持 ELF。另一方面，也可能是映像确实损坏了。你还应注意，MILO 尚不能自动区分 GZIP 压缩和非 GZIP 压缩的映像；你需要在文件名中添加 “.gz” 后缀。

**MILO 打印 “ . . . turning on virtual addressing and jumping to the Linux Kernel ” 然后没有任何反应**

一个明显的问题是内核映像构建错误或为其他 Alpha 系统构建。另一个问题是视频板是 TGA (Zxlp) 设备，但内核是为 VGA 设备构建的（或反之）。建议将内核构建为向 COM1 回显，然后在该串行端口上连接终端，或者重试随你安装的 Linux 发行版一起提供的内核。

**MILO 无法识别 SCSI 设备**

标准的 MILO 映像包含了已知在 Alpha 上稳定的尽可能多的设备驱动程序（目前包括 NCR 810、QLOGIC ISP、Buslogic 以及 Adaptec 2940 和 3940 卡）。如果你的卡不在其中，可能是因为该驱动程序在 Alpha 系统上还不够稳定。同样，值得尝试最新的 MILO 映像。你可以使用 “show” 命令来查看 MILO 映像内置了哪些 SCSI 设备。

## D.10 致谢。

我要感谢：

- Eric Rasmussen 和 Eileen Samberg，PALcode 的作者，
- Jim Paradis，键盘驱动程序、原始 MILO 界面和 AlphaBIOS 工作的贡献者，
- Jay Estabrook，因他的帮助和 bug 修复，
- David Mosberger-Tang，因他的免费 BIOS 模拟以及他的支持和鼓励，
- 最后（也是最少）感谢 Linus Torvalds，感谢他的计时器代码和内核。

MILO 还有许多事情需要完成，如果你想自己添加一些内容，请通过 mailto:david.rusling@reo.mts.dec.com 让我知道，以免我们重复工作。

最后，非常感谢 Digital 生产了如此出色的芯片（并支付我工资做这件事）。

# 附录 E

# Red Hat Linux 常见问题解答

## E.1 简介

这是官方的 Red Hat Linux FAQ。它由 faq-maintainer@redhat.com 维护；关于此 FAQ 的所有评论或建议都应发送至该地址。最新的此 FAQ 版本可从 http://www.redhat.com 获取，或通过电子邮件从 faq@redhat.com 获取。

## E.2 一般问题

### E.2.1 在哪里可以获得有关 Red Hat Linux 的信息？

- 通过 Web：http://www.redhat.com
- 通过 FTP：ftp://ftp.redhat.com

### E.2.2 我如何获取 Red Hat Linux？

Red Hat Linux 可从 Red Hat Software 或各种 Red Hat Linux 经销商处以 CD 形式获取；也可通过 FTP 从 ftp://ftp.redhat.com 及其许多镜像站点获取。

### E.2.3 Red Hat FTP 站点*很慢*。有镜像吗？

Red Hat FTP 站点有几个镜像：

| **区域** | **FTP 站点** | **目录** |
| :--- | :--- | :--- |
| **英国** | sunsite.doc.ic.ac.uk | /packages/linux/redhat |
| | nfs-uxsup.csx.cam.ac.uk | /pub/redhat/ |
| | ftp.ox.ac.uk | /pub/linux/redhat |
| **欧洲** | ftp.osb.hu | /pub/mirrors/linux/redhat |
| | sunsite.icm.edu.pl | /pub/linux/redhat |
| | ftp.vma.bme.hu | /pub/linux/redhat |
| | ftp.sfos.ro | /mirror/RedHat |
| | ftp.u-bordeaux.fr | /pub/Linux/redhat |
| | ftp.tu-chemnitz.de | /pub/linux/redhat-mirror/ |
| | ftp.wcfaua.ee | /pub/Linux/RedHat/ |
| | ftp.uni-bayreuth.de | /pub/linux/ftp.redhat.com/ |
| | ftp.pk.edu.pl | /pub/linux/redhat |
| | sunsite.uio.no | /pub/unix/Linux/RedHat/ |
| | ftp.etud.insa-tlse.fr | /pub/redhat |
| | ftp.arch.pwr.wroc.pl | /mirror/linux/redhat/ |
| | ftp.ras.ru | /pub/linux/redhat |
| | ftp.u-bordeaux.fr | /pub/linux/redhat |
| | ftp.ibp.fr | /pub/linux/distributions/redhat |
| | redhat.netvision.net.il | /pub/mirrors/redhat |
| | ftp.sorosis.ro | /pub/mirrors/ftp.redhat.com |
| | ftp.mp1-sb.mpg.de | /pub/linux/mirror/ftp.redhat.com |

