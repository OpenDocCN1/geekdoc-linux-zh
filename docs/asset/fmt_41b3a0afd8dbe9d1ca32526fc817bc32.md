
![](img/c0a399aca0d18f8822d714ad0a173123_120_0.png)

> 当你通过网络将文件复制到远程主机时，文件传输过程通常需要通过加密方法保护。`rsync` 命令可以通过 OpenSSH 进行隧道传输，以提供数据隐私。此外，`scp` 命令也可以用于提供安全的文件复制机制。这两种方法都在第 12 章“保护文件”中有所介绍。

要快速在本地复制文件，`rsync` 命令的语法与 `mv` 命令的语法类似。它如下所示：

```bash
rsync [OPTION] ... SOURCE DEST
```

某些 `rsync` 选项将帮助你快速复制文件。某些开关适用于复制大文件或在本地创建备份，因此建议回顾表 3.4 中列出的常用 `rsync` 选项。

## 表 3.4 `rsync` 命令的常用本地复制选项

| 短选项 | 长选项 | 描述 |
| :--- | :--- | :--- |
| `-a` | `--archive` | 使用归档模式。 |
| `-D` | N/A | 保留设备文件和特殊文件。 |
| `-g` | `--group` | 保留文件的所属组。 |
| `-h` | `--human-readable` | 以人类可读的格式显示数值输出。 |
| `-l` | `--links` | 将符号链接作为符号链接复制。 |
| `-o` | `--owner` | 保留文件的所有者。 |
| `-p` | `--perms` | 保留文件的权限。 |
| N/A | `--progress` | 显示文件复制过程的进度。 |
| `-r` | `--recursive` | 复制目录的内容，对于原始目录树中的任何子目录，也连续复制其内容（递归）。 |
| N/A | `--stats` | 显示详细的文件传输统计信息。 |
| `-t` | `--times` | 保留文件的修改时间。 |
| `-v` | `--verbose` | 在执行命令时提供详细的命令操作信息。 |

归档模式由 `-a`（或 `--archive`）开关启用，是一个有趣的功能。使用这一个开关等同于使用 `-rlptgoD` 选项组合，这是一套流行的用于创建目录树备份的 `rsync` 命令选项集。

列表 3.12 展示了一个使用 `rsync` 工具复制大文件的示例。请注意，当复制完成时，该工具会输出有用的信息，例如数据传输速率。如果你想要更多的文件传输统计信息，请将 `--stats` 选项添加到你的命令中。

### 列表 3.12：使用 `rsync` 命令移动并重命名文件

```bash
# ls -sh /media/USB/Parrot-full-3.7_amd64.iso
3.6G /media/USB/Parrot-full-3.7_amd64.iso
#
# rsync -v /media/USB/Parrot-full-3.7_amd64.iso /home/Christine/
Parrot-full-3.7_amd64.iso

sent 3,769,141,763 bytes  received 35 bytes  3,137,030.20 bytes/sec
total size is 3,768,221,696  speedup is 1.00

# ls -sh /home/Christine/Parrot-full-3.7_amd64.iso
3.6G /home/Christine/Parrot-full-3.7_amd64.iso
#
```

![](img/c0a399aca0d18f8822d714ad0a173123_121_0.png)

远程同步工具在其输出中通常会显示一个加速比（speedup rating）。该比率与执行同步备份相关。如果你使用 `rsync` 命令定期将某个目录备份到另一个目录位置，加速比可以让你知道有多少个文件因为未被修改且已经备份过而不需要复制。例如，如果 600 个文件中都有 600 个需要复制到备份目录位置，加速比为 1.00。如果只有 600 个文件中的 300 个需要复制，加速比为 2.00。因此，当你使用 `rsync` 命令将单个文件复制到新位置时，加速比始终为 1.00。

## 删除文件

清理整个文件系统或仅仅是你自己的目录空间，通常始于删除不需要的文件和目录。理解执行此操作所需的命令及其开关至关重要，以避免在删除这些项目时出错。

最灵活且使用最广泛的删除工具是 remove 工具。它通过 `rm` 命令调用，其基本语法如下：

```bash
rm [OPTION]... FILE
```

`rm` 工具有很多实用选项，因此务必查看其 man 页面以了解所有选项。然而，最常用选项列在表 3.5 中。

### 表 3.5 `rm` 命令的常用选项

| 短选项 | 长选项 | 描述 |
| --- | --- | --- |
| `-d` | `--dir` | 删除任何空目录。 |
| `-f` | `--force` | 继续执行删除过程，即使命令指定要删除的某些文件不存在，并且在删除任何现有文件前都不询问。 |
| `-i` | `--interactive` | 在删除任何现有文件之前进行询问。 |
| `-I` | N/A | 在删除超过三个文件时，或使用 `-r` 选项时进行询问。 |
| `-R`, `-r` | `--recursive` | 删除目录的内容，并且对于原始目录树内的任何子目录，递归地删除其内容和子目录本身。 |
| `-v` | `--verbose` | 随着命令执行提供详细的命令操作信息。 |

要简单地删除单个文件，可以使用 `rm` 命令，指定要删除的文件名，并且不使用任何开关。然而，使用 `-i`（或 `--interactive`）选项以确保你没有删除错误的文件始终是个好主意，如清单 3.13 所示。

### 清单 3.13：使用 `rm` 命令删除文件

```bash
$ ls Parrot-full-3.7_amd64.iso
Parrot-full-3.7_amd64.iso
$
$ rm -i Parrot-full-3.7_amd64.iso
rm: remove write-protected regular file 'Parrot-full-3.7_amd64.iso'? y
$
$ ls Parrot-full-3.7_amd64.iso
ls: cannot access Parrot-full-3.7_amd64.iso: No such file or directory
$
$ rm -i Parrot-full-3.7_amd64.iso
rm: cannot remove 'Parrot-full-3.7_amd64.iso': No such file or directory
$
$ rm -f Parrot-full-3.7_amd64.iso
$
```

此外，注意清单 3.13 中显示，当文件已被删除后，如果你重新输入 `rm -i` 命令，会生成错误信息，但如果你输入 `rm -f` 命令，对于缺失的文件它不会显示任何信息。`-f`（或 `--force`）开关在你要删除大量文件且希望不显示错误信息时非常有用。

删除目录树或充满文件的目录可能会比较棘手。如果你只是输入 `rm -i` 命令，你会得到错误信息，如清单 3.14 所示。相反，你需要添加 `-R` 或 `-r` 选项，以便目录及其管理的文件被删除。

### 清单 3.14：使用 `rm` 命令删除包含文件的目录

```bash
$ cd SpaceOpera/
$
$ ls -F
Emphasis/ Story-Topics/
$
$ rm -i Emphasis/
rm: cannot remove 'Emphasis/': Is a directory
$
$ rm -ir Emphasis
rm: descend into directory 'Emphasis'? y
rm: remove regular empty file 'Emphasis/melodrama.txt'? y
rm: remove regular empty file 'Emphasis/interplanetary-battles.txt'? y
rm: remove regular empty file 'Emphasis/chivalric-romance.txt'? y
rm: remove directory 'Emphasis'? y
$
$ ls -F
Story-Topics/
$
```

如果你有很多文件需要删除，希望确保你删除的是正确的文件，并且不想对每个要删除的文件都回答 `y`，请改用 `-I` 选项而不是 `-i` 开关。当删除超过三个文件以及当你正在删除一个充满文件的目录并使用其中一个递归开关时，它会询问，如清单 3.15 所示。

### 清单 3.15：使用 `rm` 命令的 `-I` 选项

```bash
$ ls -F
Story-Topics/
$
$ rm -Ir Story-Topics/
rm: remove 1 argument recursively? y
$
$ ls -F
$
```

删除空目录，即不包含任何文件的目录，很简单。通过输入 `rmdir` 命令使用移除空目录工具。你会发现添加 `-v`（或 `--verbose`）开关也很有帮助，如清单 3.16 所示。

### 清单 3.16：使用 `rmdir` 命令

```bash
$ mkdir -v EmptyDir
mkdir: created directory 'EmptyDir'
$
$ rmdir -v EmptyDir/
rmdir: removing directory, 'EmptyDir/'
$
```

如果你想删除一个没有文件但包含空子目录的目录树，你也可以使用 `rmdir` 工具。需要提供完整的目录树名称作为参数，并且必须使用 `-p`（或 `--parents`）开关。一个示例显示在清单 3.17 中。

### 清单 3.17：使用 `rmdir` 命令删除空的目录树

```bash
$ mkdir -vp EmptyDir/EmptySubDir
mkdir: created directory 'EmptyDir'
mkdir: created directory 'EmptyDir/EmptySubDir'
$
$ rmdir -vp EmptyDir/EmptySubDir
rmdir: removing directory, 'EmptyDir/EmptySubDir'
rmdir: removing directory, 'EmptyDir'
$
```

你可能会出现一种情况，即需要从目录树中仅删除空目录。在这种情况下，你需要使用 `rm` 命令并添加 `-d`（或 `--dir`）开关，如清单 3.18 所示。

### 清单 3.18：使用 `rm` 命令删除树中的空目录

```bash
$ mkdir -v EmptyDir
mkdir: created directory 'EmptyDir'
$
$ mkdir -v NotEmptyDir
mkdir: created directory 'NotEmptyDir'
$
$ touch NotEmptyDir/File42.txt
$
$ rm -id EmptyDir NotEmptyDir
rm: remove directory 'EmptyDir'? y
rm: cannot remove 'NotEmptyDir': Directory not empty
$
```

一项重要的技能是理解用于创建和删除目录的命令，以及用于查看、创建、复制、移动、重命名和删除文件的各个命令。此外，牢固掌握常用命令选项也是至关重要的知识。这种专长是你 Linux 命令行工具包中宝贵的工具。

## 链接文件和目录

理解文件和目录链接是你 Linux 旅程的重要组成部分。虽然许多人很快就能学会如何链接文件，但他们不一定理解底层的链接结构。而这可能成为一个问题。在本节中，我们将探索文件链接及其影响。

有两种类型的链接。一种是符号链接，也称为软链接。另一种是硬链接，我们将首先介绍它。

### 建立硬链接

硬链接是一个文件或目录，它有一个索引（inode）号，但有两个或更多不同的文件名。拥有一个 inode 号意味着它是文件系统中的单个数据文件。拥有两个或更多名称意味着可以通过多种方式来访问该文件。图 3.2 显示了这种关系。在这个图中，已创建了一个硬链接。该硬链接有两个文件名，一个 inode 号，因此有一个位于磁盘分区上的文件系统位置。因此，该文件有两个名称，但在物理上是同一个文件。

#### 图 3.2 硬链接文件关系

![](img/c0a399aca0d18f8822d714ad0a173123_125_0.png)

硬链接允许你拥有一个文件的伪副本，而无需真正复制其数据。这通常用于文件备份中，当文件系统空间不足以备份文件的数据时。如果某人删除了该文件的一个名称，你仍然拥有另一个链接到其数据的文件名。

要创建硬链接，使用 `ln` 命令。对于硬链接，在发出 `ln` 命令之前，原始文件必须存在。被链接的文件必须不存在。它在命令发出时被创建。清单 3.19 显示此命令的操作。

### 清单 3.19：使用 `ln` 命令创建硬链接

```bash
$ touch OriginalFile.txt
$
$ ls
OriginalFile.txt
$
$ ln OriginalFile.txt HardLinkFile.txt
$
$ ls
HardLinkFile.txt  OriginalFile.txt
$
$ ls -i
2101459 HardLinkFile.txt  2101459 OriginalFile.txt
$
$ touch NewFile.txt
$
$ ls -og
total 0
-rw-rw-rw-   2 0 Aug 24 18:09 HardLinkFile.txt
-rw-rw-rw-   1 0 Aug 24 18:17 NewFile.txt
-rw-rw-rw-   2 0 Aug 24 18:09 OriginalFile.txt
$
```

在清单 3.19 中，通过 `touch` 命令创建了一个新的空白且空的文件 `OriginalFile.txt`。然后通过 `ln` 命令将其硬链接到 `HardLinkFile.txt`。注意，`OriginalFile.txt` 是在发出 `ln` 命令之前创建的，而 `HardLinkFile.txt` 是通过发出 `ln` 命令创建的。使用 `ls -i` 命令检查这些文件的 inode 号，你可以看到两个文件的号码是相同的。

同样在清单 3.19 中，在创建硬链接并检查 inode 号之后，创建了一个新的空文件，称为 `NewFile.txt`。这样做是为了比较链接计数。使用 `ls -og` 命令，显示文件的元数据，包括文件类型、权限、链接计数、文件大小、创建日期和文件名。此命令类似于 `ls -l`，但省略了文件所有者和组。你可以快速在命令输出中找到链接计数。它们紧挨着文件大小，由于文件是空的，所以所有大小都是 0。注意 `OriginalFile.txt` 和 `HardLinkFile.txt` 的链接计数都为 2。这是因为它们都硬链接到另一个文件。`NewFile.txt` 的链接计数为 1，因为它*未*硬链接到另一个文件。

![](img/c0a399aca0d18f8822d714ad0a173123_126_0.png)

如果你想删除一个链接文件但保留原始文件，使用 `unlink` 命令。只需在命令行输入 `unlink` 并将链接文件名作为参数包含进去。

在创建和使用硬链接时，请记住以下几点重要事项：

- 在发出 `ln` 命令之前，原始文件必须存在。
- 在 `ln` 命令中列出的第二个文件在发出命令之前必须*不*存在。
- 原始文件及其硬链接共享相同的 inode 号。
- 原始文件及其硬链接共享相同的数据。
- 原始文件及其任何硬链接可以存在于不同的目录中。
- 原始文件及其硬链接必须存在于同一个文件系统上。

### 构建软链接

通常，软链接文件提供指向某个文件的指针，该文件可能位于另一个文件系统上。这两个文件不共享 inode 号，因为它们并不指向相同的数据。图 3.3 展示了软链接的关系。

#### 图 3.3 软链接文件关系

![](img/c0a399aca0d18f8822d714ad0a173123_127_0.png)

要创建符号链接，需要使用带有 `-s`（或 `--symbolic`）选项的 `ln` 命令。示例如下，见列表 3.20。

### 列表 3.20：使用 `ln` 命令创建软链接

```bash
$ touch OriginalSFile.txt
$
$ ls
OriginalSFile.txt
$
$ ln -s OriginalSFile.txt SoftLinkFile.txt
$
$ ls -i
2101456 OriginalSFile.txt 2101468 SoftLinkFile.txt
$
$ ls -og
total 0
-rw-rw-r--, 1 0 Aug 24 19:04 OriginalSFile.txt
lrwxrwxrwx. 1 17 Aug 24 19:04 SoftLinkFile.txt -> OriginalSFile.txt
$
```

与硬链接类似，在发出 `ln -s` 命令之前，原始文件必须存在。软链接文件本身必须不存在。它是在命令发出时创建的。在列表 3.20 中，您可以通过 `ls -i` 命令看到，软链接文件不像硬链接文件那样共享相同的 inode 号。此外，软链接文件不会经历链接计数的增加。`ls -og` 命令显示了这一点，它还显示了软链接文件指向原始文件的指针。

> **提示**
>
> 有时候，您会有一个软链接文件指向另一个软链接文件。
>
> 如果您想快速找到最终文件，请使用 `readlink -f` 命令，并将其中一个软链接文件名作为参数传递给它。`readlink` 实用工具将显示最终文件的名称和目录位置。

在创建和使用软链接时，请记住以下几点：

- 在发出 `ln -s` 命令之前，原始文件必须存在。
- 在 `ln -s` 命令中列出的第二个文件在发出命令之前必须不存在。
- 原始文件及其软链接不共享相同的 inode 号。
