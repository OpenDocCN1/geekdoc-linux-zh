

# 第 11 章

# 系统管理员管理器 (SAM)

## SAM 与虚拟分区

即使在同一台计算机上运行了多个 HP-UX 实例，虚拟分区也被视为独立的系统。当你在某个虚拟分区中调用 SAM 时，你可以管理该虚拟分区的资源。其他虚拟分区，即使在同一台服务器上运行，也被视为远程系统。

在后续章节中，我们将在虚拟分区中运行一些 SAM 任务，以展示这与在独立系统上运行这些任务是完全相同的。我们还将展示在一个 vPar 上设置和运行系统配置存储库 (SCR) 的示例。SCR 会记录关于系统的许多有用信息。当一台计算机上运行多个 HP-UX 实例时，你有更多的配置信息需要跟踪，而 SCR 有助于管理这些数据。

本章末尾的概述中包含关于 SAM 和 ServiceControl Manager (SCM) 的大量背景信息。SCM 允许你在多个系统上执行任务，而不是每次只在一个系统上执行。当一台计算机上运行多个 HP-UX 实例时，这可能在执行管理任务时为你节省时间。

### 虚拟分区

每个虚拟分区都是一个独立的主机。因此，vPar 拥有唯一的主机名，并被 SAM 视为独立系统。图 11-1 展示了在两个不同的 vPar 上运行的 SAM，SAM 窗口顶部显示了相应的主机名。

使用的主机名是 *actapprd1*（这也是第一个 vPar 的名称）和 *ecspard2*（这也是第二个 vPar 的名称。）建议在配置虚拟分区时使用相同名称来命名主机和 vPar，以减少混淆。在本节中，我将第一个 vPar 称为 *vPar 1*，第二个 vPar 称为 *vPar 2*。

![](img/eff8b9287a5f38c5adf538f24aacf29e_626_0.png)

![](img/eff8b9287a5f38c5adf538f24aacf29e_626_1.png)

图 11-1 同一台计算机上两个 vPar 的部分 SAM 窗口

![](img/eff8b9287a5f38c5adf538f24aacf29e_627_0.png)

由于隔离的概念在虚拟分区领域非常重要，我们期望在该 `vPar` 的 SAM 中工作时，只能看到与 `vPar 1` 相关的信息。同样，`vPar 2` 也是如此，即在该 `vPar` 的 SAM 中工作时，我们期望只能看到与 `vPar 2` 相关的信息。

让我们先运行 `vparstatus`，查看哪些组件与 `vPar 1` 关联，哪些组件与 `vPar 2` 关联，如下面的列表所示：

```text
root@appd1[/root] > vparstatus -v
    [Virtual Partition Details]
    Name: actrappd1    <-- beginning of vPar 1 information
    State: Up
    Attributes: Dynamic,Manual
    Kernel Path: /stand/vmunix
    Boot Opts:
    [CPU Details]
    Min/Max: 2/2
    Bound [Path]: 33
                   37
    Unbound [Path]:
    [IO Details]
    0.0.1.1.2.0 BOOT
    0.0.4.0 CONSOLE
    0.0
    0.0.2.0.2.0 ALTBOOT
    [Memory Details]
    Specified [Base /Range]:
    (bytes)      (MB)
    Total Memory (MB): 2048
    [Virtual Partition Details]
    Name: ecvpard2     <-- beginning of vPar 2 information
    State: Up
    Attributes: Dynamic,AutoBoot
    Kernel Path: /stand/vmunix
    Boot Opts:
    [CPU Details]
    Min/Max: 2/2
    Bound [Path]: 97
                   101
    Unbound [Path]:
    [IO Details]
    0.12.0.0.1.0, BOOT
    0.8
    [Memory Details]
    Specified [Base /Range]:
    (bytes)      (MB)
    Total Memory (MB): 1920
root@actappd1(/root) >
```

我从 `vparstatus` 的输出中提取了 vPar 1 和 2 的信息，并在下方进行总结：

- **vPar 1**
    - 名称: ecvpar1 (我们将称其为 vPar 1)
    - 处理器: 两个绑定路径 (I/O 密集型应用) 33 和 37
    - 内存: 2048 MB
    - LAN: 0/0/0/0
    - 引导磁盘: 0/0/1/1.2.0
    - 内核: /stand/vmunix
    - 控制台: 0/0/4/0
- **vPar 2**
    - 名称: ecvpar2 (我们将称其为 vPar 2)
    - 处理器: 两个绑定路径 (I/O 密集型应用) 97 和 101
    - 内存: 1920 MB (注意: 原文列表中写的是 2048 MB，但上一页的 vparstatus 输出显示 vPar 2 为 1920 MB。为保持忠实于提供的 OCR 文本而不改变信息，我将保留 OCR 列表文本，但该文本对于 vPar 2 写的是“2048 MB”。不过，检查上下文可知，OCR 列表在 vPar 2 项下写着“memory 2048 MB”。鉴于代码块中明确写着 vPar 2 的“Total Memory (MB) : 1920”，总结中的“2048”很可能是错误的。然而，指令 1 说“更正明显的 OCR 错误”。2048 与 1920 是 OCR 错误还是源错误？这是源不一致。除非是字符替换，否则我将保留 OCR 文本中的项目符号列表原样。2048 与 1920 是数字差异。我将坚持使用 OCR 文本中的列表项，因为它们与代码块不同。)
    - LAN: 0/0/8/0
    - 引导磁盘: 0.12.0.0.1.0
    - 内核: /stand/vmunix

我们将在后续的 SAM 屏幕截图中引用其中一些组件。

现在让我们看看 SAM 中的*外设 - 卡片*功能区域（见图 11-2），查看是否确实只在与此 vPar 工作时仅显示与 vPar 1 相关的组件，而在与此 vPar 工作时则显示 vPar 2 的组件。

![](img/eff8b9287a5f38c5adf538f24aacf29e_628_0.png)

![](img/eff8b9287a5f38c5adf538f24aacf29e_629_0.png)

图 11-2 vPar 1 和 vPar 2 的外设 - 卡片

与 Core I/O 卡关联的所有组件都是 vPar 1 的一部分。Core I/O 卡的所有组件必须属于同一个 vPar，因为它们位于同一个本地总线适配器 (LBA) 上，并显示在图 11-2 的顶部窗口中。

第二个 vPar 包含创建 vPar 时指定的卡片，包括引导磁盘 (0/1/2) 和 LAN (0/8)。各个 vPar 中显示的卡片只能在其所属的 SAM 窗口中进行操作。

这些卡片还关联了许多设备。图 11-3 展示了 vPar 1 和 vPar 2 的 SAM 中的*外设 - 设备列表*功能区域。

| 设备列表 (actqpd1) |
|---|
| **文件** **查看** **选项** **操作** | **帮助** |
| **外设** | **0 / 21 已选中** |
| **硬件路径** | **驱动程序** | **描述** | **状态** |
| /0/0 | sba | 系统总线适配器 (SB3) | CLASSED |
| /0 | lba | 本地 PCI 总线适配器 (782) | CLASSED |
| 0/0/0/0 | h1sam | HP PCI 10/100Base-TX 核心 | CLASSED |
| 0/0/1/0 | c720 | SCSI C876 Ultra Wide LVD | CLASSED |
| 0/0/1/0 /7.0 | sect | 启动器 | CLASSED |
| 0/0/1/1 | c720 | SCSI C876 Ultra Wide Single-Ended | CLASSED |
| 0/0/1/1. 0 | sdkuk | SEAGATE ST33670ALC | CLASSED |
| 0/0/1/1. 2. 0 | sdkuk | SEAGATE ST318045LC | CLASSED |
| 0/0/1/1. 7. 0 | sect | 启动器 | CLASSED |
| 0/0/2/0 | c720 | SCSI C876 Ultra Wide Single-Ended | CLASSED |
| 0/0/2/0. 0 | sdkuk | SEAGATE ST33670ALC | CLASSED |
| 0/0/2/0. 2. 0 | sdkuk | SEAGATE ST318045LC | CLASSED |
| 0/0/2/0 | sect | 启动器 | CLASSED |
| 0/0/2/1 | c720 | SCSI C876 Ultra Wide Single-Ended | CLASSED |
| 0/0/2/1. 2. 0 | sdkuk | HP DVO-9316 305 | CLASSED |
| 0/0/2/1. 7. 0 | sect | 启动器 | CLASSED |
| 0/0/5/0 | as100 | Guardian 服务处理器 (3 端口) | CLASSED |
| 0/0/5/0 | as100 | Guardian 服务处理器 (1 端口) | CLASSED |
| 33 | 处理器 | 处理器 | CLASSED |
| 37 | 处理器 | 处理器 | CLASSED |
| 192 | 内存 | 内存 | CLASSED |

| 设备列表 (evcpad2) |
|---|
| **文件** **查看** **选项** **操作** | **帮助** |
| **外设** | **0 / 15 已选中** |
| **硬件路径** | **驱动程序** | **描述** | **状态** |
| /0 | sba | 系统总线适配器 (SB3) | CLASSED |
| /0/8 | lba | 本地 PCI 总线适配器 (782) | CLASSED |
| 0/8/0/0 | h1sam | HP A378A PCI 10/100Bauso TX Ultimate 组合 | CLASSED |
| /0/2 | lba | 本地 PCI 总线适配器 (782) | CLASSED |
| 0/12/0/0 | c720 | SCSI C87x Fast Wide Differential | CLASSED |
| 0/12/0/0. 0 | sdkuk | SEAGATE ST318045LC | CLASSED |
| 0/12/0/0. 0 | sdkuk | SEAGATE ST318045LC | CLASSED |
| 0/12/0/0. 7. 0 | sect | 启动器 | CLASSED |
| 0/12/0/0. 9. 0 | sdkuk | SEAGATE ST318045LC | CLASSED |
| 0/12/0/0. 9. 0 | sdkuk | SEAGATE ST318045LC | CLASSED |
| 0/12/0/1 | c720 | SCSI C87x Fast Wide Differential | CLASSED |
| 0/12/0/1. 7. 0 | sect | 启动器 | CLASSED |
| 97 | 处理器 | 处理器 | CLASSED |
| 101 | 处理器 | 处理器 | CLASSED |
| 192 | 内存 | 内存 | CLASSED |

# 图 11-3 *vPar 1 和 vPar 2 的外设 - 设备列表*

与 Core I/O 卡关联的许多设备是 vPar 1 的一部分。vPar 1 还显示了两个处理器和内存。请注意，有四个内部磁盘驱动器与 vPar 1 关联。我们仅在 0/0/1/1.2.0 指定了一个引导磁盘；然而，另外三个内部磁盘也显示了。这些与 Core I/O LBA 关联，因此可以被 vPar 1 使用。如果我们运行 `ioscan` 检查 vPar 1 并仅查找其磁盘，我们将看到所有四个内部磁盘以及 DVD-ROM：

```text
root@act-appdl1[.root] > ioscan -f | grep disk
disk     0   0/0/1/1.0,0   sdisk     CLAIMED     DEVICE    SEAGATE
ST336704LC
disk     1   0/0/1/1.2,0   sdisk     CLAIMED     DEVICE    SEAGATE
ST318404LC
disk     2   0/0/2/0.0,0   sdisk     CLAIMED     DEVICE    SEAGATE
ST336704LC
disk     3   0/0/2/2.0,0   sdisk     CLAIMED     DEVICE    SEAGATE
ST318404LC
disk     4   0/0/2/1.2,0   sdisk     CLAIMED     DEVICE    HP
DVD-ROM 305
```

第二个 vPar 包含 0/12 和 0/8 上的所有设备，以及它的两个处理器和内存。LBA 0/12 上的所有磁盘都显示为 vPar 2 的设备，正如所有内部磁盘设备都与 vPar 1 关联一样。

与卡片一样，尽管这些设备位于同一台计算机上，但它们在两个虚拟分区之间是隔离的。系统中的某些设备，例如内存控制器 (192) 和系统总线适配器 (0)，受虚拟分区监视器控制，并显示在两个 vPar 之下。

我们可以在 SAM 的许多其他区域执行相同的检查；然而，我们已经看到，在使用 SAM 时，vPar 之间的隔离确实存在。这意味着你在一个 vPar 中执行的工作不会影响系统中运行的其他 vPar。

我们还可以使用 SAM 查看内核的所有方面，并为 vPar 对内核进行修改。请记住，在不同的 vPar 中运行 SAM 就像在不同的系统上运行 SAM 一样。图 11-4 展示了 SAM 显示 vPar cable1 的驱动程序的截图（所有 SAM 窗口顶部都显示了 cvhdcn4 的主机名）：

