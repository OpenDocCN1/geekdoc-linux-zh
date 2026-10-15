
`-f` 或 `--force` 选项强制系统覆盖任何现有文件，而无需提示。

## 使用交互模式

`-i` 或 `--interactive` 选项会导致 `cp` 在覆盖任何现有文件之前询问你。

## 保留所有权和权限

通常，执行 `cp` 命令的用户将拥有复制文件的所有权，并使用该账户的默认权限。`-p` 或 `--preserve` 选项会尽可能保留所有权和权限。

## 执行递归复制

如果你使用 `-R` 或 `--recursive` 选项并指定目录作为源选项，则会复制整个目录及其子目录。虽然 `-r` 也执行递归复制，但它对普通文件和目录以外的文件的行为未定义。大多数 `cp` 实现将 `-r` 视为 `-R` 的同义词，但这种行为并不有保证。

## 执行归档复制

`-a` 或 `--archive` 选项类似于 `-R`，但它还会保留所有权并原样复制链接。`-R` 选项复制符号链接指向的文件，而不是符号链接本身。（链接将在本章稍后的“管理链接”中详细描述。）

## 执行更新复制

`-u` 或 `--update` 选项告诉 `cp` 仅当原始文件比目标文件新或目标文件不存在时才复制文件。

![](img/f74c2c51e1985d4d3a6804ba2887d2f4_369_0.png)

此 `cp` 选项列表是不完整的，但它涵盖了最常用的选项。请咨询 `cp` 的 man 页面获取更多选项信息。

例如，以下命令将 `etcstab` 配置文件复制到 `/root` 中的备份位置，但仅当原始 `etcstab` 比现有的备份新时：

```bash
# cp -u etcstab rootstab-backup
```

## 使用 mv 命令

`mv` 命令（`move` 的缩写）通常用于将文件和目录从一个位置移动到另一个位置并重命名。`Linux` 不区分这两种操作，尽管许多用户会区分。`mv` 的语法与 `cp` 相似：

```bash
mv [options] source destination
```

该命令接受许多与 `cp` 相同的选项值。在之前的列表中，`--preserve`、`--recursive` 和 `--archive` 不适用于 `mv`，但其他的适用。

要移动一个或多个文件或目录，请指定文件作为源选项，并指定目录或（可选，对于移动单个文件）文件名作为目的选项：

```bash
$ ls document.odt
document.odt
$
$ mv document.odt important/purchases/
$
$ ls document.odt
ls: cannot access document.odt: No such file or directory
$
$ ls important/purchases
document.odt
$
```

前面的命令将 `document.odt` 文件移动到 `important/purchases` 子目录中。你可以看到，与 `cp` 命令不同，原始文件被移动到了新的目录位置，而不会在原始目录中留下副本。

![](img/f74c2c51e1985d4d3a6804ba2887d2f4_371_0.png)

如果移动发生在同一个底层文件系统上，`Linux` 通过重写目录条目完成工作；不需要读取和重写文件数据。这使得 `mv` 非常非常快。然而，当目标目录在另一个分区或磁盘上时，`Linux` 必须读取原始文件，将其重写新位置并删除原始文件。这会减慢 `mv`。

使用 `mv` 重命名文件与移动文件非常相似，只是源和目的文件名位于同一目录中。此 `mv` 命令在同一目录下将 `document.odt` 重命名为 `washer-order.odt`：

```bash
$ ls *.odt
document.odt
$ mv document.odt washer-order.odt
$
```

```bash
$ ls *.odt
washer-order.odt
$
```

你可以将移动和重命名操作结合。此命令同时移动并重命名一个文件：

```bash
$ mv document.odt important/purchases/washer-order.odt
$
$ ls important/purchases/washer-order.odt
important/purchases/washer-order.odt
$
```

你也可以使用 `mv` 移动或重命名整个目录；只需在命令中指定一个或多个目录作为源选项。例如，考虑以下命令：

```bash
$ mv important critical
$
$ mv critical tmp
```

第一条命令将当前目录下的 `important` 子目录重命名为 `critical`。第二条命令将重命名后的子目录移动到 `/tmp` 目录。（你可以将这两条命令合并为 `mv important tmpcritical`。）这些命令的形式与与文件使用 `mv` 命令时相同。可选，在重命名整个目录时，你可以在目录名称后添加尾随斜杠（`/`）。

## 使用 rm 命令

要删除文件，请使用 `rm` 命令。该命令名称是 `remove` 的缩写，语法简单：

```bash
rm [options] files
```

`rm` 命令接受许多与 `cp` 或 `mv` 相同的指定选项。在 `cp` 中描述的选项中，`--preserve`、`--archive` 和 `--update` 不适用于 `rm`，但其他所有适用。在 `rm` 中，`-r` 是 `-R` 的同义词。

![](img/f74c2c51e1985d4d3a6804ba2887d2f4_373_0.png)

默认情况下，`Linux` 的命令行 `rm` 命令不提供任何类型的“垃圾桶”功能。一旦你用 `rm` 删除了文件，它就消失了。除非从备份检索文件或执行低级磁盘维护（如 `debugfs`），否则无法恢复。因此，在使用 `rm` 时应小心，特别是当你以 `root` 身份登录时。当你使用 `-R` 选项时尤其如此，它可以破坏你 `Linux` 安装的大部分！

## 使用 touch 命令

`Linux` 原生文件系统为每个文件维护三个时间戳：

- 最后文件修改时间
- 最后 `inode` 变化时间
- 最后访问

许多程序依赖这些时间戳。例如，`make` 工具（帮助从源代码编译程序）使用时间戳来确定如果对象文件，哪些源文件需要重新编译。因此，有时你可能需要修改时间戳。这就是 `touch` 命令的工作，语法如下：

```bash
touch options files
```

默认情况下，`touch` 将修改和访问时间设置为当前时间。你可能会使用它，例如，当你想在已有对象文件的情况下重新编译特定的源代码文件时。如果 `files` 指定的文件不存在，`touch` 会创建空文件。这对于你想创建虚拟文件（例如，为了测试其他文件操作命令）可能非常有用。

你可以向 `touch` 传递各种指定的选项值来改变其行为：

### 仅更改访问时间

`-a` 或 `--time=at` 选项导致 `touch` 仅更改访问时间，而不更改修改时间。

### 仅更改修改时间

`-m` 或 `--time=mt` 选项导致 `touch` 仅更改修改时间，而不更改访问时间。

### 不创建文件

如果你不想让 `touch` 创建不存在的文件，向它传递 `-c` 或 `--no-create` 选项。

### 设置指定时间

`-t timestamp` 选项将时间设置为 `timestamp` 指定的值。该值格式为 `MMDDhhmm[[CC]YY][.ss]`，其中 `MM` 是月份，`DD` 是日期，`hh` 是小时（24小时制），`mm` 是分钟，`[CC]YY` 是年份（例如 `2012` 或 `12`，两者等效），`ss` 是秒。另一种设置特定时间的方法是使用 `-r refille` 或 `--reference=refille` 选项，其中 `refille` 是你想复制其时间戳的文件。

## 文件归档命令

文件归档工具将一组收集到一个单个包文件中，称为归档（`archive`）。相比一组文件，归档更便于移动，适用于跨网络传输或移动到备份介质等应用程序。

`Linux` 支持多种归档命令，最著名的是 `tar` 和 `cpio`。`dd` 命令虽然技术上不属于归档命令，但在某些方面与它们相似，因为它可以将整个分区或磁盘复制到文件中，反之亦然。

![](img/f74c2c51e1985d4d3a6804ba2887d2f4_376_0.png)

在 `Windows` 上很常见的 `zip` 格式由 `Linux` 的 `zip` 和 `unzip` 命令支持。其他归档格式，如 Roshal Archive (RAR) 和 Stuffilt，也可以使用 `Linux` 工具进行操作。

### 使用 tar 工具

`tar` 程序的名称代表“带带归档器”（tape archiver）。尽管如此，你仍然可以使用 `tar` 将数据归档到其他介质。事实上，tar 包（tarballs）经常用于一步到位在计算机之间传输多个文件，例如分发源代码时。tar 包是由 `tar` 创建的归档文件，通常使用 `gzip`、`xz` 或 `bzip2` 进行压缩。
