
> 注意虽然其他仓库通常指向镜像站点，但许多专家建议不要对安全仓库连接到镜像。

最后，还有各种小组利用 Ubuntu 的成功，提供了超出 partner、universe 和 multiverse 仓库中可用内容的额外功能。一个众名的例子是 Ultimatix (http://ultimatix.com)，它基于 Automix 的工作，后者ix 可以自动安装许多多媒体和桌面应用程序。这些被称为第三方仓库。并不是所有创建特殊仓库的第三方都与 Ubuntu 开发者密切合作，因此在使用这些项目中的软件之前要格外小心。

第三方仓库的一个风险与依赖有关。如果依赖项不存在或与关键 Ubuntu 软件包冲突，可能会影响其他软件包。对其他软件包的影响可能会导致更多软件包的问题。

这被称为依赖地狱。因此，如果你对某个第三方仓库不确定，请查看在线反馈。阅读其他用户在该仓库中遇到过的任何问题。

## 寻找合适的镜像

在安装过程中，你可能配置了指向某个镜像的连接，但该镜像并非最适合你。例如，当我从西海岸追踪到 `http://us.archive.ubuntu.com` 镜像的路由时，它实际上连接到了英国的一个服务器。任何位于美国大陆的镜像都可能我的系统提供更好的服务。

> 注意：追踪远程服务器路由的一种方法是使用 `traceroute` 命令。或者，本地用的 IP 工具可以帮助识别远程服务器的地理位置。

因此，为了找到与镜像的最佳连接，最好是找到一个离我最近的镜像。你可以从 https://launchpad.net/ubuntu/+archivemirrors 在线获取 Ubuntu 镜像列表。在选择镜像时，请考虑以下因素：

- 地理距离：物理上离你近的镜像不太受流量问题的影响。
- 协议：并非所有的镜像都支持访问 HTTP、FTP 和 rsync 服务器。
- 速度：取决于选择镜像的用户数量，较快的镜像通常会导致更快的下载速度。

如果你可以使用 GUI，该过程可以某种程度上自动化。打开“软件源”应用程序：从 GNOME 桌面，选择系统 | 管理 | 软件源。如果你想通过远程 SSH 连接安装此，请运行 `sudo software-properties-gtk` 命令。在图 8-2 中的 Ubuntu 软件选项卡中，点击“下载自”下拉框。点击“其他”打开图 8-3 中的“选择下载服务器”窗口。

你可以使用该工具来评估配置的下载服务器列表。亲自尝试一下；点击“选择最佳服务器”。当我点击此按钮时，它选择了一个几个州之外的服务器。然而，还有许多具有相同连接速度且离我更近的镜像站点。因此，记住对结果做出你自己的判断，并结合上述的 Ubuntu 镜像列表进行评估。

## 基础 apt 命令

本章早期部分描述了 `dpkg` 命令的问题之一：当存在依赖时安装会困难。虽然可以强制安装包，但覆盖现有的依赖是有风险的。无法访问依赖的已安装包会导致相关命令和应用程序出现问题。

# 第 8 章：管理更新和本地仓库

199

图 8-2 软件源

图 8-3 选择下载服务器

这就是 `apt-*` 命令可以帮助的地方。具体来说，`apt-get install package` 和 `apt-get remove package` 会安装和移除你选择的包及其所有依赖。当然，由于使用 `dpkg` 命令安装包需要管理员权限，`apt-get` 命令也是如此。

`apt-get` 命令像 `dpkg` 命令一样丰富且通用；一些人说它们更通用。为了确保本地软件包数据库是最新的，请定期运行以下命令：

```bash
$ sudo apt-get update
```

该命令适用于第 7 章中的 `cron` 守护进程，并可能适用于 `/etc/cron.daily/apt` 脚本。

`apt-get` 命令还有更多功能。以下命令查看所有当前软件包，并将它们与可用更新进行比较：

```bash
$ sudo apt-get upgrade
```

根据软件包的当前状态，可能会列出几个包，并带有它们本应该被安装或移除的消息。这些包可以使用以下命令之一捕获：

```bash
$ sudo apt-get -f install
$ sudo apt-get -f remove
```

另一种方法使用 `dselect-upgrade` 选项。`-u` 显示升级的包：

```bash
$ sudo apt-get -u dselect-upgrade
```

如果你想更新本地系统上的所有软件包，以下软件包会将所有包与可用包进行对比：

```bash
$ sudo apt-get -u dist-upgrade
```

如果你想将所有软件包更新到下一个版本，请更改 `/etc/apt/sources.list` 配置文件中的版本名称。例如，将该文件中所有的 `hardy` 实例更改为 `trepid` 将是版本升级的序曲。请注意，此操作将将升级到一个没有长期支持的版本，并可能影响支持

`/var/cache/apt/archives` 目录很容易被数个 GB 字节的可能过时的包文件填满。你可以使用以下命令清理此目录中的所有包：

```bash
$ sudo apt-get clean
```

或者，你也可以可以使用以下命令清理那些已经过时的包（在大多数情况下被更新的包所取代）：

```bash
$ sudo apt-get autoclean
```

## 更多 apt 命令

`apt-get` 命令只是许多可用的基于 `apt` 的命令之一。本节讨论的其他命令包括 `apt-cache`、`apt-file` 和 `apt-longterm`。`apt-ftarchive` 命令将在本章后面帮助创建仓库镜像。

有关 `apt` 命令和选项的完整列表，请参见 Debian Linux apt HOWTO，可在 www.debian.org/doc/ 获取。

### apt-cache

查看可用软件包简单的方法是使用 `apt-cache` 命令。假设本地仓库是最新的，例如：

```bash
$ apt-cache search
```

如果你对依赖感兴趣，例如：

```bash
$ apt-cache depends
```

### apt-file

`apt-file` 命令为包提供了搜索功能。如果你需要安装它，请运行：

```bash
$ sudo apt-file update
```

### apt-ftarchive

`apt-ftarchive` 命令可以在本章后面帮助创建仓库镜像。具体来说，以下命令创建一个 `Packages.gz` 文件：

```bash
$ sudo apt-ftarchive packages - | gzip -9 > Packages.gz
```

### Ubuntu Server

第一次运行 `apt-file` 命令时，你需要更新：

```bash
$ sudo apt-file update
```

## 第 8 章：管理更新与本地仓库

```
操作 撤销 解析器 选项 视图 帮助
C-T: 菜单 ? 帮助 Q:退出 u 更新 g:下载/安装/移除 软件包
aptitude 0.4.3
-- 安全更新
-- 可更新软件包
-- 已安装软件包
-- 未安装软件包
-- 过时本地创建软件包
-- 虚拟软件包
  任务
这些软件包的安全性更新可从 security.ubuntu.com 获取。
```

图 8-4. aptitude 工具

```
操作 撤销 解析器 选项 视图 帮助
C-T: 菜单 ? 帮助 Q:退出 u 更新 g:下载/安装/移除 软件包
aptitude 0.4.3 将使用 2642KB 的磁盘空间 DL Size: 11.8MB
-- 可更新软件包
-- 已安装软件包
-- 管理实用程序（安装软件、管理用户等）
-- main 每日支持的免费软件。
apt-utils 0.7.sububuntu 0.7.sububuntu
aptitude 3.1.1ubuntu 3.1.1ubuntu
at
command-not-found 0.2.sububuntu 0.2.sububuntu
command-not-data 0.2.sububuntu 0.2.sububuntu
cron 3.01-110 3.01-110
基于终端的包管理器
功能，包括：一种类似 mutt 的语法，用于灵活地匹配软件包，
例如用户操作的持久化、检索并
显示大多数软件包的 Debian 变更日志的能力，以及一种类似于 apt-get 的命令行模式。
aptitude 还是符合 YUI 标准的、非臃肿的、自清理的且无损的。
```
