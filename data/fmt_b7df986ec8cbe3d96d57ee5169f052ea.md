
# 输入/输出高级可编程中断控制器（IO APIC）

```
1191 static unsigned int start_edge_ioapic_irq(unsigned int irq)
1192 {
1193    int was_pending = 0;
1194    unsigned long flags;
1195
1196    spin_lock_irqsave(&ioapic_lock, flags);
1197    if (irq < 16) {
1198          disable_8259A_irq(irq);
1199      if (8259A_irq_pending(irq))
1200          was_pending = 1;
1201  }
1202      __unmask_IO_APIC_irq(irq);
1203      spin_unlock_restore(&ioapic_lock, flags);
1204
1205      return was_pending;
1206  }
1207
1208 #define shutdown_edge_ioapic_irq
```

**图 14.31** IO APIC 启动边沿触发中断

1191 对于边沿触发中断，只有状态的变化标记中断的发生。无法从`irq`的状态判断是否有中断，因此在启动时需要检查中断是否已断言。返回的整数表示此：1 表示挂起，0 表示未挂起。

1193 这个返回给调用者的局部变量初始化为默认值“未挂起”。

1196–1203 因为 IO APIC 是共享资源，这些行形成了临界区。锁在第 14.2.2.1 节中定义并初始化。中断安全的自旋锁宏来自第 14.2.8 节。

1197–1201 这些代码仅当涉及的`irq`是前16个之一时执行。

1198 因为此`irq`将在 APIC 上启动，首先使用 PIC 函数在 8259A 上将其禁用（见第 12.7.6 节）。这为了避免任何可能的竞争。

1199–1200 如果 PIC 记录到该`irq`有挂起中断，则记录并返回该信息。测试函数在第 12.7.9 节中描述。

1202 此行始终执行。它是通用的 IO APIC 代码，与`irq`的触发方式无关。

1205 如果`irq`有挂起中断，则返回值为 1；否则（无挂起中断，或不是16个之一），返回值为 0。

1208 `shutdown`是简单易见的，因为它被别名为`disable`（实际上什么都不做）；见第 14.3.1.3 节。

## 14.3.1.3 启用和禁用

实现 IO APIC 上启用和禁用边沿触发中断的简单代码如图 14.3.2 所示，来自`arch/i386/kernel/io_apic.c`。

```
1177 #define enable_edge_ioapic_irq unmask_IO_APIC_irq
1178
1179 static void disable_edge_ioapic_irq (unsigned int irq) {
```

**图 14.32** 在 APIC 上启用和禁用边沿触发`irq`（中断请求）

此别名于`unmask_IO_APIC_irq`，后者与触发无关（见第 14.4 节）。

`disable`函数什么都不做。

## 14.3.1.4 确认和结束

`acknowledge()`和`end()`的代码如图 14.33 所示，来自`arch/i386/kernel/io_apic.c`。

```
1175 static void ack_edge_ioapic_irq(unsigned int irq)
1176 {
1177     if ((irq_desc[irq].status & (IRQ_PENDING | IRQ_DISABLED)
1178         == (IRQ_PENDING | IRQ_DISABLED))
1179             mask_IO_APIC_irq(irq);
1180     ack_APIC_irq(irq);
1181 }
1182
1183 static void end_edge_ioapic_irq(unsigned int i) {}
```

图 14.33 IO APIC 确认和结束边沿触发`irq`

条件是`IRQ_PENDING`和`IRQ_DISABLED`位都设置为真。在这种情况下，应使用触发无关的函数`mask_IO_APIC_irq()`将其标记。这防止了未处理设备的中断风暴。

在所有情况下，都会调用本地 APIC 函数`ack_APIC_irq()`来发送 EOI（见第 13.2.4 节）。

边沿触发`irq`的处理程序结束后，不需要通知 IO APIC，因此该函数什么都不做。

## 14.3.2 IO APIC 上的电平触发中断

电平触发中断很特殊，因为在处理它们时没有触碰 IO APIC 寄存器。确认是在处理器中进行的，而不是在启动处理器中。对相同中断的重入保护仍然由通用`irq`层以及未确认本地 APIC 不接受中断这一点提供。

### 14.3.2.1 电平触发中断的控制器函数

还有一个用于具有电平触发中断的 IO APIC 声明并使用的`hw_interrupt_type`结构体，如图 14.34 所示，来自`arch/i386/kernel/io_apic.c`。

```
1345 static struct hw_interrupt_type ioapic_level_irq_type =
1346   "IO-APIC-level",
1347   startup_level_ioapic_irq,
1348   shutdown_level_ioapic_irq,
1349   enable_level_ioapic_irq,
1350   disable_level_ioapic_irq,
1351   mask_and_ack_level_ioapic_irq,
1352   end_level_ioapic_irq,
1353   set_ioapic_affinity;
1354 };
```

**图 14.34** 电平触发中断的控制器函数

**1353** 注意，图 14.34 中的最后一个函数并不是特定用于电平触发 APIC 的：它是通用的`set_ioapic_affinity()`函数（见第 14.4.4 节）。

### 14.3.2.2 操作电平触发 APIC

启动、关闭、启用和禁用电平触发 IO APIC 的函数实现见图 14.35，源自`arch/i386/kernel/io_apic.c`。

```
1200 unsigned int startup_level_ioapic_irq(unsigned int irq)
1201 {
1202   unmask_IO_APIC_irq(irq);
1203
1204   return 0;
1205 }
1206
1207 #define shutdown_level_ioapic_irq   mask_IO_APIC_irq
1208 #define enable_level_ioapic_irq   unmask_IO_APIC_irq
1209 #define disable_level_ioapic_irq   mask_IO_APIC_irq
```

**图 14.35** 操作电平触发 APIC

**1202** 启动函数被别名为与触发无关的`unmask_IO_APIC_irq()`（见第 14.4.1 节）。

**1204** 我们始终返回 0，一个“未挂起”的值。

**1207–1209** 这三个函数也别名为相应的与触发无关的函数（见第 14.4.1 节）。

### 14.3.2.3 结束电平触发的`irq`

本应该是相对简单的函数由于一个解决某些 IO APIC 硬件问题的补丁而变得复杂。在某些条件下，电平触发中断会以边触发的形式递送，并设置相应的的中断请求（IRR）位。因此 APIC 期望一个 EOI，但它永远不会到达，从而导致死锁。解决此问题的函数见图 14.36，源自`arch/i386/kernel/io_apic.c`。
