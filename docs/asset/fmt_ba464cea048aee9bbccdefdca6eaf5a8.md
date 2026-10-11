
```c
if (gpiod_line_request_output(output_line, "Port19,GPO",
    GPIO_LINE_ACTIVE_STATE_HIGH) == -1) {
    gpiod_line_release(output_line);
    gpiod_chip_close(output_chip);
    return -1;
}
```

```c
/* 对 max11300 设备的 port19 (GPO) 闪烁 10 次 */
for (int i=0; i < flash; i++) {
    line_value = !line_value;
    ret = gpiod_line_set_value(output_line, line_value);
    if (ret != 0) {
        ret = errno;
        gpiod_line_release(output_line);
    }
}
```

# 实验 11.2：“Nunchuk 生产者与消费者”模块

```c
gpiod_chip_close(output_chip);
return ret;
}
sleep(1);
}
gpiod_line_release(output_line);
gpiod_chip_close(output_chip);
```

IIO 驱动程序可以将它们的通道导出给其他可以使用它们的消费者驱动程序。这些驱动程序通常是 ADC，在内核中会有其他消费者；例如，电池充电器、燃油计和热传感器都会使用 IIO ADC 驱动程序的通道。在本实验中，你将开发两个驱动程序：第一个是 IIO 生产者驱动程序，它将读取来自 Nunchuk 加速度计传感器的三轴数据；第二个是 Input 消费者驱动程序，它将从 IIO 生产者驱动程序读取 IIO 通道值并将其报告给 Input 子系统。

加速度计通常用于消费级设备，且其可用性有限。使用这种生产者-消费者方法，可以轻松地将 Nunchuk 控制器的加速度计替换为在内核主线中有可用 IIO 驱动的新加速度计（或者你可以开发自己的），并且在不进行任何修改的情况下复用消费者驱动程序。

你将使用上一个 IAB 10.2 的硬件设置。

## Nunchuk 生产者模块

让我们从开发 Nunchuk 生产者驱动程序开始。该程序的操作将非常简单。你将使用 IIO 子系统开发一个读取 Nunchuk 加速度计轴加速度的驱动程序。

现在描述程序的主要部分：

### 1. 包含函数头文件：
```c
#include <linux/module.h>
#include <linux/i2c.h>
#include <linux/delay.h>
#include <linux/io/iio.h>
```

### 2. 创建一个私有的 `nunchuk_accel` 结构体：
```c
struct nunchuk_accel {
    struct i2c_client *client;
```

### 3. 在 `nunchuk_accel_probe()` 函数中，声明私有结构的实例并分配 `iio_dev` 结构：

```c
struct iio_dev *iio_dev;
struct nunchuk_accel *nunchuk_device_alloc(client->dev);
iio_dev = devm_io_alloc(&client->dev, sizeof(*nunchuk_accel));
```

### 4. 在 `nunchuk_accel_probe(function)` 中初始化 `iio_device` 和 `nunchuk_accel` 私有结构。`nunchuk_accel` 私有结构将之前通过使用 `devm_priv()` 函数分配。保持物理设备（由物理总线处理的设备，在此处为 I2C）与逻辑设备之间的指针：
```c
nunchuk_accel = devm_priv(iio_dev); /* 为了能够在程序的其他函数中访问私有结构，需要使用 devm_priv() 函数将 nunchuk_accel 指针挂载到 iio_dev 结构上 */
nunchuk_accel = client; /* 用于与 Nunchuk 设备交换数据的 I2C 设备指针 */
```
```c
iio_dev->name = "Nunchuk Accel"; /* 存储 iio_dev 名称 */
iio_dev->dev = &client->dev; /* 物理设备（由物理总线处理，此处为 I2C）与逻辑设备之间的指针 */
iio_dev->info = &iio_info; /* 存储 iio_info 结构，它包含 IIO 读取回调 */
```
```c
iio_dev->channels = 3; /* 设置设备的通道数 */
iio_dev->modes = IIO_DIRECT_MODE; /* 设备模式。DIRECT_MODE 表示采集的数据不缓存，可以直接在 sysfs 下读取 */
```

### 5. 在调用之前，设备准备好接受应用程序的请求：
```c
devm_iio_register(client->dev, iio_dev);
```

### 6. 创建 `iio_chan_spec` 结构以向用户空间暴露程序中每个通道的 sysfs 属性。`iio_chan_spec` 的 `modified` 字段设置为 1。修饰符通过使用 `struct iio_chan_spec` 的 `channel2` 字段指定用于识别程序中的轴。`info_mask` 变量指示类型：
```c
#define NUNCHUK_IO_CHAN(axis) {
  .type = IIO_ACCEL,
  .modified = 1,
  .channel2 = IIO_MOD_##axis,
  .info_mask = BIT(IIO_CHAN_RAW),
}
```
```c
static const struct iio_chan_spec nunchuk_channels[] = {
  NUNCHUK_IO_CHAN(X),
  NUNCHUK_IO_CHAN(Y),
  NUNCHUK_IO_CHAN(Z),
};
```

上述 IIO 通道定义将生成以下数据访问：
```
/sys/bus/io/devices/io:deviceX/in_acc_raw
/sys/bus/io/devices/io:deviceX/in_acc_raw
/sys/bus/io/devices/io:deviceX/in_acc_raw
```

### 7. 创建 `iio_info` 结构来描述 IO 内核为此设备使用的钩子。用于用户空间与每个通道的 sysfs 属性交互的内核钩子。
```c
static const struct iio_info nunchuk_info = {
  .read_raw = nunchuk_accel_read_raw,
};
```

`nunchuk_accel_read_raw()` 函数从用户空间读取任何 `in_acc_raw` 条目时返回每个轴的值。加速度计的轴将使用 `channel2` 修饰符进行过滤。
```c
static int nunchuk_accel_read_raw(struct iio_dev *iio_dev,
  struct iio_chan_spec const *chan,
  int *val, int *val2, long long mask) {
  char *buf;
  struct nunchuk_accel *nunchuk_accel = devm_priv(iio_dev);
  struct i2c_client *client = nunchuk_accel->client;
  /* 从 nunchuk_registers 读取数据 */
  nunchuk_registers(client, buf, ARRAY_SIZE(buf));
  /* 数据需要写入 'val'，且 'val2' 被忽略 */
  switch (chan->channel2) {
  case IIO_MOD_X:
      *val = (buf[2] << 2) | ((buf[5] >> 2) & 0x03);
      break;
    case IIO_MOD_Y:
      *val = (buf[3] << 2) | ((buf[5] >> 4) & 0x03);
      break;
    case IIO_MOD_Z:
      *val = (buf[4] << 2) | ((buf[5] >> 6) & 0x03);
      break;
  }
}
```
```c
break;
default:
  return -EINVAL;
}
  return IIO_VAL_INT;
```

声明程序支持的设备列表：
