
# SPI 通信与 LM70

嵌入式设计通常实现位暴法（bit-banging）例程来与同步串行设备进行通信。在列表 10.1 所示的接口示例中，名为 `getTotal` 的位暴法函数与连接到 x86 并行打印端口的 LM70 通信。可以增加通信延迟，以允许主机 CPU 与温度传感器之间使用更长的通信信号线。

此示例仅时钟化了 16 位温度数据。虽然位宽很短，但位暴法操作需要 CPU 周期。对于长的串行通信流，位暴法操作可能会消耗大量的 CPU 资源。这会影响其他程序的性能，因为 Linux 调度器没有实现设备驱动程序。

其他 CPU 可以包含用于同步通信的专用外设，从而减轻了 CPU 执行位暴法周期的负担。ARM SA-1110 和 PowerPC MPC860 都包含了 SPI 同步通信控制器。

# 将 LM70 连接到 MediaEngine

MediaEngine 设计允许通过 J13 控制器访问 ARM SA-1110 的串口 4。串口 4 包含两个同步控制器：多媒体通信端口 (MCP) 和 SSP。CPU 配置决定了哪一个控制器连接到串口 4 的引脚上。如果不选择任何控制器，这些引脚将变为通用输入/输出 (I/O) 引脚。Project trailblazer 可以为 ARM 处理器实现位暴法算法，但他们没有这样做。SA-1110 SSP 控制器支持 SPI，这使其非常适合与 LM70 进行同步通信。（有关 SSP 的更多信息，请参阅 SA-1110 开发人员手册的第 11.2.7 节“SPP 操作”。）图 10.3 显示了 MediaEngine 与 LM70 温度传感器之间的连接。

MediaEngine LM70 设备驱动程序使用 I/O 操作。也就是说，它不使用 CPU 中断或直接内存访问 (DMA)。与 LM70 的同步通信很短且简单；引入中断和 DMA 通道使用会增加不必要的复杂。

程序化 I/O 轮非常简单。在 SPI 通信之前，会清除 SA-1110 SSP 的第一个接收（FIFO）缓冲区。`getTotal` 函数启动 SPI 通信，然后持续监控 SSP 忙标志状态寄存器 (SSR) 位。当 SPI 通信完成时，忙标志被清除，SSP 数据寄存器 (SSDR) 包含 16 位温度读数。使用带有 SSP 控制器的串口 4 进行程序化 I/O 需要配置以下两个寄存器中的位：

- SSP 控制寄存器 1 (`SSCR1`) 配置位设置：
- 接收 FIFO 中断允许 (`RIE`): 0 屏蔽中断
- 传输 FIFO 中断允许 (`TIE`): 0 屏蔽中断
- 环回模式 (`LBM`): 0 禁用环回模式
- 串行时钟极性 (`SPO`): 0 空闲时保持 SC 低电
- 串行时钟相位 (`SPH`): 0 增加 1 个时钟周期延迟
- 外部时钟选择 (`ECS`): 0 使用内部时钟
- SSP 控制寄存器 0 (`SSCR0`) 配置位设置：
- 数据大小选择 (`DSS`): 1111 选择 16 位长度
- 帧格式 (`FRF`): 00 选择 Motorola SPI
- 同步串口启用 (`SSE`): 1 启用
- 串行时钟速率 (`SCR`): 1111111 选择慢时钟

MediaEngine 的 `LM70_mediaengine.c` 设备驱动程序位于列表 10.2，需要将 SA-1110 `SSCR1` 寄存器配置为 `0x0000`，并将 `SSCR0` 寄存器配置为 `1111 1111 1000 1111` (`0xFF8F`)。

图 10.3 LM70 温度传感器连接到 MediaEngine。

# 列表 10.2 LM70_mediaengine.c 设备驱动

```c

/*

* LM70_mediaengine v1.0 11/05/01

* www.embeddedlinuxinterfacing.com

 *

* 此代码的原始位置位于

* http://www.embeddedlinuxinterfacing.com/chapters/10/

 *

* 版权所有 (C) 2001 Craig Hollollabaugh

 *

* 本程序是免费软件；你可以根据自由软件基金会

* 发布的通用公共许可证条款分发和/或修改

*  许可证的第 2 版本，或（根据你的选择）任何后续版本。

 *

* 分发本程序的希望是它是有用的，但

* 不提供任何保证；不包含隐含的商业性

* 或针对特定用途的适用性保证。更多信息请参阅 GNU

* 库通用公共许可证。

 *

* 你应该在收到此程序的同时获得 GNU 库通用

* 许可证副本；如果没有，请写信给

* Free Software Foundation, Inc.

* 59 Temple Place, Suite 330, Boston, MA 02111-1307 USA

*/

LM70_mediaengine.c 基于 Erik Mouw 的 procfs_example.c

* 更多信息，请参阅《The Linux Kernel Procfs Guide》，Erik Mouw

* http://kernelnewbies.org/documents/kdoc/procfs-guide.html

*/

/* LM70_mediaengine

* 此设备驱动程序演示了使用 SA-1110 SPI 控制器

* 与 LM70 传感器通信。驱动程序通过轮询 I/O

* 检查 SSR 的忙标志而不是使用中断。

* 驱动程序创建了一个名为

* /proc/trailblazer/temperature 的 proc 条目。*/

```
```bash
gcc -O2 -DKERNEL -I/usr/src/linux -c LM70_mediaengine.c -o /tmp/LM70_mediaengine.o
```
```c#include <linux/module.h>
#include <linux/kernel.h>
#include <linux/procfs.h>
#include <linux/delay.h>
#include <linux/init.h>
#include <linux/io.h>
#include <asm/delay.h>

#define MODULE_VERSION "1.0"
#define MODULE_NAME "LM70"

static struct proc_entry *tb_dir;

/*
* function getTemperature
* 此函数通过轮询 I/O
* 与 LM70 通信，检查 SSR 的忙标志
* 而不是使用中断。
* 此文件。
*/
int getTemperature(void)
{
    unsigned char i;
    int temperature, status;

    /* 在 SPI 通信前需要清除 FIFO */
    for (i = 0; i < 16; i++)
    {
        status = readw(ssp_base + SSSR_OFFSET); /* 读取状态寄存器 */
        if ((status & SPP_RNE) == 0) /* 接收 FIFO 是否空？ */
            break;
        temperature = readw(ssp_base + SSDR_OFFSET); /* 读取 FIFO */
    }

    /* 启动 SPI 通信，需要向传输 FIFO 馈值 */
    outw(0x00, ssp_base + SSDR_OFFSET);

    /* 等待忙 标志未设置并读取接收 FIFO */
    for (i = 0; i < 20; i++)
    {
        status = readw(ssp_base + SSSR_OFFSET); /* 读取状态寄存器 */
        if ((status & SPP_BSY) == 0) /* 我们还在进行 SPI 帧吗？ */
            break;
        udelay(1000); /* 等待一会儿 */
    }

    temperature = readw(ssp_base + SSDR_OFFSET); /* 读取接收 FIFO */

    /* 调试用取消下行的注释 */
    // printf("temp: i is %d, temperature is 0x%04X\n",i, temperature);

    /*
    * 现在我们缩放温度值。如果温度为负，
    * 简单的移位无法执行正确操作。移位会在
    * MSB 中引入 0，导致丢失负符号位。整数除以 32
    * 保留了符号位并消最后 5 位。
    * 在此处，除以 32 之后，temperature 包含
    * LSB 位计数，其中 1 LSB 等于 0.25C。额外的
    * 除以 4 按 1 度增量缩放温度。
    */
    temperature /= 128; /* 32 * 4 = 128 */

    return temperature;
}

/*
* function proc_read_temperature
* 当用户对 /proc/trailblazer/temperature 执行读取操作时，
* 调用此函数。此函数用以摄氏 C 为单位的温度填充缓冲区。
*/
static int proc_read_temperature(char *page, char **start, off_t off,
    int count, int *eof, void *data)
{
    int len, temp;

    temp = getTemperature();
    len = sprintf(page, "%d\n", temp); /* 这里是 temp * 9 / 5 + 32 用于 F */

    return len;
}
```

## 列表 10.2 续

```c
/*
* function init_LM70_mediaengine 创建 /proc/trailblazer
* 此初始化函数创建 /proc/trailblazer 
* 目录并在其中创建一个温度条目，然后初始化
* LM70 温度传感器
*/
static int __init_LM70_mediaengine(void)
{
    unsigned int r;
    int rv = 0;

    /* 创建 trailblazer /proc_entry */
    tb_dir = proc_mkdir("trailblazer", NULL);
    if(tb_dir == NULL) {
        rv = -ENOMEM;
        goto out;
    }
    tb_dir->owner = THIS - THIS_MODULE;

    /* 创建温度文件并允许所有用户可读 - 0444 */
    temperature_file = create_proc_entry("temperature", 0444, tb_dir);
    if(temperature_file == NULL) {
        rv = -ENOMEM;
        goto no_temperature;
    }
    temperature_file->data = NULL;
    temperature_file->read_proc = &proc_read_temperature;
    temperature_file->write_proc = NULL;
    temperature_file->owner = THIS_MODULE;

    ssp_base = ioremap_nocache(SSP, SSP_base);
    printk("ssp_base = %0x%x\n", ssp_base);

    /* SSCR1 二进制值 0000 0000 0000 0 = 0x0000
    * 外部时钟选择 (ECS)     0 使用内部时钟
    * 串时钟相位 (SPH),      0 添加 1 个时钟周期延迟
    * 串时钟极性 (SPO),   0 在空闲时保持 SC 为低电
    * 回环模式 (LBM)            0 禁用环回模式
    * 发送 FIFO 中断允许 (TIE) 0 屏蔽中断
    * 接收 FIFO 中断允许 (RIE), 0 屏蔽中断
     */
    writel(0x0000, ssp_base + SSCR1_OFFSET);

    /*
    * SSC0 二进制值 1111 1111 1111 = 0xFF8
    * 数据大小选择 (DSS),               1111 选择 16 位长度
    * 帧格式 (FRF),                选择 Motorola SPI
    * 同步串行启用 (SSE), 1 为启用
    * 串行时钟速率 (SCR),            1111111 选择最慢时钟
     */
    writel(0xFF8, ssp_base + SSCR0_OFFSET);

    /* 读取寄存器并打印结果 */
    r = readl(ssp_base + SSCR1_OFFSET);
    printk("SSCR1                = 0x%04X\n",r);
    r = readl(ssp_base + SSCR0_OFFSET);
    printk("SSCR0                = 0x%04X\n",r);

    /* 所有初始化完成 */
    printk(KERN_INFO "%s s initialized\n", MODULE_NAME, MODULE_VERSION);
    return 0;

no_temperature:
    remove_proc_entry("trailblazer", NULL);
out:
    return rv;
}

/*
* function cleanupLM70_mediaengine
* 此函数关闭传感器电源并移除
* /proc/trailblazer 目录和温度条目
*/
static void __exit_cleanup_LM70_mediaengine(void)
{
    munmap(ssp_base);

    remove_proc_entry("temperature", tb_dir);
    remove_proc_entry("trailblazer", NULL);

    printk(KERN_INFO "%s %s removed\n", MODULE_NAME, MODULE_VERSION);
}

module_init(init_LM70_mediaengine);
module_exit(cleanup_LM70_mediaengine);

MODULE_AUTHOR("Craig Hollabaugh");
MODULE_DESCRIPTION("Trailblazer LM70_mediaengine");

EXPORT_NO_SYMBOLS;
```

`LM70_mediaengine.c` 设备驱动包含四个主要函数：

- `init_LM70_mediaengine`——这是设备驱动运行的初始化函数，它创建了 `/proc` 目录条目 `trailblazer` 和 `trailblazer/temperature`。随后它配置了 SA-110 的 `SSCR1` 和 `SSCR0` 寄存器，启用了串口4上的 SSP 控制器。

- `proc_read_temperature`——当用户对 `/proc/trailblazer/temperature` 执行读取操作时，就会调用此函数。`proc_read_temperature` 调用 `getTemperature`。

- `getTemperature`——此函数使用与 LM70 通信的 SSP 控制器。`getTemperature` 函数返回以摄氏度增加的值。

- `cleanup_LM70_MediaEngine`——这是设备驱动的清理函数，用于移除 `/proc` 目录条目。

图 10.4 显示的示波器采集显示了位流 `0000.1011.0011.1111`，它对应于 `22.25°C`。

到为止，Project Trailblazer 的工程师们将 LM70 温度传感器连接到了 x86 并行打印口。

# 第 10 章 同步串行通信接口

此 `ls` 输出显示模块 `i2c-core.o`、`i2c-algo-bit.o`、`i2c-dev.o` 和 `i2c-pport.o` 已编译成功。

- 使用以下命令在 `/dev` 目录下创建一个主设备号为 89、次设备号为 0 的字符设备文件：

```
root@tdev1[581]: mknod /dev/i2c0 89 0
```

- 加载 `i2c-core`、`i2c-algo-bit`、`i2c-pport` 和 `i2c-dev` 模块：

```
root@tdev1[515]: cd /root/i2c-2.6.1/
root@tdev1[516]: insmod i2c-core.o
root@tdev1[517]: insmod i2c-algo-bit.o
root@tdev1[518]: insmod i2c-pport.o
root@tdev1[519]: insmod i2c-dev.o
```

- 将 SAA1064 的 SDA 和 SCL 线连接到 x86 打印口，并将电源和地线连接到软磁盘接口器。`i2c-pport` 的作者编写了将 I2C 设备连接到并行打印端口的说明（参见 `/root/i2c-2.6.1/doc/i2c-pport`）。`i2c-pport` 设备驱动程序使用打印口控制线，允许双向通信。SDA 的控制线自动进位信号和 SCL 的控制线初始化信号。图 10.5 显示了连接四个驱动七位段数码 LED 的 SAA1064 之间连接的完整电路原理图。

> 提示
