
- `486DX` (推荐 `Pentium I`) `32MB RAM`
- `IDE` 启动 `CD` 驱动器或 `3.5"` 软驱器加上不可启动 `CD` 驱动器
- `SVGA` 兼容显卡
- 支持 `800x600` 像素分辨率的显示器
- 串口鼠标、`PS/2` 鼠标或 `USB` 鼠标

尽管上述硬件是从 `CD` 启动 `DSL` 的最低要求，但如果你只有一个软驱器，实际的最低要求如下：

- `486DX` `16MB RAM`
- `500MB` 硬盘
- `3.5"` 软驱器
- `SVGA VESA` 兼容显卡
- 串口鼠标

由于最小硬件（`486DX`）通常带有软驱器而不是 `CD` 驱动器，因此需要磁盘空间来存放 `DSL`。这种最小硬件配置及其 `DSL` 的安装将在第 8 章“以其他方式安装 `DSL`”中讨论。本章的重点是从 `CD` 或或通过 `CD` 启动，并且至少具备推荐的硬件配置。

> 注意
最新的 `Damn Small Linux` 可以在较新的基于 `Intel` 的 `Mac` 电脑上启动。然而并非所有的硬件（如网卡）都受到支持。理论上，你可以使用 `Apple Bootcamp` (`www.apple.com/macos/bootcamp`) 在这些机器之一上将 `DSL` 安装到硬盘。但该配置并未获得 `DSL` 的官方支持。

### 软件要求–DSL 版本

`Damn Small Linux` 有多个不同的版本。你使用的版本取决于运行 `DSL` 的环境。`DSL` 包含以下四个版本：

- `SYSLINUX` 版本——用于旧旧 `PC`，这些 `PC` 要求启动介质不能大于软盘镜像（即使该镜像在 `CD` 上）。有关关于 `SYSLINUX` 启动加载程序的更多信息，请参阅 `SYSLINUX FAQ` (`http://syslinux.zytor.com/faq.php`)。
- `ISOLINUX` 版本——用于启动光盘，因为不需要特殊的软盘仿真磁盘。有关更多信息，请参阅 `ISOLINUX FAQ` (`http://linux.zytor.com/iso.php`)。
- `Qemu` 虚拟机版本——设置 `Qemu` 在 `Linux` 系统内虚拟化运行 `DSL`。
- `VMware` 虚拟机版本——设置 `VMware` 在 `Windows` 系统内虚拟化运行 `DSL`。

前两个版本涉及从 `CD` 启动，这是本章的主题。另外两个版本将在第 7 章“在 `Windows` 中嵌入运行 `DSL`”中讨论。为什么 `CD` 有两个版本？因为 `DSL` 针对的是较旧和更小型的硬件，许多此类系统只有在存在实际仿真软盘的情况下才能从 `CD` 启动。这种启动的软盘大小被限制在真实软盘的大小。后来的机器设计时没有这种限制。

所以，第一个规则是：如果你的机器无法开始启动过程，或者你的机器是旧款型号，请使用 `SYSLINUX` 版本。

`DSL` 的 `SYSLINUX` 版本在启动时仿真单个软盘。`SYSLINUX` 版本的驱动程序较少，因为它们必须全部放入单个软盘大小的文件中。`Knop` 和其他选择 `ISOLINUX` 的原因是没有软盘大小限制。`ISOLINUX` 版本拥有更多驱动来支持较新的电脑。

## 获取 Damn Small Linux

有几个版本的 `Damn Small Linux` 包含在附带的 `CD` 中。你可以参考附录 `A`“关于 `CD`”来了解这些版本以及如何使用它们。然而，如果你手头没有 `CD` 或有较新版本的 `DSL` 可用，你可以考虑下载 `DSL` 副本制作自己的启动 `CD`。

### 下载 Damn Small Linux

如果你对光 `CD` 概念陌生，第一步是寻找本地 `DSL` 下载镜像。你可以通过检查 `Damn Small Linux` 网站查看最新的下载站点列表：

`http://www.dammsallsux.org/download.html`

以 `Ibiblio` 为例，导航到站点目录：

`ftp://ibiblio.pub/Linux/distributions/dammsux/current`

根据前面的讨论，选择你想要下载的版本。通常情况下你需要的 `ISOLINUX` 版本命名为 `dsl-??`，其中 `??` 被替换为 `DSL` 版本号。

创建启动 `CD` 有许多方法，许多操作系统都可以执行此任务。你需要使用具有“刻录镜像”或“写入磁盘”选项的 `CD` 刻录程序。

许多 `Linux` 系统有 `k3b` 工具和 `cdrecord` 命令来刻录 `CD`。对于 `Windows` 用户，`Nero` 和 `Roxio` 是流行的商业软件。`Windows` 还有 `CD Burn XP Pro` (`http://cdburnerxp.se`) 和 `Infra Recorder` (`http://infarecorder.sourceforge.net`) 应用。

### 进入启动提示符

通过尝试启动 `DSL` 光 `CD`。如果 `SYSLINUX` 或 `ISOLINUX` 版本都无法进入启动界面，这里是你可以尝试的一些方法：

- 确保你的 `CD` 刻录没有失败。如果你下载并刻录了自己的 `CD`，最好以非常低的速度刻录。我建议将刻录速度降低到 `4`。是的，即使你有新的 `52X` 刻录机。
- 某些电脑从 `CD-RW` 启动有困难。最好使用 `CD-R`。
- 如果你有光 `CD`（例如 `KNOPPIX`），尝试从该 `CD` 启动以查看问题是否仅针对 `DSL`。

# 34 官方 Damn Small Linux 教程

如果你的计算机无法从 `CD` 启动，你可以尝试创建一个启动软盘。`DSL` 标准启动软盘镜像 `bootfloppy.img`。你可能想检查是否有本地下载镜像以缩短下载时间。查看 `Damn Small Linux` 网站板块：`www.damnsmalllinux.org/download.html`。

找到要下载的文件。例如，

```
ftp://biblio.pub/Linux/distributions/damnsmalllinux/current/
bootfloppy.img
```

将此镜像写入一个已知的软盘。不要使用旧软盘，因为它们在发生读取错误时可能会引起麻烦。使用典型的工具创建启动软盘。通常意味着在 `Windows` 下使用 `rewrite`，或者在 `Unix/Linux` 类型系统下使用 `rewrite`。

例如，如果你的 `Unix/Linux` 系统的第一个软盘设备位于 `/dev/fd0`，且 `bootfloppy.img` 位于当前目录，你可以使用以下命令 `dd` 将镜像写入插入的软盘：

```
## dd if=bootfloppy.img of=/dev/fd0 bs=16k
```

取决于你正在使用的版本，将 `bootfloppy.img` 文件写入 `DOS` 提示符（将启动镜像位于 `C` 盘根目录；并在 `C:\windows\command` 目录下运行 `rewrite`）的过程应与以下类似：

```
C:\ cd \windows\command
C:\windows\command> rewrite
Enter disk image source file name: C:\bootfloppy.img
Enter target diskette drive: A:
Please insert a formatted diskette into drive
A and press -ENTER-<Enter>
```

`Windows` 的 `rewrite` 程序可以在此站点找到：

```
http://www.chrysocome.net/rewrite
```

创建软盘后，务必更改计算机的 `BIOS`，使软盘成为第一个启动设备。将新创建的软盘插入驱动器并开启或重启系统。如果你使用了良好的软盘且没有发生读取错误，将看到 `DSL` 启动界面。

希望你已经到达了 `DSL` 启动界面（见图 `2-2`）。如果你到达这里，需要启动软盘，或者下载并创建 `SYLINUX` 版本，只需在 `DSL` 启动提示符处按回车即可。

看到 `DSL` 启动界面后，你可以在提示符处输入许多选项来引导启动过程的方向。以下章节描述了 `DSL` 启动过程以及如何修改它。

# 第 2 章 启动 DSL

图 `2-2`

`DSL` 启动界面允许你向启动过程添加选项。

![](img/f6eecb623fe812080d8ad148db9eda3a_55_0.png)

## 理解 DSL 的启动阶段

启动 `DSL` 有三个阶段。第一阶段是到达启动提示符。启动提示符允许输入额外的启动选项。第二阶段是 `DSL` 的自动配置和环境初始化。此阶段处理启动时选项并设置 `DSL` 的运行环境。第三阶段有时需要（有时是要求）执行无法通过自动配置提供的额外设置——例如，串口、双键或 `USB` 鼠标、非美式键盘，或非默认的 `1024x768` 屏幕分辨率。

如果你的计算机引导了 `DSL CD` 启动，你应该看到一个与图 `2-2` 类似的启动界面。

让我们深入研究 `DSL` 的启动过程。

> 注意
本章仅涵盖与从现场 `CD` 启动的标准任务相关的启动过程。更高级、更详细的讨论请见第 `11` 章“设置完全重制环境”。

### 第一启动阶段：选择启动选项

启动提示符允许你自定义 `DSL` 的启动过程。例如，你可以在启动时指定完全加载到 `RAM` 中、指定你的备份文件位置，甚至指定额外应用程序的存储位置。要到达启动提示符，你可以使用 `CD`、软盘或 `U` 盘。理解这一阶段的价值在于你可以理解用于更改 `DSL` 启动方式的选项。

> 注意
