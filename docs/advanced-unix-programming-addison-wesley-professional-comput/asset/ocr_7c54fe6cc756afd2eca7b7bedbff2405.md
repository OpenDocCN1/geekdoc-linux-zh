want a signal or a thread, you set member `aio_sigevent.sigev_notify` to `SIGEV_NONE`.

The `aio_reqprio` member is used to affect the priority of the operation and is only available when two other POSIX options, `_POSIX_PRIORITIZED_IO` and `_POSIX_PRIORITY_SCHEDULING`, are supported. For more on this feature, see \[SUS2002\].

The last member, `aio_lio_opcode`, is used with the `lio_listio` system call, as explained in Section 3.9.9.

# 3.9.3 **aio_read and aio_write**

The basic AIO functions are `aio_read` and `aio_write`. Just as with `pread` and `pwrite`, the `aio_offset` member determines where in the file the I/O is to take place. It’s ineffective if the file descriptor is open to a device that doesn’t allow seeking (e.g., a socket) or, for `aio_write`, if the `O_APPEND` flag is set (Section 2.8). The buffer and size are in the control block instead of being passed as arguments.

```
**aio_read**—asynchronous read from file

```c
#include <aio.h>

int aio_read(
    struct aiocb *aiocbp    /* control block */
);
/* Returns 0 on success or -1 on error (sets errno) */
```
```

```
**aio_write**—asynchronous write to file

```c
#include <aio.h>

int aio_write(
    struct aiocb *aiocbp    /* control block */
);
/* Returns 0 on success or -1 on error (sets errno) */
```
```

A successful return from these functions just means that the operation was initiated; it certainly doesn’t mean that the I/O was successful, or even that the values set in the control block were OK. You always have to check the result with `aio_error` (next section). An implementation might report an error such as invalid offset right away, with a -1 return from `aio_read` or `aio_write`, or it might return 0 and report the bad news later.