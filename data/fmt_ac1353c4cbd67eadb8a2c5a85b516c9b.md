
![](img/c075000fa5feb4594b1442d501c7c8d8_344_0.png)

**图 11.2** MZ104 的中断信号。

### 在 MediaEngine1 上测量中断延迟

MediaEngine 的通用输入/输出信号 1 (`GPI01`) 位于目标板的连接器 `J10` 上，可以在上升沿、下降沿或两者同时产生 `SA-1110` 中断 1。Project Trailblazer 的工程师们决定将中断控制器配置为上升沿触发。（更多信息，请参阅《Intel SA-1110 开发者手册》第 9.2 节“中断控制器”）。`SA-1110` 的中断控制器连接到 `GPI01` 输入端，该端负责监控引脚状态，无论引脚被配置为输入还是输出。工程师们将 `GPI01` 设置为输出，然后产生中断信号。图 11.3 显示了 `GPI01` 输出寄存器 (`GPSR`/`GPCR`) 的内部连接、输入电平寄存器 (`GPLR`) 的连接、与中断控制器的连接以及与示波器的外部连接。

列表 11.2 显示了 `interrupt_latency_mediaengine.c` 驱动程序的源代码。

# 第 11 章 使用中断进行计时

![](img/c075000fa5feb4594b1442d501c7c8d8_345_0.png)

图 11.3 用于测量中断延迟的 MediaEngine 连接。

## 列表 11.2 `interrupt_latency_mediaengine.c` 设备驱动程序

```
/*

* interrupt_latency_mediaengine v1.0 11/25/01

* www.embeddedlinuxinterfacing.com

* 本段代码的原始位置位于

* http://www.embeddedlinuxinterfacing.com/chapters/11/

* Copyright (C) 2001 by Craig Hollabaugh

* This program is free software; you can redistribute it and/or modify

it under the terms of the GNU General Public License as

public by the Free Software Foundation; either version 2 of the License, or at your option) any later version.

* This program is distributed in the hope that it will be useful, and

WITHOUT ANY WARRANTY; even without the implied warranty of

MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU Library General Public License for more details.

* You should have received a copy of the GNU General Public License along with this program; if not, write to the

Free Software Foundation, Inc.

* 59 Temple Place, Suite 330, Boston, MA 02111-1307 USA

*/

/*

* interrupt_latency_mediaengine.c based on procfs_example.c by Erik Mrow

* For more information, please参阅《The Linux Kernel Procfs Guide》，Erik Mrow

* http://kernelnewbies.org/documents/kdoc/procfs-guide/lkprocfsguide.html

*/
```

## 列表 11.2 继续

```c
arm-linux-gcc -O2 -D_KERNEL__ -DMODULE -I/usr/src/arm-linux/include \
-c interrupt_latency_mediaengine.c
-o /tftpoot/arm-rootfs/tmp/interrupt_latency_mediaengine.o
*/
```

```c
/* interrupt_latency_mediaengine.c 模块
* 该模块使用 GPIO01 测量 MediaEngine 的瞬时中断延迟
* 配置 GRER 以产生 GPIO01 上升沿中断
* 将 GPIO01 设置为输出，然后设置 GPIO01 会产生
* 上升沿触发中断。GRER 由 ARM 内核代码重置，因此 仅设置寄存器本身是不够的。使用
* ARM 专用函数 set_GPIO_IRQ_edge。更多信息请查看内核源码。
*
* 插入模块后，读取 /proc/interrupt_latency 将断开 GPIO
* 产生中断。中断处理程序将取消 GPIO 信号。
* 在示波器上查看。包含一个中断计数器以帮助调试噪声较大的
*中断线。
*/
```

```c
#include <linux/module.h>
#include <linux/kernel.h>
#include <linux/init.h>
#include <linux/proc_fs.h>
```

```c
#include <asm/io.h>
```

```c
#define MODULE_VERSION "1.0"
#define MODULE_NAME "interrupt_latency_mediaengine"
/* 参见 9.1.1.1 Intel StrongARM SA-1100 微处理器开发者手册 */
/* 这些项也定义在 arch SA-1100.h 中，但定义方式不同*/
#define GPIO 0x90040000 /* GPIO 寄存器基地址 */
#define GPLR_OFFSET 0x00
#define GDPR_OFFSET 0x04
#define GPSR_OFFSET 0x08
#define GPCR_OFFSET 0x0C
#define GAFR_OFFSET 0x1C
#define GRER_OFFSET 0x10
#define GFER_OFFSET 0x14
#define GEDR_OFFSET 0x18
```

## 列表 11.2 继续

```c
#define GPIOLEN 0x20
#define GPIO01 0x00000002
#define IC 0x90050000 /* 中断控制器基地址 */
#define ICIP_OFFSET 0x00
#define ICMR_OFFSET 0x04
#define ICLR_OFFSET 0x08
#define ICFP_OFFSET 0x10
#define ICLEN 0x20
static void *ic_base, *gpio_base;
unsigned long gdpr, gafr, grer;
int interruptcount = 0;
struct timeval tv1, tv2;
#define INTERRUPT 1
static struct proc_entry *interrupt_latency_file;
/* function interrupt_latency
* 该函数是中断 1 的处理程序。它使用 get_timeofday
* 设置 tv2。然后清除 GPIO1。*/
void interrupt_latency(int irq, void *dev_id, struct regs *regs)
{
    get_timeofday(&tv2);
    writel(GPIO01, gpio_base + GPCR_OFFSET); /* 取消中断信号 */
    interruptcount++;
}
/* function proc_read_latency
* 当 /proc/interrupt_latency 进行读取操作时，内核
* 执行此函数。它设置 tv1。触发 GPIO01 会导致
* 中断发生。处理程序记录 tv2 并取消 GPIO1。
* 此函数返回 tv2 和 tv1 之间的时间。*/
```

11.2 继续

```c
static int proc_read_latency(char *page, char *start, off_t off,
    int count, int *eof, void *data)
{
    int len;
    get_timeofday(&tv1);
    writel(GPIO01, gpio_base + GPSR_OFFSET); /* 产生中断信号 */
    len = sprintf(page, "Start %ld%06ld\nFinish %ld%06ld\nLatency %ld%06ld\n",
        (long)tv1.sec, (long)tv1.use, (long)tv2.sec, (long)tv2.use,
        (long)(tv2.sec - tv1.sec), (long)(tv2.use - tv1.use),
        interruptcount);
    return len;
}
/* function init_latency
* 此函数创建 /proc 目录项 interrupt_latency。
* 从 Linux 请求中断 1 并配置中断控制器。*/
static int __init init_latency(void)
{
    unsigned long r;
    int rv = 0;
    interrupt_latency_file = create_proc_entry("interrupt_latency", 044, NULL);
    if (interrupt_latency_file == NULL) {
        return -ENOMEM;
    }
    interrupt_latency_file->data = NULL;
    interrupt_latency_file->read_proc = &proc_read_latency;
    interrupt_latency_file->write_proc = NULL;
    interrupt_latency_file->owner = THIS_MODULE;
    ic_base = ioremap_nocache(IC, ICLEN);
    printk("ic_base = 0x%08lx\n", ic_base);
```

## 列表 11.2 继续

```c
/* 从 Linux 请求中断 */
r = request_irq(INTERRUPT, interrupt_latency, 0,
    "interrupt_latency", NULL);
if (rv) {
    printf("Can't interrupt %d\n", INTERRUPT);
    goto no_interrupt_latency;
}
```

```c
/* 输出中断状态位 */
r = readl(ic_base + ICIP_OFFSET);
printf("ICIP = 0x%08lx\n", r);
r = readl(ic_base + ICMR_OFFSET);
printf("ICMR = 0x%08lx\n", r); /* 此处设置 INT1 位 */
r = readl(ic_base + ICLR_OFFSET);
printf("ICLR = 0x%08lx\n", r);
r = readl(ic_base + ICFP_OFFSET);
printf("ICFP = 0x%08lx\n", r);
```

```c
/* 获取更改寄存器所需的 GPIO 基地址 */
gpio_base = ioremap_nocache(GPIO, GPIOLEN);
printf("gpio_base = 0x%08lx\n", gpio_base);
```

```c
/* 配置 GPIO01 为输出 */
/* 将 GPIO01 设置为输出 */
writel(gdpr | GPIO01, gpio_base + GDPR_OFFSET);
```

```c
/* 设置 GPIO01 无复用功能 */
writel(gafr & -GPIO01, gpio_base + GAFR_OFFSET);
```

```c
writel(GPIO01, gpio_base + GPCR_OFFSET); /* 清除 GPIO01 */
gdpr = readl(gpio_base + GDPR_OFFSET); /* 保留 gdpr 位 */
printf("GDPR = 0x%08lx\n", gdpr);
```

```c
gafr = readl(gpio_base + GAFR_OFFSET); /* 保留 gafr 位 */
printf("GAFR = 0x%08lx\n", gafr);
```

## 列表 11.2 继续

```c
r = readl(gpio_base + GPLR_OFFSET);
printf("GPLR = 0x%08lx\n", r);
```

```c
grer = readl(gpio_base + GRER_OFFSET); /* 保留 grer 位 */
printf("GRER = 0x%08lx\n", grer);
```

```c
/* 设置 GPIO01 产生上升沿中断 */
writel(grer | GPIO01, gpio_base + GRER_OFFSET);
```

```c
/* 使用 ARM 专用函数请求边缘中断 */
set_GPIO_IRQ_edge(GPIO01, GPIO_RISING_EDGE);
printf("GPIO_IRQ_edge %s\n", GPIO_RISING_EDGE);
```

```c
r = readl(gpio_base + GRER_OFFSET);
printf("GRER = 0x%08lx\n", r);
```

```c
r = readl(gpio_base + GFER_OFFSET);
printf("GFER = 0x%08lx\n", r);
```

```c
r = readl(gpio_base + GEDR_OFFSET);
printf("GEDR = 0x%08lx\n", r);
```

```c
/* 全部初始化完成 */
printk(KERN_INFO "%s %s initialized\n", MODULE_NAME, MODULE_VERSION);
return 0;
}
no_interrupt_latency:
    remove_proc_entry("interrupt_latency", NULL);
}
```

```c
static void __exit cleanup_latency(void)
{
    free_irq(INTERRUPT, NULL); /* 释放中断 */
}
```

# 第 11 章 使用中断进行计时

## 列表 11.2 续

```
writel(gpdr, gpio_base + GPDR_OFFSET); /* restore gdpr */
writel(gafr, gpio_base + GAFR_OFFSET); /* restore gafr */
writel(grer, gpio_base + GRER_OFFSET); /* restore grer */
```

```
ionmap(ic_base);
ionmap(gpio_base);
```

```
remove_proc_entry("interrupt_latency", NULL);
```

```
printk(KERN_INFO "%s %s removed/in", MODULE_NAME, MODULE_VERSION);
}
```

```
module_init(init_interrupt_latency);
module_exit(cleanup_interrupt_latency);
```

```
MODULE_AUTHOR("Craig Hollabaugh");
MODULE_DESCRIPTION("interrupt_latency proc module");
```

```
EXPORT_NO_SYMBOLS;
```

`interrupt_latency_mediaengine.c` 设备驱动程序执行的操作与 `interrupt_latency_x86.c` 设备驱动程序执行的操作相似。在 `interrupt_latency_mediaengine.c` 调用 `set_GPIO_IRQ_edge` 时存在细微差异。ARM 内核维持了一个 GPIO 上沿寄存器（`GRER`）的内部副本。调用 `set_GPIO_IRQ_edge` 会通知 ARM 内核将 `GRER` 寄存器包含 `GPIO1` 位。以下控制台输出显示了 MediaEngine 目标的实时结果：

```bash
204# insmod interrupt_latency_mediaengine.o
ic_base = 0xC2C80200
ICIP = 0x00000000
ICMR = 0x0D400803
ICLR = 0x00000000
```
