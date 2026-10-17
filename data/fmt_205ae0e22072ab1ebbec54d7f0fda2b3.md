
`module_i2c_driver(ioaccel_driver);`

## 客户端驱动

在你的设备驱动中，你应该存储与 DT 节点兼容属性相同的 `device_id` 结构体值。`struct device_id` 定义在 `include/linux/dt.h` 中：

```
struct device_id {
    char name[32];
    char type[32];
    char compatible[128];
};
```

`struct i2c_driver`（在驱动中）的 `match` 字段指向驱动支持的 `device_id` 数组指针：

```
static const struct device_id ioaccel_dt_ids[] = {
    .compatible = "mma8451",
};
MODULE_DEVICE_TABLE(of, ioaccel_dt_ids);
```

当 `device_id` 条目的 `compatible` 字段与 DT 节点的兼容属性匹配时，调用驱动的 `probe()` 函数。`probe()` 函数负责从匹配的 DT 获取配置并将设备注册到框架。在你的 I2C 设备驱动中，你还需要定义一个 `device_id` 数组：

```
static const struct device_id mma8451_id[] = {
    { "mma8450", 0 },
    { "mma8451", 1 },
};
```

`probe()` 函数的第二个参数是数组中与连接设备相关的元素：

```
static int ioaccel_probe(struct i2c_client *client, const struct device_id *id)
```

你可以使用 `id->driver_data`（每个设备唯一），用于特定数据。例如，对于 `"mma8451"` 设备，`driver_data` 将为 1。I2C 核心首先尝试通过兼容字符串（OF 类型，即设备树）匹配设备，如果失败，则通过 id 表匹配。

## 设备树中的 I2C 设备

在设备树中，I2C 控制器通常在描述处理器的 `.dtsi` 文件中声明（对于 i.MX7D 查看 `arch/arm/boot/imx7s.dtsi`）。DT I2C 控制器通常声明为 `status="disabled"`。例如，在 `imx7s.dtsi` 文件中有四个 DT I2C 控制器通过 `of_platform_populate` 函数注册到 I2C 总线核心。对于 i.MX7D，i2c-mx 驱动使用 `module_i2c_driver()` 到 I2C 总线核心；`probe` 函数将被调用四次（每个匹配一次 `"fsl,imx21-i2c"`），为每个控制器初始化 `struct i2c_adapter` 结构并注册到 I2C 总线核心。见下方 i.MX7D DT I2C 控制器节点：

```
i2c1: i2c@30a2000 {
    #address-cells = <1>
    #size-cells = <0>
    compatible = "fsl,imx7d-i2c", "fsl,imx21-i2c";
    reg = <0x30a2000 0x010000>
    interrupts = <GIC_SPI 36 IRQ_TYPE_LEVEL_HIGH>
    clocks = <clks IMX7D_I2C1_ROOT_CLK>
    status = "disabled"
};
```

```
i2c2: i2c@30a30000 {
    #address-cells = <1>
    #size-cells = <0>
    compatible = "fsl,imx7d-i2c", "fsl,imx21-i2c";
    reg = <0x30a30000 0x010000>
    interrupts = <GIC_SPI 36 IRQ_TYPE_LEVEL_HIGH>
    clocks = <clks IMX7D_I2C2_ROOT_CLK>
    status = "disabled"
};
```

```
i2c3: i2c@30a40000 {
    #address-cells = <1>
    #size-cells = <0>
    compatible = "fsl,imx7d-i2c", "fsl,imx21-i2c";
    reg = <0x30a40000 0x010000>
    interrupts = <GIC_SPI 37 IRQ_TYPE_LEVEL_HIGH>
    clocks = <clks IMX7D_I2C3_ROOT_CLK>
    status = "disabled"
};
```

```
i2c4: i2c@30a50000 {
    #address-cells = <1>
    #size-cells = <0>
    compatible = "fsl,imx7d-i2c", "fsl,imx21-i2c";
};
```

`reg = <0x30a50000 0x10000>; ninterrupts = <GIC_SPI 38 IRQ_TYPE_LEVEL_HIGH>; nclocks = <clks IMX7D_I2C4_ROOT_CLK>`

`status = "disabled";`

I2c 设备的设备树声明被作为主控制器的子节点启用。在板层级/平台级（`arch/arm/boot/dts/imx7d-dsb.dts`）中：

- I2C 控制器设备已启用（`status = "okay"`）。
- I2C 总线频率通过 `clock-frequency` 属性定义。
- 板板上的 I2C 设备被描述为 I2C 控制器节点的子节点，其中 `reg` 属性提供总线上的 I2C 从机地址。
- 在 I2C 节点中，`device_id` 检查 `compatible` 属性是否匹配驱动程序的 `of_device_id` 兼容字符串之一。

在 DT 文件 `imx7d-dsb.dts` 中声明了 i2c4 控制器节点。通过向 `status` 属性写入 `"okay"` 来启用 i2c4 控制器。在 codec 子节点声明中，`reg` 属性提供了 wm8960 设备的地址。

```
&i2c4 {
    pintrl-names = "default";
    pintrl-0 = <pintrl_i2c4>; status = "okay";
    codec: wm8960@1a {
        compatible = <"wlf,wm8960">
        reg = <0x1a>; nclocks = <clks IMX7D_AUDIO_MCLK_ROOT_CLK>
        clock-names = "mclk";
        wlf,shared-rlcl
    }
};
```

i2c4 节点内部的 `pintrl-0` 属性指向 `pintrl_i2c4` 引脚功能节点，i2c4 控制器的焊盘与 I2C 功能复用。

```
pintrl_i2c4: <
    fsl,pins = mX7D_PAD_SAI1_RX_BCLK I2C4_SDA 0x4000007f
    MX7D_PAD_SAI1_RX_SYNC I2C4_SCL 0x4000007f
>;
```

# 第 6 章

## I2C 客户端驱动
