
```
$ style linuxpr.txt
readability grades:

  Kincaid: 12.1

  ARI: 13.4

  Coleman-Liau: 13.6

  Flesch Index: 48.5

  Fog Index: 15.0

  WSTP Index: 2.9

  Wheeler-Smith Index: 33.7 = school year 8

  Lix: 52.4 = school year 10

  SMOG-Grading: 13.1

sentence info:

  10651 characters

  2136 words, average length 4.99 characters = 1.60 syllables

  94 sentences, average length 22.7 words

  41% (39) short sentences (at most 18 words)

  14% (14) long sentences (at least 33 words)

  31 paragraphs, average length 3.0 sentences

  3 questions, 15 imperatives

  longest sent 53 wds at sent 91; shortest sent 1 wds at sent 42
```

在此示例中，报告表明文本非常容易阅读，但可能可以改进或面向更高级别的受众。`style` 命令还有其他命令行选项，你可以使用它们来生成关于文本的自定义报告。为了理解任何报告，你绝对需要阅读其手册页以获取更多关于可读性指数和公式的信息。

### 打印简介

Linux 有多种可用的行打印机打印后台处理系统。虽然你可以设置 KDE 和 GNOME 以支持拖放打印，但你还应了解如何从命令行使用 Linux 打印系统。缺乏这一知识，你可能会发现在控制台和纯文本会话中打印很困难，或者很难使用许多 X 客户端进行打印。

许多 Linux 发行版使用源自 BSD UNIX 的打印后台处理，它使用名为 `lpd` 的守护进程来响应打印请求生成打印过程。正如你在第 3 章“安装后配置”中学到的，`lpd` 守护进程使用系统打印机功能数据库中的定义，包括打印机名称、位置、纸张大小、过滤等。

本节将向你介绍使用 BSD 行打印机打印后台处理系统启动、停止和管理打印任务的基础知识。

### 其他打印系统

Linux 还有其他可用的打印系统，主要在其他计算机平台上，如基于 Intel 的 PC。Patrick Powell 的 LPng 打印服务是一个启用了安全的网络打印系统，包含在许多流行的发行版中。另一个打印系统是通用 UNIX 打印系统，或称为 CUPS。与 Linux 的其他所有打印系统不同，CUPS 的优势在于它是根据 GNU GPL 分发的，并且可用于多种发行版，包括 PPC Linux。

### 启动打印任务

打印任务在命令行上使用 `lpr` 命令启动。`lpr` 命令有许多命令行选项，但最简单形式可用于将文档发送到默认系统打印机，如下所示：

```
$ lpr mydocument.txt
```

在此示例中，按下回车键后，文档将被传入你的个人打印目录（位于 `/var/spool/lpd` 目录下）。`lpq` 命令，它检查目录中的新任务，然后将生成打印过程并将文档发送到打印机。你还可以使用 `lpr -P` 选项，后跟打印机名称，将任务发送到特定打印机，如下所示：

```
$ lpr -P remote1p mydocument.txt
```

在此示例中，打印任务将被发送到名为 remote1p 的打印机（在这种情况下，是一台连接到网络上另一台计算机的打印机）。`lpr` 命令也可以使用输入重定向。使用前面的 `style` 命令为例，你可以像这样将可读性报告直接发送到特定打印机：

```
$ style linuxpr.txt | lpr -P mp400
```

在此示例中，报告将在名为 mp400 的打印机上打印。

### 停止打印任务

如果您启动了一个打印任务，但随后决定要停止它，请使用 `lprm` 命令，后跟打印任务的编号。为了知道任务编号，请使用 `lpq` 命令列出当前的打印任务队列。例如，如果您启动了一个打印任务，`lpq` 命令可能会报告如下队列列表：

```
$ lpq
lp is ready and printing
Rank Owner Job Files Total Size
active bhall 4 linuxpr.txt 13558 bytes
```

您可以通过使用 `lprm` 命令并后跟“Job”（任务）编号来终止打印任务，如下所示：

```
$ lprm 4
dfA004\cube dequeued
cfA004\cube dequeued
```

按下回车键后，已删除的暂存文件的名称将会打印出来。

### 管理打印队列

在多用户环境中，可能有多个用户和打印任务争夺打印机的注意力，并排在打印队列中。作为 `root` 操作员，您可以使用 `lpc` 和 `lprm` 命令管理此队列以及系统的打印机。由于 `root` 是 `superuser`，root 操作员可以移除任何人拥有的待处理打印任务（普通用户只能移除自己拥有的打印任务）。

虽然通常在独立工作站上不需要，但 `lpc` 命令可以被 `root` 用户在网络化打印机环境中使用，以禁用或启用任何系统打印机，重新排列打印队列，启动和停止打印，以及保留和释放打印任务。更多信息请参阅 `lpc` 手册页。

#### 资源

- http://www7doc.sco.com/SHL_autorate/CTOC-Manipulating_text_with_sed.html. 关于使用 `sed` 命令的简易介绍。
- http://www.vim.org. 免费 `vim` 编辑器的主页，与 `vi` 不同，它不受版权阻碍，而是根据 GNU GPL (*General Public License*，通用公共许可证) 发布。
- http://www.vim.org/maes.html. 下载 Mac OS 版本 `vim` 的网站。
- http://space.mit.edu/~davis/jed/. `jed` 编辑器的主页。您将从此网站找到最新版本和文档。
- http://www.uni-ulm.de/uni/intgruppen/memosys/symbol07.htm. 软件行业如何削弱生产力提升的有趣历史。
- http://www.avalanche.nl/thomer/vi/vi.html. `vi` 爱好者主页。所有关于 `vi` 的地方！
- http://www.nano-editor.org/. `nano` 编辑器的主页，它是 `pine` 电子邮件客户端附带的 `pico` 编辑器的真正免费克隆版。
- http://mac-emacs.sourceforge.net/index.html. Mac OS 版本 `emacs` 的主页。
- http://glimmer.sourceforge.net/. GNOME 最复杂文本编辑器的网页。
- http://www.abiword.org/. 开源文字处理器 AbiWord 的主页。
- http://nedit.org/. 老牌的 `nedit` 编辑器的主页。源代码和二进制版本可以在此处下载。
- http://aspell.sourceforge.net/. 免费 `aspell` 拼写检查器的主页，根据其开发者的说法，旨在“最终取代 `Ispell`”。
- http://www.kdstevens.com/~stevens/ispell-page.html. `ispell` 的 `emacs` 接口作者的主页。
- http://fmq-www.cs.ucla.edu/geoff/ispell.html. Ispell 的主页，这是一个国际性、交互式拼写检查器，拥有 24 种不同语言的词典。
- http://www.gnu.org/software/diction/diction.html. GNU 版本的遗留 `style` 和 `diction` 命令的下载站点。
- http://www.astart.com/lprng/LPRng.html. LPRng 打印机服务软件的 Web 主页。
- http://www.cups.org. CUPS (*COMMON UNIX Printing System*，通用 UNIX 打印系统) 的主页。
- http://www.vistaource.com/. 用于 Linux（包括 PPC Linux）的商业 Applix 办公套件的源代码。

### 第 7 章：X11 和窗口管理器

- 什么是 X11？
- 什么是窗口管理器？
- Linux 的窗口管理器和桌面环境
- 启动 X11 会话
- 停止 X11 会话
- 配置选择器
