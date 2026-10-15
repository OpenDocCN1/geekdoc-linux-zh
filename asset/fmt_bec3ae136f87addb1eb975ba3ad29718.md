
## 运行 Slackware Linux

老牌 Linux 用户会告诉你，他们使用的第一个 Linux 发行版很可能就是 Slackware。Slackware 是目前仍在活跃开发的最古老的 Linux 发行版。尽管它没有华丽的图形化安装程序或专用工具，但 Slackware 仍然拥有一批忠实的粉丝，并且是获取安全稳定基础 Linux 系统的良好方法。

本章将探索 Slackware 发行版，讨论它的优缺点，并介绍使用它的人。它还将解释如何安装 Slackware。

## 关于 DVD

本书随附的 DVD 包含了来自 Slackware 13 三张光盘安装包的部分软件。你可以从 Slackware Store (`http://store.slackware.com`) 购买完整的 Slackware 13，或者从 Slackware 网站 (`www.slackware.com/getslack`) 查找下载 DVD 或其他 CD 镜像的地址。

## 接触 Slackware

虽然全图形化安装和 GUI 管理工具可以使安装和配置 Slackware 变得简单，但这些工具会带来一些开销。它们还隐藏了 Linux 配置过程中的某些细节。

### 第五部分：选择和安装不同的 Linux 发行版

询问 Slackware 的信徒关于 Slackware 的世界，他们可能会背诵他们的格言，“4S 原则”：稳定（Stable）、可靠（Solid）、简单（Simple）和合理（Sensible）。通过保持简单，Slackware 提供了以下优势：

- 更好的理解——因为你在 Slackware 中使用命令和配置文件，你能够更多地学习 Linux 内部的工作原理。大多数图形化安装程序和 GUI 工具隐藏了正在进行的实际配置，并且经常限制了你可以使用的功能。如果出现问题，在许多图形界面下调试问题可能会困难。Slackware 安装程序是基于菜单的，非常灵活且十分直观。
- 更少的臃肿——通常情况下，图形界面消耗的资源比其命令行对应更多。GUI 需要在发行介上占用更多空间，以及更多的硬盘空间和内存。GUI 在某些性能过强或不支持的显卡上可能无法良好运行甚至无法运行。Slackware 依赖于基础 Linux 命令、文本配置文件和一些简单的菜单驱动管理工具。
- 更适合低端电脑——Slackware 是我推荐在低端机器上运行的第一个发行版。特殊的 ZipSlack 发行版 (`www.slackware.com/zslack`) 可以从 100MB 的 Zip 驱动器或软磁盘安装。ZipSlack 可以安装在只有 4MB 内存的 386 PC 上。即使使用最新的 Linux 发行版，如果你想要 GUI，Slackware 的安装程序也让你能够选择小巧高效的窗口管理器、Web 浏览器、邮件客户端和其他图形工具。
- 稳定且安全——Linux 发行版将最新的内核、glibc 和 Linux 其他关键组件作为默认提供，而 Slackware 则选择了更稳定、经过更好测试的版本。在 Slackware 13 中，默认内核是 `2.6.27.7`。随着安全问题的出现，新的页面和公告会按年份发布 (`www.slackware.com/security`)。
- 按意图打包——Slackware 不会将其包含的软件在外观和感觉上进行统一。Apache 服务器、KDE 桌面或 Samba 文件/打印机共享的工作方式与它们从这些项目交付时基本相同。因此，通过使用这些项目获得的知识将相当容易地转移到 Linux 系统上的相同项目中。

Slackware 并没有提供统一的外观，而是给了你最大的控制权。它允许你选择的桌面环境或窗口管理器来决定桌面的呈现方式。你可以使用这些环境自带的菜单或偏好窗口随所欲地更改桌面。Slackware 包含了完整的 KDE 桌面环境。或者你可以选择更轻量、更高效的窗口管理器，例如 XFCE、`fwm2` 或 `twm`。

### 第 24 章：运行 Slackware Linux

**注意**
GNOME 桌面环境已从 Slackware 10.2 中移除，并不再包含在该发行版中。
Slackware 的创建者/维护者 Patrick Volkerding 提到，跟上 GNOME 开发的需求，以及某些不符合 Slackware 目标的 GNOME 功能（例如包含 PAM 和替换某些系统包，如 X11）。Volderding 建议，如果你想在自己的 Slackware 安装中添加 GNOME，可以访问 `http://gware.sf.net`。■

对于系统管理，Slackware 提供了一些基于 ncurses 文本窗口库的工具。Curses 允许应用程序在字符终端上提供一个面向屏幕的界面，因此你可以使用表单，有时甚至使用鼠标来为任何 shell 配置基础的 Linux 特性（不需要基于 X 的 GUI）。

最近添加的 Slackware 软件包管理工具（如 `slackpkg` 命令）使得添加、删除和升级包的任务变得更容易。关于 `slackpkg` 的信息请访问 `http://slackpkg.sourceforge.net`。还有用于创建自己的 Slackware 软件包的工具（如 `slacktrack` 命令）。按照 Slackware 的真正传统，Slackware 软件包非常简单：基本上是一个带有安装脚本的文件的 tar 包。

任何你在其他 Linux 发行版上能做的事情，在 Slackware 上也都能做到。只是可能需要多做一些手动工作。

**注意**
Slack 附带了一组良好的库，可以处理大多数应用程序的依赖。然而，对于视频、音频和其他类型的应用程序，你可能会发现自己需要寻找库。■

#### Slackware 社区特征

像许多其他成功的 Linux 发行版一样，Slackware 由一个意志坚定的个人创立的，他创建了适合自己的 Linux 系统。Slackware 用户通常是认同他观点的人。Slackware 的创建者 Patrick Volkerding 在 1993 年创立了 Slackware，供自己和朋友使用。他非常友回答了我的一些问题，我想把他的答案分享给你们。Patrick Volkerding 最初使用一个名为 SLS（以 Soft Landing 公司命名）的 Linux 发行版。

问题：你为什么不直接向 SLS 贡献？

Patrick：我尝试过。到 1993 年 4 月，我在 SLS 中收集了大量的错误（其中很多显而易见），而且似乎没有得到解决。当然，我开始在我修复的 SLS 版本上工作，并没有计划发布一个持久的发行版。遗憾的是，SLS 在线运行了几个月全是错误。

问题：你做了什么？

Patrick：我承诺将为 Slack 写一个新的安装程序，而不是使用修改后的 SLS 程序，并且新安装程序将是 Slack 的下一个变化。

问题：Slack 从初的巨大成功让你感到惊讶吗？

Patrick：绝对。我知道它比当时出的其他发行版都要好，但我没有料到会有大规模的人离开 SLS。

问题：什么样的人会被 Slack 吸引而不是其他发行版？

Patrick：它似乎吸引了那些想要用方式（使用文本编辑器）配置软件，并且不希望后台运行许多不必要程序的用户。我尽量用最少我的类型来编译软件，如果你决定从源码更新，这会让更新变得容易。

问题：你如何描述 Slack 的开发过程？

#### 第 24 章：运行 Slackware

**Patrick**: 我做的大部分工作都是研究——试图弄清楚 Linux 将向何方发展，以便我（我希望）对实现什么做出理智的选择。这里确实有一个核心开发团队（通过绕过任何官方开发层级中常见的、浪费时间的争论，该团队实际上简化了开发流程）。但我从人们那里获得了了大量的帮助，他们通过电子邮件向我反馈问题或建议，这些建议导致了系统某处的升级或修复。

跟进 Slackware 开发问题的最佳方法是阅读更改日志（可从 Slackware 主页获取）。Slackware 爱好者期望按照“准备好了就发布”的进度计划进行发布，而 Slackware 常见问题解答（FAQ）提到：“随着即将发布版本的构建工作逐渐完成，它们将被上传到当前树目录中。如果该版本不存在，可能意味着我们刚刚发布了新版本的 Slackware。”

#### Slackware 用户

从纯主观的角度来看，我使用 Slack 的朋友往往倾向于技术导向，但并不是那些可能被 Gent 等发行版吸引的极端超频和调优者。他们喜欢 Slack 是因为它运行得非常好，以至于让他们有更多时间去偷懒（slack）。

Slackware 用户通常认为自己是独行侠，尽管他们都活跃在局域网派对和网吧。他们发布得越多，Slackware 的商业化倾向就越低。对于他们的个人桌面、游戏机箱或小型办公服务器，他们认为不需要 Red Hat Enterprise 或 SUSE Linux 系统中提供的那些图形化安装和管理工具。他们对命令和手册页（man pages）感到自在。

我听过用户称 Slackware 比其他 Linux 发行版更容易使用。对于那些拥有 UNIX 或 BSD 背景的人来说，这可能是事实。你不需要等待图形化工具弹出，而且所有内容都涵盖在一个页面上。

**注意**

手册页（Man pages）是记录命令、文件格式、设备、系统调用以及 UNIX 或 Linux 系统任何其他组件的传统文档方法。手册页可以追溯到第一个 UNIX 系统。你可以从任何 shell 使用 `man` 命令后跟组件名称来阅读手册页。要学习该页系统是如何运作的，请输入 `man man`。■

#### Slackware 网上网站

Slackware 主页（`www.slackware.com`）是开始寻找 Slackware 信息的好地方。通过网站可以使用两个主要的邮件列表和一个 IRC 通道，以及指向下载站点、文档和 Slackware 商店（`store.slackware.com`）的链接。

Slackware 网站提供了一本 Slack Linux Essentials 在线书籍（`www.slackbook.org/`）和四个常见问题解答（`www.slackware.com/faq/`）。Slackware 网站上也没有所谓的“新闻”可言，跟进项目动态的最佳方法是阅读更改日志（`www.slackware.com/changelog/`）。

有关本章描述的 Slackware 版本（13）的信息，请参阅发布公告（`www.slackware.com/announce/13.0.php`）。请参阅软件包更改列表（`ftp.slackware.com/pub/slackware-current/Changelog.txt`）以获取有关处理此版本的细节。

在 Slackware 官方网站之外，最近涌出了许多提供 Slackware 信息的网站。提问关于 Slackware 的问题，一个好地方是 `http://linuxpackages.org`（关注链接：Forums Linux-Distributions Slack）。Linux Packages 网站（`www.linuxpackages.net`）提供了关于 Slackware 不同方面的一些活跃论坛。

#### 使用 Slackware 的挑战

Slackware 背后没有商业组织，也没有官方支持，因此如果你的 Slackware 系统出现任何问题，你只能自己解决。然而，Slackware 项目在 `www.slackware.com/support/` 提供了一个提供技术支持的第三方组织列表。

尽管在功能上 Slackware 可以用于大多数计算环境，但在你觉得需要所安装的系统具有二进制计算的地方（例如大型企业），你最好应该考虑 Red Hat 或 SUSE 系统。

缺乏官方软件包管理工具给 Slackware 用户带来了另一个挑战。Slackware 的打包工具相比于仅从 tarball（tar 包）安装已是一个巨大的改进，但对于那些尚未达到你可以在基于 RPM 的发行版（Fedora, Red Hat Enterprise Linux, SUSE, Mandriva）以及基于 Deb 的发行版（Debian, Ubuntu, KNOPIXX 等）中可以拥有的复杂程度的人来说。

当为 Slackware 制作的软件包需要标准 Slackware 发行版未包含的库时，开发者通常会将所需的库构建到软件包中。如果软件失败并指示缺少库，你可以尝试几种方法：

- 在软件软件包的 README 文件中查找库的描述。
- 使用 `ldd` 命令确定命令所需的库（例如，输入 `ldd /bin/cat` 显示 cat 命令所需的库）。
- 在网络上搜索术“Slackware”和缺失库的名称。

#### 从 Windows 过来

作为一名熟悉 UNIX 和 Linux 的人，你会发现 Slackware 自带的文本工具很有帮助且相当易用。然而，如果你来自 Windows 环境，你可能会发现缺乏基于 GUI 的工具以及设置功能的端到端连贯程序令人困惑。

#### 第 24 章：运行 Slackware

由于 Slackware 没有大型支持组织的支持，它在企业级领域尚未取得太大进展。大多数商业应用程序是专门为 Red Hat Enterprise Linux 创建的，或者在较程度上为 SUSE 发行版创建的，并且无法开箱即用，这一事实使得 Slackware 在企业环境中更难推销。

#### 将 Slackware 作为开发平台

Slackware 长期以来一直是开发开源软件的首选平台。它包含了大量的库和几乎你开发应用程序所需的每一个工具。Slackware 还有专门的分支项目，例如用于开发 Linux 程序的 ARM 处理器 Slackware 项目（`www.armedslack.org`）。

由于 Slackware 是一个干净、基础的 Linux 系统，在 Slack 上运行的应用程序可以在大多数其他 Linux 系统上运行。换句话说，你不会被鼓励添加许多特殊的钩，这些钩会阻止软件在广泛的 Linux、UNIX 和 BSD 系统之间迁移。

Slackware 可以轻松为技术人员提供高效的开发环境，因为该发行版不会阻碍其强大功能的使用。配置一个简单的窗口管理器很容易，而且不会产生在插入 CD 或需要软件更新时那些“帮助”你的后台进程的开销。Slackware 仅仅给你一个高效的桌面，让你知道自己需要什么，尽可能贴近硬件，并在其他时候不打扰你。

如果你对构建并向 Slackware 提交软件包感兴趣，Linux Packages 网站（`www.linuxpackages.net`）提供了关于如何操作的一些良好描述。可以在该网站主页的信息框中找到构建和提交软件包的链接。

#### 安装 Slackware

Slackware 可以从多个源免费获取。它在低配置计算机上安装和运行良好。一些 Linux 或 UNIX 知识将有用，特别是当出现问题时。

##### 获取 Slackware

Slackware 13 包含在一张 DVD（约 3.7GB）或六张 CD 上：三张安装 CD 和三张源码 CD。在之前的版本中，Slackware 在第一张安装 CD 上包含了足够的软件来安装一个轻量、高效的桌面系统。由于现在不再如此，随书 DVD 的 Slackware 软件包含了从几张官方 Slackware CD 合并的软件包，因此你可以从该 DVD 安装一个可用的桌面系统。

完整的 Slackware 发行版也可以从网络上的几十个镜像站点获取（详见 `www.slack.com/getslack`）。由于磁盘空间问题以及为了最大限度地利用带宽，Slackware 项目建议您通过 BitTorrent 获取 DVD 或 CD 镜像（ISOs）。有关可用 torrent 文件的列表，请参阅 `www.slack.com/getslack/torrents.php`。

**注意**

多年来，Slackware 只需要一张安装 CD 即可运行，但在向发行版中加入 KDE 之后，使得额外的 CD 变得成为必要。

为了帮助该项目，您可以从 `http://slack.com` 购买盒装版 Slackware 丛包。在商店中，您可以订阅 Slackware，这样每当发布新版本时（每每六到八个月发布一次），Slack 商店都会向您发送一个新版本。当版本可用时，商店将发货并扣除您的信用卡费用。喜欢 Slackware 的人们通常会支付订阅费以表示支持。

##### Slackware 13 的新功能

凭借 Slackware 13，该发行版包含三张安装 CD（外加三张源码 CD）和/或一个包含所有内容的 DVD 版本。虽然仍然提供稳定的 2.6.29 内核，但该版本包含了最新的 Firefox 浏览器。此外，以下是 Slackware 中包含的一些新应用：

- KDE 4.2——桌面、文件管理器
- SeaMonkey 1.1——浏览器、电子邮件客户端
- Thunderbird——电子邮件客户端

要使用 Slackware 软件包，请在 Slackware 13 中操作，这包含了 Slackware 软件包数据库。要让 Slackware 软件包工作，在 Slackware 13 中包含 Slackware 软件包的 HTML 页面，这比过去要简单得多。

##### 硬件要求

虽然某些版本的 Slackware 可以在较旧硬件上运行，但建议使用以下处理器：
- 386
- 486
- Pentium III
- Pentium 4
- Duron/Athlon

运行 Slackware

在没有图形界面（X Window）的情况下，Slackware 至少需要的内存为：
- 64 MB
- 128 MB
- 256 MB
- 500 MB
- 1 GB

如果您打算使用图形界面，Slackware 至少需要的内存为：
- 256 MB
- 512 MB
- 1 GB
- 2 GB
- 4 GB 或更多

Slackware 支持所有的 IDE 和 SCSI 控制器。

##### 开始安装

尽管 Slackware 安装程序已经不断演变，但其外观并没有太大变化。以下步骤描述了如何从第一张 CD 安装 Slackware。如果您想进行更完整的安装，请参考本书中的 Slackware 安装集。如果在安装过程中遇到问题，请参考 Slackware-HOWTO。

- 1. 获取 Slackware 安装盘。（如前所述，您可以从 DVD 获取，或者从 Slackware 镜像站点下载官方 ISO 并刻录到 CD。）
- 2. 将本书的 DVD 插入驱动器并重启电脑。
- 3. 从启动界面选择 slackware 以启动启动过程。如果您使用的是 CD 而不是 DVD，直接按回车。

如果 Slackware 安装正常启动，将提示输入键盘布局。

**注意**

如果 Slackware 无法启动，请参阅 CD 上的 `BOOTING.TXT` 文件以获取解决问题的信息（如果您完全无法访问 CD，可以从任何 Slackware 镜像站点获取此文件）。

- 4. 如果您使用的是美国键盘布局，按回车。如果想使用其他语言/国家的键盘布局，输入 1，按回车，然后选择您想要的。出现 登录提示。
- 5. 输入 `root` 并按回车。出现提示。
- 6. 分区您的硬盘。第 8 章解释了如何划分硬盘。Slackware 没有图形化分区工具，例如 Disk Setup。
- 7. 进入设置模式。输入以下命令进入设置模式：

```
setup
```
