
![](img/739a3b5967f8a55eff80a587614f_413_0)

这一次主要的代码段将不再详细描述。驱动的大部分将重用，因此仅突出显示新部分。

## 设备树

1. 打开设备树源文件`imx6qdl-sabresd.dtsi`（位于`Linux/arch/arm/boot/dts`）。在实验9.4中创建的`Itc24`设备节点中添加下方加粗行（中断属性）。注释掉`spidev`节点。在`ADC`节点内部创建`pinctrl00`属性，指向`pinctrl_key`引脚函数，该节点将通过“`MX6QDL_PAD_GPIO_5_GPIO1_IO05`”`PIN_FUNCTION_ID`宏使`GPIO_5`作为`GPIO1_IO05`工作。

```
&ecspi {
fsl, spi-num-chipselects = <1>;
cs-pios = <&gpio4 9 0>;
pinctrl-names = "default";
pinctrl-0 = <&pinctrl_ecspi>;
status = "okay";
}
/*chip: spidev80 {
```

```c
compatible = "spidev";
sppi-max-frequency = <20000000>;
reg = <0>;
/*
```

```c
ADC ltc242280 {
#address-cells = <1>;
#size-cells = <1>;
compatible = "arrow,ltc2422";
sppi-max-frequency = <20000000>;
reg = <0>;
pintctrl-0 = <&pintctrl_key>;
gpios = <&gpio5 GPIO ACTIVE_LOW>;
interrupts = <5 0>; // gpio 编号和极性
interrupt-parent = <&gpio1>; // gpio 中控制器
};
```

```c
pintrl_key: key {
fsl,pins = <
MX6QDL_PAD_GPIO_5_I005 0x80000000>
};
```

注释 `gpio-keys` 节点内部的 `volume-down` 节点：

```c
gpio-keys {
compatible = "gpio-keys";
pintrl-names = "default";
pintrl-0 = <&pintrl_gpio_keys>;
```

```c
power {
label = "Power Button";
gpios = <&gpio3 29 1>;
gpio-key,wakeup:
linux, code = <KEY_POWER>
};
```

```c
volume-up {
label = "Volume Up";
gpios = <&gpio4 4 1>;
gpio-key,wakeup:
linux, code = <KEY_VOLUMEUP>
};
```

```c
/*volume-down {
label = "Volume Down";
gpios = <&gpio5 1>;
gpio-key,wakeup:
linux,code = <KEY_VOLUMEDOWN>
};*/
```

### 驱动程序中的睡眠与唤醒

1. 声明一个静态等待队列：

```c
static DECLARE_WAIT_QUEUE(hello_keys_wait);
```

2. 将用户进程置于睡眠状态。在 `ltc2422_read_raw()` 回调函数中添加以下代码：

```c
wait_event_interruptible(hello_keys_wait, done);
```

3. 在中断下半部处理程序中唤醒进程：

```c
wake_up(&hello_keys_wait);
```

### 工作队列 (Workqueue)

1. 在我们的私有数据结构中声明工作项和工作队列：

```c
#include <linux/workqueue.h>

struct ADC_data {
	struct workqueue_struct *ADC_wq;
	struct work_struct work;
	struct spi_device *spi;
	uint8_t buffer[4];
	char name[8];
};
```

2. 在 `probe()` 函数创建一个新的工作队列和关联的工作线程。传统的 Workqueue 接口已废弃，并被 CMWQ（并发管理工作队列）取代。CMWQ 与原始工作queue API 保持兼容，提供了更丰富、表达力强且性能更好的 API。使用 `alloc_workqueue` 函数代替废弃的 `create_workqueue`。有关 CMWQ 的更多信息，请参阅：

`Linux/Documentation/workqueue.txt`

你将使用 `INIT_WORK()` 在运行时创建一个工作，其中第二个参数是执行延迟任务的函数：

```c
st->ADC_wq = alloc_workqueue("ADC_wq", 0, 0);
INIT_WORK(&st->work, ADC_trigger_int);
```

### 中断管理

将中断处理程序的执行分为两个部分：上半部（Top half）和下半部（Bottom half）。

![](img/739a35b59067f8a55eff80a58765146f_416_0.png)

- 1. 处理程序（上半部）：

工作队列是延迟执行任务的通用机制。你通过 `queue_work()` 将任务推入工作队列。参见下面的处理程序代码：

```c
static irq_return_t hello_keys_isr(int irq, void *data)
{
    pr_info("interrupt received. key: %s\n", HELLO_KEYS_NAME);
    struct iio_dev *dev = data;
    /* 恢复 ADC 数据以将任务推入工作队列 */
    struct ADC_data *job = iio_priv(indio_dev);
    queue_work(job->ADC_wq, &job->work);
    return IRQ_HANDLED;
}
```

- 2. 下半部：

在下半部中你将唤醒用户进程：

```c
static void ADC_trigger_int(struct work_struct *work_s)
{
    pr_info("ISR bottom done");
    done = true;
    wake_up(&hello_keys_wait);
}
```

# 列表 9-6：LTC2422_dual_trigger_bottom.c
