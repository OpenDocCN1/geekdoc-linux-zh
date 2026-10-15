
```c
 * irq_create_mapping() - 在 hwirq 和 Linux 之间创建映射
 * @domain:  irq_domain
 * @hwirq: 硬件中断号
 * 返回 Linux IRQ 编号或负数错误码
 */
int irq_create_mapping(struct irq_domain *domain, irq_hw_number_t hwirq)
{
    struct device_node *of_node;
    int virq;

    of_node = irq_domain_get_node(domain);

    /* 检查映射是否存在 */
    virq = irq_find_mapping(domain, hwirq);
    if (virq) {
        pr_debug("-> 已存在映射 %d\n", virq);
        return virq;
    }

    /* 分配 Linux IRQ 编号 */
    virq = irq_domain_alloc_descs(-1, 1, hwirq, of_node_to_nid(of_node), NULL);
    if (virq <= 0) {
        pr_debug("-> virq 分配失败\n");
        return q;
    }

    if (irq_domain_associate(domain, virq, hwirq)) {
        irq_free_descs(virq);
        return 0;
    }

    pr_debug("域 %s 上的 irq %lu 映射到虚拟 irq %u\n", of_node_full_name(of_node), hwirq, virq);

    return virq;
}
```

在编写也是控制器的 GPIO 控制器驱动时，可以在 `gpiochip_to_irq` 回调函数内部调用 `irq_create_mapping`。当驱动程序调用 `gpio_chip_to_irq()` 获取与 GPIO 引脚关联的 Linux IRQ 编号时，就会调用此回调。另一种可能性是在 `probe()` 函数中提前对每个 `hwirq` 进行映射，如下代码所示：

```c
for (int j = 0; j < gpiochip->ngpio; j++) {
```

例如，从位于 `drivers/pinctrl/pinctrl-at91-pio4.c` 的 SAMA52 PIO 控制器驱动中提取：

```c
static int atmel_gpio_to_irq(struct gpio_chip *chip, unsigned offset)
{
    struct atmel_pioctrl *atmel_pioctrl = gpiochip_get_data(chip);
}
```

# 第 7 章

## 在设备驱动中处理中断

```c
return irq_find_mapping(atmel_pioctrl->irq_domain, offset);
}
static struct gpio_chip atmel_gpio_chip = {
    .direction_input   = atmel_gpio_direction_input,
    .get               = atmel_gpio_get,
    .direction_output  = atmel_gpio_direction_output,
    .set              = atmel_gpio_set,
    .to_irq           = atmel_gpio_to_irq,
    .base             = 0,
};
```

如果 `hwirq` 尚未存在映射，`irq_create_mapping()` 将分配一个新的 Linux irq，将其与 `hwirq` 关联，并调用 `irq_domain_ops.map()` 函数（通过 `irq_domain_associate()` 回调），驱动程序可以在该函数中执行任何所需的硬件设置。在 `.map()` 中，它创建了 Linux IRQ 和 `hwirq` 之间的映射。映射是在 `.map()` 内部通过调用 `irq_set_chip_and_handler()` 函数完成的。`irq_set_chip_and_handler()` 的第三个参数（handle）返回一个包装函数，该函数将调用使用例如 `request_irq()` 或 `request_threaded_irq()` 注册的硬件处理程序，用于引起中断的“GPIO 设备”。您的 GPIO 设备也可以是一个 GPIO 控制器（例如查看位于 `drivers/pio/` 下的 `gpio-max732x.c` 驱动）。

如果 GPIO 控制器没有实现 `.map()` 函数，则可以在 `probe()` 函数中调用 `irq_set_chip_and_handler()`，正如从 `drivers/pinctrl/pinctrl-at91-pio4.c` 中的 SAMAS5D PIO4 控制器驱动程序中提取的代码所示。GPIO 控制器的每个输入引脚都映射到 GPIO 控制器的 `irq_domain` 中，并提供了一个包装句柄函数 `handle_simple_irq`，该函数将调用从 GPIO 控制器特定输入引脚申领 Linux IRQ 号的每个 GPIO 设备的中断处理程序。

```c
for (i = 0; i < atmel_pioctrl->npins; i++) {
    int irq = irq_create_mapping(atmel_pioctrl->irq_domain, i);

    irq_set_chip_and_handler(irq, &atmel_gpio_chip,
                             handle_simple_irq);
    irq_set_chip_data(irq, atmel_pioctrl);
    dev_dbg(dev,
            "atmel gpio irq domain: hwirq: %d, linux irq: %d\n",
            i, irq);
}
```

## 在设备驱动中处理中断

GPIO irqchips 通常属于以下两类之一：

1. **链式（CHAINED）GPIO irqchips**：这些通常是嵌入在 SoC 上的类型。这意味着 GPIO 有一个快速的 IRQ 处理程序，该处理程序从父中断处理程序（通常是系统中断控制器）以链式方式进入。使用 `irq_set_chained_handler()` 或相应的函数注册 GPIO irqchip，并且 **GPIO irqchip 处理程序** 将保持禁用 IRQ 的情况下，立即从父中断（例如 SAMA5D2 中的高级中断控制器 AIC 或 i.MX7D 家族中的通用中断控制器 GIC）调用。GPIO irqchip 最终会在其中断处理程序中调用类似的内容：

```c
static void atmel_gpio_irq_handler() {
    chained_irq_enter(...);
    generic_handle_irq(...);
    chained_irq_exit(...);
}
```

SoC 控制器驱动调用 `generic_handle_irq()` 来运行每个特定 GPIO 设备驱动程序的处理程序（例如本章加载的第一个驱动，或 `linux/drivers/gpio/` 下的 `gpio-max732c` 驱动）。

在下面的代码中（从 `drivers/pinctrl/at9pio4.c` 提取），你可以看到使用 `irq_set_chained_handler()` 函数创建 SAMA52 GPIO 组处理程序。它将为每个 GPIO 组处理程序创建一个。在每个 `atmel_gpio_irq_handler()` 内部，有一个对包装函数 `generic_handle_irq()` 的调用，它反过来会调用使用 `request_irq()` 函数请求此特定引脚的每个 GPIO 设备驱动的中断处理程序。
