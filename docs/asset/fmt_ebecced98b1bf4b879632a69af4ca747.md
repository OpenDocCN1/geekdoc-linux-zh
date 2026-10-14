
```
AMRECOVER Version 2.4.1p1. Contacting server on atlantic ...
220 atlantic AMANDA index server (2.4.1p1) ready.
200 Access OK
Setting restore date to today (1999-11-29)
200 Working date set to 1999-11-29.
200 Config set to daily.
200 Dump host set to atlantic.
Can't determine disk and mount point from $CWD
amrecover>
```

首先确定转储主机（即丢失文件的机器）是否正确；如果不正确，在 `amrecover>` 提示符下输入

```
sethost host
```

让它查看 `host` 上的文件系统。接下来你将输入

```
setdisk disk
```

设置目录（在上述主机上）文件曾经所在的位置。你可能还想指定 `setdate yyyy-mm-dd` 来查看特定日期的文件索引（而不是最近的）。现在你可以使用 `cd` 和 `ls` 来浏览备份中目录的内容。当你找到想要从归档中提取的文件或目录时，使用 `add name` 将 `name` 添加到要提取的文件或目录列表中。继续浏览归档，直到你对想要恢复的所有内容都使用了 `add`，然后输入 `list` 来确认你的选择。当你准备好时，输入 `extract` 从归档中提取文件。你需要回答几个问题；这里有一个示例对话：

```
Extracting files using tape drive /dev/nst0 on host atlantic.
The following tapes are needed: dailytapes01

Restoring files into directory /tmp
Continue? [Y/n]: y

Load tape dailytapes01 now
Continue? [Y/n]: y
...
```

回答完问题后，Amanda 会为你从磁带上抓取数据（在这个例子中，它将文件恢复到 `/tmp` 下；如果你不喜欢这样，使用 `lcd` 更改本地工作目录）。请记住，恢复通常需要一段时间。

使用 `help` 命令访问 `amrecover` 的在线帮助；它相当简略，但在需要时可以给你一点提示。

相关手册页：`amrecover (8)`, `amrestore (8)`

## Using Amanda Log Files for Recoveries if amrecover Is Unavailable

如果 Amanda 实用程序 `amrecover` 和 `amrestore` 不可用，你可以直接从磁带上提取归档。为此快速进行，你需要访问日志文件（当然，你应该已经熟悉它们的诊断信息）。

一旦你找到了一个（我们称之为 `logfile`）具有适当的文件日期，找到开头附近类似这样的行：

```
START taper datestamp 19991110 label Daily05 tape 0
```

该行告诉你使用哪盘磁带。现在你必须弄清楚磁带上的哪个文件号是你正在寻找的，因此找到 `logfile` 中与磁带相关的部分：

```
# grep 'SUCCESS taper' logfile > /tmp/stuff
```

现在你必须找到对应于你想要恢复的机器和目录的行。为此在 `vi` 中快速操作，使用 `view /tmp/stuff`（以只读方式调用 `vi`），使用 `/dir` 命令搜索目录，并在光标位于正确行时按下 `CTRL-G`。行号会出现在编辑器底部。

一旦你找到了它，你就找到了磁带上的文件号——由于 Amanda 使用第一个文件（即 0）对磁带进行索引，文件号应与行号相同。

### 8.5 Crash Recovery

这听起来可能有点陈词滥调，但如果你遇到系统上的严重问题，不要惊慌。除了有人用大锤对你的硬盘进行“精细调整”之外，让系统重新上线只是将文件放回原位的问题。

在着手修复系统问题之前，确保你对问题是什么以及如何修复有非常清晰的认识。例如，如果你删除了 `init` 程序，你应该计划启动机器以便访问文件系统（以及 `init` 的副本）并将 `init` 放回去。但不要过度计划：更常见的是，你认为会完美奏效的方法根本行不通。

### The Rescue CD-ROM

除了包含本书其他章节引用的工具外，随附的 CD-ROM 还可以启动你的系统并提供一堆崩溃恢复工具。

### Creating a Boot Floppy

正如第 7.3 节所述，软盘驱动器和磁盘往往速度慢且不可靠，但你可以使用 `fdutils` 包中的 `superformat` 程序让它们工作得相当不错。

你也可以使用 CD 上提供的 `RAWRITE` 程序之一在 DOS 中将映像写入软盘。有两个版本（`rawrite1` 和 `rawrite2`）；有关更多详细信息，请参阅 `tools/rawrite` 目录中的 `README` 文件。

## Booting Up

引导映像支持所有处理器（但不包括数学协处理器仿真）。它还包括标准磁盘、SCSI 磁盘、磁带和 CD-ROM 支持，以及许多控制器驱动程序，包括 Adaptec `AIC7xxx` 控制器（`a9x0` 系列）和 NCR/Symbios 控制器。它不支持非 ATAPI 或非 SCSI 驱动器。

## PROBLEM 100

症状：内核找不到磁盘或 CD-ROM 驱动器。

问题：CD 上的映像不支持该设备。

修复：请参阅 Different Boot Kernels 小节。

当你从 CD-ROM 启动时，会出现一条消息：

```
Linux Problem Solver
Bootable CD
boot:
```

`boot:` 是来自 `SYSLINUX` 系统的提示；它不是 `LILO`，但与之相似。内核映像名为 `linux`，你可以像使用 `LILO` 一样向内核传递选项。

如果你只是在引导提示符下按 `ENTER`，内核将加载并运行一个来自小型引导映像的系统（这与你制作软盘时得到的映像相同）。该系统包含一个小型 `init` 和两个虚拟控制台。第一个控制台运行一个设置脚本，第二个控制台（使用通常的 `ALT-F2` 访问）启动一个 `shell`。

设置脚本会询问你是否要挂载 CD，如果可能的话会继续挂载它。引导映像包含许多小型精简版实用程序（以防你需要 CD-ROM 驱动器用于其他用途，或只是无法使用它），但 CD 包含许多程序的完整版本。

一旦开始使用它们，你会注意到 CD 和引导映像之间的其他差异。例如，引导映像上的 `shell` 是一个非常小的 `sh` 版本，不提供命令行编辑和其他功能，但 CD 包含功能齐全的 `bash`。文本编辑器也是如此。

如何尝试修复你的系统由你决定。有时你不需要做太多就能让系统恢复运行。例如，如果你的 CD-ROM 设置比较复杂，你可以在启动后使用 `ALT+F2` 跳到另一个虚拟控制台进行快速修复。但是，某些实用程序在引导映像中不可用。

## Using an Intermediate RAM Disk

如果需要在 CD-ROM 上的实用程序与另一张 CD 上的文件一起使用，你可以创建一个新的空 RAM 磁盘并将实用程序从引导 CD-ROM 复制到 RAM 磁盘。然后你可以卸载引导 CD-ROM，挂载另一张 CD，并从 RAM 磁盘运行实用程序。

有从 1MB 到 16MB 的各种预配置 RAM 磁盘。要将 5MB 的 RAM 磁盘挂载到 `/rd`，请输入以下命令：

```
# rd mount /rd 5
```

`rd mount` 程序只是 CD-ROM `bin` 目录中的一个脚本。

> ACKNOWLEDGMENT 我们基于 Debian 发行版附带的 `install/rescue` 映像制作了 CD 的软盘引导映像。我们感谢 Debian 团队在创建清晰、易于修改的映像方面的努力。

## Different Boot Kernels

如果 CD 上的内核不支持你使用的某些特殊硬件，你可以制作自己的引导映像。该映像是一个 FAT 文件系统；你只需制作一个支持你的设备的内核，然后用它替换磁盘映像上的原始内核。首先按照第 7 章所述编译一个合适的内核，包括 RAM 磁盘和 `initrd` 支持。然后像这样挂载磁盘映像：

```
# mount -t msdos boot.bin /mnt -o loop=/dev/loop0,blocksize=1024
```

接下来用你刚制作的内核替换 `/mnt`（或你挂载映像的位置）中的 `linux` 文件。你的新映像现在已准备就绪。

如果你想更改根 RAM 磁盘映像（例如向其中添加一个实用程序），包含映像的文件是 `root.bin`，这是一个用 `gzip` 压缩的 Minix 文件系统。你可以使用相同的 loop-back 设备和上面的命令行（将 `boot.bin` 替换为 `root.bin`，将 `msdos` 替换为 `minix`）来挂载根映像（确保它已解压缩）。

### 8.6 Fixing Filesystems
