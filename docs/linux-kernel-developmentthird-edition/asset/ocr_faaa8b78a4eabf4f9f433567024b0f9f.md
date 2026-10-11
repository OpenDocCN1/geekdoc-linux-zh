The my_timer.expires value specifies the timeout value in absolute ticks. When the current jiffies count is equal to or greater than my_timer.expires, the handler function my_timer.function is run with the lone argument of my_timer.data. As you can see from the timer_list definition, the function must match this prototype:

```
```
void my_timer_function(unsigned long data);
```
```

The data parameter enables you to register multiple timers with the same handler, and differentiate between them via the argument. If you do not need the argument, you can simply pass zero (or any other value).

Finally, you activate the timer:

```
```
add_timer(&my_timer);
```
```

And, voila, the timer is off and running! Note the significance of the expired value. The kernel runs the timer handler when the current tick count is equal to or greater than the specified expiration. Although the kernel guarantees to run no timer handler prior to the timer's expiration, there may be a delay in running the timer. Typically, timers are run fairly close to their expiration; however, they might be delayed until the first timer tick after their expiration. Consequently, timers cannot be used to implement any sort of hard real-time processing.

Sometimes you might need to modify the expiration of an already active timer. The kernel implements a function, mod_timer(), which changes the expiration of a given timer:

```
```
mod_timer(&my_timer, jiffies + new_delay);  /* new expiration */
```
```

The mod_timer() function can operate on timers that are initialized but not active, too. If the timer is inactive, mod_timer() activates it. The function returns zero if the timer were inactive and one if the timer were active. In either case, upon return from mod_timer(), the timer is activated and set to the new expiration.

If you need to deactivate a timer prior to its expiration, use the del_timer() function:

```
```
del_timer(&my_timer);
```
```

The function works on both active and inactive timers. If the timer is already inactive, the function returns zero; otherwise, the function returns one. Note that you do not need to call this for timers that have expired because they are automatically deleted.

A potential race condition that must be guarded against exists when deleting timers. When del_timer() returns, it guarantees only that the timer is no longer active (that is, that it will not be executed in the future). On a multiprocessor machine, however, the timer handler might already be executing on another processor. To deactivate the timer and wait until a potentially executing handler for the timer exits, use del_timer_sync():

```
```
del_timer_sync(&my_timer);
```
```

Unlike del_timer(), del_timer_sync() cannot be used from interrupt context.