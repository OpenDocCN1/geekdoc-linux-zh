
In operating systems, especially Unix, a jiffy is the time between two successive clock ticks. Historically, this has been 10ms. As we have seen in this chapter, however, a jiffy in Linux can have various values.

The `jiffies` variable is declared in `<linux/jiffies.h>` as:

```c
extern unsigned long volatile jiffies;
```

In the next section, we look at its actual definition, which is a bit peculiar. For now, let's look at some sample kernel code. The following expression converts from seconds to a unit of `jiffies`:

`(seconds * HZ)`

Likewise, this expression converts from `jiffies` to seconds:

`(jiffies / HZ)`

The former, converting from seconds to ticks, is more common. For example, code often needs to set a value for some time in the future, for example:

```c
unsigned long time_stamp = jiffies;      /* now */
unsigned long next_tick = jiffies + 1;   /* one tick from now */
unsigned long later = jiffies + 5*HZ;    /* five seconds from now */
unsigned long fraction = jiffies + HZ / 10; /* a tenth of a second from now */
```

Converting from ticks to seconds is primarily reserved for communicating with user-space, as the kernel itself rarely cares about any sort of absolute time.

Note that the `jiffies` variable is prototyped as `unsigned long` and that storing it in anything else is incorrect.

### Internal Representation of Jiffies

The `jiffies` variable has always been an `unsigned long`, and therefore 32 bits in size on 32-bit architectures and 64-bits on 64-bit architectures. With a tick rate of 100, a 32-bit `jiffies` variable would overflow in about 497 days. With `HZ` increased to 1000, however, that overflow now occurs in just 49.7 days. If `jiffies` were stored in a 64-bit variable on all architectures, then for any reasonable `HZ` value the `jiffies` variable would never overflow in anyone's lifetime.

For performance and historical reasons—mainly compatibility with existing kernel code—the kernel developers wanted to keep `jiffies` an `unsigned long`. Some smart. When done, if the whole ordeal took longer than the timeout, the code handles the error as appropriate.

Multiple potential overflow issues are here, but let’s study one of them: Consider what happens if jiffies wrapped back to zero after setting timeout. Then the first conditional would fail because the jiffies value would be smaller than timeout despite logically being larger. Conceptually, the jiffies value should be a large number—larger than timeout. Because it overflowed its maximum value, however, it is now a small value—perhaps only a handful of ticks over zero. Because of the wraparound, the results of the if statement are switched. Whoops!

Thankfully, the kernel provides four macros for comparing tick counts that correctly handle wraparound in the tick count. They are in `<linux/jiffies.h>`. Listed here are simplified versions of the macros:

```c
#define time_after(unknown, known)  ((long)(known) - (long)(unknown) < 0)
#define time_before(unknown, known)  ((long)(unknown) - (long)(known) < 0)
#define time_after_eq(unknown, known)  ((long)(unknown) - (long)(known) >= 0)
#define time_before_eq(unknown, known)  ((long)(known) - (long)(unknown) >= 0)
```

The unknown parameter is typically jiffies and the known parameter is the value against which you want to compare.

The `time_after(unknown, known)` macro returns true if time unknown is after time known; otherwise, it returns false. The `time_before(unknown, known)` macro returns true if time unknown is before time known; otherwise, it returns false. The final two macros perform identically to the first two, except they also return true if the parameters are equal.

The timer-wraparound-safe version of the previous example would look like this:

```c
unsigned long timeout = jiffies + HZ/2;  /* timeout in 0.5s */

/* ... */
if (time_before(jiffies, timeout)) {
    /* we did not time out, good ... */
} else {
    /* we timed out, error ... */
}
```

If you are curious as to why these macros prevent errors because of wraparound, try various values for the two parameters. Then assume one parameter wrapped to zero and see what happens.

## User-Space and HZ

In kernels earlier than 2.6, changing the value of HZ resulted in user-space anomalies. This happened because values were exported to user-space in units of ticks-per-second. As these interfaces became permanent, applications grew to rely on a specific value of HZ. Consequently, changing HZ would scale various exported values by some constant—without user-space knowing! Uptime would read 20 hours when it was in fact two!

To prevent such problems, the kernel needs to scale all exported jiffies values. It does this by defining `USER_HZ`, which is the HZ value that user-space expects. On x86, because HZ was historically 100, `USER_HZ` is 100. The function `jiffies_to_clock_t()`, defined in `kernel/time.c`, is then used to scale a tick count in terms of HZ to a tick count in terms of `USER_HZ`. The expression used depends on whether `USER_HZ` and HZ are integer multiples of themselves and whether `USER_HZ` is less than or equal to HZ. If both those conditions are true, and for most systems they usually are, the expression is rather simple:

```c
return x * (HZ / USER_HZ);
```

A more complicated algorithm is used if the values are not integer multiples.

Finally, the function `jiffies_64_to_clock_t()` is provided to convert a 64-bit jiffies value from HZ to `USER_HZ` units.

These functions are used anywhere a value in ticks-per-second needs to be exported to user-space. Following is an example:

```c
unsigned long start;
unsigned long total_time;

start = jiffies;
/* do some work ... */
total_time = jiffies - start;
printf("That took %lu ticks\n", jiffies_to_clock_t(total_time));
```

User-space expects the previous value as if HZ=`USER_HZ`. If they are not equivalent, the macro scales as needed and everyone is happy. Of course, this example is silly: It would make more sense to print the message in seconds, not ticks. For example:

```c
printf("That took %lu seconds\n", total_time / HZ);
```

## Hardware Clocks and Timers

Architectures provide two hardware devices to help with time keeping: the system timer, which we have been discussing, and the real-time clock. The actual behavior and implementation of these devices varies between different machines, but the general purpose and design is about the same for each.
