

## 命令行工具

要挂载、读取、创建和写入 CD-ROM 镜像，你需要几个 Linux 实用工具：`mkisofs` 用于在你的硬盘上创建一个 ISO 镜像以容纳 CD 的内容，`mount` 用于将现有的 CD-ROM 作为 ISO 镜像挂载，`dd` 用于复制 CD 的内容，`mke2fs` 用于格式化空白的硬盘镜像文件，以及 `cdrecord` 用于将选定的文件或 ISO 镜像写入你的 CDR 或 CDWR 驱动器。请注意，在开始之前，你可能需要高达 1.4GB 的免费硬盘空间！

例如，快速复制数据 CD-ROM（如可引导的 Linux CD）的一种方法是首先使用 `dd` 命令复制 CD：

```
# dd if=/dev/scd0 of=cimage
```

然后你可以使用 `cdrecord` 命令写入该镜像，指定你的 CDR 或 CDWR 驱动器如下所示：

```
# cdrecord -v speed=2 dev=0,1,0 -data cimage
```

这将把文件 `cimage` 复制到 SCSI 驱动器上 ID 为 1（总线 0）的空白 CDR 或 CDWR 磁盘中。如果你的 CDR 或 CDWR 驱动器速度足够快，你可以使用更快的 speed= 设置。如果你下载了一个 CD-ROM 的 ISO 镜像，你可以像下面这样在本地挂载该镜像（并访问其文件和目录结构）：

```
# mount -t iso9660 -o loop=/dev/loop1 cimage /mnt/cdrom
```

此命令会将 CD-ROM 的镜像文件挂载在 `/mnt/cdrom` 目录下，就像插入了一张 CD-ROM 一样。然后你可以将文件从 `/mnt/cdrom` 复制到新目录，例如 `/mnt/cdrom_new`，以更改文件或修复任何问题。然后，你可以使用 `mkisofs` 命令并指定新的 `/mnt/cdrom_new` 目录，从新目录创建一个新的 ISO 镜像，如下所示：

```
# mkisofs -r -o new_cimage /mnt/cdrom_new
```

然后你可以写入新镜像以创建新的 CD-ROM。要写入音频 CD、混合音频曲目以创建自定义的 .mp3 文件 CD，或者直接将笔记本电脑的硬盘备份到备份 CD，你需要采取一些特殊的技巧和步骤。有关详细信息，请参阅 /usr/doc/HOWTO 目录下的 CD-Writing HOWTO（或浏览 http://www.linuxdoc.org）。

## 图形界面客户端

再次强调，就像你可以使用命令行来复制、创建和写入 CDR 和 CD-RW 磁盘一样，当你使用图形界面客户端来完成所有繁重工作时，生活会变得容易得多。Linux 中用于创建 CDR 和 CDRW 驱动器的最佳程序之一是 X-CD-Roast。你会发现这个 X11 软件包（之前讨论的实用工具的前端）包含在几乎所有现代 Linux 发行版中。

像下面这样从命令行启动客户端：

```
# xcdroast &
```

当你第一次启动该程序时，会要求你进入如图 18.16 所示的 xcdroast 设置对话框。

点击 xcdroast 的 Setup 选项卡以指定你的 CD-Writer 和 CD-Reader 设备。在拥有两个 CD-ROM（内置和外部）的笔记本上使用此客户端时效率更高。你还需要指定临时硬盘空间和镜像挂载点。如果你想验证音频曲目，请确保 Linux 已配置为与你的笔记本声音系统协同工作。

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_434_0.png)

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_435_0.png)

图 18.17 验证数据 CD 的信息，然后点击 Read Image 按钮复制 CD。

当你完成设置后，点击 Save 按钮，然后点击 Done 按钮。然后你将返回到 xcdroast 主窗口。

要复制数据 CD，将 CD 插入驱动器，然后点击 xcdroast 主窗口中的 Copy Data CD 按钮。你将看到如图 18.17 所示的对话框。

点击 Read Image 按钮以复制 CD。其内容将根据你在设置 xcdroast 时指定的默认路径保存。接下来，点击如图 18.18 所示的 Start Read Image 按钮。

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_435_1.png)

图 18.18 点击 Start Read Image 按钮开始复制你的 CD。

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_436_0.png)

图 18.19 xcdroast 客户端将读取你的 CD 内容并在你的硬盘上创建一个镜像文件。

CD 的内容（在此示例中，由于 CD 是一张“名片”CD，所以为 31MB）将被读取并保存。根据 CD 上的数据量，此过程可能需要相当长的时间。读取完成后，点击 OK 按钮继续，如图 18.19 所示。

在主对话框中，然后你可以点击 Verify Image 按钮。xcdroast 客户端将比较已复制 CD 的内容与保存在你硬盘上的镜像文件。当你满意后，取出原始 CD，然后插入一张空白的 CDR 或 CD RW 磁盘。接下来，点击 Write Image 按钮开始将镜像复制到你的新 CD。和以前一样，你将看到一个包含 CD 信息的对话框，但这次，按钮的名称不是 Start Read Image（如图 18.18 所示），而是 Start Write Image，如图 18.20 所示。

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_436_1.png)

图 18.20 点击 Start Write Image 按钮写入你的新 CD。

注意，系统还会提示你插入空白 CD。点击按钮开始写入你的 CD。注意，此过程可能比将 CD 镜像读取到你的硬盘上花的时间还要长！市场上没有 CD 写入驱动器的写入速度比读取速度快。

xcdroast 客户端还有许多其他功能，可用于直接从一个 CD 复制数据到另一个 CD。另一个很棒的功能是通过收集指定目录中的数据，然后将其写入 CD-ROM 来“母版”一个 CD。这是将近 10 张音频音乐 CD（.mp3 文件）复制到一张 CD-ROM 上的绝佳方式！务必阅读 xcdroast 的手册和文档，以充分利用你的刻录会话。

## 资源信息

- [http://promo.net/pg/](http://promo.net/pg/)
  Project Gutenberg 的主页，在那里可以下载数千本免费书籍。
- [ftp://metalab.unc.edu/pub/Linux/games/](ftp://metalab.unc.edu/pub/Linux/games/)
  原始纯文本 BSD 游戏的来源。
- [ftp://metalab.unc.edu/pub/Linux/games/strategy](ftp://metalab.unc.edu/pub/Linux/games/strategy)
  LinCity 模拟游戏的来源。
- [http://linuxberg.ozbytes.net.au/x11soft.html](http://linuxberg.ozbytes.net.au/x11soft.html)
  Linux 软件的综合索引，包括街机游戏。
- [http://www.torque.net/linux-pp.html](http://www.torque.net/linux-pp.html)
  Linux 并行端口主页。它有许多链接指向文档和软件，帮助你使用 Linux 操作并行端口设备，包括对 ATAPI CDR 和 CDWR 驱动器的支持。
- [http://www.gnug.de/wnini/cdr/html/](http://www.gnug.de/wnini/cdr/html/)
  Winfried Trumper 的 CD-Writing HOWTO。它是关于使用 Linux 将音频曲目和数据复制、整理和复制到 CDR 或 CDWR 磁盘的技巧和窍门汇编。
- [http://www.linuxdoc.org/HOWTO/Sound-HOWTO.html](http://www.linuxdoc.org/HOWTO/Sound-HOWTO.html)
  指向 Jeff Tranter 的全面 Sound-HOWTO 的链接。

### SUPPORTED.CARDS

David Hinds 列出的当前支持用于 Linux 的 PC 卡列表。可以在 `/usr/doc/pcmcia*` 或 `/usr/src/pcmcia*` 目录下找到。也可以在 `http://pcmcia.sourceforge.org/` 找到。

- [http://www.fokus.gmd.de/research/cc/glone/employees/joerg.schilling/private/cdrecord.html](http://www.fokus.gmd.de/research/cc/glone/employees/joerg.schilling/private/cdrecord.html)
  cdrecord 实用工具的主页。
- [http://krabber.automatix.de/](http://krabber.automatix.de/)
  krabber 客户端主页。它是最好的 X11 KDE 客户端之一，用于从音频 CD 中抓取 .mp3 文件。
- [http://www.fh-muenchen.de/home/ze/rz/services/projects/xcdroast/xcdr098/](http://www.fh-muenchen.de/home/ze/rz/services/projects/xcdroast/xcdr098/)
  Thomas Niederreiter 关于 X11 和 Linux 的 xcdroast 客户端的主页。你也可以在 http://www.fh-muenchen.de/rz/xcdroast/ 找到该软件。

