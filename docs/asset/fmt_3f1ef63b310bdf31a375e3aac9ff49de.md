
```
Mount: block device /dev/hdb is write-protected, mounting in read-only
```

CD-ROM 挂载后，你可以使用第 7 小时“在文件系统中移动”中介绍的命令读取目录列表和查看文件。

## Working with DOS Floppies

如果所有这些挂载和卸载的操作让你感到困惑，还有另一种使用软盘的方法。在发行版中，你会找到一个名为 `mtools` 的软件包。`mtools` 软件包包含一组命令，使你能够以与在 DOS（或 Microsoft Windows）系统上使用软盘相同的方式处理软盘上的目录和文件。此外，你不必使用 Linux 文件系统（位于 `/mnt/floppy` 或 `/dev/fd0`）来访问软盘。你可以使用旧的、熟悉的 `A:` designation 来表示软盘驱动器。使用 `mtools` 时，使用软盘前无需先挂载它。以下列表包含一些你会觉得有用的 `mtools` 命令。

- 列出软盘的内容，使用 `mdir` 命令。
- 将文件从软盘复制到 GNU/Linux 系统或从 GNU/Linux 系统复制到软盘，使用 `mcopy` 命令。
- 删除软盘上的文件，使用 `mdel` 命令。
- 重命名软盘上的文件，使用 `mren` 命令。
- 更改文件的属性，使用 `mattrib` 命令。使用此命令，你可以使文件变为只读。
- 格式化软盘，使用 `mformat` 命令。
- 检查软盘上的坏块（错误），使用 `mbadblocks` 命令。
- 在软盘上创建描述软盘内容的标签，使用 `mlabel` 命令。

## Formatting a Floppy Disk

当你购买软盘时，它们通常已预先格式化。这些磁盘可以直接在你的 GNU/Linux 系统上使用。当你想彻底擦除软盘时，你可能希望重新格式化软盘，以便销毁软盘上存储的所有信息，使软盘看起来像全新的。以下是如何使用 `mtools` 命令格式化和处理软盘的方法：

1. 将软盘放入软盘驱动器中。
2. 格式化软盘。输入 `mformat a:` 并按 Enter。如果看到以下错误消息

`mformat: Non-removable media is not supported`

`(You must tell the complete geometry of the disk, either in /etc/mtools or on the command line)`

你需要输入

`mformat -s 18 -h 2 -t 80 a:`

并按 Enter。此命令（用于格式化 1.44MB 软盘）告诉 `mformat` 命令磁盘上有 18 个扇区、2 个磁头和 80 条磁道。你可以在 `/etc/fdprm` 文件中找到此信息。你可以使用 `cat` 命令或 `less` 分页器读取此文件。
3. 为软盘贴标签。输入 `mlabel a: 'description'` 并按 Enter。其中 *description* 是你希望作为标签显示的文本。例如，要将软盘命名为 Testing，输入 `mlabel a: 'Testing'` 并按 Enter。
4. 查看软盘的内容。输入 `mdir a:` 并按 Enter。你会看到以下内容：

```
[rusty@localhost rusty]$ mdir a:
Volume in drive A is Testing (a: = TESTING)
Volume Serial Number is 1EC7-50FF
Directory for A:/

No files

1,457,664 bytes free
```

在此示例中，步骤 3 中的标签为 TESTING（显示在“Volume in drive A is Testing”这一行）。磁盘上没有文件，所有 1.44MB 都是空闲的。
5. 将文件复制到软盘。切换到包含要复制的文件的目录。要复制文件，输入 `mcopy filename a:` 并按 Enter。要查看文件是否已复制到软盘，输入 `mdir a:` 并按 Enter。
6. 将文件从软盘复制到 GNU/Linux 系统。切换到要存储文件的目录。输入 `mcopy a:filename` 并按 Enter。

## Locating Hardware Information

作为你的 GNU/Linux 系统的系统管理员（可能是你）的一项重要工作是维护系统的配置，以充分利用操作系统的灵活性和强大功能。通过了解各种配置文件为你的系统配置了哪些内容，你可以跟踪系统性能并重新配置系统以实现最佳运行。你将通过编辑控制系统行为的配置文件来实现这种性能微调。然而，在真正掌握这一点之前，你需要收集尽可能多的关于系统的信息。

### Task: Gathering Important System Information

你还记得登录提示出现之前屏幕上滚动显示的那些消息吗？它们是内核启动消息，已存储在 `/var/log/messages` 文件中。显示的消息取决于驱动程序配置在系统上。其他文件位于 `/proc` 文件系统，包含有关系统架构的信息；也就是说，连接到系统的所有总线、板卡、控制器和外设。在对系统进行任何配置更改之前，了解这些信息非常重要。以下是如何在 `vi` 文本编辑器中将这些文件作为只读文件查看的方法：

1. 以超级用户身份登录。输入 `su` 并按 Enter。系统会提示您输入 root 密码。输入密码并按 Enter。
2. 以只读方式打开内核启动消息文件。输入 `vi -R /var/log/messages` 并按 Enter。内核启动消息因系统而异，具体取决于作为模块编译或加载到内核中的驱动程序。在浏览文件时，您会注意到在启动过程中每个设备初始化时都会出现相应的消息。
3. 查找系统配置信息。您需要了解屏幕在用作文本终端时的字体和颜色、PCI 总线和 PCI 卡、CPU 类型和处理器速度、系统内存使用情况、鼠标类型、串行和 USB 端口、已挂载的文件系统，以及 Linux 内核的版本号。
4. 在文件中移动。按 `Ctrl+F` 向前移动一屏文件。按 `Ctrl+B` 向后移动一屏。
5. 读完文件后，退出（或 quit）文本编辑器。输入 `:q` 并按 Enter。`vi` 文本编辑器将关闭，您将被返回到 shell 提示符。
6. 返回到您的用户账户。输入 `su username` 并按 Enter。
7. 查看有关 CPU 类型和速度的信息。输入 `vi -R /proc/cpuinfo` 并按 Enter。`-R` 命令选项告诉 `vi` 以只读方式打开文件。`/proc/cpuinfo` 文件的示例显示在列表 9.3 中。读完文件后，输入 `:q` 并按 Enter 关闭文件并退出 `vi`。

### LISTING 9.3 /proc/cpuinfo 文件的内容

```
processor : 0
vendor_id : GenuineIntel
cpu family : 5
model : 2
model name : Pentium 75 - 200
stepping : 12
cpu MHz : 132.770406
fdiv_bug : no
hlt_bug : no
sep_bug : no
f00f_bug : yes
```

### LISTING 9.3 继续

```
coma_bug : no
fpu : yes
fpu_exception : yes
cpuid level : 1
wp : yes
flags : fpu vme de pse tsc msr mce cx8
bogomips : 264.60
```

8. 显示总系统 RAM、已用内存、空闲内存和交换空间。输入 `vi -R /proc/meminfo` 并按 Enter。完成后输入 `:q` 并按 Enter。
9. 列出启动时挂载的文件系统。输入 `vi -R /proc/mounts` 并按 Enter。不要关闭 `vi`。
10. 查看系统上安装的 PCI 设备信息。输入 `:e /proc/pci` 并按 Enter。`:e` 命令告诉 `vi` 您想要处理另一个文件。完成后输入 `:q` 并按 Enter。
11. 列出占用的 I/O 地址、IRQ 和 DMA 通道。输入 `vi -R /proc/ioports /proc/interrupts /proc/dma` 并按 Enter。您可以通过列出以空格分隔的文件名，一次在 `vi` 中打开多个文件。一次只能显示一个文件。
12. 读取 `/proc/ioports` 文件，完成后显示 `/proc/interrupts` 文件。输入 `:next` 并按 Enter。使用 `:next` 命令在文件列表中向前移动；使用 `:prev` 命令在文件列表中向后移动。
13. 读取最后一个文件，完成后退出 `vi`。

## 添加新硬件

在安装过程中，您为硬盘上的分区创建了不同的文件系统和相应的挂载点。如果您认为存储空间不足，可以考虑向系统添加第二个硬盘。以下是向系统添加磁盘所需的步骤：
