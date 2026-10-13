
指定时，其所有子目录都包含在归档中。

```
$ tar options f archive-name.tar directory-and-file-names
```

创建归档时，使用 c 选项。结合 f 选项，c 会在文件或设备上创建归档。你需要在 f 选项之前并紧挨着它输入此选项。请注意 tar 选项前没有前导短横线。表 10-7 列出了可与 tar 一起使用的不同选项。在下一个示例中，目录 mydir 及其所有子目录都保存在文件 myarch.tar 中。在此示例中，mydir 目录包含两个文件 mymeeting 和 party，以及一个名为 reports 的目录，其中包含三个文件：weather、monday 和 friday。

```
$ tar cvf myarch.tar mydir
```

```
mydir/
mydir/reports/
mydir/reports/weather
mydir/reports/monday
mydir/reports/friday
mydir/mymeeting
mydir/party
```

表 10-7：文件归档：tar

| 命令 | 执行 |
|---|---|
| `tar options files` | 将文件备份到磁带、设备或归档文件。 |
| `tar options f archive_name filelist` | 将文件备份到指定为 archive_name 的特定文件或设备。filelist：可以是文件名或目录。 |
| 选项 |  |
| `c` | 创建新的归档。 |
| `t` | 列出归档中文件的名称。 |
| `r` | 将文件追加到归档。 |
| `U` | 使用新文件和已更改文件更新归档；仅添加自归档以来被修改的文件或归档中尚未存在的文件。 |
| `--delete` | 从归档中删除文件。 |
| `w` | 在归档每个文件之前等待用户确认；可让你有选择地更新归档。 |
| `x` | 从归档中提取文件。 |
| `m` | 提取归档中的文件时，不分配新的时间戳。 |
| `M` | 创建可存储在多个软盘上的多卷归档。 |
| `f archive-name` | 将磁带归档保存到文件 archive name，而不是默认磁带设备。当给出归档名称时，f 选项将 tar 归档保存到该名称的文件中。 |
| `f device-name` | 将 tar 归档保存到软盘或磁带等设备。/dev/fd0 是软盘的设备名称；默认设备保存在 /etc/default/tar 中。 |
| `v` | 在归档时显示每个文件名。 |
| `z` | 使用 gzip 压缩或解压缩归档文件。 |
| `j` | 使用 bzip2 压缩或解压缩归档文件。 |

## 提取归档

用户稍后可以使用 x 选项从磁带中提取目录。xf 选项从归档文件或设备中提取文件。tar 提取操作会生成所有子目录。在下一个示例中，xf 选项指示 tar 从 tar 文件 myarch.tar 中提取所有文件和子目录：

```
$ tar xvf myarch.tar
mydir/
mydir/reports/
mydir/reports/weather
mydir/reports/monday
mydir/reports/friday
mydir/mymeeting
mydir/party
```

你可以使用 r 选项向已创建的归档中添加文件。r 选项将文件追加到归档。在下一个示例中，用户将 letters 目录中的文件追加到 myarch.tar 归档。这里，目录 mydocs 及其文件被添加到 myarch.tar 归档中：

```
$ tar rvf myarch.tar mydocs
mydocs/
mydocs/doc1
```

## 更新归档

如果你更改了之前归档的目录中的任何文件，可以使用 u 选项指示 tar 用任何已修改的文件更新归档。tar 命令会将每个归档文件的最后更新时间与用户目录中的时间进行比较，并将自上次归档以来被更改的文件复制到归档中。这些目录中新建的文件也会被添加到归档中。在下一个示例中，用户使用 mydir 目录中最近修改或新创建的文件更新 myarch.tar 文件。在此情况下，gifts 文件被添加到 mydir 目录。

```
tar uvf myarch.tar mydir
mydir/
mydir/gifts
```

如果需要查看归档中存储的文件，可以使用 t 选项运行 tar 命令。下一个示例列出存储在 myarch.tar 归档中的所有文件：

```
tar tvf myarch.tar
drwxr-xr-x root/root 0 2000-10-24 21:38:18 mydir/
drwxr-xr-x root/root 0 2000-10-24 21:38:51 mydir/reports/
-rw-r--r-- root/root 22 2000-10-24 21:38:40 mydir/reports/weather
-rw-r--r-- root/root 22 2000-10-24 21:38:45 mydir/reports/monday
-rw-r--r-- root/root 22 2000-10-24 21:38:51 mydir/reports/friday
```

```
-rw-r--r-- root/root 22 2000-10-24 21:38:18 mydir/mymeeting
-rw-r--r-- root/root 22 2000-10-24 21:36:42 mydir/party
drwxr-xr-x root/root 0 2000-10-24 21:48:45 mydocs/
-rw-r--r-- root/root 22 2000-10-24 21:48:45 mydocs/doc1
drwxr-xr-x root/root 0 2000-10-24 21:54:03 mydir/
-rw-r--r-- root/root 22 2000-10-24 21:54:03 mydir/gifts
```

## 归档到软盘

要将文件备份到特定设备，请将设备指定为归档。对于软盘，可以指定软盘驱动器。请确保使用空白软盘。此操作会擦除其上之前放置的任何数据。在下一个示例中，用户在 /dev/fd0 设备中的软盘上创建归档，并将 mydir 目录中的所有文件复制到其中：

```
$ tar cf /dev/fd0 mydir
```

要从设备中的磁盘提取备份文件，请使用 xf 选项：

```
$ tar xf /dev/fd0
```

如果要归档的文件占用空间超过软盘等设备可用的空间，你可以创建使用多个卷标的 tar 归档。M 选项指示 tar 在当前存储组件填满时提示你提供新的存储组件。当使用 M 选项归档到软盘驱动器时，tar 会在软盘填满时提示你放入新的软盘。然后你可以将 tar 归档保存在多个软盘上。

```
$ tar cMF /dev/fd0 mydir
```

要解包多磁盘归档，请将第一张盘放入软盘驱动器，然后使用 x 和 M 选项发出以下 tar 命令。然后会提示你按需放入其他软盘。

```
$ tar xMf /dev/fd0
```

## 压缩归档

tar 操作不会对归档文件执行压缩。如果要压缩归档文件，可以指示 tar 调用 gzip 实用程序来压缩它们。使用小写 z 选项时，tar 会先使用 gzip 压缩文件，然后再归档。提取文件时，相同的 z 选项会调用 gzip 进行解压缩。

```
$ tar czf myarch.tar.gz mydir
```

要改用 bzip2 而不是 gzip 在归档前压缩文件，可以使用 j 选项。提取文件时，相同的 j 选项会调用 bzip2 进行解压缩。

```
$ tar cjf myarch.tar.bz2 mydir
```

请记住，压缩归档中单个文件的压缩与压缩整个归档之间存在区别。通常，归档是为了将多个文件作为一个 tar 文件一起传输。为了缩短传输时间，归档应尽可能小。你可以使用压缩实用程序 gzip 对归档 tar 文件进行压缩，减少其大小，然后发送压缩版本。接收者可以将其解压缩，还原 tar 文件。对 tar 文件使用 gzip 通常会产生扩展名为 .tar.gz 的文件。扩展名 .gz 添加到被 gzip 压缩的文件上。下一个示例使用相同名称并加上 .gz 扩展名创建 myarch.tar 的压缩版本：

```
$ gzip myarch.tar
$ ls
myarch.tar.gz
```

## 归档到磁带

如果已指定默认设备，例如磁带，并且要在其上创建归档，可以直接使用 tar，而不使用 f 选项和设备或文件名。这对于备份文件很有帮助。默认设备的名称保存在名为 /etc/default/tar 的文件中。以下示例显示了使用默认磁带设备的 tar 命令的语法。如果指定目录名，其所有子目录都包含在归档中。

```
$ tar option directory-and-file-names
```

在下一个示例中，目录 mydir 及其所有子目录都保存在默认磁带设备上的磁带中：

```
$ tar c mydir
```

在此示例中，mydir 目录及其所有文件和子目录从默认磁带设备中提取并放置在用户的当前工作目录中：

```
$ tar x mydir
```
