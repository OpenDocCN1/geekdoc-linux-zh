
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
libipc-sharedcache-perl tiny macx

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

与 KDE 仍然符合我们的搜索结果（例如 `kdebase`）。通过搜索名称以 `kde` 开头的包来实现，方法如下：

```bash
$ matthew@seymour:$ apt-cache -n search kde
```

找到包最简单的方法是将 `apt-cache` 与 `grep` 结合，在搜索结果中进行搜索。例如，如果你想找到所有与 KDE 相关的包，可以运行此搜索：

```bash
$ matthew@seymour:$ apt-cache search games | grep kde
```

当你找到了想要安装的包后，像往常一样运行 `apt-get install`。如果你想先获取更多关于该包的信息，可以使用 `apt-cache showpkg`，如下所示：

```bash
$ matthew@seymour:$ apt-cache showpkg mysql-server-5.0
```

这显示了关于“反向依赖”（哪些包需要、推荐或建议）“依赖”（哪些包被需要、推荐或建议安装 `mysql-server-5.0`）以及“提供”（软件包为你提供了哪些功能）。“提供”列表非常强大，因为它允许不同的包提供某种资源。例如，一个 MySQL 数据库程序要求安装 MySQL，但当你安装 MySQL 4.1 或 MySQL 5.5 时它并不挑剔。在这种情况下，MySQL 4.1 和 MySQL 5.0 的 Debian 包在“提供”列表中都包含 "`mysql-server-4.1`"，意味着它们提供了由 MySQL 4.1 提供的功能。因此，你可以安装任何一个版本来满足基于 MySQL 的应用程序。

## 从源码编译软件

从源码编译应用程序并不困难。有两种方法可以实现：你可以使用 Ubuntu 存储库中提供的源代码，或者使用上游开发者提供的源代码（对于在 Ubuntu 存储库中不可用的项目，这种方法最有用）。对于哪种方法，你都需要安装 `build-essential` 软件包以确保你拥有编译所需的工具。你可能还需要安装 `automake` 和 `checkinstall`，它们是构建工具。

## 从 Tarball 编译

大多数不在 Ubuntu 存储库中的源代码都可以从原始作者或公司网站以压缩源码 tarball 的形式获取——即使用 `zip` 或 `bzip` 压缩的 `tar` 文件。这些压缩文件通常会解压成包含若干个文件的目录。作为普通用户编译源代码始终是一个好主意，以限制损坏或恶意代码可能造成的任何伤害，请在你的家目录下创建一个名为 `source` 的目录。

从你下载源码 tarball 的地方，使用 `tar` 的 `-C` 选项将其解压到 `/source` 目录：

```bash
matthew@seymour:-$ tar xvf packageName.tgz -C /source
matthew@seymour:-$ tar xvf packageName.tar.gz -C /source
matthew@seymour:-$ tar jxf packageName.bz -C /source
matthew@seymour:-$ tar xvf packageName.tar.bz2 -C /source
```

如果你不确定使用了什么文件压缩方法，可以使用 `file` 命令判断：

```bash
matthew@seymour:-$ file packageName
```

现在，切换目录到 `/source/packageName` 并寻找名为 `README`、`INSTALL` 或类似名称的文件。如有必要请打印该文件，因为它包含了如何编译和安装软件的具体指令。编译源码的步骤如下：

```bash
matthew@seymour:-~/source/packageName$ ./configure
```

这将运行一个脚本来检查是否满足了所有依赖条件以及构建环境是否正确。如果你缺少依赖，`configure` 脚本通常会准确告诉你它需要哪些。如果你在 Synaptic 中启用了 `Universe` 和 `Multiverse` 存储库，很有可能在里面找到缺失的软件（通常是库）。

当你的 `configure` 脚本成功后，运行以下命令编译软件：

```bash
matthew@seymour:-~/source/packageName$ make
```

最后，运行以下命令：

```bash
matthew@seymour:-~/source/packageName$ sudo make install
```

如果编译失败，检查错误信息查找原因，并在重新开始之前运行以下命令：

```bash
matthew@seymour:-~/source/packageName$ make clean
```

如果你不喜欢该软件，也可以运行以下命令将其卸载：

```bash
matthew@seymour:-~/source/packageName$ sudo make uninstall
```
