
在激活 Livna 的情况下，你可以使用 PackageKit 下载并安装显卡驱动，并由“更新系统”提供自动更新。使用搜索框搜索 `fglrx` (ATI) 或 `NVIDIA`。你只需要使用初始唯一项 `kmod-fglrx`。`Yum` 会检测包名的其余部分，选择适用于你内核的包。对于 Nvidia，你可以在 PackageKit（添加/删除软件）中或在 `yum` 命令中使用 `kmod-nvidia`。`Yum` 将检测并选择 `xorg-x11-drv-nvidia`，即 Nvidia 驱动程序窗体。

或者，你也可以在终端中输入 `yum` 命令：

```
yum install kmod-fglrx
```

## 使用仓库

几个仓库提供了你通常需要的很多软件。Fedora 主仓库很可能包含你想要的软件。在尝试第三方仓库之前，请务要检查此仓库。某些特殊应用程序，如厂商提供的显卡驱动以及第三方多媒体支持，可以在 `rpm.livna.org/fedora` 找到。另一组多媒体支持包可以在 `rpm.livna.org` 找到。Java 应用程序位于 `jpackage.org`，尽管某些已经存在于 Fedora 仓库中。这些仓库共同构成了一组软件站点，你可以使用它们提供用户期望桌面系统的大部分功能。它们都符合 Yum 标准，其 Yum 配置文件为特定的 Fedora 版本设计。这里显示了这些站点及其仓库文件。

```
download.fedoraproject.org
download.fedora.redhat.com/pub/fedora/linux/releases
rpm.livna.org/fedora
freshrmps.net
jpackage.org
atprms.net
```

Fedora 仓库，镜像链接：符合 Fedora 标准的软件。`fedora.repo`

Fedora 仓库：符合 Fedora 标准的软件。`fedora.repo`

Livna：用于驱动、多媒体和其他 RPM 包的仓库，`lvn.livna.repo`

Freshrmps：驱动和多媒体应用的备用站点。`freshrmps.repo`

Java 应用程序。`jpackage.repo`

多媒体应用程序，`atprms.repo`

要查看可用软件包，你可以使用 Web 浏览器访问这些站点。Fedora 提供了 `repodata` 目录以供详细列表。Livna 提供了简单的目录文件列表，而 Freshrps 使用了详细的 Web 界面。Livna 包通过名称中的术语 `lvn` 进一步识别。由于这些站点支持 Yum，你只需点击按钮即可下载并安装包，以及任何支持库。这使得安装过程变得非常简单。

要在软件仓库上使用 Yum，必须配置 Yum 以访问它们。这只需列出站点的 URL（包括其 Web 地址和目录位置）即可。仓库配置放置在 Linux 系统 `/etc/yum.repos.d` 下的 repo 文件中。Fedora 的 repo 文件已经安装。在用 Yum 访问它们之前，你必须为 Livna 和 Freshrps 添加 repo 文件。然而，Livna 在网站上提供了一个名为 `livna-release-9-1.noarch` 的 RPM 包，安装后它会自动设置所需的 Yum 配置文件。对于 Livna 来说，这就是。

## 仓库 repo 包文件

要安装软件包，请使用 PackageKit、`yumex` 或 `yum` 命令。所有这些都会自动使用 repo 文件检查你已启用的仓库。该规则的一个重要例外是来自第三方仓库初始安装仓库配置文件。这些配置文件（repo 文件）通常包含在它们自己的 RPM 包中。你将使用 Web 浏览器直接从仓库网站下载并安装 repo 包。例如，Livna 第三方 Fedora 仓库的 repo 包 `livna-release-8.noarch.rpm`。你将直接使用 Web 浏览器下载并安装此包，确保选择提示的下载选项。

注意：过去存在——现在可能仍然存在——Livna 仓库和 Freshprms 仓库之间存在不兼容的情况。你应该使用其中一个。Livna 目前拥有最新的集合，应为首选。

## Fedora 仓库

Fedora 仓库已为 Yum 配置好。要下载任何 Fedora 包，只需使用 PackageKit 程序管理器（系统 | 管理 | 添加/删除软件），或在命令行输入带有 `install` 选项的 `yum` 命令。将检测到包以及任何依赖软件，并要求你确认安装。下载和安装将自动完成。检查 Fedora 仓库上的 `repodata` 文件以列出可用的 Fedora 文件。在相应版本的 `os` 目录下会有 `i386`、`x86_64` 64位以及用于 PowerPC 版本的 `ppc` 文件。然后你可以点击特定的包来显示其 RPM 包数据，显示版本信息、下载包的链接以及包开发网站。虽然你可以下载包，但最好是使用 Yum 或像 PackageKit 这样的 Yum 界面。

`repodata` 目录页面提供了多种方法来浏览极其丰富的 Fedora 包集合。页面首先列出新增和更新，然后为不同的包提供分组。这些组也作为链接列在左侧栏。如果你知道包的开头，可以使用右上角的“跳转到字母索引”，显示以该字母开头的包的页面。

当你第一次从 Fedora 仓库安装包时，系统会提示你安装 Fedora GPG 密钥，用于验证包。只需点击“是”来安装密钥即可。

要下载 Fedora 包，你应该使用 PackageKit（系统 | 管理 | 添加/删除软件）、`yumex`（应用程序 | 系统工具 | Yum 扩展器）或 `yum` 命令。在 PackageKit 上，“列表”或“搜索”视图将让你访问所有包，而不仅仅是组织在浏览类别中的包……或者，你可以在终端窗口中使用带有如文所示 `$install` 选项的 `yum` 命令。以下命令安装 Gnumeric：

```
yum install gnumeric
```

以下命令从 Fedora 仓库安装 KOffice：

```
yum install koffice
```

此处显示的 Fedora 仓库文件（repo）列出了几个仓库选项。名称为 Fedora，使用 `releaserver` 和 `basesearch` 来确定名称中的发布版本和架构部分。使用 `mirrorlist` 选项代替被注释掉的 `baseurl`。同样，使用 `releaserver` 来指定发布版本。使用的 gpg RPM-GPG-fedora 已经安装在 `/etc/pki/rpm-gpg` 目录中。

```
[fedora]
name=Fedora releaserver - $basesearch
failovermethod=priority
#baseurl=http://download.fedora.redhat.com/pub/fedora/linux/releases/$reaserver/Everything
mirrorlist=http://mirrors.fedoraproject.org/mirrorlist?repo=fedora-en=$basesearch
enabled=1
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-fedora file:///etc/pki/rpm-gpg/RPM-GPG-fedora
```

# 第 4 章：安装与更新软件

`livna-release-8.noarch.rpm`

你可以直接在终端窗口中使用 `rpm` 命令下载并安装此包。

```
rpm -ivh http://rpm.livna.org/livna-release-9.rpm
```

或者，你也可以通过浏览器并选择“打开方式”为“软件安装程序”来直接安装，或者下载后右键点击并选择“打开方式”“软件安装程序”。该包将列在 Livna 网页显示的 Fedora 发布版 Livna 分类中。

你也可以稍后使用此处所示的 `rpm` 命令安装：`rpm -ivh rpm.livna.org/livna-release-9.noarch.rpm`

要手动安装 GPG 密钥，可以使用以下命令：`rpm --import http://rpm.livna.org/RPM-LIVNA-GPG-KEY`

一旦安装了仓库，所有软件包都可以通过 Yum 访问。在 PackageKit 和 `yumex` 软件包列表中，你会发现名称中带有 `lvn` 术的软件包。

要查看 Livna 上有哪些可用软件包，请使用网络浏览器访问 `www.livna.org/fedora`。在这里，你会找到每个支持发行版的目录列表。选择你的仓库，然后选择你的架构，例如 `i386` (32位) 或 `x86_64` (64位)。在这里你将看到所有可用软件包的简单文件列表。

显示了由 `livna-release` 包安装的 `livna.repo` 配置文件的的一部分。配置指定了多个 `baseurl`，而不是镜像列表。`failovermethod` 选项指示了在选择站点时使用的顺序。它可以是 `priority`（优先级）、`sequence`（顺序）或 `round robin`（轮询）、随机。`livna.repo` 文件还包含一个测试配置，让你访问一些极少使用的软件包。
