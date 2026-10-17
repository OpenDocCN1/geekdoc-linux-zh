
| appointments or todo | 待办事项列表。大写文件名在目录列表中排序。 |
| birthdays | 生日列表。 |
| calendar | 个人日历文件。你可以根据自己的兴趣保留特殊的日历，例如 `calendar.birthdays`。 |
| crontab | 个人定时任务（参见食谱 28.3 [调度命令]，第 557 页）。 |
| passwd or passwords | 个人密码文件。确保更改其权限，以便其他人无法查看（参见食谱 6.3.4 [使文件私有]，第 169 页）。 |

喜欢的格言。

### C.3 使用目录存放邮件

你可能需要一个目录来保存所有的邮件通信，包括传入和出的邮件。大多数人使用 `Mail` 或 `mail` 作为目录的名称；许多电子邮件应用程序使用其中一个名称作为存储消息的默认值。你可以在这里建立子目录，将消息存储在更整洁的文件夹中，例如 `outgoing` 用于出的邮件，`family` 用于家庭通信，`projects` 用于项目邮件。

### C.4 使用目录管理项目

在处理某种类型的项目时，有时最好将一组文件放在一起。根据你的工作和企业需求，你可能想为项目创建一个目录——例如 `jobs`（任务）、`projects`（项目）、`work`（工作）、`drafts`（草稿）或 `research`（研究），取决于你的具体工作，并为你正在进行的任何特定项目或任务创建子目录。

程序员通常有一个用于计算机源代码的 `src` 目录；其他你可能考虑的特殊工作常用目录还包括 `photos or photographs`（照片）、`art or images`（艺术图像）、`books`（书籍）以及 `music or recordings`（音乐或录音）。爱好者可能会保留 `scrapbook`（剪贴）或 `craft`（手工艺）目录。

这些大类内部可能会包含特定项目的目录，而这些项目目录可能又包含自己的用于源文件的 `src`、用于文档的 `doc`、用于致谢的 `THANKS` 文件等。

### C.5 使用目录存放临时文件

你可能希望有一个目录作为“暂存区”，用来存放那些可能很快需要处理但目前不必立即处理的新文件。我不喜欢让主目录变得杂乱，所以拥有一个 `~/tmp` 目录来放置这些东西可以保持它的整洁有序。

当然，你可以将文件保存到系统级的临时目录 `/tmp` 中，但该目录会被系统定期清理。如果你在一个多用户系统上，你可能仍然想要一个私有的临时目录（所有用户通常对 `/tmp` 具有读写权限）。

## 附录 D：进一步感兴趣的参考文献

本附录列出了你应该了解 Linux 软件和信息的重要来源。

### D.1 Linux 软件和硬件来源

这些是获取软件（包括整个 Linux 发行版）以及 Linux 硬件信息的来源。

#### D.1.1 Linux发行版

以下是最流行的 Linux 发行版。可以在 DistroWatch [http://www.distrowatch.com/] 网上找到更完整的列表，那里有一个比较其功能的图表。

- Debian Gnu/Linux 由致力于自由软件理念的志愿者开发。[http://debian.org/]
- Fedora Core 是旧 Red Hat Linux 发行版的两个当代后代之一（另一个是 Red Hat Enterprise Linux）。[http://fedora.redhat.com/]
- Gentoo 是一个小型发行版，与其他发行版不同，它仅以源码形式发布——所有二进制文件都为主机系统编译，从而提供了最高的效率。[http://www.gentoo.org/]
- KNOPPIX 是一个基于可启动 CD-ROM 光盘的德国发行版。它使用 DEB 作为包格式。[http://www.knopix.com/]
- Mandrakelin 以安装包小而著称，并让你在硬盘的分区上保留原有的操作系统。[http://www.mandrakelin.com/en/]
- muLinux 是一个为老旧计算机设计的小型发行版。[http://mulinus.sunsite.dk/]
- Red Hat Enterprise 是 Red Hat, Inc. 其广受欢迎且成熟的发行版的继者。[http://redhat.com/]
- Run Up to date Linux Everywhere (RULE) 专为需要现代 Linux 但负担不起现代计算机的用户设计。它基于最新的 Fedora Core，但可以在内存低且 CPU 较小的系统上运行。[http://www.rule-project.org/]
- Slackware Linux 是仍在发布的最古老的 Linux 发行版。[http://slackware.com/]
- SUSE Linux 是德国设计，现由 Novell 所有，在欧洲非常流行。[http://suse.com/]
- Turbolinux 是 UnitedLinux 发行版的变体，是中国最流行的发行版。[http://www.turbolinux.com/]
- Yellow Dog Linux 专为 PowerPC 电脑（如 Apple Macintoshintos）制造（Debian 及其他发行版也有此类版本）。[http://www.yellowdoglinux.com/]

#### D.1.2 Linux 及相关软件存档

这些是 Linux 免费软件和整个 Linux 发行的在线来源。

- Freshmeat 包含了数以千计的免费软件包的可搜索描述和链接。它包含一个用于你桌面的 GUI“主题”仓库。[http://freshmeat.net/ 和 http://themes.freshmeat.net/]
- FSF/UNESCO 自由软件目录是一个按类别排序的软件包大目录。[http://www.gnu.org/directory/]
- Ibiblio Linux Archive（原名 SUNsite）是一个非常大的 Linux 软件存档，可能是连续运行最久的。它包含一个供下载的完整发行版公共存档。[http://www.iblio.org/pub/Linux/]
- Savannah 托管了并非 GNU 项目但仍属于自由软件的软件包。[http://savannah.nongnu.org/]
- Scientific Applications on Linux (SAL) 是运行在基于 Linux 系统上的科学软件权威列表。[http://ftp.linux-berlin.de/lsoft/]
- Sound and MIDI Software for Linux 是基于 Linux 系统的声音和音频全面指南。[http://linux-sound.org/]
- SourceForge 是互联网上最大的免费软件开发者社区；它为免费软件开发者提供免费资源。[http://sourceforge.org/]
- Sweetcode 跟踪创新的免费软件——而不仅仅是某些原本就没有趣的旧旧应用的最新免费克隆。[http://sweetcode.org/]

#### D.1.3 Linux 硬件

这些在线资源将帮助你挑选并获取兼容 Linux 的硬件。

- Hardware.net 是兼容 Linux 的硬件集合。[http://hardware.net/]
- Linux.org 拥有硬件相关文档。[http://linux.org/]
- Laptops.org 是笔记本电脑数据库。[http://laptops.org/]
- Ratings.net 提供兼容 Linux 的硬件评测。[http://ratings.net/]
- PriceWatch.com 是硬件价格数据库。[http://pricewatch.com/]

### D.2 Linux 书籍

这些是书籍和在线资源。

#### D.2.1 通用指南

- LINUX SYSTEM ADMINISTRATOR'S GUIDE，Wirzenius 等著，1993年。一本关于系统管理的经典著作。[http://tldp.org/sag/]
- LINUX GAZETTE，一份致力于“让 Linux 更有趣”的每月网络杂志，由 SSC 出版。[http://linuxgazette.com/]
- HOWTO INDEX，Linux 文档项目。涵盖 Linux 的各个方面。[http://tldp.org/HOWDO/]
- THE LINUX FAQ，作者，包含了关于 Linux 的常见问题。[http://tldp.org/FAQ/]
- LINUX: USERS TUTORIAL AND EXPOSITION，Paul Sheer 著，Prentice Hall，2001年。Linux 使用完全指南。[http://route.sourceforge.net/]
- THE LINUX COOKBOOK，第二版，在系统上使用 TeX 排版。[http://sourceforge.net/]

#### D.2.2 Linux 工具与应用指南

- THE GNU AWK USER'S GUIDE，Arnold D. Robbins 著，1997年。[http://gnu.org/software/gawk/manual/]
- DSELECT DOCUMENTATION FOR BEGINNERS，Stéphane Bortzmeyer 著，Debian 文档项目，1999年。推荐首次使用 dselect 的用户。[http://debian.org/releases/2.1/i386/dselect-beginner.en.html]

#### GROFF 及资源

- THE TEXT PROCESSOR FOR TYPESETTERS，Ralph Cordeyer 著，2001年。[http://troff.org/]
- TBL—A PROGRAM TO FORMAT TABLES，M.E. Lesk，贝尔实验室，1976年。使用 tbl 的极具价值的介绍。[http://www.neverland.ch/groff/tbl.ps.gz]
- THE GROFF AND FRIENDS HOWTO，Dean Allen Provins 著。使用 GROFF 的介绍。[http://www.neverland.ch/groff/TheGroffFriendsHowto.ps.gz]

#### IRC

Caraballo, David, and Joseph Lo,《IRC 入门》(THE IRC PRELUDE), 网站，2000。针对初者的 IRC 优秀介绍。[http://irchelp.org/irhelp/new2irc.html]

#### PERL

Kuhn, Bradley M.,《入门 PERL》(PICKING UP PERL), 网站，2002。一个内容不错但未完结的 PERL 教程。[http://www.ebb.org/PickingUpPerl/]

#### PostScript

Capella Archive Publications，《Capella 档案出版》(CAPELLA ARCHIVE), 网站，2001。用于 PostScript 编程的实操教程和参考库。[http://www.capella.demon.co.uk/]

#### SED

Bonzini, Paolo,《SED 工具箱》(THE SEDER'S GRAB-BAG), 网站，2002。常用的 SED 信息集合，包含常见问题解答和许多示例脚本。[http://sed.sourceforge.net/grabbag/]
Pement, Eric,《SED 实用单行命令》(HANDY ONE-LINERS FOR SED), 网站，2003。列出许多用于文本编辑和处理的有用命令的单页。[http://www.student.northpark.edu/pement/sed/sedline.txt]
Pizzini, Ken，《流编辑器 SED》(SED, A STREAM EDITOR), 自由软件基金，1998。[http://www.gnu.org/software/sed/manual/sed.html]

#### TeX 及其伙伴

Doob, Michael,《TeX 温和入门》(A GENTLE INTRODUCTION TO TeX), 网页，1993。推荐的使用 plain TeX 的介绍。[ftp/ctan.tug.org/tex-archive/documentation/gentle/]
Grandis, Christophe,《METAFONT 与 TeX/LaTeX 资源》(THE METAFONT AND TeX/LaTeX RESOURCE PAGE), 网站，2003。提供了使用 METAFONT 的入门教程。[http://metafont.latex.free.fr/]
Hahn, Jane，《人人 LaTeX》(LATEX FOR EVERY), PTR Prentice-Hall Inc., 1993。对于想要利用 TeX 的力量进行信函、论文和报告排版的人来说，这是一本极佳的书。
Knuth, Donald E.,《教程》(THE TEXTBOOK), Addison-Wesley,1984。由 TeX 作者编写的原版 TeX 书。
Oetiker, Tobias, 等，《LaTeX 并不短的介绍》(THE NOT SO SHORT INTRODUCTION TO LaTeX), 网站，1999。推荐的使用 LaTeX 的介绍。[http://ctan.hug.org/tex-archive/documentation/lshort/]
Robbins, Arnold，“什么是 GNU?”，《Linux 日刊》(LINUX JOURNAL), 第 6 期，1994年10月。一篇入门教程。[http://www.linuxjournal.com/article.php?id=2840]
Underwood, Rebecca, 等，《LaTeX 与 BIBEX 教程与作业》(LaTeX AND BIBEX TUTORIALS AND ASSIGNMENT), 网站，1996。一个非常好的 LaTeX 教程，展示了如何排版文章。提供 DVI 格式在线下载。[http://www.soe.ucsc.edu/~karplus/80k/latex-tutorial-new.dvi]

#### D.2.3 UNIX 和 Linux 历史书籍

这些是关于系统及其软件历史的书。

Finseth, Craig A.,《文本编辑艺术》(THE CRAFT OF TEXT EDITING), Springer-Verlag and Co.,1991。文本编辑的理论；文本编辑器技术的性性描述。[http://www.finseth.com/~fin/craft]
Hauben, Michael 和 Ronda Hauben，《网民：网络历史与影响》(NETIZENS: ON HISTORY AND IMPACT OF THE NET), IEEE 计算机出版社，1997。一部详尽的网络社会史，包含大量关于 UNIX 历史的内容。[http://www.columbia.edu/~hauben/netbook/]
Kernigan, Brian W. 和 Rob Pike，《UNIX 编程环境》(THE UNIX PROGRAMMING ENVIRONMENT), Prentice Hall Books,1984。描述了 unix 的工具哲学以及它为程序员提供了什么。[http://cm.bell-labs.com/cm/cs/upe/]
Salus, Peter H.,《UNIX 四分之一》(A QUARTER CENTURY OF UNIX), Addison-Wesley,1994。UNIX 系统的完整历史。
Walker, A.N.,《UNIX 环境》(THE UNIX ENVIRONMENT), John Wiley and Sons Ltd.,1984。一次系统的愉快之旅；它运行在如此过时的设备上的事实恰恰证明了这些工具的韧性。

### D.3 Linux 新闻与评论

这些是 Linux 和自由软件新闻及观点的重要来源。

自由软件基金网站既是哲学读物的来源，也是 GNU 项目及其自由软件操作系统的新闻来源。[http://gnu.org/]
Linux.Com 提供特写故事、链接和 Linux 用户组（LUUGs）数据库。[http://linux.com/]
Linux Journal 是最致力于 Linux 的老牌纸质杂志。月刊。[http://linuxjournal.com/]
Linux Today 汇总并发布“互联网时间上的 Linux 新闻。”[http://linxtoday.com/]
Linux Weekly News 自1998 年以来一直关注 Linux 和自由软件运动。[http://lwn.net/]
Slashdot 是 Linux 和自由软件爱好者的流行新闻和讨论网站；新闻灵通通常通常检查几次 Slashdot。[http://slashdot.org/]

## 程序索引

| 术语 | 页码 |
| :--- | :--- |
| atrm | 557 |
| ! | 77 |
| audacity | 496 |
| & | 72, 18 |
| umix | 474 |
| && | 64 |
| aview | 18 |
| &> | 69, 98 |
| ... | 64 |
| ... | |
| > | 68, 288 |
| 5 | | 88 | 58 |
| < | 67, 44 |
| ) | |
| wm | 120 |

| 术语 | 页码 |
| :--- | :--- |
| abrev-mode | 242 |
| abiword | 535 |
| addgroup | 718 |
| adduser | 417 |
| adventure | 583 |
| ee | 263 |
| afterstep | 117, 120 |
| alias | 83, 84 |
| amaya | 667 |
| amixer | 463 |
