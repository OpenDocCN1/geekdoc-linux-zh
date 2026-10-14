
```c
130 enum mp_irq_source_types {
131     mp_INT = 0,
132     mp_NMI = 1,
133     mp_SMI = 2,
134     mp_ExtINT = 3
135 };
```

图 14.5 中断的类型

131 这是一个向量中断，其向量由 APIC 重定向表提供。

132 这是一个不可掩非中断 (nmi)。在这种情况下，向量信息是不相关的。

133 这是一个系统中断，它会将目标处理器设置为一种特殊的系统管理模式。Linux 不使用这种中断。

134 这同样也是一个向量中断，但其向量由 8259A PIC 提供。

## 14.1.1.6 pirq_entries[] 数组

默认情况下，PCI 总线的 0–7 号中断被分配到 号为 16–23 的 irq 号，但根据需要，它们可以被重定向到 0–15 之间的任意一条 irq 线路。这种重定向记录在 `pirq_entries[]` 数组中；参见图 14.6，来自 `arch/i386/kernel/io_apic.c`。

```c
171 #define MAX_PIQS 8
174 int pirq_entries[MAX_PIQS];
175 int pirq_enabled;
```

图 14.6 重定向外围组件互连 (PCI) 中断

173 只有八个 PCI 中断，编号为 0–7。

174 这个 `int` 类型的数组将 PCI 中断 0–7 映射到 0–15 范围内的 irq 号。

175 如果任何 PCI 中断被重定向，则此标志位会被设置。

## 14.1.2 读取中断配置表

Linux 提供了若干函数用于读取上一节描述的配置表；现在我们来考虑这些函数。

### 14.1.2.1 在 mp_irqs[] 中查找指定的条目

图 14.7 来自 `arch/i386/kernel/io_apic.c`，它展示了在 `mp_irqs[]` 数组中查找与特定 APIC/引脚/类型组合对应条目的函数。该函数遍历整个 `mp_irqs[]` 数组，检查是否存在与 `type`、`apic` 和 `pin` 参数匹配的条目。

## 输入/输出高级可编程中断控制器（即 IO APIC）

```c
215 static int __init_irq_entry(int apic, int pin, int type)
216 {
217   int i;
218
219   for (i=0; i<mp_irq_entries; i++)
220     if (mp_irqs[i].mp_irqtype == type &&
221       (mp_irqs[i].mp_destaptic == mp_ioapics[apic].mp_apic ||
222       mp_irqs[i].mp_destaptic == MP_APIC_ALL &&
223       mp_irqs[i].mp_destirq == pin)
224       return i;
225
226   return -1;
227 }
```

图 14.7 查找给定引脚的 irq（中断请求）

`mp_irq_entries` 变量（第 14.1.1.1 节）包含了 `mp_irqs[]` 数组中的实际条目数量，因此搜索永远不会进入未初始化的数据。

这个相当复杂的测试分解为三个部分，如下：

- `type` 参数必须与 `mp_irqtype` 字段匹配。

- 对 apicer 的测试并不那么简单。apicer 通过其序列号识别 IO APIC（例如 APIC 0、APIC 1 等）。`mp_destaptic` 通过其逻辑 ID 地址识别 APIC，因此在进行比较之前，必须将序列号转换为逻辑 ID。这是通过使用序列号作为索引访问 `mp_ioapics[]` 数组（第 14.1.1.1 节）来找到对应的逻辑 ID 实现的。另一种可能性是条目可能并不直接匹配此 APIC，而是条目可能有一个通配符值，这意味着该 irq 源连接到所有的 APIC。`MP_APIC_ALL` 掩码定义在第 14.1.1.4 节中。

- `pin` 必须与 `mp_destirq` 字段匹配。

- 如果找到匹配项，则返回 `mp_irqs[]` 数组中对应匹配条目的索引。

- 如果搜索了所有条目后未找到匹配项，则返回 `-1` 表示失败。

## 14.1.2.2 将 irq 转换为引脚号

在 14.8 中显示的来自 `arch/i386/kernel/io_apic.c` 的函数查找 ISA 总线上的特定 irq 连接的引脚。它不适用于 PCI 总线。

```c
232 static int __init_find_isa_irq_pin(int irq, int type)
233 {
234   int i;
235
236   for (i=0; i<mp_irq_entries; i++) {
237     int bus = mp_irqs[i].mp_srcbus;
```

```c
238 if((mp_bus_to_type[bus]==MP_BUS_ISA ||
239     mp_bus_to_type[bus]==MP_BUS_EISA ||
240     mp_bus_to_type[bus]==MP_BUS_MCA) &&
241     mp_irqs[i].mp_irqtype==type &&
242     mp_irqs[i].mp_destirq==irq)
243         return i;
244     }
245     return -1;
246 }
```

图 14.8 查找 ISA 总线上的特定 irq 连接的引脚

- 遍历 `mp_irqs[]` 数组直到找到条目。

- 这个 `int` 类型的数组将 PCI 中断 0–7 映射到 0–15 范围内的 irq 号。

- 如果任何 PCI 中断被重定向，则此标志位会被设置。

## 14.1.2.3 将引脚转换为 irq

图 14.9 来自 `arch/i386/kernel/io_apic.c`，返回连接到给定引脚的引脚的 irq 号。

```c
483 static int irq(int idx, int apic, int pin)
484 {
485     int irq, i;
486     int bus = mp_irqs[idx].mp_srcbus;
487
488     switch (mp_bus_to_type[bus]) {
489         case MP_BUS_ISA:
490         case MP_BUS_EISA:
491         case MP_BUS_MCA:
492             irq=mp_irqs[idx].mp_destirq;
493             break;
494         case MP_BUS_PCI:
495             {
496                 i=irq=0;
497                 while (i<apic) {
498                     irq+=mp_ioapics[i++].mp_apic;
499                 }
500                 irq+=pin;
501                 break;
502             }
503         default:
504             {
505                 printk(KERN_ERR "unknown bus type %d.\n", bus);
506                 irq=0;
507                 break;
508             }
509     }
510
511     if ((pin>=16) && (pin<=23)) {
512         if (irq_entries[pin-16] != -1) {
513             if (!irq_entries[pin-16]) {
514                 printk(KERN_DEBUG "disabling IRQ%d\n", pin-16);
515             } else {
516                 irq=irq_entries[pin-16];
517                 printk(KERN_DEBUG "using IRQ%d -> IRQ%d\n",
518                     pin-16, irq);
519             }
520         }
521     return irq;
522 }
```

- 第一个参数是 `mp_irqs[]` 数组的索引，这避免了搜索整个数组的工作。第二个参数指定 APIC，第三个参数是该 APIC 上的引脚。

- 我们通过 `mp_irqs[idx].mp_srcbus` 字段找到连接该 irq 的总线。
