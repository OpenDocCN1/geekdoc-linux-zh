
![](img/9eb7e89292d2f85707b4d49102c865b7_271_0.png)

使用 make config 配置内核是一个相当漫长的过程，也有点繁琐；然而，如果你恰好通过 Telnet 连接在远程服务器上配置内核，它就非常合适。基于行的界面可能并不优雅，但它适用于大多数场景，当下面两种方法（make menuconfig 和 xconfig）不可用时，你应将其视为默认的配置方法。

make config 是配置内核最简单的方法；然而，它可能不是初学内核黑客最合适的选择。本节及以下小节我将讨论使用 make config 方法的一个示例内核配置会话。但你应该知道，随着 Linux 不断添加对各种设备的特性和支持，make config 显示的确切步骤也会发生变化。因此，你在下面看到的内容可能与你在系统上运行 make config 时看到的内容不完全相同。我在此讨论主要决策点。如果你运行 make config 时遇到新的配置问题，只需在提示符下输入 ? 即可了解更多信息，或选择使用默认值。

![](img/9eb7e89292d2f85707b4d49102c865b7_271_1.png)

你可以通过按 Enter 键来选择默认答案。另请注意，默认答案始终以大写字母表示。

## 代码成熟度级别选项

本节中，你会被询问是否希望对实验性功能进行提示。如果你为这样一个系统配置内核，在该系统中实验、停机和崩溃是乐趣的一部分而不是负担，你可以选择查看（并可能使用）这些实验性功能。提示如下：

```
Prompt for development and/or incomplete code/drivers (CONFIG_EXPERIMENTAL)
[Y/n/?]
```

默认答案（Y）是可以的。

## 可加载模块支持

Linux 内核使用一种创新的方法来保持低调：它使用作为外部模块实现的特性和驱动程序。这些模块根据需要动态加载和卸载。这使得内核所需的内存更少，并变得更具硬件独立性。通常，你使用名为 kerneld 的程序加载模块，而 kerneld 又使用另一个名为 modprobe 的程序来管理可用模块。模块可以是设备驱动程序、文件系统、二进制可执行格式等等。本节中，你会被询问是否需要模块相关支持。第一个问题如下：

```
Enable loadable module support (CONFIG_MODULES) [Y/n/?]
```

这真的不应该是一个选项——在几乎所有场景下，你肯定希望拥有可加载模块支持。默认值是可以的。

```
Set version information on all symbols for modules (CONFIG_MODVERSIONS) [Y/n/?]
```

当你编译带有版本信息的模块时，可以在无需从头编译的情况下将其与新内核一起重用。然而，首选方法是与新内核一起编译模块以消除兼容性问题。因此首选答案是否（即输入 n）。

```
Kernel module loader (CONFIG_KMOD) [Y/n/?]
```

Linux 可以使用 kerneld 守护进程加载模块。此提示询问你是否希望在内核内部使用内核模块加载器以避免使用 kerneld 守护进程。因为 kerneld 使用 System V 进程间通信（SysV IPC）代码编写，而许多程序员认为这种代码并不十分可靠，因此最好避免使用 kerneld 并用内核模块作为替代。默认答案（Y）已足够。

## 处理器类型、内存模型和特性

本节中，你会被询问处理器家族、内存模型、数学协处理器、多处理器和其他处理器特定问题。以下是第一个提示：

```
Processor family (386, 486, 586/K5/5x86/6x86/6x86MX, Pentium-Classic, Pentium-MMX, Pentium-Pro/Celeron/Pentium-II, Pentium-III/Celeron(Coppermine), Pentium-4, K6/K6-II/K6-III, Athlon/Duron/K7, Crusoe, Winchip-C6, Winchip-2, Winchip-2A/ Winchip-3, CyrixIII/C3) [Pentium-III/Celeron(Coppermine)]
```

如果默认的处理器架构不正确，你应该选择其中一个列出的选项。在我的情况下，默认值是错误的，所以我输入 Pentium/ K6/TSC 作为处理器家族。

接下来你会被询问是否希望如下面所示配置内核以支持东芝笔记本电脑：

```
Toshiba Laptop support (CONFIG_TOSHIBA) [N/y/m/?]
```

如果你为此类笔记本电脑制作此内核，默认答案（N）是可以的。

```
/dev/cpu/microcode - Intel IA32 CPU microcode support (CONFIG_MICROCODE) [N/y/m/?]
```

如果你希望能够在 Intel 发布时更新你的 Intel IA32（Pentium Pro、PII、PIII、Pentium 4、Celeron、Xeon 等）处理器的微代码，请在此处回答 yes（y）。要了解更多信息，请访问 www.urbanmyth.org/microcode/。大多数 Linux 用户不需要此功能。

```
/dev/cpu/*/msr - Model-specific register support (CONFIG_X86_MSR) [N/y/m/?]
```

如果你希望允许系统程序访问 x86 模式特定寄存器（MSRs），请输入 y 或接受默认值。

```
/dev/cpu/*/cpuid - CPU information support (CONFIG_X86_CPUID) [N/y/m/?]
```

如果你希望允许程序访问 Intel CPU 中可用的 CPU 标识，请在此处回答 yes（y）。启用此功能将创建一个名为 /dev/cpu/CPU_number/cpuid 的设备，用于显示 CPU 标识信息。例如 /dev/cpu/0/cpuid 显示系统第一个 CPU 的信息。

![](img/9eb7e89292d2f85707b4d49102c865b7_273_0.png)

> 如果你有两个 CPU，你将拥有 /dev/cpu/0/cpuid 和 /dev/cpu/1/cpuid 设备。

如果你拥有少于 4GB 的 RAM，可以接受默认值（关闭），否则如果有 4GB 物理 RAM，请输入 4GB，如果高于 4GB，可以在此处输入 64GB。

```
defined CONFIG_M686
```

```
Math emulation (CONFIG_MATH_EMULATION) [N/y/?]
```

除非你有一台（非常老旧的）处理器内置数学协处理器，否则你应该在此处按 Enter 选择默认值。

```
MTRR (Memory Type Range Register) support (CONFIG_MTRR) [N/y/?]
```

这可能是在你（除非你是 x86 CPU 设计专家）和大多数初学内核黑客看来不太合理的问题。那么你可以在这里选择什么？默认选项通常对大多数情况是正确的。此外，你可以通过在提示符下输入 ? 字符来了解 Memory Type Range Register（MTRR）支持的含义。你将得到如下所示的帮助屏幕：

```
CONFIG_MTRR:
```

```
On Intel Pentium Pro and Pentium II systems the Memory Type Range
Registers (MTRRs) may be used to control processor access to memory ranges. This
is most useful when you have a video (VGA) card on a PCI or AGP bus. Enabling
write-combining allows bus write transfers to be combined into a larger transfer
before bursting over the PCI/AGP bus. This can increase performance of image
write operations 2.5 times or more. This option creates a /proc/mtrr file which
may be used to manipulate your MTRRs. Typically the X server should use this.
This should have a reasonably generic interface so that similar control
registers on other processors can be easily
supported.

Saying Y here also fixes a problem with buggy SMP BIOSes which only set the
MTRRs for the boot CPU and not the secondary CPUs. This can lead to all sorts of
problems.

You can safely say Y even if your machine doesn’t have MTRRs, you’ll just add
about 3k to your kernel.

See Documentation/mtrr.txt for more information.
```

如你所见，这非常有帮助。因为我为服务器配置此内核，我不太关心视频，所以我在此处选择“N”。

```
Symmetric multi-processing support (CONFIG_SMP) [Y/n/?]
```

如果你的系统上有多个处理器并且希望启用对称多处理支持，请选择默认值。在我的情况下，我没有多处理器主板；因此，我选择拒绝 SMP 支持。

## 通用设置

本节中，你配置通用选项。

```
Networking support (CONFIG_NET) [Y/n/?]
```

也许有少数人希望运行 Linux 而不使用网络支持，但对于大多数用户来说，默认值是必须的。

```
SGI Visual Workstation support (CONFIG_VISWS) [N/y/?]
```

如果你没有使用 SGI 系统，请选择默认值。

```
PCI support (CONFIG_PCI) [Y/n/?]
```

除非你使用的是只有 ISA 总线的非常老旧的 x86 系统，否则默认值是可以的。

![](img/9eb7e89292d2f85707b4d49102c865b7_275_0.png)

> 在 Sparc 系统上，如果你只有 sbus 卡，可能不需要 PCI 支持。

```
PCI access mode (BIOS, Direct, Any) [Any]
```

默认选项允许内核使用直接方法检测 PCI 配置；如果失败，它将从系统 BIOS 获取 PCI 配置，因此默认值是可以的。

```
PCI device name database (CONFIG_PCI_NAMES) [Y/n/?]
```

默认情况下，内核会在完成启动并完成 /proc/pci 和 /proc/ioports 条目的构建之前存储所有已知的 PCI 设备名称。默认答案是可以接受的。

```
EISA support (CONFIG_EISA) [N/y/?]
```
