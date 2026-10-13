
## 图形软件包管理

在菜单中标识为“添加/删除软件”（Add/Remove Software）的 Fedora Core Linux 软件包管理工具实际上名为 `redhat-config-packages` 的应用程序。该应用程序取代了不再提供的 `kpackage`、`gnorp` 和 `rpm`。“添加/删除软件”允许你选择分类排列的软件包并安装或删除它们。随着 YUM 加入 Fedora Core，你现在可以将你的软件包添加到 Fedora Core 图形工具的数据库中，提高了其相于早期版本的实用性。

通过点击桌面上的“开始”按钮，然后选择“系统”（System）、“添加/删除应用程序”（Add/Remove Applications），启动 Fedora Core GUI 软件包管理器。软件包管理工具启动后显示“添加和删除软件”界面，如图 8.2 所示。

![](img/96ce0bc6bd65a9b4c721fc1cd7169438_256_0.png)

图 8.2 如果你安装了 Fedora Core，软件包管理工具的界面看起来很熟悉；它是安装程序使用的软件包选择屏幕。

屏幕列出的软件包组织为桌面（Desktops）、应用程序（Applications）、服务器（Servers）、开发（Development）和系统（Systems）组。左侧的图形按钮允许你选择两种模式之一：安装或删除。要选择特定的软件包组进行安装或删除，请先点击相应的图形按钮。软件包组名称右侧的数字表示安装在你系统上的软件包数量以及该组中可用软件包的总数。在图 8.2 中，你可以看到 42 个可能的 GNOME 软件包中已安装了 39 个。

> 提示
> 查看（View）菜单允许你在默认组列表和单个软件包列表之间切换——如果你知道要找的软件包名称，这将非常。在“软件包视图”模式下，勾选软件包旁边的框框来安装或删除它；软件包管理器将始终解决任何依赖关系。

点击“添加软件包组”左侧的“删除软件”或“安装”按钮将弹出一个窗口，显示与相关类别相关的软件包列表。图 8.3 显示了 KDE 环境软件包的详情。

![](img/96ce0bc6bd65a9b4c721fc1cd7169438_257_0.png)

图 8.3 “已安装的软件包”列表（在此视图中已折叠）详细介绍了在选择主类别时安装的基础软件包。“未安装的软件包”是指你有权安装的软件包。

## 使用 Red Hat Network 和替代方案进行软件管理

对于 Red Hat 8 和 9 版本，由 Red Hat 提供的系统软件管理命令行应用程序是 RPM；唯一的 GUI 管理工具是 Red Hat Packages 图形客户端（`redhat-config-packages`），现在被标识为“添加/删除软件”。对于普通人来说，RPM 复杂得难以理解；它包含了额外的复杂性，以便作为通用的 .rpm 文件构建和开发工具使用，而许多人并不需要。图形软件管理客户端已针对 Fedora Core 进行了改进，使其可以使用本地和 YUM（YUM 代表 YellowDog Updater Manager，首次用于 YellowDog [PPC] Linux 发行版）。

本书之前未涵盖的是 Red Hat Network (`https://rhn.redhat.com`—见图 8.4)。没有涵盖 RHN 是因为它对本书的用户（或对使用免费提供的 FTP 下载版本的用户）不是免费的，并且它仅限于管理由 Fedora 提供的软件。

![](img/96ce0bc6bd65a9b4c721fc1cd7169438_258_0.png)

图 8.4 Red Hat Network 提供自动更新。RHN 服务是一个用户可以通过订阅 Red Hat、获取更新、错误说明和安全修复的客户端。

```bash
rpm -ivh http://ftp.freshrpmms.net/pub/freshrpmms/redhat/9/apt/apt-0.5.5cnc6-fr1.1386.rpm
```

查看 apt 的主页。最重要的命令是 `apt-get update` 和 `apt-get install package`。

apt 软件库列表已预配置在 `/etc/apt/sources.list` 中，但需要通过以下命令更新可用软件包的索引：
`# apt-get update`

一旦软件包列表更新完成，我们建议您安装 Synaptic，即图 8.5 所示的 GUI 包管理器。
`# apt-get install synaptic`

从命令行启动 synaptic，浏览可用软件包并安装您喜爱的包。

```
synaptic &
```

Synaptic 的图形化界面布局非常精美（见图 8.5）。它允许您查看所有可用软件包的列表及其任何依赖项。它还提供了一个添加新软件库的图形界面。

![](img/96ce0bc6bd65a9b4c721fc1cd7169438_260_0.png)

图 8.5 Synaptic 是 APT 软件包管理程序的图形界面，使其易于使用。

# 第 8 章 管理软件和系统资源

## YUM

一些开发者认为，尽管 APT 是一个很好的工具，但将其用于 .rpm 软件包是一种“权宜之计”。APT 还被认为冗余了用于 Debian .deb 软件包的必要代码。一种新工具 YUM 是使用 Python 语言开发的，因为 Fedora Core 安装程序 Anaconda 是用 Python 编写的，许多代码可以共享。这一决策使得 YUM 成为集成到 Fedora Core 发行版的选择。它的工作与 APT 相同，但缺乏 GUI 工具。Fedora 开发者已将对 YUM 支持集成到图形化的 Hat/Fedora 包管理工具中。您可以从 Fedora 网站以及 FreshRPMs.net 获取 YUM；YUM 的主页位于 `http://linux.duke.edu/projects/yum`。

以下是安装和配置 YUM 的方法：

- 在 Fedora 网站 `http://fedora.mplug.org/` 阅读 HOWTO 和用户 FAQ。
- 安装 Fedora GPG 密钥：
```bash
$ wget -source http://fedora.mplug.org/FEDORA-GPG-KEY | gpg --import
```
- 安装正确版本的 YUM。注意，当前版本将与示例中列出的不同；请先在 `http://download.fedora.us/fedora/redhat/` 查找正确的包版本。
```bash
# rpm -ivh http://download.fedora.us/fedora/redhat/9/i386/RPMS.stable/yum-2.0.1-0.fed.2.rh90.noarch.rpm
```
- 查看 yum 的帮助页，以熟悉所有可用选项。
```bash
$ man yum
```

一旦安装了 YUM，以下命令将非常有用（请记住，如果您配置了使用 YUM 软件库，则可以使用 Fedora 图形客户端）：

```
yum list -A 软件库中所有可用软件包的列表。
yum list installed—您的计算机上已安装的所有软件包列表。
yum list updates—您的计算机可用的所有更新列表。
yum install package—安装软件包。
yum update—带有包名运行，YUM 将更新所有已安装的软件包。
yum remove package—删除软件包及其依赖项。
yum upgrade—在不带包名运行，YUM 将升级所有软件包并删除任何过时的软件包；yum update 不会删除过时的软件包。
```

## 从源码编译软件

您会发现 APT 或 YUM 都是 Fedora Core 有用的补充。如果您想安装第 26 章“多媒体应用程序”中描述的某些多媒体应用，我们建议使用来自 FreshRPM.net 的工具。

并不是您可能想要使用的软件都以 rpm 包的形式提供，或者以您所需的精确形式存在。许多复杂的程序具有只有在编译时才能选择的选项，并且许多较小的特殊用途应用程序仅以源码形式存在。Fedora Core 提供了将源码编译为二进制应用程序所需的所有工具。首先，我们将介绍从源码 rpm 文件进行构建，然后处理源文件，最后从源码 tar 包（tarballs）进行构建。

> 对于其他软件软件包格式，您可以使用 File Roller 应用程序（在“附件”菜单中找到）轻松地显示、浏览、读取和提取压缩文件的内容，包括旧的 tar 包或 tar 归档（通过其 .gz 或 .tgz 扩展名识别）。File Roller 还支持其他压缩文件，例如用 compress 命令创建的文件（以 .Z 结尾）或以 .bz2 结尾的 bzip2 文件。Roller 客户端还 gzip 和 bzip2 格式之间转换压缩归档。

## 从 src.rpm 文件构建 RPMS

一个经验法则是，即使目录已经在 `/usr/src/redhat` 如下设置好，您也永远不要以 root 用户构建 rpms：

```
# tree /usr/src/redhat
```
