
```
matthew@seymour:~$ sudo apt-get upgrade
Reading lists... Done
Building dependency tree
Reading state information... Done
The following packages will be upgraded:
cextract google-chrome-beta icedtea6-plugin language-pack-en
language-pack-en-base language-pack-gnome-en language-pack-gnome-base
libfreetype6-jre libfreetype6-dev libsmclient libsmclient0 openjdk-6-jre
openjdk-6-jre-headless openjdk-6-jre samba-common samba-common-bin
smbclient undoubt xserver xserver xorg-core

0 newly installed, 0 to remove and 0 upgraded.
Need to get 84.8MB of archives.

After this operation, 623KB of additional disk space will be used.
Do you want to continue (Y/n)?
```

## 报告解读

报告的每个部分都告诉你是重要的信息。从“the following packages will be upgraded”这一行开始，提供了待更新软件包的确列表。如果你正在安装新软件或删除软件，你会看到标题为“The following packages will be installed”和“The following packages will be removed”的列表。结尾的摘要显示 APT 将升级总共 21 个软件包，其中 0 个新包，0个待删除，0个已升级。这是一次升级而非安装新软件，所有新包仅占用 623KB 空间。尽管你有 84.8MB 的下载量，但软件包正在覆盖现有的文件。

理解这一点很重要：基本的 `apt-upgrade` 会移除软件或添加新软件。因此，保持系统完全补丁是安全的，因为它永远不会破坏东西。然而，你偶尔会看到“0 upgraded”状态发生变化，这意味着某些内容无法删除以满足更新后软件包的依赖关系；当某些软件必须安装或删除时（如前文所述），`apt-upgrade` 永远不会执行这种操作。

在这种情况下，你需要使用 `apt-get dist-upgrade`。之所以这样命名，是因为它设计用于允许用户从 Debian/Ubuntu 的一个版本升级到新版本——这种升级不可避免地涉及更改系统几乎所有内容、删除过时的软件并安装最新功能。这是 Debian 最受喜的功能之一，因为它让你能够在不同版本之间移动，而无需下载和安装新的 CD。保持定期的更新并让发行版保持分离，对于确保安全更新和简单的错误修复不会改变你可能依赖的软件配置非常有用，特别是对于像服务器这样需要持续可用且运行的机器。

虽然 `apt-get upgrade` 和 `apt-get dist-upgrade` 用于升级软件包，但 `apt-get install` 负责添加新软件。例如，如果你想安装 MySQL 数据库服务器，你可以运行：

```
matthew@seymour:~$ sudo apt-get install mysql-server
```

在内部，APT 在软件列表中查询“mysql-server”，并发现它匹配 `mysql-server-5.5` 软件包。然后它找到了它需要的、你尚未安装的依赖项，并为你提供类似下方的报告：

```
matthew@seymour:~ sudo apt-get install mysql-server
[sudo] password for matthew:
Reading package lists... Done
Building dependency tree
Reading state information... Done

The following extras will be installed:
libaiol-mysql-perl libdbi-perl libhtml-template-perl libmysqlclient18
libnet-daemon-perl libnprpc-perl libterm-readkey-perl mysql-client-5.5
mysql-client-core-5.5 mysql-server-5.5 mysql-server-core-5.5

Suggested packages:
libipc-shared-perl tiny macx

The following NEW packages will be installed:
libaiol-libdd-mysql-perl libdbi-perl libhtml-template-perl libmysqlclient18
libnet-daemon-perl libnprpc-perl libterm-readkey-perl mysql-client-5.5
mysql-client-core-5.5 mysql-server-5.5 mysql-server-core-5.5

0 upgraded, 13 installed, 0 to remove and 0 upgraded.
Need to get 84.8MB of archives.
After this operation, 623KB of additional disk space will be used.
Do you want to continue (Y/n)?
```

报告的每个部分都告诉你信息。从“the following packages will be upgraded”这一行开始，提供了待更新软件包的确列表。如果你正在安装新软件或删除软件，你会看到标题为“The following packages will be installed”和“The following packages will be removed”的列表。结尾的摘要显示 APT 将升级总共 21 个软件包，其中 0 个新包，0个待删除，0个已升级。这是一次升级而非安装新软件，所有新包仅占用 623KB 空间。尽管你有 84.8MB 的下载量，但软件包正在覆盖现有的文件。

理解这一点很重要：基本的 `apt-upgrade` 会移除软件或添加新软件。因此，保持系统完全补丁是安全的，因为它永远不会破坏东西。然而，你偶尔会看到“0 upgraded”状态发生变化，这意味着某些内容无法删除以满足更新后软件包的依赖关系；当某些软件必须安装或删除时（如前文所述），`apt-upgrade` 永远不会执行这种操作。

在这种情况下，你需要使用 `apt-get dist-upgrade`之所以这样命名，是因为它设计用于允许用户从 Debian/Ubuntu 的一个版本升级到新版本——这种升级不可避免地涉及更改系统几乎所有内容、删除过时的软件并安装最新功能。这是 Debian 最受喜的功能之一，因为它让你能够在不同版本之间移动，而无需下载和安装新的 CD。保持定期的更新并让发行版保持分离，对于确保安全更新和简单的错误修复不会改变你可能依赖的软件配置非常有用，特别是对于像服务器这样需要持续可用且运行的机器。

虽然 `apt-get upgrade` 和 `apt-get dist-upgrade` 用于升级软件包，但 `apt-get install` 负责添加新软件。例如，如果你想安装 MySQL 数据库服务器，你可以运行：

```
matthew@seymour:~$ sudo apt-get install mysql-server
```

在内部，APT 在软件列表中查询“mysql-server”，并发现它匹配 `mysql-server-5.5` 软件包。然后它找到了它需要的、你尚未安装的依赖项，并为你提供类似下方的报告：
