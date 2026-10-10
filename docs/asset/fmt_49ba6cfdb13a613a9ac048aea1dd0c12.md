
你的 Linux 系统提供了一组名为 `mtools` 的实用程序，可让你轻松地访问格式化为 MS-DOS 的软盘和硬盘。它们仅适用于旧的 MS-DOS 或 FAT32 文件系统，而不适用于使用 NTFS 文件系统的 Windows XP、NT 或 2000。`mcopy` 命令使你可以将文件复制到软盘驱动器中的 MS-DOS 软盘或硬盘上的 Windows FAT32 分区中，或从那里复制出来。无需进行挂载等特殊操作。使用 mtools 时，你无需挂载 MS-DOS 分区即可访问它。对于 MS-DOS 软盘，请将软盘放入软盘驱动器，然后即可使用 mtool 命令访问这些文件。例如，要从 MS-DOS 软盘将文件复制到你的 Linux 系统，请使用 `mcopy` 命令。你用 `a:` 指定 A 驱动器上的 MS-DOS 磁盘。与普通 DOS 路径名不同，mtool 命令使用的路径名使用正斜杠而不是反斜杠。A 驱动器上的目录 `docs` 通过路径名 `a:/docs` 引用，而不是 `a:\docs`。与 MS-DOS 默认将第二个参数设为当前目录不同，使用 `mcopy` 时始终需要提供第二个参数。下一个示例将文件 `mydata` 复制到 MS-DOS 软盘，然后从软盘将 `preface` 文件复制到当前的 Linux 目录。

```
$ mcopy mydata a:
$ mcopy a:/preface .
```

> 你可以使用 mtools 将数据复制到 Windows 格式的软盘或 Windows FAT32 分区，Windows XP 也可以读取或写入这些分区，但你无法使用 mtools 访问 Windows XP、NT 或 2000 的硬盘文件系统（NTFS）。NTFS 分区需要不同的工具，即 NTFS 内核模块（参见第 4 章）。

你可以使用 `mdir` 命令列出 MS-DOS 磁盘上的文件，并使用 `mcd` 命令更改该磁盘上的目录。下一个示例列出了软盘驱动器中 MS-DOS 磁盘上的文件，然后切换到该驱动器的 `docs` 目录：

```
$ mdir a:
$ mcd a:/docs
```

通过 `/etc/mtools.conf` 文件配置 mtools 对 MS-DOS 或 Windows 95、98 或 ME 分区的访问。该文件列出了几个不同的默认 MS-DOS 或 Windows 分区和磁盘驱动器。每个驱动器或分区都由特定的设备名称标识。

## 文件归档和压缩

归档用于备份文件或将它们组合成一个包，然后可以作为一个文件通过 Internet 传输或发布到 FTP 站点以便轻松下载。在 Linux 和 Unix 系统上使用的标准归档实用程序是 `tar`，并且存在若干图形用户界面（GUI）前端。你可以从几种压缩程序中进行选择，包括 GNU zip（`gzip`）、Zip、bzip 和 compress。

### 使用 File Roller 进行文件归档和压缩

Red Hat 和 Fedora 提供了 File Roller 工具（可从附件菜单访问，标记为 Archive Manager），它作为归档和压缩文件的 GUI 前端，让你使用 GUI 界面执行 Zip、`gzip`、`tar` 和 bzip2 操作（参见图 10-4）。你可以查看归档的内容，提取你想要的文件，并创建新的压缩归档。当你创建归档时，通过指定文件扩展名来确定其压缩方法，例如 gzip 使用 `.gz`，bzip2 使用 `.bz2`。你可以从文件类型菜单中选择不同的扩展名，或者自己输入扩展名。要同时归档和压缩文件，你可以选择组合扩展名，如 `.tar.bz2`，它既使用 tar 进行归档，又使用 bzip2 进行压缩。点击“添加”以将文件添加到归档中。要从归档中提取文件，请打开归档以显示归档文件列表。然后你可以点击“提取”以提取特定文件或整个归档。

![](img/ab68ea377332b50bf70ef1316c8175b6_304_0.png)

图 10-4 File Roller 归档和压缩工具

> **提示** 对于流行的 `rar` 归档，你可以使用 `unrar` 工具读取和提取 `rar` 归档，但不能用于创建它们。`unrar` 可从 `rpm.livna.org` 获取，并可以使用 `yum` 下载和安装。图形前端如 `Xarchiver` 和 `Linrar` 可从 `freshmeat.net` 获取。要创建 `rar` 归档，你需要从 `www.rarlab.com` 的 `Rarlab` 购买归档工具。

> File Roller 也可以用于轻松查看归档文件的内容。从文件管理器中，右键单击归档，然后选择“`Open With`”（通过...打开）“`Archive Manager`”（归档管理器）。将显示该归档中的文件和目录列表。对于子目录，请双击其条目。此方法也适用于 RPM 软件文件，允许你浏览组成软件包的所有文件。

### 归档文件和设备：tar

`tar` 实用程序为文件和目录创建归档。使用 `tar`，你可以归档特定文件，在归档中更新它们，并随时向该归档添加新文件。你甚至可以归档包含所有文件和子目录的整个目录，所有这些都可以通过归档恢复。`tar` 实用程序最初设计用于在磁带上创建归档（“`tar`” 一词代表磁带归档，tape archive），但你可以在任何设备上创建归档，如软盘，或者你可以创建一个归档文件来保存归档。`tar` 实用程序非常适合为你的文件创建备份，或将多个文件组合成一个文件以便通过网络传输（`File Roller` 是 `tar` 的 GUI 接口）。

> **注意** 作为 `tar` 的替代方案，你可以使用 `pax`，它设计用于处理不同的 Unix 归档格式，如 `cpio`、`bcpio` 和 `tar`。你可以提取、列出和创建归档。如果你正在处理在不同归档格式上创建的 Unix 系统归档，`pax` 实用程序会很有帮助。

### 显示归档内容

GNOME 和 K 桌面中的文件管理器都具备自动显示 tar 归档文件内容的功能。内容显示效果类似于目录中的文件。你可以将文件显示为图标或带详细信息，并按名称、类型或其他字段进行排序。你甚至可以查看文件的内容。点击文本文件会用文本编辑器打开它，而图像则会使用图像查看器显示。如果文件管理器无法确定使用哪个程序来显示该文件，它会提示你选择一个应用程序。这两个文件管理器还可以在远程文件系统（例如 FTP 站点的 tar 归档）上的归档执行相同类型的操作。你可以获取其内容的列表，甚至读取其 readme 文件。Nautilus 文件管理器（GNOME）还可以解压归档。右键点击归档图标并选择“解压（Extract）”。

### 创建归档

在 Linux 中，`tar` 常用于在设备或文件中创建归档。你可以使用带有设备或文件名的 `f` 选项来指示 `tar` 将文件归档到特定设备或文件。使用带有 `f` 选项的 `tar` 命令语法如下例所示。

设备或文件名通常被称为归档名称。创建 tar 归档的文件时，文件名通常使用 `.tar` 扩展名。这仅仅是一种约定，并非强制要求。你可以列出任意数量的文件名。如果指定了目录名，其所有子目录都将包含在归档中。

```bash
$ tar -options f archive-name.tar directory-and-file-names
```

要创建归档，请使用 `c` 选项。与 `f` 选项结合使用时，`c` 在文件或设备上创建归档。此选项输入在 `f` 选项之前。你还可以在 `f` 选项前添加 `v` 选项，以便查看 `tar` 命令的结果（`v` 代表 verbose，即详细模式）。注意，tar 选项前没有短横线。表 10-6 列出了你可以与 `tar` 配合使用的不同选项。在下一个例子中，目录 `mydir` 及其所有子目录被保存在文件 `myarch.tar` 中。在此示例中，`mydir` 目录包含两个文件 `mymeeting` 和 `party`，以及一个名为 `reports` 的目录，该目录包含三个文件：`weather`、`monday` 和 `friday`。

```bash
$ tar cvf myarch.tar mydir
mydir/
mydir/reports/
mydir/reports/weather
mydir/reports/monday
mydir/reports/friday
mydir/mymeeting
mydir/party
```

### 提取归档

用户稍后可使用 `x` 选项从磁带上提取目录。`xf` 选项从归档文件或设备中提取文件。`tar` 提取操作会生成所有子目录。

在下一个例子中，`xvf` 选项指示 `tar` 从 `tar` 文件 `myarch.tar` 中提取所有文件和子目录，并在屏幕上显示所提取文件的名称：

```bash
$ tar xvf myarch.tar
mydir/
mydir/reports/
mydir/reports/weather
mydir/reports/monday
mydir/reports/friday
mydir/mymeeting
mydir/party
```
