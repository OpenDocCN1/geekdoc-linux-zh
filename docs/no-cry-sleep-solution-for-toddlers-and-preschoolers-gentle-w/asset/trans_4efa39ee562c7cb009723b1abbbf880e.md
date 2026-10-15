

mkfs 命令的语法如下。你可以在类型之后、设备之前为特定文件系统添加选项。块大小用于不检测磁盘大小的文件构建器。

```
mkfs options [-t type] file-system options device size
```

> 提示 格式化磁盘后，你可以使用本章前面描述的 e2label 命令为其命名。

同样的流程也适用于软盘。在这种情况下，mkfs 命令的参数是设备名。它使用 ext2 文件系统（mkfs 的默认值），因为软盘太小，无法支持日志文件系统。

```
# mkfs /dev/fd0
```

> 提示 在桌面上，你可以使用“系统工具”菜单中列出的软盘格式化工具来格式化软盘。格式化工具使你能够选择 MS-DOS 或 Linux 文件系统类型。

## mkswap

如果你想创建交换分区，首先使用 fdisk 或 parted 创建分区（如果尚未存在），然后使用 mkswap 命令将其格式化为交换分区。mkswap 会格式化整个分区，除非另有指示。它以交换分区的设备名为参数。

```
mkswap /dev/hdb2
```

然后你需要在 /etc/fstab 文件中为其创建一个条目，以便系统启动时自动挂载。

## CD-ROM 和 DVD ROM 刻录

在 Linux 上向 CD-ROM 光盘刻录数据涉及创建 CD-ROM 的 CD 映像文件，然后将该映像文件写入 CD-R 或 CD-RW 光盘驱动器中的光盘。使用 mkisofs 命令，你可以创建 CD 映像文件，然后将其写入 CD-R/RW 写入设备。创建 CD 映像文件后，你可以使用 cdrecord 或 cdwrite 应用程序将其写入 CD 写入设备。cdrecord 应用程序是一个功能更强大的应用程序，具有许多选项。你也可以使用 GNOME 和 KDE 刻录应用程序（如 K3b 和 GNOME Toaster）轻松创建 CD。大多数都是 mkisofs 和 cdrecord 工具的前端。要在 DVD 刻录机上刻录 DVD 光盘，可以使用 dvdrrecord（cdrecord 的对应工具）用于 DVD-R/RW 驱动器，以及 dvd+rw 工具用于 DVD+R/R 驱动器。如果你想在 DVD 刻录机上刻录 CD-ROM，只需使用 cdrecord 即可。

dvdrtools 应用程序目前仅在 DVD-R/RW 驱动器上工作；它是 dvdrtools 软件包的一部分。如果你想使用 DVD+RW/R 驱动器，你将使用 dvd+rw 工具，如 growisofs 和 dvd+rw-format。dvd+rw 工具在 Red Hat 中包含在 dvd+rw-tools 软件包中。查看 DVD+R/W 工具网站了解更多信息，http://fy.chalmers.se/~appro/linux/DVD+RW。

## mkisofs

要创建 CD 映像，首先选择要放在 CD 上的文件。然后你可以使用 mkisofs 创建它们的 ISO CD 映像。

### mkisofs 选项

你可能需要使用 mkisofs 包含几个重要选项才能正确创建数据 CD。-o 选项用于指定 CD 映像文件的名称。这可以是你想要的任何名称。-R 选项指定 RockRidge CD 协议，-J 选项提供长 Windows 95/98/ME 或 XP 名称。-r 选项除了 RockRidge 协议（-R）之外，还为你的文件设置标准全局权限，例如所有用户可读且无写权限，因为 CD-ROM 是只读的。-T 选项为在非 RockRidge 兼容系统上使用的文件名创建转换表。

-U 选项提供非标准 ISO 兼容的宽松文件名，例如长文件名、名称中包含多个句点的文件名、以句点开头的文件名（如 shell 配置文件），以及使用小写字符的文件名（也有针对这些功能的单独选项，如果你只想使用其中几个）。大多数 RPM 和源代码包名称都属于此类。-iso-level 选项可让你删除 ISO 限制，例如文件名的长度。-V 选项设置 CD 的卷标（名称）。最后，-v 选项显示映像创建的进度。

### 磁盘映像创建

最后一个参数是包含要制作 CD 映像的文件的目录。对于此，你可以指定一个目录。例如，如果你要创建包含 mydocs 目录中数据文件的 CD-ROM，你将指定该目录。此顶级目录不会包含在内，只包含其中的文件和子目录。你也可以更改到该目录，然后使用 . 表示当前目录。

如果你要创建可在 Linux 上使用的简单 CD，你将使用 mkisofs 首先创建 CD 映像。这里详细选项将显示创建进度，-V 选项可让你指定 CD 标签。名为 songs.iso 的 CD 映像使用位于 newsong 目录中的文件创建：

```
mkisofs -v -V "Goodsongs" -o moresongs.iso newsongs
```

如果你还想在 Windows 系统上使用该 CD，你将添加 -r（RockRidge 与标准全局文件访问）和 -J（Joliet）选项：

```
mkisofs -v -r -J -V "Goodsongs" -o moresongs.iso newsongs
```

如果你使用的是不符合 ISO 规范的文件名，例如字符数超过 31 个或使用小写字符的文件名，则需要包含某些选项。-U 选项可让你使用完全不受限制的文件名，而某些选项如 -L 用于不受限制的长度，只会解除特定限制。以下示例使用位于 mdoc 目录中的文件和子目录创建名为 mydoc.iso 的 CD 映像，并将 CD 映像命名为“doc”：

```
mkisofs -v -r -T -J -U -V "Greatdocs" -o mydocuments.iso mydocs
```
