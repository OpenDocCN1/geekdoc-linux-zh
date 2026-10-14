

## 26. 跨平台转换

有时候，这不可避免——出于无奈，你必须处理来自其他操作系统的磁盘，或来自这些系统中以专有格式存储数据的文件。

本章的示例涉及从其他平台转换数据——读取 DOS、Windows 和 MacOS 系统的磁盘，以及转换 DOS 文本和 Microsoft Word 文件。

如需在不同格式之间转换图像文件，请参见第432页的示例18.2 [转换图像文件]；如需在不同格式之间转换音频文件，请参见第493页的示例23.3 [转换声音文件]。

### 26.1 使用 DOS 和 Windows 磁盘

Mtools
DEB: mtools
RPM: mtools
WWW: http://mtools.linux.lu/

mtools 软件包提供了一套工具，用于方便地操作 MS-DOS 文件。这些工具允许你在不挂载的情况下使用和操作 MS-DOS 磁盘（通常是软盘，但也支持 Jaz 和 Zip 驱动器）；它们能够处理不同 Microsoft Windows 操作系统（包括 Windows NT）所使用的 MS-DOS 格式扩展。

以下示例描述了如何使用该软件包中的一些工具来获取 MS-DOS 磁盘的目录列表、在磁盘间复制文件、删除磁盘上的文件，甚至格式化磁盘。它们的使用方法和语法与等效的 MS-DOS 命令类似。

你也可以挂载 DOS 和 Windows 磁盘（参见第529页的示例26.3 [挂载 Windows 和 NT 分区]）。

### 26.1.1 列出 DOS 磁盘的内容

使用 mdir 获取 DOS 磁盘的目录列表。将磁盘的“盘符”作为参数给出，与 DOS 使用的盘符一致。例如，要指定主软驱，请使用“A:”作为要读取的驱动器，使用“B:”指定副软驱。

⇒ 要格式化主软驱中的软盘，使其可用于 MS-DOS，请键入：

```
$ mformat a: [回车]
```

注意：如果你想将软盘用于 Linux 系统且不需要 DOS 兼容性，不必使用这种 MS-DOS 格式——Linux 原生格式效率更高（参见第504页的示例24.3.1 [格式化软盘]）。如果你知道 DOS 格式化需要多长时间，你会惊讶于 Linux 格式化速度之快——快得让你以为它根本没运行！

### 26.2 使用 Macintosh 磁盘

Hfsutils
DEB: hfsutils
RPM: hfsutils
WWW: http://www.mars.org/home/rob/proj/hfs/

Apple Macintosh 计算机使用一种称为“分层文件系统”（Hierarchical File System，简称 HFS）的文件系统。如果你的内核支持 HFS 文件系统，你可以使用 mount 命令并指定“hfs”作为 -t 选项的参数来挂载这些系统的磁盘（参见第504页的示例24.3.2 [挂载软盘]）。

你也可以使用 hfsutils 软件包来使用这些磁盘，该软件包包含一套用于读写 HFS 文件系统的工具。以下示例描述了该软件包中各工具的使用方法。

### 26.2.1 指定要使用的 Macintosh 磁盘

要将 Macintosh 磁盘与任何 hfsutils 命令一起使用，必须先使用 hmount 指定 HFS 文件系统的位置。将 HFS 文件系统所在的 Linux 设备文件名作为参数给出；这会虚拟地“挂载”该磁盘，供本节描述的其他命令使用。

第一个软驱的设备文件是 /dev/fd0，第二个软驱的是 /dev/fd1。任何有效的设备名称，如 SCSI 设备或 Zip 磁盘，都可以给出。

⇒ 要将第一个软驱中的软盘作为 HFS 卷引入给 hfsutils，请键入：

```
$ hmount /dev/fd0 [回车]
```

运行此命令后，hfsutils 软件包中的其他工具将作用于第一个软驱中的 Macintosh 磁盘。

### 26.2.2 列出 Macintosh 磁盘的内容

使用 hls 获取当前通过 hmount 指定的 Macintosh 磁盘的目录列表（参见前面的示例）。

⇒ 要获取当前指定 Macintosh 磁盘的目录列表，请键入：
$ hls [回车]

将目录名作为带引号的参数给出，以仅列出该目录。

⇒ 要获取当前指定 Macintosh 磁盘中 Desktop Folder 目录的目录列表，请键入：
$ hls 'Desktop Folder' [回车]

### 26.2.3 向 Macintosh 磁盘复制文件或从中复制文件

使用 hcopy 向当前通过 hmount 指定的 Macintosh 磁盘复制文件或从中复制文件（参见第527页的示例26.2.1 [指定要使用的 Macintosh 磁盘]）。

要将文件复制到 Macintosh 磁盘，请给出要复制的源文件名以及 Macintosh 磁盘上带引号的目标目录名作为参数。

⇒ 要将文件 readme.txt 复制到当前 Macintosh 磁盘的 Desktop Folder 目录中，请键入：
$ hcopy readme.txt 'Desktop Folder' [回车]

要从 Macintosh 磁盘复制文件，请给出两个参数：目录名和要复制的文件名（作为带引号的参数），以及要复制到的 Linux 目标目录名。请记住，MacOS 使用冒号字符（:）作为路径上的分隔符。

⇒ 要将文件 Desktop Folder:Readme 从当前 Mac 磁盘复制到当前目录，请键入：
$ hcopy 'Desktop Folder:Readme' . [回车]

### 26.2.4 删除 Macintosh 磁盘上的文件

使用 hdel 删除当前通过 hmount 指定的 Macintosh 磁盘上的文件（参见第527页的示例26.2.1 [指定要使用的 Macintosh 磁盘]）。将要删除文件的路径名作为带引号的参数给出。它会同时删除你指定文件的资源分支和数据分支。

⇒ 要删除当前 Macintosh 磁盘上的文件 Desktop Folder:Readme，请键入：
$ hdel 'Desktop Folder:Readme' [回车]

