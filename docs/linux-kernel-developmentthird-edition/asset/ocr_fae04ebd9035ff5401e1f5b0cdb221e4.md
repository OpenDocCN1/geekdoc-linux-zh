# Status of the Interrupt System

It is often useful to know the state of the interrupt system (for example, whether interrupts are enabled or disabled) or whether you are currently executing in interrupt context. The macro `irqs_disabled()`, defined in `<asm/system.h>`, returns nonzero if the interrupt system on the local processor is disabled. Otherwise, it returns zero. Two macros, defined in `<linux/hardirq.h>`, provide an interface to check the kernel's current context. They are
`in_interrupt()`
`in_irq()`

The most useful is the first: It returns nonzero if the kernel is performing any type of interrupt handling. This includes either executing an interrupt handler or a bottom half handler. The macro `in_irq()` returns nonzero only if the kernel is specifically executing an interrupt handler.

More often, you want to check whether you are in process context. That is, you want to ensure you are not in interrupt context. This is often the case because code wants to do something that can only be done from process context, such as `sleep.` If `in_interrupt()` returns zero, the kernel is in process context.

Yes, the names are confusing and do little to impart their meaning. Table 7.2 is a summary of the interrupt control methods and their description.

| Function | Description |
|---|---|
| `local_irq_disable()` | Disables local interrupt delivery |
| `local_irq_enable()` | Enables local interrupt delivery |
| `local_irq_save()` | Saves the current state of local interrupt delivery and then disables it |
| `local_irq_restore()` | Restores local interrupt delivery to the given state |
| `disable_irq()` | Disables the given interrupt line and ensures no handler on the line is executing before returning |
| `disable_irq_nosync()` | Disables the given interrupt line |
| `enable_irq()` | Enables the given interrupt line |
| `irqs_disabled()` | Returns nonzero if local interrupt delivery is disabled; otherwise returns zero |
| `in_interrupt()` | Returns nonzero if in interrupt context and zero if in process context |
| `in_irq()` | Returns nonzero if currently executing an interrupt handler and zero otherwise |