

第一个 IDE 驱动器（`/dev/hda1`）。如果你有其他的 DOS 驱动器（例如 D），你可以添加另一行，将 D 驱动器定义为相应的磁盘分区。

如果你的系统的 A 驱动器是高密度 3.5 英寸驱动器，你无需更改默认的 `/etc/mtools.conf` 文件中的任何内容即可访问软驱。如果你还想访问硬盘中的任何 DOS 分区，请取消 C 驱动器相应行的注释并进行编辑。

你还可以通过 mtools 访问 Iomega Zip 驱动器。只需指定驱动器字母和相应设备的文件名。对于内置的 IDE（ATAPI）Zip 驱动器，请尝试将 `/dev/hdd4` 作为设备文件，并在 `/etc/mtools.conf` 文件中添加以下行：

```
drive e: file="/dev/hdd4"
```

之后，你可以使用 mtools 命令访问 Zip 驱动器（将其视为 E 驱动器）。例如，要查看目录列表，请将 Zip 盘放入 Zip 驱动器并输入：

```
mdir e:
```

## 学习 mtools 命令

mtools 包是一组实用工具。到目前为止，我一直在使用 mdir —— 它是 DOS 中 DIR 命令的 mtools 对应版本。其他 mtools 命令也很容易使用。

如果你熟悉 MS-DOS 命令，使用 mtools 命令就很简单了。以小写字母输入 DOS 命令，并记得在每个命令前面加上 m。由于 Linux 命令和文件名是区分大小写的，因此在输入 mtools 命令时必须全部使用小写字母。

表 3-4 总结了 mtools 中可用的命令。

| mtools 工具 | MS-DOS 命令（如果有） | mtools 工具执行以下操作 |
| :--- | :--- | :--- |
| mattrb | ATTRIB | 更改 MS-DOS 文件属性标志 |
| mbadblocks | | 测试软盘并在文件分配表 (FAT) 中标记坏块 |
| mcd | CD | 更改 MS-DOS 目录 |
| mcopy | COPY | 在 MS-DOS 和 Linux 之间复制文件 |
| mdel | DEL 或 ERASE | 删除 MS-DOS 文件 |
| mdeltree | DELTREE | 递归删除 MS-DOS 目录 |
| mdir | DIR | 显示 MS-DOS 目录列表 |
| mdu | | 列出目录及其内容所占用的空间 |
| mformat | FORMAT | 在已低级格式化的软盘上建立 MS-DOS 文件系统（在 Linux 中使用 fdformat 对软盘进行低级格式化。） |
| minfo | | 获取有关 MS-DOS 文件系统的信息 |
| mkmanifest | | 创建短名称等效项列表 |
| mlabel | LABEL | 初始化 MS-DOS 卷标 |
| mmd | MD 或 MKDIR | 创建 MS-DOS 目录 |
| mmovc | | 移动或重命名 MS-DOS 文件或子目录 |
| mmount | | 挂载 MS-DOS 磁盘 |
| mpartition | | 将 MS-DOS 文件系统创建为分区 |
| mrd | RD 或 RMDIR | 删除 MS-DOS 目录 |
| mren | REN 或 RENAME | 重命名现有的 MS-DOS 文件 |
| mshowfat | | 显示 MS-DOS 文件的 FAT 条目 |
| mtooletest | | 测试并显示当前的 mtools 配置 |
| mtype | TYPE | 显示 MS-DOS 文件的内容 |
| mwrite | COPY | 将 Linux 文件复制到 MS-DOS |
| mzip | | 在 SCSI Zip 磁盘上执行某些操作 |

你可以像使用对应的 DOS 命令一样使用 *mtools* 命令。例如，*mdir* 命令的作用与 DOS 中的 *DIR* 命令相同。表 3-4 中显示的所有其他 *mtools* 命令也是如此。

你可以使用通配符（例如 *）配合 *mtools* 命令，但你必须记住 Linux shell 是第一个看到你的命令的程序。如果你不想让 shell 到处展开通配符字符，请在包含任何通配符字符的文件名周围使用引号。例如，要复制 A 驱动器上的所有 *.txt 文件到当前目录，请使用以下命令：

```
mcopy "a:*.txt" .
```

如果你省略了引号，shell 将尝试使用当前 Linux 目录中的文件名展开字符串 a:*.txt。它还会尝试从 DOS 软盘复制这些文件（如果有）。

另一方面，如果你想从 Linux 目录复制文件到 DOS 软盘，你确实希望 shell 展开任何通配符字符。例如，要复制当前 Linux 目录中的所有 *.jpg 文件到 DOS 软盘，请像这样使用 `mcopy`：

```
mcopy *.jpg a:
```

使用 mtools 工具时，你可以使用反斜杠字符（\）作为目录分隔符，正如你在 DOS 中所做的那样。但是，当你输入包含反斜杠字符的文件名时，必须用双引号（" "）将该名称包围起来。例如，下面是一个从 A 驱动器上的子目录复制文件到当前 Linux 目录的命令：

```
mcopy "a:\test\sample.dat" .
```

## 第 4 章：安装和更新应用程序

### 本章内容

- 使用 `rpm` 命令处理 **RPM 文件**
- 使用 `dpkg`、`dselect` 和 **APT** 处理 **DEB 文件**
- 从源文件构建应用程序
- 在线更新 Linux 应用程序

大多数为 Linux 制作的软件包都以两种特殊文件格式之一进行分发：Red Hat Package Manager (RPM) 文件或 Debian (DEB) 文件。因此，你必须知道如何安装或删除以 RPM 或 DEB 文件形式提供的软件包。幸运的是，本章将向你展示如何操作 RPM 和 DEB 文件。

![](img/11709a8f88c8cd03868a929dc94c0e2b_474_0.png)

你可以在所有 Linux 发行版中安装 RPM 和 DEB 文件，但每个发行版都有其偏好的分发格式。Fedora Core 凭借其 Red Hat Linux 的血统，倾向于使用 RPM 文件，而大多数基于 Debian 的发行版，如 Knoppix、MEPIS、Ubuntu 和 Xandros，则使用 DEB 文件来分发软件。SUSE Linux 使用 RPM 格式。

许多其他开源软件包以源代码形式提供，通常位于压缩归档文件中。你必须解包、构建并安装软件才能使用它。我将描述你在下载、构建和安装基于源代码的软件包时通常遵循的步骤。

最后，我将简要描述如何在线更新你的 Linux 系统。你会发现，每个发行版都有自己用于在线更新的工具。

## 处理 RPM 文件

RPM 是一种将软件产品所需的所有必要文件打包到单个文件中的系统——称为 *RPM 文件*，或简称 *RPM*。实际上，整个 Fedora Core 和 SUSE 发行版就是大量的 RPM。操作 RPM 的最佳方式是通过 RPM 命令。你必须在终端窗口或文本控制台的 shell 提示符下输入这些命令。

![](img/11709a8f88c8cd03868a929dc94c0e2b_475_0.png)

在 Fedora Core 中，`rpm` 命令仅适用于你需要安装少量 `rpm` 文件的情况。要安装大量 `rpm` 文件，你应该从桌面选择“应用程序::添加/删除软件”。如果你从 CD 或 DVD 安装 `rpm` 文件，请先挂载 CD/DVD，然后输入 `system-config-packages`（如果你的 CD/DVD 挂载在其他目录，请将 `/media/cdrom` 替换为该目录名称）。这将打开一个包管理窗口，你可以从中选择并安装成组的软件包。

### 使用 rpm 命令

当你安装基于 `rpm` 的发行版（如 Fedora Core）时，安装程序使用 `rpm` 命令解包软件包（`rpm` 文件）并将内容复制到你的硬盘上。

你不需要理解 `rpm` 文件的内部结构，但你需要了解如何使用 `rpm` 命令来操作 `rpm` 文件。以下是你可以使用 `rpm` 命令执行的一些操作：

- 查找你系统中已安装的 RPM 的版本号和其他信息。
- 从 RPM 安装新的软件包。例如，你可能需要安装初始安装时跳过的某个软件包。
- 删除（卸载）你之前从 RPM 安装的不需要的软件。如果发现你很少（或从未）使用某个软件包，你可以卸载它以回收磁盘空间。
- 用新版本升级旧版本的 RPM。例如，在 Fedora Core 中，在你从 Fedora Core 下载站点（在线列出于 `http://fedora.redhat.com/download/mirrors.html`）下载软件包的新版本后，你可能需要升级。你必须升级 RPM 才能受益于新版本中的修复。
- 验证 RPM 是否处于正常工作状态。你可以验证软件包以检查所有必要文件是否位于正确的位置。

正如你所见，`rpm` 命令功能强大——根据你使用的选项不同，它可以做很多不同的事情。

如果你忘记了 `rpm` 的选项，请输入以下命令以查看列表：

```
rpm --help | more
```

`rpm` 选项的数量会让你惊讶！

