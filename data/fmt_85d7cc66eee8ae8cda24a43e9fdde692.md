
```gpio: gpio@7e200000 {
    compatible = "brcm,bcm2835-gpio";
    reg = <0x7e200000 0xb4>;
/*
* GPIO IP 块设计用于 3 个 GPIO bank。
* 每个 bank 都有一个自己的 GPIO 中断。
* 有一个总的“任意 bank”中断。
* 按顺序，这些中断是 GIC 中断 17, 18, 19, 20。
* 由于 BCM2835 只有 2 个 bank，第 2 个 bank
* 中断输出似乎镜像到了第
* 3 个 bank 的中断信号上。
* 所以，bank0 中断出现在 17, 20 上，
* bank1 中断出现在 18, 19 上！
*/
interrupts = <2 17>, <2 18>, <2 19>, <2 20>;

gpio-controller;
#gpio-cells = <2>;

interrupt-controller:
#interrupt-cells = <2>;
/* 定义引脚复用组
* 虽然每个引脚可以单独为各种功能
* 选择其复用，但某些
* 组只能一起切换到
* 特定的功能。
*/
dipi_gpio0: dpi_gpio {
brcm,pins = <0 1 2 3 4 5 6 7 8 9 10 11
    12 13 14 15 16 17 18 19
    20 21 22 23 24 25 26 27>;
brcm,function = <BCM2835_FSEL_ALT2>;
};
emmc_gpio22: emmc_gpio22 {
brcm,pins = <22 23 24 25 26 27>;
brcm,function = <BCM2835_FSEL_ALT3>;
};

...
di2c0_gpio0: i2c0_gpio0 {
brcm,pins = <0 1>;
brcm,function = <BCM2835_FSEL_ALT0>;
};
i2c0_gpio28: i2c0_gpio28 {
brcm,pins = <28 29>;
brcm,function = <BCM2835_FSEL_ALT0>;
};

...
spi0_gpio7: spi0_gpio7 {
brcm,pins = <7 8 9 10 11>;
brcm,function = <BCM2835_FSEL_ALT0>;
};
spi0@gpio35: spio0@gpio35 {
  brcm,pins = <35 36 37 38 39>;
  brcm,function = <BCM2835_FSEL_ALT0>;
};

[...]

uart1_gpio40: uart1@gpio40 {
  brcm,pins = <40 41>;
  brcm,function = <BCM2835_FSEL_ALT5>;
};
uart1_ctsrts_gpio42: uart1_ctsrts_gpio42 {
  brcm,pins = <42 43>;
  brcm,function = <BCM2835_FSEL_ALT5>;
}
```
```

`gpio@7e200000` 节点的 `compatible` 属性值与 `pinctrl-bcm2835.c` 引脚驱动程序中的 `compatible` 字段值匹配。

引脚控制器设备应该包含用于每个客户端设备的引脚配置节点。BCM2837 SoC 为每个客户端设备引脚控制器节点。这方面尚没有通用标准。这些引脚配置子节点的内容由绑定（binding）定义。每个引脚配置节点列出了它适用的引脚、一个或多个复用功能以及上拉/下拉配置。

- `brcm,pins`: 单元数组。每个单元包含引脚 ID。有效 ID 为整数：GPIO0, GPIO1, ...53。

- `brcm,function`: 用于复用引脚的整数：

  - 0: GPIO in

  - 1: GPIO out

  - 2: alt5

  - 3: alt4

  - 4: alt0

  - 5: alt1

  - 6: alt2

- `brcm,pull`: 应用于引脚的下拉/上拉整数：

  - 0: none

  - 1: down

  - 2: up

更多信息请访问 `bindings/pinctrl/` 并检查 `bcm2835-gpio.dt` 文件。对于本实验，通过在 SoC 中添加 `led_pins` 节点、`ledgreen` 和 `ledblue` 节点来修改树莓派3设备树文件：

``` 
/ {
  model = "Raspberry Pi 3";
};

&gpio {
  spi0_pins: spi0_pins {
    brcm,pins = <9 10 11>;
    brcm,function = <4>; /* alt0 */
  };

  spi0_cs_pins: spi0_cs_pins {
    brcm,pins = <8 7>;
    brcm,function = <1>; /* output */
  };

  i2c0_pins: i2c0 {
    brcm,pins = <0 1>;
    brcm,function = <4>;
  };

  led_pins: led_pins {
    brcm,pins = <27 22 26>;
    brcm,function = <1>; /* Output */
    brcm,pull = <1>; /* Pull down */
  };
};

&soc {
  virtgpio: virtgpio {
    compatible = "brcm,bcm2835-virtgpio";
    gpio-controller;
    #gpio-cells = <2>;
    firmware = <&firmware>;
    status = "okay";
  };

  hellokeys {
    compatible = "arrow,hellokeys";
  };
};

ledred {
  compatible = "arrow,RGBBled";
  label = "ledred";
  pinctrl-0 = <&led_pins>;
};

ledgreen {
  compatible = "arrow,RGBBled";
  label = "ledgreen";
};

ledblue {
  compatible = "arrow,RGBBled";
  label = "ledblue";
};
```

## 实验 5.2 “RGB LED平台”的代码描述

现在描述驱动的主要代码部分：

### 1. 包含函数头文件：

```c
#include <linux/module.h>

#include <linux/fs.h> /* struct file_operations

#include <linux/platform_device.h> /* platform_driver_register(), platform_set_drvdata() */

#include <linux/io.h> /* dev_ioremap(), iowrite32() */

#include <linux/of.h> /* of_property_read_string() */

#include <linux/uaccess.h> /* copy_from_user(), copy_to_user() */

#include <linux/miscdevice.h> /* misc_register()
```

### 2. 定义用于配置 GPIO 寄存器的掩码。见下方 BCM2837 处理器的掩码：

```c
#define GPIO_27 27

#define GPIO_22 22

#define GPIO_26 26
```

```c
/* 设置和清除每个 LED */
#define GPIO_27_INDEX 1 << (GPIO_27 % 32)

#define GPIO_22_INDEX 1 << (GPIO_22 % 32)

#define GPIO_26_INDEX 1 << (GPIO_26 % 32)
```

```c
/* 选择输出功能 */
#define GPIO_27_FUNC 1 << ((GPIO_27 % 10) * 3)

#define GPIO_22_FUNC 1 << ((GPIO_22 % 10) * 3)

#define GPIO_26_FUNC 1 << ((GPIO_26 % 10) * 3)
```

```c
/* 掩码 GPIO 功能 */
/* 选择 GPIO 27，你将把 GPIO 备用选择寄存器 2 的第 23 位 (FSEL7) 设置为 0b111。GPIO 引脚 27 将控制红色 LED */
#define FSEL_27_MASK      0x7 << ((GPIO_27 % 10) * 3) 
```
