
在你安装了 `CentOS 7.*` `Everything` 发行版后，你应该更新软件包。通过使用安装时设置的密码登录 `root` 账户并执行命令来实现。你需要了解哪些发行版本有助于通过考试。

## 查看 CentOS

社区企业操作系统 (`CentOS`) 自 2004 年以来一直存在。它几乎是 `RHEL` 的精确复制。虽然获取 `RHEL` 需要向红帽订阅，但 `CentOS` 是免费的，是一个很好的学习资源。

你可以在 `CentOS` 网站 `www.centos.org` 获取 `CentOS` 发行版 `ISO`。注意，该发行版与其他一样有多种口味。我们建议你获取 `CentOS 7.*` `Everything` `ISO`。

![](img/0c1e7d2699b9d354c8d2f84669d18d73_64_0.png)

随着时间的推移，会有新的 `CentOS` 发行版可用。虽然总是倾向于获取最新的版本，但在你的学习空间中使用它并没有益处。在你进入了 `CentOS 7.*` `Everything` 发行版后，你需要了解。

请注意，默认情况下 `CentOS 7.*` `Everything` 发行版不会安装图形用户界面 (`GUI`)。尽管 `CentOS` 发行版的名称是 `Everything`，但它是被安装为最小服务器的。如果你希望在该发行版中安装 `GUI`，请以 `root` 登录并执行列表 1.2 所示的命令。

### 列表 1.2：在 CentOS 上安装 GUI

```bash
# yum groupinstall "GNOME Desktop" "Graphical Administration Tools"

[...
Total download size: 727 M
Installed size: 2.3 G
Is this ok [y/d/N]: y
Downloading packages
[...
Complete!
# ln -sf /lib/systemd/system/runlevel5.target /etc/systemd/system/default.target
# reboot
```

> 如果你之前没有使用过 `CentOS` 发行版或对 `Linux` 经验有限，建议在尝试安装 `GUI` 之前阅读本章的所有内容。然而，不要让这阻碍你。如果你想尝试一下，尽管去吧。有时尝试、跌倒和再次尝试会带来极佳的学习体验。

虽然 `CentOS` 是红帽营中广流行的发行版，但你还需要一个来自 `Debian` 营的发行版。接下来，我们将探索 `Ubuntu` 发行版。

## 查看 Ubuntu

`Ubuntu Linux` 发行版由 `Canonical LTD` 管理，自 2004 年以来一直存在。这个免费且流行的 `Linux` 发行版基于 `Debian` 发行版，是你个人 `Linux` 学习空间中必不可少的。

你可以从 `www.ubuntu.com` 获取 `Ubuntu` 发行版 `ISO`。`Ubuntu` 有多个版本（flavors），我们推荐下载 `Ubuntu` 桌面版 `18.04 LTS`。

> `Ubuntu` 版本中的 `LTS` 代表长期支持（`Long Term Support`）。这是 `Canonical` 使用的指标，表示它将在更长的时间内提供维护和安全更新。对于 `18.04 LTS`，你可以依靠这些更新将持续到 2023 年 4 月。

如果你不熟悉 `Ubuntu`，需要注意几项重要事项。默认情况下，你无法登录 `root` 账户。相反，当你需要使用超级用户权限时，登录你在安装时设置的账户，并在命令行前加上 `sudo` 命令。示例如列表 1.3 所示。

### 列表 1.3：在 Ubuntu 上使用 sudo

```bash
$ sudo grep root /etc/shadow
root:l:17737:0:99999:7:::
$
```

> 注意：如果你从未在终端中执行过命令行命令，建议在尝试之前阅读整个章节。你将在本章的稍后部分阅读更多关于终端的内容。

另一个重要事项涉及安装 `Ubuntu`。如果你连接了网络，可以在安装发行版时自动更新发行版的软件。你会在安装过程中看到此选项，即“安装期间下载更新”（`Download updates during the installation`），旁边带有一个复选框。通常建议不要选择此选项。相反，你可以在成功安装后更新软件。要通过命令行更新软件，请在终端中使用超级用户权限手动执行列表 1.4 所示的命令。

### 列表 1.4：在 Ubuntu 上更新软件

```bash
$ sudo apt-get update
[sudo] password for Christine:
Hit:1 http://us.archive.ubuntu.com/ubuntu bionic InRelease
Get:2 http://us.archive.ubuntu.com/ubuntu bionic-updates InRelease [88.7 kB]
[...
Fetched 1,053 kB in 2s (631 kB/s)
Reading package lists... Done
$ sudo apt-get dist-upgrade
Reading package lists... Done
Building dependency tree
Reading state information... Done
Calculating upgrade... Done
The following packages will be upgraded:
[...
Do you want to continue? [Y/n] V
[...
$
```

如果你空间只够容纳两个 `Linux` 发行版，`CentOS` 和 `Ubuntu` 是很棒的选择。如果你有额外的资源，添加另一个发行版 `openSUSE` 是值得的。

## 查看 openSUSE

`openSUSE` 发行版于 1994 年首次发布，当时名为另一个名称 `SUSE Linux`。有许多公司参与了它的支持，其中总部位于德国的 `SUSE` 公司是原始公司。

这个发行版拥有非常忠实且稳固的基础。`openSUSE` 发行版不仅受到社区开发者的强支持，`openSUSE` 用户也非常喜爱它。它独特且流行的工具之一是 `Yet another Setup Tool`（另一个设置工具，简称 `YaST`）。`YaST` 可以被看作一个控制中心工具，允许你从一个界面控制许多系统服务。

你可以从 `https://software.opensuse.org` 获取 `openSUSE` 发行版 `ISO`。该发行版有两个主要版本：`Leap` 和 `Tumbleweed`。我们推荐你选择 `openSUSE Leap 15.*` 版本。

> `openSUSE` 社区在 2017 年更改了其发行版的版本命名方案。15.0 之前的版本是 `42.3`。在获取 `openSUSE Leap` 时，请注意这一剧烈变化。

一旦你成功安装了 `openSUSE`，在探索此发行版之前更新所有软件是一个好主意。要通过命令行更新软件，请在终端中使用超级用户权限手动执行列表 1.5 所示的命令。

### 列表 1.5：在 openSUSE 上更新软件

```bash
$ sudo zypper patch
[sudo] password for root:
Loading repository data...
Reading installed packages...
Resolving package dependencies...
[...
Note: System reboot required.
Continue? [y/n]... shows all options] (y): y
[...
Warning: One of the installed patches requires a reboot of your machine. Reboot as soon as possible.
There are some running programs that might use files deleted by recent upgrade. You may wish to check and start some of them. Run 'zypper ps'
```
