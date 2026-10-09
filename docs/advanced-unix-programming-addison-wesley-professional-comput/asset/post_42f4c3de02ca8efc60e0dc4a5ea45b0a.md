
want a signal or a thread, you set member `aio_sigevent.sigev_notify` to `SIGEV_NONE`.

The `aio_reqprio` member is used to affect the priority of the operation and is only available when two other POSIX options, `_POSIX_PRIORITIZED_IO` and `_POSIX_PRIORITY_SCHEDULING`, are supported. For more on this feature, see [SUS2002].

The last member, `aio_lio_opcode`, is used with the `lio_listio` system call, as explained in Section 3.9.9.

## 3.9.3 `aio_read` and `aio_write`

The basic AIO functions are `aio_read` and `aio_write`. Just as with `pread` and `pwrite`, the `aio_offset` member determines where in the file the I/O is to take place. It’s ineffective if the file descriptor is open to a device that doesn’t allow seeking (e.g., a socket) or, for `aio_write`, if the `O_APPEND` flag is set (Section 2.8). The buffer and size are in the control block instead of being passed as arguments.

**aio_read**—asynchronous read from file

```c
#include <aio.h>

int aio_read(
    struct aiocb *aiocbp    /* control block */
);
/* Returns 0 on success or -1 on error (sets errno) */
```

**aio_write**—asynchronous write to file

```c
#include <aio.h>

int aio_write(
    struct aiocb *aiocbp    /* control block */
);
/* Returns 0 on success or -1 on error (sets errno) */
```

A successful return from these functions just means that the operation was initiated; it certainly doesn’t mean that the I/O was successful, or even that the values set in the control block were OK. You always have to check the result with `aio_error` (next section). An implementation might report an error such as invalid offset right away, with a -1 return from `aio_read` or `aio_write`, or it might return 0 and report the bad news later.

### 3.9.4 `aio_error` and `aio_return`

**aio_error**—retrieve error status for asynchronous I/O operation

```c
#include <aio.h>

int aio_error(
    const struct aiocb *aiocbp /* control block */
);
/* Returns 0, errno value, or EINPROGRESS (does not set errno) */
```

If the operation is complete, `aio_error` returns 0 if it was successful or the `errno` value that an equivalent `read`, `write`, `fsync`, or `fdatasync` would have returned (Sections 2.9, 2.10, and 2.16.2). If the operation isn’t complete, it returns `EINPROGRESS`. If you know that the operation completed (e.g., you got a signal saying so), you can treat `EINPROGRESS` just like any other error and use the `ecrv` macro, as we did in Section 3.6.1:

```c
ecrv( aio_error(aiocbp) )
```

I should mention, though, that the asynchronous I/O calls are usually used in fairly advanced applications for which our simple “ec” error checking may not be suitable, as I noted in Section 1.4.2. Still, `ecrv` is fine during development because of its ability to provide a function-call trace.

If `aio_error` says the operation was successful, you still may want the return value from the equivalent `read` or `write` to get the actual number of bytes transmitted. You do that with `aio_return`:

**aio_return**—retrieve return status of asynchronous I/O operation

```c
#include <aio.h>

size_t aio_return(
    struct aiocb *aiocbp /* control block */
);
/* Returns operation return value or -1 on error (sets errno) */
```

You’re supposed to call `aio_return` only if `aio_error` reported success. A -1 return from `aio_return` means that you called it wrong, not that the operation returned an error. Also, you can call `aio_return` only once per operation, as the value may be discarded once it’s been retrieved.

### 3.9.5 `aio_cancel`

You can cancel an outstanding asynchronous operation with `aio_cancel`:

**aio_cancel**—cancel asynchronous I/O request

```c
#include <aio.h>

int aio_cancel(
    int fd,                   /* file descriptor */
    struct aiocb *aiocbp      /* control block */
);
/* Returns result code or -1 on error (sets errno) */
```

If the `aiocbp` argument is `NULL`, this call attempts to cancel all asynchronous operations on file descriptor `fd`. Operations that weren’t cancelled report their completion in the normal way, but those that got cancelled report (via `aio_error`) an error code of `ECANCELED`.

If the `aiocbp` argument isn’t `NULL`, `aio_cancel` tries to cancel just the operation that was started with that control block. In this case the `fd` argument must be the same as the `aio_fildes` member of the control block.

If `aio_cancel` succeeds it returns one of these result codes:

| Code | Description |
| :--- | :--- |
| `AIO_CANCELED` | All the requested operations were cancelled. |
| `AIO_NOTCANCELED` | One or more requested operations (maybe all) were not cancelled because they were already in progress. You have to call `aio_error` on each operation to find out which were cancelled. |
| `AIO_ALLDONE` | None of the requested operations were cancelled because all were completed. |

### 3.9.6 `aio_fsync`

Aside from read and write equivalents, there’s a third kind of I/O that can be done asynchronously: flushing of the buffer-cache, as is done with `fsync` or `fdatasync` (see Section 2.16.2 for the distinction). Both kinds of flushing are handled with the same call:

**aio_fsync**—initiate buffer-cache flushing for one file

```c
#include <aio.h>

int aio_fsync(
    int op,                      /* O_SYNC or O_DSYNC */
    struct aiocb *aiocbp         /* control block */
);
/* Returns 0 on success or -1 on error (sets errno) */
```

The control block is used a little differently than it is with the other calls: All buffers associated with the file descriptor given by the `aio_fildes` member are flushed, not just those associated with the operation that was started with the control block, if one even was. The request to synchronize (i.e., flush the buffers) is asynchronous: It doesn’t happen right away, but is only initiated, and you can check for completion the usual way (e.g., with `aio_error` or with a signal). So, as with `aio_read` and `aio_write`, a return of zero just means that the initiation went OK.

### 3.9.7 `aio_suspend`

Instead of getting notified asynchronously via a signal or a thread when I/O is completed, you can decide to become synchronous by simply waiting for it to complete:

**aio_suspend**—wait for asynchronous I/O request

```c
#include <aio.h>

int aio_suspend(
    const struct aiocb *const list[], /* array of control blocks */
    int cnt,                          /* number of elements in array */
    const struct timespec *timeout    /* max time to wait */
);
/* Returns 0 on success or -1 on error (sets errno) */
```

If `timeout` is `NULL`, `aio_suspend` takes an array of `cnt` control blocks, and blocks until *one* of them completes. Each must have been used to initiate an asynchronous I/O operation. If at least one is already complete at the time of the call, `aio_suspend` returns immediately.

To help in reusing the same array, it’s OK for an element of `list` to be `NULL`, but such an element is included in `cnt`.

If `timeout` isn't `NULL`, `aio_suspend` blocks at most for that amount of time, and then returns −1 with `errno` set to `EAGAIN`. The `timespec` structure is in Section 1.7.2.

Like most other system calls that block, `aio_suspend` can be interrupted by a signal, as explained further in Section 9.1.4. This leads to one very tricky situation: The completion that `aio_suspend` is waiting for could, depending on how the control block is set up, generate a signal, and that will cause `aio_suspend` to be interrupted, which causes it to return −1 with `errno` set to `EINTR`. In some cases why it returned doesn't matter, but the problem with the `EINTR` return is that any signal could have caused it, not just one from the completed I/O request. You can avoid having an asynchronous-completion signal interrupt `aio_suspend` in one of two ways:

- Use a signal to indicate completion or call `aio_suspend`, but not both.
- Set the `SA_RESTART` flag (Section 9.1.6) for the signal.

Or, let a signal interrupt `aio_suspend` and just call `aio_error` for each element of the list you pass to `aio_suspend` when it returns to see what, if anything, happened, and reissue the `aio_suspend` (perhaps in a loop) if nothing did.

## 3.9.8 Example Comparing Synchronous and Asynchronous I/O

This section shows an example of how to use the AIO calls and also demonstrates some of their advantages over synchronous I/O.

First, here's a program called `sio` that uses conventional, synchronous I/O to read a file. Every 8000 reads, it also reads the standard input.

```c
#define PATH "/aug/c3/datafile.txt"
#define FREQ 8000

static void synchronous(void)
{
    int fd, count = 0;
    ssize_t nread;
    char buff1[512], buff2[512];

    ec_neg1( fd = open(PATH, O_RDONLY) )
    timestart();
    while ( true) {
        ec_neg1( nread = read(fd, buf1, sizeof(buf1)) )
        if (nread == 0)
            break;
```
