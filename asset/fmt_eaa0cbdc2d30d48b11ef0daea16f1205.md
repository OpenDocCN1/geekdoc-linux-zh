
此时，是时候向证书中添加一些信息了。在此之前，你必须通过输入之前输入的密码来解锁你刚刚创建的私钥。然后按照以下程序操作：

你将被要求输入将包含你的证书请求中的信息。
你即将输入的内容被称为区别名称（Distinguished Name，简称 DN）。
有许多字段可以留空。
某些字段将有一个默认值。
如果你输入 `.`，该字段将留空。

# 238 第二部分 | 运行演示

```
国家名称（2位代码） [GB]: US
州或省名称（全名） [Berkshire]: Ohio
地区名称（例如，城市） [Newbury]: Cincinnati
组织名称（例如，公司） [My Company Ltd]: My Company Ltd
组织单位（例如，部门） []:Industrial, Inc.
通用名称（例如，你的域名） []:industrialpress.com
电子邮件地址 []:webmaster@industrialpress.com
```

## 启动你的 Web 服务器

## 故障排除你的证书

## 总结

## 选择 Linux 发行版

今天有数百种 Linux 发行版可用。其中一些是通用发行版，可以作为桌面、服务器或工作站系统使用；另一些则是专为商业或计算机爱好者设计的。本书的意图之一是帮助你选择最适合你的一种（或多个）发行版。

使用书中附带的 DVD，你可以直接启动到 `KNOPPIX`（在不安装到硬盘的情况下尝试 Linux）或启动到 `Fedora Core 4`（在你的电脑硬盘上安装 Linux）。因为书中附带的 `Fedora Core 4` 是完整的 PC4 版本，你可以安装全范围的桌面界面、应用程序、编程工具和服务器功能。在你尝试过 `KNOPPIX` 并准备好在硬盘上安装 Linux 后，我向你推荐 `Fedora`。

使用书中附带的 CD，你可以启动到 `Damn Small Linux`（一个较小的 Linux 系统）或 `Debian`（对你的硬盘进行网络安装）。这两个发行版可以配置为运行在较旧且性能较低、有 CD 驱动器但没有 DVD 驱动器的电脑上。对于 `Debian`，书中还提供了如何将 `Debian` 设置为微型和 Web 服务器的描述。

DVD 和 CD 中包含的其他 Linux 发行版存储在可以放入 CD 的 ISO 镜像中，在某些情况下存储在微型 CD 或可启动的信片大小 CD 中（形状像名片，但可以通过大多数 CD 驱动器读取）。由于 DVD 空间限制，其中包含的一些发行版旨在网络安装，这意味着你需要连接互联网来获取某些软件以完成完整安装。

## 工作中的 Linux

由于我认识许多在非正式场合和工作中使用 Linux 的人，我想分享一下我对美国各地不同 Linux 发行版使用情况的印象。大多数搭建小型办公室服务器的顾问使用 `Red Hat Linux`，但现在大多已转向 `Fedora Core`、`Ubuntu` 或 `Debian GNU`/`Mandriva Linux`（原 Mandolinux，`Mandriva` 在想要获得友好的 Linux 桌面的人群中很受欢迎，`Fedora` 和 `SUSE` 也很受人们喜爱）。技术上更倾向的人更喜欢 `Gentoo`（高度可调）或 `Slackware`（基础形式）。

对于使用 Macintosh 硬件过渡到 Linux 的人员，`Yellow Dog` 让他们能够安装在 `PowerPC` 上，并学习有助于扩展到 `Red Hat Linux` 系统的技能（`Yellow Dog` 是基于 `Red Hat` 的）。至于那些可启动的 Linux，每个人认为它们都是尝试的绝佳选择，也是学习 Linux 的好方法。对于一个可以放入完整 CD（或 DVD）并包含桌面软件的可启动盘，`KNOPPIX` 是一个不错的选择；对于微型 CD 大小的可启动 Linux，`Damn Small Linux` 效果很好。

## 第 7 章 ✦ 安装 Linux

本书让你接触了几种不同的 Linux 发行版。这让你能够通过实际操作来看到每个发行版的优势和劣势。你还可以尝试加入不断增长的 Linux 用户社区，因为强大的社区支持意味着更稳健的软件发行版，并在你需要时提供帮助（通过论坛和在线聊天等方式）。

## 其他发行版

似乎每五分钟就会出一个新的 Linux 发行版，我真的必须在某个时候停止写这本书。为了将发行版的描述控制在合理范围内（并实际上有空间描述如何使用 Linux），书中没有探讨一些有趣的 Linux 发行版。

书中未包含的著名发行版包括 `TurboLinux`、`Lyoris` 和 `Xandros`。`TurboLinux` (`www.turbolinux.com`) 是亚太国家流行的发行版。`Lyoris`（最初基于 `Openlinux`）和 `Xandros`（设计用于在 Microsoft Windows 环境良好运行）都是备受认可的桌面 Linux 系统（分别参见 `www.lyoris.com` 和 `www.xandros.com`）。过去一年，`Lyoris` 被 `Mandriva` 收购，尽管它仍然作为独立产品提供。后续章节将解释如何跳出本书的限制去寻找这些其他的 Linux 发行版。

## 获取自己的 Linux 发行版

通过在书中封装了几种 Linux 发行版，我希望为你节省自己获取 Linux 的麻烦。如果你有 DVD 驱动器，也许你可以利用这个机会学习 `KNOPPIX`，以便更好地理解书中讨论。如果你有 CD 驱动器，直接从书中附带的 CD 启动到 `Damn Linux`。

如果由于某些原因无法使用 CD 或 DVD 上的软件，你可能想要获取自己的 Linux 发行版来配合书中的描述。你可能想要获取自己的发行版的原因包括：

- **没有 DVD 驱动器** —— 你电脑上需要可启动的 DVD 驱动器才能使用书中附带 DVD 上的 Linux 发行版。
- **后期的发行版** —— 你可能想要比书中更新的特定发行版版本。
- **完整的发行版** —— 因为 CD 和 DVD 空间有限，且某些发行版需要订阅或其他费用，你可能想要获取自己的更完整的发行版来工作。

今天，获取 Linux 的方法并不缺少。

## 寻找另一个 Linux 发行版

你可以去每个发行版的网站，例如 `http://fedora.redhat.com/download` 或 `http://slackware.com/getslack` 来获取 Linux 软件。这些网站通常允许你下载其发行版的副本（或示例），并提供购买盒装版的机会。

然而，获取可用 Linux 发行版完整视图的一种方法是访问专门提供 Linux 发行版信息的网站。使用这些站点连接论坛并下载关于许多发行版的文档。这里是一些例子：

- **下载目录** —— 你需要从下载目录向下进入几级目录，分别描述架构、发布和介质。
- **ISO 镜像** —— 你要刻录到 CD 的镜像通常以 ISO 格式存储。
- **MD5SUM** —— 为了验证获取的 CD 是否完好，下载后在 ISO 目录中寻找名为 `MD5SUM` 或以 `.md5` 结尾的文件。

# 248 第 III 部分 ♦ 选择与安装 Linux 发行版

由于某种原因，下载 `KNOPPIX` CD 镜像（从你想要下载的目录开始）的 `wget` 命令可能如下所示：

```
$ wget -c ftp.tux.org/pub/linux/knoppix/KNOPPIX_V4.0.2CD-2005-09-23-EN.iso
```
