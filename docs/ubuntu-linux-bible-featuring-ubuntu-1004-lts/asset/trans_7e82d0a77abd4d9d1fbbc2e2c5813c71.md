

## 启用额外的仓库组件

你想要访问除主（main）和受限（restricted）组件之外仓库组件的最常见情况是处理音频和视频应用程序。用于编码数字音频和视频的各种编码器（压缩/解压缩模块）、这些编码器特定平台的根源，以及许多媒体公司为了在 Ubuntu Linux 系统上实际播放数字音频和视频格式而让你跨越的重重障碍，都使得扩展自由软件许可的边界变得必要。

默认情况下，在安装 Ubuntu Linux 发行版时，Ubuntu 仓库的主（main）、受限（restricted）和多用途（multiverse）组件都是启用的。启用意味着这些仓库组件的源包含在默认的 `/etc/apt/sources.list`文件中，这是一个文本文件，本章讨论的所有软件包安装和管理工具在查找新软件和更新软件时都会查询它。该文件的条目描述了不同的在线仓库的位置、名称以及可用的仓库组件`/etc/apt/sources.list` 中一个条目的通用格式如下：

```
deb URI distribution component-or-package(s)
```

`deb` 标识包格式；`URI` 是查找仓库位置的通用资源标识符，通常是 FTP 或 HTTP URL。`distribution` 字段通常是标准 Ubuntu 发行版的名称，但也可以任何用于标识 URI 下关联软件包所在子目录的名称，而 `component-or-package` 是仓库组件或软件包的一个（或多个）名称，这些名称也用于导航 URI 下的目录树并定位可用软件包。如果提供了多个 `component-or-package` 名称，每个名称都代表 URI 下的一个不同条目。

例如，Ubuntu Linux 10.04 版本的 `/etc/apt/sources.list` 文件中主和受限仓库组件的条目如下：

```
deb http://archive.ubuntu.com/ubuntu/ lucid main
deb-src http://archive.ubuntu.com/ubuntu/ lucid restricted
```

其中第一个标识二进制包的源，而第二个标识源包的源。类似的一对条目提供了对这些仓库组件中更新版本软件包的访问：

后两个条目为了书中的排版被拆分成了两行；它们在实际的 `/etc/apt/sources.list` 文件中是单行显示的。

## 第 19 章：添加、删除和更新软件

### 注意事项

本节中的示例反映了 Ubuntu 10.04 (Lucid) 版本的 `/etc/apt/sources.list` 设置。如果你正在使用不同的发行版本，你应该将这些示例中的 `lucid` 词替换为你正在使用的 Ubuntu 发行版名称。你不应该在 `/etc/apt/sources.list` 文件中混合不同发行版本的仓库条目，因为新版本的仓库通常会提供与旧版本仓库相同的软件，并且是针对新版本中找到的一组系统库编译的。

最后，类似的一对条目提供了对这些仓库组件中软件包安全修复的访问：

`/etc/apt/sources.list` 文件中以井号 (`#`) 开头的行是注释。如果你查看系统上默认 `/etc/apt/sources.list` 文件的行，你会发现访问伙伴仓库（partner repository）的条目已经存在，但被注释掉了。你可以通过 `sudo` 在你喜欢的编辑器中编辑此文件来启用对该仓库的访问。要这样做，请使用你喜欢的编辑器编辑 `/etc/apt/sources.list` 文件，使用如下命令：

```
$ sudo nano /etc/apt/sources.list
```

删除启用伙伴仓库的行开头的井号并保存更新后的文件。示例 `sources.list` 文件中更新后的条目如下：

```
deb http://archive.ubuntu.com/ubuntu/ lucid partner
deb-src http://archive.ubuntu.com/ubuntu/ lucid partner
```

你也可以简单地将这些条目添加到已经提供 Ubuntu 仓库主、受限、universe 或 multiverse 组件的行的末尾，但我更倾向于将它们分开，以便明确授权许可方面的差异——而且这样最接近默认 `sources.list` 文件的原始格式。

### 注意事项

为了完全清楚起见，从 universe 和 multiverse 仓库安装软件可能会向你的系统添加你或你工作的公司认为难以接受的具有许可要求的软件（例如与 MP3 相关的或视频相关的软件），Ubuntu 的人员不保证提供此类软件的支持（即使你购买了支持，也没有承诺），而且这些软件在任何地方都可能获得支持。如果你正在为企业级使用配置系统，请确保你的公司对 universe 和 multiverse 仓库中非自由软件提供的许可表示接受。我使用了书中讨论的所有软件，因此我是这本书书中讨论的每一个内容的极测试用例，但你的情况（以及你的责任）可能会有所不同。

## 第二部分：Ubuntu 桌面用户

## 其他感兴趣的仓库

如上一节所示，标准的 Ubuntu 仓库都托管在 `ubuntu.com` 域名的系统上。这完全合理，因为这是 Canonical 的人员确保其仓库完整性以及各种组件及其内容符合相关许可指南的唯一方法。然而，Ubuntu 软件的额外仓库将提供互联网上可用的条目示例（我知道这很意外），这些仓库由各种小组和个人维护。这些替代仓库站点可能只是官方 Ubuntu 仓库内容的镜像以“分担”，也可能提供官方 Ubuntu 仓库中找不到的软件。在最后一种情况下，这些软件可能提供比本地维护软件备份中更新的流行软件版本。正如前面提到的，如果你感兴趣在你的 Ubuntu 系统上处理音频和视频，你可能会发现这些替代仓库站点提供了你需要的具有前沿特性的相关软件版本。在这些站点上，你应该将条目添加到你的 `/etc/apt/sources.list` 文件中，以便从那里列出并检索软件。这通常通过使用文本编辑器将新条目连接到该文件的末尾完成，也可以使用下一节讨论的“软件源”（Software Sources）工具完成。

非官方但免费的软件包是一回事，更常见的需求是定位并安装具有各种许可限制的软件。Linux 的一个经典问题是，用于播放 CD、音频文件、DVD 和视频文件的编码器以及大部分相关软件是专有软件，需要许可，在 Linux 系统上不可用，有时甚至二者兼有。这并不是 Linux 的错，而是软件和音频/视频媒体行业中贪婪和无知的侧效应，以及有关软件专利、版权和知识产权的特定地区法律。尽管最近几个版本提供了越来越简便的方法来获取有问题的音频/视频软件包，但你可能仍然需要从非官方（或某些非 Canonical 的）仓库手动获取你需要的某些软件包。关于此类软件包的一个很好的网站是位于 `www.meduntu.org` 的 Meduntu（Multimedia, Entertainment & Distractions in Ubuntu）网站。其“仓库教程”（Repository Howto）链接到了关于如何向 `/etc/apt/sources.list` 文件添加仓库的文档，这将让你能够在 Ubuntu 系统上播放合法购买的音频视频 CD 和 DVD。

## 使用软件源工具启用额外的仓库源

编辑文本格式的配置文件是相当老派的 Linux 操作，也是你可能不想向你的 Windows 或 Mac OS X 朋友提到的事情。（你仍然可以这样做，因为既快又简单，但我们将这种事情作为你自己的 Linux 小秘密，好吗？）对于喜欢图形界面的的用户，Ubuntu 提供了一个“软件源”（Software Sources）工具，它为你提供了 `/etc/apt/sources.list` 文件中条目的图形化视图，并让你通过几次点击轻松启用、禁用或添加条目。

