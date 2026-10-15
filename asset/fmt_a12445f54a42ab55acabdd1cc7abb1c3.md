
# 入门

在这篇文章中，您将学习如何确定下一步。

## 下一步

在了解此之后，您就可以开始了。

## 文章

以下步骤显示了使用纯文本编辑器生成简单的 `DocBook XML` 文档，并输出到许多 `Linux` 系统可用 `HTML` 工具的示例。

## 在 `Linux` 中打印

如今大多数 `Linux` 系统的打印由通用打印系统 (`CUPS`) 提供。作为非管理员用户，您对打印机没有控制权。但是，您可以检查哪些打印机可用、检查打印队列（等待打印的文件），并删除任何队列中的打印任务。

### 打印到默认设备

当系统管理员（或您）为计算机配置打印机时，其中一台打印机被定义为默认打印机。如果您不确定 `Fedora Core` 或 `Red Hat` 发行版中哪个打印机是默认的，可以使用 `system-config-printer`。对于其他发行版，请检查 `CUPS` Web 界面以查看打印机配置。

大多数图形文字处理器（如 `StarOffice Writer` 和 `OpenOffice.org Writer`）允许您从可用打印机中选择。一些从命令行运行的较少 `Linux` 工具只使用默认打印机。

作为普通用户，可以使用 `PRINTER` 环境变量来覆盖默认打印机。例如，如果您的计算机默认打印机是 `lp0`，而您想打印到 `lp1`，可以通过设置 `PRINTER` 变量来更改默认打印机：

```bash
$ export PRINTER=lp1
```

为了一直生效，您可以将其添加到您的 shell 配置文件中。

### 从 Shell 打印

`lpr` 命令用于从 shell 打印文件。您可以使用 `lpr` 检查正在使用 `LPR` 还是 `CUPS` 打印服务。如果您有一个格式化好的文件，可以使用 `lpr` 进行打印。例如，如果您有一个 `PostScript` 输出文件 `file.ps`，并且您想将其打印到您的 `PostScript` 打印机，请使用以下命令行：

```bash
$ lpr file.ps
```

#### 指定打印机

如果你想指定特定的打印机（默认打印机之外），请添加 `-Pprinter` 选项。例如，要打印到 `lp0` 打印机，请输入以下命令：

```bash
$ lpr -Plp0 file.ps
```

如果你想打印一份文件的多个副本，请使用 `-num` 选项，其中 `num` 替换为你想要打印的副本数。例如，要打印五份该文件，请使用：

```bash
$ lpr -n5 file.ps
```

`lpr` 命令还可以接受标准输出进行打印。例如，你可以通过管道将 `groff` 命令的输出传递给 `lpr` 来打印其输出：

```bash
$ groff -Tps -man /tmp/chown.1 | lpr -Plp0
```

![](img/a123b4f2456cac935474ae2401b95b01_607_0.png)

`encript` 命令（在 `encript` 包中）是另一个打印文本文件的有用工具。它可以将文件转换为 `PostScript` 并将其发送到打印机或指定的文件。

### 检查打印队列

要检查已队列打印作业的状态，请使用 `lpq` 命令。`lpq` 本身会列出默认打印机队列中的作业列表。例如：

```bash
$ lpq
```

| 优先级 (Rank) | 所有者 (Owner) | 作业 (Job) | 文件 (Files) | 总大小 (Total Size) |
|---|---|---|---|---|
| active | root | 3 | hosts | 1024 bytes |
| 1st | root | 7 | (stdin) | 625 bytes |
| 2nd | root | 8 | memol.ps | 12273 bytes |
| 3rd | chuck | 9 | bikes.ps | 10880 bytes |

`lpq` 的输出显示打印机状态和等待打印的作业。`Rank` 列出了它们的队列顺序。`Owner` 是提交作业的用户。`Job` 显示作业号。`Files` 列显示文件名或标准输出（如果文件被管道或重定向到 `lpr`）。`Total Size` 显示每个文件的大小。

你可以为 `lpq` 添加选项来打印不同类型的作业。通过添加 `-Pprinter`，你可以查看任何可用打印机的队列。你还可以添加作业号（查看特定打印作业的状态）或用户名（查看该用户的所有已队列作业）。

### 移除打印作业

如果你错误地打印了一份大文档，你就会理解能够从队列中移除打印作业的价值。同样，如果打印机将停止一段时间，而每个人已经将作业打印到了另一台打印机，那么当打印机重新上线时，清除所有打印作业有时是件好事。

使用 `lprm` 移除打印作业。例如，要移除用户 `bill` 的所有作业（假设你是 `bill` 或 `root` 用户），请输入以下命令：

```bash
$ lprm bill
```

`root` 用户可以移除队列中的所有打印作业。要这样做，你需要在 `lprm` 命令行添加一个连字符 (`-`)，如下：

```bash
$ lprm -
```

你还可以通过仅向 `lprm` 命令行添加作业号，为特定打印机 (`-Pprinter`) 或特定作业重新排队打印。

### 检查打印机状态

有时打印机没有输出内容，而你不知道为什么。`lpc` 是一个状态命令，可能会为你提供有关打印机情况的线索。它是专为管理员设计的，因此可能不在你的默认 `PATH` 中。要使用 `lpc` 命令，请输入：

```bash
# /usr/sbin/lpc
```

当命令返回 `lpc>` 提示符时，输入单词 `status`：

```bash
lpc> status
h:
    printer is on device 'lpd' speed -1
    queuing is enabled
    printing is enabled
    no entries
    daemon present
```

此示例显示了打印机 `hp` 的状态：队列和打印已启用，打印机显示没有问题，没有等待的打印作业。要退出 `lpc` 命令，在 `lpc>` 提示符处输入 `exit`。

### 使用 `ghostscript` 和 `Acrobat` 显示文档

如果你每次想更改文档的内容或格式都将 `Groff` 或 `LaTeX` 文档发送到打印机，文档出版可能会消耗大量的纸。为了节省时间，请使用打印预览程序在屏幕上显示文档在打印页面上的样子。接下来的章节描述了用于显示 `Postscript` 文件的 `ghostscript` 命令以及用于显示可移植式文档格式 (`PDF`) 文件的 `Adobe Acrobat Reader`。

#### 使用 `ghostscript` 和 `gv` 命令

在 `Linux` 中显示 `Postscript` 或 `PDF` 文档，你可以使用 `ghostscript` 命令。这是一个相当原始的界面，旨在让你逐个查看文档并一次解释一个。

你可以显示计算机上拥有的任何 `PS` 或 `PDF` 文件。例如，如果安装了该包，你可以使用以下命令显示一个 `PDF` 文件（否则，你可以生成自己的 `PDF` 文件进行尝试）：

```bash
$ ghostscript /usr/share/doc/samba/* /doc/samba HOWTO-Collection.pdf
>>showpage, press <return> to continue<<
```

在提示符处，按 `Enter`（或 `Return`）键以逐页查看文件。当你到达文档末尾时，可以输入 `Postscript` 或 `PDF` 文件的文件名并翻阅该文件。完成后，退出。

`gv` 命令（`GNOME` 视器）是另一种查看 `Postscript` 文件的友好方法。要使用 `gv` 打开文件，请输入：

```bash
$ gv /usr/share/doc/samba/*
```

当 `gv` 窗口打开时，你可以翻阅文档。你还可以显示书签列表以跳转到特定页面。完成后，退出。

#### 使用 `Adobe Acrobat`

可移植式文档格式 (`PDF`) 提供了一种以打印形式存储文档的方法。使用 `Adobe Acrobat Reader`，你可以查看 `PDF` 文件。`Adobe Acrobat` 有许多很好的功能。例如，你可以在文档旁边显示书签列表并点击书签进入特定页面。你还可以显示页面缩略图以便快速滚动。

使用菜单栏或按钮，你可以翻阅文档、放大和缩小、跳转到开头或结尾。要打印副本，选择文件：打印。

### 处理图形

在 `Linux` 系统中，创建和处理图形的工具变得越来越丰富和强大。领先的是 `GNU` 图像处理程序 (`GIMP`)。`GIMP` 可以让你创作和制作图像，还可以调整照片。其他创建图形的工具包括 `ksnapshot`（截图程序）和 `kpaint`（处理位图）。

#### 使用 `GIMP` 处理图像

`GIMP` 是一种处理照片和图形图像的免费软件。使用 `GIMP` 创建图像，你可以导入绘画、照片或 3D 图像，也可以从头创建。你可以通过系统菜单选择图形 < `GIMP`，或在终端窗口中输入 `gimp` 来启动 `GIMP`。
