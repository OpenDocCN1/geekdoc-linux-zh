
`#define ADXL_TAP_X_EN (1 << 2)`

```c
#define ADXL_TAP_Y_EN (1 << 1)

#define ADXL_TAP_Z_EN (1 << 0)

u8 tap_axis_control;

u8 data_rate;

#define ADXL_FULL_RES (1 << 3)

#define ADXL_RANGE_PM_2g 0

#define ADXL_RANGE_PM_4g 1

#define ADXL_RANGE_PM_8g 2

#define ADXL_RANGE_PM_16g 3

u8 data_range;

u32 ev_code_tap[3];

u8 fifo_mode;

u8 watermark;
};
```

```c
/* 设置初始 adxl345 寄存器值 */
static const struct adxl345_platform_data adxl345_default_init = {
.tap_threshold = 50,
.tap_duration = 3,
.tap_axis_control = ADXL_TAP_Z_EN,
.data_rate = 8,
.data_range = ADXL_FULL_RES,
.fifo_mode = FIFO_BYPASS,
.watermark = 0,
};
```

```c
/* 定义一个私有结构体 */
struct adxl345 {
struct gpio_desc *gpio;
struct device *dev;
struct input_dev *input;
struct adxl1345_platform_data pdata;
struct axis_triple saved;
u8 phys[32];
int irq;
u32 model;
u32 int_mask;
const struct adxl345_bus_ops *bops;
};
```

6. 使用执行总线操作的函数初始化 `adxl345_bus_ops` 结构体，并将其作为参数传递给 `adxl345_probe()` 函数：
```c
static const struct adxl1345_bus_ops adxl345_spi_bops = {
.bustype = BUS_SPI,
.write = adxl1345_spi_write,
.read = adxl1345_spi_read,
.read_block = adxl1345_spi_read_block,
};

static int adxl1345_spi_probe(struct spi_device *spi)
{
    /* 创建私有结构体 */
    struct adxl1345 *ac;
    /* 初始化驱动并返回初始化的私有结构体 */
    ac = adxl1345_probe(&spi->dev, &adxl1345_bops);
    /* 将 SPI 设备附加到私有结构体上 */
    spi_set_drvdata(spi, ac);
    return 0;
}
```

下方是带有主要代码行注释的 `adxl1345_probe()` 例程：
```c
struct adxl1345 *adxl1345_probe(struct device *dev,
                               const struct adxl1345_bus_ops *bops)
{
    /* 声明你的私有结构体 */
    struct adxl1345 *ac;
    /* 创建输入设备 */
    struct input_dev *input_dev;
    /* 创建指向常量平台数据的指针 */
    const struct adxl1345_platform_data *pdata;
    /* 分配私有结构体 */
    ac = devm_kzalloc(dev, sizeof(*ac), GFP_KERNEL);
    /* 分配输入设备 */
    input_dev = devm_input_allocate_device(dev);
    /* 存储初始化的平台数据 */
    pdata = &adxl345_default_init;
    /* 将值存储到 ac 的 pdata 中 */
    ac->pdata = *pdata;
    /* 将输入设备存储到私有结构体 */
    ac->input = input_dev;
    ac->dev = spi->dev;
    /* 将 SPI 操作存储到私有结构体 */
    ac->bops = bops;
    /* 初始化输入设备 */
    input_dev->name = "ADXL345 accelerometer";
    input_dev->phys = ac->phys;
    input_dev->dev.parent = dev;
    input_dev->id.product = ac->model;
    input_dev->id.bustype = bops->bustype;
    /* 附加输入设备和私有结构体 */
    input_set_drvdata(input_dev, ac);
    /* 当单击中断触发时设置支持 3 个事件的 EV_KEY 类型 */
    set_bit(EV_KEY, input_dev->evbit);
    set_bit(pdata->ev_code_tap[ADXL_X_AXIS], input_dev->keybit);
    set_bit(pdata->ev_code_tap[ADXL_Y_AXIS], input_dev->keybit);
    set_bit(pdata->ev_code_tap[ADXL_Z_AXIS], input_dev->keybit);
    /* 检查是否启用了任何轴
    * 在此驱动中仅设置单击中断 */
    if (pdata->tap_axis_control & (TAP_X_EN | TAP_Y_EN | TAP_Z_EN))
        ac->int_mask = SINGLE_TAP;
    /* 获取 gpio 描述符，将方向设置为输入
    * 并存储在私有结构体中 */
    ac->gpio = devm_gpiod_get_index(dev, ADXL345_GPIO_NAME, 0, GPIOD_IN);
    /* 获取与此描述符关联的 Linux IRQ 号 */
    ac->irq = gpio_to_irq(ac->gpio);
    /* 请求线程中断 */
    devm_request_threaded_irq(input_dev->dev.parent,
        ac->irq, NULL,
        adxl345_irq,
        IRQ_TRIGGER_HIGH | IRQ_ONESHOT, dev,
        ac);
    /* 创建 sysfs 组 */
    sysfs_create_group(&dev->kobj, &adxl345_attr_group);
    /* 将输入设备注册到内核 */
    input_register_device(input_dev);
    /* 初始化 ADXL345 寄存器
    /* 设置单击阈值和时长 */
    AC_WRITE(ac, THRESH_TAP, pdata->tap_threshold);
    AC_WRITE(ac, DUR, pdata->tap_duration);
    /* 设置检测单击的轴（Z轴） */
    AC_WRITE(ac, TAP_AXES, pdata->tap_axis_control);
    /* 设置数据率和轴读取功率模式，降低噪声 */
    AC_WRITE(ac, BW_RATE, RATE(ac->pdata.data_rate) |
        (ac->pdata.low_power_mode ? LOW_POWER : 0));
    /* 设置 FIFO 模式，默认不使用 FIFO */
    AC_WRITE(ac, FIFO_CTL, FIFO_MODE(pdata->fifo_mode) |
    SAMPLES(pdata->watermark));
    /* 将所有中断映射到 INT1 引脚 */
    AC_WRITE(ac, INT_MAP, 0);
    /* 启用中断 */
    AC_WRITE(ac, INT_ENABLE, ac->int_mask);
```
