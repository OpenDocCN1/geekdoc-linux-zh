
U 盘的细节将在第 6 章“运行原生 盘安装”中讨论。

### 如何进入启动提示符

要到达启动提示符，请遵循以下步骤：

1. **计算机开启或关闭启动：**
    * 计算机开启——如果计算机已开启，插入 DSL CD。如果你恰好正在运行 Windows 且 CD 驱动设置为自动运行，则会出现关于 DSL 的信息。
    * 计算机关闭——如果计算机关闭，开启它并立即插入 DSL CD。在某些计算机上，开机后立即按下 Pause/Break 键会暂停启动，留出时间插入 CD。某些计算机有特定的键位进入 BIOS 设置；你可能还想按键进入 BIOS 以留出时间插入 CD。

2. **出现启动界面**——大多数较新的计算机会自动检查可引导 CD。DSL 启动界面（见图 2-2）应该出现。如果不能……你会得到一个只有三行文本的启动提示符。

3. **启动 DSL**——在启动提示符处按回车接受所有设置。如果 60 秒内没有任何操作，DSL 将自动启动。你看到图 2-1所示的 DSL 桌面了吗？如果没有，下一步是尝试后续章节描述的启动选项。

# 第 2 章 启动 DSL

### 启动界面的帮助

当显示 DSL 启动界面时，你应该熟悉左下角的启动提示符。你可以按回车、等待几秒，或按 F2 或 F3 查看帮助。帮助界面是启动提示符的摘要。按 F2 或其他任何键取消计时，使 DSL 不自动启动；图 2-3 显示了在启动提示符处按 F2 出现的界面。

```
dsl fb1280x1024 : fb1024x768 : fb800x600
vga=normal
sl desktop
sl noicons
sl md=(hd1)
sl skip
sl restore=(hd1)
sl toram
sl to=vgahd1
Start various at boot
sl lang (ca cs ...) : Choose/Keyboard
sl outill : Disable disk-detection
sl dma
sl failsafe
expert
boot:
Framebuffer mode (for notebooks)
Safe video mode (F3 for more)
Prompt user (for X setup)
If booting to X use desktop (default to corrupt)
Copy only the last image
Turn off automatic restore
Select boot location
Copy to HD partition and run (20 MB)
Turn on DMA accel. for all drives
BIOS: Test mode
Interactive startup/setup
```

图 2-3 按 F2 查看语言、视频、恢复和其他功能的启动选项。

图 2-4 显示了在启动提示符处按 F3 出现的界面。

从启动选项可以看出，有很多选项可以尝试。然而，大多数选项是为了解决少数问题或提供增强型的方法（例如完全从 RAM 运行）。事实是对于大多数用户来说，DSL 不需要额外选项即可启动，因此他们可以在本章的第一段后停止阅读。

有些机器需要额外的启动选项。通常困难的机器在 VGA 能力、电源管理方面存在问题，PNP 特殊启动选项可以帮助。其他启动选项可开启特殊功能（例如添加密码或启动服务）。这些选项中的将在其他章节中讨论，并在本章后面的“高级启动选项”部分经常讨论。

# 38 官方 Damn Linux 教程

DSL 接受以下启动时 `vga` 选项：

| 颜色 | 640x480 | 800x600 | 1024x768 | 1280x1024 |
|---|---|---|---|---|
| 256 | 8 bit | 771 | 773 | 775 |
| 3200 | 15 bit | 784 | 787 | 793 |
| 6500 | 16 bit | 788 | 791 | 794 |
| 16.7M | 24 bit | 789 | 792 | 795 |

*来自表格*

```
dsl vga=7xx
dsl prompt
dsl script
dsl halt=xxx
dsl minimal
dsl desktop(fluxbox)
dsl web
dsl legacy
dsl dumpfile(hda1)
dsl leafs
lowram
install
Prompt for root and dsl passwords
Password encrypted backup
Set hostname=xxx
Starts with Minimal theme
Starts with flux or Joe's WM
Waits for USB devices
Boots without union
Scans and Specify dumpfile
Feats commented filesystem
Starts X Minimal, noicons, mouse, noideraid, etc.
No X, CLI installation for hard drive, floppy.
```

**图 2-4** 按键查看用于设置、选择桌面或其他启动时功能的启动选项。

### 尝试不同的启动选项

让我们卷起袖子，尝试一些常见的启动选项并讨论一些解决方案。在启动提示符处，让我们尝试几个基础选项。

+ **视频启动选项——默认情况下，DSL 进入高分辨率 `vga=791` 模式。这对于你的计算机视频来说可能分辨率太高。使用启动选项 `vga=normal` 可能会帮助。**

```
dsl vga=normal
```

许多旧笔记本电脑需要帧缓冲视频而不是 Xvesa。启动时，你可能想尝试：

```
boot: fb800x600
```

注意我没有将单词 `dsl` 作为第一个选项。取决于你的笔记本电脑，它可能是 `fb1024x786`。如果你收到关于 `fbdev` 的错误，使用帧缓冲可能没有帮助。

注意 F3 界面上的 `vga` 分辨率表（见图 2-4）。可以使用 `vga=` 选项选择任何一个值。

正如我指出的，可能需要组合选项。尝试这种常见的选项选择：

```
boot: dsl vga=normal noapic noacpi npbios=off acpi=off noapm
```

成功了？太棒了。现在，你应该再次尝试，但这次逐个撤回之前的选项，直到你拥有了启动所需的精确选项集。我们称此为为你的特定机器微调选项。另一方面，你可能仍然面临问题，尚无法进入 DSL 系统。

- failsafe 启动选项（安全模式启动）——一组强大的预设选项组合被称为 `failsafe`。
  尝试这个：
  **failsafe**

如果 `failsafe` 对你有效，你该如何微调你的选项呢？你始终可以在命令行或 X Windows 中查看你的启动选项。输入 `showbootoptions`；或者从 DSL 命令、shell 窗口、DSL 桌面面的 System Stats（系统统计）、Boot Tab（启动选项卡）查看。然后，你可以尝试通过消除 `failsafe` 显示的每个启动选项来尝试启动。你需要这样做，是因为其中某些选项会阻止声音以及你之后将使用并享受的其他功能。

- lowram 启动选项（低内存启动）——对于内存为 64MB 或更小的机器，你可能想要考虑另一种预设选项组合'*lowram* 的用法与 `failsafe` 类似，但针对低内存系统进行了优化。同样，你可能希望使用启动代码或 System Boot 选项卡来查看预设选项，并根据你的特定需求开始微调。

- toram 启动选项（全内存启动）——对于内存丰富的机器，你可能想要尝试 `toram` 启动选项。将此选项添加到你的其他选项列表中会将 DSL 完全加载到内存中。这将提供一个极快的系统，因为不需要再次访问 CD。在确定你的机器所需的启动选项并至少拥有 128MB 内存之前，你不应该尝试这样做。

### 第二阶段启动：自动配置

DSL 的第二阶段是自动配置和环境初始化。该阶段在第一阶段启动提示按下 Enter 键后立即开始。我们输入的所有启动选项都会被处理，以确定尝试哪些自动配置。通常，此过程在无需干预的情况下运行。图 2-5 显示了典型的自动配置过程。

成功完成后，该阶段通常通过初始化 X Window 系统结束。X Window 系统用于托管图形 DSL 桌面。当然，使用启动时间选项 2 (`ds1 2`) 会防止 X 启动，并在 root 用户的 shell 提示符终止启动过程。

40 《官方 Damn Linux 籍》

![](img/f6eecb623fe812080d8ad148db9eda3a_60_0.png)

图 2-5 DSL 第二阶段启动。

希望你已经取得了成功。有些人可能已经看到了 DSL 桌面并准备好进行探索。有些人对到达运行级别 2 的系统提示符感到很满意。对于另一些人，还需要第三阶段启动。

> 注意
