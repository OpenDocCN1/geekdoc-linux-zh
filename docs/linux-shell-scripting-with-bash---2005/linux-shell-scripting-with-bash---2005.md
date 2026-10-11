# bash linux shell 脚本





*献给 F. Ray Skilton*
*教授兼作家*
*他让我在茶余饭后学到的计算机知识，远比我在课堂中学到的要多。*

---

## 关于作者

**肯·伯奇 (Ken Burch)** 毕业于加拿大安大略省圣凯瑟琳斯的布鲁克大学，获得计算机科学一等荣誉学位，并在加拿大安大略省金斯顿的皇后大学完成了硕士学业。他自 Linux 0.97 版本起便开始使用 Linux，那时 Linux 尚未普及。他是 PegaSoft Canada（`http://www.pegasoft.ca`）的创始人，该协会致力于在安大略省南部推广 Linux 倡导、教育和开发。他曾与多家公司合作，其中包括麦肯齐金融公司（Mackenzie Financial Corporation），这是加拿大最大的互助基金公司之一。肯是 Durham 地区作家圈的活跃成员，他获奖的短篇小说《距离》（“Distance”）最近刊登在《签名》（“Signatures”）选集中（ISBN 0973210001）。

## 致谢

你在阅读致谢部分？太棒了！

如今的技术书籍从定稿到出版可能只需短短四个月。这个项目耗时两年多才得以完成，经过了细致的研究和精心的开发。如果这本书看起来与你书架上的其他书有所不同，那是有充分原因的，背后有许多优秀的人士在付出努力。

1999 年夏天，我与 Addison-Wesley 出版社的 Michael Slaughter 讨论了撰写一系列 Linux 书籍的事宜。由于 Linux 始于 Bash，所以 Bash 将成为我第一本书的主题。因此，如果你一直渴望一本优秀的 Bash 书籍，请感谢 Michael。

Lawrence Law 是一位 Unix 程序员，曾工作于太平洋两岸，他为保持这本书的新鲜度和趣味性提供了实用建议，同时也辩论了上帝的存在以及称职的 IT 管理问题。

Linux 作者和演讲者 Chris Browne 抽出时间，从维护 `.org` 和 `.info` 域名中抽身出来，提供了急需的关于出版的建议。非常感谢他在 TLUG 和 Postgres 之间为我安排了时间。

Chris Johnson 从象棋比赛和编写 Bash 算法中抽身，对我研究的各个方面提出了质疑。自讨论这本书以来，我还没有见过他，但我猜想他很快就会参加一次 PegaSoft 的会议来领取一本签名版。

当 Addison-Wesley 被 Prentice Hall 收购时，手稿辗转不定，最终落入了 Sams Publishing 的 Katie Mohr 的收件箱。如果你很高兴这本书到了你手中，请买杯咖啡给她。是她向那些做决定的人推荐了这本书。

如果你心里在想“太酷了”以及“我的书架上需要这本书”，那你不是第一个。这项荣誉属于手稿的早期审阅者，是他们说服了有关部门这本书是金子般的宝藏。我不知道你们的名字，但我读到了你们的评论。

高级编辑 Scott Meyers 基本上保留了他收到的手稿原貌。如果你喜欢这本书，请发邮件告诉 Scott，他选择不折腾一件好事是明智的。

我从未弄清楚制作编辑 Elizabeth Finney 具体是做什么的。但她的头衔里有“制作”二字，所以她一定非常重要。可能是一位富有的超级模特，哈佛毕业，还是总统顾问。嘿，Liz，如果你对脱发的 Linux 极客感兴趣，给我打个电话。

因为我来自加拿大，校对编辑 Kezia Eaksey 负责清除所有多余的“u”，将每个“which”改为“that”，并确保所有的“ze”都被改为“zeë”。她眼过不留，我想我明年会请她检查一下我的所得税申报表。





约翰·特兰肯舒（John Traenkenschuh），技术编辑兼首席大师，运行了本书中的每一个示例，以确保没有最后一刻发现的 bug 被印入书中。约翰，你是否还在纳闷，为什么林纳斯是芬兰人，但“Linux”的发音却带有瑞典口音？约翰，天地之间，超乎你哲学想象的事物还有很多。

此外，感谢读者阁下抽出时间探索这本书与众不同的原因。如果你希望看到更多同等质量的书，请联系 Sams Publishing，并告诉他们你的看法。

——肯·O·伯奇（Ken O. Burch）  
2003年11月

## 我们渴望听到您的声音！

作为本书的读者，*你*是我们最重要的批评者和评论者。我们珍视您的意见，并想了解我们做对了什么，什么可以做得更好，您希望我们在哪些领域进行出版，以及您愿意分享的任何其他智慧之言。

您可以通过电子邮件或直接写信给我，告诉我您喜欢或不喜欢这本书的哪些方面——以及我们可以如何使我们的书变得更强。

*请注意，我无法为您解答与本书主题相关技术难题，且由于我收到的邮件量很大，我可能无法回复每一封邮件。*

写信时，请务必包含本书的书名和作者，以及您的姓名和电话或电子邮件地址。我将仔细审阅您的评论，并分享给您参与本书创作的作者和编辑。

- 电子邮件：[opensource@samspublishing.com](mailto:opensource@samspublishing.com)
- 邮寄：Mark Taber
  副出版总监
  Sams Publishing
  800 East 96th Street
  Indianapolis, IN 46240 USA

## 读者服务

要了解关于本书或 Sams Publishing 其他书籍的更多信息，请访问我们的网站 [www.samspublishing.com](http://www.samspublishing.com)。*在搜索框中输入 ISBN（不含连字符）或书名，即可找到您正在寻找的书籍。*

## 引言

### COSC 101

当布罗克大学（Brock University）还是我在读的时候，大多数监督入门计算机科学实验室的高年级学生，会把脚翘在前台上，摊开一本微积分书，当他们的作业被提问打断时会发出粗鲁的吼声。任何人都可以告诉你，我从不适合典型学生的模式。在我的第一个实验室课程中，我制作了一本简短的小册子，涵盖了我参加 COSC 101 第一次实验室课程时所有的疑问；具体而言，那些在故障终端上用闪烁的绿色画出的奇怪提示是什么，以及究竟如何使用它来给自己起一个像 `VAX DUDE` 这样很酷的昵称，以用于 `DEC VMS` 进程？

我不小心留下了一堆我的小册子，第二天其中一位其他监督者冲过来，生气地将其中一本举到我面前。她的学生想知道，为什么小册子里没有涵盖任何材料。如果在第一次实验室课中进行 shell 使用入门教学，会占用她的作业时间，我最好确保这种情况不再发生。它确实没有再发生，由于我的实验室学生不需要在作业之间零散地学习开发环境，他们比其他学生获得了大约三周的领先优势。

许多书籍和许多教师试图将计算机语言与其运行的环境分离开来。这就好比谈论煮鸡蛋，却不说明鸡蛋是将在微波炉中煮、在煎锅中煎、还是在水中煮。环境影响你能做什么以及你如何做。对于 shell 来说也是如此。

所以，不要让不满的监督者阻止你将脚稳稳地扎根于基础知识。就像我第一年的实验室小册子一样，本章提供了关于 *Bourne Again Shell*（再生的 Bourne Shell）的起源及开发原因的背景信息。Shell 编程有其独特的思维模式，快速回顾永远不会是浪费时间。

## 本书使用的符号

本书采用以下标准符号，用于引入新术语、描述命令语法等。

- *斜体* 用于强调文本中的要点和新术语
- *非比例字体* 代表示例 Bash 脚本、命令、开关、文件名和目录
- Bash 是一个缩写，但为了可读性，不使用全大写书写
- Control-K 代表一种按键组合，即按住 Ctrl 键，然后按下 K 键，再释放 Ctrl 键
- Return 键指的是回车键，根据键盘不同，标记为 Return 或 Enter
- 非比例斜体字体表示需要替换为适当文本的值。例如，在 `-o file` 中，单词 `file` 应替换为该开关对应的适当文件。

## Bash 的起源

Shell 是一个运行操作系统命令的程序。在使用常规桌面时，用户使用鼠标选择一个项目，然后对其应用操作，例如高亮显示图标并选择复制。而在 shell 中，人员输入指令（或操作），后跟目标及任何特殊选项。这种反直觉的界面可能会让习惯了常规桌面的新用户感到困惑。

第一个 Unix shell 由 Steven R. Bourne 于 1974 年为第七版 Unix 开发。为纪念其创建者，它被称为 Bourne shell（或 sh），它确立了 Unix shell 的标准，包括大多数 shell 通用的默认美元符号 ($) 提示符。

用户经常不得不重复输入相同的命令。编写程序来重复这些命令需要 C 等高级语言。相反，为 shell 编写命令列表供其执行，就好像 shell 在执行一个排练好的脚本一样，更为有用。随着添加了进行简单判断和循环的功能，这些 shell 脚本可以运行命令，并确定它们成功或失败，采取适当的行动，而无需诉诸另一种语言。当在脚本中以新方式组合命令时，脚本在概念上变成了一个新命令。脚本可以定制和扩展操作系统。

为了尽可能小且开放地设计，任何不必内置于 shell 的功能都没有内置。甚至算术也是由 shell 外部的其他程序执行的。这减慢了 shell 的速度，但当 shell 大部分时间都在等待其他程序或用户时，速度并非重要因素。对于 shell 而言，如果用户需要新的或更好的功能，用户可以编写额外的脚本来提供这些额外功能。

许多竞争性的 shell 开始出现，提供速度和功能上的改进。最常见的两个后继者是 csh，一种基于 C 语言的宽松 shell，以及 Korn shell (ksh)，由 David G. Korn 开发的改进版 Bourne shell。Shell 设计者将命令集成到 shell 中，以提高速度和可移植性，并使 shell 更易于使用。随着 shell 的成熟，成功的功能在 shell 之间自由复制。

Bourne shell 的一个增强版本作为 GNU 项目的一部分开发，供 Linux 操作系统使用。该 shell 被称为 Bash（取自双关语 "Bourne Again Shell"）。这个 shell 与 Steven R. Bourne 创建的最初 shell 兼容，但包含许多增强功能。它还符合 shell 的 POSIX 标准。

Bash 是大多数 Linux 发行版（包括 Red Hat、SuSE、Mandrake、Slackware 和 UnitedLinux）提供的标准 shell。

## 何时程序是 Shell 脚本？

脚本类似于程序，但对于什么构成脚本没有正式定义。它是一种简单的程序，脚本和程序共享许多共同特征。对于没有特殊要求的 Linux 程序员来说，编写 shell 脚本就足够了。

随着 shell 的成熟，它们获得了许多你可能不会期望在一个用于调度命令的程序中找到的功能。大多数 shell，包括 Bash，都可以执行位操作、字符串处理和 TCP/IP 连接。它们具有类型化变量、内置命令和用户定义的函数。Shell 和编程语言之间的界限已经变得模糊。

一般来说，shell 脚本与更复杂的程序之间有两个关键区别。首先，shell 旨在处理短小的、简单的任务。它们缺乏高级语言的严格结构和语义检查。因为假设程序员知道自己在做什么，所以 shell 脚本可以写得很快，对于短脚本来说，这通常是真的。其次，shell 总是缓慢地执行其脚本。虽然大多数 shell 执行某种预处理以加快执行速度，但它们仍然逐行解释和执行。高级语言更快，因为它们几乎总是将程序翻译成机器语言以获得完整的性能。

在处理任何编程问题时，为工作选择合适的工具至关重要。将大型项目作为 shell 脚本开发意味着你的项目运行缓慢且难以维护。用高级语言开发脚本会导致更长的开发时间和更高的成本。

## 结构化 Shell 编程的必要性

Shell 脚本仍然是商业界的主食。由于开发成本高，用高级语言开发一切是不切实际的。许多业务流程仅仅是遵循一系列步骤，之后对结果进行标记和归档。这正是脚本旨在处理的活动类型。

随着时间推移，shell 通过复制其他 shell 的功能收集了新特性。在他的书《*The Human Interface*》（人类界面）中，苹果 Macintosh 界面设计师 Jef Raskin 曾就飞机自动驾驶仪的设计与一位飞行员交谈。该设备设计有五种输入坐标的方式。这样设计的原因是通过模拟其他自动驾驶仪来降低培训成本。然而，一位飞行员指出，飞机操作员负责知道如何操作每件设备，这意味着他必须知道如何用这五种方式调整自动驾驶仪。





许多 Shell，包括 Bash，都发展出了一套针对特定或晦涩用途的特性混合体。就像自动驾驶一样，这些特性应如何使用，以及哪些特性主要是为了兼容性而提供的，往往并不明确。设计不良的脚本通常对其他程序员，甚至对几个月后编写该脚本的同一位程序员来说，几乎无法阅读。

这对严肃的商业脚本构成了问题。开发高级语言解决方案的成本很高，但杂乱的 Shell 脚本在长期维护上可能代价高昂。随着业务需求的改变，以及 Shell 脚本被一代又一代程序员修改，问题会不断升级。

作为经验法则，商业程序永远不会消失。在我最近工作过的一个地方，一个最初用于打印报告的简单 Shell 脚本逐渐演变成了一个基于 Web 的报告系统，并完全具备个性化定制和安全访问功能。原始程序员完全不知道他的脚本会变成什么样。

由于 Bash 固有的开放性和复杂的语法，任何严肃的项目适应某种标准都会受益。Bash 非常宽容，但代价并不低。例如，在 Bash 中添加 2 + 2 有很多方法。正如自动驾驶的例子所示，期望维护脚本的程序员能够应对这种冗余是不切实际的。

同样，Shell 的词引用有时是可选的，有时是必需的，这取决于上下文。以某种引用形式工作的命令，当引号中出现不同的数据时，可能会突然停止工作。

像 Shell 词引用、专用功能或可移植性特性等问题，如果被滥用，会导致维护成本增加和长期开发成本上升。

## 安装 Bash

Bash 是大多数 Linux 发行版的标准 Shell。然而，还有其他可用的 Linux Shell，而且并没有要求某个特定发行版必须包含 Bash。

Bash Shell 是开源软件，在 GNU 公共许可证（GPL）下发布。如果需要安装 Bash，C 语言源代码可从自由软件基金会（http://www.gnu.org）或其下载镜像处免费获取。

Bash 的安装程序可能会随时间变化。完整说明见随源代码附带的 README 文件。然而，安装过程主要是自动化的。基本步骤如下：

1.  运行 `configure` 程序以确定操作系统并验证编译 Bash 所需的特性。
2.  运行 `make` 来构建 Bash。
3.  运行 `make tests`。这将运行诊断测试以确保 Bash 已正确构建。
4.  运行 `make install` 将 Bash 安装到 `/usr/local/` 子目录下。

假设你的 PATH 变量设置正确，你可以在 Shell 提示符下输入 `bash` 来启动 Bash。

如果你在你的计算机上没有超级用户权限，你仍然可以在个人账户下编译和安装 Bash。使用 `configure` 的 `-prefix` 选项来指定安装 Bash 的目录。例如，`-prefix=$HOME` 或 `-prefix=$HOME/bash` 可能是不错的选择。

## Bash 与其他脚本工具

Ksh、Perl 和 Python 与 Bash 相似，但并不相同。

*Korn shell*（*ksh*）是 Bourne shell 的增强版。存在一个称为 *pdksk* 的公共领域版本。Korn shell 在许多商业 Unix 系统上是流行的 Shell。Korn shell 的大多数（并非全部）特性在 Bash 下都适用。例如，两种 Shell 都可以执行按位算术运算。一些特性有不同的名称。Korn shell 内置的 `print` 命令大致等价于 Bash 的 `printf` 命令，而 Korn shell 的 `whence` 命令等价于 `type` 命令。关于差异和移植问题的完整列表可在 Bash FAQ 中查到，地址为 `http://www.faqs.org/faqs/unix-faq/shell/bash/`。

*Perl*（Practical Extraction and Report Language，实用提取和报告语言）顾名思义，是一种用于生成报告的脚本语言。它结合了 Shell 语言、`sed` 命令和 `awk` 命令的特性，创建了一个单一的工具。它不是 Shell，Perl 脚本与 Bash 不兼容。

*Python*（名字取自“Monty Python”喜剧剧团）是一种为需要快速开发的小型项目设计的解释型语言。它不是 Shell，但像 Bash 一样，它包含许多专为交互式会话设计的特性。Python 脚本与 Bash 不兼容。

# 1. Linux 环境

在计算机早期，指令和数据通常分为两个独立的存储区域。现代计算机遵循所谓的“冯·诺依曼体系结构”，这是匈牙利出生的计算机科学家 John von Neumann 提出的一种设计。这些机器对于数据与指令具有单一的存储区域。实际上，指令和数据被视为相同，使得计算机更易于构建和使用。

基于 Unix 的操作系统，包括 Linux，将此原则扩展到长期存储。Linux 将磁盘上的信息组织为文件的集合。无论文件是程序还是数据，都被同等对待，这使得操作系统既易于构建，又灵活易用。针对某种类型文件操作的命令，往往对其他类型文件也有类似的影响，从而减少了程序员需要学习的命令数量。

本章概述了 Linux 操作系统，包括其组织方式及其常见约定。如果你是 Linux 的新手，不期望你能理解这里介绍的所有术语。在这个基础之后，后续章节将通过实际示例来展示这些原则。

## Linux 的起源

Linux 操作系统是一位名叫 Linus Torvalds 的年轻学生在芬兰赫尔辛基大学作为业余爱好创建的。对 Unix 克隆操作系统 Minix 感兴趣的 Linus，想要创建一个具有更多功能的 Minix 扩展版本。他于 1991 年开始这项工作，当时他发布了 0.02 版本并邀请程序员参与他的项目。1.0 版本于 1994 年发布。

Linux 使用 GNU 通用公共许可证（GPL），其源代码对所有人免费开放。Linux 发行版（包含 Linux 内核和其他软件，准备安装于 CD-ROM 上）不必免费，但 Linux 源代码必须保持可用。提供源代码被称为分发开源。

“Linux”这个词通常用瑞典口音发音，这在北美很难说。它最常以短音“i”且重音在第一个音节的方式发音，类似于 LIH-nicks，但有时也发音为 LYE-nicks（英语化的“Linus' Unix”）或 LEE-nicks。

严格来说，Linux 指的是启动和管理其他程序并提供系统资源访问的操作系统内核。各种开源 Shell、编译器、标准库和命令是另一个名为 **GNU** 的项目的一部分。GNU 项目由自由软件基金会（**FSF**）发起，旨在创建 Unix 的自由版本。主要的 Linux C 编译器 *gcc* 是 GNU 项目的一部分。

还有一个 GNU 内核项目，但 Linux 内核在很大程度上已经取代了这一努力。

X Windows 严格来说也不是 Linux 的一部分。Xfree86，X Windows 的开源版本，被适配到 Linux 操作系统，并在不同的许可证下发布。

### 文件和文件系统

每个 Linux 磁盘（或其他长期块存储设备）都包含一组根据称为 *file system*（文件系统）的策略或规则集组织的文件。每个磁盘可以划分为 *partitions*（分区）（或“切片”），每个分区都有其自己的文件系统。Linux 并不限制所有磁盘使用单一的文件系统：用户可以使用其他操作系统创建的磁盘，就像使用本地 Linux 磁盘一样。

标准文件系统是第二扩展文件系统，或 *ext2*。这是 Minix 文件系统的第二版，支持大容量磁盘大小和文件名。ext2 允许分区高达 4TB（太字节），文件高达 2GB（吉字节），以及 255 个字符的文件名。较新的发行版使用 *ext3*，这是 ext2 的版本，具有用于错误恢复的特殊功能。

根据你的发行版和安装选项，可能会提供对其他文件系统的支持。它们可能包括 Microsoft Windows NT、Apple HFS 或日志文件系统。

ext2 文件系统使用缓存来提高性能。如果 ext2 磁盘未正确关闭，文件可能会损坏或丢失。确保 Linux 计算机正确关闭或受到某种不间断电源保护至关重要。

为了节省空间，ext2 中包含大量零的文件（称为 *sparse files*（稀疏文件））实际上并未存储在磁盘上。某些 Shell 命令提供了创建和处理稀疏文件的选项。

每个文件都由名称标识，允许的名称由文件系统决定。出于实用性，名称很少超过 32 个字符，通常由小写字母、下划线、减号和句号组成。例如，空格和标点符号是允许的，但可能会在未预期这些符号的 Shell 脚本中引发问题。





- `.sh`—Bash shell 脚本
- `.txt`—通用文本文件
- `.log`—日志文件
- `.html`—HTML Web 页面
- `.tgz`（或 `.tar.gz`）—压缩文件归档

命令通常没有后缀。

## 目录

Shell 脚本、文本文件、可执行命令和其他常规文件统称为常规文件。它们包含可读取的数据或可执行的指令。此外，还有一些非常规文件，例如目录或命名管道；它们包含独特数据，在被访问时具有特殊行为。

文件被组织成目录，即文件列表。与 Linux 中的所有其他文件一样，目录也被视为文件。每个目录又可以包含子目录，从而创建层次化的列表。

目录被组织成单一的整体树结构。最顶层的目录称为根目录。与某些拥有独立标记磁盘的操作系统不同，Linux 将任何磁盘驱动器都视为主目录结构内的子目录。从用户的角度来看，无法判断某个特定目录属于哪块磁盘：一切都似乎位于单一磁盘上。

路径名（pathname）是一个标识特定文件位置的字符串，即为了找到该文件需要穿行的目录序列。根目录用正斜杠（/）字符表示，因此 `/payroll.dat` 代表一个名为 `payroll.dat` 且位于最顶层目录中的文件。使用更多的目录名和正斜杠可以指定额外的目录。

当用户登录时，他们会进入称为主目录的个人目录。按照惯例，Linux 主目录位于 `/home` 目录之下。路径名 `/home/jgubbis/payroll.dat` 表示用户 `jgubbis` 主目录中一个名为 `payroll.dat` 的文件。在 Bash 中，主目录由波浪号（`~`）表示。当前目录（或工作目录）由点（`.`）表示。如果路径名没有以开头的斜杠开始，Bash 会假定这是相对于当前目录的路径。`./payroll.dat` 和 `payroll.dat` 都指当前目录中一个名为 `payroll.dat` 的文件。在运行程序时，这可能不是事实。这一例外将在下一章中讨论。

父目录由双点（`..`）表示。双点可以用于路径中的任何位置，以向目录树的根部移动，实际上撤销了路径中之前提到的目录。然而，将双点用作路径中的第一个目录最合理。如果当前目录是 `/home/jgubbis`，那么路径名 `../kburch/payroll.dat` 等同于路径名 `/home/kburch/payroll.dat`。双点代表 `/home/jgubbis` 的父目录，即 `/home` 目录。

没有开头斜杠的路径名称为相对路径，因为它们根据当前目录指定文件的位置。相对路径对于表示当前目录或当前目录子目录中的文件非常有用。

带有开头斜杠的路径名称为绝对路径。绝对路径描述文件相对于根目录的位置。无论当前目录在哪里，绝对路径都能精确地标识文件。在定位始终存储在同一位置常见文件时，绝对路径非常有用。

关于文件存放位置并没有固定的规则，其放置由您的 Linux 发行版决定。早期的 Unix 变体将标准程序存储在 `/bin` 中，主目录存储在 `/usr` 中，特定于计算机的程序存储在 `/usr/bin` 中。随着程序数量和类型的增加，常见目录的数量和功能也发生了变化。

大多数 Linux 发行版包含以下目录：

- `*/dev*`—包含设备驱动程序
- `*/bin*` 和 `*/usr/bin*`—包含标准 Linux 命令
- `*/lib*` 和 `*/usr/lib*`—包含标准 Linux 库
- `*/var*`—包含配置和日志文件
- `*/etc*`—包含默认配置文件
- `*/usr/local/bin*`—包含发行版中未包含、由管理员添加的命令
- `*/opt*`—包含商业软件
- `*/tmp*`—存储临时文件
- `*/sbin*` 和 `*/usr/sbin*`—包含系统管理命令（`*/sbin*` 代表“safe” bin）

## inode 和链接

通常，每个文件只在一个目录中列出。Linux 可以为单个文件创建额外的列表项。这些快捷方式称为 *链接*，可以指向任何类型的文件。

链接有两种类型。*硬链接* 是当前目录或不同目录中另一个文件的引用。每当对硬链接执行某种操作时，实际上是对硬链接所引用的文件执行该操作。硬链接访问速度很快，因为它们不需要 *解引用*，但 Linux 限制硬链接可以放置的位置。只要文件被至少一个目录项引用，就不会被删除。例如，如果一个文件有一个硬链接，必须删除该链接和原始文件才能移除该文件。

第二种也是更常见的链接是 *符号链接*。此链接是一个包含另一个文件路径名的文件。与硬链接不同，符号链接对其使用位置没有限制。它们较慢，并且某些命令会影响链接文件本身，而不是链接指向的文件。符号链接不是“硬”的，因为它们必须被解引用：当 Linux 打开符号链接文件时，它会读取正确的路径名并打开该文件。当被引用的文件被删除时，符号链接文件就会变成一个指向不存在文件的 *悬空链接*。

使用链接意味着两个不同的路径名可以指示同一个文件。为了标识特定文件，Linux 为每个文件分配一个数字。这个数字称为 *inode*（或“索引节点”），对于任何存储设备都是唯一的。如果两个路径名引用具有相同 inode 的文件，则其中一个路径是硬链接。

在 ext2 文件系统中，inode 的数量有限，这反过来限制了磁盘上可存储的文件数量。inode 数量与磁盘空间量的比值称为 *inode 密度*。密度在磁盘或分区初始化时指定。大多数 Linux 发行版使用 4K 的 inode 密度，即每 4096 字节磁盘空间一个节点。

## 管道和套接字文件

*管道文件* 是两个程序之间共享的一种特殊文件。该文件作为共享信息的缓冲区。一个程序写入管道文件，另一个程序从管道读取。当管道文件达到特定大小时，Linux 会停止写入程序，直到读取程序能够“跟上”。

一种类似的 *UNIX 域套接字文件* 就像管道一样工作，但使用网络套接字。然而，这种文件在 shell 脚本中不太容易使用，且本书不会涵盖。

## 设备文件

最后一个常见的非常规文件类型是 *设备文件*。遵循 Linux 的文件导向设计，设备由文件表示。设备文件允许与计算机上连接的特定设备进行直接通信。实际上有两类设备文件，但 shell 程序员主要关注称为 *字符设备文件* 的类型。

所有设备文件都位于 `/dev` 目录中。尽管 `/dev` 中列出了许多文件，但并非所有这些设备实际都存在。相反，`/dev` 包含了一个可以连接到您计算机的设备列表，因为 Linux 内核被配置为识别这些设备如果它们被连接。

这些文件中的大多数对普通用户不可访问，但有几个对通用使用开放。所有用户都可以访问的一个重要设备文件是 `/dev/null`。此文件代表一个连接到您计算机的虚拟“黑洞”设备，它消耗发送到它的一切内容。这对于丢弃 shell 命令中不需要的响应很有用。也可以读取 `/dev/null`，但该文件始终为空。

另一个设备文件是 `/dev/zero`。此文件包含无尽的零流，可用于创建完全由零填充的新文件。

根据您的发行版和计算机硬件，`/dev` 中可能会出现各种其他设备。常见的设备文件包括：





- `/dev/tty` — 你的程序正在运行的终端窗口（或控制台）
- `/dev/dsp` — 在声卡上播放 AU 音频文件的接口
- `/dev/fd0` — 第一个软盘驱动器
- `/dev/hda1` — 第一个 IDE 驱动器分区
- `/dev/sda1` — 第一个 SCSI 驱动器分区

由于历史原因，*tty* 这个名称是“电传打字机”（teletypewriter）的缩写，这是一种通过电缆连接到计算机的打印机和键盘组合设备。

通过概览 Linux 的哲学理念，你现在已经准备好开始通过 Bash shell 使用 Linux 了。

## 2 操作 Shell

有一天，我父亲正在他的平底船上进行电路布线工作。他忙了好几个小时，但仍未成功。无论他尝试什么方法，都无法让他的航行灯正常工作。在感到挫败时，他关闭了灯开关……结果灯亮了。

本章简要介绍了如何在 Bash 命令提示符下进行交互式会话时如何使用 shell。就像我父亲和他的布线问题一样，在深入脚本的复杂细节之前，理解命令在基础的交互层面如何工作是至关重要的。除非你喜欢意想不到的惊喜。

### Bash 关键字

*关键字*是对计算机语言具有特殊含义的单词或符号。以下符号和单词在 Bash 中未加引号且作为命令的第一个词时具有特殊含义。

| | | | | |
|---|---|---|---|---|
| ! | esac | select | } | |
| case | fi | then | [[ | |
| do | for | until | ]] | |
| done | function | while | | |
| elif | if | time | | |
| else | in | { | | |

与大多数计算机语言不同，Bash 允许将关键字用作变量名，尽管这可能会使脚本难以阅读。为了使脚本易于理解，不应将关键字用作变量名。

### 命令基础

可以在 Bash shell 提示符处输入的命令通常存储在文件系统外部的 Linux 程序。有些命令内置于 shell 中，以便提高速度、标准化，或者因为它们在非内置情况下无法正常工作。

无论其来源如何，命令可分为几个非正式的类别。*实用工具*是在许多应用程序中都有用的通用命令，例如返回日期或统计文件中的行数。

*过滤器*是获取一个命令的结果并以某种方式对其进行修改的命令，例如删除不需要的行或将一个单词替换为另一个单词。许多命令在适当的情况下都充当过滤器。

要执行命令，请在 Bash 命令提示符处输入它。提示符通常是 $，但 Linux 发行版通常会将其自定义为其他内容。例如，S.u.S.E. 使用 > 命令提示符。

*date* 命令会在屏幕上打印当前日期和时间。

```bash
$ date
Wed Apr 4 10:44:52 EDT 2001
```

所有文件，包括 shell 命令，都是区分大小写的。按照惯例，所有 shell 命令均为小写。

```bash
$ DATE
bash: DATE: command not found
```

*参数*是提供给命令以改变其行为的其他信息。*date* 命令接受格式参数来更改日期和时间的显示方式。

```bash
$ date '+%H:%M'
10:44
```

*开关*（也称为“选项”或“标志”）是前面带有减号字符的字符，用于启用命令功能。若要查看协调世界时（UTC， formerly 称为 GMT）的日期，请使用 -u 开关。

```bash
$ date -u
Wed Apr 4 14:46:41 UTC 2001
```

由于“选项”和“标志”这两个术语在多种情境中使用，因此本书中将其称为开关。

开关和参数统称为*参数*。某些命令允许任意数量的参数，或者具有可以复杂排列的参数。

GNU 和 Linux 的惯例是，更长、更易读的选择项前面带有双减号。-u 开关的较长等效项是 --universal。

```bash
$ date --universal
Wed Apr 4 14:46:41 UTC 2001
```

长开关让读者确切知道该开关的作用。这使得将来调试 shell 脚本变得更加容易，因为 Linux 命令中的短开关没有标准惯例。大多数 Linux 命令识别长开关 --help、--verbose 和 --version。

可以在任何命令末尾添加注释，也可以单独放在一行上。注释用井号 (#) 标记。

```bash
$ date --universal # show the date in UTC format
```

内置的 Bash 命令和大多数其他 GNU 软件将 -- 视为一种特殊开关，表示开关列表的结束。当某个参数以减号开头时，可以使用此功能。

### 命令行编辑

有特殊的键组合用于编辑输入的内容或重复以前的命令。

Bash 有两种编辑模式。这些模式模拟了两个流行的 Linux 文本编辑器中使用的按键。*Vi 模式*模仿 vi 和 vim 编辑器。*Emacs 模式*的工作方式类似于 emacs、nano 或 pico。

当前编辑模式可以使用 `shopt` 命令进行检查。如果你处于 emacs 模式，则 `shopt -o emacs` 为 on（开）。如果你处于 vi 模式，则 `shopt -o vi` 为 on（开）。一次只能开启一种模式。

```bash
$ shopt -o emacs
emacs on
$ shopt -o vi
vi off
```

无论处于何种模式，箭头键都会移动光标并逐步遍历最近执行的命令：

- *左箭头* — 向左移动一个字符。不会擦除任何字符。
- *右箭头* — 向右移动一个字符。
- *上箭头* — 移动到命令历史中的上一条命令。
- *下箭头* — 移动到命令历史中的下一条命令（如果存在）。

使用左箭头和右箭头，光标可以移动到命令中的任意位置。在行的中间，新文本将插入到该行中，而不会覆盖旧的输入。

Emacs 模式是所有主要 Linux 发行版的默认模式。最常见的 emacs 键如下：

- **control-b** — 向左移动一个字符。不会擦除任何字符。
- **control-f** — 向右移动一个字符。
- **control-p** — 移动到命令历史中的上一条命令。
- **control-n** — 移动到命令历史中的下一条命令（如果存在）。
- **Tab 键** — 查找匹配的文件名，如果只有一个精确匹配，则完成它。

文件名自动补全功能尝试查找以行中最后一个单词开头的匹配文件名。如果找到匹配的文件名，Bash 将输入文件名的其余部分。例如，

```bash
$ dat
```

当按下 Tab 键时，将补全为

```bash
$ date
```

前提条件是 *date* 是仅能找到以 *dat* 字符开头的唯一命令。vi 模式的键组合如下：

- Esc — 进入/退出编辑模式。
- h — 向左移动一个字符。不会擦除任何字符。
- l — 向右移动一个字符。
- k — 移动到命令历史中的上一条命令。
- j — 移动到命令历史中的下一条命令（如果存在）。
- 按两次 Esc — 查找匹配的文件名，如果只有一个精确匹配，则完成它。

完整的键组合（或绑定）列表列在 Bash man 手册页的 Readline 部分中。可以使用 bind 命令更改、列出或重新分配默认键组合。为了避免混淆，除非你有特定的应用目标，否则最好使用默认设置。

其他编辑键由较旧的 Linux stty（设置电传打字）命令控制。运行 *stty* 会显示常用命令键以及其他关于你会话的信息。使用 -a（all）开关可查看所有设置。

```bash
$ stty
speed 9600; baud: evenp hupcl
intr = ^C; erase = ^?; kill = ^X;
eof = ^D; swtch = ^@;
susp = ^Z; dsusp = ^V;
werase = ^W; lnext = ^@;
-isrpc -istrip icrnl -ixany ixoff onlcr
-iexten echo echoe echok
-echoctl -echoke
```

这些设置中的许多仅在你处理串行端口设备时使用，否则可以忽略。其他设置是带有 caret (^) 符号的控制键组合。带有 ^@（或 ASCII 0）的键未定义。键的作用如下：

- *erase*（通常是 ^?，在 IBM 风格键盘上是退格键） — 向左移动并擦除一个字符。
- *intr*（通常是 ^C） — 中断/停止当前程序或取消当前行。
- *kill*（通常是 ^X） — 擦除当前行。





## 终端信号字符

- **rpint** (通常是 ^x) — 重绘当前行。
- **stop** (通常是 ^s) — 暂停程序，以便你在屏幕上阅读结果。
- **start** (通常是 ^q) — 恢复程序运行。
- **susp** (通常是 ^z) — 挂起当前程序。
- **werase** (通常是 ^w) — 擦除最后键入的单词。

要将挂起字符更改为 control-v，请键入：

```bash
$ stty susp '^v'
```

更改按键组合可能非常困难。例如，如果你在 Microsoft Windows 计算机上运行 X Windows 服务器（在客户端计算机上运行的软件）以访问 Linux 计算机，按键组合可能会受到以下因素的影响：

- Microsoft Windows
- X 服务器软件
- Linux 窗口管理器
- stty 设置

它们各自就像洋葱的一层，必须所有层达成一致。例如，Shift-Insert（常用来粘贴文本）可能在你的 Linux 计算机或 shell 有机会看到它之前，就被你的 X Window 服务器处理了。

## 变量赋值和显示消息

可以使用等号创建变量并为其分配文本。用双引号将文本包围起来。

```bash
$ FILENAME="info.txt"
```

变量的值可以使用 `printf` 命令打印出来。`printf` 有两个参数：一个格式化代码，以及要显示的变量。对于简单变量，格式化代码是 "%s\n"，变量名应出现在双引号内，并且名称前需要一个美元符号。

```bash
$ printf "%s\n" "$FILENAME"
info.txt
```

`printf` 还可以显示简单消息。将消息放在格式化代码的位置。

```bash
$ printf "Bash is a great shell.\n"
Bash is a great shell.
```

`printf` 和变量在 shell 脚本中起着重要作用，后续章节将对它们进行更详细的描述。

可以使用反引号将命令的结果赋值给变量。

```bash
$ DATE=`date`
$ printf "%s\n" "$DATE"
Wed Feb 13 15:36:41 EST 2002
```

显示的日期是变量 `DATE` 被赋值时的日期。变量的值保持不变，直到分配新值。

```bash
$ printf "%s\n" "$DATE"
Wed Feb 13 15:36:41 EST 2002
$ DATE=`date`
$ printf "%s\n" "$DATE"
Wed Feb 13 15:36:48 EST 2002
```

## 多个命令

多个命令可以组合在单行中。它们的执行方式取决于分隔它们的符号。

如果每个命令由分号分隔，则命令按顺序依次执行，一个接一个。

```bash
$ printf "%s\n" "This is executed"; printf "%s\n" "And so is this"
This is executed
And so is this
```

如果每个命令由双与号（`&&`）分隔，则命令会执行直到其中一个失败，或者直到所有命令都执行完毕。

```bash
$ date && printf "%s\n" "The date command was successful"
Wed Aug 15 14:36:32 EDT 2001
The date command was successful
```

如果每个命令由双竖线（`||`）分隔，则命令会执行直到每个都失败，或者直到所有命令都执行完毕。

```bash
$ date `duck' || printf "%s\n" "The date command failed"
date: bad conversion
The date command failed
```

分号、双与号和双竖线可以在单行中自由混合使用。

```bash
$ date `format-this!' || printf "%s\n" "The date command failed" && printf "%s\n" "But the print didn't!"
date: bad conversion
The date command failed
But the print didn't!
```

这些主要作为命令行快捷键。当与重定向运算符（如 `>`）混合使用时，长的命令链很难阅读，在脚本中应避免使用。

## 命令历史

Bash 会保留最近键入的命令列表。这个列表就是*命令历史*。

浏览命令历史最简单的方法是使用向上和向下箭头键。也可以使用感叹号（`!`）搜索历史。这表示 Bash 将补全的命令名称的开始部分。Bash 会执行匹配到的最近命令。例如：

```bash
$ date
Wed Apr 4 11:55:58 EDT 2001
$ !d
Wed Apr 4 11:55:58 EDT 2001
```

如果没有匹配的命令，Bash 会回复 `event not found` 错误信息。

```bash
$ !x
bash: !x: event not found
```

双 `!!` 会重复上一条命令。

```bash
$ date
Thu Jul 5 14:03:25 EDT 2001
$ !!
date
Thu Jul 5 14:03:28 EDT 2001
```

`!` 命令有许多变体，以在特定情况下提供快捷键。

负数表示相对行号。也就是说，它表示在历史中向前移动的指令数量以找到要执行的命令。`!-1` 等同于 `!!`。

```bash
$ date
Thu Jul 5 14:04:54 EDT 2001
$ printf "%a\n" $PWD
/home/kburch/
$ !-2
date
Thu Jul 5 14:05:15 EDT 2001
```

`!#` 会重复当前命令行内容。（不要将此与 shell 脚本中的 `#!` 混淆。）使用此功能可以运行一组命令两次。

```bash
$ date ; sleep 5 ; !#
date ; sleep 5 ; date ; sleep 5 ;
Fri Jan 18 15:26:54 EST 2002
Fri Jan 18 15:26:59 EST 2002
```

除非定义了名为 `HISTFILE` 的变量，否则 Bash 会在名为 `.bash_history` 的文件中保留命令历史。每次退出 Bash 会话时，Bash 都会将会话历史保存到历史文件中。如果 `histappend` shell 选项开启，历史将追加到旧历史中，直到历史文件的最大允许大小。每次启动 Bash 会话时，历史都会再次从文件中加载。

另一个 shell 选项 `histverify` 允许你在检索命令后编辑它，而不是立即执行。

Bash 有一个内置命令 `history`，可以完全控制命令历史。不带参数的 `history` 命令会列出命令历史。如果你不想看到完整的历史，可以指定要显示的命令行数。

```bash
$ history 10
  1026  set -o emacs
  1027  stty
  1028  man stty
  1029  stty -a
  1030  date edhhh
  1031  date edhhh
  1032  date
  1033  date
  1034  !
  1035  history 10
```

你可以使用 `-p` 开关测试在历史补全期间哪个命令会被匹配。

```bash
$ history -p id
history -p date
date
```

特定的命令行可以通过行号来引用。

```bash
$ !1133
date
Thu Jul  5 14:09:05 EDT 2001
```

`history -d` 删除历史中的条目。

```bash
$ history -d 1029
$ history 10
  1027  stty
  1028  man stty
  1029  date edhhh
  1030  date edhhh
  1031  date
  1032  date
  1033  !
  1034  history 10
  1035  history -d 1029
  1036  history 10
```

`-s` 开关添加新的历史条目。`-w` (write) 和 `-r` (read) 分别将历史保存或从文件加载。`-a` (append) 开关将当前会话历史追加到历史文件中。退出 shell 时会自动执行此操作。`-n` 开关从历史文件加载完整历史。`history -c` (clear) 删除整个历史。

可以使用 `!?` 搜索命令历史中包含文本的最近命令。如果在 `!?` 搜索后还有额外键入，命令片段将用尾部的 `?` 分隔。

```bash
$ date
Thu Jul 5 14:12:33 EDT 2001
$ !?ate
date
Thu Jul 5 14:12:38 EDT 2001
$ !?da? '+%Y'
date '+%Y'
2001
```

快速替换历史命令 `^` 会再次运行上一条命令，将一个字符串替换为另一个。

```bash
$ date '+%Y'
2001
$ ^'+%Y'='+'
date '+%m'
07
```

通过取消设置 `-o history` shell 选项，可以关闭 Bash 历史。`cshhist` 选项在历史中保存多行命令。`lithist` 选项将用分号分隔的命令拆分为独立的行。

## 目录命令

内置的 `pwd` (present working directory，当前工作目录) 命令返回你当前目录的名称。

```bash
$ pwd
/home/kburch
```

虽然你可能认为如此简单的命令不需要选项，但 `pwd` 有几个开关。`-P` (physical，物理) 开关显示实际目录，而默认的 `-L` (logical，逻辑) 开关显示目录，包括任何符号链接。例如，如果 `/home` 是名为 `/user_drive/homes` 的目录的链接，那么开关的工作方式如下：

```bash
$ pwd -P
/user_drive/homes/kburch
$ pwd -L
/home/kburch
```




# 第 3 章：文件、用户和 Shell 自定义

当我的一个朋友得到一台新的 Unix 计算机时，控制台显示看起来不太对劲。当我们尝试查看文件时，操作系统不知道屏幕有多大。它显示整个文件，而不是一次显示一屏。

当时我的 Unix 知识有点生疏，但我记得有一个 `stty` 命令可以更改显示属性。查看 `stty` 的帮助列表时，我注意到可以设置行数（rows）和行（line）。我认为“line”一定是显示屏幕上的行数，所以我输入了 `stty line 24`。计算机停止响应，迫使我们重新启动了它。

我们打电话给了一位拥有相同操作系统的 Unix 专业人士。他说：“那应该是有效的。让我试试。”过了一会儿，他说：“我的电脑也卡住了。”

事实证明，`stty line 24` 设置的是显示用的串行端口，将其更改为端口 24，尽管端口 24 上并没有连接任何设备。由于像 Linux 这样的基于 Unix 的操作系统拥有多种选择，有时很难预测命令实际执行的操作。本章扩展了上一章的内容，涵盖了更多基本命令及其众多有时令人困惑的选项。

## 列出文件

`ls` (*list*) 命令显示当前目录的内容。虽然 `ls` 是所有类 Unix 操作系统中通用的熟悉命令，但 Linux 使用来自 GNU `fileutils` 项目的 `ls` 命令，并具有许多特殊的开关和功能。

```bash
$ ls
archive  check-orders.sh  orders.txt
```

`ls` 有影响文件列出方式的开关，包括详细程度、排序顺序和列数。大多数 Linux 发行版为 `ls` 命令设置了某些默认值。例如，Red Hat 默认开启 `-q` 和 `-F` 开关。从编写脚本的角度来看，如果在脚本中使用 `ls` 命令而不指定适当的开关是不安全的，因为你无法确定特定发行版使用哪些默认值。

`ls` 会隐藏以句点开头的文件。这是 Linux 中用于配置文件、历史记录文件以及其他用户通常不感兴趣的文件的惯例。要查看这些文件，请使用 `-a` (all) 开关。使用 `-A` (absolutely all) 还可以显示隐含的 `.` 和 `..` 文件。

```bash
$ ls -A
.bash_history .bash_logout .bash_profile .bashrc archive
check-orders.sh orders.txt
```

文件名可以以彩色打印，以显示其文件类型。颜色在文件 `/etc/DIR_COLORS` 中定义。你可以使用自己目录中的 `.dir_colors` 文件来自定义颜色。该文件的格式在 `/etc/DIR_COLORS` 文件中有描述。

要显示不带颜色而带符号的文件，请使用 `--color` 和 `--classify`（或 `-F`）开关。（在大多数 Linux 发行版中，此功能通过别名开启。）

```bash
$ ls --color=never --classify
archive/ check-orders.sh* orders.txt
```

`--classify` 的符号包括目录（`/`）、程序（`*`）、符号链接（`@`）、管道（`|`）和 Unix 域套接字文件（`=`）。这些符号不是名称的一部分：它们是关于文件类型的提示。在此示例中，`archive` 是一个目录，`check-orders.sh` 是一个程序。

另一个非常重要的开关是 `--hide-control-chars`（或 `-q`）。Linux 文件名可以包含任何字符，甚至包括控制字符。可以使用隐藏字符创建文件名。在这种情况下，除非知道隐藏字符是什么，否则无法重命名或删除该文件。与名称的含义相反，`--hide-control-chars` 开关将文件名中不可打印的字符显示为问号，从而使其位置可见。

```bash
$ rm orders.txt
rm: orders.txt: non-existent
$ ls --color=never --classify --hide-control-chars
archive/ check-orders.sh* orders.txt?
```

完整的开关列表出现在本章末尾。

## printf 命令

内置的 `printf` (*print formatted*) 命令在屏幕上打印消息。你将在 shell 脚本中大量使用此命令。

`printf` 与 C 标准 I/O 的 `printf()` 函数非常相似，但它们并不完全相同。特别是，单引号和双引号字符串在 shell 脚本中的处理与在 C 程序中的处理不同。

内置的 `cd` (change directory) 命令更改当前目录。如第 1 章“Linux 环境”中所述，特殊目录 `..` 表示父目录，而 `.` 表示当前目录。

```bash
$ pwd
/home/ikburtch
$ cd .
$ pwd
/home/ikburtch
$ cd ..
$ pwd
/home
$ cd kburtch
$ pwd
/home/ikburtch
```

每次更改目录时，Bash 都会更新包含当前工作目录路径的变量 `PWD`。Bash 还维护第二个名为 `OLDPWD` 的变量，其中包含你所在的上一个目录。

使用减号（`-`）配合 `cd`，可以在当前目录和上一个目录之间切换。如果在两个不同的目录中工作，这是一个有用的快捷方式。

```bash
$ pwd
/home/ikburtch
$ cd ..
$ pwd
/home
$ cd -
$ pwd
/home/ikburtch
$ cd -
$ pwd
/home
```

波浪号（`~`）代表你的主目录。使用它移动到相对于主目录的目录。要移动到主目录中名为 `mail` 的目录，请输入：

```bash
$ cd ~/mail
```

虽然 `.` 和 `..` 在所有 Linux 程序中都能工作，但 `~` 和 `-` 是 Bash 的功能，仅在 Bash 和 Bash 脚本中有效。

单独使用 `cd` 会返回到你的主目录，效果等同于 `cd ~`。

如果存在 `CDPATH` 变量，则假设它包含类似 `PATH` 变量的目录列表。这是对过去用户只能在终端上使用一个 shell 会话时代的回顾，现在被视为安全风险。应避免使用它。

## 专用导航和历史记录

由于大多数用户可以打开多个 shell 会话，因此对目录之间复杂移动的需求很小。`cd -` 在两个目录之间切换，适用于大多数情况。然而，如果你局限于单个 shell 会话并希望 Bash 记住更多目录，有三个内置命令维护目录列表。

内置的 `dirs` 命令显示已保存目录的列表。当前目录始终是列表中的第一项。

```bash
$ dirs
~
```

内置的 `pushd` (push directory) 命令将目录添加（或压入）到列表中，并将当前目录更改为新目录。

```bash
$ pushd /home/kburtch/invoices
~/invoices
$
$ pushd /home/kburtch/work
~/work ~/invoices
$
$ pwd
/home/kburtch/work
```

现在列表中有三个目录。

`-n` (no change) 开关将目录放入列表中而不更改目录。`-N` (rotate Nth) 将左侧第 n 个目录（或者，如果使用 `+N`，则从右侧）移动到列表顶部。

`dirs -l` 开关显示不带任何简写形式的目录名称。

```bash
$ dirs -l
/home/kburtch/work /home/kburtch/invoices /home/kburtch
```

`-v` 开关以单列显示列表，而 `-p` 显示相同的信息但不含列表位置。`-c` 开关清除列表。`-N` (view Nth) 显示左侧第 n 个目录（或者，如果使用 `+N`，则从右侧）。

```bash
$ dirs +1
~
```

内置的 `popd` (pop directory) 命令与 `pushd` 相反。`popd` 丢弃第一个目录并移动到列表中的下一个目录。

```bash
$ popd
~/invoices
$
$ pwd
/home/kburtch/invoices
```

`popd` 的开关类似于 `pushd`：`-n` 弹出而不移动，`-N` 删除左侧第 N 个条目（或者，如果使用 `+N`，则从右侧）。

## 冒号命令

最简单的 shell 命令是冒号（`:`）。这是*冒号命令*（有时称为“空操作”或“null 命令”），什么都不做。一个什么也不做的命令有什么用？在 shell 程序中有一些地方需要语句。在这些情况下，可以使用 `:` 来表示不需要执行特殊操作。

在命令提示符处，`:` 没有效果。

```bash
$ :
$
```

冒号命令可以带有参数和文件重定向。这可能会产生奇怪的效果，例如使用反引号运行 `date` 命令，将结果传递给静默丢弃它们的空命令。

```bash
$ : `date`
$
```

这与将 `date` 的输出重定向到 `/dev/null` 文件具有相同的效果。

```bash
$ date > /dev/null
```

反引号和重定向将在后续章节中讨论。

## 参考部分

## date 命令开关

- **--date=$s** (或 -d $s) — 显示 $s 描述的时间。
- **--file=$f** (或 -f $f) — 显示文件 $f 中列出的时间。
- **--iso-8601=t** (或 -I $t) — 显示 ISO-8601 标准时间。
- **--reference=$f** (或 -r $f) — 显示文件的最后修改日期。
- **--rfc-822** (或 -R) — 使用 RFC-822 格式。
- **--universal** (或 --utc 或 -u) — 使用协调世界时。

## stty 命令开关

- **--all** (或 -a) — 显示所有 stty 设置。
- **--save** (或 -g) — 显示设置，以便将其用作 stty 的参数。
- **--file=$d** (或 -F $d) — 打开 tty 设备 $d 而不是 stdin。

## history 命令开关

- **-a** — 追加到历史记录文件。
- **-c** — 清除历史记录。
- **-d** — 删除历史记录条目。
- **-n** — 从历史记录文件加载。
- **-p** — 执行历史记录查找/替换。
- **-r** — 从文件读取历史记录。
- **-s** — 添加新的历史记录条目。

## pwd 命令开关

- **-P** — 物理目录
- **-L** — 逻辑目录

## dirs 命令开关

- **-c** — 清除所有条目
- **-l** — 显示长列表（不使用波浪号）
- **-p** — 列出条目
- **-v** — 显示详细列表




第一个参数是一个格式字符串，描述要打印的项目将以何种形式表示。例如，特殊格式代码 `%d` 代表整数，而代码 `%f` 代表浮点数。

```bash
$ printf "%d\n" 5
5
$ printf "%f\n" 5
5.000000
```

为你想要打印的每个项目包含一个格式代码。打印时，每个格式代码会被替换为相应的值。格式字符串中不属于格式指令的字符将被视为可打印字符。

```bash
$ printf "There are %d customers with purchases over %d.\n" 50 20000
There are 50 customers with purchases over 20000.
```

`printf` 有时用于将变量或固定输入重定向到命令。例如，假设你只想将一个变量通过管道传递给命令。除了使用 `printf` 之外，Bash 提供了一个快捷方式 `<<<` 重定向操作符。`<<<` 将字符串重定向到命令，就好像是通过 `printf` 传递管道数据一样。

`tr` 命令可以将文本转换为大写。下面的示例展示了使用 `printf` 和 `<<<` 将错误消息转换为大写的情况。

```bash
$ printf '%s\n' "$ERRMSG" | tr [[:lower:]] [[:upper:]]
WARNING: THE FILES FROM THE OHIO OFFICE HAVEN'T ARRIVED.
$ tr [[:lower:]] [[:upper:]] <<< "$ERRMSG"
WARNING: THE FILES FROM THE OHIO OFFICE HAVEN'T ARRIVED.
```

格式代码包括以下内容：

- `%a`—以小写十六进制格式表示浮点数
- `%A`—以大写十六进制格式表示浮点数
- `%b`—扩展反斜杠序列
- `%c`—表示单个字符
- `%d`—显示带符号的数字
- `%e`—显示浮点数，采用指数（也称为“科学”）计数法
- `%f`（或 `%F`）—显示不带指数计数法的浮点数
- `%g`—（通用）让 Bash 根据数值选择 `%e` 或 `%f`
- `%i`—与 `%d` 相同
- `%o`—显示八进制数
- `%q`—对字符串进行引用，以便 shell 脚本能正确读取
- `%s`—显示未引用的字符串
- `%u`—显示无符号数字
- `%x`—显示无符号十六进制数，使用小写字母
- `%X`—显示无符号十六进制数，使用大写字母
- `%%`—显示百分号

如果数字过大，Bash 会报告超出范围的错误。

```bash
$ printf "%d\n" 123456789123456789012
bash: printf: warning: 123456789123456789012: Numerical result out of range
```

为了与 C 语言的 `printf` 兼容，Bash 还识别以下标志，但处理方式与 `%d` 相同：

- `%j`—C 语言的 `intmax_t` 或 `uintmax_t` 整数
- `%t`—C 语言的 `ptrdiff_t` 整数
- `%z`—C 语言的 `size_t` 或 `ssize_t` 整数

同样为了兼容 C 语言，你可以使用 `l` 或 `L` 作为格式代码的前缀，以表示长数字。

`%q` 格式在 shell 脚本编程中非常重要，将在第 5 章“变量”的引用部分中讨论。

为了创建具有整齐列的报告，数字可以处理许多格式代码以指示列宽。例如，“%10d”会在一个宽度为 10 个字符的列中打印带符号的数字。

```bash
$ printf "%10d\n" 11
      11
```

同样，负数会左对齐列。

```bash
$ printf "%-10d %-10d\n" 11 12
11         12        
```

带有小数点的数字表示列宽和最小位数（对于浮点值则是小数位数）。例如，“%10.5f” 表示在一个 10 个字符宽的列中显示浮点数，且至少有五位小数。

```bash
$ printf "%10.5f\n" 17.2
   17.20000
```

最后，撇号（`'`）会根据当前国家区域设置，显示带有千位分隔符的数字。

- `\b`—退格
- `\e`—换页（即在打印机上弹出页面）
- `\n`—换行
- `\r`—回车
- `\t`—制表符
- `\v`—垂直制表符
- `\'`—单引号字符（为了与 C 语言兼容）
- `\\`—反斜杠
- `\on`—`n` 是一个八进制数，代表一个 8 位 ASCII 字符

```bash
$ printf "Two separate\nlines\n"
Two separate
lines
```

任何 8 位字节或 ASCII 字符都可以通过 `\0` 或 `\` 加上其八进制值来表示。

```bash
$ printf "ASCII 65 (octal 101) is the character \0101\n"
ASCII 65 (octal 101) is the character A
```

`printf` 识别以零开头的数字为八进制表示，以 0x 开头的数字为十六进制表示。因此，`printf` 可以在这些不同的进制之间转换数字。

```bash
$ printf "\4\n" 010
8
```

```bash
$ printf "\8\n" 0xF
15
```

```bash
$ printf "0x%x\n" 15
0xF
```

```bash
$ printf "%o\n" 8
010
```

大多数 Linux 发行版还有一个独立的 `printf` 命令，以符合 POSIX 标准。

## 获取帮助

Bash shell 自带一个 `help` 命令，用于描述各种内置的 Bash 命令。`-s` 开关会显示你所指定命令的摘要。

```bash
$ help -s printf
printf: printf format [arguments]
```

`help` 仅描述 Bash 命令。若要获取 Linux 命令的帮助，你需要使用 `man`（手册）命令。

```bash
$ man date
```

Linux 将其手册页分为多个逻辑卷。`man` 会显示任何卷中匹配的任何条目。第 1 卷包含你可以从 shell 执行的命令。若要限制搜索范围仅为 shell 命令，请使用 `man 1`。

```bash
$ man 1 date
```

如果多个手册卷中都有页面，则只显示第一个匹配卷中的页面。要在所有手册卷中查找匹配页面，请使用 `-a`（all）开关。

`-k` 开关在 Linux 手册中搜索特定关键字，并列出所有提及该关键字的手册页。

```bash
$ man 1 -k alias
```

命令 `help type` 提供的信息与 `man 1 type` 不同。`help type` 命令告知你关于 Bash 内置的 `type` 命令的信息，而 `man 1 type` 命令告知你关于 Linux `type` 命令的信息。如果你不确定某个命令是否是 Bash 命令，请始终先尝试使用 `help` 命令，然后再使用 `man` 命令。

## 修复显示

有时 Bash 会话会变得不可用。某些字符序列可能会锁定你的显示、隐藏你输入的内容，或将显示的字符变为奇怪的符号。例如，当你试图显示二进制文件时，这种情况可能会发生。

`reset` 命令尝试将 Bash 会话恢复到安全、合理的状态。如果 `reset` 失败，你可能还需要使用 `stty sane` 将会话恢复到正常状态。

`clear` 命令清除显示并将光标返回到左上角。

## 处理文件

有几个 Linux 命令用于删除、复制和移动文件。

`mkdir`（make directory）创建一个新目录。使用 `mkdir` 来组织你的文件。

```bash
$ mkdir prototypes
$ ls -l
total 4
drwxr-xr-x   2 ken     users        4096 Jan 24 12:50 prototypes
```

`mkdir` 有两个开关：

- `--mode=m`（`-m`）—设置权限模式（如 `chmod` 中那样）
- `--parents`（`-p`）—即使当前不存在，也会创建所有必要的目录

```bash
$ mkdir --parents --mode=550 read_only/backup/january
$ ls -l
total 4
drwxr-xr-x  2 ken      users      4096 Jan 24 12:50 backup
drwxr-xr-x  3 ken      users      4096 Jan 24 12:51 read_only
$ ls -l read_only/backup
total 4
dr-xr-x---  2 ken      users      4096 Jan 24 12:51 january
```

模式值将在第 15 章“Shell 安全”中结合 `chmod` 命令讨论。但是，当使用 `--parents` 时，`--mode` 仅影响列表中的最后一个目录。

`rmdir`（remove_directory）删除一个目录。在删除目录之前，该目录必须是空的。有两个开关：

- `--ignore-fail-on-non-empty`—当无法删除仍包含文件的目录时，不报告错误
- `--parents`（`-p`）—除了子目录外，还删除所有父目录

```bash
$ rmdir read_only
rmdir: read_only: Directory not empty
$ rmdir --parents read_only/backup/january/
```

`rm`（remove）命令永久删除文件。如果文件是符号链接或硬链接，它只移除链接，而保留文件本身完整。

```bash
$ rm old_notes.txt
$ ls old_notes.txt
ls: old_notes.txt: No such file or directory
```

`rm` 有几个开关：

- `--directory`（`-d`）—删除目录
- `--force`（`-f`）—从不提示用户，并忽略缺失的文件
- `--interactive`（`-i`）—始终提示用户
- `--recursive`（`-r` 或 `-R`）—删除所有子目录的内容

同时使用 `--recursive` 和 `--force` 开关会删除所有指定的文件（包括所有子目录），且不会发出警告。请确保你删除的是正确的文件。

一些 Linux 发行版默认开启 `--interactive` 开关，以便在使用 `rm` 删除特定文件时需要你确认。

```bash
$ rm --interactive old_notes.txt
rm: remove ‘old_notes.txt’? y
$
```

通常 `rm` 不会删除目录，但 `--recursive` 开关会删除遇到的任何目录。

`cp`（copy）命令将文件从一个位置复制到另一个位置。如果列出的最后一个文件是目录，`cp` 会将其他文件复制到该目录中。





# 第 3 章 文件、用户与 Shell 自定义

`cp`（复制）命令有许多开关选项——完整列表见本章末尾的参考部分。一些常见的开关如下：

- `--force` (`-f`) — 从不提示用户；始终覆盖
- `--interactive` (`-i`) — 始终提示用户
- `-link` (`-1`) — 创建硬链接而不是复制
- `--parents` (`-p`) — 将源路径附加到目标目录
- `--recursive` (`-R`) — 复制任何子目录
- `--symbolic-link` (`-s`) — 创建符号链接而不是复制
- `--update` (`-u`) — 覆盖旧文件或复制缺失文件

```
$ cp notes.txt old_notes.txt # copying
$ mkdir backup
$ cp old_notes.txt backup
$ ls backup
old_notes.txt
```

与 `rm` 类似，某些 Linux 发行版默认启用 `--interactive`，在文件将被覆盖时发出警告。

```
$ cp --interactive project_notes.txt old_notes
cp: overwrite `old_notes/project_notes.txt'? n
$
```

`mv`（移动）命令用于移动和重命名文件。这相当于对文件进行复制并删除原始文件。移动实际上也可以通过将文件移动到同一目录中的新名称来重命名文件。

```
$ mv notes.txt project_notes.txt # renaming
```

`mv` 最常见的开关与 `cp` 类似：

- `--backup` (`-b`) — 在覆盖之前，通过向名称添加 `-` 来为任何现有文件创建备份
- `--force` (`-f`) — 从不提示用户；始终覆盖
- `--interactive` (`-i`) — 在覆盖前始终提示用户
- `--update` (`-u`) — 覆盖旧文件或复制缺失文件

没有 `--recursive` 开关。当 `move` 移动一个目录时，它会自动移动该目录及其所有内容。

`namei`（name inode）命令列出路径中的所有组件，包括任何符号链接。

```
$ namei files
f: files
1 files -> /home/kem/bash/scripts
d /
d home
d kem
d bash
d scripts
```

在这种情况下，名为 `files` 的文件是一个符号链接。链接路径中的每个文件都是目录，标记为 `d`。其他文件标识包括：`l` 表示符号链接，`s` 表示套接字，`b` 表示块设备，`c` 表示字符设备，`-` 表示普通文件，`?` 表示访问路径中文件时的错误。

完整的文件权限，例如通过 `ls -l` 看到的，可以使用 `-m`（`mode`）开关显示。

## 与人交互

有几个命令可以检查谁在计算机上以及他们正在做什么。

`finger` 命令显示谁在计算机上，并提供额外信息，包括他们的会话空闲时间长短以及他们的联系方式。

```
$ finger
Login    Name             TTY  Idle  When     Bldg.    Phone
dhu     Dick Hu         *tp6  4:25  Thu 14:12 4th Floor ext 2214
mchung  Michael Chung    *con  5:07  Fri 09:57 OS Support  ext 1101
bgill   Biringer Gill    *tp7   15   Fri 13:32
```

由于对 `finger` 的 `.plan` 文件存在安全方面的担忧，一些 Linux 版本不再包含 `finger`。阅读 `finger` 的手册页以获取更多详细信息。

还有其他几个具有类似功能的命令。`users` 命令显示登录名称列表。

```
$ users
bgill dhu mchung
```

`who` 命令显示谁在计算机上，他们正在使用哪个连接，以及他们登录的时间。

```
$ who
dhu     ttyp6      Mar 29 14:12
mchung  console     Apr  6 09:57
bgill   ttyp7       Apr  6 13:32
```

`w` 命令提供更多详细信息，包括系统统计数据以及用户当前正在运行什么。

```
$ w
 3:18pm  up  9 days, 20:33,  3 users,  load average: 0.64, 0.66, 0.64
User     tty       login@        idle   JCPU   PCPU   what
dhu      ttyp6     2:12pm  4:28   8:01   8:01   csh
mchung   console    9:57am   5:10             sh
bgill    ttyp7      1:32pm   1.19           bash
```

## Shell 别名

别名是命令的简短形式。内置的 `alias` 命令为当前 Bash 会话创建简单的缩写。

要创建别名，请使用 `alias` 命令为命令及其开关指定一个名称。

```
$ alias lf='ls -qPl'
$ lf
-rw-m----- 1 kurtch devgroup 10809 Apr  6 11:00 assets.txt
-rw-m----- 1 kurtch devgroup  4713 Mar  9 2000 mailing_list.txt
```

仅输入 `alias` 命令，或者使用 `-p` 开关，会列出当前的别名。

```
$ alias
alias lf='ls -qPl'
```

Bash 只解释一次别名，允许使用命令本身的名称来创建该命令的别名。

```
$ alias ls='ls -qP' # Bash isn't confused
```

通常，只检查命令的第一个单词是否为别名。作为一个特殊的例外，如果别名字符串中的最后一个字符是空格，Bash 会检查命令中的下一个单词是否也是别名。

没有给别名提供参数方法。如果需要参数，请改为定义更强大的 shell 函数。

内置的 `unalias` 命令用于删除别名。使用 `-a` 开关可删除所有别名。

大多数 Linux 发行版都为常用命令定义了别名。例如，`dir` 通常是 `ls` 的别名。一些发行版为诸如 `rm -i` 这样的命令定义了别名，以强制用户提示，而这是默认不需要的。对于某些用户（例如习惯于禁用这些功能的高级 Unix 程序员）来说，这可能是一个问题。使用 `unalias` 删除你不想要使用的任何别名。

将别名与 shell 函数混合可能会造成混淆，因为别名仅在读取脚本行时扩展。如果在 shell 函数中使用了别名，它们会在 shell 函数定义时扩展，而不是在执行时扩展。因此，在 shell 脚本中最好完全避免使用别名。但是，可以使用 `shopt -s expand_aliases` 命令在脚本中开启它们。

## Bash 哈希表

当执行未指定路径的命令时，shell 会在（`PATH` 变量中列出的目录中）搜索该命令。当 Bash 找到命令时，它会记住命令的位置，并将位置存储在*哈希表*中。此后，Bash 会检查表中命令的位置，而不是再次搜索命令，从而使命令运行得更快。但是，如果命令在 Bash 记录其位置后移动了，shell 将无法找到该命令。

内置的 `hash` 命令维护哈希表。如果不带任何开关，`hash` 会列出已记住的命令、它们的位置以及该命令在本次会话期间被执行的次数。

```
$ hash
hits      command
  1       /bin/ls
  1       /bin/uname
  1       /usr/bin/tput
  1       /bin/stty
  1       /usr/bin/uptime
  1       /usr/bin/man
```

当指定一个命令时，Bash 会搜索该命令的新位置。例如，如果你在当前的目录中创建了自己的 `ls` 命令，并且 `PATH` 变量赋予当前目录中的文件优先权，那么 `hash ls` 命令会先找到你的 `ls` 命令，用 `./ls` 替换 `/bin/ls`。

```
$ hash ls
$ hash
hits      command
  1       /bin/touch
  0       ./ls
  1       /bin/cmdop
```

`-p`（`path`）开关显式为命令设置路径。`-d`（`delete`）开关删除特定条目，`-r`（`remove`）清空哈希表，删除所有命令。`-t`（`table`）选项列出特定命令的路径名，`-l`（`list`）以允许它们被 `hash` 命令重新使用的格式列出命令。

```
$ hash -t ls less
ls        /bin/ls
less      /usr/bin/less
```

## 自定义你的提示符

默认的 Bash 交互式提示符是美元符号（$），尽管一些发行版使用不同的符号。大多数 Linux 发行版重新定义提示符以包含额外信息，例如您当前的登录和计算机，这在您在不同账户和计算机之间切换时非常有用。

如果定义了名为 `PS1`（`prompt string 1`）的变量，Bash 将使用此变量的值作为您的主要提示符。如果在字符串中包含变量名，Bash 会将变量的值替换到您的提示符中。

```
$ declare -x PS1="Bash $ "
Bash $ pwd
/home/ke/kbrutch/archive
Bash $
```




以下内容声明了一个三行提示符，包含一个空行、当前目录、旧当前目录、登录名、计算机名，以及加粗的 $。

```bash
$ declare -x PS1="\
\SPWD (\OLDPWD)\
\\SLOGNAME@\uname -n\[\tput bold\'] \$ [\tput rms0'\']"\
\n/home/kburtch/archive ( /home/kburtch/work)\
kburtch@linux_box $
```

`\` 和 `\]` 应该包裹由 `tput` 返回的显示格式字符。否则，Bash 会假设提示符中的所有字符都是可打印的，从而无法正确换行较长的输入行。

Bash 有一个 `PS2`（*提示符字符串 2*）变量，它是用于不完整命令行（例如使用多行引号时）的提示符。默认情况下，此提示符是大于号（`>`）。

Bash 识别提示符中的以下转义序列。

-   `\a`— 蜂鸣声（ASCII 铃字符）
-   `\A`— 24 小时制时间，格式为 HH:MM
-   `\d`— 日期，格式为 "星期-月份-日期"
-   `\D{s}`— 使用格式字符串 s 运行 C `strftime` 函数
-   `\e`— ASCII 转义字符
-   `\h`— 主机名
-   `\H`— 完整主机名，包括域名
-   `\j`— 任务表中的任务数量
-   `\J`— tty 设备
-   `\n`— 换行
-   `\r`— 回车
-   `\s`— Shell 的名称
-   `\t`— 24 小时制时间
-   `\T`— 12 小时制时间
-   `\@`— AM/PM 格式的时间
-   `\u`— 用户名
-   `\v`— Bash 版本
-   `\V`— Bash 发行版
-   `\w`— 当前工作目录
-   `\W`— 当前工作目录的基名
-   `!`— 命令在历史记录列表中的位置
-   `\#`— 会话的顺序命令编号
-   `\$`— 默认提示符（超级用户为 #，其他用户为 $）
-   `\nnn`— 八进制格式的 ASCII 字符
-   `\\`— 反斜杠
-   `\f`— 开始一系列不可打印字符的序列
-   `\.`— 结束一系列不可打印字符的序列

变量在第 5 章中有更详细的讨论。你可以通过关闭 `promptvars` shell 选项来禁用变量替换。

## 长命令行

Bash 会自动滚动长命令行：当光标到达窗口右侧时，Bash 会在下一行继续该命令。

如果你想将命令拆分以便其适应多行显示，请使用反斜杠 (\) 作为行尾的最后一个字符。Bash 会打印续行提示符（通常是 `>`），以表示这是前一行命令的延续。

```bash
$ printf "%s\n" "This is a very long printf. How long is it?"
> It's so long that I continued it on the next line.
This is a very long printf. How long is it? It's so long that I continued it on the next line.
```

## 自定义命令行编辑

`bind` 命令允许你更改编辑键、编辑选项，以及创建键盘宏。更改仅影响当前的编辑模式。

`-p` 或 `-P` 开关显示各种命令行编辑功能——激活这些功能的按键组合。`-P` 开关以易读的格式显示信息。

```bash
$ shopt -o emacs
emacs	on
$ bind -P | head -5
abort can be found on "\C-g", "\C-x\C-g", "\e\C-g".
accept-line can be found on "\C-j", "\C-m".
alias-expand-line is not bound to any keys
arrow-key-prefix is not bound to any keys

$ shopt -a -o vi
$ bind -P | head -5
abort is not bound to any keys
accept-line can be found on "\C-j", "\C-m".
alias-expand-line is not bound to any keys
arrow-key-prefix is not bound to any keys
```

可以使用 `-m`（键映射）开关来选择特定的编辑模式。

```bash
$ bind -P -m vi | head -5
abort can be found on "\C-g" .
accept-line can be found on "\C-j", "\C-m" .
alias-expand-line is not bound to any keys
arrow-key-prefix is not bound to any keys
```

特殊按键由反斜杠代码表示。这些代码基于 `emacs` 文本编辑器使用的代码。

-   `\\`— 反斜杠
-   `\ "`— 双引号
-   `\ '`— 单引号
-   `\a`— 警报（铃）
-   `\b`— 退格键
-   `\c`— Control 键
-   `\d`— Delete
-   `\e`— Escape 键
-   `\f`— 换页符
-   `\M`— emacs meta 键
-   `\n`— 换行（进喂）
-   `\r`— 回车
-   `\t`— 水平制表符
-   `\v`— 垂直制表符
-   `\nnn`— 八进制格式的 ASCII 代码
-   `\xnnn`— 十六进制格式的 ASCII 代码

例如，control-g 由序列 `\C-g` 表示。

`-l`（列表）开关列出所有可能的键盘功能。

```bash
$ bind -l | head -5
abort
accept-line
alias-expand-line
arrow-key-prefix
backward-char
```

要查看特定功能，请使用 `-q`（查询）开关。

```bash
$ shopt -s -o emacs
$ bind -q abort
abort can be invoked via "\C-g", "\C-x\C-g", "\e\C-g".
```

可以使用 `-u`（取消绑定）删除绑定。如果存在多个绑定，则删除第一个。

```bash
$ bind -u abort
$ bind -q abort
abort can be invoked via "\C-x\C-g", "\e\C-g"
```

或者，`-r`（移除）根据按键序列删除绑定。

```bash
$ bind -r "\e\C-g"
$ bind -q abort
abort can be invoked via "\C-x\C-g".
```

可以使用按键序列、冒号和编辑功能的名称添加新绑定。例如，`backward-kill-line` 功能从行首到光标位置擦除所有内容。在 vi 模式下，`backward-kill-line` 通常未绑定到任何按键，因此无法使用。

```bash
$ shopt -s -o vi
$ bind -q backward-kill-line
backward-kill-line is not bound to any keys.
```

然而，`bind` 可以将 `backward-kill-line` 分配给新的按键组合。

```bash
$ bind "\C-w:backward-kill-line"
$ bind -q backward-kill-line
backward-kill-line can be invoked via "\C-w".
```

现在 control-w 将擦除到行首。

除了激活特定编辑功能的按键外，还有许多选项（或变量）。`-v` 或 `-V` 开关显示键盘选项。`-V` 更易于阅读。

```bash
$ bind -v | head -5
set blink-matching-paren on
set completion-ignore-case off
set convert-meta on
set disable-completion off
set enable-keypad off

$ bind -V | head -5
blink-matching-paren is set to 'on'
completion-ignore-case is set to 'off'
convert-meta is set to 'on'
disable-completion is set to 'off'
enable-keypad is set to 'off'
```

这些选项可以开启和关闭。

```bash
$ bind "set enable-keypad on"
$ bind -V | head -5
blink-matching-paren is set to 'on'
completion-ignore-case is set to 'off'
convert-meta is set to 'on'
disable-completion is set to 'off'
enable-keypad is set to 'on'
```

所有功能和选项的完整列表可在 `Readline` 手册页中找到。

`bind` 命令还可以定义 *键盘宏*。这些是短按键序列，会自动扩展为较长且通用的序列，以减少输入量。`-s` 或 `-S` 开关列出当前定义的所有宏。`-v` 开关更具“可读性”。

创建宏的格式与分配功能所用的格式相同，但扩展文本周围必须出现 `\'`*。

```bash
$ bind -S
$ bind '\C-w\*' >/dev/null
$ bind -S
\C-w outputs >/dev/null
```

现在 control-w 会在当前行中插入 `>/dev/null`。

## 你的会话配置文件

当你登录计算机并启动新的 Bash 会话时，你可能需要输入几个命令来定制你的会话。也许你想将编辑模式从 emacs 更改为 vi，创建新的按键绑定，或更改你的命令行提示符。而不是输入这些命令，如果它们保存在一个特殊文件中，Bash 会在你每次登录时为你运行这些命令。这个文件被称为*配置文件*，因为它包含定制会话以符合你特定需求的命令。

原始的 Bourne shell 在用户登录时运行两个配置文件。首先，名为 `/etc/profile` 的文件是执行给所有用户的通用配置文件。其次，如果在用户的 home 目录中出现名为 `.profile` 的文件，则此文件包含每个用户的额外命令。当 Bash 作为 `sh` 而不是 `bash` 启动时，它会模拟这种行为。

Bash 扩展了这一原则，根据情况运行多个配置文件。此外，Linux 发行版通常会定制通用配置文件以运行存储在其他脚本中的额外命令。

Bash 区分登录会话和其他实例。当用户或程序首次登录，或使用 Bash 的 `--login`（或 `-l`）开关模拟登录时，Bash 作为*登录 shell* 运行。登录 shell 不一定向用户提供提示符。它仅表示 Bash 是当前会话的顶层程序，当 Bash 完成其运行后，登录会话将结束。

当你处于登录 shell 中时，`login_shell` shell 选项被打开。此选项可用于验证你是否处于登录 shell 中。

```bash
$ shopt login_shell
login_shell   on
```

当启动时未提供脚本或使用 `-i` 开关时，Bash 作为*交互* shell 运行。交互 shell 向用户提供命令提示符。一




交互式 shell 不一定是登录 shell。用户可以通过在 Bash 提示符下输入 `bash` 来启动一个非登录的交互式 shell，从而启动一个全新的 Bash 副本。

Bash 会话是交互式还是登录 shell，决定了使用哪些配置文件。通过这种方式，Bash 将专门用于自定义交互式会话的命令与更通用的命令区分开来。

`/etc/profile` 文件包含所有用户共有的设置命令和环境变更。通用的配置文件可能如下所示：

```bash
#!/etc/profile
# 默认不创建核心转储文件
ulimit -S -C 0 > /dev/null 2>&1
# HOSTNAME 是执行 hostname 命令的结果
declare -x HOSTNAME="`/bin/hostname`"
# Bash 命令历史记录最多不超过 1000 行
declare -x HISTSIZE=1000
# 如果安装了 PostgreSQL，则将 Postgres 命令
# 添加到用户的 PATH 中
if test -r /usr/bin/psql/bin ; then
    declare -x PATH="${PATH}*:*/usr/bin/psql/bin"
fi
# 通用配置文件结束
```

只有超级用户可以编辑此文件。当 Bash 作为登录 shell 使用时，它会执行找到的第一个名为 `~/.bash_profile`、`~/.bash_login` 或 `~/.profile` 的文件。当会话结束时，如果存在 `~/.bash_logout`，Bash 会执行它。

例如，SuSE Linux 使用 `~/.profile` 作为用户的配置文件。（你可以通过列出主目录中的文件来检查这一点。）通过编辑此文件，你可以添加那些在登录时总是执行命令。

```bash
# 我的配置文件
short -S -O emacs     # 我更喜欢 emacs 模式而不是 vi 模式
date                  # 登录时显示日期
```

通过模拟登录使用 `--login` 开关来测试更改。

```bash
$ bash --login
Wed Feb 6 15:20:35 EST 2002
$ short -O emacs
emacs                 on
$ logout
```

在不登录的情况下运行新的 Bash 交互式会话不会执行配置文件。

```bash
$ bash
$ logout
bash: logout: not login shell: use 'exit'
$ exit
```

脚本通常不会执行登录配置文件。如果 `BASH_ENV` 环境变量包含要执行的文件的路径名，Bash 会为脚本加载配置文件。然而，你应该避免使用 `BASH_ENV`。设置一组脚本的通用环境通常是通过 `source` 命令完成的，这在第 14 章“函数和脚本执行”中有详细讨论。`BASH_ENV` 对交互式会话没有影响。

你可以使用 `--noprofile` 开关来停止执行登录配置文件。

对于既是交互式会话又不是登录会话的情况，Bash 会运行另一组文件。Bash 查找一个名为 `~/.bashrc`（Bash 资源）的自定义脚本，并执行它而不是登录配置文件。别名函数只允许在资源文件中定义。可以使用 `--init-file` 或 `--rcfile` 开关指定不同的资源文件。典型的资源文件可能包含以下内容：

```bash
# /etc/bashrc
# 防止其他人写入用户的文件
umask 002
# 为 ls 创建别名以提供默认开关
alias ls='ls -qF'
```

一些发行版会在你的登录配置文件中添加行，以便同时执行 `~/.bashrc` 中的命令。这不是 Bash 的特性，而是由你的 Linux 发行版所做的修改。你可以在 `~/.bashrc` 文件中添加以下行来测试其行为：

```bash
# 我的 bashrc 资源文件自定义
printf "\n" ".bashrc has run"
```

通过在命令提示符下启动新会话来测试它。在这种情况下，SuSE Linux 始终运行资源文件。

```bash
$ bash --login
.bashrc has run
$ logout
$ bash
.bashrc has run
$ exit
```

因此，在不检查你的发行版的情况下，你无法确定资源文件的行为。

可以使用 `--norc` 开关来抑制资源文件。你的发行版在登录期间还可以运行其他文件：

- Red Hat 和 Mandrake Linux 将你的自定义分开，将函数和别名放在 `~/.bashrc` 中，将其他自定义放在 `~/.bash_profile` 中。他们的 `.bash_profile` 脚本也会自动运行一个 `.bashrc` 文件（如果存在的话）。
- SuSE Linux 将你的自定义分开，将函数和别名放在 `~/.bashrc` 中，将其他自定义放在 `~/.profile` 中。他们的 `.profile` 脚本也会自动运行一个 `.bashrc` 文件（如果存在的话）。
- SCO Linux（也称为 Caldera Linux）使用 `~/.profile`，它调用 `~/.bashrc`。然后它运行来自 `/etc/config.d/shells` 的配置脚本来设置系统默认值。当 `~/.bashrc` 运行时，它会调用 `/etc/config.d/shells/bashrc` 来设置非交互式默认值。用户的个人自定义应分别存储在 `~/.profile.private` 和 `~/.bashrc.private` 中。

同样，通用配置文件也可以进行自定义：

- Red Hat 和 Mandrake 将自定义分散到 `/etc/bashrc` 和 `/etc/profile` 中，以模拟用户配置文件的行为。进一步自动执行的系统脚本是专门针对安装在 `/etc/profile.d` 中的软件包。
- SuSE Linux 自动设置 `/etc` 目录中许多文件的内容，包括 `/etc/profile`。因此，个人更改必须存储在名为 `/etc/profile.local` 的单独文件中，否则在系统重新配置或升级时可能会丢失。其他自动执行的系统脚本是 `/etc/SuSEconfig` 以及存储在 `/etc/profile.d` 中的已安装软件包的脚本。SuSE 还包括一个 `/etc/profile.dos` 脚本，用于定义来自 MS-DOS 的用户的自定义。这可以通过 SuSE 配置软件启用，但也可以从你的 `/etc/profile.local` 文件中执行。
- SCO Linux 仅在 `/etc/profile` 中放置适用于任何基于 Bourne 的 shell 的最小设置信息。通用的 Bash 设置应配置在 `/etc/config.d/shells/profile` 和 `/etc/config.d/shells/bashrc` 中。

## 参考部分

### ls 命令开关

- `--all`（或 `-a`）——显示所有文件，包括 `.` 和 `..`
- `--almost-all`（或 `-A`）——显示除 `.` 和 `..` 之外的所有文件
- `--block-size=n`——以 n 字节块显示文件大小
- `--classify`（或 `-F`）——在文件名后添加符号以指示其类型
- `--color=t`——对文件名使用颜色，t 等于 never、always 或 auto。
- `--dereference`（或 `-L`）——显示符号链接引用的项目
- `--directory`（或 `-d`）——显示目录本身的信息而不是显示其内容
- `--dired`（或 -D）——用于 emacs `dired` 模式的输出
- `--escape`（或 `-b`）——为不可打印字符打印八进制转义序列
- `--file-type`（或 -p）——与 `--classify` 相同
- `--format=across`（或 -x）——按行而不是按列排序
- `--format=commas`（或 -m）——将文件名显示为以逗号分隔的列表
- `--format=long`（或 -1）——显示详细（长）列表
- `--format=single-column`（或 `-1`）——每行显示一个文件
- `--format=verbose`——与长格式相同
- `--format=vertical`（或 `-c`）——按列列出条目
- `--full-time`——显示完整的日期和时间
- `--hide-control-chars`（或 `-q`）——在文件名中为不可打印字符显示 ?
- `--human-readable`（或 `-h`）——以千字节、兆字节等显示大小，而不是原始字节
- `--ignore=p`（或 `-I`）——忽略匹配模式 `p` 的文件
- `--ignore-backups`（或 `-B`）——不列出以 `~` 结尾的文件
- `--indicator-style=classify`——与 `--classify` 相同
- `--indicator-style=none`——不分类文件
- `--indicator-style=file-type`——与 `--file-type` 相同
- `--inode`（或 `-i`）——打印文件的 inode 号
- `--kilobytes`（或 `-k`）——与块大小 1024 相同
- `-f`——不排序，启用 `-a`，禁用 `-1`
- `--literal`（或 `-8`）——按原样显示名称中的不可打印字符（与 `-q` 不同）
- `--no-group`（或 `-g`）——隐藏拥有该文件的组
- `--numeric-uid-gid`（或 `-n`）——以数字而不是名称显示 UID 和 GID
- `-o`——显示不带文件组所有权信息的长列表
- `--quote-name`（或 `-Q`）——将文件名用双引号括起来
- `--quoting-style=literal`——与 `--literal` 相同
- `--quoting-style=locale`——对单个文件名使用区域设置的引用样式
- `--quoting-style=shell`——在必要时对单个文件名使用 shell 引用
- `--quoting-style=shell-always`——总是对单个文件名使用 shell 引用
- `--quoting-style=c`——对单个文件名使用 C 字符串引用
- `--quoting-style=escape`——用反斜杠转义特殊字符
- `--reverse`（或 `-r`）——反转排序顺序
- `--recursive`（或 `-R`）——列出所有子目录的内容
- `-si`（或 `-h`）——类似于 `--human-readable`，但使用 1000 的幂而不是 1024
- `--size`（或 `-s`）——以块为单位打印大小
- `--sort=size`（或 `-S`）——按文件大小排序




## ls 命令选项（续）
- `--sort=extension`（或 `-X`）—按文件名后缀排序
- `--sort=none`（或 `-u`）—按文件在目录中物理存储的顺序排序
- `--sort=time`（或 `-t`）—按时间排序。默认为 `--time=ctime`
- `--sort=version`（或 `-v`）—按字母顺序排序，同时考虑 GNU 版本号惯例
- `--time=atime`（或 `-u`）—按访问时间排序
- `--time=access`—与 atime 相同
- `--time=use`—与 ctime 相同
- `--time=ctime`（或 `-c`）—显示更改时间；如果使用 `-t`，则按更改时间排序
- `--time=status`—与 ctime 相同
- `--tabsize=n`（或 `-T`）—假设制表符停止位每隔 n 个字符，而不是默认的八个字符
- `--width=n`（或 `-w`）—假设屏幕宽度为 n 个字符，而不是实际宽度

## printf 格式代码
- `%b`—展开反斜杠序列
- `%c`—显示单个字符
- `%d`—显示有符号数字
- `%e`—显示浮点数，采用指数（也称为科学）计数法
- `%f`—显示浮点数
- `%g`—根据数值使用 `%f` 或 `%e`
- `%i`—与 `%d` 相同
- `%o`—显示八进制数
- `%q`—引用字符串，以便 shell 脚本能够正确读取
- `%s`—显示未加引号的字符串
- `%u`—显示无符号数字
- `%x`—显示无符号十六进制数，使用小写字母
- `%X`—显示无符号十六进制数，使用大写字母
- `%$`—显示百分号

## printf 反斜杠代码
- `\b`—退格
- `\f`—换页（即在打印机上弹出页面）
- `\n`—换行
- `\r`—回车
- `\t`—制表符
- `\v`—垂直制表符
- `\'`—单引号字符（为了与 C 语言兼容）
- `\\`—反斜杠
- `\0n`—$n$ 是一个八进制数，代表一个 8 位 ASCII 字符

## rm 命令选项
- `--directory`（或 `-d`）—删除目录
- `--force`（或 `-f`）—从不提示用户，并忽略缺失的文件
- `--interactive`（或 `-i`）—始终提示用户
- `--recursive`（或 `-r` 或 `-R`）—删除所有子目录的内容

## cp 命令选项
- `--archive`（或 `-a`）—与 `-dpR` 相同
- `--backup`（或 `-b`）—在覆盖前为现有文件创建备份，通过在名称后添加 `~`
- `--backup=none/off`—从不创建带编号的备份
- `--backup=numbered/t`—始终创建带编号的备份
- `--backup=existing/mul`—如果已存在则创建带编号的备份；否则创建波浪号备份
- `--backup=simple/never`—始终创建波浪号备份
- `--no-dereference`（或 `-d`）—保留链接
- `--force`（或 `-f`）—从不提示用户；始终覆盖
- `--interactive`（或 `-i`）—始终提示用户
- `--link`（或 `-l`）—创建硬链接而不是复制
- `--preserve`（或 `-p`）—尽可能保留文件属性和所有权
- `--parents`（或 `-P`）—将源路径追加到目标目录
- `--recursive`（或 `-R`）—复制任何子目录
- `-r`—类似于 `--recursive`，但不包含对管道和其他无法正确复制的文件的特殊处理
- `--sparse=wr`—截断稀疏文件（`w`=从不），完整创建它们（`w`=始终），或由命令酌情截断（`w`=自动，默认）。
- `--strip-trailing-slashes`—移除要复制文件的路径名称中的尾部斜杠
- `--symlink`（或 `-s`）—创建符号链接而不是复制
- `--suffix=s`（或 `-S s`）—将路径名称后缀替换为新后缀 *s*
- `--target-directory=d`—将文件复制到目录 *d*
- `--update`（或 `-u`）—覆盖旧文件或复制缺失的文件
- `--one-file-system`（或 `-x`）—保持在当前文件系统中

## mv 命令选项
- `--backup`（或 `-b`）—在覆盖前为现有文件创建备份，通过在名称后添加 `-`
- `--backup`=none/off—从不创建带编号的备份
- `--backup`=numbered/t—始终创建带编号的备份
- `--backup`=existing/nu1—如果已存在则创建带编号的备份；否则创建波浪号备份
- `--backup`=simple/never—始终创建波浪号备份
- `--force`（或 `-f`）—从不提示用户；始终覆盖
- `--interactive`（或 `-i`）—始终提示用户
- `--strip-trailing-slashes`—移除要复制文件的路径名称中的尾部斜杠
- `--suffix=s`（或 `-S`）—将路径名称后缀替换为新后缀 *s*
- `--target-directory=d`—将文件复制到目录 *d*
- `--update`（或 `-u`）—覆盖旧文件或复制缺失的文件

# 4. 脚本基础

当我高中购买了一台崭新的 TRS-80 Model I 计算机时，我第一次接触到了计算机。这台计算机安装在图书馆里，供任何人使用。我记得我跟着那本翻旧了的手册，输入了我的第一个 BASIC 程序。

```
10 PRINT "KEN WAS HERE";
20 GOTO 10
```

当我运行该程序时，我吃了一惊。不仅计算机忠实地一遍又一遍地执行我的指令，而且屏幕上向上滚动的文字形成了一种变化的图案。当屏幕变满时，它滚动以腾出空间容纳更多消息。如果我将消息长度更改为能整除 64（TRS-80 有 64 个字符行）的数字，消息就会在屏幕上排成整齐的专栏向上行进。我的名字中存在着意想不到的魔力。

编程的乐趣在于通过“给空灵无形之物以栖息之所和名字”来创造新事物的乐趣。即使 bug，以其古老的方式，也是创造力漫长道路上意想不到的路标，它们提供了根据你决定如何处理它们而做出的选择。一个选择通向另一个选择，任何大小的两个程序都不相同。它们确实是创造性过程的产物，与任何绘画、歌曲或诗歌一样。

在 Bash 中，旅程始于程序员编写的第一段脚本。本章介绍 shell 脚本编写的基本技术——创建有序的脚本、重定向标准文件描述符以及处理不同类型的命令。

## 创建脚本

按照惯例，Bash shell 脚本的名称以 .sh 结尾。列表 4.1 显示了一个名为 hello.sh 的脚本，这是一个非常短的脚本，它在屏幕上写入一条消息。

**列表 4.1 hello.sh**

```
# hello.sh
# 这是我的第一个 shell 脚本

printf "Hello! Bash is wonderful."
exit 0
```

以井号（#）开头的行是注释。它们是给读者的笔记，不影响脚本的执行。井号到行尾之间的所有内容实际上都被 Bash 忽略。

注释应始终具有信息量，描述脚本试图实现的目标，而不是逐行复述每个命令在做什么。我见过太多脚本，顶部只有一个注释写着“所有进入此地者，希望尽抛”。在商业环境中，清晰且有信息量的注释有助于排查和调试晦涩的问题。

exit 命令后跟一个零，通知运行你的 shell 脚本的程序该脚本运行成功。

你可以通过启动一个新的 shell 来运行你的脚本：

```
$ bash hello.sh
```

如果没有错误，Bash 会响应这条消息：

```
Hello! Bash is wonderful.!
```

## 创建行为良好的脚本

假设你的工作是编写一个 shell 脚本来运行 sync 命令，当系统上没有用户时。以下命令足以完成这项工作。

```
USERS=`who | wc -l`
if [ $USERS -eq 0 ] ; then
sync
fi
```

这在 Bash 提示符下工作得相当好。但请考虑以下问题：

- Linux 如何知道这是一个 Bash 脚本？
- 如果计算机上有一个以上的 who 命令，哪一个被执行？
- 如果成功或失败，脚本如何通知运行它的程序？
- 如果 sync 命令被意外删除或系统管理员更改了权限，会发生什么？

Bash 是一种非常有灵活性的语言：如果它要用于交互式使用，它是需要这种灵活性的。但在脚本编写中，这种灵活性可能导致安全漏洞和意外行为。为了让 shell 脚本“行为良好”，它必须做的不仅仅是在 Bash 美元提示符下输入相同的命令。





结构良好的 Bash 脚本可以分为五个部分：

-   头部
-   全局声明
-   健全性检查
-   主脚本
-   清理工作

这些部分在脚本设计中都起着重要作用。接下来，您可以回顾之前的示例，通过检查每个部分来了解如何改进它。

## 头部

头部定义了脚本的类型、编写者、版本，以及 Bash 使用的假设或 shell 选项。

脚本的第一行是*头部行*。该行位于脚本顶部，左对齐，以 `#!` 开头。这种字符组合用于标识脚本的类型。Linux 使用此信息来启动正确的程序以运行脚本。对于 Bash 脚本，这一行指示 Bash 解释器所在位置的绝对路径名。在大多数 Linux 发行版中，第一行头部如下所示：

```bash
#!/bin/bash
```

如果您不知道 Bash shell 的位置，可以使用 Linux 的 `whereis` 命令来查找：

```bash
$ whereis bash
bash: /bin/bash
```

典型脚本的开头如下所示：

```bash
#!/bin/bash
#
# 如果计算机上没有人，则刷新磁盘
#
# Ken O. Burch
# CVS: $Header$

shopt -s -o nounset
```

Bash 头部行之后是描述脚本用途和编写者的注释。*CVS* 行在第 8 章“调试和版本控制”中解释。`shopt -s -o nounset` 命令通过报告未定义的变量来检测某些拼写错误。

## 全局声明

适用于整个脚本的所有声明都应位于脚本的顶部，即在头部下方。通过将*全局声明*集中在一处，可以方便阅读脚本的人查阅它们。

```bash
## 全局声明
declare -rx SCRIPT=${0##*/}         # SCRIPT 是此脚本的名称
declare -rx who="/usr/bin/who"       # who 命令 - man 1 who
declare -rx sync="/bin/sync"         # sync 命令 - man 1 sync
declare -rx wc="/usr/bin/wc"         # wc 命令 - man 1 wc
```

## 健全性检查

下一部分，*健全性检查*，保护脚本免受计算机意外变更的影响。通常，当命令在命令行提示符下运行时，Bash 会在几个目录中搜索要运行的命令。如果找不到该命令（也许是因为拼写错误），Bash 会报告错误。对于与 Bash 进行交互式操作来说，这种行为是有益的，因为它可以节省时间，并且任何错误都可以通过几个按键轻松纠正。

另一方面，脚本在没有人工监督的情况下运行。在脚本执行任何语句之前，需要验证所有必需的文件是否可访问。所有必需的命令都应该是可执行的，并存储在预期位置。这些检查有时被称为*健全性检查*，因为除非计算机处于已知或“正常”状态，否则它们不允许脚本开始其主要任务。对于像 Linux 这样高度可定制的操作系统来说，这一点尤为重要：在一台计算机上成立的情况在另一台计算机上可能不成立。

换一种说法，Bash 依赖运行时错误检查。大多数错误仅在错误语句执行时才被捕获。在脚本早期检查危险情况可防止脚本在任务中途失败，否则将难以确定脚本在哪里中断以及需要做什么才能继续。

有时，系统管理员会无意中删除或更改文件的访问权限，使其对脚本不可用。其他时候，环境中的变更可能会改变执行哪些命令。众所周知，恶意的计算机用户还会篡改个人的登录配置文件，导致你以为正在运行的命令实际上并不是你正在使用的命令。

对于示例脚本而言，您需要验证所需的命令是否在它们应该所在的位置，并且对脚本可用。

```bash
## 健全性检查
if test -z "$BASH" ; then
    printf "$SCRIPT:$LINENO: 请通过 BASH shell 运行此脚本\n" >&2
    exit 192
fi
if test ! -x "$who" ; then
    printf "$SCRIPT:$LINENO: 命令 $who 不可用 - 中止\n" >&2
    exit 192
fi
if test ! -x "$sync" ; then
    printf "$SCRIPT:$LINENO: 命令 $sync 不可用 - 中止\n" >&2
    exit 192
fi
if test ! -x "$wc" ; then
    printf "$SCRIPT:$LINENO: 命令 $wc 不可用 - 中止\n" >&2
    exit 192
fi
```

## 主脚本

一旦验证了系统是正常的，脚本就可以继续执行其工作了。

```bash
# 如果计算机上没有人，则刷新磁盘
USERS=`who | wc -l`
if [ $USERS -eq 0 ] ; then
    sync
fi
```

## 清理工作

最后，脚本需要清理其自身。任何临时文件都应被删除，并且脚本向运行该脚本的人员或程序返回状态代码。在这种情况下，没有需要清理的文件。更复杂的脚本可能会使用一个变量来跟踪由失败命令返回的状态代码。

通过将清理部分放在程序的末尾，有一个独特的地方来执行你的清理任务，而不是在脚本中重复这些任务。

```bash
exit 0 # 一切正常
```

完成的脚本如清单 4.2 所示。

## 清单 4.2 flush.sh

```bash
#!/bin/bash
# 如果计算机上没有人，则刷新磁盘
# Ken O. Burch
# CVS: $Header$

shopt -s -o nounset

## 全局声明

declare -rx SCRIPT=${0##*/}          # SCRIPT 是此脚本的名称

declare -rx who="/usr/bin/who"       # who 命令 - man 1 who
declare -rx sync="/bin/sync"         # sync 命令 - man 1 sync
declare -rx wc="/usr/bin/wc"         # wc 命令 - man 1 wc

## 健全性检查

if test -z "${BASH}" ; then
       printf "${SCRIPT}:${LINENO}: 请通过 BASH shell 运行此脚本\n" >&2
       exit 192
fi
if test ! -x "$who" ; then
       printf "${SCRIPT}:${LINENO}: 命令 $who 不可用 - 中止\n" >&2
       exit 192
fi
if test ! -x "$sync" ; then
       printf "${SCRIPT}:${LINENO}: 命令 $sync 不可用 - \
中止\n" >&2
       exit 192
fi
if test ! -x "$wc" ; then
       printf "${SCRIPT}:${LINENO}: 命令 $wc 不可用 - 中止\n" >&2
       exit 192
fi

# 如果计算机上没有人，则刷新磁盘

USERS=`$who | $wc -l`
if [ ${USERS} -eq 0 ] ; then
       $sync
fi

## 清理工作

exit 0 # 一切正常
```

这个脚本比引入本节时那个四行脚本长得多。通常，主脚本越长，行为良好的脚本中那些行所增加的开销就越少。这个新脚本比只包含主脚本的脚本更安全可靠。

## 停止脚本

`logout` 命令，它结束交互式登录会话，不能用于停止脚本。（毕竟，脚本不是登录会话。）相反，Bash 提供了两个内置命令来终止脚本。

如前所述，`exit` 命令无条件地停止脚本。`exit` 可以包含一个状态代码，将其返回给脚本的调用者。状态代码为 `0` 表示没有错误。如果省略状态代码，则返回脚本最后执行的命令的状态。因此，最好始终提供退出状态。

```bash
exit 0 # 一切正常
```

当脚本到达其末尾时，它会自动停止，就好像在那里输入了隐式的 `exit` 一样，但 `exit` 的状态是最后执行的命令的状态。

`suspend` 命令同样无条件地停止脚本。然而，与 `exit` 不同，执行被挂起，直到脚本收到信号以唤醒并继续执行 `suspend` 命令之后的下一条语句。

```bash
suspend # 等待收到其他通知
```

此命令在第 10 章“作业控制和信号”中详细讨论。

还有一个称为 `sleep` 的 Linux 实用程序。Sleep 使脚本暂停特定的秒数，之后唤醒并继续执行 `sleep` 命令之后的下一条语句。

```bash
sleep 5 # 等待 5 秒
```

Sleep 对于在脚本中放置暂停很有用，使用户可以阅读到目前为止显示的内容。然而，Sleep 不适合同步事件，因为特定程序在计算机上运行的时长通常取决于系统负载、用户数量、硬件升级以及其他脚本无法控制的因素。

## 读取键盘输入

内置的 `read` 命令停止脚本并等待用户从键盘输入内容。输入文本被分配给伴随 `read` 命令的变量。

```bash
print "归档文件多少天？ "
read ARCHIVE_DAYS
```




在此示例中，变量 `ARCHIVE_DAYS` 包含用户输入的天数。

`read` 有多种选项。首先，`-p` (*prompt*) 是一个简写功能，它结合了 `printf` 和 `read` 语句。`read` 在等待用户响应之前会显示一条简短的消息。

```
read -p "Archive files for how many days? " ARCHIVE_DAYS
```

`-x` (*raw input*) 选项禁用了特殊字符的反斜杠转义。通常，当用户输入 `\n` 等转义序列时，`read` 会理解它们。使用原始输入时，`read` 将退格键视为与其他键盘输入的字符相同。只有当你需要自己处理反斜杠字符时，才需要使用 `-r`。

```
read -px "Enter a Microsoft Windows pathname (backslashes allowed): " -r MS_PATH
```

`-e` 选项仅在交互式环境中有效，在 shell 脚本中无效。它允许你使用 Bash 的历史记录功能来选择要返回的行。例如，你可以使用向上和向下箭头键在最近输入的命令之间移动。

可以使用 `-t` (*timeout*) 开关设置超时。如果在超时时间结束前没有输入任何内容，shell 将继续执行下一条命令，且变量的值保持不变。如果用户在超时结束后才开始输入，输入的任何内容都会丢失。超时时间以秒为单位。

```
read -t 5 FILENAME # wait up to 5 seconds to read a filename
```

如果存在名为 `TMOUT` 的变量，即使未使用 `-t`，Bash 也会在变量指定的秒数后超时。

可以使用 `-n` (*number of characters*) 开关限制读取的字符数。如果达到最大字符数，shell 将不等待按下 Enter/Return 键，直接继续执行下一条命令。

```
read -n 10 FILENAME # read no more than 10 characters
```

如果你未提供变量，`read` 会将输入的文字放入名为 `REPLY` 的变量中。结构良好的脚本应避免这种默认行为，以便脚本读者清楚地知道 `REPLY` 的值来源。

`read` 还有一些特殊用途的选项，将在第 13 章“Console Scripting”中讨论。从键盘读取时，`read` 通常返回状态码 0。

## 基本重定向

你可以将 `printf` 等命令的消息重定向到文件或其他命令。Bash 将此称为 *redirection*。有许多重定向运算符。

`>` 运算符将命令的消息重定向到文件。重定向运算符后跟写入消息的文件名。例如，要将消息 "The processing is complete" 写入名为 results.txt 的文件，可以使用：

```
printf "The processing is complete" > results.txt
```

> 运算符始终覆盖指定文件。如果一系列 printf 消息重定向到同一文件，只有最后一条消息会出现。

要在不覆盖先前消息的情况下向文件添加消息，Bash 提供了追加运算符 >>。此运算符将消息重定向到文件末尾。

```
printf "The processing is complete" >> results.txt
printf "There were no errors" >> results.txt
```

results.txt 文件包含以下两行：

```
The processing is complete
There were no errors
```

同样，可以从文件将输入重定向到命令。输入重定向符号是 <。例如，wc（单词计数）实用程序收集文件的统计数据。要统计文件中的行数，可以使用：

```
wc -lines < purchase_orders.txt
```

wc -lines 将 purchase_orders.txt 的内容视为从键盘输入。

除了文件外，命令的结果还可以作为输入重定向到另一个命令。这个过程称为管道，使用竖线（或管道）运算符 |。

```
who | wc -lines   # count the number of users
```

任意数量的命令可以用竖线符号串联起来。这样的一组命令称为流水线。

如果管道命令系列中的一个命令过早结束，例如因为你使用 control-c 中断了命令，Bash 会在屏幕上显示消息“Broken Pipe”。

命令后的行也可以被命令读取和处理。运算符 << 将脚本中其后的行视为从键盘输入。该运算符需要后跟一个标记，表示行的结束。

`<<` 列表中的数据被称为 *here file*（或 *here document*），因为在 Bourne shell 脚本中通常使用单词 HERE 作为标记词。

较新版本的 Bash 还有另一个 here file 重定向运算符 `<<<`，它重定向单行文本。第 2 章 "Operating the Shell" 的章节中有一个示例。

## 标准输出、错误和输入

Linux 假设所有输出都流向某种文件。对 Linux 而言，屏幕是一个名为 `/dev/tty` 的文件。

```
printf "Sales are up" > /dev/tty # display on the screen
```

当程序中的消息没有被重定向时，消息不会直接去屏幕。相反，输出通过一个名为 *standard output* 的特殊文件。默认情况下，标准输出代表屏幕。通过标准输出发送的所有内容都重定向到屏幕。Bash 使用符号 `&1` 来指代标准输出，你可以显式地将消息重定向到它。

```
printf "Sales are up" > results.txt # sent to a file on disk
printf "Sales are up" > /dev/tty # send explicitly to the screen
printf "Sales are up" # sent to screen via standard output
printf "Sales are up" >&1 # same as the last one
printf "Sales are up" >/dev/stdout # same as the last one
```

`/dev/stdout` 是标准输出文件的另一个名称。最后三个示例是相同的。确保 `&1` 紧挨着重定向符号，中间没有空格。

标准输出不一定指屏幕。例如，考虑以下名为 `listorders.sh` 的脚本：

```
#!/bin/bash
#
# This script shows a long listing of the contents of the orders subdirectory.
shopt -s -o nounset

ls -l incoming/orders
exit 0
```

假设你运行此脚本并将内容重定向到文件。

```
$ bash listorders.sh > listing.txt
```

在脚本内部，标准输出不再指屏幕。相反，标准输出指你重定向输出的文件，在本例中为 `listing.txt`。

```
ls -l incoming/orders # listing saved in listing.txt
ls -l incoming/orders >&1 # listing saved in listing.txt
ls -l incoming/orders > /dev/tty # listing displayed on screen
```

使用标准输出是一种将脚本及其内部任何命令的所有输出发送到新目标的方法。

脚本通常不需要知道消息流向何处；始终存在它们被重定向的可能性。然而，当发生错误并向用户打印警告消息时，你不想让这些消息与其他所有内容一起被重定向。

Linux 定义了一个专门用于用户消息的第二种文件，称为标准错误。此文件代表所有错误消息的目标。标准错误的符号是 &2。也可以使用 /dev/stderr。与标准输出一样，默认目标是屏幕。例如，

```
printf "${SCRIPT}:${LINENO: No files available for processing" >&2
```

此命令看似与没有 >&2 重定向的 printf 工作相同，但有一个重要区别。无论标准输出之前被重定向到何处，它都会向屏幕显示错误消息。

因为标准错误与标准输出一样，是另一种目标的重命名，所以标准错误也可以被重定向。标准错误的重定向符号与标准输出相同，除了以数字 2 开头。

```
$ bash listorders.sh 2> listorders_errors.txt
```

在此示例中，listorders.sh 脚本的所有错误消息都保存在文件 listorders_errors.txt 中。

如果 ls 命令直接使用 /dev/tty 将错误消息写入屏幕，就没有办法将消息重定向到单独的文件。

Linux 将所有输入视为从文件读取。这个特殊文件称为标准输入，使用符号 &0。/dev/stdin 也可用于标准输入。当命令用 | 符号连接时，第二个命令的标准输入成为第一个命令的标准输出。

单个命令可以组合多个重定向。顺序很重要，每个重定向按从左到右处理。要将标准输出和标准错误重定向到单个文件，以下命令有效。

```
$ bash listorders.sh > listorders_errors.txt >&2
```

然而，反转重定向顺序不起作用，因为它将标准错误重定向到旧的标准输出，然后将标准输出重定向到文件 listorders_errors.txt。

由于同时重定向标准输入和标准错误非常常见，Bash 提供了简写形式 &>，它重定向两者。

```
$ bash listorders.sh &> listorders_errors.txt
```





## 内置命令与 Linux 命令

最初的 Bourne shell 的设计方式是，除了 shell 的核心组成部分外，其他所有内容都作为 shell 外部的某个程序来实现。例如，即使是算术运算，也必须由外部程序来执行。这种设计使 Bourne shell 非常灵活，但也带来了一些缺点。首先，因为它不断加载和重启程序来执行甚至最简单的任务，所以速度很慢。其次，由于没有保证某个操作系统上的命令在另一个操作系统上以相同方式实现，这使得 shell 脚本难以移植；此类命令甚至可能根本不可用。

为了解决这些问题，Bash 将许多基本命令内置了。但为了与较旧的 Bourne shell 保持基本兼容性，Linux 仍然实现了 Bash 命令的自己的版本。例如，**test** 是 Bash 中的内置命令，但 Linux 还为那些不提供 **test** 内置版本的 shell 提供了自己的程序 **/usr/bin/test**。

如果你不知道某个命令是否为内置命令，Bash 的 **type** 命令会告诉你。如果该命令是 Linux 命令，它会显示该命令的路径（就像 Linux 的 **whereis** 命令那样）。

```
$ type cd
cd is a shell builtin
$ type id
id is /usr/bin/id
```

**-t** (*type*) 开关显示命令的类型。**-p** (*path*) 开关仅返回该命令的哈希表值，而不是 **PATH** 变量中的首次出现位置，并抑制其他信息。**-a** (*all*) 标志列出命令的所有变体。

```
$ type -a pwd
pwd is a shell builtin
pwd is /bin/pwd
```

有两个开关限制了搜索范围。**-f** 开关不检查任何已声明的 Bash 函数。**-p** 开关更进一步，检查 Linux 命令的路径，并忽略任何 Bash 命令、函数或别名。

**builtin** 命令显式运行内置命令。即使存在具有相同名称的别名，该命令也会执行。

```
builtin pwd
```

同样，**command** 显式运行 Linux 命令，即使存在具有相同名称的内置命令或别名。

```
command pwd
```

使用 **-v** 或 **-V**，**command** 会列出有关命令的信息，例如其路径名。如果使用 **-p**，**command** 会在标准 Linux **bin** 库中搜索该命令；如果你修改了 **PATH** 变量，这将很有用。

完整的内置 shell 命令列表见附录 B。

尽管 *builtin* 和 *command* 在测试和将旧脚本移植到 Bash 时很有用，但结构良好的脚本不应依赖它们，因为它们表明脚本设计存在歧义。

内置的 *enable* 命令暂时隐藏 shell 内置命令，并在稍后重新启用它们。*-n* 开关禁用该命令。

```
$ enable test
$ type test
test is a shell builtin
$ enable -n test
$ type test
test is /usr/bin/test
```

*-d* 开关禁用内置命令并释放其占用的任何内存。可以使用 *-f* 开关重新加载，此时必须指定包含该内置命令的文件名。

使用 *-p* 时，会打印所有已启用的 shell 内置命令。你可以将 *-p* 与 *-n* 组合使用以列出已禁用的内置命令，或使用 *-a* 显示所有内置命令。*-s* 开关将列表限制为 POSIX 特殊内置命令。

```
$ enable -pn
enable -n test
```

在结构良好的脚本中，*enable* 应在全局声明部分使用。在整个脚本中使用 *enable* 会使你难以记住某个特定命令是否为内置命令。

## Set 和 Shopt 命令

Bash 包含许多可以启用或禁用的可选功能。这些选项涉及 Bash 如何与用户进行交互式响应、在 shell 脚本中的行为方式，以及 Bash 与其他 shell 和标准的兼容性。

Bash 选项可以通过命令启用或禁用，或者在 Bash 启动时作为命令开关使用。例如，要启动 Bash 会话并禁止使用未定义变量，请使用以下命令：

```
$ bash -o nounset
```

在脚本中或在 Bash 美元提示符下，可以使用以下命令来禁止使用未定义变量：

```
$ shopt -s -o nounset
```

历史上，*set* 命令用于开启和关闭选项。随着选项数量的增加，*set* 变得难以使用，因为选项由单字母代码表示。因此，Bash 提供了 *shopt* (*shell option*) 命令，允许按名称而不是按字母开启和关闭选项。某些选项只能通过字母设置。其他选项仅在 `shopt` 命令下可用。这使得查找和设置特定选项成为一项令人困惑的任务。

`shopt -s (on)` 开启特定的 shell 选项。`shopt -u (unset)` 关闭选项。如果没有 `-s` 或 `-u`，`shopt` 会切换当前设置。

```
$ shopt -u -o nounset
```

单独使用 `shopt` 或加上 `-p` 会打印选项列表并显示它们是否开启，不包括 `-o` 选项。要查看这些选项，你需要设置 `-o`。字母代码列表存储在 shell 变量 `$_` 中。

这些开关中的大多数在特殊情况下有用。例如，在 UUCP 网络中，感叹号 (`!`) 用于电子邮件地址，但 Bash 使用 `!` 进行历史记录处理。可以使用以下命令禁用历史记录处理：

```
$ shopt -u -o histexpand
```

禁用历史记录后，可以在交互式命令行中使用 UUCP 电子邮件地址。之后，可以重新开启历史记录处理。

## 参考部分

**`command` 命令开关**

-   `-p` — 在标准 Linux 二进制库中搜索该命令
-   `-v` — 描述该命令
-   `-V` — 详细描述该命令

**`enable` 命令开关**

-   `-a` — 显示所有内置命令及其是否启用
-   `-d` — 禁用并删除内置命令
-   `-f *file*` — 启用并加载内置命令
-   `-n` — 禁用内置命令
-   `-p` — 打印内置命令列表
-   `-s` — 将结果限制为特殊的 `POSIX` 内置命令

**`read` 命令开关**

-   `-a *array*` — 将文本读取到此数组中
-   `-d *d*` — 在字符 `d` 处停止读取，而不是在换行处
-   `-e` — 使用交互式编辑
-   `-n num` — 读取 num 个字符，而不是整行
-   `-p prompt` — 显示提示符
-   `-x` — 显示原始输入
-   `-s` — 隐藏输入的字符
-   `-t sec` — 在 sec 秒后超时

**`suspend` 命令开关**

-   `-i` — 即使这是登录 shell 也进行挂起

# 5 变量

命令的结果可以写入文件或保存在变量中。由于变量保存在内存中，它们通常比文件检查起来更快。Bash 对变量大小没有上限：它们足够大，可以容纳你需要保存的任何内容。

使用变量对于 shell 脚本编程至关重要。本章深入探讨变量及其在 shell 中的使用，从基本变量到使用 eval 命令扩展变量。

## 变量基础知识

变量使用 Bash 的 declare 命令声明。要声明一个名为 COST 的变量，请使用以下命令：

```
$ declare COST
```

为了与 Korn shell 兼容，使用内置的 typeset 语句。如果你正在使用 Bash，请改用 declare。declare 具有旧 typeset 命令的所有功能。

选择好的变量名很重要。有一次，我在批改一年级计算机科学的作业时，一个学生使用了 26 个名为 A 到 Z 的变量。关于这些变量代表什么没有任何解释，我花了半个小时才确定该程序是否真的能运行。（令人惊讶的是，它确实能运行。）

名称还应保持一致。例如，在共同基金行业中，“投资组合”、“账户”和“基金”经常意味着同一件事。最好在整个脚本中只使用这三个名称中的一个。如果使用了三个不同的术语，读者可能会假设它们在含义上有细微差别。

由于 Bash 对变量名称的检查非常有限，即使开启了 nounset 选项，另一个常见的错误是使用外观相似的变量。在我大学第一年，我遇到了一个老朋友，他很沮丧，因为他的 Fortran


程序没有正常工作。当我仔细检查时，我发现他声明了一个名为 **HI\*12\*** 的变量，但在程序主体中，他将该变量拼写为 **H1\***。当程序打印 HI\*12\* 的值时，结果为零，因为它实际上从未被赋值。类似的状况也可能发生在 Bash 脚本中。

变量名以一个字母或下划线字符开头，后跟其他字母数字字符或下划线。

尽管变量可以是大写或小写，但传统惯例规定变量使用大写命名，以免与 shell *命令*混淆，而 shell 命令几乎总是小写的。`TOTAL`、`ORDERS\_EUROPE` 和 `_W3C` 都是合法的变量名。没有*保留字*，即那些在 shell 中为特定目的保留的单词。

使用等号（=）为变量分配新值。若要为变量分配空字符串，则不提供任何值。

```
$ COST=
```

否则，请包含要分配的文本。

```
$ COST=0
```

虽然 `printf %d` 对于零值和空字符串都打印零，但 Bash 认为这两个值是不同的。没有值的变量与值为零的变量并不相同。

值也可以使用第 6 章中描述的 `let` 语句进行分配。Bash 区分变量的名称和该变量代表的值。若要引用变量的值，必须在名称前加上美元符号（$）。

```
$ printf "%s" $COST
0
```

美元符号意味着“替换”。shell 将 $COST 替换为 COST 所代表的值。在这种情况下，COST 的值为零。在替换 COST 的值后，命令变为：

```
$ printf "%d" 0
```

`unset` 命令是一种命令行便利功能。在结构良好的脚本中，变量在脚本开始时声明，并且不会被取消设置。这可以防止混淆，因为程序员可以确信这些变量在脚本运行期间始终存在。

命令的结果也可以分配给变量。如果命令包含在反引号（`）中，那么所有写入标准输出的内容将存储在正在分配的变量中，而不是其他地方。

```
$ declare NUMBER_OF_FILES
$ NUMBER_OF_FILES=`ls -1 | wc -1`
$ printf "%d\n" "$NUMBER_OF_FILES"
14
```

## 预定义变量

Bash 拥有超过 50 个预定义变量。这些变量在 Bash 首次启动时创建，提供关于 Bash 会话的信息，并可用于控制 shell 的某些功能。

其中一些变量具有特殊属性，如果您取消设置该变量然后创建一个同名的新变量，这些属性可能会丢失。例如，变量 `RANDOM` 包含一个随机数。如果您使用 `unset` 删除 `RANDOM` 并声明一个名为 `RANDOM` 的新变量，那么这个新变量是一个普通的 shell 变量，并不包含随机数。因此，最好避免创建与预定义变量同名的变量。

不带开关的 `declare` 命令会列出所有当前定义的值。

- `BASH`—Bash 的完整路径名。
- `BASH_ENV`—在 shell 脚本中，脚本启动前执行的配置文件名称。
- `BASH_VERSION`—Bash 的版本（例如，`2.04.0(1)-release`）。
- `COLUMNS`—显示屏上每行的字符数（例如，80）。
- `FUNCNAME`—如果在函数内部，则为该函数的名称。
- `HOSTNAME`—计算机的名称。在某些版本的 Linux 中，这可能是机器名称。在其他版本中，它可能是完全限定域名。
- `HOSTTYPE`—计算机类型。
- `HOME`—您的主目录名称。
- `IFS`—`内部字段分隔符`，用于将一行拆分为 shell 单词的字符列表。
- `LINENO`—脚本或函数中的当前行号。
- `LINES`—显示屏上的水平行数（例如，24）。
- `OSTYPE`—操作系统的名称。
- `PATH`—冒号分隔的搜索路径列表，用于查找要执行的命令。
- `PPID`—shell 父进程的进程 ID。
- `PROMPT_COMMAND`—在设置 PS1 主提示字符串之前要执行的命令。
- `PS1`—主提示字符串。
- `PS2`—次要提示字符串。
- `PS3`—select 命令提示字符串。
- `PS4`—trace 命令输出前缀字符串。
- `PWD`—当前工作目录（由 cd 命令设置）。
- `RANDOM`—每次引用时返回 0 到 32767 之间的一个随机数。
- `SHELL`—首选使用的 shell；用于那些为您启动 shell 的程序。
- `TERM`—终端仿真类型（例如，console）。

Linux 发行版定义了额外的变量。这些变量是否存在取决于您的特定发行版。许多变量是为应用程序的使用而声明的。

- `DISPLAY` 是 X Window 显示服务器。
- `EDITOR` 是您的默认编辑器。历史上，当没有可用的可视化编辑器时，这用于指示要使用的行编辑器（参见 VISUAL）。
- `ORGANIZATION` 是您的组织名称（通常是 /etc/organization 的内容）。
- `TERM` 是终端仿真（例如，xterm 会话中的 xterm，或 Linux 控制台中的 linux）。
- `VISUAL` 是您的默认编辑器，通常与 EDITOR 相同。
- `WINDOWMANAGER` 是当前 X Windows 窗口管理器的路径。

完整列表出现在本章末尾的参考部分。

## 引号的影响

熟悉其他计算机语言的人可能会对 Bash 使用引号的方式感到困惑。单引号和双引号不用于界定字符串或字符，而是用于控制 shell 如何分组字符以及解释字符串内的特殊字符。Bash 将此过程称为*单词拆分*。

```
$ COST=0
$ COST="0"
```

这两个赋值产生相同的结果：`cost` 被分配值 0。双引号明确指出分配给 `cost` 的值包含字符零。短的字母数字值可以在没有引号的情况下分配给变量。然而，当字符串包含空格时，要分配的值不再明显。请考虑以下示例。

```
$ DISTRIBUTION_CENTERS=London
$ printf "%s" $DISTRIBUTION_CENTERS
London
$ DISTRIBUTION_CENTERS=London ; Paris ; New York
bash: Paris: command not found
bash: New: command not found
$ printf "%s" $DISTRIBUTION_CENTERS
London
```

当 Bash 检查第二个赋值语句时，它看到值 London 以空格结束。它将该值分配给变量。然后它看到分号，即命令分隔符，并期望后面跟随一个新语句。它尝试执行 *Paris* 命令（不存在该命令）。它尝试对 *New* 命令做同样的事，并给它 *York* 参数。

因此，将所有赋值值用双引号括起来是一种安全的做法。即使您的公司只在伦敦有一个配送中心，字符串中也始终有机会添加新的配送中心，这会导致 shell 脚本崩溃。始终将值包含在引号中可确保 Bash 确切知道要分配什么值。

```
$ DISTRIBUTION_CENTERS="London ; Paris ; New York"
$ printf "%s" $DISTRIBUTION_CENTERS
London; Paris; New York
```

结果仍然不正确。Bash 获取了 `DISTRIBUTION_CENTERS` 的值并移除了空格，以便 `printf` 不会将其解释为 *London*、`;`、*Paris*、`;`、*New* 和 *York* 的独立参数。`printf` 的参数也必须用双引号括起来，以保持变量的值作为保留间距的单一参数。

```
$ printf "%s" "$DISTRIBUTION_CENTERS"
London ; Paris ; New York
```

再次，始终将变量替换内容用引号括起来是一种安全的做法。因为引号不是定界符，而是关于如何解释特殊字符的提示，所以可以连续使用它们。这是将字符串中的变量与周围文本分隔开的一种便捷方式。

```
$ TAX=7.25
$ TAX_MESSAGE="The tax is "$TAX"%"
$ printf "%s" "$TAX_MESSAGE"
The tax is 7.25%
```





将每段引用的片段用空格分隔会导致之前看到的同样问题：Bash 会将它们视为三个独立的值。

或者，可以用花括号包围变量替换中的变量名，以明确变量的起始和结束位置。

```
$ TAX_MESSAGE="The tax is ${TAX}%"
```

除了空格解释外，引号的另一个效果是不进行模式匹配。通常，例如，星号 (*) 代表当前目录中的所有文件。引号可以防止星号被替换为文件列表。

```
$ printf "%s\n" *
orders.txt
archive
calc.sh
$ printf "%s\n" "*"
*
```

要打印字符串而不解释其中的特殊字符，请使用单引号。双引号不能阻止 Bash 解释特殊字符 $、‘ 和 \，但单引号会保持所有字符不变。

```
$ printf "%s" ‘${TAX_MESSAGE}’
${TAX_MESSAGE}
```

在这种情况下，单引号阻止 Bash 将该值解释为变量替换，因为美元符号不被特殊对待。

反斜杠 (\) 就像一个字符的单引号，保持该字符不变。例如，要打印双引号，请执行以下操作：

```
$ printf "%s" "\"" 
"
```

反斜杠表示第二个引号标记应被视为字符，而不是引号对的结束引号。

printf 格式化代码 %q（引号处理）会在每个对 shell 有特殊含义的字符前打印反斜杠。使用此功能可确保空格保持不变。

```
$ printf "%q" "${TAX_MESSAGE}"
The\ tax\ is\ 7.25%
```

例如，从文件读取会受 %q 影响。如果打印的变量包含空格，除非用反斜杠保护，否则 read 会将空格视为分隔符。

```
$ printf "%q %q\n" "Alpha Systems Inc" "Key West, Florida" > company.txt
$ read COMPANY LOCATION < company.txt
$ printf "%s\n" "$COMPANY"
Alpha Systems Inc
```

```
$ printf "%s %\n" "Alpha Systems Inc" "Key West, Florida" > company.txt
$ read COMPANY LOCATION < company.txt
$ printf "%\n" "$COMPANY"
Alpha
```

read 命令不知道该行的哪些文本最初属于哪个变量。它假设值由空格分隔，并将 Alpha 分配给 COMPANY。当使用 %q 时，read 知道受反斜杠保护的空格属于第一个值，它会读取直到第一个未受保护的空格为止，从而将 Alpha Systems Inc 分配给 COMPANY。

单词拆分由特殊变量 IFS 的值控制。通常，IFS 将空格、制表符和换行符视为单词分隔符——即，它使用空白字符。如果更改 IFS 的内容，新字符将被用作单词分隔符。然而，这是为了与 Bourne shell 兼容的较旧功能，脚本不应更改 IFS 变量，因为现在有 %q 格式化等较新的功能可用。

每当分配值或用美元符号进行替换时，始终用双引号包围值是一个好习惯，以防止包含空格的值出现问题。

## 变量属性

所有 Bash 变量都存储为简单字符串。每个变量都有称为属性的特定选项，可以使用 declare 命令以类似 shell 选项和 shopt 命令的方式开启或关闭这些选项。

如果变量使用 -i（整数）开关声明，Bash 将为该变量开启整数属性。shell 会记住该字符串应作为整数值处理。如果向整型变量分配非数值，Bash 不会报告错误，而是分配值为零。

```
$ declare -i NUMBER_ACCOUNTS=15
$ printf "%d\n" "$NUMBER_ACCOUNTS"
15
$ NUMBER_ACCOUNTS="Smith"  # 错误
$ printf "%d\n" "$NUMBER_ACCOUNTS"
0
$ NUMBER_ACCOUNTS=12
$ printf "%d\n" "$NUMBER_ACCOUNTS"
12
```

有时尝试分配字符串会产生错误，但你不能依赖这种行为。

```
$ NUMBER_ACCOUNTS="Smith Account"  # 错误
bash: Smith Account: syntax error in expression (error token is `Account')
```

变量属性可以使用 `-p (print)` 开关显示。

```
$ declare -p NUMBER_ACCOUNTS
declare -i NUMBER_ACCOUNTS=\"12\"
```

信息以可以保存并在另一个脚本中使用的方式显示。这允许你在命令行提示符处尝试声明，然后在满意结果后将声明写入脚本文件。

可以使用加号关闭整数属性。

```
$ declare +i NUMBER_ACCOUNTS # 关闭整数属性
$ printf "$d\n" "$NUMBER_ACCOUNTS"
bash: printf: Smith Account: invalid number
$ printf "%s\n" "$NUMBER_ACCOUNTS"
Smith Account
```

虽然 Bash 不认为分配非数值是错误，但 `printf` 命令会报告该值无法格式化为数字。

与 `printf` 命令一样，整型变量也可以分配八进制或十六进制数字。

```
$ declare -i NUMBER_ACCOUNTS=0x0F
$ printf "%i\n" "$NUMBER_ACCOUNTS"
15
```

常量是不变的变量，使用 `-r (只读)` 属性创建。如果尝试向常量分配值，Bash 会报告错误。假设常量 `COMPANY` 包含公司名称。

```
$ declare -r COMPANY="Smith and Jones"
$ printf "%s\n" "$COMPANY"
Smith and Jones
$ COMPANY="Wilson Distribution"
bash: COMPANY: readonly variable
```

可以使用加号关闭 `readonly` 属性。然而，这可能会使脚本难以阅读，因为读者会假设只读变量始终是只读的。要么移除 `readonly` 属性，要么改变脚本结构。

## 数组

数组是使用 `-a (array)` 属性创建的值列表。一个称为*索引*的数字表示数组中项目的位置。Bash 数组与其他计算机语言中的数组不同，因为它们是开放的。数组可以是任意长度，并且初始时为空字符串填充项。

```
$ declare -a PRODUCTS
```

新项使用方括号表示列表中的位置分配给数组。第一个位置是位置零（不是一）。如果指定了初始值，则分配给第一个位置。分配一个值并不是特别有用，但为了与其他 shell 兼容而包含。或者，可以通过在方括号中包含位置将初始值分配给特定位置。

```
$ declare -a DEPT[0]="accounting" DEPT[1]="shipping" \
DEPT[2]="customer service"
```

由于使用方括号，需使用花括号界定变量名并超越 shell 的路径名匹配过程。

```
$ echo "${DEPT[0]}"
accounting
$ echo "${DEPT[2]}"
customer service
```

数组中所有未分配的位置没有值。例如，PRODUCTS 数组中的位置 5 最初是一个空字符串。可以通过赋值语句分配值 hammers。

```
$ printf "%s" "${PRODUCTS[5]}"

$ PRODUCTS[5]="hammers"
$ printf "%s" "${PRODUCTS[5]}"
hammers
```

如果位置零有项，当未指定位置时，它也返回该值。

```
$ PRODUCTS[0]="screwdrivers"
$ printf "%s" "${PRODUCTS}"
screwdrivers
$ printf "%s" "${PRODUCTS[0]}"
screwdrivers
```

可以使用星号 (*) 或 at 符号 (@) 访问整个数组的位置。这两个符号仅在双引号使用时有所不同：星号返回一个字符串，每个项由 IFS 变量的第一个字符（通常是空格）分隔，而 at 符号将每个项作为单独的字符串返回，没有分隔字符。

```
$ printf "%s" "${PRODUCTS[*]}"
screwdrivers hammers
/home/kbrutch $[bash]
$ printf "%s" "${PRODUCTS[@]}"
screwdrivershammers
```

在此示例中，at 符号版本需要两个单独的 `\s` 格式化代码才能正确显示数组，每个数组项一个。

```
$ printf "\s \s\n" "${PRODUCTS[@]}"
screwdrivers hammers
```

可以使用括号中的列表分配多个值。

```
$ DIVISIONS=("North America" "Europe" "Far East")
$ printf "%s\n" "${DIVISIONS[*]}"
North America Europe Far East
```

列表项可以有可选的下标。

```
$ DIVISIONS=([3]="North America" [2]="Europe" [1]="Far East")
$ printf "%s\n" "${DIVISIONS[*]}"
Far East Europe North America
```

结合列表和 `declare` 命令，数组可以在创建时分配值。

当在变量名前使用 `#` 且位置为 `*` 或 `@` 时，返回数组中的项目数量。项目不必连续分配，数量也不反映项目存储的位置。

```
$ printf "%s\n" "${#PRODUCTS[*]}"
2
```

可以使用 `unset` 命令删除单独的数组值。通过将数组位置分配空字符串来擦除值并不会销毁它：在计算项目时，空字符串仍被视为数组项。

`read` 命令可以使用 `-a`（数组）开关将列表读入数组。使用此开关时，输入行中的每个项都会读入单独的数组位置。

`array` 属性是唯一在开启后不能关闭的变量属性。如果 Bash 允许关闭该属性，当数组变为普通变量时，数组中的数据将会丢失。

## 导出变量和 Linux 环境

shell 变量仅存在于声明它们的脚本或交互会话中。为了使 shell 变量在其起源之外可用，必须将其声明为*可导出*。使用 `declare` 的 `-x` (*export*) 开关，通过 `export` 属性将变量标记为*可导出*。`export` 属性提醒 shell，你希望将变量“导出”或提供给脚本运行的所有程序。

例如，程序 `cvs` 需要名为 `CVSROOT` 的变量存在于其所有程序中。

```
$ declare -x CVSROOT="/home/cvs/cvsroot"
```




同样地，在你的配置文件脚本中声明的任何变量都必须被导出，否则它们在命令提示符下将不存在。在配置文件脚本运行完毕后，它们就会消失。

当变量被导出时，由脚本执行的程序所做出的任何更改都会在程序完成时被丢弃。如果第二个脚本将 `CVSROOT` 更改为值 `/home/local/cvsroot`，当第二个脚本结束时，`CVSROOT` 将再次变回 `/home/cvs/cvsroot`。这些更改会被“回滚”。

通过使用导出（export）和只读（read-only）开关来创建全局常量。

```bash
$ declare -rx COMPANY_BRANCH="West Coast Branch"
```

`COMPANY_BRANCH` 仅在当前脚本中是只读变量。当它被导出到第二个脚本时，它作为普通变量被导出——只读效果会丢失。这种奇怪行为的原因源于 Linux 在程序之间共享环境变量的方式，这与 Bash shell 本身无关。

*环境变量* 是 Linux 在程序及其执行者之间共享的变量。就像洋葱的层一样，每个程序必须显式地将变量导出到环境中，下一个程序才能看到它。

虽然 Linux 提供了导出环境变量的机制，但没有方式为它们分配任何属性。Linux 没有属性的概念。Bash 属性是在环境变量最初发明之后才想到的。当 Bash 变量交给 Linux 与一个新程序共享时，属性会丢失。当第二个 shell 脚本开始时，它无法知道原始属性是什么。

与新程序共享的变量是原始变量的副本。如果一个脚本声明了一个导出的变量并运行第二个脚本，第二个脚本对该变量所做的任何更改对第一个脚本都是不可见的。第二个脚本没有方式将新值分配给第一个脚本能看到的变量。与其他编程语言不同，导出 shell 变量是一条单行道。

假设有两个脚本，分别称为 *outer.sh* 和 *inner.sh*。`outer.sh` 声明一个变量，然后运行 `inner.sh` 脚本，如清单 5.1 和 5.2 所示。

### 清单 5.1 outer.sh

```bash
# outer.sh
#
# 此脚本首先运行。

declare -rx COMPANY_BRANCH="West Coast Branch"
bash inner.sh
printf "%s\n" "$COMPANY_BRANCH"

exit 0
```

### 清单 5.2 inner.sh

```bash
# inner.sh
#
# 此脚本由 outer.sh 运行。

printf "This is the inner script.\n"

declare -p COMPANY_BRANCH
COMPANY_BRANCH="East Coast Branch"
printf "%s\n" "$COMPANY_BRANCH"

printf "Inner script finished\n"

exit 0
```

当运行 `outer.sh` 时，`COMPANY_BRANCH` 变量是只读的。然而，在 `inner.sh` 内部，只读属性已丢失。`inner.sh` 将变量更改为新值，但当 `inner.sh` 结束时，`outer.sh` 显示该变量的值未变。

```bash
$ bash outer.sh
This is the inner script.
declare -x COMPANY_BRANCH="West Coast Branch"
East Coast Branch
Inner script finished
West Coast Branch
```

将值返回给调用程序的唯一方法是将值写入文件（或标准输出），然后由调用程序读取（或赋值）该值回变量。

## eval 命令

Bash 在命令中遇到变量时执行变量替换。在命令执行之前，Bash 会搜索命令中的所有美元符号，并在命令执行前插入变量的值。Bash 只执行一次这种替换。如果变量包含带有美元符号的值，并且该值被替换到命令中，则包含美元符号的值保持不变。

```bash
$ declare -rx COMPANY="Value Book Resellers"
$ declare -rx TITLE='$COMPANY'
$ printf "%s\n" "$TITLE"
$COMPANY
```

在执行 `printf` 之前，Bash 用 `$COMPANY` 的值替换了 `TITLE`。Bash 不会重复替换过程来用“Value Book Resellers”替换 `COMPANY` 变量。替换只执行一次。

在极少数情况下，你可能希望强制 Bash 执行额外的替换轮次。Bash 的 `eval` 命令可以按需执行替换并运行结果。以下是一个简单的示例，如清单 5.3 所示，其中显示屏幕上三个变量之一。

### 清单 5.3 eval_example.sh

```bash
# eval_example.sh

short -s -o nounset

declare -r DISPLAY_VARIABLE="'$SALES_EAST'"

declare -i SALES_EAST=1000
declare -i SALES_WEST=2000
declare -i SALES_NORTH=3000

printf "DISPLAY VARIABLE = %s\n" "$DISPLAY_VARIABLE"
printf "reprocessed with eval, DISPLAY_VARIABLE = %s\n" \
`eval printf "%s\n" "$SALES_EAST"`
```

此脚本可以显示公司三个分部之一的销售数据。常量 `DISPLAY_VARIABLE` 包含要显示的变量，即 `SALES_EAST`、`SALES_WEST` 或 `SALES_NORTH`。但如果替换 `DISPLAY_VARIABLE`，只会打印字符串“`$SALES_EAST`”。

反引号运行 `eval` 并执行新的替换集。结果可以替换到原始的 `printf` 命令中。现在结果正如你预期的那样。

```bash
$ bash eval_example.sh
DISPLAY VARIABLE = $SALES_EAST
reprocessed with eval, DISPLAY_VARIABLE = 1000
```

在这个示例中，Bash 首先将 `printf` 命令处理为

```bash
printf "reprocessed with eval, DISPLAY_VARIABLE = %s\n" \
`eval printf "%s\n" "$SALES_EAST"`
```

这仅打印 `$SALES_EAST`，因为 Bash 已完成变量值的替换。当 Bash 执行 `eval` 命令时，`printf` 命令会进行第二次检查。

```bash
printf "reprocessed with eval, DISPLAY_VARIABLE = %s\n" `printf "%s\n" 1000`
```

由于 Bash 还试图运行结果，需要 `echo` 命令（`printf` 的简化版本）。`eval` 尝试像执行命令一样执行重新评估的 `DISPLAY_VARIABLE`。也就是说，对于 `eval 1000`，Bash 会试图执行数字 `1000`，这不是你想要的结果。

虽然在这个示例中并不特别现实，但当用户输入要执行的命令，或从文件读取要执行的命令时，`eval` 命令很有用。只要使用 `eval` 处理它们，命令就可以包含变量、美元函数等。

一个常见的陷阱是没有跟进替换过程。例如，假设将 `DISPLAY_VARIABLE` 分配为 `$SALES_EAST` 值时，实际上被分配的是 `SALES_EAST`，并且在 `printf` 语句中添加了第二个美元符号：

```text
printf "reprocessed with eval, DISPLAY_VARIABLE = $a\n" \\
`eval printf "$a\n" "$$DISPLAY_VARIABLE"`
```

你会得到类似这样的响应：

```text
reprocessed with eval, DISPLAY_VARIABLE = 1423SALES_EAST
```

在这种情况下，第一次替换后的命令为：

```text
printf "reprocessed with eval, DISPLAY_VARIABLE = $a\n" \\
`eval printf "$a\n" $SALES_EAST`
```

但 `$a` 是一个内置 shell 函数。Bash 并不理解 `$SALES_EAST` 应该嵌套在第一个美元符号内部；它只是从左到右读取，并在读取时进行替换。第二次替换将执行 `$$` 函数，而不是替换 `SUM` 变量的值。要正确执行，你必须用反斜杠转义第一个美元符号，以防止 Bash 对其进行替换。

```text
printf "reprocessed with eval, DISPLAY_VARIABLE = $a\n" \\
`eval printf "$a\n" "\$DISPLAY_VARIABLE"`
```

第一次替换后，你得到：

```text
printf "reprocessed with eval, DISPLAY_VARIABLE = $a\n" \\
`eval printf "$a\n" "$SUM"`
```

这防止了 `$$` 被视为内置函数：Bash 代替替换为 `$SALES_EAST`。在第一个示例中，当美元符号位于 `DISPLAY_VARIABLE` 内部时，你避开了这些问题。

通过在正确的位置转义某些引号，也可以达到相同的效果。

变量和常量是所有脚本的构建模块，但如果没有表达式，它们仅作为存储容器。这些内容将在下一章（第 6 章，“表达式”）中介绍。

## story.bash：故事生成器

清单 5.4 是一个完整的示例，展示了本章中的一些概念。`story.bash` 是一个脚本，通过替换用户选择的词语来创建故事。





# 清单 5.4 story.bash

```bash
#!/bin/bash
# story.bash: a story generator
#
# Ken O. Burtch
# CVS: $header$

shopt -s -o nounset

declare NAME          # a name
declare COLOR         # a color
declare DAY           # a day
declare RELATIONSHIP  # a person's relationship
declare OBJECT        # an everyday object
declare -a ACTIVITY   # a list of everyday activities

# Instructions

printf "$s\n" "This is a story generator. I will ask you for some" 
printf "$s\n" "common words.  Then I will compose a story."
printf "\n"

# Read the variables

read -p "Enter a man's name            : " NAME
read -p "Enter a color (eg. red)      : " COLOR
read -p "Enter a day (eg. Monday)     : " DAY
read -p "Enter a person's relationship (eg. uncle): " RELATIONSHIP
read -p "Enter an everyday object (eg. pencil)     : " OBJECT
read -p "Enter an everyday activity (eg. sleeping): " ACTIVITY[0]
read -p "Enter an everyday activity (eg. reading): " ACTIVITY[1]
printf "\n"
read -p "Press return/enter to read your story"
printf "\n"

# Write the story

printf "$s\n" "$DAY at work, $NAME realized that he had forgotten to pack"
printf "$s\n" "a lunch.  Ignoring his $SHELL prompt, $NAME decided to head"
printf "$s\n" "out early and grab lunch from a street vendor." 
printf "$s\n" "As he got outside of the front door of the office,"
printf "$s\n" "$NAME ran into his $RELATIONSHIP carrying a"
printf "$s\n" "$COLOR $OBJECT.  His $RELATIONSHIP remarked that it had" 
printf "$s\n" "been $RANDOM days since $NAME had called.  $NAME"
printf "\n" "thought he would have been off surfing the net on his"
printf "\n" "GOSTYPE computer than running into his $RELATIONSHIP.  He"
printf "\n" "offered to take the $OBJECT to get polished." \
"  He went ${ACTIVITY[0]}"
printf "\n" "down the street, wishing that his $RELATIONSHIP had stayed"
printf "\n" "home ${ACTIVITY[1]} instead."

exit 0
```

## 参考部分

### Declare 命令开关

- `-a`—声明一个数组
- `-F`—显示函数及其定义
- `-f`—显示函数名称
- `-r`—声明一个只读变量
- `-x`—声明一个导出变量
- `-i`—声明一个整数变量

### Bash 预定义变量

- `auto_resume`—如果设置，允许对已停止作业的名称进行命令补全。
- `BASH`—shell 的完整路径名。
- `BASH_ENV`—在 shell 脚本中，显示在脚本启动前执行的 profile 文件的名称。
- `BASH_VERSION`—Bash 的版本（例如，2.04.0(1)-release）。
- `BASH_VERSINFO`—一个比 `BASH_VERSION` 包含更详细版本信息的数组。

| `BASH_VERSINFO[0]` | 主版本号（即发布版本）。 |
| :--- | :--- |
| `BASH_VERSINFO[1]` | 次版本号（即版本）。 |
| `BASH_VERSINFO[2]` | 补丁级别。 |
| `BASH_VERSINFO[3]` | 构建版本。 |
| `BASH_VERSINFO[4]` | 发布状态（例如，beta1）。 |
| `BASH_VERSINFO[5]` | MACHTYPE 的值。 |

- `CDPATH`—使用 `cd` 命令时要搜索的目录的冒号分隔列表。
- `COLUMNS`—显示屏上每行的字符数（例如，80）。
- `COMP_WORDS`—在可编程补全函数中，当前命令行中各个单词的数组。
- `COMP_WORDBREAKS`—在可编程补全函数中，当前 `COMP_WORDS` 单词。
- `COMP_LINE`—在可编程补全函数中，当前命令行。
- `COMP_POINT`—在可编程补全函数中，当前命令行光标位置。
- `COMPREPLY`—在可编程补全函数中，返回的补全列表。
- `DIRSTACK`—由 `dirs`、`popd` 和 `pushd` 使用的目录列表。
- `EUID`—当前用户的有效用户 ID。
- `FCEDIT`—`fc` 命令的默认文本编辑器。
- `FIGNORE`—文件名补全时要忽略的前缀或后缀的冒号分隔列表。
- `FUNCNAME`—如果在函数内部，则为该函数的名称。
- `GLOBIGNORE`—路径名扩展时要忽略的文件名的冒号分隔模式列表。
- `GROUPS`—用户所属组的列表（以数值格式）。
- `HISTCHARS`—用于命令历史扩展的字符列表。
- `HISTCMD`—当前命令在命令历史中的位置。
- `HISTCONTROL`—确定由空格开头的命令或重复命令是否放入命令历史中。
- `HISTFILE`—包含命令历史的文件。
- `HISTFILESIZE`—`HISTFILE` 命令历史文件的最大大小。
- `HISTIGNORE`—要保留在命令历史中的命令的冒号分隔模式列表。
- `HISTSIZE`—保留在命令行历史中的命令数量（例如，1000）。
- `HOSTNAME`—计算机的名称。在某些版本的 Linux 中，这是机器名称。在其他版本中，这是一个完全限定的域名。
- `HOSTTYPE`—计算机类型。
- `HOME`—你的主目录的名称。
- `IGNOREEOF`—如果此变量存在，则指示 Bash 退出前必须输入的 EOF 字符数。
- `IFS`—*内部字段分隔符*，`read` 命令用于将一行拆分为各个部分的字符列表。
- `INPUTRC`—Readline 启动文件的名称。
- `LANG`—用于确定任何未通过以 `LC_` 开头的变量特定选择的区域类别。
- `LC_ALL`—此变量覆盖 *LANG* 和指定区域类别的其他 *LC_* 变量的值。
- `LC_COLLATE`—控制路径名扩展和模式匹配的排序顺序。
- `LC_CTYPE`—控制路径名扩展和模式匹配使用的字符类别。
- `LC_MESSAGES`—对双引号字符串（前缀美元符号）进行翻译的区域设置。
- `LINENO`—脚本或函数中的当前行号。
- `LINES`—显示屏中的水平行数（例如，24）。
- `MACHTYPE`—对计算机的描述；$HOSTTYPE 和 $OSTYPE 的组合。
- `MAIL`—要检查传入邮件的文件名。它被 *MAILPATH* 取代。
- `MAILCHECK`—如果此变量存在，则指示检查 *MAILPATH* 中传入邮件的秒数。如果未设置值，默认值为 60 秒。
- `MAILPATH`—要检查传入邮件的文件的冒号分隔列表。
- `OSTYPE`—操作系统的名称。
- `OLDPWD`—前一个工作目录（由 `cd` 命令设置）。
- `OPTERR`—如果设置，`setopts` 显示错误消息。
- `PATH`—用于查找要执行的命令的搜索路径的冒号分隔列表。
- `PIPESTATUS`—包含上一个管道中每个命令退出状态值的数组。
- `PPID`—shell 父进程的进程 ID。
- `PROMPT_COMMAND`—在设置 `PS1` 主要提示字符串之前要执行的命令。
- `PS1`—主要提示字符串。
- `PS2`—次要提示字符串。
- `PS3`—select 命令提示字符串。
- `PS4`—跟踪命令输出前缀字符串。
- `PWD`—当前工作目录（由 `cd` 命令设置）。
- `RANDOM`—每次引用时返回 0 到 32767 之间的随机数。
- `OPTARG`—`getopts` 命令处理的最后一个参数。
- `OPTIND`—`getopts` 命令要处理的下一个参数的索引。
- `SECONDS`—自启动 Bash 以来的秒数。
- `SHELL`—首选使用的 shell，用于为你启动 shell 的程序。
- `SHELLOPTS`—当前启用的 shell 选项的冒号分隔列表。
- `SHVL`—每次在 Bash 内部启动新的 Bash 会话时，此变量递增。
- `TIMEFORMAT`—`time` 命令的格式。
- `TMOUT`—如果大于零，则指示交互式会话的超时秒数。此外，也是 `read` 命令的默认超时时间。
- `UID`—当前用户的 ID（`LOGNAME` 的数值等效值）。

Linux 发行版定义了额外的变量。这些变量的存在取决于你特定的发行版。许多是为特定应用程序的使用而声明的。

- `ETC_PROFILE`—如果 /etc/profile 被执行，则显示 1
- `DISPLAY`—X Window 显示服务器
- `CVSROOT`—CVS 仓库的位置
- `EDITOR`—你的默认编辑器。历史上，这在视觉编辑器不可用时用于指示要使用的行编辑器（参见 `VISUAL`）
- `KDEDIR`—KDE 桌面的父目录
- `HOST`—完全限定的主机名（例如，host.domain.com）
- `INPUTRC`—inputrc 文件的位置（例如，/etc/inputrc）
- `LESS`—包含 `less` 命令的默认开关
- `LESSOPEN`—`less` 用于打开文件的默认命令（例如，| /usr/bin/lesspipe.sh %s）
- `LESSCHARSET`—用于 `less` 的控台字符集（例如，lat1n1）
- `LS_COLORS`—控台上 `ls` 输出的默认颜色，覆盖 /etc/DIR_COLORS
- `LOGNAME`—当前登录的名称
- `ORGANIZATION`—你组织的名称（通常是 /etc/organization 的内容）





- `PRINTER` —— 默认打印机
- `QTDIR` —— 包含 `QT`（KDE 桌面的组件包）的目录
- `PAGER` —— 默认的分页程序，通常是 `less`
- `TMPDIR` —— 默认临时目录的路径
- `TERM` —— 终端模拟类型（例如，xterm 会话使用 `xterm`，Linux 控制台使用 `linux`）
- `USER` —— 你在 OpenLinux 中的用户名
- `VISUAL` —— 你的默认编辑器，通常与 `EDITOR` 相同
- `WINDOWMANAGER` —— 当前 X Windows 窗口管理器的路径

## 表达式

表达式是用于计算值的公式。Bash 有多个内置命令和函数用于计算表达式，但它们的语法或功能并不完全相同。在某些情况下，计算同一个表达式有多种方法。此外，还有许多专门用于罕见情况的特性。因此，很少有 Bash 程序员能记住所有的细微差别。

在我与已故教授兼作家 F. Ray Skilton 的众多对话之一中，我们在讨论使用下拉菜单作为工具时，它不是用来做选择，而是作为命令的记忆辅助工具。他离开他的 Atari 计算机，问我：“你学过足够多的计算机语言，以至于开始忘记那些很久没用的命令语法了吗？”我说：“并不是真的。”他咯咯一笑。“别担心——你会的。”

## 扩展

Bash 中的表达式不仅仅包含算术运算。因为变量是字符串，许多表达式涉及将某种简写符号替换为字符串所代表的完整值。这种字符串替换过程被称为扩展，因为在执行替换后，字符串通常会变长，从而变得更长。

路径名模式匹配就是字符串扩展的一个例子。星号、问号和其他字符会被它们所代表的文件名替换，从而创建一个更长、完整的字符串值。

Bash 将扩展分为六个独立的类别。Shell 始终按以下顺序评估它们：

- 文件名花括号扩展
- 路径名波浪号扩展
- 美元符号、变量和算术表达式
- 命令替换（从左到右执行）
- 单词拆分（即通过空白或 `IFS` 变量的内容进行参数分隔）
- 路径名扩展（即路径名模式匹配）

所有这些扩展将在本节的稍后部分详细讨论。

顺序很重要，并可能导致脚本中出现微妙的问题。假设你将一个包含波浪号的路径赋值给一个变量。

```
$ ls -d ~/tmp
/home/kyburg/ch/tmp
$ TMP="~/tmp"
$ ls $TMP
~/tmp not found
```

尽管目录 `~/tmp` 存在，且直接输入命令时 `ls` 可以找到它，但 `ls` 命令找不到目录 `~/tmp`。这个问题是由扩展的顺序引起的。因为变量扩展发生在波浪号扩展之后，Bash 首先尝试替换任何波浪号。由于只发现了一个变量，它替换了 `TMP` 的值。由于波浪号扩展已经完成，波浪号保留在命令中，`ls` 会在另一个名为 `~` 的目录内寻找 `tmp` 目录。如果扩展顺序可以反转，这种情况就不会发生。

因此，永远不要在赋值给变量的路径中使用波浪号。请改用 `HOME` 变量。

此处未列出的其他类型的扩展由命令处理。由于这些是必须执行的命令，它们只在 Bash 完成其六个扩展后运行。有两个常见的内置命令解释表达式。

`test` 命令检查多种条件，并指示条件是真还是假。`test` 可以比较文件、字符串或数字。不要将其与 Linux 的 `test` 命令混淆。

`let` 命令计算表达式，并在单个命令中将结果赋值给变量。

要测试结果，你需要一个检查测试结果并采取相应措施的命令。`if` 命令是一个不错的选择。

## 基本 `if` 命令

内置的 `if` 命令运行一个命令并检查结果。如果命令成功，它执行另一组命令。通常与 `if` 命令一起使用的唯一命令是 `test`。`if` 的其他用法在第 7 章“复合命令”中更详细地描述。

基本 `if` 命令的语法如下：

```
if test arguments; then
    statements to run
fi
```

关键字 then 被视为单独的命令，需要分号将其与 if 命令分隔开。关键字 fi 出现在 if 内部最后一条要执行的命令之后。

例如，test -f 命令检查文件是否存在。

```
if test -f ./report.out ; then
    printf "The report file ./report.out exists!\n"
fi
```

只有当文件存在时，才会打印消息“报告文件 ./report.out 存在！”。如果文件不存在，则跳过 printf 命令，执行继续到 fi 之后。

## 文件表达式

内置的 test 命令包含各种针对文件的测试。它可以测试文件类型、文件可访问性、比较文件年龄或其他文件属性。以下是 Bash 文件测试的完整列表：

- `-b file` —— 如果文件是块设备文件，则为真
- `-c file` —— 如果文件是字符设备文件，则为真
- `-d file` —— 如果文件是目录，则为真
- `-e file` —— 如果文件存在，则为真
- `-f file` —— 如果文件存在且是普通文件，则为真
- `-g file` —— 如果文件设置了 set-group-id 权限，则为真
- `-h file`（或 `-l file`）—— 如果文件是符号链接，则为真
- `-k file` —— 如果文件设置了 sticky 权限位，则为真
- `-p file` —— 如果文件是管道，则为真
- `-r file` —— 如果文件可读（由你的脚本读取），则为真
- `-s file` —— 如果文件存在且不为空，则为真
- `-S file` —— 如果文件是套接字，则为真
- `-t fd` —— 如果文件描述符在终端上打开，则为真
- `-u file` —— 如果文件设置了 set-user-id 权限，则为真
- `-w file` —— 如果文件可写（由你的脚本写入），则为真
- `-x file` —— 如果文件可执行（由你的脚本执行），则为真
- `-O file` —— 如果文件（有效地）归你所有，则为真
- `-G file` —— 如果文件（有效地）归你的组所有，则为真
- `-N file` —— 如果文件有新内容（自上次读取以来），则为真
- `f1 -nt f2` —— （较新）如果文件 f1 比 f2 新，则为真
- `f1 -ot f2` —— （较旧）如果文件 f1 比 f2 旧，则为真
- `f1 -ef f2` —— （等效文件）如果文件 f1 是 f2 的硬链接，则为真

文件测试通常用于脚本开头的健全性检查。它们可用于检查所有文件是否存在且可读（如有必要还可写）。所有命令必须可执行（见清单 6.1）。

# 清单 6.1 archive.bash

```
#!/bin/bash
#
# archive.bash - 归档旧订单文件
#
# Ken O. Burtch
# CVS: $Header$
shopt -s -o nounset
## 全局声明
declare -rx SCRIPT=${0##*/}           # SCRIPT 是该脚本的名称
declare -rx who="/usr/bin/who"       # who 命令 - man 1 who
declare -rx TMP="/tmp/temp.$$"       # TMP 是一个临时文件
## 健全性检查
if test ! -x "$who" ; then
        printf "${SCRIPT}:$LINENO: the command $who is not available - aborting" >&2
        exit 192
fi
if test -f "$TMP" ; then
        if test ! -w "$TMP" ; then
                printf "${SCRIPT}:$LINENO: the temp file $TMP exists and cannot "\
"be overwritten - aborting" >&2
                exit 192
        fi
fi
```

此脚本片段确保 who 命令可执行，且 TMP 中指定的临时文件要么不存在，要么存在但可被覆盖。

## 多个测试

单个测试可以通过 -a（与）和 -o（或）开关组合在一起。前一部分中的临时文件测试可以重写为：

```
if test -f "$TMP" -a ! -w "$TMP" ; then
printf "${SCRIPT}:${LINENO}: the temp file $TMP exists and cannot "\
"be overwritten - aborting" >&2
exit 192
fi
```

这与以下写法并不完全相同

```
if test -f "$TMP" && test ! -w "$TMP" ; then
printf "${SCRIPT}:${LINENO}: the temp file $TMP exists and cannot "\
"be overwritten - aborting" >&2
exit 192
fi
```

使用 && 的版本执行 test 命令两次，可能比使用 -a 开关的版本运行得更慢，因此在 if 表达式中优先选择 -a 开关而不是使用 &&。

只要用反斜杠转义，也可以使用括号。括号对 shell 有特殊含义。在某些情况下，它们是必需的。

一种往往使 shell 程序员困惑的情况是当 not 运算符与 -a 或 -o 开关混合使用时。在大多数计算机语言中，not 作为一元运算符具有优先级并首先执行。在 Bash 中，-a 和 -o 的优先级高于 not 运算符，导致以下测试始终为假：

```
if test ! -f "$TMP" -o -f "$TMP" ; then
```

Bash 将此命令解释为“如果文件既不存在又不存在”。这种怪异行为符合 POSIX 标准。要获得预期结果，必须使用括号。

```
if test \( ! -f "$TMP" \) -o -f "$TMP" ; then
```

方括号是 test 命令的另一种形式。使用方括号可以使你的 if 命令更易读。

```
if [ -f "$TMP" -a ! -w "$TMP" ] ; then
printf "${SCRIPT}:${LINENO}: the temp file $TMP exists and cannot "\
"be overwritten - aborting" >&2
exit 192
fi
```

方括号版本在各方面都与普通的 test 命令相同。Korn shell 引入了 test 命令的一种变体，使用双方括号。Bash 为了兼容性支持这种变体。Korn shell 的 test 不会在括号之间执行单词拆分或路径名扩展，使得变量替换周围的双引号变得不必要。

```
if [ [ -f $FILE ] ] ; then
printf "%s\n" "The file exists"
fi
```





它还增强了模式匹配功能，但缺乏 Bash `test` 命令的许多特性。除非你正在将 Korn shell 脚本移植到 Bash，否则强烈建议不要使用 Korn shell 的 `test` 命令。

## 字符串

`test` 命令可以比较两个字符串。

- `-z s`—*(零长度)* 如果字符串为空，则为真
- `-n s`（或仅 *s*）—*(非空)* 如果字符串不为空，则为真
- *s1* = *s2*—如果字符串 *s1* 等于 *s2*，则为真
- *s1* != *s2*—如果字符串 *s1* 不等于 *s2*，则为真
- *s1* < *s2*—如果字符串 *s1* 小于 *s2*，则为真
- *s1* > *s2*—如果字符串 *s1* 大于 *s2*，则为真

```bash
DAY=`date '+%a'`
if [ "$DAY" = "Mon" ] ; then
    printf "The weekend is over...get to work!\n"
fi
```

`-z`（*零长度*）和 `-n`（*非零长度*）选项分别是 `=` 和 `!=` 的简写形式。请注意，没有大于等于或小于等于运算符。你可以通过结合两个测试并使用 `-a` 选项来模拟这些运算符。

如果你习惯使用其他计算机语言，请记住 `test` 命令中使用的引号并非用于字符串界定，而是用于特殊字符处理。

由于小于号和大于号运算符也用于 shell 的重定向，因此必须将这些运算符加上引号，以防止 Bash 将其解释为重定向符号，而不是传递给 `test` 命令。

```bash
COMPANY="Athabasca"
if [ "$COMPANY" \< "M" ] ; then
    printf "The company name begins with a letter less than M\n"
fi
```

字符串比较的一个常见用途是测试 shell 标志变量。*标志*是用于指示特定条件是否为真的变量。它们提供了一种记住先前测试的方法。

可以使用任意一对值来表示标志的状态，例如 true 和 false，或者 yes 和 no。然而，当标志包含诸如 "NO" 这样的意外字符串时，这可能会导致条件歧义。传统上，如果变量包含除空字符串以外的任何内容，该条件被视为真。

```bash
WEEKEND=
DAY=`date '+%a'`
if [ "$DAY" = "Sat" -o "$DAY" = "Sun" ] ; then
    WEEKEND=1
fi

# 要确定是否为周末，使用 -n（非空）和 -z（空）。
if [ -n "$WEEKEND" ] ; then
    printf "The weekend is here\n"
else
    printf "It isn't the weekend\n"
fi
```

## 算术表达式

内置的 `let` 命令执行数学计算。`let` 期望一个包含变量、等号和待计算表达式的字符串。结果将被赋值给该变量。

```bash
$ let "SUM=5+5"
$ printf %d "$SUM"
10
```

在字符串中扩展变量名时不需要使用 `$`。`let` 理解等号右侧出现的任何变量都需要将其值代入表达式中。

```bash
$ let "SUM=SUM+5"
$ printf %d "$SUM"
15
$ let "SUM=SUM-5"
$ printf %d "$SUM"
10
```

可选的美元符号是 `let` 命令的一个特殊功能，不适用于其他命令。

如果变量使用 `-i` 选项声明为整数，则 `let` 命令是可选的。

```bash
$ declare -i SUM
$ SUM=SUM+5
$ printf %d "$SUM"
15
```

如果 `SUM` 是一个字符串变量，它将被赋值为字符串 `"SUM+5"`：

```bash
$ unset SUM
$ declare SUM=0
$ SUM=SUM+5
$ printf %s "$SUM"
SUM=5
```

出现在 `let` 表达式中的任何特殊字符都必须加上引号，以防止 Bash 对其进行扩展。

`let` 命令提供四个基本数学运算符，外加一个取模运算符。只允许整数表达式（不允许小数点）。

```bash
$ let "RESULT=5 + 2"
$ printf "5 plus 2 is %d\n" "$RESULT"
5 plus 2 is 7

$ let "RESULT=5 - 2"
$ printf "5 minus 2 is %d\n" "$RESULT"
5 minus 2 is 3

$ let "RESULT=5 * 2"
$ printf "5 times 2 is %d\n" "$RESULT"
5 times 2 is 10

$ let "RESULT=5 / 2"
$ printf "5 divided by 2 is %d\n" "$RESULT"
5 divided by 2 is 2

$ let "RESULT=5 % 2"
$ printf "remainder of 5 divided by 2 is %d\n" "$RESULT"
remainder of 5 divided by 2 is 1
```

以下是按优先级排列的算术运算符。对于 C 语言程序员来说，许多这些运算符都很熟悉：

- `-,+`— 一元减号加号
- `!`— 逻辑和非取反（要使用 `!`，需禁用 shell 历史记录）
- `*, /, %`— 乘法、除法和取模
- `+, -`— 加法和减法
- `<<, >>`— 左移和右移
- `<=, >=, <, >`— 比较
- `==, !=`— 相等和不等
- `&`— 按位与
- `^`— 按位异或
- `|`— 按位或
- `&&`— 逻辑与
- `||`— 逻辑或
- `expr ? expr :`— 条件表达式
- `=, *=, /=, %=, +=, -=, <<=, >>=, &=, ^=, |=`— 自引用操作

例如，要四舍五入到最近的 10，请执行以下操作：

```bash
$ declare -i COST=5234
$ COST=$((COST+5)/10*10)
$ printf '%d\n' $COST
5230
```

必须转义括号，以防止 shell 将其视为对子 shell 的引用。

`let` 命令还可以处理八进制和十六进制值。

```bash
$ declare -i OCTAL=0
$ let "OCTAL=0775"
$ printf '%d\n' "$OCTAL"
509
```

这些操作将在下一节中描述。

## 逻辑表达式

在 `let` 中，真由值 1 表示，假由 0 表示。除 1 或 0 以外的任何值都被视为真，但逻辑运算符本身仅返回 1 或 0。

请记住，逻辑真（值大于零）与命令的成功（状态代码为零）不同。在这方面，`test` 和 `let` 是相互对立的。

要在 shell 提示符下使用逻辑取反，必须禁用 shell 历史记录选项，否则 Bash 会将 `!` 解释为历史记录查找请求。

```bash
$ let "RESULT=!0"
$ printf "logical negation of 0 is %d\n" "$RESULT"
logical negation of 0 is 1

$ let "RESULT=!1"
$ printf "logical negation of 1 is %d\n" "$RESULT"
logical negation of 1 is 0

$ let "RESULT=1 && 0"
$ printf "logical and of 1 with 0 is %d\n" "$RESULT"
logical and of 1 with 0 is 0

$ let "RESULT=1 || 0"
$ printf "logical or of 1 with 0 is %d\n" "$RESULT"
logical or of 1 with 0 is 1
```

没有逻辑异或运算符。

## 关系操作

与字符串比较不同，`let` 提供了一套完整的数值比较。这些比较的价值有限，因为大多数比较都是使用 `if` 命令中的 `test` 命令进行测试的，从而导致两套测试。在逻辑表达式中，0 表示失败。

```bash
$ let "$RESULT=1 > 0"
$ printf "1 greater than 0 is %d\n" "$RESULT"
1 greater than 0 is 1

$ let "$RESULT=1 >= 0"
$ printf "1 greater than or equal to 0 is %d\n" "$RESULT"
1 greater than or equal to 0 is 1

$ let "$RESULT=1 < 0"
$ printf "1 less than 0 is %d\n" "$RESULT"
1 less than 0 is 0

$ let "$RESULT=1 <= 0"
$ printf "1 less than or equal to 0 is %d\n" "$RESULT"
1 less than or equal to 0 is 0

$ let "$RESULT=1 == 0"
$ printf "1 equal to 0 is %d\n" "$RESULT"
1 equal to 0 is 0

$ let "$RESULT=1 != 0"
$ printf "1 not equal to 0 is %d\n" "$RESULT"
1 not equal to 0 is 1
```

## 位操作

还有一组位运算符，如下所示。

```bash
$ let "$RESULT=~5"
$ printf "bitwise negation of 5 is %d\n" "$RESULT"
bitwise negation of 5 is -6

$ let "$RESULT=5 >> 2"
$ printf "5 right-shifted by 2 is %d\n" "$RESULT"
5 right-shifted by 2 is 1

$ let "$RESULT=5 << 2"
$ printf "5 left-shifted by 2 is %d\n" "$RESULT"
5 left-shifted by 2 is 20

$ let "RESULT=5 & 3"
$ printf "bitwise and of 5 with 3 is %d\n" "$RESULT"
bitwise and of 5 with 3 is 1

$ let "RESULT=5 | 3"
$ printf "bitwise or of 5 with 3 is %d\n" "$RESULT"
bitwise or of 5 with 3 is 7

$ let "RESULT=5 ^ 3"
$ printf "bitwise exclusive-or of 5 with 3 is %d\n" "$RESULT"
bitwise exclusive-or of 5 with 3 is 6
```

## 自引用操作

自引用运算符是结合赋值与其他基本操作之一的简写形式。该操作使用赋值变量执行，然后将结果赋给赋值变量。例如，`RESULT+=5` 是 `RESULT=RESULT+5` 的简写形式。

```bash
$ let "RESULT=5"
$ let "RESULT+=5"
$ printf "The result is %d\n" "$RESULT"
The result is 10
```

其他自引用运算符包括乘法 (*=)、除法 (/=)、取模 (%=)、减法 (-=)、右移 (<<=)、左移 (>>=)、按位与 (&=)、按位异或 (^=) 和按位或 (|=)。

请注意，某些类型的自引用操作无法用简写运算符表达。`RESULT=RESULT-10` 可以写为 `RESULT-=10`，但 `RESULT=10-RESULT` 必须完整写出。

递增 (++) 运算符为变量加一。递减运算符 (-- ) 使变量减一。

```bash
$ let "CNT=0"
$ let "CNT++"
$ printf "%d\n" "$CNT"
1
```

当在另一个表达式中使用递增或递减时，运算符的位置很重要。如果运算符放在变量之前，表示应在表达式的其余部分之前更新变量。如果运算符放在变量之后，更新将在表达式求值之后发生。

```bash
$ let "CNT=5"
$ let "PRODUCT=0"
$ let "PRODUCT+=CNT*5"
$ printf "%d\n" "$PRODUCT"
25
```





```
30
$ let "CNT=5"
$ let "PRODUCT=CNT++*5"
$ printf "%d\n" "$PRODUCT"
25
$ printf "%d\n" "$CNT"
6
```

通常来说，避免使用带有此类“副作用”的表达式是个好主意，因为这会使脚本更难维护。相反，应在单独的行上执行递增和递减操作，以使结果更易于阅读。

自引用运算符不能在没有 `let` 语句的情况下与整数变量一起使用。

```
$ COST+=5
bash: COST+=5: command not found
```

## `let` 的其他功能

表达式中允许使用括号。

```
$ let "RESULT=(5+3)*2"
$ printf "The expression is %d" "$RESULT"
The expression is 16
```

`let` 命令中的赋值是一个返回被赋值值的运算符。因此，可以同时为多个变量赋值。

```
$ let "TEST=TEST2=5"
$ printf "The results are %d and %d\n" "$TEST" "$TEST2"
The results are 5 and 5
```

`let` 可以一次评估多个表达式。可以将多个小的赋值组合在一行中。

```
$ let "SUM=5+5" "SUM2=10+5"
```

在单个 `let` 命令中包含过多的赋值会导致脚本的可读性问题。当每个 `let` 都位于单独一行时，更容易在脚本中查找特定的赋值。

条件表达式运算符 (?) 是 `if` 语句的简写形式，用于根据左侧条件评估两个不同的表达式之一。由于这是 `let` 命令的一个特性，它仅适用于数值表达式，不适用于字符串。以下示例将真值限制为 1 或 0。

```
$ VALUE=5
$ let "RESULT=VALUE > 1 ? 1 : 0"
$ printf "%d\n" "$VALUE"
1
```

可以将多个条件表达式运算符串联使用。

```
$ FILE_COUNT='ls -1 | wc -1'
$ let "RESULT=FILE_COUNT=0? 0: (FILE_COUNT%2 == 0 ? \"$FILE_COUNT/2 : FILE_COUNT/2+1)"
$ printf "The files will fit in a report with 2 columns %d high\n" "$RESULT"
The files will fit in a report with 2 columns 11 high
$ printf "%d" "$FILE_COUNT"
22
```

双括号是 *let* 的别名。它们用于将 *let* 表达式作为参数嵌入到另一个命令中。Shell 会用表达式的值替换双括号。

```
declare -i X=5;
while (( X > 0 )) ; do
        printf "%d\n" "$X"
done
```

此脚本片段打印出从 4 到 0 的数字列表。嵌入的 *let* 在每次循环时将 X 减少 1，并检查 X 的值何时达到 0。

### temperature.bash：华氏度转摄氏度

为了复习 *let* 算术，脚本 *temperature.bash*（如列表 6.2 所示）将温度从华氏度转换为摄氏度。

**列表 6.2 temperature.bash**

```
#!/bin/bash
#
# temperature.bash: Convert Fahrenheit to Celsius
#
# Ken O. Burch
# CVS $Header$

short -s -o nouse

declare -i FTEMP  # Fahrenheit temperature
declare -i CTEMP  # Celsius temperature

# Title

printf "%s\n" "Fahrenheit-Celsius Conversion"
printf "\n"

# Get the value to convert

read -p "Enter a Fahrenheit temperature: " FTEMP

# Do the conversion

CTEMP="`(${'$'}FTEMP-32) /9`"
printf "The Celsius temperature is %d\n" "CTEMP"

exit 0
```

### 算术测试

`test` 命令可以比较数值，但它使用的运算符与用于比较字符串值的运算符不同。由于所有 shell 变量都存储为字符串，变量可以根据所选的运算符被当作数字或字符串进行比较。Perl 程序员会发现这与 Perl 类似。如果将字符串运算符用于整型变量，Bash 不会报告错误。

- `n1 -eq n2` — (*相等*) 如果 n1 等于 n2 则为真
- `n1 -ne n2` — (*不相等*) 如果 n1 不等于 n2 则为真
- `n1 -lt n2` — (*小于*) 如果 n1 小于 n2 则为真
- `n1 -le n2` — (*小于或等于*) 如果 n1 小于或等于 n2 则为真
- `n1 -gt n2` — (*大于*) 如果 n1 大于 n2 则为真
- `n1 -ge n2` — (*大于或等于*) 如果 n1 大于或等于 n2 则为真

例如，假设 `RESULT` 包含当前目录中的文件数量。

```
$ RESULT=`ls -1 | wc -1`
$ printf "4d" "$RESULT"
22
$ test "$RESULT" -gt 20 && printf "&s" "There are a lot of files."
There are a lot of files.
$ test "$RESULT" -le 20 && printf "There are few files"
$
```

这些测试与字符串比较测试不同。考虑以下示例。

```
$ test "$RESULT" \< 3 && printf "As a string, the result is less than 3"
As a string, the result is less than 3
```

在这种情况下，字符串 22 与字符串 3 进行比较，由于字符串 22 在字母顺序上小于 3，因此消息被打印出来。请确保选择正确的运算符进行比较。

### 模式识别

Bash 的模式识别被称为 *globbing*（通配符匹配）。Globbing 用于匹配传递给命令的文件名，也被 Korn shell 的 *test* 命令用于匹配字符串。

```
$ ls *.txt
notes.txt     project_notes.txt
```

模式识别功能通过提供通配符符号来工作，Bash 会尝试将这些符号匹配到字符串或文件名。

星号 (*) 字符表示零个或多个字符。Korn shell 的 test 可用于将变量的值与带星号的字符串进行匹配。

```
COMPANY="Athabasca"
if [[ $COMPANY = A* ]] ; then
      printf "The company name begins with a letter a \n"
fi
if [[ $COMPANY = ?* ]] ; then
      printf "The company name begins with a letter a ?\n"
fi
```

当使用引号时，这种行为不起作用。引号告诉 Korn shell 的 *test* 命令不要解释特殊字符。对 "A*" 的测试将指示名为 "A*" 的文件。

```
COMPANY="Athabasca"
if [[ "$COMPANY" = "A*" ]] ; then
      printf "The company name is A*\n"
fi
```

问号 (?) 字符是一个通配符，代表任意单个字符。

```
COMPANY="AIC"
if [[ $COMPANY = A?? ]] ; then
      printf "The company name is 3 characters beginning with A\n"
fi
```

您可以使用方括号指定一组字符。您可以列出单个字符或范围。

```
if [[ $COMPANY = [ABC]* ]] ; then
      printf "The company name begins with a A, B or C\n"
fi
if [[ $COMPANY = [A-Z]* ]] ; then
      printf "The company name begins with a letter an uppercase letter\n"
fi
if [[ $COMPANY = [A-Z0-9]* ]]; then
    printf "The company name begins with a letter an uppercase letter or number\n"
fi
```

允许部分范围。如果省略范围的起始，则范围为该字符之前的所有 ASCII 值。同样，可以省略范围的结束以指定范围起始字符之后的任何 ASCII 字符。

如果方括号集中的第一个字符是感叹号 (!) 或插入符 (^)，则不在集中的字符计为匹配。

如果使用 `shopt -s extglob` 开启扩展 glob 选项，Bash 支持几种额外的模式：

- `?(pattern-list)` — 匹配给定模式零次或一次
- `*(pattern-list)` — 匹配给定模式零次或多次
- `+(pattern-list)` — 匹配给定模式一次或多次
- `@(pattern-list)` — 精确匹配给定的一个模式
- `!(pattern-list)` — 匹配除给定模式外的任何内容

```
COMPANY="AAA Ballistics Ltd"
if [[ $COMPANY = +([A]*Ltd ) ]]; then
    printf "The company name begins with one or more A's and finishes with Ltd\n"
fi
```

您可以使用垂直线字符 (|) 分隔模式列表。

```
COMPANY="Champion Ltd"
if [[ $COMPANY = Champion*([Ltd|Corp|Inc] ) ]]; then
    printf "The company name is Champion with a standard business ending\n"
fi
```

Bash 为常见范围定义了简写形式，称为字符类：

- `[:alnum:]` — 字母数字
- `[:alpha:]` — 字母
- `[:ascii:]` — ASCII 字符
- `[:blank:]` — 空格或制表符
- `[:cntrl:]` — 控制字符
- `[:digit:]` — 十进制数字
- `[:graph:]` — 非空格字符
- `[:lower:]` — 小写字母
- `[:print:]` — 非控制字符
- `[:punct:]` — 标点符号字符





- `[::space:]`—空白字符
- `[::upper:]`—大写字母
- `[::xdigit:]`—十六进制数字

例如，`[::lower:]` 等同于范围 `[a-z]`。

```
COMPANY="2nd Rate Solutions"
if [[ $COMPANY = [[:digit:]*]] ] ; then
    printf "Company name starts with a digit\n"
fi
```

对于多语言脚本，Bash 会根据“等价类”匹配字符。如果范围是由一对等号包围的字符，Shell 将匹配该字母或来自相关字母表的相似字母。

```
COMPANY="EZ Consulting Services"
if [[ $COMPANY = [=E=* ] ] ; then
    printf "Company name starts with an E (or a similar character)\n"
fi
```

此测试将匹配包含类似 E 的字母的字符串，例如法文 É。

特定的排序符号可以通过 `[.s.]` 进行匹配，其中 *s* 是要匹配的符号。

在 Korn shell 的 `test` 命令之外，Shell 的行为工作方式大致相同。不是匹配字符串中的字符，而是通过模式匹配来匹配文件中的字符。所有功能，包括扩展通配符功能，工作方式都相同。

```
$ ls .*(.c|,).h
actions.c  coedit.c  config.c  dump.c  form.c  form.h  main.c
```

唯一的区别在于点号（`.`）的使用。因为前导点号代表 Linux“隐藏”文件，所以除非在模式表达式中指定了前导点号，否则这些文件通常保持不可见。

```
$ ls .*(.c|,).h
.hidden.c
```

因为由 Bash 执行扩展，所以所有命令都以相同方式处理这些模式。

```
$ wc -l .*(.c|,).h
     96  actions.c
    201  coedit.c
     24  config.c
    103  dump.c
     88  form.c
     12  form.h
    305  main.c
    829  total
```

如果模式不匹配任何文件，Bash 假定该模式是您打算传递给命令的文件名。

```
$ ls X*
X* not found
```

在这种情况下，没有以字母 X 开头的文件。Bash 在未能找到匹配项时，将模式 X* 作为文件名传递给 ls 命令。

## 通配符选项

有一些影响模式匹配的 Shell 选项。可以通过设置 noglob Shell 选项（shopt -s -o noglob）完全关闭文件名模式匹配。如果设置了 nullglob 选项（使用 shopt -s nullglob），则在未匹配时该模式将被丢弃。在上面的示例中，ls 将不会接收到任何参数，并将列出当前目录中的所有文件。可以通过设置 nocaseglob 选项（shopt -s nocaseglob）来禁用大小写敏感性。同样，通过设置 dotglob 选项（shopt -s dotglob），可以关闭对文件名中前导点号的特殊处理。

这些 Shell 选项具有广泛的影响；请谨慎使用。尽量在脚本的最少行数中更改设置，并清楚地注释说明更改的效果。

GLOBIGNORE 变量也会影响文件名的匹配方式。该变量类似于 PATH 变量；它是一个由冒号分隔的文件名列表，Bash 不会尝试匹配这些文件。如果您知道文件名中包含模式符号的文件，将它们添加到 GLOBIGNORE 列表中可确保 Bash 将它们视为文件而不是通配符表达式。

如果您需要更复杂的模式识别，或者需要将模式应用于整个文件，可以使用 grep 系列命令。这些内容在第 11 章“文本文件基础”和第 12 章“文本文件处理”中有描述。

## 文件名大括号扩展({...})

使用大括号可以将一个文件名扩展为多个文件名。在大括号内部，使用逗号按顺序列出每个子字符串，以构建新的参数。大括号扩展通常用于指定具有不同扩展名的根文件名。

```
$ printf '%s %s \n\n' "Files should be named:" orders.{txt,.out}
Files should be named: orders.txt orders.out
```

因为 Bash 将第一行扩展为以下内容：

```
$ printf '%s %s \n\n' "Files should be named:" orders.txt orders.out
```

所以需要三个 %s 代码，对应 printf 的每个参数。

大括号内可以包含文件匹配字符。实际的文件匹配发生在 Bash 处理完大括号之后。

## 美元符号替换

美元符号不仅用于变量替换。存在多种美元扩展，其中一些替换字符串值，另一些则模拟诸如 `wc` 和 `sed` 等 Linux 命令的功能。通过使用美元符号表达式，Shell 无需启动这些程序，因此运行速度更快。

### ANSI C 转义扩展 ($'...')

如果美元符号后跟单引号字符串，则将在该字符串中查找 ANSI C 转义序列，并将这些序列替换为对应的字符。可接受的转义序列类似于 `printf` 命令使用的特殊格式转义代码：

- `\a`—警报（铃声）
- `\b`—退格
- `\cC`—控制字符 *C*（例如，G 表示控制-G）
- `\e`—转义字符
- `\f`—换页
- `\n`—换行
- `\r`—回车
- `\t`—水平制表符
- `\v`—垂直制表符
- `\\`—字面量反斜杠
- `\'`—单引号
- `\nnn`—字符的 ASCII 八进制值（最多三位数）
- `\xnnn`—字符的 ASCII 十六进制值（最多三位数）

```
$ printf "%s\n" $'\nline 2\newline 3'
line 1
line 2
line 3
```

### 本地化翻译 ($"")

如果美元符号后跟双引号字符串，则该字符串将被翻译成当前本地化的字符集。

```
$ printf "%s\n" "To a new locale"
To a new locale
```

第 18 章“最终话题”中简要讨论了本地化。

## 变量名匹配 (!*)

如果大括号内的内容以感叹号 (!) 开头并以星号 (*) 结尾，则返回所有以指定字母开头的变量的列表。

```
$ COMPANY="Nightlight Inc."
$ printf "%s\n" "${COMP*}"
COMPANY
```

## 变量长度 (#)

带有大括号和前置井号 (#) 的美元符号返回变量内容的长度。

```
$ printf "%s\n" "${#COMPANY}"
15
```

星号或 at 符号返回 Shell 脚本中参数的数量。

```
$ printf "%s\n" "${#*}"
0
```

这与 $* 类似。

## 默认值 (:-)

如果大括号中的内容包括变量名后的尾部冒号减号，则可以指定一个默认值，如果变量为空字符串，则替换为该值。

```
$ COMPANY=
$ printf "%s\n" "${COMPANY:-Unknown Company}"
Unknown Company
```

变量的实际值保持不变。
可以移除冒号以忽略默认值：

```
$ COMPANY=
$ printf "%s\n" "${COMPANY-Nightlight Inc.}"
```

## 默认值分配 (:=)

如果在大括号中，变量名后出现尾部冒号等号，则如果变量为空字符串，将向该变量分配默认值。

```
$ printf "%s\n" "${COMPANY:=Nightlight Inc.}"
Nightlight Inc.
$ printf "%s\n" "$COMPANY"
Nightlight Inc.
```

变量的实际值已更改。通过移除冒号，不会发生分配。

## 变量存在性检查 (:?)

如果变量名后出现尾部冒号问号，则返回问号后的消息，并且 Bash 脚本退出。这提供了一些粗略的完整性检查形式。该消息是可选的。

```
$ printf "Company is %s\n" \
"${COMPANY:?Error: Company has not been defined—aborting}"
```

通过移除冒号，不会执行检查。

## 覆盖默认值 (:+)

如果变量名后出现尾部冒号加号，则加号后的消息将替换字符串的值。空字符串保持不变。

```
$ COMPANY="Nightlight Inc."
$ printf "%s\n" "${COMPANY:+Company has been overridden}"
Company has been overridden
```

通过移除冒号，具有空字符串的变量也会被替换。

## 子字符串 (:n)

如果变量名后出现尾部的冒号后跟数字，则返回子字符串。该数字指示子字符串的第一个位置，减去一。字符串中的第一个字符是字符 0。可选地，后面可以跟随冒号和第二个数字，指示子字符串的长度。

```
$ printf "%s\n" "${COMPANY:5}"
light Inc.
$ printf "%s\n" "${COMPANY:5:5}"
light
```

## 按模式移除子字符串 (%, #, %%, 和 ##)

如果变量名后出现尾部井号，则返回的子字符串已移除匹配的模式。一个井号匹配尽可能小的子字符串，两个井号匹配尽可能大的子字符串。该表达式返回模式右侧的字符。

```
$ printf "%s\n" "${COMPANY#*l*}"
ghlight Inc.
$ printf "%s\n" "${COMPANY##*1*}"
$ printf "%s\n" "${COMPANY##*+*}"
```




```
Inc.
$ printf "%s\n" "${COMPANY#*t}"
light Inc.
```

使用百分号（%），表达式返回位于模式左侧的字符。

```
$ printf "%s\n" "${COMPANY%t}"
Nightligh
$ printf "%s\n" "${COMPANY%%t}"
Nigh
```

## 通过模式替换子字符串（//）

如果变量后跟一个斜杠（/），则替换斜杠后的模式首次出现的位置。在模式之后，有一个第二个斜杠和替换字符串。如果变量后跟两个斜杠，则替换模式的所有出现位置。

```
$ printf "%s\n" "${COMPANY/Inc./Incorporated}"
Nightlight Incorporated
$ printf "You are the I in %s" "${COMPANY//I/1}"
You are the I in Night1ight Inc.
```

如果模式以数字符号（#）开头，则模式在变量值的开头匹配。如果模式以百分号（%）结尾，则模式在变量值的结尾匹配。其他出现位置将被忽略。

```
$ COMPANY="NightLight Night Lighting Inc."
$ printf "%s\n" "${#COMPANY}"
NightLight Night Lighting Inc.
$ printf "%s" "${COMPANY//Night/NIGHT}"
NIGHTlight NIGHT Lighting Inc.
$ printf "%s" "${COMPANY//#Night/NIGHT}"
NIGHTLight Night Lighting Inc.
```

如果未指定新值，则匹配的字符串将被删除。

```
$ COMPANY="Nightlight Inc."
$ printf "%s\n" "${COMPANY/light}"
Nigh Inc.
```

也可以使用范围。例如，要删除字符串中的所有标点符号，使用范围 [:punct:]。

```
$ printf "%s" "${COMPANY//[[:punct:]]}"
NightLight Inc
```

使用星号或@符号代替变量时，替换将应用于 shell 脚本的所有参数。同样，带有星号或@符号的数组将替换应用于数组中的所有元素。

## 命令结果替换（$( )）

当使用括号时，括号内的命令会被执行。这与用反引号括起命令具有相同的效果。

```
$ printf "There are %d files in this directory\n" "$(ls -l | wc -l)"
There are 28 files in this directory
$ printf "There are %d files in this directory\n" `ls -l | wc -l`
There are 28 files in this directory
```

## 算术表达式替换（(( ... ))）

当使用两对括号时，括号内的算术表达式会被求值，并返回结果。其格式与 `((...))` 形式的 let 命令的简写形式相同，区别在于表达式的结果会被替换到命令中。

```
$ ORDERS=50
$ COST=25
$ printf "There are $((3 worth of orders in this directory\n" "$((ORDERS*COST))"
There are $1250 worth of orders in this directory
```

## 其他测试表达式

test 命令的 `-o (option)` 选项用于确定是否设置了特定的 shell 选项。

```
if [ -o noglob ] ; then
    printf "Globbing is off\n"
fi
```

Bash 中有许多类型的表达式，每种都有其独特的语法和操作顺序。用斯基尔顿教授的话来说，“你是否已经学到了这么多，以至于开始忘记那些你不经常使用的语法的语法了？”下一章要简单得多。

## mixer.bash：HTML 颜色混合器

mixer.bash，如列表 6.3 所示，是一个计算网页中使用的 HTML 十六进制颜色代码的脚本。它使用了本章讨论的许多概念，包括 test 命令、美元符号替换和 let 命令。

- 列表 6.3 mixer.bash

```
#!/bin/bash
#
# mixer.bash: HTML color mixer
#
```

### 列表 6.3 续

```
# Ken O. Burtch
# CVS: $Header$

shopt -s o nounset

declare -rx SCRIPT=$(0##*/)
declare -i RED    # 颜色中红色的量
declare -i GREEN  # 颜色中绿色的量
declare -i BLUE   # 颜色中蓝色的量

# 标题

printf "%s\n" "This program mixes color values for Web pages"
printf "\n"

# 选择百分比或绝对值
# 如果未指定，默认值为 'p'

printf "%s\n" "Mix the color by (p)ercent or (a)bsolute amount?"
printf "%s\n" "The default is percentage."
read -p "Select p or a: " REPLY
REPLY=${REPLY,,}
printf "\n"

# 读取绝对值

if [ "$REPLY" = "a" ] ; then
    read -p "How much red (0..255)?" RED
    if [ $RED -gt 255 ] ; then
        printf "$SCRIPT: too much red\n" >&2
        exit 192
    fi
    if [ $RED -lt 0 ] ; then
        printf "$SCRIPT: too little red\n" >&2
        exit 192
    fi
    read -p "How much green (0..255)?" GREEN
    if [ $GREEN -gt 255 ] ; then
        printf "$SCRIPT: too much green\n" >&2
        exit 192
    fi
    if [ $GREEN -lt 0 ] ; then
        printf "$SCRIPT: too little green\n" >&2
        exit 192
    fi
    read -p "How much blue (0...255)?" BLUE
    if [ $BLUE -gt 255 ] ; then
        printf "$SCRIPT: too much blue\n" >&2
        exit 192
    fi
    if [ $BLUE -lt 0 ] ; then
        printf "$SCRIPT: too little blue\n" >&2
        exit 192
    fi
fi
```

```
# 读取百分比值并转换为绝对值

if [ "$REPLY" = "p" ] ; then
    read -p "How much red (0...100)?" RED
    if [ $RED -gt 100 ] ; then
        printf "$SCRIPT: too much red\n" >&2
        exit 192
    fi
    if [ $RED -lt 0 ] ; then
        printf "$SCRIPT: too little red\n" >&2
        exit 192
    fi
    read -p "How much green (0...100)?" GREEN
    if [ $GREEN -gt 100 ] ; then
        printf "$SCRIPT: too much green\n" >&2
        exit 192
    fi
    if [ $GREEN -lt 0 ] ; then
        printf "$SCRIPT: too little green\n" >&2
        exit 192
    fi
    read -p "How much blue (0...100)?" BLUE
    if [ $BLUE -gt 100 ] ; then
        printf "$SCRIPT: too much blue\n" >&2
        exit 192
    fi
    if [ $BLUE -lt 0 ] ; then
        printf "$SCRIPT: too little blue\n" >&2
        exit 192
    fi
    RED=$(255*RED/100)
    GREEN=$(255*GREEN/100)
    BLUE=$(255*BLUE/100)
fi
```

### 列表 6.3 续

```
# 显示结果

printf "HTML color code is #\x\x\x\n" "$RED" "$GREEN" "$BLUE"

exit 0
```

## 参考部分

### Test 命令开关

- -b *file*—如果文件是块设备文件，则为真
- -c *file*—如果文件是字符设备文件，则为真
- -d *file*—如果文件是目录，则为真
- -e *file*—如果文件存在，则为真
- *f1* -ef *f2*—（等效文件）如果文件 *f1* 是 *f2* 的硬链接，则为真
- *n1* -eq *n2*—（相等）如果 *n1* 等于 *n2*，则为真
- -f *file*—如果文件存在且是普通文件，则为真
- *n1* -ge *n2*—（大于或等于）如果 *n1* 大于或等于 *n2*，则为真
- *n1* -gt *n2*—（大于）如果 *n1* 大于 *n2*，则为真
- -g *file*—如果文件设置了 set-group-id 权限，则为真
- -G *file*—如果文件（实际）属于你的组，则为真
- -h *file*（或 -L *file*）—如果文件是符号链接，则为真
- -k *file*—如果文件设置了粘滞权限位，则为真
- *n1* -le *n2*—（小于或等于）如果 *n1* 小于或等于 *n2*，则为真
- *n1* -lt *n2*—（小于）如果 *n1* 小于 *n2*，则为真
- -n *s*（或仅 *s*）—（非空）如果字符串不为空，则为真
- -N *file*—如果文件有新内容（自上次读取以来），则为真
- *n1* -ne *n2*—（不相等）如果 *n1* 不等于 *n2*，则为真
- *f1* -nt *f2*—（较新）如果文件 *f1* 比 *f2* 新，则为真
- -O *file*—如果文件（实际）属于你，则为真
- *f1* -ot *f2*—（较旧）如果文件 *f1* 比 *f2* 旧，则为真
- -p *file*—如果文件是管道，则为真
- -r *file*—如果文件可读（由你的脚本），则为真
- -s *file*—如果文件存在且不为空，则为真
- -S *file*—如果文件是套接字，则为真
- -t *fd*—如果文件描述符在终端上打开，则为真
- -u *file*—如果文件设置了 set-user-id 权限，则为真
- -w *file*—如果文件可写（由你的脚本），则为真
- -x *file*—如果文件可执行（由你的脚本），则为真
- -z *s*—（零长度）如果字符串为空，则为真

### Test 命令字符串测试

- `s1 == s2`—如果字符串 `s1` 等于 `s2`，则为真
- `s1 != s2`—如果字符串 `s1` 不等于 `s2`，则为真
- `s1 < s2`—如果字符串 `s1` 小于 `s2`，则为真
- `s1 > s2`—如果字符串 `s1` 大于 `s2`，则为真

### 字符类

- `[alnum:]`—字母数字
- `[alpha:]`—字母
- `[ascii:]`—ASCII 字符
- `[blank:]`—空格或制表符
- `[ctrl:]`—控制字符
- `[digit:]`—十进制数字
- `[graph:]`—非空白字符
- `[lower:]`—小写字符
- `[print:]`—非控制字符
- `[punct:]`—标点符号字符
- `[space:]`—空白
- `[upper:]`—大写字符
- `[xdigit:]`—十六进制数字

### ASCII C 转义展开

- `\a`—警报（铃声）
- `\b`—退格
- `\e`—转义字符



- `\f` — 换页符
- `\n` — 换行符
- `\r` — 回车符
- `\t` — 水平制表符
- `\v` — 垂直制表符
- `\\` — 字面意义的反斜杠
- `\'` — 单引号
- `\nnn` — 字符的 ASCII 八进制值（最多三位数字）
- `\xnnn` — 字符的 ASCII 十六进制值（最多三位数字）

## 7 复合命令

**除了最简单的脚本，** 你很少想要执行所有命令。执行一组命令而忽略另一组命令，或者将一组命令重复执行几次，会非常有用。*复合命令* 是封装一组其他命令的命令。

为了提高可读性，封装的命令会被缩进，以明确其执行依赖于复合命令。我的一位主管曾抱怨我偶尔每行缩进的空格数比他所坚持的标准少一个空格。（我不得不把尺子抵在屏幕上查看是否属实。）我认为这是个次要问题，因为他转向另一位程序员指出，该程序在输入零时就会崩溃。

复合命令始终由两条括住内部命令的命令组成。结束命令通常是第一条命令名称的倒序拼写。听起来神秘的 **case** 命令实际上是复合命令 *case* 的结束命令。

### 命令状态码

每个 Linux 命令都返回一个 *状态码*（或退出状态），这是一个 0 到 255 之间的数字，指示命令遇到了什么问题。状态码为零表示最后一个命令成功运行。任何其它状态码都表示某种错误。

状态码包含在变量 `$?` 中

```
$ unzip no_file.zip
unzip:  cannot find no_file.zip, no_file.zip.zip or no_file.zip.ZIP.
$ printf "%d\n" " $?"
9
```

当 **unzip** 命令找不到要解压缩的文件时，返回的状态码为 9（表示错误）。

非正式的 Linux 惯例使用 127 及以下的代码作为 Linux 标准错误代码。在这种情况下，`ls` 返回了状态码 9，即 Linux 中“无效文件号”的错误代码。完整的 Linux 错误代码列表见附录 D，“错误代码”。

如果命令被信号中断，Bash 会返回状态码 128 加上信号编号。因此，用户定义的错误代码应在 191 以上，且不应与 Bash 为最后一个 Linux 信号（编号 63）返回的代码冲突。信号代码列表见附录 E，“信号”。

```
if test ! -x "$who" ; then
    printf "${SCRIPT}:${LINE#}o: the command $who is not available - \
          "aborting\n" >&2
    exit 192
fi
```

不幸的是，大多数 Linux 命令仅仅返回 1 或 0 来表示失败或成功。如果脚本在发生错误时立即停止，这通常就是所需的全部信息。特定的错误消息仍会显示在标准输出上。

```
$ ls po_1473.txt
po_1473.txt
$ printf '%d\n' $?
0

$ ls no_file
no_file not found
$ printf '%d\n' $?
1
```

状态码不同于第 6 章“逻辑表达式”部分中讨论的由 `let` 命令返回的真值。在 `let` 中，`false`（比较失败）的值为 0。这遵循 C 等计算机语言的惯例。然而，状态码 0 表示成功，而不是失败。

```
$ let "RESULT=1>0"
$ printf '%d %d\n' "$RESULT" $?
1 0

$ test 1 -gt 0
$ printf '%d\n' $?
0
```

`let` 将 1 赋值给 RESULT，表示 1 大于 0。`test` 命令返回状态码 0，表示 1 大于 0。此外，`let` 命令本身的状态码为 0，表示 `let` 命令成功执行了比较。

这些相反的代码和惯例可能导致难以调试的错误。Bash 有两个内置命令，称为 `true` 和 `false`。这些命令返回的是状态码，而不是 `let` 的真值。

```
$ true
$ printf "%d\n" "$?"
0
$ false
$ printf "%d\n" "$?"
1
```

true 分配成功状态码（0）。false 分配错误状态码（1）。
感到困惑了吗？

如果你需要保存逻辑比较的成功结果，最好使用 test 命令以保持一致性。大多数 shell 命令期望的是状态码，而不是真值。

在管道中，可以同时运行几个命令。从管道返回的状态码是最后一个命令的状态码。在下面的示例中，状态码对应的是 wc 命令，而不是 ls。

```
$ ls badfile.txt | wc -l
ls: badfile.txt: No such file or directory
0
$ printf "%d\n" "$?"
0
```

尽管 ls 报告了错误，但管道的结果为零，因为 wc 成功计数了零行。

Bash 还定义了一个名为 PIPESTATUS 的数组，它包含最后一个管道中每个命令的单独状态码。

```
$ ls badfile.txt | wc -l
ls: badfile.txt: No such file or directory
0
$ printf "%d %d\n" "${PIPESTATUS[0]}" "${PIPESTATUS[1]}"
1 0
```

$? 基本上是 PIPESTATUS 最后一个值的别名。

命令或管道前可以加 ! 来否定状态码。如果状态为 0，它变为 1。如果状态大于 0，它变为 0。

### if 命令

if 命令根据其他命令返回的状态码，执行两个或更多替代命令系列中的一个。

通常，if 语句与 test 命令配合使用。

```
NUM_ORDERS=`ls -l | wc -l`
if [ "$NUM_ORDERS" -lt "$CUTOFF" ]; then
    printf "%s\n" "Too few orders...try running again later"
    exit 192
fi
```

这个示例统计以文件形式存储在目录中的客户订单数量。如果当前目录中的订单文件数量不足，脚本将执行 `then` 和 `fi` 关键字之间的语句，打印消息并停止脚本。

`then` 前的分号是必需的。虽然 `then` 实际上是一个独立的命令，但它与 `if` 配合使用。因为它们在同一行上，所以需要分号来分隔命令。

`if` 命令可以有一个 `else` 部分，该部分仅在条件失败时执行。

```
NUM_ORDERS=`ls -l | wc -l`
if [ "$NUM_ORDERS" -lt "$CUTOFF" ]; then
    printf "\n\n" "Too few orders...but will process them anyway"
else
    printf "\n\n" "Starting to process the orders"
fi
```

`if` 命令可以嵌套在其他 `if` 命令内部。

```
NUM_ORDERS=`ls -l | wc -l`
if [ [ "$NUM_ORDERS" -lt $TOOFEW ]]; then
    printf "\n\n" "Too few orders...but will process them anyway"
else
    if [ [ "$NUM_ORDERS" -gt $TOOMANY ]]; then
        printf "\n\n" "There are many orders.  Processing may take a long time"
    else
        printf "\n\n" "Starting to process the orders"
    fi
fi
```

命令不能交叉嵌套；内部 `if` 必须始终在外部 `if` 之前完成。

为了在一组替代项中选择，`if` 命令可以有一个 `elif` 部分。`elif` 是 `else if` 的简写，减少了不必要的 `if` 嵌套。`elif` 部分后面可以跟随一个最终的 `else` 部分，如果存在该部分，它仅在没有替代项时执行。结合这些想法，你可以将前面的示例重写如下。

```
NUM_ORDERS=`ls -l | wc -l`
if [ "$NUM_ORDERS" -lt "$TOOFEW" ]; then
    printf "\n\n" "Too few orders...but will process them anyway"
elif [ "$NUM_ORDERS" -gt "$TOOMANY" ]; then
    printf "\n\n" "There are many orders.  Processing may take a long time"
else
    printf "\n\n" "Starting to process the orders"
fi
```

`if` 命令不一定非要与 `test` 命令一起使用。它可以运行并测试任何命令的状态码。

```
if rm "STEMPFILE" ; then
    printf "%s\n" "SSCRIPT:temp file deleted"
else
    printf "%s - status code $d\n" \
    "SSCRIPT:$LINENO: unable to delete temp file" $2
fi
```

将复杂命令嵌入 if 命令中会使脚本难以阅读和调试；应避免这样做。在这种情况下，rm 命令不如它单独出现在一行上时那样突出。同样，可以在 if 命令内部声明变量，但这使得很难确定哪些变量存在，哪些不存在。

### case 命令

case 命令将变量与一系列值或模式进行比较。如果值或模式匹配，则执行相应的语句。之所以命名为 case，是因为变量是逐个（case-by-case）进行测试的。

与测试单个命令状态码的 elif 命令不同，case 测试变量的值。在测试字符串值时，case 命令优于冗长的 elif 组。

每个单独的 case 必须以一对分号结尾。如果没有分号，Bash 将尝试执行下一个 case 指定并报告错误。

```
printf "%s -> %s 1= delete, 2= archive. Please choose one"
read REPLY
case "$REPLY" in
    1) rm "STEMPFILE" ;;
    2) mv "STEMPFILE" "STEMPFILE.old" ;;
    *) printf "ss\n" "$REPLY was not one of the choices" ;;
esac
```

模式星号 (\*) 是全匹配 case；它匹配之前所有 case 未处理的所有值。虽然这个 case 是可选的，但始终包含一个全匹配 case 是良好的设计，即使它只包含一个空语句 (:)。

模式匹配规则遵循前一章讨论的文件通配规则。例如，垂直线可以分隔多个模式。

case 不会像某些计算机语言（尤其是 C）那样“贯穿执行”。当选择了一个 case 时，仅执行该 case 中的命令。后续 case 中的命令不会被执行。

### while 循环

有几个命令用于重复一组命令。

while 命令在所测试的命令成功时重复执行封装的命令。如果命令在第一次尝试时失败，则封装的命令永远不会被执行。



`while` 循环以 `done` 命令结束，而不是像你可能预期的那样使用 `elihw`。
可以使用 `true` 命令创建一个*无限*循环。因为 `true` 总是成功，所以循环将无限期地继续。

```bash
printf "%s\n" "Enter the names of companies or type quit"
while true ; do
    read -p "Company ?"  COMPANY
    if [ "$COMPANY" = "quit" ] ; then
        break
    elif test -f "orders_$COMPANY.txt" ; then
        printf "%s\n" "There is an order file from this company"
    else
        printf "%s\n" "There are no order files from this company"
    fi
done
```

`while` 循环可以通过 `break` 命令提前停止。当遇到 `break` 时，Bash 停止执行命令并“跳出”循环，开始执行循环*之后*的*第一个*命令。
`break` 后面可以跟一个数字，指示要跳出多少层嵌套循环。例如
`break 2` 会跳出当前循环以及包含当前循环的上一层循环。
`break` 的对应命令是 `continue`，它使被包含的语句的剩余部分被忽略；循环在顶部重新开始。`continue` 后面也可以跟一个数字，指示在继续之前要跳出多少层包含的语句。

## until 循环

`while` 循环的对应形式是 `until` 循环。`until` 命令与 `while` 命令相同，除了它重复执行被包含的语句，直到条件*成功*，本质上等同于 `while !`。

```bash
until test -f "$INVOICE_FILE" ; do
    printf "%s\n" "Waiting for the invoice file to arrive..."
    sleep 30
done
```

将 `until` 与 `false` 命令结合使用会创建一个无限循环。
`break` 和 `continue` 命令可用于 `until` 循环。

### for 循环

标准的 Bourne `for in 循环` 是 here file 的一种变体。`for` 命令将一系列值读入变量，并对每个值重复执行一次被包含的命令。

```bash
for FILE_PREFIX in order invoice purchase order; do
    if test -f "$FILE_PREFIX"_vendor1.txt" ; then
        printf "%%s\n" "There is a $FILE_PREFIX file from vendor l..."
    fi
done
```

如果缺少 `in` 部分，`for` 命令将为 shell 脚本的每个参数执行被包含的语句。

`break` 和 `continue` 命令可用于 `for` 循环。

由于其他 shell 特性的存在，这种 `for` 循环并不常用。

### 嵌入式 let( ( . . . ) )

`let` 命令在表达式为零时返回状态码 1，如果表达式值为非零则返回 0。正如 `test` 命令可以用一对方括号表示以便在复合语句中更容易阅读一样，`let` 命令也有一个更容易阅读的形式：双括号。

其他编程语言中常见的 `for` 循环，是通过嵌入式 `let` 创建的，如清单 7.1 所示。

**清单 7.1 forloop.sh**

```bash
#!/bin/bash
# forloop.sh: Count from 1 to 9
for (( COUNTER=1; COUNTER<10; COUNTER++ )) ; do
    printf "The counter is now %d\n" $COUNTER
done
exit 0
```

双括号中的第一个表达式在循环开始时执行。每次循环重新开始，执行第三个表达式，并检查第二个表达式。当第二个表达式返回 `false` 时，循环结束。

```bash
$ bash forloop.sh
The counter is now 1
The counter is now 2
The counter is now 3
The counter is now 4
The counter is now 5
The counter is now 6
The counter is now 7
The counter is now 8
The counter is now 9
```

### 命令分组 ( {...} )

可以使用花括号 ( {...} ) 将命令分组在一起。

```bash
ls -1 | {
    while read FILE ; do
        echo "$FILE"
    done
}
```

在这个例子中，`ls` 命令的结果成为组内所有语句的输入。

```bash
$ test -f orders.txt && { ls -l orders.txt ; rm orders.txt; } \
    || printf "no such file"
```

如果文件 `orders.txt` 存在，该文件将被列出并删除；否则，将打印 “no such file”。只有当花括号在同一行上时，最后一个花括号命令后面的分号才是必需的。

也可以使用子 shell 对命令进行分组。子 shell 在第 9 章“参数和子 shell”中描述。

### report.bash: 报表格式化程序

report.bash 是一个读取销售数字列表并创建简单报表的脚本。销售数字文件包含产品名称、本地国家销售额和外国国家销售额。例如，report.bash 将此转换：

```text
binders 1024 576
pencils 472 235
rules 311 797
stencils 846 621
```

为以下报表：

```text
Report created on Thu Aug 22 18:27:07 EDT 2002 by kbutrch

Sales Report
```

| 产品 | 国家 | 外国 | 总计 | 平均 |
|:----------|--------:|--------:|------:|--------:|
| binders | 1024| 576| 1600| 800|
| pencils | 472| 235| 707| 353|
| rules | 311| 797| 1108| 554|
| stencils | 846| 621| 1467| 733|

产品总数：4

报表结束

### 清单 7.2 report.bash

```bash
#!/bin/bash
#
# report.bash: simple report formatter
#
# Ken O. Burtch
# CVS: $header$
#
# The report is read from DATA_FILE. It should contain
# the following columns:
#
# Column 1: PRODUCT = Product name
# Column 2: CSALES = Country Sales
# Column 3: PSALES = Foreign Sales
#
# The script will format the data into columns, adding total and
# average sales per item as well as a item count at the end of the
# report.

# Some Linux systems use USER instead of LOGNAME
if [ -z "$LOGNAME" ] ; then # No login name?
declare -rx LOGNAME="$USER" # probably in USER
fi
shopt -s -o nounset

# Global Declarations

declare -rx SCRIPT=$0###/ # SCRIPT is the name of this script
declare -rx DATA_FILE="report.txt" # this is raw data for the report
declare -i ITEMS=0 # number of report items
declare -i LINE_TOTAL=0 # line totals
declare -i LINE_AVG=0 # line average
```

**清单 7.2 续**

```bash
declare PRODUCT        # product name from data file
declare -i CSALES         # country sales from data file
declare -i FSALES          # foreign sales from data file
declare -rx REPORT_NAME="Sales Report" # report title
# Sanity Checks

if test ! -r "$DATA_FILE" ; then
       printf "$SCRIPT: the report file is missing-aborting\n" >&2
       exit 192
fi

# Generate the report

printf "Report created on %s by %s\n" "$DATE" "$LOGNAME"
printf "\n"
printf "%s\n" "$REPORT_NAME"
printf "\n"
printf "%-12s12s12s12s12s\n" "Product" "Country" "Foreign" "Total" "Average"
printf "%-12s12s12s12s12s\n" "___" "___" "___" "___" "___"

{ while read PRODUCT CSALES FSALES ; do
      let "ITEMS+=1"
      LINE_TOTAL=$(CSALES+FSALES)
      LINE_AVG=$((CSALES+FSALES)/2)
      printf "%-12s12d12d12d12d\n" "$PRODUCT" "$CSALES" "$FSALES" \
      "$LINE_TOTAL" "$LINE_AVG"
done } < $DATA_FILE
# Print report trailer

printf "%-12s12s12s12s12s\n" "___" "___" "___" "___" "___"
printf "Total number of products: %d\n" "$ITEMS"
printf "\n"
printf "End of report\n"

exit 0
```

# 8 调试和版本控制

当我在布鲁克大学（Brock University）时，麦克夸里实验室里塞满了从已经不再使用它们的教授那里传下来的二手 Macintosh Plus 计算机。有一天，我正在为我的三年级操作系统课程编写一个程序。我当时正在处理的一个简短的 C 程序被报告为没有错误。当我运行它时，单色桌面上出现了垂直条，我的软盘弹出，计算机重启了。仔细观察后，我注意到我在一个 `if` 语句中使用了 `!=` 而不是 `==`。那个小错误造成了不可预见的结果。从那时起，我将 C 语言视为一个精神不稳定的室友；我们可能一起生活和工作，但我永远不放松警惕，以免它试图在背后捅我一刀。

不幸的是，shell 脚本几乎和 C 程序一样难以调试。与 C 语言类似，shell 命令通常假设你知道自己在做什么，并且只在有问题的行实际运行时才发出错误。除非对 shell 脚本进行彻底测试，否则错误可能潜伏数月甚至数年，直到有故障的命令最终被执行。扎实的 shell 调试工具知识对于专业脚本开发至关重要。

### Shell 调试特性

有几个有用的 Bash 开关和选项可用于追踪脚本中的问题。

`-n`（*不执行*）开关检查脚本的语法错误，而不运行它。在开发期间使用此开关来检查脚本。

```bash
$ bash -n bad.sh
bad.sh: line 3: syntax error near unexpected token `fi`
bad.sh: line 3: `fi'
```

在这个例子中，脚本的第 3 行或之前有错误。术语*token*（标记）指的是源错误附近的关键词或另一段文本。

`-o errxit` 选项在命令返回错误代码时终止 shell 脚本。例外情况是循环，因此如果命令不能返回非零状态，`if` 命令无法正常工作。仅在没有其他错误处理的最简单脚本上使用此选项；例如，如果子 shell 中发生错误，它不会终止脚本。




`-O nounset` 选项会在引用未设置（或不存在）的变量时终止并报告错误。此选项用于报告拼写错误的变量名。`nounset` 并不保证能识别出所有的拼写错误（见清单 8.1）。

## 清单 8.1 nounset.bash

```bash
#!/bin/bash
#
# A simple script to list files

shopt -O -s nounset
declare -i TOTAL=0

let "TOTAL=TOTAL+1"      # not caught
printf "%s\n" "$TOTAL"

if [ $TOTAL -eq 0 ] ; then  # caught
   printf "TOTAL is %s\n" "$TOTAL"
fi
```

`-O xtrace` 选项会在执行每条命令前显示该命令。该命令中的所有替换和扩展均已完成。

```bash
declare -i TOTAL=0
if [ $TOTAL -eq 0 ] ; then
   printf "%s\n" "$TOTAL is zero"
fi
```

如果此脚本片段在 `xtrace` 选项下运行，您应该看到类似以下结果：

```text
+ alias 'rm=rm -i'
+ alias 'cp=cp -i'
+ alias 'mv=mv -i'
+ '\. /etc/bashrc \'
+ . /etc/bashrc
+++ id -gn
+++ id -u
++ '[' root = root -a 0 -gt 99 ']'
++ umask 022
++ '[' '' ']'
+ declare -i TOTAL=0
+ '[' 0 -eq 0 ']'
+ printf '%s\n' '0 is zero'
0 is zero
```

前 11 行是 Linux 发行版配置文件脚本中执行的命令。加号的数量表示脚本嵌套的层级。最后四行是 Bash 完成所有替换和扩展后的脚本片段。请注意，复合命令（如 `if` 命令）被省略了（见清单 8.2）。

## 清单 8.2 bad.bash

```bash
#!/bin/bash
#
# bad.bash: A simple script to list files

shopt -o -s nounset
shopt -o -s xtrace

declare -i RESULT
declare -i TOTAL=3

while [ $TOTAL -ge 0 ] ; do
    let "TOTAL--"
    let "RESULT=10/TOTAL"
    printf "$d\n" "$RESULT"
done
```

`xtrace` 展示了脚本逐行的执行进度。在这种情况下，脚本包含一个错误，导致 `while` 循环多执行了一次。使用 `xtrace`，您可以检查变量并发现应将 `-ge` 替换为 `-gt`，以防止在 TOTAL 为零时出现无限循环。

```text
$ bash bad.bash
+ declare -i RESULT
+ declare -i TOTAL=3
+ '[' 3 -ge 0 ']'
+ let TOTAL--
+ let RESULT=10/TOTAL
+ printf '$d\n' 5
5
+ '[' 2 -ge 0 ']'
+ let TOTAL--
+ let RESULT=10/TOTAL
+ printf '$d\n' 10
10
+ '[' 1 -ge 0 ']'
+ let TOTAL--
+ let RESULT=10/TOTAL
bad.sh: let: RESULT=10/TOTAL: division by 0 (error token is "lr")
+ printf '$d\n' 10
10
+ '[' 0 -ge 0 ']'
+ let TOTAL=0
+ let RESULT=10/TOTAL
+ printf '%d\n' -10
-10
+ '[' -1 -ge 0 ']'
```

您可以通过为 `PS4` 变量赋值来更改跟踪加号提示。将提示设置为包含变量 `LINENO` 将显示脚本或 shell 函数中的当前行。在脚本中，`LINENO` 显示脚本的当前行号，从第一行的 1 开始。当在 shell 提示符下与 shell 函数一起使用时，`LINENO` 从函数的第一行开始计数。

## 调试陷阱

内置的 `trap` 命令（在第 10 章“作业控制与信号”中有更详细的讨论）可用于在 Bash 处理完每一行后执行调试命令。通常，调试陷阱与跟踪结合使用，以提供跟踪中未列出的额外信息。

当调试陷阱与跟踪结合时，调试陷阱本身在执行时也会列在跟踪中。这使得使用 `printf` 变得有些冗余，因为命令在执行 `printf` 之前已经显示出了所有变量替换完成后的状态。相反，使用空命令 `:` 可以在不执行任何 shell 命令的情况下显示变量（见清单 8.3）。

## 清单 8.3 debug_demo.sh

```bash
#!/bin/bash
#
# debug_demo.sh : an example of a debug trap

trap ': CNT is now $CNT' DEBUG

declare -i CNT=0

while [ $CNT -lt 3 ] ; do
    CNT=CNT+1
done
```

在启用跟踪运行时，CNT 的值会在每一行之后显示。

```text
+ '[ 0 -lt 3 '
++ : CNT is now 0
+ CNT=CNT+1
++ : CNT is now 1
+ '[ 1 -lt 3 '
++ : CNT is now 1
+ CNT=CNT+1
++ : CNT is now 2
+ '[ 2 -lt 3 '
++ : CNT is now 2
+ CNT=CNT+1
++ : CNT is now 3
+ '[ 3 -lt 3 '
++ : CNT is now 3
```

### 版本控制 (CVS)

在商业环境中，金钱和职业生涯都受到威胁，创建一个无瑕疵的程序是不够的。总有一些最后时刻的更改会导致程序产生错误结果甚至崩溃。当这种情况发生时，需要尽快撤销或修正这些更改，且不能丢失数据。

*版本控制系统*是一种维护数据文件、脚本和源程序主副本的程序。这个主副本存储在一个称为*存储库*的目录中。每次添加或修改程序时，都会将其重新提交到存储库，并记录哪些更改被做出、谁做出的以及何时做出。

*CVS* (*Concurrent Versions System*) 是大多数 Linux 发行版提供的版本控制软件。它基于一个名为 RCS (*Revision Control System*) 的旧程序，CVS 可以在多个程序员之间共享脚本并记录任何更改。它可以处理单个文件、整个目录或大型项目。这些文件可以组织成称为*模块*的文件组。CVS 为文件添加时间戳，维护版本号，并在两个程序员同时更新程序的同一部分时识别潜在问题。

CVS 在开源开发中也非常流行。它可以配置为允许世界各地的程序员共同参与项目开发。

要使用 CVS，项目负责人或团队领导必须创建一个目录作为版本控制存储库，以及一个名为 *CVSROOT* 的子目录。然后您定义一个名为 *CVSROOT* 的环境变量，以便 CVS 知道在哪里找到存储库目录。例如，要将 /home/repository 设置为您团队的存储库，请在 Bash 中如下设置 *CVSROOT*：

```bash
$ declare -rx CVSROOT=/home/repository
```

存储库保存项目中所有文件的副本、更改日志以及其他共享资源。

添加到存储库的软件没有特殊要求。然而，当程序被添加或更新时，CVS 会读取文件以查找特殊字符串。如果存在这些字符串，CVS 会用关于该程序副本的最新信息替换这些字符串。CVS 文档将这些字符串称为*关键字*，尽管它们在 Bash 意义上不是关键字。

- `$Author$`—签入该修订版本的用户的登录名。
- `$Date$`—修订版本签入的日期和时间（UTC）。
- `$Header$`—一个标准头部，包含 RCS 文件的完整路径名、修订号、日期（UTC）、作者等。
- `$Id$`—与 `$Header$` 相同，只是 RCS 文件名不包含路径。
- `$Name$`—如果使用标签，这是签出此文件时使用的标签名。
- `$Locker$`—锁定该修订版本的用户的登录名（如果未锁定则为空，这是正常情况，除非使用 *cvs admin -l*）。
- `$Log$`—提交期间提供的日志消息，前面有一个包含 RCS 文件名、修订号、作者和日期（UTC）的头部。现有的日志消息不会被替换。相反，新的日志消息插入在 *$Log$* 之后。
- `$RCSfile$`—不带路径的 CVS 文件名。
- `$Revision$`—分配给该修订版本的修订号。
- `$Source$`—CVS 文件的完整路径名。
- `$State$`—分配给该修订版本的状态。

CVS 关键字可以添加到脚本的任何位置，但如果不在注释中，它们应该出现在注释或引号字符串中。这样可以防止关键字被当作可执行的 shell 命令处理。

```bash
# CVS: $Header$
```

当脚本添加到存储库时，CVS 会填充头部信息。

```bash
# CVS: $Header: /home/repository/scripts/t.sh,v 1.1 2001/03/26 
20:35:27 kburch Exp $
```

CVS 关键字头部应放置在脚本的头部。

```bash
#!/bin/bash
#
# flush.sh: Flush disks if nobody is on the computer
#
# Ken O. Burch
# CVS: $Header$
```

CVS 使用 Linux 的 *cvs* 命令进行控制。*cvs* 后面总是跟随一个 CVS 命令词以及该命令的任何参数。





# 创建转录记录

若要向 CVS 仓库添加新的项目目录，请使用 **import** 命令。**Import** 将当前目录的文件以指定名称放入仓库中。**Import** 还要求提供一个短字符串来标识谁添加了该项目，以及一个描述项目状态的字符串。这些字符串本质上就是注释，可以是任何内容：使用你的登录名和表示初始版本的 **init-rel** 是不错的选择。

```
$ cvs import scripts kburcht init-rel
```

CVS 会根据环境变量 **EDITOR** 或 **CVSEDITOR** 启动你的默认文本编辑器。CVS 不识别 **VISUAL** 变量。待编辑的文件包含以 **CVS:** 开头标记的注释行：

```
CVS:  
CVS: Enter Log. Lines beginning with `CVS:' are removed automatically  
CVS:  
CVS:
```

编辑完成后，CVS 会将你的程序添加到仓库中，并将你的注释记录在变更日志中。结果会输出到屏幕上。

```
N scripts/ftp.sh
No conflicts created by this import
```

带有 N 的 **scripts/ftp.sh** 行表示 CVS 创建了一个名为 **scripts** 的新项目，并将 Bash 脚本 **ftp.sh** 添加到其中。**ftp.sh** 现在存储在 CVS 仓库中，随时可以与开发团队成员共享。此时可以安全地删除你目录中的项目目录了。实际上，在继续对该项目的工作之前，必须删除该目录。

使用 CVS 命令 **checkout**（或 **co**）来对项目进行操作。此 CVS 命令会将项目的一份副本保存在当前目录中。它还会创建一个 CVS 目录，用于保存 CVS 使用的私有数据文件。

要使用 **checkout**，请移动到主目录并输入：

```
$ cvs checkout scripts
cvs checkout: Updating .
U scripts/ftp.sh
```

名为 **scripts** 的子目录包含从仓库中获取的项目文件个人副本。CVS 维护 **ftp.sh** 的原始副本。在你操作个人副本的同时，其他程序员也可以对 **ftp.sh** 执行 **checkout** 操作。

若要向项目目录添加新文件或目录，请使用 **add** 命令。若要添加名为 **process_orders.sh** 的文件，请使用以下命令：

```
$ cvs add process_orders.sh
```

在编写脚本时，请定期使用 **update** 命令将你的工作成果与仓库进行对比。如果其他程序员对脚本进行了修改，CVS 会更新你的项目目录以反映这些脚本更改。然而，你自己所做的更改尚未添加到仓库副本中。

```
$ cvs update
cvs update: Updating .
```

有时更改涉及脚本的相同部分，CVS 无法自动合并这些更改。CVS 将这种情况称为冲突，并在更新时用一个 c 进行标记。CVS 会标记发生冲突的位置；你必须自己编辑脚本来解决冲突。

如果在更新后没有其他问题，你可以继续编写源代码。

若要删除已存在于仓库中的脚本，请使用 `rm` 命令移除它，并执行一次 `CVS` 更新。`CVS` 将会删除该文件。

在编写源代码时，直到你准备好之前，更改不会分发给团队的其他成员。当脚本测试完毕且你准备将其发布时，使用 `commit`（或 `ci`，即 *check in* 的缩写）。在提交更改之前，请删除非必要的文件（如临时文件），以节省仓库空间。

```
$ cvs commit
```

与 `import` 类似，`CVS commit` 命令会启动你的编辑器，并提示你输入对所作更改的描述。

`CVS commit` 还会自动增加你所修改脚本的版本号。按照惯例，`CVS` 以 `1.1` 开始对项目的编号。若要启动新版本 `2.1`，请编辑 `#header` 行中的版本号（或脚本中的任何其他 `CVS` 关键字），并将数字更改为 `2.0`。`CVS` 会将脚本保存为版本 `2.1`。

在任何时候，你都可以检索某个脚本或整个项目的日志。`CVS log` 命令会显示所有相关的日志条目、脚本和版本号：

```
$ cvs log project
cvs log: Logging project
RCS file: /home/repository/scripts/ftp.sh,v
Working file: scripts/ftp.sh
head: 1.1
branch: 1.1.1
locker: atrict
access: liat:
symbolic names:
keyword substitution: kv
total revisions: 2; selected revisions: 2
description:
revision 1.1
date: 1999/01/13 17:27:33; author: kburcht; state: Exp;
branches: 1.1.1;
Initial revision
revision 1.1.1.1
date: 1999/01/13 17:27:33; author: kburtch; state: Exp; lines: +0 -0
Project started
=====================================================================
```

status 命令可以为你提供项目目录的概览，以及尚未提交到仓库的脚本列表。

```
$ cvs status scripts
cvs status: Examining scripts
=====================================================================
File: ftp.sh Status: Up-to-date
Working revision: 1.1.1.1 Wed Jan 13 17:27:33 1999
Repository revision: 1.1.1.1 /home/repository/scripts/ftp.sh,v
Sticky Tag: (none)
Sticky Date: (none)
Sticky Options: (none)
```

CVS 还有许多其他未在此处讨论的专业功能。请查阅 CVS 的手册页以获取更多信息。

可以使用 `tee` 命令将命令的输出保存到文件中。该名称象征着一根在 T 型接头处分成两股的管道：输出的副本被存储在一个文件中，而不会重定向原始标准输出。若要同时捕获标准输出和标准错误，请在将结果管道传输到 tee 之前，将标准错误重定向到标准输出。

```
$ bash buggy_script.sh >& | tee results.txt
```

tee 的 -append（-a）开关会将输出追加到现有文件的末尾。-ignore-interrupts（-i）开关确保即使 tee 被 Linux 信号中断，它仍会继续运行。

此技术不会复制在标准输入中键入的内容。若要获取脚本运行的完整记录，Linux 提供了一个 script 命令。当 shell 脚本在 script 下运行时，会在当前目录创建一个名为 typescript 的文件。typescript 文件是一个文本文件，记录在 shell 会话中出现的所有内容列表。

你可以使用 `exit` 命令停止记录过程。

```
$ script
Script started, file is typescript
$ bash buggy_script.sh
...
$ exit
exit
Script done, file is typescript
```

# 监视运行中的脚本

若要在未将 cron 脚本安装到 `cron` 下进行测试，请使用 `watch` 命令。`watch` 会定期 `重新运行` 命令并在屏幕上显示结果。`watch` 每两秒运行一次命令，但你可以通过 `--interval=`（或 `-n`）开关指定不同的秒数。你可以过滤结果，以便仅显示差异（`--differences` 或 `-d`），或者显示迄今为止的所有差异（`--differences=cumulative`）。

## 使用 Time 计时执行

有两个可用于对程序或脚本进行计时的命令。

`Bash` 内置命令 `time` 告诉你程序运行所花费的时间。你还可以使用 `time` 对一系列管道命令进行计时。除了实际使用的时间外，`time` 返回的统计数据是指脚本使用的系统资源，而不是脚本运行的任何命令。

结果格式根据 `TIMEFORMAT` 变量的值进行设置。`TIMEFORMAT` 的布局类似于 `date` 命令的格式化字符串，它使用一组 `%` 格式代码。

- `%%` — 一个字面量 `%`。
- `%[precision][I]R` — 实际时间；以秒为单位的经过时间。
- `%[precision][I]U` — 用户模式下消耗的 `CPU` 秒数。
- `%[precision][I]S` — 系统模式下消耗的 `CPU` 秒数。
- `%P` — `CPU` 百分比，计算方式为 `($U + $S) / $R`。

`precision` 指示要显示的小数位数，默认为 `3`。字符 `I`（`ion`）打印的值是以分钟和秒为单位的。如果没有 `TIMEFORMAT` 变量，`Bash` 将使用 `\nreal \t%3R\nuser \t%3U\nsys \t%3S`。

```
$ unset TIMEFORMAT
$ time ls > /dev/null
real    0m0.018s
user    0m0.010s
sys     0m0.010s
```

```
$ declare -x TIMEFORMAT="%P"
$ time ls > /dev/null
75.34
```

```
$ declare -x TIMEFORMAT="The real time is %lR"
$ time ls > /dev/null
The real time is 0m0.023s
```

请注意，由于计算机上运行的其他程序的影响，每次运行的时间可能会有细微差异。为了获得最准确的时间，请多次测试脚本并取最低值。





## Linux 也有一个 time 命令

这种变体无法对管道进行计时，但它会显示额外的统计数据。要使用它，请使用 command 命令来覆盖 Bash 的 time。

```bash
$ command time myprog
3.09user 0.95system 0:05.84elapsed 69%CPU(0avgtext+0avgdata 0maxresident)k
0inputs+0outputs(4786major+4235minor)pagefaults 0swaps
```

与 Bash time 一样，Linux time 也可以对结果进行格式化。格式可以存储在一个名为 TIME（而不是 TIMEFORMAT）的变量中，或者可以通过 -format (-f) 开关明确指定。

-   $A—字面量 $。
-   $E—实际时间；以“小时:分钟:秒”格式显示的经过时间。
-   $e—实际时间；以秒为单位的经过时间。
-   $S—以 CPU 秒为单位的系统时间。
-   $U—以 CPU 秒为单位的用户时间。
-   $P—程序使用的 CPU 百分比。
-   $M—程序在内存中的最大大小（以千字节为单位）。
-   $t—程序的平均常驻集大小（以千字节为单位）。
-   $D—非共享数据区的平均大小。
-   $P—非共享堆栈的平均大小（以千字节为单位）。
-   $X—共享文本区的平均大小。
-   $Z—系统页的大小，以字节为单位。
-   $F—主要缺页错误的数量。
-   $R—次要缺页错误的数量（即页面之前已加载且仍被 Linux 缓存的情况）。
-   $W—进程被换出的次数。
-   $c—时间片上下文切换的次数。
-   $w—自愿上下文切换的次数。
-   $I—文件系统输入的次数。
-   $O—文件系统输出的次数。
-   $r—接收套接字消息的次数。
-   $s—发送套接字消息的次数。
-   $K—接收到的信号数量。
-   $C—命令行。
-   $x—退出状态。

与您的硬件无关的统计数据显示为零。

```bash
$ command time grep ken /etc/aliases
Command exited with non-zero status 1
0.00user  0.00system  0:00.02elapsed  0%CPU  (0avgtext+0avgdata 0maxresident)k
0inputs+0outputs (142major+19minor)pagefaults 0swaps
$ command time --format "%P" grep ken /etc/aliases
Command exited with non-zero status 1
0%
$ command time --format "Major faults = %W" grep ken /etc/aliases
Command exited with non-zero status 1
Major faults = 141
```

`--portability` (-p) 开关强制 time 遵循 POSIX 标准，这与 Bash 的 `time -p` 相同，并关闭了许多扩展功能。

```bash
$ command time --portability grep ken /etc/aliases
Command exited with non-zero status 1
real  0.00
user  0.00
sys  0.00
```

结果可以通过 `--output` (-o) 重定向到文件，或者通过 `--append` (-a) 追加到文件。`--verbose` (-v) 选项会提供每个统计项的详细解释。

## 创建 Man 手册页

Linux 的 man 手册页是为 groff 程序（GNU run off）格式化的特殊文本文件。groff 基于较旧的 Unix 程序 troff（用于打印机）和 nroff（用于终端）。Troff 最初由 Joseph E. Ossanna 在 1973 年创建。通过为重要脚本创建简短的 man 手册页，可以为关于您项目的在线信息创建一个单一的访问点。

请将您自己项目的手册页放在手册的第 9 节中。最初，第 9 节用于记录 Linux 内核，但现在它遵循传统的 Unix 解释，允许个人使用。第 9 节的手册页通常存储在 /usr/share/man/man9 中。如果您无法访问此目录，请在主目录中创建一个 man9 目录，并将您的个人手册页存储在那里。通过在 Bash 配置文件中将 $HOME 添加到 MANPATH 环境变量中，man 将搜索存储在您 man9 目录中的页面。

```bash
$ mkdir ~/man9
$ declare -x MANPATH="$HOME:/usr/share/man"
```

man 手册页是包含嵌入文本中的 groff 标记代码（或宏）的文本文件。这些代码很像网页中的 HTML 标签，控制页面中使用的间距、布局和图形。您还可以定义自己的 groff 代码。这些代码总是出现在行首，并以句号开头。

以下是一些 groff 标记代码的示例：

```groff
.\$Id
.TH MAN 9 "25 July 1993" "Linux" "Nightlight Corporation Manual"
.SH NAME
ftp.sh \- script to FTP orders to suppliers
.SH SYNOPSIS
.B ftp.sh
.I file
```

groff 代码以单独的行开始，以句号 (.) 开头，后跟一个或两个字母的代码。例如，.B 代码表示随后的文本是粗体（类似于 HTML 的 <b> 标签）。

与手册页相关的 groff 预定义宏在第 7 节的手册页 man（man 7 man）中有记录。一些常用的 groff 代码如下：

-   .B—粗体
-   .I—斜体
-   .PP—开始新段落
-   .RS i—缩进 i 个字符
-   .RE—结束上一个 RS 缩进
-   .UR u—开始由 URL 链接的文本
-   .UE—结束由 .UR 开始的链接文本
-   .\—表示注释
-   .TH—页面标题
-   .SH—子标题

虽然对手册页没有严格的要求，但大多数 man 手册页包含以下一个或多个部分：SYNOPSIS（概要）、DESCRIPTION（描述）、RETURN VALUES（返回值）、EXIT STATUS（退出状态）、OPTIONS（选项）、USAGE（用法）、FILES（文件）、ENVIRONMENT（环境）、DIAGNOSTICS（诊断）、SECURITY（安全性）、CONFORMING TO（符合性）、NOTES（备注）、BUGS（缺陷）、AUTHOR（作者）和 SEE ALSO（另请参阅）。如果您正在使用 CVS，您可以在 VERSION（版本）部分中包含 CVS 关键字，例如 $Id$。

为您的程序创建简单 man 手册页的最简单方法是找到一个类似的手册页并制作一个修改后的副本。

列表 8.4 展示了一个简短且完整的 man 手册页示例。

### 列表 8.4 Man 手册页示例

```groff
./'man page supply_ftp.sh.9
.TH "SUPPLY_FTP.SH" 9 "25 May 2001" "Nightlight" "Nightlight Corporation Manual"
.SH NAME
supply_ftp.sh \- Bash script to FTP orders to suppliers
.SH SYNOPSIS
.B supply_ftp.sh
.I file
.I supplier
.SH DESCRIPTION
.B supply_ftp.sh
sends orders via FTP to suppliers.
.I file
is the name of the file to send.
.I supplier
is the name of the supplier. The suppliers and their FTP account information
are stored in the text file
.I supplier.txt
.SH RETURN VALUES
The script returns 0 on a successful FTP and 1 if the FTP failed.
.SH AUTHOR
Created by Ken O. Burtch.
.SH FILES
/home/data/supplier.txt
.SH VERSION
$Id$
```

此页面显示为

```text
SUPPLY_FTP.SH(9)   Nightlight Corporation Manual  SUPPLY_FTP.SH(9)

NAME
     supply_ftp.sh - Bash script to FTP orders to suppliers

SYNOPSIS
     supply_ftp.sh file supplier

DESCRIPTION
     supply_ftp.sh sends orders via FTP to suppliers. file is the
     name of the file to send. supplier is the name of the supplier.
     The suppliers and their FTP account information are stored in
     the text file supplier.txt

RETURN VALUES
     The script returns 0 on a successful FTP and 1 if the FTP failed.

AUTHOR
     Created by Ken O. Burtch.

FILES
```

## 源代码补丁

Linux *diff* 命令列出两个或多个文件之间的更改。

当使用正确的开关时，diff 创建一个 *patch file*（补丁文件），其中包含将一组文件升级到另一组文件所需的更改列表。

```bash
$ diff -u -recursive -new-file older_directory newer_directory > update.diff
```

例如，假设您有一个脚本用于统计当前目录中的文件数量，如列表 8.5 所示。

### 列表 8.5 *file_count.bash*

```bash
#!/bin/bash

#
# file_count: count the number of files in the current directory.
# There are no parameters for this script.

shopt -s -o nounset

declare -rx SCRIPT=$0
declare -rx ls="/bin/ls" # ls command
declare -rx wc="/usr/bin/wc" # wc command

# Sanity checks

if test -z "$BASH" ; then
    printf "Please run this script with the BASH shell\n" >&2
    exit 192
fi

if test ! -x "$ls" ; then
    printf "${SCRIPT}:$LINENO: the command $ls is not available - aborting\n" >&2
    exit 192
fi

if test ! -x "$wc" ; then
    printf "${SCRIPT}:$LINENO: the command $wc is not available - aborting\n" >&2
    exit 192
fi

ls -l | wc -l

exit 0
```

您决定脚本使用 `exit $?` 而不是 `exit 0` 更好。这段代码

```bash
$ diff -u -recursive -new-file older.sh newer.sh > file_count.diff
```

创建包含以下内容的补丁文件

```diff
@@ -26,5 +26,5 @@
 ls -l | wc -l
 -exit 0
 +exit $?
```

- 表示将删除 `exit 0` 行。+ 表示将插入 `exit $?`。然后旧脚本将被升级为新脚本。

Linux 的 patch 命令应用由 `diff` 创建的补丁文件。使用 `-p1` 和 `-s` 开关。

```bash
$ cd older_directory
$ patch -p1 -s < update.diff
```

在 file_count 脚本示例中，由于补丁是针对单个文件创建的，而不是针对目录创建的，因此 patch 会要求输入要修补的旧文件名。

```bash
$ patch -p1 -s < file_count.diff
The text leading up to this was:
--- older.sh  Tue Feb 26 10:52:55 2002
+++ newer.sh  Tue Feb 26 10:53:56 2002
---
File to patch: older.sh
```

文件 `older.sh` 现在与 `newer.sh` 相同。




## Shell 归档

*Shell 归档*（或 *shar 文件*）是一组编码为单个 shell 脚本的文本文件或脚本。脚本中的数据在此以文件形式表示。二进制文件会通过 Linux 的 uuencode 命令转换为文本。Shell 归档是自解压的归档；当 shell 脚本执行时，归档中的文件会被解压。

Linux shar (*shell archive*) 命令是一个用于创建新 shell 归档的工具。要将名为 orders.txt 的文件保存为 shell 归档，请使用以下命令：

```bash
$ shar orders.txt > orders.shar
shar: Saving orders.txt (text)
```

要提取文件，请使用 Bash 运行该 shell 归档：

```bash
$ bash orders.shar
x - creating lock directory
x - extracting orders.txt (text)
```

要创建当前目录中所有文件的 shell 归档，请使用以下命令：

```bash
$ shar * > myproject.shar
```

在归档目录时，shar 命令会递归地归档其子目录。

shar 命令有大量开关（选项）。这些开关主要用于处理特殊情况。完整列表见本章的参考部分。

还有一个 unshar 命令。它并不完全是 shar 的反操作，该命令从保存的电子邮件消息中提取 shar 归档，然后使用 Bash 解压文件。

在互联网早期，Shell 归档是通过新闻组共享文件的流行方法。Shell 归档的效率并不高，但它们展示了 shell 脚本的一种不寻常的用法，并且所有 Linux 发行版都提供支持。

虽然 shell 脚本可能不会像我在大三操作系统课程中的 C 程序那样在屏幕上输出竖线并弹出磁盘，但它们调试起来同样困难。知道 Bash 具有调试功能会让查找和修复脚本变得更容易。借助版本控制、补丁和日志，你的工作可以与其他程序员分享，由脚本更新引起的问题也可以被快速定位。这些工具在下一章关于子 shell 的内容中将会派上用场。

## 参考部分

### tee 命令开关

- `--append`（或 `-a`）—将输出附加到现有文件的末尾。
- `--ignore-interrupts`（或 `-i`）—即使被 Linux 信号中断，仍保持 tee 运行。

### Linux Time 命令开关

- `--portability`（或 `-p`）—遵循 POSIX 标准。
- `--output`（或 `-o`）—将输出重定向到文件。
- `--append`（或 `-a`）—将结果附加到文件。
- `--verbose`（或 `-v`）—提供每个统计详情的详细说明。

### Bash Time 命令格式代码

- `$$`—字面量 `%`。
- `$[precision][.1]R`—实际时间；以秒为单位的经过时间。
- `$[precision][.1]U`—用户模式下消耗的 CPU 秒数。
- `$[precision][.1]S`—系统模式下消耗的 CPU 秒数。
- `$P`—CPU 使用率，计算方式为 `($U + $S) / $R`。

### Linux Time 命令格式代码

- `$$`—字面量 `%`。
- `%R`—实际时间；以时:分:秒格式表示的经过时间。
- `%e`—实际时间；以秒为单位的经过时间。
- `%S`—以 CPU 秒为单位的系统时间。
- `%U`—以 CPU 秒为单位的用户时间。
- `%P`—程序使用的 CPU 百分比。
- `%M`—程序的最大常驻集大小（以千字节为单位）。
- `%t`—程序的平均常驻集大小（以千字节为单位）。
- `%D`—未共享数据区的平均大小。
- `%p`—未共享堆栈的平均大小（以千字节为单位）。
- `%X`—共享文本区的平均大小。
- `%Z`—系统页的大小（以字节为单位）。
- `%F`—主要页面错误的数量。
- `%R`—次要页面错误的数量（页面之前已加载且仍由 Linux 缓存）。
- `%W`—进程被换出的次数。
- `%c`—时间片上下文切换的次数。
- `%w`—自愿上下文切换的次数。
- `%I`—文件系统输入的次数。
- `%O`—文件系统输出的次数。
- `%R`—接收套接字消息的次数。
- `%S`—发送套接字消息的次数。
- `%K`—接收信号的次数。
- `%C`—命令行。
- `%X`—退出状态。

## Shell 调试选项

- `-o errexit`—如果命令返回错误代码，终止 shell 脚本。
- `-o nounset`—如果引用未设置（或不存在）的变量，则以错误终止。
- `-o xtrace`—在执行每条命令前显示该命令。

### `shar` 命令开关

- `-quiet`（`-silent` 或 `-q`）—在创建归档时隐藏状态消息。
- `-intermix-type`（`-p`）—允许打包选项在命令行中单独应用，而不是应用于所有文件。
- `-stdin-file-list`（或 `-f`）—从标准输入读取要打包的文件列表。
- `-output-prefix=s`（或 `-o`）—生成的 *shar* 文件的名称（与 `-whole-size-limit` 一起使用时）。
- `-whole-size-limit=k`（或 `-l`）—将生成的 *shar* 文件的大小限制为指定的千字节数，但不拆分单个文件。
- `-split-size-limit=k`（或 `-k`）—将生成的 *shar* 文件的大小限制为指定的千字节数，并拆分单个文件。
- `-archive-name=name`（或 `-n`）—在头部添加归档名称行。
- `-submitter=email`（或 `-m`）—在头部添加 *submitted* by（提交者）行。
- `-net-header=s`—添加 *submitted* by（提交者）和 *archive* name（归档名称）头部。
- `-cut-mark`（或 `-c`）—添加 `cut here`（在此处裁剪）行，用于标记嵌入电子邮件正文中的归档的开头。
- `-mixed-uencode`（或 `-m`）—（默认）允许文本和 uencode 二进制文件。
- `-text-files`（或 `-T`）—强制将所有文件视为文本处理。
- `-uencode`（或 `-B`）—将所有文件视为要 uencode 的二进制数据。
- `-gzip`（或 `-z`）—使用 gzip 压缩所有数据并进行 uencode。
- `-level-for-gzip=l`（或 `-g`）—设置压缩级别（1–9）。
- `--compress`（或 `-Z`）—使用 Linux `compress` 命令压缩所有数据并进行 uuencode。
- `--bits-per-code=B`（或 `-b` `$B`）—设置 `compress` 压缩字大小（默认 12 位）。
- `--no-character-count`（或 `-w`）—抑制字符计数检查。
- `--no-md5-digest`（或 `-D`）—抑制 MD5 校验和。
- `--force-prefix`（或 `-P`）—在前缀字符后添加行。
- `--here-delimiter=d`（或 `-d` `$d`）—将 `here` 文件分隔符更改为 *d*。
- `--vanilla-operation`（或 `-V`）—创建一个可以使用最少数量 Linux 命令解压的归档。
- `--no-piping`（或 `-P`）—不在 `shar` 文件中使用管道。
- `--no-check-existing`（或 `-x`）—覆盖现有的 `shar` 文件。
- `--query-user`（或 `-X`）—在解压时，覆盖前提示用户。
- `--no-timestamp`（或 `-n`）—在解包时不固定修改时间戳。
- `--quiet-unshar`（或 `-Q`）—丢弃解包注释。
- `--basename`（或 `-f`）—解压时丢弃路径名，将所有文件存储在当前目录。
- `--no-i18n`—Shell 归档中不启用国际化。
- `--print-text-domain-dir`—显示 `shar` 用于不同语言消息的目录。

## 参数和子 Shell

**T**o serve as a flexible tool，脚本在被调用时必须通过限定（qualification）来提供额外信息，说明如何以及在何处执行其任务。与命令类似，脚本使用参数进行限定。开关和参数使脚本可复用，从而减少成本和时间。

### 位置参数

有三种方法可以使用参数扩展 Linux 脚本。第一种方法使用*位置参数*。脚本可以根据参数在命令行中出现的位置（或顺序）来引用它们。由于其他两种方法依赖于位置参数，因此首先讨论位置参数。

Bash 变量 $0 是脚本的路径名。它不一定是完整的路径名，而是执行脚本时用于指定脚本的路径。

```bash
$ printf "%s\n" "$0" `/bin/bash`
```

在这种情况下，Bash 会话是通过命令 `/bin/bash` 启动的。

当与 `basename` 命令结合使用时，脚本名称会从剩余的路径名中移除。

```bash
$ declare -rx SCRIPT=`basename $0`
$ printf "%s\n" "$SCRIPT"
bash
```

一个稍快的版本使用 Bash 的子字符串功能，避免运行外部程序。

```bash
$ declare -rx SCRIPT=${0%%*/}
$ printf "%s\n" "$SCRIPT"
bash
```




通过从 $0 中查找脚本名称，可以避免在脚本被复制或重命名后打印出错误的名称。SCRIPT 始终是脚本的正确名称。

变量 $# 包含脚本或 shell 会话中参数的数量。如果没有参数，$# 为零。该数字不包括 $0 中的脚本名称。

```bash
$ printf "%d\n" $#
0
```

前九个参数放置在变量 $1 到 $9 中。（超过九个的参数可以通过在大括号内包裹数字来访问。）当使用 nounset shell 选项时，访问未定义的参数会导致错误，就像访问未声明的变量名一样。

```bash
$ printf "%s\n" $9
bash: $9: unbound variable
```

变量 $*（或 $@）将所有参数的完整列表作为单个字符串返回。

使用位置参数时，Bash 不会区分开关和参数。命令行上的每个项目都是脚本的一个独立参数。请参考以下脚本，如列表 9.1 所示。

### 列表 9.1 params.sh

```bash
#!/bin/bash
#
# params.sh: a positional parameter demonstration

printf "There are %d parameter(s)\n" "$#"
printf "The complete list is %s\n" "$@"
printf "The first parameter is %s\n" "$1"
printf "The second parameter is %s\n" "$2"
```

当脚本使用参数 -c 和 t2341 运行时，$1 指代 -c，$2 指代 t2341。

```bash
$ bash params.sh -c t2341
There are 2 parameter(s)
The complete list is -c t2341
The first parameter is -c
The second parameter is t2341
```

尽管 $@ 和 $* 都指代所有参数，但当它们被双引号包围时，行为有所不同。$* 的参数由 IFS 变量的第一个字符分隔，或者如果 IFS 为空则由空格分隔，或者如果 IFS 未设置则没有任何分隔符。$* 将参数集视为单个组。

相反，$@ 始终用空格分隔参数，并将参数视为独立项，即使它们被双引号包围。$@ 经常用于将整套开关传递给另一个命令（例如，ls $@）。

虽然位置参数是查看开关和参数的直接方式，但它们不会“遍历”列表。有一个内置的 `shift` 命令，它会丢弃 $1 中的参数，并将剩余参数依次下移一位以填补空缺。使用 `shift`，你可以依次检查每个参数，仿佛它们都是第一个参数。

列表 9.2 展示了一个使用 `shift` 的完整示例。

### 列表 9.2 param2.sh

```bash
#!/bin/bash
#
# param2.sh
#
# This script expects the switch -c and a company name. --help (-h)
# is also allowed.

shopt -s -o nounset
declare -rx SCRIPT=${0##*/}

# Make sure there is at least one parameter or accessing $1
# later will be an error.

if [ $# -eq 0 ]; then
    printf "%s\n" "Type --help for help."
    exit 192
fi

# Process the parameters

while [ $# -gt 0 ]; do
    case "$1" in
        -h | --help) # Show help
            printf "%s\n" "Usage: $SCRIPT [-h] [--help] -c company"
            exit 0
            ;;
        -c) shift
            if [ $# -eq 0 ]; then
                printf "${SCRIPT}:${LINENO}: %s\n" "company for -c is missing" >&2
                exit 192
            fi
            COMPANY="$1"
            ;;
        *) printf "${SCRIPT}:${LINENO}: %s\n" "switch $1 not supported" >&2
            exit 192
            ;;
    esac
    shift
done

if [ -z "$COMPANY" ]; then
    printf "$@\n" "company name missing" >&2
    exit 192
fi

# <-- begin work here
exit 0
```

最后一个与参数相关的开关是 $\_（美元下划线）。这个开关有两个用途。首先，当 shell（或 shell 脚本）最初启动时，它代表 shell 或 shell 脚本的路径名。其次，每次执行命令后，该命令会以包含命令路径名的变量形式放入环境中。

```bash
$ /bin/date
Fri Jun 29 14:39:58 EDT 2001
$ printf "$_\n" "$_"
/bin/date
$ date
Fri Jun 29 14:40:04 EDT 2001
$ printf "$_\n" "$_"
date
```

你可以使用 $\_ 来重复最后一个参数。

### **getopts** 命令

位置参数方法有两个局限性。首先，它要求脚本编写者测试错误并创建相应的消息。其次，**shift** 命令会破坏所有参数。如果你想在稍后访问它们，你将无法做到。

为了解决这些问题，Bash 包含了一个内置的 **getopts**（*获取选项*）命令，该命令可以提取并检查开关，而不干扰位置参数变量。意外的开关，或缺少参数的开关，会被识别并报告为错误。

使用 **getopts** 需要脚本编写者做一些准备工作。首先，你必须定义一个包含预期开关字母列表的字符串。按照惯例，这个变量被称为 **OPTSTRING**。如果任何开关需要参数，则在开关字符后添加一个冒号。

例如，如果 param2.sh 脚本期望 -h（帮助）和 -c（带有公司 ID 参数的公司 ID），那么 OPTSTRING 将是 hc:。

在选项列表之后有一个必需的第二参数：用于记录遇到的每个选项的 shell 变量名称。

每次运行 getopts 命令时，都会检查命令行上的下一个开关，并将开关的名称保存在变量 SWITCH 中。下一个待检查参数的位置在一个名为 OPTIND 的变量中。如果它不存在，OPTIND 会在检查第一个脚本参数之前自动设置为 1。如果脚本有任何参数，它会保存在一个名为 OPTARG 的变量中。列表 9.3 展示了一个测试脚本第一个参数的短脚本。

### 列表 9.3 getopt.sh

```bash
#!/bin/bash
#
# getopt.sh

declare SWITCH
getopts "hc:" SWITCH
printf "The first switch is SWITCH=%s OPTARG=%s OPTIND=%s\n" \
    "$SWITCH" "$OPTARG" "$OPTIND"
```

在这个短脚本中，未知的开关会给 SWITCH 变量赋值一个问号 (?)，并显示一条错误消息。

```bash
$ bash getopt.sh -h
The first switch is SWITCH=h OPTARG= OPTIND=2
$ bash getopt.sh -c a4327
The first switch is SWITCH=c OPTARG=a4327 OPTIND=3
$ bash getopt.sh -a
t.sh: illegal option -- a
The first switch is SWITCH=? OPTARG= OPTIND=1
```

通过使用开关列表中的第一个字符作为冒号，可以隐藏错误消息。通过使用 :hc:，针对无效开关 -a 的错误会消失，但无效选项会被保存在 OPTARG 中，以便用于自定义错误消息。

```bash
$ bash getopt.sh -a
The first switch is SWITCH=? OPTARG=a OPTIND=1
```

你还可以通过创建一个值为 0 的 OPTERR 变量来隐藏错误。这会覆盖合法开关字符串的内容。

开关通常使用 while 和 case 语句进行检查。参见列表 9.4。

### 列表 9.4 getopt_demo.sh

```bash
#!/bin/bash
#
# This script expects the switch -c and a company name. --help (-h)
# is also allowed.

shopt -s -o nounset

declare -rx SCRIPT=${0##*/}
declare -r OPTSTRING="hc:"
declare SWITCH
declare COMPANY

# Make sure there is at least one parameter

if [ $# -eq 0 ]; then
   printf "%s\n" "Type --help for help."
   exit 192
fi

# Examine individual options

while getopts "$OPTSTRING" SWITCH ; do
   case $SWITCH in
      h) printf "%s\n" "Usage: $SCRIPT [-h] -c companyid"
         exit 0
         ;;
      c) COMPANY="$OPTARG"
         ;;
      \?) exit 192
         ;;
      *) printf "$SCRIPT: $LINENO: %s\n" "script error: unhandled argument"
         exit 192
         ;;
   esac
done

printf "$SCRIPT: %s\n" "Processing files for $COMPANY..."
```

这个脚本比位置参数版本更短。脚本必须查找的唯一错误是 `OPTSTRING` 中列出的、但未被 `case` 语句处理的合法开关。

作为特殊情况，如果将变量作为额外参数提供给 `getopts` 命令，`getopts` 可以处理变量而不是脚本参数。这可以用于测试使用特定参数的开关。




## getopt 命令

虽然 `getopts` 命令在一定程度上简化了脚本编程，但它不符合 Linux 的开关标准。特别是，`getopts` 不允许使用双破折号长开关。

为了绕过这一限制，Linux 包含了其自身的 `getopt`（单数形式，*而非* `getopts`）命令。与 `getopts` 类似，`getopt` 支持长开关，并具备 `getopts` 没有的其他功能，并且在脚本中的使用方式完全不同。

由于 `getopt` 是一个外部命令，它无法像 `getopts` 那样将开关保存到变量中。它没有将环境变量导回脚本的方法。同样，除非通过 `$@` 将开关复制到 `getopt` 命令中，否则 `getopt` 不知道 shell 有哪些开关。因此，`getopt` 不是在循环中运行，而是运行一次以将作为单个组的所有参数进行处理。

与 `getopts` 一样，`getopt` 使用 `OPTARG` 选项列表。列表前可以加上 `--options`（或 `-o`），以明确表示这些是开关列表。列表项可以像 `getopts` 中那样列出，也可以作为逗号分隔的列表列出。

必须使用双破折号和 `$@` 将传递给脚本的选项列表附加到 `getopt` 命令中。双破折号表示 `getopt` 开关结束的地方和脚本开关开始的地方。

列表 9.5 包含一个脚本，该脚本使用 `getopt` 复制了 `getopts.sh` 的功能。请注意，使用 `--name`（或 `-n`）开关来为 `getopt` 指定脚本名称，以便在任何错误消息中使用该名称。

### 列表 9.5: getopt.sh

```bash
#!/bin/bash
#
#getopt.sh - a demonstration of getopt
declare -rx SCRIPT=${0##*/}
declare RESULT
RESULT=$(getopt --name "$SCRIPT" --options "-h,-c" -- "$@")
printf "status code=$? result=\"$RESULT\"\n"
```

以下是结果：

```
$ bash getopt.sh -h
 status code=0 result=" -h --"
$ bash getopt.sh -c
 getopt.sh: option requires an argument -- c
 status code=1 result=" --"
$ bash getopt.sh -x
 getopt.sh: invalid option -- x
 status code=1 result=" --"
```

状态代码指示 `getopt` 是否成功。状态代码 1 表示 `getopt` 打印了错误消息。状态代码 2 表示 `getopt` 命令本身的选项存在问题。

使用 `--longoptions`（或 `-l`）开关支持长开关。包含一个预期的长选项的逗号分隔列表。例如，要允许 `--help` 开关，请执行以下操作：

```bash
RESULT=$(getopt --name "$SCRIPT" --options "-h, -c:" \
   --longoptions "help" -- "$@")
```

`getopt` 还有其他增强功能。要为长选项指定可选参数，请添加等号和参数名称。

如果开关名称后面跟着双冒号，则表示该开关有一个可选参数，而不是必需参数。如果 `POSIXLY_CORRECT` 变量存在且选项列表以 + 开头，则不允许开关有参数，并且第一个参数被视为开关的结束。

如果 `GETOPT_COMPATIBLE` shell 变量存在，`getopt` 的行为更接近 C 语言 `getopt` 标准库函数。某些旧版本的 `getopt` 默认具有此行为。如果需要检查此行为，请使用 `-T`（或 `--test`）开关来测试 C 兼容模式：如果没有在兼容模式下运行，状态代码为 4。

在 `getopt` 检查开关之后，你打算如何处理这些开关？可以使用 `set` 命令替换原始参数：

```bash
eval set -- "$RESULT"
```

现在，可以使用位置参数或内置的 `getopts` 检查参数，如列表 9.6 所示。

### 列表 9.6: getopt_demo.sh

```bash
#!/bin/bash

# getopt_demo.sh
# This script expects the switch -c and a company name. --help (-h) is also allowed.

shopt -s -o nounset

declare -rx SCRIPT=${0##*/}
declare -r OPTSTRING="-h, -c:"
declare COMPANY
declare RESULT

# Check getopt mode

getopt -T
if [ $? -ne 4 ] ; then
    printf "%s: %s\n" "$SCRIPT" "getopt is in compatibility mode" >&2
    exit 1
fi

# Test parameters

RESULT=$(getopt --name "$SCRIPT" --options "$OPTSTRING" \
  --longoptions "help" -- "$@")
if [ $? -gt 0 ] ; then
    exit 1
fi

# Replace the parameters with the results of getopt

eval set -- "$RESULT"

# Process the parameters

while [ $# -gt 0 ] ; do
  case "$1" in
    -h | --help) # Show help
      printf "Usage: %s [-h][--help] -c companyid\n" "$SCRIPT"
      exit 0
      ;;
    -c )
      shift
      if [ $# -eq 0 ] ; then
        printf "%s:%s: %s\n" "$SCRIPT" "$LINENO" "company for -c is missing" >&2
        exit 1
      fi
      COMPANY="$1"
      ;;
  esac
  shift
done

if [ -z "$COMPANY" ] ; then
  printf "company name missing\n" >&2
  exit 1
fi

printf "%s: %s\n" "$SCRIPT" "Processing files for $COMPANY..."

# <-- begin work here

exit 0
```

这看起来可能工作量很大，但对于具有许多复杂开关的脚本来说，`getopt` 使处理它们的任务变得更加容易。

还有许多特殊的开关。`--alternative`（或 `-a`）开关允许长选项仅带有单个前导减号。使用此开关违反了 Linux 惯例。`--quiet-output`（或 `-q`）可用于检查开关，而不将处理后的列表返回到标准输出。`--quiet`（或 `-q`）通过状态代码指示任何错误，但隐藏错误消息，以便你可以创建自定义消息。`--shell`（或 `-u`）开关使用引号来保护可能被 shell 以特殊方式处理的特殊字符，例如空格。（这仅在 C 兼容模式下是必要的。）

## 子 shell

第 7 章“复合命令”中提到，可以使用花括号将一组命令组合在一起。这些命令作为一个组起作用，并返回单个状态代码。

```
$ ( sleep 5 ; printf "%s\n" "Sleep for 5 seconds" ; )
Sleep for 5 seconds
```

子 shell 是一组使用圆括号而不是花括号分组的命令。与命令组不同，如果子 shell 出现在单行上，最后一个命令后面不需要分号。

```
$ ( sleep 5 ; printf "%s\n" "Sleep for 5 seconds" )
Sleep for 5 seconds
```

子 shell 的行为像是花括号命令集和独立脚本的混合体。与语句组一样，子 shell 是一组返回单个状态代码的语句。与独立的 shell 脚本一样，子 shell 拥有自己的环境变量。

```
$ declare -ix COUNT=15
$ ( COUNT=10 ; printf "%d\n" "$COUNT" ; )
10

$ printf "%d\n" "$COUNT"
15

$ ( COUNT=20 ; printf "%d\n" "$COUNT" )
20

$ printf "%d\n" "$COUNT"
15
```

在这个例子中，命令组可以改变 shell 会话中变量 `COUNT` 的值，因为该组作为会话的一部分运行。子 shell 无法改变主程序中 `COUNT` 的值，因为它运行起来就像是一个独立的 shell 脚本。`COUNT` 是会话中变量的副本，子 shell 只能改变其私有的 `COUNT` 副本。

子 shell 通常与管道一起使用。使用管道（或文件重定向），可以将命令的结果重定向到子 shell 进行处理。数据出现在子 shell 的标准输入中，如列表 9.7 所示。

### 列表 9.7: subshell.sh

```bash
#!/bin/bash
#
# subshell.sh
#
# Perform some operation to all the files in a directory

shopt -s -o nounset
declare -rx SCRIPT=${0##*/}
declare -rx INCOMING_DIRECTORY="incoming"

ls -1 "$INCOMING_DIRECTORY" |
(
    while read FILE ; do
        printf "%s: Processing %s...\n" "$SCRIPT" "$FILE"
        # <-- do something here
    done
)
printf "Done\n"
exit 0
```

子 shell 中的 read 命令每次从标准输入读取一行。在这种情况下，它读取由 ls 命令创建的文件列表。

```
$ bash subshell.sh
subshell.sh: Processing alabama_orders.txt...
subshell.sh: Processing new_york_orders.txt...
subshell.sh: Processing ohio_orders.txt...
Done
```

子 shell 继承的不仅仅是环境变量。这一主题将在第 14 章“函数和脚本执行”中详细讨论。

参数处理大大增加了脚本的灵活性，而子 shell 是不可缺少的工具。但在脚本真正被称为专业之前，仍有许多基础知识需要掌握。没有作业控制和信号处理的脚本仍然是不完整的。




## 参考章节

## getopt 命令开关

- `--longoptions`（或 `-l`）—预期长选项的逗号分隔列表。
- `--alternative`（或 `-a`）—允许长选项仅使用单个前导减号。
- `--quiet-output`（或 `-q`）—检查开关，但不将处理后的列表返回到标准输出。
- `--quiet`（或 `-q`）—通过状态码指示任何错误，但隐藏错误消息。
- `--shell`（或 `-u`）—使用引号保护特殊字符。
- `--test`（或 `-t`）—测试 C 兼容性模式。

# 10 作业控制与信号

虽然我在葡萄园长大，但我并没有花太多时间在田间。我想，那是我父亲的一种避免让我偏向于汗水和晒伤生活的做法。不知为何，有一种农业技能我始终未能掌握，那就是使用手势信号。那些在户外度过了多年时光的人似乎习惯了在远距离和噪音中做手势，能够理解最令人费解的动作。而我却不是这样。

一个夏天，我父亲正试图用他的拖拉机将一台重型设备装上一辆皮卡车的后部。他让我站在卡车底部附近，以便对齐设备并告诉他何时开始降低。当一切看起来都到位时，我给了他信号。不幸的是，我的眼镜够厚，导致球面像差——也就是说，有时物体看起来是歪的，因为通过镜片的光线发生了弯曲。几乎立刻，我看到设备没有居中，于是开始上下跳动，疯狂地做手势。但我父亲直到设备发出令人毛骨悚然的咔嚓声，压垮了卡车的一侧，才注意到有任何不对劲。

无论是我的信号传达不当，还是他的注意力不集中，这都无关紧要。重要的是产生了一个无法沟通的重要条件。类似地，脚本需要能够向其他脚本委派职责，并在紧急事务发生时互相中断。这种协作是通过作业控制和 Linux 信号处理实现的。

## 作业控制

你可以通过在命令末尾输入一个_ampersand_（&）来启动后台任务。Bash 将后台任务称为*作业*。任何在后台运行的命令或脚本都是一个*作业*。在交互式会话期间，shell 会维护一个所有未完成作业列表。使用 Bash 命令管理后台任务被称为*作业控制*。

作业控制在命令提示符下默认可用，但在脚本中必须使用 `-o monitor` shell 选项启用。如果没有作业控制，虽然仍可以从脚本启动后台任务，但 Bash 的作业管理命令将不可用。

内置的 `jobs` 命令列出活动作业。当后台任务完成时，该作业将从列表中移除。

```bash
$ sleep 60 &
[1]+ 28875
$ jobs
[1]+  Running          sleep 60 &
```

在交互式会话中，Bash 在显示命令提示符之前会自动检查并报告后台作业的任何变化。作业状态以与 `jobs` 命令相同的格式显示。`set -b` 命令会导致作业状态的变化在发生时立即显示，即使这意味着要在用户输入时中断他/她。在带有作业控制的脚本中，后台任务的状态也会被检查和打印。

加号指示当前正在运行的作业，即使用 `fg` 命令时进入前景的作业。减号指示最后启动的作业。

Linux 为所有作业分配唯一的*进程标识符*（或 PID）。你可以使用 `-l`（*长格式*）开关查看它。

```bash
$ jobs -l
[1]+ 28875 Running      sleep 60 &
```

方括号中的数字是作业在 shell 作业列表中的位置。作业的 PID 号可以使用百分号（%）扩展为一个命令。`kill` 命令可以停止一个作业。要杀死第一个后台任务，使用 `%1`。以下示例产生的结果与键入 `kill 28875` 相同。

```bash
$ kill %1
[1]+  Terminated         sleep 60
```

其他作业列表百分号代码包括用于当前后台任务的 `%` 和 `%+`，用于最后启动的后台任务的 `%-`，以及用于名称为 *name* 的作业的 `%*name*`。你可以使用 `%?` 搜索作业名称，这会匹配包含特定子串的任意作业。

```bash
$ sleep 10 &
[1] 13692
$ kill %?ele
$
[1]+  Terminated         sleep 10
```

作业号替换与变量替换不同，尽管 `jobs` 命令的 `-x`（*执行*）开关使其表现得像那样。

```bash
$ printf "${d\n" %1
bash: printf: $1: invalid number
$ jobs -x printf "${d\n" %1
6259
```

在这种情况下，`printf` 命令（不像 `kill`）不是作业控制命令，也不知道作业号。`jobs -x` 命令将作业号替换为 PID 号，然后运行 `printf` 命令。

`-p`（`PID`）开关仅列出进程标识符。显示的作业可以缩小为三种类型：状态变化的作业 `-n`（`new status`），正在运行的作业 `-r`（`running`），以及停止的作业 `-s`（`stopped`）。

你可以使用内置的 `disown` 命令将后台任务从 Bash 的作业列表中移除。

```bash
$ sleep 10 &
[1] 14611
$ sleep 10 &
[2] 14623
$ sleep 10 &
[3] 14628
$ disown $2
$ jobs
[1] Running         sleep 10 &
[3]+ Running        sleep 10 &
```

被放弃的任务即使不再出现在 shell 的作业列表中，仍会继续运行，但作业控制命令将不接受该任务。在这种情况下，第二个作业继续运行，但 `$2` 不再被定义。当第二个作业完成时，Bash 无法通知用户，因为它不再监控该任务。`disown` 命令在移除你不需要跟踪的后台命令时很有用，例如 MP3 播放器、Web 浏览器或 X Window 桌面上的其他后台应用程序。

`-a`（`all`）开关放弃所有作业，就好像后台任务是在没有作业控制的脚本中启动的一样。`-r`（`running`）开关放弃所有正在运行的作业。

你可以使用内置的 `wait` 命令强制脚本等待一个或多个后台任务完成。如果没有指定作业，`wait` 会挂起脚本，直到所有后台任务完成。

```bash
$ sleep 5 &
[1] 7338
$ wait
[1]+ Done                 sleep 5
```

## 信号

*信号*有时被称为*软件中断*；它是一个请求，要求从程序中跳出并执行紧急任务。当 Bash 接收到信号时，它会完成当前命令，识别接收到的是哪个信号，并采取适当的行动。如果之后它能够继续执行脚本，它就会这样做，前进到下一个命令。

信号通过内置的 `kill` 命令发送给脚本。尽管其名称暗示，`kill` 可以做的不仅仅是使用默认的 `SIGTERM` 信号终止程序。假设一个缓慢的命令正在后台运行。

```bash
$ ( sleep 60; echo "DONE"; ) &
[1] 7613
```

`kill` 命令可以使用 `SIGSTOP` 信号挂起该命令。

```bash
$ kill -SIGSTOP 7613
[1]+ Stopped                ( sleep 60; echo "DONE"; )
```

命令停止后，它保持不活跃状态，直到接收到另一个信号，例如 `SIGCONT`。

```bash
$ kill -SIGCONT 7613
$ DONE
[1]+ Done                    ( sleep 60; echo "DONE"; )
```

`SIGCONT` 信号在中断点继续执行。Linux 定义了 63 个不同的信号。最常发送给脚本的信号包括 `SIGTERM`（立即退出脚本）、`SIGSTOP`（停止脚本，暂时使其休眠）、`SIGHUP`（挂断连接）和 `SIGCONT`（继续停止的脚本）。完整列表见附录 E，“信号”。

内置的 `disown` 命令影响信号如何与后台任务共享。如果使用 `-h`（`SIGHUP`）开关，当接收到 `SIGHUP`（例如用户注销时）时，Bash 不会将 `SIGHUP` 共享给特定任务的后台作业。

## suspend 命令

内置的 `suspend` 命令停止脚本，直到接收到信号，就好像脚本接收到 `SIGSTOP` 信号一样。它等效于使用命令 `kill -SIGSTOP $$` 强制脚本自我停止。在脚本中使用 `suspend` 需要启用作业控制。参见清单 10.1。

**清单 10.1** `suspend_demo.sh`

```bash
#!/bin/bash
#
# suspend_demo.sh
#
# 等待 SIGCONT 信号，然后打印一条消息
#
# 关闭干扰脚本执行的 shell 设置。
# 具体来说，我们关闭 nounset 和 monitor 设置。
# 这是因为我们需要能够处理 SIGCONT 信号，
# 而 monitor 设置会干扰这一点。
shopt -s -o nounset
shopt -s -o monitor # 启用作业控制

# 等待 SIGCONT
```





## 列表 10.1 续

```bash
suspend
printf "%s\n" "Who woke me up?"
exit 0
```

当此脚本运行时，它会停止，直到收到 SIGCONT 信号为止。

```bash
$ bash suspend_demo.sh &
[1] 9185
$ 
[1]+  Stopped                bash suspend_demo.sh
$ kill -SIGCONT 9185
$ Who woke me up?
[1]+  Done                   bash suspend_demo.sh
$ 
```

## 陷阱

在 Bash 交互式运行时，它代表用户处理大多数信号。当脚本正在运行且需要执行特殊操作时，处理相应信号是脚本的责任。Bash 采取的操作取决于接收到的信号。

- SIGQUIT 始终被忽略
- 如果启用了作业控制，SIGTIN 将被忽略；否则，它将暂停脚本
- 如果启用了作业控制，SIGTTOU 将被忽略；否则，它将暂停脚本
- 如果启用了作业控制，SIGSTOP 将被忽略；否则，它将暂停脚本
- 如果启用了作业控制，SIGTSTP 将被忽略；否则，它将暂停脚本
- SIGHUP 会发送给脚本启动的所有后台任务，如有必要，还会唤醒已停止的任务

例如，Bash 通常通过向所有子脚本传递信号来处理 SIGHUP 信号（除非使用了 `disown -h`）。你可以通过设置 `huponexit` shell 选项在交互式会话中激活相同的行为：当会话终止时，SIGHUP 会发送给所有正在运行的作业。

其他信号会终止脚本，除非创建了信号处理器（或陷阱）。陷阱是一组命令，在接收到信号时执行。内置的 `trap` 命令管理脚本的信号处理器。

`-l`（列表）开关会列出所有信号及其对应的数字。

并非所有信号都可以通过陷阱捕获。某些信号，如 SIGKILL，即使安装了信号处理器，也始终会终止脚本。

信号处理器通过向 `trap` 命令提供一组命令和一组处理程序来创建。可以使用信号名称或数字。例如，SIGWINCH 是窗口改变大小时生成的信号。通过安装陷阱，每次窗口大小调整时都可以显示一条消息。

```bash
$ trap "printf \"There are %s lines\n\" \"${LINES}\"" SIGWINCH
```

改变窗口大小会导致：

```bash
$ There are 32 lines
$ There are 43 lines
$ There are 37 lines
```

你可以使用 `-p`（打印）开关查看当前的陷阱。

```bash
$ trap -p SIGWINCH
trap -- 'printf "There are %s lines\n" "${LINES}"' SIGWINCH
```

要恢复默认处理器，请不要提供陷阱。

```bash
$ trap SIGWINCH
$ trap -p SIGWINCH
```

SIGUSR1 和 SIGUSR2 是用户定义的信号，没有预定义的含义。它们可以随意在脚本中使用。当以下脚本接收到 SIGUSR1 信号时，它会等待当前命令完成，打印消息 SIGUSR1，并恢复脚本，如列表 10.2 所示。

## 列表 10.2 trap_demo.sh

```bash
#!/bin/bash
#
# trap_demo.sh
#
# Wait indefinitely for SIGUSR1, print a message when one arrives.

shopt -s -o nounset
trap 'printf "SIGUSR1\n"' SIGUSR1

# Infinite loop!
while true ; do
    sleep 1
done

printf "%s\n" "Should never get here!" >&2
exit 192
```

脚本将持续运行，直到被终止。

```bash
$ bash trap_demo.sh &
[1] 544
$ kill -SIGUSR1 544
SIGUSR1
$ kill 544
[1]+  Terminated              bash trap_demo.sh
```

信号处理器的两个最常见用途是唤醒暂停的脚本以及临时阻止某些关键命令的信号，这些命令必须不被中断。要临时忽略信号，请使用空引号或 `null` 命令作为信号处理器，并在不可中断的命令完成后恢复原始信号处理器。

```bash
trap : SIGINT SIGQUIT SIGTERM
# some command that must not be interrupted
trap SIGINT SIGQUIT SIGTERM
```

## 退出处理器

退出处理器是一组命令，每当脚本结束时执行。退出处理器使用不存在的信号 `EXIT`（信号编号 0），如列表 10.3 所示。

## 列表 10.3 exithrap_demo.sh

```bash
#!/bin/bash
#
# exithrap_demo.sh
#
# Display "Goodbye" when this script exits.

shopt -s -o nounset
trap 'printf "Goodbye\\n"' EXIT

sleep 5

exit 0
```

当 shell 退出时，消息 `Goodbye` 将被打印。

```bash
$ bash exithrap_demo.sh
Goodbye
```

当有大量清理工作要做时，退出处理器通常调用一个 shell 函数来执行工作。shell 函数在第 14 章“函数和脚本执行”中有描述。

## killall 命令

Linux 的 `killall` 命令通过程序名而不是通过进程 ID 号来终止进程。顾名思义，所有匹配的作业都会被终止。如果指定了绝对路径，则仅终止运行特定文件的进程。

```bash
$ sleep 15 &
[1] 1225
$ killall sleep
[1]+ Terminated               sleep
```

`killall` 有多个开关。`-e` 开关不终止文件名较长的已交换出（swapped out）进程。`-g` 开关终止进程组。`-i` 开关在终止前提示。`-q` 开关在没有任何进程被终止时抑制警告。`-w` 开关强制 `killall` 等待直到所有进程运行完毕。

## 保持谦让

所有 Linux 程序都在 -20 到 19 之间的优先级数字下运行。优先级表示程序的重要性，数字越低，获得运行时间的比例越高。

Linux 的 `nice` 命令改变命令的优先级。当脚本消耗大量资源时，应始终使用 `nice`，以防止更重要的作业（如处理用户会话）被减慢或中断。当后台任务启动时，Bash 会自动对其执行 nice 操作。

默认情况下，`nice` 降低优先级（即增加优先级数字）10。可以使用任何数字，但优先级只能降低，且永远不能小于 19。（然而，超级用户可以降低或提高任何程序的优先级。）调整值可以指定为减号后的数字，或者使用可读性更强的 `--adjustment=VALUE`（或 `-n VALUE`）开关。

```bash
$ nice --adjustment=20 big_script.sh &
```

相应的 `renice` 命令改变正在运行的后台任务的优先级。与 `nice` 一样，优先级只能降低。与 `nice` 不同，优先级是一个具体的优先级值，而不是偏移量。

优先级是命令后紧跟的一个数字（没有 -）。可选的 `-p`（PID）开关表示参数是进程标识号。`-g` 开关表示一组进程组。`-u` 开关表示要更改的用户名。显然，你只能对自己拥有的程序执行 `renice`。

```bash
$ bash big_script.sh &
[1] 22516
$ renice 10 22516
22516: old priority 0, new priority 10
```

## 进程状态

`jobs` 命令显示后台任务的基本信息。为了获取更详细的信息，Linux 有一个 `ps`（进程状态）命令。这个命令有很多开关，有些带有前导减号，有些没有。其中一些开关是为了与其他操作系统保持兼容。完整的列表在本章的参考部分中给出。

对于 shell 脚本编写而言，最有用的开关是 `-lu`，它以长格式列出特定用户正在运行的所有进程。

```bash
$ ps -lu ken
  F S   UID   PID  PPID C PRI NI ADDR SZ WCHAN TT  TIME CMD
100 S 500 1838 1837 0 62 0 - 547 wait4 pts/1 00:00:01 bash
000 R 500 2274 1838 0 72 0 - 611 - pts/1 00:00:00 ps
```

长格式中的重要列如下：

| 列 | 描述 |
| :----- | :---------- |
| S      | 进程状态 |
| UID    | 运行该程序的会话的用户 ID |
| PID    | 进程标识号 |
| PPID   | 运行该程序的程序的进程标识号 |
| PRI    | Linux 优先级值 |
| NI     | nice 值 |
| TTY    | 该程序使用的 tty 设备，由 tty 命令返回 |
| TIME   | 进程使用的 CPU 时间 |
| CMD    | 命令名称 |

进程的状态是一个通用指示，表示它是否正在运行，如果没有，原因是什么：

- D—不可中断睡眠，通常由等待输入或输出引起
- R—正在运行或等待运行
- S—睡眠
- T—被跟踪或已停止
- Z—一个已失效（“僵尸”）进程，等待被删除

请注意，`ps` 已知的在不同版本的 Linux 之间存在显著变化。为了获得最佳的可移植性，除非避免使用更高级的开关，否则 `ps` 仅应用于调试。

使用信号和陷阱允许脚本协同工作，并相互通知重要事件。退出处理器保证每当脚本退出时，所有必要的清理命令都会执行。`nice` 命令确保高优先级脚本获得 Linux 的最大关注。接下来的两章将研究 Linux 为脚本提供用于处理数据的工具。





## 参考部分

### jobs 命令开关
- `-1`——除常规信息外，还列出进程 ID
- `-P`——仅列出进程 ID
- `-n`——仅打印自上次通知以来状态发生变化的进程
- `-r`——显示正在运行的任务
- `-S`——显示已停止的任务
- `-x c args`——在所有出现于可选参数 `args` 中的任务规格均被替换为该任务进程组领导者的进程 ID 后，运行命令 `c`

### kill 命令开关
- `-1 n`——列出信号名称；`n` 是可选的信号编号列表
- `-S`——指定要发送的信号名称
- `-n`——指定要发送的信号编号

### renice 命令开关
- `-p pids`——根据进程标识符列表进行 nice 值调整
- `-g gids`——根据进程组列表进行 nice 值调整
- `-u users`——根据用户列表进行 nice 值调整

### ps 命令开关
- `-A`——选择所有进程
- `-a`——选择所有具有 tty 的进程，但不包括任何会话领导者
- `a`——选择终端上的所有进程，包括其他用户的进程
- `-C`——按命令名称选择进程
- `-c`——对于 `-1` 选项提供不同的调度器信息
- `C`——使用原始 CPU 时间而非衰减平均值来计算 %CPU
- `c`——使用真实的命令名称
- `-columns`（或 `cols` 或 `-width`）——设置屏幕宽度
- `-cumulative`（或 `s`）——包含某些已终止子进程的数据（作为与父进程之和）
- `-a`——选择所有进程，但省略会话领导者
- `-deselect`——否定选择
- `-e`——选择所有进程
- `e`——在命令后显示环境变量
- `-f`——显示完整列表
- `-forest`（或 `-H` 或 `f`）——显示进程层级结构（森林视图）
- `-format`（或 `u`）——显示面向用户的格式
- `-Group`（或 `-G`）——按真实组名或 ID 选择
- `-group`（或 `-g`）——按有效组名或 ID 选择
- `-no-headers`（或 `h`）——不打印表头行
- `-html`——显示经过 HTML 转义的输出
- `-headers`——重复打印表头行
- `-j`（或 `J`）——使用 jobs 格式
- `-l`（或 `1`）——使用长格式
- `L`——列出所有格式说明符
- `-lines`（或 `-row`）——设置屏幕高度
- `-m`——显示线程
- `m`——显示所有线程
- `-N`——等同于 `-deselect`
- `-n`（或 `N`）——设置命名列表文件
- `n`——对 wcH 和用户使用数值输出
- `-no-header`——不打印表头行
- `-nul`（或 `-null` 或 `-zero`）——显示未填充对齐的输出，并使用 NULL 字符
- `-o`（或 `0`）——预加载的 `-o`
- `-o`（或 `o`）——用户自定义格式
- `-pid`（或 `-p`）——按进程 ID 选择
- `p`——按进程 ID 选择
- `x`——将输出限制为正在运行的进程
- `-sid`（或 `-s` 或 `-n` 或 `n`）——选择属于给定会话的进程，其中 `n` 为 SID
- `s`——显示信号格式
- `-sort`——指定排序顺序
- `T`——选择此终端上的所有进程
- `-tty`（或 `-t`）——按终端选择
- `-user`（或 `-U`）——按真实用户名或 UID 选择
- `--user`（或 `-u`）——按有效用户名或 ID 选择
- `U`——选择指定用户的进程
- `--version`（或 `-V` 或 `V`）——打印版本信息
- `-w`（或 `w`）——显示宽格式输出
- `x`——选择没有控制 tty 的进程
- `X`——旧版 Linux i386 寄存器格式
- `Y`——不显示标志；用 `rss` 替代 `addr`

## ps 命令排序代码
- `c`（或 `cmd`）——可执行文件的简单名称
- `C`（或 `cmdline`）——完整命令行
- `f`（或 `flags`）——如同长格式中 `f` 字段所示的标志
- `g`（或 `pgid`）——进程组 ID
- `G`（或 `pgrp`）——控制 tty 的进程组 ID
- `j`（或 `cutime`）——累计用户时间
- `J`（或 `cstime`）——累计系统时间
- `k`（或 `utime`）——用户时间
- `K`（或 `stime`）——系统时间
- `m`（或 `minflt`）——次要页面错误次数
- `M`（或 `majflt`）——主要页面错误次数
- `n`（或 `cminflt`）——累计次要页面错误次数
- `N`（或 `cmajflt`）——累计主要页面错误次数
- `o`（或 `session`）——会话 ID
- `p`（或 `pid`）——进程 ID
- `P`（或 `ppid`）——父进程 ID
- `r`（或 `rss`）——常驻集大小
- `R`（或 `resident`）——常驻页面数
- `s`（或 `size`）——以千字节为单位的内存大小
- `S`（或 `share`）——共享页面数量
- `t`（或 `tty`）——tty 的次设备号
- `T`（或 `starttime`）——进程启动时间
- `U`（或 `uid`）——用户 ID 号
- `u`（或 `user`）——用户名
- `v`（或 `vsze`）——总虚拟内存使用量（以字节为单位）
- `y`（或 `priority`）——内核调度优先级

## 11
## 文本文件基础

文本文件是包含人类可读文本的文件。根据操作系统的不同，每行以换行符、回车符或两者组合结尾。按照 Linux 约定，每行以换行符结尾，即 printf 中的 `\n`（新行）字符。

本章示例使用一个文本文件，该文件按名称、价格、数量和供应商编号列出若干件家具，如清单 11.1 所示。

```
Listing 11.1 orders.txt

Birchwood China Hutch,475.99,1,756
Bookcase Oak Veneer,205.99,1,756
Small Bookcase Oak Veneer,205.99,1,756
Reclining Chair,1599.99,1,757
Bunk Bed,705.99,1,757
Queen Bed,925.99,1,757
Two-drawer Nightstand,125.99,1,756
Cedar Toy Chest,65.99,1,757
Six-drawer Dresser,525.99,1,757
Pine Round Table,375.99,1,757
Bar Tool,45.99,1,756
Lawn Chair,55.99,1,756
Rocking Chair,287.99,1, 757
Cedar Armoire,825. 99,1,757
Mahogany Writing Desk,463.99,1,756
Garden Bench,149.99,1,757
Walnut TV Stand,388.99,1,756
Victorian-style Sofa,1225.99,1,757
Chair - Rocking,287.99,1,75
Grandfather Clock,2045.99,1,756
```

Linux 包含许多用于处理文本文件的实用程序。某些程序可以充当过滤器，处理文本以便通过管道传递给另一个命令。当文本文件通过管道传递时，被称为*文本流*，即文本字符流。

### 处理路径名

Linux 有三个用于路径名的命令。

*basename* 命令检查路径并显示文件名。它不会检查文件是否存在。

```
$ basename /home/kburtch/test/orders.txt
orders.txt
```

如果包含后缀作为第二个参数，*basename* 会在后缀与文件后缀匹配时删除该后缀。

```
$ basename /home/kburtch/test/orders.txt .txt
orders
```

用于提取文件路径的对应程序是 *dirname*。

```
$ dirname /home/kburtch/test/orders.txt
/home/kburtch/test
```

路径中最后一个目录后没有尾部斜杠。

要验证路径名是否是正确的 Linux 路径名，请使用 *pathchk* 命令。该命令验证路径中的目录（如果已存在）是否可访问，且目录和文件名称是否过长。如果路径存在问题，*pathchk* 会报告问题并返回错误代码 1。

```
$ pathchk "-/x" && echo "Acceptable path"
Acceptable path
$ mkdir a
$ chmod 400 a
$ pathchk "a/test.txt"
pathchk: directory 'a' is not searchable
$ pathchk "~/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"\
'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'\
'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'\
'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'\
'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'\
'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'\
'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'\
'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'\
" && echo "Acceptable path"
pathchk: name
'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'
'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'
'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'
'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'
'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'
'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'
'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'
'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'
'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'
has length 388; exceeds limit of 255
```




使用 `-p` 可移植性开关时，pathchk 会为所有符合 POSIX 标准的 Unix 系统执行更严格的可移植性检查。这会识别路径名中不允许出现的字符，例如空格。

```
$ pathchk “new file.txt”
$ pathchk -p “new file.txt”
pathchk: path 'new file.txt' contains nonportable character ''
```

pathchk 适用于检查来自外部源的路径名，例如来自另一个脚本的路径名或由用户输入的路径名。

## 文件截断

基于 Unix 的操作系统（包括 Linux ext3 文件系统）的一个特定特性是磁盘空间为文件预留的方式。在 Linux 中，文件的磁盘空间永远不会被释放。例如，如果你用一个字节覆盖一个 1MB 的文件，Linux 仍然会为该文件保留 1MB 的磁盘空间。

如果你正在处理文件大小差异很大的文件，你应该删除并重新创建文件以释放磁盘空间，而不是简单地覆盖它。

这种行为影响所有文件，包括目录。如果一个程序从一个大目录中删除了所有 5,000 个文件，并将单个文件放入该目录，该目录仍会保留为 5,000 个文件条目预留的空间。释放此空间的唯一方法是删除并重新创建目录。

## 识别文件

如第 3 章“文件、用户和 Shell 定制”中所述，内置的 `type` 命令可以识别命令是否为内置命令，如果是 Linux 命令，则显示其所在位置。

要测试除命令以外的文件，Linux `file` 命令会执行一系列测试来确定文件类型。首先，`file` 确定文件是否为常规文件或为空文件。如果文件是常规文件，`file` 会查阅 `/usr/share/magic` 文件，通过检查文件的前几个字节来尝试确定文件包含的内容。如果文件是 ASCII 文本文件，它会对常见单词进行检查，以尝试确定文本的语言。

```
$ file empty_file.txt
empty_file.txt: empty

$ file orders.txt
orders.txt: ASCII text
```

`file` 也适用于程序。如果 `check-orders.sh` 是一个 Bash 脚本，`file` 会将其识别为 shell 脚本。

```
$ file check-orders.sh
check-orders.sh: Bourne-Again shell script text

$ file /usr/bin/test
/usr/bin/test: ELF 32-bit LSB executable, Intel 80386, version 1,
dynamically linked (uses shared libs), stripped
```

在脚本编程中，`file` 的 `-b`（简要）开关会隐藏文件名，仅返回对文件的评估结果。

```
$ file -b orders.txt
ASCII text
```

其他有用的开关包括 `-f`（文件），用于从特定文件中读取文件名。`-i` 开关返回适合 Web 编程的 MIME 类型描述。使用 `-z`（压缩）开关时，`file` 会尝试确定存储在压缩文件内的文件类型。`-L` 开关会跟随符号链接。

```
$ file -b -i orders.txt
text/plain, ASCII
```

## 创建和删除文件

如第 3 章“文件、用户和 Shell 定制”中所述，文件使用 `rm`（移除）命令删除。`-f`（强制）命令会在文件权限指示脚本无法写入文件时删除文件，但 `rm` 永远不会从脚本不拥有的目录中删除文件。（粘性位是一个例外，将在第 15 章“Shell 安全性”中讨论。）

与处理文件时一样，在尝试删除文件之前，始终要检查文件是否存在。请参阅清单 11.2。

**清单 11.2** `rm_demo.sh`

```bash
#!/bin/bash
#
# rm_demo.sh: deleting a file with rm
shopt -s -o nounset

declare -rx SCRIPT=${0##/}
declare -rx FILE2REMOVE="orders.bak"
declare -x STATUS

if [ ! -f "$FILE2REMOVE" ]; then
  printf '%s\n' "$SCRIPT: $FILE2REMOVE does not exist" >&2
  exit 192
else
  rm "$FILE2REMOVE" >&2
fi
STATUS=$?

if [ $STATUS -ne 0 ] ; then
  printf "%s\n" "$SCRIPT: Failed to remove file ${FILE2REMOVE}"
  exit $STATUS
fi

exit 0
```

在删除多个文件时，避免使用 `-r`（递归）开关或文件名通配符。相反，获取要删除的文件列表（使用如 `find` 等命令，下文将讨论），并在尝试删除任何文件之前对每个单独的文件进行测试。这比替代方法慢，但如果出现问题，不会删除任何文件，你可以安全地检查问题的原因。

新的空文件使用 `touch` 命令创建。该命令之所以称为 `touch`，是因为当它用于现有文件时，即使不修改文件内容，也会更改其修改时间。

`touch` 经常与 `rm` 结合使用，为脚本创建新的空文件。使用 `>>` 追加输出时，如果文件存在不会导致错误，从而无需记住文件是否存在。

例如，如果脚本要生成名为 `run_results.txt` 的摘要文件，可以使用清单 11.3 创建一个新文件。

**清单 11.3** `touch_demo.sh`

```bash
#!/bin/bash
#
# touch_demo.sh: using touch to create a new, empty file

shopt -s -o nounset

declare -rx RUN_RESULTS="./run_results.txt"

if [ -f "$RUN_RESULTS" ] ; then
    rm -f "$RUN_RESULTS"
    if [ $? -ne 0 ] ; then
        printf "%s\n" "Error: unable to replace $RUN_RESULTS" >&2
    fi
fi
touch "$RUN_RESULTS"

printf "Run started %s\n" "$(date)" >> "$RUN_RESULTS"
```

`-f` 开关强制每次都创建一个新文件。

## 移动和复制文件

文件使用 `mv`（移动）命令重命名或移动到新目录。如果使用 `-f`（强制），`mv` 会覆盖现有文件而不是报告错误。仅在覆盖文件安全时使用 `-f`。

你可以将 `touch` 与 `mv` 结合使用，在开始新文件之前将旧文件备份到不同的名称下。Linux 备份文件的约定是将其重命名为以波浪号（`~`）结尾。请参阅清单 11.4。

**清单 11.4** `backup_demo.sh`

```bash
#!/bin/bash
#
# backup_demo.sh

shopt -s -o nounset

declare -rx RUN_RESULTS="./run_results.txt"

if [ -f "$RUN_RESULTS" ] ; then
    mv -f "$RUN_RESULTS" "$RUN_RESULTS"~
    if [ $? -ne 0 ] ; then
        printf "%s\n" "Error: unable to backup $RUN_RESULTS" >&2
    fi
    touch "$RUN_RESULTS"
fi

printf "Run started %s\n" "$(date)" >> "$RUN_RESULTS"
```

由于覆盖备份总是安全的，因此使用 `-f` 开关强制移动。归档文件通常比直接删除更好，因为在 Linux 中没有“恢复删除”文件的方法。

与 `mv` 类似的是 `cp`（复制）命令。`cp` 创建文件的副本，并且不删除原始文件。`cp` 还可以使用 `--link` 开关创建链接而不是副本。

## 关于文件的更多信息

有两个 Linux 命令可以显示通过 `test` 命令无法轻松发现的有关文件的信息。

Linux `stat` 命令显示文件的一般信息，包括所有者、大小和最后访问时间。

```
$ stat ken.txt
```

```
File: "ken.txt"
Size: 84        Blocks: 8        Regular File
Access: (0664/-rw-rw-r--)  Uid: ( 503/ kburcth) Gid: ( 503/ kburcth)
Device: 303  Inode: 131093  Links: 1
Access: Tue Feb 20 16:34:11 2001
Modify: Tue Feb 20 16:34:08 2001
Change: Tue Feb 20 16:34:08 2001
```

为了使信息在脚本中更易读，请使用 `-t`（简略）开关。每个 `stat` 项之间用空格分隔。

```
$ stat -t orders.txt
orders.txt 21704 80 81fd 503 503 303 114674 1 6f 89 989439402
981490652 989436657
```

Linux `statfile` 命令具有与 `stat` 类似的功能，但具有更广泛的格式化选项。`statfile` 类似于 `date` 命令：它有一个字符串参数，描述状态信息应如何显示。该参数通过 `-f`（格式）开关指定。

最常见的 `statfile` 格式代码如下：

- `%c`—标准格式
- `%d`—日（零填充）
- `%D`—mm/dd/yy
- `%H`—小时（24 小时制）
- `%I`—小时（12 小时制）
- `%j`—年中的第几天（1..366）
- `%m`—月
- `%M`—分钟
- `%S`—秒
- `%U`—周数（周日为一周开始）
- `%w`—星期（周日）
- `%Y`—年
- `%%`—百分号字符
- `%_A`—使用文件最后访问时间
- `%_a`—文件名（无后缀）
- `%_C`—使用文件 inode 更改时间
- `%_d`—设备 ID
- `%_e`—自纪元以来经过的秒数
- `%_f`—文件系统类型
- `%_i`—inode 号
- `%_L`—使用当前（本地）时间





-   $i$ — 硬链接数量
-   $m$ — 使用文件最后修改时间
-   $M$ — 类型/属性/访问位
-   $n$ — 文件名
-   $R$ — Rdev ID（字符/块设备）
-   $s$ — 文件大小（字节）
-   $U$ — 使用当前（UTC）时间
-   $u$ — 用户 ID（uid）
-   $z$ — 序列号（1, 2, ……）

完整的列表显示在本章末尾的参考部分。

默认情况下，任何涉及时间的格式化代码都将基于文件的修改时间。

```bash
$ stattime -f "%c" orders.txt
Tue Feb  6 15:17:32 2001
```

通过使用时间代码，可以选择其他类型的时间。格式参数是从左到右读取的，这意味着可以在一个格式字符串中组合不同的时间代码。例如，使用 $c$ 会将格式代码更改为 inode 更改时间（通常是文件创建的时间）。使用 $L$（*本地时间*）或 $U$（*UTC 时间*）会使 `stattime` 的行为类似于 date 命令。

```bash
$ stattime -f "modified time = %c current time = %L%o" orders.txt
modified time = Tue Feb  6 15:17:32 2001 current time = Wed May
  9 15:49:01 2001
```

```bash
$ date
Wed May  9 15:49:01 2001
```

`stattime` 可以创建有意义的归档文件名。通常，文件会以诸如 `orders.txt` 这样的名称发送，而脚本希望将订单保存为包含日期作为名称一部分的文件。

```bash
$ stattime -f "a_%_a_%_L%M%d.txt" orders.txt
orders_0509.txt
```

除了生成新文件名外，`stattime` 还可以用于将文件的信息保存到变量中。

```bash
$ BYTES='stattime -f "% s" orders.txt'
$ printf "The file size is %d bytes\n" "$BYTES"
The file size is 21704 bytes
```

当通过标准输入提供文件列表时，该命令会依次处理每个文件。$z$ 代码提供文件名在列表中的位置，从 1 开始。

## 在账户之间传输文件 (wget)

Linux 提供了一个方便的工具，用于从当前计算机上的其他登录点或通过网络下载文件。*wget*（*web get*）使用 FTP 或 HTTP 获取文件。*wget* 专为获取文件而设计，使其在 Shell 脚本中易于使用。如果连接中断，*wget* 会尝试重新连接并继续下载文件。

*wget* 程序使用与 Web 浏览器相同的地址格式，支持 ftp:// 和 http:// URL。通过在主机名之前添加 *user:* 和 *password*，可以将登录信息添加到 URL 中。FTP URL 可以以可选的 ;*type*=a 或 ;*type*=i 结尾，用于 ASCII 或 IMAGE FTP 下载。例如，要在当前计算机上以密码 *jabber12* 从 *kburtch* 登录中下载 *info.txt* 文件，使用：

```bash
$ wget ftp://kburtch:jabber12@localhost/info.txt;type=i
```

默认情况下，*wget* 使用 --*verbose* 消息报告。要仅报告错误，请使用 --*quiet* 开关。要记录发生了什么，请使用 --*append-output* 和一个日志文件名将结果追加到日志文件中，并使用 --*server-response* 开关记录服务器响应。

```bash
$ wget --server-response --append-output wget.log \
 ftp://kburtch:jabber12@localhost/info.txt;type=i
```

可以使用 --*mirror* 开关复制整个账户。

```bash
$ wget --mirror ftp://kburtch:jabber12@localhost;type=i
```

为了更容易地复制一组文件，--*globopt* 开关可以启用文件模式匹配。--*globopt* on 使 *wget* 对文件名中的任何特殊字符进行模式匹配。例如，要检索所有文本文件：

```bash
$ wget --globopt on 'ftp://kburtch:jabber12@localhost/*.txt'
```

还有许多此处未涵盖的专用开关。完整的开关列表在参考部分中。*wget* 主页（http://www.gnu.org/software/wget/wget.html）上提供了文档。

## 使用 FTP 传输文件

除了 *wget* 之外，在账户之间传输文件最常见的方式是使用 ftp 命令。FTP 是一种客户端/服务器系统：如果计算机上尚未设置 FTP 服务器，则必须设置一个。大多数 Linux 发行版默认安装 FTP 服务器。

使用 FTP 客户端时，你必须使用标准输入重定向必要的下载命令，但使用 *wget* 时则不需要。

要在脚本中使用 *ftp*，你需要使用三个开关。-n（*非交互式*）开关禁用正常的 FTP 用户提示。-u（*无自动登录*）抑制登录提示，要求你使用 *open* 和 *user* 命令显式登录。-v（*详细*）显示有关传输的更多详细信息。可以使用 here file 将 ftp 命令嵌入脚本中。

```bash
ftp -i -n -v <<!
open ftp.nightlight.com
user incoming_orders password
cd linux_lightbulbs
binary
put $1
!
if [ $? -ne 0 ] ; then
	printf "%s\n" "$SCRIPT: FTP transfer failed" >&2
	exit 192
fi
```

此脚本片段打开到名为 ftp.nightlight.com 的计算机的 FTP 连接。它将文件放置在 incoming_orders 账户的 linux_lightbulbs 目录中。如果发生错误，将打印错误消息并停止脚本。

处理通过 FTP 发送的文件很困难，因为没有办法知道文件是否仍在传输中。FTP 服务器不会将文件保存到临时文件，然后移动到最终位置，而是会创建一个空文件，并缓慢地将数据保存到文件中。仅仅存在文件并不足以表明传输已完成。处理这种情况的常规方法是等待文件在合理的时间范围内（例如一小时）被修改。如果文件最近没有被修改，则传输可能已完成，文件可以安全地重命名并移动到永久目录。

某些发行版有 ftpcopy（或 ftpcp）命令，它可以一次复制整个目录。使用它时必须小心，因为它主要用作镜像工具，并且会删除本地文件中未位于远程账户中的文件。

## 使用安全 FTP (sftp) 传输文件

作为 OpenSSH（Open Secure Shell）项目的一部分，Secure FTP（sftp）是另一个以类似 FTP 的方式工作的文件传输程序，但它对传输进行加密，使其无法被中间计算机拦截或读取。加密过程会增加数据量并减慢传输速度，但为机密信息提供了保护。

必须在 sftp 命令行上指定计算机和用户账户。SFTP 会提示你输入密码。

```bash
$ sftp root@our_web_site.com:/etc/httpd/httpd.conf
Connecting to our_web_site.com...
root@our_web_site.com's password:
Fetching /etc/httpd/httpd.conf to httpd.conf
```

出于安全目的，SFTP 通常会要求用户提供 Linux 登录密码。它不请求标准输入的密码，而是请求控制终端的密码。这意味着你不能在批处理文件中包含密码。解决此问题的方法是使用 `ssh-keygen` 命令使用 SSH 公钥认证。如果你还没有这样做，请按照以下方法生成新的密钥对。

```bash
$ ssh-keygen -t rsa
```

一对认证密钥存储在用户主目录下的 `~/.ssh` 中。你必须将公钥（以 `.pub` 结尾的文件）复制到远程机器，并将其添加到名为 `~/.ssh/authorized_keys` 的文本文件中。访问远程登录的每个本地登录都需要在 `authorized_keys` 中有一个公钥。如果存在密钥对，SFTP 会自动使用密钥而不是 Linux 登录密码。

与 FTP 一样，SFTP 需要一个命令列表来执行。SFTP 包含一个 `-b`（*batch*）开关，用于指定包含要执行的命令的单独批处理文件。要在脚本中使用方便的 here file，请使用名为 `/dev/stdin` 的批处理文件。

SFTP 理解的命令与 FTP 类似。就 shell 脚本编程而言，基本传输命令是相同的。传输始终是“二进制”的。有一个 `-v`（*verbose*）开关，但它会产生大量信息。当使用 `-b` 开关时，SFTP 会显示执行的命令，因此不需要 `-v` 开关来记录传输期间发生了什么。

```bash
sftp -C -b /dev/stdin root@our_web_site.com <<!
cd /etc/httpd
get httpd.conf
!
STATUS=$?
if [ $STATUS -ne 0 ] ; then
printf "%s\n" "Error: SFTP transfer failed" >&2
exit $STATUS
fi
```

`-c`（*compress*）选项尝试压缩数据以进行更快的传输。有关 *ssh*、*sftp* 和相关程序的更多信息，请访问 http://www.openssh.org/。

## 验证文件

通过计算校验和，可以进一步检查通过 FTP 或 wget 发送的文件。Linux 的 `cksum` 命令统计文件中的字节数并打印循环冗余检查（CRC）校验和，可用于验证文件是否完整无损地到达。该命令使用符合 POSIX 的算法。

```bash
$ cksum orders.txt
491404265 21799 orders.txt
```

还有一个 Linux `sum` 命令，提供与旧版 Unix 系统的兼容性，但请注意 `cksum` 与 `sum` 不兼容。





为了获得更高的校验和安全性，某些发行版包含了`md5sum`命令来计算 MD5 校验和。`–status` 开关会静默地测试文件。`–binary`（或 `-b`）开关将文件视为二进制数据，而不是文本。`–warn` 开关会打印关于错误 MD5 格式警告信息。`–check`（或 `-c`）检查文件的校验和。

```bash
$ md5sum orders.txt
945eeccl37074a43e232730a44774004  orders.txt
$ md5sum orders.txt > orderssum.txt
$ md5sum –check orderssum.txt
file1.txt: OK
```

两个文件之间的差异可以通过 Linux 的 `cmp` 命令来精确定位。

```bash
$ cmp orders.txt orders2.txt
orders.txt orders2.txt differ: char 179, line 6
```

如果两个文件没有差异，`cmp` 不会打印任何内容。

## 拆分大文件

使用 Linux 的 `split` 命令可以将极大的文件拆分为较小的文件。文件可以按字节或按行进行拆分。`–bytes=s`（或 `–b s`）开关创建的文件不超过 *s* 字节。`–lines=s`（或 `-l s`）开关创建的文件不超过 *s* 行。`–line-bytes=s`（或 `-c s`）开关限制每行不超过 *s* 字节。大小是一个数字，可选带有 b（512 字节块）、k（千字节）或 m（兆字节）后缀。最后一个参数是新文件名使用的文件前缀。

```bash
$ split –bytes=10k huge_file.txt small_file
$ ls -l small_file*
-rw-rw-r-- 1 kburtch kburtch 10240 Aug 28 16:19 small_fileaa
-rw-rw-r-- 1 kburtch kburtch 10240 Aug 28 16:19 small_fileab
-rw-rw-r-- 1 kburtch kburtch  1319 Aug 28 16:19 small_fileac
```

你可以使用 Linux 的 `cat` 命令重新组装拆分后的文件。该命令组合文件并将其写入标准输出。务必注意按正确顺序组合拆分后的文件。

```bash
$ cksum huge_file.txt
491404265 21799  huge_file.txt
$ cat small_fileaa small_fileab small_fileac > new_file
$ cksum new_file
491404265 21799 new_file
```

如果执行拆分的区域设置与重新组装文件时的区域设置相同，则可以使用通配符匹配（wildcard globbing）作为 `cat` 的文件名是安全的。

Linux 的 `csplit`（*上下文拆分*）命令在特定模式出现的位置拆分文件。

`csplit` 的基本模式是以斜杠包围的正则表达式，后跟可选的偏移量。该正则表达式表示将成为下一个新文件第一行的行。偏移量表示从匹配行向前或向后移动的行数，默认为零。模式 `*/\d\cg/\+\*` 将文件拆分为两个较小的文件，第一个文件以模式 `\d\cg` 的第一次出现结束。

对模式进行引用可以防止其被 Bash 解释，而不是由 `csplit` 命令解释。

`-prefix=R`（或 `-f P`）开关设置新文件名的前缀。`-suffix=S`（或 `-b S`）使用指定的 C printf 函数代码写入文件编号。`-digits=D`（或 `-n D`）开关指定文件编号的最大位数。默认值为两位数字。

```bash
$ csplit -prefix "chairs" orders.txt "/Chair/"   
107   
485   
$ ls -l chairs*
-rw-rw-r--   1 kburcht  kburcht   107 Oct  1 15:33 chairs00
-rw-rw-r--   1 kburcht  kburcht   485 Oct  1 15:33 chairs01
$ head -1 chairs01
Reclining Chair,1599.99,1,757  
```

模式 `Chair` 的第一次出现是在 `Reclining Chair` 行中。可以列出多个模式。用百分号（`%`）而不是斜杠分隔的模式表示应忽略文件的一部分，直到指示的模式为止。它也可以有偏移量。单独的数字表示该特定行开始下一个新文件。花括号内的数字重复最后一次模式特定次数，或者星号匹配模式的所有出现。

要将 `orders.txt` 文件拆分为独立的文件，每个文件都以单词 `Chair` 开头，请使用所有出现模式。

```bash
$ csplit -prefix "chairs" orders.txt "/Chair/*" "(* *)"
107   
222   
23    
179   
61    
$ ls -l chairs*
-rw-rw-r--   1 kburcht  kburcht   107 Oct  1 15:37 chairs00
-rw-rw-r--   1 kburcht  kburcht   222 Oct  1 15:37 chairs01
-rw-rw-r--   1 kburcht  kburcht   23  Oct  1 15:37 chairs02
-rw-rw-r--   1 kburcht  kburcht   179 Oct  1 15:37 chairs03
-rw-rw-r--   1 kburcht  kburcht   61  Oct  1 15:37 chairs04
```

`-elide-empty-files`（或 `-z`）开关不会保存空文件。`-keep-files`（或 `-k`）在发生错误时不会删除生成的文件。`-quiet`（或 `-silent` 或 `-q` 或 `-B`）开关隐藏进度信息。

`csplit` 在拆分包含重复信息的大文件时很有用，例如将客户发送的单个订单提取为单个文本文件。

## 制表符和空格

Linux expand 命令将制表符字符转换为空格。默认是八个空格，但你可以通过 -tabs=n（或 -t n）将其更改为 n 个空格。-tabs 开关也可以使用逗号分隔的制表位列表。

```bash
$ printf '\tA\tTEST\n' > test.txt
$ wc test.txt
        1       2       8 test.txt
$ expand test.txt | wc
        1       2      21
```

-initial（或 -i）开关仅转换一行之前的制表符。

```bash
$ expand -initial test.txt | wc
        1       2      15
```

对应的 unexpand 命令将多个空格转换回制表符。默认是八个空格对应一个制表符，但你可以使用 -tabs=n 开关更改此设置。默认情况下，仅转换初始制表符。使用 -all（或 -a）开关将考虑一行的所有空格。

在处理文件之前，使用 expand 移除文件中的制表符。

## 临时文件

临时文件，即仅在脚本执行期间存在的文件，传统上使用 $$ 函数命名。该函数返回当前脚本的进程 ID 号。通过在临时文件的名称中包含此数字，使每次运行脚本时文件名都是唯一的。

```bash
$ TMP="/tmp/reports.$$"
$ printf '%s\n' "$TMP"
/tmp/reports.20629
$ touch "$TMP"
```

这种传统方法的缺点在于临时文件的名称是可以预测的。恶意程序在你的脚本运行时可以看到其进程 ID，并利用这些信息识别你的脚本正在使用哪些临时文件。临时文件可能被删除或数据被替换，以改变你的脚本的行为。

为了获得更好的安全性，或创建多个具有唯一名称的文件，Linux 提供了 mktemp 命令。该命令创建一个临时文件，并将名称打印到标准输出，以便可以存储在变量中。每次 mktemp 创建新文件时，文件都会被赋予唯一的名称。名称由程序提供的文件名模板生成，该模板以字母 X 结尾，重复六次。mktemp 用唯一的随机代码替换这六个字母以创建新的文件名。

```bash
$ TMP=`mktemp /tmp/reports.XXXXXX`
$ printf "%s\n" "$TMP"
/tmp/reports.3LnWVw
$ ls -1 "$TMP"
-rw---- 1 kburcch kburcch    0 Aug  1 14:34 reports.3LnWVw
```

在这种情况下，字母 XXXXXX 被代码 3LnWVw 替换。

`mktemp` 使用 `-d (directories)` 开关创建临时目录。你可以使用 `-q (quiet)` 开关抑制错误消息。

## 锁定文件

当许多脚本共享相同的文件时，需要一种方法让一个脚本向另一个脚本表明它已完成其工作。这种情况通常发生在由两个不同开发团队监督的脚本需要共享文件时，或者共享文件在同一时间只能被一个脚本使用时。

同步脚本的一种简单方法是使用锁定文件。*锁定文件* 类似于标志变量：文件的存在表示某种条件，在这种情况下，表示该文件正被其他程序使用，不应被修改。

大多数 Linux 发行版包含一个名为 `/var/lock` 的目录，这是放置锁定文件的标准位置。

假设发票文件在同一时间只能被一个脚本访问。可以创建一个名为 `invoices_lock` 的锁定文件，以确保只有一个脚本具有访问权限。

```bash
declare -r INVOICES_LOCKFILE="/var/lock/invoices_lock"
while test ! -f "$INVOICES_LOCKFILE" ; do
   printf "Waiting for invoices to be printed...\n"
   sleep 10
done
touch "$INVOICES_LOCKFILE"
```

此脚本片段每 10 秒检查一次 `invoices_lock` 是否存在。当文件消失时，循环完成，脚本创建一个新的锁定文件并继续进行工作。当工作完成后，脚本应移除锁定文件，以允许其他脚本继续进行。

如果一个脚本完成时未移除锁定文件，会导致下一个脚本无限循环。可以修改 `while` 循环以使用超时，这样如果一段时间后发票文件无法访问，脚本将停止并报错。

```bash
declare -r INVOICES_LOCKFILE="/var/lock/invoices_lock"
declare -ir INVOICES_TIMEOUT=1800    # 30 minutes
TIME=$(date +%s)
TIME_STARTED=$TIME
time_out=0
while test ! -f "$INVOICES_LOCKFILE" ; do
   printf "Waiting for the invoices to be printed...\n"
```




## 命名管道

当少数脚本共享同一个文件时，锁定文件非常方便。当太多脚本都在等待锁定文件时，就会发生*竞态条件*：计算机花费大量时间仅仅是在检查锁定文件是否存在，而不是做有用的工作。幸运的是，还有其他共享信息的方式。

两个脚本可以使用一种称为*命名管道*的特殊类型文件来共享数据。这些管道（也称为 FIFO 或队列）是文件，一个脚本可以读取它，同时另一个脚本可以写入它。其效果类似于管道运算符 (|)，该运算符将一个命令的结果作为另一个命令的输入转发。与 shell 管道不同，使用命名管道的脚本相互独立运行，它们之间仅共享管道文件。不需要锁定文件。

`mkfifo` 命令创建一个新的命名管道。

```
$ mkfifo website_orders.fifo
$ ls -l website_orders.fifo
prw-rw-r-- 1 khurcht khurcht 0 May 22 14:14 orders.fifo
```

`ls` 输出左侧的文件类型 `p` 表示这是一个命名管道。如果使用 `ls` 的文件名类型选项 (-F)，则文件名后面会跟一个竖线 (|) 以表示管道。

命名管道可以像常规文件一样被读取。例如，假设你想创建一个脚本来记录来自公司网站的新订单，如列表 11.5 所示。

**列表 11.5: do_web_orders.sh**

```bash
#!/bin/bash
#
# do_web_orders.sh: 读取订单列表并显示读取日期

declare -rx SCRIPT=${0##*/}
declare -rx QUEUE="website_orders.fifo"
declare DATE
declare ORDER

if test ! -r "$QUEUE" ; then
	 printf "%s\n" "$SCRIPT: $LINENO: 命名管道缺失或不可读" >&2
	 exit 192
fi

{
	 while read ORDER ; do
		 DATE=date
		 printf "%s : %s\n" "$DATE" "$ORDER"
	done
} < $QUEUE

printf "程序完成"
exit 0
```

在此示例中，管道内容逐行读取，就像它只是一个常规文件一样。

当脚本从管道读取数据且没有数据可用时，它会休眠（或阻塞），直到有更多数据可用。如果写入管道的程序完成，读取管道的脚本会将此视为文件结束。while 循环将完成，脚本将在循环后继续执行。

要通过管道发送订单，必须将它们打印出来或以其他重定向方式写入管道。要模拟一系列订单，可以使用 cat 命令将订单文件写入命名管道。即使 cat 命令在后台运行，它也会继续向命名管道写入订单，直到脚本读取完所有行。

```
$ cat orders.txt > website_orders.fifo &
$ sh do_web_orders.sh
Tue May 22 14:23:00 EDT 2001: Birchwood China Hutch,475.99,1,756
Tue May 22 14:23:00 EDT 2001: Bookcase Oak Veneer,205.99,1,756
Tue May 22 14:23:00 EDT 2001: Small Bookcase Oak Veneer,205.99,1,756
Tue May 22 14:23:00 EDT 2001: Reclining Chair,1599.99,1,757
Tue May 22 14:23:00 EDT 2001: Bunk Bed,705.99,1,757
Tue May 22 14:23:00 EDT 2001: Queen Bed,925.99,1,757
Tue May 22 14:23:00 EDT 2001: Two-drawer Nightstand,125.99,1,756
Tue May 22 14:23:00 EDT 2001: Cedar Toy Chest,65.99,1,757
Tue May 22 14:23:00 EDT 2001: Six-drawer Dresser,525.99,1,757
Tue May 22 14:23:00 EDT 2001: Pine Round Table,375.99,1,757
Tue May 22 14:23:00 EDT 2001: Bar Stool,45.99,1,756
Tue May 22 14:23:00 EDT 2001: Lawn Chair,55.99,1,756
```

使用 `tee`，一个程序可以同时向两个或更多命名管道写入。

由于命名管道不是常规文件，诸如 `grep`、`head` 或 `tail` 等命令可能会表现异常或无限期阻塞，等待管道上出现或完成信息。如有疑问，请在这些命令使用前验证该文件不是管道。

## 进程替换

有时，竖线管道运算符无法用于将一系列命令连接在一起。当管道中的某个命令不使用标准输入，或者它使用两个输入源时，无法形成管道。要在普通管道不起作用时创建管道，Bash 使用一种称为*进程替换*的特殊功能。

当命令被包含在 `<(...)` 中时，Bash 在子 shell 中单独运行该命令，将结果重定向到一个临时命名管道，而不是标准输入。Bash 用包含命令结果的命名管道文件的名称替代该命令。

进程替换可以通常使用文件名的任何地方使用。例如，Linux 的 `grep` 命令，一个文件搜索命令，可以搜索文件中的字符串列表。可以使用临时文件搜索日志文件中对当前目录中文件的引用。

```
$ ls -1 > temp.txt
$ grep -f temp.txt /var/log/nightrun_log.txt
Wed Aug 29 14:18:38 EDT 2001 invoice_error.txt deleted
$ rm temp.txt
```

因为文件列表是从 `temp.txt` 读取的，而不是标准输入，所以无法使用管道来组合这些命令。然而，可以使用进程替换代替临时文件名，将这两个命令重写为一个命令。

```
$ grep -f <(ls -1) /var/log/nightrun_log.txt
Wed Aug 29 14:18:38 EDT 2001 invoice_error.txt deleted
```

在这种情况下，`ls -1` 的结果被写入一个临时管道。`grep` 从管道读取文件列表，并将其与 `nightrun_log.txt` 文件的内容进行匹配。Bash 用临时管道的名称替代 `ls` 命令这一事实可以通过 `printf` 语句检查。

```
$ printf "%s\n" <(ls -1)
/dev/fd/63
```

Bash 将 `-f <(ls -1)` 替换为 `-f /dev/fd/63`。在这种情况下，管道被打开为文件描述符 `63`。左尖括号 `<` 表示使用它的命令读取该临时文件。同样，右尖括号 `>` 表示临时管道是被写入而不是被读取。

## 打开文件

文件可以通过将内容管道到命令，或将文件重定向为命令或命令组的标准输入来读取。这是查看文本文件内容的最简单方法，但它有两个缺点。首先，一次只能检查一个文件。其次，它阻止脚本与用户交互，因为 `read` 命令从重定向的文件而不是键盘读取。

代替管道或重定向，可以使用 `exec` 命令将文件重定向到描述符号来打开文件以读取，如列表 11.6 所示。

**列表 11.6: open_file.sh**

```bash
#!/bin/bash
#
# open_file.sh: 打印 orders.txt 的内容

shopt -s -o unset

declare LINE

exec 3 < orders.txt
while read LINE <&3 ; do
 printf "%s\n" "$LINE"
done
exit 0
```

在这种情况下，文件 `orders.txt` 被重定向到文件描述符 3。描述符 3 是程序通常可以使用的最低编号。文件描述符 0 是标准输入，文件描述符 1 是标准输出，文件描述符 2 是标准错误。

`read` 命令从描述符 3（`orders.txt`）接收输入，该输入正被 `<&` 重定向。`read` 也可以使用 Korn shell 的 `-u` 开关从特定的文件描述符读取。

如果用 `exec` 打开的文件不存在，Bash 会报告一个 `bad file number` 错误。文件描述符也必须是一个字面数字，而不是变量。

如果不使用 `exec`，文件描述符仍然可以打开，但不能重新分配。

```
3< orders.txt
3< orders2.txt
```



在本例中，文件描述符 3 指向 *orders*.txt。第二行不起作用，因为描述符 3 已经打开。如果使用 *exec*，第二行会将描述符 3 重新打开为 *orders2*.txt。

为了节省文件描述符，*exec* 可以将一个描述符复制到另一个描述符。若要使输入文件描述符 4 指向与文件描述符 3 相同的文件，请执行以下操作：

```
exec 4<&3
```

现在，描述符 3 和 4 指向同一文件，可以互换使用。描述符 3 可以用来打开另一个文件，并通过从描述符 4 复制回来将其恢复为原始值。如果省略描述符 4，Bash 假设你想更改标准输入（描述符 0）。

你可以通过在文件描述符后添加减号来移动它。这会在描述符被复制后关闭原始文件。

```
exec 4<&3-
```

类似地，你可以使用 *>&* 复制输出文件描述符，并通过添加减号来移动它们。默认输出是标准输出（描述符 1）。

要打开文件以进行写入，请使用输出重定向符号 *(&)*。

```
exec 3>orders.txt
exec 4>&3
while read LINE <&3 ; do
    printf "${A}n\" "$LINE" >&4
done
```

*<&* 符号用于以读写模式打开文件。

```
exec 3<>orders.txt
```

读取或写入将从文件开头顺序进行。向文件写入会覆盖其内容。只要被覆盖的字符长度与原始字符相同，新字符就会替换旧字符。例如，如果文件中的下一行是 *dog*，写入 *cat* 覆盖 *dog* 会替换单词 *dog*。然而，如果文件中的下一行是 *horse*，写入 *cat* 会产生两行——*cat* 行和 *se* 行。*cat* 后面的换行符会覆盖字母 *r*。脚本现在将读取 *se* 这一行。

*<&* 在常规文件中的实用性有限，因为没有办法“回退”并重写刚刚读取的内容。你只能覆盖即将读取的内容。

列表 11.7 中的脚本读取整个文件，并在文件末尾添加“*Processed* on”消息。

### 列表 11.7 open_files2.sh

```bash
#!/bin/bash
#
# open_files2.sh

shopt -o -S nounset

declare LINE

exec 3>orders.txt
while read LINE <&3 ; do
    printf "%s\n" "$LINE"
done
printf "\n" "Processed on "'date' >&3
exit 0
```

`<>` 对于套接字编程特别有用，这在第 16 章“网络编程”中有讨论。

文件可以被打开，也可以被关闭。输入文件描述符可以用 `<&-` 关闭。请务必包含一个文件描述符，否则这将关闭标准输入。输出文件描述符可以用 `>&-` 关闭。如果没有指定描述符，这将关闭标准输出。

作为一种特殊的 Bash 约定，文件描述符可以通过路径名引用。形式为 `/dev/fd/n` 的路径指的是文件描述符 `n`。例如，标准输出是 `/dev/fd/1`。使用此语法，可以在运行 Linux 命令时引用已打开的文件描述符。

```bash
$ exec 4>results.out
$ printf "\n" "Send to fd 4 and standard out" | tee /dev/fd/4
Send to fd 4 and standard out
$ exec 4>&-
$ cat results.out
Send to fd 4 and standard out
```

## 使用 head 和 tail

Linux `head` 命令返回文件中的前几行。默认情况下，`head` 打印前 10 行。你可以使用 `-lines=n`（或 `-n n`）开关指定行数。

```bash
$ head -lines=5 orders.txt
Birchwood China Hutch, 475, 99, 1, 756
Bookcase Oak Veneer, 205, 99, 1, 756
Small Bookcase Oak Veneer,205.99,1,756
Reclining Chair,1599.99,1,757
Bunk Bed,705.99,1,757
```

你可以将 `-lines` 开关缩写为一个减号和行数。

```bash
$ head -3 orders.txt
Birchwood China Hutch,475.99,1,756
Bookcase Oak Veneer,205.99,1,756
Small Bookcase Oak Veneer,205.99,1,756
```

行数后可以使用 c 表示字符，l 表示行数，k 表示千字节，或 m 表示兆字节。`-bytes`（或 `-c`）开关打印你指定的字节数。

```bash
$ head -9c orders.txt
Birchwood
$ head -bytes=9 orders.txt
Birchwood
```

Linux `tail` 命令显示文件中的最后几行。与 `head` 类似，行数或字节数后可以使用 c 表示字符，l 表示行数，k 表示千字节，或 m 表示兆字节。

开关与 `head` 命令类似。`-bytes=n`（或 `-c`）开关打印你指定的字节数。`-lines=n`（或 `-n`）开关打印你指定的行数。

```bash
$ tail -3 orders.txt
Walnut TV Stand,388.99,1,756
Victorian-style Sofa,1225.99,1,757
Grandfather Clock,2045.99,1,756
```

结合使用管道中的 `tail` 和 `head`，你可以显示任何一行或行范围。

```bash
$ head -5 orders.txt | tail -1
Bunk Bed,705.99,1,757
```

如果起始行使用的是加号而不是减号，`tail` 会从文件开头计数该数量的行并打印剩余部分。这是 `tail` 的一个特性，而不是 `head` 命令的特性。

```bash
$ tail +17 orders.txt
Walnut TV Stand,388.99,1,756
Victorian-style Sofa,1225.99,1,757
Grandfather Clock,2045.99,1,756
```

在脚本中对任意文件使用 `head` 或 `tail` 时，请务必检查文件是否为常规文件，以避免令人不快的意外情况。

## 文件统计信息

Linux `wc`（单词计数）命令提供关于文件的统计信息。默认情况下，`wc` 显示文件的行数、单词数和字符数。要使 `wc` 在脚本中有用，必须使用开关来返回单个统计值。

`-bytes`（或 `-c` 或 `-C`）开关返回文件大小，其值与 `stat -fsize` 返回的文件大小相同。

```bash
$ wc -bytes invoices.txt
20411 invoices.txt
```

要在脚本中使用 `wc`，请将文件通过标准输入传入，以抑制文件名的显示。

```bash
$ wc -bytes < status_log.txt
57496
```

`-lines`（或 `-l`）开关返回文件中的行数。也就是说，它统计换行符的数量。

```bash
$ wc -lines < status_log.txt
1569
```

`-max-line-length`（或 `-L`）开关返回最长行的长度。`-words`（或 `-w`）开关统计文件中的单词数。

当变量值被打印到管道中时，可以将 `wc` 与变量一起使用。

```bash
$ declare -r TITLE='Annual Grain Yield Report'
$ printf "%s\n" "$TITLE" | wc -words
4
```

## 截取

Linux `cut` 命令从文件中所有行中删除子字符串。

`-fields`（或 `-f`）开关打印由特定字符标记的行的一部分。`-delimiter`（或 `-d`）开关选择该字符。如果要使用空格作为分隔符，必须用反斜杠转义或将其括在引号中。

```bash
$ declare -r TITLE='Annual Grain Yield Report'
$ printf "%s\n" "$TITLE" | cut -d ' ' -f2
Grain
```

在本例中，分隔符是空格，由空格标记的第二个字段是 `Grain`。在使用 `printf` 进行截取时，请务必确保打印了换行符；否则，`cut` 将返回空字符串。

多个字段用逗号表示，范围表示为用减号 (-) 分隔的两个数字。

```bash
$ printf "%s\n" "$TITLE" | cut -d ' ' -f 2,4
Grain Report
```

使用分隔符字符分隔多个字段。要在显示结果时使用不同的分隔符字符，请使用 `-output-delimiter` 开关。

`-characters`（或 `-c`）开关打印指定字符的位置。这与美元符号表达式子字符串类似，但可以指定任何字符或字符范围。`-bytes`（或 `-b`）开关作用相同，但旨在为多字节国际字符提供未来的支持。

```bash
$ printf "%s\n" "$TITLE" | cut -characters 1,3,6-8
Anl G
```

`-only-delimited`（或 `-s`）开关忽略不包含分隔符字符的行。这是跳过数据文件开头的标题或其他注释的一种简单方法。

用于多行时，`cut` 会截取每一行。

```bash
$ cut -d, -f1 < orders.txt | head -3
Birchwood China Hutch
Bookcase Oak Veneer
Small Bookcase Oak Veneer
```

列表 11.8 中的脚本将 `orders.txt` 中的数量字段相加。

### 列表 11.8 cut_demo.sh

```bash
#!/bin/bash
#
# cut_demo.sh: compute the total quantity from orders.txt

shopt -o -s nounset

declare -i QTY
declare -ix TOTAL_QTY=0

cut -d, -f3 orders.txt | {
  while read QTY ; do
    TOTAL_QTY=TOTAL_QTY+QTY
  done

  printf "The total quantity is %d\n" "$TOTAL_QTY"
}
exit 0
```

## 粘贴

Linux `paste` 命令将两个或多个文件中的行合并为一行。对于两个文件，`paste` 将第一个文件的第一行、一个制表符字符以及第二个文件的第一行写入标准输出，然后继续处理第二行



直到所有行都被写完为止。如果一个文件比另一个文件短，缺失的行将使用空白行来填充。

`–delimiters (–d)` 开关是一个由一个或多个分隔符组成的列表，用于替代制表符（Tab）。如果 `paste` 命令需要的分隔符数量多于列表中提供的数量，它会循环使用该列表，如清单 11.9 所示。

### 清单 11.9 two\_columns.sh

```bash
#!/bin/bash
#
# two\_columns.sh

shopt -s -O nounset

declare -r ORDERS="orders.txt"
declare -r COLUMN1="column1.txt"
declare -r COLUMN2="column2.txt"
declare -i LINES

LINES=`wc -l < "$ORDERS"`
LINES=LINES/2

head -SLINES < "$ORDERS" > "$COLUMN1"

LINES=LINES+1
tail +$LINES < "$ORDERS" > "$COLUMN2"

paste -delimiters="|" "$COLUMN1" "$COLUMN2"

rm $COLUMN1
rm $COLUMN2
exit 0
```

运行此脚本后，`orders.txt` 的内容会被分隔成两列，由垂直线界定。

```bash
$ sh two_columns.sh

Birchwood China Hutch,475.99,1,756|Bar Stool,45.99,1,756
Bookcase Oak Veneer,205.99,1,756|Lawn Chair,55.99,1,756
Small Bookcase Oak Veneer,205.99,1,756|Rocking Chair,287.99,1,756
Reclining Chair,1599.99,1,757|Cedar Armoire,825.99,1,757
Bunk Bed,705.99,1,757|Mahogany Writing Desk,463.99,1,756
Queen Bed,925.99,1,757|Garden Bench,149.99,1,757
Two-drawer Nightstand,125.99,1,756|Walnut TV Stand,388.99,1,756
Cedar Toy Chest,65.99,1,757|Victorian-style Sofa,1225.99,1,757
Six-drawer Dresser,525.99,1,757|Chair - Rocking,287.99,1,757
Pine Round Table,375.99,1,757|Grandfather Clock,2045.99,1,756
```

假设你有一个名为 `order1.txt` 的文件，其中包含从 `orders.txt` 中分离出来的项目，字段在单行中以列表形式分隔。

```text
Birchwood China Hutch
475.99
1
756
```

`paste` 的 `--serial (-s)` 开关将每个文件的所有行粘贴到一个条目中，而不是逐个地将每个文件的一行合并到一行中。此开关将分散的字段重新组合成单行。

```bash
$ paste -serial -delimiter="" order1.txt
Birchwood China Hutch,475.99,1,756
```

要合并两个或多个文件的行，使这些行依次排列，请在使用 `-m` 开关时使用 `sort` 命令。

## 列

使用 `paste` 命令创建的列并不适用于所有场景。为了美观的显示效果，Linux 的 `column` 命令可以创建固定宽度的列。列的大小会根据 `COLUMNS` 环境变量确定的屏幕大小进行适配，或者使用 `-c` 开关适配特定的行宽。

```bash
$ column < orders.txt
Birchwood China Hutch,475.99,1,756     Bar Stool,45.99,1,756
Bookcase Oak Veneer,205.99,1,756      Lawn Chair,55.99,1,756
Small Bookcase Oak Veneer,205.99,1,756 Rocking Chair,287.99,1,757
Reclining Chair,1599.99,1,757         Cedar Armoire,825.99,1,757
Bunk Bed,705.99,1,757                Mahogany Writing Desk,463.99,1,756
Queen Bed,925.99,1,757                Garden Bench,149.99,1,757
Two-drawer Nightstand,125.99,1,756    Walnut TV Stand,388.99,1,756
Cedar Toy Chest,65.99,1,757           Victorian-style Sofa,1225.99,1,757
Six-drawer Dresser,525.99,1,757       Chair - Rocking,287.99,1,757
Pine Round Table,375.99,1,757         Grandfather Clock,2045.99,1,756
```

`-t` 开关通过由 `-s` 开关指定的字符分隔的条目创建表格。

```bash
$ column -s ', ' -t < orders.txt | head -5
Birchwood China Hutch        475.99  1  756
Bookcase Oak Veneer          205.99  1  756
Small Bookcase Oak Veneer    205.99  1  756
Reclining Chair             1599.99  1  757
Bunk Bed                     705.99  1  757
```

表格的填充顺序可以使用 `-x` 开关进行调换。

## 折叠

Linux 的 `fold` 命令确保一行不超过特定的字符数。如果一行过长，会插入回车符。`fold` 默认在 80 个字符处换行，但可以使用 `-width=n`（或 `-w`）开关在任何字符处进行折叠。`-spaces`（或 `-s`）开关会在最近的空间处折叠以保留单词。`-bytes`（或 `-b`）开关将制表符计为一个字符，而不是将其展开。

```bash
$ head -3 orders.txt | cut -d, -f 1
Birchwood China Hutch
Bookcase Oak Veneer
Small Bookcase Oak Veneer
$ head -3 orders.txt | cut -d, -f 1 | fold -width=10
Birchwood
China Hutch
h
Bookcase O
ak Veneer
Small Book
case Oak V
eneer
$ head -3 orders.txt | cut -d, -f 1 | fold -width=10 -spaces
Birchwood
China
Hutch
Bookcase
Oak Veneer
Small
Bookcase
Oak Veneer
```

## 连接

Linux 的 `join` 命令将两个文件合并在一起。`join` 每次检查每个文件的一行。如果行的某个段匹配，它们将被合并为一行。相同段只输出一个实例。假设文件已按相同顺序排序。

行段（或字段）是通过三个开关选择的。`-1` 开关选择第一个文件的字段号。`-2` 开关选择第二个文件的字段号。`-t` 开关指定分隔一个字段和另一个字段的那个字符。如果使用这些开关，`join` 会按空格分隔字段，并检查每行的第一个字段。

假设 `orders.txt` 文件中的数据被分成两个文件，一个包含定价信息（`orders1.txt`），另一个包含数量和账户信息（`orders2.txt`）。

要合并这两个文件，使用逗号作为字段分隔符，并将第一个文件的第 1 个字段与第二个文件的第 1 个字段进行比较。

```bash
$ join -1 1 -2 1 -t, orders1.txt orders2.txt
Birchwood China Hutch,475.99,1,756
Bookcase Oak Veneer,205.99,1,756
Small Bookcase Oak Veneer,205.99,1,756
Reclining Chair,1599.99,1,757
Bunk Bed,705.99,1,757
```

如果任一文件包含具有唯一字段的行，该字段将被丢弃。只有当两个文件中都找到匹配字段时，行才会被连接。要打印未配对的行，使用 `-a 1` 打印第一个文件中的唯一行，或使用 `-a 2` 打印第二个文件中的唯一行。这些行将按照它们在文件中出现的顺序打印。

匹配的方向可以使用 `-v` 开关反转。`-v 1` 打印第一个文件中的唯一行，`-v 2` 打印第二个文件中的唯一行。

当使用 `-ignore-case`（或 `-i`）开关时，测试是不区分大小写的。

可以使用 `-o`（output）开关重新排列字段。使用逗号分隔的字段列表来指定字段顺序。字段通过文件编号（1 或 2）、一个点号以及该文件中的字段号来指定。零是连接字段的简写形式。

```bash
$ join -1 1 -2 1 -t, -o '1.2,2.3,2.2,0' orders1.txt orders2.txt
475.99,756,1,Birchwood China Hutch
205.99,756,1,Bookcase Oak Veneer
205.99,756,1,Small Bookcase Oak Veneer
1599.99,757,1,Reclining Chair
705.99,757,1,Bunk Bed
```

## 合并

`merge` 命令执行三方文件合并。这通常用于合并来自两个不同源对同一个文件的修改。合并是按行进行的。如果存在冲突的修改，`merge` 会显示警告。

为了便于阅读，可以使用 `-L (label)` 开关为文件指定标题，而不是使用文件名来报告冲突。此开关可以重复使用三次，分别对应三个文件。

例如，假设有三组冰淇淋订单。原始订单集（`file1.txt`）如下所示：

```text
1 quart vanilla
2 quart chocolate
```

这些订单已被两个人修改。Barrie 商店现在有（`file2.txt`）以下内容：

```text
1 quart vanilla
1 quart strawberry
2 quart chocolate
```

而 Orillia（`file3.txt`）如下所示：

```text
1 quart vanilla
2 quart chocolate
4 quart butter almond
```

`merge` 命令将这三个文件重新组合成一个文件。

```bash
$ merge -L "Barrie Store" -L "Original Orders" -L "Orillia Store" file2.txt
file1.txt file3.txt
```

`file1.txt file3.txt` 将修改 `file2.txt`，使其包含：

```text
1 quart vanilla
1 quart strawberry
2 quart chocolate
4 quart butter almond
```

然而，如果 *butter almond* 和 *strawberry* 订单都被添加为第三行，`merge` 会报告冲突：

```bash
$ merge -L "Barrie Store" -L "Original Orders" -L "Orillia Store" file2.txt
file1.txt file3.txt
merge: warning: conflicts during merge
```

`file2.txt` 将包含冲突的详细信息：

```text
««««« Barrie Store
1 quart strawberry
=======
4 quart butter almond
>>>>>>> Orillia Store
```

如果没有合并问题，`merge` 返回零退出状态。

`-q (quiet)` 开关抑制冲突警告。`-p (print)` 将输出写入标准输出，而不是覆盖原始文件。`-3` 开关以 `diff3 -A` 格式报告冲突。





## 参考章节

### type 命令选项
- `-a`—显示命令的所有位置
- `-p`—显示命令的路径名
- `-t`—指示命令的类型

### file 命令选项
- `-b`—简要模式
- `-c`—显示魔术文件输出
- `-f file`—从 *file* 读取要处理的文件列表
- `-i`—显示 MIME 类型
- `-L`—跟随符号链接
- `-m list`—以冒号分隔的魔术文件列表
- `-n`—在每个文件处理后刷新输出
- `-p`—允许块或字符特殊文件
- `-v`—版本
- `-z`—检查压缩文件

### stat 命令选项
- `-l`—显示关于链接的信息
- `-f`—显示关于文件所在文件系统的信息

### stat ftime 命令格式代码
- `%%`—百分号字符
- `%_A`—使用文件最后访问时间
- `%_a`—文件名（不含后缀）
- `%_C`—使用文件 inode 变更时间
- `%_d`—设备 ID
- `%_E`—自纪元以来经过的秒数
- `%_f`—文件系统类型
- `%_g`—组 ID (gid) 号
- `%h`—路径的三位哈希码
- `%i`—Inode 号
- `%l`—使用当前（本地）时间
- `%n`—硬链接数
- `%M`—使用文件最后修改时间
- `%m`—类型/属性/访问位
- `%N`—文件名
- `%R`—Rdev ID（字符/块设备）
- `%s`—文件大小（字节）
- `%t`—使用当前（UTC）时间
- `%u`—用户 ID (uid)
- `%z`—序列号 (1,2,...)
- `%A`—完整的星期名称
- `%a`—缩写星期名称
- `%B`—完整的月份名称
- `%b`—缩写月份名称
- `%C`—世纪数字
- `%c`—标准格式
- `%D`—mm/dd/yy
- `%d`—日期（零填充）
- `%e`—日期（空格填充）
- `%H`—小时（24小时制）
- `%I`—小时（12小时制）
- `%j`—天数 (1...366)
- `%M`—分钟
- `%m`—月份
- `%n`—换行（新行）字符
- `%p`—am/pm
- `%P`—AM/PM
- `%r`—hh:mm:ss AM/PM
- `%s`—秒
- `%T`—hh:mm:ss (24小时制)
- `%t`—制表符字符
- `%U`—周数（周日开始）
- `%V`—周数（周一开始）
- `%w`—星期几（0为周日）
- `%X`—当前日期
- `%Y`—年份
- `%y`—年份（两位数）
- `%Z`—时区

### wget 命令选项
- `--accept L` (或 `-A list`)—逗号分隔的后缀和模式列表，用于接受
- `--append-output log` (或 `-a log`)—类似于 `-output-file`，但是追加而不是覆盖
- `--background` (或 `-b`)—在后台运行，就像使用 `&` 启动一样
- `--continue` (或 `-c`)—恢复已终止的下载
- `--cache=0` (或 `-C 0`)—在“关闭”时不返回缓存的网页
- `--convert-links` (或 `-k`)—转换文档链接以反映本地目录
- `--cut-dirs=N`—忽略 URL 路径名中的前 `N` 个目录
- `--delete-after`—删除已下载的文件以“预加载”缓存服务器
- `--directory-prefix=P` (或 `-P P`)—将文件保存在 `P` 下，而不是当前目录
- `--domains list` (或 `-D list`)—仅接受给定的主机域名
- `--dot-style=S`—进度信息可以显示为 `default`、`binary`、`computer`、`mega` 或 `micro`
- `--exclude-directories=list` (或 `-X list`)—下载时要拒绝的目录
- `--exclude-domains list`—拒绝给定的主机域名
- `--execute cmd` (或 `-e cmd`)—运行资源文件命令
- `--follow-ftp`—下载 HTML 文档中的 FTP 链接
- `--force-directories` (或 `-x`)—保存文件时始终为主机名创建目录
- `--force-html` (或 `-H`)—即使 `-input-file` 看起来不像，也将其视为 HTML 文档
- `--glob=0` (或 `-g 0`)—在“开启”时允许 FTP URL 文件名中的文件通配符
- `--header=H`—指定要发送到 Web 服务器的 HTTP 头
- `--http-passwd=P`—指定密码（而不是在 URL 中）
- `--http-user=U`—指定用户名（而不是在 URL 中）
- `--ignore-length`—忽略 Web 服务器返回的错误文档长度
- `--include-directories=list` (或 `-I list`)—下载时要接受的目录
- `--input-file=R` (或 `-i R`)—从给定文件读取要获取的 URL；它可以是 HTML 文档
- `--level=D` (或 `-l D`)—最大递归级别（默认为 5）
- `--mirror` (或 `-m`)—启用递归、无限级别、时间戳，并保持一个 `.listing` 文件
- `--no-clobber` (或 `-nc`)—不替换现有文件
- `--no-directories` (或 `-nd`)—将所有文件保存在当前目录
- `--no-host-directories` (或 `-nh`)—从不为主机名创建目录
- `--no-host-lookup` (或 `-nl`)—禁用大多数主机的 DNS 查找
- `--no-parent` (或 `-np`)—仅检索父目录以下的文件
- `--non-verbose` (或 `-nv`)—显示一些进度信息，但不是全部
- `--output-document=P` (或 `-O P`)—创建一个包含所有文件的 *P* 文件；如果是 `-`，则所有文件都写入标准输出
- `--output-file log` (或 `-o log`)—将所有错误消息记录到给定文件
- `--passive-ftp`—使用“被动”检索，当 wget 在防火墙后面时很有用
- `--proxy=O` (或 `-x O`)—将代理支持设置为“开”或“关”
- `--proxy-passwd=P`—指定代理服务器的密码
- `--proxy-user=U`—指定代理服务器的用户名
- `--quiet` (或 `-q`)—抑制进度信息
- `--quota=Q` (或 `-Q Q`)—当当前文件超过 Q 字节时停止下载；也可以指定 *k* 千字节或 *m* 兆字节；*inf* 禁用配额
- `--recursive` (或 `-r`)—递归获取
- `--reject L` (或 `-R L`)—逗号分隔的后缀和模式列表，用于拒绝
- `--relative list` (或 `-L`)—忽略所有绝对链接
- `--retr-symlinks`—将远程符号链接视为新文件
- `--save-headers` (或 `-s`)—在文档文件中保存 Web 服务器头
- `--server-response` (或 `-S`)—显示服务器响应
- `--span-hosts` (或 `-H`)—在递归检索时跨越主机
- `--spider`—检查文件是否存在，但不下载它
- `--timeout=S` (或 `-t S`)—网络套接字超时（秒）；*0* 表示无超时
- `--timestamping` (或 `-N`)—仅获取新文件
- `--tries=N` (或 `-t N`)—最多尝试 N 次；如果是 inf，则永远尝试
- `--user-agent=U` (或 `-U U`)—指定不同的用户代理，以访问不允许 wget 的服务器
- `--verbose` (或 `-v`)—默认显示所有进度信息
- `--wait=S` (或 `-w s`)—在检索之间暂停 s 秒。还可以指定 m 分钟、h 小时和 d 天。

### ftp 命令选项
- `-A`—主动模式 ftp（不尝试被动模式）
- `-a`—使用匿名登录
- `-d`—启用调试
- `-e`—禁用命令行编辑
- `-f`—强制通过代理进行的传输重新加载缓存
- `-g`—禁用文件名通配符
- `-1`—在多个文件传输期间关闭交互式提示
- `-n`—初始连接时不自动登录
- `-o file`—自动获取文件时，将内容保存在 file 中
- `-p`—使用被动模式（默认）
- `-P port`—连接到指定端口而不是默认端口
- `-r sec`—每隔 sec 秒重试连接
- `-R`—重启所有非代理自动获取
- `-t`—启用数据包跟踪
- `-T dir, max l, incj`—设置方向 dir 的最大字节/秒传输速率；可选增量 inc
- `-v`—启用详细消息（终端默认）
- `-V`—禁用详细和进度

### csplit 命令选项
- `-suffix=Format=PM7` (或 `-b PML`)—使用 printf 格式 PM7 而不是 1d
- `-prefix=PPX` (或 `-z PPX`)—使用前缀 PPX 而不是 xx
- `-keep-files` (或 `-k`)—在错误时不删除输出文件
- `-digits=D` (或 `-n D`)—使用指定数字位数而不是两位
- `-quiet` (或 `-silent` 或 `-s`)—不打印进度信息
- `-elide-empty-files` (或 `-z`)—删除空的输出文件

### expand 命令选项
- `-initial` (或 `-i`)—不转换非空白字符后的 Tab 字符
- `-tabs=N` (或 `-t N`)—将 Tab 更改为每隔 N 个字符，而不是八个
- `-tabs=L` (或 `-t L`)—使用逗号分隔的显式 Tab 位置列表

### unexpand 命令选项
- `-all` (或 `-a`)—转换所有空白，而不是初始空白
- `-tabs=N` (或 `-t N`)—将 Tab 更改为每隔 N 个字符，而不是八个
- `-tabs=L` (或 `-t L`)—使用逗号分隔的显式 Tab 位置列表

### mktemp 命令选项
- `-d`—创建一个目录而不是一个文件
- `-q`—如果发生错误则静默失败
- `-u`—以“不安全”模式运行；创建文件然后删除它，以便脚本稍后创建它

### head 命令选项
- `-bytes=B` (或 `-c B`)—打印前 B 个字节
- `-lines=L` (或 `-n L`)—打印前 L 行，而不是前 10 行
- `-quiet` (或 `-silent` 或 `-q`)—从不打印带有文件名的标题

### tail 命令选项
- `-retry`—继续尝试打开文件
- `-bytes=N` (-c N)—输出最后 N 个字节
- `-follow[=ND]` (或 `-f ND`)—随着由名称 N 或描述符 D 指示的文件增长，输出追加的数据
- `-lines=N` (或 `-n N`)—输出最后 N 行，而不是最后 10 行
- `-max-unchanged-stat=N`—即使文件被删除或重命名，也继续检查文件最多 N 次（默认为 5）




# ## tail 命令开关

- `-max-consecutive-size-changes=N` — 在连续 $N$ 次迭代（默认为 200）文件大小相同后，确保文件名指向同一个 inode
- `-pid=PID` — 当进程 ID 为 $PID$ 的进程终止后结束
- `-quiet`（或 `-silent` 或 `-q`） — 从不输出包含文件名的标题
- `-sleep-interval=S`（或 `-s S`） — 在每次迭代之间休眠 $S$ 秒

# ## wc 命令开关

- `-bytes`（`-chars` 或 `-c`） — 打印字节计数
- `-lines`（或 `-l`） — 打印换行符（新行）计数
- `-max-line-length`（或 `-L`） — 打印最长行的长度
- `-words`（或 `-w`） — 打印单词计数

# ## cut 命令开关

- `-bytes=L`（或 `-b L`） — 仅显示这些指定的字节
- `-characters=L`（或 `-c L`） — 仅显示这些指定的字符
- `-delimiter=D`（或 `-d D`） — 使用分隔符 $D$ 替代 Tab 字符作为字段分隔符
- `-fields=L`（或 `-f L`） — 仅显示这些指定的字段
- `-only-delimited`（或 `-s`） — 不显示没有分隔符的行
- `-output-delimiter=D` — 使用分隔符 $D$ 作为输出分隔符

# ## paste 命令开关

- `-delimiters=L`（或 `-d L`） — 使用字符列表 $L$ 替代 Tab 字符
- `-serial`（或 `-s`） — 逐个粘贴文件，而不是并行粘贴

# ## join 命令开关

- `-1 F` — 根据文件 1 的字段 $F$ 进行连接
- `-2 F` — 根据文件 2 的字段 $F$ 进行连接
- `-a file` — 打印 *file* 中未配对的行
- `-e s` — 用字符串 $s$ 替换缺失的输入字段
- `-ignore-case`（或 `-i`） — 在比较字段时忽略大小写差异
- `-o F` — 在构建输出行时遵循格式 $F$
- `-c c` — 使用字符 c 作为输入和输出字段分隔符
- `-v file` — 抑制来自 file 的连接输出行

# ## merge 命令开关

- `-h` — 通过将文件 2 到文件 3 的所有更改合并到文件 1 来解决冲突
- `-e` — 合并冲突标记为 ==== 和 ====
- `-E` — 合并冲突标记为 <<<<< 和 >>>>>
- `-L label` — 最多使用三次来指定用于替代文件名的标签
- `-p` — 写入标准输出
- `-q` — 不发出有关冲突的警告

# 12

# 文本文件处理

几年前，我的一位老高中朋友 Dan 带着两本复印件和一张 CD-ROM 来到了我家。“你一定要试试这个，”他说，“这是名为 Linux 的免费操作系统的 0.9 版本。”

我们将 Linux 加载到一台备用的 386 计算机上。该发行版的命令提示符不显示当前目录。经过几分钟的搜索和实验，Dan 使用 `rm -f *` 删除了他的临时文件。几秒钟后，他用 control-c 中断了命令，看起来很担心。“那花的时间太久了。我觉得我可能进错目录了。”

“损坏得有多严重？”我问道，并输入了 `ls`。Shell 响应为“command not found”。他一直在 `/bin` 目录下删除文件。

“我们该怎么办？”他问，“CD-ROM 仍然挂载着，但当我们无法列出任何内容时，我们找不到恢复 bin 目录的文件。”

我没有批评他：我自己也有几个 `rm` 的惨痛故事。过了一会儿，我冒险输入了 `find . -type f -maxdepth 1 -print`，当前目录下的文件在屏幕上滚动显示。我笑了。“你搞坏了 `ls`，但 `find` 命令仍然完好无损。”我们设法替换了缺失的文件，业务恢复了正常。`find` 命令救了我们，避免了完全重新安装。

本章包含更多关于使用上一章开头介绍的 `orders.txt` 文件处理文本文件的示例。

## 查找行

Linux `grep` 命令在文件中搜索匹配模式的行。在其他基于 Unix 的系统中，还有另外两个 `grep` 命令，称为 `egrep`（扩展 grep）和 `fgrep`（固定字符串 grep）。Linux 将这些变体合二为一。`egrep` 命令使用 `--extended-regexp`（或 `-E`）开关运行 `grep`，而 `fgrep` 命令使用 `--fixed-strings`（或 `-F`）开关运行 `grep`。

奇怪的名字 `grep` 起源于 Unix 早期，当时其中一行编辑命令是 `g/ze/p`（全局搜索正则表达式并打印匹配的行）。由于此编辑器命令使用频率极高，创建了一个单独的 `grep` 命令，以便在无需先启动行编辑器的情况下搜索文件。

`grep` 使用称为*正则表达式*的匹配模式，这与扩展 test 命令（`[[ . . ]]`）的模式匹配类似。基本符号如下：

- `.*` — 零个或多个字符
- `.+` — 一个或多个字符
- `?` — 跟随一个字符，该字符是可选的
- `.` — 单个字符（这在扩展 test 中是 `?`）
- `^` — 行首
- `$` — 行尾
- `[. . .]` — 字符列表，包括范围和字符类
- `[n]` — 跟随一个项，该项应出现 *n* 次
- `{n}` — 跟随一个项，该项应出现 *n* 次或更多
- `{n, m}` — 跟随一个项，该项应出现 *n* 到 *m* 次
- `(…)` — 一个子模式，用于改变操作顺序

请注意，这些符号与用于文件匹配的通配符符号不完全相同。例如，在命令行中，问号代表任何字符，而在 `grep` 中，句号具有此功能。

字符 `?`、`+`、`{`、`}` 和 `)` 必须用反斜杠转义，以防止 Bash 将它们视为文件匹配字符。

假设你想匹配 `orders.txt` 文件中所有包含 *w* 的订单。

```bash
$ grep 'w' orders.txt
Mahogany Writing Desk,463.99,1,756
Walnut TV Stand,388.99,1,756
```

星号 (`*`) 是一个占位符，代表零个或多个字符。

```bash
$ grep "*Desk" orders.txt
Mahogany Writing Desk,463.99,1,756
```

`--fixed-strings` 开关抑制了模式匹配字符的含义。当与 `*Desk` 一起使用时，`grep` 搜索精确的字符串，包括星号，而文件中任何地方都没有出现星号。

```bash
$ grep --fixed-strings "*Desk" orders.txt
$
```

脱字符 (`^`) 表示行的开始。使用脱字符来检查行首的模式。

```bash
$ grep "^R" orders.txt

Reclining Chair,1599.99,1,757
Rocking Chair,287.99,1,757
```

`-ignore-case`（或 `-i`）开关使搜索不区分大小写。搜索 `*W*` 会显示所有包含 `w` 或 `v` 的行。

```bash
$ grep -ignore-case "*W*" orders.txt

Birchwood China Hutch,475.99,1,756
Two-drawer Nightstand,125.99,1,756
Six-drawer Dresser,525.99,1,757
Lawn Chair,55.99,1,756
Mahogany Writing Desk,463.99,1,756
Walnut TV Stand,388.99,1,756
```

`-invert-match`（或 `-v`）开关显示不匹配的行。匹配的行不会显示。

```bash
$ grep -invert-match "*r*" orders.txt

Bunk Bed,705.99,1,757
Queen Bed,925.99,1,757
Pine Round Table,375.99,1,757
Walnut TV Stand,388.99,1,756
```

正则表达式可以用垂直线 (`|`) 连接在一起。这与结合两个单独 `grep` 命令的结果具有相同的效果。

```bash
$ grep "*Stool*" orders.txt
Bar Stool,45.99,1,756
$ grep "*Chair*" orders.txt
Reclining Chair,1599.99,1,757
Lawn Chair,55.99,1,756
Rocking Chair,287.99,1,757
Chair - Rocking,287.99,1,757
$ grep "*Stool*||*Chair*" orders.txt
Reclining Chair,1599.99,1,757
Bar Stool,45.99,1,756
Lawn Chair,55.99,1,756
Rocking Chair,287.99,1,757
Chair - Rocking,287.99,1,757
```

为了识别匹配的行，`-line-number`（或 `-n`）开关同时显示行号和该行。使用 `cut`、`head` 和 `tail`，第一个行号可以保存到一个变量中。可以使用 `-byte-offset`（或 `-b`）显示文件中的字节偏移量。

```bash
$ grep -line-number "*Chair - Rock*" orders.txt
19:Chair - Rocking,287.99,1,757
$ FIRST=$(grep -line-number "*Chair - Rock*" orders.txt | cut -d: -f1 | head -1)
$ printf "First occurrence at line \n" "$FIRST"
First occurrence at line 19
```




`-count`（或 `-c`）选项统计匹配数量并显示总数。

```
$ CNT=`grep --count "Chair" orders.txt`
$ printf "There are $d chair(s).\n" "$CNT"
There are 4 chair(s).
```

`grep` 同样识别标准字符类。

```
$ grep "[^[:cntrl:]]" orders.txt
$
```

Linux `grep` 选项的完整列表见本章末尾的参考部分。

## 查找文件

Linux `locate` 命令会查询数据库并返回包含特定字符组的所有路径名列表，类似于固定字符串的 `grep`。

```
$ locate /orders.txt
/home/kburch/test/orders.txt
/home/kburch/orders.txt
$ locate orders.txt
/home/kburch/test/orders.txt
/home/kburch/test/advocacy/old_orders.txt
/home/kburch/orders.txt
```

旧版本的 `locate` 会显示系统上的任何文件，甚至包括你通常没有权限访问的文件。新版本仅显示你有权限查看的文件。

`locate` 数据库由名为 `updatedb` 的命令维护。Linux 发行版通常每天执行一次该命令。因此，`locate` 速度非常快，但仅适用于查找至少已存在一天的文件。

## 搜索文件

Linux `find` 命令用于搜索满足特定条件的文件，例如具有特定名称或大于特定大小的文件。`find` 类似于以下循环，其中 *MATCH* 是匹配条件：

```
ls --recursive | while read FILE ; do
# test file for a match
if [ $MATCH ] ; then
printf "%s\n" "$FILE"
fi
done
```

此脚本递归搜索当前目录下的子目录，查找文件名匹配某个名为 *MATCH* 的条件。

find 比此脚本片段功能强大得多。与内置的 test 命令类似，find 选项会创建描述待查找文件特性的表达式。还有一些选项用于改变 find 的整体行为，以及其他选项用于指示在找到匹配项时执行的操作。

基本的匹配选项是 -name，它指定要查找文件的名称。名称可以是具体的文件名，也可以包含 shell 路径通配符（glob）字符，如 * 和 ?。如果使用模式匹配，必须用引号将该模式括起来，以防止 shell 在 find 命令检查之前对其进行扩展。

```
$ find . -name '*.txt'
./orders.txt
./advocacy/linux.txt
./advocacy/old_orders.txt
```

第一个参数是要开始搜索的目录。在这种情况下，它是当前目录。

前一个 find 命令匹配任何类型的文件，包括管道或目录等文件，这通常不是用户的本意。-type 选项将文件限制为特定类型。-type f 选项仅匹配常规文件，这是最常见的搜索类型。类型也可以是 b（块设备）、c（字符设备）、d（目录）、p（管道）、l（符号链接）或 s（套接字）。

```
$ find . -name '*.txt' -type f
./orders.txt
./advocacy/linux.txt
./archive/old_orders.txt
```

选项 -name '*.txt' -type f 是一个 find 表达式的示例。这些选项匹配同时满足这两个条件的文件（隐含逻辑“与”）。还有其他运算符选项用于将条件组合成逻辑表达式，如下所示：

- `( expr )`—强制先测试括号内的选项
- `-not expr`（或 `! expr`）—确保不匹配该选项
- `expr -and expr`（或 `expr -a expr`）—默认行为；查找匹配两组选项两者的文件
- `expr -or expr`（或 `expr -o expr`）—逻辑“或”。查找匹配任一组选项的文件
- `expr , expr`—始终检查两组选项，但使用右侧组的结果来确定匹配

例如，要统计常规文件和目录的数量，请执行以下操作：

```
$ find . -type d -or -type f | wc -1
```

也可以统计没有 `.txt` 后缀的文件数量。

```
$ find . -name "*.txt" -type f | wc -l
185
```

必须使用反斜杠或引号转义括号，以防止 Bash 将其解释为子 shell。使用括号时，可以表示以 `.txt` 或 `.sh` 结尾的文件数量如下：

```
$ find . "( -name "*.txt" -or -name "*.sh" )" -type f | wc -l
11
```

某些表达式选项涉及时间测量。历史上，`find` 的时间以天为单位测量，但 GNU 版本增加了以分钟为单位的 `min` 选项。`find` 寻找精确匹配。

要搜索早于某个时间段的文件，请包含加号或减号。如果时间前有一个`加号 (+)`，`find` 将搜索大于该时间量的时间。如果时间测量前有一个`减号 (-)`，`find` 将搜索小于该时间量的时间。加号和减号零天的指定是不同的：`+0` 天意味着“比零天更老”，换句话说，是一天或多天前的文件。同样，分钟中的 `-5` 意味着“比 5 分钟年轻”或“零到四分钟前的文件”。

有几个选项用于测试 `access time`（访问时间），即文件最后一次被读取或写入的时间。`-anewer` 选项检查一个文件的访问时间是否比指定文件更近。`-atime` 测试文件被访问了多少天前。`-amin` 以分钟为单位检查访问时间。

同样，你可以使用 `-cnewer`、`-ctime` 和 `-cmin` 检查 inode 更改时间。inode 时间通常（但不总是）代表文件创建的时间。你可以使用 `-newer`、`-mtime` 和 `-mmin` 检查 `modified time`（修改时间），即文件最后一次被写入的时间。

要查找未在超过一天时间内更改的文件：

```
$ find . -name "*.sh" -type f -mtime +0
./archive/old_orders.txt
```

要查找在过去 10 到 60 分钟内被访问过的文件：

```
$ find . -name "*.txt" -type f -amin +9 -amin -61
./orders.txt
./advocacy/linux.txt
```

`-size` 选项测试文件大小。默认测量单位是 512 字节块，这对许多用户来说反直觉，且是常见的错误来源。与具有不同时间测量选项的时间测量选项不同，要更改 `size` 的测量单位，必须在数值后跟随 `b (bytes)`、`c (characters)`、`k (kilobytes)` 或 `w (16-bit words)`。没有 `m (megabytes)`。与时间测量一样，数值可以有减号 (-) 来测试小于指定大小的文件，或加号 (+) 来测试更大的文件。

例如，使用此命令查找大于 1MB 的日志文件：

```
$ find . -type f -name "*.log" -size +1024k
./logs/giant.log
```

find 将匹配的路径显示在标准输出上。历史上，必须使用 `-print` 选项。现在，对于大多数类 Unix 操作系统（包括 Linux），打印输出是默认行为。如果兼容性是个问题，请在 find 参数末尾添加 `-print`。

要对成功匹配执行不同的操作，请使用 `-exec`。-exec 选项在每个匹配的文件上运行一个程序。这通常与 rm 结合使用以删除匹配文件，或与 grep 结合使用以进一步测试文件是否包含特定模式。通过一对花括号（{}）将文件名插入到命令中，并且命令以一个转义的分号结尾。（如果分号未转义，shell 会将其解释为 find 命令的结束，而不是命令的一部分。）

```
$ find . -type f -name "*.txt" -exec grep Table {} \;
Pine Round Table,375.99,1,757
Pine Round Table,375.99,1,757
```

可以指定多个操作。要在 grep 匹配后显示文件名，请包含 `-print`。

```
$ find . -type f -name "*.txt" -exec grep Table {} \; -print
./orders.txt
Pine Round Table,375.99,1,757
./archive/old_orders.txt
```

find 期望 {} 单独出现（即周围有空格）。它不能与其他字符组合，例如尝试形成新的路径名。

对于大量文件，-exec 选项可能速度较慢：命令必须在每个匹配项上执行。当可以选择将结果管道传输到第二个命令时，执行速度比使用 -exec 时显著更快。管道通过两个命令而不是数百或数千个命令生成结果。

-ok 选项的工作方式与 -exec 相同，除了它会交互式地验证是否应该运行该命令。

```
$ find . -type f -name "*.txt" -ok rm {} \;
< rm ... ./orders.txt > ? n
< rm ... ./advocacy/linux.txt > ? n
< rm ... ./advocacy/old_orders.txt > ? n
```

-ls 操作选项以更多细节列出匹配文件。find 为每个匹配文件运行 ls -dils。

```
$ find . -type f -name "*.txt" -ls
243000    4 -rw-rw-r--   1 kburtch    kburtch       592 May 17 14:41 ./orders.txt
114683    0 -rw-rw-r--   1 kburtch    kburtch         0 May 17 14:41 ./advocacy/1
```




## 排序

Linux 的 `sort` 命令用于对单个文件或多个文件进行排序。文件可以显式命名，也可以通过重定向标准输入进行排序。`sort` 的开关与其他命令（如 `grep` 或 `cut`）完全不同。`sort` 是最后几个支持长选项版本的命令之一；因此，这里使用的是短选项。即便如此，常用选项的开关也与其他 Linux 命令不同。

要正确地对*文件*进行排序，`sort` 命令需要知道*排序键*，即每行中决定行顺序的字符。对于排序而言，键以外的任何内容都会被忽略。默认情况下，整行被视为键。

`-f`（*合并大小写*）开关执行不区分大小写的排序（不像许多其他 Linux 命令那样使用 `-i` 开关）。

```
$ sort -f orders.txt
Bar Stool,45.99,1,756
Birchwood China Hutch,475.99,1,756
Bookcase Oak Veneer,205.99,1,756
Bunk Bed,705.99,1,757
Cedar Armoire,825.99,1,757
Cedar Toy Chest,65.99,1,757
Chair - Rocking,287.99,1,757
Garden Bench,149.99,1,757
Grandfather Clock,2045.99,1,756
Lawn Chair,55.99,1,756
Mahogany Writing Desk,463.99,1,756
Pine Round Table,375.99,1,757
Queen Bed,925.99,1,757
Reclining Chair,1599.99,1,757
Rocking Chair,287.99,1,757
Six-drawer Dresser,525.99,1,757
Small Bookcase Oak Veneer,205.99,1,756
Two-drawer Nightstand,125.99,1,757
Victorian-style Sofa,1225.99,1,757
Walnut TV Stand,388.99,1,756
```

`-r`（*反向*）开关会反转排序顺序。

```
$ head orders.txt | sort -f -r
Two-drawer Nightstand,125.99,1,756
Small Bookcase Oak Veneer,205.99,1,756
Six-drawer Dresser,525.99,1,757
Reclining Chair,1599.99,1,757
Queen Bed,925.99,1,757
Pine Round Table,375.99,1,757
Cedar Toy Chest,65.99,1,757
Bunk Bed,705.99,1,757
Bookcase Oak Veneer,205.99,1,756
Birchwood China Hutch,475.99,1,756
```

如果只使用行的一部分作为键，则使用 `-k`（*键*）开关来确定使用哪些字符。字段分隔符是任何一组空格或制表符字符，但你可以使用 `-t` 开关更改此设置。

要对订单文件的前 10 行按第二个及后续字段进行排序，请使用以下命令：

```
$ head orders.txt | sort -f -t, -k2
Two-drawer Nightstand, 125.99, 1,756
Reclining Chair, 1599.99, 1,757
Bookcase Oak Veneer, 205.99, 1,756
Small Bookcase Oak Veneer, 205.99, 1,756
Pine Round Table, 375.99, 1,757
Birchwood China Hutch, 475.99, 1,756
Six-drawer Dresser, 525.99, 1,757
Cedar Toy Chest, 65.99, 1,757
Bunk Bed, 705.99, 1,757
Queen Bed, 925.99, 1,757
```

键的位置后可以跟随结束位置，用逗号分隔。例如，要仅根据第二个字段进行排序，请使用键 `-k 2,2`。

如果字段编号包含小数部分，则它表示键开始的该字段中的字符。字段中的第一个字符为 1。第一个字段始终从行首开始。例如，要忽略第一个字符进行排序，请指定键从第一个字段的第二个字符开始。

```
$ head orders.txt | sort -f -k1.2
Reclining Chair, 1599.99, 1,757
Cedar Toy Chest, 65.99, 1,757
Pine Round Table, 375.99, 1,757
Birchwood China Hutch, 475.99, 1,756
Six-drawer Dresser, 525.99, 1,757
Small Bookcase Oak Veneer, 205.99, 1,756
Bookcase Oak Veneer, 205.99, 1,756
Queen Bed, 925.99, 1,757
Bunk Bed, 705.99, 1,757
Two-drawer Nightstand, 125.99, 1,756
```

有许多影响键解释方式的开关。`-b`（*空白*）开关表示键是带有前导空格的字符串，这些空格应被忽略。`-n`（*数值*）开关将键视为数字。此开关识别负号和十进制部分，但不识别正号。`-g`（*通用数字*）开关将键视为 C 语言浮点数表示法，允许无穷大、非数字（NaN）和科学计数法。此选项比 `-n` 慢。数值开关总是隐含 `-b`。`-d`（*电话簿*）开关在排序键中仅使用字母数字字符，忽略句点、连字符和其他标点符号。`-i`（*忽略不可打印字符*）开关在排序键中仅使用可打印字符。`-M`（*月份*）开关按月份名称缩写进行排序。

可以有多个排序键。可以通过将字符附加到键数量末尾来对单个键应用键解释开关，例如 `-k4,4M`，其含义为“按包含月份名称的第四个字段排序”。`-x` 和 `-f` 开关也可以这样使用。

作为一个更复杂的示例，以下 `sort` 命令按 `account` 号码反向排序，然后按 `product` 名称排序。该排序不区分大小写，并跳过前导空格：

```
$ head orders.txt | sort -t, -k4,4rn -k1,1fb
Bunk Bed,705.99,1,757
Cedar  Toy  Chest,65.99,1,757
Pine Round Table,375.99,1,757
Queen Bed,925.99,1,757
Reclining Chair,1599.99,1,757
Six-drawer Dresser,525.99,1,757
Birchwood China Hutch,475.99,1,756
Bookcase Oak Veneer,205.99,1,756
Small Bookcase Oak Veneer,205.99,1,756
Two-drawer Nightstand,125.99,1,756
```

对于长排序，`-c`（*仅检查*）开关在尝试排序之前检查文件是否需要排序。如果文件已排序，此开关返回状态码 `0`。

`sort` 开关的完整列表出现在参考部分。

## 字符编辑（`tr`）

Linux 的 `tr`（*转换*）命令替换或删除标准输入中的字符，并将结果写入标准输出。

`-d`（*删除*）开关删除特定字符。

```
$ printf "$a\n" 'The total is $234.45 US'
The total is $234.45 US
$ printf "$a\n" 'The total is $234.45 US' | tr -d '$'
The total is 234.45 US
```

字符范围表示为第一个字符、减号和最后一个字符。

```
$ printf "$a\n" 'The total is $234.45 US' | tr -d 'A-Z'
The total is $234.45
```

`tr` 支持 GNU 字符类。

```
$ printf "$a\n" 'The total is $234.45 US' | tr -d '[:upper:]'
The total is $234.45
```

在没有选项的情况下，`tr` 将一个字符集映射到另一个字符集。第一个参数中的第一个字符更改为第二个参数中的第一个字符。第一个参数中的第二个字符更改为第二个参数中的第二个字符。（以此类推。）

```
$ printf "$a\n" "The cow jumped over the moon" | tr 'aeiou' 'AEIOU'
The cOw jUmPed OvEr tHe mOoN
```




## 文件编辑 (sed)

Linux 的 **sed** (*流编辑器*) 命令对文本文件进行逐行更改。虽然名称中包含“编辑器”一词，但它并不是通常意义上的文本编辑器。你不能使用它交互式地修改文件。而 **grep** 命令是在文件中定位正则表达式模式，**sed** 命令则是在定位模式后，在发现模式的位置进行更改。

**sed** 的主要参数是一个由斜杠分隔的复杂四部分字符串。

```bash
$ sed "s/dog/canine/g" animale.txt
```

第一部分指示 **sed** 将执行何种编辑。第二部分是 **sed** 正在查找的字符模式。第三部分是要通过命令应用的字符模式。第四部分是编辑的范围（如果目标模式出现多次）。在此示例中，在 **sed** 表达式 “s/**dog**/canine/g” 中，**编辑** 命令是 **s**，要匹配的模式是 **dog**，要应用的模式是 **canine**，范围是 **g**。使用该表达式，**sed** 将把文件 **animale.txt** 中所有字符串 **dog** 的出现替换为 **canine**。

围绕 **sed** 表达式使用引号非常重要。许多对 shell 有特殊含义的字符对 **sed** 也有特殊含义。为了防止 shell 在 **sed** 有机会分析表达式之前解释这些字符，必须对表达式加上引号。

与 **grep** 类似，**sed** 使用正则表达式来描述模式。此外，Linux 版本的 **sed** 处理的行长度没有限制。

一些 **sed** 命令可以通过包含行号来操作特定行。也可以通过初始行和步进因子指定行号。**1-2** 从第 1 行开始搜索所有行，步长为 2。也就是说，它选择文件中的所有奇数行。可以通过第一行、逗号和最后一行指定地址范围。**1,10** 搜索前 10 行。末尾的感叹号会反转搜索的方向。**1,10!** 搜索除前 10 行以外的所有行。如果没有指定行，则搜索所有行。

### s (替换) 命令

**sed s** (*替换*) 命令将匹配的模式替换为新的文本。

要在订单文件的前 10 行中将单词 **Pine** 替换为 **Cedar**，请使用以下命令：

```bash
$ head order5.txt | sed 's/Pine/Cedar/g'
Birdwood China Hutch,475.99,1,756
Bookcase Oak Veneer,205.99,1,756
Small Bookcase Oak Veneer,205.99,1,756
Reclining Chair,1599.99,1,757
Bunk Bed,705.99,1,757
Queen Bed,925.99,1,757
Two-drawer Nightstand,125.99,1,756
Cedar Toy Chest,65.99,1,757
Six-drawer Dresser,525.99,1,757
Cedar Round Table,375.99,1,757

Pine Round Table becomes Cedar Round Table.
```

如果替换字符串为空，则会删除该模式的出现。

```bash
$ head orders.txt | sed 's/757//g'
Birchwood China Hutch,475.99,1,756
Bookcase Oak Veneer,205.99,1,756
Small Bookcase Oak Veneer,205.99,1,756
Reclining Chair,1599.99,1,
Bunk Bed,705.99,2,
Queen Bed,925.99,1,
Two-drawer Nightstand,125.99,1,756
Cedar Toy Chest,65.99,1,
Six-drawer Dresser,525.99,1,
Pine Round Table,375.99,1,
```

脱字符 (^) 表示行的开始。

```bash
$ head orders.txt | sed '/^Bunk/a DISCONTINUED - Bunk'
Birchwood China Hutch,475.99,1,756
Bookcase Oak Veneer,205.99,1,756
Small Bookcase Oak Veneer,205.99,1,756
Reclining Chair,1599.99,1,757
DISCONTINUED - Bunk Bed,705.99,1,757
Queen Bed,925.99,1,757
Two-drawer Nightstand,125.99,1,756
Cedar Toy Chest,65.99,1,757
Six-drawer Dresser,525.99,1,757
Pine Round Table,375.99,1,757
```

可以使用 I (不区分大小写) 修饰符执行不区分大小写的测试。

```bash
$ head orders.txt | sed 's/BED/BED/Ig'
Birchwood China Hutch,475.99,1,756
Bookcase Oak Veneer,205.99,1,756
Small Bookcase Oak Veneer,205.99,1,756
Reclining Chair,1599.99,1,757
Bunk BED,705.99,1,757
Queen BED,925.99,1,757
Two-drawer Nightstand,125.99,1,756
Cedar Toy Chest,65.99,1,757
Six-drawer Dresser,525.99,1,757
Pine Round Table,375.99,1,757
```

**sed** 支持 GNU 字符类。若要隐藏价格，请将所有数字替换为下划线。

```bash
$ head orders.txt | sed 's/[[:digit:]]/_/g'
Birchwood China Hutch,____,__-__-
Bookcase Oak Veneer,____,____'-__
Small Bookcase Oak Veneer,____,'__'__
Reclining Chair,_ . ' ' _
Bunk Bed, _ . ' ' _
Queen Bed, _ . ' ' _
Two-drawer Nightstand, _ . ' ' _
Cedar Toy Chest, _ . ' ' _
Six-drawer Dresser, _ . ' ' _
Pine Round Table, _ . ' '
```

### d (删除) 命令

**d** (*删除*) 命令删除匹配的行。你可以使用模式 `'/$'` 删除空行（也就是说，空行是行首、行尾，中间什么都没有）。

```bash
$ head orders.txt | sed '/^$/d'
```

如果没有模式，你可以在 d 之前放置行号来删除特定行。例如，`1d` 删除第一行。

```bash
$ head orders.txt | sed '1d'
Bookcase Oak Veneer,205.99,1,756
Small Bookcase Oak Veneer,205.99,1,756
Reclining Chair,1599.99,1,757
Bunk Bed,705.99,1,757
Queen Bed,925.99,1,757
Two-drawer Nightstand,125.99,1,756
Cedar Toy Chest,65.99,1,757
Six-drawer Dresser,525.99,1,757
Pine Round Table,375.99,1,757
```

单独的 d 会删除所有行。

### 面向行的命令

有几个面向行的命令。**a** (*追加*) 命令在匹配行之后插入新文本。**i** (*插入*) 命令在匹配行之前插入文本。**c** (*更改*) 命令替换一组行。

要在 Cedar Toy Chest 之前插入标题 DISCOUNTED ITEMS:，请执行以下操作：

```bash
$ head orders.txt | sed '/Cedar Toy Chest/i\
DISCOUNTED ITEMS:'
Birchwood China Hutch,475.99,1,756
Bookcase Oak Veneer,205.99,1,756
Small Bookcase Oak Veneer,205.99,1,756
Reclining Chair,1599.99,1,757
Bunk Bed,705.99,1,757
Queen Bed,925.99,1,757
Two-drawer Nightstand,125.99,1,756
DISCOUNTED ITEMS:
Cedar Toy Chest,65.99,1,757
Six-drawer Dresser,525.99,1,757
Pine Round Table,375.99,1,757
```

要将 Bunk Bed、Queen Bed 和 Two-drawer Nightstand 替换为 Items deleted 消息，可以使用：

```bash
$ head orders.txt | sed \
'/^Bunk Bed/;/^Two-drawer/c/\n<Items deleted>\n'
Birchwood China Hutch,475.99,1,756
Bookcase Oak Veneer,205.99,1,756
Small Bookcase Oak Veneer,205.99,1,756
Reclining Chair,1599.99,1,757
<Items deleted>
Cedar Toy Chest,65.99,1,757
Six-drawer Dresser,525.99,1,757
Pine Round Table,375.99,1,757
```

您必须在 *插入*、*追加* 和 *更改* 命令后跟随一个转义的行结束符。

### l (列表) 命令

**l** (*list*) 命令用于显示不可打印的字符。它显示字符的 ASCII 码或反斜杠序列。

```bash
$ printf "%s\015\t\004\n" "ABC" | sed -n "l"
ABC^M^I^D$
```

在这种情况下，`\015`（回车）显示为 `^M`，`\t` 制表符字符显示为 `^I`，`\n` 换行符显示为 `$` 和一个换行符。没有反斜杠等价物的字符 `\004` 显示为 `^D`。`A`、`B` 和 `C` 显示为它们本身。

### y (转换) 命令

**y** (*转换*) 命令是 *替换* 命令的一种特殊短格式。它执行一对一的字符替换。它本质上等同于单字符替换的一组操作。

例如，`y/a/b` 等同于 `s/a/b/`：

```bash
$ head orders.txt | sed "y/a/A/"
Birchwood China Hutch,475.99,1,756
Bookcase Oak Veneer,205.99,1,756
Small Bookcase Oak Veneer,205.99,1,756
Reclining Chair,1599.99,1,757
Bunk Bed,705.99,1,757
Queen Bed,925.99,1,757
Two-drawer Nightstand,125.99,1,756
Cedar Toy Chest,65.99,1,757
Six-drawer Dresser,525.99,1,757
Pine Round Table,375.99,1,757
```

然而，对于多字符模式，*转换* 将第一个模式的任何出现替换为第二个模式的第一个字符，第二个字符替换为第二个模式的第二个字符，依此类推。其工作方式类似于 `tr` 命令。

```bash
$ printf "%s\n" "order code B priority 1" | sed "y/B1/C2/"
order code C priority 2
```

## tr 命令参考

**tr** 支持字符等价性。例如，要将名为 FOREIGN_STRING 的变量中的任何 e 类字符转换为普通 e，请使用：

```bash
$ printf "$FOREIGN_STRING" | tr "[eeé]" "e"
```

**-truncate-set-n**（或 **-t**）忽略第一个参数中没有第二个参数中匹配字符的任何字符。

**-complement**（或 **-c**）开关反转匹配的含义。第一个参数中的字符不会映射到第二个参数中，但不在第一个参数中的字符会被更改为指定的字符。

```bash
$ printf "%s\n" "The cow jumped over the moon" | tr -complement 'aeiou' '?'
???e???o??uu???o??e???e???e???moo??
```

**-squeeze-repeats**（或 **-s**）开关将多个出现的字母减少为每个指定字母的单个字符：

```bash
$ printf "%s\n" "aaabbbccc" | tr -squeeze-repeats 'c'
aaabbbc
```

**tr** 最普遍的用途是将 MS-DOS 文本文件转换为 Unix 文本文件。DOS 文本文件具有回车符和换行符，而 Linux 仅使用换行符标记行尾。需要删除多余的回车符。

```bash
$ tr -d '\r' < dos.txt > linux.txt
```

Apple 文本文件使用回车符而不是换行符。**tr** 也可以通过替换回车符来处理这种情况。

```bash
$ tr '\r' '\n' < apple.txt > linux.txt
```

**tr** 识别的其他转义字符如下：

- `\o` — ASCII 八进制值 o（一到三个八进制数字）
- `\\` — 反斜杠
- `\a` — 可听蜂鸣声
- `\b` — 退格符
- `\f` — 换页符
- `\n` — 换行
- `\r` — 回车
- `\t` — 水平制表符
- `\v` — 垂直制表符

你可以使用接下来讨论的 **sed** 命令执行更复杂的文件编辑。





不受 `sed` 影响的行可以通过 `~quiet`（或 `~n` 或 `~silent`）开关隐藏。

与 `transform` 命令类似，还有其他 `sed` 命令模仿了 Linux 命令。`p`（打印）命令通过打印匹配行来模仿 `grep` 命令。只有在使用了 `~quiet` 开关时，这才有用。`~`（行号）命令会打印匹配行的行号。`q`（退出）命令使 `sed` 表现得像 `head` 命令，显示行直到遇到某一行。

```
$ head orders.txt | sed -quiet '/^$B/p'\
Bunk Bed,705.99,1,757\
Queen Bed,925.99,1,757\
\
$ head orders.txt | sed -quiet '/^$B/d'\
5\
6
```

剩余的 `sed` 命令代表专用操作。控制流由 `n`（下一行）命令处理。文件可以用 `r` 读取或用 `w` 写入。`a`（追加下一行）将两行合并为一行用于匹配目的。`d`（多行删除）删除多行。`p` 是多行打印。`h`、`H`、`g`、`G` 和 `x` 允许你将行保存到临时缓冲区，以便你可以进行修改，显示结果，然后恢复原始文本以进行进一步分析。这就像电子计算器的内存一样工作。复杂的 `sed` 表达式可以在表达式中使用 `b` 命令嵌入分支到标签。`t`（测试）命令充当 `shell if` 或 `switch` 语句，尝试一系列操作直到其中一个成功。子命令可以用花括号嵌入在 `sed` 中。可以使用 `info sed` 找到关于这些命令的更多文档。

长的 `sed` 脚本可以存储在文件中。你可以使用 `~files`（或 `~f`）开关从文件读取 `sed` 脚本。你可以使用 `#` 字符包含注释，就像 `shell` 脚本一样。

`sed` 表达式也可以使用 `~expression`（或 `~e`）开关指定，或者当使用 `~filename` 时从标准输入读取。

你不能在 `sed` 模式中使用 `ASCII` 值转义序列。

## 压缩文件

大多数 Linux 程序区分归档和压缩。*归档* 是将多个文件存储到单个文件中。*压缩* 是通过编码文件来减小文件大小。一般来说，归档文件占用的空间比原始文件多，因此大多数归档文件也被压缩。

Linux 的 `bzip2`（BWH zip）命令使用 Burrows–Wheeler–Huffman 压缩来压缩文件。这是最常用的压缩格式。大多数发行版上都提供了较旧的压缩程序。`gzip`（GNU zip）使用 `LZ77` 压缩进行压缩，并广泛用于较旧的发行版。`compress` 是较旧的 Lempel–Ziv 压缩程序，在大多数版本的 `Unix` 上可用。`zip` 是 DOS `pkzip` 程序的 Linux 版本。`hexbin` 解压某些 Macintosh 归档。

**Linux tar**（*tape archive*）命令是最常用的归档命令，当使用正确的命令行选项时，它在归档时会自动进行压缩。虽然该命令最初用于收集文件以便存储在磁带驱动器上，但它也可以创建磁盘文件。

最初，**tar** 命令不使用命令行开关：使用的是一系列单个字符。Linux 版本支持命令行开关以及旧的单字符语法以向后兼容。

要在文件上使用 **tar**，`--file`（*F*（或 *-f*））开关指示要操作的文件名。必须指定至少一个操作开关以指示 **tar** 将如何处理文件。远程文件可以通过前面的主机名和冒号来指定。

`--create`（*-c*）开关创建一个新的 tar 文件。

```
$ ls -1 orders.txt
-rw-rw-r--  1 kburcht  kburcht     592 May 11 14:45 orders.txt
$ tar --create --file orders.tar orders.txt
$ ls -1 orders.tar
-rw-rw-r--  1 kburcht  kburcht   10240 Oct  3 12:06 orders.tar
```

归档文件明显大于原始文件。要应用压缩，使用 `--bzip`（或 *-I*）、`--gzip`（或 *-z*）、`--compress`（或 *-Z*）或 `--use-compress-program` 来选择压缩类型以指定特定的压缩程序。

```
$ tar --create --file orders.tbz --bzip orders.txt
$ ls -1 orders.tbz
-rw-rw-r--  1 kburcht  kburcht     421 Oct  3 12:12 orders.tbz
$ tar --create --file orders.tgz --gzip orders.txt
$ ls -1 orders.tgz
-rw-rw-r--  1 kburcht  kburcht     430 Oct  3 12:11 orders.tgz
```

可以同时归档多个文件。

```
$ tar --create --file orders.tbz --bzip orders.txt orders2.txt
$ ls -1 orders.tbz
-rw-rw-r--  1 kburcht  kburcht     502 Oct  3 12:14 orders.tbz
```

新的归档会覆盖现有的归档。

要恢复原始文件，使用 `--extract` 开关。使用 `--verbose` 查看文件名。**tar** 无法自动检测压缩格式；你必须指定正确的压缩开关以避免错误。

```
$ tar --extract --file orders.tbz
tar: 502 garbage bytes ignored at end of archive
tar: Error exit delayed from previous errors
$ tar --extract --bzip --file orders.tbz
$ tar --extract --verbose --bzip --file orders.tbz
orders.txt
orders2.txt
```

`--extract` 开关还会恢复文件路径名中的任何子目录。将文件解压到最初压缩所在的目录很重要，以确保它们被恢复到正确的位置。

`tar` 命令还可以使用 `--concatenate`（或 `-A`）将文件追加到归档中，使用 `--compare`（或 `--diff` 或 `-d`）与归档进行比较，使用 `--delete` 从归档中删除文件，使用 `--list` 列出内容，并使用 `--update` 替换现有文件。除非使用 `--verbose`，否则 `tar` 会静默地执行这些功能。

`tar` 开关的完整列表出现在参考部分。

另一个归档程序 `cpio`（*copy in/out*）提供用于与其他版本的 `Unix` 兼容。`rpm` 包管理器命令基于 `cpio`。

## 参考部分

### `grep` 命令开关

- `--after-context=n`（或 `-A n`）— 打印匹配行后的 `n` 行
- `--before-context=n`（或 `-B n`）— 打印匹配行前的 `n` 行
- `--context[=n]`（或 `-C [n]`）— 显示匹配行周围的 `n` 行（默认为 2）
- `--basic-regexp`（或 `-G`）— 模式不是扩展正则表达式
- `--binary-files=binary`— 正常的二进制文件行为；如果模式在二进制文件的某处存在，则发出消息
- `--binary-files=without-match`（或 `-I`）— `grep` 假设所有二进制文件都不匹配
- `--binary-files=text`（或 `-a` 或 `--text`）— 显示来自二进制文件的匹配项
- `--byte-offset`（或 `-b`）— 在每行输出之前打印输入文件中的字节偏移量
- `--count`（或 `-c`）— 打印每个输入文件的匹配行计数
- `--directories=read`（或 `-d read`）— `grep` 使用其正常行为，将目录读取为普通文件
- `--directories=skip`（或 `-d skip` 或 `-x`）— 忽略目录
- `--directories=recurse`（或 `-d recurse` 或 `-r` 或 `--recursive`）— 检查所有子目录中的文件
- `-fixed-strings`（或 `-F`）— 将模式视为字符串，忽略字符的任何特殊含义
- `-invert-match`（或 `-v`）— 选择不匹配模式的行
- `-no-filename`（或 `-h`）— 隐藏每个匹配项的文件名
- `-line-number`（或 `-n`）— 显示带有结果的行号
- `-line-regexp`（或 `-x`）— 仅匹配整行
- `-mmap`— 使用内存映射来加速在 grep 运行时不会收缩的文件上的搜索
- `-no-messages`（或 `-s`）— 抑制关于缺失文件的错误消息
- `-null`（或 `-Z`）— 使用 null 字符而不是回车符分隔项
- `-quiet`（或 `-q`）— 仅搜索到第一个匹配项并不显示它
- `-regexp=P`（或 `-E P`）— 使用字符串 P 作为匹配模式，这对于以点开头的模式很有用
- `-with-filename`（或 `-H`）— 打印带有每个匹配项的文件名
- `-word-regexp`（或 `-w`）— 仅匹配由空格或其他非单词字符与行其余部分分隔的整个“单词”

### `find` 命令开关

有大量的 `find` 表达式开关。它们包括以下内容：

- `-empty`— 匹配一个空普通文件或目录
- `-false`— 始终匹配失败
- `-fstype FS`— 文件必须位于类型为 FS 的文件系统上
- `-gid N`— 匹配数字组 ID N
- `-group N`— 文件必须由该组 ID 拥有。组 ID 可以是名称或数字
- `-daystart`— 从当天开始而不是 24 小时前测量时间
- `-depth`— 在目录本身之前查找目录的内容（深度优先遍历）
- `-file FILE`— 将 `-ls` 结果写入指定文件
- `-follow`— 跟随符号链接。通常，链接不被跟随
- `-fprint F`— 将 `-print` 结果写入文件 F
- `-fprint0 F`— 将 `-print0` 结果写入文件 F
- `-fprintf F FORMAT`— 将 `-printf` 结果写入文件 F
- `-mindepth N`— 从当前目录至少下降 N 个目录
- `-ilname pattern`— 大小写不敏感的 `-lname`




# find 命令开关

- `-iname pattern` — 不区分大小写的 `-name`
- `-inum n` — 文件必须具有此 inode 号
- `-ipath pattern` — 不区分大小写的 `-path`
- `-iregex pattern` — 不区分大小写的 `-regex`
- `-links n` — 文件必须具有 `n` 个链接
- `-lname pattern` — 文件必须是一个匹配指定模式的符号链接
- `-ls` — 以 `ls -dils` 格式列出文件
- `-maxdepth n` — 从当前目录最多向下遍历 `n` 层目录
- `-noleaf` — 对于 CD-ROM，不假设目录包含 `.` 和 `..` 条目
- `-nogroup` — 文件不能属于已知组
- `-nouser` — 文件不能属于已知用户
- `-ok cmd` — 类似于 `-exec`，但在运行命令前提示用户
- `-path pattern` — 类似于 `-name`，但匹配 `find` 返回的完整路径
- `-perm mode` — 文件必须具有指定的权限位。`-mode` 要求所有设置的位都必须设置。`+mode` 允许任何权限位被设置。
- `-print` — 默认操作，将路径名打印到标准输出
- `-print0` — 打印以 ASCII `NUL` 字符分隔的文件名
- `-printf format` — 根据 `printf` 格式字符串打印文件名
- `-prune` — 在没有 `-depth` 开关的情况下，不向下遍历当前目录
- `-regex pattern` — 类似于 `-name`，但模式是正则表达式
- `-true` — 始终为真
- `-user name` — 文件必须属于此用户 ID。ID 可以是数字
- `-uid` — 文件必须属于此数字 `uid`
- `-xdev` (或 `-mount`) — 不检查当前文件系统以外的已挂载文件系统
- `-xtype` — 类似于 `-type`，但检查符号链接

### find -printf 格式化代码

- `%%` — 字面百分号
- `%a` — 文件的最后访问时间，格式由 C 语言 `ctime` 函数返回
- `%c` — 文件的最后访问时间，格式由 `c` 指定，`c` 是 `%`（自 1970 年 1 月 1 日以来的秒数）或一个 `strftime` 时间指令
- `%b` — 文件的大小（以 512 字节块为单位，向上取整）
- `%c` — 文件的最后状态更改时间，格式由 C 语言 `ctime` 函数返回
- `%C` — 文件的最后状态更改时间，格式由 *c* 指定，与 `%A` 相同
- `%d` — 文件在目录树中的深度；0 表示文件是命令行参数
- `%f` — 文件的名称，去掉任何前导目录（仅最后一个元素）
- `%F` — 文件所在文件系统的类型；此值可用于 *-fSTYPE*
- `%g` — 文件的组名，如果组没有名称，则为数字组 ID
- `%G` — 文件的数字组 ID
- `%h` — 文件名称的前导目录（除最后一个元素外的所有部分）
- `%H` — 发现文件时的命令行参数
- `%i` — 文件的 inode 号（十进制）
- `%k` — 文件的大小（以 1KB 块为单位，向上取整）
- `%l` — 符号链接的对象（如果文件不是符号链接，则为空字符串）
- `%m` — 文件的权限位（八进制）
- `%n` — 指向文件的硬链接数量
- `%p` — 文件的路径名
- `%P` — 文件的路径名，去掉发现文件时的命令行参数名称
- `%s` — 文件的大小（以字节为单位）
- `%t` — 文件的最后修改时间，格式由 C 语言 *ctime* 函数返回
- `%T` — 文件的最后修改时间，格式由 *c* 指定，与 `%A` 相同
- `%u` — 文件的用户名，如果用户没有名称，则为数字用户 ID
- `%U` — 文件的数字用户 ID

### sort 命令开关

- *-b* (*--ignore-leading-blanks*) — 忽略排序字段或键中的前导空格
- *-c* (*-check*) — 检查文件但不排序
- *-d* (*-dictionary-order*) — 键中只考虑字母数字字符
- *-f* (*-ignore-case*) — 不区分大小写的排序
- *-g* (*-general-numeric-sort*) — 根据通用数值进行比较（隐含 *-b*）
- *-i* (*-ignore-nonprinting*) — 忽略不可打印字符
- *-k* *POS1* , *POS2* ( *-key*=*POS1* , *POS2* ) — 在字符位置 *POS1* 开始一个键，并可选地在字符位置 *POS2* 结束
- -m (-merge) — 合并已排序的文件
- -M (-month-sort) — 比较月份缩写形式（隐含 -b）
- -n (-numeric-sort) — 比较数值（隐含 -b）
- -o F (-output=F) — 将结果写入文件 F
- -r (-reverse) — 反转排序顺序
- -s (-stable) — 保持键排序相同的行的原始相对顺序
- -t S(-field-separator=S) — 使用分隔符字符 S 代替空格
- -T D(-temporary-directory=D) — 使用目录 D 作为临时文件目录，而不是 $TMPDIR 或 /tmp
- -u (-unique) — 配合 -c，检查严格顺序；配合 -n，仅输出相等序列中的第一个
- -z (-zero-terminated) — 以 ASCII NUL 字节（C 字符串）结束行

### tar 命令开关

- -absolute-path (或 -P) — 不从文件名中去除前导 /
- -after-date D (或 -newer D 或 -N D) — 仅存储比给定日期更新的文件
- -append (或 -r) — 将文件追加到归档末尾
- -atime-preserve — 不更改恢复文件的访问时间
- -block-size N(-b N) — N*512 字节的块大小（默认 N=20）
- -checkpoint — 在读取归档时打印目录名称（比 -verbose 更简洁）
- -compare (或 -diff 或 -d) — 列出文件系统与归档之间的差异
- -concatenate (或 -catenate 或 -A) — 将归档追加到另一个归档
- -create (或 -c) — 创建新归档
- -delete — 从归档中删除文件
- -dereference(-h) — 归档符号链接指向的文件
- -directory D(-C D) — 在文件列表中，切换到新目录 D
- -exclude P — 排除给定文件
- -exclude-from F(-X F) — 排除给定文件中列出的文件
- -extract (或 -get 或 -x) — 提取归档中的文件
- -files-from F(-T F) — 要提取的文件在指定文件中
- -force-local — 将归档文件名中的冒号视为文件名的一部分
- -info-script F (或 -new-volume-script F 或 -F F) — 对于多卷归档，在每卷末尾运行给定脚本
- -ignore-failed-read — 当文件无法读取时不停止处理
- -ignore-zeros (-z) — 忽略归档中的零块
- -incremental (-G) — 使用旧式 GNU 格式增量备份进行创建/列出/提取
- -interactive (或 -confirmation 或 -w) — 用户确认
- -keep-old-files (-k) — 不覆盖现有文件
- -label N (-V N) — 指定卷标签 N
- -list (或 -t) — 列出归档中的文件
- -listed-incremental (-g) — 使用新式 GNU 格式增量备份进行创建/列出/提取
- -modification-time (-m) — 不更改提取文件的修改时间
- -multi-volume (-n) — 创建/列出/提取多卷归档
- -null — 配合 -files-from，tar 期望以 ASCII NUL 字符结尾的名称（即 C 字符串）
- -old-archive (或 -portability 或 -o) — 写入 Unix V7 格式归档
- -one-file-system (-1) — 创建归档时保持在当前文件系统内
- -preserve — 等同于 -save-permissions 和 -same-order
- -read-full-blocks (-B) — 读取完整块（用于读取 4.2BSD 管道）
- -record-number (-R) — 在每条消息中显示归档内的记录号
- -remove-files — 删除添加到归档中的文件
- -to-stdout (-c) — 将提取的文件打印到标准输出
- -same-permissions (或 -preserve-permissions 或 -p) — 提取所有文件权限
- -starting-file F (-K F) — 从归档中的文件 F 开始提取/列出
- -same-order (或 -preserve-order 或 -s) — 对提取的名称进行排序以匹配归档
- -same-owner — 使提取的文件具有与添加者相同的属主
- -sparse (-S) — 高效处理稀疏文件
- -tape-length N (-L) — 在写入 N*1024 字节后更换卷
- -totals — 使用 -create 时打印保存的总字节数
- -update (或 -u) — 如果文件比归档中已有的文件更新，则添加文件
- -verify (-v) — 在写入每个归档后进行验证




### tr 命令开关

- `-complement`（或 `-c`）—对第一个字符集取补
- `-delete`（或 `-d`）—删除第一个字符集中的字符；不进行转换
- `-squeeze-repeats`（或 `-s`）—将重复的字符序列替换为一个
- `-truncate-set1`（或 `-t`）—将第一个字符集截断为与第二个字符集相同的长度

### sed 命令开关

- `-quiet`（或 `-silent` 或 `-n`）—只有使用 `p` 时，`sed` 才会产生输出
- `-file=script`（或 `-e script` 或 `-expression=script` 或 `-f script`）—名为 `script` 的文件包含要运行的 `sed` 命令

### sed 编辑代码

- `: label`—`b` 和 `t` 命令的标签
- `#comment`—注释，持续到下一个换行符（新行）
- `( )`—嵌套命令块
- `=`—打印当前行号
- `a`—附加文本
- `b [label]`—跳转到（`branches to`）`label`，如果没有标签则跳转到 `sed` 脚本的末尾
- `c`—替换选定的行
- `d`—删除并启动新的编辑周期
- `D`—删除至第一个内嵌换行符（新行）并启动新周期
- `g`（或 `G`）—将保留空间复制/附加到模式空间
- `h`（或 `H`）—将模式空间复制/附加到保留空间
- `i`—插入文本
- `l`—列出当前行
- `p`—打印当前模式空间
- `P`—打印当前模式空间至第一个内嵌换行符（新行）
- `q`—退出 `sed` 脚本
- `x`—交换从文件 `f` 读取的文本
- `t [label]`—如果替换成功，则跳转到 `label` 或脚本末尾
- `$x$`—交换保留空间和模式空间的内容
- `n`（或 `N`）—将输入的下一行读取/附加到模式空间
- `s`—替换文本
- `w f`—将当前模式空间写入文件 `f`
- `y`—转写模式空间中的字符

# 13 控制台脚本

在我曾任职的任何一家公司，如果你被指派编写一个短小的实用程序，两周后却交回了一个外观漂亮的 X Windows 应用程序，你将会被叫到老板面前并受到严厉的批评。在商业世界中，时间就是金钱，而开发 GUI 应用程序既耗时又昂贵。

控制台脚本，有时也称为基于文本或终端的脚本，是设计用于在纯文本环境中运行的脚本，例如 Linux 控制台、Telnet 会话或 xterm 窗口。控制台脚本易于设计和快速构建，但它们不必对用户不友好。Bash 和 Linux 都提供了编写友好控制台脚本的功能，而不会耗尽一个部门的开发预算。

## Linux 控制台

在 Unix 的早期，计算机是一台没有键盘和显示器的数字处理设备。为了控制计算机，必须将一个独立的管理工作站连接到系统。这个专用工作站被称为控制台。系统管理员通过其键盘监督计算机的启动和关机。所有关键错误消息都显示在控制台的屏幕上，有时也显示在其打印机上。

基于 Unix 的 Linux 仍然需要一个专用控制台。但从 Linux 的角度来看，控制台并不是一个独立的设备——它是计算机的键盘和显示器。控制台是 Linux 计算机首次启动时出现的纯文本显示。当在 X Windows 中打开终端窗口时，它们并不是控制台。控制台隐藏在桌面的“后面”。

Linux 实际上创建了七个虚拟控制台（也称为 VC 或 VT），其工作方式类似于独立的 X Windows 终端会话。每个控制台都可以通过 Alt-F1 到 Alt-F7 键进行选择。

控制台表现得像一个增强型 DEC VT-100 终端，任何设计用于在 VT-100（或 xterm 窗口）上运行的程序也可以在 Linux 控制台上运行。文本按照由 Linux `consolechars` 命令（或已弃用的 `setfont` 命令）选择的当前控制台字体绘制。

要确定当前会话是否位于控制台上，请使用 `tty` 命令。此命令会打印你所在的终端名称。

```
$ tty # 不是控制台
/dev/pts/1
```

每个控制台都有唯一的 `tty` 设备名称，从 /dev/tty1 到 /dev/tty7。主控制台，即 Linux 启动时出现的那个，是 /dev/tty1。

```
$ tty # 主控制台
/dev/tty1
```

Linux 的 `fgconsole` 命令打印控制台的编号。如果你不在控制台上，它会报告错误。

```
$ fgconsole
1
```

如果你的发行版没有 `fgconsole`，请检查 `tty` 返回的名称：

```bash
IS_CONSOLE=
TTY="tty"
case "$TTY" in
/dev/tty*|/dev/vc/* IS_CONSOLE="1" ;;
*) printf "%s\n" "This is a console" ;;
esac
```

一些 Linux 命令只能在控制台上工作，而不是在文本会话中。错误消息并不总是直观易懂。

```
$ showkey
Couldn't get a file descriptor referring to the console
$ setleds
KDG_E T_TLE D: Invalid argument
Error reading current led setting. Maybe stdin is not a VT?
```

## 控制台键盘

Shell 脚本可以控制控制台键盘的按键布局，更改当前输入模式以及 LED 指示灯。

控制台输入模式决定了用户输入的按键如何被预处理。有四种输入模式：

- *Scancode*（或 **RAW**）模式—脚本读取代表键盘上单个按键的数字代码。按下或释放按键会产生不同的代码。一次按键最多可以返回六个独立的扫描码。
- **Keycode**（或 **MEDIAN**）模式—脚本读取代表控制台驱动程序对按键解释的数字代码。通常返回两个按键代码，一个用于按下，另一个用于释放。不同的按键具有不同的按键代码。例如，按下左 Shift 或右 Shift 键会返回不同的按键代码。
- **ASCII**（或 **XLATE**）模式—这是正常的控制台模式。脚本读取每个键盘字符的 ASCII 字符代码。Shift 键等修饰键只影响其他按键。
- **UTF-8**（或 **UNICODE**）模式—与 ASCII 模式相同，只是返回 16 位 Unicode 字符而不是 ASCII。对于大多数字符，ASCII 和 UTF-8 是一样的。然而，这种模式可以为特定的按键返回多达三个字节，而不是通常的 ASCII 单字节。

Linux 的 `showkey` 命令可以演示这些模式中的每一种。使用 `--scancodes` 以扫描码模式运行程序，使用 `--keycodes` 以按键码模式运行程序，等等。以下示例显示按下 a 键时发生的情况。

```
$ showkey --keycodes
kb mode was XLATE
press any key (program terminates after 10s of last keypress)... 
keycode  28 release
keycode  30 press
keycode  30 release
$ showkey --scancodes
kb mode was XLATE
press any key (program terminates after 10s of last keypress)... 
0x9c
0x1c
0x9e
$ showkey --keycodes
kb mode was XLATE
press any key (program terminates after 10s of last keypress)... 
a ( 0xe1 )
```

`kbd_mode` 命令更改当前的键盘模式：-s（扫描码）、-k（按键码）、-a（ASCII）或 -u（UTF-8）。

脚本可以安全地在 ASCII 和 UTF-8 模式之间切换。在这两种情况下，Return 或 Enter 键都被正常处理，并且诸如 `read` 之类的命令按预期行为工作。

在扫描码或按键码模式下情况会更加复杂。按下 Return 键不再返回 ASCII/UTF-8 代码 13，因此，`read` 不再确定何时结束读取。唯一的解决办法是使用 `timeout` 功能，并让脚本检查代表 Return 键的相应扫描码或按键码。

如果控制台具有大写字母锁定、滚动锁定和数字锁定的 LED 指示灯，可以使用 `setleds` 命令将其打开或关闭。没有参数时，`setleds` 显示当前设置。

```
$ setleds
Current default flags:  NumLock off    CapsLock off    ScrollLock off
Current flags:          NumLock off    CapsLock off    ScrollLock off
Current leds:           NumLock off    CapsLock off    ScrollLock off
```

要关闭灯光，请使用以下开关：-num 关闭数字锁定灯，-caps 关闭大写锁定灯，-scroll 关闭滚动锁定灯。使用加号可以打开相应的灯。

变更的范围由另外三个标志反映：-P（让 Linux 认为灯已改变，即使它实际上没有改变），-D（同时更改 Linux 控制台驱动程序和灯光），以及 -L（更改灯光并让 Linux 认为灯未改变）。

例如，要在 tty1 上设置数字锁定灯，你可以使用

```
$ setleds -D +num < /dev/tty1
$ setleds
Current default flags:  NumLock on     CapsLock off    ScrollLock off
Current flags:          NumLock on     CapsLock off    ScrollLock off
Current leds:           NumLock on     CapsLock off    ScrollLock off
```

NumLock 灯现在应该已开启。

键位映射是一个列表，确定控制台键盘上的哪个键转换为哪个字符。更改键位映射会更改按键布局，通常是为了反映不同国家使用的键盘。

键位映射由 Linux 安装程序选择，但可以随时使用 Linux 的 `loadkeys` 命令手动更改。`dumpkeys` 命令显示当前的键位映射。

```
$ dumpkeys | head
keymaps  0-2,4-6,8-9,12
keycode  1 = Escape
          alt    keycode  1 = Meta_Escape
          shift  alt    keycode  1 = Meta_Escape
          control alt    keycode  1 = Meta_Escape
keycode  2 = one       exclam
          alt    keycode  2 = Meta_one
          shift  alt    keycode  2 = Meta_exclam
keycode  3 = two       at    at    at    nul
          alt    keycode  3 = Meta_two
kb mode was XLATE
```

要确定要使用的按键代码，请使用 `showkey`。




## 控制台显示

控制台的 VT-100 兼容显示器不是由 Linux 命令控制的，而是通过打印到显示器的特殊字符序列进行控制。控制台将这些字符识别为要执行的命令，并且这些字符不会显示出来。

Linux `setterm` 命令就像一个 `printf` 命令，打印出适当的字符以执行显示命令。`setterm` 的一些开关使用 "on" 或 "off" 来启用或禁用功能。由于 `setterm` 本质上是一个 `printf` 命令，你可以通过捕获命令的输出，将常用命令保存到变量中。这样做可以提高脚本的性能。

`-reset` 开关将终端设置恢复为启动状态。这与使用第 3 章“文件、用户和 Shell 定制”中描述的 `reset` 命令相同。

有几个开关用于更改文本颜色。颜色是黑色、红色、绿色、黄色、蓝色、品红色、青色、白色之一，或者在这些颜色前加上 `bright`。`default` 是默认颜色。`-foreground` 开关设置控制台正常文本颜色。`-background` 设置控制台背景文本颜色。`-ulcolor` 开关设置控制台下划线文本颜色。`-hcolor` 开关设置控制台暗淡文本颜色。

可以通过相应的开关开启或关闭不同的文本样式：`-bold`、`-half-bright`、`-blink`、`-reverse` 或 `-underline`。

```bash
$ setterm -ulcolor bright blue
$ setterm -underline on; printf "This is bright blue!\n" ; \
setterm -underline off
This is bright blue
```

由于 Linux 控制台无法显示下划线，带下划线的文本会以你选择的下划线颜色显示。在这种情况下，颜色是亮蓝色。在 xterm 窗口中，文本实际上是带下划线的。

也可以通过将 `setterm` 的结果存储在变量中来实现同样的效果。

```bash
$ UNDERON=$(setterm -underline on)
$ UNDEROFF=$(setterm -underline off)
$ printf "$UNDERON""This is underlined""$UNDEROFF"\n
This is underlined
```

`-inversescreen` 开关反转控制台的色彩。如果你使用两次，`-inversescreen` 可以使显示器闪烁，以提醒用户重要事件。例如，要闪烁屏幕一秒，请执行以下操作：

```bash
$ setterm -inversescreen on
$ sleep 1
$ setterm -inversescreen off
```

其他有用的开关包括：

- `-cursor`—显示或隐藏输入光标
- `-repeat`—打开或关闭控制台键盘重复
- `-appcrskeys`—打开或关闭光标键应用模式
- `-linewrap`—打开或关闭控制台自动换行

这些功能可以打开或关闭。例如，要隐藏输入光标，请输入以下内容：

```bash
$ setterm -cursor off
```

还有其他属性用于控制如电源节省和 Tab 使用等功能。请参阅本章末尾的参考部分以获取完整的开关列表。

## tput

你可以使用 `setterm` 命令适用于任何终端显示，但尝试使用控制台特有的功能会被忽略。相反，有一个旧命令叫 `tput`（*terminal put*），它的工作方式与 `setterm` 非常相似，但适用于所有纯文本显示。

`tput` 有一个参数；一个基于 `terminfo` 终端数据库的屏幕属性代码。这些代码与 `setterm` 开关不同。你可以在 `terminfo` 手册页（`$ man 5 terminfo`）上找到完整列表。

```bash
$ tput cols # width of display
80
$ tput clear # clear the screen
```

## select 菜单

内置的 `select` 命令创建简单的菜单。`select` 是一个特殊的循环。该命令后跟一个参数列表，并将它们显示为编号选项。当用户通过输入该数字选择一项时，参数会被赋值给 `select` 变量，并且执行 `select` 语句内部的命令。参见列表 13.1。

**列表 13.1 select_demo.sh**
```bash
#!/bin/bash
# # select_demo.sh: a simple select menu
#
shopt -s -o nounset

declare -i
SCRIPT=${0##*/}

printf "\$\n" "Select a document type:"
select ITEM in "orders" "purchase orders" "packing slips" ; do
    if [ -z "$ITEM" ] ; then
        printf "Please choose 1, 2 or 3...\n"
    else
        printf "Processing $ITEM documents...\n"
    fi
done
printf "Done\n"
```

当选择的项目不在列表中时，变量会被赋值为空字符串。循环持续直到读取到 EOF（通常是 Control-D）。

```text
Select a document type:
1) orders
2) purchase orders
3) packing slips
#? 1
Processing orders documents...
#? 4
Please choose 1, 2 or 3...
#?
1) orders
2) purchase orders
3) packing slips
#?
```

旧版本的 Bash 每次遇到 `select` 语句时都会显示菜单。新版本仅在 `REPLY` 变量为空时显示列表，例如当用户在 `select` 提示符处按下 `Return` 键时。

提示符位于变量 `PS3` 中。如果未定义 `PS3`，Bash 使用 `#?` 作为提示符。若要更改提示符，请更改 `PS3` 的值。用户的响应也保存在变量 `REPLY` 中。如果缺少 `in` 部分，Bash 将从脚本参数中选择。

与其他循环类似，`select` 命令可以使用 `break` 和 `continue`。

## 自定义菜单

虽然 `select` 命令可以用很少的工作创建简单的菜单，但它不提供任何用于复杂用户交互的功能。为了提供外观更友好的通信并支持更复杂的屏幕，Linux `dialog` 命令创建弹出文本屏幕对话框。

该命令适用于任何纯文本显示。有几种类型的对话框：

- 背景文本框（`-textbox`）—在处理其他内容时监控命令
- 日历框（`-calendar`）—选择日期
- 复选列表（`-checklist`）—可选择项目的列表
- 文件选择（`-fileselect`）—选择文件
- 进度条（`-gauge`）—温度计图表
- 信息框（`-infobox`）—状态消息
- 输入框（`-inputbox`）—请求用户输入文本
- 菜单（`-menu`）—列出替代选择
- 消息框（`-msgbox`）—带有“确定”按钮的信息框
- 密码框（`-passwordbox`）—请求用户输入文本但隐藏输入
- 单选列表（`-radiolist`）—替代项目列表
- 尾部框（`-tailbox`）—监控命令
- 时间框（`-timebox`）—选择时间值
- 是/否框（`-yesno`）—询问是/否问题
- 文本框
- 是否框

使用 `-yesno` 开关创建是否框。对话框包含带有“是”和“否”按钮的消息。该开关接受三个参数：文本、高度和宽度。所有对话框都有这三个参数。`-defaultno` 开关使“否”按钮成为默认按钮。

例如，要创建一个消息为“你确定吗？”、宽 70 个字符、高 7 个字符并在屏幕居中显示的对话框，你输入以下内容。

```bash
$ dialog -yesno "Are you sure?" 7 70
```

`dialog` 返回的状态码指示选择了哪个按钮：0 是“是”（或其他对话框中的“确定”），1 是“否”（或其他对话框中的“取消”）。状态码为 -1 表示错误或用户通过按下 Escape 键中止了对话框。图 13.1 显示了一个典型的是/否对话框。

你可以通过在消息中嵌入换行代码（\n）将长文本分成单独的行。

```bash
$ dialog -title Testbox -yesno "Delete files:\nAre you sure?" 7 70
```

`-checklist` 开关创建一个复选框列表。基本参数是文本标题、列表的高度和宽度。在这些之后，每个检查列表项使用其名称、项目文本以及指示其当前是否被选中（on）或未选中（off）的信息来描述。选中的项会打印到标准错误。

```bash
$ dialog -checklist "Printer type:" 20 70 14 p1 "p 1" on p2 \
"printer 2" off fax "Fax" off
```

在这种情况下，打印机 1 和传真机被选中。

![](img/7da864b222941ec315ee1c456ff472dd_261_0.png)

**图 13.1** 一个是否对话框。

可以将结果捕获到变量中。由于标准输出用于绘制屏幕，而结果写入标准错误，因此需将标准错误重定向到文件。

```bash
$ declare CHOICE_FILE="/tmp/choice.$$"
$ declare CHOICE
$ dialog --checklist "Printer type:" 20 70 14 p1 "printer 1" on p2 \
"printer 2" off fax "Fax" off 2> "$CHOICE"
$ CHOICE="cat "$CHOICE_FILE""
```

文件选择对话框（见图 13.2）使用 `-fselect` 开关创建。此对话框需要起始目录，以及高度和宽度。

```bash
$ dialog -fselect "$HOME" 10 50
```

![](img/7da864b222941ec315ee1c456ff472dd_261_1.png)

**图 13.2** 一个文件选择对话框。




仪表是一个显示百分比进度的温度计条形图。新的百分比值会逐个从标准输入读取，直到到达文件末尾为止。`~gauge` 开关需要提供一个文本消息、高度、宽度以及一个可选的起始百分比（参见列表 13.2）。百分比可以通过命名管道发送给仪表，这将在第 11 章“文本文件基础”中讨论。

假设你希望显示一个显示打印发票系列文件进度的温度计图形，这些发票文件存储在一个名为 `invoices` 的目录中。下面的演示在发票被发送给另一个名为 `print_invoice` 的脚本时显示发票。

## 列表 13.2 `gauge_demo.sh`

```bash
#!/bin/bash
#
# gauge_demo.sh: a thermometer graph demo

shopt -s -o nounset

declare -rx SCRIPT=$0
declare -rx QUEUE=/status_fifo
declare -rx INVOICES_DIR="invoices"
declare -ix TOTAL_INVOICES=0
declare -ix NUM_INVOICES=0
declare -ix PERCENT=0

# count the invoices waiting to print
TOTAL_INVOICES=$(ls -1 $INVOICES_DIR | wc -l)

# create the pipe
mkfifo $QUEUE
if [ $? -ne 0 ] ; then
    printf "%s\n" "$SCRIPT:$LINENO: unable to create $QUEUE" >&2
    exit 192
fi

# print the invoices in a background subshell
# print the progress to the pipe
(
    cd $INVOICES_DIR
    ls -1 | (
        while read INVOICE ; do
            let "NUM_INVOICES++"
            print_invoice "$INVOICE"
            PERCENT=100*$NUM_INVOICES/$TOTAL_INVOICES
            printf "%d\n" "$PERCENT"
        done
    )
) > $QUEUE &

# display the progress.  dialog will stop when nothing
# more is printed by the subshell
dialog --gauges "Printing invoices" 7 70 0 < $QUEUE

wait          # wait for the subshell to finish
rm $QUEUE     # delete the pipe
sleep 1       # make sure results can be read by user

exit 0
```

*信息框* 是向用户显示的状态消息。它没有按钮，并且 `dialog` 命令立即完成。`--infobox` 开关需要一个文本消息，以及高度和宽度。

```bash
$ dialog --infobox "Connecting to server" 7 70
```

*输入框* 允许用户键入响应。`--inputbox` 开关需要提示文本、高度、宽度以及一个可选的用户默认响应。

```bash
$ dialog --print-size --inputbox "Connect to which host?" 7 70 0  2> size.txt
$ cat size.txt
Size: 7, 70
$ rm size.txt
$ dialog --print-size --no-shadow --nocancel --inputbox \
    "Connect to which host?" 7 70
```

剩余的对话框与前面讨论的类似。

-   *菜单* 是一个用户可以选择选项的列表。`--menu` 开关需要菜单标题文本、高度、宽度和菜单高度。每个项目都由一个标签名和菜单项文本指定。
-   *消息框* 向用户显示一条消息，带有一个单一的**确定**按钮。`--msgbox` 开关需要一个文本消息，以及高度和宽度。
-   *密码框* 类似于输入框，但用户输入的内容不会显示。`--passwordbox` 需要一个文本消息、高度和宽度，以及一个可选的默认密码。
-   *单选列表* 显示一个选项列表，用户只能选择其中一项。`--radiolist` 开关需要标题文本、高度、宽度和列表高度。每个项目的指定方式与复选列表相同。
-   *尾部框* 显示文件中的最后文本，仿佛使用了 `tail -f` 命令。`--tailbox` 开关需要文件名，以及高度和宽度。
-   *文本框* 在对话框中显示文本文件的内容。用户可以浏览该文件。`--textbox` 开关需要文件名、高度和宽度。
-   *背景文本框* 是尾部框和文本框的组合。文本显示效果仿佛使用了 “tail -f” 命令，但用户也可以自由浏览内容。`--textboxbg` 开关需要一个文件名、高度和宽度。
-   *时间框* 允许用户选择时间。`--timebox` 开关需要提示文本、高度、宽度，以及以小时、分钟和秒为单位的初始时间。
-   *日历框*，如图 13.3 所示，显示一个日历并允许用户选择日期。`--calendar` 开关需要提示文本、高度、宽度，以及起始的日、月和年。

![](img/7da864b222941ec315ee1c456ff472dd_264_0.png)

图 13.3 日历对话框。

您可以使用 `--and-widget` 开关组合连续的对话框。

```bash
$ dialog -inputbox "Connect to which host?" 7 70 "" -and-widget -inputbox \
"And what TCP/IP port?" 7 70
```

您必须为输入框提供初始字符串参数（如果没有则使用 `""`），否则 *dialog* 会认为 `-and-widget` 是可选字符串。

有许多用于自定义框的外观和行为的开关。这些列在本章的参考部分中。

## 参考部分

### showkey 命令开关

-   -scancodes（或 -s）— 扫描码转储模式
-   -keycodes（或 -k）— 键码转储模式（默认）
-   -ascii（或 -a）— ASCII 转储模式

### setleds 命令开关

-   -caps—清除大写锁定
-   +caps—设置大写锁定
-   -D—更改控制台标志和 LED
-   -F—更改控制台标志（默认）
-   -L—更改 LED
-   -num—清除数字锁定
-   +num—设置数字锁定
-   -scroll—清除滚动锁定
-   +scroll—设置滚动锁定

### dumpkeys 命令开关

-   -charset=c（或 -c C）—根据字符集 c 解释字符代码值
-   -compose-only—仅显示组合键组合
-   -full-table（或 -f）—以规范形式显示按键绑定
-   -funcs-only—显示功能键字符串定义
-   -keys-only—显示按键绑定，不带字符串定义
-   -long-info（或 -1）—打印有关键盘驱动器的详细信息
-   -numeric（或 -n）—以十六进制格式显示值
-   -short-info（或 -i）—打印有关键盘驱动器的摘要信息

### setterm 命令开关

-   -append [ c ]—将控制台屏幕（默认为当前）转储到文件，如果文件存在则追加
-   -appcursorkeys [on|off]—设置光标键应用程序模式为开或关
-   -background c—将背景文本颜色设置为颜色 c
-   -blank [ 0-60 ]—屏幕变黑之前的分钟数（默认为 0，即不变黑）
-   -blength [ n ]—控制台蜂鸣器持续时间（毫秒）（默认为 0）
-   -bfreq h—控制台蜂鸣器频率（音高）（赫兹）（默认为 0）
-   -blink [on|off]—开启或关闭闪烁文本打印。如果不处于控制台，关闭闪烁文本也会关闭所有其他属性
-   -bold [on|off]—开启或关闭粗体打印。如果不处于控制台，关闭粗体也会关闭所有其他属性
-   -clear [ all|rest ]—清除屏幕并将光标移到起始位置。rest 清除至屏幕末尾
-   -clrtabs [ tab1 tab2 tab2 ... ]—清除制表位
-   -cursor [on|off]—开启或关闭控制台光标
-   -defaultc—将渲染选项恢复为默认值
-   -dump [ c ]—将控制台屏幕（默认为当前）保存到文件
-   -file f—设置 -dump 或 -append 的文件名
-   -foreground c—将前景文本颜色设置为颜色 c
-   -half-bright [on|off]—开启或关闭暗淡打印。如果不处于控制台，关闭暗淡也会关闭所有其他属性
-   -hcolor c—设置半亮字符的颜色
-   -initialize—将绘制特性恢复为默认值
-   -inversescreen [on|off]—反转屏幕颜色
-   -linewrap [on|off]—开启或关闭自动换行
-   -msg [on|off]—启用或禁用 printk 内核消息
-   -msglevel n—将 printk 消息级别设置为 n
-   -reset—将屏幕恢复为开机状态
-   -reverse [on|off]—开启或关闭反色文本打印。如果不处于控制台，关闭反色文本也会关闭所有其他属性
-   -softscroll [on|off]—开启或关闭软键盘滚动
-   -store—将当前渲染选项保存为默认值
-   -tabs [tab1 tab2 tab3 . . . ]—设置制表位位置
-   -term terminal_name—使用 terminal_name 代替 TERM 变量的值
-   -ulcolor c—设置下划线字符的颜色
-   -underline [on|off]—开启或关闭下划线打印。如果支持下划线，则使用 ulcolor

### dialog 命令开关

-   -aspect r—基于提示字符串长度相对于对话框的比例 r，作为强制换行过长行的指南（默认为 9）
-   -backtitle b—要在屏幕顶部的背景上显示的字符串 b
-   -beep—每次屏幕重绘时发出蜂鸣声
-   -beep-after—如果输入中断则发出蜂鸣声
-   -begin y x—对话框左上角的位置，而不是居中
-   -clear—退出时清除屏幕





- `--separate-widget` $s$——对于多个 `--and-widget` 对话框，使用字符串 $s$ 分隔来自不同对话框的结果
- `--shadow`——在对话框周围显示 3D 阴影
- `--sleep` $s$——在处理完一个对话框后延迟 $s$ 秒
- `--stderr`——将消息定向到标准错误输出（默认值）
- `--stdout`——将消息定向到标准输出
- `--tab-correct`——将每个 Tab 字符转换成一个或多个空格
- `--tab-len` $n$——指定 `--tab-correct` 中 Tab 对应的空格数量（默认为 8）
- `--title` $t$——在对话框顶部显示标题 $t$

## 14 函数与脚本执行

我曾与一位牧师讨论过“牧师倦怠”的问题。当人们为从事神职生涯而接受培训时，他们被期望不仅要精通信仰所教授的概念，还要掌握会计、咨询、写作、平面设计以及其他十几种技能。虽然这确保了牧师在推动教众前进所需的所有领域都有现成的背景知识，但这也让许多新的教会领导人产生了一种感觉，即他们必须独自承担教众的需求，无法或不愿将责任委托给他人。没有任何人类能够有效地承担如此多的职责。这种负担往往会导致压力、无助感、情绪崩溃，甚至放弃他们所选的职业。

Shell 脚本是快速解决简单问题的工具。当脚本变得庞大或复杂时，它们会变得难以维护。就像患有“牧师倦怠”的人一样，它们必须将职责委托给其他脚本，并相互协调以完成工作，而不会在负载下崩溃。

### 运行脚本

Bash 脚本是文本文件，而不是包含可执行指令的文件。脚本不能直接执行；它需要一个解释器来执行指令。对于 Bash 脚本而言，解释器就是 Bash 程序。Linux 必须能够找到解释器才能运行脚本。

一种方式是显式运行解释器以启动一个新的 Bash 会话。要运行名为 _delayed_shipments.sh_ 的脚本，您需要将名称作为参数提供给 Bash。

```bash
$ bash delayed_shipments.sh
```

另一种方式要求在第一行使用 `#!` 行。这指定了运行脚本所需的解释器路径名。在这种情况下，`#!/bin/bash` 指定了位于 `bin` 目录中的 Bash shell 的路径名。应该设置脚本的权限位，以允许用户运行脚本。（权限位将在下一章中进一步讨论。）然后，脚本可以在不显式启动 Bash 的情况下运行；Linux 会自动为您启动 Bash。

```bash
$ ./delayed_shipments.sh
```

### Linux 执行环境

正如后面关于导出变量的章节所述，当 Linux 程序运行时，它并不是从“空状态”开始的，而是继承了由前一个程序导出的任何变量。导出的变量被称为环境变量，因为它们成为新程序运行环境的一部分。

变量并不是由原始程序导出的唯一事物。环境包括：

- 打开的文件
- 当前工作目录
- 文件创建模式 *umask*
- 由 *trap* 设置的任何信号处理程序
- 导出的环境变量
- 导出的 shell 函数
- 在调用时启用的选项（默认情况下或通过命令行参数）或由 *set* 启用的选项
- *shopt* shell 选项
- Shell 别名
- 各种进程 ID，包括后台任务的进程 ID、`$$` 的值和 `$PPID` 的值

子 shell 从其父脚本继承其环境。子 shell 的环境由以下内容组成：

- 打开的文件（可能被子 shell 的重定向修改）
- 当前工作目录
- *umask* 值
- 标记为导出的 Shell 变量
- 信号陷阱

与环境变量一样，导出打开文件、工作目录或陷阱的过程是单向的。如果新程序决定关闭标准输出，它只关闭原始程序标准输出的副本。原始程序不会受到新程序操作的影响。整个环境的行为方式相同。

### Source 命令（.）

当一个脚本由另一个脚本执行时，在第二个脚本完成运行后，在脚本中声明的所有变量、别名和其他项都会丢失。结果只能由文件、标准输出或脚本的状态码返回。

相反于运行第二个脚本，您可以将第二个脚本插入到第一个脚本中。内置的 `source` 命令（通常用点号 `.` 缩写）将第二个脚本复制到第一个脚本中，就好像程序员输入了这些行一样。由于第二个脚本被视为第一个脚本的一部分，因此当第二个脚本执行结束时，其中的声明不会丢失。它表现为一个组合后的单一脚本。例如，考虑清单 14.1 中显示的两个脚本。

**清单 14.1 source1.sh**

```bash
#!/bin/bash
#
# source1.sh: including source fragments
#
# Source command example
shopt -s -o nounset

declare -rx SCRIPT=${0##*/}
declare -r source2="source2.sh"

if test ! -r "${source2}" ; then
  printf "SCRIPT: the command ${source2} is not available\n" >&2
  exit 1
fi

source ${source2}
printf "The variable YEAR is %s\n" "$YEAR"
exit 0
```

*source2.sh: 这将被插入到 source1.sh 中*

```bash
declare -r YEAR=$(date +%Y)
```

当脚本运行时，source2.sh 的内容在 source 命令所在的位置插入到原始脚本中。当声明变量 YEAR 时，实际上是在原始脚本中声明它。

```bash
$ bash source1.sh
The variable YEAR is 2003
```

变量 YEAR 在 printf 命令的位置存在；没有错误。

请注意，被 source 的脚本是一个片段，而不是独立的脚本；它不包含 exit 命令或 #! 行。

source 命令可用于定义多个脚本之间共享的常见声明项。这节省了程序员在几个不同的脚本中反复输入相同定义的时间。将声明项放在一个地方也使脚本更易于维护。参见清单 14.2。

**清单 14.2 common.sh**

```bash
# common.sh

# This script contains fragment global definitions and should be executed
# with the source command ( . ).

# Common constants

declare -rx SCRIPT=${0##*/}
declare -r ORDERS_DIR="/usr/local/orders"
declare -r ARCHIVE_DIR="$ORDERS_DIR/archive"
declare -r START_DATE=$(date)
```

脚本片段中的参数指的是包含在 source 命令中的参数，而不是原始脚本。如果 source 中没有包含参数，则使用原始脚本的参数。

您可以使用 `return` 命令提前结束 source 脚本片段。此命令具有与 `exit` 命令相同的格式。如果您使用 `exit`，整个脚本将停止。

由于 source 脚本片段不像程序那样执行，因此它们不需要有执行权限即可运行；它们只需要有读取权限，以便 Bash 可以加载它们。

### 使用 exec 切换脚本

运行脚本的第三种方式是使用内置的 `exec` 命令。当使用 `source` 运行另一个脚本或插入脚本片段时，控制权始终在原始脚本的下一行恢复。相反，`exec` 命令提供了一种无条件切换到新脚本的方式。Bash 完全丢弃原始脚本，且永不返回。参见清单 14.3 和 14.4。

**清单 14.3 exec1.sh**

```bash
#!/bin/bash

# exec1.sh
#
# Source command example
shopt -s -o nounset

declare -rx SCRIPT=${0##*/}
declare -r exec2="./exec2.sh"
if test ! -x "$exec2" ; then
	printf "$SCRIPT:$LINENO: the script $exec2 is not available\n" >&2
	exit 192
fi

exec $exec2 "$@"
```




## 14.3 使用 exec 命令

**exec** 会销毁当前 shell，并用命令行中指定的命令替代它。

```bash
#!/bin/bash
#
# exec1.sh

declare -rx SCRIPT=${0##*/}

exec2="$PWD/exec2.sh"

if [ ! -x "$exec2" ]; then
printf "$SCRIPT: unable to execute $$exec2.\n" >&2
exit 1
fi

printf "$SCRIPT: Transferring control to $$exec2, never to return...\n"
exec "$exec2"

printf "$SCRIPT:$LINENO: exec failed!\n" >&2
exit 1
```

![](img/7da864b222941ec315ee1c456ff472dd_273_0.png)

```bash
#!/bin/bash
#
# exec2.sh

declare -rx SCRIPT=${0##*/}

printf "$$SCRIPT: now running exec2.sh"
exit 0
```

在 `exec1.sh` 中执行 **exec** 命令后，该脚本会被丢弃，Bash 开始执行 `exec2.sh`。当 `exec2.sh` 执行完毕后，`exec1.sh` 不会恢复执行。

```bash
$ bash exec1.sh
exec1.sh: Transferring control to exec2.sh, never to return...
exec2.sh: now running exec2.sh
```

你可以使用 **exec** 命令来运行其他程序，而不仅仅是其他 shell 脚本。如果使用 -c 选项，**exec** 会在运行新程序前销毁所有变量。-i 选项会以用户登录时运行的第一个程序的方式运行该程序（通过在参数 $0 中加入减号实现）。-a 选项可以为 $0 指定一个特定的名称。

除非设置 **execfail** 选项，否则 **exec** 永远不返回。如果没有设置该选项且脚本无法运行新程序，脚本将直接退出。

一个专用命令 **execl** 主要用于作为一系列其他脚本的“前端”脚本。例如，一个脚本可以检查客户发送的文件，对其进行分类，然后使用 **execl** 运行相应的脚本来处理它。由于没有理由返回到原始脚本，**execl** 是合适的命令。

## 编写周期性脚本

Linux 中有几个用于调度周期性任务的命令。主要的调度程序称为 **cron**（意为 *chronological*，按时间顺序的）。**cron** 程序在后台持续运行，在特定时间启动脚本或其他程序。

**crontab**（*chronological table*，时间表）命令维护一个任务列表供 **cron** 执行。每个用户都有自己的 crontab 表。-l（*list*，列出）选项列出当前已调度的任务。如果你没有权限使用 *cron*，Linux 会报告错误。因为作业是成组地从 crontab 表中添加或删除的，所以总是先用 -l 选项开始，并将当前表保存到一个文件中。

```bash
$ crontab -l > cron.txt
```

保存当前表后，可以编辑该文件。有五个列用于指定程序运行的时间：分钟、小时、日期、月份和星期几。未使用的列用星号标记，表示任何合适的时间。时间以多种格式表示：单独的值（1）、逗号分隔的列表（1,15）、范围（0-6, 9-17）以及带步长值的范围（1-31/2）。可以使用名称来表示月份或星期几。

最后一列包含要执行的命令名称。以下行在每天凌晨 1:00 运行名为 cleanup.sh 的脚本。

```bash
* * 1 * * /home/kcburch/cleanup.sh
```

环境变量也可以在 crontab 中初始化。当 shell 脚本由 *cron* 启动时，它不是从登录会话启动的，并且不会执行任何 profile 文件。只有少数几个变量被定义：`PWD`、`HOSTNAME`、`MACHTYPE`、`LOGNAME`、`SHELL`、`HOSTTYPE`、`OSTYPE`、`HOME`、`TERM` 和 `PWD`。你必须在脚本或 crontab 列表中显式设置其他值。

`PATH` 仅定义为 `/usr/bin:/bin`。其他路径通常由 profile 文件添加，因此不可用。

由于在 *cron* 下运行的脚本不在登录会话中，因此没有屏幕可写入标准输出。通常写入标准输出的内容会被 *cron* 捕获并发送到拥有 *cron* 脚本的账户。邮件的标题行是无用的 *cron*。即使打印一个空行也会导致发送看似空的电子邮件。因此，设计为在 *cron* 下运行的脚本应将其输出写入日志文件，或者创建并发送带有有意义标题的电子邮件。常见的做法是编写一个包装脚本，以捕获执行实际工作的脚本的输出。

示例 14.6 中的示例展示了一个包装脚本，它运行示例 14.5 中名为 `show_users.sh` 的脚本。

### 示例 14.5 show_users.sh

```bash
#!/bin/bash

# show_users.sh: show all users in the database table "users"

export -o -O nounset

declare -rx SCRIPT=${0##*/}
declare -rx SQL_CMDS="sort_inventory.sql"
declare -rx ON_ERROR_STOP

if [ ! -r "$$SQL_CMDS" ]; then
printf "$$SCRIPT: the SQL script $$SQL_CMDS doesn't exist or is not \
readable" >&2
exit 192
fi

RESULTS="psql -user gordon -dbname custinfo -quiet -no-align -tuples-only \
-field-separator ',' -file "$$SQL_CMDS"\n
if [ $$ -ne 0 ]; then
printf "$$SCRIPT: SQL statements failed." >&2
exit 192
fi
```

### 示例 14.6 show_users_wrapper.sh

```bash
#!/bin/bash

# show_users_wrapper.sh - show_users.sh wrapper script

shopt -s -o nounset

declare -rx SCRIPT=$(${@##/})
declare -rx USER="kburch"
declare -rx MAIL="/bin/mail"
declare -rx OUTPUT="mktemp /tmp/script_out.XXXXXX"
declare -rx SCRIPT2RUN=./show_users.sh

# sanity checks

if test ! -x "$$MAIL" ; then
printf "$$SCRIPT:$${LINFO}: the command $${MAIL} is not available - aborting" >&2
exit 1
fi

if test ! -x "$$SCRIPT2RUN" ; then
printf "$$SCRIPT:$${LINFO}: the command $${SCRIPT2RUN} is not available\
 - aborting" >&2
exit 1
fi

# record the date for any errors, and create the OUTPUT file
date > $$OUTPUT

# run the script

$SCRIPT2RUN 2>&1 > "$OUTPUT"

# mail errors to USER

if [ $? -ne 0 ] ; then
    $mail -s "$SCRIPT2RUN failed" "$USER" < "$OUTPUT"
fi

# cleanup

rm "$OUTPUT"
exit 0
```

## 编写持续执行脚本

**守护进程**（**daemon**）是一个独立于 shell 会话运行的程序，持续执行某些任务。例如，服务器软件几乎总是守护进程，因为它持续运行，等待客户端请求服务。

Linux 的 **nohup**（*no hang up*，不挂断）命令运行程序，使其在会话断开后不会退出。如果你希望从命令行交互方式启动守护进程，就需要这个命令。*nohup* 略微降低程序的优先级，并且如果标准输出打开，则将其重定向到名为 **nohup.out** 的文件，因为一旦 shell 会话终止，就不再拥有标准输出来写入。

一般来说，需要一个前端脚本来设置并启动守护脚本。为了避免生成 **nohup.out** 文件，使用 *exec* 将标准输出关闭或重定向到守护脚本是良好的设计实践。此外，*nohup* 不会自动将命令置于后台。前端脚本必须使用 *&* 来完成此操作。

例如，示例 14.7 和 14.8 展示了一对检查进入名为 **ftp_incoming** 的目录中的文件的脚本。

### 示例 14.7 ftp_daemon.sh

```bash
#!/bin/bash
#
# ftp_daemon.sh: a script fragment for the wrapper.

shopt -s -o nounset

declare -rx SCRIPT=${0##*/}
declare -rx INCOMING_FTP_DIR="/home/ftp/ftp_incoming"

cd $INCOMING_FTP_DIR
while true; do
    # Do something to files in the incoming directory here
done
```

示例 14.8 展示了一个将 ftp_daemon.sh 守护进程化的包装脚本。

### 示例 14.8 ftp_daemon_wrapper.sh

```bash
#!/bin/bash
#
# ftp_daemon_wrapper.sh - start our sample daemon
#

shopt -s -o nounset

declare -rx SCRIPT=$0##//)
declare -rx DAEMON="ftp_daemon.sh"
declare -rx DAEMON_LOG="ftp_daemon.log"

if test -f "$DAEMON_LOG" ; then
    if test ! -w "$DAEMON_LOG" ; then
        printf "\$\n" "SCRIPT:$LINENO: unable to write to the log file\
—aborted" >&2
        exit 1
    fi
fi

# Standard Output is now the log file
# Redirect Standard Error there as well

exec 1>$DAEMON_LOG
exec 2>&1

# Start the daemon in the background

nohup bash ftp_daemon.sh &
echo "Daemon $DAEMON started"
exit 0
```

守护进程本身是一个具有无限循环的脚本。有两种检查待办任务的方法。第一种是轮询，守护进程检查是否有工作要做。如果没有工作，它会休眠几秒钟，释放 CPU 时间供其他任务使用，然后再进行检查。

示例 14.9 中显示的脚本每 30 秒检查一次名为 ftp_incoming 的目录中是否有新到达的文件。如果文件超过 30 分钟未更改，则它们的名称会被加上时间戳，并且文件会被移动到一个名为 processing 的新目录中。




# 列表 14.9 	 polling.sh

```bash
#!/bin/bash
#
# polling.sh: a daemon using polling to check for new files

shopt -s -o nounset

declare -rx SCRIPT=${0##*/}
declare -rx INCOMING_FTP_DIR="/home/ftp/ftp_incoming"
declare -rx PROCESSING_DIR="/home/ftp/processing"
declare -rx statftime="/usr/bin/statftime"
declare FILE
declare FILES
declare NEW_FILE

printf "$SCRIPT started at %s\n" "$(date)"

# Sanity checks

if test ! -r "$INCOMING_FTP_DIR" ; then
    printf "%s\n" "$SCRIPT:$LINENO: unable to read the incoming directory - aborted" >&1
    exit 1
fi
if test ! -x "$PROCESSING_DIR" ; then
    printf "%s\n" "$SCRIPT:$LINENO: unable to read the incoming directory - aborted" >&1
    exit 1
fi
if test ! -r "$statftime" ; then
    printf "%s\n" "$SCRIPT:$LINENO: unable to find or execute $statftime - aborted" >&1
    exit 1
fi

# Poll for new FTP files

cd $INCOMING_FTP_DIR
while true; do

    # Check for new files more than 30 minutes unchanged
FILES=`find . -type f -mmin +30 -print`

# If new files exist, move them to the processing directory

if [ ! -z "$FILES" ] ; then
    printf "$SCRIPT: new files have arrived at %s\n" "$(date)"
    printf "\n" "$FILES" | {
        while read FILE ; do
            # Remove leading "./"
            FILE="${FILE#./}"
            # Rename the file with the current time
            NEW_FILE="$STATFTIME -f "%L_%T.dat" "$FILE""
            if [ -z "$NEW_FILE" ] ; then
                printf "\n" "$SCRIPT:$LINENO: statftime failed to create a new filename - skipping"
            else
                # Move the file to the processing directory
                printf "\n" "$SCRIPT: moved $FILE to $PROCESSING_DIR/$NEW_FILE"
                mv "$FILE" "$PROCESSING_DIR/$NEW_FILE"
            fi
        done
    }
    sleep 30
done

printf "$SCRIPT finished unexpectedly at %s\n" "$(date)"
exit 1
```

该脚本可以使用*阻塞*代替轮询。通过用 `suspend` 命令替换 `sleep` 命令，脚本将无限期休眠，直到通过 `kill -SIGCONT` 命令唤醒。当一个脚本依赖另一个脚本时，这非常有用。

守护脚本会一直运行，直到它被 `suspend` 或 `kill` 命令停止。它可以启动为在后台运行并自动重启自身：

```bash
$ { ( while true ; do nohup bash polling.sh ; done ; ) \
>/dev/null 2>&1 </dev/null & } &
```

此命令行创建两个进程。外层进程将标准输入、输出和错误重定向到 `/dev/null`，因为它们不再适用。内层进程在 `while` 循环中重复 bash 脚本。当命令提示符返回时，使用 `ps` 命令可以看到 `polling.sh` 脚本正在运行。（可以通过使用 `exec` 在 `while` 循环前关闭标准输入、输出和错误，从而消除其中一个命令分组。）

## Shell 函数

函数是将小型子脚本嵌入 Bash 脚本中的方法，无需将它们保存在单独的文件中。由于它们嵌入在脚本中，因此使用时无需加载。这反过来使它们比单独的脚本运行得更快。像单独的脚本一样，函数可用于将复杂脚本分解为单独的、命名的任务，以提高可读性。

Shell 函数与其他编程语言中的函数不同之处在于，它们返回状态码而不是返回值。由于没有返回值，它们不能用于表达式中。

与变量一样，函数必须在使用之前声明。函数使用 *function* 命令而不是 *declare* 命令进行声明。每个函数都有一个名称，组成函数的语句用花括号包围。参见列表 14.10。

# 列表 14.10 function.sh

```bash
#!/bin/bash
#
# function.sh - A simple function example

declare -rx SCRIPT=${0##*/}
declare -rx TMP="/tmp/temp.$$"
declare -rx TRASH_DIR="$HOME/.trash"

# $TRASH_TMP
#
# Move the TMP file to the trash directory

function trash_tmp {

  if test ! -d "$TRASH_DIR" ; then
    printf "%s\n" "$SCRIPT:$FUNCNAME:$LINENO: trash directory \
$TRASH_DIR is missing" >&2
    exit 1
  fi
  if test -f "$TMP" ; then
    mv $TMP "$TRASH_DIR/."
  fi
}

readonly -f trash_tmp
declare -t trash_tmp

printf "This is a function test\n" > $TMP
trash_tmp

exit 0
```

函数 `trash_tmp` 将 `TMP` 文件移动到用户主目录中名为 `trash` 的目录。函数由 `function` 命令创建，但直到在程序中明确命名才会执行。

`readonly` 命令防止函数被重新定义。该命令将在本章后面详细讨论。

通常，函数不会执行 `DEBUG` 陷阱。`declare -t` 开启函数中的调试陷阱执行。

与脚本类似，函数可以有参数。虽然参数 `$0` 保留脚本的路径名，但其他参数是提供给函数的参数，`$#` 指示参数的数量。当函数完成时，参数变量恢复为之前的值。

`FUNCNAME` 变量在函数执行期间包含函数的名称。在报告错误时使用 `$SCRIPT:$FUNCNAME:` 可以识别发生错误的脚本和函数。

因为函数不是子脚本，函数返回状态码的方式以及声明变量的方式不同。

在脚本中，`exit` 命令返回状态码。在函数中，`exit` 命令退出包含该函数的脚本。要在不退出脚本的情况下返回状态码，函数使用 `return` 命令代替。`return` 语句的使用方式与 `exit` 语句相同。

### 局部变量

在函数内部声明的变量仅在函数持续期间存在。这些被称为*局部变量*。当函数完成时，变量会被丢弃，就像子脚本丢弃变量一样。参见列表 14.11。

# 列表 14.11 function2.sh

```bash
#!/bin/bash
#
# function2.sh: A simple function example with local variables
#
shopt -s -o nounset

declare -rx SCRIPT=$0##*/
declare -rx TMP=/tmp/temp.$$*

# TRASH FILE
#
# Move the specified file to the trash directory
# The first parameter is the file to move

function trash_file {
declare -r TRASH_DIR="$HOME/.trash"

if test ! -d "$TRASH_DIR" ; then
printf "%s\n" "$SCRIPT:$FUNCNAME:$LINENO: trash \
directory $TRASH_DIR is missing" >&2
return 1
fi
if test -f "$1" ; then
mv $1 "$TRASH_DIR"/
fi
return 0
}
readonly -f trash_file
declare -t trash_file

printf "This is a function test\n" > $TMP
trash_file $TMP
if [ $? -ne 0 ] ; then
printf "%s\n" "$SCRIPT:$LINENO: unable to trash $TMP--aborting" >&2
exit 1
fi

exit 0
```

在 function2.sh 中，变量 TRASH_DIR 仅存在于函数 trash_file 内部。当发生错误时，函数不会退出脚本，而是返回一个状态码来指示其是否成功，从而让主脚本决定是否应该退出。

`local` 命令也可以在函数内部声明局部变量并分配初始值。然而，`local` 缺少 `declare` 命令使用的其他开关。因此，最好使用 `declare` 命令代替。

如果未明确声明新变量，当函数完成时，它们不会被丢弃。这种行为是为了与 Bourne shell 保持向后兼容，但可能导致变量意外残留。

```bash
$ function f { COMPANY="NightLight Inc." ; } 
$ f
$ printf "%s\n" "$COMPANY"
NightLight Inc.
```

在此示例中，变量 COMPANY 在微小的 f 函数结束时没有被丢弃，因为它未在 f 内部正式声明。

```bash
$ function f { declare COMPANY="Nightlight Inc." ; }
$ f
$ printf "$a\n" "$COMPANY"
$
```

## 递归和嵌套函数

在 Bash 中，函数可以嵌套或递归使用。局部变量与嵌套函数共享。参见列表 14.12。

# 列表 14.12 factorial.sh

```bash
#!/bin/bash
#
# factorial.sh: A recursive function example
#
shopt -s -o nounset

declare -rx SCRIPT=$0##*/
declare -i REPLY

# FACTORIAL : compute a factorial
#
# $1 is the number to compute the factorial for

function factorial {
	declare -i RESULT=1			# shared with factorial1

	function factorial1 {
		declare -i FACT=$1		# the current number
		let "FACT--"			# deduct one
		if [ $FACT -gt 1 ] ; then
			factorial1 $FACT	# repeat
			let "RESULT=RESULT*FACT"	# and multiply in result
		else
			RESULT=1			# factorial of 1 is 1
		fi
		return				# leave function
	}
}
```





清单 14.12 *续*

```
def factorial $( # start with param 1
 printf "$!\n" $RESULT
)
readonly -f factorial
declare -t factorial

printf "Factorial of what number? -> "
read REPLY
factorial $REPLY
exit 0
```

当函数名与内置命令名称相同时，可能会发生意外的递归。当函数覆盖内置命令时，使用 `builtin` 命令来执行命令，而不是执行该函数。

```
function ls (
 command ls -CFP $*
)
readonly -f ls
declare -t ls
```

如果没有 `command` 内置命令，该函数将陷入永无止境的递归。

## 函数属性

与变量一样，函数也有属性。由于函数不是通过 `declare` 命令声明的，因此使用不同的命令来更改函数属性。

使用带有 `-f` (*函数*) 选项的 `export` 命令可以将函数共享给子 shell。

```
export -f trash_file
```

在用户的启动配置文件中创建的导出函数充当比 shell 别名更强大的版本。

因为函数是通过命令声明的，所以可以使用 `unset -f` 随时重新定义或丢弃函数。在脚本中，这是一种危险的做法，因为删除或重新定义函数会使你的脚本难以调试。当脚本因错误而意外停止时，可能很难知道当时定义的是哪个版本的函数。

结构良好的脚本会在脚本顶部附近创建函数，并使用 `readonly` 命令设置只读属性。

```
readonly -f trash_file
```

只读函数不能被取消设置或重新定义。
使用 `declare` 命令和 `-F` (函数) 选项可以列出当前函数。使用 `-p` 选项可以连同所有变量一起列出完整的函数。

也可以使用旧的 Bourne shell 语法创建函数，即省略 “function” 一词，并在函数名称后添加一对空括号。

## 参考部分

### exec 命令选项

- -c—使 exec 在运行新程序之前销毁所有变量
- -l—以用户登录时运行的第一个程序的方式运行该程序
- -a n—为 $0 指定不同的程序名称 n

### crontab 命令选项

- -u user—列出要修改的 crontab 所属的其他用户名称
- -l—列出当前的 crontab
- -r—删除当前的 crontab
- -e—使用默认编辑器编辑当前的 crontab

# 15
Shell 安全

**系**统安全往往是一把双刃剑。许多公司在系统管理工具上花费了大量资金；通常他们未对管理员人员进行充分培训。系统资源短缺的第一个消息必然来自程序员自己。

在我曾任职的一家公司，官方政策是防止系统上的程序员访问性能监控工具。当管理负责人发现这些工具可以访问时，他下令使其安全化。几周后，员工们悄悄重新启用了这些工具，因为禁用它们阻碍了公司的第一道防线。

Shell 脚本中的安全性，就像系统安全一样，并非要将所有东西都收紧到脚本几乎无法运行的程度，而是要确保脚本不会做出任何不必要的假设，从而使移植到新系统或调试困难问题变得雪上加霜。它涉及在紧急情况下或在同事恶意破坏时使脚本具备防崩溃能力。就像使用 `nounset` shell 选项一样，更多的安全性意味着更少的维护。

## 基本的 Linux 安全模型

Linux 上的所有文件都有所有者和组。但是谁拥有文件？每个文件都被分配了特定登录的用户 ID 号。用户进一步分为组，每个用户被分配一个组号。最初，Unix 将用户分配给一个单一的组，称为主要的 `gid`。BSD 4.3 引入了额外的补充组。就文件而言，用户必须拥有一个主要或补充组，以匹配文件的 `GID`，才有资格获得组访问权限。

每个 Linux 用户都有一个 `uid`（用户 ID 号），并且 Linux 系统上的每个文件都有一个 `uid` 号，表明谁拥有该文件。

`numeric-uid-gid` `ls` 选项显示八进制数，而不是文件 `uid` 和 `gid` 所有者的名称。

$ id
uid=500(ken) gid=100(users) groups=100(users),14(uucp),16(dialout)

$ ls -numeric -uid -gid -l
total 11068
drwx— 2 500 100 4096 Dec 5 2000 Mail
drwxr-xr-x 11 500 100 4096 Jan 23 00:52 archive
-rw-r-r— 1 500 100 267 Nov 30 09:33 script.sh
-rw-r-r— 1 500 100 36 Feb 12 11:51 company.txt
-rw-r-r— 1 499 100 309 Feb 12 15:45 eval_example.sh

大多数文件由用户 500 (ken) 和主组 100 (users) 拥有。因为我的登录名是 ken，除了最后一个文件外，我在所有文件上都具备所有者访问权限。因为 eval_example.sh 由其他人拥有，但属于我的组之一，如果尝试访问该文件，则应用组访问权限。
只有文件的所有者才能删除它。
每个文件都有一个文件访问权限号，指示哪些用户可以访问它。文件权限中的每一位表示执行某些类型操作的权利，如读取文件、写入文件或执行程序。

文件权限分为三位的组。每组表示特定类型用户的访问权限。由于三位组成一个八进制（基数 8）数字，因此权限通常写作四个八进制数字。最右边的数字代表不属于任何其他类别的用户的访问权限：这些通常称为“其他”或“全球”权限。从右数第二位代表与文件在同一组中的用户的访问权限。第三位代表文件所有者的访问权限。例如，/tmp 目录的用户权限数为 777，表示任何用户都有完全权限。

对于目录，读取访问表示读取目录内容的能力。写入访问允许用户在目录中创建新文件，实际上是“写入”一个新的目录项。因为目录永远不能被执行，所以执行权限允许程序搜索目录内容。如果没有执行权限，用户只有在知道名称的情况下才能在目录中运行程序。

每个三位组内各位的含义部分取决于文件的类型。左边的位指示读取文件的能力。中间的位启用写入。右边的位使文件可执行，或者在目录的情况下，使当前目录能够移动到该目录。常见的用户权限数 755 表示文件可以被任何人读取或执行，但只有文件的所有者可以进行更改。

以下是各位的完整分解。

- 1 (八进制 1)—其他人执行
- 2 (八进制 2)—其他人写入
- 4 (八进制 4)—其他人读取
- 8 (八进制 10)—组执行
- 16 (八进制 20)—组写入
- 32 (八进制 40)—组读取
- 64 (八进制 100)—用户执行
- 128 (八进制 200)—用户写入
- 256 (八进制 400)—用户读取
- 512 (八进制 1000)—粘滞位
- 1024 (八进制 2000)—设置 gid
- 2048 (八进制 4000)—设置 uid

`ls` 命令不显示八进制数字。相反，它显示位列表，`-rwxrwxrwx.` 当出现字母时，对应的位是开启的。减号表示访问权限已关闭。

实际的 Linux 安全模型要复杂得多，有更多的 ID 号类型，但这些不影响 shell 脚本编程。第四个也是最左边的权限数字代表特殊程序和目录的访问权限。这些将在本章后面的 chmod 部分中介绍。通常，这个数字是零。

超级用户、root 或 uid 0 始终拥有所有文件的完全访问权限。

## 了解你是谁 (id)

Linux `id` 命令识别你的登录名称和组，以及你所属的任何补充组。该命令显示名称和相应的数字。

```
$ id
uid=503 (kburtch) gid=503 (kburtch) groups=503 (kburtch)
```

在当前会话下创建的任何文件都属于 `uid` 并隶属于组 `gid`。

```
$ touch temp.txt
$ ls -l temp.txt
-rw-rw-r-- 1 kburtch kburtch 0 Jun 25 11:45 temp.txt
```

各种 ID 选项会隐藏部分信息。`--user` (或 `-u`) 选项仅打印 `uid` 信息。`--group` (或 `-g`) 选项仅打印组信息。`--groups` (或 `-G`) 选项仅打印补充组信息。`--real` (或 `-r`) 选项显示实际 uid 或 gid，而不是有效 uid 或 gid。`--name` (或 `-n`) 选项仅显示名称，而不显示数值。

```
$ id --user --real --name
kburtch
```





## 转移所有权（chown/chgrp）

Linux 的 `chown`（*更改所有者*）命令用于更改文件的所有者。要使用 `chown`，必须是文件的所有者。只有 root 可以使用 `chown` 更改所有权。普通用户也可以用它来更改组，前提是该用户也是目标组的成员。

所有者可以是数字 *uid* 或名称。

```bash
$ chown order_sys orders.txt
```

`--reference` 开关可以从另一个文件复制所有权信息。

```bash
$ chown --reference=last_orders.txt orders.txt
```

为了在开关方面提供额外的安全性，`--from` 开关可以在更改为新的所有者之前验证旧的所有者。`--reference` 和 `--from` 开关不能在一个单独的 `chown` 命令中组合使用。

```bash
$ chown --from="kburtch" order_sys orders.txt
```

当所有者后面跟有一个冒号和组名时，`chown` 会同时更改所有者和组。如果缺少组部分，组将设置为主人的组。如果缺少所有者部分，则只更改所有者。也可以使用冒号在 `--from` 开关中指定组。

```bash
$ chown order_sys:ngroup orders.txt
```

`--recursive`（或 `-R`）开关递归更改子目录中的文件。`--changes`（或 `-c`）开关会通告每次更改。`--verbose`（或 `-v`）开关提供更多详细信息。`--quiet`（或 `-silent` 或 `-f`）开关隐藏错误消息。`--dereference` 开关取消符号链接的引用（即操作链接指向的文件而非链接本身）。

使用 `chown` 来确定谁可以访问脚本及其相关文件，从而最大程度地减少隐藏脚本问题可能导致的麻烦。

避免在超级用户登录下运行脚本。在超级用户登录下运行的脚本可以更改任何文件的所有者。然而，如果你发现为了运行执行系统管理以外任务的脚本而必须使用超级用户登录，这就表明文件的所有权设置不正确。请更改文件的所有者，甚至创建一个新的虚拟用户来拥有这些文件，而不是在超级用户登录下运行。超级用户脚本中的错误影响范围广泛，非常危险，且难以追踪。

Linux 的 `chgrp`（*更改组*）命令是 `chown :group` 的简写形式。`chgrp` 仅更改所属组。

## 更改访问权限（chmod）

就像 `chown` 用于更改文件所有权一样，Linux 的 `chmod`（*更改模式*）命令用于更改文件的权限。该名称源自 Linux 术语 *file mode*（文件模式），它由权限位和一些其他文件信息组成的数字。尽管名称暗示该命令可以更改任何文件模式设置，但此命令仅更改访问权限。

权限可以用两种方式表示。

首先，它们可以用四位八进制权限数字表示。

```bash
$ touch orders.txt
$ ls -l orders.txt
-rw-r-- 1 ken users 0 May 9 12:48 orders.txt
$ chmod 0755 orders.txt
$ ls -l orders.txt
-rwxr-xr-x 1 ken users 0 May 9 12:48 orders.txt
```

对于不习惯使用八进制数字的人，可以使用加号添加权限，或使用减号移除权限。权限按用户 (u)、组 (g)、其他人 (o) 或所有 (a) 进行分组，并可以拥有读取 (r)、写入 (w) 或执行 (x) 权限。因此，要为文件和文件的组添加读取权限，可以这样做：

```bash
$ chmod 0000 orders.txt
$ ls -l orders.txt
------ 1 ken users 0 May 9 12:48 orders.txt
$ chmod ug+r orders.txt
$ ls -l orders.txt
-r-r--- 1 ken users 0 May 9 12:48 orders.txt
```

要移除非文件所有者且不在同一组内的用户的写入权限，可以这样做：

```bash
$ chmod a+rwX orders.txt
$ ls -l orders.txt
-rwxrwXrwx 1 ken users 0 May 9 12:48 orders.txt
$ chmod o-w orders.txt
$ ls -l orders.txt
-rwxwR-rx-x 1 ken users 0 May 9 12:48 orders.txt
```

等号会使权限设置为指定值，而不是将其加到或减自现有权限集。字母 u、g 和 o 分别指代用户、组和其他访问位的当前值。例如，g=u 将组权限设置为用户权限相同的值。

```bash
$ chmod 0755 orders.txt
$ ls -l orders.txt
-rwxr-xr-x 1 ken users 0 May 9 12:48 orders.txt
$ chmod g=u orders.txt
$ ls -l orders.txt
-rwxrwXr-x 1 ken users 0 May 9 12:48 orders.txt
```

另一个简写符号，x，仅当文件是目录或者已经对某些用户具有执行权限时，才分配执行权限。

除了 r、w 和 x 之外，还有三个可以更改的特殊访问位。它们都位于文件权限数字最左侧的八进制位中：set_uid 或 set_gid（s），或者所谓的“在交换设备上保存程序文本”（t）位。

t 权限通常称为粘滞位（sticky bit），主要用于临时文件目录。通常，只有文件的所有者可以删除文件。设置粘滞位后，文件的所有者或该文件所在目录的所有者可以删除该文件，这使得编写临时文件清理脚本变得更容易。任何人都可以向设置了粘滞位的目录中添加文件。粘滞位对其他类型的文件没有意义；即使可以设置它，它也会被忽略。在其他一些 Unix 版本中，粘滞位具有其他含义。

下一节将描述设置 setuid/setgid 位的效果。这些位对 shell 脚本没有影响。

chmod 不会更改符号链接。Linux 忽略符号链接上的权限，它们始终显示为 0777 权限。唯一重要的访问权限是符号链接所指向文件的权限。如果无法访问某个文件，通过符号链接也无法访问它。

chmod 的开关与 chown 命令相同，但没有用于验证旧权限的 -from 开关。

如果没有出现 g、o 或 a，权限将如同输入了 a 一样应用，但只允许合理的更改。什么是合理的更改？这由 umask 命令决定。

使用 chmod 来限定有权访问文件的用户如何更改该文件。正确的权限应反映文件的使用方式。如果文件不经常更新，请移除写入权限以保护其免受意外更改。如果文件由其所有者维护，仅由其组读取，请移除组的写入权限。具有 777 权限的文件是程序员工作马虎或忙碌的顾问匆忙工作的迹象。

在大多数情况下，你不想让其他用户对文件有任何访问权限；请移除其他用户的所有访问权限。如果你无法移除其他用户的所有访问权限，请考虑更改文件的所有权。

运行脚本的用户必须始终能够读取它。与普通程序不同，执行权限并不允许用户运行脚本。因为 Bash 必须加载脚本才能执行它，所以脚本必须是可读的。如果你希望用户能够直接运行脚本，而无需引用 Bash 程序，请同时包含执行和读取权限。

不要依赖目录的访问权限来保护文件。文件将来可能会移动的可能性始终存在；移动文件不应改变对其包含数据的访问方式。

## 默认访问权限（umask）

Bash 使用内置的 `umask` 命令确定文件的默认访问权限。`umask`，即 *用户文件创建掩码*，是一个指示哪些访问权限通常被禁止的数字。单独运行 `umask` 会以八进制数显示当前的 `umask` 值，而 `-s` 开关则显示 `umask` 允许哪些位。

```bash
$ touch newfile.txt
$ ls -l newfile.txt
-rw-rw-r-- 1 kburcht kburcht     0 May 22 11:34 newfile.txt
$ umask
0002
$ umask -S
u=rw, g=rw, o=rx
```

在此示例中，`umask` 设置为 2，这意味着位 2（其他用户可以写入文件）通常应为关闭状态。`touch` 命令赋予了所有用户读取和写入权限，除了不被允许写入的其他用户。

你可以通过指定八进制数或权限字符串来创建新的 `umask` 值。

```bash
$ umask 0
$ rm newfile.txt
$ touch newfile.txt
$ ls -l newfile.txt
-rw-rw-rw- 1 kburcht kburcht     0 May 22 11:40 newfile.txt
```

在 `umask` 为 0（允许所有权限）的情况下，`touch` 命令创建了一个任何人可写或可读的文件。

遵守 `umask` 命令完全取决于单个脚本或命令。Bash 中没有任何内置机制强制程序检查 `umask` 值。在脚本中应用 `umask` 很繁琐，因为 `umask` 和权限都使用八进制表示法，但如清单 15.1 所示，这是可以做到的。

### 清单 15.1 calculate_mode.sh

```bash
#!/bin/bash
#
# calculate_mode.sh: 展示如何遵守 umask 的片段

DESIRED_MODE="$1"
# 从八进制转换为十进制
DESIRED_MODE_DECIMAL=`printf "\$d" 0*$DESIRED_MODE`
# 获取 umask 并转换为十进制
UMASK_DECIMAL=`printf "$d" \`umask\`
# 反转 umask 中的位，使设置的位代表允许的位
let "UMASK_INVERT=~$UMASK_DECIMAL"
# 仅允许 umask 允许的位
```





## 清单 15.1（续）

```bash
let EFFECTIVE_MODE=DESIRED_MODE_DECIMAL & UMASK_INVERT
# Convert back to octal
MODE=$(printf "%o" "$EFFECTIVE_MODE")
printf "Desired mode = %d\n" $DESIRED_MODE
printf "Umask id = %d\n" umask
printf "Effective mode = %d\n" $MODE
```

使用掩码值为 2 时，全员读写权限的结果如下：

```bash
$ sh calculate_mode.sh 666
Desired mode = 666
Umask id = 0002
Effective mode = 664
```

如果使用 umask 的 -p 开关，umask 命令会打印出恢复当前 umask 值所需的 umask 命令。

## setuid/setgid 与脚本

有时程序需要代表多个人执行操作。例如，Linux 的 lp 命令代表计算机上的用户打印文件。程序不是以特定用户的所有权运行，而是可以以其自身的权限（即创建者的权限）运行。为了实现这一点，Linux 提供了 setuid 和 setgid 权限。当设置这些权限时，程序将临时以创建者的权限运行，而不是以运行该程序的人的权限运行。

setuid 和 setgid 权限在某些情况下是必要的，但它们也会引入安全漏洞。如果程序存在漏洞，可能会允许用户执行绕过正常系统安全机制的操作。当 setuid 或 setgid 程序代表超级用户进行操作时，这尤为危险。

对于 Bash 脚本，Bash 会忽略脚本上的 setuid 和 setgid 位。脚本始终以运行该脚本的所有者的身份运行。毕竟，脚本是数据，而不是以特定所有者身份运行的编译后的程序。

如果脚本绝对需要以 setuid 或 setgid 方式运行，可以创建一个简短的 C 语言“包装”程序来运行脚本，然后在该 C 程序上设置 setuid 或 setgid。当包装程序运行时，它先以包装程序的所有者身份运行，然后再运行 Bash 脚本。

使用包装程序有两个缺点。首先，从安全角度来看是有风险的。除非脚本是为大量用户的需求服务的，否则 setuid 可能会向过多的人开放访问权限。在更改权限时，很容易忘记处理包装程序或脚本。脚本也比编译后的程序更敏感于环境和退出状态的变化。作为包装程序的替代方案，可以考虑使用 Linux sudo 命令。

其次，包装程序会给机器带来额外的负载，因为必须运行两个程序而不是一个。好的做法是尽量避免使用包装程序，除非绝对必要，并尽可能应用许多安全检查。

## chroot 命令

Linux 的 chroot 命令仅对超级用户脚本可用。chroot 更改根目录 / 的表观位置。通过移动根目录，你可以将脚本可访问的文件隔离到文件系统的特定分支中。

chroot 可以应用于命令。要运行的命令必须出现在新的目录结构中，并且路径应相对于新的根目录。

```bash
$ chroot /home/kburtch ls /
```

在此示例中，ls 指的是 /home/kburtch/bin/ls；ls 必须位于 kburtch 目录中。

现在，ls 无法访问 /home/kburtch 之外的文件。当 / 被修改后，除了使用新的根目录结束会话外，没有办法撤销 chroot。

如果没有指定命令，chroot 假设新根目录下有一个名为 /bin/sh（通常是指向 Bash 的链接）的命令，并尝试启动一个新的 shell 会话。例如，此命令

```bash
$ chroot /home/kburtch/
```

通过运行 /home/kburtch/bin/sh 启动一个新的 shell 会话。目录 / 现在指的是 /home/kburtch/。对 orders.txt 的引用现在指的是 /home/kburtch/orders.txt。

chroot 通过限制可访问的目录，为超级用户脚本提供了一定程度的安全性。但是，使用 chroot 时要小心。在之前的示例中，脚本无法访问 /usr/bin 中的任何 Linux 命令，因为该目录再也无法被“看到”。脚本所需的任何 Linux 命令都必须链接到 chroot 使用脚本可见的目录中。

## 资源限制（ulimit）

内置命令 ulimit 对脚本的资源使用设置限制。与 chroot 类似，该命令为脚本运行的环境设置边界。资源指的是操作系统限制，例如允许打开的文件数量或程序可以请求的最大内存量。

单词 unlimited 表示没有限制。-a 开关显示所有资源限制的列表。

```bash
$ ulimit -a
core file size          (blocks, -c) 0
data seg size          (kbytes, -d) unlimited
file size               (blocks, -f) unlimited
max locked memory    (kbytes, -l) unlimited
max memory size      (kbytes, -m) unlimited
open files              (-n) 1024
pipe size              (512 bytes, -p) 8
stack size            (kbytes, -s) unlimited
cpu time              (seconds, -t) unlimited
max user processes        (-u) 1024
virtual memory        (kbytes, -v) unlimited
```

单独的开关指定特定的资源：

- `-c`—核心文件的最大大小
- `-d`—进程数据段的最大大小
- `-f`—Shell 创建的文件的最大大小
- `-l`—可以锁定的最大内存量
- `-m`—最大常驻集大小
- `-n`—打开文件描述符的最大数量
- `-p`—管道大小（无法设置）
- `-s`—最大堆栈大小
- `-t`—最大 CPU 时间
- `-u`—单个用户的最大进程数
- `-v`—Shell 可用的最大虚拟内存量

每个资源都有一个最大的硬限制和一个当前的软限制，软限制可以是高达最大值以内的任何数量。例如，堆栈大小可以既有硬限制也有软限制。你可以使用 -H（硬限制）和 -S（软限制）开关来检查这些限制。

```bash
$ ulimit -H -s
unlimited
$ ulimit -S -s
8192
```

这里的堆栈大小限制为 8K，但可以更改为任意字节数。要更改限制，请向 ulimit 命令提供新值

```bash
$ ulimit -S -s 16384
$ ulimit -S -s
16384
```

特殊值 hard 和 soft 分别指当前的硬限制或软限制。使用它们将一个限制复制到另一个限制。

```bash
$ ulimit -H -s soft
$ ulimit -H -s
16384
```

## 受限 Shell

当 Bash 以 rbash 名称启动或在运行 Bash 时提供 -r 选项时，Bash 进入受限模式。受限 shell 防止脚本或用户在当前目录之外创建或访问文件。特别是，受限 shell 具有以下限制：

- 不能用 cd 更改目录
- 不能设置或取消设置 SHELL、PATH、ENV 或 BASH_ENV 的值
- 不能指定包含 / 的命令名称
- 不能将包含 /（斜杠）的文件名作为内置命令的参数
- 不能将包含斜杠的文件名作为 hash 内置命令 -p 选项的参数
- 不能在启动时解析 shell 环境中 SHELLOPTS 的值
- 不能使用 <, |, <, >, >> 重定向运算符重定向输出
- 不能使用 exec 内置命令将 shell 替换为另一个命令
- 不能使用 enable 内置命令的 -f 和 -a 选项添加或删除内置命令
- 不能指定内置命令的 -p 选项
- 不能用 set +r 或 set +o restricted 关闭受限模式
- 不能导出 shell 函数

除此之外，受限的 Bash shell 与普通 shell 的操作方式相同。这些限制是在读取任何启动文件之后强制执行的，因此 profile 文件可以在不受限制的情况下设置用户环境。唯一的例外是函数定义不能在启动时导入。

```bash
$ bash -r
$ cd ..
bash: cd: restricted
$ echo $DATE > temp.txt
bash: temp.txt: restricted: cannot redirect output
$ NOW="date"
$ printf "$a\n" "$NOW"
Thu Jul 5 16:59:28 EDT 2001
$ exit
exit
```

受限 shell 非常具有约束力，但提供了高水平的安全性。在脚本编程中使用时，请在运行受限脚本之前重定向标准输出和标准错误，因为脚本本身无法重定向标准输出。





## 安全文件删除（wipe）

`rm` 命令通过删除目录项来移除文件，但旧信息仍然存在于磁盘上，直到新文件将其覆盖。通常，除了设备驱动程序级别之外，这些信息无法访问。然而，对于必须永远不能被读取的敏感信息，这可能无法接受。

`wipe` 工具首先用随机数据覆盖文件中的所有信息，然后像 `rm` 命令那样删除该文件。磁盘上不会留下任何不诚实的人可以读取的内容。

```bash
$ ls
loginz.txt
$ wipe loginz.txt
$ ls
```

`-s` 开关会安静地擦除（不是通常的 `-q`）。`-r` 会擦除所有子目录。`-D` 会擦除数据但保留文件。为了更快擦除，`-z` 用零填充文件，而不是随机数据。`-b` 使用特定字符覆盖文件。还有少数其他 `wipe` 开关，主要与随机数据的生成方式有关。

请谨慎使用 `wipe`。如果指定了设备文件（如硬盘分区）而不是普通文件，`wipe` 将尝试擦除整个分区。

所有 shell 脚本程序员都需要仔细关注安全问题。他们不仅保护重要的程序和数据安全，还限制了脚本错误可能造成的损害范围。

## 参考章节

### id 命令开关

- **`-g`**`roup`（或 **-g**）——仅打印组 ID
- **`-g`**`roups`（或 **-G**）——仅打印辅助组
- **`-n`**`ame`（或 **-n**）——打印名称而不是数字；适用于 **-ugG**
- **`-r`**`eal`（或 **-r**）——打印真实 ID 而不是有效 ID；适用于 **-ugG**
- **`-u`**`ser`（或 **-u**）——仅打印用户 ID

### chown 命令开关

- **-c**`hanges`（或 **-c**）——当发生变更时提供详细输出
- **-d**`ereference`——跟随符号链接
- **-no-dereference**（或 **-h**）——影响符号链接本身，而非其指向的文件
- **-quiet**（或 **-f** 或 **-silent**）——抑制大多数错误消息
- **-reference=f**——使用文件 `f` 的所有者和组
- **-recursive**（或 **-R**）——递归操作文件和目录

### chmod 命令开关

- **-changes**（或 **-c**）——类似 verbose，但仅在发生变更时报告
- **-quiet**（或 **-f** 或 **-silent**）——抑制大多数错误消息
- **-recursive**（或 **-R**）——递归变更文件和目录
- **-reference=f**——使用文件 `f` 的模式值
- **-verbose**（或 **-v**）——为处理的每个文件输出诊断信息

### ulimit 命令开关

- **-c**——核心文件的最大尺寸
- **-d**——进程数据段的最大尺寸
- **-f**——由 shell 创建的文件的最大尺寸
- **-l**——可以锁定的最大内存量
- **-m**——最大驻留集大小
- **-n**——最大打开文件描述符数量
- **-p**——管道大小（不可设置）
- **-s**——最大栈大小
- **-t**——最大 CPU 时间
- **-u**——单个用户的最大进程数
- **-v**——可用给 shell 的最大虚拟内存量

### wipe 命令开关

- **-Bsize**——覆盖块设备扇区计数
- **-b**——自定义字节；使用特定字节覆盖一次
- **-D**——擦除后保留文件
- **-a**——擦除后保留文件
- **-E**——使用随机字符设备；禁用 tiger 哈希
- **-e**——使用 tiger 哈希函数
- **-f**——强制文件擦除并抑制权限警告
- **-I**——禁用交互
- **-i**——提示是否移除每个文件
- **-L**——将 wipe 安全级别设置为 0
- **-p cnt**——执行 `cnt` 次 wipe 序列，包括随机路径
- **-r**（或 **-R**）——对所有子目录中的文件重复执行过程
- **-Ssize**——设置块设备扇区大小的字节大小（默认为 512）
- **-B**——禁用百分比报告和部分警告
- **-V**——如果文件大小超过特定限制，则显示百分比
- **-v**——始终显示百分比
- **-Tsize**——块设备缓冲区大小（默认为 4096）
- **-tsize**——设置 tiger 哈希输入缓冲区大小
- **-xcnt**——启用随机路径和（可选）执行的路径次数
- **-X**——禁用随机路径
- **-Z**——覆盖 -x
- **-z**——将文件清零（用零填充）
- **-1num**（竖线）——将通用安全级别设置为 `num`

# 16 网络编程

“原来你是肯·伯克特啊？”他带着一个并不愉快的微笑说道。Sun 电脑经销商握了握我的手。

当时，我和朋友正在尼亚加拉地区运营第一个互联网新闻和邮件服务。为了寻找辅助的 Usenet 信息源，我们联系了这位 Sun 经销商，询问他们是否允许我们的计算机与他们的计算机进行网络连接。我们多次发送邮件，但从未收到回复。谜团被解开了，因为该经销商解释说，他已经设置了一个 Usenet 信息源，并通过电子邮件发送了连接信息。不幸的是，他没有意识到他的电子邮件是随新闻一起路由的，这使得我们的计算机能够连接，因此我们从未收到他的消息。一个简单的沟通疏忽给他留下了坏印象。

网络是一个非常复杂的问题，因为其本质要求在不确定的信道上进行复杂的通信。幸运的是，Bash 处理了大多数细节，这使得编写和使用企业级脚本变得容易。

## 套接字

要在网络上通信，两个程序必须遵循通信协议。该协议定义了如何响应新连接、如何确认数据通过网络安全到达、当连接意外终止时该怎么办等等。通过计算机网络发送文件比将文件保存到硬盘要不可靠得多。

网络中的每台计算机都被指定一个 IP 地址和一个或多个主机名。主机名通常是同一台机器的别名。你可以使用 `host` 命令查找主机名所指的机器的 IP 地址。

```bash
$ host www.vaxxine.com
www.vaxxine.com is a nickname for alpha.vaxxine.com
alpha.vaxxine.com has address 209.5.212.5
alpha.vaxxine.com has address 209.5.212.5
```

`-v` 开关会生成域主文件副本。可以使用 `-t` 开关请求特定信息——`t` 有很多选项。

`localhost` 是 Linux 中所有 Linux 系统当前计算机的别名。机器之间的连接被称为*套接字*（sockets）。该名称可追溯至 20 世纪 80 年代初，当时它们首次与 BSD Unix 一起使用。该术语象征两台独立计算机上的两个想象中的连接器。当建立连接时（想象一根电缆连接到套接字），两台计算机即可通信。

互联网和许多局域网（LAN）的主要协议是 *TCP/IP*（传输控制协议/互联网协议）。你可以在 Bash 中使用特殊的 `/dev/tcp` 路径名来打开网络 TCP/IP 套接字。这不是实际文件的位置：Bash 将此路径名解释为打开套接字的请求。

Bash 还可以使用 `/dev/udp` 路径名创建 UDP（用户数据报协议）套接字。然而，UDP 用于发送可能无法到达目的地的短消息，本章不予介绍。

除了协议之外，套接字还需要一个*端口*。端口是用于标识远程计算机上不同服务的数字。不同的程序监听不同的端口号，等待新连接。虽然没有要求特定服务必须在特定端口上可用，但一些服务被分配了传统端口号。例如，Web 服务器通常分配给端口号 80。这是 Web 浏览器默认连接的端口。

Bash 处理打开和维护套接字的大多数细节。对于 Bash 脚本来说，套接字是一个具有非寻常路径名的常规文件。套接字表现得像命名管道一样，阻塞直到有新技术信息可供读取。当套接字关闭时，`read` 命令指示已达到文件末尾。与管道不同，套接字始终可读且可写。

## 客户端-服务器与点对点

虽然网络协议建立了通信规则，但它们对两台计算机之间交换的消息没有严格限制。如果在两台计算机之间打开套接字，且双方都等待对方发送第一条消息，程序将无限期等待。为了解决这个问题，有两种常见的网络策略——客户端-服务器和点对点。

最常见的策略是*客户端-服务器*。一个程序被指定为*服务器*。它应请求“提供”数据。另一个程序是*客户端*，它发起请求。Web 服务器和浏览器是客户端-服务器对的例子。Web 浏览器总是发起与服务器的对话。

或者，*点对点*（或 P2P）策略将客户端和服务器集成到单个程序中，通常通过为客户端和服务器功能分配不同的端口来实现。每个程序都可以接收请求或发起请求。因为所有程序都被视为平等的（或“对等”），且没有单一的服务器作为共享数据的监督者，所以这种策略适用于在多台并行计算机之间共享大型任务或数据。





由于客户端-服务器架构的简洁性，它是联网最常见的方法。服务器就像 Bash 函数一样，隐藏了查找数据并将其返回给客户端的所有复杂性。

Bash 脚本只能作为客户端编写，因为没有方法配置 Bash 去监听指定端口上的传入连接。

## 网络客户端

网络连接始终作为可读可写的文件打开（`<>`）。以 `/dev/tcp` 开头的路径名会打开 TCP/IP 连接。在路径名后跟随主机名和端口号。例如，要打开与当前计算机上 Web 服务器的连接，请执行以下操作：

```
$ exec 3<> /dev/tcp/localhost/80
```

假设当前计算机上正在端口 8080 上运行一个 Web 服务器。（端口 8080 是在个人账户下运行 Web 服务器的标准端口。）可以使用 `exec` 打开一个用于读写的连接，并获取默认 Web 页面，如清单 16.1 所示。

### 清单 16.1 getpage.sh

```bash
#!/bin/bash
#
# getpage.sh - 获取网页
#
shopt -o -s nounset

declare LINE
declare -rx SCRIPT=$0

# 打开一个连接到本地主机的 HTML 套接字
# 用于读和写

printf "Connecting to host\n"
exec 3<> /dev/tcp/localhost/8080

# 发送 HTTP 请求以获取默认页面

printf "Sending request to host\n"
printf "%s HTTP/1.0\r\n" "GET \">/" >&3
printf "Accept: text/html, text/plain\r\n" >&3
printf "Accept-Language: en\r\n" >&3
printf "User-Agent: %s (Bash Script)\r\n" "$SCRIPT" >&3
printf "\r\n" >&3

# 读取响应并在屏幕上显示

printf "Receiving page\n"
printf "%%s\n" "___________________"
while read LINE < &3 ; do
    printf "%s\n" "$LINE"
done

exit 0
```

运行此脚本将获取并显示网页。

```
$ bash getpage.sh
Connecting to host
Sending request to host
Receiving page

HTTP/1.0 200 Document follows
Date: Wed, 04 Jul 2001 18:26:27 GMT
Server: NCSA/1.5.2
Last-modified: Tue, 22 Aug 2000 18:33:31 GMT
Content-type: text/html
Content-length: 108

<html>
<head>
<title>Test Page</title>
<body>
This is the home page for Widget Inc.
</body>
</html>
```

其他网络服务，如 Telnet 和 SMTP，也可以以同样的方式访问。

## CGI 脚本编程

*CGI*（通用网关接口）脚本是由 Web 服务器运行的程序。信息通过环境变量和标准输入传递给脚本，脚本通过向标准输出返回网页或文档来做出响应。

CGI 脚本必须放置在特殊目录中（通常称为 `cgi-bin`）。拥有标准目录可以将所有脚本集中在一个中心位置，并防止未经授权的人发布脚本以及网页。如果 Web 服务器尚未如此配置，则需要配置它以允许 CGI 脚本。脚本文件以 `.cgi` 结尾，而不是 `.sh` 或 `.bash`，以便将它们与通用脚本区分开来。

CGI 脚本在返回任何信息之前，必须写入正确的 HTTP Web 服务器响应（或标头）。最短的标头是一行内容描述行，用于描述返回给 Web 浏览器的数据类型，后跟一个空行。内容要么是用于纯文本的 `text/plain`，要么是用于网页的 `text/html`。例如，要返回简单文本，请使用以下方法：

```bash
printf "Content-type: text/plain \r\n"
printf "\r\n"
```

与 HTTP 客户端示例一样，Web 服务器期望所有行都以回车符和换行符结尾，而不是简单的换行符。标头之后出现的数据不需要使用额外的回车字符进行格式化。

清单 16.2 显示了一个简短的 CGI 脚本，它运行 `env` 命令并向 Web 浏览器返回环境变量列表。

### 清单 16.2 env.cgi

```bash
#!/bin/bash
#
# env.cgi - 显示可供 CGI 程序使用的环境变量
#

shopt -s -O nounset

declare -rx SCRIPT=${0##*/}
declare GATEWAY_INTERFACE

if [ -z "$GATEWAY_INTERFACE" ] ; then
   printf "%s\n" "$SCRIPT: this script should be run by a web browser" >&2
   exit 192
fi

# 写入响应标头

printf "Content-type: text/plain\r\n"
printf "\r\n"

# 生成要返回的文本消息

env

exit 0
```

由于 CGI 脚本在独特的环境中运行，因此很难从命令行测试它们。相反，将它们存储在 `cgi-bin` 目录中，并尝试通过 Web 浏览器运行脚本。这里列出了最常见的错误：

- 403 禁止访问—脚本权限错误，或者脚本不在 CGI 目录中
- 404 未找到—CGI 脚本缺失或使用了错误的 URL。
- 500 内部服务器错误—脚本未返回正确的 CGI 标头。

服务器错误是最常见的错误。这发生在脚本在能够写入 HTTP 标头之前因错误而停止时。任何写入标准错误的消息都会出现在 Web 服务器的错误日志中。如果返回的网页缺少信息或信息不正确，请检查 Web 服务器日志中的错误。

由于检查 Web 服务器错误日志不方便，CGI 脚本应尝试捕获任何错误并通过 Web 页面上的标准输出显示它们。

若要返回网页，请将内容更改为 text/html。在使用网页显示错误时，请确保字体和颜色设置为合理的值，以便错误清晰可见。在清单 16.3 中，错误显示在页面底部的黑字白底框中。

### 清单 16.3 html_env.cgi

```bash
#!/bin/bash
#
# html_env.cgi - 显示提供给 CGI 程序的环境变量

shopt -o nounset

## 声明

declare -rx SCRIPT=${0##*/}
declare GATEWAY_INTERFACE

if [ -z "$GATEWAY_INTERFACE" ]; then
    printf "%s\n" "$SCRIPT: this script should be run by a web browser" >&2
    exit 192
fi

declare -ix ERRORS=$(mktemp /tmp/env_errors.XXXXX)
if [ -z "$ERRORS" ]; then
    ERRORS="/tmp/env_errors.$$"
    printf "mktemp failed\n" 2> "$ERRORS"
fi

# 写入响应标头

printf "Content-type: text/html\r\n"
printf "\r\n"

# 写入 HTML 标头

printf "<html>"
printf "<head>"
printf "<title>%s result=%s</title>" "$SCRIPT" "$?"
printf "</head>"
printf "<body>"
printf "<h1>%s result=%s</h1>" "$SCRIPT" "$?"

# 生成要返回的网页

printf "<pre>"
env 2> "$ERRORS"
printf "</pre>"

# 显示任何错误

if test -s "$ERRORS"; then
    printf "<br />\n"
    printf "<table border=\"1\" summary=\"Error\">\n"
    printf "<tr bgcolor=\"White\"><td>\n"
    printf "<font color=\"Black\" size=\"3\">\n"
    printf "<p><b>Errors</b><br />\n"
    cat "$ERRORS"
    printf "</p>\n"
    printf "<br />\n"
    printf "<p>If the problem persists, contact tech support.</p>\n"
    printf "</font></td></tr></table>\n"
    rm -f "$ERRORS"
fi

# 写入 HTML 尾部

printf "<br />\n"
printf "<h6>Host %s - Script %s - Time %s</h6>" "$HOSTNAME" "$SCRIPT" "$(date)"
printf "</body>"
printf "</html>"

exit 0
```

## CGI 环境变量

CGI 程序具有由 Web 服务器分配的其他环境变量。不同的 Web 服务器包含不同的变量。以下是一些常见变量的列表：

- **AUTH_TYPE**—如果页面受密码保护，则为授权类型
- **CONTENT_LENGTH**—正在写入标准输入的字节数（用于 POST 表单）
- **CONTENT_TYPE**—表单的内容类型
- **DOCUMENT_ROOT**—Web 服务器文档树的根目录
- **GATEWAY_INTERFACE**—Web 服务器使用的 CGI 标准版本
- **HTTP_ACCEPT**—浏览器可接受的数据类型（例如，`text/html`）
- **HTTP_ACCEPT_CHARSET**—Web 浏览器请求的字符集
- **HTTP_ACCEPT_ENCODING**—Web 浏览器允许的压缩方法（例如，`gzip`）
- **HTTP_ACCEPT_LANGUAGE**—Web 浏览器请求的语言（例如，英语为 `en`）
- **HTTP_USER_AGENT**—用户使用的浏览器
- **HTTP_HOST**—URL 的主机名
- **HTTP_REFERER**—执行此 CGI 程序的网页
- **PATH_INFO**—包含在 URL 中的额外信息
- **PATH_TRANSLATED**—作为文档树根下的文件/目录的 PATH_INFO
- **QUERY_STRING**—对于 GET 表单，即表单中的变量
- **REMOTE_ADDR**—用户计算机的 IP
- **REMOTE_HOST**—用户计算机的主机名
- **REMOTE_USER**—访问受密码保护页面时使用的用户名
- **REQUEST_METHOD**—通常是 `GET` 或 `POST`
- **SCRIPT_NAME**—正在执行的脚本的路径名
- **SCRIPT_FILENAME**—正在执行的脚本的绝对路径名
- **SERVER_ADDR**—Web 服务器的 IP 地址
- **SERVER_ADMIN**—发送给 Web 服务器负责人的电子邮件地址
- **SERVER_NAME**—Web 服务器的域名




- `SERVER_PORT`——用于连接 Web 服务器的 TCP/IP 端口
- `SERVER_PROTOCOL`——服务器使用的 HTTP 版本
- `SERVER_SOFTWARE`——Web 服务器的描述

## 表单处理

环境变量在 HTML 中的等价物是表单。每个表单都包含一组变量。例如，表单输入标签：

```html
<input type='hidden' name="user" value="bmith">
```

是以下命令的 HTML 等价形式：

```bash
declare user="bmith"
```

其他非隐藏输入标签代表那些值可以被用户通过表单上的项目修改的变量。此类项目包括按钮、菜单和文本框。在所有这些情况下，用户所做的选择会在表单发送给 CGI 脚本之前被保存为该变量的新值。

由于 CGI 脚本并未接收到 Web 页面的副本，它如何得知输入标签的值呢？有两种方法。较旧的 **GET** 方法将 HTML 变量存储在一个名为 `QUERY_STRING` 的环境变量中。请考虑以下表单。

```html
<html>
<head>
<title>Form Test</title>
</head>
<body>
<form action="http://localhost/cgi-bin/form.cgi">
<input type="hidden" name="user" value="bmith">
<input type="submit" name="submit" value="Click Me!">
</form>
</body>
</html>
```

查询字符串包含这两个变量的名称和值。

`user=bmith&submit=Click+Me%21`

表单难以处理的原因之一是信息是经过编码的。标准表单编码（x-www-form-urlencoded）将空格转换为加号，将非字母数字字符转换为带有前导百分号的 ASCII 十六进制数。在这种情况下，感叹号被转换为十六进制 21。

**POST** 方法将变量写入标准输入，如果变量列表变得非常长，这就消除了 Web 服务器中缓冲区溢出的风险。它还使变量不出现在 Web 页面的 URL 中。如果脚本在 while 循环中读取变量，则由于该行没有以换行符结尾，while 循环中的最后一行不会执行。

```bash
while read LINE; do
    echo "$LINE"
done
echo "$LINE"
```

这显示了与使用 GET 方法时出现在 QUERY_STRING 中的相同编码信息。

`user=smith&submit=Click+Me%21`

列表 16.4 中所示的 form.cgi 脚本解码并显示表单变量。

### 列表 16.4 form.cgi

```bash
#!/bin/bash

# form.cgi - decode and display all variables in a form

shopt -s -o nounset

# DECODE: decode all variables in $1 and display them

function decode {
    declare VARIABLES="$1"         # the list of variables to process
    declare VAR                     # variable to decode
    declare NAME                    # variable name
    declare VALUE                   # value of variable
    declare LAST                    # last decoded variable
    declare -i CNT=1                # running total of variables processed
    declare PART1                   # part before % hex code
    declare PART2                   # part after a % hex code
    declare TMP                     
    declare REMAINING               # remaining variables to process
    declare HEX                     # ASCII code as hexadecimal
    declare OCT                     # ASCII code as octal

    # Replace '+' with ' '
    VARIABLES="${VARIABLES//+/ }"

    # Hex code replacement

    while true; do
        LAST="$VAR"                 # remember last variable
        VAR="${VARIABLES%%&*}"     # extract next variable
        REMAINING="${VARIABLES*&}"  # variables left to process
        NAME="${VAR%*=}"           # variable's name is before =
        VALUE="${VAR#*=}"          # variable's encoded value is after =

        # Process any hex values

        while true; do
            PART1="${VALUE%%\%*}"          # value before last %
            if [ "$PART1" = "$VALUE" ]; then # same as whole value?
                break                              # then no % left
            fi
            TMP="${VALUE#*\%}"            # value after last %
            HEXA="${TMP:0:2}"                # extract two digit hex code
            PART2="${TMP:2}"                  # value after the hex code
            VALUE="$PART1"$(printf "\\x$HEXA")"$PART2" # combine, replacing hex code
        done
        printf "Var %d %s is `%s`\n" "$CNT" "$NAME" "$VALUE" # display variable
        if [ "$REMAINING" = "$VARIABLES" ]; then # remaining same as last?
            printf "%s\n" "<br />"           # all variables done
            printf "%s\n" "End of CGI variables<br />" # display end message
            break
        fi
        VARIABLES="$REMAINING"               # do remaining variables
        CNT=CNT+1                              # increment count
    done
} # end of decode
readonly -f decode
declare -t decode

# Declarations

declare -rx SCRIPT=${0##*/}
declare GATEWAY_INTERFACE
if [ ! -z "$GATEWAY_INTERFACE" ]; then
    printf "%s\n" "$SCRIPT: this script should be run by a web browser" >&2
    exit 192
fi

declare -rx ERRORS=`mktemp /tmp/env.errors.XXXXXX`
if [ ! -z "$ERRORS" ]; then
    ERRORS=`/tmp/env.errors.XXXXXX`
    printf "%s\n" "mktemp failed" 2> "$ERRORS"
fi
declare QUERY_STRING               # ensure QUERY_STRING exists
declare REQUEST_METHOD               # ensure REQUEST_METHOD exists

# Write Response Header

printf "Content-type: text/html\r\n"
printf "\r\n"

# Write HTML Header

printf "<html>"
printf "<head>"
printf "<title>$SCRIPT results</title>"
printf "</head>"
printf "<body>"
printf "<h1>$SCRIPT results</h1>"

# For POST, read the data into QUERY_STRING
# Otherwise, variables are already in QUERY_STRING

if [ "$REQUEST_METHOD" = "POST" ]; then
    while read LINE; do
        QUERY_STRING="$QUERY_STRING$LINE"
    done
    QUERY_STRING="$QUERY_STRING$LINE"
fi

# Generate Web Page to Return

# Display original, encoded variables

printf "Processing: $QUERY_STRING<br />"

printf "<pre>"

decode "$QUERY_STRING" 2> "$ERRORS"

printf "</pre>"

# Display any errors

if test -s "$ERRORS"; then
    printf "%s\n" "$ERRORS"
    printf "<table border=\"1\" summary=\"errorlist\">"
    printf "<tr bgcolor=\"White\"><td>"
    printf "<font color=\"black\" size=\"3\"><b>"
    printf "<p><b>Error(s)</b><br />"
    printf "<pre>"
    cat "$ERRORS"
    printf "</pre></font></td></tr></table>"
    printf "&nbsp;<br />"
    printf "<i>If the problem persists, contact tech support.</i></p>"
    rm -f "$ERRORS"
fi

# Write HTML Trailer

printf "&nbsp;<br /></h6>"
printf "Host %s - Script %s - Time " "$HOSTNAME" "$SCRIPT"
date
printf "</h6>"
printf "</body>"
printf "</html>\n"

exit 0
```

使用列表 16.5 中的表单运行 `form.cgi`，即可查看来自表单的变量列表和解码后的值。

假设你有一个表单用于向技术支持部门发送消息。

### 列表 16.5 form.html

```html
<html>
<head>
<title>Form Test</title>
</head>
<body>
<h1>Ask Tech Support Question</h1>
<form action="http://localhost/cgi-bin/form.cgi">
<input type="submit" name="submit" value="Send Question">
<input type="textarea" name="message" value="" maxlength="80">
<input type="text" name="name" value="" maxlen="80">
</form>
</body>
</html>
```

当表单提交给 form.cgi 时，decode 函数报告如下：

```
Var 1 submit is 'Send Question'
Var 2 message is 'When will the email system upgrade occur?'
Var 3 name is 'Alice Q. Walters'
End of CGI variables
```

该脚本适用于 GET 和 POST 表单。图 16.1 展示了技术支持示例的图片。

![](img/7da864b222941ec315ee1c456ff472dd_314_0.png)

图 16.1 询问技术支持表单。

## 基本网页剥离 (lynx)

互联网上的网页中有大量可用信息。可以从新闻网站获取头条新闻，也可以从竞争对手的网站抓取价格。这些信息的很大一部分是公开的，并且可以通过 shell 脚本访问。

访问这些信息最简单的方式是通过 lynx，这是大多数 Linux 发行版都有的文本 Web 浏览器。lynx 有两种用于检索数据以供脚本处理的模式。-source 开关会返回 Web 页面的 HTML 源代码，就像你在图形 Web 浏览器上使用“查看源代码”选项一样。

```bash
$ lynx -source http://www.pegaoffa.ca | head -10
<?xml version="1.0"?>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" 
        "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" 
<head>

<meta name="generator" content="HTML Tidy, see www.w3.org" />
<meta http-equiv="Content-Type" 
      content="text/html; charset=iso-8859-1" />
<meta name="description" content="Linux Software Solutions" />
<meta name="keywords"
```





你可以通过用 Bash 打开一个套接字并发送相应的 HTTP 命令来获得相同的效果。然而，浏览器可以为你处理诸如 Cookie 和网站别名等 Web 服务器问题。

当 Web 页面包含多种类型信息时，`-source` 开关很有用。例如，你可以搜索 HTML 标签，并通过查找标题文本的字体和样式来识别新闻网站上的头条新闻。

`-dump` 开关返回 Web 页面的渲染版本。在内容简单的 Web 页面上，此开关会隐藏 HTML 标签，从而使页面更容易处理。通常，lynx 会为 Web 页面上的所有链接添加脚注，但你可以通过 `-no-list` 开关来隐藏这些脚注。

```bash
$ lynx -dump --no-list http://www.pegasoft.ca
REFRESH(10 sec): http://www.pegasoft.ca/frames.html
```

![](img/7da864b222941ec315ee1c456ff472dd_315_0.png)

使用 `-source` 选项，你可以查看加拿大国家研究委员会（NRCC）网站上的官方时间。时间是包含 UTC 的 Web 页面的第一行。

```bash
$ lynx -dump http://time5.nrc.ca/webclock_e.shtml | grep UTC | head -1
15:45:55 UTC
```

列表 16.6 中显示的脚本从 NRCC 中提取官方时间，并将其与本地计算机上的时间进行比较。

# 列表 16.6 compare_time.sh

```bash
#!/bin/bash
#
#  compare_time.sh: compare our time against National Research
#  Council of Canada's atomic clock.

shopt -s -o nounset

# Global declarations

declare -rx SCRIPT="${0##*/}"    # name of our script
declare -rx lynx="/usr/bin/lynx"   # lynx command
declare -rx date="/bin/date"    # date command

declare  OUR_TIME      # our time as reported by date(1)
declare  TIME_PAGE     # the content of the NRCC web page
declare  TIME_LINE     # the page line with the time on it
declare  OFFICIAL_TIME   # the correct time from the line

declare -rx NRCC="time5.nrc.ca/webclock_e.shtml"  # NRCC web site

# Sanity Check

if test ! -x "$date" ; then
    printf "$$SCRIPT: the command $$date is not available -- aborting\n" >&1
    exit 192
fi
if test ! -x "$lynx" ; then
    printf "$$SCRIPT: the command $$lynx is not available -- aborting\n" >&1
    exit 192
fi

# Get the Time

OUR_TIME=`$$date --universal '+%H:%M:%S'`
TIME_PAGE=`$$lynx -dump -nolist "http://$$NRCC"`
if [ -z "$$TIME_PAGE" ] ; then
    printf "$$SCRIPT: the web page $$NRCC has moved -- aborting\n" >&1
    exit 192
fi
TIME_LINE=`printf "$$e\n" "$$TIME_PAGE" | grep UTC | head -1`
if [ -z "$$TIME_LINE" ] ; then
    printf "$$SCRIPT: the format of the web page $$NRCC has changed --\
aborting\n" >&1
    exit 192
fi
OFFICIAL_TIME="`printf "%s\n" "$TIME_LINE"` | sed "s/.*: / /;s/UTC/ /g"`
# Display time
printf "Note: This script doesn't take into account Internet delays\n"
printf "Our computer time = "%s UTC\n" "$OUR_TIME"
printf "Official UTC time = "%s UTC\n" "$OFFICIAL_TIME"
exit 0
```

Web 页面的内容和地址很容易发生变化。在剥离 Web 页面时，务必仔细检查页面是否已移动以及内容是否已更改。`compare_time.sh` 脚本检查了 lynx 是否获取了 Web 页面，以及包含时间的行是否确实被 grep 找到。如果 Web 页面位置已更改，你可以使用 Google 等搜索引擎重新找到它。

运行该脚本会显示 NRCC 时间与本地计算机时间的并排比较。

```bash
$ bash compare_time.sh
Note: This script doesn't take into account Internet delays
Our computer time = 14:55:56 UTC
Official UTC time = 14:56:51 UTC
```

有关 lynx 的更多信息，请访问 http://lynx.browser.org。

## 参考部分

### host 命令开关

- `-a`—等同于 `-v -t`
- `-c`—查找非 Internet 数据的类
- `-d`—开启调试模式
- `-l`—开启列表模式
- `-r`—禁用递归处理
- `-s`—递归查找答案中找到的签名
- `-t q`—查询类型 q 以查找特定类型信息
- `-v`—详细输出
- `-w`—无限期等待直到收到回复

### 常见的 CGI 变量

- `AUTH_TYPE`—如果页面受密码保护，则为授权类型
- `CONTENT_LENGTH`—写入标准输入的字节数（用于 POST 表单）
- `CONTENT_TYPE`—表单的内容类型
- `DOCUMENT_ROOT`—Web 服务器文档树的根目录
- `GATEWAY_INTERFACE`—Web 服务器使用的 CGI 标准版本
- `HTTP_ACCEPT`—浏览器可接受的数据类型（例如，text/html）
- `HTTP_ACCEPT_CHARSET`—Web 浏览器请求的字符集
- `HTTP_ACCEPT_ENCODING`—Web 浏览器允许的压缩方法（例如，gzip）
- `HTTP_ACCEPT_LANGUAGE`—Web 浏览器请求的语言（例如，en 代表英语）
- `HTTP_USER_AGENT`—用户使用的浏览器
- `HTTP_HOST`—URL 的主机名
- `HTTP_REFERER`—执行此 CGI 程序的 Web 页面
- `PATH_INFO`—包含在 URL 中的额外信息
- `PATH_TRANSLATED`—`PATH_INFO`，作为文档树根下的文件/目录
- `QUERY_STRING`—对于 GET 表单，表单上的变量
- `REMOTE_ADDR`—用户计算机的 IP 地址
- `REMOTE_HOST`—用户计算机的主机名
- `REMOTE_USER`—访问受密码保护页面时使用的用户名
- `REQUEST_METHOD`—通常是 GET 或 POST
- `SCRIPT_NAME`—正在执行的脚本的文件名
- `SCRIPT_FILENAME`—正在执行的脚本的绝对路径名
- `SERVER_ADDR`—Web 服务器的 IP 地址
- `SERVER_ADMIN`—用于向 Web 服务器负责人发送电子邮件消息的电子邮件地址
- `SERVER_NAME`—Web 服务器的域名
- `SERVER_PORT`—用于连接 Web 服务器的 TCP/IP 端口
- `SERVER_PROTOCOL`—服务器使用的 HTTP 版本
- `SERVER_SOFTWARE`—Web 服务器的描述

### lynx 页面剥离开关

- `-auth=id:pw`—使用登录 ID 和密码 pw 对受保护文档进行身份验证
- `-base`—为 `-source` 转储的输出添加 BASE 标签前缀
- `-buried_news`—在新闻文章中搜索其他文章引用（默认开启）
- `-cmd_script=f`—输入来自文件 f
- `-connect_timeout=n`—连接超时秒数（默认是 18000）
- `-crawl`—将每个页面输出到文件（使用 `-dump`）或将输出格式化到标准输出
- `-dont_wrap_pre`—禁止 `<pre>` 中文字的换行（默认关闭）
- `-dump`—将文件转储到标准输出并退出
- `-get_data`—GET 表单的用户数据，从标准输入读取，并以行中的 `--` 终止
- `-image_links`—切换所有图像的链接包含（默认关闭）
- `-link=n`—`-crawl` link.dat 文件的起始 cfile 名称（默认是 0）
- `-mime_header`—包含 MIME 头并强制源转储
- `-nolist`—禁用转储中的链接列表功能（默认关闭）
- `-noreaddir`—不跟随 Web 服务器 Location: 重定向（默认关闭）
- `-path=id:pw`—类似于 `-auth`，但适用于代理 Web 服务器
- `-post_data`—POST 表单的用户数据，从标准输入读取，并以行中的 `--` 终止
- `-reload`—清除代理服务器上的缓存（默认关闭）
- `-source`—将文件的源转储到标准输出并退出
- `-stdin`—从标准输入读取起始文件
- `-tlog`—切换当前会话中 lynx 跟踪日志的使用（默认开启）
- `-trace`—开启 lynx 跟踪模式（默认关闭）
- `-traversal`—遍历从起始文件派生的所有 HTTP 链接
- `-useragent=b`—伪装成浏览器 b
- `-width=n`—转储格式化的屏幕宽度（默认是 80）
- `-with_backspaces`—如果 `-dumping` 或 `-crawling`，则在输出中发出退格符（默认关闭）

# 17 数据结构和数据库

我一直说，我宁死也不愿在一个没有窗户的狭小办公室里，对着绿色单色终端工作。当然，我大学毕业后第一份工作正是如此，只不过那个单色终端是琥珀色而不是绿色的。

当我在该公司使用的定制 BASIC 软件中思考一个税务问题时，我的电话响了，总裁让我去他的办公室。他的办公室当然有窗户。总裁在早期编写了大部分软件，他让我去他的终端旁。他说：“看看这个。这是一个由九个数字组成的数组。我通过将一个索引乘以三并加上第二个索引，将它变成了一个二维的 3×3 数组！很酷，对吧？”

由于我以全 A 的成绩大学毕业，我强忍住打了个哈欠，说：“哦，是的，先生。您非常聪明。”

这是我第一次意识到，那家公司以及我后来工作的每一家公司的软件都是在一个高中编程水平上编写的。哈希表和二叉树被认为过于复杂且不必要地冒险，尽管它们能节省时间和金钱。价值数百万美元的公司依赖于平文件（flat files）和简单数组——这些是老板能理解的东西，因此是安全的。如果软件缓慢且笨拙，公司总是可以申购最新的硬件来提高性能。

在小公司工作可能会看重编程技能。本章演示了如何完成这些“危险”的操作，如果你足够幸运，不会因为编程水平超过初级水平而受到训斥。

## 使用 Bash 数组实现关联数组

*关联数组*（也称为“查找表”或 Perl 语言所说的“哈希表”）是包含成对值的表。第一项是*键*，即被查找的已知值。第二项是与键*关联*的值。对于一个电话号码表，键可能是员工姓名，关联的值则是每位员工的电话分机号。




使用 Bash 数组可以轻松地创建关联数组。可以利用一个特殊分隔符将一对项目组合成单个项目。该字符应为一个很少使用的字符，例如波浪号。

```bash
TABLE[$NEXTITEM]="$1$SEPARATOR$2"  # add the pair to the table
printf "%s\n" "Added $1 / $2 at $NEXTITEM"
let "NEXTITEM++"
```

如果 `NEXTITEM` 是一个包含 `TABLE` 数组中下一个空闲位置的整数变量，则该对被添加到表中，且 `NEXTITEM` 递增到下一个空闲位置。如果 `NEXTITEM` 从零开始，该对将添加到位置零，且 `NEXTITEM` 递增至一。

要查找一项，必须搜索该表，直到找到该项或到达表的末尾为止。

```bash
while [ $ITEM -lt $NEXTITEM ] ; do     # reached end of table?
KEY=${TABLE[$ITEM]}
KEY=${KEY%$SEPARATOR*}
if [ "$KEY" = "$KEY2FIND" ] ; then
break
else
let "ITEM=ITEM+1"
fi
done
```

如果 `ITEM` 是表中的位置，当循环完成时，`ITEM` 将是包含正确对的表位置，或者 `ITEM` 将等于 `NEXTITEM`；即位于表末尾之后的一个位置。

列表 17.1 包含了一个完整的脚本，用于创建关联数组并在其中搜索项目对。

### 列表 17.1 lookup.sh

```bash
#!/bin/bash
# lookup.sh
#
# create a lookup table and look up items
#
# Ken O. Burtch
# CVS: $Header$
shopt -s -o nounset

declare -ax TABLE             # the lookup table
declare -ix NEXTITEM=0        # next free spot in table
declare -x SEPARATOR="-"      # delimiter for key/value
declare -rx SCRIPT=${0##*/}  # name of the script

# add_table: add a key/value pair to the lookup table
#				 (doesn't check for uniqueness)
#
#	parameter 1: the key
#	parameter 2: the associated value

function add_table {
	declare TEMP

	# Check the number of parameters

	if [ $# -ne 2 ] ; then
		printf "%s\n" "$SCRIPT: $FUNCNAME: Expected two parameters" >&2
		return
	fi

	# Make sure the separator isn't in the key or value

	TEMP="${1//${SEPARATOR}/_}"				# remove separator (if any)
	if [ "$1" != "$TEMP" ] ; then			# from key. Found any?
		printf "%s\n" "$SCRIPT: $FUNCNAME: Key $1 must not contain $SEPARATOR" >&2
		return
	fi
	TEMP="${2//${SEPARATOR}/_}"				# remove separator (if any)
	if [ "$2" != "$TEMP" ] ; then			# from value. Found any?
		printf "%s\n" "$SCRIPT: $FUNCNAME: Value $2 must not contain $SEPARATOR" >&2
		return
	fi

	TABLE[$NEXTITEM]="${1}${SEPARATOR}${2}"	# add the pair to the table
	printf "%s\n" "Added $1 / $2 at $NEXTITEM"
	let "$NEXTITEM++"
}
readonly -f add_table

# lookup_table: search for and display item matching key in the lookup table
#
function lookup_table {
	declare -i ITEM=0				# position in array
	declare KEY
	declare VALUE

	# The key must not contain the separator

	TEMP="${1//${SEPARATOR}/_}"				# remove separator (if any)
	if [ "$1" != "$TEMP" ] ; then  # from key. Found any?
	    printf "%s\n" "$SCRIPT: $FUNCNAME: Key must not contain $SEPARATOR" >&2
	    return
	fi

	while [ $ITEM -lt $NEXTITEM ] ; do  # reached end of table?
	    KEY=${TABLE[$ITEM]}  # if not, get the pair
	    KEY=${KEY%${SEPARATOR}*}  # extract the key part
	    if [ "$KEY" = "$1" ] ; then  # is it the key we want?
	        break  # good, it matches
	    else  # otherwise
	        let "ITEM=ITEM+1"  # move to the next item
	    fi
	done

	# Display search results

	if [ $ITEM -eq $NEXTITEM ] ; then
	    printf "%s\n" "$1 is not in the table"
	else
	    VALUE=${TABLE[$ITEM]}
	    VALUE=${VALUE#*${SEPARATOR}}
	    printf "%s\n" "$1 has the value $VALUE"
	fi
}

readonly -f lookup_table

# Main script begins

printf "Building the lookup table...\n\n"

add_table "4324" "Hazel's Ladies Wear"
add_table "1879" "Crowther Insurance Brokers Limited"
add_table "3048" "Clarke Plumbing"
add_table "4267" "Sharkur LLP"
add_table "9433" "Scott Furniture Ltd"
add_table "2018" "Zap Electric"
add_table "2250" "Sommor Water"

printf "\nLooking up some items...\n\n"

lookup_table "1879"
lookup_table "2250"
lookup_table "0000"

exit 0
```

`add_table` 函数将一对项目添加到关联数组中。这两个项目被组合成一个由分隔符字符分隔的单个值（在这种情况下，是一个波浪号）。该对被添加到表的末尾，且表中的下一个空闲位置 `NEXTITEM` 增加 1。

`lookup_table` 函数在表中搜索键并返回关联的值。表被搜索该键。如果找到该键，则显示公司名称。否则，脚本通知该 ID 号码不在表中。

该脚本创建了一个包含 ID 号码及其关联公司名称的示例查找表。

```bash
$ lookup.sh
Building the lookup table...

Added 4324 / Hazel's Ladies Wear at 0
Added 1879 / Crowther Insurance Brokers Limited at 1
Added 3048 / Clarke Plumbing at 2
Added 4267 / Sharkur LLP at 3
Added 9433 / Scott Furniture Ltd at 4
Added 2018 / Zap Electric at 5
Added 2250 / Sommer Water at 6

Looking up some items...

1879 has the value Crowther Insurance Brokers Limited
2250 has the value Sommer Water
0000 is not in the table
```

## 使用 Bash 数组实现的哈希表

哈希表以使其能够快速再次找到的方式存储单个项目。哈希表依赖于一个哈希值，或者数学公式，该公式将存储的项目转换为单个数字。该数字用于确定项目在哈希表中的存储位置。良好的哈希算法会在表中尽可能均匀地分散项目。

编写自己的哈希公式是可能的，但就此处目的而言，Linux MD5 校验和功能表现相当出色，并能创建唯一数字。你可以将其用作哈希公式。

```bash
HEXCODE=`echo "$1" | $MD5SUM`          # compute the hash value (hex)
HEXCODE=`${HEXCODE:0:4}`                # take first 4 hex digits
CODE=`printf "%d\n" 0x"$HEXCODE"`        # convert to 0...65535
printf "%d\n" "${CODE%TABLE_SIZE}"       # restrict to table size
```

此例程获取由 `md5sum` 计算的前四个十六进制数字，并将其转换为 0 到 65535 之间的数字。然后，该数字被限制在表的大小内。如果表大小为 100，则哈希码在 0 到 99 之间，即 100 项数组中的位置。

两个项目可能生成相同的哈希值。这被称为*碰撞*，且项目必须存储在表中不同的位置。

与关联数组类似，哈希表也可以存储在 Bash 数组中，如列表 17.2 所示。

### 列表 17.2 hash.sh

```bash
#!/bin/bash
# 
# hash.sh
# 
# Create a hash table and look up items
# 
# Ken O. Burtch
# CVS: $Header$
shopt -s -o nounset

declare -ax TABLE			# the hash table
declare -ix TABLE_SIZE=100	# size of the hash table
declare -rx SCRIPT=${0##*/}	# name of the script
declare -rx MD5SUM='/usr/bin/md5sum'	# used for hash generation

# hash_of: generate a table position from a string
#
function hash_of {
    declare HEXCODE			# 4 hex digits of MD5 signature
    declare -i CODE			# the hex digits in decimal

    HEXCODE=`echo "$1" | $MD5SUM`	# compute the hash value (hex)
    HEXCODE=${HEXCODE:0:4}		# take first 4 hex digits
    CODE=`printf '%d\n' 0x$HEXCODE`	# convert to 0...65535
    printf '%d\n' $((CODE%TABLE_SIZE))	# restrict to table size
}
readonly -f hash_of

# add_hash: add item to the hash table
#
function add_hash {
    declare -i ITEM=0			# current position in table

    # Empty strings are used for empty table positions

    if [ -z "$1" ] ; then
        printf '%s\n' "$SCRIPT: $FUNCNAME: Cannot add empty items" >&2
        return
    fi

    # Search for a free position
    ITEM=`hash_of "$1"`
    # search starts here
    shopt -u -o nounset
    while [ -n "${TABLE[ITEM]}" ] ; do
        # empty spots will cause error
        printf '%s\n' "Position $ITEM for $1 in use, moving forward..."
        let "ITEM=ITEM+1"   # if not, keep looking
    done
    shopt -s -o nounset      # safe to use now
    TABLE[ITEM]="$1"         # add the item to the table
    printf "%s\n" "Added $1 at $ITEM"
}
readonly -f add_hash

# lookup_hash: search and display items in the hash table
#
function lookup_hash {
    declare -i ITEM=0        # position in array

    # Empty items used for empty hash table positions

    if [ -z "$1" ] ; then
        printf '%s\n' "$SCRIPT: $FUNCNAME: Cannot lookup empty items" >&2
        return
    fi

    # Find the item or arrive at an empty spot

    ITEM=`hash_of "$1"`
    # search starts here

    shopt -u -o nounset
    while [ -n "${TABLE[ITEM]}" ] ; do
        # empty spots will cause errors
        if [ "${TABLE[ITEM]}" = "$1" ] ; then   # reached an empty spot?
            break                                 # good, it matches
        else                                      # may be inserted after
            let "ITEM=ITEM+1"                     # move to the next item
        fi
    done

    # Display search results

    if [ -z "${TABLE[ITEM]}" ] ; then
        printf "%s\n" "$1 is not in the table"
    else
        printf "%s\n" "$1 is in the table at $ITEM"
    fi
}
```





## 列表 17.2（续）

```bash
}
readonly -f lookup_hash

# 主脚本开始

if [ ! -x "$MD5SUM" ] ; then
  printf "无法运行命令 %s\n" "$MD5SUM" >&2
  exit 129
fi
printf "正在构建哈希表...\n\n"

add_hash "Hazel's Ladies Wear"
add_hash "Crowther Insurance Brokers Limited"
add_hash "Clarke Plumbing"
add_hash "Shakur LLP"
add_hash "Scott Furniture Ltd"
add_hash "Zap Electric"
add_hash "Sommer Water"

printf "\n正在查找某些条目...\n\n"

lookup_hash "Hazel's Ladies Wear"
lookup_hash "Sommer Water"
lookup_hash "Bogus test data"

exit 0
```

`add_hash` 函数将条目添加到哈希表中。如果发生冲突，`add_hash` 会尝试在表中的下一个位置添加该条目。它会继续在表中移动，直到找到一个空位置为止。

`lookup_hash` 函数在哈希表中搜索条目。如果未在预期位置找到该条目，它会继续在表中移动，直到遇到一个空位置为止。它会报告该条目的位置，或者宣布找不到该条目。

```bash
$ bash hash.sh
正在构建哈希表...

已在位置 34 添加 Hazel's Ladies Wear
已在位置 29 添加 Crowther Insurance Brokers Limited
已在位置 19 添加 Clarke Plumbing
已在位置 70 添加 Shakur LLP
已在位置 86 添加 Scott Furniture Ltd
已在位置 49 添加 Zap Electric
位置 70 上的 Sommer Water 已被占用，继续向后移动...
已在位置 71 添加 Sommer Water

正在查找某些条目...
Hazel's Ladies Wear 在表中，位于位置 34
Sommer Water 在表中，位于位置 71
Bogus test data 不在表中
```

可以将哈希表与关联数组结合使用，以创建具有快速查找时间的 Perl 风格哈希。

## 使用 Bash 数组实现二叉树

哈希选择看似随机的位置来存储条目。由于条目分散存放，因此很难对其进行排序。

二叉树提供了一种折中方案：它比哈希慢，但其中包含的条目是已排序的，并且可以按排序顺序显示。*二叉树* 是一种族谱结构，其中每个父节点有两个子节点。子节点根据父节点进行排序。通常，字母顺序在父节点之前的子节点存储在左侧，而字母顺序在父节点之后的子节点存储在右侧。

二叉树的一个常见问题是*退化树*。如果添加到二叉树中的条目是按照树的排序条件预先排序的，那么该树就是一个单一的长列表。如有必要，请在将条目添加到树之前对它们进行随机化处理。

二叉树可以用 Bash 数组表示。树每一层的大小是已知的。第一个条目，即树的*根*，始终是一个单一条目。树的下一行有两个条目，即根的两个子节点。下一行有四个条目，以此类推。因此，如果树的根在 Bash 数组中的位置为零，那么第二行位于位置 1 和 2，第三行位于位置 3、4、5 和 6。

```bash
if [ "${TREE[$ITEM]}" > "$1" ] ; then   # 按字母顺序排序
    let "ITEM=ITEM*2+1"                 # 较小的条目到左子节点
else
    let "ITEM=ITEM*2+2"                 # 较大的条目到右子节点
fi
```

你可以使用这个简单的数学公式将树存储在数组中。例如，树中位置 1 的条目的左子节点存储在位置 1*2+1，即位置 3。右子节点位于位置 4，即下一个位置。条目按字母顺序排序（或者至少按其 ASCII 值排序）。

由于新条目是添加到 TREE 数组中的空位置，因此必须在检查空位置时暂时关闭 *nounset* shell 选项。从技术上讲，空位置是“未设置”的，如果该选项保持开启状态会导致错误。

列表 17.2 展示了一个将二叉树存储在 Bash 数组中的脚本。

## 列表 17.3 `binary.sh`

```bash
#!/bin/bash
#
# binary.sh
#
# 创建二叉树并查找条目
# Ken O. Butsch
# CVS: $Header$
#
shopt -s -o nounset

declare -ax TREE                      # 二叉树
declare -rx SCRIPT=${0##*/}           # 脚本名称

# add_tree: 向二叉树添加条目
#
function add_tree {
    declare -i ITEM=0                 # 数组中的当前位置

    # 空字符串用于树的叶节点

    if [ -z "$1" ] ; then
        printf '%s\n' "$SCRIPT: $FUNCNAME: 无法添加空条目" >&2
        return
    fi

    # 查找空闲的叶节点

    shopt -u -o nounset               # 叶节点会导致错误
    while [ -n "${TREE[$ITEM]}" ] ; do
        if [ ${TREE[$ITEM]} > "$1" ] ; then  # 按字母顺序排序
            let "ITEM=ITEM*2+1"       # 较小的条目到左子节点
        else
            let "ITEM=ITEM*2+2"        # 较大的条目到右子节点
        fi
    done
    shopt -s -o nounset               # 现在可以安全使用了
    TREE[$ITEM]="$1"                  # 将条目添加到树中
    printf '%s\n' "已在位置 $ITEM 添加 $1"
}
readonly -f add_tree

# dump_tree: 按字母顺序显示树中的条目
#
function dump_tree {
    declare -i ITEM                   # 当前位置
    declare -i NEW_ITEM               # 子节点位置

    if [ $# -gt 0 ] ; then            # 条目编号？
        ITEM="$1"                     # 检查它
    else                              # 否则是用户调用
        ITEM=0                        # 我们从顶部开始
    fi

    shopt -u -o nounset
    if [ -n "${TREE[$ITEM]}" ] ; then # 叶节点会导致错误
        let "NEW_ITEM=ITEM*2+1"       # 叶节点？则无事可做
        dump_tree "$NEW_ITEM"          # 否则前往左子节点
        printf "%s\n" "$ITEM = ${TREE[$ITEM]}"    # 显示左子节点
        let "NEW_ITEM=ITEM*2+2"        # 显示此条目
        dump_tree "$NEW_ITEM"          # 前往右子节点
    fi
    shopt -s -o nounset               # 显示右子节点
    readonly -f dump_tree

# lookup_tree: 在二叉树中搜索并显示条目
#
function lookup_tree {
    declare -i ITEM=0                 # 数组中的位置

    # 空条目用于叶节点

    if [ -z "$1" ] ; then
        printf "%s\n" "$SCRIPT: $FUNCNAME: 无法查找空条目" >&2
        return
    fi

    # 找到该条目或到达空叶节点

    shopt -u -o nounset
    while [ -n "${TREE[$ITEM]}" ] ; do # 叶节点会导致错误
        if [ "${TREE[$ITEM]}" = "$1" ] ; then # 到达叶节点？未找到
            break                          # 否则是找到该条目？
        elif [ "${TREE[$ITEM]}" > "$1" ] ; then # 很好
            let "ITEM=ITEM*2+1"            # 继续搜索
        else
            let "ITEM=ITEM*2+2"            # 较小的条目到左子节点
                                           # 较大的条目到右子节点
        fi
    done

    # 显示搜索结果

    if [ -z "${TREE[$ITEM]}" ] ; then
        printf "%s\n" "$1 不在树中"
    else
        printf "%s\n" "$1 在树中，位于位置 $ITEM"
    fi
}
readonly -f lookup_tree

# 主脚本开始

printf "正在构建树...\n"

add_tree "Hazel's Ladies Wear"
add_tree "Crowther Insurance Brokers Limited"
add_tree "Clarke Plumbing"
add_tree "Shakur LLP"
add_tree "Scott Furniture Ltd"
add_tree "Zap Electric"

printf "\n树中包含...\n\n"

dump_tree

printf "\n正在查找某些条目...\n\n"

lookup_tree "Zap Electric"
lookup_tree "Clarke Plumbing"
lookup_tree "Bogus test data"

exit 0
```

`add_tree` 函数将条目按字母顺序排序后添加到树中。

`lookup_tree` 函数在树中搜索条目。如果该函数到达数组中未设置的位置，它就知道该条目不存在。

`dump_tree` 函数遍历树，按排序顺序访问每个条目并显示该条目。

```bash
$ bash binary.sh
正在构建树...

已在位置 0 添加 Hazel's Ladies Wear
已在位置 1 添加 Crowther Insurance Brokers Limited
已在位置 3 添加 Clarke Plumbing
已在位置 2 添加 Shakur LLP
已在位置 5 添加 Scott Furniture Ltd
已在位置 6 添加 Zap Electric
```


该树包含...

```
3 = Clarke Plumbing
1 = Crotwer Insurance Brokers Limited
0 = Hazel's Ladies Wear
5 = Scott Furniture Ltd
2 = Shakur LLP
6 = Zap Electric
```

查找一些项目...

```
Zap Electric is in the tree at 6
Clarke Plumbing is in the tree at 3
Bogus test data is not in the tree
```

由于其排序特性，二叉树也可以用作简单的排序。然而，`Linux` 的 *sort* 命令几乎总是更快。

## 使用 PostgreSQL 数据库 (`psql`)

对于少量数据，文本文件和 Bash 数组快速且方便。如果你要处理数十万条信息，你需要使用数据库来管理你的信息。

大多数数据库（包括 Oracle、MySQL 和 PostgreSQL）都附带控制台客户端应用程序。这些应用程序有时被称为“监控器”或“控制台监控器”。控制台客户端在外观和操作上与 shell 非常相似，但它们使用不同的命令提示符，并期望输入 `SQL` 命令而不是 `Linux` 或 `Bash` 命令。通过适当的选项，控制台客户端可以代表 Bash 脚本执行数据库命令。

PostgreSQL 数据库在大多数 `Linux` 发行版中都有提供，但根据你的安装设置，它可能不会默认安装。例如，“桌面”或“工作站”安装可能不包含 PostgreSQL。PostgreSQL 数据库有一个名为 `psql` 的控制台客户端。如果未安装 `psql`，请查看它是否在你的发行版光盘中可用。本节其余部分假设你已安装 PostgreSQL 并且数据库服务器正在运行。

要登录到 PostgreSQL，请使用带有 `-user username`（或 `-U username`）选项的 `psql`。`-list`（或 `-l`）选项列出所有可用的数据库。

```bash
$ psql -user gordon --list
```

数据库列表

| 名称 | 所有者 | 编码 |
| :--- | :--- | :--- |
| custinfo | postgres | SQL_ASCII |
| template0 | postgres | SQL_ASCII |
| template1 | postgres | SQL_ASCII |

（3 行）

使用 `--dbname db`（或 `-d db`）选项选择起始数据库。你可以使用 `-command sqlcmd`（或 `-c sqlcmd`）选项运行简短的查询。这类似于 Bash 的 `-e` 选项。还有一个 `-file` 选项用于运行包含在单独文件中的命令。

```bash
$ psql --user gordon --dbname custinfo --command "SELECT COUNT(*) FROM USER"
 count 
--------
     3
(1 row)
```

可以从脚本中使用 psql 来访问数据库。SQL 命令可以通过标准输入重定向到 psql。你可以使用 `-file=-` 为脚本提供特殊功能，例如在出错时显示行号。可以使用 here file 将 SQL 命令直接放置在调用 psql 之后。

```bash
psql --user gordon --dbname custinfo --file=- <<! 
select count(*) from products
!
```

此脚本片段统计 `products` 表中产品的数量。

```
 count
-------
   165
(1 row)
```

可以在 here file 中包含 Shell 变量以自定义你的 SQL 命令。

```bash
declare Id=5
psql --user gordon --dbname custinfo --file=- <<! 
select product_name from products where product_id = $ID
!
```

查询结果放置在标准输出上。可以使用反引号或重定向标准输出捕获它们。

```bash
RESULT='psql --user gordon --dbname custinfo --file=- <<! 
select product_name from products where product_id = $ID
!'
```

或者甚至

```bash
RESULT=`printf '%s' "select product_name from products where product_id = $ID" | psql --user gordon --dbname custinfo --file=-`
```

psql 使用列标题、边框和总计显示命令结果。虽然这些在交互会话中看起来很吸引人，但它们会给脚本增加更多的工作。可以使用适当的选项关闭这些格式化功能。

```bash
psql --user gordon --dbname custinfo --file=- -quiet --no-align --tuples-only \
--field-separator "," -file "-" <<!
select * from products
;
```

结果以 CSV（逗号分隔值）格式显示。`--no-align`（或 `-A`）移除了列之间的空白填充。`--field-separator` `,`（或 `-F` `,`）使用特定字符分隔列；在这种情况下，它们用逗号分隔。`--tuples_only`（或 `-t`）移除标题和总计。最后，使用 `--quiet`（或 `-q`）抑制进度信息。

PostgreSQL 有一套不寻常的状态码。成功时返回状态码 0，发生内部错误（例如，无法分配内存）时返回 1，客户端断开连接时返回 2，由于错误导致 SQL 命令中止时返回 3。只有声明了名为 `ON_ERROR_STOP` 的变量时才会出现 3 代码；除非存在此变量，否则 PostgreSQL 会忽略错误并继续执行下一个数据库命令；它不会报告问题。

由于这种状态码方案，如果脚本使用 `--file` 选项查找 SQL 命令文件，而该文件不存在，psql 会返回成功状态。在执行 psql 之前检查所有文件非常重要。

列表 17.4 展示了一个完整的示例，执行存储在一个单独文件中的一组 SQL 命令。

### 列表 17.4 show_users.sh

```bash
#!/bin/bash
#
# show_users.sh: show all users in the database table "users"

shopt -s o_nounset

declare -rx SCRIPT=$0${##*/}
declare -r SQL_CMDS="sort_inventory.sql"
declare -rx ON_ERROR_STOP

if [ ! -r "${SQL_CMDS}" ]; then
  printf "${SCRIPT}: the SQL script ${SQL_CMDS} doesn’t exist or is not \
readable" >&2
  exit 192
fi

RESULTS=`psql --user gordon --dbname custinfo --quiet --no-align --tuples-only \
--field-separator "," --file "${SQL_CMDS}"`
if [ $! -ne 0 ]; then
  printf "${SCRIPT}: SQL statements failed." >&2
  exit 192
fi
```

除了使用反引号捕获结果外，你还可以使用 `--output` *fname*（或 `-o` *fname*）将结果重定向到文件。

## 使用 MySQL 数据库

MySQL 数据库在大多数 Linux 发行版中都有提供，但根据你的安装设置，它可能不会默认安装。MySQL 数据库有一个名为 `mysql` 的控制台客户端，名称恰如其分。本节其余部分假设你已安装 MySQL 并且数据库服务器正在运行。

要登录到 MySQL，请使用带有 `--user=username`（或 `-u` *username*）和 `--password=pwd`（或 `-p` *pwd*）选项的 `mysql`。如果你使用 `--password` 时省略了密码，MySQL 会提示你输入。

输入 `quit`（或 `\q`）以退出客户端。

```bash
$ mysql --user gordon --password=tifbigl98
mysql> quit
$
```

你可以使用 `--exec=sqlcmd`（或 `-e` *sqlcmd* *execute* *command*）选项运行简短的查询。这类似于 Bash 的 `-e` 选项。

```bash
$ mysql --user gordon --password=tifbigl98 --exec="SHOW DATABASES"
+----------+
| Database |
+----------+
| bahaetest |
| mysql    |
| test     |
+----------+
$
```

MySQL 成功时返回状态码零（0），出错时返回 1。你可以使用 `$?` 变量以通常方式检查状态码，如列表 17.5 所示。

### 列表 17.5 show_mysqlDb.sh

```bash
#!/bin/bash
#
# show_mysqlDb.sh
#
# Show all databases

shopt -s o_nounset

declare -rx SCRIPT=${0%#/}

$ mysql --user=gordon --password=tifbigl98 --exec="SHOW DATABASES"
if [ $? -ne 0 ] ; then
    printf "$SCRIPT: SQL statement failed." >&2
    exit 192
fi
```

你可以通过重定向输入从文件加载一组 SQL 命令，如列表 17.6 所示。

### 列表 17.6 showusers.bash

```bash
#!/bin/bash
#
# showusers.bash: Show users in the bushitest/user table

shopt -s -o nounset

declare -rx SCRIPT=$0${##*/}
$ mysql -user=gordon -password=tifbig198 <<HERE
USE bushitest
select * from user
QUIT
HERE
if [ $? -ne 0 ] ; then
    printf "$SCRIPT: SQL statement failed." >&2
    exit 192
fi
```

如果 bushitest 数据库有一个名为 user 的表，脚本将返回类似这样的列表：

```bash
$ sh showusers.bash
name
Sally
Jane
Britney
```

Here file 末尾不需要 QUIT。MySQL 会自动移除边框和标题，以便于脚本处理信息。

## 参考部分

### psql 命令选项

- `--echo-all`（或 `-a`）—追踪 SQL 命令
- `--no-align`（或 `-A`）—无输出对齐
- `--command q`（或 `-c q`）—运行 SQL 查询 q




## psql 命令开关

- `--dbname d`（或 `-d d`）— 使用数据库 d
- `--echo-queries`（或 `-e`）— 打印 SQL 命令（但不包括反斜杠命令）
- `--echo-hidden`（或 `-E`）— 打印由反斜杠命令引发的 SQL 命令
- `--file f`（或 `-f f`）— 运行文件 f 中的 SQL 命令
- `--field-separator c`（或 `-F c`）— 使用字符 c 分隔列
- `--host h`（或 `-h h`）— 计算机 h 上拥有数据库
- `--html`（或 `-H`）— 使用简单的 HTML 输出
- `--list`（或 `-l`）— 列出可用的数据库
- `--output f`（或 `-O f`）— 将查询结果保存到文件 f
- `--port p`（或 `-p p`）— 使用 TCP/IP 端口 p
- `--ps2 s`（或 `-P s`）— 执行 \ps2 命令 s
- `--quiet`（或 `-q`）— 隐藏状态信息
- `--record-separator s`（或 `-R s`）— 使用字符 s 作为行分隔符
- `--single-step`（或 `-s`）— 在执行 SQL 命令前提示
- `--tuples-only`（或 `-t`）— 不打印列名或总计
- `--table-attr o`（或 `-T o`）— --html 的 HTML 表格选项
- `--username u`（或 `-U u`）— 以用户 u 身份登录数据库
- `--variable s`（或 `-V s`）— 分配 \set 值
- `--password`（或 `-W`）— 提示输入 \password
- `--expanded`（或 `-X`）— 使用扩展行格式
- `--no-pager`（或 `-Z`）— 不执行启动文件中的指令

### mysql 命令开关

- `--batch`（或 `-B`）— 以制表符分隔的格式打印结果
- `--exec=c`（或 `-e c`）— 运行 SQL 命令 c
- `--force`（或 `-f`）— 发生错误后继续执行
- `--host=h`（或 `-h h`）— 计算机 h 上拥有数据库
- `--unbuffered`（或 `-n`）— 不对查询结果进行缓冲
- `--password=p`（或 `-p p`）— 提供登录密码
- `--port=p`（或 `-P p`）— 使用 TCP/IP 端口 p
- `--quick`（或 `-q`）— 不缓存结果
- `--raw`（或 `-r`）— 配合 --batch，不转换结果
- `--silent`（或 `-S`）— 隐藏状态信息
- `--socket=f`（或 `-S f`）— 使用 Unix 域套接字文件 f
- `--user=u`（或 `-u u`）— 以用户 u 身份登录数据库
- `--wait`（或 `-w`）— 如果数据库宕机，尝试重新连接

# 18
## 最后的话题

奥妙与晦涩。过时的与先进的。本章包含适合那些需要了解 Bash shell 所有细节的人的主题混合。

## echo 命令

内置的 **echo** 命令是 *printf* 的早期形式。Bash 提供它以兼容 Bourne shell。*echo* 不使用格式字符串；它显示所有变量，就好像使用了“$@\n”格式一样。当您不需要 *printf* 的完整功能时，它有时可以作为快捷方式使用。

```
$ echo "$BASH_VERSION"
2.05a.0(1)-release
```

在显示字符串后会自动添加换行符。可以使用 -n（*no new line*）开关来抑制它。

```
$ echo -n "This is "; echo "one line."
This is one line
```

如果使用 -e（*escape*）开关，*echo* 会将某些转义序列解释为特殊字符。

- `\\a` — 蜂鸣声（“警告”）
- `\\b` — 退格符
- `\\c` — 抑制下一个字符；在字符串末尾，抑制末尾的换行符
- `\\e` — 转义字符
- `\\f` — 换页符
- `\\n` — 换行符（新行）
- `\\r` — 回车符
- `\\t` — 水平制表符
- `\\v` — 垂直制表符
- `\\\\` — 反斜杠
- `\\num` — 字符的八进制 ASCII 码

```
$ echo '\101'
\101
$ echo -e '\101'
A
```

-e 开关开启转义序列解释。这是默认设置。

## set 的更多用途

内置 set 命令用于开启或关闭某些 shell 选项。然而，set 还有其他用途。

当 set 有参数时，参数会被分配给位置参数。这是更改位置参数值的唯一方法。

```
$ printf '%s %s \n' "$1" "$2" "$3"

$ set 'first' 'second' 'third'
$ printf '%s %s \n' "$1" "$2" "$3"
first second third
```

当 set 单独使用时，它的作用类似于 env 命令，显示所有变量。它还显示所有函数。

## 日期转换

Linux date 命令以多种格式返回当前日期。带有 -d 开关的 date 可以转换任意文本日期并以不同格式显示。

```
$ date -d 'may 1 10am'
Tue May  1 09:00:00 2001
$ date -d '8pm 01/03/02'
Thu Jan  3 19:00:00 2002
```

在一些较旧的 Linux 发行版中，提供了 convdate 命令，它执行类似的功能。

```
$ convdate '8pm 01/03/02'
Thu Jan  3 19:00:00 2002
```

-n（*number*）开关返回自 1970 年 1 月 1 日（纪元）以来的秒数。-c 开关返回距纪元秒数对应的日期字符串。

```
$ convdate -n 'may 1 10am'
998722000
$ convdate -o 998722000
Tue May  1 10:00:00 2001
```

## 补全

当 Bash 猜测用户正在输入什么时，就会发生补全。在文件名补全中，用户按下 Tab 键（或 vi 模式下的 Esc 键）来确定 Bash 是否根据前几个字符识别正在输入的文件名。这种补全机制可以通过使用两个内置命令供 shell 脚本使用。

*compgen*（*generate completions*）命令生成可能的补全列表。为了使用 *compgen*，您需要使用 *-A*（*action*）开关指明补全类型：

- `-A alias`（或 `-a`）— 别名
- `-A arrayvar` — 数组变量名
- `-A binding` — Bind 命令键绑定名称
- `-A builtin`（或 `-b`）— 内置 shell 命令
- `-A command`（或 `-c`）— Linux 命令
- `-A directory`（或 `-d`）— 目录名
- `-A disabled` — 被禁用的内置 shell 命令名称
- `-A enabled` — 被启用的内置 shell 命令名称
- `-A export`（或 `-e`）— 导出的 shell 变量
- `-A group`（或 `-g`）— 组名补全
- `-A file`（或 `-f`）— 文件名
- `-A functions` — Shell 函数名
- `-A helpopic` — Shell *help* 命令识别的主题
- `-A hostname` — *HOSTFILE* 变量指示的文件中的主机名
- `-A job`（或 `-j`）— 作业表中的作业名称
- `-A keyword`（或 `-k`）— Shell 保留字
- `-A running` — 正在运行的作业名称
- `-A service`（或 `-s`）— 完成网络服务名称
- `-A setopt` — 短 -o 选项的名称
- `-A shopt` — 短选项的名称（不是 -o 选项）
- `-A signal` — 信号名称
- `-A stopped` — 停止的作业名称
- `-A user`（或 `-u`）— 用户名
- `-A variable`（或 `-v`）— Shell 变量名

要查找所有以 *t* 开头的目录，使用

```
$ compgen -A directory t
tia
test
texttools
```

补全过程比您想象的要复杂得多。脚本可以运行通过 `-F (function)` 开关指定的函数或程序，或使用 `-C (command)` 开关运行命令，以创建初始的可能补全列表。参数包括正在补全的命令名称（$1）、正在补全的 shell 单词（$2）以及正在补全的单词之前的单词（$3）。

```
$ function info { printf "$1\n" "$Cmd=$1 Word=$2 Prev=$3" ; }
$ compgen -A directory -F info t
bash: warning: compgen: -F option may not work as you expect
Cmd= Word=t Prev=
temp
tia
texttools
```

在这种情况下，*t* 是正在补全的单词，且 *t* 之前没有命令或单词。

可接受的匹配结果返回在 COMPREPLY 变量中（或者对于 -O 返回到标准输出）。将 `trucking_reports` 赋值给 COMPREPLY 会将 `trucking_reports` 添加到可能的匹配列表中。

```
$ function info { printf "$1\n" "$Cmd=$1 Word=$2 Prev=$3" ; \
        COMPAREPLY="trucking_reports" ; }
$ compgen -A directory -F info t
bash: warning: compgen: -F option may not work as you expect
Cmd= Word=t Prev=
temp
tia
texttools
trucking_reports
```

在完成函数和命令时，几个变量提供额外信息。COMP_LINE 是正在补全的命令。COMP_POINT 是光标相对于命令起始位置的位置。COMP_WORDS 是命令中单词的数组。COMP_CWORD 是光标在 COMP_WORDS 数组中的索引位置。

Bash 包含许多命令的配置文件，以便知道需要哪种补全。这些被称为 *completion specifications*。如果使用 -G 开关，过程将接收一个路径名模式并创建额外的匹配。在找到可能的解决方案列表后，shell 变量 FIGNORE 中找到的任何项目都会被丢弃。-n（*words*）开关用于缩小列表范围。

在用户的自定义过滤之后，-X（*exclude*）开关应用路径名模式匹配以进一步减少列表。&amp; 代表正在补全的单词的文本


替换。通过 `-s` 开关提供的后缀或通过 `-P` 开关提供的前缀将添加到所有保留的项目中。这是最终列表。

```bash
$ compgen -A directory -X tia t
test
texttools
$ compgen -A directory -S '.txt,' -X tia t
test.txt
texttools.txt
```

`complete` 命令在补全特定命令时设置默认的补全行为。它使用与 `compgen` 相同的选项，但将其保存以供该命令未来使用。你也可以以这种方式分配补全命令和函数。

```bash
$ compgen -A directory t
temp
tia
texttools
$ complete -A directory -X tia ls
$ ls t
temp
texttools
$ complete -A directory -P info ls
$ ls t
Cmd=ls P=info ls
$ complete -p ls
complete -d -P info ls
```

`-p`（`print`）开关列出当前已定义的命令补全规则。

```bash
$ complete -r ls
$ complete -d -P info ls
```

`-r`（`remove`）命令移除已定义的补全规则。

`-o`（`option`）开关用于设置各种选项。`-o dirnames` 在没有其他匹配项时尝试匹配目录。`-o filenames` 允许对单词进行更改（例如去掉末尾的斜杠），以帮助识别匹配项。`-o default` 是默认值，在匹配失败时不提供特殊处理。较新版本的 Bash 还支持 `-o nospace`，它防止在补全后的单词末尾附加空格。

补全命令可以与函数组合，以创建功能强大的新命令行实用工具。

## 区域设置（Locales）

在 Linux 中，用户的语言和文化由其“区域设置”（locale）表示。区域设置信息存储在环境变量中。其中一些标准变量包括：

- `LC_CTYPE`—字符类别和大小写转换
- `LC_COLLATE`—字符集的排序规则
- `LC_NUMERIC`—基数字符（用于分隔数字和基数的字符）和千位分隔符
- `LC_MONETARY`—类似于 `LC_NUMERIC`，但用于格式化货币
- `LC_MESSAGES`—诊断消息和用户对话的格式化
- `LC_TIME`—本地月份的拼写以及日期格式化的其他方面

这些变量中的每一个都包含要使用的区域设置类别名称。这些类别存储在位于 `/usr/lib/locale` 的区域设置数据库中。数据库通过 Linux 的 `localedef` 命令进行更新。

`locale` 命令显示当前的区域设置配置。`en_US` 是美国英语的类别，`en_CA` 是加拿大英语，`fr_CA` 是加拿大法语，等等。

```bash
$ locale
LANG=en_US
LC_CTYPE="en_US"
LC_NUMERIC="en_US"
LC_TIME="en_US"
LC_COLLATE="en_US"
LC_MONETARY="en_US"
LC_MESSAGES="en_US"
LC_PAPER="en_US"
LC_NAME="en_US"
LC_ADDRESS="en_US"
LC_TELEPHONE="en_US"
LC_MEASUREMENT="en_US"
LC_IDENTIFICATION="en_US"
LC_ALL=
```

`locale -a`（`all`）显示所有区域设置类别的列表。`-m`（`map`）开关显示所有字符映射的列表。

区域设置通常在 Linux 安装过程中由用户选择。若要更改区域设置，请为某个 `LC` 变量分配新值。

```bash
$ LC_NUMERIC=fr_CA # 使用加拿大法语数字约定
```

某些 Bash 和 Linux 命令受配置的影响。例如，美元双引号替换会将字符串转换为当前区域设置的首选字符集。`LC_COLLATE` 的值会影响 Bash 进行路径名模式匹配的顺序，以及 Linux `sort` 命令的排序顺序。

## du 命令

Linux `du`（`disk usage`）命令显示目录及其内部所有子目录所使用的磁盘空间量。`-s`（`summarize`）开关仅显示总计。`--human-readable`（或 `-h`）开关将总计转换为最接近的兆字节或吉字节。

```bash
$ pwd
/home/kburch
$ du --summarize --human-readable
36M		.
$ du --summarize --human-readable . archive
36M		.
28M		archive
```

对于脚本，有一些开关控制结果的分组方式以及使用的单位。空间总和可以是字节（或 `-b`）、千字节（或 `-k`）、兆字节（或 `-m`），或者 `-blocksize=b` 字节的块。默认单位是千字节。`-si`（或 `-h`）开关使用 1000 而不是 1024 作为单位基数。你可以确定命令行中所有文件的 `-total`（或 `-c`），以及目录内所有文件的 `-all`（或 `-a`）总计。`-separate-dirs`（或 `-s`）显示子目录的总计，这是默认行为。

数量和文件名由制表符（Tab）字符分隔。若要提取其中一列，请使用 `cut` 命令。

```bash
$ TAB=$(printf '\t')
$ du -all -kilobytes incoming_orders | cut -d"$TAB" -f1
20
12
40
56
132
```

其他开关影响文件的搜索方式。`-dereference-args`（或 `-D`）开关解引用作为符号链接的路径。`-count-links`（`-l`）开关将指向同一文件的每个硬链接计为单独的文件。`-one-file-system`（`-x`）开关将搜索限制在当前文件系统中。搜索可以限制在 `-max-depth=n` 层子目录级别，或者可以通过 `-exclude=pattern` 排除某些文件，或通过 `-exclude-from=file`（或 `-X file`）中的文件列表排除文件。

## 内存使用情况

Linux `free` 命令报告系统中的内存使用情况。

```bash
$ free
              total        used        free      shared  buffers  cached
Mem:         61792       58756        3036       10116    36152    8988
-/+ buffers/cache:      13616       48176
Swap:        514072        8180      505892
```

total、used 和 free 列分别表示内存总量、当前由 Linux 内核使用的内存量以及空闲内存量。free 和 used 列的总和始终等于 total。最后三列显示已使用内存的分配情况；即在共享内存中、缓冲区或缓存中。最后一行显示在磁盘上分配、已使用和空闲的交换空间。

`-t` 开关显示额外的总计行。

```bash
$ free -t
              total        used        free      shared  buffers  cached
Mem:         61792       58760        3032       10136    36152    8988
-/+ buffers/cache:      13620       48172
Swap:        514072        8180      505892
Total:       575864       66940      508924
```

默认情况下，显示单位为千字节。`-b` 开关显示字节，`-m` 开关显示兆字节。

`free` 对脚本不友好。要获取所需信息，必须使用 `cut` 和 `grep`。各列由空格分隔，必须压缩空格才能配合 `cut` 使用。

```bash
$ free | grep "Mem"
Mem: 61792 58880 2912 10120 36156 9068
$ free | grep "Mem" | tr -s ' '
Mem: 61792 58876 2916 10120 36156 9068
$ free | grep "Mem" | tr -s ' ' | cut -d' ' -f2
61792
```

## noclobber 和强制覆盖

通常，当使用 `>` 重定向标准输出时，同名现有文件会被覆盖。

```bash
$ printf "First line\n" > temp.txt
$ printf "Second line\n" > temp.txt
$ cat temp.txt
Second line
```

为防止覆盖重要文件提供安全措施，`noclobber` shell 选项防止重定向覆盖文件。

```bash
$ shopt -s noclobber
$ printf "First line\n" > temp.txt
$ printf "Second line\n" > temp.txt
bash: temp.txt: cannot overwrite existing file
```

可以使用 `>|` 代替 `>` 来强制覆盖文件。

```bash
$ printf "Second line\n" >| temp.txt
$ cat temp.txt
Second line
```

`noclobber` 选项主要旨在用于交互式会话，其中用户可能会输入错误的文件名。然而，它也可以在脚本中用作调试工具，识别那些使用了 `>` 而不是 `>>` 或脚本运行之间未清理文件的地方。

例如，在以下脚本片段中，创建了日志，但日志中缺少日期。使用 `noclobber` 时，Bash 会对覆盖日期的那一行显示错误。

```bash
#!/bin/bash

shopt -s noclobber

declare -rx LOG="log.txt"

date > $LOG
printf "Results of night batch run:\n" > $LOG

# 等等。
```

`printf` 应使用 `>>` 重定向。不应在脚本中使用 `>`，因为这会使使用 `noclobber` 的目的落空。

## fc 命令

内置 `fc`（*fix command*）命令列出并编辑命令历史。此命令在很大程度上已被 `history` 和 `!` 历史召回命令所取代。

`fc` 启动默认编辑器以修改最近执行的命令。当你离开编辑器时，命令将执行。不需要整个命令，只需命令的首字符即可进行匹配。或者，你可以指定要编辑的行范围。如果行以减号开头，则从历史末尾开始计数行（其中 `-1` 是最近的命令）。

使用 `-s`（*substitute*）开关，`fc` 不启动编辑器，而是在执行命令前将指定的单词的所有出现替换为另一个单词。例如，要使用 `pico` 编辑文件，然后使用 `gcc` 编译器编译该文件，请使用 `-s "pico=gcc"` 将 `pico` 替换为 `gcc`。

```bash
$ pico project.c
$ fc -s "pico=gcc" p
gcc project.c
```

`-l`（*list*）开关列出历史中最近期的项目，你可以指定要显示的首行，或首行和末行。`-n`（*no line numbers*）开关抑制历史中的行号，而 `-r`（*reverse*）则反转其打印顺序。

## ! 字指定符和修饰符

`!` 历史召回命令的基本功能在第 3 章中讨论过。事实上，`!` 具有许多功能，使你能够选择要召回的命令，并确定在执行前是否应将新信息替换到命令中。




## Shell 历史词指定符
`:!` 识别词指定符，它们可以召回不同于命令的某个词。这里的“词”指的是 shell 意义上的词；即由空白字符分隔的字符串。词指定符使用冒号与历史召回命令的其余部分分隔。

- `!n` 选择历史行中的第 n 个词。第 0 个词是命令本身。

```bash
$ printf "%s\n" "date"^\
Jul 14 14:34:41 EDT 2001
$ NOW=!!!2
NOW="date"^\
$ printf "%s\n" "$NOW"\
Jul 14 14:34:55 EDT 2001
```

- `!^` 指示命令后的第一个词，等同于 `!:1`。
- `!$` 指示最后一个词。
- `!*` 代表从 `^` 到 `$`。

```bash
$ touch temp.txt
$ rm !!!^\
rm temp.txt
```

其他指定符包括：
- `!:$` （由历史搜索匹配的最后一个词）
- `!:x–y` （从词 x 到词 y，包含两端）
- `!:x*` （从词 x 到结尾）
- `!:x-` （从词 x 到结尾，但不包括最后一个词）

```bash
$ printf "%s and %s\n" "apples" "oranges"\
apples and oranges
$ printf "Two fruits are %s and %s\n" !!!:2*\
printf "Two fruits are %s and %s\n" "apples" "oranges"
Two fruits are apples and oranges
```

在词指定符之后，你可以包含一系列命令修饰符，每个修饰符前都有一个冒号：
- `:s` — 指示路径名的后缀
- `:g` — 使更改在整个命令行范围内“全局”生效
- `:h` — 指示路径名的路径部分
- `:p` — 打印但不执行
- `:r` — 显示不含文件名的路径名
- `:s/old/new` — 将字符串 old 的第一次出现替换为 new（本质上与 `:s` 相同）
- `:t` — 显示路径名的文件名部分
- `:q` — 对替换后的词加引号
- `:x` — 将词拆分为单个单词后对其加引号
- `:l` — 重复上一个 `:s`

这里有一些示例。

```bash
$ touch /home/kburch/temp.txt
$ ls -l /home/kburch/temp.txt
-rw-rw-r-- 1 kburch kburch 0 Jul 5 14:49 /home/kburch/temp.txt
$ ls -l !!2:t
ls -l temp.txt
-rw-rw-r-- 1 kburch kburch 0 Jul 5 14:48 temp.txt
$ ls -l *1:2:2:e
ls -l *.txt
-rw-rw-r-- 1 kburch kburch 0 Jun 25 12:02 last_orders.txt
-rw-rw-r-- 1 kburch kburch 592 May 11 14:45 orders.txt
-rw-rw-r-- 1 kburch kburch 0 Jul 5 14:48 temp.txt
-rw-rw-r-- 1 kburch kburch 33 Jul 4 14:48 test.txt
$ ls -l 1-3:2:g/temp/orders
ls -l /home/kburch/orders.txt
-rw-rw-r-- 1 kburch kburch 592 May 11 14:45 /home/kburch/orders.txt
```

## 从 C 运行脚本
脚本通常与 C 等高级语言结合使用，以便无需重新编译和链接大型项目即可提供定制化功能。虽然 Guile 和 Scheme 等脚本语言是流行的选择，但 Bash 本身也是一种脚本语言，也许是 Linux 下最典型的脚本语言。

C 函数 `system` 启动一个 shell 并在该 shell 中运行命令。该命令的参数是一个字符串，它就像用户在交互式会话中键入该命令一样被执行。`system` 返回 shell 的退出状态，或者在启动 shell 出现问题时返回 -1。

清单 18.1 中展示的 C 程序运行一个 `ls` 命令。

**清单 18.1 c_system.c**

```c
/* c_system.c: run a shell command from C using system */

#include <stdio.h>
#include <stdlib.h>

int main() {
    int result;

    result = system("ls -l *.sh");
    return 0;
}
```

当程序运行时，shell 命令会被执行。

```bash
$ c_system
company.txt
log.txt
orders.txt
temp.txt
```

当使用 system 运行脚本时，会创建两个 shell 会话；一个用于 `system`，另一个用于运行脚本（除非脚本是使用 `execl` 启动的）。若要运行脚本而不是 shell 命令，C 的 `popen` 函数是一种更少麻烦的方法。`popen` 运行一个程序，并附接一个管道到或来自该程序，就像使用了 shell 管道操作符 | 一样。该命令有两个参数：要运行的程序及其参数，如果 C 程序读取脚本的标准输出则为 `r`，如果程序写入脚本的标准输入则为 `w`。当程序完成时，使用 `pclose` 命令关闭管道。

对于 shell 脚本而言，`popen` 运行的程序是 Bash。你可以使用 `popen` 重写 `c_system.c` 程序，如清单 18.2 所示。

**清单 18.2 c_popen.c**

```c
/** c_popen.c: run a Bash command from C using popen */
#include <stdio.h>
#include <stdlib.h>

int main() {
    FILE *f = NULL;                  /* the pipe file */
    char s[255] = "";                /* a string buffer */

    f = popen("/bin/bash -c \"ls -l *.txt\"", "r"); /* open the pipe */
    while (!feof(f)) {              /* while more output */
        fgets(s, 255, f);          /* get the next line */
        printf("%s", s);            /* print the results */
    }
    pclose(f);                      /* close the pipe */

    return 0;                       /* successful status */
}
```

结果是一样的。

```bash
$ ./c_popen
company.txt
log.txt
orders.txt
temp.txt
```

如果 C 变量需要与 Bash 脚本共享，它们必须导出到 shell 的环境变量中。C 的 `putenv` 函数声明或更改一个环境变量。声明的形式应与 Bash 变量赋值相同。由于 `putenv` 会增加环境的大小，因此它可能会失败。如果赋值成功执行，该命令返回零。

使用 putenv 时的一个常见错误是重用分配给环境的字符串。该命令实际上创建了指向被分配字符串的指针；它并未将字符串复制到环境中。运行诸如 `putenv(s)` 这样的命令意味着字符串 `s` 必须保持原样，直到它从环境中移除为止。

为了举一个简单的变量共享示例，假设你创建了一个名为 `c_script.sh` 的脚本，用于将名为 `COUNT` 的变量乘以第一个脚本参数，如清单 18.3 所示。

**清单 18.3 c_script.sh**

```bash
#!/bin/bash
#
# c_script.sh: an example of exporting a C variable to a script

shopt -s -o nounset
let "COUNT=COUNT*$1"
echo "$COUNT"

exit 0
```

该脚本假设变量 `COUNT` 存在。

```bash
$ declare -ix COUNT=4
$ bash c_script.sh 3
12
```

使用 putenv 和 popen，可以将 C 变量复制到环境中，并从管道中读取该变量的新值，如清单 18.4 所示。

**清单 18.4 c_script.c**

```c
/* c_script.c: run a script from C using popen */

#include <stdio.h>
#include <stdlib.h>

int main() {

    FILE *f = NULL;                /* the pipe file */
    char env_count[255] = "";      /* string buffer for COUNT */
    int count = 5;                 /* C variable count */

    /* Declare COUNT in the environment */

    sprintf(env_count, "COUNT=%d", count);  /* declare env var */
    putenv(env_count);                  /* export it */
    
    f = popen("/bin/bash c_script.sh 2", "r"); /* open the pipe */
    fscanf(f, "%d", &count);            /* read new count */
    pclose(f);                          /* close the pipe */
    printf("count is %d\n", count);     /* print result */

    return 0;
}
```

当程序执行时，C 变量 `count` 被赋值 10。

```bash
$ c_script
count is 10
```

## 旅程的终点
当我开始写这本书时，我收到了很多诸如“关于 Bash shell 有什么可了解的？我使用 Bourne shell 已经 20 年了。”之类的评论。我会对他们说，“你知道 Bash 可以打开网络套接字吗？”他们盯着我看，问道，“真的吗？”

Bash 不仅仅是一个 Bourne shell 的继任者或 Korn shell 的流行替代方案。它是一个功能齐全的 shell，拥有强大的脚本语言和数十个内置命令和函数。它也是开源的，是 Linux 中值得捆绑使用的工具。

## 参考章节

### echo 命令开关
- `-G` — 不解释转义代码
- `-e` — 解释转义代码
- `-n` — 抑制尾随的换行符（新行）

### echo 转义代码
- `\a` — 蜂鸣声（"alert"）
- `\b` — 退格
- `\c` — 抑制下一个字符；在字符串末尾，抑制尾随的回车符
- `\E` — 转义字符
- `\f` — 换页符
- `\n` — 换行符（新行）




### compgen 命令开关

- `-A action`—选择补全类型
- `-C command`—运行命令并将其结果作为可能的补全项
- `-F func`—从 shell 函数 func 获取可能的补全项列表
- `-G globpat`—使用文件名通配模式 globpat 生成补全项
- `-P prefix`—为每个可能的补全项添加前缀
- `-o option`—指定 *compspecs* 的解析方式（默认值、文件名或目录名）
- `-S suffix`—为每个可能的补全项添加后缀
- `-W list`—指定一个可能的补全项列表
- `-X filterpat`—使用 *filterpat* 过滤补全列表

### 转义字符
- `\r`—回车
- `\t`—水平制表符
- `\v`—垂直制表符
- `\\`—反斜杠
- `\num`—字符的八进制 ASCII 码

# compgen 操作类型

- `-A alias`（或 -a）—别名
- `-A arrayvar`—数组变量名
- `-A binding`—命令键绑定名称
- `-A builtin`（或 -b）—内置 shell 命令
- `-A command`（或 -c）—Linux 命令
- `-A directory`（或 -d）—目录名
- `-A disabled`—已禁用的内置 shell 命令名称
- `-A enabled`—已启用的内置 shell 命令名称
- `-A export`（或 -e）—已导出的 shell 变量
- `-A group`（或 -g）—组名补全
- `-A file`（或 -f）—文件名
- `-A function`—shell 函数名
- `-A help`（或 -H）—shell help 命令识别的主题
- `-A hostname`—HOSTFILE 变量指定文件中记录的主机名
- `-A job`（或 -j）—作业表中的作业名称
- `-A keyword`（或 -k）—shell 保留字
- `-A running`—正在运行的作业名称
- `-A _setopt`—shopt -o 选项的名称
- `-A shopt`—shopt 选项的名称（非 -o 选项）
- `-A signal`—信号名称
- `-A stopped`—已停止的作业名称
- `-A user`（或 -u）—用户名
- `-A variable`（或 -v）—shell 变量名

### complete 命令开关

- `-A action`—选择补全类型
- `-C command`—运行命令并将其结果作为可能的补全项
- `-F func`—从 shell 函数 func 获取可能的补全项列表
- `-G globpat`—使用文件名通配模式 globpat 生成补全项
- `-P prefix`—为每个可能的补全项添加前缀
- `-p`—列出补全项
- `-o option`—指定补全项的解析方式（默认值、文件名或目录名）
- `-r`—移除补全
- `-S suffix`—为每个可能的补全项添加后缀
- `-W list`—指定一个可能的补全项列表
- `-X filterpat`—使用 filterpat 过滤补全列表

### du 命令开关

- `-all`（或 -a）—记录所有文件的计数，而不仅仅是目录
- `-block-size=size`—使用大小为 size 字节的块
- `-bytes`（或 -b）—以字节为单位打印大小
- `-total`（或 -c）—生成总计
- `-dereference-args`（或 -B）—解析参数中的符号链接
- `-human-readable`（或 -h）—打印四舍五入到易于理解的数值的大小
- `-si`（或 -H）—类似于 -human-readable，但使用 1000 的幂而非 1024
- `-kilobytes`（或 -k）—以 KB（千字节）为单位打印大小
- `--count-links`（或 `-l`）—如果文件是硬链接，则每次记录其大小
- `--dereference`（或 `-L`）—解析所有符号链接
- `--megabytes`（或 `-m`）—类似于 `-block-size=1048576`
- `--separate-dirs`（或 `-S`）—不包含子目录的大小
- `--summarize`（或 `-s`）—仅显示每个参数的总计
- `--one-file-system`（或 `-x`）—跳过位于不同挂载文件系统上的目录
- `--exclude-from=`*f*（或 `-X` *f*）—排除匹配文件 *f* 中列出的通配模式的文件
- `--exclude=`*PAT*—排除匹配通配模式 *PAT* 的文件
- `--max-depth=`*N*—当根 `du` 目录向下 *N* 层或更少时，打印目录（或在使用 `--all` 时为文件）的总计

### ! 单词修饰符

- `:e`—表示路径名的后缀
- `:g`—使更改在整个命令行上“全局”生效
- `:h`—表示路径名的路径部分
- `:p`—打印但不执行
- `:x`—表示不含文件名的路径名
- `:s/`*old*`/`*new*`—将字符串 `old` 的第一次出现替换为 `new`（本质上与 `:`* 相同）
- `:t`—表示路径名的文件名部分
- `:q`—引用被替换的单词
- `:w`—引用在拆分为单个单词之后的单词
- `:g`—重复最后一次 `:s`

## 一个完整的示例

PEEK 是一个展示 shell 脚本功能的有趣且实用的例子。作为一个资源监控和故障排除脚本，`peek` 会休眠 20 或 30 秒。唤醒后，它会使用 `free` 和 `vmstat` 等命令检查（或“窥视”）系统统计信息，并绘制代表计算机活动的图形。在显示区域的顶部，会显示最后更新的时间以及实际的 CPU 和内存使用情况。在图形下方，会出现关于潜在问题或瓶颈的警告。

由于 `vmstat` 等命令的格式随时间变化，脚本可能需要针对某些发行版进行修改。此版本是为 Red Hat 7.3 设计的。图 A.1 展示了 `peek` 的运行效果。

![](img/7da864b222941ec315ee1c456ff472dd_357_0.png)

完整的源代码见列表 A.1。

# 列表 A.1 peek.sh 的完整源代码

```bash
#!/bin/bash
#
# peek.sh
#
# Show system resource usage graphs. Record and display alarms messages
# for important conditions
#
# by Ken O. Burtch
#
# CVS: $Id$
#
# -------------------------------------------

shopt -s -o nounset
shopt -s -o noclobber


# Bash Variabes
#
# Bash may not declare these. Declare them before we test their values.
#
# -------------------------------------------

declare -ri COLUMNS                    # BASH COLUMNS variable
declare -ri LINES                     # BASH LINES variable


# Global Declarations
#
# -------------------------------------------

declare -rx SCRIPT=$(0##*/)           # script name

# Commands paths
# Change these paths as required for your system

declare -rx ping="/bin/ping"          # check network connections
declare -rx vmstat="/usr/bin/vmstat"  # check resource usage
declare -rx df="/bin/df"             # check disk space
declare -rx free="/usr/bin/free"     # check free memory
declare -rx hostname="/bin/hostname"  # name of computer

# Settings
#
# How long vmstat tests and delay between screen updates. These values should
# be good for most systems.

declare -rix INTERVAL=4 # vmstat interval (seconds)
declare -rix SLEEP=23 # sleep time between updates (seconds)

# Alarm Settings
#
# These determine when an alarm is announced. Changes these to suit your
# system.

declare -rix THRASHING=8000 # context switch limit before warning (faults)
declare -rix DISK_LIMIT=2500 # disk bottleneck limit before warning (faults)
declare -rix CPU_LIMIT=90 # CPU busy limit before warning (percent)
declare -rix NET_LIMIT=9 # LAN ping limit before warning (mseconds)
declare -rix MEM_LIMIT=95 # Virtual memory warning limit (percent)
declare -rx LAN_HOST=hitcomi # Computer to ping over LAN (hostname)
declare -rix DISK_GRAPH_TOP=100 # disk interrupt limit (interrupts)

# Graph bar values
#
# All bars start at zero for each of the seven columns

declare -i CPU1=0 CPU2=0 CPU3=0 CPU4=0 CPU5=0 CPU6=0 CPU7=0 CPU8=0
declare -i MEM1=0 MEM2=0 MEM3=0 MEM4=0 MEM5=0 MEM6=0 MEM7=0 MEM8=0
declare -i PAG1=0 PAG2=0 PAG3=0 PAG4=0 PAG5=0 PAG6=0 PAG7=0 PAG8=0
declare -i NET1=0 NET2=0 NET3=0 NET4=0 NET5=0 NET6=0 NET7=0 NET8=0
declare -i DSK1=0 DSK2=0 DSK3=0 DSK4=0 DSK5=0 DSK6=0 DSK7=0 DSK8=0

# Alarm Log
#
# The alarm log holds no more than 8 entries

declare LOG1 LOG2 LOG3 LOG4 LOG5 LOG6 LOG7 LOG8

declare LASTLOG= # last alarm message
declare SYSTEM_OK= # cleared if there was an alarm
declare LOG_UPDATED= # set if the log has changed

# Global constants
#
# Put put values in variables for speed

declare -rx HOME_CURSOR=\'tput home\' # cursor to top-left corner
declare -rx UP=\'tput cuu1\' # move cursor up
declare -rx DOWN=\'tput cud1\' # move cursor down
\#declare -rx DOWN=\'echo -e \"\e[B\"\' 
declare -rx LEFT=\'tput cub1\' # move cursor left
declare -rx RIGHT=\'tput cuf1\' # move cursor right
```





## 列表 A.1 续

```bash
declare -rx CEOL='tput el' # 清除到行尾
declare -rx INVERSE='tput smso' # 开启反色显示
declare -rx INVERSE_OFF='tput rmso' # 关闭反色显示
declare -rx UP10='$SUSSUSSUPSUSPSSUSSUPSUSPSSUSSUP$'
declare -rx DOWN10='$DOWN$DOWN$DOWN$DOWN$DOWN$DOWN$DOWN$DOWN$DOWN$DOWN$'

# VMSTAT 字段

declare -ix PROC_R= # 就绪进程
declare -ix PROC_B= # 阻塞进程
declare -ix PROC_W= # 已交换出进程的
declare -ix MEM_SWAPd= # 活动虚拟内存 (KB)
declare -ix MEM_FREE= # 空闲虚拟内存 (KB)
declare -ix MEM_BUF= # 缓冲空间 (KB)
declare -ix MEM_CACHE= # 磁盘缓存 (KB)
declare -ix SWAP_SI= # 换入页数
declare -ix SWAP_SO= # 换出页数
declare -ix IO_BLKI= # 发送到 IO 设备的块数
declare -ix IO_BLKO= # 从 IO 设备接收的块数
declare -ix SYS_S= # 中断（包括时钟中断）
declare -ix SYS_CS= # 上下文切换
declare -ix CPU_US= # 用户 CPU 使用率
declare -ix CPU_SY= # 系统 CPU 使用率
declare -ix IDLE= # CPU 空闲时间

# 其他全局变量

declare TIME=`date '+%H:%M:%S'` # 当前时间
declare TMP= # 临时结果
declare TMP2=
declare TMP3=
declare -i CPU= # 当前 CPU 忙碌百分比
declare -i MEM= # 当前虚拟内存使用百分比
declare PAGE= # 当前上下文切换次数
declare NET= # 当前网络速度 (毫秒/秒)
declare LEN= # 字符串长度
declare OLD= # 用于修正 vmstat 结果
declare -i DSK= # 磁盘活动（中断）
declare -i MEM_TOTAL=0 # 总虚拟内存

# 函数

# 垂直条形图
# 绘制一个高度为 10 个字符的垂直条形图。条形使用 `#` 绘制，
# 空白区域使用 `.` 绘制。
#
# 参数 1 - 图表的值，百分比
# 参数 2 - 条形的旧值，用于加速绘制
#

function vertical_bar {

    declare -i DOTCNT  # 要绘制的点数
    declare -i CNT     # 要绘制的名号数

    # 如果新条形在此处的值与旧条形相同，则无需重新绘制，
    # 因为内容没有变化——除非它是零，因为我们可能正在
    # 首次绘制这一列。

    if [ $1 -ne 0 ] ; then
        if [ $1 -eq $2 ] ; then
            printf "%s" "$RIGHT""$RIGHT"
            return

        fi
    fi

    # 将条形的大小转换为 0 到 10 之间的数字
    # 四舍五入到最接近的整数
    # 如果百分比超出范围，则限制在 0 到 10 之间

    if [ $1 -gt 100 ] ; then
        CNT=10
    elif [ $1 -lt 0 ] ; then
        CNT=0
    else
        CNT=$((($1+5) / 10))     # 0..100 四舍五入到 0..10
    fi

    # 绘制垂直条形。DOTCNT 是要绘制的点数，
    # 用于填充图表。

    DOTCNT=10-CNT
    while [ $((DOTCNT--)) -gt 0 ] ; do
        printf "%s" ".""$DOWN""$LEFT"
    done
    while [ $((CNT--)) -gt 0 ] ; do
        printf "%s" "#""$DOWN""$LEFT"
    done

    printf "%s" "$SUP10" "$RIGHT""$RIGHT"

}

readonly -f vertical_bar
declare -t vertical_bar


# CPU 图表
#
# 更新垂直条形 CPU 使用率图表。
# 参数 1 - 要添加到图表中的新条形高度
# ______________________________________

function cpu_graph {

 if [ -z "$1" ]; then # 调试
        alarm "$FUNCNAME 接收到空字符串"
        return
fi
LAST="$SCPUB"
CPU8="$SCPUB"
CPU7="$SCPU6"
CPU6="$SCPU5"
CPU5="$SCPU4"
CPU4="$SCPU3"
CPU3="$SCPU2"
CPU2="$SCPU1"
CPU1="$1"

        vertical_bar "$SCPU8" "$LAST"
        vertical_bar "$SCPU7" "$SCPUB"
        vertical_bar "$SCPU6" "$SCPUB"
        vertical_bar "$SCPU5" "$SCPUB"
        vertical_bar "$SCPU4" "$SCPU5"
        vertical_bar "$SCPU3" "$SCPU4"
        vertical_bar "$SCPU2" "$SCPU3"
        vertical_bar "$SCPU1" "$SCPU2"

        printf "%s" "$RIGHT""$RIGHT"

}

readonly -f cpu_graph
declare -t cpu_graph

```

```bash
# MEM 图表
# # 更新垂直条形内存图表
# 参数 1 - 要添加到图表中的新条形高度
# ______________________

function mem_graph {

    # 健全性检查

    if [ -z "$1" ] ; then # 调试
        alarm "$FUNCNAME 接收到空字符串"
        return
    fi

    # 将新值插入图表

    LAST=$MEM8
    MEM8=$MEM7
    MEM7=$MEM6
    MEM6=$MEM5
    MEM5=$MEM4
    MEM4=$MEM3
    MEM3=$MEM2
    MEM2=$MEM1
    MEM1="$1"

    # 绘制条形

    vertical_bar "$MEM8" "$LAST"
    vertical_bar "$MEM7" "$MEM8"
    vertical_bar "$MEM6" "$MEM7"
    vertical_bar "$MEM5" "$MEM6"
    vertical_bar "$MEM4" "$MEM5"
    vertical_bar "$MEM3" "$MEM4"
    vertical_bar "$MEM2" "$MEM3"
    vertical_bar "$MEM1" "$MEM2"

    printf "%s" "$RIGHT""$RIGHT"
}
readonly -f mem_graph
declare -t mem_graph

# PAGE 图表
# 更新垂直条形页面错误图表
# 参数 1 - 要添加到图表中的新条形高度

function page_graph {
    # 健全性检查
    if [ -z "$1" ]; then # 调试
        alarm "$FUNCNAME 接收到空字符串"
        return
    fi

    # 将新值插入图表

    LAST="$PAG8"
    PAG8="$PAG7"
    PAG7="$PAG6"
    PAG6="$PAG5"
    PAG5="$PAG4"
    PAG4="$PAG3"
    PAG3="$PAG2"
    PAG2="$PAG1"
    PAG1="$1"

    # 绘制条形

    vertical_bar "$PAG8" "$LAST"
    vertical_bar "$PAG7" "$PAG8"
    vertical_bar "$PAG6" "$PAG7"
    vertical_bar "$PAG5" "$PAG6"
    vertical_bar "$PAG4" "$PAG5"
    vertical_bar "$PAG3" "$PAG4"
    vertical_bar "$PAG2" "$PAG3"
    vertical_bar "$PAG1" "$PAG2"
    printf "%s" "$RIGHT""$RIGHT"
}

readonly -f page_graph
declare -t page_graph

# NET 图表
# 更新垂直条形网络流量图表
# 参数 1 - 要添加到图表中的新条形高度
#
----------------------

function net_graph {

    # 健全性检查

    if [ -z "$1" ] ; then # 调试
        alarm "$FUNCNAME 接收到空字符串"
        return
    fi

    # 将新值插入图表

    LAST="$SNET8"
    NET8="$SNET7"
    NET7="$SNET6"
    NET6="$SNET5"
    NET5="$SNET4"
    NET4="$SNET3"
    NET3="$SNET2"
    NET2="$SNET1"
    NET1="$1"

    # 绘制条形

    vertical_bar "$SNET8" "$LAST"
    vertical_bar "$SNET7" "$SNET8"
    vertical_bar "$SNET6" "$SNET7"
    vertical_bar "$SNET5" "$SNET6"
    vertical_bar "$SNET4" "$SNET5"
    vertical_bar "$SNET3" "$SNET4"
    vertical_bar "$SNET2" "$SNET3"
    vertical_bar "$SNET1" "$SNET2"

    printf "%s" "$RIGHT" "$RIGHT"

}
readonly -f net_graph
declare -t net_graph

# DISK 图表
#
# 更新垂直条形磁盘中断图表
# 参数 1 - 要添加到图表中的新条形高度
#
function disk_graph {
## 健全性检查
if [ -z "$1" ] ; then # 调试
alarm "$FUNCNAME 接收到空字符串"
return
fi
# 将新值插入图表
LAST="$DSK8"
DSK8="$DSK7"
DSK7="$DSK6"
DSK6="$DSK5"
DSK5="$DSK4"
DSK4="$DSK3"
DSK3="$DSK2"
DSK2="$DSK1"
DSK1="$1"
# 绘制条形
vertical_bar "$DSK8" "$LAST"
vertical_bar "$DSK7" "$DSK8"
vertical_bar "$DSK6" "$DSK7"
vertical_bar "$DSK5" "$DSK6"
vertical_bar "$DSK4" "$DSK5"
vertical_bar "$DSK3" "$DSK4"
vertical_bar "$DSK2" "$DSK3"
vertical_bar "$DSK1" "$DSK2"
printf "%s" "$RIGHT""$GRIGHT"
}
readOnly -f disk_graph
declare -t disk_graph
# 警报
#

# 向警报日志添加消息。重复的消息将被丢弃。
# 参数 1 = 要添加的消息
#
________

function alarm {
    # 如果本次有任何记录，意味着系统不正常，即使是
    # 一条被抑制的重复消息

    SYSTEM_OK=

    # 忽略重复的警报
    [ "$1" = "$LASTLOG" ] && return
    LASTLOG=$1

    # 将日志消息添加到警报列表中
    LOG8="$LOG7"
    LOG7="$LOG6"
    LOG6="$LOG5"
    LOG5="$LOG4"
    LOG4="$LOG3"
    LOG3="$LOG2"
    LOG2="$LOG1"
    LOG1="$TIME - "$1"

    LOG_UPDATED=1
}
readonly -f alarm
declare -t alarm

#
________
# 主脚本从这里开始
#
________

# 用法/帮助
#
________

if [ $# -gt 0 ] ; then
    if [ "$1" = "-h" -o "$1" = "-help" ] ; then
        printf "$\n" "$SCRIPT::$LINE0: 显示系统资源使用图表"
        printf "$\n" "此脚本没有参数"
        printf "\n"
```





# 附录 A

## 清单 A.1（续）

```bash
    exit 0
    else
        printf "&\n" "$SCRIPT:$LINENO: Unexpected options/parameters"
        exit 192
fi
fi

# Sanity checks
# -------------------------------

if [ ! -x "$p1ng" ] ; then
    printf "&\n" "$SCRIPT:$LINENO: Can't find/execute $p1ng" >&2
    exit 192
fi
if [ ! -x "$v$mat" ] ; then
    printf "&\n" "$SCRIPT:$LINENO: Can't find/execute $v$mat" >&2
    exit 192
fi
if [ ! -x "$4$#" ] ; then
    printf "&\n" "$SCRIPT:$LINENO: Can't find/execute $4$#" >&2
    exit 192
fi
if [ ! -x "$f$ee" ] ; then
    printf "&\n" "$SCRIPT:$LINENO: Can't find/execute $f$ee" >&2
    exit 192
fi
if [ -z "$LINES" ] ; then
    printf "&\n" "$SCRIPT:$LINENO: LINES is not declared. Export LINES" >&2
    exit 192
fi
if [ $LINES -lt 35 ] ; then
    printf "&\n" "$SCRIPT:$LINENO: Your display must be >= 35 lines high" >&2
    exit 192
fi
if [ -z "$COLUMNS" ] ; then
    printf "&\n" "$SCRIPT:$LINENO: COLUMNS is not declared. Export COLUMNS" >&2
    exit 192
fi
if [ $COLUMNS -lt 80 ] ; then
    printf "&\n" "$SCRIPT:$LINENO: Your display must be >= 80 columns wide" >&2
    exit 192
fi
if [ -z "$HOME_CURSOR" ] ; then
    printf "%s\n" "$SCRIPT:$LINENO: cannot HOME the cursor" >&2
    printf "%s\n" "on this $TERM display" >&2
    exit 192
fi
if [ -z "$UP" ]; then
    printf "%s\n" "$SCRIPT:$LINENO: cannot move the cursor UP" >&2
    printf "%s\n" "on this $TERM display" >&2
    exit 192
fi
if [ -z "$DOWN" ]; then
    printf "%s\n" "$SCRIPT:$LINENO: cannot move the cursor DOWN" >&2
    printf "%s\n" "(Some terminfo/termcap databases have curl/do set" >&2
    printf "%s\n" " improperly)" >&2
    printf "%s\n" " (Try declaring down as DOWN=\${'s[B]}" >&2
    exit 192
fi
if [ -z "$LEFT" ]; then
    printf "%s\n" "$SCRIPT:$LINENO: cannot move the cursor LEFT" >&2
    printf "%s\n" "on this $TERM display" >&2
    exit 192
fi
if [ -z "$RIGHT" ]; then
    printf "%s\n" "$SCRIPT:$LINENO: cannot move the cursor RIGHT" >&2
    printf "%s\n" "on this $TERM display" >&2
    exit 192
fi
if [ -z "$SCOL" ]; then
    printf "%s\n" "$SCRIPT:$LINENO: cannot clear to end of line" >&2
    printf "%s\n" "on this $TERM display" >&2
    exit 192
fi
if [ ! -x "$hostname" ]; then
    printf "%s\n" "$SCRIPT:$LINENO: cannot find or execute $hostname" >&2
    exit 192
fi
declare -rx HOST=`uname -n`                 # name of computer

# Get the total amount of physical memory

MEM_TOTAL=`free | grep ""Mem" | tr -s " " | cut -d" -f2`

# Clear the screen

tput reset
tput clear
```

```bash
printf "%s - system monitor script  Please wait...\n" "$0"

# _________________________
# Main Loop
# _________________________

while true ; do

    # Get the system statistics with vmstat

    TMP="nice -20 $vmstat $INTERVAL 2 2>&1"
    if [ $? -ne 0 ] ; then
        alarm "printf "vmstat error: $g" "$TMP" | tail -1"
        VMSTAT=
    else
        VMSTAT="printf "\$s\n" "$TMP" | tail -1"
    fi
    LEN=${#VMSTAT}  # length of VMSTAT
    OLD=$

    # Reduce all spaces to single spaces. Trim leading spaces

    while [ $LEN -ne $OLD ] ; do
        OLD=$LEN
        VMSTAT="${VMSTAT//}  /  }"
        VMSTAT="printf "\$a\n" "$VMSTAT" | sed 's/\\/\\g'
        LEN=${#VMSTAT}
    done

    # Extract the vmstat columns into variables
    # Use only what we need

    #PROC_R="printf "\$8\n" "$VMSTAT" | cut -d, -f1"
    #PROC_B="printf "\$8\n" "$VMSTAT" | cut -d, -f2"
    PROC_W="printf "\$8\n" "$VMSTAT" | cut -d, -f3"
    MEM_SWPD="printf "\$8\n" "$VMSTAT" | cut -d, -f4"
    MEM_FREE="printf "\$8\n" "$VMSTAT" | cut -d, -f5"
    MEM_BUP="printf "\$8\n" "$VMSTAT" | cut -d, -f6"
    MEM_CACHE="printf "\$8\n" "$VMSTAT" | cut -d, -f7"
    #SWAP_SI="printf "\$8\n" "$VMSTAT" | cut -d, -f8"
```

```bash
#SWAP_SO=`printf "%s\n" $VMSTAT | cut -d' ' -f9`
#IO_BLKI=`printf "%s\n" $VMSTAT | cut -d' ' -f10`
#IO_BLK0=`printf "%s\n" $VMSTAT | cut -d' ' -f11`
SYS_SI=`printf "%s\n" $VMSTAT | cut -d' ' -f12`
SYS_CS=`printf "%s\n" $VMSTAT | cut -d' ' -f13`
CPU_US=`printf "%s\n" $VMSTAT | cut -d' ' -f14`
CPU_SY=`printf "%s\n" $VMSTAT | cut -d' ' -f15`
IDLE=`printf "%s\n" $VMSTAT | cut -d' ' -f16`

# Get ready to update the screen
TIME=`date '+%H:%M:%S'`
SYSTEM_OK=1
LOG_UPDATED=0

# Perform the network test
#
# (some ping's won't return an error if it fails so we'll double check by
# making sure "trip" is in the result. No "trip" means probably an error
# message.)
TMP=`$ping $LAN_HOST -C 1 2>&1`
TMP2=`$?`
TMP3=`printf "%s" "$TMP" | grep trip`
if [ $TMP2 -ne 0 -o -z "$TMP3" ]; then
    alarm "Ping to LAN host $LAN_HOST failed: network load unknown"
    NET=99
else
    NET=`printf "%s\n" "$TMP3" | cut -d' ' -f4 | cut -d' ' -f1`
    if [ $(NET/0.4) = "msec" ]; then
        NET=`printf "%s\n" "$TMP3" | cut -d' ' -f5 | cut -d' ' -f1`
    fi
fi

# Draw stats bar at the top of the screen
printf "%s" "$HOME_CURSOR"$INVERSE$TIME
printf "%s" "CPU: $CPU_US% user, $CPU_SY% sys, $IDLE% idle
printf "%s\n" "MEM: $MEM_TOTAL total, $MEM_FREE free $"INVERSE_OFF"

# Compute values for the vertical bar graphs & Alarm tests
# CPU busy is the 100% minus the idle percent
```

```bash
# Show an alarm if the CPU limit is exceeded three times
# or if the kernel usage exceeds 50%

CPU=100-IDLE
if [ $CPU_SY -gt 50 ]; then
    alarm "Kernel bottleneck - system CPU usage $CPU_SY%"
fi

if [ $CPU -gt $CPU_LIMIT ]; then
    if [ $CPU1 -gt $CPU1_LIMIT ]; then
        if [ $CPU2 -gt $CPU2_LIMIT ]; then
            alarm "CPU bottleneck - $CPU% busy"
        fi
    fi
fi

# Signs of heavy system loads

if [ $SYS_CS -gt $THRASHING ]; then
    alarm "System Thrashing - $SYS_CS context switches"
elif [ $PROC_W -gt 0 ]; then
    alarm "Swapped out $PROC_W processes"
fi

# Show an alarm if the net limit is exceeded three times

if [ $NET -gt $NET_LIMIT ]; then
    if [ $NET1 -gt $NET1_LIMIT ]; then
        if [ $NET2 -gt $NET2_LIMIT ]; then
            alarm "Network bottleneck - $NET ms"
        fi
    fi
fi

if [ $SYS_SI -gt $DISK_LIMIT ]; then
    alarm "Disk bottleneck - $SYS_SI device interrupts"
fi

# Physical memory is used memory / total memory
# Show an alarm if the limit is exceeded three times

MEM=100*\(MEM_TOTAL-MEM_FREE\)/MEM_TOTAL
if [ $MEM2 -gt $MEM2_LIMIT ]; then
    if [ $MEM1 -gt $MEM1_LIMIT ]; then
        if [ $MEM -gt $MEM_LIMIT ]; then
            alarm "virtual memory shortage - memory $MEM% in use"
        fi
    fi
fi
```

```bash
# Check temp directory space

TMP=`$df 2>&1`
if [ $? -ne 0 ] ; then
    alarm "`printf "%s" "$TMP" | tail -1`"
else
    TMP=`printf "%s" "$TMP" | grep "/tmp"`
    if [ -n "$TMP" ] ; then
        TMP=`printf "%s" "$TMP" | grep "100%"`
        if [ -n "$TMP" ] ; then
            alarm "$0: /tmp appears to be full"
        fi
    fi
fi

PAGE=$SYS_CS/80                              # top of Faults graph is 8000

# Draw vertical bar graphs

printf "\n"
cpu_graph "$CPU"
mem_graph "$MEM"
page_graph "$PAGE"
net_graph "`$((10*NET))`"                # 100% = 10 nanoseconds

printf "%s\n" "$DOWN10"
printf "%s\n" "CPU Used        Memory            Thrashing (CS)"
printf "%s\n" "    LAN Traffic"

DSK=$SYS_SI/DISK_GRAPH_TOP
disk_graph "$DSK"

printf "%s\n" "$DOWN10"
printf "%s\n" "Disk Traffic"

# Nothing new logged?  Then show all is well in log
# ($SYSTEM_OK is cleared in the alarm function)

[ -n "$SYSTEM_OK" ] && alarm "System OK"
```

```bash
# Show alarm history, but only if it has changed

if [ -n "$LOG_UPDATED" ] ; then
    printf "%s\n"  "$LOG1""$CEOL"
    printf "%s\n"  "$LOG2""$CEOL"
    printf "%s\n"  "$LOG3""$CEOL"
    printf "%s\n"  "$LOG4""$CEOL"
    printf "%s\n"  "$LOG5""$CEOL"
    printf "%s\n"  "$LOG6""$CEOL"
    printf "%s\n"  "$LOG7""$CEOL"
    printf "%s\n"  "$LOG8""$CEOL"
fi

# sit quietly for a while before generating next screen

nice sleep $SLEEP

done

exit 0
```

# 附录 B

## Bash 内置命令摘要

- **alias**——管理别名。
- **bg**——在后台启动挂起的任务。
- **bind**——管理键盘映射。
- **builtin**——运行内置 Shell 命令。
- **cd**——更改目录。
- **command**——运行 Linux 命令。
- **declare**——声明变量。
- **dirs**——显示 `cd` 目录堆栈。
- **disown**——停止监控后台任务。
- **echo**——打印到标准输出。
- **enable**——启用或禁用内置 Shell 命令。
- **eval**——执行命令，但首先执行 Shell 替换/展开。
- **exec**——离开 Shell 并切换到新程序。
- **exit**——退出 Bash 并返回状态码。
- **export**——管理导出变量。
- **false**——返回非零状态码。
- **fc**——查找并编辑命令历史行。
- **fg**——在前台运行挂起的任务。
- **function**——声明函数。
- **hash**——管理 Bash 命令表。
- **history**——管理命令历史。
- **jobs**——管理后台任务。
- **let**——求值表达式。
- **local**——声明局部函数变量。
- **logout**——在交互模式下退出 Shell。
- **popd**——丢弃 `cd` 目录堆栈条目。




## Bash 选项

### 表 C.1 shopt 选项

| 选项 | 默认值 | 描述 |
| :------- | :------- | :------- |
| `-o allelexport` | 关闭 | 所有被修改或创建的变量都会被导出。 |
| `-o braceexpand` | 开启 | Shell 执行花括号展开。 |
| `cdable_vars` | 关闭 | 内置的 `cd` 命令假设未识别的目录是包含目录路径的变量。 |
| `cdspell` | 关闭 | 检查 `cd` 路径中目录部分的拼写错误。 |
| `checkhash` | 关闭 | 在尝试路径搜索以查找要运行的命令之前，验证命令查找表中的命令是否仍然存在。 |
| `checkwinsize` | 关闭 | 确定在每个命令执行后显示窗口是否已调整大小。 |
| `cmdhist` | 开启 | 允许多行历史命令编辑。 |
| `dotglob` | 关闭 | 允许在路径名展开中包含 `.files`。 |
| `-o emacs` | 关闭 | 使用 Emacs 风格的行编辑键。 |
| `-o errexit` | 关闭 | 如果命令以非零状态退出，则立即退出。 |
| `execfail` | 关闭 | 当内置的 `exec` 命令无法执行某个命令时，脚本会失败。 |
| `expand_aliases` | 开启 | 允许使用别名。 |
| `extglob` | 关闭 | 为文件名启用扩展模式匹配功能。 |
| `-o hashall` | 开启 | 记住命令查找时的位置。 |
| `histappend` | 关闭 | 命令历史追加到历史文件，而不是覆盖它。 |
| `histredit` | 关闭 | 允许用户编辑失败的历史替换。 |
| `-o histexpand` | 开启 | 启用 `!` 风格的历史替换。 |
| `-o history` | 开启 | 启用命令历史。 |
| `histverify` | 关闭 | 历史替换可以被进一步编辑。 |
| `hostcomplete` | 开启 | 完成包含 `@` 的主机名。 |
| `huponexit` | 关闭 | 当此脚本退出时，向所有仍在运行的作业发送挂起信号。 |
| `-o ignoreeof` | 关闭 | 确保交互式 shell 在读取文件结束时不会退出。 |
| `interactive-comments` | 开启 | 允许在交互式命令中出现注释。 |
| `-o keyword` | 关闭 | 所有赋值参数都被放入命令的环境中，而不仅仅是那些位于命令名称之前的参数。 |
| `lithist` | 关闭 | 包含多个命令的行会被拆分，并作为单独的命令存储在命令历史中。 |
| `mailwarn` | 关闭 | 当有新材料到达且处于 shell 提示符时，通知用户。 |
| `-o monitor` | 开启 | 启用作业控制。 |
| `no_empty_cmd_completion` | 关闭 | 不允许在空行上进行命令补全。 |
| `nocaseglob` | 关闭 | 在模式匹配文件名时忽略大小写。 |
| `-o noclobber` | 关闭 | 如果已设置，则不允许通过输出重定向覆盖现有的常规文件。 |
| `-o noexec` | 关闭 | 读取命令但不执行它们。 |
| `-o noglob` | 关闭 | 禁用文件名生成（`*globbing*`）。 |
| `-o notify` | 关闭 | 立即通知用户作业终止。 |
| `-o nounset` | 关闭 | 在替换时，将未设置的变量视为错误。 |
| `nullglob` | 关闭 | 不匹配任何内容的模式返回空字符串，而不是其本身。 |
| `-o onecmd` | 关闭 | 读取并执行一条命令后退出。 |
| `-o physical` | 关闭 | 如果已设置，在执行更改当前目录的命令（如 `cd`）时，不跟随符号链接。 |
| `-o posix` | 关闭 | 符合 POSIX 1003.2 标准。 |
| `-o privileged` | 关闭 | 每当实际用户 ID 和有效用户 ID 不匹配时开启。禁用处理 `*$ENV*` 文件和导入 shell 函数。关闭此选项会导致有效 uid 和 gid 被设置为实际 uid 和 gid。 |
| `progcomp` | 开启 | 启用可编程补全。 |
| `shoptvars` | 开启 | 处理提示字符串中的变量和参数。 |
| `restricted_shell` | - | 如果 shell 是受限 shell，则为开启状态。此选项是只读的。 |
| `shift_verbose` | 关闭 | 当没有剩余参数可 shift 时返回错误。 |
| `sourcepath` | 开启 | 使用 `PATH` 变量查找 `.` 或 `source` 命令的脚本。 |
| `-o verbose` | 关闭 | 在读取时打印 shell 输入行。 |
| `-o vi` | 关闭 | 使用 vi 风格的行编辑键。 |
| `xpg_echo` | 关闭 | 内置命令 `echo` 默认处理转义序列。 |
| `-o xtrace` | 关闭 | 在执行时打印命令及其参数。 |

### 表 C.2 Bash set 开关

| 开关 | 描述 |
| :--- | :--- |
| `-a` | 等同于 `allexport` |
| `-b` | 等同于 `notify` |
| `-e` | 等同于 `errexit` |
| `-f` | 等同于 `noglob` |
| `-h` | 等同于 `hashall` |
| `-I` | 强制 shell 为“交互式”。交互式 shell 在启动时始终读取 `~/.bashrc` |
| `-k` | 等同于 `keyword` |
| `-m` | 等同于 `monitor` |
| `-n` | 等同于 `noexec` |
| `-o option` | 修改 shopt 选项（等同于 `shopt -o`） |
| `-p` | 等同于 `privileged` |
| `-t` | 等同于 `oncmd` |
| `-u` | 等同于 `nounset` |
| `-v` | 等同于 `verbose` |
| `-x` | 等同于 `xtrace` |
| `-B` | 等同于 `braceexpand` |
| `-C` | 等同于 `noclobber` |
| `-H` | 等同于 `histexpand` |
| `-P` | 等同于 `physical` |

## 错误代码

以下列表包含错误代码的 C 语言缩写形式、错误代码的数值值以及对该错误的简短描述。

| **C 名称** | **数值** | **描述** |
| --- | --- | --- |
| `EPERM` | 1 | 操作不被允许 |
| `ENOENT` | 2 | 没有那个文件或目录 |
| `ESRCH` | 3 | 没有那个进程 |
| `EINTR` | 4 | 系统调用被中断 |
| `EIO` | 5 | I/O 错误 |
| `ENXIO` | 6 | 没有那个设备或地址 |
| `E2BIG` | 7 | 参数列表过长 |
| `ENOEXEC` | 8 | 执行格式错误 |
| `EBADF` | 9 | 无效的文件描述符 |
| `ECHILD` | 10 | 没有子进程 |
| `EAGAIN` | 11 | 请再试一次 |
| `ENOMEM` | 12 | 内存不足 |
| `EACCES` | 13 | 权限被拒绝 |
| `EFAULT` | 14 | 无效的地址 |
| `ENOTBLK` | 15 | 需要块设备 |
| `EBUSY` | 16 | 设备或资源忙 |
| `EEXIST` | 17 | 文件已存在 |
| `EXDEV` | 18 | 跨设备链接 |
| `ENODEV` | 19 | 没有那个设备 |
| `ENOTDIR` | 20 | 不是目录 |
| `EISDIR` | 21 | 是一个目录 |
| `EINVAL` | 22 | 无效的参数 |
| `ENFILE` | 23 | 文件表溢出 |
| `EMFILE` | 24 | 打开的文件过多 |
| `ENOTTY` | 25 | 不是 tty 设备 |
| `ETXTBSY` | 26 | 文本文件忙 |
| `EFBIG` | 27 | 文件太大 |
| `ENOSPC` | 28 | 设备上没有剩余空间 |
| `ESPIPE` | 29 | 非法的 seek 操作 |
| `EROFS` | 30 | 只读文件系统 |
| `EMLINK` | 31 | 链接过多 |
| `EPIPE` | 32 | 管道破裂 |
| `EDOM` | 33 | 数学参数超出定义域 |
| `ERANGE` | 34 | 数学结果无法表示 |
| `EDEADLK` | 35 | 资源死锁可能会发生 |
| `ENAMETOOLONG` | 36 | 文件名太长 |
| `ENOLCK` | 37 | 没有可用的记录锁 |
| `ENOSYS` | 38 | 功能未实现 |
| `ENOTEMPTY` | 39 | 目录不为空 |
| `ELOOP` | 40 | 遇到了过多的符号链接 |
| `EMOUNTDBLOCK` | - | 等同于 `EAGAIN` |
| `ENMSG` | 42 | 没有所需类型的消息 |
| `EIDRM` | 43 | 标识符已被移除 |
| `ECHRNG` | 44 | 通道号超出范围 |
| `EL2NSYNC` | 45 | 第 2 级未同步 |
| `EL3HLT` | 46 | 第 3 级已停止 |
| `EL3RST` | 47 | 第 3 级已重置 |
| `ELNRNG` | 48 | 链路号超出范围 |
| `EUNATCH` | 49 | 协议驱动未附加 |
| `ENOCSI` | 50 | 没有可用的 CSI 结构 |
| `EL2HKT` | 51 | 第 2 级已停止 |
| `EBADE` | 52 | 无效交换 |
| `EBAAD` | 53 | 无效的请求描述符 |
| `EXFULL` | 54 | 交换已满 |
| `ENOANO` | 55 | 没有 anode |
| `EBADRPC` | 56 | 无效的请求代码 |
| `EBADSLT` | 57 | 无效的槽位 |
| `EDEADLOCK` | - | 等同于 `EDEADLK` |
| `EBFONT` | 59 | 无效的字体文件格式 |
| `ENOSTR` | 60 | 设备不是流 |
| `ENODATA` | 61 | 没有可用数据 |




## C 名称 | 值 | 描述

| C 名称 | 值 | 描述 |
|:-------|:-----:|:------------|
| ETIME | 62 | 计时器过期 |
| ENOSR | 63 | 流资源耗尽 |
| ENONET | 64 | 机器不在网络上 |
| ENOPKG | 65 | 未安装包 |
| EREMOTE | 66 | 对象是远程的 |
| ENOLINK | 67 | 链路已断开 |
| EADV | 68 | 通告错误 |
| ESRMNT | 69 | 同步挂载错误 |
| ECOMM | 70 | 发送时发生通信错误 |
| EPROTO | 71 | 协议错误 |
| EMULTIHOP | 72 | 尝试多跳 |
| EDOTDOT | 73 | RFS 特定错误 |
| EBADMSG | 74 | 不是数据消息 |
| EOVERFLOW | 75 | 值对于定义的数据类型而言太大 |
| ENOTUNIQ | 76 | 名称在网络上不唯一 |
| EBADFD | 77 | 文件描述符状态不佳 |
| EREMCHG | 78 | 远程地址已更改 |
| ELIBACC | 79 | 无法访问所需的共享库 |
| ELIBBAD | 80 | 访问了损坏的共享库 |
| ELIBSCN | 81 | .out 中的 .lib 部分已损坏 |
| ELIBMAX | 82 | 链接了太多共享库 |
| ELIBEXEC | 83 | 无法直接执行共享库 |
| EILSEQ | 84 | 非法字节序列 |
| ERESTART | 85 | 被中断的系统调用应重新启动 |
| ESTRPIPE | 86 | 流管道错误 |
| EUSERS | 87 | 用户过多 |
| ENOTSOCK | 88 | 在非套接字上进行套接字操作 |
| EDESTADDRREQ | 89 | 需要目标地址 |
| EMSGSIZE | 90 | 消息太长 |
| EPROTOTYPE | 91 | 套接字的协议类型错误 |
| ENOPROTOOPT | 92 | 协议不可用 |
| EPROTONOSUPPORT | 93 | 协议不受支持 |
| ESOCKTNOSUPPORT | 94 | 套接字类型不受支持 |
| EOPNOTSUPP | 95 | 传输端点不支持此操作 |
| EPFNOSUPPORT | 96 | 协议族不受支持 |
| EAFNOSUPPORT | 97 | 协议不支持该地址族 |
| EADDRINUSE | 98 | 地址已被使用 |
| EADDRNOTAVAIL | 99 | 无法分配请求的地址 |
| ENETDOWN | 100 | 网络已关闭 |
| ENETUNREACH | 101 | 网络不可达 |
| ENETRESET | 102 | 网络因复位而断开连接 |
| ECONNABORTED | 103 | 软件导致连接中断 |
| ECONNRESET | 104 | 连接被对等方复位 |
| ENOBUFS | 105 | 没有可用的缓冲区空间 |
| EISCONN | 106 | 传输端点已连接 |
| ENOTCONN | 107 | 传输端点未连接 |
| ESHUTDOWN | 108 | 传输端点关闭后无法发送 |
| ETOOMANYREFS | 109 | 引用过多；无法拼接 |
| ETIMEDOUT | 110 | 连接超时 |
| ECONNREFUSED | 111 | 连接被拒绝 |
| EHOSTDOWN | 112 | 主机已关闭 |
| EHOSTUNREACH | 113 | 没有到主机路由 |
| EALREADY | 114 | 操作正在进行中 |
| EINPROGRESS | 115 | 操作当前正在进行中 |
| ESTALE | 116 | 过期的 NFS 文件句柄 |
| EUCLEAN | 117 | 结构需要清理 |
| ENOTNAM | 118 | 不是 XENIX 命名类型文件 |
| ENAVAIL | 119 | 没有可用的 XENIX 信号量 |
| EISNAM | 120 | 是命名类型文件 |
| EREMOTEIO | 121 | 远程 I/O 错误 |
| EDQUOT | 122 | 超过配额 |
| ENOMEDIUM | 123 | 未找到介质 |
| EILTYPEMTYPE | 124 | 介质类型错误 |

## E

## 信号

以下列表包含 C 语言中信号的简短形式、信号的数值以及该信号用途的简短描述。

| 值 | C 名称 | 描述 |
| :--- | :--- | :--- |
| 1 | SIGHUP | 连接挂断 |
| 2 | SIGINT | 中断 |
| 3 | SIGQUIT | 退出 |
| 4 | SIGILL | 非法指令（不重置） |
| 5 | SIGTRAP | 跟踪陷阱（不重置） |
| 6 | SIGABRT | 由 abort 使用 |
| 7 | SIGBUS | 总线错误 |
| 8 | SIGFPE | 浮点异常 |
| 9 | SIGKILL | 终止（无法捕获或忽略） |
| 10 | SIGUSR1 | 用户定义 |
| 11 | SIGSEGV | 段错误 |
| 12 | SIGUSR2 | 用户定义 |
| 13 | SIGPIPE | 向无人读取的管道写入 |
| 14 | SIGALRM | 闹钟 |
| 15 | SIGTERM | 终止（kill 默认值） |
| 17 | SIGCHLD | 子进程状态变更 |
| 18 | SIGCONT | 停止的进程已继续 |
| 19 | SIGSTOP | 停止（无法捕获或忽略） |
| 20 | SIGTSTP | 从 tty 请求用户停止 |
| 21 | SIGTTIN | 尝试后台 tty 读取 |
| 22 | SIGTTOU | 尝试后台 tty 写入 |
| 23 | SIGURG | I/O 通道上的紧急状况 |
| 24 | SIGXCPU | 超过 CPU 时间限制 |
| 25 | SIGXFSZ | 超过文件大小限制 |
| 26 | SIGVTALRM | 虚拟计时器过期 |
| 27 | SIGPROF | 分析计时器过期 |
| 28 | SIGWINCH | 窗口大小变更 |
| 29 | SIGIO | 输入/输出可能 |
| 30 | SIGWR | 电源故障 |
| 31 | SIGSYS | 无效的系统调用 |

## F

### ASCII 表

以下是 ASCII 代码列表、其官方名称、这些代码对应的控制台按键以及用于表示它们的特殊 HTML 或 `printf` 字符。

| 十进制 | 八进制 | 十六进制 | 名称 | 键盘 | HTML/printf 等价项 |
| :------ | :---- | :---------- | :--- | :------- | :--------------------- |
| 0 | 0 | 0 | NUL | Control-@ | - |
| 1 | 1 | 1 | SOH | Control-A | - |
| 2 | 2 | 2 | STX | Control-B | - |
| 3 | 3 | 3 | ETX | Control-C | - |
| 4 | 4 | 4 | EOT | Control-D | - |
| 5 | 5 | 5 | ENQ | Control-E | - |
| 6 | 6 | 6 | ACK | Control-F | - |
| 7 | 7 | 7 | BEL | Control-G | - |
| 8 | 10 | 8 | BS | Control-H | `\b` |
| 9 | 11 | 9 | TAB | Control-I | `\t` |
| 10 | 12 | A | LF | Control-J | `\n` |
| 11 | 13 | B | VT | Control-K | `\v` |
| 12 | 14 | C | FF | Control-L | `\f` |
| 13 | 15 | D | CR | Control-M | `\r` |
| 14 | 16 | E | SO | Control-L | - |
| 15 | 17 | F | SI | Control-M | - |
| 16 | 20 | 10 | DLE | Control-N | - |
| 17 | 21 | 11 | DC1 | Control-O | - |
| 18 | 22 | 12 | DC2 | Control-P | - |
| 19 | 23 | 13 | DC3 | Control-Q | - |
| 20 | 24 | 14 | DC4 | Control-R | - |
| 21 | 25 | 15 | NAK | Control-S | - |
| 22 | 26 | 16 | SYN | Control-T | - |
| 23 | 27 | 17 | ETB | Control-U | - |
| 24 | 30 | 18 | CAN | Control-V | - |
| 25 | 31 | 19 | EM | Control-W | - |
| 26 | 32 | 1A | SUB | Control-X | - |
| 27 | 33 | 1B | ESC | Control-Y | - |
| 28 | 34 | 1C | FS | Control-Z | - |
| 29 | 35 | 1D | GS | - | - |
| 30 | 36 | 1E | RS | - | - |
| 31 | 37 | 1F | US | - | - |
| 32 | 40 | 20 | 空格 | 空格键 | - |
| 33 | 41 | 21 | ! | ! | - |
| 34 | 42 | 22 | " | " | &quot; |
| 35 | 43 | 23 | # | # | - |
| 36 | 44 | 24 | $ | $ | - |
| 37 | 45 | 25 | % | % | - |
| 38 | 46 | 26 | & | & | &amp; |
| 39 | 47 | 27 | ' | ' | - |
| 40 | 50 | 28 | ( | ( | - |
| 41 | 51 | 29 | ) | ) | - |
| 42 | 52 | 2A | * | * | - |
| 43 | 53 | 2B | + | + | - |
| 44 | 54 | 2C | , | , | - |
| 45 | 55 | 2D | - | - | - |
| 46 | 56 | 2E | . | . | - |
| 47 | 57 | 2F | / | / | - |
| 48 | 60 | 30 | 0 | 0 | - |
| 49 | 61 | 31 | 1 | 1 | - |
| 50 | 62 | 32 | 2 | 2 | - |
| 51 | 63 | 33 | 3 | 3 | - |
| 52 | 64 | 34 | 4 | 4 | - |
| 53 | 65 | 35 | 5 | 5 | - |
| 54 | 66 | 36 | 6 | 6 | - |
| 55 | 67 | 37 | 7 | 7 | - |
| 56 | 70 | 38 | 8 | 8 | - |
| 57 | 71 | 39 | 9 | 9 | - |
| 58 | 72 | 3A | : | : | - |
| 59 | 73 | 3B | ; | ; | - |
| 60 | 74 | 3C | < | < | &lt; |
| 61 | 75 | 3D | = | = | - |
| 62 | 76 | 3E | > | > | &gt; |
| 63 | 77 | 3F | ? | ? | - |
| 64 | 100 | 40 | @ | @ | - |
| 65 | 101 | 41 | A | A | - |
| 66 | 102 | 42 | B | B | - |
| 67 | 103 | 43 | C | C | - |
| 68 | 104 | 44 | D | D | - |
| 69 | 105 | 45 | E | E | - |
| 70 | 106 | 46 | F | F | - |
| 71 | 107 | 47 | G | G | - |
| 72 | 110 | 48 | H | H | - |
| 73 | 111 | 49 | I | I | - |
| 74 | 112 | 4A | J | J | - |
| 75 | 113 | 4B | K | K | - |
| 76 | 114 | 4C | L | L | - |
| 77 | 115 | 4D | M | M | - |
| 78 | 116 | 4E | N | N | - |
| 79 | 117 | 4F | O | O | - |
| 80 | 120 | 50 | P | P | - |
| 81 | 121 | 51 | Q | Q | - |
| 82 | 122 | 52 | R | R | - |
| 83 | 123 | 53 | S | S | - |
| 84 | 124 | 54 | T | T | - |
| 85 | 125 | 55 | U | U | - |
| 86 | 126 | 56 | V | V | - |
| 87 | 127 | 57 | W | W | - |
| 88 | 130 | 58 | X | X | - |
| 89 | 131 | 59 | Y | Y | - |
| 90 | 132 | 5A | Z | Z | - |
| 91 | 133 | 5B | [ | [ | - |
| 92 | 134 | 5C | \ | \ | - |
| 93 | 135 | 5D | ] | ] | - |
| 94 | 136 | 5E | ^ | ^ | - |
| 95 | 137 | 5F | _ | _ | - |
| 96 | 140 | 60 | ` | ` | - |
| 97 | 141 | 61 | a | a | - |





| 十进制 | 八进制 | 十六进制 | 名称 | 键盘 | HTML/printf 等价物 |
| :-----: | :---: | :-----------: | :--: | :------: | :--------------------: |
| 98 | 142 | 62 | b | b | - |
| 99 | 143 | 63 | c | c | - |
| 100 | 144 | 64 | d | d | - |
| 101 | 145 | 65 | e | e | - |
| 102 | 146 | 66 | f | f | - |
| 103 | 147 | 67 | g | g | - |
| 104 | 150 | 68 | h | h | - |
| 105 | 151 | 69 | i | i | - |
| 106 | 152 | 6A | j | j | - |
| 107 | 153 | 6B | k | k | - |
| 108 | 154 | 6C | l | l | - |
| 109 | 155 | 6D | m | m | - |
| 110 | 156 | 6E | n | n | - |
| 111 | 157 | 6F | o | o | - |
| 112 | 160 | 70 | p | p | - |
| 113 | 161 | 71 | q | q | - |
| 114 | 162 | 72 | r | r | - |
| 115 | 163 | 73 | s | s | - |
| 116 | 164 | 74 | t | t | - |
| 117 | 165 | 75 | u | u | - |
| 118 | 166 | 76 | v | v | - |
| 119 | 167 | 77 | w | w | - |
| 120 | 170 | 78 | x | x | - |
| 121 | 171 | 79 | y | y | - |
| 122 | 172 | 7A | z | z | - |
| 123 | 173 | 7B | { | { | - |
| 124 | 174 | 7C | \| | \| | - |
| 125 | 175 | 7D | } | } | - |
| 126 | 176 | 7E | ~ | ~ | - |
| 127 | 177 | 7F | DEL | Delete | - |

## 术语表

**绝对路径** 是指从根目录引导到文件的路径名。

**别名** 是命令的简短形式。

**参数** 是提供给命令的额外信息，用于改变其行为。

**数组** 在 Bash 编程中，是包含开放列表值的变量。

**归档** 是将多个文件存储到单个文件中的过程。

**属性** 是可以使用 declare 命令开启或关闭的变量选项。

**绑定** 是将特定按键与 Bash 编辑功能关联起来。

**阻塞** 是脚本在等待管道或套接字读取更多信息时，或等待信息被读取（因为管道或套接字已满）时停止执行。

**内置命令** 是 Bash 的一部分，而不是存储在磁盘外部的 Linux 命令。

**CGI** 代表通用网关接口，一种从 Web 服务器运行脚本的方法。

**命令历史** 是最近输入的commands列表。

**压缩** 是通过编码文件来减小文件大小。

**冲突** 是涉及脚本相同部分且 CVS 无法自动合并的更改。

**控制台** 是连接到系统的管理终端。

**常量** 是声明为只读属性的变量。

**cron 任务** 是供 cron 命令执行的任务列表。

**当前目录** 是文件的默认目录，在 Linux 中用 . 表示。

**CVS** 是并发版本系统，一种流行的版本控制系统。

**守护进程** 是独立于 shell 会话运行的程序，持续执行某些任务。

**悬空链接** 是指向已删除文件的符号链接。

**发行版** 是完整的 Linux 系统，通常组装在 CD-ROM 或 DVD-ROM 上。

**ext2** 是第二扩展文件系统，标准的 Linux 磁盘存储标准。

**ext3** 是第三扩展文件系统，一种使用称为“日志记录”的技术来防止因设备故障导致数据丢失的变体。

**_emacs 模式_** 涉及在交互式会话中使用类似 emacs 编辑器的按键进行命令编辑。

**环境** 是 Linux 术语，指从一个程序导出到另一个程序的变量和打开文件的集合。

**环境变量** 是 Linux 通过其环境在程序之间共享的变量。

**纪元** 是 Linux 日历的开始，即 1970 年 1 月 1 日。

**扩展** 是替换嵌入在可执行行中的变量和表达式。

**导出变量** 是将变量提供给从脚本运行的程序的过程。

**表达式** 是计算值的公式。

**FIFO**（先进先出）是命名管道。

**文件名补全** 是 Bash 在交互式会话中搜索匹配指定字符的合适文件名的过程。

**过滤器** 是接受一个命令的结果并以某种方式修改它们以提供给另一个命令或文件的命令。

**标志** 是指示给定条件的字符串变量，如果值不是空字符串。

**通配** 是 shell 使用其通配符文件名匹配约定进行的模式匹配。

**硬链接** 是与其代表的文件表现完全相同的链接。

**Here 文件** 是与 << 重定向操作符相关联的数据行。

**主目录** 是用户登录时分配的目录，在 Bash 中用 ~ 指定。

**主机名** 是用于引用网络上特定机器的计算机名称。

**索引** 是数组中项的位置。

**inode 密度** 表示每存储容量的 inode 数量。

**inode** 是 Linux 文件的唯一识别编号。

**作业控制** 是使用内置 shell 命令管理后台任务的能力。

**作业** 是从 shell 启动的后台任务。

**关键字** 是对 Bash 具有特殊含义的单词或符号。

**链接** 是指向文件的快捷方式。

**锁文件** 是指示特定条件的文件，通常表示资源或另一个文件正在使用中。

**命名管道** 是一种特殊文件，一个脚本可以读取它，而另一个脚本可以写入它。

**开源** 指以源代码形式向公众发布的软件，以便程序员可以重建或修改软件以满足其需求。

**参数** 是开关或参数。

**父目录** 是直接包含当前目录的目录，在 Linux 中用 `..` 指定。

**补丁文件** 包含用于将一组文件升级到另一组文件的更改列表。

**路径名**（或 *路径*）是描述文件位置的字符串。

**权限** 是对文件的访问权。

**PID** 是进程标识符。

**管道文件** 是命名管道。

**管道** 是由管道符号（`|`）连接的一系列命令。

**轮询** 是持续检查以查看守护进程是否有新工作要做。

**进程替换** 是通过临时管道文件重定向命令的输入或输出，以便由另一个命令读取或写入。

**常规文件** 包含可读的数据或可执行的指令，与目录或管道等文件相反。

**相对路径** 是从当前目录引导到文件的路径名。

**仓库** 是版本控制系统维护的数据库，所有主副本都保存在这里。

**根目录** 是目录层次结构中最顶层的目录，即 `/` 目录。

**健全性检查** 是脚本开头处的测试，用于验证文件和变量的存在。

**shar 文件** 是由 `shar` 命令创建的 shell 归档。

**Shell** 是运行操作系统命令的程序。

**Shell 归档** 是作为单个 shell 脚本编码的文本文件或脚本的集合。

**Shell 选项** 是启用或禁用特定 Bash 功能的标志。

**稀疏文件** 是包含大量零的文件，在 `ext2` 下不占用任何磁盘空间。

**标准错误** 是写入错误消息的默认文件。符号是 `&2`，路径是 `/dev/stderr`。

**标准输入** 是读取命令输入的默认文件。符号是 `&0`，路径是 `/dev/stdin`。

**标准输出** 是写入输出的默认文件。符号是 `&1`，路径是 `/dev/stdout`。

**状态代码** 是 0 到 255 之间的数字，指示前一个命令执行时发生的问题。

**开关**（也称为“选项”或“标志”）是由减号处理的字符，用于启用命令功能。

**符号链接** 是有时被处理为与其代表的文件不同的链接。

**文本流** 是 shell 管道中的文本文件。





**TCP/IP** 代表传输控制协议/互联网协议，是互联网的通信标准。

**Traps**（陷阱）是信号处理程序。

**UDP** 代表用户数据报协议。

**Utilities**（实用工具）是提供适用于许多应用程序的通用功能的命令，例如返回日期或统计文件中的行数。

**Version control systems**（版本控制系统）是维护数据文件、脚本和源程序主副本的程序，用于跟踪更改并在多个程序员之间共享脚本。

**vi mode**（vi 模式）是使用类似于 vi 编辑器的按键以交互方式进行命令编辑。

**Word designators**（单词指定符）是 `!` 历史回忆命令的语法，用于选择或修改特定的行项目。

**Word splitting**（单词拆分）是 Bash 将命令参数拆分为单个单词的过程。

**Words**（单词）由 shell 命令及其在引号和反斜杠被解释后的每个参数组成。

# 索引

## 符号

- `&&` 多命令，18
- `*`（星号），通配符，101
- `\`（反斜杠）代码，30-31
  - 编辑命令，40
  - printf 命令，47
- `:` 命令，24
- `:-`（默认值扩展），106
- `:=`（默认值赋值扩展），106
- `:n`（子字符串扩展），107
- `:+`（默认值覆盖扩展），107
- `:?`（变量存在性检查扩展），107
- `!`（文件名扩展），104
- `{ , }`，分组命令，122
- `-1` 开关，join 命令，195
- `-2` 开关，join 命令，195
- `-a` (--alternative) 开关，getopt 命令，154
- `-a` (—all) 开关，unexpand 命令，182
- `-a` (--append) 开关
  - man 命令，32
  - tee 命令，133, 141
  - time 命令，136, 142
- `-a` (absolutely all) 开关，ls 命令，28
- `-A` (action) 开关，compgen 命令，321, 333-334
- `-a` (all) 开关
  - jobs 命令，159
  - locale 命令，324
  - ls 命令，28
  - type 命令，62
- `-a` (array) 属性，74
- `-A` (concatenate) 开关，tar 命令，225
- `-A` (label) 开关，merge 命令，197
- `-a` 开关，21, 91
- `--amin` 开关，find 命令，212
- `--anewer` 开关，find 命令，212
- `--appendsork` 开关，setterm 命令，238
- `--atime` 开关，find 命令，212
- `-b` (—binary) 开关，md5sum 命令，180
- `-b` (bytes) 开关，192, 195
- `-b` (backup) 开关，mv 命令，34
- `-b` (batch) 开关，shuf 命令，179
- `-b` (blank) 开关，sort 命令，216
- `-b` (brief) 开关，file 命令，172
- `-b s` (—byte=$5) 开关，split 命令，180
- `-b S` (—suffix=$5) 开关，split 命令，181
- `-b` 开关，free 命令，326
- `--background` 开关，setterm 命令，237
- `-c` (—bytes) 开关，190-191
- `-c` (—bytes=n) 开关，tail 命令，190
- `-c` (—changes) 开关，chown 命令，270
- `-c` (—characters) 开关，cut 命令，192
- `-c` (—check) 开关，md5sum 命令，180
- `-c` (—complement) 开关，tr 命令，218
- `-c` (—count) 开关，grep 命令，210
- `-c` (—create) 开关，tar 命令，224
- `-c` (check only) 开关，sort 命令，217
- `-C` (command) 开关，compgen 命令，322
- `-C` (compress) 开关，stpf 命令，179
- `-C s` (—line-byte=$5) 开关，split 命令，180
- `-c` 开关，21-23, 320
- `--calendar` 开关，dialog 命令，244
- `--caps` 开关，setlog 命令，236
- `-cmni` 开关，find 命令，212
- `--newer` 开关，find 命令，212
- `-ctime` 开关，find 命令，212
- `--curtime` 开关，setterm 命令，238
- `-d` (compare) 开关，tar 命令，225
- `-d` (delete) 开关，37, 217
- `-d` (—delimiter) 开关，191-193
- `-d` (directory) 开关，33, 183
- `-d` (phone directory) 开关，sort 命令，216
- `-d` 开关，20, 63, 320
- `-D` 开关，236, 278
- `-dump` 开关，lynx，295
- `-e` (escape) 开关，echo 命令，319
- `-e` 开关，58, 164
- `-E` 开关，echo 命令，320
- `-exec` 开关，find 命令，213
- `-f` (--fields) 开关，cut 命令，191
- `-f` (--quiet) 开关，chown 命令，270
- `-f` (file) 开关，file 命令，172
- `-f` (fold character cases together) 开关，sort 命令，215
- `-f` (force) 命令，删除文件，172~173
- `-f` (force) 开关，33~34, 173~174
- `-f` (function) 命令，export 命令，264
- `-F` (function) 开关，265, 322
- `-f F` (--file F) 开关，tar 命令，224
- `-f P` (--prefix=P) 开关，csplit 命令，181
- `-f` 开关，62~6
- `-F` 开关
  - ls 命令，28
  - setcls 命令，236
- `-foreground` 开关，setterm 命令，237
- `-g` (general number) 开关，sort 命令，216
- `-g` (--group) 开关，id 命令，269
- `-G` (--group) 开关，id 命令，269
- `-g` 开关，164
- `-G` 开关，compgen 命令，322
- `-h` (SIGHUP) 开关，disown 命令，160
- `-hbc0r` 开关，setterm 命令，237
- `-I` (--bzip) 开关，tar 命令，224
- `-i` (--ignore-case) 开关
  - grep 命令，209
  - join 命令，196
- `-i` (--ignore-interrupts) 开关，tee 命令，133, 141
- `-i` (--initial) 开关，expand 命令，182
- `-i` (ignore unprintable) 开关，sort 命令，216
- `-I` (integer) 属性，73
- `-i` (interactive) 开关，33~34
- `-i` (not interactive) 开关，FTP 命令，177
- `-i` 开关，file 命令，172
- `-inversescreen` 开关，setterm 命令，237~238
- `-k` (--krp-files) 开关，csplit 命令，181
- `-k` (key) 开关，sort 命令，215
- `-k` (开关)，man 命令，32
- `-l` (--lines) 开关，wc 命令，191
- `-l` (--list) 开关，psql 命令，313
- `-l` (--longtopions) 开关，getopt 命令，152
- `-L` (--max-line-length) 开关，wc 命令，191
- `-L` (label) 开关，merge 命令，197
- `-l` (link) 开关，cp 命令，34
- `-l` (list) 开关
  - bind 命令，40
  - crontab 命令，254
  - fc 命令，327
  - hash 命令，37
  - pwd 命令，21
  - trap 命令，161
- `-L` (long) 开关，jobs 命令，158
- `-s s` (--line=s) 开关，split 命令，180
- `-L` 开关，172, 236
- `-linewrap` 开关，setterm 命令，238
- `-ls` 开关，find 命令，213
- `-lu` 开关，ps 命令，165
- `-m` (keemap) 开关，bind 命令，40
- `-m` (modern) 开关，mkdir 命令，32
- `-M` (months) 开关，sort 命令，216
- `-mmin` 开关，find 命令，212
- `-mtime` 开关，find 命令，212
- `-n` (--line-number) 开关，grep 命令，209
- `-n` (--name) 开关，151, 269
- `-n` (new status) 开关，jobs 命令，159
- `-n` (no auto-login) 开关，FTP 命令，177
- `-n` (no change) 开关，23
- `-n` (no execution) 开关，125
- `-n` (no line numbers) 开关，fc 命令，327
- `-n` (no new line) 开关，echo 命令，319
- `-n` (not zero length) 开关，92
- `-n` (number) 开关，date 命令，320
- `-n` (number of characters) 开关，read 命令，58
- `-n` (numeric) 开关，sort 命令，216
- `-N` (rotate Nth) 开关，23
- `-N` (view Nth) 开关，23
- `-n D` (-(digits=D)) 开关，csplit 命令，181
- `-n I` (-(lines=n)) 开关，head 命令，189
- `-n` 开关，21, 63
- `-N` 开关，popd 命令，23
- `-name` 开关，find 命令，211
- `-name “*.txt” -type f` 开关，find 命令，211
- `-newer` 开关，find 命令，212
- `-num` 开关，setleds 命令，236
- `-o` (option) 开关
  - complete 命令，323
  - tesc 命令，109
- `-o` (output) 开关
  - join 命令，196
  - time 命令，136, 142
- `-o errexit` 调试选项，125, 143
- `-o nounset` 调试选项，126, 143
- `-o` 开关，21, 91
- `-o xtrace` 调试选项，126-127, 143
- `-ok` 开关，find 命令，213
- `-p` (-portability) 开关
  - patchck 命令，171
  - time 命令，136, 142
- `-P` (parents) 开关
  - cp 命令，34
  - mkdir 命令，32-33
  - rmdir 命令，33
- `-p` (path) 开关
  - hash 命令，37
  - type 命令，62
- `-p` (PID) 开关
  - jobs 命令，159
  - renice 命令，164
- `-p` (print) 属性，74
- `-p` (print) 开关
  - complete 命令，323
  - find 命令，213
  - merge 命令，197
  - trap 命令，162
- `-P` 开关，23
  - bind 命令，39
  - command 命令，62
  - enable 命令，63
  - history 命令，20
  - pwd 命令，21
  - readonly 命令，265
  - shopt 命令，64
  - umask 命令，274
- `-p` 开关，62, 323
- `-printf` 开关，find 命令，214, 227-228
- `-q` (-quiet) 开关
  - csplit 命令，181
  - getopt 命令，154
  - merge 命令，197
  - mktexnp 命令，183
- `-Q` (-quiet-output) 开关，getopt 命令，154
- `-q` (query) 开关，bind 命令，40
- `-q` 开关，28, 164
- `-r` (-real) 开关，id 命令，269
- `-r` (raw input) 开关，read 命令，58
- `-r` (read-only) 属性，74
- `-r` (recursive) 开关，rm 命令，33
- `-R` (recursive) 开关，34, 270
- `-r` (remove) 开关
  - bind 命令，41
  - complete 命令，323
  - hash 命令，37
- `-r` (reverse) 开关
  - fc 命令，327
  - sort 命令，215
- `-r` (running) 开关，jobs 命令，159
- `-r` 开关，history 命令，21
- `-repeat` 开关，setterm 命令，238
- `-reset` 开关，setterm 命令，237
- `-s` (-(only-delimited)) 开关，cut 命令，192
- `-s` (-(serial)) 开关，paste 命令，194
- `-s` (-(silent)) 开关，expr 命令，181
- `-s` (-(spaces)) 开关，fold 命令，195





# 索引

## -s
- (--squeeze-repeats) 选项，tr 命令，218
- (all) 选项，help 命令，31
- (set) 选项，shopt 命令，64
- (stopped) 选项，jobs 命令，159
- (substitute) 选项，fc 命令，327
- (symbolic-link) 选项，cp 命令，34
- 选项
  - bind 命令，42
  - columns 命令，194
  - enable 命令，63
  - history 命令，21
  - wipe 命令，278
- -S 选项
  - compgen 命令，323
  - umask 命令，273
- --scroll 选项，sedcols 命令，236
- --size 选项，find 命令，212
- --source 选项，lync，294-295

## -t
- (--truncate-set1) 选项，tr 命令，218
- (table) 选项，hash 命令，37
- (terse) 选项，stat 命令，175
- (timeout) 选项，read 命令，58
- (type) 选项，type 命令，62
- n 选项，expand 命令，182
- 选项
  - columns 命令，194
  - free 命令，326
  - host 命令，282
  - join 命令，195
  - sort 命令，215
- -type f 选项，find 命令，211
- -type 选项，find 命令，211

## -u
- (--shell) 选项，getopt 命令，154
- (--user) 选项，id 命令，269
- (unbind) 选项，bind 命令，41
- (unset) 选项，shopt 命令，64
- (update) 选项，34
- 选项，renice 命令，164
- -ulcor 选项，setterm 命令，237

## -v
- (--invert-match) 选项，grep 命令，209
- (-verbose) 选项
  - chown 命令，270
  - FTP 命令，177
  - sftp 命令，179
  - tar 命令，224-225
  - time 命令，136, 142
  - wget 命令，177
- (variables) 选项，bind 命令，41
- 选项，23
  - command 命令，62
  - host 命令，282
  - join 命令，196
  - killall 命令，164

## -w
- (--width=n) 选项，fold 命令，195
- (--words) 选项，wc 命令，191
- -W (words) 选项，compgen 命令，322
- 选项，history 命令，21

## -X
- (exclude) 选项，compgen 命令，322

## -x
- (execute) 选项，jobs 命令，158
- (export) 选项，declare 命令，76
- 选项，columns 命令，194

## -Z
- (--compress) 选项，tar 命令，224
- (--idle-empty-files) 选项，csplit 命令，181

## -z
- (--gzip) 选项，tar 命令，224
- (compressed) 选项，file 命令，172
- (zero length) 选项，92
- 选项，wipe 命令，278

## --
- all 选项，du 命令，325
- append-output 选项，wget 命令，177
- blocksize=B bytes 选项，du 命令，325
- bytes 选项，du 命令，325
- checklist 选项，dialog 命令，240
- classify 选项，ls 命令，28
- color 选项，ls 命令，28
- command sqlcmd 选项，psql 命令，314
- count-links 选项，du 命令，325
- duantle dB 选项，psql 命令，314
- defaulthost 选项，dialog 命令，240
- delete 选项，tar 命令，225
- dereference 选项，chown 命令，270
- dereference-args 选项，du 命令，325
- exclude-from=f 选项，du 命令，325
- exclude=f 选项，du 命令，325
- exec=sqcmd 选项，mysql 命令，316
- extract 选项，tar 命令，224
- file 选项，psql 命令，314
- fixed-strings 选项，grep 命令，208
- from 选项，chown 命令，270
- fselect 选项，dialog 命令，241
- gauga 选项，dialog 命令，242–243
- glob 选项，wget 命令，177
- glob=on 选项，wget 命令，177
- hide-control-chars 选项，ls 命令，28
- human-readable 选项，du 命令，324
- ignore-fail-on-non-empty 选项，rmdir 命令，33
- infobox 选项，dialog 命令，243
- init-file 选项，资源文件，44
- inputbox 选项，dialog 命令，243
- keycodes 选项，showkey 命令，235
- kilobytes 选项，du 命令，325
- link 选项，cp (copy) 命令，174
- list 选项，tar 命令，225
- login 选项，配置文件，43
- max-depth=n 选项，du 命令，325
- megabytes 选项，du 命令，325
- menu 选项，dialog 命令，243
- mirror 选项，wget 命令，177
- msgraph 选项，dialog 命令，243
- no-list 选项，lynx，295
- nofile 选项，配置文件，44
- nore 选项，资源文件，44
- numeric-uid-gid ls 选项，267
- one-file-system 选项，du 命令，325
- output frame 选项，psql 命令，316
- output-delimiter 选项，cut 命令，192
- password=pwd 选项，mysql 命令，316
- passwordbox 选项，dialog 命令，243
- quiet 选项，wget 命令，177
- radiolist 选项，dialog 命令，243
- rcfile 选项，资源文件，44
- reference 选项，chown 命令，270
- scancodes 选项，showkey 命令，235
- separate-dirs 选项，du 命令，325
- server-response 选项，wget 命令，177
- si 选项，du 命令，325
- status 选项，md5sum 命令，180
- summarize 选项，du 命令，324
- tabs 选项，expand 命令，182
- tabs=n 选项，unexpand 命令，182
- tailbox 选项，dialog 命令，243
- textbox 选项，dialog 命令，244
- textboxg 选项，dialog 命令，244
- timebox 选项，dialog 命令，244
- total 选项，du 命令，325
- update 选项，tar 命令，225
- use-compress-program 选项，tar 命令，224
- user username 选项，psql 命令，313
- user=username 选项，mysql 命令，316
- warn 选项，md5sum 命令，180
- yesno 选项，dialog 命令，240

## $$ (双美元符号)
- 函数，80
- 替换，80
- 临时文件，创建，182

## $
- (美元符号) 展开
- $' (本地化翻译)，105
- $ (ANSI C 转义展开)，105, 113–114
- % (子字符串移除)，107
- %% (子字符串移除)，107
- (...) (算术表达式替换)，109
- (...) (算术结果替换)，109
- // (子字符串替换)，108
- :- (默认值展开)，106
- := (默认值赋值展开)，106
- :n (子字符串)，107
- :+ (默认值覆盖展开)，107
- ? (变量扩展检查展开)，107
- $' (ANSI C 转义展开)，105, 113–114

## +
- $* (本地化翻译展开)，105
- $_.($dollar sign, underscore) 选项，148
- $AUTHORS CVS 关键字，130
- $Date$ CVS 关键字，130
- $Header$ CVS 关键字，130
- $Id$ CVS 关键字，130
- $Locker$ CVS 关键字，130
- $Log$ CVS 关键字，130
- $Name$ CVS 关键字，130
- $RCSfile$ CVS 关键字，130
- $Revision$ CVS 关键字，130
- $Source$ CVS 关键字，130
- $State$ CVS 关键字，130
- $ = (行号) 命令，223

## !
- (感叹号)，浏览命令历史，19
- 历史调用命令，327-328, 335
- !! (双感叹号)，重复命令，19
- !# (感叹号，井号)，重复命令，19
- !* (变量名匹配展开)，106
- !? (感叹号，问号)，搜索命令历史，21

## <
- > 文件，打开，188
- 运算符，59
- << 运算符，59

## >
- 运算符，59

## -
- (减号)，当前目录，22

## (
- ) (括号)，let 命令，98
- (( )) (双括号)
  - 嵌入式 let 命令，121-122
  - let 命令，99
- (.( )) (命令结果替换展开)，109
- ({,}) (算术表达式替换展开)，109

## %
- (子字符串移除展开)，107
- %% (子字符串移除展开)，107

## .
- (当前目录)，22
- (source) 命令，运行脚本，251

## ..
- (父目录)，22

## +N
- 选项，pop 命令，23

## #
- (子字符串移除展开)，107
- ## (子字符串移除展开)，106

## ?
- (问号) 通配符，101
- (问号) 条件表达式运算符，let 命令，98

## "
- " (双引号)，单词拆分，70-73
- “” (引号)
  - 通配符，101
  - 单词拆分，70-73

## ;
- (分号)，多个命令，18

## /
- / (子字符串替换展开)，108

## /dev
- 目录，11
- /dev/dsp 设备文件，12
- /dev/fd0 设备文件，12
- /dev/hda1 设备文件，12
- /dev/null 设备文件，11
- /dev/sda1 设备文件，12
- /dev/stderr 文件，61
- /dev/stdin 文件，61
- /dev/stdout 文件，60
- /dev/tty 设备文件，12
- /dev/tty 文件，60-61
- /dev/zero 设备文件，11

## /etc
- /etc/profile 文件，43

## [
- ] (方括号)
  - 数组，赋值，75
  - 通配符，101
  - test 命令，91

## ~
- (波浪号)
  - 当前目录，22
  - 变量，88
- ~/.bashrc (Bash 资源) 脚本，44

## _
- _ETC_PROFILE 变量，85

## ^
- (向上箭头) 快速替换历史命令，21
- ^? 键，16
- ^C 键，16
- ^Q 键，17
- ^R 键，17
- ^S 键，17
- ^W 键，17
- ^X 键，16
- ^Z 键，17

## |
- (竖线)，通配符，102
- || (双竖线)，多个命令，18




## 数字

- 403 禁止访问错误消息，286
- 404 未找到错误消息，286
- 500 内部服务器错误消息，286
- -a (--alternative) 开关，getopt 命令，154
- -a (--all) 开关，unexpand 命令，182
- -a (--append) 开关
  - man 命令，32
  - tee 命令，133, 141
  - time 命令，136, 142
- -a (绝对所有) 开关，ls 命令，28
- -aA (--action) 开关，compgen 命令，321, 333-334
- -a (所有) 开关
  - jobs 命令，159
  - locale 命令，324
  - ls 命令，28
  - type 命令，62
- a (追加) 命令，向行中插入文本，221
- -a (--array) 属性，74
- -A (--concatenate) 开关，tar 命令，225
- -A (--label) 开关，merge 命令，197
- -a 开关
  - history 命令，21
  - versus 非运算符，91
- 绝对路径，10
- 访问权限数字（文件），268
- 访问权限（文件），270-274
- 按访问时间查找文件，212
- 访问
  - 数组，75
  - 命令历史中的命令行，20
- 按账号编号排序文件，217
- add 命令，131
- 添加
  - 命令历史中的命令行，21
  - 将目录添加到存储库，131
  - 将文件添加到存储库目录，131
  - 项目
    - 到关联数组，305
    - 到二叉树，312
    - 到哈希表，308
  - 将行添加到文件，192, 194
- add_hash 函数，哈希表，308
- add_table 函数，关联数组，305
- add_tree 函数，二叉树，312
- alias 命令，36
- 别名，36, 99
- -all 开关，du 命令，325
- -amin 开关，find 命令，212
- -anewer 开关，find 命令，212
- ANSI C 转义扩展 ($?)，105, 113-114
- -append-output 开关，wget 命令，177
- 追加命令历史会话历史，21
- 应用补丁文件，140
- -appcursorkeys 开关，setterm 命令，238
- 归档文件，223-224
- 参数
  - date 命令，14
  - 位置参数，146-147
- 算术表达式替换扩展
  - ($(...))，109
- 算术表达式
  - let 命令，93-95, 99-100
  - 运算符，94-95
- 算术运算符，94-95
- 算术测试，100-101
- 数组属性，76
- 数组
  - 访问，75
  - 关联
    - 添加项目，305
    - add_table 函数，305
    - 创建，302-305
    - 查找项目，302-305
    - 哈希表，309
    - ITEM 变量，302
    - 键，301
    - lookup_table 函数，305
    - NEXTITEM 变量，302
    - 搜索键，305
  - 创建，74

## B

- -b (--binary) 开关，md5sum 命令，180
- -b (--bytes) 开关
  - cut 命令，192
  - fold 命令，195
- -b (备份) 开关，mv 命令，34
- -b (批处理) 开关，sfsp 命令，179
- -b (空格) 开关，sort 命令，216
- -b (简略) 开关，file 命令，172
- -b s (--byte=s) 开关，split 命令，180
- -b S (--suffix=S) 开关，caps split 命令，181
- -b 开关，free 命令，326
- 背景文本对话框，setterm 命令，237
- 后台任务。*参见 jobs*
- 创建背景文本对话框，244
- 反斜杠 (\) 代码，30-31
  - 编辑命令，40
  - printf 命令，47
- 备份文件，命名，174-176
- basename 命令，170
- BASH 变量，69, 82
- BASH_VERSION 变量，82
- BASH_ENV 变量，69, 82
- BASH_VERSION 变量，69, 82
- 二叉树
  - add_tree 函数，312
  - Bash 数组，存储，309-312
  - 退化树，309
  - dump_tree 函数，312-313
  - 项目
    - 添加，312
    - 显示，312-313
    - 排序，313
  - lookup_tree 函数，312
  - 根节点，309
  - sort 命令，313
- bind 命令开关，39-42
  - 绑定，16
    - 更改，17
    - control-b，15
    - control-f，15
    - control-n，15
    - control-p，15
    - 创建，41
    - 删除，41
    - emacs 编辑模式，15
- 按位运算符（逻辑表达式），96-97
- 索引，74
  - 列表，读入，76
  - PIPESTATUS，117
  - 存储
    - 二叉树，309-312
    - 哈希表，306-308
  - 值，分配/删除，75-76
- 箭头键，导航命令，15
- ASCII 代码，列表，367-370
- ASCII 模式（控制台输入模式），235
- 技术支持询问表单，294
- 分配
  - 绑定，41
  - 命令结果到变量，18, 69
  - 值
    - 到数组，75-76
    - 到变量，68
  - 变量，17, 98
- 关联数组
  - 添加项目，305
  - add_table 函数，305
  - 创建，302-305
  - 查找项目，302-305
  - 哈希表，309
  - ITEM 变量，302
  - 键，301, 305
  - lookup_table 函数，305
  - NEXTITEM 变量，302
- 星号 (*)，通配符匹配，101
- -a 开关，find 命令，212
- 属性（变量）
  - -a，74
  - 数组，76
  - 显示，74
  - -I，73
  - 整型变量，73-74
  - Linux，77
  - -p，74
  - -r，74
  - 开启/关闭，73
- auto_resume 变量，82

- 阻塞方法（守护程序脚本），259
- --blocksize=b 字节 开关，du 命令，325
- break 命令，120–121
- 拆分长命令行，39
- 浏览命令历史，19
- **内置 Bash 命令**
  - echo，319–320
  - false，状态代码，116
  - fc (fix command)，327
  - getopts (get options)，148–150
  - host，281–282, 297
  - if，88–89
  - let
    - (!) (双括号)，99
    - () (括号)，98
    - 别名，99
    - 算术表达式，93–95, 99–100
    - 分配多个变量，98
    - 条件表达式运算符，98
    - 评估多个表达式，98
    - 解释表达式，88
    - 逻辑表达式，95–98
  - set，320
  - suspend，160
  - test
    - [ ] (方括号)，91
    - 算术测试，100–101
    - 文件测试，89–90
    - 解释表达式，88
  - **Korn shell**，92
    - -n 开关，92
    - -o 开关，109
    - 字符串比较，92
    - 字符串测试，113
    - 开关，112–113
    - -z 开关，92
  - time，134, 142
  - true，状态代码，116
  - 与 Linux 命令对比，62
- **builtin 命令**，62
- --bytes 开关，du 命令，325
- bzip2 (BWH zip) 命令，223

## C

- -c (--bytes) 开关
  - head 命令，190
  - wc 命令，191
- -c (--bytes=n) 开关，tail 命令，190
- c (change) 命令，221
- -c (--changes) 开关，chown 命令，270
- -c (--characters) 开关，cut 命令，192
- -c (--check) 开关，md5sum 命令，180
- -c (--complement) 开关，tr 命令，218
- -c (--count) 开关，grep 命令，210
- -c (--create) 开关，tar 命令，224
- -c (--check only) 开关，sort 命令，217
- -C (command) 开关，compgen 命令，322
- -C (compress) 开关，stp 命令，179
- **C 程序**
  - ls 命令，运行，329
  - open 函数，330–331
  - putenv 函数，330–331
  - 脚本，运行，330
  - system 函数，329
  - 变量，共享，331–332
- -C s (--line-byte=s) 开关，split 命令，180
- -c 开关，23
  - date 命令，320
  - history 命令，21

- 缓存 ext2，8
- 创建日历对话框，244
- -calender 开关，dialog 命令，244
- -caps 开关，selids 命令，236
- 回车符，115
- case 命令，115, 119
- 不区分大小写的文件排序，215
- cat 命令，180, 185
- cd (change directory) 命令，22
- CDPATH 变量，22, 83
- CGI (Common Gateway Interface) 环境变量，288–289, 298
- **CGI (Common Gateway Interface) 脚本**，284
  - 错误消息，285-287
  - 表单
    - *显示变量*，290-293
    - *输入标签*，289
- **cgi-bin 目录**，284-285
- **更改**
  - 绑定，17
  - 文件所有权，270
  - 文件权限，270, 272
    - *默认访问权限*，273-274
    - *八进制权限数字*，271
  - 文件名颜色，28
  - 键位映射，236
  - 区域设置，324
  - Linux 控制台显示中的文本样式，237
- **字符类（范围）**，102-103, 113
- **字符设备文件**，11
- **字符等价性，tr (translate) 命令**，218
- **字符，在文件中编辑**，217-218
- **复选框，创建**，240
- **检查**
  - 运行时错误，54-55
  - MySQL 数据库中的状态代码，316
- **--checklist 开关，dialog 命令**，240
- **checkout 命令**，131
- **chgrp (change group) 命令**，270
- **chmod (change mode) 命令**，270-272, 279
- **chown (change owner) 命令**，270, 278-279
- **croots 命令**，275
- **csuim 命令，验证文件**，179
- **--classifv 开关，ls 命令**，28
- **清理部分（脚本）**，55-57
- **clear 命令**，32
- **清除 Bash 会话显示**，32
- **客户端-服务器网络**，282-283
- **cndhist 选项（命令历史）**，21
- **-cmin 开关，find 命令**，212
- **cmp 命令**，180
- **-cnewer 开关，find 命令**，212
- **代码**
  - ASCII 代码，列表，367-370
  - 错误代码，列表，361-364
  - 转义代码，echo 命令，332
  - 补丁文件，创建/应用，139-140
  - pecl shell 脚本示例，337-334
  - 排序代码，ps 命令，168
- **碰撞**，306
- **-color 开关，ls 命令**，28
- **列**
  - 创建，30
  - 在文件中，194
- **columns 命令**，194
- **COLUMNS 变量**，69, 83
- **-command sjclcmd 开关，psql 命令**，314
- **组合**
  - 对话框，244
  - 文件，195-196
  - 多个命令，18
- **command 命令**
  - 递归函数，264
  - 开关，62-64
- **命令历史**
  - 浏览，19
  - cndhist 选项，21
  - 命令行
    - *访问*，20
    - *添加*，21
    - *删除*，21
  - 文件，从加载/保存，21
  - history 命令，20-21
  - listhist 选项，21
  - 保存，histappend shell 选项，20
  - 搜索，21
  - 会话历史，追加，21
  - 关闭，21
- **命令修饰符，词标识符**，328-329
- **命令结果替换扩展 (...)，109**
- **命令**，13
  - :(冒号)，24
  - -(行号)，223
  - ! 历史回忆，327-328, 335
  - . (source)，运行脚本，251




# 索引

- `^`（向上箭头）快速替换历史命令，21
- `a`（追加），221
- 添加，131
- 别名，36
- 参数，14
- 基本名称，170
- 绑定，39-42
- 中断，120-121
- 内置命令，62-63
- 内置，62
- bzip2（BWH zig），223
- `c`（更改），221
- 案例，115, 119
- 大小写敏感性，14
- 连接，180, 185
- 更改目录，22
- 检出，131
- 更改组，270
- 更改模式，270-272, 279
- 更改所有者，270, 278-279
- CSH主机，275
- 仓库，179
- 清除，32
- 比较，180
- 列，194
- 命令，62-64, 264
- 命令历史，19-21
- 注释，15
- 生成补全，321-322, 333-334
- 完整，323, 334
- 补全规范，322
- 复合，115
- 控制台字符，234
- 续行提示符，39
- 继续，120-121
- 复制，33-34, 48-49, 174
- 时间表，254-256, 265
- 上下文分割，180-181, 202
- 剪贴，191-192, 204
- 并发版本系统，130
  - 并发版本系统提交，132
  - 并发版本系统日志，132
- `d`（删除），221
- `D`（多行删除），223
- 日期，14, 24, 184, 320
- 声明，67-69, 73, 76, 82, 262
  - 确定类型，62
- 对话框，239-244, 247-248
- 差异，139-140
- 目录，23-25
- 脱离，159-160
- 磁盘使用情况，324-325, 334-335
- 转储按键，236, 245
- 回显，319-320, 332
- 编辑，39
  - 显示编辑功能，39
  - Emacs 模式，15
  - 历史验证 Shell 选项，20
  - 短命令，15
  - Vi 模式，15-16
- `\`（反斜杠）代码，40
- 扩展 grep，207
- ELF，118-119
- 启用，63-64
- 转义，115
- 评估，79
- 执行，187, 252-253, 265
- 正在执行，14
- 退出，57, 261
- 退出处理程序，163
- 展开，182, 203
- 导出，264
- -f（强制），172-173
- 假，116
- 修复命令，327
- 数字，158
- 文件图标，234
- 固定字符串 grep，207
- 文件，171-172, 198
- 过滤器，14
- 查找，210-214, 226-228
- 查号，35
- 折叠，195
- 空闲，325-326
- 文件传输工具，177
  - 开关，202
  - 传输文件，177–178
- 文件复制，178
- 函数，260–261
- 函数摘要，查看，31
- 获取选项，148–156
- 全局搜索，207–210, 225–226
- 分组，122
- 哈希，37
  - 哈希 列表，37
  - 哈希表，37
- 头部，189–190, 203
- 帮助，31
  - 帮助 类型，32
- 历史，20–21, 25
- 主机，281–282, 297
- `i`（插入），221
- 标识，269, 278
- 如果，88–89, 117–118
- 导入，131
- 作业，158–159, 166
  - 作业 –s，159
- 连接，195–196, 204
- 键盘模式，235
- 杀死，158, 166
- 杀死所有，163–164
- `l`（列表），222
- 更少，139
- 让，93–100, 116, 121–122
- 加载按键，236
- 局部，262
- 区域设置，324
- 区域定义，324
- 定位，210
- 长命令行，39
- 列出，27–28, 45–47, 329
- 手册，31–32
  - 手册 1，32
  - 手册 1 类型，32
- 模型，180
- 合并，196–197, 205
- 创建目录，32–33
- 命名管道，184
- 临时目录，182–183, 203
- 多重，18
- 移动，34, 49, 174
- My SQL，316–318
- `N`（追加下一个），223
- `n`（下一个），223
- 名称，34
- 在...中导航，15
- 优先级，164
- 无挂断，256
- 选项，开启/关闭，63–64
- `p`（打印），223
- 参数，14
- 粘贴，192–194, 204
- 补丁，140
- 路径检查，170–171
- 路径，设置，37
- 管道，59
- 管道连接，59
- 弹出目录，23
- 打印格式化，17, 28–31, 47
- 打印选项，64
- 优先排序，164
- 进程状态，164–168
- Postgres SQL，313–318
- 推入目录，23
- 打印工作目录，21, 25
- `q`（退出），223
- 读取，57–58, 64, 76, 155, 187
- 只读，261, 264–265
- 重定向，58–61
- 重新优先级，164–166
- 重复，19, 119
- 重置，32
- 结果，赋值给变量，18, 69
- 返回，252
- 移除，33, 48, 132, 172, 278
- 递归目录，33
- 流编辑器，219–220, 223, 231–232
  - Sed 替换，219
- 选择，238–239
- 设置，63, 320
- 设置后台作业，158
- 设置 LED，235–236, 245
- 设置终端，237–238, 246–247
- SSH 文件传输协议，178–179
- Shell 归档，141–144
- 移位，147–148
- 商店，15, 63-64, 73
  - 商店 → 展开别名，36
- 显示按键，235, 245
- 信号，列表，365-366
- 睡眠，57
- 排序，215-217, 228-229, 313
- 分割，180
- 状态，174-175, 198
- 状态文件，175-176, 198-200
- 状态，133
- 状态码，115-118
- 字符串类型，16, 24, 32
- 子 shell，154-155
- 超级用户，274
- 求和，179
- 暂停，57, 65, 160
- 开关，14-15
- `t`（测试），223
- 尾部，190, 203
- 磁带归档，224-225, 229-230
- 技术，133, 141
- 测试，88-92, 100-101, 109, 112-113, 116
- 时间，134-136, 142-143
  - 时间-a 开关，136, 142
  - 时间-o 开关，136, 142
  - 时间-p 开关，136, 142
  - 时间-v 开关，136, 142
- 触觉，173
- 终端放置，238
- 翻译，29, 217-218, 231
- 陷阱，128, 161-162
- 真，116, 120
- 尝试，234
- 类型，62, 171, 198
- 用户限制，275-276, 279
- 用户掩码，273-274
- 取消别名，36
- 取消展开，182, 203
- 取消设置，69, 76
- 取消 Shell 归档，141
- 更新，131
- 更新程序，210
- 用户，35
- 实用工具，14
- `w`，35
- 监视，134
- 单词计数，191, 204
- 万维网获取，177, 200-202
- 谁，35
- 擦除，278-280
- `y`（转换），222
- `:`（冒号），24
- `^`（向上箭头）快速替换历史命令，21
- 注释（脚本），15, 52
- 比较字符串，测试命令，92
- 生成补全 命令，321-323, 333-334
- 完整 命令，323, 334
- 补全，321-322
- 复合命令，115
- 补全回复 变量，83
- 补全文件，223-224
- 补全当前单词 变量，83
- 补全行 变量，83
- 补全点 变量，83
- 补全单词 变量，83
- 条件表达式运算符，let 命令，98
- 控制台客户端，Postgres SQL，313-315
- 控制台脚本，233
- 控制台字符 命令，234
- 控制台。参见 Linux 输入模式，234-235 虚拟，233
- 常量（变量），创建，74
- 持续执行脚本，编写，256-259
- 续行提示符（命令），39
- 继续 命令，120-121
- 控制-b 绑定（Emacs 编辑模式），15
- 控制-f 绑定（Emacs 编辑模式），15
- 控制-n 绑定（Emacs 编辑模式），15
- 控制-p 绑定（Emacs 编辑模式），15
- 转换
  - 消息文本转大写，29
  - 制表符转空格，182
- 复制
  - 文件描述符，188
  - 文件，33, 174
- --count–links 开关，磁盘使用情况 命令，325
- 计数 变量，子 shell，154
- 复制 命令，33-34, 48-49, 174
- 创建
  - 数组，74
  - 关联数组，302-305
  - 后台文本对话框，244
  - 绑定，41
  - 日历对话框，244
  - 复选框，240
  - 列，30
  - 常量，74
  - 对话框，239-240
  - Linux 中的目录，32
  - 文件选择对话框，241
  - 文件名，28, 176
  - 文件，173
  - 函数，265
  - 仪表，242-243
  - 全局常量，77
  - 哈希公式，305
  - 无限循环，120
  - 信息对话框，243
  - 宏，42
  - 手册页，137
  - 菜单对话框，243
  - 消息对话框，243
  - 命名管道，184
  - 密码对话框，243
  - 补丁文件，139-140
  - 单选列表对话框，243
  - 脚本
    - 清理部分，55-57
    - 设计原则，52
    - 全局声明，54
    - 头部，53
    - 合理性检查，54-55
  - Shell 别名，36
  - 信号处理程序，161
  - 尾部对话框，243
  - 临时目录，183
  - 临时文件，182
  - 文本对话框，244
  - 时间对话框，244
- 笔录，133
- 变量，17, 68
- while 循环，119
- 是/否 对话框，240
- Cron 程序，253-256
- 时间表 命令
  - 周期性脚本，编写，254-256
  - 开关，265
- 时间表 表，编辑，254
- 上下文分割 命令，180-181, 202
- c-time 开关，查找 命令，212
- 当前目录，9
  - 文件，列出，27
  - 新目录，切换到，23
  - 切换，22
- 光标开关，设置终端 命令，238
- 自定义菜单
  - 复选框，创建，240
  - 对话框
    - 组合，244
    - 创建，239-244
    - 仪表，创建，242-243
- 自定义
  - 配置文件，42-45
  - 提示符，37-38
  - Postgres SQL 命令，314
- 剪贴 命令，191-192, 204
- CSV（并发版本系统），129
  - 命令，130-133
  - 检出，131
  - 并发版本系统提交，132
  - 并发版本系统日志，132
  - 状态，133
  - 关键字，130
- 并发版本系统 命令，130
- 并发版本系统提交 命令，132
- 并发版本系统日志 命令，132
- 并发版本系统根 变量，85
- D
  - -d（比较）开关，磁带归档 命令，225
  - d（删除）命令，221
  - -d（删除）开关
    - 哈希 命令，37
    - 翻译 命令，217

*我们如何让此索引更有用？请通过电子邮件联系我们：indexes@samspub.com*





## d

- **-d（--delimeter）开关**
    - cut 命令，191
    - paste 命令，193
- **-d（directory）开关**
    - mktemp 命令，183
    - run 命令，33
- **D（多行删除）命令**，223
- **-d（phone directory）开关**，sort 命令，216
- **-d 开关**
    - date 命令，320
    - enable 命令，63
    - history 命令，20
- **-D 开关**
    - setleds 命令，236
    - wipe 命令，27

## 守护进程脚本

256-259

## 悬挂链接

11

## 数据库

- 区域设置，更新，324
- MySQL，316-317
- PostgreSQL，313-315
- 210

## date 命令

320

- 参数，14
- 锁定文件，184
- 开关，24

## --dbname db 开关

psql 命令，314

## 调试陷阱

128

## 脚本调试

- 调试陷阱，128
- **-n（no execution）开关**，125
- **-o errexit 选项**，125，143
- **-o nounset 选项**，126，143
- **-o xtrace 选项**，126-127，143

## declare 命令

67

- 局部变量，声明，262
- 开关，76，82
- 变量
    - 创建，68
    - 列出预定义变量，69
    - 开启/关闭属性，73

## 声明

- 局部变量，262
- Shell 函数，260-261
- 变量，67

## 更改默认访问权限

273-274

## 默认值赋值扩展

106

## 默认值覆盖扩展

107

## 默认值扩展

106

## --default= 开关

dialog 命令，240

## 定义关键字宏

42

## 退化树

309

## --delete 开关

tar 命令，225

## 删除

- 绑定，41
- 命令历史中的命令行，20
- 从 Linux 中删除目录，33
- 文件，33，172-173，278
- 文件中的行，192，221
- 多个文件，173
- 从代码仓库中删除脚本，132
- Shell 别名，36
- 文件中的子字符串，191
- 数组中的值，76

## 分隔符

- 文件，排序，215
- 多个文件字段，191-192
- 空格，用作，191

## --dereference 开关

chown 命令，270

## --dereference-args 开关

du 命令，325

## 描述符（文件）

187-189

## 确定命令类型

62

## 设备文件

11-12

## 对话框

- 背景文本，创建，244
- 日历，创建，244
- 组合，244
- 创建，239-240
- 文件选择，创建，241
- 信息，创建，243
- 输入，创建，243
- 菜单，创建，243
- 密码，创建，243
- 单选列表，创建，243
- 尾部，创建，243
- 文本，创建，244
- 时间，创建，244
- 是否，创建，240

## dialog 命令

239-244，247-248

## diff 命令，补丁文件

139-140

## 目录

- .（当前目录），22
- ..（父目录），22
- /dev，11
- cgi-bin，284-285
- 命令，21-22，25
- 当前目录，9
    - 列出文件，27
    - 切换，22-23
- dirs 命令，23-25
- 执行权限，268
- 文件，添加至，131
- 主目录，9
- Linux，从中创建/删除，32-33
- 父目录，9
- 路径名，9-10
- popd 命令，23
- pushd 命令，23
- 读取访问，268
- 代码仓库，129-132
- 根目录，9，275
- 保存的目录，查看，23
- 临时目录，创建，183
- 查看，21
- 写入访问，268

## dir -1 开关

23

## dirs 命令

23-25

## DIRSTACK 变量

83

## 禁用内置 Bash 命令

63

## disown 命令

159-160

## DISPLAY 变量

70，85

## 显示

- 作业控制中的活动作业，158
- 命令行编辑功能，39
- 补全列表，321
- 错误消息，286-287
- 文件行长度，191
- 文件行号，191
- 文件大小，191
- 文件单词数，191
- 文件中的首行，189-190
- 表单变量，290-293
- 二叉树中的项，312-313
- 作业控制中的作业状态变化，158
- 键位映射，236
- 文件中的末行，190
- man 页，138-139
- 信号，161
- 文件中的符号，28
- 文本中的不可打印字符，222
- 变量属性，74

## 发行版，登录时运行多个文件

44

## 分割文件

180-181

## dotglob shell 选项

104

## du（磁盘使用量）命令

324-325，334-335

## -dump 开关

lynx，295

## dump，树函数，二叉树

312-313

## dumpkeys 命令

236，245

## e

## ~（转义）开关

- echo 命令，319
- killall 命令，164
- read 命令，58

## -E 开关

echo 命令，320

## echo 命令

319-320，332

## 编辑

- 文件中的字符，217-218
- 命令，39
- \（反斜杠）代码，40
- emacs 模式，15
- history shell 选项，20
- shop 命令，15
- stty 命令，16
- vi 模式，15-16
- crontab 表，254
- 文件，219-223

## EDITOR 变量

70，85

## egrep（扩展 grep）命令

207

## el$ 命令

118-119

## emacs 编辑模式（命令）

15

## enable 命令

63-64

## 环境变量

77-78，250，254

## 等价类（范围）

103

## erase 键，vi 编辑模式功能

16

## 错误代码，列表

361-364

## 错误处理

- 调试陷阱，128
- -no（no execution）开关，125
- -o errexit 调试选项，125，143
- -o nounset 调试选项，126，143
- -o xtrace 调试选项，126-127，143
- 运行时错误检查，54-55

## 错误消息

- 403 禁止，286
- 404 未找到，286
- 500 内部服务器错误，286
- 显示，286-287
- Linux 控制台，234

## esc 命令

115

## Esc 键

16

## 转义代码，echo 命令

332

## 转义序列（Bash 提示符）

38-39

## EUID 变量

83

## eval 命令

79

## --exclude-from=f 开关

du 命令，325

## --exclude=f 开关

du 命令，325

## exec 命令

- 文件，打开，187
- 脚本，运行，252-253
- 开关，265

## -exec 开关

find 命令，213

## -exec=sqllmnd 开关

mysql 命令，316

## 执行命令

14

## 执行权限，目录

268

## exit 命令

57，261

## 退出处理器

163

## expand 命令

182，203

## 扩展

87

- :=（默认值），106
- :=（默认值赋值），106
- :#（子字符串），107
- :+（默认值覆盖），107
- :?（变量存在性检查），107
- !*（变量名匹配），106
- #（子字符串移除），107
- #（变量长度），106
- ##（子字符串移除），107
- $（美元符号）扩展，105-109，113-114
- $（' 区域设置翻译），105
- $（ANSI C 转义），105，113-114
- %（子字符串移除），107
- %%（子字符串移除），107
- (...)（算术表达式替换），109
- (...)（命令结果替换），109
- //（子字符串替换），108
- 文件测试，89-90
- 解释，88
- shell 求值顺序，87

## export 命令

264

## 导出变量

参见 环境变量

## 表达式

87

- 算术
    - let 命令，93-95，99-100
    - 运算符，94-95
- 条件表达式运算符，98
- 逻辑
    - 按位运算符，96-97
    - let 命令，95-98，116
    - 关系运算符，96
    - 自引用运算符，97-98

## ext2

8

## ext3

8

## -extract 开关

tar 命令，224

## f

## -f（--fields）开关

cut 命令，191

## -f（--quiet）开关

chown 命令，270

## -f（file）开关

file 命令，172

## -f（fold character case together）开关

sort 命令，215

## -f（force）命令

删除文件，172-173

## -f（force）开关

- cp 命令，34
- mv 命令，34，174
- rm 命令，33
- touch 命令，173

## -f（function）开关

export 命令，264

## -F（function）开关

- compgen 命令，322
- readonly 命令，265

## -f F（--file F）开关

tar 命令，224

## -f P（--prefix=P）开关

csplit 命令，181

## -f 开关

- enable 命令，63
- type 命令，62

## -F 开关

- ls 命令，28
- setsels 命令，236

## false 命令，状态代码

116

## fc（fix command）

327

## FCE2DT 变量

83

## fg 命令

158

## ficonsole 命令

234

## fgrep（固定字符串 grep）命令

207

## 字段编号，文件排序

216

## FIFOs

参见 命名管道

## FIGNORE 变量

83

## file 命令

171-172，198

## 文件名扩展（*）

104

## 文件选择对话框，创建

241

## --file 开关

psql 命令，314

## 文件测试

89-91

## 文件名，创建

176

## 文件

- 访问权限数字，268
- 归档，223-224
- 备份，174-176
- 回车符，218
- 字符编辑，217-218
- 关闭，189
- 列，194
- 组合，195-196
- 压缩，223-224
- 复制，33，174
- 创建，173
- 当前目录，在其中列出，27
- 删除，33，278
- 描述符，187-189
- /dev/stderr，61
- /dev/stdin，61
- /dev/stdout，60
- /dev/tty，60-61
- 设备，11-12
- 目录，9-11
- 编辑，219-223
- /etc/profile，43
- 字段，重排，196
- 文件名，创建，176
- 查找，210-214
- 首行，显示，189-190
- 通用信息，查看，174
- 此处，60
- 识别，171
- 末行，显示，190
- 行
    - 添加，192-194
    - 删除，221
    - 显示长度，191
    - 查找，207-210
    - 合并，194
    - 移除，192
    - 替换，221
    - 换行，195
- 链接，10-11
- 锁定，183-184
- 合并，196-197
- 在 Linux 中移动，34
- 多个字段，分隔符，192
- 多个文件
    - 删除，173
    - 登录时通过发行版切换，44
- 命名管道，184-187
- 名称
    - 更改颜色，28
    - 使用隐藏字符创建，28
    - 多个文件名扩展，104
    - 后缀代码，8
- 行数，显示，191
- 打开，187-188
- 覆盖，noclobber shell 选项，326-327
- 所有权，更改，270
- 补丁，创建/应用，139-140
- 权限，9-10
- 权限，更改，270-274
- 管道，11
- 配置文件，42-45
- 常规，9
- 删除，172-173
- 重命名，34，174




# 索引

- 资源, 44
- 恢复, 224
- 大小, 显示, 191
- 套接字, 11
- 排序, 214-217
- 分割, 180-181
- 标准错误文件, 61
- 标准输入文件, 61
- 标准输出文件, 60-61
- 子字符串, 移除, 191
- 符号, 显示, 28
- 临时文件, 182
- 文本, 169
    - 显示不可打印字符, 222
    - 识别, 171
    - 插入到行中, 221

- 路径名, basename 命令, 170
- 路径名, pathchk 命令, 170-171
- 在其中替换字符, 222
- 文本流, 170
- 截断, 171
- 传输, 177-179
- 验证, 179-180
- 单词计数, 显示, 191

- 过滤器, 14
- find 命令, 210-214, 226-228
- find 表达式, 211
- 查找
    - 文件行, 207-210
    - 文件, 210-214
    - 关联数组中的项, 302-305
- fingor 命令, 35

- -fixed-strings 选项, grep 命令, 208
- 标志。参见 选项
- 闪烁屏幕, Linux 控制台显示, 237-238
- fold 命令, 195

- 字体 (文本), Linux 控制台, 234
- 脚注, 在 lynx 中隐藏, 295
- for 循环, 121
- 格式代码, 29-30
- \\ (反斜杠), 30-31
    - find -printf 命令, 227-228
    - printf 命令, 47

- statfile 命令, 175-176, 198-200
- time 命令, 134-135, 142-143

- 表单
    - Ast Tech Support, 294
    - 输入标签, 289
    - POST 方法编码, 289
    - 变量, 显示, 290-293
    - x-www-form-urlencoded 编码, 289

- free 命令, 325-326

- -from 选项, chown 命令, 270
- -select 选项, dialog 命令, 241

- FTP 命令, 177-178, 202

- fpcopy 命令, 178
- FUNCNAME 变量, 69, 83

- function 命令, 声明 shell 函数, 260-261

- 函数
    - $, 创建临时文件, 182
    - add_hash, 哈希表, 308
    - add_table, 关联数组, 305
    - add_tree, 二叉树, 312
    - 属性, 264
    - 创建, 265
    - dump_tree, 二叉树, 312-313
    - 列出, 265
    - 局部变量, 261-263
    - lookup_hash, 哈希表, 308
    - lookup_table, 关联数组, 305
    - lookup_tree, 二叉树, 312
    - 嵌套, 263-264
    - popen (C 程序), 330-331
    - putenv (C 程序), 330-331
    - 只读, 265
    - 递归, 263-264
    - 重新定义, 264
    - 下标, 与其共享, 264
    - system (C 程序), 329

## G

- -g (通用数字) 选项, sort 命令, 216
- g (组) 权限, 271
- -g (-group) 选项, id 命令, 269
- -G (-group) 选项, id 命令, 269
- -g 选项, 164
- -G 选项, cmpgen 命令, 322
- --gauges 选项, dialog 命令, 242-243
- 仪表, 创建, 242-243
- getopt (获取选项) 命令
    - 选项, 151-156
    - 变量, 148-152
- GET_COMPATIBLE 变量, 152
- --glob 选项, wget 命令, 177
- --glob=on 选项, wget 命令, 177
- 全局常量, 创建, 77
- 全局声明 (脚本), 54
- 通配符匹配, 101-104, 113
- GLOBIGNORE 变量, 83, 104
- GNU 项目, 开发, 8
- grep 命令, 207-210, 225-226
- groff (GNU run off), man 手册页, 136-139
- 分组命令, 122
- GROUPS 变量, 83

## H

- -h (SIGHUP) 选项, disown 命令, 160
- h 键, vi 编辑模式功能, 16
- 硬链接, 10
- 硬资源限制 (脚本), 276
- hash 命令, 37
- 哈希公式, 创建, 305
- hash is 命令, 37
- 哈希表, 37, 305
    - 添加项, 308
    - add_hash 函数, 308
    - 关联数组, 309
    - 冲突, 306
    - lookup_hash 函数, 308
    - 搜索其中的项, 308
    - 存储, 306-308
- 哈希值。参见 关联数组
- -hcolor 选项, setterm 命令, 237
- head 命令, 189-190, 203
- 标题 (脚本), 53
- hello.sh shell 脚本, 51
- help 命令, 31
- help type 命令, 32
- here 文件, 60
- --hide~control-chars 选项, ls 命令, 28
- 隐藏
    - 内置 Bash 命令, 63
    - lynx 中的脚注, 295
- histappend shell 选项, 20
- histchars 变量, 83
- HISTCMD 变量, 83
- HISTCONTROL 变量, 83
- HISTFILE 变量, 83
- HISTFILESIZE 变量, 83
- HISTIGNORE 变量, 83
- history 命令, 20-21, 25. 另见 ^ (上 caret) 快速替换 history 命令
- HISTSIZE 变量, 83
- histverif shell 选项, 20
- 主目录, 9
- HOME 变量, 69, 83
- host 命令, 281-282, 297
- HOST 变量, 85
- HOSTNAME 变量, 69, 83
- 主机名, 281
- HOSTTYPE 变量, 69, 83
- HTML
    - 颜色混合器脚本示例, 109-112
    - 论坛, 289
- --human-readable 选项, du 命令, 324

## I

- -I (--bzip) 选项, tar 命令, 224
- -i (--ignore-case) 选项
    - grep 命令, 209
    - join 命令, 196
- -i (--ignore-interrupts) 选项, tee 命令, 133, 141
- -i (忽略不可打印字符) 选项, sort 命令, 216
- -i (--initial) 选项, expand 命令, 182
- i (插入) 命令, 221
- -l (整数) 属性, 73
- -l (交互式) 选项, 33-34
- -l (非交互式) 选项, FTP 命令, 177
- -l 选项, file 命令, 172
- id 命令, 269, 278
- 识别文件/文本类型, 171
- if 命令, 88-89, 117-118
- | (列表) 命令, 395
- IFS (内部字段分隔符) 变量, 69, 73, 84
- --ignore-fail-on-non-empty 选项, rm dir 命令, 33
- IGNOREEOF 变量, 84
- 忽略信号, 163
- import 命令, 将目录添加到仓库, 131
- 索引 (数组), 74
- 无限循环, 创建, 120
- 信息对话框, 创建, 243
- --infobox 选项, dialog 命令, 243
- --init-file 选项, 资源文件, 44
- inode 密度, 11
- inode 时间, 按此查找文件, 212
- 输入对话框, 创建, 243
- 输入模式 (控制台), 234-235
- --inputbox 选项, dialog 命令, 243
- INPUTRC 变量, 84-85
- 将文本插入到行中, 221
- 整型变量, 属性, 73-74
- 交互式 shell, 42
- 解释表达式, 88
- intr 键, vi 编辑模式功能, 16
- -inversescreen 选项, setterm 命令, 237-238
- IP 号码, 281
- ITERM 变量, 关联数组, 302
- 连接
    - 文件, 195-196
    - 正则表达式, 209

## K

- -k (--keep-files) 选项, cp split 命令, 181
- -k (键) 选项, sort 命令, 215
- k 键, vi 编辑模式功能, 16
- k - 选项, man 命令, 32
- kbd_mode 命令, 235
- KDEDIR 变量, 85
- 键组合。参见 绑定
- 键盘
    - 功能
        - 创建绑定, 41
    - 查看, 40
    - 输入, 在脚本中读取, 57-58
    - 列出功能, 40
    - 宏, 定义, 42
    - 选项, 查看, 41
- 键盘快捷键。参见 绑定
- 键码模式 (控制台输入模式), 235
- --keycodes 选项, showkey 命令, 235
- 键盘映射, 236
- 键 (关联数组), 301, 305
- 关键字
    - CVS 关键字, 130
    - Linux 搜索, 32
- kill 命令
    - 任务, 停止, 158
    - 选项, 166
- kill 键, vi 编辑模式功能, 16
- killall 命令, 163-164
- --killbytes 选项, du 命令, 325
- Korn shell
    - 通配符匹配, 101-104, 113
    - test 命令, 91-92

## J

- j 键, vi 编辑模式功能, 16
- job 命令, 166
- 作业控制, 157-158
- 任务, 157
    - 活动任务, 在作业控制中显示, 158
    - 分离, 159
    - 百分比代码, 158
    - PID, 查看, 158
    - 优先级, 164
    - 状态, 显示作业控制中的变化, 158
    - 停止, 158
- jobs -x 命令, 159
- jobs 命令, 158-159
- join 命令, 195-196, 204

## L

- -L (标签) 选项, merge 命令, 197
- -l (--lines) 选项, wc 命令, 191
- -l (链接) 选项, cp 命令, 34
- l (列表) 命令, 222

如何使此索引更有用？请通过电子邮件联系我们：indexes@samspublishing.com

- -1 (列表) 选项
    - bind 命令, 40
    - crontab 命令, 254
    - fc 命令, 327
    - hash 命令, 37
    - trap 命令, 161
- -I (--list) 选项, psql 命令, 313
- -I (长) 选项, jobs 命令, 158
- -I (--longoptions) 选项, getopt 命令, 152
- -L (--max-line-length) 选项, wc 命令, 191
- 1 键, vi 编辑模式功能, 16
- -1 s (--line=s) 选项, split 命令, 180
- -L 选项
    - file 命令, 172
    - setlds 命令, 236

- LANG 变量, 84
- LC_ALL 变量, 84
- LC_COLLATE 变量, 84, 323-324
- LC_CTYPE 变量, 84, 323
- LC_MESSAGES 变量, 84, 324
- LC_MONETARY 变量, 323
- LC_NUMERIC 变量, 323
- LC_TIME 变量, 324
- LED 灯 (键盘), 开启/关闭, 235
- less 命令, 显示 man 手册页, 139
- LESS 变量, 85
- LESSCHARSET 变量, 85
- LESSOPEN 变量, 85
- let 命令
- () (双括号), 99
- () (括号), 98
- 别名, 99
- 条件表达式运算符 (?), 98
- 嵌入, 121-122
- 表达式
    - 算术, 93-95, 99-100
    - 解释, 88
    - 逻辑, 95-98
    - 多个表达式, 98
    - 多个变量, 赋值, 98
- verse 命令状态码, 116
- LINENO 变量, 69, 84
- LINES 变量, 69, 84
- -linewrap 选项, setterm 命令, 238
- -link 选项, cp (复制) 命令, 174

- 链接
    - 悬空链接, 11
    - 硬链接, 10
    - inode 密度, 11
    - 路径, 在 Linux 文件中列出, 34
    - 符号链接, 10-11, 21
- Linux
    - 备份文件, 重命名, 174
    - Bash 脚本, 运行, 249-250
    - 命令
        - -F 选项, 265
        - -p 选项, 265
        - basename, 170
        - bzip2 (BWH zip), 223
        - cat, 180
        - dbggr (更改组), 270
        - chmod (更改模式), 270-272, 279
        - chown (更改所有者), 270, 278-279
        - droot, 275
        - dksum, 179
        - cmp, 180
        - columns, 194
        - comnandl, 62-64, 264
        - consoleclear, 234
        - cp (复制), 33-34, 48-49
        - crontab (时间表), 254-256, 265
        - csplit (上下文分割), 180-181, 202
        - cut, 191-192, 204
        - cvs, 130
        - date, 320
        - declare, 262
        - dialog, 239-244, 247-248
        - du (磁盘使用), 324-325, 334-335
        - dumkeys, 236, 245
        - egrep (扩展 grep), 207
        - exit, 252-253, 265
        - exit, 261
        - expand, 182, 203
        - export, 264
        - fjconsole, 234
        - grep (固定字符串 grep), 207
        - file, 171-172, 198
        - find, 210-212, 226-227
        - fold, 195
        - free, 325-326




- function, 260-261
- getopt（获取选项）, 151-156
- grp, 207-210, 225-226
- head, 189-190, 203
- id, 269, 278
- join, 195-196, 204
- kbd_mode, 235
- killall, 163-164
- loadkeys, 236
- local, 262
- locate, 210
- man（手册）, 31-32
- man 1（手册 1）, 32
- man 1 type（手册 1 类型）, 32
- merge, 205
- mkdir（创建目录）, 32-33
- mktemp, 182-183, 203
- mv（移动）, 34, 49
- name（名称节点）, 34
- nohup（不挂断）, 256
- passwd, 192-194, 204
- pathchk, 170-171
- readonly, 261, 264
- retrieving information, 62
- rm（移除）, 33, 48
- rmdir（移除目录）, 33
- running, 62
- sed（流编辑器）, 219-220, 223, 231-232
- sed s（替换）, 219
- select, 238-239
- setleds, 235-236, 245
- setterm, 237-238, 246-247
- shar, 141-144
- showkey, 235, 245
- sort, 214-217, 228-229
- split, 180
- stat, 174-175, 198
- statheme, 175-176, 198-200
- sudo, 274
- sum, 179
- tail, 190
- tar（磁带归档）, 224-225, 229-230
- time, 135-136, 142-143
- tput（终端输出）, 238
- tr（转换）, 217-218, 231
- tty, 234
- ulimit, 275-276, 279
- umask, 273-274
- unexpand, 182, 203
- unshar, 141
- versus Bash built-in commands, 62
- wc（字数统计）, 191, 204
- wget, 177, 200-202

### consoles

- displays, 237-238
- error messages, 234
- keyboard, 234-236
- text fonts, 234
- underlined text, 237
- virtual, 233

### development

- of, 7
- device files, 11-12
- directories, 9-11, 32-33
- environment variables, 77-78
- file systems, 8

### files

- copying, 33
- deleting, 33
- listing file path components, 34
- moving, 34
- renaming, 34
- keyword searches, 32
- links, 10-11
- partitions, 8
- pipe files, 11

### predefined variables

- CVSROOT, 85
- DISPLAY, 70, 85
- EDITOR, 70, 85
- _ETC_PROFILE, 85
- HOST, 85
- INPUTRC, 85
- KDEDIR, 85
- LESS, 85
- LESSCHARSET, 85
- LESSOPEN, 85
- LOGNAME, 85
- LS_COLORS, 85
- ORGANIZATION, 70, 85
- PAGER, 86
- PRINTER, 86
- QDIR, 86
- TEMPDIR, 86
- TERM, 70, 86
- USER, 86
- VISUAL, 70, 86
- WINDOWMANAGER, 70, 86
- security, 267–269
- socket files, 11
- variable attributes, 77

### --list switches, tar command, 225

- active jobs in job control, 158
- Bash command options, 64
- built-in Bash commands, 63
- file link path components in Linux, 34
- files in current directories, 27
- functions, 265
- keyboard functions, 40
- macros, 42
- predefined variables, 69
- shell aliases, 36
- signals, 161

### lidhist option (command history), 21

### loading

- command histories from files, 21
- MySQL commands into MySQL databases, 317

### loadkeys command, 236

### local command, 262

### local variables, 261–263

### locale command, 324

### locale translation expansions (S\*), 105

### localedef command, 324

### locales

- changing, 324
- databases, updating, 324
- variables, 323–324

### locate command, 210

### locate database, maintaining, 210

### locating

- files via pathname, 210
- items
  - in associative arrays, 302–305
  - in binary trees, 312
  - in hash tables, 308
  - keys in associative arrays, 305

### lock files, 183–184

### logging

- into MySQL databases, 316
- into PostgreSQL databases, 313

### logical expressions, 211

- bitwise operators, 96–97
- let command, 95–98, 116
- relational operators, 96
- self-referential operators, 97–98

### login shells, 42

- --login switches, profile files, 43
- LOGNAME variable, 85

### long command lines, breaking up, 39

### long switches, 14

### lookup tables. See associative arrays

### lookup_hash functions, hash tables, 308

### lookup_table functions, associative arrays, 305

### lookup_tree functions, binary trees, 312

### loops

- for, 121
- infinite, creating, 120
- until, 120
- while, 119–120

### ls (list) command, 27–28, 45–47, 329

### -ls switches, find command, 213

### LS_COLORS variable, 85

### -lu switches, ps command, 165

### lynx, 296–297

- --dump switches, 295
- footnotes, hiding, 295
- --no-list switches, 295
- --source switches, 294–295
- switches, 299

## M

### -m (keymap) switches, bind command, 40

### -m (model) switches, mdir command, 32

### -M (months) switches, sort command, 216

### MACHYTYPE variable, 84

### macros

- creating, 42
- groff (GNU run off) predefined macros, 137

### -N (view Nth) switches

- keyboard macros, defining, 42
- listing, 42

### MAIL variable, 84

### MAILCHECK variable, 84

### MAILPATH variable, 84

### maintaining

- locate databases, 210

### man (manual) command, 31-32

### man 1 type (manual 1 type) command, 32

### man 1 (manual 1) command, 32

### man pages, 136

- creating, 137
- displaying, 138-139

### --max-depth=n switches, du command, 325

### md5sum command, 180

### MEDIUMRAW mode, 5ex keycode mode

### --megabytes switches, du command, 325

### memory usage, monitoring, 325

### menu dialog boxes, creating, 243

### -menu switches, dialog command, 243

### menus

- custom
- combining dialog boxes, 244
- creating check boxes, 240
- creating dialog boxes, 239-244
- gages, 242-243
- select, 238-239

### merge command, 196-197, 205

### merging

- file lines, 194
- files, 195-197

### message dialog boxes, creating, 243

### messages

- converting text to uppercase, 29
- printing to screen, 28-31
- redirections, 58-61
- standard error files, 61
- standard input files, 61
- standard output files, 60-61

### mixer.bash script example, 109-112

### mkdir (make directory) command, 32-33

### mkfifo command, creating named pipes, 184

### mktemp command, 182-183, 203

### --mirror switches, wget command, 177

### -mum in switches, find command, 212

- modified time, finding files by, 212
- monitoring message usage, free command, 325

### moving

- file descriptors, 188
- files in Linux, 34
- root directories, 275

### -msgbox switches, dialog command, 243

### -mtime switches, find command, 212

### multiple commands, 18

- multiple file names, 104
- multiple files
  - archiving, 224
  - renaming, 173
  - testing, 90-91
- multiple sort keys, 216
- multiple variables, assigning, 98

### mv (move) command, 34, 49, 174

### MySQL commands, 316-318

### MySQL databases, 316-317

### N (append next) command, 223

### n (-line-number) switches, grep command, 209

### -n (-name) switches

- getopt command, 151
- id command, 269

### -n (new status) switches, jobs command, 159

### -n (no auto-login) switches, FTP command, 177

### -n (no change) switches, 23

### -n (no execution) switches, 125

### -n (no line numbers) switches, fc command, 327

### -n (no new line) switches, echo command, 319

### -n (no zero length) switches, 92

### -n (number) switches, date command, 320

### -n (number of characters) switches, read command, 58

### -n (numeric) switches, sort command, 216

### -N (rotate Nth) switches, 23

### -N (view Nth) switches, 23

### -n D (-digits=D) switches, csplit command, 181

### -n I (-lines=n) switches, head command, 189

### n (next) command, 223

### n spaces, 182

### -n switches

- enable command, 63
- history command, 21

### -N switches, popd command, 23

### -name switches, find command, 211

### -name "*.txt" -type f switches, find command, 211

### named pipes

- creating, 184
- process substitution, 186–187
- reading, 184–185

### namei (name inode) command, 34

### naming

- files, 8, 28
- switches, 14
- variables, 67

### navigating in commands, 15

### nested functions, 263–264

### networking

- CGI environment variables, 288–289, 298
- CGI scripts, 284
- displaying form variables, 290–293
- error messages, 285–287
- form input tags, 289
- client-server, 282–283
- forums, 289
- hostnames, 281
- IP numbers, 281
- P2P, 282
- protocols, 282
- sockets, 282
- Web servers, opening connections to, 283–284

### NEXTITEM variables, associative arrays, 302

### -newer switches, find command, 212

### nice command, 164

### no change (-n) switch, 23

### nocasglob shell option, 104

### noclobber shell option, overwriting files, 326–327

### noglob shell option, 104

### nohup (no hang up) command, 256

### -no-list switches, lynx, 295

### -norprofile switches, profile files, 44

### -nore switches, resource files, 44

### not operators versus -a and -o switches, 91

### nullglob shell option, 104

### -num switches, setlds command, 236

### -numeric-uid-gid is switches, 267

## O

### -o (option) switches

- complete command, 323
- test command, 109

### o (other access) permissions, 271

### -o (output) switches

- join command, 196
- time command, 136, 142

### -o errexit debugging option, 125, 143

### -o nounset debugging option, 126, 143

### -o switches

- history command, 21
- versus not operators, 91

### -o xtrace debugging option, 126–127, 143

### octal permissions numbers, 271

### -ok switches, find command, 213

### OLDPWD variable, 22, 84

### -one-file-system switches, du command, 325

### opening

- connections to Web browsers, 283–284
- file descriptors, 187
- files, 187–188

### operators

- arithmetic, 94–95
- bitwise (logical) expression, 96–97
- conditional expression operators, 98
- redirexions, 59
- relational (logical) expressions), 96
- self-referential (logical expression), 97–98

### OSTRPNG variable, 148–150

### OPTARG variable, 85, 149

### OPTERR variable, 84, 149

### OPTIND variable, 85, 149

### ORGANIZATION variable, 70, 85

我们如何让此索引更实用？请通过电子邮件联系：indexes@sampublishing.com
我们如何让此索引更实用？请通过电子邮件联系：indexes@samsublishing.com




## O
OSTYPE 变量，70, 84
--output[name] 开关，psql 命令，316
--output[delimiter] 开关，cut 命令，192
覆盖文件，noclobber shell 选项，326-327

## P
- **-P (parents) 开关**
  - cp 命令，34
  - mkdir 命令，32-33
  - rmdir 命令，33
- **-p (path) 开关**
  - hash 命令，37
  - type 命令，62
- **-p (PID) 开关**
  - jobs 命令，159
  - rename 命令，164
- **-p (--portability) 开关**
  - pathchk 命令，171
  - time 命令，136, 142
- **-p (print) 属性，74**
- **p (print) 命令，223**
- **-p 开关**
  - complete 命令，323
  - find 命令，213
  - merge 命令，197
  - trap 命令，162
- **p 开关，23**
  - bind 命令，39
  - command 命令，62
  - enable 命令，63
  - history 命令，20
  - pwd 命令，21
  - readonly 命令，265
  - shopt 命令，64
  - unmk 命令，27
- **-P 开关**
  - cmpgen 命令，323
  - type 命令，62
- **P2P (peer-to-peer) 网络，282**
- **PAGER 变量，86**
- 参数，14
- getopt (get option) 命令，151-154
- getops (get options) 命令，148-150
- 位置参数，145-148
- 父目录，9, 22
- 括号 ()，let 命令，98
- 部分范围，通配符，102
- 分区，8
- 密码对话框，创建，243
- --password[=]开关，mysql 命令，316
- --passwordbox 开关，dialog 命令，243
- paste 命令，192-194, 204
- patch 命令，140
- 补丁文件，139-140
- **PATH 变量，70, 84**
- **pathck 命令，170-171**
- 路径名，9
  - 绝对路径，10
  - basename 命令，170
  - 文件，定位，210
  - pathchk 命令，170-171
  - 相对路径，10
- 模式识别。参见通配符
- peek shell 脚本示例，337-354
- 权限
  - g (group)，271
  - o (other access)，271
  - r (read)，271
  - setgid，274-275
  - setuid，274-275
  - t，272
  - u (user)，271
  - w (write)，271
  - x (execute)，272
- PID (process identification numbers)，查看，158
- 管道文件，11
- 管道（命令），59
  - 命令状态码，117
  - PIPESTATUS 数组，117
  - 进程替换，186-187
  - 文本流，170

### PIPESTATUS *数组*
- PIPESTATUS *数组*，117
- PIPESTATUS *变量*，84
- 轮询方法（守护脚本），257–259
- popd (pop *目录*) 命令，23
- popen 函数（C 程序），330–331
- 端口，282
- 位置参数，145–148
- POST 方法编码（表单），289
- PostgreSQL *数据库*
  - 登录，313
  - 状态码，315
- PPID *变量*，70, 84
- 预定义 *变量*
  - auto_resume, 82
  - BASH, 69, 82
  - BASH_ENV, 69, 82
  - BASH_VERSIONINFO, 82
  - BASH_VERSION, 69, 82
  - CDPATH, 83
  - COLUMNS, 69, 83
  - COMP_CWORD, 83
  - COMP_LINE, 83
  - COMP_POINT, 83
  - COMP_WORDS, 83
  - COMPREPLY, 83
  - CSHROOT, 85
  - DIRSTACK, 83
  - DISPLAY, 70, 85
  - EDITOR, 70, 85
  - _ETC_PROFILE, 85
  - EUID, 83
  - FCDKIT, 83
  - FIGNORE, 83
  - FUNCNAME, 69, 83
  - GLOBIGNORE, 83
  - GROUPS, 83
  - histchars, 83
  - HISTCMD, 83
  - HISTCONTROL, 83
  - HISTFILE, 83
  - HISTFILESIZE, 83
  - HISTIGNORE, 83
  - HISTSIZE, 83
  - HOME, 69, 83
  - HOST, 85
  - HOSTNAME, 69, 83
  - HOSTTYPE, 69, 83
  - IFS (internal field *separator*), 69, 73, 84
  - IGNOREEE, 84
  - INPUTRC, 84–85
  - KDEDIR, 85
  - LANG, 84
  - LC_ALL, 84
  - LC_COLLATE, 84
  - LC_CTYPE, 84
  - LC_MESSAGES, 84
  - LESS, 85
  - LESSCHARSET, 85
  - LESSOPEN, 85
  - LINEHO, 69, 84
  - LINES, 69, 84
  - listing, 69
  - LOGNAME, 85
  - LS_COLORS, 85
  - MACHTYPE, 84
  - MAIL, 84
  - MAILCHECK, 84
  - MAILPATH, 84
  - OLDPWD, 84
  - OPTARG, 85
  - OPTERR, 84
  - OPTIND, 85
  - ORGANIZATION, 70, 85
  - OSTYPE, 70, 84
  - PAGER, 86
  - PATH, 70, 84
  - PIPESTATUS, 84
  - PPID, 70, 84
  - PRINTER, 86
  - PROMPT_COMMAND, 70, 84
  - PS1, 70, 84
  - PS2, 70, 84
  - PS3, 70, 84
  - PS4, 70, 85
  - PWD, 70, 85
  - QTDIR, 86
  - RANDOM, 70, 85
  - SECONDS, 85
  - SHELL, 70, 85
  - SHELLOPTS, 85
  - SHLVL, 85
  - TMPDIR, 86
  - TERM, 70, 86
  - TIMEFORMAT, 85
  - TMOUT, 85
  - UID, 85
  - USER, 86
  - VISUAL, 70, 86
  - WINDOWMANAGER, 70, 86
- present working directory (pwd) 命令，21, 25
- PRINTER 变量，86
- printf (print formatted) 命令，17, 28–31, 47
  - -printf 开关，find 命令，214, 227–228
  - 打印
    - Bash 命令选项，64
    - 内置 Bash 命令，63
    - 向屏幕输出消息，28–31
    - 不解释特殊字符的字符串，72
    - 变量值，17
  - 优先级
    - 命令，164
    - 作业，164
  - 进程替换，186–187
  - 配置文件，42–45
  - 提示符
    - 续行提示，39
    - 自定义，37–38
    - 转义序列，38–39
  - PROMPT_COMMAND 变量，70, 84
  - ps (process status) 命令，165–168
  - PS1 (prompt string 1) 变量，37, 70, 84
  - PS2 (prompt string 2) 变量，38, 70, 84
  - PS3 (prompt string 3) 变量，70, 84
  - PS4 (prompt string 4) 变量，70, 85
  - psql 命令，314–318
    - psql 控制台客户端
      - 配置，314–315
      - PostgreSQL_databases，登录，313
  - pushd (push directory) 命令，23
  - putenv 函数（C 程序），330–331
  - pwd (present working directory) 命令，21, 25
  - PWD 变量，70, 85

## Q – R
- **-q (--quiet) 开关**
  - csplit 命令，181
  - getopt 命令，154
  - merge 命令，197
  - mktemp 命令，183
- **-Q (--quiet-output) 开关**，getopt 命令，154
- **-q (query) 开关**，bind 命令，40
- **q (qui) 命令**，223
- **-q 开关**
  - killall 命令，164
  - ls 命令，28
  - **QTDIR 变量，86**
  - **queues *参见命名管道***
- **--quiet 开关**，wget 命令，177
- **-r (raw input) 开关**，read 命令，58
- **r (read) 权限**，271
- **r (read-only) 属性**，74
- **-r (--real) 开关**，id 命令，269
- **-r (recursive) 开关**，rm 命令，33
- **-R (--recursive) 开关**
  - chown 命令，270
  - cp 命令，34
- **-r (remove) 开关**
  - bind 命令，41
  - complete 命令，323
  - hash 命令，37
- **-r (reverse) 开关**
  - fc 命令，327
  - sort 命令，215
- **-r (running) 开关**，jobs 命令，159
- **r 开关**，history 命令，21
- **竞态条件**（锁文件），184
- **单选项对话框**，创建，243
- **--radiolist 开关**，dialog 命令，243
- **RANDOM 变量，70, 85**
- **范围**
  - 字符类，102–103, 113
  - 等价类，103
  - 通配符，102
- **RAW 模式 *参见 scancode 模式***
- **-rfile 开关**，资源文件，44
- **读取权限（目录）**，268

## read 命令
- read 命令，57, 187
  - 数组，将列表读入，76
  - 子 shell，155
  - 开关，58, 64
- 只读函数，265
- 读取
  - 文件，187–188
  - 脚本中的键盘输入，57–58
  - 将列表读入数组，76
  - 命名管道，184–185
- readonly 命令
  - 函数，264
  - shell 函数，261
  - 开关，265
- 重排文件字段，196
- 重新评估拆分文件，180
- 编写循环脚本，254–256
- 递归函数，263–264
- 重新定义函数，264
- 重定向，58–59
  - 组合使用，61
  - 标准错误，61
  - 标准输入，61
  - 标准输出，60
- --reference 开关，chown 命令，270
- 正则表达式
  - grep 命令，208
  - 连接，209
  - sed 命令，219
- 常规文件，9
- 关系运算符（逻辑表达式），96
- 相对路径，10
- 重新加载内置 Bash 命令，63
- 移除
  - 绑定，41
  - 命令历史，21
  - 命令历史中的命令行，20
  - 从 Linux 移除目录，33
  - 文件，33, 172–173, 278
  - 文件中的行，192
  - 从仓库移除脚本，132
  - shell 别名，36
  - 文件中的子字符串，191
  - 数组中的值，76
- 重命名
  - 备份文件，174
  - 文件，34, 174
- renice 命令，164–166
- -repeat 开关，setterm 命令，238
- 重复命令，19, 119
- 替换
  - 文本中的字符，222
  - 文件中的行，221
- 报表格式化示例脚本，122–124
  - report.bash 报表格式化示例脚本，122–124
- 仓库，129
  - 目录，添加，131
  - 脚本，删除，132
  - 更新，131
- reset 命令，32
  - -reset 开关，setterm 命令，237
- 资源文件，44
- 资源限制（脚本），275–276
- 恢复
  - Bash 会话，32
  - 文件，224
- 受限 shell，277
- 获取 Linux 命令信息，62
- return 命令，252
- 反转文件排序顺序，215
- rm (remove) 命令
  - 文件，移除，172
  - 脚本，从仓库删除，132
  - 开关，33, 48
- rmdir (remove directory) 命令，33
- 根目录，9, 275
- 根（二叉树），309
- rotate Nth (-N) 开关，23
- rprint 键，vi 编辑模式功能，17
- 运行
  - 内置命令，62
  - Linux 命令，62
  - C 程序中的 ls 命令，329
  - 通过分发版登录时运行多个文件，44
  - 脚本，52
  - 脚本
    - con 程序，253–256
    - C 程序中，330
    - supeuser 登录，270




## 脚本
- 405
- 通过 .（source）命令，251
- 通过 exec 命令，252-253
- 通过 Linux，249-250

运行时错误检查，54-55

## s
- -s（所有）开关，help 命令，31
- -s（仅分隔符）开关，cut 命令，192
- -s（串行）开关，paste 命令，194
- -s（设置）开关，shopt 命令，64
- -s（静默）开关，caplot 命令，181
- -s（空格）开关，fold 命令，195
- -s（压缩重复项）开关，tr 命令，218
- -s（停止）开关，jobs 命令，159
- -s（替换）开关，fc 命令，327
- -s（符号链接）开关，cp 命令，34

### -s 开关
- bind 命令，42
- columns 命令，194
- enable 命令，63
- history 命令，21
- pipe 命令，278

### -S 开关
- compgen 命令，323
- umask 命令，273

健全性检查（脚本），54-55, 90-91

## 保存
- 命令历史，20-21
- 文件描述符，188

扫描码模式（控制台输入模式），234
- -scanodes 开关，showkey 命令，235
- 脚本片段，参数，252
- 脚本 Shell，受限，277

## 脚本
- .（source）命令，251
- .bashrc（Bash 资源），44
- 别名，开启/关闭，36
- CGI，284
- 显示表单变量，290-293
- 错误消息，285-287
- 表单输入标签，289
- 清理部分，55-57
- 注释，52
- 控制台，233
- 控制台输入模式，切换，235
- 持续执行，编写，256-259
- 守护进程，256-259

### 调试
- -n（不执行）开关，125
- -o errexit 选项，125, 143
- -o nounset 选项，126, 143
- -o xtrace 选项，126-127, 143
- 调试陷阱，128

- 设计原则，52
- 退出处理器，163
- 全局声明，54
- 头部，53
- hello.sh，51
- 文件（here files），60
- 键盘输入，读取，57-58
- mixer.bash 示例，109-112
- 参数，148-154
- peek Shell 脚本示例，337-354
- 位置参数，145-148
- 配置文件，44
- 循环，编写，254-256

### 重定向
- 组合，61
- 标准错误，61
- 标准输入，61
- 标准输出，60

- report.bash 报表格式化器示例脚本，122-124
- 仓库，从中删除，132
- 资源限制，275-276

### 运行
- .（source）命令，251
- com 程序，253-256
- exec 命令，252-253
- 在 C 程序中，330
- Linux，249-250
- 高级标志，270

- 运行时错误检查，54-55
- 健全性检查，54-55, 90-91
- Shell 函数，260-261

## 信号
- 忽略，163
- 列表，365-366
- 列出，161
- SIGCONT，160-161
- SIGHUP，160-161
- SIGKILL，161
- SIGQUIT，161
- SIGSTOP，160
- SIGTERM，160
- SIGTRAP，161
- SIGTTIN，161
- SIGTTOU，161
- SIGUSR1，162
- SIGUSR2，162
- SIGWINCH，161

- 标准错误文件，61
- 标准输入文件，61
- 标准输出文件，60-61
- 停止，57, 160
- 故事：bash（故事生成器）示例，80-82
- 同步，锁文件，183-184
- temperature.bash 脚本示例，99-100
- 计时，134-136, 142-143
- 查看运行，134

- scroll 开关，sedol5 命令，236

## 搜索
- 用于键的关联数组，305
- 命令历史，19-21

### 项目
- 在二叉树中，312
- 在哈希表中，308
- Linux 关键字搜索，32

## SECONDS 变量，85

## 安全性
- 目录，268

## 文件
- 访问权限数字，268
- 删除，278

### Linux
- 访问权限数字，268
- chown（更改所有者）命令，270
- 执行权限（目录），268
- id 命令，269
- 读取访问（目录），268
- uid，267
- 写入访问（目录），268

- 权限，271-272
- 受限 Shell，277
- 根目录，移动，275
- 脚本，救援限制，275-276
- setgid 权限，274-275
- setuid 权限，274-275

## sed（流编辑器）命令，220, 223
- 编辑代码，231-232
- 行号，219
- 正则表达式，219
- 开关，231

- sed s（替换）命令，219
- select 命令，238-239
- select 菜单，238-239
- --separate-dirs 开关，du 命令，325
- --server-response 开关，wget 命令，177

- 会话配置文件，42-45
- set 命令，63, 320
- set-b 命令，158
- setgid 权限，274-275
- setleds 命令，235-236, 245
- setterm 命令，237-238, 246-247
- setuid 权限，274-275

- sftp（安全 FTP）命令，178-179
- shar（Shell 归档）命令，141-144

## 共享
- C 程序变量，331-332
- 带下标的函数，264

- Shell 归档，141
- Shell 函数，260-261

## Shell 脚本
- 清理部分，55-57
- 注释，52
- 设计原则，52
- 全局声明，54
- 头部，53
- hello.sh，51
- 文件（here files），60
- 键盘输入，读取，57-58

#### 重定向
- 组合，61
- 标准错误，61
- 标准输入，61
- 标准输出，60

- 运行，52

## statftime 命令，407
- 健全性检查，54–55
- 标准错误文件，61
- 标准输入文件，61
- 标准输出文件，60–61
- 停止，57

## SHELL 变量，70, 85

## SHELLOPTS 变量，85

## Shell
- 别名，36
- 命令，13–15
- 扩展，求值顺序，87
- histappend Shell 选项，20
- histverify Shell 选项，20
- 交互式，42

### Korn
- 通配符匹配，101–104
- test 命令，91–92

- 登录，42
- 受限，277

- shift 命令，147–148

## SHLVL 变量，85

## shopt（Shell 选项）命令，15, 63–64, 73
- shop -> expand_aliases 命令，36

## showkey 命令，235, 245
- --si 开关，du 命令，325

## SIGCONT 信号，160–161

## SIGHUP 信号，160–161

## SIGKILL 信号，161

## 信号处理器，161–163

## 信号，159
- 忽略，163
- 列表，365–366
- 列出，161
- SIGCONT，160–161
- SIGHUP，160–161
- SIGKILL，161
- SIGQUIT，161
- SIGSTOP，160
- SIGTERM，160
- SIGTSTP，161
- SIGTTIN，161
- SIGTTOU，161
- SIGUSR1，162
- SIGUSR2，162
- SIGWINCH，161
- 陷阱，161–162

## SIGQUIT 信号，161

## SIGSTOP 信号，160

## SIGTERM 信号，160

## SIGTSTP 信号，161

## SIGTTIN 信号，161

## SIGTTOU 信号，161

## SIGUSR1 信号，162

## SIGUSR2 信号，162

## SIGWINCH 信号，161

- -size 开关，find 命令，212

## sleep 命令，57

## 套接字文件，11

## 套接字，282

## 软资源限制（脚本），276

## 软件中断。参见 信号

## sort 代码，ps 命令，168

## sort 命令
- 二叉树，313
- 开关，215–217, 228–229

## sort 键，215–216

## 排序
- 文件，214
- 账号编号，217
- 不区分大小写的排序，215
- 更改字段分隔符，215
- 字段号，216
- 反转排序顺序，215
- 二叉树中的项目，313

- -source 开关，lync，294–295

## 稀疏文件存储，88

## split 命令，180

## 分割文件，180–181

## 标准错误文件，61

## 标准输入文件，61

## 标准输出文件，60–61

## 启动键，vi 编辑模式功能，17

## stat 命令，174–175, 198

## statftime 命令
- 创建归档文件名，176
- 保存文件，176
- 格式代码，175–176, 198–200

*我们如何让此索引更有用？请通过电子邮件联系我们：indexes@samspublishing.com*





## 状态代码
- 命令，115-118
- MySQL 数据库，检查时，316
- PostgreSQL 数据库，315
- shell 函数，返回时，261

## status 命令
- 133
- `--status` 选项，mfdsum 命令，180

## 粘滞位权限
参见 t 权限

## stop 键
- vi 编辑模式功能，17

## 停止
- 守护进程脚本，259
- 作业，158
- 脚本，57, 160
- while 循环，120

## 存储
- 在 Bash 数组中存储二叉树，309-312
- 在 Bash 数组中存储哈希表，306-308

## 故事生成器（story.bash）脚本示例
- 80-82

## story.bash（故事生成器）脚本示例
- 80-82

## 字符串
- 比较，92
- 展开，87
- `:-`（默认值），106
- `:=`（默认值赋值），106
- `:n`（子字符串），107
- `:+a`（默认值覆盖），107
- `:?`（变量存在性检查），107
- `!*`（变量名匹配），106
- `#`（子字符串移除），107
- `#`（变量长度），106
- `##`（子字符串移除），107
- `$*`（本地化翻译），105
- `$'`（ANSI C 转义），105, 113-114
- `%`（子字符串移除），107
- `%%`（子字符串移除），107
- `(.*)`（算术表达式替换），109
- `(.-)`（命令结果替换），109
- `//`（子字符串替换），108

- 文件测试，89-90
- 通过 let 命令解释，88
- 通过 test 命令解释，88
- shell 求值顺序，87
- 打印且不进行特殊字符解释，72
- 测试，113

## stty 命令
- 16, 24, 32

## 下标
- 函数，共享时，264
- shell 函数，260-261

## 子 shell
- 154-155, 250

## 替换（变量）
- 87
- `$$` 函数，80
- eval 命令，79

## 子字符串展开
- 107

## 子字符串移除展开
- 107

## 子字符串替换展开
- 108

## 子字符串
- 从文件中移除，191

## sudo 命令
- 274

## sum 命令
- 179
- `--summarize` 选项，du 命令，324

## 超级用户登录
- 运行脚本，270

## sus 键
- vi 编辑模式功能，17

## suspend 命令
- 57, 65, 160

## SWITCH 变量
- 149

## 选项
参见各单独条目

## 切换
- 当前目录，22-23
- Linux 控制台显示中的文本颜色，237

## 符号链接
- 10-11, 21

## 符号
- 在文件中显示，28

## 同步脚本
- 锁文件，183-184

## 系统函数（C 程序）
- 329

## T

## -t (table) 选项
- hash 命令，37

## -t (terse) 选项
- stat 命令，175

## t (test) 命令
- 223

## -t (timeout) 选项
- read 命令，58

## -t (--truncate-set-il) 选项
- tr 命令，218

## -t (type) 选项
- type 命令，62

## t n 选项
- expand 命令，182

## t 权限
- 272

## -t 选项
- column 命令，194
- free 命令，326
- host 命令，282

## -u (-user) 选项
- join 命令，195
- sort 命令，215

## Tab 键
- emacs 编辑模式功能，15

## --tabs 选项
- expand 命令，182

## 制表符
- 转换为空格，182
- `--tabs=n` 选项，unexpand 命令，182

## 标签
- 表单输入，289

## tail 命令
- 190, 203

## tail 对话框
- 创建，243
- `--tailbox` 选项，dialog 命令，243

## tar (tape archive) 命令
- 224–225, 229–230

## TCP/IP (传输控制协议/互联网协议)
- 282

## tee 命令
- 133, 141

## TEMPDIR 变量
- 86

## 温度
- bash 脚本*示例*，99–100

## 临时目录
- 创建，183

## 临时文件
- 创建，182

## TERM 变量
- 70, 86

## 终端脚本
*参见* 控制台脚本

## test 命令
- *表达式*
  - *算术测试*，100–101
  - *文件测试*，89–91
  - *解释*，88
- Kora shell，91–92
- 状态代码，116
- 字符串测试，113
- 字符串，比较，92
- *选项*，92, 109, 112–113

## 测试
- *文件*，89–91
  - *字符串*，113

## 文本
- *字符，替换*，222
- *颜色，在 Linux 控制台显示中切换*，237
- *文件*，169–171
- *字体，Linux 控制台*，234
- *行，插入*，221
- *空格，转换为制表符*，182
- *样式，在 Linux 控制台显示中更改*，237
- *制表符，转换为空格*，182
- *下划线，Linux 控制台*，237
- *不可打印字符，显示*，222
- *大写，转换为*，29

## 文本对话框
- 创建，244
- `--textbox` 选项，dialog 命令，244

## 文本流
- 170

## 基于文本的脚本
*参见* 控制台脚本

## time 命令
- 134–136, 142–143
- time 对话框，创建，244
- `--timebox` 选项，dialog 命令，244

## TIMEFORMAT 变量
- 85

## 脚本计时
- 134–136, 142–143

## TMOUT 变量
- 85

## total 选项
- id 命令，325

## touch 命令
- 173

## tr (terminal put) 命令
- 238

## tr (translate) 命令
- 29, 217–218, 231

## 转录
- 创建，133

## 传输文件
- 177–179

## trap 命令
- 128, 161–162

## 陷阱
- 161–162

## true 命令
- *创建无限循环*，120
  - *状态代码*，116

## 截断文件
- 171

## tty 命令
- 12, 234

## 开启/关闭
- *脚本中的别名*，36
- *属性*，73
- *Bash 命令选项*，63–64
- *命令历史记录*，21
- *键盘 LED 灯*，235
- *-r (只读)* 属性，74

## type 命令
- 62, 171, 198
- `-type f` 选项，find 命令，211
- `-type` 选项，find 命令，211

## U

## -u (-shell) 选项
- getopt 命令，154

## -u (unbind) 选项
- bind 命令，41

## -u (unset) 选项
- shopt 命令，64

## -u (update) 选项
- 34

## -u (user) 权限
- 271

## -u (-user) 选项
- id 命令，269

## -u 选项
- renice 命令，164

## UDP (用户数据报协议)
- 套接字，282

## uid (用户 ID 号)
- 267

## UID 变量
- 85

## uicolor 选项
- setterm 命令，237

## ulimit 命令
- 275~276, 279

## umask 命令
- 273~274

## unalias 命令
- 36

## 下划线文本
- Linux 控制台，237

## unexpand 命令
- 182, 203

## UNICODE 模式
参见 UTF-8 模式

## unset 命令
- 数组，删除值，76
- 变量，69

## unshar 命令
- 141

## until 循环
- 120

## 上箭头 (`^`) 快速替换历史命令
- 21

## update 命令
- 131
- `-update` 选项，tar 命令，225

## updatedb 命令
- 210

## 更新
- 本地化数据库，324
- 仓库，131

## 大写文本
- 转换为消息，29

## use-compress-program 选项
- tar 命令，224

## user username 选项
- psql 命令，313

## USER 变量
- 86

## user=username 选项
- mysql 命令，316

## users 命令
- 35

## UTF-8 模式（控制台输入模式）
- 235

## 实用程序
- 14

## V

## -v (`-invert-match`) 选项
- grep 命令，209

## -v (variables) 选项
- bind 命令，41

## -v (`-verbose`) 选项
- chown 命令，270
- FTP 命令，177
- sftp 命令，179
- tar 命令，224~225
- time 命令，136, 142
- wget 命令，177

## -v 选项
- 23
- command 命令，62
- host 命令，282
- join 命令，196
- killall 命令，164

## 变量文本匹配展开
- 107

## 变量长度展开
- 106

## 变量名匹配展开
- 106

## 变量
- `-`（空闲），88
- 算术测试，100~101
- 赋值，17

### 属性
- 数组，76
- 显示，74
- 整型变量，73~74
- Linux，77
- 开启/关闭，73

- auto\_resume, 82
- BASH, 69, 82
- BASH\_ENV, 69, 82
- BASH\_VERSION, 82
- BASH\_VERSION, 69, 82
- C 程序变量，共享，331~332
- CDPATH, 22, 83
- CGI 环境，288~289, 298
- COLUMNS, 69, 83
- 命令，将结果赋值给，18, 69
- COMPWORLD, 83
- COMPWORD, 83
- COMPPOINT, 83
- COMPRPROMPT, 83
- 构成要素，创建，74
- COUNT, 154
- 创建，17, 68
- CVSROOT, 85
- 声明，67
- DIRSTACK, 83
- DISPLAY, 70, 85
- EDITOR, 70, 85
- 环境，77~78, 250, 254
- \_ETC\_PROFILE, 85
- EUID, 83
- 导出，76
- FCEDIT, 83
- FIGnore, 83
- 标志，92
- 表单变量，显示，290–293
- FUNCNAME, 69, 83
- GETOPT_COMPATIBLE, 152
- GLOBIGNORE, 83, 104
- GROUPS, 83
- histchars, 83
- HISTCMD, 83
- HISTCONTROL, 83
- HISTFILE, 83
- HISTFILESIZE, 83
- HISTIGNORE, 83
- HISTSIZE, 83
- HOME, 69, 83
- HOST, 85
- HOSTNAME, 69, 83
- HOSTTYPE, 69, 83
- IFS (内部字段分隔符), 69, 73, 84
- IGNOREEOF, 84
- INPUTRC, 84–85
- 整型，属性，73–74
- ITEM, 302
- KDEDIR, 85
- LANG, 84
- LC_ALL, 84
- LC_COLLATE, 84, 323–324
- LC_CTYPE, 84, 323
- LC_MESSAGES, 84, 324
- LC_MONETARY, 323
- LC_NUMERIC, 323
- LC_TIME, 324
- LESS, 85
- LESSCHARSET, 85
- LESSOPEN, 85
- LINEO, 69, 84
- LINES, 69, 84
- local, 261–263
- LOGNAME, 85
- LS_COLORS, 85
- MACHYTYPE, 84
- MAIL, 84
- MAILCHECK, 84
- MAILPATH, 84
- 多个，赋值，38
- 命名，67
- NEXTITEM, 302
- OLDPWD, 22, 84
- OPSTRING, 148–150
- OPTARG, 85, 149
- OPTERR, 84, 149
- OPTIND, 85, 149
- ORGANIZATION, 70, 85
- OSTYPE, 70, 84
- PAGER, 86
- PATH, 70, 84
- PIPESTATUS, 84
- PPID, 70, 84
- 预定义变量，列表，69
- PRINTER, 86
- PROMPT_COMMAND, 70, 84
- PS1 (提示字符串 1), 37, 70, 84
- PS2 (提示字符串 2), 38, 70, 84
- PS3 (提示字符串 3), 70, 84
- PS4 (提示字符串 4), 70, 85
- PWD, 70, 85
- QTDIR, 86
- RANDOM, 70, 85
- SECONDS, 85
- SHELL, 70, 85
- SHELLOPTS, 85
- SHVL_, 85
- 替换
  - `$$` 函数，80
  - eval 命令，79
- SWITCH, 149
- TEMPIRD, 86
- TERM, 70, 86
- TIMEFORMAT, 85
- TMOUT, 85
- UID, 85
- USER, 86
- 值，18
  - 赋值，68
  - 打印，17
- VISUAL, 70, 86
- WINDOWMANAGER, 70, 86
- 单词分割，70–73





## 验证
- 命令编辑模式，15
- 文件，179-180

## 版本控制系统
参见 CVS

- vi 编辑模式（命令），15-17
- 查看第 N 个（-N）开关，23

## 查看
- 命令功能摘要，31
- 目录，21
- 文件通用信息，174
- 任务 PID，158
- 键盘选项，41
- 宏，42
- 运行脚本，134
- 已保存的目录，23
- 特定键盘功能，40
- 陷阱，162
- 变量属性，74
- 虚拟控制台，233
- VISUAL 变量，70、86

## W
- -w (--width=n) 开关，fold 命令，195
- -w (--words) 开关，wc 命令，191
- -W (words) 开关，compgen 命令，322
- w (写) 权限，271
- w 命令，35
- -w 开关，history 命令，21
- --warn 开关，mfdsum 命令，180
- watch 命令，134
- wc (word count) 命令，191、204

## Web 浏览器
- lynx，294-297
- 打开连接，283-284

### 网页剥离，294-297

## Web 服务器
- CGI 环境变量，288-289、298
- CGI 脚本，284-285
- 显示表单变量，290-293
- 错误消息，285-287
- 表单输入标签，289

### weease 键，vi 编辑模式功能，17

### wget (web get)，177、200-202

### while 循环，119-120

- who 命令，35
- WINDOWMANAGER 变量，70、86
- wipe 命令，278-280
- 单词指示符，320-329、335
- 单词拆分，70-73
- 工作目录。参见当前目录
- 包装程序，274
- 文件行换行，195

### 写访问（目录），268

## 编写
- 持续执行脚本，256-259
- 文件，188
- 通过 crontab 命令运行定期脚本，254-256

## X - Y - Z
- x (执行) 权限，272
- X Windows，8
- x-www-form-urlencoded 编码（表单），289
- XLATE 模式。参见 ASCII 模式

## y
- y (转换) 命令，222
- yesno 对话框，创建，240
- --yesno 开关，dialog 命令，240

- -Z (--compress) 开关，tar 命令，224
- -z (compressed) 开关，file 命令，172
- -z (--elide-empty-files) 开关，csplit 命令，181
- -z (--gzip) 开关，tar 命令，224
- -z (zero length) 开关，92
- -z 开关，wipe 命令，278

