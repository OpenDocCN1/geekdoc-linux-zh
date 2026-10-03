
# Developing Lift Monitoring and Snow-Making Control for the RPX-CLLF

## LISTING 9.4 Continued

```c
printf("IMMR = 0x%8X\n", immap);
printf("io_base = 0x%8X\n", io_base);
printf("BR5 = 0x%8X\n", immap->_im_memctl.memc_br5);
printf("OR5 = 0x%8X\n", immap->_im_memctl.memc_or5);
printf("PAR = 0x%4X\n", immap->_im_ioport.iop_par);
printf("PADIR = 0x%4X\n", immap->_im_ioport.iop_padir);
```

```c
/* everything initialized */
printf("KERN_INFO %s initialized\n", MODULE_NAME, MODULE_VERSION);
return 0;
```

```c
/* this removes /proc entries if we have an error along the way */
no_snowheater1:
    remove_proc_entry("snowheater1", tb_dir);
no_snowwatervalve3:
    remove_proc_entry("snowwatervalve3", tb_dir);
no_snowwatervalve2:
    remove_proc_entry("snowwatervalve2", tb_dir);
no_snowwatervalve1:
    remove_proc_entry("snowwatervalve1", tb_dir);
no_liftoperatorswitchtop:
    remove_proc_entry("liftoperatorswitchtop", tb_dir);
no_liftoperatorswitchbase:
    remove_proc_entry("liftoperatorswitchbase", tb_dir);
no_lifighspeed:
    remove_proc_entry("lifighighpeed", tb_dir);
no_liftslowspeed:
    remove_proc_entry("liftslowspeed", tb_dir);
no_liftmotorcontroller:
    remove_proc_entry("liftmotorcontroller", tb_dir);
no_liftacains:
    remove_proc_entry("liftacains", tb_dir);

out:
    return rv;
}
```

```c
/* exit cleanup_lifmon_snowcon
 * cleanup_lifmon_snowcon de-asserts the OUTPUT_ENABLE signal.
 * It removes the /proc entry files and prints a message to the system log.
 */
static void __exit cleanup_lifmon_snowcon(void)
{
    immap->_im_ioport.iop_padir &= ~PA0; /* make PA0 an input */

    /* release the ioremap */
    munmap(io_base);

    /* removing the /proc entries */
    remove_proc_entry("liftacains", tb_dir);
    remove_proc_entry("liftmotorcontroller", tb_dir);
    remove_proc_entry("liftslowspeed", tb_dir);
    remove_proc_entry("lifighspeed", tb_dir);
    remove_proc_entry("liftatorswitchbase", tb_dir);
    remove_proc_entry("liftatorswitchtop", tb_dir);
    remove_proc_entry("snowwatervalve1", tb_dir);
    remove_proc_entry("snowwatervalve2", tb_dir);
    remove_proc_entry("snowwatervalve3", tb_dir);
    remove_proc_entry("snowheater1", tb_dir);

    printk(KERN_INFO "%s removed\n", MODULE_NAME, MODULE_VERSION);
}
```

# CHAPTER 9 Memory I/O Interfacing

## LISTING 9.4 Continued

> (Note: The OCR text for some listings was fragmented across pages; the logic above reflects the intended flow of the code provided.)

## SPI 通信与 LM70

### 提示

`LM70` 是美国国家半导体（National Semiconductor）提供的 `LM` 温度传感器系列中的其中一个设备。其他温度传感器（如 `LM78`）提供了额外的内置接口功能。`LM78` 具有一个内置温度传感器、7 个用于监测电压的模拟输入、3 个转速计输入、一个看门狗定时器、一个中断控制器和 32 字节 RAM。更多信息请访问美国国家半导体网站（www.national.com）。

## SPI 通信与 LM70

`LM70` 工作在连续温度转换模式下。在此模式下，`LM70` 作为从设备工作，接受与主机微处理器的通信。它是一个 `SPI` 兼容设备，通过三个信号与主机通信：片选信号 (`/CS`) 和双向串行数据线 (`SI/O`)。与 `LM70` 的同步通信非常简单。由于它会自动确定温度（连续转换模式），`LM70` 不需要像其他温度传感器那样从主机发送温度转换命令。此外，`SPI` 总线不支持多个设备；因此，与 `LM70` 的 `SPI` 通信不需要数据包格式或地址信息。`SPI` 通信包括：主机拉低 `LM70` 的 `/CS` 线，在发送 16 个时钟脉冲的同时在 `SI/O` 信号上读取 `LM70` 的输出，然后释放片选信号。`LM70` 在串行时钟信号的下降沿输出 10 位温度（最高有效位 [MSB] 先行）、3 个高位和 2 个未定义位。这种 11 位的温度表示是一个补码字，最低位 (LSB) 分辨率为 0.25°C。

让我们通过检查两个温度示例的位来明确这个温度值。如果温度为 25°C，与 `LM70` 的通信将返回二进制值 `0000 0100 1001 1111`，它等于 `0x049F`。前五位有效位不包含温度信息，但它们会影响温度值的大小。这些位通过将温度值除以 32（即 $2^5$）来移除。`0x049F` 除以 32 等于 `0x64`，等于 100。每个最低位对应 0.25°C；因此，100 乘以 0.25°C 等于 25°C。如果温度为 -25°C，与 `LM70` 的通信将返回二进制值 `1111 0011 1001 1111`，它等于 `0xF39F`。除以 32 得到值 `0xF9C`，对应 -100。-100 乘以 0.25°C 等于 -25°C。

`LM70` 数据表包含串行总线时序和开关特性。这些规格规定了通信速度的上限，但在本设计中这不需要担心。事实上，本设计特意减慢了同步通信以增加设计的可靠性。通常，`Trailblazer` 目标板将位于通信机柜或机箱内。板载的温度传感器将很近（在 20 英尺以内），用于测量外部温度。使用慢速同步通信使线路驱动器克服长线带来的额外电容。

与 `LM70` 温度传感器通信的设备驱动程序执行五个步骤：

1. 它在 `SC` 高电/`CS` 高电时初始化串行通信。通过拉低 `/CS` 进入起始条件。
2. 它通过拉低 `SC` 进行数据传输。`LM70` 随后用第一位信息主动驱动 `SI/O` 信号。
3. 它拉高 `SC`，然后对 `SI/O` 信号上的第一个数据位进行采样。
4. 它继续翻转 `SC` 信号并采样 `SI/O` 直接收到 16 位。
5. 它通过拉高 `/CS` 进入停止条件并终止通信。

## 将 LM70 连接到 x86 并行打印端口

`LM70` 的 `SPI` 信号线——`/CS`、`SC` 和 `SI/O` 以及电源线和地 (`GND`) 直接连接到并行端口（见图 10.1）。该端口驱动 `/CS` 和 `SC`，但不驱动 `SI/O`。`LM70` 驱动 `SI/O` 线，该线返回串行数据流。由于其连续转换模式，无需向传感器发送数据。

| x86 并行打印端口 | 引脚 | 功能 | LM70 数字温度传感器 |
| :--- | :--- | :--- | :--- |
| | D1 | 片选 | /CS |
| | D2 | 串行时钟 | SC |
| Status 5 | SELECT | 串行数据 | SI/O |
| | GND | GND | GND |

图 10.1 LM70 温度传感器连接到 x86 并行打印端口。

### 提示

在连接接口电路之前，检查你的 x86 并行打印端口信号电压。某些打印端口使用 +5V，而较新的主板使用 +3.3V。你可能无法通过 +3.3V 信号为 +5 设备供电。或者可能会通过将 +3.3V 设备连接到 +5V 信号而损坏它们。

## SPI 通信与 LM70

x86 `LM70` 设备驱动程序通过并行端口连接实现 `SPI` 信号通信。该驱动程序通过 `/proc` 条目为用户提供温度数据。

> （注：提供的 OCR 文本似乎存在碎片或重复的代码痕迹，已根据逻辑进行处理。）

# 第 10 章 同步串行通信接口

## 列表 10.1（续）

```c
outb(data, SPPDATOPORT); /* 将数据写入并行端口 */
}
```

```c
/*
 * 函数 getTemperature
 * 此函数与 LM70 进行 SPI 通信。
 * LM70 在 SC 信号的下降沿上产生串行输出。
 * 此例程在 SC 信号上升沿后读取该串行流的 SI/O 线。
 * LM70 先发送最高位 (MSB)，此例程
 * 执行位移操作。SC 和 /CS 信号被刻意减慢，
 * 以为带有额外电容的长通信线留出稳定时间。
 *
 * 返回
 * getTemperature 函数返回以摄氏度为单位的温度
 * 精度为 1 度的增量
 *
 * 此例程不执行通信错误检查或
 **/
int getTemperature(void)
{
    unsigned char i;
    int temperature;

    assertCS(CS); /* 进入起始条件 */
    udelay(DELAY);

    temperature = 0;
    for (i = 0; i < 16; i++) {
        clkLow();
        udelay(DELAY);
        clkHigh();
        udelay(DELAY);
        temperature = ((temperature << 1) | readBit());
        /* 平移温度位，然后将输入位或入最低位 (LSB) */
    }

    deassertCS();

    /*
     * 现在我们需要对温度值进行缩放。如果温度低于零，简单地右移
     * 位无法执行正确的操作。移位会在 MSB 中引入 0，
     * 导致负符号位。整数除以 32 可以
     * 保留符号位并消除最后 5 个未使用的位。
     *
     * 在此时，除以 32 之后，temperature 包含
     * LSB 位的计数，其中 1 个 LSB 等于 0.25C。
     * 再次除以 4 可将温度按 1 度的增量进行缩放。
     */

    temperature /= 128; /* 32 * 4 = 128 */

    return temperature;
}
```

```c
/*
 * 函数 proc_read_temperature
 * 当用户对 /proc/trailblazer/temperature 执行读取操作时，调用此函数。
 * 此函数将页面缓冲区填充为摄氏度温度值
 */
static int proc_read_temperature(char *page, char **start, off_t off,
                                 int count, int *eof, void *data)
{
    int len, temp;

    temp = getTemperature();
    len = sprintf(page, "%d", temp); /* 若转换为华氏度使用 temp * 9 / 5 + 32 */

    return len;
}
```

```c
/*
 * 函数 init_LM70_x86
 * 此初始化函数创建 /proc/trailblazer 目录
 *并在其中创建一个温度条目，然后初始化
 * LM70 温度传感器
 */
static int __init init_LM70_x86(void)
{
    int rv = 0;

    /* 创建 trailblazer /proc 项 */
    tb_dir = proc_mkdir("trailblazer", NULL);
    if (tb_dir == NULL) {
        rv = -ENOMEM;
        goto out;
    }
    tb_dir->owner = THIS_MODULE;

    /* 创建温度文件并允许所有人可读 - 0444 */
    temperature_file = create_proc_entry("temperature", 0444, tb_dir);
    if (temperature_file == NULL) {
        rv = -ENOMEM;
        goto no_temperature;
    }
    temperature_file->data = NULL;
    temperature_file->read_proc = proc_read_temperature;
    temperature_file->write_proc = NULL;
    temperature_file->owner = THIS_MODULE;

    initializeSensor();

    /* 所有初始化完成 */
    printk(KERN_INFO "%s is initialized\n", MODULE_NAME, MODULE_VERSION);
    return 0;

no_temperature:
    remove_proc_entry("trailblazer", NULL);
out:
    return rv;
}
```

```c
/*
 * 函数 cleanup_LM70_x86
 * 此清理函数会关闭传感器电源并移除
 * /proc/trailblazer 目录和温度条目。
 */
static void __exit cleanup_LM70_x86(void)
{
    powerdownSensor();

    remove_proc_entry("temperature", tb_dir);
    remove_proc_entry("trailblazer", NULL);

    printk(KERN_INFO "%s removed\n", MODULE_NAME, MODULE_VERSION);
}
```

```c
module_init(init_LM70_x86);
module_exit(cleanup_LM70_x86);

MODULE_AUTHOR("Craig Willoughby");
MODULE_DESCRIPTION("Trailblazer LM70_x86");
EXPORT_NO_SYMBOLS;
```

`LM70_x86.c` 设备驱动程序包含四个主函数：

- `init_LM70_x86`：此初始化函数创建 `/proc/trailblazer` 目录并在其中创建一个温度条目，然后初始化 `LM70` 温度传感器。
- `proc_read_temperature`：当用户对 `/proc/trailblazer/temperature` 执行读取操作时调用此函数。此函数将页面缓冲区填充为摄氏度温度值。
- `getTemperature`：此例程与 `LM70` 进行 `SPI` 通信。
- `cleanup_LM70_x86`：此清理函数会关闭传感器电源并移除 `/proc/trailblazer` 目录和温度条目。

使用 `SSP` 控制器的 `Serial Port 4` 端口需要配置以下两个寄存器中的位：

- `SSP` 控制寄存器 1 (`SSCR1`) 配置位设置：
  - 接收 FIFO 中断允许 (`RIE`)：0 屏蔽中断
  - 发送 FIFO 中断允许 (`TIE`)：0 屏蔽中断
  - 环回模式 (`LBM`)：0 禁用环回模式
  - 串行时极性 (`SPO`)：0 空闲时保持 `SC` 低电平
  - 串行时相位 (`SPH`)：0 增加 1 个时钟周期
  - 外部时钟选择 (`ECS`)：0 使用内部时钟

- `SSP` 控制寄存器 0 (`SSCR0`) 配置位设置：
  - 数据大小选择 (`DSS`)：1111 选择 16 位长度
  - 帧格式 (`FRF`)：00 选择 Motorola SPI
  - 同步串口启用 (`SSE`)：1 Enable
  - 串行速率 (`SCR`)：1111111 选择最慢时钟
