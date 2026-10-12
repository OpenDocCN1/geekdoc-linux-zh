
如果有任何软件包被选中移除，通过从主菜单选择“移除”即可启动此过程。移除过程完成后，你将返回到 `dselect`。

### 退出

要退出 `dselect`，请从主菜单选择“退出”。

### 使用 apt-get

**目标 2.2 安装与软件包管理**

- 使用 Debian 软件包管理。涉及使用以下命令和程序：`dpkg`、`dselect`、`apt`、`apt-get`、`alien`。

`apt-get` 是一个命令行工具，具有 `dselect` 的大部分功能，但没有有时并不需要的界面开销。`apt-get` 工具会自动获取软件包，就像 `dselect` 一样，以及任何所需的依赖项。

### 编辑 sources.list 文件

在 `apt-get` 获取软件包进行安装之前，它必须知道从哪里获取它们。`/etc/apt/sources.list` 文件列出了软件包的可能来源。这与 `dselect` 中 `apt` 来源使用的文件相同。该文件以简单的资源列表布局，使用以下格式：

```
deb uri distribution component
```

用于二进制软件包，以及：

```
deb-src uri distribution component
```

用于源代码软件包。

URL 代表通用资源标识符（Uniform Resource Identifier），它是大多数人熟悉的常见 URL 格式的一个超集。它使用以下语法：

```
protocol://host/path
```

URL 的 `//host` 部分仅用于 HTTP 和 FTP 方法。`sources.list` 文件中支持的四种协议类型如下：

- `cd-rom`—本地 CD-ROM 驱动器
- `file`—本地目录
- `http`—网站
- `ftp`—FTP 站点

Debian 通常同时有两个当前分发版。它们如下：

- `stable`—这是最新的官方发行版。对该分发版所做的唯一更新是安全更新。
- `unstable`—此版本处于持续变化状态。它最终将成为下一个 `stable` 版本。不建议在生产系统中使用。

并非所有站点都提供所有组件，因此必须单独指定。标准组件如下：

- `main`—主要软件包集合。
- `contrib`—次要软件包。
- `non-free`—Debian 是一个完全免费的发行版，但一些有用的软件包不被视为免费。这些软件包位于此组件中，并不被视为 Debian 发行版的一部分。

我们建议将速度最快的源放在 `sources.list` 文件的顶部。可以使用 `#` 符号向列表中添加注释，这在添加其他源时可能非常有用。为特定应用程序或软件包添加源是很常见的。`sources.list` 文件的一个示例如下：

```
# See sources.list(5) for more information, especially
# Remember that you can only use http, ftp or file URLs
# CDROMs are managed through the apt-cdrom tool.
deb http://http.us.debian.org/debian unstable main contrib non-free
deb http://non-us.debian.org/debian-non-US unstable/non-US main contrib non-free
deb http://security.debian.org stable-updates main contrib non-free
```

```
#HelixCode
deb http://spidermonkey.helixcode.com/distributions/debian unstable main
```

```
# Uncomment if you want the apt-get source function to work
#deb-src http://http.us.debian.org/debian stable main contrib non-free
#deb-src http://non-us.debian.org/debian-non-US stable non-US
```

### 更新可用软件包

Debian 软件包数据库维护了一个可用软件包的列表。定期更新此列表以及在您对 `sources.list` 文件进行任何更改时更新此列表都非常有用。要更新列表，请运行以下命令：

```
apt-get update
```

`apt-get` 将遍历源列表并更新软件包数据库。

### 安装软件包

当指示 `apt-get` 安装软件包时，它首先检查该软件包是否已下载。如果没有，`apt-get` 将访问列表中具有最新版本的第一个源。如果需要依赖项，它们也会被获取。要安装软件包，请使用以下命令：

```
apt-get install package_name
```

例如：

```
norbert:~# apt-get install ethereal
Reading Package Lists... Done
Building Dependency Tree... Done
The following extra packages will be installed:
  libpcap0
The following NEW packages will be installed:
  ethereal libpcap0
0 packages upgraded, 2 newly installed, 0 to remove and 202 not upgraded.
Need to get 1240kB of archives. After unpacking 3153kB will be used.
Do you want to continue? [Y/n]
Get:1 http://http.us.debian.org unstable/main ethereal 0.8.13-2 [1202kB]
Get:2 http://http.us.debian.org unstable/main libpcap0 0.4a6-3 [38.6kB]
Fetched 1240kB in 16s (74.0kB/s)
Selecting previously deselected package libpcap0.
(Reading database ... 53531 files and directories currently installed.)
Unpacking libpcap0 (from .../libpcap0_0.4a6-3_i386.deb) ...
Selecting previously deselected package ethereal.
Unpacking ethereal (from .../ethereal_0.8.13-2_i386.deb) ...
Setting up libpcap0 (0.4a6-3) ...
Setting up ethereal (0.8.13-2) ...
```

当安装 `Ethereal` 软件包时，它还需要 `libpcap0`。`apt-get` 工具会提示用户获取依赖项。如果您在提示处回答 `Yes`（是），额外的软件包将自动获取并一次性安装。

### 升级软件包

`apt` 系统最强大的功能之一是可以将已安装的所有软件包一次性升级到最新版本。为此，请使用以下命令：

```
apt-get upgrade
```

在进行升级之前，请务必执行 `apt-get update`，以确保软件包列表是最新的。根据系统的互联网连接速度，升级可能需要一段时间。

### 删除软件包

可以使用 `apt-get` 和 `dpkg` 删除软件包。该命令如下所示：

```
apt-get remove package_name
```

### 升级发行版

虽然 Debian 的安装可能不像其他发行版那样流畅，但它弥补了这一点，因为即使升级到发行版的新版本，您也只需运行一次即可。当一个新发行版发布时，整个发行版都可以通过 `apt-get` 工具升级到新版本。

```
apt-get dist-upgrade
```

这与正常升级程序的区别在于，`apt` 使用更智能的依赖项检查，可能会以其他软件包为代价升级更重要的软件包。

### 清理软件包归档

当 `apt-get` 安装软件包时，它会在 `/var/cache/apt/archives` 和 `/var/cache/apt/archives/partial` 目录中的归档中保留 `deb` 文件的副本。随着时间推移，这些文件可能会占用大量磁盘空间。要清除这些目录中的所有文件，请使用以下命令：

```
apt-get clean
```

有时保留一些归档可能有益。要仅清除不再当前且无法再次下载的软件包，请使用以下命令：

```
apt-get autoclean
```

### apt-get 选项
