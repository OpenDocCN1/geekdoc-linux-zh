
```c
#define ADXL345_CHANNEL(reg, axis, idx) {
    .type = IIO_ACCEL,
    .modified = 1,
    .channel2 = IIO_MOD##axis,
    .address = reg,
    .info_mask_separate = BIT(IIO_CHAN_INFO_RAW),
    .info_mask_shared_by_type = BIT(IIO_CHAN_INFO_SCALE) |
    BIT(IIO_CHAN_INFO_SAMP_FREQ),
    .scan_index = idx,
    .scan_type = {
        .sign = 's',
        .realbits = 13,
        .storage_bits = 16,
        .endianness = IIO_LE,
    },
    .event_spec = &adxl345_event,
    .num_event_specs = 1
}
```

# 工业 I/O 子系统

# 第 11 章

你将创建用于用户态与事件 sysfs 属性交互的内核钩子：

```c
static const struct iio_info adx1345_info = {
    .driver_module        = THIS_MODULE,
    .read_raw             = adx1345_read_raw,
    .write_raw            = adx1345_write_raw,
    .read_event_value     = adx1345_read_event,
    .write_event_value    = adx1345_write_event,
};
```

- `read_event_value`: 读取与事件相关的配置值。
- `write_event_value`: 为事件写入配置值。

可以通过写入 `/sys/bus/iio/devices/devicex/events/` 目录下的 sysfs 属性来启用事件通知。

## 将 IIO 事件传递到用户态

`iio_push_event()` 函数尝试将事件添加到列表中供用户态读取。它通常在线程化中断（threaded IRQ）中调用。

```c
int iio_push_event(struct iio_dev *dev, u64 ev_code, s64 timestamp);
```

- `iio_dev`: 指向 IIO 设备结构的指针。
- `ev_code`: 包含通道类型、修饰符和事件类型；有一些宏用于打包/解包事件代码：`IIO MOD EVENT CODE` 和 `IIO EVENT CODE EXTRACT`。
- `timestamp`: 事件发生的时间。

在下面的代码段中，你将看到如何将 IIO 事件传递到用户态。你将在下一章节开发的 ADXL345 IIO 驱动的中断处理程序内部发送这些事件。

```c
/* 中断服务程序 */
static irreturn_t adx1345_event_handler(int irq, void *handle)
{
    u32 tap_stat, int_stat, ret;
    struct iio_dev *indio_dev = handle;
    struct adx1345_data *data = iio_priv(indio_dev);
    data->timestamp = iio_get_time_ns(indio_dev);
/*
 * 在清除中断之前应该读取 ACT_TAP_STATUS
 * 避免读取 ACT_TAP_STATUS 以防敲击检测被禁用
 * 如果任何一个轴已启用，则读取 ACT_TAP_STATUS
 */
if (data->axis_control & (TAP_X_EN | TAP_Y_EN | TAP_Z_EN)) {
    ret = regmap_read(data->regmap, ACT_TAP_STATUS, &tap_stat);
    if (ret) {
        dev_error(data->dev, "error reading ACT_TAP_STATUS\n");
        return ret;
    }
} else {
    tap_stat = 0;
}/*
 * 读取 INT_SOURCE (0x30) 寄存器。
 * 清除中断 */
ret = regmap_read(data->regmap, INT_SOURCE, &int_stat);
if (ret) {
    dev_err(data->dev, "error reading INT_SOURCE\n");
}
/*
 * 如果发生了 SINGLE_TAP 事件，则调用 adxl345_do_tap 函数
 * 并传递 ACT_TAP_STATUS 参数
 */
if (int_stat & (SINGLE_TAP)) {
    dev_info(data->dev, "single tap has occurred\n");

    if (tap_stat & TAP_X) {
        iio_push_event(indio_dev,
            iio_MOD_EVENT_CODE(IIO_ACCEL,
                IIO_MOD_X,
                IIO_EV_TYPE_THRESH,
                0),
            data->timestamp);
    }
    if (tap_stat & TAP_Y) {
        iio_push_event(indio_dev,
            iio_MOD_EVENT_CODE(IIO_ACCEL,
                IIO_MOD_Y,
                IIO_EV_TYPE_THRESH,
                0),
            data->timestamp);
    }
    if (tap_stat & TAP_Z) {
        iio_push_event(indio_dev,
            iio_MOD_EVENT_CODE(IIO_ACCEL,
                IIO_MOD_Z,
                IIO_EV_TYPE_THRESH,
                0),
            data->timestamp);
    }
}
return IRQ_HANDLED;
}
```

# 工业 I/O 子系统

## IIO 工具

在开发 IIO 驱动期间，可以使用一些实用工具。它们位于内核树的 `/tools/iio/`：

- `iio`: 列举 IIO 触发器、设备和通道。
- `iio_event`: 监控 IIO 设备 ioctl 接口的事件。
- `iio_generic_buffer`: 监控来自 IIO 设备缓冲区。
- `libio`: Analog Devices 开发的用于 IIO 设备的库。地址为 https://github.com/analogdevicesinc/libiio。

## 实验 11.1: "IIO 混合信号设备"

在本实验中，你将创建一个控制 Maxim MAX1130 设备的 IIO 驱动。还将编写几个从用户态控制 GPIO 的应用程序。

MAX1130 在单个集成电路 (IC) 中集成了 IIXI™ 多通道模拟数字转换器 (ADC) 和 12 位多通道数字模拟转换器 (DAC)。该设备提供两个混合信号高电压端口，可以配置为 ADC 输入、DAC 输出、通用输入端口 (GPI)、通用输出端口 (GPO) 或模拟终端。你可以在此处查看与设备设备的所有信息：https://www.maximintegrated.com/en/products/analog/data-converters/analog-to-digital-converters/MAX1130.html。

在本实验中，你将使用来自 MIKROE 的 IIXI™ CLICK 板。该板的文档位于：https://www.mikroe.com/pixi-click。

在开发驱动之前，你可以使用 GUI 软件创建一个自定义设计。该工具可以在 Maxim 网站下载。实验文件夹中包含了 `MAX1130ConfigurationSetupV1.4.zip` 工具以及作为驱动开发起点的自定义设计。

在工具的下一张截图中，你可以看到用于驱动开发的配置：

![](img/eebd1edc8b2bd72a2e214ef70e7c33_460_0.png)

这些是在配置 IIXI 端口时使用的参数：

- 端口 0 (`P0`) -> 单端 ADC，采样平均值 = 1，内部参考电压，电压范围 0V 到 10V
