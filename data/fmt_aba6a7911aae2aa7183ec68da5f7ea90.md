
## 12.7.6 禁用

在 PIC 上禁用特定 irq 的函数如图 12.37 所示，来自 `arch/i386/kernel/8259.c`。

```c
185 void disable_8259A_irq(unsigned int irq)
186 {
187     unsigned int mask=1<<irq;
188     unsigned long flags;
189
190     spin_lock_irqsave(&i8259A_lock, flags);
191     cached_irq_mask|=mask;
192     if (irq&8)
193     outb(cached_A1,0xA1);
194     else
195     outb(cached_21,0x21);
196 spin_unlock_irqrestore(&i8259A_lock, flags);
197 }
```

**图 12.37** 禁用一条特定的 irq 线

187 设置 `mask` 中对应于 `irq` 编号的位。所有其他位均清零。

190 此时 `EFLAGS` 的值被保存在本地变量 `flags` 中，并在释放自旋锁时恢复（宏的定义请参见第 12.8 节）。

191 在 `cached_irq_mask` 中设置相应的位，而不影响任何其他位。位被置位意味着对应的 irq 线被禁用。

192–195 这些与图 12.36 中的 206–209 行相同，注释也同样适用。

## 12.7.7 确认

在 i386 架构中既有硬件确认周期也有软件确认周期。CPU 会自动处理硬件确认；这不属于系统的考虑范围。PIC 可以被设置为非自动 EOI（中断结束）模式。在这种情况下，PIC 在接收到来自 CPU 的硬件确认后，在收到软件的正式确认（确认这样做是安全的）之前，不能发送任何后续中断。

本节分为两个部分。首先是直接的确认，在第 12.7.7.1 节中介绍。然而，在少数情况下，如果软件检测到中断是伪中断（例如来自一条未使用的 irq 线），那么它必须进一步询问 PIC 以试图弄发生了什么。这在第 12.7.7.2 节中处理。

### 12.7.7.1 确认可编程中断控制器的中断接收

图 12.38 中的代码来自 `arch/i386/kernel/i8259.c`，显示了实际向 8259A 确认已接收并正在处理中断的函数。代码名称警告 8259A 是一个脆弱的野兽；它几乎必须按照这种方式执行（先掩码它，*然后*发送 EOL，且向两个 8259A 发送 EO 的顺序非常重要）。

```c
266 void mask_and_ack_8259A(unsigned int irq)
267 {
268 unsigned int irqmask = 1 << irq;
269 unsigned long flags;
270
271 spin_lock_irqsave(&i8259A_lock, flags);
287 if (cached_irq_mask & irqmask)
288 goto spurious_8259
289 cached_irq_mask |= irqmask;
290
handle_real_irq:
291 if (irq&8) {
292     outb(cached_A1,0xA1);
293     outb(cached_A1,0xA1);
294     outb(cached_A1,0xA1);
295 }
296 } else {
297     outb(cached_21,0x21);
298     outb(cached_21,0x21);
299     outb(cached_21,0x21);
300 }
301 spin_unlock_irqrestore(&i8259A_lock, flags);
302 return;
303 spurious_8259:
304 if (cached_irq_mask & irqmask) {
305     printf("spurious interrupt on %d\n", irq);
306     cached_irq_mask &= irqmask;
307 }
308 spin_unlock_irqrestore(&i8259A_lock, flags);
309 return;
311 }
```

*(注：由于原文提供的代码块存在严重的逻辑混乱和重复错误，翻译时严格遵循“不翻译代码块”原则，保留其原样。)*

图 12.38 向可编程中断控制器确认中断接收

来自 `arch/i386/kernel/i8259.c` 的代码显示了实际向 8259A 确认已接收并正在处理中断的函数。代码名称警告 8259A 是一个脆弱的野兽；它几乎必须按照这种方式执行（先掩码它，*然后*发送 EOL，且向两个 8259A 发送 EO 的顺序非常重要）。

（此处代码块内容由于原文混乱，已按要求不翻译）

# 8259A 可编程中断控制器

316–333 在此处，该 irq 已被确定为伪假中断（spurious）。这是真实的伪假中断处理范围。这种伪假中断通常是硬件问题的征象，因此有很多工作需要完成。我们报告它，然后返回并对其进行确认。

317 该静态掩码在函数调用与调用之间保持。它记录了之前被报告为伪假中断的 irqs。

322 如果静态 `spurious_irq_mask` 中没有设置与正在处理的 irq 对应的位（`irqmask`），则会打印消息，因此每个伪假的 irq 都会在它第一次发生时被报告。

324 设置静态掩码中的该位，使其不会再次被报告。

326 该变量在第 4.5.1.1 节中声明。它跟踪自系统启动以来累计的伪假中断总数。它只在 `get_irq_list()` 函数中读取，该函数供 `/proc` 文件系统使用。

332 从理论上讲，这个 irq 并不需要处理，在 Linux 中这不会引起问题，那么我们为什么不这样做这样做呢？此外，在退出时会释放自旋锁（spinlock）。

## 12.7.7.2 判断中断是否正在被服务

图 12.39 所示的函数查询 PIC 以确定指定的 irq 是否正在被服务。它会在 8259A 内部寄存器之间切换，这缓慢。此函数期望调用者已持有中断控制器自旋锁。

```
static inline int int8259A_irq_real(unsigned int irq)
{
    int value;
    int irqmask = 1<<irq;

    if (irq < 8) {
        outb(0x0B,0x20);
        value = inb(0x20) & irqmask;
        outb(0x0A,0x20);
        return value;
    }
    outb(0x0B,0xA0);
    value = inb(0xA0) & (irqmask >> 8);
    outb(0x0A,0xA0);
    return value;
}
```

> 图 12.39 判断中断是否正在被服务

246 这创建了一个掩码，其中唯一设置的位是与正在检查的 irq 对应的位。

246–252 如果 irq 节点小于 8，则它在主 PIC 上。

这向中断控制寄存器写入 `0000 1011`。第 3 位指定了该字节的格式为操作控制字 3（operation control word 3）。该控制字指定了下次从中断控制寄存器读取将返回哪个内部寄存器。该寄存器由位 0 和位 1 指定。值 11 表示将来从此端口读取将返回服务寄存器（ISR）中的值。该寄存器中设置的位指定当前正在被服务的 irqs。

这从 ISR 读取并屏蔽掉目标位以外的其他所有位。此之后，如果 irq 正在被服务，则 `value` 为 1；否则为 0，无论其他哪些 irqs 正在被服务。

这向端口 `0x20` 写入 `0000 1010`。此更改将未来的读取切换回中断请求寄存器（IRR）。这是默认设置。

如果此 irq 正在被服务，则返回 TRUE；否则返回 FALSE。

如果所说的 irq 属于从 PIC，则执行此代码。

这向从 PIC 的内部控制寄存器写入以更改下次读取的源。

这从 ISR 读取并与此 irq 对应的位进行屏蔽（移到低字节位置）。如果对应此 irq 的位被设置，则值为 1，否则为 0。

这向端口 `0xA0` 写入 `0000 1010`。此更改将未来的读取指向 IRR 寄存器。

如果此 irq 正在被服务，则返回 TRUE；否则 FALSE。

## 12.7 结束

图 12.40 所示的代码来自 `arch/i386/kernel/i829.c` 显示了中断处理后调用的函数。它允许该 irq 再次发生。

```
static void end_8259A_irq (unsigned int irq)
{
    if ((irq_desc[irq].status & (IRQ_DISABLED|IRQ_INPROGRESS))
        enable_8259A_irq(irq);
}
```

> 图 12.40 中断处理完成
