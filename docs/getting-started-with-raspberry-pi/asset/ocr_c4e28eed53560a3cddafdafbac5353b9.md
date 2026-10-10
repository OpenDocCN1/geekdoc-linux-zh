Support for high-resolution timers (`CONFIG_HIGH_RES_TIMERS`) has been merged with the 2.6.21 kernel. It makes use of hardware-specific high-speed timers to provide high-precision capabilities to APIs such as `nanosleep()`. On Pentium-class machines, the kernel leverages the TSC to offer this capability.

# Real Time Clock

The RTC tracks absolute time in nonvolatile memory. On x86 PCs, RTC registers constitute the top few locations of a small chunk of battery-powered $ ^{[4]} $ *complementary metal oxide semiconductor* (CMOS) memory. Look at Figure 5.1 in Chapter 5, “Character Drivers,” for the location of the CMOS in the legacy PC architecture. On embedded systems, the RTC might be internal to the processor, or externally connected via the I²C or SPI buses discussed in Chapter 8, “The Inter-Integrated Circuit Protocol.”

$ ^{[4]} $ RTC batteries last for many years and usually outlive the life span of computers, so you should never have to replace them.

You may use the RTC to do the following:

+   - Read and set the absolute clock, and generate interrupts during clock updates.
+   - Generate periodic interrupts with frequencies ranging from 2HZ to 8192HZ.
+   - Set alarms

Many applications need the concept of absolute time or *wall time*. Because `jiffies` is relative to the time when the system booted, it does not contain wall time. The kernel maintains wall time in a variable called `xtime`. During boot, `xtime` is initialized to the current wall time by reading the RTC. When the system halts, the wall time is written back to the RTC. You can use `do_gettimeofday()` to read wall time with the highest resolution supported by the hardware:

```
#include <linux/time.h>
static struct timeval curr_time;
do_gettimeofday(&curr_time);
my_timestamp = cpu_to_le32(curr_time.tv_sec); /* Record timestamp */
```

There are also a bunch of functions available to user-space code to access wall time. They include the following:

+   - `time()`, which returns the calendar time, or the number of seconds since Epoch (00:00:00 on January 1, 1970)
+   - `localtime()`, which returns the calendar time in broken-down format
+   - `mktime()`, which does the reverse of `localtime()`