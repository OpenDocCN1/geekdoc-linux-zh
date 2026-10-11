
```
arson KDE search for burning cdr
bootcd-dvdplus booted extension to use DVD+ media
burn - Command line Data-CD, Audio-CD, ISO-CD, Copy-CD writing tool
ca-utils - text metric graphics
cdcontrol - A parallel barrier allows you to write to one or more CD-Writers
at once
cdblagen - generates front cards and tray cards for CDs
cdpoaster - Tlk/Frk for burning cdrom
cdw - Tool for burning CD's console version
cd-common - Tool for burning CD's common files
cdpuburn - a collection of packages to put heavy load on CPU
cswdr - One Atm CD Rip
dvd+rw-tools - DVD=RW tools
dvd-backup - Tool to rip DVD's from the command line
gcdw - Tool for burning CD's - graphical version
gcombust - GTK+ based CD mastering and burning program
- lines deleted...
```

输出显示了几个我可以安装的潜在 CD/DVD 刻录程序。要发现更多关于任何软件包的信息，输入 `apt-cache show packageName`，其中 `packageName` 是你想要信息的软件包名称。例如，为了获取更多关于 `dvd-rw-tools` 软件包的信息，我输入 `apt-cache show dvd-rw-tools`，输出显示了软件包的描述。然后我可以使用 `apt-get install` 安装该软件包。

![](img/fb03f7f944c69a481f34f490e877a2b9_459_0.png)

提示：要搜索软件包名称中出现的关键词，请使用 `--names-only` 选项，如下：`apt-cache search --names-only keyword`，其中 `keyword` 是出现在软件包名称中的内容。例如，如果我想查找名称中包含 `selinux` 的软件包，我输入 `apt-cache search --names-only selinux`。

# 从源码文件构建软件包

> 提示
>
> 定期运行 `apt-get clean` 来清理本地仓库（位于 `/var/cache/apt/archives` 目录）中已安装的 DEB 文件。你可以通过删除这些 DEB 文件来释放一些磁盘空间。

## 从源码文件构建软件包

许多开源软件包以源码形式分发，不包含可执行的二进制文件。在使用此类软件之前，你必须通过编译来构建可执行的二进制文件，并且必须遵循某些指令来安装软件包。在本节中，我将向你展示如何从源码文件构建软件包。

### 下载并解压软件

源码通常以压缩 tar 存档的形式分发。这些存档是由 `tar` 程序创建并用 `gzip` 程序压缩的。发行形式为具有 `.tar.gz` 或 `.tar.Z` 扩展名的单个文件——通常称为压缩 tar 包（tarball）。如果你需要该软件，必须下载并解压它。

### 从源文件构建软件包

大多数开源软件软件包（包括 XMMS）都带有一个名为 `COPYING` 的文件。该文件包含 GNU 公用许可证（GPL）的全文，它详细规定了你可以使用和分发软件的条件。如果你不熟悉 GNU GPL，请阅读此文件并将许可证展示给你的法律顾问，以获得完全解释并评估其对你业务的适用性。

要构建软件包，请遵循 `README` 或 `INSTALL` 文件中的说明。对于 XMMS 软件包，README 文件列出了一些前提条件（如库），并告诉你要使用哪些命令来构建和安装软件包。在 XMMS 的情况下，说明指示你使用以下步骤：

- 1. 输入 `./configure` 来运行一个检查你的系统配置并创建一个名为 `Makefile` 的文件——这是一个用于构建和安装软件包的 `make` 命令文件。（你可以输入 `./configure--` 来查看 `configure` 接受的选项列表。）

如果你遇到任何关于缺少包的错误，你必须安装缺失的包。使用你发行发行版的安装工具来添加缺失的包。例如，在 Debian 中使用 `apt-get install` 命令。在 Fedora Core 中，选择主菜单->系统设置->添加/删除应用程序。在 SUSE 中，使用 YaST GUI 工具。

- 2. 输入 `make` 来构建软件。

这一步会编译所有子目录下的源文件。（编译源代码会将每个源文件转换为对象文件——一个包含你的 PC 处理器可以理解的二进制指令的文件。）

- 3. 输入 `make install` 来安装软件。

这一步将库和可执行文件复制到系统中的相应目录。

尽管所有这些步骤都是针对 XMMS 的，但大多数其他软件包也遵循这些步骤：`configure`、`make` 和 `install`。`configure` 脚本会猜测依赖系统的变量，并创建一个包含构建和安装软件所需的命令的 `Makefile`。

通常情况下，你除了构建软件的命令外不需要做任何事情，但你必须在系统上安装软件开发工具。在 Fedora Core 中，你必须安装开发工具（Development Tools）和 GNOME 软件开发包。在 Debian 中，为了构建和运行 XMMS，你还必须安装 X 软件开发包，因为它是一个 X 应用程序。

### 从源文件构建软件包

安装 XMMS 后，尝试通过在终端窗口输入 `xmms` 从 GNOME 或 KDE 桌面启动它。在 XMMS 窗口中，按 `L` 打开“加载文件”对话框并选择一个 MP3 文件进行播放。你的 PC 必须有一个声卡，且声卡必须正确配置，以便 XMMS 运行。

XMMS 已经随 Fedora Core 提供，但该版本不包含播放 MP3 文件所需的插件。在构建新版本的 XMMS 后，你应该能够播放 MP3 文件。

总结来说，这里是你下载、解压、构建和安装典型软件包时遵循的步骤概述：

- 1. 使用 Web 浏览器从匿名 FTP 或网站下载源代码，通常是 `.tar.gz` 格式的文件。

- 2. 使用 `tar xzv filename` 命令解压文件。

- 3. 使用类似 `cd software_dir` 的命令切换到软件解压后的新子目录。

- 4. 读取任何 `README` 或 `INSTALL` 文件，以了解构建和安装软件必须遵循的任何特定指令。

- 5. 构建软件的细节在不同软件软件包之间可能略有不同，但通常你输入以下命令来构建和安装软件：

```bash
./configure
make
make install
```

- 6. 读取软件附带任何其他文档，以了解如何使用该软件以及在使用之前是否必须对其进行配置。

## 安装 SRPMS

如果你有 Fedora Core 的源码 CD（你可以从 `fedora.redhat.com/mirrors.html` 列出的任一站点下载源码 CD 镜像），你可以安装源文件并直接从源文件构建各种应用程序。Fedora 源代码文件也以 RPM 形式提供，就像可执行二进制文件一样，这些源码 RPM 文件通常被称为 SRPMS（源 RPM）。

要安装特定的源 RPM 并构建应用程序，请遵循以下步骤：

- 1. 通过输入 `mount /mnt/cdrom` 挂载 DVD-ROM，或者或等待 GNOME 桌面自动挂载 DVD。

- 2. 通常，源 RPM 位于 `SRPMS` 目录。输入以下命令切换到该目录：

```bash
cd /mnt/cdrom/SRPMS
```

- 3. 使用 `rpm -i` 命令安装源 RPM 文件。例如，安装到 Web 服务器 (httpd) 源码，输入：

```bash
rpm -ivh http*.src.rpm
```

文件安装在 `/usr/src/redhat/SOURCES` 目录下。一个带有 `.spec` 扩展名的 spec 文件被放置在 `/usr/src/redhat/SPECS` 目录下。spec 文件描述了软件并包含了构建和安装软件所需的信息。

- 4. 使用 spec 文件配合 `rpmbuild` 命令构建软件。通过使用 `rpmbuild` 命令的不同选项，执行从解压源文件到构建和安装二进制文件的不同任务。例如，要处理整个 spec 文件，输入：

```bash
rpmbuild -ba packagename.spec
```

此处 `packagename` 是 SRPM 的名称。此命令通常构建软件并安装二进制文件。

# 在线更新 Linux 应用程序
