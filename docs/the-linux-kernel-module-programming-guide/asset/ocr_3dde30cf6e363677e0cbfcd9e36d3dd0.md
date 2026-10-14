more, the function prototype with unsigned long argument may be an obstacle to the forward-edge protection of control-flow integrity. Thus, it is better to use a unique prototype to separate from the cluster that takes an unsigned long argument. The timer callback should be passed a pointer to the timer_list structure rather than an unsigned long argument. Then, it wraps all the information the callback needs, including the timer_list structure, into a larger structure, and it can use the container_of macro instead of the unsigned long value. For more information see: Improving the kernel timers API.

Before Linux v4.14, setup_timer was used to initialize the timer and the timer_list structure looked like:

```
struct timer_list {
    unsigned long expires;
    void (*function)(unsigned long);
    unsigned long data;
    u32 flags;
    /* ... */
};

void setup_timer(struct timer_list *timer, void (*callback)(unsigned long),
    unsigned long data);
```

Since Linux v4.14, timer_setup is adopted and the kernel step by step converting to timer_setup from setup_timer. One of the reasons why API was changed is it need to coexist with the old version interface. Moreover, the timer_setup was implemented by setup_timer at first.

```
void timer_setup(struct timer_list *timer,
    void (*callback)(struct timer_list *), unsigned int flags);
```

The setup_timer was then removed since v4.15. As a result, the timer_list structure had changed to the following.

```
struct timer_list {
    unsigned long expires;
    void (*function)(struct timer_list *);
    u32 flags;
    /* ... */
};
```

The following source code illustrates a minimal kernel module which, when loaded, starts blinking the keyboard LEDs until it is unloaded.

```
/*
 * kbleds.c - Blink keyboard leds until the module is unloaded.
 */

#include <linux/init.h>
#include <linux/kd.h> /* For KDSETLED */
```