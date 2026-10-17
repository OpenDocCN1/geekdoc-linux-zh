
```
= setenv bootargs console=ttyS1,115200 root=/dev/nfs rs=ip-dhcp kgdbwait
kgdb8250=ttyS1,115200
= tfftp 000000 mpc8548.uImage
Speed: 1000, full duplex
Using etSECO device
TFTP from server 192.168.0.9; our IP address is 192.168.0.18
Filename `8548/uImage`.
Load address: 0x060000
Loading: #################################################################################################################################################################################
done
Bytes transferred = 1854347 (1c4b8 hex)
= tfftp 000000 mpc8548.dtb
Speed: 1000, full duplex
Using etSECO device
TFTP from server 192.168.0.9; our IP address is 192.168.0.18
Filename `8548/dtb`.
Load address: 0xc00000
##
done
Bytes transferred = 16384 (400 hex)
=> bootm 600000 - c000000
## Booting kernel from Legacy Image at 06000000 ...
Image Name: Montavista Linux Kernel 6/2.27/frees
Image Type: PowerPC Linux Kernel Image (gzip compressed)
Data Size: 1854283 Bytes = 1.8 MB
Load Address: 00000000
Entry Point: 00000000
Verifying Checksum ... OK
## Flattened Device Tree blob at 0xc00000
Booting using the fdt blob at 0xc00000
Uncompressing Kernel Image ... OK
Loading Device Tree to 0x07f9000, end 0x7ffffff ... OK
kgdb8250: ttyS1 init delayed, use io:/mmio/mbase syntax for early init.
Using MPC85xx CDS machine description
```

# 列表 14-1 继续 内存映射：CAM0=256Mb, CAM1=0Mb, CAM2=0Mb residual: 0Mb

```
Linux version 2.6.27.28.freescale-8548cds.0908109110 (chris@pluto) (gcc version 4.3.3 (MontVista Linux Sourcery G++ 4.3-2317) #1 PREEMPT Mon Mar 29 11:09:48 EDT
console [udbg0] enabled
setup_arch: bootmem
mpc85xx_cds_setup_arch()
<.. many messages deleted ..>
serial: 8250/16550 driver 4 ports, IRQ sharing enabled
serial8250.0: tty0 at MMIO 0xe004500 (irq = 42) is a 1650A
serial8250.0: tty1 at MMIO 0xe004600 (irq = 42) is a 1650A
console handler: [udbg0] -> real [tty1]
kgdb: Registered I/O driver kgdb8250.
kgdb: Waiting for connection from remote gdb...
```

大部分启动序列在第 7 章“引导加载程序”中关于 U-Boot 的介绍中非常熟悉。回想第 7 章，内核命令行由 U-Boot `bootargs` 环境变量定义。注意我们添加了 `kgdb` 参数，该参数指示内核强制执行早期断点并等待主机调试器（你的交叉调试器）连接。

请注意，启动序列并没有完成。由于我们在命令行中放置了 `kgdb`，内核一直完成初始化，直到串口驱动程序加载并命中了一个预定义的断点。在此处，它将无限期地等待外部调试器的连接。

你还应该注意新的内核命令行参数。这种特定的架构（Power）和平台（8548CDS）使用 8250 串口驱动以及由 `../drivers/serial/8250_kgdb.c` 实现的特殊 8250 基 KGDB 驱动。你必须告诉 KGDB 使用哪个串口进行调试，其语法与使用控制设备类似。

现在内核已就绪并正在等待主机调试器，我们可以开始调试会话。我们在开发工作站上调用交叉 `gdb` 并连接到目标机。

> ⁴ 在某些架构和平台上，你可以配置 KGDB 使用以太网甚至 USB。

一旦你设置了初始断点并执行了 `continue` 命令，你随时可以通过向你的交叉 `gdb` 发送 Ctrl-C 来停止执行。列表 14-4 展示了这种操作方法。

# 列表 14-4 进程内核调试话

```
(gdb) c
Continuing.

<<<<< 用户在此处输入 Ctrl-C >>>>>>>

Program received signal SIGTRAP, Trace/breakpoint trap.
0x0058048 in kgdb_breakpoint () at kernel/kgdb.c:1802
1802 wmb(); /* * 断点前的同步点 */
(gdb) bt
#0 0x0058048 in kgdb_breakpoint () at kernel/kgdb.c:1802
#1 0x019bcc in kgdb8250_interrupt (irq=<value optimized out>, dev_id=<value optimized out>) at drivers/serial/8250_kgdb.c:145
#2 0x005aa4f0 in handle_irq_event (irq42, action=0xc58af20) at kernel/irq/c:140
#3 0x005cc1c in handle_fast_io_irq (irq42, desc=0xc039a950) at kernel/irq/chip.c:424
#4 0x0004b04 in do_IRQ (regs=value optimized out) at include/linux/irq.h:289
#5 0x000f310 in ret_from_except_full ()
#6 0x0008144 in cpu_idle () at arch/powerpc/kernel/idle.c:59
#7 0x002d022c in rest_init () at init/main.c:481
#8 0x036e75c in start_kernel () at init/main.c:691
#9 0x0000030 in skip_inv()
(gdb)
```

你可以在列表 14-4 中看到编译器优化的效果。这将在 14.3.2 节中进一步讨论。

## 14.2.4 与 KGDB 共享控制台串口

虽然可以使用单个串口同时用于系统控制台和通过串口进行 KGDB，但这显然并非理想选择。取决于你的架构和平台，KGDB 的完善程度各异。一旦离开 x86 架构，情况就会变得不那么确定。KGDB 有许多连接选项，包括串口、以太网端口，在某些平台上甚至还有 USB。可以确定的是，这些选项中...

本书的其他地方提到过：如果你认为自己将需要使用 KGDB 进行内核调试，那么增加一个串口的成本是完全合理的，特别是如果为了满足成本目标，在可以在生产环境中将其移除。通过它所节省的烦恼（即开发者的时间）将远超增加的开发成本带来的回报。

要在控制台和 KGDB 之间共享串口，你需要两个命令行参数。使用内核命令行 `kgdb` 来指定要使用哪个串口，并使用 `kgdbcon` 指定你将把此端口与软控制台共享。在使用串口控制台时使用 `kgdboc` 参数，其方式类似于在内核命令行上描述设备：

```
kgdb kgdboc=tty1,115200
```
