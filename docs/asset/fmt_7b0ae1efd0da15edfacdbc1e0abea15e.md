
| `-r` 或 `--remove` | 移除软件包但保留配置文件 |

| `-P` 或 `--purge` | 移除软件包，包括配置文件 |

| `-p` 或 `--print-avail` | 显示有关已安装软件包的信息 |

###### 表 7.4 `dpkg` 主要操作*（续）*

| 操作 | 描述 |
| :--- | :--- |
| `-I` 或 `--info` | 显示未安装包文件的信息 |
| `-l pattern` 或 `--list pattern` | 列出所有名称匹配 `pattern` 的已安装包 |
| `-L` 或 `--listfiles` | 列出与包关联的已安装文件 |
| `-S pattern` 或 `--search pattern` | 查找拥有由 `pattern` 指定的文件的包 |
| `-C` 或 `--audit` | 搜索部分安装的包，并建议如何处理它们 |

###### 表 7.5 用于微调 `dpkg` 操作的选项

| 选项 | 配合使用的操作 | 描述 |
| :--- | :--- | :--- |
| `--root=dir` | 所有 | 使用位于 `dir` 的根目录来修改 Linux 系统。可用于维护一个与其他 Linux 安装相互独立的系统，例如在操作系统安装或紧急维护期间。 |
| `-B` 或 `--auto-deconfigure` | `-r` | 禁用依赖于正在被移除的包。 |
| `--force=things` | 多种 | 强制执行特定操作。有关此选项 `things` 详情的信息，请参阅 `dpkg` 的手册页。 |
| `--ignore-depends=package` | `-i`, `-r` | 忽略指定包的依赖信息。 |
| `--no-act` | `-i`, `-r` | 检查依赖、冲突及其他问题，而不会实际安装或移除包。 |
| `--recursive` | `-i` | 安装指定目录及所有子目录中匹配包名通配符的所有包。 |
| `-G` | `-i` | 如果已安装同一包的新版本，则不安装该包。 |
| `-E` 或 `--skip-same-version` | `-i` | 如果已安装相同版本的包，则不安装该包。 |

与 `rpm` 一样，`dpkg` 在某些情况下期望的是包名，而在其他情况下期望的是包文件名。具体来说，`--install` (`-i`) 和 `--info` (`-I`) 都需要包文件名，但其他命令使用较短的包名。

作为一个示例，请考虑以下命令，该命令安装了 `samba-common_3.0.28a-1ubuntu4.7_amd64.deb` 包：

```
# dpkg -i samba-common_3.0.28a-1ubuntu4.7_amd64.deb
```

如果您正在升级一个包，在安装新包之前可能需要移除旧包。为此，请使用 `dpkg` 的 `-r` 选项：

```
# dpkg -r samba
```

要查找已安装包的信息，请使用 `dpkg` 的 `-p` 参数，如清单 7.2 所示。此清单省略了包功能的扩展英文描述。

###### 清单 7.2: `dpkg` 包信息查询输出

```
$ dpkg -p samba-common

Package: samba-common

Priority: optional

Section: net

Installed-Size: 7112

Maintainer: Ubuntu Core Developers <ubuntu-devel-discuss@lists.ubuntu.com>

Architecture: amd64

Source: samba

Version: 3.0.28a-1ubuntu4.7

Replaces: samba (<< 3.0.20b-1)

Depends: debconf (>= 0.5) | debconf-2.0, libc6 (>= 2.4), libcomerr2w

(>= 1.33-3), libkrb53 (>= 1.6.dfsg.2), libldap-2.4-2 (>= 2.4.7), libncurses5w

(>= 5.6+20071006+3), libpam-modules, libpopt0 (>= 1.10), libreadline5w

(>= 5.2), libuuid1, ucf

Size: 3058414
```

基于 Debian 的系统通常使用一种称为 `dselect` 的高层次实用工具来处理包的安装和移除。`dselect` 实用工具提供了一个文本模式列表，显示已安装包和来自指定源（如 CD-ROM 驱动器或 FTP 站点）的可用包，并允许您选择要安装和移除的包。当您想要安装多个包时，此接口可能非常有用，但在仅操作一两个包时，`dpkg` 通常更方便。由于 `dpkg` 可以接受包文件名作为输入，因此它也是安装从非常规来源下载的包或自行创建的包的首选方法。

##### 使用 APT

Advanced Package Tool（高级包工具，APT）是 Debian 包管理的另一种选择。这些工具围绕 `apt-get` 实用工具展开，该工具使您能够轻松升级包，尤其是在您拥有快速互联网连接的情况下。基于 Debian 的系统包含一个文件 `/etc/apt/sources.list`，该文件指定了可获取重要包的位置。如果您从 CD-ROM 安装操作系统，并且其中包含包，则可能会有一些行位于文件顶部，被井号（`#`）注释掉，指示您可以从中获取更新包的 FTP 或 Web 站点目录。（如果最初进行的是网络安装，这些行可能未被注释。）

![](img/9903a4d3f7abd8dcbef1035fa04a3406_350_0.png)

> 虽然 APT 最常与 Debian 系统相关联，但也提供了针对基于 RPM 系统的移植版本。请访问 `http://apt4rpm.sourceforge.net` 获取有关此移植版本的信息。

`apt-get` 实用工具通过从 `/etc/apt/sources.list` 中列出的源获取可用包的信息，然后利用该信息升级或安装包来工作。其语法与 `dpkg` 类似：

```
apt-get [options] [package-names]
```

表 7.6 描述了 `apt-get` 命令，表 7.7 描述了最常用的选项。在大多数情况下，您实际上*使用* `apt-get` 时不会用到任何选项，只需一个命令和可能的一个或多个包名。该实用工具的一个特别常见用途是保持系统与任何新包同步。如果 `/etc/apt/sources.list` 包含指向最新文件存档 FTP 站点的指针，以下两个命令可以实现此目标：

```
# apt-get update
# apt-get dist-upgrade
```

###### 表 7.6 `apt-get` 命令

| 命令 | 描述 |
| :------- | :----------- |
| `update` | 从 `/etc/apt/sources.list` 中列出的安装源获取有关可用包的更新信息。 |
| `upgrade` | 基于本地存储的可用包信息，将所有已安装的包升级到最新版本。 |
| `dselect-upgrade` | 执行运行 `dselect` 后未完成的包状态变更（安装、移除等）。 |
| `dist-upgrade` | 类似于 `upgrade`，但执行“智能”冲突解决，以避免因破坏依赖关系而升级包。 |
| `install` | 通过包名（而非包文件名）安装包，从包含最新版本的源获取包。 |
| `remove` | 通过包名移除指定包。 |
| `source` | 使用 `/etc/apt/sources.list` 中列出的可用包信息和安装存档，通过包文件名检索最新可用的源包文件。 |
| `check` | 检查包数据库的一致性和损坏的包安装。 |
| `clean` | 执行维护工作，帮助清除 Debian 包数据库中关于已检索文件的信息。如果您不使用 `dselect` 进行包管理，请定期运行此命令以节省磁盘空间。 |
| `autoclean` | 类似于 `clean`，但仅移除不再可下载的包的信息。 |

###### 表 7.7 最常用的 `apt-get` 选项

| 选项 | 配合使用的命令 | 描述 |
| :----- | :----------------- | :--------- |
| `-d` 或 `--download-only` | `upgrade`, `dselect-upgrade`, `install`, `source` | 下载包文件但不安装它们。 |
| `-f` 或 `--fix-broken` | `install`, `remove` | 尝试修复依赖关系未满足的系统。 |
| `-m`, `--ignore-missing`, 或 `--fix-missing` | `upgrade`, `dselect-upgrade`, `install`, `remove`, `source` | 忽略所有无法检索的包文件（由于网络错误、文件缺失等原因）。 |
| `-q` 或 `--quiet` | 所有 | 省略一些进度指示信息。可以加倍使用（例如，`-qq` 产生更少的进度信息）。 |
| `-s`, `--simulate`, `--just-print`, `--dry-run`, `--recon`, 或 `--no-act` | 所有 | 模拟操作而不会实际修改、安装或移除文件。 |
| `-y`, `--yes`, 或 `--assume-yes` | 所有 | 在安装脚本中的任何是/否提示中产生“是”的响应。 |
| `-b`, `--compile`, 或 `--build` | `source` | 检索源包后对其进行编译。 |
| `--no-upgrade` | `install` | 使 `apt-get` 在已安装旧版本时不升级包。 |

![](img/9903a4d3f7abd8dcbef1035fa04a3406_352_0.png)

> 如果您使用 `apt-get` 自动升级系统上的所有包，您实际上是将系统的控制权交给了发行版维护者。虽然 Debian 或其他发行版维护者不太可能以这种方式试图侵入您的计算机，但在您最少监管的情况下进行自动更新很容易破坏系统上的某些东西，特别是如果您过去曾从非常规来源获取包。

APT 的图形用户界面前端 `Synaptic` 是可用的。它展示了可用包的列表；或者您可以使用搜索按钮缩小范围。当您找到想要安装或移除的包时，点击其名称左侧的方框。当您完成所有选择后，点击应用以使 `Synaptic` 进行更改。图 7.2 展示了 `Synaptic` 的使用。APT 套件还包括几个额外的工具，包括 `apt-key`、`apt-sortpkgs` 和 `apt-cache`。这些工具中的大多数都非常技术性；然而，`apt-cache` 有一个有用的搜索功能，通过搜索关键字激活，它搜索 APT 数据库的名称和描述。例如，输入 `apt-cache search samba` 会找到所有明确提到 Samba 的包。

314   第 7 章 • 软件包与系统备份的管理

图 7.2   `Synaptic` 为 APT 工具提供图形用户界面（GUI）。

![](img/9903a4d3f7abd8dcbef1035fa04a3406_353_0.png)

##### 处理 Tarball

所有发行版都可以使用 tarball——即通过 `tar` 工具收集在一起的文件，通常使用 `compress`、`gzip` 或 `bzip2` 进行压缩。与 RPM 和 Debian 软件包类似，tarball 可以包含源代码、二进制文件或与架构无关的文件（如文档或字体）。然而，这些文件缺少依赖信息，并且不维护已安装文件的数据库。因此，通过 tarball 安装的程序比通过 RPM 或 Debian 软件包安装的程序更难卸载。不过，Slackware 会维护一个数据库，记录通过 Slackware 的 tarball 和 Slackware 的 `pkgtool` 工具安装的文件。

###### `tar` 和 Tarball 的作用

`tar` 是一个多用途工具，最初是为将文件归档到磁带而创建的——其名称取自“tape archiver”（磁带归档器）。（接下来的“备份和恢复计算机”一节将更详细地描述 `tar` 的这一作用。）由于 Unix（进而 Linux）将硬件设备视为文件，像 `tar` 这样的磁带归档程序可用于在磁盘上创建归档文件。这些文件随后可以被压缩、复制到软盘或其他可移动介质、通过网络发送等。

在 Linux 世界中，tarball 扮演的角色与 Windows 世界中 `zip` 文件类似。但两者存在差异。`zip` 工具（包括 Linux 中的 `zip` 和 `unzip` 命令）先压缩文件，然后将其添加到归档中。相比之下，`tar` 不直接支持压缩，因此为了压缩文件，需要使用第二个工具（如 `gzip`、`bzip2` 或 `compress`）对生成的归档进行压缩。在 Linux 系统中，`gzip` 和 `bzip2` 程序最为流行，尽管 `compress` 仍用于某些旧的 Unix 系统。（`gzip` 工具可以解压旧的 `compress` 归档。）生成的文件可能有两个扩展名（如 `.tar.gz` 或 `.tar.bz2`），或者将双扩展名合并为单个三字符扩展名（`.tgz` 或 `.tb2`），以便在支持较长或多个扩展名受限的文件系统（如 DOS 的 FAT）上轻松存储。旧的 `compress` 归档使用大写 Z 扩展名，因此这些 tarball 具有 `.tar.Z` 扩展名。

作为一种软件包分发机制，tarball 主要被 Slackware 发行版使用，Slackware 是仍在通用中的最古老的重大 Linux 发行版之一。Slackware 摒弃花哨的配置工具，推崇简单实用的方式。在这方面，Slackware 类似于 Debian，但 Slackware 使用 `tar` 的自定义扩展方式来跟踪软件包的安装。如前所述，Debian 也使用源代码 tarball 作为其源代码软件包管理系统的一部分，但大多数管理员无需担心这一细节。

虽然大多数其他发行版不依赖 tarball，但任何发行版都可以使用它们。当您面临从源代码编译程序的任务时，tarball 特别有用，尤其是当您必须修改该源代码以适应您的系统时。接下来的“编译源代码”一节描述了如何编译以 tarball 形式提供的源代码软件。

二进制 tarball 包含预编译的程序。有时，tarball 包含的程序文件形式允许您直接将 tarball 解压到目标目录。例如，您可以切换到 `/usr/local` 目录并解压 tarball，使程序文件直接放入 `/usr/local/bin`、`/usr/local/man` 等位置。其他时候，您可能需要在临时目录中解压 tarball，然后运行安装工具来安装软件。

![](img/9903a4d3f7abd8dcbef1035fa04a3406_354_0.png)

> 如果您不确定如何继续进行 tarball 安装，请将其解压到临时目录，并查找说明。有时，您会在程序的网站或获取软件的 FTP 站点上找到单独的安装说明。

###### 使用 `tar` 命令

`tar` 程序是一个包含许多选项的复杂软件包。然而，您使用该工具所做的操作大多可以通过几个常用命令来覆盖。表 7.8 描述了主要的 `tar` 命令，表 7.9 描述了修改命令行为的限定符。每次运行 `tar` 时，您恰好使用一个命令，并且通常使用至少一个限定符。

**表 7.8** `tar` 命令

| 命令 | 缩写 | 描述 |
| --- | --- | --- |
| `--create` | c | 创建归档 |
| `--concatenate` | A | 将 `tar` 文件追加到归档中 |
| `--append` | r | 将非 `tar` 文件追加到归档中 |
| `--update` | u | 追加比归档中文件新的文件 |
| `--diff` 或 `--compare` | d | 将归档与磁盘上的文件进行比较 |
| `--list` | t | 列出归档内容 |
| `--extract` 或 `--get` | x | 从归档中提取文件 |

**表 7.9** `tar` 限定符

| 命令 | 缩写 | 描述 |
| --- | --- | --- |
| `--directory dir` | C | 在执行操作前更改到目录 `dir` |
| `--file [host:]file` | f | 使用名为 `host` 的计算机上名为 `file` 的文件作为归档文件 |
| `--listed-incremental file` | g | 执行增量备份或恢复，使用 `file` 作为之前归档文件的列表 |
| `--one-file-system` | 1 (仅在旧版本中可用) | 仅备份或恢复一个文件系统（分区） |
| `--multi-volume` | M | 创建或提取多磁带归档 |
| `--tape-length N` | L | 在 N 千字节后更换磁带 |
| `--same-permissions` | p | 保留所有保护信息 |
| `--absolute-paths` | P | 保留文件名中的前导 `/` |

**表 7.9** **`tar` 限定符***（续）*

| 命令 | 缩写 | 描述 |
| :--- | :--- | :--- |
| `--verbose` | v | 列出所有读取或提取的文件；与 `--list` 一起使用时，显示文件大小、所有权和时间戳 |
| `--verify` | W | 在写入后验证归档 |
| `--exclude` `file` | (无) | 从归档中排除 `file` |
| `--exclude-from` `file` | X | 从归档中排除 `file` 中列出的文件 |
| `--gzip` 或 `--ungzip` | z | 通过 `gzip` 处理归档 |
| `--bzip2` | j (某些旧版本使用 I 或 y) | 通过 `bzip2` 处理归档 |
