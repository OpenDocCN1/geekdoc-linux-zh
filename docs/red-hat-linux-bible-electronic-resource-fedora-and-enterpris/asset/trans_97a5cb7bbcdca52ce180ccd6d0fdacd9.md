

$ lpr file.ps

如果要指定特定打印机（而非默认打印机），请添加 `-P` 选项。例如，要打印到 lp0 打印机，可以输入以下命令：

```
$ lpr -Plp0 file.ps
```

如果要打印文档的多份副本，请使用 `-#num` 选项，其中 num 替换为你想要的副本数量。例如，要打印文件的五份副本，请使用：

```
$ lpr -#5 file.ps
```

`lpr` 命令也可以接受标准输出进行打印。例如，你可以通过管道将 `groff` 命令的输出传送给 `lpr` 来打印，如下所示：

```
$ groff -Tps -man /tmp/choen.l | lpr -Plp0
```

> **提示：** `enscript` 命令（在 `enscript` 软件包中）是另一个用于打印纯文本文件的有用工具。它将文件转换为 PostScript 并发送到打印机或指定文件。

## 检查打印队列

要检查已排队打印作业的状态，可以使用 `lpq` 命令。单独使用时，`lpq` 会列出默认打印机队列中的作业。例如：

```
$ lpq
hp is ready and printing
Rank    Owner    Job    Files         Total Size
active    root     3     hosts         1024 bytes
1st       root     7     (stdin)       625 bytes
2nd       root     8     mem01.ps      12273 bytes
3rd       chuck    9     bikes.ps      10880 bytes
```

`lpq` 的输出显示打印机状态和等待打印的文件。Rank 列出它们在队列中的顺序。Owner 是将作业加入队列的用户。Job 显示作业编号。Files 列显示文件名或标准输出（如果文件是通过管道或重定向传给 lpr 的）。Total Size 显示每个文件的大小（以字节为单位）。

| Rank  | Owner | Job | Files    | Total Size |
|-------|-------|-----|----------|------------|
| active| root  | 3   | hosts    | 1024 bytes |
| 1st   | root  | 7   | (stdin)  | 625 bytes  |
| 2nd   | root  | 8   | mem01.ps | 12273 bytes|
| 3rd   | chuck | 9   | bikes.ps | 10880 bytes|

你可以向 `lpq` 添加选项以打印不同类型的信息。通过添加 `-Pprinter`，你可以查看任何可用打印机的队列。你也可以添加作业编号（查看特定打印作业的状态）或用户名（查看某用户的所有排队作业）。

## 移除打印作业

如果你曾经误打印过大型文档，就会明白能够从队列中移除打印作业的价值。同样，如果打印机将停机一段时间，而每个人已经将作业打印到另一台打印机上，有时在打印机重新上线时能够清除所有打印作业会很方便。

在 Red Hat Linux 中使用 `lprm` 移除打印作业。例如，要移除名为 `bill` 的用户的所有作业（假设你是 `bill` 或 root 用户），请输入以下命令：

```
$ lprm bill
```

root 用户可以移除队列中的所有打印作业。为此，请在 `lprm` 命令行中添加短划线 (-)，如下所示：

```
$ lprm -
```

你也可以通过添加作业编号，移除特定打印机 (`-Pprinter`) 的排队打印作业或特定作业编号的作业。

## 检查打印机状态

有时打印机没有任何输出，而你却不知原因。`lpc` 命令是一个打印机状态命令，运行它可能会给你一些关于打印机状况的线索。`lpc` 命令面向管理员，因此它可能不在你的默认 PATH 中。要启动 `lpc` 命令，请输入以下内容：

```
# /usr/sbin/lpc
lpc> status

hp:
		printer is on device 'lpd' speed -l
		queing is enabled
		printing is enabled
		no entries
		daemon present

lpc>
```

当命令返回 `lpc>` 提示符时，输入单词 `status`。此例显示了打印机 `hp` 的状态。这里，排队和打印均已启用。打印机显示无问题，无打印作业等待。

## 使用 Ghostscript 和 Acrobat 显示文档

如果每次想更改文档内容或格式都将 Groff 或 LaTeX 文档发送到打印机，Red Hat Linux 的发布工作会非常消耗纸张。为了节省纸张和减少奔波时间，你可以使用一些打印预览程序，在屏幕上显示文档在打印页面上的外观。以下部分介绍用于显示 PostScript 文件的 `ghostscript` 命令和用于显示便携文档格式 (PDF) 文件的 Adobe Acrobat 阅读器。

### 使用 ghostscript 和 gv 命令

要在 Red Hat Linux 中显示 PostScript 或 PDF 文档，可以使用 `ghostscript` 命令。`ghostscript` 命令是一个相当简陋的界面，旨在让你逐步浏览文档并逐行解释它们。（如果系统未安装 `ghostscript` 命令，你可以通过安装随本书附带的 CD #1 中的 ghostscript 软件包来获取它。）

你可以显示计算机上碰巧拥有的任何 .ps 或 .pdf 文件。例如，如果安装了 samba 软件包，你可以输入以下命令来显示一个 PDF 文件（否则，你可以找一个自己的 PDF 文件尝试）：

```
$ ghostscript /usr/share/doc/samba-*/docs/Samba-HOWTO-Collection.pdf
>>showpage, press <return> to continue<<
```

在提示符下，按 Enter（或 Return）键逐页浏览文件。文件读完后，你可以输入另一个 PostScript 或 PDF 文件的名称并翻阅该文件。完成后，输入 quit。

`gv` 命令（ghostview）是查看 PostScript 文件的另一种更友好的方式。（如果系统未安装 `gv` 命令，你可以通过安装随本书附带的 CD #3 中的 `gv` 软件包来获取它。）

要使用 `gv` 打开名为 `xbash.ps` 的文件，请输入以下命令：

```
$ gv /usr/share/doc/bash-doc-*/bashref.ps
```

当 ghostview 窗口打开时，你可以看到文档。在页面上左键单击鼠标并上下移动以滚动文档。使用 Page Up 和 Page Down 键翻页。你可以单击左栏中的页码跳转到特定页面，或单击“Print All”按钮打印整个文档。

### 使用 Adobe Acrobat Reader

便携文档格式 (PDF) 提供了一种按打印外观存储文档的方式。使用 Adobe Acrobat Reader，你可以非常友好地查看 PDF 文件。Adobe Acrobat 使在 PDF 文件中移动变得容易。PDF 文件可能包含超链接、目录、图形和多种字体。

Adobe Acrobat Reader 的最新版本（版本 5.06）可从 Guru Labs (www.gurulabs.com/downloads.html) 处获得 RPM 格式。此版本可以使用其他 PDF 阅读器中不可用的许多 PDF 功能，包括版本 1.4 中的一些新压缩功能。（顺便说一句，你可以安装 Acrobat Plug-in RPM，以便在浏览网页时使用同一阅读器播放 PDF 内容）。

安装 Adobe Acrobat Reader 后，输入以下命令启动程序：

```
$ acroread
```

单击“文件” -> “打开”，然后选择要显示的 PDF 文件名。图 6-12 显示了在 Adobe Acrobat Reader 中查看的 PDF 文件示例。

![](img/27a85d56d393921ced6412ae6e8336bf_259_0.png)

**图 6-12**：在 Adobe Acrobat Reader 中显示 PDF 文件。

Acrobat Reader 有许多不错的功能。例如，你可以在文档旁显示书签列表，并单击书签转到特定页面。你还可以显示页面缩略图，以快速浏览并选择页面。

使用菜单栏或按钮，你可以翻阅 PDF 文档、放大和缩小、跳转到文档开头或结尾，并显示文档的不同视图（以及显示书签和页面缩略图）。要打印副本，请单击**文件** → **打印**。

## 处理图形

在 Red Hat Linux 中，用于创建和处理图形的工具变得越来越丰富和强大。首当其冲的是 **GNU 图像处理程序 (GIMP)**。GIMP 允许你合成和创作图像，以及修饰照片。Red Hat Linux 中附带的其他创建图形的工具包括 **ksnapshot**（一个用于屏幕捕获的程序）和 **kpaint**（用于处理位图图像）。

> **交叉引用：** 请参阅第 8 章，了解其他多媒体应用程序的描述，例如用于处理数码相机图像的 gphoto 窗口。

### 使用 GIMP 处理图像

GIMP 是随 Red Hat Linux 附带的免费软件程序，用于处理照片和图形图像。要使用 GIMP 创建图像，你可以导入绘图、照片或 3D 图像，也可以从头开始创建。你可以通过单击系统菜单中的**图形** → **The GIMP**，或在终端窗口中输入 **gimp&** 来启动 GIMP。

