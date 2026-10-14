

$ hls RET

作为带引号的参数给出目录的名称。

- 要列出当前指定的 Macintosh 磁盘中 `Desktop Folder` 目录的内容，输入：

```
$ hls 'Desktop Folder' RET
```

## 27.2.3 Copying Files to and from a Macintosh Disk

使用 hcopy 将文件复制到使用 hmount 当前指定的 Macintosh 磁盘，或从该磁盘复制文件（参见章节 Specifying the Macintosh Disk to Use）。

要将文件复制到 Mac 磁盘上，将源文件名作为参数给出，并将 Mac 磁盘上的目标目录名作为带引号的参数给出。

- 要将文件 `readme.txt` 复制到当前 Mac 磁盘中的 `Desktop Folder` 目录，输入：

```
$ hcopy readme.txt 'Desktop Folder' RET
```

要从 Mac 磁盘复制文件，将要复制的目录和文件名作为带引号的参数给出，并给出要复制到的目标目录名。

- 要将文件 `Desktop Folder:Readme` 从当前 Mac 磁盘复制到当前目录，输入：

```
$ hcopy 'Desktop Folder:Readme' . RET
```

## 27.2.4 Deleting Files on a Macintosh Disk

使用 hdel 删除使用 hmount 当前指定的 Macintosh 磁盘上的文件（参见章节 Specifying the Macintosh Disk to Use）。将要删除的文件路径名作为带引号的参数给出。它会删除你指定的文件的资源分支和数据分支。

- 要删除当前 Mac 磁盘上的文件 `Desktop Folder:Readme`，输入：

```
$ hdel 'Desktop Folder:Readme' RET
```

## 27.2.5 Formatting a Macintosh Disk

要为 Mac 格式化磁盘，将空的 HFS 文件系统写入磁盘，使用 hformat。将磁盘所在的 Linux 设备文件名作为参数给出；例如，第一个软盘驱动器的设备文件是 `/dev/fd0`，第二个驱动器是 `/dev/fd1`

- 要使用 Macintosh HFS 文件系统格式化第一个软盘驱动器中的磁盘，输入：

```
$ hformat /dev/fd0 RET
```

如果磁盘上当前已有分区，此命令将无法工作；使用 `-f` 选项强制格式化，从而擦除磁盘上任何现有的分区和数据。

将驱动器的标签作为带引号的参数给出给 `-l` 选项。标签名不能包含冒号字符（`:`）。

- 要使用 Mac HFS 文件系统格式化第一个软盘驱动器中的磁盘，覆盖任何现有的 Mac 文件系统，输入：

```
$ hformat -f /dev/fd0 RET
```

- 要使用 Mac HFS 文件系统格式化第二个软盘驱动器中的磁盘，并为其指定卷标为 `Work Disk`，输入：

```
$ hformat -l 'Work Disk' /dev/fd1 RET
```

当磁盘具有多个分区时，将要格式化的分区号作为额外参数给出。要格式化整个介质，将 `0` 作为要使用的分区给出。

- 要使用 Mac HFS 文件系统格式化 SCSI 磁盘 `/dev/sd2` 的第二个分区，输入：

## 27.4 Converting Microsoft Word Files

`@sf{Debian}: `word2x`\
`@sf{WWW}: http://word2x.alcom.co.uk/`

使用 word2x 将 Word 6 文件转换为可读的格式。它可以将文件转换为两种不同的格式：LaTeX 和纯文本。

当原始文档的 *layout*，包括其格式和字体特征很重要时，转换为 LaTeX。当你只需要文档的完整 *text* 时，将其转换为纯文本。`word2x` 可以将其输出发送到标准输出，因此后一种转换对于添加到管道很有用。

Word 文件通常具有 `.doc` 或 `.DOC` 扩展名，你不必指定——例如，如果你要转换的 Word 文件名为 `resume.doc`，你可以简单地给出 `resume` 作为源文件。（但如果同一目录中存在另一个名为 `resume` 的文件，此技巧将不起作用。）

如果不指定输出文件，`word2x` 会将其输出写入具有相同基本文件名的文件，并使用适合输出格式的扩展名。这对于转换同一目录中的大量 Word 文件很有用——指定诸如 `*.doc` 之类的通配符作为输入且不指定输出名称将转换它们全部。

你还可以设置输出文件使用的最大行宽；将宽度作为 `-w` 选项的参数指定。

以下配方描述了如何使用 `word2x` 将 Word 文件转换为 LaTeX 和纯文本格式。

**NOTE:** 虽然 `word2x` 在转换方面做得相当不错，但它不会转换嵌入在 Word 文档中的任何图片。

另一种读取 Word 文件的方法是将其导入 AbiWord 或 StarWriter 文字处理器（参见章节 [Other Word Processors and Typesetting Systems](#)）。

- [27.4.1 Converting Word to LaTeX](#)
- [27.4.2 Converting Word to Plain Text](#) — Converting Word to plain text.

## 27.4.1 Converting Word to LaTeX

要将 Word 文件转换为 LaTeX 格式，使用 `word2x` 并将 `latex` 作为 `-f` 选项的参数使用。

