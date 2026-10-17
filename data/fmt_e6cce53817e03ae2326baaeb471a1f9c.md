
压缩文件的命令是`gzip <filename>`，代表 GNU zip。在你的主目录下对一个文件运行`gzip`，然后运行`ls`查看发生了什么。现在，使用`more`查看压缩文件。要解压缩文件，使用`gzip -d <filename>`。现在再次使用`more`查看文件。系统上的许多文件以压缩格式存储。例如，帮助页（man pages）通常是压缩的，并在你阅读它们时自动解压缩。

你之前使用过`cat`命令查看文件。你可以使用`zcat`命令对压缩文件执行相同的操作。压缩一个文件然后输入`zcat <filename>`。你会看到文件内容被写入屏幕。通常，当命令和文件名中包含`z`时，它们与压缩有关——`z`代表 zip。你可以使用`zcat <filename> | less`来正确查看压缩文件。你也可以使用命令`zless <filename>`，它的作用与`zcat <filename> | less`相同。

工具箱的新成员是`bzip2`。这是一个类似于`gzip`的压缩程序，不同之处它更慢，但压缩率高 20%-30%。它适用于压缩从互联网下载的文件（以减少传输量）。用`bzip2`压缩的文件扩展名为`.bz2`。注意，压缩效果的提升很大程度上取决于被压缩的数据类型。有时为了巨大的速度代价换取微小的尺寸缩小，而偶尔这非常值得。频繁压缩和解压缩的文件永远不要使用`bzip2`。

## 4.14 搜索文件

你可以使用该命令搜索文件。切换到根目录并输入`find`。它将通过递归进入每个子目录及其子目录，列出它能看到的所有文件，并在所有子目录下重复执行`find`命令。换句话说，从根目录执行`find`，会打印出系统上所有的文件。如果你像刚才那样输入`find`，它会运行很长时间——按 Ctrl+C 停止它。

现在回到你的主目录并再次运行`find`。你会看到你所有的个人文件。你可以指定一些`find`选项来查找特定的文件。

- `find -type d`只显示目录而不显示其包含的文件。
- `find -type f`只显示文件而不显示包含它们的文件的目录，尽管它仍然会进入所有目录。
- `find -name <filename>`仅查找名为`<filename>`的文件。例如，`find -name '*.c'`将找到所有以`.c`结尾的文件（不带引号字符的`find -name *.c`也可以，你稍后会明白为什么）。`find -name Mary.Jones.letter`将找到名为 Mary.Jones.letter 的文件。

## 4.15 在文件内部搜索

- `find -size [[+-]]<size>`仅查找大小大于（`+`）或小于（`-`）`<size>`千字节的文件，如果未指定符号，则查找大小恰等于`<size>`千字节的文件。
- `find <directory> [<directory ...>]`在指定的每个目录中启动`find`。

对于几乎任何类型的文件搜索，都有许多更多选项。更多细节请参阅`find(1)`（即运行`man 1 find`）。还要查看`-exec`选项，它会导致`find`为其找到的每个文件执行一个命令，例如：

```
find /usr -type f -exec ls -al '{}' ';'
```

`find`的缺点是主动读取目录来寻找文件。这个过程很慢，特别是当你从根目录开始时。替代命令是`locate <filename>`。它通过搜索之前创建的所有系统文件数据库来查找，因此可以瞬间找到文件。其对应的`updatedb`用于更新`locate`使用的文件数据库。在某些系统上，`updatedb`每天在 04h00 自动运行。

尝试这些操作（`updatedb`将需要几分钟）：

```
updatedb
locate rpm
locate deb
locate passwd
locate HOWTO
locate README
```

你通常会想在许多文件中搜索特定的单词或短语，例如，当许多文件中包含电话号码、姓名和地址时。`grep`命令对文件进行行搜索，并打印包含你指定单词的行。`grep`命令摘要如下：

```
grep [options] <pattern> <filename> [...]
```

- 单词、字符串或模式在文中是同义的，基本上意味着你尝试查找的字母和数字。模式也可以是带有通配符的字符串，我们稍后会看到。

运行`grep`单词 "the" 显示包含它的行：`grep 'the' Mary.Jones.letter`。现在尝试`grep 'the' *.letter`。

`grep -n <pattern> <filename>`显示文件中单词所在的行号。

`grep -C <num> <pattern> <filename>`输出单词所在行前后`<num>`行。

`grep -A <num> <pattern> <filename>`输出单词所在行之后的`<num>`行。

`grep -B <num> <pattern> <filename>`输出单词所在行之前的`<num>`行。

`grep -v <pattern> <filename>`只打印不包含你搜索单词的行。

`grep -i <pattern> <filename>`功能与普通`grep`相同，但不区分大小写。

## 4.16 复制到 MS-DOS 和 Windows 格式的软盘

一个名为`mtools`的包允许读写 MSDOS/Windows 格式的软盘。这些不是标准的 UNIX 命令，但包含在大多数 LINUX 发行版中。这些命令支持 Windows “长文件名”软盘。将软盘插入你的 A: 驱动器。

```bash
mdir A:
touch myfile
mcopy file A:
mdir A:
```

注意，在 LINUX 下没有所谓的 A: 磁盘。只有`mtools`包理解 A:，以保留 MS-DOS 用户的习惯。完整的命令列表如下：

| `floppyd` | `mcopy` | `mformat` | `mmount` | `mshowfat` |
| `mattrib` | `mdel` | `minfo` | `mm` | `mtooltest` |

## 基础命令

## 4.17 归档与备份

| `mbadblocks` | `mdeltree` | `mkmanifest` | `mpartition` | `mtype` |
| `mcat` | `mdir` | `mlabel` | `mrd` | `mzip` |
| `mcd` | `mdu` | `mmd` | `mren` | `xcopy` |

输入`info mtools`命令可以获得详细的帮助。通常情况下，将任何 MS-DOS 命令转换为小写并在其前面加上`m`前缀，即可得到相应的 LINUX 命令。

## 4.17 归档与备份

> 在开始任何工作之前，请务必确保你有一个安全的备份方法。

系统管理员的主要活动之一就是制作备份。千万不要低估计算机中信息可能会蒸发或变得混乱的可能性，这是至关重要的。因此，必须不断进行数据备份。备份是你的文件的副本，可以作为计算机部分或全部被销毁时的替代品。其核心思想是将目录中的所有数据（如通常情况下，即一个目录及其所有子目录以及这些子目录中的所有文件等）都存储在一个单独的分区中（通常经过压缩），以便在紧急情况下进行检索。当我们需要以这种方式存储许多文件时，能够将许多文件打包成一个文件是非常有用的，这样我们就可以对单个文件执行操作。当许多文件被打包在一起时，这个打包后的文件被称为归档。通常归档的扩展名为`.tar`，代表 tape archive（磁带归档）。

要创建一个目录的归档，请使用`tar`命令：

```bash
tar -c -f <filename> <directory>
```

创建一个包含几个文件的目录，并运行`tar`命令对其进行备份。将创建一个`<filename>`文件。请仔细注意`tar`报告的任何错误信息。列出文件并检查其大小是否与你要归档的目录大小匹配。你也可以使用`tar`命令的 verify 选项（见 man 页）来检查`<filename>`的完整性。现在删除目录，然后使用`tar`命令的 extract（提取）选项恢复它：

```bash
tar -x -f <filename>
```

你应该看到目录被重建，且所有文件都完好无损。很好的选项是在处理过程中显示归存档中添加或提取的所有文件，这对于监控归档进度非常有帮助。

## 4.18 命令搜索的路径 4. 基础命令

显而易见，你可以归档任何你想要的东西；通常的做法将其命名为`<directory>.tar`，这让所有人清楚它到底是什么。另一个重要的选项是`-p`，它可以保留文件的详细属性信息。

一旦你有了一个`.tar`文件，你可能想用`gzip`将其压缩。这将创建一个`<directory>.tar.gz`，为了简便，有时称为`<directory>.tgz`。
