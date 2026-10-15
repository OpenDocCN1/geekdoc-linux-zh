
$ head -2 heart ...列出前几行

I hear her breathing,

I'm surrounded by the sound.

$ tail -2 heart ...列出后几行

Floating in this secret place,

I never shall be found.

$

```

## 重命名文件：mv

现在我已经了歌词的第一稿，我想再创建几个版本。为了表示文件 "heart" 是第一个版本，我决定使用 `mv` 工具将其重命名为 "heart.ver1"，它的工作方式如图 20 所示。以下是我如何使用 `mv` 工具的第一种形式重命名文件的：

| 工具 | 描述 |
| :--- | :--- |
| `mv -i` `oldFileName` `newFileName` | `mv -i` `{fileName}*` |
| `mv -i` `oldDirectory` `newDirectoryName` | |

`mv` 的第一种形式将 `oldFileName` 重命名为 `newFileName`。如果 `newFileName` 已经存在，它将被替换。第二种形式允许你将一组文件移动到目录，第三种形式允许你移动整个目录。如果文件在同一个系统内，这些选项实际上并不会移动文件的物理内容；它们只是在移动标签。因此，`mv` 是一个非常快的工具。`-i` 选项会在 `newFileName` 已经存在时提示你进行确认。

图 2.20

mv 命令描述。

```bash
$ mv heart heart.ver1 ...重命名为 "heart.ver1"

$ ls

heart.ver1
```

`mv` 工具的第二种和第三种形式将在本章稍后部分说明。

## 创建目录：mkdir

为了不让我的主目录被 "heart" 的各个版本弄乱，我决定创建一个名为 "lyrics" 的子目录来存放所有内容。为了做到，我使用了 `mkdir` 工具，它的工作方式如图 21 所示。以下是我的操作：

| 工具 | 描述 |
| :--- | :--- |
| `mkdir [-p]` `newDirectoryName` | `mkdir` 工具创建一个目录。`-p` 选项创建 `newDirectoryName` 路径中不存在的任何父目录。如果 `newDirectoryName` 已经存在，则会显示错误信息且不会对现有文件进行任何修改。 |

图 2.21

mkdir 命令描述。

```bash
$ mkdir lyrics ...创建一个名为 "lyrics" 的目录

$ ls -lf ...确认。

-rw-r--r-- 1 glass 106 Jan 30 23:28 heart

drwxr-xr-x 2 glass 512 Jan 30 19:49 lyrics/
```

"lyrics" 权限标志开头的字母 "d" 表示它是一个目录。通常，你应该将相关文件放在它们自己的独立目录中。如果你为目录命名合理，那么即使在创建多年后，也容易追踪文件。一旦 "lyrics" 目录创建完成，下一步是将 "heart.ver1" 移动到它的新位置。为了这样做，我使用了 `mv` 并通过以下命令确认了操作：

```bash
$ mv heart.ver1 lyrics ...移动到 "lyrics"

$ ls ...列出当前目录。

lyrics/ ..."heart.ver1" 消失了。

$ ls lyrics ...列出 "lyrics" 目录。

heart.ver1 ..."heart.ver1" 已移动。

```

## 切换目录：cd

虽然我可以留在主目录，并通过在文件名前以前缀 "lyrics/" 来访问各个版本的歌词文件，但这样做相当不方便。要用 UNIX vi 编辑器编辑文件 "heart.ver1"，我必须执行以下操作：

```bash
$ vi lyrics/heart.ver1 ...调用 vi 编辑器。
```

通常，如果你打算进行大量工作，将你的 shell 移动到一个目录是一个好主意。要这样做，请使用 `cd` 命令。`cd` 并不是真正的 UNIX 工具，而是你的 shell 将 `cd` 识别为特殊关键字并直接执行它。注意我在我在书开头描述的命名法，使用斜体编写 shell 命令。图 2.22 显示了 `cd` 如何工作。

> Shell 命令：cd [ directoryName ]

`cd`（切换目录）shell 命令会更改 shell 当前的工作目录。如果省略了 `directoryName` 参数，shell 将移动到它自己的主目录。

图 2.22

cd shell 命令描述。

下面的示例显示了我如何进入 "lyrics" 目录并使用 `pwd` 确认了我的新位置：

```bash
$ pwd ...显示我所在的位置。

/home/glass

cd lyrics ...进入 "lyrics"

$ pwd ...显示我所在的位置。

/home/glass/lyrics
```

图 2.23 是 `cd` 引起移动的插图。

## 删除目录：rmdir 35

在为我的歌词创建了五个版本后，我的工作完成了。我回到主目录，并创建了一个名为"lyrics.final"的子目录来存储歌词的最终版本。我还将原始的“目录”重命名为“lyrics.draft”，我觉得这个名字更好。执行这些操作的命令如下：

```

$ cd ~ ...回到主目录。

$ mkdir lyrics.final ...创建最终歌词目录。

$ mv lyrics lyrics.draft ...重命名旧目录。

$ -
```

我歌词的最终版本存储在"lyrics.draft"目录下一个名为"heart.ver5"的文件中，然后我将其复制到"lyrics.final"目录中一个名为"heart.final"的文件中：

```

$ cp lyrics.draft/heart.ver5 lyrics.final/heart.final

$ -
```

## 删除目录：rmdir

虽然为了后世是保留东西的一个好理由，但在多用户系统中，这可能会干扰你的磁盘空间。因此，我决定删除"lyrics.draft"目录，以避免超出我有限的磁盘配额。不过，在删除它之前，我使用 cpio 工具对其内容进行了存档，该工具在第3章中有描述。要删除目录，我使用了 rmdir 工具，它的工作原理如图 2.25 所示。

> 工具：rmdir { 目录名 }

rmdir 从目录列表中删除所有目录。目录在删除之前必须是空的。要递归地删除一个目录及其所有内容，请使用带有 -r 选项的 rm 工具（稍后将描述）。

图 2.25

rmdir 命令的描述。

我尝试在"lyrics.draft"目录仍包含草稿版本时删除它，结果收到了以下错误消息：

```

$ rmdir lyrics.draft

rmdir: lyrics.draft: 目录不空

$ -
```

为了删除"lyrics.draft"目录中的文件，我使用了接下来描述的 rm 工具。

## 第2章 非程序员准备的 UNIX 工具

## 删除文件：rm

rm 工具允许你从层级结构中移除文件的标签。在大多数情况下，每个文件只有一个引用文件的标签，UNIX 会删除文件本身。因此，移除标签的操作会导致文件的物理内容被释放。然而，在第3章中，我将向你展示一些单个文件具有多个标签的情况。在这些情况下，移除一个标签可能不会影响它所指的文件。图 2.26 提供了 rm 的描述。

```

工具：rm -fi { 文件名 } *

rm 工具从目录层级结构中移除文件的标签。如果文件名不存在，则显示错误消息。-i 选项在删除文件之前提示用户确认；按 y 确认你的请求，否则按 n。如果 fileName 是目录，-r 选项将导致其所有内容（包括子目录）被递归删除。-f 选项将抑制所有错误消息。

```

图 2.26

rm 命令的描述。

为了删除"lyrics.draft"目录中的每个文件，我进入了"lyrics.draft"目录并使用 rm 进行删除：

```

$ cd lyrics.draft ..进入 "lyrics.draft" 目录。

$ rm heart.ver1 heart.ver2 heart.ver3 heart.ver4 heart.ver5

$ ls ..空无一物。

$ _
```

现在所有文件都删除了，我回到主目录并删除了草稿目录：

```

$ cd ..回到我的主目录。

$ rmdir lyrics.draft ..这次成功了。

$ _
```

正如你在第4章中将看到的，当你使用 shell 时，删除一组文件有一种简单得的方法。我本可以写成：

```

$ cd lyrics.draft ..进入 "lyrics.draft" 目录。

$ rm * ..删除当前目录下的所有文件。
```
