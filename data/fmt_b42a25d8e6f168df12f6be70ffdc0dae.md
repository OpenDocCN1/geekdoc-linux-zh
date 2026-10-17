
对于单个系统上的软件管理，在 RPM 还是 DEB 的争论中，双方都有支持者，且各自有不同的观点。尽管 RPM 是管理企业级软件安装、更新和维护的首选格式，但 DEB 在 Linux 爱好者中非常流行。本章涵盖了 RPM（Fedora 和红帽企业版）以及（在某种程度上）DEB 打包和软件管理。

## 理解 DEB 打包

Debian 软件包将与一组软件相关的多个文件和元数据封装在一个归档文件中。这些文件包含（命令）、配置文件、文档和其他软件项。元数据包括依赖关系、许可、软件包大小、描述和其他信息。在 Ubuntu、Debian 和其他 Linux 发行版中，有多种命令行和图形工具可处理 DEB 文件。其中包括以下几个：

`Ubuntu 软件中心` 从 GNOME 活动菜单中选择 Ubuntu 应用。出现的窗口允许你通过关键词或浏览类别来搜索你需要的应用程序和软件包。

![](img/cc1e2b1a5739a47bac1a4c7cfac7c1a6_266_0.png)

- `aptitude` `aptitude` 命令是一个软件包安装工具，提供了一个在 shell 中运行的面向屏幕的菜单。运行命令后，使用方向键高亮你想要的选择，按回车键选择。你可以升级软件包、获取新软件包或查看已安装的软件包。
- `apt` 有一组 `apt` 命令（`apt-get`、`apt`、`apt-config`、`apt-cache` 等）可以管理安装。

Ubuntu 软件中心在查找和安装软件包方面非常直观。然而，这里有几个可以帮你使用 `apt` 命令安装和管理软件包的命令示例。在这种情况下，我使用 `apt` 命令来安装和管理软件包：

```
sudo apt-get update  # 获取最新的软件包列表
sudo apt-cache search vsftpd  # 搜索 vsftpd
sudo apt-cache show vsftpd  # 显示 vsftpd 的信息
sudo apt-get install vsftpd  # 安装 vsftpd
sudo apt-get upgrade  # 升级软件包
sudo apt-cache list  # 列出已安装的软件包
```

## 理解 RPM

RPM 软件包是多个文件的整合，用于提供（例如，字处理器、命令行界面、配置文件和文档）。软件可以包含在 RPM 内部。RPM 文件还包含元数据，元数据存储了有关软件包的信息、它来自哪里、它需要什么以及其他信息。

### 什么是 RPM？

在查看 RPM 内部之前，你可以通过 RPM 本身的名字了解到关于它的许多信息。要找出系统中当前安装的 RPM 软件包名称（在本例中为 Firefox 浏览器），你可以在 Fedora 或红帽企业 Linux 的 shell 中输入以下命令：

```
# -q firefox
firefox-67.0-4.fc30
```

从这中你可以知道软件包的基础名称是 firefox。版本号是 67.0（由上游制作者 Mozilla 项目分配）。发布版本（由打包者 Fedora 分配）在每次重新构建软件包时都是 4。firefox 软件包是为 Fedora 30 (fc30) 构建的，架构是 86 位 (x86_64)。

当 firefox 软件包安装时，可能是从安装介质（如 CD 或 DVD）复制的，或者从 YUM 仓库下载的。无论它来自哪里，一旦软件包安装，其名称将在本地目录显示为 firefox-67.0-4.fc30.x86_64。要找出 RPM 内部有什么，你可以使用 RPM 命令以外的选项来查询本地数据库，在本例中：

```
# -qi firefox
Name : firefox
Version : 67.0
Release : 4.fc30
Architecture: x86_64
Install Date : Sun 02 Jun 2019 09:37:25 PM EDT
Group : Unspecified
Size : 266429426
License : MPLv1.1 or GPL2+ or LGPL2+
Signature : RSA/SHA256, Fri 24 May 2019 12:09:57 PM EDT, Key ID ef3c11lcc9
Source RPM : firefox-67.0-4.fc30.src.rpm
Build Date : Thu 23 May 2019 10:03:55 AM EDT
Build Host : buildwh-08.ph2.fedoraproject.org
Relocations : (not reloc)
Packager : Fedora Project
Vendor : Fedora Project
URL : https://www.mozilla.org/firefox/
Bug URL : https://bugs.fedoraproject.org/firefox
Summary : Mozilla Firefox Web browser
Description :
Mozilla Firefox 是一个开源网络浏览器，为标准兼容性、性能和可移植性而设计。
```

# 第三部分：成为 Linux 系统管理员

作为上游软件提供者，他们通常在特定的许可条件下，将软件提供给任何需要它的人。

Linux 发行版获取源代码并将其构建为二进制执行文件。然后，它将这些二进制文件与文档、配置文件、脚本以及从上游提供者提供的其他组件收集在一起。

在所有这些组件都收集到 RPM 包中后，安装该 RPM 包，你可以添加更多软件包，让用户测试该包的有效性，并将其放置在针对特定发行版和架构（32位 x86，64位 x86）的 RPM 存储库中。该存储库被放置在安装 CD 或 DVD 上，或者放在作为 FTP 或 NFS 服务器提供的目录中。

## 安装 RPM 包

当你安装 Fedora 或 Red Hat Enterprise Linux 系统时，许多单独的 RPM 软件包构成了该安装。Linux 安装好后，你可以使用“软件”窗口（如前文所述）添加更多软件包。有关安装 Linux 的信息，请参阅第 9 章“安装 Linux”。

然而，开发的第一个用于安装 RPM 软件包的工具是 `rpm` 命令。使用 `rpm`，你可以安装、更新、查询、验证和删除 RPM 软件包。但是，该命令存在一些主要缺点：

- 对于大多数软件包，系统上必须安装其他软件（库、可执行文件等）。当你尝试用 `rpm` 安装软件包时，如果某个依赖包未安装，则包安装将失败，并告诉你需要哪些组件。此时，你必须去寻找该包，该包本身可能还有需要你安装的依赖项才能使其工作。这种情况被亲切地称为“依赖地狱”（dependency hell），并被用作说明为什么 DEB 包比 RPM 包更好的例子。在 RPM 相关的打包工具能够实现此功能之前，DEB 打包工具就可以自动解决软件包依赖。
- RPM 的位置：`rpm` 命令要求你在想要安装时提供 RPM 文件的确 exact 位置。换句话说，如果 RPM 包在当前目录下，你需要提供 `firefox-67.0-4.fc30.x86_64.rpm` 作为选项；或者如果它在服务器上，则需要提供 `http://example.com/firefox-67.0-4-fc30.x86_64.rpm`。

随着 Red Hat Linux 和其他基于 RPM 的应用程序越来越流行，显然，必须采取某些措施来使包安装更加方便。答案是 YUM 工具。

# 第 10 章：获取和管理软件

## 使用 YUM 管理 RPM 软件包

Yellow Updater Modified (`YUM`) 项目旨在解决管理 RPM 软件包依赖关系的头疼问题。它的主要贡献是不再将 RPM 软件包视为单个组件，而是将它们视为大型软件存储库（repositories）的一部分。

有了存储库，处理依赖关系的问题就不再取决于安装软件的人，而是取决于提供该软件的 Linux 发行版或第三方软件分发商。因此，例如，将由 Fedora 项目负责，确保其 Linux 发行版中每个软件包所需的每个组件都能通过其他某个存储库得到解决。

存储库之间可以相互构建。例如，`rpmfusion.org` 存储库可以假设用户已经访问了主存储库。如果从 `rpmfusion.org` 安装的软件包需要 Fedora 存储库中的库或命令，那么在安装 `rpmfusion.org` 包的同时，可以同时下载并安装 Fedora 包。

Yum 存储库可以放在 Web 服务器（`http://`）、FTP 服务器（`ftp://`）、本地介质（如 CD 或 DVD）或本地目录（`file://`）的存储库中。这些存储库的位置将存储在用户系统的 `/etc/yum.conf` 文件中，或者更常见的，位于 `/etc/yum.repos` 目录下的配置文件。

## 从 yum 迁移到 dnf
