

正如第 7.3 节所述，软盘驱动器和磁盘往往速度慢且不可靠，但你可以使用 fdutils 包中的 superformat 程序让它们工作得相当不错。

你也可以使用 CD 上提供的 RAWRITE 程序之一在 DOS 中将映像写入软盘。有两个版本（rawrite1 和 rawrite2）；有关更多详细信息，请参阅 tools/rawrite 目录中的 README 文件。

## Booting Up

引导映像支持所有处理器（但不包括数学协处理器仿真）。它还包括标准磁盘、SCSI 磁盘、磁带和 CD-ROM 支持，以及许多控制器驱动程序，包括 Adaptec AIC7xxx 控制器（a9x0 系列）和 NCR/Symbios 控制器。它不支持非 ATAPI 或非 SCSI 驱动器。

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

boot: 是来自 SYSLINUX 系统的提示；它不是 LILO，但与之相似。内核映像名为 linux，你可以像使用 LILO 一样向内核传递选项。

如果你只是在引导提示符下按 ENTER，内核将加载并运行一个来自小型引导映像的系统（这与你制作软盘时得到的映像相同）。该系统包含一个小型 init 和两个虚拟控制台。第一个控制台运行一个设置脚本，第二个控制台（使用通常的 ALT-F2 访问）启动一个 shell。

设置脚本会询问你是否要挂载 CD，如果可能的话会继续挂载它。引导映像包含许多小型精简版实用程序（以防你需要 CD-ROM 驱动器用于其他用途，或只是无法使用它），但 CD 包含许多程序的完整版本。

一旦开始使用它们，你会注意到 CD 和引导映像之间的其他差异。例如，引导映像上的 shell 是一个非常小的 sh 版本，不提供命令行编辑和其他功能，但 CD 包含功能齐全的 bash。文本编辑器也是如此。

如何尝试修复你的系统由你决定。有时你不需要做太多就能让系统恢复运行。例如，如果你的 CD-ROM 设置比较复杂，你可以在启动后使用 ALT+F2 跳到另一个虚拟控制台进行快速修复。但是，某些实用程序在引导映像中不可用。

## Using an Intermediate RAM Disk

如果需要在 CD-ROM 上的实用程序与另一张 CD 上的文件一起使用，你可以创建一个新的空 RAM 磁盘并将实用程序从引导 CD-ROM 复制到 RAM 磁盘。然后你可以卸载引导 CD-ROM，挂载另一张 CD，并从 RAM 磁盘运行实用程序。

有从 1MB 到 16MB 的各种预配置 RAM 磁盘。要将 5MB 的 RAM 磁盘挂载到 /rd，请输入以下命令：

```
# rd mount /rd 5
```

rd mount 程序只是 CD-ROM bin 目录中的一个脚本。

> ACKNOWLEDGMENT 我们基于 Debian 发行版附带的 install/rescue 映像制作了 CD 的软盘引导映像。我们感谢 Debian 团队在创建清晰、易于修改的映像方面的努力。

## Different Boot Kernels

如果 CD 上的内核不支持你使用的某些特殊硬件，你可以制作自己的引导映像。该映像是一个 FAT 文件系统；你只需制作一个支持你的设备的内核，然后用它替换磁盘映像上的原始内核。首先按照第 7 章所述编译一个合适的内核，包括 RAM 磁盘和 initrd 支持。然后像这样挂载磁盘映像：

```
# mount -t msdos boot.bin /mnt -o loop=/dev/loop0,blocksize=1024
```

接下来用你刚制作的内核替换 /mnt（或你挂载映像的位置）中的 linux 文件。你的新映像现在已准备就绪。

如果你想更改根 RAM 磁盘映像（例如向其中添加一个实用程序），包含映像的文件是 root.bin，这是一个用 gzip 压缩的 Minix 文件系统。你可以使用相同的 loop-back 设备和上面的命令行（将 boot.bin 替换为 root.bin，将 msdos 替换为 minix）来挂载根映像（确保它已解压缩）。

## 8.6 Fixing Filesystems

修复损坏文件系统的基石是 fsck 程序。它会遍历整个文件系统结构，找到错误，并在你希望的情况下修复它们。它通常在启动时运行；由于文件系统错误可能导致非常严重的问题，Unix 系统会格外确保文件系统的稳定性。

fsck 本身是一个包装程序，它会调用适用于该文件系统的 fsck。例如，Minix 文件系统的 fsck 将无法在第二扩展文件系统上工作。真正的 fsck 程序通常位于 /sbin 中，并命名为 fsck.fs，其中 fs 是目标文件系统；大多数系统上的两个标准 fsck 是 fsck.ext2（通常只是 e2fsck 的硬链接）和 fsck.minix。

## Operating fsck Manually

有时你必须手动运行 fsck——不要因此感到惊慌。只需运行以下命令（例如，如果你需要检查的分区是 /dev/hda1）：

```
# fsck /dev/hda1
```

fsck 检查 /dev/hda1 是否有错误，如果发现错误，会询问你是否要修复它们。它按错误逐个进行询问，如果磁盘问题很多，这可能会非常繁琐。使用 fsck -p 可强制对问题回答 yes。

如果有 /etc/fstab 可用，你可以让 fsck 查找设备。在此示例中，fsck 查找 /home 设备：

```
# fsck /home
```

当没有 /etc/fstab 可用，并且你记不起所需文件系统的设备名称时，使用 fdisk -l 列出磁盘的当前分区表（连同设备名称）。

> NOTE 除非文件系统以只读方式挂载，否则不要在当前已挂载的文件系统上运行 fsck。

