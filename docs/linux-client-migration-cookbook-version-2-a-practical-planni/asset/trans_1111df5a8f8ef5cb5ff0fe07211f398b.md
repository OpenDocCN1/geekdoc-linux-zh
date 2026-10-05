

![](img/23b949da14ff7bab8762f0f0361af394_255_0.png)

# 管理员

打印机 1 已成功添加。

> Copyright 1993-2002 Easy Software Products, All Rights Reserved. The Common UNIX Printing System, CUPS and the CUPS logo 是 Easy Software Products 的商标。所有其他商标均为其各自所有者的财产。

图 9-9 CUPS Web 界面打印机添加成功消息

- 9. 您已将打印机添加到 CUPS。请参见第 229 页图 9-10。

![](img/23b949da14ff7bab8762f0f0361af394_256_0.png)

# 打印机

默认目标：printer1

| printer1 | HP LaserJet 系列 CUPSPS v1.1 |
| --- | --- |
| 说明：AD6380 服务器域上的测试打印机 | 位置：虚拟打印机 |
| 打印机状态：空闲，接受作业。 | 设备 URI：smb://smb3lab26/printer1 |

- 打印测试页 | 停止打印机 | 拒绝作业 | 修改打印机
- 配置打印机 | 删除打印机

Copyright 1993-2002 Easy Software Products, All Rights Reserved. The Common UNIX Printing System, CUPS and the CUPS logos 是 Easy Software Products 的商标。所有其他商标均为其各自所有者的财产

**图 9-10** 带有 printer1 的 CUPS Web 界面管理打印机页面

本节中的截图是使用连接到域控制器 smb3lab26 的 Active Directory 域 AD6380 的 Red Hat 桌面客户端创建的。

要测试您使用 **lpadmin** 或 Web 界面添加的打印机，只需打印一个文件，或使用 Web 界面上的“打印测试页”按钮。

> **重要：** 在创建打印机过程中使用用户名和密码会将您的密码暴露在 CUPS 定义文件中。最好使用特殊的打印机用户，或让打印机共享对所有人可用。

第 9 章 集成指南 229 页

# 第 4 部分

# 附录

在本书的第 4 部分中，包含了：

- 附录 A，“233 页：Windows 用户的 Linux 术汇表”
- 附录 B，“255 页：使用企业管理工具”
- 附录 G，“329 页：应用程序移植”
- 附录 F，“321 页：桌面自动化与脚本”
- 附录 E，“313 页：客户端个性化”
- 附录 C，“277 页：使用 Versora Progression Desktop 自动化桌面迁移”
- 附录 D，“289 页：使用 Useful Desktop Multiplier 深度多站计算”

![](img/23b949da14ff7bab8762f0f0361af394_260_0.png)

# Windows 用户的 Linux 术汇表

本附录描述了基础术语。
在本附录中，我们讨论了以下主题：

- 234 页“这一切意味着什么”
- 234 页“常见 Linux 术语”

# 这意味着什么

对于初次涉足 Linux 世界的 Microsoft Windows 用户来说，有很多新术语需要学习。本词表简要解释了 Linux 产品中常见的许多术语、缩写和简称的意义和重要性。（其中某些术语并非 Linux 特有，但对许多 Windows 用户来说可能仍然是全新的。）此文档应有助于减少围绕 Linux 的困惑；然而，大多数常见的硬件、软件和通信术语未包含在此，因为它们在其他地方很容易找到。

> 注意：为了保持定义简洁，某些内容可能会被过度简化。它们并非为了提供深度教程，而是为了给新用户提供通用的解释。

如果您找不到要找的单词，还有许多其他来源可以供选择的缩写、简称和通用计算机术语（并非特定于 Linux）。由于某些术语可能出现在一个字典中而在另一个字典中不出现，而且某些定义在一个来源中比另一个更清晰或更全面，以下是按字母顺序排列的选择：

- 计算机在线字典 http://wombat.doc.ic.ac.uk/foldoc/foldoc.cgi?Free+On-line+Dictionary
- IBM 术语网站 http://www-306.ibm.com/software/globalization/terminology/
- Lucent 技术术汇表 http://www.lucent.com/search/glossary
- TechWeb 技术百科书 http://www.techweb.com/encyclopedia
- Ugeek 技术术汇表 http://www.geek.com/glossary/glossary.htm
- Whatis.com http://www.whatis.com

# 常见 Linux 术语

账户名称（Account Name）与登录 ID、用户 ID 或用户名相同。分配给 Linux 系统用户的名称。系统上可以设置具有唯一账户名的多个用户，每个用户具有不同的访问（权限）级别。安装 Linux 后，账户名由超级用户（Superuser）或 root 操作员分配。

# ACPI（高级配置和电源接口）

高级配置和电源接口在 x86 平台上提供了电源管理功能。

# ALSA（高级 Linux 音效）

用于访问声卡和其他设备的框架。ALSA 包括对大多数音频芯片和适配器的支持。

# APM（高级电源管理）

一种行业标准，允许系统处理器和各种组件进入节电模式，包括挂起、睡眠和关闭。APM 对于移动设备尤为重要，因为它可以节省电量。

# 存档（Archive）

一个包含多个文件的文件，通常经过压缩以节省空间。流行的存档格式包括 ar、zip。

# Awk（由 Aho, Weiner 和 Kernigh 分 开发）

一种以模式匹配语法实用的编程语言，通常用于数据检索和转换。其 版本称为 Gawk。

# 后台进程（Background Process）

在没有用户输入的情况下运行的程序。在 Linux 等多任务系统中，当用户与前景交互时，可以运行后台进程。某些后台进程（例如守护进程）不需要输入。

# Bash（Bourne Shell）

Bourne Shell 的增强版本。（另等参见 Korn Shell。）

# BDF 字体

用于 X Window系统的位图字体。（另等参见 PostScript 字体和 TrueType 字体。）

# Bin

包含可执行程序的目录。

# 二进制文件（Binaries）

已编译成可执行程序的源代码。在 Linux 世界中，某些软件仅以源码发行；其他包包含源码和二进制文件；另一些仅以二进制格式发行。

# 启动盘（Boot Disk）

包含操作系统（如 Linux）的磁盘（软盘或光盘），用于启动计算机并从命令行运行基本程序。如果系统变得无法启动，这可能是必要的。启动盘可用于分区和格式化硬盘、恢复主引导记录或复制特定文件等。

# 引导加载程序（Bootloader）

处理计算机初始启动的应用程序。引导加载程序设置初始环境，然后将过程交给选定的系统。（另等参见 GRUB 和 LILO。）

# Bot（机器人）

Robot 的缩写。一种旨在极少人工干预的情况下搜索互联网信息的程序。

# Bourne Shell

一种流行的命令行 Shell，比 DOS 命令提示符有许多优势。（另等参见 Bash 和 Korn Shell。）

# BSD（Berkeley软件发行版）

来自加州伯克利分校的 UNIX 发版。（另等参见 FreeBSD。）

# Bzip2

一种新的 Linux 文件压缩程序，提供的体积比 Gzip 小。文件扩展名通常为 .bz2。

# CGI（通用网关接口）

用于 Web 服务器在页面和应用程序之间传输数据并将数据返回 Web页面或浏览器。CGI 脚本通常使用 Perl 语言创建，并生成动态 Web 内容（包括电子商务购物篮、小组和调查问卷）。

# CHS（柱面/头部/扇区）

FDISK 在分区期间所需的磁盘信息。

# 客户端（Client）

从服务器请求服务（例如电子邮件）的机器。

