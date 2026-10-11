ment data. The difference between the two macros is the initial reference count. The first macro creates the tasklet with a count of zero, and the tasklet is enabled. The second macro sets count to one, and the tasklet is disabled. Here is an example:

```
`DECLARE_TASKLET(my_tasklet, my_tasklet_handler, dev);`
```

This line is equivalent to

```
```c
struct tasklet_struct my_tasklet = { NULL, 0, ATOMIC_INIT(0),
                                     my_tasklet_handler, dev };
```
```

This creates a tasklet named my_tasklet enabled with tasklet_handler as its handler. The value of dev is passed to the handler when it is executed.

To initialize a tasklet given an indirect reference (a pointer) to a dynamically created struct tasklet_struct, t, call tasklet_init():

```
`tasklet_init(t, tasklet_handler, dev); /* dynamically as opposed to statically */`
```

# ## Writing Your Tasklet Handler

The tasklet handler must match the correct prototype:

```
`void tasklet_handler(unsigned long data);`
```

As with softirqs, tasklets cannot sleep. This means you cannot use semaphores or other blocking functions in a tasklet. Tasklets also run with all interrupts enabled, so you must take precautions (for example, disable interrupts and obtain a lock) if your tasklet shares data with an interrupt handler. Unlike softirqs, however, two of the same tasklets never run concurrently—even though two different tasklets can run at the same time on two different processors. If your tasklet shares data with another tasklet or softirq, you need to use proper locking (see Chapter 9, “An Introduction to Kernel Synchronization,” and Chapter 10, “Kernel Synchronization Methods” ).

# ## Scheduling Your Tasklet

To schedule a tasklet for execution, tasklet_schedule() is called and passed a pointer to the relevant tasklet_struct:

```
`tasklet_schedule(emv_tasklet); /* mark my_tasklet as pending */`
```