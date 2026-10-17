
```c
static void bcm2835_gpio_irq_handler(struct irq_desc *desc)
{
    struct gpio_chip *chip = irq_desc_get_handler(desc);
    bcm2835_pinctrl *pc = gpichip_get_data(chip);
    struct irq_chip *host_chip = irq_desc_get_chip(desc);
    int irq = irq_desc_get_irq(desc);
    int group;

    for (int i = 0; i < BCM2835_NUM_IRQS; i++) {
        if (chip->irq.parents[i] == irq) {
            group = i;
            break;
        }
    }
    /* 这不应该发生，每个 IRQ 都有一个 bank * */
    if (i == BCM2835_NUM_IRQS)
        BUG();
}
chained_irq_enter(host_chip, desc);
switch (group) {
    case 0: /* IRQ0 覆盖 GPIO 0-27 */
        bcm2835_gpio_irq_handle_bank(pc, 0, 0xffffff);
        break;
    case 1: /* IRQ1 覆盖 GPIO 28-45 */
        bcm2835_gpio_irq_handle_bank(pc, 0, 0xf0000000);
        bcm2835_gpio_irq_handle_bank(pc, 1, 0x00003ffff);
        break;
    case 2: /* IRQ2 覆盖 GPIO 46-63 */
        bcm2835_gpio_irq_handle_bank(pc, 1, 0x003fc000);
        break;
}

chained_irq_exit(host_chip, desc);
```

```c
static void bcm2835_gpio_bank(struct bcm2835_pinctrl *pc, int bank, u32 mask)
{
    unsigned long events;
    unsigned offset;
    unsigned gpio;

    events = bcm2835_gpio_read(pc, bank * 32);
    events &= mask;
    while (events) {
        offset = __ffs(events);
        generic_handle_irq(pc->gpio_chip);
        events &= ~(1 << offset);
    }
```

- 通用（GENERIC）GPIO irqchips：这些与链式 GPIO irqchips 相同，但不使用链式中断。相反，GPIO 分发由通用 IRQ 处理程序通过 `request_irq()` 执行。GPIO 将在其中断处理程序调用如下内容：

```c
static irqreturn_t foo_gpio_irq(int irq, void *data)
    generic_handle_irq(...);
```

嵌套线程（NESTED THREADED）GPIO irqchips：这些是扩展器以及任何位于总线上的其他 GPIO。当然，此类需要读取 GPIO 状态的驱动可能会触发其他中断，需要产生线程并屏蔽父级中断直到中断被处理。相反，此类驱动的特征是在其中断处理程序调用如下内容：

```c
static irqreturn_t foo_gpio_irq(int irq, void *data)
    handle_nested_irq();
```

在本书的 7.4 节中，将实现扩展 GPIO。

## GPIO 描述符接口

本节描述基于描述符的 GPIO 接口。对于已弃的整数 GPIO 接口，请参考 `Documentation/gpio/`。所有适用于基于描述符 GPIO 的函数都带有 `gpiod_` 前缀。`gpiod_` 前缀用于旧接口。内核中的其他函数不应使用。强烈不要使用旧函数，新代码应仅使用 `<linux/gpio/consumer.h>` 和描述符。

### 获取 GPIO

GPIO 描述符通过使用 `devm_gpio_get()` 函数返回的 `gpio_desc` 结构体识别每个 GPIO。该函数取参数为 GPIO 消费者 `dev`、GPIO 消费者 `con_id` 和可选的初始化标志 `flags`：

```c
struct gpio_desc *devm_gpio_get(struct device *dev, const char *con_id, enum gpio_flags flags);
```

`devm_gpio_get()` 函数的变体 `devm_gpio_get_index()` 允许访问函数内部的多个 GPIO。`devm_gpio_get_index()` 通过 Device Tree 查找 GPIO `con_id` 其索引 `idx` 返回描述符：

```c
struct gpio_desc *devm_gpio_get_index(struct device *dev, const char *con_id, unsigned int idx, enum gpio_flags flags);
```

`flags` 参数可以指定 GPIO 的方向和初始值。是一些重要值：

- `GPIOD_ASIS` 或 0 不初始化 GPIO。必须稍后用专用函数设置。
- `GPIOD_IN` 将 GPIO 初始化为输入。
- `GPIOD_OUT_LOW` 将 GPIO 初始化为值为 0 的输出。
- `GPIOD_OUT_HIGH` 将 GPIO 初始化为值为 1 的输出。

可以使用 `devm_gpiod_put()` 函数释放 GPIO 描述符。

### 使用 GPIO

每当你编写需要控制 GPIO 的 Linux 驱动时，必须指定 GPIO 方向。这可以通过 `devm_gpio_get*()` 函数的标志参数完成，如果你将标志参数设置为 `GPIOD_ASIS`，则稍后调用 `gpiod_direction_*()` 函数：

```c
int gpiod_direction_input(struct gpio_desc *desc);
int gpiod_direction_output(struct gpio_desc *desc, int value);
```

返回零表示成功，否则返回负 `errno`。对于输出 GPIO，提供的值成为初始输出值。这有助于避免系统启动期间的信号抖（glitching）。

大多数 GPIO 控制器可以通过内存读/写指令访问。它们不需要睡眠，并且可以在硬（非线程）中断处理程序内部安全地执行。

你可以使用以下函数从原子上下文中访问 GPIO：

```c
int gpiod_set_value(struct gpio_desc *desc);
void gpiod_set_value(struct gpio_desc *desc, int value);
```

由于驱动不应该关心物理电平，所有 `gpiod_set_xxx()` 函数都与*逻辑*值操作。这意味着它们会检查 GPIO 是否配置为低电平有效，如果是，它们会在驱动物理电平之前操作该值。

总结示例：

| 函数 | 物理引脚 |
|---|---|
| `gpiod_set_value(desc, 0);` | 低电平有效 (高电平有效) | 低 |
| `gpiod_set_value(desc, 1);` | 默认 (高电平有效) | 高 |
| `gpiod_set_value(desc, 1);` | 低电平有效 | 高 |
| `gpiod_set_value(desc, 1);` | 低电平有效 | 低 |

### 映射到 IRQ 的 GPIO

中断可以通过 GPIO 发生。通过以下函数获取给定 GPIO 对应的 Linux IRQ：

```c
int gpiod_to_irq(const struct gpio_desc *desc);
```

你将传递之前使用 `devm_gpiod_get*` 获取的 GPIO，`gpiod_to_irq()` 将返回该 GPIO 对应的 Linux IRQ，如果无法映射则返回负 `errno`。`gpiod_to_irq()` 函数不允许睡眠。

## 平台驱动程序

# 第 5 章

## 设备树中的 GPIO

GPIO 被映射到设备树中的设备和功能。具体的实现方法取决于提供 GPIO 的 GPIO 控制器（请参阅你控制器的设备树绑定文件）。
