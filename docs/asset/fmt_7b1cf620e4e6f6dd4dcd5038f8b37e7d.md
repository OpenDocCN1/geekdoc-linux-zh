
当你运行 `Configure` 时，可以指定选项，例如指定不同的 Perl 位置或不同的编译器。

Perl 5.0 通过扩展与数据库交互。如果你在系统中安装了这些扩展，只要 `Configure` 能找到头文件和库，就会包含该扩展。再次，你可以告知 `Configure` 文件安装的子目录，如果它们不在 C 编译器搜索的标准目录中。

表 A.2 列出了某些 `Configure` 选项及其影响。要查看完整的选项列表，请检查你下载的 Perl 版本的 `INSTALL` 文件。

### A.2 UNIX 安装配置选项

| 选项 | 结果 |
| --- | --- |
| `-Dcc` | 指定替代编译器 |
| `-h` | 列出选项 |
| `-O` | 使用现有的 `CONFIG.SH` 但覆盖某些项 |
| `-des` | 接受默认值并提供简洁输出 |
| `-Dprefix` | 指定 Perl 安装目录 |
| `-Usedl` | 强制 Perl 静态编译 |

### 网络

关于 Perl 和 UNIX 的更多信息，你应该访问 http://www.perl.com/perl/faq/index.html 的 Perl FAQ。Larry Wall 的文档可用 http://www.atmosmos.washington.edu/perl/perl.html

### Windows 95 和 Windows NT

为 Windows NT 或 Windows 95 安装 Perl 5.0 相对简单。下载压缩包 `107-i86` 后，使用 WinZip 将文件提取到文件信息包含的子目录。如果你想在 C 盘上安装 Perl，只需指定该驱动器；文件将安装在名为 `PERL5` 的子目录中。

提取文件后，寻找名为 `INSTALL.TXT` 的 README 文件。此文件包含了有关 Perl 5.0 安装的最新信息。另一个文件 `README.TXT` 包含其他信息，如 GNU 通用公共许可证、系统要求以及 UNIX 版和 Win32 版 Perl 之间的差异。

除了这些文件外，你必须找到一个名为 `WIN95.TXT` 的文件，它详细说明了在 Windows 95 上运行 Win32 版 Perl 的任何问题。在本书期间，在 Windows 95 上运行 Win32 版 Perl 的某些问题与 16 位外壳 `COMMAND.COM` 有关。

要安装 Win32 版 Perl，从命令提示符运行 `INSTALL.BAT`。这会将 Perl 添加到注册表，创建 `PERLBIN` 子目录（如果不存在），并将该目录添加到路径。此外，如果是在覆盖现有安装进行安装，

应用程序会将包含现有版本 `PERL.EXE` 的文件重命名为包含版本号的文件（例如 `PERL.4.36.EXE`）。

如果你有任何现 Perl 脚本或库，可以在安装过程后将它们复制到 `\PERL5BIN` 子目录下。

你可以使用压缩文件 `107-SRC.ZIP` 中的源码编译 `PERL.EXE`。在下载此文件后，将文件提取到你为创建二进制文件而解压的 `\PERL5` 子目录中。Perl 5.0 是使用 Microsoft Visual C++ 编译的，你可以使用位于 `\PERL5EXE-SRC` 中名为 `PERMAK` 的 makefile 来编译源代码。

你也可以使用 make 来编译 `PERL.EXE` 和 `PERLGOB` 文件。

| 网上资源 |
| :--- |
| 你可以在 http://www.perl.org/PerLFaq.htm 找到适用于 Win32 的 Perl 常见问题 (FAQ) |

## MacPerl

安装 MacPerl 的说明可以在 ftp://ftp.switch.ch/software/mac/perl/ 找到。寻找名为 `MAC_PERL_INFO` 的文件。安装包含四个文件：`MAC_PERL_50RTM_APPL.BIN`、`MAC_PERL_50RTM_APPL.DISK1.BIN`、`MAC_PERL_50RTM_APPL.DISK2.BIN` 和 `MAC_PERL_50RTM_TOOL.BIN`。

你必须运行 System 7 来安装 MacPerl。此外，你需要 Metroworks CodeWarier C/C++ 编译器 (http://www.metroworks.com)、`CGWI_164.SIT.BIN` Socket库以及 `DB_185b.SIT.BIN` Berkeley db库。

按照 Metroworks CodeWarier 的说明进行编译。

MacPerl 首页位于 http://err.ethz.ch/~neri/macintosh/perl.html，并可以在 http://www.unimelb.edu.au/~ssicolot/macperl-primer/home.html 找到常见问题。MacPerl 入门指南可以在 http://www.unimelb.edu.au/~ssicolot/macperl-primer/home.html 获取。

## OS/2

下载包含 Perl 可执行文件和相关文件的压缩文件。此时，适用于 OS/2 的 Perl 版本为 Perl 5.001，补丁级别为 "m"。下载文件后，将文件提取到你的硬盘。请阅读 `README` 以获取文件说明和最新信息。

当前版本的文件指定了 Perl 用户需要将其系统格式化为 HPFS，然后将 `PERL5X.EXE` 和 `PERLGOB.EXE` 复制到 PATH 子目录。`PERL5.DLL` 被复制到 LIBPATH 子目录，并设置变量 `PERL5LIB` 为任何现有和新的 Perl 库目录。

检查 `README` 以获取更多信息，并查看你可能需要安装和运行 Perl 的其他文件和应用程序。

## Linux

如果你使用的是 Slack 的 Linux 安装，版本 3.0 包含了一个 Perl 5.001 副本。当你安装 Linux 或使用包安装工具时，请确保安装了 D 磁盘集。该磁盘集包含 C 库、GNU 编译器以及 Perl。

## 其他操作系统

对于任何操作系统，每个版本的 Perl 通常都会在安装文件中附带说明。如果安装文件经过压缩，你需要适当的软件来提取文件。你还应该寻找任何名为 `README`、`INSTALL` 或 `SETUP` 的文件。

![](img/13bc4258f89bbca754b8ea331d6f5de2_574_0.png)

## 附录 B

## Perl 网络参考

## 目录

- Perl、Web 和 CGI 相关 Usenet
- Web 相关的 Perl 和 CGI 网站
    - Yahoo
    - cgi-lib.pl 首页
    - cgi.pm
    - CGI 集合
    - HFPM 首页
    - Selina Sol 的 CGI 脚本存档
    - 在 www.stars.com 探索星
- 可用的 CGI 脚本
    - PureAmiga
    - MacPerl
    - 适用于 Win32 的 Perl
    - CGI 脚本和 HTML 表单入门
    - NCSA CGI 文档
- 服务器端包含
- 包含通用 Perl 信息的网站
    -  Perl 文档
    - CPAN 网站
    - DBI
    - gd.pm 图形库
    - sgmls.pm

Perl 变得非常流行，是因为它的用途与其能力成比例，而且在许多不同的操作系统上免费提供。附录 A，“Perl 的获取与安装”描述了你可以在何处获取操作系统的 Perl，并为一些最流行的操作系统提供了一些安装说明。本附录列出了你可以在那里获取 Perl 相关的库、脚本、文档等内容的互联网网站。

第一部分描述了你可以浏览并获取有用信息的 usets。此外，每当你对 Perl 或 CGI 编程有任何问题时，你可以在这些小组之一发布帖子，通常可以在八小时内收到至少一个回复。

第二部分描述了拥有有用的 Web、CGI 和 Perl 相关的库、脚本、代码和文档的网站，这些非常有帮助。这些网站可能还包括用于数据库访问以及其他重要互联网活动的库。

最后部分描述了拥有常用的 Perl 库、示例、代码和文档的网站，这些内容不一定与 Web 相关。

### 附录 B -- 网络参考

如果你是 CGI 编程的新手，你会想要查看本附录列出的网站。这样做将让你对可用内容有良好的了解。一个特定的 usenet 组是 **comp.lang.perl**。当你有 Perl 问题或通用问题时，这个组是你最可能发帖的地方。你可以在 http://www.perl.org/faq/ 找到该 usenet 的常见问题解答。

另一个非常有用的网站是 **comp.lang.misc**。如果 **comp.lang.perl** 没有你需要的，**comp.lang.misc** 可能会有，特别是关于工具方面。

要查看最新的 Perl 相关公告，请检查 **comp.lang.announce**。你还应该检查附录 A 和本附录中列出的 CPAN 网站以获取新发布。

usetenet **comp.lang.perl.modules** 如果你想查看模块、对现有模块有疑问或询问是否存在支持特定需求的模块非常有用。

最后一个 usenet 是 **comp.lang.perl.tk**。Tk 是一种由 Sun 开发的界面工具，主要与 Perl（一种嵌入式脚本语言）配合。Perl 5.0 的 Tk 扩展有很多允许集成。如果你对这两个工具都感兴趣，想要查看这个 usenet。你可以在 http://w4.cornell.edu/~vhpk/ptktFAQ.html 找到该 usenet 的常见问题解答。

另一个 usenet 是 **comp.infosystems.www.authoringcgi**。该小组包含许多关于使用 Perl 进行 CGI 的引用，这仍然是最流行的方法之一。你会想要浏览所有以 **comp.infosystems.www** 开头的 usets，以找到最符合你需求的。

表 B.1 使用 Perl 的 Web 编程 Usnets

| Usenet 名称 | 主题 |
| --- | --- |
| comp.lang.perl | Perl 语言讨论 |
| comp.lang.perl.misc | 通用 语言和工具讨论 |
| comp.lang.perl.announce | Perl 相关公告 |
| comp.lang.perl.tk | Perl/Tk 集成讨论 |
| comp.infosystems.www. | Web 开发中的 CGI 问题 |

## Web 相关的 Perl 和 CGI 网站

以下网站对于建立你的 CGI 脚本库非常棒。此外，这些网站让你了解哪些内容可以供你自己使用或修改。你会对大量的自由软件和共享软件感到惊讶。

## B -- Perl 参考资料

### Yahoo

搜索信息或文件的最佳起点之一是 Yahoo（参见 B.1），它是 Web 上组织最有序、全面的搜索网站之一。你可以通过 http://www.yahoo.com 访问 Yahoo。

图 B.1：这展示了 Yahoo WWW 网站。

要查找多种与 Perl 相关的信息，你可以访问 Yahoo 关于 CGI 的 Perl 编程网站：http://www.yahoo.com/Computers_and_Internet/Programming_Languages/Perl/。你可以从 http://www.yahoo.com/Computers_and_Internet/Internet/World_Wide_Web/CGI_Common_Gateway_Interface/ 开始访问通用 CGI 编程信息；或者通过 http://www.yahoo.com/Computers_and_Internet/Internet/World_Wide_Web/Perl/ 查找特定于 Web 信息，包括一个 Perl 脚本部分。

## cgi-lib.pl 主页

使用 Perl 进行 CGI 开发最实用的库之一是是由 Stephen Brenner 创建的 cgi-lib.pl。这是一个强大、简单且易于使用的库，同时在 http://www.bio.cam.ac.uk/cgi-lib/ 提供了相关说明和示例。该库包含了诸如 `ReadParse`（解析从表单传递给脚本的数据）以及 `HtmlTop/HtmlBody`（打印 HTML 文档的 `<HEAD>` 和 `<body>` 部分）等函数。该库兼容 Perl 4.0 和 Perl 5.0，非常值得学习。

## cgi.pm

`cgi.pm` 是另一个 CGI 库，为使用 Perl 执行 CGI 编程提供了强大的函数。该库需要 Perl 5.001，使用 Perl 5.0 进行 Web 相关活动。该库对于你的 Perl 库列表必不可少。可以在 http://www-genome.wi.mit.edu/ftp/pub/software/WWW/cgi_docs.html 访问文档、源代码和示例。

## CGI 集合

该网站有一组脚本，其中一些在本章早期已经创建，特别是查看 `Logger.cgi` 脚本，它执行了一个非常有用的功能。你可以通过 http://www.seclab.net/cgi.html 访问该网站。

表 B.2 CGI 集合脚本

## HFPM 主页

这样的网站意味着 CGI/Perl 程序员将工作得更轻松。该网站提供的模块获取表单内容；执行某些处理；并将结果输出到电子邮件，或与网页阅读器通信。你需要 Perl 5.0 和基于 Unix 的系统来使用该网站列出的模块。你还需要 `cgi-pm`（在本章中讨论）以及 `pipeline`（在 HFPM 分发版中提供）。

你可以通过 http://seilab.cs.ucdavis.edu/~hoagland/hfpm/ 访问该网站。

## Selena Goi 的 CGI 脚本存档

这个引人注目且实用的网站包含许多复杂的 CGI 脚本，例如 Web Chat 1.0、一个幻灯片脚本、一个访客簿脚本以及一个完整的购物车脚本。该网站不仅提供示例，还让你看到它们的运行效果。此外，你还可以查看示例使用的 HTML 和其他文档。示例有完整的文档说明且易于理解。

这是一个必访问的网站；你可以通过 http://www2.eff.org/-erict/Scripts/ 访问它。表 B.3 列出了示例并描述了它们的功能。

表 B.3 Selena Goi 的 CGI 脚本示例

| 示例 | 描述 |
| --- | --- |
| Selena Goi's Electronic Outlet 2.0 (database) | 实现类数据库购物车系统所需的完整文件集 |
| Selena's Electronic Outlet 2.0 (HTML) | 与前一示例相同，基于 HTML |
| Cool Runnings Music Catalog | 针对目录的购物车概念 |
| The Form Processor | 处理表单输入，使用隐藏变量 |
| Database Manager 2.0 | 数据库管理工具 |
| Database Search Engine 1.0 | 为 Database Manager 2.0 搜索引擎 |
| Groupware Calendar | 可供小组读取/修改的日历 |
| Keyword Search Engine 3.0 | 遍历 HTML 文档，搜索关键词并返回输出 |
| authentication-lib.pl | 认证模块 |
| date.pl | 基于日期的模块 |

## 访问 www.stars.com

这是一个非常丰富的资源，被描述为“Web 开发者的百科全书”。网站位于 http://www.stars.com。包含了 HTML、CGI、数据库和样式指南的教程。当你访问 http://www.Stars.com/Vlib/ Web 开发库时，你会发现它有 69 个链接，以及所有关于 Perl 进行 CGI 脚本在 UNIX 或 Windows 上完成的示例，包括动画、留言板和邮件。你可以通过 http://www.net/users/PureAmiga/index.html 访问该网站。Adam's Perl 页面 http://marketplace.com/~adam/，你可以在这里 http://ethz.ch/~neeri/macintosh/perl.html 找到该页面，在 http://unimelb.edu/~ssilcot/perl-primer/home.html 找到 MacPerl 入门，在 ftp://perl.com/pub/ha/MacPerl/faq.html 找到 MacPerl FAQ。

## 去 CGI 脚本

另一个用于 CGI 脚本的优秀资源，该网站按类别列出了 CGI 示例：
- Animators
- Automated WWW Generators
- Bulletin Boards
- Chat Scripts
- Comments
- Dynamic Links (Add Links)
- Environment Variable
- File Upload
- Guestbooks
- Height/Width Inserters
- Phone Directory
- Random Number Generators
- Shopping Carts
- Web-Based E-Mail
- WWW Page

该网站包含对 CGI 和表单的简要介绍，可以通过 http://kufacts.cc.edu/forms-intro.html 访问。该网站不仅描述了过程，还提供了演示 HTML 和 CGI 如何交互的图形。

## Perl for Win32

一个关于 Perl for Win32 信息的有用网站，位于 http://www.perl.com/PerlFaq.html 之后。维护该网站的公司还提供了被认为是 Windows NT 和 Windows 9 最稳定的端口。此外，在 http://www.perl.com/perlis.html 可以获得名为 `PER.DLL` 的动态库 (DLL)。该库配合 Microsoft Internet 提高访问 CGI 的效率。注意该 DLL 的发布可能还是测试版。

## NCSA 的 CGI 文档

如果你想学习某些东西，必须回到源。该网站包含了关于所有 CGI 程序员编写安全 CGI 脚本的技巧。

## 服务器端包含

Yahoo 维护着一个服务器端包含 (SSI) 的网站。你可以通过 http://www.yahoo.com/Computers_and_Internet/Internet/World_Wide_Web/HTTP/Servers/Server_Side_Scripting/Server_Side_Includes/ 访问该网站（通过访问 www.yahoo.com 然后点击链接到达此网站比直接输入 URL 更好）。

## 附加 B -- Perl 参考

从该网站，你可以访问 SSI 的有用教程，位于 http://www.carleton.ca/~dmcfet/html/ssi.html。此外，SSI 适用于 Web 服务器 NCSA HTTPD (http://niac.edu/docs/tutorials/html)，它不兼容 CERN 服务器。然而，你可以在 http://sw.WebTools/fake.html 访问模块 `fakessi.pl`。该模块提供了类似 SSI 的。

## 包含通用 Perl 信息的网站

本节列出了包含 Perl 材料的网站，这些材料可能与 Web 或 CGI 相关，但适用于任何类型的应用程序。

## 基础 Perl 文档

当你使用 Perl 时，你会想要查看一些基础 Perl 文档。查看以下网站：

- Larry Wall 提供的 Perl 手册 (http://www.atmos.washington.edu/perl/perl.html)
- Tom Christensen 提供的 Perl 语言主页 (http://www.perl.com/perl/)
- Perl 5.0 扩展的要概述 (http://www.perl.com/perl/info/perl5-brief.html)
- Perl FAQ (http://www.perl.com/perl/faq/index.html)
- 通用 Perl 信息 (http://www.perl.com/perl/everything_to_know/index.html)
- 大学 Perl 存档 (http://www0.cisle.edu/perl/)
- Tom Christensen 提供的 Perl 数据结构食谱 (http://www.perl.com/perl/pdsc/)

## CPAN 站点

CPAN 代表全面 存档网络。表 B.4 列出了 CPAN 站点。

## 表 B.4 CPAN 镜像站点

| 站点 | URL |
| --- | --- |
| 北洲加拿大 | ftp://enterprise.ic.gc/pub/perl/CPAN/ |
| 北洲加利州 | ftp://ftp.digital.com/pub/plan/perl/CPAN/ |
| 北洲加利州 | ftp://ftp.cdrom.com/pub/perl/CPAN/ |
| 北洲科罗拉多州 | ftp://ftp.cs.colorado.edu/pub/perl/CPAN/ |
| 北洲佛罗里达州 | ftp://ftp.cisl.edu/pub/perl/CPAN/ |
| 北洲伊利诺伊州 | ftp://uiarchive.cso.uiuc.edu/pub/lang/perl/CPAN/ |
| 北洲纽约州 | ftp://ftp.rge.com/pub/languages/perl/CPAN/ |

## 附录 B -- Perl 参考

| 北洲：俄克拉荷马 | ftpp://ftp.uoknor.edu/mirrors/CPAN/ |
| 北洲：德克萨斯 | ftpp://ftp.sterling.com/programming/languages/perl/ |
| 北洲：德克萨斯 | ftpp://ftp.sedl.org/pub/mirrors/CPAN/ |
| 北洲：德克萨斯 | ftpp://ftp.metronet.com/pub/perl/ |
| 非洲：澳大利亚 | ftpp://ftp.is.co.za/programming/perl/CPAN/ |
| 澳大利亚 | ftpp://ftp.coombs.anu.edu.au/pub/perl/ |
| 新西兰 | ftpp://ftp.mame.mu.oz/au/pub/perl/CPAN/ |
| 欧洲：奥地利 | ftpp://ftp.tekotago.ac.nz/pub/perl/CPAN/ |
| 比利时 | ftpp://ftpp.kulnet.kuleven.be/pub/mirror/CPAN/ |
| 欧洲：捷克克 | ftpp://ftp.sunsite.mff.cuni.cz/Languages/Perl/CPAN/ |
| 欧洲：丹麦 | ftpp://ftp.sunsite.auc.dk/pub/languages/perl/CPAN/ |
| 欧洲：芬兰 | ftpp://ftp.funet.fi/pub/languages/perl/CPAN/ |
| 欧洲：法国 | ftpp://ftp.ibp.fr/pub/perl/CPAN/ |
| 欧洲：法国 | ftpp://ftp.pasteur.fr/pub/computing/unix/perl/CPAN/ |
| 欧洲：德国 | ftpp://ftp.leo.org/pub/comp/programming/languages/perl/CPAN/ |
| 欧洲：德国 | ftpp://ftp.rz.ruhr-uni-bochum.de/pub/CPAN/ |
| 欧洲：希腊 | ftpp://ftp.ntua.gr/pub/lang/perl/ |
| 欧洲：匈牙利 | ftpp://ftp.kfki.hu/pub/packages/perl/CPAN/ |
| 欧洲：意大利 | ftpp://cis.utovrm.it/CPAN/ |
| 欧洲：荷兰 | ftpp://ftp.cs.ruu.nl/pub/PERL/CPAN/ |
| 欧洲：波兰 | ftpp://ftp.pk.edu/pub/lang/perl/CPAN/ |
| 欧洲：葡萄牙 | ftpp://ftp.sunsite.icm.edu.pl/pub/CPAN/ |
| 欧洲：葡萄牙 | ftpp://ftp.ciuminho.pt/pub/lang/perl/ |
| 欧洲：西班牙 | http://ftp.etse.urv.es/pub/mirror/perl/ |
| 欧洲：西班牙 | http://ftp.redisis/mirror/CPAN/ |
| 欧洲：瑞典 | http://ftp.sunnet.se/pub/lang/perl/CPAN/ |
| 欧洲：瑞士 | http://ftp.switch.ch/mirror/CPAN/ |
| 欧洲：英国 | http://ftp.demon.co.uk/pub/mirrors/perl/CPAN/ |
| 欧洲：英国 | http://sunsite.doc.ic.ac.uk/packages/CPAN/ |
| 欧洲：英国 | http://unix.hexa.ac.uk/mirrors/perl-CPAN/ |
| 日本 台湾 | http://ftp.lab.kdd.co.jp/lang/perl/CPAN/ |
| 南美洲：智利 | http://sunsite.dcc.uchile.cl/pub/Lang/perl/CPAN/ |

CPAN 站点有一个名为 `/MODULES` 的子目录，包含了存储在每个 CPAN 站点的各种 Perl 模块引用。要访问模块列表，请访问 `/modules/01modules.index.html`。你可以在 `/modules/00modlist.long.html` 模块开发标准的描述。模块按作者、类别和模块进行列出。

每个 CPAN 站点还有一个值得查看的子目录 `/SCRIPTS`。该子目录被分为若干子目录，每个子目录代表不同的类别。每个类别可以包含许多你可以检查、复用和使用的 Perl 脚本。

## DBI

`DBI`（即 Perl 数据库接口）是 Perl 的数据库 API。查找有关此接口信息的最佳方法是 http://www.hermetica.com/teologia/DBI/index.html。你可以在 http://www.hermetica.com/teologia/DBI/DBI/index.html 下载最新版本。此外，你可以在该站点找到任何现有的驱动。适用于 Oracle、MySQL、mSQL、Informix 和 Qbase 数据库的可用驱动。目前正在计划实现 ODBC 接口。

关于 DBI 信息的另一个站点位于 http://www.fugue.com/dbi/。你也可以在此处订阅三个 DBI 邮件列表。

## gd.pm 图形库

`gd` 是一个最初用 C 语言编写（目前也是如此）的图形库，但 gd 的版本已经移植到了 Perl。你可以在 http://www-genome.wi.mit.edu/ftp/pub/software/WWW/Gd.html 获取该库。该库允许你创建三个类：`Image`（图像）、`Font`（字体）和 `Polygon`（多边形）。

## sgmlps

此 Perl 库解析 sgmls 和 nsmsgperl 模块的，。

## 将电子书作为 Windows 帮助文件阅读

要将电子书作为 Windows 帮助文件阅读，请打开 CD-ROM 中 `EBOOKS` 子目录下的名为 `PERWLW.HLP` 的文件。点击向前或向后的箭头可以逐章节向前或向后翻页。要查看书籍目录，请选择要查看的章节编号。

## 查找示例代码

在阅读此书时，你会注意到示例应用程序和程序段通过代码列表头与正文隔离开，如下所示：

列表 10.1 (10_01.htm) 正在创建新的 snare 页面...

此列表表示特定的代码段（或示例）包含在 CD 中。要找到该代码，请浏览到 CD 上的 `CODE` 子目录，并选择与所指章节的列表头中所引用的文件名的文件。对于此示例，你需要查看第 10 章子目录并打开 1_01.htm 文件。

![](img/13bc4258f89bbca754b8ea331d6f5de2_586_0.png)

## 请在我的留言板上签名

姓名：
Joe User

留言：
嘿，这真的太酷。
我该如何在我的网站上实现这些功能？

登录

## Joe User

嘿，这真的太酷。
我该如何在我的网站上实现这些功能？

## Netscape - [留言板]

文件 编辑 视图 主 书签 目录 窗口 帮助

后退 向前 刷新 图片 打开 打印 查找 停止

位置: http://canyon.canyon.com/cgi-bin/harlan/showguestbook

Joe User, 1996/2/7, 19:27
嘿，这真的太酷。
我该如何在我的网站上实现这些功能？

William Sherman, 1996/2/8, 16:05
嘿，网站很酷。
但我真正想知道的是，这里是否有人来自亚特兰大。

Joshua Chamberlain, 1996/2/8, 16:08
我不是亚特兰大的，是缅州的。

我想和任何感兴趣的人聊聊哲学。我的邮箱地址是 jlc@bowdoin.edu
谢谢。

文档：完成

## Netscape - [留言板]

Joe User, 1996/2/7, 19:27
嘿，这真的太酷。
我该如何在我的网站上实现这些功能？

William Sherman, 1996/2/8, 16:05
嘿，网站很酷。
但我真正想知道的是，这里是否有人来自亚特兰大。

显示后两条条目

## Netscape - [留言板]

Joshua Chamberlain, 1996/2/8, 16:08
我不是亚特兰大的，是缅州的。

我想和任何感兴趣的人聊聊哲学。我的邮箱地址是 jlc@bowdoin.edu
谢谢。

Sam Grant, 1996/2/8, 16:13
大家好。

我考虑退休到密西西比州的维克斯堡堡。那里有人对此有异议吗？

显示后两条条目

## Netscape - [留言板]

文件 编辑 视图 转 书签 选项 目录 窗口 帮助

后退 向前 主页 刷新 图片 打开 打印 查找 停止

位置: http://canyon.canyon.com/cgi-bin/showguestbook2/582

Dave Harlan, 1996/2/8, 16:14
感谢所有出色的回复。
我希望大家都能使用这些信息。

如果需要更多帮助，请告诉我。

## 请在我的留言板上签名

...但首先，是当下的名言：

> 愤世嫉俗者是一个提着偷偷来的灯笼寻找诚实之的人。
-- Edgar A. Shoaff

... 我们现在回到常规留言板。

姓名：
留言：

## 用户信息

感谢您对我们实验的兴趣。我们需要以下信息来将互联网使用情况与人口统计数据相关起来。请提供下方所有字段中的信息。这些信息将仅用于本研究。未经您的许可，绝不会使用任何关于您的特定信息。

## 身份

电子邮件地址：
名： 姓：

## 你在哪里？

大洲：北美洲 国家：美国

## 关于你

性别：女 年龄：20-25

年收入：$25,000-40,000 职业：技术

## 关于你和网络

网络经验：6个月到2年 网络连接：28800

你是否因工作目的使用网络？是 是 否

 提交信息
