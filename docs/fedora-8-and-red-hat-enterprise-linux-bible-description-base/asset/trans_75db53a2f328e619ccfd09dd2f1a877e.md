

-   [RPMforge.net](http://rpmforge.net) — 该网站代表了三个独立仓库的合并，这些仓库曾提供 Fedora RPM 软件包：dag.wiiers.com、www.freshrpms.net 和 dries.ulyssis.org。他们致力于确保其提供的软件包与 Fedora 仓库保持兼容。有关 RPMforge 项目目标的更多信息，请参阅该网站的清单（[http://rpmforge.net/manifest.php](http://rpmforge.net/manifest.php)）。要配置您的 Fedora 系统以访问 RPMforge.net 仓库，请查找适用于 Fedora 8 的 rpmforge-release 软件包（目前可能尚未可用，但您阅读此内容时或许已经可用）：
    > http://rpmforge.net/user/packages/rpmforge-release

-   [Livna.org](http://rpm.livna.org) — 最初作为 Fedora.us 网站的扩展，rpm.livna.org 包含不属于 Fedora 项目的 RPM 软件包。这是一个获取音频和视频播放器（例如 xine、mplayer、ffmpeg、ogle 等）的好地方，这些播放器可能不符合 Red Hat 公司所遵循的许可证要求。通过安装 livna-release RPM，yum 将被配置为访问 rpm.livna.org 仓库。请在以下 URL 查找适用于 Fedora 8 的 livna-release RPM：
    > http://rpm.livna.org/fedora/8/i386/

-   [Dag](http://dag.wiiers.com/packages) — 该网站包含来自 2400 多个不同项目的超过 45,000 个 RPM。目前，该仓库尚未针对最新的 Fedora 版本进行更新，并且没有可自动设置从 yum 访问该仓库的 RPM。但是，您可以从合并后的 RPMForge.net 网站查找 Dag 软件包。

-   [FreshRPMs](www.freshrpms.net) — 另一个拥有大量高质量 RPM 的网站是 FreshRPMs.net。该网站拥有大量音频和视频播放器，这些播放器不在主流的 Fedora 仓库中。通过安装 freshrpms-release RPM，yum 将被配置为访问 FreshRPMs 仓库。请在以下 URL 查找适用于 Fedora 8 的 freshrpms-release RPM：
    > http://ayo.freshrpms.net/fedora/linux/8/i386/RPMG.freshrpms/

-   [Dribble](http://dribble.org.uk) — Dribble 仓库中包含了专注于趣味软件的 RPM 软件包。许多软件包是用于游戏和主机游戏模拟器的。请在以下 URL 查找 dribble-release 软件包，您可以使用它来自动为您的 Fedora 系统启用 Dribble 仓库：
    > http://dribble.org.uk/listrpm1.html

-   [ATRPMs](http://atrpms.net/dist/f8) — 该网站提供包含许多视频卡、无线网卡以及其他 Fedora 未包含的硬件驱动程序的 RPM。如果您想尝试个人视频录像机，该网站也提供 MythTV 项目的 RPM。通过安装 atrpms-package-config RPM，yum 将被配置为访问 atrpms.net 仓库。请在以下 URL 查找适用于 Fedora 8 的 atrpms-package-config RPM：

## 使用 yum 下载并安装 RPM

在确定了仓库之后，下载并安装您想要的 RPM 就像使用 *install* 选项运行 yum 来请求该 RPM 一样简单。在连接到互联网的情况下，以 root 用户身份打开一个终端窗口。

yum 首先会下载您可能需要的来自每个仓库的所有软件包的元数据和头文件。然后，在向您展示它认为您需要的依赖项列表后，它会询问您是否要安装必要的软件包。以下是使用 yum 命令下载 *madwifii* 媒体播放器的一个示例：

```
# yum install madwifi
Setting up Install Process
Parsing package install arguments
fedora 100%|=========================| 2.1 kB 00:00
atrpms 100%|=========================| 951 B 00:00
Reading repository metadata in from local files
primary.xml.gz 100%|==========| 2.5 MB 00:04
.
.
.
Transaction Summary
===============================================
Install 4 Package(s)
Update 0 Package(s)
Remove 1 Package(s)
Total download size: 17M
Is this ok [y/N]: y
Downloading Packages
.
.
.
```

正如从这个示例中可以看到的那样，yum 检查了两个不同的软件仓库：适用于 Fedora 8 的 Fedora 和 atrpms 软件包。在列出依赖项之后，yum 会询问安装它们是否没问题。输入 y 即可安装该软件包及其所有依赖项。

某些软件包，包括前面示例中显示的 madwifii 软件包，需要安装与您当前运行的内核相匹配的版本。因此，安装此类软件包时可能会同时带来更新的内核软件包。

## 使用 yum 本地安装软件包

如果您想使用 yum 安装来自本地系统的 RPM 软件包（通过插入 Fedora DVD 或将 RPM 复制到本地目录），可以使用 yum 的 *localinstall* 选项。例如，如果您插入随本书附带的 Fedora DVD（并且它已挂载在 `/media/disk/` 上），您可以输入以下命令来安装 gftp 软件包：

```
# yum localinstall /media/disk/Fedora/Packages/gftp-*
yum localinstall /media/disk/Fedora/Packages/gftp-2.0.18-7.fc8.rpm
.
.
.
Resolving Dependencies
---> Running transaction check
---> Package gftp.i386 1:2.0.18-7.fc8 set to be updated
Dependencies Resolved
================================================================================
Package    Arch     Version                  Repository        Size
================================================================================
Installing:
gftp       i386     1:2.0.18-7.fc8           /media/disk/Fedora/Packages/gftp-2.0.18-7.fc8.rpm
  946 k

Transaction Summary
================================================================================
Install    1 Package(s)
Update     0 Package(s)
Remove     0 Package(s)

Total download size: 946 k
Is this ok [y/N]: y
```

使用 `yum localinstall` 而不是 `rpm` 命令安装 RPM 软件包的一个好理由是，`yum` 会检查您正在安装的软件包是否依赖于其他已安装或需安装的其他软件包。如果 `yum` 发现需要其他软件包，它将搜索您配置的任何 `yum` 仓库（至少是主要的 Fedora 仓库）以下载并安装您所需的内容。

在这个示例中，您发现 gftp 不需要安装任何额外的软件包。因此，在提示符处输入 `y` 只会导致安装该一个软件包。

## 使用 yum 列出软件包

除了下载和安装新的 RPM 软件包外，yum 还可以用于列出可用的软件包以及已安装的软件包。以下示例说明了 yum 的一些用途。

如果您想查看可从您配置的仓库下载的所有软件包列表，请输入以下内容：

```
# yum list | less
```

在末尾添加 `less` 命令可以让您滚动查看软件列表（该列表可能很长，具体取决于您指向哪些仓库）。如果您尝试安装某个软件包并以类似 `package xyzpackage needs xyzfile (not provided)` 的消息失败，您可以使用 `provides` 选项检查包含缺失文件的软件包，如下所示：

```
# yum provides missingfile
```

使用 `provides` 选项，yum 将在您的仓库中搜索您输入的任何文件（而不是 `missingfile`）并返回找到的包含该文件的任何软件包名称。要搜索仓库中软件包描述中的特定字符串，请使用 `search` 选项。例如，以下命令在任何软件包描述中搜索 `arcade`（此搜索将找到一些游戏）：

```
# yum search arcade
```

由于 yum 软件包在安装后不会自动删除，您可能希望偶尔清理它们。要清除 `/var/cache/yum` 目录子目录中的软件包，请输入以下内容：

```
# yum clean packages
```

如果您想检查从主 Fedora 仓库以外的仓库安装的 RPM，可以使用 `list extras` 选项来完成。这是一个示例：

```
# yum list extras
Setting up repositories
Reading repository metadata in from local files
Extra Packages
AdobeReader_enu.i386
flash-plugin.i386 9.0.48.0-release installed
```

显示的列表包括 Acrobat Reader（我这是从 Adobe 网站获取的），它在显示 PDF 文件方面做得很好。另一个软件包用于在 Firefox 网络浏览器中运行 Flash 插件。请注意，该列表包括配置在您系统上的仓库中位于 Fedora 之外的所有软件包。（例如，如果配置了 Livna 和 ATRPMs 仓库，它将列出从这些仓库安装的软件包。）

## 使用 yum-utils 软件包

yum-utils 软件包中包含一些用于处理 yum 仓库和管理软件包的实用工具。要获取这些实用工具，请输入以下 yum 命令：

```
# yum install yum-utils
```

这些实用工具提供了不同的方法来清理仓库、获取但不安装软件包以及执行不同类型的查询。以下是一些示例：

-   **package-cleanup** — 检查本地 RPM 数据库中的依赖性问题和不需要的软件包。选项包括 `--problems`（用于检查 RPM 数据库中的依赖性问题）和 `--orphans`（用于列出当前不再需要的软件包...

