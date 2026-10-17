
6. 写入 `iio_info` 结构体。`sysfs` 数据通道属性的读/写用户空间操作映射到以下内核回调函数：

```c
static const struct iio_info max11300_info = {
    .read_raw = max11300_read_adc,
    .write_raw = max11300_write_dac,
};
```

`max11300_read_adc()` 函数包含一个 `switch(mask)`，根据收到的 `info_mask` 值选择不同的任务。如果收到的 `info_mask` 值为 `IIO_CHAN_INFO_RAW = "raw"`，则调用 `max11300_reg_write()` 函数，该函数通过 `SPI` 事务将 `DAC` 值写入选定的端口 `DAC` 寄存器。

当 `max11300_read_adc()` 函数接收到 `info_mask` 值 `IIO_CHAN_INFO_RAW = "raw"` 时，它首先读取 `ADC` 通道地址到 `ADC` 端口模式。一旦选择了 `ADC` 端口模式，就会调用 `max11300_reg_read()` 或 `max11300_reg_read_differential()` 函数，这些函数通过 `SPI` 事务读取选端口 `ADC` 数据寄存器的值。返回的 `ADC` 值存储在 `val` 变量中，然后通过 `IIO_VAL_INT` 标识符返回给用户空间。

# GPIO 驱动接口

`MAX11300` 驱动还将包含一个 `GPIO` 控制器，用于配置和控制在设备 `DT` 节点中选择为 `GPIO` 的 `MAX11300` 端口（端口1和端口3）。

在本书的第 5 章中，你将看到如何使用 `GPIOLib` 框架的 `GPIO` 描述符消费者接口从内核空间控制 `GPIO`。

大多数处理器使用复合引脚控制器。这些复合引脚控制器将在 `GPIO` 功能之上产生中断，并允许将处理器的 `I/O` 引脚复用为 `GPIO`。`pintrl` 驱动将 `gpio_chip` 结构体注册到内核，将 `irq_chip` 结构体注册到 `IRQ` 系统，并将 `pintrl_desc` 注册到 `Pintrl` 子系统。`GPIO` 和引脚控制器在 `pintrl` 驱动内部通过 `pintrl_add_gpio_range()` 函数相互关联，该函数有一范围需要由选定引脚控制器处理的 `GPIO`。

# 第11 章

## 工业 I/O 子系统

```c
st->gpichip.owner = THIS_MODULE;

/* 注册一个 gpio_chip */
return gpichip_add_data(&st->gpichip, st);
}
```

3. 这些是控制 `MAX11300 GPIO` 控制器 线的回调函数：

```c
/*
* struct gpio_chip_get 回调函数。
* 它获取 GPIO 线的输入值 (0=低, 1=高)
* 通过访问 MAX11300 的 GPI_DATA 器
 */
static int max11300_gpio_get(struct gpio_chip *chip, unsigned int offset)
{
    struct max11300_state *st = gpichip_get_data(chip);
    int ret = 0;
    u16 read_val;
    u8 reg;
    int val;

    mutex_lock(&st->gpio_lock);

    if (st->gpio_offset[offset] == PORT_MODE_3)
        dev_info(st->dev, "the gpio %d cannot be configured in input mode\n", offset);

    /* 对于从 16 到 19 的 GPIO [offset] */
    if (st->gpio_offset[offset] > 0x0F) {
        reg = GPIO_DATA_TO_16_ADDRESS;
        ret = st->ops->reg_read(st, reg, &read_val);
        if (ret)
            goto err_unlock;
    } else {
        reg = GPIO_DATA_15_TO_0_ADDRESS;
        ret = st->ops->reg_read(st, reg, &read_val);
        if (ret)
            goto err_unlock;
    }

    val = (int)read_val;
    val = val << 16;

    if (val & BIT(st->gpio_offset[offset]))
        val = 1;
    else
        val = 0;

    mutex_unlock(&st->gpio_lock);
    return val;

err_unlock:
    mutex_unlock(&st->gpio_lock);
    return ret;
}
```

```c
/* struct gpio_chip set 回调函数。
* 它以 GPIO_ACTIVE_HIGH 模式 (0=低, 1=高) 设置 GPIO 线的输出值
* 写入 max11300 的 GPIO_DATA 器 */
```

```c
static void max11300_gpio_set(struct gpio_chip *chip, unsigned int offset, int value)
{
    struct max11300_state *st = gpiochip_get_data(chip);
    u8 reg = 0;
    unsigned int val = 0;
    mutex_lock(&st->gpio_lock);
    if (st->gpio_offset[offset] == PORT_MODE_1)
        dev_info(st->dev, "the GPIO %d cannot accept this output\n", offset);
    if (value == 1 && (st->gpio_offset[offset] > 0xF)) {
        dev_info(st->dev, "The GPIO output is set high and port_number is %d. Pin is < 0xF\n",
            st->gpio_offset[offset]);
        val = BIT(st->gpio_offset[offset]);
        val << 16;
        reg = GPIO_DATA_19_TO_16_ADDRESS;
        st->ops->reg_write(st, reg, val);
    } else if (value == 0 && (st->gpio_offset[offset] > 0xF)) {
        dev_info(st->dev, "The GPIO output is set low and port_number is %d. Pin is < 0xF\n",
            st->gpio_offset[offset]);
        val &= ~BIT(st->gpio_offset[offset]);
        val << 16;
        reg = GPIO_DATA_19_TO_16_ADDRESS;
        st->ops->reg_write(st, reg, val);
    } else if (value == 1 && (st->gpio_offset[offset] < 0xF)) {
        dev_info(st->dev, "The GPIO output is set high and port_number is %d. Pin is < 0xF\n",
            st->gpio_offset[offset]);
        val |= BIT(st->gpio_offset[offset]);
        reg = GPIO_DATA_15_TO_0_ADDRESS;
        st->ops->reg_write(st, reg, val);
    } else if (value == 0 && (st->gpio_offset[offset] < 0xF)) {
        dev_info(st->dev, "The GPIO output is low and port_number is %d. Pin is < 0xF\n",
            st->gpio_offset[offset]);
