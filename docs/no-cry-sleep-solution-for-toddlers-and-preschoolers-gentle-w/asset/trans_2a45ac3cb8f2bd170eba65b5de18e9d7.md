

## 表 29-2
Linux 软件包文件扩展名
（续）

| 扩展名 | 文件 |
|---|---|
| .tar | tar 归档文件，使用 tar 的 xvf 选项解压。 |
| .tar.gz | gzip 压缩的 tar 归档文件。使用 gunzip 解压缩并使用 tar 解压。使用 tar 的 z 选项，如 xvzf，可在一步中同时解压缩和解压。 |
| .tar.bz2 | bzip2 压缩的 tar 归档文件。使用 tar -xvj 解压。 |
| .tz | 使用 compress 命令压缩的 tar 归档文件。 |
| .Z | 使用 compress 命令压缩的文件（使用 decompress 命令解压缩）。 |
| .deb | Debian Linux 软件包。 |

## Red Hat 软件包管理器（RPM）

包括 Red Hat、Mandrake、Caldera 和 SuSE 在内的多个 Linux 发行版使用 RPM 将 Linux 软件组织成可自动安装、更新或删除的软件包。RPM 是一个命令行驱动的软件包管理系统，能够安装、卸载、查询、验证和更新 Linux 系统上安装的软件包。RPM 软件包作为软件应用程序自身的安装程序运行。Linux 软件应用程序通常由多个需要安装到不同目录的文件组成。程序本身很可能放置在名为 /usr/bin 的目录中，在线手册文件如 Man 页面放在其他目录中，库文件放在另一个目录中。此外，安装可能需要修改系统上的某些配置文件。RPM 软件包会为你执行所有这些任务。此外，如果你以后决定不再想要某个特定应用程序，可以卸载软件包以从系统中删除所有文件和配置信息。RPM 的工作方式类似于 Windows 安装向导，可自动安装软件，包括配置、文档、图像、示例和程序文件，以及应用程序可能使用的任何其他文件。所有文件都会安装到系统上的相应目录中。RPM 维护已安装软件的数据库，跟踪所有已安装的文件。这使你也可以使用 RPM 卸载软件，自动删除属于该应用程序的所有文件。

## RPM 工具

要安装和卸载 RPM 软件包，你可以直接从 shell 提示符使用 rpm 命令，或使用 Red Hat 发行版软件管理工具 redhat-config-packages。redhat-config-packages 工具是 rpm 命令的 GUI 前端。虽然你应该为特定发行版下载 RPM 软件包，但许多 RPM 软件包设计为可在任何 Linux 系统上运行。你可以在其网站 www.rpm.org 上了解更多关于 RPM 的信息。该网站包含 RPM 的最新版本、文档以及 RPM 支持程序，如 rpm2html 和 rpm2cpio。rpm2html 会读取包含 RPM 软件包的目录并生成网页，列出这些软件包作为可用于下载它们的链接。rpm2cpio 是一个用于提取 RPM 的 Perl 脚本。此外，《Red Hat Linux 自定义指南》为 RPM 和 redhat-config-packages 提供了优秀的教程。

## RPM 软件包

RPM 软件包的命名约定因发行版而异。在 Red Hat 上，软件包名称包含软件包版本以及其平台（i386 代表 Intel PC）和 .rpm 扩展名。以下是 Intel 系统上 Emacs 编辑器 RPM 软件包的示例：

```
emacs-21.2-18.i386.rpm
```

你 DVD-ROM 或发行版 CD-ROM 上的 RPM 软件包仅代表可用于 Linux 的软件包的一小部分。rpmfind.net 上也设有庞大的 RPM 软件包存储库。此处的软件包按发行版、组和名称编入索引。该网站包含每个发行版的软件包，包括 Red Hat。

> 提示 带有 noarch 术语的 RPM 软件包用于架构无关的软件包。这意味着它们设计为可安装在任何 Linux 系统上。没有 noarch 的软件包可能是发行版或架构相关的，设计为安装在特定类型的机器上。

你可以将这些软件包放在系统上的一个目录中，然后使用 rpm 或 GUI RPM 实用程序（如 redhat-config-packages 工具）进行安装。通常，你应始终尝试使用为你的 Red Hat 发行版设置的 RPM 软件包版本；例如，如果你运行 Red Hat 9.0，最好下载指定为 Red Hat 9.0 的软件包，而不是下载 Red Hat 7.3 的相同软件包。特定版本的软件包将保存在版本目录中。在许多情况下，尝试安装为不同发行版准备的 RPM 软件包可能会失败。

## 从桌面安装：redhat-config-packages

redhat-config-packages 工具为管理由你的 Red Hat 发行版提供的 Red Hat RPM 软件包提供了一个有效且易于使用的界面，无论你是从 CD-ROM、DVD-ROM、硬盘还是网络安装的。它可在任何窗口管理器上运行，包括 GNOME 和 KDE。你可以使用系统设置窗口中的 Packages 图标访问 redhat-config-packages。这将打开一个软件包管理窗口，最初显示可用于安装软件包的软件包类别列表。有关更多详细信息，请参阅第 4 章。

> 提示 你也可以直接安装特定的 RPM 软件包。首先使用文件管理器显示它，然后双击它。这会调用 redhat-config-packages 工具来安装该软件包。它还会检查依赖软件包并同时安装它们。如果你使用 CD-ROM 而不是 DVD-ROM，将提示你根据需要插入其他 CD-ROM。

## 更新软件

你可以使用发行版更新代理（如 Red Hat Network）自动更新 Linux 系统。你也可以使用 FTP 客户端、Web 浏览器或 GNOME 或 KDE 文件管理器手动下载软件包，然后使用 rpm 命令或 redhat-config-packages 工具安装软件。

