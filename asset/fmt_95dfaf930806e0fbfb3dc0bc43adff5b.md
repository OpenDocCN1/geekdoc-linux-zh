
- 数据叉存储在一个文件中。
- 资源叉位于子目录 `resource.frk`（或 `RESOURCE.FRK`）中。
- Finder 信息是文件 `finder.dat`（或 `FINDER.DAT`）中的一条记录。
- 每个数据叉目录有单独的 `finder.dat`。

注意：`genisoimage` 需要知道 PC Exchange 文件所在（或复制自）磁盘的原生 FAT 簇大小。该大小由 `-cluster-size` 给出。可以使用 DOS 实用工具 `chkdsk` 找到簇大小或分配大小。可能无法用于 PC Exchange v2.2 或更高版本的文件（随 MacOS 8.1 提供）。

在 Linux 下使用时，包含 PC Exchange 文件的 DOS 介质应以 `msdos` 类型挂载（而不是 `vfat`）。

### SGI/XINET

用于 SGI 机器挂载 HFS 磁盘时。数据叉存储在一个文件中。资源叉位于同名文件位于子目录 `.HSResource` 中。Finder 信息是文件 `.HSAncillary` 中的一条记录。每个数据叉目录有单独的 `.HSAncillary`。

### Thursby Software Systems DAVE

允许 Macintosh 在 SMB 服务器上存储 Apple 文件。数据叉存储在一个文件中。资源叉位于子目录 `resource.frk` 中。使用 AppleDouble 格式存储资源叉。

### Services for Macintosh

由 NT 服务器在 NTFS 文件系统上存储的文件格式。数据叉作为文件名存储。资源叉存储为名为 `filename:AFP_Resource` 的 NTFS 流。Finder 信息存储为名为 `filename:Ap_fApInfo` 的 NTFS 流。NTFS 流通常对用户不可见。

警告：`genisoimage` 仅部分支持 SFM 格式。如果存储在 NT 服务器上的 HFS 文件或文件夹的名称中包含非法 NT 字符，NT 会将这些字符转换为 Private Use Unicode 字符。这些字符是：`” * / < > ? \ |` 以及文件名最后一个字符如果是空格或句点，还有控制字符代码 `0x01` 到 `0x1f` 以及 Apple 的苹果标志。

不幸的是，这些私有 Unicode 字符无法被 `genisoimage` NT 可执行文件读取。因此，包含这些字符的任何文件或目录名称将被忽略——包括此类目录的内容。

### Mac OS X AppleDouble

当 HFS/HFS+ 文件通过 Mac OS X 复制到非 HFS 文件系统（如 UFS、NFS 等）时，文件以 AppleDouble 格式存储。数据叉存储在一个文件中。资源叉存储在与数据叉同名但前缀为 `_` 的文件中。Finder 信息也存储在相同的 `_` 文件中。

### Mac OS X HFS (Alpha)

这不是真正的 Apple/Unix 编码，而是 Mac OS X 系统上实际的 HFS/HFS+ 文件。数据叉存储在一个文件中。资源叉存储为具有相同名称但后缀为 `/rsrc` 的伪文件。Finder 信息仅通过 Mac OS X 库调用可用。

另见 `README.macox`。

仅在 Mac OS X 上使用时才有效。

如果发现一个文件具有零长度的资源叉和空的 finderinfo，则认为它没有 Apple/Unix 编码——因此可以使用其他方法设置 TYPE 和 CREATOR。

`genisoimage` 将尝试从 finder 信息设置 CREATOR、TYPE、日期以及可能的其他标志。此外，如果存在，Macintosh 文件名从 finder 信息中设置，否则 Macintosh 名称基于 Unix 文件名——见下文 HFS MACINTOSH 文件名部分。

使用 `-apple` 时，TYPE 和 CREATOR 存储在 ISO9660 目录记录中的可选系统使用或 SUSP 字段中——方式与 Rock Ridge 属性非常相似。实际上，为了简化操作，Apple 扩展被添加在现有 Rock Ridge 属性的开头（即，为了获取 Apple 扩展，你也会获得 Rock Ridge 扩展）。

Apple 扩展要求资源叉存储为 ISO9660 *关联文件*。这就像存储在 ISO9660 文件系统中的任何正常文件一样，只是在目录记录中设置了关联文件标志（位 2）。该文件与数据叉（非 Apple 机器看到的文件）同名。其他操作系统通常忽略关联文件。

使用 `-hfs` 时，TYPE 和 CREATOR 以及其他 finder 信息存储在一个单独的 HFS 目录中，在 ISO9660 卷上不可见。HFS 目录引用上述描述的数据和资源叉文件。

在大多数情况下，使用 `-hfs` 比使用 `-apple` 更好，因为后者强加了文件名中允许使用的有限 ISO9660 字符。然而，Apple 扩展的优势在于文件在磁盘上打包更高效，可能可以在 CD 上容纳更多文件。

#### HFS MACINTOSH 文件名

在可能的情况下，随 Apple/Unix 文件存储的 HFS 文件名将被用于 CD 的 HFS 部分。然而，并非所有的 Apple/Unix 编码都将 HFS 文件名与 finderinfo 一起存储。在这些情况下，将使用 Unix 文件名——其中特殊字符会被转义。特殊字符包括 `^` 以及代码大于 127 的字符。

AUFS 通过使用 `:` 后跟两个十六进制数字的字符代码来转义这些字符。Netatalk 和 EtherShare 有类似的方案，但使用 `%` 代替 `:`。

如果 `genisoimage` 找不到 HFS 文件名，它会使用单个字符，将任何 `%xx` 或 `:xx` 字符（xx 为两个十六进制数字）转换为单个字符代码。如果 xx 不是十六进制数字（[0-9a-fA-F]），则保持原样——尽管剩余的 `:` 会被转换为 `%`，因为 `:` 是 HFS 目录分隔符。必须小心，因为普通的带有 `%xx` 或 `:xx` 的 Unix 文件也会被转换。例如：

- This:2File 转换为 This%2File
- This:File 转换为 This%File
- This:t7File 转换为 This%t7File

虽然 HFS 文件名似乎支持大写和小写字母，但文件系统是大小写不敏感的，即文件名 aBc 和 AbC 是相同的。如果在目录中找到具有相同 HFS 名称的文件，`genisoimage` 将尝试通过在一个文件名后添加 `_` 字符来创建唯一名称。

如果文件存在 HFS 文件名，`genisoimage` 可以使用此名称作为 ISO9660、Joliet 和 Rock Ridge 文件名的起点，使用 `-mac-name`。没有 HFS 名称的普通 Unix 文件仍使用其 Unix 名称。例如：

如果一个 MacBinary（或 PC Exchange）文件以 *someimage.gif.bin* 的形式存储在 Unix 文件系统中，但包含一个名为 *someimage.gif* 的 HFS 文件，那么该名称将出现在 CD 的 HFS 部分。然而，由于 `genisoimage` 使用 Unix 名称作为其他名称的起点，生成的 ISO9660 名称可能是 *SOMEIMAG.BIN*，而 Joliet/Rock Ridge 将是 *someimage.gif.bin*。此选项将使用 HFS 文件名作为起点，ISO9660 名称可能是 *SOMEIMAG.GIF*，而 Joliet/Rock Ridge 将是 *someimage.gif*。

`-mac-name` 目前无法与 `-T` 一起使用——*TRANS.TBL* 文件中将使用 Unix 名称，而不是 Macintosh 名称。

用于将任何 HFS 文件名转换为 Joliet/Rock Ridge 文件名的字符集默认为 `cp10000`（Mac Roman）。可以使用 `-input-hfs-charset` 指定所使用的字符集。其他内置的 HFS 字符集包括：`cp10006`（MacGreek）、`cp10007`（MacCyrillic）、`cp10029`（MacLatin2）、`cp10079`（MacIcelandic）和 `cp10081`（MacTurkish）。

注意：从各种 Apple/Unix 格式中获取的 HFS 文件名所使用的字符代码不会被转换，因为它们假定已经是正确的 Apple 字符集。

仅从 HFS 文件名导出的 Joliet/Rock Ridge 名称会被转换。现有的 `genisoimage` 代码会过滤掉 ISO9660 和 Joliet 文件名中的非法字符，但由于 `genisoimage` 期望直接处理 Unix 名称，它保持 Rock Ridge 名称不变。但是，由于 `/` 是合法的 HFS 文件名字符，`-mac-name` 将 Rock Ridge 文件名中的 `/` 转换为 `_`。
