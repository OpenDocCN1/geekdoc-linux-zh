
| `f archive-name` | Saves the tape archive to the file `archive name`, instead of to the default tape device. When given an `archive name`, the `f` option saves the `tar` archive in a file of that name. |
| `f device-name` | Saves a `tar` archive to a device such as a floppy disk or tape. `/dev/fd0` is the device name for your floppy disk; the default device is held in `/etc/default/tar-file`. |
| `v` | Displays each filename as it is archived. |
| `z` | Compresses or decompresses archived files using `gzip`. |
| `j` | Compresses or decompresses archived files using `bzip2`. |

## 提取归档文件

用户稍后可以使用 `x` 选项从磁带中提取目录。`xvf` 选项从归档文件或设备中提取文件。`tar` 提取操作会生成所有子目录。在下一个示例中，`xvf` 选项指示 `tar` 从 `tar` 文件 `myarch.tar` 中提取所有文件和子目录：

```
$ tar xvf myarch.tar
mydir/
mydir/reports/
mydir/reports/weather
mydir/reports/monday
mydir/reports/friday
mydir/meeting
mydir/party
```

你使用 `r` 选项向已创建的归档中添加文件。`r` 选项将文件追加到归档中。在下一个示例中，用户将 `letters` 目录中的文件追加到 `myarch.tar` 归档中。这里，目录 `mydocs` 及其文件被添加到 `myarch.tar` 归档中：

```
$ tar rvf myarch.tar mydocs
mydocs/
mydocs/doc1
```

## 更新归档

如果更改了之前归档的目录中的任何文件，你可以使用 `u` 选项指示 `tar` 用任何已修改的文件更新归档。`tar` 命令比较每个归档文件的最后更新时间与用户目录中的时间，并将自上次归档以来被更改的任何文件复制到归档中。这些目录中创建的任何新文件也会被添加到归档中。在下一个示例中，用户使用 `mydir` 目录中最近修改或新创建的任何文件更新 `myarch.tar` 文件。在这种情况下，`gifts` 文件被添加到 `mydir` 目录。

```
tar uvf myarch.tar mydir
mydir/
mydir/gifts
```

如果需要查看归档中存储了哪些文件，可以使用 `t` 选项运行 `tar` 命令。下一个示例列出存储在 `myarch.tar` 归档中的所有文件：

```
tar tvf myarch.tar
drwxr-xr-x root/root 0 2000-10-24 21:38:18 mydir/
drwxr-xr-x root/root 0 2000-10-24 21:38:51 mydir/reports/
-rw-r--r-- root/root 22 2000-10-24 21:38:40 mydir/reports/weather
-rw-r--r-- root/root 22 2000-10-24 21:38:45 mydir/reports/monday
-rw-r--r-- root/root 22 2000-10-24 21:38:51 mydir/reports/friday
-rw-r--r-- root/root 22 2000-10-24 21:38:11 mydir/meeting
-rw-r--r-- root/root 22 2000-10-24 21:36:42 mydir/party
drwxr-xr-x root/root 0 2000-10-24 21:48:45 mydocs/
-rw-r--r-- root/root 22 2000-10-24 21:48:45 mydocs/doc1
drwxr-xr-x root/root 0 2000-10-24 21:54:03 mydir/
-rw-r--r-- root/root 22 2000-10-24 21:54:03 mydir/gifts
```

## 归档到软盘

要将文件备份到特定设备，请将设备指定为归档。对于软盘，你可以指定软盘驱动器。确保使用空白软盘。此操作会擦除其上之前放置的任何数据。在下一个示例中，用户在 `/dev/fd0` 设备上的软盘上创建归档，并将 `mydir` 目录中的所有文件复制到其中：

```
$ tar cf /dev/fd0 mydir
```

要提取设备上磁盘上的备份文件，请使用 `xf` 选项：

```
$ tar xf /dev/fd0
```

如果你要归档的文件占用的空间超过软盘等设备可用的空间，你可以创建使用多个卷标的 `tar` 归档。`M` 选项指示 `tar` 在当前存储组件填满时提示你输入新的存储组件。当使用 `M` 选项归档到软盘驱动器时，`tar` 会在软盘填满时提示你放入新的软盘。然后你可以将 `tar` 归档保存在多个软盘上。

```
$ tar cMF /dev/fd0 mydir
```

要解包多磁盘归档，请将第一个磁盘放入软盘驱动器，然后使用 `x` 和 `M` 选项发出以下 `tar` 命令。然后在需要时提示你放入其他软盘。

```
$ tar xMF /dev/fd0
```

## 压缩归档

`tar` 操作不对归档文件执行压缩。如果要压缩归档文件，可以指示 `tar` 调用 `gzip` 实用程序来压缩它们。使用小写 `z` 选项，`tar` 首先使用 `gzip` 压缩文件，然后再归档。相同的 `z` 选项在提取文件时调用 `gzip` 进行解压缩。

```
$ tar czf myarch.tar.gz mydir
```

要使用 `bzip` 而不是 `gzip` 在归档前压缩文件，你使用 `j` 选项。相同的 `j` 选项在提取文件时调用 `bzip` 进行解压缩。

```
$ tar cjf myarch.tar.bz2 mydir
```

请记住，压缩归档中单个文件与压缩整个归档之间存在区别。通常，归档是为了将多个文件作为一个 `tar` 文件一起传输。为了缩短传输时间，归档应尽可能小。你可以使用压缩实用程序 `gzip` 对归档 `tar` 文件进行压缩，减少其大小，然后发送压缩版本。接收者可以对其进行解压缩，还原 `tar` 文件。使用 `gzip` 对 `tar` 文件进行压缩通常会得到扩展名为 `.tar.gz` 的文件。扩展名 `.gz` 会添加到被 `gzip` 压缩的文件中。下一个示例使用相同名称并添加 `.gz` 扩展名创建 `myarch.tar` 的压缩版本：

## 归档到磁带

如果您已指定默认设备，例如磁带，并且想要在上面创建归档，您可以简单地使用 `tar` 而不带 `f` 选项和设备或文件名。这对于备份文件非常有帮助。默认设备的名称保存在名为 `/etc/default/tar` 的文件中。以下是使用默认磁带设备时 `tar` 命令的语法示例。如果指定了目录名，则其所有子目录都包含在归档中。

```
$ tar option directory-and-file-names
```

在下一个示例中，目录 `mydir` 及其所有子目录都保存到默认磁带设备上的磁带中：

```
$ tar c mydir
```

在此示例中，`mydir` 目录及其所有文件和子目录从默认磁带设备中提取并放置在用户的当前工作目录中：

```
$ tar x mydir
```

> 注意 还有其他归档程序可以使用，例如 `cpio` 和 `shar`。但是，`tar` 是用于归档应用程序软件时最常用的。

## 文件压缩：`gzip`、`bzip2` 和 `zip`

存在多种减少文件大小的原因。最常见的两个原因是节省空间，或如果您通过网络传输文件，则节省传输时间。您可以通过创建文件的压缩副本来有效地减小文件大小。每次需要文件时，您都可以对其进行解压缩。压缩通常与归档结合使用，以便您可以一次性压缩整个目录及其文件。解压缩会生成归档文件的副本，然后可以将其提取，从而生成这些文件和目录的副本。文件卷管理器提供了一个 GUI 界面来执行这些任务。

## 使用 `gzip` 压缩

Linux 和 Unix 系统上可用的压缩实用程序有多种。Linux 系统的大多数软件使用 GNU `gzip` 和 `gunzip` 实用程序。`gzip` 实用程序压缩文件，而 `gunzip` 解压缩它们。要压缩文件，请输入命令 `gzip` 和文件名。这会用压缩版本替换该文件，并带有 `.gz` 扩展名。

```
$ gzip mydata
$ ls
mydata.gz
```
