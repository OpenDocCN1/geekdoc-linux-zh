
```c
/* 初始化 polled input */
ioacceler->i2c_client = client;
ioacceler->polled_input->private = ioacel;
ioacceler->polled_input->interval = 50;
ioacceler->polled_input->poll = ioacel;
ioacceler->polled_input->input->dev = &client->dev;
ioacceler->polled_input->input->name = "IOACCEL keyboard";
ioacceler->polled_input->input->id.bustype = BUS_I2C;
```

```c
/* 设置事件类型 */
set_bit(EV_KEY, ioacceler->polled_input->input->evbit);
set_bit(KEY_1, ioacceler->polled_input->input->keybit);
```

```c
/* 注册设备，现在在取消注销前它是全局的 */
input_register_polled_device(ioacceler->polled_input);
return 0;
}
```

```c
static int io2c_remove(struct i2c_client *client) {
    struct ioacel_dev *ioacceler;
    ioacceler = i2c_get_client_data(client);
    input_unregister_polled_device(ioacceler->polled_input);
    dev_info(&client->dev, "io2c_remove()");
    return 0;
}
```

```c
/* 将项添加到设备树 */
static const struct of_device_id ioacceler_dt_ids[] = {
    {.compatible = "arrow,adxl345"},
};
```

```c
MODULE_DEVICE_TABLE(of, ioacceler_dt_ids);
static const struct i2c_device_id i2c_ids[] = {
    {"adxl345", 0}
};
MODULE_DEVICE_TABLE(i2c, i2c_ids);
```

```c
/* 创建 i2c 驱动 */
static struct i2c_driver ioacceler_driver = {
    .driver = {
        name = "adxl345",
        owner = THIS_MODULE,
        .match_table = ioacceler_dt_ids,
    },
    .probe = ioacel_probe,
    .remove = io2c_remove,
    .id_table = i2c_ids,
};
```

```c
/* 注册到 i2c 总线 */
module_i2c_driver(ioacceler_driver);
```

# 第10章

## 输入子系统

`MODULE_LICENSE("GPL");`

`MODULE_AUTHOR("Alberto@arroweurope.com");`

`MODULE_DESCRIPTION("这是一个加速度计平台驱动");`

# i2c_rpi3_accel.c

使用 `i2c-tools` 扫描 `i2c` 总线。列出可用的 I2C 总线和连接到 `i2c` 总线的设备：

```bash
root@raspberry:home/pi# i2c-detect -1
i2c-1 bcm2835 (i2c@7e0400) I2C adapter
root@raspberry:home/pi# i2c-detect -y 1
00: 0 1 2 3 4 5 6 7 8 9 a b c d e
10:                             1d
20:
30:
40:
50:
60:
70:
```

为 `ADXL345` 设备设置测量模式：

```bash
root@raspberry:home/pi# i2c-set -y 1 0x33 0x08
```

`0x33` 值对应于 `OUT_X_MSB` 寄存器地址。移动树莓派板，观察 `OUT_X_MSB` 寄存器值的变化。设置一个值范围来生成事件。值的范围将位于 `ioacel_poll(1)` 函数内部：

```bash
root@raspberry:home/pi# insmod i2c_rpi3_accel.co
adxl345 1-01d: my_probe() function is called.
input: IOACCEL keyboard as /devices/platform/3f804000.i2c/i2c-1/1-01d/input0
```

执行事件应用程序查看输入设备。选择 0。移动树莓派板，直到生成 `EV_KEY` 事件：

```bash
root@raspberry:home/pi# evtest
No device specified, typing to scan all of /dev/input*
Available devices:
/dev/input0: IOACCEL keyboard
Select device number [-]: 0
Input driver version is 1.0
Input device ID: bus 0x18 vendor 0x0 product 0x0
Input device name: "IOACCEL keyboard"
Supported events:
Event type 0 (EV_SYN)
Event type 1 (EV_KEY)
Event code 2 (KEY_1)
```

# 第 10 章

## 输入子系统

`Wii Nunchuk` 使用带有 6 引脚专用接口，暴露 `I2C` 信号、`+3V` 和 `GND`。`MOD-Wii-EXT-NUNCHUCK` 包含一个 `UEXT` 适配器，它提供了一种支持三种串口通信接口的通用接口：`I2C`、`SPI` 和 `RS232`。在 `MOD-Wii-EXT-NUNCHUCK` 中，只有 `I2C` 信号连接到 `Nunchuk` 设备。

本实验 10.2 的灵感来自 Bootlin 的嵌入式 Linux 内核与驱动训练材料，位于 https://bootlin.com/training/kernel/

## LAB 10.2 硬件描述

你将使用树莓派 40 脚 GPIO 头的 I2C 引脚连接到 Nunchuk 的 UEXT 接口，如下图所示：

| 引脚编号 | 信号名称 |
|---|---|
| 1 | 3.3V |
| 2 | GND |
| 3 | TXD |
| 4 | RXD |
| 5 | SCL |
| 6 | SDA |
| 7 | MISO |
| 8 | MOSI |
| 9 | SCK |
| 10 | SSEL |

![](img/eebd1e8dc8b2bd72a2e2142ef70e7c33_386_0.png)

将树莓派的 I2C 引脚连接到 Nunchuk 设备的 I2C 引脚：

- 将树莓派 `SCL` 连接到 `UEXT SCL`（引脚 5）。
- 将树莓派 `SDA` 连接到 `UEXT SDA`（引脚 6）。

在两个板卡之间连接相应的电源引脚：

- 将树莓派 `3.3V` 连接到 `UEXT 3.3V`（引脚 1）。
- 将树莓派 `GND` 连接到 `UEXT GND`（引脚 2）。

两个板卡之间的硬件设置已经完成！！

## LAB 10.2 设备树描述

打开 `bcm2710-ri-3-b.dts` DT 文件，并找到 `i2c1` 控制器主节点。在 `i2c1` 节点内部，你可以设置一个 `pinctrl-0` 属性，指向 `i2c1_pins` 引脚配置节点，该节点配置了 I2C 模式下的 `i2c1` 控制器引脚。`i2c1_pins` 引脚配置节点定义在 `bcm2710-ri-3-b.dts` 文件的 `gpio` 节点属性内部。

通过向 `status` 属性写入 "okay" 来启用 `i2c1` 控制器。你将将其设置为 `100Khz` 时钟频率属性。Nunchuk 设备通过最大频率为 100kHz 的 I2C 总线接口与树莓派进行通信。

你可以在下方看到用于我们 Nunchuk 设备的设备树配置：

```
&i2c1 {
pintrl-names = "default";
pintrl-0 = &i2c1_pins;
clock-frequency = <100000>;
status = "okay";

nunchuk: nunchuk@52 {
  compatible = "nunchuk";
  reg = <0x52>;
}
```
