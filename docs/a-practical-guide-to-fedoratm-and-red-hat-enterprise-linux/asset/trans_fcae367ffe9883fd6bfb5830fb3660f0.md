

您可以使用 `yumdownloader` 的 `--source` 选项来下载 RPM 源代码包文件。**yumdownloader** 工具会自动启用所需的源代码仓库。请参阅第 582 页，其中提供了一个示例，用于在工作目录中下载本地系统所安装发行版内核源代码最新版本的 RPM 文件。如果没有 `--source` 选项，**yumdownloader** 将下载可执行 RPM 文件。请参阅第 549 页了解有关安装此类文件的信息。

![](img/243613168ac865b539f12460d966088e_597_0.png)

## yum.conf：配置 yum

您不需要配置 **yum**：默认安装后，它已准备好可以使用。本节面向希望修改配置文件的 **yum** 用户，描述了 **yum** 的配置文件。主要配置文件 `/etc/yum.conf` 包含全局设置。在 Fedora/RHEL 发行版中，`/etc/yum.repos.d` 目录中的文件定义了仓库。以下是默认的 yum.conf 文件：

```bash
$ cat /etc/yum.conf
[main]
cachedir=/var/cache/yum/$basearch/$releaseserver
keepcache=0
debuglevel=2
logfile=/var/log/yum.log
exactsarch=1
obsoletes=1
gpgcheck=1
plugins=1
installonly_limit=3
...
# PUT YOUR REPOS HERE OR IN separate files named file.repo
# in /etc/yum.repos.d
```

标记为 `[main]` 的部分定义了全局配置选项。`cachedir` 指定了 **yum** 存储已下载包的目录，但由于 `keepcache` 设置为 0，**yum** 在安装完这些包后不会保留它们。记录的信息量由 `debuglevel` 指定，值为 10 时生成最详细的信息。`logfile` 指定了 **yum** 保存日志的位置。

将 `exactsarch` 设置为 1 会导致 **yum** 仅使用相同架构的包来更新软件包，从而防止例如 i686 包替换 i386 包。您可以使用 `retries` 来指定 **yum** 在返回错误之前尝试获取文件的次数（默认值为 10）。将此参数设置为 0 可使 **yum** 持续尝试直到成功。

将 `obsoletes` 设置为 1 会导致 **yum** 在更新软件包时替换已废弃的包；当您安装软件包时，此设置不起作用。当 `gpgcheck` 设置为 1 时，**yum** 会检查其安装的软件包上的 GPG（第 1160 页）签名。此检查验证了软件包的真实性。将 `plugins` 设置为 1 会启用 **yum** 插件，从而扩展 **yum** 的功能。`metadata_expire` 参数指定了 **yum** 使用元数据（关于它从仓库下载的包）的秒数（如果数值后跟 m，则为分钟），然后它会再次下载该信息。此参数默认为 6 小时。

虽然 **yum** 配置信息的其余部分（指定 **yum** 仓库的内容）可以出现在 `yum.conf` 文件中，但 Fedora/RHEL 将此信息放在 `/etc/yum.repos.d` 中。

**可选**   有些软件包应当仅被安装，而不被更新。`/etc/yum.conf` 中的参数 **installonlypkgs** 用于标识这些软件包。与内核相关的软件包默认属于 **installonlypkgs**：通常您不希望更新内核；而是希望安装一个新的，同时保留旧的以防需要。**installonly_limit** 参数指定了 **yum** 保留的 **installonlypkgs** 软件包的版本数量。更多信息请参阅 `yum.conf` 手册页。

## YUM 仓库

正如 `/etc/yum.conf` 中所述，Fedora/RHEL 将每个仓库的信息存储在一个单独的 `/etc/yum.repos.d` 目录下的文件中：

```bash
$ ls /etc/yum.repos.d
fedora.repo  fedora-updates.repo  fedora-updates-testing.repo
```

在这些文件之一中设置的参数会覆盖 **[main]** 部分（在 `yum.conf` 中）设置的相同参数。这些文件中的每一个都包含一个标头，例如 **[fedora]**，它为仓库提供了一个唯一的名称。文件名通常类似于仓库名称，并加上 `fedora-` 前缀和 `.repo` 文件扩展名。常用仓库包括 `fedora`（存储在 `fedora.repo` 文件中），它包含安装介质上存在的软件包（稳定软件包）；`updates`（存储在 `fedora-updates.repo` 文件中），它包含稳定软件包的更新版本；以及 `updates-testing`（存储在 `fedora-updates-testing.repo` 文件中），它包含尚未准备好发布的更新。最后一个仓库默认未启用；除非您正在测试不稳定软件包，否则请勿启用它。切勿在生产系统上启用 `updates-testing` 仓库。

**可选**   每个 *.repo* 文件包含几个相关仓库的规范，这些仓库通常是被禁用的。例如，`fedora.repo` 文件除了包含 [fedora] 外，还持有 [fedora-debuginfo] 和 [fedora-source]。您不能使用 **yum** 下载源代码文件。相反，请使用 **yumdownloader**（第 540 页）来完成此任务。

下一个示例展示了 `fedora.repo` 文件的一部分，该部分指定了 fedora 仓库的参数：

```bash
$ cat /etc/yum.repos.d/fedora.repo
[fedora]
name=Fedora $releasever - $basearch
failovermethod=priority
#baseurl=http://download.fedoraproject.org/pub/fedora/linux/releases/$releasever/Everything/$basearch/os/
#mirrorlist=https://mirrors.fedoraproject.org/metalink?repo=fedora-$releasever&arch=$basearch
enabled=1
metadata_expire=7d
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-fedora-$basearch
...
```

每个仓库规范文件包含用括号括起来的仓库名称（{}）、**name**、**failovermethod**、**baseurl** 和 **mirrorlist**。**name** 提供了 `yum` 显示的仓库非正式名称。**failovermethod** 决定了如果第一个镜像站点失败，`yum` 联系初始镜像站点和额外镜像站点的顺序；**priority** 按出现的顺序选择站点，而 **roundrobin** 随机选择站点。**baseurl** 指示主仓库的位置；默认情况下它是被注释掉的。**mirrorlist** 指定包含 baseurls（即主仓库的镜像）列表的文件 URL。一次只能启用 **baseurl** 或 **mirrorlist** 其中之一。这些定义使用两个变量：`yum` 将 `$basearch` 设置为系统架构（例如 i686），将 `$releasever` 设置为发行版版本（例如 Fedora 15 的 15）。

如果 **enabled** 设置为 1，则文件描述的仓库处于启用状态（`yum` 将使用它）；如果 **enabled** 设置为 0，则处于禁用状态。**metadata_expire** 指定 `yum` 认为元数据有效的时间长度：在此时间段后，`yum` 会下载新的元数据。默认为六小时。如前所述，**gpgcheck** 决定 `yum` 是否检查其下载文件上的 GPG 签名。**gpgkey** 指定 GPG 密钥的位置。更多选项请参阅 **yum.conf man** 页。

### 添加仓库

有许多软件包仓库。如需更多信息和仓库列表，请访问 fedoraproject.org/wiki/Third_party_repositories。您还可以在互联网上搜索 **fedora repositories**。这些站点中最有趣的一个是 repos.fedorapeople.org。这些站点为其仓库提供仓库规范文件。通过将仓库规范文件放置在 /etc/yum.repos.d 目录中，即可向本地系统添加仓库，但请留意以下安全提示。

### 使用您信任的仓库

#### 安全

> 在添加到系统的仓库中要有选择性：当您添加一个仓库时，您正在信任运行该仓库的人不会在您下载的软件包中放入恶意软件。此外，不受 Fedora/RHEL 支持的软件包可能会与其他软件包冲突，并/或导致升级失败。

### BitTorrent

下载 BitTorrent 文件最简单的方法是点击网络浏览器或 Nautilus 文件浏览器中的 torrent 文件对象；此操作会打开运行 `transmission` BitTorrent 客户端的图形界面。本节描述了 BitTorrent 的工作原理，并解释了如何从命令行下载 BitTorrent 文件。

BitTorrent 协议实现了一种混合的客户端/服务器和 P2P（第 1265 页）文件传输机制。BitTorrent 有效地分发大量静态数据，例如 Fedora/RHEL 安装 ISO 镜像。它可以替代如匿名 FTP 等协议，在这些协议中不需要客户端身份验证。每个下载文件的 BitTorrent 客户端都提供额外的带宽用于上传该文件，从而减轻初始源的压力。通常，BitTorrent 下载速度比 FTP 下载更快。与 FTP 等协议不同，BitTorrent 将多个文件组合成一个单一的软件包：一个 BitTorrent 文件。

