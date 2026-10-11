
# 在设备驱动程序中使用 Regmap API

`regmap_read(data->regmap, INT_SOURCE, &int_stat);`

```c
/*
 * 如果发生了 SINGLE_TAP 事件，将调用 adxl345_do_tap 函数
 * 并将 ACT_TAP_STATUS 寄存器作为参数
 */
if (int_stat & (SINGLE_TAP)) {
    dev_info(data->dev, "single tap interrupt occurred\n");

    if (tap_stat & TAP_X_EN) {
        iio_push_event(indio_dev, IIO_MOD_EVENT_CODE(IIO_ACCEL, 0, IIO_MOD_X, IIO_EV_TYPE_THRESH, 0), data->timestamp);
    }

    if (tap_stat & TAP_Y_EN) {
        iio_push_event(indio_dev, IIO_MOD_EVENT_CODE(IIO_ACCEL, 0, IIO_MOD_Y, IIO_EV_TYPE_THRESH, 0), data->timestamp);
    }

    if (tap_stat & TAP_Z_EN) {
        iio_push_event(indio_dev, IIO_MOD_EVENT_CODE(IIO_ACCEL, 0, IIO_MOD_Z, IIO_EV_TYPE_THRESH, 0), data->timestamp);
    }
}

return IRQ_HANDLED;
```

## 9. IIO 触发器缓冲区设置

在 `adxl345_core_probe(struct)` 例程中，使用 `devm_iio_triggered_buffer_setup()` 函数分配一个 IIO 触发器缓冲区。该函数结合了设置触发器时通常执行的常用任务。它分配缓冲区并设置了“pollfunc top half”和“pollfunc bottom half”处理程序。`adxl345_trigger_handler` `pollfunc bottom half` 处理程序在内核线程上下文中运行，所有的处理都在这里完成。它从 ADXL345 设备读取三个轴的数据，并使用 `iio_push_to_buffers_with_timestamp()` 函数将值存储在内部缓冲区（连带有在 top half 获取的时间戳）。`pollfunc top half` 应该尽可能少，因为它在中断上下文中运行。最常见的操作是记录当前时间戳，因如此，你可以使用 `iio_pollfunc_store_time(devm_)` 函数。在调用 `devm_iio_triggered_buffer_setup()` 之前，`iio_dev` 结构体应该已经完全初始化但尚未注册。在实践，这意味着该函数应该在调用 `devm_iio_device_register()` 之前调用。

```c
int adxl345_core_probe(struct device *dev, struct regmap *regmap, const char *name)
{
    struct iio_dev *indio_dev;
    struct adxl345_data *data;

    /* pf->timestamp = iio_get_time_ns(); */
    devm_iio_triggered_buffer_setup(dev, indio_dev,
    &iio_pollfunc_store_time,
    adxl345_trigger_handler, NULL);

    devm_iio_device_register(dev, indio_dev);

    return 0;
}

static irqreturn_t adxl345_trigger_handler(int irq, void *p)
{
    struct iio_poll *pf = p;
    struct iio_dev *indio_dev = pf->indio_dev;
    struct adxl345_data *data = iio_priv(indio_dev);

    /* 6 字节轴 + 2 字节填充 + 8 字节时间戳 */
    u16 buf[8];
    int i, ret, j = 0, base = DATA0;
    u16 sample;

    /* 读取开启的通道数据 */
    for_each_bit(i, indio_dev->active_mask) {
        ret = regmap_read(data->regmap, base + i * sizeof(sample), &sample);
        if (ret < 0)
            goto done;
        buf[j++] = sample;
    }

    iio_push_to_buffers_with_timestamp(indio_dev, buf, pf->timestamp);

done:
    iio_notify(indio_dev);
    return IRQ_HANDLED;
}
```

## 10. 声明驱动支持的设备

```c
static const struct of_device_id adxl345_dt[] = {
    {compatible = "maxim,adxl345"},
};
MODULE_DEVICE_TABLE(of, adxl345_dt);
```

## 11. `device_id` 结构

```c
static const struct spi_device_id adxl345_id[] = {
    {name = "adxl345"},
};
MODULE_DEVICE_TABLE(spi, adxl345_id);
```

## 12. 添加 `spi_driver` 结构

```c
static struct spi_driver adxl345_driver = {
    .driver = { .name = "adxl345", .of_match_table = adxl345_dt },
    .probe = adxl1345_spi_probe,
};
```

## 13. 模块注册

```c
module_spi_driver(adxl345_driver);
```

## 14. 编译部署

在 `linux-5.4` 目录下创建一个新的 `adxl345.c` 并将 `adxl345.o` 添加到 `Makefile`，然后编译并部署到树莓派：

```bash
# 第 12-1: adxl345.c
```

```bash
# 第 12-2: Makefile
```

# 在设备驱动程序中使用 Regmap API

### BW_RATE 位域

```c
/* BW_RATE 位域 */
#define LOW_POWER (1 << 4)
#define RATE(x) ((x) & 0xF)
```

### POWER_CTL 位域

```c
/* POWER_CTL 位域 */
#define PCTL_MEASURE (1 << 3)
#define PCTL_STANDBY 0x00
```

### DATA_FORMAT 位域

```c
/* DATA_FORMAT 位域 */
#define ADXL_FULL_RES (1 << 3)
```

### FIFO_CTL 位域

```c
/* FIFO_CTL 位域 */
#define FIFO_MODE(x) ((x) & 0x03) << 6
#define FIFO_BYPASS 0
#define FIFO_FIFO 1
#define FIFO_STREAM 2
#define SAMPLES(x) ((x) & 0x1F)
```

### FIFO_STATUS 位域

```c
/* FIFO_STATUS 位域 */
#define ADXL_X_AXIS 0
#define ADXL_Y_AXIS 1
#define ADXL_Z_AXIS 2
```

### 中断轴启用

```c
/* 中断轴启用 */
#define ADXL_TAP_EN (1 << 2)
#define ADXL_TAP_Y_EN (1 << 1)
#define ADXL_TAP_Z_EN (1 << 0)
```
