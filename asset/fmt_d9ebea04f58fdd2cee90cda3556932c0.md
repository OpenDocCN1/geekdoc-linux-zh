
# 第 7 章
## 设备驱动程序中的中断处理

中断控制器驱动程序通过调用 `irq_domain_add_*()` 函数之一来分配并注册 `irq_domain`。该函数在成功时将返回一个指向 `irq_domain` 结构的指针。驱动程序必须提供 `irq_domain` 结构作为参数。大多数驱动程序使用线性映射通过 `irq_domain_add_linear()` 映射 IRQ：

```c
/*
 * irq_domain_add_linear() - 分配并注册一个 irq_domain。
 * @of_node: 指向中断控制器的指针。
 * @size: 域中的中断数量。
 * @ops: irq_domain_ops
 * @host_data: 控制器数据 */
struct irq_domain *irq_domain_add_linear(struct device_node *of_node,
	unsigned int size,
	const struct irq_domain_ops *ops,
	void *host_data)
{
    ...
}
```

在大多数情况下，`irq_domain` 是空的。通过调用 `irq_create_mapping()` 填充 `irq_desc` 映射，`irq_create_mapping` 接收 `irq_domain` 和 `hwir`：

```c
unsigned int irq_create_mapping(struct irq_domain *domain,
	irq_hw_number_t hwir)
{
	struct device_node *of_node;
	int virq;
	/* 检查是否存在映射 */
	virq = irq_find_mapping(domain);
	if (virq) {
		pr_debug("-> 已存在映射 %u\n", virq);
		return virq;
	}
	/* 分配 Linux IRQ */
	virq = irq_alloc_desc(domain, hwir);
	if (virq < 0) {
		pr_debug("-> irq 分配失败\n");
		return virq;
	}
	/* 将 desc 与域关联 */
	if (!irq_domain_associate(domain, virq)) {
		irq_free_desc(virq);
		return virq;
	}
	pr_debug("-> 域 %s  irq %u\n", domain->name, virq);
	return virq;
}
```

当编写用于 GPIO 控制器的驱动程序时，`irq_create_mapping()` 可以从 `gpio_to_irq()` 函数调用。当驱动程序调用 `gpio_to_irq()` 获取与 GPIO 关联的 Linux irq 时，该回调函数就会被调用。

如果 `hwir` 尚未映射，则 `irq_create_mapping` 将分配一个新的 `irq_desc`，将其与之关联并调用 `irq_domain_ops.map()` 函数，以便驱动程序执行任何必要的设置。在 `.map()` 函数中，`.map()` 创建了 中中断号与 `hwir` 之间的映射。映射是在 `.map()` 内部通过调用 `irq_set_chip_and_handler()` 完成的。`irq_set_chip_and_handler()` 的第三个参数（handle）决定了用于调用引起“GPIO 设备”驱动程序的中断处理程序（通过 `request_irq()` 或 `request_threaded_irq()` 注册）的封装函数。

GPIO 中断控制器通常使用以下两种函数之一：

- 1. `链式 GPIO 芯片`：这些通常是嵌入在 SoC 中的类型。这意味着对于 GPIO 有一个快速中断处理程序，它会在父中断处理器中被调用，通常是系统中断控制器。GPIO 中断芯片通过调用 `irq_set_chained_handler_and_data()` 向其父中断处理器注册，然后 GPIO 中断处理器（作为参数传递给 `irq_set_chained_handler_and_data()`）将在保持中断关闭的情况下立即从其父中断处理器中调用。随后 GPIO 中断芯片会在中断处理程序中执行以下序列：

```c
static void gpio_irq_handler() {
    chained_irq_enter(...);
    generic_handle_irq(...);
    chained_irq_exit(...);
}
```

```c
struct gpio_irq_chip *irq;
...
irq = &pc->gpio_chip;
irq->irq = &bcm2835_gpio_irq_chip;
irq->parent_handler = bcm2835_gpio_irq_handler;
irq->num_parents = BCM2835_NUM_IRQS;
irq->parents = devm_calloc(dev,
                                                           sizeof(*irq->parents),
                                                           GFP_KERNEL);
if (irq->parents)
    return -ENOMEM;
/*
 * 为所有组使用该处理器：这是必要的，
 * 因为我们使用一个 gpiochip 来覆盖所有线路 - 
 * irq 处理程序需要确定是哪个组和
 * （bank）触发了 IRQ，并查找每个组和
 * 的数据。
 */
for (i = 0; i < BCM2835_NUM_IRQS; i++) {
    irq->parents[i] = irq_parse_and_map(np, i);
    irq->default_type = IRQ_TYPE_NONE;
    irq->handler = handle_level_irq;
```

```c
err = gpiochip_add_data(&pc->gpio_chip, pc);
if (err) {
    dev_err(dev, "could not add GPIO chip\n");
    return err;
}
```

`gpiochip_add_data()` 函数会调用 `gpiochip_add_irqchip()`，后者会调用 `irq_set_chained_handler_and_data()`，该函数为给定的 IRQ 设置处理器和数据。见下方从 `gpiochip_add_irqchip()` 函数中提取的代码片段：

```c
if (gpiochip->irq.parent_handler) {
    void *data = gpiochip->irq.parent_handler_data ?: gpiochip;
    for (i = 0; i < gpiochip->irq.num_parents; i++) {
        /*
         * 父 IRQ 芯片已经在使用该 IRQ 芯片的
         * 数据数据，因此我们的回调直接使用
         * handler_data。
        */
        irq_set_chained_handler_and_data(gpiochip->irq.parents[i],
                                          gpiochip->irq.parent_handler,
                                          data);
    }
}
```

`gpiochip_add_irqchip()` 函数还会调用 `irq_domain_add_simple()`，它会注册一个 `irq_domain` 结构并映射范围 IRQ。

## 设备驱动程序中的中断处理

每个 GPIO 组（bank）中断都有一个父处理器。在 `bcm2835_gpio_irq_handler()` 函数中，有对 `bcm2835_gpio_irq_handle_bank()` 的调用，后者又调用 `generic_handle_irq()`。通用封装函数将调用每个使用 `request_irq()` 函数请求 GPIO 中断的 GPIO 驱动程序的中断处理器。`generic_handle_irq()` 函数的参数是 Linux IRQ ，它是通过 `irq_linear_revmap` 函数从一个字中获取的。

```c
```
