
# Linux 基础大师指南

## 摘要

本书旨在用于导师引导的培训。对于自学者，其意图是在一台运行中的 Linux 电脑旁阅读本书，以便你可以立即操作每个主题，练习每条命令。

本书面向初级 Linux 系统管理员（对于想要进一步了解其 Linux 系统的家庭用户来说也可能有趣且有用）。然而，本书并非用于介绍 Linux 桌面应用程序，如文本编辑器、浏览器、邮件客户端、多媒体或办公软件。

更多信息和免费的 `.pdf` 文件请访问 `http://linux-training.be`。

欢迎随时联系作者：

- `Paul Cobbaut`: `pcobbaut@gmail.com`, `http://www.linkedin.com/in/cobbaut`
- `Serge van Ginderachter`: `serge@ginsys.eu`, 编译构建脚本和基础设施设置
- `Ywein Van den Brauwe`: `ywein@crealau.eu`, 许可与法律章节
- `Hendrik De Vloed`: `hendrik.devloed@ugent.be`, `builderheap.pl` 脚本

Linux 培训项目的贡献者：

- 我们还感谢我们的审稿员：
  - `Wouter Verhest`: `wo@uter.be`, `http://grep`
  - `Geert Goossens`: `mail.goossens.geert@gmail.com`, `http://www.linkedin.com/in/geertgoossens`
  - `Elie De Brauer`: `elie@de-brauer.be`, `http://www.de-brauer.be`
  - `Christophe Vandeplas`: `christophe@vandeplas.com`, `http://christophe.vandeplas`
  - `Bert Desmet`: `bert@devnox.be`, `http://blog.bdesmet.be`
  - `Rich Yonts`: `richychs@gmail.com`

- `24.3. if elif` ............................................................................. `242`
- `24.7. 练习：测试测试与循环` ................................. `244`
- `25.6. 使用 shebang 获取 shell 选项` ................................. `252`
- `25.8. 解决方案：参数与选项` ................................. `254`
- `28. 用户管理` ................................................................. `274`
- `28.7. 用户管理` ................................................................. `277`
- `30. 配置文件` ................................................................. `291`

# 第一部分 Linux 简介

# 第 1 章 Linux 历史

本章简要介绍了 `Unix` 的历史以及 `Linux` 的所处位置。

如果你急于开始使用 `Linux`，而不想听这些关于历史、发行版和许可证的废话，请直接跳转到第 11 部分 - 第 8 章 目录操作第 73 页。

## 1.1. 1969

所有操作系统的根源都可以追溯到 1969 年，当时 `Dennis Ritchie` 和 `Ken Thompson` 在 `AT&T` 贝尔实验室开发了 `C` 语言和 `Unix` 操作系统。他们向世界分享了他们的源代码（是的，在 70 年代就有开源概念了），包括来自加利福尼亚州伯克利的的嬉皮士们。到 1975 年，当 `AT&T` 开始商业化 `Unix` 时，大约一半的代码是由他人编写的。嬉皮士们对商业公司出售他们编写的软件感到不悦；由此产生的（法律）斗争导致了两个版本的 `Unix`：官方的 `AT&T Unix` 和免费的 `BSD`。

基于 `FreeBSD`、`OpenBSD`、`NetBSD`、`DragonFly BSD` 和 `PC-BSD` 的 `BSD` 后代开发仍在进行。

```
https://en.wikipedia.org/wiki/Dennis_Ritchie
https://en.wikipedia.org/wiki/Ren_Thompson
https://en.wikipedia.org/wiki/BSD
https://en.wikipedia.org/wiki/Comparison_of_BSD_operating_systems
```

## 1.2. 1980s

在 80 年代，公司开始开发自己的 `Unix`：`IBM` 创建了 `AIX`，`SunOS`（后来的 `Solaris`），`HP` 创建了 `HP-UX`，其他十几个公司也做了同样的事情。结果是 `Unix` 方言的混乱局面，以及实现相同功能的多种不同方法。这就是 `Linux` 的第一个真正根源，当时 `Richard Stallman` 结束了那个 `Unix` 割裂时代，每个人通过启动 `GNU` 项目（`GNU` 的含义是“`GNU` 不是 `Unix`”）来开始重新发明轮子。他的目标是创建一个所有人都能免费获取的操作系统，并且每个人都能共同工作（就像在 70 年代那样）。你今天在 `Linux` 上使用的许多命令行工具都是 `GNU` 工具。

```
https://en.wikipedia.org/wiki/Richard_Stallman
https://en.wikipedia.org/wiki/IBM_AIX
https://en.wikipedia.org/wiki/HP-UX
```

## 1.3. 1990s

90 年代始于一位说瑞典语的芬兰学生 `Linus Torvalds`，他买了一台 `386` 计算机并编写了一个全新的符合 `POSIX` 标准的内核。他将源代码发布到网上，认为它将支持除 `386` 硬件以外的所有设备。许多人接受了这种内核与 `GNU` 工具的结合，剩下的正如俗说，都是历史了。

```
https://en.wikipedia.org/wiki/Linus_Torvalds
https://en.wikipedia.org/wiki/History_of_Linux
https://en.wikipedia.org/wiki/Linux
https://en.lwn.net
http://www.levenez.com/unix/ (一张巨大的 Unix 历史海报)
```

## 1.4. 2015

今天，世界上超过 97% 的超级计算机（包括完整的前 10 名）、超过 80% 的智能手机、数百万台桌面电脑、约 70% 的 `Web` 服务器、大部分平板电脑以及多种设备（`dvd` 播放器、洗衣机、`dsl` 调制解调器、路由器、自动汽车、空间站笔记本电脑……）都在运行 `Linux`。`Linux` 是目前全球最常用的操作系统。

`Linux` 内核 4.0 版本于 2015 年 4 月发布。得益于来自 `Red Hat`、`Intel`、`三星`、`博通`、`德州仪器`、`IBM`、`Novell`、`高通`、`诺基亚`、`Oracle`、`Google`、`AMD` 甚至`微软`（以及更多）等数百家商业公司的数千名开发者的贡献，其源代码增加了几十万（相比 2015 年 2 月的 3.19 版本）。

```
http://kernelnewbies.org/DevelopmentStatistics
http://kernel.org
http://www.top500.org
```

# 第 2 章 发行版

本章要介绍当前 Linux 发行版。

`Linux` 发行版是基于 `Linux` 内核的一系列（通常是开源的）软件集合。发行版（或简称 `distro`）可以将服务器软件、系统管理工具、文档和许多桌面应用程序封装在**中心安全软件仓库**中。发行版旨在提供共同的外观和体验、安全且易于软件的管理，通常具有特定的用途。

让我们来看一些流行的发行版。

## 2.1. Red Hat

`Red Hat` 是一家价值数十亿美元的商业 `Linux` 公司，在开发 `Linux` 上投入了大量精力。他们拥有数百名 `Linux` 专家，并以卓越的支持闻名。他们免费提供产品（`Red Hat Enterprise Linux` 和 `Fedora`）。虽然 `Red Hat Enterprise Linux` (`RHEL`) 经过充分测试，并在发布后提供长达七年的支持，但 `Fedora` 是一个更新更快但没有支持的发行版。

## 2.2. Ubuntu

`Canonical` 从 2004 年开始发送带有 `Ubuntu Linux` 的免费光盘，并迅速在家庭用户中流行（许多人从 `Microsoft Windows` 转过来）。`Canonical` 希望 `Ubuntu` 是一个易于使用的图形化 `Linux` 桌面，不需要命令行。当然，他们也希望通过销售 `Ubuntu` 的支持来盈利。

## 2.3. Debian



Debian 背后没有公司。相反，有数千名组织良好的开发者每两年选出一个 Debian 项目负责人。Debian 被认为是最稳定的 Linux 发行版之一。它也是每个 Ubuntu 版本的基础。Debian 有三个版本：`stable`（稳定版）、`testing`（测试版）和`unstable`（不稳定版）。每个 Debian 版本都以《玩具总动员》电影中的角色命名。

## 2.4. 其他

`CentOS`、`Oracle Enterprise Linux` 和`Scientific Linux` 等发行版基于 `Red Hat Enterprise Linux`，并共享许多相同的原理、目录和系统。`Linux Mint` 和`Ubuntu` 基于`Debian`。

## 2.5. 选择哪一个？

今天，世界上超过 97% 的超级计算机（包括完整的前 10 名）、超过 80% 的智能手机、数百万台桌面电脑、约 70% 的 Web 服务器、大部分平板电脑以及多种设备（`dvd` 播放器、洗衣机、`dsl` 调制解调器、路由器、自动汽车、空间站笔记本电脑……）都在运行 Linux。Linux 是目前全球最常用的操作系统。

| 发行版名称 | 原因 |
| :--- | :--- |
| `Red Hat` (`RHEL`) | 你需要企业支持 |
| `Fedora` | 你需要快速更新 |
| `Debian` | 你需要稳定性 |
| `Ubuntu` | 你需要易用的图形化桌面 |
| `Linux Mint` | 你想要熟悉的界面 |
| `Kali Linux` | 你是安全专业人员/渗透测试员 |
| `CentOS` | 你想要基于 `RHEL` 的替代方案 |

# 第 3 章 许可

本章简要解释 Linux 中使用的许可。

## 3.1. 关于许可

存在两种主要的软件范式：自由与开源（`FOSS`）和私有软件。这两种方法的区别在于控制权。对于私有软件，控制权更倾向于供应商；而在自由与开源软件中，控制权更倾向于用户。尽管范式不同，但它们适用相同的版权法。法律理论认为，`FOSS` 的作者与公有领域不同，并没有放弃权利。`FOSS` 允许实施需要用户遵守的许可条件。

## 3.2. 公有领域软件和免费软件

在意义上是作者独创创作的软件受版权保护。非原创性软件不属于版权保护范围，原则上可以自由使用。公有领域软件可以在无需许可或支付费用的情况下自由使用、复制或执行。在某些情况下，第三方甚至将其作为自己的作品展示，并通过修改原始作品提取出某些版本。

免费软件不是公有领域软件或 `FOSS`。它是不需要支付许可费的私有软件；但必须遵守严格的许可。在使用第三方软件之前务必检查您的许可。

私有软件的示例包括 `IBM` 的 `AIX`、`HP` 的 `HP-UX` 以及 `Oracle Database`。未经支付许可费，您无法安装或使用这些软件。您不允许分发副本，也不允许修改源代码。

（四项自由）自由软件向其用户提供了这四项自由，而开源软件运动则指出了其《开源定义》以及点对点软件开发的优势。

最近，“自由与开源软件”（`FOSS`）这一术语已作为一种中性的替代方案出现。另一个使用频率较低的变体是“自由/libre/开源软件”（`FLOSS`），它使用 `libre` 来澄清 `free` 在“自由（freedom）”中的含义，而不是“免费（no charge）”。

自由软件的示例有 `gcc`、`MySQL` 和 `gimp`。

关于四项自由的详细信息可以在此处找到：

```
http://www.gnu.org/philosophy/free-sw.html
```

开源定义可以在此处找到：

```
http://www.opensource.org/docs/osd
```

上述定义基于此处获取的 Debian 自由软件指南：

```
http://www.debian.org/social_contract@guidelines
```

## 3.4. GNU 通用公共许可证

越来越多的软件正在基于 `GNU GPL` 发布（2006 年 `Java` 是基于 `GPL` 发布的）。该许可证（`v2` 和 `v3`）是自由软件基金会背书的主要许可证。其主要特征是开源传染（`copyleft`）原则。这意味着在连续用户链中的每一个人，为了获得赋予的使用权，如果他们选择分发对软件的改进及其衍生作品，需要在相同条件下将这些改进或衍生作品也分发给其他用户。换句话之，包含了 `GNU` 软件的软件需要转作为 `GNU GPL` 软件（或兼容软件，见下文）分发。在专有许可的作品中包含版权保护的 `GNU` 软件部分。`GPL` 已在法院获得维护。

## 3.5. GPLv3 软件

你几乎可以在没有任何条件的情况下使用 `GPLv3` 软件。如果你只是运行软件，则不需要接受 `GPLv3` 的条款。然而，任何其他用途——例如修改或分发软件——都意味着接受。

如果你在内部使用软件（包括通过网络），你可以修改软件而无义务分发你的修改。你可以聘请第三方在你指导和控制下专门为你软件工作。但如果你修改了软件并在非仅仅内部的情况下使用它，这将被视为分发。你必须根据 `GPLv3` 分发你的修改（开源传染原则）。如果你分发 `GPLv3` 软件，还有几项额外的义务。请仔细检查 `GPLv3` 许可证。

你使用 `GPLv3` 软件创建输出：`GPLv3` 不自动适用于输出内容。

## 3.6. BSD 许可证

原始的伯克利分发许可证有多个版本。最常见的是三条款许可证“新 `BSD` 许可证”或“修改版 `BSD` 许可证”。

这是一个许可性的自由软件许可证。该许可证对软件如何重新分发施加了极小的限制。这与上面讨论的具有传染机制的许可证（如 `GPLv2`、`v3`）形成对比。

当你仅仅使用软件时，这种差异并不重要，但当你开始重新分发软件的逐字副本或你自己的修改版本时，这种差异就会体现出来。

## 3.7. 其他许可证

无论是否为 `FOSS`，软件都有许多种许可证。在使用任何软件之前，你应该阅读并理解它们。

## 3.8. 软件许可证的组合

当你使用多个来源或希望在不同的许可证下重新分发你的软件时，你需要验证所有许可证是否兼容。某些 `FOSS` 许可证（如 `BSD`）与专有许可证兼容，但大多数并不兼容。如果你检测到许可证不兼容，你必须联系作者协商不同的许可证条件，或放弃使用不兼容的软件。

## 第二部分。安装 Linux

## 第 4 章。安装 Debian 8

本模块是 Debian 8 实际安装的步骤演示。

我们开始从互联网下载镜像并在 `Virtualbox` 中安装 Debian 8。我们还将对这台新机器进行一些配置，如设置 `IP` 地址和主机名。

如果你想安装 `CentOS`、`Fedora`、`Red Hat Linux`、... 请查看下一章。

## 4.2. 下载

所有截图均制作于 2014 年 11 月

在此处下载 Debian：

![](img/127a5ac6776c2933c37f7b2f9e005369_25_0.png)

在这个网站上点击几次后，我最终在这里下载了 Debian 8 (测试版)。等 debian 8 发布后（大约在 2015 年某时候），应该只需要点击一下了。

![](img/127a5ac6776c2933c37f7b2f9e005369_26_0.png)

你还有许多其他 Unix 工具可以下载并安装 Debian。我们稍后会详细讨论。

这个小截图显示了下载 `netinst_iso` 文件的过程。大部分软件将在安装过程中下载。这意味着当安装完成后，`paul` 将拥有所有软件包的最新版本。

![](img/127a5ac6776c2933c37f7b2f9e005369_26_1.png)

我已经在笔记本电脑上安装了 Debian 8（显示 `paul@debian8` 提示符）。无论如何，这是开始安装前的下载文件。

```
paul@debian8:~$ ls -hl debian-testing-amd64-netinst.iso
-rw-r--r-- 1 paul paul 231M Nov 10 17:59 debian-testing-amd64-netinst.iso
```

# 安装 Debian 8

创建一个新的 `Virtualbox`（我已经有五个，你现在可能一个还没有）。点击“New（新建）”按钮将启动向导，帮助你创建虚拟机。

![](img/127a5ac6776c2933c37f7b2f9e005369_27_0.png)

机器需要一个名称，截图显示他将其命名为 `server42`。

![](img/127a5ac6776c2933c37f7b2f9e005369_27_1.png)

`Virtualbox` 的大部分默认设置都是可以。

512MB 的内存足够练习此书中的所有主题。

![](img/127a5ac6776c2933c37f7b2f9e005369_28_0.png)

我们不在乎虚拟磁盘格式。

![](img/127a5ac6776c2933c37f7b2f9e005369_28_1.png)

选择“动态分配（dynamically allocated）”可以节省一些磁盘空间（会有轻微的性能影响）。

![](img/127a5ac6776c2933c37f7b2f9e005369_29_0.png)

8GB 对于学习 Linux 服务器来说绰绰有。



![](img/127a5ac6776c2933c37f7b2f9e005369_29_1.png)

向导结束了。你的虚拟机几乎准备好开始安装。

## 安装 Debian 8

首先，确保将下载的 `.iso` 镜像挂载到虚拟 CD 驱动器（通过打开“Settings（设置）”、“Storage（存储）”，然后点击圆形的 CD 图标）。

![](img/127a5ac6776c2933c37f7b2f9e005369_30_0.png)

我个人禁用了声音和 `USB`，因为我从不使用这些功能。我还删除了软磁盘使用和 `PS/2` 鼠标指针。这可能不怎么重要，但我喜欢这种节省某些资源的想法。

现在启动虚拟机并开始实际安装。几秒钟后，你应该会看到类似这样的屏幕。选择“Install（安装）”开始安装 `Debian`。

![](img/127a5ac6776c2933c37f7b2f9e005369_30_1.png)

## 安装 Debian 8

首先选择你想要使用的语言。

![](img/127a5ac6776c2933c37f7b2f9e005369_31_0.png)

选择你的国家。此信息将用于建议下载镜像。

![](img/127a5ac6776c2933c37f7b2f9e005369_31_1.png)

## 安装 Debian 8

选择正确的键盘。由于大多数服务器通过 `ssh` 远程管理，这一点并不重要。

![](img/127a5ac6776c2933c37f7b2f9e005369_32_0.png)

输入主机名（带有完全限定域名 `fqdn`）。

![](img/127a5ac6776c2933c37f7b2f9e005369_32_1.png)

## 安装 Debian 8

给 `root` 用户设置密码。记住这个密码（或使用 `hunter`）。

![](img/127a5ac6776c2933c37f7b2f9e005369_33_0.png)

建议创建一个普通用户账户。`Debian` 8 接受用户名和全名。

![](img/127a5ac6776c2933c37f7b2f9e005369_33_1.png)

## 安装 Debian 8

“使用整个磁盘（use entire disk）”指的是你之前在 `Virtualbox` 中创建的虚拟磁盘。

![](img/127a5ac6776c2933c37f7b2f9e005369_34_0.png)

默认设置通常是你需要的。只有在你清楚自己在做什么时才进行更改。

![](img/127a5ac6776c2933c37f7b2f9e005369_34_1.png)

## 安装 Debian 8

接受分区布局（同样在你清楚自己在做什么时进行更改）。

![](img/127a5ac6776c2933c37f7b2f9e005369_35_0.png)

这是无法回头的时刻，按下将永久擦除（虚拟）计算机上的数据。

![](img/127a5ac6776c2933c37f7b2f9e005369_35_1.png)

软件从镜像仓库下载，最好是距离较近。

![](img/127a5ac6776c2933c37f7b2f9e005369_36_0.png)

此设置比利时完成的。

![](img/127a5ac6776c2933c37f7b2f9e005369_36_1.png)

## 安装 Debian 8

将代理字段留（除非你确定自己在代理服务器之后）。

![](img/127a5ac6776c2933c37f7b2f9e005369_37_0.png)

选择你是否想向 `Debian` 项目发送匿名统计（它收集有关安装软件包的数据）。你可以在这里查看统计：`http://popcon.debian.org/`

![](img/127a5ac6776c2933c37f7b2f9e005369_37_1.png)

## 安装 Debian 8

选择要安装的软件，我们的训练不需要任何图形化内容。

![](img/127a5ac6776c2933c37f7b2f9e005369_38_0.png)

最新版本正在下载。

![](img/127a5ac6776c2933c37f7b2f9e005369_38_1.png)

## 安装 Debian 8

说“是”在虚拟机上安装启动加载程序。

![](img/127a5ac6776c2933c37f7b2f9e005369_39_0.png)

首次启动显示 `grub`

![](img/127a5ac6776c2933c37f7b2f9e005369_39_1.png)

几秒钟后，你应该看到大量文本在屏幕上滚动（`dmesg`）。之后你会看到这个 `getty` 界面并被允许第一次登录。

![](img/127a5ac6776c2933c37f7b2f9e005369_40_0.png)

现在你应该可以使用 `root` 账户登录你的虚拟机。你记得密码吗？是 `hunter2` 吗？

![](img/127a5ac6776c2933c37f7b2f9e005369_40_1.png)

从现在起，书中的截图将像这样。你可以在终端中输入这些命令（在登录后）。

```
root@server42:-# who am i
root             tty1      2014-11-10 18:21
root@server42:-# hostname
server42
root@server42:-# date
Mon Nov 10 18:21:56 CET 2014
```

## 4.3. virtualbox 网络

你也可以远程（或从你的 `Windows`/`Mac`/`Linux` 宿主机）使用 `ssh` 或 `putty` 进行登录。将虚拟机中的网络设置更改为“桥接（bridge）”。这将使虚拟机能够从你的 `DHCP` 服务器接收 `IP` 地址。

`Virtualbox` 的默认网络设置是将虚拟网络节点连接到 `nat`。此截图显示在 `nat` 时的 `IP` 地址为 `10.0.2.15`：

## 4.4. 设置主机名

在安装过程中会询问服务器的主机名，因此不需要手动进行配置。

```
root@server42:~# hostname
server42
root@server42:~# cat /etc/hostname
server42
root@server42:~# dnsdomainname
paul.local
root@server42:~# grep server42 /etc/hosts
127.0.1.1 server42.paul.local server42
root@server42:~#
```

## 4.5. 添加静态 IP 地址

此示例展示了如何为你的服务器添加静态 `IP`。设置在下次重启（或下次 `ifdown`）之前有效。

```
root@server42:~# ifconfig eth0:0 10.104.33.39
```

向 `/etc/network/interfaces` 文件添加几行内容以使额外的 `IP` 地址永久生效。

```
root@server42:~# vi /etc/network/interfaces
root@server42:~# tail -4 /etc/network/interfaces
auto eth0:0
iface eth0:0 inet static
address 10.104.33.39
netmask 255.255.255.0
root@server42:~# ifconfig
eth0: Link enc=Ethernet Haddr=00:00:27:f5:74:cf
inet addr=192.168.1.11 Bcast:192.255.255.0
inet6 addr=fe80::201:ff2f:74c4:f64/64 Scope:Link
UP BROADCAST MULTICAST MTU:1500 Metric:1
RX packets=528 errors=0 dropped=0 overruns=0 frame=0
TX packets=333 errors=0 dropped=0 overruns=0 carrier=0
collisions=0 txuelen=0
RX bytes=4549 (44.3 KB) TX bytes=48763 (47.6 KB)
```

```
eth0: Link enc=Ethernet Haddr=00:00:27:f5:74:cf
inet addr=10.104.33.39 Bcast:10.255.255.0 Mask:255.0.0.0
UP BROADCAST MULTICAST MTU:1500 Metric:1
```



```
lo Link enc=Local Loopback
inet addr=127.0.0.1 Mask:255.0.0.0
inet6 addr=::1/128 Scope:Host
UP LOOPBACK Metric:1
RX packets=0 errors=0 dropped=0 overruns=0 frame=0
TX packets=0 errors=0 dropped=0 overruns=0 carrier=0
collisions=0 txuelen=0
RX bytes=0 (0.0 B) TX bytes=0 (0.0 B)
```

```
root@server42:~#
```

## 4.6. Debian 包管理

要从在线仓库获取关于最新软件包的信息：

```
root@server42:~# aptitude update
Get: 1 http://ftp.be.debian.org/jessie InRelease [191 kB]
Get: 2 http://security.debian.org/jessie/updates [84.1 kB]
Get: 3 http://ftp.be.debian.org/jessie-updates InRelease [117 kB]
Get: 4 http://ftp.be.debian.org/jessie-backports InRelease [118 kB]
Get: 5 http://security.debian.org/jessie/updates/main Sources [14 B]
Get: 6 http://ftp.be.debian.org/jessie/main Sources/DiffIndex [786 B]
... (输出省略)
```

下载并更新所有已安装的软件包：

```
root@server42:~# aptitude upgrade
Resolving dependencies...
以下新软件包将要安装:
firmware-linux-free irlb lhsinal linux-3.16.0-4-amd64
以下软件包将要升级:
lib-bin libc libmagic libpaper-utils libpaper1 sqlite3-0
12 个已升级，4 个新安装，0 个将移除，0 个未升级。
需要下载 44.9 MB 的存档。解压后将使用 61 MB。
继续吗？[Y/n]
... (输出省略)
```

安装新软件（此示例中使用 `vim` 和 `tmux`）：

```
root@server42:~# install vim tmux
以下新软件包将要安装:
tmux-runtime
0 个已升级，3 个新安装，0 个将移除，0 个未升级。
需要下载 24.3 MB 的存档。解压后将使用 29.0 MB。
继续吗？[Y/n]
Get: 1 http://ftp.be.debian.org/jessie/main tmux 1.9-6 [245 kB]
Get: 2 http://ftp.be.debian.org/jessie/main vim-runtime 2:748-1 [5046 kB]
Get: 3 http://ftp.be.debian.org/jessie/main vim amd64 2:748-1 [952 kB]
```

参考 Linux 中的包管理章节。

# 第 5 章. 安装 CentOS 7

本模块是实际安装 `CentOS 7` 的逐步演示。我们从互联网下载并安装 `CentOS 7` 虚拟机。我们将对这台新机器进行一些基础配置，例如设置 `IP` 地址和主机名。对于其他版本的 `CentOS` 或如 `RHEL` (`Red Hat Linux`)、`Fedora` 等发行版，该过程也相似。

## 5.1. 下载 CentOS 7 镜像

本演示使用笔记本电脑通过 `Virtualbox` 虚拟机。第一个任务是下载 `CentOS 7` 的 `.iso` 镜像。如 `CentOS 7` 网站目前所示（2014 年 11 月），它们会经常变化，所以当你访问时看起来可能不同。

`![](img/127a5ac6776c2933c37f7b2f9e005369_46_0)` 你可以下载完整的 `DVD` 进行 `CentOS 7` 桌面的图形化安装。你可以选择它，因为它简单且能让你运行 `CentOS 7` 虚拟机。

**安装 CentOS 7**

我点击了“替代下载”（`alternative downloads`），选择了 `CentOS 7` 和 `x86_64`，然后进入了镜像列表。每个镜像都是包含 `CentOS 7` 介质的服务器。因为我目前在比利，所以我选择了比利的镜像。

`![](img/127a5ac6776c2933c37f7b2f9e005369_47_0)`

再次有完整 `DVD` 和更多选项。本演示将使用最小的 `.iso` 文件，因为体积小得多。下载需要几分钟。

`![](img/127a5ac6776c2933c37f7b2f9e005369_47_1)`

下载后验证文件大小以确保正确。如果你使用 `Windows` 或 `Mac OSX`，可能需要右键点击文件并选择“属性”。在上面的笔记本电脑上：

```
$ paul@debian8~$ ls -lh CentOS-7.0-1406-x86_64-Minimal.iso
-rw-r--r-- 1 paul 566M Nov 1 14:45 CentOS-7.0-1406-x86_64-Minimal.iso
```

如果你理解该命令请不要担心。只需确保该文件的大小与 `CentOS 7` 网站上提到的一致即可。

## 5.2. Virtualbox

当我启动 `Virtualbox` 时会显示此截图。我已经有四个虚拟机，你可能一个都没有。

`![](img/127a5ac6776c2933c37f7b2f9e005369_48_0)`

以下是创建新虚拟机的步骤。首先点击 `New`（新建）并为你的机器命名（我选择了 `server33`）。点击 `Next`（下一步）。

`![](img/127a5ac6776c2933c37f7b2f9e005369_48_1)`

没有图形界面的 `Linux` 电脑在半 `GB` 内存上运行良好。

`![](img/127a5ac6776c2933c37f7b2f9e005369_49_0)`

`Linux` 虚拟机需要一个虚拟硬盘。

`![](img/127a5ac6776c2933c37f7b2f9e005369_49_1)`

任何格式都适用于我们的目的，所以我留下了默认的 `vdi`。

`![](img/127a5ac6776c2933c37f7b2f9e005369_50_0)` 动态分配类型可以节省空间（直到虚拟磁盘填充到 100%）。它会让虚拟机比固定大小慢一点，但对于我们的目的来说，固定大小的速度提升并不值得。

`![](img/127a5ac6776c2933c37f7b2f9e005369_50_1)`

在主机电脑上的虚拟磁盘文件名称将是 `server33.vdi`（我留了默认值并使用了虚拟机名称）。16 `GB` 也足够运行 `Linux`，除非你向虚拟机拷贝了大量文件。文件大小会远小于 16`GB`。

`![](img/127a5ac6776c2933c37f7b2f9e005369_51_0)` 现在你应该回到 `Virtualbox` 的启动界面。如果一切顺利，你应该能在列表中看到刚刚创建的机器。

`![](img/127a5ac6776c2933c37f7b2f9e005369_51_1)` 完成设置后，我们进入虚拟机的 `Settings`（设置）并挂载之前下载的 `.iso` 文件。

`![](img/127a5ac6776c2933c37f7b2f9e005369_52_0)` 这是正确挂载 `.iso` 文件的截图。

`![](img/127a5ac6776c2933c37f7b2f9e005369_52_1)`

## 5.3. CentOS 7 安装

以下截图将展示从首次启动虚拟机（已挂载 `.iso` 文件）到首次登录的每一个步骤。

启动时你应该能看到这个，否则请检查之前步骤中 `.iso` 文件的挂载情况。选择“`Test this media and install CentOS 7`”安装 `CentOS 7`。

`![](img/127a5ac6776c2933c37f7b2f9e005369_53_0)`

### 安装 CentOS 7

仔细选择你希望 `CentOS` 使用的语言。尽管我的母语不是英语，但我总是使用英语安装操作系统。

同样选择正确的键盘，我用的是美式 `qwerty` 布局，但你的可能不同。

`![](img/127a5ac6776c2933c37f7b2f9e005369_54_0.png)`

你应该会到达一个摘要页面（带有一个或多个警告）。

`![](img/127a5ac6776c2933c37f7b2f9e005369_54_1.png)`

### 安装 CentOS 7

从配置网络开始。在演示期间，我在 `192.168.1.42` 运行着一个 `DHCP` 服务器，你的可能不同。如果此步失败，请向他人（网络管理员？）寻求帮助。

`![](img/127a5ac6776c2933c37f7b2f9e005369_55_0.png)`



选择你的时区，并激活`ntp`。

![](img/127a5ac6776c2933c37f7b2f9e005369_55_1.png)

## 安装 CentOS 7

选择一个离你最近的镜像源。如果你找不到本地镜像，可以从这张截图中复制（它是一个通用的`CentOS`镜像）。

![](img/127a5ac6776c2933c37f7b2f9e005369_56_0.png)

在验证镜像之前，可能需要几秒钟。

![](img/127a5ac6776c2933c37f7b2f9e005369_56_1.png)

### 我没有选择任何硬件（因为我想在本次培训中显示所有内容）

![](img/127a5ac6776c2933c37f7b2f9e005369_57_0.png)

在配置完网络、位置、软件等一切内容后，你应该回到此页面。确保没有警告（并且你在每个地方都做了正确的选择）。

![](img/127a5ac6776c2933c37f7b2f9e005369_57_1.png)

## 安装 CentOS 7

在安装程序从互联网下载时，你可以输入`root`密码并创建一个用户账户。这是最长的一步，可能需要几分钟（如果你的互联网连接慢，可能需要一个小时）。

![](img/127a5ac6776c2933c37f7b2f9e005369_58_0.png)

如果你看到这个，说明安装成功。

是时候重启电脑并首次启动`CentOS 7`了。

![](img/127a5ac6776c2933c37f7b2f9e005369_58_1.png)

当虚拟机启动时，此屏幕会短暂出现。你不需要做任何操作。

![](img/127a5ac6776c2933c37f7b2f9e005369_59_0.png)

几秒钟后，你应该看到登录屏幕。这被称为`tty`或`getty`。你可以输入`root`作为用户名。登录过程会要求输入密码（在输入密码时屏幕上不会显示任何内容）。

![](img/127a5ac6776c2933c37f7b2f9e005369_59_1.png)

## 安装 CentOS 7

登录后的样子就是这样。你已经登录了自己的`Linux`机器，非常好。

![](img/127a5ac6776c2933c37f7b2f9e005369_60_0.png)

后续所有的截图都将只有纯文本，不再有图像。

例如，这张截图显示在我新的`CentOS 7`上输入了三条命令。

```
[root@localhost ~]# who am i
root     pts/0         2014-11-01 22:14
[root@localhost ~]# hostname
localhost.localdomain
[root@localhost ~]# date
Sat Nov 1 22:14:37 CET 2014
```

使用`ssh`时，相同的命令将得到此截图：

```
[root@localhost ~]# who am i
root     pts/0         2014-11-01 21:00 (192.168.1.135)
[root@localhost ~]# hostname
localhost.localdomain
[root@localhost ~]# date
Sat Nov 1 22:10:04 CET 2014
```

如果最后一部分太快了，请先查看下一个主题：`CentOS 7`首次登录。

## 5.4. CentOS 7 首次登录

完成安装后，你只需要登录即可，这是`Virtualbox`中的屏幕。

![](img/127a5ac6776c2933c37f7b2f9e005369_61_0.png)

## 5.5. 网络界面

此屏幕将显示你的网络界面。默认情况下，`Virtualbox`通过`nat`连接。

![](img/127a5ac6776c2933c37f7b2f9e005369_62_0.png)

如果你想使用桥接或主机网络，必须更改`Virtualbox`中的设置。

```
[root@localhost ~]# ip addr
1: lo: <LOOPBACK,UP,LOWER> mtu 65536 
    inet 127.0.0.1/8 scope host lo
2: eth0: <BROADCAST,MULTICAST,LOWER> mtu 1500 
    link/ether 08:00:27:81:00:01
    inet 192.168.56.10/24 scope global eth0 192.168.56.255
```

## 5.6. 配置网络

为你的电脑上添加一个静态地址。

![](img/127a5ac6776c2933c37f7b2f9e005369_57_1.png)

## 5.7. 添加静态地址

此示例显示了如何为你的电脑添加静态`IP`。

| `IPv4` 配置 | <隐藏> |
| :--- | :--- |
| 地址 `104.33.32/16` | |

在此界面中，你希望使用静态`IP`而不是`DHCP`。

```
root@localhost ~]# nmui
```

`nmui`工具将允许你设置`IP`地址、网关和`DNS`。

### 5.4. 设置主机名

配置完网络、位置、软件等一切内容后，你应该回到此页面。确保没有警告（并且你在每个地方都做了正确的选择）。

`CentOS 7`

![](img/127a5ac6776c2933c37f7b2f9e005369_61_0.png)

---

### 5.8. 包管理

即使是网络安装，`CentOS 7`也没有安装某些软件包的最新版本。幸运的是，只需要运行一个命令（以`root`身份）。

```
[root@server ~]# yum update
```

你也可以使用`yum`安装一个或多个软件包。不要忘记定期运行`yum update`。

```
[root@server ~]# yum update -y && yum install vim -y
```

## 5.9. 从 Linux 和 MacOSX 登录

你可以在`Linux`或`MacOSX`上打开终端并使用`ssh`登录到你的虚拟机。

```
paul@debian:- $ ssh root@192.168.1.110
root@192.168.1.110: password:
Last login: Sun Nov 2 11:53:57 2014
[root@server33~]# hostname
server33.netsec.local
[root@server33~]#
```

## 5.10. 从 MS Windows 登录

`MS Windows`没有安装`ssh`，但你可以从`http://www.chiark.greenend.org/~sgtatham/putty/download.html`下载`putty.exe`（只需在谷歌搜索即可）。

像截图所示使用`putty.exe`（我通过给`IP`地址命名为`'server33'`并点击`'save'`保存了它）。

![](img/127a5ac6776c2933c37f7b2f9e005369_65_0.png)

## 安装 CentOS 7

第一次你会收到一条关于密钥的消息，接受它即可（这在`ssh`章节中会有解释）。

![](img/127a5ac6776c2933c37f7b2f9e005369_66_0.png)

输入你的用户名（或`root`）和正确的密码（输入密码时屏幕上不会显示任何字符）。

```
root@server33:- 
login as: root
troot192.168.1.110's password:
Last login: Sun Nov 2 12:07:49 2014 from 192.168.1.35
[root@server33]#
[root@server33]# hostname
server33.netsec.local
[root@server33 -]#
```

## 第 6 章 在家获取 Linux

本章展示了如何在`Virtualbox`中安装`Ubuntu`。请将其视为旧版本，并使用`CentOS7`或`Debian8`（它们现在都有各自的章节）。

本书假设你可以访问一台运行良好的`Linux`计算机。大多数公司都有一个或多个`Linux`服务器，如果你已经登录了它，那么你就没问题了（跳过本章并进入下一章）。

另一个选项是在带有（或没有）`Microsoft Windows`的电脑上插入`Ubuntu Linux` CD并按照说明进行安装。`Ubuntu`将调整（或创建）分区，并在启动时设置菜单以选择`Windows`或`Linux`。

如果你目前无法使用`Linux`电脑，且你无法或不确定是否要在电脑上安装`Linux`，那么本章提出了第三种选择：在虚拟机中安装`Linux`。

在虚拟机中（由`Virtualbox`提供）安装既简单又安全。即使你犯了错误并导致虚拟`Linux`机器崩溃，真实计算机上的任何内容也不会受到影响。



本章提供了简单的步骤和截图，帮助你在 `VirtualBox` 虚拟机中获得一个可运行的 `Ubuntu` 服务器。这些步骤与安装 `Fedora` 或 `CentOS` 甚至 `Debian` 非常相似，如果你愿意，也可以使用 `VMware` 代替 `VirtualBox`。

## 6.1. 下载 Linux CD 镜像

首先从互联网上你选择的发行版下载 Linux CD 镜像（`.ISO` 文件）。请注意选择你电脑的 CPU 架构；如果不确定，请选择 `i386`。选择错误的 CPU 类型（例如，在你使用旧款 `Pentium` 时选择了 `x86_64`）将导致 CD 无法启动。

![](img/127a5ac6776c2933c37f7b2f9e005369_68_0.png)

## 下载 Ubuntu Server

你现在可以下载 `Ubuntu Server` 了它是完全免费的。

![](img/127a5ac6776c2933c37f7b2f9e005369_68_1.png)

## 6.2. 下载 VirtualBox

第二步（`ISO` 文件下载完成后）是下载 `VirtualBox`。如果你正在运行 `Microsoft Windows`，请下载并安装 Windows 版 `VirtualBox`！

![](img/127a5ac6776c2933c37f7b2f9e005369_68_2.png)

在这里，你会找到 `VirtualBox` 二进制文件及其源代码的链接。

### VirtualBox 二进制文件

通过下载，你同意软件包的条款和条件。二进制文件发布于：

- `VirtualBox` `4.1.8` for `Windows` hosts `x86`/`amd64`
- `VirtualBox` `4.1.8` for `OS X` `x86`/`amd64`
- `VirtualBox` `4.1.8` for `Linux` hosts
- `VirtualBox` `4.1.8` for `Solaris` hosts `x86`/`amd64`

## 6.3. 创建虚拟机

现在启动 `VirtualBox`。与下面的截图相反，你的左侧面板应该是空的。

![](img/127a5ac6776c2933c37f7b2f9e005369_69_0.png)

点击 `New` 创建一个新的虚拟机。我们将一起通过向导。下面的截图是在 `Mac OSX` 上拍摄的；如果你运行的是 `Microsoft Windows`，它们会有所不同。

![](img/127a5ac6776c2933c37f7b2f9e005369_69_1.png)

### Name

为你的虚拟机（并可能选择 32 位或 64 位）。

![](img/127a5ac6776c2933c37f7b2f9e005369_70_0.png)

给虚拟机一些内存（如果你有 `2GB` 或更多，给 `512MB`；否则选择 `256MB`）。

![](img/127a5ac6776c2933c37f7b2f9e005369_70_1.png)

### Disk

选择创建新磁盘（记住，这将虚拟磁盘）。

![](img/127a5ac6776c2933c37f7b2f9e005369_71_0.png)

如果出现下面的问题，选择 `vdi`。

![](img/127a5ac6776c2933c37f7b2f9e005369_71_1.png)

磁盘大小选择 `10GB` 和 `16GB` 之间。

![](img/127a5ac6776c2933c37f7b2f9e005369_72_0.png)

点击创建虚拟磁盘。

![](img/127a5ac6776c2933c37f7b2f9e005369_73_0.png)

点击创建虚拟机。

![](img/127a5ac6776c2933c37f7b2f9e005369_73_1.png)

## 6.4. 挂载 CD 镜像

在我们启动虚拟机之前，让我们查看一些设置（点击 `Settings`）。

![](img/127a5ac6776c2933c37f7b2f9e005369_74_0.png)

如果你的界面看起来不同，找到名为 `storage` 的按钮即可。

![](img/127a5ac6776c2933c37f7b2f9e005369_74_1.png)

记得你下载的 `.ISO` 文件吗？点击 `Empty` 旁的 CD 图标将此 `.ISO` 文件连接到此虚拟机。

![](img/127a5ac6776c2933c37f7b2f9e005369_75_0.png)

现在点击另一个 CD 图标并将 `ISO` 文件挂载到此虚拟驱动器。

![](img/127a5ac6776c2933c37f7b2f9e005369_75_1.png)

验证你的下载已被接受。如果 `VirtualBox` 在此点报错，你可能没有完成 CD 的下载。

![](img/127a5ac6776c2933c37f7b2f9e005369_76_0.png)

将网络适配设置为桥接（`bridge`）而不是 `NAT` 可能很有用。桥接通常能让你的虚拟机连接到互联网。

![](img/127a5ac6776c2933c37f7b2f9e005369_76_1.png)

## 6.5. 安装 Linux

虚拟机现在准备就绪了。在启动时给出选择，选择 `install` 并按照屏幕上的指令操作。安装完成后，你就可以登录机器并开始练习 `Linux` 了！

# 第三部分 命令行的第一步

## 目录

- 7. `man` 页面 ............................................................ 71
- 7.1. `man $command` ................................................ 72
- 7.2. `man configfile` ................................................ 72
- 7.3. `man $daemon` ................................................................. 72
- 7.4. `man -k (apropos)` ................................................ 72
- 7.5. `whatis` ........................................................ 72
- 7.6. `whereis` ................................................................ 73
- 7.7. `man sections` ............................................... 73
- 7.8. `man $section file` ................................................ 73
- 7.9. `man man` ................................................................ 73
- 7.10. `mandb` ................................................................ 73
- 8. 操作目录 ................................................. 74
- 8.1. `pwd` ................................................................................. 75
- 8.2. `cd` ................................................................................. 75
- 8.3. 绝对路径和相对路径 ................................................. 76
- 8.4. 路径补全 ................................................ 77
- 8.5. `is` ................................................................................. 77
- 8.6. `mkdir` ................................................................ 79
- 8.7. `rmdir` ................................................................ 79
- 8.8. 练习：操作目录 ............................... 81
- 8.9. 答案：操作目录 ............................... 82



# 第 9 章 操作文件
9. 操作文件 . . . . . . . . . . . . . . . . . . . . . . . . . . . . 84
- 9.1. 所有文件都是 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 85
- 9.2. 一切都是文件 . . . . . . . . . . . . . . . . . . . . . . . . . . . 85
- 9.3. 文件 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 85
- 9.4. `touch` . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 86
- 9.5. `rm` . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 87
- 9.6. `cp` . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 88
- 9.7. `mv` . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 89
- 9.8. `rename` . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 90
- 9.9. 练习：操作文件 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 91
- 9.10. 答案：操作文件 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 92

# 第 10 章 查看文件内容
10. 查看文件内容 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 94
- 10.1. `head` . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 95
- 10.2. `tail` . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 95
- 10.3. `cat` . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 96
- 10.4. `tac` . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 97
- 10.5. `more` and `less` . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 98
- 10.6. `strings` . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 99
- 10.7. 练习：查看文件内容 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 99
- 10.8. 答案：查看文件内容 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 100

# 第 11 章 Linux 文件树
11. `Linux` 文件树 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 101
- 11.1. 文件系统层次结构 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 102
- 11.2. `man hier` . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 102
- 11.3. 根目录 `/` . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 102
- 11.4. 二进制目录 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 103
- 11.5. 配置目录 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 105
- 11.6. 数据目录 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 107
- 11.7. 内存中目录 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 109
- 11.8. `usr` Unix 系统资源 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 114
- 11.9. `var` 变量数据 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 116
- 11.10. 练习：文件系统树 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 118
- 11.11. 答案：文件系统树 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 120

# 第 7 章 man pages（帮助页）

本章将解释 `Unix` 或 `Linux` 计算机上 `man` `pages`（也称为手册页）的使用。

你将学习`man`命令以及相关的命令，如`whereis`、`whatis`和`mandb`。

大多数 `Unix` 文件和命令都有非常完善的 `man` `pages`来解释它们的用法。当你使用多个版本的 `Unix` 或多个 `Linux` 发行版时，由于选项和参数有时会有不同，`man` `pages` 也会变得非常有用。

## 7.1. `man` `$command`

输入`man`后紧跟一个命令（你想要获取帮助的命令）并开始阅读。按`q`退出 `man` `page`。某些 `man` `pages` 包含示例（在末尾）。

```
paul@laika~$ man whois
Reformatting whois(1), please wait...
```

## 7.2. `man` `$configfile`

某些配置文件（`configuration` `files`）有它们自己的手册。

```
paul@laika:~$ man syslog.conf
Reformatting syslog.conf(5), please wait...
```

## 7.3. `man` `$daemon`

对于你系统上的大多数守护进程（`daemons`，后台程序）也是如此。

```
paul@laika:~$ man syslogd
Reformatting syslogd(8), please wait...
```

## 7.4. `man` `-k` (`apropos`)

`man -k` (`apropos`) 会显示包含特定字符串的 `man` `pages` 列表。

```
paul@laika:~$ man -k syslog
im-syslog-setup (8) - configure laptop mode to syslog.conf ...
logger (1) - shell command interface to the syslog(3) ...
syslog-facility (8) - Setup and remove LOCALX facility for syslogd
syslog.conf (5) - syslogd(8) configuration file
syslog (8) - Linux system logging utilities.
syslog-listfiles (8) - list system logfiles
```

## 7.5. `whatis`

若只想查看 `man` `page` 的描述，使用`whatis`后紧跟一个字符串。

```
paul@u810:~$ whatis route
route (8) - manipulate the IP routing table
```

## 7.6. `whereis`

可以使用`whereis`显示 `man` `page` 的位置。

```
paul@laika:~$ whereis -m whois
whois: /usr/share/man/man1/whois.gz
```

该文件可以直接被`man`读取。

```
paul@laika:~$ man /usr/share/man/man1/whois.gz
```

## 7.7. `man` `sections`

此时你已经注意到圆括号之间的数字了。`man` 会向你解释这些是章节。可执行程序和 `shell` 命令位于第一部分。

- 1: 可执行程序或 `shell` 命令
- 2: 系统调用（内核提供的函数）
- 3: 库调用（程序库中的函数）
- 4: 特殊文件（通常位于`/dev`中）
- 5: 文件格式和约定`/etc/passwd`
- 6: 游戏
- 7: 杂项（包括宏包和约定），例如`man(7)`
- 8: 系统管理命令（通常仅限 `root` 用户）
- 9: 内核例程 [非标准]

## 7.8. `man` `$file`

因此，当你引用命令的 `man` `page` 时，你会看到写成`passwd(1)`；如果是指`passwd`文件，你会看到`passwd(5)`。截图解释了如何在正确的章节中打开 `man` `page`。



```
paul@RHEL52 ~~$ man password          # 打开找到的第一个
paul@RHEL52 ~~$ man 5 password          # 打开第 5 部分的页面
```

## 7.9. man db

如果你想了解更多关于 `man` 的信息，请阅读《终极手册》（The Fantastic Manual, RTFM）。

遗憾的是，手册页并没有无万能的答案……

```
paul@laika:~$ man woman
No manual entry for woman
```

## 7.10. mandb

如果你确信 `man page` 存在但无法访问它，可以尝试在 Debian/Mint 上运行 `mandb`。

```
root@laika:~# mandb
0 man subdirectories contained newer man pages.
0 manual pages were added.
0 stray cats were added.
0 old database entries were purged.
```

或者在 CentOS/Redhat 上运行 `makewhat`。

```
[root@centos65 ~#] apropos scsi
scsi: nothing
[root@centos65 ~#] apropos scsi
h (4) Smart Array
l (8) list SCSI devices (or hosts) and their attributes
d (4) Driver for SCSI Drives
sd (4) SCSI tape device
```

# 第 8 章 目录操作

本模块是对处理目录常用命令的简要概述：`pwd`、`cd`、`ls`、`mkdir` 和 `rmd`。这些命令在任何 Linux（或 Unix）系统上可用。本模块还讨论了绝对路径、相对路径以及 `bash` shell 中的路径自动补全。

## 8.1. pwd

可以使用 `pwd` 命令（打印目录）显示“你在这里”。试试看：打开一个命令行界面（也称为终端、控制或 xterm）并输入 `pwd`。该工具会显示你当前的目录。

```
paul@debian:~$ pwd
/home/paul
```

## 8.2. cd

你可以使用 `cd` 命令（切换目录）更改当前目录。

```
paul@debian:~$ cd /etc
paul@debian:~$ pwd
/etc
paul@debian:~$ cd /bin
paul@debian:~$ pwd
/bin
```

## 8.3. cd ~

可以使用 `cd ~` 命令切换到家目录。

```
paul@debian:~$ cd ~
paul@debian:~$ pwd
/home/paul
```

## 8.4. cd /

可以使用 `cd /` 命令切换到根目录。

```
paul@debian:~$ cd /
paul@debian:~$ pwd
/
```

## 8.5. cd .. (返回)

可以使用 `cd ..` 命令返回上级目录。

```
paul@debian:~$ cd ..
paul@debian:~$ pwd
/home
```

## 8.6. cd -

可以使用 `cd -` 命令切换到上一个目录。

```
paul@debian:~$ cd -
paul@debian:~$ pwd
/etc
```

## 8.7. pwd (绝对路径)

可以使用 `pwd` 命令显示你所在的绝对路径。

```
paul@debian:~$ cd /etc
paul@debian:~$ pwd
/etc
```

## 8.8. 相对路径 (相对路径)

```
paul@debian:~$ cd ..
paul@debian:~$ pwd
/home
```

## 8.9. ls (列出目录)

可以使用 `ls` 命令查看目录内容。

```
paul@debian:~$ ls
```

## 8.10. mkdir (创建目录)

可以使用 `mkdir` 命令创建新目录。

```
paul@debian:~$ mkdir testdir
```

## 8.11. rmdir (删除目录)

可以使用 `rmdir` 命令删除空目录。

```
paul@debian:~$ rmdir testdir
```

### 8.5.3. ls -lh

另一个常用的选项 `ls -h`。它以更易于人类阅读的格式显示数字（文件大小）。下面还展示了向 `ls` 提供选项的一些不同方式。我们将在本书的后部分解释输出的详细信息。

注意，我们在截图未使用字母 `L` 作为选项，而不是数字 `1`。

```
paul@debian:~$ ls -l -nhntotal 17M
-rw-r--r 1 paul 17M Sep 17 00:03 allfiles.txt
-rw-r--r 1 paul 95K Sep 17 00:03 dmesg.txt
-rw-r--r 1 paul 20K Sep 17 00:04 services
drwxr-xr-x 2 paul 4.0K Sep 17 00:04 stuff
-rw-r--r 1 paul 0 Sep 17 00:04 summer.txt
paul@debian:~$ ls -l -lh
total 17M
-rw-r--r 1 paul 17M Sep 17 00:03 allfiles.txt
-rw-r--r 1 paul 95K Sep 17 00:03 dmesg.txt
-rw-r--r 1 paul 20K Sep 17 00:04 services
drwxr-xr-x 2 paul 4.0K Sep 17 00:04 stuff
-rw-r--r 1 paul 0 Sep 17 00:04 summer.txt
paul@debian:~$ ls -l -1
total 17M
-rw-r--r 1 paul 17M Sep 17 00:03 allfiles.txt
-rw-r--r 1 paul 95K Sep 17 00:03 dmesg.txt
-rw-r--r 1 paul 20K Sep 17 00:04 services
drwxr-xr-x 2 paul 4.0K Sep 17 00:04 stuff
-rw-r--r 1 paul 0 Sep 17 00:04 summer.txt
paul@debian:~$
```

### 8.6. mkdir

在 Unix 树中漫游很有趣，但使用 `mkdir` 创建自己的目录更有趣。你必须给 `mkdir` 至少提供一个参数，即要创建的新目录名称。在输入开头的 `/` 之前请思考一下。

```
paul@debian:-$ mkdir mydir
paul@debian:~$ cd mydir
paul@debian:~/mydir ls -l
total 8
drwxr-xr-x 2 paul 4096 Sep 17 00:07
drwxr-xr-x 4 paul 4096 Sep 17 00:07 ..
paul@debian:~/mydir mkdir stuff
paul@debian:~/mydir otherstuff
paul@debian:~/mydir ls -l
total 8
drwxr-xr-x 2 paul 4096 Sep 17 00:07 otherstuff
drwxr-xr-x 2 paul 4096 Sep 17 00:07 stuff
paul@debian:~/mydir$ 
```

### 8.6.1 mkdir -p

该命令将失败，因为 `threirsdeep` 的父目录不存在。

```
paul@debian:-$ mkdir mydir2/mysubdir2/threedirsdeep
mkdir: cannot create directory 'mydir2/mysubdir2/threedirsdeep': No such file
or or directory
```

当给出选项 `-p` 时，`mkdir` 将根据需要创建父目录。



```
paul@debian:-$ mkdir -p mydir2/mysubdir2/threedirsdeep
paul@debian:~$ cd mydir2
paul@debian:~/mydir2 ls -l
total 4
drwxr-xr-x 2 paul 4096 Sep 17 00:11 mydir2
paul@debian:~/mydir2 cd mysubdir
paul@debian:~/mydir2/mysubdir2 ls -l
total 4
drwxr-xr-x 2 paul 4096 Sep 17 00:11 threedirsdeep
paul@debian:~/mysubdir$ cd threedirsdeep/
paul@debian:~/mysubdir/threedirsdeep$ pwd
/home/paul/mydir2/mysubdir2/threedirsdeep$
```

### 8.7. `rmdir`

当目录为空时，你可以使用 `rmdir` 删除该目录。

```
paul@debian:-$ ls -l
total 8
drwxr-xr-x 2 paul 4096 Sep 17 00:08 otherstuff
drwxr-xr-x 2 paul 4096 Sep 17 00:08 stuff
paul@debian:~/mydir rmdir otherstuff
paul@debian:~/mydir$ cd ..
paul@debian$ rmdir mydir
mdir: failed to remove 'mydir': Directory not empty
paul@debian:~$ rmdir mydir/stuff
paul@debian:~$ rmdir mydir
paul@debian:-$
```

#### 8.7.1 `rmdir -p`

与 `mkdir -p` 类似，你也可以使用 `rmdir` 递归删除目录。

```
paul@debian:~$ mkdir -p testdir/subdir
paul@debian:~$ rmdir -p testdir/subdir
paul@debian:~$
```

## 8.8. ：目录操作

1. 显示当前目录。
2. 进入 `/etc` 目录。
3. 现在使用三个键切换到家目录。
4. 使用十一个键切换到 `/boot/grub` 目录。
5. 进入当前目录的父目录。
6. 进入根目录。
7. 列出根目录的内容。
8. 列出根目录的详情。
9. 留在此处并列出 `/etc` 的内容。
10. 留在此处并列出 `/bin/sbin` 的内容。
11. 留在此处并列出 `~` 的内容。
12. 列出家目录中的所有文件（包括隐藏文件）。
13. 以易读格式列出 `/boot` 中的文件。
14. 在家目录中创建一个 `testdir` 目录。
15. 进入 `/etc` 目录，在此处并在家目录中创建一个 `newdir` 目录。
16. 使用一个命令创建 `~/dir1/dir2/dir3` 目录（`dir3` 是 `dir2` 的子目录，`dir2` 是 `dir1` 的子目录）。
17. 删除 `testdir` 目录。
18. 如果时间允许（或者你在等待其他学生完成练习），使用并理解 `pushd` 和 `popd`。使用 `bash` 的 man 页查找这些命令的信息。

## 8.9. 答案：目录操作

1. 显示当前目录。

```
pwd
```

2. 进入 `/etc` 目录。

```
cd /etc
```

3. 现在使用三个键切换到家目录。

```
cd .. (按回车键)
```

4. 使用十一个键切换到 `/boot/grub` 目录。

```
cd /boot/grub (使用 Tab 键)
```

5. 进入当前目录的父目录。

```
cd .. (在 cd 和 .. 之间加空格)
```

6. 进入根目录。

```
cd /
```

7. 列出根目录的内容。

```
ls
```

8. 列出根目录的详情。

```
ls -l
```

9. 留在此处并列出 `/etc` 的内容。

```
ls /etc
```

10. 留在此处并列出 `/bin/sbin` 的内容。

```
ls /bin/sbin
```

11. 留在此处并列出 `~` 的内容。

```
ls ~
```

12. 列出家目录中的所有文件（包括隐藏文件）。

```
ls -al ~
```

13. 以易读格式列出 `/boot` 中的文件。

```
ls -lh /boot
```

14. 在家目录中创建一个 `testdir` 目录。

```
mkdir ~/testdir
```

15. 进入 `/etc` 目录，在此处并在家目录中创建一个 `newdir` 目录。

```
cd /etc ; mkdir ~/newdir
```

16. 使用一个命令创建 `~/dir1/dir2/dir3` 目录。

```
mkdir -p ~/dir1/dir2/dir3
```

17. 删除 `testdir` 目录。

```
rmdir testdir
```

18. 如果时间允许（或者你在等待其他学生完成练习），使用并理解 `pushd` 和 `popd`。使用 `bash` 的 man 页查找这些命令。

```
man bash # 打开手册
pushd # 搜索 pushd
n # 下一个（执行两次或三次）
```

`Bash` Shell 有两个内置命令 `pushd` 和 `popd`。这两个命令都作用于一个公共的历史目录栈。`pushd` 将目录加入栈并切换到新目录，`popd` 从栈中移除一个目录并设置当前目录。

```
paul@debian7:/etc$ cd /bin
paul@debian7:/bin$ pushd /lib
lib /bin
paul@debian7:/lib$ pushd /proc
proc /lib /bin
paul@debian7:/proc$ popd
lib /bin
paul@debian7:/$ popd
/bin
```

# 第 9 章：文件操作

在本章中，我们学习如何使用 `file`、`touch`、`rm`、`cp`、`mv` 和 `rename` 等命令来识别、创建、删除、拷贝和移动文件。

## 9.1. 所有文件对大小敏感

`Linux`（或任何 `Unix`）上的文件是对大小敏感的。这意味着 `FILE1` 与 `file1` 不同，`/etc/hosts` 与 `/etc/Hosts` 不同（后者在典型的 `Linux` 上不存在）。

此截图显示两个文件之间的区别，一个是大写的 `W`，另一个是小写的 `w`。

```
paul@laika:~/Linux$ ls
winter.txt Winter.txt
paul@laika:~/Linux$ cat Winter.txt
It is cold.
paul@laika:~/Linux$ cat Winter.txt
it is very cold!
```

## 9.2. 万物皆文件

目录是一种特殊的文件，但它仍然是一个文件（且大小敏感）。每个终端窗口（例如 `/dev/pts/4`）、任何硬盘或分区（例如 `/dev/sdb1`）以及任何进程都在系统中以文件的形式表示。在整个课程中，你会发现 `Linux` 上的一切都是文件。

## 9.3. `file`

`file` 工具确定文件类型。`Linux` 不使用扩展名来确定文件类型。该命令不关心文件是以 `.txt` 还是 `.pdf` 结尾。作为系统管理员，你应该使用该命令确定文件类型。以下是典型 `Linux` 系统上的示例。

```
paul@laika:-$ file pic33.png
pic33.png: PNG image data, 3840 x 1200, 8-bit/color RGBA, non-interlaced
paul@laika:-$ file /etc/passwd
/etc/passwd: ASCII text
paul@laika:-$ file HelloWorld.c
HelloWorld.c: ASCII C++ program text
```

`file` 命令使用包含模式的魔法文件来识别文件类型。魔法文件位于 `/usr/share/file/magic`。对于 `/dev` 和 `/proc` 中的内容，请参考 `man 5`。

对于 `/dev` 和 `/proc` 中的特殊文件使用 `-s` 参数很有趣。



```
root@debian6-## file /dev/sda
/dev/sda: block special
root@debian6-## file -s /dev/sda
/dev/sda: boot sector, partition 1: ID=0x83, active,starthead...
root@debian6-## /proc/cpuinfo
/proc/cpuinfo: empty
root@debian6-## file -s /proc/cpuinfo
/proc/cpuinfo: ASCII C++ program text
```

## 9.4. touch

### 9.4.1. 创建空文件

创建一个空文件的一种简单方法是使用`touch`。（我们将在本书的后部分看到许多其他创建文件的方法。）

这张截图从一个空目录开始，使用`touch`创建了两个文件并列出了这些文件。

```
paul@debian:~$ ls -1
total 0
paul@debian:~$ touch file42
paul@debian:~$ touch file33
paul@debian:~$ ls -1
total 0
-rw-r--r-- 1 paul paul 0 Oct 15 08:57 file33
-rw-r--r-- 1 paul paul 0 Oct 15 08:56 file42
paul@debian:-$
```

### 9.4.2. touch -t

`touch`命令可以在创建空文件时设置某些属性。你能通过观察下面的截图判断出设置了什么吗？如果不能，请查看`touch`的手册。

```
paul@debian:~$ touch -t 200505050000 SinkoDeMayo
paul@debian:~$ touch -t 130207111630 BigBattle.txt
paul@debian:~$ ls -1
total 0
-rw-r--r-- 1 paul paul 0 Jul 11 1302 BigBattle.txt
-rw-r--r-- 1 paul paul 0 Oct 15 08:57 file33
-rw-r--r-- 1 paul paul 0 Oct 15 08:56 file42
-rw-r--r-- 1 paul paul 0 May 5 2005 SinkoDeMayo
paul@debian:-$
```

## 9.5. rm

### 9.5.1. 永久删除

当你不再需要某个文件时，使用`rm`删除它。与某些图形用户界面不同，命令行通常没有回收站或垃圾桶可以恢复文件。当你使用`rm`删除一个文件时，它就消失了。因此，删除文件时要小心！

```
paul@debian?:-$ ls
BigBattle.txt file33 file42 SinkoDeMayo
paul@debian?:-$ rm BigBattle.txt
paul@debian?:-$ ls
file33 file42 SinkoDeMayo
paul@debian?:-$
```

### 9.5.2. rm -i

为了防止误删文件，你可以输入`rm -i`。

```
paul@debian?:-$ ls
file33 file42 SinkoDeMayo
paul@debian?:-$ rm -i file33
rm: remove regular empty file `file33'? yes
paul@debian?:-$ rm -i SinkoDeMayo
rm: remove regular empty file `SinkoDeMayo`? n
paul@debian?:-$ ls
file42 SinkoDeMayo
paul@debian?:-$
```

### 9.5.3. rm -rf

默认情况下，`rm -r`不删除非空目录。然而，`rm`接受允许你删除任何目录的选项。`rm -rf`语句非常有名，因为它会擦除任何内容（只要你有权限这样做）。当你以`root`身份登录时，要非常小心使用`rm -rf`（`f`表示强制，`r`表示递归），因为`root`意味着权限限制对你不适用。你可以通过命令擦除整个文件系统。

```
paul@debian?:-$ mkdir test
paul@debian?:-$ rm test
rm: cannot remove 'test': Is a directory
paul@debian?:-$ rm -rf test
paul@debian?:-$ ls
is: cannot access test: No such file or directory
paul@debian?:$
```

## 9.6. cp

### 9.6.1. 复制文件

要复制文件，请使用`cp`并指定源目标参数。

```
paul@debian:~$ ls
file42 SinkoDemayo
paul@debian:~$ cp file42 file42.copy
paul@debian:~$ ls
file42 file42.copy SinkoDemayo
```

### 9.6.2. 复制到另一个目录

如果目标是一个目录，则源文件将被复制到该目标目录。

```
paul@debian:~$ mkdir dir42
paul@debian:~$ cp SinkoDemayo dir42
paul@debian:~$ ls dir42
SinkoDemayo
```

### 9.6.3. cp -r

要复制整个目录，请使用`cp -r`（`-r`选项用于递归复制子目录中的所有文件）。

```
paul@debian:~$ ls
dir42 file42.copy SinkoDemayo
paul@debian:~$ cp -r dir42/dir33
paul@debian:~$ ls
dir33 file42 file42.copy SinkoDemayo
SinkoDemayo
```

### 9.6.4. 将多个文件复制到目录

你可以使用`cp`将多个文件复制到目录。在这种情况下，最后一个参数（即目标）必须是一个目录。

```
paul@debian:~$ cp file42 file42.copy SinkoDemayo dir42/
paul@debian:~$ ls dir42/
file42 file42.copy SinkoDemayo
```

### 9.6.5. cp -i

为了防止覆盖现有文件，请使用`-i`（交互式）。

```
paul@debian:~$ cp SinkoDemayo file42
paul@debian:~$ cp SinkoDemayo file42
paul@debian:~$ cp -i SinkoDemayo file42
cp: overwrite `file42`? n
paul@debian:~$
```

## 9.7. mv

### 9.7.1. 重命名文件

使用`mv`重命名文件或将文件移动到另一个目录。

```
paul@debian:~$ ls
dir33 file42.copy SinkoDeMayo
paul@debian:~$ mv file42 file33
paul@debian:~$ ls
dir33 file42.copy SinkoDeMayo
paul@debian:~$
```

当你只需要重命名一个文件时，`mv`是首选命令

### 9.7.2. 重命名目录

`mv`命令可以用于重命名目录。

```
paul@debian:~$ ls -l
total 8
drwxr-xr-x 2 paul paul 4096 Oct 15 09:36 dir33
drwxr-xr-x 2 paul paul 4096 Oct 15 09:36 dir42
-rw-r--r-- 1 paul paul 0 Oct 15 09:38 file33
-rw-r--r-- 1 paul paul 0 Oct 15 09:16 file42.copy
-rw-r--r-- 1 paul paul 0 May 5 2005 SinkoDeMayo
paul@debian:~$ mv dir33 backup
```

### 9.7.3. mv -i

这张截图显示`mv -i`会询问是否覆盖现有文件。

```
paul@debian:~$ mv -i file33 SinkoDeMayo
mv: overwrite 'SinkoDeMayo'? no
paul@debian:~$
```

## 9.8. rename

### 9.8.1. 关于 rename

`rename`命令是 Linux 基础需要区分 Linux 发行版的少数情况之一。书中基础部分的几乎每个命令在大多数 Linux 计算机上运行。但`rename`不同。

当你需要重命名多个文件时，尝试使用`mv`。

### 9.8.2. Debian/Ubuntu 上的 rename



Debian 上的 `rename` 命令使用正则表达式（正则表达式或 sh regex 将在后续章节解释）来批量重命名文件。下面的 `rename` 将 `.txt` 结尾的文件名的所有 `txt` 替换为 `png`。

```
paul@debian7:~/test42$ ls
abc.txt file33.txt file42.txt
paul@debian7:~/test42$ rename 's/.txt/.png/' *.txt
paul@debian7:~/test42$ ls
abc.png file33.png file42.png
```

第二个示例将 `.png` 结尾的文件名的（第一个）`file` 替换为 `document`。

```
paul@debian7:~/test42$ ls
abc.png file33.png file42.png
paul@debian7:~/test42$ rename 's/.file/document/' *.png
paul@debian7:~/test42$ ls
abc.png document33.png document42.png
paul@debian7:~/test42$
```

### 9.8.3. CentOS/RHEL/Fedora 上的 rename

在 Red Hat Linux 上，`conf` 的语法略有不同。下面的第一个示例重命名 `*.conf`，将任何 `.conf` 替换为 `.backup`。

```
[paul@centos7 ~]$ touch one.conf two.conf three.conf
[paul@centos7 ~]$ rename .conf .backup *.conf
[paul@centos7 ~]$ ls
one.backup three.backup two.backup
[paul@centos7 ~]$
```

第二个示例重命名所有（`*`）文件，将 `one` 替换为 `ONE`。

```
[paul@centos7 ~]$ ls
one.backup three.backup two.backup
[paul@centos7 ~]$ rename one ONE *
[paul@centos7 ~]$ ls
ONE.backup three.backup two.backup
[paul@centos7 ~]$
```

## 9.9. 练习：处理文件

- 1. 列出 `/bin` 目录下的文件
- 2. 显示文件 `/bin/cat`、`/etc/passwd` 和 `/usr/bin/passwd` 类型
- 3a. 从 `http://linux-training.be` 下载 `wolf.jpg` 和 `LinuxFun.pdf` (`wget http://linux-training.be/files/studentfiles/wolf.jpg` 和 `wget http://linux-training.be/files/books/LinuxFun.pdf`)
- 3b. 显示 `wolf.jpg` 和 `LinuxFun.pdf` 的文件类型
- 3c. 将 `wolf.jpg` 重命名为 `wolf.pdf` (使用 `mv`)
- 3d. 显示 `wolf.pdf` 和 `LinuxFun.pdf` 的文件类型

## 9.10. 解决方案：文件操作

1. 列出 `/bin` 目录下的文件

```
ls /bin
```

2. 显示 `/bin/cat`、`/etc/passwd` 和 `/usr/bin/passwd` 的文件类型。

```
file /bin/cat /etc/passwd /usr/bin/passwd
```

3a. 从 `http://linux-training.be` 下载 `wolf.jpg` 和 `LinuxFun.pdf`（使用 `wget http://linux-training.be/files/studentfiles/wolf.jpg` 和 `wget http://linux-training.be/files/books/LinuxFun.pdf`）

```
wget http://linux-training.be/files/studentfiles/wolf.jpg
wget http://linux-training.be/files/studentfiles/wolf.png
wget http://linux-training.be/files/books/LinuxFun.pdf
```

3b. 显示 `wolf.jpg` 和 `LinuxFun.pdf` 的文件类型。

```
file wolf.jpg LinuxFun.pdf
```

3c. 将 `wolf.jpg` 重命名为 `wolf.pdf`（使用 `mv`）。

```
mv wolf.jpg wolf.pdf
```

4. 显示 `wolf.pdf` 和 `LinuxFun.pdf` 的文件类型。

```
file wolf.pdf LinuxFun.pdf
```

5. 创建目录 `~touched` 并进入该目录。

```
mkdir ~touched ; cd ~touched
```

6. 在 `touched` 中创建文件 `today.txt` 和 `yesterday.txt`。

```
touch today.txt yesterday.txt
```

7. 将 `yesterday.txt` 的日期修改为昨天的日期（将 `20081025` 替换为昨天）

```
touch -t 200810251400 yesterday.txt
```

8. 将 `yesterday.txt` 复制到 `copy.yesterday.txt`

```
cp yesterday.txt copy.yesterday.txt
```

9. 将 `copy.yesterday.txt` 重命名为 `kim`

```
mv copy.yesterday.txt kim
```

10. 创建一个名为 `~testbackup` 的目录并将 `~touched` 中的所有文件复制到该目录中。

```
mkdir ~/testbackup ; cp -r ~touched ~/testbackup/
```

11. 使用 `rm` 删除 `~testbackup` 目录及其其中的所有文件。

```
rm -rf ~/testbackup
```

12. 创建目录 `~etcbackup` 并将 `/etc` 中所有的 `*.conf` 文件复制到该目录中。你包含 `/etc` 的所有子目录了吗？

```
cp -r /etc/*.conf ~/etcbackup
```

只有直接位于 `/etc/` 下的 `*.conf` 文件会被复制。

- 12. 使用 `rename` 将所有的 `*.conf` 文件重命名为 `*.backup`。（如果你有多个发行版可用，请在所有发行版上尝试！）

在 RHEL 上：`touch 1.conf 2.conf ; rename conf backup *.conf`

在 Debian 上：`touch 1.conf 2.conf ; rename 's/conf/backup/' *.conf`

# 第 10 章 文件内容操作

在本章中，我们将使用 `head`、`tail`、`tac`、`cat`、`more`、`less` 和 `strings` 命令查看文本文件的内容。

我们还将领略命令行上 `cat` 等工具的可能性。

## 10.1. head

你可以使用 `head` 来显示文件的前十行。

```
paul@debian7~$ head /etc/passwd
root:x:0:0:root:/root:/bin/bash
demon:x:1:1:daemon:/usr/sbin:/bin/sh
bin:x:2:2:bin:/bin:/sh
sys:x:3:3:sys:/dev:/sh
sync:x:4:65534:sync:/bin:/sync
games:x:5:60:game:/usr/bin:/sh
man:x:6:12:man:/var/cache/man:/bin/sh
lp:x:7:7:lp:/var/spool/lpd:/bin/sh
mail:x:8:8:mail:/var/mail:/bin/sh
news:x:9:news:/var/spool:/bin/sh
root@debian7~$
```

`head` 命令也可以显示文件的前 `n` 行。

```
paul@debian7~$ head -4 /etc/passwd
root:x:0:0:root:/root:/bin/bash
demon:x:1:1:daemon:/usr/sbin:/bin/sh
bin:x:2:2:bin:/bin:/sh
sys:x:3:3:sys:/dev:/sh
paul@debian7~$
```

并且 `head` 还可以显示前 `n` 字节。

```
paul@debian7~$ head -c14 /etc/passwd
root:x:0:0:roopaul@debian7~$
```

## 10.2. tail

与 `head` 类似，`tail` 命令将显示文件的最后几行。



## 10.2. tail

与 `head` 类似，`tail` 命令将显示文件的最后几行。

```
paul@debian7~$ tail /etc/services
vboxd      20012/udp
binkp       24554/tcp
asp          27374/tcp
ast          27374/udp
csync2      30865/tcp
dircproc     57000/tcp
ffidos       60177/tcp
fido        60179/tcp
paul@debian7~$
```

你可以使用 `tail -n` 指定你想看到的行数。

```
paul@debian7~$ tail -3 /etc/services
fido        60179/tcp
paul@debian7~$
```

## 9.10. 解决方案：文件操作

1. 列出 `/bin` 目录下的文件

```
ls /bin
```

2. 显示 `/bin/cat`、`/etc/passwd` 和 `/usr/bin/passwd` 的文件类型。

```
file /bin/cat /etc/passwd /usr/bin/passwd
```

3a. 从 `http://linux-training.be` 下载 `wolf.jpg` 和 `LinuxFun.pdf`（使用 `wget http://linux-training.be/files/studentfiles/wolf.jpg` 和 `wget http://linux-training.be/files/books/LinuxFun.pdf`）

```
wget http://linux-training.be/files/studentfiles/wolf.jpg
wget http://linux-training.be/files/studentfiles/wolf.png
wget http://linux-training.be/files/books/LinuxFun.pdf
```

3b. 显示 `wolf.jpg` 和 `LinuxFun.pdf` 的文件类型

```
file wolf.jpg LinuxFun.pdf
```

3c. 将 `wolf.jpg` 重命名为 `wolf.pdf`（使用 `mv`）。

```
mv wolf.jpg wolf.pdf
```

4. 显示 `wolf.pdf` 和 `LinuxFun.pdf` 的文件类型。

```
file wolf.pdf LinuxFun.pdf
```

5. 创建目录 `~touched` 并进入该目录。

```
mkdir ~touched ; cd ~touched
```

6. 在 `touched` 中创建文件 `today.txt` 和 `yesterday.txt`。

```
touch today.txt yesterday.txt
```

7. 将 `yesterday.txt` 的日期修改为昨天的日期（将 `20081025` 替换为昨天）

```
touch -t 200810251400 yesterday.txt
```

8. 将 `yesterday.txt` 复制到 `copy.yesterday.txt`

```
cp yesterday.txt copy.yesterday.txt
```

9. 将 `copy.yesterday.txt` 重命名为 `kim`

```
mv copy.yesterday.txt kim
```

10. 创建一个名为 `~testbackup` 的目录并将 `~touched` 中的所有文件复制到该目录中。

```
mkdir ~/testbackup ; cp -r ~touched ~/testbackup/
```

11. 使用 `rm` 删除 `~testbackup` 目录及其其中的所有文件。

```
rm -rf ~/testbackup
```

12. 创建目录 `~etcbackup`并将 `/etc` 中所有的 `*.conf` 文件复制到该目录中。你包含 `/etc` 的所有子目录了吗？

```
cp -r /etc/*.conf ~/etcbackup
```

只有直接位于 `/etc/` 下的 `*.conf` 文件会被复制。

- 12. 使用 `rename` 将所有的 `*.conf` 文件重命名为 `*.backup`。（如果你有多个发行版可用，请在所有发行版上尝试！）

在 RHEL 上：`touch 1.conf 2.conf ; rename conf backup *.conf`

在 Debian 上：`touch 1.conf 2.conf ; rename 's/conf/backup/' *.conf`

# 第 10 章 文件内容操作

在本章中我们将使用 `head`, `tail`, `tac`, `cat`, `more`, `less` 和 `strings` 命令查看文本文件的内容。

我们还将领略命令行上 `cat` 等工具的可能性。

## 10.1. head

你可以使用 `head` 来显示文件的前十行。

```
paul@debian7~$ head /etc/passwd
root:x:0:0:root:/root:/bin/bash
demon:x:1:1:daemon:/usr/sbin:/bin/sh
bin:x:2:2:bin:/bin:/sh
sys:x:3:3:sys:/dev:/sh
sync:x:4:65534:sync:/bin:/sync
games:x:5:60:game:/usr/bin:/sh
man:x:6:12:man:/var/cache/man:/bin/sh
lp:x:7:7:lp:/var/spool/lpd:/bin/sh
mail:x:8:8:mail:/var/mail:/bin/sh
news:x:9:news:/var/spool:/bin/sh
root@debian7~$
```

`head` 命令也可以显示文件的前 `n` 行。

```
paul@debian7~$ head -4 /etc/passwd
root:x:0:0:root:/root:/bin/bash
demon:x:1:1:daemon:/usr/sbin:/bin/sh
bin:x:2:2:bin:/bin:/sh
sys:x:3:3:sys:/dev:/sh
paul@debian7~$
```

并且 `head` 还可以显示前 `n` 字节。



```
paul@debian7~$ head -c14 /etc/passwd
root:x:0:0:roopaul@debian7~$
```

## 10.2. tail

与`head`类似，`tail`命令将显示文件的最后几行。

```
paul@debian7~$ tail /etc/services
vboxd      20012/udp
binkp       24554/tcp
asp          27374/tcp
ast          27374/udp
csync2      30865/tcp
dircproc     57000/tcp
ffidos       60177/tcp
fido        60179/tcp
paul@debian7~$
```

你可以使用`tail -n`指定你想看到的行数。

```
paul@debian7~$ tail -3 /etc/services
fido        60179/tcp
paul@debian7~$
```

（注：原文 10.2 结尾处代码块似乎有断行，已按原样保留）

## 10.8. 解决方案：文件内容

1. 显示`/etc/services`的前12行。

```
head -12 /etc/services
```

2. 显示`/etc/passwd`的最后一行。

```
tail -1 /etc/passwd
```

3. 使用`cat`创建一个名为`count.txt`的文件，内容如下：

```
cat > count.txt
One
Two
Three
Four
Five (按下 Ctrl-d 结束)
```

4. 使用`cp`将该文件备份到`cnt.txt`。

```
cp count.txt cnt.txt
```

5. 使用`cat`将该文件备份到`catcnt.txt`。

```
cat count.txt > catcnt.txt
```

6. 反序显示`catcnt.txt`的所有行（最后一行在最）。

```
tac catcnt.txt
```

7. 使用`more`显示`/etc/services`。

```
more /etc/services
```

8. 显示`/usr/bin/passwd`命令中的可读字符字符串。

```
strings /usr/bin/passwd
```

9. 使用`ls`找到`/etc`目录中最大的文件。

```
ls -ls /etc
```

10. 打开两个终端窗口（或标签页），确保你处于同一个目录下。在第一个终端执行`echo This is the first line > tailing.txt`，然后在第二个终端中使用`tail -f tailing.txt`。现在回到第一个终端并执行`echo This is another line >> tailing.txt`（注意双大于`>>`），验证第二个终端的`tail -f`是否显示了两个行。按Ctrl-C停止`tail -f`。

11. 使用`cat`创建一个名为`tailing.txt`的文件，其中包含`tailing.txt`的内容，随后是`/etc/passwd`的内容。

```
cat /etc/passwd >> tailing.txt
```

12. 使用`cat`创建一个名为`tailing.txt`的文件，其中包含`/etc/passwd`的内容，在其后是`tailing.txt`的内容。

```
mv tailing.txt tmp.txt ; cat /etc/passwd tmp.txt > tailing.txt
```

## 第 11 章. Linux 文件树

本章将介绍Linux文件树中常见的目录。它还展示了在Unix系统中，一切皆文件。

## 11.1. 文件系统层次结构标准 (FHS)

许多Linux发行版部分地遵循文件系统层次结构标准（FHS）。FHS有助于未来更多Unix/Linux文件系统更好地符合标准。可以在`http://www.pathname.com/fhs`在线查看FHS，我们在那里看到：“文件系统层次结构被设计供Unix发行版开发者使用”。

## 11.2. man hier

不同的Linux发行版之间的文件系统存在一些差异。为了帮助你的机器，请输入`man hier`来查找有关文件系统层次结构的信息。该手册将解释你计算机上的目录结构。

## 11.3. 根目录 /

所有的Linux系统都有从根目录开始的目录结构。根目录由斜杠`/`表示，如下所示`/`。你Linux系统上存在的所有内容都可以在这个根目录之下找到。让我们简要查看根目录的内容。

```
[paul@RHEL4u3 ~]$ ls /
bin dev home media mnt sbin srv tftpboot usr
boot etc lib misc opt root selinux sys tmp var
```

## 11.4. 二进制目录

二进制文件是包含编译后的源文件（或机器码）的文件。二进制文件可以在计算机上执行。有时二进制文件也被称为可执行文件。

### 11.4.1. /bin

`/bin`目录包含所有用户使用的二进制文件。根据FHS，`/bin`目录应该包含`/bin/cat`和`/bin/date`（以及其他文件）。

在下方的图中，你看到了常见的Unix/Linux命令，如`cat`、`cpio`、`dd`、`dd`、`echo`、`grep`等。这些中的许多命令都将在本书中进行介绍。

```
paul@alika~$ ls /bin
archdetect      grep     mt               setupcon
autopartition false     mt-gnu           sh
bash           console mv               sh.distrib
bunzip2        fuser    nano              sleep
bcat            fusermount  nc.traditional stralign
bczmp          get_mountpoints netcat          tty
dbzdiff       grep      netstat         sync
bzgrep       grep      nfs-3g          sysfs
bzgrep       gzip      nfs-3g.probe    talf
bzgrep       gzip      parsed_devices tar
bzip2        hostname parted_server tempfile
bzip2ipecover  hw-detect               touch
bzless        ip        partman-commit true
cat            kbd_mode perform_recipe ulockmgr
              kill      pidof             umount
              ... 
```

### 11.4.2. 其他 bin 目录

你可以在许多其他目录中找到`/bin`子目录（注：原文为 /bin，此处意译为 bin 子目录）。一个名为`serena`的用户可以将她的程序放在`/home/serena/bin`中。

某些应用程序在直接从源码安装时会将它们存放在`/opt`中。`samba`服务器安装可以使用`/opt/samba/bin`来存储其二进制文件。

### 11.4.3. /sbin

`/sbin`包含配置操作系统的二进制文件。许多系统二进制文件需要`root`权限才能执行某些任务。

下方是一个包含更改IP地址、分区磁盘和创建`ext4`系统的系统二进制文件的截图。

```
paul@ubu10:~$ ls -l /sbin/mkfs.ext4
-rwxr-xr-x 1 root 9112 02-02
-rwxr-xr-x 1 root 6570 07-02 fdisk
-rwxr-xr-x 1 root 5514 08-18 ipconfig
```

# Linux 文件树结构



```
paul@RHEL4u4:~$ ls /etc/sysconfig/ network saslauthd
apmd firstboot irda
apm-scripts grub irqbalance networking selinux
hidd hid keyboard nptd spassassin
autofs http kudzu openif.conf squid
bluetooth bwn0 ms_sensors pand syslog
clock i18n mouse pcmia sys-config-sec
console init mouse.bg pgsql sys-config-users
crond installall named prelink sys-logviewer
desktop ipmi netdump devices tux
diskdump iptables netdump_dsa rhn vncversvers
dund iptables-cfg netdump_id_dsa samba xineted
```

`/etc/sysconfig/firstboot` 文件告诉红帽设置向程序（Red Hat Setup Agent）不要在启动时运行。如果你想在下次重启时运行红帽设置向程序，只需删除此文件，并运行`chconfig -level 5 firstboot`即可。红帽设置向程序允许你安装最新更新、创建用户账户、加入红帽网络等。它随后会再次创建`/etc/sysconfig/firstboot`。

```
paul@RHEL4u4:~$ cat /etc/sysconfig/firstboot
RUN_FIRSTBOOT=NO
```

`/etc/sysconfig/harddisks` 文件包含了一些用于调整硬盘的参数。该文件本身具有说明性。

你可以在`/etc/sysconfig/hwconf`中看到由`kudzu`检测到的硬件。Kudzu 是红帽的一个用于硬件自动发现和配置的软件。

键盘类型和键位表在`/etc/sysconfig/keyboard`文件中设置。有关更多控制台键盘的信息，请查看`keymaps(5)`、`dumpkeys(1)`、`loadkeys(1)`的手册页以及`/lib/kbd/keymaps`目录。

```
root@RHEL4u4:/etc/sysconfig# cat keyboard
KEYBOARD_TYPE="pc"
KEYTABLEMAP="us"
```

我们将在网络章节中讨论网络。

## 11.6. 数据目录

### 11.6.1. `/home`

用户可以在`/home`下存储个人或项目数据。一种常见的做法（但对于 lhs 来说并非强制性）是以用户名的格式来给用户主目录命名，格式为`/home/$USERNAME`。例如：

```
paul@ubu606:-$ ls /home
geert annik paul tom
```

除了为每个用户（或每个项目或组）提供存储个人文件的地方外，用户的主目录还作为存储配置文件的地方。一个典型的 Unix 用户配置包含许多隐藏文件（以点符号开头的文件）。Unix 用户配置的隐藏文件包含了该用户的设置。

```
paul@ubu606:-$ ls -d /home/*
/home/paul/ /home/paul/.bash_profile /home/paul/.ssh
/home/paul/. /home/paul/.bashrc /home/paul/.viminfo
/home/paul/.bash_history /home/paul/.lesshst
```

### 11.6.2. `/root`

在许多系统中，`/root` 是 root 用户个人数据和配置的默认位置。如果默认不存在，则由管理员创建。

### 11.6.3. `/srv`

你可以使用`/srv`来存放由系统提供的数据。FHS（文件系统层次结构）允许将`cvs`、`rsync`、`ftp`和`www`数据放置在此位置。FHS 也允许在`/srv`中进行管理性命名，例如`/srv/project55/ftp`和`/srv/sales/www`。

在 Sun Solaris（或 Oracle Solaris）上，`/export`用于此目的。

### 11.6.4. `/media`

`/media`目录作为 CD-ROM、数码相机和各种 USB 连接设备的设备的挂载点。由于`/media`在 Unix 世界还很新，你可能会遇到没有这个目录的运行系统。Solaris 9 没有它，但 Solaris 10 有。如今大多数 Linux 发行版都将所有可移动媒体挂载到`/media`。

```
paul@debian5:-$ ls /media/
cdrom cdrom0 usbdisk
```

### 11.6.5. `/mnt`

根据 FHS，`/mnt`目录应该是空的，并且应该用于临时挂载点。

Unix 和 Linux 管理员过去在这里创建许多目录，例如`/mnt/something/`。你可能会遇到许多在`/mnt`内部创建和/或挂载了多个目录的系统，用于各种本地和远程文件系统。

### 11.6.6. `/tmp`

应用程序和用户在需要时应使用`/tmp`存储临时数据。存储在`/tmp`中的数据可能使用磁盘空间或 RAM。两者都由操作系统管理。永远使用`/tmp`存储重要或你想存档的数据。

## 11.7. 内存目录

### 11.7.1. `/dev`

`/dev`中的设备文件看起来像普通文件，但实际上并不位于硬盘上。当内核识别硬件时，`/dev`目录会生成相应的文件。

#### 常见物理设备

硬盘设备等常见硬件由`/dev`中的设备文件表示。下面是笔记本电脑上的 SATA 设备和台式机上 IDE 连接驱动器的截图。（这些设备的详细含义稍后讨论。）

```
# SATA 或 SCSI 或 USB
# paul@laika:-$ ls /dev/sd*
/dev/sda /dev/sda1 /dev/sda2 /dev/sda3 /dev/sdb /dev/sdb1 /dev/sdb2

# IDE 或 ATAPI
# paul@barry:-$ ls /dev/hd*
/dev/hda /dev/hda1 /dev/hda2 /dev/hdb /dev/hdb1 /dev/hdb2 /dev/hdc
```

除了表示硬件外，某些设备也是特殊的。这些设备非常有用。

#### `/dev/tty`

例如，`/dev/tty1`代表连接到系统的终端（像 Gnome 或 KDE 的命令行终端表示为`/dev/pts/1`）。

#### `/dev/null`

在 Linux 上你会发现另一个特殊设备`/dev/null`，它具有无限存储，但无法从中检索内容。从技术上讲，写入`/dev/null`的任何内容都会被丢弃，不是备份的地方。

### 11.7.2. `/proc`

`/proc`是另一个特殊目录，看起来像普通文件，但不占用磁盘空间。它实际上是内核的视图，或者说是与内核交互的界面。

```
paul@RHEL4u:~$ ls -t /proc
```

当列出`/proc`目录时，你会看到许多数字（Unix 上）和一些信息（Linux 上）。



```
paul@laike:-$ ls /proc
2339 4724 5418 6568 6701 7201 10175 4727 5421 6569 6996 7204 cpuinfo 1021 2873 4761 5658 6996 crypto 1023 2975 4873 5661 6328 typeinfo 141 2975 4874 5665 6652 partitions 15045 2972 4878 5927 6719 disks 15197 4980 5359 6126 6713 dm 15521 4828 5083 6032 6737 sched_debug 15554 3069 5143 6035 6755 driver 15527 5023 6228 6794 7266 self 15619 3147 5414 6418 6816 slabinfo 18108 3507 5203 6918 7282 filesystems 18191 5209 5418 6591 6968 stat 18203 3193 6228 6496 7319 swq-trigger 18896 3246 5272 6421 7157 sys 19799 3248 5921 6422 7163 iomem 19804 3213 5394 6161 7123 time_list 19830 5326 6472 7115 7529 irq 19987 5379 6426 6818 7986 uptime 19942 5370 6425 7175 7529 version 20485 5462 6450 7191 7808 version_signature 2221 5414 6551 7192 8392 vmcore 23704 5416 6568 7199 7938 locks
```

`/proc` 内部的文件属性是什么？查看当前日期和时间将显示不断更新的文件（内核的视图）。

```
root@RHELu4:-$ date
Mon Jan 29 18:06:32 EST 2007
root@RHELu4:-$ ls -al /proc/cpuinfo
-r-r--r-- 1 root 0 root Jan 29 18:06:18 /proc/cpuinfo
root@RHELu4:-$ ... time passes...
root@RHELu4:-$ date
Mon Jan 29 18:10:00 EST 2007
root@RHELu4:-$ ls -al /proc/cpuinfo
-r-r--r-- 1 root 0 root Jan 29 18:10:00 /proc/cpuinfo
```

`/proc` 中的大多数文件都是 0 字节，但它们包含了大量数据。你可以通过 `cat` `/proc/cpuinfo` 等文件看到这一点，它包含了关于 CPU 的信息。

```
root@RHELu4:-$ file /proc/cpuinfo
/proc/cpuinfo: empty
root@RHELu4:-$ cat /proc/cpuinfo
processor
  : 0
vendor_id
  : AuthenticAMD
cpu family
  : 15
model
  : 43
model name : AMD Athlon(tm) 64 X2 Core Processor 4600+
stepping : 1
cpu MHz : 2398.628
cache size : 512 KB
fdiv_bug : no
hlt_bug : no
f00_bug : no
coma_bug : no
fpu : yes
fpu_exception : yes
cpuid level : 1
wp : yes
flags : fpu vme pse tsc mser cx8 apric mtrr ge...
bogomips : 4803.54
```

为了好玩，这是 Sun Blade 1000 上的 `/proc/cpuinfo`……

```
paulspasha:~$ cat /proc/cpuinfo
cpu : TI UltraSparc III (Cheetah)
fpu : UltraSparc III integrated FPU
promblib : Version 3 Revision 2
prom : 4.2.2
type : nudu4
ccpus probed : 2
ccpus active : 2
Cpu0Bogo : 498.68
Cpu0ClkTck : 000000002cb41780
Cpu1Bogo : 498.68
Cpu1ClkTck : 000000002cb41780
MMU Type : Cheetah
State : 
CPU0 : online
CPU1 : online
```

# /proc/interrupts

在 x86 ELV 架构上，`/proc/interrupts` 显示中断信息。

```
paul@RHELv4u~$ cat /proc/interrupts
CPU
0:      13876877    IO-APIC-edge      timer
1:      15              IO-APIC-edge      i8042
8:      1               IO-APIC-edge      rtc
9:      0               IO-APIC-level    acpi
12:     67              IO-APIC-edge      i8042
14:     128             IO-APIC-edge      ideo
15:     124320          IO-APIC-edge      idel
169:    111993          IO-APIC-level    ioc0
177:    2428            IO-APIC-level    eth0
NMI:                               0
LOC:    13878037
ERR:                               0
MIS:                               0
```

在带有两个 CPU 的机器上，该文件看起来如下：

```
paul@laika:~$ cat /proc/interrupts
CPU             CPU1
0:      860013          IO-APIC-edge      timer
1:      4533            IO-APIC-edge      i8042
7:      0               IO-APIC-edge      parport0
8:      6588227         IO-APIC-edge      rtc
10:     2314            IO-APIC-fastei   acpi
12:     133             IO-APIC-edge      i8042
14:     0               IO-APIC-edge      libata
15:     72269           IO-APIC-edge      libata
18:     1               IO-APIC-fastei   yenta
19:     115036          IO-APIC-fastei   eth0
20:     126871          IO-APIC-fastei   libata,ohci3194
21:     302004          IO-APIC-fastei   ehci_hcd:usb1, uhci_hcd:usb2
22:     13334           IO-APIC-fastei   saa7133[0], saa7133[0]
24:     2347319         IO-APIC-fastei   nvidia
NMI:                72              42
LOC:    860000          859994
ERR:
```

# /proc/kcore

物理内存在 `/proc/kcore` 中表示。不要尝试用 `cat` 这个文件，而应使用调试器。`/proc/kcore` 等同于你的物理内存，外加四个字节。

```
paul@laika:~$ ls -lh /proc/kcore
-r-------- 1 root 2.0G 2007-01-30 08:57 /proc/kcore
paul@laika:~$
```

## 11.7.3. /sys Linux 2.6 热插拔



`/sys`目录是为了Linux 2.6内核创建。从2.6版本开始，Linux使用`sysfs`支持USB和IEEE 1394 (FireWire)热插拔设备。请参阅`udev(8)`（`devfs`的继承者）和`hotplug(8)`的手册页获取更多信息（或访问`http://linux-kernel-hotplug.sourceforge.net/`）。

基本上，`/sys`目录包含了关于硬件的内核信息。

# 11.8. /usr 系统资源

虽然`usr`的读音与`user`相似，但请记住它代表Unix System Resources（Unix系统资源）。`/usr`层次结构应该包含共享的只读数据。有些人选择将`/usr`挂载为只读。这可以通过它自己的分区或从只读NFS共享来实现（NFS将稍后进行讨论）。

## 11.8.1. /usr/bin

`/usr/bin`目录包含许多命令。

```
paul@deb508:~$ ls /usr/bin | wc -l
1395
```

（在Solaris上，`/bin`目录是指向`/usr/bin`的符号链接）。

## 11.8.2. /usr/include

`/usr/include`目录包含C语言的通用文件。

```
paul@bub010:~$ ls /usr/include/
ailib.h expat_config.h math.h search.h
af_vs.h expat_external.h mcheck.h semaphore.h
asio.h expat.h memory.h setjmp.h
Alcntl.h menu.h sgtty.h
aliases.h features.h mntent.h shadow.h
...
```

## 11.8.3. /usr/lib

`/usr/lib`目录包含不被用户或脚本直接执行的库。

```
paul@deb508:~$ ls /usr/lib | head -7
4suite
ao
apt
arj
assell
avahi
bonobo
```

## 11.8.4. /usr/local

管理员可以使用`/usr/local`目录在本地安装软件。

```
paul@deb508:~$ ls /usr/local/
bin etc include lib share
```

## 11.8.5. /usr/share

`/usr/share`目录包含了架构无关的数据。

## 11.8.6. /usr/sbin

`/usr/sbin`目录包含了系统范围的可执行命令。

## 11.8.7. /usr/bin

`/usr/bin`目录包含了系统范围的普通执行文件。

## 11.8.8. /usr/local

`/usr/local`目录包含了用户本地安装的软件文件。

14. 读取`random`的man页并解释`/dev/random`和`/dev/urandom`之间的差异。

# 11.11 答案：文件系统树

1. 文件`/bin/cat`是否存在？`/bin/dd`和`/bin/echo`呢？这些文件的类型是什么？

```
ls /bin/cat ; file /bin/cat
ls /bin/dd ; file /bin/dd
ls /bin/echo ; file /bin/echo
```

2. `/boot`目录下的Linux内核文件（`vmlinux*`）大小是多少？

```
ls -lh /boot/vmlinuz*
```

3. 创建一个目录`~/test`。然后执行以下命令：

```
cd ~/test
dd if=/dev/zero of=zeros.txt count=1 bs=100
od zeros.txt
```

`dd`将从`/dev/zero`文件复制一次（`count=1`）大小为100字节（`bs=100`）的块数据到`~/test/zeros.txt`。你能描述`/dev/zero`的功能吗？

`/dev/zero`是一个Linux设备。它可以被视为零的源。你不能向`/dev/zero`发送内容，但可以从它读取零。

4. 现在执行以下命令：

```
dd if=/dev/random of=random.txt count=1 bs=100; od random.txt
```

`dd`将从`/dev/random`文件复制一次（`count=1`）大小为100字节（`bs=100`）的块数据到`~/test/random.txt`。你能描述`/dev/random`的功能吗？

`/dev/random`在你的Linux上充当随机数生成器。

5. 执行这两个命令，并查看每个输出行的第一个字符。

```
ls -l /dev/sd* /dev/hd*
ls -l /dev/tty* /dev/input/mou*
```

第一个`ls`显示的是块设备(b)，第二个显示的是字符设备(c)。你能告诉我块设备和字符设备之间的区别吗？

块设备总是以块为单位进行写入（或读取）的。对于硬盘，512字节的块是常见的。字符设备作为字符流（或字节流）工作。鼠标和键盘是典型的字符设备。

6. 使用`cat`描述`/etc/hosts`和`/etc/resolv.conf`。你对这些文件的用途有什么看法？

```
/etc/hosts 包含主机及其 IP 地址
/etc/resolv.conf 应该包含 DNS 服务器的 IP 地址。
```

7. `/etc/skel/`中是否有任何文件？也检查是否有隐藏文件。

`"ls -al /etc/skel/"`。是的，那里应该有隐藏文件。

8. 显示`/proc/cpuinfo`。你的Linux运行在什么架构上？

该文件至少包含一行带有`Intel`或其他`cpu`字样。

9. 显示`/proc/interrupts`。这个文件有多大？这个文件存储在哪里？

大小为零，你得到的是内容数据。它没有存储在任何地方，因为`/proc`是一个虚拟文件系统，允许你与内核通信。（如果你回答“存储在内存中”，也是正确的……）

10.你能进入`/root`目录吗？有（隐藏）文件吗？

尝试`"cd /root"`。在大多数现代Linux系统上，普通用户无法访问`/root`目录。

11. 如果`/sbin`中存在`areconfig`, `fdisk`, `parted`, `shutdown`和`grub-install`，为什么这些二进制文件在`/sbin`中而不在`/bin`中？

因为这些文件仅供系统管理员使用。

12. `/var/log`是文件还是目录？`/var/spool`呢？

两者都是目录。

13. 打开两个命令提示符（`gnome-terminal`中的`Ctrl-Shift-T`）或终端（`Ctrl-Alt-F1`, `Ctrl-Alt-F2`, ...），并在两者中都执行`who am i`。然后尝试从一个终端`echo`一个单词到另一个终端。

```
tty-terminal: echo Hello > /dev/tty1
```

```
pts-terminal: echo Hello > /dev/pts/1
```

14. 读取`random`的man页并解释`/dev/random`和`/dev/urandom`之间的差异。

```
man 4 random
```

# 第四部分。shell 扩展

## 目录

- 12. 命令与参数 ............................................................................ 125

- 12.1. 参数 ................................................................................................ 126

- 12.2. 空格删除 ................................................................................ 126

- 12.3. 单引号 ................................................................................................ 127

- 12.4. 双引号 ................................................................................ 127

- 12.5. `echo` 与引号 ................................................................................ 127

- 12.6. 命令 ................................................................................................ 128



### 12.7. 别名

### 12.8. 显示 `shell` 扩展

### 12.9. 练习：命令与参数

### 12.10. 答案：命令与参数

### 13. 控制运算符

### 13.1. 分号

### 13.2. `&` 符号

### 13.3. `$` 符号

### 13.4. `&&` 符号

### 13.5. `|` 符号

### 13.6. `||` 符号

### 13.7. `#` 符号

### 13.8. 转义字符

### 13.9. 练习：控制运算符

### 13.10. 答案：控制运算符

### 14. `shell` 变量

### 14.1. `$` 符号

### 14.2. 大小写敏感

### 14.3. 创建变量

### 14.4. 引号

### 14.5. `set`

### 14.6. `unset`

### 14.7. `$PS1`

### 14.8. `$PATH`

### 14.9. `env`

### 14.10. `export`

### 14.11. 删除变量

### 14.12. 取消变量

### 14.13. 练习：`shell` 变量

### 14.14. 答案：`shell` 变量

### 15. `shell` 嵌入与选项

### 15.1. `shell` 嵌入

### 15.2. `shell` 选项

### 15.3. 练习：`shell` 嵌入

### 15.4. 答案：`shell` 嵌入

### 16. `shell` 历史

### 16.1. 重复上一个命令

### 16.2. 重复其他命令

### 16.3. `history`

### 16.4. `-n`

### 16.5. `Ctrl-`

### 16.6. `$HISTSIZE`

### 16.7. `$HISTFILE`

### 16.8. `$HISTFILESIZE`

### 16.9. 防止命令执行

### 16.10. (可选)正则表达式

### 16.11. (可选)`Korn shell` 历史

### 16.12. 练习：`shell` 历史



# 16.13. 解决方案：shell 扩展

# 17. 文件通配 (file globbing)

*   17.1. * 星号
*   17.2. ? 问号
*   17.3. [] 方括号
*   17.4. a-z 和 0-9 范围
*   17.5. `$LANG` 和方括号
*   17.6. 防止文件通配
*   17.7. 练习：shell 通配
*   17.8. 解决方案：shell 通配

# 第 12 章 命令与参数

本章通过仔细观察`命令`和`参数`来向你介绍`shell 扩展`。了解`shell 扩展`非常重要，因为你 Linux 系统上的许多`命令`在执行之前会经过`shell`处理并极有可能被修改。

大多数 Linux 系统使用的命令行界面或`shell`被称为`bash`，它代表`Bourne again shell`（再次的 Bourne 壳）。`bash` shell 结合了来自`sh`（原始的 Bourne shell）、`esh`（C shell）和`ksh`（Korn shell）的特性。

本章经常使用`echo`命令来演示 shell 特性。`echo`命令非常简单：它回显它收到的输入。

```
paul@laika:~$ echo Burtonville
Burtonville
paul@laika:~$ echo Smurfs are blue
Smurfs are blue
```

## 12.1. 参数

shell 的主要功能之一是执行命令行扫描。当你在 shell 的命令提示符处输入命令并按回车键时，shell 将开始扫描该行，将其切割成各个参数。在扫描行的过程中，shell 可能会对你输入的参数进行许多更改。

这个过程被称为 shell 扩展。当 shell 完成对该行的扫描和修改后，它就会被执行。

## 12.2. 空格移除

由一个或多个连续空格（或制表符）分隔的部分被视为独立的参数，任何空格都会被移除。第一个参数是要待执行的命令，任何其他参数都会传递给该命令。shell 实际上是将你的命令切割成一个或多个参数。

这解释了为什么以下四个不同的命令行在 shell 扩展后是相同的。

```
paul@RHELv4u ~$ echo Hello World
Hello World
paul@RHELv4u ~$ echo Hello World
Hello World
paul@RHELv4u ~$ echo Hello
Hello World
paul@RHELv4u ~$ echo Hello World
Hello World
```

`echo`命令将显示它从 shell 接收到的每一个参数。`echo`命令还会在收到的参数之间添加一个新的新空格。

## 12.3. 单引号

你可以通过对空格加引号来防止空格被移除。被引号括的字符串的内容被视为一个参数。在下面的截图中，`echo`接收到

```
[paul@RHEL4b ~]$ echo 'A line with single quotes'
A line with    single quotes
[paul@RHEL4b ~]$
```

## 12.4. 双引号

你也可以通过对空格加双引号来防止空格被移除。与上面相同，`echo`只接收到一个参数。

```
[paul@RHEL4b ~]$ echo \"A line with double quotes"
A line with    double quotes
[paul@RHEL4b ~]$
```

在书的后续部分，当我们讨论变量时，我们将看到单引号和双引号之间的重要区别。

## 12.5. `echo` 与引号

带引号的行可以包含`echo`命令识别的特殊转义字符（当使用`echo -e`时）。下面的截图显示了如何使用`\n`表示换行，以及使用`\t`表示制表符（通常是八个空格）。

```
[paul@RHEL4b ~]$ echo -e \"A line with \n newline"\ line with
a newline
[paul@RHEL4b ~]$ echo -e \"A line with \n newline"\ line with
a newline
[paul@RHEL4b ~]$ echo -e \"A line with \t tab"\ line with
 a tab
[paul@RHEL4b ~]$ echo -e \"A line with \t tab"\ line with
 a tab
[paul@RHEL4b ~]$
```

`echo`命令生成的不仅仅是空格、制表符和换行符。请查看手册页（man page）获取选项列表。

## 12.6. 命令

### 12.6.1. 外部命令还是内置命令？

并不是所有命令都是 shell 外部的，有些是内置的。外部命令是拥有自己的二进制文件并存在于文件系统某处的程序。许多外部命令位于`/bin`或`/sbin`。内置命令是 shell 本身不可或缺的一部分。

### 12.6.2. `type`

要确定给 shell 的命令是作为外部命令执行还是内置命令执行，请使用`type`命令。

```
paul@laika:-$ type cd
cd is a shell builtin
paul@laika:-$ type cd
```

（注：原文文本中存在大量重复和 OCR 错误，此处已根据核心信息进行清理和翻译。）

## 12.9. 练习：命令与参数

*   1. 这一行中有几个参数（不包括命令本身）。
    ```
    touch /etc/cron/cron.allow 'file 42.txt' "file 33.txt"
    ```
*   2. `tac`是 shell 内置命令吗？
*   3. `rm`有别名吗？
*   4. 读取`rm`的帮助页，确保你理解`rm`的`-i`选项。创建并删除一个文件来测试`-i`选项。
*   5. 执行：`alias rm='rm -i'`。用测试文件测试你的别名。这是否按预期工作？
*   6. 列出所有当前别名。
*   7a. 创建一个名为 'city' 的别名，输出你的家乡。
*   7b. 使用你的别名测试它是否工作正常。
*   8. 执行`set -x`显示每个命令的 shell 扩展。
*   9. 通过执行你的`city`和`rm`别名来测试`set -x`的功能。
*   10. 执行`set +x`停止显示 shell 扩展。
*   11. 删除你的`city`别名。
*   12. `cat`和`passwd`命令的位置在哪里？
*   13. 解释以下命令之间的区别：
    ```
    echo
    /bin/echo
    ```
*   14. 解释以下命令之间的区别：
    ```
    echo Hello
    echo -n Hello
    ```
*   15. 显示 A B C，其中 B 和 C 之间有两个空格。
*   (可选) 16. 完成以下命令（不要使用空格）以精确显示以下输出：
    ```
    4+4   =8
    10+14 =24
    ```
*   17. 使用`echo`精确显示以下：



```
??\"
```

找到两个使用单引号的解决方案，两个使用双引号和一个不使用引号的（并感谢 Google 的 René 和 Dariush 提供的额外提示）。

- 18. 使用一个 `echo` 命令在三行中显示三个单词。

## 12.10. 答案：命令与参数

- 1. 这一行中有几个参数（不包括命令本身）。

答案：三个

- 2. `tac` 是 shell 内置命令吗？

`type tac`

- 3. `rm` 有现有别名吗？

`alias rm`

- 4. 读取 `rm` 的帮助页，确保你理解 `rm` 的 `-i` 选项。创建并删除一个文件来测试 `-i` 选项。

```bash
man rm
touch testfile
rm -i testfile
```

- 5. 执行：`alias rm='rm -i'`。用测试文件测试你的别名。这是否按预期工作？

```bash
touch testfile
rm testfile # 应该询问确认
```

- 6. 列出所有当前别名。

`alias`

- 7a. 创建一个名为 `city` 的别名，输出你的家乡。

```bash
alias city='echo Antwerp'
```

- 7b. 使用你的别名测试它是否工作正常。

```bash
city # 它应该显示 Antwerp
```

- 8. 执行 `set -x` 显示每个命令的 shell 扩展。

```bash
set -x
```

- 9. 通过执行你的 `city` 和 `rm` 别名测试 `set -x` 的功能。

```bash
# shell 应该显示解析后的别名并执行命令：
paul@db503:$ set -x
paul@db503:$ city
echo antwerp
antwerp
```

- 10. 执行 `set +x` 停止显示 shell 扩展。

```bash
set +x
```

- 11. 删除你的 `city` 别名。

```bash
unalias city
```

# 12. `cat` 和 `passwd` 命令的位置在哪里？

`which cat` (可能是 `/bin/cat`)

`which passwd` (可能是 `/usr/bin/passwd`)

# 13. 解释以下命令之间的区别：

```bash
echo
```

```bash
/bin/echo
```

`echo` 命令将由 shell 解释为内置的 `echo` 命令。`/bin/echo` 命令将让 shell 执行位于 `/bin` 目录下的 `echo` 二进制文件。

# 14. 解释以下命令之间的区别：

```bash
echo
echo -n Hello
```

`echo` 命令的 `-n` 选项将防止 `echo` 输出末尾换行符。`echo Hello` 会输出六个字符，`echo -n Hello` 只输出五个字符。

（`-n` 选项在 Korn shell 中可能不起作用）。

# 15. 显示 A B C，其中 B 和 C 之间有两个空格。

```bash
echo "A B C"
```

# 16. 完成以下命令（不要使用空格）以精确显示以下输出：

```
4+4 =8
10+14 =24
```

解决方案是使用 `echo` 显示带有 `\t` 的制表符。

```bash
echo -e "4+4\t=8"; echo -e "10+14\t=24"
```

# 17. 使用 `echo` 显示以下：

```bash
??\\
echo '??\\\'
echo -e '??\\\\'
echo "??\\\\\"
echo -e "??\\\\\\\\"
echo ??\\\
```

找到两个使用单引号的解决方案，两个使用双引号和一个不使用引号的（感谢 René 和 Dariush 提供的提示）。

# 18. 使用一个 `echo` 命令在三行中显示三个单词。

```bash
echo -e "one \ntwo \nthree"
```

# 第 13 章 控制运算符

在本章中，我们使用控制运算符在命令行上放置多个命令。我们还简要讨论了参数（`$?`）和类似的字符（`&`）。

# 13.1. `;` 分号

你可以通过分号在命令行上放置两个命令。分号前面的命令执行完 shell 扩展后，分号后面的命令也会执行。使用分号分隔的命令是按顺序执行的。

```bash
echo Hello ; echo World
```

分号之前的命令顺序执行。

```bash
paul@db503:$ echo Hello
paul@db503:$ echo World
```

## 13.2. `&` 符号

当行以 `&` 结尾时，shell 将在后台执行命令。你将立即获得提示符，而命令在后台运行。

```bash
sleep 20 &
[1] 1234

paul@db503:$ sleep 20 &

paul@db503:$

[1] 1234
```

# 13.3. `$?` 参数

`$?` 存储了上一个命令的退出状态。通常 `0` 表示成功，非零表示失败。

```bash
ls /tmp
echo $?
0

ls /nonexistent
echo $?
2
```

## 13.4. `&&` 符号

shell 将 `&&` 解释为逻辑与。只有当第一个命令执行成功（返回状态为 `0`）时，才会执行第二个命令。

```bash
ls /tmp && echo Success
ls /nonexistent && echo Success
```

## 13.5. `||` 竖线符号

shell 将 `||` 解释为逻辑或。只有当第一个命令执行失败（返回状态非 `0`）时，才会执行第二个命令。

```bash
ls /tmp || echo Failed
ls /nonexistent || echo Success
```

# 13.6. 结合 `&&` 和 `||`

你可以使用 `&&` 和 `||` 在命令行上编写 `if-then-else` 结构。此示例使用 `echo` 来显示 `rm` 命令是否成功。

```bash
rm file && echo It worked! || echo It failed!
```

## 13.7. `#` 号

井号（`#`）之后的所有内容都会被 shell 忽略。这对于编写 shell 命令很有用，但对命令执行或 shell 扩展没有影响。

```bash
mkdir test # 创建一个目录
```

# 13.8. `\` 转义特殊字符

反斜杠 `\` 字符允许使用控制字符，如果不让 shell 解释它，这被称为转义字符。

```bash
echo hello \; world
```

### 13.8.1. 行尾反斜杠

以反斜杠结尾的行将延续到下一行。shell 不解释换行符，并将等待 shell 扩展和命令行执行，直到遇到不带反斜杠的换行符。

```bash
echo This command line \
> is split in three \
> parts
```

## 13.9. 练习：控制运算符

- 0. 每个问题都可以通过一条命令来回答！
- 1. 当你输入 `passwd` 时，执行的是哪个文件？
- 2. 那是一个什么类型的文件？
- 3. 执行两次 `pwd`。（记住 `0`）。
- 4. 在 `cd /etc` 之后执行 `ls`，但仅当 `cd /etc` 没有报错时。
- 5. 在 `cd etc` 之后执行 `cd /etc`，但仅当 `cd etc` 失败时。
- 6. 当 `touch test42` 成功时显示 `it worked`，`touch` 失败时显示 `it failed`。全部作为普通用户（非 `root`）在一行中完成。在你的家目录和 `/bin/` 下测试这一行。
- 7. 执行 `sleep 6`，这个命令是在做什么？
- 8. 在后台执行 `sleep 200`（不要等待它完成）。
- 9. 写一条执行 `rm file55` 的命令行。如果 `file55` 被删除，你的命令行应该打印 `'success'`；如果有问题，则打印 `'failed'`。
- （可选）10. 使用 `echo` 显示 `"Hello World with strange characters \* { } ~ \ \ \."`（包含所有引号）

## 13.10. 答案：控制运算符

0. 每个问题都可以通过一条命令来回答！

1. 当你输入 `passwd` 时，执行的是哪个文件？

```bash
which passwd
```

```bash
/usr/bin/passwd
```

3. 执行两次 `pwd` 命令。（记住 `0`）。

```bash
pwd ; pwd
```

4. 在 `cd /etc` 之后执行 `ls`，但仅当 `cd /etc` 没有报错时。

```bash
cd /etc && ls
```

5. 在 `cd etc` 之后执行 `cd /etc`，但仅当 `cd etc` 失败时。

```bash
cd etc || cd /etc
```



6. 当 `touch test42` 成功时 `echo it worked`，显示 `it worked`，当 `touch` 失败时 `echo it failed`，显示 `it failed`。作为普通用户（非 `root`）在一行中完成。在你的家目录和 `/bin/` 下测试此项。

```
paul@deb503:~$ cd ; touch test42 && echo it worked || echo it failed
it worked
paul@deb503:~$ cd /bin; touch test42 && echo it worked || echo it failed
touch cannot touch 'test42': Permission denied
it failed
```

7. 执行 `sleep 6`，这个命令是在做什么？

```
pausing for six seconds
```

8. 在后台执行 `sleep 200`（不要等待它完成）。

```
sleep 200 &
```

9. 写一条执行 `rm file55` 的命令行。如果 `file55` 被删除，你的命令行应该打印 `'success'`；如果有问题，则打印 `'failed'`。

```
rm file55 && echo success || echo failed
```

10. 使用 `echo` 显示 `"Hello World with strange characters \* \ { } ~ \\\\\ \."`（包含所有引号）。

```
echo \"Hello World with strange' \* \{ \} \ ~ \\\\\\ \.\"
echo "\"Hello World with strange' characters * { } ~ ..\"
```

# 第 14 章 shell 变量

在本章中，我们学习在 `shell` 中管理环境变量。这些变量通常是应用程序需要的。

## 14.1. `$` 美元符号

`shell` 解释的另一个重要字符是美元符号 `$`。`shell` 会寻找一个名为美元符号后跟字符串的环境变量，并将其替换为该变量的值（如果变量不存在则留空）。

以下是使用 `$HOSTNAME`、`USER`、`SUID`、`$SHELL` 和 `$HOME` 的示例。

```
[paul@RHELv43 ~]$ echo This is the $SHELL shell
This is the /bin/bash shell
[paul@RHELv43 ~]$ echo This is $SHELL on computer RHELv43.localdomain
[paul@RHELv43 ~]$ echo The userid of $USER is $UID
The userid of paul is 500
[paul@RHELv43 ~]$ echo My homedir is $HOME
My homedir is /home/paul
```

## 14.2. 区分大小写

这个示例说明 `shell` 变量是大小写敏感的！

```
[paul@RHELv43 ~]$ echo Hello $USER
Hello paul
[paul@RHELv43 ~]$ echo Hello $user
Hello
```

## 14.3. 创建变量

这个示例创建了变量 `$MyVar` 并设置了它的值。然后使用 `echo` 验证该值。

```
[paul@RHELv43 gen]$ gen MyVar=555
[paul@RHELv43 gen]$ echo $MyVar
555
[paul@RHELv43 gen]$ $
```

## 14.4. 引号

注意双引号仍然允许解析变量，而单引号则防止这种操作。

```
[paul@RHEL4u3 ~]$ MyVar=555
[paul@RHEL4u3 ~]$ echo $MyVar
555
[paul@RHEL4u3 ~]$ echo "$MyVar"
555
[paul@RHEL4u3 ~]$ echo '$MyVar'
$MyVar
```

`shell` 会在双引号行中将变量替换为它们的值，但在单引号中不会。

```
paul@RHEL4u3 ~]$ city=Burton
paul@RHEL4u3 ~]$ echo "We are in $city."
We are in Burton.
```

## 14.5. set

使用 `set` 命令列出所有变量。在 `Ubuntu` 系统中，`set` 命令会列出环境变量。这些环境变量在 `shell` 中显示。

## 14.6. unset

使用 `unset` 命令从环境变量中移除。

```
[paul@RHEL4b ~]$ hello=test
[paul@RHEL4b ~]$ echo hello
[paul@RHEL4b ~]$ unset hello
[paul@RHEL4b ~]$ echo hello
```

## 14.7. $PS1

`PS1` 决定了 `shell` 的提示符。你可以使用反转义字符，如 `\u` 表示用户名，`\w` 表示工作目录。在 `bash` 中多次更改 `shell` 提示符。

```
paul@deb503:~$ cd ; touch test42 && echo it worked || echo it failed
it worked
paul@deb503:~$ cd /bin; touch test42 && echo it worked || echo it failed
touch cannot touch 'test42': Permission denied
it failed
```

## 14.8. $PATH

`$PATH` 变量决定了 `shell` 在哪里查找可执行文件。它由冒号分隔目录。

```
[paul@RHEL4b ~]$ echo $PATH
/usr/bin:/bin
```

## 14.9. env

`env` 命令不带选项时将显示导出变量的列表。`set` 带选项的区别是 `set` 列出所有变量，包括未导出到子 `shell` 的变量。但 `env` 也可以启动一个干净的 `shell`（没有任何继承环境的 `shell`）。`env -i` 命令会清除 `shell` 的环境。

```
[paul@RHEL4b ~]$ echo $PATH
/usr/bin:/bin
```

## 14.10. export

可以使用 `export` 命令将 `shell` 变量导出到其他 `shell`。这将把变量导出到子 `shell`。

```
[paul@RHEL4b ~]$ var3=three
[paul@RHEL4b ~]$ var4=four
[paul@RHEL4b ~]$ export var4
[paul@RHEL4b ~]$ echo var3 $var4
three four
[paul@RHEL4b ~]$ bash
[paul@RHEL4b ~]$ echo var3 $var4
four
```

## 14.11. 划定变量

到目前为止，我们已经看到 `bash` 从美元符号开始解释变量，一直到第一个非字母数字（且非下划线）字符为止。在某些情况下，这可能会引起问题。可以通过示例所示的大括号来解决这个问题。

```
[paul@HEL4b ~]$ prefix=Super
[paul@HEL4b ~]$ echo Hello $prefix and $prefixgirl
Hello
[paul@HEL4b ~]$ echo Hello ${prefix}man and ${prefix}girl
Hello Superman and Supergirl
[paul@HEL4b ~]$
```

## 14.12. 未绑定变量

下面的示例尝试显示变量 `$MyVar` 的值，但由于该变量不存在而失败了。默认情况下，当变量未绑定（不存在）时，`shell` 不显示任何内容。

```
[paul@HEL4vu3 gen]$ echo $MyVar
[paul@HEL4vu3 gen]$
```

然而，有一个 `nounset` `shell` 选项，你可以用变量不存在时生成错误。

```
paul@laika:-$ set -u
paul@laika:-$ echo $MyVar
bash: Myvar: unbound variable
paul@laika:-$ set +u
paul@laika:-$ echo $MyVar
```



在 bash 中，`set -u` 等同于 `set -o nounset`，同样 `set +u` 等同于 `set +o nounset`。

## 14.13. 练习：shell 变量

1. 使用 `echo` 显示 Hello 后跟上你的用户名。（使用 bash 变量！）
2. 创建一个值为 42 的变量 `answer`。
3. 将 `$LANG` 的值复制到 `$MyLANG`。
4. 列出所有当前 shell 变量。
5. 列出所有导出的 shell 变量。
6. `env` 和 `set` 命令显示了你的变量吗？
7. 销毁你的 `answer` 变量。
8. 创建两个变量，并导出其中一个。
9. 在交互式子 shell 中显示导出的变量。
10. 创建一个变量并赋值为 'Dumb'，创建另一个值为 'do' 的变量。使用 `echo` 和这两个变量来输出 Dumbledore。
11. 在 bash 手书中找到反斜线转义字符列表。将时间添加到你的 `PS1` 提示符中。

## 14.14. 答案：shell 变量

1. 使用 `echo` 显示 Hello 后跟上你的用户名。（使用 bash 变量！）

```bash
echo Hello $USER
```

2. 创建一个值为 42 的变量 `answer`。

```bash
answer=42
```

3. 将 `$LANG` 的值复制到 `$MyLANG`。

```bash
MyLANG=$LANG
```

4. 列出所有当前 shell 变量。

```bash
set
# 注：Ubuntu/Debian 下可能需要使用 set more
```

5. 列出所有导出的 shell 变量。

```bash
env
export
declare -x
```

6. `env` 和 `set` 命令显示了你的变量吗？

| 命令 | 说明 |
| :--- | :--- |
| `env` | 显示环境变量 |
| `set` | 显示所有 shell 变量 |

7. 销毁你的 `answer` 变量。

```bash
unset answer
```

8. 创建两个变量，并导出其中一个。

```bash
var1=1
export var2=2
```

9. 在交互式子 shell 中显示导出的变量。

```bash
bash
echo $var2
```

10. 创建一个变量并赋值为 'Dumb'，创建另一个值为 'do' 的变量。使用 `echo` 和这两个变量来输出 Dumbledore。

```bash
varx=Dumb
vary=do

echo ${varx}le${vary}re
# 或者
echo "$varx""le$vary""re"
```

11. 在 bash 手书中找到反斜线转义字符列表。将时间添加到你的 `PS1` 提示符中。

```bash
PS1='\t \u\h \W$ '
```

## 第 15 章. shell 嵌入与选项

本章简要介绍子 shell、嵌入 shell 和 shell 选项。

### 15.1. shell 嵌入

shell 可以嵌入到命令行中，换句话说，命令行扫描可以产生包含当前 shell 分叉的新进程。你可以使用变量来证明创建了新的 shell。在截图中，变量 `$var1` 只存在于（临时的）shell 中。

```bash
[paul@RHELv43 gen]$ echo $var
[paul@RHELv4u3 gen]$ echo $var=5; $(var=echo $var1)
5
[paul@RHELv4u3 gen]$ echo $var1
[paul@RHELv4u3 gen]$
```

你可以在嵌入 shell 中嵌入 shell，这被称为 shell 的嵌套嵌入。

截图显示了嵌入 shell 中的嵌入 shell。

```bash
paul@deb503:-$ A=shell
paul@deb503:-$ echo $C$B$A$ $(B=sub;C$B$A); echo $(C=sub;C$B$A)
shell shell subshell
```

#### 15.1.1. 反引号 (backticks)

截图显示了嵌入 shell 中的嵌入 shell。

```bash
paul@deb503:-$ A=shell
paul@deb503:-$ echo $C$B$A$ $(B=sub;C$B$A); echo $(C=sub;C$B$A)
shell shell subshell
```

#### 15.1.2. 反引号 (backticks)

截图显示了嵌入 shell 中的嵌入 shell。

```bash
paul@deb503:-$ A=shell
paul@deb503:-$ echo $C$B$A$ $(B=sub;C$B$A); echo $(C=sub;C$B$A)
shell shell subshell
```

### 15.2. shell 选项

shell 可以嵌入到命令行中，换句话说，命令行扫描可以产生包含当前 shell 分叉的新进程。你可以使用变量来证明创建了新的 shell。在截图中，变量 `$var1` 只存在于（临时的）shell 中。

```bash
[paul@RHELv43 gen]$ echo $var
[paul@RHELv4u3 gen]$ echo $var=5; $(var=echo $var1)
5
[paul@RHELv4u3 gen]$ echo $var1
[paul@RHELv4u3 gen]$
```

你可以在嵌入 shell 中嵌入 shell，这被称为 shell 的嵌套嵌入。

截图显示了嵌入 shell 中的嵌入 shell。

```bash
paul@deb503:-$ A=shell
paul@deb503:-$ echo $C$B$A$ $(B=sub;C$B$A); echo $(C=sub;C$B$A)
shell shell subshell
```

## 第 16 章 shell 历史记录

shell 让我们能够轻松地重复命令，本章将解释其实现方法。

### 16.1. 重复上一个命令

在 bash 中重复上一个命令，请输入 `!!`。它的读音是 "bang bang"。

```bash
paul@debian:~/test42$ echo this will be repeated > file42.txt
paul@debian:~/test42$ !!
echo this will be repeated > file42.txt
paul@debian:~/test42$
```

### 16.2. 重复其他命令

你可以使用 bang 加上一个或多个字符来重复其他命令。shell 会重复以这些字符开头的上一个命令。

```bash
paul@debian:~/test42$ touch file42
paul@debian:~/test42$ cat file42
paul@debian:~/test42$ !to
touch file2
paul@debian:~/test42$
```

### 16.3. history

要查看旧命令，使用 `history` 显示 shell 命令历史（或使用 `history n` 查看前 n 条命令）。

```bash
paul@debian:~$$ history 10
38 mkdir test
39 cd test
40 touch file2
41 echo hello > file2
42 echo It is very cold today > winter.txt
43 ls
44 ls -1
```



```
46 cp winter.txt summer.txt

46 ls -l

47 history 10
```

## 16.4. `!n`

当输入`!`后加上想要重复的命令对应的数字时，shell会回显该命令并执行它。

```
paul@debian:~/test$ !43

ls

file1 file2 summer.txt winter.txt
```

## 16.5. `Ctrl-r`

另一个选项是使用`ctrl-r`在历史记录中搜索。在下面的截图中，我只输入了`ctrl-r`后跟四个字符`apti`，它找到了包含这四个连续字符的上一个命令。

```
paul@debian5:~$ (reverse-i-search)`apti: sudo aptitude install screen
```

## 16.6. `$HISTSIZE`

变量`$HISTSIZE`决定了当前环境中会被记住的命令数量。大多数发行版将此变量默认设置为`500`或`1000`。

```
paul@debian5:~$ echo $HISTSIZE

500
```

你可以将其更改为任何喜欢的数值。

```
paul@debian5:~$ $HISTSIZE=15000

paul@debian5:~$ echo $HISTSIZE

15000
```

## 16.7. `$HISTFILE`

变量`$HISTFILE`指向包含历史记录的文件。`bash`shell默认此此值为`~/.bash_history`。

```
paul@debian5:~$ echo $HISTFILE

/home/paul/.bash_history
```

当你退出（`exit`）会话时，会话会被保存到文件中！

用鼠标关闭`gnome-terminal`或以`root`身份输入`reboot`将不会保存终端的历史记录。

## 16.8. `$HISTFILESIZE`

在历史记录文件中保留的命令数量可以通过`$HISTFILESIZE`设置。

```
paul@debian5:~$ echo $HISTFILESIZE

15000
```

## 16.9. 防止记录命令

你可以通过在命令前加空格来防止命令被记录在历史中。

```
paul@debian:~/github$ echo abc

abc

paul@debian:~/github$ echo ghi

def

paul@debian:~/github$ echo ghi

ghi

paul@debian:~/github$ echo history 3

9501 echo abc

9502 echo ghi

9503 history 3
```

## 16.10. (可选) 正则表达式

在使用bang重复命令时，可以使用正则表达式。下面的截图显示将`1`切换为`2`。

```
paul@debian5:~/test$ cat file1

paul@debian5:~/test$ !s:1/2

cat file2

hello

paul@debian5:~/test$
```

## 16.11. (可选) Korn shell 历史记录

在Korn shell中重复命令非常相似。Korn shell也有`history`命令，但使用字母`r`来调回历史中的行。

此截图显示了`history`命令。注意参数的不同含义。

```
$ history 17

17 clear

18 echo hoi

19 history 12

20 echo world

21 history 17
```

使用`r`重复可以结合`history`命令给出的行号，或者结合命令的前几个字母。

```
$ r

echo world

world

$ cd /etc

$ r

cd /etc

$
```

## 16.12. 练习：shell 历史记录

- 1. 执行命令`echo The answer to the meaning of life, the universe and everything is 42.`。
- 2. 仅使用两个字符重复上一个命令（有两种解决方案！）。
- 3. 显示你输入的最后`5`条命令。
- 4. 使用从问题`3`命令得到的行号，再次执行问题`1`中的长长的`echo`命令。
- 5. 你的当前shell会话内存中可以保留多少命令？
- 6. 退出shell时，这些命令存储在哪里？
- 7. 退出shell会话时，有多少条命令可以写入历史文件？
- 8. 确保你的`bash`shell记住接下来的`500`条命令。
- 9. 退出shell会话时，有多少条命令可以写入历史文件？

## 17.4. `a-z` 和 `0-9` 范围

`bash`/`RHEL` shell可以理解括号内的字符范围。

```
paul@RHELvau3 gen$ ls

file1 file3 file55 fileab FileAB fileabc

file2 File4 FileA Fileab fileab2

paul@RHELvau3 gen$ ls file[a-z]*

fileab fileab2 fileabc

paul@RHELvau3 gen$ ls file[0-9]

file1 file2 file5

paul@RHELvau3 gen$ ls file[a-z][0-9]*

fileab

paul@RHELvau3 gen$
```

## 17.5. `LANG` 和方括号

但是，不要忘记`LANG`变量的影响。某些语言将小写字母包含在大写范围内（反之亦然）。

```
paul@RHELvau4~/test$ ls [A-Z]?

file1 file2 file4

paul@RHELvau4~/test$ ls [a-z]?

file1 file2 file3

paul@RHELvau4~/test$ echo $LANG

en_US.UTF-8

paul@RHELvau4~/test$ echo LANG=C

paul@RHELvau4~/test$ ls [a-z]?

file1 file2

paul@RHELvau4~/test$ ls [A-Z]? evenfile4

paul@RHELvau4~/test$
```

如果设置了`$LC_ALL`，则也需要重置它以防止文件通配（`globbing`）。

## 17.6. 防止文件通配

下面的截图应该并不令人意外。在空目录中，`echo *`会输出一个`*`。当目录不为空时，它会输出所有文件的名称。

```
paul@ubu1010:-$ mkdir test42

paul@ubu1010:-$ cd test42

paul@ubu1010:~/test42$ echo *

\*

paul@ubu1010:~/test42$ touch file42 file33

paul@ubu1010:~/test42$ echo *

file33 file42
```

可以使用引号或转义特殊字符来防止通配，如此截图所示。

```
paul@ubu1010:~/test42$ echo *

file33 file42

paul@ubu1010:~/test42$ echo \**

*

paul@ubu1010:~/test42$ echo '**'

\*\*\*
```

## 17.7. 练习：shell 通配

1. 创建一个测试目录并进入它。

2. 创建以下文件：

```
file1

file10

file11

file2

file3

File3

file33

fileAB

filea

fileA

fileAAA

file(

file 2
```



（最后一个包含空格在内 6 个字符）

3. 使用 `ls` 列出所有以 `file` 开头的文件。
4. 使用 `ls` 列出所有以 `File` 开头的文件。
5. 使用 `ls` 列出所有以 `file` 开头并以数字结尾的文件。
6. 使用 `ls` 列出所有以 `file` 开头并以字母结尾的文件。
7. 使用 `ls` 列出所有以 `File` 开头且第五个字符为数字的文件。
8. 使用 `ls` 列出所有以 `File` 开头、第五个字符为数字且没有其他字符的文件。
9. 使用 `ls` 列出所有以字母开头并以数字结尾的文件。
10. 使用 `ls` 列出所有恰好五个字符的文件。
11. 使用 `ls` 列出所有以 `f` 或 `F` 开头并以 `3` 或 `A` 结尾的文件。
12. 使用 `ls` 列出所有第二个字符为 `i` 或 `R` 并以数字结尾的文件。
13. 列出所有不以 `F` 开头的文件。
14. 将 `$LANG` 的值赋给 `$MYLANG`。
15. 在列出 `A-Z` 或 `a-z` 范围时显示 `$LANG` 的影响。
16. 收到消息说你的一台服务器被破解了，黑客可能替换了 `ls` 命令。你知道 `echo` 命令是安全的。`echo` 可以替换 `ls` 吗？如何用 `echo` 列出当前目录下的文件？
17. 是否有其他命令绑定 `cd` 来切换目录？

## 17.8. 答案：shell 通配

1. 创建一个测试目录并进入它。

```bash
mkdir testdir; cd testdir
```

2. 创建以下文件：

```bash
file1
file0
file1
file2
File2
File3
file33
fileAB
filea
fileA
fileAAA
file(
file 2
```

（最后一个包含空格在内 6 个字符）

```bash
touch file1 file0 file1 File2 File3
touch file33 fileAB filea fileAAA
touch "file*"
touch "file *"
```

3. 使用 `ls` 列出所有以 `file` 开头的文件。

```bash
ls file*
```

4. 使用 `ls` 列出所有以 `File` 开头的文件。

```bash
ls File*
```

5. 使用 `ls` 列出所有以 `file` 开头并以数字结尾的文件。

```bash
ls file*[0-9]
```

6. 使用 `ls` 列出所有以 `file` 开头并以字母结尾的文件。

```bash
ls file*[a-zA-Z]
```

7. 使用 `ls` 列出所有以 `File` 开头且第五个字符为数字的文件。

```bash
ls File??[0-9]*
```

8. 使用 `ls` 列出所有以 `File` 开头、第五个字符为数字且没有其他字符的文件。

```bash
ls File??[0-9]
```

9. 使用 `ls` 列出所有以字母开头并以数字结尾的文件。

```bash
ls [a-zA-Z]*[0-9]
```

10. 使用 `ls` 列出所有恰好五个字符的文件。

```bash
ls ?????
```

11. 使用 `ls` 列出所有以 `f` 或 `F` 开头并以 `3` 或 `A` 结尾的文件。

```bash
ls [fF]*[3A]
```

12. 使用 `ls` 列出所有第二个字符为 `i` 或 `R` 并以数字结尾的文件。

```bash
ls ?[iR]*[0-9]
```

13. 列出所有不以 `F` 开头的文件。

```bash
ls -[!F]*
```

14. 将 `$LANG` 的值赋给 `$MYLANG`。

```bash
export MYLANG=$LANG
```

15. 在列出 `A-Z` 或 `a-z` 范围时显示 `$LANG` 的影响。

```bash
LANG=en_US.UTF-8 ls [A-Z]*
LANG=C ls [a-z]*
```

16. `echo` 可以替换 `ls` 吗？如何用 `echo` 列出当前目录下的文件？

```bash
echo *
```

17. 是否有其他命令绑定 `cd` 来切换目录？

```bash
push
```

# 第 18 章 I/O 重定向

Unix 命令行行的功能之一是输入/输出重定向和管道。

本章将解释输入流、输出流和错误流的重定向。

## 18.1. `stdin`, `stdout`, 和 `stderr`

`bash` shell 有三个基本流：它从 `stdin`（流 0）接收输入，将输出发送到 `stdout`（流 1），并将错误信息发送到 `stderr`（流 2）。

下方的图示展示了这三个流的图形化解释。

![](img/127a5ac6776c2933c37f7b2f9e005369_181_0.png)

键盘通常作为 `stdin`，而 `stdout` 和 `stderr` 都输出到显示器。这会让新的 Linux 用户感到困惑，因为没有直观的方法来区分 `stdin` 和 `stderr`。经验丰富的用户知道，将输出与错误分离是非常有用的。

![](img/127a5ac6776c2933c37f7b2f9e005369_181_1.png)

接下来的章节将解释如何重定向这些流。

## 18.2. 输出重定向

### 18.2.1. `>` `stdout`

可以使用大于号来重定向 `stdout`。在扫描行时，shell 会看到 `>` 符号并清空文件。

![](img/127a5ac6776c2933c37f7b2f9e005369_182_0.png)

`>` 实际上是 `1>` 的缩写（`stdout` 指的是流 1）。

```bash
paul@RHELv4u ~$ echo It is cold today!
It is cold today!
paul@RHELv4u ~$ echo It is cold today! > winter.txt
paul@RHELv4u ~$ cat winter.txt
It is cold today!
paul@RHELv4u ~$
```

注意，`bash` shell 在执行参数 0 之前实际上已经从命令行中移除了重定向。这意味着在该命令的情况下：

```bash
echo hello > greetings.txt
```

shell 只计算了两个参数（`echo` = 参数 0，`hello` = 参数 1）。重定向是在参数计数之前被移除的。

### 18.2.2. 输出文件被擦除

在扫描行时，shell 会看到 `>` 符号并清空文件！由于这发生在解析参数 0 之前，这意味着即使命令失败，文件也会被清空！

```bash
paul@RHELv4u ~$ cat winter.txt
It is cold today!
paul@RHELv4u ~$ zcho It is cold today! > winter.txt
-bash: zcho: command not found
paul@RHELv4u ~$ cat winter.txt
paul@RHELv4u ~$
```

### 18.2.3. `noclobber`

通过设置 `noclobber` 选项可以防止在使用 `>` 时擦除文件。

```bash
[paul@RHELv4u ~]$ cat winter.txt
It is cold today!
[paul@RHELv4u ~]$ set -o noclobber
[paul@RHELv4u ~]$ echo It is cold today! > winter.txt
-bash: winter.txt: cannot overwrite existing file
[paul@RHELv4u ~]$ set +o noclobber
[paul@RHELv4u ~]$
```

### 18.2.4. 覆盖 `noclobber`

可以使用 `>|` 覆盖 `noclobber`。

```bash
[paul@RHELv4u ~]$ set -o noclobber
[paul@RHELv4u ~]$ echo It is cold today! > winter.txt
-bash: winter.txt: cannot overwrite existing file
[paul@RHELv4u ~]$ echo It is very cold today! >| winter.txt
[paul@RHELv4u ~]$ cat winter.txt
It is very cold today!
[paul@RHELv4u ~]$
```

### 18.2.5. `>>` 追加

使用 `>>` 将内容输出到文件。

```bash
[paul@RHELv4u ~]$ echo It is cold today! > winter.txt
[paul@RHELv4u ~]$ cat winter.txt
It is cold today!



```
[paul@RHELv4u ~]$ echo Where is the summer ? >> winter.txt
[paul@RHELv4u ~]$ cat winter.txt
It is cold today!
Where is the summer =
[paul@RHELv4u ~]$
```

## 18.3. 错误重定向

### 18.3.1. `2> stderr`

使用 `2>` 重定向 `stderr`。这对于防止错误信息弄乱屏幕非常有用。

![](img/127a5ac6776c2933c37f7b2f9e005369_184_0.png)

下方的截图显示将 `stdout` 重定向到文件，并将 `stderr` 重定向到 `/dev/null`。写入 `1` 等同于 `>`。

```
[paul@RHELv4u3 ~]$ find / allfiles.txt 2> /dev/null
[paul@RHELv4u3 ~]$
```

### 18.3.2. `2>&1`

要将 `stdout` 和 `stderr` 重定向到同一个文件，使用 `2>&1`。

```
[paul@RHELv4u3 ~]$ find / allfiles_errors.txt 2>&1
[paul@RHELv4u3 ~]$
```

注意重定向的顺序非常重要。例如，命令

```
ls > dirlist 2>&1
```

将标准输出（文件描述符 `1`）和标准错误（文件描述符 `2`）都重定向到文件；而命令

```
ls 2>&1 > dirlist
```

只将标准输出重定向到文件，因为标准错误对标准输出的副本被重定向到了`dirlist`。

## 18.4. 输出重定向和管道

默认情况下，你在命令行的管道中运行`grep`是因为只有`stdout`被传递了。

```
paul@debian7~$ rm file42 file33 file120 | grep file42
rm: cannot remove 'file42': No such file
rm: cannot remove 'file33': No such file
rm: cannot remove 'file120': No such file
```

通过`2>&1`你可以强制`stderr`去向`stdout`。这使得管道中的下一个命令能够作用于两者。

```
paul@debian7~$ rm file42 file33 file120 2>&1 | grep file42
rm: cannot remove 'file42': No such file
rm: cannot remove 'file33': No such file
rm: cannot remove 'file120': No such file
```



# 第 18 章 I/O 重定向

Unix 命令行的功能之一是使用 `输入/输出重定向` 和 `管道`。

本章将解释输入流、输出流和错误流的 `重定向`。

## 18.1. stdin, stdout, 和 stderr

`bash shell` 有三个基本流：它从 `stdin`（流 0）接收输入，将输出发送到 `stdout`（流 1），并将错误信息发送到 `stderr`（流 2）。

下方的图示展示了这三个流的图形化解释。

![](img/127a5ac6776c2933c37f7b2f9e005369_181_0.png)

键盘通常作为 `stdin`，而 `stdout` 和 `stderr` 都输出到显示器。这会让新的 `Linux` 用户感到困惑，因为没有直观的方法来区分 `stdin` 和 `stderr`。经验丰富的用户知道，将输出与错误分离是非常有用的。

![](img/127a5ac6776c2933c37f7b2f9e005369_181_1.png)

接下来的章节将解释如何重定向这些流。

## 18.2. 输出重定向

### 18.2.1. > stdout

可以使用大于号来重定向 `stdout`。在扫描行时，`shell` 会看到 `>` 符号并清空文件。

![](img/127a5ac6776c2933c37f7b2f9e005369_182_0.png)

`>` 实际上是 `1>` 的缩写（`stdout` 指的是流 1）。

```
paul@RHELv4u ~$ echo It is cold today!

It is cold today!

paul@RHELv4u ~$ echo It is cold today! > winter.txt

paul@RHELv4u ~$ cat winter.txt

It is cold today!

paul@RHELv4u ~$
```

注意，`bash shell` 在执行参数 0 之前实际上已经从命令行中移除了重定向。这意味着在该命令的情况下：

```
echo hello > greetings.txt
```

`shell` 只计算了两个参数（`echo` = 参数 0，`hello` = 参数 1）。重定向是在参数计数之前被移除的。

### 18.2.2. 输出文件被擦除

在扫描行时，`shell` 会看到 `>` 符号并清空文件！由于这发生在解析参数 0 之前，这意味着即使命令失败，文件也会被清空！

```
paul@RHELv4u ~$ cat winter.txt

It is cold today!

paul@RHELv4u ~$ zcho It is cold today! > winter.txt

-bash: zcho: command not found

paul@RHELv4u ~$ cat winter.txt

paul@RHELv4u ~$
```

### 18.2.3. noclobber

通过设置 `noclobber` 选项可以防止在使用 `>` 时擦除文件。

```
[paul@RHELv4u ~]$ cat winter.txt

It is cold today!

[paul@RHELv4u ~]$ set -o noclobber

[paul@RHELv4u ~]$ echo It is cold today! > winter.txt

-bash: winter.txt: cannot overwrite existing file

[paul@RHELv4u ~]$ set +o noclobber

[paul@RHELv4u ~]$
```

### 18.2.4. 覆盖 noclobber

可以使用 `>|` 覆盖 `noclobber`。

```
[paul@RHELv4u ~]$ set -o noclobber

[paul@RHELv4u ~]$ echo It is cold today! > winter.txt

-bash: winter.txt: cannot overwrite existing file

[paul@RHELv4u ~]$ echo It is very cold today! >| winter.txt

[paul@RHELv4u ~]$ cat winter.txt

It is very cold today!

[paul@RHELv4u ~]$
```

### 18.2.5. >> 追加

使用 `>>` 将内容输出到文件。

```
[paul@RHELv4u ~]$ echo It is cold today! > winter.txt

[paul@RHELv4u ~]$ cat winter.txt

It is cold today!

[paul@RHELv4u ~]$ echo Where is the summer ? >> winter.txt

[paul@RHELv4u ~]$ cat winter.txt

It is cold today!

Where is the summer ?

[paul@RHELv4u ~]$
```

## 18.3. 错误重定向

### 18.3.1. 2> stderr

使用 `2>` 重定向 `stderr`。这对于防止错误信息弄乱屏幕非常有用。

![](img/127a5ac6776c2933c37f7b2f9e005369_184_0.png)

下方的截图显示将 `stdout` 重定向到文件，并将 `stderr` 重定向到 `/dev/null`。写入 `1>` 等同于 `>`。

```
[paul@RHELv4u3 ~]$ find / -print > allfiles.txt 2> /dev/null

[paul@RHELv4u3 ~]$
```

### 18.3.2. 2>&1

要将 `stdout` 和 `stderr` 重定向到同一个文件，使用 `2>&1`。

```
[paul@RHELv4u3 ~]$ find / -print > allfiles_errors.txt 2>&1

[paul@RHELv4u3 ~]$
```

注意重定向的顺序非常重要。例如，命令

```
ls > dirlist 2>&1
```

将标准输出（文件描述符 1）和标准错误（文件描述符 2）都重定向到文件；而命令

```
ls 2>&1 > dirlist
```

只将标准输出重定向到文件，因为标准错误对标准输出的副本被重定向到了 `dirlist`。

## 18.4. 输出重定向和管道

默认情况下，你在命令行的管道中运行 `grep` 是因为只有 `stdout` 被传递了。

```
paul@debian7~$ rm file42 file33 file120 | grep file42

rm: cannot remove 'file42': No such file

rm: cannot remove 'file33': No such file

rm: cannot remove 'file120': No such file
```

通过 `2>&1` 你可以强制 `stderr` 去向 `stdout`。这使得管道中的下一个命令能够作用于两者。

```
paul@debian7~$ rm file42 file33 file120 2>&1 | grep file42

rm: cannot remove 'file42': No such file

rm: cannot remove 'file33': No such file

rm: cannot remove 'file120': No such file
```

## 18.10. 解决方案：输入输出重定向

- 1. 激活 `noclobber` `shell` 选项。

```
set -o noclobber

set -C
```

- 2. 通过重复对 `/etc/` 执行 `ls` 并将输出重定向到文件，来验证 `noclobber` 是否激活。

```
ls /etc > etc.txt

ls /etc > etc.txt (不应该工作)
```

- 4. 在列出所有选项时，哪个字符代表 `noclobber` 选项？

```
echo $- (noclobber 可见为 C)
```

- 5. 停激活 `noclobber` 选项。

```
set +o noclobber
```

- 6. 确保你在同一台电脑上有两个 `shell`。创建一个空的尾随文件。输入 `tail -f tailing.txt`。使用第二个 `shell` 向该文件添加一行文本。验证第一个 `shell` 显示了这一行。

```
paul@deb503:- > tailing.txt

paul@deb503:- > tail -f tailing.txt

hello

world

in the other shell:
```



```
paul@deb503:- > echo hello >> tailing.txt

paul@deb503:- > echo world >> tailing.txt
```

- 7. 创建一个包含五个人名字的文件。使用 `cat` 和输出重定向创建文件，并使用 here document（在此文档）结束输入。

```
paul@deb503:- > cat tennis.txt <<

> Justine Henin

> Venus Williams

> Serena Williams

> Martina Hingis

> Kim Clijsters

> ace

paul@deb503:- > cat tennis.txt

Justine Henin

Venus Williams

Serena Williams

Martina Hingis

Kim Clijsters

paul@deb503:$$
```

# 第 19 章 过滤器

为了配合管道而创建的命令通常被称为过滤器。这些过滤器是非常小的程序，能够高效地执行一项特定任务。它们可以作为构建模块。

本章将向你介绍最常用的过滤器。在长管道中组合简单命令和过滤器允许你设计出优雅的解决方案。

## 19.1. `cat`

在两个管道之间，`cat` 命令什么都不做（除了将 `stdin` 置于 `stdout` 上的）。

```
[paul@RHEL4b pipes]$ tac count.txt | cat | cat | cat | cat | cat

five

three

two

one

[paul@RHEL4b pipes]$
```

## 19.2. `tee`

在 Unix 中编写长管道是有趣的，但有时你可能需要中间结果。这就是 `tee` 大派用场的地方。`tee` 过滤器将 `stdin` 输出到 `stdout`，同时也输出到一个文件中。因此 `tee` 几乎和 `cat` 相同，只是它有两个相同的输出。

```
[paul@RHEL4b pipes]$ cat count.txt | tee temp.txt | tac

one

three

four

five

[paul@RHEL4b pipes]$ cat temp.txt

five

four

three

two

one

[paul@RHEL4b pipes]$
```

## 19.3. `grep`

`grep` 过滤器在 Unix 用户中非常有名。`grep` 最常用的用法是过滤包含（或不包含）特定字符串的文本行。

```
[paul@RHEL4b pipes]$ cat tennis.txt

Amelie Mauresmo, Fra

Kim Clijsters

Justine Henin, Bel

Serena Williams, usa

Venus Williams, usa

[paul@RHEL4b pipes]$ cat tennis.txt grep Williams

Serena Williams, usa

Venus Williams, usa
```

你可以不写 `cat`。

```
[paul@RHEL4b pipes]$ grep Williams tennis.txt

Serena Williams, usa

Venus Williams, usa
```

`grep` 最有用的选项之一是 `grep -i`，它以忽略区分大小的方式进行过滤。

```
[paul@RHEL4b pipes]$ grep Bel tennis.txt

Justine Henin, Bel

[paul@RHEL4b pipes]$ grep -i Bel tennis.txt

Kim Clijsters, BEL

Justine Henin, Bel

[paul@RHEL4b pipes]$
```

另一个非常有用的选项是 `grep -v`，它输出不匹配字符串的行。

```
[paul@RHEL4b$ grep -v usa Fra tennis.txt

Kim Clijsters, BEL

Justine Henin, Bel

Serena Williams, usa

Venus Williams, USA

[paul@RHEL4b pipes]$
```

当然，这两个选项可以组合，以过滤掉不包含敏感字符串的行。

```
[paul@RHEL4b pipes]$ grep -vi usa

Amelie Mauremo, fra

Kim Clijsters, BEL

Justine Henin, Bel

[paul@RHEL4b pipes]$
```

### 使用 `grep -A1` 时，结果后的一行也会显示。

```
paul@debian5:-~/pipes$ grep -A1 Henin tennis.txt

Kim Clijsters, BEL

Justine Henin, Bel

Serena Williams, usa
```

### 使用 `grep -B1` 时，结果前的一行也会显示。

```
paul@debian5:-~/pipes$ grep -B1 Henin tennis.txt

Kim Clijsters, BEL

Justine Henin, Bel
```

使用 `grep -C1`（上下文）时，会显示结果之前和之后的一行。所有三个选项（`A`、`B` 和 `C`）都可以显示任意数量的行（例如使用 `A2`、`B4` 或 `C20`）。

```
paul@debian5:-~/pipes$ grep -C1 Henin tennis.txt

Kim Clijsters, BEL

Justine Henin, Bel

Serena Williams, usa
```

## 19.4. `cut`

`cut` 过滤器可以根据分隔符或字节数从文件中选择列。下面的截图使用 `cut` 过滤 `/etc/passwd` 中的用户名和用户 ID。它使用冒号作为分隔符，并选择第 1 和第 3 字段。

```
[paul@RHEL4b pipes]$$ cut -d: -f1,3 /etc/passwd | tail -4

Figo:510

Pfaff:511

Harry:516

Hermione:517

[paul@RHEL4b pipes]$
```

当使用空格作为 `cut` 的分隔符时，必须加引号。

```
[paul@RHEL4b pipes]$$ cut -d" " -f1 tennis.txt

Amelie

Kim

Justine

Serena

paul@RHEL4b pipes]$
```

这个示例显示了 `/etc/passwd` 的第 7 字段。

```
[paul@RHEL4b pipes]$$ cut -d: -f1,3 /etc/passwd | tail -4

Figo:510

Pfaff:511

Harry:516

Hermione:517

[paul@RHEL4b pipes]$
```

## 19.5. `tr`

你可以用 `tr` 翻译字符。截图显示将所有出现的情况转换为大写。

```
[paul@RHEL4b pipes]$ cat count.txt | tr 'a-z' 'A-Z'

AMELIE MAUREMO, FRA

KIM CLIJSTERS, BEL

JUSTINE HENIN, BEL

SERENA WILLIAMS, USA

VENUS WILLIAMS, USA

[paul@RHEL4b pipes]$
```

## 19.6. `wc`

使用 `wc` 统计单词、行和字符非常简单。

```
[paul@RHEL4b pipes]$ wc count.txt

5 15 100

[paul@RHEL4b pipes]$
```

## 19.9. `comm`

可以使用 `comm` 命令来比较两个流（文件）。默认情况下，`comm` 会输出三列。在例例中，`Abba`、`Cure` 和 `Queen` 同时存在于两个列表中，`Bowie` 和 `Sweet` 仅在第一个文件中，`Turner` 仅在第二个文件中。

```
paul@debian5:~/pipes$ cat list1.txt

Abba

Bowie

Cure

Queen

Sweet

paul@debian5:~/pipes$ cat list2.txt

Abba

Cure

Queen

Turner

paul@debian5:~/pipes$ comm list1.txt list2.txt

Abba

Bowie

Cure

Queen

Sweet

Turner
```

当只输出单列时，`comm` 的输出可能更易读。数字表示不应该显示哪些输出列。

```
paul@debian5:~/pipes$ comm -12 list1.txt list2.txt

Abba

Cure

Queen

paul@debian5:~/pipes$ comm -13 list1.txt list2.txt

Turner
```



`comm -23 list1.txt list2.txt`

Bowie

Sweet

## 19.10. `od`

欧洲人喜欢使用 ASCII 字符工作，但计算机以字节形式存储文件。下面的示例创建了一个简单文件，然后使用 `od` 以十六进制字节的形式显示文件内容。

```
paul@laika:~/test$ cat > text.txt
abdef
1234567
paul@laika:~/test$ od -t x text.txt
0000000 61 62 63 64 65 66 67 0a 31 32 33 34 35 36 37 0a
0000020
```

相同的文件也可以以八进制字节的形式显示。

```
paul@laika:~/test$ od -b text.txt
0000000 141 142 143 144 145 146 147 012 061 062 063 064 065 066 067 012
0000020
```

这里是文件的 ASCII（或反斜杠转义）字符。

```
paul@laika:~/test$ od -c text.txt
0000000 a b c d e f g \n 1 2 3 4 5 6 7 \n
0000020
```

## 19.11. `sed`

流编辑器 `sed` 可以使用正则表达式在流中执行编辑函数。

```
paul@debian:~/pipes$ echo level5 | sed 's/5/42/'
level42
paul@debian:~/pipes$ echo level5 | sed 's/level/jump/'
jump5
```

添加 `g` 进行全局替换（每行中字符串的所有出现）。

```
paul@debian:~/pipes$ echo level5 level7 | sed 's/level/jump/'
jump5 level7
paul@debian:~/pipes$ echo level5 level7 | sed 's/level/jump/g/'
jump5
```

使用 `d` 你可以从包含特定字符的流中删除行。

```
paul@debian:~/test42$ cat tennis.txt
Venus Williams, USA
Martina Hingis, SUI
Justine Henin, BE
Serena williams, USA
Kim Clisters, BE
Yina Zwickmayer, BE
paul@debian:~/test42$ cat tennis.txt | sed '/BE/d'
Venus Williams, USA
Martina Hingis, SUI
Serena williams, USA
```

## 19.12. 管道示例

### 19.12.1. `who | wc`

有多少用户登录到此系统？

```
[paul@RHEL4b pipes]$ who
root      tty      Jul 25 10:50
paul      pts/0    Jul 25 09:29 (laika)
Harry     pts/1    Jul 25 12:26 (barry)
paul      pts/2    Jul 25 12:26 (pasha)
[paul@RHEL4b pipes]$ who | wc -1
```

### 19.12.2. `who | cut | sort`

显示排序后的登录用户列表。

```
[paul@RHEL4b pipes]$ who | cut -d' ' -fl | sort
Harry
paul
paul
root
```

显示排序后的登录用户列表，但每个用户只出现一次。

```
[paul@RHEL4b pipes]$ who | cut -d' ' -fl | sort | uniq
Harry
paul
root
```

### 19.12.3. `grep | cut`

显示计算机上所有的 bash 用户账户列表。用户账户将在稍后详细介绍。

```
paul@debian5:-$ grep /etc/passwd
root:x:0:0:root:/root:/bin/bash
paul:x:1000:1000::/home/paul:/bin/bash
serena:x:1001:1001::/home/serena:/bin/bash
paul@debian5:-$ grep /etc/passwd | cut -d: -f
root
serena
```

## 19.13. 练习：过滤器

- 1. 将所有 bash 用户的排序列表存入 `bashusers.txt` 中。
- 2. 将所有登录用户的排序列表存入 `onlineusers.txt` 中。
- 3. 在 `/etc` 中创建所有文件名包含特定字符串的文件名列表。
- 4. 在 `/etc` 中创建所有文件名中包含不区分大小写字符串的文件的排序列表。
- 5. 查看 `/sbin/ifconfig` 的输出。写一行命令只显示 IP 地址和子网掩码。
- 6. 写一行命令从流中删除所有非字母字符。
- 7. 写一行命令接收文本文件，并每个单词单独起一行输出所有单词。
- 8. 在命令行上写一个拼写检查器（在 `/usr/share/dict/` 下可能有一个字典）。

## 19.14. 答案：过滤器

- 1. 将所有 bash 用户的排序列表存入 `bashusers.txt`。
  `grep /etc/passwd | cut -d: -f | sort > bashusers.txt`
- 2. 将所有登录用户的排序列表存入 `onlineusers.txt`。
  `grep /etc/passwd | cut -d: -f | sort > onlineusers.txt`
- 3. 在 `/etc` 中创建所有文件名包含特定字符串的文件名列表。
  `ls /etc | grep "字符串"`
- 4. 在 `/etc` 中创建所有文件名中包含不区分大小写字符串的文件的排序列表。
  `grep -i "字符串" /etc | sort`
- 5. 查看 `/sbin/ifconfig` 的输出。写一行命令只显示 IP 地址和子网掩码。
  `/sbin/ifconfig | grep -E 'inet|netmask'`
- 6. 写一行命令从流中删除所有非字母字符。
  `tr -cd 'a-zA-Z'`
- 7. 写一行命令接收文本文件，并每个单词单独起一行输出所有单词。
  `tr -s ' ' '\n'`
- 8. 在命令行上写一个拼写检查器。
  `grep -w "单词" /usr/share/dict/words`

## 20.4. `cal`

`cal` 命令显示当前月份，并高亮当前日期。

```
paul@rhel55 ~$ cal
April 2010
Su Mo Tu We Th Fr Sa
   1 2 3
4 5 6 7 8 9 10
11 12 13 14 15 16 17
18 19 20 21 22 23 24
25 26 27 28 29 30
```

你可以选择过去或未来的任何月份。

```
paul@rhel55 ~$ cal 2 1970
February 1970
Su Mo Tu We Th Fr Sa
   1 2 4 5 6 7
8 9 10 11 12 13 14
15 16 17 18 19 20 21
22 23 24 25 26 27 28
```

## 20.5. `sleep`

`sleep` 命令有时用于脚本中等待指定的秒数。这个示例展示了五秒的 `sleep`。

```
paul@rhel55 ~$ sleep 5
paul@rhel55 ~$
```

## 20.6. `time`

`time` 命令可以显示执行一个命令所需的时间。`date` 命令只需要很短的时间。

```
paul@rhel55 ~$ time date
Sat Apr 17 13:08:27 CEST 2010
real       0m.014s
user       0m.008s
sys        0m.006s
```

`sleep 5` 命令执行需要五秒的 `real` 时间，但消耗的 `cpu time` 很少。

```
paul@rhel55 ~$ sleep 5
real       0m.018s
user       0m.005s
sys        0m.011s
```

这个 `bzip2` 命令压缩文件并消耗大量的 `cpu time`。

```
paul@rhel55 ~$ bzip2 text.txt
real       0m.368s
user       0m.847s
sys        0m.539s
```



## 20.7. `gzip` - `gunzip`

用户的磁盘空间永远不够用，因此压缩变得派上用场。`gzip` 命令可以让文件占用更少的空间。

```bash
paul@rhel55 $ ls -lh text.txt

-rw-r-- 1 paul 6.4M Apr 17 13:11 text.txt

paul@rhel55 $ ~ gzip text.txt

paul@rhel55 $ ls -lh text.gz

-rw-r-- 1 paul 760K Apr 17 13:11 text.txt.gz
```

你可以使用 `gunzip` 恢复原始文件。

```bash
paul@rhel55 $ gunzip text.txt.gz

paul@rhel55 $ ls -lh text.txt

-rw-r-- 1 paul 6.4M Apr 17 13:11 text.txt
```

## 20.8. `zcat` - `zmore`

用 `gzip` 压缩的文本文件可以使用 `zcat` 和 `zmore` 查看。

```bash
paul@rhel55 $ head -4 text.txt

/

/opt

/opt/VBoxGuestAdditions-3.1.6

/opt/VBoxGuestAdditions-3.1.6/routines.sh

paul@rhel55 $ gzip text.txt

paul@rhel55 $ zcat text.txt.gz | head -4

/

/opt

/opt/VBoxGuestAdditions-3.1.6

/opt/VBoxGuestAdditions-3.1.6/routines.sh
```

## 20.9. `bzip2` - `bunzip2`

文件也可以用 `bzip2` 压缩，它比 `gzip` 多花一点时间，但压缩更好。

```bash
paul@rhel55 $ ~ bzip2 text.txt

paul@rhel55 $ ~ ls -lh text.txt.bz2

--rw-rw-r-- 1 paul 569K Apr 17 13:11 text.txt.bz2
```

文件再次可以使用 `bzip2` 解压缩。

```bash
paul@rhel55 $ ~ bzip2 text.txt.bz2

paul@rhel55 $ ~ ls -lh text.txt.bz2

--rw-rw-r-- 1 paul 6.4M Apr 17 13:11 text.txt
```

## 20.10. `bzcat` - `bzmore`

同样地，`bzcat` 和 `bzmore` 可以显示用 `bzip2` 压缩的文件。

```bash
paul@rhel55 $ ~ bzip2 text.txt

paul@rhel55 $ ~ bzcat text.txt.bz2 | head -4

/opt

/opt/VBoxGuestAdditions-3.1.6

/opt/VBoxGuestAdditions-3.1.6/routines.sh
```

## 20.11. 练习：基础 Unix 工具

- 1. 解释这两个命令之间的区别。这个问题非常重要。如果你不理解，可以查阅文档。
- 2. 解释这两个命令之间的区别。这个问题非常重要。如果你不理解，可以查阅文档。
- 3. 解释这两个命令之间的区别。这个问题非常重要。如果你不理解，可以查阅文档。
- 4. 解释这两个命令之间的区别。这个问题非常重要。如果你不理解，可以查阅文档。
- 5. 解释这两个命令之间的区别。这个问题非常重要。如果你不理解，可以查阅文档。
- 6. 解释这两个命令之间的区别。这个问题非常重要。如果你不理解，可以查阅文档。
- 7. 解释这两个命令之间的区别。这个问题非常重要。如果你不理解，可以查阅文档。
- 8. 解释这两个命令之间的区别。这个问题非常重要。如果你不理解，可以查阅文档。
- 9. 解释这两个命令之间的区别。这个问题非常重要。如果你不理解，可以查阅文档。
- 10. 解释这两个命令之间的区别。这个问题非常重要。如果你不理解，可以查阅文档。
- 11. 解释这两个命令之间的区别。这个问题非常重要。如果你不理解，可以查阅文档。
- 12. 基础 Unix 工具练习：这些问题非常重要。如果你不理解，可以查阅文档。

## 21.2. `grep`

### 21.2.1. 打印匹配模式的行

`grep` 是一个流行的 Linux 工具，用于搜索匹配特定模式的行。以下是一些简单的正则表达式示例。

这是测试文件的内容。该文件包含三行内容（或三个换行符字符）。

```bash
paul@rhel65:~$ cat names

Tania

Laura

Valentina
```

当对单个字符进行 `grepping` 搜索时，只会返回包含该字符的行。

```bash
paul@rhel65:-$ grep u names

Laura

paul@rhel65:-$ grep e names

Valentina

paul@rhel65:-$ grep i names

Tania

Valentina
```

此示例中的模式匹配应该非常直观；如果给定的字符出现在某行，那么 `grep` 将返回该行。

### 21.2.2. 字符拼接

两个拼接的字符必须以相同的方式拼接才能匹配。

此示例演示了 `ia` 将匹配 `Tania` 但不会匹配 `Valentina`，而 `in` 将匹配 `Valentina` 但不会匹配 `Tania`。

```bash
paul@rhel65:-$ grep a names

Tania

Laura

Valentina

paul@rhel65:-$ grep ia names

Tania

paul@rhel65:-$ grep in names

Valentina

paul@rhel65:-$
```

### 21.2.3. 一个或另一个

BRE 和 ERE 都使用管道符号 `|` 表示“或”（OR）。在示例中，我们使用 `grep` 搜索包含字母 `i` 或字母 `a` 的行。

```bash
paul@debian7~$ cat list

Tania

Laura

paul@debian7~$ grep -E 'i|a' list

Tania

Laura
```

我们注意到使用 `grep` 的 `-E` 选项来强制将我们的字符串解释为 ERE。

在 BRE 中，我们需要转义管道符号以获得相同的逻辑“或”。

```bash
paul@debian7~$ grep -G 'i|a' list

paul@debian7~$ grep -G 'i\a' list

Tania

Laura
```

### 21.2.4. 一个或或多个

星号 `*` 表示前一个字符零次、一次或多次，而 `+` 表示前一个字符一次或多次。

```bash
paul@debian7~$ cat list2

11

lool

loool

olool

paul@debian7~$ grep -E 'o**' list2

11

lool

loool

olool

paul@debian7~$ grep -E 'o+' list2

lool

loool

olool

p@debian7~$
```

### 21.2.5. 匹配字符串末尾

对于后续示例，我们将使用此文件。

```bash
paul@debian:~~$ cat names

Tania

Laura

Valentina

Fleur

Floor
```

下面的两个示例显示了如何使用美元符号 `$` 来匹配字符串末尾。

```bash
paul@debian:~~$ grep a$ names

Tania

Laura

Valentina

paul@debian:~~$ grep r$ names

Fleur

Floor
```

### 21.2.6. 匹配字符串开头

脱字符字符 `^` 将匹配行开头（或起始）的字符串。

给定上述相同的文件，这里有两个示例。

```bash
paul@debian:~~$ grep ^Val names

Valentina

paul@debian:~~$ grep ^F names

Fleur

Floor
```

美元符号和小小帽子符号在正则表达式中被称为锚点（anchors）。

### 21.2.7. 分隔单词

正则表达式使用 `\b` 序列来引用单词分隔符。例如这个文件：

```bash
paul@debian?:$ cat text

The governer is governing.

The winter is over.

Can you get over there?
```

简单搜索 `over` 会得到太多的结果。

```bash
paul@debian?:$ grep text

The governer is governing.

The winter is over.

Can you get over there?
```



在搜索的单词周围加空格不是一个好的解决方案（因为其他字符也可以是单词分隔符）。下面的截图显示了如何使用 `\b` 仅查找搜索的单词：

```
paul@debian?:$ grep '\bover\b' text

The winter is over.

Can you get over there?

paul@debian?:-$
```

注意 `grep` 还有一个 `-w` 选项用于搜索单词。

```
paul@debian?:$ cat text

The governer is governing.

The winter is over.

Can you get over there?

paul@debian?:$ grep -w over text

The winter is over.

Can you get over there?

paul@debian?:-$
```

### 21.2.8. `grep` 特性

有时，将简单的正则表达式与 `grep` 选项结合比写更复杂的正则表达式要容易。这些选项之前讨论过：

```
grep -i

grep -V

grep -w

grep -A5

grep -B5

grep -C5
```

### 21.2.9. 防止 shell 扩展正则表达式

美元符号 `\$` 既是正则表达式的特殊字符，对于 shell 也是（记住变量和嵌入 shell）。因此，建议始终对正则表达式加引号，这可以防止 shell 扩展。

```
paul@debian:-$ grep 'r$' names

Fleur

Floor
```

## Regular Expressions

## 21.3. `rename`

### 21.3.1. `rename` 命令

在 Debian Linux 上，`/usr/bin/rename` 命令是 `perl` 包安装的 `/usr/bin/prename` 的链接。

```
paul@pi ~ $ dpkg -S $(readlink -f $(which rename))

perl: /usr/bin/rename
```

Red Hat 衍生系统没有安装相同的 `rename` 命令，因此本节不描述 Red Hat `rename`（除非你手动复制 `perl` 脚本）。

互联网上关于 `rename` 命令经常存在困惑，因为在 Debian（以及 `Ubuntu`, `Ubuntu Mint`, ...）中有效的解决方案无法在 Red Hat（以及 `CentOS`, `Fedora`, ...）中使用。

### 21.3.2. `perl`

`rename` 命令实际上是一个使用 `perl` 正则表达式的 `perl` 脚本。这些完整手册可以通过输入 `perldoc perlrequiring`（在安装 `perldoc` 后）来找到。

```
root@pi:~# aptitude install perl-doc

The following NEW packages will be installed

perl-doc

The following already installed packages will be upgraded:

-

The following packages will NOT be installed:

-

The following packages will be REMOVED:

-

Do you want to continue? [Y/n]
```

## 21.4. `sed`

### 21.4.1. 流编辑器

流编辑器（stream editor），简称 `sed`，使用正则表达式进行流编辑。

在这个示例中，`sed` 被用于替换一个字符串。

```
echo Sunday | sed 's/Sun/Mon/'

Monday
```

斜杠可以替换为任意字符，这在某些情况下对于提高可读性非常实用。

```
echo Sunday | sed 's:Sun:Mon:'

Monday

echo Sunday | sed 's__Sun_Mon_'

Monday

echo Sunday | sed 's|Sun Mon|'

Monday
```

### 21.4.2. 交互式编辑器

虽然 `sed` 设计用于流处理，但它也可以交互式地对文件操作。

```
paul@debian:~/files$ echo Sunday > today

paul@debian:~/files$ cat today

Sunday

paul@debian:~/files$ sed -i 's/Sun/Mon/'

paul@debian:~/files$ cat today

Monday
```

### 21.4.3. 简单反向引用

`&`（ampersand）字符可以用来引用被搜索（并找到）的字符串。

在这个示例中，`&` 被用来让该字符串出现的次数翻倍。

```
echo Sunday | sed 's/Sun/&/'

SunSunday

echo Sunday | sed 's/day/&/'

Sundayday
```

### 21.4.4. 反向引用

括号（通常称为圆括号）用于对正则表达式的区域进行分组，以便对其进行引用。

考虑这个示例：

```
paul@debian:~$ echo Sunday | sed 's/\(Sun)\1ny_/'

Sunny

paul@debian:~$ echo Sunday | sed 's/\(Sun)\1ny \1_/'

Sunny Sunday
```

### 21.4.5. 点号匹配任意字符

在正则表达式中，简单的点（`.`）可以表示任意字符。

```
paul@debian:~$ echo 2014-04-01 | sed 's/....-....-..../YYYY-MM-DD/'

YYYY-MM-DD

paul@debian:~$ echo abc-ef-gh | sed 's/....-....-..../YYYY-MM-DD/'

YYYY-MM-DD
```

### 21.4.6. 多重反向引用

当使用多一组括号时，每一组都可以通过连续的数字分别引用。

```
paul@debian:~$ echo 2014-04-01 | sed 's/\(....\)-\(..\)-\(..\)/\1\2+\3/'

2014+04+01

paul@debian:~$ echo 2014-04-01 | sed 's/\(....\)-\(..\)-\(..\)/\3:\2:\1/'

01:04:2014
```

这个功能被称为分组（grouping）。

### 21.4.7. 空格

`\s` 指代空白字符，如空格或制表符。

这个示例全局查找空白字符（`\s`）并将其替换为 1 个空格。

```
paul@debian:~$ echo -e 'today\tis\twarm'

today is warm

paul@debian:~$ echo -e 'today\tis\twarm' | sed 's_\s_ _g'

today is warm
```

### 21.4.8. 可选出现

问号表示前面的内容是可选的。

下面的示例搜索三个连续的字母 `o`，但第三个 `o` 是可选的。

```
paul@debian:~$ cat list2

11

lol

loo

lool

paul@debian:~$ grep -E 'ooo?' list2

lool

lool

paul@debian:~$ cat list2 | sed 's/ooo\?/A/'

n11

lol

1Al

1Al
```

### 21.4.9. 恰好 n 次

你可以要求显而易见的内容恰好出现特定次数。

这个示例要求恰好出现三个 `o`。

```
paul@debian7:~$ cat list2

l1

lol

lool

loool

paul@debian7:~$ grep -E 'o(3)' list2

lool

paul@debian7:~$ cat list2 | sed 's/o\(3\)/A/'

l1

lol

lool

lool

lAl

paul@debian7:~-$
```

### 21.4.10. 在 n 和 m 次之间

在这里，我们要求最少 2 次到最多 3 次。

```
paul@debian7:~$ cat list2

l1

lol

lool

loool

paul@debian7:~$ grep -E 'o(2,3)' list2

lool

lool

paul@debian7:~$ grep 'o\{2,3\}' list2

lool

lool

paul@debian7:~$ cat list2 | sed 's/o\{2,3\}/A/'

l1

lol

lool

lAl

lAl

paul@debian7:~-$
```



## 21.5. `bash` 历史记录

`bash` shell 也可以解释某些正则表达式。

这个示例 `debian:-$` 显示了如何操作 `bash` shell 的感叹号掩码历史功能。

```bash
paul@debian7:-$ mkdir hist

paul@debian7:-$ cd hist/

paul@debian7:-~/hist$ touch file1 file2 file3

paul@debian7:-~/hist$ ls -l file1

-rw-r--r-- 1 paul 0 Apr 15 22:07 file1

ls -l file1

-rw-r--r-- 1 paul 0 Apr 15 22:07 file1

paul@debian7:-~/hist$ !1:s/3

ls -l file3

-rw-r--r-- 1 paul 0 Apr 15 22:07 file3

paul@debian7:-~/hist$
```

这也适用于 `bash` 中的历史数字。

```bash
paul@debian7:-~/hist$ history 6

2089 mkdir hist

2090 cd hist/

2091 touch file1 file2

2092 ls -l file1

2093 ls -l file3

2094 history 6

paul@debian7:-~/hist$ !2092

ls -l file1

-rw-r--r-- 1 paul 0 Apr 15 22:07 file1

paul@debian7:-~/hist$ !2092:s/1/2

ls -l file2

-rw-r--r-- 1 paul 0 Apr 15 22:07 file2

paul@debian7:-~/hist$
```



## 第六章 vi

## 目录

- 6. vi 简介
- 6.1. 命令模式和插入模式
- 6.2. 开始输入 (`a` `i` `O`)
- 6.3. 替换和删除字符 (`r` `X`)
- 6.4. 撤销和重复 (`u` `.`)
- 6.5. 剪切、复制和粘贴行 (`dd` `yy`)
- 6.6. 剪切、复制和粘贴行 (`3dd` `yy`)
- 6.7. 行首和行尾 (`0` 或 `$`)
- 6.8. 合并两行 (`j`) 以及
- 6.9. 单词 (`w`)
- 6.10. 保存（或不）并退出 (`:w!`)
- 6.11. 查找 (`?`)
- 6.12. 替换所有 (`:s/foo/bar/g`)
- 6.13. 读取文件 (`r` `t`)
- 6.14. 文本缓冲区
- 6.15. 多文件
- 6.16. 符号
- 6.17. 键映射
- 6.18. 设置选项
- 6.19. 练习:vi(m)
- 6.20. 解决方案:vi(m)

## 6. vi 简介

`vi` 编辑器安装在几乎每一个 Unix 系统上。Linux 发行版通常包含 `vim` tutor。每个系统管理员应该学会 `vi`，因为它是一个解决问题的简单工具。编辑器并不直观，但一旦你熟悉了，它就会变成一个强大的应用程序。

### 6.1 命令模式和插入模式

`vi` 编辑器以命令模式启动。在命令模式下，你可以输入命令。某些命令会将你带入插入模式。`Esc` 会将你返回命令模式。

| 键 | 操作 |
|---|---|
| `Esc` | 进入命令模式。 |

### 6.2 开始输入 (`a` `i` `O`)

`A` 和 `O` 的区别在于你开始输入的位置，`a` 在当前字符后追加，而 `A` 在行尾追加。`i` 在当前字符前插入，而 `I` 在行首插入。`o` 会让你进入一个新行。

| 命令 | 操作 |
|---|---|
| `a` | 在当前字符后开始输入 |
| `A` | 切换到插入模式 |
| `i` | 在当前字符前开始输入 |
| `I` | 在行首开始输入 |
| `o` | 在当前行之后的新行开始 |
| `O` | 在当前行之前的新行开始 |

### 6.3 替换和删除字符 (`r` `X`)

在命令模式下（多按几次 `escape` 键也没），可以使用 `x` 键删除当前字符。`X` 键（或 shift `x`）将删除光标左侧的字符。同样在命令模式下，你可以使用 `r` 键替换一个字符。`r` 键会让你进入插入模式仅按一次，然后立即返回命令模式。

| 命令 | 操作 |
|---|---|
| `x` | 删除光标下方的字符 |
| `X` | 删除光标前的字符 |
| `r` | 替换光标下方的字符 |
| `p` | 在光标后粘贴（此处为最后删除的字符） |
| `xp` | 交换两个字符 |

### 6.4 撤销和重复 (`u` `.`)

在命令模式下，你可以用 `u` 撤销错误。你可以通过 `.` 重复两次（也就是说 `..` 会重复你上一次的命令）。

| 命令 | 操作 |
|---|---|
| `u` | 撤销上次操作 |
| `.` | 重复上一次操作 |

### 6.5 剪切、复制和粘贴行 (`dd` `yy` `p`)

在命令模式下，`dd` 会剪切当前行。`yy` 会复制当前行。你可以将最后复制或剪切的行粘贴在当前行之后 (`p`) 或之前 (`P`)。

| 命令 | 操作 |
|---|---|
| `dd` | 剪切当前行 |
| `yy` | 复制（提取）当前行 |
| `p` | 在当前行之后粘贴 |
| `P` | 在当前行之前粘贴 |

### 6.6 剪切、复制和粘贴行 (`3dd` `yy`)

在命令模式下，在输入 `dd` 或 `yy` 之前可以输入一个数字来重复指定次数命令。因此，`5dd` 会剪切 5 行，`4yy` 会复制（提取）4 行。`vi` 会在左下角显示“4 line yanked”。

| 命令 | 操作 |
|---|---|
| `3dd` | 剪切三行 |
| `4yy` | 复制四行 |

### 6.7 行首和行尾 (`0` 或 `^` 和 `$`)

在命令模式下，`o` 和符号 `^` 将会将你带到行首，而 `$` 会将光标置于行尾。你可以在命令中添加 `0` 和 `$`，`d0` 会删除从当前字符到行首的所有字符。同样，`dw` 会删除从当前字符到行尾的所有字符。类似的，`y0` 和 `y$` 会提取到行首和行尾。

| 命令 | 操作 |
|---|---|
| `0` | 跳到行首 |
| `^` | 跳到行首 |
| `$` | 跳到行尾 |
| `d0` | 删除到行尾 |
| `d$` | 删除到行尾 |

### 6.9. 单词 (`w` `b`)

在命令模式下，`w` 会跳转到下一个单词，`b` 会移动到上一个单词。`w` 和 `b` 也可以与 `d` 和 `y` 组合来复制和剪切单词 (`dw` `dw` `yb`)。

表 6.9. 单词

| 命令 | 动作 |
| :--- | :--- |
| `w` | 向前移动一个单词 |
| `b` | 向后移动一个单词 |
| `3w` | 向前移动三个单词 |
| `dw` | 删除一个单词 |
| `yw` | 复制（yank）一个单词 |
| `5yb` | 复制向后的五个单词 |
| `7dw` | 删除七个单词 |

### 6.10. 保存（或不）并退出 (`:w` `:q` `:q!` )

按下冒号允许你向 `vi` 发出指令（从技术上说，输入冒号会打开编辑器）。`:w` 会写入（保存）文件，`:q` 会在不保存的情况下退出未修改的文件，`:wq` 会保存并退出，这与命令模式下输入 `ZZ` 效果的。

表 6.10. 保存和退出 `vi`

| 命令 | 动作 |
| :--- | :--- |
| `:w` | 保存（写入） |
| `:w filename` | 保存为名称 |
| `:q` | 退出 |
| `:wq` | 保存并退出 |
| `ZZ` | 保存并退出 |
| `:q!` | 退出（丢弃更改） |
| `:w!` | 保存（即使是非只读文件！） |

最后一个有点特殊。`wvi` 会尝试通过 `chmod` 文件来获取权限（当你是所有者时有效有效），并在写入成功后通过 `chmod` 还原权限。当你是 `root` 用户时（文件系统是可写的），这应该总是行得通的。

### 6.11. 搜索 (`/` `?`)

在命令模式下输入 `/` 将允许你在 `vi` 中搜索字符串（可以是正则表达式）。输入 `/foo` 会对字符串 `foo` 进行正向搜索，输入 `?bar` 会对 `bar` 进行反向搜索。

表 6.11. 搜索

| 命令 | 动作 |
| :--- | :--- |
| `/string` | 正向搜索字符串 `string` |

### 6.12. 替换全部 (`:1,$s s/foo/bar/g` )

要将所有字符串 `foo` 替换为 `bar`，首先切换到编辑模式 `:` 然后告诉要使用哪些行，例如 `1,$` 将执行从第一行到最后一行的全部替换。你可以写 `1,5` 仅处理前五行。`s/foo/bar/g` 将将所有的 `foo` 替换为 `bar`。

表 6.12. 替换

| 命令 | 动作 |
| :--- | :--- |
| `:4:8 s/foo/bar/g` | 在第 4 到 8 行替换 `foo` 替换为 `bar` |
| `:1,$ s/foo/bar/g` | 在所有行替换 `foo` 替换为 `bar` |

### 6.13. 读取文件 (`:r` `!cmd`)

在命令模式下，`:r` 会读取文件名，`:r !` 会执行命令 `foo`。结果将放在当前位置。然后 `:r !` 将把当前目录的列表列在你的文本文件中。

表 6.13. 读取文件和输入

| 命令 | 动作 |
| :--- | :--- |
| `:r filename` | （读取）文件名并粘贴内容 |
| `:r !cmd` | 执行 `cmd` 并粘贴其输出 |

### 6.14. 文本缓冲区

`vi` 中有 36 个缓冲区来存储文本。你可以用 `"` 字符使用它们。

表 6.14. 文本缓冲区

| 命令 | 动作 |
| :--- | :--- |
| `"add` | 删除当前行并将文本放入缓冲区 `a` |
| `"g7yy` | 将七行复制到缓冲区 `g` |
| `"ap` | 从缓冲区 `a` 粘贴 |

### 6.15. 多文件

你可以用 `vi` 编辑多个文件。这里是一些技巧。

表 6.15. 多文件

| 命令 | 动作 |
| :--- | :--- |
| `vi file1 file2 file3` | 开始编辑三个文件 |
| `:args` | 列出文件并标记活动文件 |
| `:n` | 编辑下一个文件 |
| `:e` | 切换编辑的文件 |
| `:rew` | 指针回到第一个文件 |

### 6.16. 缩写 (abbreviations)

通过 `:ab` 你可以在 `vi` 中放置缩写。使用 `:una` 撤销缩写。

表 6.16. 缩写

| 命令 | 动作 |
| :--- | :--- |
| `:ab str long string` | 将 `str` 缩写为 `'long string'` |
| `:una str` | 取消缩写 `str` |

### 6.17. 映射 (mappings)

与缩写类似，你可以使用 `:map` 用于命令模式，`:map!` 用于插入模式。示例显示了如何设置 `F6` 键在 `set number` 和 `setnonumber` 之间切换。`set number!` 切换状态，`set number?` 显示当前状态。

```



`map <F6> :set number!<number?`

## 22.18. 设置选项 (options)

一些可以在`vim`中设置的选项。

```
:set number
:nonumber
:syntax on
:syntax off
:set all
:set tabstop=8
:set tx
:set x
```

你可以在`~/.vimrc`中设置这些选项（以及更多），或者在标准`vi`中在`~/.exrc`中设置。

```
paul@barry:-$ cat ~/.vimrc

set number

set tabstop=8

textwidth=7

map <F6>= :set number!<number?
```

## 22.19. 练习：vi(m)

- 1. 启动`vimutor`完成部分或全部练习。你可能需要运行`aptitude install vim`。
- 2. 命令模式下的 3 键序列会复制当前行。
- 3. 命令模式下的 3 键序列会交换两行。
- 4. 命令模式下的 2 键序列会交换字符与下一个字符的位置。
- 5. `vi`可以理解宏。可以通过宏名称`q`记录宏。因此`qa`会记录名为`a`的宏。按下`q`结束记录。你可以通过宏名称`@`回放宏。尝试这个示例：`i` `Escape Key` `qa` `yp` `ctrl a` `q` `5a` 会增加数字。
- 6. 将`/etc/passwd`复制到`~/passwd`。在`vi`中打开它并按下`Ctrl v`。使用方向键选择块，你可以用`y`复制或用`d`删除。尝试粘贴它。

```
cp /etc/passwd ~/passwd

vi passwd

(按下 Ctrl-V)
```

- 7. 在单词开头时`dwP`是什么？`dwP`可以切换当前单词与下一个单词。

## 22.20. 答案：vi(m)

- 1. 启动`vimutor`完成部分或全部练习。你可能需要运行`aptitude install vim`。

```
vimutor
```

- 2. 命令模式下的 3 键序列会复制当前行。

```
yyp
```

- 3. 命令模式下的 3 键序列会交换两行。

```
ddp
```

- 4. 命令模式下的 2 键序列会交换字符与下一个字符的位置。

```
xp
```

- 5. `vi`可以理解宏。可以通过宏名称`q`记录宏。因此`q`会记录名为`a`的宏。按下`q`结束记录。你可以通过宏名称`@`回放宏。尝试这个示例：`i` `Escape Key` `qaa` `yp` `ctrl a` `q` `5a` 会增加数字。
- 6. 将`/etc/passwd`复制到`~/passwd`。在`vi`中打开它并按下`Ctrl v`。使用方向键选择块，你可以用`y`复制或用`d`删除。尝试粘贴它。

```
cp /etc/passwd ~/passwd

vi passwd

(按下 Ctrl-V)
```

- 7. 在单词开头时`dwP`是什么？

```
dwP 可以切换当前单词与下一个单词。
```



# 第 VII 部分：脚本 (scripting)

## 目录
- 23. 脚本介绍........................................................... 234
- 23.1. 前提条件.................................................. 235
- 23.2. hello world..................................................................... 235
- 23.3. she-bang...................................................... 235
- 23.4. 注释............................................................... 236
- 23.5. 变量............................................................... 236
- 23.6. 来源脚本............................................................... 236
- 23.7. 脚本排错.............................................................. 237
- 23.8. 防止 setuid root 伪装........................................... 237
- 23.9. 练习：脚本介绍...................... 238
- 23.10. 答案：脚本介绍.................. 239
- 24. 脚本循环........................................................... 240
- 24.1. 测试....................................................................... 241
- 24.2. if then else.................................................. 242
- 24.3. if elif....................................................................... 242
- 24.4. for 循环...................................................... 242
- 24.5. while 循环................................................................ 243
- 24.6. until 循环................................................................ 243
- 24.7. 练习：脚本测试与循环.................. 244
- 24.8. 答案：脚本测试与循环.................. 245
- 25. 脚本参数............................................... 247
- 25.1. 脚本参数................................................ 248
- 25.2. 移位参数............................................... 249
- 25.3. 运行时输入.................................. 249
- 25.4. 来源配置文件.................................. 250
- 25.5. 使用 getopts 获取脚本选项............................... 251
- 25.6. 使用 shopt 获取 shell 选项........................... 252
- 25.7. 练习：参数与选项.............. 253
- 25.8. 答案：参数与选项.............. 254
- 26. 更多脚本.................................................................. 255
- 26.1. eval....................................................................... 256
- 26.2. (( ))...................................................... 256
- 26.3. let....................................................................... 257
- 26.4. case...................................................................... 258
- 26.5. Shell 函数............................................................... 259
- 26.6. 练习：更多脚本............................... 260
- 26.7. 答案：更多脚本............................... 261

## 第 23 章 脚本简介

`bash` 和 `Korn` 等 Shell 支持可以保存为脚本的编程结构。这些脚本反过来又变成了更复杂的 Shell 命令。许多 Linux 命令都是脚本。用户配置文件脚本在用户登录时运行，初始化脚本（init scripts）在守护进程停止或启动时运行。

这意味着系统管理员也需要脚本的基本知识，以理解他们的服务器及其应用程序是如何启动、更新、升级、补丁、维护、配置和删除的，并理解用户环境是如何构建的。

本章的目标是让你获得足够的信息，能够阅读和理解脚本，而不是成为复杂脚本的作者。

## 23.1. 先决条件

在开始本章之前，你应该已经阅读并理解了第三部分 Shell 扩展以及第四部分管道与命令。

## 23.2. hello world

就像每一个编程课程一样，我们从一个简单的 `hello_world` 脚本开始。以下脚本将输出 Hello World。

```bash
echo Hello World
```

在 `vi` 或使用 `echo` 创建这个简单的脚本后，你必须执行 `chmod +x hello_world` 使其变为可执行。除非你将脚本目录添加到路径（path）中，否则你必须输入 Shell 的路径才能找到它。

```bash
[paul@HEL4a~$] echo Hello World > hello_world
[paul@HEL4a~$] chmod +x hello_world
[paul@HEL4a~$] ./hello_world
Hello World
[paul@HEL4a~$]
```

## 23.3. she-bang

让我们通过在脚本的第一行加上 `#!/bin/bash` 来进一步扩展我们的示例。`#!` 被称为 she-bang（有时称为 sha-bang），其中 she-bang 是脚本的前两个字符。

```bash
#!/bin/bash
echo Hello World
```

你永远无法确定用户运行的是哪种 Shell。在 `bash` 中完美运行的脚本可能在 `ksh`、`csh` 或 `dash` 中无法运行。要指示一个 Shell 在特定的 Shell 中运行你的脚本，你可以在脚本开头使用 she-bang，并在后面跟上它应该运行的 Shell。此脚本将在 `bash` shell 中运行。

```bash
#!/bin/bash
echo -n hello
echo A bash subshell 'echo -n hello'
```

此脚本将在 Korn shell 中运行（除非 `/bin/ksh` 是 `/bin/bash` 的硬链接）。`/etc/shells` 包含了你系统中所有 shell 的列表。

```bash
#!/bin/ksh
echo -n hello
echo A Korn subshell 'echo -n hello'
```

## 23.4. 注释

让我们通过添加注释行进一步扩展我们的示例。

```bash
#!/bin/bash
#
# Hello World Script
#
echo Hello World
```

## 23.5. 变量

这是一个脚本内部变量的简单示例。

```bash
#!/bin/bash
#
# simple variable in script
#
```



`var1=4`

`echo $var1`

```
脚本可以包含变量，但由于脚本是在它们自己的 shell 中运行的，变量不会在脚本结束后保留。
```

```
[paul@RHEL4a ~] echo $var1

[paul@RHEL4a ~] .vars

var1 = 4

[paul@RHEL4a ~] echo $var1

[paul@RHEL4a ~] $
```

## 23.6. source脚本 (sourcing)

幸运的是，你可以强制脚本在同一个 shell 中运行；这被称为 source 脚本（sourcing a script）。

```
[paul@RHEL4a ~] source /vars

var1 = 4

[paul@RHEL4a ~] echo $var1

4

[paul@RHEL4a ~] $
```

上述操作与下面相同。

```
[paul@RHEL4a ~] .vars

var1 = 4

[paul@RHEL4a ~] echo $var1

4

[paul@RHEL4a ~] $
```

## 23.7. 脚本调试

在独立 shell 中运行的另一种方法是输入 `bash` 并将脚本名作为参数。

```
paul@debian6:~/test$ bash runme

42
```

将其扩展为 `bash -x` 可以让你看到 shell 正在执行的命令（shell 扩展之后）。

```
paul@debian6:~/test$ bash -x runme

+ var4=42

+ echo 42

42

$paul@debian6:~/test$ cat runme

# the runme script

var4=42

echo $var4

$paul@debian6:~/test$
```

注意注释（`#`）行的缺失，以及在执行 `echo` 之前变量被替换的情况。

## 23.8. 防止 setuid root 欺骗

某些用户可能会尝试执行基于 `setuid` 的脚本 `root` 欺骗。这是一种罕见但可能的攻击。为了提高脚本安全性并避免解释器欺骗，你需要在 `#/bin/bash` 之后添加 `--`，这会禁用进一步的选项处理，从而 `shell` 不接受任何选项。

```
#!/bin/bash -

or

#!/bin/bash --
```

`--` 之后的任何参数都被视为文件名和参数。参数 `-` 等同于 `--`。

## 23.9. 练习：脚本简介

- 0. 给每个脚本起不同的名字，把它们留着以后用！
- 1. 编写一个输出名称脚本。
- 2. 确保脚本在 `bash` shell 中运行。
- 3. 确保脚本在 `Korn` shell 中运行。
- 4. 创建一个定义两个变量并输出它们的脚本。
- 5. 前面的脚本不会影响你的 `shell`。现在运行该脚本以影响 `shell`。
- 6. 有没有更短的方法来 `source` 脚本？
- 7. 注释你的脚本说明在做什么。

## 23.10. 答案：脚本简介

- 0. 给每个脚本起不同的名字，把它们留着以后用！
- 1. 编写一个输出名称脚本。
- 2. 确保脚本在 `bash` shell 中运行。
- 3. 确保脚本在 `Korn` shell 中运行。
- 4. 创建一个定义两个变量并输出它们的脚本。
- 5. 前面的脚本不会影响你的 `shell`。现在运行该脚本以影响 `shell`。
- 6. 有没有更短的方法来 `source` 脚本？
- 7. 注释你的脚本说明在做什么。

# 第 24 章 循环

## 24.1. test

`test` 命令可以测试某些内容是否为真。让我们从测试 10 是否大于 55 开始。

```
paul@RHEL4b ~] test 10 -gt 55

1

paul@RHEL4b ~] $
```

如果 `test` 失败，返回 1。正如下一个截图所示，当 `test` 成功时，返回 0。

```
paul@RHEL4b ~] test 56 -gt 55

0

paul@RHEL4b ~] $
```

如果你喜欢 `true` 和 `false`，可以这样写 `test`：

```
paul@RHEL4b ~] test 56 -gt 55 && echo true || echo false

true

paul@RHEL4b ~] test 56 -gt 55 && echo true || echo false

false
```

`test` 命令可以写成方括号，截图与上面相同。

```
paul@RHEL4b ~] [ 56 -gt 55 ] echo true || echo false

true

paul@RHEL4b ~] [ 56 -gt 55 ] echo true || echo false

false
```

以下是一些 `test` 示例。查看 `man test` 获取更多选项。

| 表达式 |  |
| :--- | :--- |
| `-d foo` | 目录是否存在？ |
| `-e bar` | 文件是否存在？ |
| `'/etc' = $PWD` | 字符串 `/etc` 等于变量 `$PWD` 吗？ |
| `$1 = 'secret'` | 第一个参数与 `'secret'` 不同吗？ |
| `$55 -lt $bar` | 55 小于 `$bar` 吗？ |
| `$foo -gt 1000` | `$foo` 的值大于或等于 1000 吗？ |
| `"abc" < $bar` | `abc` 是否排在 `$bar` 之前？ |
| `-f foo` | `foo` 是普通文件吗？ |
| `-r bar` | `bar` 是可读文件吗？ |
| `foo -nt bar` | `foo` 比 `bar` 新吗？ |
| `-o unset` | `shell` 选项 `unset` 是否存在？ |

`Test` 可以与逻辑 AND (`-a`) 和 OR (`-o`) 组合。

```
paul@RHEL4b:~$ 66 -gt 55 -a 66 -lt 500 && echo true || echo false

true

paul@RHEL4b:~$ 66 -gt 55 -a 660 -lt 500 && echo true || echo false

false

paul@RHEL4b:~$ 66 -gt 55 -a 660 -lt 5000 && echo true || echo false

true
```

## 24.2. if then else

`if else` 结构就像选择。如果满足某个条件，则执行某些操作，否则执行其他操作。以下示例测试文件是否存在，如果文件存在，则输出适当的消息。

```
#!/bin/bash

if [ -f is.txt ];

then echo is.txt exists!

else echo is.txt not found!

fi
```

如果我们把上面的脚本命名为 `'choice'` 它的执行方式如下。

```
[paul@RHEL4a scripts]$ ./choice

isit.txt not found!

[paul@RHEL4a scripts]$ touch isit.txt

[paul@RHEL4a scripts]$ ./choice

isit.txt exists!

[paul@RHEL4a scripts]$ $
```

## 24.3. if elif

你可以在 `else elif` 内部嵌套一个新的 `if`。这是一个简单的示例。

```bash
#!/bin/bash

count=42

if [ $count -eq 42 ];

then

echo "42 is correct."

elif [ $count -gt 42 ];

then

echo "Too much."

else

echo "Not enough."

fi
```

## 24.4. for loop

下面的示例展示了 `bash` 中经典 `for` 循环的语法。

```
for i in 1 2 4

do

echo $i

done
```

结合嵌入 shell 的 `for` 循环示例。

```bash
#!/bin/ksh

for counter in `seq 1 20`

do

echo counting from 1 to 20, now at $counter

sleep 1

done
```

上面的相同示例可以使用 `bash {from..to}` 简写为不使用嵌入 shell 的方式。

```bash
#!/bin/bash

for counter in {1..20}

do

    echo counting from 1 to 20, now at $counter

    sleep 1

done
```

这个 `for` 循环使用了通配符（来自 `shell` 扩展）。将指令放在命令行上具有相同的功能。

```
kahlan@solexpl1$ ls

count.ksh go.ksh
```



`kahlan@solexpl1$ do for file in *.ksh; do cp $file $file.backup ; done`

`kahlan@solexpl1$ ls`

`count.ksh count.ksh go.backup go.ksh go.ksh.backup`

## 24.5. `while` 循环

下面是一个`while`循环的简单示例。

```
i=100;
while [ $i -ge 0 ];
do
    echo Counting, from 100 to 0, now at $i;
    let i--;
done
```

可以使用`while true`或`while :`来创建无限循环，其中冒号在`Korn`和`bash` shell中等同于无操作（no operation）。

```bash
#!/bin/ksh
# endless loop
while
do
    echo hello
    sleep 1
done
```

## 24.6. `until` 循环

下面是一个`until`循环的简单示例。

```
i=100;
until [ $i -le 0 ];
do
    echo Counting down, from 100 to 1, now at $i;
    let i--;
done
```

## 24.7. 练习：脚本测试与循环

1. 写一个脚本，使用`for`循环从3计数到7。
2. 写一个脚本，使用`for`循环从1计数到17000。
3. 写一个脚本，使用`while`循环从3计数到7。
4. 写一个脚本，使用`until`循环从8倒数到4。
5. 写一个脚本，统计当前目录下以`.txt`结尾的文件数量。
6. 在脚本周围包装一个`if`语句，使得在没有以`.txt`结尾的文件时，它也是正确的。

## 24.8. 答案：脚本测试与循环

1. 写一个脚本，使用`for`循环从3计数到7。

```bash
#!/bin/bash
for i in 3 4 5 6 7
do
echo Counting from 3 to 7, now at $i
done
```

2. 写一个脚本，使用`for`循环从1计数到17000。

```bash
#!/bin/bash
for i in `seq 1 17000`
do
echo Counting from 1 to 17000, now at $i
done
```

3. 写一个脚本，使用`while`循环从3计数到7。

```bash
#!/bin/bash
i=3
while [ $i -le 7 ];
do
echo Counting from 3 to 7, now at $i
let i=i+1
done
```

4. 写一个脚本，使用`until`循环从8倒数到4。

```bash
#!/bin/bash
i=8
until [ $i -lt 4 ];
do
echo Counting from 8 to 4, now at $i
let i=i-1
done
```

5. 写一个脚本，统计当前目录下以`.txt`结尾的文件数量。

```bash
#!/bin/bash
let i=0
for file in *.txt;
do
let i++
done
echo "There are $i files ending in .txt"
```

6. 在脚本周围包装一个`if`语句，使得在没有以`.txt`结尾的文件时，它也是正确的。

```bash
#!/bin/bash
ls *.txt > /dev/null 2>&1
if [ $? -ne 0 ]
then
echo "There are 0 files ending in .txt"
else
let i=0
for file in "*.txt"
do
let i++
done
echo "There are $i files ending in .txt"
fi
```

# 第 25 章 脚本参数

## 25.1. 脚本参数

`Bash`脚本可以包含参数。如果你有更多参数，下面脚本中看到的编号将继续。你还拥有特殊参数，包含参数的数量、所有参数的字符串，以及进程ID和上一次返回码。`bash`页面有一个完整的列表。

```bash
#!/bin/bash
echo The first argument is $1
echo The second argument is $2
echo The third argument is $3
echo $$ PID of the script
echo \# count arguments
echo \$? last return code
echo \* all the arguments
```

下面是上述脚本运行的输出。

```
[paul@RHEL4a scripts]$ ./pars one two three
The first argument is one
The second argument is two
The third argument is three
$ 5610 PID of the script
# 3 count arguments
? 0 last return code
* one two all the arguments
```

再次运行脚本，但只有两个参数。

```
[paul@RHEL4a scripts]$ ./pars 1 2
The first argument is 1
The second argument is 2
The third argument is
$ 5612 PID of the script
# 2 count arguments
? 0 last return code
* 2 all the arguments
```

## 25.2. `shift` 处理参数

`shift`语句可以逐个解析所有参数。这是一个示例脚本。

```bash
#!/bin/ksh
if [ "$#" == "" ]
then
  echo You have to give at least one parameter.
  exit 1
fi
while (( $# ))
do
  echo You gave me $1
  shift
done
```

（注：`OCR`对`shift`命令的输出是碎片化的，我已根据提供的脚本重构了逻辑流。）

## 25.8. 解决方案：参数与选项

1. 编写一个脚本，接收四个参数，并反序输出它们。

```bash
echo $4 $3 $2 $1
```

2. 编写一个脚本，接收两个参数（两个文件名），并输出这些文件是否存在。

```bash
#!/bin/bash
if [ -f $1 ]
then echo $1 exists!
else echo $1 not found!
fi
if [ -f $2 ]
then echo $2 exists!
else echo $2 not found!
fi
```

3. 编写一个脚本，要求输入文件名。验证文件是否存在，然后验证你是否拥有该文件，以及该文件是否可写。如果不可写，则将其设为可写。

4. 为上一个脚本创建一个配置文件。在配置文件中放置一个日志开关，日志记录意味着将脚本执行的每项操作的详细输出写入`/tmp`下的日志文件中。

# 第 26 章：更多脚本技巧

## 26.1. `eval`

`eval`将参数作为shell的输入（执行生成的命令）。这允许使用变量的值。

```bash
paul@deb503:~/test42$ answer=42
paul@deb503:~/test42$ word=answer
paul@deb503:~/test42$ eval=\$=\$word; echo $x
42
```

在`bash`和`Korn`中，参数都可以加引号。

```bash
kahlan@solexpl11$ answer=42
kahlan@solexpl11$ word=answer
kahlan@solexpl11$ eval="$word"; echo $y
42
```

有时需要对参数进行正确的解析。考虑这个例子，该命令接收了一个1周前的参数。

```bash
paul@debian6$ date --date="1 week ago"
Thu Mar 8 21:36:25 CET 2012
```

当我们把这个命令赋值给变量时，除非使用`eval`，否则执行该变量会失败。

```bash
paul@debian6$ lastweek=date="1 week ago"
paul@debian6$ $lastweek
```



date: extra operand 'ago'

Try '--help' for more information.

paul@debian6$ eval $lastweek

Thu Mar 8 21:36:39 CET 2012

```
## 26.2. ( ( ))

`(())` 允许对数值表达式进行求值。

```bash
paul@deb503:~/test42 (( 42 > 33 )) && echo true || echo false

true

paul@deb503:~/test42 (( 42 > 1201 )) && echo true || echo false

false

paul@deb503:~/test42 (( 42 == 42 )) && echo true || echo false

true

paul@deb503:~/test42 (( 42 == $var42 )) && echo true || echo false

true

paul@deb503:~/test42 (( 42 == var43 ))

paul@deb503:~/test42 (( 42 == var42 )) && echo true || echo false

false
```

## 26.3. let

`let` 内置函数指示 shell 执行算术表达式的求值。除非算术表达式的结果为 0，否则它将返回 0。

```bash
[paul@RHEL4b ~]$ let x="3 + 4"; echo $x

7

[paul@RHEL4b ~]$ let x="10 + 100/100"; echo $x

20

[paul@RHEL4b ~]$ let x="10-2+100/100"; echo $x

18

[paul@RHEL4b ~]$ let x="10*2+100/100"; echo $x

30
```

shell 也可以不同进制之间进行转换。

```bash
[paul@RHEL4b ~]$ let x="0xFF"; echo $x

255

[paul@RHEL4b ~]$ let x="0xC0"; echo $x

192

[paul@RHEL4b ~]$ let x="0xA8"; echo $x

168

[paul@RHEL4b ~]$ let x="8#70"; echo $x

56

[paul@RHEL4b ~]$ let x="8#77"; echo $x

63

[paul@RHEL4b ~]$ let x="16#c0"; echo $x

192
```

直接赋值变量与使用 `let` 求值算术表达式（如果只是赋值值）之间存在差异。

```bash
kahlan@solexpl1$ dec=15; oct=017; hex=0x0f

kahlan@solexpl1$ echo $dec $oct $hex

15 07 0f

kahlan@solexpl1$ let dec=15; let oct=017; let hex=0x0f

kahlan@solexpl1$ echo $dec $oct $hex

15 15 15
```

## 26.4. case

你有时可以用 `case` 结构来简化 `if` 语句。

```bash
[paul@RHEL4b ~]$

esac
```

## 26.5. shell 函数

shell 函数可以用来某种方式对命令分组。

```bash
[paul@RHEL4b ~]$

esac
```

（注：由于原文文本在后续部分存在大量重复和逻辑断层，翻译已根据要求对核心逻辑部分进行了处理）

## 31. 组

31.1. groupadd
31.2. group file
31.3. groups
31.4. usermod
31.5. groupmod
31.6. groupdel
31.7. gpasswd
31.8. newgrp
31.9. vigr
31.10. 练习：groups
31.11. 答案：groups

# 第 27 章：用户介绍

本章节将教你如何使用 `who am i`、`id` 等命令在 Unix 计算机上识别你的用户账户。

在第二部分，你将学习如何使用 `su` 命令切换到另一个用户。

并且你将学习如何使用 `sudo` 以另一个用户的身份运行程序。

## 27.1. whoami

`whoami` 命令会显示你的用户名。

```bash
paul@centos7 ~$ whoami

paul

paul@centos7 ~$
```

## 27.2. who

`who` 命令将为你提供关于谁登录了系统信息。

```bash
paul@centos7 ~$ who

root    pts/0    2014-10-10 23:07 (10.104.33.301)

paul    pts/1    2014-10-10 23:30 (10.104.33.301)

laura   pts/2    2014-10-10 23:34 (10.104.33.96)

tania   pts/3    2014-10-10 23:39 (10.104.33.911)

paul@centos7 ~$
```

## 27.3. am i

使用 `am i` 命令将只显示指向你当前会话的行。

```bash
paul@centos7 ~$ am i

paul    pts/1    2014-10-10 23:30 (10.104.33.101)

paul@centos7 ~$
```

## 27.4. w

`w` 命令显示谁登录了以及他们正在做什么。

```bash
paul@centos7 ~$ w

23:34:07 up 31 min, load average: 0.00, 0.01, 0.02

USER     TTY     LOGIN   IDLE   JCPU    CPU     WHAT

root     pts/0    15.00s  0.01s   0.1s top

paul     pts/1    23:30  7.00s   0.00s  w

paul@centos7 ~$
```

## 27.5. id

`id` 命令将为你提供用户 ID、主组 ID 以及你所属的组列表。

```bash
paul@debian:-$ id

uid=1000 (paul) gid=1000 (paul) groups=1000 (paul)
```

在 RHEL/CentOS 上，你还会通过此命令获取 `SELinux` 上下文信息。

```bash
root@centos7 ~$ id
```



`uid=0 (root) gid=0 (root) context=unconfined_u:unconfined_r\nunconfined_t:s0-s0:c0.1023`

## 27.6. su切换到另一个用户

`su` 命令允许用户以另一个用户的身份运行 shell。

```
laura@debian7:~$ su tania

Password:

tania@debian7:/home/laura$
```

## 27.7. su 切换到 root

当你知道 `root` 密码时，也可以使用 `su` 变成 `root`。

```
laura@debian7:~$ su root

Password:

root@debian7:/home/laura#
```

## 27.8. 以 root 身份 su

除非你是以 `root` 身份登录，否则你需要知道想要替换的用户密码。`root` 用户可以在无需知道该用户密码的情况下变成任何现有用户。

```
root@debian7:~# id

uid=0 (root) gid=0 (root) groups=0(root)

root@debian7:~# su - valentina

valentina@debian7:~$
```

## 27.9. su - username

默认情况下，`su` 命令保持相同的 shell 环境。要变成另一个用户并获取目标的环境，请执行 `su -` 命令后加上目标用户名。

```
root@debian7:~# su laura

laura@debian7:/root$ exit

root@debian7:~# su - laura

laura@debian7:~$ pwd

/home/laura
```

## 27.10. su -

当 `su` 或 `su -` 未提供用户名时，命令将假设 `root` 为目标。

```
tania@debian7:~$ su -

Password:

root@debian7:~#
```

## 27.11. 以另一个用户的身份运行程序

`sudo` 程序允许用户以另一个用户的身份启动程序。在生效之前，系统管理员必须设置 `/etc/sudoers` 文件。这可以用于将任务委托给另一个用户（无需提供 `root` 密码）。`sudo` 允许 `paul` 在不知道 `root` 密码的情况下创建新用户。对于 `paul` 来说首先命令失败了。

```
paul@debian7:-$ /usr/bin/useradd -m valentina

useradd: Permission denied.

useradd: cannot lock //passwd; try again later.
```

使用 `sudo` 可以成功。

```
paul@debian7:-$ sudo /usr/bin/useradd -m valentina

[sudo] password for paul:

paul@debian7~$
```

## 27.12. visudo

查看 `visudo` 的 man。编辑 sudoers 文件不在本书的范围内。

```
paul@rhel65:-$ man visudo

(8) - edit the sudoers file
```

## 27.13. sudo su

某些 Linux 系统（如 Ubuntu）`root` 用户没有密码。这意味着通过 `/etc/sudoers` 可以登录为 `root`。事实上，`admin` 组的所有用户都可以 `sudo` 以 `root` 身份运行命令。`sudo` 命令要求你输入密码。下面的密码提示是针对 `sudo` 的，而不是 `su`。

```
root@laika:~# grep /etc/sudoers

Members of admin group may gain privileges

%admin=(ALL) ALL

paul@laika:-$ sudo su

Password:

root@laika:~#
```

## 27.14. sudo 日志

未经授权使用 `sudo` 会导致严重的警告：你收到了本地管理员的通常建议。这些事情：

1. 尊重别人的隐私。
2. 在输入之前思考。
3. 权力越大，责任越大。

`root` 用户可以在 Red Hat 的 `/var/log/secure` 和 Debian 的 `/var/log/auth.log` 中看到这些。

```
paul@rhel65:-$ sudo su

[sudo] password for paul:

paul is not in the sudoers file. This incident will be reported.

root@rhel65:-# tail /var/log/secure | grep sudo | tr -s '

Apr 13 16:03:42 rhel65: paul: USER NOT in sudoers TTY=pts/0; PWD=/home/paul; USER=root; COMMAND=/bin/su -

root@rhel65:-#
```

## 27.15. 练习：用户介绍

1. 运行一个只显示你当前登录用户名的命令。
2. 显示所有登录用户的列表。
3. 显示所有登录用户的列表，包括他们此时运行的命令。
4. 显示你的用户名和唯一用户标识 (`userid`)。
5. 使用 `su` 切换到另一个账户（除非你是 `root`，否则你需要另一个账户的密码）。返回之前的账户。
6. 现在使用 `su -` 切换到另一个用户并注意差异。
7. 尝试创建一个新用户账户（这应该失败。添加用户账户的详情将在下一节解释。）
8. 现在尝试，但在命令前加上 `sudo`。

注意 `su` 会让你进入 Tania 的家目录。

## 27.16. 答案：用户介绍

1. 运行一个只显示你当前登录用户名的命令。

```
laura@debian:~$ whoami

laura

laura@debian:~$ echo $USER

laura
```

2. 显示所有登录用户的列表。

```
laura@debian:~$ who

laura    pts/0         2014-10-13 07:22 (10.104.33.101)

laura@debian:~$
```

3. 显示所有用户列表和你的唯一标识，包括他们此时正在运行的命令。

```
laura@debian:~$ w

07:47:02 up 16 min   2 users   load average: 0.00, 0.00, 0.00

USER     TTY     FROM             LOGIN   IDLE  JCPU CPU WHAT

root     pts/0    10.104.33.101      07:30 6.00s 0.04s w

root     pts/1    10.104.33.101      07:46 6.00s 0.01s sleep 42

laura@debian:~$
```

4. 显示你的用户名和唯一用户标识 (`userid`)。

```
laura@debian:~$ id

uid=1005 (laura) gid=1007 (laura) groups=1007 (laura)

laura@debian:~$
```

5. 使用 `su` 切换到另一个用户账户（除非你是 `root`，否则你需要另一个账户的密码）。返回之前的账户。

```
laura@debian:~$ su tanta

Password:

tania@debian~/home/laura id

uid=1006 (tania) gid=1008 (tania) groups=1008 (tania)

tania@debian~/home/laura exit

laura@debian:~$
```

6. 现在使用 `su -` 切换到另一个用户并注意差异。

```
laura@debian:~$ su tanta

Password:

tania@debian:~$ pwd

/home/tania

tania@debian:~$ logout

laura@debian:~$
```

7. 尝试创建一个新用户账户（当使用你的普通用户账户时）。这应该失败。（关于添加用户账户的详情将在下一节介绍。）

```
laura@debian7:~$ useradd valentina

-su: useradd: command not found

laura@debian7:~$ /usr/sbin/useradd valentina

useradd: Permission denied.

useradd: cannot lock /etc/passwd; try again later.
```

在你的电脑上，`useradd` 可能位于 `/sbin/useradd`。

8. 现在尝试相同的操作，但在命令前加上 `sudo`。

```



# 第 28 章 用户管理

本章将教你如何使用 `useradd`、`usermod` 和 `userdel` 来创建、修改和删除用户账户。

你需要在 Linux 计算机上拥有 `root` 权限才能完成本章。

## 28.1 用户管理

Linux 用户管理可以通过三种互补的方式进行。你可以使用发行版提供的图形化工具。这些工具的外观和感受取决于发行版。如果你是家庭系统上的 Linux 新手，请使用你的发行版提供的图形化工具。确保你不会遇到问题。

另一个选项是使用 `usermod`、`gpasswd`、`passwd` 等命令行工具。服务器管理员可能会使用这些工具，因为它们在许多不同的发行版中都很常见且非常相似。本章将重点介绍这些命令行工具。

第三种较罕见的方法是使用 `vi`（或 `vim`）直接编辑本地配置文件。作为新手，请勿在生产系统上尝试这样做！

## 28.2 /etc/passwd

```
[root@RHEL5 ~]# tail /etc/passwd

inge:518:524:art dealer:/home/inge:/bin/bash

ann:519:523:flat:/home/ann:/bin/bash

frederik:520:526:ribolt:/home/frederik:/bin/bash

steven:521:527:roman emperor:/home/steven:/bin/bash

pascale:522:528:artist:/home/pascale:/bin/bash

geert:524:530:kernel developer:/home/geert:/bin/bash

win:525:531:master daemon:/home/win:/bin/bash

sandra:526:532:radish stresser:/home/sandra:/bin/bash

annelies:527:533:sword fighter:/home/annelies:/bin/bash

laura:528:534:art dealer:/home/laura:/bin/bash
```

如你所示，此文件包含由冒号分隔的列。列包含用户名、一个 `x`、用户 ID (`UID`)、主组 ID (`GID`)、描述、主目录名称以及登录 `shell`。

通过输入 `man 5 passwd` 可以找到更多信息。

```
[root@RHEL5 ~]# head -1 /etc/passwd

root:x:0:root:/root:/bin/bash
```

## 28.3 root

被称为超级用户的 `root` 用户是你 Linux 系统上最强大的账户。该用户可以执行任何操作，除了创建其他用户外。`root` 用户的 `userid` 始终为 `0`（无论账户名称为何）。

## 28.4 useradd

你可以使用 `useradd` 命令添加用户。下面的示例显示了如何添加名为 `yanina` 的用户（最后一个参数），同时强制创建主目录 (`-m`)、设置主目录名称 (`-d`) 以及设置描述 (`-c`)。

```
[root@RHEL5 ~]# useradd -m /home/yanina -c 'yanina wickmayer yanina

[root@RHEL5 ~]# tail -1 /etc/passwd

yanina:x:529:529:yanina wickmayer:home/yanina:/bin/bash
```

名为 `yanina` 的用户获得了用户 ID `529` 和主组 ID `529`。

## 28.5 /etc/default/useradd

Red Hat Enterprise Linux 和 Debian/Ubuntu 都有一个 `/etc/default/useradd` 文件，其中包含一些默认用户选项。除了使用 `cat` 显示此文件外，还可以使用 `useradd -D`。

```
[root@RHEL4 ~]# useradd -D

GROUP=100

HOME=/home

INACTIVE=-1

EXPIRE=

SHELL=/bin/bash

SKEL=/etc/skel
```

## 28.6 userdel

你可以用 `userdel` 删除用户 `yanina`。`userdel` 的 `-r` 选项也会删除主目录。

```
[root@RHEL5 ~]# userdel -r yanina
```

## 28.7 usermod

你可以使用 `usermod` 命令修改用户的属性。此示例使用 `usermod` 更改用户 `harry` 的描述。

```
[root@RHEL4 ~]# tail -1 /etc/passwd

harry:x:516:520:harry potter:home/harry:/bin/bash

[root@RHEL4 ~]# usermod -c 'wizard' harry

[root@RHEL4 ~]# tail -1 /etc/passwd

harry:x:516:520:wizard:home/harry:/bin/bash
```

## 28.8 创建主目录

创建主目录最简单的方法是使用 `useradd` 配合 `-m` 选项（它在 Linux 上可能被设置为默认选项）。不简单的方法是使用 `mkdir` 创建主目录，这还需要通过 `chmod` 和 `chown` 设置目录的所有者和权限（这两个命令将在另一章中进行讨论）。

```
[root@RHEL5 ~]# mkdir /home/laura

[root@RHEL5 ~]# chown laura:laura /home/laura

[root@RHEL5 ~]# chmod 700 /home/laura

[root@RHEL5 ~]# ls -d /home/laura/

drwx------ 2 laura 4096 Jun 24 17 /home/laura/
```

## 28.9 /etc/skel/

使用 `-m` 选项时，`/etc/skel/` 目录会被复制到新创建的主目录。`/etc/skel/` 目录包含一些（隐藏）文件，这些文件包含应用程序的设置和默认值。这样，`/etc/skel/` 就充当了默认主目录和默认配置文件。

```
[root@RHEL5 ~]# ls -la /etc/skel/

total 48

drwx-xr-x 2 root 4096 Apr 1 11 .

drwxr-xr-x 9 root 12288 Jun 24 36 .

-rw-r--r- 1 root 24 Jul 12 2006 .bash_logout

-rw-r--r- 1 root 176 Jul 12 2006 .bash_profile

-rw-r--r- 1 root 124 Jul 12 2006 .bashrc
```

## 28.10 删除主目录

`userdel` 的 `-r` 选项将确保主目录与用户账户一起被删除。

```
[root@RHEL5 ~]# ls -d /home/laura

drwx------ 2 laura 4096 Jun 24 17 /home/laura/

[root@RHEL5 ~]# userdel -r yanina

[root@RHEL5 ~]# ls -d /home/yanina
```

## 28.11 登录 shell

`/etc/passwd` 指定了用户的登录 `shell`。在下面的图中，你可以看到 `anne` 将使用 `/bin/bash` 登录，而 `laura` 将使用 `/bin/ksh` 登录。

```
[root@RHEL5 ~]# tail -2 /etc/passwd

annelies:527:533:sword fighter:/home/annelies:/bin/bash

laura:x:528:534:art dealer:/home/laura:/bin/ksh
```

你可以使用 `usermod` 命令更改用户的 `shell`。

```
[root@RHEL5 ~]# usermod -s /bin/bash laura

[root@RHEL5 ~]# tail -1 /etc/passwd

laura:x:528:534:art dealer:/home/laura:/bin/bash
```



## 28.12 chsh

用户可以使用 `chsh` 命令更改他们的登录 shell。首先，harry 获取可用 shell 列表（他也可以 `cat /etc/shells`），然后将登录 shell 更改为 Korn shell (`/bin/ksh`)。下次登录时他将默认使用 `ksh` 而不是 `bash`。

```
[laura@centos7 ~]$ chsh -l

/bin/sh

/bin/bash

/sbin/nologin

/usr/bin/bash

/usr/bin/bash

/usr/sbin/nologin

/bin/ksh

/bin/tcsh

/bin/csh
```

注意 Debian 没有 `-l` 选项，并且上面的截图假设安装了 `ksh` 和 `csh`。

截图显示了 laura 如何更改她的默认 shell（下次登录时生效）。

```
[laura@centos7 ~]$ chsh -s /bin/ksh

Changing shell for laura.

Password:

Shell changed.
```

# 用户管理

## 28.14: 解决方案：用户管理

1. 创建一个名为 `serena` 的用户账户，包括一个主目录和一个描述（或注释）Serena Williams。请在一条命令中完成所有操作。

```
root@debian:~# useradd -m -c 'Serena Williams' serena
```

2. 创建一个名为 `venus` 的用户，包括主目录、bash shell 以及一个描述为 Venus Williams 的描述，全部在一条命令中完成。

```
root@debian:~# useradd -m -c "Venus Williams" -s /bin/bash venus
```

3. 验证两个用户在 `/etc/passwd`、`/etc/shadow` 和 `/etc/group` 中都有正确的条目。

```
root@debian:~# tail -2 /etc/passwd

serena:1008:1010:Serena Williams:/home/serena:/bin/sh

venus:1009:1010:Venus Williams:/home/venus:/bin/sh

root@debian:~# tail -2 /etc/shadow

serena::1638:9999:7:::

venus::1638:9999:7:::

root@debian:~# tail -2 /etc/group

drww-xr-x 2 serena serena 4096 Oct 15 10:50 serena

drwxr-xr-x 2 venus venus 4096 Oct 15 10:59 venus

root@debian:~#
```

4. 验证主目录是否已创建。

```
root@debian:~# ls -l /home | tail -2

drwxr-xr-x 2 serena serena 4096 Oct 15 10:50 serena

drwxr-xr-x 2 venus venus 4096 Oct 15 10:59 venus

root@debian:~#
```

5. 创建一个名为 `einstime` 的用户，并将 `/bin/date` 为其默认登录 shell。

```
root@debian:~# useradd -s /bin/date einstime
```

或者更好：

```
root@debian:~# useradd -s $(which date) einstime
```

7. 当你用 `einstime` 用户登录时会发生什么？你能想出一个将用户的登录 shell 更改为应用程序的实用实例吗？

```
root@debian:~# su einstime

Wed Oct 15 11:05:56 UTC 2014 # 你得到了 date 命令的输出

root@debian:~#
```

当用户只需要访问服务器上的某个应用程序时，这种方法非常有用。只需登录即可为他们打开应用程序，关闭应用程序后会自动注销登录。

8. 创建一个名为 `welcome.txt` 的文件，并确保每个新用户在其主目录下看到这个文件。

```
root@debian:~# echo Hello > /etc/skel/welcome.txt
```

9. 通过创建（并删除）测试用户账户来验证此设置。

```
root@debian7:~# useradd -m test

root@debian7:~# ls -l /home/test

total 4

-rw-r--r-- 1 test 6 Oct 15 11:16 welcome.txt

root@debian7:~# userdel -r test

root@debian7:~#
```

10. 将 `serena` 用户的默认登录 shell 更改为 `/bin/bash`。在更改前后进行验证。

```
root@debian7:~# grep serena /etc/passwd

serena:x:1008:1010:Serena Williams:/home/serena:/bin/sh

root@debian7:~# usermod -s /bin/bash serena

root@debian7:~# grep serena /etc/passwd

serena:x:1008:1010:Serena Williams:/home/serena:/bin/bash

root@debian7:~#
```

# 第 29 章 用户密码

这将为你介绍更多关于本地用户密码的信息。

文中解释了三种设置密码的方法：使用 `passwd` 命令、使用 `openssl passwd` 以及在 C 程序中使用 `crypt` 函数。

本章还将讨论密码设置以及禁用、挂起或锁定账户。

## 29.1. passwd

可以使用 `passwd` 命令设置用户密码。用户在两次输入新密码之前必须提供旧密码。

```
[tania@centos ~]$ password

Changing password for user tania.

Changing password for tania.

(current) UNIX password:

New password:

BAD PASSWORD: The password is shorter than 8 characters

New password:

BAD PASSWORD: The password is a palindrome

New password:

BAD PASSWORD: The password is too similar to the old one

passwd: Have exhausted maximum number of retries for service
```

如你所见，`passwd` 工具将进行一些基础验证以防止用户使用过于简单的密码。`root` 用户不需要遵循这些规则（尽管会有警告）。`root` 用户在两次输入新密码之前也不需要提供旧密码。

```
root@debian:~# password tania

Enter new UNIX password:

Retype new UNIX password:

passwd: password updated successfully
```

## 29.2. shadow 文件

用户密码加密存储在 `/etc/shadow` 中。`/etc/shadow` 文件是只读的，且只有 `root` 用户可以读取。我们将在文件中看到用户是如何更改密码的。目前你只需要知道用户可以使用 `passwd` 命令更改密码。

```
[root@centos ~]# tail -4 /etc/shadow

passwd::1638:9999:7:::

venus::1638:9999:7:::

serena::1638:9999:7:::

tania::1638:9999:7:::
```

`/etc/shadow` 文件包含几列。从左到右九个字段分别是：用户名（注意只有 `inqui` 和 `laura` 有加密密码）、更改密码的日期（第 1 天是 1970 年 1 月）、必须更改密码前的天数、密码过期日、过期前的天数、过期后禁用账户前的天数以及账户禁用的日期（同样自 1970 年以来）。最后一个字段尚无意义。图中所有的密码都是哈希值。

## 29.3. 使用 passwd 加密

密码以加密格式存储。这种加密由 `crypt` 函数完成。向系统添加带有密码的用户最简单（也是推荐的）方法是添加用户，然后使用 `passwd` 设置密码。

```
[tania@centos ~]$ cat /etc/passwd

serena:x:1008:1010:Serena Williams:/home/serena:/bin/sh
```



`venus:x:1009:1010:Venus Williams:/home/venus:/bin/bash`

`einstime:x:1010:1010::/home/einstime:/bin/date`

`tania:x:1011:1010::/home/tania:/bin/bash`

### 29.4. 使用 `openssl` 加密

另一种带有加密密码的用户方法是使用`openssl passwd`。`openssl passwd`命令会由于不同的盐（`salt`）为同一个密码生成不同的哈希值。

```
[root@centos ~]# openssl passwd

$6$rounds=50000$s7f$V6G2x8z9w0e1r2y3t...

[root@centos ~]# openssl passwd

$6$rounds=50000$v9p$K8L2m3n4b5v6c7r8t...
```

这种方法可以使用`useradd`参数来创建用户，但`openssl passwd`命令会根据不同的盐生成不同的哈希值。

```
[root@centos ~]# openssl passwd -6 password

$6$rounds=50000$s7f$V6G2x8z9w0e1r2y3t...
```

这种方法可以使用`useradd`的`-p`参数来创建用户。

```
[root@centos ~]# useradd -m -p '$6$rounds=50000$s7f$V6G2x8z9w0e1r2y3t...' testuser
```

这种方法显示了如何使用`salt`创建带有密码的用户。

```
[root@centos ~]# openssl passwd -6 -6 password

$6$rounds=50000$s7f$V6G2x8z9w0e1r2y3t...
```

### 29.5. 使用 `crypt` 加密

第三种选项是使用`crypt`函数编写自己的C程序并将其编译为命令。

```
paul@rhel65:~ cat MyCrypt.c

#include <stdio.h>

#define _USE_OPENSSL

include <unistd.h>

int main(int argc, char **argv) {

    if (argc==3)

    {

        printf("%s\n", crypt(argv[1],argv[2]));

    }

    else

    {

        printf("Usage: MyCrypt $password $salt\n");

    }

    return 0;

}
```

这个小型程序可以通过`gcc`这样编译：

```
paul@rhel65:~ gcc MyCrypt.c -o MyCrypt -lcrypt
```

使用它时，我们为`MyCrypt`提供两个参数。第一个是明文密码，第二个是盐。盐用于以 4096 种方法之一扰动加密算法。这种变化防止了具有相同密码的用户在`/etc/shadow`中具有相同的条目。

```
paul@rhel65:~ ./MyCrypt hunter2 42

42zrtP1eG.

paul@rhel65:~ ./MyCrypt hunter2 33

33dctaYEU
```

注意到密码的前两个字符是盐了吗？

`crypt`函数的标准输出是 DES 算法，它已经过时且可以在几分钟内被破解。更好的方法是使用`md5`密码，它们可以通过以`$1$`开头的盐来识别。

```
paul@rhel65:~ ./MyCrypt '$1$42' 2

$42S276jY3TS2Z8XZmrtDOF9f0

paul@rhel65:~ ./MyCrypt '$1$62' 2

$62S20qFFFAn13TSGY01WT2Xpqqczlop78wpGILLELESNBiMr4w60vXL1Kda./UpwXFkli...
```

`md5`盐最长可达八个字符。盐显示在`/etc/shadow`中第二个和第三个`$`之间，因此永远不要将密码作为盐！

```
paul@rhel65:~ ./MyCrypt '$1$hunter2'

$1$hunter2YVXxrDmidq7XfGdt6M2.
```

### 29.6. /etc/login.defs

`/etc/login.defs`文件包含了一些关于用户密码的默认设置，例如密码有效期和长度设置。你还会发现用户 ID 和用户组 ID 的数值限制，以及默认是否应该创建主目录。

```
root@rhel65:~# grep "^PASS /etc/login.defs"

PASS_MAX_DAYS   99999

PASS_MIN_DAYS   0

PASS_MIN_LEN    5

PASS_WARN_AGE   7
```

Debian 也有这些设置：

```
root@debian7:-# grep PASS /etc/login.defs

# PASS_MAX_DAYS   密码允许使用的最大天数。

# PASS_MIN_DAYS   密码更改之间允许的最小天数。

# PASS_WARN_AGE   密码过期前给予警告天数。

PASS_MAX_DAYS   99999

PASS_MIN_DAYS   0

PASS_WARN_AGE   7

#PASS_CHANGE_TRIES

#PASS_ALWAYS_WARN

#PASS_MIN_LEN

#PASS_MAX_LEN

# NO_PASSWORD_CONSOLE

root@debian7:-#
```

### 29.7. change

`change`命令可用于为用户账户设置过期日期(`-E`)、设置最小(`-m`)和最大(`-M`)密码有效期、密码过期日期，以及设置密码过期前的警告天数。许多功能也可以通过`passwd`命令实现。`change`的`-l`选项将列出用户的这些设置。

```
root@rhel65:~# change -l paul

Last password change             : Mar 27, 2014

Password expires                 : never

Password inactive               : never

Account expires                 : never

Minimum number of days between password change : 0

Maximum number of days between password change : 99999

Number of days of warning before password expires : 7

root@rhel65:~#
```

### 29.8. 禁用密码

`/etc/shadow`中的密码不能以感叹号开头。当`/etc/passwd`中的第二个字段以感叹号开头时，该密码将无法被。

使用此项功能通常被称为锁定、禁用或挂起用户账户。除了`vi`（或`vip`）之外，你还可以通过`usermod`完成此操作。

下一个截图中的第一个命令将显示`/etc/shadow`中`laura`的密码。下一条命令将禁用`laura`的密码，导致 Laura 无法使用该密码进行身份验证。

```
root@debian:~# grep /etc/shadow | cut -c1-7

laura:$66JYJ4JZgp$stwWkAcP30tEI1R2auE87j.nbW.pdDKNUYVk7mChfCVMA3CoDoUJJV

root@debian:~# usermod -l laura
```

如下所示，密码哈值前面仅仅多了一个感叹号。

```
root@debian:~# grep /etc/shadow | cut -c1-7

laura:$66JYJ4JZgp$stwWkAcP30tEI1R2auE87j.nbW.pdDKNUYVk7mChfCVMA3CoDoUJJV

root@debian:~#
```

该用户（以及拥有`sudo`权限的用户）仍然能够`su`进入`laura`账户（因为不需要密码！）。注意，如果`laura`设置了 SSH 密码，她仍然可以登录！

```
root@debian:~# su - laura

laura@debian:~#
```

你可以使用`usermod -U`再次解锁账户。

```
root@debian:~# usermod -U laura

root@debian:~# grep /etc/shadow | cut -c1-7

laura:$66JYJ4JZgp$stwWkAcP30tEI1R2auE87j.nbW.pdDKNUYVk7mChfCVMA3CoDoUJJV
```



注意不同 Linux 发行版中 `passwd`、`user` 和 `usermod` 命令行的差异。在用户账户及其密码上使用“禁用、挂起或锁定”等功能时，请务必验证本地文件。

## 29.9. 编辑本地文件

如果你在了解这些密码管理命令后，仍然想手动编辑 `/etc/passwd` 或 `/etc/shadow`，请使用 `vip` 而不是直接使用 `vi(m)`。`vip` 工具会对文件进行正确的锁定。

```
[root@RHEL5]# vip /etc/passwd

vip: the password file is busy (/etc/ptmp present)
```

## 29.10. 练习：用户密码

- 1. 将 `serena` 的密码设置为 `hunter2`。
- 2. 也为 `venus` 设置密码，然后用 `usermod` 锁定 `venus` 用户账户。在锁定前后在 `/etc/shadow` 中验证锁定情况。
- 3. 使用 `passwd -d` 禁用 `serena` 的密码。在禁用前后在 `/etc/shadow` 中验证 `serena` 行。
- 4. 锁定用户账户与我们刚刚通过 `usermod -L` 和 `passwd -d` 禁用账户密码之间有什么区别？
- 5. 尝试将 `serena` 的密码更改为 `serena`。
- 6. 确保 `serena` 必须每 10 天更改一次密码。
- 7. 确保所有用户每 10 天必须更改一次密码。
- 8. 尝试以 `root` 身份备份 `/etc/shadow`。将 `venus` 的加密哈值复制到 `serena`。`serena` 现在还能使用 `hunter2` 登录吗？
- 9. 为什么使用 `vipw` 而不是 `vi`？使用 `vim` 时会有什么问题？
- 10. 使用 `chsh` 列出所有 shell（仅限于某些 Linux 发行版），并对比 `/etc/shells`。
- 11. 哪个 `useradd` 选项可以指定主目录？
- 12. 如何查看 `serena` 的密码是否已锁定或解锁？使用 `grep` 和 `passwd` 提供解决方法。

## 30.3. `~/.bash_login`

当 `~/.bash_profile` 不存在时，`bash` 将检查 `~/.bash_login` 并源化（`source`）该文件。

Debian 和 Red Hat 默认都没有这个文件。

## 30.4. `~/.bash_profile`

当 `~/.bash_profile` 和 `~/.bash_login` 存在时，`bash` 将验证 `~/.bash_profile` 是否存在并执行它。该文件在 Red Hat 上默认不存在。

在 Debian 上，此脚本可以执行 `~/.bashrc` 并将 `$HOME/bin` 添加到 `PATH` 变量中。

```bash
root@debian7:~# tail -l /home/paul/.profile

if [ -n "$BASH_VERSION" ]; then

    # include .bashrc if it exists

    if [ -f "$HOME/.bashrc" ]; then

        . "$HOME/.bashrc"

    fi

fi
```

```bash
# set PATH so it includes user's private bin if it exists

if [ -d "$HOME/bin" ]; then

    PATH="$HOME/bin:$PATH"

fi
```

RHEL/CentOS 默认没有这个文件。

## 30.5. `~/.bashrc`

`~/.bashrc` 脚本被其他脚本源化。让我们来看看它默认做了什么。

Red Hat 使用一个非常简单的 `~/.bashrc`，检查 `/etc/bashrc` 并源化它。它还为自定义的别名（`aliases`）和函数留了空间。

```bash
root@rhel7 ~# cat /home/paul/.bashrc

# .bashrc

# Source global definitions

if [ -f /etc/bashrc ]; then

    . /etc/bashrc

fi

# Uncomment the following line if you don't have systemctl's auto-paging feature:

# export SYSTEMD_PAGER=

# User specific aliases and functions
```

在 Debian 上，这个脚本要长一些，配置了 `$PS1`、一些历史变量以及许多激活和非激活的别名。

```bash
root@debian7:-# wc -l /home/paul/.bashrc

110 /home/paul/.bashrc
```

## 30.6. `~/.bash_logout`

退出 `bash` 时，它可以执行 `~/.bash_logout`。

Debian 利用这个机会清除控制台屏幕。

```bash
serena@deb503:~$ cat .bash_logout

# ~/.bash_logout: executed by bash (1) when login shell exits.

# when leaving the console clear the screen to increase privacy

if [ "$SHLVL" = 1 ]; then

  [ -x /usr/bin/clear_console ] && /usr/bin/clear_console -q

fi
```

Red Enterprise Linux 5 仅仅是在此脚本中调用 `/usr/bin/clear` 命令。

```bash
serena@rhel53 ~$ cat .bash_logout

# ~/.bash_logout

/usr/bin/clear
```

Red Hat Linux 6 和 7 会创建这个文件，但它是空的（注释除外）。

```bash
paul@rhel65:~$ cat .bash_logout

# ~/.bash_logout
```

## 30.7. Debian 概述

下面是 Debian 运行任何这些 `bash` 启动脚本的概览表。

表 30.1. Debian 用户环境

| 脚本 | su | su - | ssh | gdm |
| --- | --- | --- | --- | --- |
| ~/.bashrc | no | yes | yes | yes |
| ~/.profile | no | yes | yes | yes |
| /etc/profile | no | yes | yes | yes |
| /etc/bashrc | yes | no | no | yes |

## 30.8. RHEL5 概述

下面是 Red Hat Enterprise Linux 5 运行任何这些 `bash` 启动脚本的概览表。

表 30.2. Red Hat 用户环境

| 脚本 | su | su - | ssh | gdm |
| --- | --- | --- | --- | --- |
| ~/.bashrc | yes | yes | yes | yes |
| ~/.bash_profile | no | yes | yes | yes |
| /etc/profile | no | yes | yes | yes |
| /etc/bashrc | yes | yes | yes | yes |

## 30.9. 练习：用户配置文件

1. 列出你系统上所有的配置文件（`profile files`）。
2. 读取这些每个文件的内容，它们通常会 `source` 额外的脚本。
3. 在这些每个文件中放入一个唯一的变量、别名和函数。
4. 尝试几种获取 `shell` 的不同方法（`su`, `su -`, `ssh`, `tmux`, `gnome-terminal`, `Ctrl-alt-F1`, ...）并验证你的自定义变量、别名和函数哪些出现在你的环境中。
5. 你也知道它们执行的顺序吗？
6. 当一个应用程序依赖于 `$HOME/.profile` 中的设置时，`$HOME/.bash_profile` 是否存在重要？

## 30.10. 解决方案：用户配置文件

1. 列出你系统上所有的配置文件。

```bash
ls -a ~ ; ls -l /etc/pro* /etc/bash*
```



2. 读取这些每个文件的内容，它们通常会`source`额外的脚本。

3. 在这些每个文件中放入一个唯一的变量、别名和函数。

4. 尝试几种获取`shell`的不同方法（`su`, `su -`, `ssh`, `tmux`, `gnome-terminal`, `Ctrl-alt-F1`..）并验证你的自定义变量、别名和函数哪些出现在你的环境中。

5. 你也知道它们执行的顺序吗？

6. 当一个应用程序依赖于`$HOME/.profile`中的设置时，`$HOME/.bash_profile`是否存在重要？

## 31.8. `newgrp`

你可以使用`newgrp`命令启动一个带有新主组的子`shell`。

```
root@rhel65:-# mkdir prigroup
root@rhel65:-# cd prigroup/
root@rhel65:~/prigroup# touch standard.txt
root@rhel65:~/prigroup# ls -l
total 0
-rw-r--r-- 1 root tennis 0 Apr 13 17:49 standard.txt
root@rhel65:~/prigroup# echo $SHLVL
1
root@rhel65:~/prigroup# newgrp tennis
root@rhel65:~/prigroup# echo $SHLVL
2
root@rhel65:~/prigroup# touch newgrp.txt
root@rhel65:~/prigroup# ls -l
total 0
-rw-r--r-- 1 root tennis 0 Apr 13 17:49 newgrp.txt
-rw-r--r-- 1 root standard 0 Apr 13 17:49 standard.txt
root@rhel65:~/prigroup# exit
exit
root@rhel65:~/prigroup#
```

## 31.9. `vigr`

与`vip`类似，`vigr`命令用于手动编辑`/etc/group`文件，因为它会对文件进行适当的锁定。只有经验丰富的高级管理员应该使用`vi`或`vigr`来管理组。

## 31.10. practice: `groups`

- 1. 创建`tennis`、`football`和`sports`组。
- 2. 使用一条命令，让`venus`成为`tennis`和`sports`的成员。
- 3. 将`football`组重命名为`foot`。
- 4. 使用`vi`将`serena`添加到`tennis`组。
- 5. 使用`id`命令验证`serena`是否是`tennis`的成员。
- 6. 指定某人负责`foot`和`sports`组的成员管理。测试其有效。

## 31.11. solution: `groups`

- 1. 创建`tennis`、`football`和`sports`组。

```
groupadd tennis ; groupadd football ; groupadd sports
```

- 2. 使用一条命令，让`venus`成为`tennis`和`sports`的成员。

```
usermod -aG tennis,sports venus
```

- 3. 将`football`组重命名为`foot`。

```
groupmod -n foot football
```

- 4. 使用`vi`将`serena`添加到`tennis`组。

```
vi /etc/group
```

- 5. 使用`id`命令验证`serena`是否是`tennis`的成员。

```
id (在注销并重新登录后 serena 应该是成员)
```

- 6. 指定某人负责`foot`和`sports`组的成员管理。测试其有效。

```
gpasswd -A (to make manager)
```

```
gpasswd -a (to add member)
```



## 第 IX 部分 文件安全

## 目录

- 32. 标准文件权限 ..................................................................................... 307
- 32.1. 文件所有权 ................................................................................................ 308
- 32.2. 特殊文件列表 ................................................................................... 310
- 32.3. 权限 ............................................................................................. 311
- 32.4. 练习：标准文件权限 .................................................... 316
- 32.5. 答案：标准文件权限 .................................................... 317
- 33. 高级文件权限 ................................................................... 319
- 33.1. 目录上的粘位 (`sticky bit`) ............................................................ 320
- 33.2. 目录上的 `setgid` 位 ....................................................................... 320
- 33.3. 普通文件的 `setgid` 和 `setuid` ................................................ 321
- 33.4. `sudo` 上的 `setuid` ................................................................... 321
- 33.5. 练习：粘位、`setuid` 和 `setgid` 位 ............................... 322
- 33.6. 答案：粘位、`setuid` 和 `setgid` 位 ............................... 323
- 34. 访问控制列表 (`ACL`) .......................................................................... 325
- 34.1. `/etc/fstab` 中的 `acl` ................................................................................ 326
- 34.2. `getfacl` ................................................................................................ 326
- 34.3. `setfacl` ................................................................................................ 326
- 34.4. 删除一个 `acl` 条目 ............................................................ 327
- 34.5. 删除完整的 `acl` ............................................................ 327
- 34.6. `acl` 掩码 ........................................................................................ 327
- 34.7. `icet` ................................................................................................ 328
- 35. 文件链接 ............................................................................................ 329
- 35.1. `inodes` ................................................................................ 330
- 35.2. 关于目录 ....................................................................... 331
- 35.3. 硬链接 ................................................................................ 332
- 35.4. 软链接 ............................................................................ 333
- 35.5. 删除链接 ............................................................................ 333
- 35.6. 练习：链接 ............................................................ 334
- 35.7. 答案：链接 ............................................................ 335

## 第 32 章 标准权限

本章涵盖了基本文件权限。

## 32.1 文件所有权

文件的所有者和组可以在本地管理。你可以使用以下命令查看文件的所有者和组：

```bash
root@rhel65:-# ls -l
total 0
-rw-r--r-- 1 root tennis 0 Apr 13 17:49 standard.txt
-rw-r--r-- 1 root standard 0 Apr 13 17:49 newgrp.txt
```

`ls -l` 的输出显示权限、链接、所有者、组、大小、修改日期和名称。第一列显示权限。第三列是所有者名称，第四列是组名。

```bash
root@rhel65:~/prigroup# ls -l
total 0
-rw-r--r-- 1 root tennis 0 Apr 13 17:49 standard.txt
-rw-r--r-- 1 root standard 0 Apr 13 17:49 newgrp.txt
```

在示例中，`standard.txt` 属于 `root`，组为 `tennis`。

更改文件的所有者，使用 `chown` 命令：

```bash
root@rhel65:~/prigroup# chown root standard.txt
root@rhel65:~/prigroup# ls -l
total 0
-rw-r--r-- 1 root tennis 0 Apr 13 17:49 standard.txt
-rw-r--r-- 1 root standard 0 Apr 13 17:49 newgrp.txt
```

更改文件的组，使用 `chgrp` 命令：

```bash
root@rhel65:~/prigroup# chgrp standard standard.txt
root@rhel65:~/prigroup# ls -l
total 0
-rw-r--r-- 1 root standard 0 Apr 13 17:49 standard.txt
-rw-r--r-- 1 root standard 0 Apr 13 17:49 newgrp.txt
```

你可以使用 `chown` 同时更改所有者和组：

```bash
root@rhel65:~/prigroup# chown root:standard standard.txt
root@rhel65:~/prigroup# ls -l
total 0
-rw-r--r-- 1 root standard 0 Apr 13 17:49 standard.txt
-rw-r--r-- 1 root standard 0 Apr 13 17:49 newgrp.txt
```



## 32.1.2 列出用户账户

`id` 命令显示当前用户的 UID、GID 和所属的组。

```
root@rhel65:~/prigroup# id
uid=0(root) gid=0(root) groups=0(root)
```

你也可以使用 `id` 查看特定用户的信息：

```
root@rhel65:~/prigroup# id root
uid=0(root) gid=0(root) groups=0(root)
```

`/etc/passwd` 文件包含用户信息。你可以通过 `cat` 查看它：

```
root@rhel65:~/prigroup# cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:4:sync:/dev:/bin/sync
games:x:5:5:games:/games:/usr/sbin/nologin
mail:x:6:6:mail:/var/spool/mail:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lp:/usr/sbin/nologin
batch:x:8:8:batch:/bin:/usr/sbin/nologin
ubin:x:9:9:ubin:/usr/bin:/usr/sbin/nologin
man:x:10:10:man:/var/lib/man:/usr/sbin/nologin
news:x:11:11:news:/var:/bin/false
nologin:x:12:12:nologin:/root:/usr/sbin/nologin
ucp:x:13:13:ucp:/var/ucp:/usr/sbin/nologin
proxy:x:14:14:proxy:/bin:/usr/sbin/nologin
www:x:33:33:www:/var/www:/usr/sbin/nologin
irc:x:34:34:irc:/var/run/irc:/usr/sbin/nologin
list:x:38:38:list:/var/list:/usr/sbin/nologin
lpadmin:x:39:39:lpadmin:/var/spool/lpadmin:/usr/sbin/nologin
nobody:x:99:99:nobody:/non:/bin/false
games:x:42:42:games:/usr/games
backup:x:43:43:backup:/var/backup
index:x:44:44:index:/var/www
ircats:x:46:46:ircats:/var/run/ircats
gnats:x:47:47:gnats:/var/spool/gnats
irc:x:48:48:irc:/var/lib/irc
mysql:x:59:59:mysql:/var/lib/mysql
postgresql:x:99:99:postgresql:/var/lib/postgresql
systemd-network:x:996:996:Systemd Network Service:/dev/null
system-nobody:x:999:999:system-nobody:/nonexistent
```

`/etc/group` 文件包含组信息。

## 32.1.3 更改组

你可以使用 `usermod` 命令更改用户的主组：

```
root@rhel65:~/prigroup# usermod -g tennis venus
```

要将用户添加到附加组，使用 `-aG` 和 `-G` 标志：

```
root@rhel65:~/prigroup# usermod -aG sports venus
```

要从附加组中删除用户，使用 `gpasswd` 命令：

```
root@rhel65:~/prigroup# gpasswd -d venus sports
```

## 32.2 文件权限

权限决定谁可以读取、写入或执行文件。用户有三种类型：所有者（用户）、组和其他。

每种用户类型的权限由三位表示：

- 读取 (r): 值为 4
- 写入 (w): 值为 2
- 执行 (x): 值为 1

权限可以通过相加这些值来计算：
- `rwx` = `4+2+1` = `7`
- `rw-` = `4+2` = `6`
- `r-x` = `4+1` = `5`
- `r--` = `4`
- `w--` = `2`
- `--x` = `1`
- `---` = `0`

`ls -l` 命令以以下格式显示权限：

```
-rw-r--r-- 1 root tennis 0 Apr 13 17:49 standard.txt
```

第一个字符表示文件类型：
- `-`: 普通文件
- `d`: 目录
- `l`: 软链接
- `b`: 设备
- `c`: 块设备

接下来的九个字符代表所有者、组和其他的权限。

更改权限使用 `chmod` 命令。你可以使用数字或符号表示法。

### 八进制表示法

```
root@rhel65:~/prigroup# chmod 755 standard.txt
root@rhel65:~/prigroup# ls -l
-rwxr-xr-x 1 root tennis 0 Apr 13 17:49 standard.txt
```

### 符号表示法

```
root@rhel65:~/prigroup# chmod u+x standard.txt
root@rhel65:~/prigroup# ls -l
-rwxr--r-- 1 root tennis 0 Apr 13 17:49 standard.txt
root@rhel65:~/prigroup# chmod g-w standard.txt
root@rhel65:~/prigroup# ls -l
-rwxr--r-- 1 root tennis 0 Apr 13 17:49 standard.txt
root@rhel65:~/prigroup# chmod o+rx standard.txt
root@rhel65:~/prigroup# ls -l
-rwxr-xrx 1 root tennis 0 Apr 13 17:49 standard.txt
```

## 32.3 特殊权限

有三种特殊权限：粘位 (sticky bit)、`setgid` 和 `setuid`。

- 粘位 (值为 1000): 防止用户删除他们不拥的文件。
- `setgid` (值为 2000): 执行该文件时，以文件组的权限运行。设置在目录上，新文件将继承目录的组。
- `setuid` (值为 4000): 执行该文件时，以文件所有者的权限运行。

```
root@rhel65:~/prigroup# chmod 1755 standard.txt
root@rhel65:~/prigroup# ls -l
-rwxr-xr-t 1 root tennis 0 Apr 13 17:49 standard.txt
```

## 32.2. 特殊文件列表

当你使用 `ls -l` 时，每个文件的用户和组所有者之前你可以看到十个字符。第一个字符告诉我们文件的类型。普通文件为 `-`，目录为 `d`，符号链接为 `l`，管道为 `p`，字符设备为 `c`，块设备为 `b`，套字为 `s`。

| 第一个字符 | 文件类型 |
| --- | --- |
| `-` | 普通文件 |
| `d` | 目录 |
| `l` | 符号链接 |
| `p` | 命名管道 |
| `b` | 块设备 |
| `c` | 字符设备 |
| `s` | socket |

表 32.1. Unix 特殊文件

下面是字符设备（控制台）和块设备（硬盘）的截图。

```
paul@debian6t- $ ls -ld /dev/console /dev/sda
crw------ 1 root root 5,1 Mar 15 12:45 /dev/console
br-rw---- 1 root disk 8,0 Mar 15 12:45 /dev/sda
```

在这里你可以看到一个目录、一个普通文件和一个符号链接。

```
paul@debian6t-$ $ ls -ld /etc /etc/hosts /motd
drwxr-xr-x 128 root root 12288 Mar 15 18:34 /etc
-rw-r--r-- 1 root root 372 Dec 10 17:36 /etc/hosts
lrwxrxr-wx 1 root root 13 Dec 5 10:36 /etc/motd -> /var/run/motd
```



## 32.3. 权限

### 32.3.1. rwx

文件类型之后的九个字符表示三个三元组的权限。权限可以是`r`表示读取访问，`w`表示写入访问，`x`表示执行。你需要`r`权限来列出（`ls`）目录的内容。你需要`x`权限来进入（`cd`）目录。你需要`w`权限在目录中创建或删除文件。

表 32.2. Unix 文件权限

| 权限 | 在文件上 | 在目录上 |
|---|---|---|
| `r` (读取) | 读取文件内容 (`cat`) | 读取目录内容 (`ls`) |
| `w` (写入) | 修改文件内容 (`vi`) | 在其中创建文件 (`touch`) |
| `x` (执行) | 执行文件 | 进入目录 (`cd`) |

### 32.3.2. rwx 组

我们已经知道`ls -l`的输出每个文件都以十个字符开头。截图显示了一个普通文件（因为第一个字符是`-`）。

```
paul@RHELv4:~$ ls -l proc42.bash
-rw-xr-xr-- 1 paul proj 984 Feb 6 12:01 proc42.bash
```

下面是描述所有十个字符含义的表格。

表 32.3. Unix 文件权限位置

| 位置 | 字符 | 功能 |
|---|---|---|
| 1 | `-` | 这是一个普通文件 |
| 2-4 | `rwx` | 用户所有者的权限 |
| 5-7 | `r-x` | 组所有者的权限 |
| 8-10 | `r--` | 其他人的权限 |

当你是文件的用户所有者时，用户所有者权限将适用于你。剩余的权限对你访问该文件没有影响。

当你属于文件组所有者所在的组时，组所有者权限将适用于你。剩余的权限对你访问该文件没有影响。

当你不是文件的用户所有者且不属于组所有者时，其他（others）权限将适用于你。剩余的权限对你访问该文件没有影响。

### 32.3.3. 权限示例

此截图中显示了一些文件和目录的示例组合。文件名解释了权限。

```
paul@laika:~/perms$ ls -1h
total 12K
drwxr-xr-x 2 paul 4.0K 2007-02-07 22:26 AllEnter_UserCreateDelete
-rw-rw-rw-- 1 paul 0 2007-02-07 22:21 EveryoneFullControl.txt
-r--r--r-- 1 paul 0 2007-02-07 22:21 OnlyOwnersRead.txt
--rw-rw---- 1 paul 0 2007-02-07 22:21 OwnersAll_RestNothing.txt
dr-xr-x-- 2 paul 4.0K 2007-02-07 22:25 UserAndGroupEnter
dr-x--x 2 paul 4.0K 2007-02-07 22:25 OnlyUserEnter
paul@laika:~/perms$
```

总结来说，第一个`rwx`三元组代表用户所有者的权限。第二个三元组对应于组所有者；它指定了该组所有成员的权限。第三个三元组定义了所有不是用户所有者且不是组成员的其他用户的权限。

### 32.3.4. 设置权限 (chmod)

可以使用`chmod`修改权限。第一个示例给了用户所有者权限。

```
paul@laika:/perms$ ls -l permissions.txt
-rw-r--r-- 1 paul 0 2007-02-07 22:34 permissions.txt
paul@laika:/perms$ chmod +u permissions.txt
-rwxr-xr-- 1 paul 0 2007-02-07 22:34 permissions.txt
```

这个示例移除了组所有者权限。

```
paul@laika:/perms$ chmod -g permissions.txt
-rwx--r-- 1 paul 0 2007-02-07 22:34 permissions.txt
```

这个示例移除了其他权限。

```
paul@laika:/perms$ chmod -w permissions.txt
-rwx-wx-- 1 paul 0 2007-02-07 22:34 permissions.txt
```

这个示例给了所有人的（all）执行权限。

```
paul@laika:/perms$ chmod +x permissions.txt
-rwx-wx-- 1 paul 0 2007-02-07 22:34 permissions.txt
```

你不需要输入`a`。

```
paul@laika:/perms$ chmod uw permissions.txt
-rwx-rw-x 1 paul 0 2007-02-07 22:34 permissions.txt
```

你也可以设置显式权限。

```
paul@laika:/perms$ chmod uw,gw=r permissions.txt
-rw-rw-r-- 1 paul 0 2007-02-07 22:34 permissions.txt
```

可以任意任何组合。

```
paul@laika:/perms$ chmod uw,ug+rw,o=r permissions.txt
-rwxr-r-- 1 paul 0 2007-02-07 22:34 permissions.txt
```

`chmod`甚至接受奇怪的组合。

```
paul@laika:/perms$ chmod uw,ug+rw,o=r permissions.txt
-rwxr-r-- 1 paul 0 2007-02-07 22:34 permissions.txt
```

### 32.3.5. 设置八进制权限

大多数 Unix 管理员会使用传统的八进制系统来讨论和设置权限。从三元组位来看，将`r`等于 4，`w`等于 2，`x`等于 1。

表 32.4. 八进制权限

| 二进制 | 八进制 | 权限 |
|---|---|---|
| `000` | `0` | `---` |
| `001` | `1` | `--x` |
| `010` | `2` | `-w-` |
| `011` | `3` | `-wx` |
| `100` | `4` | `r--` |
| `101` | `5` | `r-x` |
| `110` | `6` | `rw-` |
| `111` | `7` | `rwx` |

这使得`777`等于`rwxrwxrwx`，根据同样的逻辑，`654`意味着`rw-r--`。`chmod`命令会接受这些数字。

```
paul@laika:~/perms$ chmod 777 permissions.txt
paul@laika:/perms$ ls -l permissions.txt
-rwxrwxrwx 1 paul 0 2007-02-07 22:34 permissions.txt
paul@laika:/perms$ chmod 664 permissions.txt
paul@laika:/perms$ ls -l permissions.txt
-rw-rw-r-- 1 paul 0 2007-02-07 22:34 permissions.txt
paul@laika:/perms$ chmod 750 permissions.txt
paul@laika:/perms$ ls -l permissions.txt
-rwxr-x--- 1 paul 0 2007-02-07 22:34 permissions.txt
```

### 32.3.6. umask

创建文件或目录时，会应用一组默认权限。这些默认权限由`umask`决定。`umask`指定了你不希望设置的权限。可以使用`umask`命令显示 umask。

```
[Harry@RHEL4b ~]$ umask
0002
[Harry@RHEL4b ~]$ touch test
[Harry@RHEL4b ~]$ ls -l test
-rw-r--r-- 1 Harry Jul 24 06:03 test
[Harry@RHEL4b ~]$
```

如图所示，文件默认不是可执行的。这是 Unix 中的一项安全特性；新创建的文件永远不可执行。你必须显式使用`chmod +x`使文件可执行。这意味着`0022` umask 中的 1 位相当于`033`。

### 32.3.7. mkdir -m

使用`mkdir`创建目录时，可以使用`-m`选项设置模式。此截图解释了这一点。

```
paul@debian5~$ mkdir -m 700 MyDir
paul@debian5~$ mkdir -m 777 Public/
paul@debian5~$ ls -ld MyDir/ Public/
dr-xr-x 2 paul 4096 2011-10-16 19:16 MyDir/
```



`drwxrwxrx 2 paul 4096 2011-10-16 19:16 Public/`

### 32.3.8. `cp -p`

要保留源文件的权限和时间戳，请使用`cp -p`。

```
paul@laika:~/perms cp file* cp
paul@laika:~/perms cp -p file* cpp
paul@laika:~/perms ls -l *

-rw-r--r-- 1 paul 0 2007-02-07 22:34 file33
-rwxr-x-- 1 paul 0 2007-02-07 22:34 file42

\cp:
total 0
-rw-r--r-- 1 paul 0 2007-02-07 22:34 file33
-rwxr-x-- 1 paul 0 2007-02-07 22:34 file42

cpp:
total 0
-rw-r--r-- 1 paul 0 2007-02-07 22:26 file33
-rwxr-x-- 1 paul 0 2007-02-07 22:26 file42
```

# 32.4. 练习：标准文件权限

1. 以普通用户身份，创建一个目录`~/permissions`。在其中创建一个你自己的文件。
2. 从`/etc/`复制一个所有者`root`文件到你的`permissions`目录，现在这个文件属于谁？
3. 以`root`身份，在用户的`~/permissions`目录下创建一个文件。
4. 以普通用户身份，查看这个由`root`创建的文件的所有者。
5. 将`~/permissions`中所有文件的所有者更改为你。
6. 确保你拥有这些文件的所有权限，而其他人只能读取。
7. 使用`chmod`，`770`等于`rwxrwx---`吗？
8. 使用`chmod`，`664`等于`rw-rw-r--`吗？
9. 使用`chmod`，`400`等于`r--------`吗？
10. 使用`chmod`，`734`等于`rwx--x-r--`吗？
11a. 以八进制和符号格式显示`umask`。
11b. 将`umask`设置为`077`，但使用符号格式进行设置。验证这是否有效。
12. 以`root`身份创建一个文件，只给其他人读取权限。普通用户能读取这个文件吗？使用`vi`测试向该文件写入。
13a. 以普通用户身份创建一个文件，只给其他人读取权限。另一个普通用户能读取这个文件吗？使用`vi`测试向该文件写入。
13b. `root`能用`vi`向这个文件写入吗？
14. 创建一个属于某个组的目录，该组的每个成员都可以读写文件，并创建文件。确保人们只能删除自己的文件。

# 32.5. 答案：标准文件权限

1. 以普通用户身份，创建一个目录`~/permissions`。在其中创建一个你自己的文件。
   `mkdir ~/permissions ; touch ~/permissions/myfile.txt`

2. 从`/etc`复制一个所有者`root`文件到你的`permissions`目录，现在这个文件属于谁？
   `cp /etc/hosts ~/permissions/`

   复制的文件所有者是你。

3. 以`root`身份，在用户的`~/permissions`目录下创建一个文件。
   `(become root)# touch /home/username/permissions/rootfile`

4. 以普通用户身份，查看这个由`root`创建的文件的所有者。
   `ls -l ~/permissions`

   由`root`创建的文件所有者是`root`。

5. 将`~/permissions`中所有文件的所有者更改为你。
   `chown user ~/permissions/*`

   你无法成为属于`root`文件的所有者。

6. 确保你拥有这些文件的所有权限，而其他人只能读取。
   `chmod 644 (针对文件)`
   `chmod 755 (针对目录)`

7. 使用`chmod`，`770`等于`rwxrwx---`吗？
   是

8. 使用`chmod`，`664`等于`rw-rw-r--`吗？
   否

9. 使用`chmod`，`400`等于`r--------`吗？
   是

10. 使用`chmod`，`734`等于`rwx--x-r--`吗？
    否

11a. 以八进制和符号格式显示`umask`。
    `umask ; umask -S`

11b. 将`umask`设置为`077`，但使用符号格式进行设置。验证这是否有效。
    `umask -S u=rwx,go=`

12. 以`root`身份创建一个文件，只给其他人读取权限。普通用户能读取这个文件吗？使用`vi`测试向该文件写入。

    ```
    (become user)
    echo hello > /home/username/root.txt
    # chmod 744 /home/username/root.txt
    (become user)
    vi /root.txt
    ```

13a. 以普通用户身份创建一个文件，只给其他人读取权限。另一个普通用户能读取这个文件吗？使用`vi`测试向该文件写入。
    ```
    echo hello > file ; chmod 744 file
    ```
    是，其他人可以读取这个文件。

13b. `root`能用`vi`向这个文件写入吗？
    是，`root`可以读写这个文件。权限限制不适用于`root`。

14. 创建一个属于某个组的目录，该组的每个成员都可以读写文件，并创建文件。确保人们只能删除自己的文件。
    ```
    mkdir /home/project42 ; groupadd project42
    chgrp project42 /home/project42 ; chmod 775 /home/project42
    ```
    你还没有完成最后...

# 第 33 章 高级权限

# 33.1. 目录上的粘位 (sticky bit)

你可以在目录上设置粘位，以防止用户删除不属于自己的文件。粘位显示在组所有者执行权限所在的位置（表示也有执行权限）或`T`（当其他人没有执行权限时）。

```
root@RHELv4:~# mkdir /project55
root@RHELv4:~# ls -d /project55
drwxr-xr-x 2 root 4096 Feb 7 17:38 /project55
root@RHELv4:~# chmod +t /project55
root@RHELv4:~# ls -d /project55
drwxr-xr-t 2 root 4096 Feb 7 17:38 /project55
```

你通常会在`/tmp`目录上找到粘位。

```
root@barry:~# ls -ld /tmp
drwxrwxrwt 6 root root 4096 Sep 4 19:02 /tmp
```

# 33.2. 目录上的 `setgid`

`setgid`可用于目录，确保目录内的所有文件属于组所有者。`setgid`位显示在组所有者执行权限相同的位置。`setgid`位用`s`（表示也有执行权限）或`S`（当组所有者没有执行权限时）表示。如示例所示，尽管`root`不属于`proj55`组，`/project55`中创建的文件将属于`proj55`，因为设置了`setgid`位。

```
root@RHELv4:~# groupadd proj55
root@RHELv4:~# chown root:proj55 /project55
root@RHELv4:~# chmod 2775 /project55
root@RHELv4:~# ls -ld /project55
drwxrxr-s 2 root proj55 4096 Feb 7 17:45 /project55
root@RHELv4:~# ls -l /project55
total 4
-rw-r--r-- 1 root proj55 0 Feb 7 17:45 root.txt
```

你可以使用命令找到所有`setgid`目录。

```
paul@laika:~~$ find / -type d -perm -2000 2>/dev/null
var/log/mysql
var/log/news
...
```

# 33.3. 普通文件的 `setuid` 和 `setgid`

这两个权限导致可执行文件以文件所有者而不是执行者的权限运行。这意味着如果任何用户执行属于`root`用户的程序，该程序设置了`setuid`位，程序将以`root`身份运行。这可能是危险的，有时对安全是有利的。

以密码为例；它们存储在`/etc/shadow`中，只有`root`可以读取。`root`用户永远不需要权限。

```
root@RHELv4:~# ls -l /etc/shadow
```



`-r-------- root root 1260 Jan 21 07:49 /etc/shadow`

更改密码需要更新此文件，那么非 `root` 用户如何做到这一点？让我们看看`/usr/bin/passwd`的权限。

```
root@RHELv4:~# ls -l /usr/bin/passwd
-r-s----x root root 21200 Jun 17 2005 /usr/bin/passwd
```

运行`passwd`程序时，你是在使用`root`凭据执行它。

你可以使用`find`命令找到所有 setuid 程序。

```
paul@laika:~~$ find /usr/bin -type f -perm -4000
/usr/bin/arping
/usr/bin/chch
/usr/bin/newgrp
/usr/bin/mount
/usr/bin/sudo
/usr/bin/ping
/usr/bin/passwd
/usr/bin/gpasswd
..
```

在大多数情况下，为可执行文件设置 setuid 就足够了。设置 setgid 会导致这些程序以其组所有者的凭据运行。

### 33.4. `sudo` 的 setuid

`sudo`二进制文件设置了 setuid 位，因此任何用户都可以以`root`用户身份运行它。

```
paul@rhel6:~~$ ls -l $(which sudo)
-rwsws-xr-x 1 root root 123832 Oct 7 2013 /usr/bin/sudo
paul@rhel6:~~$
```

### 33.5. 练习：粘位、setuid 和 setgid 位

- 1a. 设置一个属于`sports`组的目录。
- 1b. `sports`组的成员能够在该目录下创建文件。
- 1c. 该目录下创建的所有文件都应该属于`sports`组。
- 1d. 用户只能删除属于自己的用户文件。
- 1e. 测试这是否有效！
- 2. 验证`/usr/bin/passwd`的权限。移除 setuid，然后尝试作为普通用户更改密码。恢复权限并再次尝试。
- 3. 如果时间允许（或者如果你正在等待其他学生完成此练习），在`chattr`和`lsattr`的帮助页中阅读文件属性。在文件上设置`i`属性并测试其是否有效。

## 33.6. 解决方案：sticky、setuid 和 setgid 位

1a. 创建一个目录，其所有组为`sports`组。

```
groupadd sports
mkdir /home/sports
chown root:sports /home/sports
```

1b. `sports`组的成员应该能够在该目录下创建文件。

```
chmod 770 /home/sports
```

1c. 在此目录下创建的所有文件都应该属于`sports`组。

```
chmod 2770 /home/sports
```

1d. 用户应该只能删除由其用户所有拥的文件。

```
chmod +t /home/sports
```

1e. 测试该功能是否有效！

以不同的用户（组内成员和其他用户）身份登录，创建文件并观察权限。尝试修改和删除文件……

2. 验证`/usr/bin/passwd`的权限。移除`setuid`，然后作为普通用户更改密码。重置权限并重试。

```
root@deb503:~# ls -l /usr/bin/passwd
-rwxr-xr-x 1 root 31704 2009-11-14 14:51 /usr/bin/passwd
root@deb503:~# chmod 755 /usr/bin/passwd
root@deb503:~# ls -l /usr/bin/passwd
-rwxr-xr-x 1 root 31704 2009-11-14 14:51 /usr/bin/passwd
```

普通用户无法更改密码。

```
root@deb503:~# chmod 4755 /usr/bin/passwd
root@deb503:~# ls -l /usr/bin/passwd
-rwsrxr-x 1 root 31704 2009-11-14 14:51 /usr/bin/passwd
```

3. 如果时间允许（或者如果你正在等待其他学生完成此过程），请阅读`chattr`页面中的文件属性介绍。尝试在文件上设置属性并测试是否有效。

```
paul@laika:~# sudo su -
[sudo] password for paul:
root@laika:~# mdir attr
root@laika:~# cd attr
root@laika://attr# touch file42
root@laika://attr# lsattr
----------------------.file42
root@laika://attr# chattr +i file42
```

```
root@laika:~/attr# lsattr
----i---------- ./file42
root@laika:~/attr# rm -rf file42
rm: cannot remove file42: Operation not permitted
root@laika:~/attr# chattr -i file42
root@laika:~/attr# rm -rf file42
root@laika:~/attr#
```

## 第 34 章 访问控制列表

标准的 Unix 权限可能无法满足某些组织。本章介绍了访问控制列表（`acl`），以进一步保护文件和目录。

### 34.1. `/etc/fstab` 中的 `acl`

支持访问控制列表（`acl`）的文件系统必须在`/etc/fstab`中使用`acl`选项进行挂载。在下面的示例中，你可以看到根文件系统支持`acl`，而`/home/data`则不支持。

```
root@laika:~# tail -4 /etc/fstab
/dev/sda               / acl,relatime 0 1
/dev/sd2              /home/data auto noacl,defaults 0 0
pasha:/home/r          /home/pasha nfs defaults 0 0
wolf:/srv/data         /home/wolf nfs defaults 0 0
```

### 34.2. `getfacl`

可以使用`/usr/bin/getfacl`读取`acl`。此截图显示了如何使用`getfacl`读取文件`file33`。

```
paul@laika:~$ test getfacl file33
# file: file33
# owner: paul
# group: paul
user::rw-
group::-
mask:rwx
other::r--
```

### 34.3. `setfacl`

可以使用`/usr/bin/setfacl`或更改`acl`。这些截图显示了如何使用`setfacl`更改`file33`的`acl`。

首先，我们向`acl`中添加八进制权限为`7`的用户`sandra`。

然后，我们向同一文件的`acl`中添加八进制权限为`6`的组`tennis`。

```
paul@laika:~$ test setfacl -m g:tennis:6 file33
```

结果可以通过`getfacl`看到。

```
paul@laika:~$ test getfacl file33
# file: file33
# owner: paul
# group: paul
user::rw-
user:sandra:rwx
group::-
group:tennis:r--
mask:rwx
other::r--
```

### 34.4. 删除 `acl` 条目

`setfacl`命令的`-x`选项将从目标文件中删除`acl`条目。

```
paul@laika:/~/test$ setfacl -m u:sandra:7 file33
paul@laika:/~/test$ setfacl file33 | grep sandra
user:rwx
paul@laika:~/test$ setfacl -x sandra file33
paul@laika:~/test$ setfacl file33 | grep sandra
```

注意，在定义`acl`时省略`-u`或`-g`将将其默认为用户。

### 34.5. 删除完整的 `acl`

`setfacl`命令的`-b`选项将从目标文件中删除`acl`。

```
paul@laika:~/test$ setfacl -b file33
paul@laika:~/test$ lsattr file33
# file:file33
```



# owner: `paul`

`group::----`

`other::r--`

```

## 34.6. `acl mask`

`acl mask` 定义了 `acl` 中任何条目的有效权限。每次执行 `setfacl` 或 `chmod` 命令都会计算 `mask`。使用 `no-mask` 开关可以防止这种计算。

```

`paul@laika:~/test$ setfacl --no-mask u:sandra:rw file33`

`paul@laika:~/test$ setfacl file33`

`# file:file33`

`# owner: paul`

`user::rw`

`user:sandra:rw`

`other::r--`

## 34.7. `nautilus`

桌面用户可能想使用 `nautilus` 图形化工具管理 `acls`。

| 基础 | 权限 | 带有 |
|---|---|---|
| 访问控制列表 | | |
| 条目 | 读取 | 写入 | 执行 |
| `paul` | | |
| `sandra` | | |
| `Mask` | | |
| `Other` | | |

你需要安装 `nautilus` 来管理。

```

`paul@laika:~$ install nautilus`

## 第 35 章 链接

`Linux` 拥有许多`硬链接`和`符号链接`。要理解文件系统的链接，首先必须什么是 `inode`。

## 35.1. `inodes`

### 35.1.1. `inode` 内容

`inode` 是包含文件元数据的数据结构。当文件系统在硬盘上存储新文件时，它不仅存储文件的内容（数据），还存储如文件名、创建日期、权限、所有者等额外属性。除了文件名和文件内容的所有信息都存储在文件的 `inode` 中。`ls -l` 命令将显示部分 `inode` 内容，如所示。

```

`root@rhel53 $ # ls -ld /home/project42/`

`drwxr-xr-x 4 root project42 4K Mar 27 14:29 /home/project42/`

### 35.1.2. `inode` 表

`inode` 表包含所有的 `inodes`，并在创建文件系统（`mkfs`）时创建。你可以使用 `df -i` 命令查看挂载的文件系统使用了和剩余多少 `inodes`。

```

`root@rhel53 $ # df -i`

`Filesystem Inodes Used Free IUse% Mounted on`

`/dev/mapper/GroupVol0-lvroot 4947968 115326 483264 3% /`

`/dev/sda1 26104 45 26069 1% /boot`

`tmpfs 64417 1 64416 1% /dev/shm`

`/dev/sda2 262144 2207 259937 4% /home/project42`

`/dev/sdb1 74400 5519 68881 8% /home/project33`

`/dev/sdb5 0 0 0 /home/sales`

`/dev/sdb6 100744 11 100733 1% /home/research`

在上面的 `df -i` 图中，你可以看到几个挂载文件系统的 `inode` 使用情况。你没有看到 `/dev/sdb5` 的数字，因为它是一个 `fat` 文件系统。

### 35.1.3. `inode` 号

每个 `inode` 都有一个唯一的编号（`inode` 号）。你可以通过 `ls -li` 命令查看 `inode` 号。

```

`paul@RHEL4u4:~$ touch file1`

`paul@RHEL4u4:~$ touch file2`

`paul@RHEL4u4:~$ touch file3`

`paul@RHEL4u4:~$ ls -li`

`total 12`

`1234567 -rw-r-- 1 paul 0 file1`

`1234568 -rw-r-- 1 paul 0 file2`

`1234569 -rw-r-- 1 paul 0 file3`

这三个文件连续创建并获得了不同的 `inode`。你看到的所有信息都存在于 `inode` 中，除了文件名（文件名包含在目录）。

### 35.1.4. `inode` 和文件内容

让我们其中一个文件中放入一些数据。

```

`paul@laika:~/test$ ls -li`

`total 16`

`817262 drwxr-xr-x 2 paul 4096 Feb 5 15:38 ..`

`800768 dr-rw-r-- 1 paul 4096 Feb 5 15:42 --`

`817266 -rw-r-- 1 paul 0 Feb 5 15:38 file1`

`817270 -rw-r-- 1 paul 92 Feb 5 15:42 file2`

`817268 -rw-r-- 1 paul 0 Feb 5 15:38 file3`

`paul@laika:~/test$ cat file2`

现在是冬天，非常冷。我们不喜欢冷，我们更喜欢炎热的夜晚。`cat` 命令显示的数据不在 `inode` 中，而在其他地方。`inode` 包含指向该数据的指针。

### 35.2. 关于目录

### 35.2.1. 目录是一个表

目录是一种特殊文件，包含一个将文件名映射到 `inode` 的表。使用 `ls -ali` 查看当前目录将显示文件的内容。

```

`paul@RHELv4u:~/test$ ls -ai`

`total 32`

`817262 drwxr-xr-x 2 paul 4096 Feb 5 15:42 ..`

`800768 dr-rw-r-- 1 paul 4096 Feb 5 15:42 --`

`817266 -rw-r-- 1 paul 0 Feb 5 15:38 file1`

`817270 -rw-r-- 1 paul 92 Feb 5 15:42 file2`

`817268 -rw-r-- 1 paul 0 Feb 5 15:38 file3`

`paul@RHELv4u:~/test$`

### 35.2.2. `.` 和 `..`

你可以看到五个名称，以及它们到五个 `inode` 的映射。`.` 是到自身的映射，而点点 `..` 是到父目录的映射。另外三个名称是到不同 `inode` 的映射。

## 35.3. 硬链接

### 35.3.1. 创建硬链接

当我们对文件创建一个`硬链接`时，目录中会增加一个条目。新文件被映射到一个现有的索引。

```

`paul@RHEL4u4:~~/test$ ln file2 hardlink_to_file2`

`paul@RHEL4u4:~~/test$ ls -li`

`total 24`

`817266-rw-r-- 1 paul 0 Feb 5 15:38 file1`

`817270-rw-r-- 2 paul 92 Feb 5 15:42 file2`

`817266-rw-r-- 1 paul 0 Feb 5 15:38 file3`

`817270-rw-r-- 2 paul 92 Feb 5 15:42 hardlink_to_file2`

两个文件都具有相同的 `inode`，因此它们将始终具有相同的权限和所有者。两个文件都具有相同的内容。实际上，这两个文件现在是等等的，这意味着你可以安全地删除原始文件，硬链接文件将保留。`inode` 包含一个计数器，记录指向自身的硬链接数量。当计数器归零时，`inode` 就会清空。

### 35.3.2. 查找硬链接

你可以使用 `find` 命令查找具有特定 `inode` 的文件。下面的截图显示了如何搜索指向 `inode 817270` 的所有文件名。记住，`inode` 在分区内是唯一的。

```

`paul@RHEL4u4:~~/test$ find -inum 817270 2> /dev/null`

`/home/paul/test/file2`

`/home/paul/test/hardlink_to_file2`

## 35.4. 符号链接

符号链接（有时称为软链接）不链接到 `inode`，而是创建一个名称到名称的映射。符号链接使用 `ln -s` 创建。如下所示，`符号链接` 有自己的 `inode`。

```

`paul@RHELv4:~/test ln -s file2 symlink_to_file2`

`paul@RHELv4:~/test ls -l`

`total 32`

`817273 -rw-rw-- 1 paul paul 13 Feb 17:06 file1`

`817270 -rw-rw-- 2 paul paul 106 Feb 5 17:04 file2`

`817270 -rw-rw-- 1 paul paul 0 Feb 5 15:38 file3`

`817270 -rw-rw-- 2 paul paul 106 Feb 5 17:04 hardlink_to_file2`



817267 lrwxrwxrwx 1 paul paul 5 Feb 5 16:55 symlink_to_file2 -> file2

paul@RHELv4:~/test

符号链接上的权限没有意义，因为应用的是目标文件的权限。硬链接限于它们所在的分区（因为它们指向 inode），而符号链接可以链接到任何地方（其他文件系统，甚至是网络系统）。

## 35.5. 删除链接

可以使用 `rm` 删除链接。

```
paul@laika:-$ touch data.txt
paul@laika:-$ ln -s data.txt sl_data.txt
paul@laika:-$ ln data.txt hl_data.txt
paul@laika:-$ rm sl_data.txt
paul@laika:-$ rm hl_data.txt
```

## 35.6. 练习：链接

1. 创建两个名为 `winter.txt` 和 `summer.txt` 的文件，并在其中放入一些文本。
2. 为 `winter.txt` 创建一个名为 `hlwinter.txt` 的硬链接。
3. 显示这三个文件的 inode 号，硬链接应该具有相同的 inode。
4. 使用 `find` 命令列出两个硬链接文件。
5. 关于文件的所有信息都在 inode 中，但两点除外：说出它们是哪些！
6. 为 `summer.txt` 创建一个名为 `slsummer.txt` 的符号链接。
7. 找到所有 inode 号为 2 的文件。这些信息告诉了你什么？
8. 查看目录 `/etc/init.d/` `/etc/rc2.d/` `/etc/rc3.d/` ... 你看到链接符号（=）了吗？
9. 使用 `ls -l` 查看 `/lib...`
10. 使用 `find` 在你的主目录中查找没有(!!)一个硬链接的普通文件。

## 35.7. 答案：链接

1. 创建两个名为 `winter.txt` 和 `summer.txt` 的文件，并在其中放入一些文本。

```
echo > winter.txt ; echo hot > summer.txt
```

2. 为 `winter.txt` 创建一个名为 `hlwinter.txt` 的硬链接。

```
ln winter.txt hlwinter.txt
```

3. 显示这三个文件的 inode 号，硬链接应该具有相同的 inode。

```
ls -li winter.txt summer.txt hlwinter.txt
```

4. 使用 `find` 命令列出两个硬链接文件。

```
find . -inum xyz # 将 xyz 替换为 inode 号
```

5. 关于文件的所有信息都在 inode 中，但两点除外：说出它们是哪些！
文件名在目录中，而内容位于磁盘的某处。

6. 为 `summer.txt` 创建一个名为 `slsummer.txt` 的符号链接。

```
ln -s summer.txt slsummer.txt
```

7. 告诉你有多个 inode（每个分区一个）。

8. 查看目录 `/etc/init.d/` `/etc/rc2.d/` `/etc/rc3.d/` ... 你看到链接了吗？

```
ls -l /etc/init.d
```

```
ls -l /etc/rc2.d
```

```
ls -l /etc/rc3.d
```

9. 使用 `ls -l` 查看 `/lib...`

```
ls -l /lib
```

10. 使用 `find` 在你的主目录中查找没有一个硬链接的普通文件。

```
find ~ -links 1 -type f
```

# 附录

## 目录

| 章节 | 页码 |
|---|---|
| A.键盘设置 | 338 |
| A.1. 关于布局 | 338 |
| A.2. X布局 | 338 |
| A.3. Shell 布局 | 338 |
| B.硬件 | 340 |
| B.1. 总线 | 340 |
| B.2. 中断 | 341 |
| B.3. I/O 端口 | 342 |
| B.4. DMA | 342 |
| C. 许可证 | 344 |

## 附录 A 键盘设置

### A.1. 关于布局

许多人（如美国人）偏好 US-qwerty 布局。如果你不是来自美国并希望在系统中使用本地布局，最佳实践是在安装时选择。这样键盘布局将始终正确。此外，每当你使用 `ssh` 远程管理 Linux 系统时，将使用本地布局，不受服务器配置的影响。因此可以在运行时更改键盘布局，因为很多人需要这样做。以下是一些对你的建议。

### A.2. X 布局

这是 `/etc/X11/xorg.conf` 中的相关部分，首先是 azerty，然后是 US-qwerty。

```
paul@RHEL5 ~$ grep -i kb /etc/X11/xorg.conf
    "XkbModel" "pc105"
    "XkbLayout" "be"
```

```
paul@RHEL5 ~$ grep -i kb /etc/X11/xorg.conf
    "XkbModel" "pc105"
    "XkbLayout" "us"
```

在 Gnome 或 KDE 或其他图形环境中，查看偏好中的图形菜单，那里有一个选择布局的部分。使用图形菜单而不是编辑 `xorg.conf`。

### A.3. Shell 布局

在 `bash` 环境中，查看 `/etc/sysconfig/keyboard` 文件。下面是一个 US-qwerty 配置，随后是比利时的 azerty 配置。

```
paul@RHEL5 ~$ cat /etc/sysconfig/keyboard
KEYBOARDTYPE="pc"
KEYTABLE="us-latin1"
```

```
paul@RHEL5 ~$ cat /etc/sysconfig/keyboard
KEYBOARDTYPE="pc"
KEYTABLE="be-latin1"
```

键盘本身可以在 `/usr/share/keymaps` 或 `/lib/kbd/keymaps/` 中找到。

```
paul@RHEL5 ~$ ls -l /lib/kbd/keymaps/
total 52
drwxr-xr-x 2 root root Apr 1 00:14  amiga
```

```
drwxr-xr-x 2 root 4096 Apr 1 00:14 atari
drwxr-xr-x 8 root 4096 Apr 1 00:14 i386
drwxr-xr-x 2 root 4096 Apr 1 00:14 include
drwxr-xr-x 4 root 4096 Apr 1 00:14 mac
lrwxrwxrwx 1 root 3 Apr 00:14 -> mac
drwxr-xr-x 2 root 4096 Apr 1 00:14 sun
```

## 附录 B 硬件

### B.1. 总线

#### B.1.1. 关于总线

硬件组件通过 `总线` 与 `处理器` 或 `cpu` 通信。今天最常见的总线是 `usb`、`pci`、`agp`、`pci-express` 和作为 `pc-card` 的 `pcmcmia`。这些都是即插总线。

旧的 `x86` 计算机通常有 `isa` 总线，可以使用 `跳线帽` 或 `拨开关` 进行配置。

#### B.1.2. /proc/bus

要列出 Linux 内核识别的计算机总线，请查看下方 Ubuntu 7.04 和 RHEL4 的 `/proc/bus/` 目录（截图）。

```
root@laika:~# ls /proc/bus/
input pccard pci usb
```

```
root@RHEL4b ~# ls /proc/bus/
input pci usb
```

你能猜到这两个截图是在笔记本电脑上拍摄的吗？

#### B.1.3. /usr/sbin/lsusb

要列出所有连接到系统的 `usb` 设备，你可以读取 `/proc/bus/usb` 内容（如果存在），或使用 `lsusb` 更易读的输出，它在带有 Ubuntu 的服务器上执行。

```
root@shaka:-# lsusb
Bus 001 Device 002: ID 0430:0100 Sun Microsystems, Inc. 3-button Mouse
Bus 001 Device 003: ID 0430:0000 Sun Microsystems, Inc. Type 6 Keyboard
Bus 001 Device 001: ID 04b0:0136 Nikon Corp. Coolpix 7900 (storage)
root@shaka:-#
```



# 如果你有任何新条目，请将其发送给维护者。
# 最新版本可以通过以下地址获取：
# http://www.linux-ux.org/ids
# $Id: us.ids, v 1.225 2006/07/13 04:18:02 dbrowell Exp $

## B.1.5. `/usr/bin/lspci`

要获取所有 PCI 设备列表，你可以查看 `/proc/bus/pci` 或运行 `lspci`（部分输出）。

```
paul@laika:-$ lspci

...

0006.00 FireWire (IEEE 1394): Texas TSB43AB22/IEEE-139...

0008.00 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL-816...

0009.00 Multimedia controller: Philips Semiconductors SAA133/SAAA713...

0010.00 Network controller: Linksys RT2500 802.11g Cardus/mini-PCI

0007.00 RAID bus controller: VIA Technologies, Inc. In. VIA64120 SATA...

0012.00 USB Interface: Intel Corporation, Inc. VTEC56B8A/VTEC686B/A...

0010.00 USB Controller: VIA Technologies, Inc. VT82xxxxx UHCI USB 1...

0010.01 USB Controller: VIA Technologies, Inc. VT82xxxxx UHCI USB 1...

...
```

## B.2. 中断 (interrupts)

### B.2.1. 关于中断

中断或 `IRQ` 是设备向 CPU 发出的请求。当设备需要 CPU 注意时，它会触发一个中断（可能是因为设备已准备好供 CPU 读取）。

自从引入 PCI 以来，`IRQ` 可以在设备之间共享。

中断 0 始终预留给定时器，中断 1 留给键盘。`IRQ` 2 用作 `IRQ` 8 到 15 的通道，这与 `IRQ` 9 相同。

### B.2.2. `/proc/interrupts`

你可以在 `/proc/interrupts` 中查看系统的中断列表。

```
paul@laika:-$ cat /proc/interrupts

CPU

CPU1

0 1320048 555 IO-APIC-edge      timer

1 102244 1 IO-APIC-edge      18042

8 0 0 IO-APIC-edge      parport0

9 2 1 IO-APIC-edge      rtc

10 30662 131 IO-APIC-fastei   acpi

12 151 2 IO-APIC-edge      18042

15 47073 0 IO-APIC-edge      ideal

18 0 1 IO-APIC-fastei   venta

19 31056 1 IO-APIC-fastei   libata,ohci3194

20 19042 1 IO-APIC-fastei   eth0

21 44052 1 IO-APIC-fastei   uhci_hcd:usbl,uhci_hcd:usb2,...

22 188352 1 IO-APIC-fastei   rao
```

### B.2.3 `dmesg`

你也可以使用 `dmesg` 查找启动时的 `IRQ`。

```
paul@laika:~$ dmesg | grep irq 1[45]

[ 28.930069] ata3: PATA max UDMA/133 cmd 0x1f0 c0tl1 0x376 bmdma 0x2090 irq 14

[ 28.930071] ata4: PATA max UDMA/133 cmd 0x170 c0tl1 0x376 bmdma 0x2098 irq 15
```

## B.3. I/O 端口 (io ports)

### B.3.1. 关于 I/O 端口

反方向的通信（从 CPU 到设备）通过 IO 端口发生。CPU 向设备的 IO 端口写入数据或控制代码。这不仅仅是单向通信，CPU 还可以使用设备的 IO 端口读取有关设备的状态信息。与中断不同，端口不能共享！

## B.3.2. `/proc/ioports`

你可以通过 `/proc/ioports` 查看系统的 IO 端口列表。

```
[root@RHEL4b ~]# cat /proc/ioports

0000-001f : dma1

0020-002f : pic1

0040-004f : timer0

0050-0053 : timer1

0060-006f : keyboard

0070-007f : rtc

0080-008f : dma page reg

00a0-00a1 : pic2

00c0-00cf : dma2

00e0-00ef : fpu

0170-0177 : idel
```



无论是商业还是非商业用途均可，前提是所有副本都必须复制了本许可证、版权声明以及说明本许可证适用于本文档的许可公告，且您不得使用任何超出本许可证范围的条件。您不得使用技术措施来阻碍或控制您所收到的副本的阅读或进一步分发。但是，您可以接受以交换副本的补偿。如果您分发了大量副本，还必须遵守第 3 节中的条件。

您可以在上述相同条件下出借副本，并展示副本。

## 3. 大批量复制

如果您出版了数量超过 100 份的本文档打印副本（或通常有打印副本的介质副本），且副本的封面需要“封面文本”（`Cover Texts`），则必须将副本装在封内内，并在封上清晰、易读地载明所有这些封面文本：正封面上的“封面文本”和封底上的“封底文本”。这些封面还必须清晰、易读地标识您为出版者，并展示全文，且标题的所有文字均同等显著且可见。您还可以在封面上添加其他材料。对封面进行修改的复制，只要保留了本文档的标题并满足这些条件，在其他方面可以被视为逐字复制。

如果每个封面所需的文本量太大而无法合法地容纳，您应该将列出的前面的文本（在合理范围内能容下的数量）放在封底，并将剩余部分延续相邻页面。

如果您出版或分发了数量超过 100 份的本文档不透明副本（`Opaque copies`），您必须在每份不透明副本旁包含一份机器可读的透明副本（`Transparent copy`），或者在每份不透明副本注明一个计算机网络位置，通用网络可以通过标准网络协议从那里下载免费添加材料副本。

如果您使用后者，在开始大量分发不透明副本时，必须合理地停止，以确保在最后一次向公众（直接或通过您的代理或零售商）分发该不透明副本后的至少一年内，透明副本仍保持在该位置。

建议（而非要求）您在重新分发任何大量副本之前联系本文档的作者，以便他们有机会为您提供更新版本的本文档。

## 4. 修改

您可以在第 2 节和第 3 节的条件下复制并分发本文档的修改版本（`Modified Version`），前提是您必须完全按照本许可证发布修改版本，由修改版本承担本文档的角色，从而许可任何拥有该版本副本的人对修改版本进行分发和修改。此外，您必须在修改版本执行以下操作：

- A. 在标题页（以及封面页，如果有）使用与本文档标题不同、且与之前的版本不同的标题（如果存在之前的版本，则应列在本文档的“历史”部分中）。如果该版本的原始出版者给予了许可，您可以使用与之前的版本相同的标题。
- B. 在标题页上列出负责修改版本中修改的一或多个个人或实体作为作者，同时列本文档的至少五位主要作者（如果作者少于五位，则列出所有作者），除非他们免除了此项要求。
- C. 像其他副本一样，在标题页上注明修改版本的出版者名称。
- D. 保留本文档的所有版权声明。
- E. 在其他副本旁边添加您的修改的适当版权声明。
- F. 在版权声明之后立即包含一份许可公告，允许公众根据下方附录中列出的许可证条款使用修改版本。
- G. 在该许可证中保留“不变章节”（`Invariant Sections`）的完整列表，并在文档许可公告中保留封面文本。
- H. 包含一份未经更改的许可证副本。
- I. 保留“历史”部分，保留其标题，并添加添加一个项目，说明标题页上给出的修改版本的标题、年份、新作者和出版者。如果文档中没有该部分，则创建一个，说明标题页上给出的文档的标题、年份、作者和出版者，并添加一个描述前一节所述修改版本的项目。
- J. 保留文档中给出的供公众访问本文档的地址（如果有），同样保留文档中给出的其基于之前的版本的网络位置。如果网络已发生变化，
- K. 保留文档中给出的供公众访问本文档的地址（如果有），同样保留文档中给出的其基于之前的版本的网络位置。如果网络已发生变化，
- L. 保留文档中给出的供公众访问本文档的地址（如果有），同样保留文档中给出的其基于之前的版本的网络位置。如果网络已发生变化，
- M. 保留文档中给出的供公众访问本文档的地址（如果有），同样保留文档中给出的其基于之前的版本的网络位置。如果网络已发生变化，
- N. 保留文档中给出的供公众访问本文档的地址（如果有），同样保留文档中给出的其基于之前的版本的网络位置。如果网络已发生变化，
- O. 保留文档中给出的供公众访问本文档的地址（如果有），同样保留文档中给出的其基于之前的版本的网络位置。如果网络已发生变化。

# 许可证

翻译被视为一种修改，因此您可以根据第 4 节的条款分发文档的翻译版本。用翻译替换“不变部分”（`Invariant Sections`）需要版权所有者的特殊许可，但您可以在包含不变部分原始版本的基础上，包含部分或全部不变部分的文本。您可以包含本许可证的公告、文档中的所有许可证公告以及任何免责声明，前提是您必须包含本许可证的原始英文版本以及公告和免责声明的原始版本。如果翻译版本与许可证、公告或免责声明的原始版本出现分歧，以原始版本为准。

如果文档中的某节名为“致谢”（`Acknowledgements`）、“献辞”（`Dedications`）或“历史”（`History`），则保留其标题（第 1 节）的要求通常意味着需要更改实际标题。

# 9. 终止

除非本许可证明确规定，否则您不得复制、修改、分许可或分发文档。任何其他复制、修改、分许可或分发文档的尝试均无效，并将自动终止您根据本许可证享有的权利。

然而，如果您停止了对本许可证的所有违反行为，则您从特定版权所有者处获得的许可将恢复：(a) 临时恢复，直到版权所有者明确并最终终止您的许可；(b) 如果版权所有者在停止行为后的 60 天内通过某种合理手段通知您存在违反行为。

此外，如果版权所有者通过某种合理手段通知您违反行为，且这是您首次收到该版权所有者关于违反本许可证（针对任何作品）的通知，并且您在收到通知后 30 天内发生了违反行为，则您从特定版权所有者处获得的许可将永久恢复。

您根据本节享有的权利终止，并不终止根据本许可证从您处获得副本或权利的方的许可。如果您的权利已被终止且未被永久恢复，接收部分或全部材料的副本并不赋予您使用它的权利。

# 10. 本许可证的未来修订

自由软件基金会（`Free Software Foundation`）可能会随时发布 `GNU` 自由文档许可证的新修订版本。此类新版本将与当前版本相似，但在细节上可能会不同，以解决新的问题或关注。请参见 `http://www.gnu.org/licenses/`

许可证的每个版本都有一个不同的版本号。如果文档指定适用于您的本许可证的特定编号版本“或更高版本”，则您可以选择遵循该特定版本或由自由软件基金会发布（非以草稿形式发布）的更高版本的条款和条件。如果文档未指定本许可证的版本号，您可以选择自由软件基金会发布过的任何版本（非以草稿形式发布）。如果文档指定代理人可以决定可以使用本许可证的哪些未来版本，则代理人对某个版本的公开声明接受将永久性约束您在文档中使用选择该版本。

# 11. 重新许可

大规模作者协作站点（`Massive Multiauthor Collaboration Site`，或“`MMC` 站点”）是指任何发布受版权保护的作品并为任何人编辑这些作品提供设施的万网服务器。任何人都可以编辑的公共 `wiki` 是此类服务器的示例。站点中包含的“大规模作者协作”（或“`MMC`”）是指在 `MMC` 站点上如此发布的任何受版权保护的作品集。

`CC-BY-SA` 指由知识产权组织（`Creative Commons Corporation`）发布的知识产权署名-相同方式共享 3.0 许可证，该组织是一家总部位于加利福尼亚州旧金山的非营利机构，以及该组织发布的该许可证的未来拷贝共享版本。

“授权”（`Authorize`）是指将文档全部或部分作为另一份文档重新发布。

如果一个 `MMC` 根据本许可证许可，并且所有最初在非 `MMC` 以外的地方根据本许可证发布并随后全部或部分合并到该 `MMC` 中的的作品符合以下条件，则该 `MMC`“符合重新许可条件”：(1) 没有封面文本或不变部分，且 (2) 是在 2008 年 11 月 1 日之前合并的。

`MMC` 运算符可以在 2009 年 8 月 1 日之前的任何时间在同一站点上以 `CC-BY-SA` 重新发布该站点内的 `MMC`，前提是该 `MMC` 符合重新许可条件。

# 索引

| 符号 | |
| :--- | :--- |
| ( (shell) | 136 |
| ! (shell) | 156 |
| ! (bash history) | 256 |
| ! (file globbing) | 163 |
| ? (file globbing) | 162 |
| / | 76, 102 |
| /bin | 103, 128 |
| /bin/bash | 125, 292 |
| /bin/cat | 103 |
| /bin/sh | 225 |
| /bin/date | 103 |
| /bin/ksh | 125, 292 |
| /bin/rm | 125 |
| /boot | 105 |
| /boot/grub | 105 |
| /boot/grub/grub.cfg | 105 |
| /boot/grub/grub.conf | 105 |
| /dev | 85, 109 |
| /dev/null | 109, 175 |
| /dev/pts/1 | 109 |
| /dev/random | 120 |
| /dev/tty1 | 109 |
| /dev/urandom | 119, 121 |
| /dev/zero | 120 |
| /etc | 105 |
| /etc/bashrc | 293 |
| /etc/default | 276 |
| /etc/fstab | 326 |
| /etc/group | 299, 308 |
| /etc/hosts | 105 |
| /etc/init.d/ | 105 |
| /etc/input | 292 |
| /etc/login.defs | 286 |
| /etc/passwd | 191, 225 |
| /etc/profile | 292 |
| /etc/resolv.conf | 120 |
| /etc/shadow | 283, 285, 321, 301 |
| /etc/shells | 235, 278 |
| /etc/skel | 277 |
| /etc/sudoers | 269, 270 |
| /etc/sysconfig | 105 |
| /etc/sysconfig/firstboot | 106 |
| /etc/sysconfig/hardlinks | 106 |
| /etc/sysconfig/hwconf | 106 |
| /etc/sysconfig/keyboard | 106 |
| /etc/X11/xorg.conf | 105 |
| /export | 107 |
| /home | 107 |
| /lib | 104 |
| /lib/kbd/keymaps/ | 106 |
| /lib/modules | 104 |
| /lib/32 | 104 |
| /lib/64 | 104 |
| /media | 107 |
| /opt | 104 |
| /proc | 85, 109 |
| /proc/bus | 340 |
| /proc/bus/pci | 341 |
| /proc/bus/dev/ | 340 |
| /proc/epinfo | 110 |
| /proc/dma | 342 |
| /proc/interrupts | 112, 341 |
| /proc/ioports | 342 |
| /proc/xcore | 112 |
| /proc/scys | 111 |
| /root | 107 |
| /run | 117 |
| /sbin | 103, 128 |
| /svr | 107 |
| /sys | 113 |
| /tmp | 108, 320 |
| /usr | 114 |
| /usr/bin | 114 |
| /usr/bin/getfac | 326 |
| /usr/bin/passwd | 321 |
| /usr/bin/setfac | 326 |
| /usr/include | 114 |
| /usr/lib | 114 |
| /usr/local | 114 |
| /usr/share | 114 |
| /usr/share/games | 115 |
| /usr/share/man | 115 |
| /usr/src | 115 |
| /var | 116 |
| /var/cache | 116 |
| /var/lib | 117 |
| /var/lib/rpm | 117 |
| /var/lib/ututils/usb.db | 340 |
| /var/lock | 117 |
| /var/log | 116 |
| /var/log/messages | 116 |
| /var/log/syslog | 116 |
| /var/run | 117 |
| /var/spool | 116 |
| /var/tmp | 117 |
| .. | 75 |
| .. (directory) | 331 |
| . (shell) | 156 |
| .bash_history | 157 |
| .bash_login | 293 |
| .bash_logout | 294 |
| .bash_profile | 292 |
| .bashrc | 292, 293 |
| .exrc | 229 |
| .vmrc | 229 |
| . (backtick) | 151 |
| . | 75 |

| C | |
| :--- | :--- |
| ' (single quote) | 151 |
| * (double quotes) | 127 |
| ((shell) | 256 |
| -- (shell) | 237 |
| - (file globbing) | 163 |
| - [shell] | 241 |
| $ (shell variables) | 136 |
| $ embedded shell | 151 |
| $ (shell variables) | 142 |
| SHISTFILE | 157 |
| SHISTFILESIZE | 157 |
| SHISTSIZE | 157 |
| SLANG | 164 |
| SPATH | 128, 145 |
| * | 76 |
| * (file globbing) | 162 |
| * (slashes) | 138 |
| & | 136 |
| #/bin/bash | 235 |
| # (shell) | 235 |
| # (pound sign) | 138 |
| > | 173 |
| >> | 174 |
| ] | 117 |
| 2> | 175 |
| 2> | 175 |
| 2&.1 | 175 |
| 777 | 314 |
| cal | 198 |
| case | 258 |
| case sensitive | 85 |
| cat | 192 |
| cd | 75 |
| cd- | 76 |
| CentOS | 7 |
| chage | 286 |
| chgrp(1) | 309 |
| chconf | 106 |
| chmod | 274 |
| chmod(1) | 226, 313 |
| chmod +x | 235, 315 |
| chown | 277 |
| chown(1) | 309 |
| chsh | 278 |
| chsh | 235 |
| Ctrl | 96 |
| ctrl-r | 157 |
| current directory | 75 |
| cut | 191 |
| cut(1) | 184 |

```
env(1), 146, 146
隐藏文件, 77
环境变量, 142
EOF, 96, 177
转义字符 (shell), 165
HP-UX, 4
eval, 256
http://www.pathname.com/fhs/, 102
可执行文件, 103
```

# I

```
exit (bash), 157
IBM, 4
export, 146
id, 267
```

# F

```
IEEE 1394, 113
Fedora, 7
if then else (bash), 242
FHS, 102
inode, 329, 332
文件, 85
inode 节点, 330
file(1), 104
插入模式(vi), 223
文件闪烁, 161
中断, 341
文件所有权, 308
IO 端口, 342
文件系统层次结构标准 (Filesystem Hierarchy Standard), 102
IRQ, 341
过滤器, 181
isa, 340
find(1), 196, 320, 332
```

# K

```
FreeWire, 113
Ken Thompson, 4
for (bash), 242
内核, 104
FOSS, 10
keymaps(5), 106
自由自由, 11
自由软件 (Free Software), 10
Korn shell, 158
Korn Shell, 278
自由软件, 10
ksh, 158, 235
免费软件, 10
函数 (shell), 259
```

# L

```
gcc(1), 285
less(1), 98
getfac, 326
let, 257
getopry, 251
Linux Torvalds, 4
GID, 296
Linux Mint, 7
glob(7), 162
In, 338
GNU, 4
ln(1), 332
gpasswd, 301
loadkeys(1), 106
GPL, 11
locate(1), 197
GPL, 31
逻辑与, 137
grep, 206, 207, 210
逻辑或, 137
grep(1), 182
grep -v, 183
Libibc, Libre, 10
ls, 77, 311, 330
grep -v(1), 299
ls(1), 77, 330
groupadd(1), 300
ls -l, 310
groupmod(1), 300
lspci, 341
groups, 298
lsusub, 340
groups(1), 299
```

# M

```
gunzip(1), 200
magic, 85
zip, 200
makewhatis, 73
gzip(1), 200
man(1), 72, 72, 73
```

# H

```
mand(1), 72, 73
硬链接, 332
man -k, 72
head(1), 95
md5, 285
here 指令, 197
mkdir(1), 79, 315
here document, 177
mkdir -p, 79
here string, 177
mkfs, 330
more(1), 98
mv, 89
```

# S

```
salt (加密), 285
Scientific, 7
sed, 190, 215, 216
set, 152
set(shell), 143
set +x, 130
setfacl, 326
setgid, 330, 320
setuid, 237, 231, 321, 321
set -x, 130
she-bang (shell), 235
shell, 291
shell 注释, 138
shell 嵌入, 151
shell 转义, 138
shell 扩展, 126, 226
shell shift, 249
shopt, 252
骨架, 105
sleep, 198
软链接, 333
Solaris, 4
sort, 191
sort, 186
source, 236
标准输入, 96
标准输出, 96
stderr, 172
stdin, 172, 182
sticky bit, 320
strings(1), 98
su, 266
su, 297, 268, 301
sudo - ,
sudo, 270
Sun, 4
SunOS, 4
super, 275
sys link, 333
sysfs, 104
System V, 4
```

# N

```
noclobber, 174
```

# O

```
进制权限, 314
od(1), 189
open source, 2
open ,, 0
opens,, 44
Linux,,7
```

# P

```
目录, 75
--,             ,,,
, 283, 284
passwd(1), 73, 321
主用户组, 276
专有软件, 10
push, 83
```

# R

```
随机数, 122
read, 249
reboot, 157
Red Hat, 7
正则表达式, 158
rename, 90
仓库, 6
Richard Stallman, 4
rm, 87
rm(1), 333
rmdir, 79
rmdir -p, 80
rm -rf, 87
root, 268, 269, 270, 275
root目录, 102
rpm, 117
```

# T

```
tab 键(bash), 77
tac, 97
tail(1), 95
test(1), 182
test, 241
time, 199
touch(1), 86
tr(1), 184
type(shell), 128
```

# U

```
Ubuntu, 7
umask(1), 315
ualias(bash), 130
uniq, 191
uniq(1), 187
Unix, 4
unset, 152
unset(shell), 143
until (bash), 243
updatedb(1), 197
usb, 113, 340
useradd, 276, 277, 284
useradd(1), 277
useradd(-D), 276
userdel(1), 276
usermod, 287, 287, 302
usermod(1), 276
```

# V

```
vi, 302
vi(1), 222
vigr(1), 302
vim(1), 222
vim-tutor(1), 222
vipw, 287
visudo, 269
自由软件, 10
```

# W

```
w, 267
wct(1), 185
whatis(1), 72
whereis(1), 72
which(1), 128
while (bash), 243
空格符(shell), 126
who, 191, 267
whoami, 267
who am i, 267
通配符, 163
```

# X

```
X, 105
X Window System, 105
```

# Z

```
zcat, 200
zmore, 200
```
