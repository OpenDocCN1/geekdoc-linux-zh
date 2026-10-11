# # The Time of Day

221

```
```
usec += (xtime.tv_nsec / 1000);
} while (read_seqretry(&xtime_lock, seq));
```
```

This loop repeats until the reader is assured that it read the data without an intervening write. If the timer interrupt occurred and updated xtime during the loop, the returned sequence number is invalid and the loop repeats.

The primary user-space interface for retrieving the wall time is gettimeofday(), which is implemented as sys_gettimeofday() in kernel/time.c:

```
```
asminkage long sys_gettimeofday(struct timeval *tv, struct timezone *tz)
{
    if (likely(tv)) {
        struct timeval ktv;
        do_gettimeofday(&ktv);
        if (copy_to_user(tv, &ktv, sizeof(ktv)))
            return -EFAULT;
    }
    if (unlikely(tz)) {
        if (copy_to_user(tz, sys_tz, sizeof(sys_tz)))
            return -EFAULT;
    }
    return 0;
}
```
```

If the user provided a non-NULL tv value, the architecture-dependent do_gettimeofday() is called. This function primarily performs the xtime read loop previously discussed. Likewise, if tz is non-NULL, the system time zone (stored in sys_tz) is returned to the user. If there were errors copying the wall time or time zone back to user-space, the function returns -EFAULT. Otherwise, it returns zero for success.

The kernel also implements the time() system call, but gettimeofday() largely supersedes it. The C library also provides other wall time-related library calls, such as ctime() and etime().

The settimeofday() system call sets the wall time to the specified value. It requires the CAP_SYS_TIME capability.

Other than updating xtime, the kernel does not make nearly as frequent use of the current wall time as user-space does. One notable exception is in the filesystem code, which stores various timestamps (accessed, modified, and so on) in inodes.

> 2 Some architectures, however, do not implement sys_time() and instead specify that it is emulated in the C library through the use of gettimeofday().