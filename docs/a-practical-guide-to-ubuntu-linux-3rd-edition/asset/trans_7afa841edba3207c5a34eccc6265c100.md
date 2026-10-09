
和系统管理员，他为我撰写系统管理、网络、互联网和编程章节提供了巨大的帮助。

还要感谢顾问洛林·卡拉汉（Lorraine Callahan）和史蒂夫·沃姆普勒（Steve Wampler）；罗纳德·希勒（Ronald Hiller，Grabrurn Technology）；查尔斯·A·普拉特（Charles A. Plater，韦恩州立大学）；鲍勃·帕洛沃达（Bob Palowoda）；汤姆·比亚拉斯基（Tom Bialaski，Sun Microsystems）；罗杰·哈特穆勒（Roger Harttmulle，Network Associates旗下的TIS Labs）；孔文（Kaowen Liu）；安迪·施皮策（Andy Spitzer）；里克·施奈德（Rik Schneider）；杰西·C·劳伦特（Jesse C. Laurent）；史蒂夫·贝伦图（Steve Bellentoo）；雷·W·希尔特布兰特（Ray W. Hiltrbrandt）；珍妮弗·惠特姆（Jennifer Witham）；格特-扬·哈根纳尔斯（Gert-Jan Hagenaaars）；以及卡斯珀·迪尔克（Casper Dirk）。

《Ubuntu Linux®实用指南》（第三版）部分基于我之前的两本UNIX著作：《UNIX System V实用指南》和《UNIX系统实用指南》。许多人帮助过我完成那两本书，此处也要感谢帕特·帕谢加尼（Pat Parseghian）；凯瑟琳·赫梅威博士（Dr. Kathleen Hemenway）；布莱恩·拉罗斯（Brian LaRose）；拜伦·A·杰夫（Byron A. Jeff，克拉克·亚特兰大学）；查尔斯·斯特罗斯（Charles Stross）；杰夫·吉特林（Jeff Gitlin，Lucent Technologies）；库尔特·霍肯伯里（Kurt Hockenbury）；莫里·巴赫（Maury Bach，英特尔以色列）；彼得·H·萨卢斯（Peter H. Salus）；拉胡尔·戴夫（Rahul Dave，宾夕法尼亚大学）；肖恩·沃尔顿（Sean Walton，Intelligent Algorithmic Solutions）；蒂姆·塞格尔（Tim Segall，Computer Sciences Corporation）；贝赫鲁兹·福鲁赞（Behrouz Forouzan，DeAnza College）；迈克·基南（Mike Keenan，弗吉尼亚理工州立大学）；迈克·约翰逊（Mike Johnson，俄勒冈州立大学）；赞德琳·普莱恩（Jandelyn Plane，马里兰大学）；阿诺德·罗宾斯（Arnold Robbins）和萨蒂什·梅农（Satish Menon，佐治亚理工学院）；克利夫·沙弗（Cliff Shaffer，弗吉尼亚理工州立大学）；以及史蒂文·斯蒂帕内克（Steven Stepainek，加利福尼亚州立大学北岭分校），感谢他们审阅了这本书。

我继续感谢那些帮助过我的UNIX书籍早期版本的许多人。特别感谢罗杰·西佩尔（Roger Sippel）、劳拉·金（Laura King）和罗伊·哈林顿（Roy Harrington）让我接触了UNIX系统。我的母亲海伦·索贝尔博士（Dr. Helen Sobell）在多个关键节点为原稿提供了宝贵的意见。此外，还要感谢以撒·拉比诺维奇（Isaac Rabinovitch）、拉斐尔·芬克尔教授（Professor Raphael Finkel）、伦道夫·本顿教授（Professor Randolph Benton）、鲍勃·格林伯格（Bob Greenberg）、乌多·波奇教授（Professor Udo Poach）、朱迪·罗斯（Judy Ross）、罗伯特·维罗夫博士（Dr. Robert Veroff）、迈克·丹尼博士（Dr. Mike Denny）、乔·迪马蒂诺（Joe DiMartino）、约翰·马德森博士（Dr. John Madsen）、黛安·舒尔茨（Diane Schulz）、罗伯特·荣格（Robert Jung）、查尔斯·惠特克（Charles Whitaker）、唐·克拉根（Don Cragun）、布莱恩·多赫蒂（Brian Dougherty）、罗伯特·费什博士（Dr. Robert Fish）、盖伊·哈里斯（Guy Harris）、廖平（Ping Liao）、加里·林德格伦（Gary Lindgren）、贾里特·罗森伯格博士（Dr. Jarrett Rosenberg）、彼得·史密斯博士（Dr. Peter Smith）、比尔·韦伯（Bill Weber）、迈克·比安奇（Mike Bianchi）、斯科特·莫里斯（Scooter Morris）、克拉克·埃科伊斯（Clarke Echois）、奥利弗·格里勒迈尔（Oliver Grillemeyer）、大卫·科尔恩博士（Dr. David Korn）、斯科特·韦卡特博士（Dr. Scott Weikart），以及理查德·柯蒂斯博士（Dr. Richard Curtis）。

最后，感谢彼得和他的家人提供了饮食以及一个非常舒适的工作场所。我花了大量时间阅读手稿，地点在JumpStart，那是彼得家附近的咖啡和三明治店。如果你在附近（旧金山24街与格雷罗街交叉口），请进来打个招呼。

我对本书中的任何错误和遗漏负责。如果你发现错误或有任何评论，请告诉我（mgs@sobell.com），我将在下一次印刷中修正。我的主页（www.sobell.com）列出了错误列表并致谢发现者。它还提供了书中较长脚本的副本以及指向互联网上有趣Linux页面的链接。

马克·G·索贝尔（Mark G. Sobell）
加利福尼亚州旧金山

## 1 欢迎使用 Linux

### 本章内容

- Ubuntu Linux . . . . . . . . . . . . . . . . . 2
- UNIX和GNU-Linux的历史 . . . . . . . . . . . . . . . . . 3
- Linux的传承：UNIX . . . . . . . . . . . . . . . . 3
- Linux有什么优点？ . . . . . . . . . . . . 6
- Linux概述 . . . . . . . . . . . . . . . . 12
- Linux的其他特性 . . . . . . . . . . . . 17
- 本书使用的约定 . . . 19

操作系统是低级软件，它负责调度任务、分配存储，并处理与外围硬件（如打印机、磁盘驱动器、屏幕、键盘和鼠标）的接口。操作系统主要由两部分组成：*内核*和*系统程序*。内核为计算机上运行的所有其他程序分配机器资源——包括内存、磁盘空间和*CPU*（第1143页）周期。系统程序包括设备驱动程序、库、实用程序、Shell（命令解释器）、配置文件和脚本、应用程序、服务器以及文档。它们执行更高级的后台任务，通常在客户端/服务器关系中充当服务器。许多库、服务器和实用程序是由GNU项目编写的，稍后将会讨论。

### Linux内核

Linux内核由芬兰本科生林纳斯·托瓦兹（Linus Torvalds）开发，他利用互联网立即将源代码免费提供给他人。托瓦兹于1991年9月发布了Linux 0.01版本。

这个新的操作系统是通过大量的艰苦工作才组合起来的。世界各地的程序员迅速扩展内核并开发其他工具，添加功能以匹配已在BSD UNIX和System V UNIX（SVR4）中发现的功能，以及新的功能。Linux这个名字是Linus和UNIX的组合。

Linux操作系统是由世界各地许多人的合作开发而成的，它是互联网的产物，也是一个免费操作系统。换句话说，所有源代码都是免费的。你可以自由地研究、重新分发和修改它。因此，代码免费提供——软件、源码、文档或支持（通过新闻组、邮件列表和其他互联网资源）均不收费。正如GNU自由软件定义（在附录D中引用）所述：

> “自由软件”关乎自由，而非价格。要理解这个概念，你应该将“自由”理解为“言论自由”，而不是“免费啤酒”。

### Ubuntu Linux

**发行版** 各个组织将Linux内核和系统程序打包为Linux发行版（访问distrowatch.com获取更多信息）。一些最流行的发行版包括SUSE、Fedora、Ubuntu、Red Hat、Debian和Mandriva。发行版之间最大的区别通常在于用户如何安装操作系统。其他区别包括默认安装的图形配置工具以及用于保持系统最新状态的工具。

**Canonical** 在马克·沙特尔沃斯（Mark Shuttleworth）的领导下，Canonical有限公司（www.canonical.com），即Ubuntu Linux的赞助商，支持许多类似的Linux发行版：Ubuntu运行GNOME桌面管理器，Kubuntu（www.kubuntu.org）运行KDE桌面管理器，Edubuntu（www.edubuntu.org）包含许多与学校相关的应用程序，而Xubuntu（www.xubuntu.org）运行轻量级的Xfce桌面，使其非常适合较旧、较慢的机器。

自2004年10月首次发布以来，Ubuntu一直是一个面向社区的项目。Ubuntu维护着若干种使其有效运作的结构，并邀请社区成员参与所有这些结构。有关Ubuntu治理的更多信息，请参见www.ubuntu.com/community/processes/governance。

Ubuntu Linux基于Debian Linux，专注于增强可用性、无障碍性和国际化。虽然Ubuntu最初针对桌面用户，但最近的版本越来越强调服务器市场。随着每六个月发布一次新版本，Ubuntu提供了前沿的软件。

Ubuntu系统使用GNOME桌面管理器（www.gnome.org），并包含OpenOffice.org生产力工具套件、Firefox网络浏览器、Pidgin（以前称为Gaim）即时通讯客户端以及一系列工具和游戏。为了保持系统上的软件最新，Ubuntu使用Debian的deb包格式和各种基于APT的工具。

Ubuntu的治理结构遵循仁慈独裁者模型：马克·沙特尔沃斯是终身自封的仁慈独裁者（SABDFL）。该结构包括技术委员会（Technical Board）、Ubuntu社区理事会（Ubuntu Community Council）、地方社区（Local Communities, LoCo's）以及宇宙主宰者（Masters of the Universe, MOTU; wiki.ubuntu.com/MOTU）。有关Ubuntu的更多信息，请参见www.ubuntu.com/aboutus/faq。

### UNIX和GNU-Linux的历史

本节介绍了UNIX与Linux之间以及GNU与Linux之间关系的一些背景。

### Linux的传承：UNIX

UNIX系统是由需要一组现代计算工具来帮助其项目的研究人员开发的。该系统允许一组在项目中合作的人员共享选定的数据和程序，同时保持其他信息私密。

大学和学院通过“四年效应”在推动UNIX操作系统的普及中发挥了重要作用。当UNIX操作系统在1975年变得广泛可用时，贝尔实验室以象征性的费用将其提供给教育机构。反过来，学校将其用于其计算机科学课程，确保计算机系学生熟悉它。由于UNIX是一个如此先进的开发系统，学生适应了复杂的编程环境。随着这些学生毕业并进入工业界，他们期望在类似先进的环境中工作。随着他们在商业世界中步步高升，UNIX操作系统进入了工业界。

除了让学生接触UNIX操作系统外，加州大学伯克利分校的计算机系统研究组（CSRG）对其进行了重大添加和修改。实际上，它进行了如此多受欢迎的更改，以至于该系统的某个版本被称为Berkeley软件发行版（BSD）UNIX系统（或仅称为Berkeley UNIX）。另一个主要版本是UNIX System V（SVR4），它源自AT&T和UNIX System Laboratories开发和维护的版本。

