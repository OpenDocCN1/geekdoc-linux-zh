
![](img/96d9ccd181675a8ae8b6a1146c919d2b_70_1.png)

### 未解决的依赖关系

许多软件包依赖于其他软件包或库才能正常工作。为了确保系统拥有正常工作所需的所有软件包，`Red Hat` `Linux` 在每次安装或移除软件包时都会检查这些软件包依赖关系。如果一个软件包要求另一个未安装的软件包，则存在未解决的依赖关系。

- 安装软件包以满足依赖关系
- 不安装具有依赖关系的软件包
- 忽略软件包依赖关系

总安装大小：`425M`

### `X` 配置

只要选择进行工作站安装，`X` `Window` 系统默认就会安装。配置 `X` `Window` 系统的第一步是选择您的显示器。如果列表中没有您的显示器，您可以手动输入手册或供应商网站上可用的频率设置。图 1-17 显示了 `X` 显示器配置屏幕。

![](img/96d9ccd181675a8ae8b6a1146c919d2b_71_0.png)

> 第 9 章详细讨论了 `X` `Window` 系统的配置。

![](img/96d9ccd181675a8ae8b6a1146c919d2b_71_1.png)

下一个选项允许您选择视频卡，如图 1-18 所示。在大多数情况下，安装程序可以为您检测视频卡。如果检测不正确，您可以手动选择卡或选项。

此屏幕上还提供了一个“使用图形登录”的选项。这会让系统启动到图形用户界面（`GUI`）登录屏幕，而不是普通的文本登录。如果在 `X` `Window` 设置期间做出错误选择，设置后启动时可能会遇到问题。建议您在测试 `X` `Window` 之前保持此选项禁用，并在设置完成后启用它。

### 即将安装

安装程序现在将显示“即将安装”屏幕。这是在对系统进行所有更改之前的最后一次警告。如果现在重新启动，您可以忘记直到此点所做的所有操作，系统仍保持原状。点击“`Next`”（下一步）开始安装 `Red Hat`。根据安装介质、所选软件包数量和计算机速度，这可能需要一些时间。

![](img/96d9ccd181675a8ae8b6a1146c919d2b_72_0.png)

图 1-18：`X` 视频卡配置

### 安装过程

下一步是设置程序复制安装期间选择的所有文件。图 1-19 显示了复制过程。

![](img/96d9ccd181675a8ae8b6a1146c919d2b_72_1.png)

图 1-19：安装软件包

安装完所有软件包后，系统将提示您创建启动盘。如果由于内核或 `LILO` 问题导致 `Linux` 无法启动，启动盘可以挽救您和您的系统。强烈建议您创建该磁盘。

就这样！重新启动并享受新的 `Red Hat` 安装。

## `Debian` 安装

`Debian` 的安装过程不如 `Red Hat` 那么顺畅，但 `Debian` 在其他方面弥补了这一不足。例如，一旦您理解了 `Debian` 的安装过程中使用的打包系统，您就可以极大地自定义安装源。这样，您可以同时从许多不同的媒体源进行安装。

### 引导

要开始 `Debian` 安装，您需要从安装 `CD` 或几张软盘启动。最简单的方式当然是 `CD-ROM`。开始安装时，您会看到图 1-20 中所示的“欢迎使用 `Debian`”屏幕。

![](img/96d9ccd181675a8ae8b6a1146c919d2b_73_0.png)

`Debian` 在其 `FTP` 网站上为许多不同配置提供了多个启动盘。创建这些启动盘使用的同一个 `Raw Write` (`rawwrite.exe`) 工具，与您之前用于创建 `Red Hat` 磁盘的工具相同。

```
Welcome to Debian GNU/Linux 2.2!

This is the Debian Rescue disk. Keep it once you have installed your system,
as you can boot from it to repair the system on your hard disk (if that ever
becomes necessary (press <F3> for details).

On most systems, you can go ahead and press <ENTER> to begin installation.
You will probably want to try doing that before you try anything else. If
you run into trouble or if you already have questions, press <F3> for
quick installation help.

WARNING: You should completely back up all of your hard disks before
proceeding. The installation procedure can completely and irreversibly
erase them! If you haven't made backups yet, remove the rescue disk
from the drive and press <RESET> or <Control-Alt-Del> to get back to
your old system.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law. For copyright information, press <F1B>.

This disk uses Linux 2.2.17
(from kernel-image-2.2.17-2.2.17pre6-1)

Press <F3> for help, or <ENTER> to boot.
boot:
```

图 1-20：欢迎使用 `Debian`

你可能会惊讶地发现，屏幕上显示这是一个救援磁盘。安装完成后，你可以使用启动光盘或磁盘来修复系统安装。该屏幕上可用的选项如下：

- `<ENTER>` — 启动安装
- `F1` — 安装帮助
- `F3` — 启动方法
- `F10` — 版权信息

`F3` 功能显示用于恢复或安装的可能启动方法。选项如下：

- `linux` — 启动默认安装。
- `ramdisk0` 和 `ramdisk1` — 启动安装，并从磁盘 0 或 1 读取 `RAM` 磁盘。这用于恢复模式，并将文件系统加载到 `ramdisk`（`RAM` 磁盘）中，这是一个看起来像普通磁盘的内存区域。
- `floppy0` 和 `floppy1` — 启动安装，并挂载第一或第二软驱中的磁盘。
- `rescue` — 启动并将任意卷挂载为根文件系统。你必须提供一个选项来指定要挂载的根卷（例如，`rescue root=/dev/hda1`）。

### 基础系统配置和安装

`Linux` 内核加载后，你将看到此版本的发布说明。在设置过程中，你可以访问其他控制台以获取信息。表 I-4 显示了控制台。

| 控制台编号 | 用途 |
| :--- | :--- |
| `Alt-1` | 设置程序 |
| `Alt-2` | `Shell` 提示符 |
| `Alt-3` | 调试消息 |
| `Alt-4` | 内核消息 |

发布说明将告诉你安装使用的是哪个内核，以及关于此次安装的其他重要说明。`Debian` 安装遵循特定的流程，但在某些情况下，如果必要，它会允许你按非顺序执行操作。图 1-21 显示了配置选项。每次返回菜单时，下一步都会作为默认选项给出。在这种情况下，它要求你配置键盘。选择你系统使用的键盘类型。

![](img/96d9ccd181675a8ae8b6a1146c919d2b_75_0.png)

图 1-21：主菜单

#### 磁盘设置

下一步是分区并设置数据卷和交换分区，如图 1-22 所示。

![](img/96d9ccd181675a8ae8b6a1146c919d2b_75_1.png)

图 1-22：磁盘驱动器选择

选择你要分区的硬盘。根据你的系统配置，你可能需要注意 `LILO` 限制屏幕中的警告，如图 1-23 所示。如本章前面所述，如果 `Linux` 内核存储在硬盘上 `8GB` 障碍之外，或超过 `1023` 号柱面，某些系统将无法启动。新版 `LILO` 允许你从驱动器的任何位置启动，前提是你的系统拥有足够新的 `BIOS`。如果系统不支持此功能，或者你只是不确定，请在 `8GB` 障碍以下创建一个 `/boot` 分区。

![](img/96d9ccd181675a8ae8b6a1146c919d2b_76_0.png)

图 1-23：`LILO` 限制屏幕

`Debian` 使用 `cfdisk` 处理分区。按你认为合适的方式设置分区。对于实验目的，将卷拆分可能是一个好主意，这样你可以获得不仅仅是单卷系统的经验。拆分磁盘的一种好方法是将 `/home`、`/tmp` 和 `/var` 放在单独的分区上。你也可以将 `/usr` 放在单独的分区上，但请确保至少分配 `1GB` 的磁盘空间，以便以后安装软件。别忘了创建交换分区！
