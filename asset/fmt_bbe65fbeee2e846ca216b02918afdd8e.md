
你也可以通过 `mtools` 访问 Iomega Zip 驱动器。只需指定一个驱动器字母和相应设备的 `filename` 即可。对于内置 IDE（ATAPI）Zip 驱动器，请尝试使用 `/dev/hdd4` 作为设备文件，并在 `/etc/mtools.conf` 文件中添加以下行：

```
drive e: file="/dev/hdd4"
```

之后你应该能够使用 `mtools` 命令访问 Zip 驱动器（将其称为 E 驱动器）。例如，要查看目录列表，请将 Zip 磁盘放入 Zip 驱动器并输入：

```
mdir e:
```

## 学习 mtools 命令

`mtools` 包是一组实用程序的集合。到目前为止，我一直在使用 `mdir`——它是 DOS 中 `DIR` 命令的 `mtools` 对应项。其他 `mtools` 命令也相当容易使用。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_485_0.png)

如果你熟悉 MS-DOS 命令，使用 `mtools` 命令就很简单。将 DOS 命令以小写字母输入，并记得在每个命令前加上 `m`。因为 Linux 命令和文件名区分大小写，所以在输入 `mtools` 命令时必须全部使用小写字母。

表 3-4 总结了 `mtools` 中可用的命令。

### 表 3-4 mtools 命令

| mtools 实用程序 | MS-DOS 命令（如果有） | mtools 实用程序的功能 |
|---|---|---|
| `mattrib` | `ATTRIB` | 更改 MS-DOS 文件属性标志 |
| `mbadblocks` |  | 测试软盘并在文件分配表（FAT）中标记坏块 |
| `mcd` | `CD` | 更改 MS-DOS 目录 |
| `mcopy` | `COPY` | 在 MS-DOS 和 Linux 之间复制文件 |
| `mdel` | `DEL` or `ERASE` | 删除 MS-DOS 文件 |
| `mdeltree` | `DELTREE` | 递归删除 MS-DOS 目录 |
| `mdir` | `DIR` | 显示 MS-DOS 目录列表 |
| `mdu` |  | 列出目录及其内容占用的空间 |
| `mformat` | `FORMAT` | 在低级格式化的软盘上放置 MS-DOS 文件系统。（在 Red Hat Linux 中使用 `fdformat` 对软盘进行低级格式化。） |
| `minfo` |  | 获取有关 MS-DOS 文件系统的信息 |
| `mkmanifest` |  | 制作短名称等效列表 |
| `mlabel` | `LABEL` | 初始化 MS-DOS 卷标 |
| `mmd` | `MD` or `MKDIR` | 创建 MS-DOS 目录 |
| `mmove` |  | 移动或重命名 MS-DOS 文件或子目录 |
| `mmount` |  | 挂载 MS-DOS 磁盘 |
| `mpartition` |  | 创建 MS-DOS 文件系统作为分区 |
| `mrd` | `RD` or `RMDIR` | 删除 MS-DOS 目录 |
| `mren` | `REN` or `RENAME` | 重命名现有 MS-DOS 文件 |
| `mshowfat` |  | 显示 MS-DOS 文件的 FAT 条目 |
| `mtoolstest` |  | 测试并显示当前 `mtools` 配置 |
| `mtype` | `TYPE` | 显示 MS-DOS 文件的内容 |
| `mwrite` | `COPY` | 将 Linux 文件复制到 MS-DOS |
| `mzip` |  | 对 SCSI Zip 磁盘执行某些操作 |

你可以像使用相应的 DOS 命令一样使用 `mtools` 命令。例如，`mdir` 命令的工作方式与 DOS 中的 `DIR` 命令相同。表 3-4 中显示的所有其他 `mtools` 命令也一样。

你可以使用通配符（如 `*`）与 `mtools` 命令，但必须记住 Linux shell 是首先看到你命令的程序。如果你不想让 shell 到处展开通配符，请对包含任何通配符的文件名使用引号。例如，要将 A 驱动器中的所有 `*.txt` 文件复制到当前 Red Hat Linux 目录，请使用以下命令：

```
mcopy "a:*.txt"
```

如果省略引号，shell 会尝试使用当前 Linux 目录中的文件名展开字符串 `a:*.txt`。它还会尝试从 DOS 软盘复制这些文件（如果有的话）。

另一方面，如果你想从 Linux 目录复制文件到 DOS 软盘，你希望 shell 展开任何通配符。例如，要将当前 Linux 目录中的所有 `*.jpg` 文件复制到 DOS 软盘，请这样使用 `mcopy`：

```
mcopy *.jpg a:
```

使用 `mtools` 实用程序时，你可以使用反斜杠字符 (`\`) 作为目录分隔符，就像在 DOS 中一样。然而，当你输入包含反斜杠字符的文件名时，必须用双引号 (`""`) 将名称括起来。例如，这里有一个命令可以将 A 驱动器上子目录中的文件复制到当前 Linux 目录：

```
mcopy "a:\test\sample.dat"
```

## 格式化 DOS 软盘

假设你在家用 PC 上运行 Red Hat Linux，且系统上已不再有 MS-DOS，但你想将一些文件复制到 MS-DOS 软盘上并带到办公室。如果已有格式化的 MS-DOS 软盘，你只需挂载该软盘并使用 Linux `cp` 命令将文件复制到软盘即可。但如果没有格式化的 DOS 软盘怎么办？`mtools` 软件包再次派上用场。

`mtools` 软件包提供了 `mformat` 实用程序，可将软盘格式化为在 MS-DOS 中使用。与一次性格式化软盘的 DOS `format` 命令不同，`mformat` 命令要求你遵循两步流程：

- 1. 使用 `fdformat` 命令对软盘进行低级格式化。

`fdformat` 命令使用软盘设备名称作为参数；设备名称包含格式化软盘所需的所有参数。

图 3-5 说明了软盘驱动器设备的设备命名约定。如图 3-5 所示，你可以使用以下命令格式化系统 A 驱动器中的 3.5 英寸高密度软盘：

```
fdformat /dev/fd0H1440
```

## 2. 使用 `mformat` 命令在低级格式化的软盘上放置 MS-DOS 文件系统。

如果软盘在 A 驱动器中，输入以下命令创建格式化的 DOS 软盘：

```
mformat a:
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_488_0.png)

图 3-5：

这就是在 Red Hat Linux 中构造软盘驱动器名称的方法。

表示软盘容量（以千字节为单位）的 3 或 4 位数字：

5.25 英寸：360、720 或 1200

3.5 英寸：360、720 或 1440

以下其中一个字母：

`d` = 低密度 5.25 英寸

`D` = 低密度 3.5 英寸

`h` = 高密度 5.25 英寸

`H` = 高密度 3.5 英寸

以下其中一个字母：

`0` = 第一个软盘驱动器 (`A:`)

`1` = 第二个软盘驱动器 (`B:`)

### 第 4 章：管理应用程序

## 本章内容

- 学习 RPM

- 安装和移除软件 RPM

- 从源文件构建应用程序

- 使用 Red Hat Network 更新 Red Hat Linux 应用程序

大多数 Red Hat Linux 软件包以名为 Red Hat Package Manager（RPM）文件的特殊文件形式分发，因此你应该知道如何安装或移除以 RPM 文件形式提供的软件包。在本章中，我将向你展示如何使用 RPM 文件。

许多其他开源软件包以源代码形式提供，通常在压缩归档中。你必须构建并安装软件才能使用它。我描述了下载、构建和安装基于源的软件包时通常遵循的步骤。

最后，我简要介绍了 Red Hat Network 以及在注册后如何使用 Red Hat 的 Update 代理来更新 Red Hat Linux 应用程序。

## 使用 Red Hat Package Manager

Red Hat Package Manager（RPM）是一种将软件产品所需的所有文件打包到单个文件中的系统——称为 RPM 文件或简称为 RPM。事实上，整个 Red Hat Linux 发行版就是大量 RPM。处理 RPM 的最佳方式是通过 `RPM` 命令。你必须在终端窗口或文本控制台的 shell 提示符下输入这些命令。

## 使用 RPM 命令

当你从随附 DVD 安装 Red Hat Linux 时，Red Hat 安装程序使用 `rpm` 命令解包软件包（RPM 文件）并将内容复制到你的硬盘。

你不必了解 RPM 文件的内部结构，但应该知道如何使用 `rpm` 命令来处理 RPM 文件。以下是你可以使用 `rpm` 命令完成的一些操作：

- 查找系统上已安装的 RPM 的版本号和其他信息。

- 从 RPM 安装新的软件包。你可能会安装在初始安装期间跳过的软件包。例如，在重新构建内核之前，你必须安装 Linux 内核的源文件。你可以使用 `rpm` 命令完成此操作。

- 移除（卸载）之前从 RPM 安装的不需要的软件。如果你发现很少（或从不）使用某个软件包，可以卸载它以收回磁盘空间。
