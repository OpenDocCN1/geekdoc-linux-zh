

Linux 设备驱动程序驻留在内核中，并期望内核提供某些服务。其中一些服务由 Linux 内核代码直接提供，例如中断处理，而其他一些服务则由类似内核的运行时提供。

Milo 最强大的特性是你可以将未经修改的 Linux 设备驱动程序嵌入其中。这使其具备支持所有 Linux 支持的设备的可能性。Milo 包含针对其构建所依赖的 Linux 内核中配置的所有块设备，以及大量的块设备代码（例如，`ll_rw_blk()`）。

Milo 从真实的文件系统加载 Linux 内核，而不是从引导块或其他奇怪的地方加载。它支持 MSDOS、EXT2 和 ISO9660 文件系统。支持 Gzip 压缩文件，并建议使用这些文件，特别是当从相当缓慢的软盘加载时。Milo 通过其 `.gz` 后缀来识别这些文件。

Milo 内置了一个简单的键盘驱动程序，该驱动程序与同样简单的视频驱动程序一起，使其拥有一个简单的用户界面。该界面允许你列出已配置设备上的文件系统、引导 Linux 或运行闪存更新实用程序，并设置控制系统引导的环境变量。与 LILO 类似，你可以向内核传递参数。

Milo 必须告知 Linux 内核这是什么类型的系统、有多少内存以及这些内存中哪些是空闲的。它使用 HWRPB（Hardware Restart Parameter Block，硬件重启参数块）数据结构及相关内存簇描述来实现这一点。这些数据在将控制权移交给 Linux 内核之前，被放置在虚拟内存中的适当位置。

## E.3 预构建的标准 Milo 镜像

如果你计划在基于标准 Alpha 的系统上运行 Linux，那么有一些预构建的“标准”Milo 镜像可供你使用。这些镜像（连同源代码和其他有趣的内容）可以在 [ftp://gatekeeper.dec.com/pub/Digital/Linux-Alpha/MiniLoader](ftp://gatekeeper.dec.com/pub/Digital/Linux-Alpha/MiniLoader) 找到。

`images` 子目录包含每个标准系统（例如 AlphaPC64）的一个目录，其中的 Milo 镜像遵循以下命名约定：

- 1. `milo` - 迷你加载器可执行镜像，此镜像可以通过多种方式加载，
- 2. `fmu.gz` - 闪存管理实用程序，
- 3. `milo.dd` - 引导块软盘镜像。应使用 `rawrite.exe` 或 Linux 上的 `dd` 来写入这些镜像。

`test-images` 目录，就像 `images` 子目录一样，包含每个标准系统的一个目录。这些镜像具有一定的实验性质，但通常包含所有最新特性。

## E.4 如何构建 Milo

你单独构建 Milo，而不是将其与内核一起构建。由于 Milo 需要内核的部分功能才能工作（例如中断处理），你必须首先配置并构建与你要构建的 Milo 相匹配的内核。通常这意味着使用相同版本号构建内核。因此，`milo-1.3.76.tgz` 将针对 `linux-1.3.76.tar.gz` 进行构建。Milo 可能针对更高版本的内核进行构建，但也可能不行。在剩余的讨论中，我假设你的内核源代码和对象文件存储在 `/usr/src/linux` 子树中。

要构建 Milo，请将工作目录更改为 Milo 源目录，并调用 make：

```
make KSrc=/usr/src/linux config
```

与 Linux 内核一样，你会被询问一系列问题

回显到串行端口的输出 (MINI_SERIAL_ECHO) [y]

如果可能，最好将内核 printk 回显到 `/dev/ttyS0`。如果你能（并且想要），则输入 "y"，否则输入 "n"。

使用 Digital 的 BIOS 模拟代码（非免费）(MINI_DIGITAL_BIOS_EMU) [y]

此代码作为库包含在内，只要用于基于 Alpha 的系统就可以自由分发。源代码不可用。如果你回答 "n"，则构建免费软件的替代 BIOS 模拟。其源代码与 Milo 一起提供。

## E.5 如何加载 Milo

加载 Milo 最普遍支持的方法是通过 Windows NT ARC 固件，因为大多数出货系统都支持这一点。然而，加载 Milo 的方式多种多样。它可以从中加载：

- 应急引导块软盘，
- Windows NT ARC 固件，
- Digital 的 SRM 控制台，
- Alpha 评估板调试监视器，
- 闪存/ROM。

### E.5.1 从 Windows NT ARC 固件加载 Milo

如果并非全部，那么大多数基于 Alpha AXP 的系统都包含 Windows NT ARC 固件，这是引导 Milo 进而引导 Linux 的首选方法。一旦 Windows NT 固件正在运行，并且你拥有适合你系统的正确 Milo 镜像，这种方法就完全是通用的。

Windows NT ARC 固件是一个程序可以运行并回调固件以执行操作的环境。Windows NT OSLoader 是一个完全这样做的程序。`Linload.exe` 是一个简单得多的程序，它仅仅做了加载和执行 Milo 所需的工作。它将适当的映像文件加载到内存的 0x00000000，然后对其进行 swap-PAL PALCall。Milo 与 Linux 一样，使用与 Windows NT 不同的 PALCode，这就是为什么必须发生交换的原因。Milo 将自己重定位到 0x200000，并像以前一样通过 PALCode 重置入口点继续。

在添加 Linux 引导选项之前，你需要将 `linload.exe` 和你希望加载的适当 Milo 复制到 Windows NT ARC 固件可以读取的某个位置。在以下示例中，假设你正在从 DOS 格式软盘启动：

- 1. 在引导菜单中，选择 Supplementary menu...
- 2. 在 Supplementary menu 中，选择 Set up the system...
- 3. 在 Setup menu 中，选择 Manage boot selection menu...
- 4. 在 Boot selections menu 中，选择 Add a boot selection
- 5. 选择 Floppy Disk 0
- 6. 输入 `\nlinload.exe` 作为 osloader 目录和名称
- 7. 回答 "yes" 表示操作系统与 osloader 位于同一分区
- 8. 输入 "/" 作为操作系统根目录
- 9. 我通常输入 "Linux" 作为此引导选择的名称
- 10. 回答 "No" 表示你不想在启动时初始化调试器
- 11. 此时你应该回到了 Boot selections menu，选择 Change a boot selection 选项并选择你刚创建的那个作为编辑对象
- 12. 使用向下箭头 ↓ 显示 OSLOADFILENAME，然后输入你想使用的 Milo 镜像名称，例如 `noname.arc` 并按 Return
- 13. 按 Esc 返回 Boot Selections menu
- 14. 选择 Setup Menu（或再次按 Esc）并选择 Supplementary menu，以及 save changes 选项
- 15. 按 Esc 回到 Boot menu，你可以尝试引导 Milo。如果你不想要 Linux 作为第一个引导选项，你可以更改 Boot selections menu 中引导选项的顺序。

完成所有这些步骤后，你应该拥有一个看起来像这样的引导选择：

```
LOADIDENTIFIER=Linux
SYSEMPARTITION=muli(0)disk(0)fdisk(0)
OSLOADER=muli(0)disk(0)fdisk(0)\nlinload.exe
OSLOADPARTITION=muli(0)disk(0)fdisk(0)
OSLOADFILENAME=\noname.arc
OSLOADOPTIONS=
```

现在你可以引导 Milo（然后是 Linux）。你可以直接从 Windows NT 理解的文件系统（如硬盘上的 NTFS 或 DOS）加载 `linload.exe` 和 Milo。**OSLOADOPTIONS** 的内容会传递给 Milo，Milo 将其解释为命令。因此，为了直接从 Windows NT 引导 Linux 而在 Milo 中不停留，你可以在 **OSLOADOPTIONS** 中传递以下内容：

```
boot sda2:vmlinux.gz root=/dev/sda2
```

有关可用命令的更多信息，请参阅第 E.6 节 *Milo 的用户界面*。

通过 WNT ARC 固件加载 Milo 的另一种（相当巧妙的）方法是将 Milo 放在 MS-DOS 软盘上并命名为 *fwupdate.exe*，然后选择“Upgrade Firmware”选项。

### E.5.2 从评估板调试监视器加载 Milo

评估板（以及经常从其克隆的设计）包含对 Alpha 评估板调试监视器的支持。在考虑使用此方法引导 Milo 之前，请查阅你的系统文档。以下系统 *已知* 包含调试监视器支持：

- AlphaPC64（第 E.5.6 节）
- EB64+（第 E.5.6 节）
- EB66+（第 E.5.6 节）
- EB164（第 E.5.6 节）

在考虑使用此方法之前，你应该注意到早期版本的评估板调试监视器不包含视频或键盘驱动程序，因此你必须准备好通过串行端口连接另一个系统，以便你可以使用调试监视器。它的接口非常简单，输入 `help` 会显示大量命令。其中最有意思的包括 *boot* 或 *load* 字样。

