
```
$ tar options archive-name.tar directory-and-filenames
```

要创建存档，请使用 `c` 选项。与 `f` 选项结合时，`c` 在文件或设备上创建一个存档。你在 `f` 选项之前并紧邻输入 `c` 选项。`tar` 选项前面没有横杠。表 12-7 列出了你可以与 `tar` 使用的不同选项。

| 命令 | 执行功能 |
| --- | --- |
| tar options files | 将文件备份到磁带、设备或存档文件。 |
| tar options archive_name list | 将文件备份到指定为 `archive_name` 的特定文件或设备。`filesize` 可以文件名或目录。 |
| c | 创建新存档。 |
| --delete | 从存档中删除文件。 |
| archive-name | 将磁带存档保存到文件名，而不是默认的磁带设备。当给定存档名称时，`f` 选项将存档保存在该名称的文件中。 |
| device-name | 将 tar 存档保存到设备如软磁盘或磁带。`/dev/fd0` 是你的软磁盘的设备名；默认设备存储在 `/etc/default/tar-file` 中。 |
| j | 使用 bzip2 压缩或解压缩存档文件 |
| m | 从存档中提取文件时，不分配新的时间戳。 |
| M | 创建可能存储在几块软磁盘上的多卷存档。 |
| r | 将文件追加到存档。 |
| t | 列出存档中文件的名称。 |
| U | 使用新文件和更改的文件更新存档；仅添加自归档以来被修改的文件，或存档中已不存在的文件。 |
| w | 在归档每个文件之前等待用户确认；允许你选择性地更新存档。 |
| x | 从存档中提取文件。 |
| v | 在归档时显示每个文件名。 |
| z | 使用 gzip 压缩或解压缩归档文件 |

表 12-7 文件存档：tar

目录 `mydir` 及其所有的子目录被保存在文件 `myarch.tar` 中。在这个示例中，`mydir` 目录包含两个文件 `mymeting` 和 `party`，以及一个名为 `reports` 的目录，该目录有三个文件：`weather`、`monday` 和 `friday`。

```
$ tar cvf myarch.tar mydir/mydir/reports/
```

用户可以使用 `x` 选项从存档中提取文件。`x` 选项用于从设备或文件提取存档。在示例中：

```
$ tar cvf myarch.tar mydir/mydir/reports/
```

`r` 选项将文件追加到存档。`r` 选项用于将文件追加到存档。

```
$ tar cvf myarch.tar mydir/mydir/reports/
```

`f` 选项将存档保存到文件名，而不是默认的磁带设备。当给定存档名称时，`f` 选项将存档保存在该名称的文件中。

```
$ tar cvf myarch.tar mydir/mydir/reports/
```

`z` 选项使用 `gzip` 压缩或解压缩归档文件。

```
$ tar cvf myarch.tar mydir/mydir/reports/
```

## 更新存档

如果你更改了存档中的任何文件，可以使用 `u` 选项指令 `tar` 进行更新。只有自归档以来被修改的文件或新创建的文件会被添加到存档中。。

## 压缩存档

> 注意：若要使用多个 CD/ROM 备份文件，你会首先使用 `-M`（多卷）选项创建一个分卷存档。DVD 大小将通过 `--tape-length=29400` 指定。

## 第 12 章：文件、目录与存档 277

```
myarchprog myarch.tar cvf $*
```

这里展示了带有多个参数的 `myarchprog` 脚本运行：

```
$ myarchprog mydata preface
```

```
mydata preface
```

## 归档到磁带

如果你指定了一个默认设备（例如磁带），并想在上面创建存档，可以简单使用不带 `f` 选项以及设备或文件名的 `tar`。这对于备份你的文件很有帮助。默认设备的名称存储在 `/etc/default/tar/` 文件中。使用默认磁带设备的 `tar` 命令的语法如下例所示。如果指定了目录名，则所有的子目录都将包含在存档中。

```
$ tar option directory-and-filenames
```

在下一个示例中，目录 `mydir` 及其所有子目录被保存到默认磁带设备上：

```
$ tar c mydir
```

在这个示例中，`mydir` 目录及其所有文件和子目录从默认磁带中提取，并在用户的工作目录中使用：

```
$ tar x mydir
```

> 注意：你可以使用其他存档程序，如 cpio、pax 和 shar。然而，`tar` 是归档应用软件时最常用的程序。

## 文件压缩：gzip, bzip2, 和 zip

你可能出于多种原因想要减小文件大小：最常见的两个是节省空间，如果你正在跨网络传输文件，则是为了节省传输时间。你可以通过创建文件的压缩副本来有效缩小文件大小。当你再次需要该文件时，可以将其解压。压缩通常与存档结合使用，以便一次性压缩整个目录及其文件。解压会生成存档文件的副本，然后可以提取它，从而生成这些文件和目录的副本。Roller 为这些任务提供了 GUI。关于 `gzip` 的更多信息，请查看 man 页面或在线页面 www.gnu.org/software/gzip/manual/。对于 `bzip2`，也请查看其 man 页面或在线文档 www.bzip2.org/docs.html。

## 使用 gzip 进行压缩

Linux 和 Unix 系统提供了多种压缩工具供使用。Linux 系统的大多数软件使用 GNU `gzip` 和 `gunzip` 工具。`gzip` 工具用于压缩文件，

`gunzip` 用于解压它们。要压缩文件，输入命令 `gzip` 和文件名。这会将文件替换为具有 `.gz` 扩展名的压缩版本。

```
$ gzip mydata
$ ls
mydata.gz
```

要压缩一个 gzip 文件，请使用带有 `-d` 选项的 `gzip` 或 `gunzip` 命令。这些命令会压缩具有 `.gz` 扩展的压缩文件，并将其替换为具有相同根文件名但没有 `.gz` 扩展的解压版本。当你使用 `gzip` 时，甚至不需要输入 `.gz` 扩展；`gzip` 和 `gzip -d` 会自动假设它。表 12-8 列出了不同的 `gzip` 选项。

```
$ gzip mydata
$ ls
mydata
```

在桌面桌面上，你可以通过文件管理器找到存档并双击它来提取其内容。你也可以右键点击并选择“打开存档管理器”。这会启动 File Roller 程序，它将打开存档并列出其内容。然后你可以选择提取存档。如果 File Roller（bzip2、zip 或 gzip）是经过压缩的，将使用相应的工具解压存档（tar）。

| 选项 | 执行 |
| :--- | :--- |
| -c | 将文件的压缩版本发送到标准输出；每个文件单独列出：gzip -c mydata preface > myfiles.gz |
| -d | 解压压缩文件；或可以使用 gzip：gzip -d myfiles.gz gunzip myfiles.gz |
| -h | 显示帮助列表。 |
| -1 file-list | 显示列出的每个文件的压缩前和解压后的大小：gzip -1 myfiles.gz |
| -r directory-name | 递归搜索指定的目录并压缩其中的所有文件；搜索从当前工作目录开始。当与 gzip 使用时，指定目录的压缩文件会被解压。 |
| -v file-list | 对于每个压缩或解压的文件，显示其名称和大小缩减的百分比。 |
| -num | 决定压缩的速度和大小；范围从 -1 到 -9。数字越小，速度越快但压缩率越低，导致文件较大且压缩和解压速度快。因此，-1 压缩最快但体积最大；-9 产生一个非常小的文件，但压缩和解压需要更长时间。默认是 -6。 |

表 12-8 gzip 选项

## 第 12 章：文件、目录与存档 279

你也可以压缩归档过的 tar 文件。这将产生扩展名为 `.tar.gz` 的文件。压缩后的存档通常用于跨网络传输极大的文件。

```
$ gzip myarch.tar
$ ls
myarch.tar.gz
```

你可以使用调用 gzip 的 tar 选项逐个压缩 tar 文件的成员。使用 `z` 选项，会调用 `gzip` 在将文件放入存档之前进行压缩。然而，使用 `z` 选项压缩成员的存档无法更新，也无法添加。所有成员都必须压缩，且必须全部压缩。

## compress 和 decompress 命令

你可以使用 `compress` 和 `decompress` 创建 .Z 文件。`compress` 和 `decompress` 用于压缩解压 .Z 文件。`gzip` 工具是标准的压缩工具，应该用来代替 `compress`。

## 使用 bzip2 进行压缩

另一种流行的压缩工具是 `bzip2`。它使用 Burrows-Wheeler 排序算法和霍夫编码来压缩文件。其命令行选项设计上类似于 `gzip`，但并不完全相同（请参 bzip2 页面）。它分块压缩文件并允许你指定块的大小（块越大压缩率越高）。以下示例压缩 tar 文件。

```
$ bzip2 mydata
$ ls
mydata.bz2
```

要解压 bzip 文件，使用 `bunzip2` 命令：

```
$ bunzip2 mydata.bz2
```

## 使用 Zip

Zip 是一种基于 PKZIP 的压缩和存档工具，最初用于 DOS 系统。Zip 是一种跨平台工具，用于 Windows、Mac、MS-DOS、OS/2、Unix 和 Linux 系统。Zip 命令可以处理 PKZIP 创建的存档并使用 Zip 存档。使用 `zip` 命令压缩文件。这将创建一个具有 zip 扩展的文件。如果没有列出文件，zip 将压缩后的数据输出到标准输出。你还可以使用 - 参数让 zip 从标准输入读取。

要压缩目录，需要包含 `-r` 选项。此示例压缩了一个文件：

```
$ zip mydata
$ ls
mydata.zip
```

此示例归档并压缩了 **reports** 目录：

```
$ zip -r reports
```

它支持完整的存档操作集。使用 `-f` 选项，你可以更新 Zip 存档中的特定文件。`-u` 选项替换或添加文件，`-d` 选项从 Zip 存档中删除文件。还存在用于加密文件、进行 DOS 到 Unix 换行转换以及包含隐藏文件的选项。

要解压并提取 Zip 文件，你使用 **unzip** 命令：

```
$ unzip mydata.zip
```

# 第 13 章

# 办公与数据库应用程序

Linux 现在有多种办公套件可用（参见表 13-1）。这些包括专业级文字处理器、演示文稿管理器、绘图工具和电子表格。本章将介绍免费提供的版本。Sun（太阳公司）启动了使用 StarOffice 代码开发一个完全开源的办公套件。该应用程序被称为 OpenOffice.org，提供了与 GNOME 集成的 Office 应用程序，并且目前是大多数 Linux 发行版支持的主要应用程序。KOffice 是一个专为 KDE 设计的完全免费的办公套件。CodeWeavers 提供的 CrossOver 为直接在 Linux 上运行 Microsoft Windows 应用程序提供了可靠支持，并将其与 KDE 和 GNOME 集成。你也可以从 Sun 购买 StarOffice 等商业办公套件。对于桌面出版，特别是 PDF 生成，你可以使用 Scribus。

Linux 还提供了多种数据库管理系统。这些包括高商业级数据库管理系统，如 Oracle、IBM 的 DB2 等许多。也有开源系统可用，例如 MySQL 和 PostgreSQL。这些在 Linux 系统上用得最广泛。大多数适用于 Linux 的数据库管理系统都是为支持大型关系型数据库而设计的。对于个人数据库，你可以使用正在为 KDE 和 GNOME 开发的桌面数据库管理系统。此外，还有一些可以使用 HBase 语言访问数据库的软件。这些是最初为 PC 开发的格式的小型数据库。（可在 Linux 下运行的各种数据库管理系统列在本章稍后的表 13-8 中。）

Linux 还提供了几种文本编辑器，范围从用于笔记的简单文本编辑器到具有拼写检查器、缓冲区或模式匹配等复杂功能的编辑器不等。它们都能生成字符文本文件，并用于编辑任何 Linux 文本文件。文本编辑器通常用于系统管理任务，向位于 `/etc` 目录下的 Linux 配置文件或用户主目录下的用户初始化或应用程序点文件（dot files）添加条目。你可以使用任何文本编辑器处理任何编程语言或 shell 脚本的源代码文件。

# 第五部分：应用程序

| 网站 | 描述 |
| --- | --- |
| www.openoffice.org | 基于 StarOffice 的 OpenOffice.org 开源办公套件 |
| http://koffice.org | KOffice，适用于 KDE |
| http://live.gnome.org/GnomeOffice | GNOME Office，适用于 GNOME |
| www.sun.com/staroffice | StarOffice 套件 |
| www.codewavers.com | CrossOver (支持 MS Office) |
| www.scribus.net | Scribus 桌面出版工具 |

表 13-1 Linux 办公套件

# 在 Linux 上运行 Microsoft Office：CrossOver 和 Wine

Linux 用户主要关注的问题之一是他们将如何访问他们的 Microsoft Office 文件，特别是 Word 文件。Linux 操作系统及其应用程序设计为提供无缝访问 MS Office文件的能力。主要的 Linux 办公套件（包括 KOffice、OpenOffice.org 和 StarOffice）都能读取和管理任何 MS Office 文件。此外，办公套件在办公任务的功能和支持方面已非常接近 MS Office 的水平。

如果你想在 Linux 上运行任何 Windows 应用程序，有三个重要的替代方案：Wine Windows API 支持、VMware 平台技术以及 CodeWeavers 提供的 CrossOver Office。VMware 和 CrossOver 都是商业产品。

Wine 允许你使用支持的 Windows API 直接运行许多 Windows 应用程序。请访问 Wine 网站 (winehq.com) 查看支持的应用程序列表。良好的应用程序可能直接从 Wine 运行，如 NewsBin 阅读器所示。通常情况下，你需要一个运行良好的 Windows 系统，以便从中为特定应用程序复制系统 DLL。你也可以通过直接将字体复制到 Wine 字体目录来导入 Windows 字体。每个用户可以安装自己的 Wine 版本及其模拟的 c: 分区，Windows 应用程序安装在其中。模拟驱动器被安装为 `.wine` 目录中的 drive_c。wine 目录是一个隐藏目录。它通常不会通过 `ls` 命令或 GNOME 文件管理器显示。你也可以使用 Linux 的任何目录作为你的 Windows 应用程序数据文件，而不是使用模拟的 c: 盘。这些被 Windows 应用程序引用为 z: 盘。

在终端窗口中，使用 `wine` 命令配合安装程序将自动将应用程序安装在模拟的 c: 盘上。以下示例安装了 MS Office：

```bash
$ wine /media/OFFICE/setup.exe
```

虽然你在处理最新版本的 MS Office 时可能会遇到困难，但像 Office 2003 等早期版本应该不会产生问题。当你插入 Office 光盘时，它将挂载到 `/media` 目录，并使用光盘标签作为文件夹名称。检查 `/media` 文件夹（计算机窗口中的文件系统）以查看实际名称。然后你用 Wine 运行 Office 的 setup.exe 程序。根据 Office 的版本，你可能会遇到 Office setup.exe 程序的子文件夹。前面的示例假设 Office 的标签为 OFFICE，且 Office 的 setup.exe 程序位于光盘的顶层目录。

安装程序将启动，你会被提示输入产品密钥。输入时务必只使用大写字母。 应用程序 | Wine | Microsoft Office，然后选择应用程序名称以正常启动程序。如果你右键点击菜单项（例如 Microsoft Word），可以选择“创建快捷方式到桌面”以在桌面上添加该应用程序的图标。Wine 在用户模拟的 c 盘上引用该应用程序，其对应以下 Word：

```bash
wine "C:\Program Files\Microsoft Office\Office11\WINWORD.EXE"
```

“我的文档”（My Documents）文件夹由 Wine 设置为用户主目录。Wine 正在不断更新以适应最新版本的 Windows 应用程序。然而，对于某些应用程序，你可能需要从运行良好的系统复制 DLL 文件到 wine/drive_c/windows/system32。

尽管 Wine 有效，但其稳定性不如 CrossOver。CrossOver Office 是一种商业产品，你对其安装并运行 MS 应用。CrossOver 由 CodeWeavers 开发，还支持 Windows 插件以及 Photoshop 等流行的 Windows 应用程序。CrossOver 提供标准版和专业版，提供可靠的应用支持。你可以在 codeavers.com 了解 CrossOver。

CrossOver 可以按私有用户模式或用户模式安装。在私有用户模式下，每个用户安装自己的 Windows 软件（如 Office 完整版）。在用户模式下，Windows 软件安装一次，所有用户共享。
