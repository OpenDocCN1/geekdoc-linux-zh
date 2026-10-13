
网络，或设置安全性。在第17章中，我将介绍 YaST 控制中心，以及你可以通过控制中心执行的各种系统管理任务。

如果你在文本控制台，你仍然可以使用 YaST——通过其命令行。例如，要从命令行安装一个 RPM，请键入 **/sbin/yast -i**，后面跟上 RPM 包的名称。

![](img/b7e91b81e0d84c8a5261ee14a48991b2_340_0.png)

YaST 曾经是专有软件，但在 2004 年，Novell 在 GNU 通用公共许可证（GPL）下发布了 YaST——与 Linux 本身所使用的开源许可证相同。

## 检测所有硬件（嗯，几乎全部！）

SUSE Linux 最好的地方之一就是它能在安装和设置期间检测到几乎所有的硬件。对于所有检测到的硬件，SUSE Linux 会加载访问该硬件所需的任何驱动程序，并处理所有配置步骤，例如在 `/etc/fstab` 配置文件中添加条目，以及在 `/media` 目录中创建可用于挂载存储设备的子目录。出色的硬件检测意味着你通常可以在大多数 PC 上顺利安装 SUSE Linux，而不会遇到任何麻烦。

如果在安装 SUSE Linux 之后添加了硬件，你可以将硬件连接到 PC，打开电源，然后从 YaST 控制中心运行相应的硬件配置模块（有关 YaST 控制中心的更多信息，请参见第17章）。

## 顺畅而简单的安装

SUSE Linux 的安装既不过度简化，也不无谓地复杂——恰到好处。凭借其硬件检测能力和 YaST 图形界面工具，普通用户也能轻松完成 SUSE Linux 的安装。安装程序甚至让诸如调整硬盘上 Windows 分区大小以便为 SUSE Linux 腾出空间这样可能很复杂的步骤也变得简单。你只需指定 Windows 分区的大小，安装程序便会负责缩小该分区的尺寸。

安装程序不是引导用户逐个浏览一系列固定的安装屏幕，而是将所有选项呈现在一个屏幕中。然后，你只需更改需要更改的项目，例如时区，也许还有 KDE 或 GNOME 桌面之间的软件选择。安装程序会在安装最小系统并重新启动后处理所有其他配置。总而言之，SUSE Linux 的安装顺畅而简单。

## 我爱 YOU——YaST 在线更新

YaST 在线更新，简称 YOU，让你可以轻松保持 SUSE Linux 系统更新。你只需要一条高速互联网连接。然后，你就可以从你选择的在线服务器下载最新的软件更新。你可以将其设置为自动下载并安装更新，也可以只下载，然后手动安装更新。我将在第18章中介绍 YOU。

## 自动挂载我的 Windows 分区和 USB 记忆棒

如果你有 Windows 分区，SUSE Linux 会自动挂载它们，这样你就可以轻松访问 Windows 分区中的文件。例如，在 Windows XP/SUSE Linux 双启动系统中，你可能会发现 Windows XP 分区挂载在 Linux 文件系统中的 /windows 目录下。如果由于某种原因 Linux 没有自动挂载 Windows XP 分区，你可以键入 su - 成为 root，然后键入 mount /dev/hda2 /windows 来挂载它，因为 Windows XP 分区通常是硬盘上的第二个分区（当然，这仅适用于你的 PC 安装了 Windows XP 的情况）。

当你将 USB 记忆棒插入 USB 端口时，SUSE Linux 会检测到它并将其挂载到 /media 目录下的一个子目录中。插入后，你可以通过单击桌面上的“我的电脑”图标，再单击标记为 /dev/sda1 的硬盘图标来访问 USB 记忆棒——这是分配给 USB 记忆棒的设备名称。

## KDE 桌面自动登录

自动登录 KDE 桌面不利于安全，但当你的 SUSE Linux 系统处于安全环境（例如家中）时，这很方便。启动系统后，SUSE Linux 会自动将你登录，你可以直接从 KDE 桌面开始使用。

顺便说一下，如果你在办公室和其他人在一起，并想关闭此功能，请从 KDE 桌面选择主菜单➜控制中心。然后选择系统管理➜登录管理器。单击“管理员模式”并输入 root 密码。接着单击“便捷”选项卡，并单击以关闭“启用自动登录”复选框。

## 对笔记本电脑的良好支持

SUSE Linux 持续改进一些对笔记本电脑用户很重要的功能。当你的笔记本电脑使用电池运行时，你会希望在空闲时关闭系统的各个部件来节省电量。SUSE Linux 可以通过其对 ACPI（高级配置与电源接口）的支持来实现这一点。你可以通过面板上的一个图标（看起来像电源插头的那个图标）访问电源管理模块。在这个模块的菜单中，你可以查看剩余电池电量，并将系统挂起到磁盘，以便稍后恢复，而无需经历长时间的系统重启。

## 轻松浏览 Windows 共享

在 SUSE Linux 系统的 KDE 桌面上单击“网络浏览”，网络浏览器会自动检测并显示你局域网中的 Windows 工作组。然后，你可以通过单击某个工作组，再单击特定 Windows PC 的图标来浏览共享文件夹。你可以轻松地将文档从 Windows 共享复制到你的 SUSE Linux 系统，或使用 OpenOffice.org Writer 等 Linux 软件打开它们。

## 那个可爱的壁虎吉祥物

你懂我的意思。看一下 KDE 或 GNOME 桌面（或访问 `www.suse.com`），你就能看到这只可爱的壁虎吉祥物，它已经成为 SUSE Linux 在世界范围内的象征。好在 Novell 收购 SUSE 之后没有对吉祥物做任何改动。你一定会同意——这是一个可爱的吉祥物。

## SUSE 日益增长的人气

难道你不喜欢成为潮流的一部分吗？我喜欢。SUSE 正在崛起，我们可以乘势而上——至少，在浪潮持续期间。SUSE Linux 在欧洲已经广受欢迎，并且还在不断改进。随着 Novell 收购德国 SUSE Linux AG 以及 openSUSE 项目（`www.opensuse.org`）的创立，SUSE Linux 的前景蒸蒸日上。openSUSE 是一个由 Novell 赞助的开源项目，开发者、最终用户和其他开源爱好者社区可以参与其中，并继续推动 SUSE Linux 的发展。所有这些最新发展都在 SUSE Linux 周围产生了明显的“热潮”，使其成为从家庭用户到企业服务器都适用的新兴 Linux 发行版。而美妙之处在于，你和我——我们——都是为 SUSE 的人气做出贡献的群体中的一员。

## 第22章：SUSE 狂热者的十大精彩网站

### 本章内容

- www.suse.com
- portal.suse.com/sdb/en/index.html
- distrowatch.com/table.php?distribution=suse
- www.suseforums.net
- www.linuxquestions.org/questions/f60
- www.linuxforums.org/forum/forum-36.html
- www.linux-laptop.net/
- packman.links2linux.org
- www.tldp.org/
- www.linuxhq.com/guides/

在这个互联网时代，当我们几乎需要任何信息时，我们都会求助于网站。对于 SUSE 狂热者——我们这些总是想找到有关 SUSE Linux 及相关内容的最新新闻和信息的人——网上有足够多的网站来满足每个人的信息需求。在所有可用的 SUSE 和 Linux 相关网站中，我精选了十个我认为对 SUSE Linux 用户最有用的网站。我将在本章中介绍这十个网站。

### http://www.opensuse.org

对于任何与 SUSE Linux 相关的内容，你都必须从这里开始——这是 SUSE Linux 的官方网站。你可以浏览此网站获取 SUSE Linux 的最新新闻、openSUSE 项目里程碑，报告 bug，并下载 SUSE Linux。

### http://portal.suse.com/sdb/en/index.html

这是 SUSE 门户的英文页面。如果你想使用其他语言（如德语、法语或西班牙语）的站点，请单击页面顶部的相应链接。

SUSE 门户使你可以访问 SUSE 支持数据库（简称 SDB）。你可以按关键字搜索 SDB，或按类别浏览数据库。这里有一个指向 SUSE 主 FTP 服务器（`ftp.suse.com/pub`）的链接，以及一个镜像站点列表，你可以从中下载 SUSE Linux。

通过 SUSE 门户，你还可以访问和搜索 SUSE Linux 硬件数据库，查看有关 SUSE Linux 对特定硬件设备（如显卡、网卡、打印机、调制解调器等）支持程度的信息。

### http://distrowatch.com/table.php?distribution=suse

该网页提供有关最新 SUSE Linux 发行版的摘要信息，以及许多指向有关 SUSE 的新闻、评论、论坛和文档的链接。通过此网站上的链接，你还可以以相当低的成本购买 CD 和 DVD 版 SUSE Linux（如果你没有高速互联网接入，并且无法轻松下载庞大的 ISO 文件，这会很方便）。

### http://www.suseforums.net

这是一个面向 SUSE Linux 的在线论坛。你可以免费注册为用户，然后发布问题，或在论坛中搜索以前发布的问题和答案。你也可以不注册直接浏览论坛。

### http://www.linuxquestions.org/questions/f60

LinuxQuestions.org 设有多个关于 Linux 的论坛，其中包括一个 SUSE Linux 论坛。我给出的这个 URL 可以直接带你进入 SUSE Linux 论坛。
