
这种技术被称为管道（`piping`），将在本小时稍后的“使用管道链接命令”一节中进行讨论。

## 让控制台为你工作服务

尽管你看到的实际图像文件列表取决于你在“第 2 小时：安装 Fedora”中安装的桌面环境和其他软件，但你几乎可以瞬间获得一个长串匹配的文件列表。

`locate` 使用的数据库在系统运行 `updatedb` 命令时重建一次。`locate` 显示的数据可能无法与你过去几个小时内完成的工作保持同步。然而，它使得 `locate` 能够快速地查找整个磁盘上的大量文件。

## 保存找到的文件列表

有时，保存搜索命令的输出是有帮助的。Shell可以通过将输出重定向到文件来帮助你保存 `find` 和 `locate` 等命令的输出。你可以将此类文件加载到 `emacs` 或 `vi` 等编辑器中进行编辑、解析或打印。要重定向命令的标准输出以满足你的需求，请使用大于号（`>`）符号后跟目标文件名。将 JPEG 文件列表保存到名为 `myjpegs.txt` 的文件中。

```bash
[you@workstation20 you]$ locate '*.jpg' > myjpegs.txt

[you@workstation20 you]$ ls -l

total

drwxr-xr-x 2 you you 4096 08-04 20:23 firstfiles

-rw-rw-r-- 1 you you 7944 08-04 21:12 myjpegs.txt

-rw-rw-r-- 1 you you 132 08-04 20:18 mymyfile.txt

-rw-rw-r-- 1 you you 135 08-04 20:18 mymyfile.txt

drwxr-xr-x 2 you you 4096 08-04 20:23 *new*

[you@workstation20 you]$
```

如你所见，你的主目录下有一个名为 `myjpegs.txt` 的文本文件列表。该文件包含了 `locate` 命令报告的你 Linux 文件系统中的 JPEG 文件列表。如果你想查看该文件，可以将其加载到 `emacs` 或 `vi` 中。

你可以重定向提示符处提供的几乎每个可用命令的输出。还可以使用双大于号（`>>`）将命令的标准输出追加到现有文件中。例如，要将所有 GIF 图像列表添加到 `myjpegs.txt` 中，请使用

```bash
[you@workstation20 you]$ locate '*.gif' >> myjpegs.txt

[you@workstation20 you]$
```

## 重定向输出时要小心

为了避免意外覆盖重要内容，在将命令输出追加到现有文件时请务必小心。当你使用单大于号（`>`）将命令的输出重定向到已存在的文件时，原文件的内容会被新数据覆盖。因此，在重定向数据时小心使用双大于号（`>>`）非常重要，这样你就不会覆盖文件。

## 在文本文件中搜索单词模式

你现在已经在主目录下创建了一个名为 `mypegs.txt` 的长文本文件，其中包含了存储在你的 Linux 文件系统中所有 JPEG 图像和所有 GIF 图像。但假设你想通过过滤来缩小列表：使用 `grep` 仅找到球的图片

你可以将 `mypegs.txt` 加载到 `emacs` 或 `vi` 中并视觉搜索符合你标准的文件，但通过使用 `grep` 命令搜索 `mypegs.txt` 可以更快地找到你需要的内容。`grep` 命令的唯一目的是在提供的文本文件中搜索你提供的单词或模式。你可以像这样调用 `grep`：

```bash
grep pattern1 [file2 ...]
```

这里，`pattern` 是要搜索的文本字符串，而 `file1`、`file2` 等是 `grep` 搜索的文件。这些文件中包含文本字符串或模式的行将显示在标准输出上（即控制台上）。尝试搜索球的图片：

```bash
[@@workstation20]$ grep ball mypegs.txt
/usr/share/apps/klines/balls.jpg
/usr/lib/openoffice/share/gallery/bullets/bluball.gif
/usr/lib/openoffice/share/gallery/bullets/darkball.gif
/..
/usr/lib/openoffice/share/gallery/rulers/gldballs.gif
/usr/lib/openoffice/share/gallery/rulers/grnballs.gif
/usr/lib/openoffice/share/gallery/rulers/whiteballs.gif
[@@workstation20]$
```

`grep` 命令在 `mypegs.txt` 中找到了许多包含 `ball` 单词的文件名。通过这种方法，`grep` 是从长列表中挖掘数据的伟大工具。

## 搜索包含特定单词的文本文件

你也可以使用 `grep` 来帮助寻找包含特定单词的文件。例如，你的主目录下目前有三个文本文件：`mypages.txt`、`mypymfile.txt` 和 `myfile.txt`。假设你需要找到其中哪些包含 `Unix` 单词。

使用带有 `-l`（列出文件）选项的 `grep`，你可以快速方便地获取结果：

```bash
[you@workstation20 you]$ grep -l Unix *
mynewfile.txt
myfile.txt
[you@workstation20 you]$
```

在这种情况下，`grep` 报告了工作目录中的两个文件 `mynewfile.txt` 和 `myfile.txt`。

### 注意大小写

当你使用 `grep` 时，它是区分大小写的。若要执行不区分大小写的搜索，请使用 `-i` 参数。

### 使用命令输出完成复杂任务

Shell 的最大优势之一是它允许执行多个步骤。连接命令的关键技术是使用管道——允许一个命令的输出作为另一个——以及命令替换——允许一个命令的输出

## 使用管道连接命令

有时将一个命令的输出作为另一个是非常方便的。例如，你已经有了 JPEG 和 GIF 图像列表，然后用 `grep` 搜索该文件。

## 第 5 小时

假设你现在想知道是否有 `.png` 或 `.tif` 图像。将 `locate` 的输出直接发送给 `grep` 不是很有帮助吗？你可以通过管道（`|`）来实现：

```bash
[you@workstation20 you]$ locate '*.gif' '*.jpg' '*.tif' '*.png' | grep ball
/usr/lib/openoffice/share/gallery/bullets/bluball.gif
/usr/lib/openoffice/share/gallery/bullets/darkball.gif
/..
/usr/share/pixmaps/ball.png
/usr/share/ImageMagick/images/ball.png
[you@workstation20 you]$
```

你生成了整个系统中四种格式图像列表。`locate` 命令（你提供了参数）的输出直接发送给了 `grep`，由 `grep` 搜索接收到的数据。

管道的一个更平凡但同样实用的应用是命令输出的分页。例如，尝试以下命令：

```bash
[you@workstation20 you]$ ls -l /usr/bin | more
```

这个列表很长；在你有机会看到之前，大部分内容都会滚动到控制台顶部。然而，通过管道将此命令的输出发送另一个名为 `more` 的命令，就可以解决这个问题。`more` 命令是一个分页器：它一次显示一页文件或输入数据，暂停并要求用户按空格键继续显示下一屏信息。尝试将 `ls` 的输出通过管道交给 `more`

## 将一个命令的答案作为另一个命令的参数

另一个基本的 Shell 工具是命令替换。命令替换允许将命令的输出作为一组命令行

## 让控制台为你工作

...作为另一个命令的参数。此过程允许第一个命令的结果改变第二个命令的行为，从而影响其输出，并根据当前情况对命令进行自定义。

假设你想创建一个名为 `jpegs` 的目录，并将系统中的每个 JPEG 图像都收集其中，以便索引和访问。你已经知道如何在 Linux 系统中通过 `locate` 找到所有以 `.jpg` 结尾的文件。有了这个输出，你可以使用命令替换将这些文件收集到一起：

```bash
you@workstation20$ mkdir jpegs
you@workstation20$ ln -s '$(locate *.jpg)' jpegs
you@workstation20$
```
