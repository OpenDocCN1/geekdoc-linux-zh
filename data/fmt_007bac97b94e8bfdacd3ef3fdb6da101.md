
一旦同事们开始把你看作本地系统管理员，你就很难从这个角色中脱身。这未必是坏事，但我们认识好几个为了摆脱而换工作的人。由于许多管理任务是无形的，你可能还会发现自己被期望既当全职管理员，又当全职工程师、作家或分析师。

不情愿的管理员通常倾向于摆出恶劣态度、提供糟糕服务来搪塞请求。这种做法通常会适得其反；它既让你形象变差，又会制造额外的问题。

相反，不妨详细记录你花在系统管理上的时间。你的目标应该是将工作量控制在可管理的水平，并积累证据，以便在请求卸下管理职责时使用。在大多数组织中，你需要向管理层游说六个月到一年才能找到接替者，所以要提前规划。

另一方面，你可能会发现自己其实喜欢系统管理，并且更愿意做这项工作而不是“正经工作”。就业前景依然不错。不幸的是，你的政治问题可能会进一步加剧。欲知更多乐趣，请参阅第 32 章 `管理、政策` 和 `政治`。

10. 这种倾向在西蒙·特拉瓦利亚的《来自地狱的混蛋操作员》系列故事中得到了既充满爱意又残忍的记录；档案见 `bofh.nkt.net`。（可在 `BOFH` 下查找。）

## 1.14 推荐阅读

ROBBINS, ARNOLD. UNIX in a Nutshell (4th Edition). Sebastopol, CA: O’Reilly Media, 2008.

SIEVER, ELLEN, AARON WEBER, AND STEPHEN FIGGINS. Linux in a Nutshell (5th Edition). Sebastopol, CA: O’Reilly Media, 2006.

GANCARZ, MIKE. Linux and the Unix Philosophy. Boston: Digital Press, 2003.

SALUS, PETER H. The Daemon, the GNU & the Penguin: How Free and Open Software is Changing the World. Reed Media Services, 2008.

这部由 UNIX 最著名的历史学家撰写的关于开源运动的迷人历史也可在 `groklaw.com` 上以知识共享许可获得。该书本身的 URL 非常长；请在 `groklaw.com` 上查找当前链接，或尝试此压缩等价链接：`tinyurl.com/deu7`。

RAYMOND, ERIC S. The Cathedral & The Bazaar: Musings on Linux and Open Source by an Accidental Revolutionary. Sebastopol, CA: O’Reilly Media, 2001.

### 系统管理

LIMONCELLI, THOMAS A., CHRISTINA J. HOGAN, AND STRATA R. CHALUP. The Practice of System and Network Administration (Second Edition). Reading, MA: Addison-Wesley, 2008.

这是一本不错的书籍，对系统管理中的策略和程序方面有特别强的覆盖。作者在 `everythingsysadmin.com` 维护一个系统管理博客。

FRISCH, ÆLEEN. Essential System Administration (3rd Edition). Sebastopol, CA: O’Reilly Media, 2002.

这是一本经典的全方位 UNIX 系统管理指南，可惜有些过时了。我们希望新版本正在制作中！

### 核心工具

CHRISTIANSEN, TOM, AND NATHAN TORKINGTON. *Perl Cookbook (2nd Edition).* Sebastopol, CA: O’Reilly Media, 2003.

BLANK-EDELMAN, DAVID N. *Automating System Administration with Perl (2nd Edition).* Sebastopol, CA: O’Reilly Media, 2009.

PILGRIM, MARK. *Dive Into Python.* Berkeley, CA: Apress, 2004.

这本书也可以在 `diveintopython.org` 上免费在网上获取。

FLANAGAN, DAVID, AND YUKIHIRO MATSUMOTO. *The Ruby Programming Language.* Sebastopol, CA: O’Reilly Media, 2008.

这本书乐观地副标题为 *Everything You Need to Know,* 不幸的是有点枯燥。然而，它涵盖了 Ruby 1.9 版本，并包含了只有语言设计者才能真正知道的丰富细节。最适合那些已经具备 Perl 或 Python 工作知识的人。

## 1.15 练习

- 1. **E1.1** 你会使用什么命令来阅读关于终端驱动程序 `tty` 的资料（不是 `tty` 命令）？如果你想阅读保存在 `/usr/local/share/man` 中的本地 `tty` 手册页，该怎么办？

- 2. **E1.2** 你站点的 `man` 命令的行为是否受系统范围配置文件控制？如果想将本地资料存储在 `/doc/man` 中，你会向此文件添加什么行？要在 `/doc/man` 中使其成为手册页层级中的完整成员，需要使用什么目录结构？

- 3. **E1.3** Linux 内核开发的当前状态是什么？热点问题是什么？关键人物是谁？项目是如何管理的？

- 4. **E1.4** 研究几种 UNIX 和 Linux 系统，并为以下每个应用推荐一个操作系统。解释你的选择。

  - a) 在家庭办公室工作的单用户

  - b) 大学计算机科学实验室

  - c) 企业 Web 服务器

  - d) 运行运输公司数据库的服务器集群

- 5. **E1.5** 假设你发现 Apache `httpd` 的某个功能在 Ubuntu 上似乎不能按文档所述工作。

  - a) 在报告错误之前你应该做什么？

  - b) 如果你决定错误是真实的，应该通知谁以及如何通知？

  - c) 为了使错误报告有用，必须包含哪些信息？

- 6. **E1.6** Linux 已在生产环境中取得了巨大进展。UNIX 注定要灭亡吗？为什么或为什么不？

# 2 脚本编写与 Shell

![](img/14d78e3cecac4581d37024baf1e94cca_77_0.png)

优秀的系统管理员会编写脚本。脚本标准化并自动化管理任务的执行，释放管理员的时间用于更重要和更有趣的任务。从某种意义上说，脚本也是一种低成本的文档，因为它们充当完成特定任务所需步骤的权威大纲。

就复杂性而言，管理脚本从封装几个静态命令的简单脚本到管理整个站点主机配置和行政数据的重大软件项目不等。在本书中，我们主要关注系统管理员通常遇到的较小、日常的脚本项目，因此我们不会过多讨论大型项目所需支持功能（例如，错误跟踪和设计评审）。

管理脚本应强调程序员效率和代码清晰度，而非计算效率。这并不是粗心的借口，而只是认识到脚本运行在半秒还是两秒之间很少重要。即使是定期从 `cron` 运行的脚本，优化也可能具有惊人地低的投资回报率。

很长一段时间以来，管理脚本的标准语言是由 shell 定义的。大多数系统的默认 shell 是 `bash`（“Bourne-again” shell），

但 `sh`（原始的 Bourne shell）和 `ksh`（Korn shell）在少数 UNIX 系统上仍在使用。Shell 脚本通常用于轻量级任务，例如自动化一系列命令或组合多个过滤器来处理数据。

Shell 总是可用，因此 shell 脚本相对可移植，除了它们调用的命令之外几乎没有依赖关系。无论你是否选择 shell，shell 可能会选择你：大多数环境都包含大量现有的 `sh` 脚本，而这些脚本经常需要由管理员阅读、理解和调整。

对于更复杂的脚本，建议转向真正的编程语言，例如 Perl 或 Python，两者都非常适合管理工作。这些语言相对于 shell 包含了几十年语言设计的进步，而它们强大的文本处理功能（对管理员来说不可或缺）强大到 `sh` 只能哭泣并羞愧地退缩。

Perl 和 Python 的主要缺点是其环境设置起来可能有点挑剔，尤其是在你开始使用具有编译组件的第三方库时。Shell 通过没有模块结构和没有第三方库来规避这个问题。

本章快速介绍了 `bash`、Perl 和 Python 作为脚本语言，以及正则表达式作为通用技术。

## 2.1 SHELL 基础

在我们开始 shell 脚本编写之前，让我们回顾一下 shell 的一些基本特性和语法。本节中的内容适用于 `sh` 系中的所有主要 shell（包括 `bash` 和 `ksh`，但不包括 `csh` 或 `tcsh`），无论你使用的是哪个确切平台。尝试一下你不熟悉的形式，并进行实验！

### 命令编辑

我们见过太多人用方向键编辑命令行。你在文本编辑器里会这样做吗？
