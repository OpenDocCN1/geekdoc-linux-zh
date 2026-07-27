# Linux 系统命令：终极手册









https://archive.org/details/linuxsystemcomma0000volk
























IDG 是全球领先的 IT 媒体、研究和展会公司。IDG 成立于 1964 年，在 1997 年合并了价值 25 亿美元的业务，拥有 9000 多名员工：IDG 提供了最广泛的媒体选择，覆盖 75 个国家的 IT 买家，占全球 IT 市场的 95%。IDG 的多样化产品和服务涵盖了印刷出版、在线出版、展会和会议、市场研究、教育和培训等关键领域。凭借全球营销影响力，我们每月通过杂志和报纸接触 5 亿读者。IDG 的领先品牌包括 PC World、Worldmarket 和 Channel 系列出版。IDG Books Worldwide 是历史上增长最快的图书出版商之一，通过在线和纸质触达全球读者。IDG 为在线用户提供互联网（http://www.idg.net），该网站与全球 55 个国家的 225 多个目标网站相竞争。国际数据公司（DCI）为全球 41 多个国家的决策者和全球 400 多名研究人员提供市场数据和分析。IDG World 是 35 个国家举办的 168 多场全球会议和展览的领先制作者，包括 E3（电子娱乐博览会）、Macworld、ComNet、Windows Expo、ICE（互联网连接博览会）、Agenda、DEMO、JPOW 等。IDG Training 是领先的提供商，在全球 230 多个地点设有培训中心，提供 785 门培训课程。IDG Marketing 通过 IDG 全球的印刷、在线和曝光开发整合营销计划，帮助领先的 IT 公司建立国际品牌知名度。有关公司的更多信息请访问 www.idg.com。



# 鸣谢




Amy Eoff

Linda Marousek





York Production Services
封面设计

# 关于作者
Patrick Volkerding 是广誉的 Linux 发行版 Slack 的创始人。他与 Kevin Reichard 合作编写了《Linux 配置与安装》，该书已出版第四版。



本书面向各种类型的 Linux 用户：

- 想要在办公室或家里使用 UNIX 版本的程序员
- 想要一个拥有本地和互联网所需所有工具的稳定操作系统的终端用户
- 想要了解更多关于先进操作系统的学生
无论你是谁，你都会非常喜欢使用 Linux 作为操作系统。
# 本书的目的
命令是 Linux 操作系统的核心。许多 Linux 专家倾向于使用命令而不是图形化工具来配置和使用 Linux 系统。既然可以快速输入命令，为什么要等待窗口打开呢？为什么要点击多层菜单呢？
本书的目的是为你提供最常用的 Linux 命令及其许多常用选项的参考。你可以把这本书看作是写作时的字典，或者是修理汽车时的维修手册。当你需要提醒自己如何使用工具让你的 Linux 系统按你的预期工作时，请翻开本书。
# Linux 简史
Linux 起于芬兰赫尔辛基大学的一个小型学生项目。Linux Torvalds 想要一个小型类 UNIX 操作系统，于是他开始编写。他得到了来自全球志愿者的帮助，他们通过公告板、电子邮件和互联网协作创建了 Linux 操作系统。
该团队最终创建了一个非常卓越的操作系统，它运行良好、非常稳定，并且与微软、苹果和太阳公司的产品相竞争。Linux 提供了以下特性：
- **多任务** —— Linux 以类 UNIX 的方式原生同时运行多个任务（程序）。它还支持抢占式多任务，允许为不同的进程设置优先级。
- **用户友好** —— X Window 系统界面和一系列优秀的工具让 Linux 变得易于使用。
今天，Linux 拥有数百万用户，而且数字每天都在增长。Linux 受欢迎的原因之一是成本。Linux 本身免费的。许多 Linux 书籍附带免费的 Linux CD，因此你只需买书就能获得一个功能全且强大的操作系统。即使是像 Slackware Linux 和 Red Hat Linux 等发行版使用不同的安装过程，通常也有不同的管理工具。
# 获取 Linux
本书不包含含有 Linux 的 CD。然而，我们强烈建议你查看 M&T Books Slack 系列中的其他书籍，所有这些书籍都附带了包含 Slack Linux 的 CD。
# 自由软件基金会
Linux 是许多热诚志愿者的产物，其中许多人还把时间给了自由软件基金会（FSF）。FSF 是一个由 Richard Stallman 领导的理想集团，他的信念是所有软件应该是自由的。为了支持这一信念，他们直接或在 GNU 许可证的支持下向世界发布了许多实用软件。
结果是大量的 GNU 命令被整合到 Linux 中。我们在书中用图标标记了它们。GNU 命令通常是最受欢迎的 UNIX 命令的克隆。它们的创建方式避开了 UNIX 的许可限制。因此，它们非常有用，并且通常运行良好。
你可以通过以下方式联系自由软件基金会：
1-617-542-2652（传真）
http://www.gnu.org/
# 本书使用的规范
对于本书第 5 至 11 章列出的命令，我们采用了一致的方法。我们认为这种一致性将帮助你扩展对 Linux 的使用并掌握新的命令和概念。所有命令都以相同的方式设置，由以下部分组成：
- 标题，示例命令行用法
- 最常用的命令行选项列表
- 实际使用的示例（适用于大多数命令，但并非所有）


- 选项在不作为整个命令行的一部分呈现时，使用等宽字体列出。
- 新概念用*斜体*文本标记。
书中使用了以下图标：
# X Window 系统命令
此特殊图标用于指示该命令是 X Window 系统命令。
# GNU 命令
此特殊图标用于指示该命令是 GNU 命令。
### 交叉引用
此图标用于引用书中其他部分的材料，以及可以在在线手册页上找到的信息。
### 注意
此图标告诉你是重要内容。例如，它可以是一个帮助你掌握当前任务的概念，或者是理解后续材料的基础性内容。
> 提示 此图标表示一种更高效的方法，或一种可能不显而的技术。
# 联系我们
我们希望收到你的反馈。在你在使用本书后，请花时间在 http://mycents.com 注册（详情见书末的 mycents 页）。你可以通过电子邮件联系我们：reichard@mr.net 由于邮件量，我们无法保证立即回复。你也可以访问我们的网站。Slackware 网站：www.slackware.com Reichard 网站：www.reichard.com
# 简要目录
前言 . . . . . . . . . . . . . . . . . . . . . . . . vii
## 第一部分：Linux 操作 . . . . . . . . . . . . . . . . . 2
- 第 1 章：Linux 结构与命令 ................................. . 5
- 第 3 章：Linux/DOS 交叉引用 . . . . . . . . . . . . . . . 33


- 第 6 章：文件管理命令 . . . . . . . . . . . . . . . . . . 191
- 第 8 章：互联网/电子邮件命令 . . . . . . . 311
- 第 10 章：网络命令 . . . . . . . . . . . . . . . . . . . 395






- 第一部分：剖析 Linux 操作 . . . . . . . .2
  命令行 ...................................................................................................6
  目录 ...............................................................................................................10
  参数 ...................................................................................................................14
  X Window 系统命令行选项 .................................................15
- 第三章：Linux/DOS 交叉引用 ..............................................33
- 第二部分：命令篇 . . . . . . . . . . . . .................56
- 第六章：文件管理命令 .......................................191
- 第八章：互联网/电子邮件命令 .......................311
- 第十章：网络命令 ........................................395
- 第十一章：Mtools 命令 ................................................... 419
- 第三部分：通过 Linux Shell 交互 . . . . . . . . . .428
  Shell 类型 ................................................................................................... 431
- 索引 ................................................................................................................ 437
# Linux® 系统命令
Patrick Volkerding

IDG Books Worldwide, Inc. 旗下
加州福斯特市 • 伊利诺伊州芝加哥 • 印第安纳州印第安波利斯 • 纽约州纽约
# 剖析 Linux 操作
在使用任何操作系统时，一个令人沮丧的方面就是，当你缺乏必要的知识，无法在一个不熟悉的操作系统上实现你的需求时。这就是为什么我们在本书的开头安排了四个章节来剖析某些特定的 Linux 操作。每一章在你的 Linux 使用中都扮演着特定的角色，从第 1 章的 Linux 介绍，到第 2、3、4 章的特定参考工作。
我们为什么要包含一个 DOS 参考章节呢？DOS 已经过时了吗？DOS 仍然是 Windows 95/98 的基础，如果你是一个高级用户，你可能大部分工作都是使用 DOS 命令而不是图形界面。如果你有 DOS 经验并想了解 Linux 中类似的工具，那么第 3 章就是为你为你准备的。
- **第一章** Linux 结构与命令
- **第三章** Linux/DOS 交叉引用




- 即使是 GUI 程序也更像工具而不是完整的应用程序。即使你在使用 XFree86（X Window 系统的 Linux 版本，这是 UNIX 世界中流行的图形界面）时，你基本上仍然在使用一组小型且易于使用的命令。
由于 Linux 的核心是它的命令，任何想要精通 Linux 的人都应该渴望首先掌握它的命令结构。这正是本书的作用：《Linux 系统命令》是 Linux 命令结构的列表。但在使用这些命令之前，你需要了解 Linux 是如何处理命令的，以及如何将这些命令输入系统。
# 命令行
正如前面提到的，Linux 是一个命令行驱动的操作系统。命令是通过命令行给操作系统的。当你看到以下内容时，你知道 Linux 准备好接受命令了：
$
对于 root 用户（也称为超级用户），默认情况如下：
当你运行终端模式时，提示符可能会出现在全屏中，也可能出现在窗口中，如图 1 所示。美元符号被称为提示符，它是 Linux 用来告诉你它已准备好接受命令的机制。在提示符处，你可以输入单个命令或命令与选项的组合，其和被称为命令。命令本身就是它的意思。无论你在提示符处输入什么，Linux 都会将其解释为命令或执行某事的指令。你可以直接使用命令执行某些操作，例如移动和复制文件。你还可以使用命令运行其他程序，例如 elvis 或 emacs。Linux 有一套特定的命令，所以如果你输入的内容不符合其中任何一个命令，它会告诉你找不到该命令。（实际上，当你查看目录时可以看到命令列表，但我们操得太急了。）操作系统中有数百计的命令。
# 第一章：Linux 结构与命令
![图 1-1 在 X Window 系统中运行的 Xterm。]
命令拥有选项，用于更好地指定命令的行为。这些选项可以告诉命令仅在特定情况下执行操作。通过一个通用命令及其某些选项可以最好地看到这一点。`ls` 命令是最基础且最常用的命令之一。它本身运行时，仅仅是列出给定目录中的文件，如图 1-2 所示。
![图 1-2 单独使用 ls 命令列出给定目录中的文件。]
该图向我们展示了这个特定目录包含一组目录。（本章中的文件和目录名称并不重要；你只需要知道识别这些文件和目录的机制，以及它们如何应用于几乎任何命令。）然而，该命令本身仅指所有用户可访问且未以某种方式隐藏的文件。隐藏文件以点（.）开头，因此你需要告诉 `ls` 命令查找所有文件，包括隐藏文件。这是通过选项 `-a` 实现的
`ls` 命令的一个选项，可以为你提供所有文件和目录的列表，包括隐藏文件，如图 1-3 所示。
![](img/2cc16c5632743593217f446101e4719f_23_0.png)
图 1-3 `ls` 命令的 `-l` 选项
进一步以这个例子，你可以要求 `ls` 命令使用 `-l`（字母 l，而不是数字 1）选项返回当前目录中文件或目录的详细列表，如图 1-4 所示。
![](img/2cc16c5632743593217f446101e4719f_23_1.png)
图 1-4 `ls` 命令的 `-l` 选项
极少有 Linux 命令不具备某种形式的选项或参数。
> 交叉引用







-   **目录（Directories）**：表示关于其他文件信息的文件。Linux 操作系统中的文件是分层存储的，文件存储在其他文件的集合之中。目录将在下一节中解释。（在 X Windows 系统中，目录通常表示为文件夹。）
-   **链接（Links）**：文件系统中表示同一个文件的多个名称。链接对于从几个不同的目录表示同一个命令或使用不同的名称来说特别有价值。不创建相同文件的多个副本可以节省磁盘空间。
## 目录
正如你之前看到的，目录仅仅是用于存储其他文件的文件。对于像 Linux 这样的操作系统来说，目录是必不可少的。在 Linux 中，每个命令都是文件，每个设备都是文件，每个程序至少是一个文件（但通常更多）。将所有这些文件加起来，你最终会得到一个混乱混乱的文件系统，其中有数千个独立文件。更糟糕的是，Linux 设计是用于在网络上的，这意味着每个用户都可以访问跨网络以及可能的文件服务器上的数千个其他文件。如果这些文件不能存储在某种层次结构中，跟踪这些文件将是不可能的。这就是目录大显身场的地方。
Linux 中的目录层次结构（你可以将其想象成金字塔）实际上非常简单。有一个根目录，位于金字塔的顶端，用斜杠（`/`）表示。每个目录都是根目录的子目录。此外，子目录中还有子目录。Linux 中的目录层次结构（你可以视化为金字塔）实际上非常简单。有一个根目录，位于金字塔的顶端，用斜杠（`/`）表示。每个目录都是根目录的子目录。此外，子目录中还有子目录。Linux 中的目录层次结构（你可以视化为金字塔）实际上非常简单。有一个根目录，位于金字塔的顶端，用斜杠（`/`）表示。每个目录都是根目录的子目录。此外，子目录中还有子目录。Linux 中的目录层次结构（你可以视化为金字塔）实际上非常简单。
，，，，重复））
如图 1-3 所示。
![](img/2cc16c5632743593217f446101e4719f_23_0.png)
图 1-3 `ls` 命令的 `-l` 选项
如图 1-4 所示。
![](img/2cc16c5632743593217f446101e4719f_23_1.png)
图 1-4 `ls` 命令的 `-l` 选项
> 交叉引用







-   **目录（Directories）**：表示关于其他文件信息的文件。Linux 操作系统中的文件是分层存储的，文件存储在其他文件的集合之中。目录将在下一节中解释。（在 X Windows 系统中，目录通常表示为文件夹。）
-   **链接（Links）**：文件系统中表示同一个文件的多个名称。链接对于从几个不同的目录表示同一个命令或使用不同的名称来说特别有价值。不创建相同文件的多个副本可以节省磁盘空间。
## 目录
正如你之前看到的，目录仅仅是用于存储其他文件的文件。对于像 Linux 这样的操作系统来说，目录是必不可少的。在 Linux 中，每个命令都是文件，每个设备都是文件，每个程序至少是一个文件（但通常更多）。将所有这些文件加起来，你最终会得到一个混乱混乱的文件系统，其中有数千个独立文件。更糟糕的是，Linux 设计是用于在网络上的，这意味着每个用户都可以访问跨网络以及可能的文件服务器上的数千个其他文件。如果这些文件不能存储在某种层次结构中，跟踪这些文件将是不可能的。这就是目录大显身场的地方。
Linux 中的目录层次结构（你可以将其想象成金字塔）实际上非常简单。有一个根目录，位于金字塔的顶端，用斜杠（`/`）表示。每个目录都是根目录的子目录。此外，子目录中还有子目录。
## 标准输入输出和重定向
下一个 Linux 谜题涉及到链接命令和文件的*标准输入输出（I/O）*。不要被这个技术术语吓到：标准 I/O 实际上涉及到命令行是如何构造的，以及输出输出。
Linux 就像所有其他操作系统一样，它需要知道输入从哪里来以及输出应该发送到哪里。其他操作系统，如 Windows 和 Macintosh，在输入输出方面会做出假设。Linux 如此，在某些情况下，但在大多数情况下你对对工作的来源和去向进行一些思考。
`cat` 命令功能极其强大。它可以显示文件内容、向文件添加内容以及更多。在单独于命令行运行时，它也可以作为一种原始的文本编辑器使用：
```
```
光标将进入下一行，然后你可以输入文本。因为你没有指定文本应该去哪里，Linux 和 `cat` 命令假设输入到屏幕上，它将永远丢失，因为没有将文本保存到磁盘的机制。大多数 Linux 命令假设标准输入来自键盘，而标准输出显示在终端。在这种情况下，`cat` 可以提高你的打字技巧，但在其他情况下几乎没用。
然而，当你与文件名结合时，`cat` 的实用性会增加。结合 `cat` 和文件名会将现有文件显示在屏幕上，如图 1-6 所示。
![](img/2cc16c5632743593217f446101e4719f_26_0.png)
图 1-6 文件结合 cat
而不是使用来自键盘的标准输入，`cat` 使用来自文件的标准输入。文件的内容没有被更改；它们只是被显示在屏幕上。
你可以通过红色符号使用 `cat` 将按键存储到文件中。这些符号是操作系统的组成部分，用于修改标准输入输出。你可以将 `cat` —— 或者任何其他 Linux 命令与红色符号结合，以将其输出重定向到文件。在下面的示例中，`cat` 的输出（通常发送到屏幕）被重定向到文件 `kevin.report`。
```
```

# 第一章：Linux 结构与命令
输出会按键逐次发送到文件 `kevin.report`。输入 Ctrl-D 可停止重定向并结束 `cat` 命令。
重定向既可用于输入也可用于输出。可以通过以下方式告诉 `cat` 命令将一个文件复制到新文件名：
```
```
在这里，输入是 `kevin.report`，输出是 `pat.report`。`kevin.report` 的内容没有任何变化。
另一个重定向符号用于将文本追加到现有文件中。在这里，将 `kevin.report` 的内容追加到名为 `pat.report` 的现有文件中：
```
```
如果你在输入处省略文件名，`cat` 将假设使用按键进行追加。以下命令行允许你直接将按键追加到名为 `kevin.report` 的文件末尾：
```
```
以下是实用的重定向符号：
- > 用于将命令的输出发送到文件或其他命令。例如，`cat > file` 用于将 `cat` 命令的输出发送到 `file`。
- < 用于将文件或命令的输入发送到命令。例如，`cat < file` 意味着 `cat` 将使用 `file` 作为输入。
- >> 用于将输入追加到现有文件。例如，`cat >> file` 告诉 Linux 将按键追加到名为 `file` 的现有文件中。
- | 管道符号，当你运行一个命令并将其输出发送到另一个命令时使用。例如，`cat | grep` 运行 `cat` 命令并将输出发送给 `grep` 命令，然后运行 `grep` 命令。（我们将在下一节之后详细介绍管道。）
## 参数
输入/输出符号似乎提供了几种实现相同功能的方法。确实，取决于命令行的结构，`<` 和 `>` 看起来似乎是可以互换的。然而，这两个符号都是必不可少的。看起来相似的命令行在操作系统的处理上可能大不相同。例如，这条命令行
```
```
功能上等同于
```
```
然而，这两个命令行实际上是不同的。在第一个中，`pat.file` 是 `cat` 命令的一个参数。在 Linux 世界中，参数是变量命令行修饰符；在此实例中，参数恰好是一个文件。在第二个示例中，`pat.file` 是 `cat` 命令的输入。
涉及重定向符号的命令行其复杂性是无限的。在 Shell 脚本中，看到如下使用两个重定向符号的情况并不罕见：
```
```
这告诉 `cat` 使用 `file1` 作为输入，并将输出发送到 `file2`。
## 管道
正如 `|` 所示，管道仅仅是一个额外的重定向工具。它的优势在于可以直接与命令配合工作，告诉一个命令将另一个命令的输出作为输入。其使用方式如下：
```
```
命令与管道符号的组合被称为管道（pipeline）。管道通常用于为打印准备文件。
## X Window 系统命令行选项
X 窗口系统命令贯穿第 5 章到第 11 章。这些命令共享一组公共命令行选项。为了避免在每个命令中都列出这些选项，它们被列在表 1-1 中。
表 1-1 窗口命令行选项
| 选项 | 用途 |
| -background red green blue | 将背景颜色设置为红、绿、蓝。 |
| -bg color | 使用颜色作为窗口背景。 |
| -fg color | 使用颜色作为窗口前景。 |
| -font font | 使用指定的字体名称。 |
| -foreground color | 使用颜色作为窗口前景。 |
| -geometry WidthxHeight | 设置窗口大小。 |
| -height rows | 以行为单位设置基础窗口的高度。 |
| -reverse | 反转前景和背景颜色。 |
## 第一部分：阐明 Linux 过程
| 选项 | 用途 |
| -rv | 反转前景和背景颜色。 |
| -Wb red green blue | 将背景颜色设置为红、绿、蓝。 |
| -WG WidthHeight+x+y | 设置窗口大小（WidthHeight）和位置（x+y）。 |
| -WG +x+y | 以 x y 像素为单位设置窗口左上角的位置。 |
| -Wi | 将窗口作为图标而非完整窗口启动。 |
| -Wi x y | 以 x y 像素为单位设置窗口左上角的位置。 |
| -Ws width height | 以宽 x 高像素单位设置窗口大小。 |
| -Ww columns | 以列为单位设置基础窗口的宽度。 |

# 第 2 章：揭秘 Linux 命令
## 如果你想...
## 请使用此 Linux 命令...
- 收听音频 CD
- 刻录 CD
- 查看日历
- 列出正在的客户端应用程序
- 显示时钟
- 显示默认颜色映射表
- 切割列、字节或字符
- 合并文件
- 在特定时间运行命令
- 比较文件
- 比较排序后的文件
- 比较三个文本文件
- 编译 Fortran 程序
- 压缩文件
- 转换并复制文件
- mkisofs, mkhybrid
- bc, dc, xcalc
- clear
- xclipboard
- showrgb
- xstdcmap
- column
- dircolors
- xargs
- zcmp, zdiff
- diff, diff3, sdiff
- gcc, g++
- gzexe
- minicom, seyon




| :--- | :--- |
| 统计字数、行和字节 | wc |
| 修改系统日期 | date |
| 解码 uuenoded 文件 | udecode |
| 删除目录 | rmdir |
| 创建目录 | mkdir |
| 列出磁盘剩余空间 | df |
| 查看 X 显示信息 | xdpyinfo |
| 显示域名 | dnsdomainname |
| 将 DOS 文件转换为 Linux 文件 | fromdos |
| 编辑文本文件 | ed, elvis, emacs, joe, jove, vi, vim, xedit |
| 创建电子邮件 | elm, mail, mailx, metasend, pine |
| 收到的电子邮件通知 | biff, newmail, xbiff, wnewmail, metasend |
| 打印电子邮件 | printmail |
| 通过电子邮件回复 | Rnmail |
# 第 2 章：揭秘 Linux 命令
## 如果你想...
## 请使用此 Linux 命令...
- 从服务器获取电子邮件 | fetchmail
- 从电子邮件中分离 MIME 内容 | splitmail |
- 显示文件的最后 10 行 | tail |
- 返回环境变量 | printenv |
- 查看 X 事件信息 | xev |
- 计算用于验证文件的字节数 | cksum |
- 创建 Linux 交换区 | mkswap |
- 查找文件 | find |
- 返回 finger 信息 | finger |
- 查看字体服务器信息 | fsinfo |
- 格式化文本文件 | fmt, groff
- 生成分形 | xfractint
- 编辑图形 | gimp, xv
- 修改当前组权限 | newgrp |
## 第一部分：阐明 Linux 详解
## 如果你想...
## 请使用此 Linux 命令...
- 创建新组 | groupadd |
- apropos, info, man, whatis,
- 修改 HFS 工作目录 | hcd |
- 删除 HFS 文件的两个分支 | hdel |
- 创建 HFS 文件系统 | hformat |
- 创建新的 HFS 目录 | hmkdir |
- 打印 HFS 工作目录的完整路径 | hpwd |
- 删除空的 HFS 目录 | hrmdir |
- 显示或更改当前的 HFS 卷 | hvol |
- 启动操作 HFS 卷的 X shell | xhfs |
- 显示主机名 | hostname |
- 编辑图像 | gimp, xv
- 安装 Slackware 软件包 | installpkg |




- 排序文件 | join |
- 显示内核符号 | ksyms |
- 重建内核表 | depmod |
- 返回内核模块信息 | modinfo |
- 修改 X 映射表 | xmodmap
- 查看关键字信息 | whatis |
- 列出文件 | ls |
- 登录系统 | login |
- 修改 HFS (Macintosh) 文件属性 | hattrib |
- 在 HFS (Macintosh) 卷中复制文件 | hcopy |
- 以长格式显示 HFS (Macintosh) 目录 | hdir |
- 列出 HFS (Macintosh) 目录中的文件 | hls |
## 第一部分：阐明 Linux 详解
## 如果你想...
## 请使用此 Linux 命令...
- 创建新的 HFS (Macintosh) 目录 | hmkdir |
- 打印 HFS (Macintosh) 工作目录的完整路径 | hpwd |
- 删除空的 HFS (Macintosh) 目录 | hrmdir |
- 显示或更改当前的 HFS (Macintosh) 卷 | hvol |
- 启动操作 HFS (Macintosh) 卷的 X shell | xhfs |
- 编码电子邮件 | mimencode, mmencode |
- 创建多媒体电子邮件 | metasend |
- 读取电子邮件 | elm, mail, mailx, pine, readmsg |
- 从服务器获取电子邮件 | fetchmail |
- 从电子邮件中分离 MIME 内容 | splitmail |
- 显示文件的最后 10 行 | tail |
- 返回环境变量 | printenv |
- 查看 X 事件信息 | xev |
- 计算用于验证文件的字节数 | cksum |
- 创建 Linux 交换区 | mkswap |
- 查找文件 | find |
- 返回 finger 信息 | finger |
- 查看字体服务器信息 | fsinfo |
- 格式化文本文件 | fmt, groff |
- 生成分形 | xfractint |
- 编辑图形 | gimp, xv |
- 修改当前组权限 | newgrp |
- 查看在线帮助 | xman |
- 修改 HFS 文件属性 | hattrib |
- 在 HFS 卷中复制文件 | hcopy |
- 以长格式显示 HFS 目录 | hdir |
- 列出 HFS 目录中的文件 | hls |

## 第一部分：Linux 流程详解
## 如果你想...
## 请使用此 Linux 命令...
- 监控 PCMIA 设备
- 绘制数据
- 打印文件
- 删除打印作业
- 结束进程
- 返回进程 ID
- 显示 X 窗口或字体属性
- 移除文件
- 设置 X 资源数据库
- 反转文件行
- 设置根窗口图像
- 调度任务
- 在 X 中创建截屏
- 搜索文件
- 启动 X 会话管理器
- sxpm
- ghostview, gs
- pr
- ps
- snice
- top
- xrefresh
- rdir
- appres, listres, viewres
- xsetroot
- chroot
- xmag
- xwud, xv
- zgrep, zfgrep, zgrep




- xllperf
- xllperfcomp
- shadowconfig
- chsh
- ash, bash, tcsh, zsh
- shar
- un
- splitvt
- shutdown
- setup
- sort
- ispell
- csplit, split
- xspread, sc
- strace
- tload, xload
- uptime, w
- wish
- rxvt, xterm
- stty, setterm
- latex
- info
- strings
- ftp, tftp, nctftp
- tee
- file
- umount
- uncompress, zcat
- bzip2, gunzip, gzip, zcat
- bzip2, unzip
## 如果你想...
- 监控 UPS
- 创建新用户
- 修改用户账户
- 配置显卡
- 查看压缩文件
- 将文本设置为指定宽度
- 浏览万维网
- 编辑 X 资源
- 通过 xmodem 接收
- 通过 ymodem 接收
- 通过 zmodem 接收

- powerd
- newcomers, useradd, adduser
- usermod
- SuperProbe
- zmore, zcat, zless
- fold
- lynx, netscape
- editres
- rx
- sx
- rb
- sb
- rz
- sz

## Linux/DOS 交叉引用

DOS 和 Linux 的相似性比你想象的要得多——DOS 和 Linux 都源于 UNIX，且在这三个操作系统系统中，命令和文件系统的行为通常是相同的。如果你的背景是 DOS 或 Windows（Windows 本质上是 DOS 的图形界面），你完全可以过渡到 Linux。本章列出了一些常用的 DOS 命令及其对应的 Linux 命令。

## DOS 命令对应表

| DOS 命令 | Linux 对应命令 |
| --- | --- |
| APPEND | 无 |
| ASSIGN | 无 |
| ATTRIB | chmod |
| BACKUP | cpio, tar |
| BREAK | 无 |
| CALL | exec |
| CD | cd |
| CHCP | 无 |
| CHDIR | cd |
| CHKDSK | fsck |
| CHOICE | 无 |
| CLS | clear, reset |
| COMMAND | bash, csh, sh |
| COMP | cmp, diff, diff3, sdiff |
| COPY | cp, cat |
| CTTY | stty |
| DATE | date |
| DBLSPACE | 无 |
| DEFRAG | 无 |
| DEL | rm |
| DELTREE | rmdir, rm |
| DIR | Is |
| DISKCOMP | 无 |
| DISCOPY | dd |
| DOSKEY | history (Korn and bash shells) |
| DOSSHELL | 无 |
| ECHO | echo |
| EDIT | elvis, emacs, joe, jed, jove, pico, vi |
| EXIT | exit |
| EXPAND | gunzip, uncompress, bunzip2 |

## Linux 命令对应表

| DOS 命令 | Linux 对应命令 |
| :--- | :--- |
| FASTHELP | apropos, man, xman, whatis |
| FASTOPEN | 无 |
| FC | cmp, diff, diff3, sdiff |
| FDISK | fdisk |
| FIND | find |
| FOR | for (shell command) |
| FORMAT | mkfs |
| GOTO | goto (C shell) |
| GRAFTABL | 无 |
| GRAPHICS | 无 |
| HELP | apropos, man, whatis |
| IF | if (shell command) |
| INTERLNK | 无 |
| INTERSVR | 无 |
| JOIN | 无 |
| LABEL | 无 |
| LOADFIX | 无 |
| LOADHIGH | 无 (不需要) |
| MEM | free |
| MIRROR | 无 |
| MKDIR | mkdir |
| MODE | stty, seterm |
| MORE | less, more |
| MOVE | mv |
| MSAV | 无 |
| MSBACKUP | cpio, tar |
| MSD | 无 |
| NLSFUNC | 无 |
| PATH | echo $PATH |
| PAUSE | sleep |

| DOS 命令 | Linux 对应命令 |
| --- | --- |
| POWER | 无 |
| PRINT | lpr |
| PROMPT | PS |
| RECOVER | 无 |
| REM | |
| RENAME | mv |
| REPLACE | 无 |
| RESTORE | cpio, tar |
| RMDIR | rmdir |
| SET | export, setenv |
| SETVER | 无 |
| SHARE | 无 |
| SHIFT | shift |
| SMARTDRV | 无 |
| SORT | sort |
| SUBST | 无 |
| SYS | 无 |
| TIME | date |
| TREE | 无 |
| TYPE | cat, less, more |
| UNDELETE | 无 |
| UNFORMAT | 无 |
| VER | uname |
| VERIFY | 无 |
| VOL | 无 |
| VSAF | 无 |
| XCOPY | cp |

## Linux 命令 A Z

这里是第 5 到第 11 章中描述的命令字母顺序列表。此列表并不构成完整的命令集——请查看在线的 man 和 info 页面——但它列出了你可能最常用的命令。

## 元素章节

| 元素 | 章节 |
|---|---|
| actsync | 互联网/电子邮件命令 |
| afpd | 网络命令 |
| agetty | 通用命令 |
| ansi2knr | 编程命令 |
| answer | 互联网/电子邮件命令 |
| appres | 通用命令 |
| apropos | 通用命令 |
| ar | 编程命令 |
| arch | 通用命令 |
| as | 编程命令 |
| ash | 通用命令 |
| atalkd | 网络命令 |
| atbm | 通用命令 |
| audiocompose | 互联网/电子邮件命令 |
| audiosend | 互联网/电子邮件命令 |
| banner | 通用命令 |
| basename | 文件管理命令 |
| bash | 通用命令 |
| bc | 通用命令 |
| bdftopcf | 通用命令 |
| biff | 互联网/电子邮件命令 |
| bison | 编程命令 |
| bitmap | 通用命令 |
| bmtoa | 通用命令 |
| bootpd | 网络命令 |
| boottest | 网络命令 |
| bpe | 文本处理命令 |
| bzip2 | 文件管理命令 |
| cal | 通用命令 |



## 元素
# 章节

| 元素 | 章节 |
| :--- | :--- |
| cat | 文本处理命令 |
| cc | 编程命令 |
| cd | 文件管理命令 |
| cdrecord | 通用命令 |
| cdwrite | 通用命令 |
| checkalias | 互联网/电子邮件命令 |
| checknews | 互联网/电子邮件命令 |
| chfn | 互联网/电子邮件命令 |
| chgrp | 文件管理命令 |
| chmod | 文件管理命令 |
| chown | 文件管理命令 |
| chroot | 文件管理命令 |
| chsh | 通用命令 |
| cksum | 通用命令 |
| clear | 通用命令 |
| cmp | 文本处理命令 |
| colcrt | 通用命令 |
| colrm | 文本处理命令 |
| column | 文本处理命令 |
| comm | 文本处理命令 |
| compress | 文件管理命令 |
| cp | 文件管理命令 |
| cpp | 编程命令 |
| csh | 通用命令 |
| csplit | 文本处理命令 |
| ctags | 编程命令 |
| cut | 文本处理命令 |
| date | 通用命令 |
| dc | 通用命令 |
| 元素 | 章节 |
| :--- | :--- |
| dd | 文件管理命令 |
| diff | 文本处理命令 |
| diff3 | 文本处理命令 |
| dir | 文件管理命令 |
| dcolors | 通用命令 |
| dnsdomainname | 网络命令 |
| dnsquery | 网络命令 |
| dumpkeys | 通用命令 |
| echo | 通用命令 |
| egrep | 文本处理命令 |
| elm | 互联网/电子邮件命令 |
| elvis | 文本处理命令 |
| emacs | 文本处理命令 |
| env | 通用命令 |
| etags | 编程命令 |
| expand | 文本处理命令 |
| fastmail | 互联网/电子邮件命令 |
| faucet | 网络命令 |
| fetchmail | 互联网/电子邮件命令 |
| fgrep | 文本处理命令 |
| file | 文件管理命令 |
| find | 文件管理命令 |
| finger | 互联网/电子邮件命令 |
| flex | 编程命令 |
| fmt | 文本处理命令 |
| fold | 文本处理命令 |
| formail | 互联网/电子邮件命令 |
| frm | 互联网/电子邮件命令 |
| fromdos | 文件管理命令 |

## 元素
# 章节

- fsinfo: 通用命令
- fsls: 通用命令
- fstobdf: 通用命令
- ftp: 互联网/电子邮件命令
- ftpcount: 互联网/电子邮件命令
- funzip: 文件管理命令
- fuser: 网络命令
- g77: 编程命令
- gawk: 编程命令
- gcc: 编程命令
- gdb: 编程命令
- getfilename: 文件管理命令
- getkeycodes: 通用命令
- getlist: 互联网/电子邮件命令
- getpeername: 网络命令
- getty: 通用命令
- gimp: 通用命令
- gnuplot: 通用命令
- gprof: 编程命令
- grep: 文本处理命令
- grovi: 文本处理命令
- groff: 文本处理命令
- groij4: 文本处理命令
- grops: 文本处理命令
- grotty: 文本处理命令
- gs: 文本处理命令
- gunzip: 文件管理命令
- g: 文本处理命令
- gzexe: 文件管理命令 |

| 元素 | 章节 |
| :--- | :--- |
| gzip | 文件管理命令 |
| hattrib | 文件管理命令 |
| hcd | 文件管理命令 |
| hcopy | 文件管理命令 |
| hdel | 文件管理命令 |
| hdir | 文件管理命令 |
| head | 文本处理命令 |
| hformat | 文件管理命令 |
| hfs | 文件管理命令 |
| hls | 文件管理命令 |
| hmount | 文件管理命令 |
| hose | 网络命令 |
| host | 网络命令 |
| hostname | 网络命令 |
| hpwd | 文件管理命令 |
| hname | 文件管理命令 |
| hrmdir | 文件管理命令 |
| humount | 文件管理命令 |
| hvol | 文件管理命令 |
| id | 通用命令 |
| image | 编程命令 |
| info | 通用命令 |
| ispell | 文本处理命令 |
| joe | 文本处理命令 |
| join | 文本处理命令 |
| jove | 文本处理命令 |
| kdb_mode | 通用命令 |
| kill | 通用命令 |
| killall | 通用命令 |

## 元素
# 章节

- latex: 文本处理命令
- less: 文本处理命令
- listres: 通用命令
- In: 文件管理命令
- locate: 文件管理命令
- locateddb: 文件管理命令
- lockfile: 通用命令
- login: 通用命令
- logname: 文本处理命令
- look: 文本处理命令
- lpq: 文本处理命令
- lpr: 文本处理命令
- lprm: 文本处理命令
- ls: 文件管理命令
- lynnx: 互联网/电子邮件命令
- mail: 互联网/电子邮件命令
- mailx: 互联网/电子邮件命令
- make: 编程命令
- makepend: 编程命令
- makestrs: 编程命令
- makewatch: 通用命令
- man: 通用命令
- manpath: 通用命令
- mattrib: Mtools 命令
- mbadblocks: Mtools 命令
- mc: 文件管理命令
- mcd: Mtools 命令
- mcookie: 通用命令
- mcopy: Mtools 命令

## 第一部分：阐明 Linux 过程
## 元素
# 章节

- mdel: Mtools 命令
- mdir: Mtools 命令
- merge: 文件管理命令
- messages: 互联网/电子邮件命令
- metamail: 互联网/电子邮件命令
- metasend: 互联网/电子邮件命令
- mformat: Mtools 命令
- mimencode: 互联网/电子邮件命令
- minicom: 通用命令
- mkdir: 文件管理命令
- mkdirhier: 文件管理命令
- mkdosfs: 文件管理命令
- mkfifo: 文件管理命令
- mkfontdir: 文件管理命令
- mkfs: 文件管理命令
- mkmanifest: 文件管理命令
- mknod: 文件管理命令
- mlabel: Mtools 命令
- mmd: Mtools 命令
- mmencode: 互联网/电子邮件命令
- mmount: Mtools 命令
- mmove: Mtools 命令
- more: 文本处理命令
- mrd: Mtools 命令
- mread: Mtools 命令
- mren: Mtools 命令
- msgfmt: 编程命令
- mtest: Mtools 命令
- mtype: Mtools 命令 |

| 元素 | 章节 |
| :--- | :--- |
| mv | 文件管理命令 |
| mwrite | Mtools 命令 |
| mzip | 通用命令 |
| netstat | 网络命令 |
| newgrp | 文件管理命令 |
| newmail | 互联网/电子邮件命令 |
| newsgroups | 互联网/电子邮件命令 |
| nice | 通用命令 |
| nohup | 通用命令 |
| roff | 文本处理命令 |
| objcopy | 编程命令 |
| oclock | 通用命令 |
| od | 文件管理命令 |
| p2c | 编程命令 |
| passwd | 通用命令 |
| paste | 文本处理命令 |
| pathchk | 通用命令 |
| perl | 编程命令 |
| pico | 文本处理命令 |
| pidof | 通用命令 |
| pine | 互联网/电子邮件命令 |
| ping | 网络命令 |
| pname | 通用命令 |
| Pnews | 互联网/电子邮件命令 |
| popclient | 互联网/电子邮件命令 |
| postnews | 互联网/电子邮件命令 |
| pr | 文本处理命令 |
| printenv | 通用命令 |
| printf | 文本处理命令 |

## 元素
# 章节

- printmail: 互联网/电子邮件命令
- procmail: 互联网/电子邮件命令
- ps: 通用命令
- psbb: 文本处理命令
- pwd: 文件管理命令
- rb: 通用命令
- rclock: 通用命令
- rcp: 网络命令
- rdjpgcom: 通用命令
- readmsg: 互联网/电子邮件命令
- reconfig: 通用命令
- ref: 编程命令
- refer: 文本处理命令
- renice: 通用命令
- reset: 通用命令
- resize: 通用命令
- rev: 文本处理命令
- richtext: 互联网/电子邮件命令
- rlogin: 网络命令
- rm: 文件管理命令
- rmail: 互联网/电子邮件命令
- rmdir: 文件管理命令
- Rnmail: 互联网/电子邮件命令
- rpcgen: 编程命令
- rsh: 网络命令
- rstart: 网络命令
- runscript: 通用命令
- runtime: 通用命令
- rusers: 网络命令



| Element | 章节 |
| --- | --- |
| rwall | 网络命令 |
| rwho | 网络命令 |
| rx | 通用命令 |
| rvxt | 通用命令 |
| rz | 通用命令 |
| sb | 通用命令 |
| script | 通用命令 |
| sdiff | 文本处理命令 |
| sed | 文本处理命令 |
| selection | 文本处理命令 |
| seyon | 通用命令 |
| shar | 通用命令 |
| shelltool | 通用命令 |
| showaudio | 互联网/电子邮件命令 |
| showexternal | 互联网/电子邮件命令 |
| showfont | 通用命令 |
| shownascii | 互联网/电子邮件命令 |
| showpartial | 互联网/电子邮件命令 |
| showpicture | 互联网/电子邮件命令 |
| showrgb | 通用命令 |
| shrinkfile | 文件管理命令 |
| size | 文件管理命令 |
| skill | 通用命令 |
| sleep | 通用命令 |
| sliplogin | 网络命令 |
| smproxy | 通用命令 |
| snice | 通用命令 |
| sockdown | 网络命令 |
| soelim | 文本处理命令 |
| sort | 文本处理命令 |
| split | 文本处理命令 |
| splitmail | 互联网/电子邮件命令 |
| splitvt | 通用命令 |
| sq | 文件管理命令 |
| startx | 通用命令 |
| trace | 通用命令 |
| strings | 通用命令 |
| strings-gnu | 通用命令 |
| strip | 编程命令 |
| stty | 通用命令 |
| su | 通管理命令 |
| sum | 文件管理命令 |
| sunst | 通用命令 |
| sx | 通用命令 |
| sxpm | 通用命令 |
| sz | 通用命令 |
| tac | 文本处理命令 |
| tail | 文本处理命令 |
| talk | 网络命令 |
| tcsh | 通用命令 |
| tee | 通用命令 |
| telnet | 网络命令 |
| test | 文件管理命令 |
| tftp | 互联网/电子邮件命令 |
| tload | 通用命令 |
| top | 通用命令 |
| tr | 文本处理命令 |
| trn | 互联网/电子邮件命令 |
| troff | 文本处理命令 |
| true | 通用命令 |
| ul | 通用命令 |
| unexpand | 文本处理命令 |
| uniq | 文本处理命令 |
| unshar | 通用命令 |
| unsq | 文件管理命令 |
| unzip | 文件管理命令 |
| unziipsfx | 文件管理命令 |
| updateddb | 文件处理命令 |
| uptime | 通用命令 |
| users | 通用命令 |
| uucp | 网络命令 |
| uudecode | 互联网/电子邮件命令 |
| uuencode | 互联网/电子邮件命令 |
| ustat | 互联网/电子邮件命令 |
| uux | 互联网/电子邮件命令 |
| vi | 文本处理命令 |
| viewres | 通用命令 |
| vim | 文本处理命令 |
| vrfy | 互联网/电子邮件命令 |
| w | 通用命令 |
| wc | 文本处理命令 |
| whatis | 通用命令 |
| who | 通用命令 |
| whoami | 通用命令 |
| wish | 通用命令 |
| wnewmail | 互联网/电子邮件命令 |
| workbone | 通用命令 |

## 第一部分：深入明 Linux 程序

| Element | 章节 |
| --- | --- |
| workman | 通用命令 |
| write | 网络命令 |
| x11perf | 通用命令 |
| x11perfcomp | 通用命令 |
| x3270 | 网络命令 |
| xargs | 通用命令 |
| xauth | 通用命令 |
| xdiff | 互联网/电子邮件命令 |
| xcalc | 通用命令 |
| xclipboard | 通用命令 |
| xclock | 通用命令 |
| xmap | 通用命令 |
| xcmsdb | 通用命令 |
| xconsole | 通用命令 |
| xcutsel | 通用命令 |
| xdm | 通用命令 |
| xdpyinfo | 通用命令 |
| xedit | 文本处理命令 |
| xev | 通用命令 |
| xeyes | 通用命令 |
| xf86config | 通用命令 |
| xfd | 通用命令 |
| xfilemanager | 文件管理命令 |
| xfm | 文件管理命令 |
| xfonts | 通用命令 |
| xfractint | 通用命令 |
| xfs | 通用命令 |
| xgc | 通用命令 |
| xgettext | 编程命令 |
| xhfs | 文件管理命令 |
| xhost | 通用命令 |
| xieperf | 通用命令 |
| xinit | 通用命令 |
| xkill | 通用命令 |
| xload | 通用命令 |
| xlock | 通用命令 |
| logo | 通用命令 |
| xlsatoms | 通用命令 |
| xlsclients | 通用命令 |
| xlsfonts | 通用命令 |
| xmag | 通用命令 |
| xman | 通用命令 |
| xmessage | 通用命令 |
| xmh | 互联网/电子邮件命令 |
| xkmf | 编程命令 |
| xmodmap | 通用命令 |
| xon | 通用命令 |
| xpaint | 通用命令 |
| xpmroot | 通用命令 |
| xrdb | 通用命令 |
| xrefresh | 通用命令 |
| xset | 通用命令 |
| xsetroot | 通用命令 |
| xsm | 通用命令 |
| xsmclient | 通用命令 |
| xspread | 通用命令 |
| xstdcmap | 通用命令 |
| xterm | 通用命令 |
| xv | 通用命令 |
| xvidtune | 通用命令 |
| xvpictoppm | 通用命令 |
| xwd | 通用命令 |
| xwininfo | 通用命令 |
| xwud | 通用命令 |
| xxgdb | 编程命令 |
| yacc | 编程命令 |
| yes | 通用命令 |
| ytalk | 网络命令 |
| zcat | 文件管理命令 |
| zcmp | 文本处理命令 |
| zdiff | 文本处理命令 |
| zgrep | 文本处理命令 |
| zfgrep | 文本处理命令 |
| zforce | 文件管理命令 |
| zgrep | 文本处理命令 |
| zmore | 文本处理命令 |
| znew | 文件管理命令 |
| zoo | 文件管理命令 |
| zsh | 通用命令 |

### 命令

本节包含七章，涵盖了主要的 Linux 命令，并按组和功能进行排序。这些章节中介绍的每个命令的格式都是相同的。将给出命令名称，随后是命令行示例以及对命令用途的解释。如果适用，还会提供可用的命令行选项、示例和相关命令。此外，我们还会注明该命令是 GNU 命令还是 X Window 系统命令。

- **第 5 章** 通用命令
- **第 6 章** 文件管理命令
- **第 7 章** 文本处理命令
- **第 8 章** 互联网/电子邮件命令
- **第 9 章** 编程命令
- **第 10 章** 网络命令
- **第 11 章** Mtools 命令



## 通用命令

通用命令用于处理你日常的计算任务。它们是 Linux 操作系统的“主力军”：虽然它们并不华丽，但所有用户都可以访问。在了解它们之后，你会惊讶于自己使用它们的频率竟然如此高。

### agetty 处理登录请求

### agetty 选项(s) 参数

### 目的

agetty 命令是一个专为 Linux 环境和拨号线路优化的 tty 管理包。它打开一个 tty 端口，提示输入用户名，并调用 login 命令。通常情况下，你不会手动调用 agetty；它通常在系统启动时由 `/etc/initab` 文件调用。

## 参数

- baud_rate: 设置一个由逗号分隔开的一个或多个波特率列表；当 agetty 接收到 BREAK 字符时会调用它。
- port: 指定相对于 `/dev` 目录的路径名。
- term: 设置 TERM 变量，覆盖来自 init 的设置。

### 选项

- -f issue_file: 显示 issue_file 而不是默认的 /etc/issue 文件。
- -h: 启用硬件 (RTS/CTS) 流控。默认情况下，agetty 决定是否适合软件 (XON/XOFF) 流控。
- -i: 在写入登录提示符之前禁用传输 /etc/issue 文件。
- -I initstring: 设置发送到 tty 或调制解调器的初始字符串；这可以包含调制解调器初始化字符串。
- -l login_program: 调用 login_program 而不是默认的 /bin/login。
- -L: 强制该线路为本地硬接线串口。
- -m: 从 Hayes 兼容调制解调器发布的 CONNECT 状态消息中检测波特率。
- -n: 不提示用户用户名。它最初被设想为将 Linux 用作公告板系统 (BBS) 使用的工具；然而，在如今安全意识提高的今天，此选项可能被认为是相当危险的。
- -t timeout: 如果无法读取用户名，则在 timeout 秒后超时。
- -w: 在发送 /etc/issue 文件和登录提示符之前等待用户发送回车符或换行符。通常与 -I 选项配合使用。

### 相关命令

- getty
- stty
- tty

| appres 列出 X 资源 (X窗口系统命令) | appres class toolkitoptions |

### 目的

appres 命令列出应用程序指定的 X 资源。你可以指定一个通用应用程序，也可以指定一个特定的部件。

> 提示 输出可能非常多，因此你可能想将输出通过到另一个文件中。

### 示例

```
$ appres XTerm
*mainMenu*interrupt*Label: Send INT Signal
*mailMenu*logging*Label: Log to File
*mainMenu*quit*Label: Quit
...
```

### 相关命令

- - listres
- xrddb

### 目的

apropos 命令在 whatis 数据库中搜索有关指定关键词的信息，并在默认编辑器中返回这些信息。whatis 数据库包含命令的短文本摘要。

### 示例

```
$ apropos xterm
xterm (lx) - X 终端模拟器
```

### 相关命令

- - man
- whatis
- xman

### arch 返回机器架构 arch

### 目的

arch 命令列出运行 Linux 的 PC 机器架构。这可以是 i386、i486 或 i586（针对基于 Pentium 的 PC）。

### 示例

```
$ arch
i586
```

### 相关命令

uname

### ash 启动 Ash Shell ash

### 目的

ash 命令启动 ash shell，它是许多 Linux 命令行 shell 之一。

> 交叉引用
有关 shell 的更多信息，请参阅第 12 章。

### atobm 转换位图图像

### atobm 选项(s)
filename

### 目的

atobm 命令将 ASCII 字符串转换为位图文件。关于 X窗口系统位图文件的更多解释，请参见 bitmap 命令。

### 选项

- -chars cc 设置用于指定构成位图文件的 0 和 1 的字符。默认是使用破折号 (-) 表示 0，使用井号 (#) 表示 1。
- -name variable 设置在写入转换后的位图文件名时使用的变量名。默认使用 filename 命令行参数的基名。
- -xhot number: 设置“热点” X 坐标。
- -yhot number: 设置“热点” Y 坐标。

### 相关命令

- bitmap
- bmtoa

### banner 打印横幅

### banner 消息 message

### 目的

banner 命令使用星号打印字符字符串横幅。横幅的总宽度为 132 个字符，横幅是侧向打印的。如果没有给出字符字符串，将提示你输入一个字符串。

你可以使用 -wn 选项更改横幅宽度，其中 n 被替换为横幅的字符宽度。（此命令以前很流行，当时输出可以重定向到可以在纸卷上打印的打字机。）

### 选项

- -w num 将横幅宽度设置为 *num* 个字符。

### 示例

```
$ banner kevin
```

### 目的

bash 命令启动 Bourne Again SHell，它是流行的 UNIX Bourne shell 的克隆版本。

> 交叉引用
有关 bash 的更多细节，请参阅第 12 章。输入 man bash 查看 bash 手册页。

### 目的

bc 命令充当在线计算器和工具。

> 交叉引用
有关 bash 的更多细节，请参阅第 12 章。输入 man bash 查看 bash 手册页。

### 目的

bc 命令作为在线计算器和工具。

> 交叉引用
有关 bash 的更多细节，请参阅第 12 章。输入 man bash 查看 bash 手册页。

### 目的

bc 命令充当在线计算器和工具。

> 交叉引用
有关 bash 的更多细节，请参阅第 12 章。输入 man bash 查看 bash 手册页。

### 目的

bc 命令充当在线计算器和工具。

> 交叉引用
有关 bash 的更多细节，请参阅第 12 章。输入 man bash 查看 bash 手册页。

### 目的

bc 命令充当在线计算器和工具。

> 交叉引用
有关 bash 的更多细节，请参阅第 12 章。输入 man bash 查看 bash 手册页。

### 目的

bc 命令充当在线计算器和工具。

> 交叉引用
有关 bash 的更多细节，请参阅第 12 章。输入 man bash 查看 bash 手册页。

### 目的

bc 命令充当在线计算器和工具。

> 交叉引用
有关 bash 的更多细节，请参阅第 12 章。输入 man bash 查看 bash 手册页。

### 目的

bc 命令充当在线计算器和工具。

> 交叉引用
有关 bash 的更多细节，请参阅第 12 章。输入 man bash 查看 bash 手册页。

### 目的

bc 命令充当在线计算器和工具。

> 交叉引用
有关 bash 的更多细节，请参阅第 12 章。输入 man bash 查看 bash 手册页。

### 目的

bc 命令充当在线计算器和工具。

> 交叉引用
有关 bash 的更多细节，请参阅第 12 章。输入 man bash 查看 bash 手册页。

### 目的

bc 命令充当在线计算器和工具。

> 交叉引用
有关 bash 的更多细节，请参阅第 12 章。输入 man bash 查看 bash 手册页。

### 目的

bc 命令充当在线计算器和工具。

> 交叉引用
有关 bash 的更多细节，请参阅第 12 章。输入 man bash 查看 bash 手册页。

### 目的

bc 命令充当在线计算器和工具。

> 交叉引用
有关 bash 的更多细节，请参阅第 12 章。输入 man bash 查看 bash 手册页。

### 目的

bc 命令充当在线计算器和工具。

> 交叉引用
有关 bash 的更多细节，请参阅第 12 章。输入 man bash 查看 bash 手册页。

### 目的

bc 命令充当在线计算器和工具。

> 交叉引用
有关 bash 的更多细节，请参阅第 12 章。输入 man bash 查看 bash 手册页。

### 目的

bc 命令充当在线计算器和工具。

> 交叉引用
有关 bash 的更多细节，请参阅第 12 章。输入 man bash 查看 bash 手册页。

### 目的

bc 命令充当在线计算器和工具。

> 交叉引用
有关 bash 的更多细节，请参阅第 12 章。输入 man bash 查看 bash 手册页。

### 目的

bc 命令充当在线计算器和工具。

> 交叉引用
有关 bash 的更多细节，请参阅第 12 章。输入 man bash 查看 bash 手册页。

### 目的

bc 命令充当在线计算器和工具。

> 交叉引用
有关 bash 的更多细节，请参阅第 12 章。输入 man bash 查看 bash 手册页。

### 目的

bc 命令充当在线计算器和工具。

> 交叉引用
有关 bash 的更多细节，请参阅第 12 章。输入 man bash 查看 bash 手册页。

### 目的

bc 命令充当在线计算器和工具。

> 交叉引用
有关 bash 的更多细节，请参阅第 12 章。输入 man bash 查看 bash 手册页。

### 目的

bc 命令充当在线计算器和工具。



## 第 5 章：通用命令

(PCF)，X 字体服务器更易于使用。PCF 字体可以被任何机器读取。

### 选项

- -i 禁止计算墨水度量。跳过计算可以加快处理速度。
- -l 将字体位顺序设为最低位（LSB）优先。
- -L 将字体位顺序设为 LSB 优先。
- -m 将字体位顺序设为最高位（MSB）优先。
- -M 将字体位顺序设为 MSB 优先。
- -o outputfile 指定输出文件的名称。
- -pn 字体字形的填充大小设置为 n。每个字形的每条扫描线都填充为 1、 2、 4 或 8 字节。
- -t 在可能的情况下将字体转换为“终端字体”。此选项允许字体服务器更快地渲染字体。
- -un 将字体扫描行单位设置为 n。当字体位顺序与字体字节顺序不符时，此选项是必要的；n 可以是 1、 2 或 4 字节。

### 示例

```
$ bdftopf -t -o fontfile.pcf fontfile.dbf
```

### 目的

bitmap 命令用于创建和编辑位图。位图是以网格形式布局的图像文件，用于 X Window 系统的各种用途，从图标、光标到网页图形元素等。它们以实际 C 代码的形式存储，可以直接插入程序中。

此程序可以为光标指定“热点”（hot spot），告诉窗口管理器光标的具体指向位置，例如箭头尖或交叉准线的中心。

basename 用于 C 代码输入文件。要查看图像的实际显示效果，请按 Alt+I。

### 提示

当程序实际运行时，可以使用若干命令，例如反转当前图像和标记位图的一个区域。这些命令可以通过窗口左侧的按钮可用。

### 选项

- -size WIDTHxHEIGHT 指定位图网格的大小，单位为像素。
- -sw dimension 指定方形的宽度，单位为像素。
- -sh dimension 指定方形的高度，单位为像素。
- -gt dimension 设置网格容差；如果尺寸值低于该维度，则将关闭网格。
- -grid 关闭网格线。
- -grid 开启网格线。
- -axes 关闭主轴。
- -axes 开启主轴。
- -dashed 关闭框架和网格线的虚线效果。
- -dashed 开启框架和网格线的虚线效果。
- -stippled 关闭高亮方形的点彩填充。
- -stippled 开启高亮方形的点彩填充。
- -proportional 关闭比例模式（在该模式下，方形宽度等于高度）。
- -proportional 开启比例模式（在该模式下，方形宽度等于高度）。
- -d filename 设置用于作虚线点胶的位图文件名。
- -stipple filename 设置用于高亮点胶的位图文件名。
- -hl color 设置用于高亮的颜色。
- -fr color 设置框架和网格线的颜色。

### 相关命令

- -atbm
- bmtoa

### 目的

bmtoa 命令将 X Window System 位图文件转换为 ASCII 字符串。有关 X Window System 位图文件的更多信息，请参阅 bitmap 命令。

### 选项

- -chars cc 设置用于指定组成位图文件的 0 和 1 的字符。默认使用破折号（-）表示 0，使用井号（#）表示 1。

### 示例

```
$ bmtoa bitmap_file
```

### 相关命令

- -atbm
- bitmap

### cal

显示日历 cal 选项 月 年

### 目的

cal 命令显示当前月份的日历，在指定月份和年份时显示特定月份的日历，或者在仅指定年份时显示该年份 12 个月的日历。年份可以在 1 到 9999 之间，月份可以在 1 到 12 之间。

> 提示 cal 命令基于英/美式习惯。要查看格列哥略日历，请使用命令 cal 1752。

### 选项

- -month 指定月份。
- -year 指定年份。
- -j 返回儒略日，其中天数编号在 1 到 365 之间（闰年除外）。

### 示例

以下示例显示当前月份：

```
cal
```

此示例显示 1997 年 7 月的日历。

```
cal 7 1997
```

此示例显示 1997 年全年的日历。

```
cal 1997
```

此示例显示 1752 年全年的日历。

```
cal 1752
```

### 相关命令

```
date
```

### cdrecord

创建 CD

### cdrecord 选项
设备设置

### 目的

cdrecord 命令将数据录制到 CD 上。cdrecord 命令在符合橙色书籍（Orange Book）标准的设备上录制数据或音频。

### 选项

- -check 检查驱动程序是否存在。
- -debug 打印额外信息。
- -defgap=num 将前隙（pregap）大小设置为 num。这应该只在创建一次刻录（track-at-once）磁盘时配合 TEAC 驱动器使用。
- -dummy 一个会话。
- -eject 在之后吐出 CD。
- -fix 完成 CD。
- -ignores 忽略媒体。
- -inq 执行查询。
- -load 加载媒体。
- -multi 录制多会话。
- -nof 不完成 CD。
- -pr 列出所有空白类型。
- -dev=target 设置 SCSI 目标。
- -driver=name 指定用户提供的名称。
- -fs=num 将 FIFO 缓冲区大小设置为 num。
- -speed=num 设置速度因子，作为音频速度的倍数。
- -timeout=num 将 SCSI 命令超时时间设置为 num。

# 74 第二部分：命令

- -prcap 打印能力。
- -reset 重置 SCSI 总线。
- -scan 扫描所有设备。
- -toc 打印目录。
- -v 增加详细程度。
- -V 增加详细程度。

# 设置

- blank=type 清空。类型可以是以下之一：
- all 清空整个磁盘。
- -fast 清空 PMA。 
- -track 清空特定轨道。
- -session 清空上一个会话。
- -tail 清空轨道末尾。
- -unclose 取消上一个会话关闭。
- -unreserve 取消轨道预留。
- -help 列出所有清空类型。

### 轨道选项

- -audio 以 CD-DA 音频格式写入所有轨道。
- -cdi 以 CDI 格式写入所有轨道。
- -data 以 CD-ROM 模式 1 格式记录所有轨道。带有轨道数据的文件应包含 ISO-9660 或 Rock Ridge 文件系统镜像。这是默认值。
- -isos 使用 ISO-9660 文件系统的大小作为下一个轨道的 own。
- -mode2 以 CD-ROM 模式 2 格式写入所有轨道。
- -pad 在此及后续每个轨道的末尾添加 15 扇零数据。
- -padsize=num 设置附加到下一个轨道的数据量（指定为 num）。该值每个新轨道都会重置为 0。
- -nopad 避免填充轨道。这是默认值。
- -pregap=num 将下一个轨道的前隙大小设置为 num。
- -preemp 在目录中指示所有条目均使用 50/15 秒预加重采样。
- -nopemp 在目录中指示所有条目均以线性数据母带。这是默认值。
- -swab 假设音频数据为字节交换（小端序）顺序。
- -tsize=num 指定原始磁盘上的有效数据量。
- -xa1 以 CD-ROM XA 模式 1 格式写入所有轨道。
- -xa2 以 CD-ROM XA 模式 2 格式写入所有轨道。



### cdwrite
创建 CD

### 目的
`cdwrite` 命令在符合橙色书（Orange Book）标准的 CD 刻录机上记录数据或音频轨道，写入单次会话、红书（Red Book）或黄书（Yellow Book）磁盘。你需要知道哪个设备存放了 CD 录制，尽管在大多数情况下，它是 SCSI 设备。轨道选项允许你定义轨道的格式化。

> 注意 `cdwrite` 命令已不再受支持。你应该使用 `cdrecord` 命令。

### 选项
- -e, --eject 在录制完成后弹出磁盘。
- -D device, --device 设置 CD 刻录机的设备名称。这通常是你的 SCSI 设备的通用地址。
- -s speed, --speed 设置写入速度（1 为单速，2 为双倍速，以此此类推）。
- -y, --dummy 模拟录制 CD 的过程，但关闭激光器。在测试录制时有用。
- --hp 设置惠尔-帕奇（Hewlett-Packard）模式。
- --ims 设置 IMS 模式。
- --kodak 设置柯达（Kodak）模式。
- --philips 设置飞利浦（Philips）模式。
- --yamaha 设置雅马哈（Yamaha）模式。
- -v, --verbose 在每个轨道写入时返回进度显示。
- -h, --help 打印简短帮助信息并退出。

### 轨道选项
- -a, --audio 以红书音频格式写入后续轨道。
- -b bytes, --bytes bytes 指定下一个轨道的数据块长度。
- -d, --data 以黄书数据格式写入后续轨道。这是默认值。
- -p, -preempt 在目录中指示所有条目均已使用 50/15 秒抢占进行采样。
- -n, -nopreempt 在目录中指示所有条目均已使用线性数据进行母带。（这是默认值。）
- -P, -pad 在此轨道及随后的每个数据轨道末尾添加 15 个扇区的零填充数据。
- -N, -nopad 避免填充轨道。（这是默认值。）

### 相关命令
cdrecord

```
chsh
更改 Shell | chsh [-s shell] user
```

### chsh
### 目的
`chsh` 命令更改你的登录 shell。root 用户可以指定 shell。

### 选项
- -s 指定新的 shell。

### 示例
$ chsh -s /bin/bash

### cksum
### 目的
`cksum` 命令计算文件的冗余校验（CRC）。

### 示例
$ cksum file

### clear
### 目的
`clear` 命令清除屏幕。

### 示例
$ clear

### colcrt
### 目的
`colcrt` 命令校正格式。

### 示例
$ colcrt

### csh
### 目的
`csh` 是一种 shell。

### 相关命令
```
tbl
```

### date
### 目的
`date` 命令显示日期和时间。

### 选项
- -s 指定格式。
- -d 指定显示日期或字符串表示的日期。
- -u 设置 UTC 世界标准时间。

### 格式
- %a 星期简写。
- %A 星期全称。
- %b 月份简称。
- %B 月份全称。
- %d 日期。
- %m 月份。
- %y 年份。
- %Y 年份。
- %H 小时（24小时制）。
- %M 分钟。
- %S 秒。
- %T 时间。
- %Z 时区名称。
- %s Unix 时间戳。
- %u 星期几。
- %U 一周几。
- %W 一周几。
- %V 周数。
- %j 一年中的第几天。
- %N 纳秒。
- %l。
- %P 格式。

### 示例
$ date -d "20 Jan 2023"
$ date +%Y-%m-%d

## Part II
### 目的
`dc` 命令是一个高精度计算器。

### 示例
```
10 + 20 |
```



# Options

- -charset 指定用于解释返回值的字符集；charset 必须是 iso-8859-1（ASCII & 英语；默认值）、iso-8859-2、iso-8859-3、iso-8859-4 或 iso-8859-8。
- -compose-only 返回关于键组合的信息。以规范格式打印每个键的完整输出。
- -funcs-only 返回关于功能键的信息。打印每个键的有限信息：可接受的 keycode、可以绑定到键上的操作数量、action 代码的范围，以及 Linux 内核支持的函数键数量。
- -keys-only 返回按键绑定的信息，而不是字符串定义。
- -l 打印每个键的信息：可接受的 keycode 关键字、可以绑定到键上的操作数量、action 代码的范围、Linux 内核支持的函数键数量，以及支持的 action符号及其数值。
- -n 以十六进制格式返回信息。

```
echo
Echoes Input    echo option string
```

# Purpose

echo 命令将文本或值回到标准输出（通常是屏幕）。它实际上存在三个版本：

1. 作为 Linux 命令 (/bin/echo)
2. 作为 C shell 命令
3. 作为 Bourne shell 命令

这三个版本可以互换使用。唯一的区别是 C shell 版本的限制得多（它不以相同的方式支持控制字符，也不支持 -n 选项）。

## 第 5 章：通用命令

# Option

-n 避免在文本末尾打印换行符。

# Control Character

- \a 警报（铃声）。
- \b 退格格。
- \c 不换行。
- \f 换页。
- \n 换行。
- \r 回车。
- \t 水平制表符。
- \v 垂直制表符。
- \\ 反斜杠。
- \nnn 任意字符的 ASCII 代码（八进制格式）。

# Example

这会在屏幕上打印字符串 Good afternoon：
$ echo "Good afternoon"
这会将字符串 We are testing the printer 发送给打印机：
$ echo "We are testing the printer" | lp

```
env Change Environment for a Command env [variable=value] command
```

# Purpose

env 命令为命令临时更改环境变量，或显示当前的环境变量及其值。你的 Linux 系统有一组变量，可以应用于各种情况；例如，与其让每个命令和程序都拥有自己的文本编辑器，大多数程序只需调用 EDITOR 环境变量并调用系统编辑器。其他变量控制默认 shell、你的终端类型、你的命令路径以及你的主目录。

使用带有选项的 env，你可以临时更改所有或选定的环境变量，并让你选择的命令使用新值。当你输入不带选项的 env 时，该命令列出所有当前环境变量。

# Options

- -i 完全忽略当前环境。
- -u variable 取消指定的变量。

Purpose
fsinfo 命令返回关于正在运行的 X Window System 字体服务器的信息。

# Related Commands

- fslsfonts
- xfs

| fslsfonts | fslsfonts option(s) |
| :--- | :--- |
| 列出字体 | pattern |
| (X Window System Command) | |

Purpose
lsfonts 命令列出由运行的 X 字体服务器提供的字体。你可以列出所有字体（可能非常多），也可以用模式匹配字体，该模式支持通配符。（如果你使用 * 和 ? 通配符，必须对它们加引号。）

## 第 5 章：通用命令

# Options

- -1 将输出格式化为单列（数字 1）。
- -C 将输出格式化为多列。
- -l 列出字体属性（字母 l）。
- -l1 列出字体属性。
- -111 作用与 xlsfonts 中的 -111 选项相同。
- -m 列出每个字体的最小和最大边界。
- -n columns 设置输出的列数。
- -server host:port 指定 X 字体服务器。
- -w width 设置输出宽度；默认为 79 个字符。
- -u 保持输出不排序。

# Related Commands

- fsinfo
- fstobdf
- showfont
- xfs
- xlsfonts

| fstobdf Create BDF Font (X Window System Command) | fstobdf option(s) |
| :--- | :--- |

# Purpose

fstobdf 命令从字体服务器读取 X 字体并生成 BDF（Adobe 的字形位图分布格式）字体。

# Options

- -fn fontname 指定来自 X 字体服务器的字体。
- -server servername 指定 X 字体服务器。

# Related Commands

- bdftopcf
- fslsfonts
- xfs

| getkeycodes | getkeycodes |
| :--- | :--- |
| 获取 Keycodes | |

# Purpose
getkeycodes 命令从内核返回 scancode 到 keycode 的映射表。

| getty | getty option(s) |
| :--- | :--- |
| 管理登录会话 | arguments |

# Purpose
getty 命令是一个通用的 tty 管理包。它打开 tty 端口，提示输入用户名，并调用 /bin/login 命令。通常，你不会自己调用 getty；它通常在系统启动时由 /etc/init 文件调用。

> 交叉引用
查看在线联页页以获取许多可用选项的完整列表。（输入 man getty。）

# Related Commands

- aty
- stty

# gimp option(s) file(s)

Purpose
gimp 命令启动 Linux 上最先进的图像处理程序之一。gimp 命令是 *GNU Image Manipulation Program* 的缩写。凭借全套图形工具，gimp 是一款复杂但功能强大的软件。我们没有涵盖该软件的所有功能；关于该软件已经写了整本书。

# Options

- -b commands, --batch commands 以批模式运行，循环执行命令。
- -n, --no-interface 不带用户界面运行。
- --display display 在指定的 X 显示上显示。
- --no-data 在不加载图案、渐变、调色板和笔的情况下运行。
- --no-splash 不显示启动窗口运行。
- --no-splash-image 不在启动窗口显示图像运行。
- --no-shm 不在 gimp 及其插件之间使用共享内存运行。
- --no-xshm 不使用 X 共享内存扩展运行。

# Related Command

- xv

### 第二部分：命令

```
gnuplot
Interactive Plotting
(GNU Command)
```

```
gnuplot option(s) file(s)
```

# Purpose

gnuplot 命令启动交互式绘制程序。它可以绘制任意数量的函数和文件，比较实际数据与理论曲线。此外，gnuplot 支持自定义和标记的 X 和 Y 范围，并具有可选的自动缩放、智能轴比例和智能标记。

# Options

- -persist 在 gnuplot 退出后保留绘制窗口。
- -raise 在绘制后提升绘制窗口。
- -norise 在绘制后最小化绘制窗口。
- -gray 在彩色显示器上请求灰度渲染。
- -mono 在彩色显示器上强制单色渲染。
- -clear 请求在显示新图形之前清除。
- -tvwm 相对于当前显示部分设置几何规格。
- -pointsize size 设置点的大小。

```
id
Personal Identification
```

```
id option(s)
username
```

# Purpose
id 命令返回你自己或其他指定用户名的信息。这些信息包括用户 ID 和组 ID，以及有效的用户 ID 和组 ID。

# Options

- -g 仅返回组信息。
- -G 返回附加组信息。
- -n 与 -g、-G 或 -u 使用时返回名称（而不是数字）。
- -r 返回真实 ID 和组 ID，而不是有效 ID。
- -u 仅返回用户 ID。

![](img/2cc16c5632743593217f446101e471f_106_0.png)

# Purpose

info 命令返回关于给定主题的超文本信息，该主题可以是命令或学科。这些信息以 GNU texinfo 格式在大纲形式存储。

### 交叉引用

访问 Texinfo 网站 (http://texinfo.org) 获取有关 texinfo 格式的信息。

当你带主题启动 info 后，可以在大纲上下移动，查看相关主题。如果你不带主题启动 info，将看到欢迎屏幕（存储在 /usr/local/info/dir），解释 info 如何工作以及你如何在系统中移动。

# Options

- --directory directory 使用目录而不是标准的 info 目录 (/usr/local/info/dir)。
--dribble file 将按键存储在文件中，然后可以使用 --restore 选项返回 info 会话中的特定位置。
-f file 使用文件而不是标准的 info 文件。

--help
显示 info 命令的帮助信息。

-n node
指定开始的节点。

-o file
将信息发送到文件而非标准输出。

--restore file
运行文件（使用 --dribble 选项创建）。

--subnodes
显示子主题。

--version
显示 info 版本。

### 相关命令

+   man
xman

| kbd_mode 键盘模式 | kbd_mode 选项(s) |
| :--- | :--- |

### 目的

kbd_mode 命令返回当前键盘模式或更改它。

### 选项

+   -a 将模式设置为 XLATE (ASCII)。
-k 将模式设置为 MEDIUM-RAW。
-s 将模式设置为 RAW。
-u 将模式设置为 Unicode。

| kill 杀死进程 | kill 选项(s) PID |
| :--- | :--- |

### 目的

kill 命令结束一个进程 ID (PID)。只有 PID 的所有者或特权用户（例如 root 用户）才能杀死进程。

### 注意

此命令也内置在 bash 和 csh shell 中，尽管它们在这些里的工作方式有所不同。

### 选项

+   -l 列出可以发送给进程的有效信号。
-signal 指定由 kill -1 返回的信号。

### 相关命令

```
killall
ps
```

| killall 杀死所有进程 | killall 选项(s) name |
| :--- | :--- |

### 目的

killall 命令按名称杀死所有进程，无论有多少进程正在使用该命令。要杀死运行可执行文件的进程，请在命令名中使用 / somewhere。

### 选项

+   -e 对进程名进行精确匹配（限制为 15 个字符）。
-g 杀死指定进程所属的进程组。
-q 如果没有杀死任何进程，则抑制投诉。
-V 显示版本号并退出。
-w 等待指定的进程死亡。
-i 确认进程是否应该被杀死。
-l 列出有效信号。
-v 在详详细模式下运行；列出结果和 ID。
-signal 指定由 killall -1 返回的信号。

### 相关命令

+   kill
ps

| listres 列出资源 (X Window 系统命令) | listres 选项(s) widget |
| :--- | :--- |

### 目的

listres 命令返回 widget 资源数据库的列表。它列出首次定义每个资源的类、实例和类名以及每个资源的类型。如果没有指定特定的 widget 或 -all 选项，将打印一个包含 widget 名称及其类层次结构的双列列表。

### 选项

+   -all 返回所有已知 widget 和对象的信息。

+   -nosuper 忽略继承自父类的资源。

+   -variable 通过类记录变量的名称来识别 widget，而不是通过类名。

+   -format printf-string 指定用于 printf 风格的格式字符串，用于打印每个资源的名称、实例、类和类型。

## 第 5 章：通用命令

```
login
登录系统登录 login 用户名选项
```

### 目的

login 命令用于登录 Linux 系统。如果你没有在命令行上指定用户名，login 命令将提示你输入一个用户名。

注意
login 命令还执行一些行政管理操作，例如设置 tty 的 UID 和 GID，并在有任何待处理邮件时通知用户。root 用户可以设置 login 命令以执行某些基本身份验证（更多信息请参阅手册页）。此外，login 命令可用于指定 root 用户可以登录的位置；tty 列表可以位于 /etc/security 并由 login 检查。

### 选项

+   -f 跳过第二次登录身份验证；在 Linux 下工作不正常。

+   -h host 将远程主机名传递给 login；供服务器使用并由超级用户设置。在 Linux 下也无法正常工作。

+   -p 保留 getty 之前使用的环境。

```
logname
打印登录名
(GNU 命令) logname 选项(s)
```

### 目的

logname 命令返回调用进程的登录名，在 /etc/utmp 文件中查找。如果没有找到登录名，则生成错误消息。

### 选项

--help 打印简短的帮助信息并退出。
--version 打印版本号并退出。

| makewhatis 生成 whatis | makewhatis 选项(s) manpath |
| :--- | :--- |

### 目的

makewhatis 命令构建并更新 whatis 和 apropos 数据库使用的 whatis 数据库。

> 注意
必须安装 Perl 才能运行。

### 选项

+   -g 使用全局 whatis 文件，而不是每个 man 目录一个。
-h 显示帮助屏幕。
-v 在详详细模式下运行。
-u 仅用新的手册页更新数据库。默认是完全重建数据库。
-w 返回 manpath。

### 相关命令

+   - apropos
- man
xman

| man 在线手册页 | man 选项(s) section 标题 |
| :--- | :--- |

### 目的

man 命令格式化并显示在线手册页中的内容。这些页面是 Linux 和 UNIX 系统的官方文档，并采用严格的格式。在寻找晦涩的选项和命令时它们非常有用，但在寻找命令的通用解释时效果并不好。

通常，你必须将特定的命令与 man 命令匹配。然而，你可以从章节开始搜索并以此方式缩小范围。

### 选项

+   -a 显示所有匹配标题的手册页，而是第一页。这在查看如 mount 等在多个不同手册章节中包含手册页的单词时有用。

+   -c 重新格式化手册页，即使已存在格式化页面。

+   -C config_file 指定要使用的 man.conf 文件；默认是 /usr/lib/man.conf。

+   -d 显示调试信息，而非实际手册页。

+   -D 显示调试信息和手册页。

+   -f 调用类似于 what 命令的摘要。

+   -h 打印 man 命令的单行摘要。
+   -k 与 apropos 命令相同。
+   -m system 在系统处搜索手册页。
+   -M path 指定搜索手册页时使用的路径。默认使用环境变量 PATH。如果未设置，则在 /usr/lib/man.conf 中查找。
+   -p string 指定在 nroff 或 troff 之前运行的预处理器。实际上对 Linux 并不适用。
+   -P pager 指定使用的分页器（即格式化并显示页面的命令）；默认是 /usr/bin/less -is。
+   -S section_list 指定要搜索的章节列表。
+   -t 使用 /usr/bin/groff -Tps -mandoc 来格式化手册页。

### 第二部分：命令

-W 显示手册页的位置，而非实际页面。

-W 显示手册页的位置，每行一个文件名。

### 相关命令

+   apropos
manpath
whatis
xman

### 目的

mcookie 命令为 xauth X 认证系统创建魔法 cookie（具体来说，是一个 128 位的随机十六进制数）。它通常与 xauth 命令直接使用。

### 选项

-v 在详详细模式下运行。

-f filename 将文件名添加到生成随机 cookie 的内容列表中。

> 注意
在 Linux 和 X Window 术语中，cookie 有两个含义。此命令和 X 身份验证系统使用的 cookie 与 Netscape Navigator 浏览器生成的用于存储用户信息（如会话信息，供 Web 服务器访问）的 cookie 不同。

### 相关命令

xauth

### minicom
启动串口通信

### 目的

minicom 命令启动了一个与 Telix 类似的串行通信包。（如果你知道或用过 Telix，说明你老了。）它的特点是具有一个带有自动重拨次数的拨号目录、支持串口设备上的 UUCP 风格锁文件、独立的脚本解释器、捕获到文件、具有独立配置的多个用户等。在如今的时代，使用串口通信包——它通常*不用于*访问互联网，而是用于连接公告板系统（BBS）——似乎有些古。

当你运行 minicom 时，有几个选项和命令可用。查看在线手册页以获取更多信息；也可以在启动后自行研究 minicom。

### 选项

+   -a 设置属性用法。
-c 设置颜色用法。
-d 启动时直接拨号目录输入。
-l 指定对带有高位的字符进行字面翻译。
-m 用 Alt (Meta) 键覆盖命令键。
-M 用 Alt (Meta) 键覆盖命令键，假设 Alt 键是字符的第 8 位（发送 128 + 字符代码）。
-S 在启动时运行指定的脚本。
-p 使用指定的伪终端而非普通终端。
-C filename 在启动时捕获名为 *filename* 的文件。
-8 在进行任何修改的情况下传递 8 位字符。



 -t 设置终端类型，覆盖 `TERM` 环境变量。
-O 跳过初始化。
-S 以设置模式启动 minicom，并显示配置菜单。（仅限 root 用户）。
-z 显示终端状态行。

### 相关命令

seyon

| mzip 弹出 Zip/Jaz 磁盘 | mzip 选项(s) 驱动器 |
| :--- | :--- |

### 目的

The `mzip` 命令用于弹出磁盘并更改 Zip/Jaz 驱动器的写保护模式。

### 选项

+ -e 弹出磁盘。
+ -f 即使在磁盘已挂载的情况下也弹出。
+ -r 将权限设为只读。
+ -u 临时取消磁盘的保护，直到将其弹出。
+ -q 返回当前磁盘的状态。
+ -w 将权限设为可读可写。
+ -p 将权限设为带密码保护的写保护。
+ -x 为磁盘添加密码保护。

### nice
以良好的优先级运行命令
(GNU 命令)

| nice 选项 命令参数(s) |
| :--- |

### 目的

`nice` 命令允许你为命令设置优先级；如果系统负载过重，命令将不会运行，或者不会占用过多的系统资源。`nice` 值可以在 19（最低优先级）到 -20（最高优先级）之间设置，但只有特权用户可以设置负优先级。

> 注意

如果没有任何参数，`nice` 命令将打印当前的调度优先级。此外，此 GNU 命令的描述包含在大多数 Linux 发行版中，而不是 nice shell 命令中。

### 选项

+ -ADJUST 将优先级增加 10（ADJUST 的值）。
-adjustment 向命令的优先级添加 *adjustment* 值，而不是 10。

### nohup
不挂断信号
(GNU 命令)

| nohup 命令参数 |
| :--- |

### 目的

`nohup` 命令确保命令行上指定的命令在不被中断的情况下运行，即使你注销了系统。

> 注意

此命令的 GNU 版本与大多数 UNIX 系统中的 `nohup` 命令几乎相同。

# # oclock
圆形时钟 (X 窗口系统命令)

oclock 选项(s)

### 目的

`oclock` 命令启动一个圆形模拟时钟。

### 选项

+ -fg color 设置时钟指针和宝石装饰的颜色。
- -bg color 设置背景颜色。
- -jewel color 设置宝石的颜色。
- -minute color 设置分针的颜色。
- -hour color 设置时针的颜色。
- -bd color 设置窗口边框颜色。
- -bw width 设置窗口边框宽度。
- -transparent 将时钟缩小至保留宝石、指针和边框。

### 相关命令

+ rclock
xclock

### passwd
更改密码

passwd name

### 目的

`passwd` 你的密码。你可以单独运行 `passwd`，系统会提示输入旧密码和新密码。

新密码长度至少为六个字符，且包含大写和小字母。此外，特权用户可以通过在命令行指定用户名和新密码来更改其他用户的密码。

```
pathchk
检查路径
(GNU 命令)
```

pathchk 文件名

### 目的

`pathchk` 命令检查文件名是否有效（即路径中的目录是否可搜索）或是否具有移植性（满足长度要求）。

### 选项

-p 检查 POSIX 可移植性。

```
pidof
显示进程 ID
```

pidof 选项(s) 程序

### 目的

`pidof` 命令列出正在运行程序的进程 ID。你通常不会单独使用它，而是在运行级别更改脚本中使用。它实际上是 `killall5` 命令的软链接。

### 选项

+ -s 仅返回一个 PID。
-o pids 忽略 PIDs。
-x 返回运行指定脚本的 shell 的进程 ID。

### 相关命令

+ halt
init
killall5
reboot
shutdown

| printenv
打印环境变量 (GNU 命令) | printenv 变量 |
| :--- | :--- |

### 目的

`printenv` 命令打印你的环境变量。如果你指定了一个变量，该命令将返回关于该变量的信息；如果你未指定，`printenv` 命令将打印所有变量的信息。

| ps
打印状态 | ps 选项(s) |
| :--- | :--- |

### 目的

`ps` 命令返回有关进程状态的信息。该命令提供了一组长且复杂的选项。

> 交叉引用
查看在线手册页以获取有关选项的更多信息。

| rb
接收 Ymodem | rb 选项(s) |
| :--- | :---

### 目的

`rb` 命令用于使用 Ymodem 传输协议接收文件。

### 选项

+ -a 去除回车和所有从第一个 Ctrl-z 开始的字符。
-b 二进制文件传输覆盖。
-q 在静音模式下工作。
-v 在详细模式下工作，并将文件名列表追加到 /tmp/rzlog。
-y 覆盖任何同名的现有文件。

![](img/2cc16c5632743593217f446101e4719f_120_0.png)

目的
`rclock` 命令将模拟时钟与预约提醒结合起来。如果有邮件等待，它会进入反转视频模式。

### 选项

+ -fg color 设置窗口的前景颜色。
-bg color 设置窗口的背景颜色。
-fn font 设置用于提醒的字体。
-iconic 启动标识模式。
-adjust ddhhmm 在非 root 用户的情况下调整时钟（dd=天，hh=小时，mm=分钟）。
-update n 更改时钟更新频率（以秒为单位，默认为 30 秒）。
-mail n 更改检查新邮件的频率（以秒为单位，默认为 60 秒）。

### 相关命令

+ oclock
xclock

### rdjpgcom
JPEG 中的注释

rdjpgcom 选项 文件

### 目的

`rdjpgcom` 命令读取 JPEG 文件并打印其中的注释。你通常不会单独使用它，而是在脚本格式中使用。其大小限制为 64K。

### 选项

+ -verbose 以详细模式输出。

### 相关命令

+ jpeg
djpeg
wrjpgcom

### reconfig
配置 Xconfig (X 窗口系统命令)

reconfig <Xconfig>
>X86

### 目的

`reconfig` 命令将旧的 Xconfig（XFree6 3.1 之前的版本）转换为新的 Xconfig。

> 提示 你可能需要编辑 Xconfig 文件。

### renice
更改优先级

renice 选项 用户

### 目的

`renice` 命令更改一个或多个运行进程的调度优先级。

### 选项

+ -g 强制参数解释为进程组 ID。
-p 按优先级值排序。
-u 强制参数解释为用户名。

### reset
重置终端

reset

### 目的

`reset` 命令重置终端。它调用一系列命令来实现。

### 相关命令

```
reset
stty
tput
```

### resize
调整屏幕大小 (X 窗口系统命令)

resize 选项(s)

### 目的

`resize` 命令将 TERM 和 TERC 设置为 xterm 窗口的尺寸。为了实现这一点，

### 第二部分：命令

必须是命令行的一部分或重定向到文件。

### 选项

+ -u 生成 Bourne shell 命令，即使当前不是 Bourne shell。
-c 生成 C shell 命令，即使当前不是 C shell。
-s [rows columns] 使用 Sun 控制台转义序列而不是 xterm 转义码。如果指定了行和列，xterm 窗口将被调整大小。

![](img/2cc16c5632743593217f446101e4719f_123_0.png)

目的
`runscript` 命令是 minicom 终端软件的解释器。它通常用于自动登录远程服务器或公告板，而不是在互联网上登录。你也可以将主目录作为最后一个参数。
脚本中可以识别以下命令：expect, send, goto, gosub, return, exit, print, set, inc, dec, if, timeout, verbose, sleep, break, 和 call。实际脚本语言接近 BASIC，minicom 源码带有两个示例脚本：scriptdemo 和 unixlogin。

### 相关命令

minicom



-e 强制发送方转义所有控制字符；通常 XON、XOFF、DLE、CR-CR 和 Ctrl-X 会被转义。

- -v 在详细输出模式下运行，并将文件名列表追加到 /tmp/rzlog。此命令与 sx 命令相关。

### 目的

rxvt 命令是一个用于 X Window系统的彩色 VT100 终端模拟器。它实际上是流行的 xterm 终端模拟器的精简版本，缺少了一些你可能不会需要的 xterm 特性（Tektronix 4014 仿真、会话日志和工具包的可配置性）。优点是 rxvt 使用的交换空间比 xterm 少得多。如果你在内存紧张的环境下操作，可能考虑从 xterm 切换到 rxvt。

> 提示：有关资源的更多信息请参 xterm 命令，因为 rxvt 接受与 xterm 大部分相同的资源。

# 

- -7 以 7 位模式运行，移除键盘输入的所有字符的第 8 位。
- -8 以 8 位纯模式运行，允许将键盘输入字符的第 8 位传递给应用程序。
- -bg color 将背景颜色设置为 color。
- -bigfont keysym 将 Alt-keysym 设置为增大字体大小的开关，而不是默认的 Alt->。
- -C 捕获系统控制台消息。
- -display display-name 在指定的 display-name 上打开 rxvt。
- -e command [options] 在启动 rxvt 后立即运行命令及其命令行选项。如果使用此选项，它必须是命令行的最后一个选项。
- -fat 使用粗滚动条代替默认的滚动条。
- -fg color 将前景颜色设置为 color。
- -font fontname 将文本字体设置为 fontname。
- -geometry geometry 使用指定的 X 几何形状打开窗口。
- -ic 以未标识身份启动。
- -ls- 添加到窗口 shell 的 argv[0] 中，使其成为登录 shell。
- -ls- - 添加到窗口 shell 的 argv[0] 中，使其成为登录 shell。它还会告诉 rxvt 如果接收到铃声字符时保持图标化（iconified）。
- -ma 如果接收到铃声字符时，从图标打开 rxvt。
- -meta string 更改 Alt+ 键位的设置。默认情况下，rxvt 在接收到 Alt 键按下时发送转义前缀。你可以为字符串指定 escape、8bit 或 ignore。
- -n text 将窗口图标或图标管理器中的名称设置为 text。除非也设置了 -T 选项，否则还会将标题栏中的窗口标题设置为 text。
- -pagedown keysym 将 Alt-keysym 设置为向下滚动页的开关，而不是默认的 Alt-Next Page。
- -pageup keysym 将 Alt-keysym 设置为向上滚动页的开关，而不是默认的 Alt-Prev_Page。
- -secure keysym 将 Alt-keysym 设置为增大字体大小的开关，而不是默认的 Alt-s。
- -sl number 保存滚动文本的行数，而不是默认的 64。
- -smallfont keysym 将 Alt-keysym 设置为减小字体大小的开关，而不是默认的 Alt-<<。
- -T text 将标题栏中的字符串设置为 text。
- -thin 无论如何都使用细滚动条。

| rz | rz 选项(s) |
| :--- | :--- |
| 接收 Zmodem | |

### 目的

rz 命令用于使用 Zmodem 协议接收批量文件。路径由发送程序提供，并在需要（且可行）时创建目录。通常，rz 命令由调用的 Zmodem 程序自动发出，但某些缺陷的 Zmodem 实现可能需要以旧方式启动 rz。

### 选项

- -a 移除回车和从第一个 Ctrl-Z 开始的所有字符。
- -b 二进制文件传输覆盖。
- -c 请求 16 位 CRC。
- -D 将文件数据输出到 /dev/null；用于测试。
- -e 强制发送方转义所有控制字符；通常 XON、XOFF、DLE、CR-CR 和 Ctrl-X 会被转义。
- -p 如果目标文件存在则跳过文件。
- -q 在静默模式下运行。
- -t time 将超时更改为 time 十分之一秒。
- -v 在详细输出模式下运行，并将文件名列表追加到 /tmp/rzlog。
- -y 覆盖任何同名的现有文件。

### sb
发送 Ymodem

sb 选项(s) filename

### 目的
sb 命令使用 Ymodem 协议将文件发送到另一个系统。此命令有许多可用的选项。

交叉引用
更多信息请参阅在线手册页。

### script
保存脚本

script 选项 filename

### 目的
script 命令将终端会话中的每个字符保存到指定的文本文件名。如果没有指定文件名，字符将保存到 typescript。

### 选项
- -a filename 将按键记录追加到现有文件名中。

### seyon
串口通信
(X Window系统命令)

seyon 选项(s)

### 目的
seyon 命令是一个基于 X Window 的电信包，用于连接远程客户端和公告板系统（BBS）。所有的选项和命令都出现在界面中，尽管在命令行启动 seyon 时，还可以设置一些额外的选项。

### 注意事项

此命令支持广泛的资源以及一种脚本语言。更多信息请参阅在线手册页。

### 选项

- - -- 将命令行的剩余部分传递给终端模拟器。
- - -dial 覆盖 dialAutoStart 资源。
- -emulator terminal-emulator 为 seyon 指定终端模拟器；如果未指定，则使用 xterm。
- -entries entries-list 用 entries-list 覆盖默认的 PhoneEntries 资源。
- - -modems device-list 覆盖现有的 modems 资源。
- - -nodefargs 不传递终端模拟选项。
- -noemulator 告诉 seyon 启动自己的终端模拟器。
- -script script 在 seyon 启动后执行脚本。

| shar Shell 存档 | shar 选项(s) filename |
| :--- | :--- |
| | |

### 目的

shar 命令创建 shell 存档（也称为 shar 文件），这些文件是文本格式的，可以发送给另一个用户，用户可以使用 bin/sh 对其解包并执行。

### 选项

- -a 自动生成头文件。
- -b 在压缩时使用 -x 作为参数。（由于许多原因，这是一个应避免的选项。）
- -B 将所有文件视为二进制文件。（由于许多原因，这是一个应避免的选项。）
- -c 以 cut 行作为 shar 文件开头。
- -d XXX 使用 XXX 作为文件分隔符，而不是默认的 SHAR_EOF。
- -f 仅通过文件名恢复，而不是恢复整个路径。
- -F 强制在每行前添加前缀字符，即使不需要。
- -g 在压缩时使用 -X 作为 gzip 参数。（由于许多原因，这是一个应避免的选项。）
- -l XX 将 shar 文件限制为 XX 千字节，但不拆分文件。
- -L XX 将 shar 文件限制为 XX 千字节，但会拆分文件。
- -m 避免在从存档解包文件时生成 touch 命令来恢复文件修改日期。
- -M 判断文件是文本还是二进制并进行相应的存档，这意味着二进制文件将被 uencode。（由于许多原因，这是一个应避免的选项。）
- -n name 指定包含在 shar 文件头中的存档名称。
- -o XXX 将存档保存为文件 XXX.01 到 XXX.nn，而不是标准输出。
- -p 允许位置参数选项。
- -P 在 shar 文件中使用临时文件代替管道。
- -s who@where 覆盖自动确定的提交者名称。
- -S 从标准输入读取要打包的文件列表，而不是文件名。
- -T 将所有文件视为文本。
- -V 原始版 shar 文件，在解包环境中只需要 sed 和 echo。
- -v 在静默模式下运行，禁用解包存档时输出的注释。
- -w 在解包存档时不进行 wc -c 检查。
- -x 不经检查覆盖现有文件。
- -X 在覆盖现有文件之前进行检查。
- -z 使用 gzip 和 uuencode 压缩所有文件打包。（由于许多原因，这是一个应避免的选项。）
- -Z 使用 compress 和 uuencode 压缩所有文件打包。（由于许多原因，这是一个应避免的选项。）

### 相关命令

unshar

### 目的
shelltool 命令在终端窗口中运行 shell 或程序。尽管 shelltool 文档是这么说的，但在 Linux 环境中不需要安装 OpenWindows 即可运行此命令，除非在使用 OpenWindows 程序，否则实际上没有理由运行它。

### 选项

- -B boldstyle 设置显示粗文本的样式。
- -C 重定向系统控制台输出到 shelltool。
- -I command 将命令传递给 shell。



### showfont
显示字体
(X Window 系统命令)

### showfont 选项

### 目的

showfont 命令显示由 X 字体服务器管理的字体。你需要运行 X 字体服务器，该命令才能正常工作。返回的信息包括字体信息、字体属性、字符度量标准和字符位图。你可以使用通配符来匹配宽范围的字体名称。

### 选项

- - bitmap_padn 设置字体的位图填充单元（n 为 0、1 或 2，其中 0 是 ImageRectMin，1 是 ImageRectMaxWidth，2 是 ImageRectMax）。
- - extents_only 仅显示字符的范围（extents），不显示位图。
- - end char 确定要显示字符范围的末尾（char 为数字）。
- - fn name 指定要显示的字体。
- - lsb 指定字体的位序为 LSBFirst（最低有效位优先）。
- - LSB 指定字体的位序为 LSBFirst（最低有效字节优先）。
- - msb 指定字体的位序为 MSBFirst（最高有效位优先）。
- - MSB 指定字体的位序为 MSBFirst（最高有效字节优先）。
- - pad n 扫描字体的扫描单元（n 为 8、16、32 或 64）。
- - server host:port 指定要连接的 X 字体服务器。
- - start char 确定要显示字符范围的起始（char 为数字）。
- - unit n 设置字体的扫描行单元（n 为 8、16、32 或 64）。
- - noprops 不返回字体属性。

### 相关命令

- fs
fslsfonts
xlsfonts

### showrgb
显示颜色数据库
(X Window 系统命令)

showrgb 数据库

### 目的

showrgb 命令读取 dbm 数据库中的格式并将其转换回源形式，打印到屏幕上。

### skill
重新调整进程优先级

### skill 选项 PID

### 目的

skill 命令向指定的进程发送信号或重新调整其优先级。它可以向一组进程发送终止信号，或者也可以发送其他信号（前加 - 符号）。要查看可用信号的列表，请使用 skill -l 或 skill -L 命令行。

### 选项

- -f 在快速模式下运行，在该模式下，允许读取进程的机器相关代码做出决策以提高速度，是以牺牲错误报告为代价。
- -i 在交互模式下运行，系统会针对每个待处理的进程提示用户。
- -n 仅显示进程 ID（PID）。
- -v 在详细模式下运行，显示成功的操作。
- -w 在进程不可达时发出警告。

### 相关命令

- - kill
nice
- ps
- renice
- signal
- snice

### sleep

### 目的

sleep 命令暂停系统指定的时间：秒数、分钟、小时和天数。

### snice

### 目的

snice 命令更改所选进程的调度优先级。默认新优先级为 +4，但可以使用形式为 +n（或 -n）的参数来指定不同的值。无效的优先级将向下取整（或向上取整）到第一个接受的值。

### 选项

- -f 在快速模式下运行，在该模式下，允许读取进程的机器相关代码做出决策以提高速度，但是以牺牲错误报告为代价。（snice 手页指出此选项并不有效）。
- -i 在交互模式下运行，系统会针对每个待处理的进程提示用户。
- -n 仅显示进程 ID。
- -v 在详细模式下运行，显示成功的操作。
- -w 在进程不可达时发出警告。

### 相关命令

- kill
nice
ps
renice
signal
skill

### smproxy

### 目的

smproxy 命令允许不支持 X11R6 会话管理的 X 应用程序参与 X11R6 会话。

### 选项

- -clientId id 设置上一个会话使用的 Session ID。
- -restore saveFile 设置用于保存上一个会话状态的文件。

### splitvt
分 Shell

| splitvt | splitvt 选项 shell |
| :--- | :--- |

### 目的

splitvt 命令在两个窗口中运行两个 shell。shell 是你的默认 shell（通常是 xterm）。在窗口之间移动请使用 Ctrl-W。

### 选项

- -login 在每个窗口下运行程序，就像它们是登录 shell 一样。
- -lower command 在下方窗口中运行 *command*。
- -nologin 不允许每个窗口下的程序像登录 shell 一样运行。
- -norc 不加载 ~/.splitvtrc。
- -rcfile file 加载 *file* 作为启动文件而不是 ~/.splitvtrc。
- -s numlines 为上方窗口设置 *numlines*（行数）。
- -t title 设置 xterm 标题栏的标题。
- -upper command 在上方窗口中运行 *command*。

### startx
启动 X (X Window 系统命令)

| startx | startx |
| :--- | :--- |

### 目的

startx 命令从 Linux 命令行启动 X Window 系统会话。它实际上是 xinit 命令的前以前端。

当你启动 startx 时，它会在你的主目录中查找一个名为 .xinitrc 的文件。该文件包含了关于你的 X Window 设置的信息，以及你希望与你的 X 环境一起运行的客户端。大多数客户端都运行在后台，列表中的最后一个客户端除外，该客户端应该在前台运行（这通常是一个窗口管理器）。

> 提示
与此命令相关的设置并不多；你可能需要检查 xinit 以获取更多信息。一个实用的选项是 -bpp，可以用于设置显示器的颜色深度。例如，要使用 16 位颜色，你可以输入 startx --bpp 16。

### 相关命令

xinit

### strace

### 目的

strace 命令用于跟踪系统调用和信号。你用它来运行指定的命令；strace 然后会跟踪进程使用的系统调用和信号。结果信息将打印到屏幕或文件（使用 -o 选项）。这是一个非常有用的命令，因为你不需要源代码就能看到命令在哪里出了问题。

### 选项

- -acolumn 按指定的列数对齐。
- -c 统计每个系统调用的时间、调用和错误并报告摘要。
- -d 显示 strace 自身的调试输出。
- -eab=set 缩短输出。
- -eraw=set 以十六进制格式打印指定的参数。
- -eread=set 以十六进制格式打印所有字符串。
- -esignal=set 仅跟踪部分信号。
- -etrace=set 仅跟踪集。
- -everbose=set 对指定的集合解引用结构。
- -f 跟踪子进程。
- -i 在调用时打印指令指针。
- -ofname 将输出写入文件名。
- -O 设置跟踪系统调用的开销到。
- -ppid 附加到进程并开始跟踪。
- -q 抑制消息。
- -r 在每次调用进入时打印相对时间戳。
- -s strsize 设置打印的最大字符串大小（默认为 32）。
- -Ssby 按 -c 选项的输出进行排序。
- -t 在跟踪的每行开头打印时间。
- -tt 在跟踪的每行开头打印时间，包括微秒。
- -T 返回返回在系统调用上花费的时间。
- -v 提供详细输出。
- -x 以十六进制格式打印非 ASCII 字符串。
- -xx 以十六进制格式打印所有字符串。

### 相关命令

ptrace
time
trace

| strings | strings 选项 filename(s) |
| :--- | :--- |

### 目的

strings 命令在文件中搜索可打印的字符串。默认情况下，字符串的长度至少为四个字符时才会被显示。



## 第 5 章：通用命令

大多数 Linux 实现包含两个版本的 strings：原始 UNIX 版本 (strings)，本章将介绍它；以及 GNU 版本 (strings-gnu)，它是一个更高级的版本。

### 选项

- -a 搜索整个对象文件以查找字符串。默认情况下仅搜索对象文件的文本和数据段。
- -f 打印包含字符串的文件名以及字符串本身。
- -n num 将字符串的最小字符数设置为 *num*，而不是默认的四位。
- -o 打印字符串在文件中的十进制偏移量以及字符串本身。
- -t {o,x,d} 打印字符串在文件中的偏移量（格式）以及字符串本身。单字符参数指定偏移量的基数——八进制、十六进制或十进制。
- --target=bfdname 指定系统默认格式之外的对象代码格式。

### 目的

stty 命令返回并更改终端设置。在不带参数的情况下，stty 返回当前设置：波特率、行控制号以及与 `stty sane` 设置的值不同的不同的行设置。

## 非选项设置

如果在设置前加上 -，则可以切换为反向行为。

- - clocal: 禁用调制解器控制信号。
- creadad: 允许接收输入。
- crtscts: 启用 RTS/CTS 握手。
- cs5 cs6 cs7 cs8: 将字符设置为 5、6、7 或 8 位。
- cstopb: 每个字符使用 2 个停止位（带有 - 时）。
- hup: 当最后一个进程关闭 tty 时发送挂起信号。
- hupcl: 当最后一个进程关闭 tty 时发送挂起信号。
- parenb: 在输出中产生校验位，并在输入中期望校验位。
- parodd: 设置奇数奇偶（前加 - 则为偶数奇偶）。

### 输入设置

如果在设置前加上 -，则可以切换为反向行为。

- - brkint: 中断引起中断信号。
- icrnl: 将回车转换为换行符。
- ignbrk: 忽略中断。
- igncr: 忽略回车符。
- ignpar: 忽略奇偶错误。
- imabel (np): 当输入缓冲区满时有字符到达，启用蜂鸣且不刷新输入缓冲区。
- inlcr: 将换行符转换为回车符。
- inpck: 启用输入奇偶校验。
- istrip: 去除输入字符的高位（第 8 位）。
- iuclc (np): 将大写字母转换为小写字母。
- ixany (np): 允许任何字符重启输出。
- ixon: 启用 XON/XOFF 流控。
- ixoff tandem 当系统输入缓冲区几乎满时，启用发送停止字符；当它再次几乎为空时发送起始字符。
- parmrk: 使用 255-0-字符序列标记奇偶错误。

### 输出设置

如果在设置前加上 -，则可以切换为反向行为。

- - bs1 bs0 (np) 设置退格键延迟样式。
- cr3 cr2 cr1 cr0 (np) 设置回车延迟样式。
- ff1 ff0 (np) 设置换页延迟样式。
- nl11 nl10 (np) 设置换行符延迟样式。
- ocrnl (np) 将回车转换为换行符。
- ofdel (np) 使用删除字符填充，而不是空字符。
- ofill (np) 使用填充字符而不是定时来实现延迟。
- olcuc (np) 将小写字母转换为大写字母。
- onlcr (np) 将换行符转换为回车-换行符。
- onret (np) 使用换行符作为回车符。
- onocr (np) 不在第一列打印回车符。
- opost 对输出进行后处理。
- tab3 tab2 tab1 tab0 (np) 设置水平制表延迟样式。
- vt1 vt0 (np) 设置垂直制表延迟样式。

### 选项

- -a 打印当前设置。
- -g 以可以被另一个 stty 命令使用的格式打印设置。

### su
切换用户
(GNU 命令)

su option(s)

### 目的

su 命令运行一个带有替换用户 ID 和替换组 ID 的 shell。基本上，它允许你临时地作为新用户登录系统，并具有真实和有效的用户 ID、组 ID 和补充组。shell 取自密码输入，如果没有处指定，则使用 `/bin/sh`。如果用户有密码，su 会提示输入，除非该用户的真实用户 ID 为 0（超级用户）。

> 注意
> 当运行此命令时，当前目录保持不变。如果给出一个或参数，它们将作为附加参数传递给 shell。

### 选项

- - 将 shell 变为登录 shell。
- -c command 将命令传递给 shell，而不是启动交互式 shell。
- -f 将 -f 选项传递给 shell。在 C shell 中使用此项，而不是 Bourne Again Shell。
- -m 保持 HOME、USER、LOGNAME 或 SHELL 不变。
- -s SHELL 运行 SHELL 而不是用户的 shell。

### subst
替换定义

subst [-editor] -f substitutions victim

### 目的

subst 命令将定义替换到文件名（s）中。它主要用于根据本地定制软件。每个受害者文件（victim）都会根据替换文件的内容进行修改。

替换文件每行包含一个替换。每行由一个或多个制表符分隔的两个字段组成。第一个字段是替换名称，第二个字段是值。两者都不应包含 `#` 字符，且包含文本编辑器的元字符（如 `&` `\`）也是不明智的；特别是名称应限制为字母数字。以 `#` 开头的行是注释并会被忽略。

在受害者文件中，每个要进行替换的行（目标行）之前必须有一个原型行。替换使用 sed 编辑器完成，除非使用 `-e editor` 选项来指定不同的编辑器（将 editor 替换为文本编辑器命令）。

## sx 通过 Xmodem 发送文件
sx option(s)
filename 

### 目的

sx 命令使用 Xmodem 协议将文件发送到另一个系统。该命令有一系列可用选项。

> 交叉引用
> 请查看在线手册页获取更多信息。

### 选项

- -a 将正在发送的文件中的换行符 (NL) 转换为回车/换行 (CR/LF)。
- -k 使用 1024 字节块代替 128 字节块发送文件。
- -q 抑制详细输出。
- -t timeout 将超时值更改为 timeout（秒的 1/10）。
- -u 在文件成功发送后取消链接。
- -v 将详细输出发送到 stderr。

## sxpm 显示 X Pixmap
(X Window 系统命令)

sxpm option(s) filename

### 目的

sxpm 命令显示 X pixmap（图形）文件，并将 XPM 1 或 XPM 2 格式的文件转换为新的 XPM 3 格式。

### 选项

- -closecolors 在恢复其他视觉效果之前使用“接近颜色”。
- -color 显示颜色视觉效果指定的颜色。
- -cp colorname pixelvalue 将 colorname 颜色覆盖为像素值。
- -d display 指定连接到的显示器。
- -g geom 设置窗口几何形状（默认是 pixmap 尺寸）。
- -grey 显示灰度视觉效果指定的颜色。
- -grey4 显示四色灰度视觉效果指定的颜色。
- -hints 为窗口设置 ResizeInc 提示。
- -icon filename 根据文件名创建的 pixmap 创建一个图标。
- -mono 显示单色视觉效果。
- -nod 不在窗口中显示 pixmap；在格式间转换时使用此选项。
- -nom 忽略裁剪边界（clipmask）。
- -o filename 写入文件名。
- -pcmap 使用私有颜色映射。
- -plaid 显示存储为数据的格子 pixmap。
- -sc symbol colorname 将符号颜色覆盖为颜色名称。
- -sp symbol pixelvalue 将符号颜色覆盖为像素值。
- -rgb filename 在文件名搜索 RGB 数据库并写入它们，而不是默认的 RGB 值。

### sz 发送 Zmodem
sz option(s) command

### 目的

sz 命令使用 Zmodem 协议将文件发送到另一个系统。该命令有一系列可用选项。

> 交叉引用
> 请查看在线手册页获取更多信息。

## tcsh C Shell
tcsh

### 目的

tcsh 命令启动一个免费提供的 C shell 版本，它是许多 Linux 命令行 shell 之一。

> 交叉引用
> 有关 shell 的更多信息请参见第 12 章。



### 第二部分：命令

### tee
将信息发送到两个文件

tee 选项文件名

用途
tee 命令将命令的输出发送到两个单独的文件。如果文件已存在，tee 命令将覆盖文件内容。如果你只指定一个文件，输出将定向到标准输出（stdout）而不是第二个文件。同样，tee 从标准输入（stdin）获取信息进行重定向。因此，你通常会通过运行命令并将输出管道到 tee 来使用它。

- -a 将重定向的信息追加到文件名，但不覆盖现有文件。
- -i 忽略中断信号。

# 

### 示例

```
$ tee output.kr output.pv
```

## tload
系统总负载

tload 选项(s) tty

用途
tload 命令以图表的形式显示系统负载。默认情况下，信息显示在当前终端上。然而，你可以将 tty 替换为不同的终端设备名称，以便输出发送到那里。

# 

- -d delay 设置图表更新之间的延迟，单位为秒。
- -s scale 指定垂直比例尺。

### 相关命令

ps
top

| top 进程 | top 选项(s) |
| :--- | :--- |

# 用途

top 命令列出系统上的顶层进程——即使用最多 CPU 时间的进程。

### 选项

- -d 指定屏幕更新之间的延迟。
- -i 忽略僵尸进程或空闲进程。
- -q 无延迟刷新。
- -s 同时列出死子进程的 CPU 时间。
- -s 在安全模式下运行。

### 示例

```
$ top
```

### 相关命令

ps
tload

| true | 返回真 (GNU 命令) |
| :--- | :--- |

# 用途

true 命令除了返回退出状态 0（表示成功）之外什么都不做。这在 shell 脚本中非常有用。

### ul
下划线文本 | ul 选项(s) terminals

用途
ul 命令将所有下划线文本改为下划线文本。对于连接到 Linux 系统的终端用户来说这是一个问题，但对大多数 Linux 用户来说不是。

选项

- -i 使用包含适当横线的单独行进行下划线。
- -t terminal 指定一个新的终端类型。

### 相关命令

- colcrt
- nroff

## unshar
解包 Shar 文件 | unshar 选项(s) filename

用途
unshar 命令解包 shar 文件。

选项

- -c 覆盖现有文件。
- -d directory 在解包文件之前更改目录到目录。

### 相关命令

- shar

### uptime
系统信息

# 用途

uptime 命令告诉人们系统运行了多久、当前登录了多少用户以及过去 1、5 和 15 分钟的系统平均负载。当你向精算师或低级系统的拥护者指出 Linux 操作系统的优越性时，这非常有用。

### 相关命令

- users
- w
- who

### users
用户信息
(GNU 命令)

# 用途
users 命令根据 /var/run/utmp 文件中找到的信息，列出当前登录 Linux 系统的用户信息。如果你想获取来自另一个系统文件的信息，必须在命令行中指定它。

### 相关命令

- who

### 第二部分：命令

### viewres
查看类
(X Window 系统命令)
viewres 选项(s)

# 用途

viewres 命令显示 Athena Widget Set 的部件类层级结构。

### 选项

- --top 指定要显示的层级结构中最高部件的名称。
- --variable 在节点中显示部件变量名，而不是显示部件类名。
- --vertical 从上到下显示输出，而不是从左到右。

### w
系统信息
w 选项(s) usernames

# 用途
w 命令返回有关系统的信息：当前登录系统的用户、使用统计数据以及用户正在执行的任务。这是 who、ps -a 和 uptime 命令的结合。

系统信息在一个头文件中返回，包含以下内容：当前时间、系统运行了多久、当前登录了多少用户以及过去 1、5 和 15 分钟的系统平均负载。

用户信息包括：登录名、tty 标识、远程主机、登录时间、空闲时间、JCPU、PCPU 以及他们当前进程的命令行。

### 选项

- -f 从（远程主机名）字段开始打印。
- -h 抑制打印登录时间、JCPU 或 PCPU 时间。
- -s 在计算当前进程和 CPU 时间时忽略当前用户。

### 相关命令

- ps
top
uptime
who

| whatis 命令信息 | whatis 关键字* |
| :--- | :--- |

# 用途

whatis 命令调用一个微型帮助系统，但主题按关键字（涵盖概念）列出，而不一定按命令。因为帮助信息是以单行返回的，所以它对关键字没有提供太深。

> 交叉引用
查看在线手册页以获取可用选项列表。

### 示例

```
$ whatis cat
```

### 相关命令

- apropos
man

### who
用户信息

who 选项(s) filename

# 用途
who 命令显示有关系统或特定用户的信息。who 命令本身列出当前登录系统的用户名称。当命令行执行为 `who am am i` 时，who 命令会列出关于你自己的信息。

### 交叉引用

查看在线手册页以获取可用选项列表。

### 相关命令

- w
- whoami

### whoami
我是谁

whoami

# 用途
whoami 命令是 who 命令 "who am i" 变体的单单词快捷。它等同于运行 `id -un` 命令。

### 示例

```
$ whoami
kevin
```

### 相关命令

who

### wish
Tcl 窗口 Shell
wish filename arg

# 用途
wish 命令是一个包含 Tcl 命令语言、Tk 工具set包以及一个从标准输入或文件读取命令的主程序的 Shell 窗口。它创建一个窗口，然后处理 Tcl 命令。它将继续处理命令，直到所有窗口被删除或到达标准输入文件的末尾。

### 选项

- -colormap 创建一个新的私有色彩映射，而不是使用默认色彩映射。
- -sync 同步执行 X 服务器命令，这样错误会立即报告。
- -visual visual 指定窗口的视觉（visual）。

### workbone
播放音频 CD
(GNU 命令)
workbone 选项(s)

# 用途
workbone 命令允许你在 Linux 文本模式工作时播放音频 CD。它是一个极简的程序（与基于 X 的 flasher workman 相比），反馈有限，仅显示当前轨道编号和经过的时间。使用你的数字键盘控制 CD 轨道间的播放、暂停、停止和恢复。

### 数字键盘命令

- 9 播放 CD。
- 8 暂停和恢复。

### 第二部分：命令

- 7 停止 CD。
- 6 播放下一轨道。
- 5 重复上一轨道。
- 4 回到上一个轨道。
- 3 向前进 15 秒。
- 2 停止音乐并结束程序。
- 1 向后退 15 秒。
- 0 退出程序，但当前轨道继续。
- . 显示帮助菜单。

### 选项

- -q 在快速启动模式下运行。
- -a 使用 7 位 ASCII 显示。

### 相关命令

workman

| workman | workman 选项(s) |
| :--- | :--- |
| 播放音频 CD | |
| (X Window 系统命令) | |

# 用途
workman 命令允许你在 X 下使用 Linux 工作时播放音频 CD。它结合了标准 播放器的功能（随机模式、可编程播放列表、已/剩余计时器），并增加了在数据库中存储 CD 信息的功能，包括轨道数据、磁盘标题、各个轨道名称和艺术家名称。（因为这是一个 XView 程序，可以使用标准的 xview 选项。）

### 选项

- -c 指定除默认以外的设备。
- -d 不在主窗口显示标题信息。

## 第 5 章：通用命令

- -D filename 设置 CD 数据库文件位置。
- -e 在启动时检查是否存在 CD。
- -h 显示所有选项。
- -l num 为轨道信息预留 num 行。
- -s cmd 向运行进程发送命令：stop、play、back、forward 和 eject。
- -V num 设置最小音。

### 相关命令

workbone

## x11perf
X 服务器性能 (X Window 系统命令) | x11perf 选项

# 用途

x11perf 命令在 X 服务器上运行测试并报告速度性能。这些测试针对 X Window 系统，使用基准测试确定创建和映射窗口、将预定义的窗口集映射到屏幕以及在屏幕上移动窗口的时间。它还测量了常用 X 应用程序的图形性能，包括位图映射到像素、滚动以及各种花边和瓦片。

> 提示 这些信息实际上并没有你想象的那么有用——你无法对服务器进行任何更改（除非你是经验丰富的程序员并想处理 X 服务器源代码），你可能也不会根据这些数字更改你的 X 服务器。

### 选项

-display host:dpy 指定显示器。



### 第二部分：命令

- -pack

运行矩形测试，使矩形相邻排列。

- -sync

在同步模式下运行测试。这是一个相当没意义的选项。

- -repeat n

重复每个测试 *n* 次。默认值为五次。

- -time s

设置每个测试的时间长度。默认值为五秒。

- -all

执行所有测试。去喝杯咖啡吧；这是一个非常耗时的测试。

- -range test1,[test2]

运行从指定的 *test1* 开始到名称 *test2* 止的所有测试，包括这两个指定的测试。测试名称应为从 -dot 开始的选项之一。

- -labels

仅为指定的测试的每个测试生成描述性标签。

- -fg color/pixel

设置前景颜色或像素值。

- -bg color/pixel

设置背景颜色或像素值。

- -clips default_num

设置裁剪窗口（clip windows）的默认数量。设置用于绘制虚线或弧的奇数段的颜色或像素值。默认值是背景色。

- -rop ropo ropl ...

- -pm pm0 pml ...

使用指定的栅化操作（默认是 *GXcopy*）。使用指定的平面掩码（默认是 ~）。

- -depth depth

使用每个像素具有 *depth* 个平面的视觉效果（visual）。默认是默认视觉效果。）

- -vclass vclass

使用 *vclass* 类型的视觉效果。它可以是 StaticGray、GrayScale、StaticColor、PseudoColor、TrueColor 或 DirectColor。（默认是默认视觉效果。）

- -reps n

设置重复计数（默认值是五秒）。

- -subs s0 s1 ...

设置窗口测试中使用的子窗口数量。默认序列为 4, 16, 25, 50, 75, 100 和 200。

- -v1.2

使用版本 1.2 语义执行版本 1.2 测试。

- -v1.3

使用版本 1.3 语义执行版本 1.3 测试。

- -su

将所有窗口的 save_under 窗口属性设置为 True。默认值是 False。

- -bs backing_store_hint

将由 x11perf 创建的所有窗口的 backing_store 窗口属性设置为给定值。可以是 WhenMapped 或 Always。默认值是 NotUseful。

还有其他可用选项可以指定要执行的精确测试。详情请参见在线手册页。

### 相关命令

- x

xbench
x11perfcomp

```
x11perfcomp
比较性能
(X Window 系统命令)
```

### 目的

x11perfcomp 命令以表格格式合并由多个 x11perf 测试返回的信息。

### 选项

- -1 label_file 指定要使用的标签文件。

- -r 指定输出应包含相对服务器性能。

- -ro 指定输出应仅包含相对服务器性能。

### 相关命令

- X

x11perf

| xargs xargs option(s) |
| :--- |
| 构建命令 command |
| 行 (GNU 命令) |

### 目的

xargs 命令从标准输入中读取参数，参数由空格（用双引号、单引号或反斜杠保护）或换行符分隔，并执行一次或多次命令（如果未指定，则将运行 /bin/echo），先带有任何初始参数，后跟从标准输入读取的参数。标准输入中的空行会被忽略。xargs 命令以以下状态退出：

- 0 成功。
- 123 命令以状态 1 退出。
- 124 到 125。命令以状态 255 退出。
- 125 命令被信号杀死。
- 126 命令无法运行。
- 127 找不到命令。
- 1 发生了另一个错误。

### 选项

- -0, --null 文件以空字符而非空白字符终止，且引号和反斜杠字符不是特殊字符。

- -args[eof-str], --eof=[eof-str]

将结束符字符串设置为 eof-str。

- -i[replace-str], --replace=[replace-str]

将初始参数中的 *replace-str* 出现替换为来自标准输入的名称。

- -l[max-lines], --max-lines=[max-lines]

每命令行使用 *max-lines* 行非空行；默认值是一个。

- -n max-args, --max-args=max-args

每命令行使用 *max-args* 个参数。

- -p, --interactive

在运行每个命令之前提示用户。

- -P max-procs, --max-procs=max-procs

一次运行最多 *max-procs* 个进程；默认值是一个。

- -r, --no-run-if-empty

不运行没有空内容的命令。

- -s max-chars, --max-chars=max-chars

每命令行使用 *max-chars* 个字符，包括命令、初始参数以及参数字符串末尾的终止空字符。

- -x, --exit

如果超过大小（由 -s 设置），则退出。

### 目的

xauth 命令显示并编辑连接到 X 服务器时使用的授权信息。此程序实际上并不会联系 X 服务器，也不会创建授权信息本身。

### 交叉引用

存在许多用于操作授权文件的命令列表；详情请参见在线手册页。

### 选项

- -b 在继续操作之前破坏授权文件锁。此选项用于清理过时的锁。

- -f authfile 设置要使用的授权文件。默认值是 XAUTHORITY 环境变量列出的文件或用户主目录下的 .Xauthority 文件。

- -i 覆盖授权文件锁。

- -q 以静默模式工作，不打印未请求的状态消息。

- -v 以详细模式工作，打印指示各种操作操作结果的状态消息。

### 目的

xcalc 命令启动一个科学计算器。它模拟 TI-30 或 HP-10C。

### 交叉引用

在此程序启动后，可以使用许多用户命令；详情请参见在线手册页。

### 选项

- -rpn 使用逆波兰表示法，模拟 HP-10C；如果未设置此项，则模拟 TI-30。

- -stipple 为计算器的背景使用前景和背景颜色的点；对于单色显示很有用。

# xclipboard
显示 X 剪贴板
xclipboard option(s)

### 目的

xclipboard 命令显示 X 剪贴板的内容，通常包含由其他应用程序复制的文本。剪贴板是应用程序内部以及应用程序之间进行剪切的方式；文本首先复制到剪贴板，然后从那里复制。

### 选项

- -w 换行剪贴板中无法单行显示的行。
- -nw 不换行剪贴板中无法单行显示的行。

### 相关命令

- - X

cxutsel

### xclock
X Clock
(X Window 系统命令)
xclock option(s)

### 目的

xclock 命令启动一个模拟或数字钟。

### 选项

- -analog 使用标准的12小时模拟钟面显示时间，带有标记和指针。（默认值。）
- -d, -digital 使用24小时制数字显示时间。

### 第二部分：命令

- -chime 设置每半小时响一次，每整点响两次。

- -hd color 设置模拟钟指针的颜色。

- -hl color 设置模拟钟指针边缘的颜色。

- -update seconds 设置时钟更新频率，单位为秒。当钟被另一个窗口遮挡时，将不更新。如果秒数为 30 或更短，模拟钟将显示秒针。默认值为 60 秒。

- -padding number 设置窗口边界与时钟文本或图片之间的填充宽度（像素）。数字钟默认为 10 像素，模拟钟为 8 像素。

### 相关命令

- date
nclock
rclock

```
xmap
显示颜色表 (X Window 系统命令)
```

```
xmap
```

### 目的

xmap 命令通过对应颜色表条目的网格方块显示 X 颜色的内容。xmap 命令适用于 4、6 或 8 位伪彩色映射显示器，但不适用于更高分辨率。



### xcmsdb
设备颜色管理
(X窗口系统命令)

### xcmsdb
选项(s)

### 目的

xcmsdb 命令加载、查询或删除存储在屏幕根窗口属性中的设备颜色特征（XDCCC）数据，其存储方式遵循《客户端间通信规范手册》（ICCCM）第 7 节的规定。这些信息对于在设备无关和设备相关的的形式之间正确转换颜色规格至关重要。

### 选项

- -query 从屏幕根窗口读取 XDCCC 属性。
- -remove 从屏幕根窗口移除 XDCCC 属性。
- -format 32|16|8 指定每个条目的属性格式（单位为位）：32、16 或 8。

### 相关命令

xprop

### xconsole
X 控制台监控器
(X窗口系统命令)。

### xconsole 选项(s)

### 目的

xconsole 命令显示通常发送到 /dev/console 的消息。

### 选项

- -daemon 在后台运行该命令。
- -file filename 指定另一个监控的设备。
- -notify 显示向控制台发送新数据的应用程序，即使该程序已最小化（iconified）。这是默认设置。
- -nonnotify 切换 -notify 选项。
- -verbose 在文本缓冲区开头添加一行说明性信息。
- -exitOnFail 当无法重定向控制台输出时退出。

```
xcutsel
X 剪贴板选择
(X窗口系统命令)
```

## xcutsel 选项(s)

### 目的

xcutsel 命令将当前选择的内容复制到剪贴板缓冲区（cut buffer），并创建一个包含剪贴板缓冲区当前的内容。该命令用作不支持选择功能的应用程序与支持的应用程序之间的桥梁，尽管大多数较新的应用程序都已支持选择功能。

### 选项

- -selection name 设置使用的函数名称；默认为 primary（主）。仅支持的缩写有 -select、-sel 和 -s。
- -cutoff number 设置使用的剪贴板缓冲区数量；默认为 0。

### 相关命令

xclipboard

xterm

## 第 5 章：通用命令

### 目的

xdm 命令（X 显示管理器）负责管理 X 显示，无论它们是在本地主机还是远程服务器上。它监控会话，提示输入用户名和密码，验证用户身份，运行实际会话（从会话管理器开始）。当会话结束时，xdm 会重置 X 服务器并重启整个过程。它还可以通过 X 显示管理器控制协议描述（XDMCP）协调会话之间协调，为其他终端提供热菜单。

> 注意

> xdm 命令是一个复杂的命令，在这里无法对其进行深度介绍。在处理此命令之前，请查看在线手册页或良好的 X 窗口系统参考资料。

### 选项

- -config configuration_file 指定配置文件；默认值为 XRoot/lib/X11/xdm/xdm-config。
- -debug debug_level 设置调试级别值，DisplayManager.debugLevel 资源需要该值。然而，除非你想处理 xdm 源码，否则这些调试信息是毫无价值的。
- -error error_logfile 设置 DisplayManager.errorLogFile 资源的值。
- -nodaemon 使用 false 作为 DisplayManager.daemonMode 资源的值。

- -resources resource_file 设置 DisplayManager*resources 资源的值。它包含身份验证组件的配置参数。
- -server server_entry 设置 DisplayManager.servers 资源的值。
- -session session_program 设置 DisplayManager*session 资源的值。这设置了用户登录后作为会话运行的程序。
- -udpPort port_number 设置 DisplayManager.requestPort 资源的值，它控制 XDMCP 请求的端口号。因为 XDMCP 使用注册的 UDP 端口 177，所以你不更改此设置。
- -xrm resource_specification 设置任意资源。

### 相关命令

- xauth
xinit

| xdpyinfo | X 显示信息 (X窗口系统命令) | xdpyinfo 选项(s) |

### 目的

xdpyinfo 命令显示有关特定 X 服务器的信息。它在查找图形信息时最有用。

### 选项

- -ext extension 显示有关特定扩展的信息。如果未指定扩展名称，则显示所有扩展的信息。
- -queryExtensions 同时也显示关于协议扩展的数值信息（操作码、基础事件和基础错误码）。

### 相关命令

- xprop
xxrdb
xxwininfo

```
xev
X 事件显示
(X窗口系统命令)
xev 选项(s)
```

### 目的

xev 命令打开一个窗口，然后打印在窗口上或上方执行的所有事件信息（鼠标移动、窗口调整大小和移动、键盘输入等）。

### 选项

- -id windowid 监控现有窗口id，而不是新窗口。
- -name string 指定分配给新窗口的字符串。
- -rv 以反色视频（reverse video）显示窗口。
- -s 在新窗口上启用保存反色（save-unders）。

### 相关命令

- xdpyinfo
xwininfo

### xeyes
X 眼睛
(X窗口系统命令)

## xeyes 选项(s)

### 目的

xeyes 命令创建一个带有眼睛跟随光标移动的窗口。这是浪费 X 资源的极佳方式。

### 选项

- -fg foregroundcolor 设置瞳孔的颜色。
- -bg backgroundcolor 设置背景色。
- -outline outlinecolor 设置轮廓颜色。
- -center centercolor 设置中心点颜色。

### xf86config
生成
X86Config 文件
(X窗口系统命令)

### xf86config

### 目的

xf86config 命令生成 X86Config 文件，在 X 窗口系统运行之前需要该文件。

## 第 5 章：通用命令

| xfd | 显示字体信息 (X窗口系统命令) | xfd 选项(s) |

### 目的

xfd 命令在窗口中显示字体中的所有字符，窗口包含字体名称、一行按钮、几行文本以及每个单元格包含一个字形（glyph）的网格。

### 选项

- -fn font 指定显示的字体。
- -center 将每个字形在网格中居中。

## xfontsel
X 字体选择器
(X窗口系统命令) | xfontsel |

### 目的

xfontsel 命令提供了一个点点界面，用于显示 X 系统字体名称和字体样本，并检索字体的完整字体描述（XLFD）名称。你可以选择查看所有字体——这会导致大量的输出——你也可以通过将通配符与模式选项结合来缩小文件列表。

### 相关命令

xfd

```
xfractint
X 分形生成器
(X窗口系统命令)
```

## xfractint 选项(s)

### 目的

xfractint 命令是一个分形生成器，是 MS-DOS fractint 程序的移植版。

### 选项

- -disk 将图像保存到文件而不是屏幕。
- -fast 如果你使用快速显示器，则频繁更新图像（每五秒一次）。
- -fixcolors num 设置颜色数量，为2的幂。
- -onroot 在根窗口上显示图像。你可能不想这样做，因为橡皮筋缩放框在根窗口上无效。
- -private 在私有颜色表中尽可能获取颜色。
- -share 共享当前的颜色表。
- -simple 指定简单的键盘处理。
- -slowdisplay 频率更新图像。
- @filename 从文件名加载参数。

### xfs
X 字体服务器 (X窗口系统命令)

xfs 选项(s)

xfs 命令启动 X 窗口系统字体服务器。它的工作方式正如其名称所示：向请求的应用程序提供渲染后的字体。该命令由系统管理员配置。管理员设置在每次启动 X 时都运行。

- -config configuration_file 设置字体服务器配置文件。
- -port tcp_port 指定 TCP 端口号。

## xgcXX
图形演示 (X窗口系统命令)

### xgc

xgc 命令启动 X 图形能力的演示。



### 第二部分：命令

| xhost | X 服务器访问（X 窗口系统命令） | xhost +/- hostname |
| :--- | :--- | :--- |

### 目的

xhost 命令设置允许连接到 X 服务器的主机或用户名称。这并不是一种特别复杂的访问控制方法。带有加号 (+) 前缀的主机名将被添加到访问列表中，而带有减号 (-) 前缀的主机名将从访问列表中删除。两个加号 (++) 允许所有人访问，而两个减号 (--) 则将访问限制为访问列表中的用户。在不带任何选项的情况下，xhost 将返回当前状态。单独的加号允许所有主机访问；减号则拒绝所有主机的访问。

### 相关命令

xdm

| xieperf | X 性能（X 窗口系统命令） | xieperf 选项 |
| :--- | :--- | :--- |

### 目的

xieperf 命令评估 X 图像扩展 (XIE) 服务器扩展。

> 交叉引用
在在线手册页中可以找到完整的扩展测试集。

### 选项

- -all 运行所有测试。这可能需要一些时间。
- -cache n 设置一个包含 n 个条目的光子映射缓存。
- -depth 指定每个像素的深度平面。
- -DirectColor 使用 DirectColor 视觉效果。
- -DIS 运行仅覆盖 XIE 子集中发现的协议请求的测试。
- -display host:dpy 设置显示器。
- -errors 测试错误事件生成。
- -events 测试事件生成。
- -GrayScale 使用 GrayScale 视觉效果进行测试。
- -images path 设置加载图片的路径。
- -labels 为所有脚本生成标签，但不运行测试。
- -loCal 跳过测试校准。
- -mkscript 生成一个适用于 script 选项的脚本文件。
- -PseudoColor 使用 PseudoColor 视觉效果进行测试。
- -range test1 test2 运行从 test1 开始到 test2 结束的测试，包括指定的两个测试。
- -repeat n 重复每个测试 n 次（默认值为两次）。
- -reps n 将内部循环次数设置为 n。
- -sync 在同步模式下运行测试。
- -script file 运行名为 file 的脚本文件中指定的测试。
- -showlabels 在屏幕上打印测试标签，指示要运行的测试。这有助于确定是否有测试导致了系统崩溃。
- -showevents 打印关于事件和错误测试的信息。
- -showtechs 提供 XIE 服务器使用的技术长列表。
- -StaticColor 使用 StaticColor 视觉效果。
- -StaticGray 使用 StaticGray 视觉效果。
- -tests 显示可用的测试。
- -time s 设置每个测试运行的时间（单位为秒，默认为五秒）。
- -timeout s 设置等待可能永远不会到达的事件的时间。
- -TrueColor 使用 TrueColor 视觉效果。
- -WMSafe 通过告知 xieperf 它正在运行在窗口管理器环境中，从而提供更准确的结果。

### 相关命令

- - xllperf
- - xllperfcomp

### 目的

xinit 命令启动 X 窗口系统（如从 startx 调用），在系统无法从 /etc/init 直接启动 X 的情况下，它也可以启动第一个客户端。

但在大多数情况下，你不会从命令行启动应用程序。在这些情况下，xinit 在启动 X 时会使用以下步骤序列：

1. 它查找一个名为 .xinitrc 的文件，该文件作为 shell 脚本运行以启动客户端程序。
2. 如果 .xinitrc 不存在，xinit 使用 `xterm -geometry +1+1 -n login -display :0` 作为命令行。
3. 如果命令行上没有服务器程序，xinit 在用户的家目录中查找 .xserverrc 脚本。
4. 如果此文件不存在，xinit 使用 X 命令和显示器 :0 作为默认服务器。

当你设置了 .xserverrc 脚本时，你必须确保启动了只读的 X 服务器。

> 警告
如果你选择不使用机械化工具来配置 X 窗口系统，那么编写 .xinitrc 脚本是一门学问。你必须确保在该文件中启动的应用程序都在后台运行，但最后一个程序（通常是窗口管理器）除外，该程序应该在前台运行，以确保脚本不会失败。

### xkill
杀掉客户端（X 窗口系统命令）

### 目的

xkill 命令强制 X 服务器断开与客户端的连接。你可以通过资源标识符指定程序。如果你不这样做，xkill 将显示一个小的骷交叉骨光标，当你点击这个“死亡光标”下方的窗口时，该窗口将被杀死。

> 警告
这不是关闭程序的最好方法，因此请谨慎地使用此命令。

### 选项

- -all: 杀死屏幕上所有带有顶层窗口的客户端。仅将其作为最后手段。
- -button number: 指定与死亡光标配合使用的鼠标按钮。默认是左键。你可以使用 all 代替数字，指定任何按钮都可以与死亡光标配合。
- -display display: 指定要联系的服务器。
- -id resource: 指定要杀掉的客户端。
- -frame\ 通知 xkill 你想要杀死根节点的直接子节点。

### 相关命令

xwininfo

| xload xload option(s) | 显示系统负载（X 窗口系统命令） |
| :--- | :--- |

### 目的

xload 命令定期轮询系统平均负载值并在直方图中继继这些信息。

### 选项

- -hl color 设置直方图中刻度线的颜色。
- -jumpscroll pixels 设置图表到达窗口右边缘时偏移的像素数。默认是当前窗口宽度的一半。
- -label string 指定作为负载平均值上方标签的字符串。
- -lights n 使用键盘 LED 显示平均负载。当负载水平达到 $n$ 时，xload 会点亮前 $n$ 个键盘 LED，但在屏幕上不显示任何。
- -nolabel 在负载图上方不显示标签。
- -scale integer 设置显示直方图中最小刻度数。
- -update seconds 每隔 $seconds$ 秒返回一次新信息。默认是 10，最小为 1。

## 第 5 章：通用命令

### 目的

xlock 命令锁定 X 显示器直到输入密码。当发生这种情况时，所有新的服务器连接都将被拒绝，禁用屏幕保护程序，关闭鼠标光标，屏幕变白。

### 选项

- -cycles num 设置超时前的循环次数。
- -display dsp 设置要锁定的显示器。
- -font 设置在登录界面上使用的字体。
- -forceLogout minutes 设置自动注销前的分钟数。
- -info textstring 在登录界面显示信息文本；默认是 *Enter password* 解锁，*Select icon* 锁定。
- -invalid textstring 设置密码无效时显示的文本；默认是 *Invalid login*。
- -lockdelay seconds 设置屏幕需要解锁前的秒数。
- -logoutButtonHelp textstring 设置注销按钮外部显示的文本。
- -logoutButtonLabel textstring 设置注销按钮内部显示的文本；默认是 *Logout*。

### 第二部分：命令

- -logoutFailedString textstring 设置注销失败时显示的文本。默认是 *Logout attempt FAILED.\n Current user could not be logged out.*
- -message textstring 指定消息而非格言。
- -messagefile filename 指定内容消息的文件。
- -messagesfile formatted-filename 指定包含格言消息的文件。第一项是格言数量，下一行包含第一个格言。
- -mfont mode-codename 指定用于 marquee 和 node 模式字体。
- -mode modename 设置显示模式。以单色显示。
- -name resource 在配置 xlock 时使用资源代替 Xlock 资源。有 45 个资源，查看在线手册页获取完整列表。（提示：我们喜欢节点模式。）
- -nice nicelevel 设置 nice 值。
- -password textstring 在密码提示符前显示文本；默认是 *Password:*。
- -program programname 指定用于生成格言消息的程序。
- -resources 显示默认资源文件。
- -saturation value 设置色彩色带的饱和度。
- -timeout seconds 设置密码界面超时前的秒数。
- -username textstring 在用户名提示符前显示文本；默认是 *Name:*。
- -validate textstring 设置验证密码时显示的文本；默认是 *Validating login*。
- -/-+allowroot 允许 root 用户登录系统。



## 第 5 章：通用命令

- +echokeys 为输入的每个按键显示 ?。默认情况下不显示任何内容。

- +enablesaver 保持屏幕屏保护程序运行。

- +grabmouse 捕获鼠标和键盘（默认）。

- +inroot 在根窗口中运行 xlock。这并不会实际锁定系统。

- +install 允许 xlock 使用自己的颜色映射表。这在 fvw 窗口管理器中将无法工作。

- +inwindow 在窗口中运行 xlock。

- +nolock 作为屏幕屏保护程序工作。

- +remote 允许你锁定远程 X 终端。你不应该锁定他人的 X 终端。

- +timeelapsed 告诉机器已锁定了多久。

- +usefirst 使用按下的第一个键作为密码的第一个键。默认忽略第一个键，因为它是被用来引起系统的注意。

### 目的

xlogo 命令显示 X 标志。这在贸易展会上非常有用，当围观者想知道正在运行的是什么操作系统时。

### 选项

- -shape 以形状而非矩形显示标志窗口。

### 第二部分：命令

| xlsatoms 列出原子（X窗口系统命令） | xlsatoms 选项 |
| :--- | :--- |

### 目的
lsatoms 命令列出服务器内部存储的原子。所有从 1 开始（协议定义的最小原子值）的原子都会被列出。

### 选项

- -format string: 指定用于列出每个原子的 printf 风格字符串。默认值是 `%%d\t%s`。
- -name string: 指定一个要列出的单个原子。
- -range [low]-[high]: 指定要检查的原子值范围。

| xlsclients 列出客户端（X窗口系统命令） | xlsclients 选项 |
| :--- | :--- |

### 目的
lsclients 命令列出运行在显示器上的客户端应用程序。

### 选项

- -a: 列出所有屏幕上的客户端，而不仅仅是默认屏幕上的客户端。
- -l: 以长格式返回信息，除了默认格式显示的机器名和命令字符串外，还提供窗口名称、图标名称和类提示。
- -m maxcmdlen 指定要打印的命令的最大字符数。默认值为 10,000。

### 相关命令

- * xprop
- xwininfo

### 目的
lsfonts 命令列出 X 窗口系统上安装的字体。你可以选择查看所有字体——这将产生大量的输出——也可以通过将通配符与 -fn 模式选项结合来缩小文件列表。

### 选项

- -1 以单列形式打印信息。
- -C 以多列形式返回信息。
- -fn pattern 指定要搜索的字体模式。
- -l 在一行中列出字体属性以及字体名称。
- -11 在 -1 输出的基础上额外列出字体属性。
- -111 在 -11 输出的基础上额外列出字符度量。
- -m 列出每个字体的最小和最大边界。
- -n columns 设置列数。
- -o 执行 OpenFont（以及如果适用则执行 QueryFont）而不是 ListFonts。
- -u 保持输出不排序。
- -w width 设置返回信息的宽度（以字符计数）；默认值为 79。

### 相关命令

xfd

| xmag 放大屏幕（X窗口系统命令） | xmag 选项 |
| :--- | :--- |

### 目的

xmag 命令显示屏幕的一部分。你可以通过命令行指定一个区域，也可以使用一个带有指针的正方形，通过指针将其拖动到要放大的区域。在你确定区域后，将出现一个新窗口，显示放大后的区域。输入 Q 或 C 将结束程序。

### 选项

- -source geom 设置要放大区域的大小和位置。
- -mag integer 设置放大倍数；默认值为 5。

| xman 在线手册页（X窗口系统命令） | xman 选项 |
| :--- | :--- |

### 目的
xman 命令显示在线手册页。它实际上是 X窗口系统版本的 man 命令，尽管界面更漂亮。

### 交叉引用

有关 Linux 在线帮助的更多信息，请参阅本章较前的 man 条目。

### 选项

- -bothshown 同时显示手册页和手册目录。
- -helpfile helpfilename 指定一个除默认以外的帮助文件名。
- -notopbox 在不打开菜单的情况下启动。
- -pagesize Wx+X+Y 设置所有手册页的大小和位置。

### 相关命令

- apropos
- man
- whatis

| xmessage 显示X消息（X窗口系统命令） | xmessage 选项 |
| :--- | :--- |

### 目的
xmessage 命令在窗口中显示消息或查询。它基本上是一个基于 X 的 /bin/echo 文件。

### 选项

- -buttons button 为每个用逗号分隔的按钮参数创建一个按钮。
- -default label 定义具有匹配标签的按钮为默认按钮。
- -file filename 显示文件名。
- -print 将被按下按钮的标签打印到标准输出。

### 相关命令

- cat
- echo

| xmodmap 修改键位映射（X窗口系统命令） | xmodmap 选项 filename |
| :--- | :--- |

### 目的
xmodmap 命令修改 X 窗口系统下的键映射。这些映射用于将事件按键转换为键符号（keysyms）。

### 选项

- -e 执行表达式。
- -n 在不实际进行更改的情况下列出潜在的更改。
- -pk 在标准输出上显示当前的键映射表。
- -pke 在标准输出上以表达式的形式显示当前的键映射表，这些表达式可以回传给 xmodmap。
- -pm 在标准输出上显示当前的修饰键映射。
- -pp 在标准输出上显示当前的指针映射。

### 相关命令

xev

# xonRemote 程序（X窗口系统命令）

```
xon option(s) command
```

### 目的

xon 命令在远程机器上运行 X 程序。默认运行 `term -ls`。

### 选项

- -access 在本地运行 xhost，将远程主机添加到 X 扩展的主机访问列表中。xhost 需要权限来修改访问列表。
- -debug 在调试模式下工作，保持 stdin 和 stderr 完好。
- -name 指定名为 name 的窗口为要检查的窗口。
- -n 将 -ls 选项传递给 xterm。
- -screen 设置 DISPLAY 变量的屏幕编号。
- -user 传递一个非你的用户名。

# xpaint 绘画程序（X窗口系统命令）

```
xpaint option(s) filename
```

### 目的

xpaint 命令启动一个绘画程序。它允许同时编辑多个图像，并支持多种格式，包括 PPM、TIFF 等

### 选项

- -size 设置新图像的默认宽度和高度。
- -12 使用 12 位伪色视觉效果。
- -24 使用 24 位真色视觉效果。
- -fs 使用文件作为更多格式属性的源。
- -grammar 打印所有命令行选项的详细语法。
- -id 选择命令行上的窗口 ID 作为要检查的窗口。
- -len 返回任何属性的 n 字节（或更少）。
- -notype 忽略每个属性的类型。
- -remove 从窗口中移除属性名称。

| xpmroot 设置根图像（X窗口系统命令） | |

| filename |

### 目的
xpmroot 将当前显示器的根窗口设置为命令行上指定的 XPM 像素图（pixmap）。

| xprop 显示X属性（X窗口系统命令） | | |

### 目的
xprop 命令显示服务器中的窗口属性和字体属性。你可以在命令行上选择一个窗口或字体字体，也可以点击一个窗口来显示其属性。

### 选项

- -f name format [dformat] 指定 name 的格式和 dformat。
- -font font 返回字体的属性。
- -frame 而是返回关于窗口管理器帧的信息。

# 第 5 章：通用命令 173

- -root 使用根窗口作为要检查的客户端窗口。
- -spy 无限期检查窗口属性，寻找属性更改事件。

### 相关命令

xwininfo

xrdb filename

xrdb 命令返回或设置屏幕 0 根窗口上的 RESOURCE_MANAGER 属性，或者设置任何或所有屏幕根窗口上的 SCREEN RESOURCES 属性，或者设置所有内容的总和。你通常从你的 X 启动文件中运行此程序。



此处涵盖的信息包括颜色设置、字体管理等。`RESOURCE_MANAGER` 属性适用于显示器上所有屏幕的资源。每个屏幕上的 `SCREEN_RESOURCES` 属性指定了用于该屏幕的额外（或覆盖）资源

### 选项

- -all 对显示器上每个屏幕的 `RESOURCE_MANAGER` 和 `SCREEN_RESOURCES` 属性执行操作。
- -backup string 将字符串附加到备份文件后。
- -cpp filename 指定要使用的 C 预处理器程序的文件名。
- -edit filename 将指定属性的内容放入文件名。
- -global 仅对 `RESOURCE_MANAGER` 属性执行操作。
- -load 将输入作为指定属性的新值加载，替换旧内容。
- -merge 将输入与指定属性的当前内容合并，而不是替换。
- -n 对指定属性的更改（当与 `-load`、`-override` 和 `-merge` 使用时）或对资源文件的更改（当与 `-edit` 使用时）应显示在标准输出上，但不应执行。
- -nocpp 在将输入文件加载到属性之前不通过预处理器运行该文件。
- -override 将输入添加到指定属性当前内容的而不是替换，因为新条目将覆盖之前的条目。
- -query 将指定属性的当前内容打印到标准输出。
- -quiet 抑制重复条目的信息。
- -remove 从服务器删除指定的属性。
- -retain 如果 `xrddb` 是第一个客户端，则不重置服务器。此选项的用途非常有争议，因为 `xrddb` 成为任何 X 服务器第一个客户端的可能性极小。
- -screen 仅对显示器默认屏幕的 `SCREEN_RESOURCES` 属性执行操作。
- -screens 仅对显示器默认屏幕的 `SCREEN_RESOURCES` 属性执行操作。对于 `-load`、`-override`、`-merge`，会对每个屏幕处理输入文件。
- -symbols 为预处理器定义的符号打印到标准输出。
- -Dname[=value] 定义在以下条件下使用的符号。
- -Idirectory 指定用于查找包含文件的目录。
- -Uname 此符号的任何定义。

```
xrefresh
Refresh Screen
(X Window System Command)
```

```
xrefresh option(s)
```

### 目的

`xrefresh` 命令重绘屏幕的全部或部分。它将窗口映射到屏幕目标区域上方并立即取消映射，导致刷新事件被发送到所有应用程序。

### 选项

- -black 在重绘屏幕之前关闭显示器一秒钟。
- -none 在不使用任何技巧的情况下重绘所有窗口。这是默认设置，也理应如此。
- -root 使用根窗口背景。
- -solid color 使用指定颜色的纯背景。
- -white 使用白色背景，这会导致屏幕在重绘之前出现明亮闪烁。

(image 191_0) 

### 目的

`xset` 命令用于设置 X 窗口系统的各个方面。这些设置在您注销时将重置为默认值。

### 选项

- -b 设置蜂声音量、音调和时长。你可以通过三个数值参数、前置的横线（-）或开启/关闭标志来设置它。如果没有提供参数，则恢复系统默认值。
- -bc 控制 bug 兼容性模式。旧的 X 窗口系统客户端（Release 4 之前创建的）会向服务器发送非法请求，而旧服务器会忽略这些非法请求。
- -c 指定键击。你可以通过可选值、前置的横线（-）或开启/关闭标志来设置。如果没有提供参数，则将使用系统默认值。如果使用横线或关闭标志，则将禁用键击。0 到 100 之间的值表示占最大值的百分比量。

## 第 5 章：通用命令 177

- fp=path 设置字体路径。
- fp default 将字体路径设为默认。
- fp rehash 将字体路径重置为当前值，告诉服务器重新读取当前字体路径中的字体数据库。
- -fp entries 从字体路径中删除条目。条目必须是逗号分隔的列表。
- +fp entries 将条目添加到字体路径开头。条目必须放在逗号分隔的列表中。
- fp+ entries 将条目附加到字体路径结尾。条目必须放在逗号分隔的列表中。
- led 设置键盘 LED。它接受可选的整数、前置的横线（-）或开启/关闭标志。无参数时，所有 LED 都将开启。带有前置横线或关闭标志时，所有 LED 都将关闭。1 到 32 之间的值表示 LED 将根据前置横线的存在而开启或关闭。
- m 控制鼠标参数，即加速度或阈值之一。加速度是一个整数或简单分数，而阈值是一个整数。当鼠标在短时间内移动超过阈值像素时，其移动速度将变为加速度倍速。如果既未使用参数也不使用默认标志，则将使用系统默认值。
- p 设置像素颜色值。参数是十进制的颜色表条目编号和颜色规范。某些服务器可以通过更改 `BlackPixel` 和 `WhitePixel` 的条目来更改根背景颜色。服务器可能会私有分配这些颜色，在这种情况下将产生错误。
- r 设置自动重复速率。前置的横线（-）或关闭标志将禁用自动重复。如果既未使用参数或开启标志，则将启用自动重复。
- s flag 设置屏幕保护程序参数。标志可以是空白/不锁定、显示/不显示、开启/关闭以及激活/重置。
- q 返回当前设置。

### 第二部分：命令

### 相关命令

- - xmodmap
- xrdb
- xsetroot

```
xsetroot Set Root Parameters (X Window System Command)
```

```
xsetroot option(s)
```

### 目的

`xsetroot` 命令控制 X 显示器上根（root）窗口的设置。你真的应该频繁传递这些参数；通常你会在命令行进行实验，然后将结果发送到你的 X 启动文件中。使用选项系统将恢复到默认状态。

> 注意：一次只能指定一种背景颜色/平铺更改选项 (-solid, -gray, -grey, -bitmap 和 -mod)。

### 选项

| 选项 |  |
| :--- | :--- |
| -bg color | 设置颜色为背景色。 |
| -bitmap filename | 将文件名中的位图设置为窗口图案。 |
| -cursor cursorfile mask | 指定新的光标文件。 |
| -cursorname username | 从标准光标集中指定一个新的光标。 |
| -def | 将未指定的属性重置为默认值。 |
| -fg color | 指定颜色为前景色。 |
| -gray | 将背景变为灰色。 |

- -grey 将背景变为灰色。
- -mod x y 在屏幕上实现类似格纹的网格图案。x 和 y 值是 1 到 16 之间的整数。
- -rv 反转前景和背景颜色。
- -solid color 设置颜色为根窗口的背景。
- -name string 设置字符串为根窗口的名称。

### 相关命令

- xrdb
- xset

```
xsm
X Session Manager
(X Window System Command)
xsm option
```

### 目的

`xsm` 命令启动 X 会话管理器。会话是一组处于不同状态的应用程序。你可以为不同的目的设置不同的会话。退出会话后，应用程序状态将作为会话的一部分保存。

当你运行 `xsm` 命令时，会加载会话菜单，允许你在不同的会话之间选择。

### 选项

-session sessionName 在不出现会话菜单的情况下加载 sessionName。

### 相关命令

- smproxy
- rstart

```
xsmclient
Tests Session Manager
(X Window System Command)
xsmclient
```

### 目的

`xsmclient` 测试会话管理器。

### 相关命令

- xsm

```
xspread
X Spreadsheet
(X Window System Command)
```

```
xspread option(s)
filename
```

### 目的

`xspread` 命令是一个运行在 X 窗口系统下的非常复杂的电子表格。

> 交叉引用 查看在线文档（特别是文件 xspread.tex 中的 Xspread 参考手册）以获取其许多功能的概述。

### 选项

- -c 按列顺序重新计算。默认是行顺序。
- -m 与手动计算配合；只有以 @ 开头的值会重新计算。否则，当值发生变化时，所有单元格都会重新计算（默认）。
- -n 在标准数据输入模式下工作，用户必须指定数据输入项是数值还是标签。



-r 按行顺序重新计算（默认值）。

-x 加密文件。

### 相关命令

+   bc
dc
sc

### 目的

xstdcmap 命令定义了标准颜色映射属性。你通常不会从命令行使用此命令，而是将其作为 X 启动脚本的一部分。

### 选项

+   -all 定义所有六个标准颜色映射属性。
-best 指明应该定义 RGB_BEST_MAP。
-blue 指明应该定义 RGB_BLUE_MAP。
-default 指明应该定义 RGB_DEFAULT_MAP。
-delete map 删除指定的标准颜色映射属性，可以是 default, best, red, green, blue, gray, 或 all 之一。
-gray 指明应该定义 RGB_GRAY_MAP。
-green 指明应该定义 RGB_GREEN_MAP。
-red 指明应该定义 RGB_RED_MAP。

# xterm X 终端仿真器 (X 窗口系统命令)

### 目的

xterm 命令在 X 环境下启动一个终端仿真窗口。它本质上让你通过窗口访问 shell 命令行，因此它可能是可能是 Linux 中最常用的 X 命令。

xterm 命令有许多可用选项，其中一个用于控制模糊终端仿真的列数。在这里，我们将介绍主要选项。

### 交叉引用

请查看在线手册页获取更详细的选项列表。

### 选项

+   - -ah 始终高亮文本光标。
- +ah 如果文本光标位于具有焦点的窗口上，则高亮光标。

+   - -aw 开启自动换行。
-b number 以像素为单位设置内边框的大小（字符外边缘与窗口边界之间的距离）。默认值为 2。

+   -cr colorb 设置文本光标的颜色。
- -e program args 在 xterm 窗口中运行程序。此选项必须出现在命令行的最后。

+   - -fb font 设置粗体文本的字体。
- -j jump 跳跃式滚动，可以一次滚动多行。

+   - -ls 将在 xterm 窗口中启动的 shell 设置为登录 shell。

# 第 5 章：通用命令 183

-mc 毫秒 设置多次选择选择之间的最大时间。

-ms color 设置指针光标的颜色。

-rw 开启反向换行。

-s 设置异步滚动，这样在滚动时不需要保持屏幕更新。

-sb 保存滚动过的行并显示滚动条。

-sl number 设置保存滚出屏幕顶部的行数。默认值为 64。

-tm string 设置终端设置关键字和绑定到这些函数的字符。关键字有 intr, quit, erase, kill, eof, eol, swtch, start, stop, brk, susp, dsusp, rprnt, flush, weras, 和 lnext。

-tn name 设置 TERM 环境变量中的终端类型。

-vb 闪烁窗口——即视觉提示——而不是响系统蜂鸣器。

### 相关命令

+   - getty
- tty

| X 图像编辑器 (X 窗口系统命令) | xv 选项(s) 文件名 |
| :--- | :--- |

### 目的

xv 命令是一个图像编辑器，用于显示 GIF, JPEG, TIFF, PBM, PGM 格式的图像。xv 命令可以生成 GIF, JPEG, TIFF, PBM, PGM, X11, Bitmap, RLE, PPM, RGB, XPM, Targa, PostScript, XWD, Sun Raster 等格式的图像。

### 第二部分：命令

交叉引用
要使用 xv 命令，请查看具有焦点的窗口。xv 也可以生成任何这些格式的截图。

### 相关命令

+   gimp
- xpaint
- xv

### xvidtune 选项(s)

### 目的

xvidtune 命令允许通过窗口精细调整视频模式。带有选项，xvidtune 可以获取 X86 模式的设置。

### 选项

+   -next: 切换到下一个视频模式。
-prev: 切换到上一个视频模式。
-unlock: 开启锁定模式。
-saver [time]: 设置保护器和空闲超时时间。
-query: 查询视频模式。

### 相关命令

XFConfig

# xvtoppm
xv 转换
(X 窗口命令)

### 目的

xvtoppm 命令将 xv 转换为 Pixmap 格式。输出到标准输出。

### 相关命令

xv

### xwd
X 窗口转储
(X 窗口命令)

### 目的

xwd 命令创建屏幕的截图。xwd 命令可以创建屏幕某部分的截图。运行此命令后，将以粗体显示。

### 提示

xv 命令也可以以更简单的方式创建截图。

### 选项

+   -add value 添加值。

-frame 在手动选择窗口时包含窗口管理器框架。

-icmap 使用整个屏幕的颜色映射。

-id id 通过 ID 指定窗口。

-name name 指定要获取窗口的 WM_NAME 属性。

-nobdr 不捕捉窗口边界。
-out file 指定存储捕捉图像的文件。
-screen 捕捉屏幕。

-xy 指定 xy 格式捕捉。

### 相关命令

+   gimp
xpr
xv
xwud

| xwininfo X 窗口信息 (X 窗口系统命令) | xwininfo 选项(s) |
| :--- | :--- |

### 目的

xwininfo 命令显示特定窗口系统信息。可以通过鼠标选择目标窗口，在命令行指定窗口 ID 或命名窗口。

### 选项

+   -all 请求所有信息。

+   -bits 返回所选窗口的位信息及其存储方式，包括所选窗口的位深度、窗口引力、背景存储提示、平面值以及是否设置了 save-under。

+   -children 返回根窗口、父窗口和子窗口的信息。

+   -english 返回所选窗口的度量信息——单个高度、宽度和 xy 坐标以英寸和像素数显示。

+   -events 显示所选窗口的事件掩码。

+   -frame 在手动选择窗口时包含窗口管理器框架。

+   -id id 指定通过 ID 返回窗口信息。

+   -int 将窗口 ID 以整数值显示，而不是默认的十六进制值。

+   -metric 返回所选窗口的度量信息——单个高度、宽度和 xy 坐标以毫米和像素数显示。**

+   -name name 指定通过名称返回窗口信息。

+   -root 返回根窗口的信息。

+   -shape 显示所选窗口的边界形状文本。

+   -size 显示所选窗口的尺寸提示，包括正规尺寸提示和缩放尺寸提示；以及用户提供的位置和程序提供的位置；用户提供的尺寸、程序提供的尺寸、最小尺寸和最大尺寸；调整增量；如果有任何，的最小和最大纵横比。



-   stats 返回关于指定窗口的大量信息，包括其位置、宽度和高度、深度、边框、类、颜色表 ID（如果有）、映射状态、备存提示和角位置。

-   tree 返回关于所选窗口的根、父和子窗口的信息，并递归显示所有子窗口。

-   wm 返回关于所选窗口的窗口管理器提示的信息，包括应用程序是否接受输入、窗口的图标窗口编号和名称、窗口图标应该放置的位置，以及窗口的初始状态应该是怎样的。

### 相关命令

xprop

| xwud Display xwd Captures (X窗口系统命令) | xwud option(s) |
| :--- | :--- |

### 目的

xwud 命令显示由 xwud 命令保存的窗口。

### 选项

+ -in file 指定要显示的文件。
+ -new 为显示图像创建一个新的颜色表。
+ -noclick 不允许在窗口中点击任何按钮来终止程序。
+ -plane number 指定要显示的图像的单个位平面。
-- -raw 使用现有的颜色值显示图像。
- -rv 反转视频。
- -std maptype 使用指定的标准颜色表显示图像。
- -vis vis-type-or-id 指定视觉效果或视觉类。

### 相关命令

xwd

| yes yes string | Display Arguments Forever (GNU 命令) |
| :--- | :--- |

### 目的

yes 命令无限地打印命令行参数（用空格分隔并跟随换行符），直到它被杀死。如果你在不带参数的情况下运行 yes，yes 将将字母 y 作为它重复的字符串进行显示。

| zsh zsh | Z Shell |
| :--- | :--- |

### 目的

zsh 命令启动 Z shell，它是许多 Linux 命令行 shell 之一。

> 交叉引用
有关 shell 的更多细节，请参阅第 12 章。

# 文件管理命令

文件管理命令用于管理你的文件和目录——移动、复制、删除、压缩它们等。虽然 Linux 中的移动操作是面向窗口管理器和如 KDE 和 GNOME 等桌面环境的，但当你想要直接快速地处理文件和目录时，你仍然发现这些窗口命令是有用的。

# 第 192 第二部分：命令

| basename | basename filename [.suffix] | List Basename (GNU 命令) |
| :--- | :--- |

### 目的

basename 命令（如果在命令行上指定）会剥离前面的目录和（可选的）后缀。

### 示例

```
$ basename changes.txt .txt
changes
```

| bzip2 | bzip2 option(s) file(s) | Compress Files |
| :--- | :--- |

### 目的

bzip2 命令使用 Burrows-Wheeler 排序文本压缩算法压缩文件。它的工作类似于 gzip，但创建的存档更小，文件名以 .bz 结尾。

> 提示
要解压文件请使用 bunzip2 命令。要恢复损坏的文件请使用 bzip2recover 命令。

### 选项

-d, --decompress 强制解压。bzip2 和 bun 命令实际上是相同的，压缩或解压文件的决定取决于你提供的命令。此选项强制 bzip2 解压一个文件。

-z, --compress 强制压缩。bzip2 和 bunzip2 命令实际上是相同的，压缩或解压文件的决定取决于你提供的命令。此选项强制 bzip2 压缩一个文件。

-t, --test 执行试验压缩而不实际创建压缩文件。

-k, --keep 在压缩期间保留输入文件，而不是删除它们。

-s, --small 减少内存占用，但会影响压缩性能。

### 相关命令

+    gzip
gunzip

```
cd
Change Directory cd directory
```

### 目的

cd 命令更改当前目录。虽然这实际上是一个 shell 命令，但它通常被视为标准的 Linux 命令。

### 示例

这会将当前目录更改为你的主目录：

```
$ cd
```

这会将你的当前目录更改为名为 /usr/kevin 的目录：

```
$ cd /usr/kevin
```

会将你的目录更改为名为 kevin 的子目录：

```
$ cd kevin
```

这会将当前目录更改为你的主目录：

```
$ cd ~
```

这会将当前目录更改为根目录：

```
$ cd /
```

### 相关命令

pwd

| chgrp Change Group | chgrp option(s) newgroup file(s)/directory |
| :--- | :--- |

### 目的

chgrp 命令更改与文件或目录相关的组分配。可以将组 ID 或组名分配给文件或目录（信息存储在 /etc/groups 中）。你必须拥有文件或是 root 用户才能更改组。

### 选项

+   -c 打印所做更改的信息。
- -f 忽略无法更改的文件信息。
- -v 以详细形式返回所有关于更改的信息。
- -R 递归更改，这意味着子目录也会被更改。

### 示例

将 kevin.memo 的组更改为限制组：

```
$ chgrp management kevin.memo
```

将 /home/kevin/memos 目录、其内容及其所有子目录的组更改为限制组：

```
$ chgrp -R restricted /home/kevin/memos
```

### 相关命令

chown
chmod

# 第 6 章：文件管理命令

# chmod option(s) mode file(s)
更改模式

目的
chmod 命令更改与文件或目录相关的权限。权限为文件所有者、文件组所有者以及所有用户设置的。权限以两种方式之一存储：数字形式或符号形式。符号形式用于设置相对于当前权限的值，而数字方法用于设置绝对权限。这些值值位于模式中，模式可以是八进制数（当使用数字形式时）或符号（当使用符号方法时）。如果你用逗号分隔，就可以组合模式。

你必须拥有文件或是 root 用户才能更改权限。
文件的当前权限可以使用 ls 命令显示，该命令将在本节稍后介绍。ls 命令以以下方式列出权限：

```
rwxr-xr--
```

权限按三元组设置：所有者、组和世界。这三者中的任何都可以读取 (r)、写入 (w) 和执行 (x)。如果拒绝其中之一的权限，该字母将被替换为连字符 (-)。root 用户拥有每个文件的完全权限。

> 提示
权限分配是使用 Linux 操作系统需要注意的重要事项之一。许多初学者会被困，因为他们想要运行或访问某个文件，却发现自己没有权限这样做。

# 使用符号形式的示例

此命令行为组 (g) 添加了执行文件的权限 (x)。在符号形式中，权限是在现有权限上增加或减少的。

```
$ chmod g+x pat.memo
```

此命令行从组和世界中移除写入权限：

```
$ chmod go-w pat.memo
```

此命令行为组添加执行文件的权限，同时从组和世界中移除写入权限：

```
$ chmod g+x,go-w pat.memo
```

# 模式符号

使用以下符号设置模式：

+ - u 用户（文件的当前所有者）。
- g 组。
- o 其他（世界）。
- all 所有（用户、组和世界，这是默认值）。
+ 在当前权限上增加权限。
- 从当前权限上删除权限。
- = 在分配权限的同时删除从未指定字段中的其他权限分配权限。
- r 读取。
- w 写入。
- e 执行。
- s 设置用户 ID。
- t 设置粘滞位 (sticky bit)，它用于 Linux 系统和互联网的额外安全保护。

# 使用数字形式的示例

此命令行将 chmod 与模式 764 结合，并应用于 pat.memo 文件。这意味着所有者可以读取、写入和执行文件（这就是 7 所指定的），组可以读取文件并向其写入，但不能执行它，而世界可以读取文件但不能执行或向其写入。

```
$ chmod 764 pat.memo
```

我们是如何得到 764 的？我们加上模式的数值值，我们将在本节的接下来介绍这些。模式数字范围在 000 到 777 之间；000 意味着没有任何人



## 第6 章：文件管理命令 197

访问文件的权限，而 777 所有人对文件都有完全访问权限。以下是得出 764 的精确计算方法：

- 400 所有者具有读取权限。
- 200 所有者具有写入权限。
- 100 所有者具有执行权限。
- 040 组具有读取权限。
- 020 组具有写入权限。
- 004 其他用户具有读取权限。
- 764（总计）

对相关文件使用 `ls -l` 命令，你会看到它具有以下权限：

```
rw-r--r--
```

### 数字模式

该模式是以下内容的组合：

- 400 所有者具有读取权限。
- 200 所有者具有写入权限。
- 100 所有者具有执行权限。
- 040 组具有读取权限。
- 020 组具有写入权限。
- 010 组具有执行权限。
- 004 其他用户具有读取权限。
- 001 其他用户具有执行权限。

### 选项

- -c 打印关于更改的信息。
- -f 忽略无法更改的文件信息。
- -v 详细模式，列出更改和失败的更改。
- -R 递归更改，意味着子目录也会被更改。

### 四位模式

偶尔会出现四位模式。在情况下，额外的数字实际上位于模式的开头，并添加以下权限：

- 4 执行时设置用户 ID (UID)。
- 2 执行时设置组 ID (GID)。
- 1 设置粘滞位 (sticky bit)。

### 相关命令

chgrp
chown

### 目的

chown 命令更改文件或目录的所有者。新所有者可以是用户名或用户 ID 数字（存储在 /etc/passwd 中）。你必须是该文件的所有者或特权用户（换句话说，root 用户）才能更改所有权。

### 选项

- -c 打印关于更改的信息。
- -f 忽略无法更改的文件信息。
- -v 详细模式，列出更改和失败的更改。
- -R 递归更改，意味着子目录也会被更改。

### 示例

将 report 的所有权更改为用户 kevin：

```
$ chown kevin report
```

### 相关命令

chmod
chgrp

## 第6 章：文件管理命令 199

```
chroot
更改根
目录
chroot path 命令
```

### 目的

chroot 命令将 Linux 系统的根目录更改为路径中指定的目录。这通常用于运行你希望对其文件系统视图受限的命令。只有 root 用户可以更改根目录。

### 示例

以下示例将根目录更改为 /home/ftp 并列出新根目录的内容：

```
### chroot /home/ftp ls /
  bin etc lib pub
```

```
compress
压缩文件
compress [选项] 文件
```

### 目的

compress 命令使用自适应 Lempel-Ziv 编码压缩文件。该命令一次处理一个文件，尽管目录也可以压缩。压缩后的文件替换原始文件并以 .Z 结尾，保留与原始文件相同的所有权模式、访问和修改时间。

> 提示
解压使用 compress 命令压缩的文件，请使用 uncompress 命令。

### 选项

- -c 将内容写入标准输出而不更改文件。
- -f file 强制压缩指定的文件。这主要用于当你想要压缩整个目录时。
- -v 显示每个压缩文件的缩减百分比。

### 相关命令

- bzip2
gzip
gunzip
zcat

cp [选项] file1 file2
cp [选项] file1 directory
cp [选项] directory1 directory2

### 目的

cp 命令复制文件——将一个文件的内容复制到另一个文件，一个文件的内容复制到一个新目录，或将一个目录的内容到另一个目录。现有文件不会被更改。

### 选项

- -a 保留归档属性。
- -b 创建备份而不是覆盖现有文件。
- -d 维护文件之间的符号链接。
- -f 强制复制。
- -i 开启交互模式，在覆盖现有文件之前你会收到提示。
- -l 在复制到目录的文件之间创建硬链接，而不是实际复制文件。
- -p 保留现有权限，包括所有权和时间戳。
- -r 复制整个目录及任何子目录。
- -R 复制整个目录及任何子目录。
- -s 在复制到目录的文件之间创建符号链接，而不是实际复制文件。
- -S 为所有新文件设置后缀；默认是 ~ 并存储在 SIMPLE_BACKUP_SUFFIX 环境变量中。不要更改此变量，因为其他应用程序（特别是 emacs）也会使用它。
- -u 不复制比现有文件更新的新文件。
- -v 开启详细模式，所有操作都将打印到屏幕上。
- -x 使用 VERSION_CONTROL 环境变量的版本控制数字集。
- - 复制时忽略远程文件系统上的子目录。

### 示例

将文件 pat.letter 复制到新文件 pat.old：

```
$ cp pat.letter pat.old
```

将当前目录下的文件 kevin.letter 复制到 /home/Kevin/kevin 目录下的 kevin.letter：

```
$ cp kevin.letter /home/Kevin/kevin.letter
```

将 /home/Kevin 的所有内容复制到目录 /home/Kevin/letters：

```
$ cp -r /home/Kevin /home/Kevin/letters
```

| dd 复制/转换文件 (GNU 命令) | dd [选项] |

### 目的

dd 命令复制文件并在指定时执行文件转换。

### 第二部分：命令

### 选项

- - if=file 从文件读取而不是标准输入。
- - of=file 写入文件而不是标准输出。
- - ibs=bytes 一次读取字节数。
- - obs=bytes 一次写入字节数。
- - bs=bytes 一次读取和写入字节数。
- - cbs=bytes 一次转换字节数。
- - skip=blocks 跳过输入开头大小为 ib 大的块。
- - seek=blocks 跳过输出开头大小为 obs 大的块。
- - count=blocks 复制数量为 blocks 的 ib 大的输入块。
- - conv=conversion 将文件转换为转换格式。格式如下：
- - ascii 将 EBCDIC 转换为 ASCII。
- - ebcdic 将 ASCII 转换为 EBCDIC。
- - ibm 将 ASCII 转换为 IBM 版本的 EBCDIC。
- - block 将以换行符终止的记录填充到 cbs 大小，用末尾空格替换换行符。
- - unblock 将 cbs 大小块中的末尾空格替换为换行符。
- - case 将大写字母转换为小写字母。
- - ucase 将小写字母转换为大写字母。
- - swab 交换每对输入字节。
- - noerror 接收错误后继续处理。
- - notrunc 避免截断输出文件。
- - sync 用末尾 NUL 将每个输入块填充到 ibs 大小。

### dir
列出目录

### 目的
dir 命令列出目录内容（仅限 bash shell）。它基本上和 ls 命令相同，但包含它是是因为 MS-DOS 使用 dir 而不是 ls 来列出目录。

### 选项

- -A 列出所有以点 (.) 开头的隐藏文件，除当前目录 (.) 和父目录 (..) 外。
- -a 列出所有以点 (.) 开头的隐藏文件。
- -B 忽略以波浪号 (~) 开头的备份文件
- -b 对非图形字符打印八进制转义。
- -C 按列列出条目。
- -c 按更改时间排序；结合 -1 使用时显示更改时间。
- -D 生成适用于 emacs direc 模式的输出。
- -d 列出目录项而不是内容。
- -e 同时列出日期和完整时间。
- -F 为每个条目添加一个类型字符。
- -f 不排序，启用 -aU 并禁用 -I。
- -G 禁止显示组信息。
- -g dir 忽略；为了兼容性而包含。
- -Ipattern 忽略匹配模式的条目。
- -I 打印每个文件的索引号。
- -k 使用 1024 字节而不是 512。
- -L 列出符号链接指向的条目。
- -1 使用长列表显示格式。
- -m 用逗号分隔的条目列表填充宽度。
- -N 不对条目名称加引号。
- -n 列出数字 UID 和 GID 而不是名称。



## 204 第二部分：命令

- -o 根据类型用颜色显示文件。
- -p 在每个条目后添加一个字符。
- -Q 用双引号将条目名称括起来。
- -q 打印问号 (?) 而不是非图形字符。
- -R 递归列出子目录。
- -r 在排序时反序列出文件。
- -S 按文件大小排序。
- -s 打印每个文件的块大小。
- -Tcols 将每个 cols 的制表符设为 cols，而不是 8 个字符。
- -t 按修改时间排序；与 -1 配合使用显示修改时间。
- -U 按目录顺序列出条目，不进行任何排序。
- -u 按最后访问时间排序；与 -1 配合时显示该时间。
- -wcols 假设宽度为 cols（代表字符数），而不是当前值。
- -x 按扩展名字母顺序排序。
- -X 按行而非列列出条目。
- -1 每行列出一个文件。

| file 显示文件类型 | file 选项(s) 文件名 |
| :--- | :--- |

### 目的
file 命令返回给定文件的文件类型。有时，必须咨询 magic 文件 (/etc/magic)。不要完全依赖返回的信息——此命令返回的信息并不总是准确的，它在检测文本型或面向文本的文件类型（如 ASCII 文件、shell 脚本、PostScript 文件和命令）时效果最好。

### 选项

- -c 自动检查 magic 文件。
- -f list 对 *list* 中的文件运行 file 命令。
- -L 跟踪符号链接。
- -m file 检查 *file* 以获取文件类型，而不是使用 magic 文件。
- -z 检查压缩文件。

### 目的
find 命令用于查找文件。它可以非常简单，也可以随你的需要变得复杂。你可以输入任意数量的条件——与文件名相关的通配符、文件创建或最后访问的时间、存在什么链接等。它会遍历目录树，从根目录或你指定的另一个目录开始。

你可以使用 find 命令来判断某是否真的懂 Linux。如果他们使用 find 命令并将 -print 始终放在命令行的末尾，这意味着他们懂的是 UNIX 而不是 Linux。在标准的 UNIX 中，find 命令需要在行末使用 -print，告诉命令将输出打印到屏幕。然而，Linux 版本的 find 不需要 -print，而是假设你总是想输出到屏幕。因此，任何将 -print 作为示例命令行一部分的书籍或杂志文章都说明作者并不真正懂 Linux。

### 选项

- -amin min 将 *min* 替换为以下任意内容以查找访问过的文件：
- -m 在 *m* 分钟前。
- -m 正好在 *m* 分钟前。
- -m 少于 *m* 分钟前。

### 第二部分：命令

- -anewer file 查找在修改之后访问的文件。

- -atime days 查找访问过的文件：
- -d 在 d 天前。
- -d 正好在 d 天前。
- -d 少于 d 天前。

- -cmin min 查找更改的文件：
- -m 在 m 分钟前。
- -d 正好在 m 分钟前。
- -d 少于 m 分钟前。

- -cnewer file 查找在修改之后更改的文件。

- -ctime days 查找更改的文件：
- -d 在 d 天前。
- -d 正好在 d 天前。
- -d 少于 d 天前。

- -daystart 假设时间从今天开始计算，而不是从现在开始。

- -empty 即使文件为空也继续搜索。

- -exec command {} 在找到文件后运行 Linux 命令。

- -false 如果匹配成功，则返回假值。

- -follow 跟踪符号链接及关联目录。

- -fstype type 查找存储在特定系统类型的文件：ufs, 4.2, 4.3, nfs, tmp, mfs, S51K 和 S52K。

- -gid num 查找属于特定组 num 的文件。

- -group group 查找属于特定组的文件，组可以是 ID 或名称。

- -iname file 搜索指向文件的符号链接，可以包含元字符和通配符。不区分大小写。

- -iname file 查找命名的文件。不区分大小写。

- -inum num 查找 inode 节点为 num 的文件。

- -ipath name 查找匹配 name 的文件，name 是绝对路径名。不区分大小写。

- -links num 查找有 num 个链接的文件。

- -lname file 搜索指向文件的符号链接，可以包含元字符和通配符。必须匹配大小。

- -maxdepth num 在进入 num num 层目录后停止搜索。

- -mindepth num 从 num 层目录及更深处开始搜索。

- -mmin min 查找修改的文件：
- -m 在 m 分钟前。
- -exactly 正好在 m 分钟前。
- -m 少于 m 分钟前。

- -mtime days 查找修改的文件：
- -d 在 d 天前。
- -d 正好在 d 天前。
- -d 少于 d 天前。

- -name file 查找名为 file 的文件。必须匹配大小。

- -newer file 查找比 file 更晚修改的文件。

- -nogroup 查找组所有者不在 /etc/group 列表的文件。

- -nouser 查找所有者不在 /etc/passwd 列表的文件。

- -ok command {} \; 在找到文件后运行 Linux 命令，并验证你确实想运行该命令。

- -path name 查找匹配 name 的文件，name 是绝对路径名。区分大小写。

- -perm nnn 查找权限匹配指定权限（如 rwx）的文件。

- -size num[c] 查找包含 num 个块的文件，如果加上 c 则代表 num 个字符。

- -type t 返回类型为 t 的文件名，可以是 b（块设备文件）, c（字符设备文件）, d（目录）, f（普通文件）, l（符号链接）, p（管道），或 s（套接字）。

- -user user 查找属于指定用户的文件。

### 示例
以下查找整个文件系统中所有在两天内更改过的文件：

```
$ find / -ctime -2
```

这列出了你家目录下的所有文件和目录：

```
$ find $HOME
```

| fromdos 从 DOS 转换 | fromdos < dosfile.txt > unixfile.txt |
| :--- | :--- |

### 目的
fromdos 命令将 DOS 文本文件转换为 UNIX 文件，将 DOS 文本文件末尾的回车/换行 (CR LF) 序列替换为 UNIX 换行 (LF)。

| funzip 从 Zip 文件提取内容 | funzip password input_file |
| :--- | :--- |

### 目的
funzip 命令是一个用于从管道中的 Zip 存档提取内容的过滤器。

### 相关命令

gzip

unzip
zip

| getfilename 以新格式重命名文件 | getfilename format-name filename |
| :--- | :--- |

### 目的
getfilename 命令要求用户以给定格式命名文件。它本身没用，但与 mailcap 类的命令（如 mailto）结合使用时变得有用。

### 相关命令

+ mailto
metamail

| gunzip 解压缩存档 (GNU 命令) | gunzip option(s) file(s) |
| :--- | :--- |

### 目的
gunzip 命令用于解压缩 gzip 命令或 UNIX compress 和 pack 命令压缩的文件。

### 选项

- -c 使用标准输出而不更改原始文件。
- -N 保留原始名称时间戳。
- -q 静默模式，不返回状态信息。
- -t 测试新文件的完整性。
- -v 详细模式，向屏幕显示所有更改，包括新文件名。

### 第二部分：命令

相关命令
compress
gzip
pack

| gzexe 压缩执行文件 (GNU Command) | gzexe option file(s) |
| :--- | :--- |

### 目的
gzexe 命令压缩执行文件。当你运行压缩的可执行文件时，它会自动解压并运行。运行压缩命令需要一点时间，但你可以节省宝贵的磁盘空间。

### 选项

-d 解压缩压缩的可执行命令。

| gzip 压缩文件 (GNU Command) | gzip option(s) file(s) |
| :--- | :--- |

### 目的
gzip 命令使用 Lempel-Ziv 压缩文件。压缩后的文件重命名为 file.gz 并删除原始文件。原始文件的访问权限和时间戳由新的压缩文件维护。

### 选项

- -c 使用标准输出而不更改原始文件。

- -d 解压缩文件（与 gunzip 相同）。



- -f 在已存在压缩文件、具有多个链接或已经压缩的情况下强制压缩。
- -l 对已经通过 deflate、compress、gzip、lzh 或 pack 压缩过的文件创建压缩文件。
- -N 保留原始名称和时间戳。
- -q 在静默模式下工作，不返回状态信息。
- -r 在递归模式下工作，对子目录也进行压缩。
- -S 后缀 在新文件名后添加指定的后缀，而不是默认的 .gz。
- -t 测试新文件的数据完整性。
- -v 在冗余模式下工作，在屏幕上显示所有更改，包括新文件的名称。

### 相关命令

gunzip

| hattrib 修改文件属性 | hatattrib (选项) hfs_path |
| :--- | :--- |

### 目的

hatattrib 命令修改 HFS (Macintosh) 文件属性。

### 选项

+ -c 设置创建者属性。
+ -t 设置类型属性。
+ +i 设置不可见标记。
+ -i 清除不可见标记。
+ +1 设置锁定标记。
+ -l 清除锁定标记。

### 相关命令

hcopy
hls

### hcd 修改工作目录
hcd hfs_path

### 目的

hcd 命令更改当前 HFS 卷的“当前工作目录”。所有后续的 HFS 命令都将相对于此目录解释文件名。

### 选项

hfs_path 设置新工作目录的路径。

### 相关命令

hls
hpwd

### hcopy 复制文件
hcopy mode source_path
target_path

### 目的

hcopy 命令在 HFS 卷和 Linux 文件系统之间传输文件。如果复制了多个文件，目标路径必须是一个目录。

### 模式

+ -m MacBinary II，建议用于复制二进制文件。
- -b BinHex，建议用于 ASCIIZ 文件；保留 Macintosh 文件的两个分叉（forks）。
- -t Text，仅复制 Macintosh 文件的数据叉并进行行尾翻译。
- -r Raw data，不进行任何翻译并仅复制数据叉。
Automatic，由 hcopy 决定哪种模式最有效。

### 相关命令

hatattrib
hls

| hdel 删除文件 | hdel hfs_path |
| :--- | :--- |

### 目的

hdel 命令删除 Macintosh 数据文件的两个分叉。

### 相关命令

rmdir

| hdir 显示目录 | hdir hfs_path |
| :--- | :--- |

### 目的

hdir 命令以长格式格式显示 HFS 目录的内容。它等同于 hls -1。

### 相关命令

hls

| hformat 创建 HFS 文件系统 | hformat (选项) 目标分区 |
| :--- | :--- |

### 目的

hformat 命令为卷创建一个新的 HFS 文件系统。关键在于必须指定指向该卷目的地的 Linux 路径（无论是作为块设备还是普通文件），并且该路径必须已经存在。

### 选项

- -f 将整个分区格式化为单个文件系统，擦除所有现有数据。
- -l label 为新的 HFS 文件系统指定标签。

```
hfs
运行 HFS Shell
hfs hfs_path partition
```

### 目的

hfs 命令启动一个基于 Tcl 的 shell，，用于操作 HFS 卷。在 hfc 中，你可以运行各种命令来挂载卷、更改目录以及进行其他操作。

### 命令

+ - mount path 将路径挂载为 HFS 卷。
- umount path 卸载之前挂载的路径。
- vol path 将之前挂载的路径设为当前。
- info 返回关于当前挂载卷的信息。
- pwd 打印 HFS 目录的完整路径。
- cd directory 将当前工作目录更改为路径。
- dir directory 返回指定目录的内容。
- mkdir directory 在目录处创建一个新的空目录。
- rmdir directory 删除指定的目录。
- create path 在路径处创建一个新文件。
- del file 删除指定文件的两个分叉。
- stat path 返回关于指定 HFS 路径的状态信息。
- cat file 显示指定 HFS 文件的数据叉。
- copyin unixfile 将 UNIX 文件复制到 HFS 卷。
- copyout hfsfile 将 HFS 文件复制到 UNIX 卷。
- format path 格式化指定的 UNIX 路径。

### 相关命令

xhfs

| hls 列出内容 | hls (选项) hfs_path |
| :--- | :--- |

### 目的

hls 命令列出 HFS 卷中的文件和目录。

### 选项

+ - -1 每行列出一个文件。
- -a 列出目录中的所有文件，包括隐藏文件。
- -b 显示非图形字符，使用类似于 C 语言中使用的字母和八进制反斜杠序列。
- -c 根据状态更改时间对内容进行排序。
- -d 列出目录名而不包含其内容。
- -f 按磁盘原始顺序显示内容，不进行任何排序。
- -i 显示每个文件的目录 ID。
- -l 以长格式列出文件，包括文件类型、权限、硬链接数、所有者名称、组名、字节大小和时间戳（修改时间，除非选择了其他时间）。
- -m 水平列出文件，并用逗号分隔。
- -q 在文件名的非图形字符处用问号代替。
- -r 反序排序文件名。
- -s 在文件名左侧打印文件大小（以 1K 块为单位）。
- -t 按时间戳排序文件（最新优先），而不是按字母顺序。
- -x 按列打印列表，并进行水平排序。
- -w cols 设置屏幕宽度为 cols 个字符。默认值为 80。
- -C 按列列出文件并进行垂直排序。
- -F 按字符列出文件类型：/ 表示目录，@ 表示符号链接，| 表示 FIFO，= 表示套接，* 表示 Macintosh 可执行文件，普通文件留空。
- -N 原样列出文件，不进行任何转义或问号替换。
- -Q 用双引号（""包裹文件名，并按照 C 语言中的的方式显示非图形字符。
- -R 递归列出目录内容。
- -S 按文件大小排序，而不是按字母顺序，大文件在前。
- -U 按磁盘原始顺序显示内容，不进行任何排序。

### 相关命令

| hmount 挂载 HFS 卷 | hmount path partition |
| :--- | :--- |

### 目的

hmount 命令挂载一个新的 HFS 卷并将其设当前。

### 相关命令

| hpwd 打印工作目录 | hpwd |
| :--- | :--- |

### 目的

hpwd 命令显示当前工作目录的完整路径名。

### 相关命令

hcd

| hrename 重命名 HFS 文件 | hrename source_path target_path |
| :--- | :--- |

### 目的

hrename 命令更改指定文件或目录的名称和或位置。

| hrmdir 删除 HFS 目录 | hrmdir directory |
| :--- | :--- |

### 目的

hrmdir 命令从当前卷中删除空的 HFS 目录。

| humount 卸载 HFS 卷 | humount volume |
| :--- | :--- |

### 目的

humount 命令卸载当前的 HFS 卷。

### 相关命令

hmount

# 218 第二部分：命令

```
hvol
显示当前卷
hvol path
```

### 目的
hvol 命令显示当前 HFS 卷的名称和路径。

### 相关命令
mount
humount

```
In
链接文件
In (选项) originalfile
linkfile
In (选项) file(s)
directory
```

在 ln 命令链接两个或多个文件。结果是文件只有一份，但可以通过多个目录访问。其目的是减少文件占用的磁盘空间。虽然你在单用户 Linux 系统上可能不需要链接文件，但如果你在管理网络安装则可能需要。Linux 本身在安装中使用链接；某些 Linux 文件存储在标准位置，但链接使得标准位置有效。

两种类型的链接是硬链接和符号链接。大多数情况下你会倾向于符号链接，因为它们更容易用 ln 命令跟踪。

> **提示** 你可以为两个文件相同的名称，也可以为链接文件一个新名称。始终记住第一个名称是原始文件，第二个是链接文件；如果你反了顺序，就会破坏原始文件。

# 第6 章 文件管理命令 219

### 选项

+ -b 在删除原始文件前对其进行备份。
+ -d 创建目录的硬链接（仅特权用户可用）。
+ -f 强制链接，不询问覆盖现有文件的权限。
+ -F 创建目录的硬链接（仅特权用户可用）。
+ -i 在覆盖现有文件前确认。
+ -n 在引用符号链接之前引用它们。
+ -s 创建符号链接。
+ -S 后缀 在备份文件的末尾添加后缀，而不是标准的波浪号 (~)。

### 示例

将 kevin 文件链接到 pat 文件：
$ ln pat kevin

### 相关命令

+ chmod
chown
cp
ls
mv

| locate | locate (选项) |
| :--- | :--- |
| 查找模式 | pattern(s) |

### 目的

locate 命令在文件名数据库中查找匹配的模式。模式可以包含 shell 风格的元配符 (*, ?, 和 []），但 / 和 . 被视为文件名的一部分。如果没有元配符，则从数据库返回包含该字符串的所有文件名。（该字符串不需要匹配整个文件名）。如果包含了元配符，locate 命令显示包含



精确模式，因此请在带有元字符的模式的开头或结尾使用 `*`。

### 选项

- -d path 在 path 中搜索文件名数据库，path 是一个由冒号分隔的数据库文件名列表。
- --help 打印选项列表并退出。
- --version 返回 locate 命令的版本。

### 相关命令

- find
- locateddb
- lockfile
- updatedb
- xargs

### 目的

`locate` 命令在文件名数据库中查找模式，并返回匹配的文件名。模式可以包含 shell 风格的元字符（`*`、`?` 和 `[`），但 `/` 和 `.` 被视为文件名的一部分。如果没有元字符，则从数据库中返回所有包含该字符串的文件名。（该字符串不需要匹配整个文件名）。如果包含了元字符，`locate` 命令将显示包含精确模式的文件名，因此请在带有元字符的模式的开头或结尾使用 `*`。

### 相关命令

- find
- locate
- lockfile
- updatedb
- xargs

### lockfile
锁文件

# lockfile 选项 filename

### 目的

`lockfile` 命令创建一个或多个信号文件，用于限制对文件的访问。如果 `lockfile` 无法按顺序创建信号文件，它将等待八秒并重试；你可以使用 -r 选项指定重试次数。生成的文件访问权限为 0，需要用 `rm -f` 删除。

### 选项

- -r num 在放弃之前的重试次数。

### 相关命令

rm

### ls
列出文件
(GNU 命令)

### ls 选项(s) 名称(s)

### 目的

`ls` 命令列出指定目录的内容或指定文件的扩展信息。如果未给出名称，则假设你想查看当前目录的内容。默认情况下，文件按列列出并垂直排序。虽然这是一个复杂的命令，特别是在选项众多的 GNU 版本中（有 38 个选项），但你很可能会经常使用 `-F` 和 `-l` 选项，而最少使用 `-u` 和 `-c` 选项。

### 选项

- -1 每行列出一个文件。
- -A 列出目录的所有内容，排除当前目录（`.`）和父目录（`..`）。但会显示所有其他隐藏文件。
- -b 使用字母和八进制转义序列显示非图形字符，这些序列与 C 语言中使用的相同。
- -B 忽略备份文件（以 `~` 结尾的文件）。
- -c 根据状态更改时间排序内容。
- -C 按列列出文件并垂直排序。
- -d 列出所有文件和目录，但不列出目录的内容。
- -e 完整显示所有时间。
- -f 按磁盘顺序显示内容，不进行任何排序。
- -F 通过字符列出文件类型：`/` 表示目录，`@` 表示符号链接，`|` 表示管道（FIFO），`=` 表示套接字，普通文件为空。
- -G 在长格式列出文件时忽略组所有权。
- -i 显示每个文件的 inode 号。
- -I pattern 忽略匹配模式的文件。
- -k 以千字节为单位列出文件大小。
- -l 以长格式列出文件，包括文件类型、权限、硬链接数、所有者名称、组名、字节大小和时间戳（修改时间，除非选择了其他时间）。
- -L 通过符号链接显示文件，而不是列出链接的内容。
- -m 水平列出文件，用逗号分隔。
- -n 列出数字 UID 和 GID 而不是文件名。
- -o 切换文件的彩色显示。
- -p 在每个文件名后附加一个字符以指示类型。
- -q 用问号代替文件名中的非图形字符。
- -Q 用双引号（""）包围文件名，并按 C 语言中的方式显示非图形字符。
- -r 反序排序文件名。
- -R 递归列出目录内容。
- -S 在文件名左侧打印文件大小（以 1K 块为单位）。
- -S 按文件大小而非按字母顺序排序，最大的文件在前。
- -t 按时间戳排序文件（最新优先），而不是按字母顺序。
- -Tcols 将制表位设置为 `cols*cols` 列。默认值为 8。设置为 0 则禁用制表符。
- -u 按最后访问时间排序文件，而不是修改时间。
- -U 按磁盘顺序显示内容，不进行任何排序。
- -w cols 设置屏幕宽度为 `cols` 个字符。默认值为 80。
- -x 按水平排序分列列出列表。
- -X 按文件扩展名字母顺序排序文件。

### 相关命令

dircolors

# mc 启动 Midnight Commander (GNU 命令)
# mc 选项(s) 目录1 目录2

### 目的

`mc` 命令启动 Midnight Commander，这是一个用于 Linux 的目录浏览器和文件管理器，不需要 X 窗口系统。它允许你通过鼠标操作和下拉菜单，或者在命令行中输入命令（如使用 `vi` 命令）来移动、复制和删除文件及目录。

### 交叉引用

Midnight Commander 与一组大量的命令相关；请查看在线 man 页面。

### 选项

- -b 黑白模式工作。
- -c 彩色模式工作。
- -C 使用 arg 代替默认。
- -d 关闭鼠标支持。
- -f 显示搜索路径。
- -l 设置卷 ID。
- -P 在 Midnight Commander 退出后打印工作目录。
- -s 以慢速模式工作。
- -t 使用 termcap。
- -u 禁用并发 shell。
- -U 启用 shell。
- -v 启动内部查看器。
- -x 在 term 下工作。

| merge | merge 选项(s) file1 |
| 合并三个文件 | file2 |

### 目的

`merge` 命令合并三个文件，将 file2 的所有更改合并到 file3。如果存在冲突会提示。

### 相关命令

- diff
- diff3

### mkdir
创建目录
(GNU 命令)

# mkdir 选项(s) 

### 目的

`mkdir` 命令用于创建目录。它也可以创建目录层级。新目录的默认模式为 0777。

### 选项

- -m 将新目录模式设置为 mode。
- -p 如果需要创建父目录。

# mkdirhier
创建目录层级

mkdirhier directory

### 目的

`mkdirhier` 命令创建目录层级。该命令已被 GNU 版本的 mkdir 命令取代，后者可以创建层级。

### 相关命令

mkdir

# mkdosfs
创建 DOS FAT 文件系统

mkdosfs 选项(s)

### 目的

`mkdosfs` 命令在 Linux 设备（通常是磁盘分区）上创建 MS-DOS FAT 文件系统。

### 选项

- -c 检查分区坏块。
- -f fats 指定文件系统中文件分配表（fats）的数量。默认且限制为 2。
- -F fatsize 指定使用的文件分配表（fats）类型：12 位、16 位或 32 位。创建 FAT32 文件系统时使用的选项。
- -i volume 设置新文件系统的卷 ID。
- -l filename 从文件名读取坏块列表。
- -m message_file 设置在未正确安装操作系统的情况下启动文件系统时用户收到的消息。
- -n volume 设置文件系统的卷名。
- -r dir_entries 设置根目录可用条目的数。
- -s sectors 设置每个簇扇区数。

### 相关命令

mkfs

| mkfifo | mkfifo 选项(s) |
| 创建 FIFO (GNU 命令) | filename |

### 目的

`mkfifo` 命令创建一个 FIFO（或命名管道）。新 FIFO 的模式为 0666。

### 选项

- -m mode 将新 FIFO 的模式设置为 mode。



## mkfontdir 创建字体目录 (X Window 系统命令)

mkfontdir 目录

### 目的

mkfontdir 命令在指定的目录下创建 X 字体文件的索引，名为 fonts.dir。你没有选项更改此文件名，你也不应该这样做——这是 X 字体服务器和 X 服务器查找字体信息时的使用的。

### 相关命令

- - xfs
- xset

## mkfs 构建文件系统

mkfs 选项(s) 文件系统 块

### 目的

mkfs 命令在指定的设备（通常是硬盘分区）上构建 Linux 文件系统。文件系统可以是设备名或挂载点，而 blocks 指的是用于文件系统的块数。

> 注意
> 该命令实际上是构建文件系统所需的所需的许多命令的前端程序。

### 选项

- -l filename 从文件名中读取坏块列表。
- -v 详细输出。
- -c 在构建文件系统之前检查坏块。
- -t ftype 指定要构建的文件系统类型。
- -v 提供关于生成文件系统所需的每个步骤的信息。

## mkmanifest 恢复 Linux 文件名 mkmanifest 文件(s)

### 目的

mkmanifest 命令创建一个 shell 脚本，用于恢复被 MS-DOS 文件名限制截断的 Linux 文件名。

### 相关命令

mtools

### mknod 创建特殊文件 (GNU 命令)

mknod 选项(s)文件名 文件类型 主设备号 次设备号

### 目的

mknod 命令使用给定的文件名创建特殊文件（FIFO、字符特殊文件或块特殊文件）。这些文件的默认模式为 0666。文件类型可以是以下之一：

- - p FIFO。
- - b 块（缓冲）特殊文件。
- - c 字符（缓冲）特殊文件。
- - u 字符（不缓冲）特殊文件。

> 注意 Major_dev 和 minor_dev 指的是主设备号和次设备号。

### 选项

- -m mode 将新文件的模式设置为 mode。这是一个符号值。

### mv 移动文件

mv 选项(s) 源 目标

### 目的

mv 命令移动文件——更准确地说，是它们在文件层次结构中被它们一个新名称和一个新位置。如果目标是一个目录，mv 将源移动到该目录下的同名文件中。否则，如果给出两个文件作为源和目标，它会将第一个文件移动到第二个文件上。如果新文件不可写，mv 将询问你是否确认要覆盖一个文件。

### 选项

- -b 在删除文件之前创建备份。
- -f 在不提示的情况下删除现有目标文件。
- -i 在覆盖目标文件之前提示你。
- -S 为备份设置后缀；系统默认值为 ~。其他命令假设后缀为 ~，所以除非你有充分理由，否则不要更改它。
- -u 拒绝将文件移动到具有相同或更晚修改时间的新目标。
- -v 详细模式；在移动每个文件之前打印其名称。

### 相关命令

cp

## newgrp 更改组权限

group 组名

### 目的

newgrp 命令在你已经登录系统后更改你的组权限。如果你没有指定新的组名，将使用你的登录组名。

### 相关命令

login

| 命令 | 选项 |
| :--- | :--- |
| od 打印八进制文件偏移量 (GNU 命令) | od 选项(s) 文件 \|n |

### 目的

od 命令以八进制格式打印文件偏移量，并以 2 字节八进制数打印文件数据。提供了许多可用选项。

### 交叉引用

> 要查看其他可用选项，请查看在线手册页以获取更多信息。

| 命令 | 选项 |
| :--- | :--- |
| pwd 打印工作目录 (GNU 命令) | pwd \|n |

### 目的

pwd 命令打印当前（工作）目录的名称。

# 警告

> 不要将此命令与 passwd 命令（在第 5 章介绍）混淆，后者更改密码。

## 第 6 章：文件管理命令 231

| 命令 | 选项 |
| :--- | :--- |
| rm 删除文件 (GNU 命令) | rm 选项(s) 文件名 |

### 目的
rm 命令从 Linux 文件系统中删除文件。在文件实际被删除之前，你会收到提示（如果运行 rm 时带有 -i 选项）。

### 选项

- -d 使用 unlink 命令而不是 rdir 命令删除链接的目录。（只有 root 用户可以访问 -d 选项。）
- -f 忽略不存在的文件。
- -i 显式设置在删除文件之前进行提示。
- -r 递归删除目录的内容。
- -v 在详细模式下工作，在删除每个文件之前打印其名称。

| 命令 | 选项 |
| :--- | :--- |
| rmdir 删除空目录 (GNU 命令) | rmdir 选项(s) 目录 |

### 目的
rmdir 命令删除空目录。包含内容的目录将不会删除。

### 选项

- -p 如果父目录作为命令行的一部分被提到，则删除父目录。

### size 列出大小 (GNU 命令)

### 目的
size 命令列出命令行上列出的*目标文件(s)* 的段大小和总大小。每个文件生成一行输出。

### 选项

- -A 输出类似于 System V 的 size 输出。
- -B 输出类似于 Berkeley 的 size 格式。
- -d 大小以十进制列出。
- -o 大小以八进制列出。
- -x 大小以十六进制列出。
- --target 指定目标代码格式为 *bfdname*。bfdname

## sq 压缩排序单词列表

### 目的

sq 命令压缩一个排序的单词列表。它通常用于大型文本文件，例如字典。压缩是通过消除公共前缀并将其替换为单个字符实现的，该字符编码了与前一个单词共享字符的数量。

### 相关命令

unsq

# 第 6 章：文件管理命令

| 命令 | 选项 |
| :--- | :--- |
| sum 执行文件校验和 (GNU 命令) | sum 选项(s) 文件名(s) |

### 目的
sum 命令对文件进行校验和并计算块数。它为每个命名的文件计算一个 16 位的校验和。它打印每个文件的校验和以及文件中的块数。GNU 版本的 sum 使用与 BSD sum 命令兼容的算法计算校验和，并以 1K 块为单位打印文件大小。

### 选项

- -r 使用 BSD 兼容的算法，这是默认值。
- -s 使用 System V 兼容的算法并打印文件大小。

| 命令 | 选项 |
| :--- | :--- |
| test 检查类型 (GNU 命令) | test 表达式 |

### 目的
test 命令根据表达式的结果返回 0（真）或 1（假）。

### 交叉引用

> 有关表达式的更多信息，请查看在线手册。

## unsq 解压缩排序单词列表

### 目的

unsq 命令解压缩一个由 sq 命令压缩的排序单词列表。

### unzip 解压文件

### 目的

unzip 命令解压使用 PKZip 或 WinZip 格式的 MS-DOS/Windows 文件。

> 交叉引用
> 如需更多可用选项请查看在线手册。

### 相关命令

unzfx

## unzfx 创建自解压 Zip

### 目的
unzfx 命令通过在现有 Zip 存档前附加创建一个新的自解压存档。

### 交叉引用

> 如需更多可用选项请查看在线手册。

### 相关命令

updatedb

### 目的

updatedb 命令更新 locate 命令使用的文件名数据库。该数据库包含了上次更新时特定目录树中的文件。

### 选项

- --localpaths=path1 path2 指定放入数据库的本地目录。
- --netpaths=path1 path2 指定放入数据库的网络目录。
- --netuser=user 指定搜索网络目录的用户。
- --old-format 使用旧格式而不是新格式创建数据库。
- --output=dbfile 指定要构建的数据库文件。
- --prunepaths=path1 path2 指定不放入数据库的目录。

### 相关命令

locate

### 第二部分：命令

## xfilemanager 启动 X 界面管理器 (X Window 系统命令)

xfilemanager 选项(s)

### 目的

xfilemanager 命令启动一个具有拖放能力的 X 界面管理器。它可以执行所有常规的文件管理器任务，如移动和复制文件、启动应用程序以及管理目录。

### 选项

- -doubleClickTime 设置鼠标点击之间被视为双击的间隔时间；默认为 300 毫秒。
- -iconDir path 设置文件图标目录。
- -iconFont fontname 设置图标使用的字体。
- -multiWindow 在单独窗口中显示目录。
- -noDragCopyAsk 在拖放复制文件时不进行确认。
- -noDragDeleteAsk 在拖放删除文件时不进行确认。
- -noDragExecAsk 在拖放执行文件时不进行确认。
- -noDragMoveAsk 在拖放移动文件时不进行确认。
- -rootDir path 设置打开时的根目录。默认值是用户的主目录。
- -saveWS 在退出前保存工作区设置。
- -selectColor colname 设置标记所选文件的颜色。



## 第6 章：文件管理命令 237

- singleWindow 在一个大窗口中显示所有内容。
- trashcan directory 开启垃圾桶选项；删除的文件将发送到垃圾桶目录，而不是从系统中删除。

### 相关命令

mc
xfm

### 目的

xfm 命令启动一个具有拖放能力的基于 X 窗口的文件管理器。它可以用于执行所有常见的文件管理器任务，如移动和复制文件、启动应用程序以及管理目录。它实际上包含两个共同工作的不同组件：应用程序管理器和文件管理器。

> 注意
> 在新系统上运行此此命令之前，请使用 xfm.install 脚本创建新的配置文件。

### 选项

- -appmgr 仅启动应用程序管理器。
- -filemgr 仅启动文件管理器。

### 相关命令

mc
xmanager

```
xhfs left_path
打开 HFS 文件 right_path
管理器
(X 窗口系统命令)
```

### 目的

xhfs 命令打开一个用于复制和浏览文件的图形化应用程序。显示器分为两侧：一边是 HFS 卷，另一边是 Linux 文件系统。你可以通过双击文本文件来查看它们，也可以通过选择文件并点击复制按钮来复制文件。在按下复制按钮后，你可以从以下模式中选择：

+ -m MacBinary II，推荐用于复制二进制文件。
- -b BinHex，推荐用于 ASCII 文件；保留 Macintosh 文件的两个分支。
- -t Text，仅复制 Macintosh 文件的数据分支并进行行尾翻译。
- -r Raw 原始数据，不进行任何翻译并仅复制数据分支。
- -s Automatic，由 hcopy 决定哪种模式最有效。

### 相关命令

hcopy
hfs

```
zcat file
解压缩
Gzip 文件
```

### 目的

zcat 命令解压缩 gzip 压缩的文件并将其写入标准输出（通常是屏幕，工作方式与 cat 命令相同）。

### 相关命令

cat
gzip

| zforce 强制使用新文件名 | zforce filename(s) |
| :--- | :--- |

### 目的

zforce 命令强制使用 gzip 命令压缩的文件具有 .gz 扩展名。

### 相关命令

gzip

| znew 重新压缩的文件 (GNU 命令) | znew option(s) filename.Z filename.gz |
| :--- | :--- |

### 目的

znew 命令获取现有的压缩 .Z 文件并将其重新压缩为 gzip (.gz) 格式。随后旧的 .Z 文件将被删除。

### 选项

+ -9 最佳压缩方法；也是最慢的。
- -f filename.gz 压缩新的 filename.gz，即使 filename.gz 存在。
- -K 检查新的 filename.gz 文件是否比旧 filename.Z 文件小；如果不是，则不进行重新压缩。
- -P 管道到转换程序，节省磁盘空间。
- -t 在删除旧 filename.Z 文件之前测试新的 filename.gz。
- -v 详细模式。

### 相关命令

gzip

| zoo 操作压缩归包 | zoo option(s) archivefile |
| :--- | :--- |

### 目的

zoo 命令使用 Lempel-Ziv 压缩算法创建文件存档。它可以处理同一文件的多个版本并存储每个版本。要查看 zoo 选项的摘要，请输入 zoo -h。

> 交叉引用
> 更多信息请参见详细的在线 zoo 手册页。

## #文本处理命令

这些命令旨在直接与文本文件交互。在 Linux 中，这可以意味着许多事情：终端用户可以使用这些命令编辑或创建信函和备录，程序员可以使用这些命令编辑源代码，而系统管理员可以使用这些命令创建和编辑配置文件。

| bpe bpe | bpe filename |
| :--- | :--- |
| 编辑二进制文件 | |

### 目的

bpe 命令用于修改或编辑二进制文件，可以是十六进制或 ASCII 格式。在显示二进制文件时，有几个命令可用；要进入编辑模式，选择 e 进行 ASCII 编辑，或选择 E 进行十六进制编辑。

### 命令

+ - D 从当前文件位置转储一页。
- 编辑文件的 ASCII 部分。
- 编辑文件的十六进制部分。
- 在当前文件位置之后查找文件中字符串。
- 在当前文件位置之后定位文件十六进制字节。
- 显示下一个扇区。
- 显示上一个扇区。
- 退出程序。
- 将修改后的扇区写入磁盘。
-向前滚动两行。
- 向后滚动两行。
- 在当前文件位置之后查找文件中字符串。
- 显示帮助信息。

### 相关命令

+ - hd
- - od

| cat | cat option(s) files |
| :--- | :--- |
| 读取并打印文件 | |

### 目的

cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux 操作系统中最常用的命令。cat 命令是 Linux



## column 将输入格式化列

目的

`column` 命令将输入格式化为列，无论是来自文件还是来自标准输入。

选项

- -c num 将列数设置为 `num`。
- -s char 将 `char` 设置为列分隔符。必须与 `-t` 配合使用。
- -t 将输入格式化为表格而不是列。默认使用空格格式化，除非通过 `-s` 设置了替代方案。
- -x 在填充行之前填充字符。

## comm 比较两个文件的内容

目的

`comm` 命令比较两个已经用 `sort` 命令排序过的文件的内容。输出结果被分为三列：

file1 中的行 | file2 中的行 | 两个文件中共有的行

> 注意此命令与 `diff` 和 `uniq` 命令相似，不同之处 `comm` 可以与两个排序后的文件一起用于寻找重复或唯一的行。

选项

- -1 不打印第一列。
- -2 不打印第二列。
- -3 不打印第三列。
- -12 不打印第一列和第二列。
- -13 不打印第一列和第三列。
- -23 不打印第二列和第三列。

### 相关命令

```
cmp
diff
sdiff
sort
uniq
```

### 目的

`csplit` 命令将一个长文件分割为两个或多个小文件。你可以告诉 `csplit` 根据大小或内容分割文件，并使用特定的表达式作为分割标记。原始文件将保持不变。

新文件将以 xx 开头。第一个文件是 `xx00`（记住，Linux 喜欢用 0 开头），下一个文件是 `xx01`，以此此类推。限制是 100 个文件，因此数值最大的文件名是 `xx99`。

### 选项

- -f txt 使用 `txt` 代替 xx 作为新文件名的开头。
- -k 即使命令失败也保留文件。
- -n num 在文件名中使用长度为 `num` 的数字，而不是默认的两个。
- -q 抑制字符计数。
- -s 抑制字符计数。
- -z 不创建空文件，但保持编号。

### 第二部分：命令

## 参数

- /expr/ 创建从当前行开始到包含 `expr` 的行的文件。你可以添加一个后缀，在 `expr` 之前或之后 *num* 行结束文件 —— 使用 `+num` 或 `-num`。
- %expr% 忽略从当前行到第一个包含 `expr` 的行的部分。
- line 在当前行创建一个文件，并在 `line` 之前的一行结束。
- {n} 重复 `n` 行参数。默认是重复一次参数。

### 示例

这将一个名为 `bonfire` 的文件分成 20 章节，每章都以 *Chapter* 开头。

```
$ csplit -k bonfire '/Chapter/' {20}
```

| cut 切割文件列或字段 | cut 选项(s) 文件 |
| :--- | :--- |

### 目的

`cut` 命令从文件或一组文件中剪取列或字段并显示它们。你可以使用这些信息查看文件的部分，或者获取这些信息并发送到另一个新文件中。

### 选项

- -c list 剪取 *list* 中指定的列。
- -d character 指定确定列或字段的分隔符；默认是制表符。如果使用非字母数字字符（如空格），则必须用单引号括起来。此时此选项必须与 `-f` 选项配合使用。
- -f list 剪取 *list* 中指定的字段。
- -s 抑制没有分隔符的行；与 `-f` 选项使用。

### 示例

这从 `payroll` 文件中提取第一和第四字段并显示在屏幕上：

```
$ cut -f1,4 payroll
```

这从 `payroll` 文件中提取第一和第四列并将其放入名为 `payroll.old` 的新文件中：

```
$ cut -c1,4 payroll > payroll.old
```

### 相关命令

- grep
- join
- paste

### 目的

`diff` 命令比较两个文件并返回不同的行。差异文件的行号用 `<` 和 `>` 符号标记。file1 的差异行用 `<` 标记，file2 的差异行用 `>` 标记。三个连字符 (---) 分隔文件的内容。

diff 命令也可以比较不同目录下的文件。在这种情况下，请使用目录。

> 提示此命令处理较小的文本文件效果最好。

### 选项

- -a 比较所有文件，包括二进制文件。
- -b 忽略空格的差异。
- -B 忽略文件内的空行。
- -c 为每个差异打印三行上下文。
- -d 尝试寻找更具体的差异，导致处理时间增加。
- -e 返回使用 ed 文本编辑器从 file1 重新创建 file2 的命令。
- -H 扫描分散的小变化；会遗漏许多其他变化。
- -i 比较文件时忽略大小写。
- -I expr 忽略匹配 `expr` 的文件行。
- -n 返回 RCS diff 格式的信息。
- -N 将不存在的文件视为空。
- -t 将输出中的制表符扩展为空格。
- -T 在行首插入制表符。
- -u 将文件的旧版本和新版本单行打印。
- -w 忽略制表符和空格（空白）。
- -y 返回两列信息。

## 目录

- -l 将输出分页 pr。
- -r 递归运行 diff 查看公共子目录中的文件。
- -s 返回相同的文件。
- -Sfile 比较目录时以 file 开头，忽略字母顺序排在 file 之前的的文件。
- -x expr 忽略匹配 `expr` 的文件；不能使用通配符。
- -X filename 忽略匹配 filename 的文件；可以使用通配符。

### 示例

```
$ diff letter.1212 letter 1213
1cl
< December 12, 1997
---
```

> December 13, 1997...

### 相关命令

```
cmp
diff3
sdiff3
```

### 目的

diff3 命令比较三个文件并返回它们之间的差异，类似于 diff，但不会自动返回差异。相反，会返回以下代码之一：

- - = = = 三个文件都不同。
- - = = -1 file1 不同。
- - = = -2 file2 不同。
- - = = -3 file3 不同。

### 选项

- -a 将所有文件视为文本；用于判断是否存在差异。
- -A 创建一个 ed 脚本，显示所有文件的 file1 和 file2 的差异。
- -e 创建一个 ed 脚本，将 file2 和 file3 的差异放入 file1。
- -E 创建一个 ed 脚本，显示合并后的差异。
- -m 在 ed 脚本末尾添加 w (save) 和 q (quit) 命令。
- -L 使用文件名 own文件名。
- -s 在输出中使用一个分隔符，而不是默认的两个空格。
- -T 在每行开头插入制表符。
- -x 创建一个 ed 脚本，显示 file1 中的所有差异。
- -X 创建一个 ed 脚本，显示 file1 中的所有差异。
- -3 创建一个 ed 脚本，将 file1 和 file3 的差异放入 file1。

### 相关命令

cmp
diff
sdiff

### 目的

egrep 命令在多个文件或文件中搜索文本（称为模式或表达式）。它是 grep 命令的亲戚，通常是三者中最强大且速度最快的。然而，它不支持所有的 ASCII 字符 只要用引号括起来，它可以搜索 +, |, (, )，但不会搜索以 \ 开头的模式。

选项

- -A num 显示匹配模式后的 num 行。
- -B num 显示匹配模式前的 num 行。
- -b 返回匹配行的块号。
- -c 在不列出实际匹配项的情况下返回匹配数。

# 第七章：文本处理命令 255

- -C 显示匹配模式前后的两行。
- -e pattern 当模式以连字符 (-) 开头时搜索模式。
- -f file 使用文件中的模式。
- -h 列出包含匹配的文件但不列文件名。
- -i 匹配时忽略大小写。
- -l 列出匹配的文件。
- -L 列出不包含匹配行的文件。
- -n 列出匹配行及其行号。
- -s 抑制无法读取或访问的文件错误信息。
- -v 列出不匹配模式的行。
- -w 只列出匹配的单词。
- -x 只列出匹配的行。

### 示例

这在当前目录（如 * 所示）搜索字符串 Cogwell Cogs 和 Spacely Sprockets：

```
$ egrep "Cogwell Cogs|Spacely Sprockets" *
```


在命令行中，你实际上是在调用 elvis 编辑器。它响应所有的标准 vi 命令。

### 选项

- -e 启动时进入冒号命令模式，类似于 UNIX 的 ex 命令。
- -m file 在文件中搜索编译器的错误信息。
- -r 调用 elvrec 命令来恢复文件。
- -R 以只读模式打开文件。
- -s 在安全模式下工作，这样新手就不会对文件或系统造成太大破坏。
- -t tag 以 tag 作为第一行打开文件。
- -v 启动时进入视觉命令模式，类似于 UNIX 的 vi 命令。

### 相关命令

- elvrec
emacs
joe
jove
vi

![](img/2cc16c5632743593217f446101e4719f_271_0.png)

### 目的

emacs 命令启动一个文本编辑器。大多数 Linux 发行版都安装了 emacs 以在 X 窗口系统运行，但它也可以被安装并配置为在终端界面运行。

# 第 7 章：文本处理命令 257

> 注意

emacs 的完整文档可以通过 info 命令在网上找到。（输入 info emacs。）

### 选项

- +number 打开位于第 *number* 行的文件。
- -font font 为窗口指定等宽字体。（用于 X 窗口。）
- -i 在将 emacs 窗口最小化时使用百叶池位图图标。（用于 X。）
- -name name 为初始 X 窗口指定一个名称。
- -nw 在 X 下的终端界面工作。
- -q 不加载初始化文件。
- -r 以反色视频显示。（用于 X。）
- -t file 使用 *file* 作为终端代替标准输入/输出。
- -title title 为初始 X 窗口指定一个标题。
- -u user 加载用户的初始化文件。

### 相关命令

- elvis
joe
jove
vi

| expand 将制表转换为空格 | expand 选项文件(s) |

### 目的

expand 命令将制表转换为空格。

### 选项

- -i 仅转换行首的制表。

### fgrep

搜索模式或表达式

fgrep string file(s)

### 目的

fgrep 命令在文件中搜索你输入的文本字符串，并输出包含该文本的行。你可以输入多个文件名或从标准输入管道传输文本。

> 注意

grep 是 egrep 和 grep 命令的兄弟版本，通常被认为三者中最简单。运行 fgrep 等同于运行 grep -F string。

### 选项

- -A num 显示匹配模式后的 num 行。
- -B num 显示匹配模式前的 num 行。
- -b 返回匹配行的块号。
- -c 返回匹配项的数量，而不列出具体的匹配项。
- -C 显示匹配模式前后的两行。
- -e pattern 当模式以连字符 (-) 开头时搜索该模式。
- -f file 使用文件中的模式。
- -h 列出匹配项的行，但不列出包含这些行的文件。
- -i 匹配时忽略大小写。
- -L 列出包含匹配项的文件，但不列出具体的匹配项。
- -n 列出不包含匹配行的文件。
- -n 列出匹配行及其行号。
- -v 列出不匹配模式的行。
- -w 列出匹配的单词。
- -x 列出匹配的行。
- -num 显示匹配模式前后 num 行。

### 相关命令

egrep
grep

| fmt 格式化文件 | fmt 选项(s) 文件 |

### 目的

fmt 命令通过将文本对齐到右边界并消除换行来格式化文件。然而，fmt 命令会保留原始文件的空格、缩进和空行。

> > 注意

由于此功能不是由文本编辑器执行的，通常在文本编辑器内部调用（elvis 有此机制）或从文本编辑器管道传输。此外，由于它经常用于格式化文件并直接发送到打印机，它通常作为流水线中的一步。

### 选项

- -c 覆盖前两行的格式化。
- -p prefix 格式化以 prefix 开头的行。
- -s 覆盖合并行。
- -t 标记段。
- -u 应用单词间一个空格、句子间两个空格的均匀间距。
- -w num 设置行宽 num 个字符；默认值为 72。

### fold

将文本格式化为特定宽度

fold 选项(s) 文件(s)

### 目的

fold 命令将文本格式化为特定宽度，通过在单词中间折断来实现该宽度。默认为 80 个字符。

### 选项

- -b 计算字节而不是字符。在这里，制表和格式命令（如退格键和回车键）被视为可计数的。
- -s 仅在空格处折断。
- -w 设置行宽 num 个字符；默认值为 80。

### ghostview

显示 PostScript 文件
（X 窗口系统命令）

ghostview 选项(s) 文件名

### 目的

ghostview 命令使用 ghostscript 解释器显示 PostScript 文件。该命令与许多选项相关，但通常只带文件名调用。（通常使用 gv 命令代替 ghostview。）

> **交叉引用**

查看在线手册页获取更多关于许多选项的信息。（输入 man gv 查看描述。）

### grep

在文件中搜索文本字符串

grep 选项(s) 模式 文件(s)

### 目的

grep 命令在文件或多个文件中搜索文本字符串（称为模式或表达式），并在屏幕上显示搜索结果。

> 注意

grep 命令是 grep 和 egrep 命令的亲属。

### 选项

- -A num 显示匹配模式后的 num 行。
- -b num 返回匹配行的块号。
- -B num 显示匹配模式前的 num 行。
- -c 返回匹配项的数量，而不列出具体的匹配项。
- -C 显示匹配模式前后的两行。
- -e pattern 当模式以连字符 (-) 开头时搜索该模式。
- -f file 使用文件中的模式。
- -h 列出匹配项的行，但不列出包含这些行的文件。
- -i 匹配时忽略大小写。
- -1l 列出包含匹配项的文件，但不列出具体的匹配项。
- -L 列出不包含匹配行的文件。
- -n 列出匹配行及其行号。
- -s 抑制错误消息。
- -v 列出不匹配模式的行。
- -w 只列出匹配的单词。
- -x 只列出匹配的行。
- -num 显示匹配模式前后 num 行。

### 相关命令

egrep
grep

| fmt 格式化文件 | fmt 选项(s) |

### 目的

fmt 命令通过将文本对齐到右边界并消除换行来格式化文件。然而，fmt 命令会保留原始文件的空格、缩进和空行。

> > 注意

由于此功能不是由文本编辑器执行的，通常在文本编辑器内部调用（elvis 有此机制）或从文本编辑器管道传输。此外，由于它经常用于格式化文件并直接发送到打印机，它通常作为流水线中的一步。

### 选项

- -c 覆盖前两行的格式化。
- -p prefix 格式化以 prefix 开头的行。
- -s 覆盖合并行。
- -t 标记段。
- -u 应用单词间一个空格、句子间两个空格的均匀间距。
- -w num 设置行宽 num 个字符；默认值为 72。

### fold

将文本格式化为特定宽度

fold 选项(s) 文件(s)

### 目的

fold 命令将文本格式化为特定宽度，通过在单词中间折断来实现该宽度。默认为 80 个字符。

### 选项

- -b 计算字节而不是字符。在这里，制表和格式命令（如退格键和回车键）被视为可计数的。
- -s 仅在空格处折断。
- -w num 设置行宽 num 个字符；默认值为 80。

### ghostview

显示 PostScript 文件
（X 窗口系统命令）

ghostview 选项(s) 文件名

### 目的

ghostview 命令使用 ghostscript 解释器显示 PostScript 文件。该命令与许多选项相关，但通常只带文件名调用。（通常使用 gv 命令代替 ghostview。）

> **交叉引用**

查看在线手册页获取更多关于许多选项的信息。（输入 man gv 查看描述。）

### grep

在文件中搜索文本字符串

grep 选项(s) 模式 文件(s)

### 目的

grep 命令在文件或多个文件中搜索文本字符串（称为模式或表达式），并在屏幕上显示搜索结果。

> 注意

grep 命令是 grep 和 egrep 命令的亲属。

### 选项

- -A num 显示匹配模式后的 num 行。
- -b num 返回匹配行的块号。
- -B num 显示匹配模式前的 num 行。
- -c 返回匹配项的数量，而不列出具体的匹配项。
- -C 显示匹配模式前后的两行。
- -e pattern 当模式以连字符 (-) 开头时搜索该模式。
- -f file 使用文件中的模式。
- -h 列出匹配项的行，但不列出包含这些行的文件。
- -i 匹配时忽略大小写。
- -1l 列出包含匹配项的文件，但不列出具体的匹配项。
- -L 列出不包含匹配行的文件。
- -n 列出匹配行及其行号。
- -s 抑制错误消息。
- -v 列出不匹配模式的行。
- -w 只列出匹配的单词。
- -x 只列出匹配的行。
- -num 显示匹配模式前后 num 行。

### 示例

```
$ grep "pixmap" *
```

### 相关命令

egrep
fgrep

| grodvi | grodvi 选项(s) |
| Convert Groff | 文件(s) |

### 目的

grodvi 命令将 groff 输出转换为 TeX DVI 格式。

### 选项

- -d 不使用 pic 实现绘图命令。
- -Fdir 搜索目录 dir 用于字体和设备文件。
- -wn 设置默认行厚度为 em 的千分之一。

### 相关命令

eqn
groff
tfmt
ttroff

### groff

格式化 Groff 文档

groff 选项(s) 文件(s)

### 目的

groff 命令是 groff 格式命令的前端。它通常运行 troff 程序和处理器为特定设备准备文档。

处理器由设备文件中的 postpro 命令指定。

### 设备

- - ps PostScript 打印机和预览器（默认）。
- -dvi TeX DVI 格式。
- -x75 X Window 75-dpi 预览器。
- -x100 X Window 100-dpi 预览器。
- -ascii 无格式的打印机。
- -latin1 使用 ISO Latin-1 字符集的打印机。

### 选项

- -e 使用 eqn 预处理。
- -p 使用 pic 预处理。
- -R 使用 refer 预处理。
- -s 使用 soelim 预处理。
- -t 使用 tbl 预处理。
- -V 在不执行管道的情况下打印管道。
- -z 抑制 troff 输出；打印错误消息。
- -Z 覆盖来自 troff 的处理器输出。
- -P 将参数传递给处理器。
- -L1 将输出发送到打印机。
- -Larg 将参数传递给队列。
- -T 为 dev 准备输出。默认是 ps。
- -X 使用 gxditview 预览而非常用的处理器。
- -N 不允许 eqn 分隔符有换行。
- -S 在安全模式下运行。

### 相关命令

eqn
postpro
troff
tblj

![](img/2cc16c5632743593217f446101e4719f_279_0.png)

### 目的

grolj4 命令是 HP LaserJet 4 系列的 groff 驱动器，产生 PCL5 格式输出。

### 选项

- -cn 每页打印 n 份。
- -Fdir 在 dir/devlj4 中搜索字体和设备描述文件。
- -l 以横向方向打印文档。
- -p size 设置纸张尺寸为：letter, legal, executive, a4, com10, monarch, c5, b5, 或 dl。
- -wn 设置默认行厚度为 em 的千分之一。



groups 驱动
用于 groff 的 PostScript

### groups 选项
filename(s)

### 目的

groups 命令是 groff 的 PostScript 驱动程序。它现在是一个有些多余的命令，因为 groff 的默认输出已经是 PostScript。

### 选项

- -bn 用于不符合《文档结构规范 3.0》的预览器和打印机调度程序。n 指定了 groff 如何处理这种情况；具体值请参考在线手册页。
- -cn 打印每页的 n 份副本。
- -Fdir 在目录 dir/devname 中搜索字体和设备描述文件。
- -g 猜测页面长度。
- -l 以横向方向打印文档。
- -m 开启手动进纸。
- -wn 将默认行线宽设置为 em 的 n 千分之一。

### 相关命令

- -eqn
groff
tfmtodit
tgroff

## groty 专为打字机格式化输出

### groty 选项
filename(s)

### 目的

groty 命令为打字机类型设备格式化输出。

### 选项

- -b 抑制粗体字符的覆盖打印。
- -B 对粗体斜体字符使用覆盖打印。
- -d 忽略所有 \D 命令。
- -f 使用换页。
- -Fdir 在目录 dir/devname 中搜索字体和设备描述文件。
- -h 强制水平制表。
- -o 抑制覆盖打印，粗体或下划线字符除外。- -u 抑制斜体字符的下划线。
- -U 对粗体斜体字符使用下划线。

### 相关命令

```
eqn
groff
tfmtodit
ttroff
```

| gs Ghostscript 预览器 | gs 选项文件 |
|---|---|
| 目的 gs 命令读取一个或多个文件并将其作为 Ghostscript 程序执行。执行后，它将从标准输入流（通常是键盘）读取后续输入。每行都会被单独解释。要退出解释器，输入 quit 或 Ctrl-C。 | |

### 选项

- -h 打印帮助信息，包括可用设备。

# 第 7 章：文本处理命令

- -? 打印帮助信息，包括可用设备。
- -filename arg1 ... 将下一个参数视为文件名，但获取所有剩余参数（即使它们具有开关的语法形式），并在运行文件之前，在 userdict（而非 systemdict）中定义这些字符串的数组 ARGUMENTS。当 Ghostscript 完成文件执行后，它将返回 shell。
- -dname=token 在 systemdict 中定义一个给定定义的名称。该 token 必须恰是一个 token（由 token 操作定义）且不能包含任何空格。
- -sname=string 在 systemdict 中定义一个以给定字符串为值的名称。
- -q 启动 gs 时不显示正常的启动消息。
- -gnumber1xnumber2 指定宽度和高度。
- -rnumber1xnumber2 指定 X 和 Y 分辨率。
- -Idirectories 将指定的目录列表添加到库文件搜索路径头部。
- -- 告诉 Ghostscript 标准输入来自文件或管道。

```
head 显示文件开头
head options file(s)
```

### 目的

head 命令显示文件的开头。默认是十行。如果指定了多个文件，会在每个文件的开头放置一个页眉。

### 选项

- -c num 打印文件的前 *num* 字节。
- -c numk 打印文件的前 *num* 千字节。
- -c numm 打印文件的前 *num* 兆字节。
- -n num 打印文件的前 *num* 行。
- -v 在每个文件的开头打印页眉。

```
ispell
检查单词
拼写
(GNU 命令)
```

```
ispell 选项 file(s)
```

### 目的

ispell 命令根据系统字典检查文件或多个文件中的单词拼写。如果 ispell 在运行过程中遇到不在字典中的单词，它会询问你如何处理该单词，并显示拼写正确的单词，此时你输入一个命令。ispell 命令还会创建一个个人字典文件，该文件也会被检查，允许你将经常使用的单词存放在其中。（你无法更改系统字典文件。）如果你覆盖了 ispell 的建议，该单词将被添加到个人字典。

> 提示
ispell 命令被用作 emacs 文本器的拼写检查器。

### 选项

- -b 创建备份文件，在原始文件名后添加 .bak。
- -B 查找单词挤在一起（连接）时缺失的空格。
- -C 忽略连接字符串。
- -d file 使用文件作为字典文件，而非标准的 ispell 字典。
- -L num 显示拼写错误周围的 *num* 行。
- -M 在屏幕底部显示交互命令。
- -N 抑制交互命令 own。
- -n 检查 *nroff* 或 *troff* 文件的拼写。
- -p file 使用 *file* 作为个人字典文件，而非你的标准 ispell 个人字典。
- -P 抑制根/前缀组合的建议。
- -S 按正确性概率水平对替换单词进行排序。
- -t 检查 *TeX* 或 *LaTeX* 文件的拼写。
- -T type 假设文件格式化为 *type*。
- -w chars 将 127 以上的字符原样发送到终端。
- -W num 设置用于终端屏幕优化的波特率为 num。
- -V 每次按键后更新列数和控制键前缀。

### 命令

- -a 将单词添加到个人字典。
- -i 搜索系统字典。
- -q 不保存退出 ispell。
- -r 替换单词。
- -u 将单词添加到个人字典。
- -x 滚动窗口使光标位于窗口中心。
- !command 在启动 shell 后运行 *command*。

### 相关命令

- -wc

### joe
Joe 自己的编辑器
(GNU 命令)

### 全局选项
### 局部选项
file(s)

### 目的

joe 命令是一个 ASCII 文本编辑器。它具有“无模式”用户界面。

joe 命令模拟了多种编辑器：WordStar、pico 或 emacs。

### 注意

模式由命令控制，你可以输入。（输入 man joe 查看信息。）

### 交叉引用

查看在线手册页获取完整列表。

### 模拟命令行

- -joe 启动通用 joe。
- -jstar 以 WordStar 模式启动 joe。注意控制键。
- -jacs 以 emacs 模式启动 joe。
- -jpico 以 pico 模式启动 joe。
- rjoe 以限制模式启动 joe。

### 全局命令行

- -asis 将 127 以上的字符原样发送到终端，而非反向 128 以下对应的字符。
- -backpath path 将备份文件存储在指定的目录而非每个文件的原始位置。
- -baud nnn 设置用于终端屏幕优化的波特率为 nnn。
- -beep 在命令错误和光标超出边界时响铃。
- -columns nnn 设置屏幕列数为 nnn。
- -csmode 启动 joe 与 tty 之间的流控制，根据 termcap 条目向 tty 输出额外的 ^es。^es 条目允许终端在长终端命令后追赶。
- -exask 要求 ^KX 命令验证其即将写入的文件名。
- -force 强制文件最后一行为换行符。
- -help 显示帮助屏幕。
- -keepup 每次按键后更新状态行的列数和控制键前缀，而非每两次按键一次。
- -lightoff 关闭块高亮。
- -lines nnn 设置屏幕行数为 nnn。
- -marking 高亮 ^KB 和光标之间的文本。
- -mid 滚动窗口使光标位于窗口中心。此选项在没有滚动命令的慢速终端上是强制的。
- -nobackups 防止创建备份文件。




## 272 第二部分：命令

- -notice 防止在编辑器启动时显示版权声明。
- -nosta 移除最顶部的状态行。
- -noxon 关闭 S/^Q 的处理，这在 WordStar 或 emacs 模式下非常有用。
- -orphan 将额外的文件放在命令行而不是额外的窗口中。这对于尝试模仿 emacs 的 joe 很有用。
- -pg nnn 指定在执行 PgUp/PgDn (^U^V) 后保留的行数。如果给出 -1，则保留窗口的一半内容。
- -skiptop nnn 跳过屏幕顶部的 nnn 行。

### 本地选项

- +nnn 光标从指定的第 nnn 行开始。
- -crlf joe 使用 CR-LF 作为换行结束符，而不仅仅是 LF。这用于编辑 MS-DOS 或 VMS 文件。
- -word 当你输入的内容超出右侧边界时，joe 会对前一个单词进行折行。
- -autoindent 当你在缩进过的行上按下回车键时，该缩进会复制到新行。
- -overwrite 输入时将覆盖现有字符而不是在它们之前插入。
- -largin nnn 设置左边距为 nnn。
- -rmargin nnn 设置右边距为 nnn。
- -tab nnn 设置制表符宽度为 nnn。
- -indentc nnn 设置 ^K 和 ^J 的缩进字符。（32 为空格，9 为制表符）。
- -istep nnn 设置 ^K 和 ^J 的缩进步长。
- -linums 在每行前显示行号。
- -rdonly 以只读模式加载文件。
- -keymap name 使用 joerc 文件的备用部分进行按键序列绑定。

### 相关命令

- elvis
- emacs
- jove
- pico
- vi
- vim

| 合并两个文件的行 (GNU 命令) | join 选项(s) file1 file2 |
| :--- | :--- |

### 目的

join 命令根据共同的字段合并两个文件（file1 和 file2）的行。

### 选项

- - -1 field 在 file1 的第 field 字段上合并。
- - -2 field 在 file2 的第 field 字段上合并。
- -a file-number 打印 file1 或 file2 中每个无法配对的行的列表。
- -e string 用字符串替换空输出字段。
- -o field-list 使用 field-list 中的格式来构建输出行。
- -t char 将 char 插入作为输入和输出字段的分隔符。
- -v file 为 file（可以是 file1 或 file2）中的每个无法配对的行打印一行，而不是按正常方式输出。

### jove 文本编辑器 jove 选项(s) file(s)

### 目的

jove 命令启动 Jonathan 版本的 Emacs。它基于原始的 emacs 编辑器，尽管 jove 旨在兼容 emacs，但这两个编辑器之间存在一些主要差异，你不应该依赖它们的行为完全一致。

### 选项

- -d 指定当前目录。
- -+num 加载文件并将光标置于第 num 行而不是文件开头。如果未指定 num，则光标将位于文件末尾。
- -p file 解析后续参数指定的文件中的错误消息。假设错误消息的格式类似于 C 编译器、lint 或 grep 的输出。
- -ttag 在紧随 -t 之后的字符字符串上运行 g 命令（如果有，如 -tTagname），否则在后续参数上运行（如 -t Tagname）。
- -w 将窗口分为二。发生这种情况时，两个窗口都显示同一个文件，或者读取列表中的第二个文件并在自己的窗口中显示。
- -r 运行 jove 恢复程序。当系统崩溃、jove 崩溃或在 jove 中意外注销时使用此命令。如果有任何需要恢复的缓冲区，它将找到它们。

### 相关命令

- elvis
- emacs
- joe
- pico

## 第7 章：文本处理命令 275

vi
vim

less 选项(s) file(s)

### 目的

less 命令交互式地显示文件的部分。它被设计为旧 UNIX more 命令的更高级版本——它允许你在文件中向后移动也可以向前移动——而且它只读取文件的部分而不是整个文件，因此它比文本编辑器更快。你可能会发现 less 命令是你经常使用的命令之一，因为它非常灵活，并提供了 cat 命令和你的编辑器的最佳特性。该命令的 X Window 版本 xless 同样存在。它的工作原理与 less 命令相同， 它在 X 窗口中运行。

### 选项

- -? 显示可用命令及其功能摘要。
- --help 显示可用命令及其功能摘要。
- -a 在最后显示的行之后创建一个新的显示（默认是两行）。
- -buffers 指定字节大小的缓冲区。每个文件使用一个缓冲区。
- -B 如果通过管道读取数据，则根据需要自动分配缓冲区。

## 276 第二部分：命令

- -c 从顶部而不是底部重绘屏幕。
- -C 从顶部而不是底部重绘屏幕，并在绘图前清除屏幕。
- -d 抑制在“哑”终端上显示的错误消息，例如提示终端没有清除屏幕的能力。
- -e 在第二次到达文件末尾时退出 less。
- -E 在第一次到达文件末尾时退出 less。
- -f 强制 less 强制打开非普通文件（如目录或设备驱动程序），并在打开二进制文件时抑制错误消息。
- -g 高亮显示匹配最后一次搜索的字符串。
- -G 抑制字符串的高亮。
- -hnum 指定向后滚动的最大 num 行数。
- -i 搜索时忽略大小写。如果搜索模式中包含大写字母，则考虑大小写。
- -I 搜索时忽略大小写，即使搜索模式中包含大写字母。
- -jnum 指定一个置于顶部的“目标”行。这可以是文本搜索、行号、百分比或标记位置的对象。负数会将“目标”行相对于屏幕底部定位。
- -kfilename 打开 less 格式的文件，而不是作为普通文件打开。
- -m 以类似 more 命令的详细模式打开，在屏幕底部列出百分比。
- -M 以详细模式打开，屏幕底部列出百分比和行号。
- -n 关闭行号。

## 第7 章：文本处理命令

- -N 在每行前显示行号。
- -n 从管道输出到文件。如果文件存在，less 会询问是否覆盖。
- -O 从管道输出到文件。如果文件存在，less 不询问是否覆盖。
- -pattern 从第一次出现 pattern 的的地方。
- -prompt 定义三种提示方式：
- -Pstring 长字符串提示。
- -Pmstring 中字符串提示。
- -Plstring 短字符串提示。
- -q 在尝试滚动文件末尾或回到开头时静默模式。
- -Q 完全静默模式，不会产生系统声音。
- -r 显示原始字符而不是波浪号。可能会导致显示错误。
- -s 将连续的空行合并为一个。通常用于 nroff 文件。
- -S 将长屏幕的行裁剪而不是折叠到下一行。
- -ttag 编辑包含标签的文件，由 ctags 命令生成。
- -Ttagfile 指定使用的 tags 文件而不是 ./tags。
- -u 将退格和返回视为打印字符。
- -U 将退格和返回视为控制字符。
- -V 显示 less 版本号。
- -w 将文件后的行显示为空行而不是波浪号~。
- -xnum 设置制表符位置，默认为 8。
- -X 禁止向终端发送 termcap 初始化和去初始化字符串。

### 第二部分

- -yn 指定向前滚动的最大行数。
- -z] 将默认滚动窗口大小改为 num 行；默认是一个屏幕。

### 命令

h 显示帮助信息。
- 空格、Ctrl-V、f、Ctrl-F 向前滚动默认行数（一个窗口，可以通过 -z 选项更改）。
- z num 向前滚动默认行数；如果指定 num，则将成为新的窗口大小。
- 回车、Ctrl-N、e、Ctrl-E、j、Ctrl-D num 向前滚动 n 行（默认 1）。
- 向向前一行。
- 向前半个屏幕；如果指定 num，less 将向前滚动该行数，并成为默认值。
- b、Ctrl-B、Esc-v 向后滚动默认行数（一个窗口，可以通过 -z 选项或 w 命令更改）。
- w num 向后滚动默认行数（一个窗口，可以通过指定 num ）。
- y、Ctrl-Y、Ctrl-P、k、Ctrl-K num 向后滚动默认行数（一行）。
- u、Ctrl-U num 向后滚动默认行数（半个屏幕）。如果指定 num，它将成为 d 和 u 命令的默认值。



, % num 滚动到文件的 *num* 百分比位置。
Num 必须在 0 到 100 之间。

{
如果 * 出现在屏幕的第一行，则滚动到匹配的 { }。
}

如果 } 出现在屏幕的第一行，则滚动回匹配的 {。

(
如果 * 出现在屏幕的第一行，则滚动到匹配的 )。
)

如果 ) 出现在屏幕的第一行，则滚动回匹配的 (。

[
如果 * 出现在屏幕的第一行，则滚动到匹配的 ]。
]

如果 ] 出现在屏幕的第一行，则滚动回匹配的 [。

Esc-Ctrl-F char1 char2
如果 *char1* 出现在屏幕的第一行，则滚动到匹配的 *char2*。

Esc-Ctrl-B char1 char2
如果 *char2* 出现在屏幕的第一行，则滚动回匹配的 *char1*。

m letter
用小写字母 *letter* 标记当前位置。

' letter
返回到用小写字母 *letter* 标记的位置。

Ctrl-X Ctrl-X
返回到用小写字母 *letter* 标记的位置。

/pattern
从显示的第二行开始，搜索 *pattern* 的下一次出现。

!pattern
搜索下一个不包含 *pattern* 的行。

/*pattern
从显示的第二行开始搜索 *pattern* 的下一次出现，并将搜索范围扩展到命令行列表中的后续文件。

/@pattern
从命令行列出的第一个文件的第一行开始，搜索 *pattern* 的下一次出现。

?pattern
从屏幕第一行之前的行开始，向文件中文件中搜索 *pattern* 的下一次出现。

# 280 第二部分：命令

?!pattern向后搜索不包含 pattern 的行。

?*pattern从屏幕第一行之前的行开始，向后搜索 pattern 的下一次出现，并将搜索范围向后扩展到命令行列表中的之前的文件。

?@pattern 从命令行列出的最后一个文件的最后一行开始，搜索 pattern 的下一次出现。

Esc-/pattern从显示的第二行开始，搜索 pattern 的下一次出现，并将搜索范围扩展到命令行列表中的后续文件。

Esc-*pattern从屏幕第一行之前的行开始，向后搜索 pattern 的下一次出现，并将搜索范围向后扩展到命令行列表中的之前的文件。

n 重复上一次搜索。

N 重复上一次搜索，但方向反向。

Esc-n 重复上一次搜索，并将搜索扩展到命令行中指定的文件。

Esc-N 重复上一次搜索，但方向反向，并将搜索扩展到命令行中指定的文件。

Esc-u 关闭对搜索匹配模式的高亮显示。

:e filename 打开一个新的文件名。如果未指定新文件，则重新加载当前文件。

Ctrl-X, Ctrl-V, E filename打开一个新的文件名。如果未指定新文件，则重新加载当前文件。

:n num 打开 less 命令行中输入的下一个文件。如果存在 *num*，则打开该数字指示的文件。

:p num 打开 less 命令行中输入的上一个文件。如果存在 *num*，则打开该数字指示的文件。

:x num 打开命令行上的第一个文件。如果存在 *num*，则打开命令行上该数字指示的文件。

= Ctrl-G, :f 返回正在查看的文件信息：名称、行号、正在显示的最后一行的字节偏移量、文件长度、文件行数以及最后一次显示行之上的文件百分比。

-option 在 less 运行时更改命令行 *option*。如果需要值，则会询问你；如果未输入新值，则显示当前值。

-+option 将命令行 *option* 重置为默认值。

--option 将命令行 *option* 重置为默认值的反值。在处理需要数值或字符串输入的选项时没有用处。

_option 返回 *option* 的当前值。

+command 每当加载新文件时运行 *command*。

v 打印版本号。

q, :q, :Q, ZZ 退出 less。

v 启动编辑器（由环境环境变量 VISUAL 或 EDITOR 定义）来编辑当前文件。

! shell-command 执行指定的 *shell-command*。要在命令中列出当前文件，使用百分号 (%)。要在命令行中列出之前查看的命令，使用井号 (#)。要重复上一个 shell 命令，使用 !!。要启动一个没有命令的 shell，使用 !。

### 第二部分：命令

使用 mark_letter 将文件的部分通过管道发送到指定的 shell-command。（使用 m letter 命令标记文件。）该部分的起始是屏幕顶部，结束部分是屏幕底部。

### 编辑命令

- * 左箭头, Esc-h 将光标向左移动一个空格。
- * 右箭头, Esc-l 将光标向右移动一个空格。
- * Ctrl-left, Esc-b 将单词向左移动。
- * Ctrl-right, Esc-w 将单词向右移动。
- * Home, Esc-0 将光标移动到屏幕开头。
- * End, Esc-$ 将光标移动到屏幕末尾。
- * Backspace 删除左侧的字符。
- * Delete, Esc-x 删除光标下的字符。
- * Ctrl-Backspace, Esc-b 删除左侧的单词。
- * Ctrl-Delete, Esc-x 删除光标下的单词。
- * 上箭头, Esc-k 获取上一行。
- * 下箭头, Esc-j 获取下一行。
- * Tab 补全部分文件名。如果有多个匹配，每次使用 Tab 都会循环显示文件名。
- * Esc-Tab 补全部分文件名。如果有多个匹配，每次使用 Tab 都会反向循环文件名。
- * Ctrl-L 补全部分文件名。如果有多个匹配，将显示所有文件名。

Ctrl-U 删除行或取消命令。



-n 假设文件是由 ditroff 生成的。

-p 使用 `pr` 命令格式化文件（与 `print` 相同）。

-t 假设文件是由 troff 生成的。

-v 假设文件包含用于如 Benson Varian 等设备的位栅图像。

### 通用选项

-C class 在突发页（burst page）上指定作业分类。

-h 抑制突发页的打印。

-i [col] 缩进输出的列数数字。如果未指定 col，则每行将缩进八个字符。

-m 在打印作业完成后发送邮件。

-Pprinter 将输出发送到打印机。

-r 在置存 spooling完成后或打印完成后删除文件（配合 -s 选项）。

-s 使用符号链接而不是将文件复制到置存目录。如果你执行了此操作，请在文件打印之前不要修改它们。

-T title 为 `pr` 指定标题名称，而不是文件名。

-U user 指定一个在突发页上打印的用户名。

-wnum 使用 `num` 作为 `pr` 的页宽。

-num 打印每个文件的 `num` 份。

-[num]font 指定要挂载在字体位置 `num` 的字体。

### 相关命令

+   lpc
lpd
lpq
lprm
pr

### lprm
从打印队列中移除打印作业
lprm option(s) job-ID
username

### 目的

`lprm` 命令从打印队列中移除打印作业。使用 `lpq` 命令来确定作业 ID。你必须是作业的所有者或超级用户才能移除打印作业。

### 选项

+   -Pprinter 指定一个打印队列而不是默认队列。
-user 删除由用户拥有的作业。

### 相关命令

+   lpd
lpq
l1pr

### more
显示文件的全部或部分
more option(s) file(s)

### 目的

`more` 命令一次显示一个屏幕文件的全部或部分。在功能上，它在很大程度上被 `less` 命令取代了。

> 注意
输入 q 退出 `more`。按空格键继续向下滚动查看文件。
当 `more` 显示文件时，可以使用某些命令。它们与 `vi` 文本编辑器一样在屏幕底部输入。这些命令将在本节的后续显示。

### 命令

Retrun 显示下一行文本。如果提供了参数，该参数将成为新的默认值。

b 或 ^B 向后移动一屏幕文本。如果提供了参数，该参数将成为新的默认值。

d 或 ^D 滚动 11 行文本。如果提供了参数，该参数将成为新的默认值。

f 跳过一屏幕文本。如果提供了参数，该参数将成为新的默认值。

h 或 ? 显示命令摘要。

Ctrl-L 重绘屏幕。

n 重复上一次搜索。

q 或 Q 退出 `more`。

s 跳过一行文本。如果提供了参数，该参数将成为新的默认值。

v 在当前行启动 `vi`。

z 显示下一屏文本。如果提供了参数，该参数将成为新的默认值。

' 回到上一次搜索开始的地方。

= 显示当前行号。

/pattern 搜索模式 pattern 的下一次出现处。如果提供了参数，该参数将成为新的默认值。

!cmd 或 !cmd 在子壳中运行 cmd。

:f 显示当前文件和行号。

:n 打开下一个文件。

:p 打开上一个文件。

. 重复上一个命令。

### 选项

+num 从行号 `num` 开始显示。

+/pattern 在显示文件前搜索模式 pattern。

-num 将屏幕大小设置为 `num` 行。

-c 关闭滚动；相反，屏幕将通过清空并从顶部开始绘制新文本。

-d 在屏幕底部显示以下提示：[按空格继续，按'q' 退出]。

-f 统计逻辑行数，而不是屏幕行数。

-l 忽略 ^L（分页符）作为特殊字符。

-p 关闭滚动；相反，屏幕将通过清空并显示新文本。

-s 将多个空行压缩为一行。

-u 抑制下划线。

### 相关命令

less

| 调用 groff 命令的 nroff | nroff option(s) filename |
| :--- | :--- |

### 目的

`nroff` 命令调用 `groff` 命令来模拟其他 UNIX 系统上的 `nroff` 命令。

> 交叉引用

请参见本章较早之前的 `groff` 命令以获取详情和命令行选项。

### 相关命令

+   groff

+   troff

### paste
合并文件
(GNU 命令)

目的

`paste` 命令合并文件并将文件并排放置。`file1` 的第一行将后随 `file2` 的第一行，中间用制表符分隔并以换行符结束。

选项

+   -dchar 使用 `char` 代替制表符来分隔行。
-s 合并文件中的行，而不是在同一行上打印两个文件的内容。

相关命令

+   cut
join

### pico
文本编辑器

pico option(s) filename

目的

`pico` 文本编辑器是一个基于 `pine` 邮件管理器中使用的组合工具的轻量级工具。如果你经常使用 `pine` 并希望在你的工具中保持某些一致性，你可能希望使用 `pico` 来满足基础编辑需求。

选项

+   +n 加载一个文件，并将光标所在的第 `n` 行插入到文件中。
-d 重新绑定 Del 键，使其删除光标所在的字符而不是其左侧的字符。

-e 启用文件名补全。

-g 在当前选择之前显示光标，而不是在显示器的左下角。

-k 删除光标到行末尾的文本，而不是删除整行。

-m 启用鼠标功能；仅在 X Window 环境下运行时可用。

-nn 在新邮件到达时通知你；每隔 `n` 秒检查一次。

-o dir 在 `dir` 目录中工作。

-rn 设置第 `n` 列以限制右边距。

-t 启用工具模式，该模式既不提供保存退出的提示，也不提供缓冲区重命名。用于在其他工具（如 `elm` 或 `Pnews`）中编写文本。

-v 在不编辑的情况下查看文件。

-w 禁用换行。

-x 禁用底部的键菜单。

-z 启用 ^z 挂起。

### 相关命令

pine

### pr
准备打印文件
(GNU 命令)
pr options file

### 目的

`pr` 命令准备打印文件。它并没有实际打印文件——你需要将文件发送到打印机来实现这一点——但它会创建一个适用于打印的分页、列格式文件。

### 选项

+   +page 从 *page* 开始打印。

+   -column 打印 `column` 数字列。

+   -a 跨列打印而不是向下打印。

+   -b 在最后一页对齐列。

+   -c 使用脱字符 (^G) 打印控制字符；其他不可打印字符使用八进制表示。

+   -d 输出双倍行距。

+   -e width 将制表符扩展为空格；如果指定了 *width*，则交换宽度。

+   -F 在页之间使用分页符而不是换行符。

+   -i[out-tab-char] 用 *header* 替换标题中的文件名。

+   [out-tab-width] 将空格替换为制表符。你可以指定输出制表符 (*out-tab-char*) 或制表符宽度 (*out-tab-width*)，默认值为8。

+   -l page-length 将页设置为 *page-length* 行；默认值为66。

+   -m 并打印所有文件，每列一个。

+   -n[number-separator] 在每列前打印行号；对于并行文件，在每行前打印行号。可选参数 *number-separator* 是数字后的字符。可选参数 *digits* 是每个行号的位数；默认值为5。

+   -o left-margin 使用 *left-margin* 宽的边距偏移每行。

+   -r 在无法打开文件时忽略警告。

+   -s[column-separator] 使用单个字符 *column-separator* 分隔列。

-t 抑制所有页的页眉和页脚。

-v 使用八进制表示打印不可打印字符。

-w page-width 将页宽设置为 *page-width* 列；默认值为72。

### 相关命令

+   lpd
llpq
lpr
lprm

### printf
目的

`printf` 命令打印字符串，使用的 & 指令和 \ 转义字符与 C 语言的 `printf` 命令相同。（输入 `man 3 printf` 获取指令和转义字符的描述。）

### psbb
目的

`psbb` 命令从 PostScript 文返回边界框的尺寸。如果找到了，它会打印一行：
lx lly urxury
如果没有找到，它会打印一条消息并退出。



## 第 7 章：文本处理命令

```
refer
预处理
书目
引用
(GNU 命令)
```

refer option(s) filename

### 目的

refer 命令为 groff 命令预处理书目引用。它将 filename 的内容复制到标准输出，但位于 .[. 和 . 之间的行会被解释为引引用，而位于 .R1 和 .R2 之间的行将被解释为关于如何处理引用的命令。

关于引用及其意义的更详细描述，以及对晦涩选项的引用，可以在 man 页面中找到。（输入 `man refer` 查看相关信息。）

```
rev
反转文件行
```

rev filename

### 目的

rev 命令反转文件的行顺序。它将文件复制到标准输出，并反转每行中字符的顺序。我们尚未看到过该命令的实际应用，也不确定是否存在此类应用。

```
sdiff
合并两个文件
(GNU 命令)
```

sdiff option(s) file1 file2

### 目的

sdiff 命令合并两个文件并将结果打印到第三个文件中。

### 选项

-a
将所有文件视为文本并按行进行比较，即使它们看起来不像文本。

-b
忽略空白字符数量的变化。

-B
忽略仅插入或删除空行的变化。

-d
更改算法以找到更小的变化集。

-H
使用启发式方法加速处理具有大量散乱小变化的大文件。

--expand-tabs
在最终文件中将制表符扩展为空格。

-i
忽略大小写变化。

-I regexp
忽略仅插入或删除匹配 *regexp* 的行的变化。

--ignore-all-space
在比较行时忽略空白字符。

--ignore-blank-lines
忽略仅插入或删除空行的变化。

--ignore-case
忽略大小写。

--ignore-matching-lines=regexp
忽略插入或删除匹配 *regexp* 的行的变化。

--ignore-space-change
忽略空白字符数量的变化。

-l
仅打印两个公共行的左侧列。

--minimal
更改算法以寻找更小的变化集。

-o file
将合并后的输出保存到 *file*。

-s
不打印公共行。

--speed-large-files    使用启发式方法加速处理具有大量散乱变化的大文件。

-t    将制表符扩展为空格。

--text    将所有文件视为文本。

-w columns    设置输出的列宽。

-W    在比较行时忽略水平空白字符。

### 相关命令

+ cmp
comm
diff
diff3

### 目的

sed 命令读取文件并根据命令列表修改输入。然后将输入写入标准输出。

### 选项

-a    作为 'w' 函数参数列出的文件在任何处理开始之前会被创建（或截断）。

-e command    将 command 指定的编辑命令添加到命令列表中。

-f command_file    将 command_file 中的命令添加到命令列表中。

-n    抑制每行输入的打印回显（echoing）。

# 选择性传输字符 (selection Transfer Characters)

### 目的

selection 命令从当前的 Linux 控制台获取字符，并将其粘贴到当前控制台的其他部分。该命令通常在系统启动时从 /etc/rc.local 文件启动，并作为后台进程运行。

### 选项

+   -aacc 超过 delta 像素的移动将乘以 accel（默认值为 2）。

+   -bbaud-rate 设置鼠标的波特率。这是一个应避免的选项，因为设置错误的波特率会导致鼠标冻结，Linux 和 XFree86 的其他地方提供了其他设置波特率的机制。

+   -cl|m|r 将复制键设置为左侧 (l)、中间 (m) 或右侧 (r)。（默认为左侧）。

+   -ddelta 超过 delta 像素的移动将乘以 accel（默认值为 25）。

+   -mmouse-device 设置鼠标设备（默认为 /dev/mouse）。

+   -pl|m|r 将粘贴键设置为左侧 (l)、中间 (m) 或右侧 (r)。（默认为右侧）。

+   -ssample-rate 设置鼠标的采样率（默认值为 100）。

+   -tmouse-type 设置鼠标类型：Microsoft 为 ms，Mouse Systems 为 msc，MS 系列为 mm，Logitech 为 logi，总 Mouse 为 bm，MSC 3 字节为 sun，PS/2 为 ps2。默认是 ms。尽管此功能似乎很有用，但这是一个应避免的选项，因为设置鼠标类型会导致鼠标冻结，Linux 和 XFree86 的其他地方提供了其他设置鼠标类型的机制。

-wslack 设置指针重新出现在屏幕另一侧之前的空隙量。

### 相关命令

gpm

| soelim 解析请求 | soelim option filename(s) |
|---|---|

### 目的

soelim 命令解释 groff 输入中的 .so 请求。它读取指定的文件名并替换如下形式的行：

+   * so filename
它将这些行替换为 filename 的内容。

### 选项

-C 即使在 .so 后面跟着非空格或换行符的字符，也能识别 .so。

### 相关命令

groff

| sort 排序、合并或比较文件行 (GNU 命令) | sort option(s) filename(s) |
|---|---|

### 目的

sort 命令对文件的行进行排序、合并或比较。它将结果输出到屏幕上。可以使用选项显示更多或更的内容。

### 模式选项

-c 检查文件是否已排序；如果不是，则打印错误信息。

-m 合并文件，但要求文件必须是排序的。

### 通用选项

+POS1 [-POS2] 在每行中设置字段作为排序键。

-b 忽略行首空白。

-d 排序时忽略除字母、数字和空白外的字符。

-f 将小写字母转换为等大写字母进行排序。

-i 忽略非 ASCII 字符。

-k POS1[,POS2] 在每行中设置字段作为排序键。

-M 将月份缩写转换为大写。

-n 使用数值比较。

-o file 将输出写入文件。

-r 反转顺序。

-t 指定分隔符。

-u 显示一组相等行。

### 目的

split 命令将文件分成两个或多个输出文件。默认每 1000 行分割一个文件，但可以通过命令行选项进行更改。

### 选项

+   - lines 使用行数作为文件的数量（默认为 1000）。

+   - b bytes[bkm] 按字节数分割文件。你可以添加字符来指定不同的单位：
- b 512 字节块
- k 1K 块
- m 1MB 块

+   -C bytes[bkm] 按字节数分割文件，但确保文件在完整行处结束。你可以添加字符来指定不同的单位：
- b 512 字节块
- k 1K 块
- m 1MB 块

### 目的

tac 命令（cat 的相反）用于按反序显示文件；即文件的最后一行先显示，然后是倒数第二行，依此类推。

### 选项

-b 将分隔符附加到之前的记录的开头。

-r 将分隔符设置为正则表达式。

-s string 设置字符串作为记录分隔符。

### 相关命令

cat

| tail | tail option(s) filename |
|---|---|
| 输出最后十行 | |
| 文件行 | |
| (GNU 命令) | |

### 目的

tail 命令将 filename 的最后十行打印到屏幕上。可以使用选项显示更多或更少的内容。该命令是 head 命令的相反，用于显示文件的前十行。

### 选项

+   -c num 显示 num 字节。
-f 循环尝试读取文件末尾更多字符，假设文件正在增长。
-1 num 显示 num 行。
-q 不打印文件名头。
-v 打印文件名头。



## 第 7 章：文本处理命令 301

| tr 翻译或删除字符 (GNU 命令) | tr option(s) [string1] [string2] |
| :--- | :--- |

### 目的

tr 命令翻译或删除字符，将 string1 替换为 string2。

+ 交叉引用
请查看在线手册页以获取可用选项列表。

| troff 文本格式化 (GNU 命令) | troff option(s) filename |
| :--- | :--- |

### 目的

troff 命令是一个文本格式化器，是 groff 格式化家族的一部分。你通常不会单独使用它，而是通过 groff 命令来调用它。

+ 交叉引用
查看本章较早之前的 groff 命令以获取可用选项和更多信息。

### 相关命令

groff

### unexpand 转换文本文件制表符 (GNU 命令)

unexpand option(s) filename

### 目的

unexpand 命令将文本文件中的空格转换为制表符。

### 选项

- -a 将所有两个或多个空格或制表符的字符串（而不只是开头的）转换为制表符。
- -t tab 设置制表符的间距，而不是默认的 8。

## uniq 去除重复行 (GNU 命令)

uniq option(s) filename1 filename2

### 目的

uniq 命令从指定的文件 (filename1) 中删除重复行，并将其发送到另一个文件 (filename2)，或者如果没有指定文件名，则发送到标准输出。

### 选项

- -c 统计重复行。
- -d 返回重复行，但不返回唯一的行。
- -fn 跳过行的前 n 个字段；字段由空格或制表符分隔。
- -sn 跳过字段的前 n 个字符；字段由空格或制表符分隔。
- -u 返回唯一的行，重复行则将被丢弃。

## 第 7 章：文本处理命令 303

- -w n 比较行的前 n 个字符。
- -n 跳过行的前 n 个字段；字段由空格或制表符分隔。
- +n 跳过字段的前 n 个字符；字段由空格或制表符分隔。
- --check-chars=n 比较行的前 n 个字符。
- --skip-chars=n 跳过字段的前 n 个字符；字段由空格或制表符分隔。
- --skip-fields=n 跳过行的前 n 个字段；字段由空格或制表符分隔。

### 相关命令

- comm
- sort

```
vi
运行可视化文本编辑器
vi option(s) filename
```

### 目的

vi 命令启动一个可视化文本编辑器。在某些 Linux 系统中，它实际上是 elvis 文本编辑器的快捷方式。（从技术上说，其他 UNIX 系统上找到 vi 编辑器与这里的 vi 并不相同。）

> 交叉引用
查看本章较早之前的 elvis 命令以获取可用选项和更多信息。

```
vim
文本编辑器
vim option(s) filename
```

### 目的

vim 文本编辑器是一个兼容 vi 的文本编辑器，对于编辑文本文件非常有用。

### 交叉引用

查看在线手册页以获取可用选项列表。

| wc 统计文本文件字数 | wc option(s) filename |
| :--- | :--- |

### 目的

wc 命令统计文本文件中的行、单词和字符数；如果没有指定文件名，则统计标准输入。当与管道中的其他文本处理命令结合时，这是一个非常有用的命令。

### 选项

- -bytes 打印字符计数。
- -c 打印字符计数。
- --chars 打印字符计数。
- -l 打印文件的行数。
- --lines 打印文件的行数。
- -W 打印文件的单词数；这是默认值。
- --words 打印文件的单词数；这是默认值。

### 示例

```
$ wc /etc/passwd
21 26 750 /etc/passwd
```

## 第 7 章：文本处理命令 305

| xedit 启动文本编辑器 (X Window系统命令) | xedit filename(s) |
| :--- | :--- |

### 目的

xedit 命令启动一个在 X Window 系统下的简单文本编辑器。

| zcmp 比较并解压压缩文件 | zcmp option(s) file(s) |
| :--- | :--- |

### 目的

zcmp 命令解压 gzip 压缩的文件并调用 cmp。与此命令相关的选项实际上是 cmp 选项，它们会随压缩文件一起传递给 cmp。

> 交叉引用
查看本章较早之前的 cmp 命令以获取可用选项和更多信息。

### 相关命令

- - cmp
- gzip
- zcat
- zgrep
- zfgrep

## zdiff
解压文件

zdiff option(s) file(s)

### 目的

zdiff 命令解压 gzip 压缩的文件并调用 diff。与此命令相关的选项实际上是 diff 选项，它们会随压缩文件一起传递给 diff。

### 交叉引用
查看本章较早之前的 diff 命令说明以获取可用选项和更多信息。

### 相关命令

- - diff
- gzip

### zegrep
解压文件

zegrep option(s) file(s)

### 目的

zgrep 命令解压 gzip 压缩的文件并调用 egrep。与此命令相关的选项实际上是 egrep 选项，它们会随压缩文件一起传递给 egrep。

### 交叉引用
查看本章较早之前的 egrep 命令以获取可用选项和更多信息。

### 相关命令

- - egrep
- gzip
- zgrep
- zfgrep

## zfgrep
解压文件

z

 option(s) file(s)

### 目的

zgrep 命令解压 gzip 压缩的文件并调用 fgrep。与此命令相关的选项实际上是 fgrep 选项，它们会随压缩文件一起传递给 fgrep。

### 交叉引用
查看本章较早之前的 fgrep 命令说明以获取可用选项和更多信息。

### 相关命令

- - fgrep
- gzip
- zgrep
- zegrep

### zgrep
解压文件

z option(s) file(s)

### 目的

zgrep 命令解压 gzip 压缩的文件并调用 grep。与此命令相关的选项实际上是 grep 选项，它们会随压缩文件一起传递给 grep。

### 交叉引用
查看本章较早之前的 grep 命令以获取可用选项和更多信息。

### 相关命令

- - grep
- gzip
- zgrep
- zfgrep



## 第 8 章：网络/电子邮件命令 313

- -T 忽略之前设置为已忽略的新型层级中的新闻组。
- -v 设置 actsync 的详细输出级别，范围从 0（无调试信息）到 4（全调试信息）。
- -z 在执行每个命令之前，让 actsync 暂停 `sec` 秒。
- -d 忽略带有数字路径组件的新闻组。

### 相关命令

- -ctlinnd
- getlist
- innd
- printmail

## # 回答 answer 创建电话留言

### answer 选项(s)

### 目的

answer 命令是一个秘书工具，用于将电话留言转录为可以配合 `elm` 命令使用的格式的电子邮件消息。启动后，answer 会检查 .elm/aliases 文件以获取用户列表，并引导用户通过一个模拟电话留言条的表单（包含如收件人 Message-To 和请回电 Please Call 等字段）。

### 选项

- -p 提示消息字段。
- -u 允许不在 .elm/aliases 文件中的名称。

### 相关命令

- - elm
- mail
- printmail

### audiocompose
制作音频

### audiocompose filename

### 目的

audiocompose 命令用于录音。如果你想录制音频片段并附加到发出的邮件消息中，请使用此命令。在命令行运行此命令并指定一个文件名；系统会提示你录制文件，然后询问你是否在录制后收听该文件。

然后，你需要使用 audiosend、mailto 或 metamail 命令将文件附加到发出的邮件消息中。你必须在你的 Linux 系统上安装了音频设备，通常路径为 `/dev/audio`。

如果你想将此格式设置为系统的默认格式，你需要为 `audiocompose` 设置一个 `RECORD_AUDIO` 环境变量。

### 示例

```
$ audiosend hello
```

### 相关命令

- - audiosend
- mailto
- metamail
- showaudio

### audiosend
发送音频

### audiosend
e_mail_address

### 目的

与 audiocompose 不同，audiosend 命令既可以录音也可以将其电子邮件给另一个用户。音频段构成了整个邮件消息；你不能在邮件消息中附加文本或其他文件。

该命令非常简单：你在命令行上使用 audiosend 并配合一个电子邮件地址。（如果你未指定地址，命令将提示你输入。）命令随后会提示你主题（Subject）和抄送（Cc）字段，之后你录制消息。在发送消息之前，audiosend 会询问你是想重新录制还是收听。你必须在你的 Linux 系统上安装了音频设备，通常路径为 `/dev/audio`。

如果你想将此格式设置为系统的默认格式，你需要为 `audiocompose` 设置一个 `RECORD_AUDIO` 环境变量。

### 示例

```
$ audiosend hello
```

### 相关命令

- - audiocompose
- showaudio

### 目的

biff 命令通知你收到了新邮件，只要你的系统使用 sendmail 或 smail 作为邮件传输代理。要查看 biff 的当前状态，请在命令行中单独输入它。启用 biff 请使用 `y` 选项；禁用 biff 请使用 `n` 选项。

### 选项

- -n 开启 biff。
- -y 开启 biff。

### 相关命令

- - xbiff

### checknews
检查新新闻消息

### 目的

checknews 命令通常用于用户配置文件 (.profile) 或 shell 脚本 (.login) 中，以便调用 readiness 命令以便在用户登录时检查是否有未读的 Usenet 新闻消息。readiness 命令配合 `-c` 选项使用。

### 相关命令

readnews

### chfn
更改 finger 信息
chfn 选项(s)

### 目的

chfn 命令更改存储在你的 finger 个人资料中的信息。这些信息将通过网络返回给任何通过 finger 命令请求信息的人。这些信息包括你的姓名、办公室号码、办公室电话和家庭电话。如果你决定以交互方式输入新的 finger 信息（即你单独在命令行运行 chfn 时使用的过程），现有的 finger 信息将以括号形式返回。

> 注意
> 默认情况下，信息不会存储在 Linux 系统上；你必须手动输入。

### 选项

- -f name 输入你的全名。
- -h number 输入你的家庭电话。
- -o office 输入你的办公室号码。
- -p number 输入你的办公室电话。
- -u 返回帮助信息。
- -v 打印版本号。

### 示例

```
$ chfn
正在更改 Kevin 的 finger 信息。
Name [Kevin]:
Office [101]:
Office Phone [555-1212]:
Home Phone [555-1213]:
```

### 相关命令

- - answer
- finger
- passwd

### 目的

elm 命令是一个交互式邮件系统，其功能比 mail 命令更高级。你可以使用 elm 从命令行发送消息（带有来自命令行的文本输入），从命令行向用户发送文件，或者不指定任何内容并使用 elm 界面读取和发送邮件。

### 选项

- -a 使用方向键光标。
- -c 展开别名。
- -d level 设置调试级别。
- -f folder 从文件夹读取邮件而非收件箱。
- -i file 在发出的邮件消息中包含文件。
- -m 关闭菜单。
- -s 指定主题。

### 相关命令

- - fastmail
- mail
- metamail
- pine

| fastmail 选项(s) | |
| :--- | :--- |
| 快速发送邮件 | filename address |

### 目的

fastmail 命令用于从远程服务器获取邮件并将其转发到本地投递系统，在那里可以使用 elm 管理。fastmail 设计用于拨号上网，可以获取 POP3、IMAP 或 SMTP。

> 注意
> 请查看在线手册获取运行 fetchmail 的可用选项。

如果你没有在命令行上指定邮件服务器，fetchmail 将查询 ~/.fetchmail 列出的服务器。该文件也控制 fetchmail 的所有方面。通常，使用此文件配置 fetchmail 比在命令行传递选项更好。

### 通用选项

- -V 显示版本信息并验证 fetchmail 是否正常工作。
- -c 通知你有邮件等待，但不实际获取或删除。它还会关闭作为守护进程运行的 fetchmail。
- -s 静默模式，抑制正常输出到标准错误的所有/状态消息。
- -v 详细模式，fetchmail 与邮件服务器之间所有的控制消息都会输出到标准错误。

### 获取选项

- -a 从邮件服务器获取旧新消息。
- -k 将获取的消息留在邮件服务器上，而不是删除它们。
- -K 从远程邮件服务器删除已获取的消息。
- -F 在获取新消息之前，从邮件服务器删除之前获取的消息。此选项仅适用于 POP3 和 IMAP 服务器。
- -p 指定与邮件服务器通信时使用的协议。选项如下：

| | | |
| :--- | :--- |
| POP2 | 使用邮局协议 2。 |
| POP3 | 使用邮局协议 3。 |
| APOP | 使用 MD5 认证的 POP3。 |
| RPOP | 使用 RPOP 认证的 POP3。 |
| KPOP | 在端口 1109 上使用 Kerberos v4 认证的 POP3。 |
| IMAP | 使用 IMAP2bis、IMAP4 或 IMAP4rev1。 |
| IMAP-K4 | 使用 RFC 1731 Kerberos v4 认证的 IMAP4 或 IMAP4rev1。 |

### 相关命令

- - elm
- rmail
- sendmail



## 第8 章：互联网/电子邮件命令 321

IMAP-GSS 使用带有 RFC 1731 GSSAPI 认证的 IMAP4 或 IMAP4rev1。

ETRN 使用 ESMTP ETRN。

- -U, --uidl 强制在 POP3 中使用 UIDL。
- -P, --port 指定连接的 TCP/IP 端口。
- -r folder, --folder folder 获取整个文件夹。

## 中继选项

- -D domain, --smtpaddress domain 指定发送到 SMTP 的 RCPT 行中包含的域名。
- -m, --mda 强制将邮件直接发送到 MDA，而不是通过 25 端口。
- -S host, --smthost host 指定用于转发邮件的主机列表列表（hunt list）。
- -Z nnn, --antispam nnn 指定被解释为监听器垃圾邮件拦截响应的 SMTP 错误代码。值为 -1 可禁用此选项。

## 资源管理选项

- -b, --batchlimit num 指定在连接被故意断开并重建之前发送到 SMTP 监听器的最大消息数。
- -B, --fetchlimit 限制单次轮询从给定服务器接收的消息数。
- -e, --expunge num 设置向 IMAP 服务器发布 EXPUNGE 命令的频率（以消息数为单位）。
- -l, --limit num 指定大于 num 字节的消息将不会被获取，不会被标记为已读，并将将留在服务器上。

## 身份验证选项

- -A, --auth 指定身份验证格式。
可能的值有 password（密码）、kerberos_v5 或 kerberos（凯伯洛斯 认证）。

- -I specification, --interface specification 要求在轮询之前特定的接口设备必须处于开启状态并具有特定的本地 IP 地址（或范围）。

- -M interface, --monitor interface 监控 IP 接口的空闲状态。

- -u name, --username name 指定用户名。

## 杂项选项

- -E, --envelope 指定携带邮件地址副本的标头。

- -f path name, --fetchmailrc 指定 .fetchmailrc 文件的另一个位置。
- -i path name, --idfile path name 指定 .fetchids 文件的另一个位置。
- -n, --nowrite 禁用重写 RFC 822 地址标头。

### 相关命令

- elm
- imapd
- mail
- sendmail

```
finger
Return User Information finger option(s) user
```

### 目的

finger 命令返回关于用户的信息，这些信息存储在用户的 .plan 和 .project 文件中。（大多数用户并不会去设置这些文件，所以如果没有返回任何信息，请不要惊讶。）

此外，许多管理员出于安全考虑关闭了此功能。你可以指定用户作为登录名 [必须完全匹配] 或作为名或姓（将会返回所有匹配项；在网络环境中这可能是一个长列表）。

### 选项

- -l 以长格式显示信息。除了 -s 选项提供的信息（登录名、真实名、终端名、写入状态、空闲时间、办公室位置和办公室电话）外，该选项还增加了主目录、家庭电话号码、登录 shell、邮件状态以及 .plan、project 和 .forward 文件的内容。

- -m 覆盖对名和姓的匹配。
- -p 取消 .plan 和 .project 文件的投递。
- -s 以短格式显示信息：登录名、真实名、终端名、写入状态、空闲时间、办公室位置和办公室电话号码。

### 相关命令

chfn

| formail Format Mail | formail option(s) |
| :--- | :--- |

### 目的

formail 命令将标准输入（在此情况下通常是一个文件）格式化为邮箱格式，然后可以由邮件程序进行处理。

### 选项

- +num 跳过前 num 条消息。
- -num 仅分割 num 数量的消息。
- -a headerfield 为缺少标头的消息添加标头字段。
- -b 忽略虚假的 From 字段。
- -c 合并超过一行的标头字段。
- -d 允许松散格式化。
- -e 将消息紧挨放置，而不是在它们之间插入空行。
- -f 忽略非邮箱格式的行。
- -i headerfield 即使字段已存在也添加新的标头字段；旧的标头字段将被重命名为 Old-headerfield。

## frm 列表 From/Subject 字段

frm option(s) [folder username]

### 目的

frm 命令列出邮箱或文件夹中选中消息的 From 和 Subject 字段。

### 选项

- -n 使用与 readmsg 命令相同的编号方案。
- -q 在静音模式下工作，仅为指定的邮箱或文件夹生成一行摘要。
- -Q 在极静模式下工作，仅返回错误消息。
- -s status 使用状态来指定消息；状态可以是新的（new）、未读的（unread）、旧的（old）或已读的（read）。
- -S 总结消息数。
- -t 显示完整的 From 字段，即使这意味着取代 Subject 字段。
- -v 在列出内容之前打印标头。

### 相关命令

elm
mail
mailx
readmsgmsg

| ftp Transfer File | ftp option(s) host name |
| :--- | :--- |

### 目的

ftp 命令连接到远程计算机——是在你自己的网络还是更广泛的互联网。连接到远程计算机后，你可以来回复制文件、删除文件并查看目录内容，只要你在远程计算机上拥有适当的权限即可。（注：原文后续部分包含大量重复"Two different levels of the"等占位符，根据指令要求不重复输出原文）

### 第二部分：命令

- cr
- delete
- debug
- dir
- disconnect
- get
- glob
- hash
- help
- idle
- image
- bell
- binary
- bye
- case
- cd
- cdup
- chmod
- close
（注：原文末尾包含大量重复占位符，根据指令要求不重复输出原文）



### 第二部分：命令

| 命令 | 说明 |
| :--- | :--- |
| mdir filename(s) | 返回多个指定文件名的目录信息。 |
| mget filename(s) | 从远程机器获取指定的文件。 |
| mkdir directory | 在远程机器上创建一个新目录。 |
| mls directory localfile | 将远程目录的内容列到本地文件中。 |
| mode modename | 将模式更改为新的 modename。默认是流模式。 |
| modtime filename | 显示指定文件的最后修改时间。 |
| mput filename(s) | 将本地机器的指定文件上传到 FTP 服务器。 |
| newer remotefile | 如果远程文件比本地机器的版本新，则下载该远程文件。 |
| nlist directory localfile | 将远程目录的内容列到本地文件中。 |
| open host (port) | 打开到指定主机（以及可选端口）的连接。如果你没有指定主机，命令将提示你输入一个主机。 |
| prompt | 关闭（或开启）交互式提示。 |
| proxy command | 在另一个连接上运行命令。 |
| put file1 file2 | 将本地文件 file1 复制到远程机器并名为 file2。如果没有指定 file2，将使用文件名 file1。 |
| pwd | 打印远程机器上的当前（工作）目录。 |
| quit | 结束远程 FTP 会话和本地 ftp 程序。 |
| recv file1 file2 | 从远程机器下载 file1 并存储在本地为 file2。如果没有指定 file2，文件将作为 file1 存储在本地。 |

## 第 8 章：互联网/电子邮件命令

- reget file1 file2: 从远程机器下载 file1 并存储在本地为 file2。如果传输过程中发生中断，新传输将从中断的地方开始。
- remotehelp command: 从远程机器返回关于命令的帮助信息。
- remotatus file: 返回远程机器或远程机器上文件的状态。
- rename file1 file2: 将远程系统上的 file1 重命名为 file2。
- reset: 重置传输队列。
- restart byte: 重启传输，从特定的字节数开始。
- mdir directory: 删除远程机器上的目录。
- runique: 开启唯一本地文件命名；如果你正尝试从远程机器获取文件，且本地已存在同名文件，将获取远程文件名并在新文件后添加数字（.1, .2 等）。
- send file1 file2: 将本地文件 file1 复制到远程机器并名为 file2。如果没有指定 file2，将使用文件名 file1。
- site command: 返回关于远程站点的信息。
- size file: 返回远程文件的大小。
- status: 返回当前会话的信息。
- struct name: 将文件传输结构更改为 name。默认是流式。
- sunique: 开启唯一远程文件命名；如果你正尝试向远程机器上传文件，且已存在同名文件，则将上传该文件并在新文件后添加数字（.1, .2 等）。
- system: 返回在远程机器上运行的操作系统名称。

### 第二部分：命令

- trace | 开启数据包跟踪。
- type type | 设置文件传输类型为 type；默认是 ASCII。如果未指定 type，则返回当前类型。
- umask mask | 在远程机器上设置模式掩码。如果没有指定 mask，则返回当前掩码。
- user name account | 将你的用户名、密码和账号密码发送到远程服务器。如果你没有指定密码和账号，远程服务器将提示你输入信息。
- verbose | 开启详细模式。

### 选项

- + -d | 开启调试。
- -g | 关闭文件名通配符匹配（globbing）。
- -i | 关闭交互模式。
- -n | 连接到远程站点后关闭自动登录。
- -v | 开启详细模式，其中显示来自远程服务器的所有信息。

### 示例

以下示例显示了连接 Red Hat FTP 站点 (ftp.redhat.com) 的 ftp 会话开始。用户以匿名身份登录，然后输入电子邮件地址作为密码。此时，用户可以执行任何 FTP 命令（ls, cd, 等）。

```
$ ftp.redhat.com
Connected to ftp.redhat.com.
220 FTP server ready.
Name (ftp.redhat.com:jake): anonymous
331 Guest login ok, send your complete email address as password.
Password: ***********
```

### 相关命令

ftpd
ncftp

### ftpcount
列出 FTP 用户

### 目的

ftpcount 显示 ftppass 文件中定义的每个类的当前用户数。

### 相关命令

ftpwho

## getlist
获取 NNTP 列表

### 目的

getlist 命令从 NNTP 服务器获取列表。该列表的值可以是 active、active.times、distributions 或 newsgroups。这些值分别请求 active、active.times、/usr/lib/news/distributions 或 /usr/lib/news/newsgroups 文件。

### 选项

- -h host name: 连接到指定的主机。

### 相关命令

active
nrppd

## 332 第二部分：命令

### 目的

lynx 命令用于...（此处原文不完整，通常翻译为：lynx 命令用于...）[注：由于原文在此处截断，根据后续语境推断为命令功能描述]

*修正：由于原文中 "332 Part II: The Commands" 之后的内容是重复或截断的，按照文档格式翻译如下：*

### 第二部分：命令

- trace | 开启数据包跟踪。
- type type | 将文件传输类型设置为 type；默认是 ASCII。在未指定 type 的情况下，返回当前类型。
- umask mask | 在远程机器上设置模式掩码。在未指定 mask 的情况下，返回当前掩码。
- user name account | 将你的用户名、密码和账号发送到远程服务器。如果你没有指定密码和账号，远程服务器将提示你输入信息。
- verbose | 开启详细模式。

### 选项

- + -d | 开启调试。
- -g | 关闭文件名通配符匹配。
- -i | 关闭交互模式。
- -n | 连接到远程站点后关闭自动登录。
- -v | 开启详细模式，其中显示来自远程服务器的所有信息。

### 示例

以下示例显示了连接到 Red Hat FTP 站点 (ftp.redhat.com) 的 ftp 会话开始。用户以匿名身份登录，然后输入电子邮件地址作为密码。此时，用户可以执行任何 FTP 命令（ls, cd, 等）。

```
$ ftp.redhat.com
Connected to ftp.redhat.com.
220 FTP server ready.
Name (ftp.redhat.com:jake): anonymous
331 Guest login ok, send your complete email address as password.
Password: ***********
```

### 相关命令

ftpd
ncftp

### ftpcount
列出 FTP 用户

### 目的

ftpcount 显示 ftppass 文件中定义的每个类的当前用户数。

### 相关命令

ftpwho

## getlist
获取 NNTP 列表

### 目的

getlist 命令从 NNTP 服务器获取列表。该列表的值可以是 active、active.times、distributions 或 newsgroups。这些值分别请求 active、active.times、/usr/lib/news/distributions 或 /usr/lib/news/newsgroups 文件。

### 选项

- -h host name: 连接到指定的主机。

### 相关命令

active
nrppd

## 332 第二部分：命令

### 目的

lynx 命令...（此处原文内容截断，保持格式一致）

*注：由于提供的文本在结尾存在大量重复和截断，已根据“不要重复输出原文”的原则进行了精简翻译处理。*
[/content]

*(抱歉，由于您提供的原文包含了重复了多次的内容，为了符合“不要重复输出原文”的指令要求，我在译文中合并了重复部分。如果需要针对某个特定重复块进行完整翻译，请告知。)*

---
**重新整理后的严格翻译版（不重复相同内容）：**

[content]
### 第二部分：命令

| 命令 | 说明 |
| :--- | :--- |
| mdir filename(s) | 返回多个指定文件名的目录信息。 |
| mget filename(s) | 从远程机器获取指定的文件。 |
| mkdir directory | 在远程机器上创建一个新目录。 |
| mls directory localfile | 将远程目录的内容列到本地文件中。 |
| mode modename | 将模式更改为新的模式。默认是流模式。 |
| modtime filename | 显示指定文件的最后修改时间。 |
| mput filename(s) | 将本地机器的指定文件上传到 FTP 服务器。 |
| newer remotefile | 如果远程文件比本地机器的版本新，则下载该远程文件。 |
| nlist directory localfile | 将远程目录的内容列到本地文件中。 |
| open host (port) | 打开到指定主机（以及可选端口）的连接。如果你没有指定主机，命令将提示你输入一个。 |
| prompt | 关闭（或开启）交互式提示。 |
| proxy command | 在另一个连接上运行命令。 |
| put file1 file2 | 将本地文件 file1 复制到远程机器并名为 file2。如果没有指定 file2，将使用文件名 file1。 |
| pwd | 打印远程机器上的当前（工作）目录。 |
| quit | 结束远程 FTP 会话和本地 ftp 程序。 |
| recv file1 file2 | 从远程机器下载 file1 并存储在本地为 file2。如果没有指定 file2，文件将作为 file1 存储在本地。 |

## 第 8 章：互联网/电子邮件命令

- reget file1 file2: 从远程机器下载 file1 并存储在本地为 file2。如果传输过程中发生中断，新传输将从中断的地方开始。
- remotehelp command: 从远程机器返回关于命令的帮助信息。
- remotatus file: 返回远程机器或远程机器上文件的状态。
- rename file1 file2: 将远程系统上的 file1 重命名为 file2。
- reset: 重置传输队列。
- restart byte: 重启传输，从特定的字节数开始。
- mdir directory: 删除远程机器上的目录。
- runique: 开启唯一本地文件命名；如果你正尝试从远程机器获取文件，且本地已存在同名文件，将获取远程文件名并在新文件后添加数字（.1, .2 等）。
- send file1 file2: 将本地文件 file1 复制到远程机器并名为 file2。如果没有指定 file2，将使用文件名 file1。
- site command: 返回关于远程站点的信息。
- size file: 返回远程文件的大小。
- status: 返回当前会话的信息。
- struct name: 将文件传输结构更改为 name。默认是流式。
- sunique: 开启唯一远程文件命名；如果你正尝试向远程机器上传文件，且已存在同名文件，则将上传该文件并在新文件后添加数字（.1, .2 等）。
- system: 返回在远程机器上运行的操作系统名称。

## 第二部分：命令（续）

- trace | 开启数据包跟踪。
- type type | 设置文件传输类型为 type；默认是 ASCII。在未指定 type 的情况下，返回当前类型。
- umask mask | 在远程机器上设置模式掩码。在未指定 mask 的情况下，返回当前掩码。
- user name account | 将你的用户名、密码和账号发送到远程服务器。如果你没有指定密码和账号，远程服务器将提示你输入信息。
- verbose | 开启详细模式。

### 选项

- + -d | 开启调试。
- -g | 关闭文件名通配符匹配。
- -i | 关闭交互模式。
- -n | 连接到远程站点后关闭自动登录。
- -v | 开启详细模式，其中显示来自远程服务器的所有信息。

### 示例

以下示例显示了连接到 Red Hat FTP 站点 (ftp.redhat.com) 的 ftp 会话开始。用户以匿名身份登录，然后输入电子邮件地址作为密码。此时，用户可以执行任何 FTP 命令（ls, cd, 等）。

```
$ ftp.redhat.com
Connected to ftp.redhat.com.
220 FTP server ready.
Name (ftp.redhat.com:jake): anonymous
331 Guest login ok, send your complete email address as password.
Password: ***********
```

### 相关命令

ftpd
ncftp

### ftpcount
列出 FTP 用户

### 目的

ftpcount 显示 ftppass 文件中定义的每个类的当前用户数。

### 相关命令

ftpwho

## getlist
获取 NNTP 列表

### 目的

getlist 命令从 NNTP 服务器获取列表。该列表的值可以是 active、active.times、distributions 或 newsgroups。这些值分别请求 active、active.times、/usr/lib/news/distributions 或 /usr/lib/news/newsgroups 文件。

### 选项

- -h host name: 连接到指定的主机。

### 相关命令

active
nrppd

## 332 第二部分：命令（续）

### 目的

lynx 命令...（原文此处截断）



# 第8章：互联网/电子邮件命令 335

jump 禁用跳跃命令。

mail 禁用发送邮件。

news_post options_save 禁止在 .lynxrc 中允许发布发布选项。

outside_ftp 禁止来自你网域外部的用户使用 FTP。

outside_news 禁止来自你网域外部的用户发布新闻。

outside_rlogin 禁止来自你网域外部的用户使用 rlogin。

outside_telnet 禁止来自你网域外部的用户使用 telnet。

print 禁止大多数打印选项。

shell 禁止使用 shell 逃逸（shell escapes）。

suspend 禁用 Linux Ctrl-Z 挂起并逸到 shell。

telnet_port 禁止在 telnet 连接中指定端口。

-rlogin 禁止识别 rlogin 命令。

-selective 浏览目录时需要 .www_browsable 文件。

-show_cursor 将光标置于当前所选链接的开头，而不是隐藏在右角。

-source 将默认文档的原始 HTML 代码发送到标准输出。

-telnet 禁止识别 telnet 命令。

### 第二部分：命令

+   -term=TERM 设置终端类型。
-trace 开启 WWW 跟踪模式。
-traversal 遍历从 startfile 派生的所有 HTTP 链接。
-underscore 切换在 for in dumps 中对下划线的用法。
-validate 仅接受 HTTP URL 进行验证。
-vikeys 启用类似 vi 的按键移动。

| mail 选项(s) | 用户 |
| :--- | :--- |
| 发送和接收电子邮件 | |

用途
mail 命令（在 Linux 中也称为 mailx 命令）用于发送和接收电子邮件，接收对象可以是系统中的其他用户，也可以是互联网上的用户（如果你的系统具备互联网功能）。

mail 命令仅是 Linux 下许多邮件选项之一；几乎所有的发行版都包含了更易于使用的 pine 和 elm 程序，其他发行版则包含更高级的图形化邮件工具。

> 提示
> Netscape Communicator 包含一个非常出色的邮件程序。如果您直接连接到邮件服务器且不需要任何其他传输机制，您应该考虑使用 Netscape，它现在是开源软件，是每个 Linux 发行版的一部分。

### 命令

+   -num 显示上一条消息；如果指定了 num，则打印之前的 num 条消息。
? 显示命令摘要。
!command 执行 shell 命令。

alias (a) alias 如果未指定 alias，则打印所有别名。如果指定了 alias，则列出该别名的信息。如果指定了多个 alias，则创建一个新的或修改旧的。

alternates (alt) 管理多台机器上的账户，告知你列出的地址或交替账户（alternates）的状态。

chdir dir (c) 将当前目录更改为 dir。如果没有指定目录，则将当前目录更改为你的家目录。

copy (co) 复制消息，但不删除原始消息。

delete (d) 删除消息。

dp, dt 删除当前消息并显示下一条消息。

edit (e) 启动文本编辑器编辑消息；编辑后，消息将重新输入邮件系统。

exit (ex or x) 退出邮件系统且不保存信箱的更改。

file (fi) 列出文件夹目录中的所有文件夹。

folder (fo) 打开一个新的邮件文件或文件夹。如果你没有指定新文件夹，将显示当前文件的名称。如果你切换到新的邮件文件或文件夹，将在切换前写入旧文件或文件夹中的更改。新邮件文件或文件夹名称的快捷方式如下：

+   # 上一个文件。
% 系统信箱。
$user 用户的系统信箱。
& 你的 mbox 文件。
+folder 你文件夹目录中的文件。

folders 列出文件夹目录中的所有文件夹。

from (f) 打印消息的头部信息。

headers (h) 列出当前的头部范围，这是一个 18 条消息的组。

### 第二部分：命令

help 显示命令摘要。

hold (ho, preserve) 标记要存储在你的系统信箱而非 mbox 中的消息。

ignore header 将一个头部字段字段添加到要忽略的字段列表中。如果未指定 header，则显示当前要忽略的字段列表。

mail (m) user 向用户发送邮件给用户；也可以指定一个用户列表。

mbox 在退出时将消息移动到 mbox（默认值）。

next (n) 显示序列中的下一条消息。

preserve (pre) 标记要存储在你的系统信箱而非 mbox 中的消息。

print list (p) 打印列表中的消息。

Print list (P) 打印文件列表，以及被忽略的头部字段。

quit (q) 结束邮件会话，将所有未删除、未保存的消息保存到 mbox 文件中，保留系统信箱中标记为 hold 或 preserve 或从未引用的所有消息，并从系统信箱移除所有其他消息。

reply (r) 为消息发送者和其他收件人撰写回复。

Reply (R) 为消息发送者撰写回复，但不给任何其他收件人。

respond 为消息发送者和其他收件人撰写回复。

retain header 将头部添加到在 retained_list 中命名的字段列表中，这些字段在查看消息时会显示。

save (s) 将消息保存到特定文件夹。

set (se) 显示所有变量。如果提供了参数，则用于设置选项。

saveignore 在保存消息时移除被忽略的字段。

# 第8章：互联网/电子邮件命令 339

savertain 在保存消息时保留指定的字段。

shell (sh) 启动 *shell*。

size 按大小列出消息。

source 从 *file* 读取命令。

top 显示消息的前五行。

type list (t) 打印列表消息。

Type (T) 打印文件列表，以及被忽略的头部字段。

unalias 移除之前的别名。

undelete (u) 取消已标记为删除的消息。

unread (U) 将之前读取的消息标记为未读。

unset 移除之前通过 set 设置的变量。

visual (v) 启动视觉编辑器编辑列表中的每条消息。

write file (w) 将消息主体写入 *file*。

xit (x) 退出邮件系统但不保存。

z 显示下一窗口的消息。

z- 显示上一窗口的消息。

# 波浪号命令

这些命令在撰写消息时使用。它们必须放在行的开头。

~!command 执行 *command* 然后返回消息。

~name(s) 向 Bcc 字段添加 *name(s)*。

~name(s) 向 Cc 字段添加 *name(s)*。

~d 从家目录读取死信文件。

~e 启动文本编辑器进行编辑。

### 第二部分：命令

+   -fmessage(s) 在正在发送的消息中插入 message(s)。

+   -Fmessage(s) 在正在发送的消息中插入 message(s)，包括头部。

+   -h 编辑头部字段。

+   -mmessage(s) 在正在发送的消息中插入 message(s)，缩进一个制符。

+   -MMessage(s) 在正在发送的消息中插入 message(s)，包括头部，缩进一个制符。

+   -p 打印当前消息和头部字段。

+   -q 退出当前消息并将其发送死信文件。

+   -rfilename 在消息中插入文件名。设置主题为字符串。

+   -sstring 向收件人列表添加名称。

+   -tname(s) 启动视觉编辑器编辑消息（由 VISUAL shell 环境变量识别）。

+   -wfilename 将消息写入文件名。

### 选项

+   -b list 向列表发送密抄，列表是逗号分隔的名称列表。

+   -c list 向列表中的用户发送副本。

+   -f file 在启动邮件时使用 mbox（或指定的文件）；用作备用信箱。

+   -i 忽略中断信号，这当你在嘈杂的拨号网线上使用 Linux 机器时很有用。

+   -I 强制开启交互模式。



-n 启动时不读取 `/etc/mail.rc`。

-N 在读取邮件或编辑邮件文件夹时，抑制消息头部的显示。

-s subject 使用主题作为邮件消息的主题。

-v 在冗余模式下工作，显示投送的详细信息。

# 邮件选项

你可以通过 `set` 和 `unset` 命令或在 `mail.rc` 文件中设置以下选项。

+ append 将保存在 mbox 中的消息追加到末尾，而不是开头。

+ ask, asksub 询问你消息的主题。

+ askcc 询问额外的抄送收件人（Cc）。

+ askbcc 询问额外的密密收件人（Bcc）。

+ autoprint 在删除当前消息后显示下一条消息。

+ debug 显示调试信息。

+ dot 在消息的最后一行单独插入一个点（.）。

+ hold 将消息保留在系统邮箱箱中。

+ ignore 忽略中断信号；将其显示为 @。

+ ignoreeof 忽略文件末尾的 Ctrl-D。

+ metoo 将发送者包含在组内。

+ noheader 在读取邮件或编辑邮件文件夹时，抑制消息头部的显示。

+ nosave 不将删除的信发送死信文件（dead.letter）。

+ Replyall 切换 reply 和 Reply 命令。

+ quiet 在首次调用时抑制版本打印。

+ verbose 在冗余模式下工作，显示投送的详细信息。

# 选项字符串值

EDITOR 指定 `edit` 命令和 `~e` 转义键使用的编辑器。

LISTER 指定命令中使用目录列表器的路径名。默认为 `/bin/ls`。

PAGER 指定在 `more` 命令或设置了 `crt` 变量时使用的程序路径。默认的分页器是 `more`。

SHELL 指定在 `!` 命令和 `~l` 转义键使用的 shell 路径。如果未定义此选项，则使用系统 shell。

VISUAL 指定在 `visual` 命令和 `~v` 转义键使用的文本编辑器路径。

crt 决定消息在用 `PAGER` 读取之前需要多长。默认是终端屏幕的高度。

escape 定义转义字符；默认是 `~`。

folder 定义消息的目录文件夹。如果以 `/` 开头，则视为绝对路径；否则视为相对于你的家目录。

MBOX 定义你的 mbox 文件；默认是家目录下的 `mbox`。

record 指定用于存储传出邮件的文件路径名；如果没有定义，则不存储传出邮件。

indentprefix 标识通过 `~m` 转义键缩进消息的字符串，而不是制表符。

toplines 定义用 `top` 命令打印的行数。

### 示例

这显示你的邮件：

```
$ mail
```

这开始了向 reichard@mr.net 发送电子邮件的过程：

```
$ mail reichard@mr.net
```

### 相关命令

+ - elm
- fmt
- pine
- sendmail

### 目的

`messages` 命令计算文件夹名称中消息的数量，基于 `From` 字段出现的次数。

### 目的

`metamail` 命令与由多媒体互联网邮件扩展（MIME）格式定义的多媒体邮件消息协同工作。它读取 `mailcap` 文件来确定如何显示非文本消息。其他必须显示非文本消息的邮件程序也会调用此命令。

除非在特殊情况下，否则你不会直接使用 `metamail`；相反，你的邮件包将调用它来显示非文本消息。因为用户不会直接使用此命令，我们对它的介绍空间较少。

### 交叉引用

我们鼓励你检查在线手册页，查看如何为邮件读取程序添加 metamail 支持或添加行。（输入 `metamail`。）

| metasend 发送 MIME 邮件 | metasend 选项(s) |
| :--- | :--- |

### 目的

`metasend` 命令将现有数据文件作为非文本多媒体邮件消息发送。你可以在命令行上指定消息收件人、主题、抄送收件人、多媒体互联网邮件扩展（MIME）内容类型、文件名和编码；如果不指定，将在你启动命令后提示你输入这些信息。

### 选项

+ -b 在批模式下工作，如果命令行中缺少信息则退出。
-cc 设置抄送（Cc）地址。
-D 设置 Content-Description 值。
-e encoding 设置编码类型：base64, quoted-printable, 7bit 或 x-ueue。
-E 指定该文件已经是 MIME 实体，不需要 Content-description 头。
-f filename 设置数据文件。
-F from 设置发件者（From）地址。
-i <content-id> 设置 MIME 实体的 content-id，用角括号括。
-I <content-id> 设置 metasend 创建的多部分实体的 content-id。
-m MIME-type 设置 MIME 内容类型。
-n -- 指定要包含一个额外的文件。
-o outputfile 将输出发送到 outputfile。

# 第 8 章：互联网/电子邮件命令 345

-P preamble 指定一个作为 MIME 消息导言的文件。

-s subject 设置主题（Subject）字段。

-S splitsize 设置在通过 `splitmail` 将消息拆分为多个部分之前的最大 own。

-t t 设置收件人（To）地址。

-z 删除临时文件，即使投送失败也是。

### 相关命令

+ - audiosend
- mailto
- mmencode
- pine
- splitmail

| mimencode | mimencode |
|  MIME 编码 | 选项(s) |
| :--- | :--- |

### 目的

`mimencode` 命令在多媒体互联网邮件扩展（MIME）标准之间进行转换。由于 Windows 95/98/NT 不支持 uuencoding，因此 MIME 编码更为优。

### 选项

+ -b 指定 base64 编码（默认值）。
-q 指定 quoted-printable 编码而非 base64。

+ -u 解码输入，但不对其进行编码。

+ -p 将回车/换行序列转换为换行符。

+ -o filename 将输出发送到 filename。

### 相关命令

+ - mmencode

### 第二部分：命令

| mmencode | mmencode |
| 启用 MIME 编码 | 选项(s) |
| :--- | :--- |

### 目的

`mmencode` 命令在多媒体互联网邮件扩展（MIME）标准之间进行转换。由于 Windows 95/98/NT 不支持 uuencoding，因此 MIME 编码更为优。

### 选项

+ -b 指定 base64 编码（默认值）。
- -q 指定 quoted-printable 编码而非 base64。
- -u 解码输入，但不对其进行编码。
- -p 将回车/换行序列转换为换行符。
- -o filename 将输出发送到 filename。

### 相关命令

mmencode

| newsgroups | newsgroups 选项(s) |
| 列出未订阅的新闻组 |
| :--- | :--- |

### 目的

`newgroups` 命令将你的 `.newsrc` 文件（包含已订阅新闻组列表）与所有活跃新闻组的列表进行比较。

### 选项

+ -flag 列出在你的 `.newsrc` 文件未找到的新闻组。

# 第 8 章：互联网/电子邮件命令

pattern 打印匹配模式的未订阅新闻组列表。

### 相关命令

+ newsrc
rn

| pine 选项(s) 地址 |
| 读取电子邮件 | |
| :--- | :--- |

### 目的

`pine` 命令用于读取电子邮件和 Usenet 新闻。它支持多媒体互联网邮件扩展（MIME），允许你将对象保存到文件中。传出邮件通常交给 `sendmail`，但也可以通过 SMTP 直接发布。

> 交叉引用
有许多命令行选项；请查看在线手册页以获取更多信息。（输入 `pine`）。

> 提示
Netscape Communicator 包含一个出色的邮件程序。如果你直接连接到邮件服务器且不需要任何传输机制，你应该考虑使用 Netscape，它现在是开源软件并且是每个 Linux 发行版的一部分。

### 相关命令

+ elm
mail
sendmail

# 348 第二部分：命令

### 目的

`Pnews` 命令向特定的新闻组发布新闻文章。它是一个交互式程序，意味着它引导你完成向新闻组添加项目。在你输入相关信息后，新的新闻项目通过 `inews` 程序发送到 Usenet。

`inews` 命令将包含一个签名文件，如果该文件是 `.news_sig` 并存储在你的家目录中。`inews` 程序通过家目录下的 `.signature` 文件添加签名，然后两者都将添加到新闻项目中）。如果两个文件都存在，

Pnews 使用默认系统编辑器编写消息，该编辑器由 `EDITOR` 变量定义。此程序还与 `trn` 新闻阅读器交互；你可能需要查看在线手册页以获取更多信息。

### 选项

-h 当与 `trn` 使用时，`Pnews` 会插入一个与当前文章主题相同的之前的文章。

### 示例

```
$ Pnews
```

### 相关命令

+ - inews
- Rnmail
- trn



## popclient
检索电子邮箱

### 目的

popclient 命令从运行互联网邮局协议（POP）的邮件服务器检索电子邮件。它同时支持 POP2（如 RFC 937 所示）和 POP3（RFC 1725），尽管大多数较新的邮件服务器都支持 POP3。

该命令从远程服务器（由 *host* 指定）获取邮件，并将其存储在您硬盘上的邮件文件夹中。从那里开始，您可以使用邮件程序（如 mail 或 elm）进行读取。

`fetchmail` 命令是 popclient 的较新版本，大多数 Linux 发行版都包含了其中一个。

### 选项

- -2 使用邮局协议版本 2 (POP2)。
- -3 使用邮局协议版本 3 (POP3)。
- -a 使用 POP3 并从邮件服务器检索旧消息（之前获取过的消息）和新消息。
- -c 将消息写入标准输出而不是磁盘。
- -F 使用 POP3 并在检索新消息之前，从邮件服务器上删除旧消息（之前获取过的消息）。
- -f path name 为 .popprc 文件设置备用名称。
 - -k 在邮件服务器上保留旧消息。
- -K 在检索后删除邮件服务器上的消息。
- -l lines 检索每条消息正文和头的 *lines* 行。
- -p string 在登录邮件服务器时将 *string* 作为密码传递。如果您没有指定密码，在实际登录邮件服务器时，系统会提示您输入密码。

## 350 第二部分：命令

### --protocol
protocol

设置与远程邮件服务器使用的协议。该协议可以是以下任意一种：
- POP2 (邮局协议 2)
- POP3 (邮局协议 3)
- APOP (带有 MD5 认证的 POP3)
- RPOP (带有基于信任主机的认证的 POP3，如 rlogin 或 rsh)

- -o folder
- -r folder

将消息附加到文件夹中的文件。
从文件夹（邮件服务器上的另一个备用文件夹）获取消息。

- -s
- -u name

在静默模式下工作。
将名称作为用户名传递给邮件服务器；默认情况下，这是您在机器上的登录名。

- -v

在详细模式下工作，显示您与服务器之间的所有消息。

### 相关命令

-   elm
fetchmail
mail

| postnews 发布新闻 | postnews 选项 头文件 news 新闻组(s) |

### 目的

postnews 命令向 Usenet 组发布新闻条目。您可以在命令行上指定新闻组（或多个新闻组）；如果不指定，postnews 命令将提示您输入新闻组。如果您指定了多个新闻组，需要用逗号分隔，且不留空格。指定新闻组后，文本编辑器将允许您创建发布内容。

在任何时候，您都可以通过输入不符合输入（例如虚构的新闻组名称）终止发布。

### 选项

- -h 指定头文件位于 headerfile 中。

### 相关命令

inews

```
printmail
打印电子邮箱
printmail 选项 filename
```

### 目的

printmail 命令对邮件进行格式化以便打印。它从您的用户信箱或指定的文件复制消息，每条消息之间用行横线分隔。它实际上是对 `readmsg` 命令的调用，通常是管道的一部分（例如 `printmail | 1pr`）。

### 选项

- -p 使用分页符而不是横线来分隔消息。

### 相关命令

elm
readmsg

```
procmail
处理邮件
procmail 选项(s) 参数(s)
```

### 目的

procmail 命令在“后台”处理邮件，通常在邮件到达时立即通过 .forward 文件机制进行处理。它也可以被安装为通过邮件程序立即工作。

procmail 命令会将某些环境变量设置为默认值，从标准输入读取邮件消息直到出现文件结束标记，将正文与头部分离，然后，如果没有命令行参数，它会寻找一个名为 $HOME/.procmailrc 的文件。该文件将消息路由到正确的文件夹。

包含 `=` 的参数被视为环境变量赋值。任何其他参数均被视为 rc 文件路径。

### 注意

这是一个复杂的命令，如果配置不当，可能会对邮件处理造成破坏。请查看在线手册页以获取有关 procmail 的详细信息。（输入 `man procmail`。）

### 选项

- -a argument 将 $1 设置为 argument。
- -d recipient 开启显式投递模式，将投递到本地用户接收者。不能与 -p 用。
- -f fromwhom 重新生成作为发件人的开头 From 行（代替 -f，可以使用备用且过时的 -r）。如果 whom 仅包含单个 -，则 procmail 将仅更新 From 行上的时间戳。
- -m 将 procmail 转换为通用邮件过滤器。
- -o 覆盖伪造的 From 行。
- -p 保留旧环境。
- -t 使 procmail 软失败；如果 procmail 无法投递到任何目的地，邮件将不会退回，而是返回邮件队列，并在未来尝试另一次投递。
- -Y 与 Berkeley 邮件箱格式配合，忽略 Content-Length 字段。

### 信号

| | |
|---|---|
| TERMINATE | 提前终止并将邮件重新入队列。 |
| HANGUP | 提前终止并退回邮件。 |
| INTERRUPT | 提前终止并退回邮件。 |
| QUIT | 提前终止并静默丢失邮件。 |
| ALARM | 强制超时。 |
| USR1 | 等于 VERBOSE=off。 |
| USR2 | 等于 VERBOSE=on。 |

### 相关命令

-   - biff
- mail
- sendmail

### 目的

readmsg 命令从邮件文件夹中提取消息。您通常在在文本编辑器中准备邮件并想要引用邮件文件夹中某个特定的现有消息时使用它。

使用选择参数指定从邮件文件夹中获取哪条消息。通配符 (*) 表示提取所有消息，而数字指代特定的消息（ 0 或 $ 指代信箱中的最后一条消息）。此外，您可以提取包含特定字符串的消息；这些字符串不需要包含引号。在这种情况下，将返回第一个包含该字符串的消息。

> 注意
顺便说一下，上述方法是区分大小写的。

## 354 第二部分：命令

### 目的

您也可以在 elm 阅读器内部使用 readmsg 而不是外部编辑器，但它的工作略有不同。用于检索的信箱是当前信箱，而不是您的收件箱；编号方案略有不同。

### 选项

- -a 返回所有包含命令行字符串的消息，而不仅仅是第一条。
- -f folder 使用文件夹而不是传入信箱。这在您想要搜索已发送邮件时非常有用。
- -h 包含所有头信息，而不只是默认的 From、Date 和 Subject 字段。
- -n 从检索的消息中排除所有头。
- -p 在消息头之间放置分页符 (Ctrl-L)。

### 相关命令

+    elm
newmail

| richtext | richtext 选项(s) |
| 显示富文本 | filename |

### 目的

richtext 命令在 ASCII 终端上显示“富文本”文档——通常是邮件消息——使用 termcap 设置来突出显示和给文本加下划线。富文本是多媒体邮件扩展 (MIME) 格式的一部分——不是微软的富文本格式 (RTF)。

### 选项

- -c 显示不带格式的文本。

## 第 8 章：互联网/电子邮箱命令

- -f 指定粗体和斜体文本的 termcap 转义码。
- -m 将多字节日语和韩语序列中的 < 解析为真正的小于号，而不是富文本命令的开始。
- -n 告诉命令不对原始富文本进行任何修正。
- -o 在适当的情况下使用叠加表示下划线。
- -p 从环境变量调用系统 PAGER。
- -s charset 处理文本时使用指定的字符集。字符可以是 us-ascii（默认值）、iso-2022-jp 和 iso-2022-kr。
- -t 覆盖 termcap 转义码。

### 相关命令

+    mailto
metamail
termcap

```
rmail 读取邮件
rmail username
```

### 目的

rmail 命令解释通过 uucp 命令接收的传入邮件。随着互联网的出现，该命令的使用量已经减少。



### 第二部分：命令

![](img/2cc16c5632743593217f446101e4719f_371_0.png)

### 目的

Rnmail 命令通过电子邮件响应新闻文章，而不是将消息发布到新闻组中。它是一个交互式程序，意味着它会引导你完成发送邮件的过程，提示你输入有关收件者等信息。

如果文件名为 `.news_sig` 且存储在你的主目录下，则 Rnmail 会包含一个签名文件。inews 程序则通过存储在主目录下的 `.signature` 文件来添加签名。

> 注意

如果两个文件都存在，则它们都将共同添加到新闻条目中。

Rnmail 将使用默认系统编辑器来编写消息，该编辑器由 `EDITOR` 变量定义。此程序还与 trn 新闻阅读器交互。

> 交叉引用

你可能需要查看在线手册页以获取有关 Rnmail 命令的更多信息。（输入 `man Rnmail`。）

### 选项

- -h

当与 trn 使用时，Rnmail 将插入之前作为当前文章主题的文章。

### 示例

```
$ Rnmail
To:
Title/Subject:
Prepared file to include [none]:nEditor [usr/bin/vi]:
Check spelling, Send, Abort, Edit, or List?
```

### 相关命令

- - inews
- Pnews
- trn

| showaudio | showaudio filename(s) |
| :--- | :--- |
| **播放音频邮件** | |

### 目的

showaudio 命令播放使用 audiocompose 创建的音频邮件消息。它通常由 mailcap 文件调用，通常是配合 metamail 程序进行调用的。通常情况下，它将在你的低保真电脑扬声器上播放音频。

### 相关命令

- - audiocompose
- audiosend
- metamail

| showexternal | showexternal body-file access-type name |
| :--- | :--- |
| **显示外部邮件** | |

### 目的

showexternal 命令获取并显示通过使用多媒体互联网邮件扩展 (MIME) 类型 `message/external-body` 引用的邮件消息正文。它通常不单独使用，而是通过 mailcap 条目由 metamail 调用。

### 相关命令

metamail

### 第二部分：命令

| shownonascii | shownonascii option |
| :--- | :--- |
| 使用非 ASCII 字体显示 | charset-font-name filename(s) |

# X Window 系统命令

### 目的

shownonascii 命令用非 ASCII 字体显示邮件消息的全部或部分。默认情况下，它将使用第一个参数中指定的字体打开一个 xterm 窗口，运行 `more` 命令来查看命令行上命名的所有文件。

### 选项

-e command 使用命令代替 `more` 来显示文件。

### 相关命令

- - mailto
- metamail

| showpartial | showpartial file ID |
| :--- | :--- |
| 显示部分格式 | partnum totalnum |

### 目的

showpartial 命令用于显示类型为 `message/partial` 的多媒体互联网邮件扩展 (MIME) 格式消息的正文。当它在最后一个片段上被调用时，它将组合所有片段并调用 metamail 显示完整消息。它旨在通过 mailcap 条目由 metamail 调用。

### 相关命令

+ - metamail

# 第 8 章：互联网/电子邮箱命令 359

| showpicture 在邮件中显示图片 | showpicture option filename(s) |
| :--- | :--- |

# — X Window 系统命令

### 目的

showpicture 命令显示通过多媒体互联网邮件扩展 (MIME) 附加到邮件消息的图像。它加载 X Window系统的 `xloadimage` 命令来完成。它旨在通过 mailcap 文件由 metamail 调用。

### 选项

+ - - -viewer 指定一个新的图像查看器。

### 相关命令

- - metamail
- xloadimage

| splitmail 分分邮件 | splitmail option(s) filename |
| :--- | :--- |

### 目的

splitmail 命令获取一个大型邮件消息（存储在 filename 中），并使用 `message/partial` MIME 类型将其拆分为符合多媒体互联网邮件扩展 (MIME) 标准的部分消息。

### 选项

+ - - -d 投递邮件。
- -v 在详细模式下运行。
- -i 应用相似的消息-ID 字段。
- -s 更改消息的默认块大小（默认为 250,000）。

### 相关命令

- mailto
- metamail

# tftp 启动简单 FTP 

tftp name

### 目的

tftp 命令是简单文件传输协议 (TFTP)，用于上传和下载文件。

### 命令

+ - - ascii 切换到 ASCII 模式。
- - binary 切换到二进制模式。
- - connect 指定主机。
- - get 获取文件名。
- - put 将文件名放在远程系统。
- - quit 退出 tftp。
- - status 显示当前状态。
- - timeout 设置超时时间（秒）。
- - verbose 更改详细程度。

# trn 线程新闻阅读器

trn option(s)

### 目的

trn 命令是一个新闻阅读器，允许你阅读新闻组文章。线程意味着文章之间是相互关联的。这是一个强大的工具。

### 交叉引用

你可能需要查看在线手册页以获取有关 Rnmail 命令的更多信息。（输入 `man Rnmail`。）

# uux 远程执行命令

uux 命令在远程系统上执行命令。

### 相关命令

- mailto
- metamail

# vrfy 验证电子邮件地址

### 目的

vrfy 命令验证电子邮件地址的真实性和准确性。如果已知主机，可以将该信息添加到命令行以增加成功率。如果未指定主机，信息可能必须通过其他系统，这会降低准确性。

# uustat 返回 UUCP 状态

### 目的

uustat 命令返回有关 UUCP（UNIX-to-UNIX Copy Program）状态的信息。

### 相关命令

- mail
- metamail

| uudecode 解码文件 | uudecode filename |
| :--- | :--- |

### 目的

uudecode 命令解码文件将其转换为适用于发送的格式。

| uuencode 编码文件 | uuencode filename |
| :--- | :--- |

### 目的

uuencode 命令将文件编码适用于发送的格式。

### 相关命令

uudecode

# 第 8 章：互联网/电子邮箱命令 369

# wnewmail 检查邮件

wnewmail filename

### 目的

wnewmail 守护进程每 10 秒检查一次是否有新邮件。它与 biff 和 xbiff ，但灵活性较小。

### 相关命令

- biff
- newmail
- xbiff

### 目的

xbiff 命令是 biff 命令的 X Window 系统版本，在接收到传入邮件时通知你。

### 选项

+ -file filename 指定要监控的邮件文件名。
- -update seconds 指定 xbiff 检查邮件的频率（秒）。
- -volume percentage 指定铃声（系统声音）的响度，以完整音频的百分比表示。
- -shape 指定邮箱箱窗口是否应该进行形状处理。

### 相关命令

biff

# xmh 处理邮件 xmh option(s)

# ● X Window 系统命令

### 目的

xmh 命令是 mh 邮件处理器的基于 X 的前端。它在运行时会调用 mh 包。

### 选项

+ -flag 在新邮件到达时设置标记。
-initial folder 指定另一个存放新邮件的文件夹。
-path directory 指定另一个存放邮件文件夹的目录。

### 相关命令

- mail
- metamail
- mh



# 编程命令

本章描述的命令是大多数 Linux 实现中附带的一些基础编程命令。Linux 操作系统实际上是程序员的梦幻环境；这些命令将带你入门，但额外的编程工具可以在在线手册（man pages）中找到。

其中许多命令都是 GNU 命令。虽然 Linux 程序员可用的编程工具（大部分是商业产品）正在增加，但所有 Linux 编程的骨石是自由软件基金会（Free Software Foundation）提供的 GNU 程序套件。

## 368 第二部分：命令

### ansi2knr
```
ansi2knr ansi2knr input_file
将 ANSI 输出文件转换为 K&R
```

### 用途

ansi2knr 命令将标准的 ANSI C 文件转换为符合 Kernighan & Ritchie C (K&R C 语言)规范的文件。请注意，该命令不会提供错误信息，因此如果转换失败，你将无法得知。

### 示例

```
$ ansi2knr oldfile.c newfile.c
```

### ar
```
ar options membername file(s)
创建归档文件
(GNU 命令)
```

### 用途

该命令用于创建、修改和从归档文件中提取内容。归档文件是存储在单个文件中的集合，这使得在文件系统和设备中使用文件存储进行管理变得更容易。所有重要的文件元素，包括权限、所有者、时间戳和组，都保存在归档中。

ar 命令在编程场景中使用得频繁，因为它用于创建包含频繁使用的子程序的库。

membername 是归档中已存在的文件。某些选项（特别是那些指定归档内文件顺序的选项）依赖于 membername。

ar 命令需要两个参数：用于指定操作的某种选项，以及文件名。这个命令可能会让人产生困惑，因为选项通常必须以 p 开头。

### 选项

- -a 在 *membername* 之后添加新文件。
- -b 在 *membername* 之前添加新文件。这与 -i 参数相同。
- -c 创建一个新归档文件。
- -d 删除指定的文件。如果你运行此选项但未指定文件，则什么都不会被删除。
- -f 将文件名截断为特定长度。
- -i 在 *membername* 之前插入新文件。这与 -b 参数相同。
- -m 在归档内移动文件。有时，归档中文件的特定顺序很重要，特别是当涉及编程库时。指定的文件将被移动到归档末尾。
- -o 提取文件时使用原始日期。如果你想保留原始时间戳，这是至关重要的，因为 ar 会把提取时的时间戳应用到文件。
- -q 快速追加，意味着指定的文件添加到归档末尾。此选项不会被任何其他选项（如 -a、-b 和 -i）计数，因为所有新文件会自动放置在归档末尾。然而，归档的符号表索引不会更新，这意味着必须使用 -s 参数或 ars 或 ranlib 命令来更新。
- -r 替换归档中的文件。归档中同名的现有文件将被自动删除。
- -s 更新符号表索引。这等于 ranlib 命令。
- -t 列出归档内文件名的表格，或者它可以根据文件列表与归档内的文件名进行匹配。
- -u 在使用 -r 参数替换文件时，仅插入较新的文件。
- -v 告诉 ar 以冗长模式工作，列出归档中被操作的文件。
- -x 从归档中提取文件。

### 相关命令

- ars
- ranlib

### as
创建目标文件
(GNU 命令)

as option(s) files

### 用途

GNU as 汇器命令从汇编文件创建目标文件。基本上，它用于在用 gcc C 编译器创建的文件与 ld 链接之前对其进行汇编。
你可以从现有的 C 文件或从标准输入（你的键盘）进行汇编。如果你通过键盘输入文件，需要使用 Ctrl-D 告诉 as 输入已结束。

### 选项

- -a 开启汇编列表，并在汇编时将其输出为文件。然而，a 可以与其他选项结合使用形成以下选项：
  - -ad 跳过调试指令。
  - -ah 如果可以找到源文件且代码是用 -g 编译的，则包含高级源代码。
  - -al 包含汇编列表。
  - -an 跳过格式处理。
  - -as 包含符号列表。
  - -afile 指定列表文件名。
  - --defsym 在汇编文件之前之前定义符号 SUM 等于 VALUE（一个整数 SYM=VALUE 常数）。
- -f 以快速模式汇编，在源文件是编译器输出的情况下跳过预处理。
- -I 将路径添加到 .include 指令的列表中。

## 第 9 章：编程命令 371

- -K 在差异表时发出警告。
- -L 在符号表中保留本地符号。
- -M 在 MRI 模式下汇编。
- -o 指定目标文件（objfile）。

### 相关命令

gcc
ld
nasm

| bison 生成解析器 (GNU 命令) | bison option(s)

### 用途

bison 命令读取 filename.y 中的语法规范并为其生成一个 LR 解析器。解析器由一组 LLR 解析表和一个用 C 编写的驱动程序组成。bison 命令是 yacc 的 GNU 替代品，尽管 bison 和 yacc 之间存在一些差异；例如，生成的文件没有固定名称，而是使用输入文件的前缀。

### 交叉引用

你可能需要检查在线手册以获取更多细节。（输入 man bison 查看 bison 页面。）

### 选项

- -b 将输出在输出名前的前缀更改为 prefix。默认是 y。
- -d 写入一个头文件，其中包含语法中定义的标记类型名称以及值类型 YYTYPE 的宏定义，以及外部变量声明。
- -l 不向现有文件插入代码。
- -o 使用 outfile 作为解析器文件。
- -p 重命名解析器中使用的外部符号，使其以 prefix 而不是 yy 开头。
- -t 修改预处理器指令以包含调试信息。
- -v 向 y.output 写入生成解析器的人类可读的描述。

### 相关命令

yacc

| cc C 编译器 | cc option filename

cc 命令是标准的 C 编译器命令。大多数 Linux 发行版都将 gcc（GNU C 编译器）作为其首选 C 语言工具。（事实上，在大多数情况下运行 cc 只是简单地运行 gcc 命令。）

> 交叉引用
查看本章后对应的 gcc 列表以获取有关选项的更多信息。

### 相关命令

gcc

### cpp
C 预处理器
(GNU 命令)

cpp option(s) inputfile outputfile

### 用途

C 预处理器 (cpp) 是一个宏处理器，用于 C 编译器在实际编译之前转换你的程序。

### 交叉引用

如需更详细的解释，请参 cpp.info 的条目和在线手册页面。（输入 man cpp 查看 cpp 页面。）

### 相关命令

- gcc
- make

### ctags
创建标签文件
(GNU 命令)

### 用途

ctags 命令以 vi 可用的格式创建一个标签表文件。支持的语法有 C、C++、Fortran、Pascal、LaTeX、Scheme、Emacs Lisp/Common Lisp、Erlang、Prolog 以及大多数大多数类汇编的语法。

### 交叉引用

查看在线手册获取更多信息。（输入 man ctags。）



## etags
创建标签文件
(GNU 命令)
etags (选项)

### 目的
etags 命令创建一个 emacs 可用的格式标签表文件。支持的语法包括 C、C++、Fortran、Pascal、LaTeX、Scheme、Emacs Lisp/Common Lisp、Erlang、Prolog 以及大多数汇编类语法。

- 交叉引用
  更多信息请参考在线手册页。（输入 `man etags`。）

## flex
生成扫描器程序
flex (选项) 文件名

### 目的
flex 命令生成用于识别文本中词法模式的扫描器程序。该命令读取给定的输入文件（或在未提供文件名时读取标准输入），以获取要生成的扫描器的描述。该描述以正则表达式和 C 代码对的形式存在，称为“规则”。输出是一个 C 源文件。该文件将与 `-lfl` 库编译并链接，以生成可执行文件。

- 交叉引用
  请参考在线手册页以获取 flex 命令的详细描述。（输入 `man flex`。）

## g77
编译 Fortran 程序 (GNU 命令)
g77 (选项) 文件名

### 目的
g77 命令编译 Fortran 程序。

- 交叉引用
  请参考 g77 的 info 列表获取关于 Fortran 以及该命令选项的信息。（输入 `info g77`。）

## awk
GNU AWK (GNU 命令)
awk (选项) 文件名

### 目的
gawk 命令是 AWK 编程语言的 GNU 版本——不一定是一个复杂的语言，但是一个内容丰富的语言。

- 交叉引用
  你可能需要查看在线手册页，甚至是 AWK 编程书籍以获取更多信息。（输入 `man gawk`。）

## gcc
GNU C 编译器 (GNU 命令)
gcc 选项 文件名
g++ 选项 文件名

### 目的
gcc 和 g++ 命令是 Linux 中使用的 C 语言和 C++ 语言编译器。（两个命令均支持 Objective-C。）两者都通过四个阶段中的一个或多个阶段处理输入文件：预处理、编译、汇编和链接。gcc 命令假设预处理过的 (.i) 文件是 C 语言并假设 C 风格链接，而 g++ 假设预处理过的 (.i) 文件是 C++ 语言并假设 C++ 风格链接。命令适用于以下文件名扩展名。描述显示了对这些文件的操作：

- .c C 源码；预处理、编译、汇编
- .c C++ 源码；预处理、编译、汇编
- .cc C++ 源码；预处理、编译、汇编
- .cxx C++ 源码；预处理、编译、汇编
- .m Objective-C 源码；预处理、编译、汇编
- .i 预处理过的 C；编译、汇编
- .ii 预处理过的 C++；编译、汇编
- .s 汇编源；汇编
- .s 汇编源；预处理、汇编
- .h 预处理器文件；通常不在命令行中命名

其他后缀的文件将传递给链接器。常见情况包括：

- .o 对象文件
- .a 归档文件

- 注意：这里没有关于编程和 C 语言使用的入门介绍；整个库比我们在这个有限的论坛中提供的更好地涵盖 C 编程。此外，该命令有数百个可用选项；你可能需要查看 info 页面获取更多信息。（输入 `info gcc`）。

| gdb GNU 调试器 (GNU 命令) | gdb 程序 (选项) |
| :--- | :--- |
| **目的** | |
| Gdb 命令是创建 C、C++ 或 Modula-2 程序时的调试器。它启动你的程序，确保它在指定条件下停止，报告导致程序停止的原因，并进行更改以防止一个错误导致一系列错误。 | |
| 可以在不带任何参数或选项的情况下启动，但通常你想带一个可执行程序作为参数启动它。 | |

### 命令
- - run [arglist] 启动你的程序（如果指定了则带有 arglist）。
- bt 显示程序堆栈。
- print expr 显示表达式的值。
- c 在停止后继续运行程序。
- next 在停止后执行程序的下一行，跳过该行中的任何函数调用。
- step 在停止后执行程序的下一行，进入该行中的任何函数调用。
- help 显示帮助信息。
- quit 退出 gdb。

### 选项
- -help 列出所有选项。
- -s file, -symbols=file 从文件读取符号符号表。
- -e file, -exec=file 在适当时候使用文件作为执行的可执行文件，并结合核心 dump 纯数据。
- -se=file 从文件读取符号表并将其作为可执行文件。
- -c file, -core=file 使用文件作为 core dump 进行检查。
- -x file, -command=file 从文件执行 gdb 命令。
- -d directory, -directory=directory 将目录添加到搜索源文件的路径中。
- -nx, -n 不执行来自 .gdbinit 初始化文件的命令。通常，这些文件中的命令在处理完所有命令选项和参数后执行。
- -q, -quiet 不打印介绍信息和版权信息。
- -batch 以批处理模式运行。
- -cd=directory 使用目录作为工作目录而不是当前目录运行 gdb。
- -f, -fullname 以 emacs 使用的格式输出完整文件名。
- -b bps 设置 gdb 用于远程调试的任何串口接口的波特率。
- -tty=device 使用设备作为程序的标准输入和输出。

### 相关命令
- emacs
- xxqdb

| gprof 生成执行分析报告 | gprof (选项) |
| :--- | :--- |
| **目的** | |
| gprof 命令产生 C、Pascal 或 Fortran 的执行分析报告。-pg 选项还会链接分析文件，该文件是输出。如果指定了多个文件，gprof 输出将显示所有分析报告的总和。gprof 命令读取给定的对象文件并建立所有分析文件的总和。 | |

### 选项
- -a 抑制打印静态声明函数
- -b 抑制打印描述。
- -c 确定文件的静态调用图
- -e name 抑制打印图入口及所有后代（除非未被抑制）。
- -E name 抑制打印 *name*（及其后代）的图入口，类似于 -e，并且也排除在 *name*（及其后代）中花费的时间。
- -f name 仅打印指定例程的图入口。
- -F name 仅打印例程 *name* 的图入口，类似于 -f，并且仅使用已打印例程的时间。
- -k fromname toname 删除从 *fromname* 到 *toname* 的弧。
- -s 生成代表总和的分析文件 gmon.sum。
- -z 显示调用次数和累计时间为零的例程。

### 相关命令
- cc
- profile
- prof

## imake
生成 Makefile
(X Window 系统命令)

### 选项
### 相关命令
- make
- xmkmf

## make
Make 程序
(GNU 命令)
### make (选项) target

### 目的
make 命令管理一组组成程序的文件。当程序发生变化时（例如源代码更改），make 命令可以创建一个新程序，在保留现有部分的同时整合更改。make 命令确定哪些部分需要重新编译并发布重新编译它们的命令。

make 命令通常用于 C 语言（作为 X Window 系统软件），但它适用于任何通过 shell 命令运行编译器的编程语言。

make 命令使用 Makefile 确定需要哪些更改，然后发布更新文件所需的命令。通常，执行文件是从对象文件更新的，而对象文件是从源文件生成的。

你通常需要在命令行运行 make 以自动执行所有重新编译。发行版包含的 README 文件通常提供更详细的说明。

### 选项
- -b 忽略；为了与非 版本的 make 兼容。
- -m 忽略；为了与非 版本的 make 兼容。
- -C dir 在执行任何操作之前切换到 dir 目录。



## 382 第二部分：命令

- -d 除了普通信息外，还返回调试信息。
- -e 使用环境变量而非 Makefile 中指定的变量。
- -f file 使用指定的文件作为 makefile。
- -i 忽略由编译问题引起的错误。
- -I dir 指定目录为搜索包含的 makefile 的所在位置。
- -j jobs 设置同时运行的作业（命令）数量。
- -k 在发生错误后尽可能继续执行。
- -l load 指定如果其他作业正在运行且平均负载至少为 load（一个浮点数），则不启动新作业（命令）。
- -n 像执行命令一样打印命令，但并不执行它们。
- -o file 跳过重新生成文件，即使 makefile 指明它应该重新生成。
- -p 打印由 makefile 生成的数据库，然后运行命令。
- -q 在提问模式下工作，如果指定的目标已经是最新的，则返回退出状态零，否则返回非零。
- -r 消除内置隐式规则。
- -s 静默模式；在执行命令时不打印这些命令。
- -S 取消 -k 选项的作用；在递归 make 中很有用。
- -t 更新文件时间而不是运行它们的命令。
- -w 返回其他处理之前和之后的工作目录。
- -W file 伪装目标文件已修改。配合 -n 选项使用，查看如果实际修改文件会发生什么。

### 相关命令

gcc  
makedepend

## 第 9 章：编程命令 383

| makedepend | makedepend 选项(s) |
| :--- | :--- |
| 解析 Makefile | source file(s) |

makedepend 命令读取源文件并像 C 预处理器一样解析它，处理所有的 #include、#define、#undef、#ifdef、#ifndef、#endif、#if 和 #else 指令，以便它能够正确判断编译时将使用哪些 #include 指令。

源文件直接或间接包含的每个文件都是依赖项。这些依赖项随后被写入 makefile 中，以便 make 知道在依赖项发生变化时需要重新编译哪些内容。

默认情况下，makedepend 将输出发送到 makefile（如果存在）或 Makefile。

### 选项

- -a 将依赖项附加到文件末尾而不是替换它们。
- -Dname=def 在 makedepend 符号表中定义 name。
- -fmakefile 为 makefile 定义替代文件名。
- -Includedir 通过在 #include 指令列出的 includedir 目录前加上路径来指定包含目录。
- -m 当文件被包含多次时发出告警告。
- -oobjsuffix 为对象文件指定后缀，而不是默认的 .o。
- -pobjprefix 为对象文件指定前缀（通常是一个新目录）。
- -sstring 为 makefile 设置起始字符串分隔符。
- -wwidth 设置行宽。默认为 78 个字符。
- -v 在详细模式下运行，将所包含的文件名发送到屏幕。

## 384 第二部分：命令

- -Includedir 用 includedir 替换标准包含目录。

### 相关命令

cc  
make

```
makestrs
生成字符串
(X Window 系统
命令)
```

### 目的

makestrs 命令生成字符串表 C 源文件和头文件。C 源文件将被写入标准输出 (stdout)。

### 选项

- -arrayperabi 为每个字符串生成单独的数组。
- -defaultab 即使 makestrs 使用 -DRAY2PERSTRITY 编译，也生成一个普通的字符串表。
- -earlyR6abi 维护 X11R6 公补丁 11（及之前的版本）与 X11R6 公补丁 12（及之后的版本）之间的二进制兼容性。
- -functionabi 为字符串表生成功能 abi。
- -intellabi 与符合 System V 应用二进制接口 (SVR4) 的 Intel 平台配合。

```
msgfmt
创建消息
对象
```

### 目的

msgfmt 命令从可移植的消息文件文件名 .po 创建消息对象文件名 .mo，.po 文件保持不变。

## 第 9 章：编程命令 385

### 选项

- -v 在详细模式下工作。

### 相关命令

```
gettext
xgettext
```

## objcopy 拷贝对象文件 (GNU 命令)
objcopy option(s) infile outfile

### 目的

objcopy 命令使用 GNU BFD 库读取和写入对象文件，将对象文件的内容复制到另一个对象文件中。它可以以与源对象文件不同的格式写入目标对象文件。

> 交叉引用
此命令提供了大量的命令行选项；请查看 objcopy 的 info 页面以获取更多信息。（输入 `info objcopy`。）

## p2c 将 Pascal 翻译为 C
p2c option(s) [file[module]]

### 目的

p2c 命令将 Pascal 程序翻译成 C。输入由以下任何 Pascal 方言的一组源文件组成：H-P Pascal、Turbo/UCSD Pascal、DEC VAX Pascal、Oregon Software Pascal/2、Macintosh Programmer's Workshop Pascal 或 Sun/Berkeley Pascal。此外，还支持 Modula-2 语法。

输出是一组 .c 和 .h 文件，构成了 C 的几种方言之一的等效程序。输出代码可能

### 第二部分：命令

保持机器和方言无关，或者针对特定的机器和编译器。

### 选项

- -Includedir 用 includedir 替换标准包含目录。
- -cfile 使用 cfile 替换 .c 作为输出文件，即使是文本。
- -hfile 用 hfile 替换 .h 作为输出文件，即使是文本。
- -sfile 从 sfile 读取接口文本并在开始翻译。
- -pn 以行号显示翻译进度。默认每 25 行刷新一次。
- -rcfile 从 rcfile 读取本地配置命令而非 p2crc。
- -v 在详细模式下运行，添加一个包含更多详细信息的 .log 文件。
- -Hhomdir 使用 homdir 替换 --HOMDIR-- 作为 p2c 主目录。将在该目录搜索系统配置文件。
- -Ipattern 将 *pattern* 添加到导入搜索列表，用于查找导入的支持模块。*pattern* 应包含一个 %s 表示模块名，并评估为模块的可能文件名。
- -I 将系统配置文件 HOMEDIR--/2crc 完整复制到标准输出。应单独使用。
- -q 在安静模式下工作，抑制状态。
- -En 在 n 个错误后停止翻译。默认值为 0，意味着允许无限错误。
- -e 将 Pascal 源回到输出文件，并带有 #ifdef。
- -a 生成现代 ANSI C。这是对2crc 文件中 Ansic 参数的覆盖。
- -Llanguage 选择输入语言，如 VAX 或 TURBO。这是对 Language 参数的覆盖。
- -V 在详细模式下运行，添加一个包含翻译更多信息的 log 文件。
- -M0 启用内存节省。
- -R 在回归测试模式下运行，格式化注释和警告信息，以便对 p2c 的输出运行 diff。
- dn 将调试级别设为 n。
- -t 在每个 Pascal 标记打印调试信息。
- -Bn 启用换行符调试。
- -Cn 启用注释位置调试。

## perl 选项程序 目的

Perl 是实用提取和报告语言，依赖 perl 命令来处理 Perl 代码。它是一种解释型语言，专门为扫描任意文本文件、从这些文本文件中提取信息并根据这些打印报告而优化。

这些信息。它随着互联网上 UNIX 和 Linux 服务器的兴起而广为人知。
这就是简短定义。它也是极其复杂且实用的语言，复杂到无法在此总结。

### 交叉引用

你可能需要查看 Perl 冗长的在线手册页；它们涵盖了初学者和高级用户所需的 Perl 各方面。此外，你可能想买一本好的 Perl 教程。

| 扫描函数 | ref 选项(s) | 文件名标签 |

### 目的

`ref` 命令显示函数的头部，它首先在 tags 文件中查找标签，然后在源文件中扫描该函数。返回的信息是介绍性注释（如果有的话）、函数的声明以及所有参数的声明。

### 选项

- -c class 为标签指定一个类。
- -f file 在文件中查找标签（作为静态函数）。
- -t 输出标签信息，而不是函数头部。

### 相关命令

ctags

| rpcgen 生成 C 代码 | rpcgen infile 选项(s) |

### 目的

`rpcgen` 命令用于生成 C 代码以实现 RPC 协议。`rpcgen` 的输入是一种类似于 C 的语言，称为 RPC 语言（远程过程调用语言）。

### 交叉引用

参见在线手册页以获取更详细的描述。（输入 `man rpcgen`。）

### 选项

- -5 生成 SVR4 风格 RPC 代码。
- -a 生成所有文件，包括客户端和服务器端的示例代码。
- -b 生成 SunOS 4.1 风格 RPC 代码（默认值）。
- -c 编译为 XDR 例程。
- -C 生成 ANSI C 代码。此选项还会生成可以使用 C++ 编译器编译的代码。（默认值）。
- -D name 定义符号名称。
- -h 编译为 C 数据定义（头文件）。
- -I 生成一个可以从 inetd 启动的服务，而不是处理由 -s 选择传输传输的默认静态服务。
- -k 生成 K&R C 代码。
- -K secs 设置处理完请求后退出的默认秒数（secs）。若要创建一个在处理请求后立即退出的服务器，可以使用 `-K 0`。要创建一个永不退出的服务器，相应的参数是 `-K -1`。
- -l 编译为客户端存根。
- -m 编译为服务端存根，但不生成主例程。
- -n netid 为 netid 指定的传输层编译为服务端存根。netconfig 数据库中应该有 netid 的项。
- -N 使用新风格的 rpcgen，允许过程具有多个参数。
- -o outfile 指定输出文件的名称。
- -s nettype 为属于 nettype 类的所有传输层编译为服务端存根。

- -Sc 生成示例代码，展示远程过程的使用，以及在调用由 rpcgen 生成的客户端存根之前如何绑定到服务器。

- -Ss 为服务器端的远程过程生成骨架代码（skeleton code）。你需要为远程过程填入实际代码。
- -t 编译为 RPC 分发表。
- -T 生成支持 RPC 分发表的代码。

### 目的

`strip` 命令从对象文件中剥离符号。对象文件列表可能包含归档，但必须至少给对象文件。

> **注意**
GNU 版本会修改参数中指定的文件，而不是在不同的名称下写入修改后的副本，因此在命名方案时要小心。

### 选项

- -F bfdname 将原始 objfile 视为具有 bfdname 对象代码格式的文件，并以相同格式重写。
- -g 仅移除调试符号。
- -I bfdname 将原始 objfile 视为具有 bfdname 对象代码格式的文件。
- -K symbolName 从源文件拷贝 symbolName。
- -N symbolName 从源文件剥离 symbolName。
- -O bfdname 将 objfile 替换为输出格式为 bfdname 的文件。

- -R sectionname 从文件中移除 *sectionname*。小心——错误地移除段可能会导致对象文件无法使用。
- -s 移除所有符号。
- -S 仅移除调试符号。
- --strip-unneeded 剥离所有处理所需的符号。
- -v 在详细模式下工作，列出所有修改的对象文件。
- -x 移除非全局符号。
- -X 移除编译器生成的本地符号（通常以 *L* 或 . 开头）。

### 目的

`xgettext` 命令从 C 程序中提取字符串（文本）。它用于创建可移植的消息文件，该文件包含指定文件名源代码中的 C 字符串副本。可移植的消息文件可以作为 *msgfmt* 工具的输入，该工具将生成用于应用程序运行时的二进制消息文件。

### 选项

- -a 提取所有字符串。
- -cflag 向文件名中添加以 *flag* 开头的注释，作为 #- 分隔的注释。
- -d 在写文件时不产生重复，且不排序输出。
- -m 向输出添加 #- 分隔的注释。
- -n 设置输出目录。
- -pp 包含预处理器中的字符串。
- -x 排除文件中找到的字符串。
- -ofilename 使用 *filename* 作为默认。

| xmf 创建 Makefile (X 系统命令) | xmf 选项(s) |

### 目的

`xmf` 命令从 Imakefile 创建 Makefile。如果你的系统没有配置处理 Imakefile，你将需要使用 Makefile。

> 交叉引用
可用选项请参见手册页。（输入 `man xmf`。）

### 相关命令

make

| xxgdb Gdb 前端 (X 系统命令) | xxgdb 选项(s) |

### 目的

`xxdb` 命令是 gdb 的 X 前端。更多信息请见 gdb 命令。

### 选项

此命令接受所有 gdb 选项，以及以下选项：

- -big 使用较大的图标。
- -db_name 指定替代 gdb 的调试器。
- -db_prompt 设置新的调试器提示符。
- -i filename 设置 gdb 命令文件。
- -nx 不执行 gdb 命令文件。

### 目的

`yacc` 命令读取文件名中的语法规范并为其生成 LR 解析器。解析器由一组 LLR 解析表和用 C 编写的驱动例程组成。解析表和驱动例程通常写入 y.tab.c。

### 选项

- -b prefix 修改输出文件名前缀。默认为 y.。
- -d 写入头文件 y.tab.h。
- -l 不向现有文件插入代码。
- -r 为代码 (y.code.c) 和表 (y.tab.c) 生成独立的文件。
- -t 修改预处理器指令包含调试信息。
- -v 将生成的解析器的可读描述写入 y.output。

### 相关命令

bison

# 390 第二部分：命令

## 网络命令

网络命令将你连接到远程机器（在你的网络上或互联网上），并在连接后——帮助你完成会话。大多数情况下，这些命令用于 TCP/IP 网络（如互联网）。然而，许多此类命令也适用于 UUCP、AppleTalk 和其他类型的网络。

| afpd 启动 AppleTalk 守护进程 | afpd 选项(s) |

目的

`afpd` 命令启动 Linux 的 AppleTalk 协议 (AFP) 接口，指定哪些卷对用户可用。默认列列表通常在 /etc/AppleVolumes.system 中生成并一个

以下文件之一："/etc/AppleVolumes.system, $HOME/AppleVolumes 或 $HOME/.AppleVolumes。

### 选项

- -c maxconnections 指定最大连接数。默认值为五。
- -d 抑制守护进程的分叉（forking），并将所有 AFP 命令的跟踪写入标准输出。
- -f volumes 指定读取不同的 volumes 文件以获取默认卷列表。
- -g 设置访客账户名称。
- -n nbpname 使用 nbpname 进行名称绑定协议 [NBP] 注册。
- -s volumes 指定读取不同的 volumes 文件。
- -u 先读取用户的默认卷列表。

### 相关命令

atalkd

| atalkd 管理 AppleTalk 网络管理 | atalkd 选项 |
| :--- | :--- |

### 目的

atalkd 命令管理所有用户级 AppleTalk 网络管理：路由、名称注册与查找、区域查找以及 AppleTalk 回显协议 (AEP)。通常情况下，该命令在系统启动时由 /etc/rc 调用，并从 /etc/atalkd.conf 文件获取参数。

### 选项

- -f configfile 使用除默认 /etc/atalkd.conf 以外的配置文件。

### 相关命令

afpd

### 目的

bootpd 命令启动引导协议 (BOOTP) 服务器。它通常不直接从命令行运行，而是在 /etc/inetd.conf 文件中列出时由 inetd 调用。通过这种方式，它只有在引导请求到达时才会被启动。之后，它将一直保持在内存中，直到连续15 分钟没有请求。bootpd 配置文件 (bootptab) 存储了 bootpd 客户端所需的名称和地址信息。

此命令可以从 shell 启动。手动启动 bootpd 的良好时机是流量很大且你不希望用户等待服务器加载的时候。如果你知道有很多引导请求在等待，这可以更快地建立连接。

### 选项

- -c chdir-path 设置 bootpd 在检查客户端文件存在性和大小时使用的当前目录。
- -d debug_level 设置 debug_level 变量。
- -i 强制使用 inetd 模式，如果在15 分钟内没有请求，bootpd 将终止。这被认为是一个过时的选项，但为了兼容旧版本而予以保留。
- -s 强制使用独立模式，无论如何 bootpd 都将留在内存中。这被认为是一个过时的选项，但为了兼容旧版本而予以保留。
- -t timeout 指定 bootpd 在退出前等待请求的时间（以分钟为单位）。值为 0 表示 bootpd 不退出。

# 配置文件

bootptab 指定包含已知客户端和客户端选项的配置文件的名称。

dumpfile 指定 bootpd 在接收到 SIGURS1 信号时将其内部数据库转储的目标的文件名。

### 相关命令

- - bootptest
- inetd

| bootptest 测试引导服务器 | bootptest 选项(s) server_name |
| :--- | :--- |

### 目的

bootptest 命令通过每秒发送一次请求来测试 BOOTP 服务器（指定为 server_name），直到收到响应或有十个请求未得到答复。

### 选项

- -f bootfile 在请求的 boot-file 字段中使用 bootfile。
- -h 使用硬件地址来识别客户端。
- -m magic_number 用 magic_number 初始化厂商选项字段的第一个字字。

### 相关命令

- - bootpd

# dnsdomainname
显示域名

dnsdomainname 选项
主机名

### 目的

dnsdomainname 命令返回有关当前主机名的信息；特权用户可以使用该命令设置新的主机名。

### 选项

- -f 打印完整域名。
- -s 打印短域名。
- -F file 检查文件的主机名。

# dnsquery
显示 DNS 信息

dnsquery 选项(s)

### 目的

dnsquery 命令通过 Berkeley 命名系统 (BIND) 解析器库调用查询名称服务器。

### 选项

- -n name server 通过 IP 地址或域名指定名称服务器。
- -t type 将感兴趣的资源记录类型设置为以下之一：

### 第二部分：命令

等一下，下方的列表是：
- -c class 将感兴趣的资源记录类别设置为以下之一：
A 地址
NS 命名服务器
CNAME 规范别名
PTR 域名指针
SOA 权威起始点
WKS 熟知服务

| HINFO | 主机信息 |
| MINFO | 邮箱信息 |
| MX | 邮件交换 |
| RP | 责任人 |
| MG | 邮件组成员 |
| AFSDB | DCE 或 AFS 服务器 |
| ANY | 通配符 |

- - IN Internet
- - HS Hesiod
- - CHAOS Chaos
- ANY 通配符

- -p num 指定超时前的等待周期。
- -r num 设置在名称服务器没有响应时的重试次数。
- -s 使用数据流而不是数据包。

# faucet 服务器-客户端连接

### 目的

faucet 命令是伯克利软件发行版 (BSD) 网络管道的装置，提供了网络管道的功能。它作为服务器-客户端连接的服务器端，并与 hose 命令（在本章后文中描述）配合，特别是当你无法方便访问它时。

# 第10章：网络
显示域名, 401

> 注意
faucet 命令不被认为是非常安全的网络方法。请谨慎使用。

该命令还有许多选项。以下这些是最常用的。

### 选项

- -c chdir-path 设置 bootpd 在检查客户端文件存在性和大小时使用的当前目录。
- -d debug_level 设置 debug_level 变量。
- -i 强制使用 inetd 模式，如果在15 分钟内没有请求，bootpd 将终止。这被认为是一个过时的选项，但为了兼容旧版本而予以保留。
- -s 强制使用独立模式，无论如何 bootpd 都将留在内存中。这被认为是一个过时的选项，但为了兼容旧版本而予以保留。
- -t timeout 指定 bootpd 在退出前等待请求的时间（以分钟为单位）。值为 0 表示 bootpd 不退出。

# 配置文件

bootptab 指定包含已知客户端和客户端选项的配置文件的名称。

dumpfile 指定 bootpd 在接收到 SIGURS1 信号时将其内部数据库转储的目标的文件名。

### 相关命令

- - bootptest
- inetd

| bootptest 测试引导服务器 | bootptest 选项(s) server_name |
| :--- | : |

### 目的

bootptest 命令通过每秒发送一次请求来测试 BOOTP 服务器（指定为 server_name），直到收到响应或有十个请求未得到答复。

### 选项

- -f bootfile 在请求的 boot-file 字段中使用 bootfile。
- -h 使用硬件地址来识别客户端。
- -m magic_number 用 magic_number 初始化厂商选项字段的第一个字字。

### 相关命令

- - bootpd

# dnsdomainname
显示域名

dnsdomainname 选项
主机名

### 目的

dnsdomainname 命令返回有关当前主机名的信息；特权用户可以使用该命令设置新的主机名。

### 选项

- -f 打印完整域名。
- -s 打印短域名。
- -F file 检查文件的主机名。

# dnsquery
显示 DNS 信息

dnsquery 选项(s)

### 目的

dnsquery 命令通过 Berkeley 命名系统 (BIND) 解析器库调用查询名称服务器。

### 选项

- -n name server 通过 IP 地址或域名指定名称服务器。
- -t type 将感兴趣的资源记录类型设置为以下之一：
A 地址
NS 命名服务器
CNAME 规范别名
PTR 域名指针
SOA 权威起始点
WKS 熟知服务

### 第二部分：命令

| HINFO | 主机信息 |
| MINFO | 邮箱信息 |
| MX | 邮件交换 |
| RP | 责任人 |
| MG | 邮件组成员 |
| AFSDB | DCE 或 AFS 服务器 |
| ANY | 通配符 |

- -c class 将感兴趣的资源记录类别设置为以下之一：

- - IN Internet
- - HS Hesiod
- - CHAOS Chaos
- ANY 通配符

- -p num 指定超时前的等待周期。
- -r num 设置在名称服务器没有响应时的重试次数。
- -s 使用数据流而不是数据包。

# faucet 服务器-客户端连接

### 目的

faucet 命令是伯克利软件发行版 (BSD) 网络管道的装置，提供了网络管道的功能。它作为服务器-客户端连接的服务器端，并与 hose 命令（在本章后文中描述）配合，特别是当你无法方便访问它时。

# 第10章：网络
显示域名, 401

> 注意
faucet 命令不被认为是非常安全的网络方法。请谨慎使用。

该命令还有许多选项。以下这些是最常用的。

### 选项

- -c chdir-path 设置 bootpd 在检查客户端文件存在性和大小时使用的当前目录。
- -d debug_level 设置 debug_level 变量。
- -i 强制使用 inetd 模式，如果在15 分钟内没有请求，bootpd 将终止。这被认为是一个过时的选项，但为了兼容旧版本而予以保留。
- -s 强制使用独立模式，无论如何 bootpd 都将留在内存中。这被认为是一个过时的选项，但为了兼容旧版本而予以保留。
- -t timeout 指定 bootpd 在退出前等待请求的时间（以分钟为单位）。值为 0 表示 bootpd 不退出。



## 404 第二部分：命令

### 相关命令

### host

| host | host 选项 |
| :--- | :--- |
| 主机信息 | 主机名、服务器 |

### 目的
`host` 命令使用 DNS 打印指定主机名或服务器的信息。你也可以指定 IP 地址，这些地址将通过 DNS 转换为主机名。

### 选项

- -a class 查找任意 类型的资源记录
- -A 查找主机名的 IP 地址，然后进行反向查找以检查它们是否匹配。同时也查找地址的主机名，然后进行反向查找以检查是否匹配。还会检查给定区域内所有主机的 IP 地址。如果所有内容都匹配，则不返回任何信息。
- -c class 查找指定的资源记录类（ANY, CH, CHAOS, CS, CSNET, HS, HIOD, IN, INTERNET 或 **）。默认为 IN。
- -C 列出区域内的所有机器，确定该区域的服务器是否具有权威性。
- -d 在调试模式下工作。
- -dd 在调试模式下工作，但比 -d 更详细。
- -D 返回区域内唯一主机的数量，以及每个名称具有多个地址的主机名称。
- -e 抑制有关特定区域之外主机的信息。
- -E 返回区域内唯一主机的数量，以及额外区域主机的名称。
- -file 将输出发送到*file* 以及标准输出。
- -F file 将输出发送到*file*，额外的资源数据发送到标准输出。
- -G zone 返回区域内唯一主机的数量和网关主机的名称。
- -H zone 返回区域内唯一主机的数量。
- -i 返回有关 IP 地址的信息：主机名和类（始终为 PTR）。
- -I chars 忽略关于名称包含非法字符（由 *chars* 指定）的主名的警告。
- -l zone 返回*zone* 中所有主机的信息。
- -L level 使用 -l 选项时指定搜索级别。
- -m 打印 MB、MG 和 MR 记录；将 MR 和 MG 记录扩展为 MB 记录。
- -o 抑制向标准输出发送数据。
- -p server 返回有关特定区域内主服务器的信息。设计用于配合 -l 选项使用。
- -P servers 返回首选主机的信息；*servers* 是逗号分隔的列表。配合 -l 选项使用。
- -q 在静默模式下抑制警告，但不忽略错误消息。
- -r 从服务器请求缓存信息，而不是新的查询信息。
- -R 当发现非完全限定名时搜索本地命令的组件。
- -S 将所有主机（但不包括子区域）返回标准输出，包括主机类和 IP 地址。配合 -l 选项使用。
- -t 请求资源记录中类型条目的信息；类型为 A, ANY, NS, PTR 或 **。
- -T 打印缓存数据的生存时间（TTL）信息。
- -u 使用 TCP 代替 UDP。
- -v 在详细模式下工作。
- -vv 在详细模式下工作，包括主机上的默认设置。
- -w 持续工作直到主机返回信息。
- -x 查询多个主机和区域；也可以用 -x 查询多个服务器。
- -X 查询多个服务器以及多个主机和区域。
- -Z 在资源记录中包含尾部点，以及生存时间数据和类名。

### 相关命令

### hostname

### 目的
`hostname` 命令返回有关当前主机名的信息。特权用户可以使用该命令设置新的主机名。

### 选项

- -d 打印域名系统 (DNS) 域名。
- -f 打印完整域名。
- -s 打印短域名。
- -F 检查文件中的主机名。

## netstat

### 目的
`netstat` 命令显示网络连接、路由表、接口统计、伪装连接和 netlink 消息。在没有任何选项的情况下，`netstat` 命令列出所有打开的套字。

> 注意 此命令可能会返回大量数据。请查看在线手册页获取所有数据类型的列表。（输入 `man netstat`。）

### 选项

- -A, --af family 设置地址族的格式。family 变量是地址族关键字的逗号分隔列表：inet, unix, ipx, ax25, netrom 和 ddp。
- -c, --continuous-r, --route 每秒打印一次选定的表。返回内核路由表。
- -i, --interface iface 返回所有网络接口；如果列出了 iface，则返回特定接口的信息。
- -M, --masquerade 返回所有伪装会话的列表。结合 -e 选项返回扩展信息。
- -N, --netlink 返回 netlink 信息。
- -v, --verbose 在详细模式下返回信息。
- -n, --numeric 返回数值地址而不是符号化的主机、端口或用户名。

## ping

| ping | ping hostname |
| :--- | :--- |
| 检查远程主机 | |

### 目的
`ping` 命令向网络主机发送 ICMP ECHO_REQUEST 包以确定网络性能。基本上，`ping` 用于查看网络上的另一台计算机是否可以访问。

### 选项

- -c count 在发送（并接收）`count` 个 ECHO_RESPONSE 包后停止。
- -d 在所使用的套接字上设置 SO_DEBUG 选项。
- -f 按照包返回的速度输出包，或每秒 100 次，以较快者为准。
- -i 在发送包之间等待秒数。
- -l 以尽可能快的速度发送包，然后进入正常模式。
- -n 以数值模式工作。
- -p 指定填充包的“pad”字节。
- -q 在静默模式下工作；显示启动和结束时的摘要行。
- -r 绕过正常路由表直接发送到附加的主机。
- -R 在 ECHO_REQUEST 包中包含 RECORD_ROUTE 选项并在返回包时显示路由。
- -s 指定发送的数据字节。默认为 56。
- -v 输出详细信息。

## rcp
远程复制

### 目的
`scp` 命令在机器之间复制文件。这些机器可以是本地网络或互联网上的。（通常，网络管理员会禁用 rcp 和其他“r”命令。）

### 选项

- -k realm
- -p 保留修改时间。
- -r 递归复制目录。
- -x 使用 DES 加密文件。

### 相关命令

- rlogin
- rsh

## rlogin
远程登录

### 目的
`rlogin` 命令在指定的主机上打开会话。它最初使用 Kerberos 授权，但如果远程主机不支持，可以使用标准的 Berkeley主机授权机制。

> 引用
查看在线手册页获取有关 Kerberos 认证的详细信息。（输入 `man rlogin`。）

### 选项

- -8 始终允许 8 位输入数据路径；否则，除非远程端的停止起始字符不是 ^S/^Q，否则将剥除校验位。
- -d 在与远程主机通信的 TCP 套接字上开启调试。
- -e 定义转义字符，替换默认的波浪 (~)。
- -E 防止任何字符识别为转义字符。
- -K 关闭 Kerberos 认证。
- -k 在 realm 中获取远程主机的票，而不是根据 krb_realmoofhost 指定的远程主机 realm。
- -L 以 litout 模式运行。
- -x 使用 DES 加密。

### 相关命令

- rcp
- rsh

| rsh rsh option(s) |
| :--- | :--- |
| 远程 Shell 主机命令 |

### 目的
`rsh` 命令在远程主机上运行命令。它将其标准输入复制到远程命令，将远程命令的标准输出复制到标准输出，并将远程命令的标准错误复制到标准错误。中断、退出和终止信号会传递给远程命令；rsh 通常在远程命令结束时终止。



### 选项

- -X 关闭 Kerberos 认证。
- -d 开启 socket 调试。
- -k realm 获取指定 realm 中远程主机的票据，而不是远程主机所在 realm 的票据（由 krb_realmofhost 决定）。
- -l username 指定远程用户名。
- -n 将输入从特殊设备 /dev/null 重定向。
- -x 开启 DES 加密。

### 相关命令

- rcp
- rsh
- rlogin

### 目的

rstart 命令实际上是一个 远程启动（Remote Start）客户端的示例实现。它使用 rsh 作为底层的远程执行机制。

### 选项

- -ccontext 指定命令的上下文，它是一个通用环境。默认值为 x。
- -g 将命令行上的命令解释为协议文档中定义的通用命令。
- -l username 告诉 rsh 以指定的用户名运行命令。
- -v 在详细模式下运行，丢弃来自远程主机 rstart 辅助程序的输出，并断开与 rsh 的连接。

### 相关命令

- rsh
- rstartd

| rusers | rusers 选项 |
|---|---|
| 生成用户信息 | 主机名 |

### 目的

rusers 命令生成关于登录到特定主机（或主机）或本地网络上所有机器的用户信息。

### 选项

- -a 列出所有机器，即使目前没有用户登录。
- -l 以长格式返回列表：用户名、主机名、用户登录的 tty、用户登录的日期和时间、用户在键盘上输入的时间，以及他们登录的远程主机（如果适用）。

如果机器在 11 分钟内没有向 rwho 报告，则认为该机器已宕机。还会报告小于一小时的用户空闲时间。

### 选项

- -a 报告所有用户，即使是过去一小时内未在机器前输入过的用户。

### 相关命令

- rusers

- users
- who

## rwall
### 发送系统消息

## rwall 主机名文件名

### 目的

rwall 命令向登录到指定主机名的所有用户发送消息。消息可以通过指定的文件发送，也可以直接输入并用 EOF (Ctrl+D) 结束。

## rwho
### 检查登录用户

## rwho 选项

### 目的

rwho 命令显示登录到本地机器的用户。输出与 who 命令类似，不同之处在于信息涵盖了本地网络上的所有人。如果机器在 11 分钟内未向 rwho 报告，则假设该机器已损坏。还会报告小于一小时的用户空闲时间。

### 选项

- -a 报告所有用户，甚至是过去一小时内未在机器前输入过的用户。

### 相关命令

- rusers

## sliplogin
### 通过 SLIP 登录

sliplogin 用户名

### 目的

sliplogin 命令允许你使用串行链路接口协议（SLIP）连接到互联网系统。它从 /etc/slip.hosts 文件中获取信息（匹配登录名）然后启动连接。/etc/slip.hosts 文件必须由 root 用户配置。

## sockdown
### 管理系统关机 (GNU 命令)

sockdown 选项

### 目的

sockdown 命令在其由 fd 命令指定的一个文件描述符上执行关机系统调用。sockdown 可使用的值如下：

- 0 转换为只写文件描述符。0 的符号表示为 writeonly。
- 1 转换为只读文件描述符。1 的符号表示为 readonly。
- 2 完成关机——未来不允许任何读取或写入。2 的符号表示为 tally。

## 与用户聊天

## talk
### 用户名 [tty]

### 目的

talk 命令允许你与当前登录到系统的另一个用户进行交互式聊天。当双方运行 talk 命令时，屏幕会分成，一个用户的输入显示在屏幕的一部分，另一个用户的输入显示在屏幕的另一部分。

用户名可以是系统上的某人。如果你想与另一个系统上的用户聊天，必须以 user@host 的格式指定用户名。如果用户有多个终端，可以使用 tty 指定终端。要退出 talk，请输入 Ctrl-D。

### 相关命令

- write
- ytalk

## 连接到远程主机

## telnet
### 选项 主机名

## 目的 

telnet 命令使用 Telnet 协议启动到远程主机的连接。从那里，你可以将远程主机作为。

### 选项

- -a 尝试自动登录。
- -d 开启调试。
- -e 设置转义字符。
- -l 告诉 rsh 以指定的用户名运行命令。
- -n 将输入从特殊设备 /dev/null 重定向。
- -x 开启 DES 加密。
- -y 开启 socket 调试。
- -v 在详细模式下运行，丢弃来自远程主机 rstart 辅助程序的输出，并断开与 rsh 的连接。

## uucp
### 复制文件
uucp 选项 源文件
uucp 选项 目标文件

### 目的

uucp 命令在之间复制文件。

### 交叉引用

查看的在线手册。

## write
### 写入消息
write 用户名

### 目的

write 命令向...发送消息。

## x270
### 访问系统
x270 选项 源文件
目标目录
x270 选项 主机名

### 目的

x270 命令添加 MS-DOS 文件系统。

### 交叉引用

查看的在线手册。

## ytalk
### 在网络上聊天
ytalk 选项
用户名

### 目的

ytalk 命令是。

### 选项

- -a 执行文本文件传输，将换回符/换行符转换为换行符。
- 保留文件修改时间。
- -x 如果正在覆盖现有文件则不警告。
- -v 在详细模式下运行。

## Mtools
### 命令

Mtools 系列命令用于 MS-DOS 文件和目录。

## mattrib
### 修改属性
mattrib 选项 文件

### 目的

mattrib 命令更改 MS-DOS 文件的属性。

## 属性

- a 归档位。
- h 隐藏位。
- r 只读位。
- s 系统位。

## mbadblocks
### 识别坏块
mbadblocks 驱动

### 目的

mbadblocks 命令扫描驱动（软磁盘）的坏块。

## mcd
## 目录

### 目的

mcd 命令更改。

### 相关命令

- mdir

## mcopy
### 复制文件
mcopy 选项 源文件目标文件
mcopy 选项 源文件

### 目的

mcopy 命令在之间复制 MS-DOS 文件。

### 选项

- -a 执行文本文件传输，将换回符/换行符转换为换行符。
- 保留文件修改时间。
- -x 如果正在覆盖现有文件则不警告。
- -v 在详细模式下运行。

### 相关命令

- mread
- mwrite

## mdel
### 删除文件
mdel 选项 文件

### 目的

mdel 命令删除 MS-DOS 文件。

### 选项

- -v 在详细模式下运行，删除文件时会在屏幕上打印文件名。

## mformat
### 格式化软磁盘
mformat 选项 驱动

### 目的

mformat 命令在 Linux 格式化的磁盘片上添加 MS-DOS 文件系统。

### 选项

- 1 覆盖 2m 格式的使用，即使磁盘当前的几何结构是 2m。
- 2 以 2m 格式工作——轨道 0 头 0 的扇区数。
- h 指定头数（面）。
- H 指定隐藏扇区数。
- 1 设置可选卷标。
- M 设置软件扇区。
- n 设置序列号。
- t 指定轨道数（不是磁柱）。
- s 指定每轨道扇区数。
- S 指定大小代码。
- X 将磁盘格式化为 Xdf 磁盘，用于 OS/2。

### 相关命令

- mlabel



## mrd
删除目录树

mrd 选项
msdosdosdirectory

### 目的
mrd 命令删除 MS-DOS 目录树以及其中的任何文件和子目录。此操作发生在软盘上的 MS-DOS 文件系统上。

### 选项
- -v: 以详细模式运行，在删除时列出每个文件和目录。

## mdir
列出目录内容

mdir 选项(s)
msdosdosdirectory

### 目的
mdir 命令显示 MS-DOS 目录的内容，通常位于软盘上。

### 选项
- -a: 列出隐藏文件。
- -w: 以宽格式输出，不显示文件大小或创建日期。

## mlabel
创建卷标签

mlabel 选项(s) drive器
new_label

### 目的
mlabel 命令在软盘上创建 MS-DOS 卷标签。在不带选项的情况下，它会显示当前标签。如果没有设置 c 选项，系统会提示你输入新标签；此时，如果你不输入新标签直接按回车，现有的标签将被删除。

### 选项
- -c: 清除现有标签，且不提示用户。
- -s: 显示现有标签，且不提示用户。

### 相关命令
mformat

### 目的
mmd 命令在软盘上创建 MS-DOS 子目录。如果目录已存在，则会发生错误。

### 选项
- -v: 以详细模式运行，在创建目录时返回目录名称。

### 相关命令
mrd

### 目的
mmount 命令挂载 MS-DOS 磁盘。它读取 MS-DOS 磁盘的引导扇，配置驱动器几何结构并将其挂载，同时将 mountargs 传递给 mount 命令。

### 相关命令
mount

| mmove 移动/重命名文件或目录 |
| :--- | :--- |
| mmove 选项 sourcefile targetfile |
| mmove 选项 sourcefile(s) targetdirectory |

### 目的
mmove 命令移动或重命名现有 MS-DOS 文件或子目录。

### 选项
- - 以详细模式运行，如果新文件名无效，则显示新文件名。

### 相关命令
mren

| mrd 删除目录 |
| :--- | :--- |
| mrd 选项 msdosdirectory |

### 目的
mrd 命令从软盘上删除 MS-DOS 目录。

### 选项
- -v: 以详细模式运行，在删除目录时显示目录名称。

### 相关命令
mdeltree
mmd

## mread
复制文件
mread 选项(s)
msdosfile unxifile

### 目的
mread 命令将 MS-DOS 文件复制到 Linux 系统。这是一个过时的命令，但某些旧脚本可能支持它。首选命令是 mcopy。

### 相关命令
- - mcopy
- - mtype

## mren
重命名文件
mren 选项 sourcefile
targetfile

### 目的
mren 命令重命名软盘上的 MS-DOS 文件。

### 选项
- -v: 以详细模式运行，如果新文件名无效，则显示新文件名。

### 相关命令
- - mmove

## mtest
配置工具
mtest

### 目的
mtest 命令读取 Mtools 文件并将累计配置打印到标准输出，该输出可以作为配置文件使用。你可以用它将旧配置文件转换为新的配置文件。

## mtype
显示文件
mtype 选项(s) msdosfile

### 目的
mtype 命令显示 MS-DOS 文件。

### 选项
- -s: 从显示的文件中去除高位。
- -t: 假设该文件为文本文件。

### 相关命令
- - mcd
- - mread

## mwrite
复制文件
mwrite unixfile dosfile

### 目的
mwrite 命令将 Linux 文件复制到软盘上的 MS-DOS 文件系统。该命令被认为是过时的，仅存在是为了提供对旧 shell 脚本的向后兼容。请使用 mcopy 命令。

### 相关命令
- - mcopy

##通过 Linux Shell 交互
我们对 Linux Shell 的回顾在这一章结束，这一章对用户至关重要。要与 Linux Shell 交互，你可以使用命令行。Shell 是一种命令行功能，演示了如何与系统交互，反之亦然。

## Linux Shells
大多数 Linux 发行版至少包含六种 shell。可用的 shell 类型包括：
- bash (Bourne Again Shell)
- csh (C Shell)
- tcsh (T C Shell)
- sh (Bourne Shell)
- ksh (K Shell)
- ash (Ash)
- zsh (Z Shell)

当你安装 Linux 发行版时，shell 通常由管理员设置。要更改你的登录 shell，请使用以下命令：
```bash
chsh -s /csh
```
或
```bash
chsh -s /zsh
```

## Shell 变量
Shell 环境变量提供存储信息的方法，供 shell 脚本使用。你也可以自己设置或使用变量。你可以通过在变量前加上美元符号并使用 echo 命令查看任何 shell 变量的内容。例如，你可以输入以下内容查看你的路径：
```bash
echo $PATH
```

| 变量 | 解释 |
| --- | --- |
| IFS | 内部字段分隔符，用于扩展后的单词拆分以及使用 read 内置命令拆分行。默认值是空格-制表符-换行符。 |
| PATH | 命令的搜索路径。它是由冒号分隔的目录列表，shell 在其中查找命令。默认路径取决于系统并由安装 bash 的管理员设置。 |
| HOME | 当前用户的家目录；cd 命令的默认参数。 |
| CDPATH | cd 命令的搜索路径。它是由冒号分隔的目录列表，shell 在其中查找 cd 命令指定的目标目录。 |
| ENV | 如果 bash 执行 shell 脚本时设置了此参数，其值将被解释为包含初始化 shell 命令的文件，如 .bashrc。ENV 的值在解释为路径之前会经过参数扩展、命令替换和算术扩展。PATH 不用于搜索结果路径名。 |
| MAIL | 如果此参数设置为文件名且未设置 MAILPATH 变量，bash 会告知指定文件中有邮件到达。 |
| MAILCHECK | 指定 bash 检查邮件的频率（秒）。默认为 60 秒。当需要检查邮件时，shell 会在提示之前进行检查。如果未设置此变量，shell 将禁用邮件检查。 |
| MAILPATH | 用于检查邮件的冒号分隔的路径列表。可以通过 ? 分隔路径和消息来指定要打印的消息。 |



## 434 第三部分：通过 Linux Shell 交互

MAIL_WARNING 如果设置，且自上次检查以来已访问过 bash，将显示消息“The mail in mailfile has been read”（mail文件中的邮件已读）。

PS1 设置主提示符。默认值为 bash\$。

PS2 设置次级提示符，许多应用程序用它来提供输入。默认值为 >。

PS3 设置 `select` 命令的提示符。

PS4 设置在执行跟踪中命令前使用的字符值。默认值是 `+`。

HISTSIZE 设置命令历史记录中记住的命令数量。默认值为 500。

HISTFILE 设置命令历史记录保存的文件名。默认值为 `~/.bash_history`。

HISTFILESIZE 设置历史文件的最大行数。默认值为 500。

IGNOREEOF 控制 shell 在接收到 EOF（文件结束符）字符作为唯一输入时的动作。如果设置，该值表示在 bash 退出前作为输入行输入的连续 EOF 字符数。如果该变量存在但不是数值或没有值，则默认值为 10。如果不存在，EOF 表示 shell 的输入结束。这仅对交互式 shell 有效。

TEOUT 如果设置为大于零的值，该值被解释为发出主提示符后等待输入的秒数。如果在该秒数内没有收到输入，bash 将终止。

FIGNORE 一个用冒号分隔的后缀列表，在执行文件名补全时忽略。后缀匹配 FIGNORE 中某条目的的文件名将从匹配文件名列表中排除。示例值为 `.o~`。

# 索引

## A

- 访问远程计算机, 27
- 服务器, 20
- actsync 命令, 311-313
- afpd 命令, 395-396
- agetty 命令, 60–66
- 别名 (aliases)
  - elm 和, 20
  - 列出, 20
- 匿名 FTP, 325
- ANSI, 转换为 K&R, 368
- ansi2knr 命令, 368
- answer 命令, 313
- APPEND DOS 命令, 34
- 合并文件, 20
- AppleTalk
  - 守护进程，启动, 395–396
  - 文件守护进程, 20
  - 网络管理, 396–397
  - 网络支持, 20
- appres (列出 X 资源) 命令, 61–62
- apropro (搜索 whatis 数据库)
  - 命令, 62
- ar 命令, 368–370
- arch (返回机器架构)
  - 命令, 63
- 架构, 20
- 存档, 20
- BACKUP DOS 命令, 34
- 压缩的, 240
- 坏块, 420
- 文件, 368-370
- banner 命令, 64–65
- shell, 29, 114–116
- 横幅，打印, 20, 64–65
- 参数 (arguments)
- basename, 192
- 永久显示, 189
- basename, 文件, 20
- I/O (输入/输出), 14
- 列出, 192
- as 命令, 370–371
- bash 命令, 65
- ASCII, 转换为/从位图, 20
- bash shell, 431
- ash (ash shell) 命令, 63
- 批命令, 20
- ash shell, 52
- 批处理，电子邮件, 26
- ASSIGN DOS 命令, 34
- bc 命令, 65–68
- atalkd 命令, 396–397
- BDF 字体, 77–88
- atom (转换位图图像) 命令, 64
- dfopf 命令, 68–69
- 文件开头，显示, 267–268
- 原子 (X), 20
- 参考文献, 293
- ATTRIB DOS 命令, 34
- biff 命令, 315
- 属性 (attributes)
- 二进制文件, 419–420
- 编辑, 243–244
- 根目录窗口, 28
- 文本，查找, 29
- bison 命令, 371–372
- bitmap 命令, 69–70
- 组合, 314
- 位图 (bitmaps)
- 电子邮件，播放, 357
- 转换, 71
- 编辑, 20, 69–70
- audiocompose 命令, 314
- 字体，转换, 68–89
- audiosend 命令, 314–315
- 图像，转换, 64
- 授权 (X), 20
- 查看, 20
- AWL (GNU), 375
- 位 (bits), 9
- 坏块, 420
- 搜索, 20
- 后台 (X)
- bmaa 命令, 71
- 属性, 20
- 引导程序，安装, 20
- 图像, 20
- 启动服务器
- cc 命令, 372
- 启动, 397-398
- 测试, 398
- cd 命令, 193-194
- CD DOS 命令, 34
- CD-ROM，创建, 73-77
- bootpd 命令, 397-398
- hottest comod, 398
- Bootstrap Protocol, 20
- 音频 CD, 21
- 边界框，尺寸, 292
- cdwrite 命令, 76-77
- Bourne Again shell, 65, 431
- bpe 命令, 243-244
- 删除, 301
- BREAK DOS 命令, 34
- 传输, 296-297
- transl, 301
- 基于文本, 332-336
- 在网络聊天, 417
- 字节，计数, 22
- CHCP DOS 命令, 34
- bzip2 命令, 192-193
- CHDIR DOS 命令, 34
- checknews 命令, 316
- 代码，生成, 388
- 校验和 (checksums), 233
- chfn 命令, 316
- 执行配置文件, 378-379
- chgp 命令, 194
- Pascal 转换, 385-385
- 预处理器, 373
- chmod 命令, 195-198
- C 程序, 20, 391-392
- C shell, 79, 131
- C++
- 程序，编译, 20, 431
- cal 命令, 72
- 类 (classes), 136
- 计算器 (X), 146
- 日历, 21, 72
- CALL DOS 命令, 34
- 客户端/服务器, 400-401-404
- 客户端应用程序, 166-197
- 运行, 21
- 剪贴板，显示内容, 21
- 压缩文件, 205
- CLS DOS 命令, 34
- 文件, 21, 246-253-254
- cmp 命令, 246-247
- 颜色, 21, 297-298
- crt 命令, 79
- 设备 (devices), 118
- 目录, 20
- Fortran 程序, 21
- 存档 (archives), 240
- 压缩文件, 315
- 压缩, 20, 370
- 配置, 2, 2




# 索引

- devices (继续) 目录树，删除, 423
- PC 卡, 27
- 磁盘可用空间,列出, 22
- PCMIA, 监控, 28
- DISKCOMP DOS 命令, 34
- diff 命令, 251-253
- DISKCOPY DOS 命令, 34
- diff3 命令, 253-254
- dir 命令, 203-204
- 磁盘
- DIR DOS 命令, 34
- DOS, 挂载, 424-425
- dircolors 命令, 82-83
- 软磁盘，格式化, 23
- 目录, 7-8, 10-11
- 挂载, 27
- 修改, 22, 193-194, 420
- 颜色, 82-83
- DNS 信息, 显示, 399-400
- 内容,列出, 423
- DNS 服务器,查询, 22
- 创建, 22, 225
- dnsdomaincommand 名称, 399
- 当前目录, 10
- dnsquery 命令, 399-400
- 空的,删除, 231
- etc, 11
- 文档, Groff, 格式化, 263-264
- 文件列出, 221-223
- 域名
- 字体,创建, 227
- 显示, 399
- HFS, 24-26, 213, 217
- 显示, 22
- 层级结构, 225
- DOS
- 列出内容, 203-204
- 命令交叉引用, 33-36
- 移动, 425
- 磁盘,挂载, 424-425
- 所有权,修改, 198
- FAT 文件系统, 225-226
- 打印, 22
- 文件系统,创建, 22
- 删除, 28, 425
- 文件,转换为 Linux, 22
- 重命名, 425
- 文本文件,转换为 UNIX, 208
- 根目录, 10
- DOSKEY DOS 命令, 34
- 根目录,修改, 199
- DOSHELL DOS 命令, 34
- sbin, 11
- 驱动程序, PostScript, 265
- 子目录, 10, 424
- 驱动器,分区, 27
- usr, 11
- dumpkeys 命令, 83-84
- var, 11
- 工作, 212, 216-217, 230

# 索引 443

## E
- 快速邮件, 398
- echo 命令, 84-85
- 蚀刻邮件, 319-322
- ECHO DOS 命令, 34
- 格式化,非 ASCII, 358
- echo,输入, 22
- 格式化, 22, 26
- EDIT DOS 命令, 34
- From 字段,列出, 324-325
- 编辑
- 传入的, 22, 26
- 位图, 69-70
- MIME, 26-27
- 二进制文件, 243-244
- MIME 编码,启用, 345, 346
- 图形, 23
- 图像, 24, 183-184
- 支持 MIME 的, 343-345, 358
- 资源 (X), 30
- 多媒体, 22, 27
- 文本文件, 22
- 图片, 359
- 编辑器
- 打印, 22, 26, 351
- Joe's Own Editor, 270-273
- 处理, 351-353
- Jonathan's Own Version of Emacs
- 读取, 22, 27, 354-355, 274-275
- 读取消息, 353-354
- pico, 289-290
- 回复, 22, 26
- 文本, 255-257, 303-305
- 响应新闻组, 356-357
- egrep 命令, 254-255
- 弹出可移动介质, 22
- 获取, 22, 26, 349-350
- Jaz 磁盘, 25
- Zip 磁盘, 25
- 服务器, 23
- 电子邮件
- 地址,验证, 362
- 音频,播放, 357
- 批处理,发送, 23, 26
- 检查, 315
- 检查新的, 363
- 创建, 22, 26
- 仿真,启动, 255
- 解码文件, 361
- 编码, 26
- 文件, 23, 361
- 外部,显示, 352
- 环境, 85-86
- 修改, 23, 104
- etc 目录, 11
- 可执行文件,压缩, 21, 210
- 执行,配置文件, 378-379
- expand 命令, 257
- EXPAND DOS 命令, 34
- 表达式, 258-259
- 电子邮件,显示, 357
- 二进制, 243-244
- 开始,显示, 243-268
- 检查, 78
- 校验和, 233
- 合并, 21
- 压缩, 21, 28-30, 192-193, 199-200, 209-211
- FAT 文件系统, DOS, 225-226, 305-508
- faucet 命令, 400-401
- FC DOS 命令, 34
- FDISK DOS 命令, 34
- fastmail 命令, 318-319
- FASTHELP DOS 命令, 34
- FASTOPEN DOS 命令, 34
- fetchmail 命令, 319-322
- fgrep 命令, 258-259
- 字段,切割, 250
- FIFO (GNU), 23, 226
- 文件命令, 204-205
- 文件管理器,列出, 286-288, 299-300, 427
- 文件系统, 9
- 八进制,偏移量, 27
- 创建, 23, 227
- 格式化, 23, 259
- 在, 25, 218-219
- 列出, 25, 221-223
- 锁定, 221
- 长的,分割, 249-250
- makefiles, 380, 383-384
- 合并, 26, 224, 289, 293-295
- 移动, 27, 229, 425
- 名称, 209, 220
- 对象, 370-371
- 对象文件,复制, 385
- 八进制,偏移量, 230
- 普通, 9
- 所有权,修改, 27, 198
- 权限,模式, 27
- PostScript, 28, 260
- 打印, 28, 244-246
- 读取, 244-246, 295
- 删除, 28, 231
- 重命名, 425, 426
- 反转行, 28
- 搜索, 28, 205-208
- 查找, 23, 28
- 信号, 221
- shar,解包, 134
- 排序, 21, 25
- 排序, 29
- 分割, 29, 298
- 特殊 (GNU), 228
- 标签文件, 373, 374
- 文本文件,转换表符, 302
- 文本,格式化, 301
- 类型, 29, 204-205
- 验证,计数, 23
- 查看, 30
- 配置, 30, 154
- 配置, 29, 208
- find 命令, 205-208
- FIND DOS 命令, 34
- finger, 23
- 配置文件修改, 316-317
- finger 命令, 322-323
- 软磁盘, 23, 422
- 挂载, 27
- fmt 命令, 259
- 字体, 155
- 目录, 227
- 列出, 23, 86-87, 167-198
- 位图,转换, 68-89
- 目录, 227
- 列出, 23, 86-87, 167-198
- 服务器, 23, 157

# 索引 444

## F
- 强制新的, 239
- 列, 21, 248
- 修正, 78-79
- 电子邮件, 22, 26, 358
- 文件, 23, 259
- 软磁盘, 23, 422
- Groff 文档, 263-264
- gawk 命令, 375
- gcc 命令, 375-376
- gdb 命令, 376-378
- 调试器前端, 392-393
- 通用命令, 59-189
- getfilename 命令, 209
- getcodes 命令, 88
- getlist 命令, 331
- getpeername 命令, 402
- getty 命令, 88
- 邮件, 323-324
- 输出,打字机, 265-266
- PCL5, 264
- 文本, 260, 301

## Fortran
- 编译, 375
- 执行, 378-379
- 程序,编译, 21
- 四位数,权限, 198
- 符号, 23
- 格式,创建, 26
- 格式化, 23, 259
- 调试器, 376-378
- 目录,空的, 231
- FIFO,创建, 21, 226
- 文件,行, 300-302
- 文件,大小, 231
- 文件, 23, 273, 275, 289, 293-295, 298, 300

## GNU
- 存档文件, 368-370
- AWK, 375
- 文档引用, 29
- C 编译器, 375
- 字符, 301
- 校验和, 233
- 调试器, 376-378
- 目录,空的, 231
- FIFO,创建, 21, 226
- 文件,行, 300-302
- 文件,大小, 231

## FTP
- 服务器,启动, 23
- 启动, 360
- 用户,列出, 331
- ftp 命令, 325-331
- , 331

# 索引 445

## G
- gnuplot 命令, 90
- GOTO DOS 命令, 34
- gprof 命令, 378-379
- GRAFT DOS 命令, 34
- GRAPHICS DOS 命令, 34
- 图形,编辑, 23
- grep 命令, 261-262
- godvi 命令, 262
- Groff 文档,格式化, 263-264
- Groff 命令, 263-264
- grolj 命令, 264
- 组,命令, 265
- 分配,修改, 194
- 创建, 24
- 符号, 23
- 权限, 23, 229-230
- gs 命令, 266-267
- gunzip 命令, 209-210
- gzexe 命令, 210
- gzip 命令, 210-211

# 索引 446 H
- 挂起, 101
- hattrib 命令, 211-212
- hcd 命令, 212
- hcopy 命令, 212-213
- delel 命令, 213
- hdiram 命令, 213
- head 命令, 267-268
- Header,函数, 388
- HELP DOS 命令, 34
- 帮助,在线, 24
- hformat 命令, 213-214
- HFS
- 属性, 25, 211-212
- 内容,列出, 215-216
- 创建, 25, 213-214
- 目录, 24-26, 213, 217
- 显示, 24
- 文件属性, 24
- 文件管理器,打开, 238




## 448 索引

### HFS（续）
- 文件系统, 24
- 文件, 24, 26–212–217
- 分叉 (forks), 25
- Shell (shell), 24, 26, 214–215
- 卷 (volumes), 24, 26, 216–217
- hfs 命令, 214–215
- 层级结构，目录, 216
- hls 命令, 216
- hmount 命令, 216
- hose 命令, 403–404
- 主机 (host), 24, 404–406
- 名称 (name), 24, 406–407
- 远程, 408, 415
- host 命令, 404–406
- hostname 命令, 406–407
- hpwd 命令, 216–217
- hrenname 命令, 217
- hrmdir 命令, 217
- humount 命令, 217
- hvol 命令, 218

### GNU, 89
- 根目录窗口, 28
- imake 命令, 380
- IMAP 邮件服务器，启动, 24
- In 命令, 218–219
- 传入电子邮件, 26
- info 命令, 91–95
- 输入 (input)
  - 列, 248
  - 回显 (echoing), 22, 84–85
  - 修改, 295
- interlnk DOS 命令, 34
- Internet 服务器, 24
- Internet/电子邮件服务器, 311–364
- 解析请求, 297
- intersvr DOS 命令, 34
- ispell 命令, 268–269

### J
- Jaz 磁盘，弹出, 25, 100
- joe 命令, 270–273
- Joe's Own Editor (GNU), 270–273
- join 命令, 273
- JOIN DOS 命令, 25
- 合并排序文件, 25
- Jonathan's Own Version of Emacs, 274–275

### I
- I/O (输入/输出)
  - 参数, 14
  - 管道 (pipes), 14
  - 标准 I/O, 11–34
- id 命令, 90–91
- if DOS 命令, 34
- 图像 (images)
  - 位图，转换, 66
  - 编辑, 24, 183–354
- jove 命令, 274–275
- JPEG 文件, 106

### K
- K&R，从 ANSI 转换, 368
- 列出 (listing)
  - basename, 192
  - kbd_mode 命令, 92
  - 客户端应用程序，运行, 21, 166–167
  - 内核 (kernel)
    - 消息，日志, 25
    - 内容，HFS 卷, 215–216
    - 模块, 25
    - 目录内容, 203–204, 423
    - 符号，显示, 25
  - 磁盘可用空间, 22
  - 键盘, 92
  - 文件大小, 232
  - 信息，查看, 25, 83–84
  - 文件, 25, 221–223
  - 字体, 23, 86–87, 167–168
  - 键位映射 (keymaps)
    - 修改, 170
    - 空闲内存, 26
    - X, 修改, 25
  - 来自自字段 (From fields), 324–325
  - 击键，保存到文件, 25
  - 新闻组, 27, 346–347
  - 关键字，信息, 25
  - 资源, 28, 94
- kill 命令, 92–93
- 主题字段 (Subject fields), 324–325
- killall 命令, 93–94
- 用户，网络, 27
- 单词, 232, 234
- Korn shell, 431
- listres 命令, 94

### L
- LABEL DOS 命令, 34
- LOADFIX DOS 命令, 34
- 标签 (labels)，卷, 423–424
- LOADHIGH DOS 命令, 34
- Lempel-Ziv 编码，文件压缩, 210–211
- locate 命令, 219–220
- locateb 命令, 220
- less 命令, 275–283
- 模式查找, 219–220
- lockfile 命令, 221
- 锁文件, 221
- 登录 (log in), 25, 95, 文件, 273, 293, 297–298, 320–303, 搜索, 283, 会话管理, 88
- 链接文件, 25, 218–219, 链接 (links), 10
- SLIP, 414
- 日志 (logging) in, 10
- 日志消息，内核, 25
- ls 命令, 7–8, 221–223, 颜色, 21
- 登录命令 (login), 95, 名称查看, 25
- logname 命令, 95–96
- look 命令, 283
- lpq 命令, 283–284
- lpr 命令, 284–285
- lprs 命令, 286
- lynx 命令, 332–346

### M
- Macintosh。见 HFS
- 放大屏幕, 168
- 邮件服务器，启动, 24, 26
- 邮件。见 electronic mail
- mail 命令, 336–343
- make 命令, 381–382
- makedepend 命令, 383–384
- makefiles，创建, 392, 解析, 383–384
- makestrs 命令, 384
- makwhat 命令, 96
- man 命令, 96–98
- 手页 (man pages), 96–98, 168–169
- mattrib 命令, 419–428
- mbadblocks 命令, 419–428
- 消息对象 (message objects), 384–385
- 消息，计数, 343, 内核, 日志, 25, 组，检查, 316
- metamail 命令, 343–346
- metasend 命令, 344–345
- mformat 命令, 422
- Midnight Commander (GNU)，启动, 223–224
- MIME，电子邮件, 26, 以及 23, 编码, 27, 启用, 345, 346
- MIME 邮件, 343–344
- 部分格式, 358
- 发送, 344–345
- mimencode 命令, 345
- minicom 命令, 99–100
- mimicript 命令, 108
- MIRROR DOS 命令, 34
- mkdir 命令, 225
- MKDIR DOS 命令, 34
- mkdirhier 命令, 225
- mkdosfs 命令, 225–226
- mkfifo 命令, 226
- mkfontdir 命令, 227
- mkfts 命令, 227
- mkmanifest 命令, 228
- mknod 命令, 228
- mlabel 命令, 423–424
- mmd 命令, 424
- mmncode 命令, 346
- mmount 命令, 424–425
- mmove 命令, 425
- MODE DOS 命令, 34
- 调制调器，xmodem, 30, ymodem, 30
- 模块，内核, 25, 卸载, 27
- more 命令, 286–288
- MORE DOS 命令, 34
- 挂载，DOS 磁盘, 424–425, 软磁盘, 27, 鼠标，终端模式, 27
- MOVE DOS 命令, 34
- 移动，目录, 225, 文件, 27, 229, 425
- mrd 命令, 423, 425
- mread 命令, 426
- mren 命令, 426
- MSAV DOS 命令, 34
- MSD DOS 命令, 34
- msgfmt 命令, 384–385
- mtest 命令, 426
- Mtools 命令, 419–427
- mtype 命令, 427
- mv 命令, 9, 229
- mzip 命令, 100

### N
- netstat 命令, 407
- 网络命令, 395–418
- 网络，AppleTalk，管理, 396–397, 聊天, 417, 统计, 27, 407, 用户，列出, 27
- newsgroups 命令, 346–347, 检查更新, 316, 在线手册, 96–98, 列出, 27
- nice 命令, 101
- NLSFUNC 命令, 34
- nohup 命令, 101
- nroff 命令, 288

### O
- olock 命令, 102
- 八进制文件, 27
- od 命令, 230
- 偏移量，打印, 230

### P
- 绘画程序 (X), 171–172
- 解析器，生成, 371–372, 解析 makefiles, 383–384
- 分区驱动, 27
- passwd 命令, 102–103
- 模式搜索, 258–259
- POWER DOS 命令, 34
- PAUSE DOS 命令, 34
- pr 命令, 290–292
- 暂停系统, 119
- PC 卡，设备, 27
- 打印后台守护进程 (daemon), 284–285, PCMIA
- 日志 (logging)，内核, 25, 移除, 27
- more 命令, 286–288
- MORE DOS 命令, 34
- 打印任务 (print jobs)，删除, 28
- pine 命令, 347
- ping 命令, 408
- printmail 命令, 351
- 管道 符号, 13
- 优先级 (priorities), 107
- 管道 (pipes), 14
- 命令 (commands), 27
- 像素 (pixmaps), 130–131
- 进程 (processes), 118–119
- 进程 (processes)，绘图数据, 28
- 进程 (processes), 90, CPU 时间使用, 28
- 进程 (processes)，结束, 28
- Pnews 命令, 348
- popclient 命令, 349–350
- ID (ID), 28
- 发帖新闻文章, 27, 348
- 杀死 (killing), 92–93, 93
- 状态 (status), 20
- printenv 命令, 104, 修改, 195–198
- printf 命令, 292
- 模式 (mode), 27
- 打印 (printing), 230
- 属性 (properties), 181
- 代理 (proxies), 120
- ps 命令, 104
- pwd 命令, 230

### Q
- 查询，DNS 服务器, 22

### R
- rb 命令, 104–105
- rclock 命令, 105
- rpc 命令, 409
- rdjpcm 命令, 106
- 读取电子邮件, 26, 347
- 读取文件, 244–246
- 读取消息，新闻组, 27
- readmsg 命令, 353–354
- reconfig 命令, 106
- RECOVER DOS 命令, 34
- reset 命令, 107
- 重定向 (redirection), 13
- resize 命令, 107–108
- 重定向符号 (redirection symbols), 13
- 资源数据库 [X], 28, 173–175
- ref 命令, 388
- refer 命令, 293
- 刷新屏幕 (refresh screen), 28, 175–176
- RENAME DOS 命令, 34
- 重命名 (renaming),- 24, 425
- RESTORE DOS 命令, 34



## 索引 455

- 恢复文件名, Linux, 228
- 获取电子邮件, 26
- rev 命令, 293
- 翻转文件行, 293
- 富文本，显示, 354-355
- richtext 命令, 354-355
- login 命令, 409-410
- rm 命令, 9, 231
- rmail 命令, 354-355
- rmdir 命令, 231
- RMDIR DOS 命令, 34
- mail 命令, 356-357
- 根目录, 10
  - 修改, 28, 199
  - 子目录, 10
  - 窗口, 28
- rpcgen 命令, 388-390
- rsh 命令, 410-411
- rstart 命令, 411-412
- runscript 命令, 108
- runtime 命令, 109
- rusers, 412
- rwall 命令, 413
- rwho 命令, 413
- rx 命令, 109-110
- rxvt 命令, 110-112
- rz 命令, 112
- sb 命令, 113
- sbin 目录, 11
- 扫描器程序，生成, 374
- 扫描函数头, 388
- 计划命令, 20, 21
- 任务调度, 28
- 屏幕
  - 清除, 78
  - 放大, 28, 168
  - 刷新, 28, 175-176
  - 调整大小, 107-108
  - 屏幕截图 (X), 28
- script 命令, 113
- sdiff 命令, 293-295
- 搜索
  - 表达式, 258-259
  - 文件名模式, 220
  - 文件, 23, 28, 205-208, 254-255, 261-262
  - 行, 283
  - 模式, 258-259
  - 字符串, 123-124, 124-125
- whatis 数据库, 62
- sed 命令, 295
- selection 命令, 296-297
- 自解压 zip 文件, 234-235
- 信号量文件, 221
- 串口通信, 99-100

## s

- 保存
  - 击键记录到文件, 25
  - 窗口, 188-189
- 服务器
  - 访问, 158
  - 启动服务器, 397-398
  - DNS, 查询, 22
  - 服务器（续）

## 索引 456

- Tcl 命令外壳, 29
- 字体, 23, 86, 157
  - 类型, 431–432
- FTP, 23, 325
- 变量, 432–434
- Internet，启动, 24
- X Window System, HFS 卷
  - 启动, 23
  - 操作, 24
  - 邮件, 24, 26
- shell, 189
- NNTP, 331
- shelltool 命令, 116
- X Window System, 性能, 29
- SHIFT DOS 命令, 34
- showaudio 命令, 357
- Session Manager [X], 179
- showexternal 命令, 357
- 启动, 28
- showfont 命令, 117–118
- 代理, 120
- shownonascii 命令, 358
- 测试, 180
- showpartial 命令, 358
- SET DOS 命令, 34
- showpicture 命令, 359
- SETVER DOS 命令, 34
- showrgb 命令, 118
- seseyon, 113–114
- 关, 29
- size 命令, 232
  - 大小，文件，列出, 232
- 影子密码，启用/禁用, 29
- skill 命令, 118–119
- shar 命令, 114–116
- Slackware
  - shar 文件，解包, 134
  - 安装, 29
  - 包, 24, 27
- SHARE DOS 命令, 34
- shell
  - sleep 命令, 119
  - 存档, 29, 114–116
  - ash shell, 52
  - Bourne Again, 65
  - C Shell, 79
  - C, 131
  - 修改, 29, 77–78
  - HFS, 运行, 214–215
  - 启动, 24, 29
  - 远程, 410–411
  - 在同一窗口中运行, 29
  - 拆分为两个窗口, 121
  - slip，登录, 414
  - login 命令, 414
  - snice 命令, 119–120
  - sockdown 命令, 414
  - socket 信息, 402
  - sort 命令, 297–298
  - SORT DOS 命令, 34
  - 排序文件，合并, 25
  - 结构, 5-16
  - 行, 29-297
  - 从制 转换为空格, 257
  - 特殊文件, GNU, 228
  - 拼写, 29, 268
  - split 命令, 298-299
  - splitmail 命令, 359-360
  - subst 命令, 128-129
  - splitvt 命令, 121
  - sx 命令, 129
  - sq 命令, 130
  - Spreadsheet [X], 180-181
  - 启动, 29
  - 符号形式, 195-196
  - 标准 I/O (输入/输出), 11–14
  - 启动, 25
  - 统计，网络, 27
  - 系统调用, 29, 122–123
  - 系统信息, 135, 136–137
  - 系统加载信息, 29, 132–133
  - 系统消息, 413
  - 系统关机, 414
  - 系统用法, 29
  - sz 命令, 131
  - strip 命令, 390-391
  - 从对象文件剥离, 390-391
  - 内核，重建, 25
  - 模块, 25
  - 文本, 123-124, 124-125
  - 从制表转换为空格, 257
  - 字符串, 123-124
  - syncgroups, 311–313
  - 同步新闻组, 27, 30, 311

## 索引 458

- tac 命令, 299-300
- 启动, 255-256, 305
- 标签文件, 373, 374
- pico, 289-290
- tail 命令, 300
- talk 命令, 415
- vim, 303-304
- 磁带驱动，控制, 27
- 任务，调度, 28
- 编辑, 22
- 文本格式化, 23
- Tcl 命令外壳, 29, 139
- tcsh 命令, 131
- tee 命令, 132
- head, 20
- telnet 命令, 415
- telnet 连接, IBM 3270
- 制表符转换, 302
- 单词，计数, 304
- 文本处理命令, 243–308
- Textinfo, 91-95
- textinfo 信息, 29, 设置, 29, 125–127
- 终端仿真，360-361
- Terminal Emulator [X], 182-183
- 终端模式，鼠标, 27
- TIME DOS 命令, 34
- test 命令, 233
- tload 命令, 132–133
- TeX, 29
- top 命令, 133
- tr 命令, 301
- 跟踪系统调用, 122–123
- 从 C 程序中提取, 296-297, 391-392
- Pascal 翻译为 C, 385–387
- 富文本, 354–355
- TREE DOS 命令, 34
- 搜索文件, 254-255
- trivial FTP, 启动, 360
- 搜索字符串, 261-262
- trn 命令, 360-361
- 下划线, 134
- troff 命令, 301
- true 命令, 133

## 索引 459

- TYPE DOS 命令, 34
- 打字机输出, 265-266
- 谁登录, 415
- users 命令, 135
- 下划线文本, 134
- 工具程序，配置, 426
- 视频模式, 184
- 视图，多线程, 360-361
- 视觉文本编辑器, 303

## 索引 470

- UNDLETE DOS 命令, 34
- UNFORMAT 命令, 34
- UNIX, 从 DOS 转换, 208
- UPS, 234
- Usenet. 另见
- users 命令, 135
- user 命令, 302
- unexpand 命令, 334
- unshare 命令, 362
- ucode 命令, 361
- uniq 命令, 302
- unix 命令, 362
- updated 命令, 334
- uptime 命令, 135
- upzip 命令, 334
- us 文件, 234
- 验证, 360
- 卷, 218
- vrfy 命令, 362-363
- workman 命令, 140
- writing 命令, 416
- World Wide Web. 另见

## 索引 471

- 原子, 166
- ，列出, 166
- 缓冲区, 150
- 剪贴板, 147
- 命令行选项, 15–17
- 调色板, 181
- 控制台控制, 149
- cut, 150
- cutsel 命令, 150
- ddm 命令, 151-152
- dpyinfo 命令, 152-153
- 显示, 22, 163
- 显示管理器, 151-152
- 显示信息, 152
- 事件, 153
- 眼睛, 24
- 154
- 文件管理器，启动, 236-237
- 字体, 155, 167–168
- 分形, 156
- 图形演示, 157
- 初始化器, 160–161
- 键映射，修改, 25, 170
- 启动, 30

## 索引 472

- w 命令, 136–137
- wc 命令, 304
- Web 浏览, 332–336
- whatis 数据库，搜索, 62
- whatami 命令, 138
- who 命令, 138
- wish 命令, 139
- 窗口, 172, 188-189
- newmail 命令, 363
- 单词，计数, 22
- 文本文件，计数, 304
- 工作目录, 139–140
- 打印, 216–217, 230

## 索引 473

- xargs 命令, 144-145
- xauth 命令, 145-146
- xdiff 命令, 363-364
- xcalc 命令, 146
- xclipboard 命令, 147
- xclock 命令, 147-148
- xmap 命令, 148
- xcmsdb 命令, 149
- xconfig 文件, 106
- xconsole 命令, 149-150
- XCOPY DOS 命令, 34
- xdm 命令, 151-152
- xedit 命令, 305
- xev 命令, 153
- xeyes 命令, 154
- x86config 命令, 154
- Xf86config 文件，生成, 30
- xf86config 文件，生成, 154
- xfd 命令, 155
- xfilemanager 命令, 236-237
- xfm 命令, 237
- xfontsel 命令, 155
- xfractint 命令, 156
- xfs 命令, 238
-237, 237
- xgc 命令, 157
- xgettext 命令, 391-392
- xhost 命令, 158
- x11perf 命令, 141-143
- xierperf 命令, 158-160
- x11perfcomp 命令, 143-144
- xinit 命令, 160-161



## 462 索引

- xkill 命令, 161–162
- xload 命令, 162
- xlock 命令, 163–165
- xlogo 命令, 165
- xlsatoms 命令, 166
- xlsclients 命令, 166–167
- xlsfonts 命令, 167–168
- xmag 命令, 168
- xman 命令, 168–169
- xmessage 命令, 169–170
- hmh 命令, 364
- xkmkf 命令, 392
- Xmodem, 30, 109–110
  - 文件, 发送, 129
- xmodmap 命令, 170
- xon 命令, 171
- xpaint 命令, 171–172
- xpmroot 命令, 172
- xpropro 命令, 172–173
- xrdb 命令, 173–175
- xrefresh 命令, 175–176
- xset 命令, 176–178
- xsetroot 命令, 178–179
- xsm 命令, 179
- xsmclient 命令, 180
- xspread 命令, 180–181
- xstcdmap 命令, 181
- xterm 命令, 182–183
- xv 命令, 183–184
- xvidtune 命令, 184
- xvipictoppm 命令, 185
- xwd 命令, 185–186
- xwininfo 命令, 186–188
- xwud 命令, 188–189
- xxdb 命令, 392–393

## Y

- yacc 命令, 393
- yes 命令, 189
- Ymodem, 30, 104–105, 113
- yytalk 命令, 417

## Z

- Z shell, 189, 431
- zcat 命令, 238–239
- zcmp 命令, 305
- zdiff 命令, 306
- zegrep 命令, 306
- zzfgrep 命令, 307
- zforce 命令, 238–239
- zgrep 命令, 307
- Zip 磁盘, 弹出, 25, 100
- Zip 文件, 过滤器, 208–209
- 压缩文件
  - 自解压, 234–235
  - 解压缩, 29, 234
- Zmodem, 112
  - 文件, 发送, 131
- zmore 命令, 308
- znew 命令, 239
- zoo 命令, 240
- zsh 命令 (Z shell), 845

## 备注

## 备注

## 备注

## my2cents.idgbooks.com

## 注册本书 —— 赢奖！

访问 http://my2cents.idgbooks.com 注册本书，我们将自动让您参加我们精彩的月度抽奖活动。这也是向我们提供反馈的机会：让我们知道您对这本书的看法，以及您希望看到哪些其他主题的内容。

## 在线探索 IDG 图书！

IDG Books Online 网站是您处理技术问题时的在线资源——无论是在家里还是办公室。IDG Books Online 网站经常更新，提供独家软件、内幕消息、在线书籍和现场活动！

## 您可以在 www.idgbooks.com 做的 10 提高生产力并提升职业的事

1. 为您自己的编程项目获取源代码。
2. 下载软件。
3. 阅读网络独家内容：来自 IDG Books 全球作者的特别文章和书籍节选。
4. 利用资源帮助您作为 Novell 或微软专业人士晋升。
5. 购买 IDG Books 全球书籍，或寻找出售这些书的方便书店。
6. 注册您的书籍并赢奖。
7. 与作者在线聊天。
8. 订阅我们最新书籍的定期邮件更新。
9. 建议您想阅读或编写的书。
10. 就我们的书籍和网站提供您的宝贵见解（2美分建议）。

您还没有上网吗？通过 IDG Books 开始非常简单！在当地零售商处即可开启互联网之旅。

## LINUX 系统
终极购物手册

## 即时 Linux 解决方案
您正赶着完成工作，然后却卡住了。您记不起需要继续执行任务的 Linux 命令。听起来很熟悉吗？《Linux 系统命令》一书将为您解解围——这是一本清晰的一站式参考书，将逐条命令展示如何让 Linux 发挥作用。

## 您的一站式指南：

- Linux 结构及其命令概览
- DOS 命令及其等效命令
- 从 A 到 Z 的 Linux 命令
- KDE 和 GNOME 的命令
- 文件管理命令
- 文本处理命令
- 互联网/电子邮件命令
- 编程命令
- Mtools 命令
- Linux Shell 概述

# 关于作者

Patrick Volkerding 是 Slackware 的创建者，这是一个广受誉的 Linux 发行版。Kevin Reichard 是一位 UNIX/Linux 专家，也是一位多产计算机书籍作者。他们还合作编写了《Linux 配置与安装》，目前已是第四版。

| 读者级别 | 价格 |
| :--- | :--- |
| 全部 | 19.99 美元 |
| Linux | 29.99 加拿大 |
| | 18.99 英镑 |

Linux 是 Linux Inc. 在美国和其他国家的注册商标。M&T Books 标志是 IDG Books Worldwide 的商标。
M&T Books 是 IDG Books Works 旗下品牌，国际 Data Group 旗下，位于 Foster City, CA 94404，美国制造

ISBN 0-7645-4669-4 519999
