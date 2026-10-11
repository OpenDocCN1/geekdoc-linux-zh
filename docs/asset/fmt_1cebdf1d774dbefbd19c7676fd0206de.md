
```
C:\SLACK> REWRITE B:
```

现在准备好启动安装磁盘了。假设你已经选择并创建了引导磁盘（如果没有，请参见前面的章节），将引导磁盘放入 A 盘重启。当磁盘启动时，你会看到欢迎消息和满屏信息，以及屏幕底部的

```
boot:
```

提示符。你需要在此提示符处输入一些信息，告诉内核在哪里挂载你的根磁盘。如果你在 B 上有 3.5 英软磁盘驱动器，太极了——你会想它作为根磁盘。如果没有，你必须依靠驱动器中的根磁盘。由于根磁盘在驱动器中，你无法从软磁盘安装或在安装过程结束时制作引导磁盘，因为磁盘将“挂载”在驱动器中，在机器重启之前无法移除（无论屏幕如何提示）。以下是在 `boot:` 提示符处输入使用 A 盘中解压根磁盘的命令：

```
boot: mount root=/dev/fd0 ramdisk=0
```

如果根磁盘在 B:，请将其插入 B: 并输入此命令：

```
boot: mount root=/dev/fd1 ramdisk=0
```

内核现在将启动。如果你使用 A 盘作为根磁盘，系统会提示交换磁盘并按下 `Enter`。一旦完成此操作，根磁盘将开始加载，最终给你登录提示符。从这里你可以安装 Linux。警告：如果你使用这种方法在 A 盘中使用根磁盘进行安装，在关机之前你无法从驱动器中移除根磁盘。结果是，在配置系统时你无法安装引导磁盘内核，并且将

# 第 2 章：安装 Linux

你需要一种不同的方法来启动启动。启动机器的一种简单方法是使用安装启动盘，并在启动提示符处使用略有不同的命令。例如，如果你将 Linux 安装在 `/dev/hda2` 上，你可以在启动盘的启动提示符处使用此命令启动 Linux：

```
boot: mount root=/dev/hda2 ramdisk=0 ro
```

这将在 `/dev/hda2` 上启动 Linux，不带内存磁盘，且为只读。如果你使用 UMSDOS，你可能希望以读写模式启动系统，如下：

```
boot: mount root=/dev/hda2 ramdisk=0 rw
```

一旦你的机器开始运行，你可以根据需要切换到不同的内核，使用光盘ROM 上 `KERNELS` 目录下的选项之一，或者从 `/usr/src/linux` 中的内核源码中编译自己的内核。这将提供最佳性能，因为它不包含任何必要的驱动程序。

## 使用 Loadlin 从 DOS 启动 Linux

`Loadlin` 是对于同时也运行 MS-DOS 或 Windows 95 的 Linux 用户的实用工具。使用 `Loadlin`，你可以从 DOS 提示符启动 Linux，或者在 Windows 95 中设置一个图标允许你切换到 Linux。`Loadlin` 可能是从硬盘启动 Linux 最安全的方法，因为它完全不需要触动分区表——你只需正常启动 DOS，并在需要时使用 `LOADLIN.EXE` 命令启动 Linux。

要使用 `Loadlin`，你需要在你的 DOS 驱动器上安装它。要做到这一点，你需要使用一个解压缩程序，例如 `UNZIPEXE` 或 `PKUNZIP.EXE`；大多数 DOS 用户已经拥有这些程序的副本。假设你的 Slackware 光盘在 E 盘上，并且你想将 `Loadlin` 放在 C 盘上；按如下方式解压文件：

```
C:\> PKUNZIP -d E:\KERNELS\LOADLIN16.ZIP
```

`-d` 标志告诉命令保留 zip 存档中找到目录结构。将在你的机器上创建一个 `C:\LOADLIN` 目录，其中包含许多文件。

下一步是从光盘ROM 上 `KERNELS` 下的子目录中选择一个合适的内核。`BOOTDSKS.144` `WHICH.ONE` 文档可能对你做出选择有所帮助。实际的内核文件将名为 `ZIMAGE` 或 `BZIMAGE`；这是你想要复制到 `C:\LOADLIN` 目录的文件。

对于此示例，我们将使用 `E:\KERNELS\BARE.I` 目录中的内核：

```
C:\> CD LOADLIN
C:\LOADLIN COPY E:\KERNELS\BARE.I\ZIMAGE
```

现在我们有了启动 Linux 系统所需的一切。要做到这一点，你需要知道以下信息：

- 你打算启动的 Linux 分区的设备名称（例如 `/dev/hda2`）
- 你计划使用的 Linux 内核的路径和文件名（例如 `C:\LOADLIN\ZIMAGE`）
- 分区是否应该挂载为只读（如原生 Linux 分区所示，以便在启动时进行安全的文件系统检查）或读写（UMSDOS 需要的，它在启动时不检查文件系统）

这些信息被传递给 `LOADLIN.EXE` 程序，该程序反过来将 Linux 加载到内存并启动它。这是一个示例：

```
C:\LOADLIN> LOADLIN C:\LOADLIN\ZIMAGE ROOT=/dev/hda2 RO
```

这加载了 Linux 内核并在只读 `RO` 模式启动 `/dev/hda2` 分区。如果你在使用 UMSDOS，你需要将 `RO` 替换为 `RW` 以使用读写模式。

> 某些 DOS 驱动程序会干扰 `Loadlin`，特别是用于扩展内存的 `emm386` 驱动程序。如果发生这种情况，你必须从 `CONFIG.SYS` 文件中删除该驱动程序并重试。此外，`Loadlin` 不会在 Windows 95 下直接运行，尽管你仍然可以它设置一个图标先将电脑切换到 DOS 模式（换句话说，过程是在 Windows 95 下启动 DOS 会话然后启动 `Loadlin`。我们将在下一节进一步解释）。

如果一切顺利，你的机器应该切换到 Linux。如果你想进一步自动化此过程，请编辑 `C:\LOADLIN` 目录下的 `LINUX.BAT` 文件。然后将 `LINUX.BAT` 复制到 `C:\DOS` 目录，你就可以通过简单在提示符处输入 `LINUX` 从 DOS 切换到 Linux。

## 在 Windows 95 中添加 Linux 图标

对于运行 Windows 95 的用户：

1. 使用鼠标右键点击 Windows 桌面。在“新建”下，选择“快捷方式”。
2. Windows 95 将显示“创建快捷方式”对话框，询问用于启动程序的命令行。将你的 `LINUX\LOADLIN\LINUX.BAT` 路径输入到框中并按回车键。例如：

```
C:\LOADLIN\LINUX.BAT
```

3. Windows 将为程序想要一个标题。默认的 Linux 应该没问题，但你可以输入你喜欢的任何内容。
4. 现在你需要选择一个图标。同样，你可以挑选你喜欢的任何。（我们使用急救图标——Linux 来救援了！)

现在你会看到桌面上出现了新的 Linux 图标。然而，它还没有准备就绪；正如我们所回的，`Loadlin` 不会在 Windows 95 下直接运行，你需要为其设置一个图标先将电脑切换到 DOS 模式。

1. 右键点击 Linux 图标并选择属性。
2. 点击“快捷”选项卡。
3. 勾选“在 DOS 模式下运行”。
4. 点击确定。

## 使用 Loadlin 无软盘安装 Linux

使用 `Loadlin` 无软盘安装 Linux

这很少见，但在某些情况下（尤其是使用笔记本电脑时），软盘控制器无法正常工作，导致引导磁盘无法加载。首先，你需要像以前一样安装 `Loadlin`，在 C 驱动器上解压 `loadlin16.zip`：

```
C:\> UNZIPEXE E:\KERNELS\LOADLIN16.ZIP
```

接下来，从光盘ROM 的 `KERNELS` 目录选择一个内核并将其安装到 `LOADLIN` 目录。在此示例中，我们将使用 `E:\KERNELS\BARE.I` 中的内核：

```
C:\> COPY E:\KERNELS\BARE.I\ZIMAGE
```

现在你需要将引导磁盘镜像 `COLOR.GZ` 复制到 `LOADLIN` 目录：

```
C:\> COPY ROOTDS\COLOR.GZ
```

现在你可以使用 `Loadlin` 启动系统。进入 `LOADLIN` 目录并使用 `Loadlin` 加载内核：

```
C:\> LOADLIN INIT=COLOR.GZ
```

这将启动 Linux 并给你登录提示符。从这里你可以登录并照常安装 Linux。

### 重新编译内核

大多数 Linux 用户会发现附带光盘上的预编译内核应该适用于他们；如果你留心了第一章，你将获得一个优化 Linux 安装和使用的硬件配置。

然而，在极少数你需要重新编译内核（无论是通过 Linux HOW-TO 指导还是通过专家的建议；这在使用不支持的 SCSI、总线鼠标或声卡时会发生），方法如下：

0. 如果你还没有安装 C 编译器和内核源码，请安装它们。
2. 以 root 身份登录，并按照以下步骤重新编译内核：

```
cd /usr/src/linux
make config
```

此时你将选择你的驱动程序。重复步骤 3 直到你对选择满意。

如果你使用 `LILO`，以下命令将构建并安装新内核：
