```
```
556
    unregister_kprobe(&jprobe_eg);
}
MODULE_LICENSE("GPL");
```
```

When Listing 21.4 invokes register_kprobes() to register the kprobe, a kprobe is inserted at the beginning of printk(). When this probe is hit, Kprobes replace the saved return address with that of the registered jprobe handler, jprintk(). It then copies a portion of the stack and returns, thus passing control to jprintk() with printk()'s argument list. When jprintk() calls jprobe_return(), the original call state is restored, and printk() continues to execute normally.

When you insert this jprobe user module, the network driver no longer emits useless messages announcing $0 buffers, rather it prints saner information such as this:

> > Number of Free Receive buffers = 12.

# ### Return Probes

A return probe (or a kretprobe in Kprobes terminology) is another specialized Kprobes helper. It eases the work of inserting a kprobe when you need to probe a function's return point. If you use vanilla Kprobes to investigate return points, you might need to register them at multiple places because a function can return via multiple code paths. However, if you use return probes, you need to insert only one kretprobe, rather than register, say, 20 Kprobes to cover a function's 20 return paths.

The function tty_open() defined in drivers/char/tty_io.c has seven return paths. The successful path returns 0, and others return error values such as -ENXIO and -ENODEV. A single kretprobe is sufficient to alert you about failures, irrespective of the associated code path. Listing 21.5 implements this kretprobe.

# #### Listing 21.5. Registering Return Probe Handlers

```
```
Code View:
#include <linux/kernel.h>
#include <linux/module.h>
#include <linux/kprobes.h>
#include <linux/kallsyms.h>

/* kretprobe at exit from tty_open() */
static int
kret_tty_open(struct kretprobe_instance *kreti,
               struct pt_regs *regs)
{
    /* The EAX register contains the function return value
       on x86 systems */
    if ((int) regs->eax) {
        /* tty_open() failed. Announce the return code */
        printk("tty_open returned %d\n", (int)regs->eax);
    }
    return 0;
}

/* Per-probe structure */
static struct kretprobe kretprobe_eg = {
    .handler = (kretprobe_handler_t)kret_tty_open
};
```
```