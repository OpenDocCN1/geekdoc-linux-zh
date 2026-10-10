```
```
...
handler:  f8a8c000  <rtc_interrupt>
           flags: 20000000  (SA_INTERRUPT)
           mask: 0
           name: f8a8c29d  "rtc"

crash> quit
bash>
```
```

Let's now shift gears and look at a case where the kernel freezes, rather than generate an "oops." Consider the following buggy driver `init()` routine:

```
```
static int __init
mydrv_init(void)
{
  
    spin_lock(&mydrv_wq.lock);   /* Usage before initialization! */
    spin_lock_init(&mydrv_wq.lock);
  
    /* ... */
}
```
```

The code is erroneously using a spinlock before initializing it. Effectively, the CPU spins forever trying to acquire the lock, and the kernel appears to hang. Let's debug this problem using kdump. In this case, there will be no auto-trigger because there is no panic, so force a crash dump by pressing the magic Sysrq key combination, Alt-Sysrq-c. You may need to enable Sysrq by writing a 1 to `/proc/sys/kernel/sysrq`:

```
```
bash> echo 1 > /proc/sys/kernel/sysrq
bash> insmod mydrv.ko
```
```

This induces the kernel to hang inside `mydrv_init()`. Press the Alt-Sysrq-c key combination to trigger a crash dump:

```
```
Alt-Sysrq-c
...
→ Messages announcing that a crash dump
has been triggered
```
```

Save the dump to disk after kexec boots the capture kernel, boot back to the original kernel, and run crash on the saved dump:

```
```
bash> crash vmlinux vmcore.dump
...
PANIC: "SysRq : Trigger a crashdump"
PID: 2115
COMMAND: "insmod"
  TASK: f7e57000  [THREAD_INFO: f6170000]
CPU: 0
STATE: TASK_RUNNING (SYSRQ)
crash>
```
```

Test the waters by checking the identity of the process that was running at the time of the crash. In this case, it