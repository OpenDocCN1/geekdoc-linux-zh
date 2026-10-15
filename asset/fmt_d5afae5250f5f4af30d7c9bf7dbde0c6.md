
```bash
title=Gentoo Linux
root (hd0,0)
kernel /kernel-2.6.13-gentoo-r3 root=/dev/hd0
initrd /initrd-2.6.13-gentoo-r3
```

### 32. 重启。
运行 `umount` 卸载分区并按照如下方式重启退出根分区：

```bash
# exit; cd /
# umount /mnt/gentoo/proc /mnt/gentoo
# reboot
```

移除安装盘并允许计算机从硬盘启动。几分钟后，你应该能看到 GRUB 界面。选择 Gentoo Linux（按回车）。

从现在起，你将从硬盘启动并直接在操作系统中工作。如果你安装有问题，会看到错误消息（例如缺少内核驱动程序），我建议去 http://forums.gentoo.com 搜索导致问题的驱动程序。很有可能其他人遇到过相同的问题，并能为你提供解决方案。

![](img/a2d958d7eab32ca5b89b2b8af808aa70_428_0.png)

# 398 第三部分 ♦ 选择并安装 Linux 发行版

### 33. 安装桌面环境。
对于我们大多数人来说，仅仅通过命令行工作是不够的。以下命令安装了一套基础桌面包，包括 X Window 系统 (`xfree`)、KDE 桌面 (`kde`)、Mozilla 浏览器 (`mozilla`) 和 Openoffice 办公套件 (`openoffice-bin`)。通过网络安装这些需要很长的时间！

```bash
# emerge xfree kde mozilla openoffice-bin
```

作为替代，如果你在 CD-ROM 上有这些包，可以使用以下命令识别包的位置并从该位置进行安装：

```bash
# export PKGD1="* /mt/cdrom/packages"
# emerge -k kde mozilla openoffice-bin
```

你也可以通过只安装 GNOME 或 KDE（而不是两者）来节省时间。如果你不计划创建文档或电子表格，可能不需要安装 `openoffice-bin`。

### 34. 配置 X。
现在你的桌面软件已经安装完成，你需要配置 X Window 系统使其与你的显卡和显示器正常工作。输入你的显卡和显示器的配置类型：

```bash
# /usr/X11R6/bin/xf86_config
```

到此时，你应该已经拥有了一个 Gentoo 系统。如需更多文档，请查看 www.gentoo.org/doc/en/index.xml。

## 总结

在几年里，Gentoo 已经成为 Linux 爱好者的首选发行版，这些爱好者热于对 Linux 系统的组件和设置进行完全控制。

Portage 的核心是 Portage 包管理系统。使用 Portage `emer` 命令，你可以安装成千上万个 Gentoo 软件包，这些软件包可以被下载并从头开始构建，并根据你为使用 Linux 系统而选择的设置进行定制。

如果你不想学习 Linux 系统的内部工作原理（并花费大量时间让它运行），那么 Gentoo 可能并不适合你。一个经验丰富的 Linux 用户通常需要尝试几次才能让 Gentoo 运行起来，而某些人在没有大量帮助的情况下可能完全无法安装和运行它。然而，如果你想调优和修改你的操作系统，Gentoo 是一个极佳的选择。

# 第14章

# 运行 Slackware Linux

## 本章内容

老牌 Linux 用户在谈起他们使用的第一个 Linux 发行版时，很多人会说是 Slackware。Slackware 是仍在活跃开发的最老的 Linux 发行版。尽管它没有花哨的图形安装程序或专门的 GUI 工具，但 Slackware 仍然拥有许多忠实的粉丝，并且是获取基础 Linux 系统的良好方法。本章探索了 Slackware 发行版，讨论了它的优缺点，并介绍了使用它的人。它解释了如何安装 Slackware。

![](img/a2d958d7eab32ca5b89b2b8af808aa70_430_0.png)

两个 Slackware 10.2 CD 镜像位于本书的附录中。你可以按照附录 A 中的描述将这些镜像刻录 CD。你也可以从 Slack Store (http://store.slackware.com) 购买 Slackware。

- 进入 Slackware
- Slackware 社区特征
- 安装 Slackware
- 启动 Slackware

## 进入 Slackware

虽然全图形化安装和 GUI 管理工具可以让 Linux 的安装和配置变得简单，但这些工具带有开销。它们还隐藏了一些 Linux 配置的细节。

正如 Slackware 致力于 Slackware 的价值，他们可能会背诵他们的格言“45法则”：稳定 (Stable)、稳固 (Solid)、简单 (Simple) 和合理 (Sensible)。通过保持基础性，Slackware 提供了以下优势：

- **基础理解**——因为你在 Slackware 中使用命令和配置文件，所以你学到更多关于 Linux 内部运行原理的知识。大多数图形安装程序都隐藏了 Linux 配置的一些细节。

# 第 14 章 运行 Slackware Linux 401

在其他 Linux 发行版中可以做的任何事情，在 Slackware 中都可以做到。这可能需要更多的手动操作才能实现目标。Slackware 并没有官方使用像红帽软件包管理器 (RPM) 或 Debian 文件那样的全功能包管理系统。然而，某些包管理工具与 Slackware 的原生包格式兼容：gzipped 压缩归档（我稍后会描述这些工具）。通常情况下，大多数用户都会变得熟练于构建和安装自己的应用程序（使用 `tar`、`make` 和类似工具）。

Slackware 自带一套良好的库，可以处理大多数 Linux 应用程序的依赖需求。对于视频、音频某些其他类型的应用程序，你可能会发现自己一直在到处寻找库。在其他发行版中为你节省这些麻烦的包依赖满足工具（如 `yum` 和 `apt`）开始针对 Slackware 开发或适配。

## Slackware 社区的特征

与许多其他成功的 Linux 发行版一样，Slackware 由一个意志坚定的个人创立，他创建了适合自己的 Linux 系统。Slackware 用户是相当认同这个发行版的人。

### Slackware 的创建者

Patrick Volkerding 在 1993 年创立了 Slackware，作为一个供自己和朋友使用的 Linux 发行版。他很愿意回答我关于 Slackware 的一些问题，我想把他的回答分享给你们：

Patrick 最初使用一种名为 SLS Linux 的发行版（命名为 Soft Landing Linux，即制作它的公司）。他为什么不选择留在 SLS 而创建自己的发行版呢？

> Patrick：我尝试过。到 1993 年 4 月，我已经在 SLS 中收集了一份巨大的错误列表，以及针对大部分错误的修复方案。有很多人可以把这些提交给 Peter McDonald（SLS 的作者/维护者），但 SLS 中的错误（其中很多非常显而易见）从未被修复。
>
> 当然，我当时致力于我的补丁版 SLS 版本，并没有发布长期发行版的计划。我当时想，只要把它放到网上，SLS 就会修复这些问题，可能就此了。SLS 是一个很棒的发行版，但它所开启的许多想法没有得到足够的认可。遗憾的是，当时 Peter 忙于发明内核模块，导致 SLS 在网上挂了几个月，满是错误且没有得到任何更新。

## 402 第三部分 选择和安装 Linux 发行版

在 MacDonald 建议 Slackware 侵犯了他的版权之后，Patrick 决定迈出一步，将 Slackware 从 SLS 中分离出来（尽管 SLS 代码的唯一许可是“自由分发；不限制。”）。

**Patrick:** 所以，我向 Peter 承诺我会为 Slackware 写一个全新的安装程序，而不是使用修改过的 SLS 安装程序，而且新的安装程序将是 Slackware 在线进行的下一个更改。

Slackware 从一开始就取得巨大成功让他感到惊讶吗？

**Patrick:** 绝对是。我比当时出的其他发行版更了解它，但我并没有料到会发生从 SLS 的大规模迁出。

什么样的人会选择 Slackware 而不是其他 Linux 发行版？

**Patrick:** 它似乎吸引了那些想要用老办法配置 Slackware（使用文本编辑器），并且不希望有必要的程序在后台运行的用户。我尽量减少在编译 Slackware 时加入我自己的修改，如果你决定走那条路，这也使得从源码更新变得变得简单。

在 Linux 早期，我认为大多数用户都是这样的。随着时间的推移和各种发行版专注于不同的市场，平均 Linux 用户的画像发生了很大变化。今天大多数商业 Linux 发行版似乎都针对想要像 Windows 一样通过点击式界面管理机器的用户。Slackware 和其他低级发行版服务于不同的众群——那些不介意操作系统时有学习曲线、只要系统不干扰他们的用户。
