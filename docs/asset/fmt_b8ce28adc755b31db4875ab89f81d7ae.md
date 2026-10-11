
```c
int8_t LTC2422_read(uint8_t *adc_channel, int32_t *code, uint16_t timeout)
{
    int fd;
    int ret;
    int32_t value;
    uint8_t buffer[4];
    unsigned int val;

struct spi_ioc_transfer tr = {
    /* 无数据需要发送 */
    .tx_buf = 0,
    .rx_buf = (unsigned long) buffer, /* 存储接收到的数据 */
    .delay_usecs = 0, /* 无延迟 */
    .speed_hz = SPI_CLOCK_RATE, /* SPI 时钟频率 (Hz) */
    .bits_per_word = 8, /* 传输大小 */
    .len = 3 /* 传输字节数 */
};

/* 打开设备 */
fd = open("/dev/spidev2.1", O_RDWR);
if (fd < 0)
{
    close(fd);
    return (1);
}

/* 执行传输 */
ret = ioctl(fd, SPI_IOC_MESSAGE(1),&tr);
if (ret < 1)
{
    close(fd);
    return (1);
}

/* 关闭设备 */
close(fd);

value = buffer[0] << 16;
value |= buffer[1] << 8;
value |= buffer[2];

/* 确定通道号 */
*adc_channel = (&value & SPI_DATA_CHANNEL_MASK) ? 1 : 0;
printf("the value is %x\n", value);

/* 返回代码 */
*code = value;
return(0);
}

/* 从 ADC 代码计算电压 */
float LTC2422_voltage(uint32_t adc_code, float LTC2422_lsb)
{
    float adc_voltage;
    if (adc_code & 0x200000)
    {
        adc_code &= 0xFFFF;
        adc_voltage=(float)adc_code*LTC2422_lsb;
    }
    else
    {
        adc_code &= 0xFF;
        adc_voltage=(float)adc_code*LTC2422_lsb;
    }
    return(adc_voltage);
}

void delay(unsigned int ms)
{
    usleep(ms*1000);
}

int8_t read_adc()
{
    float adc_voltage;
    int32_t adc_code;
    uint8_t adc_channel;
    int32_t adc_array[2];
    /* 读取数据。由于驱动程序，你不知道是哪个通道 */
    LTC2422_read(&adc_channel, &adc_code, 1000);
    /* 获取当前数据 */
    adc_array[adc_channel] = adc_code;
    /* 驱动程序会切换通道 */
    delay(1000);
    LTC2422_read(&adc_channel, &adc_code, 1000);
    adc_array[adc_channel] = adc_code;
    /* DC934 板连接到 VOUTA 为 CH1 */
    adc_voltage = LTC2422_voltage(adc_array[1], LTC2422_lsb);
    printf(" ADC A : %f\n", adc_voltage);

    /* DC934 板连接到 VOUTB 为 CH0 */
    adc_voltage = LTC2422_voltage(adc_array[0], LTC2422_lsb);
    printf(" ADC B : %f\n", adc_voltage);

    return(0);
}

int main(void)
{
    read_adc();
    printf("Application terminated\n");
    return 0;
}
```

# 第 11 章

## 用于设备驱动的工业 I/O 子系统

“使用 i2c-utils 工具包与 LTC2607 交互（在加载模块之前）” `i2cdect` 是 i2c 工具包中的一个工具。它可以从用户空间探测 i2c 总线并报告正在使用的地址。

`root@x7dsabres:~# i2cdect -1` /* 列出可用总线，LTC2607 在总线 2 上 */

| i2c-3 | i2c | 30a50000.i2c | I2C adapter |
| i2c-1 | i2c | 30a30000.i2c | I2C adapter |
| i2c-2 | i2c | 30a4000.i2c | I2C adapter |
| i2c-0 | i2c | 30a20000.i2c | I2C adapter |

`root@x7dsabres:~# i2cdect -y 2` /* 查看检测到的设备，查看 LTC2607 地址 */

```
0 1 2 3 4 5 6 7 8 9 a b c d e f
-- -- -- -- -- -- -- -- -- -- -- -- -- --
00: -- -- -- -- -- -- -- -- -- -- -- -- -- --
20: -- -- -- -- -- -- -- -- -- -- -- -- -- --
30: -- -- -- -- -- -- -- -- -- UU -- -- -- --
40: -- -- -- -- -- -- -- -- -- -- -- -- -- --
50: -- -- -- -- -- -- -- -- -- -- -- -- -- --
60: 60 -- 72 73 -- -- -- -- -- -- -- -- -- --
70: -- -- -- -- -- -- -- -- -- -- -- -- -- --
```

`root@x7dsabres:~# insmod ltc2607_imx_dual_device.ko` /* 加载模块。你会看到 probe() 函数被调用两次。原因是驱动匹配了具有相同 DT 兼容属性的设备。现在你可以在用户空间管理两个设备 */

```
ltc2607 2-007
```

## 用于设备驱动的工业 I/O 子系统

ADC B : 0.0011

应用程序已终止

```
root@imx7dsabsred:~# cd /sys/bus/io/devices/iio:device2/ /* 修改到 iio_device2/ */
root@imx7dsabsred:~# /sys/bus/io/devices/iio:device2# echo 65535 > out_voltage2_raw /* 将输出设置为 5 V */
root@imx7dsabsred:~# ./LTC2422-spidev /* 使用你的应用获取两个 ADC 输出 *
the value is 6ff6ac
the value is 6ff6b
the value is 2ffc6b
```

ADC A : 4.9928

ADC B : 4.9956

应用程序已终止

```
root@imx7dsabsred:~# rmmod ltc2607_imx_dual_device.ko /* 移除模块 *
ltc2607 2-0072: DAC_remove()
ltc2607 2-0072: DAC_remove()
```

### 实验 11.3：“IIO 子系统 ADC” 模块

你已经通过 `spidev` 驱动在用户态控制了 `LTC2422` 驱动。现在你将使用 `IIO` 框架开发 `LTC2422` 驱动。你将使用该驱动通过 `SPI` 读取 `ADC` 通道；然后将使用用户应用程序 `LTC2422_app` 将这些数字转换为真实的模拟电压。

驱动的主要部分分为三类描述：设备树、作为 `SPI` 交互的工业框架以及作为 `IIO` 设备的工业框架。

### 设备树

修改 `arch/dts/` 文件夹下的设备树文件，包含你的 `DT` 驱动设备节点。`DT` 节点必须有一个 `compatible` 属性，与驱动程序之一 `_device_id_` 结构体中存储的字符串完全相同。
