from it and `wake_up/wake_up_interruptible()` to wake up when needed.

An example of the first usage of waitqueues is interaction between the page allocator (in mm/page_alloc.c; `__alloc_pages()`) and the kswapd kernel daemon (in mm/vmscan.c; kswap()), by means of wait queue kswapd_wait, declared in mm/vmscan.c; the kswapd daemon sleeps on this queue, and it is woken up whenever the page allocator needs to free up some pages.

An example of autonomous waitqueue usage is interaction between user process requesting data via `read(2)` system call and kernel running in the interrupt context to supply the data. An interrupt handler might look like (simplified `drivers/char/rtc_interrupt()`):

```
static DECLARE_WAIT_QUEUE_HEAD(rtc_wait);
void rtc_interrupt(int irq, void *dev_id, struct pt_regs *regs)
{
spin_lock(&rtc_lock);
rtc_irq_data = CMOS_READ(RTC_INTR_FLAGS);
spin_unlock(&rtc_lock);
wake_up_interruptible(&rtc_wait);
}
```

So, the interrupt handler obtains the data by reading from some device-specific I/O port (CMOS_READ() macro turns into a couple outb/inb) and then wakes up whoever is sleeping on the `rtc_wait` wait queue.

Now, the `read(2)` system call could be implemented as:

```
ssize_t rtc_read(struct file file, char *buf, size_t count, off_t *ppos)
{
DECLARE_WAITQUEUE(wait, current);
unsigned long data;
ssize_t retval;
add_wait_queue(&rtc_wait, &wait);
current->state = TASK_INTERRUPTIBLE;
do {
spin_lock_irq(&rtc_lock);
data = rtc_irq_data;
rtc_irq_data = 0;
spin_unlock_irq(&rtc_lock);

if (data != 0)
break;

if (file->f_flags & O_NONBLOCK) {
retval = -EAGAIN;
goto out;
}
if (signal_pending(current)) {
retval = -ERESTARTSYS;
goto out;
}
schedule();
```