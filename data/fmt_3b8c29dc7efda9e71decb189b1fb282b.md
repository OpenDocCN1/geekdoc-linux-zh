

```
init 2
```

同样，命令 `init 6` 将在不向用户发出任何警告的情况下停止并重新启动系统。这不会损害系统，但如果在生产系统上使用，可能会损害你在用户眼中的声誉。在关闭过程中，系统会通过 TERM 信号要求所有进程终止。如果失败，则会用 KILL 信号将其杀死。此外，`sync` 原语会使磁盘与缓冲区同步，以确保不会丢失数据。

一旦系统被带到停止状态，安全地关闭电源。系统将无法响应控制台或任何远程连接的情况会时有发生。在这些情况下，可能需要循环电源以重新获得访问权限。在某些系统上，有一个专门的按钮用于此操作，标记为 TOC。在许多现代 UNIX 系统上，电源开关会在切断系统电源之前激活固件版本的磁盘同步程序。这一改进大大提高了从手动关闭中恢复的可能性。

## UNIX 启动和关闭策略

在大多数情况下，你不应允许普通用户启动、重新启动或关闭系统。原因之一是，用户无法运行 `reboot`、`init` 或 `shutdown` 命令；只有超级用户才能执行它们。此外，在安全性重要的情况下，正在重新启动的系统可能容易受到攻击。如果你禁止用户重新启动，你就可以对重新启动的系统持怀疑态度。最后，也是最重要的是，用户不太可能确定单个工作站在整个网络中的作用。他们关闭的系统可能有会计办公室打印机用的打印服务器，老板的

表 3.3 Windows 2000 启动文件

| 文件 | X86 位置 | RISC 位置 |
|---|---|---|
| `NTLDR` | 系统分区根目录 | - |
| `boot.ini` | 系统分区根目录 | - |
| `BOOTSECT.DOS` | 系统分区根目录 | - |
| `NTDETECT.COM` | 系统分区根目录 | - |
| `NTBOOTDD.SYS` | 系统分区根目录 | - |
| `NTOSKRNL.EXE` | `SystemRoot\System32` | `SystemRoot\System32` |
| `OSLOADER.EXE` | - | `OS\nt40` |
| `HAL.DLL` | `SystemRoot\System32` | `OS\nt40` |
| `*.pal` (ALPHA) | - | `OS\nt40` |
| `System` | `SystemRoot\System32\Config` | `SystemRoot\System32\Config` |
| `Device Drivers` | `SystemRoot\System32\Drivers` | `SystemRoot\System32\Drivers` |

在此情况下，了解每个文件的含义和功能就变得很重要了。

表 3.3 列出了成功启动 Windows 2000 所需的文件，以及每个文件的相应位置。

## `NTLDR`

`NTLDR` 位于系统分区的根目录下，并由启动驱动器上的引导扇区自动加载。`NTLDR` 控制 Windows 2000 系统的启动过程。此程序在基于 RISC 的系统上不是必需的。基于 RISC 的系统的固件执行 `NTLDR` 的功能。

## `BOOT.INI`

`boot.ini` 是 `NTLDR` 访问的第一个文件。它是一个简单的文本文件，提供可用操作系统的列表。本章后面将对 `boot.ini` 进行更详细的描述。此文件在基于 RISC 的系统上既不是必需的也不包含在内。

## `BOOTSECT.DOS`

`BOOTSECT.DOS` 包含 DOS 引导扇区的副本，该扇区以前驻留在启动驱动器上。如果机器同时包含 Windows 2000 和 DOS 安装，则此文件才存在，并且会在两者之间双启动。如果用户选择启动 DOS，`NTLDR` 将访问此文件。此文件在基于 RISC 的系统上既不是必需的也不包含在内。

## `NTDETECT.COM`

`NTLDR` 使用 `NTDETECT.COM` 来检测 Windows 2000 系统上存在的硬件。`NTDETECT.COM` 仅在基于 x86 的系统上是必需的；在基于 RISC 的系统上不包含。

## `NTBOOTDD.SYS`

`NTBOOTDD.SYS` 在基于 x86 的系统上是必需的，这些系统从没有板载 BIOS 的 SCSI 控制器启动，或其板载 BIOS 已被禁用。`NTBOOTDD.SYS` 只是系统 SCSI 控制器的相应驱动程序的副本。此文件在基于 RISC 的系统上既不是必需的也不包含在内。

## `NTOSKRNL.EXE`

`NTOSKRNL.EXE` 是 Windows 2000 内核。Windows 2000 内核是操作系统的核心和灵魂，正如所有操作系统的内核一样。它位于基于 x86 和基于 RISC 系统的启动分区上。`NTOSKRNL.EXE` 加载硬件抽象层，即 HAL，并开始加载设备驱动程序和系统服务的过程。

## `OSLOADER.EXE`

`OSLOADER.EXE` 仅在基于 RISC 的系统上是必需的。它执行到加载内核为止的所有功能，以及加载 HAL 和所需的任何 `*.pal` 文件。

## `HAL.DLL`

NT 使用 HAL 将特定于平台的问题对 Windows 2000 隐藏起来。HAL 使 Windows 2000 能够使用相同的系统调用与各种硬件平台通信。HAL 将这些高级系统调用翻译成低级硬件例程。Windows 2000 开箱即用时包含大多数系统的 HAL。然而，一些专有系统可能需要定制的 HAL 文件，该文件将由硬件供应商提供。如果 Windows 2000 在系统设置期间无法为您的硬件找到合适的 HAL，您将被提示通过软盘提供专有 HAL。

## `*.PAL` FILES

- `.pal` 文件包含仅用于基于 ALPHA 的 RISC 平台的硬件特定代码。

## `SYSTEM`

`System` 文件包含 Windows 2000 注册表的系统配置单元。系统配置单元包含完成启动过程所需的驱动程序和服务信息。

## `DRIVERS`

`Drivers` 文件夹包含支持 Windows 2000 系统上安装的硬件所需的所有驱动程序文件。

## THE WINDOWS 2000 PRE-BOOT PROCESS

- 在 Windows 2000 甚至开始启动之前，系统必须启动并执行其自身的一组例程。预启动过程中的主要参与者是 BIOS，即基本输入输出系统。BIOS 是一个非常简单的操作系统，存储在系统板上的闪存中。BIOS 负责在系统硬件和操作系统之间提供一个基础的通信通道。

预启动过程的第一阶段是上电自检，即 POST 例程。BIOS 执行此例程并执行诸如内存测试、中断测试以及键盘和鼠标控制器和内置磁盘控制器等基本硬件的测试等功能。如果 POST 例程因任何原因失败，系统将无法启动，直到您采取纠正措施为止。

在 POST 例程成功完成后，BIOS 定位启动设备，通常是固定磁盘。它将主引导记录 MBR 加载到内存中并执行 MBR 中包含的程序。活动分区由 MBR 程序扫描分区引导记录表来定位。

此时，活动分区的引导扇区被加载到内存中。在 Windows 2000 的情况下，引导扇区包含 `NTLDR`，它被加载并初始化。这就是引导过程真正开始的地方。

## THE WINDOWS 2000 BOOT PROCESS

`NTLDR` 程序是引导过程的第一步。我们将在本节中重点介绍 x86 系统的引导。如果您想了解有关引导 RISC 系统的更多信息，我们建议您购买 Microsoft Press 参考指南之一，例如 Windows 2000 Beta Training Kit。

`NTLDR` 首先将处理器切换到 32 位平坦内存模式（386 模式）。接下来，`NTLDR` 启动内置的简单文件系统驱动程序以访问操作系统。此时，`NTLDR` 可能会访问 `NTBOOTDD.SYS`（在不太可能使用没有 BIOS 的 SCSI 控制器时）以从 SCSI 设备启动。一旦 `NTLDR` 获得了文件系统的访问权限，它就会检查 `boot.ini` 文件以确定系统上有哪些操作系统。`boot.ini` 文件包含每个操作系统的条目，指定其在系统上的位置。有关 `boot.ini` 文件的详细描述以及修改它的说明将在本章后面给出。以下示例 `boot.ini` 包含 Windows 2000 和 DOS 的条目：

```
[boot loader]

timeout=30

default=multi(0)disk(0)rdisk(0)partition(1)\WINNT

[operating systems]

multi(0)disk(0)rdisk(0)partition(1)\WINNT="Microsoft Windows 2000 Server" /fastdetect

C:\="Microsoft MS-DOS 6.22"
```

一旦 `NTLDR` 检查了 `boot.ini` 文件，它就会向用户呈现一个屏幕，允许选择其中一个已安装的操作系统。如果 Windows 2000 是唯一已安装的操作系统，则不会显示选择屏幕。如果用户在指定的超时时间内未选择操作系统（默认为 30 秒），`NTLDR` 将选择默认值。如果用户选择的操作系统不是 Windows 2000，`NTLDR` 将加载并运行 `BOOTSECT.DOS` 并将控制权交还给该操作系统。

