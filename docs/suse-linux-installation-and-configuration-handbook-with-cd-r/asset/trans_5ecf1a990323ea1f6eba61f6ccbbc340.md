

## 附录

- A 获取更多信息 615
- B 硬件兼容性列表 625
- C YaST 657
- D 调优 Linux 系统的技巧 681
- E 各种实用工具 693

## 获取更多信息

本章内容

- SuSE 帮助系统 616
- 软件需求 616
- 章节逐章导读 618

### SuSE 帮助系统

SuSE Linux 附带了由 SuSE 团队创建的帮助系统。SuSE Linux 的帮助系统是一个程序，由一个大型在线数据库和一个额外的支持数据库组成。

SuSE 帮助系统可在任何 Web 浏览器上运行。如果您刚刚安装了 Linux，可以通过发出以下命令启动 SuSE 帮助系统：

```
bash$hilfe
```

您也可以通过将 SuSE 帮助系统索引页面的正确地址传递给浏览器来轻松启动它。以下是一个示例：

- 在 X Windows 中，运行以下其中一个应用程序：
  - Netscape—通过输入 bash$netscape 运行它。
  - Arena—通过输入 bash$arena 运行它。
  - KFM—要在 KDE 中运行它，请打开任何文件管理器窗口。

在地址栏中输入 http://localhost 并按 Enter。

在 SuSE Linux 控制台中，只需发出 hilfe 命令即可。虽然，您可以指定 -nox 参数以强制其使用 lynx 作为浏览器：

```
bash$hilfe -nox
```

SuSE 帮助系统是一个支持关键词搜索的页面。从类别中选择您想要了解更多信息的文档，或输入查询以搜索随 SuSE 提供的整个文档中的关键词。

### 软件需求

附录需要特殊软件包似乎有点奇怪。然而，您需要安装某些软件包和应用程序才能获取更多信息和功能。例如，SuSE 帮助系统必须通过 Web 服务器运行才能与任何 Web 浏览器兼容。此外，要访问任何应用程序的文档，您首先必须安装该应用程序。您也可以通过安装文档和 HOWTO 软件包来获取更多信息。以下是在 SuSE Linux CD 上可用的文档。

软件包需求：

Series doc：

- a11man—所有软件包的所有手册页。
- books—一些书籍。
- dns_faq—域名系统常见问题解答（及答案）。
- elispint—Emacs Lisp 编程。
- elispman—GNU Emacs Lisp 参考手册。
- fhs—文件系统层次结构标准。
- gawkdoc—gawk 的文档。您仅在要开发 shell 脚本时才需要此文档。
- gccinfo—gcc 的 GNU info 页面。您仅在要开发 Linux 应用程序时才需要此文档。
- ge_info—GNU Emacs 的 Info 文件。您仅在要将 Emacs 用作编辑器时才需要此文档。
- gppinfo—libg++ 的文档。您仅在要开发 Linux 应用程序时才需要此文档。
- howto series—随 SuSE Linux 提供的 howto 系列有多种格式和多种语言。阅读 HOWTO 时选择您想要使用的语言和格式。请注意，使用 SuSE 帮助系统时使用 HTML。
- inf2htm—info2html，可将 info 页面转换为 HTML 页面。此软件包使 SuSE 帮助系统能够从 info 页面生成 HTML 文件。
- javadox—Java JDK1.1.3 文档和演示。您仅在要开发 Java 应用程序时才需要此文档。
- ldp—Linux 文档项目 HTML 归档。
- ldpman series—来自 Linux 文档项目的手册页。同样，此软件包有多种语言。请选择您想要的 ldpman 系列中的语言。
- libcinfo—GNU C 库和 GDBM 库的 Info 文件。您仅在要开发 Linux 应用程序时才需要此文档。
- lx_docu—内核文档。您仅在要修改内核时才需要此文档。祝好运！
- man9—来自第 9 节的一些手册页。
- manyfaqs—常见问题解答集。
- odshtm1—来自 Offenes Deutsches Schulnetz 的 HTML 页面。
- perlref—Perl 5 参考指南。您仅在要开发 Perl 脚本时才需要此文档。
- ppp_nt—Linux 连接到 Windows NT。
- pyth_doc—Python 文档（HTML）。
- rfc—RFC（评论请求）。
- sdb—SuSE 支持数据库。您必须与以下其中一个软件包一起安装此软件包才能运行 SuSE 支持数据库，其中包含大量关于如何在 SuSE Linux 上配置和排除故障的信息：
- sdb_xx—sdb 的语言。您必须安装至少一种语言才能使 SuSE 支持数据库正常运行。
- susehelp—SuSE 帮助系统（基础）。
- suse1xen—SuSE Linux 手册（英文）。这是随 SuSE Linux 完整发行版提供的 SuSE Linux 手册。它也有其他语言版本。
- susepakxx—SuSE 帮助系统。您必须以其中一种可用语言安装此软件包才能运行您的 SuSE 帮助系统。帮助系统有英文、德文和法文版本。
- uucpdoc—Taylor UUCP 文档。
- xe_info—X Emacs 的 Info 文件。您仅在要将 X Emacs 用作编辑器时才需要此文档。
- xf86html—来自 XFree86 的 HTML 页面。

Series n：

- Apache—Apache Web 服务器。SuSE 支持数据库系统要求您运行一个 Web 服务器以在支持数据库中搜索关键词。

### 章节逐章导读

本节按章节指导您如何找到本书各章中讨论的软件的正确文档。本节提到的大部分文档随 SuSE Linux 提供。

以下各节中列出的每个软件包都有自己的文档位于 /usr/doc/packages/<package name> 目录中。您可以在此目录中阅读文件，以及章节逐章列表中每个条目旁边的列表。

#### 第 1 章，“预安装 SuSE Linux”

- FIPS—文档位于第一个 SuSE Linux CD 上的 FIPS 软件包中，位于 CDROM:/dosutils/fips
- 分区调整器—PResizer 的文档位于随本书提供的 CD 上，位于 CDROM:/extra/presizer
- Power Quest Partition Magic—http://www.powerquest.com

#### 第 2 章，“安装 SuSE Linux”

- SuSE Linux 手册

#### 第 3 章，“安装 X Window 系统”

- XFree86-HOWTO
- XFree86-Video-Timings-HOWTO
- XWindow-User-HOWTO
- XFree86 网站 http://www.xfree86.org
- X 协会网站 http://www.x.org

#### 第 4 章，“管理用户和组”

- User-Group-HOWTO
- 本章中使用的命令的手册页（bash、passwd 等）
- YaST 文档和帮助页面

#### 第 5 章，“管理文件系统”

- mkfs、mkswap 和 fstab 的各种手册页
- NFS-HOWTO

#### 第 6 章，“备份系统”

- YaST—YaST 手册页。您也可以阅读附录 C，“YaST”
- tar—tar info 页面
- cpio—cpio 手册和 info 页面
- Time Navigator—http://www.quadratic-software.com

#### 第 7 章，“系统升级”

- KDE 网站 http://www.kde.org
- GNOME 网站 http://www.gnome.org
- 软件包中的各种 README 和 INSTALL 文件

#### 第 8 章，“安装新内核”

- Kernel-HOWTO
- 内核文档位于 /usr/src/linux/Documentation
- 内核配置模块中的内核帮助

#### 第 9 章，“配置系统启动序列”

- Linux 文档项目 http://www.linuxdoc.org
- LILO 文档

#### 第 10 章，“声卡配置”

Sound-HOWTO.gz 和 Sound-Playing-HOWTO.gz HOWTO 是很好的信息来源：

- isapnp 工具—isapnp 和 pupdump 手册页。
- pciutils—pciutils 主页 http://atrey.karlin.mff.cuni.cz/~mj/pciutils.html
- OSS—OSS 文档。您还应查看 4Front 网站 http://www.4front.com 获取更多信息
- OSS/Lite—内核文档
- ALSA—http://www.alsa-project.org
- ESD—enlightenment 网站 http://www.enlightenment.org

#### 第 11 章，“打印”

- Printing-HOWTO
- Printing-Usage-HOWTO

#### 第 12 章，“配置外设”

- 内核文档位于 /usr/src/linux/Documentation
- CD-Writing-HOWTO
- Hardware-HOWTO
- PCI-HOWTO
- Fax-Server-HOWTO
- ZIP-Drive-HOWTO

#### 第 13 章，“配置 TCP/IP 网络”

- Firewall-HOWTO
- NET-3-HOWTO
- NET3-4-HOWTO
- Networking-Overview-HOWTO

