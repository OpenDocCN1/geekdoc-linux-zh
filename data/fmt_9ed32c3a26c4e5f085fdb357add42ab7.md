
| 模式 | 说明 |
| :--- | :--- |
| `c` | 从文件和/或目录列表创建归档。 |
| `x` | 提取归档。 |
| `r` | 将指定的路径追加到归档末尾。 |
| `t` | 列出归档的内容。 |

`tar` 使用选项的方式略显奇异，因此我们需要示例来展示它是如何运行的。首先，让我们重新创建上一章中的实验场：

```
$mkdir -p playground/dir-{00(1..9),0{10..99},100}
$ touch playground/dir-{00(1..9),0{10..99},100}/file-{A..Z}
```

接下来，让我们为整个 `playground` 创建一个 `tar` 归档：

```
$ tar cf playground.tar
```

此命令创建了一个名为 `playground.tar` 的 `tar` 归档，其中包含了 `playground` 目录结构。我们可以看到，模式和 `f` 选项（用于指定 `tar` 归档名称）可以合并在一起，且不需要前导横杠。注意，模式必须在任何其他选项之前指定。

要列出归档的内容，我们可以这样操作：

```
$ tar tf playground.tar
```

为了获得更详细的列表，我们可以添加 `v`（详细模式）选项：

```
$ tar tvf playground.tar
```

现在，让我们在一个新位置提取 `playground`。我们将通过创建一个新目录 `foo`、进入该目录并提取 `tar` 归档来实现：

```
$ mkdir foo
$ cd foo
$ tar xf ../playground
$ ls
playground
```

如果我们检查 `~/foo/playground` 的内容，会发现归档已成功安装，创建了原始文件的精确复制。然而，有一个例外：除非你是以该用户身份操作，否则从归档中提取的文件和目录将归执行恢复操作的用户所有，而不是原始所有者所有。

`tar` 的另一个有趣行为是它处理归档中路径的方式。路径的默认是相对的，而不是绝对的。`tar` 通过在创建归档时简单地删除路径中的任何前导斜杠来实现这一点。为了演示，我们将重新创建归档，这次指定一个绝对路径：

```
me@linuxbox foo$ cd
me@linuxbox~$ tar cf playground2.tar ~/playground
```

记住，当我们按下回车键时，`~/playground` 会展开为 `/home/me/playground`，因此我们的演示将获得绝对路径。接下来，我们将像以前一样提取归档看看发生了什么：

```
me@linuxbox ~$ cd foo
me@linuxbox foo$ tar xf ../playground2.tar
me@linuxbox foo$ ls
home
playground
me@linuxbox foo$ ls home

me@linuxbox foo$ ls home/me/
playground
```

在这里我们可以看到我们提取了第二个归档，它相对于当前工作目录 `~/foo` 重新创建了目录 `home/me/playground`，而不是相对于根目录（如果是绝对路径的话）。这看起来像是一个奇怪的修复方法，但对于将归档提取到任何位置而不被强制提取到原始位置是非常有用的。包含详细选项 (`v`) 重复练习将让我们更清楚地看到发生了。

让我们考虑一个 `tar` 应用的假设但实用的示例。假设我们想将家目录及其内容从一个地方拷贝到另一个，并且我们有一个大 USB 驱动器用于传输。在我们的现代 Linux 系统中，该驱动器“自动”挂载在 `/media` 目录下。重要的是，当我们连接它时，磁盘卷名为 `BigDisk`。为了制作 `tar` 归档，我们可以执行以下操作：

```
me@linuxbox~$ sudo tar cf /media/BigDisk/home.tar /home
```

文件写入后，我们卸载驱动器并将其连接到第二台电脑上。同样，它挂载在 `/media/BigDisk`。要提取归档，我们执行：

```
me@linuxbox2 ~$ cd /
me@linuxbox2~$ sudo tar xf /media/BigDisk/home.tar
```

重要的是，我们必须先切换目录到 `/`，这样提取才相对于根目录，因此归档内的所有路径都是相对的。

在提取归档时，可以限制提取的内容。例如，如果我们想从归档中提取单个文件，可以这样做：

```
tar x archive.tar pathname
```

通过在命令末尾添加路径，我们确保 `tar` 将恢复指定的文件。可以指定多个路径。注意，路径必须是存储在归档中的完整、精确的相对路径。在指定路径时，通常不支持通配符；然而，GNU `tar`（Linux 发行版中最常见的版本）通过 `--wildcards` 选项支持它们。这里有一个使用我们之前的 `playground.tar:file` 的示例：

```
[me@linuxbox] $ cd foo
[me@linuxbox foo] $ tar xf ../playground2.tar --wildcards 'home/me/playground/dir*/file-A'
```

此命令将仅提取匹配指定路径（包括通配符 `dir*`）的文件。`tar` 通常配合 `find` 使用来生成归档。在这个示例中，我们

在最基本的用法下，`zip` 的调用方式如下：

```
zip 选项 压缩文件...
```

例如，为了为我们的 `playground` 创建 `zip` 压缩包，我们可以这样做：

```
@me@linuxbox ~$ zip -r playground.zip playground
```

除非我们包含了用于递归的 `-r` 选项，否则只会存储 `playground` 目录（但不包含其任何内容）。虽然会自动添加 `.zip` 扩展名，但为了清晰起见，我们会手动包含文件扩展名。在创建 `zip` 压缩包的过程中，`zip` 通常会显示一系列如下所示的消息：

```
+ adding: playground/dir-020/file-Z (stored 0%)
adding: playground/dir-020/file-Y (stored 0%)
adding: playground/dir-020/file-X (stored 0%)
adding: playground/dir-087/ (stored 0%)
adding: playground/dir-087/file-S (stored 0%)
```

这些消息显示了添加到压缩包中的每个文件的状态。`zip` 将使用两种存储方法之一将文件添加到压缩包中：要么在不压缩的情况下“存储”文件（如此处所示），要么“压缩”（deflate）文件以进行压缩。存储方法后显示的数值表示所实现的压缩率。由于我们的 `playground` 不仅包含空文件，因此对其内容未进行任何压缩。

使用 `unzip` 程序解压 `zip` 文件的内容非常简单：

```
@me@linuxbox ~$ cd foo
@me@linuxbox foo$ unzip ../playground.zip
```

关于 `zip`（与 `tar` 相比）需要注意的一点是，如果指定了已存在的压缩包，它将会被更新而非替换。这意味着现有的压缩包会被保留，但新文件会被添加，且匹配的文件会被-

可以通过指定特定的文件来从 `zip` 压缩包中选择性地列出和提取文件：

```
@me@linuxbox ~$ unzip -l playground.zip playground/dir-087/file-Z
Archive: ./playground.zip
Length Date Name
0 10-05-12 09:25 playground/dir-087/file-Z
-----------
0 1 file
```

```
@me@linuxbox ~$ cd foo
@me@linuxbox foo$ unzip ../playground.zip playground/dir-087/file-Z
Archive: ../playground.zip
replace playground/dir-087/file-Z? [y]es, [n]o, [A]ll, [N]one, [r]ename: y
extracting: playground/dir-087/file-Z
```

使用 `-l` 选项会导致 `unzip` 仅列出压缩包的内容而不提取文件。如果没有指定文件，`unzip` 将列出列表中所有的文件。可以添加 `-v` 选项来增加列表的详细程度。请注意，当压缩包提取与现有文件冲突时，系统会在替换文件之前提示用户。

像 `tar` 一样，`zip` 可以利用标准输入和输出，尽管这在实现上实用性稍低。可以通过 `-option` 选项将文件名列表管道传输给 `zip`：

```
$me@linuxbox ~]$ cd
$me@linuxbox ~]$ find -name "file-A" | zip -@ file-A.zip
```
