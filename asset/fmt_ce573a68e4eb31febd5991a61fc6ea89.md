
## I2C 客户端驱动

打开并修改 `at91-sama5d2_xplained_common.dtsi` 设备树文件，在 `i2c1` 控制器节点内部添加 `ltc3206@1` 子节点。`ltc3206` 节点的 `pintrl-0` 属性指向 `pintrl_cs_default` 配置节点，在该节点中 PB25 焊盘被复用为 GPIO。

PB25 焊盘也被复用为 ic 节点的 GPIO。这包含在 `at91-sama5d2_xplained_07670.dtsi` 中。注释掉 `at91-sama5d2_xplained_common.dtsi` 内部的以下行：

`ltc3206` 节点的 `pintrl-0` 属性指向 `pintrl_cs_default` 配置节点，在该节点中 PB25 焊盘被复用为 GPIO。

`gpios` 属性将是驱动可用的 GPIO6 端口的 GPIO 14，这样你就可以将引脚方向设置为输出，并将物理电平从 0 驱动到 1 以控制 ENGRB/S 引脚。`reg` 属性提供了 LTC3206 的 I2C 地址。在 `ltc3206` 节点内部有五个子节点代表不同的显示设备。这五个节点中的每个节点都有一个 `label` 属性，以便驱动识别它们并使用提供的标签名称创建设备：

``` 
&ic3 {
clock-frequency = <100000>;
pintrl-names = "default";
pintrl-0 = <pinctrl_i2c3>;
status = "okay";
}
```

``` 
ltc3206: ltc3206@1b {
    compatible = "arrow,ltc3206";
    reg = <0x1b>;
    pintrl = <pintrl_cs>;
    gpios = <&gpio6 14 GPIO_ACTIVE_LOW>;
```

``` 
led1r {
label = "red";
}
```

``` 
led1b {
label = "blue";
}
```

``` 
led1g {
label = "green";
}
```

``` 
ledmain {
label = "main";
}
```

``` 
ledsub {
label = "sub";
}
```

## 第6章

### I2C 客户端驱动

``` 
sii902x: sii902x@39 {
    compatible = "SII,sii902x";
    pinctrl-names = "default";
    pinctrl-0 = <pinctrl_sii902x>;
    interrupt-parent = <gpio2>;
    interrupts = <13 IRQ_TYPE_EDGE_FALLING>
    mode_str="1280x70M@0";
    bits-per-pixel = <16>;
    reg = <0x9>;
    status = "okay";
}
};

[...]
};
```

查看位于 `iomux` 节点内部的 `pinctrl_cs` 配置节点，在该节点中 SAIL_TX_SYNC 焊盘被复用为 GPIO 信号：

``` 
pinctrl_cs: cs_gpiogrp {
    fsl,pins = <MXD_PD4_SAII1_TX_SYNC_GPIO6_IO14 0x2>
};
```

## 实验 6.2 SAMAD2 处理器的设备树

打开 SAMAD2B-XULT 板的原理图并查找 J22 连接器。你会发现 EXP_TWCK1_PD5 引脚连接到 SAMAD2 处理器的 PD5 焊盘，EXP_TWD1_PD4 引脚连接到 PD4 焊盘。你必须将 PD5 和 PD4 焊盘配置为 I2C 信号。要查找 `arch/arm/boot/dts/` 目录下 `sama5d2-pinfunc.h` 文件分配所需的 I2C 功能的宏，请找到下一个宏：

``` 
#define PIN_PD4__TWD1 PINMUX_PIN(PIN_PD4, 1, 2)
#define PIN_PD5__TCK1 PINMUX_PIN(PIN_PD5, 1, 2)
```

现在找到 J17 连接器。看到 ISC_D11/EXP_PB25 引脚连接到 SAMAD2 处理器的 PB25 焊盘。你必须将此引脚配置为 GPIO 信号。要查找 `arch/arm/boot/dts/` 目录下 `sama5d2-pinfunc.h` 文件分配所需的 GPIO 功能的宏，请找到下一个宏：

``` 
#define PIN_PB25__GPIO PINMUX_PIN(PIN_PB25, 0, 0)
```

## I2C 客户端驱动
