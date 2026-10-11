
```c
static int adxl345_write_raw(struct iio_dev *indio_dev,
  struct iio_chan_spec *chan,
  int val, int val2, long mask)
{
  struct adxl345_data *data = iio_priv(indio_dev);
  switch (mask) {
    case IIO_CHAN_INFO_SAMP_FREQ:
      data->data_rate = RATE(val);
      return regmap_write(data->regmap, BW_RATE, data->data_rate | 
          (data->low_power_mode ? LOW_POWER : 0));
    default:
      return -EINVAL;
  }
}
```

- `adxl345_read_event`：当从用户空间读取带有掩码 `IIO_EV_INFO_VALUE` 和 `IIO_EV_INFO_PERIOD` 的每个轴 sysfs 属性时，该函数返回 `THRESH_TAP` 和 `DUR` 寄存器的值。

```c
static int adxl345_read_event(struct iio_dev *indio_dev,
  struct iio_chan_spec *chan,
  enum iio_event_type type,
  enum iio_event_direction dir,
  enum iio_event_info info,
  int *val, int *val2)
{
struct adxl345_data *data = iio_priv(indio_dev);
switch (info) {
    case IIO_EV_INFO_VALUE:
        *val = data->tap_threshold;
        break;
    case IIO_EV_INFO_PERIOD:
        *val = data->tap_duration;
        break;
    default:
        return -EINVAL;
}

return IIO_VAL_INT;
}
```

- `adxl345_write_event`：当从用户空间返回带有掩码 `IIO_EV_INFO_VALUE` 和 `IIO_EV_INFO_PERIOD` 的每个轴 sysfs 属性时，该函数设置 `THRESH_TAP` 和 `DUR` 寄存器的值。

```c
static int adxl345_write_event(struct iio *indio_dev,
                               const struct iio_chan_spec *chan,
                               enum iio_event_type type,
                               enum iio_event_direction dir,
                               enum iio_event_info info,
                               int val, int val2) {

struct adxl345_data *data = iio_priv(indio_dev);
switch (info) {
    case IIO_EV_INFO_VALUE:
        data->tap_threshold = val;
        return regmap_write(data->regmap, THRESH_TAP, data->tap_threshold);
    case IIO_EV_INFO_PERIOD:
        data->tap_duration = val;
        return regmap_write(data->regmap, DUR, data->tap_duration);
    default:
        return -EINVAL;
}
```

- 查看下面 SPI map 配置和初始化的主要代码行：

```c
static const struct regmap_config adxl345_spi_regmap = {
    .reg_bits = 8,
    .val_bits = 8,
    /* 设置第 7 和 6 位启用多字节读取 */
    .read_flag_mask = BIT(7) | BIT(6),
};
```

```c
static int adxl345_spi_probe(struct spi_device *spi)
{
    struct regmap *regmap;
    /* 从驱动结构体获取 id */
    const spi_device_id *id = spi_get_device_id(spi);
    regmap = devm_regmap_init_spi(spi, &adxl345_spi_regmap);
    return adxl345_core_probe(spi->dev, regmap, id->name);
}
```

- `adxl345_core_routine` 返回一个线程中断。驱动将添加线程中断以处理单击中断。在线程中断中，中断处理程序 `adxl345_event_handler` 在线程内部执行。允许阻塞，这对于 SPI 设备通常是必要的，中断处理程序需要与其通信。在你的驱动中，你将在中断处理程序中使用 `regmap_read()` 函数通过 SPI 与 ADXL345 设备通信。单击事件将使用 `io_push_function()` 发送到用户空间。

```c
/* 请求的线程中断 */
devm_request_threaded_irq(dev, dev->irq, NULL, adxl345_event_handler, IRQ_TRIGGER_HIGH | IRQ_ONESHOT, dev_name(dev), indo_dev);

/* 中断服务程序 */
static irqreturn_t adxl345_event_handler(int irq, void *handle)
{
    u32 tap_stat, *stat;
    struct iio_dev *indio_dev = handle;
    struct adxl345_data *data = iio_priv(indio_dev);

    data->timestamp = iio_get_time_ns(indio_dev);

    if (data->tap_axis_control & (TAP_X_EN | TAP_Y_EN | TAP_Z_EN)) {
        regmap_read(data->regmap, ACT_TAP_STATUS, &stat);
    }
    else
        tap_stat = 0;
```

- 读取 `INT_SOURCE` `0x30` 寄存器
- 清除中断

# 在 Linux 设备驱动程序中使用 Regmap API

```c
regmap_read(data->regmap, INT_SOURCE, &int_stat);
```

```c
/*
* 如果发生了 SINGLE_TAP 事件，将调用 axl345_do_tap 函数
* 并将 ACT_TAP_STATUS 寄存器作为参数传入
*/
```

```c
if (int_stat & (SINGLE_TAP)) {
    dev_info(data->dev, "单击击中断已发生\n");
```

```c
if (tap_stat & TAP_X_EN){
    iio_push_event(indio_dev,
    IIO_MOD_EVENT_CODE(IIO_ACCEL,
    0,
    IIO_MOD_X,
    IIO_EV_TYPE_THRESH,
    0),
    data->timestamp);
}
```

```c
if (tap_stat & TAP_Y_EN) {
    iio_push_event(indio_dev,
    IIO_MOD_EVENT_CODE(IIO_ACCEL,
    0,
    IIO_MOD_Y,
    IIO_EV_TYPE_THRESH,
    0),
    data->timestamp);
}
```
