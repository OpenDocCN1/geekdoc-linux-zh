
any function defined with this attribute is placed in a separate ELF section named `.init.text`. Its use is similar to the following:

```c
static int __init loop_init(void)
```

This invocation would place the compiled loop_init() function into the `.init.text` section of the loop.ko object module. When the module is loaded, the kernel allocates a chunk of memory for the main body of the module, which is pointed to by the struct module member named module_core. It then allocates a separate chunk of memory to hold the `.init.text` section. After the initialization function is called, the kernel frees the memory that contained the initialization function. Because the object module is split like this, we need to inform gdb of this addressing scheme to be able to use symbolic data for debugging the initialization function.⁹ Listing 14-19 demonstrates these steps.

## Listing 14-19

Debugging Module init Code

```text
$ ppc_64x-gdb -silent vmlinux
(gdb) target remote /dev/ttyS0
Remote debugging using /dev/ttyS0
breakinst () at arch/ppc/kernel/ppc-stub.c:825
825

<< Place a breakpoint before calling module init >>
(gdb) b module.c:1907
Breakpoint 1 at 0x0036418: file kernel/module.c, line 1907.
(gdb) c
Continuing.

Breakpoint 1, sys_init_module (umod=0xd102ef40, len=0x2c3b, uargs=0x10016338 ***)
at kernel/module.c:1907
1907		ret = mod->init();

<< Discover init addressing from struct module >>
(gdb) 1smod
Address	Module
0xd1022f40	loop
(gdb) set $m=(struct module *)0xd102ef40
(gdb) p $m->module_core
$1 = (void *) 0xd102b000
(gdb) p $m->module_init
$2 = (void *) 0xd1031000
```

⁹ As of this writing, there is a bug in gdb that prevents this technique from working properly. Hopefully, by the time you read this, it will be fixed.

```text
< Now load a symbol file using the core and init_addr>
(gdb) add-symbol-file ./drivers/block/loop ko 0xd102000 -s init.text
0xd1031000
add symbol table from file "../drivers/block/loop ko" at
.text_addr = 0xd102000
.init.text_addr = 0xd1031000
(y or n) y
Reading symbols from /home/chris/sandbox/2.6.13-
-amc/drivers/block/loop ko . done.
(gdb) b loop_init
Breakpoint 3 at 0x031000: file drivers/block/loop c, line 1244.
(gdb) c
Continuing.

<< Breakpoint hit, proceed to debug module init function>>
Breakpoint 3, 0xd1031000 in loop_init() file drivers/block/loop c, line 1244
1244         if (max_loop < 1 || max_loop > 256) {
(gdb)
```

### 14.3.6 printk Debugging

Debugging kernel and device driver code using `printk` is a popular technique, mostly because `printk` has evolved into a very robust method. You can call `printk` from almost any context, including from interrupt handlers. `printk` is the kernel's version of the familiar `printf()` C library function. `printk` is defined in `./kernel/printk.c`.

It is important to understand the limitations of using `printk` for debugging. First, `printk` requires a console device. Moreover, although the console device is configured as early as possible during kernel initialization, there are many calls to `printk` before the console device has been initialized. We present a method to cope with this limitation later, in Section 14.5, “When It Doesn't Boot.”

The `printk` function allows the addition of a string marker that identifies the level of severity of a given message. The header file `.../include/linux/kernel.h` defines eight levels:

```c
#define KERN_EMERG    "<0>" /* system is unusable */
#define KERN_ALERT    "<1>" /* action must be taken immediately */
#define KERN_CRIT     "<2>" /* critical conditions */
#define KERN_ERR      "<3>" /* error conditions */
#define KERN_WARNING  "<4>" /* warning conditions */
#define KERN_NOTICE   "<5>" /* normal but significant condition */
#define KERN_INFO     "<6>" /* informational */
#define KERN_DEBUG    "<7>" /* debug-level messages */
```

A simple `printk` message might look like this:

```c
printk("foo! entered w/%s\n", arg);
```

If the severity string is omitted, the kernel assigns a default severity level, which is defined in `printk.c`. In recent kernels, this is set at severity level 4, `KERN_WARNING`. Specifying `printk` with a severity level might look something like this:

```c
printk(KERN_CRIT "vmalloc failed in foo()\n");
```

By default, all `printk` messages follow a predefined *loglevel* are displayed on the system console device. The default loglevel is defined in `printk.c`. In recent Linux kernels, it has the value 7. This means that any `printk` message that is greater in importance than `KERN_DEBUG` will be displayed on the console.

You can set the default kernel loglevel in a variety of ways. At boot time, you can specify the default loglevel on your target board by passing the appropriate kernel command line parameters to the kernel at boot time. Three kernel command line options defined in `main.c` affect the default loglevel:

- *debug*—Sets the console loglevel to 10
- *quiet*—Sets the console loglevel to 4
- *loglevel=*—Sets the console loglevel to your choice of value

Using *debug* effectively displays every `printk` message. Using *quiet* displays all `printk` messages of severity `KERN_ERR` or higher.

`printk` messages can be logged to files on your target or via the network. Use `klogd` (kernel log daemon) and `syslogd` (system log daemon) to control the logging behavior of `printk` messages. These popular utilities are described in man pages and many Linux references, and are not described here.

### 14.3.7  Magic SysReq Key

This useful debugging aid is invoked through a series of special predefined key sequences that send messages directly to the kernel. For many target architectures and boards, you use a simple terminal emulator on a serial port as a system console. For these architectures, the Magic SysReq key is defined as a break character followed by a command character. Consult the documentation on the terminal emulator you use for how to send a break character. Many Linux developers use the `minicom` terminal emulator. For `minicom`, the break character is sent by typing

Ctrl-A F. After sending the break in this manner, you have 5 seconds to enter the command character before the command times out.

This useful kernel tool can be very helpful for development and debugging, but it can also cause data loss and system corruption. Indeed, the b command immediately reboots your system without any notification or preparation. Open files are not closed, disks are not synced, and file systems are not unmounted. When the reboot (b) command is issued, control is immediately passed to the reset vector of your architecture in a most abrupt and stunning manner. Use this powerful tool at your own peril!

This feature is well documented in the Linux kernel documentation subdirectory in a file called sysrq.txt. There you find the details for many architectures and the description of available commands.

For example, another way to set the kernel loglevel just discussed is to use the Magic SysReq key. The command is a number from 0 through 9, which results in the default loglevel being set to the number of the command. From minicom, press Ctrl-A F followed by a number, such as 9. Here is how it looks on the terminal:

```text
$ SysRq : Changing Loglevel
    loglevel set to 9
```

Commands can be used to dump registers, shut down your system, reboot your system, dump a list of processes, dump current memory information to your console, and more. See the documentation file in any recent Linux kernel for the details.

This feature is most commonly used when something causes your system to lock up. Often the Magic SysReq key provides a way to learn something from an otherwise dead system.

### 14.4 Hardware-Assisted Debugging

By now you've probably realized that you cannot debug very early kernel-startup code with KGDB. This is because KGDB is not initialized until after most of the low-level hardware-initialization code has executed. Furthermore, if you are assigned the task of bringing up a brand-new board design and porting a bootloader and the Linux kernel, having a hardware-debug probe is without a doubt the most efficient means of debugging problems in these early stages of board porting.
