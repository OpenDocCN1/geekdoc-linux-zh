# Introduction to the Linux Operating System

Figure 2.30 Linux network device registration 2: linux/net/core/dev.c.

```
/*
 * Default initial state at registry is that the
 * device is present.
 */
set_bit(_LINK_STATE_PRESENT, &dev->state);

dev->next = NULL;
dev_init_scheduler(dev);
write_lock_bb(&dev_base_lock);
 *dp = dev;
dev->deadbeef = 0;
write_unlock_bb(&dev_base_lock);

/* Notify protocols, that a new device appeared. */
otifier_call_chain(&netdev, NETDEV_REGISTER, dev);

net_run_sbin_hotplug(dev, "register");

return 0;
```

# 2.9 A Day in the Life of a Kernel Module

One of the critically acclaimed features of Linux today is that it achieves the flexibility of a microkernel without the need for server processes with the inevitable overhead of domain-crossing process communication. This is done through modules. This is illustrated in Figure 2.31.

Modules are runtime loadable code that is linked into the kernel. This is achieved through a relatively simple interface that works by defining a generic set of routines to initialize and clean up a module, and to export an interface with a set of symbols (variables, functions, and on) and module cross-dependencies. Dealing with cross dependencies is not rocket science—it is what link loaders do every day when you compile and link an application that uses several functions from different libraries. What happens is kernel code is annotated by explicit listing of the symbols that are exported (see /proc/ksyms), and the module management tools use these to resolve what is and isn't needed.

There are some applications for managing modules that live in /sbin, such as insmod, rmmod, and modprobe. The first two can be used manually (via scripts) to add or delete a module. The latter is actually invoked by the kernel (so the kernel that uses modules requires a filesystem with at least /sbin so