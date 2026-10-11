
# 第 1337 行

这一行是该部分的入口点。

## 8.3 依赖架构的内存初始化

第 1364 行
`machine_init()`（查看文件 `arch/ppc/kernel/setup.c`，行 532）设置机器特定信息，例如 NVRAM、L2、CPU 缓存行大小、调试等。

第 1365 行
`MMU_init()`（查看文件 `arch/ppc/mm/init.c`，行 234）发现高内存和低内存的总内存大小。然后它初始化 MMU 硬件（`MMU_init_hw()`，行 267）、设置哈希页表（`arch/ppc/mm/hashtable.s`）、映射从 `KERNELBASE` 开始的所有 RAM（`mapin_ram()`，行 272）、映射所有 I/O（`setup_io_mappings()`，行 285），并初始化上下文管理 `mmu_context_init()`（行 288）。

第 1385 行
关闭 IR 和 DR 以设置 SDR1。它持有页表的地址以及哈希值中有多少位被用于页表索引。

第 1395 行
清除 TLB，加载 SDR1（哈希表基础和大小），设置分段，并根据特定的 PPC 平台初始化 BAT 寄存器。

第 1412–1419 行
开启 IR、DR 并通过 RFI 跳转到 `start_kernel /init/main.c`。注意在 PowerPC 架构的中断发生期间，指令地址寄存器（ISR）的内容持有处理器在处理完中断后必须返回的地址。此值保存在保存恢复寄存器 0（SRR0）中。机器状态寄存器（MSR）则保存在保存恢复寄存器 1（SRR1）中。简而言，在中断时：

- IAR->SRR0
- MSR->SRR1

RFI 指令通常在中断程序结束时执行，它是该过程的反过程，将 SRR0 恢复到 IAR，SRR1 恢复到 MMR。简写：

- SRR0->IAR
- SRR1->MSR

# 第 8 章 • 启动内核

第 1385–1419 行的代码通过以下三个步骤开启和关闭内存：

- 设置 SRR1 中所需的 MSR 位（见图 8.1）。
- 设置 SRR0 中期望的跳转地址。
- 执行 RFI 指令。

## 8.3.2 基于 x86 的硬件管理

上电时，所有 Intel 处理器都处于实模式模式。实模式是早期处理器的兼容模式。随着处理器变得复杂，旧留代码仍然需要运行。在实模式下，处理器可以使用相同的指令执行为 86 和 8088 编写的程序，更重要的是地址转换是处理器访问系统的方式。早期处理器具有 20 位总线，访问访问 64K 内存。这是早期代码的限制。在实模式下，线性地址与物理地址相同。当我们遍历初始化内存的代码时，看到了后续处理器使用的更多特性以及添加到软件中的复杂结构。`setup.S` 中的代码执行了以下重要函数：

```
arch/i86/boot/setup.S

307 #define SMAP 0x53d

308

good820:

310 xor %ebx,%ebx      # 计数器

311 mov $E820,SMAP,%edi   # 指向白名单

312                      # 我们可以直接写入它

313 jpe820:

314 mov $0x0000e20,%ax  # e820，高字清零

315 movl $SMAP,%edx        # 'SMAP'

316 movl $20,%ecx          # e820 记录的大小

317 pushw %ds               # 数据记录

318 popw %es

319 int $0x15               # 调用

320 jc fail820             # 如果失败则跳转到 e801

323 cmpl $SMAP,%eax    # 检查返回值是否为 'SMAP'

324 jne fail820          # 如果失败则跳转到 e801

326...

333 good820:

334 movb (E820NR),%al   # 直到 32 条目

335 cmmp $E820MAX,%al

336 jnl fail820

337 incb (E820NR)

338 movw %di,%ax

339 addw $20,%ax

340 movw %ax,%di

341 again:

342 cmpl $0,%ebx       # 检查 %ebx 是否设置为 EOF

343 jneq fail820

345 fail820:
```

第 307–345 行
查看代码段，我们首先看到（第 321 行）调用 BIOS int15h 函数，ax=0xe20。这返回了 BIOS 感知的许多类型内存的地址和长度。这个简单的内存映射表示获取 Linux 所有内存页的基础池。通过进一步研究代码可见，内存可以通过可以通过方法获取：E820、0xe01 和 0x88。这三种方法都与现有的 BIOS 发行版及其平台兼容。

```
arch/i386/boot/setup.S

595 # 现在我们将系统移动到它的正确位置 ... 但我们检查是否为大内核。在这种情况下我们不能移动它

597 test $LOADED_HIGH,%cs:loadflags

598 jz do_move         # 则我们有一个正常加载镜像

599 # 否则我们有一个高加载 bImage

602 jump end_move      # ... 并跳过移动

603

604 do_move:

605 movw $0x100,%ax    # 目标段起始

606 movw %cs,%bp        # 即 SETUPSEG

607 subw $DELTA_INITSEG,%bp # 即 AKINITISEG

608 movw %cs:start_sys_seg,%bx # 源段起始

609 cld

610 do_move:

611 movw %ax,%es      # 目标段

612 incb %ah      # 而不是 add ax,#0x100

613 movw %bx,%ds      # 源段

614 addw $0x100,%bx

615 subw %di,%di

616 subw %si,%cx

617 movw $0x800,%bx

618 rep

619 movw

620 cmpw %bp,%bx      # 假设 start_sys_seg > 0x2000，

621 所以我们可能会读取比需要的多的页，但

622 永远不会覆盖 INITSEG

623 因为目标比源

624 至少低一页

626 jl do_move

627

628 end_move;
```

# 第 595–628 行
该代码是由 `build.c` 创建并由 `LILO` 加载的内核镜像。它由初始化段（地址 0x9000）、设置段（0x9200）和压缩镜像组成。镜像最初加载在地址 0x10000。如果是 LARGE（>0x7FF），则留在原地；否则，将其移动到 0x1000。

## 8.3 依赖架构的内存初始化

### 在 Intel 实实地址模式下形成 20 位物理地址

原始 IBM PC 中的 Intel 8088 处理器只有 20 条地址线 [0...19]。这允许系统在内部访问多达 1MB 加上 64K 字节的内存（0 到 0x10FFFF），但在*物理上*（在总线上），最后的 64K 可寻址内存实际上是真实内存的*第一个* 64K！

在处理器内部，20 位地址由一个 16 位的段选择器和一个 16 位的段偏移量组成。段选择器左移 4 位并加到偏移量上，该偏移量会进行 4 位扩展。这些寄存器的之和即在总线上可见的物理地址。

例如：

为了获得最高地址，我们向段选择器（CS、DS、ES 等）加载值 0xFFFF，向索引寄存器（SI、DI 等）加载值 0xFFFF。在处理器内部，段被左移 4 位并加到偏移量上。

```
0FFFF 左移 4 位 = 0x0 FFF00

加上偏移量               + 0x00FFFF

内部求和               = 0x10FFFF

外部物理地址            = 0x00FFFE
```
