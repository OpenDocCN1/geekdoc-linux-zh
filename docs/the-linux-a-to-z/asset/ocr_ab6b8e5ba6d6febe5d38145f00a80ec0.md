The only things here which require some explanation are the macro definitions for TRACE_TXT() and TRACE_CHR(). These are provided to give a very simple trace facility for debugging purposes. At various strategic locations throughout the device driver code, calls to these macros are inserted so that ‘got here’ type messages can be displayed on the machine's console terminal. Trace messages are displayed on the console screen using the kernel's internal function: console_print(). The display of trace messages is controlled by the state of a flag variable whose value can be set or reset via an appropriate ioctl() call. The two commands to ioctl() dealt with by the driver are TDD_TRON to turn tracing on and TDD_TROFF to turn it off again. Neither of these ioctl() commands takes any other parameters.

# 26.2 init Function

Moving on into the driver code proper, the first thing to look at is the initialization function, tdd_init():

```
void tdd_init(void)
{
    tdd_trace = TRUE;

    if (register_chrdev(30, "tdd", &tdd_fops))
        TRACE_TXT("Cannot register tdd driver as major device 30")
    else
        TRACE_TXT("Tiny device driver registered successfully")

    qhead = 0;
    write_busy = FALSE;
    read_busy = FALSE;
    tdd_trace = FALSE;
    return;
}
```

This routine is executed at system boot time. Remember that a call to the routine needs to be added to the chr_dev_init() function in the file:

`/usr/src/linux/drivers/char/mem.c`

assuming your kernel source is stored in /usr/src/linux.

When tdd_init() is executed it calls the kernel function register_chrdev() to add its file_operations structure to the character device routine address table. A message is displayed on the machine console, using the debug trace facility, to report the success or failure of this operation. The routine then initializes the driver's static variables and finally returns.