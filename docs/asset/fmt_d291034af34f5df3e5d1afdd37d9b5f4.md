
| `gunzip file.gz` | 解压缩 `file.gz` 创建 `file`。原文件 `file.gz` 被删除。 |

| `gunzip -c file.gz` | 将文件解压缩到标准输出。 |

| `cat file \| gzip` | 在管道中压缩数据 |

## bzip2

`bzip2 [options] [files]`

`bzip2 [options] [files]` 标准输入/输出 `--opt` `--help` `--version`

* `bzip2 [options] [files]`

* `bzcat [options] [files]`

`bzip2` 和 `bunzip2` 以 Burrows-Wheeler 格式压缩和解压缩文件。压缩文件的扩展名为 `.bz2`。

## 示例命令

* `bzip2 file`: 压缩文件创建 `file.bz2`。原文件被删除。

* `bunzip2 file.bz2`: 解压缩 `file.bz2` 创建 `file`。原文件 `file.bz2` 被删除。

* `bunzip2 -c file.bz2`: 将文件解压缩到标准输出。

* `cat file \| bunzip2 \| ...`: 在管道中压缩数据。

* `cat file.bz2 \| bunzip`: 从管道中解压缩数据。

* `bzcat file.bz2`: 将文件解压缩到标准输出。

* `tar -czjf tarfile dir`: 将目录 `dir` 打包成 BZipped TAR 文件。添加 `-v` 可在处理时打印文件名。

## compress

`compress [options] [files]`

`uncompress [options] [files]`

`zcat [options] [files]`

标准输入/输出 `-file` `--help` `--version`

`compress` 和 `uncompress` 以经典的 Unix 压缩格式（Lempel-Ziv）压缩和解压缩文件。压缩文件的扩展名为 `.Z`。

## 示例命令

* `compress file`: 压缩文件创建 `file.Z`。

* `uncompress file.Z`: 解压缩 `file.Z` 创建 `file`。

* `uncompress -c file.Z`: 将文件解压缩到标准输出。

* `zcat file.Z`: 将文件解压缩到标准输出。

* `cat file \| compress \| ...`: 在管道中压缩数据。

* `cat file.Z \| uncompress`: 从管道中解压缩数据。

* `tar -ZF tarfile dir`: 将目录 `dir` 打包成压缩 TAR 文件。使用 `-ZF` 在处理时打印文件名。

## zip

`zip archive.zip [options] [files]`

`unzip [options] archive.zip [files]`

标准输入/输出 `-file` `--help` `--version`

`zip` 以 Windows Zip 格式压缩文件，`unzip` 提取它们。压缩文件的扩展名为 `.zip`。

* `zip archive.zip file1 file2...`: 打包。

```
zip -r archive.zip dir
unzip -l archive.zip
unzip archive.zip
```

* 递归打包目录。
* 列出内容。
* 解包。

## 7z

```
7z stdin输入输出 -file --help --version
```

`7z` 命令也称为 `7-Zip`，用于打包压缩文件和目录。默认情况下，它生成扩展名为 `.7z` 的 `LZMA` 格式归档文件。它支持压缩方法，例如 `ZIP`、`gzip` 和 `bzip2`（原文本此处似有误，保留原意：`ZIP2`可能为笔误，但根据规则不修改语义，仅格式化；若原文为“ZIP, gzip and ZIP2”则保留，但通常应为 bzip2，此处严格遵循“不修改语义”原则，仅对标识符加反引号）。
*注：原文“支持支持压缩方法”重复词，保留原文内容不删除，仅格式化。*
它支持压缩方法，例如 `ZIP`、`gzip` 和 `bzip2`（原文写的是 `ZIP2`，按原文处理：`ZIP`、`gzip` 和 `ZIP2`），但你也可以使用原始 Linux 命令（分别为 `zip`、`gzip` 和 `bzip2`），这些在 Linux 机器上更为常见。`7z` 还可以从多种归档文件中提取内容，甚至是 `Microsoft CAB` 文件。查看帮助页获取完整列表。

```
7z a archive.7z file1 file2...
```

* 打包。

```
7z l archive.7z
```

* 列出内容。

```
7z x archive.7z
```

* 解包。

你好，这是一个非常的文件。

那只敏捷的棕色狐狸跳过了那只懒惰狗。

回见。

假设你删除了第一行，将第二行的“brown”改为“blue”，并在末尾添加一行，创建一个文件 `fileB`：

那只敏捷的蓝色狐狸跳过了

那只懒惰狗。

回见。

Linux 万岁！

`diff` 命令报告了两个标记为 `1,2c1` 和 `4a4` 的差异：

```
→ diff fileA fileB fileA lines 1-2 became fileB line 1
1,2c1 < Hello, this is a wonderful file. Lines 1-2 of fileA
< The quick brown fox jumped over diff separator
-- > The quick blue fox jumped over Line 1 of fileB
4a4 Line 4 was added in fileB
< Linux rules! The added line
```

开头的符号 `<` 和 `>` 分别表示 `fileA` 和 `fileB`。这种输出格式是默认的：还有许多其他格式可用，其中某些可以直接提供给其他工具。尝试一下看看它们是什么样子的。

| 选项 | 输出格式 |
| :--- | :--- |
| `-c` | 上下文差异格式，如 `patch` 命令所用（`man patch`）。 |
| `-D macro` | C 预处理器格式，使用 `#ifdef macro ... #else... #endif`。 |
| `-u` | 统一格式，合并文件并在删除处前加 `"-"`，在添加处前加 `"+"`。供 `git` 使用。 |
| `-y` | 并排格式；使用 `-w` 调整输出宽度。 |
| `-q` | 不报告更改，仅说明文件是否存在差异。 |

`diff` 也可以比较目录。默认情况下，它会比较这些目录中任何相同的文件，并列出出现在其中一个目录而不在另一个目录中的文件：

* `diff dir1 dir2`

要递归比较整个目录树，运行 `diff -r`，它会生成一个关于所有差异的（可能是海量的）报告。

* `diff -r dir1 dir2`

## 有用的选项

* `-b` 忽略空格。
* `-B` 忽略空行。
* `-i` 忽略大小写。
* `-r` 比较目录时，递归进入子目录。

`diff` 是操作文件差异的命令族的一员。其他命令还包括 `diff`（它一次比较三个文件）以及 `sdiff`（它根据你的指令合并两个文件之间的差异创建第三个文件）。

## comm

`comm [options] file1 file2`

标准输入 `-file` `-opt` `--help` `--version`

`comm` 命令比较两个排序后的文件并产生三列制表符分隔的输出：

1. 出现在 `file1` 中但不在 `file2` 中的所有行。
2. 出现在 `file2` 中但不在 `file1` 中的所有行。
3. 同时出现在两个文件中所有行。

例如，如果 `commfile1` 和 `commfile2` 包含以下行：

`commfile1`: `apple`, `baker`, `charlie`

`commfile2`: `baker`, `charlie`, `dark`

那么 `comm` 会产生此三列输出：

* `comm commfile1 commfile2`

```
  apple
  baker
  charlie
  dark
```

## 有用的选项

* `-1` 抑制第一列。
* `-2` 抑制第二列。
* `-3` 抑制第三列。
* `-23` 显示只出现在第一个文件中的行。
* `-13` 显示只出现在第二个文件中的行。
* `-12` 仅显示共同行。

## cmp

`cmp [options] file1 file2 [offset1] [offset2]`

标准输入/输出 `-file` `opt` `--help` `--version`

`cmp` 命令比较两个文件。如果它们的内容相同，`cmp` 不报告任何内容；否则，它列出第一个差异的位置：

* `cmp myfile yearfile`

```
myfile yearfile differ: byte 225, line 4
```

默认情况下，`cmp` 不会告诉你差异是什么，只告诉你在哪里。它也非常适合比较二进制文件，而 `diff` 在文本文件上的操作效果最好。

通常情况下 `cmp` 从每个文件的开头开始比较，如果你提供了偏移量（offsets），它从其他地方开始：

* `cmp myfile yourfile 10 20`

此比较将从 `myfile` 的第 10 个字符和 `yourfile` 的第 20 个字符开始。

## 有用的选项

* `-l` 详细输出：逐字节打印所有差异：

* `cmp -l myfile yourfile`

```
225 167 127
```
