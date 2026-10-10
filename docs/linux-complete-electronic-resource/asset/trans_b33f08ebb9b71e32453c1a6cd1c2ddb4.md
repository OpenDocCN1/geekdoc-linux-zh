

## CD-ROM 光驱

许多常见的 CD-ROM 光驱连接到标准 IDE 控制器。CD-ROM 的另一种常见接口是 SCSI。由于 SCSI 支持包括每个设备支持多个逻辑单元，因此您可以使用 CD-ROM 库（磁盘阵列）。此外，还支持一些专有接口，如 NEC CDR-74、Sony CDU-541 和 CDU-51a、Texas Instruments DM-3224 以及 Mitsumi。

Linux 支持 CD-ROM 的标准 ISO 9660 文件系统以及 High Sierra 文件系统扩展。

## 磁带驱动器

如果支持 SCSI 控制器，则支持任何 SCSI 磁带驱动器，包括四分之一英寸、DAT 和 8MM 磁带驱动器。连接至软盘控制器的设备，如软盘磁带驱动器也得到支持，其他一些接口，如 QIC-02，也得到支持。

## 打印机

Linux 支持完整的并行打印机系列。如果 MS-DOS 或其他操作系统能够从并行端口访问您的打印机，那么 Linux 也应该能够访问它。Linux 打印软件包括 Unix 标准的 lp 和 lpr 软件。如果您拥有网络，该软件允许您通过网络进行远程打印。Linux 还包含允许大多数打印机处理 PostScript 文件的软件。

有关具体支持的打印机列表，请参见第 7 章。

## 调制解调器

与打印机支持一样，Linux 支持全系列串行调制解调器，无论是内置式还是外置式。Linux 上可用的电信软件非常多，包括 Kermit、pcomm、minicom 和 seyon。如果您的调制解调器可以在同一台机器上的其他操作系统中访问，那么您应该能够在 Linux 中毫不费力地访问它。

## 以太网卡

Linux 支持许多流行的以太网卡和局域网适配器。Linux 还支持一些 FDDI、帧中继和令牌环卡，以及所有 Arnet 卡。您的发行版内核源代码中包含了受支持网卡的列表。

## Linux 信息源

还可以获取许多其他有关 Linux 的信息来源。特别是，许多关于通用 Unix 的书籍都会很有用，尤其是对不熟悉 Unix 的读者。我们建议您在试图深入探索 Linux 这片“丛林”之前，先浏览一下其中一本书。

在线也可获取电子形式的信息。您必须能够访问 Internet、Usenet 或 FidoNet 等在线网络才能访问这些信息。一个好的起点是 http://MetaLab.unc.edu/LDP/HOWTO/META-FAQ.html。如果您无法上线，您也许能够找到有人愿意为您提供这些文档的纸质复印件。

### 在线文档

许多 Linux 文档可以通过匿名 FTP 从世界各地的 Internet 归档站点以及像 FidoNet 和 CompuServe 这样的网络获取。Linux CD-ROM 发行版也包含此处提到的文档。如果您可以向 Internet 站点发送电子邮件，您可能能够通过电子邮件接收 FTP 站点文档或文件的电子邮件 FTP 服务器之一来检索这些文件。

http://MetaLab.unc.edu/LDP/HOWTO/META-FAQ.html 列出了著名的 Linux 归档站点。为了减少网络流量，您应该使用在地理位置上离您最近的 FTP 站点。

附录 A 包含通过匿名 FTP 可获取的 Linux 文档的部分列表。文件名因站点而异。大多数站点在它们的 Linux 归档的 docs 子目录中保存与 Linux 相关的文档。例如，FTP 站点 MetaLab.unc.edu 将 Linux 文件保存在 `/pub/Linux` 中，而将 Linux 相关文档保存在 `/pub/linux/docs` 中。

可用的在线文档示例：

- Linux 常见问题解答（FAQ），关于 Linux 的常见问题集锦；
- Linux HOWTO 文档，描述系统的具体方面，如安装 HOWTO、打印 HOWTO 和以太网 HOWTO；
- Linux META-FAQ，即 Internet 上的信息源列表。

这些文档中的许多也定期发布在一个或多个与 Linux 相关的 Usenet 新闻组中；请参见下文“Usenet 新闻组”。

### Linux 在万维网上

Linux 文档项目主页位于万维网：http://metalab.unc.edu/LDP/。该网页列出了许多 HTML 格式的 HOWTO 和其他文档，以及指向其他对 Linux 用户感兴趣的站点的指针，如《*Linux Journal*》（一本月刊）。您可以在 http://www.ssc.com/ 找到该杂志。

### 书籍和其他出版作品

Linux 文档项目的书籍是通过 Internet 进行的一项努力的结果，旨在撰写和发行一套正宗的 Linux 手册，它们是商业 Unix 版本附带文档的对应物，涵盖安装、操作、编程、网络和内核开发。

Linux 文档项目手册可以通过匿名 FTP 和邮寄订单获取。http://Metalab.unc.edu/LDP/HOWTO/META-FAQ.html 列出了可获取的手册并说明了获取方法。

许多大型出版商，包括 Sytex、MIS-Press、Digital Press、O'Reilly Associates 和 SAMS，都已加入 Linux 热潮。请查阅计算机书店或 SSC 的网页 http://www.ssc.com/，或者有时在其站点 http://www.linuxjournal.com 上发布的《*Linux Journal*》中的书评。

大量关于通用 Unix 的书籍也适用于 Linux。在使用和编程接口方面，Linux 与其他 Unix 实现没有太大差异。关于使用和编程 Linux 您想要知道的大部分事情都可以在通用 Unix 文本中找到。事实上，这本书旨在补充当前可用的 Unix 书籍库。在这里，我们介绍了最重要的 Linux 特有细节，并希望您能参考其他来源获取更深入的信息。

有了好的 Unix 书籍以及本书，您应该能够处理几乎任何事情。附录 B 列出了几本强烈推荐 Unix 新手和专家阅读的 Unix 书籍。

《*The Linux Journal*》在全球发行，是了解 Linux 社区动态的绝佳方式，尤其如果您无法访问 Usenet 新闻。请访问 http://ssc.com/ 获取订阅《*Linux Journal*》的信息。

### Usenet 新闻组

*Usenet* 是一个全球性的电子新闻和讨论论坛，拥有多样化的 *新闻组*（newsgroups），即专门针对特定主题的讨论区域。许多关于 Linux 开发的讨论都在 Internet 和 Usenet 上进行。不出所料，有许多 Usenet 新闻组专门用于 Linux。

最初的 Linux 新闻组 alt.os.linux 是为了将一些关于 Linux 的讨论从 comp.os.minix 和各种邮件列表转移过来而创建的。很快，alt.os.linux 上的流量变得足够大，以至于在 comp 层级中创建一个新的新闻组是合理的。1992 年 2 月进行了一次投票，并创建了 comp.os.linux。

comp.os.linux 迅速成为 Usenet 小组中最受欢迎（也是最吵闹）的小组之一，比 comp.os 层级中的任何其他小组都更受欢迎。1992 年 12 月，进行了一次投票以拆分该新闻组以减少流量；只有 comp.os.linux.announce 通过了这次投票。1993 年 7 月，该小组最终被拆分到一个新的层级中。近 2,000 人参与了 comp.os.linux 重组的投票，使其成为有史以来规模最大的 Usenet 投票之一。

如果您没有 Usenet，对于下文列出的许多（如果并非全部）新闻组，都有可用的邮件转新闻网关。

- comp.os.linux.answers：用于发布 Linux FAQ、How-To、README 以及其他回答 Linux 相关问题的文档。这将有助于降低其他 c.o.l.* 组的流量，并将 comp.os.linux.announce 留给真正的公告。
- comp.os.linux.announce：一个受调节的新闻组，用于关于 Linux 的公告，包括错误报告和软件的重要补丁。如果您阅读任何 Linux 新闻组，请阅读这一个。通常，该组中的重要帖子不会交叉发布。该组还包含许多关于 Linux 的定期帖子，包括附录 C 中描述的在线文档。

发布到上述新闻组的内容必须得到调节员 Matt Welsh 和 Lars Wirzenius 的批准。如果您想提交一篇文章，只需像往常一样发布该文章；新闻软件会将该文章转发给调节员以获取批准。但是，如果您的新闻系统设置不正确，您可能需要直接将文章发送至 linux-announce@tc.cornell.edu。

- comp.os.linux.development.apps：一个不受调节的新闻组，用于讨论与 Linux 应用程序编写以及将应用程序移植到 Linux 相关的问题和讨论。

