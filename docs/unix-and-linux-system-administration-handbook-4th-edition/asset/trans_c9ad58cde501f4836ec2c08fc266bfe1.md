

控制分离从行政角度来看很有趣，但它并不影响软件包分发系统，除非它们可能需要由管理员手动添加。

## RHN：Red Hat Network

随着 Red Hat 优雅地退出消费级 Linux 业务，Red Hat Network 已成为 Red Hat Enterprise Linux 的系统管理平台。你通过订阅购买访问 Red Hat Network 的权利。最简单地说，你可以将 Red Hat Network 用作一个功能强大的网络门户和邮件列表。以这种方式使用时，Red Hat Network 与多年来由各种 UNIX 厂商运行的补丁通知邮件列表并没有太大区别。但如果你愿意为此付费，还可以使用更多功能。有关当前价格和功能，请参阅 rhn.redhat.com。

Red Hat Network 提供基于 Web 的界面用于下载新软件包，以及命令行替代方案。从 Red Hat Enterprise 5 开始，CLI 工具是 yum；在那之前它是笨拙、易引发依赖问题的工具 up2date。yum 甚至能让你在无需人工干预的情况下下载和安装新软件包。一旦注册，你的机器就会自动获取所需的所有补丁和错误修复，而无需你 ever 干预。

自动注册的缺点是 Red Hat 决定你需要哪些更新。你可能会考虑你到底有多信任 Red Hat（以及他们打包的软件维护者）不会搞砸事情。鉴于 Red Hat 过去在一些小事上，比如要发布哪个编译器，所做的一些有趣选择，有些人可能会保持怀疑态度。

一个合理的折中方案可能是为你组织中的一台机器注册自动更新。你可以定期从该机器拍摄快照，以测试作为内部发布的候选版本。

## APT：高级打包工具

APT 是最成熟的软件包管理系统之一。只需一条 apt-get 命令，甚至可以像 Red Hat Network 一样，让你的机器在无需人工干预的情况下持续保持最新状态，就能升级整个系统中的所有软件。

在 Ubuntu 系统上使用 apt-get 的第一条规则（事实上管理所有 Debian 软件包也一样）是忽略 dselect 的存在，它充当 Debian 软件包系统的前端。它并不是一个坏主意，但用户界面很差，对新手用户来说可能令人望而生畏。一些文档会试图引导你使用 dselect，但要坚强，坚持使用 APT。

如果你使用 apt-get 管理来自标准镜像的库存 Ubuntu 安装，最简单的方法是访问 packages.ubuntu.com 上的主列表查看可用软件包。该网站包含一个不错的搜索界面。如果你设置了自己的 apt-get 服务器（参见第 390 页），那么当然你会知道自己提供了哪些软件包，并且可以按你想要的方式列出它们。

发行版通常包含仅用于声明其他软件包作为先决条件的虚拟软件包。apt-get 会在需要时下载和升级先决条件软件包，因此虚拟软件包使得可以作为一个整体安装或升级多个软件包变得容易。例如，安装 gnome-desktop-environment 软件包会获取并安装运行 GNOME UI 所需的所有软件包。

一旦你设置了 /etc/apt/sources.list 文件（下面详细介绍）并知道你想要的软件包的名称，剩下的唯一任务就是以特权用户身份运行 apt-get update 以刷新 apt-get 的软件包信息缓存。之后，只需以特权用户身份运行 apt-get install package-name 即可安装软件包。同一命令也会更新已安装的软件包。

假设我们想安装一个修复安全漏洞的 sudo 软件包新版本。首先，总是明智的做法是执行 apt-get update：

```
ubuntu$ sudo apt-get update
Get:1 http://http.us.debian.org stable/main Packages [824kB]
Get:2 http://non-us.debian.org stable/non-US/main Release [102B]
...
```

现在我们可以实际获取该软件包了。请注意，我们在获取新的 sudo 软件包时正在使用 sudo——apt-get 甚至可以升级正在使用的软件包！

```
ubuntu$ sudo apt-get install sudo
Reading Package Lists... Done
Building Dependency Tree... Done
1 packages upgraded, 0 newly installed, 0 to remove and 191 not upgraded.
Need to get 0B/122kB of archives. After unpacking 131kB will be used.
(Reading database ... 24359 files and directories currently installed.)
Preparing to replace sudo 1.6.1-1 (using .../sudo_1.6.9p10-1ubuntu3.4_i386.deb)
...
Unpacking replacement sudo ...
Setting up sudo (1.6.2p2-2) ...
Installing new version of config file /etc/pam.d/sudo ...
```

### apt-get 配置

配置 apt-get 很简单；你需要知道的几乎所有内容都可以在 Ubuntu 社区关于软件包管理的文档中找到：

help.ubuntu.com/community/AptGet/Howto

最重要的 apt-get 配置文件是 /etc/apt/sources.list，它告诉 apt-get 从哪里获取软件包。每行指定以下内容：

- 一种软件包类型，目前为 Debian 风格软件包的 deb 或 deb-src，或 RPM 的 rpm 或 rpm-src
- 一个指向文件、CD-ROM、HTTP 服务器或 FTP 服务器的 URL，用于获取软件包

