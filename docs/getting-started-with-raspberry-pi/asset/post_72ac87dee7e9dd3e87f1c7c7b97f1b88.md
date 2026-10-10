
add_interrupt_randomness(irq); /* Contribute to entropy pool */
/* ... */
}

The generation of strongly random numbers depends on the size of the entropy pool:

```
bash> od -x /dev/random
0000000 7331 9028 7c89 4791 7f64 3deb 86b3 7564
0000020 ebb9 e806 221a b8f9 af12 cb30 9a0e cc28
0000040 68d8 0bbf 68a4 0898 528e 1557 d8b3 57ec
0000060 b01d 8714 b1e1 19b9 0a86 9f60 646c c269
```

The output stops after a few lines, signaling that the entropy pool is exhausted. To replenish the entropy pool and restart the random stream, jab the keyboard several times after switching to an unused terminal or push the mouse around the screen.

A dump of `/dev/urandom`, however, produces a continuous pseudo random stream that never stops.

`/dev/mem` and `/dev/kmem` are classic pseudo char devices that are tools that let you peek inside system memory. These char nodes export raw interfaces connected to physical memory and kernel virtual memory, respectively. To manipulate system memory, you may `mmap( )` these nodes and operate on the returned regions. As an exercise, change the hostname of your system by accessing `/dev/mem`.

All the char devices discussed in this section (`null`, `zero`, `random`, `urandom`, `mem`, and `kmem`) have different minor numbers but the same statically assigned major number, 1. Look at `drivers/char/mem.c` and `drivers/char/random.c` for their implementation. Two other pseudo drivers belong to the same major number family: `/dev/full`, which emulates an always full device; and `/dev/port`, which peeks at system I/O ports. We use the latter in Chapter 19.

## Misc Drivers

Misc (or miscellaneous) drivers are simple char drivers that share certain common characteristics. The kernel abstracts these commonalities into an API (implemented in `drivers/char/misc.c`), and this simplifies the way these drivers are initialized. All misc devices are assigned a major number of 10, but each can choose a single minor number. So, if a char driver needs to drive multiple devices as in the CMOS example discussed earlier, it's probably not a candidate for being a misc driver.

Consider the sequence of initialization steps that a char driver performs:

- Allocates major/minor numbers via `alloc_cdev_region()` and friends
- Creates `/dev` and `/sys` nodes using `class_device_create()`
- Registers itself as a char driver using `cdev_init()` and `cdev_add()`

A misc driver accomplishes all this with a single call to `misc_register()`:

```c
static struct miscdevice mydrv_dev = {
    MYDRV_MINOR,
    "mydrv",
    &mydrv_fops
};

misc_register(&mydrv_dev);
```

In the preceding example, `MYDRV_MINOR` is the minor number that you want to statically assign to your misc driver. You may also request a minor number to be dynamically assigned by specifying `MISC_DYNAMIC_MINOR` rather than `MYDRV_MINOR` in the `mydrv_dev` structure.

Each misc driver automatically appears under `/sys/class/misc/` without explicit effort from the driver writer. Because misc drivers are char drivers, the earlier discussion on char driver entry points hold for misc drivers, too. Let's now look at an example misc driver.

## Device Example: Watchdog Timer

A watchdog's function is to return an unresponsive system to operational state. It does this by periodically checking the system's pulse and issuing a reset⁽ᵃʳ⁾ if it can't detect any. Application software is responsible for registering this pulse (or "heartbeat") by periodically strobing (or "petting") the watchdog using the services of a watchdog device driver. Most embedded controllers support internal watchdog modules. External watchdog chips are also available. An example is the Netwinder W83977AF chip.

⁽ᵃʳ⁾ A watchdog may issue audible beeps rather than a system reset. An example scenario is when a timeout occurs due to a power supply problem, assuming that the watchdog circuit is backed up using a battery or a super capacitor.

Linux watchdog drivers are implemented as misc drivers and live inside `drivers/char/watchdog/`. Watchdog drivers, like RTC drivers, export a standard device interface to user land, so conforming applications are rendered independent of the internals of watchdog hardware. This API is specified in `Documentation/watchdog/watchdog-api.txt` in the kernel source tree. Programs that desire the services of a watchdog operate on */dev/watchdog*, a device node having a misc minor number of 130.

*Listing 5.9* implements a device driver for a fictitious watchdog module built in to an embedded controller. The example watchdog contains two main registers as shown in *Table 5.2*: a service register (*WD_SERVICE_REGISTER*) and a control register (*WD_CONTROL_REGISTER*). To pet the watchdog, the driver writes a specific sequence (*0xABCD* in this case) to the service register. To program watchdog timeout, the driver writes to specified bit positions in the control register.

**Table 5.2. Register Layout on the Watchdog Module**

| Register Name | Description |
| :--- | :--- |
| WD_SERVICE_REGISTER | Write a specific sequence to this register to pet the watchdog. |
| WD_CONTROL_REGISTER | Write the watchdog timeout to this register. |

Strobing the watchdog is usually done from user space because the goal of having a watchdog is to detect and respond to both application and kernel hangs. A critical application^[1] such as the graphics engine in *Listing 5.10* opens the watchdog driver in *Listing 5.9* and periodically writes to it. If no write occurs within the watchdog timeout due to an application hang or a kernel crash, the watchdog triggers a system reset. In the case of *Listing 5.10*, the watchdog will reboot the system if

- The application hangs inside `process_graphics()`
- The kernel, and consequently the application, dies

The watchdog starts ticking when an application opens */dev/watchdog*. Closing this device node stops the watchdog unless you set `CONFIG_WATCHDOG_NOWAYOUT` during kernel configuration. Setting this option helps you tie into the possibility that the watchdog monitoring process (such as *Listing 5.10*) gets killed by a signal while the system continues running.

### *Listing 5.9*. An Example Watchdog Driver

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
.name = "watchdog", /* /dev/watchdog */
.fops = &my_wdt_dog /* Watchdog driver entry points */
}

/* Driver methods */
struct file_operations my_wdt_dog = {
.owner = THIS_MODULE,
.open = my_wdt_open,
.release = my_wdt_close,
.write = my_wdt_write,
.ioctl = my_wdt_ioctl
}

/* Module Initialization */
static int __init
my_wdt_init(void)
{
/* ... */
misc_register(&my_wdt_dev);
/* ... */
}

/* Open watchdog */
static void
my_wdt_open(struct inode *inode, struct file *file)
{
/* Set the timeout and enable the watchdog */
WD_CONTROL_REGISTER |= DEFAULT_WATCHDOG_TIMEOUT << TIMEOUT_SHIFT;
WD_CONTROL_REGISTER |= 1 << WENABLE_SHIFT;
}

/* Close watchdog */
static int
my_wdt_close(struct inode *inode, struct file *file)
{
/* If CONFIG_WATCHDOG_NOWAYOUT is chosen during kernel
configuration, do not disable the watchdog even if the
application desires to close it */
#ifndef CONFIG_WATCHDOG_NOWAYOUT
/* Disable watchdog */
WD_CONTROL_REGISTER &= ~(1 << WENABLE_SHIFT);
#endif
return 0;
}

/* Pet the dog */
static ssize_t
my_wdt_write(struct file *file, const char *data,
size_t len, loff_t *ppose)
{
/* Pet the dog by writing a specified sequence of bytes to the
watchdog service register */
WD_SERVICE_REGISTER = 0xABCD;
}

/* ioctl method. Look at Documentation/watchdog/watchdog-api.txt
for the full list of ioctl commands. This is standard across
watchdog drivers, so conforming applications are rendered
hardware-independent */
static int
```

^[1] If you need to monitor the health of several applications, you may implement a multiplexer in the watchdog device driver. If any one of the processes that open the driver becomes unresponsive, the watchdog attempts to self-correct the system.
