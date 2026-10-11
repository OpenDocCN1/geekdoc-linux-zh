
```c
/* 要通过 SPI 接收命令字节的 LSB 位，必须为 1 */
st->tx_cmd = ((reg << 1) | 1);

ret = spi_sync_transfer(spi, t, ARRAY_SIZE(t));
if (ret < 0)
    return ret;

/*
 * 在小端 CPU 中，通过 SPI 接收的（BE 格式）第一个字节
 * （ADC 的 MSB）将存储在 "st->rx_msg" 的低地址
 * 使用 cpu16_to_cpu() 拷贝到 "value" 的高地址
 */
*value = cpu16_to_cpu(st->rx_msg);

return 0;

/* 在差分模式（补码）下读 MAX11300 寄存器的函数 */
static int max11300_reg_read_differential(struct max11300_state *st, u8 reg, int *value)
{
    struct spi_device *spi = container_of(st->dev, struct spi_device, dev);
    int ret;

    struct spi_transfer t[] = {
        .tx_buf = &st->tx_cmd,
        .len = 1,

        {
            .rx_buf = &st->rx_msg,
            .len = 2,
        },
    };

    dev_info(st->dev, "read differential channel\n");
    /* 命令字节的 LSB 必须为 1 */
    st->tx_cmd = ((reg << 1) | 1);

    ret = spi_sync_transfer(spi, t, ARRAY_SIZE(t));
    if (ret < 0)
        return ret;

    /*
     * 将存储在 "st->rx_msg" 中的接收到的 SPI 
     * 扩展为 int 补码
     */
    *value = sign_extend32(cpu16_to_cpu(st->rx_msg), 16);

    return 0;
}
```

# 作为 IIO 设备的工业框架

这些是主要代码部分：

## 1. 包含所需的头文件

```c
#include <linux/iio.h> /* devm_iio_alloc(), iio_priv() */
```

## 2. 创建管理设备的全局数据结构

```c
struct max11300_state {
    struct device *dev; // SPI 设备指针
    const struct max11300_rw_ops *ops; // spi 回调函数指针
    struct gpio_chip *gpio; // gpio 控制器
    mutex gpio_lock;
    u8 num_ports; // MAX11300 设备的端口数
    u8 gpios[]; // DT 中声明为 GPIO 的端口数（0 到 9）
    u8 offset_mode[20]; // 0..1 范围内 "offset" 的 gpio 端口模式（1 和 3）
    u8 modes[20]; // MAX11300 的 gpio 端口模式
    u8 adc_range[20]; // ADC 相关模块的电压范围
    u8 dac_range[20]; // DAC 相关模块的电压范围
    u8 dac_reference[20]; // ADC 电压参考：0: 内部，1: 外部
    u8 adc_samples[20]; // ADC 相关模块的采样数
    u8 negative_port; 
    u8 tx_cmd; // SPI 传输的命令字节
    be16 tx_msg; // BE 格式的 SPI 传输值
    be16 rx_msg; // BE 格式的 SPI 接收值
};
```

## 3. 在 `max11300_probe()` 函数中，声明私有结构实例并分配 `iio_dev` 结构体

```c
struct iio_dev *indio;
struct max11300_state *state;
indio = devm_iio_alloc(dev, sizeof(*state));
```

## 4. 在 `max11300_probe()` 函数中初始化 `iio_dev` 和数据私有结构

数据私有结构之前已使用 `iio_priv()` 函数分配。保留物理设备与逻辑设备之间的指针：

```c
st = iio_priv(indio); /* 为了在驱动的其他部分访问私有数据结构，
需要使用 iio_priv() 函数将其附加到 iio_dev 结构上。你将使用相同的函数 iio_priv() 获取私有结构的指针 */
st->dev = dev; /* 存储 SPI 设备指针，用于与 MAX11300 设备交换数据 */

dev_set_drvdata(dev, indio); /* 将 SPI 设备与 iio_dev 关联 */
indio->name = name; /* 存储 iio_dev 名称。在 probe() 函数中执行此操作之前，
你将使用 spi_get_device_id() 获取触发匹配的 spi_device_id */
indio->parent = dev; /* 保留物理设备（在此处为物理总线处理的设备）与本地设备之间的指针 */
indio->info = &max11300_info; /* 存储 iio_info 结构的地址，
包含指向读/写回调的指针 */
max11300_alloc_ports(st); /* 配置设备的 IIO 通道以生成
sys 条目。该将在下一点中详细描述 */
```

## 5. `max11300_alloc_ports(st)` 函数

`max11300_alloc_ports(st)` 函数使用 `fnode_property_u32()` 函数从 `max1300` 节点的通道子节点返回 DT 属性，并将这些属性的值存储在全局结构的变量中。`max11300_set_port_modes()` 使用这些变量配置 `max11300` 的端口。`max11300_alloc_ports(st)` 函数通过 `max11300_setup_port(*st)` 函数生成不同的 IIO sysfs 条目：

* 该函数将分配并配置 `iio` 设备的 `iio` 通道。
* 它还将读取每个端口（通道）的 DT 属性并将其存储在全局结构中

```c
static int max11300_alloc_ports(struct max11300_state *st)
{
    unsigned int curr_port = 0, num_ports = st->num_ports, port_mode_count = 0,
    st->num_pios = 0;
    /* 从全局结构恢复 iio dev */
    iio_dev *iio_dev = iio_priv_to_dev(st);
    /* 所有 iio 通道规范的存储指针 */
    iio_chan_spec *ports;
    /* 允许设备描述 fnode_handle 指针 */
    fnode_handle *child;
    u32 reg, tmp;
    int ret;
    /* 遍历 DT 中的每个 MAX11300 子节点；
     * 如果节点中发现错误，则遍历下一个
     * （继续）
     */
    device_for_each_child_node(st->dev, child) {
        ret = fnode_property_read_u32(child, "reg", &reg);
        if (ret || reg >= ARRAY_SIZE(st->port_modes))
```

# 第 11 章

## 工业 I/O 子系统

```c
/*
* 将 DT "port,mode" 属性的值存储
* 在全局结构体中，以便了解每个端口的模式
* 程序的其他函数
*/
ret = fwnode_property_read_u32(child, "port-mode", &tmp);
if (!ret)
    st->port_modes[reg] = tmp;
```

```c
/* 所有 DT 节点应包含 port-mode 属性 */
else
    dev_info(st->dev, "port-mode is not found\n");
continue;
```
