
# 第 28 章：软件管理

Red Hat 和 rpmfind.net 等 RPM 软件包上的软件包将具有扩展名 `.rpm`。包含源码的 RPM 软件包扩展名为 `.src.rpm`。其他软件包（例如你需要编译的源码形式的包）则以各种压缩归档的形式存在。这些通常具有 `.tar.gz` 或 `tar.bz2` 扩展名。本章稍后将进行详细说明。表 28-2 列出了你在各种 Linux 中会找到。

RPM 维护一个已安装软件的数据库，跟踪所有文件。这让你能够使用 RPM 卸载属于。

要安装和卸载 RPM 软件包，你可以使用命令行中的 `rpm` 命令、发行版管理工具（如 Mandrake Software Manager 或 SuSE 的 Yast Control Center），或任何可用的基于窗口的 RPM 工具，如 Package。你应该从特定的发行版下载 RPM，但许多 RPM 软件包设计用于任何系统。许多这些包的名称中包含 `noarch`。你可以在 rpm.org 了解更多关于 RPM 的信息。

RPM 软件包的命名规范随发行版而异。在 Red Hat 上，包名包含了包版本以及平台（Intel PC 为 i386）和 `.rpm` 扩展。红 Hat RPM 软件包的示例所示：

```
kernel-2.4.18-13.i386.rpm
```

Mandrake 对 RPM 软件包使用了略不同的命名格式，包含了 `mdk` 项。

```
kernel-2.4.18-13mdk.i686.rpm
```

SuSE 使用简单的命名格式。软件包位于不同的子目录下。

DVD-ROM 或发行版 CD-ROM 上的 RPM 软件包仅代表 Linux 软件的一小部分。一个丰富的 RPM 仓库也位于 http://rpmfind.net/linux/RPM。这里的软件包按发行版、组和名称索引。它包含了每个发行版的包，包括 Red Hat。从 http://rpmfind.net，你可以下载 `rpmfind` 命令，它允许你搜索 RPM 软件包，是在本地系统还是 rpmfind.net 上的 RPM 仓库。你可以使用 `rpmfind` 下载和更新软件包。rpmfind 会检测你的系统发行版并列出相应的 RPM 包。通过 `--appropos` 选项，你可以使用更通用的术语来定位一个包，而不是文件名模式。通过 `--upgrade` 选项，你可以下载并安装已安装包的更新版本。`rpmfind` 命令还会创建一个 `.rpmfind` 配置文件，你可以在其中指定此类功能，例如下载目录、搜索的远程服务器以及系统中本地 RPM 包的位置。

> 带有 noarch 术语的 RPM 软件包用于架构无关的包。这意味着它们被设计为安装在任何 Linux 发行版上。不带 noarch 的包可能取决于发行版，设计为安装在特定的发行版上，如 Caldera、Mandrake 或 SuSE。

你可以将这些包放在系统中的某个目录下，然后使用 rpm 或 GUI 工具进行安装。通常情况下，你应该始终尝试使用为你的发行版设置的 RPM 软件包版本。在许多情况下，尝试安装为其他发行版设计的 RPM 软件包可能会失败。这里列出了常用的 RPM 包管理器：

- Kpackage RPM 软件包管理器
- GnomeRPM GnomeRPM 软件包管理器
- rpm 管理 RPM 软件包的 shell 命令

## K 桌面包管理器：Kpackage

KDE 桌面提供了一个强大且易用的 RPM 软件包管理器，称为 Kpackage。只要你的系统中安装了 K Desktop，你就可以在任何窗口管理器或桌面（包括 Gnome）下运行 Kpackage。你可以通过在 K 菜单实用菜单中选择其项或在终端窗口中输入 `kpackage` 命令来启动 Kpackage。

Kpackage 的右侧包含两个面板：一个用于属性（Properties），另一个用于文件列表（File List）。属性面板显示当前所选 RPM 软件包的软件信息，包括版本号和作者。文件列表列出了软件包中包含的所有文件，包括 README 文件。如果你在 K Desktop 上使用 Kpackage，可以点击文件列表中的任何文件，它将由文本编辑器显示。这是读取安装文件（如 README 或 install 文件）的方便方法。要卸载包，选择它并点击“卸载”（Uninstall）。

## GnomeRPM

GnomeRPM 为在你的 Gnome 上管理 RPM 软件包提供了一个高效且易用的界面。只要你的系统中安装了 Gnome，它就可以运行在任何窗口管理器上。GnomeRPM 窗口显示两个窗格，左侧显示不同已安装 RPM 软件包类别的树形列表。展开一个类别可以在右侧窗格中显示相应的包。你可以通过选择包并点击图标栏中的卸载图标来查询包，或者通过右键点击它并在弹出菜单中选择“卸载”（Uninstall）。你也可以使用相同的方法来查询包以及显示信息和文件列表。GnomeRPM 还具有一个查找（find）实用程序，你可以用它轻松定位 RPM 包。在查找窗口中，你可以查询或卸载该包。要用 GnomeRPM 安装新包，点击“安装”（Install）图标。这会打开一个显示要安装的选中包的窗口。然后点击“添加”（Add）来打开一个在系统中查找包的窗口。你可以添加任意数量的包。点击“安装”（Install）来安装这些包。要升级已安装的包，点击“升级”（Upgrade）并按照步骤操作。

在 Gnome 上，如果你只想知道某个包是什么，以及该包中的文件列表，可以右键点击该包并选择“显示信息”（Show Info）条目。打开的窗口将显示软件描述以及包中所有文件的列表。还有按钮可以让你安装或升级软件。

## 更新软件

如第 4 章所示，你可以使用发行版代理（如 Red Hat Network、Mandrake 的软件管理器或 SuSE 的在线更新）自动更新你的 Linux 系统。你也可以使用 FTP 客户端、Web 浏览器或 Gnome 或 KDE 文件管理器手动下载包，然后使用 `rpm` 命令安装软件。你还可以使用 Kpackage 或 Gnome RPM 直接访问发行版的 FTP 站点，下载包并自动安装到你的系统中。只需在位置框中输入该站点的 FTP URL 即可。

对于 rpm 命令，你使用 `-U` 选项来升级包。在以下示例中，带有 `-Uvh` 选项的 rpm 命令升级 emacs：

```
$ rpm -Uvh emacs-21.2-2.i386.rpm
```

使用 Webmin 或 Linuxconf 也可以软件安装。从“软件包”（Software Packages）页面，你可以查看已安装的包或安装新包，还可以搜索包。

## 命令行安装：rpm

如果你无法访问桌面，或者更倾向于从命令行界面工作，可以使用 `rpm` 命令来管理和安装软件包。`rpm` 是实际执行软件包安装、删除和查询的命令。事实上，GnomeRPM 和 Kpackage 使用 `rpm` 命令来安装和删除包。RPM 包是软件文件的归档，包含了关于如何安装这些文件的信息。RPM 包的文件以 `.rpm` 结尾，表示可以由 Red Hat 包管理器安装的软件包。

通过 `rpm` 命令，你可以维护包、查询包、构建自己的包并验证已有的包。维护包涉及安装新包、升级到新版本以及卸载包。`rpm` 命令使用一组选项来确定采取的操作。此外，某些任务（如安装或查询包）有自己的选项，以进一步限定它们执行的操作类型。例如，`-q` 选项用于查询包。

### 表 28-3. Red Hat 包管理器 (RPM) 选项

| 操作模式 | 效果 |
| :--- | :--- |
| **查询选项（与 -q 一起使用）** | |
| `-qf filename` | 查询拥有该文件的包。 |
| `-qr` | 列出此包依赖的包。 |
| `-qp package-name` | 查询未安装的包。 |
| `-qi` | 显示所有包信息。 |
| `-ql` | 列出包中的文件。 |
| `-qd` | 列出包中的文档文件。 |
| `-qc` | 列出包中的配置文件。 |
| `-q --dump` | 列出详细信息。 |
| **通用选项（可与任何选项一起使用）** | |
| `-vv` | 调试；显示所有采取的操作。 |
| `--quit` | 仅显示错误消息。 |
| `--version` | 显示 rpm 版本号。 |
| `-help` | 显示帮助信息。 |
| `--root` | 使用目录作为所有操作的顶级目录（而不是 root）。 |
| `--dbpath` | 使用指定目录下的 RPM 数据库。 |
| `--dbpath cmd` | 将 RPM 的输出传递给 cmd。 |
| `--rebuilddb` | 重建 RPM 数据库；可与 -root 和 -dbpath 使用。 |
| `--initdb` | 构建新的 RPM 数据库；-root 和 -dbpath 选项。 |
| **其他信息来源** | |
| RPM-HOWTO | 更详细的信息，特别是关于如何构建自己的 RPM 包。 |
| Man rpm | 选项的详细列表。 |

### 表 28-3. Red Hat 包管理器 (RPM) 选项（续）

| 操作模式 | 效果 |
| :--- | :--- |
| **卸载选项（与 -e 一起使用）** | |
| `--test` | 测试卸载。不删除，只检查哪些内容会被删除。 |
| `--nodeps` | 不检查依赖关系进行卸载。 |
| `--allmatches` | 移除包的所有版本。 |
| **查询选项（与 -q 一起使用）** | |
| `package-name` | 查询包。 |
| `-qa` | 查询所有包。 |

你使用 `-i` 选项安装新包，使用 `-U` 选项将已安装的包升级到新版本。使用 `-e` 选项时，rpm 卸载包。`-q` 选项告诉你包是否已安装，而 `-qa` 选项显示所有已安装包的列表。将此输出通过到分页器程序（如 `more`）是最佳做法。

```
rpm -qa | more
```

在下一个示例中，用户检查系统中是否已经安装了 Mozilla。注意，不需要 RPM 归档的完整文件名。如果该包已安装，你的系统已经注册了它的名称及其所在位置。

```
rpm -q mozilla
mozilla-1.0rc3-0
```

请记住已安装的软件包名称与包文件名之间的区别。文件名以 `.rpm` 文件结尾，且只能通过 `p` 选项进行查询。

你可以将 `q` 选项与 `i` 或 `l` 选项结合，以显示包的信息。`-qi` 选项显示软件信息，例如版本号等（而 `-qpi` 查询未安装的包文件）。`-ql` 选项显示软件包中所有文件的列表列表。`-h` 选项提供 rpm 选项的完整列表。这里显示了常用的查询选项：

- `-q application` 检查应用程序是否已安装
- `-qa application` 列出所有已安装的 RPM 应用程序
- `-qf filename` 查询拥有该文件的应用程序
- `-qR application` 列出此应用程序依赖的应用程序
- `-qi application` 显示所有应用程序信息
- `-ql application` 列出应用程序中的文件
- `-qd application` 仅列应用程序中的文档文件
- `-qc application` 仅列应用程序中的配置文件

如果你想查询一个 RPM 包文件（以 `.rpm` 结尾的文件），你可以使用相同的查询选项，但需要添加 `p` 选项，如下所示：

- `-qpi RPM-file` 显示 RPM 包中所有的包信息
- `-qpl RPM-file` 列出 RPM 包中的文件
- `-qpd RPM-file` 仅列出 RPM 包中的文档文件
- `-qpc RPM-file` 仅列出 RPM 包中的配置文件
- `-qpR RPM-file` 列出此 RPM 包依赖的包

如果你的 RPM 查询输出了很长的数据列表（例如详尽的文件列表），你可以将输出通过管道到 `more` 命令以进行分屏查看，甚至将输出重定向到文件中。

```
rpm -ql mozilla | more
rpm -qpl openmotif-2.2.2-5.386.rpm > mytemp
```

rpm 命令的语法如下（`rpm-package-name` 是你想要安装的软件包的名称）：

```
rpm -options rpm-package-name
```

软件包的文件名通常很长，包含了关于版本和发布的信息。以 `.rpm` 结尾。

如果你是从 CD-ROM 安装的，可以切换到 CD-ROM 的 RPM 目录，该目录持有 RPM 包，它可能位于红色 CD-ROM 上类似于 `RedHat` 的目录中。`ls` 命令列出所有软件软件包。如果你知道某个包名称的开头，应该在 `ls` 命令中包含它并加上通配符 `*`。包列表非常详细，一个屏幕无法显示所有内容。这对于显示包的详细名称很有帮助。以下示例列出了大多数 X Window System 软件包：

```
ls x*
```

你使用 `-i` 选项安装新包，使用 `-U` 选项用新版本更新当前已安装的包。如果你尝试使用 `-i` 选项安装已安装包的更高版本，你将收到一个错误，提示该包已安装。在下一个示例中，用户首先使用 `-i` 选项安装一个新包，然后使用 `-U` 选项更新一个包。通常的做法是包含 `-v` 和 `-h` 选项。在这里，`-v` 是详细选项，显示所有正在被安装的文件，而 `-h` 显示一个交叉符号以表示 RPM 仍在运行。在接下来的示例中，用户安装了从 rpmfind 获取的 XV 屏幕捕屏程序的软件包。注意输入的文件名。要列出全名，你使用 `ls` 命令配合前几个字符和星号，即 `ls hd*`。`-h` 选项显示 `#` 符号表示安装正在进行。带有 `-q` 选项的 rpm 命令用于检查软件是否已安装。对于已安装的包，需要使用软件名称——在这种情况下是 `xv-3.10a-23`。

```
[root@turtle mypackages]# ls *
xv-3.10a-23.i386.rpm
[root@turtle mypackages]# rpm -ihv xv-3.10a-23.i386.rpm
#######################################
[root@turtle mypackages]# rpm -q xv
xv-3.10a-23
```

要显示有关已安装包的信息，使用 `-qi`；而 `-ql` 显示给定的 RPM 包中包含的文件列表。

```
# rpm -ql xv
# rpm -ql xv
```

要显示直接从 RPM 包中获取的信息，你在 `q` 选项上添加 `p` 限定符。`-qpi` 组合显示有关特定包的信息，而 `-ql` 显示给定的 RPM 包中的文件列表。在这种情况下，你必须指定 RPM 包的完整名称。你可以通过 `ls` 命令配合前几个字符和星号 `ls hd*` 来避免输入整个包名。

```
[root@turtle mypackages]# ls *
xv-3.10a-23.i386.rpm
[root@turtle mypackages]# rpm -ihv xv-3.10a-23.i386.rpm
#######################################
[root@turtle mypackages]# rpm -q *
[root@turtle mypackages]# rpm -q xv
xv-3.10a-23
[root@turtle mypackages]# rpm -qpi xv
xv-3.10a-23
[root@turtle mypackages]# rpm -ql xv
[root@turtle mypackages]# rpm -ql *
[root@turtle mypackages]# rpm -ql xv
[root@turtle mypackages]#
[root@turtle mypackages]# rpm -ihv *
[root@turtle mypackages]# rpm -U *
[root@turtle mypackages]# rpm -v *
[root@turtle mypackages]# rpm -qi *
[root@turtle mypackages]# rpm -ql *
[root@turtle mypackages]# rpm -qd *
[root@turtle mypackages]# rpm -qc *
[root@turtle mypackages]# rpm -h *
[root@turtle mypackages]# rpm -qpi *
[root@turtle mypackages]# rpm -qpl *
[root@turtle mypackages]# rpm -qpd *
[root@turtle mypackages]# rpm -qpc *
[root@turtle mypackages]# rpm -qpR *
[root@turtle mypackages]# rpm -q *
[root@turtle mypackages]# rpm -qa *
[root@turtle mypackages]# rpm -qf *
[root@turtle mypackages]# rpm -qR *
[root@turtle mypackages]# rpm -qi *
[root@turtle mypackages]# rpm -ql *
[root@turtle mypackages]# rpm -qd *
[root@turtle mypackages]# rpm -qc *
[root@turtle mypackages]# rpm -qpi *
[root@turtle mypackages]# rpm -qpl *
[root@turtle mypackages]# rpm -qpd *
[root@turtle mypackages]# rpm -qpc *
[root@turtle mypackages]# rpm -qpR *
```

使用 `-qi` 选项显示有关已安装包的信息，而 `-ql` 显示给定的 RPM 包中包含的文件列表。
