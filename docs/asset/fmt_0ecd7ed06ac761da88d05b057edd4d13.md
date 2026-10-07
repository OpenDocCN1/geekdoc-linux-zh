
“软件包”面板提供了缩小显示软件包范围的方法。你可以选择显示更新、已安装软件包或未安装的软件包。你可以进一步指定类别（例如存储库），仅显示来自特定存储库的软件包。点击软件包将在下方面板中显示其详细信息，你可以在该处选择描述、软件包包含的文件以及（如果可用）变更日志。

要选择软件包，只需勾选你想安装的项。一旦选中，软件包将会被添加到“处理队列”面板中。

![](img/6775ff646544702d90d6288b3c111705_97_0.png)

图 4-15：从 Livna 存储库访问的软件软件包

![](img/6775ff646544702d90d6288b3c111705_98_0.png)

图 4-16：Yum Extender

## 第 4 章：安装和更新软件

要查看可用的软件包，你可以使用网络浏览器访问相关站点。Fedora 提供了 `repodata` 目录用于详细列表。Livna 提供了简单的目录列表，而 Freshrpm 则使用详细的网页界面。Livna 软件包在名称中通过 `lvn` 术语进一步标识。由于这些站点支持 Yum，你可以点击按钮下载并安装软件包以及任何支持库。这使得安装过程变得非常简单。

要使用软件仓库，必须配置 Yum 以访问它们。这只需要列出站点的 URL，包括其 Web 地址和目录位置。仓库配置存放在你 Linux 系统的 `/etc/yum.repos.d` 下的 `.repo` 文件中。Fedora 的仓库已经安装。在通过 Yum 访问它们之前，你需要添加 Livna 和 Freshrpm 的 `.repo` 文件。Livna 在其网站上提供了一个名为 `livna-release-9.noarch` 的 RPM 软件包，安装后会自动设置所需的 Yum 配置文件。对于 Livna，这

### 仓库 repo 包包文件

要安装软件包，请使用 PackageKit、yumex 或 `yum` 命令。它们都会自动使用 `.repo` 文件检查你启用的仓库。此规则的一个重要例外是，仓库配置文件（`.repo` 文件）的初始安装通常包含在自身的 RPM 软件包中。你需要使用网络浏览器直接从仓库网站下载并安装 repo 包。例如，Livna 第三方 Fedora 仓库的 repo 包 `livna-release-9.noarch`。你可以直接使用网络浏览器下载并安装此包，并确保选择下载时的提示安装。

> 注意：过去在 Livna 仓库和 Freshrpm 仓库之间存在过（且现在可能仍然存在）不兼容的情况。你应该使用其中之一。Livna 目前拥有最新的收集集合，将会被优先考虑。

### Fedora 仓库

Fedora 仓库已为 Yum 配置好。要下载任何 Fedora 软件包，只需使用 PackageKit 软件包管理器（应用程序；添加/删除软件），或在命令行上使用带有 `install` 选项的 `yum` 命令。系统将检测软件包以及任何依赖软件，并询问你确认安装。下载和安装将自动完成。检查 Fedora 仓库上的 `repodata` 文件可以列出可用的 Fedora 文件。在相应版本的目录中会有一个，`i386.x86_64` 用于 64 位版本，`ppc` 用于 PowerPC 版本。然后你可以点击特定软件包显示其 RPM 数据，显示版本信息和下载软件包的链接，以及软件包开发网站。虽然你可以手动下载软件包，但最好使用 Yum 或像 PackageKit 这样的 Yum 界面。

`repodata` 目录页提供了多种方法来浏览极其丰富的 Fedora 软件包集合。第一页列出了所有最近的内容和更新，然后为不同的软件包提供分组。这些分组也列在左侧栏的链接中。如果你知道某个软件包的首字母，可以使用右上角的“跳转字母”索引，显示以该字母开头的软件包页面。

当你第一次从 Fedora 仓库安装软件包包时，系统会提示你安装 Fedora GPG 密钥，用于验证软件包身份。只需点击“是”安装密钥即可。

要下载 Fedora 软件包，你应该使用 PackageKit（应用程序 | 添加/删除软件）、`yum`（应用程序 | 系统工具 | Yum 扩展器）或 `yum` 命令。在 PackageKit 中，你可以通过其查找框访问所有软件包，而不仅仅是侧边栏列出的类别。或者，你可以在终端窗口中使用如所示带有 `install` 选项的 `yum` 命令。以下命令安装 `gnumeric`：

```bash
yum install gnumeric
```

以下命令从 Fedora 仓库安装 `KOffice`：

```
yum install koffice
```

这里显示的 Fedora `.repo` 文件列出了若干个仓库选项。名称为 `Fedora`，并使用 `releasever` 和 `basearch` 来确定名称中的版本和架构部分。`mirrorlist` 选项取代了 `baseurl`（后者被注释掉了）。同样，使用 `releasever` 来指定版本。`gpgkey` 即 `RPM-GPG-KEY-Fedora` 已经安装在 `/etc/pki/rpm-gpg-directory` 中。

```
[fedora]
name=$releasever - $basearch
failovermethod=priority
#baseurl=http://download.fedora.redhat.com/pub/fedora/releases/$releasever/Everything/$os/
mirrorlist=http://mirrors.fedoraproject.org/mirrorlist?repo=fedora-$releasever&arch=$basearch
enabled=1
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-Fedora file
```

### Livna

`http://rpm.livna.org` 为许多软件包提供了站点门户，包括像 MPlayer 等多媒体应用，以及由于许可问题未包含在 Fedora 中的软件。几个热门软件包包括 ATI 和 NVIDIA 显卡驱动程序。Livna 专门负责配置不同的驱动程序以兼容 Fedora。例如，你可以直接从 Livna 网站下载 NVIDIA 驱动程序并尝试在你的系统中安装。作为替代方案，Livna 提供了一个已经为 Fedora 配置好的驱动程序版本。更安全更可靠的方法是直接安装 NVIDIA 驱动程序的 Livna 软件包。Livna 还提供了 ATI 驱动程序包 (`fglrx`)。

要配置你的系统访问 `rpm.livna.org`，只需在 `/etc/yum.repos.d` 目录下安装 `livna-release` 配置文件，并下载 Livna GPG 密钥。软件包的名称将类似于

```
livna-release-9.noarch
```

或者，你可以通过浏览器选择“软件安装程序”来安装它。软件包名称将类似于

```
livna-release-9.noarch
```

要手动安装 GPG 密钥，你需要使用以下命令：

```
rpm --import http://livna.org/GPG-KEY
```

一旦仓库安装，所有软件包都可以通过 Yum 访问。你会在 PackageKit 和 yum 列表中找到名称带有 `livna` 术语的包。

要查看 Livna 上有哪些可用软件包，请使用网络浏览器访问 `www.livna.org/fedora`。在这里你会找到每个版本的目录列表。选择你的版本目录，然后选择架构，例如 `i386` (32位) 或 `x86_64` (64位)。在这里你会看到所有可用软件包的简单列表。

这里显示了由 `livna-release` 安装的仓库配置文件的一部分。该配置指定了多个站点而不是镜像列表。`failovermethod` 指明了选择时使用的顺序。它可以是优先级（priority）、顺序（sequence）或轮询（random）。`livna.repo` 还持有一个测试配置，允许你访问新的更新软件包。

```
[livna]
name=Livna for Fedora Core $releaser=$base
baseurl=
http://livna.org/fedora/$baseurl/
http://livna.cat.pks.edu/fedora/$baseurl/
http://wftp.tu-chemitz.de/pub/livna/fedora/$baseurl/
http://ftp-stud.fht-esslingen.de/pub/Mirrors/rpm.livna.org/fedora/$base/
http://mirror.atrpm.net/livna/fedora/$releaser=$base/
http://tummy.com/pub/livna.org/fedora/$releaser=$base/
failovermethodpriority
#mirrorlist=http://rpm.livna.org/mirrorlist-7
enabled=1
gpgcheck=1
gpgkeyfile=/etc/pki/rpm-gpg/RMP-GPG-KEY-livna
```

### Freshrmps

Freshrmps 提供了许多多媒体软件包，但没有显卡驱动程序。它提供了一种为你的系统动态编译内核模块模块的方法。如果你在使用 Livna，则不应使用 Freshrmps。你不应该混合使用 Livna 和 Freshrmps 仓库软件包，它们可能不兼容。

下载并安装 freshprms，请使用 `freshprms-release` 软件包。在 `www.freshprms.net` 网上有一个直接链接。在 `ay.freshprms.net` 也可以找到该包的链接。点击 Fedora 链接将列出 Fedora 的 freshprms-release 软件包。你需要的包类似于：

```
freshprms-release-1.1-2-fc.noarch.rpm
```

### atprms

对于 atprms，你将需要创建自己的 repo 文件。内容列在 `http://atprms.net/install.html` 的 yum 部分。你可以将这些内容复制并粘贴到你的文本编辑器中，并将文件保存为 `atprms.repo`。将此文件保存在 `/etc/yum.repos.d` 目录下。这里显示了 atprms-repo 文件的有效内容。对此文件的一个有用更改是将 GPG 密钥指定为一个文件，位于 `/etc/pki/rpm-gpg` 目录。使用此 GPG 密钥后，就不需要在网站上引用它了。

```
[atprms]
name=Fedorareleaser - Atprms
baseurl=http://atprms.net/$f/releaser-$basearch-atprms/stable
### gpgkey=http://ATprms.net/RPM-GPG-KEY.atprms
gpgfile=file:///etc/pki/rpm-gpg/RPM-GPG-KEY.atprms
enabled=1
gpgcheck=1
```

`gpgkey` 是 `RPM-GPG-KEY-atprms`，位于 `http://ATprms.net/RPM-GPG-KEY`。你可以一次性完成安装和下载，但你可能想将该文件保存到第一个 `/etc/pki/rpm-gpg` 目录，并从那里导入它。你可以通过在浏览器中右键点击 atprms 安装页面上的链接进行下载，或者像这里所示在终端中使用 `wget`。

`wget http://ATprms.net/RPM-GPG-KEY.atprms` 下载到 `/etc/pki/rpm-gpg` 目录。

请确保导入密钥。

```
rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY.atprms
```

### 额外的 Java ：jpackage.org

虽然 Fedora 包含了大量的 Java 软件集合，但你可以从 `http://jpackage.org` 下载额外的 Java 应用程序。只需使用你的 yum 仓库获取 Java 包即可。请记住，`jpackage.org` 不提供 JRE。你必须从 Sun 下载并安装。此外，`jpackage.org` 上的开发包是商业性的。

首先下载并安装 `jpackage.repo`。先将 `jpackage.repo` 放在 `/etc/yum.repos.d` 中。检查该仓库是否已为你的特定 Fedora 版本设置好。如果没有，你将使用通用版本。使用 `enabled` 选项来激活或停用某个版本。默认将设置为通用版本。

软件包将显示在 PackageKit（列表或搜索视图）中。它们的标识符为 `jpp`。

针对不同 Linux 发行版的 Jpack repo 文件配置显示在 `www.jpackage.org/yum.php`。在这里你可以找到最新 Fedora 发行版的列表。你也可以下载通用版本，它将启用 Fedora。这里列出了一个 `jpackage.repo` 示例。像 Fedora 一样，它使用了镜像列表（mirrorlist）。`gpgkey` 位于 `http://www.jpackage.org/yum.asc`。由于许可限制，Jpackage 无法自由发布 JDK 等开发工具。你必须从 Jpackage 进行商业购买。JRE 也是非免费 Java 包的一部分。

如果你下载了 `generic_repo` 文件，你将发现 Fedora 的仓库列表。…… 免费和非免费仓库也已启用。禁用不适用于你发行版的那个。在 Fedora 的泛用配置中使用的镜像列表在之前的 Fedora 示例中显示过，尽管它被注释掉了。

### Yum 配置

Yum 选项在 `/etc/yum.conf` 文件中配置，`/etc/yum.repos.d` 目录持有列出可用 Yum 仓库的仓库文件（repo）。仓库文件的扩展名为 `.repo`。检查 `yum.conf` 文件以查看项格式中的 Yum 选项列表。`yum.conf` 文件由由括号括的头部分隔的不同段落组成，第一个始终是主段（main）。之后可以跟 Yum 服务器仓库，从括号括围的仓库标签开始。然而，在 Fedora 上，这些目前放置在 `/etc/yum.repos.d` 目录下的独立仓库文件中。

```
[main]
cachedir=/var/cache/yum
keepcache=0
debuglevel=2
logfile=/var/log/yum.log
tolerant=1
exactarch=1
obsolete=1
gpgcheck=1
plugins=1
metadata_expire=1800
installonly_limit=2
```

```
### 将你的 REPOS 放在这里或命名为 file.repo 的独立文件中
### 在 /etc/yum.repos.d
```

### /etc/yum.conf

`yum.conf` 文件将只有带有 Yum 选项设置的主段。有一些通用的 Yum 选项，如 `logfile`（列出 Yum 日志的位置）和 `distroverpkg`（用于确定使用哪个发行版本）。软件包将下载到 `cachedir` 选项指定的目录，在本例中为 `/var/cache/yum`。你可以选择保留下载的软件包或在安装后删除它们。`tolerant` 选项允许软件包安装错误，`retries` 选项指定了访问软件包的次数。`exactarch` 和 `obsolete` 都适用于由 `yum update` 命令调用的 Yum 更新过程。`tolerant` 选项将允许软件包错误。

您在其中需要的软件包。然后只需为它提供一个配置文件并指定其位置即可，非常简单。

### 管理 Yum 缓存

启用 `keepcache` 选项后，Yum 将其下载的软件包保留在 `/var/cache/yum` 目录下。如果您想保存或复制任何特定的软件包，可以在那里找到它们。缓存让您能够轻松卸载和重新安装软件包，而无需重新下载。软件包将保留在缓存中。如果禁用了缓存，软件包在安装后将自动删除。

您的缓存可能会迅速增大，因此您可能需要经常清理它。如果您刚刚删除了这些软件包（因为它们已经安装），可以使用 `clean packages` 选项。

```
yum clean packages
```

Yum 还维护了一个软件包头文件列表，其中包含所有下载软件包的信息。这些头文件用于更新您的系统，显示已安装哪些内容。您可以选择使用 `clean headers` 选项移除头文件。

如果您想让 Yum 访问缓存中的软件包，可以使用 `-C` 选项。以下列表仅列出缓存中的软件包。

```
yum -C list
```

### 使用 rpm 手动安装软件包

如果您要安装的不是 Yum 仓库的软件包，且您没有桌面访问权限或倾向于从命令行界面工作，可以使用 `rpm` 命令来管理和安装软件软件包（您可以通过选择“应用程序 | 系统工具”菜单中的“终端”来打开终端窗口）。某些情况下您将不会使用 `rpm` 命令。大多数软件现在位于 Yum 支持的 Fedora 仓库中。您将使用 `yum` 命令或 PackageKit（添加/删除软件）前端来安装您的软件包。Yum 的优势是可以自动安装任何依赖包，而 `rpm` 命令虽然会检测新软件包，但不会安装它们。您必须按照正确的顺序单独安装任何软件包。

对于不属于 Yum 支持仓库且依赖包很少或没有依赖包的软件包，您可以直接使用 `rpm` 命令。您还可以使用 `rpm` 命令跳过 Yum，强制安装特定软件包而不是通过 Yum 仓库（Yum 的 `localinstall` 选项可以实现相同目的，或者在 PackageKit 仓库管理器中仅选择“安装 DVD”）。

`rpm` 命令执行软件软件包的安装、删除和验证。每个软件软件包实际上是一个 RPM 软件包，由软件文件归包和有关如何安装这些文件的信息组成。每个归包作为一个单一文件存在，文件名以 `.rpm` 结尾，表示它是由 Red Hat 软件包管理器安装的软件软件包。
