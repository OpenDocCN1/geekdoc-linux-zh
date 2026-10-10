
`git clone https://github.com/GrayHatacking/GH6`

Dockerfile 提供了开发环境：

```bash
cd GH6/24
docker build -t kali
```

本章将使用的监控程序是 KVM（Linux 默认），它需要在主机上安装。若要在容器中使用它，你必须重定向 `/dev/kvm` 设备，如下：

```bash
docker run --device=/dev/kvm -it kali
```

## 监控程序攻击面

在上一章中，你学习了指令如何分为不同的组：无害、敏感等。为了探索大多数功能，我们的重点应该放在陷阱进入 VMM 的指令上；正如我们所知，大多数指令都是特权的。这是我们研究中假设的初始访问级别。

虚拟化栈由多个组件组成，每个组件运行在不同级别。漏洞的影响取决于受影响的组件。最好的情况下，我们可以直接从非权限客户机破坏 VMM（在 VMX root 模式下）。或者，我们的目标主机或特权客户机（分区/dom0）内的内核态执行，而在糟糕的情况下，我们仍然用户态栈。组件之间交互，破坏低权限组件可以扩大攻击面，从而在更高级别的组件中被进一步利用。

下图概述了类型-2 监控程序和类型-1 监控程序的不同组件暴露的攻击面。

![](img/0add480ffb73b6bc89b65d99f7d6b37a_812_0.png)

对于一般的（现代的硬件辅助监控程序），我们探索攻击面的起点将查看导致不同退出原因代码的条件。发生 VM-Exit 后，CPU 在 VMX root 模式下从存储在虚拟机控制结构（VMCS）主机状态区域的指令指针处恢复执行。这指向监控程序代码，该代码（在保存某些状态后）会检查 VMCS 退出原因字段并决定采取哪些操作。

我们可以在 Linux 内核源码找到可能的退出原因定义列表：

https://github.com/torvalds/linux/blob/master/tools/arch/x86/include/uapi/asm/vmx.h

这些退出条件中的某些是我们无法接触的（要么由外部事件引起，要么取决于特定的 CPU 特性或 VMCS 配置而不可用），但许多可以通过在客户机执行特定指令来触发。

**注意** 在在本章末尾，我们将编写几个模糊器（fuzzers用于探索 `EXIT_REASON_IO_INSTRUCTION`、`EXIT_REASON_MSR_READ` 和 `EXIT_REASON_MSR_WRITE`。

除了 VM-Exit 条件外，攻击面还可以通过基于共享内存的通信机制暴露——例如，仿真硬件设备中的直接内存访问 (DMA)，或者 VMBus$^1$ 或 VIRTIO.$2$ 使用的缓冲区。遗憾的是，我们在本章中不会涵盖这个主题。

最后，不依赖硬件辅助虚拟化的监控程序暴露了更大的攻击面，但这些现在不是常见的目标。

## 单内核 (Unikernel)

如前所述，我们需要能够从客机 VM 执行任意的 Ring-0 代码。实现这一点的方法是实现一个内核驱动，在部署在 VM 中的通用操作系统中执行任意代码。这种方法存在一些问题。首先，完整的操作系统既缓慢又臃肿。其次，并发执行多个任务引入了不确定性。为了避免这些问题，我们将根据以下要求实现自己的单内核$^3$：

- **简单性**：它应该具有很小的内存占用并且是高效。
- **快速（重）启动**：达到不可恢复的状态是很常见的，因此我们必须重启。
- **韧性**：内核必须尝试从无效状态中恢复并尽可能持续运行。当这不可能时，我们需要重启。
- **确定性**：实现完全的确定性是不可能的，但我们需要尽可能接近它。这对于 bug 重现和模糊用例最小化（fuzz-case minimization）非常重要。
- **可移植性**：它应该能够在大多数监控程序实现上运行而无需重大修改。

我们的单内核将与外部工具通信，允许它们在 VM 的 Ring-0 注入并执行任意代码。我们必须能够收集执行结果并发送回工具。在接下来的章节中，我们将介绍该内核的开发过程。

## 实验 24-1：启动与通信

为了启动我们的内核，我们将使用 GRUB 来避免编写自己的启动加载程序的麻烦。通常，监控程序支持 BIOS 启动和/或 UEFI。幸运的是，`grub-mkrescue`⁴ 允许我们生成用于启动的 ISO 介质。

我们的内核镜像将是一个 ELF 文件，在代码段开头放置一个 Multiboot⁵ 头部。当 GRUB 启动镜像时，它留给我们的环境是 32 位保护模式；我们希望使用所有用的处理器特性，因此我们必须切换到长模式（long-mode）。

让我们从产生 Multiboot2 头部并切换到长模式的引导代码开始实现：

```asm
;; bootstrap.asm

extern kmain

global _start

[bits 32]

[section .bss]

align 0x1000

resb 0x2000

stack_top:

pd: resb 0x10000 * 4 ; 4 PDs = maps 4GB

pdpt: resb 0x10000 ; 1 PDPT

pml4: resb 0x10000 ; 1 PML

[section .data]

; minimal 64-bit GDT

gdt:

dq 0x0000000000000000

dq 0x00A09B00000FFFF ; kernel CS

dq 0x000C993000000ffff ; kernel DS

gdt_end:

; TODO: TSS

gdtr:

dw gdt_end - gdt - 1 ; GDT limit

dq gdt ; GDT base

[section .text]

align 8,2 db 0

;;multiboot2 header

mb_header_size equ (mb_header_end - mb_header)

mb_header:

dd 0xE85250D6 ; magic field

db 0 ; architecture field: i386 32-bit protected-mode

dd mb_header_size ; header length field

dd 0xFFFFFFFF & (0xE85250D6 + mb_header_size) ; checksum field

dw 0 ; termination tag

dw 0 ; tag type

dw 0 ; flags

db 8 ; tag size

mb_header_end:

;; kernel code starts here

_start:

mov esp, stack_top

mov edi, pd

mov ecx, 512*4

mov eax, 0x87

init_pde:

mov word [edi], eax

add eax, 0x200000

add edi, 8

dec ecx

jnz init_pde

mov word [pdpt], pd + 7

mov word [pdpt+0x08], pd + 0x1007

mov word [pdpt+0x10], pd + 0x2007

mov dwarf [pdpt+0x18], pd + 0x3007

mov eax, pml4

mov dwarf [eax], pdpt + 7

mov cr3, eax ; load page-tables

mov ecx, 0xC000080

rdsr

or eax, 0x101 ; LME

wrmsr ; set EFER

lgdt [gdtr] ; load 64-bit GDT

mov eax, 0xba ; DE | PAE | PGE | PCE

mov cr4, eax

mov eax, 0x8000003 ; PG | PE | MP | NE

mov cr0, eax

jmp code64

[bits 64]

code64:

mov ax, 0x10

mov ds, ax

mov ss, ax

call kmain
```

`.text` 段以产生 Multiboot2 头的指令开始 ①。在入口处 ② 设置了 8KB 栈，并映射了前 4GB 内存 ③后续步骤包括在 EFER 寄存器中设置长模式 ④、加载 64 位 GDT ⑤、启用分页 ⑥ 并进入长模式 ⑦。代码以调用 `kmain` 结束。

为了内核与外部世界之间的通信，可以使用简单且广泛提供的设备：串口。大多数监控程序实现了串口仿真，它们通常允许将其转发到主机的机制中，例如套接字或管道。让我们为内核添加串口支持：

```c
/* common.c */

static uint16_t serialPort = 0x3f8; /* TODO: set it dynamically */

static void outb(uint16_t port, uint8_t val) {
    asm_volatile("outb %0, %1" : : "a(val), "d(port)");
}
```
