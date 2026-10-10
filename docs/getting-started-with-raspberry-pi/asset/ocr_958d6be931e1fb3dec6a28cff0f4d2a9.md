watchdog operate on */dev/watchdog*, a device node having a misc minor number of 130.

*Listing 5.9* implements a device driver for a fictitious watchdog module built in to an embedded controller. The example watchdog contains two main registers as shown in *Table 5.2*: a service register (*WD_SERVICE_REGISTER*) and a control register (*WD_CONTROL_REGISTER*). To pet the watchdog, the driver writes a specific sequence (*0xABCD* in this case) to the service register. To program watchdog timeout, the driver writes to specified bit positions in the control register.

Table 5.2. Register Layout on the Watchdog Module

| Register Name | Description |
| :--- | :--- |
| WD_SERVICE_REGISTER | Write a specific sequence to this register to pet the |
| | watchdog. |
| WD_CONTROL_REGISTER | Write the watchdog timeout to this register. |

Strobing the watchdog is usually done from user space because the goal of having a watchdog is to detect and respond to both application and kernel hangs. A critical application^[1] such as the graphics engine in *Listing 5.10* opens the watchdog driver in *Listing 5.9* and periodically writes to it. If no write occurs within the watchdog timeout due to an application hang or a kernel crash, the watchdog triggers a system reset. In the case of *Listing 5.10*, the watchdog will reboot the system if

+   * The application hangs inside `process_graphics()`
+   * The kernel, and consequently the application, dies

The watchdog starts ticking when an application opens */dev/watchdog*. Closing this device node stops the watchdog unless you set `CONFIG_WATCHDOG_NOWAYOUT` during kernel configuration. Setting this option helps you tie into the possibility that the watchdog monitoring process (such as *Listing 5.10*) gets killed by a signal while the system continues running.

# *Listing 5.9*. An Example Watchdog Driver

```
Code View:

```c
#include <linux/miscdevice.h>
#include <linux/watchdog.h>

#define DEFAULT_WATCHDOG_TIMEOUT    10  /* 10-second timeout */
#define TIMEOUT_SHIFT               5   /* To get to the timeout field
                                             in WD_CONTROL_REGISTER */
#define WENABLE_SHIFT               3   /* To get to the
                                             watchdog-enable field in
                                             WD_CONTROL_REGISTER */

/* Misc structure */
static struct miscdevice my_wdt_dev = {
  .minor = WATCHDOG_MINOR, /* defined as 130 in
                             include/linux/miscdevice.h*/
```
```

^[1] If you need to monitor the health of several applications, you may implement a multiplexer in the watchdog device driver. If any one of the processes that open the driver becomes unresponsive, the watchdog attempts to self-correct the system.