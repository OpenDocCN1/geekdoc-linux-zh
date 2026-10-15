
# 附录

## 参考书目

**Craig Hunt**: *TCP/IP Network Administration*. Sebastopol, Calif., O'Reilly & Associates, Inc. 1991. 这是一本管理 TCP/IP 的标准书籍。它是为 Sun 的 Solaris 操作系统而非 Linux 设计的。很好的参考书籍，特别是对于那些将管理复杂网络的人。

**Olaf Kirch**: *The Linux Network Administrators' Guide*. 该文档针对复杂网络的人士，但其早期章节也涵盖了 TCP/IP 的基础知识。可以在 Web `http://sunsite.nc.edu/LDP` 免费获取。O'Reilly & Associates, Inc. 出版了该版本。

《Linux Bible》，San Jose, Calif., Yggdasil Computing Inc., 1997. 本卷重印了许多免费的 Linux 文档，包括 Olaf Kirch 的《Linux 网络管理员指南》以及关于各种网络主题（包括以太网和串口）的“howtos”。这些文档提供了关于 Linux 下网络的丰富信息。随着本书的进行，我们将为你指向特定的文档，提供所讨论特定主题的详细信息。

Steven Baker 的 *Net worth* 每月在《UNIX Review》杂志上发表。Baker 先生对网络主题有深入的了解，且文笔很好。他在1992年和1993年的专栏讨论了我们在这里提出的许多基础问题。据我们所知，这些专栏还没有以书的形式出版，但你可以在当地大学的图书馆找到它们。以下专栏对初学者特别感兴趣：

- *1992年1月：……的介绍*
- *1992年2月：互联网。*
- *1992年3月：IP 层*
- *1992年4月：IP 地址*
- *1992年5月：……的历史*
- *1992年7月：路由*

欲了解更多关于 InterNIC 的信息——特别是如何提交互联网域名请求——请访问 InterNIC 网站：

```
http://www.internic.net
```

---

## 第 3 章

第 3 章讨论了特定于 Linux 的主题。因此，额外信息的主要来源是描述 Linux 系统本身的文档。这些文档可以从以下网站下载：

```
http://www.linux.org/info/index.html
```

- 若要进一步了解编译 Linux 内核，请查看 Linux Kernel HOWTO。有关正在被编译进内核的任何特定子系统的详细信息，请查看 `/usr/src/linux/Documentation` 目录下的文档。这些文档作为 Linux 内核源代码的标准部分包含。
- 有关网络配置文件的更多信息，请查看文件本身。它们包含了解释内容的注释，并且提供的细节比我们这里提供的要详细得多。
- 有关配置命令 `ifconfig` 和 `route` 信息，请使用 `man` 命令查看它们的帮助页。
- 有关脚本 `rc.inet1` 和 `rc.inet2` 的更多信息，您应该阅读这些文件。它们包含了解释其行为的注释。特别是脚本 `rc.inet2` 将描述它开启了哪些网络功能以及关闭了哪些。
- 有关 `pppd` 的更多信息，请使用 `man` 查看其帮助页。该帮助页还提供了 `ppd` 配置文件的信息。遗憾的是，拨号器上的 `ppp` 脚本特定于您的 Linux 系统和 ISP，因此没有更多可用信息。
- 有关 `dial` 的更多信息，请查看其源代码附的文档。特别是 `dial-examples` 的帮助页对于解释 `dial` 配置文件中相当复杂的语法非常有帮助。

---

## 第 4 章

`ftp`、`ncfftp`、`telnet` 和 `trn` 都是经典的程序，但初学者可的信息并不多。然而，您可能会发现以下内容有所帮助：

- 每个程序的帮助页都有帮助。虽然编写并不总是最清晰，但页面是完整的。使用 `man` 命令查看它们。
- 每个程序都汇编了一份 FAQ（即常见问题解答文档）。大多数 FAQ 被汇总在一起，可以很容易从互联网下载；详细信息请查看网站 `http://www.rfcs.org`。

以下 RFC 也有涉及：

- RFC 959 描述了文件传输协议 (FTP)。这特别有用，因为它定义了 FTP 服务器返回的所有消息。
- RFC 854 描述了 TELNET 协议。
- RFC 977 描述了网络新闻传输协议 (NNTP)。

`lynx` 带有丰富的文档，包括一份完整的教程。如需访问此文档，只需调用 `lynx`，然后按 `h` 显示其帮助屏幕。您可以从该屏幕选择教程，并阅读或打印它。关于 HTML 和 Web 浏览器的主题已经编写了许多书籍。您可能会发现以下信息源有所帮助。

- 超文本传输协议 (HTTP) 定义在 RFC 1945 (版本 1.0) 和 RFC 2068 (版本 1.1) 中。
- 超文本标记语言 (HTML) 由万维网联盟 (W3) 定义并正在不断扩展，该组织包含了计算世界许多最具影响力的组织。欲免费下载定义 HTML 并描述其未来方向的 W3 出版物请查看 URL `http://www.w3.org/WWW/TR`。

---

## 第 5 章

关于 SMTP 的最佳信息来源是 Jonathan B. Postel 编写的 RFC 821 定义。该文档可在 NIC 网站获取；查找文档 STD010。

若要对 UUCP 有良好的总结，您应该查看 Ed Ravin、Tim O'Reilly、Dale Dougherty 和 Grace Todino 写的《Using and Managing UUCP》(Sebastopol, Calif., O'Reilly & Associates, Inc., 1996)。这本书结合了这些作者之前的两本书的内容，即《Using UUCP and Usenet》和《Managing UUCP and Ucenet》，这两本书是 O'Reilly 最初的 Nutshell 系列书籍。它已更新以涵盖 Taylor UUCP。

如果您对通过 UUCP 接收邮件感兴趣，请务必检查您当地的 ISP。据我们所知，有两个 ISP 提供廉价的邮件服务：

- Ripco Communications，芝加哥 (`http://www.ripco.com`)
- Connix Communications，康涅狄格州米德菲尔德 (`http://www.connix.com`)，Connix 还通过 UUCP 提供新闻推送。

关于 `sendmail`，有两本书脱颖而出：

- Bryan Costales 和 Eric Allman 写的《sendmail》，第二版 (Sebastopol, Calif., O'Reilly & Associates, Inc., 1997)。
- Bryan Costales 和 Eric Allman 写的《sendmail Desktop Reference》(Sebastopol, Calif., O'Reilly & Associates, 1997)。

`sendmail Desktop Reference` 的设计旨在让知识丰富的用户快速查询信息。`sendmail` 则更具教程性，旨在引导您进入 `sendmail` 设计和配置的弯折路径。这些书中包含了关于 `sendmail` 的信息，其详细程度令您感到恐惧的存在。如果您必须进行任何复杂的邮件路由，`sendmail` 就是那个程序，而这些就是那些书。

---

## 第 6 章

关于在 Linux 下使用以太网的更多信息，请查看文档：

```
http://sunsite.unc.edu/pub/Linux/docs/HOWTO/Ethernet-HOWTO
```

布线信息来自 1997 年 Siemon 公司目录。可以通过此处获取副本：

```
http://www.siemon.com
```

与布线标准 TIA/EIA 568A 的材料位于：

```
http://www.siemon.com/standard.html
```

在以下位置还有一个关于家庭布线选项的有趣章节：

```
http://www.siemon.com/homecable/homecable.html
```

请注意，这里描述的大部分硬件看起来很好，但价格昂贵。

关于可以传递给内核的参数更多信息，我们记录在：

```
http://sunsite.unc.edu/pub/Linux/docs/HOWTO/Kernel-HOWTO
```

关于如何通过参数将内核传递给 lilo 的良好总结，我们记录在：

```
http://sunsite.unc.edu/pub/Linux/docs/howto/mini/LILO
```

最后，如果您对《查拉图斯特拉》(Also Spach Zarathustra) 感兴趣，我们强烈推荐 1954 年由 Fritz Reiner 和芝加哥交响乐团录制的版本 (RCA Victor 09026-61494-2)，该版本作为 RCA Living Stereo 系列的一部分以 CD 形式发行。这段由 20 世纪伟大指挥家之一演绎的经典表演由 John Pfeiffer 使用原始模拟录音设备为 CD 精心重制。大声播放它吧！

---

## 第 7 章

`inetd`、`ftpd` 和 `telnetd` 由其帮助页描述得很详尽。`inetd` 在 Linux-to-document 中也有讨论；欲下载副本，请访问网站 `http://www.linux.org`。

Apache 带有丰富的 HTML 格式文档。文档与 Apache 源码归包一起；或若要交互式查看文档，请访问网站 `http://www.Apache.org`。

关于我们认为的构建 CGI 脚本和 Java 程序的良好总结，请参见 Fred Butzen 和 Dorothy Forbes 写的《The Linux Database》(New York, MIS:Press, 1997)。其重点是与关系型数据库交互的脚本和程序，但您也可以将其用于普通的脚本和程序。

---

## 附录

欲获取 NFS 及其他网络资源共享系统的彻底描述，我们推荐 Michael Saltifaller 的《TCP/IP and NFS: Internetworking in a UNIX Environment》(Reading, Mass., Addison-Wesley Publishing Co., 1991)。

关于 Linux 下打印的信息，请查看最佳信息来源 Linux printing how-to。同样可通过 URL `http://www.linux.org` 获取。

关于 X Windows 系统出版了许多书籍。我们有两本特别有帮助：

- Neil Mansfield 写的《The Joy of X》(Reading, Mass., Addison-Wesley Publishing Co., 1993)。在解释 X Windows 系统复杂的架构方面做得非常好。
- Ellie Cutler、Daniel Gilly 和 Tim O'Reilly 写的《X Window System in a Nutshell》(Sebastopol, Calif., O'Reilly & Associates, Inc., 1992)。这是一本关于 X Windows 系统、其命令和库调用的优秀手册和参考书（如果您有 X 编程的冲动）。

最后，如果您对常用计算机术语的详尽且博学（通常幽默）的定义感兴趣，请参 Stan Kelly-Boot 写的第二版《The Computer Contradiction》(Cambridge, Mass., The MIT Press, 1995)。强烈推荐。

---

## 附录 B：参考文献

关于防火墙的更多信息，我们建议您特别阅读两个手册：

- `ipfwd` 手册页对什么是防火墙及其工作原理进行了良好的通用讨论。
- `ipfwadm` 命令的手册页概述了该命令，并详细介绍了如何配置和调优防火墙。

关于 SOCKS，最好的信息来源是与软件包随带的文档。您可以从 SOCKS 章节中提到的互联网网站下载这些文档。

关于本章中简要提到的安全外壳 `ssh`，请参阅 William Lefebvre 的文章《The Secure Shell》，该文章发表在 1997 年 9 月份的 *UNIX Review*。这篇文章对 `ssh` 进行了良好的总结，并让您了解它在内网中是如何工作的。

最后，为了对 DNS 和 bind 进行深入讨论，我们推荐 Paul Albitz 和 Cricket Liu 著的《DNS and bind》（加州塞巴斯托波，O'Reilly & Associates, Inc., 1996），现已出版第二版。这是一本典型的 O'Reilly 作品：可读性强、组织良好且内容详尽。

---

## 第 9 章

关于 Windows 95 的书籍已经有很多。其中一些值得一读。对于普通大众来说，可能最有帮助的书是 Andy Rathbone 的《Windows 95 for Dummies》（加州福斯特特市，IDG Books Worldwide, 1995）。不要被标题误骗了——Linux 用户不是“傻瓜”，但这本书是对 Windows 95 及其迷宫般的通道的极佳介绍，特别是对于那些将使用你内网的 Windows 95 用户来说，将非常有帮助。

关于 NetBIOS 和 SMB 协议的良好介绍，请参见 Steven Baker 的文章《Serve up Microsoft networking on UNIX》（*UNIX Review*），1997年8月，第 15-22页。

微软在支持和扩展 SMB 协议方面投入了大量。关于微软对 SMB 的观点，请访问：

```
ftp://ftp.microsoft.com/developer/drg/SMB.TXT
```

两个 RFC 描述了 NetBIOS 和 TCP/IP 之间的交互：

- RFC 1001 描述了如何将 NetBIOS 封装在 TCP/IP 中。
- RFC 1002 描述了 NetBIOS 命名规范。它还描述了 NetBIOS 名称服务器的结构（微软称为 WINS）。

关于 Samba 的更多信息，请参考以下 URL：

- `http://samba.anu.edu.au` - Samba 首页
- `http://samba.anu.edu.au/cifs/docs/what-is-smb.html` - Richard Sharpe 的 SMB 入门。该页面还提供了指向互联网上其他 SMB 相关资源的链接。
- `http://samba.anu.edu.au/samba/docs/faq/sambafaq.html` - Samba FAQ。该文档的副本包含在 Samba 源码中，但它一直在不断扩展和修订。如果你在运行 Samba 时遇到问题，第一步应该是获取此 FAQ 的最新副本。

最后，关于 Windows 命令 `NET` 的更多信息，请参阅 Tom Yager 的文章《Taming command Windows, part II》（*UNIX Review*，1997年11月，第 33-42页）。作者讨论了它在现实世界场景中的用法，特别是作为集成 UNIX 和 Windows NT 的辅助；但他的大部分讨论适用于 Windows 95。

---

## 第 10 章

关于加密技术的著作已经有很多。一个信息来源是国家安全局（NSA）的网站，地址为 `http://www.nsa.gov`。NSA 是负责电子情报的极秘密机构。该网站包含了对冷战密码学方面的一些迷人的描述。

密码学历史本身就是一个迷人的故事。关于这段历史，我们热烈推荐 David Kahn 著的《The Codebreakers》（纽约，Macmillan, 1967）。这本书结束于计算机加密时代的开始，但它对加密和破译的人类故事描述得非常精彩，特别是美国海军的“魔法”（Magic）项目（该项目破解了日本的外交和海军密码），以及英国 Ultra 小组破解了德国的“恩尼”（Enigma）密码，这对盟军在第二次世界大战中的胜利起到了关键性作用。

关于 PPG 软件包的详细描述，请参 Simpson Garfinkel 著的《PGP》（加州塞巴斯托波，O'Reilly & Associates, 1995）。

关于安全的 `ssh` 的更多信息，请参阅 William Lefebvre 发表在 1997 年 9 月份 *UNIX Review* 上的《The Secure Shell》。这篇文章对 `ssh` 进行了良好的总结，并让您了解如何在您的内网中使用它。

关于安全和防火墙的信息，我们推荐两本书：由 Simpson Garfinkel 和 Gene Spaff 著的《Practical Unix and Internet Security》（加州塞巴斯托波，O'Reilly & Associates, 1996），以及 D. Brent Chapman 和 Elizabeth D. Zwicky 著的《Building Internet Firewalls》（加州塞巴斯托波，O'Reilly & Associates, 1995）。这两本书都包含了许多关于
