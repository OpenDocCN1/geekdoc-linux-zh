
```
/*
 * function interrupt_latency
 * 此函数是中断 1 的处理程序。它使用 do_gettimeofday
 * 设置 tv2 结构体。它清除 GPIO01。
 */
void void_interrupt_latency(int irq, void *dev_id, struct pt_regs *regs)
{
    do_gettimeofday(&tv2);
    writel(GPIO1, gpio_base + GPCR_OFFSET); /* 取消中断信号 */
    interruptcount++;
}

/*
 * function proc_read_interrupt_latency
 * 对 /proc/interrupt_latency 发生读取操作时，内核会执行
 * 此函数。此函数设置 tv1 结构体。它拉高 GPIO01，
 * 这应该立即导致中断 1 发生。处理程序记录
 * tv2 并拉低 GPIO01。此函数返回 tv2 和 tv1
 * 之间的时间差。
 */

static int proc_read_interrupt_latency(char *page, char **start, off_t off,
    int count, int *eof, void *data)
{
    int len;

    do_gettimeofday(&tv1);
    writel(GPIO1, gpio_base + GPCR_OFFSET); /* 拉高中断信号 */

    len = sprintf(page, "Start %i.%06i\nFinish %i.%06i\nlatency %6i/Count %6i\n",
        (int) tv1.tv_sec, (int) tv1.tv_use,
        (int) tv2.tv_sec, (int) tv2.tv_use,
        (int) tv2.tv_use - interruptcount);
    return len;
}

/*
* function init_interrupt_latency
* 此函数创建 /proc 目录项 interrupt_latency。它
 * 向 Linux 请求中断 1，然后配置中断控制器。
 */
static int __init_init_interrupt_latency(void)
{
    unsigned long r;
    int rv = 0;

    interrupt_latency_file = create_proc_entry("interrupt_latency", 0444, NULL);
    if(interrupt_latency_file == NULL) {
        return -ENOMEM;
    }

    interrupt_latency_file->data = NULL;
    interrupt_latency_file->read_proc = &proc_read_interrupt_latency;
    interrupt_latency_file->write_proc = NULL;
    interrupt_latency_file->owner = THIS_MODULE;

    ic_base = ioremap_nocache(IC, ICLEN);
    printk("ic_base = 0x%08X\n",ic_base);

    /* 从 linux 请求中断 */
    rv = request_irq(INTERRUPT, interrupt_interrupt_latency, 0,
        "interrupt_latency", NULL);
    if (rv) {
        printf("Can't get interrupt %d\n", INTERRUPT);
        goto no_interrupt_latency;
    }

    /* 打印中断控制器状态位 */
    r = readl(ic_base + ICIP_OFFSET);
    printf("ICIP = 0x%08X\n", r);
    r = readl(ic_base + ICMR_OFFSET);
    printf("ICMR = 0x%08X\n", r); /* INT1 在此处设置标志位 */
    r = readl(ic_base + ICLR_OFFSET);
    printf("ICLR = 0x%08X\n", r);
    r = readl(ic_base + ICFP_OFFSET);
    printf("ICFP = 0x%08X\n", r);

    /* 获取用于更改寄存器的 GPIO 基 */
    gpio_base = ioremap_nocache(GPIO, GPIO1);
    printf("\ngpio_base = 0x%08X\n", gpio_base);

    /* 配置 GPIO01 为输出 */
    writel(gdpr | GPIO01, gpio_base + GDPR_OFFSET);

    /* 设置 GPIO01 无复用功能 */
    writel(gafr & ~GPIO01, gpio_base + GAFR_OFFSET);

    writel(GPIO01, GPCR_OFFSET); /* 清除 GPIO01 */
    gdpr = readl(gpio_base + GDPR_OFFSET); /* 保留 gpio 位 */
    printf("GDPR = 0x%08X\n", gdpr);

    gafr = readl(gpio_base + GAFR_OFFSET); /* 保留 gafr 位 */
    printf("GAFR = 0x%08X\n", gafr);

    r = readl(gpio_base + GPLR_OFFSET);
    printk("GPLR %d=0x%08X\n", r);

    grer = readl(gpio_base + GRER_OFFSET); /* 保留 grer 位 */
    printk("GRER %d=0x%08X\n", grer);

    /* 设置 GPIO01 升沿中断 */
    writel(grer | GPIO01, gpio_base + GRER_OFFSET);

    /* 使用 ARM 特有的 Linux 函数请求边缘中断 */
    set_GPIO_IRQ_edge(GPIO_RISING_EDGE);
    printk("set_GPIO_IRQ_edge\n");

    r = readl(gpio_base + GFER_OFFSET);
    printk("GFER %d=0x%08X\n", r);

no_interrupt_latency:
    // ... 清理代码
}
```

# 列表 11.3 继续

+   * 版权所有 (C) 2001 Craig Hollabaugh
* 本程序是免费软件；您可以根据自由软件基金会
* 发布的 GNU Library General Public License 条款对其进行重新分发和/或
* 修改，具体取决于该许可证的第 2 个
* 版本，或（根据您的选择）任何后续版本。
* 本程序的分发是希望它是有用的，
* **不提供任何保证**；甚至不提供关于商品性或
* 特定用途的适用性的暗示保证。更多信息请参见 GNU
* Library General Public License。
* 您应该已随本程序收到一份 GNU Library General Public
* License 副本；如果没有收到，请写信至：
* Free Software Foundation, Inc.,
* 59 Temple Place, Suite 330, Boston, MA 02111-1307 USA

```
interrupt_latency_rpxcllf.c 基于 Erik Mrowk 的 procfs_example.c。
了解更多信息，请参阅《Linux Kernel Procfs Guide》，Erik Mrowk
 http://kernelnewbies.org/documents/kdoc/procfs-guide/lkprocfsguide.html
```

```
powerpc-linux-gcc -O2 -D_KERNEL -DMODULE -I/usr/src/powerpc-linux/include \
-c interrupt_latency_rpxcllf.c \
-o /tmp/boot/powerpc-rootfs/tmp/interrupt_latency_rpxcllf.o
```

+   interrupt_latency_rpxcllf
* 该模块使用 PA0 和 IRQ2 测量 RPX-CLLF 的瞬时中断延迟。
* 配置 SIU 以产生 IRQ2 边沿中断。
* 将 PA0 配置为输出，然后设置 PA0 就会产生一个
* 上沿，从而产生中断。

+   * 《Motorola MPC860 PowerQUIC 用户手册》第 11.5.1 节

+   * 插入模块后，读取 /proc/interrupt_latency 将断言 PA0
* 产生中断。中断处理程序将撤销 PA0 信号。
* 在示波器上查看。包含一个中断计数器以帮助调试噪声
* 中路。

```
/*
#include <linux/module.h>
#include <linux/kernel.h>
#include <linux/init.h>
#include <linux/proc_fs.h>

#include <asm/io.h>

#include <linux/interrupt.h>
#include <asm/irq.h>
#include <asm/mpcxx.h>
#include <asm/8xx_immap.h>
#include <asm/time.h>

#define MODULE_VERSION "1.0"
#define MODULE_NAME "interrupt_latency_rpxllf"

volatile image_t *immap;
static void *io_base;
```

```
#define PA0 0x8000
#define SIEL_ED2 0x08000000
```

```
int interruptcount = 0;
#define INTERRUPT SIQ IRQ2
```

struct time tv1, tv2; /* do_gettimeofofday 填充这些 * /

static struct proc_dir_entry *interrupt_latency_file;

```
/*
* function interrupt_latency
* 此函数是中断 2 的中断处理程序。它使用 do_gettimeofday
* 设置 tv2 结构。它清除 PA0。
*/
```

```
void interrupt_latency(int irq, void *dev_id, struct pt_regs *regs)
{
    do_gettimeofday(&tv2);
    immap->ioport_iopadat = PA0; /* 撤销中断信号 * /

interruptcount++;
}
```

```
/*
* function proc_read_interrupt_latency
* 当对 /proc/interrupt_latency 进行读取操作时，内核
* 执行此函数。此函数设置 tv1 结构。它断言
* PA0，这应该立即导致中断 2 发生。处理程序
* 记录 tv2 并撤销 PA0。此函数返回 tv2 和 tv1
* 之间的时间差。
*/
static int proc_read_interrupt_latency(char *page, char **start, off_t off,
    int count, int *eof, void *data)
{
    int len;

do_gettimeofday(&tv1);
    imapmap->im.ioport_padat &= PA0; /* 断言中断信号 */
```

```
len = sprintf(page, "Start %9i%%06i\nFinish %9i%%06i\nLatency %16i\n\nCount %18i\n\n", (int) tv1.tv_sec, (int) tv1.tv_use,
    (int) tv2.tv_sec, (int) tv2.tv_use,
    (int) tv2.tv_use - tv1.tv_use,
    interruptcount);

return len;
}
```

```c
/*
* function init_interrupt_latency
* 此函数创建 /proc 目录条目 interrupt_latency。它向
* Linux 请求中断 2，然后配置中断控制器。
*/
static int init_interrupt_latency(void)
{
    unsigned long r;
    int rv = 0;

    interrupt_latency_file = create_proc_entry("interrupt_latency", 0, NULL);
    if(interrupt_latency_file == NULL) {
```

```c
return -ENOMEM;
}

interrupt_latency_file->data = NULL;
interrupt_latency_file->read_proc = &proc_read_interrupt_latency;
interrupt_latency_file->write_proc = NULL;
interrupt_latency_file->owner = THIS_MODULE;

/* request interrupt from linux */
rv = request_8xxirq(INTERRUPT, interrupt_latency, 0,
    "interrupt_latency", NULL);

if ( rv ) {
printk("Can't get interrupt");
printk("Can't get interrupt\n", rv);
powerpc-linux-gcc -O2 -D_KERNEL -DMODULE -I/usr/src/powerpc-linux/include \
-c interrupt_latency_rpxcllf.c \
-o /tmp/boot/powerpc-rootfs/tmp/interrupt_latency_rpxcllf.o
printk("Can't get interrupt\n", rv);
```

```'t 错误：
```

* interrupt_latency_rpxcllf.c based on procfs_example.c by Erik Mrowk.
* For more information, please see, The Linux Kernel Procfs Guide, Erik Mrowk
* http://kernelnewbies.org/documents/kdoc/procfs-guide/lkprocfsguide.html

```

```

powerpc-linux-gcc -O2 -D_KERNEL -DMODULE -I/usr/src/powerpc-linux/include \

-c interrupt_latency_rpxcllf.c \

-o /tmp/boot/powerpc-rootfs/tmp/interrupt_latency_rpxcllf.o

```

+   interrupt_latency_rpxcllf
* 该模块使用 PA0 和 IRQ2 测量 RPX-CLLF 的瞬时中断延迟。
* 配置 SIU 以产生 IRQ2 边沿中断。
* 将 PA0 配置为输出，然后设置 PA0 就会产生一个
* 上沿，从而产生中断。

+   * 《Motorola MPC860 PowerQUIC 用户手册》第 11.5.1 节

+   * 插入模块后，读取 /proc/interrupt_latency 将断言 PA0
* 产生中断。中断处理程序将撤销 PA0 信号。
* 在示波器上查看。包含一个中断计数器以帮助调试噪声
* 中路。
/*
```

```
#include <linux/module.h>

#include <linux/kernel.h>

#include <linux/init.h>

#include <linux/proc_fs.h>

#include <asm/io.h>

#include <linux/interrupt.h>

#include <asm/irq.h>

#include <asm/mpcxx.h>

#include <asm/8xx_immap.h>

#include <asm/time.h>

#define MODULE_VERSION "1.0"

#define MODULE_NAME "interrupt_latency_rpxllf"

volatile image_t *immap;

static void *io_base;
```

```

```
#define PA0 0x8000

#define SIEL_ED2 0x08000000
```

```

```
int interruptcount = 0;

#define INTERRUPT SIQ IRQ2
```
