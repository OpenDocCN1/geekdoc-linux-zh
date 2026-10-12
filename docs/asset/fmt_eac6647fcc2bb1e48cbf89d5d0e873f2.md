
操作系统是负责调度任务、分配存储以及处理外设（如打印机、键盘和鼠标）接口的底层软件。操作系统分为两个部分：内核和系统程序。内核将内存、磁盘和 CPU 时间分配给所有运行程序。系统程序包括设备驱动、库、实用工具、壳、配置文件、应用程序、服务器和文档。它们执行高级任务，通常在客户端/服务器关系中工作。

![](img/f67bdb23d5a8cb457175c8ce91ec3c2_40_0)

# 第一章 欢迎来到 LINUX

Linux 内核由芬兰大学生 Lin Torvals 开发，他利用互联网让其他人免费获得源代码。Torvalds 在 1991 年 9 月发布了 Linux 0.01 版本。

这款操作系统的诞生是许多人的共同努力结果。世界各程序员迅速扩展了内核并开发了其他工具，在现有 BSD UNIX 和 System UNIX (SVR) 功能的基础上增加了功能。Linux 的名称是 Linux 和 UNIX 的结合。

Linux 操作系统是许多人通过互联网合作的产物，是一种免费操作系统。换句话说，源代码是免费的。你可以自由地研究、分发和修改它。正如 GNU 自由软件定义（附录 D）所示

自由软件关乎自由，而不是价格。要理解这个概念，你应该把“free”理解为自由，而不是免费

## UBUNTU LINUX

- 发行版 各种组织将 Linux 内核和系统程序封装成 Linux 发行版（访问 `distrowatch.com` 获取更多信息）。流行的发行版包括 SUSE、Fedora、Ubuntu、Red Hat 和 Mandriva。发行版之间最大的区别通常是用户如何安装操作系统。其他区别包括默认安装了哪些图形工具以及使用哪些工具来更新系统。

Ubuntu 基于 Debian，侧重于易用性、可访问性和国际化。尽管 Ubuntu 最初针对桌面

UNIX 与 GNU–LINUX 的历史 3

用户，最近的发布越来越强调软件市场。通过每六个月计划发布一次新版本，Ubuntu 提供了尖端软件。

Ubuntu 系统使用 `GNOME` 桌面管理器（`www.gnome.org`），并包含了 `OpenOffice` 生产力工具套、`Firefox` 浏览器、`Pidgin`（原 `Gaim`）IM 客户端以及各种工具和游戏。为了保持系统软件更新，Ubuntu 使用 Debian 的 `deb` 包格式和各种基于 `APT` 的工具。

Ubuntu 的治理结构遵循仁慈独裁模型：Mark Shuttleworth 是自封的终身仁慈独裁者（`SADFL`）。该结构包括技术委员会、Ubuntu 社区委员会、本地社区（`LoCos`）和宇宙之主（`MOTU`）。有关 Ubuntu 的更多信息，请访问 `www.ubuntu.com/about/faq`。

### UNIX 与 GNU–LINUX 的历史

本节介绍了 UNIX 与 Linux 以及 GNU 与 Linux 之间关系的背景。

### UNIX 的历史：UNIX

UNIX 系统是由研究人员开发的，他们需要一组现代计算工具来帮助他们的项目。该系统让一组共同工作项目的人能够在保持其他信息私密的同时，选择数据和程序。

大学和学院通过“四年效应”在促进 UNIX 操作系统的普及方面起着重要作用。当 UNIX 操作系统在 1975 年广泛可用时，贝尔实验室以名义价格提供给教育机构。学校反过来将其推荐给他们的计算机科学专业，确保计算机科学专业的学生熟悉它。由于 UNIX 是一项先进的开发系统，学生们熟悉了复杂的编程环境。这些学生毕业后进入工业界，他们期望在类似的先进环境中工作。随着越来越多的人在商业世界步步晋升，UNIX 操作系统进入了工业领域。

除了向学生介绍 UNIX 操作系统外，加州大学伯伯克利分校的计算机系统研究小组（CSRG）对其进行了重大的补充和更改。事实上，它进行了如此许多受欢迎的更改，以至于该系统的一个版本被称为 UNIX 系统的伯克利软件发行版（`BSD`）（或简称为伯克利 UNIX）。另一个主要版本是 UNIX System V（`SVR4`），它源自由 AT&T 和 UNIX 系统实验室开发和维护的版本。

### 迈向 1983

Richard Stallman（`www.stallman.org`）宣布¹了创建一个操作系统（包括内核和系统程序）的 GNU 项目，并提交了《GNU 宣言》，²其开头如下：

GNU 代表“GNU's Not UNIX”（GNU 不是 UNIX），我正在编写的完整兼容 UNIX 的软件系统的名称，我可以免费送给每个可以使用它的人。

几年后，当 Stallman 意识到这句话引起了混乱时，他在前面的句子添加了一个脚注：

> 这里的措辞很粗率。本意是没有人需要为使用 GNU 系统支付“许可”费用。这些词并没有说明这一点，人们经常将其解释为 GNU 的副本应该以低价或免费分发。我们后来在宣言中提到了公司提供营利分发服务的可能性。随后，我仔细学习了“free”在自由意义上和“free”在价格意义上。自由软件是指用户有自由分发和更改的软件。某些用户可以免费获得副本，其他用户如果资金支持改进软件，那就好了。重要的是，每个拥有副本的人都有自由与他人协作使用它。

在宣言中，在简要解释了项目以及到目前为止取得的成就后，Stallman 继续写道：

#### 为什么我必须编写 GNU

我认为黄金法则要求，如果我喜欢一个程序，我必须把它分享给其他喜欢它的人。软件销售商想要分化并征服用户，让每个用户同意不与他人分享。我拒绝以这种方式与其他用户建立团结。出于良知，我不签署保密协议或软件许可协议。多年来，我在人工智能实验室工作以抵抗这种倾向和非人性行为，但最终他们太过分。我不能留在一个违背我的意愿为我做这些事的机构。

为了让我继续不失体地使用计算机，我决定整合一套足够的自由软件，以便我能够与任何非自由软件和谐相处。

1. `www.gnu.org/gnu/initial-announcement.html`

2. `www.gnu.org/gnu/manifesto.html`

UNIX 与 GNU–LINUX 的历史 5

已从人工智能实验室辞职，以拒绝麻省理工学院任何阻止我赠送 GNU 的法律理由。

#### 下一个场景，1991

GNU 项目已朝着目标顺利进展。除了内核外，GNU 操作系统的大部分已已完成。Richard Stallman 后来写道：

> 到 90 年代初，我们已经组成了内核之外的整个系统（我们还在开发一个内核，即 GNU Hurd，它运行在 Mach 之上）。开发这个内核比我们预想的困难得多，我们仍在努力工作。

> ……许多人认为，一旦 Linux Torvalds 完成了内核的编写，他的朋友就开始寻找其他自由软件，而且由于某种特殊原因，构建类 UNIX 系统所需的所有东西已经准备就绪了。

他们发现的是偶然——那就是 GNU 系统。可用的自由软件加起来是一个完整的系统，因为 GNU 项目自 1984 年以来一直致力于创建一个系统。《GNU 宣言》设定了开发自由类 UNIX 系统的目标，即 GNU。当 Linux 完成时，系统几乎完成了。今天，Linux 运行在 FreeBSD（`www.freebsd.org`）、NetBSD（`www.netbsd.org`）和 Darwin（`developer.apple.com`）之上。

#### 代码是自由的

自由软件传统可以溯到 UNIX 以名义价格发布的时代，这促进了它的成功。随着 UNIX 的商业化，这一传统最终消失了，使其变得不可用。

3. `www.gnu.org/gnu/initial-announcement.html`

4. `www.gnu.org/gnu/manifesto.html`

5. `www.gnu.org/software/hurd.html`

6. `www.gnu.org/philosophy/linux.html`

7. `www.gnu.org/software/hurd-and-linux.html`

第 1 章欢迎来到 Linux

### 第 1 章欢迎来到 Linux

两个教授创建了 MINIX：Doug Comer 创建了 GNU，Andrew Tanenbaum 创建了 MINIX。Lin Torvalds 创建了 Linux 以应对 MINIX 的缺陷。每当在代码简单性和效率之间选择时，Tanenbaum 选择了简单性（为了教学）。Linux 走向了相反的方向。你可以从互联网免费获取 Linux。你也可以通过购买 Linux 的商业软件包（称为发行版），包括安装、软件和支持来支持自由基金会（`www.fsf.org`）。

#### ！

Linux 的两个词是 Have Fun！这些词出现在提示和文档中。UNIX——现在是 Linux——文化充满了幽默。例如，GNU 替换了名为 `less` 的 Unix 页面工具为改进后的 `less`。查看 PostScript 文档的工具名为 `ghostscript`，以及编辑器 `vi` 的几种替代品之一。虽然带有 Intel 处理器的机器外部有“Intel Inside”标志，但某些 Linux 机器展示着“Linux Inside”标志。Torvalds 本人也被看到穿着一件带有“Linux Inside”标志的 T 恤。

#### LINUX 有什么好处？
