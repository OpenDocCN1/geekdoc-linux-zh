
```
PAM-1.0
auth required pam_listfile.so item sense=deny
file=/etc/vsftpd.passwd users onerr=succeed
auth required pam_stack.so service=system-auth
auth required pam_shells.so
account required pam_stack.so service=system-auth
session required pam_stack.so service=system-auth
```

## 软件管理

由于 Red Hat 软件包管理器（`RPM`）的广泛使用，安装、卸载或更新软件包包一直是一个简单的过程。软件不再使用标准的 tar 归包，而是被封装在专门用于 `RPM` 的特殊归包中。`RPM` 归包包含了构成软件的所有程序文件、配置文件、数据文件，甚至是文档。通过一个简单的操作，Red Hat 软件包管理器就能为您安装所有这些内容。它还会检查该程序正确运行可能需要的任何其他软件包。您可以创建自己的 `RPM` 包。Red Hat 提供了 `redhat-config-packages` 来管理您的 `RPM` 包，安装新包以及更新或卸载您已有的包。`redhat-config-tools` 提供了一个易用的界面来管理软件包，让您能够轻松获取软件包的详细信息，包括其安装的文件的完整列表。

您可以使用 `Yum` 和 `APT` 仓库来更新 Red Hat Fedora Linux，例如 Red Hat Update 仓库（可以通过 Red Hat Update Agent `RHN` 访问，见第 4 章）。您还可以使用 `Yum` 工具从不同的 Red Hat 软件仓库（`linux.duke.edu/projects/yum`）下载。新版本可以从 `rpmfind` 的 BitTorrent 服务（`rpmfind.net/BitTorrent`）下载。

您还可以下载应用程序版本的源代码，并在系统上进行编译和安装。这个过程曾经很复杂，但随着 `configure` 脚本的引入已经显著简化。大多数当前的源代码（包括 GNU 软件）都附带一个 `configure` 脚本。该脚本会自动检测您的系统配置并生成一个 `Makefile`，它用于编译应用程序并创建一个与您的系统兼容的二进制文件。在大多数情况下，通过几次 `Makefile` 操作，您就可以在系统上编译并安装源代码。

### 软件仓库

您可以从许多在线源下载 Linux 软件。您可以找到针对特定类型应用程序（如 `GNOME` 和 `KDE`）的网站，特定发行版（如 Red Hat）的网站。Red Hat Network 可以自动下载和更新从构成 Red Hat 发行版的 `RPM` 包安装的软件。某些网站是 `RPM` 包仓库，例如 `rpmfind.net`，而另一些如 `freshmeat.net` 的网站则引导您前往原始站点。

| 表 29-1 | FTP 和 网站 | 应用程序 |

| :--- | :--- | :--- |

| Linux 软件网站 | `ftp.redhat.com` | 为 Red Hat 封装在 `RPM` 包中的软件 |

| | `freshmeat.net` | Linux 软件，包括 `RPM` |

| | `rpmfind.net` | `RPM` 包仓库 |

| | `freshrpms.net` | 定制化 `RPM` 包 |

| | `sourceforge.net` | Linux 开源软件包 |

| | `www.gnome.org` | `GNOME` 软件 |

| | `apps.kde.com` | `KDE` 软件 |

| | `rpmseek.com` | Linux 软件搜索网站 |

| | `www.filewatcher.org` | Linux FTP 站点监控器 |

| | `www.gnu.org` | GNU 归档 |

| | `www.ximian.com` | Xian Desktop，适用于 `GNOME` 的办公应用程序 |

大量的开源 Linux 项目可以在 `sourceforge.net` 找到。在这里，您可以找到软件的详细文档和最新版本的软件包。对于为 `GNOME` 桌面设计的应用程序，可以检查 `www.gnome.org`，可以在 `apps.kde.com` 找到 `KDE` 应用程序。对于特定的数据库和办公应用程序，您可以直接从公司网站下载软件包，例如用于 Oracle 数据库的 `www.oracle.com`。表 29-1 列出了几个流行的 Linux 网站。

### 软件包类型

Red Hat 和 `rpmfind.net` 等 `RPM` 网站上的软件包具有文件扩展名 `.rpm`。包含源代码的 `RPM` 包扩展名为 `.src.rpm`。其他软件包（如以源代码形式存在需要您编译的包）以各种压缩归包的形式出现。这些通常具有 `.tar.gz`、`.gz` 或 `.tar.bz2` 扩展名。本章后面将详细介绍。表 29-2 列出了您可以使用的各种 Linux 软件包常见的常见扩展名。

| 表 29-2 | 扩展名 | 文件 |

| :--- | :--- | :--- |

| Linux 软件包文件扩展名 | `.rpm` | 用 Red Hat 软件包管理器创建的软件包，用于 Red Hat、Caldera、Mandrake 和 SuSE 发行版。 |

| | `.src.rpm` | 应用程序源码版本的软件包，用 Red Hat 软件包管理器创建。 |

| | `.gz` | `gzip` 压缩文件（使用 `gunzip` 解压）。 |

| | `.bz2` | `bzip2` 压缩文件（使用 `bzip2` 解压，在 `tar` 中也使用 `j` 选项，例如 `xvzf`）。 |

| 表 29-2 Linux 软件包文件扩展名（续） | 扩展名 | 文件 |

| :--- | :--- | :--- |

| | `.tar` | 归档文件，使用 `tar` 的 `xvf` 提取 |

| | `.gz` | 压缩归档文件，使用 `gunzip` 解压并使用 `tar` 提取，在 `tar` 中使用 `z` 选项（如 `xvzf`）以一步完成解压和提取。 |

| | `.bz2` | `bzip` 压缩归档文件。使用 `tar -xvj` 提取。 |

| | `.tz` | 用 `compress` 命令压缩的归档文件。 |

| | `.z` | 用 `compress` 命令压缩的文件（使用解压命令解压）。 |

| | `.deb` | Debian Linux 包。 |

### Red Hat 软件包管理器 (RPM)

多个 Linux 发行版（包括 Red Hat、Mandrake、Caldera 和 SuSE）使用 `RPM` 将软件组织成可以自动安装、更新或删除的程序包。`RPM` 是一个命令行软件包管理系统，能够安装、卸载、查询和更新安装在 Linux 系统上的软件包。`RPM` 软件应用程序作为软件应用程序自身的安装程序运行。Linux 软件应用程序由多个需要安装在不同目录下的文件组成。程序本身最可能位于 `/usr/bin` 目录，手册文件在其他目录，库文件在另一个目录。此外，安装可能需要修改系统上的配置文件。`RPM` 软件包会为您完成所有这些任务。如果您以后决定不再某个特定应用程序，可以卸载以从系统中删除所有文件和配置信息。

### RPM 工具

要安装和卸载 `RPM` 包，您可以直接使用 `rpm` 命令。

### 第 29 章：软件管理

对于 `redhat-config-packages`，你可以使用文件管理器找到 `RPM` 文件并双击 `RPM` 包文件。在 `GNOME` 上，你也可以右键点击它，并选择“打开方式 | 安装软件包”，或者在 `KDE` 上，选择“安装软件包”。`redhat-config-packages` 会启动并检查所需的你可能需要的任何依赖包。它会为你安装该 `RPM` 包。

如果你正在使用 `rpm` 命令，应该使用 `-U` 选项来升级软件包。在下面的示例中，带有 `-U` 选项的 `rpm` 命令为 Emacs 安装升级：

```
# rpm -Uvh emacs-21.2-18.i386.rpm
```

### 命令行安装：rpm

如果你无法访问桌面，或者倾向于使用命令行界面，可以使用 `rpm` 命令来管理和安装软件包。`rpm` 是实际执行软件包安装、删除和查询的命令。事实上，`redhat-config-packages` 使用 `rpm` 命令来安装和删除包。`RPM` 包是软件文件的归档，包含了关于如何安装这些文件的信息。`RPM` 包的文件名以 `.rpm` 结尾，表示可以由 Red Hat 包管理器（`RPM`）安装的软件包。

### RPM 命令

通过 `rpm` 命令，你可以维护软件包、查询它们、构建你自己的包并验证你已有的包。维护软件包涉及安装新包、升级到新版本以及卸载软件包。`rpm` 命令使用一组选项来确定采取什么操作。此外，某些任务（如安装或查询软件包）有自己的选项，以进一步限定它们执行的操作类型。例如，`-q` 选项查询软件包，但当与 `-l` 选项结合时，它会列出该包中的所有文件。表 29-3 列出了 `rpm` 选项集。`rpm` 命令的语法如下（`rpm-package-name` 是你想要安装的软件包的名称）：
