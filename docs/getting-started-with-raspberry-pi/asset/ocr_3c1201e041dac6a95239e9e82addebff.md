```
Code View:
```
struct roller_device_struct { /* Device-specific structure */
/* ... */
struct tasklet_struct tskit;
/* ... */
}

void __init roller_init()
{
struct roller_device_struct *dev_struct;
/* ... */

/* Initialize tasklet */
tasklet_init(&dev_struct->tskit, roller_analyze, dev);
}

/* The bottom half */
void
roller_analyze()
{
/* Analyze the waveforms and switch to
polled mode if required */
}

/* The interrupt handler */
static irqreturn_t
roller_interrupt(int irq, void *dev_id)
{
struct roller_device_struct *dev_struct;

/* Capture the wave stream */
roller_capture();

/* Mark tasklet as pending */
tasklet_schedule(&dev_struct->tskit);

return IRQ_HANDLED;
}
```
```

`tasklet_init()` dynamically initializes a tasklet. The function does not allocate memory for a `tasklet_struct`, rather you have to pass the address of an allocated one. `tasklet_schedule()` announces that the corresponding tasklet is pending execution. Like for interrupts, the kernel offers a bunch of functions to control the execution state of tasklets on systems having multiple processors:

+   - `tasklet_enable()` enables tasklets.

+   - `tasklet_disable()` disables tasklets and waits until any currently executing tasklet instance has exited.

+   - `tasklet_disable_nosync()` has semantics similar to `disable_irq_nosync()`. The function does not wait for active instances of the tasklet to finish execution.