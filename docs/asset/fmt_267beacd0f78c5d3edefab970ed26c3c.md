
#include <linux/kthread.h>

struct task_struct *kthread_create(int (*threadfn)(void *data),
  void *data, const char namefmt[], ...);

```
- `threadfn` 是内核线程运行的函数。
- `data` 是发送给函数的参数。
- `namefmt` 代表内核线程名称，如 ps/top 中所示，可以包含 `%d`, `%s` 等，将根据 printf 语法进行替换。
```

例如，以下调用将创建一个名为 `mythread0` 的内核线程：

```c
kthread_create(func, NULL, "mythread%d", 0);
```

启动内核线程，调用 `wake_up_process()`：

```c
#include <linux/sched.h>
```

或者，可以使用 `kthread_run()` 来创建内核线程：

```c
struct task_struct *kthread_run(int (*threadfn)(void *data),
               void *data, const char namefmt[], ...);
```

停止线程，使用 `kthread_stop()`。该函数通过向线程发送信号来实现。结果是，线程会在某个任务中间被中断。但如果线程函数从未返回且不检查信号，它永远不会停止。

# 实验 7.3 "keyed class"

在本章的最后一个驱动程序中，你将结合之前章节在本中学到的许多概念来开发驱动程序。你将创建一个名为 Keyled 的新类。Keyled 类下将创建多个 LED 设备，每个 LED 设备下还会创建多个 sysfs 条目。你将通过用户空间写入注册到 Keyled 类的每个 LED 设备下的 sysfs 条目来控制每个 LED。在你的驱动程序中，将为每个设备初始化一个 `struct cdev`（添加 `file_operations` 结构体参数），然后将其添加到内核空间，这样你可以在 `/dev` 下看到可以使用系统调用控制的设备；通过写入 `/sys/class/Keyled/<led_device>/` 目录下的 sysfs 条目来控制 LED。

每个 LED 设备的闪烁周期将通过两个按钮通过中断进行增加或减少。一个内核线程将使用 `msleep()` 函数来切换到 LED 的 GPIO 输出值。

## 实验 7.3 i-MX7D 处理器的硬件描述

你将使用 i-MX7D 的三个引脚来控制每个 LED。这些引脚在 DT 中复用为 GPIO。查看 MCIM7D-SABRE 原图第 20 页查看 MikroBus 连接器。你将使用 MOSI 引脚控制绿色 LED，SCK 引脚控制蓝色 LED，以及 MKBUS_PWM 引脚控制红色 LED。

为了获取 LED，你将使用带有 microBOOST 节点的 Color click™ 配板。使用 https://www.mikroe.com/color-click 的 Color click 板。

将 MCIM7D-SABRE 的 PWM 引脚到 Color click 的 RD 引脚，MOSI 引脚到 GR，SCK 连接到 BL。从 MCIM7D-SABRE 板向 Color click 板提供 VCC = +5V，并在板之间连接 GND。

## 实验 7.3 SAMA5D2 处理器的硬件描述

你将使用 S5D2 的三个引脚来控制每个 LED。这些引脚在 DT 中复用为 GPIO。SAMA5D2B-XULT 板集成了一个 RGB LED。查看 SAMA5D2B-XULT 原图第 11 页查看 RGB LED：

| | | | | VDD_LED |
|---|---|---|---|---|
| [7] LED_RED_PB6 | R326 | 470R | Red | |
| [7] LED_GREEN_PB5 | R325 | 470R | Green | 阳极 2 |
| [7] LED_BLUE_PB0 | R328 | 470R | Blue | 3 |

查找 SAMA5D2B-XULT 原图并在第 11 页找到按钮 BP1。该按钮将用于生成其中一个中断。第二个中断将使用 MikroElektronika Button R click 板上的按钮生成。查看该板：https://www.mikroe.com/button-r-click。将 SAMA5D2 处理器的 PB25 焊盘（位于 SAMA5D2B-XULT 原图第 15 页的 J17 连接器引脚 30）连接到 Button R click 板的 INT 引脚。

# 第 7 章 设备驱动程序中的中断处理

## 实验 7.3 BCM2837 处理器的硬件描述

你将使用 BCM2837 的三个引脚来控制每个 LED。这些引脚必须在 DT（设备树）中复用为 GPIO。

为了获取这些 GPIO，你将使用 GPIO 扩展连接器。访问 Raspberry-Pi-3B-V1.2-Schematics 查看该连接器：

![](img/6ae71abd6b0ad6512145782465527d4b_316_0.png)

### GPIO 扩展

为了获取 LED，你将使用带有 mikroBUST™ 规格的 Color click™ 扩展板。访问 https://www.mikroe.com/color-click 查看 Color click™ 扩展板。你可以从上述链接或从本书的 GitHub 仓库下载原理图。

将 GPIO EXPANSION GPIO27 连接到 Color click™ 的 RD 引脚，GPIO22 连接到 GR，GPIO26 连接到 BL。

为了产生两种中断，你将使用两个 MikroElektronika Button R 按钮板。访问 https://www.mikroe.com/button-click 查看该板。你可以从该链接或本书的 GitHub 仓库下载原理图。将 GPIO 扩展连接器的 GPIO23 和 GPIO24 引脚连接每个 Button R 板的 INT 引脚。

## 实验 7.3 iMX7D 处理器的设备树

从 MCIM7D_SABRE microBUST 插座可以看出，MOSI 引脚连接到 iMX7D 的 SAI2_TXC 焊，SCK 引脚连接到 SAI2_RXD 焊，PWM 引脚连接到 GPIO1_IO02 焊。你必须将 SAI2_TXC、SAI2_RXD 和 GPIO1_IO02 焊配置为 GPIO 信号。要查找 `arch/arm/boot/dts/` 下 `imx7d-pinfunc.h` 文件中为所需 GPIO 功能分配的宏：

```
#MX7D_PAD_SAI2_TX_BCLK_GPIO06_IO20      0x0220 0x0490 0x0000 0x5 0x0
#MX7D_PAD_SAI2_RXD_DATA_GPIO06_IO21      0x0224 0x0494 0x0000 0x5 0x0
```

进入 `arch/arm/boot/dts/` 下的 `imx7d-pinfunc.h` 文件并找到以下宏：

```
#MX7D_PAD_GPIO1_IO02__GPIO1_IO02      0x0008 0x0338 0x0000 0x0 0x0
```

USRB1 按钮连接到 iMX7D 处理器的 SD2_WP 焊，USB0 连接到 iMX7D 处理器的 SD2_RESET 焊。要查找 `arch/arm/boot/dts/` 目录下 `imx7d-pinfunc.h` 文件中为所需 GPIO 功能分配的宏并找到以下宏：

```
#MX7D_PAD_SD2_WP__GPIO5_IO10      0x01b8 0x0420 0x0000 0x5 0x0
#MX7D_PAD_SD2_RESET_0_GPIO5_IO11      0x01b4 0x0424 0x0000 0x5 0x0
```

现在，你可以修改设备树文件 `imx7d-sdb`，其中添加以下代码：

```
/ {
  model = "Freescale i.MX7 Sabre5D Board";
  compatible = "fsl,imx7-sdb", "fsl,imx7";
  memory {
    reg = <0x08000000>;
  };
  [...]
```

```
ledpwm {
  compatible = "arrow,ledpwm";
  pinctrl-names = "default";
  pinctrl-0 = <&pinctrl_keys_gpio&pinctrl_gpio&pinctrl_gpio_led>;
  bp1 {
label = "KEY_1";
gpios = <&gpio5 10 GPIO_ACTIVE_LOW>;
tigger = "falling";
bp2 {
label = "KEY_2";
gpios = <&gpio5 11 GPIO_ACTIVE_LOW>;
