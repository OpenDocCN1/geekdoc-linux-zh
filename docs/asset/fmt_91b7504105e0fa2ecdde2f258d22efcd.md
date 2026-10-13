
- `single`——与 `rescue` 类似，但尝试从硬盘启动。
- `root=<device>`——类似于 `/etc/lilo.conf` 条目，此选项允许您从 CD-ROM 或其他存储设备启动。
- `vga=<mode>`——允许您更改控制台的分辨率；请尝试 `ask` 模式。

### 注意

> 如果您不记得在 `lilo.conf` 中为 `LILO:` 提示指定的确切标签，请按 Tab 键让 LILO 打印可用内核列表。如果这不起作用，您也可以尝试在 `LILO:` 提示出现前按下 Alt 或 Shift 键。

### 如何卸载 LILO

您可以使用 `lilo -u` 命令（以 `root` 身份）卸载 LILO。或者，如果 LILO 未安装在 MBR 上，您可以使用 Linux 或 MS-DOS 下的 `fdisk` 使另一个分区处于活动状态来禁用它。如果 LILO 已作为 MBR 安装，您可以在 MS-DOS 下启动并使用命令 `fdisk /mbr` 恢复原始 MBR。

### 故障排除 LILO

您不应该遇到任何与 LILO 相关的问题，但如果确实遇到了，您将会看到 70 种不同的警告或错误消息之一。这里没有列出所有消息，但表 3.2 列出了最有可能出现的六个 `LILO:` 提示或初始错误。

| 提示 | 描述 |
| :--- | :--- |
| `L<span>` | `nn` 代表 16 个磁盘错误代码之一。 |
| `LI` | 第二阶段引导加载程序已加载，但无法运行。 |
| `LIL` | 无法读取描述符表。 |
| `LIL?` | 第二阶段引导加载程序加载到了错误的地址。 |
| `LIL` | LILO 发现描述符表已损坏。 |
| `LILO` | LILO 运行成功。 |

磁盘错误代码可能指示诸如软驱门打开、驱动器超时、控制器错误、介质问题、BIOS 错误，甚至是一读问题（通过重新启动可以克服）等问题。总体而言，LILO 的一些常见问题包括：
- 内核更改后未重新运行 `/sbin/lilo`
- 在创建新启动映射时错误使用 `/sbin/lilo`
- 从非常大的（2GB+）分区安装和启动 Linux
- 在安装 Linux 和 LILO 之后安装另一个操作系统（例如 Windows 95，它会覆盖 MBR）
- 手动编辑后 `/etc/lilo.conf` 中的错误
- MBR 损坏
- 在 Linux 交换分区中安装 LILO（这应该是 impossible 的）
- 缺少 Linux 内核映像（`/etc/lilo.conf` 中的错误）
- 在 DOS 分区上安装 Linux 并从该分区启动，然后对 DOS 分区进行碎片整理
- 在 `LILO:` 提示处传递错误的内核消息

如果遇到麻烦，一定要参考 Almesberger 的 readme 文件，它位于 `/usr/share/doc/lilo` 目录下。采纳他的建议：不要惊慌！通过一些预见性、检测和坚持，您应该能够避免或克服问题。

### 使用 LOADLIN.EXE 引导 Linux

`LOADLIN.EXE` 是一个使用 DOS MBR 引导 Linux 的程序。Hans Lermen 编写的这个实用程序还可以传递内核选项。当您需要从 DOS 启动以正确初始化调制解调器或声卡，使它们能在 Linux 下工作时，`LOADLIN.EXE` 非常有用。

在使用 `LOADLIN.EXE` 之前，您需要做两件事：
1. 将 `LOADLIN.EXE` 复制到 DOS 分区（例如 `C:\LOADLIN`）。
2. 将内核映像（`/vmlinuz`）的副本放在您的 DOS 分区上。

例如，在 DOS 命令行中键入以下内容以引导 Linux：
`loadlin c:\vmlinuz root=/dev/hda3 ro`

请确保在命令行中插入您的根分区。`ro` 代表只读。当您第一次引导 Linux 分区时，应将其挂载为只读以防止数据丢失。

如果您有 UMSDOS 文件系统，可以键入以下内容：
`loadlin c:\vmlinuz root=/dev/hda1 rw`
`rw` 代表读写。以这种方式启动 UMSDOS 文件系统是安全的。同样，请确保替换为您自己的分区。`LOADLIN.EXE` 接受许多选项：请参见第一张 CD-ROM 上 `dosutils` 目录中 `LOADLIN.TGZ` 文件的文档。

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_101_0.png)

### 安装和使用 BootMagic

BootMagic 是 PowerQuest 的 PartitionMagic 程序中包含的商业引导加载程序。此引导加载程序必须使用 Windows 安装，并且可以在您在单独分区中安装 Linux 后进行安装和配置。如果您的计算机没有 CD-ROM 驱动器，您将不得不使用另一台计算机将 `BTMAGIC` 目录从 PartitionMagic CD-ROM 复制到软盘，然后再复制到您的 Windows 桌面。然后您可以单击 `Setup.exe` 程序来安装 BootMagic。您会看到一个对话框，如图 3.1 所示。

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_102_0.png)

**常备一张启动盘！**

如果在安装 Linux 时询问，请务必创建一张 Linux 启动盘！如果在安装或配置替代引导加载程序时出现问题，拥有启动盘可以避免许多麻烦。BootMagic 会覆盖主可引导硬盘的 MBR，并会抹去之前的 LILO 安装！如果您想使用 BootMagic 和 LILO，请确保先将 LILO 安装到根原生 Linux 分区！

接下来的七个对话框中，请填写您的用户信息、目录位置等。然后，系统会询问您是否要创建可引导的 BootMagic 软盘。这是个好主意，如果之后您在启动 Windows 或 Linux 时遇到麻烦，这张软盘可能会很有用。创建软盘后，您将看到一个用于将其他可引导分区添加到 BootMagic 初始启动菜单的 BootMagic 配置对话框。单击“添加”按钮开始。

为了显示您的 Linux 分区，请单击“高级”复选框，然后单击根 Linux 分区。完成后，单击“确定”将 Linux 添加到 BootMagic 的启动菜单中。然后，系统会（在新对话框中）要求为您的 Linux 分区命名并选择图标。完成后单击“确定”，您将看到 BootMagic 的主对话框（如图 3.2 所示）。

主对话框用于设置默认启动的操作系统。单击您的新 Linux 条目，然后单击向上箭头/重新排序按钮，将 Linux 移动到列表顶部。选中您的 Linux 条目时，单击“设为默认”按钮，以确保您的计算机默认启动到 Linux。请注意，您可以设置启动延迟、删除或重命名条目，以及启用或禁用 BootMagic。完成后，单击“保存/退出”按钮，BootMagic 将安装完成。

## Red Hat Linux—安装和用户服务

### 图 3.2

使用 BootMagic 配置对话框中的按钮来重新排序操作系统列表，并选择默认引导的操作系统。

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_103_0.png)

当您重新启动计算机时，您将会看到一个供选择的引导操作系统的图形菜单。您可以使用鼠标点击，或者等待预设的时间延迟，然后 Linux 将会启动。

## 摘要

本章介绍了配置、安装和使用 LILO 的基础知识，向您介绍了 `LOADLN.EXE` 启动实用程序，并展示了 PowerQuest 公司的一款商业启动实用程序 BootMagic 的安装和配置。希望您已经看到，使用 LILO 可以让您在 PC 上安装的操作系统的数量上拥有更大的灵活性，并且 Linux 可以与其他系统一起使用。别忘了阅读 LILO 的文档，因为您不仅可以了解操作系统如何从硬盘启动，还可以了解如何自定义 Linux 引导提示符。

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_104_0.png)

## 配置 X Window 系统，版本 11

### 本章内容

- 什么是 X11？ 68
- XFree86 或其他 X11？ 68
- XFree86 4.0.1 的新特性 69
- 选择配置工具 72
- 检查 `XF86Config` 文件 90
- 使用 `startx` 命令启动 X11 99
- 使用 `xdm` 103
- XFree86 故障排除 104

### 什么是 X11？

X 窗口系统（The X Window System）是一个网络窗口系统，它为具有位图显示的计算机构建图形界面客户端提供了一组基本的通信协议和功能。您永远不应该将 X 窗口系统称为 X Windows；正确的称呼是 X、X11、X 版本 11 或 X 窗口系统版本 11。
