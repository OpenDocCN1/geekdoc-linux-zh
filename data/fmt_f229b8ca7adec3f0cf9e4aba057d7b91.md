
```c
#ifndef _DT_BINDINGS_MAXIM_MAX1300_H
#define _DT_BINDINGS_MAXIM_MAX1300_H

#define PORT_MODE_0 0
#define PORT_MODE_1 1
#define PORT_MODE_2 2
#define PORT_MODE_3 3
#define PORT_MODE_4 4
#define PORT_MODE_5 5
#define PORT_MODE_6 6
#define PORT_MODE_7 7
#define PORT_MODE_8 8
#define PORT_MODE_9 9
#define PORT_MODE_10 10
#define PORT_MODE_11 11
#define PORT_MODE_12 12

#define ADC_SAMPLES_1 0
#define ADC_SAMPLES_2 1
#define ADC_SAMPLES_4 2
#define ADC_SAMPLES_8 3
#define ADC_SAMPLES_16 4
#define ADC_SAMPLES_32 5
#define ADC_SAMPLES_64 6
#define ADC_SAMPLES_128 7

/* ADC voltage ranges */
#define ADC_TAGE_RANGE_NOT_SELECTED 0
#define ADC_TAGE_RANGE_PLUS10 1 // 0 to +5V range
#define ADC_TAGE_RANGE_PLUSMINUS5 2 // -5V to +5V range
#define ADC_TAGE_RANGE_MINUS10 3 // -10V to 0 range
#define ADC_TAGE_RANGE_PLUS25 4 // 0 to +2.5V range

/* DAC voltage ranges mode */
#define DAC_TAGE_RANGE_NOT_SELECTED 0
#define DAC_TAGE_RANGE_PLUS10 1
#define DAC_TAGE_RANGE_PLUSMINUS5 2
#define DAC_TAGE_RANGE_MINUS10 3

#endif /* _DT_BINDINGS_MAXIM_MAX1300_H */
```

# LAB 11.1 驱动描述

驱动的主要代码部分将通过三个不同的类别进行描述：作为 SPI 交互的工业框架、作为 IIO 设备的工业框架以及 GPIO 驱动接口。`MAX11300` 驱动基于 Paul Cerciel 的 `AD5592R` 驱动：

`https://elixir.bootlin.com/linux/latest/source/drivers/iio/dac/ad5592r.c`

## 作为 SPI 交互的工业框架

这些是主要代码部分：

### 1. 包含所需的头文件

```c
#include <linux/spi/spi.h>
```

### 2. 创建一个 `spi_driver` 结构体

```c
static struct spi_driver max11300_spi_driver = {
    .driver = {
        .name = "max11300",
        .of_match_table = of_match_ptr(max11300_of_match),
    },
    .probe = max11300_spi_probe,
    .remove = max11300_spi_remove,
    .id_table = max11300_spi_ids,
};
module_spi_driver(max11300_spi_driver);
```

### 3. 作为驱动注册到 SPI 总线

```c
module_spi_driver(max11300_spi_driver);
```

### 4. 将 `"maxim,max11300"` 添加到驱动支持的设备列表中。与 `MAX11300` DT 节点中 `compatible` 属性对应的兼容变量矩阵

```c
static const struct of_device_id max11300_of_match[] = {
    {.compatible = "maxim,max11300"},
};
MODULE_DEVICE_TABLE(of, max11300_of_match);
```

### 5. 定义一个 `spi_device_id` 结构体数组

```c
static const struct spi_device_id max11300_spi_ids[] = {
    {.name = "max11300"},
};
MODULE_DEVICE_TABLE(spi, max11300_spi_ids);
```

### 6. 使用读写函数初始化 `max11300_rw_ops`，这些函数将通过 SPI 访问 `MAX11300` 设备的寄存器

```c
/*
 * 使用回调函数初始化 struct max11300_rw_ops
 * 将通过 SPI 读/写 MAX11300 寄存器
 */
static const struct max11300_rw_ops max11300_rw_ops = {
    .reg_write = max11300_reg_write,
    .reg_read = max11300_reg_read,
    .reg_read_differential = max11300_reg_read_differential,
};

/* 写 MAX11300 寄存器的函数 */
static int max11300_reg_write(struct max11300_state *st, u8 reg, u16 val)
{
    struct spi_device *spi = container_of(st->dev, struct spi_device, dev);

    struct spi_transfer t[] = {
        .tx_buf = &st->tx_cmd,
        .len = 1,

        .tx_buf = &st->tx_msg,
        .len = 2,
    };

    /* 要通过 SPI 传输，命令字节的 LSB 必须为 0 */
    st->tx_cmd = (reg << 1);

    /*
     * 在小端 CPU 中，存储在 "val" 变量高地址的
     * 字节（DAC 的 MSB）将存储在 "st->tx_msg" 变量的低地址
     * 使用 cpu_to_be16()
     */
    st->tx_msg = cpu_to_be16(val);

    return spi_sync_transfer(spi, t, ARRAY_SIZE(t));
}

/* 在 SE 模式下读 MAX11300 寄存器的函数 */
static int max11300_reg_read(struct max11300_state *st, u8 reg, u16 *value)
{
    struct spi_device *spi = container_of(st->dev, struct spi_device, dev);
    int ret;

    struct spi_transfer t[] = {
        .tx_buf = &st->tx_cmd,
        .len = 1,

        .rx_buf = &st->rx_msg,
        .len = 2,
    };

    dev_info(st->dev, "read SE channel\n");
```

## 第 11 章

## Industrial I/O 子系统
