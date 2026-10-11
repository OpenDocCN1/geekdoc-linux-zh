
# 《Linux 全合一指南 新手入门手册》

![](img/11709a8f88c8cd03868a929dc94c0e2b_3_0.png)

## 作者简介

**Naba Barkakati** 是一位电气工程师，也是一位成功的计算机书籍作者，在从 MS-DOS 和 Windows 到 UNIX 和 Linux 的多种系统中拥有丰富的经验。1984年，他从马里兰大学学院分校（College Park）获得电气工程博士学位后，购买了人生第一台个人电脑——IBM PC-AT。在从事全职工程工作的同时，Naba 梦想为新兴的 PC 软件市场编写软件。幸运的是，他没有像微软那样建立软件帝国，而是最终撰写了成功的计算机书籍。目前，Naba 是美国政府问责办公室（GAO）技术与工程中心的资深技术员。

过去15年里，Naba 撰写了超过25本计算机书籍，主题涵盖从 C++ Windows 编程到 Linux。他著有多部畅销书，如《The Waite Group's Turbo C++ Bible》（威特团 Turbo C++ 圣经）、《Object-Oriented Programming in C++》（C++ 面向对象编程）、《X Window System Programming》（X 窗口系统编程）、《Visual C++ Developer's Guide》（Visual C++ 开发者指南）、《Borland C++ 4 Developer's Guide》（Borland C++ 4 开发者指南）和《Linux Secrets》（Linux 内幕）。他的书被翻译成多种语言，包括西班牙语、法语、波兰语、希腊语、意大利语、中文、日语和韩语。Naba 最新的书是《Red Hat Fedora Linux Secrets》（红帽 Fedora Linux 内幕），同样由威立出版社，股份有限公司出版。

Naba 与妻子 Leha 以及女儿 Ivy、Emily 和 Ashley 住在美国马里兰州的北波托马克（North Potomac）。

## 献词

我想将这本书献给我的妻子 Leha，以及我的女儿 Ivy、Emily 和 Ashley。

## 作者致谢

我要感谢 Terri Varveris 让我启动了这本书——这是一套关于 Linux 的八本快速参考指南，重点介绍了几个主要的 Linux 发行版。作为项目编辑，Christopher Morris 指导我完成了手稿提交流程，并推动各项工作进展。我很感激 Terri 和 Chris 在这个项目中给予我的指导和支持。

我要感谢 Jason Luster 审阅手稿的技术准确性，并提出了许多改进书籍内容的有用建议。

感谢威立出版社的所有人，将我的初稿手稿变成了这本编辑精良、包装精美的书籍。

当然，如果没有 Linux，这本书就没有存在的理由。为此，我们要感谢 Linus Torvalds 和全球无数的 Linux 开发者。最后，一如既往，我最大的感谢献给我的妻子 Leha 和我们的女儿 Ivy、Emily 和 Ashley——是她们对我的爱和支持让我继续前行。谢谢你们一直在那里！

## 出版方致谢

我们为这本书感到自豪；请通过我们在 www.dummies.com/register/ 的在线注册表单向我们发送您的评论。

帮助推出这本书的一些人包括：

### 获取、编辑和媒体开发

- **项目编辑：** Christopher Morris
- **获取编辑：** Terri Varrvers
- **校对编辑：** Heidi Unger
- **技术编辑：** Dan DiNicolo
- **编辑经理：** Kevan Kirschner
- **版权编辑：** Laura Moss
- **媒体开发专员：** Travis Silvers
- **媒体开发经理：** Laura VanWinkle
- **媒体开发主管：** Richard Graves
- **编辑助理：** Amanda Foxworth
- **漫画：** Rich Tennant (www.the5thwave.com)

### 排版服务

- **项目协调员：** Erin Smith
- **版式和图形：** Andrea Dahl, Denny Hager, Melanee Prendergast, Heather Ryan, Erin Zeltner
- **校对人员：** Vicki Broyles, Joe Niesen
- **索引编制者：** Johnna VanHoose

### 技术类“新手版”出版与编辑

- **Richard Swadley**，副总裁兼执行集团出版人
- **Andy Cummins**，副总裁兼出版人
- **Mary Bednarek**，执行获取总监
- **Mary C. Corder**，编辑总监

### 消费者类“新手版”出版

- **Diane Graves Steele**，副总裁兼出版人
- **Joyce Pepple**，获取总监

### 排版服务

- **Jerry Fahey**，生产服务副总裁
- **Debbie Stalley**，排版服务总监

## 引言

当你考虑到 Linux 的起源及其持续演化的方式时，它确实令人惊叹。从作为芬兰人 **Linus Torvalds** 的业余爱好这一谦逊起点开始，Linux 已发展成为一个成熟的操作系统，其特性可与任何商业 UNIX 操作系统相媲美。更棒的是，Linux——包括其所有源代码——对任何人都是免费提供的。你只需要从互联网站点下载它，或者以象征性的费用从众多 Linux CD 供应商那里通过 CD 或 DVD 获取即可。

Linux 确实打破了“一分钱一分货”的规则。尽管 Linux 是免费的，但在性能、特性和可靠性方面，它绝不起眼。Linux 的健壮性与其开发和更新方式有关。世界各地的许多开发人员协作添加特性。用户持续下载增量版本并在各种系统配置中进行测试。Linux 版本经历的 beta 测试比任何商业软件都严格得多。

自 1994 年 3 月 14 日发布 Linux 内核 1.0 以来，全球 Linux 用户数量呈指数级增长。许多 Linux 发行版——操作系统与应用程序及安装工具的组合——已被开发出来，以简化和使用安装过程。一些 Linux 发行版是商业销售并提供支持的，而许多仍保持免费可用。

与许多免费软件不同，Linux 附带了大量在线信息，涉及为各种 PC 和外围设备安装和配置操作系统等主题。一小部分核心 Linux 用户仅凭在线文档就能熟练有效地使用 Linux。然而，绝大多数用户却带着某种特定目的（例如设置 Web 服务器或学习 Linux）转向 Linux。此外，大量的 Linux 用户在家中使用他们的系统。对于这些新用户来说，在线文档并不易用，且文档通常未涵盖用户可能想到的 Linux 的具体用途。

如果你刚开始使用 Linux，你需要一本实用指南，不仅要指导你完成 Linux 的安装和设置，还要展示如何使用 Linux 完成特定任务，例如设置 Web 服务器或开发软件。你可能还想在最终选定一个喜欢的发行版之前，先尝试不同的 Linux 发行版。

## 关于本书

相应地，《Linux 全方位桌面参考傻瓜书》（*Linux All-in-One Desktop Reference For Dummies*）附带一张 DVD，其中包含七个不同的 Linux 发行版——Debian GNU/Linux 3.1r0、Fedora Core 5、Knoppix 4.0.2、MEPIS 3.3.1、SUSE Linux 10.0、Ubuntu 5.04 以及 Xandros 3.02 公开流通版——以及安装和使用其中任何一个发行版的说明。（*提示：* 你可以直接使用本书 DVD 上的 Knoppix Live CD 来快速、无风险地体验 Linux。）

《Linux 全方位桌面参考傻瓜书》（*Linux All-in-One Desk Reference For Dummies*）在一本书中为你提供了八份不同的快速参考指南。综合起来，这八个小册子提供了关于安装、配置和使用 Linux 的详细信息。

你会最喜欢这本书的一点是，你不必按章节顺序阅读，甚至不必按章节中的部分阅读。你完全可以翻到你想看的话题，快速找到关于 Linux 的紧迫问题的答案，无论是关于使用 OpenOffice.org 文字处理软件还是设置 Apache Web 服务器。

以下是你可以使用这本书做的部分事情：

- 从随书附带的 DVD-ROM 安装和配置 Linux——Debian、Fedora Core、Knoppix、MEPIS、SUSE、Ubuntu 或 Xandros。（你只需从 DVD 启动即可使用 Knoppix。）
- 通过 DSL 或电缆调制解调器将 Linux PC 连接到互联网。
- 使用 PPP 设置拨号网络。
- 在你的现有网络中添加无线以太网。
- 获取针对 Linux 特定用途的技巧、技术和快捷方式，例如：
  - 设置和使用互联网服务：Web、邮件、新闻、FTP、NFS 和 DNS。
  - 使用 Samba 设置 Windows 服务器。
  - 使用 Linux 命令。
