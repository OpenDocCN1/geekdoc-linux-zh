
```text
psm0: <PS/2 Mouse> irq 12 on atkbdc0
psm0: model Generic PS/2 mouse, device ID 0
fdc0: <NEC 72065B or clone> at port 0x3f0-0x3f5,0x3f7 irq 6 drq 2 on isa0
fdc0: FIFO enabled, 8 bytes threshold
fd0: <1440-KB 3.5" drive> on fdc0 drive 0
```

内核还找到了软盘控制器和软盘驱动器。`fdc0` 是软盘控制器的设备名称，而 `fd0` 是软盘驱动器本身的设备名称。(`fd0` 类似于 Windows/DOS 中的 A:。它是你在想要访问此设备时使用的设备名称。)

下一条消息显示内核已找到 SoundBlaster AWE 64 声卡，并给出了该卡正在使用的资源信息：

```text
sbc0: <Creative SB AWE64> at port 0x220-0x22f,0x330-0x331,0x388-0x38b
irq 5 drq 1,5 on isa0
pcm1: <SB16 DSP 4.16> on sbc0
```

请注意，在这种情况下，`sbc0` 实际上是声卡相关设备组的名称。声卡使用多个设备，具体取决于你要访问哪些功能，包括 `dsp`（WAV 和 MP3 文件等输出的位置）和 `mixer`（控制各种音频设备的音量）。

你在启动消息中还可能会看到以下部分行：

- unknown: <PNP0033> can't assign resources

- unknown: <PNP0F13> can't assign resources

- unknown: <PNP0501> can't assign resources

- unknown: <PNP0700> can't assign resources

- unknown: <PNP0401> can't assign resources

- unknown: <PNP0501> can't assign resources

这些行表明内核在系统中找到了一些“即插即用”（通常缩写为 PnP）设备，但它不了解这些设备，且无法为它们分配资源。这些消息是无害的。如果你不喜欢看到它们，请注意，正如 FreeBSD FAQ 所说，“FreeBSD 项目将乐意通过 send-pr 接受驱动程序贡献。”（这是给那些擅长编写设备驱动程序的 C 大师们的。）

下一条消息显示内核已找到硬盘，并提供了关于硬盘的各种信息，包括设备名称、容量、制造商和型号、几何参数以及硬盘所在的控制器：

- `ad0`: 19473MB <Maxtor 92049U6> [39566/16/63] at `ata0-master` UDMA33

- `ad1`: 14664MB <IBM-DJNA-351520> [29795/16/63] at `ata0-slave` UDMA33

它还告诉你硬盘使用的访问模式。在这种情况下，两个硬盘都使用 Ultra DMA 33。（这将在第18章“理解硬盘和文件系统”中更详细地讨论。）

最后一条消息显示内核已挂载根文件系统：

Mounting root from `ufs:/dev/ad0s1a`

挂载根文件系统后，内核将控制权交给一个名为 `init` 的进程。浅灰色的消息是由在 `init` 阶段发生的事件触发的。你可以通过颜色来区分内核消息和非内核消息。内核消息显示为白色；非内核消息显示为浅灰色。

## init

`init` 程序是操作系统下运行的第一个实际进程，因此其进程 ID 为 1。`init` 负责启动构成完全功能操作系统的其他所有进程；为此，它必须先确定磁盘是否处于良好状态。

当 FreeBSD 系统正确关机时，它会在每个磁盘上运行一个名为 `sync` 的程序，以确保所有数据已写出，卸载文件系统，然后设置文件系统的“干净”标志。这类似于 Windows 关机时经过的过程。如果 FreeBSD 系统未正确关机，干净标志将不会被设置。

## 文件系统一致性检查

`init` 做的第一件事之一是检查是否设置了干净标志。如果已设置，`init` 会挂载文件系统以供使用。如果未设置，`init` 会先在文件系统上运行 `fsck` 程序，以确保其未受损。该程序会修复它发现且知道如何修复的任何损坏。`fsck` 类似于 Windows 中的 Scandisk 程序，此过程类似于你在不当关机后重启 Windows 时看到的“系统未正常关闭”程序。如果 `fsck` 在此时遇到无法修复的错误，它会将系统置于单用户模式，以便系统管理员（如果你正在阅读这本书，那很可能就是你）可以手动进行必要的修复。

假设干净标志已设置，或者如果标志未设置，`fsck` 能够修复损坏，`init` 接下来会挂载在 `/etc/fstab` 文件中列出的每个设置了启动时挂载标志的文件系统（参见第8章“FreeBSD 文件系统”中的“理解 /etc/fstab 文件”）。

> **提示**
>
> 如果需要，你也可以手动运行 `fsck`。关于 `fsck` 及其各种选项的更多信息可在第8章中找到。从 FreeBSD 5.0 开始，文件系统一致性检查将在后台运行，因此你不再需要等到它完成才能使用系统。

## 系统配置脚本

在文件系统挂载后，`init` 读取位于 `/etc` 和 `/etc/defaults` 中的系统配置脚本（也称为 *Run Control* 或 *Resource Configuration* 脚本，缩写为 *rc* 脚本）。此外，`init` 检查 `/usr/local/etc/rc.d` 目录中是否有任何应在启动时运行的额外脚本（这些可能是启动 Web 服务器、数据库服务器或你希望在启动时自动运行的任何其他程序的脚本）。如果你熟悉 Windows 和/或 DOS，这部分启动过程类似于 `config.sys`、`autoexec.bat`、`system.ini` 以及控制 Windows 启动选项的注册表部分。

> **注意**
>
> `rc` 脚本这一术语实际上源自 MIT 的 CTSS 系统中的 RunCom，即“运行命令”，大约在 1965 年。虽然缩写 `rc` 自那时起已被重新分配给许多不同的含义，但其一般应用保持不变：一组存储在文件中并批量执行的命令。在典型的 Unix 术语中，`rc` 本身的含义足够清晰，以至于不需要知道它代表什么，大多数人也不知道。

> 本书将在 Sun 风格的运行级别中称为 *Run Control*，而在 FreeBSD 自己的启动脚本中称为 *Resource Configuration*。

> **注意**
>
> 为了完整性，应该提到 `init` 还会检查并读取一个名为 `/etc/rc.local` 的文件，该文件可用于启动诸如 Web 服务器等程序。然而，此文件已弃用，在 FreeBSD 的未来版本中可能不再受支持。因此，建议将你的启动脚本放在 `/usr/local/etc/rc.d` 目录中，而不是 `/etc/rc.local` 文件中。

### BSD 与 Sys V 运行控制

如果你来自 Sys V Unix 背景，读完上一节可能会感到有点困惑。所以，这里是一个澄清：在 BSD `init` 中，运行级别的概念并不真正存在。你基本上只有单用户模式和带有网络支持的多用户模式。Sys V 运行级别中那种没有网络支持的多用户模式在这里是不存在的。此外，BSD 中没有像 Sys V 中那样的 `inittab` 文件。另外，启动选项主要由一个名为 `rc.conf` 的文件控制。不像 Sys V 中那样，没有针对不同运行级别目录中带有链接的独立文件来启动大多数服务。（你将在第10章中了解更多关于 `init` 的内容。）

## getty 和 login

读取运行控制脚本后，`init` 在控制台（以及多个虚拟终端）上启动一个程序。这个程序通常是 `getty` 程序，但不一定。另一个常用于替代 `getty` 的常见程序是 `xdm`，它在系统启动后立即启动 X-Windows 系统的图形登录会话（类似于 NT 登录会话）。要启动的程序在文件 `/etc/ttys` 中定义。就本次讨论而言，我们假设它是 `getty` 程序。

`getty` 程序初始化终端（或控制台），并控制各种安全选项和终端类型选项。再次强调，这些选项及其值在 `/etc/ttys` 中定义。然后 `getty` 程序启动 `login` 程序来验证你的登录名和密码。

## 登录到 FreeBSD

在所有启动过程完成后，你会看到一个类似于这样的屏幕：

```text
FreeBSD/1386 (amnesiac) (tty p0)

login:
```

假设你在安装过程中没有配置任何网络信息，系统的默认主机名是 "amnesiac"。输入你在安装期间为自己创建的普通用户（而非 `root` 用户）的登录名。按 Enter 键，然后当提示时，输入你设置给自己的密码。注意，密码将

不会在屏幕上显示。实际上，屏幕上什么也不会显示。别担心，你的密码正在被读取。
