

# 理解 Unix • 第 2 章

……指的是遵循特定设计哲学的操作系统。而“Linux”是一个极其流行的免费的类 Unix 操作系统，它根据 Unix 的哲学设计，但实际上它并不是一个真正符合 Unix 哲学的标准实现。*nix* 的历史非常丰富、错综复杂且混乱，以至于我们无法呈现一个全面的面貌。了解“System V”*nix 的血统与源自伯克利软件发行版（BSD）血统之间的区别，对于理解为什么命令似乎永远没有相同的开关和选项（-ef 与 ps -aux）非常有帮助。如果你想查看所有 *nix 变种的族树，可以花几分钟时间浏览 www.levenez.com/unix/ 上的图表，只需寻找 Linux 在何处。

虽然这些区别让你感到头疼，但好消息是，这些术语对你的日常工作并不重要，尽管熟悉历史无疑会很有帮助。为了处理所有这些细节，我们将遵循其他作者的做法，避免使用笨拙的商标名称，也避免使用“Unix-like”这种连字符组合，而在指代 Linux 或符合标准的操作系统时，我们将这一堆 Unix 及其朋友统称为“*nix”。

另一个好消息是，只要具备一些基本的 Linux 技能，你就能开启一个更广泛的领域，那里有许多专利和免费的 *nix 实现在等着你。了解 Linux 及其术语将帮助你在在使用以下流行的 *nix 操作系统时感到如如家。其中有些你可能听说过，即使没有亲身接触过。按照可能遇到概率的粗略顺序排列，你可能在工作中的某时候看到的 *nix 操作系统有：

- Linux，我们最好的朋友，提供色彩丰富的发行版。
- Apple OS X，很少有人知道在所有这些精美界面背后运行着一个基于 FreeBSD 的完全符合标准的 Unix 系统。尝试“实用工具”文件夹中的终端（Terminal）应用程序并拥抱 Unix 的美好。
- Solaris，来自太阳微系统公司。
- HP-UX，来自惠尔罗普。
- AIX，IBM 的 Unix 变体。
- Tru64，现在通过 Compaq DEC 归惠尔罗普所有，其早期生命被称为 Digital Unix。
- FreeBSD、OpenBSD，源自伯克利遗产的免费开源 *nix。

# 第 2 章 • 理解 Unix

而且，从历史角度来看，这些遗产仍然活跃良好：

- UNIX System V ("System 5")，又名 SVR5，来自 AT&T，后来成为 SCO UnixWare。
- 伯克利软件发行版 (BSD) UNIX，在许多变体中仍然活跃。

在 *nix shell 提示符下度过一段时光后，窗口将变得不再陌生：你一眼就了！我很兴地报告，这些 *nix 朋友在设计上都非常精英，远非粗俗。在你介绍 *nix 的过程中，我们也会尽力防止你说出太多的脏话。

# Linux 发行版

就像讨论拥有众多参与者的 *nix 一样，即使 Linux 本身也有丰富的选择，无论好坏。Linux 有多种不同的版本，体现了使用该操作系统的人们的多样性，他们利用其开源特性进行调整和创建，以创建一个以自己的方式解决问题的 Linux。

一些常见的 Linux 发行版包括：Ubuntu（我们本文的选择）、Red Hat Enterprise (RHEL)、Fedora、SUSE Linux Enterprise (Novell)、OpenSUSE、Gentoo、Debian、Mandriva 以及数百种其他版本。如果你想关注免费开源发行版，当你第一次访问 http://distrowatch.com/ 时可能会惊讶得掉下巴。

所有发行版都实现了 Linux 内核，在命令行提示符下你将在所有版本中体验到相似的内容。发行版之间的不同之处在于默认安装中包含哪些软件、如何将软件包添加到系统、默认使用什么窗口管理器用户界面（GUI）（如果有的话）以及关于稳定更新的发布哲学。

对于取证工作来说，意识到有不同的版本很有用，而且程序、日志和配置文件的位置在不同的 Linux 发行版之间也不同。“完成某件事不止一种方法”的格言在 Linux 中仍然适用。

# 获取一个 Linux！

是时候让手指离开键盘了！不需要被所有的选择所击垮——只需获取一个 Ubuntu Linux 副本。Ubuntu 之广受欢迎，是因为它是最容易安装的，而且它的安装 CD 还是所谓的“活动光盘”（Live CD）——你甚至不需要安装就可以尝试。

![](img/fd8e85097b37559dbc07dc22fd8cb1fe_20_0.png)

整个操作系统可以从 CD 驱动器启动，你完全不需要担心硬盘上的 Windows 安装受到任何影响。

所以，浏览 http://ubuntu.com/ 并顺着直觉找到下载部分，我们就可以拿到 Linux 了。在此时，http://www.ubuntu.com/getubuntu/downloadmirrors 提供了全球范围内下载点的列表，可以免费获取最新的 Ubuntu Linux 发行版。如果你带宽受限，只要愿意等待长达 10 周下载，Ubuntu 会为你寄送免费的 CD 或 DVD。不过，下载软件很容易的。查看 Ubuntu 页面 2.1 显示了你将在哪里选择默认设置。

**Ubuntu 页面 - 默认设置**

![](img/fd8e85097b37559dbc07dc22fd8cb1fe_21_0.png)

# 第 2 章 • 理解 Unix

下载将以 .iso 文件的形式出现。ISO 文件是磁盘镜像。不要犯尝试刻录 .iso 文件本身这种初级错误。如果你电脑自带了 OEM CD 刻录程序，那么事情就很简单了。例如，IBM/联想 Thinkpad 就带了类似的程序。这就是 Nero 可能会称呼的。见图 2.2。

# 从 LiveCD 启动 Ubuntu Linux

一旦你将 ISO 镜像正确刻录到 CD-ROM 上，将其插入电脑的 CD-ROM 驱动器并重启。

如果你最终回到了 Windows，很可能是你的基本输入输出系统（BIOS）将硬盘的优先级设置为高于 CD-ROM。快速调整 BIOS 设置即可修复该问题。当你启动电脑时，通常在启动时的第一个闪屏处按下 F2 或 DEL 或启动时提到的其他按键，即可进入 BIOS 配置。在 Boot（启动）选项下，你可以修改计算机搜索可启动媒体的顺序。阅读屏幕上的说明如何更改顺序（对于 Phoenix BIOS，使用右方向键进入 Boot 菜单，向下移动到 CD-ROM 设备并按下 Shift 和 1）。这是一个让 Ubuntu LiveCD 在硬盘操作系统之前启动的启动顺序示例（见图 2.3）。

| Main | Advanced | Security | Power | Boot | Exit |
| --- | --- | --- | --- | --- | --- |
| | Removable Devices | | | | Item Specific Help |
| | CD-ROM Drive | | | | 查看或配置设备的按键：<Enter> 展开或折叠带有 + 或 - 的设备 <Ctrl+Enter> 展开所有 <Shift+> 启用或禁用设备 <> 和 > 移动设备向上或向下 <n> 在硬盘或可移动磁盘之间移动设备 <> 删除未安装的设备。 |
| | Hard Drive | | | | |
| Network boot from AMD Am7C970A | | | | |
| F1 Help | T Select Item -/+ Change Values F9 Setup Defaults | | | |
| Esc Exit | <-- Select Menu Enter > Sub-Menu F10 Save and Exit | | |

**2.3 你需要更改启动顺序以便 CD-ROM 在硬盘之前启动**

![](img/fd8e85097b37559dbc07dc22fd8cb1fe_22_0.png)

如果你没有 OEM 刻录软件，不要担心。只需从 http://isorecorder.alexfeinman.com/isceptor.htm 获取 ISO Recorder Power 的副本即可。

