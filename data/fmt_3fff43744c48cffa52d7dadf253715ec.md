
使用 `mdel` 删除 DOS 磁盘上的文件。通过要删除磁盘的“驱动器号”提供要删除的文件作为参数。

- ⇒ 要删除主软盘中 DOS 磁盘上的 `resume.doc`，请输入：

```
$ mdel a:
```

### 26.1.4 格式化 DOS 磁盘

要格式化 DOS 磁盘，将要格式化的文件名和要格式化的磁盘的“驱动器号”作为参数。

- ⇒ 要格式化主软盘中的磁盘，请输入：

```
$ mformat a: RET
```

# 第 26 章：跨平台转换

## 26.2.5 格式化 Macintosh 磁盘

要为 Macintosh 格式化磁盘，可以使用 `hformat` 向磁盘写入一个空的 HFS 文件系统。将磁盘驱动器的 Linux 设备文件作为参数提供；例如，第一个软驱动器的设备文件为 `/dev/fd0`，第二个驱动器为 `/dev/fd1`。

- ⇒ 要将第一个软驱动器中的磁盘格式化为 Macintosh HFS 文件系统，输入：

```
hformat /dev/fd0 RET
```

如果磁盘上已存在分区，此命令将无法工作；请使用 `-f` 选项强制格式化，这将删除磁盘中包含的任何现有分区和数据。

使用 `-1` 选项的参数为驱动器指定一个标签。标签名称不能包含冒号 (`:`)。

- ⇒ 这里有两种使用方法。

- 要将第一个软驱动器中的磁盘格式化为 Macintosh HFS 文件系统，并覆盖任何现有的 Macintosh 文件系统，输入：

```
hformat -f /dev/fd0 RET
```

- 要将第二个软驱动器中的磁盘格式化为 Macintosh HFS 文件系统，并为其指定卷标签“Work Disk”，输入：

```
hformat -1 'Work Disk' /dev/fd1 RET
```

当磁盘有多个分区时，请将要格式化的分区编号作为额外参数。要格式化整个介质，请提供“0”作为要使用的分区号。

- ⇒ 这里有两种使用方法。

- 要将 `/dev/sd2` SCSI 磁盘的第二个分区格式化为 Macintosh HFS 文件系统，输入：

```
hformat /dev/sd2 RET
```

- 要将 `/dev/sd2` 整个 SCSI 磁盘格式化为 Macintosh HFS 文件系统，覆盖任何现有的 Macintosh 文件系统并为其指定标签“Joe's Work Disk”，输入：

```
hformat -1 'Joe's Work Disk' /dev/sd2 0 RET
```

## 26.3 挂载 Windows 和 NT 分区

如果你的 Linux 内核支持 VFAT 文件系统，就可以挂载 Windows 分区；如果你的内核支持 NTFS 文件系统，就可以挂载 NT 分区（只读）。

- ⇒ 要将设备 `/dev/hdd1` 上的 Windows 分区挂载到 `/home/roger/mywin`，输入：

```
$ -t vfat /dev/hdd1 /home/roger/mywin RET
```

上一个示例中的命令使 `/dev/hdd1` 上的 Windows 分区在 `/home/roger/mywin` 目录下供 Linux 使用。

- ⇒ 要将设备 `/dev/hea1` 上的 Windows NT 分区挂载到 `/mnt`，输入：

```
$ -t ntfs /dev/hea1 /mnt RET
```

上一个示例使 `/dev/hea1` 上的 Windows NT 分区以只读文件系统的形式在 `/mnt` 目录下供 Linux 使用。

## 26.4 在 DOS 和 Linux 之间转换文本文件

在所有版本的 DOS（以及后续的所有 Microsoft Windows）中，文本文件通常包含回车符和换行符（两者都是“不可见”的控制字符），用来表示每行的结束。在 Linux 和其他 Unix 系统中，文本文件只有换行符。

在这些操作系统中，源自另一个操作系统的文本文件可能会显示异常——在 DOS 和 Windows 中，Linux 文本文件的内容可能看起来连在一起了；在 Linux 中，DOS 或 Windows 文本文件的每行末尾可能会有 `~M` 回车符。

有几种方法可以在这两种系统之间转换文本。

### 方法 #1

- `Tofrodos`

DEB: `tosysutils`

RPM: `tofrodos`

WWW: `http://www.uni-kassel.de/hrz/server/Software/dos2unix/`

`fromdos` 和 `todos` 工具允许你在 DOS 和 Linux 之间转换文本文件。

要将文本文件从 DOS 转换为 Linux（移除文件中的 `~M` 字符），请使用 `fromdos`。它会转换你作为参数提供的文本文件，移除所有行尾的换行符。

要将文本文件从 Linux 转换为 DOS 和 Windows 使用的格式，请使用 `todos`。它会在你作为参数提供的文件的行尾添加换行符。

- ⇒ 这里有两种使用方法。

- 要移除文本文件 `autoexec.bat` 中的换行符，输入：

```
$ fromdos autoexec.bat RET
```

- 要为当前目录下所有 `.tex` 扩展名的文本文件添加换行符，输入：

```
$ todos *.tex RET
```

注意：这两个命令都会直接写入你指定的文件。要为原始文件制作备份，请使用 `-b` 选项；在转换之前，这会为每个指定的文件创建一个带有 `.bak` 扩展名的副本。

### 方法 #2

使用 `col` 过滤器过滤掉文本中的回车符，如第 310 页食谱 13.1.9 [移除回车符]所示。

- ⇒ 要过滤文件 `README.TXT` 中的回车符并写入名为 `readme.txt` 的新文件，输入：

```
$ col < README.TXT > readme.txt RET
```

### 方法 #3

另一种从 DOS 转换的方法是使用 `tr` 过滤器删除回车符（参见第 316 页食谱 13.4 [文本中的字符转换]）。

- ⇒ 要过滤文件 `README.TXT` 中的回车符并写入名为 `readme.txt` 的新文件，输入：

```
$ tr -d '\r' < README.TXT > readme.txt RET
```

注意：`tr -d` 选项删除指定的字符。这是移除回车符的一种快速方法。

ZIP 文件压缩通过一个或多个文件并将它们压缩成一个具有 `.zip` 扩展名的新文件。这是大多数初次接触 Linux 或通用 UNIX 系统的人在提到“文件归档”时会想到的。但在 UNIX 世界中，文件归档和压缩是独立的工具，尽管它们通常是配合配合的。我们会创建压缩的 tar 归档（参见食谱 8.5 [管理文件归档]，第 199 页）。然后我们可以使用 `gzip` 或 `bzip2` 压缩这些归档或其他任何文件（参见食谱 8.4 [使用文件压缩]，第 196 页）。

在与使用其他操作系统的用户收发文件时，通常使用 ZIP 归档格式。`zip` 和 `unzip` 工具可以像其他操作系统流行的 PKZIP 工具一样创建和提取 ZIP 归档。

以下食谱展示了如何使用这些工具。

## 26.7.1 压缩文件

使用 `zip` 创建一个文件或一组文件的 ZIP 归档。接收的参数是要创建的 ZIP 归档名称以及放入归档的文件规格。

为归档名称提供 `.zip` 扩展名是可选的；如果归档已存在，则给定的文件将被添加到归档中。

- 这里有两种使用此方法。

- 要制作一个包含当前目录下所有 `.png` 文件的 ZIP 归档文件 `zippy.zip`，输入：

```
$ zip zippy *.png
```

- 要将当前目录下所有的 `.tiff` 文件添加到现有的 ZIP 归档文件 `zippy.zip` 中，输入：

```
$ zip zippy *.tiff
```

在指定目录时，如果只给出目录名称，则该目录本身（而不包含其内容）将被包含在归档中。在目录中指定通配符将包含其所包含的文件和任何子目录名称，但它不会进入这些子目录来包含其中可能存在的任何文件。使用 `-r` 选项可以递归进入任何指定的目录，从而包含其内容。

- 要制作一个包含当前目录下所有文件的 ZIP 归档 `zippy.zip`，输入：

```
$ zip zippy *
```

如果当前目录包含任何目录，这些目录名称将包含在 ZIP 归档中，但不会包含它们的任何内容。

要制作一个包含当前目录下所有文件以及 `addons` 目录下所有文件的 ZIP 归档 `zippy.zip`，输入：
