
下面的图表示了中断硬件（SW5 按钮键）与 i.MX6 SoC 中断控制器之间的 DT 连接。该方案将在本章稍后的部分用于你的第一个管理中断的内核模块。请查看 `Linux/arch/arm/boot/dts/imx6qldli.dtsi` 文件中每个中断节点控制器的声明。

# 第 6 章

![](img/739a35b59067f8a55eff80a58765146f_230_0.png)

## i.MX6 SoC

| SW5 | gpio1_5 | gpio1:gpio@0209c000 hwirq = 92 | intc compatible = arm,cortex-a9-gic |
| hwirq = 5 | compatible = "fsl,imx6q-gpio" | | Cortex-A CPU |

SABRE 板的 SW5 按钮键将通过 gpio1 控制器的 `gpio1_5` 引脚连接到 i.MX6 处理器的八个掩码中的一个。

在 i.MX6 处理器中，每个 GPIO 输入都有一个专用的边缘检测电路，可以通过软件配置以检测输入信号上的上升沿、下降沿、逻辑低电平或逻辑高电平。边缘检测电路的可以通过设置中断掩码寄存器 `GPIO_IMR` 中的相应位来可选地掩码。这些筛选后的输出通过或（OR）逻辑组合生成两个单位的中断线：

- GPIOx 信号 0 - 15 的组合中断指示
- GPIOx 信号 16 - 31 的组合中断指示

此外，GPIO1 提供了其每个高低位中断源的可视性（即 GPIO1 中断 n，n = 0 - 7）。然而，无法获取其他 GPIOx 的单独中断指示。

处理 SW5 后，`gpio1_5` 引脚将发生电平变化，导致 GPIO 控制器产生硬件 irq 编号为 5 的中断，此中断将通过硬件 irq 编号为 98 的 IRQ 信号通知 GIC 中断控制器（见表 205）。

## 平台驱动程序中的中断处理

3.1. IMX6DQRM 第 221 页上的 ARM 域中断摘要。GIC 将相应的 IRQ 信号转发给一个或两个 A9 核心。运行在 A9 核心上的软件代码可以查询 GIC 以确定哪个外设设备导致了中断，并采取适当的操作。

存在链中断（chained interrupts）方法，这意味着对于 GPIO 有一个快速 IRQ 处理程序，它会在从父 IRQ 处理程序（通常是系统中断控制器）的链中被调用。这意味着 GPIO irq 是使用 `irq_set_chained_handler()` 或相应的 `gopchip_set_chained_irq()` 辅助函数注册的。

查看 `Linux/drivers/gpio/gpio-mxc.c` 中 i.MX6 系统中断控制器的处理程序设置：

```c
/* 为每个项目设置处理程序 *
irq_set_chained_handler(port->irq, mx3_gpio_irq_handler);
irq_set_handler_data(port->irq, port);
if (port)->irq > 0) {
    /* 为 GPIO 16 到 31 设置处理程序 */
    irq_set_chained_handler(port->irq_high,
        mx3_gpio_irq_handler);
    irq_set_handler_data(port->irq_high, port);
}
```

GPIO irqchip 处理程序将在禁用 IRQ 的情况下立即从父级 irqchip 处调用。GPIO irqchip 随后会在其中断处理程序中调用如下的序列：

```
chained_irq_enter(...);
generic_handle_irq(...);
chained_irq_exit(...);
```

在 `Linux/drivers/gpio/gpio-mxc.c` 中查看 GPIOqchip 处理程序：

```c
static void mx3_gpio_irq_handler(struct irq_desc *desc) {
    u32 irq_stat;
    struct mxc_port *port = irq_get_data(irq);
    struct irq_chip *chip = irq_get_chip(irq);

    chained_irq_enter(chip);
    irq_stat = readl(port->base + ISR) & readl(port->base + GPIO_IMR);

    ir___handler(port);
    chained_irq_exit(chip);
}
```

这是中断传播描述（在 GIC 的左侧）：

- 1. 处于中断上下文（`interruptchip-gic.c`）。`generic_handle_irq(irq)` 调用了 `_handle_irq(irq)`。
- 2. 现在处于中断上下文（`gpio-mxc.c`）。使用 `__request_irrequest(irq)`。
- 3. 注册 SW5 中断使用 `devm_request_irq()`。

## i.MX6 SoC 硬件操作

NXP iMX 设备全局中断控制器（GIC）收集来自所有 CPU 的 128 个中断请求并提供接口。前 32 个中断是 CPU 私有的。每个源都可以通过中断启用寄存器启用或禁用。当中断源启用且相应的中断源断言时，中断控制器根据中断类型断言普通或快速中断。

中断控制器只能在超级模式下访问。中断请求按以下顺序排序：快速中断以及相同优先级的普通中断按源编号。所有中断源共有十六个中断级别，零级为最低优先级。中断级别可以通过中断优先级寄存器进行配置。这些寄存器与普通中断掩码寄存器一起支持软件控制的中断优先级。

## 第6 章

![](img/739a35b59067f8a55eff80a58765146f_234_0.png)

`mag3110` 从设备节点将“gpio3 控制器节点”作为其“中断父”，并将“i2c3 控制器节点”作为其“节点父”（mag3110 设备连接到 i2c3 总线）。在 `mag3110` 节点中，GPIO 中断属性有两个字段（第一个是 gpio3 引脚值，第二个值是 Linux/include/dt-bindings/interrupt-controller/irq.h 文件提供的 IRQ 绑定之一），这些字段由 gpio3 控制器节点的 `#interrupt-cells` 属性指定。

“intc 节点”是“gpio3 控制器节点”和“i2c3 控制器节点”的“父级中断控制器节点”。在 gpio3 控制器和 i2c3 控制器的属性中有三个字段，这些字段由 ARM® 通用中断控制器 intc 节点的 `#interrupt-cells` 属性指定。请查看 `Linux/arch/arm/boot/dts` 文件夹下的 `imx6qdl.tsi` 文件中的 i2c3、gpio3 和 intc 节点。

在 i2c3 节点中，`interrupts` 属性的第二个字段为 38。将 CPU 私有的中断数加上 38 得到 70，这与 i2c3 的 hwirq 匹配（参见 IMX6QDRM 第 221 页的表 3.1 ARM® 域中断摘要）。

```
reg = <0x021a8000 0x4000>;
interrupts = <0 38 IRQ TYPE LEVEL HIGH>;
clocks = <clks IMX6QDL_CLK_I2C3>;
status = "disabled";
```

```
gpio3: gpio@020a4000 {
  compatible = "fsl,imx6q-gpio", "fsl,imx35-gpio";
  reg = <0x020a4000 0x4000>;
  interrupts = <0 70 IRQ TYPE LEVEL HIGH>;
  interrupt = <0 71 IRQ TYPE LEVEL HIGH>;
  gpio-controller;
  #gpio-cells = <2>;
  interrupt-controller;
  #interrupt-cells = <2>;
}
```

```
intc: interrupt-controller@800a0100 {
  compatible = "arm,cortex-a9-gic";
  #interrupt-cells = <3>;
  #address-cells = <1>;
  #size-cells = <1>;
  interrupt-controller;
  reg = <0x00a01000 0x1000>;
  <0x00a00100 0x100>;
}
```

在 `imx6qdl-mag3110-sabred.dtsi` 文件中查找 `mag3110` 节点：

```
&i2c3 {
  clock-frequency = <100000>;
  pinctrl-names = "default";
  pinctrl-0 = <&pinctrl_i2c3>;
  status = "okay";
}
```
