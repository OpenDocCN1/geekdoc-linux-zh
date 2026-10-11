```
```C
if (!copy_from_user(system_utsname.nodename, name, len)) {
    system_utsname.nodename[len] = 0;
    errno = 0;
}
up_write(&uts_sem);
return errno;
}

asmlinkage long sys_gethostname(char *name, int len)
{
    int i, errno;

    if (len < 0)
        return -EINVAL;
    down_read(&uts_sem);
    i = 1 + strlen(system_utsname.nodename);
    if (i > len)
        i = len;
    errno = 0;
    if (copy_to_user(name, system_utsname.nodename, i))
        errno = -EFAULT;
    up_read(&uts_sem);
    return errno;
}
```

```

The points to note about this example are:

+   1. The functions may block while copying data from/to userspace in `copy_from_user()`/`copy_to_user()`. Therefore they could not use any form of spinlock here.
+   2. The semaphore type chosen is read–write as opposed to basic because there may be lots of concurrent **gethostname(2)** requests which need not be mutually exclusive.

Although Linux implementation of semaphores and read–write semaphores is very sophisticated, there are possible scenarios one can think of which are not yet implemented, for example there is no concept of interruptible read–write semaphores. This is obviously because there are no real–world situations which require these exotic flavours of the primitives.

# 2.15 Kernel Support for Loading Modules

Linux is a monolithic operating system and despite all the modern hype about some "advantages" offered by operating systems based on micro–kernel design, the truth remains (quoting Linus Torvalds himself):

> ```
> … message passing as the fundamental operation of the OS is
> just an exercise in computer science masturbation. It may
> feel good, but you don't actually get anything DONE.
> ```

Therefore, Linux is and will always be based on a monolithic design, which means that all subsystems run in the same privileged mode and share the same address space; communication between them is achieved by the usual C function call means.

However, although separating kernel functionality into separate "processes" as is done in micro–kernels is definitely a bad idea, separating it into dynamically loadable on demand kernel modules is desirable in some