
- **9.** 文件`data.txt`需要按数字排序，并将其输出保存到新文件`newdata.txt`中。以下哪些命令可以完成此任务？（选择所有适用的选项。）
  - A. `sort -n -o newdata.txt data.txt`
  - B. `sort -n data.txt > newdata.txt`
  - C. `sort -n -o data.txt newdata.txt`
  - D. `sort -o newdata.txt data.txt`
  - E. `sort data.txt > newdata.txt`

- **10.** 以下哪些命令可以将`data.txt`和`datatoo.txt`文件的内容按顺序显示到`STDOUT`？（选择所有适用的选项。）
  - A. `ls data.txt datatoo.txt`
  - B. `sort -n data.txt > datatoo.txt`
  - C. `cat -n data.txt datatoo.txt`
  - D. `ls -l data.txt datatoo.txt`
  - E. `sort data.txt datatoo.txt`

- **11.** 文本文件`StarGateAttacks.txt`需要进行特殊格式化以便审阅。以下哪个命令是快速完成此任务的最佳命令？
  - A. `printf`
  - B. `wc`
  - C. `pr`
  - D. `paste`
  - E. `nano`

- **12.** 你需要将字符串`42.777`格式化为正确的两位小数浮点数。以下哪个`printf`命令的`FORMAT`设置是正确使用的方式？
  - A. `"%s\n"`
  - B. `"%.2s\n"`
  - C. `"%d\n"`
  - D. `"%.2c\n"`
  - E. `"%.2f\n"`

- **13.** 一个`Unicode`编码的文本文件`MyUnicode.txt`需要被查看。在决定使用什么实用程序查看文件内容之前，你对其使用了`wc`命令。该实用程序向`STDOUT`显示`2020 6786 11328`。以下哪项是正确的？（选择所有适用的选项。）
  - A. 该文件有 2,020 行。
  - B. 该文件有 2,020 个字符。
  - C. 该文件有 6,786 个单词。
  - D. 该文件有 11,328 个字符。
  - E. 该文件有 11,328 行。

- **14.** 以下哪项最能定义文件描述符？
  - A. 代表文件类型的字母
  - B. 代表进程打开文件的数字
  - C. 文件名的另一种说法
  - D. 代表标准输出的六个字符名称
  - E. 指示文件分类的符号

- **15.** 默认情况下，`STDOUT`流向哪个项目？
  - A. `/dev/tty`，其中`n`是一个数字
  - B. `/dev/null`
  - C. `>`
  - D. `/dev/tty`
  - E. `pwd`

- **16.** 以下哪个命令可以将文件`SpaceOpera.txt`显示到输出，同时将其副本保存到文件`SciFi.txt`中？
  - A. `cat SpaceOpera.txt | tee SciFi.txt`
  - B. `cat SpaceOpera.txt > SciFi.txt`
  - C. `cat SpaceOpera.txt 2> SciFi.txt`
  - D. `cp SpaceOpera.txt SciFi.txt`
  - E. `cat SpaceOpera.txt && SciFi.txt`

- **17.** 以下哪个命令将生成的任何错误消息都放入黑洞？
  - A. `sort SpaceOpera.txt 2> BlackHole`
  - B. `sort SpaceOpera.txt && BlackHole`
  - C. `sort SpaceOpera.txt > BlackHole`
  - D. `sort SpaceOpera.txt 2> /dev/null`
  - E. `sort SpaceOpera.txt > /dev/null`

- **18.** 以下哪个命令将确定文件`Problems.txt`中有多少条记录包含单词`error`？
  - A. `grep error Problems.txt | wc -b`
  - B. `grep error Problems.txt | wc -w`
  - C. `grep error Problems.txt | wc -l`
  - D. `grep Problems.txt error | wc -w`
  - E. `grep Problems.txt error | wc -l`

- **19.** 你想找到名为`42.tmp`的任何文件，该文件存在于当前目录的树结构中，并将其内容显示到`STDOUT`。以下哪些允许你构建一个命令来做到这一点？（选择所有适用的选项。）
  - A. `xargs (find . -name 42.tmp) cat`
  - B. `cat \`find . -name 42.tmp\``
  - C. `cat $(find . -name 42.tmp)`
  - D. `cat {find . -name 42.tmp}`
  - E. `find . -name 42.tmp | xargs cat`

- **20.** 你想编辑文件`SpaceOpera.txt`并决定使用`vim`编辑器来完成此任务。以下哪些是你可能会使用的`vim`模式？（选择所有适用的选项。）
  - A. `Insert`
  - B. `Change`
  - C. `Command`
  - D. `Ex`
  - E. `Edit`

## 系统启动和配置

### 第二部分

![](img/c0a399aca0d18f8822d714ad0a173123_196_0.png)

## 第 5 章：解释启动过程

- 目标 1.1：总结 `Linux` 基础知识。

![](img/c0a399aca0d18f8822d714ad0a173123_198_0.png)

![](img/c0a399aca0d18f8822d714ad0a173123_199_0.png)

本章检查 `Linux` 系统中的启动和初始化过程。首先，我们将查看计算机固件在启动过程中所起的作用，然后讨论 `Linux` 引导加载程序以及如何配置它们。接下来，本章讨论了 `Linux` 初始化过程，展示 `Linux` 如何决定在启动时启动哪些后台应用程序。本章最后介绍了一些可用于帮助挽救无法启动的系统的系统恢复选项。

### `Linux` 启动过程

当你打开 `Linux` 系统的电源时，它会触发一系列事件，最终导致登录提示符。通常，你不需要担心这些事件背后发生了什么；你只需登录并开始使用你的应用程序。

然而，有时你的 `Linux` 系统可能没有完全正确地启动，或者你期望在后台运行的应用程序可能没有运行。在这种情况下，了解 `Linux` 如何启动操作系统并启动程序有助于你解决问题。

以下部分逐步说明启动过程的步骤，以及你如何监视启动过程以查看哪些步骤失败了。

### 跟踪启动过程

`Linux` 启动过程可以分为三个主要步骤：

1. 工作站固件启动，执行硬件的快速检查（称为加电自检，或 `POST`），然后在可引导设备上查找引导加载程序。
2. 引导加载程序运行，并确定要加载哪个 `Linux` 内核程序。
3. 内核程序加载到内存中，并启动系统运行所需的后台程序（例如桌面环境的图形桌面管理器或服务器的 `Web` 和数据库服务器）。

虽然从表面上看，这三个步骤可能显得简单，但一系列操作协同工作以保持启动过程运行。每个步骤都会执行多个操作，为你的系统运行 `Linux` 做准备。

## 查看引导过程

你可以通过在系统引导时监视系统控制台屏幕来监控 `Linux` 引导过程。当系统检测硬件和加载软件时，你会看到许多信息性消息滚动经过。

某些图形桌面版 `Linux` 发行版在启动时会将引导消息隐藏在一个单独的控制台窗口中。通常，你可以按下`Esc`键或`Ctrl+Alt+F1`键组合来查看这些消息。

通常，引导消息滚动得很快，很难看清发生了什么。如果你需要排查引导问题，可以使用`dmesg`命令查看引导时消息。大多数 `Linux` 发行版会将引导内核消息复制到内存中的一个特殊环形缓冲区，称为`kernel ring buffer`（内核环形缓冲区）。该缓冲区是循环的，并设置为预定的大小。随着新消息记录在缓冲区中，旧消息会被轮换出去。

`dmesg` 命令显示当前存储在内核环形缓冲区中的最新引导消息，如图 5.1 所示。

### 列表 5.1 `Ubuntu` 工作站上 `dmesg` 命令的输出

```bash
$ dmesg
[    0.000000] Linux version 5.11.0-40-generic (buildd@lgw01-amd64-010) (gcc (Ubuntu 9.3.0-17ubuntu1~20.04) 9.3.0, GNU ld (GNU Binutils for Ubuntu) 2.34) #44~20.04.2-Ubuntu SMP Tue Oct 26 18:07:44 UTC 2021 (Ubuntu 5.11.0-40.44~20.04.2-generic 5.11.22)
[    0.000000] Command line: BOOT_IMAGE=/boot/vmlinuz-5.11.0-40-generic root=UUID=5423117e-4aaf-4416-ada7-01e07073b2e1 ro quiet splash
[    0.000000] KERNEL supported cpus:
[    0.000000]   Intel GenuineIntel
[    0.000000]   AMD AuthenticAMD
[    0.000000]   Hygon HygonGenuine
[    0.000000]   Centaur CentaurHauls
[    0.000000]   Shaoin  Shaogirl
[    0.000000] x86/fpu: Supporting XSAVE feature 0x001: 'x87 floating point registers'
[    0.000000] x86/fpu: Supporting XSAVE feature 0x002: 'SSE registers'
[    0.000000] x86/fpu: Supporting XSAVE feature 0x004: 'AVX registers'
[    0.000000] x86/fpu: xstate_offset[2]:  576, xstate_sizes[2]:  256
[    0.000000] x86/fpu: Enabled xstate features 0x7, context size is 832 bytes, using 'standard' format.
[    0.000000] BIOS-provided physical RAM map:
[    0.000000] BIOS-e820: [mem 0x0000000000000000-0x0000000000000fff] usable
[    0.000000] BIOS-e820: [mem 0x000000000009fc00-0x000000000009ffff] reserved
[  0.000000] BIOS-e820: [mem 0x000000000000f000-0x00000000000fffff] reserved
[  0.000000] BIOS-e820: [mem 0x00000000010000-0x0000000000dfffff] usable
[  0.000000] BIOS-e820: [mem 0x00000000df0000-0x00000000dffffff] ACPI data
[  0.000000] BIOS-e820: [mem 0x00000000fec00000-0x00000000fec00fff] reserved
[  0.000000] BIOS-e820: [mem 0x00000000fee00000-0x00000000fee00fff] reserved
[  0.000000] BIOS-e820: [mem 0x00000000ffcc0000-0x00000000ffffffff] reserved
[  0.000000] BIOS-e820: [mem 0x0000000100000000-0x000000021ffffff] usable
[  0.000000] NX (Execute Disable) protection: active
[  0.000000] SMBIOS 2.5 present.
[  0.000000] DMI: innotek GmbH VirtualBox/VirtualBox, BIOS VirtualBox 12/01/2006
[  0.000000] Hypervisor detected: KVM
[  0.000000] kvm-clock: Using msrs 4b564d01 and 4b564d00
[  0.000000] kvm-clock: cpu 0, msr 109001001, primary cpu clock
[  0.000000] kvm-clock: using sched offset of 3933158608 cycles
[  0.000001] clocksource: kvm-clock: mask: 0xfffffffffffffffx max_cycles: 0x1cd424ed4ffb, max_idle_ns: 881590591483 ns
[  0.000003] tsc: Detected 1497.589 Mhz processor
```

大多数 `Linux` 发行版还将引导消息存储在日志文件中，通常位于`/var/log`文件夹中。对于基于 `Debian` 和基于 `Red Hat` 的系统，该文件通常是`/var/log/boot.log`，但一些旧版 `Linux` 系统可能使用`/var/log/boot`。

虽然能够看到引导期间生成的不同消息很有帮助，但了解是什么生成了这些消息也很有用。本章将讨论这三个引导步骤中的每一个，并通过一些示例展示其工作原理。

## 固件启动

所有兼容 `IBM` 的工作站和服务器都使用某种内置固件来控制已安装操作系统的启动方式。在较旧的工作站和服务器上，这种固件被称为`Basic Input/Output System (BIOS)`（基本输入/输出系统）。在较新的工作站和服务器上，一种称为`Unified Extensible Firmware Interface (UEFI)`（统一可扩展固件接口）的方法维护系统硬件状态并启动已安装的操作系统。

### `BIOS` 启动

`BIOS` 固件有一个简单的菜单界面，允许你更改某些设置以控制系统如何查找硬件，并定义 `BIOS` 应使用哪个设备来启动操作系统。

原始 `BIOS` 固件的一个局限性是它只能从硬盘读取一个扇区的数据到内存中运行。这不足以加载整个操作系统。为了绕过这一限制，大多数操作系统（包括 `Linux` 和 `Microsoft Windows`）将引导过程分为两部分。

首先，`BIOS` 运行一个`bootloader`（引导加载程序）程序，这是一个小型程序，用于初始化必要的硬件以查找并运行完整的操作系统程序。它通常位于同一硬盘上的另一个位置，但有时位于单独的内部或外部存储设备上。

引导加载程序通常有一个配置文件，因此你可以告诉它在哪里找到要运行的实际操作系统文件，甚至生成一个小型菜单，允许用户在多个操作系统之间进行引导选择。

为了开始引导过程，`BIOS` 必须知道在已安装的存储设备上哪里可以找到引导加载程序。大多数 `BIOS` 设置允许你从几个位置加载引导加载程序：

- 内部硬盘
- 外部硬盘
- `CD` 或 `DVD` 驱动器
- `USB` 内存棒
- `ISO` 文件
- 使用 `NFS`、`HTTP` 或 `FTP` 的网络服务器

从硬盘引导时，你必须指定硬盘以及硬盘上的分区，以便 `BIOS` 从中加载引导加载程序。这是通过定义`Master Boot Record`（主引导记录，`MBR`）来完成的。

`MBR` 是系统第一个硬盘分区上的第一个扇区。计算机系统只有一个 `MBR`。`BIOS` 查找 `MBR` 并将存储在那里的程序读入内存。由于引导加载程序必须容纳在一个扇区中，它必须非常小，因此不能做太多事情。引导加载程序主要指向实际操作系统内核文件的位置，该文件存储在安装在系统的单独分区的引导扇区中。内核引导文件没有大小限制。

![](img/c0a399aca0d18f8822d714ad0a173123_202_0.png)

引导加载程序不需要直接指向操作系统内核文件；它可以指向任何类型的程序，包括另一个引导加载程序。你可以创建一个初级引导加载程序，它指向一个次级引导加载程序，后者提供加载多个操作系统的选项。这个过程被称为`chainloading`（链式加载）。

### `UEFI` 启动

随着操作系统变得更加复杂，显然需要开发一种新的引导方法。

`Intel` 于 1998 年创建了`Extensible Firmware Interface`（`EFI`，可扩展固件接口）来解决 `BIOS` 的一些局限性。到 2005 年，这一想法在其他供应商中流行起来，`Universal EFI (UEFI)` 规范被采纳为标准。如今，几乎所有兼容 `IBM` 的桌面和服务器系统都使用 `UEFI` 固件标准。
[/content]
</think>

[content]
- **9.** 文件`data.txt`需要按数字排序，并将其输出保存到新文件`newdata.txt`中。以下哪些命令可以完成此任务？（选择所有适用的选项。）

  - A. `sort -n -o newdata.txt data.txt`
  - B. `sort -n data.txt > newdata.txt`
  - C. `sort -n -o data.txt newdata.txt`
  - D. `sort -o newdata.txt data.txt`
  - E. `sort data.txt > newdata.txt`

- **10.** 以下哪些命令可以将`data.txt`和`datatoo.txt`文件的内容按顺序显示到`STDOUT`？（选择所有适用的选项。）

  - A. `ls data.txt datatoo.txt`
  - B. `sort -n data.txt > datatoo.txt`
  - C. `cat -n data.txt datatoo.txt`
  - D. `ls -l data.txt datatoo.txt`
  - E. `sort data.txt datatoo.txt`

- **11.** 文本文件`StarGateAttacks.txt`需要进行特殊格式化以便审阅。以下哪个命令是快速完成此任务的最佳命令？

  - A. `printf`
  - B. `wc`
  - C. `pr`
  - D. `paste`
  - E. `nano`

- **12.** 你需要将字符串`42.777`格式化为正确的两位小数浮点数。以下哪个`printf`命令的`FORMAT`设置是正确使用的方式？

  - A. `"%s\n"`
  - B. `"%.2s\n"`
  - C. `"%d\n"`
  - D. `"%.2c\n"`
  - E. `"%.2f\n"`

- **13.** 一个`Unicode`编码的文本文件`MyUnicode.txt`需要被查看。在决定使用什么实用程序查看文件内容之前，你对其使用了`wc`命令。该实用程序向`STDOUT`显示`2020 6786 11328`。以下哪项是正确的？（选择所有适用的选项。）

  - A. 该文件有 2,020 行。
  - B. 该文件有 2,020 个字符。
  - C. 该文件有 6,786 个单词。
  - D. 该文件有 11,328 个字符。
  - E. 该文件有 11,328 行。

- **14.** 以下哪项最能定义文件描述符？

  - A. 代表文件类型的字母
  - B. 代表进程打开文件的数字
  - C. 文件名的另一种说法
  - D. 代表标准输出的六个字符名称
  - E. 指示文件分类的符号

- **15.** 默认情况下，`STDOUT`流向哪个项目？

  - A. `/dev/tty`，其中`n`是一个数字
  - B. `/dev/null`
  - C. `>`
  - D. `/dev/tty`
  - E. `pwd`

- **16.** 以下哪个命令可以将文件`SpaceOpera.txt`显示到输出，同时将其副本保存到文件`SciFi.txt`中？

  - A. `cat SpaceOpera.txt | tee SciFi.txt`
  - B. `cat SpaceOpera.txt > SciFi.txt`
  - C. `cat SpaceOpera.txt 2> SciFi.txt`
  - D. `cp SpaceOpera.txt SciFi.txt`
  - E. `cat SpaceOpera.txt && SciFi.txt`

- **17.** 以下哪个命令将生成的任何错误消息都放入黑洞？

  - A. `sort SpaceOpera.txt 2> BlackHole`
  - B. `sort SpaceOpera.txt && BlackHole`
  - C. `sort SpaceOpera.txt > BlackHole`
  - D. `sort SpaceOpera.txt 2> /dev/null`
  - E. `sort SpaceOpera.txt > /dev/null`

- **18.** 以下哪个命令将确定文件`Problems.txt`中有多少条记录包含单词`error`？

  - A. `grep error Problems.txt | wc -b`
  - B. `grep error Problems.txt | wc -w`
  - C. `grep error Problems.txt | wc -l`
  - D. `grep Problems.txt error | wc -w`
  - E. `grep Problems.txt error | wc -l`

- **19.** 你想找到名为`42.tmp`的任何文件，该文件存在于当前目录的树结构中，并将其内容显示到`STDOUT`。以下哪些允许你构建一个命令来做到这一点？（选择所有适用的选项。）

  - A. `xargs (find . -name 42.tmp) cat`
  - B. ``cat $(find . -name 42.tmp)``
  - C. `cat $(find . -name 42.tmp)`
  - D. `cat {find . -name 42.tmp}`
  - E. `find . -name 42.tmp | xargs cat`

- **20.** 你想编辑文件`SpaceOpera.txt`并决定使用`vim`编辑器来完成此任务。以下哪些是你可能会使用的`vim`模式？（选择所有适用的选项。）

  - A. `Insert`
  - B. `Change`
  - C. `Command`
  - D. `Ex`
  - E. `Edit`

## 系统启动和配置

### 第二部分

![](img/c0a399aca0d18f8822d714ad0a173123_196_0.png)

## 第 5 章：解释启动过程

- 目标 1.1：总结 `Linux` 基础知识。

![](img/c0a399aca0d18f8822d714ad0a173123_198_0.png)

![](img/c0a399aca0d18f8822d714ad0a173123_199_0.png)

本章检查 `Linux` 系统中的启动和初始化过程。首先，我们将查看计算机固件在启动过程中所起的作用，然后讨论 `Linux` 引导加载程序以及如何配置它们。接下来，本章讨论了 `Linux` 初始化过程，展示 `Linux` 如何决定在启动时启动哪些后台应用程序。本章最后介绍了一些可用于帮助挽救无法启动的系统的系统恢复选项。

### `Linux` 启动过程

当你打开 `Linux` 系统的电源时，它会触发一系列事件，最终导致登录提示符。通常，你不需要担心这些事件背后发生了什么；你只需登录并开始使用你的应用程序。

然而，有时你的 `Linux` 系统可能没有完全正确地启动，或者你期望在后台运行的应用程序可能没有运行。在这种情况下，了解 `Linux` 如何启动操作系统并启动程序有助于你解决问题。

以下部分逐步说明启动过程的步骤，以及你如何监视启动过程以查看哪些步骤失败了。

### 跟踪启动过程

`Linux` 启动过程可以分为三个主要步骤：

1. 工作站固件启动，执行硬件的快速检查（称为加电自检，或 `POST`），然后在可引导设备上查找引导加载程序。
2. 引导加载程序运行，并确定要加载哪个 `Linux` 内核程序。
3. 内核程序加载到内存中，并启动系统运行所需的后台程序（例如桌面环境的图形桌面管理器或服务器的 `Web` 和数据库服务器）。

虽然从表面上看，这三个步骤可能显得简单，但一系列操作协同工作以保持启动过程运行。每个步骤都会执行多个操作，为你的系统运行 `Linux` 做准备。

## 查看引导过程

你可以通过在系统引导时监视系统控制台屏幕来监控 `Linux` 引导过程。当系统检测硬件和加载软件时，你会看到许多信息性消息滚动经过。

某些图形桌面版 `Linux` 发行版在启动时会将引导消息隐藏在一个单独的控制台窗口中。通常，你可以按下`Esc`键或`Ctrl+Alt+F1`键组合来查看这些消息。

通常，引导消息滚动得很快，很难看清发生了什么。如果你需要排查引导问题，可以使用`dmesg`命令查看引导时消息。大多数 `Linux` 发行版会将引导内核消息复制到内存中的一个特殊环形缓冲区，称为`kernel ring buffer`（内核环形缓冲区）。该缓冲区是循环的，并设置为预定的大小。随着新消息记录在缓冲区中，旧消息会被轮换出去。

`dmesg` 命令显示当前存储在内核环形缓冲区中的最新引导消息，如图 5.1 所示。

### 列表 5.1 `Ubuntu` 工作站上 `dmesg` 命令的输出

```bash
$ dmesg
[    0.000000] Linux version 5.11.0-40-generic (buildd@lgw01-amd64-010) (gcc (Ubuntu 9.3.0-17ubuntu1~20.04) 9.3.0, GNU ld (GNU Binutils for Ubuntu) 2.34) #44~20.04.2-Ubuntu SMP Tue Oct 26 18:07:44 UTC 2021 (Ubuntu 5.11.0-40.44~20.04.2-generic 5.11.22)
[    0.000000] Command line: BOOT_IMAGE=/boot/vmlinuz-5.11.0-40-generic root=UUID=5423117e-4aaf-4416-ada7-01e07073b2e1 ro quiet splash
[    0.000000] KERNEL supported cpus:
[    0.000000]   Intel GenuineIntel
[    0.000000]   AMD AuthenticAMD
[    0.000000]   Hygon HygonGenuine
[    0.000000]   Centaur CentaurHauls
[    0.000000]   Shaoin  Shaogirl
[    0.000000] x86/fpu: Supporting XSAVE feature 0x001: 'x87 floating point registers'
[    0.000000] x86/fpu: Supporting XSAVE feature 0x002: 'SSE registers'
[    0.000000] x86/fpu: Supporting XSAVE feature 0x004: 'AVX registers'
[    0.000000] x86/fpu: xstate_offset[2]:  576, xstate_sizes[2]:  256
[    0.000000] x86/fpu: Enabled xstate features 0x7, context size is 832 bytes, using 'standard' format.
[    0.000000] BIOS-provided physical RAM map:
[    0.000000] BIOS-e820: [mem 0x0000000000000000-0x0000000000000fff] usable
[    0.000000] BIOS-e820: [mem 0x000000000009fc00-0x000000000009ffff] reserved
[  0.000000] BIOS-e820: [mem 0x000000000000f000-0x00000000000fffff] reserved
[  0.000000] BIOS-e820: [mem 0x00000000010000-0x0000000000dfffff] usable
[  0.000000] BIOS-e820: [mem 0x00000000df0000-0x00000000dffffff] ACPI data
[  0.000000] BIOS-e820: [mem 0x00000000fec00000-0x00000000fec00fff] reserved
[  0.000000] BIOS-e820: [mem 0x00000000fee00000-0x00000000fee00fff] reserved
[  0.000000] BIOS-e820: [mem 0x00000000ffcc0000-0x00000000ffffffff] reserved
[  0.000000] BIOS-e820: [mem 0x0000000100000000-0x000000021ffffff] usable
[  0.000000] NX (Execute Disable) protection: active
[  0.000000] SMBIOS 2.5 present.
[  0.000000] DMI: innotek GmbH VirtualBox/VirtualBox, BIOS VirtualBox 12/01/2006
[  0.000000] Hypervisor detected: KVM
[  0.000000] kvm-clock: Using msrs 4b564d01 and 4b564d00
[  0.000000] kvm-clock: cpu 0, msr 109001001, primary cpu clock
[  0.000000] kvm-clock: using sched offset of 3933158608 cycles
[  0.000001] clocksource: kvm-clock: mask: 0xfffffffffffffffx max_cycles: 0x1cd424ed4ffb, max_idle_ns: 881590591483 ns
[  0.000003] tsc: Detected 1497.589 Mhz processor
```

大多数 `Linux` 发行版还将引导消息存储在日志文件中，通常位于`/var/log`文件夹中。对于基于 `Debian` 和基于 `Red Hat` 的系统，该文件通常是`/var/log/boot.log`，但一些旧版 `Linux` 系统可能使用`/var/log/boot`。

虽然能够看到引导期间生成的不同消息很有帮助，但了解是什么生成了这些消息也很有用。本章将讨论这三个引导步骤中的每一个，并通过一些示例展示其工作原理。

## 固件启动

所有兼容 `IBM` 的工作站和服务器都使用某种内置固件来控制已安装操作系统的启动方式。在较旧的工作站和服务器上，这种固件被称为`Basic Input/Output System (BIOS)`（基本输入/输出系统）。在较新的工作站和服务器上，一种称为`Unified Extensible Firmware Interface (UEFI)`（统一可扩展固件接口）的方法维护系统硬件状态并启动已安装的操作系统。

### `BIOS` 启动

`BIOS` 固件有一个简单的菜单界面，允许你更改某些设置以控制系统如何查找硬件，并定义 `BIOS` 应使用哪个设备来启动操作系统。

原始 `BIOS` 固件的一个局限性是它只能从硬盘读取一个扇区的数据到内存中运行。这不足以加载整个操作系统。为了绕过这一限制，大多数操作系统（包括 `Linux` 和 `Microsoft Windows`）将引导过程分为两部分。

首先，`BIOS` 运行一个`bootloader`（引导加载程序）程序，这是一个小型程序，用于初始化必要的硬件以查找并运行完整的操作系统程序。它通常位于同一硬盘上的另一个位置，但有时位于单独的内部或外部存储设备上。

引导加载程序通常有一个配置文件，因此你可以告诉它在哪里找到要运行的实际操作系统文件，甚至生成一个小型菜单，允许用户在多个操作系统之间进行引导选择。

为了开始引导过程，`BIOS` 必须知道在已安装的存储设备上哪里可以找到引导加载程序。大多数 `BIOS` 设置允许你从几个位置加载引导加载程序：

- 内部硬盘
- 外部硬盘
- `CD` 或 `DVD` 驱动器
- `USB` 内存棒
- `ISO` 文件
- 使用 `NFS`、`HTTP` 或 `FTP` 的网络服务器

从硬盘引导时，你必须指定硬盘以及硬盘上的分区，以便 `BIOS` 从中加载引导加载程序。这是通过定义`Master Boot Record`（主引导记录，`MBR`）来完成的。

`MBR` 是系统第一个硬盘分区上的第一个扇区。计算机系统只有一个 `MBR`。`BIOS` 查找 `MBR` 并将存储在那里的程序读入内存。由于引导加载程序必须容纳在一个扇区中，它必须非常小，因此不能做太多事情。引导加载程序主要指向实际操作系统内核文件的位置，该文件存储在安装在系统的单独分区的引导扇区中。内核引导文件没有大小限制。

![](img/c0a399aca0d18f8822d714ad0a173123_202_0.png)

引导加载程序不需要直接指向操作系统内核文件；它可以指向任何类型的程序，包括另一个引导加载程序。你可以创建一个初级引导加载程序，它指向一个次级引导加载程序，后者提供加载多个操作系统的选项。这个过程被称为`chainloading`（链式加载）。

### `UEFI` 启动

随着操作系统变得更加复杂，显然需要开发一种新的引导方法。

`Intel` 于 1998 年创建了`Extensible Firmware Interface`（`EFI`，可扩展固件接口）来解决 `BIOS` 的一些局限性。到 2005 年，这一想法在其他供应商中流行起来，`Universal EFI (UEFI)` 规范被采纳为标准。如今，几乎所有兼容 `IBM` 的桌面和服务器系统都使用 `UEFI` 固件标准。
