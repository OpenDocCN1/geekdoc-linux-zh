
`matthew@semour:~$ apt update`

`update` 命令指示 APT 联系所有已配置的服务器并下载最新的文件列表。如果你的列表已过期，APT 需要一到几钟来下载更新。否则，此命令在几秒钟内即可执行。

在下载最新信息后，你将返回命令行。现在你可以要求 APT自动下载任何已更新的软件，使用此命令：

```
matthew@semour:~$ apt upgrade
```

## 第 9 章 管理软件

如果你在机器上安装了许多软件，那么软件更新的可能性就会更大。APT 会扫描你的软件并与服务器上的最新软件包信息进行对比，生成类似如下报告：

```bash
matthew@seymour:~$ sudo apt upgrade
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following packages will be upgraded:
cabstract google-chrome-beta icedtea6-plugin language-pack-en
language-pack-en-base language-pack-gnome-en language-gnome-base
libfreetypes2-dev libmclient libwbclient0 openjdk-6-jre
openjdk-6-jre-headless openjdk-6-jre-lib samba-common samba-bin
smbclient update windbind xserver-common xserver-xorg-core
21 upgraded, 0 newly installed, 0 to remove and 0 not upgraded. Need to get 84.8MB of archives.
```

在此操作之后，将额外使用 623KB 的磁盘空间。你确定要继续吗 [Y/n]？

此报告的每个部分都告诉你某些重要信息。在顶部，“The following packages will be upgraded”（将升级以下软件包）这一行提供了可用更新的精确列表。如果你正在安装新软件或删除软件，你会看到名为“Following packages will be installed”（将安装以下软件包）和“Following packages will be removed”（将移除以下软件包）的列表。底部的摘要显示 APT 将共升级 21 个软件包，0 个新软件包，0 个待删除，0 个未升级。这是因为升级而非安装新软件，因此新软件包仅占用额外的 623KB 空间。尽管下载了 84.8MB 的数据，但软件包正在覆盖现有文件。

需要理解的是基本的 `apt upgrade` 永远不会移除或添加软件。因此，使用此命令来保持系统完全补丁是安全的，因为它永远不会破坏系统。然而，偶尔你会看到“0 not upgraded”（0 未升级）状态发生变化，这意味着某些内容无法升级。这发生在必须安装或删除某些软件以满足更新软件包的依赖关系时（如前所述，`apt upgrade` 永远不会这样做）。在这种情况下，你需要使用 `apt dist-upgrade`，它之所以叫这个名字是因为它设计用于允许用户从 Debian/Ubuntu 的一个版本升级到新版本——这种升级不可避免地涉及系统中几乎所有内容，移除 Debian 的过时功能并安装最新功能。这是无需下载和安装新 CD 即可跨版本迁移的最强大的功能之一。保持定期升级和发行版升级（distro upgrades）对于确保安全更新和修复你可能依赖的简单 bug 非常有用，特别是对于那类需要持续可用且正常运行的机器（例如服务器）。

虽然 `apt upgrade` 和 `apt dist-upgrade` 用于升级软件包，但 `apt install` 负责添加新软件。例如，如果你想安装 MySQL 数据库服务器，运行以下命令：

```bash
matthew@seymour:~$ sudo apt install mysql-server
```

### 在命令行上操作

在内部，APT 在其软件列表中查询 `mysql-server`，并发现它匹配 `mysql-server-5.7` 软件包。它找到了你尚未安装的所需的依赖项，并给你提供如下报告：

```bash
$ matthew@seymour:~$ sudo apt install mysql-server
[sudo] password for matthew:
Reading package lists... Done
Building dependency tree
Reading state information... Done
The extra packages will be installed:
libaiboverent-core-2.1.6 libhtml-template-perl mysql-client-5.7
mysql-client-core-5.7 mysql-common mysql-server mysql-server-5.7
mysql-server-core-5.7
Suggested packages:
libpc-sharedcache-perl tinyca mailx
The following NEW packages will be installed:
libaiboverent-core-2.1.6 libhtml-template-perl mysql-client-5.7
mysql-client-core-5.7 mysql-common mysql-server mysql-server-5.7
mysql-server-core-5.7
0 upgraded, 9 newly installed, 0 remove and 0 not upgraded.
Need to get 20.3 MB of archives.
After this position, 160 MB of additional disk space will be used. Do you want to continue [Y/n]:
```

这次，我们可以看到 APT 挑选并选择了安装 MySQL Server 5.7 需要的所有依赖项，但它也列出了一个没有选择安装的推荐软件包（recommended）和两个建议软件包（suggested）。“推荐”软件包仅仅是如此：制作 MySQL 软件包（或其依赖项）的人认为你同时也拥有 `mailx` 软件包是一个明智的主意。如果你想添加它，按 `n` 终止 apt 并按如下方式重新运行：

```bash
$ matthew@seymour:~$ sudo apt install mysql-server mailx
```

“建议”软件包仅仅是推荐的较低程度的形式。它们不会为你选择的软件提供任何关键重要的功能，但你可能在某些关键（正在安装软件的主体）功能或任务中需要它们。

APT 维护一个软件包缓存，其中存储了它已下载并安装的 DEB 文件。这通常位于 `/var/cache/apt/archives`，有时会占用你计算机上几百 MB 的空间。你可以通过运行 `apt clean` 来清理软件包缓存，它会删除所有缓存的 DEB 文件。或者，你可以运行 `apt autoclean`。

#### 查找软件

由于有许多软件包可用，可能很难找到你确切需要的。`apt-cache` 工具用于此操作：

```bash
matthew@seymour:~$ apt-cache search
```

根据你拥有的存储库，该工具返回约 1000 个软件包。你可以通过几种方式过滤这些信息。首先，你可以使用 `-n` 参数指示 `apt-cache` 仅搜索名称，而不是描述：

```bash
matthew@seymour:~$ apt-cache -n search kde
```

另一种限制结果的方法是使用某些正则表达式，例如 `^` 表示“开始”，`$` 表示“结束”。例如，你可能想搜索以 kde 开头的程序，如下：

```bash
matthew@seymour:~$ apt-cache -n search ^kde
```

也许寻找软件包的方法是将 `apt-cache` 与 `grep` 结合起来对结果进行搜索。例如，如果你想找到所有与 kde 相关的软件包，可以运行：

```bash
matthew@seymour:~$ apt-cache search | grep kde
```

当你找到了想要安装的软件包后，照常通过 `apt install` 运行。如果你想先获取该软件包的更多信息，可以使用 `apt-cache showpkg`，如下：

```bash
matthew@seymour:~$ apt-cache showpkg mysql-server-5.7
```
