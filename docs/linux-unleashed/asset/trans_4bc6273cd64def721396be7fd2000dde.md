
## 杂项演示程序和实用工具

以下程序可能会让你感兴趣。如果你是个狼人，**月球相位**（Phase of the Moon）将特别有用！

### 凯撒密码（Caesar）

在命令行输入**caesar**。该程序尝试解密编码后的单词。输入`man caesar`可查看 man 手册页。

### 幸运饼干（Fortune）

在命令行输入*fortune*，以获取你的 Linux 幸运饼干信息。

### 数字（Number）

在命令行输入*number* <*number*>。将作为参数< *number*> 给出的阿拉伯数字（例如，41）转换为等价的英文（forty-one）。

### 月球相位（Phase of the Moon）

在命令提示符处输入*pom*。该程序会告诉你当前月亮的相位。正如 man 手册页所述，这在预测他人的行为（也许也包括你自己）时非常有用！输入`man pom`可查看 man 手册页。

### 雨（Rain）

在命令提示符处输入*rain*。你的屏幕会变得像暴雨中的水坑一样泛起涟漪。在大多数 Linux 控制台屏幕上，该程序运行速度太快，甚至看起来都不怎么像真的。按 Ctrl+C 退出。

### 蠕虫（Worms）

在命令提示符处输入*worms*（不要与上面的*worm*程序混淆）。这会在你的屏幕上布满蠕动的小虫。与*rain*一样，该程序在 Linux 控制台屏幕上的运行速度也过快。输入`man worms`可查看其 man 手册页。

### 摘要

现在你应该能够坐在机器前玩你最喜欢的游戏来消磨时间了。如果你还没有安装 X 系统，也许这是一个额外的激励！本章会引导你回到之前你可能没有阅读过的一些章节。

-   要安装 X 系统，请阅读第 22 章，“安装和配置 XFree86。”
-   要使用几种编程语言编写你自己的游戏，请参阅第五部分，从第 25 章“gawk”开始。
-   要备份你的系统以免丢失高分记录，请参阅第 45 章，“备份。”

## Adabas-D 及其他数据库

作者：Tim Parker

### 本章内容

-   dBASE 兼容数据库 986
-   dbMan 993
-   Adabas-D 994
-   LINCKS 997
-   其他数据库产品 997

本章介绍了一些 Linux 的常见数据库应用程序。本章主要关注的这些应用程序是 Adabas-D、FlagShip 和 dbMan V。我们还简要介绍了 LINCKS，这是一个免费的 Linux 面向对象数据库管理系统（DBMS）。

### dBASE 兼容数据库

大约十年前，只有一个数据库系统被广泛使用，即 Ashton-Tate 的 dBASE。在 Windows 出现之前，DOS 下的几乎所有数据库都是基于 dBASE 编写的，随着 UNIX 在小平台上的发展，dBASE 系统的移植版本也出现在那里。尽管 dBASE 软件包的拥有权多次易主，但基于 Windows 的版本出现得不够快（或不够稳定）来维持 dBASE 系统的流行度。很快，其他数据库开始取代 dBASE。

随着更快、更强大版本的 dBASE 的发展，几家公司推出了兼容产品，扩展了 dBASE 语言的功能。这些按照 dBASE 语言集编写的产品通常被称为 xBase，以显示其与 dBASE 的联系。其中几个 xBase 系统受到了编程人员的极大欢迎，特别是 Clipper，这是一个与 dBASE 兼容的语言编译器，它极大地加速了 dBASE 应用程序的执行速度。

虽然许多编程人员现在将 dBASE 视为一种复古的数据库系统，但仍然有成千上万（甚至可能数百万）的应用程序是使用该关系数据库软件包编写的。其中许多软件包至今仍在使用，要么保持最初开发的确切格式，要么移植到较新的 xBase 版本和较新的操作系统。由于 xBase 语言和应用永远消失的可能性很小，因此 Linux 上引入了 xBase 移植版也就不足为奇了。

提供 FlagShip（dBASE 和 Clipper 兼容的数据库系统）的公司为许多操作系统（主要基于 UNIX）提供版本。他们的 Linux 版本是商业产品，在美国售价约为 199 美元。但是，有几个版本的 FlagShip 演示版可用，这些演示版在十天或三十天后过期，允许你查看现有的 dBASE 或 Clipper 应用程序是否能在 Linux 下运行。如果可以并且你想迁移它们，然后你可以购买完整的 FlagShip 副本。

### 什么是 xBase？

xBase 是对最初 dBASE 编程语言实现的通用术语。该数据库 DOS 版本中的主要玩家有 FoxPro（现归微软所有）、dBASE V（现归 Borland 所有）和 Clipper（归 Computer Associates 所有）。

xBase 是一种包含通常出现在编程语言中的语句的语言，例如 IF、ELSE、ENDIF 和 WHILE。编程语言结构专为访问数据库中的记录而设计，而非通用编程。例如，xBase 中的 GOTO 语句指的是数据库中的一个记录，而不是程序代码中的位置。xBase 拥有一些强大的语句用于处理文件以及从表单和屏幕获取数据。

此外，使用 xBase 建立文件之间的关系非常容易。文件中所有字段的名称、类型和长度都记录在文件头中。可以在不更改使用该文件的程序的情况下向文件中添加新字段。此方案允许不同的、互不相关的程序都以各自的方式访问数据库文件，并且都使用文件头中的字段。

xBase 数据库的三大制造商在很大程度上忽略了 Linux 作为其产品平台。我们在 Linux 上拥有的是 FlagShip 和 dbMan（来自 Versasoft Corporation）。这两款产品都运行在多个 UNIX 实现上。

比较这两款产品就像比较苹果和橙子。FlagShip 以 Clipper 版本 5 为模型。dbMan 软件包类似于 dBASE III+ 或 FoxPlus。与 Clipper 一样，FlagShip 是一个编译器。dbMan 主要是一个解释器，尽管可以“编译”dbMan 程序。FlagShip 也是一种面向对象的语言，这使得它在哲学上与 dbMan 以及 FoxPro 和 dBASE 不同。Clipper 和 FlagShip 具有几个类似 C 的特性。实际上，对于 Linux 用户来说，这种相似性是一个加分项。

两者的目标市场也不同。dbMan 主要面向个人用户。如果你想要一个可以在桌面上运行的程序来跟踪向客户计费的工时，或者维护客户电话列表或销售记录，dbMan 可以完成这项任务。

相比之下，对于简单的数据库操作（如邮件列表或客户跟踪列表），FlagShip 可能有些杀鸡用牛刀，换句话说，它不适合休闲用户而非程序员。这并不意味着你不能将其用于简单应用，但你可能需要学习一点编程才能真正使用 FlagShip 的强大功能。FlagShip 更现实的目标是想要开发或移植软件包的人。传统上，dBASE 文件始终有独立的数据文件（.DBF）和索引文件。数据文件的格式对于所有 xBase 来说基本是统一的。很难找到两个使用相同索引文件格式的产品，但你可以使用相同的 .DBF 文件配合 FlagShip 和 dbMan。

### 什么是 FlagShip？

FlagShip 是一个编译器，这意味着它生成可执行代码，没有中间的伪代码。FlagShip 没有解释版本，因此你可能需要像 FoxPro 或 dBASE 这样的解释器来开发复杂的应用程序。FlagShip 旨在让现有的 xBase 应用程序无需修改（或在某些情况下进行最少修改以纠正文件名问题）即可在 Linux 和其他 UNIX 版本下运行。不收取运行时或用户版税，因此一旦应用程序开发和编译完成，它就可以在任何地方分发，无需向作者支付版税。

> 许多网站允许你下载 FlagShip 演示版，你可以像 AltaVista (http://www.altavista.digital.com) 或 Yahoo! (http://www.yahoo.com) 这样的搜索引擎找到它们，或者直接通过 FlagShip 的供应商 Multisoft Datentechnik GmbH 在 http://www.fship.com 获取。该公司还有一个 FTP 服务器，位于 ftp://fship.com/pub/multisoft。演示版相当大（约 4.5MB）。可以从 FTP 和网站获取 FlagShip 的多份文档。请确保下载英文文件，因为大多数网站都提供英文和德文文档（Multisoft Datentechnik GmbH 总部位于德国）。

FlagShip 与 dBASE 和 Clipper 完全兼容，以及与大多数其他 xBase 版本兼容，例如 Fox、FoxPlus、FoxPro、dbMan、QuickSilver 等。它包含了 xBase 兼容程序的所有真正不错的特性，例如：

-   宏支持
-   数组、对象和代码块
-   用户定义函数和用户定义命令
-   索引和数组排序
-   与大多数 xBase 文件格式兼容，包括 .dbf、.dbt、.mem、.lbl、.frm 和 .fmt
-   用于在一个应用程序中将 C 代码和 FlagShip 代码接口的 C API

FlagShip 没有 dBASE 点提示符或交互式命令界面的等效物，这是其他 xBase 产品中常见的功能。但是，有一个名为 dbu 的公共领域程序，它提供了创建文件和索引、添加、修改或定位记录以及交互式浏览文件的功能。

