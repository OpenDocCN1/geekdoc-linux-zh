
## 选择题

-   C. 无；`-t` 选项无效，因此会导致 `mkfs` 中止其操作。
-   D. 它将 ext2 文件系统转换为 ext4 文件系统。
-   E. 它在 `devda4` 上创建一个新的 ext2 文件系统，覆盖任何现有文件系统及其数据。

**12. 以下哪项最能概括 Windows 的 `FDISK` 和 Linux 的 `fdisk` 之间的差异？**

-   A. Linux 的 `fdisk` 是 Windows `FDISK` 的一个简单克隆，但被编写为在 Linux 而非 Windows 上运行。
-   B. 这两个程序是完全独立的，实现类似的目标，尽管 Linux 的 `fdisk` 更加灵活。
-   C. Windows 的 `FDISK` 使用 GUI 控件，而 Linux 的 `fdisk` 使用命令行界面，但它们的功能相似。
-   D. 尽管名称相似，但它们是完全不同的工具——Windows 的 `FDISK` 命令处理磁盘分区，而 Linux 的 `fdisk` 格式化软盘。
-   E. Windows 的 `FDISK` 命令管理 GPT 磁盘，而 Linux 的 `fdisk` 管理 MBR 磁盘。

**13. 应该将哪个挂载点与交换分区关联？**

-   A. `/`
-   B. `/swap`
-   C. `/boot`
-   D. `/mem`
-   E. 以上都不是

**14. `fsck` 用于强制使用特定文件系统类型的选项是哪个？**

-   A. `-A`
-   B. `-N`
-   C. `-t`
-   D. `-C`
-   E. `-f`

**15. `df` 可以报告以下哪些信息？**

-   A. 文件系统已挂载多长时间
-   B. ext3fs 分区上使用的 inode 数量
-   C. 分区的文件系统类型
-   D. 分区上已使用的可用磁盘空间百分比
-   E. 与文件系统关联的挂载点

**16. 日志文件系统相对于常规（非日志）文件系统的一个优势是什么？**

-   A. 日志系统比非日志文件系统更古老且测试更完善。
-   B. 日志文件系统永远不需要用 `fsck` 进行检查。
-   C. 日志文件系统支持 Linux 所有权和权限；非日志文件系统不支持。
-   D. 在电源故障或系统崩溃后，日志文件系统需要更短的磁盘检查时间。
-   E. 日志文件系统记录所有事务，使其可以撤销。

**17. 为了访问 USB 闪存驱动器上的文件，你输入 `mount devsd1 mediaflash` 作为 root。该命令会挂载哪种类型的文件系统？**

-   A. Ext2fs
-   B. FAT
-   C. HFS
-   D. ReiserFS
-   E. 以上所有

**18. 以下哪个 `etcstab` 条目会在启动时挂载 `devsdb2` 作为 `/home` 目录？**

-   A. `devsdb2 reiserfs /home defaults 0 0`
-   B. `devsdb2 /home reiserfs defaults 0 0`
-   C. `/home reiserfs devsdb2 auto 0 0`
-   D. `/home devsdb2 reiserfs auto 0 0`
-   E. `reisersfs devsdb2 /home noauto 0 0`

**19. 为了使得普通用户（UID 为 1000）可以挂载可移动磁盘（如 USB 闪存驱动器），你可能在 `etcfstab` 中指定哪些文件系统选项？（选择三项。）**

-   A. `user`
-   B. `users`
-   C. `owner`
-   D. `owner`
-   E. `uid=1000`

![](img/f74c2c51e1985d4d3a6804ba2887d2f4_360_0.png)

如果你访问由 DOS 使用的可移动磁盘或分区上的文件分配表（FAT）文件系统，可以使用以下两种文件系统类型代码之一进行操作：`msdos`，它将文件名限制为 8.3 格式；或者 `vfat`，它支持 Windows 风格的长文件名。此外，`umsdos` 文件系统类型代码是 Linux 专有的扩展，支持 Linux 风格的长文件名。UMSDOS 支持在 2.6.11 内核之后停止了。

有两个文件名特别特殊。由单个点（`.`）组成的文件名表示当前目录，而由双点（`..`）组成的文件名表示父目录。例如，如果你的当前目录是 `homemerry`，那么 `.` 指向 `homejames`，而 `..` 指向 `/home`。

注意 Linux 文件名是大小敏感的。例如，`Filename.txt` 或 `FILENAME.TXT` 这三个文件都可以存在同一个 Linux 目录下，它们被视为完全不同的文件。在 Windows 下，这三个文件名都指向同一个文件。这种差异对于大多数从 Windows 迁移到 Linux 的人并不是主要问题，但你应该意识到这一点。

## 探索通配符扩展规则

你可以在许多命令中使用通配符。通配符代表其他字符的符号或符号集。Linux 中常见的通配符有三类：

- 问号（`?`）代表单个字符。例如，`b??k` 匹配 `book`、`balk`、`buck` 或任何以 a 开以 k 结尾的四个字符的文件名。
- 星号（`*`）匹配任何字符或字符集，包括任何字符。例如，`b*k` 匹配 `book`、`balk` 和 `buck`，以及 `bk`、`bbk` 和 `buck`。任何字符和数量的字符都可以作为文件名，因为它以 b 开头并以 k 结尾。

### 括号值

位于方括号（`[]`）中的字符通常匹配集合中的任何字符。例如，`b[ae]ok` 匹配 `book` 和 `boek`。每个括号组用于单字符匹配。如上面的示例所示，名称中的第二个字符可以是 a 或 e。你可以在同一个名称中使用多个括号。例如，`b[ae]o[ks]` 搜索第二个和第四个位置的字符集。匹配此通配符设置的名称包括 `book`、`boek`、`baos` 和 `beos`。

还可以使用括号指定值范围。例如，`b[a-z]ck` 匹配 `back`、`buck` 以及其他这种格式的第二个字符为小写字母的四字母文件名。这与 `b7ck` 不同——因为 Linux 以大小敏感的方式处理文件名，而且 `?` 匹配任何字符（而不只是任何小写字母）。

通配符在 shell 中实现并传递给你调用的命令。例如，如果你输入 `ls b??k` 且该通配符匹配了三个文件 `balk`、`book` 和 `buck`，那么结果就与你输入 `ls balk book buck` 的完全一样。这种通配符扩展过程被称为文件通配（file globbing）、文件名扩展（filename expansion）或简单的通配（globbing）。

## 理解文件命令

文件操作命令对于日常文件操作至关重要。这些命令允许你列出、复制、移动、重命名和删除文件。

## 使用 ls 命令

为了操作文件，了解它们的信息是有帮助的。这是 `ls` 命令的工作，它的名称是 list（列表）的缩写。`ls` 命令显示目录中的文件名。它的语法简单：

```
ls [options] [files]
```

选项列表和文件列表都是可选的。如果你省略了文件列表，`ls` 会显示当前目录的内容：

```
$ pwd
homeChristine/my-work
$ ls
project_a354 project_c923 project_m1321 punch_list.txt
$
```

要显示不在当前目录中的内容，必须包含目录名：

```
$ ls -F homeChristine/
afile.txt file.dat my-work/ newfile.dat
bfile.txt hlink_afile NewDir/ script.*
bigprogram.sh* important/ newfile.dat slink_bfile@n$
```

这输出了 `homeChristine` 目录的内容，通过 `-F` 选项包含了各种文件类型。接下来的列表项“显示文件类型”描述了这些符号（如 图`）的含义。

你可以在 `ls` 命令中提供一个或多个文件或目录名。此外，你可以使用文件通配：

```
$ *.txt homeChristine/my-work/
afile.txt bfile.txt
homeChristine/my-work:
```

```
project_a354 project_c923 project_m1321 punch_list.txt
$
```

在这种情况下，`ls` 命令显示了所有指定的文件和目录的信息。此输出显示了当前工作目录中的 `*.txt` 文件以及 `homeChristine/my-work/` 目录的内容。

默认情况下，`ls` 创建按文件名排序的列表，如示例所示。在过去，大写字母出现在小写字母之前。然而，最近版本的 `ls` 排序命令是不大小敏感的。

最常见的 `ls` 选项之一是 `-l`，它创建一个长列表。此输出包含了权限字符串、所有者、文件大小、文件创建日期等，以及以下内容：

```
$ ls -l
-rw-r--r-- 1 user group 1024 Jan 1 02:00 file.txt
-rw-r--r-- 1 user group 1024 Jan 1 02:01 file.dat
drwxr-xr-x 1 user group 4096 Jan 1 02:02 directory/
lrwxrwxrwx 1 user group 0 Jan 1 02:03 link -> file.txt
```

（注：由于提供的原始文本包含大量重复和 OCR 错误，上述译文已根据核心逻辑内容进行清理整理。）

![](img/f74c2c51e1985d4d3a6804ba2887d2f4_367_0.png)

此示例在目标目录上使用了尾随斜杠（`/`）。这种做法有助于避免由拼写错误引起的问题。例如，如果目标目录被误写为 `TempDi`（缺少最后的 r），`cp` 将将 `file.dat` 复制为名为 `TempDi` 的文件，而不是 `TempDir` 目录。添加尾随斜杠明确表示你意图将文件复制到子目录中。如果目录不存在，`cp` 会报错，这样你就不会留下命名其妙的神秘文件。

此外，源和目的选项可以是包含文件的整个目录：

```
$ ls -F
file.dat new_file.dat TempDir/
$ ls TempDir/
file2.dat file.dat
$ cp -R TempDir NewDir
$ ls NewDir/
file2.dat file.dat
```

注意在 `cp` 命令上使用了选项 `-R`，用于复制目录及其内容。`cp` 命令支持大量的选项。以下是几个允许你修改命令操作的有用选项：

### 强制覆盖

`-f` 或 `--force` 选项强制系统覆盖任何现有文件，而无需提示。

### 使用交互模式

`-i` 或 `--interactive` 选项会导致 `cp` 在覆盖任何现有文件之前询问你。

### 保留所有权和权限

通常，执行 `cp` 命令的用户将拥有复制文件的所有权，并使用该账户的默认权限。`-p` 或 `--preserve` 选项会尽可能保留所有权和权限。

### 执行递归复制

如果你使用 `-R` 或 `--recursive` 选项并指定目录作为源选项，则会复制整个目录及其子目录。虽然 `-r` 也执行递归复制，但它对普通文件和目录以外的文件的行为未定义。大多数 `cp` 实现将 `-r` 视为 `-R` 的同义词，但这种行为并不有保证。

### 执行归档复制

`-a` 或 `--archive` 选项类似于 `-R`，但它还会保留所有权并原样复制链接。`-R` 选项复制符号链接指向的文件，而不是符号链接本身。（链接将在本章稍后的“管理链接”中详细描述。）

### 执行更新复制

`-u` 或 `--update` 选项告诉 `cp` 仅当原始文件比目标文件新或目标文件不存在时才复制文件。

![](img/f74c2c51e1985d4d3a6804ba2887d2f4_369_0.png)

此 `cp` 选项列表是不完整的，但它涵盖了最常用的选项。请咨询 `cp` 的 man 页面获取更多选项信息。

例如，以下命令将 `etcstab` 配置文件复制到 `/root` 中的备份位置，但仅当原始 `etcstab` 比现有的备份新时：

```
# cp -u etcstab rootstab-backup
```

## 使用 mv 命令

`mv` 命令（move 的缩写）通常用于将文件和目录从一个位置移动到另一个位置并重命名。Linux 不区分这两种操作，尽管许多用户会区分。`mv` 的语法与 `cp` 相似：

```
mv [options] source destination
```

该命令接受许多与 `cp` 相同的选项值。在之前的列表中，`--preserve`、`--recursive` 和 `--archive` 不适用于 `mv`，但其他的适用。

要移动一个或多个文件或目录，请指定文件作为源选项，并指定目录或（可选，对于移动单个文件）文件名作为目的选项：

```
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

如果移动发生在同一个底层文件系统上，Linux 通过重写目录条目完成工作；不需要读取和重写文件数据。这使得 `mv` 非常非常快。然而，当目标目录在另一个分区或磁盘上时，Linux 必须读取原始文件，将其重写新位置并删除原始文件。这会减慢 `mv`。

使用 `mv` 重命名文件与移动文件非常相似，只是源和目的文件名位于同一目录中。此 `mv` 命令在同一目录下将 `document.odt` 重命名为 `washer-order.odt`：

```
$ ls *.odt
document.odt
$ mv document.odt washer-order.odt
$
```

```
$ ls *.odt
washer-order.odt
$
```

你可以将移动和重命名操作结合。此命令同时移动并重命名一个文件：

```
$ mv document.odt important/purchases/washer-order.odt
$
$ ls important/purchases/washer-order.odt
important/purchases/washer-order.odt
$
```

你也可以使用 `mv` 移动或重命名整个目录；只需在命令中指定一个或多个目录作为源选项。例如，考虑以下命令：
