
```
tigger = "falling";

}
```
`nledred` {
`label` = `"led"`;
`colour` = `"red"`;
`gpios` = <&gpio1 2 GPIO_ACTIVE_LOW>;
}

`ledgreen` {
`label` = `"led"`;
`colour` = `"green"`;
`gpios` = <&gpio6 20 GPIO_ACTIVE_LOW>;
}

`ledblue` {
`label` = `"led"`;
`colour` = `"blue"`;
`gpios` = <&gpio6 21 GPIO_ACTIVE_LOW>;
}

[...]

`&iomuxc` {
`pintrl-names` = `"default"`;
`pintrl-0` = <&pintrl_hog_1>;
}

`nimx7d-sdb` {
`pintrl_hog_1`: hoggrp {
`fsl,pins` = <
MX7D_PAD_DC_BDR0__GPIO2_28 0x59
`pintrl_keys_gpio`: keys_gpio {
`fsl,pins` = <
MX7D_PAD_SD2_WP__GPIO5_IO10 0x32
MX7D_PAD_SD2_RESET__GPIO5_IO11 0x32;
`pintrl_led_s`: led_grp {
`fsl,pins` =
MX7D_PAD_SAI2_TX_BCLK_GPIO6_IO20 0x1
MX7D_PAD_SAI2_RXD_DATA__GPIO6_IO21 0x1;
[...]
`&iomuxc` {
`pintrl-names` = `"default"`;
`pintrl-0` = <&rlrl_2rl_rl_cs>;
}

`imx7d-sdb` {
`pintrl_hog_2`: hog-2 {
`fsl,pins` = <
MX7D_PAD_GPIO1_IO05 0x14
};
`pintrl_led`: led_grp {
`fsl,pins` =
MX7D_PAD_GPIO1_IO02 0x11
};
}

注意不要在设备树中重复配置同一个引脚。配置是由驱动程序设置的。如果两个驱动程序配置了同一个引脚，将应用最后一个驱动程序的设置。检查 `imx7d-sdb` 中的 `ecspi3` 节点，可以发现 `pintrl-0` 分配了 `"default"` 名称并指向 `pintrl_spi3` 和 `pintrl_spi3_cs` 节点：

```
pintrl_spi3_cs: ecspi3_cs_grp {
    fsl,pins = <
        MX7D_PAD_SA2_CD_GPIO5 0x800000
MX7D_PAD_SAI2_TX_DATA__GPIO6_IO22 0x2
}
```

```
pintrl_spi3: spi3_grp {
    fsl,pins = <
        MX7D_PAD_SAI2_TX_SYNC__ECSPI3_MISO 0x2
MX7D_PAD_SAI2_TX_BCLK__ECSPI3_MOSI 0x2
MX7D_PAD_SAI2_RXD_DATA__ECSPI3_SCLK 0x2
}
```

可以看到 `SAI2_TX_BCLK` 和 `SAI2_RX_DATA` 被两个不同的驱动程序配置。你可以注释掉 `ecspi3` 的整个定义，或者通过将 `status` 设置为 `"disabled"` 来禁用。如果选择第二个选项，请下面的代码：

```
&ecspi3 {
    fsl,spi-num-selects = <1>;
    pintrl-names = "default"
    pintrl-0 = &pintrl_spi3 &pintrl_spi3_cs;
    cs-gpios = &gpio5 9 GPIO_ACTIVE_HIGH, &gpio6 22 0x2;
    status = "disabled"
}
```

# 7.3 SAM5D2 处理器的设备树

从 `SAM5D2B-XULT` 可以看出 `LED_RED_PB6` 引脚连接到 `SAM5D2` 处理器的 `PB6` 焊，`LED_GREEN_PB5` 引脚连接到 `PB5` 焊，`LED_BLUE_PB0` 引脚连接到 `PB0` 焊。你需要将 `PB6`、`PB5` 和 `PB0` 配置为 `GPIO` 信号。查找分配所需功能（`GPIO`）的宏，进入 `arch/arm/boot/dts/` 下的 `sama5d2-pinfunc.h` 并找到宏：

```
#define PIN_PB6_GPIO   PINMUX_PIN(PIN_PB6, 0, 0)
#define PIN_PB5_GPIO   PINMUX_PIN(PIN_PB5, 0, 0)
#define PIN_PB0_GPIO   PINMUX_PIN(PIN_PB0, 0, 0)
```

对于板，你必须将 `SAMA5D2` 处理器的 `PB9` 和 `PB25` 焊配置为 `GPIO` 信号。查找分配所需功能（`GPIO`）的宏，进入 `linux/arch/boot/dts/` 下的 `sama5d2-pin file` 并找到以下宏：

```
#define PIN_PB9__GPIO   MUX_PIN(PB9, 0, 0)
#define PIN_PB25__GPIO   MUX_PIN(PB25, 0, 0)
```

`PB25` 焊点也被复用为 `GPIO`：

```
pintrl_adc_default: adc_default {
    pinmux = <PD23__GPIO>;
    bias-disable;
}

[...]

pintrl_key_gpio_default: key_gpio_default {
    key {
        pinmux = <PB25__GPIO,
               <PB9__GPIO>;
        bias-pull-up;
    }

    led {
        pinmux = <PB0__GPIO,
               <PB5__GPIO,
               <PB6__GPIO>;
        bias-pull-up;
    }
}

[...]
}/ {
    model = "Atmel SAMAD2 Xplained";
    compatible = "atmel,sama5d2-xplained", "atmel,sama5d2", "atmel,sama55";

    chosen {
        stdout-path = "serial0:115200n8";
    };

[...]
ledpwm {
  compatible = "arrow,ledpwm";
  pinctrl-names = "default";
  pinctrl-0 = <&pintrl_led_gpio_default>;
}
bp1 {
  label = "PB_KEY";
  gpios = <&gpioA 41 GPIO_ACTIVE_LOW>;
  tigger = "falling";
}
p2 {
  label = "MIKROBUS_KEY";
  gpios = <&gpioA 57 GPIO_ACTIVE_LOW>;
  tigger = "falling";
}
red {
  label = "led";
  colour = "red";
  gpios = <&gpioA 38 GPIO_ACTIVE_LOW>;
}
green {
  label = "led";
  colour = "green";
  gpios = <&gpioA 37 GPIO_ACTIVE_LOW>;
}
blue {
  label = "led";
  colour = "blue";
  gpios = <&gpioA 32 GPIO_ACTIVE_LOW>;
}
}
```

# 设备驱动程序中的中断处理

`leds` {
```c
compatible = "gpio-leds";
pintrl-names = "default";
pintrl-0 = <&pintrl_led_gpio_default>;
status = "disabled";
```
`red` {
```c
label = "red";
ngpios = <&pio_A 38 GPIO_ACTIVE_LOW>;
```
};
`green` {
```c
label = "green";
ngpios = <&pio_A 37 GPIO_ACTIVE_LOW>;
```
};
`blue` {
```c
label = "blue";
ngpios = <&pio_A 32 GPIO_ACTIVE_LOW>;
```
};
`linux,default-trigger` = `"heartbeat"`;
