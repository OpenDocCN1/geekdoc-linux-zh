
## 实验 6.1: “I2C I/O 扩展器设备”模块

在接下来的实验中，你将实现第一个驱动程序来控制 I2C 设备。该驱动程序将管理连接到 I2C 总线的 PCF8574 I/O 扩展器。你可以基于此设备的多个开发板来完成此实验，下一个实验参考：https://www.waveshare.com/gcf8574-io-expansion-board。

### 实验 6.1 用于 i.MX7D 处理器的硬件描述

在本实验中，你将使用 MCIM7D-SABRE microBUS™ 的 I2C 引脚连接到 PCF8574 I/O 扩展板。

查看 MCIM7D-SABRE 电原理图的第 20 页以查看 MicroBus 连接器，并寻找 SDA 和 SCL。将这些引脚连接到 PCF8574 I/O 扩展板上的相应引脚。同时在两个板之间连接 VCC 3.3V 和 GND。

### 实验 6.1 用于 SAMA5D2 处理器的硬件描述

对于 SAMA5D2 处理器，打开 SAMA5DB-XULT 原理图，寻找板上带有 i2c 信号引脚的连接器。SAMA5D2B-XULT 拥有五针、单针、单针和一个36 针插座（J7, J8, J9, J16, J17, J20, J21, J22），用于启用各种扩展卡的 PIO 连接。这些插字的物理和电气实现与 Arduino R3 扩展（扩展板）系统匹配。

你可以通过 J22 插座访问 I2C 信号，如下一步所示：

![](img/6ae71abd6b0ad6512145782465527d4b_215_0.png)

### 第 6 章

#### I2C 客户端驱动

你也可以从 ISC J18 插座获取相同的 TWCK1、TWD1 I2C 信号，如下所示。在两个不同的连接器上具有相同的信号可以简化与多块 PCF8574 板的连接。你也可以从此 J18 连接器获取 3V3 和 GND 信号。

#### ISC

![](img/6ae71abd6b0ad6512145782465527d4b_216_0.png)

### 实验 6.1 用于 BCM2837 处理器的硬件描述

对于 BCM2837 处理器，你将使用 GPIO 扩展连接器获取 I2C 信号。打开 Raspberry-Pi-3B-V1.2 原理图查看连接器。GPIO2 和 GPIO3 引脚将用于获取 SDA1 和 SCL1 信号。

![](img/6ae71abd6b0ad6512145782465527d4b_217_0.png)

#### GPIO 扩展

### 实验 6.1 用于 iMX7D 处理器的设备树

从 MCIM7D-SABRE 看到 MKBUS_I2C_SCL 连接到 iMX7D 处理器的 I2C3 焊盘，以及 MKBUS_I2C_DA 焊盘。你需要将这些焊盘配置为 I2C 信号。在 `linux/arch/boot/dts/` 中查找 `imx7d.h` 中分配所需 I2C 功能的宏：

```
#define MX7D_PAD_I2C3_DA

#define MX7D_PAD_I2C3_SCL
```

### 第 6 章

现在，你可以修改设备树文件 `imx7d-dsb.dts`，添加 `ioexp@38` 和 `ioexp@39` 子节点，启用 i2c3 控制器主。`clock-frequency` 属性设置为 100K，`pinctrl-0` 属性指向 `pintrl_i2c3` 配置节点，其中 I2C3_SDA 和 I2C3_SCL 焊盘复用为 I2C 信号。`reg` 属性提供了连接到 I2C 总线的两个 PCF8574 I/O 扩展器的地址。

```
&i2c3 {
clock-frequency = <100000>;
pinctrl-names = "default";
pinctrl-0 = <pintrl_i2c3>;
status = "okay";
};
```
```
ioexp@38 {
compatible = "arrow,ioexp";
reg = <0x38>;
}
ioexp@39 {
compatible = "arrow,ioexp";
reg = <0x39>;
}
```
```
ii902x@39 {
compatible = "ii902x";
pinctrl-names = "default";
pinctrl-0 = <pintrl_ii902x>;
interrupt-parent = &gpio2;
interrupts = <13 IRQ_TYPE_FALLING>;
mode_str = "<120M@60";
bits-per-pixel = <16>;
reg = <0x39>;
status = "okay";
}
```
```
[...]
```

查看下方的 `pintrl_i2c3` 引脚配置节点，I2C 控制器焊盘复用为 I2C 信号：

```
pinctrl_i2c3: <
fsl,pins = <MX7D_PAD_I2C3_SDA 0x4000007f
MX7D_PAD_I2C3_SCL 0x4000007f
>;
```

#### I2C 客户端驱动

### 实验 6.1 用于 SAMA5D2 处理器的设备树

打开 SAMA5D2B-XULT 原理图查看 J22 连接器。看到 EXP_TW1_PD5 引脚连接到 SAMA5D2 处理器的 PD5 焊盘，EXP_TWDI_PD4 引脚连接到 PD4 焊盘。你需要将 PD5 和 PD4 焊盘配置为 I2C 信号。在 `linux/arch/arm/boot/dts/` 目录下的 `Sama5d2-pinfunc.h` 文件中查找分配所需 I2C 功能的宏。在下方加粗显示用于配置 PD4 和 PD5 焊盘为 I2C 信号的所需宏：

```
#define PIN_PD4
#define PIN_PD4_GPIO
#define PIN_PD4_TWD1
#define PIN_PD4_UXD2
#define PIN_PD4_GCOL
#define PIN_PD4_ISC_D10
#define PIN_PD4_NCS0
#define PIN_PD5
#define PIN_PD5_GPIO
#define PIN_PD5_TWCK1
#define PIN_PD5_UTX2
#define PIN_PD5_GRX2
#define PIN_PD5_ISC_D9
#define PIN_PD5_NCS1

100
PINMUX_PIN(PIN_PD4, 0, 0)
PINMUX_PIN(PIN_PD4, 1, 2)
PINMUX_PIN(PIN_PD4, 2, 1)
PINMUX_PIN(PIN_PD4, 4, 2)
PINMUX_PIN(PIN_PD4, 5, 2)
PINMUX_PIN(PIN_PD4, 6, 2)
101
PINMUX_PIN(PIN_PD5, 0, 0)
PINMUX_PIN(PIN_PD5, 1, 2)
PINMUX_PIN(PIN_PD5, 2, 1)
PINMUX_PIN(PIN_PD5, 4, 2)
PINMUX_PIN(PIN_PD5, 5, 2)
PINMUX_PIN(PIN_PD5, 6, 2)
```

注意：每个外设的 I/O 被组分为 IO 组，列在“IO Set”列中。对于所有外设，必须使用属于同一 组的 I/O。如果混合了来自不同 IO 组的 I/O，则无法保证时序。

| 引脚 | 功能 | IO 组 |
|---|---|---|
| PD4 | TWD1 | 1 |
| PD5 | TWCK1 | 2 |

### 实验 6.1 BCM2837 处理器的设备树

打开并修改 `bcm2710-rpi-3-b.dts` 设备树，使用 i2c master 节点添加 `ioexp@38` 和 `ioexp@39` 子节点。通过向 `status` 属性写入 "okay" 来启用 I2C 控制器。主节点的 `pincrl-0` 指向 `i2c1_pins` 配置节点，其中 GPIO2 和 GPIO3 引脚被复用为 I2C 信号。在子节点中，`reg` 属性提供了连接到 I2C 总线的两个 PCF8574 I/O 扩展器的 I2C 地址。

```c
&i2c1 {
    pinctrl-names = "default";
    pinctrl-0 = &i2c1_pins;
    clock-frequency = <1000000>;
    status = "okay";
}
```

```c
ioexp@38 {
    compatible = "arrow,ioexp";
    reg = <0x38>;
}
```

```c
ioexp@39 {
    compatible = "arrow,ioexp";
    reg = <0x39>;
}
```

查看 `i2c1_pins` 引脚配置节点，其中 I2C 控制器引脚被复用为 I2C 信号：

```c
i2c1_pins: i2c1 {
    brcm,pins = <2 3>;
    brcm,function = <4>;
    /* GPIO2 and GPIO3 pins */
    /* ALT0 复用功能 */
}
```
