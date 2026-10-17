
Updating cache...###################### [100%]

Computing transaction...

Removing packages (1):

`i2c-tools-3.1.1-r0@cortexa9hf_vfp_neon`

释放了 79.3kb。

确认更改？(Y/n):

# 将 Linux 内核模块移植到 HummingBoard

现在描述所需的设备树（Device Tree）和内核源文件。所有设备树修改将在 `imx6qdl-hummingboard.dtsi` 文件中进行（位于 `Linux/arch/boot/dts`）。将使用 MikroBus 连接到外部设备（查看原理图第 6 页![](img/739ab59067f8a55eff0a58765146f339.png)）。在第 5 章之前开发的驱动程序不需要任何修改即可移植到 HummingBoard。

## LAB 5.2: "LED Platform device" 模块和 LAB 5.3: "LED fsfs device" 模块

将 "MikroEle Button" 连接到 HummingBoard 的 `PWM1_OUT` 引脚。iMX6 芯片上的每个引脚（pad）都有 NXP 分配的名称。`PWM1_OUT` 引脚连接到 `DIS_DAT8`（查看 SOM 原理图第 4 页）。对于 `DIS_DAT8` 引脚，它是 `GPIO4_29`。

打开 `imx6qdl-hummingboard2.dtsi` 文件。在 `&iomux` 节点内处添加 `hellokeys` 和 `pinctrl_led` 配置节点：

```
hellokeys {
    compatible = "arrow,hellokeys";
    reg = <0x02A8000 0x4000>;
    gpios = <gpio4 29 0>;
    pinctrl-0 = <&pinctrl_led>;
};
```

```
pinctrl_led: led {
    pins = <MXQDL_PAD_DIS_DAT8 GPIO4_IO029 0x8000000>;
};
```

在 `led_platform.c` 和 `led_sysfs_platform.c` 驱动源文件中替换以下代码行：

```
#define GPIO_DIR_MASK (1 << 2); /* bank 中的 GPIO 号 */
#define GPIO_DATA_MASK (1 << 2); /* bank 中的 GPIO 号 */
```

替换为这些新内容：

```
#define GPIO_DIR_MASK (1 << 29)
#define GPIO_DATA_MASK (
```

在上述驱动源文件中将 GPIO 数据和方向地址更改为 GPIO4 端口地址（查看 IMX6DQ 原理图第 1422 页），如下代码所示：

| 地址 | 描述 | 宽度 | 类型 | 值 | 引用 |
|---|---|---|---|---|---|
| 20A_8000 | GPIO 数据寄存器 (GPIO4_DR) | 32 | R/W | 0000_0000h | 28.5.1/1423 |
| 20A_8004 | GPIO 方向寄存器 (GPIO4_GDIR) | 32 | R/W | 0000_0000h | 28.5.2/1424 |

```
static int GPAT = 0x02A8000;
static int GPDIR = 0x02A004;
```

## LAB 5.4: "LED UIO Platform device" 模块

在 `UIO_app.c` 中替换以下代码行：

```
#define GPIO2_GDIR_offset 0x04
#define GPIO_DIR_MASK (1 << 2); /* bank 中的 GPIO 号 */
#define GPIO_DATA_MASK (1 << 2); /* bank 中的 GPIO 号 */
```

替换为这些新内容：

```
#define GPIO4_GDIR_offset 0x04
#define GPIO_DIR_MASK (1 << 29)
#define GPIO_DATA_MASK (1 << 29)
```

打开 `imx6qdl-hummingboard2.dtsi` 文件。添加 UIO 节点：

```
UIO {
  compatible = "arrow,UIO";
  reg = <0x02A8000 0x4000>;
};
```

## LAB 6.1: "Switch interrupt device" 模块

将开关（Switch click）连接到：

```
intkey {
    compatible = "arrow,intkey";
    reg = <0x02A8000 0x4000>;
    pios = <gpio4 27 0>;
    interrupts = <27 IRQ_TYPE_BOTH>;
    interrupt-parent = <&gpio>;
};
```

将 `PWM1_OUT` 引脚连接到 `imx6qdl-hummingboard2.dtsi` 文件。添加 `intkey` 节点：

```
intkey {
    compatible = "arrow,intkey";
    reg = <0x02A8000 0x4000>;
    pios = <gpio4 27 0>;
    interrupts = <27 IRQ_TYPE_BOTH>;
    interrupt-parent = <&gpio>;
};
```

## LAB 6.3: "Switch gpioolib platform device" 模块

在 HummingBoard 上，使用 GPIO 号 125 控制 LED。现在使用以下 shell 命令从用户空间控制 LED：

注意最初 `gpio125` 不存在，但在将其导出到用户空间后就存在了：

```
root@imx6qsolidrun:~# echo 125 > /sys/class/gpio/export
```

将 GPIO 配置为输出：

```
root@imx6qsolidrun:~# echo out > /sys/class/gpio/gpio125/direction
```

切换 LED 开启状态：

```
root@imx6qsolidrun:~# echo 1 > /sys/class/gpio/gpio125/value
root@imx6qsolidrun:~# echo 0 > /sys/class/gpio/gpio125
```

取消 GPIO 引脚导出，以便从内核空间使用：

```
root@imx6qsolidrun:~# echo 125 > /sys/class/gpio/unexport
```

## 实验 9.1: “输入子系统加速度计”模块

HummingBoard 没有连接到 i.MX6 i2c 总控制板加速度计。因此，你需要将 HummingBoard 连接到包含加速度计的外部板上。你可以使用 NXP LFSTBEB8845X 的 MMA8451 子板：用于 MMA845X 的传感器工具箱加速度计板，地址 http://www.npx.com/products/sensors/accelerometers/3-axis-accelerometers/sensor-toolbox-accelerometer-board-for-mma845x/LFSTBEBB845X。

将子板连接到 i.MX6 i2c3 总控制器，该控制器可以通过 HummingBoard microBUS Click 模块访问。打开 `imx6dl-hummingboard2.dtsi` 文件。在 `i2c3` 节点内部添加 `mma8451` 节点：

```
clock-frequency = <100000>;
pintrl-names = "default";
pintrl-0 = <<pintrl_hummingboard2_i2c3>;
status = "okay";
mma8451@i2c {
    compatible = "arrow,mma8451";
    reg = <0x1c>;
}
```

需要 `evtest` 应用程序来测试此驱动。该应用程序未包含在 "core-image-x11" 中。

查看我们的 "core-image-x11" 提供的包以验证是否未包含 `evtest` 应用程序：

```
~/solidrun-release-bsp/poky$ source oe-init-build-env
~/solidrun-release-bsp/poky/build$ bitbake -g core-image-x11
```
