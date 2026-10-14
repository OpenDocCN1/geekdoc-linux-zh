
drives, we can manage those devices, too. Preparing a blank floppy for use is a two step process. First, we perform a low-level format on the diskette, and then create a file system. To accomplish the formatting, we use the fdformat program specifying the name of the floppy device (usually /dev/fd0):

```
[me@linuxbox ~]$ sudo fdformat /dev/fd0
Double-sided, 80 tracks, 18 sec/track. Total capacity 1440 kB.
Formatting ... done
Verifying ... done
```

Next, we apply a FAT file system to the diskette with mkfs:

```
[me@linuxbox ~]$ sudo mkfs -t msdos /dev/fd0
```

Notice that we use the "msdos" file system type to get the older (and smaller) style file allocation tables. After a diskette is prepared, it may be mounted like other devices.

## 直接向设备传输数据/从设备传输数据

虽然我们通常认为计算机上的数据是以文件的形式组织的，但也可以将数据视为“原始”形式。例如，如果我们查看磁盘驱动器，就会发现它由操作系统视为目录和文件的大量“块”数据组成。然而，如果我们将磁盘驱动器视为简单的大量数据块集合，就可以执行有用的任务，例如克隆设备。

dd 程序执行此任务。它从一个地方复制数据块到另一个地方。它使用独特的语法（出于历史原因），通常这样使用：

```
dd if=input_file of=output_file [bs=block_size [count=blocks]]
```

假设我们有两只相同大小的 USB 闪存驱动器，并且想将第一个驱动器完全复制到第二个驱动器。如果我们将两只驱动器都连接到计算机，并且它们分别分配为设备 /dev/sdb 和 /dev/sdc，我们可以用以下命令将第一个驱动器上的所有内容复制到第二个驱动器：

```
dd if=/dev/sdb of=/dev/sdc
```

或者，如果只有第一个设备连接到计算机，我们可以将它的内容复制到普通文件中以便以后恢复或复制：

```
dd if=/dev/sdb of=flash_drive.img
```

**Warning!** The dd command is very powerful. Though its name derives from “data definition,” it is sometimes called “destroy disk” because users often mistype either the if or of specifications. **Always double check your input and output specifications before pressing enter!**

## 创建 CD-ROM 映像

刻录可记录 CD-ROM（CD-R 或 CD-RW）包括两个步骤；首先，构建一个 iso 映像文件，该文件是 CD-ROM 的精确文件系统映像，其次，将映像文件写入 CD-ROM 介质。

### 创建 CD-ROM 的映像拷贝

如果我们想制作现有 CD-ROM 的 iso 映像，可以使用 dd 读取 CD-ROM 上的所有数据块并将其复制到本地文件。假设我们有一张 Ubuntu CD，并且想制作一个 iso 文件以便以后制作更多拷贝。在插入 CD 并确定其设备名称（我们假设为 /dev/cdrom）后，我们可以像这样制作 iso 文件：

```
dd if=/dev/cdrom of=ubuntu.iso
```

此技术也适用于数据 DVD，但不适用于音频 CD，因为音频 CD 不使用文件系统进行存储。对于音频 CD，请查看 cdrdao 命令。

### 从一组文件创建映像

要创建包含目录内容的 iso 映像文件，我们使用 genisoimage 程序。为此，我们首先创建一个包含希望包含在映像中的所有文件的目录，然后执行 genisoimage 命令来创建映像文件。例如，如果我们创建了一个名为 ~/cd-rom-files 的目录并在其中填充了 CD-ROM 的文件，我们可以用以下命令创建名为 cd-rom.iso 的映像文件：

```
genisoimage -o cd-rom.iso -R -J ~/cd-rom-files
```

“-R” 选项会添加 Rock Ridge 扩展的元数据，这允许使用长文件名和 POSIX 风格的文件权限。同样，“-J” 选项启用 Joliet 扩展，这允许 Windows 使用长文件名。

### 换个名字也是程序...

如果你查看有关创建和刻录光学介质（如 CD-ROM 和 DVD）的在线教程，你会经常遇到两个程序 mkisofs 和 cdrecord。这些程序是 Jörg Schilling 编写的名为 “cdrtools” 的流行软件包的一部分。2006 年夏季，Schilling 先生对 cdrtools 软件包的一部分进行了许可变更，在许多 Linux 社区人士看来，这与 GNU GPL 存在许可不兼容。因此，cdrtools 项目的一个分支被启动，现在其中包含 cdrecord 和 mkisofs 的替代程序，分别命名为 wodim 和 genisoimage。

## 写入 CD-ROM 映像

在我们有了映像文件后，就可以将其刻录到光学介质上。我们下面讨论的大多数命令都可应用于可记录 CD-ROM 和 DVD 介质。

### 直接挂载 ISO 映像

我们可以使用一个技巧在 iso 映像仍在硬盘上时将其挂载，并将其视为已在光学介质上。通过向 mount 添加 “-o loop” 选项（以及所需的 “-t iso9660” 文件系统类型），我们可以将映像文件作为设备挂载并将其附加到文件系统树中：

```
mkdir /mnt/iso_image
mount -t iso9660 -o loop image.iso /mnt/iso_image
```

在上面的示例中，我们创建了一个名为 /mnt/iso_image 的挂载点，然后将映像文件 image.iso 挂载到该挂载点。映像挂载后，可以像真实的 CD-ROM 或 DVD 一样对待。记住在不再需要时卸载映像。

