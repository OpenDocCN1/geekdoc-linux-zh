
> 40 #define SPURIOUS_APIC_VECTOR 0xff441 #define ERROR_APIC_VECTOR 0xfe

> 42 #define INVALIDATE_TLB_VECTOR 0xfd

> 43 #define RESCHEDULE_VECTOR 0xfc

> 44 #define FUNCTION_VECTOR 0xfb

> 51 #define LOCAL_TIMER_VECTOR 0xef

> 58 #define FIRST_DEVICE_VECTOR 0x31

> 59 #define FIRST_SYSTEM_VECTOR 0xef

> 62 #define IO_APIC_VECTOR(irq)

> 23 #define FIRST_EXTERNAL_VECTOR 0x20

> 25 #define SYSCALL_VECTOR 0x80

## 12.5.3 预留中断向量

> 图 12.21 来自 `<asm-i86/hw_irq.h>`，显示了若干特殊中断向量的定义。

> 在第 12.6.1.2 节描述了 `setup_irq()` 函数。第二个参数是 `struct irq`，在第 12.5.4 节中初始化。

> `setup_irq()` 函数在第 12.6.1.2 节中描述。第二个参数是 `struct irq`，在第 12.5.4 节中初始化。

## 12.5.4 释放中断

（此处未提供原文内容，故跳过翻译）

# 请求和释放中断线

```
695	printk("Bad boy: %s at 0%%x) called us without a
696	dev_id!\n", devname, (irq)[-1]);
697	#endif
698
699	if (irq >= NR_IRQS)
700		return -EINVAL;
701	if (!handler)
702		return -EINVAL;
703
704	action = (struct irqaction*)
705	kmalloc(sizeof(struct irqaction), GFP_KERNEL)
706	if (!action)
707		return -ENOMEM;
708
709	action->handler = handler;
710	action->flags = irqflags;
711	action->mask = 0;
712	action->name = devname;
713	action->next = NULL;
714	action->dev_id = dev_id;
716
716	retval = setup_irq(irq, action);
717	if (retval)
718		kfree(action);
719		return retval;
720	}
```

**图 12.24** 检查 irq线的请求

**677** `irq` 参数是要分配的中断线编号。

**678** `handler` 参数是一个指向在 irq 发生时调用的函数指针。该函数接受三个参数：irq 号、指向设备标识符的指针以及指向保存的寄存器值的指针。

**679** `request_irq()` 的第三个参数是 `flags`，它指定了该 irq 要求的处理类型。这些标志在第 17.1.3.4 节处理信号时已正式定义。对于当前的上下文，以下信息就足够了。

- `SA_INTERRUPT`：处理程序必须在禁用中断的情况下执行。
- `SA_SHIRQ`：此 irq 是共享的。
- `SA_SAMPLE_RANDOM`：可以使用中断的随机性来保持随机数生成器的随机性。但这会为每个中断的处理增加开销，可以指定该中断是否可用于此。设置时，则可以使用。
- `SA_PROBE`：内核在设置期间探测设备时正在使用此线。

**680** 第四个参数 `devname` 是一个指向设备 ASCII 名称的指针，该设备与此 irq 线关联。

**681** 最后一个参数 `dev_id` 是一个指向标识符的指针，它将在中断发生期间作为第二个参数传递给处理程序。它必须是全局唯一的的。通常使用表示设备的数据结构的地址。

**693-696** 如果中断要共享，那么在请求时必须传入一个非空的 `dev_id` 是至关重要的，否则稍后将无法区分哪个是哪个中断。特别是，它会搞乱中断的释放逻辑。因此，会进行合理性检查。此类请求仍会被接受，但会受到警告（警告）。

**695** 错误消息给出了声称中断的设备名称，以及调用此函数的地址。`(&irq)` 是指向栈上第一个参数的指针。其下 `(&irq)[1]` 是指向栈上返回地址的指针（即调用此函数的下一条指令）。

**699-700** 请求的 irq 线大于最大容量是无效的，因此向调用者返回 `EINVAL`。

**701-702** 必须提供处理程序；否则向调用者返回 `EINVAL`。

**704-705** 这预留了一块足够容纳 `struct irqaction` 的内核内存。

**706-707** 如果无法获取此内存，向调用者返回 `ENOMEM`。

**709-714** 此代码填充了 `struct irqaction` 中的六个字段。除了 `mask` 和 `next` 之外，大部分字段是从输入参数复制的。

**711** `mask` 字段设置为 0，稍后使用。这是结构中一个非常新的字段，用于存储 SMP 亲和性信息。
