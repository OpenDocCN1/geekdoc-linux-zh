
## 概要

引导操作的选项如下：

-   `-a[c|R|S|D] devicefile`
    接受一个新位置（由 `devicefile` 指定）并将其传递给加载的映像。如果该映像是 HP-UX 内核，内核将擦除其预定义的 I/O 配置，并配置为指定的 `devicefile`。如果指定了 C、R、S 或 D 选项，内核将分别把 `devicefile` 配置为控制台、根、交换或转储设备。请注意，`-a` 可以重复多次使用。

-   `-f number`
    使用指定数字，并将其作为标志字传递给加载的映像。

-   `-i string`
    在启动系统时，设置 init 的初始运行级别（参见 `init(M)`）。指定的运行级别将覆盖 `/etc/inittab` 中 `initdefault` 条目所指定的任何运行级别（参见 `inittab(4)`）。

-   `-lm`
    在 LVM 维护模式下启动系统，仅配置根卷，然后启动单用户模式。

-   `-F`
    与 Switch/UX 软件一起使用。忽略启动盘上的任何锁定。仅当确定持有锁定的处理器不再运行时，才应使用 `-F` 选项。（如果未指定此选项且磁盘被其他处理器锁定，内核将从该磁盘启动以避免损坏，因为如果其他处理器仍在使用该磁盘，会导致损坏！）

`boot` 对其可加载的对象文件施加了一些限制。它仅接受 HP-UX 魔数 `EXECMAGIC` (0407)、`SHAREMAGIC` (0410) 和 `DYNAMICMAGIC` (0413)。参见 `magic(4)`。对象文件必须包含 `HPUX AUX_ID` 类型的辅助标头，并且它必须是第一个辅助标头（参见 `a.out(4)`）。

## ll 和 ls 操作

`ll` 和 `ls` 操作列出由可选 `devicefile` 指定的 HP-UX 目录的内容。输出类似于 `ls -afl` 命令的输出，但不打印日期信息。

默认的 `devicefile` 的生成方式与 `boot` 相同，默认为当前目录。

### set autoofile 操作

`set autoofile` 操作用指定的字符串覆盖自动执行文件 `autoofile` 的内容（参见“示例”部分中的 `autoexecute`）。

### show autoofile 操作

`show autoofile` 操作显示自动执行文件 `autoofile` 的内容（参见“示例”部分中的 `autoexecute`）。

## 诊断信息

如果遇到错误，`hpux` 会打印诊断消息以指示错误原因。这些消息分为通用、引导、复制、配置和系统调用类别。系统调用错误消息在 `errno(2)` 中描述。其余消息列于下方。

### 通用

-   **devicefile 规范中的次要设备号无效**
    `devicefile` 规范中的次要设备号无法识别。

-   **devicefile 规范中的路径无效**
    `devicefile` 规范中的硬件路径无法识别。

-   **命令过于复杂，无法解析**
    命令行包含过多的参数。

-   **devicefile 规范中缺少路径**
    `devicefile` 规范需要（但不包含）硬件路径组件。

-   **panic (in hpxkboot): (display=#number, flags=#number) string**
    发生了严重的内部 `hpx` 错误。请报告给您最近的 HP 现场代表。

### 引导

-   **魔数无效**
    指定的对象文件没有可识别的魔数。

-   **flags 规范中的数字无效**
    无法识别 `-f` 选项中的 flags 规范数字。

-   **Exec failed: Cannot find /stand/venux or /venux**
    找不到 `/stand/venux` 或 `/venux`。

-   **从原始字符设备引导**
    在从原始设备引导时，指定的管理器仅具有字符接口，如果块大小不正确，这可能会导致问题。

-   **is1 不存在，请按系统 RESET 按钮以继续**
    失败的引导操作在内存中覆盖了 `is1`。无法将控制权交还给 `is1`。

-   **短读**
    指定的对象文件内部不一致；长度不足。

-   **将覆盖**
    加载指定的对象文件将覆盖 `hpx`。

### 配置

-   **无法添加路径，错误编号**
    在将硬件路径添加到 I/O 树时发生了未知错误。给出了内部错误编号。请联系您的 HP 现场代表。

-   **设备倒卷错误**
    在尝试倒卷设备时遇到错误。

-   **跳过文件错误**
    在尝试对磁带设备进行向前定位时遇到错误。

-   **跳过计数为负数**
    如果指定了跳过计数，其值必须大于或等于零。

-   **无主要设备号**
    指定的管理器在块设备或字符设备切换表中没有条目。

-   **路径与另一路径不兼容**
    指定了多个不兼容的硬件路径。

-   **路径过长**
    指定的硬件路径对于指定的管理器而言组件过多。

-   **路径过短**
    指定的硬件路径对于指定的管理器而言组件过少。

-   **表已满**
    指定给 `hpux` 的设备过多。

## 示例

作为以下示例的引言，这里简要概述了 HP-UX 系统引导序列。

### 自动引导

各种 HP-UX 系统上的自动引导过程遵循相似的通用序列。当 HP-UX 系统处理器通电或按下系统重置按钮时，将执行处理器相关代码（固件）以验证硬件和系统整体完整性（参见 `pdc(8M)`）。检查硬件后，`pdc` 为用户提供通过按下 Esc 键来覆盖自动序列的选项。此时，控制台上通常会显示类似以下的消息。

```
(c) Copyright. Hewlett-Packard Company. 1994.
All rights reserved.

PDC ROM rev. 130.0
32 MB of memory configured and tested.

Selecting a system to boot.
To stop selection process, press and hold the ESCAPE key...
```

如果未检测到键盘活动，`pdc` 将通过加载 `isl`（参见 `isl(8M)`）并转移控制权给它来启动自动引导序列。由于正在发生自动引导序列，`isl` 找到并执行自动引导文件，该文件在 HP-UX 系统上要求以适当参数运行 `hpux`。`isl` 在控制台上显示类似以下的消息：

```
Booting from: scsi 6 HP 2213A
Hard booted.
Fsi Revision A.02.D9 March 27, 1990
Isl booting hpux boot disk:/0;/stand/vmunix
```

`hpux`，即二级系统加载器，随后宣布其正在执行的操作，在此情况下为 `boot`，加载映像的来源 `devicefile`，以及加载映像的 TEXT 大小、DATA 大小、BSS 大小和起始地址，如下所示，然后将控制权传递给映像。

```
Booting disk(scsi,6:0)/stand/wnunix
96561e+197312+43948a start 0xc6:50
```

加载的映像随后显示大量的配置和状态消息。

### 交互引导

要以交互方式使用 `hpxux`，必须在 `pdc` 允许的间隔内按下 Esc 键以交互模式启动 `is1`。`pdc` 然后搜索并显示所有可引导设备，并提供一组引导选项。如果选择了适当的选项，`pdc` 将加载 `is1`，`is1` 将交互式地提示输入命令。显示类似以下的信息：

```
Selection process stopped.

Searching for Potential Boot Devices.
To terminate search, press and hold the ESCAPE key.

Device Selection    Device Path          Device Type
-------------------------------------------------------------------------------
    p0                  scsi.6.0            QUANTUM PD210S
    p1                  scsi.1.0            NP          2213A
    p2                  lan.ffffff-ffffff.f.f   fhoLBooT

b) Boot from specified device
a) Search for bootable devices
x) Enter Boot Administration Mode
k) Exit and continue boot sequence

Select from menu: b p0 is1

Trying scsi.6.0
Boot path initialized.
Attempting to load p0

Hard booted.
FSL Revision A.00.2G Mar 27, 1994
IS1...
```

尽管 `hpxux` 的所有操作和选项都可以从 `is1` 交互式使用，但也可以从自动执行文件中执行。在下面的示例中，用户输入是显示在每个 `IS1:` 提示后的该行剩余部分。每个示例的其余部分是系统显示的文字。在回顾 `hpxux` 各种选项和操作的具体示例之前，以下是自动引导过程中采取步骤的概述。尽管所示的硬件配置和引导路径针对单台 Series 800 机器，但所有型号的用户界面都是一致的。当按下系统重置按钮时，`pdc` 执行自检，假设硬件测试通过，`pdc` 宣布自身，向控制终端发送 BELL 字符，并给用户 10 秒钟的时间通过输入任何字符来覆盖自动引导序列。控制台上显示类似以下的文本：

```
Processor Dependent Code (PDC) revision 1.2
Duplex Console IO Dependent Code (IODC) revision 3

Console path            = 56.0.0.0.0.0.0.0 (dec)
                          38.0.0.0.0.0.0.0 (hex)

Primary boot path       = 44.3.0.0.0.0.0.0 (dec)
                          2c.00000003.0.0.0.0.0 (hex)
```
