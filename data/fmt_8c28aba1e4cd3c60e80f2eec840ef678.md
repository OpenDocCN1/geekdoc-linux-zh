
压缩算法（用于执行压缩的数学技术）分为两类：无损和有损。无损压缩保留原始文件中包含的所有数据。这意味着当从压缩版本恢复文件时，其余部分与原始未压缩版本完全相同。另一方面，有损压缩在执行压缩时会删除数据，以便应用更大程度的压缩。当恢复有损文件时，它与原始文件不匹配；而是一个近似值。无损压缩的例子有 `JPEG`（用于图像）和 `MP3`（用于音乐）。在我们的讨论中，我们将专门讨论无损压缩，因为计算机上的大多数数据无法忍任何数据丢失。

### gzip

`gzip` 程序用于压缩一个或多个文件。执行时，它会将原始文件替换为文件的压缩版本。相应的 `gzip` 程序用于将压缩文件恢复为原始的未压缩格式。以下是一个示例：

```
[linuxbox]$ ls -l /etc > foo.txt
[linuxbox]$ ls -l foo*
-rw-r---- 1 me 15738 2008-10-14 07:15 foo.txt
[linuxbox]$ gzip foo.txt
[linuxbox]$ ls -l foo*
-rw-r---- 1 me 15738 2008-10-14 07:15 foo.txt.gz
[linuxbox]$ gunzip foo.txt
[linuxbox]$ ls -l foo*
-rw-r---- 1 me 15738 2008-10-14 07:15 foo.txt
```

在例例中，我们从目录列表创建一个名为 `foo.txt` 的文件。我们运行 `gzip`，它将原始文件替换为压缩后的版本 `foo.txt.gz`。在 `foo.*` 的目录列表中，我们看到原始文件已被压缩版本替换，且压缩版本的大小大约是原始文件的五分之一。我们还可以看到压缩文件与原始具有相同的权限和时间戳。

接下来，我们运行 `gunzip` 程序来压缩文件。之后，我们可以看到文件的压缩版本已被替换为原始文件，并且同样保留了权限和时间戳。

`gzip` 有许多选项。这里是几个：

表 18-1: `gzip` 选项

| 选项 | 描述 |
| --- | --- |
| `-c` | 将输出写入标准输出并保留原始文件。也可以用 `--stdout` 和 `--to-stdout` 指定 |
| `-d` | 解压缩。这使得 `gzip` 表现得像 `gunzip` 一样。也可以用 `--decompress` 或 `--uncompress` 指定 |
| `-f` | 如果已存在原始文件的压缩版本，则强制压缩。也可以用 `--force` 指定 |
| `-h` | 显示用法信息。也可以用 `--help` 指定 |
| `-l` | 列出每个压缩文件的压缩统计信息。也可以用 `--list` 指定 |
| `-r` | 如果命令行上的一个或多个参数是目录，则递归压缩其中的文件。也可以用 `--recursive` 指定 |
| `-t` | 测试压缩文件的完整性。也可以用 `--test` 指定 |
| `-v` | 压缩时显示详细信息。也可以用 `--verbose` 指定 |
| `-number` | 设置压缩量；数字为 1（最快）到 9（最慢）之间的整数。默认值为 6。 |

我们经常看到以 `.tar` 或 `.tgz` 结尾的文件，它们分别表示“纯”`tar` 归档和 `gzipped` 压缩归档。一个 `tar` 归档可以包含一组独立的文件、一个或多个目录层次结构，或者这两者的混合。命令语法如下：

```
tar mode[options] pathname...
```

其中 `mode` 是以下操作模式之一（此处仅显示了部分列表；完整列表请参阅 `tar` 的 man 页）：

表 18-2: `tar` 模式

| Mode | Description |
| --- | --- |
| c | 从一组文件和/或目录创建归档。 |
| x | 提取归档。 |
| r | 将指定的路径追加到归档末尾。 |
| t | 列出归档的内容。 |

`tar` 使用表达选项的方式略显奇怪，因此我们需要一些示例来展示它是如何运行的。首先，让我们重新创建上一章中的实验场：

```
[me@linuxbox ~]$ mkdir -p playground/dir-{001..100}
[me@linuxbox ~]$ touch playground/dir-{001..100}/file-{A..Z}
```

接下来，让我们为整个 `playground` 创建一个 `tar` 归档：

```
[me@linuxbox ~]$ tar cf playground.tar playground
```

此命令创建一个名为 `playground.tar` 的 `tar` 归档，包含了整个 `playground` 目录层次结构。我们可以看到，模式和 `f` 选项（用于指定 `tar` 归档名称）可以合并，并且不需要前导横杠。然而，`mode` 必须在任何其他选项之前始终指定。

要列出归档的内容，我们可以这样做：

```
[me@linuxbox ~]$ tar tf playground.tar
```

## 18 – 归档与备份

为了获得更详细的列表，我们可以添加 `v`（详细）选项：

```
me@linuxbox ~]$ tar tvf playground.tar
```

现在，在新位置提取 `playground`。我们将通过创建一个名为 `foo` 的新目录、进入该目录并提取 `tar` 归档来实现：

```
me@linuxbox ~]$ mkdir foo
me@linuxbox ~]$ cd foo
me@linuxbox foo]$ tar xf ../playground
me@linuxbox foo]$ ls
playground
```

如果我们检查 `~/foo/playground` 的内容，会发现归档已成功安装，创建了原始文件的精确复制。有一个例外：除非你以超级用户身份操作，否则从归档中提取的文件和目录将由执行恢复的用户所有，而不是原始所有者。

`tar` 的另一个有趣行为是它如何处理归档中的路径。路径默认是相对的，而不是绝对的。`tar` 通过在创建归档时简单地删除路径中的任何前导斜杠来实现。为了演示，我们将重新创建归档，这次指定一个绝对路径：

```
me@linuxbox foo]$ cd
me@linuxbox ~]$ tar cf playground2.tar ~/playground
```

当你按下按键时，`~/playground` 会展开为 `/home/me/playground`，因此我们的演示将得到一个绝对路径。接下来，我们将提取归档并观察会发生什么：

```
me@linuxbox]$ cd foo
me@linuxbox foo]$ tar xf ../playground
me@linuxbox foo]$ ls
home playground
me@linuxbox foo]$ ls home
```

### 归档文件

在这里我们可以看到已经提取了第二个归档，它相对于我们当前的目录 `~/foo` 重建了 `home/me/playground` 目录，而不是相对于根目录（如果是绝对路径则会是这种情况）。这看起来这种工作方式很奇怪，但实际上它更有用，因为它允许我们将归档提取到任何位置，而不是被迫从其原始位置提取。在包含详细选项（`v`）的情况下重复该练习，将更清晰地看到发生了什么。

让我们考虑一个假设但实用的 `tar` 示例。假设我们想将 `home` 目录及其内容从一个系统复制到另一个系统，并且有一个大 USB 盘可以用于传输。在我们的现代 Linux 系统中，驱动器“自动”挂载在 `/media` 目录。假设磁盘有一个名为 `BigDisk` 的卷。要创建归档，我们使用以下命令：

```
me@linuxbox ~]$ tar cf /media/BigDisk/backup.tar ~/home
```

（注：OCR 文本在末尾中断或变得重复。我将处理已有的内容。）

## 18 – 归档与备份

（再次，带有横杠参数的 `f` 选项）。

## zip

`zip` 程序既是压缩工具也是归档工具。该程序使用的文件格式对 Windows 用户来说很熟悉，因为它读取和写入 `.zip` 文件。然而，在 Linux 中，`gzip` 是主要的压缩程序，`bzip2` 紧随其后。

在最基础的用法中，`zip` 的调用方式如下：

```
zip options zipfile...
```

例如，为了为我们的 `playground` 目录创建一个 `zip` 归档，我们可以这样操作：

```bash
me@linuxbox -]$ zip -r playground.zip playground
```

除非我们包含递归的 `-r` 选项，否则只会存储 `playground` 目录（但不包含其任何内容）。虽然添加 `.zip` 扩展名是自动的，但为了清晰起见，我们会加上文件扩展名。

在创建 `zip` 归档期间，`zip` 通常会显示一系列此类消息：
