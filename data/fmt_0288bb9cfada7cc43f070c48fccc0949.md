
# Yum 存储库

repos 文件中的存储库条目以括号括起来的头部开始。`name` 选项为存储库提供名称。URL 引用被分配给 `baseurl` 选项。应该只有一个 `baseurl` 选项，但你可以为它列出多个 URL，每个独占一行。你可以使用 `mirrorlist` 选项来列出镜像列表。`mirrorlist` 选项可以列出镜像列表，每个独占一行。`mirrorlist` 选项可以列出镜像列表，每个独占一行。`mirrorlist` 选项可以列出镜像列表，每个独占一行。`mirrorlist` 选项可以列出镜像列表，每个独占一行。`mirrorlist` 选项可以列出镜像列表，每个独占一行。`mirrorlist` 选项可以列出镜像列表，每个独占一行。`mirrorlist` 选项可以列出镜像列表，每个独占一行。`mirrorlist` 选项可以列出镜像列表，每个独占一行。`mirrorlist` 选项可以列出镜像列表，每个独占一行。`mirrorlist` 选项可以列出镜像列表，每个独占一行。`mirrorlist` 选项可以列出镜像列表，每个独占一行。`mirrorlist` 选项可以列出镜像列表，每个独占一行。`mirrorlist` 选项可以列出镜像列表，每个独占一行。`mirrorlist` 选项可以列出镜像列表，每个独占一行。`mirrorlist` 选项可以列出镜像列表，每个独占一行。`mirrorlist` 选项可以列出镜像列表，每个独占一行。`mirrorlist` 选项可以列出镜像列表，每个独占一行。`mirrorlist` 选项可以列出镜像列表，每个独占一行。`mirrorlist` 选项可以列出镜像列表，每个独占一行。`mirrorlist` 选项可以列出镜像列表，每个独占一行。`mirrorlist` 选项可以列出镜像列表，每个独占一行。`mirrorlist` 选项可以列出镜像列表，每个独占一行。`mirrorlist` 选项可以列出镜像列表，每个独占一行。`mirrorlist` 选项可以列出镜像列表，每个独占一行。`mirrorlist` 选项可以列出镜像列表，每个独占一行。`mirrorlist` 选项可以列出镜像列表，每个独占一行。`mirrorlist` 选项可以列出镜像列表，每个独占一行。`mirrorlist` 选项可以列出镜像列表，每个独占一行。`mirrorlist` 选项可以列出镜像列表，每个独占一行。`mirrorlist` 选项可以列出镜像列表，每个独占一行。`mirrorlist` 选项可以列出镜像列表，每个独占一行。`mirrorlist` 选项可以列出镜像列表，每个独占一行。`mirrorlist` 选项可以列出镜像列表，每个独占一行。`mirrorlist` 选项可以列出镜像列表，每个独占一行。`mirrorlist` 选项可以列出镜像列表，每个独占一行。`mirrorlist` 选项可以列出镜像列表，每个独占一行。`mirrorlist` 选项可以列出镜像列表，每个独占一行。`mirrorlist` 选项可以列出镜像列表，每个独占一行。`mirrorlist` 选项可以列出镜像列表，每个独占一行。`mirrorlist` 选项可以列出镜像列表，每个独占一行。

一旦配置好，你可以下载 Fedora Extras 和 Fedora Core 软件包。在命令行中输入带有 `install` 选项的 `yum` 命令（在桌面上打开终端（右键点击桌面））。系统将检测到包以及任何不同的软件，并询问你确认安装。下载和安装将是自动的。访问 `fedaproject.org/extras/4/` 查找可用的 Fedora Extras 列表。以下的 `gnumeric` 现在是一个 Fedora Extras 包。

```
yum install gnumeric
```

> 如果你没有可用的 Fedora Core 4 DVD-ROM，可以使用相同的 `yum` 命令下载并安装任何所需的额外 Fedora Core 包。例如，如果你需要安装 `gnucash`，只需输入以下内容：

```
yum install gnucash
```

## 第 31 章：软件管理

### APT

高级软件包工具（Advanced Package Tool）是一个最初基于 Debian 的旧安装工具。当前版本已修改为用于 RPM 软件包。你可以从 Fedora Extras 或 `freshrpm.net` 下载 APT。APT 将配置文件存放在 `/etc` 目录。`apt.conf` 文件包含选项设置，使用一种类似于 DNS 配置的更复杂的格式。

存储库列在 `sources.list` 文件中。每个条目由类型、URL 和路径名，以及标识软件的组件组成。最后一个组件是存储库的名称。以下是 `freshrpm` 的 `sources.list` 条目：

```
rpm http://ayo.freshrpm.net fedora/linux/i386 core updates freshrpm
```

你使用 `apt-get` 命令来安装和管理软件包。`apt-get` 工具接受两个参数：要执行的命令和包名。命令是一个术语，如 `install` 用于安装包，或 `remove` 用于卸载包。要安装一个包，你可以使用：

```
apt-get install xine
```

升级只需使用 `upgrade` 命令即可。在指定软件包的情况下，带有 `update` 选项的 `apt-get` 将升级你的整个系统，从 FTP 站点下载或从 CD-ROM 复制，并根据需要安装包。`-u` 选项显示正在升级的软件包。

```
apt-get -u update
```

### 红帽软件包管理器 (RPM)

包括 Fedora Core、Red Hat 和 Mandrake 在内的多个 Linux 发行版都使用 RPM 将 Linux 软件组织成你可以自动安装、更新或删除的软件包。RPM 是一个命令行驱动的软件包管理系统，能够对 Linux 系统安装的软件进行安装、卸载、查询、验证和更新。一个 RPM 软件包作为其软件应用程序的安装程序运行。Linux 应用程序通常由几个需要安装在不同目录的文件组成。项目本身可能被放在 `/usr/bin` 目录，手动文件放在其他目录，而库文件放在另一个目录。此外，安装可能需要修改你系统上的配置文件。RPM 软件包会为你完成所有这些任务。此外，如果你决定不再某个特定的应用程序，可以卸载软件包以从系统中删除文件和配置信息。RPM 的工作方式与 Windows 安装向导类似，会自动安装软件，包括配置、文档、图像、示例和程序文件，以及应用程序可能使用的任何其他文件。所有内容都安装在系统上相应的目录中。RPM 维护一个已安装软件的数据库，跟踪所有已安装的文件。使你能够使用 RPM 卸载软件，自动删除属于应用程序的所有文件。

### RPM 工具

要安装和卸载 RPM 软件包，你可以直接从 shell 提示符使用 `rpm` 命令，或者使用软件管理工具 `system-config-packages`。`system-config-packages` 是 `rpm` 命令的 GUI 前端。尽管你应该为你特定的发行版下载 RPM 软件包，但许多 RPM 软件设计为可以在任何 Linux 上运行。你可以在我们的网站 `www.rpm.org` 了解更多关于 RPM 的信息。该网站包含 RPM 最新版本、文档以及 RPM 支持程序，如 `rpm2html` 和 `rpm2cpio`。`rpm2html` 获取一个包含 RPM 软件包的目录并生成 Web 链接供你下载；`rpm2cpio` 是一个提取 RPM 的 Perl 脚本。此外，《红帽 Linux 定制化指南》为 RPM 和 `system-config-packages` 都提供了极好的教程。

### RPM 软件包

RPM 软件包的命名规范随发行版而异。包名包括软件包版本以及其平台（Intel PC 使用 `i386`）和 `.rpm` 扩展名。Intel 系统 Emacs 编辑器的 RPM 软件包示例在此：

```
emacs-21.4-3.i386.rpm
```

你 DVD-ROM 或发行版 CD-ROM 上的 RPM 软件包仅代表 Linux 可软件包的一小部分。一个丰富的 RPM 软件包库也位于 `rpmfind.net`。此处的软件包按发行版、组和名称进行索引。该网站包含每个发行版的软件包。

> 带有 `noarch` 术的 RPM 软件包用于体系无关的包。这意味着它们被设计为安装在任何 Linux 系统上。没有 `noarch` 的包可能取决于发行版或体系，设计用于安装在特定类型的机器上。

你可以将软件包放在系统上的某个目录中，然后使用 `rpm` 或 GUI RPM 工具（如 `system-config-packages`）。通常情况下，如果你决定不再某个特定的应用程序，可以卸载软件包以从系统中删除文件和配置信息。RPM 的工作方式与 Windows 安装向导类似，会自动安装软件，包括配置、文档、图像、示例和程序文件，以及应用程序可能使用的任何其他文件。所有内容都安装在系统上相应的目录中。RPM 维护一个已安装软件的数据库，跟踪所有已安装的文件。使你能够使用 RPM 卸载软件，自动删除属于应用程序的所有文件。

### 更新软件

你可以使用更新代理自动更新系统。如果你正在使用 `rpm` 命令，使用 `U` 选项进行升级。在下面的示例中，使用 `rpm` 命令配合 `Uvh` 选项为 `emacs-21.4-3.i386.rpm` 安装升级包。

## 命令行安装：rpm
