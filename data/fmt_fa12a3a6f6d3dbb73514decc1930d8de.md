
全单颜色的图像包含完全冗余的数据。如果我们足够聪明，可以这样编码数据：只需描述我们有一个包含 10,000 个黑色像素的区块即可。因此，与其存储一个包含 30,000 个零的数据块（黑色在图像文件中通常表示为零），我们不如将数据压缩为数字 10,000，后面紧跟一个零来表示我们的数据。这种压缩方案被称为行程游程编码（run-length encoding），是基础压缩技术之一。今天的技术要先进和复杂得多，但基本目标仍然相同——消除冗余数据。

压缩算法（用于执行压缩的数学技术）分为两大大类。

- 无损压缩（Lossless）：无损压缩保留原始文件中包含的所有数据。这意味着当从压缩版本恢复文件时，恢复后的文件与原始未压缩文件完全相同。
- 有损压缩（Lossy）：另一方面，有损压缩在执行压缩时删除数据，以便应用更多的压缩。当恢复有损文件时，它与原始版本不匹配；相反，它是近似值。有损压缩的例子有 `JPEG`（用于图像）和 `MP3`（用于音乐）。

在我们的讨论中，我们将专注于无损压缩，因为计算机上的大多数数据无法容忍任何数据丢失。

## gzip

`gzip` 程序用于压缩一个或多个文件。执行时，它用原始文件的压缩版本替换原始文件。相应的 `gzip` 程序用于将压缩文件恢复到其原始的未压缩格式。以下是一个示例：

```
me@linux ~]$ ls -l /etc > foo.txt

me@linux ~]$ ls -l foo.*

-rw-r--r--r 1 me 15738 2025-10-14 07:15 foo.txt

me@linux ~]$ gzip foo.txt

me@linux ~]$ ls -l foo.*

-rw-r--r--r 1 me 3230 2025-10-14 07:15 foo.txt.gz

me@linux ~]$ gunzip foo.txt

me@linux ~]$ ls -l foo.*
-rw-r--r--r 1 me 15738 2025-10-14 07:15 foo.txt
```

在这个示例中，我们从目录列表创建一个名为 `foo.txt` 的文件。接下来，我们运行 `gzip`，它用一个名为 `foo.*` 的压缩版本替换了原始文件。在 `foo*` 的目录列表中，我们看到原始文件已被压缩版本替换，且压缩版本的大小约为原始文件的五分之一。我们还可以看到压缩文件与原始文件具有相同的权限和时间戳。

接下来，我们运行 `gunzip` 程序来解压文件。之后，我们可以看到文件的压缩版本已被原始文件替换，同样保留了权限和时间戳。

`gzip` 有许多许多选项，如表 18-1 所示。

表 18-1：`gzip` 选项

| 选项 | 长格式选项 | 描述 |
| --- | --- | --- |
| `-c` | `--stdout --tstdout` | 将输出写入标准输出并保留原始文件。 |
| `-d` | `--decompress --uncompress` | 解压。这导致 `gzip` 像 `gunzip` 一样工作。 |
| `-f` | `--force` | 即使原始文件的压缩版本存在也强制压缩。 |
| `-h` | `--help` | 显示用法信息。 |
| `-l` | `--list` | 列出每个压缩文件的压缩统计信息。 |
| `-r` | `--recursive` | 如果命令行上的一个或多个参数是目录，则递归压缩其中包含的文件。 |
| `-t` | `--test` | 测试压缩文件的完整性。 |
| `-v` | `--verbose` | 在压缩时显示详细信息。 |
| `-number` | | 设置压缩率。`number` 是 1（最快，压缩率最低）到 9（最慢，压缩率最高）之间的整数。 |

# 18 – 归档与备份

## tar

在 Unix 类软件世界中，`tar` 程序是归档文件的经典工具。它的名字是 tape archive（磁带存档）的缩写，揭示了它作为制作备份磁带工具的起源。虽然它仍然被用于传统任务，但它在其他存储设备上同样得手。我们经常看到扩展名为 `.tar` 或 `.tgz` 的文件，它们分别表示“纯”`tar` 归档和经过 `gzip` 压缩的归档。一个 `tar` 归档可以由一组独立的文件、一个或多个目录或它们的混合体组成。命令语法为：

```
tar mode[options] pathname...
```

这里，`mode` 是表 18-2 中列出的以下操作模式之一（此处仅显示了部分列表；完整列表请参见 `tar` 页面）。

表 18-2：`tar` 模式

| 模式 | 说明 |
| --- | --- |
| `c` | 从文件和/目录列表创建归档。 |
| `x` | 提取归档。 |
| `r` | 将指定的路径追加到归档末尾。如果归档不存在，则创建它。 |
| `t` | 列出归档的内容。 |

`tar` 使用了一种略显奇怪的方式来表示选项，因此我们需要一些示例来展示它是如何工作的。首先，让我们重新创建上一个章节中的实验场。

```
[@linuxbox ~]$ mkdir -p playground/dir-{001..100}
[@linuxbox ~]$ touch playground/dir-{001..100}/file-{A..Z}
```

接下来，让我们为整个 `playground` 创建一个 `tar` 归档。

```
[@linuxbox ~]$ tar cf playground.tar playground
```

此命令创建了一个名为 `playground.tar` 的 `tar` 归档，其中包含了整个 `playground` 目录树。我们可以看到，模式和 `f` 选项（用于指定 `tar` 归档的名称）可以合并，且不需要前导横杠。注意，模式必须始终在任何选项之前指定。

若要列出归档的内容，我们可以这样做：

```bash
[me@linuxbox ~]$ tar tf playground.tar
```

为了获得更详细的列表，我们可以添加 `v`（详细模式）选项。

```bash
[me@linuxbox ~]$ tar tvf playground.tar
```

现在，让我们在一个新位置提取 `playground`。我们将通过创建一个名为 `foo` 的新目录、进入该目录并提取 `tar` 归档来实现。

```bash
[me@linuxbox ~]$ mkdir foo
[me@linuxbox ~]$ cd foo
[me@linuxbox ~]$ tar xf ../playground
[me@linuxbox ~]$ ls
```

如果我们检查 `~/playground` 的内容，会发现归档已成功提取，创建了原始文件的精确复制。然而，有一个例外：除非我们以超级用户身份进行操作，否则从归档中提取的文件和目录将归执行恢复操作的用户所有。

`tar` 的另一个有趣行为是它处理归档中路径的方式。路径的默认是相对路径，而不是绝对路径。`tar` 通过在创建归档时简单地删除路径中的任何领先斜杠来实现这一点。为了演示，我们将重新创建归档，这次指定一个绝对路径。

```bash
[me@linuxbox ~]$ cd
[me@linuxbox ~]$ tar cf playground.tar ~/playground
```

记住，当我们按下回车键时，`~/playground` 会展开为 `/home/me/playground`，我们将为演示获得一个绝对路径。接下来，我们将提取归档并观察发生了什么。

```bash
[me@linuxbox ~]$ cd foo
[me@linuxbox ~]$ tar xf ../playground
[me@linuxbox ~]$ ls
home
[me@linuxbox ~]$ ls home/playground
```

在这里我们可以看到，当我们提取归档时，我们相对于当前工作目录 `~/foo` 重新创建了目录 `home/playground`，而不是相对于根目录（如果是绝对路径就会变成那样）。这种工作方式似乎很奇怪，但它实际上更有用，因为它允许我们将归档提取到任何位置，而不是被强制提取到原始位置。通过包含详细模式选项 `v` 并重复该练习，将更清晰地看到其过程。

让我们考虑一个 `tar` 运行的假设性实际示例。假设我们想将家目录及其内容从一个系统拷贝到另一个系统，并且我们有一个大 USB 硬盘可以用于传输。在我们现代 Linux 系统上，该驱动器挂载在 `/media` 目录下。假设在连接磁盘时，其卷名为 `BigDisk`。为了制作归档，我们可以执行以下操作：

```bash
[me@linuxbox ~]$ sudo tar cf /media/BigDisk/home.tar /home
```

文件写入后，我们挂载驱动器并将其连接电脑。同样，它挂载在 `/media/BigDisk`。要提取它，我们可以这样做：

```bash
[me@linuxbox ~]$ cd /
[me@linuxbox ~]$ sudo tar xf /media/BigDisk/home.tar
```

这里重要的是，我们必须切换目录到 `/`，这样提取就是相对于根目录的，因为归档内的所有路径都是相对路径。在提取归档时，可以限制提取的内容。例如，如果我们想从归档中提取单个文件，可以这样操作：

```
tar xf archive.tar pathname
```

通过在命令末尾添加 `pathname`，`tar` 将只会提取指定的文件。可以指定多个路径。注意，`pathname` 必须是完整且精确的。由于归档中存储的是相对路径，在指定路径时，通常不支持通配符；但是，GNU 版本的 `tar` 通过 `--wildcards` 选项支持它们。

## 归档文件

使用 `tar` 创建归档（`c` 模式）并将其发送到标准输出而不是文件（使用带横杠参数的 `f` 选项），从而通过 `ssh` 提供的加密隧道传输归档。在本地系统中，我们执行 `tar` 并让其展开从标准输入提供的归档（再次使用带横杠参数的 `f` 选项）（`x` 模式）。

## zip

`zip` 程序既是压缩工具也是归档工具。该程序使用的文件格式对 Windows 用户来说很熟悉，因为它能够读取和写入 `.zip` 文件。然而，在 Linux 中，`gzip` 是主要的压缩程序，`bzip2` 紧随其后。

在最基础的用法中，`zip` 的调用方式如下：

```
zip options zipfile...
```

例如，为了为我们的 `playground` 创建一个 `zip` 归档，我们可以这样做：

```
[me@linux ~]$ zip -r playground.zip playground
```

除非我们包含用于递归的 `r` 选项，否则只会存储 `playground` 目录（但不包含其任何内容）。虽然添加 `.zip` 扩展名是自动的，但为了清晰起见，我们将包含文件扩展。
在创建 `zip` 归档期间，`zip` 通常会显示类似下面的消息：

```
adding: playground/dir-028/file-Z (stored 0%)
adding: playground/dir-028/file-Y (stored 0%)
adding: playground/dir-028/file-X (stored 0%)
adding: playground/dir-087/ (stored 0%)
adding: playground/dir-087/file-S (stored 0%)
```

这些消息显示了添加到归档中的每个文件的状态。`zip` 将使用两种存储方法之一将文件添加到归档：要么不压缩直接“存储”（store）文件（如所示），要么“压缩”（deflate）来对其压缩。存储方法后显示的数值表示已实现的压缩量。由于我们的 `playground` 仅包含空文件，因此对其内容没有进行任何压缩。
使用 `unzip` 程序提取 `zip` 文件的内容是非常直接的。

```
[me@linuxbox ~$] cd foo
[me@linuxbox foo]$ unzip ../playground.zip
```

关于 `zip`（与 `tar` 相比）需要注意的一点是，如果指定了已存在的归档，它将进行更新而不是替换。这意味着现有归档会被保留，但会添加新文件并替换匹配的文件。

可以通过指定文件让 `unzip` 从 `zip` 归档中删除和提取文件。

```
[me@linuxbox ~$] unzip -l playground.zip playground/dir-087/file-Z
Archive: ../playground.zip
Length Date Name
0 10-05-25 09:22 playground/dir-087/file-Z
0 1 file
[me@linuxbox ~$] cd foo
[me@linuxbox foo]$ unzip ../playground.zip playground/dir-087/file-Z
Archive: ../playground.zip
replace filename/dir-087/file-Z? [y]es, [n]o, [A]ll, [N]one, [r]ename:
```
