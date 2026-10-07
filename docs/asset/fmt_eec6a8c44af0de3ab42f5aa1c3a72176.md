
由于有可安装的软件，基于 Debian 的发行版提供了许多管理软件的方法。实际上，它们都使用 Debian 的高级软件包工具（APT）。Slashdot 上的一人曾说：“欢迎来到 Slashdot。如果你想不出新词，就说 APT 很酷，你就能融入其中。”

为什么 APT 很酷？嗯，它是第一个正确处理依赖关系的系统。其他发行版使用的文件具有依赖关系。例如，Red 使用具有依赖关系的 RPM 文件。GIMP 的 RPM 依赖于 GTK。结果是如果你在没有 GTK RPM 的情况下尝试安装 GIMP，你的安装将失败。所以，获取 GTK RPM 后再次尝试。

相比之下，APT 设计为能够自动查找并下载软件包的依赖关系。因此，如果你想安装 GIMP 软件包及其所需的任何其他软件，无需手动寻找，不再需要担心寻找正确的版本，更不需要手动完成。APT 还可以处理断点续传，这意味着如果你在升级过程中丢失网络连接（或者电量耗尽，或者你不得不退出），下次运行时 APT 将从停止的地方继续。

## 日常 APT 使用

为了让你能够快速彻底地搜索软件包，APT 使用可用软件包的本地缓存。尝试运行以下命令：

```
matthew@seymour:$ sudo apt update
```

`apt update` 命令指示 APT 联系它所配置的所有服务器并下载最新的文件更新列表。如果你的列表已过期，APT 需要一分钟左右下载更新。否则，该命令将在几秒钟执行完毕。

在下载最新的软件包信息后，你将返回命令行。现在你可以要求 APT 自动下载任何已更新的软件，使用此命令：

```
matthew@seymour:$ sudo apt upgrade
```

如果你在机器上安装了许多软件，那么软件更新的可能性就会更大。APT 会扫描你的软件，并将其与服务器上的最新包信息进行对比，生成类似下方的报告：

```
matthew@semour:-$ sudo apt upgrade
Reading lists... Done
Building dependency tree
Reading state information... Done
The following packages will be upgraded:
abstract google-chrome-beta cedtea-6-plugin language-pack-en
language-pack-en-base language-pack-gnome-en language-pack-gnome-en-base
freetypes libfreetype6-dev libsmclient libwbclient0 openjdk-6-jre
openjdk-6-jre-headless openjdk-6-jre-lib samba-common samba-bin
smbclient update winbind xserver-common xserver-xorg-core
21 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
```

执行此操作后，将使用 623KB 的额外磁盘空间。

你想要继续吗 [Y/n]？

此报告的每个部分都传了重要信息。从顶部开始，“The following packages will be upgraded”这一行给出了可用更新的包列表。如果你正在安装新软件或删除软件，会出现某些标题为“The following packages will be installed”和“The following packages will be removed”的列表。底部的摘要显示 APT 将总共升级 21 个包，其中 0 个新包，0 个待删除和 0 个未升级。这是因为是升级而不是安装新软件，所有新包仅占了 623KB 的额外空间。尽管你有 84.8MB 的下载量，但这些包正在覆盖旧文件。

重要的一点是，基本的 `apt upgrade` 永远不会移除软件或添加新软件。使用此命令来保持系统完全补丁状态是安全的，因为它永远不会弄坏任何东西。然而，你偶尔会看到“0 not upgraded”状态，这意味着某些内容无法升级。当必须安装某些软件以满足更新包的依赖关系时，就会发生这种情况，正如之前提到的，`apt upgrade` 永远不会这样做。在这种情况下，你需要使用 `apt dist-upgrade`，它的名字是因为它旨在允许用户从 Debian/Ubuntu 的版本升级到新版本——这种升级不可避免地涉及系统上几乎所有内容的更改，移除 Debian 过时的功能，因为它允许你在无需下载和安装新 CD 的情况下从一个版本移动到另一个版本。保持定期更新和发行升级对于确保安全更新和简单的错误修复不会改变你可能依赖的配置非常有用，特别是对于那些需要持续可用和运行的机器，例如服务器。

虽然 `apt upgrade` 和 `apt dist-upgrade` 用于升级包，但 `apt install` 负责添加新软件。例如，如果你想安装 MySQL 数据库服务器，请运行此命令：

```
matthew@semour:-$ sudo apt install mysql-server
```

### 在命令行中操作

在内部，APT 在其软件列表中查询 `mysql-server`，并发现它与 `mysql-server-5.7` 包匹配。然后它找到了它需要的但你尚未安装的依赖项，并给你提供如下的报告：

```
matthew@semour~$ sudo apt install mysql-server
[sudo] password for matthew:
```

Reading package lists... Done

Building dependency tree

Reading state information... Done

The extra packages will be installed:

libibaevent-core-2.1.6 libhtml-template-perl mysql-client-5.7

mysql-client-core-5.7 mysql-common mysql-server mysql-server-5.7

mysql-server-core-5.7

Suggested packages:

libipc-sharedache-perl tinyyca mailx

The NEW packages will be installed:

libibaevent-core-2.1.6 libhtml-template-perl mysql-client-5.7

mysql-client-core-5.7 mysql-common mysql-server mysql-server-5.7

mysql-server-core-5.7

0 upgraded, 9 newly installed, to remove and 0 not upgraded.

Need to get 20.3 MB of archives.

After this operation, 160 MB of additional disk space will be used. Do you want to continue [Y/n]?
```

这一次，你可以看到 APT 已经挑选并选定了安装 MySQL Server 5.7 所需的所有依赖项，但它也列出了推荐的包和两个它没有选择安装的建议包。`recommended` 包仅仅是如此：制作该包的人（或其依赖项）认为你同时也拥有 `mailx` 包是一个明智的主意。如果你想添加它，按 `n` 终止 apt 并按如下方式重新运行：

```
matthew@semour~$ sudo apt install mysql-server mailx
```

`Suggested` 包仅仅是推荐的更低级的形式。它们不会向你想要安装的软件添加任何关键功能，但你可能在正在安装的主软件时需要它们。

APT 维护一个包缓存，其中存储它已下载并安装的 DEB 文件。这通常位于 `/var/cache/apt/archives`，有时会占用数百兆字节的空间。你可以通过运行 `apt clean` 来清理包缓存，它会删除所有缓存的 DEB 文件。或者，你可以运行 `apt autoclean`，它会删除超过某些时间的缓存 DEB 文件并保留较新的包。

对于你已经安装的包运行 `apt install` 时，APT 会考虑你的命令并查找是否有新版本可下载。另一个重要的日常操作是移除不再需要的东西，你通过如下方式使用 `apt remove` 命令来实现：

```
matthew@semour:-$ apt remove
```
