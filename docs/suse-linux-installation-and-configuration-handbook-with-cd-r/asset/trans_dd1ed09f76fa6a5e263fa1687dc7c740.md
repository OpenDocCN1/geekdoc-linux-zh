

## 第14章，“配置域名服务”
- Firewall-Piercing-HOWTO
- IP-Masquerade-HOWTO
- IP-Subnetworking-HOWTO
- UNIX-Internet-Fundamentals-HOWTO
- The DNS-HOWTO.gz
- BIND 制作者的网站 http://www.isc.org
- http://www.intac.com/~cdp/cptd-faq/ 网站上有一个大型 FAQ

## 第15章，“通过 Samba 连接 Windows”
- SMB-HOWTO

## 第16章，“与其他操作系统连接”
- netatalk—你应该阅读 NET-3-HOWTO.gz 中的 AppleTalk 部分
- ncpsfs—你应该阅读 IPX-HOWTO.gz
- marsnwe—该软件包的完整文档位于 /usr/doc/packages/marsnwe

## 第17章，“配置 Usenet 新闻服务”
- News-Leafsite-HOWTO

## 第18章，“设置 Apache Web 服务器”
- Apache 网站 http://www.apache.org

## 第19章，“配置 FTP 服务器”
- proftpd 的完整文档位于 /usr/doc/packages/proftpd 目录
- ProFTPD 网站 http://www.proftpd.net

## 第20章，“配置邮件服务器”
- sendmail 网站 http://www.sendmail.org
- /usr/doc/packages/sendmail 中的 sendmail 文档

## 第21章，“配置拨入服务器”
- mgetty—http://alpha.greenie.net/mgetty/
- pppd—pppd 手册页

## 第22章，“将 SuSE Linux 设置为代理服务器”
- Squid2 的完整文档位于 /usr/doc/packages/squid2 目录
- Squid 网站 http://squid.nlanr.net/Squid

## 第23章，“连接到 Internet”

ISP-Hookup-HOWTO.gz、Modem-HOWTO.gz 和 PPP-HOWTO.gz HOWTO 对感兴趣的读者非常重要：

- isapnptools—isapnp 和 pnppdump 手册页。你还应该阅读 Plug-and-Play-HOWTO.gz
- pppd—pppd 手册页
- pciutils—pciutils 主页 http://atrey.karlin.mff.cuni.cz/~mj/pciutils.html
- minicom—Minicom 的完整信息位于 /usr/doc/packages/minicom
- wvdial—wvdial 已集成在 YaST 中，因此你应该使用 YaST 帮助来使用 wvdial。查看 /usr/doc/packages/wvdial，其中包含多种语言的 wvdial 完整信息

## 第24章，“配置桌面”
- KDE—KDE 帮助、KDE 快速入门指南 和 KDE 用户指南
- GNOME—GNOME 帮助、GNOME 快速入门指南 和 GNOME 用户指南

## 第25章，“安装和配置 StarOffice”
- StarOffice—StarOffice 帮助 和 StarOffice Sun Microsystems 网页 http://www.sun.com/products/staroffice
- StarOffice 中的打印—参见第 11 章

## 第26章，“安装和配置 WordPerfect”
- Corel WordPerfect 帮助
- Corel WordPerfect 网站 http://linux.corel.com

## 第27章，“安装 GIMP”
- GIMP 网站 http://www.gimp.org

## 第28章，“安装和配置 Netscape Communicator”
- Netscape 帮助—Netscape 帮助 和 Netscape 在线帮助
- Netscape 网站 http://www.netscape.com

## 第29章，“配置 MySQL”
- 本地系统上存储的 MySQL 文档 /usr/doc/packages/mysql/html/index.html
- MySQL 网站 http://www.mysql.com

## 第30章，“安装和配置 Oracle”
- Oracle 文档
- SuSE 在线 Oracle 安装

## 第31章，“使用 Shell”
- bash—bash 手册 和 info 页面
- csh—csh 手册 和 info 页面
- Midnight Commander

## 附录 B，“硬件兼容性列表”
- SuSE 硬件在线列表数据库。

## 附录 C，“YaST”
- SuSE 硬件在线列表数据库

## 附录 D，“调整 Linux 系统的技巧”
- /usr/doc/howto/en/Tips-HOWTO.gz 处的 tricks HOWTO
- Linux 调优网站 http://tune.linux.com

## 附录 E，“各种实用程序”
- tar—tar info 页面

## 硬件兼容性列表

本附录中

- 支持的主板、CPU 和内存 626
- 支持的视频显卡 626
- 硬盘控制器 640
- 硬盘 642
- 磁带驱动器 642
- CD-ROM 643
- CD 刻录机 644
- 可移动驱动器 644
- 鼠标 645
- 控制器（I/O） 645
- 控制器（多端口） 645
- 网络适配器 646
- ISDN 648
- 口袋和便携适配器 648
- 声音卡 650
- 调制解调器 651
- 打印机 652
- 扫描仪 653
- 业余无线电 654
- 串口终端 654
- 操纵杆 655
- 视频采集板/帧 grabber/TV 调谐器 655
- UPS 656

本附录尝试列出 SuSE Linux 支持的大多数硬件。如果你的硬件未在此列表中出现，请查看 SuSE 网站 http://cdb.suse.de/cdb_english.html 上的最新更新。你会找到一个具有搜索功能的大型硬件数据库，该数据库更新非常频繁。

### 支持的主板、CPU 和内存

Linux 支持今天存在的几乎所有主板。几乎不可能找到与 Linux 有问题的的板。ISA、VLB、EISA 和 PCI 总线均受支持。PS/2 和 Microchannel（MCA）也在标准中受支持。2.2.x 内核及更高版本中也存在对 MCA 的支持，但该代码仍有点 buggy。

Linux 支持多种 x86 处理器。支持 Intel/AMD/Cyrix 386SX/DX/SL/DXL/SLC 和 486SX/DX/SL/SX2/DX2/DX4。此外，支持 Intel Pentium、Pentium Pro 和 Pentium II。AMD K5 和 K6 工作良好，尽管应避免使用较旧版本的 K6，因为它们 buggy。但是，将 BIOS 设置中的内部缓存设置为禁用可以作为此问题的解决方法。IDT Winchip C6/PSME2066A 处理器也在 Linux 下受支持。此外，如果你没有数学协处理器，Linux 具有内置的 FPU 仿真。

Linux 支持使用多个处理器的系统，也称为 SMP 系统。Linux 自内核 2.0.x 分支以来就支持这些系统。2.2.x 分支在此领域提供更好的支持，而即将推出的 2.4.x 分支有望提供更好的支持。

Linux 支持所有存在的内存类型。所有内存，如 DRAM、EDO 和 SDRAM 都可与 Linux 一起使用。在某些系统上，如果你有超过 64MB 内存，可能需要告诉内核你有多少内存。这对于内核 2.0.x 分支也是必要的。要告诉内核你有多少内存，只需将以下行添加到你的 /etc/lilo.conf 文件中：

```
append="mem=96M"
```

然后，运行 lilo。确保你输入了内存的正确大小。不要输入超过你实际拥有的值，因为它会导致内核崩溃。

### 支持的视频显卡

Linux 对今天可用的大多数视频显卡都有良好的支持。尽管如此，这种支持并非来自 Linux，而是来自为 Linux 提供著名 X Window 系统端口的 XFree86。

XFree86 支持以下卡：

- 2 the Max MAXColor S3 Trio64V+
- 3DLabs Oxygen GMX
- 928Movie
- AGX（通用）
- ALG-5434(E)
- 3Dexplorer
- ATI Mach64 GT（264GT），又名 3D RAGE，Int. RAMDAC
- ATI Mach64 VT（264VT），内部 RAMDAC
- ATI Mach64 with AT&T 20C408 RAMDAC
- ATI Mach64 with ATI68860 RAMDAC
- ATI Mach64 with ATI68860B RAMDAC
- ATI Mach64 with ATI68860C RAMDAC
- ATI Mach64 with ATI68875 RAMDAC
- ATI Mach64 with CH8398 RAMDAC
- ATI Mach64 with IBM RGB514 RAMDAC
- ATI Mach64 with Internal RAMDAC
- ATI Mach64 with STG1702 RAMDAC
- ATI Mach64 with STG1703 RAMDAC
- ATI Mach64 with TLC34075 RAMDAC
- ATI Pro Turbo+PC2TV，3D Rage II+DVD
- ATI Ultra Plus
- ATI Video Xpression
- ATI Video Xpression+
- ATI WinBoost
- ATI WinBoost with AT&T 20C408 RAMDAC
- ATI WinBoost with ATI68860 RAMDAC
- ATI WinBoost with ATI68860B RAMDAC
- ATI WinBoost with ATI68860C RAMDAC
- ATI WinBoost with ATI68875 RAMDAC
- ATI WinBoost with CH8398 RAMDAC
- ATI WinBoost with Mach64 CT（264CT）
- ATI WinBoost with STG1702 RAMDAC
- ATI WinBoost with STG1703 RAMDAC

