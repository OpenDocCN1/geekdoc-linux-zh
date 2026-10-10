# Calibrating Delay...1197.46 BogoMIPS (lpj=2394935)

During boot, the kernel calculates the number of times the processor can execute an internal delay loop in one jiffy, which is the time interval between two consecutive ticks of the system timer. As you would expect, the calculation has to be calibrated to the processing speed of your CPU. The result of this calibration is stored in a kernel variable called loops_per_jiffy. One place where the kernel makes use of loops_per_jiffy is when a device driver desires to delay execution for small durations in the order of microseconds.

To understand the delay-loop calibration code, let’s take a peek inside calibrate_delay(), defined in init/calibrate.c. This function cleverly derives floating-point precision using the integer kernel. The following snippet (with some comments added) shows the initial portion of the function that carves out a coarse value for loops_per_jiffy:

```
loops_per_jiffy = {1 << 12}; /* Initial approximation = 4096 */
printk(KERN_DEBUG "Calibrating delay loop... ");
while ((loops_per_jiffy <<= 1) != 0) {
    ticks = jiffies; /* As you will find out in the section, "Kernel
                      Timers," the jiffies variable contains the
                      number of timer ticks since the kernel
                      started, and is incremented in the timer
                      interrupt handler */
    while (ticks == jiffies); /* Wait until the start
                               of the next jiffy */
    ticks = jiffies;
    /* Delay */
    __delay(loops_per_jiffy);

    /* Did the wait outlast the current jiffy? Continue if
       it didn't */
    ticks = jiffies - ticks;
    if (ticks) break;
}
loops_per_jiffy >>= 1; /* This fixes the most significant bit and is
                       the lower-bound of loops_per_jiffy */
```

The preceding code begins by assuming that loops_per_jiffy is greater than 4096, which translates to a processor speed of roughly one million instructions per second (MIPS). It then waits for a fresh jiffy to start and executes the delay loop, __delay(loops_per_jiffy). If the delay loop outlasts the jiffy, the previous value of loops_per_jiffy (obtained by bitwise right-shifting it by one) fixes its most significant bit (MSB). Otherwise, the function continues by checking whether it will obtain the MSB by bitwise left-shifting loops_per_jiffy. When the kernel thus figures out the MSB of loops_per_jiffy, it works on the lower-order bits and fine-tunes its precision as follows:

```
loopbit = loops_per_jiffy;
/* Gradually work on the lower-order bits */
while (lps_precision-- && (loopbit >>= 1)) {
    loops_per_jiffy |= loopbit;
    ticks = jiffies;
    while (ticks == jiffies); /* Wait until the start
                               of the next jiffy */
    ticks = jiffies;
```