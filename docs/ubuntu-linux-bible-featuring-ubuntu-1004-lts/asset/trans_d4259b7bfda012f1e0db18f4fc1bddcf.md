

# 第 24 章：使用虚拟机和模拟器

产品，所有这些程序都在虚拟机程序之上运行一个管理操作系统，虚拟机本身也是如此。这个管理操作系统可以与虚拟机程序通信，并用于管理虚拟机实例以及分配给它们的资源。虚拟化技术，例如基于内核的虚拟机（KVM，其中 Linux 内核运行在宿主系统上，等同于虚拟机程序），也在致力于半虚拟化设备驱动程序。

- **内核级虚拟化（Kernel-level virtualization）**：在技术上不需要虚拟机程序，而是将 Linux 内核的独立版本和关联的虚拟机作为用户空间进程运行在物理宿主机上。这为在单个宿主机上运行多个虚拟机提供了一种简便的方法，但只有那些遵循并支持相应内核级虚拟化技术的虚拟机才能运行。示例包括用户模式 Linux（UML），它已经在 Linux 主线内核中支持了很长时间；以及在 Linux 2.6.20 主线内核中引入的 KVM。UML 不需要任何单独的管理软件。KVM 使用宿主内核中的设备驱动程序在主 Linux 内核与虚拟机之间进行通信，并使用稍稍修改的 QEMU 进程作为其虚拟机的显示和执行容器。KVM 的内核级虚拟化是全虚拟化的特化版本，其中 Linux 内核充当虚拟机程序；我认为 UML 和 KVM 足够独特，足以自成一类别。Ubuntu 内核包含 KVM 模块，KVM 的用户空间组件在 Ubuntu 仓库中可用。

- **硬件虚拟化（Hardware virtualization）**：与半虚拟化和全虚拟化非常相似，硬件虚拟化使用虚拟机程序，但仅在提供硬件化支持的系统中可用。基于虚拟机程序的系统（如 Xen 和 VMware ESXi）以及内核级虚拟化技术（如 KVM）可以利用最新一代 Intel（Intel VT）和 AMD（AMD-V，又名 Pacifica）处理器提供的硬件化支持。硬件虚拟化环境中的虚拟机可以运行未修改的操作系统，因为虚拟机程序可以使用硬件的虚拟化支持来处理特权和保护操作以及硬件访问请求，并与虚拟机通信和管理。Xen 和 KVM 在 Ubuntu 仓库中可用。

这些虚拟化方法各有其优缺点。如前提到的，取决于你的硬件，单一虚拟机技术实际上可以支持上述虚拟机方法中的多种。在 Intel VT 和 AMD-V 处理器上，KVM 同时支持内核级和硬件虚拟化。在这些相同的处理器上，

## 我可以使用哪些类型的虚拟化？

除了硬件虚拟化外，上一节描述的所有虚拟化技术都可以在任何带有 Pentium 或更高级处理器的 x86 兼容系统上使用。我建议至少使用 Pentium IV 或同等的处理器，并且还建议使用 64 位处理器，因为这些处理器更现代、更强大，并且通常提供硬件化虚拟化支持。

如果你的系统使用的是具有硬件化虚拟化支持的处理器（例如 Intel VT 和 AMD SVM 处理器），你可以在 KVM 和 Xen 等虚拟化技术下将未修改的操作系统作为虚拟机运行。硬件虚拟化支持允许你像在物理系统上一样，通过安装在虚拟机来安装并运行 Microsoft Windows 操作系统。（当然，你也可以使用任何 Linux 安装盘，并将任何标准 Linux 发行版安装为虚拟机，而无需任何修改。）在撰写本文时，提供硬件化虚拟化支持的处理器如下：

- Intel VT（虚拟化技术，又名 Vanderbilt）：选定的 Pentium IV、Pentium D、Xeon 5000 及后续型号、Xeon LV、Core Duo、Core 2 Duo、Core 2 Quad 以及四核处理器
- AMD-SVM（虚拟化/安全虚拟机，又名 Pacifica）：AMD Athlon 64（“F”和“G”系列）socket AM2、Athlon64 X2（“F”和“G”系列）、Turion 64 X2、更新的 Opteron 以及所有更新处理器

要确定给定系统中的处理器是否支持虚拟化，你可以检查 `/proc/cpuinfo` 文件中的标志位（flags），你可以通过如下命令来实现：

```
cat /proc/cpuinfo | grep flags
```

取决于你使用的是 AMD 还是 Intel 处理器，该命令的输出非常不同：

```
AMD flags : fpu tsc msr pae mce cx8 apic mtr mca mov \
pat pse36 clifush fmx ssr sse2 syscall \
nx mmxext fxsr_opt 1m 3nowext 3down up pni \
c16 lahf_lm cr8_legacy
```

```
Intel flags : fpu vme de pse tsc msr pae mce cx8 apic sep \
mtr pse mca mov pat pse36 clifush dt acpi \
mmx fxsr sse sse2 ss ht tm pbe syscall nx 1m \
constant_tsc arch_perfmon pebs bts_good \
pni monitor ds_cp1 vmx est tm2 ssse3 cx16 \
xtpr lahf_lm
```

如果你使用的是 Intel CPU，你会在 `flags` 字段中寻找 `vmx` 字段。如果你使用的是 AMD CPU，你会在 `flags` 字段中寻找 `svm` 字段。以下是一到位完成此操作的简单方法：

```bash
# grep '(vmx|svm)' /proc/cpuinfo
```

如果你看到此命令的任何输出，说明你的系统支持虚拟化。恭喜你！

## 选择虚拟化技术

选择虚拟化技术的关键在于你愿意做多少工作以及你想如何使用这些机器：

- 操作系统解决方案（如 VirtualBox 和 VMware Server）最容易安装和理解，除了最初安装外，对系统的修改非常少。VirtualBox 的内核驱动程序在安装 VirtualBox 时构建，VMware Server 也是如此。在这两者中，VirtualBox 更易使用和管理，但 VMware 更像是一个行业标准。
- 虚拟机程序解决方案（如 Xen）可以比其他方法提供更高的性能和灵活性，但需要额外的管理开销。当启动虚拟机程序并加载域内核时，系统的启动配置不同。你必须使用专用工具（xm、virt_manager 等）来配置和管理虚拟机。
- 内核级虚拟机（如 KVM）比基于虚拟机程序的虚拟机更容易管理，但无法提供同等的内存使用、执行优先级等管理粒度。

建议？如果你只是想偶尔运行 Windows 应用程序，请使用 VirtualBox。如果你想从桌面系统尝试更高级的虚拟化技术，请尝试 KVM。如果你需要完整的、企业级的虚拟化环境并愿意学习一下，请选择 Xen（遗憾它在本章中没有讨论，但有很多关于 Xen 的优秀书籍，包括《Professional Xen Virtualization》，Wrox, 2008, ISBN:047013814）。

# Linux 下流行的模拟软件

大多数系统最为人知的模拟包根本不是桌面计算机模拟器——而是多街机游戏模拟器（MAME; www.mame.net），它允许你直接从只读存储器镜像玩各种古老的街机视频游戏。

