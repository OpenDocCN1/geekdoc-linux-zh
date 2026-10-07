

## 第 25 章 办公效率应用

![](img/446debe023486a07fde575245cf7a3ff_871_0.png)

图 25.17 KDE 词典位于“辅助工具”（Accessories）菜单下，也可以方便地从 KDE 面板小部件中调用。

在“附加组件”（Extras）菜单下，有许多实用的应用程序，包括以下：

- * AddressBook（地址簿）应用程序
- Kandy 应用程序，它可以将您的地址簿同步到手机手机中
- KArm，一个闹钟应用程序，以及 KTimer，一个秒表程序
- KNote，一个黄色的“便签条”，以及 Kijots，一个轻巧、组织良好的笔记工具，对于在看书或听讲座时记录笔记非常有用
- GnuCash 个人财务管理器
- KTouch 盲打字辅导程序
- KVocTrain 词汇构建应用程序

“附加组件”菜单还包括其他编程环境、图形查看器以及数十种其他应用程序（包括游戏）。你应该花些时间浏览“附加组件”菜单，并尝试你在那里发现的一些效率（以及非效率）工具。

## 展望开源办公软件

Mark Davis 是弗吉尼亚亚州诺福克的 Lake Taylor 渡性护理医院（LTH）（http://www.laketlor.org）的信息系统总监，他最近将该机构从使用 SCO UNIX 切换到了 Linux。

由于 LTH 使用的是薄客户端拓扑结构，所有应用程序都从位于整个设施的中心提供，因此必须对网络带宽问题给予特别关注。虽然他们意识到在没有开源替代方案时将使用商业应用程序，但他们对那些强调非专有、开放标准的应用程序给予了最高考虑。使用开源应用程序让 Davis 能够编辑源代码并根据 LTH 的需求对应用程序进行定制。非专有的、开放标准的则则允许将应用程序轻松地集成到整个系统中。

一种常见的修改是移除那些代表安全隐患的功能（例如访问命令提示符或不需要的功能），并减少网络带宽（例如移除动画图标和启动屏幕）。

随着新 Linux 系统的部署，LTH 的员工开始了一项工作，这项工作涵盖了现代业务所需的所有效率应用。总拥有成本（TCO）显著降低，系统的稳定性与 LTH 使用商业版 SW UNIX 时相当甚至更高。

此外，LTH 使用的开源应用程序包括 Mozilla、Dillo、HylaFax、OpenOffice、Seynon、Seypled-clayed、IceWM、GIMP、Apache、Postfix、Gnumeric、J-Pilot、Quanta、Webal、dclit 和 vnc。LTH 使用了许多商业应用程序，包括 Retail、Netscape、Word、FoxBase、Merge、Application、Gerimenu、Context Codelink、Monette Ultrracare、Kronos Time Keep Center 和 AIS Xess。因为现在使用一台运行 Microsoft Windows 的单机（经过修改以限制安全问题）通过 VNC 来运行应用程序。（请参阅第 27 章“在 Red Hot Linux 中使用模拟器和其他跨平台工具”获取更多关于 VNC 的信息。）

## 为 Microsoft Windows 编写的效率应用

Microsoft Windows 与 Linux 有本质上的不同，但你可以通过 Red Hat 提供的名为 Wine 的应用程序在 Linux 中安装并运行某些 Windows 应用程序。Wine 允许你在基于 UNIX 的系统上使用 Microsoft Windows 和 DOS 程序。Wine 包含一个可以执行 Windows 二进制文件的程序加载器，以及一个实现 Windows 命令调用的 .dll 库，该库使用相应的 UNIX 和 X11 命令调用。要了解更多关于 Wine 以及在 Red Hot Linux 中处理 Microsoft Windows 应用程序的其他工具，请参阅第 27 章。

要检查你喜欢的应用程序是否受 Wine 支持，可以查看 Wine 数据库：http://appdb.winehq.org/appbrowse.php。

## 第 25 章 办公效率应用

## 相关 Red Hat Linux 命令

以下命令让你能够访问 Red Hat Linux 中的效率应用、工具和进程：

- fax—一个 fax 程序
- gimp—图形图像编辑器
- koshell—KOffice 套件
- kspread—KDE 的 KSpread 表格
- oword—OpenOffice 的文字处理器
- gnumeric—电子表格编辑器
- mrproject—项目管理客户端
- abiword—GNOME 的文字处理器
- pilot—xfer—文件传输工具

## 参考文献

- http://www.openoffice.org—OpenOffice 套件的主页。
- http://www.pclinonline.com/modules.php?name=News&file=sid=3199—关于 OpenOffice.org 的技巧、技巧和增强链接集合。该网站中的一个链接是关于如何将 OpenOffice.org 作为数据库前端的 PDF 文件。
- http://www.gnome.org/gnome-office/—GNOME 网站。
- http://www.koffice.org—KOffice 网站。
- http://en.hancom.com/—Hancom。
- http://www.sun.com/software/staroffice/6.0/—StarOffice 6.0 网站。
- ftp://http.corel.com/pub/linux/Office2000/updates/installscript/**用于在 Red Hat Linux 及其他发行版中安装 Corel Office 2000 套件的脚本。或者你可以尝试 http://linux.corel.com/products/wpo2000_linux/index.html。
- http://bulldog.tzo.org/webcal/webcal.html—基于 WebCal 日历和日程程序的主页。
- http://www.horde.org/projects.php—Horde 项目主页。
- http://quanta.sourceforge.org—KDE 的 Quantum Plus Web 开发工具。
- http://www.kronos.com/discover/prod_serv/tkc.htm—基于 Linux 的时间记录系统，支持开放标准且比竞争产品更有性价比。
- http://www.hamrick.com/vsm.html—VueScan 商业扫描应用程序，支持比 SANE 软件更广泛的扫描仪。

## 第 26 章

## 多媒体应用

## 本章内容

- 在 Red Hat Linux 中刻录
- 声音与音乐
- 观看电视和视频
- 在 Red Hat Linux 中使用相机
- 在 Red Hat Linux 中使用扫描仪
- 图形处理
- 参考文献

本章提供了多媒体内容的概述，包括音频和视频。随着新 Linux 系统的部署，你将学习如何创建和处理图形。

## 在 Red Hat Linux 中刻录

刻录（或创建）自己的 CD 是 Linux 爱好者的基本技能。由于多媒体文件越来越大，CD（以及 DVD）已成为媒体内容的标准媒介。（即使是压缩音频，单个歌曲通常需要几兆字节的存储空间。）可以使用 CD 来：

- 记录和存储媒体数据、备份文件、图形图像和音乐
- 从音乐 CD 中提取音频轨道（刻录是指从自己的 CD 中提取音乐轨道并供个人使用刻制自己的 CD）

