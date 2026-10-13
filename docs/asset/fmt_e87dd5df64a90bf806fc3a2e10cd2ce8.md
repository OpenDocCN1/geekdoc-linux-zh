
## 将文件复制到 DOS 分区

一旦 MS-DOS 分区被引用，你就可以使用它们的驱动器号从那里拷贝文件。以下命令将 `mydoc.html` 拷贝到 `c` 分区并重命名为 `mydoc.htm`。注意使用正斜杠而不是反斜杠。

```
$ mcopy mydoc.html c:/webstuff/mydoc.htm
```

由于 DOS 和 Linux 处理换行符的方式不同，将文件拷贝到 Linux 分区时应使用 `-t` 选项。以下命令将 `mydoc.txt` 从 `c:/project` 目录拷贝到 `/newdocs` 目录：

```
$ mcopy -t c:/project/mydoc.txt
```

归档用于备份文件或将其合并为一个软件包，然后可以通过互联网传输或发布到 FTP 站点以便下载。Linux 和 Unix 系统使用的标准归档工具是 `tar`，存在多种压缩程序供选择，包括 GNU zip `gzip`、`Zip`、`bzip` 和 `compress`。

### 使用 File Roller 进行归档和压缩

Red Hat 有 `File Roller` 工具（可从“应用程序”菜单访问），它作为访问和压缩文件的图形界面，让你能够使用图形界面执行 `zip`、`gzip`、`tar` 和 `bzip2` 操作（见图 10-4）。你可以查看归档的内容、提取所需的文件并创建新的压缩归档。当你创建归档时，通过指定文件扩展名来确定压缩方法，例如 `gzip` 使用 `.gz`，`bzip2` 使用 `.bz2`。你可以从文件类型菜单选择不同的扩展名，或者自己扩展扩展名。要归档并压缩文件，你可以选择组合扩展名 `.tar.bz2`，它既归档又压缩。

图 10-4 File Roller 归档和压缩工具

![](img/b575339375dd1a4a4eb2f8188c6df286_235_0.png)

使用 `bzip2`。点击“添加（Add）”按钮将文件添加到你的包中。要从包中提取文件，打开包以显示文件列表。然后你可以点击“提取（Extract）”按钮提取特定文件或整个包。其他可选 GUI 工具还有 `guiTAR`、`LnxZip`、`Ark`、`KArchive` 和 `Xtar`。

# 第 10 章：管理 Linux 文件、目录和存档

## 存档文件和目录

`tar` 工具用于为文件和目录创建存档。通过 `tar`，你可以归档特定文件，在包中更新它们，并根据需要向该包添加新文件。你甚至可以归档包含所有文件和子目录的整个目录，所有内容都可以从包中恢复。`tar` 工具最初设计用于在磁带上创建存档。`tar` 一词代表 tape（磁带）。你可以在任何设备（如软磁盘）上创建存档，也可以也可以创建一个包来存放该存档。`tar` 工具是制作文件备份或将多个文件合并为一个文件以进行跨网络传输的理想选择型工具（`File Roller` 是 `tar` 的 GUI 界面）。

> 注意：可以使用 `pax` 作为 `tar` 的替代方案。`pax` 设计用于与各种 Unix 存档格式（如 `c`、`bcpio` 和 `tar`）配合工作。你可以提取、列出和创建存档。如果你正在处理在不同存档格式的 Unix 系统创建的存档，`pax` 非常帮助。

### 显示存档内容

GNOME 和 K Desktop 的两个文件管理器都具有自动显示 `tar` 文件内容的能力。内容显示就像是目录中的文件一样。你可以以图标或详细信息列出文件，并按名称、类型或其他字段进行排序。你甚至可以显示文件的内容。点击文本文件将用文本编辑器打开它，图像将用图像查看器显示。如果文件管理器无法确定使用哪个程序显示文件，它会提示你选择应用程序。两个文件管理器都可以对存储在远程文件系统上的存档（例如 FTP 站点上的存档）执行相同的操作。你可以获取其内容列表并读取它们的 `readme` 文件。`Nautilus` 文件管理器（GNOME）还可以提取存档。右键点击存档图标并选择“提取（Extract）”。

### 创建存档

在 Linux 上，`tar` 通常用于用于在设备或文件上创建存档。你可以通过使用 `f` 选项配合设备或文件的名称，引导 `tar` 将文件归档到特定设备或文件。使用 `f` 选项的 `tar` 命令语法如下一个示例所示。在为存档创建文件时，文件名通常赋予 `.tar` 扩展名。这是一个约定，并不是强制要求的。你可以使用任意数量的文件。如果指定了目录名称，其所有子目录都将包含在存档中。

```
$ tar archive-name.tar directory-and-file-names
```

创建一个存档，使用 `c` 选项。与 `f` 选项结合使用，`c` 在文件或设备上创建一个存档。你可以在 `f` 选项之前或紧邻输入该选项。注意，`tar` 存档之前没有连字符。表 10-7 列出了你可以与 `tar` 一起使用的选项。在下一个示例中，目录 `mydir` 及其所有子目录保存在文件 `myarch.tar` 中。在这个示例中，`mydir` 目录包含两个文件 `mymeeting` 和 `party`，以及一个名为 `reports` 的目录，该目录有三个文件：`weather`、`monday` 和 `friday`。

```
$ tar cvf myarch.tar mydir

mydir/

mydir/reports/

mydir/reports/weather

mydir/reports/monday

mydir/reports/friday

mydir/mymeeting

mydir/party
```

| 命令 | 执行 |
| --- | --- |
| `tar options files` | 将文件备份到磁带、设备或存档文件。 |
| `tar options archive_name filelist` | 将文件备份到指定为 `archive_name` 的特定文件或设备。`filelist`；可以是文件名或目录。 |
| Options（选项） | |
| `c` | 创建新存档。 |
| `t` | 列出存档中文件的名称。 |
| `r` | 将文件追加到存档中。 |
| `U` | 使用新文件和更改的文件更新存档；仅添加自归档以来修改的文件或存档中已不存在的文件。 |
| `--delete` | 从存档中删除文件。 |
| `w` | 在归档每个文件之前等待用户的确认；允许你选择性地更新存档。 |
| `x` | 从存档中提取文件。 |
| `m` | 从存档中提取文件时，不分配新的时间戳。 |
| `M` | 创建一个多卷存档，可以存储在多个软磁盘上。 |
| `f archive-name` | 将存档保存到文件名，而不是默认的磁带设备。当给定存档名称时，`f` 选项将存档保存到该名称的文件中。 |
| `f device-name` | 将 `tar` 存档保存到设备（如软磁盘或磁带）。`/dev/fd0` 是软磁盘的设备；默认设备存储在 `/etc/default/tar-file` 中。 |
| `v` | 在归档时显示每个文件名。 |
| `z` | 使用 `gzip` 压缩或解压存档文件。 |
| `j` | 使用 `bzip2` 压缩或解压存档文件。 |

表 10-7 文件存档：`tar`

### 提取存档

用户可以使用 `x` 选项从磁带上提取目录。`xf` 选项从存档文件或设备中提取文件。`tar` 提取操作会生成所有子目录。在下一个示例中，`xf` 选项引导 `tar` 从 `tar` 文件 `myarch.tar` 中提取所有文件和子目录。

```
$ tar xvf myarch.tar

mydir/

mydir/reports/

mydir/reports/weather

mydir/reports/monday

mydir/reports/friday
```

使用 `x` 选项从磁带上提取目录。`xf` 选项从存档文件或设备中提取文件。`tar` 提取操作会生成所有子目录。在下一个示例中，`xf` 选项引导 `tar` 从存档文件 `myarch.tar` 中提取所有文件和子目录。

```
$ tar xvf myarch.tar

mydir/

mydir/reports/

mydir/reports/weather

mydir/reports/monday

mydir/reports/friday
```
