
```c
#define ADXL345_GPIO_NAME   "int"

/* DEVIDS */
#define ID_ADXL345          0xE5

/* INT_ENABLE/INT_MAP/INT_SOURCE 位掩 */
#define SINGLE_TAP          (1 << 6)
#define WATERMARK           (1 << 1)

/* TAP_AXES 位掩 */
#define TAP_X_EN            (1 << 2)
#define TAP_Y_EN            (1 << 1)
#define TAP_Z_EN            (1 << 0)

/* BW_RATE 位掩 */
#define LOW_POWER           (1 << 4)
#define RATE(x)             ((x) & 0xF)

/* POWER_CTL 位掩 */
#define PCTL_MEASURE        (1 << 3)
#define PCTL_STANDBY        0x00

/* DATA_FORMAT 位掩 */
#define ADXL_FULL_RES       (1 << 3)

/* FIFO_CTL 位掩 */
#define FIFO_MODE(x)        ((x) & 0x33) << 6
#define FIFO_BYPASS         0
#define FIFO_FIFO           1
#define FIFO_STREAM         2
#define SAMPLES(x)          ((x) & 0x1F)

/* FIFO_STATUS 位掩 */
#define ADXL_X_AXIS        0
#define ADXL_Y_AXIS        1
#define ADXL_Z_AXIS        2

/* 中断轴已启用 */
```

# 第 12 章

## 在设备驱动程序中使用 Regmap API

```c
#define ADXL_TAP_X_EN (1 << 2)
#define ADXL_TAP_Y_EN (1 << 1)
#define ADXL_TAP_Z_EN (1 << 0)
```

### 4. 创建一个私有的 `adxl1345_data` 结构体：

```c
struct adxl1345_data {
    struct gpio_desc *gpio;
    struct regmap *regmap;
    struct iio_trigger *trig;
    struct device *dev;
    struct axis_triple saved;
    u8 data_range;
    u8 tap_threshold;
    u8 tap_duration;
    u8 tap_axis_control;
    u8 data_rate;
    u8 fifo_mark;
    u8 watermark;
    u8 low_power_mode;
    int irq;
    int ev_enable;
    u32 int_mask;
    s64 timestamp;
};
```

### 5. 创建 `iio_chan_spec` 和 `iio_event_spec` 结构体以暴露用户空间的通道和事件 sysfs 属性。`scan_index` 变量定义了启用通道的放置顺序，较低的 `scan_index` 将放置在较高索引通道之前。每个通道都需要一个唯一的 `scan_index`。

```
/* 每个轴将有两个事件 sysfs 属性
* 你将通过向带有位掩码 IIO_EV_INFO_VALUE 的 sysfs 属性写入
* 设置与特定轴相关的 THRESH_TAP 寄存器值
* 你将通过带有位掩码 IIO_EV_INFO_PERIOD 的 sysfs 属性写入
* 修改与特定轴相关的 DUR 寄存器
* THRESH_TAP 和 DUR 寄存器已为所有轴注册，因此
* 使用 mask_shared_by 代替 mask_separate 可能更有意义*/
```

```c
static const struct iio_adxl1345_event = {
    .type = IIO_EV_TYPE_THRESH,
    .dir = IIO_EV_DIR_EITHER,
    .mask_separate = BIT(IIO_EV_INFO_VALUE) |
    BIT(IIO_EV_INFO_PERIOD)
}
```

```
/* 每个轴将有自己的通道 sysfs 属性，并且有两个用于
* IIO_ACCEL 类型的共享 sysfs 属性
* 你将通过读取每个通道 sysfs 属性来获取每个轴的值
```

## 在设备驱动程序中使用 Regmap API

- 位掩码 `IIO_CHAN_RAW`
- 有一个共享属性通过位掩码
- `IIO_CHAN_INFO_SCALE` 来读取缩放值
- 有一个共享属性通过位掩码
- `IIO_CHAN_INFO_SCALE` 来写入加速度采样率

```c
#define ADXL345_CHANNEL(reg, axis, idx) { \
    .type = IIO_ACCEL, \
    .modified = 1, \
    .channel = IIO##axis, \
    .address = reg, \
    .info_mask_separate = BIT(IIO_CHAN_INFO_RAW), \
    .info_mask_shared_type = BIT(IIO_CHAN_INFO_SCALE) | \
    BIT(IIO_CHAN_INFO_SAMP_FREQ), \
    .scan_index = idx, \
    .scan_type = { \
        .bits = 13, \
        .storage_bits = 16, \
        .endianness = IIO_LE, \
    }, \
    .event_spec = &adxl345_event, \
    .num_event_specs = 1 }
```

```c
static const struct iio_chan_spec adxl345_channels[] = {
    ADXL345_CHANNEL(DATAX0, X, 0),
    ADXL345_CHANNEL(DATAY0, Y, 1),
    ADXL345_CHANNEL(DATAZ0, Z, 2),
    IIO_CHAN_SOFT_TIMESTAMP(3),
```

### 6. 创建 `iio_info` 结构体以声明 IIO 内核如何使用该设备。有四个对应于用户空间通道和事件的钩子。

```c
static const struct iio_info adxl345_info = {
    .driver_module = THIS_MODULE,
    .read_raw = adxl345_read_raw,
    .write_raw = adxl345_write_raw,
    .read_event = adxl345_read_event,
    .write_event = adxl345_write_event,
};
```

每个回调函数的简要描述：

- `adxl345_read_raw`: 当用户空间读取带有位掩码 `IIO_CHAN_INFO_RAW` 的通道 sysfs 属性时，该函数返回轴值。当用户空间读取带有位掩码 `IIO_CHAN_INFO_SCALE` 的共享 sysfs 属性时，它返回加速度缩放值。你可以在下面的 `regmap_bulk_read()` 函数中看到，它通过 SPI 访问每个轴的寄存器。
