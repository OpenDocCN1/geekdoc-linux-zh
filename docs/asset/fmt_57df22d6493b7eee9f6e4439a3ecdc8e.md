
查看 `IMX6DQ` 第 312 页并检查 `i2c3` 控制器的引脚分配。`i2c` 控制器的时钟和数据信号可以从下表所示：

## 设备驱动内核框架

| 信号 | 引脚 (模式) | 复用/输入选择寄存器 |
|---|---|---|
| `I2C3_SCL` | `EIM_D17 (ALT6)` | `IOMUXC_SW_MUX_CTL_PAD_EIM17`<br>`IOMUXC_I2C3_SCL_IN_SELECT` |
| | `GPIO_3 (ALT2)` | `IOMUXC_SW_MUX_CTL_PAD_GPIO03` |
| | | 表格续... |
| `I2C3_DA` | `GPIO_5 (ALT6)` | `IOMUXC_SW_MUX_CTL_PAD_GPIO05`<br>`IOMUXC_I2C3_SCL_IN_SELECT` |
| | `EIM_D18 (ALT6)` | `IOMUXC_SW_MUX_CTL_PAD_EIM18`<br>`IOMUXC_I2C3_SCL_IN_SELECT` |
| | `GPIO_6 (ALT2)` | `IOMUXC_I2C3_DA_IN_SELECT` |
| | `GPIO_16 (ALT6)` | `IOMUXC_SW_MUX_CTL_PAD_GPIO16`<br>`IOMUXC_I2C3_DA_IN_SELECT` |
| | | `IOMUXC_I2C3_DA_IN_SELECT` |

在 `SABRE` 原图中图中看到 `I2C3_SCL` 和 `I2C3_DA` 连接到 `GPIO_3` 和 `GPIO_6`。在 `imx6-sabresd.dtsi`（位于 `Linux/boot/ts`）中添加新节点：

1. 向 `i2c` 控制器节点添加 `LTC2607` 子节点。在 "`reg`" 属性写入 `LTC2607` `i2c` 地址。如果 `i2c` 控制器状态为禁用，请通过 `status = "okay"` 启用它。

```dtts
i2c3 {
    clock-frequency = <100000>
    pintrl-names = "default"
    pintrl-0 = <&pintrl_i23>;
    status = "okay";
    galax_ts {
        compatible = "galax_ts";
        reg = <0x04>;
        interrupt-parent = <&gpio6>;
        interrupts = <7 2>;
        wakeup-gpios = <&gpio6 7 0>;
    }
    mag3110e {
        compatible = "mag31100";
        reg = <0x0e>;
        position = <2>;
        vdd-supply = <&reg_sensor>;
    }
}
```

```dtts
vdd-supply = &reg_sensor;
interrupt-parent = <&gpio3>;
interrupts = <16>;
```

```dtts
is1290238 {
    compatible = "is129023";
    reg = <0x44>;
    position = <9>;
    vdd-supply = <&reg_sensor;
    interrupt-parent = <&gpio3;
    interrupts = <9 2>;
}
```

```dtts
ltc2607@72 {
    compatible = "arrow,ltc2607";
    reg = <0x72>;
}
```

```dtts
ltc2607@73 {
    compatible = "arrow,ltc2607";
    reg = <0x73>;
}
```

2. 构建新的设备树并拷贝到 `tftp` 文件夹：

`~/my-linux-imx$ source /opt/poky/1.7/environment-setup-cortex9hf-v-neon-poky-linux-gnueabi`

`~/my-linux-imx$ make imx6-sabresd.dtb`

`~/my-linux-imx$ cp /arch/boot/dts/imx6-sabresd.dtb /var/lib/tftp`

## 作为 I2C 交互的 IIO 框架

1. 包含所需的头文件：

```c
#include <linux/i2c.h> /* struct i2c_driver, struct i2c_client(), i2c-get_client_data(), i2c-set_client_data() */
```

2. 创建 `i2c_driver`：

```c
static struct i2c_driver ltc2607_driver = {
    .driver = {
        .name = LTC2607_DRV_NAME,
        .owner = THIS_MODULE,
        .of_match_table = dac_dt_ids,
    },
    .probe = ltc2607_probe,
    .remove = ltc2607_remove,
    .id_table = ltc2607_id,
};
```

3. 作为驱动程序注册到 `i2c` 总线：

```c
module_i2c_driver(ltc2607_driver);
```

4. 向驱动支持的设备列表添加 "`ltc2607`"：

```c
static struct device_id dac_dt_ids[] = {
    {.compatible = "arrow,ltc2607", },
};
MODULE_DEVICE_TABLE(of, dac_dt_ids);
```

5. 定义 `i2c` `device_id` 结构体数组：

```c
static const struct i2c_device_id ltc2607_id[] = {
    { "ltc2607", 0 },
};
MODULE_DEVICE_TABLE(i2c, ltc2607_id);
```

## 作为 IIO 设备的 IIO 框架

1. 如果驱动程序需要支持多个设备，则需要在物理设备（在本例中由物理总线处理）和逻辑设备（在本例中由子系统处理）之间保留指针。这样，当调用 `remove()` 例时（通常是总线检测到设备移除时），可以找到逻辑设备进行注销。相反，当逻辑侧发生事件时（例如执行 `IIO_raw` 回调函数），可以找到对应的 `i2c` 从机，以执行特定操作。

私有结构必须存储在某处。总线抽象给了我们指向 `struct device` 的 `void` 指针。

```c
struct ltc2607_device {
  struct i2c_client *client;
  char name[8];
}
```

3. 在 `ltc2607_probe()` 函数中，声明该结构的实例：

```c
struct ltc2607_device *data;
```

4. 为了在驱动程序的其他部分访问私有数据，需要使用 `iio_priv()` 函数将其附加到 `iio_dev` 结构上。你将使用相同的函数 `iio_priv()` 获取指向私有结构的指针 "`data`" 。在 `probe()` 中将数据附加到 `indio_dev`：

每个私有结构都是为每个 `probe` 动态分配的。

5. 在 `remove()` 函数中恢复我们的私有数据结构，你需要使用 `i2c_set_clientdata()` 将其附加到 `i2c_client` 结构中。该函数将指针 "`data`"（在第3步中声明）存储到私有结构 `dev->driver_data` 中。我们将使用 `i2c_get_clientdata(client)` 函数检索指针数据。

```c
i2c_set_clientdata(client, data);
data = i2c_get_clientdata(client);
```

6. 在 `ltc2607_probe()` 中分配 `indio_dev` 结构：

```c
indio_dev = devm_iio_dev_alloc(&client->dev,
               sizeof(*data));
```

7. 初始化 `IIO` 设备。在物理设备（在本例中由物理总线 `I2C` 处理的设备）和逻辑设备之间保持指针：
