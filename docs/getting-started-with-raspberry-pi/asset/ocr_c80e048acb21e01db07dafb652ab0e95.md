![](bbox=[0.2, 0.06, 0.9, 0.56])

The driver has to first request the IRQ and associate an interrupt handler with it:

```
```c
#define ROLLER_IRQ  7
static irqreturn_t roller_interrupt(int irq, void *dev_id);

if (request_irq(ROLLER_IRQ, roller_interrupt, IRQF_DISABLED |
        IRQF_TRIGGER_RISING, "roll", NULL)) {
    printk(KERN_ERR "Roll: Can't register IRQ %d\n", ROLLER_IRQ);
    return -EIO;
}
```
```

Let's look at the arguments passed to request_irq(). The IRQ number is not queried or probed but hard-coded to ROLLER_IRQ in this simple case as per the hardware connection. The second argument, roller_interrupt(), is the interrupt handler routine. Its prototype specifies a return type of irqreturn_t, which can be IRQ_HANDLED if the interrupt is handled successfully or IRQ_NONE if it isn't. The return value assumes more significance for I/O technologies such as PCI, where multiple devices can share the same IRQ.

The IRQF_DISABLED flag specifies that this interrupt handler has to be treated as a fast handler, so the kernel