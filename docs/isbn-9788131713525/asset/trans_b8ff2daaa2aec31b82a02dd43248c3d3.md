
在列表 16-3 中，我们列出了 `lite5200.c` 平台初始化文件中的函数。除了 `platform_init()` 之外，所有函数都声明为 static。因此，如图 16-3 所示，这是平台初始化文件的入口点。该文件中的其余函数仅在文件内部被引用。

让我们来看看入口函数 `platform_init()`。列表 16-8 重新列出了来自 `lite5200.c` 文件的 `platform_init()` 函数。

# 列表 16-8

## Lite5200 platform_init 函数

```c
void __init
platform_init(unsigned long r3, unsigned long r4,
           unsigned long r5, unsigned long r6,
           unsigned long r7)
{
  /* Generic MPC52xx platform initialization */
  /* TODO Create one and move a max of stuff in it.
     Put this init in the syslib */

  struct bi_record *bootinfo = find_bootinfo();

  if (bootinfo)
    parse_bootinfo(bootinfo);
  else {
    /* Load the bd_t board info structure */
    if (r3)
      memcpy((void*)&__res, (void*)(r3+KERNELBASE),
             sizeof(bd_t));

    #ifdef CONFIG_BLK_DEV_INITRD
    /* Load the initrd */
    if (r4) {
      initrd_start = r4 + KERNELBASE;
      initrd_end = r5 + KERNELBASE;
    }
    #endif

    /* Load the command line */
    if (r6) {
      *(char *)(r7+KERNELBASE) = 0;
      strcpy(cmd_line, (char *)(r6+KERNELBASE));
    }
  }

  /* PPC Sys identification */
  identify_ppc_sys_by_id(mfspr(SPRN_SVR));

  /* BAT setup */
  mpc52xx_set_bat();

  /* No ISA bus by default */
  isa_io_base         = 0;
  isa_mem_base        = 0;

  /* Powersave */
  /* This is provided as an example on how to do it.  But you
   * need to be aware that NAP disable bus snoop and that may
   * be required for some devices to work properly, like USB
   *... */
  /* powersave_nap = 1; */

  /* Setup the ppc_md struct */
  ppc_md.setup_arch = lite5200_setup_arch;
  ppc_md.show_cpuinfo = lite5200_show_cpuinfo;
  ppc_md.show_percpuinfo = NULL;
  ppc_md.init_IRQ       = mpc52xx_init_irq;
  ppc_md.get_irq       = mpc52xx_get_irq;

  #ifdef CONFIG_PCI
  ppc_md.pci_map_irq = lite5200_map_irq;
  #endif

  ppc_md.find_end_of_memory = mpc52xx_find_end_of_memory;
  ppc_md.setup_io_mappings = mpc52xx_map_io;

  ppc_md.restart   = mpc52xx_restart;
  ppc_md.power_off = mpc52xx_power_off;
  ppc_md.halt      = mpc52xx_halt;

  /* No time keeper on the LITE5200 */
  ppc_md.time_init    = NULL;
  ppc_md.get_rtc_time = NULL;
  ppc_md.set_rtc_time = NULL;

  ppc_md.calibrate_decr   = mpc52xx_calibrate_decr;
  #ifdef CONFIG_SERIAL_TEXT_DEBUG
  ppc_md.progress          = mpc52xx_progress;
  #endif
}
```

这个函数包含了该平台所需的大量定制内容。它首先查找由引导加载程序提供的板级特定数据。我们将推迟到第 16.3.2 节“板级信息结构”中再讨论这些细节。

接下来，如果你的内核配置了初始 RAM 磁盘（initrd），那么 RAM 磁盘映像的起始和结束地址将被保存。请注意，按照惯例，它们是通过 PowerPC 通用寄存器 r4 和 r5 传递的。将 initrd 地址通过这些寄存器传递是引导加载程序的责任。稍后，内核将使用这些地址从原始内存（引导加载程序放置的位置或非易失性闪存映像）中加载 initrd 映像到内部内核 RAM 磁盘结构。

接下来我们看到了一段代码，用于存储内核命令行，其地址通过寄存器 r6 和 r7 传递给 `platform_init()`，分别标记起始地址和结束地址。这与前面描述的存储静态内核命令行的方法在一个特定细节上有所不同：这个内核命令行是从引导加载程序传递给 `platform_init()` 的，而不是编译进内核的。

复制 initrd 和内核命令行非常直接。基本上，从引导加载程序传入的寄存器包含了这些数据结构的内存地址。然而，有一个小的微妙之处。你可能已经对常量 `KERNELBASE` 的作用产生了好奇。理解这一点是掌握引导序列中较复杂部分的关键。

引导加载程序提供的地址是物理地址。这意味着它们是数据驻留在内存芯片中的实际硬件地址。引导加载程序通常在没有虚拟内存支持的情况下运行。然而，内核本身静态链接到一个众所周知的、用户可配置的基地址。这个地址就是 `KERNELBASE`。（该值本身与讨论无关——它是用户可配置的，但几乎从未从默认值 0xC0000000 更改。）

这在 `head.S` 中设置了一个有趣的情况。当内核被解压缩并重新定位到 RAM（通常位于位置 0）时，它所有的代码和数据符号都链接在内核的虚拟地址 `KERNELBASE` 上。通过检查内核构建过程中生成的内核符号映射文件 `System.map`，可以看到这一点。然而，在启用 MMU 之前的执行上下文是这样的：物理地址就是实际的硬件地址。这意味着，在启用 MMU 和虚拟内存映射之前的所有代码必须是可重定位的，并且对符号的访问必须经过修正。这涉及到在访问符号地址时添加一个偏移量。一个例子可以使这一点更清晰。

- 初始 RAM 磁盘（initrd）在第 6 章中介绍过。
- 我们在第 4 章中介绍了 `System.map` 文件。

### 16.3.1 早期变量访问

假设在引导过程很早期的一个代码段需要访问变量 `cmd_line`——那么早以至于我们正在执行 1:1 真实到物理的映射。如前所述，这个变量定义在 `head.S` 中，在内核链接时会进入 .data 段。从 Linux 内核的 `System.map` 文件中，你可以找到 `cmd_line` 的链接地址：

```bash
$ cat System.map | grep cmd_line
c0150000 D cmd_line
```

如果我们在真实 = 物理模式（MMU 禁用）下运行，并使用其符号访问此变量，我们将试图读取或写入大于 3GB 的地址。大多数较小的嵌入式系统在这个区域没有任何 RAM，结果将是未定义的或导致崩溃。即使在那个地址有物理 RAM，在引导过程这么早期也不大可能被映射并可访问。因此，我们必须调整对该变量的引用才能访问它。

列表 16-9 重新列出了来自 `head.S` 的一个代码片段，它正是这样做的。

# 列表 16-9

## 变量引用修正

```assembly
relocate_kernel:
addis r9,r26,klimit@ha /* fetch klimit */
lwz r25,klimit@l(r9)
addis r25,r25,-KERNELBASE8h
```

PowerPC `head.S` 中的这段代码片段是我们所描述问题的一个很好的例子。变量 `klimit` 表示内核映像的末尾。它在其他地方被定义为 `char *klimit`。因此，它是一个指针——它是一个包含地址的地址。在列表 16-9 中，我们获取 `klimit` 的地址，将其与之前计算并传入 r26 的偏移量相加，并将结果值存入寄存器 r9。此时，寄存器 r9 包含调整后的 `klimit` 地址的高 16 位，低 16 位为零。该地址由之前计算并传入寄存器 r26 的偏移量进行了调整。

在下一行中，`lwz` 指令使用寄存器 r9 和 `klimit` 的偏移量（`klimit` 地址的低 16 位）作为有效地址，从中加载寄存器 r25。（记住，`klimit` 是一个指针，我们关心的是 `klimit` 指向的值）。此时，寄存器 r25 保存了存储在变量 `klimit` 中的指针。在列表 16-9 的最后一行，你从 r25 中减去内核链接的基地址（`KERNELBASE`），以将指针调整为我们的实际物理地址。如果用 C 语言表示，看起来是这样的：

```c
unsigned int *tmp;            /* represents r25 */
tmp = *klimit;
tmp -= KERNELBASE;
```

总之，我们引用了存储在 `klimit` 中的指针，并调整了其值到我们的真实（物理）地址，以便使用其内容。当内核启用 MMU 和虚拟寻址时，我们就不再需要担心这个问题了——内核将在其链接的地址处运行，无论它实际位于物理内存的何处。

### 16.3.2 板级信息结构

许多引导加载程序用于 PowerPC 平台，但目前仍然没有统一的方法来传递板级特定数据，例如串口波特率、内存大小以及引导加载程序已配置的其他低级硬件参数。来自列表 16-8 的平台初始化文件支持两种不同的方法：存储为 `struct bi_record` 的数据和存储为 `struct bd_info` 的数据。两种方法提供类似的结果：硬件特定数据通过这些结构从引导加载程序传递给内核。

来自列表 16-8，以下是保存引导加载程序提供的硬件配置的代码片段：

```c
struct bi_record *bootinfo = find_bootinfo();

if (bootinfo)
    parse_bootinfo(bootinfo);
else {
    /* Load the bd_t board info structure */
    if (r3)
        memcpy((void*)&__res, (void*)(r3+KERNELBASE),
               sizeof(bd_t));
```

- 每种方法都有其自身的渊源。结构体 `bd_info` 起源于 U-Boot，而结构体 `bi_record` 是统一所有平台的一次尝试。这两种方法都受许多平台支持。

