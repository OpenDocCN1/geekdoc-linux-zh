
```c
chan->output = output;

chan->channel = id;

chan->info_mask = BIT(IIO_CHAN_INFO_RAW);

chan->scan_type.sign = 'u';

chan->scan_type.realbits = 12;

chan->scan_type.storagesbits = 16;

chan->scan_type.endianness = IIO_BE;

chan->extend_name = "mode_5_DAC";
}
```

```c
/* 具有正电压范围的 DAC */

static void max11300_setup_port_6_mode(struct iio_dev *io_dev,
struct iio_dev_chan *chan, bool output,
unsigned int id, unsigned long port_mode)
{
    chan->type = IIO_VOLTAGE;
    chan->indexed = 1;
    chan->address = port_mode;
    chan->output = output;
    chan->channel = id;
    chan->info_mask = BIT(IIO_CHAN_INFO_RAW);
    chan->scan_type.sign = 'u';
    chan->scan_type.realbits = 12;
    chan->scan_type.storagesbits = 16;
    chan->scan_type.endianness = IIO_BE;
    chan->extend_name = "mode_6_DAC_ADC";
}
```

```c
/* 单极端模式下具有正电压范围和直二进制格式的 ADC */

static void max11300_setup_port_7_mode(struct iio_dev *io_dev,
unsigned int id, unsigned long port_mode)
{
    chan->type = IIO_VOLTAGE;
    chan->indexed = 1;
    chan->address = port_mode;
    chan->output = output;
    chan->channel = id;
    chan->info_mask = BIT(IIO_CHAN_INFO_RAW);
    chan->scan_type.sign = 'u';
    chan->scan_type.realbits = 12;
    chan->scan_type.storagesbits = 16;
    chan->scan_type.endianness = IIO_BE;
    chan->extend_name = "mode_7_ADC";
}
```

/* 具有补码值的差分模式 ADC */
```c
static void max11300_setup_port_8_mode(struct iio_dev *iio_dev, struct iio_chan_spec *chan, bool output, unsigned id, unsigned id2, unsigned int port_mode)
{
    chan->type = IIO_VOLTAGE;
    chan->differential = 1;
    chan->address = port_mode;
    chan->indexed = 1;
    chan->output = output;
    chan->channel = id;
    chan->channel12 = id2;
    chan->info_mask_separate = BIT(IIO_CHAN_INFO_RAW);
    chan->scan_type.sign = 's';
    chan->scan_type.realbits = 12;
    chan->scan_type.endianness = IIO_BE;
    chan->extend_name = "mode_8_ADC";
}
```

- 此函数将分配并配置 `iio` 设备的 `iio` 通道。
- 它还会读取每个端口（通道）的 DT 属性，并将它们存储
- 在设备全局结构中

```c
static int max11300_alloc_ports(struct max11300_state *st)
{
    unsigned int i = 1, curr_port = 0, num_ports = st->num_ports, port_mode_6_count = 0, offset = 0;
    st->num_gpios = 0;
    /* 从全局结构中恢复 iio 设备 */
    struct iio_dev *iio_dev = iio_priv_to_dev(st);
    /* 存储所有 iio 通道规范的指针 */
    struct iio_chan_spec *ports;
    /* 指向允许设备描述对象的 device_node_handle 指针 */
    struct device_node_handle *child;
    u32 reg, temp;
    int ret;
    - 遍历 DT 中的每个 MAX11300 子节点。如果出错，则
    - 遍历到下一个节点（继续）
```
