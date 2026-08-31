

# Linux 简明指南 (Plain English 系列)

## MIS:Press Slackware 系列

## 引言

欢迎来到*简明 Linux 手册*！无论您是 Linux 新手还是高级 Linux 黑客，我们认为您都会发现本书非常有用。

本书面向所有 Linux 用户：寻求微软/苹果个人计算机操作系统替代方案的好奇用户、希望在办公室或家中使用 UNIX 版本的程序员、需要稳定互联网服务器的网站管理员、需要具备本地和互联网使用工具的稳定操作系统的终端用户、想要搭建 Linux 服务器的网络工程师，以及想要了解更多先进操作系统知识的学生。他们都会很高兴将 Linux 作为他们的操作系统。

### Linux 简史

如今被称为 Linux 的系统最初诞生于芬兰赫尔辛基大学的一个小型学生项目。Linus Torvalds 想要一个小型的类 UNIX 操作系统，于是他开始编写一个。他得到了来自全球各地志愿者的帮助，这些志愿者通过公告板、电子邮件和互联网协作，共同创建了 Linux 操作系统。

这个团队最终创造出了一个相当出色的操作系统，运行良好、非常稳定，可与微软、苹果和 Sun 的产品相媲美。Linux 提供以下特性：

- **多任务处理**—Linux 以类 UNIX 方式原生支持同时运行多个任务（程序）。它还支持抢占式多任务处理，可为不同进程设置优先级。
- **多用户**—许多用户可以同时连接到一台 Linux 服务器。Linux 是当今地球上最经济、功能可能最丰富的多用户操作系统。
- **用户友好**—X Window 系统界面和大量优秀工具使 Linux 易于使用。

如今，Linux 拥有五十万用户，而且这个数字每天都在增长。原因之一是成本—Linux 本身是免费的，只有那些打包 Linux 发行版的公司才会收费（而且很多公司根本不收费）。这些发行版，如 Red Hat Linux，在安装过程和附带工具方面各不相同。您只需付一本书的价格就能获得一个功能完备、强大的操作系统；参见书目中列出的 Slackware 系列图书，这些书附带 Slackware Linux CD-ROM。

虽然本书涵盖所有 Linux 实现，但真正的重点是 Slackware Linux 发行版。有些命令，如`httpd`（Apache Web 服务器）和`pkgtool`（用于更新软件包），并非在所有 Linux 发行版中都能找到。我们在列出 Slackware 特有命令的地方做了标注。

### 获取 Linux

本书不附带 Linux CD-ROM。但是，我们强烈建议您查看 Slackware 系列中的其他书目，这些书都附带 Slackware Linux CD-ROM。您可以在书目部分查看书目列表。

### 自由软件基金会

Linux 是许多热心志愿者的产物，其中许多志愿者也为自由软件基金会贡献了自己的时间。FSF 是一个由 Richard Stallman 领导的理想主义团体，他们相信所有软件都应该是免费的，因此他们向世界发布了大量有用的软件，无论是直接发布还是根据 GNU 许可证发布。

结果是一系列并入 Linux 的 GNU 命令；我们用图标标注了它们。这些 GNU 命令通常是使用最广泛的 UNIX 命令的克隆版本，其设计方式使得 UNIX 的许可方案不会生效。因此，它们非常有用，而且通常工作得很好。（然而，无论自由软件基金会怎么声称，根本不存在什么"GNU Linux"或"基于 Linux 的 GNU 系统变体"这类东西。我们不会卷入 FSF 和 Linux 之间的政治纷争；我们只想指出，Linux 是一个现实存在。）

您可以通过以下方式联系自由软件基金会：

Free Software Foundation

59 Temple Place, Suite 330

Boston, MA 02111-1307

1-617-542-5942 (voice)

1-617-542-2652 (fax)

gnu@prep.ai.mit.edu

http://www.gnu.org/

### 本书使用的约定

我们对本书第5章列出的命令采取了一致的编排方式。所有命令都按相同的方式组织：标题、命令行使用示例、命令用途（较为详细）、命令行选项（通常是全部选项）、命令本身需要进一步输入时的子命令（例如`mail`或`ftp`）、实际使用示例，以及相关命令。我们认为这种一致性将帮助您扩展 Linux 的使用，掌握新的命令和概念。

此外，正文本身遵循以下约定：

- 直接输入 Linux 系统的命令使用等宽字体。
- 新概念用*斜体*文本标记。
- X Window 系统和 GNU 命令用特殊图标标注。

### 联系我们

您可以通过电子邮件给我们写信：*reichard@mr.net*。由于我们收到的电子邮件数量众多，无法保证立即回复。您还可以访问 MIS:Press 专门为 Slackware 系列设立的网站：*http://www.mispress.com/linux/index.html*。

## 1.minsk

## Linux 结构与命令

根据您的背景，Linux 要么是一个极其复杂而难以理解的系统（如果您的背景是 Microsoft Windows 或 Macintosh 世界的话），要么只是另一个简单的、命令行驱动的操作系统（如果您的背景是 MS-DOS 或 UNIX 世界的话）。事实介于两者之间：是的，Linux 有时确实难以理解；是的，即便您正在运行 X Window 系统，它也是围绕命令行构建的。然而，就操作系统而言，Linux 并不比 MS-DOS 或 UNIX 更复杂，而且它实际上拥有一些可与 Windows 和 Macintosh 相媲美的工具。

在您准备深入探索 Linux 操作系统之前，有两条规则会让您的生活更轻松：

- Linux 实际上是一系列小而易于使用的命令的集合。如果您能够简化任务并将它们分解为离散的元素，您几乎可以做任何事情。
- 即使您在使用 XFree86（Linux 版本的图形界面）工作时，您基本上仍然是在使用一系列小而易于使用的命令。

很容易推断出，任何想要掌握 Linux 的人都应该首先渴望掌握其命令结构。这就是本书的用武之地：《*Linux in Plain English*》是一份 Linux 命令结构的清单。但在使用这些命令之前，您需要了解 Linux 如何处理命令，以及如何将命令输入系统。

### 命令行

我们已经提到过，Linux 是一个*命令行驱动*的操作系统。命令通过命令行交给操作系统。当您在屏幕上看到以下内容时，就知道 Linux 已准备好接受命令：

`$`

这可能在您运行*终端*模式时出现在全屏幕上，也可能在您运行 X Window 系统时出现在`xterm`窗口中，如图1.1所示。

`![](img/387edf6ffeb560ccc38b30f5b14659a9_11_0.png)`

*图 1.1 在 X Window 系统中运行的 Xterm。*

美元符号称为*提示符*，它是 Linux 用来告诉您已准备好接受命令的机制。在提示符处，您可以输入单个命令或命令与选项的组合，其总和称为*命令行*。

*命令*就是字面上的意思。无论您在提示符处输入什么，Linux 都会将其解释为命令，即执行某事的指令。您可以直接使用命令来做某事，例如移动和复制文件。您也可以使用命令来运行其他程序，例如`elvis`或`emacs`。Linux 有一套特定的命令，所以如果您输入的内容与其某个命令不匹配，它会告诉您找不到该命令。（您实际上可以在查看目录时看到命令列表，但这有点超前了。）Linux 操作系统中 literally 有数百个命令。

命令有*选项*，用于更好地指定命令的行为。这些选项可以告诉命令仅在特定情况下执行操作。这可以通过一个通用命令及其一些选项来最好地说明。

`ls`命令是最基本、最常用的命令之一。它用于列出当前目录中的文件。单独使用时，它仅仅列出给定目录中的文件，如图1.2所示。

`![](img/387edf6ffeb560ccc38b30f5b14659a9_12_0.png)`

*图 1.2 单独使用 ls 命令。*

这告诉我们这个特定目录包含一个名为`fig1_1.gif`的单个文件。（本章中的文件和目录名称并不重要；您只需要了解调用这些文件和目录的机制，以及它们如何应用于几乎任何 command。）然而，`ls`命令本身仅指向所有用户可访问的文件，以及不以某种方式隐藏的文件。隐藏文件以点（`.`）开头，因此您需要告诉`ls`命令查找所有文件，包括隐藏文件。这是通过*选项*完成的。当我们向`ls`命令添加`-a`选项时，我们会得到所有文件和目录的列表，包括隐藏文件，如图1.3所示。

`![](img/387edf6ffeb560ccc38b30f5b14659a9_13_0.png)`

*图 1.3 向 ls 命令添加 -a 选项。*

将示例更进一步，我们可以要求`ls`命令使用`-l`选项返回当前目录中文件或目录的长列表，如图1.4所示。

`![](img/387edf6ffeb560ccc38b30f5b14659a9_13_1.png)`

*图 1.Qt creator 的界面上有个“添加新文件”的按钮，点击后会弹出文件添加向导。在向导的第一个页面上，有一些文件类型选项，比如“C++ Class”、“Qt Resource File”、“JavaScript File”等。其中有一个选项是“C++ Source File”，它的图标是一个白色的 C++ 字样在蓝色背景上。

我现在正在用 PyQt 实现一个类似的向导界面。我已经用 Qt Designer 设计好了 UI，现在需要编写 Python 代码来实现向导页面的切换逻辑。我已经有了`WizardPage`类和`WizardPage2`类，分别对应向导的第一页和第二页。

在`WizardPage`类的`initializePage()`方法中，我需要根据用户的选择来决定当点击“下一步”按钮时应该进入哪个页面。具体来说，如果用户选择了“C++ Source File”，那么下一步应该进入`WizardPage2`；如果用户选择了其他类型，下一步也应该进入某个特定页面（假设这些页面的类我已经定义好了）。

我的问题是：在 PyQt 中，如何在一个`QWizardPage`的子类中调用`nextId()`方法来动态设置下一步的页面 ID？请提供具体的代码示例，包括如何注册页面和设置默认页面 ID。

背景补充：我使用的是 PyQt5，我的主窗口是一个`QWizard`实例，我已经通过`addPage()`方法添加了`WizardPage`和`WizardPage2`实例。 4 向 ls 命令添加 -l 选项。*

很少有 Linux 命令没有任何选项或参数。第5章列出了所有命令，并用大量篇幅介绍了这些选项。

### 文件

`ls`命令用于列出当前目录或给定目录中的文件。在某些方面，它在 Linux 世界中是一个异类，因为它不直接用于文件，而文件是 Linux 用于组织信息的方法。浏览本书的其余部分时，您会看到绝大多数命令都是与文件结合使用的。

这并不奇怪，因为 Linux 操作系统中的*所有东西都是文件*。您看到 `ls` 命令用于列出目录中的文件，这个命令如此方便的原因就在于 Linux 中的一切都是文件。命令实际上是作为程序被调用的文件。连接到您 PC 的设备实际上在 Linux 操作系统中由文件表示（通常以`dev`开头）。当您打印文件时，您实际上是将文件发送到代表打印机的文件。

在基本层面上，文件不过是存储设备（如硬盘或软盘驱动器）上有组织的区域，由比特组成。比特不过是电子格式中的数字播放器，代表 0 或 1。Linux 操作系统获取这些比特，并以对您和操作系统都可识别的方式对它们进行格式化。没有这种组织，硬盘的内容将只是随机的零和一。这种组织方案称为文件系统。

这就是 Linux 操作系统的主要功能是跟踪和操纵这些文件的原因。`ls`命令的重要性怎么强调都不为过，因为它让您知道文件系统的某一部分在给定时间有哪些文件。这就是为什么 Linux 中最常用的命令涉及在基本层面上操纵文件，例如用于编辑文件的`elvis`、用于删除文件的`del`，以及用于移动文件的`mv`。

文件有四种类型：

- 设备文件
- 目录
- 链接
- 普通文件

下面按其在 Linux 操作系统中的重要顺序逐一解释：

普通文件是 Linux 文件的主力，通常包含由其他程序和操作系统 transient 系统本身操作的数据。普通文件可以是 ASCII 文本文件、某程序的程序（例如供页面排版程序使用的格式化文件，或供数据库管理器使用的数据库文件）、命令文件（包含程序的进一步指令，但以 ASCII 文本形式存储，例如 Perl 或 Tcl 脚本），或可执行程序文件。

- *目录*是表示其他文件信息的文件。Linux 操作系统中的文件按层级存储，文件存放在其他文件的集合中。目录将在本章后面进行解释。
- *设备文件*代表连接到 PC 上的设备。这些设备存储在`/dev`目录中；例如，磁带驱动器由`/dev/st0`表示。
- *链接*是文件系统中代表同一文件的多个名称。链接在 Linux 中并不是什么大问题，除非你在网络环境中工作。链接是旧 UNIX 时代的遗留物，当时硬盘空间非常紧张，用户会共享一个文件，但由于网络的需求，给文件起了不同的名称。

### 目录

正如你之前看到的，目录只是用于存储其他文件的文件。目录对于像 Linux 这样的操作系统来说是绝对必需的。在 Linux 中，每个命令都是一个文件，每个设备都是一个文件，每个程序至少是一个文件（但通常更多）。把所有这些文件加起来，你最终会得到一个乱七八糟的文件系统，有数千个独立的文件。更糟糕的是，Linux 设计用于网络环境，这意味着每个有罪用户都可以访问网络上数千个其他文件，可能在文件服务器上。除非这些文件能以某种层级结构存储，否则没有办法有效地跟踪它们。这就是目录的用武之地。

Linux 中的目录层级结构，你可以将其想象为金字塔，实际上非常简单。有一个*根目录*，它位于金字塔的顶部，用斜杠（`/`）表示。每个目录都是根目录的*子目录*。此外，子目录中还有子目录。

作为用户，你始终"处于"某个目录中。这称为*当前目录*。你的命令提示符通常会显示当前目录的名称（以斜杠开头，表示目录层级从根目录开始）。

标准的 Linux 安装，例如 Slackware Linux，有一套相当可预测的目录集合。当你的当前目录是根目录时，Linux 具有如图 1.5 所示的一组子目录。

`![](img/387edf6ffeb560ccc38b30f5b14659a9_16_0.png)`

*图 1.5 典型 Slackware Linux 安装中的根目录。*

其中一些目录几乎在所有 Linux 和 UNIX 安装中都能找到，例如`etc`、`sbin`、`usr`和`var`。其他目录是 Linux 独有的，例如`boot`、`cdrom`、`mnt`、`proc`和`shlib`。还有一些是面向用户的，例如`root`和`users`。如果你自己安装了 Linux，你可能至少有一个*主目录*（`root`，以 root 用户登录时使用），可能还有两个（比如`users`下的命名目录）。

Linux 有许多用于创建自己目录的命令，这些命令在本书中都会介绍。

### 标准输入/输出和重定向

Linux 拼图中的第三块涉及以*标准输入和输出*台上的文件概念Т标准输入和输出和重定向

Linux 拼图中的第三部分是使用*字面标准输入和输出*（I/O）将命令和文件链接起来。不要被这个技术术语吓倒：标准 I/O 实际上涉及命令行的结构以及命令结果应该发送到哪里。

Linux 与其他所有操作系统一样，需要知道输入将来自哪里以及输出应该发送到哪里。其他操作系统，如 Windows 和 Macintosh，在涉及输入和输出时会做出假设。在某些情况下 Linux 也是如此。但在大多数其他情况下，你需要考虑一下你的工作来自哪里以及它要到哪里去。标准 I/O 背后的基本原理最好通过例子来解释。

`cat`命令是一个非常多功能的命令。它可以用来显示文件内容、向文件添加内容等等。当单独在命令行上运行时，它可以作为一个简单的文本编辑器使用：

```
$ cat
```

光标将转到下一行，然后你可以输入文本。因为你没有指定文本应该去哪里，Linux 和`cat`命令假设输入应该发送到屏幕。输入到屏幕后，它就永久丢失了，因为没有将文本保存到磁盘的机制。大多数 Linux 命令假设标准输入意味着来自键盘的输入，标准输出意味着显示在终端上。在这种情况下，`cat`可以用来提高你的打字技能，但除此之外它没什么用处。

然而，当`cat`与命令行中的文件名结合使用时，它的用途就增加了。将`cat`和文件名结合使用可以在屏幕上显示现有文件，如图 1.6 所示。

`![](img/387edf6ffeb560ccc38b30f5b14659a9_18_0.png)`

> kevin:"$ cat kevin.letter

> 我注意到

> 斯佩利飞轮制造厂

> 实际上与我们的地产线相邻。

> 因此，我们恭敬地请求

> 将该建筑移走。

> kevin:"$

图 1.6 将 cat 与文件结合使用。

`cat`不再使用来自键盘的标准输入，而是使用来自文件的标准输入。文件的内容没有被更改；它们只是被显示在屏幕上。

你可以使用`cat`通过*重定向*符号将按键存储到文件中。这些符号是操作系统的核心部分，用于改变标准 I/O。你可以将`cat`——或者任何其他 Linux 命令，就此而言——与重定向符号结合使用，将其输出重定向到文件。在下面的例子中，`cat`的输出通常会发送到屏幕，但现在被重定向到名为`kevin.report`的文件：

```
$ cat > kevin.report
```

输出逐次按键发送到文件`kevin.report`。键入`Ctrl-D`停止重定向并结束`cat`命令。

重定向可以用于输入和输出。`cat`命令可以通过以下方式被告知将文件复制到新文件名：

```
$ cat kevin.report > pat.report
```

这里，输入是`kevin.report`，输出是`pat.report`。`kevin.report`本身没有任何改变。

有一个单独的重定向符号用于将文本追加到现有文件。在这里，`kevin.report`的内容被追加到名为`pat.report`的现有文件中：




```bash
$ cat kevin.report >> pat.report
```

如果你省略输入文件名，`cat` 会假设应该使用按键来追加。以下命令行允许你直接将按键追加到名为 `kevin.report` 的文件末尾：

```bash
$ cat >> kevin.report
```

实际上有四个重定向符号：

- `>` 用于将命令的输出发送到文件或另一个命令。例如，`cat > file` 用于将 `cat` 命令的输出发送到 `file`。
- `<` 用于将文件或命令的输入发送到命令。例如，`cat < file` 意味着 `cat` 应该使用 `file` 作为输入。
- `>>` 用于将输入追加到现有文件。例如，`cat >> file` 告诉 Linux 将按键追加到名为 `file` 的现有文件中。
- `|` 是管道符号。当你想运行一个命令然后将其输出发送给另一个命令时使用。例如，`cat | grep` 运行 `cat` 命令并将其输出发送给 `grep` 命令，然后运行 `grep` 命令。（我们将在本章后面介绍管道。）

当你查看这些符号时，可能似乎有几种不同的方法可以做同样的事情。确实，`<` 和 `>` 可以根据命令行的结构互换使用。然而，两个符号都是必需的。看起来相似的命令行实际上可能被操作系统以完全不同的方式处理。例如，这个命令行：

```bash
$ cat pat.file
```

在功能上与这个相同：

```bash
$ cat < pat.file
```

然而，这两个命令行实际上是不同的。在第一个中，`pat.file` 是 `cat` 命令的参数。在 Linux 世界中，参数是命令行修饰符，是变量；在这种情况下，参数恰好是一个文件。在第二个例子中，`pat.file` 是 `cat` 命令的输入。

谈到重定向符号，命令行的复杂程度是没有限制的。像下面这样使用两个重定向符的情况并不少见，尤其是在 shell 脚本中：

```bash
$ cat < file1 > file2
```

这告诉 `cat` 使用 `file1` 作为输入，并将输出发送到 `file2`。

### 管道

管道，正如 `|` 所示，仅仅是另一种重定向工具。它的优势在于可以直接与命令配合工作，告诉一个命令使用另一个命令的输出作为输入。其命令使用方式如下：

```bash
$ command1 | command2
```

命令与管道符号的组合称为管道线。管道常用于为打印准备文件时。

### X Window 系统选项

在第五章中有许多 X Window 系统命令。这些命令共享一组共同的命令行选项。为了避免在每个命令中重复列出这些选项，我们将它们统一列在这里。

| 选项 | 用途 |
|---|---|
| `-background red green blue` | 将背景色设置为 `red green blue`。 |
| `-background color` | 使用 `color` 作为窗口背景色。 |
| `-bg color` | 使用 `color` 作为窗口背景色。 |
| `-display host:disp_num` | 连接到指定显示，即在给定 `host` 上的 `disp_num` 编号的 X 服务器（几乎总是 0）。 |
| `-fg color` | 使用 `color` 作为窗口前景色。 |
| `-fn fontname` | 使用指定的 `fontname`。 |
| `-font fontname` | 使用指定的字体。 |
| `-foreground_color red green blue` | 将前景色设置为 `red green blue`。 |
| `-foreground color` | 使用 `color` 作为窗口前景色。 |
| `-geometry WidthxHeight+x+y` | 设置窗口大小（`Width x Height`）和位置（`x+y`）。 |
| `-geometry WidthxHeight` | 设置窗口大小。 |
| `-geometry +x+y` | 设置窗口左上角的位置。 |
| `-height rows` | 以 `rows` 设置基础窗口的高度。 |
| `-position x y` | 以 `x y` 像素设置窗口左上角的位置。 |
| `-reverse` | 反转前景色和背景色。 |
| `-rv` | 反转前景色和背景色。 |
| `-size width height` | 以 `width x height` 像素设置窗口大小。 |
| `-Wb red green blue` | 将背景色设置为 PACKAGE设置为 `red green blue`。 |
| `-Wf red green blue` | 将前景色设置为 `red green blue`。 |
| `-WG WidthxHeight+x+y` | 设置窗口大小（`Width x Height`）和位置（`x+y`）。 |
| `-WG WidthxHeight` | 设置窗口大小。 |
| `-WG +x+y` | 以 `x y` 像素设置窗口左上角的位置。 |
| `-Wh rows` | 以 `rows` 设置基础窗口的高度。 |
| `-Wi` | 以图标形式启动窗口，而不是完整窗口。 |
| `-width columns` | 以 `columns` 设置基础窗口的宽度。 |
| `-Wp x y` | 以 `x y` 像素设置窗口左上角的位置。 |
| `-Wr host:disp_num` | 连接到指定显示，即在给定 `host` 上的 `disp_num` 编号的 X 服务器（几乎总是 0）。 |
| `-Ws width height` | 以 `width x height` 像素设置基础窗口大小。 |
| `-Wt fontname` | 使用指定的 `fontname`。 |
| `-Ww columns` | 以 `columns` 设置基础窗口的宽度。 |

### 简明 Linux

人类不会用计算机术语思考，这正是我们需要这样一本参考书籍的原因。命令往往相当晦涩，其用途并不总是显而易见的。为了促进您的 Linux 学习，我们汇编了这份命令列表，并按关键词和功能进行了分类。您可以查找左栏中以斜体显示的关键词——例如，`print`——然后查看哪些 Linux 命令可以帮助完成该任务。接着前往第五章获取该命令的完整说明。

| 如果你想... | 使用 Linux 命令... |
|---|---|
| 控制服务器访问 | `xhost` |
| 追加文件 | `cat` |
| 了解你的机器架构 | `arch` |
| 创建归档 | `cpio`, `tar` |
| 处理归档 | `ar` |
| ASCII 转位图 | `atobm` |
| 位图转 ASCII | `bmtoa` |
| 在指定时间打印 | `atq` |
| 在指定时间运行命令 | `at` |
| 列出原子 | `xlsatoms` |
| 管理授权信息 | `xauth` |
| 设置背景属性 | `xsetroot` |
| 设置背景图像 | `xpmroot` |
| 打印横幅 | `banner` |
| 显示文件基本名 | `basename` |
| 运行批处理命令 | `batch` |
| 显示文件开头 | `head` |
| 显示文件结尾 | `tail` |
| ASCII 转位图 | `atobm` |
| 位图转 ASCII | `bmtoa` |
| 查看和编辑位图 | `bitmap` |
| 编译 C 程序 | `gcc` |
| 编译 C++ 程序 | `gcc`, `g++` |
| 执行计算 | `bc`, `pname`, `xcalc` |
| 查看日历 | `cal` |
| 清屏 | `clear` |
| 列出运行的客户端 | `xlsclients` |
| 显示剪贴板内容 | `xclipboard` |
| 显示时钟 | `oclock`, `xclock` |
| 显示颜色数据库 | `showrgb` |
| 显示颜色映射 | `xcmap` |
| 设置颜色映射属性 | `xstdcmap` |
| 剪切列 | `cut` |
| 创建列 | `column` |
| 合并文件 | `cat`, `join` |
| 在指定时间运行命令 | `at` |
| 构建命令行 | `xargs` |
| 比较文件 | `cmp`, `diff`, `diff3`, `sdiff`, `zcmp`, `zdiff` |
| 比较压缩文件 | `zcmp`, `zdiff` |
| 比较已排序的文件 | `comm` |
| 比较文本文件 | `diff`, `diff3`, `sdiff` |
| 比较三个文本文件 | `diff3` |
| 编译 C 程序 | `gcc` |
| 编译 C++ 程序 | `gcc`, `g++` |
| 编译 Fortran 程序 | `g77` |
| 压缩可执行文件 | `gzexe` |
| 压缩文件 | `gzip`, `znew` |
| 连接到另一台计算机 | `minicom`, `seyon` |
| 复制文件 | `cp`, `cat` |
| 统计字数 | `wc` |
| 返回当前日期 | `date` |
| 更改系统日期 | `date` |
| 解码文件 | `uudecode` |
| 删除文件 | `rm` |
| 删除目录 | `rmdir` |
| 更改目录 | `cd` |
| 创建目录 | `mkdir` |
| 打印当前目录 | `pwd` |
| 列出磁盘可用空间 | `df` |
| 锁定显示 | `xlock` |
| 查看显示信息 | `xdpyinfo` |
| 查询 DNS 服务器 | `dnsquery` |
| 显示域名 | `dnshostname` |
| 回显输入 | `echo` |
| 编辑文本文件 | `elvis`, `emacs`, `vi`, `vim`, `xedit` |
| 创建电子邮件 | `elm`, `mail`, `metasend`, `pine` |
| 编码电子邮件 | `mimencode`, `mmencode` |
| 格式化电子邮件 | `formail` |
| 通知传入电子邮件 | `biff`, `xbiff`, `wnewmail` |
| 创建多媒体电子邮件 | `metasend` |
| 打印电子邮件 | `printmail` |
| 阅读电子邮件 | `elm`, `mail`, `pine`, `readmsg` |
| 通过电子邮件回复 | `Rmail` |
| 通过 POP 检索电子邮件 | `popclient` |
| 批量发送电子邮件 | `fastmail` |
| 拆分 MIME 电子邮件 | `splitmail` |
| 启动电子邮件服务器 | `imapd`, `sendmail` [1] |
| 编码文件 | `uuencode` |
| 返回环境变量 | `printenv` |
| 设置环境变量 | `env` |
| 查看事件信息 | `xev` |
| 创建 FIFO | `mkfifo` |
| 检查文件 | `cksum` |
| 查找文件 | `find` |
| 更改 finger 信息 | `chfn` |
| 返回 finger 信息 | `finger` |
| 启动字体服务器 | `xfs` |
| 查看字体服务器信息 | `fsinfo` |
| 列出字体 | `fslsfonts`, `showfont`, `xfd`, `Xfontsel`, `xlsfonts` |
| 格式化文件 | `fmt`, `groff` |
| 格式化软盘 | `fdformat` |
| 编译 Fortran 程序 | `g77` |
| 生成分形 | `xfractint` |
| 启动 FTP 服务器 | `ftpd` |
| 编辑图形 | `xv` |
| 更改组 | `chgrp`, `newgrp` |
| 查看在线帮助 | `apropos`, `info`, `man`, `whatis`, `Xman` |
| 返回主机信息 | `host` |
| 设置主机名 | `hostname` |
| 查看键盘信息 | `dumpkeys`, `kdb_mode` |
| 修改键盘映射 | `xmodmap` |
| 保存击键到文件 | `script` |
| 查看关键词信息 | `whatis` |
| 编辑图像 | `xv` |
| 启动 IMAP 邮件服务器 | `imapd` |
| 启动 Internet 服务器 | `inetd` |
| 连接已排序的文件 | `join` |
| 链接文件 | `ln` |
| 列出文件 | `dir`, `ls` |
| 锁定显示 | `xlock` |
| 远程登录 | `rlogin` |
| 登录系统 | `login` |
| 查看登录名 | `logname` |
| 创建电子邮件 | `elm`, `mail`, `metasend`, `pine` |
| 编码电子邮件 | `mimencode`, `mmencode` |
| 格式化电子邮件 | `formail` |
| 通知传入电子邮件 | `biff`, `xbiff`, `wnewmail` |
| 创建多媒体电子邮件 | `metasend` |
| 打印电子邮件 | `printmail` |
| 阅读电子邮件 | `elm`, `mail`, `pine`, `readmsg` |
| 通过电子邮件回复 | `Rmail` |
| 通过 POP 检索电子邮件 | `popclient` |
| 批量发送电子邮件 | `fastmail` |
| 拆分 MIME 电子邮件 | `splitmail` |
| 启动邮件服务器 | `imapd`, `sendmail` |
| 列出空闲内存 | `free` |
| 合并文件 | `paste` |
| MIME 编码电子邮件 | `mimencode`, `mmencode` |
| 拆分 MIME 电子邮件 | `splitmail` |
| 更改模式 | `chmod` |
| 挂载磁盘 | `mount` |
| 挂载软盘 | `fdmount` |
| 挂载磁带驱动器 | `mt` |
| 移动文件 | `mv` |
| 创建多媒体电子邮件 | `metasend` |
| 列出网络用户 | `rusers` |
| 检查 Usenet 新闻 | `checknews` |

[1] 修正了原文中 “Rnm ail” 为 “Rmail”，以及将 “imapd, sendmail” 放在正确的行中。另外修正了 “fslsfonts, showfont, xfd,升空 Xfontsel, xlsfonts” 中的 “升空” 为 “Xfontsel”（这是 X Window 系统字体选择器的标准名称，“升空”显然是 OCR 误识别）。

| 如果你想... | 使用 Linux 命令... |
|---|---|
| 在 Usenet 发布新闻 | `Pnews`, `postnews` |
| 阅读 Usenet 新闻 | `trn` |
| 列出 Usenet 新闻组 | `getlist` |
| 友好地运行命令 | `nice` |
| 设置选项 | `xset` |
| 更改所有者 | `chown` |
| 显示 X 像素图 | `sxpm` |
| 分区驱动器 | `fdisk` |
| 更改密码 | `passwd` |
| 更改权限 | `chmod` |
| 通过 POP 接收电子邮件 | `popclient` |
| 查看 PostScript 文件 | `ghostview` |
| 在特定时间打印 | `atq` |
| 打印电子邮件 | `printmail` |
| 打印文件 | `lpr` |
| 准备文件以便打印 | `pr` |
| 删除打印作业 | `lprm` |
| 查看进程状态 | `ps`, `w` |
| 结束进程 | `kill`, `killall`, `xkill` |
| 重新设置进程优先级 | `snice` |
| 返回进程 ID | `pidof` |
| 列出占用 CPU 时间最多的进程 | `top` |
| 显示 X 属性 | `xprop` |
| 刷新屏幕 | `xrefresh` |
| 删除文件 | `rm` |
| 删除目录 | `rmdir` |
| 设置 X 资源数据库 | `xrdb` |
| 列出 X 资源 | `appres`, `listres`, `viewres` |
| 反转文件行 | `rev` |
| 设置 root 属性 | `xsetroot` |
| 设置 root 图像 | `xpmroot` |
| 更改 root 目录 | `chroot` |
| 计划任务 | `cron` |
| 清除屏幕 | `clear` |

| 如果你想... | 使用 Linux 命令... |
|---|---|
| 放大屏幕 | `xmag` |
| 刷新屏幕 | `xrefresh` |
| 创建屏幕截图 | `xwd`, `xv` |
| 显示屏幕截图 | `xwud`, `xv` |
| 搜索文件 | `egrep`, `fgrep`, `grep` |
| 搜索压缩文件 | `zegrep`, `zfgrep`, `zgrep` |
| 启动会话管理器 | `xsm` |
| 控制服务器访问 | `xhost` |
| 查看 X 服务器性能 | `x11perf` |
| 比较 X 服务器性能 | `x11perfcomp` |
| 更改你的 shell | `chsh` |
| 创建 shell 归档 | `shar` |
| 解包 shell 归档 | `unshar` |
| 在两个窗口中运行两个 shell | `splitvt` |
| 跟踪信号 | `strace` |
| 排序文件 | `sort` |
| 检查拼写 | `ispell` |
| 分割文件 | `csplit`, `split` |
| 启动电子表格 | `pname`, `xspread` |
| 跟踪系统调用 | `strace` |
| 显示系统使用率 | `uptime`, `w` |
| 显示系统负载 | `tload`, `xload` |
| 显示系统统计信息 | `systat` |
| 创建磁带归档 | `cpio`, `tar` |
| 挂载磁带驱动器 | `mt` |
| 运行 Tcl 命令 shell | `wish` |



# Linux 命令参考

## 1. 常用命令速查表

| 如果你想... | 使用 Linux 命令... |
| --- | --- |
| 与另一台计算机远程通信 | `minicom`, `seyon` |
| 启动终端仿真器 | `rxvt`, `xterm` |
| 更改终端设置 | `stty` |
| 查看 texinfo 信息 | `info` |
| 在二进制文件中查找文本 | `strings` |
| 编辑文本文件 | `elvis`, `emacs`, `vi`, `vim`, `xedit` |
| 跟踪系统调用 | `strace` |
| 传输文件 | `ftp`, `tftp` |
| 将数据发送到两个文件 | `tee` |
| 确定文件*类型* | `file` |
| *卸载*文件系统 | `umount` |
| *解压*文件 | `gunzip`, `gzip`, `zcat` |
| *解压* zip 文件 | `unzip` |
| 检查 Usenet *新闻* | `checknews` |
| 在 Usenet 发布*新闻* | `Pnews`, `postnews` |
| 阅读 Usenet *新闻* | `trn` |
| above | `getlist` |
| 列出*用户*信息 | `who`, `rwho` |
| 切换*用户* | `su` |
| 列出已登录*用户* | `users` |
| 列出网络*用户* | `rusers` |
| 返回环境*变量* | `printenv` |
| 设置环境*变量* | `env` |
| 配置*显卡* | `SuperProbe` |
| 查看*文件* | `cat`, `less`, `more` |
| 查看压缩*文件* | `zmore` |
| 搜索 *whatis* 数据库 | `apropos` |
| 设置页面*宽度* | `fold` |
| 显示*窗口*信息 | `xwinfo` |
| 统计*字数* | `wc` |
| 浏览万维网 | `lynx` |
| 启动万维网服务器 | `httpd` |
| 启动 X Window 系统 | `startx` |
| 生成 XF86Config 文件 | `Xf86config` |
| 通过 xmodem 接收 | `rx` |
| 通过 xmodem 发送 | `sx` |
| 通过 ymodem 接收 | `rb` |
| 通过 ymodem 发送 | `sb` |
| 通过 zmodem 接收 | `rz` |
| 通过 zmodem 发送 | `sz` |

## 2. Linux/DOS 交叉参考

DOS 和 Linux 之间的相似性比你想象的要多——DOS 和 Linux 都源于 UNIX，而且在大多数情况下，命令和文件系统在三种操作系统中的工作方式相同。如果你的背景是 DOS，你肯定可以过渡到 Linux。本章列出了一些常用的 DOS 命令及其 Linux 对应命令。

| DOS 命令 | Linux 命令 |
| --- | --- |
| `APPEND` | 无 |
| `ASSIGN` | 无 |
| `ATTRIB` | `chmod` |
| `BACKUP` | `cpio`, `tar` |
| `BREAK` | 无 |
| `CALL` | `exec` |
| `CD` | `cd` |
| `CHCP` | 无 |
| `CHDIR` | `cd` |
| `CHKDSK` | `e2fsck` |
| `CHOICE` | 无 |
| `CLS` | `clear`, `reset` |
| `COMMAND` | `bash`, `csh`, `sh` |
| `COMP` | `cmp`, `diff`, `diff3`, `sdiff` |
| `COPY` | `cp`, `cat` |
| `CTTY` | `stty` |
| `DATE` | `date` |
| `DBLSPACE` | 无 |
| `DEFRAG` | 无 |
| `DEL` | `rm` |
| `DELTREE` | `rmdir` |
| `DIR` | `dir`, `ls` |
| `DISKCOMP` | 无 |
| `DISKCOPY` | 无 |
| `DOSKEY` | `history` (Korn 和 bash shell) |
| `DOSSHELL` | 无 |
| `ECHO` | `echo` |
| `EDIT` | `vi` |
| `EXIT` | 无 |
| `EXPAND` | `gunzip`, `uncompress`, `unpack` |
| `FASTHELP` | `apropos`, `man`, `xman`, `whatis` |
| `FASTOPEN` | 无 |
| `FC` | `cmp`, `diff`, `diff3`, `sdiff` |
| `FDISK` | `fdisk` |
| `FIND` | `find` |
| `FOR` | `for` (shell 命令) |
| `FORMAT` | 无 |
| `GOTO` | `goto` (C shell) |
| `GRAFTABL` | 无 |
| `GRAPHICS` | 无 |
| `HELP` | `apropos`, `man`, `whatis` |
| `IF` | `if` (shell 命令) |
| `INTERLNK` | 无 |
| `INTERSVR` | 无 |
| `JOIN` | 无 |
| `LABEL` | 无 |
| `LOADFIX` | 无 |
| `LOADHIGH` | 无（谢天谢地） |
| `MEM` | `free` |
| `MIRROR` | 无 |
| `MKDIR` | `mkdir` |
| `MODE` | `stty`, `tty` |
| `MORE` | `less`, `more`, `xmore` |
| `MOVE` | `mv` |
| `MSAV` | 无 |
| `MSBACKUP` | `cpio`, `tar` |
| `MSD` | 无 |
| `NLSFUNC` | 无 |
| `PATH` | `env` |
| `PAUSE` | `sleep` |
| `POWER` | 无 |
| `PRINT` | `lpr` |
| `PROMPT` | `PS1` |
| `RECOVER` | 无 |
| `REM` | `#` |
| `RENAME` | `cat` |
| `REPLACE` | 无 |
| `RESTORE` | `cpio`, `tar` |
| `RMDIR` | `rmdir` |
| `SET` | `env` |
| `SETVER` | 无 |
| `SHARE` | 无 |
| `SHIFT` | 无 |
| `SMARTDRV` | 无 |
| `SORT` | `sort` |
| `SUBST` | 无 |
| `SYS` | 无 |
| `TIME` | `date` |
| `TREE` | 无 |
| `TYPE` | `cat`, `less`, `more` |
| `UNDELETE` | 无 |
| `UNFORMAT` | 无 |
| `VER` | `uname` |
| `VERIFY` | 无 |
| `VOL` | 无 |
| `VSAFE` | 无 |
| `XCOPY` | `cp` |
| `XTREE` | `mkdir` |

## 3. Linux 命令 A 到 Z

以下是第 5 章中描述的命令的字母顺序列表。这并不构成完整的 Linux 命令集——请查看在线手册和 info 页面以获取完整信息——但它确实列出了你最常用的命令。

| 命令 | 章节 |
| --- | --- |
| `ansi2knr` | 编程命令 |
| `answer` | 互联网/电子邮件命令 |
| `appres` | 通用命令 |
| `apropos` | 通用命令 |
| `ar` | 编程命令 |
| `arch` | 通用命令 |
| `as` | 编程命令 |
| `at` | 系统管理命令 |
| `atq` | 系统管理命令 |
| `atrm` | 系统管理命令 |
| `atobm` | 通用命令 |
| `audiocompose` | 互联网/电子邮件命令 |
| `audiosend` | 互联网/电子邮件命令 |
| `banner` | 通用命令 |
| `basename` | 文件管理命令 |
| `bash` | 通用命令 |
| `batch` | 系统管理命令 |
| `bc` | 通用命令 |
| `bdftopcf` | 通用命令 |
| `biff` | 互联网/电子邮件命令 |
| `bison` | 编程命令 |
| `bitmap` | 通用命令 |
| `bmtoa` | 通用命令 |
| `bpe` | 文本处理命令 |
| `cal` | 通用命令 |
| `cat` | 文本处理命令 |
| `cc` | 编程命令 |
| `cd` | 文件管理命令 |
| `checknews` | 互联网/电子邮件命令 |
| `chgrp` | 文件管理命令 |
| `chmod` | 文件管理命令 |
| `chown` | 文件管理命令 |
| `chroot` | 文件管理命令 |
| `chsh` | 通用命令 |
| `cksum` | 通用命令 |
| `clear` | 通用命令 |
| `cmp` | 文本处理命令 |
| `colcrt` | 通用命令 |
| `colrm` | 文本处理命令 |
| `column` | 文本处理命令 |
| `comm` | 文本处理命令 |
| `cp` | 文件管理命令 |
| `cpio` | 系统管理命令 |
| `chfn` | 互联网/电子邮件命令 |
| `cpp` | 编程命令 |
| `cron` | 系统管理命令 |
| `csh` | 通用命令 |
| `csplit` | 文本处理命令 |
| `ctlinnd` | 系统管理命令 |
| `ctags` | 编程命令 |
| `cut` | 文本处理命令 |
| `date` | 通用命令 |
| `diff` | 文本处理命令 |
| `diff3` | 文本处理命令 |
| `dir` | 文件管理命令 |
| `diskd` | 系统管理命令 |
| `diskseek` | 系统管理命令 |
| `df` | 系统管理命令 |
| `dnshostname` | 网络命令 |
| `dnsquery` | 网络命令 |
| `du` | 系统管理命令 |
| `dumpkeys` | 通用命令 |
| `echo` | 通用命令 |
| `egrep` | 文本处理命令 |
| `elm` | 互联网/电子邮件命令 |
| `elvis` | 文本处理命令 |
| `emacs` | 文本处理命令 |
| `env` | 通用命令 |
| `etags` | 编程命令 |
| `expand` | 文本处理命令 |
| `fastmail` | 互联网/电子邮件命令 |
| `faucet` | 网络命令 |
| `fdformat` | 系统管理命令 |
| `fdisk` | 系统管理命令 |
| `fdmount` | 系统管理命令 |
| `fdrawcmd` | 系统管理命令 |
| `fgrep` | 文本处理命令 |
| `file` | 文件管理命令 |
| `find` | 文件管理命令 |
| `finger` | 互联网/电子邮件命令 |
| `flex` | 编程命令 |
| `fmt` | 文本处理命令 |
| `fold` | 文本处理命令 |
| `formail` | 互联网/电子邮件命令 |
| `free` | 系统管理命令 |
| `frm` | 互联网/电子邮件命令 |
| `fsinfo` | 通用命令 |
| `fslsfonts` | 通用命令 |
| `fstobdf` | 通用命令 |
| `ftp` | 互联网/电子邮件命令 |
| `ftpcount` | 互联网/电子邮件命令 |
| `ftpd` | 系统管理命令 |
| `ftpwho` | 系统管理命令 |
| `funzip` | 文件管理命令 |
| `fuser` | 网络命令 |
| `g77` | 编程命令 |
| `gawk` | 编程命令 |
| `gcc` | 编程命令 |
| `getfilename` | 文件管理命令 |
| `getkeycodes` | 通用命令 |
| `getlist` | 互联网/电子邮件命令 |
| `getpeername` | 网络命令 |
| `ghostview` | 文本处理命令 |
| `gprof` | 编程命令 |
| `grep` | 文本处理命令 |
| `grodvi` | 文本处理命令 |
| `groff` | 文本处理命令 |
| `grolj4` | 文本处理命令 |
| `grops` | 文本处理命令 |
| `grotty` | 文本处理命令 |
| `gunzip` | 文件管理命令 |
| `gzexe` | 文件管理命令 |
| `gzip` | 文件管理命令 |
| `head` | 文本处理命令 |
| `hose` | 网络命令 |
| `host` | 网络命令 |
| `hostname` | 网络命令 |
| `httpd` | 系统管理命令 |
| `id` | 通用命令 |
| `imake` | 编程命令 |
| `imapd` | 系统管理命令 |
| `inetd` | 系统管理命令 |
| `inews` | 系统管理命令 |
| `info` | 通用命令 |
| `injnews` | 系统管理命令 |
| `innd` | 系统管理命令 |
| `ispell` | 文本处理命令 |
| `join` | 文本处理命令 |
| `kdb_mode` | 通用命令 |
| `kill` | 通用命令 |
| `killall` | 通用命令 |
| `less` | 文本处理命令 |
| `lilo` | 系统管理命令 |
| `listres` | 通用命令 |
| `ln` | 文件管理命令 |
| `locate` | 文件管理命令 |
| `locatedb` | 文件管理命令 |
| `lockfile` | 文件管理命令 |
| `login` | 通用命令 |
| `logname` | 通用命令 |
| `look` | 文本处理命令 |
| `lpq` | 文本处理命令 |
| `lpr` | 文本处理命令 |
| `lprm` | 文本处理命令 |
| `ls` | 文件管理命令 |
| `lynx` | 互联网/电子邮件命令 |
| `mail` | 互联网/电子邮件命令 |
| `make` | 编程命令 |
| `makedepend` | 编程命令 |
| `makefloppies` | 系统管理命令 |
| `makestrs` | 编程命令 |
| `makewhatis` | 通用命令 |
| `man` | 通用命令 |
| `manpath` | 通用命令 |
| `mattrib` | Mtools |
| `mbadblocks` | Mtools |
| `mc` | 文件管理命令 |
| `mcd` | Mtools |
| `mcookie` | 通用命令 |
| `mcopy` | Mtools |
| `md5sum` | 系统管理命令 |
| `mdel` | Mtools |
| `mdir` | Mtools |
| `messages` | 互联网/电子邮件命令 |
| `metasend` | 互联网/电子邮件命令 |
| `mformat` | Mtools |
| `mimencode` | 互联网/电子邮件命令 |
| `minicom` | 通用命令 |
| `mkdir` | 文件管理命令 |
| `mkdirhier` | 文件管理命令 |
| `mkfifo` | 文件管理命令 |
| `mkfontdir` | 文件管理命令 |
| `mkmanifest` | 文件管理命令 |
| `mknod` | 文件管理命令 |
| `mlabel` | Mtools |
| `mmd` | Mtools |
| `mmencode` | 互联网/电子邮件命令 |
| `mmount` | Mtools |
| `mmove` | Mtools |
| `more` | 文本处理命令 |
| `mount` | 系统管理命令 |
| `mren` | Mtools |
| `mrd` | Mtools |
| `mread` | Mtools |
| `msgfmt` | 编程命令 |
| `mt` | 系统管理命令 |
| `mtest` | Mtools |
| `mtype` | Mtools |
| `mv` | 文件管理命令 |
| `mwrite` | Mtools |
| `nice` | 通用命令 |
| `newgrp` | 文件管理命令 |
| `nohup` | 通用命令 |
| `nroff` | 文本处理命令 |
| `objcopy` | 编程命令 |
| `oclock` | 通用命令 |
| `passwd` | 通用命令 |
| `paste` | 文本处理命令 |
| `pathchk` | 通用命令 |
| `perl` | 编程命令 |
| `pico` | 文本处理命令 |
| `pidof` | 通用命令 |
| `pine` | 互联网/电子邮件命令 |
| `ping` | 网络命令 |
| `pkgtool` | 系统管理命令 |
| `pname` | 通用命令 |
| `Pnews` | 互联网/电子邮件命令 |
| `popclient` | 互联网/电子邮件命令 |
| `postnews` | 互联网/电子邮件命令 |
| `pr` | 文本处理命令 |
| `printenv` | 通用命令 |
| `printf` | 文本处理命令 |
| `printmail` | 互联网/电子邮件命令 |
| `procmail` | 互联网/电子邮件命令 |
| `ps` | 通用命令 |
| `psbb` | 文本处理命令 |
| `pwd` | 文件管理命令 |
| `quota` | 系统管理命令 |
| `rb` | 通用命令 |
| `rcp` | 网络命令 |
| `rdjpgcom` | 通用命令 |
| `readmsg` | 互联网/电子邮件命令 |
| `readprofile` | 系统管理命令 |
| `reconfig` | 通用命令 |
| `ref` | 编程命令 |
| `refer` | 文本处理命令 |
| `relaynews` | 系统管理命令 |
| `renice` | 通用命令 |
| `reset` | 通用命令 |
| `resize` | 通用命令 |
| `rev` | 文本处理命令 |
| `rexecd` | 系统管理命令 |
| `richtext` | 互联网/电子邮件命令 |
| `rlogin` | 网络命令 |
| `rm` | 文件管理命令 |
| `rmail` | 互联网/电子邮件命令 |
| `rmdir` | 文件管理命令 |



| `rmmod` | 系统管理命令 |  
| `Rnmail` | 互联网/电子邮件命令 |  
| `rpcgen` | 编程命令 |  
| `rsh` | 网络命令 |  
| `rstartd` | 系统管理命令 |  
| `rstart` | 网络命令 |  
| `runscript` | 通用命令 |  
| `ruptime` | 通用命令 |  
| `rusers` | 网络命令 |  
| `rwall` | 网络命令 |  
| `rwho` | 网络命令 |  
| `rx` | 通用命令 |  
| `rxvt` | 通用命令 |  
| `rz` | 通用命令 |  
| `sb` | 通用命令 |  
| `script` | 通用命令 |  
| `sdiff` | 文本处理命令 |  
| `sed` | 文本处理命令 |  
| `selection` | 文本处理命令 |  
| `sendmail` | 系统管理命令 |  
| `sessreg` | 系统管理命令 |  
| `setfdprm` | 系统管理命令 |  
| `setterm` | 系统管理命令 |  
| `seyon` | 通用命令 |  
| `shar` | 通用命令 |  
| `shelltool` | 通用命令 |  
| `showaudio` | 互联网/电子邮件命令 |  
| `showexternal` | 互联网/电子邮件命令 |  
| `showfont` | 通用命令 |  
| `shownonascii` | 互联网/电子邮件命令 |  
| `showpartial` | 互联网/电子邮件命令 |  
| `showpicture` | 互联网/电子邮件命令 |  
| `showrgb` | 通用命令 |  
| `shrinkfile` | 文件管理命令 |  
| `size` | 文件管理命令 |  
| `skill` | 通用命令 |  
| `sleep` | 通用命令 |  
| `sliplogin` | 网络命令 |  
| `smproxy` | 通用命令 |  
| `snice` | 通用命令 |  
| `sockdown` | 网络命令 |  
| `soelim` | 文本处理命令 |  
| `sort` | 文本处理命令 |  
| `split` | 文本处理命令 |  
| `splitmail` | 互联网/电子邮件命令 |  
| `splitvt` | 通用命令 |  
| `sq` | 文件管理命令 |  
| `startx` | 通用命令 |  
| `strace` | 通用命令 |  
| `strings` | 通用命令 |  
| `strings-gnu` | 通用命令 |  
| `strip` | 编程命令 |  
| `stty` | 通用命令 |  
| `su` | 通用命令 |  
| `sum` | 文件管理命令 |  
| `sunst` | 通用命令 |  
| `superformat` | 系统管理命令 |  
| `SuperProbe` | 系统管理命令 |  
| `sx` | 通用命令 |  
| `sxpm` | 通用命令 |  
| `systat` | 通用命令 |  
| `sz` | 通用命令 |  
| `tac` | 文本处理命令 |  
| `tail` | 文本处理命令 |  
| `talk` | 网络命令 |  
| `tee` | 通用命令 |  
| `telnet` | 网络命令 |  
| `telnetd` | 系统管理命令 |  
| `test` | 文件管理命令 |  
| `tftp` | 互联网/电子邮件命令 |  
| `tload` | 通用命令 |  
| `top` | 通用命令 |  
| `tr` | 文本处理命令 |  
| `trn` | 互联网/电子邮件命令 |  
| `troff` | 文本处理命令 |  
| `true` | 通用命令 |  
| `ul` | 通用命令 |  
| `umount` | 系统管理命令 |  
| `unexpand` | 文本处理命令 |  
| `uniq` | 文本处理命令 |  
| `unshar` | 通用命令 |  
| `unsq` | 文件管理命令 |  
| `unzip` | 文件管理命令 |  
| `unzipsfx` | 文件管理命令 |  
| `updatedb` | 文件管理命令 |  
| `uptime` | 通用命令 |  
| `users` | 通用命令 |  
| `uucp` | 网络命令 |  
| `uudecode` | 互联网/电子邮件命令 |  
| `uuencode` | 互联网/电子邮件命令 |  
| `uustat` | 互联网/电子邮件命令 |  
| `uux` | 互联网/电子邮件命令 |  
| `vi` | 文本处理命令 |  
| `viewres` | 通用命令 |  
| `vim` | 文本处理命令 |  
| `vrfy` | 互联网/电子邮件命令 |  
| `w` | 通用命令 |  
| `wc` | 文本处理命令 |  
| `whatis` | 通用命令 |  
| `who` | 通用命令 |  
| `whoami` | 通用命令 |  
| `wish` | 通用命令 |  
| `wnewmail` | 互联网/电子邮件命令 |  
| `write` | 网络命令 |  
| `x11perf` | 通用命令 |  
| `x11perfcomp` | 通用命令 |  
| `xargs` | 通用命令 |  
| `xauth` | 通用命令 |  
| `xbiff` | 互联网/电子邮件命令 |  
| `xcalc` | 通用命令 |  
| `xclipboard` | 通用命令 |  
| `xclock` | 通用命令 |  
| `xcmap` | 通用命令 |  
| `xcmsdb` | 通用命令 |  
| `xconsole` | 通用命令 |  
| `xcpustate` | 通用命令 |  
| `xcutsel` | 通用命令 |  
| `xdfcopy` | 系统管理命令 |  
| `xdm` | 通用命令 |  
| `xdpyinfo` | 通用命令 |  
| `xedit` | 文本处理命令 |  
| `xev` | 通用命令 |  
| `xeyes` | 通用命令 |  
| `xf86config` | 通用命令 |  
| `xfd` | 通用命令 |  
| `xfilemanager` | 文件管理命令 |  
| `xfm` | 文件管理命令 |  
| `xfontsel` | 通用命令 |  
| `xfractint` | 通用命令 |  
| `xfs` | 通用命令 |  
| `xgc` | 通用命令 |  
| `xgettext` | 编程命令 |  
| `xhost` | 通用命令 |  
| `xieperf` | 通用命令 |  
| `xinit` | 通用命令 |  
| `xkill` | 通用命令 |  
| `xload` | 通用命令 |  
| `xlock` | 通用命令 |  
| `xlogo` | 通用命令 |  
| `xlsatoms` | 通用命令 |  
| `xlsclients` | 通用命令 |  
| `xlsfonts` | 通用命令 |  
| `xmag` | 通用命令 |  
| `xman` | 通用命令 |  
| `xmessage` | 通用命令 |  
| `xmh` | 互联网/电子邮件命令 |  
| `xmknmf` | 编程命令 |  
| `xmodmap` | 通用命令 |  
| `xon` | 通用命令 |  
| `xpaint` | 通用命令 |  
| `xpmroot` | 通用命令 |  
| `xrdb` | 通用命令 |  
| `xrefresh` | 通用命令 |  
| `xset` | 通用命令 |  
| `xsetroot` | 通用命令 |  
| `xsm` | 通用命令 |  
| `xsmclient` | 通用命令 |  
| `xspread` | 通用命令 |  
| `xstdcmap` | 通用命令 |  
| `xterm` | 通用命令 |  
| `xv` | 通用命令 |  
| `xvidtune` | 通用命令 |  
| `xvpictoppm` | 通用命令 |  
| `xwd` | 通用命令 |  
| `xwininfo` | 通用命令 |  
| `xwud` | 通用命令 |  
| `xxgdb` | 编程命令 |  
| `yacc` | 编程命令 |  
| `yes` | 通用命令 |  
| `ytalk` | 网络命令 |  
| `zcat` | 文件管理命令 |  
| `zcmp` | 文本处理命令 |  
| `zdiff` | 文本处理命令 |  
| `zegrep` | 文本处理命令 |  
| `zfgrep` | 文本处理命令 |  
| `zforce` | 文件管理命令 |  
| `zgrep` | 文本处理命令 |  
| `zmore` | 文本处理命令 |  
| `znew` | 文件管理命令 |  
| `zoo` | 文件管理命令 |  

## 按组分类的 Linux 命令 5

本节涵盖主要的 Linux 命令，按组和功能分类。八个类别如下：

- 通用命令
- 文件管理命令
- 文本处理命令
- 互联网命令
- 编程命令
- 网络命令
- 系统管理命令
- Mtools

每个命令的格式相同。先给出命令名称，然后是示例命令行、命令说明、可用的命令行选项、示例和相关命令。变量以*斜体*列出。此外，我们还会注明某个命令是否为 GNU 命令或 X Window 系统命令。

---

### 通用命令

这些命令用于日常计算任务。

#### `appres`

##### 列出 X 资源

X Window System 命令

`appres` *class* *toolkitoptions*

## 用途

`appres` 命令列出一个应用程序指定的资源。你可以指定一个通用应用程序，也可以指定一个特定的部件。

输出可能非常庞大，因此你可能需要将输出重定向到另一个文件。

### 示例

```
$ appres XTerm
*mainMenu*interrupt*Label:	Send INT Signal
*mailMenu*logging*Label:	Log to File
*mainMenu*quit*Label:	Quit
...
```

## 相关命令

- `listres`
- `xrdb`

#### `apropos`

##### 搜索 Whatis 数据库

`apropos keyword`

## 用途

`apropos` 命令在 whatis 数据库中搜索有关指定关键字的信息，并将信息返回到默认的 EDITOR 中。whatis 数据库包含命令的简短文本摘要。

### 示例

```
$ apropos xterm
```

`resize (1x) - set TERMCAP and terminal settings to current xterm window size`

`xterm (1x) - terminal emulator for X`

## 相关命令

- `man`
- `whatis`
- `xman`

#### `arch`

## 用途

列出运行 Linux 的 PC 的机器架构。这可能是 `i386`、`i486` 或 `i586`（基于 Pentium 的 PC）。

### 示例

```
$ arch
i586
```

## 相关命令

- `uname`

#### `atobm`

##### 位图转换器

`atobm` *option(s) filename*

## 用途

`atobm` 命令将 ASCII 字符串转换为位图文件。有关 X Window System 位图文件的更多说明，请参阅 `bitmap` 命令。

## 选项

- `-chars` *cc*：设置用于指定位图文件中 0 和 1 的字符。默认使用短横线（`-`）表示 0，井号（`#`）表示 1。
- `-name` *variable*：设置写入转换后的位图文件名时使用的变量名。默认使用命令行参数中的文件名的基本名称。
- `-yhot` *number*：设置"热点"的 Y 坐标。

## 相关命令

- `bitmap`
- `bmtoa`

#### `banner`

##### 打印横幅

`banner option message`

## 用途

`banner` 命令使用星号打印最多 10 个字符的横幅。横幅的总宽度为 132 个字符，横幅为横向打印。

### 示例

```
$ banner kevin
```

## 选项

- `-w num` 设置横幅宽度为 *num* 个字符。

#### `bash`

##### Bourne Again Shell

GNU 命令

`bash` *option(s)*

## 用途

`bash` 命令启动 Bourne Again Shell，这是一个流行的 UNIX shell 的克隆。有关 `bash` 的更多信息，请参阅第 6 章。

#### `bc`

##### 计算器

`bc` *option(s) files*

GNU 命令

## 用途

`bc` 命令用作在线计算器，以及无限精度算术工具。它可以直接输入数字。它可以嵌入到 shell 脚本中，使用类似于 C 编程语言的语法。它还可以用于将数字转换为不同的进制。

在命令行输入 `bc` 命令后，可以直接输入算术函数。使用完 `bc` 命令后，输入 `EOF`、`quit` 或 `Ctrl-C`。

## 选项

- `-l` 添加数学库中的函数。
- `-s` 覆盖扩展，实现 POSIX 一致性。
- `-p` 在使用 POSIX bc 的扩展时打印警告。

### 示例

```
$ bc
scale=5
sqrt((55*6)/5)
8.12402
quit
```

##### 常用指令

| 运算符 | 说明 |
|----------|-------------|
| `+` | 加法。 |
| `-` | 减法。 |
| `/` | 除法。 |
| `*` | 乘法。 |
| `%` | 取余。 |
| `^` | 幂运算。 |
| `sqrt(n)` | 平方根。 |

##### 值存储

- `scale=n`：使用 *n* 位小数设置精度；默认值为 0。最好与十进制一起使用。默认值还意味着输出为整数。可以通过单独输入 `scale`（不带值）来查看当前值。对于 10 到 15 之间的数字，使用字母 A–F。
- `ibase=n`：设置输入进制（默认值为 10）。可以通过单独输入 `ibase`（不带值）来查看当前值。对于 10 到 15 之间的数字，使用字母 A–F。
- `obase=x`：设置输出进制（默认值为 10）。可以通过单独输入 `obase`（不带值）来查看当前值。对于 10 到 15 之间的数字，使用字母 A–F。
- `last`：返回最后一个值。对于 10 到 15 之间的数字，使用字母 A–F。

##### 关键字

- `for` (*exp*) [*statements*]：如果 *exp* 为真，则执行 *statements*。
- `if` (*exp*) [*statements*] (`else` [*statements*])：如果 *exp* 为真，则执行 *statement*。也可以与 `else` 扩展一起使用；在这种情况下，将执行备选的 *statements*。
- `while` (*exp*) [*statements*]：如果 *exp* 为真，则重复执行 *statement*。
- `break`：结束 `for` 或 `while` 语句。
- `continue`：跳转到 `for` 语句的下一次迭代。这是 GNU 扩展。
- `define` *a*(*b*)：定义函数 *a*，参数为 *b*。

##### GNU 扩展

- `halt`：停止 `bc` 命令。
- `limits`：返回 `bc` 命令的本地限制。
- `print` *list*：一个特殊的命令，用于打印一系列特殊字符。*list* 是一个逗号分隔的表达式和字符串列表，按顺序打印。

字符串可以包含特殊字符，包括以下内容：

- `a`：响铃
- `b`：退格
- `f`：换页
- `n`：换行
- `r`：回车
- `q`：双引号
- `t`：制表符
- `\\`：反斜杠

##### 其他运算符和关键字

- **赋值**：`=+` `=-` `=*` `=/` `=^` `=`
- **关系**：`<` `<=` `>` `>=` `==` `!=`
- **一元**：`-` `++` `--`

##### 数学库函数

- `s`：正弦。
- `c`：余弦。
- `a`：反正切。
- `e`：指数；以 *e* 为底。
- `l`：自然对数。
- `j(n,x)`：贝塞尔函数。

##### 其他符号

- `/* */`：注释行。
- `{ }`：括号语句。
- `[ ]`：数组索引。

#### `bdftopcf`

##### 位图字体转换

X Window System 命令

`bdftopcf option(s) fontfile.bdf`

## 用途

`bdftopcf` 命令将字体从 X 位图分发格式（BDF）转换为可移植编译格式（PCF），这种格式更易于 X 字体服务器使用。PCF 字体可以被任何机器读取。

## 选项

- `-i`：禁止计算墨迹度量。跳过计算可以加快处理速度。
- `-l`：将字体位顺序设置为最低有效位（LSB）优先。
- `-L`：将字体字节顺序设置为最低有效位（LSB）优先。
- `-m`：将字体位顺序设置为最高有效位（MSB）优先。
- `-M`：将字体字节顺序设置为最高有效位（MSB）优先。
- `-o outputfile`：指定输出文件的名称。
- `-pn`：字体字形的填充设置为 *n*。每个字形的每条扫描线填充到 1、2、4 或 8 字节。
- `-t`：尽可能将字体转换为"终端字体"。此选项允许字体服务器更快地渲染字体。
- `-un`：将字体扫描线单位设置为 *n*。当字体位顺序与字体字节顺序不同时，需要使用此选项；*n* 可以是 1、2 或 4 字节。

### 示例

```
$ bdftopcf -t -o fontfile.pcf fontfile.dbf
```

#### `bitmap`

##### 位图编辑器

X Window System 命令

```
bitmap option(s) filename basename
```

## 用途



`bitmap`程序用于创建和编辑位图。位图是按网格布局的图像文件，在 X Window System 中用于多种用途，从图标和光标到网页图形元素。它们以实际的 C 代码形式存储，可以直接插入到程序中。

该程序可以为光标指定一个“热点”，告诉窗口管理器光标具体指向的位置，例如箭头的尖端或十字准线的中心。

`basename`用于 C 代码输入文件。

要查看图像的实际显示效果，按`Alt-I`。

该程序实际运行时有大量可用命令，例如反转当前图像和标记位图的一部分。这些命令可通过窗口左侧的按钮使用。

## 选项

- `-size WIDTHxHEIGHT`指定位图网格的大小。

- `-sw` *dimension* 指定正方形的宽度（以像素为单位）。

- `-sh` *dimension* 指定正方形的高度（以像素为单位）。

- `-gt` *dimension* 设置网格容差；如果尺寸大小低于该值，网格将被关闭。

- `-grid` 关闭网格线。

- `+grid` 打开网格线。

- `-axes` 关闭主轴。

- `+axes` 打开主轴。

- `-dashed` 关闭框架和网格线的虚线显示。

- `+dashed` 打开框架和网格线的虚线显示。

- `-stippled` 关闭高亮方块的点状显示。

- `+stippled` 开启高亮方块的点状显示。

- `-proportional` 关闭比例模式，即方块的宽度等于高度。

- `+proportional` 开启比例模式，即方块的宽度等于高度。

- `-dashes *文件名*` 设置要用作虚线点状的位图*文件名*。

- `-stipple *文件名*` 设置要用作高亮点状的位图*文件名*。

- `-hl *颜色*` 设置用于高亮的*颜色*。

- `-fr *颜色*` 设置用于边框和网格线的*颜色*。

## 相关命令

`atobm`

`bmtoa`

### bmtoa

### 位图转换器

X Window 系统命令

`bmtoa` *选项* *文件名*

## 用途

`bmtoa`命令将 X Window 系统位图文件转换为 ASCII 字符串。有关 X Window 系统位图文件的更多信息，请参阅`bitmap`命令。

### 示例

```
$ bmtoa bitmap_file
```

## 选项

`-chars` *cc*

设置用于指定位图文件中 0 和 1 的字符。默认使用短横线（`-`）表示 0，井号（`#`）表示 1。

## 相关命令

`atobm`

`bitmap`

### cal

### 日历

`cal`选项(s) 月 年

## 用途

`cal`命令显示三个月的日历（当前月前后各一个月），或在指定月和年时显示特定月和年的日历，或仅在指定年时显示特定年份 12 个月的日历。年份范围可为 1 至 9999，月份范围可为 1 至 12。

`cal`命令基于英美惯例。要查看格利高里历，请使用命令行`cal 1752`。

### 示例

```
cal
cal 7 1997
cal 1997
cal 1752
```

## 选项

| 选项 | 说明 |
|------|------|
| month | 指定月份。 |
| year | 指定年份。 |
| -j | 返回儒略日，日期编号为 1 至 365（闰年除外）。 |

## 相关命令

`date`

### chsh

### 更改 Shell

`chsh` *选项(s) shell*

## 用途

`chsh`命令更改您的登录 shell。您可以指定一个 shell，或从可用 shell 列表中选择一个。

## 选项

| 选项 | 说明 |
|------|------|
| -l | 列出`/etc/shells`中列出的可用 shell，不做更改。 |
| -s | 指定新的 shell。 |

### 示例

```
$ chsh zsh
```

### cksum

### 校验文件

`cksum` *文件(s)*

## 用途

`cksum`命令对指定的*文件*执行循环冗余校验（CRC），以确保文件未损坏。

### 示例

```
$ cksum CHANGES.TXT
4005661398      2344  CHANGES.TXT
```

### clear

## 用途

`clear`命令清除屏幕，适用于在终端模式下工作时使用。

### 示例

```
clear
```

### colcrt

### 颜色校正

`colcrt` *选项(s)* *文件*

## 用途

`colcrt`命令校正由`tbl`或`nroff`命令生成的转义字符和反向换行的格式。此命令适用于在终端模式下使用 Linux 时。通常不单独使用，而是作为更长命令行的一部分。

## 选项

| 选项 | 说明 |
|------|------|
| - | 关闭下划线。 |
| -2 | 开启双倍行距。 |

### csh

## 用途

`csh`启动 C shell，这是众多 Linux 命令行 shell 之一。有关 shell 的更多信息，请参阅第 6 章。

### date

### 日期

`date`选项 +格式

`date`选项 字符串（用于特权用户）

## 用途

`date`命令显示当前日期和时间。多种格式允许您控制显示格式。特权用户（如 root 用户）可以使用此命令设置系统日期。

## 选项

- `+format`：以特定格式显示日期；格式选项见下一节。

- `-s`：设置日期。此选项仅对特权用户可用。

- `-u`：以世界时（也称为格林威治标准时间 GMT）返回时间。

### 格式

- `%a`：缩写星期几（`Sun`、`Mon` 等）。

- `%A`：完整拼写星期几（`Sunday`、`Monday` 等）。

- `%b`：缩写月份（`Jan`、`Feb` 等）。与`%h`相同。

- `%B`：完整拼写月份（`January`、`February` 等）。

- `%c`：返回特定国家的时间。

- `%d`：以两位数字返回日期（01–31）。

- `%D`：以 `mm/dd/yy` 格式返回日期。

- `%e`：以数字返回日期（1–31）。

- `%h`：缩写月份（`Jan`、`Feb` 等）。与`%b`相同。

- `%H`：以 24 小时制返回小时（00–23）。

- `%I`：以 12 小时制返回小时（00–12）。

- `%j`：以儒略日格式返回日期（1–365）。

- `%k`：以 24 小时制返回小时，不带前导零（1–23）。

- `%l`：以 12 小时制返回小时，不带前导零（1–12）。

- `%m`：以两位数字返回月份（01 表示一月，02 表示二月等）。

- `%M`返回分钟数（0–59）。

- `%n`插入换行符。

- `%p`将时间转换为 a.m. 和 p.m.（区别于默认的 AM 和 PM）。

- `%r`以 12 小时格式返回 *hh:mm:ss:a/pm*。

- `%s`返回自“纪元”1970-01-01 00:00:00 UTC 以来的秒数。

- `%S`返回秒数（0–59）。

- `%t`插入制表符。

- `%T`指定时间以 *hh:mm:ss* 格式返回。

- `%U`返回月份的日期（01–31 出奇，原文可能有误，应为 `%d` 的功能）。

- `%w`以数字返回星期几（星期日为 0）。

- `%W`以数字返回周数（0–51），周一开始。

- `%x`返回特定国家的时间格式。

- `%X`返回特定国家的日期格式。

- `%y`以两位数字返回年份 *(97)*。

- `%Y`以四位数字返回年份 *(1997)*。

- `%Z`返回时区名称。

### 日期设置选项

特权用户还可以使用`date`命令设置系统日期。日期可以是数字或非数字格式。数字字符串必须为 *Mmddhhmmyy* 格式。

### 示例

```
$ date 0101153097
```

这将日期设置为 1997 年 1 月 1 日 *(0101)* *(97)*，下午 3:30 *(1530)*。

### dumpkeys

### 键盘信息

`dumpkeys` *选项(s)*

## 用途

`dumpkeys`命令返回有关当前键盘驱动程序的信息。

## 选项

- `-c`字符集

  指定解释返回值的*字符集*；*字符集*必须是`iso-8859-1`（ASCII 英文；默认值）、`iso-8859-2`、`iso-8859-3`、`iso-8859-4`或`iso-8859-8`。

- `--compose-only`

  返回有关组合键的信息。

- `-f`

  以规范格式打印每个键的完整输出。

- `--funcs-only`

  返回有关功能键的信息。

- `-i`

  打印每个键的有限信息：可接受的键码关键字、可绑定到键的操作数、操作码范围以及 Linux 内核支持的功能键数量。

- `--keys-only`

  返回有关键绑定的信息，不包括字符串定义。

- `-l`

  打印每个键的信息：可接受的键码关键字、可绑定到键的操作数、操作码范围、Linux 内核支持的功能键数量以及支持的操作符号及其数值。

- `-n`

  以十六进制格式返回信息。

### echo

### 回显输入

`echo`选项 字符串

## 用途

`echo`命令将文本或值回显到标准输出，通常是屏幕。它实际上有三个版本：作为 Linux 命令（`/bin/echo`）、作为 C shell 命令和作为 Bourne shell 命令。三者可以互换使用。唯一的区别是 C shell 版本功能更有限，不支持控制字符和此处提到的`-n`选项。

## 选项

| 选项 | 说明 |
|------|------|
| -n | 避免在文本末尾打印换行符。 |

### 控制字符

| 控制字符 | 说明 |
|----------|------|
| \a | 警报（响铃）。 |
| \b | 退格。 |
| \c | 不换行。 |
| \f | 换页。 |
| \n | 换行。 |
| \r | 回车。 |
| \t | 水平制表符。 |
| \v | 垂直制表符。 |
| \\ | 反斜杠。 |
| \nnn | 任意字符的 ASCII 码。 |

### 示例

```
$ echo "Good afternoon!"
```

这将字符串 *Good afternoon!* 打印到屏幕。

```
$ echo "We are testing the printer" | lp
```

这将字符串 *We are testing the printer* 发送到打印机。

## env

### 设置环境

`env option [variable=value] command`

## 用途

`env`命令用于更改环境变量或显示当前环境变量及其值。你的 Linux 系统拥有一组可应用于各种情况的变量；例如，不是每个命令和程序都有自己的文本编辑器，它们大多只是调用`EDITOR`环境变量来使用系统编辑器。其他变量则控制默认 shell、终端类型、命令路径和主目录。

## 选项

- `-`完全忽略当前环境。

- `-i`完全忽略当前环境。

- `u` *variable*

学而思网校

TAL.COM

### fsinfo

### 字体服务器信息

X Window System 命令

```
fsinfo -server *servername*
```

## 用途

`fsinfo`命令返回正在运行的 X Window System 字体服务器的信息。

## 相关命令

- `fslsfonts`

- `xfs`

### fslsfonts

### 列出字体

X Window System 命令

```
fslsfonts *option(s)* *pattern*
```

## 用途

`fslsfonts`命令列出正在运行的 X 字体服务器所提供的字体。你可以列出所有字体（可能数量庞大），也可以使用 *pattern* 来匹配字体，pattern 支持通配符。（如果使用`*`和`?`通配符，必须对它们进行转义。）

## 选项

- `-1`以单列格式输出。

- `-C`以多列格式输出。

- `-l`列出字体属性。

- `-ll`列出字体属性。

- `-lll`作用与`xlsfonts`的`-lll`选项相同。

- `-m`列出每种字体的最小和最大边界。

- `-server` *host:port* 指定 X 字体服务器。

- `-w` *width* 设置输出宽度；默认为 79 个字符。

- `-n` *columns* 设置输出的列数。

- `-u`输出时不排序。

## 相关命令

- `xfs`

- `showfont`

- `xlsfonts`

### fstobdf

### 创建 BDF 字体

`fstobdf *option(s)*`

## 用途

`fstobdf`命令从字体服务器读取 X 字体并生成 BDF 字体。

## 选项

- `-fn` *fontname* — 指定来自 X 字体服务器的字体。

- `-server` *servername* — 指定 X 字体服务器。

## 相关命令

- `xfs`

- `bdftopcf`

- `fslsfonts`

### getkeycodes

### 获取键码

`getkeycodes`

## 用途

`getkeycodes`命令从内核返回扫描码到键码的映射表。

### id

### 个人身份识别

`id *option(s) username*`

## 用途

`id`命令返回关于你自己或其他指定 *username* 的信息。此信息包括用户 ID 和组 ID，以及适用的有效用户 ID 和组 ID。

## 选项

- `-g`仅返回组信息。

- `-G`返回补充组信息。

- `-n`与`-g`、`-G`或`-u`选项一起使用时，返回名称（而非数字）。

- `-r`返回真实用户 ID 和组 ID，而非有效 ID。

- `-u`仅返回用户 ID。

### info

### GNU 命令

```
info option topic
```

## 用途

`info`命令返回关于给定主题的超文本信息，该主题可以是命令或学科。此信息以 GNU texinfo 格式按大纲形式存储；一旦你用某个主题启动了 info，就可以在大纲中上下移动，查看相关主题。如果启动 info 时不指定主题，你将看到 info 的初始界面（存储在`/usr/local/info/dir`中），说明 info 的工作原理以及如何在系统中导航。

## 选项

- `-d directory` — 使用 directory 而非标准 info 目录（`/usr/local/info/dir`）。

- `--dribble file` — 将按键记录到 file 中，然后可以使用`--restore`选项返回到 info 会话中的特定位置。

- `-f file` — 使用 file 而非标准 info 文件。

- `--help` — 显示关于 info 命令的帮助信息。

- `-n node` — 指定要开始阅读的节点。

- `-o file` — 将信息发送到 file 而非标准输出。

- `--restore file` — 运行 file（使用`--dribble`选项创建）。

- `--subnodes` — 显示子主题。

- `--version` — 显示 info 版本。

## 相关命令

- `xman`

### kdb_mode

### 键盘模式

`kdb_mode *option(s)*`

## 用途

`kdb_mode`命令返回当前键盘模式或更改键盘模式。

## 选项

- `-a`将模式设置为 XLATE（ASCII）。

- `-k`将模式设置为 MEDIUM-RAW。

- `-s`将模式设置为 RAW。

- `-u`将模式设置为 Unicode。

### kill

### 终止进程

`kill *option(s)* PID`

## 用途

`kill`命令终止进程 ID（PID）。只有该 PID 的所有者或特权用户（即 root 用户）才能终止进程。

此命令也是`bash`和 C shell 的内置命令，不过在那些 shell 中的工作方式略有不同。

## 选项

- `-l` — 列出进程 ID。

- `-signal` — 指定由`ps -f`或`kill -l`返回的 *信号*。

## 相关命令

- `killall`

- `ps`

### killall

### 终止所有进程

`killall *option(s)* *name*`

## 用途

`killall`命令按名称终止所有进程，无论有多少进程正在使用该命令。要终止正在运行可执行文件的进程，请在命令名中使用 `/`。

## 选项

| 选项 | 描述 |
|------|------|
| -i | 确认是否确实要终止进程。 |
| -l | 列出进程 ID。 |
| -v | 以详细模式运行；列出结果和 ID。 |
| -signal | 指定由`ps -f`或`killall -l`返回的 *信号*。 |

## 相关命令

- `kill`

- `ps`

### listres

### 列出资源

X Window System 命令

`listres *option(s) widget*`

## 用途



`listres`命令返回小部件资源数据库的列表。列出每个资源首次定义的类、实例名和类名，以及每个资源的类型。如果未指定特定小部件或给出`-all`选项，则会打印两列的小部件名称及其类层次结构列表。

## 选项

- `-all` — 返回所有已知小部件和对象的信息。
- `-nosuper` — 忽略从超类继承的资源。
- `-variable` — 按类记录变量的名称（而非类名）来标识小部件。
- `-top *name*` — 指定要作为层次结构顶层的小部件*名称*。
- `-format *printf-string*` — 指定 printf 风格的格式字符串，用于打印每个资源的名称、实例、类和类型。

## login

### 登录系统

`login username option`

## 用途

`login`命令用于登录 Linux 系统。如果未在命令行上指定*username*，`login`命令将提示输入。

该命令执行一些管理操作，例如设置 tty 的 UID 和 GID，以及在有待收邮件时通知用户。root 用户可以设置`login`命令以执行一些基本身份验证（更多信息请查看手册页）。此外，`login`命令可用于指定 root 用户可以登录的位置；`tty`列表位于`/etc/securetty`，由`login`进行检查。其他安全限制可以存储在`/etc/usertty`中。

## 选项

- `-f` 跳过第二次登录身份验证；在 Linux 下无法正常工作。
- `-h` *host* 将远程*主机*的名称传递给`login`；由服务器使用，由超级用户设置。
- `-p` 保留 getty 使用的先前环境。

## logname

### 打印登录名

GNU 命令

`logname *option(s)*`

## 用途

`logname`命令返回调用进程的登录名，该名称在文件`etc/utmp`中查找。如果找不到登录名，将生成错误消息。

## 选项

- `--help` — 打印简短的帮助消息，然后退出。
- `--version` — 打印版本号，然后退出。

## makewhatis

### 构建 Whatis

`makewhatis *option(s) manpath*`

## 用途

`makewhatis`命令构建并更新`whatis`数据库，该数据库供`whatis`和`apropos`命令使用。必须安装 Perl 才能正常工作。

## 选项

- `-u` — 仅用更新的手册页更新数据库。默认是完全重建数据库。
- `-w` — 返回`manpath`。

## 相关命令

- `apropos`
- `man`
- `xman`

## man

### 在线手册页

`man *option(s) section title*`

## 用途

`man`命令格式化并显示在线手册页。这些页面是 Linux 和 UNIX 操作系统的官方文档，采用严格的格式。在查找晦涩的选项和命令时非常有用。

通常，必须将特定命令与`man`命令匹配。然而，你可以开始在各个章节中搜索，并以此来缩小搜索范围。

`man`命令会询问你是否要保存格式化后的页面。保存它们可以在你再次访问`man`页面时节省时间。

## 选项

- `-a`：显示与*title*匹配的所有手册页，而不仅仅是第一个。
- `-c`：重新格式化`man`页面，即使已存在格式化页面。
- `-C` *config_file*：指定要使用的 man.config 文件；默认为`/usr/lib/man.config`。
- `-d`：显示调试信息，而不是实际的`man`页面。
- `-D`：显示调试信息和`man`页面。
- `-f`：以`whatis`命令的方式调用摘要。
- `-h`：打印`man`命令的单行摘要。
- `-k`：与`apropos`命令相同。
- `-m` *system*：在*system*中搜索`man`页面。
- `-M` *path*：指定搜索`man`页面时使用的*path*。默认情况下，使用环境变量 MANPATH。如果未设置，则在`/usr/lib/man.config`中查找列表。
- `-p` *string*：指定在`nroff`或`t roff`之前运行的预处理器。对 Linux 不太适用。
- `-P` *pager*：指定要使用的分页程序；默认为`/usr/bin/less -is`。
- `-S` *section_list*：指定要搜索的*section_list*。
- `-t`：使用`/usr/bin/groff -Tps -mandoc`格式化 man 页面。
- `-w`：显示`man`页面的位置，而不是实际页面。
- `-W`：显示`man`页面的位置，而不是实际页面，每行一个文件名。

## 相关命令

- `apropos`
- `manpath`
- `whatis`
- `xman`

## manpath

### Man 命令的路径

`man *option(s)*`

## 用途

`manpath`命令设置或返回 man 命令的路径。它首先检查`$MANPATH`变量，然后是`/etc/manpath.conf`，最后是用户环境变量和当前工作目录。

## 选项

- `-c` 使用 catpath 查找格式化页面。
- `-d` 打印调试信息。
- `-g` 从`/etc/manpath.conf`中的全局引用创建 MANPATH。
- `-m system` 在 system 中搜索 man 页面。
- `-q` 抑制错误消息。

## 相关命令

- `apropos`
- `man`
- `whatis`
- `xman`

## mcookie

### 生成 Cookie

X Window 系统命令

## mcookie

## 用途

`mcookie`命令为`xauth` X 权限系统创建 magic cookies（具体来说，是一个 128 位的随机十六进制数）。通常直接与`xauth`命令一起使用。

## 相关命令

`xauth`

## minicom

### 串行通信

`minicom *option(s)*`

## 用途

`minicom`命令启动一个串行通信软件包，有点类似于 Telix。它具有自动重拨的拨号目录、对串行设备上 UUCP 风格锁文件的支持、独立的脚本语言解释器、文件捕获、多用户个人配置等功能。

运行`minicom`时，有许多可用的选项和命令。查看在线手册页以获取更多信息；另外，启动`minicom`后也可以自行探索。

有一个 X Window 系统版本`xminicom`可用。它的工作方式与`minicom`相同，只是在 X 窗口中运行。

## 选项

- `-a`：设置属性使用。
- `-c`：设置颜色使用。
- `-d`：启动时直接拨打目录输入。
- `-l`：指定对高位设置的字符进行字面翻译。
- `-m`：用`Alt`（`Meta`）键覆盖命令键。
- `-M`：用`Alt`（`Meta`）键覆盖命令键，假设`Alt`键是字符的第 8 位（发送 128 + 字符代码）。
- `-t`：设置终端类型，覆盖环境 TERM 变量。
- `-o`：跳过初始化。
- `-s`：在设置模式下启动`minicom`，显示配置菜单。（仅适用于 root 用户。）
- `-z`：显示终端状态行。

## 相关命令

`seyon`

## nice

### 以 nice 方式运行命令

GNU 命令

`nice *option* *command* *argument(s)*`

## 用途

`nice`命令允许你为命令设置优先级；如果系统负载较重，命令将不会运行或占用过多系统资源。nice 值可以设置在 15（最低优先级）到 -20（最高优先级）之间，但只有特权用户才能设置负优先级。

如果没有参数，`nice`命令将打印当前调度优先级。

此描述是 GNU 命令，而非`nice` shell 命令。

## 选项

- *-adjustment*

将*adjustment*而不是 10 添加到命令的优先级。

## nohup

GNU 命令

`nohup *command arguments*`

## 用途

`nohup`命令确保在同一命令行上指定的命令不受中断地运行，即使你退出系统。

## oclock

### 圆形时钟

X Window 系统命令

`oclock *option(s)*`

## 用途

`oclock`命令启动一个圆形模拟时钟。

## 选项

- `-fg` *color* — 设置指针和宝石的颜色。
- `-bg` *color* — 设置背景颜色。
- `-jewel` *color* — 设置宝石的颜色。
- `-minute` *color* — 设置分针的颜色。
- `-hour` *color* — 设置时针的颜色。
- `-bd` *color* — 设置窗口边框的颜色。
- `-bw` *width* — 设置窗口边框的宽度。
- `-transparent` — 将时钟精简为宝石、指针和边框。

## 相关命令

`xclock`

## passwd

### 更改密码

```
passwd name password
```

## 用途

`passwd`更改你的密码。你可以直接运行`passwd`，然后系统会提示你输入旧密码和新密码。

新密码必须至少六个字符，且包含大小写字母。

特权用户可以通过在命令行上指定用户名和新密码来更改其他用户的密码。

## pathchk

### 检查路径

GNU 命令

`pathchk *option filename*`

## 用途

`pathchk`命令检查*filename*是否有效（即路径名中的目录是否可搜索）或可移植（满足长度要求）。

## 选项

- `-p`：检查 POSIX 可移植性。

## pidof

### 显示进程 ID

`pidof *option(s) program*`

## 用途

`pidof`命令列出正在运行的程序的进程 ID。通常不会单独使用它，而是在运行级别更改脚本中使用。它实际上是`killall5`命令的链接。

## 选项

- `-s` 仅返回一个 PID。
- `-o` *pids* 省略*p EXPENSES pid。

## 相关命令

- `halt`
- `init`
- `reboot`
- `shutdown`

## pname

### 电子表格计算器

`pname *option(s) filename*`

## 用途

`pname`电子表格计算器的工作方式类似于财务电子表格：你将数据输入到由单元格组成的行和列中，单元格可以包含值、标签字符串或表达式（公式）。计算方式与电子表格相同。

## 选项

- `-c` 以列顺序重新计算的方式启动 pname。
- `-m` 以自动重新计算禁用的方式启动 pname。
- `-n` 以快速数字输入模式启动 pname。
- `-r` 以行顺序重新计算的方式启动 pname。
- `-R` 以自动换行操作设置为递增行的方式启动 pname。
- `-x` 使 Get 和 Put 命令加密和解密数据文件。
- `-C` 以自动换行操作设置为递增持的方式启动 pname。

### 命令

`pname`有一组广泛的命令可供使用。查看在线手册页以获取完整列表。

## printenv

### 打印环境变量

GNU 命令

```
printenv variable
```

## 用途

`printenv`命令用于打印您的环境变量。如果指定一个变量，该命令将返回该变量的信息；如果不指定变量，`printenv`命令将打印所有变量的信息。

## ps

### 查看进程状态

```
ps option(s)
```

## 用途

`ps`命令返回进程的相关信息。该命令有一长串复杂的可用选项；更多信息请查看在线手册页。

## rb

### 接收 Ymodem 文件

```
rb option(s)
```

## 用途

`rb`命令用于通过 Ymodem 传输协议接收文件。

## 选项

- `a` — 去除回车符以及从第一个 Ctrl-Z 开始的所有字符。
- `b` — 二进制文件传输覆盖。
- `D` — 将文件数据输出到`/dev/null`；用于测试。
- `q` — 以静默模式运行。
- `t` *time* — 将超时时间改为*time*个十分之一秒。
- `v` — 以详细模式运行，将文件名列表追加到`/tmp/rzlog`。
- `y` — 覆盖任何同名现有文件。

## rdjpgcom

### JPEG 注释

`rdjpgcom *option jpeg_file*`

## 用途

`rdjpgcom`命令读取*jpeg_file*文件并打印其中的文本注释。JPEG 格式允许"注释"（COM）块，通常用于标注和标题。最大大小为 64K，但文件中没有块数限制。

## 选项

`-verbose`

打印 JPEG 图像尺寸以及注释。

## 相关命令

- `cjpeg`
- `djpeg`
- `wrjpgcom`

## reconfig

### 重新配置 Xconfig

X 窗口系统命令

```
reconfig <Xconfig> XF86Config
```

## 用途

`reconfig`命令将旧的`Xconfig`文件（用于 XFree86 3.1 之前的版本）转换为新的`XF86Config`文件。您需要编辑新的`XF86Config`文件。

## renice

### 更改优先级

`renice *priority who option(s)*`

## 用途

`renice`命令更改一个或多个正在运行的进程的调度优先级。

## 选项

- `-g`

  强制将*who*参数解释为进程组 ID。

- `-p`

  将*who*的解释重置为（默认的）进程 ID。

- `-u`

  强制将*who*参数解释为用户名。

## reset

### 重置终端

```
reset
```

## 用途

`reset`命令重置终端。它会调用多个命令来完成此操作。

## 相关命令

- `reset`
- `stty`
- `tput`

## resize

### 重置终端

X 窗口系统命令

```
resize option(s)
```

## 用途

`resize`命令将 TERM 和 TERMCAP 设置调整为当前`xterm`的大小。要实现这一点，该命令必须是命令行的一部分，或重定向到文件。

- `-u` 生成 Bourne shell 命令，即使 Bourne shell 不是当前 shell。
- `-c` 生成 C shell 命令，即使 C shell 不是当前 shell。
- `-s` *[rows columns]* 使用 Sun 控制台转义序列，而不是`xterm`转义码。如果指定了*rows*和*columns*，`xterm`窗口将被要求调整自身大小。

## runscript

### 运行 Minicom 脚本

`runscript *scriptname*`

## 用途

`runscript`命令是`minicom`终端软件的脚本解释器。通常用于自动登录远程 UNIX 服务器或公告板系统。

脚本中可识别的命令如下：expect、send、goto、gosub、return、exit、print、set、inc、dec、if、timeout、verbose、sleep、break 和 call。实际的脚本语言接近 BASIC，`minicom`源代码附带了两个示例脚本：`scriptdemo`和`unixlogin`。

## 相关命令

`minicom`

## ruptime

### 主机状态

```
ruptime option(s)
```

## 用途

`ruptime`命令显示本地机的主机状态。这是由网络上每台主机每分钟广播的数据包形成的。11 分钟内未收到状态报告的机器将显示为已关闭。

## 相关命令

- `rwho`
- `uptime`

## rx

### 接收 Xmodem 文件

```
rx option(s) filename
```

## 用途

`rx`命令通过 Xmodem 传输协议接收文件。

## 选项

- `a`: 去除回车符以及从第一个 Ctrl-Z 开始的所有字符。
- `b`: 二进制文件传输覆盖。
- `c`: 请求 16 位 CRC。
- `D`: 将文件数据输出到`/dev/null`；用于测试。
- `e`: 强制发送方转义所有控制字符；通常 XON、XOFF、DLE、CR-@-CR 和 Ctrl-X 会被转义。
- `q`: 以静默模式运行。
- `t` *time*: 将超时时间改为*time*个十分之一秒。
- `v`: 以详细模式运行，将文件名列表追加到`/tmp/rzlog`。

## rxvt

### 终端仿真器

X 窗口系统命令

```
rxvt option(s)
```

## 用途



`rxvt` 命令是 X 窗口系统的 VT100 终端仿真器。它实际上是流行的 `xterm` 终端仿真器的精简版本，缺少一些您可能不会想念的 `xterm` 功能（Tektronix 4014 仿真、会话日志和工具包式可配置性）。其优点是 `rxvt` 使用的交换空间比 `xterm` 少得多。如果在内存受限的环境中操作，您可能想考虑从 `xterm` 切换到 `rxvt`。

有关资源的更多信息请参阅 `xterm` 命令，因为 `rxvt` 接受大多数与 `xterm` 相同的资源。

## 选项

- `-7`

  以 7 位模式运行，从键盘输入的所有字符中剥离第 8 位。

- `-8`

  以 8 位干净模式运行，允许键盘输入字符的第 8 位传递给应用程序。

- `-bg color`

  将背景色设置为 `color`。

- `-bigfont keysym`

  将 `Alt-keysym` 设置为增大字体的切换键，而不是默认的 `Alt->`。

- `-C`

  捕获系统控制台消息。

- `-display display-name`

  在指定的 `display-name` 上打开 `rxvt`。

- `-e command [options]`

  启动 `rxvt` 后立即运行命令及其命令行选项。如果使用此选项，它必须是命令行上的最后一个选项。

- `-fat`

  使用粗滚动条，而不是默认的细滚动条。

- `-fg color`

  将前景色设置为 `color`。

- `-font fontname`

  将文本字体设置为 `fontname`。

- `-geometry geometry`

  使用指定的 X `geometry` 打开窗口。

- `-ic`

  以图标化状态启动。

- `-ls`

  在窗口 shell 的 `argv[0]` 前添加 `-`，使其成为登录 shell。

- `-ls-`

  从窗口 shell 的 `argv[0]` 中移除 `-`，使其成为登录 shell。它还告诉 `rxvt` 如果收到响铃字符则保持图标化。

- `-ma`

  如果收到响铃字符，则从图标打开 `rxvt`。

- `-meta string`

  更改 `alt+key` 设置。默认情况下，`rxvt` 在收到 `alt` 按键时发送转义前缀。您可以为 `string` 指定 `escape`、`8thbit` 或 `ignore`。

- `-n text`

  将窗口图标或图标管理器中的名称设置为 `text`。除非同时设置了 `-T` 选项，否则它还将窗口标题栏中的标题设置为 `text`。

- `-pagedown keysym`

  将 `Alt-keysym` 设置为向下滚动一页的切换键，而不是默认的 `Alt-Next_Page`。

- `-pageup keysym`

  将 `Alt-keysym` 设置为向上滚动一页的切换键，而不是默认的 `Alt-Prev_Page`。

- `-secure keysym`

  将 `Alt-keysym` 设置为增大字体的切换键，而不是默认的 `Alt-s`。

- `-sl number`

  保存 `number` 行滚动文本，而不是默认的 64 行。

- `-smallfont keysym`

  将 `Alt-keysym` 设置为减小字体的切换键，而不是默认的 `Alt-<`。

- `-T text`

  将标题栏中的字符串设置为 `text`。

- `-thin`

  无论什么情况都使用细滚动条。

## `rz`

### Receive Zmodem

```text
rs option(s)
```

## 用途

`rz` 命令用于通过 Zmodem 协议接收批量文件。路径名由发送端程序提供，必要时（且可能的情况下）会创建目录。通常，`rz` 命令由调用它的 Zmodem 程序自动发出，但某些有缺陷的 Zmodem 实现可能需要以传统方式启动 `rz`。

## 选项

- `a`：去除回车符以及从第一个 Ctrl-Z 开始的所有字符。
- `b`：二进制文件传输覆盖。
- `D`：将输出文件数据发送至 `/dev/null`；用于测试。
- `e`：强制发送端转义所有控制字符；通常，XON、XOFF、DLE、CR-@-CR 和 Ctrl-X 会被转义。
- `p`：如果目标文件已存在，则跳过该文件。
- `q`：以静默模式工作。
- `t time`：将超时时间改为 `time` 个十分之一秒。
- `v`：以详细模式工作，将文件名列表追加到 `/tmp/rzlog`。
- `y`：覆盖任何同名现有文件。

## `sb`

### Send Ymodem

```text
sb option(s) filename
```

## 用途

`sb` 命令使用 Ymodem 协议将文件发送到另一个系统。该命令有一长串选项；更多信息请参见在线手册页。

## `script`

### 脚本会话

```text
script option filename
```

## 用途

`script` 命令将终端会话中的每个字符保存到指定的文本 `filename` 中。如果未指定 `filename`，则字符将保存到 `typescript` 中。

## 选项

- `-a filename` — 将按键记录追加到现有的 `filename`。

## `seyon`

### 电信

X Window System 命令

```text
seyon option(s)
```

## 用途

`seyon` 命令是一个基于 X Window 的电信软件包，用于连接远程客户端和电子公告板系统。所有选项和命令都存在于界面中，不过在命令行启动 `seyon` 时还可以设置一些额外选项。

该命令支持广泛的资源以及一种脚本语言。更多信息请参见在线手册页。

## 选项

| 选项 | 描述 |
| --- | --- |
| `--` | 将命令行的其余部分传递给终端模拟器。 |
| `-dial` | 覆盖 `dialAutoStart` 资源。 |
| `-emulator terminal-emulator` | 为 `seyon` 指定终端模拟器；如果未指定，则使用 `xterm`。 |
| `-entries entries-list` | 用 `entries-list` 覆盖 `defaultPhoneEntries` 资源。 |
| `-modems device-list` | 覆盖现有的 `modems` 资源。 |
| `-nodefargs` | 不传递终端模拟选项。 |
| `-noemulator` | 告诉 `seyon` 不要启动其自己的终端模拟器。 |
| `-script script` | 在 `seyon` 启动后执行 `script`。 |

## `shar`

### Shell 归档

```text
shar option(s) filename
```

## 用途

`shar` 命令创建 shell 归档（也称为 shar 文件），其为文本格式，可以邮寄给另一个用户，该用户可以用 `bin/sh` 解包并执行它们。

## 选项

- `-a` 自动生成头部。
- `-b` 压缩时使用 `-X` 作为参数。（出于多种原因，应避免使用此选项。）
- `-B` 将所有文件视为二进制文件。（出于多种原因，应避免使用此选项。）
- `-c` 在 shar 文件开头添加剪切线。
- `-d XXX` 使用 `XXX` 作为文件分隔符，而非默认的 `SHAR_EOF`。
- `-f` 仅按文件名恢复，而非恢复整个路径。
- `-F` 强制在每行行首添加前缀字符，即使并非必需。
- `-g` 压缩时使用 `-X` 作为 gzip 的参数。（出于多种原因，应避免使用此选项。）
- `-l XX` 将 shar 文件限制为 `XX` 千字节，但不拆分文件。
- `-L XX` 将 shar 文件限制为 `XX` 千字节，但会拆分文件。
- `-m` 避免生成 `touch` 命令，以在从归档解包文件时恢复文件修改日期。
- `-M` 判断文件是文本还是二进制，并相应地进行归档，这意味着二进制文件会进行 uuencode 编码。（出于多种原因，应避免使用此选项。）
- `-n name` 指定要包含在 shar 文件头部中的归档名称。
- `-o XXX` 将归档保存到文件 `XXX.01` 至 `XXX.nn`，而非标准输出。
- `-p` 允许位置参数选项。
- `-P` 在 shar 文件中使用临时文件替代管道。
- `-s who@where` 覆盖自动确定的提交者名称。
- `-S` 从标准输入而非文件名读取要打包的文件列表。
- `-T` 将所有文件视为文本。
- `-V` 生成普通 shar 文件，解包环境仅需 `sed` 和 `echo`。
- `-v` 以静默模式工作，禁用归档解包时要输出的注释。
- `-w` 解包归档时不使用 `wc -c` 检查。
- `-x` 不检查直接覆盖现有文件。
- `-X` 覆盖现有文件前进行检查。
- `-z` 在打包前使用 `gzip` 和 `uuencode` 压缩所有文件。（出于多种原因，应避免使用此选项。）
- `-Z` 在打包前使用 `compress` 和 `uuencode` 压缩所有文件。（出于多种原因，应避免使用此选项。）

## 相关命令

- `unshar`

## `shelltool`

### 运行 Shell

```text
shelltool option(s)
```

## 用途

`shelltool` 命令在终端窗口中运行 shell 或程序。尽管 `shelltool` 文档如此说明，但您无需在 Linux 环境中安装 OpenWindows 即可运行此命令，不过除非您正在使用 OpenWindows 应用程序，否则实际上几乎没有理由运行它。

## 选项

- `-B boldstyle` 设置粗体文本的显示样式。
- `-C` 将系统控制台输出重定向到 `shelltool`。
- `-I command` 将 `command` 传递给 shell。

## `showfont`

### 显示字体

X Window System 命令

```text
showfont option(s)
```

## 用途

`showfont` 命令显示由 X 字体服务器管理的字体。需要运行 X 字体服务器此命令才能工作。返回的信息包括字体信息、字体属性、字符度量标准和字符位图。您可以使用通配符匹配大量字体名称。

## 选项

- `-bitmap_padn` — 设置字体的位图填充单位（n 为 0、1 或 2，其中 0 表示 ImageRectMin，1 表示 ImageRectMaxWidth，2 表示 ImageRectMax）。
- `-extents_only` — 仅显示字符范围，不显示位图。
- `-end char` — 确定要显示的字符范围的结束（char 为数字）。
- `-fn name` — 指定要显示的字体。
- `-lsb` — 指定位顺序为 `LSBFirst`（最低有效位优先）。
- `-LSB` — 指定字节顺序为 `LSBFirst`（最低有效字节优先）。
- `-msb` — 指定位顺序为 `MSBFirst`（最高有效位优先）。
- `-MSB` — 指定字节顺序为 `MSBFirst`（最高有效字节优先）。
- `-pad n` — 设置字体的扫描填充单位（n 为 8、16、32 或 64）。
- `-server host:port` — 指定要联系的 X 字体服务器。
- `-start char` — 确定要显示的字符范围的开始（char 为数字）。
- `-unit n` — 设置字体的扫描线单位（n 为 8、16、32 或 64）。
- `-noprops` — 不返回字体属性。

## 相关命令

- `fs`
- `fslsfonts`
- `xlsfonts`

## `showrgb`

### 显示颜色数据库

X Window System 命令

```text
showrgb database
```

## 用途

`showrgb` 命令读取 dbm 数据库格式的 `database`，并将其转换回源格式，输出到屏幕上。

## `skill`

### 重新设置进程优先级

```text
skill option(s) PID
```

## 用途

`skill` 命令用于向指定进程发送信号或重新设置其优先级。它向一组进程发送终止信号，或者可以改用指定信号（前面加 `-`）。要查看可用信号列表，请使用 `skill -l` 命令。

## 选项

| 选项 | 说明 |
| --- | --- |
| `-f` | 以快速模式运行，允许读取进程的机器相关代码做出决策以提高速度，但会牺牲错误报告。 |
| `-i` | 以交互模式运行，对每个候选进程提示用户进行操作。 |
| `-v` | 以详细模式运行，显示成功的操作。 |
| `-w` | 当进程不可达时发出警告。 |
| `-n` | 仅显示进程 ID。 |

## 相关命令

- `kill`
- `nice`
- `ps`
- `renice`
- `signal`
- `snice`

## `sleep`

### 暂停

GNU 命令

```text
sleep number
```

## 用途

`sleep` 命令将系统暂停指定的时间：`number`s 秒、`number`m 分钟、`number`h 小时和 `number`d 天。

## `snice`

### 重新设置进程优先级

```text
snice priority PID
```

## 用途

`snice` 命令更改选定进程的调度优先级。默认情况下，新优先级为 +4，但可以使用 `+n`（或 `-n`）形式的参数来指定不同的值。无效的优先级会被向下（或向上）舍入到第一个可接受的值。

## 选项

- `-f` 以快速模式运行，允许读取进程的机器相关代码做出决策以提高速度，但会牺牲错误报告。
- `-i` 以交互模式运行，对每个候选进程提示用户进行操作。
- `-v` 以详细模式运行，显示成功的操作。
- `-w` 当进程不可达时发出警告。
- `-n` 仅显示进程 ID。

## 相关命令

- `kill`
- `nice`
- `ps`
- `renice`
- `signal`
- `skill`

## `smproxy`

### 会话管理器代理

X Window 系统命令

```text
smproxy option(s)
```

## 用途

`smproxy` 命令允许不支持 X11R6 会话管理的 X 应用程序参与 X11R6 会话。

## 选项

- `-clientId id` 设置上一次会话中使用的会话 ID。
- `-restore saveFile` 设置用于保存上一次会话状态的文件。

## `splitvt`

### 分割 Shell

```text
splitvt option(s) shell
```

## 用途

`splitvt` 命令在两个窗口中运行两个 shell。该 shell 是您的默认 shell（通常是 `xterm`）。

要在窗口之间移动，请使用 `Ctrl-W`。

## 选项

- `-login` — 将每个窗口下的程序作为登录 shell 运行。
- `-lower command` — 在下窗口中运行 `command`。
- `-nologin` — 不允许将每个窗口下的程序作为登录 shell 运行。
- `-norc` — 不加载 `~/.splitvtrc`。
- `-rcfile file` — 加载 `file` 作为启动文件，而不是 `~/.splitvtrc`。
- `-s numlines` — 设置顶部窗口的 `numlines`（行数）。
- `-t title` — 设置 `xterm` 标题栏的 `title`。
- `-upper command` — 在上窗口中运行 `command`。

## `startx`

### 启动 X 会话

X Window 系统命令

```text
startx
```

## 用途

`startx` 命令从 Linux 命令行启动 X Window 系统会话。它实际上是 `xinit` 命令的前端。

启动 `startx` 时，它会在您的主目录中查找名为 `xinitrc` 的文件。该文件包含有关 X Window 设置的信息，以及您希望在 X 环境中运行的客户端程序。这些客户端程序大多应在后台运行，但列表中的最后一个客户端程序应在前台运行（通常是窗口管理器）。

与此命令相关的设置不多；更多信息请查看 `xinit`。

## 相关命令

- `xinit`

## `strace`

### 跟踪系统调用

```text
strace option(s) command
```

## 用途

`strace` 命令用于跟踪系统调用和信号。您可以使用它来运行指定的 `command`；`strace` 随后跟踪进程使用的系统调用和信号。结果信息会打印到屏幕或文件（使用 `-o` 选项）。这是一个有用的命令，因为您不需要源代码就能看到命令在哪里出现问题。

## 选项

- `-acolumn`：在指定列数中对齐。
- `-c`：统计每个系统调用的时间、调用次数和错误，并报告摘要。
- `-d`：显示 `strace` 本身的调试输出。
- `-eabbrev=set`：缩写大型结构的输出。
- `-eraw=set`：以未解码（十六进制）格式打印指定系统调用集的参数。
- `-eread {read,write}=set`：以十六进制打印给定文件描述符的所有输入和输出。
- `-esignal=set`：仅跟踪指定的信号子集。
- `-etrace=set`：仅跟踪指定的系统调用集。



- **-e** `verbose=set`：对指定的系统调用集解引用结构。
- **-f**：跟踪子进程。
- **-i**：在系统调用时打印指令指针。
- **-o** `filename`：将输出写入`filename`。
- **-O** `overhead`：将跟踪系统调用的开销设置为`overhead`微秒。
- **-p** `pid`：附加到进程`pid`并开始跟踪。
- **-q**：抑制消息。
- **-r**：在进入每个系统调用时打印相对时间戳。
- **-s** `strsize`：设置要打印的最大字符串大小（默认为 32）。
- **-S** `sortby`：按`sortby`对`-c`选项的输出进行排序。
- **-t**：以时间开始跟踪的每一行。
- **-tt**：以包含微秒的时间开始跟踪的每一行。
- **-T**：返回系统调用中花费的时间。
- **-v**：提供详细输出。
- **-x**：以十六进制字符串格式打印非 ASCII 字符串。
- **-xx**：以十六进制字符串格式打印所有字符串。

## 相关命令
- `ptrace`
- `time`
- `trace`

### strings

### 查找字符串

```
strings option(s) filename(s)
```

## 用途
`strings`命令在文件中搜索可打印的字符串。默认情况下，字符串必须至少包含四个字符才会显示。此命令通常用于在二进制文件中搜索可打印文本。

大多数 Linux 实现包含两个版本的`strings`：原始 UNIX 版本（`strings`）和 GNU 版本（`strings-gnu`），后者是更高级的版本。

## 选项
- **-a**：在整个对象文件中搜索字符串。默认情况下仅搜索对象文件的文本段和数据段。
- **-f**：打印包含字符串的文件名以及字符串本身。
- **-n** `num`：将字符串的最小字符数设置为`num`，而不是默认的四个。
- **-o**：打印字符串在文件中的十进制偏移量以及字符串本身。

## 相关命令
- `hexdump`
- `strings-gnu`

### strings-gnu

### 查找字符串

GNU 命令

```
strings option(s) filename(s)
```

## 用途
`strings`命令在文件中搜索可打印的字符串。默认情况下，字符串必须至少包含四个字符才会显示。此命令通常用于在二进制文件中搜索可打印文本。

大多数 Linux 实现包含两个版本的`strings`：原始 UNIX 版本（`strings`）和 GNU 版本（`strings-gnu`），后者是更高级的版本。

## 选项
- **-a**：在整个对象文件中搜索字符串。默认情况下仅搜索对象文件的文本段和数据段。
- **-f**：打印包含字符串的文件名以及字符串本身。
- **-n** `num`：将字符串的最小字符数设置为`num`，而不是默认的四个。
- **-o**：打印字符串在文件中的十进制偏移量以及字符串本身。
- **-t {o,x,d}**：打印字符串在文件中的十进制偏移量以及字符串本身。单字符参数指定偏移量的基数——八进制、十六进制或十进制。
- **--target=**`bfdname`：指定除系统默认格式外的对象代码格式。

# stty

### 修改终端设置

### GNU 命令

`stty` *设置选项*

## 用途
`stty`命令用于返回和修改终端设置。不带参数时，`stty`返回当前设置：波特率、线路规程号，以及与`stty sane`设置值相比已被更改的线路设置。

### 非选项设置
在设置前加`-`可切换相反行为。

- **clocal**：禁用调制解调器控制信号。
- **cread**：允许接收输入。
- **crtscts**：启用 RTS/CTS 握手。
- **cs5 cs6 cs7 cs8**：将字符大小设置为 5、6、7 或 8 位。
- **cstopb**：每个字符使用两个停止位（加`-`时使用一个）。
- **hup**：当最后一个进程关闭 tty 时发送挂起信号。
- **hupcl**：当最后一个进程关闭 tty 时发送挂起信号。
- **parenb**：在输出中生成奇偶校验位，并在输入中期望奇偶校验位。
- **parodd**：设置奇校验（前面加`-`时为偶校验）。

### 输入设置
在设置前加`-`可切换相反行为。

- **brkint**：中断产生中断信号。
- **icrnl**：将回车转换为换行。
- **ignbrk**：忽略中断。
- **igncr**：忽略回车。
- **ignpar**：忽略奇偶校验错误。
- **imaxbel (np)**：当输入缓冲区已满时若有字符到达，启用蜂鸣且不清空输入缓冲区。
- **inlcr**：将换行转换为回车。
- **inpck**：启用输入奇偶校验检查。
- **istrip**：剥除输入字符的高（第 8）位。
- **iuclc (np)**：将大写字符转换为小写。
- **ixany (np)**：允许任何字符重新启动输出。
- **ixon**：启用 XON/XOFF 流控制。
- **ixoff tandem**：当系统输入缓冲区几乎已满时启用发送停止字符，当缓冲区再次几乎为空时发送开始字符。
- **parmrk**：用 255-0-字符序列标记奇偶校验错误。

### 输出设置
在设置前加`-`可切换相反行为。

- **bs1 bs0 (np)**：设置退格延迟样式。
- **cr3 cr2 cr1 cr0 (np)**：设置回车延迟样式。
- **ff1 ff0 (np)**：设置换页延迟样式。
- **nl1 nl0 (np)**：设置换行延迟样式。
- **ocrnl (np)**：将回车转换为换行。
- **ofdel (np)**：使用删除字符作为填充，而非空字符。
- **ofill (np)**：使用填充（补齐）字符代替定时延迟。
- **olcuc (np)**：将小写字符转换为大写。
- **onlcr (np)**：将换行转换为回车-换行。
- **onlret (np)**：将换行用作回车。
- **onocr (np)**：不在第一列打印回车。
- **opost**：对输出进行后处理。
- **tab3 tab2 tab1 tab0 (np)**：设置水平制表符延迟样式。
- **vt1 vt0 (np)**：设置垂直制表符延迟样式。

### su

### 切换用户

GNU 命令

`su` *选项*

## 用途
`su`命令使用替代用户和替代组 ID 运行 shell。基本上，它允许你临时以新用户身份登录系统，具有实际和有效的用户 ID、组 ID 和补充组。shell 取自密码条目，若未指定则为`/bin/sh`。如果用户有密码，`su`会提示输入密码，除非该用户的实际用户 ID 为 0（超级用户）。

当前目录保持不变。如果给定一个或多个参数，它们将作为额外参数传递给 shell。

## 选项
- **-**：使 shell 成为登录 shell。
- **-c** *command*：将命令传递给 shell，而非启动交互式 shell。
- **-f**：将`-f`选项传递给 shell。与 C shell 一起使用，而非 Bourne Again SHell。
- **-m**：保留`HOME`、`USER`、`LOGNAME`或`SHELL`不变。
- **-s** *SHELL*：运行`SHELL`而非用户的 shell。

### subst

### 替换定义

`subst` *目标文件 替换文件*

## 用途
`subst`将定义替换到*文件名*中。主要用于根据本地条件定制软件。每个*目标文件*根据*替换文件*的内容进行修改。

*替换文件*每行包含一个替换。每行由两个字段组成，以制表符分隔。第一个字段是替换的*名称*，第二个是*值*。两者均不应包含字符`#`，使用文本编辑器的元字符如`&`和`\`也不明智；名称尤其应限制为字母数字字符。以`#`开头的行是注释，将被忽略。

在*目标文件*中，每个要进行替换的行（*目标行*）前面必须有一个*原型行*。替换使用`sed`编辑器完成。

### sx

### 发送 Xmodem

```
sx 选项 文件名
```

## 用途
`sx`命令使用 Xmodem 协议将文件发送到另一个系统。此命令有大量选项；更多信息请参阅在线手册页。

### sxpm

### 显示 X 像素图

X 窗口系统命令

```
sxpm 选项 文件名
```

## 用途
`sxpm`显示 X 像素图（图形）文件，可以将 XPM 1 或 XPM 2 格式的文件转换为较新的 XPM 3 格式。

## 选项
- **-closecolors**：在回退到其他视觉效果之前使用"近似颜色"。
- **-color**：显示为彩色视觉指定的颜色。
- **-cp** *颜色名称 像素值*：将颜色名称的颜色覆盖为像素值。
- **-d** *显示器*：指定要连接的显示器。
- **-g** *几何参数*：设置窗口几何（默认为像素图大小）。
- **-grey**：显示为灰度视觉指定的颜色。
- **-grey4**：显示为 4 色灰度视觉指定的颜色。
- **-hints**：为窗口设置 ResizeInc 提示。
- **-icon** *文件名*：从文件创建像素图图标。
- **-mono**：显示单色视觉。
- **-nod**：不在窗口中显示像素图；在格式之间转换时使用此选项。
- **-nom**：忽略剪裁蒙版。
- **-o** *文件名*：写入到文件名。
- **-pcmap**：使用私有颜色图。
- **-plaid**：显示作为数据存储的格子像素图。
- **-sc** *符号 颜色名称*：将符号颜色覆盖为颜色名称。
- **-sp** *符号 像素值*：将符号颜色覆盖为像素值。
- **-rgb** *文件名*：在文件名中搜索 RGB 数据库，并输出其而非默认 RGB 值。
- **-v**：以详细模式打印扩展信息。

### systat

### 系统统计

`systat` *选项* *主机名*

## 用途
`systat`命令通过主机自身的`systat`服务检查指定的*主机名*获取系统信息。如果`systat`服务不可用，则查询`daytime`或`netstat`信息。

## 选项
| 选项 | 描述 |
|--------|-------------|
| **-n** | 查询`netstat`服务。 |
| **-p** *端口* | 指定主机上的*端口*。 |
| **-s** | 查询`systat`服务（默认设置）。 |
| **-t** | 查询`daytime`服务。 |
| **--netstat** | 查询`netstat`服务。 |
| **--port** *端口* | 指定主机上的*端口*。 |
| **--systat** | 查询`systat`服务（默认设置）。 |
| **--time** | 查询`daytime`服务。 |

### sz

### 发送 Zmodem

`sz` *选项* *命令*

## 用途
`sz`命令使用 Zmodem 协议将文件发送到另一个系统。此命令有大量选项；更多信息请参阅在线手册页。

### tee

### 将信息发送到两个文件

`tee` *选项* *文件名*

## 用途
`tee`命令将命令的输出发送到两个独立的文件。如果文件已存在，`tee`命令将覆盖文件内容。

## 选项
- **-a**：将路由信息追加到*文件名*，但不覆盖现有文件。

### 示例
```
$aooc-idktell
```

```tsync
```

# tload

### 系统总负载

`tload` *选项*

## 用途
`tload`命令以图形的形式列出系统负载。

## 选项
| 选项 | 说明 |
|--------|-------------|
| `-d` *延迟* | 设置图形更新之间的延迟，单位为秒。 |
| `-s` *比例* | 指定垂直比例。 |

## 相关命令
- `ps`
- `top`

### top

### 进程监控

`top` *选项*

## 用途
`top`命令列出系统中的顶级进程——即那些占用 CPU 时间最多的进程。

## 选项
| 选项 | 描述 |
|--------|-------------|
| `d` | 指定屏幕更新之间的延迟。 |
| `q` | 无延迟刷新。 |
| `S` | 同时列出已终止子进程的 CPU 时间。 |
| `s` | 以安全模式运行。 |
| `i` | 忽略僵尸进程或空闲进程。 |

### 示例
```
$ top
```

## 相关命令
- `ps`
- `tload`

### true

### 返回真

GNU 命令

`true`

## 用途
`true`命令除了返回退出状态码 0（即成功）之外，不做任何事情。这在 shell 脚本中很有用。

### ul

### 下划线

`ul` *选项* 终端

## 用途
`ul`命令将所有带下划线的文本转换为下划线文本。这对于连接到 Linux 系统的终端用户来说是一个问题，而对大多数 Linux 用户来说不是。

## 选项
- **-i**：使用单独的一行，包含适当的破折号来表示下划线。
- **-t** 终端：指定新的终端类型。

### unshar

### 解压 Shar 文件

`unshar` *选项 文件名*

## 用途
`unshar`命令解压`shar`文件。

## 选项
- **-c**：覆盖现有文件。
- **-d** *目录*：在解压文件之前切换到*目录*。

## 相关命令
- `shar`

### uptime

## 用途
`uptime`命令显示系统已运行多长时间、当前有多少用户登录，以及过去 1 分钟、5 分钟和 15 分钟的系统平均负载。

## 相关命令
- `users`
- `w`
- `who`

### users

### 用户信息

GNU 命令

```
users *文件名*
```

## 用途
`users`命令根据`/etc/utmp`文件中的信息，列出当前登录 Linux 系统的用户信息。如果您想从其他系统文件中获取信息，必须在命令行上指定。

## 相关命令
- `who`

### viewres

### 查看类

X 窗口系统命令

`viewres` *选项*

## 用途
`viewres`程序显示 Athena 部件集的部件类层次结构。

## 选项
- **-top** *名称*：指定要显示的层次结构中最顶层部件的名称。
- **-variable**：在节点中显示部件变量名称，而不是部件类名称。
- **-vertical**：从上到下而不是从左到右显示。

### w

### 系统信息

`w` *选项* 用户名

## 用途
`w`命令返回有关系统的信息：当前登录系统的用户、使用统计信息以及用户正在执行的任务。这是`who`、`ps -a`和`uptime`命令的组合。

系统信息以标题形式返回，包括以下内容：当前时间、系统已运行多长时间、当前有多少用户登录，以及过去 1 分钟、5 分钟和 15 分钟的系统平均负载。

用户信息包括以下内容：登录名、tty 名称、远程主机、登录时间、空闲时间、JCPU、PCPU 以及他们当前进程的命令行。

## 选项
- **-h**：不打印标题。
- **-u**：在计算当前进程和 CPU 时间时忽略当前用户。
- **-s**：不打印登录时间、JCPU 或 PCPU 时间。
- **-f**：打印`from` (*远程主机名*) 字段。

## 相关命令
- `free`
- `ps`
- `top`
- `uptime`

### whatis

### 命令信息

`whatis` *选项 关键词*

## 用途
`whatis`命令调用一个微型帮助系统，但主题按关键词（涵盖概念）列出，而不一定按命令列出。由于帮助信息以单行形式返回，关于关键词的深度不大。

有关可用选项的列表，请参阅在线手册页。

### 示例
```
$ whatis cat
```

## 相关命令
- `apropos`
- `man`

### who

### 用户信息

`who` *选项* *文件名*

## 用途
`who`命令显示有关系统或特定用户的信息。单独使用时，`who`命令列出当前登录系统的用户名。作为命令行`who am i`，`who`命令列出关于您的信息。

有关可用选项的列表，请参阅在线手册页。

## 相关命令
- `w`
- `whoami`

### whoami

## 用途
这是`who am I`变体命令的一个单词快捷方式。它与`id -un`相同。

### 示例
```
$ whoami
kevin
```



## 相关命令

`who`

### wish

Tcl 窗口 Shell

`wish` `文件名` `参数`

## 用途

`wish` 命令是一个包含 Tcl 命令语言、Tk 工具包以及从标准输入或文件中读取命令的主程序的 Shell 窗口。它创建一个主窗口，然后处理 Tcl 命令。它将继续处理命令，直到所有窗口都被删除或标准输入到达文件末尾。

## 选项

- **-colormap new** — 创建新的专用色彩映射，而不是使用默认的色彩映射。
- **-sync** — 同步执行 X 服务器命令，以便立即报告错误。
- **-visual** `视觉` — 指定窗口的视觉。

## 相关命令

`Tk`

### x11perf

X 服务器性能

X 窗口系统命令

`x11perf` `选项`

## 用途

`x11perf` 命令在 X 服务器上运行一组测试，并报告速度性能。这些测试专门针对 X 窗口系统，使用基准测试来确定创建和映射窗口所需的时间、将一组预先存在的窗口映射到屏幕上的时间，以及在屏幕上移动窗口的时间。它还测量常用 X 应用程序的图形性能，包括将位图映射到像素、滚动以及各种点图案和平铺图案。这些信息实际上并不像您想象的那么有用——您无法对服务器进行任何更改（除非您是经验丰富的程序员并且想要处理 X 服务器源代码），而且您可能不会根据这些数字来更改您的 X 服务器。

## 选项

- **-display** `主机:显示` — 指定显示。
- **-pack** — 运行矩形测试，使矩形紧密排列在一起。
- **-sync** — 以同步模式运行测试。这是一个相当无用的选项。
- **-repeat** `n` — 重复每项测试 `n` 次。默认值为五次。
- **-time** `s` — 设置每项测试的时长。默认值为五秒。
- **-all** — 执行所有测试。出去喝杯拿铁吧，这是一个耗时的测试。
- **-range** `test1,[test2]` — 运行从指定的 `test1` 开始到名称 `test2` 为止的所有测试，包括两个指定的测试。测试名称应为以下从 `-dot` 开始的选项之一。
- **-labels** — 仅生成每项指定测试的描述性标签。
- **-fg** `颜色/像素` — 设置前景色或像素值。
- **-bg** `颜色/像素` — 设置背景色或像素值。
- **-clips** `default_num` — 设置默认的裁剪窗口数量。
- **-ddbg** `颜色/像素` — 设置用于绘制 DoubleDashed 线或圆弧的奇数段的颜色或像素值。默认值为背景色。
- **-rop** `rop0 rop1 ...` — 使用指定的光栅操作（默认值为 `GXcopy`）。
- **-pm** `pm0 pm1 ...` — 使用指定的平面掩码（默认值为 `~0`）。
- **-depth** `深度` — 使用每个像素 `深度` 平面的视觉。（默认值为默认视觉）。
- **-vclass** `vclass` — 使用 `vclass` 类型的视觉。可以是 `StaticGray`、`GrayScale`、`StaticColor`、`PseudoColor`、`TrueColor` 或 `DirectColor`。（默认值为默认视觉）。
- **-reps** `n` — 设置重复次数（默认值为五秒）。
- **-subs** `s0 s1 ...` — 设置在窗口测试中使用的子窗口数量。默认序列是 4、16、25、50、75、100 和 200。
- **-v1.2** — 使用 1.2 版语义执行 1.2 版测试。
- **-v1.3** — 使用 1.3 版语义执行 1.3 版测试。
- **-su** — 将所有窗口的 `save_under` 窗口属性设置为 `True`。默认值为 `False`。
- **-bs** `backing_store_hint` — 将 `x11perf` 创建的所有窗口的 `backing_store` 窗口属性设置为给定值。可以是 `WhenMapped` 或 `Always`。默认值为 `NotUseful`。

还有许多指定要执行的确切测试的选项。详情请参阅在线手册页。

## 相关命令

- `x`
- `xbench`
- `x11perfcomp`

## x11perfcomp — 性能比较

X Window System 命令

`x11perfcomp` `选项` `文件名`

## 用途

`x11perfcomp` 以表格形式合并多个 `x11perf` 测试返回的信息。

## 选项

- **-l** `标签文件` — 指定要使用的标签文件。
- **-r** — 指定输出应包含相对服务器性能。
- **-ro** — 指定输出应仅包含相对服务器性能。

## 相关命令

- `X`
- `x11perf`

## xargs — 构建命令行

GNU 命令

`xargs` `选项` `命令`

## 用途

`xargs` 命令从标准输入读取参数，参数之间以空白字符（可用双引号、单引号或反斜杠保护）或换行符分隔，并使用初始参数后接从标准输入读取的参数执行该命令（如果未指定命令，则运行 `/bin/echo`）。标准输入中的空行将被忽略。该命令以如下状态退出：

| 状态 | 含义 |
|------|------|
| 0 | 成功 |
| 123 | 命令退出状态为 1–125 |
| 124 | 命令退出状态为 255 |
| 125 | 命令被翊信号终止 |
| 126 | 命令无法运行 |
| 127 | 命令未找到 |
| 1 | 发生其他错误 |

## 选项

| 选项 | 说明 |
|------|------|
| `-0`, `--null` | 文件名以空字符而非空白字符终止，且引号和反斜杠字符不再作为特殊字符。 |
| `-e[eof-str]`, `--eof[=eof-str]` | 将文件结束字符串设置为 `eof-str`。 |
| `-i[replace-str]`, `--replace[=replace-str]` | 将初始参数中的 `replace-str` 替换为从标准输入读取的名称。 |
| `-L[max-lines]`, `--max-lines[=max-lines]` | 每个命令行使用 `max-lines` 个非空输入行；默认为一行。 |
| `-n max-args`, `--max-args=max-args` | 每个命令行使用 `max-args` 个参数。 |
| `-p`, `--interactive` | 在运行每个命令之前提示用户。 |
| `-P max-procs`, `--max-procs=max-procs` | 同时运行最多 `max-procs` 个进程；默认为一个。 |
| `-r`, `--no-run-if-empty` | 不运行只包含空白字符的命令。 |
| `-s max-chars`, `--max-chars=max-chars` | 每个命令行最多使用 `max-chars` 个字符，包括命令、初始参数以及参数字符串末尾的终止空字符。 |
| `-x`, `--exit` | 如果超出大小限制（由 `-s` 设置）则退出。 |

## xauth — X 授权信息

X Window System 命令

```
xauth 选项 命令 参数...
```

## 用途

`xauth` 命令显示和编辑用于连接 X 服务器的授权信息。该程序实际上不会与 X 服务器通信，也不会自行创建授权信息。

## 选项

- **-b** 在继续之前强制解除授权文件锁。此选项用于清理过期的锁。
- **-f** `授权文件` 设置要使用的授权文件。默认为 `XAUTHORITY` 环境变量指定的文件或用户主目录中的 `.Xauthority` 文件。
- **-i** 覆盖授权文件锁。
- **-q** 以安静模式工作，不打印未经请求的状态消息。
- **-v** 以详细模式工作，打印指示各种操作结果的状态消息。

还有大量用于操作授权文件的命令；详情请参阅在线手册页。

## xcalc — X 计算器

X Window System 命令

```
xcalc 选项
```

## 用途

`xcalc` 命令启动科学计算器。它模拟 TI-30 或 HP-10C 计算器。

该程序启动后可用的用户命令有很多；详情请参阅在线手册页。

## 选项

| 选项 | 说明 |
|------|------|
| `-rpn` | 使用逆波兰表示法，模拟 HP-10C；如果未设置此选项，则模拟 TI-30。 |
| `-stipple` | 使用前景色和背景色的点阵图案作为计算器背景；对单色显示器很有用。 |

## xclipboard — 显示 X 剪贴板

`xclipboard` `选项`

## 用途

`xclipboard` 命令显示剪贴板的内容，剪贴板通常包含由其他应用程序复制到那里的文本选择。剪贴板是应用程序在内部以及与其他应用程序之间进行剪切和粘贴的方式；文本首先复制到剪贴板，然后再从那里复制出去。

## 选项

| 选项 | 说明 |
|------|------|
| `-w` | 对剪贴板中过长而无法在一行中显示的行进行换行。 |
| `-nw` | 不对剪贴板中过长而无法在一行中显示的行进行换行。 |

## 相关命令

- `x`
- `xcutsel`

### xclock

X Window System 命令

`xclock` `选项`

## 用途

`xclock` 命令启动模拟时钟或数字时钟。

## 选项

- **-analog** 使用标准 12 小时模拟钟面显示时间，带有刻度和指针。
- **-d, -digital** 使用 24 小时数字显示时间。
- **-chime** 设置在半点响一声、整点响两声的报时。
- **-hd color** 设置模拟时钟指针的颜色。
- **-hl color** 设置模拟时钟指针边缘的颜色。
- **-update seconds** 设置时钟更新的频率，单位为`秒`。当时钟被其他窗口遮挡时，不会更新。如果 `seconds` 为 30 或更小，模拟时钟将显示秒针。默认为 60 秒。
- **-padding number** 设置窗口边框与时钟文本或图像之间填充的宽度（以像素为单位）。数字时钟默认为 10 像素，模拟时钟默认为 8 像素。

## 相关命令

- `oclock`

## xcmap — 显示颜色映射

X Window System 命令

```
xcmap 选项
```

## 用途

`xcmap` 命令以对应于颜色映射条目的方格网格形式显示 X 颜色的内容。

## xcmsdb — 设备颜色管理

X Window System 命令

```
xcmsdb 选项
```

## 用途

`xcmsdb` 命令加载、查询或移除按照 ICCCM 第 7 节的规定存储在屏幕根窗口属性中的设备颜色特性数据。这些信息对于设备无关颜色规范与设备相关颜色规范之间的正确转换是必需的。

## 选项

- **-query** 从屏幕根窗口读取 `XDCCC` 属性。
- **-remove** 从屏幕根窗口移除 `XDCCC` 属性。
- **-format 32|16|8** 指定位每条目属性格式：32、16 或 8。

## 相关命令

`xprop`

## xconsole — X 控制台监视器

X Window System 命令

`xconsole` `选项`

## 用途

`xconsole` 命令显示通常发送到 `/dev/console` 的消息。

## 选项

- **-daemon** 在后台运行该命令。
- **-file filename** 指定要监视的其他设备。
- **-notify** 显示向控制台发送新数据的应用程序，即使该应用程序已最小化。此为默认设置。
- **-nonotify** 切换 `-notify` 选项。
- **-verbose** 向文本缓冲区添加信息丰富的第一行。
- **-exitOnFail** 在无法重定向控制台输出时退出。

## xcpustate — X CPU 状态

X Window System 命令

`xcpustate` `选项`

## 用途

`xcpustate` 显示各种 CPU 状态。

## 选项

- **-count** `迭代次数` — 指定显示更新次数的限制。默认没有限制。
- **-interval** `秒` — 设置更新间隔；默认为一秒。

## 相关命令

- `xload`
- `xperfmon`

## xcutsel

### X 剪切选择

X Window System 命令

```
xcutsel option(s)
```

## 用途

`xcutsel` 命令将当前选择复制到剪切缓冲区，并创建一个包含剪切缓冲区当前内容的选择。该命令用作不支持选择的应用程序与支持选择的应用程序之间的桥梁，尽管大多数较新的应用程序都支持选择。

## 选项

- **-selection** `name` — 设置要使用的功能名称；默认值为 `primary`。唯一支持的缩写形式为 `-select`、`-sel` 和 `-s`。
- **-cutbuffer** `number` — 设置要使用的剪切缓冲区编号；默认值为 0。

## 相关命令

`xclipboard`

`xterm`

### xdm

### X 显示管理器

X Window System 命令

`xdm` `option(s)`

## 用途

X 显示管理器负责管理 X 显示，无论这些显示位于本地主机还是远程服务器上。它管理整个会话，提示输入登录名和密码，对用户进行身份验证，并运行实际的会话（会话以会话管理器开始和结束）。当会话结束时，`xdm` 会重置 X 服务器并重新启动整个流程。它还可以通过 XDMCP 协调各会话之间的工作，向其他终端提供主机菜单。

`xdm` 是一个复杂的命令，无法在此深入介绍。在着手使用该命令之前，请参阅在线手册页或查阅有关 X Window System 的权威参考资料。

## 选项

- **-config** `configuration_file` — 指定配置文件；默认值为 `<XRoot>/lib/X11/xdm/xdm-config`。
- **-debug** `debug_level` — 设置调试级别值，供 `DisplayManager.debugLevel` 资源使用。但是，除非您要研究 `xdm` 的源代码，否则这些调试信息毫无价值。
- **-error** `error_logfile` — 设置 `DisplayManager.errorLogFile` 资源的值。
- **-nodaemon** — 将 `DisplayManager.daemonMode` 资源的值设为 `false`。
- **-resources** `resource_file` — 设置 `DisplayManager.resources` 资源的值。它包含身份验证部件的配置参数。
- **-server** `server_entry` — 设置 `DisplayManager.servers` 资源的值。
- **-session** `session_program` — 设置 `DisplayManager.session` 资源的值。

  这会设置在用户登录后作为会话运行的程序。
- **-udpPort** `port_number` — 设置 `DisplayManager.requestPort` 资源的值，该值控制 XDMCP 请求的端口号。由于 XDMCP 使用已注册的 UDP 端口 177，因此不应更改此设置。
- **-xrm** `resource_specification` — 设置任意资源。

## 相关命令

`xauth`

`xinit`

### xdpyinfo

### X 显示信息

X Window System 命令

```
xdpyinfo option(s)
```

## 用途

`xdpyinfo` 命令显示有关特定 X 服务器的信息。在查找图形信息时最为有用。

## 选项

- **-ext** `extension` — 显示有关特定扩展的信息。如果未指定扩展，则显示所有扩展的信息。
- **-queryExtensions** — 同时显示有关协议扩展的数字信息（操作码、基础事件、基础错误）。

## 相关命令

`xprop`

`xrdb`

`xwininfo`

### xev

### X 事件显示

X Window System 命令

`xev` `option(s)`

## 用途

`xev` 命令打开一个窗口，然后打印在该窗口上或上方执行的任何操作的事件信息（鼠标移动、窗口调整大小和移动、键盘输入等）。

## 选项

- **-id** `windowid` — 监视现有的 `windowid`，而非新窗口。
- **-name** `string` — 指定将 `string` 分配给新窗口。
- **-rv** — 以反色显示窗口。
- **-s** — 在新窗口上启用保存底图功能。

## 相关命令

`xdpyinfo`

`xwininfo`

### xeyes

### X 眼睛

X Window System 命令

`xeyes` `option(s)`

## 用途

`xeyes` 命令创建一个带有眼睛的窗口，眼睛会跟随光标的移动。浪费 X 资源的绝佳方式。

## 选项

- **-fg** `foregroundcolor` — 设置眼睛瞳孔的颜色。
- **-bg** `backgroundcolor` — 设置背景色。
- **-outline** `outlinecolor` — 设置眼睛轮廓的颜色。
- **-center** `centercolor` — 设置眼睛中心的颜色。

### xf86config

### 生成 XF86config 文件

X Window System 命令

```
xf86config
```



## 用途

`xf86config`命令生成`XF86Config`文件，该文件是在运行 X Window System 之前必需的。

### xfd

### 显示字体信息

X Window System 命令

`xfd` *option(s)*

## 用途

`xfd`命令在一个窗口中显示 X 字体的所有字符，该窗口包含正在显示的字体名称、一行命令按钮、几行用于显示字符度量信息的文本，以及一个每个单元格包含一个字形的网格。

## 选项

- **-fn** *font* — 指定要显示的字体。
- **-center** — 将每个字形在其网格中居中。

### xfontsel

### X 字体选择器

X Window System 命令

```
xfontsel option(s)
```

## 用途

`xfontsel`提供了一个点击式界面，用于显示 X Window System 字体名称以及字体示例，并检索字体的完整 X 逻辑字体描述 (XLFD) 名称。您可以选择/species 以查看所有字体——这会产生大量输出——或者您可以将通配符与 *-pattern* 选项结合使用，以缩减字体列表。

## 相关命令

`xfd`

### xfractint

### X 分形生成器

X Window System 命令

`xfractint` *option(s)*

## 用途

`xfractint`命令是一个分形生成器，是 MS-DOS 分形程序 fractint 的移植版本。

## 选项

- **-disk** — 将图像保存到文件而非屏幕。
- **-fast** — 如果使用快速显示器，则频繁更新图像（每五秒一次）。
- **-fixcolors** *num* — 设置颜色数量，以 2 的幂表示。
- **-onroot** — 在根窗口上显示图像。您可能不想这样做，因为橡皮筋缩放框在根窗口上无法工作。
- **-private** — 在私有颜色图中尽可能多地获取颜色。
- **-share** — 共享当前颜色图。
- **-simple** — 指定更简单的键盘处理方式。
- **-slowdisplay** — 如果使用慢速显示器，则较少更新图像。
- **@** ***filename*** — 从 *filename* 加载参数。

### xfs

### X 字体服务器

X Window System 命令

`xfs` *option(s)*

## 用途

`xfs`命令启动 X Window System 字体服务器。它的工作原理与名称完全一致：向请求的应用程序提供渲染后的字体。该命令由系统管理员配置，设置为每次启动 X 时自动启动。

## 选项

- **-config** *configuration_file* — 设置字体服务器配置文件。
- **-port** *tcp_port* — 指定 TCP 端口号。

### xgc

### X 图形演示

X Window System 命令

`xgc` *option(s)*

## 用途

`xgc`命令启动 X 图形功能的演示。有关选项列表，请参阅在线手册页。

### xhost

### X 服务器访问

X Window System 命令

```
xhost +/- hostname
```

## 用途

`xhost`程序设置授权连接到 X 服务器的主机或用户名称。这不是一种特别复杂的访问控制方法。主机名前带有加号 (+) 的将被添加到访问列表中，而主机名前带有减号 (-) 的将从访问列表中删除。两个加号 (++) 允许所有人访问，而两个减号 (--) 则将访问权限限制为访问列表中的用户。不带任何选项时，`xhost`将返回当前状态。

## 相关命令

`xdm`

## xieperf

### X Window System 命令

`xieperf` *选项*

## 用途

`xieperf`命令用于评估 XIE 服务器扩展。完整的测试集可参见联机手册页。

## 选项

- **-all** — 运行所有测试。这可能需要一些时间。
- **-cache** *n* — 设置包含 *n* 个条目的光图缓存。
- **-depth** *深度* — 指定每像素的 *深度* 层数。
- **-DirectColor** — 使用 DirectColor 视觉模式。
- **-DIS** — 仅运行涵盖 XIE 的 DIS 子集中协议请求的测试。
- **-display** *主机:显示号* — 设置显示。
- **-errors** — 测试错误事件生成。
- **-events** — 测试事件生成。
- **-GrayScale** — 使用 GrayScale 视觉模式进行测试。
- **-images** *路径* — 设置加载图像的 *路径*。
- **-labels** — 生成所有脚本的标签，但不运行测试。
- **-loCal** — 跳过测试校准。
- **-mkscript** — 生成适合与 script 选项配合使用的脚本文件。
- **-PseudoColor** — 使用 PseudoColor 视觉模式进行测试。
- **-range** *测试1* *测试2* — 运行从 *测试1* 开始到 *测试2* 结束的测试，包括指定的两个测试。
- **-repeat** *n* — 将每个测试重复 *n* 次（默认为两次）。
- **-reps** *n* — 将内循环重复次数设置为 *n*。
- **-sync** — 以同步模式运行测试。
- **-script** *文件* — 运行名为 *文件* 的脚本文件中指定的测试。
- **-showlabels** — 在屏幕上打印测试标签，指示要运行的测试。这有助于确定是否有测试导致系统崩溃。
- **-showevents** — 打印有关事件和错误测试的信息。
- **-showtechs** — 提供 XIE 服务器使用的技术的详细列表。
- **-StaticColor** — 使用 StaticColor 视觉模式。
- **-StaticGray** — 使用 StaticGray 视觉模式。
- **-tests** — 显示可用的测试。
- **-time** *秒* — 设置每个测试应运行的 *秒* 数（默认为五秒）。
- **-timeout** *秒* — 设置测试等待可能永远不会到达的事件的时间。
- **-TrueColor** — 使用 TrueColor 视觉模式。
- **-WMSafe** — 通过告知 `xieperf`它正在窗口管理器环境中运行，提供更准确的结果。

## 相关命令

`x11perf`、`x11perfcomp`

---

### xinit

### X 初始化器

### X Window System 命令

`xinit` *客户端 选项(s)*

## 用途

`xinit`命令启动 X Window System（从 *startx* 调用），也可以在无法直接从 `/etc/init` 启动 X 的系统上启动第一个客户端。

然而，在大多数情况下，您不会从命令行启动应用程序。在这些情况下，`xinit`启动 X 时会使用一系列步骤：

- 它首先查找名为 `.xinitrc` 的文件，该文件作为 shell 脚本运行以启动客户端程序。
- 如果此文件不存在，`xinit`使用 `xterm -geometry +1+1 -n login -display :0` 作为命令行。
- 如果命令行上没有服务器程序，`xinit`会在用户的主目录中查找 `.xserverrc`。
- 如果此文件不存在，`xinit`使用 `X :0` 作为默认服务器。

当您设置 `.xserverrc` 脚本时，必须确保启动正确的 X 服务器。

如果您选择不使用机械化工具来配置 X Window System，编写 `.xinitrc` 是一门学问。您必须确保此文件中启动的应用程序在后台运行，但最后一个程序（通常是窗口管理器）除外，它应该在前台运行以确保脚本不会失败。

---

### xkill

### 终止客户端

X Window System 命令

```
xkill 选项(s)
```

## 用途

`xkill`命令强制 X 服务器切断与客户端的连接。您可以通过资源标识符指定程序。如果不这样做，`xkill`将显示一个骷髅交叉骨光标，当您点击它时，这个死亡光标下方的窗口将被终止。

这不是关闭程序的最佳方式，因此请谨慎使用此命令。

#### 注意

## 选项

| 选项 | 描述 |
|--------|-------------|
| -all | 终止屏幕上所有具有顶级窗口的客户端。仅将此作为最后的手段。 |
| -button *数字* | 指定与死亡光标一起使用的鼠标按钮。默认为左鼠标按钮。您可以使用 *all* 代替数字来指定死亡光标的任何按钮。 |
| -display *显示名* | 指定要联系的服务器。 |
| -id *资源* | 指定要终止的客户端。 |
| -frame | 告诉 `xkill`您想要终止根的直接子窗口。 |

## 相关命令

`xwininfo`

---

### xload

### 显示系统负载

X Window System 命令

```
xload 选项(s)
```



## 用途

`xload`命令定期轮询系统平均负载，并以直方图形式传递信息。

## 选项

- **-hl** *颜色* — 设置直方图中刻度线的颜色。
- **-jumpscroll** *像素* — 设置图表到达窗口右边缘时偏移的*像素*数。默认为窗口宽度的一半。
- **-label** *字符串* — 指定在负载平均值上方显示为标签的*字符串*。
- **-lights** *n* — 使用键盘 LED 显示平均负载。当负载水平达到*n*时，`xload`点亮前*n*个键盘 LED，但屏幕上不显示任何内容。
- **-nolabel** — 在负载图上方不显示标签。
- **-scale** *整数* — 设置显示直方图中最小刻度数。
- **-update** *秒* — 每*秒*返回新信息。默认为 10，最小为 1。

---

### xlock

### 锁定显示

X Window System 命令

`xlock` *选项(s)*

## 用途

`xlock`命令锁定 X 显示，直到输入密码。发生这种情况时，所有新的服务器连接将被拒绝，屏幕保护程序被禁用，鼠标光标被关闭，屏幕被消隐。

## 选项

- **-cycles** *数字* — 设置模式超时前的周期数。
- **-display** *显示* — 设置要锁定的显示。
- **-font** *字体名* — 设置登录提示屏幕上使用的*字体名*。
- **-forceLogout** *分钟* — 设置自动注销前的*分钟*数。
- **-info** *文本字符串* — 在登录屏幕上显示信息文本；默认为 *Enter password to unlock; select icon to lock.*
- **-invalid** *文本字符串* — 设置密码被认为无效时显示的*文本字符串*；默认为 *Invalid login.*
- **-lockdelay** *秒* — 设置屏幕需要密码解锁前的*秒*数。
- **-logoutButtonHelp** *文本字符串* — 设置注销按钮显示时按钮外显示的消息*文本字符串*。
- **-logoutButtonLabel** *文本字符串* — 设置注销按钮显示时按钮内显示的消息*文本字符串*；默认为 *Logout.*
- **-logoutFailedString** *文本字符串* — 设置注销失败时显示的*文本字符串*。默认为 *Logout attempt FAILED.\n Current user could not be automatically logged out.*
- **-message** *文本字符串* — 指定消息，而非 fortune。
- **-messagefile** *文件名* — 指定一个文件，其内容为消息。
- **-messagesfile** *格式化-文件名* — 指定包含 fortune 消息的文件。第一条记录是 fortune 的数量，下一行包含第一个 fortune。
- **-mfont** *模式-字体名* — 指定与字幕和 nose 模式一起使用的字体。
- **-mode** *模式名* — 设置显示模式。
- **-mono** — 以单色显示。
- **-name** *资源* — 配置`xlock`时使用*资源*代替 Xlock 资源。共有 45 个；有关完整列表，请查看联机手册页。（提示：我们喜欢 **nose** 模式。）
- **-nice** *nice级别* — 设置 nice 级别。
- **-password** *文本字符串* — 在密码提示前显示*文本字符串*；默认为 *Password:*。
- **-program** *程序名* — 指定用于生成 fortune 消息的程序。
- **-resources** — 显示默认资源文件。
- **-saturation** *值* — 设置颜色渐变的饱和度。
- **-timeout** *秒* — 设置密码屏幕超时前的*秒*数。
- **-username** *文本字符串* — 在用户名提示前显示*文本字符串*；默认为 *Name:*。
- **-validate** *文本字符串* — 设置验证密码时显示的*文本字符串*；默认为 *Validating login*。
- **-/+allowroot** — 允许 root 用户登录系统。
- **-/+echokeys** — 为每个输入的键显示 ?。默认不显示任何内容。
- **-/+enablesaver** — 保持屏幕保护程序运行。
- **-/+grabmouse** — 抓取鼠标和键盘（默认）。
- **-/+inroot** — 在根窗口中运行`xlock`。这实际上不会锁定系统。
- **-/+install** — 允许`xlock`使用自己的颜色图。这不能与 *unsupported* 窗口管理器配合使用。
- **-/+inwindow** — 在窗口中运行`xlock`。
- **+/-nolock** — 作为屏幕保护程序工作。
- **-/+remote** — 允许您锁定远程 X 终端。您不应该锁定别人的 X 终端。
- **-/+timeelapsed** — 告诉您机器已锁定多长时间。
- **-/+usefirst** — 将按下的第一个键用作密码的第一个键。默认忽略第一个键，因为它用于引起系统注意。

### xlogo

### 显示 X 徽标

X Window System 命令

`xlogo` *选项*

## 用途

`xlogo`命令显示 X 徽标。这在贸易展览会上非常有用，当旁观者想知道运行的是什么操作系统时。

## 选项

- **-shape** — 将徽标窗口显示为形状而非矩形。

### xlsatoms

### 列出原子

X Window System 命令

`xlsatoms` *选项*

## 用途

`xlsatoms`命令列出服务器中的内部原子。列出从 1 开始的所有原子（协议定义的最低原子值）。

## 选项

| 选项 | 说明 |
|--------|-------------|
| -format *字符串* | 指定用于列出每个原子的`printf`样式字符串。默认值为 `%ld\t%s`。 |
| -name *字符串* | 指定要列出的单个原子。 |
| -range [*低*]-[*高*] | 指定要检查的原子值范围。 |

### xlsclients

### 列出 X 客户端

X Window System 命令

`xlsclients` *选项*

## 用途

`xlsclients`命令列出在显示器上运行的客户端应用程序。

## 选项

- **-a** — 列出所有屏幕上的客户端，而不仅仅是默认屏幕上的那些。
- **-l** — 以长格式返回信息，除了默认格式中显示的机器名称和命令字符串外，还提供窗口名称、图标名称和类提示。
- **-m** *maxcmdlen* — 指定要打印的命令中的最大字符数。默认值为 10,000。

## 相关命令

`xprop`

`xwininfo`

### xlsfonts

### 列出 X 字体

X Window System 命令

`xlsfonts` *选项*

## 用途

`xlsfonts`命令列出 X Window System 上安装的字体。你可以选择查看所有字体（结果会输出大量信息），或者通过将通配符与 *-pattern* 选项结合使用来缩小文件列表范围。

## 选项

| 选项 | 说明 |
|--------|-------------|
| -1 | 以单列打印信息。 |
| -C | 以多列返回信息。 |
| -fn *模式* | 指定要搜索的字体*模式*。 |
| -l | 在一行上列出字体属性及其名称。 |
| -ll | 除 -l 输出外，还列出字体属性。 |
| -lll | 除 -ll 输出外，还列出字符度量。 |
| -m | 列出每种字体的最小和最大边界。 |
| -n *列数* | 设置列数。 |
| -o | 执行 **OpenFont**（以及 **QueryFont**，如适用）而非 **ListFonts**。 |
| -u | 保持输出未排序状态。 |
| -w *宽度* | 设置返回信息的字符宽度；默认值为 79。 |

## 相关命令

`xfd`

### xmag

### 放大屏幕

X Window System 命令

`xmag` *选项*

## 用途

`xmag`命令显示屏幕的一部分。你可以在命令行上指定区域，或者使用一个带指针的方块拖动到要放大的区域上方。确定区域后，将弹出一个新窗口，显示放大后的区域。键入 **Q** 或 **Ctrl-C** 将结束程序。

## 选项

- **-source** *几何参数* — 设置要放大区域的大小和位置。
- **-mag** *整数* — 设置放大级别；默认值为 5。

### xman

`xman` *选项*

## 用途

`xman`命令显示联机手册页。它实际上是`man`命令的 X Window System 版本，不过界面更美观。有关 Linux 联机帮助的更多信息，请参阅`man`的条目。

## 选项

| 选项 | 说明 |
|--------|-------------|
| **-bothshown** | 同时显示手册页和手册目录。 |
| **-helpfile** *文件名* | 指定默认以外的帮助文件。 |
| **-notopbox** | 启动时不显示打开菜单。 |
| **-pagesize** *宽x高+X+Y* | 设置所有手册页的大小和位置。 |

## 相关命令

- `apropos`
- `man`
- `whatis`

### xmessage

X Window System 命令

`xmessage` *选项*

## 用途

`xmessage`命令在窗口中显示消息或查询。它基本上是基于 X 的`/bin/echo`。

## 选项

- **-buttons** *按钮,按钮,...* 定义要在消息窗口中显示的按钮。
- **-default** *标签* — 定义标签匹配的按钮为默认按钮。
- **-file** *文件名* — 显示文件。
- **-print** — 将按下的按钮的标签打印到标准输出。

## 相关命令

`cat`

`echo`

### xmodmap

### 修改键位映射

X Window System 命令

`xmodmap` *选项* *文件名*

## 用途

`xmodmap`命令修改 X Window System 下的键位映射。这些用于将事件击键转换为键码。

## 选项

- **-e** *表达式* — 执行*表达式*。
- **-n** — 列出可能的更改而不实际进行更改。
- **-pk** — 在标准输出上显示当前的键位映射表。
- **-pke** — 以表达式的形式在标准输出上显示当前的键位映射表，这些表达式可以反馈给`xmodmap`。
- **-pm** — 在标准输出上显示当前的修饰键映射。
- **-pp** — 在标准输出上显示当前的指针映射。

## 相关命令

`xev`

### xon

### 远程程序

X Window System 命令

```
xon 选项 命令
```

## 用途

`xon`命令在远程机器上运行 X 程序。默认为`xterm -ls`。

## 选项

- **-access** — 在本地运行`xhost`以将远程主机添加到 X 服务器中的主机访问列表。`xhost`需要修改访问列表的权限才能正常工作。
- **-debug** — 在调试模式下工作，保持 stdin、stdout 和 stderr 不变。
- **-name** *窗口名称* — 为默认的`xterm`命令指定应用程序名称和窗口标题。
- **-nols** — 不向`xterm`传递 **-ls** 选项。
- **-screen** *屏幕编号* — 设置传递给远程命令的 DISPLAY 变量的屏幕编号。
- **-user** *用户名* — 向远程机器传递除自己以外的用户名。

### xpaint

### X 绘图程序

X Window System 命令

`xpaint` *选项* *文件名*

## 用途

`xpaint`命令启动绘图程序。它允许同时编辑多个图像，并支持多种格式，包括 PPM、XBM、TIFF 等。

## 选项

- **-size** — 设置新图像的默认宽度和高度。
- **-12** — 使用 12 位伪彩色视觉。
- **-24** — 使用 24 位真彩色视觉。

### xpmroot

### 设置根窗口图像

X Window System 命令

`xpmroot` *文件名*

## 用途

`xpmroot`命令将当前 X 显示的根窗口设置为命令行中由*文件名*指定的 XPM 像素图。

### xprop

### 显示 X 属性

X Window System 命令

`xprop` *选项*

## 用途

`xprop`命令显示 X 服务器中的窗口和字体属性。你可以在命令行上选择窗口或字体，或者单击窗口以显示其属性。

## 选项

- **-f** *名称 格式 [d格式]* — 为*名称*指定*格式*和*d格式*。
- **-font** *字体* — 返回字体*字体*的属性。
- **-frame** — 改为返回有关窗口管理器边框的信息。
- **-fs** *文件* — 使用*文件*作为更多属性格式的来源。
- **-grammar** — 打印所有命令行选项的详细语法。
- **-id** *id* — 在命令行上选择窗口*id*作为要检查的窗口。
- **-name** *名称* — 指定名为*窗口*的窗口为要检查的窗口。
- **-len** *n* — 返回任何属性的*n*个字节（或更少）。
- **-notype** — 忽略每个属性的类型。
- **-remove** *属性名* — 从窗口中移除属性的名称。
- **-root** — 使用根窗口作为要检查的客户端窗口。
- **-spy** — 无限期检查窗口属性，查找属性更改事件。

## 相关命令

`xwininfo`

### xrdb

### X 资源数据库

X Window System 命令

`xrdb` *选项(s) 文件名*

## 用途

`xrdb`命令返回或设置 screen 0 根窗口上的 RESOURCE_MANAGER 属性，或任意/所有屏幕根窗口上的 SCREEN_RESOURCES 属性，或同时处理两者。通常从 X 启动文件中运行此程序。

此处涵盖的信息包括颜色设置、字体管理等。RESOURCE_MANAGER 属性用于应用于显示的所有屏幕的资源。每个屏幕上的 SCREEN_RESOURCES 属性指定用于该屏幕的附加（或覆盖）资源。

## 选项

- **-all** — 对显示的所有屏幕的 RESOURCE_MANAGER 以及 SCREEN_RESOURCES 执行操作。
- **-backup** *字符串* — 将*字符串*附加到备份文件。
- **-cpp** *文件名* — 指定要使用的 C 预处理程序的路径名。
- **-edit** *文件名* — 将指定属性的内容放入*文件名*中。
- **-global** — 仅对 RESOURCE_MANAGER 属性执行操作。
- **-load** — 将输入加载为指定属性的新值，替换旧内容。
- **-merge** — 将输入与指定属性的当前内容合并，而非替换它们。
- **-n** — 将更改显示到指定属性（与 **-load**、**-override** 和 **-merge** 一起使用时）或资源文件（与 **-edit** 一起使用时）应显示在标准输出上，但不执行。
- **-nocpp** — 在将输入文件加载到属性之前，不通过预处理器运行它。
- **-override** — 将输入添加到指定属性的当前内容中，而非替换它们，新条目覆盖先前条目。
- **-query** — 将指定属性的当前内容打印到标准输出。
- **-quiet** — 抑制有关重复条目的信息。
- **-remove** — 从服务器中删除指定属性。
- **-retain** — 如果`xrdb`是第一个客户端，则不重置服务器。此选项的用处颇有争议，因为`xrdb`成为任何 X 服务器的第一个客户端的可能性极小。
- **-screen** — 仅对显示的默认屏幕的 SCREEN_RESOURCES 属性执行操作。
- **-screens** — 仅对显示的默认屏幕的 SCREEN_RESOURCES 属性执行操作。对于 **-load**、**-override** 和 **-merge**，输入文件将为每个屏幕处理。
- **-symbols** — 将预处理器定义的符号打印到标准输出。
- **-Dname[=value]** — 定义符号以用于以下条件：
- **-Idirectory** — 指定用于查找包含文件的目录。
- **-Uname** — 删除此符号的任何定义。

### xrefresh

### 刷新屏幕

X Window System 命令

```
xrefresh *选项(s)*
```



## 用途

`xrefresh` 命令重绘您的全部或部分屏幕。它在屏幕的所需区域上映射一个窗口，然后立即取消映射它，从而向所有应用程序发送刷新事件。

## 选项

- `-black` 在重绘屏幕之前关闭显示器一秒钟。
- `-none` 没有任何花招地重绘所有窗口。这是默认设置，而且理应如此。
- `-root` 使用根窗口背景。
- `-solid` *颜色* 使用指定颜色的 solid 背景。
- `-white` 使用白色背景，这会导致屏幕在重绘前出现明亮的闪烁。

## xset

### 设置选项

X Window System 命令

```
xset *选项(s)*
```

## 用途

`xset` 命令用于设置 X Window System 的各个方面。注销时，这些设置将重置为默认值。

## 选项

| 选项 | 描述 |
|--------|-------------|
| `b` | 设置蜂鸣器音量、音调和持续时间。您可以使用三个数字参数、前置破折号（`-`）或开/关标志进行设置。如果未给定参数，则恢复系统默认值。 |
| `bc` | 控制错误兼容模式。早期的 X Window System 客户端（Release 4 之前创建的）向服务器发送非法请求，而旧服务器会忽略非法请求。 |
| `c` | 指定按键点击。您可以使用可选值、前置破折号（`-`）或开/关标志进行设置。如果未给定参数，则使用系统默认值。如果使用破折号或关闭标志，将禁用按键点击。0 到 100 之间的值表示最大音量百分比。 |
| `fp=路径` | 设置字体路径。 |
| `fp default` | 将字体路径重置为默认值。 |
| `fp rehash` | 将字体路径重置为其当前值，告诉服务器重新读取当前字体路径中的字体数据库。 |
| `-fp 条目` | 从字体路径中删除 *条目*。条目必须是逗号分隔列表。 |
| `+fp 条目` | 将 *条目* 前置到字体路径。条目必须是逗号分隔列表。 |
| `fp+` | 将 *条目* 附加到字体路径。条目必须是逗号分隔列表。 |

- `led` 设置键盘 LED。它接受可选整数、前置破折号（`-`）或开/关标志。无参数时，所有 LED 都打开。有前置破折号或关闭标志时，所有 LED 都关闭。1 到 32 之间的值表示 LED 将根据是否存在前置破折号而打开或关闭。
- `m` 控制鼠标参数，即 *加速* 或 *阈值*。*加速* 是整数或简单分数，而 *阈值* 是整数。当鼠标在短时间内移动超过 *阈值* 像素时，它的移动速度将加快 *加速* 倍。如果未使用参数或使用了默认标志，则使用系统默认值。
- `p` 设置像素颜色值。参数是以十进制表示的颜色图条目编号和颜色规范。在某些服务器上，可以通过更改 *BlackPixel* 和 *WhitePixel* 的条目来更改根背景颜色。服务器可以选择私有分配这些颜色，在这种情况下将生成错误。
- `r` 设置自动重复速率。前置破折号或关闭标志将禁用自动重复。无参数或开启标志时，将启用自动重复。
- `s` 设置屏幕保护程序参数。标志可以是 `blank/noblank`、`expose/noexpose`、`on/off` 和 `activate/reset`。
- `q` 返回当前设置。

## 相关命令

- `xmodmap`
- `xrdb`
- `xsetroot`

## xsetroot

### 设置根参数

X Window System 命令

```
xsetroot 选项(s)
```

## 用途

`xsetroot` 命令控制 X 显示器上背景（根）窗口的设置。您真的不应该经常传递这些参数；通常，您会在命令行上测试，然后将结果发送到 X 启动文件中。

无选项时，系统恢复为其默认状态。一次只能指定一个背景颜色/平铺更改选项（`-solid`、`-gray`、`-grey`、`-bitmap` 和 `-mod`）。

## 选项

- `-bg` *颜色* — 将 *颜色* 设置为背景颜色。
- `-bitmap` *文件名* — 将 *文件名* 中的位图设置为窗口图案。
- `-cursor` *光标文件 掩码文件* — 指定新的光标文件。
- `-cursorname` *光标名称* — 从标准光标集中指定新光标。
- `-def` — 将未指定的属性重置为默认值。
- `-fg` *颜色* — 将 *颜色* 指定为前景颜色。
- `-gray` — 使背景变为灰色。
- `-grey` — 使背景变为灰色。
- `-mod` x y — 在屏幕上实现类似格子的网格图案。x 和 y 值为 1 到 16 之间的整数。
- `-rv` — 反转前景和背景颜色。
- `-solid` *颜色* — 将 *颜色* 设置为根窗口的背景。
- `-name` *字符串* — 将 *字符串* 设置为根窗口的名称。

## 相关命令

- `xrdb`
- `xset`

## xsm

### X 会话管理器

X Window System 命令

```
xsm *选项*
```

## 用途

`xsm` 命令启动 X 会话管理器。会话是一组处于各种状态的应用程序。你可以为各种用途设置不同的会话。退出会话后，应用程序的状态将作为会话的一部分保存。

运行该命令时，会加载一个会话菜单，让你在不同的会话之间进行选择。

## 选项

- `-session` *sessionName* — 加载 *sessionName*，不显示会话菜单。

## 相关命令

- `smproxy`
- `rstart`

## xsmclient

### 测试会话管理器

X Window System 命令

## 用途

`xsmclient` 测试 X 会话管理器。

## 相关命令

- `xsm`

## xspread

### X 电子表格

X Window System 命令

```
xspread 选项 文件名
```

## 用途

`xspread` 命令是在 X Window System 下运行的功能非常强大的电子表格。你需要查看在线文档（具体来说是文件 `xspread.tex` 中的 Xspread 参考手册），以了解其众多功能的概况。

## 选项

- `-c`：按列顺序重新计算。默认为按行顺序。
- `-m`：使用手动重新计算；仅重新计算以 `@` 开头的值。否则，当值更改时，所有单元格都会重新计算（默认）。
- `-n`：以标准数据输入模式工作，用户必须指定数据输入项是数字还是标签。
- `-r`：按行顺序重新计算（默认）。
- `-x`：加密文件。

## 相关命令

- `bc`
- `sc`

## xstdcmap

### X 色彩映射工具

X Window System 命令

```
xstdcmap *选项*
```

## 用途

`xstdcmap` 命令定义标准色彩映射属性。通常你不会从命令行使用此命令，而是将其作为 X 启动脚本的一部分。

## 选项

- `-all` — 定义所有六种标准色彩映射属性。
- `-best` — 指示应定义 `RGB_BEST_MAP`。
- `-blue` — 指示应定义 `RGB_BLUE_MAP`。
- `-default` — 指示应定义 `RGB_DEFAULT_MAP`。
- `-delete` *map* — 删除指定的标准色彩映射属性，可选 **default**、**best**、**red**、**green**、**blue**、**gray** 或 **all**。
- `-gray` — 指示应定义 `RGB_GRAY_MAP`。
- `-green` — 指示应定义 `RGB_GREEN_MAP`。
- `-red` — 指示应定义 `RGB_RED_MAP`。

## xterm

### X 终端模拟器

X Window System 命令

```
xterm 选项
```

## 用途

`xterm` 命令在 X 下启动一个终端模拟窗口。它本质上让你通过窗口访问 Linux 命令行，因此可能是 Linux 中使用最频繁的 X 命令。

## 选项

`xterm` 有很多选项，包括控制冷门终端模拟器中列数的选项。这里，我们将介绍主要选项；更多详细列表请查看联机手册页。

- `-ah` — 始终高亮显示文本光标。
- `+ah` — 仅在文本光标位于有焦点的窗口上时高亮显示。
- `-aw` — 开启自动环绕。
- `-b` *number* — 设置内边框大小（字符外边缘与窗口边框之间的距离），单位为像素。默认为 2。
- `-cr` *color* — 设置文本光标的颜色。
- `-e` *program args* — 在 `xterm` 窗口中运行 *program*。此选项必须出现在命令行的最后。
- `-fb` *font* — 设置粗体文本的字体。
- `-j` — 设置跳跃滚动，可一次滚动多行。
- `-ls` — 将 `xterm` 窗口中启动的 shell 设置为登录 shell。
- `-ms` *milliseconds* — 设置多次点击选择之间的最大时间间隔。
- `-ms` *color* — 设置指针光标的颜色。

## 心地勇敢做学问

——上海天文台成立20周年之际访王绶琯先生

**【编者按】王绶琯先生是我国著名天文学家，中国现代天文学的开拓者，紫金山天文台的创建者。曾任紫金山天文台和上海天文台台长，上海天文台名誉台长。中科院院士叶叔华曾评价王先生道："王绶琯的名字与中国现代天文学的历史相联系。王绶琯是中国现代天文学的奠基人。"新中国成立后的几年中，全国所有的天文研究机构都与他的名字有关。他是当之无愧的我国现代天文学界的"帅才"。**

2012年7月，上海天文台迎来50周年台庆。SAO NEWS 专程采访了王绶琯先生。

**SAO NEWS：** 王先生，您被任命上海天文台台长的时间很有意思。能否请您讲讲当时任命的具体情况？

**王绶琯**：其实，当时任命我任上海天文台代理台长，我并不是决定去还是不去。在到上海任命之前，我是紫金山天文台台长，在南京有很多学术事务要处理。后来中科院组织部门定了，意思是我兼任。后来当要任命我上海天文台台长时，我也想了想不去，想把紫金山天文台台长辞掉。不过一问，还是兼任，所以就没去成。

**SAO NEWS：** 您被任命时，情况如何？天文台是在什么情况下成立的？

**王绶琯**：关于我们台成立的时间，众说不一。当时上海天文台不是一个新成立的机构，中科院在上海的研究机构很多，中科院组织部门把这些机构合并成几个大所。上海天文台是由原来的上海天文研究机构——佘山观象台和佘山人造卫星观测站合并组建的，再加上原来属于紫金山天文台的授时和纬度站的人员。当时任命佘山观象台原台长王燮奎为副台长。由于合并，也给上海天文台带来了一批人才，比如常和、张和、施智发等现在还在岗的同志。王燮奎当时身体不好，施智发还未平反。另外，新侯看我过来，因为解放前我是他老师。他说既然是成立新所，名义上还是按新所来办，所以按新所来建所，1970年上海天文台单独成立。

## xv

### 图像查看器

X Window 系统命令

```
xv *选项 文件名*
```

## 用途

`xv` 图像编辑器可显示 GIF、JPEG、TIFF、PBM、PGM、PPM、X11 位图、Utah Raster Toolkit RLE、PDS/VICAR、Sun Rasterfile、BMP、PCX、IRIS RGB、XPM、Targa、XWD、PostScript 和 PM 格式的图像。它还可以用于以任意这些格式生成屏幕截图。

要使用此命令，你需要查阅文档，该文档超过 100 页。它是 PostScript 格式的，可以在 `/usr/doc/xv/xvdocs.ps` 找到。

## 相关命令

`xvpictoppm`

## xvidtune

### 视频模式调节器

X Window 系统命令

```
xvidtune *选项*
```

## 用途

`xvidtune` 命令允许你通过 XFree86 X 服务器视频模式扩展来微调视频性能。使用选项时，`xvidtune` 提供命令行界面来切换视频模式或获取/设置显示器节能超时时间。不使用选项时，`xvidtune` 显示各种按钮和滑块，可以交互式地调整现有视频模式。生成的输出可以插入到 `XF86Config` 文件中。

## 选项

| 选项 | 描述 |
|--------|-------------|
| `-next` | 切换到下一个视频模式。 |
| `-prev` | 切换到上一个视频模式。 |
| `-unlock` | 打开模式切换键盘组合。 |
| `-saver` *暂停时间* [*关闭时间*] | 设置 *暂停* 和 *关闭* 屏幕保护程序的不活动超时时间。数值单位为秒。 |
| `-query` | 显示显示器参数和扩展屏幕保护程序超时时间。 |

## 相关命令

`XF86Config`

## xvpictoppm

### Xv 转换

X Window 系统命令

```
xvpictoppm
```

## 用途

`xvpictoppm` 命令将 `xv` 创建的缩略图文件转换为标准可移植像素图格式文件。

## 相关命令

`xv`

## xwd

### X Window 转储

X Window 系统命令

```
xwd *选项*
```

## 用途

`xwd` 命令创建屏幕或屏幕某一部分的截图并保存到文件中。随后可以打印或转换为其他文件格式。运行此命令后，光标变为小十字准线图标；将光标置于要捕获的窗口上并按鼠标左键。将光标置于屏幕背景或根窗口上将捕获整个屏幕。系统声音指示截图的开始和结束。

`xv` 命令也可以更方便地创建截图。

## 选项

- `-add` *数值* — 向每个像素添加 *数值*。
- `-frame` — 在截图中专门包含窗口管理器边框。
- `-icmmap` — 使用整个屏幕的第一个已安装颜色映射来获取 RGB 值，而非所选窗口的颜色映射。
- `-id` *id* — 通过指定 *id* 而非指针来指定窗口。
- `-name` *名称* — 指定应捕获具有 `WM_NAME` 属性的窗口。
- `-nobdrs` — 不将窗口边框作为截图的一部分捕获。
- `-out` *文件* — 指定存储捕获图像的文件。
- `-root` — 自动捕获根窗口作为截图。
- `-screen` — 自动捕获根窗口作为截图。
- `-xy` — 指定 xy 格式捕获。

## 相关命令

`xpr`
`xwud`

## xwininfo

### X Window 信息

X Window 系统命令

```
xwininfo 选项
```

## 用途

`xwininfo` 命令显示有关特定窗口的系统信息。你可以用鼠标选择目标窗口，在命令行上通过 ID 指定窗口，或在命令行上命名窗口。

## 选项

- `-all`：请求所有信息。
- `-bits`：返回有关所选窗口原始位信息以及所选窗口存储方式的信息，包括所选窗口的位重力、窗口重力、后备存储提示、后备平面值、后备像素，以及窗口是否设置了保存下层。
- `-children`：返回有关所选窗口的根窗口、父窗口和子窗口的信息。
- `-english`：返回所选窗口的英制信息—分别显示高度、宽度以及 x 和 y 位置，单位为英寸和像素数。
- `-events`：显示所选窗口的事件掩码。
- `-frame`：手动选择窗口时包含窗口管理器边框。
- `-id` *id*：通过其 *id* 指定要返回窗口信息的窗口。
- `-int`：将窗口 ID 显示为整数值，而非默认的十六进制值。
- `-metric`：返回所选窗口的公制信息—分别显示高度、宽度以及 x 和 y 位置，单位为毫米和像素数。
- `-name` *名称*：通过其 *名称* 指定要返回窗口信息的窗口。
- `-root`：返回根窗口的信息。
- `-shape`：显示所选窗口的边框形状范围。
- `-size`：显示所选窗口的大小提示，包括正常大小提示和缩放大小提示、用户提供的位置、程序提供的位置、用户提供的尺寸、程序提供的尺寸、最小尺寸、最大尺寸、调整大小增量，以及最小和最大纵横比（如有）。
- `-stats`：返回有关指定窗口的大量信息，包括窗口位置、宽度和高度、深度、边框宽度、类别、颜色映射 ID（如有）、映射状态、后备存储提示，以及角的位置。
- `-tree`：返回有关所选窗口的根窗口、父窗口和子窗口的信息，并递归显示所有子窗口。
- `-wm`：返回有关所选窗口的窗口管理器提示信息，包括应用程序是否接受输入、窗口的图标窗口编号和名称、窗口图标应放置的位置，以及窗口的初始状态应为何种状态。

## 相关命令

`xprop`

## xwud

### 显示 XWD 截图

X Window 系统命令

```
xwud *选项*
```

## 用途

`xwud` 显示 `xwd` 命令保存的窗口。

## 选项

- `-in` *文件* — 指定要显示的文件。
- `-new` — 创建新的颜色映射来显示图像。
- `-noclick` — 不允许窗口中的任何按钮按下终止程序。
- `-plane` *数值* — 指定要显示的图像的单个位平面。
- `-raw` — 使用现有颜色值来显示图像。
- `-rv` — 反转视频。
- `-std` *映射类型* — 使用指定的标准颜色映射显示图像。
- `-vis` *视觉类型或id* — 指定视觉或视觉类别。

## 相关命令

`xwd`

## yes

### 永久显示参数

GNU 命令

```
yes *字符串*
```



## 用途

`yes` 命令永久打印命令行参数，参数之间以空格分隔并后跟换行符，直到被终止。

### 摘要

## 引言

在本文中，我们提出了一种用于 3D 形状生成的深度学习新框架。我们的方法结合了变分自编码器（`VAE`）和生成对抗网络（`GAN`）的优势，以从 2D 图像输入生成高质量的 3D 模型。

## 相关工作

3D 形状生成在计算机图形学和计算机视觉领域已经得到了广泛研究。早期方法依赖手工设计的特征和基于模板的方法 [1]。随着深度学习的出现，基于神经网络的方法取得了显著进展 [2, 3]。

近期研究探索了 3D 形状的各种表示方法，包括体素网格 [4]、点云 [5] 和隐函数 [6]。然而，这些方法往往在生成精细几何细节和保持方面存在困难。

我们的方法通过引入一种混合表示来解决这些局限性，该表示能有效捕获局部和全局形状属性。

## 文件管理命令

这些命令用于管理你的文件和目录—移动它们、复制它们、删除它们、压缩它们，等等。

### `basename`

### 基名列表

GNU 命令

`basename *文件名.后缀*`

## 用途

`basename` 命令（如果在命令行上指定）去除前导目录和后缀。

### 示例

```
$ basename changes.txt

changes
```

## `cd`

## 切换目录

```
cd *directory*
```

## 用途

`cd` 命令用于更改当前目录。虽然这实际上是一个 shell 命令，但通常被视为标准的 Linux 命令。

### 示例

```
$ cd
```

这将当前目录更改为您的主目录。

```
$ cd /usr/kevin
```

这将当前目录更改为名为`/usr/kevin`的目录。

```
$ cd kevin
```

这将您的目录更名为名为`kevin`的子目录。

```
$ cd ~
```

这将当前目录更改为您的主目录。

```
$ cd /
```

这将当前目录更改为根目录。

## 相关命令

`pwd`

打印当前目录的名称。

## `chgrp`

## 更改组

```
chgrp option(s) newgroup file(s)/directory
```

## 用途

`chgrp` 命令用于更改与文件或目录相关联的组分配。可以将组 ID 或组名称分配给文件或目录（该信息存储在`/etc/groups`中）。要更改组，您必须拥有该文件或是 root 用户。

## 选项

- **`-c`**：打印有关所做更改的信息。
- **`-f`**：忽略无法更改的文件的相关信息。
- **`-v`**：以详细形式返回有关更改的所有信息。
- **`-R`**：递归模式，这意味着子目录也会被更改。

### 示例

```
$ chgrp management kevin.memo
```

这将 `kevin.memo` 的组更改为 `restricted` 组。

```
$ chgrp -R management /home/kevin/memos
```

这将目录`/home/kevin/memos`、其内容以及其中所有子目录的组更改为 `restricted` 组。

## 相关命令

- `chown`
- `chmod`

## `chmod`

## 更改模式

```
chmod *option(s)* *mode* *file(s)*
```

## 用途

`chmod` 命令用于更改与文件相关联的权限。权限设置为文件的所有者、文件的组所有者以及所有人。权限以两种形式之一存储：数字形式或符号形式。符号形式用于相对于当前权限设置值，而数字方法用于设置绝对权限。这些值以模式表示，可以是八进制数（使用数字形式时）或符号（使用符号方法时）。如果模式之间用逗号分隔，可以组合使用。

要更改权限，您必须拥有该文件或是 root 用户。

文件的当前权限可以使用 `ls` 命令显示，该命令在本节的其他地方有介绍。`ls` 命令以以下方式列出权限：

`rwxr--w--`

权限按三元组设置：所有者、组和其他人。三者中的任何一个都可以读取（`r`）、写入（`w`）和执行（`x`）。如果拒绝三者之一的权限，则该字母会被连字符（`-`）替代。root 用户对每个文件都有完全权限。

权限是使用 Linux 操作系统时需要注意的更重要的事项之一。许多初学者会因此绊倒，因为他们想要运行或访问某个文件，却发现自己没有权限这样做。

## 符号形式示例

```
$ chmod g+x pat.memo
```

此命令行将执行文件的权限（`x`）添加到组（`g`）。在符号形式中，权限是添加或 subtract 到现有权限的。

```
$ chmod go-w pat.memo
```

此命令行从组和全世界移除写入权限。

```
$ chmod g+x,go-w pat.memo
```

此命令行将执行文件的权限添加到组，同时从组和全世界移除写入权限。

## **符号**

以下符号用于设置模式：

- **`u`**：用户（文件的当前所有者）。
- **`g`**：组。
- **`o`**：其他（全世界）。
- **`all`**：所有（默认）。
- **`+`**：将权限添加到当前权限。
- **`-`**：从当前权限中删除权限。
- **`=`**：分配权限，同时从未指定字段中删除其他权限。
- **`r`**：读取。
- **`w`**：写入。
- **`x`**：执行。
- **`s`**：设置用户 ID。
- **`t`**：设置粘滞位，用于 Linux 系统和 Internet 上的额外安全性。
- **`l`**：设置强制锁。

## **数字形式示例**

```
$ chmod 764 pat.memo
```

此命令行将 `chmod` 与模式 764 结合使用，应用于文件 `pat.memo`。这意味着所有者可以读取、写入和执行文件（这是 7 所指定的），组可以读取文件并写入，但不能执行，而全世界可以读取文件但不能执行或写入。

我们如何得出 764？因为我们把模式的数值相加，这将在下一节中介绍。模式数字的范围可以在 000 到 777 之间；000 表示没有人对文件有任何访问权限，而 777 表示每个人都有对文件的完全访问权限。以下是用于得出 764 的确切计算：

- 400：所有者具有读取权限。
- 200：所有者具有写入权限。
- 100：所有者具有执行权限。
- 040：组具有读取权限。
- 020：组具有写入权限。
- 004：全世界具有读取权限。
- 764：（总计）

使用 `ls` 命令查看相关文件，您会看到它具有以下权限：

```
rwxrw-r--
```

### 模式

模式是以下内容的组合：

- 400：所有者具有读取权限。
- 200：所有者具有写入权限。
- 100：所有者具有执行权限。
- 040：组具有读取权限。
- 020：组具有写入权限。
- 010：组具有执行权限。
- 004：全世界具有读取权限。
- 002：全世界具有写入权限。
- 001：全世界具有执行权限。

## 选项

- **`-c`** 打印有关所做更改的信息。
- **`-f`** 忽略无法更改的文件的相关信息。
- **`-v`** 详细模式，列出更改和失败的更改。
- **`-R`** 递归模式，这意味着子目录也会被更改。

### 四位数模式

偶尔会有四位数模式。在这些情况下，额外的数字实际上在模式的开头，并添加以下权限：

- **`4`** 执行时设置用户 ID。
- **`2`** 执行时设置组 ID。
- **`1`** 设置粘滞位。

## 相关命令

- `chgrp`
- `chown`

## `chown`

## 更改所有者

```
chown option(s) *newowner* *file(s)*
```

## 用途

`chown` 命令用于更改文件或目录的所有权。新所有者可以是用户名（存储在`/etc/passwd`中的一个）或用户 ID 号码。要更改所有权，您必须是该文件的所有者或特权用户（即 root 用户）。

## 选项

- **`-c`** — 打印有关所做更改的信息。
- **`-f`** — 忽略无法更改的文件的相关信息。
- **`-v`** — 详细模式，列出更改和失败的更改。
- **`-R`** — 递归模式，这意味着子目录也会被更改。

### 示例

```
$ chown kevin report
```

这将 `report` 的所有权更改为用户 `kevin`。

## 相关命令

`chmod`
`chgrp`

## `chroot`

更改根目录

```
chroot path
```

## 用途

`chroot` 目录将 Linux 系统的根目录更改为 `path` 中指定的目录。只有 root 用户可以更改根目录。

## `cp` 复制文件

```
cp option(s) file1 file2
cp option(s) file1 directory
cp option(s) directory1 directory2
```

## 用途

`cp` 命令用于复制文件——将一个文件的内容复制到另一个文件、将文件的内容复制到新目录，或从一个目录复制到另一个目录。现有文件不会被更改。

## 选项

- **`-a`** 保留归档属性。
- **`-b`** 创建备份而不是覆盖现有文件。
- **`-d`** 维护文件之间的符号链接。
- **`-f`** 强制复制。
- **`-i`** 打开交互模式，在覆盖现有文件之前会提示您。
- **`-l`** 创建复制到目录的文件之间的硬链接，而不是实际复制文件。
- **`-p`** 保留现有权限，包括所有权和时间戳。
- **`-r`** 复制整个目录及任何子目录。
- **`-R`** 复制整个目录及任何子目录。
- **`-s`** 创建复制到目录的文件之间的符号链接，而不是实际复制文件。
- **`-S`** 为所有新文件设置后缀；默认是 `~`，存储在 `SIMPLE_BACKUP_SUFFIX` 环境变量中。不要更改此变量，因为其他应用程序（特别是 `emacs`）也在使用它。
- **`-u`** 不复制到比现有文件更新的新文件。
- **`-v`** 打开详细模式，所有操作都会打印到屏幕。
- **`-V`** 使用通过 `VERSION_CONTROL` 环境变量设置的版本控制编号。
- **`-x`** 复制时忽略远程文件系统上的子目录。

## `cp`

## 复制文件

### 示例

```
$ cp pat.letter pat.old
```

这会将文件 `pat.letter` 复制到一个名为 `pat.old` 的新文件中。

```
$ cp kevin.letter /home/Kevin/kevin.letter
```

这会将当前目录中的文件 `kevin.letter` 复制到 `/home/Kevin` 目录中存储的文件 `kevin.letter`。

```
$ cp -r /home/Kevin /home/Kevin/letters
```

这会将 `/home/Kevin` 的全部内容复制到目录 `/home/Kevin/letters` 中。

## `dir`

## 列出目录内容

`dir` *选项* *目录*

## 用途

`dir` 命令用于列出目录的内容。它与 `ls` 命令基本相同，但因 MS-DOS 使用 `dir` 而非 `ls` 来列出目录，所以该命令被包含在内。

## 选项

- **`-A`** 不列出 `.` 和 `..`
- **`-a`** 列出以 `.` 开头的隐藏文件
- **`-B`** 忽略以波浪号 (`~`) 开头的备份文件
- **`-b`** 为不可打印字符打印八进制转义序列
- **`-C`** 按列列出条目
- **`-c`** 按更改时间排序；与 `-l` 结合使用时显示更改时间
- **`-D`** 生成适合 `emacs` *dired* 模式的输出
- **`-d`** 列出目录条目而非内容
- **`-e`** 同时列出日期和完整时间
- **`-F`** 为每个条目追加类型标识字符
- **`-f`** 不进行排序，启用 `-aU` 并禁用 `-lsto`
- **`-G`** 禁止显示组信息
- **`-g`** 被 `dir` 忽略；为兼容起见而包含
- **`-I*pattern*`** 忽略匹配 `PATTERN` 的条目
- **`-i`** 打印每个文件的索引编号
- **`-k`** 使用 1024 字节块，而非 512
- **`-L`** 列出符号链接指向的条目
- **`-l`** 使用长列表格式
- **`-m`** 用逗号分隔的条目列表填充宽度
- **`-N`** 不对条目名称加引号
- **`-n`** 列出数字 UID 和 GID 而非名称
- **`-o`** 根据类型以颜色显示文件
- **`-p`** 为每个条目追加类型标识字符
- **`-Q`** 用双引号括起条目名称
- **`-q`** 用问号 (`?`) 代替不可打印字符
- **`-R`** 递归列出子目录
- **`-r`** 排序时以逆序列出
- **`-S`** 按文件大小排序
- **`-s`** 打印每个文件的块大小
- **`-Tcols`** 将制表位设置为每 *cols* 列而非 8
- **`-t`** 按修改时间排序；与 `-l` 一起使用时显示修改时间
- **`-U`** 按目录顺序列出条目，不进行任何排序
- **`-u`** 按最后访问时间排序；与 `-l` 一起使用时显示此时间
- **`-wcols`** 假设屏幕宽度为 *cols* 而非当前值
- **`-X`** 按扩展名字母顺序排序
- **`-x`** 按行而非按列列出条目
- **`-1`** 每行列出一个文件

## `file`

## 确定文件类型

`file` *选项* *文件名*

## 用途

`file` 命令返回给定文件的文件类型。有时需要查阅 magic 文件（`/etc/magic`）。不要过分依赖返回的信息——此命令返回的信息并不总是正确的，它在检测基于文本或以文本为导向的文件类型时效果最佳，如 ASCII 文件、shell 脚本、PostScript 文件和命令。

## 选项

- **`-c`** — 自动检查 magic 文件
- **`-f`** *list* — 对 *list* 中的文件运行 `file` 命令
- **`-L`** — 跟随符号链接
- **`-m`** *file* — 检查 *file* 以确定文件类型，而非使用 magic 文件
- **`-z`** — 检查压缩文件

Linux 命令，按组组织

## `find`

## 查找文件

```
find 路径 条件
```

## 用途

`find` 命令用于查找文件。它可以就这么简单，也可以如您所愿那样复杂。您可以输入任意数量的条件——与文件名相关的通配符、文件创建或最后访问时间、存在什么链接等等。它从根目录或您指定的另一个目录开始遍历目录树。

您可以使用 `find` 命令来判断某人是否真正了解 Linux。如果他们使用 `find` 命令时总是在命令行末尾放置 `-print`，那说明他们了解的是 UNIX，而不是 Linux。在标准 UNIX 中，`find` 命令需要在命令行末尾加上 `-print`，以告诉命令将输出打印到屏幕。然而，Linux 版本不需要 `-print`，因为默认假设您总是想输出到屏幕。所以任何在示例命令行中包含 `-print` 的书籍或杂志文章都表明作者并不真正了解 Linux。

## 选项

| 选项 | 说明 |
|---|---|
| `-amin min` | 查找被访问时间： |
| `+m` | 超过 m 分钟前 |
| `m` | 正好 m 分钟前 |
| `-m` | 少于 m 分钟前 |
| `-anewer file` | 查找修改后被访问的文件 |
| `-atime days` | 查找被访问时间： |
| `+d` | 超过 d 天前 |
| `d` | 正好 d 天前 |
| `-d` | 少于 d 天前 |
| `-cmin min` | 查找被更改时间： |
| `+m` | 超过 m 分钟前 |
| `m` | 正好 m 分钟前 |
| `-m` | 少于 m 分钟前 |
| `-cnewer file` | 查找修改后被更改的文件 |
| `-ctime days` | 查找被更改时间： |
| `+d` | 超过 d 天前 |
| `d` | 正好 d 天前 |
| `-d` | 少于 d 天前 |
| `-daystart` | 假设时间从当天开始计算，而非从现在 |
| `-empty` | 即使文件为空也继续搜索 |
| `-exec command {}` | 找到文件后运行 Linux 命令 |
| `-false` | 如果匹配则返回假值 |
| `-follow` | 跟随符号链接及相关目录 |
| `-fstype type` | 查找存储在特定文件系统类型上的文件：`ufs`、`4.2`、`4.3`、`nfs`、`tmp`、`mfs`、`S51K` 和 `S52K` |
| `-gid num` | 查找属于特定组 `num` 的文件 |
| `-group group` | 查找属于特定组的文件，可以是 ID 或名称 |
| `-iname file` | 搜索指向 word `file` 的符号链接，可包含元字符和通配符，不区分大小写 |
| `-inum num` | 查找具有特定 inode 编号 `num` 的文件 |
| `-ipath name` | 查找匹配 `name` 的文件，`name` 为绝对路径，不区分大小写 |
| `-links num` | 查找具有 `num` 个链接数的文件 |
| `-lname file` | 搜索指向 `file` 的符号链接，可包含元字符和通配符，必须区分大小写 |
| `-maxdepth num` | 在向下遍历 `num` 层目录后停止搜索 |
| `-mindepth num` | 从 `num` 层目录及以下开始搜索 |
| `-mmin min` | 查找被修改时间： |
| `+m` | 超过 m 分钟前 |
| `m` | 正好 m 分钟前 |
| `-m` | 少于 m 分钟前 |
| `-mtime days` | 查找被修改时间： |
| `+d` | 超过 d 天前 |
| `d` | 正好 d 天前 |
| `-d` | 少于 d 天前 |



## find 命令选项

| 选项 | 描述 |
|------|------|
| `-name file` | 查找名为 `file` 的文件，必须区分大小写 |
| `-newer file` | 查找比 `file` 修改时间更近的文件 |
| `-nogroup` | 查找组所有者未在 `/etc/group` 中列出的文件 |
| `-nouser` | 查找所有者未在 `/etc/passwd` 中列出的文件 |
| `-ok command {}` | 找到文件后运行 Linux 命令，并确认您确实要运行该命令 |
| `-path name` | 查找匹配 `name` 的文件，`name` 为绝对路径，区分大小写 |
| `-perm nnn` | 查找权限匹配指定文件权限（如 `rwx`）的文件 |
| `-size num[c]` | 查找包含 `num` 个块的文件，若添加 `c` 则为 `num` 个字符 |
| `-type t` | 返回类型为 `t` 的文件名称，`t` 可以是 `b`（块特殊文件）、`c`（字符特殊文件）、`d`（目录）、`f`（普通文件）、`l`（符号链接）、`p`（管道）或 `s`（套接字） |
| `-user user` | 查找属于指定用户的文件 |

### 示例

```
$ find / -ctime -2
```

这会查找整个文件系统中更改时间少于两天的所有文件。

```
$ find $HOME
```

这会列出您主目录中的所有文件和目录。

## funzip

### 过滤式解压

```
funzip password input_file
```

### 用途

`funzip` 命令是一个通过管道从 ZIP 压缩包中提取文件的过滤器。

### 相关命令

- `gzip`
- `unzip`
- `zip`

## getfilename

### 获取文件名

```
getfilename format-name filename
```

### 用途

`getfilename` 命令用于按要求格式请求用户指定一个文件名。该命令本身单独使用意义不大，但与支持 `mailcap` 的程序（如 `mailto`）结合使用时非常有用。

### 相关命令

- `mailto`
- `metamail`

## gunzip

### 解压压缩文件

GNU 命令

```
gunzip option(s) file(s)
```

### 用途

`gunzip` 命令用于解压由 `gzip` 命令或 UNIX 的 `compress` 和 `pack` 命令压缩的文件。

> 与其他 UNIX 系统不同，Linux 操作系统中没有 `compress` 命令。要解压使用 UNIX `compress` 命令压缩的文件，应使用 `gunzip`。

### 选项

- `-c` — 使用标准输出，不修改原始文件。
- `-N` — 保留原始文件名和时间戳。
- `-q` — 静默模式工作，不返回状态信息。
- `-t` — 测试新文件的数据完整性。
- `-v` — 详细模式工作，将所有更改显示到屏幕上，包括新文件的名称。

### 相关命令

- `gzip`

## gzexe

### 压缩可执行文件

GNU 命令

```
gzexe option file(s)
```

### 用途

`gzexe` 命令用于压缩可执行文件。当你运行被压缩的可执行文件时，它会自动解压并运行。运行压缩后的命令会稍微慢一点，但可以节省宝贵的磁盘空间。

### 选项

- `-d` — 解压被压缩的可执行命令。

## gzip

### 压缩文件

GNU 命令

```
gzip option(s) file(s)
```

### 用途

`gzip` 命令使用 Lempel-Ziv 编码压缩文件。压缩后的文件会被重命名为 `file.gz`，并删除原始文件。新压缩文件会保留与原始文件关联的访问权限和时间戳。

### 选项

- `-c` — 使用标准输出，不修改原始文件。
- `-d` — 解压文件（与 `gunzip` 相同）。
- `-f` — 强制压缩，适用于压缩文件已存在、具有多个链接或已被压缩的情况。
- `-l` — 将已经由 `deflate`、`compress`、`gzip`、`lzh` 或 `pack` 压缩过的文件再次压缩。
- `-N` — 保留原始文件名和时间戳。
- `-q` — 静默模式工作，不返回状态信息。
- `-r` — 递归模式工作，子目录也会被压缩。
- `-S suffix` — 为新的文件名添加指定后缀，代替默认的 `.gz`。
- `-t` — 测试新文件的数据完整性。
- `-v` — 详细模式工作，将所有更改显示到屏幕上，包括新文件的名称。

### 相关命令

- `gunzip`

## ln

### 链接文件

```
ln option(s) originalfile linkfile
```

```
ln option(s) file(s) directory
```

### 用途

`ln` 命令用于链接两个或多个文件。其目的是减少文件占用的磁盘空间，在更大的多用户系统中，多个用户在多种情况下可能会使用相同的文件。虽然你在单用户 Linux 系统上可能觉得没必要链接文件，但如果你管理网络安装，就可能会需要这个功能。而且 Linux 本身在标准安装中就使用了链接；某些 Linux 文件存储在非标准位置，但链接使其看起来像是位于标准位置。

链接有两种类型：硬链接和符号链接。大多数情况下，你应该坚持使用符号链接，因为使用 `ls` 命令更容易跟踪它们。

你可以为两个文件使用相同的名称，也可以为 `linkfile` 使用新名称。始终记住，第一个名称是原始文件，第二个名称是新的链接文件；如果顺序颠倒，会破坏原始文件。

### 选项

- `-b` — 在删除原始文件之前进行备份。
- `-d` — 创建指向目录的硬链接（仅特权用户可用）。
- `-f` — 强制创建链接，不询问是否覆盖现有文件。
- `-F` — 创建指向目录的硬链接（仅特权用户可用）。
- `-i` — 覆盖现有文件前进行确认。
- `-n` — 在取消引用之前替换符号链接。
- `-s` — 创建符号链接。
- `-S` *suffix* — 在备份文件末尾添加 *suffix*，而不是标准的波浪号（`~`）。

### 示例

```
$ ln pat kevin
```

这将文件 `kevin` 链接到 `pat`。

### 相关命令

- `chmod`
- `chown`
- `cp`
- `ls`
- `mv`

## locate

### 定位模式

```
locate option(s) pattern(s)
```

### 用途

`locate` 命令在文件名数据库中定位 *pattern* 并返回匹配的文件名。*pattern* 可以包含 shell 风格的元字符（`*`、`?` 和 `[]`），但 `/` 和 `.` 被视为文件名的一部分。如果没有元字符，则返回数据库中包含该字符串的任意位置的所有文件名。如果包含元字符，`locate` 命令显示包含精确模式的文件名，因此使用元字符时请在模式的开头或结尾加上 `*`。

### 选项

- `-d` *path* — 在 *path* 中搜索文件名数据库，*path* 是以冒号分隔的数据库文件名列表。
- `--help` — 打印选项列表并退出。
- `--version` — 返回 `locate` 版本并退出。

### 相关命令

- `find`
- `locatedb`
- `lockfile`
- `updatedb`
- `xargs`

## locatedb

### 定位文件

GNU 命令

```
locatedb option(s) pattern(s)
```

### 用途

`locatedb` 命令在文件名数据库中定位 *pattern* 并返回匹配的文件名。*pattern* 可以包含 shell 风格的元字符（`*`、`?` 和 `[]`），但 `/` 和 `.` 被视为文件名的一部分。如果没有元字符，则返回数据库中包含该字符串的任意位置的所有文件名。如果包含元字符，`locate` 命令显示包含精确模式的文件名，因此使用元字符时请在模式的开头或结尾加上 `*`。

### 相关命令

- `find`
- `locate`
- `lockfile`
- `updatedb`
- `xargs`

## lockfile

```
lockfile option filename
```

### 用途

`lockfile` 命令创建一个或多个信号量文件，用于限制对文件的访问。如果 `lockfile` 无法按顺序创建信号量文件，它会等待八秒钟然后重试；你可以使用 `-r` 选项指定重试次数。生成的文件访问权限为 `0`，需要使用 `rm -f` 删除。

### 选项

- `-r` *num* — 在放弃之前重试 *num* 次。

### 相关命令

- `rm`

## ls

### 列出文件

GNU 命令

```
ls option(s) name(s)
```

### 用途

`ls` 命令用于列出指定目录的内容或指定文件的扩展信息。如果没有给出名称，则假定你要查看当前目录的内容。默认情况下，文件以列的形式按垂直方向排序。虽然这是一个复杂的命令，尤其是选项繁多的 GNU 版本（有 38 个选项），但你很可能最常使用 `-F` 和 `-l` 选项，最少使用 `-u` 和 `-c` 选项。

### 选项

- `-1` — 每行列出一个文件。
- `-7` — 将 ASCII（ISO 646）范围（`0x20`-`0x7E`）之外的所有字符视为不可打印的控制字符。
- `-8` — 将 8 位 ISO 8859 字符集（`0x20`-`0x7E`、`0xA1`-`0xFF`）中的所有字符视为可打印字符，包括 ASCII。（默认设置。）
- `-a` — 列出目录中的所有文件，包括隐藏文件。
- `-A` — 列出目录中的所有内容，但排除 `.` 和 `..`。
- `-b` — 使用字母和八进制反斜杠序列显示非图形字符，类似于 C 语言中的用法。
- `-B` — 忽略备份文件（以 `~` 结尾的文件）。
- `-c` — 按状态更改时间排序内容。
- `-C` — 以列的形式列出文件，按垂直方向排序。
- `-d` — 像其他文件一样列出目录，不显示其内容。
- `-e` — 完整列出所有时间。
- `-f` — 按磁盘中的顺序显示内容，不进行任何排序。
- `-F` — 用字符列出文件类型：`/` 表示目录，`@` 表示符号链接，`|` 表示 FIFO，`=` 表示套接字，普通文件不显示任何字符。

### 续

- `-G` — 以长格式列出文件时省略组所有权。
- `-i` — 显示每个文件的索引编号。
- `-I` *pattern* — 忽略与 *pattern* 匹配的文件。
- `-k` — 以千字节为单位列出文件大小。
- `-l` — 以长格式列出文件，包括文件类型、权限、硬链接数量、所有者名称、组名称、以字节为单位的大小以及时间戳（除非选择其他时间，否则为修改时间）。
- `-L` — 通过符号链接显示文件，而不是列出链接的内容。
- `-m` — 水平列出文件，以逗号分隔。
- `-n` — 列出数字 UID 和 GID，而不是文件名。
- `-N` — 在列表中省略文件名。
- `-o` — 切换按颜色显示文件。
- `-p` — 为每个文件名追加一个表示类型的字符。
- `-q` — 在文件名中的非图形字符位置打印问号。
- `-Q` — 将文件名用双引号（`"`）括起来，并以类似 C 语言的方式显示非图形字符。
- `-r` — 按反向顺序排列文件名。
- `-R` — 递归列出目录的内容。
- `-s` — 在文件名左侧打印文件大小（以 1K 块为单位）。
- `-S` — 按文件大小而非字母顺序排序文件，最大的文件在前。
- `-t` — 按时间戳（最新的在前）而非字母顺序排序文件。
- `-T` *cols* — 将制表位设置为 *cols* 列。默认值为 8。设置为 0 则禁用制表符。
- `-u` — 按文件最后访问时间而非修改时间排序。
- `-U` — 按在磁盘上发现的顺序显示内容，不进行任何排序。
- `-w` *cols* — 将屏幕宽度设置为 *cols* 个字符。默认值为 80。
- `-x` — 以列的形式打印列表，按水平方向排序。
- `-X` — 按文件扩展名字母顺序排序文件。

## Midnight Commander

```
mc 选项 目录1 目录2
```

### 用途

`mc` 命令启动 Midnight Commander，这是一个适用于 Linux 的目录浏览器和文件管理器，不需要 X Window 系统。它允许你移动、复制和删除文件及目录，可以通过鼠标操作和下拉菜单，也可以像在 `vi` 中一样在命令行输入命令。

Midnight Commander 有大量相关命令；更多详情请参阅在线手册页。

### 选项

- `-b`：以黑白模式工作。
- `-c`：以彩色模式工作。
- `-C` *参数*：使用 *参数* 指定的颜色集，而非默认颜色集。
- `-d`：关闭鼠标支持。
- `-f`：显示 Midnight Commander 文件的编译内置搜索路径。
- `-l` *文件*：将 `ftpfs` 与服务器的对话保存到文件。
- `-P`：在 Midnight Commander 退出后打印最后的工作目录。（请参阅手册页中关于 shell 脚本的部分，此选项非常实用。）
- `-s`：以慢速模式工作，此时线条绘制被抑制，详细模式关闭。
- `-t`：使用 `TERMCAP` 获取终端信息。
- `-u`：禁用并发 shell。
- `-U`：启用并发 shell。
- `-v` *文件*：启动内部查看器查看文件。
- `-x`：在 `xterm` 下工作。

## mkdir

### 创建目录

GNU 命令

```
mkdir 选项 目录
```

### 用途

`mkdir` 命令用于创建目录。新目录的默认模式为 `0777`。

### 选项

- `-m` *模式* — 将新目录的模式设置为 *模式*。
- `-p` — 根据需要创建新的父目录。

## mkdirhier

### 创建目录层次结构

```
mkdirhier 目录
```

### 用途

`mkdirhier` 创建目录层次结构。此命令已被 GNU 版本的 `mkdir`（单独介绍）所取代，后者可以创建目录层次结构。

### 相关命令

- `mkdir`

## mkfifo

### 创建 FIFO

GNU 命令

```
mkfifo 选项 文件名
```

### 用途

`mkfifo` 创建 FIFO，即命名管道。新 FIFO 的模式为 `0666`。

### 选项

- `-m` *模式* — 将新 FIFO 的模式设置为 *模式*。

## mkfontdir

### 创建字体目录

X Window 系统命令

```
mkfontdir 目录
```

### 用途

`mkfontdir` 在指定的 *目录* 中创建 X 字体文件的索引 `fonts.dir`。没有选项可以更改此文件名，你也不希望更改——这是 X 字体服务器和 X 服务器查找字体信息时使用的名称。

### 相关命令

- `xfs`
- `xset`

## mkmanifest

### 恢复 UNIX 文件名

```
mkmanifest 文件
```

### 用途

`mkmanifest` 命令创建一个 shell 脚本，用于恢复因 MS-DOS 文件名限制而被截断的 Linux 文件名。

### 相关命令

- `arc`
- `pcomm`
- `mtools`

## mknod

### 创建特殊文件

GNU 命令

```
mknod 选项 文件名 文件类型 主设备号 次设备号
```

### 用途

`mknod` 命令使用给定的 *文件名* 创建特殊文件（FIFO、字符特殊文件或块特殊文件）。这些文件的默认模式为 `0666`。*文件类型* 可以是以下之一：

| 文件类型 | 描述 |
|----------|-------------|
| `p` | FIFO |
| `b` | 块（缓冲）特殊文件 |
| `c` | 字符（非缓冲）特殊文件 |
| `u` | 字符（非缓冲）特殊文件 |

*主设备号* 和 *次设备号* 指的是主要和次要设备编号。

### 选项

- `-m` *模式* — 将新文件的模式设置为 *模式*。这是一个符号值。

## mv

### 移动文件

```
mv 选项 源文件 目标
```

### 用途

`mv` 命令移动文件——或者更准确地说，给它们一个新的名称和在文件层次结构中的新位置。如果目标指定为一个目录，`mv` 将源文件移动到该目录中同名的文件中。否则，如果给出两个文件作为源和目标，它将第一个文件移动到第二个文件上。

如果新文件不可写，`mv` 会要求你确认是否要覆盖该文件。

### 选项

- `-b`：在删除文件之前创建备份。
- `-f`：删除现有的目标文件，不提示你。
- `-i`：在覆盖目标文件之前提示你。
- `-S`：设置备份的新后缀；系统默认为 `~`。
- `-u`：拒绝将文件移动到具有相同或更新修改时间的目标位置。
- `-v`：详细模式；在移动每个文件之前打印其名称。

### 相关命令

- `cp`

## newgrp

### 新组

```
newgrp GID
```

### 用途

`newgrp` 命令在你已经登录系统后更改你的组权限。如果你不指定新的 GID，则使用你的登录 GID。

### 相关命令

- `login`
- `group`

## pwd

### 打印工作目录

GNU 命令

```
pwd
```

### 用途

`pwd` 命令打印当前（工作）目录的名称。

## rm

### 删除文件

GNU 命令

```
rm 选项 文件名
```

### 用途

`rm` 命令从 Linux 文件系统中删除目录。在实际删除文件之前，系统会提示你。

与标准 UNIX 版本的 `rm` 不同，此 GNU 版本默认不删除目录。

### 选项

- `-d`：使用 `unlink` 命令而非 `rmdir` 命令删除链接的目录。（只有 root 用户才能访问 `-d` 选项。）



- `-f`：忽略不存在的文件。
- `-i`：显式设置在删除文件之前进行提示。
- `-r`：递归删除目录的内容。
- `-v`：在详细模式下工作，在删除每个文件之前打印其名称。

按组组织的Linux命令

## rmdir

GNU命令

`rmdir` *选项 目录*

## 用途

`rmdir`命令删除空目录。有内容的目录不会被删除。

## 选项

- `-p` 如果父目录作为命令行的一部分被提及，则删除它们。

## shrinkfile

## 缩小文件

`shrinkfile` *选项 文件名*

## 用途

`shrinkfile`命令按行边界缩小文件，保留文件末尾的数据。截断在行边界上进行，其中行是一系列以换行符结尾的字节。没有行长度限制，文件可以包含任何二进制数据。

## 选项

- `-s` *数值* — 将最大大小更改为*数值*。
- `-v` — 如果文件被缩小，则打印状态行。

## size — 列出大小

GNU 命令

`size` *选项 目标文件*

## 用途

`size` 命令列出各节区的大小以及命令行中指定的*目标文件*的总大小。每个文件生成一行输出。

## 选项

| 选项 | 说明 |
|--------|-------------|
| `-A` | 输出类似于 System V `size` 的输出。 |
| `-B` | 输出类似于 Berkeley `size` 的格式。 |
| `-d` | 大小以十进制列出。 |
| `-o` | 大小以八进制列出。 |
| `-x` | 大小以十六进制列出。 |
| `--target` *bfdname* | 将目标代码格式指定为 *bfdname*。 |

## sq — 压缩词表

```
sq 输入文件 输出文件
```

## 用途

`sq` 命令压缩已排序的词表。它通常用于大型文本文件，如词典。压缩的方式是通过消除共同前缀并用单个字符替代，该字符编码了与前一单词共享的字符数。

## 相关命令

`unsq`

## sum — 文件校验和

GNU 命令

`sum` *选项 文件名*

## 用途

`sum` 对文件执行校验和计算并统计块数。它为每个指定文件计算一个 16 位校验和。它打印每个文件的校验和以及该文件的块数。GNU 版本的 `sum` 使用与 BSD `sum` 兼容的算法计算校验和，并以 1K 块为单位打印文件大小。

## 选项

- `-r` — 使用与 BSD 兼容的算法，这是默认设置。
- `-s` — 使用与 System V 兼容的算法，并以 512 字节块为单位打印文件大小。

## test — 检查文件类型

GNU 命令

```
test 表达式
```

## 用途

`test` 命令根据条件*表达式*（可以为一元或二元）的求值结果返回状态 0（真）或 1（假）。可用的表达式种类繁多；更多信息请查阅在线手册或 `info` 页面。

## unsq — 解压词表

```
unsq 输入文件 输出文件
```

## 用途

`unsq` 命令对由 `sq` 压缩过的已排序词表进行解压。

## 相关命令

`sq`

## unzip — 解压文件

`unzip` *选项*

## 用途

`unzip` 命令将使用 PKZip 或 WinZip ZIP 格式（在 MS-DOS/Windows 系统上常见）压缩的文件解压。有关众多选项的更多信息，请参阅在线手册页面。

## 相关命令

`unzipsfx`

## unzipsfx — 自解压 ZIP

`unzipsfx` *选项*

## 用途

`unzipsfx` 创建一个新的归档文件，将 `unzip` 前置到现有的 ZIP 归档之前，形成自解压归档。有关众多选项的更多信息，请参阅在线手册页面。

## 相关命令

`unzip`

## updatedb — 更新文件名数据库

GNU 命令

`updatedb` *选项*

## 用途

`updatedb` 命令更新 `locate` 命令使用的文件名数据库。该数据库包含数据库上次更新时特定目录树中的文件列表。

## 选项

- `--localpaths=路径1 路径2` — 指定要加入数据库的非网络目录。
- `--netpaths=路径1 路径2` — 指定要加入数据库的网络目录。
- `--netuser=用户` — 指定用于搜索网络目录的用户。
- `--old-format` — 以旧格式而非新格式创建数据库。
- `--output=数据库文件` — 指定要构建的数据库文件。
- `--prunepaths=路径1 路径2` — 指定不加入数据库的目录。

## xfilemanager — X 文件管理器

X Window 系统命令

```
xfilemanager 选项
```

## 用途

`xfilemanager` 命令启动一个支持拖放功能的基于 X 的文件管理器。可用于执行所有常规文件管理器任务，如移动和复制文件、启动应用程序以及管理目录。

## 选项

- `-doubleClickTime` *时间*：设置鼠标点击被识别为双击前的间隔时间；默认值为 300 毫秒。
- `-iconDir` *路径*：设置文件图标目录。
- `-iconFont` *字体名*：设置图标使用的字体。
- `-multiWindow`：在单独的窗口中显示目录。
- `-noDragCopyAsk`：通过拖动复制文件前不询问确认。
- `-noDragDeleteAsk`：通过拖动删除文件前不询问确认。
- `-NoDragExecAsk`：通过拖动执行文件前不询问确认。
- `-noDragMoveAsk`：通过拖动移动文件前不询问确认。
- `-rootDir` *路径*：设置打开目录。默认为用户的主目录。
- `-saveWS`：退出前保存工作区设置。
- `-selectColor` *颜色名*：设置标记选中文件时使用的颜色。
- `-singleWindow`：在一个大窗口中显示所有内容。
- `-trashcan` *目录*：开启回收站选项；删除的文件将发送到回收站*目录*，而不是从系统中彻底删除。

## 相关命令

- `mc`
- `xfm`

## xfm — X 文件管理器

X Window 系统命令

`xfm` *选项*

## 用途

`xfilemanager` 命令启动一个支持拖放功能的基于 X 的文件管理器。可用于执行所有常规文件管理器任务，如移动和复制文件、启动应用程序以及管理目录。它实际上有两个不同的组件协同工作：应用程序管理器和文件管理器。

在新系统上运行此命令前，请使用 `xfm.install` 脚本创建新的配置文件。

## 选项

- `-appmgr` — 仅启动应用程序管理器。
- `-filemgr` — 仅启动文件管理器。

## 相关命令

- `mc`
- `xfilemanager`

## zcat — 解压文件

```
zcat 文件
```

## 用途

`zcat` 命令解压 `gzip` 压缩的文件并将其写入标准输出，通常是屏幕（工作方式与 `cat` 相同）。

## 相关命令

`gzip`

## zforce — 强制新文件名

`zforce` *文件名*

## 用途

`zforce` 命令强制使用 `gzip` 命令压缩的文件具有 `.gz` 文件扩展名。

## 相关命令

`gzip`

## znew — 新压缩文件

GNU 命令

`znew` *选项 filename.Z filename.gz*

## 用途

`znew` 命令将现有的 `.Z` 压缩文件重新压缩为 gzip（`.gz`）格式。旧的 `.Z` 文件随后将被删除。

## 选项

- `-9` — 最佳压缩方法；也是最慢的。
- `-f` — 压缩新的 *filename.gz*，即使 *filename.gz* 已存在。
- `-K` — 检查新的 *filename.gz* 文件是否比旧的 *filename.Z* 文件更小；如果不是，则不执行重新压缩操作。
- `-P` — 通过管道连接到转换程序，节省磁盘空间。
- `-t` — 在删除旧的 *filename.Z* 文件前测试新的 *filename.gz*。
- `-v` — 详细模式。

## 相关命令

`gzip`

## zoo — 操作压缩归档

`zoo` *选项 归档文件*

## 用途

`zoo` 命令使用 Lempel-Ziv 压缩算法创建文件归档。更多信息请参阅内容丰富的在线手册页面。

## 文本处理命令

这些命令设计用于直接处理文本文件。

## bpe — 二进制文件编辑器

`bpe` 文件名

## 用途

`bpe` 命令用于以十六进制或 ASCII 方式修改或编辑二进制文件。显示二进制文件时有多种命令可用；要进入编辑模式，选择 `e` 进行 ASCII 编辑或 `E` 进行十六进制编辑。

### 命令

- `D`：从当前文件位置转储一页。
- `e`：编辑文件的 ASCII 部分。
- `E`：编辑文件的十六进制部分。
- `F`：查找文件中当前位置之后的字符串。
- `H`：查找文件中当前位置之后的十六进制字节。
- `N`：显示下一个扇区。
- `P`：显示上一个扇区。
- `Q`：退出程序。
- `S`：设置当前文件指针。
- `W`：将修改后的扇区写入磁盘。
- `+`：向前滚动两行。
- `-`：向后滚动两行。
- `/`：查找文件中当前位置之后的字符串。
- `?`：显示帮助。

## 相关命令

`hd`

`od`

### cat

#### 连接文件

```
cat option(s) files
```

## 用途

`cat` 命令是 Linux 操作系统中最有用的命令，这得益于它所执行的众多（大多时候是）日常功能。从基本层面来说，它读取一个文件并将其输出到标准输出（通常是屏幕，除非标准输出已被管道连接到另一个命令或文件）。`cat` 命令还可以与 `>` 运算符结合使用，将多个文件合并为一个文件，以及与 `>>` 运算符结合使用，将文件追加到现有文件末尾。最后，`cat` 命令在与新文件的名称结合使用时，可以创建一个新的文本文件。

## 选项

- `-A` 或 `--show-all`：打印非打印字符和控制字符，但换行符和制表符除外；在每行末尾放置一个美元符号；将制表符打印为 `^I`。（与 `-vET` 相同。）
- `-e`, `-E`, 或 `--show-ends`：在每行末尾打印一个美元符号 (`$`)。
- `-n`：对行进行编号，从第一行的开头开始以 1 起算。
- `-s`：压缩空白行。
- `-t`：将每个制表符打印为 `^I`，将换页符打印为 `^L`。
- `-T` 或 `--show-tabs`：将每个制表符打印为 `^I`。
- `-u`：不做任何事情；存在此选项是为了与其他 UNIX 脚本兼容。
- `-v`：显示非打印字符和控制字符，但换行符和制表符除外。

### 示例

```
$ cat report
```

这将显示名为 `report` 的文件。

```
$ cat report report2
```

这将先显示文件 `report`，紧接着显示文件 `report2`。

Linux 命令，按组分类

### 续

```
$ cat report report2 > report3
```

这将把 `report` 和 `report2` 合并成一个名为 `report3` 的新文件。合并的顺序与命令行中指定文件的顺序一致。

```
$ cat report > report2
```

这将把文件 `report` 的内容复制到一个名为 `report2` 的新文件中。原有文件 `report` 保持不变。

```
$ cat > report
```

这将创建一个名为 `report` 的新文件，并将你随后的键盘输入发送到该文件中。你可以按 `Ctrl-D` 结束输入。

```
$ cat report >> report2
```

这将把文件 `report` 的内容追加到现有文件 `report2` 的末尾。

```
$ cat - >> report
```

这将把键盘输入追加到现有文件 `report2` 的末尾。你可以按 `Ctrl-D` 结束输入。

## 相关命令

- `cp`
- `more`
- `page`

### cmp

## 比较文件

```
cmp option(s) filename1 filename2
```

## 用途

`cmp` 命令比较两个文件的内容。如果文件之间没有差异，`cmp` 将不返回任何内容。如果文件不同，则 `cmp` 返回第一个差异处的行号和字节位置。此命令可用于二进制文件以及文本文件，这与仅适用于文本的工具（如 `diff`）不同。

## 选项

- `-c` — 将差异字节打印为字符。
- `-i` *num* — 忽略文件中前 *num* 个字节。
- `-l` — 显示文件内所有差异的字节位置和不同的字符。
- `-s` — 以静默模式工作，仅返回退出码而不显示任何差异实例。退出码为以下之一：
  - `0` — 文件相同。
  - `1` — 文件不同。
  - `2` — 其中一个文件无法读取。

### 示例

```
$ cmp report memo
report memo differ: char 12, line 1
```

## 相关命令

- `comm`
- `diff`
- `sdiff`

### colrm

#### 删除列

```
colrm start stop file
```

## 用途

`colrm` 命令从指定文件中删除列，但每行只能有一个字符，以空格分隔。

### column

#### 列格式化

```
column option(s) file
```

## 用途

`column` 命令将输入格式化为列，无论是从 *文件* 还是从标准输入。

## 选项

- `-c` *num* — 将列数设置为 *num*。
- `-s` *char* — 将 *char* 设置为列分隔符。必须与 `-t` 结合使用。
- `-t` — 将输入格式化为表格而非列。默认使用空格进行格式化，除非已通过 `-s` 设置了替代方案。
- `-x` — 在填充行之前先填充字符。

### comm

## 比较文件

```
comm option(s) file1 file2
```

## 用途

`comm` 命令比较两个已通过 `sort` 命令排序的文件的内容。输出分为三列：

| 仅在 file1 中的行 | 仅在 file2 中的行 | 在两个文件中都有的行 |
|---|---|---|

此命令类似于 `diff` 和 `uniq` 命令，但 `comm` 可用于两个已排序的文件，以找出重复或唯一的行。

## 选项

- `-1` — 禁止打印第一列。
- `-2` — 禁止打印第二列。
- `-3` — 禁止打印第三列。
- `-12` — 禁止打印第一列和第二列。
- `-13` — 禁止打印第一列和第三列。
- `-23` — 禁止打印第二列和第三列。

## 相关命令

- `cmp`
- `diff`
- `sdiff`
- `sort`

### csplit

#### 拆分文件

```
csplit option(s) file arguments
```

## 用途

`csplit` 命令将一个长文件拆分为两个或多个较小的文件。你可以通过大小或内容来告诉 `csplit` 如何拆分文件，使用特定表达式作为拆分的标记。原始文件将保持不变。

新文件将以 `xx` 开头。第一个文件是 `xx`<sup>00</sup>（记住，Linux 喜欢一切从 0 开始），下一个文件是 `xx`<sup>01</sup>，依此类推。文件数量限制为 100 个，因此数值上最高的文件名是 `xx`<sup>99</sup>。

## 选项

| 选项 | 说明 |
|--------|-------------|
| `-f txt` | 使用 *txt* 代替 `xx` 作为新文件名的开头。 |
| `-k` | 即使命令行失败也保留文件。 |
| `-n num` | 在文件名中使用 **num** 位数字，而非默认的两位。 |
| `-q` | 抑制字符计数。 |
| `-s` | 抑制字符计数。 |
| `-z` | 不创建空文件，但保持编号。 |

### 参数

| 参数 | 说明 |
|----------|-------------|
| `/expr/` | 创建一个文件，从当前行开始到包含 `expr` 的行结束。你可以添加一个后缀，使文件在 *expr* 之前或之后 `num` 行结束——分别为 `+num` 或 `-num`。 |
| `%expr%` | 创建一个以 `expr` 开头的文件。你可以添加一个后缀，使文件在 *expr* 之前或之后 `num` 行结束——分别为 `+num` 或 `-num`。 |
| **line** | 在当前行创建文件，并在 *line* 之前一行结束。 |
| `{n}` | 将参数重复 `n` 行。默认是将参数重复一次。 |

### cut

#### 剪切列

```
cut option(s) files
```

## 用途

`cut` 命令从文件或一组文件中剪切列或字段并显示它们。你可以使用该信息来查看文件的部分内容，或者将该信息发送给另一个新文件。

## 选项

| 选项 | 说明 |
|--------|-------------|
| `-c` *list* | 剪切 *list* 中指定的列。 |
| `-d` *character* | 指定用于确定列或字段的分隔符；默认为制表符。如果使用了非字母数字字符（如空格），则必须用单引号括起来。此选项必须与 `-f` 选项结合使用。 |
| `-f` *list* | 剪切 *list* 中指定的字段。 |
| `-s` | 抑制不含分隔符的行；与 `-f` 选项一起使用。 |

### 示例

```
$ cut -f1,4 payroll
```



这将从文件`payroll`中剪切第一和第四个字段，并将其显示在屏幕上。

```
$ cut -c1,4 payroll > payroll.old
```

这将从文件`payroll`中剪切第一和第四列，并将它们放入一个名为`payroll.old`的新文件中。

## 相关命令

- `grep`
- `join`
- `paste`

### diff

#### 列出文件差异

```
diff option(s) diroptions file1 file2
```

## 用途

`diff`命令比较两个文件并返回不同的行。不同文件的行号用`<`和`>`符号标记：来自`file1`的不同行用`<`标记，来自`file2`的不同行用`>`标记。三个连字符（`---`）分隔文件的内容。

`diff`命令还可用于比较不同目录中的文件。在这种情况下，请使用`diroptions`。

此命令最适合用于较小的文本文件。

## 选项

- `-a`：比较所有文件，包括二进制文件。
- `-b`：忽略行末尾的空白。
- `-B`：忽略文件内的空白行。
- `-c`：为每个差异打印三行上下文。
- `-d`：通过忽略变化较多的区域来加快处理速度。
- `-e`：返回使用`ed`文本编辑器从`file1`重新创建`file2`的命令。
- `-H`：扫描分散的小改动；会遗漏许多其他改动。
- `-i`：比较文件时忽略大小写。
- `-I expr`：忽略匹配`expr`的文件行。
- `-njay`：以`RCS diff`格式返回信息。
- `-N`：将不存在的文件视为空文件。
- `-t`：在输出中将制表符扩展为空格。
- `-T`：在行首插入制表符。
- `-u`：将文件的旧版本和新版本作为单行打印。
- `-w`：忽略制表符和空格（空白字符）。
- `-y`：以两列形式返回信息。

## diff

#### 列出文件差异

#### DIROPTIONS

- `-l`：将输出分页传递给`pr`。
- `-r`：递归运行`diff`以查看公共子目录中的文件。
- `-s`：返回相同的文件。
- `-S file`：比较目录时从`file`开始，忽略按字母顺序排在`file`之前的文件。
- `-x expr`：忽略匹配`expr`的文件；不能使用通配符。
- `-X filename`：忽略匹配`expr`的文件；可以使用通配符。

### 示例

```
$ diff letter.1212 letter.1213
1c1
< December 12, 1997
---
> December 13, 1997
...
```

## 相关命令

- `cmp`
- `diff3`
- `sdiff`

### diff3

#### 列出文件差异

```
diff3 选项 文件1 文件2 文件3
```

## 用途

`diff3`命令比较三个文件并返回它们之间的差异，与`diff`类似，但不会自动返回差异。相反，会返回以下代码之一：

- `====` 三个文件都不同。
- `====1` `file1`不同。
- `====2` `file2`不同。
- `====3` `file3`不同。

## 选项

- `-a` 将所有文件视为文本；可用于确定二进制文件之间是否存在差异。
- `-A` 创建一个`ed`脚本，以括号形式显示文件之间的所有差异。
- `-e` 创建一个`ed`脚本，将`file2`和`file3`之间的差异放入`file1`中。
- `-E` 创建一个`ed`脚本，合并以括号分隔的未合并更改。
- `-i` 在`ed`脚本末尾添加`w`（保存）和`q`（退出）命令。
- `-L name` 在输出中使用`name`代替文件名。
- `-m` 创建一个合并更改的新文件；这是直接完成的，不使用`ed`脚本。
- `-T` 在差异的每一行开头插入制表符，而不是默认的两个空格。
- `-x` 创建一个`ed`脚本，将所有文件差异放入`file1`中。
- `-X` 创建一个`ed`脚本，将所有文件差异放入`file1`中。这与`-x`相同，只是差异被括号包围。
- `-3` 创建一个`ed`脚本，将`file1`和`file3`之间的差异放入`file1`中。

## 相关命令

- `cmp`
- `diff`
- `sdiff`

### egrep

## 搜索文件

```
egrep 选项 模式 文件
```

## 用途

`egrep`命令在文件中搜索文本（称为`模式`或`表达式`），可以针对多个文件或单个文件。它与`fgrep`和`grep`命令是近亲，通常被认为是三者中最强大、最快的。但它不支持所有 ASCII 字符——只要用引号括起来，它可以搜索`+`、`|`、`(`、`)`和`?`，但不会搜索以`\`开头的模式。

## 选项

- `-A num` — 显示匹配模式后的`num`行。
- `-B num` — 显示匹配模式前的`num`行。
- `-b` — 返回匹配行的块号。
- `-c` — 返回匹配数量，不列出实际匹配内容。
- `-C` — 显示匹配模式前后各两行。
- `-e pattern` — 当`pattern`以连字符（`-`）开头时搜索`pattern`。
- `-f file` — 从`file`中使用`pattern`。
- `-h` — 列出匹配行，不列出包含它们的文件。
- `-i` — 匹配时忽略大小写。
- `-l` — 列出包含匹配的文件，不列出实际匹配内容。
- `-L` — 列出不包含匹配行的文件。
- `-n` — 列出匹配行及其行号。
- `-s` — 抑制关于无法读取或访问文件的错误消息。
- `-v` — 列出不匹配模式的行。
- `-w` — 仅列出匹配的完整单词。
- `-x` — 仅列出匹配的完整行。

### 示例

```
$ egrep "Cogswell Cogs|Spacely Sprockets" *
```

这会搜索当前目录——用`*`表示——查找字符串`Cogswell Cogs`和`Spacely Sprockets`。

## 相关命令

- `grep`
- `fgrep`

### elvis

## 文本编辑器

```
elvis 选项 文件名
```

## 用途

`elvis`命令启动一个文本编辑器。它是流行的`vi`文本编辑器的克隆版本；在 Linux 系统上，如果你在命令行使用`vi`，实际上调用的是`elvis`文本编辑器。它响应所有标准的`vi`命令。

## 选项

- `-r`：调用`elvrec`命令来恢复文件。
- `-R`：以只读状态打开文件。
- `-s`：在安全模式下工作，这样新手就不会对文件或系统造成太大损害。
- `-t tag`：打开文件时以`tag`作为第一行。
- `-m file`：在`file`中搜索编译器的错误消息。
- `-e`：以冒号命令模式启动，类似于 UNIX 的`ex`命令。
- `-v`：以可视命令模式启动，类似于 UNIX 的`vi`命令。

## 相关命令

- `elvrec`
- `emacs`
- `vi`

### emacs

## 文本编辑器

GNU 命令

X Window System 命令

```
emacs 选项 文件名
```

## 用途

`emacs`命令启动一个文本编辑器。大多数 Linux 发行版安装的`emacs`在 X Window System 下工作，但也可以安装和配置为在终端界面下工作。

`emacs`的完整文档可以使用`info`命令在线查看。

## 选项

- `+number` — 在第`number`行打开文件。
- `-font font` — 为窗口指定固定宽度`font`。（用于 X。）
- `-i` — 在将`emacs`窗口最小化时使用厨房水槽位图图标。（用于 X。）
- `-name name` — 为初始 X 窗口指定`name`。
- `-nw` — 在 X 下使用终端界面工作。
- `-q` — 不加载`init`文件。
- `-r` — 以反色显示。（用于 X。）
- `-t file` — 使用`file`作为终端，而不是标准输入/输出。
- `-title title` — 为初始 X 窗口指定`title`。
- `-u user` — 加载`user`的`init`文件。

## 相关命令

- `elvis`
- `vi`

### expand

### 扩展制表符

```
expand 选项 文件
```

## 用途

`expand`命令将制表符转换为空格。

## 选项

- `-i` 仅转换行首的制表符。

### fgrep

### 快速 Grep

```
fgrep 选项 模式 文件
```

## 用途

`fgrep`命令在文件中搜索文本（称为`模式`或`表达式`），可以针对多个文件或单个文件。它与`egrep`和`grep`命令是近亲，通常被认为是三者中最简单的。如果有任何行匹配则返回 0，没有行匹配则返回 1，遇到错误则返回 2。

## 选项

- `-A num`：显示匹配模式后的`num`行。
- `-B num`：显示匹配模式前的`num`行。
- `-b`：返回匹配行的块号。
- `-c`：返回匹配数量，不列出实际匹配内容。
- `-C`：显示匹配模式前后各两行。
- `-e pattern`：当`pattern`以连字符（`-`）开头时搜索`pattern`。
- `-f file`：从`file`中使用`pattern`。
- `-h`：列出匹配行，不列出包含它们的文件。
- `-i`：匹配时忽略大小写。
- `-l`：列出包含匹配的文件，不列出实际匹配内容。
- `-L`：列出不包含匹配行的文件。
- `-n`：列出匹配行及其行号。
- `-v`：列出不匹配模式的行。
- `-w`：仅列出匹配的完整单词。
- `-x`：仅列出匹配的完整行。
- `-num`：显示匹配模式前后各`num`行。

## 相关命令

- `egrep`
- `grep`

### fmt

### 格式化文件

```
fmt 选项 文件
```

## 用途

`fmt`命令通过将文本对齐到右边距并消除换行符来格式化文件。但是，`fmt`命令会保留原始文件中的间距、缩进和空行。

由于文本编辑器不提供此功能，通常在文本编辑器中调用（`elvis`有这样的机制），或从文本编辑器管道输出。此外，由于它通常用于格式化文件然后直接发送到打印机，所以通常作为管道中的一个步骤存在。

## 选项

- `-c`：覆盖前两行的格式化。
- `-p prefix`：格式化以`prefix`开头的行。
- `-s`：覆盖连接行。
- `-t`：标记段落。
- `-u`：应用统一间距，单词之间只有一个空格，句子之间有两个空格。
- `-w num`：将行宽设置为`num`个字符；默认值为 72。

## fold

### 格式化页面

```
fold option(s) file(s)
```

## 用途

`fold`命令将文本格式化为特定宽度，必要时会在单词中间截断以达到该宽度。默认宽度为 80 个字符。

## 选项

- `-b` 按字节而非字符计数。在此模式下，制表符和格式控制命令（如退格命令和回车符）均计入统计。
- `-s` 仅在空格处截断。
- `-w num` 将行宽设置为`num`个字符；默认值为 80。

## ghostview

## 查看 PostScript 文件

X Window 系统命令

```
ghostview option(s) filename
```

## 用途

`ghostview`命令使用`ghostscript`解释器显示 PostScript 文件。该命令有大量相关选项，但通常只需指定文件名即可调用。（有关众多选项的更多信息，请参阅在线手册页。）

## grep

## 搜索文件

```
grep option(s) pattern file(s)
```

## 用途

`grep`命令在一个或多个文件中搜索文本字符串（称为`模式`或`表达式`），并在屏幕上显示搜索结果。

`grep`命令与`fgrep`和`egrep`命令同属一类，被认为是其中功能最有限的一个。

## 选项

- `-A num` — 显示匹配模式之后的`num`行。
- `-b` — 返回匹配行的块编号。
- `-B num` — 显示匹配模式之前的`num`行。
- `-c` — 返回匹配数量，不列出实际匹配。
- `-C` — 显示匹配模式前后各两行。
- `-e pattern` — 当`pattern`以连字符（`-`）开头时使用此选项搜索。
- `-f file` — 从`file`中使用模式。
- `-h` — 列出包含匹配的行，不列出包含它们的文件。
- `-i` — 匹配时忽略大小写。
- `-l` — 列出包含匹配的文件，不列出实际匹配。
- `-L` — 列出不包含匹配行的文件。
- `-n` — 列出匹配行及其行号。
- `-s` — 抑制错误消息。
- `-v` — 列出不匹配该模式的行。
- `-w` — 仅列出匹配到的完整单词。
- `-x` — 仅列出匹配到的完整行。
- `-num` — 显示匹配模式前后各`num`行。

### 示例

```
$ grep "mail pixmap" *
```

这会搜索当前目录——如`*`所示——查找字符串`mail pixmap`。

## 相关命令

- `egrep`
- `fgrep`

## grodvi

## 将 Groff 转换为 DVI

```
grodvi option(s) filename(s)
```

## 用途

`grodvi`命令将`groff`输出转换为 TeX DVI 格式。

## 选项

| 选项 | 说明 |
|--------|-------------|
| `-d` | 不使用`tpic`特殊命令来实现绘图命令。 |
| `-Fdir` | 在目录`dir/devdvi`中搜索字体和设备描述文件。 |
| `-wn` | 将默认线条粗细设置为`n`个千分之一 em。 |

## 相关命令

- `eqn`
- `groff`
- `tfmtodit`
- `troff`

## groff

## 文档格式化

```
groff option(s) filename(s)
```

## 用途

`groff`命令是`groff`文档格式化命令的前端。它通常运行`troff`程序和一个后处理器，以准备适用于特定设备的文档。

后处理器由设备描述文件中的`postpro`命令指定。

## 设备

| 设备 | 说明 |
|--------|-------------|
| `ps` | PostScript 打印机和预览器（默认） |
| `dvi` | TeX DVI 格式 |
| `X75` | X Window 75-dpi 预览器 |
| `X100` | X Window 100-dpi 预览器 |
| `ascii` | 无格式化的行式打印机 |
| `latin1` | 带有 ISO Latin-1 字符集的行式打印机 |

## 选项

| 选项 | 说明 |
|--------|-------------|
| `-e` | 使用`eqn`预处理。 |
| `-p` | 使用`pic`预处理。 |
| `-R` | 使用`refer`预处理。 |
| `-s` | 使用`soelim`预处理。 |
| `-t` | 使用`tbl`预处理。 |
| `-V` | 打印管道而不执行。 |
| `-z` | 抑制`troff`的输出，打印错误消息。 |
| `-Z` | 覆盖来自`troff`的后处理输出。 |
| `-Parg` | 将`arg`传递给后处理器。 |
| `-l` | 将输出发送到打印机。 |
| `-Larg` | 将`arg`传递给假脱机程序。 |
| `-Tdev` | 为`dev`准备输出。默认值为`ps`。 |
| `-X` | 使用`gxditview`预览，而不是使用通常的后处理器。 |
| `-N` | 不允许`eqn`分隔符中出现换行。 |
| `-S` | 以更安全模式运行。 |

## 相关命令

- `eqn`
- `troff`
- `tbl`

## grolj4

## 用于 LaserJet 4 的 Groff

```
grolj4 option(s) filename(s)
```

## 用途

`grolj4`是用于 H-P LaserJet 4 系列的`groff`驱动程序，生成 PCL5 格式的输出。

## 选项

- `-cn`：打印每页的`n`份副本。
- `-Fdir`：在目录`dir/devlj4`中搜索字体和设备描述文件。
- `-l`：以横向 orientation 打印文档。
- `-p size`：将纸张大小设置为`size`：`letter`、`legal`、`executive`、`a4`、`com10`、`monarch`、`c5`、`b5`或`dl`。
- `-wn`：将默认线条粗细设置为`n`个千分之一 em。

## 相关命令

- `eqn`
- `groff`
- `tfmtodit`
- `troff`

## grops

## 用于 PostScript 的 Groff

```
grops option(s) filename(s)
```

## 用途



`grops`命令是`groff`的PostScript驱动程序。这是一个有些冗余的命令，因为`groff`的默认输出就是PostScript。

## 选项

- **-bn** — 与不遵循文档结构约定 3.0 的预览器和假脱机程序配合使用。*n* 指定`grops`如何处理这种情况；具体数值请参阅在线手册页。

- **-cn** — 打印每页的 *n* 份副本。

- **-Fdir** — 在目录 *dir/devname* 中搜索字体和设备描述文件。

- **-g** — 猜测页面长度。

- **-l** — 以横向 orientation 打印文档。

- **-m** — 打开手动进纸。

- **-wn** — 将默认线条粗细设置为 *n* 个千分之一 em。

## 相关命令

- `eqn`

- `groff`

- `tfmtodit`

- `troff`

## grotty

## 用于打字机的 Groff

```
grotty option(s) filename(s)
```

## 用途

`grotty`命令为打字机类设备格式化输出。

## 选项

- **-b** 抑制粗体字符的重叠打印。

- **-B** 对粗斜体字符使用重叠打印。

- **-d** 忽略所有`\D`命令。

- **-f** 使用换页符。

- **-F*dir*** 在目录 *dir/devname* 中搜索字体和设备描述文件。

- **-h** 使用水平制表符。

- **-o** 抑制重叠打印，粗体或下划线字符除外。

- **-u Belmont** 抑制斜体字符的下划线。

- **-U** 对粗斜体字符使用下划线。

## 相关命令

- `eqn`

- `groff`

- `tfmtodit`

- `troff`

## head

## 显示文件顶部

```
head option file(s)
```

## 用途

`head`命令显示文件的开头。默认显示 10 行。如果指定多个文件，每个文件开头都会放置一个标题。

## 选项

| 选项 | 说明 |

|--------|-------------|

| **-c** *num* | 打印文件的前 *num* 个字节。 |

| **-c** *numk* | 打印文件的前 *num* 千字节。 |

| **-c** *numm* | 打印文件的前 *num* 兆字节。 |

| **-n** *num* | 打印文件的前 *num* 行。 |

| **-v** | 在每个文件开头打印标题。 |

## ispell

## 拼写检查器

GNU 命令

```
ispell option(s) file(s)
```

## 用途

`ispell`命令根据系统词典检查 *file* 或 *files* 中单词的拼写。如果`ispell`遇到词典中没有的单词，它会询问您如何处理该单词，并显示正确拼写的单词，此时您输入一个命令。`ispell`命令还会创建一个人工词典文件，该文件也会被检查，允许您将常用单词放入其中。（您无法更改系统词典文件。）如果您覆盖了`ispell`的建议，该单词将被添加到个人词典中。

`ispell`命令在`emacs`文本编辑器中用作拼写检查器。

## 选项

- **-b** 创建备份文件，在原文件名后添加 *.bak*。

- **-B** 检查缺少的空格，即单词被挤在一起（连接）的情况。

- **-C** 忽略连接的字符串。

- **-d *file*** 使用 *file* 作为词典文件，而不是标准的`ispell`词典。

- **-L *num*** 显示拼写错误单词周围的 *num* 行。

- **-M** 在屏幕底部显示交互式命令。

- **-N** 抑制交互式命令的显示。

- **-n** 检查`nroff`或`troff`文件的拼写。

- **-p *file*** 使用 *file* 作为个人词典文件，而不是您标准的`ispell`个人词典。

- **-P** 抑制词根/词缀组合的建议。

- **-S** 按正确可能性级别对替换单词进行排序。

## Ispell: 拼写检查器（续）

- **-t** — 检查`tex`或`latex`文件的拼写。

- **-T *type*** — 假设文件按 *type* 格式化。

- **-w *chars*** — 将 *chars* 排除在拼写检查之外。

- **-W *num*** — 跳过长度不超过 *num* 个字符的单词。

- **-V** — 以帽子符号表示法显示控制字符（例如 ^C），并使用 - 表示高位。

### 命令

- **a** — 将该单词标记为拼写正确，但不将其添加到个人词典。

- **i** — 将该单词添加到个人词典。

- **l** — 搜索系统词典。

- **q** — 退出`ispell`，不保存拼写更改。

- **r** — 用建议替换该单词。

- **居民生活环境日益改善，健身设施、休闲绿地和现代化的垃圾处理系统提升了生活品质。

- **圈** — 扫描墙，**高声**。

- **猪** — 修复问题行为，效果很好。

- **虎** — 思考问题的全球化的选题。

- **龙** — 龙的显示器是龙圆形的。

- **马** — 马的控制面板是长方形的。

- **羊** — 羊的使用说明书是黄色的。

- **! *command*** — 在启动 shell 后运行 *command*。

## 相关命令

`wc`

## join: 合并文件

GNU 命令

```
join option(s) file1 file2
```

## 用途

`join`命令在共同的合并字段上合并两个文件（*file1* 和 *file2*）的行。

## 选项

- **-1** *field*

  - 在 *file1* 的 *field* 字段上合并。

- **-2** *field*

  - 在 *file2* 的 *field* 字段上合并。

- **-a** *file-number*

  - 列出 *file1* 或 *file2* 中每个无法配对的行。

- **-e** *string*

  - 用 *string* 替换空的输出字段。

- **-o** *field-list*

  - 使用 *field-list* 中的格式构造输出行。

- **-t** *char*

  - 将 *char* 作为输入和输出字段分隔符。

- **-v** *file*

  - 为 *file*（*file1* 或 *file2*）中每个无法配对的行打印一行，而不是正常输出。

**GNU 命令**

## less

`option(s) file(s)`

## 用途

`less`命令以交互方式显示文件的部分内容。它设计为旧 UNIX `more`命令的更高级版本——它允许您在文件中向后以及向前移动——而且它读取文件的部分内容，而非整个文件，因此它比文本编辑器更快。

您可能会发现`less`命令是您最常用的命令之一，因为它非常灵活，并且提供了`cat`命令和文本编辑器的最佳特性。

## 选项

- `-?`   显示可用命令及其功能摘要。

- `-h`   显示可用命令及其功能摘要。

- `-a`   在显示的最后一条之后创建新显示。

（默认是两行。）

- `-bbuffers`   按缓冲区大小字节显示。一个缓冲区为 1 千字节，每个文件使用 10 个缓冲区。

- `-B`   如果数据通过管道读取，则根据需要自动分配缓冲区。

- `-c`   从顶部重绘屏幕，而不是底部。

- `-C`   从顶部重绘屏幕，而不是底部，并在重绘前清除屏幕。

- `-d`   抑制在哑终端上显示的错误消息，例如提示终端缺少清屏能力。

- `-e`   当第二次到达文件末尾时退出`less`。

- **-g**

  - 仅高亮显示与最后一次搜索命令匹配的字符串，而不是所有搜索命令。

- **-G**

  - 抑制字符串的高亮显示。

- **-num**

  - 指定向后滚动的最大 *num* 行数。

- **-i**

  - 搜索时忽略大小写。如果搜索模式中包含大写字母，则考虑大小写。

- **-I**

  - 搜索时忽略大小写，即使搜索模式中包含大写字母。

- **-jnum**

  - 指定要置于屏幕顶部的"目标"行。这可以是文本搜索、标签搜索、行号、文件百分比或标记位置的对象。负数会使"目标"行相对于屏幕底部定位。

- **-kfilename**

  - 将文件作为 `lesskey` 文件打开，而不是作为普通文本文件。

- **-m**

  - 以`more`命令的详细模式打开，在屏幕底部显示百分比。

- **-M**

  - 以`more`命令的详细模式打开，在屏幕底部显示百分比、行号和总行数。

- **-n**

  - 关闭行号显示。

- **-N**

  - 在显示中每行的开头列出**行号**。

- **-ofilename**

  - 从管道将输出复制到 *filename*。如果 *filename* 存在，`less`会在覆盖前请求**权限**。

- **-Ofilename**

  - 从管道将输出复制到 *filename*。如果 *filename* 存在，`less`不会请求**权限**直接覆盖。

- **-ppattern**

  - 在 *pattern* 的**首次**出现处启动`less`。

- **-Pprompt**

  - 用以下三种方式之一定义**提示符**：

- **-Pstring**

  - 提示符为 *string*。

- **-Pmstring**

  - 中等**提示符**为 *string*。

- **-Pmstring**

  - 长**提示符**为 *string*。

- **-q**

  - 以**安静**模式工作，如果尝试滚动超出文件末尾或文件开头，则不发出声音。

- **-Q**

  - 以完全**安静**模式工作，不发出月份的时候，南北半球的气温趋势是完全相反的！

- **-r**

  - **显示**"原始"字符，而不是使用**插入符号**。可能导致显示错误。

- **-s**

  - 将连续的**空行**压缩为**单行空行**，排放是**冗长的**。通常与`nroff`文件一起使用。

- **-S**

  - 截断超过屏幕宽度的**行**，不将其**折叠**到下一行。

- **-ttag**

  - 编辑包含 *tag* 的文件，该文件位于 `./tags` 中，并由`ctags`命令生成。

- **-Ttagfile**

  - 指定要使用的标签文件，而不是 `./tags`。

- **-u**

  - 将**退格**和**回车**视为可打印字符。

- **-U**

  - 将**退格**和**回车**视为控制字符。

- **-V**

  - 显示`less`的版本号。

- **-w**

  - 将文件末尾之后的**行**表示为**空行**，而不是**波浪号**（~）字符。

- **-xnum**

  - 设置每隔 *num* 个位置为一个**制表位**；默认值为八。

- **-X**

  - 禁用向终端发送`termcap`初始化和反初始化字符串。

- **-ynum**

  - 指定向前滚动的最大**行数**。

- **-[z]num**

  - 将默认滚动窗口大小更改为 *num* 行；默认值为**一屏**。

### 命令

- **h**

  - 显示帮助信息。

- **Space, Ctrl-V, f, Ctrl-F**

  - 向前滚动默认行数（一窗口；可通过 **-z** 选项更改）。

- **z num**

  - 向前滚动默认行数；如果指定了 *num*，则它成为新的窗口大小。

- **Enter, Ctrl-N, e, Ctrl-E, j, Ctrl-J** — 向前滚动一行。

- **d, Ctrl-D *num*** — 向前滚动半屏；如果指定了 *num*，`less`向前滚动该数量的行，并将其设为默认值。

- **b, Ctrl-B, Esc-v** — 向后滚动默认行数（一窗口；可通过 **-z** 选项或 **w** 命令更改）。

- **w *num*** — 向后滚动默认行数（一窗口；可通过指定 *num* 更改）。

- **y, Ctrl-Y, Ctrl-P, k, Ctrl-K** — 向后滚动默认行数（一行）。

- **u, Ctrl-U *num*** — 向后滚动默认行数（半屏）。如果指定了 *num*，它将成为 **d** 和 **u** 命令的默认值。

- **r, Ctrl-R, Ctrl**。

- **r, Ctrl-R, Ctrl-L** — 重绘屏幕。

- **R** — 重绘屏幕并丢弃缓冲区中的输入。

- **F** — 向前滚动，即使到达文件末尾（类似于 `tail -f`）。

- **g, <, Esc-<** — 滚动到文件开头。

- **G, >, Esc->** — 滚动到文件末尾。

- **p, % *num*** — 滚动到文件中 *num* 百分比的位置。*Num* 必须在 0 到 100 之间。

- **{** — 如果 **{** 出现在屏幕顶行，则滚动到匹配的 **}**。

- **}** — 如果 **}** 出现在屏幕顶行，则向后滚动到匹配的 **{**。

- **(** — 如果 **(** 出现在屏幕顶行，则滚动到匹配的 **)**。

- **)** — 如果 **)** 出现在屏幕顶行，则向后滚动到匹配的 **(**。

- **[** — 如果 **[** 出现在屏幕顶行，则滚动到匹配的 **]**。

- **]** — 如果 **]** 出现在parcel 屏幕顶行，则向后滚动到匹配的 **[**。

## less

## 查看文件

### 续

| Esc-Ctrl-F char1 char2 | 如果 char1 出现在屏幕顶行，则滚动到匹配的 char2。 |

| Esc-Ctrl-B char1 char2 | 如果 char2 出现在屏幕顶行，则向后滚动到匹配的 char1。 |

| m letter | 使用小写字母标记当前位置。 |

| ' letter | 返回到用小写字母标记的位置。 |

| Ctrl-X Ctrl-X | 返回到用小写字母标记的位置。 |

| /pattern | 从第二显示行开始，搜索 pattern 的下一个出现位置。 |

| !pattern | 搜索不包含 pattern 的行。 |

| /*pattern | 从第二显示行开始搜索 pattern 的下一个出现位置，并将搜索扩展到命令行列表中的下一个文件。 |

| /@pattern | 从命令行中列出的第一个文件的第一行开始，搜索 pattern 的下一个出现位置。 |

| ?pattern | 在文件中向后搜索 pattern 的下一个出现位置，从屏幕顶行正上方的行开始。 |

| ?*pattern | 从屏幕顶行正上方的行开始向后搜索 pattern 的下一个出现位置，并将搜索向后扩展到命令行列表中的前一个文件。 |

| ?@pattern | 从命令行中列出的最后一个文件的最后一行开始，搜索 pattern 的下一个出现位置。 |

| Esc-/pattern | 从第二显示行开始搜索 pattern 的下一个出现位置，并将搜索扩展到命令行列表中的下一个文件。 |

| Esc-*pattern | 从屏幕顶行正上方的行开始向后搜索 pattern 的下一个出现位置，并将搜索向后扩展到命令行列表中的前一个文件。 |

| n | 重复上一次搜索。 |

| N | 重复上一次搜索，但方向相反。 |

| Esc-n | 重复上一次搜索，并将搜索扩展到命令行中指定的文件。 |

| Esc-N | 重复上一次搜索，但方向相反，并将搜索扩展到命令行中指定的文件。 |

| Esc-u | 关闭搜索结果中匹配 pattern 的高亮显示。 |

| :e filename | 打开新的 *filename*。如果未指定新文件，则重新加载当前文件。 |

| Ctrl-X, Ctrl-V, E filename | 打开新的 *filename*。如果未指定新文件，则重新加载当前文件。 |

| :n num | 打开命令行上的下一个文件。如果存在 *num*，则将打开命令行上该数量的文件。 |

| :p num | 打开命令行上的前一个文件。如果存在 *num*，则将打开命令行上该数量的前一个文件。 |

| :x num | 打开命令行上的第一个文件。如果存在 *num*，则将打开命令行上该数量的文件。 |

| =, Ctrl-G, :f | 返回正在查看的文件信息：名称、显示底行的行号、字节偏移量、文件长度、文件中的行数，以及最后显示行上方文件所占的百分比。 |

| -option | 在`less`运行时更改命令行选项。如果需要值，系统会提示输入；如果未输入新值，则显示当前值。 |

| -+option | 将命令行选项重置为默认值。 |

| --option | 将命令行选项重置为默认值的相反值。对于需要数字或字符串输入的选项，此操作无效。 |

| _ option | 返回 *option* 的当前值。 |

| +command | 每次加载新文件时运行 *command*。 |

| V | 打印版本号。 |

| q, :q, :Q, ZZ | 退出`less`。 |

| v | 启动编辑器（由 `VISUAL` 或 `EDITOR` 定义）来编辑当前文件。 |

### 续

| `! shell-command` | 运行指定的 *shell-command*。要在命令中列出当前文件，使用百分号 (%)。要在命令行中列出先前查看的命令，使用井号 (#)。要重复上一个 shell 命令，使用 `!!`。要启动不带命令的 shell，使用 `!`。 |



| `\| mark_letter shell-command` | 使用`mark_letter`将 Katz 通过管道将文件的一部分发送给指定的`shell-command`。（使用`m letter`命令标记文件。）部分的起始位置是屏幕顶部，结束位置是`mark-letter`。 |

## 编辑命令

- `Left arrow`、`Esc-h` 将光标向左移动一个空格。
- `Right arrow`、`Esc-l` 将光标向右移动一个空格。
- `Ctrl-left-arrow`、`Esc-b`、`Esc-left-arrow` 将光标向左移动一个单词。
- `Ctrl-right-arrow`、`Esc-w`、`Esc-right-arrow` 将光标向右移动一个单词。
- `Home`、`Esc-0` 将光标移动到行首。
- `End`、`Esc-$` 将光标移动到行尾。
- `Backspace` 删除光标左侧的字符，或取消命令。
- `Delete`、`Esc-x` 删除光标下的字符。
- `Ctrl-Backspace`、`Esc-Backspace` 删除光标左侧的单词。
- `Ctrl-Delete`、`Esc-X`、`Esc-Delete` 删除光标下的单词。
- `Up arrow`、`Esc-k` 检索上一个命令行。
- `Down arrow`、`Esc-j` 检索下一个命令行。
- `Tab` 补全部分文件名。如果匹配多个文件名，每次使用`Tab`时会在潜在文件名之间循环。
- `Esc-tab` 补全部分文件名。如果匹配多个文件名，每次使用`Tab`时会按相反方向在潜在文件名之间循环。
- `Ctrl-L` 补全部分文件名。如果匹配多个文件名，将显示所有潜在文件名。
- `Ctrl-U` 删除命令行或取消命令。

## 相关命令

`more`

## `look`

### 查找行

`look option(s) string file`

### 用途

`look`命令查找以`string`开头的行。如果未指定`file`，则使用`/usr/dict/words`。

### 选项

- `-a` 使用备用字典`/usr/dict/web2`。
- `-d` 仅比较字母数字字符。
- `-f` 忽略大小写。
- `-t` 设置字符串终止字符。

### 相关命令

`grep`

`sort`

## `lpq`

### 检查打印队列

`lpq option(s) user`

### 用途

`lpq`检查打印队列（由`lpd`使用），并报告指定作业的状态，可以按作业 ID 或用户指定。单独在命令行上使用时，`lpq`返回队列中所有作业的信息。

`lpq`命令报告用户名、当前队列中的排名、组成作业的文件名、作业标识符以及总字节大小。

### 选项

- `-l` — 打印作业条目中每个文件的信息；默认是在单行截断信息。
- `-Pprinter` — 指定特定打印机；默认是 PRINTER 环境变量的值或默认行式打印机。

### 相关命令

- `lpc`
- `lpd`
- `lpr`
- `lprm`

## `lpr`

### 行式打印机

`lpr option(s) file(s)`

### 用途

`lpr`将文件发送到打印后台守护进程，然后在打印机可用时将文件发送到打印机。文件选项用于指定特定类型的文件（假设要发送的是文本文件），以便打印机可以相应调整。

### 文件选项

- `-c` 假设文件由`cifplot`生成。
- `-d` 假设文件由 TeX（DVI 格式）生成。
- `-f` 使用过滤器将每行的第一个字符解释为标准 FORTRAN 回车控制字符。
- `-g` 假设文件由`plot`例程生成。
- `-l` 将控制字符过滤为可打印字符并抑制分页。
- `-n` 假设文件由`ditroff`生成。
- `-p` 使用`pr`命令格式化文件（与`print`相同）。
- `-t` 假设文件由`troff`生成。
- `-v` 假设文件包含适用于 Benson Varian 等设备的栅格图像。

### 通用选项

- `-C class` 在标题页上指定作业分类。
- `-h` 抑制打印标题页。
- `-i [cols]` 将输出缩进`num`列。如果未指定`num`，则每行缩进八个字符。
- `-m` 打印作业完成时发送邮件。
- `-P printer` 将输出发送到`printer`。
- `-r` 在假脱机完成或打印完成后删除文件（使用`-s`选项时）。
- `-s` 使用符号链接，而不是将文件复制到假脱机目录。如果这样做，在文件打印之前不要更改文件。

## `lpr`

### 行式打印机

### 续上

- `-T title` — 为`pr`指定一个`标题`名称，而非文件名。
- `-U user` — 指定要打印在分隔页上的`用户`名。
- `-w num` — 使用`num`作为`pr`的页面宽度。
- `-[num] font` — 指定要在字体位置`num`上装载的`字体`。

### 相关命令

- `lpc`
- `lpd`
- `lpq`
- `lprm`
- `pr`

---

## `lprm`

### 删除打印作业

`lprm option(s) job-ID username`

### 用途

`lprm`命令从打印假脱机中删除打印作业。使用`lpq`命令来确定作业 ID。您必须是作业的所有者或是超级用户才能删除打印作业。

### 选项

- `-Pprinter` 指定`打印机`队列而非默认队列。
- 删除`用户`拥有的作业。

### 相关命令

- `lpd`
- `lpq`
- `lpr`

---

## `more`

### 显示文件

`more option(s) file(s)`

### 用途

`more`命令逐屏显示文件的全部或部分内容。在功能上，它已基本被`less`命令所取代。

键入`q`退出`more`。按空格键继续向下滚动文件。

### 选项

- `+num`: 从第`num`行开始显示。
- `+/pattern`: 在文件显示前搜索字符串。
- `-num`: 将屏幕大小设置为`num`行。
- `-c`: 关闭滚动；取而代之的是清除屏幕，并从屏幕顶部开始绘制新文本。
- `-d`: 在屏幕底部显示以下提示：[按空格键继续，`q`退出。]
- `-f`: 计算逻辑行数，而非屏幕行数。
- `-l`: 忽略`^L`（换页符）作为特殊字符。
- `-p`: 关闭滚动；取而代之的是清除屏幕并显示新文本。
- `-s`: 将多个空行压缩为一行。
- `-u`: 抑制下划线。

### 命令

以下命令在`more`显示文件时使用。它们在屏幕底部输入，方式与 vi 文本编辑器相同。

- `RETURN`: 显示下一行文本。如果提供了参数，则该参数成为新的默认值。
- `b`或`^B`: 向后移动一屏文本。如果提供了参数，则该参数成为新的默认值。
- `d`或`^D`: 滚动 11 行文本。如果提供了参数，则该参数成为新的默认值。
- `f`: 向前跳过一屏文本。如果提供了参数，则该参数成为新的默认值。
- `h`或`?`: 显示命令摘要。
- `Ctrl-L`: 重绘屏幕。
- `n`: 重复上次搜索。
- `q`或`Q`: 退出`more`。
- `s`: 向前跳过一行文本。如果提供了参数，则该参数成为新的默认值。
- `v`: 在当前行启动`vi`。
- `z`: 显示下一屏文本。如果提供了参数，则该参数成为新的默认值。
- `'`: 返回到上次搜索开始的位置。
- `=`: 显示当前行号。
- `/pattern`: 搜索`pattern`的下一次出现。如果提供了参数，则该参数成为新的默认值。
- `!cmd`或`:!cmd`: 在子 shell 中运行`cmd`。
- `:f`: 显示当前文件和行号。
- `:n`: 打开下一个文件。
- `:p`: 打开上一个文件。
- `.`: 重复上一个命令。

### 相关命令

`less`

---

## `nroff`

### 文档格式化

`nroff option(s) filename`

### 用途

`nroff`命令调用`groff`命令来模拟在其他 UNIX 系统上 found 的 nroff 命令。有关详细信息和命令行选项，请参阅`groff`命令。

---

## `paste`

### 合并文件

GNU 命令

`paste option(s) file(s)`

### 用途

`paste`选项合并文件并将文件并排放置。`file1`的第一行将跟在`file2`的第一行之后，以制表符分隔并以换行符结尾。

### 选项

- `-d char` — 使用`char`而非制表符来分隔行。
- `-s` — 合并文件中的行，而非将两者打印在同一行上。

### 相关命令

`cut`

`join`

---

## `pico`

### Pine 编辑器

`pico option(s) filename`

### 用途

`pico`文本编辑器是一款基于`pine`邮件管理器中的撰写工具的轻量工具。如果您大量使用`pine`并希望保持工具的一致性，您可能希望使用`pico`来满足基本的编辑需求。

### 选项

- `+n` — 加载文件时，将光标置于文件第`n`行。
- `-d` — 重新绑定`Delete`键，以便删除光标所在位置的字符，而非其左侧的字符。
- `-e` — 启用文件名补全。
- `-g` — 在当前选择之前显示光标，而非显示器的左下角。
- `-k` — 从光标处删除到行尾的文本，而非整行。
- `-m` — 启用鼠标功能；仅在 X Window 下运行时可用。
- `-n n` — 新邮件到达时通知您；每`n`秒检查一次邮件。
- `-o dir` — 在`dir`目录中工作。
- `-r n` — 设置用于限制右边距的`n`列。
- `-t` — 启用工具模式，其中退出时不提示保存，且不重命名缓冲区。用于在其他工具（如`elm`或`Pnews`）中撰写文本时。
- `-v` — 查看文件而不进行编辑。
- `-w` — 禁用自动换行。
- `-x` — 禁用屏幕底部的键菜单。
- `-z` — 启用`^Z`挂起。

### 相关命令

`pine`

---

## `pr`

### 打印文件

GNU 命令

`pr file`

### 用途

`pr`命令为打印准备文件。它实际上并不打印文件——您需要将文件发送到打印机才能打印——但`pr`命令创建一个分页、分栏的适合打印的文件。

### 选项

| 选项 | 描述 |
| --- | --- |
| `+page` | 从第`page`页开始打印。 |
| `-column` | 打印`column`列。 |
| `-a` | 横向打印各列，而非纵向。 |
| `-b` | 在最后一页使各列等长。 |
| `-c` | 使用脱字符（`^G`）打印控制字符；以八进制反斜杠表示法打印其他不可打印字符。 |
| `-d` | 双倍行距打印输出。 |
| `-e width` | 将制表符展开为空格输入；如果指定了`width`，则将制表符替换为`width`。 |
| `-F` | 在页面之间使用换页符而非换行符。 |
| `-h header` | 用`header`替换页眉中的文件名。 |
| `-i[out-tab-char] [out-tab-width]` | 将空格替换为制表符。您可以指定输出制表符（`out-tab-char`）或输出制表符的宽度（`out-tab-width`），默认值为 8。 |
| `-l page-length` | 将页面长度设置为`page-length`行；默认值为 66。 |
| `-m` | 并行打印所有文件，每列一个文件。 |
| `-n[number-separator[digits]]` | 在每列前面加上行号；对于并行文件，在每一行前面加上行号。可选参数`number-separator`是每个数字后打印的字符。可选的`digits`是行号的位数；默认值为 5。 |
| `-o left-margin` | 用宽度为`left-margin`个空格的边距来偏移每一行。 |
| `-r` | 当文件无法打开时忽略警告。 |
| `-s[column-separator]` | 用单个字符`column-separator`分隔各列。 |
| `-t` | 禁止在所有页面上打印页眉和页脚。 |
| `-v` | 以八进制反斜杠表示法打印不可打印字符。 |
| `-w page-width` | 将页面宽度设置为`page-width`列；默认值为 72。 |

---

## `printf`

### 打印并格式化

GNU 命令

`printf argument`

### 用途

`printf`命令打印一个`字符串`，使用`%`指令和`\`转义符的方式与 C 语言的`printf`命令相同。

---

## `psbb`

### PostScript 边界框

`psbb file`

### 用途

`psbb`返回 PostScript 文档的边界框尺寸。如果找到边界框，则打印一行：

> `llx lly urx ury`

然后退出。如果未找到，则打印一条说明消息并退出。

## `refer`

### Groff 的参考资料

GNU 命令

`refer 选项 文件名`

### 用途

`refer`为`groff`命令预处理文献引用。它将`文件名`的内容复制到标准输出，但`.\[`和`.\]`之间的行被解释为引文，而`.R1`和`.R2`之间的行被解释为关于如何处理引文的命令。关于引文及其意义的更详细描述，以及关于不常用选项的参考，可以在手册页中找到。

## `rev`

### 反转行

`rev 文件名`

### 用途

`rev`命令反转文件的行。它将文件复制到标准输出，反转每一行中字符的顺序。

## `sdiff`

### 比较文件

```text
sdiff 选项 文件1 文件2
```

### 用途

`sdiff`命令合并两个文件并将结果输出到第三个文件。

### 选项

- `-a`：将所有文件视为文本并逐行比较，即使它们看起来不是文本。
- `-b`：忽略空白字符数量的变化。
- `-B`：忽略仅插入或删除空行的更改。
- `-d`：更改算法以查找更小的更改集合。
- `-H`：使用启发式方法加速处理具有大量分散的小更改的大文件。
- `--expand-tabs`：在最终文件中将制表符扩展为空格。
- `-i`：忽略大小写的变化。
- `-I 正则表达式`：忽略仅插入或删除匹配`正则表达式`的行的更改。
- `--ignore-all-space`：比较行时忽略空白字符。
- `--ignore-blank-lines`：忽略仅插入或删除空行的更改。
- `--ignore-case`：忽略大小写。
- `--ignore-matching-lines=正则表达式`：忽略插入或删除匹配`正则表达式`的行的更改。
- `--ignore-space-change`：忽略空白字符数量的变化。
- `-l 行数`：只打印两个共同行的左列。
- `--minimal`：更改算法以寻找更小的更改集合。
- `-o 文件` — 将合并后的输出保存到`文件`。
- `-s` — 不打印共同行。
- `--speed-large-files` — 使用启发式方法加速处理具有大量分散的小更改的大文件。
- `-t` — 将制表符扩展为空格。
- `--text` — 将所有文件视为文本。
- `-w 列数` — 设置输出宽度为`列数`。
- `-W` — 比较行时忽略水平空白字符。

### 相关命令

- `cmp`
- `comm`
- `diff`
- `diff3`

## `sed`

### 流编辑器

`sed 选项 文件名`

### 用途

`sed`命令读取文件并按照命令列表指定的内容修改输入。然后将输入写入标准输出。

### 选项

- `-a` — 在 w 函数的参数中列出的文件在任何处理开始之前被创建（或截断）。
- `-e 命令` — 将`命令`指定的编辑命令追加到命令列表中。
- `-f 命令文件` — 将`命令文件`中的命令追加到命令列表中。
- `-n` — 抑制输入每一行的回显。

## `selection`

### 选择文本

`selection 选项`

### 用途

`selection`命令从当前 Linux 控制台获取字符，并将它们粘贴到当前控制台的另一部分。该命令通常在引导时从`/etc/rc.local`文件启动，并作为后台进程运行。

### 选项

- `-a 加速倍数`

  超过`delta`像素的移动会乘以`加速倍数`（默认为 2）。

- `-b 波特率`

  设置鼠标的波特率。**警告：**应避免使用此选项，因为设置不正确的波特率可能导致鼠标冻结，而且在 Linux 和 XFree86 的其他地方有其他机制可以设置波特率。

- `-c l|m|r`

  将复制按钮设置为左键（`l`）、中键（`m`）或右键（`r`）。（默认为左键。）

- `-d delta`

  超过`delta`像素的移动会乘以`加速倍数`（默认为 25）。

- `-m 鼠标设备`



设置鼠标（默认为`/dev/mouse`）。

- **-p** l|m|r

  将粘贴按钮设置为左键（`l`）、中键（`m`）或右键（`r`）。（默认为右键。）

- **-s** 采样率

  设置鼠标的采样率（默认为 100）。

- **-t** 鼠标类型

  设置鼠标类型：Microsoft 为`ms`，Mouse Systems 为`msc`，MM Series 为`mm`，Logitech 为`logi`，Bus Mouse 为`bm`，MSC 3-bytes 为`sun`，PS/2 鼠标为`ps2`。默认为`ms`。**警告：** 应避免使用此选项，因为设置鼠标类型可能导致鼠标冻结，而且在 Linux 和 XFree86 的其他地方有其他机制可以设置鼠标类型。

- **-w** 松弛度

  设置指针重新出现在屏幕另一侧之前的松弛度。

## soelim

### Groff 解释器

`soelim` *选项 文件名*

## 用途

**soelim** 命令解释 groff 输入中的`.so`请求。它读取指定的 *文件名* 并将以下形式的行：

```
.so file
```

替换为 *文件名* 的内容。

## 选项

- **-C**

  即使`.so`后面跟着空格或换行符以外的字符也能识别。

## 相关命令

`groff`

## sort

### 排序文件

GNU 命令

```
sort 选项 文件名
```

## 用途

`sort` 命令对文本文件的行进行排序、合并或比较。结果输出到屏幕。

## 模式选项

可以使用以下选项更改模式：

- **-c**

  检查文件是否已排序；如果没有，则打印错误信息。

- **-m**

  通过将它们作为一组排序来合并文件，但文件必须已经排序。

## 通用选项

- **+起始位置 [-结束位置]**

  在每一行内，设置用作排序键的字段。

- **-b**

  忽略行首的空白字符。

- **-d**

  按电话簿顺序排序，排序时忽略除字母、数字和空白字符以外的所有字符。

- **-f**

  排序时将小写字符折转为等效的大写字符。

- **-i**

  忽略非 ASCII 字符。

- **-k 起始位置[,结束位置]**

  在每一行内设置用作排序键的字段。

- **-M**

  将月份缩写转换为大写并按顺序排序。

- **-n**

  按算术值比较。

- **-o** *文件*

  将输出写入 *文件*。

- **-r**

  反转顺序。

- **-t** *分隔符*

  指定 *分隔符* 作为字段分隔符。

- **-u**

  使用 **-m** 选项时只显示相等比较的行序列中的第一行，或使用 **-c** 选项时检查没有一对连续行相等比较。

## split

### 分割文件

GNU 命令

```
split 选项 输入文件 输出文件
```

## 用途

**split** 命令将一个文件分割成两个或多个输出文件。默认是每 1,000 行分割一次文件，但可以通过命令行选项更改。

## 选项

- **-行数** — 使用 *行数* 作为文件中的行数（默认为 1000）。

- **-b** *字节数*[**bkm**] — 按 *字节数* 个字节分隔文件。可以添加字符来指定不同的单位：

  - **b** — 512 字节块

  - **k** — 1 千字节块

  - **m** — 1 兆字节块

- **-C** *字节数*[**bkm**] — 按 *字节数* 个字节分隔文件，但确保文件以完整行结束。可以添加字符来指定不同的单位：

  - **b** — 512 字节块

  - **k** — 1 千字节块

  - **m** — 1 兆字节块

## tac

### 辩证 cat

GNU 命令

```
tac 选项 文件名
```

## 用途

**tac** 命令（**cat** 的相反）用于按反向顺序显示文件；即，先显示文件的最后一行，然后是倒数第二行，依此类推。

## 选项

- **-b** 将分隔符附加到它前面记录的开头。

- **-r** 将分隔符设置为正则表达式。

- **-s** *字符串* 将 *字符串* 设置为记录分隔符。

## 相关命令

**cat**

## tail

### 打印文件末尾

GNU 命令

```
tail option(s) filename
```

## 用途

**tail** 命令将 *filename* 的最后 10 行输出到屏幕。可以使用选项来显示更多或更少的内容。该命令与 **head** 命令相反，后者用于显示文件的前 10 行。

## 选项

- **-c** *num*：显示 *num* 个字节。

- **-f**：持续循环读取文件末尾的新增内容，适用于文件不断增长的情况。

- **-l** *num*：显示 *num* 行。

- **-q**：不打印文件名标题。

- **-v**：打印文件名标题。

## 相关命令

`head`

## tr

### 转换字符

GNU 命令

```
tr option(s) [string1 [string2]]
```

## 用途

**tr** 命令转换或删除字符，将 *string1* 替换为 *string2*。

## troff

GNU 命令

```
troff option(s) filename
```

## 用途

**troff** 命令是一个文本格式化器，属于 **groff** 格式化器家族的一部分。通常你不会单独使用它，而是由 **groff** 命令自动调用。更多信息请参见 **groff** 命令。

## 相关命令

`groff`

## Unexpand

### 取消扩展文件

GNU 命令

```
unexpand option(s) filename
```

## 用途

**unexpand** 命令将文本文件中的空格转换为制表符。

## 选项

**-a**

将所有两个或两个以上的空格或制表符字符串转换为制表符，而不仅仅是开头的空格。

**-t** *tab1*

将制表符设置为每隔 *tab1* 个空格，而非默认的 8 个。

## uniq

### 创建唯一文件

GNU 命令

```
uniq option(s) filename1 filename2
```

## 用途

**uniq** 命令从指定文件（*filename1*）中去除重复行，然后将其发送到另一个文件（*filename2*）；如果未指定其他文件，则输出到标准输出。

## 选项

- **-c**：统计重复行的数量。

- **-d**：返回重复行，不返回唯一行。

- **-f*n***：跳过每行的前 *n* 个字段；字段以空格或制表符分隔。

- **-s*n***：跳过字段的前 *n* 个字符；字段以空格或制表符分隔。

- **-u**：返回唯一行，重复行将被忽略。

- **-w *n***：比较每行的前 *n* 个字符。

- **-*n***：跳过每行的前 *n* 个字段；字段以空格或制表符分隔。

- **+*n***：跳过字段的前 *n* 个字符；字段以空格或制表符分隔。

- **--check-chars=*n***：比较每行的前 *n* 个字符。

- **--skip-chars=*n***：跳过字段的前 *n* 个字符；字段以空格或制表符分隔。

- **--skip-fields=*n***：跳过每行的前 *n* 个字段；字段以空格或制表符分隔。

## 相关命令

- `comm`

- `sort`

## vi

### 文本编辑器

```
vi option(s) filename
```

## 用途

**vi** 命令实际上是 **elvis** 文本编辑器的快捷方式。（严格来说，其他 UNIX 系统上的 **vi** 编辑器与此处的不完全相同。）更多信息请参见 **elvis**。

## vim

### 增强版 Vi

```
vim option(s) filename
```

## 用途

**vim** 文本编辑器是一个与 **vi** 兼容的文本编辑器，适用于编辑文本文件。可用选项列表请参见在线手册页。

## wc

### 字数统计

```
wc option(s) filename
```

## 用途

**wc** 命令统计文本文件中的字数；如果未指定文件名，则统计标准输入。该命令与管道中的其他文本处理命令结合使用时非常实用。

## 选项

- **-bytes** 打印字符数。

- **-c** 打印字符数。

- **--chars** 打印字符数。

- **-l** 打印文件中的行数。

- **--lines** 打印文件中的行数。

- **-w** 打印文件中的单词数；这是默认选项。

- **--words** 打印文件中的单词数；这是默认选项。

### 示例

```
$ wc textfile
3 24
```

## xedit

### X 编辑器

X Window System 命令

```
xedit filename(s)
```

## 用途

**xedit** 命令启动一个运行在 X Window System 下的简单文本编辑器。

## zcmp

### 比较压缩文件

```
zcmp option(s) file(s)
```

## 用途

**zcmp** 命令解压用 **gzip** 压缩的文件，并调用 **cmp**。与该命令相关的选项实际上是 **cmp** 的选项，这些选项连同压缩文件一起传递给 **cmp**。

## 相关命令

- `cmp`

- `gzip`

- `zegrep`

- `zfgrep`

## zdiff

### 比较压缩文件

```
zdiff option(s) file(s)
```

## 用途

**zdiff** 命令解压用 **gzip** 压缩的文件，并调用 **diff**。与该命令相关的选项实际上是 **diff** 的选项，这些选项连同压缩文件一起传递给 **diff**。

## 相关命令

- `diff`

- `gzip`

## zegrep

### 在压缩文件中搜索

```
zegrep option(s) file(s)
```

## 用途

**zegrep** 命令解压用 **gzip** 压缩的文件，并调用 **egrep**。与该命令相关的选项实际上是 **egrep** 的选项，这些选项连同压缩文件一起传递给 **egrep**。

## 相关命令

- `egrep`

- `gzip`

- `zgrep`

- `zfgrep`

## zfgrep

### 在压缩文件中搜索

```
zfgrep option(s) file(s)
```

## 用途

**zfgrep** 命令解压用 **gzip** 压缩的文件，并调用 **fgrep**。与该命令相关的选项实际上是 **fgrep** 的选项，这些选项连同压缩文件一起传递给 **fgrep**。

## 相关命令

- `fgrep`

- `gzip`

- `zgrep`

- `zegrep`

## zgrep

### 在压缩文件中搜索

## 用途

**zgrep** 命令解压用 **gzip** 压缩的文件，并调用 **grep**。与该命令相关的选项实际上是 **grep** 的选项，这些选项连同压缩文件一起传递给 **grep**。

## 相关命令

- `grep`

- `gzip`

- `zegrep`

- `zfgrep`

## zmore

### 压缩文件版 More

GNU 命令

```
zmore file(s)
```

## 用途

**zmore** 命令是经典 UNIX **more** 命令的 GNU 版本。**zmore** 一次一屏地将文件输出到屏幕。其独特之处在于 **zmore** 可以显示用 **gzip** 压缩的文件。**zmore** 没有命令行选项，只有在运行时才能调用相关命令。

### 命令

| Command | Description |
|---------|-------------|
| `space` | 打印文件的下一屏。 |
| `d` 或 `^D` | 打印接下来的 11 行，或用 `i[num]` 设置的 *num* 行。 |
| `i` | 打印文件的下一屏。 |
| `i[num]` | 将显示的行数设置为 *num*，而不是整屏。 |
| `Q` | 退出当前文件的阅读，并移动到下一个文件（如果有）。 |

## 相关命令

- `more`

- `less`

## 互联网/电子邮件命令

这些命令用于阅读和发送电子邮件、阅读和发送 Usenet 帖子、从 FTP 服务器下载文件，以及浏览万维网。

### answer

### 电话留言系统

```
answer option(s)
```

## 用途

**answer** 命令是一个秘书工具，用于将电话留言转录为 **elm** 中的电子邮件。启动后，**answer** 会检查`.elm/aliases`文件中的用户列表，然后引导用户填写一个模拟电话留言单格式的表单（包含 "Message-To:" 和 "Please Call" 等字段）。

## 选项

- **-p** 提示输入留言字段。

- **-u** 允许使用不在`.elm/aliases`文件中的名称。

## 相关命令

- `mail`

- `printmail`

### audiocompose

### 录制音频

```
audiocompose filename
```

## 用途

**audiocompose** 命令用于录制音频。如果你想录制音频片段并附加到外发的邮件中，这就是你要使用的命令。在命令行中运行此命令并指定文件名；系统会提示你录制文件，然后询问是否要在录制后收听该文件。

之后，你需要使用 **audiosend**、**mailto** 或 **metamail** 命令将该文件附加到外发的邮件中。

你的 Linux 系统必须安装音频设备，通常为`/dev/audio`。

如果你想将此格式设为系统默认，需要设置一个`RECORD_AUDIO`环境变量为`audiocompose`。

### 示例

```
$ audiosend hello
```

## 相关命令

- `audiosend`

- `mailto`

- `metamail`

- `showaudio`

## audiosend 电子邮箱地址

## 用途

`audiosend` 命令与 `audiocompose` 不同，它既可以录制音频，又可以将其通过电子邮件发送给其他用户。音频部分构成整个电子邮件；你无法在邮件中附加文本或其他文件。

该命令很简单：在命令行中使用`audiosend`，并加上一个电子邮箱地址。（如果你未指定地址，命令将提示你输入。）然后命令会提示你输入主题和抄送字段，之后你录制自己的消息。在发送消息之前，`audiosend` 会询问你是否要重新录制消息或收听它。

> 你的 Linux 系统必须安装了音频设备，通常位于`/dev/audio`。

> 如果你想将此格式设为系统默认，你需要设置一个`RECORD_AUDIO`环境变量为`audiocompose`。

### 示例

```
$ audiosend hello
```

## 相关命令

- `audiocompose`

- `showaudio`

### biff

### 邮件通知

```
biff 选项
```

## 用途

当系统使用 **sendmail** 或 **smail** 作为邮件传输代理时，**biff** 命令会通知你有新邮件到达。要查看 **biff** 的当前状态，请单独在命令行中输入它。要启用 **biff**，请使用 **y** 选项；要禁用 **biff**，请使用 **n** 选项。

## 选项

| 选项 | 描述 |
|--------|-------------|
| `n` | 关闭 **biff**。 |
| `y` | 开启 **biff**。 |

## 相关命令

- `xbiff`

### checknews

## 用途

**checknews** 命令通常用于用户配置文件（`.profile`）或 shell 脚本（`.login`）中，在用户登录时调用 **readnews** 命令以检查是否有未读的 Usenet 新闻消息。**readnews** 命令与 **-c** 选项一起使用。

## 相关命令

- `readnews`

### chfn

### 更改 Finger 信息

```
chfn 选项
```

## 用途

`chfn` 命令更改存储在 finger 配置文件中的信息。这些信息会通过网络返回给任何通过`finger`命令请求获取你信息的人。这些信息包括你的姓名、办公室号码、办公室电话和住宅电话。（默认情况下，Linux 系统不会存储这些信息；你必须自己输入。）如果你决定交互式地输入新的 finger 信息（如果你在命令行中单独运行`chfn`时的默认操作），现有的 finger 信息会以方括号形式显示。

## 选项

- **-f** *姓名* — 输入你的全名。

- **-h** *号码* — 输入你的住宅电话号码。

- **-o** *办公室* — 输入你的办公室号码。

- **-p** *号码* — 输入你的办公室电话号码。

- **-u** — 返回帮助信息。

- **-v** — 打印版本号。

### 示例

```
$ chfn
Changing finger information for Kevin.
Name [Kevin]:
Office [101]:
Office Phone [555-1212]:
Home Phone [555-1213]:
```

## 相关命令

- `finger`

- `passwd`

### elm

### 电子邮件

```
elm 选项
```

## 用途

**elm** 命令是一个交互式邮件系统，功能比 **mail** 命令更先进。你可以使用 **elm** 从命令行发送消息（通过命令行输入文本）、从命令行发送文件给用户，或者不指定任何内容而使用 **elm** 界面来阅读和发送邮件。

## 选项

- **-a** 使用箭头光标。

- **-c** 展开别名。

- **-d** *级别* 设置调试级别。

- **-f** *文件夹* 从 *文件夹* 而不是收件箱读取邮件。



- **-i** `文件` 在 outgoing 邮件消息中包含 `文件`。

- **-m** 关闭菜单，使用空间显示更多消息标题。

- **-s** `主题` 指定主题。

## 相关命令

- `fastmail`

- `mail`

- `metamail`

- `pine`

### fastmail

`fastmail` `选项` `文件名` `地址列表`

## 用途

`fastmail` 命令以交错方式向大量人群发送批量邮件，以避免邮件系统过载。基本上，它是一个面向普通用户的简化邮件系统。

## 选项

- **-b** `bcc列表` — 向 `bcc列表` 中的电子邮件地址发送密送副本（BCC）。

- **-c** `cc列表` — 向 `cc列表` 中的电子邮件地址发送抄送副本（CC）。

- **-C** `注释` — 将 `注释` 作为 Comments: 行添加到 RFC822 标头中。

- **-d** — 在调试模式下列出错误。

- **-f** `发件人` — 将 `发件人` 设置为 From: 行中的用户名。

- **-i** `msg-id` — 向邮件消息添加消息 ID。

- **-r** `replyto` — 设置 reply-to 字段。

- **-R** `参考文献` — 为消息设置描述性/参考文本。

- **-s** `主题` — 使用 `主题` 设置消息的 Subject: 行。

## 相关命令

- `elm`

- `rmail`

- `sendmail`

### finger

### Finger 信息

`finger` `选项` 用户

## 用途

`finger` 命令返回关于用户的信息，这些信息存储在他们的 `.plan` 和 `.project` 文件中。（大多数用户懒得设置这些文件，所以如果未返回信息不要惊讶。）你可以将 `用户` 指定为登录名（必须完全匹配）或名字/姓氏（返回所有匹配项；在网络环境中这可能是一个很长的列表）。

## 选项

| 选项 | 描述 |
|--------|-------------|
| `-l` | 以长格式显示信息。除 `-s` 选项提供的信息（登录名、真实姓名、终端名、写入状态、空闲时间、办公室位置和办公室电话号码）外，此选项还会添加主目录、住宅电话号码、登录 shell、邮件状态以及 `.plan`、`.project` 和 `.forward` 文件的内容。 |
| `-m` | 覆盖名字和姓氏的匹配。 |
| `-p` | 取消发送 `.plan` 和 `.project` 文件。 |
| `-s` | 以短格式显示信息：登录名、真实姓名、终端名、写入状态、空闲时间、办公室位置和办公室电话号码。 |

## formail

### 格式化邮件

`formail` `选项`

## 用途

`formail` 命令将标准输入（通常是文件）格式化为邮箱格式，然后可以由邮件程序处理。

## 选项

- `+`数量 — 跳过前 `数量` 条消息。

- `-`数量 — 仅拆分 `数量` 条消息。

- `a` 标头字段 — 向缺少标头的消息添加 `标头字段`。

- `b` — 忽略伪造的 From: 字段。

- `c` — 连接超过一行的标头字段。

- `d` — 允许宽松的格式。

- `e` — 将消息紧接在一起，而不是在它们之间插入空行。

- `f` — 忽略非邮箱格式的行。

- `i` 标头字段 — 即使已存在标头字段也添加新的 `标头字段`；旧标头字段将重命名为 `Old-标头字段`。

## frm

### 列出邮件字段

```
frm 选项 [文件夹 | 用户名]
```

## 用途

`frm` 命令列出邮箱或文件夹中选定消息的 From: 和 Subject: 字段。

## 选项

- **-n** — 使用与 `readmsg` 相同的编号方案。

- **-q** — 在安静模式下工作，只为每个指定的邮箱或文件夹生成一行摘要。

- **-Q** — 在非常安静模式下工作，仅返回错误消息。

- **-s** `状态` — 使用 `状态` 指定消息；`状态` 可以是 new、unread、old 或 read。

- **-S** — 汇总消息数量。

- **-t** — 显示完整的 From: 字段，即使这意味着要移开 Subject: 字段。

- **-v** — 在列出内容之前打印标头。

## 相关命令

- `readmsg`

- `elm`

- `mail`

- `mailx`

## ftp

### 文件传输协议

`ftp` `选项` 主机名

## 用途

`ftp` 命令连接到远程计算机——可以是你自己网络上的，也可以是更广泛的互联网上的。连接到远程计算机后，你可以来回复制文件OPT(DE)

## ftp

## 上古卷轴

续

### 命令

- **! `command` arg(s)** 在本地机器上运行 shell，并可选择性地附带 `参数`。

- **$ `macro` arg(s)** 在本地机器上运行 `宏`。

- **? `command`** 显示指定 FTP `命令` 的帮助信息。

- **account `password`** 指定登录远程系统后所需的密码。这用于非匿名性质的 FTP 服务器。

- **append `file1 file2`** 将本地 `file1` 追加到远程 `file2`。

- **ascii** 将传输模式设置为 ASCII（文本）格式，这是默认模式。如果你以 ASCII 格式传输二进制文件，你会发现二进制文件已被损坏为垃圾数据。

- **bell** 每次文件传输时播放系统声音。

- **binary** 将传输模式设置为二进制（文件）格式。这可用于传输任何文件；它是 `ascii` 设置的反面。

- **bye** 结束远程 FTP 会话和本地 `ftp` 程序。

- **case** 将所有传入文件的文件名改为小写。

- **cd `directory`** 将远程机器上的当前目录更改为 `directory`。这只有在远程 FTP 服务器上拥有 `cd` 命令权限时才有效。

- **cdup** 将远程机器上的当前目录在层级结构中向上提升一级。

- **chmod `options file`** 更改远程机器上指定 `file` 的权限。如果没有通过 `options` 指定新权限，`ftp` 命令将提示你输入新权限。

- **close** 结束远程 FTP 会话，但保留本地 `ftp` 程序继续运行。

- **cr** 将回车符剥离设置为 on（开启）。

- **delete `filename`** 从远程 FTP 服务器删除 `filename`。

- **dir** `directory filename`

返回远程机器上指定 `directory` 的内容（如果未指定 `directory`，则返回当前工作目录），可以显示到屏幕上或保存到本地机器上的指定 `filename` 中。

- **disconnect**

结束远程 FTP 会话，但保留本地 `ftp` 程序继续运行。

- **get** `file1 file2`

从远程机器下载 `file1` 并在本地保存为 `file2`。如果未指定 `file2`，文件将在本地保存为 `file1`。

- **glob**

为 `mget`、`mdelete` 和 `mput` 命令开启文件名扩展功能。

- **hash**

为每个传输的块返回哈希标记（#）。

- **help** `command`

返回指定 `command` 的帮助信息。

- **idle** `seconds`

将远程机器上的 idle（空闲）设置设为 `seconds` 秒。

- **image**

将传输模式设置为二进制（文件）格式。这可用于传输任何文件；它是 `ascii` 设置的反面。

- **lcd** `directory`

将当前本地目录更改为 `directory`。如果未指定 `directory`，当前本地目录将更改为主目录。

- **ls** `directory filename`

列出远程机器上 `directory` 的内容（如果未指定 `directory`，则为当前工作目录），可以显示到屏幕上或保存到本地机器上的指定 `filename` 中。

- **macdef** `macrofile`

定义一个宏，以空行结束；结果存储在 `macrofile` 中。

- **mdelete** `filename(s)`

删除远程机器上的 `文件`。

- **mdir** `filename(s)`

返回多个指定 `filename(s)` 的目录信息。

- **mget** `filename(s)`

从远程机器获取指定的 `filename(s)`。

- **mkdir** `directory`

在远程机器上创建新的 `directory`。

- **mls** `directory localfile`

将远程 `directory` 的内容列出到 `localfile` 中。

Linux 命令，

按组分类

- **mode** `modename` — 将模式更改为新的 `modename`。默认是流模式。

- **modtime** `filename` — 显示指定 `filename` 的最后修改时间。

- **mput** `filename(s)` — 将指定的 `filename(s)` 从本地机器上传到 FTP 服务器。

- **newer** `remotefile` — 如果 `remotefile` 比本地机器上的版本更新，则下载 `remotefile`。

- **nlist** `directory` `localfile` — 将远程 `directory` 的内容列出到 `localfile` 中。

- **open** `host` (`port`) — 打开与指定 `host` 和可选 `port` 的连接。如果未指定主机，命令将提示你输入一个。

- **prompt** — 关闭（或开启）交互式提示。

- **proxy** `command` — 在另一个连接上运行 `command`。

- **put** `file1` `file2` — 将本地文件 `file1` 复制到远程机器，保存为 `file2`。如果未指定 `file2`，则使用 `file1` 作为名称。

- **pwd** — 打印远程机器上的当前（工作）目录。

- **quit** — 结束远程 FTP 会话和本地 `ftp` 程序。

- **recv** `file1` `file2` — 从远程机器下载 `file1` 并在本地保存为 `file2`。如果未指定 `file2`，文件将在本地保存为 `file1`。

- **reget** `file1` `file2` — 从远程机器下载 `file1` 并在本地保存为 `file2`。如果传输过程中断，新的传输将从旧的传输中断处开始。

- **remotehelp** `command` — 从远程机器返回关于 `command` 的帮助信息。

- **remotestatus** `file` — 返回远程机器的状态或远程机器上 `file` 的状态。

- **rename** `file1` `file2` — 将远程系统上的 `file1` 重命名为 `file2`。

- **reset** — 重置传输队列。

- **restart** `byte` — 重新开始传输，从指定的 `byte` 计数开始。

- **rmdir** `directory` — 删除远程机器上的 `directory`。

- **runique** 开启唯一的本地文件命名；如果你正尝试从远程机器获取一个文件，而本地已存在同名文件，远程文件名将被获取并在新文件名后添加编号（.1、.2 等）。

- **send** `file1 file2` 将本地文件 `file1` 复制到远程机器，保存为 `file2`。如果未指定 `file2`，则使用 `file1` 作为名称。

- **site** `command` 返回关于远程站点的信息。

- **size** `file` 返回远程 `file` 的大小。

- **status** 返回当前会话的信息。

- **struct** `name` 将文件传输结构更改为 `name`。默认是流式传输。

- **sunique** 开启唯一的远程文件命名；如果你正尝试上传文件到远程机器，而远程已存在同名文件，文件将被上传并在新文件名后添加编号（.1、.2 等）。

- **system** 返回远程机器上运行的操作系统名称。

- **trace** 开启数据包跟踪。

- **type** `type` 将文件传输协议类型设置为 `type`；默认是 ASCII。如果没有指定 `type`，则返回当前类型。

- **umask** `mask` 设置远程机器上的模式掩码。如果没有指定 `mask`，则返回当前掩码。

- **user** `name password account` 将用户名、密码和账号发送给远程服务器。如果没有指定密码或账号，远程服务器将提示你输入这些信息。

- **verbose** 开启详细模式。

## 相关命令

`ftpd`

## ftpcount

## 用途

`ftpcount` 显示 `ftpaccess` 文件中定义的每个类别的当前用户数量。

## 相关命令

`ftpwho`

## getlist

## 获取新闻组列表

`getlist` `option` `list`

## 用途

`getlist` 从 NNTP 服务器获取列表。该列表可以是 `active`、`active.times`、`distributions` 或 `newsgroups` 之一。这些值分别请求 `active`、`active.times`、`/usr/lib/news/distributions` 或 `/usr/lib/news/newsgroups` 文件。

## 选项

**-h** `hostname`

连接到指定的 `hostname`。

## 相关命令

- `active`

- `nnrpd`

## lynx

## 文本 WWW 浏览器

`lynx` `选项(s)` URL

## 用途

`lynx` 命令启动一个基于字符的万维网浏览器。它不会在富图形环境中显示图像。因此，它是一个相当快速的 Web 浏览器，因为无需等待图形加载。

## 选项

- **-anonymous** — 指定匿名账户。

- **-ascii** — 在日本模式下禁用小繁（Kanji）翻译。

- **-auth=**ID `passwd` — 为需要此类身份验证的网站设置 ID 和`密码`。

- **-book** — 启动 `lynx` 时以书签页面作为初始文档。

- **-cache=**number — 设置缓存文档的`数量`；默认值为 10。

- **-case** — 开启区分大小写的字符串搜索。

- **-cfg=**filename — 指定新的配置文件。

- **-crawl** — 与 `-traversal` 一起使用时将每个页面输出到文件；与 `-dump` 一起使用时将每个页面输出到标准输出。

- **-display=**display — 为 X rexecd 程序设置显示变量。

- **-dump** — 将默认文档的格式化输出发送到标准输出。

- **-editor=**editor — 使用指定的`编辑器`启动编辑模式。

- **-emacskeys** — 使用类似 `emacs` 的键位移动。

- **-force_html** — 无论如何都将第一个文档解释为 HTML 页面。

- **-ftp** — 禁用 FTP 访问。

- **-get_data** — 使用 GET 方法从标准输入发送表单数据并转储结果。

- **-head** — 发送 HEAD 请求以获取 MIME 头信息。

- **-homepage=**URL — 设置与起始页面不同的主页。

- **-image_links** — 切换是否包含所有图像的链接。

- **-index=**URL — 将默认索引文件设置为指定的 URL。

- **-localhost** — 禁用指向远程主机的 URL。

- **-locexec** — 仅允许从本地文件执行本地程序。

- **-mime_header** — 显示获取文档的 MIME 头信息及其源代码。

- **-nobrowse** — 禁用目录浏览。

- **-noexec** — 禁用本地程序执行。

- **-nolist** — 在转储中禁用链接列表功能。

- **-nolog** — 禁用向文档所有者发送错误邮件。

- **-noprint** — 禁用打印功能。

- **-noredir** — 阻止自动重定向，并打印一条包含新 URL 链接的消息。

- **-nostatus** — 禁用检索状态消息。

- **-number_links** — 开始对链接进行编号。

- **-post_data** — 使用 POST 方法从标准输入发送表单数据并转储结果。

- **-realm** — 限制对起始领域内 URL 的访问。

- **-reload** — 刷新代理服务器上的缓存（仅影响第一个文档）。

- **-restrictions=option** — 禁用服务；`option` 为以下选项之一：

| 选项 | 描述 |
|--------|-------------|
| `all` | 限制所有选项 |
| `bookmark` | 禁止更改书签文件的位置。 |
| `bookmark_exec` | 禁止通过书签文件执行链接。 |
| `change_exec_perms` | 禁止更改文件的执行权限（但仍允许目录）。 |
| `default` | 禁用匿名用户的默认服务。 |
| `dired_support` | 禁止本地文件管理。 |
| `disk_save` | 禁止将二进制文件保存到磁盘。 |



### 命令与限制

以下列表列出了可用的限制命令及其说明：

- `download`：禁用下载。
- `editor`：禁止编辑。
- `exec`：禁用执行脚本。
- `exec_frozen`：禁止更改本地执行选项。
- `file_url`：禁用通过 URL 打开文件。
- `goto`：禁用`goto`命令。
- `inside_ftp`：禁止来自您域内的人员建立 FTP 连接。
- `inside_news`：禁止来自您域内的人员发布 Usenet 新闻。
- `inside_rlogin`：禁止来自您域内的人员进行 rlogin。
- `inside_telnet`：禁止来自您域内的人员进行 telnet。
- `jump`：禁用`jump`命令。
- `mail`：禁用外发邮件。
- `news_post`：禁用新闻发布。
- `options_save`：禁止在`.lynxrc`中保存选项。
- `outside_ftp`：禁止来自您域外的人员进行 FTP。
- `outside_news`：禁止来自您域外的人员发布新闻。
- `outside_rlogin`：禁止来自您域外的人员进行 rlogin。
- `outside_telnet`：禁止来自您域外的人员进行 telnet。
- `print`：禁止大多数打印选项。
- `shell`：禁止 shell 转义。
- `suspend`：禁止 Linux `Ctrl-Z` 挂起并转义到 shell。
- `telnet_port`：禁止在 telnet 连接中指定端口。

#### 其他命令行选项

- `-rlogin`：禁用对 rlogin 命令的识别。
- `-selective`：需要`.www_browsable`文件才能浏览目录。
- `-show_cursor`：将光标定位在当前所选链接的起始位置，而不是隐藏在右下角。
- `-source`：将默认文档的原始 HTML 代码发送到标准输出。
- `-telnet`：禁用对 telnet 命令的识别。
- `-term=TERM`：设置终端类型。
- `-trace`：开启 WWW 跟踪模式。
- `-traversal`：遍历从`startfile`派生的所有 HTTP 链接。
- `-underscore`：切换在转储中使用下划线格式。
- `-validate`：仅接受 HTTP URL 进行验证。
- `-vikeys`：启用类似 vi 的键位移动。

### mail

#### 发送和读取邮件

`mail` *选项(s)* *用户(s)*

**用途**

`mail`命令（在 Linux 中也称为`mailx`命令）用于发送和接收电子邮件，可以来自系统上的其他用户，也可以来自整个互联网上的用户（如果您的系统具有互联网功能）。

`Mail`只是 Linux 下众多电子邮件选项之一；几乎所有发行版都包含更易于使用的`pine`和`elm`程序，其他发行版还包含更高级的图形邮件工具。

**示例**

```
$ mail
```

这显示您的邮件。

```
$ mail reichard@mr.net
```

这开始向`reichard@mr.net`发送电子邮件的过程。

**选项**

- `-b` *list*：向*list*发送密送副本，*list*是以逗号分隔的名称列表。
- `-c` *list*：向*list*中的用户发送副本。
- `-f` *file*：启动`mail`时使用`mbox`（或指定*file*）；用作替代邮箱。
- `-i`：忽略中断信号，当您在有噪音的拨号线路上使用 Linux 机器时非常有用。
- `-I`：强制交互模式。
- `-n`：启动时不读取`/etc/mail.rc`。
- `-N`：读取邮件或编辑邮件文件夹时不显示邮件头。
- `-s` *arg*：使用*arg*作为邮件主题。
- `-v`：以详细模式工作，显示投递详情。

**命令**

- `-num`：显示前一条消息；如果指定了*num*，则打印前*num*条消息。
- `?`：显示命令摘要。
- `!command`：执行 shell *command*。
- `alias` (a) *alias*：如果未指定*alias*，则打印所有别名。如果指定了*alias*，则列出有关该别名的信息。如果指定了多个*aliases*，则创建新的别名或修改旧的别名。
- `alternates` (alt)：管理多台计算机上的账户，通知您所列地址或替代地址的状态。
- `chdir` dir (c)：将当前目录更改为*dir*。如果未指定目录，则当前目录更改为您的主目录。
- `copy` (co)：复制消息，但不删除原始消息。
- `delete` (d)：删除消息。
- `dp`, `dt`：删除当前消息并显示下一条消息。
- `edit` (e)：启动文本编辑器编辑消息；编辑后，消息重新进入`mail`。
- `exit` (ex or x)：退出`mail`，不保存对邮箱的更改。
- `file` (fi)：列出文件夹目录中的所有文件夹。
- `folder` (fo)：打开新的邮件文件或文件夹。如果您不指定新文件夹，则显示当前文件的名称。如果您确实切换到新的邮件文件或文件夹，切换前将写入旧邮件文件或文件夹的更改。新邮件文件或文件夹名称的快捷方式有：
  - `#`：上一个文件
  - `%`：系统邮箱
  - `%user`：用户的系统邮箱
  - `&`：您的 mbox 文件
  - `+folder`：您的*folder*目录中的文件
- `folders`：列出文件夹目录中的所有文件夹。

### mail（续）

#### 收发邮件（续）

- `from` (f)：打印消息的标题头。
- `headers` (h)：列出当前范围的标题头，即一组18条消息。
- `help`：显示命令摘要。
- `hold` (ho, preserve)：标记将存储在系统邮箱中而非`mbox`中的消息。
- `ignore` *header*：将标题字段添加到忽略列表中。如果未指定*header*，则显示当前要忽略的字段列表。
- `mail` (m) *user*：向*user*发送邮件；也可以指定多个用户。
- `mbox`：退出时将消息移至`mbox`。默认行为。
- `next` (n)：显示序列中的下一条消息。
- `preserve` (pre)：标记将存储在系统邮箱中而非`mbox`中的消息。
- `print` *list* (p)：打印*list*中的更多消息。
- `Print` *list* (P)：打印*list*中的文件，以及被忽略的标题字段。
- `quit` (q)：结束`mail`会话，将所有未删除、未保存的消息保存到`mbox`文件中，保留所有标记为`hold`或`preserve`或从未在系统邮箱中引用的消息，并从系统邮箱中删除所有其他消息。
- `reply` (r)：撰写对消息发送者及其他收件人的回复。
- `Reply` (R)：撰写对消息发送者的回复，但不包括其他收件人。
- `respond`：撰写对消息发送者及其他收件人的回复。
- `retain` *header*：将*header*添加到`retained_list`中命名的字段列表，查看消息时显示这些字段。
- `save` (s)：将消息保存到特定文件夹。
- `set` (se)：显示所有变量。如果提供参数，则用于设置选项。
- `saveignore`：保存消息时移除被忽略的字段。
- `saveretain`：保存消息时保留指定的字段。
- `shell` (sh)：启动 shell。
- `size`：按大小列出消息。

| 命令 | 描述 |
|---------|-------------|
| `source` *file* | 从*file*读取命令。 |
| `top` | 显示消息的前五行。 |
| `type` *list* (t) | 打印*list*中的消息。 |
| `Type` (T) | 打印*list*中的文件，以及被忽略的标题字段。 |
| `unalias` | 丢弃先前的别名。 |
| `undelete` (u) | 恢复之前标记为删除的消息。 |
| `unread` (U) | 将之前已读的消息标记为未读。 |
| `unset` | 丢弃先前用`set`命令设置的变量。 |
| `visual` (v) | 启动可视化编辑器并编辑列表中的每条消息。 |
| `write` *file* (w) | 将消息正文（不含标题）写入*file*。 |
| `xit` (x) | 退出`mail`，不保存对邮箱的更改。 |
| `z` | 显示下一窗口的消息。 |
| `z-` | 显示上一窗口的消息。 |

#### 波浪线命令

这些命令在撰写消息时使用。它们必须放在行首。

| 命令 | 描述 |
|---------|-------------|
| `~!` *command* | 运行*command*，然后返回消息。 |
| `~b` *name(s)* | 将*name(s)*添加到密送字段。 |
| `~c` *name(s)* | 将*name(s)*添加到抄送字段。 |
| `~d` | 从主目录读取`dead.letter`文件。 |
| `~e` | 启动文本编辑器进行进一步编辑。 |
| `~f` *message(s)* | 将*message(s)*插入正在发送的消息中。 |
| `~F` *message(s)* | 将*message(s)*插入正在发送的消息中，包括标题头。 |
| `~h` | 编辑标题字段。 |
| `~m` *message(s)* | 将*message(s)*插入正在发送的消息中，缩进一个制表符。 |
| `~M` *message(s)* | 将*message(s)*插入正在发送的消息中，包括标题头，缩进一个制表符。 |
| `~p` | 打印当前消息及标题字段。 |
| `~q` | 退出当前消息并将其发送到`dead.letter`文件。 |
| `~r` *filename* | 将*filename*插入消息中。 |
| `~s` *string* | 将主题设置为*string*。 |
| `~t` *name(s)* | 将*name(s)*添加到收件人列表。 |
| `~v` | 启动 VISUAL 编辑器编辑消息。 |
| `~w` *filename* | 将消息写入*filename*。 |
| `~\|` *command* | 通过*command*管道传输消息（通常是`fmt`）。 |
| `~:` *mail-command* | 执行*mail-command*。 |
| `~~` *string* | 将*string*插入消息中，前面加上`~`。 |

#### 邮件选项

您可以通过`set`和`unset`命令设置以下选项，也可以在`mail.rc`文件中设置。

- `append`：将消息附加到`mbox`中，而不是前置插入。
- `ask`, `asksub`：询问您消息的主题。
- `askcc`：询问您是否需要额外的抄送收件人。
- `askbcc`：询问您是否需要额外的密送收件人。
- `autoprint`：删除当前消息后显示下一条消息。
- `debug`：显示调试信息。
- `dot`：在消息的最后一行单独插入一个点（.）。
- `hold`：将消息保留在系统邮箱中。
- `ignore`：忽略中断信号；将它们显示为@。
- `ignoreof`：忽略文件末尾的`Ctrl-D`。
- `metoo`：将发送者作为组的一部分包含在内。
- `noheader`：读取邮件或编辑邮件文件夹时抑制消息标题的显示。
- `nosave`：不将删除的信件发送到`dead.letter`文件。
- `Replyall`：交换`reply`和`Reply`命令（参见“命令”部分）。
- `quiet`：首次调用时不打印版本信息。
- `verbose`：以详细模式工作，显示投递详情。

#### 选项字符串值

| 选项 | 描述 |
|--------|-------------|
| `EDITOR` | 与`edit`命令和`~e`转义一起使用的编辑器。 |
| `LISTER` | 在`folders`命令中使用的目录列表程序的路径名。默认是`/bin/ls`。 |
| `PAGER` | 在`more`命令或设置`crt`变量时使用的程序路径名。默认分页程序是`more`。 |
| `SHELL` | 在`!`命令和`~!`转义中使用的 shell 路径名。如果未定义此选项，则使用默认系统 shell。 |
| `VISUAL` | 在`visual`命令和`~v`转义中使用的文本编辑器路径名。 |
| `crt` | 确定消息多长时才使用`PAGER`阅读。默认是终端屏幕的高度。 |
| `escape` | 定义转义字符；默认是`~`。 |
| `folder` | 定义存储消息文件夹的目录。如果以`/`开头，则视为绝对路径；否则，视为相对于您的主目录。 |
| `MBOX` | 您的`mbox`文件；默认是您主目录中的`mbox`。 |
| `record` | 用于存储发出邮件的文件路径名；如果未定义，则不存储发出邮件。 |
| `indentprefix` | 通过`~m`转义缩进消息时使用的字符串，替代制表符。 |
| `toplines` | 定义使用`top`命令时打印的行数。 |

**相关命令**

- `fmt`
- `sendmail`

### messages

#### 统计消息数

`messages` *foldername*

**用途**

`messages`命令统计*foldername*中的消息数量，根据`From:`字段出现的次数来计数。

### metamail

#### 多媒体邮件

`metamail` *option(s)*

**用途**

`metamail`命令处理多用途互联网邮件扩展（MIME）格式定义的多媒体邮件消息。它读取`mailcap`文件以确定如何显示非文本消息。需要显示非文本消息的其他邮件程序也会调用它。

除非遇到特殊情况，您不会直接使用`metamail`；相反，您的邮件包会调用它来显示非文本消息。由于用户不会直接使用此命令，我们对此不做过多介绍；相反，我们建议您查看在线手册页面，了解如何为邮件阅读程序添加`metamail`支持或添加相关行。

### _metasend

#### 发送多媒体邮件

`metasend` *选项*

**用途**

`metasend`命令将现有数据文件作为非文本多媒体邮件消息发送。你可以在命令行中指定收件人、主题、抄送收件人、MIME 内容类型、文件名和编码；如果不指定，启动命令后系统会提示你输入这些信息。

**选项**

| 选项 | 说明 |
| --- | --- |
| `-b` | 以批处理模式工作，如果命令行中缺少信息则退出。 |
| `-c` cc | 设置抄送（CC）地址。 |
| `-D` | 设置 Content-description 值。 |
| `-e` encoding | 设置编码类型：`base64`、`quoted-printable`、`7bit`或`x-uue`。 |
| `-E` | 指定该文件已经是 MIME 实体，不需要 Content-description 头。 |
| `-f` filename | 设置数据文件。 |
| `-F` from | 设置发件人地址。 |
| `-i` <content-id> | 设置 MIME 实体的 content-id，需用尖括号括起来。 |
| `-I` <content-id> | 设置由`metasend`创建的多部分实体的 content-id。 |
| `-m` MIME-type | 设置 MIME 内容类型。 |
| `-n --` | 指定要包含额外的文件。 |
| `-o` outputfile | 将输出发送到`outputfile`。 |
| `-P` preamblefile | 指定用作 MIME 消息前言的文件。 |
| `-s` subject | 设置主题字段。 |
| `-S` splitsize | 设置通过`splitmail`分割消息之前的最大大小。 |
| `-t` to | 设置收件人（To:）地址。 |
| `-z` | 删除临时文件，即使投递失败。 |

**相关命令**

- `audiosend`
- `mailto`
- `mmencode`
- `splitmail`

### mimencode

#### MIME 编码

`mimencode` *选项*

**用途**

`mimencode`命令进行多用途互联网邮件编码（MIME）标准的编码和解码。由于 MS-DOS/Windows/Windows 95/Windows NT 不支持`uuencode`编码，因此 MIME 编码更为可取。

**选项**

- `-b`：指定`base64`编码（默认）。
- `-q`：指定`quoted-printable`编码而非`base64`。
- `-u`：对输入进行解码，而非编码。
- `-p`：将回车/换行符序列转换为换行符。
- `-o` *filename*：将输出发送到*filename*。

### mmencode

#### MIME 编码

`mmencode` *选项*

**用途**

（此处内容未提供，保留原文结构）



`mmencode`命令进行多用途互联网邮件编码（MIME）标准的编码和解码。由于 MS-DOS/Windows/Windows 95/Windows NT 不支持 `uuencode` 编码，因此 MIME 编码更为可取。

## 选项

- **-b**

  指定 base64 编码（默认）。

- **-q**

  指定 quoted-printable 编码而非 base64。

- **-u**

  对输入进行解码，而非编码。

- **-p**

  将回车/换行符序列转换为换行符。

- **-o** *filename*

  将输出发送到 *filename*。

### pine

### 电子邮件/新闻

`pine` *选项* *地址*

## 用途

`pine`命令用于阅读电子邮件和 Usenet 新闻。它支持 MIME（多用途互联网邮件扩展），允许你将 MIME 对象保存到文件中。在某些情况下，它还可以启动正确的程序来查看对象。

发出的邮件通常交给 `sendmail` 处理，但也可以通过 SMTP 直接发送。命令行选项很多；更多信息请参阅在线手册页。

## 相关命令

- `elm`

- `mail`

- `sendmail`

### Pnews

### 发布新闻文章

`Pnews` *新闻组 标题*

`Pnews -h` *headerfile*

## 用途

`Pnews`命令向特定新闻组发布新闻文章。它是一个交互式程序，这意味着它会引导你完成将项目添加到新闻组的过程。输入相关信息后，新的新闻条目将通过 `inews` 程序发送到 Usenet。

如果文件名为 `.news_sig` 且存储在你的主目录中，`Pnews` 将包含签名文件。`inews` 程序通过存储在你主目录中的 `.signature` 文件添加签名。（如果两个文件都存在，则它们都将添加到新闻条目中。）

`Pnews` 将使用默认的系统编辑器来撰写消息，该编辑器由 `EDITOR` 变量定义。此程序还与 `trn` 新闻阅读器交互；更多信息请参阅在线手册页。

### 示例

```
$ Pnews
```

> 我看你以前从未使用过这个版本的 `Pnews`。这次我会给你额外的帮助，但之后你必须记住你学到的内容。

```
$ Pnews alt.linux.slackware
```

## 选项

`-h`

与 `trn` 一起使用时，`Pnews` 将插入作为当前文章主题的先前文章。

## 相关命令

- `inews`

- `Rnmail`

- `trn`

### popclient

### POP 邮件客户端

`popclient` *选项* **主机**

## 用途

`popclient` 从运行 Internet 邮局协议（POP）的邮件服务器检索电子邮件。它支持 POP2（RFC 937 中规定）和 POP3（RFC 1725）。

此命令用于从远程服务器（由**主机**指定）获取邮件并存储在硬盘的邮件文件夹中。然后你可以使用 `mail` 或 `elm` 等邮件程序阅读。

## 选项

- **-2** — 使用邮局协议版本 2（POP2）。

- **-3** — 使用邮局协议版本 3（POP3）。

- **-a** — 使用 POP3 并从邮件服务器检索旧（先前检索过的）和新消息。

- **-c** — 将消息写入标准输出而不是磁盘。

- **-F** — 使用 POP3 并在检索新消息之前从邮件服务器删除旧（先前检索过的）消息。

- **-f** *pathname* — 设置 `.poprc` 文件的替代名称。

- **-k** — 在邮件服务器上保留旧消息。

- **-K** — 检索后删除邮件服务器上的消息。

- **-l** *lines* — 检索每条消息正文和标题的 *lines* 行。

- **-p** *string* — 登录邮件服务器时将 *string* 作为密码传递。如果未指定，登录邮件服务器时系统将提示你输入密码。

- **--protocol** *proto* — 设置与远程邮件服务器一起使用的协议。协议可以是：

  - POP2（邮局协议 2）

  - POP3（邮局协议 3）

  - APOP（带 MD5 认证的 POP3）

  - RPOP（基于可信主机认证的 POP3，如 rlogin/rsh）

- **-o** *folder* — 将消息追加到 *folder* 中的文件 welcomingly。

- **-r** *folder* — 从 *folder* 中获取消息，即邮件服务器上的替代文件夹。

- **-s** — 以静默模式工作。

- **-u** *name* — 将 *name* 作为用户传递给邮件服务器；默认情况下，这是你在本机上的登录名。

- **-v** — 以详细模式工作，显示你与服务器之间的所有消息。

## 相关命令

- `fetchmail`（`popclient` 的更新版本——大多数 Linux 发行版会包含其中之一）

### postnews

### 发布新闻

`postnews` *选项* *headerfile* *新闻组*

## 用途

`postnews`命令向 Usenet 新闻组发布新闻条目。你可以在命令行中指定新闻组（或多个新闻组）；如果不指定，`postnews`命令将提示你输入新闻组。如果指定了新闻组，需要用逗号分隔，但不要有空格。指定新闻组后，文本编辑器允许你创建帖子。

在任何时候，你都可以通过输入不符合规范的输入（例如虚构的新闻组名称）来终止发布。

## 选项

- **-h** — 指定标题位于 *headerfile* 中。

## 相关命令

`inews`

### printmail

### 打印邮件

`printmail` *选项 文件名*

## 用途

`printmail`命令格式化邮件以便打印。它从你的用户邮箱或指定的 *文件名* 中复制邮件雷，每条消息之间用一行破折号分隔。它实际上是对 `readmsg` 命令的调用，通常是管道的一部分（如 `printmail | lpr`）。

## 选项

`-p` 使用换页符而不是破折号来分隔消息。

## 相关命令

- `elm`

- `readmsg`

## procmail

### 处理邮件

`procmail` *选项(s)* *(s)*

## 用途

`procmail`命令在后台运行以处理邮件，通常通过 `.forward` 文件机制在邮件到达时立即处理。它也可以配置为通过邮件程序直接立即工作。

`procmail`命令将一些环境变量设置为默认值，从 `stdin` 读取邮件消息直至出现文件结束标记，将正文与标题头分离，然后如果没有命令行参数，则查找名为 `$HOME/.procmailrc` 的文件。该文件将消息路由到正确的文件夹。

包含 `=` 的参数被视为环境变量赋值。任何其他参数都被假定为 `rcfile` 路径。

这是一个复杂的命令，如果配置不当可能会对邮件处理造成一些损害。请查阅联机手册页以获取有关 `procmail` 的更详细信息。

## 选项

- **-d** *收件人*

  - 开启显式投递模式，投递目标为本地用户 *收件人*。不能与 `-p` 同时使用。

- **-f**

  - 重新生成以 *fromwhom* 作为发件人的 *From* 行开头（代替 `-f` 可以使用备用且已废弃的 **-r**）。如果 *fromwhom* 由单个 `-` 组成，则 `procmail` 将仅更新 *From* 行上的时间戳。

- **-m**

  - 将 `procmail` 转换为通用邮件过滤器。

- **-o**

  - 覆盖伪造的 *From* 行。

- **-p**

  - 保留旧环境。

- **-t**

  - 使 `procmail` 软失败；如果 `procmail` 无法投递到任何目的地，邮件将不会退回，而是返回邮件队列，稍后再次尝试投递。

- **-Y**

  - 使用 Berkeley 邮箱格式，忽略 *Content-Length*: 字段。

- **-a** *argument*

  - 将 `$1` 设置为 *argument*。

### 信号

| 信号 | 描述 |

|--------|-------------|

| TERMINATE | 提前终止并将邮件重新排队。 |

| HANGUP | 提前终止并退回邮件。 |

| INTERRUPT | 提前终止并退回邮件。 |

| QUIT | 提前终止并静默丢失邮件。 |

| ALARM | 强制超时。 |

| USR1 | 等同于 `VERBOSE=off`。 |

| USR2 | 等同于 `VERBOSE=on`。 |

## 相关命令

- `biff`

- `mail`

- `sendmail`

### readmsg

### 读取消息

```
readmsg 选项(s) 选择 文件夹
```

## 用途

`readmsg`命令从邮件文件夹中提取消息。通常在准备用文本编辑器编写邮件时执行此操作，此时你希望引用邮件文件夹中特定、现有的消息。

使用选择参数来指定要从邮件文件夹中获取哪条消息。通配符 (`*`) 表示提取所有消息，而数字则指代特定消息（`0` 或 `$` 指邮箱中的最后一条消息）。此外，您可以提取包含特定字符串的消息；这些字符串不需要用引号括起来。在这种情况下，将返回包含该字符串的第一条消息。（顺便说一下，这种方法区分大小写）。

您也可以在 `elm` 新闻阅读器内部使用 `readmsg`，而不是在外部编辑器中使用，但在这种情况下工作方式略有不同。用于检索消息的邮箱是当前邮箱，而不是您的收件箱；将提取当前的 `elm` 消息；编号方案也略有不同。

## 选项

- **-f** *文件夹*

  - 使用指定的文件夹而不是收件箱。这在想要搜索已发送邮件时非常有用。

- **-h**

  - 包含所有标题头信息，而不仅仅是默认的 `From:`、`Date:` 和 `Subject:` 字段。

- **-n**

  - 从检索到的消息中排除所有标题头。

- **-p**

  - 在消息标题头之间放置换页符（Ctrl-L）。

- **-a**

  - 返回所有包含命令行上字符串的消息，而不仅仅是第一条。

## 相关命令

- `elm`

- `newmail`

### richtext

### 查看富文本文档

```
richtext 选项(s) 文件名
```

## 用途

`richtext` 在 ASCII 终端上显示"富文本"文档——通常是邮件消息——使用 termcap 设置来高亮和下划线显示文本。富文本是多用途互联网邮件扩展 (MIME) 的一部分，用于多媒体互联网邮件，而非微软的富文本格式 (RTF)。

## 选项

- **-c** 显示无格式文本。

- **-f** 指定粗体和斜体文本的 termcap 转义代码。

- **-m** 在多字节日文和韩文序列中将 `<` 解释为真正的小于符号，而不是富文本命令的开始。

- **-n** 告诉命令不对原始富文本进行任何修正。

- **-o** 在适当时使用重打印实现下划线。

- **-p** 调用系统环境变量中的 `PAGER`。

- **-s** *字符集* 处理文本时使用指定的 *字符集*。*字符集* 可以是 *us-ascii*（默认值）、*iso-2022-jp* 和 *iso-2022-kr* 之一。

- **-t** 覆盖 termcap 转义代码。

## 相关命令

- `mailto`

- `metamail`

- `termcap`

### rmail

### 远程 UUCP 邮件

`rmail` *用户名*

## 用途

`rmail`命令解释通过 uucp 接收的传入邮件。随着互联网的出现，此命令的使用已减少。

## 相关命令

`sendmail`

### Rnmail

### 回复新闻/邮件

`Rnmail` *目标列表*

## 用途

`Rnmail`命令通过电子邮件回复新闻文章，而不是将消息发布到新闻组。它是一个交互式程序，这意味着它会引导您完成发送邮件的过程，提示您输入有关邮件收件人等信息。

`Rnmail` 会包含签名文件，如果该文件为 `.news_sig` 并存储在您的主目录中。`inews` 程序通过存储在您主目录中的 `.signature` 文件添加签名。（如果两个文件都存在，则它们都将添加到新闻项目中。）

`Rnmail` 将使用默认的系统编辑器来撰写消息，该编辑器由 `EDITOR` 变量定义。此程序还与 `trn` 新闻阅读器交互；您可以查阅联机手册页以获取更多详细信息。

### 示例

```
$ Rnmail
To:
Title/Subject:
Prepared file to include [none]:
Editor [usr/bin/vi]:
Check spelling, Send, Abort, Edit, or List?
```

## 选项

**-h**

与 `trn` 一起使用时，`Rnmail` 将插入当前文章主题的前一篇文章。

## 相关命令

- `inews`

- `Pnews`

- `trn`

### showaudio

### 播放音频电子邮件

`showaudio` *文件名(s)*

## 用途

`showaudio`命令播放使用 `audiocompose` 创建的音频电子邮件。它通常由 mailcap 文件调用，通常是通过 `metamail` 程序调用。通常它会在您的低保真电脑扬声器上播放音频。

## 相关命令

- `audicompose`

- `audiosend`

- `metamail`

### showexternal

### 显示 MIME 外部内容

`showexternal` *主体文件 访问类型 名称*

## 用途

`showexternal`命令获取并显示通过引用包含的邮件消息主体，使用 MIME 类型 *message/external-body*。它通常不单独使用，而是由 `metamail` 通过 mailcap 条目调用。

## 相关命令

`metamail`

### shownonascii

### 显示非 ASCII 内容

X 窗口系统命令

`shownonascii` *选项* *字符集字体名称* *文件名(s)*

## 用途

`shownonascii`命令以非 ASCII 字体显示邮件消息的全部或部分内容。默认情况下，它将打开一个 `xterm`，使用第一个参数中指定的字体，运行 `more` 命令查看命令行上指定的所有文件。

## 选项

**-e** *命令*

使用 *命令* 代替 `more` 来显示文件。

## 相关命令

`mailto`

`metamail`

### showpartial

### 显示部分邮件

```
showpartial 文件 ID 部分编号 总数
```

## 用途

`showpartial`命令用于显示 MIME 格式化消息中类型为 *message/partial* 的主体。当调用最后一部分时，它会将所有部分组合起来并调用 `metamail` 显示完整消息。它旨在由 `metamail` 通过 mailcap 条目调用。

## 相关命令

`metamail`

## showpicture

### 显示邮件图像

X Window System 命令

`showpicture` *参数 文件名*

## 用途

`showpicture`命令用于显示通过 MIME 附加到邮件消息中的图像。它会调用 X Window System 的 `xloadimage` 命令来实现此功能。该命令设计为由 `metamail` 从 mailcap 文件中调用。

### 参数

- **-viewer** — 指定一个新的图像查看器。

## 相关命令

`metamail`

### splitmail

### 拆分邮件

`splitmail` *参数 文件名*

## 用途

`splitmail`命令将一个较大的邮件消息（存储在 *filename* 中）拆分为符合 MIME 标准的部分消息，使用 *message/partial* MIME 类型。

### 参数

- `-d` 发送邮件。

- `-v` 以详细模式工作。

- `-i` 应用相似的消息 ID 字段。

- `-s` 更改消息的默认分块大小（默认值为 250,000）。

## 相关命令

`mailto`

`metamail`

### tftp

### 简单文件传输协议（Trivial FTP）

```
tftp 主机名
```

## 用途

`tftp`命令启动简单文件传输协议。

### 命令

| 命令 | 描述 |

|---------|-------------|

| `ascii` | 切换至 ASCII 模式。 |

| `binary` | 切换至二进制模式。 |

| `connect` *主机名* | 设置要连接的 *主机名*。 |

| `get` *文件名* | 从主机获取 *文件名*。 |

| `mode ascii` | 切换至 ASCII 模式。 |

| `mode binary` | 切换至二进制模式。 |

| `put` *文件名* | 将 *文件名* 上传至远程主机。 |

| `quit` | 退出 `tftp`。 |

| `status` | 显示当前状态。 |

| `timeout` *超时时间* | 设置总传输超时时间，单位为秒。 |

| `verbose` | 切换详细模式。 |

### 线程化新闻阅读器

```
trn 参数 新闻组
```

## 用途

`trn`命令启动一个新闻阅读器，允许您按线程阅读 Usenet 新闻组文章。线程化意味着文章按照回复顺序相互关联。

这是一个复杂但实用的命令。值得您花时间阅读大量的在线手册页面以获取更多信息。

### uudecode

### 解码文件

```
uudecode 文件名
```

## 用途

`uudecode`命令解码文件，将其从适合通过电子邮件发送的格式转换回来。

## 相关命令

`uuencode`

### uuencode



### 编码文件

```bash
uuencode 文件名
```

`uuencode`命令编码文件，将其转换为适合通过电子邮件发送的格式。

## 相关命令

`uudecode`

### `uustat`

#### UUCP 状态

`uustat` 参数

##### 用途

`uustat`命令返回关于 UUCP 状态的信息。有关可用参数的列表，请参阅在线手册页面。

### `uux`

`uux` 参数 命令

#### 用途

`uux`命令在远程系统上执行命令，或使用来自远程系统的文件在本地系统上执行命令。有关可用参数的列表，请参阅在线手册页面。

### `vrfy`

#### 验证电子邮件地址

`vrfy` 参数 地址 主机名

##### 用途

`vrfy`命令验证电子邮件地址的存在性和准确性。如果主机已知，该信息可以添加到命令行中，增加验证存在性和准确性的机会。如果未指定主机名，信息可能需要通过其他邮件系统，这会降低准确性。

有关可用参数的列表，请参阅在线手册页面。

### `wnewmail`

#### 邮箱标记

`wnewmail` 文件名

##### 用途

`wnewmail`守护进程每 10 秒检查一次是否有新邮件。它类似于`biff`和`xbiff`，但灵活性较低。

## 相关命令

- `biff`
- `newmail`
- `xbiff`

### `xbiff`

#### X 邮箱标记

X Window System 命令

```bash
xbiff 参数
```

##### 用途

`xbiff`命令是`biff`命令的 X Window System 版本，当收到新邮件时通知您。

#### 参数

- `-file` 文件名

  指定要监控的邮件文件名。默认值为`/usr/spool/mail/用户名`。

- `-update` 秒数

  指定`xbiff`检查邮件的频率，单位为秒。默认值为每 30 秒。

- `-volume` 百分比

  指定铃声音量（系统声音），以最大音量的百分比表示。

- `-shape`

  指定邮箱窗口是否应为异形窗口。

## 相关命令

`biff`

### `xmh`

#### X MH

X Window System 命令

`xmh` 参数

##### 用途

`xmh`命令是基于 X 的`mh`邮件处理程序的前端界面。单独使用时，它会调用`mh`软件包。

#### 参数

- `-flag` — 当新邮件到达时提醒您。
- `-initial` 文件夹 — 指定新邮件的另一个文件夹。
- `-path` 目录 — 指定邮件文件夹的另一个目录。

## 相关命令

`mail`

`metamail`

`mh`

## 编程命令

这些是大多数 Linux 实现中附带的一些基本编程命令。Linux 操作系统实际上是程序员的理想环境；这些命令将帮助您入门，但在线手册页面中还涵盖了其他编程工具。

### `ansi2knr`

#### 将 ANSI C 转换为 K&R C

`ansi2knr` 输入文件 输出文件

##### 用途

此命令将标准 ANSI C 文件转换为符合 Kernighan & Ritchie C 规范的文件。请注意，没有错误消息，因此如果转换失败，您不会知道。

##### 示例

```bash
$ ansi2knr oldfile.c newfile.c
```

### `ar`

#### 操作归档文件

GNU 命令

```bash
ar 参数 成员名 文件
```

##### 用途

`ar`命令用于创建、修改和提取归档文件。归档文件是存储在单个文件中的文件集合，这使得它们在文件系统和设备使用中更容易存储和管理。文件的所有重要元素，包括权限、所有者、时间戳和组，都保存在归档中。

此命令在编程场景中使用最多，因为它用于包含常用子程序库的创建。

成员名是归档中已存在的文件。某些选项，特别是指定归档内文件顺序的选项，需要依赖成员名。

`ar`命令需要两个参数：某种指定操作的选项，以及文件名。此命令可能令人困惑，因为选项通常必须以`p`开头。

##### 参数

- `-a`：在成员名之后添加新文件。
- `-b`：在成员名之前添加新文件。这与`i`参数相同。
- `-c`：创建新归档。
- `-d`：删除指定文件。如果运行此选项但未指定文件，则不会删除任何内容。
- `-f`：将文件名截断为特定长度。
- `-i`：在成员名之前插入新文件。这与`b`参数相同。
- `-m`：在归档内移动文件。有时归档中文件的具体顺序很重要，尤其是涉及编程库时。指定名称的文件将被移动到归档末尾。
- `-o`：提取文件时使用原始日期。如果您想保留原始时间戳，这一点至关重要，因为`ar`会将提取时的时间戳应用到文件上。
- `-p`：打印归档内的文件名。
- `-q`：快速追加，意味着将指定文件添加到归档末尾。此选项不受其他任何选项（如`a`、`b`和`i`）的影响，因为所有新文件都会自动放置在归档末尾。但是，归档的符号表索引不会更新，这意味着必须使用`s`参数或`ars`或`ranlib`命令来更新它。
- `-r`：替换归档内的文件。归档中同名现有文件将自动删除。
- `-s`：更新符号表索引。这相当于`ranlib`命令。
- `-t`：列出归档内文件名的表格，或者将文件列表与归档内的文件名进行匹配。
- `-u`：使用`r`参数替换文件时，仅插入较新的文件。
- `-v`：告诉`ar`在详细模式下工作，列出归档中被操作的文件。
- `-x`：从归档中提取文件。

## 相关命令

`ars`

`ranlib`

### `as`

#### 汇编器

`as option(s) files`

##### 用途

**GNU 汇编器**命令将汇编文件转换为目标文件。基本上，它用于在通过`ld`链接之前，汇编由`gcc` C 编译器生成的文件。

你可以从现有的 C 文件或标准输入（键盘）进行汇编。如果通过键盘输入文件，需要使用`Ctrl-D`告知`as`输入已结束。

#### 选项

- `-a`

  - 开启汇编列表，在汇编文件时输出。不过，还可以与其他多个选项组合使用：
    - `-ad`：省略调试指令。
    - `-ah`：如果源文件可以找到且代码使用`-g`编译，则包含高级源代码。
    - `-al`：包含汇编列表。
    - `-an`：省略表格处理。
    - `-as`：包含符号列表。
    - `-afile`：指定列表文件名。

- `--defsym`

  - 在文件汇编前，将符号`SUM`定义为等于`VALUE`（整数`SYM=VALUE`常量）。

- `-f`

  - 以快速模式汇编，在源为编译器输出时跳过预处理。

- `-Ipath`

  - 将`path`添加到`.include`指令的列表中。

- `-K`

  - 当差异表被修改为长位移时发出警告。

- `-L`

  - 保留符号表中的局部符号，以`L`开头。

- `-M`

  - 以 MRI 兼容模式汇编。

- `-o objfile`

  - 指定目标文件输出为`objfile`。

- `-R`

  - 将数据段折叠到文本段中。

- `-v`

  - 返回`as`的版本。

- `-W`

  - 抑制警告。

- `--`

  - 要汇编的源文件（`files`）或从标准输入汇编（`--`）。

## 相关命令

- `gcc`
- `ld`

### `bison`

#### 解析器生成器

**GNU 命令**

`bison option(s)`

##### 用途

`bison`命令获取文件`filename.y`中的语法规范，并为其生成 LR 解析器。解析器由一组 LALR 解析表和一个用 C 语言编写的驱动例程组成。解析表和驱动例程通常写入文件`y.tab.c`。

它是`yacc`命令的 GNU 替代版本。`bison`和`yacc`之间存在一些差异：例如，生成的文件没有固定名称，而是使用输入文件的前缀。你可以查看在线手册页面获取更多详情。

#### 选项

- `-b` prefix

  - 将输出文件名的前缀更改为`prefix`。默认为`y`。

- `-d`

  - 编写一个头文件，包含为语法中定义的令牌类型名称和语义值类型`YYSTYPE`的宏定义，以及外部变量声明。

- `-l`

  - 不将代码插入现有文件。

- `-o` outfile

  - 使用`outfile`作为解析器文件。

- `-p` prefix

  - 重命名解析器中使用的外部符号，使它们以`prefix`开头，而不是`yy`。

- `-t`

  - 更改预处理指令以包含调试信息。

- `-v`

  - 将生成的解析器的人类可读描述写入`y.output`。

## 相关命令

`yacc`

### `cc`

#### C 编译器

`cc option filename`

##### 用途

`cc`命令是标准的 C 编译器命令。Linux 以`gcc`，即 GNU C 编译器，作为其首选的 C 语言工具。查看`gcc`的条目以获取更多信息。

### `cpp`

#### C 编译器预处理器

**GNU 命令**

`cpp option(s) inputfile outputfile`

##### 用途

C 预处理器是 C 编译器使用的宏处理器，用于在实际编译前转换程序。如需更详细的说明，请参阅 cpp.info 的`info`条目和在线手册页面。

## 相关命令

- `gcc`
- `imake`

### `ctags`

`ctags option(s)`

##### 用途

`ctags`命令创建`vi`可用的标签表文件。支持的语法包括 C、C++、Fortran、Pascal、LaTeX、Scheme、Emacs Lisp/Common Lisp、Erlang、Prolog 以及大多数类汇编语法。

更多信息请参阅在线手册页面。

### `etags`

#### Emacs 标签

`etags option(s)`

##### 用途

`etags`命令创建`emacs`可用的标签表文件。支持的语法包括 C、C++、Fortran、Pascal、LaTeX、Scheme、Emacs Lisp/Common Lisp、Erlang、Prolog 以及大多数类汇编语法。

更多信息请参阅在线手册页面。

### `flex`

#### 快速词法分析器生成器

`flex option(s) filename`

##### 用途

`flex`命令生成识别文本中词法模式的扫描器程序。此命令读取给定的输入文件（如果未提供文件名，则读取标准输入），获取要生成的扫描器的描述。描述的形式为正则表达式和 C 代码的配对，称为`rules`（规则）。输出是一个 C 源文件。此文件与`-lfl`库编译并链接以生成可执行文件。

更多信息请参阅在线手册页面。

### `g77`

#### Fortran 编译器

**GNU 命令**

`g77 option(s) filename`

##### 用途

`g77`命令编译 Fortran 程序。有关 Fortran 和此命令的信息，请参阅 g77 的`info`列表。

### `gawk`

`gawk option(s) filename`

##### 用途

`gawk`命令是 AWK 编程语言的 GNU 版本——不一定是复杂的语言，但确实是一门涉及广泛的编程语言。你可以查看在线手册页面，或者甚至找一本 AWK 编程书籍获取更多信息。

### `gcc/g++`

#### C/C++ 编译器

**GNU 命令**

`gcc option filename`

`g++ option filename`

##### 用途

`gcc`和`g++`命令是 Linux 中使用的 C 语言和 C++ 语言编译器。[还支持 Objective-C。] 两者都将输入文件通过一个或多个以下四个阶段进行处理：预处理、编译、汇编和链接。`gcc`命令假设预处理后的（`.i`）文件是 C 文件，并采用 C 风格链接，而`g++`假设预处理后的（`.i`）文件是 C++ 文件，并采用 C++ 风格链接。命令适用于以下文件扩展名：

- `.c` - C 源文件；预处理、编译、汇编
- `.C` - C++ 源文件；预处理、编译、汇编
- `.cc` - C++ 源文件；预处理、编译、汇编
- `.cxx` - C++ 源文件；预处理、编译、汇编
- `.m` - Objective-C 源文件；预处理、编译、汇编
- `.i` - 预处理后的 C；编译、汇编
- `.ii` - 预处理后的 C++；编译、汇编
- `.s` - 汇编器源文件；汇编
- `.S` - 汇编器源文件；预处理、汇编
- `.h` - 预处理器文件；通常不在命令行中指定

具有其他后缀的文件将传递给链接器。常见情况包括：

- `.o` - 目标文件
- `.a` - 归档文件

这里不介绍 C 语言编程和使用入门；整个图书馆的藏书对 C 编程的介绍比我们在这个有限的空间里能做得要好得多。此外，此命令有数百个可用选项；你可以查看 info 页面获取更多信息。

### `gprof`

#### 显示性能分析数据

`gprof option(s)`

##### 用途

`gprof`命令生成 C、Pascal 或 Fortran77 程序的执行性能分析。被调用例程的影响被纳入每个调用者的性能分析中。性能分析数据取自调用图性能分析文件（默认为`gmon.out`），该文件由使用`cc`、`pc`和`f77`的`-pg`选项编译的程序创建。`-pg`选项还会链接为性能分析编译的库例程版本。

`gprof`读取给定的目标文件（默认为`a.out`），并建立其符号表与`gmon.out`中调用图性能分析之间的关系。如果指定了多个性能分析文件，`gprof`输出将显示给定性能分析文件中性能分析信息的总和。

#### 选项

- `-a`

  - 禁止打印静态声明的函数。

- `-b`

  - 禁止打印性能分析中每个字段的描述。

- `-c`

  - 使用检查目标文件文本空间的启发式方法确定程序的静态调用图。

- `-e` name

  - 禁止打印例程`name`及其所有后代的图性能分析条目（除非它们有其他未被抑制的祖先）。

- `-E` name

  - 禁止打印例程`name`（及其后代）的图性能分析条目，与`-e`类似，并且还将`name`（及其后代）中花费的时间从总时间和百分比时间计算中排除。

- `-f` name

  - 仅打印指定例程`name`及其后代的图性能分析条目。

### `gprof`

#### 显示性能分析数据

- `-F` name

  仅打印例程`name`及其后继例程的图表分析项，类似于`-f`，同时仅在总时间和百分比计算中使用所打印例程的时间。

- `-k` fromname toname

  删除从例程`fromname`到例程`toname`的弧。

- `-s`

  生成一个性能分析文件`gmon.sum`，该文件表示所有指定性能分析文件中分析信息的总和。

- `-z`

  显示使用量为零的例程（如调用次数和累计时间所示）。

## 相关命令

- `cc`
- `monitor`
- `profile`
- `prof`

### `imake`

#### Make 前端

X 窗口系统命令

`imake option(s)`

##### 用途

`imake`命令根据模板、一组`cpp`宏函数以及每个目录的输入文件（称为 Imakefile）生成`makefile`。这样可以将机器依赖性（如编译器选项、替代命令名称和特殊的`make`规则）与要构建的各种项的描述分开。

#### 选项

- `-Ddefine`

  设置目录特定的变量；发送给`cpp`。

- `-Idirectory`

  设置包含`imake`模板和配置文件的目录。

- `-Ttemplate`

  指定主模板文件。

- `-f filename`

  设置每个目录的输入文件名。

- `-C filename`

  指定在当前目录中构建的`.c`文件的名称。

- `-s filename`

  指定要生成的`make`描述文件的名称，但不调用`make`。

- `-e`

  执行最终的 Makefile。

- `-v`

  打印用于生成 Makefile 的`cpp`命令行。

## 相关命令

- `make`
- `xmkmf`

### `make`

#### Make 程序

GNU 命令

`make option(s) target`

##### 用途

`make`命令管理构成程序的一组文件。当程序发生更改时，例如源代码更改，`make`命令可以创建新程序，保留程序的现有部分，同时纳入更改。`make`命令确定程序的哪些部分需要重新编译，并发出重新编译它们的命令。

`make`命令最常与 C 编程语言（以及 X 窗口系统软件）一起使用，但它可以与任何编译器通过 shell 命令运行的编程语言一起使用。

`make`命令使用`Makefile`来确定需要进行哪些更改，并发出更新文件所需的命令。通常，可执行文件从目标文件更新，而目标文件源自源文件。

通常，你只需要在命令行上运行`make`来自动执行所有重新编译。分发版中包含的 README 文件通常会提供更详细的说明。

#### 选项

- `-b`

  忽略；包含此项是为了与非 GNU 版本的`make`兼容。

- `-m`

  忽略；包含此项是为了与非 GNU 版本的`make`兼容。

- `-C` dir

  在执行任何操作之前切换到`dir`目录。

- `-d`

  除正常信息外，返回调试信息。



- `-e`

  使用环境变量而非 `makefile` 中指定的变量。

- `-f` *file*

  使用 *file* 作为 `makefile`。

- `-i`

  忽略编译问题引起的错误。

- `-I` *dir*

  指定 *dir* 作为搜索包含 `makefile` 的位置。

- `-j` *jobs*

  设置同时运行的 *jobs*（命令）数量。

- `-k`

  出错后尽可能继续执行。

- `-l` *load*

  指定如果还有其他作业正在运行，且平均负载至少为 *load*（浮点数），则不应启动新的作业（命令）。

- `-n`

  打印命令如同它们被执行了一样，但不实际执行。

- `-o` *file*

  跳过重新制作 *file*，即使 `makefile` 指示应该重新制作它。

- `-p`

  打印从 `makefile` 生成的数据库，然后运行命令。

- `-q`

  在问题模式下工作，返回退出状态，如果指定的目标已经是最新的则为零，否则非零。

- `-r`

  消除内置的隐式规则。

- `-s`

  打印执行时的命令。

- `-S`

  取消 `-k` 选项的效果；在递归 `make` 中有用。

- `-t`

  触摸文件而不是运行它们的命令。

- `-w`

  在其他处理之前和之后返回工作目录。

- `-W` *file*

  假装目标 *file* 已被修改。将此选项与 `-n` 选项一起使用，以查看如果实际修改文件会发生什么。

## 相关命令

- `gcc`

- `makedepend`

### makedepend

Make 依赖关系

X 窗口系统命令

`makedepend` *option(s) sourcefile(s)*

## 用途

`makedepend` 命令读取 *sourcefile* 并像 C 预处理器一样解析它，处理所有 `#include`、`#define`、`#undef`、`#ifdef`、`#ifndef`、`#endif`、`#if` 和 `#else` 指令，以便正确判断在编译中将使用哪些 `#include` 指令。

*sourcefile* 直接或间接包含的每个文件都是一个依赖项。然后将这些依赖项写入 `makefile`，以便 `make` 在依赖项更改时知道要重新编译什么。

默认情况下，`makedepend` 将输出发送到 `makefile`（如果存在）或 `Makefile`。

## 选项

- `-a`

  将依赖项追加到文件末尾，而不是替换它们。

- `-Dname=def`

  在 `makedepend` 符号表中定义 *name*。

- `-fmakefile`

  定义 `makefile` 的备用文件名。

- `-Iincludedir`

  通过预置 *includedir* 目录来指定包含目录，这些目录列在 `#include` 指令中。

- `-m`

  当文件将被包含多次时发出警告。

- `-oobjsuffix`

  指定目标文件的后缀，而不是默认的 `.o`。

- `-pobjprefix`

  指定目标文件的前缀（通常是新目录）。

- `-sstring`

  为 `makefile` 设置新的起始字符串分隔符。

- `-wwidth`

  设置行宽。默认为 78 个字符。

- `-v`

  在详细模式下运行，将包含的文件名发送到屏幕。

- `-Yincludedir`

  用 *includedir* 替换标准包含目录。

## 相关命令

- `cc`

- `make`

### makestrs

生成字符串表

X 窗口系统命令

`makestrs` *option(s)*

## 用途

`makestrs` 命令生成字符串表 C 源文件和头文件。C 源文件被写入 `stdout`。

## 选项

- `-arrayperabi`

  为每个字符串生成单独的数组。

- `-defaultab`

  即使 `makestrs` 使用 `-DARRAYPERSTR` 编译，也生成正常的字符串表。

- `-earlyR6abi`

  保持 X11R6 公共补丁 11（及更早版本）与 X11R6 公共补丁 12（及更高版本）之间的二进制兼容性。

- `-functionabi`

  生成字符串表的功能性 abi。

- `-intelabi`

  与符合 System V 应用程序二进制接口（SVR4）的 Intel 平台一起工作。

### msgfmt

创建消息选项

```
msgfmt option filename.po
```

## 用途

`msgfmt` 命令从可移植消息文件 *filename.po* 创建消息对象 *filename.mo*，该文件保持不变。

## 选项

- `-v`

  在详细模式下工作。

## 相关命令

- `gettext`

- `xgettext`

### objcopy

目标文件复制

GNU 命令

```
objcopy option(s) infile outfile
```

## 用途

`objcopy` 命令使用 GNU BFD 库读取和写入目标文件，将一个目标文件的内容复制到另一个目标文件。它以不同于源目标文件的格式写入目标目标文件。

此命令有大量命令行选项可用；有关更多信息，请查看 `objcopy` 的 `info` 页面。

### Perl 语言

## 用途

Perl 是实用报表提取语言（Practical Extraction and Report Language）。它是一种解释型语言，经过优化，用于扫描任意文本文件、从这些文本文件中提取信息，以及基于这些信息打印报告。随着 Internet 上 UNIX 和 Linux 服务器的兴起，Perl 变得广受欢迎。

以上是简短定义。它也是一种极其复杂且有用的语言，复杂到无法在此概括。你需要查阅关于 `perl` 的冗长在线手册页，它们涵盖了 `perl` 的方方面面，既适合初学者也适合高级用户。此外，你可能还想投资一本好的 `perl` 教材。

## 显示 C 函数头

```
ref option(s) filename tag
```

## 用途

`ref` 命令显示函数的头信息，它在标签文件中查找，然后扫描源文件以定位该函数。返回的信息包括介绍性注释（如果有的话）、函数的声明以及所有参数的声明。

## 选项

- `-c` *class*：指定标签的*类*。

- `-f` *file*：在*file*中查找标签（作为静态函数）。

- `-t`：输出标签信息，而非函数头信息。

## 相关命令

`ctags`

## rpcgen

## RPC 编译器

`rpcgen` *infile* *option(s)*

## 用途

`rpcgen` 命令生成用于实现 RPC 协议的 C 代码。`rpcgen` 的输入是一种类似于 C 的语言，称为 RPC 语言（远程过程调用语言）。更详细的描述请参阅在线手册页。

## 选项

- `-5`

  生成 SVR4 风格的 RPC 代码。

- `-a`

  生成所有文件，包括客户端和服务器端的示例代码。

- `-b`

  生成 SunOS4.1 风格的 RPC 代码（默认值）。

- `-c`

  编译为 XDR 例程。

- `-C`

  生成 ANSI C 代码。此选项还会生成可以用 C++ 编译器编译的代码。（默认。）

- `-D` *name*

  定义符号 *name*。

- `-h`

  编译为 C 数据定义（头文件）。

- `-I`

  生成可以从 `inetd` 启动的服务，而不是默认的静态服务（该服务处理通过 `-s` 选择的传输方式）。

- `-k`

  生成 K&R C 代码。

- `-K` *secs*

  设置服务请求后默认的 *secs* 秒退出时间。要创建服务完请求后立即退出的服务器，可以使用 `-K 0`。要创建永不退出的服务器，应使用 `-K -1`。

- `-l`

  编译为客户端存根。

- `-m`

  编译为服务器端存根，但不生成 *main* 例程。

- `-n` *netid*

  编译为 *netid* 指定的传输方式的服务器端存根。`netconfig` 数据库中应有 *netid* 的条目。

- `-N`

  使用 `rpcgen` 的新风格，允许过程具有多个参数。

- `-o` *outfile*

  指定输出文件的名称。

- `-s` *nettype*

  编译为属于 *nettype* 类的所有传输方式的服务器端存根。

- `-Sc`

  生成示例代码，展示如何使用远程过程以及在调用 `rpcgen` 生成的客户端存根之前如何绑定到服务器。

- `-Ss`

  生成服务器端远程过程的骨架代码。你需要填充远程过程的实际代码。

- `-t`

  编译为 RPC 调度表。

- `-T`

  生成支持 RPC 调度表的代码。

## strip

## 从目标文件中剥离

GNU 命令

`strip` *filename*

## 用途

`strip` 命令从目标文件中剥离符号。目标文件列表可以包含归档文件，但必须至少给定一个目标文件。**警告：** GNU 版本会修改其参数中命名的文件，而不是将修改后的副本写到不同名称的文件下，因此在命名方案中要小心谨慎。

## 选项

- `-F` *bfdname*

  将原始 *objfile* 视为具有目标代码格式 *bfdname* 的文件，并以相同格式重写。

- `-g`

  仅移除调试符号。

- `-I` *bfdname*

  将原始 *objfile* 视为具有目标代码格式 *bfdname* 的文件。

- `-K` *symbolname*

  从源文件中复制 *symbolname*。

- `-N` *symbolname*

  从源文件中移除 *symbolname*。

- `-O` *bfdname*

  用输出格式 *bfdname* 的文件替换 *objfile*。

- `-R` *sectionname*

  从文件中移除 *sectionname*。要小心——错误地移除某个节区可能导致目标文件无法使用。

- `-s`

  移除所有符号。

- `-S`

  仅移除调试符号。

- `--strip-unneeded`

  剥离重定位处理不需要的所有符号。

- `-v`

  在详细模式下工作，列出所有被修改的目标文件。

- `-x`

  移除非全局符号。

- `-X`

  移除编译器生成的局部符号（通常以 `L` 或 `.` 开头）。

## xgettext 从 C 程序中获取文本

```
xgettext option(s) filename
```

## 用途

`xgettext` 命令从 C 程序中提取字符串（文本）。它用于创建可移植的消息文件，其中包含指定文件名中源代码里 C 字符串的副本。可移植消息文件可以作为 `msgfmt` 工具的输入，该工具将生成应用程序运行时使用的消息文件的二进制形式。

## 选项

- `-a`

  提取 ALL 字符串，而不仅仅是那些在

- `-cflag`

  将 *flag* 开头的注释添加到 *filename*，作为 `#` 分隔的注释。

- `-d`

  产生重复内容，写入文件时不排序输出，也不覆盖现有的输出文件。

- `-mstring`

  用 `xgettext` 命令的输出填充 `msgstr` 行。

- `-n`

  向输出文件添加 `#` 分隔的行号注释，指示源文件中每个提取字符串遇到的行号。

- `-ofilename`

  使用 *filename* 作为默认输出文件。

- `-ppathname`

  设置输出文件的目录。

- `-xfilename`

  从提取过程中排除 *filename* 中找到的字符串。

- `-P`

  包含预处理器语句中的字符串。

## 相关命令

`msgfmt`

## xmkmf

## 创建 Makefile

X Window 系统命令

```
xmkmf option(s) topdirectory currentdirectory
```

## 用途

`xmkmf` 命令从 `Imakefile` 创建 `Makefile`。如果你的 Linux 系统未配置为处理 `Imakefile`，则应使用 `Makefile`。

## 相关命令

`imake`

## xxgdb

## X GDB 调试器

X Window 系统命令

`xxgdb` *option(s)*

## 用途

`xxgdb` 命令是 `gdb` 调试器的 X Window 系统前端。更多信息请参阅 `gdb` 命令。

## 选项

此命令接受所有 `gdb` 选项，以及以下选项。

- `-bigicon` — 使用更大的图标。

- `-db_name` — 指定要使用的调试器，而不是 `gdb`。

- `-db_prompt` — 设置新的调试器提示符。

- `-i` *filename* — 设置初始的 `gdb` 命令文件。

- `-nx` — 不执行 `gdb` 命令文件。

## 相关命令

`gdb`

## yacc

## YACC 解析器生成器

`yacc` *option(s)* *filename*

## 用途

`yacc` 命令读取文件中 *filename* 的语法规范，并为其生成 LR 解析器。解析器由一组 LALR 解析表和一个用 C 语言编写的驱动例程组成。解析表和驱动例程通常写入 `y.tab.c` 文件。

## 选项

- `-b` *prefix*

  将输出文件的名称前缀更改为 *prefix*。默认值为 `y`。

- `-d`

  写入头文件 `y.tab.h`。

- `-l`

  不将代码插入现有文件。

- `-r`

  将代码（`y.code.c`）和解析表（`y.tab.c`）生成到不同的文件中。

- `-t`

  更改预处理指令以包含调试信息。

- `-v`

  以人类可读的形式写入生成解析器的描述。

## 相关命令

`bison`

## 网络命令

这些命令用于连接到远程机器（无论是你的局域网还是互联网），连接成功后帮助你完成会话。

## dnshostname 显示域名

`dnshostname` *选项* *主机名*

## 用途

`dnshostname` 命令返回当前主机名的信息，而特权用户可以使用该命令设置新的主机名。

## 选项

- `-f` — 打印完整域名。

- `-s` — 打印短域名。

- `-F` *文件* — 从 *文件* 中检查主机名。

## dnsquery 查询 DNS 服务器

`dnsquery` *选项*

## 用途

`dnsquery` 命令通过 BIND 解析器库调用查询域名服务器。

## 选项

- `-n` *域名服务器* — 指定域名服务器，可以是 IP 地址或域名。

- `-t` *类型* — 设置感兴趣的资源记录类型，以下为可选值：

| 记录类型 | 描述 |
| --- | --- |
| A | 地址 |
| NS | 域名服务器 |
| CNAME | 规范名称 |
| PTR | 域名指针 |
| SOA | 起始授权机构 |
| WKS | 知名服务 |
| HINFO | 主机信息 |
| MINFO | 邮箱信息 |
| MX | 邮件交换 |
| RP | 负责人 |
| MG | 邮件组成员 |
| AFSDB | DCE 或 AFS 服务器 |
| ANY | 通配符 |

- `-c` *类别* — 设置感兴趣的资源记录类别，以下为可选值：

| 类别 | 描述 |
| --- | --- |
| IN | 互联网 |
| HS | Hesiod |
| CHAOS | Chaos |
| ANY | 通配符 |

- `-p` *数值* — 指定超时前等待的时间。

- `-r` *数值* — 设置域名服务器未响应时的重试次数。

- `-s` — 使用流而非数据包。

## faucet

## 网络管道修复

`faucet` *选项* *端口*

## 用途

`faucet` 命令是 BSD 网络管道的固定装置，提供网络上的管道功能。它作为服务器-客户端连接的服务器端，与 `hose` 配合良好，特别是在你无法轻松访问目标账户时（如 root 账户，其中 `.rhosts` 并非好主意）。基本上，`faucet` 创建一个 BSD 套接字，将其绑定到命令行指定的 *端口*，并监听连接。每次 `faucet` 获得连接时，它都会运行 *命令* 及其 *参数*。

`faucet` 命令不被认为是安全的网络方法。请谨慎使用。

## 选项

此命令还有更多选项；以下是最常用的。查看在线手册页获取完整列表。

- `-localhost` — 指定监听套接字应绑定到本地主机上的特定互联网地址。

- `-daemon` — 指定 `faucet` 在套接字上开始监听后，应使用 `setsid()` 系统调用与控制终端分离。

- `-shutdown` — 将双向套接字转为单向套接字。

- `-serial` — 告诉 `faucet` 在一个子进程完成之前等待，再接受更多连接。

- `-pidfile` *文件名* — 将其进程 ID 写入 *文件名*。

## fuser

## 文件使用者

`fuser` *选项 文件名*

## 用途

`fuser` 文件名列出使用特定文件或文件系统的进程 ID。返回的信息包括：

- `c` — 当前目录



- `e` — 可执行文件
- `f` — 打开的文件
- `m` — 映射文件或共享库
- `r` — 根目录

## 选项

- `-` — 将选项重置为默认值。
- `-signal` — 向进程发送信号。使用`-l`查看信号名称列表。
- `-a` — 显示所有文件，不仅仅是正在访问的文件。
- `-k` — 终止访问该文件的所有进程。
- `-l` — 返回信号名称列表。
- `-m` — 返回已挂载文件系统的信息。
- `-s` — 以静默模式运行。
- `-u` — 返回进程的用户名。
- `-v` — 以详细模式工作，返回进程 ID、用户名、命令名称和访问字段。

# `getpeername`

## 获取对端名称

`getpeername` 选项

## 用途

`getpeername` 返回套接字连接的信息。

## 选项

- `fd`：指定文件描述符。
- `verbose`：返回更详细的信息。

# `hose`

## 网络管道终端

`hose` 选项

## 用途

`hose` 命令是 BSD 网络管道的固定装置，提供网络上的管道功能。它作为服务器-客户端连接的客户端，与`faucet`配合良好，特别是在你无法轻松访问目标账户时（如 root 账户，其中`.rhosts`并非好主意）。基本上，`hose`创建一个 BSD 套接字，将其绑定到命令行指定的端口，并监听连接。每次`hose`获得连接时，它都会运行命令及其参数。

> `faucet` 命令不被认为是安全的网络方法。请谨慎使用。

## 选项

此命令还有更多选项；以下是最常用的。查看在线手册页获取完整列表。

- `-delay` `n` — 指定重试之间等待`n`秒。
- `-retry` `n` — 指定连接应重试`n`次。
- `-shutdown r` — 使其成为只读套接字。
- `-shutdown w` — 使其成为只写套接字。
- `-unix` — 指定端口不是互联网端口号或服务名称，而是 UNIX 域套接字的文件名。

# `host`

## 主机信息

`host` 选项 主机名 服务器

## 用途

`host` 命令使用 DNS 打印指定主机名或服务器的信息。你还可以指定 IP 地址，这些地址将通过 DNS 转换为主机名。

## 选项

- `-a` — 查找 ANY 类型的资源记录类别。
- `-A` — 查找主机名的 IP 地址，然后执行反向查找以验证是否匹配。还查找地址的主机名，然后执行反向查找以验证是否匹配。还检查给定区域中所有主机名的 IP 地址。如果完全匹配则返回无信息。
- `-c` 类别 — 查找指定的资源记录类别（ANY、CH、CHAOS、CS、CSNET、HS、HESIOD、IN、INTERNET 或 `*`）。默认为 IN。
- `-C` — 列出区域中的所有机器，确定区域的域名服务器是否权威。
- `-d` — 以调试模式工作。
- `-dd` — 以调试模式工作，但比`-d`更详细。
- `-D` — 返回区域中唯一主机的数量，以及每个名称有多个地址的主机名。
- `-e` — 抑制特定区域外主机的信息。
- `-E` — 返回区域中唯一主机的数量，以及区域外主机的名称。
- `-f` 文件 — 将输出发送到文件以及标准输出。
- `-F` 文件 — 将输出发送到文件，额外资源数据发送到标准输出。
- `-G` 区域 — 返回区域中唯一主机的数量和网关主机的名称。
- `-H` 区域 — 返回区域中唯一主机的数量。
- `-i` — 返回 IP 地址的信息：主机名和类别（始终为 PTR）。
- `-I` 字符 — 忽略关于主机名中包含非法字符的警告。
- `-l` 区域 — 返回区域中所有主机的信息。
- `-L` 级别 — 使用`-l`选项时指定搜索的级别。
- `-m` — 打印 MB、MG 和 MR 记录；将 MR 和 MG 记录扩展为 MB 记录。
- `-o` — 抑制将数据发送到标准输出。
- `-p` 服务器 — 返回特定区域中主服务器的信息。设计用于与`-I`选项配合使用。
- `-P` 服务器 — 返回首选主机的信息；服务器为逗号分隔的列表。与`-l`选项配合使用。
- `-q` — 在静默模式下抑制警告，但不抑制错误消息。
- `-r` — 从服务器请求缓存信息，而非新查询的信息。
- `-R` — 发现非完全限定名称时搜索本地命令的组成部分。
- `-S` — 将所有主机（但不包括子区域）返回到标准输出，包括主机类别和 IP 地址。与`-l`选项配合使用。
- `-t` 类型 — 请求资源记录中类型条目的信息；类型为 A、ANY、NS、PTR 或 `*`。
- `-T` — 打印缓存数据的生存时间信息。
- `-u` — 使用 TCP 而非 UDP。
- `-v` — 以详细模式工作。
- `-vv` — 以详细模式工作，包括`host`上的默认值。
- `-w` — 持续工作直到`host`返回信息。
- `-x` — 查询多个主机和区域；还可与`-X`配合使用查询多个服务器。
- `-X` — 查询多个服务器以及多个主机和区域。
- `-Z` — 在资源记录中包含尾随点，以及生存时间数据和类别名称。

## 相关命令

`hostname`

# `hostname`

## 设置主机名

`hostname` 选项 主机名

## 用途

`hostname` 命令返回当前主机名的信息，而具有权限的用户可以使用该命令设置新的主机名。

## 选项

- `-d`：打印域名系统（DNS）域名。
- `-f`：打印完整域名。
- `-s`：打印短域名。
- `-F` 文件：从文件中检查主机名。

# `ping`

## 用途

`ping` 命令向网络主机发送 ICMP ECHO_REQUEST 数据包，以确定网络性能。

## 选项

- `-c 次数`

  在发送（并接收）指定次数的 ECHO_RESPONSE 数据包后停止。

- `-d`

  在正在使用的套接字上设置 SO_DEBUG 选项。

- `-f`

  尽可能快地输出数据包，或者每秒一百次，以两者中更快的为准。

- `-i 等待时间`

  在发送数据包之间等待指定的秒数。

- `-l 预加载`

  在进入正常行为模式之前，尽快发送指定数量的数据包。

- `-n`

  以数字模式工作。

- `-p 模式`

  指定用于填充发送数据包的“填充”字节。

- `-q`

  以静默模式工作；除了启动时和完成时的摘要行外，不显示任何内容。

- `-r`

  绕过正常的路由表，直接发送到连接网络上的主机。

- `-R`

  在 ECHO_REQUEST 数据包中包含 RECORD_ROUTE 选项，并在返回的数据包上显示路由缓冲区。

- `-s 数据包大小`

  指定要发送的数据字节数。默认值为 56。

- `-v`

  打印详细输出。

# `rcp` 远程文件复制

`rcp` 选项 文件1 文件2

## 用途

`rcp` 命令在机器之间复制文件。这些机器可以是本地网络或互联网上的机器。

## 选项

- `-k` 领域：在指定的领域中获取远程主机的票据，而不是远程主机所在的领域。
- `-p`：保留修改时间。
- `-r`：递归复制目录。
- `-x`：使用 DES 加密对文件进行加密。

## 相关命令

`rlogin`

`rsh`

# `rlogin`

## 用途

`rlogin` 命令在指定的主机名上打开远程会话。它最初使用 Kerberos 授权，但如果远程主机不支持 Kerberos，则使用标准的 Berkeley `rhosts` 授权机制。（有关 Kerberos 认证的更多详细信息，请参阅在线手册页。）

## 选项

- `-8`：始终允许八位输入数据路径；否则，除非远程端的停止和启动字符不是 ^S/^Q，否则奇偶校验位会被剥离。
- `-d`：在用于与远程主机通信的 TCP 套接字上启用套接字调试。
- `-e`：定义转义字符，替换默认的波浪号（~）字符。
- `-E`：阻止任何字符被识别为转义字符。
- `-K`：关闭 Kerberos 认证。
- `-k`：在指定的领域中获取远程主机的票据，而不是由`krb_realmofhost`确定的远程主机所在领域。
- `-L`：在`litout`模式下运行会话。
- `-x`：启用 DES 加密。

## 相关命令

`rsh`

`kerberos`

`krb_sendauth`

`krb_realmofhost`

# `rsh`

## 远程 Shell

`rsh` 选项 主机名 命令

## 用途

`rsh` 在远程主机名上运行命令。它将标准输入复制到远程命令，将远程命令的标准输出复制到其标准输出，并将远程命令的标准错误复制到其标准错误。中断、退出和终止信号会传播到远程命令；`rsh`通常在远程命令结束时终止。

## 选项

- `-K`

  关闭 Kerberos 认证。

- `-d`

  启用套接字调试。

- `-k` 领域

  在指定的领域中获取远程主机的票据，而不是由`krb_realmofhost`确定的远程主机所在领域。

- `-l` 用户名

  指定远程用户名。

- `-n`

  从特殊设备`/dev/null`重定向输入。

- `-x`

  启用 DES 加密。

# `rstart`

## 远程启动

X Window 系统命令

```
rstart 选项 主机名 命令 参数
```

## 用途

`rstart` 命令实际上是一个远程启动客户端的示例实现。它使用`rsh`作为其底层远程执行机制。

## 选项

| 选项 | 描述 |
| :--- | :--- |
| `-c` 上下文 | 指定命令的上下文，即通用环境。默认为 X。 |
| `-g` | 将命令行上的命令解释为通用命令，如协议文档中所定义。 |
| `-l` 用户名 | 告诉`rsh`以指定的用户名运行命令。 |
| `-v` | 以详细模式运行，丢弃来自远程主机`rstart`助手的输出，并断开与`rsh`连接的关联。 |

## 相关命令

- `rsh`
- `rstartd`

# `rusers`

## 当前用户

`rusers` 选项 主机名

## 用途

`rusers` 命令生成有关特定主机（或主机）或本地网络上所有机器上已登录用户的信息。

## 选项

- `-a`：列出所有机器，即使当前没有用户登录。
- `-l`：以长格式返回列表：用户名、主机名、用户登录的 tty、用户登录的日期和时间、自用户上次在键盘上打字以来的时间，以及他们从中登录的远程主机（如适用）。

## 相关命令

- `rwho`
- `users`
- `who`

# `rwall`

## 向用户写入

```
rwall 主机名 文件名
```

## 用途

`rwall` 命令向指定主机名上所有已登录用户发送消息。消息可以通过指定的文件名发送，也可以直接输入并以 EOF（Ctrl-D）终止。

# `rwho`

## 谁已登录

`rwho` 选项

## 用途

`rwho` 命令显示谁在本地机器上登录。输出类似于`who`，只是信息涵盖本地网络上的所有人。如果某台机器在 11 分钟内未向`rwho`报告，则假定该机器已宕机。同时报告用户不到一小时的空闲时间。

## 选项

- `-a`：报告所有用户，即使那些在过去一小时内未在其机器上打字的人。

## 相关命令

`rusers`

# `sliplogin`

## SLIP 登录

`sliplogin` 登录名

## 用途

`sliplogin` 命令允许您使用 SLIP 连接登录互联网系统。它从`/etc/slip.hosts`文件中获取信息（匹配登录名），然后启动连接。`/etc/slip.hosts`文件必须由 root 用户配置。

# `sockdown`

## 关闭套接字

GNU 命令

`sockdown` 选项

## 用途

`sockdown` 命令对其由`fd`指定的文件描述符执行`shutdown`系统调用。`how` 的可能值包括：

- `0` — 转换为只写文件描述符
- `writeonly` — 与上述相同的符号表示
- `1` — 转换为只读文件描述符
- `readonly` — 与上述相同的符号表示
- `2` — 完全关闭—将来不允许任何读取或写入
- `totally` — 与上述相同的符号表示

# 与另一用户交谈

```
talk 用户名 [tty]
```

## 用途

`talk` 命令允许您与当前登录系统的另一用户进行交互式聊天。当双方都运行`talk`命令时，屏幕会分割，一个用户的打字显示在屏幕的一半，另一个用户的打字显示在屏幕的另一半。

用户名可以是您自己系统上的某人。如果您想与另一系统上的用户聊天，则必须将用户名指定为`user@host`。如果用户有多个终端在使用，可以使用`tty`指定终端。

要退出`talk`，请键入 Ctrl-D。

## 相关命令

`write`

# `telnet`

## 远程连接

`telnet` 选项(s) 主机名

## 用途

`telnet` 命令使用 Telnet 协议启动与远程主机的连接。连接成功后，你就可以像使用自己的机器一样使用远程主机。

## 选项

- `-a`：尝试自动登录。
- `-d`：开启调试模式。
- `-e` 转义字符：设置转义字符。
- `-l` 用户：将用户作为变量 USER 发送给远程系统；与`-a`一起使用。
- `-n` 跟踪文件：将跟踪信息记录到跟踪文件中。

# `uucp`

## UNIX 到 UNIX 的复制

```
uucp 选项(s) 源文件 目标文件
uucp 选项(s) 源文件 目标目录
```

## 用途

`uucp` 命令在系统之间复制文件。有关可用选项的列表，请参阅在线手册页。

# `write`

## 向另一用户写入

`write` 用户

## 用途

`write` 命令向另一用户发送消息，该用户可以选择是否继续对话。

# `ytalk`

## 聊天程序

`ytalk` 选项(s) 用户名

## 用途

`ytalk` 命令是一个多用户聊天程序。它还可以用于与`talk`用户聊天。

## 选项

- `-x`：禁用 X Window System 界面。
- `-s`：在 shell 中启动`ytalk`窗口。

## 相关命令

`talk`

# 系统管理命令

这些命令让你的 Linux 系统运行更加顺畅，范围从调度系统杂务到直接处理 PC 硬件。

## 在特定时间运行命令

```
at 选项(s) 时间 日期
at -c 作业-ID
```

## 用途

`atailable` 命令在特定的时间和/或特定的日期运行一个命令或一组命令。这些命令必须是自给自足的，不需要你或其他用户的输入。通常，这些命令是系统管理命令，涉及系统备份、电子邮件投递等。

`at` 命令的命令和时间直接在命令行输入。首先输入`at`命令，然后输入命令运行的时间，接着输入要运行的命令。完成后，按`Ctrl-D`。在指定时间，`at`会运行该命令；如果命令有任何输出，将以电子邮件形式发送给你。

在设置作业时，你有许多选项。你可以使用`HHMM`格式或`HH:MM`格式（24 小时制）指定时间，假设命令将从即将到来的第一个实例开始运行。你还可以指定`AM`或`PM`。你也可以使用`midnight`、`noon`或`teatime`（下午 4 点）等词来指定时间。命令还可以设置为在特定日期运行，使用`MMDDYY`、`MM/DD/YY`或`DD.MM.YY`形式。（注意斜杠和点的使用。）

还可以设置从当前时间开始的特定间隔。例如，你可以告诉`at`在两周后运行一个命令，使用`today + 2 weeks`作为指定符。其他间隔包括`minutes`、`hours`和`days`。你可以按以下方式组合时间和日期：`at 4pm + 3 days`。最后，你可以将时间与`tomorrow`组合：`at 1pm tomorrow`。

并非所有用户都能访问此命令。`root`用户始终可以访问`at`命令。此外，超级用户可以通过`/etc/at.allow`和`/etc/at.deny`文件中的用户名来指定哪些用户可以访问`at`命令，以及明确拒绝特定用户的访问。如果`/etc/at.allow`存在，则只有该文件中的用户名才能运行`at`命令；如果不存在，则检查`/etc/at.deny`，结果是任何未在`/etc/at.deny`中提到的人都可以使用`at`命令。

### 示例

```
$ at 1am
ls
Ctrl-D
```

## 选项

- `-b`：与`batch`命令相同。
- `-d`：与`atrm`命令相同。
- `-f` 文件：从文件而不是标准输入中获取输入（即命令的名称）。
- `-l`：与`atq`命令相同。



- `-m`：作业完成时发送电子邮件。
- `-q 队列`：使用队列指定符为`at`命令设置 nice 值。该指定符为单个字母，范围从`a`到`z`。字母越高，命令运行得"越友好"（有关 nice 值和 Linux 操作系统的说明，请参阅`nice`）。`at`的默认值是`c`，因此如果你希望在系统压力较小时运行命令，可以选择`m`这样的字母作为队列指定符。相反，如果你希望无论如何都要运行命令，则应使用`a`作为队列指定符。
- `-v`：打印版本号。

## 相关命令

- `atq`
- `atrm`
- `batch`

## `atq`

### 打印 At 作业

`atq 选项 用户 作业-ID`

### 用途

`atq`命令列出已使用`at`命令调度的所有作业（对于超级用户）或特定用户的作业，以及特定作业 ID。这与`at -l`相同。

### 选项

- `-q 队列`：使用队列指定符为`at`命令设置 nice 值。该指定符为单个字母，范围从`a`到`z`。字母越高，命令运行得"越友好"（有关 nice 值和 Linux 操作系统的说明，请参阅`nice`）。`at`的默认值是`c`，因此如果你希望在系统压力较小时运行命令，可以选择`m`这样的字母作为队列指定符。相反，如果你希望无论如何都要运行命令，则应使用`a`作为队列指定符。
- `-v`：显示已完成但尚未从队列中删除的作业。

## 相关命令

- `at`
- `atrm`
- `batch`

## `atrm`

### 删除作业

`atrm 选项 用户 作业-ID`

### 用途

`atrm`命令删除使用`at`命令调度的作业。超级用户可以删除所有作业，而其他用户只能删除自己的作业。这与`at -d`相同。

## 相关命令

- `at`
- `atq`
- `batch`

## `batch`

### 运行批处理命令

`batch 选项(s) 时间`

### 用途

`batch`命令一次运行一系列从命令行作为标准输入输入的命令。`batch`和`at`的区别在于`batch`在系统负载较轻时自动运行命令；在这种情况下，你不指定命令何时运行。但是，你可以使用`batch`命令指定执行时间。

从命令行输入完命令后，使用`Ctrl-D`结束输入。

### 选项

| 选项 | 说明 |
| --- | --- |
| `-f 文件` | 从`文件`而不是命令行的标准输入运行命令。 |
| `-m` | 作业完成时发送电子邮件。 |

### 示例

```shell
$ batch
pr -aBAT_ID kevin.memo
lp kevin.memo
Ctrl-D
```

## 相关命令

`at`

## `cpio`

### 创建归档

`cpio 标志 选项(s)`

### 用途

`cpio`命令用于创建归档，可以在本地文件系统或磁带备份上。默认是复制到磁带归档。

### 标志

`cpio`命令必须与以下一个或多个标志结合使用：

- `-i 选项 模式`：复制与`模式`匹配的所有文件，模式可以包含通配符。（如果使用通配符，必须用引号引起来，以便 shell 不会解释它们。）如果未指定`模式`，则复制所有文件。
- `-o 选项`：复制按名称指定的所有文件。
- `-p 选项 目录`：将文件复制到本地目录，而不是磁带归档。

每个标志可用的选项是各选项说明的一部分。

### 选项

- `-0`：文件列表以空字符结尾，而不是换行符；这样文件名中包含换行符的文件也可以被包含。（与`-i`和`-p`标志一起使用。）
- `-a`：将文件的访问时间设置为现在。（与`-i`和`-p`标志一起使用。）
- `-A`：将新文件追加到磁盘上的现有归档。这必须与`-O`或`-F`选项一起使用。（与`-i`和`-p`标志一起使用。）
- `-b`：交换半字和字节。（与`-o`标志一起使用。）
- `-B`：将块大小设置为每条记录 5120 字节，而不是默认的每条记录 512 字节。（与`-i`和`-o`标志一起使用。）
- `-c`：以 ASCII 文本形式读取和写入头信息。（与`-i`和`-o`标志一起使用。）

## `cpio`

### 创建归档

- `-C num`

  将块大小设置为`num`，而非默认的每记录 512 字节。（与`-i`和`-o`标志配合使用。）

- `-d`

  根据需要创建目录。（与`-o`和`-p`标志配合使用。）

- `-E file`

  从归档文件`file`中提取找到的文件。（与`-o`标志配合使用。）

- `-F file`

  使用`file`作为归档文件。（与`-i`和`-o`标志配合使用。）

- `-H type`

  指定格式`type`，在将归档文件移动到非 Linux 机器时很有用。默认值为`bin`（二进制格式）。其他类型包括`crc`（带校验和的 SVR4）、`hpodc`（惠普便携格式）、`newc`（SVR4 便携格式）、`odc`（POSIX.1 便携格式）、`tar`或`ustar`（POSIX.1 tar）。（与`-i`和`-o`标志配合使用。）

- `-I file`

  将`file`作为输入归档文件读取。（与`-o`标志配合使用。）

- `-l`

  建立链接而非复制文件。（与`-p`标志配合使用。）

- `-L`

  跟随任何符号链接。（与`-i`和`-p`标志配合使用。）

- `-m`

  保留修改时间。（与`-o`和`-p`标志配合使用。）

- `-M mesg`

  在切换介质时打印`mesg`。必须与`-I`或`-O`配合使用。（与`-i`和`-o`标志配合使用。）

- `-n`

  显示用户和组 ID；必须与`-v`配合使用。（与`-o`标志配合使用。）

- `-O file`

  将输出定向到另一台机器上的`file`。（与`-i`标志配合使用。）

- `-r`

  重命名文件；提示您输入新文件名。（与`-o`标志配合使用。）

- `-s`

  交换字节。（与`-o`标志配合使用。）

- `-S`

  交换半字。（与`-o`标志配合使用。）

- `-t`

  打印预定归档文件的内容表；实际上不创建归档。（与`-o`标志配合使用。）

- `-u`

  新文件可以无条件覆盖旧文件。（与`-o`和`-p`标志配合使用。）

- `-v`

  启用详细模式，列出所有文件。（与所有标志配合使用。）

- `-V`

  启用修改的详细模式，用点代替文件名打印。（与所有标志配合使用。）

## 相关命令

`tar`

## `cron`

### Cron 守护进程

`crond 选项(s)`

### 用途

`crond`命令启动`cron`守护进程，该进程扫描`crontab`文件并在适当的时间运行其中的命令。`cron`系统是一种设置任务以使其定期执行的方式。

### 选项

- `-b`

  在后台运行`crond`；除非指定`-d`，否则这是默认设置。

- `-c 目录`

  指定包含`crontab`文件的目录。

- `-d[调试级别]`

  设置调试级别；默认值为零。

- `-f`

  在前台运行`crond`。

- `-l 日志级别`

  设置日志级别；默认值为 8。

## `ctlinnd`

### 控制 InterNetNews

`ctlinnd 选项(s)`

### 用途

`ctlinnd`命令向 InterNetNews 服务器`innd`的控制通道发送消息。在正常运行模式下，消息被发送到服务器，然后服务器执行请求的操作，并将带有文本消息和`ctlinnd`退出代码的回复发送回来。

与此命令关联的选项和命令列表很长；有关更多信息，请查看在线手册页。

## 相关命令

`innd`

## `df`

### 磁盘空闲空间

`df 选项(s) 磁盘设备`

### 用途

`df`命令返回 Linux 系统上空闲磁盘空间量，可以是在所有已挂载的硬盘系统上，也可以是在特定的`磁盘设备`上。`磁盘设备`必须是设备名称（如`/dev/hd1`、`/dev/hd2`等）或特定目录（如`/bin`）。空间以 1K 块为单位显示。

### 选项

- `-a`：报告所有文件系统，包括那些有 0 块（空文件系统）的。
- `-i`：以 inode 格式报告：已用、空闲和已用百分比的 inode。
- `-P`：以 POSIX 格式报告：每个文件系统一行。
- `-t 类型`：报告特定`类型`的设备。
- `-T`：返回每个文件系统的`类型`。
- `-x 类型`：排除特定`类型`的设备。

## 相关命令

`du`

## `diskd`

### 磁盘守护进程

`diskd 选项(s)`

### 用途

`diskd`守护进程等待磁盘插入指定的驱动器，然后运行命令或退出。当您希望在插入磁盘后立即将其自动挂载时，这很有用。

已知长时间重复使用此命令会导致硬件损坏。

### 选项

- `-d 驱动器`：指定要监控的驱动器。默认为驱动器 0（`/dev/fd0`）。
- `-i 间隔`：设置轮询间隔，以十分之一秒为单位。默认为 10（一秒）。
- `-e 命令`：指定磁盘插入后要执行的`命令`。

## `diskseek`

### 磁盘寻道守护进程

`diskseek 选项(s)`

`diskseekd 选项(s)`

### 用途

`diskseek`命令访问软盘驱动器以清除灰尘。（真的！）有两种方式调用此命令。您可以使用`diskseek`一次性访问驱动器，或者使用`diskseekd`每 16 分钟访问一次驱动器。

### 选项

- `-d 驱动器`：设置要访问的驱动器；默认为驱动器 0（`/dev/fd0`）。
- `-i 间隔`：设置访问驱动器的`间隔`（以秒为单位），如果您运行的是`diskseekd`。默认为 1000 秒。您可以将`diskseekd`与间隔 0 结合使用，这在从`crontab`使用`diskseek`时很有用。
- `-p pid文件`：将`diskseekd`守护进程的进程 ID 存储在`pid文件`中，而非默认的`/var/run/diskseekd.pid`。

## `du`

### 磁盘使用量

`du 选项(s) 文件(s) 目录`

### 用途

`du`命令以 1K 块为单位列出文件或目录（及其所有子目录）使用的磁盘空间量。如果未指定文件或目录，则默认为当前目录。

### 选项

- `-a`：返回所有文件的信息，而不仅仅是目录。
- `-b`：以字节（而非块）为单位返回信息。
- `-c`：总计所有列出的文件和目录。
- `-D`：包括作为命令行的符号链接。
- `-k`：以千字节（默认）为单位返回信息。
- `-l`：总计所有文件，包括可能已被计入的链接。
- `-L`：包括符号链接。
- `-r`：当`du`无法访问文件或目录时报告。
- `-s`：在静默模式下工作，仅报告总计。
- `-S`：从总计中排除子目录。

## 相关命令

`df`

## `fdisk`

### 磁盘分区工具

`fdisk 选项(s) 设备`

### 用途

`fdisk`命令在硬盘上创建和删除分区。硬盘设备通常是以下之一：

- `/dev/hda`
- `/dev/hdb`
- `/dev/sda`
- `/dev/sdb`

分区由设备名称后跟分区号指定。例如，第一个硬盘驱动器上的第一个分区是`/dev/hda1`。

### 选项

`-l`

列出所有已知硬盘的分区表，然后退出。

`-s 分区`

打印非 DOS`分区`的大小。

## `fdmount`

### 挂载软盘

`fdmount 选项(s)`

### 用途

`fdmount`挂载软盘。这可以是 Linux 格式的软盘，也可以是 MS-DOS 软盘。它还会检查磁盘是否写保护，如果是，则以只读方式挂载。

### 选项

- `-d`

  以守护进程模式运行。

- `--detach`

  在后台运行守护进程，并将其与其终端分离。

- `-f`

  即使`/etc/mtab`分别表示驱动器已挂载或未挂载，也尝试执行挂载或卸载操作。

- `-h`

  显示简短的参数说明。

- `-i 间隔`

  设置守护进程模式的轮询间隔。

- `-l`

  列出所有已知的驱动器及其符号名称、类型和挂载状态。

- `-p 文件`

  将守护进程的进程 ID 转储到`文件`。

- `--nodev`

  使用 NODEV 选项挂载。

- `--noexec`

  使用 NOEXEC 选项挂载。

- `--nosuid`

  使用 NOSUID 选项挂载。对 MS-DOS 文件系统忽略。

- `--nosync`

  即使不在守护进程模式下运行，也不使用 SYNC 选项挂载。

- `-o 选项`

  设置 MS-DOS 特定的文件系统选项：`check`、`conv`、`dotsOK`、`debug`、`fat`、`quiet`、`blocksize`。

- `-r`

  以只读方式挂载磁盘。

- `-s`

  使用 SYNC 选项挂载。

## 相关命令

- `mount`
- `mmount`
- `superformat`
- `floppycontrol`
- `setfdprm`

## `fdrawcmd`

### 软盘控制器

`fdrawcmd 选项`

### 用途

`fdrawcmd`向软盘控制器发送原始命令。您必须对选定的驱动器具有写权限。

此命令关联有多种命令。更多信息请参阅在线手册页。

### 选项

所有数字可以用八进制（0209）、十进制（137）或十六进制（0x89）表示。

- `command`：直接发送`command`。
- `drive=drive`：指定驱动器；默认为 0（`/dev/fd0`）。
- `length=length`：设置从磁盘读取和写入数据命令的传输数据长度。
- `mode`：指定多个通过"或"运算组合在一起的标志，描述`command`的属性。
- `parameter`：为`command`设置参数。
- `rate=rate`：指定数据传输速率：0 表示高密度，1 表示双密度 5.25 英寸磁盘，2 表示双密度 3.5 英寸磁盘。
- `repeat=count`：将命令重复`count`次。

## `fdformat`

### 软盘格式化

`fdformat 选项 设备`

### 用途

`fdformat`用于格式化软盘驱动器。这格式化为 Linux 格式，而非正常的 DOS 格式。软盘设备名通常为`/dev/fd0`或`/dev/fd1`。

### 选项

- `-n`：跳过格式化验证。

## `free`

### 空闲内存

`free 选项`

### 用途

`free`命令返回有关内存使用情况的信息：总空闲内存、已用内存、共享内存和缓冲区。

### 选项

- `-b`：以字节为单位返回信息。
- `-k`：以千字节为单位返回信息（默认值）。
- `-m`：以兆字节为单位返回信息。
- `-o`：抑制`buffer adjusted`行。
- `-s time`：每隔`time`秒定期返回信息。
- `-t`：在一行上打印信息。

## 相关命令

`du`

## `ftpd`

### FTP 守护进程

`ftpd 选项`

### 用途

`ftpd`命令启动 DARPA FTP 守护进程，用于处理传入的 FTP 请求。它使用 TCP 协议，并在`services`文件的 ftp 服务中指定的端口进行监听。

### 选项

- `-a`：使用`ftpaccess`文件来控制访问。
- `-A`：禁用`ftpaccess`访问控制。
- `-d`：开启调试模式。
- `-l`：在 syslog 中记录会话。
- `-L`：在 syslog 中记录所有会话。
- `-t timeout`：设置`timeout`秒的非活动超时时间。
- `-i`：将上传的文件传输记录到`xferlog`文件。
- `-o`：将下载的文件传输记录到 syslog。

## 相关命令

- `ftp`
- `inetd`

## `ftpwho`

### 用途

`ftpwho`命令显示每个 ftp 用户的当前进程信息。

## 相关命令

`ftpcount`

## `httpd`

### Apache Web 服务器

`httpd 选项`

### 用途

`httpd`命令启动 Apache Web 服务器。它可以作为守护进程启动，并始终在后台运行（最高效的配置），也可以在每次请求 HTTP 服务时由 Internet 守护进程`inetd`调用。

### 选项

- `-d serverroot`

  将`ServerRoot`变量的初始值设置为`serverroot`。此变量指定 Web 服务器程序的实际位置。默认值为`/usr/local/etc/httpd`。

- `-f config`



在启动时运行`config`文件中的命令。如果`config`不以`/`开头，则将其视为相对于`ServerRoot`的路径。默认值为`conf/httpd.conf`。

- **-X**

  以单进程模式运行。这在调试 Web 设置时很有用，但在向外界提供 Web 服务时应避免使用。

## 相关命令

`inetd`

`imapd`

## 用途

`imapd`命令启动一个支持 IMAP 远程邮件访问协议的邮件服务器。它很少在命令行上单独启动，而是通过在`inetd`守护进程配置中与其他 Internet 服务器工具一起启动。

## 相关命令

`inetd`

`inetd`

Internet 服务器

`inetd` *选项*

## 用途

`inetd`命令启动一系列 Internet 服务。传入的请求在此处进行路由——此守护进程监听指定 Internet 套接字上的连接，当套接字上有连接建立时，`inetd`决定哪个服务应处理该套接字连接。它通常由`/etc/rc.local`在启动时运行。

有关配置此文件的更多信息，请参阅在线手册页。

## 选项

**-d**

开启调试。

## 相关命令

`ftpd`

`telnetd`

`inews`

发送新闻

`inews` *选项*

## 用途

`inews`命令从文件或标准输入（如果未指定文件）读取 Usenet 新闻文章（可能包含头信息），检查格式是否符合 Usenet 标准，然后将文章传递给`inn.conf`文件中指定的 Usenet 新闻服务器。输入由文章头信息、一个空行和消息正文组成。

有关配置选项和命令行选项，请查阅在线手册页。

## 相关命令

- `injnews`

- `innd`

`inews`

发布新闻文章

`injnews` *选项*

## 用途

`inews`命令从文件或标准输入（如果未指定文件）读取 Usenet 新闻文章（可能包含头信息），检查格式是否符合 Usenet 标准，然后将文章传递给`inn.conf`文件中指定的 Usenet 新闻服务器。输入由文章头信息、一个空行和消息正文组成。

有关配置选项和命令行选项，请查阅在线手册页。

## 相关命令

- `inews`

- `innd`

`inews`

新闻组转发

`inews` *选项* *文件名*

## 用途

`inews`命令从文件读取 Usenet 新闻文章，添加一些头信息，并执行一些一致性检查。如果新闻文章通过检查，则将其传递给`inn.conf`文件中指定的 Usenet 新闻服务器。

## 选项

| 选项 | 描述 |
|--------|-------------|
| `-D` | 以调试模式工作。 |
| `-o` *organization* | 指定新的`organization`。 |
| `-O` | 不填写`Organization`字段。 |
| `-R` | 拒绝控制消息。 |

## 相关命令

`innd`

`innd`

InterNetNews 守护进程

`innd` 选项

## 用途

`innd`命令启动 InterNetNews 守护进程，处理所有传入的 NNTP 源。它将`active`、`newsfeeds`和`hosts.nntp`文件读入内存。然后打开 NNTP 端口以接收来自远程站点的文章，并打开一个命名管道供`ctlinnd`使用，以指导服务器执行某些操作。它还打开`history`数据库和两个日志文件，以替换其标准输出和标准错误。

一旦文件和套接字打开，`innd`就使用 select 和非阻塞 I/O 等待连接及其端口上的数据就绪。如果没有可用数据，则它将刷新其内存中的数据结构。

配置此命令可能是一件复杂的事情；更多信息请查阅在线手册页。

`lilo`

Linux 引导加载程序

`lilo` *选项*

## 用途

`lilo`命令安装 Linux 引导加载程序，控制 Linux 的启动方式。以前，当您想在系统中与其他操作系统一起使用 Linux 时，您需要安装`lilo`以确保加载首选的操作系统——或者更确切地说，首选的内核。如今，有其他比`lilo`更好的引导工具。**警告**：如果您是新用户，请不要使用`lilo`作为引导管理器。

## 选项

- `-v`

  以详细模式运行，提供更多有关其活动的信息。

- `-q`

  列出`/boot/map`中的当前映射文件。

- `-m` *映射文件*

  使用`映射文件`替代默认的映射文件。

- `-C` *配置文件*

  指定非默认的配置。

- `-d` *延迟*

  在加载列表中的第一个内核之前等待`延迟`个十分之一秒。

- `-D` *标签*

  使用带有`标签`的内核作为默认启动内核，而非列表中的第一个。

- `-r` *根目录*

  对`根目录`执行`chroot`；用于从引导软盘修复设置时。

- `-t`

  测试而不写入新的引导扇区或映射文件。

- `-c`

  开启映射压缩，合并来自相邻扇区的读取请求。

- `-f` *磁盘表*

  设置磁盘几何参数文件；默认值为`/etc/disktab`。

- `-i` *引导扇区*

  设置新的引导扇区文件；默认值为`/boot/boot.b`。

- `-l`

  生成线性扇区地址，而非扇区/磁头/柱面地址。

- `-P` {fix|ignore}

  修复或忽略损坏的分区表。

- `-s` *保存文件*

  将旧的引导扇区信息保存在`保存文件`中。

- `-S` *保存文件*

  将旧的引导扇区信息保存在`保存文件`中，如果已存在则覆盖。

## `lilo` Linux 加载器

续

| 选项 | 说明 |
|---|---|
| **-u** *device-name* | 通过复制回`device-name`（保存的引导记录）卸载 LILO，并检查时间戳。 |
| **-U** *device-name* | 通过复制回`device-name`（保存的引导记录）卸载 LILO，但不检查时间戳。 |
| **-R** *command line* | 为引导加载器在下次执行时设置默认的`command line`。 |
| **-I** *label* | 指定运行内核的路径名，由`label`指定。 |

### `makefloppies`

#### 软盘节点

`makefloppies` *option(s)*

## 用途

`makefloppies` shell 脚本创建新的软盘块设备文件。它使用`floppycontrol`程序将次设备号转换为有意义的名称。它还根据这些名称以及物理驱动器的类型来决定是否创建某个块设备文件。

## 选项

- **-l** 使用本地目录，而非`/dev`。
- **-n** 报告将要执行的操作，但不实际执行。
- **-t** 按驱动器类型命名设备，而非软盘类型。

## 相关命令

- `floppycontrol`
- `mtools`
- `rawcmd`
- `setfdprm`
- `superformat`

## `md5sum` - 检查 MD5 消息摘要

GNU 命令

`md5sum` *option(s) filename*

## 用途

`md5sum`命令计算并检查 MD5 消息摘要。它生成一个 128 位的指纹或消息摘要。它还检查其他文件中存在的消息摘要是否相同。

## 选项

- **-b**：假定所有文件均为二进制文件。
- **-c** *file*：检查`file`（MD5 校验和、二进制//text 标志以及文件名）是否正常。
- **-s** *string*：为`string`计算消息摘要。
- **-t** *text*：假定所有文件均为文本文件。

### `mount`

## 用途

`mount`命令挂载文件系统。这是一个复杂的命令，供系统管理员使用；更多信息请参阅在线手册页。

### 挂载磁带驱动器

GNU 命令

```
mt option operation count
```

## 用途

`mt`命令控制磁带驱动器。默认磁带驱动器的名称是`/usr/include/sys/mtio.h`，但这可以通过环境变量`TAPE`或`mt`的命令行选项来覆盖。每个使用该命令的命令行都应以操作结尾。

### 操作

| 操作 | 说明 |
|-----------|-------------|
| `asf` *count* | 将绝对空间设置为文件号`count`。等效于先倒带再执行`fsf` *count*。 |
| `bsf` *count* | 后退`count`个文件。磁带定位在下一个文件的第一个块上。 |
| `bsfm` | 后退`count`个文件标记。磁带定位在文件标记的磁带始端一侧。 |
| `bsr` *count* | 后退`count`个记录。 |
| `eof`, `weof` *count* | 在当前位置写入`count`个 EOF 标记。 |
| `eom` | 跳到磁带上已记录媒体的末尾（用于在磁带上追加文件）。 |
| `erase` | 擦除磁带。 |
| `fsf` *count* | 前进`count`个文件。磁带定位在下一个文件的第一个块上。 |
| `fsr` *count* | 前进`count`个记录。 |
| `offline`, `rewoffl` | 倒带并卸载磁带。 |
| `retension` | 倒带，然后将磁带卷到卷轴末端，再重新倒带。 |
| `rewind` | 倒带。 |
| `status` | 打印磁带设备的状态信息。 |

## 选项

| 选项 | 说明 |
|--------|-------------|
| `-f` *device* | 使用`device`而非默认磁带驱动器。 |

### `pkgtool`

### 软件维护

`pkgtool` *option(s)*

## 用途

`pkgtool`命令是 Slackware Linux 发行版提供的标准软件包维护工具。`setup`实用程序调用它来执行系统安装。它也可以不带任何参数调用，此时将允许用户通过交互式菜单系统安装、删除（或在彩色版本中查看）软件包。`pkgtool`实用程序有两个版本：`/sbin/pkgtool.tty`和`/usr/lib/setup/cpkgtool`。它们的功能类似，但第一个使用标准 tty 文本输出，而第二个使用全屏（可能为彩色）ncurses 输出。彩色版本依赖于`/usr/lib/terminfo`终端库的存在。

## 选项

大多数用户运行`pkgtool`时不希望使用任何选项。这些选项通常仅在`setup`运行`pkgtool`时使用。欢迎尝试使用它们，但请谨慎。

- **-sets #A#B#C#** — 安装磁盘集 A、B、C。使用#符号分隔磁盘集名称。
- **-source_mounted** — 不尝试在每次更换磁盘时卸载并重新挂载源设备。
- **-ignore_tagfiles** — 安装遇到的每个`.tgz`软件包，无论标签文件如何说明。
- **-tagfile** *tagfile* — 指定标签文件。
- **-source_dir** *directory* — 指定可以找到每个磁盘的子目录的目录。
- **-target_dir** *directory* — 指定目标根目录的位置。
- **-source_device** *device* — 指定要安装自的源设备。如果已提供`-source_mounted`选项，则不使用此项。它通常用于从软盘安装时，例如`-source_device/dev/fd0u1440`或`-source_device /dev/fd1h1200`。

### `quota`

### 磁盘使用情况

`quota` *option(s)*

`quota` *option(s)* user

`quota` *option(s)* group

## 用途

`quota`命令显示特定用户、所有用户或组的磁盘使用情况和限制。

## 选项

- **-g** 打印用户所属组的组配额。
- **-q** 返回使用量超过配额的文件系统信息。
- **-v** 显示未分配存储空间的文件系统上的配额。

按组分类的 Linux 命令

### `readprofile`

### 读取内核配置文件

`readprofile` *option(s)*

## 用途

`readprofile`命令传递 /proc/profile 信息，以三列形式打印以下数据：时钟滴答数、内核中发生这些滴答数的 C 函数，以及该例程的归一化负载，计算为滴答数与例程长度之比。

## 选项

- **-a** 打印映射文件中的所有符号。
- **-i** 提供内核使用的分析步骤信息。
- **-m** *mapfile* 指定`mapfile`，默认值为`/usr/src/linux/System.map`。当映射文件不是您最后编译的文件时，这很有用。
- **-p** *profile* 指定不同的分析缓冲区，默认值为`/proc/profile`。
- **-r** 重置分析缓冲区。
- **-t** 提供简洁格式输出（未填充）。
- **-v** 提供详细格式输出：分为四列并用空白填充。它添加了内核函数的 RAM 地址。

## `relaynews`：管理 Usenet 新闻

`relaynews` *option(s)*

## 用途

`relaynews`命令广播（网络）从其标准输入读取的新闻文章。

## 选项

- **-a** 不携带重复的文章。
- **-d** 开启调试。
- **-g** 在每篇文章中自动生成`Xref:`头。
- **-i** 将标准输出重定向至`/var/lib/news/log`。
- **-n** 启用 NNTP 模式，在此模式中历史条目会在文章被拒绝时生成。
- **-o** days 丢弃超过`days`天的文章。
- **-r** 分别将标准输出和错误信息重定向至`/var/lib/news/log`和`/var/lib/news/errlog`。
- **-s** 在丢弃文章之前发出警告。
- **-u** 在处理成功后取消链接（删除）任何文件名参数。
- **-x** excluded-site 从新闻邻居列表中排除`excluded-site`。

### `rexecd`

## 用途

`rexecd`启动远程执行服务器，允许远程用户打开`rexec`会话。

### `rmmod`

### 移除模块

`rmmod` *option* *module*

## 用途

`rmmod`命令从内核中卸载已加载的模块，只要它们没有被内核或其他模块使用。您可以指定多个模块，它们将按照在命令行中引用的顺序被移除。

## 选项

- **-r**：递归移除模块；如果指定了顶层模块，那么顶层模块使用的模块也将被移除。

## 相关命令

- `insmod`
- `lsmod`
- `ksyms`
- `modules`

## `rstartd`

### 远程启动助手

X Window System Command

`rstartd` *选项*

## 用途

`rstartd`命令是远程启动 rsh 助手的一个示例实现，与 rstart 命令协同工作。`rstartd`命令实际上是一个 shell 脚本，它使用 `-c` 选项调用 rstartserver。

## 选项

- **-c 配置文件名** 指定配置文件。

## 相关命令

- `rsh`
- `rstart`

## `sendmail`

## 发送/接收邮件

`sendmail` *选项*

## 用途

`sendmail`命令通过互联网发送和接收电子邮件。用户实际上并不直接访问它；相反，用户会使用更友好的前端界面（如 `mail`），然后将消息发送给`sendmail`，由它处理实际的邮件传输。

配置`sendmail`可能是一件棘手的事情，而且过于复杂，不适合在此详述。请参阅在线手册页或`sendmail`相关书籍以获取进一步指导。

## `sessreg`

## 设置 Utmp/Wtmp 条目

X Window System Command

`sessreg` *选项* *用户名*

## 用途

`sessreg`命令管理`xdm`会话的 utmp/wtmp 条目。更详细的说明请参阅在线手册页。

## 选项

- **-a** 将此会话添加到 utmp/wtmp。-a 或 -d 必须设置其中一个。
- **-d** 从 utmp/wtmp 中删除此会话。-a 或 -d 必须设置其中一个。
- **-l 线路名** 设置条目的线路名。对于终端会话，这是终端设备文件名的最终路径名部分（如 ttyd0）。对于 X 会话，它应该是提供给用户会话的本地显示名称（通常为 :0）。
- **-u utmp-文件** 设置备用的 utmp 文件。
- **-w wtmp-文件** 设置备用的 wtmp 文件。
- **-x Xservers-文件** 将*槽位号*设置为 ttys 文件的行数加上在此文件中找到*线路名*的索引。
- **-t ttys-文件** 设置一个备用文件，供**-x**使用，以统计主机上的终端会话数量。

## 相关命令

`xdm`

## `setfdprm`

## 设置软盘参数

`setfdprm` *选项* *设备*

## 用途

`setfdprm`命令设置软盘参数。它可用于清除旧参数集或启用诊断消息。不带选项时，`setfdprm`从 `/etc/fdprm` 文件中加载新的参数集到设备文件。

## 选项

- **-c** *设备名* 清除`设备名`的参数集。
- **-n** *设备名* 禁用自动配置`设备名`的格式检测。
- **-p** *设备名* 为`设备名`永久加载新的参数集。
- **-y** *设备名* 启用自动配置`设备名`的格式检测。

## `setterm`

`setterm` *选项*

## 用途



`setterm`命令通过一长串选项设置终端属性。这些选项可以在在线手册页中找到。

## superformat

## 格式化软盘

`superformat` *选项*

## 用途

`superformat`命令格式化软盘。hippocampus

它适用于 Linux 格式化，但同时也会调用`mformat`在格式化后的软盘上建立 MS-DOS 文件系统。（安装 MS-DOS 文件系统是可选的。）

## 选项

以下列出了基本选项。此外，还有一些高级选项，您可能永远不会用到；更多信息请参阅在线手册页。

- **-2** 格式化可由`2m`程序读取的大容量磁盘。
- **-B** 使用`mbadblocks`程序验证磁盘。
- **-d** *驱动器* 指定要格式化的驱动器；默认为第一个软盘驱动器（`/dev/fd0`）。
- **--dd** 格式化双倍密度磁盘。
- **-D** *驱动器* 指定供`mformat`使用的 DOS 驱动器盘符，`a:`或`b:`。
- **-f** 跳过验证。
- **-H** *磁头数* 指定磁头数量（默认为 2）。
- **--hd** 格式化高密度磁盘。
- **-l** 不使用 2m 格式。
- **--no2m** 不使用 2m 格式。
- **-s** *扇区数* 设置扇区数量。这里的"扇区"不是指物理扇区数，而是指等效的Tail | Explanation
- **-t** *磁道数* 设置磁道数量。默认值为 40 或 80，取决于驱动器类型或密度。
- **-v** *详细级别* 设置数值详细级别：1 为每个格式化磁道打印一个点，2 为每个格式化磁道打印一个变化的符号，3 为每个格式化磁道打印一行完整信息，列出磁头和磁道，而 6 和 9 则打印调试信息。
- **-V** 在进程结束时而非每个磁道格式化后验证格式化结果。

## 相关命令

- `fdrawcmd`
- `floppycontrol`
- `getfdprm`
- `mtools`
- `xdfcopy`

## xdfcopy

处理 Xdf 磁盘

`xdfcopy` *选项 source target*

## 用途

`xdfcopy`命令用于复制和格式化 Xdf 软盘，这是一种 OS/2 操作系统使用的格式。

## 选项

- **-D**_dosdrive_ — 指定要格式化的 DOS 驱动器盘符。此选项有大量适用条件；详情请查看在线手册页。
- **-n** — 在将映像复制到磁盘之前不对磁盘进行格式化。

## 相关命令

- `mtools`
- `floppycontrol`
- `performat`

## MTOOLS

`Mtools`系列命令用于处理 MS-DOS 文件和软盘上的目录。这使你可以用 Linux 与 MS-DOS 格式化的软盘配合使用。

## mattrib

更改 MS-DOS 属性

`mattrib` *选项* *msdos文件*

## 用途

`mattrib`命令更改存储在软驱上的 MS-DOS 文件的文件属性。添加属性标志使用`+`，移除属性标志使用`-`。

## 属性

- **a** — 存档位。
- **h** — 隐藏位。
- **r** — 只读位。
- **s** — 系统位。

## mbadblocks

MS-DOS 坏块

`mbadblocks` *驱动器*

## 用途

`mbadblocks`扫描指定的`驱动器`（一个 MS-DOS 软盘）中的坏块。它将坏块标记为不可读。

## mcd

更改 MS-DOS 目录

`mcd 目录`

## 用途

`mcd`命令更改 MS-DOS 软盘上的当前目录。未指定目录时，返回当前设备和目录。

## 相关命令

- `mdir`

## mcopy

复制 MS-DOS 文件

```
mcopy 选项 sourcefile targetfile
mcopy 选项 sourcefile(s) targetdirectory
```

## 用途

`mcopy`命令将 MS-DOS 文件复制到 Linux 系统或从 Linux 系统复制，通常使用软驱。它可以用来将文件复制到目标文件，也可以将多个文件复制到指定目录。使用 MS-DOS 软盘时，需要在文件或目录名前面加上`A:`。

## 选项

| 选项 | 说明 |
|--------|-------------|
| `t` | 执行文本文件传输，将回车/换行符转换为仅换行符。 |
| `m` | 保留文件修改时间。 |
| `n` | 覆盖现有文件时不发出警告。 |
| `v` | 以详细模式工作。 |

## 相关命令

- `mread`
- `mwrite`

## mdel

删除 MS-DOS 文件

`mdel *选项* msdos文件`

## 用途

`mdel`命令删除一个 MS-DOS 文件，通常在软驱上。

## 选项

- **-v**
  以详细模式工作，删除文件时将文件名打印到屏幕上。

## mformat

格式化 MS-DOS 软盘

`mformat 选项 驱动器`

## 用途

`mformat`命令为低级 Linux 格式化的磁盘添加 MS-DOS 文件系统。此格式化包括引导扇区、FAT 和根目录。

## 选项

- `1` - 覆盖使用 2m 格式，即使当前磁盘几何结构是 2m 几何结构。
- `2` - 以 2m 格式工作——磁道 0、磁头 0 上的扇区数。
- `h` - 指定磁头数（面数）。
- `H` - 指定隐藏扇区数。
- `l` - 设置可选卷标。
- `M` - 设置软件扇区大小。
- `n` - 设置序列号。
- `t` - 指定磁道数（非柱面数）。
- `s` - 指定每磁道扇区数。
- `S` - 指定大小代码。
- `X` - 将磁盘格式化为 Xdf 磁盘，供 OS/2 使用。

## 相关命令

- `mlabel`
- `mrd`

## mrd

删除 MS-DOS 目录树

`mrd 选项 msdos目录`

## 用途

`mrd`命令删除 MS-DOS 目录树，以及其中的所有文件和子目录。此操作发生在软驱上的 MS-DOS 文件系统中。

## 选项

- **-v** — 以详细模式工作，列出每个被删除的文件和目录。

## mdir

显示 MS-DOS 目录

```
mdir *选项* *msdos目录*
```

## 用途

`mdir`命令显示 MS-DOS 目录的内容，通常在软驱上。

## 选项

| 选项 | 说明 |
|--------|-------------|
| `a` | 列出隐藏文件。 |
| `w` | 以宽格式输出，不显示文件大小或创建日期。 |

## mlabel

创建标签

`mlabel *选项* *驱动器* *新标签*`

## 用途

`mlabel`命令在软驱上创建 MS-DOS 卷标。无选项时，显示当前标签。如果未设置`c`或`s`选项，会提示你输入新标签；此时，如果你不输入新标签而直接按`回车键`，现有标签将被删除。

## 相关命令

- `mformat`

## mmd

创建子目录

`mmd 选项 目录`

## 用途

`mmd`命令在软驱上创建 MS-DOS 子目录。如果目录已存在，将报错。

## 选项

- `v`
  以详细模式工作，返回创建时的目录名称。

## 相关命令

- `mrd`

## mmount

挂载 MS-DOS 磁盘

`mmount *驱动器* *挂载参数*`

## 用途

`mmount`命令挂载 MS-DOS 磁盘。它读取 MS-DOS 磁盘的引导扇区，配置驱动器几何结构，并将其挂载，将`mount-args`传递给`mount`。

## 相关命令

- `mount`

## mmove

移动/重命名 MS-DOS 文件

```
mmove 选项 sourcefile targetfile
mmove 选项 sourcefile(s) targetdirectory
```

## 用途

`mmove`命令移动或重命名现有的 MS-DOS 文件或子目录。

## 选项

| 选项 | 说明 |
|--------|-------------|
| `v` | 以详细模式工作，如果新名称无效则显示新文件名。 |

## 相关命令

- `mren`

## Linux 命令，按组分类

## mren

重命名 MS-DOS 文件

`mren *选项 sourcefile targetfile*`

## 用途

`mren`命令重命名软驱上的 MS-DOS 文件。

## 选项

| 选项 | 说明 |
|--------|-------------|
| `v` | 以详细模式工作，如果新名称无效则显示新文件名。 |

## 相关命令

- `mmove`

## mrd

删除 MS-DOS 目录

`mrd *选项* *msdos目录*`

## 用途

`mrd`命令从软盘上删除 MS-DOS 目录。

## 选项

- **v** — 以详细模式工作，删除时显示目录名称。

## 相关命令

- `mdeltree`
- `mmd`

## mread

复制 MS-DOS 文件

`mread *选项* *msdos文件* *unix文件*`

## 用途

`mread`命令将 MS-DOS 文件复制到 Linux 系统。这是一个已废弃的命令，但某些旧脚本可能仍支持它。推荐使用的命令是`mcopy`。

## 相关命令

- `mcopy`
- `mtype`

## mtest

## 用途

`mtest`命令读取 mtools 配置文件并将累积配置打印到标准输出，这些输出随后可用作配置文件。你可以用它来将旧配置文件转换为新配置文件。

## mtype

显示 MS-DOS 文件

`mtype 选项 msdos文件`

## 用途

`mtype`命令显示 MS-DOS 文件。

## 选项

- `s`: 从显示的文件中去除高位比特。
- `t`: 假定文件为文本文件。

## 相关命令

- `mcd`
- `mread`

## mwrite

将 Linux 文件写入 MS-DOS

```
mwrite unixfile dosfile
```

## 用途

`mwrite`命令将 Linux 文件复制到软盘上的 MS-DOS 文件系统。该文件被视为已废弃，仅用于与旧 shell 脚本保持向后兼容；请改用`mcopy`。

## 相关命令

```
mcopy
```

## Linux Shell

你无法在运行 Linux 时不运行`shell`，这是一种与你交互的工具，提供了一种直接与操作系统核心通信的方式。你认为由操作系统执行的操作，大多数情况下实际上是由 shell 执行的：它接收你的命令，解释它们，并将它们传递给操作系统核心；它提供自己的一套命令（其中一些在第 5 章中作为操作系统命令介绍过；这其实是一种没有区别的区别）；它还提供自己的脚本机制。

大多数 Linux 发行版至少包含六到七种 shell，但人们通常坚持使用自由软件基金会默认的 Bourne Again Shell（`bash`），这是在大多数 UNIX 系统上流行的 Bourne shell 的克隆版本。此外，许多用户切换到 C shell（`csh`）或精简版的 C shell，`tcsh`。（安装 Linux 发行版时，通常会询问你希望在系统上安装哪些 shell。有大量可用的 Linux shell，包括`ash`和`zsh`。）要查看系统上安装了哪些 shell，请使用以下命令行：

```
$ chsh -l
/bin/sh
/bin/bash
/bin/csh
/bin/tcsh
...
```

要更改登录 shell，请使用以下命令行之一：

```
$ chsh -s /bin/csh
```

或

```
$ exec /bin/csh
```

我们不会花太多时间讨论 shell；关于 shell 的在线文档已经足够多，市面上关于 shell 及其用法的书籍也*汗牛充栋*。相反，我们会花一些时间来介绍 shell 变量。

## Shell 变量

这些变量由 shell 设置。它们在各种情况下使用，但通常用于 shell 脚本中。

| 变量 | 说明 |
| --- | --- |
| IFS | 内部字段分隔符，用于扩展后的单词分割，以及使用`read`内置命令时将行分割为单词。默认值是**空格-制表符-换行符**。 |
| PATH | 命令的搜索路径。这是一个以冒号分隔的目录列表，shell 在其中查找命令。默认路径取决于系统，由安装 bash 的管理员设置。 |
| HOME | 当前用户的主目录；`cd`命令的默认参数。 |
| CDPATH | `cd`命令的搜索路径。这是一个以冒号分隔的目录列表，shell 在其中查找`cd`命令指定的目标目录。 |
| ENV | 如果在 bash 执行 shell 脚本时设置此参数，其值将被解释为包含初始化 shell 命令的文件名，如`.bashrc`。ENV 的值在被解释为路径名之前，会经历参数扩展、命令替换和算术扩展。PATH 不用于搜索生成的路径名。 |
| MAIL | 如果将此参数设置为某个文件名，且 MAILPATH 变量未设置，`bash`会通知用户指定文件中有新邮件到达。 |
| MAILCHECK | 指定`bash`检查邮件的频率（以秒为单位）。默认值为 60 秒。当需要检查邮件时，shell 会在提示之前进行检查。如果未设置此变量，shell 将禁用邮件检查。 |
| MAILPATH | 要检查邮件的路径名列表，以冒号分隔。可以通过使用`?`将路径名与消息分开来指定要打印的消息。 |
| MAIL_WARNING | 如果设置，并且`bash`正在检查邮件的文件自上次检查以来已被访问，则会打印消息 *The mail in mailfile has been read*。 |
| PS1 | 设置主提示符。默认值是`bash\$`。 |
| PS2 | 设置辅助提示符，许多应用程序用它提供输入。默认值是`>`。 |
| PS3 | 设置`select`命令的提示符。 |
| PS4 | 设置执行跟踪中命令前使用的字符值。默认值是`+`。 |
| HISTSIZE | 设置在命令历史中记住的命令数量。默认值为 500。 |
| HISTFILE | 设置保存命令历史的文件名。默认值为`~/.bash_history`。 |
| HISTFILESIZE | 设置历史文件中的最大行数。默认值为 500。 |
| IGNOREEOF | 控制 shell 在收到作为唯一输入的 EOF 字符时的行为。如果设置，该值是在`bash`退出之前，作为输入行上的第一个字符键入的连续 EOF 字符的数量。如果该变量存在但没有数值，或没有值，则默认值为 10。如果不存在，EOF 表示 shell 的输入结束。这仅对交互式 shell 有效。 |
| TMOUT | 如果设置为大于零的值，该值被解释为发出主提示后等待输入的秒数。如果在该秒数内输入未到达，bash 将终止。 |
| FIGNORE | 执行文件名补全时要忽略的后缀列表，以冒号分隔。后缀与 FIGNORE 中某项匹配的文件名将从匹配的文件名列表中排除。示例值为`.o:~`。 |

## 窗口管理器

*窗口管理器*控制以 XFree86 形式启动 X Window 系统时的界面。它控制窗口的形状和滚动条的形式、分配内存，并监管应用程序。

大多数 Linux 发行版（包括 Slackware Linux）的默认窗口管理器是`fvwm`。（不，`fvwm`不代表任何含义。）基本上，`fvwm`与 Motif 窗口管理器（稍后我们会简要介绍）有一些共同之处，但差异足够大，不会引起版权律师的兴趣。Slackware Linux 中还可以找到其他窗口管理器：基于 Sun Microsystems 的 OpenWindows 界面的 Open Look 窗口管理器（`olwm`）；标签窗口管理器（`twm`）；以及模拟 Windows 95 界面的`fvwm-95`窗口管理器。`fvwm`、`olwm`和`twm`窗口管理器分别如图 7.1、7.2 和 7.3 所示。

![](img/387edf6ffeb560ccc38b30f5b14659a9_564_0.png)

*图 7.1 fvwm 窗口管理器。*

![](img/387edf6ffeb560ccc38b30f5b14659a9_564_1.png)

*图 7.2 olwm 窗口管理器。*

![](img/387edf6ffeb560ccc38b30f5b14659a9_564_2.png)

*图 7.3 twm 窗口管理器。*

从这些图中可以看出，每个窗口管理器在屏幕上呈现窗口的方式不同。所有窗口管理器在屏幕左上角都有菜单，都有显示应用程序描述标题栏，都有滚动条，角落都有用于调整窗口大小的手柄。然而，除此之外，还有一些外观和感觉上的差异，这些差异不一定影响应用程序，但可能会影响你与应用程序的交互方式。

除了上述窗口管理器之外，大多数 Linux 发行版——包括 Slackware Linux——还有*虚拟窗口管理器*，它呈现的桌面大于平均屏幕尺寸。这些虚拟屏幕往往会占用大量 RAM，因为屏幕上看不见的部分仍然会被绘制到显存中。（这不适用于`fvwm`，它使用不同的方法存储桌面上看不见的部分。）

这些免费窗口管理器与商业领域不同，在商业领域中，Motif 窗口管理器（`mwm`）占据主导地位，无论是直接的还是通过其在通用桌面环境（CDE）中的实现。由于`mwm`是商业软件，因此无法通过 Linux 或 XFree86 获得，尽管许多第三方供应商（如 Metro Link）提供收费的 Motif 库和`mwm`。

使用窗口管理器有一个缺点：它们往往会消耗大量内存。X Window 系统是为内存充足的工作站设计的，效率可以更高。你应该计划至少分配 4MB 的 RAM 用于使用 X Window 系统。这种情况在使用 XFree86 时会有所改善，它使用共享库来减少内存使用。此外，`fvwm`是目前最节省内存的窗口管理器，使用的内存约为`twm`的一半。

我们不会花很多时间解释窗口管理器；了解窗口管理器的最佳方法是实际操作它。如果你需要更多信息，请查看参考书目中的其他 Linux 文本列表。

### 窗口操作

查看图 7.1 时，你可以看到窗口可以分解为几个基本元素。窗口具有三维阴影效果。窗口两侧有边条，角落的元素称为*框架*，用于调整窗口大小。此外，窗口顶部有一个标题栏，显示窗口标题。



要移动窗口，将光标放在标题栏或侧边条上，按下第一个鼠标按钮，然后将窗口拖动到新位置。

标题栏旁边有两个按钮。左侧按钮会调用一个菜单，可用于移动、调整大小、最小化、最大化或关闭窗口。右侧按钮将窗口变为图标。

## 命令行选项

以下是`fvwm`支持的命令行选项：

| 选项 | 结果 |
| --- | --- |
| `-d *displayname*` | 使用`*displayname*`而非存储在环境变量`$DISPLAY`中的默认`displayname`。 |
| `-debug` | 在调试（同步）模式下工作，有助于生成准确的错误消息。 |
| `-f *config_file*` | 使用`*config_file*`而非默认的`.fvwmrc`配置文件。 |
| `-s` | 在多屏幕显示中将`fvwm`限制为一个屏幕，如`-d`选项所设置。 |
| `-no-m4FP` | 覆盖`m4`对`.fvwmrc`配置文件的预处理。 |
| `-m4-prefix` | 为所有内置命令添加`m4_`前缀。 |
| `-m4opt *option*` | 将`*option*`传递给`m4`。 |

## 配置文件

启动`fvwm`时，它会在你的主目录中查找名为`.fvwmrc`的初始化文件。该文件包含按键和按钮绑定、配色方案以及启动应用程序和选项的信息。

当你查看一个文件时，你会看到一长串选项。其中一些以`#`开头，这会将该行注释掉并使其失效。以下选项可以在`.fvwmrc`文件中设置：

| 选项 | 用途 |
| :--- | :--- |
| `StdForeColor *颜色名称*` | 将菜单和未选中窗口的前景色设置为`*颜色名称*`。单色显示器默认此颜色为黑色。 |
| `StdBackColor *颜色名称*` | 将菜单和未选中窗口的背景色设置为`*颜色名称*`。单色显示器默认此颜色为白色。 |
| `StickyForeColor *颜色名称*` | 将未选中窗口的粘性标题的前景色设置为`*颜色名称*`。单色显示器默认此颜色为黑色。 |
| `StickyBackColor *颜色名称*` | 将未选中窗口的粘性窗口的背景色设置为`*颜色名称*`。单色显示器默认此颜色为白色。 |
| `HiForeColor *颜色名称*` | 设置选中窗口的标题颜色。单色显示器默认此颜色为黑色。 |
| `HiBackColor *颜色名称*` | 设置选中窗口的背景色。单色显示器默认此颜色为白色。 |
| `MenuForeColor *颜色名称*` | 设置菜单前景色。 |
| `MenuBackColor *颜色名称*` | 设置菜单背景色。 |
| `MenuStippleColor *颜色名称*` | 设置菜单上不可用（灰色显示）选项的颜色。 |
| `PagerBackColor *颜色名称*` | 设置分页器背景色。 |
| `PagerForeColor *颜色名称*` | 设置分页器前景色。 |
| `Font *字体名称*` | 设置菜单、调整大小指示器和图标标签的字体。 |
| `WindowFont *字体名称*` | 设置窗口标题栏的字体。 |
| `PagerFont *字体名称*` | 设置窗口图标名称的字体。 |
| `IconFont *字体名称*` | 设置图标名称标签的字体。 |

## 配置文件（续）

| 选项 | 用途 |
|--------|---------|
| `NoTitle *窗口名称*` | 为指定的`*窗口名称*`隐藏标题。 |
| `NoBorder *窗口名称*` | 为指定的`*窗口名称*`隐藏装饰性边框。 |
| `Sticky *窗口名称*` | 将`*窗口名称*`设置为"粘性的"，即在虚拟桌面变化时视口不会移动。 |
| `StaysOnTop *窗口名称*` | 让`*窗口名称*`永远不会被其他窗口遮挡。 |
| `StartsOnDesk *窗口名称* *桌面编号*` | 让`*窗口名称*`放置在指定的`*桌面编号*`上，如果你使用多个桌面的话。 |
| `CirculateSkip *窗口名称*` | 当调用`circulate-up`或`circulate-down`功能时跳过`*窗口名称*`。 |
| `CirculateSkipIcons` | 在运行`circulate`和`warp`操作时跳过图标。 |
| `WindowListSkip *窗口名称*` | 从窗口列表中省略`*窗口名称*`。 |
| `Style *窗口名称* *选项*` | 可与前面的命令一起使用，将所有制设置放在一个综合命令中。 |
| `CenterOnCirculate` | 在`circulating`时将目标窗口居中。 |
| `DeskTopSize *水平x垂直*` | 以物理屏幕尺寸的倍数设置虚拟桌面大小。 |
| `DeskTopScale *比例*` | 相对于屏幕设置虚拟桌面比例。 |
| `BoundaryWidth *宽度*` | 设置装饰窗口的边界宽度；默认为 6。 |
| `NoBoundaryWidth *宽度*` | 设置无边界窗口的装饰宽度。默认为 1。 |
| `XORvalue *数字*` | 设置在进行橡皮筋式窗口移动或调整大小时用于位异或的值。 |
| `EdgeScroll *水平* *垂直*` | 设置当光标到达页面边缘时要滚动的页面百分比。 |

## 配置文件（续）

| 选项 | 用途 |
| --- | --- |
| `PagingDefault *值*` | 确定是否启用分页（`*值*`为 1 时）或禁用分页（`*值*`为 0 时）。 |
| `EdgeResistance *滚动 移动*` | 设置鼠标移动到屏幕边缘时（由`*滚动*`值设置）和窗口移动到屏幕边缘时（由`*移动*`值设置）的参数。 |
| `OpaqueMove *百分比*` | 设置使用不透明窗口移动的最大窗口大小。 |
| `ClickToFocus` | 设置键盘输入聚焦活动窗口，直到明确选择另一个窗口。 |
| `SloppyFocus` | 使用鼠标设置焦点。 |
| `MWMBorders` | 使用`mwm`风格的窗口边框。 |
| `MWMButtons` | 使用`mwm`风格的按钮配置。 |
| `MWMMenus` | 使用`mwm`风格的菜单。 |
| `MWMDecorHints` | 使用`mwm`风格的窗口提示。 |
| `MWMFunctionHints` | 使用`mwm`风格的窗口功能。 |
| `MWMHintOverride` | 使用`mwm`风格的图标化提示覆盖。 |
| `Lenience` | 让`fvwm`忽略 ICCCM 约定。 |
| `OpaqueResize` | 使用窗口边框而非轮廓来调整窗口大小。 |
| `DontMoveOff` | 不允许窗口移出桌面。 |
| `AutoRaise *延迟*` | 设置窗口的自动提升，并指定窗口获得输入焦点与自动提升之间的延迟（以毫秒为单位）。 |
| `Pager *X Y*` | 设置窗口跨桌面移动的分页样式，窗口在`*X*`和`*Y*`处出现。 |

## 配置文件（续）

| 选项 | 用途 |
|---|---|
| `Mouse *按钮 上下文 修饰符 功能*` | 设置多个鼠标参数：`*button*`为按钮编号，`*context*`为绑定上下文（`R`表示根窗口，`W`表示应用程序窗口，`T`表示标题栏，`S`表示窗口栏，`F`表示窗口框架，`I`表示图标窗口，或`0`到`9`表示标题栏按钮），`*modifier*`为键修饰符（`N`表示无修饰符，`C`表示`Ctrl`键，`S`表示`Shift`键，`M`表示`Meta`键，或`A`表示任意），`*function*`为内置功能。 |
| `Key *键名* *上下文 修饰符 功能*` | 将键绑定到功能：`*key*`为键，`*context*`为绑定上下文（`R`表示根窗口，`W`表示应用程序窗口，`T`表示标题栏，`S`表示窗口栏，`F`表示窗口框架，`I`表示图标窗口，或`0`到`9`表示标题栏按钮），`*modifier*`为键修饰符（`N`表示无修饰符，`C`表示`Ctrl`键，`S`表示`Shift`键，`M`表示`Meta`键，或`A`表示任意），`*function*`为内置功能。 |
| `IconBox *左 上 右 下*` | 设置屏幕上放置图标的区域。 |
| `StubbornIconPlacement` | 让`IconBox`不被窗口覆盖。 |
| `StubbornIcons` | 让窗口将图标展开到其原始位置。 |
| `SuppressIcons` | 隐藏图标。 |
| `StickyIcons` | 无论你移动虚拟屏幕到哪里，都将图标放在同一位置。 |
| `IconPath *路径*` | 设置黑白图标位置的文件路径。 |
| `PixmapPath *路径*` | 设置彩色图标位置的文件路径。 |
| `Icon *窗口名称* *位图文件*` | 为特定的`*窗口名称*`设置位图。 |

## 配置文件（续）

| 选项 | 用途 |
| --- | --- |
| `DecorateTransients` | 装饰临时窗口。 |
| `RandomPlacement` | 随机放置窗口，而不是等待用户放置。 |
| `SmartPlacement` | 将窗口放在空旷区域，而不是等待用户放置。 |
| `StubbornPlacement` | 将窗口放在除图标上方的任何位置，而不是等待用户放置。 |
| `NoPPosition` | 添加新窗口时忽略`*PPosition*`字段。 |
| `ClickTime *延迟*` | 设置按钮按下和按钮释放之间的延迟（以毫秒为单位）。 |
| `ModulePath` | 设置模块的路径。 |
| `Module *模块名称*` | 设置启动时要加载的模块。选项有：`GoodStuff`（推荐）、`FvwmPager`、`FvwmBanner`、`FvwmWinList`、`FvwmClean`、`FvwmIdent`、`FvwmSave`、`FvwmScroll`、`FvwmDebug`和`FvwmSound`。这些模块有自己的手册页。 |
| `Cursor *光标编号 光标类型*` | 更改光标样式。 |
| `ButtonStyle *按钮编号 宽度x高度*` | 设置标题栏按钮中的形状。 |
| `AppsBackingStore` | 为应用程序设置后备存储，这违反 ICCCM 的图片。 |
| `SaveUnders` | 设置保存下方区域。 |
| `BackingStore` | 为窗口管理器设置后备存储，这违反 ICCCM 的指南。 |
| `Popup *弹出菜单名称*` | 设置一个弹出菜单，稍后绑定到鼠标按钮或键。 |
| `Function *功能名称*` | 设置一个功能，稍后绑定到鼠标按钮或键。 |

## Fvwm 变量

`fvwm`窗口管理器支持以下变量：

| 变量 | 用途 |
|---|---|
| `SERVERHOST` | 设置运行 X 服务器的机器名称。 |
| `CLIENTHOST` | 设置运行客户端的机器。 |
| `HOSTNAME` | 设置运行客户端的规范主机名。 |
| `USER` | 设置运行该程序的用户名称。 |
| `HOME` | 指定用户的主目录。 |
| `VERSION` | 返回 X 主协议版本。这对某些 X 应用程序可能很重要。 |
| `REVISION` | 返回 X 次要协议修订号。这对某些 X 应用程序可能很重要。 |
| `VENDOR` | 返回 X 服务器的供应商。通常不太重要。 |
| `RELEASE` | 返回 X 服务器的发布版本号，例如 X11R6 对应的 6。 |
| `WIDTH` | 设置显示器的宽度（以像素为单位）。 |
| `HEIGHT` | 设置显示器的高度（以像素为单位）。 |
| `X_RESOLUTION` | 返回显示器的 X 分辨率（以每米像素数为单位）。 |
| `Y_RESOLUTION` | 返回显示器的 Y 分辨率（以每米像素数为单位）。 |
| `PLANES` | 返回默认根窗口支持的位平面数。 |
| `BITS_PER_RGB` | 返回 RGB 颜色中的有效位数。 |
| `TWM_TYPE` | 返回`twm`类型；它始终是`fvwm`。 |
| `CLASS` | 返回视觉类别（`StaticGray`、`GrayScale`、`StaticColor`、`PseudoColor`、`TrueColor`、`DirectColor`或`NonStandard`之一）。 |
| `COLOR` | 返回`yes`表示彩色，`no`表示灰度。 |
| `FVWM_VERSION` | 返回`fvwm`版本。 |
| `OPTIONS` | 列出编译进窗口管理器的选项。 |
| `FVWMDIR` | 设置模块的路径。 |

## 参考文献

本书是 MIS:Press 出版的 Slackware Linux 系列书籍之一。该 Slackware 系列涵盖了多种情况下的 Slackware Linux。书目如下：

- **Linux 配置与安装**，第二版，Patrick Volkerding、Kevin Reichard 和 Eric F. Johnson 著，$39.95。两张 CD-ROM。523 页。ISBN 1-55828-492-3。第三版（ISBN 1-55828-566-0）计划于 1997 年出版。
- **Linux 编程**，Patrick Volkerding、Eric Foster-Johnson 和 Kevin Reichard 著，$39.95。CD-ROM。374 页。ISBN 1-55828-507-5。
- **Linux 数据库**，Fred Butzen 和 Dorothy Forbes 著，$39.95。CD-ROM。456 页。ISBN 1-55828-491-5。
- **Linux 互联网服务器**，Kevin Reichard 著，$39.95。CD-ROM。512 页。ISBN 1-55828-545-8。

你可以在`http://www.mispress.com/linux/booklist.htm`获取每本书的更多信息。

## 索引

- `ansi2knr`, 422
- `answer`, 358
- `appres`, 46
- `apropos`, 47
- `ar`, 423-424
- `arch`, 48
- `as`, 425-426
- `at`, 482-483
- `atq`, 484
- `atrm`, 485
- `atobm`, 49
- `audiocompose`, 359
- `audiosend`, 360
- `banner`, 50
- `basename`, 218
- `bash`, 51, 555-558
- `batch`, 486
- `bc`, 52-54
- `bdftopcf`, 55
- `biff`, 361
- `bison`, 427
- `bitmap`, 56
- `bmtoa`, 58
- `bpe`, 276
- `cal`, 59
- `cat`, 277-278
- `cc`, 428
- `cd`, 219
- `checknews`, 362
- `chin`, 363
- `chgrp`, 220
- `chmod`, 221-224
- `chown`, 225
- `chroot`, 226
- `chsh`, 60
- `cksum`, 61
- `clear`, 62
- `cmp`, 279
- `colcrt`, 63
- `colrm`, 280
- `column`, 281
- `comm`, 282
- `cp`, 227-228
- `cpio`, 487-489
- `cpp`, 429
- `cron`, 490
- `csh`, 64
- `csplit`, 283
- `ctlinnd`, 491
- `ctags`, 430
- `cut`, 284
- `date`, 65-66
- `df`, 492
- `diff`, 285-286
- `diff3`, 287-288
- `dir`, 229-230
- `diskd`, 493
- `diskseek`, 494
- `dnshostname`, 456
- `dnsquery`, 457
- `du`, 495
- `dumpkeys`, 67
- `echo`, 68
- `egrep`, 289-290
- `elm`, 364
- `elvis`, 291
- `emacs`, 292
- `env`, 69
- `etags`, 431
- `expand`, 293
- `fastmail`, 365
- `faucet`, 458
- `fdformat`, 499
- `fdisk`, 496
- `fdmount`, 497
- `fdtablemd`, 498
- `fgrep`, 294
- `file`, 231
- `find`, 232-234
- `finger`, 366
- `flex`, 432
- `fmt`, 295
- `fold`, 296
- `formail`, 367
- `free`, 500
- `frm`, 368
- `fsinfo`, 70
- `fstobdfs`, 71
- `fstobdf`, 72
- `ftp`, 369-373
- `ftpcount`, 374
- `ftpd`, 501
- `ftpwho`, 502
- `funzip`, 235
- `fuser`, 459
- `fvwm`, 559-567
- `fvwm-95`, 559
- `g77`, 433
- `gawk`, 434
- `gcc`, 435
- `getfilename`, 236
- `getkeycodes`, 73
- `getlist`, 375
- `getpeername`, 460
- `ghostview`, 297
- `gprof`, 436-437



以下是按字母顺序排列的Linux命令索引，包含命令名称及对应的页码或功能说明：

- `grep`, 298-299
- `grodvi`, 300
- `groff`, 301-302
- `grolj4`, 303
- `grops`, 304
- `grotty`, 305
- `gunzip`, 237
- `gzexe`, 238
- `gzip`, 239
- `head`, 306
- `hos`, 461
- `host`, 462-463
- `hostname`, 464
- `httpd`, 503
- `id` 支持流式视频和音频功能。
- `id`, 74
- `imake`, 438
- `imapd`, 504
- `inetd`, 505
- `inews`, 506
- `info`, 75
- `ininews`, 507
- `innd`, 509
- `ispell`, 307-308
- `join`, 309
- `kdb_mode`, 76
- `kill`, 77
- `killall`, 78
- `less`, 310-317
- `lilo`, 510-511
- `listres`, 79
- `ln`, 240-241
- `locate`, 242
- `locatedb`, 243
- `lockfile`, 244
- `login`, 80
- `logname`, 81
- `look`, 318
- `lpq`, 319
- `lpr`, 320-321
- `lprm`, 322
- `ls`, 245-246
- `lynx`, 376-379
- `mail`, 380-385
- `make`, 439-440
- `makedepend`, 441-442
- `makefloppies`, 512
- `makestrs`, 443
- `makewhatis`, 82
- `man`, 83-84
- `manpath`, 85
- `mattrib`, 536
- `mbadblocks`, 537
- `mc`, 247
- `mcd`, 538
- `mcookie`, 86
- `mcopy`, 539
- `md5sum`, 513
- `mdel`, 540
- `mdir`, 543
- `messages`, 386
- `metamail`, 387
- `metasend`, 388-389
- `mformat`, 541
- `mmencode`, 390
- `minicom`, 87
- `mkdir`, 248
- `mkdier`, 249
- `mkfifo`, 250
- `mkfontdir`, 251
- `mkmanifest`, 252
- `mknod`, 253
- `mlabel`, 544
- `mmd`, 545
- `mmencode`, 391
- `mmount`, 546
- `mmove`, 547
- `more`, 323-324
- `mount`, 514
- `mren`, 548
- `mrd`, 542
- `mread`, 550
- `msgfmt`, 444
- `mt`, 515
- `mtest`, 551
- `mtype`, 552
- `mv`, 254
- `mwrite`, 553
- `nice`, 88
- `newgrp`, 255
- `nohup`, 89
- `nroff`, 325
- `obcopy`, 445
- `oclock`, 90
- `oltvm`, 559
- `passwd`, 91
- `paste`, 326
- `若赞`, 92
- `perl`, 446
- `pico`, 327
- `pidof`, 93
- `pine`, 392
- `ping`, 465
- `pkgtool`, 516
- `pname`, 94
- `Pnews`, 393
- `popclient`, 394-395
- `postnews`, 396
- `pr`, 328-329
- `printenv`, 95
- `printf`, 330
- `printmail`, 397
- `procmail`, 398-399
- `ps`, 96
- `psbb`, 331
- `pwd`, 256
- `quota`, 517
- `rb`, 97
- `rcp`, 466
- `rdjpegcom`, 98
- `readmsg`, 400
- `readprofile`, 518
- `reconfig`, 99
- `ref`, 447
- `refer`, 332
- `relaynews`, 519
- `renice`, 100
- `reset`, 101
- `resize`, 102
- `rev`, 333
- `rexecd`, 520
- `richtext`, 401
- `rlogin`, 467
- `rm`, 257
- `rmail`, 402
- `rmdir`, 258
- `rmmod`, 521
- `Rmail`, 403
- `rpcgen`, 448-449
- `rsh`, 468
- `rstart`, 489
- `rstartd`, 522
- `runscript`, 103
- `ruptime`, 104
- `rusers`, 470
- `rwall`, 471
- `rwho`, 472
- `rx`, 105
- `rxvt`, 106-107
- `rz`, 108
- `sb`, 109
- `script`, 110
- `sdiff`, 334-335
- `sed`, 336
- `selection`, 337
- `sendmail`, 523
- `sessreg`, 524
- `setfdprm`, 525
- `setterm`, 526
- `seyon`, 111
- `shar`, 112-113
- `shells`, 555-558
- `shelltool`, 114
- `showaudio`, 404
- `showexternal`, 405
- `showfont`, 115-116
- `shownonascii`, 406
- `showpartial`, 407
- `showpicture`, 408
- `showrgb`, 117
- `shrinkfile`, 259
- `size`, 260
- `skill`, 118
- `sleep`, 119
- `splogin`, 473
- `smproxy`, 121
- `snice`, 120
- `sockdown`, 474
- `soelim`, 338
- `sort`, 339
- `split`, 340
- `splitmail`, 409
- `splitvt`, 122
- `sq`, 261
- `startx`, 123
- `strace`, 124-125
- `strings`, 126
- `strings-gnu`, 127
- `strip`, 450
- `stty`, 128-129
- `su`, 130
- `sum`, 262
- `sunst`, 131
- `superformat`, 527-528
- `SuperProbe`, 529-530
- `sx`, 132
- `sxpm`, 133
- `systat`, 134
- `sz`, 135
- `updatedb`, 267
- `uptime`, 142
- `users`, 143
- `uucp`, 477
- `uudecode`, 412
- `uuencode`, 413
- `uustat`, 414
- `uux`, 415
- `vi`, 347
- `viewres`, 144
- `vim`, 348
- `vrfy`, 416
- `w`, 145
- `wc`, 349
- `whatis`, 146
- `who`, 147
- `whoami`, 148
- `window managers`, 559-567
- `wish`, 149
- `wnewvmail`, 417
- `write`, 478
- `x11perf`, 150-151
- `x11perfcomp`, 152
- `xargs`, 153-154
- `xauth`, 155
- `xbiff`, 418
- `xcalc`, 156
- `xclipboard`, 157
- `xclock`, 158
- `xcositmap`, 159
- `xcmsdb`, 160
- `xconsole`, 161
- `xcpustate`, 162
- `xcutsel`, 163
- `xdfcopy`, 533
- `xdm`, 164-165
- `xdpyinfo`, 166
- `xedit`, 350
- `xev`, 167
- `xeyes`, 168
- `xf86config`, 169
- `xfd`, 170
- `xfilemanager`, 268
- `xfm`, 269
- `xfontsel`, 171
- `xfracint`, 172
- `xfs`, 173
- `xgc`, 174
- `xgettext`, 451
- `xhost`, 175
- `xieperf`, 176-177
- `xinit`, 178
- `xkill`, 179
- `xload`, 180
- `xlock`, 181-182
- `xlogo`, 183
- `xlsatoms`, 184
- `xlsclients`, 185
- `xlsfonts`, 186
- `xmag`, 187
- `xman`, 188
- `xmessage`, 189
- `xmh`, 419
- `xmkmf`, 452
- `xmodmap`, 190
- `xon`, 191
- `xpaint`, 192
- `xpmroot`, 193
- `xprop`, 194
- `xrdb`, 195-196
- `xrefresh`, 197
- `xset`, 198-199
- `xsetroot`, 200
- `xsm`, 201
- `xsmclient`, 202
- `xspread`, 203
- `xstdcmap`, 204
- `xterm`, 205-206
- `xv`, 207
- `xvidtune`, 208
- `xvpictoppm`, 209
- `xwd`, 210-211
- `xwinfo`, 212-213
- `xwud`, 214
- `xxgdb`, 453
- `yacc`, 454
- `yes`, 215
- `ytalk`, 479
- `zcat`, 270
- `zcmp`, 351
- `zdiff`, 352
- `zegrep`, 353
- `zfgrep`, 354
- `zforce`, 271
- `zgrep`, 355
- `zmore`, 356
- `znew`, 272
- `zoo`, 273
- `tac`, 341
- `tail`, 342
- `talk`, 475
- `tee`, 136
- `telnet`, 476
- `telnetd`, 531
- `test`, 263
- `tftp`, 410
- `tload`, 137
- `top`, 138
- `tr`, 343
- `trn`, 411
- `troff`, 344
- `true`, 139
- `twm`, 559
- `ul`, 140
- `umount`, 532
- `unexpand`, 345
- `uniq`, 346
- `unshar`, 141
- `unsq`, 264
- `unzip`, 265
- `unzipsfx`, 266

## LINUX JOURNAL

每月*Linux Journal*都会为您带来最完整的信息，介绍这个强大的系统能为您和您的工作做些什么。*Linux Journal*告诉您需要了解的知识，让Linux为您所用。

- 了解Linux技术的最新趋势
- 对Linux开发人员及其他知名人士的专访
- 掌握Linux软件的最新发布动态
- 通过阅读我们的教程避免常见错误
- Linux相关产品评测
- 关于GNU、编程、技术支持等的专栏

有疑问？

致电 (206) 782-7733 或 (888) 66 LINUX

传真：+1 (206) 782-7191

网址：http://www.ssc.com/

如需获取SSC其他出版物的免费目录，请发送电子邮件至 `info@ssc.com`

*只需寄回此页，我将自动获得一期免费样刊*

## MIS:Press

### Linux 深入浅出

*我还希望订阅。* 今天就订阅，我将节省超过50%的

**1年**
- $22 美国
- $27(USD) 加拿大
- $32(USD) 其他国家

**2年**
- $39 美国
- $49(USD) 加拿大
- $54(USD) 其他国家

请预留6-8周处理时间

| 姓名 | | |
|-------|-------|-------|
| 公司 | | |
| 地址 | | |
| 城市 | 州 | 邮政编码 |
| 国家 | 电话 | |
| 传真 | 电子邮件 | |
| 信用卡号 | | 到期日 |

☐ Visa ☐ MasterCard ☐ American Express ☐ 随函附支票

签名

**邮寄地址：LINUX JOURNAL • 邮政信箱 85867 • 西雅图, WA • 98145-1867 • 美国**

## MIS:Press Slackware系列的其他图书：

- LINUX：配置与安装，第二版
- Linux编程
- Linux数据库
- Linux互联网服务器

作为领先的UNIX变体，Linux已成为最受欢迎的PC操作系统之一。这本涵盖所有Linux命令的指南，精简了浩如烟海的Linux文档，帮助您在需要时找到所需的Linux命令。

这本结构清晰、必不可少的参考书面向Linux用户、程序员和系统管理员，提供了从多种角度访问所有Linux命令的快捷方式。如果您知道想要哪种类型的命令，可以按类型浏览命令列表。如果您知道某个DOS命令并想要对应的Linux等效命令，可以查阅Linux/DOS交叉索引。如果您对命令的功能有大致了解但不知道具体名称，可以查阅*以通俗语言表述的*命令列表。此外，对于那些极少数您确切知道需要使用哪个Linux命令的时刻，还提供了按字母顺序排列的交叉索引。而且，尽管本书属于*MIS:Press Slackware系列*，但它涵盖了所有主流Linux发行版，包括Slackware Linux、Red Hat Linux和Caldera。

**PATRICK VOLKERDING**和**KEVIN REICHARD**是*MIS:Press Slackware系列*的丛书编辑，这是一套涵盖Slackware Linux（最受欢迎的Linux发行版）各个方面的雄心勃勃的图书系列。Volkerding是Slackware Linux的创始人，而Reichard是一位UNIX专家和资深的UNIX/Linux图书作者。他们共同撰写了（与Eric Pharmacy Eric Foster-Johnson合著）*Linux：配置与安装*（现已出版至第二版）和*Linux编程*。

MIS Press, Inc., Henry Holt and Company, Inc.的子公司, 115 West 18th Street, New York, New York 10011

http://www.mispress.com

- 揭秘文件系统
- 通用命令
- 系统管理命令
- 互联网命令
- 与DOS等效命令交叉索引的Linux命令
- Shell命令与变量
- 窗口管理器，包括`fvwm`和`twm`

封面插图 © Paul & Lindamarie Ambrose, FPG

封面设计 Gary Szczeina

US $19.95

CAN $27.95

90000

ISBN 1-55828-542-3

9 781558 285422

| 级别 |
|-------|
| 全部 |
| 操作系统 |
| Linux |
