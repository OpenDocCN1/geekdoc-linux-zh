
以下额外软件包将被安装：
libdbd-mysql-perl libdbi-perl libnet-daemon-perl libplrpc-perl
mysql-client-5.0 mysql-server-5.0
建议安装的软件包：
dbishell libcompress-zlib-perl
推荐安装的软件包：
mailx

将安装以下新的软件包：
libdbd-mysql-perl libdbi-perl libnet-daemon-perl libplrpc-perl
mysql-client-5.0 mysql-server-5.0
已升级 0 个，新安装 7 个，要卸载 0 个，有 1 个未升级。
需要下载 28.5MB 的归档文件。
解压后将额外占用 65.0MB 的磁盘空间。
是否继续 [Y/n]？

这次你可以看到 APT 已经获取并选中了安装 MySQL Server 5.0 所需的全部依赖，但它还列出了个“推荐”软件包和两个“建议”软件包，且没有选中它们进行安装。“推荐”软件包的意思就是：MySQL 软件包的作者（或其依赖的作者）认为你同时也安装 mailx 包是个明智的选择。如果你想添加它，按 N 终止 apt-get，然后像这样重新运行：

apt-get install mysql-server mailx

“建议”软件包只是一种更低级别的推荐。它们不会为你选择安装的软件增加任何关键功能，但你有可能在某些较小的场景下需要它们。

## 注意

APT 维护着一个软件包缓存，里面存放着它已下载并安装的 .deb 文件。这个缓存通常位于 /var/cache/apt/archives，有时会占用你电脑上数百兆字节的空间。你可以通过运行 apt-get clean 让 APT 清理软件包缓存，这会删除所有缓存的 .deb 文件。或者，你也可以运行 apt-get autoclean，它会删除超过一定时限的缓存 .deb 文件，从而保留较新的软件包。

如果你尝试用已经安装过的软件包运行 apt-get install，APT 会将你的命令视为 apt-get update，并检查是否有新版本可供下载。

最后一种日常软件包操作当然是移除不再需要的东西。这可以通过 apt-get remove 命令来完成，如下所示：

apt-get remove firefox

移除软件包可能很危险，因为 APT 也会移除所有依赖你所选软件包的其他软件。例如，如果你运行 apt-get remove libgtk2.0-0（Ubuntu 的主要图形工具包），你很可能会发现 APT 坚持要移除一百多个其他东西。这里的教训是：当你卸载软件时，在按 Y 继续卸载之前，一定要仔细阅读 APT 的报告。

直接执行 `apt-get remove` 会保留你程序的配置文件，这样如果你以后重新安装它，也无需重新配置。如果你想连配置文件一起删除，可以使用这个命令：

```
apt-get remove --purge firefox
```

这将执行一次完全卸载。

> **注意。**
> 
> 通过不带任何参数运行 apt-get 命令，你可以看到更全面的 apt-get 参数列表。底部那句晦涩难懂的话：“This APT has Super Cow Powers”，如果你运行 `apt-get moo` 命令，会变得更加令人费解。

## 查找软件

由于可用的软件包太多，使用命令行 APT 很难精确找到你需要的东西。通用的搜索工具叫 apt-cache，用法如下：

```
apt-cache search kde
```

根据你启用的软件源不同，这会返回大约一千个软件包。许多结果中甚至不包含 KDE 这个名字，而是因为描述中包含“KDE”一词而被匹配出来。

你可以通过几种方式筛选这些信息。首先，你可以让 apt-cache 只在软件包名称中搜索，而不是在描述中搜索。这可以通过 `-n` 参数实现，如下所示：

```
apt-cache --n search kde
```

现在搜索结果从 1006 个软件包减少到了 377 个。

另一种限制搜索结果的方法是使用一些基本正则表达式，比如 `^`（表示“开头”）和 `$`（表示“结尾”）。例如，你可能想搜索主 KDE 套件中的程序，而不想要库（通常命名为类似 libkde 的东西）、附加组件（比如 xmms-kde），以及那些实际上与 KDE 无关却仍然匹配我们搜索条件的东西（如 tkdesk）。这可以通过搜索以 kde 开头的软件包名称来实现，如下所示：

```
apt-cache -n search ^kde.
```

也许查找软件包最简单的方法，是把 apt-cache 和 grep 结合起来，在搜索结果中再进行搜索。例如，如果你想找到所有与游戏相关的 KDE 软件包，可以运行如下搜索：
