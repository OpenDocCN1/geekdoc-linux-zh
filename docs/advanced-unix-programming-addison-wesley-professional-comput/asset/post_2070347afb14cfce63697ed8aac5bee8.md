
Assuming the file offsets are starting at zero, if we write 100 bytes on `fd1` and then read 100 bytes on `fd2`, we get the 100 bytes we just wrote. But if we write on `fd3` and then read on `fd3`, we get whatever is *after* the written data, and an end-of-file if there wasn't anything because a file description has only a single offset, used by both `read` and `write`.

You can find out where the file offset is and/or set it to a new value with `lseek` (Section 2.13) on a file descriptor. The new value then affects the next `read` or `write` on that file descriptor.

Later, in Chapter 6, we're going to see how to duplicate an open file descriptor. By "duplicate" I don't mean copying, like `fd1 = fd2;`. I mean using a system call that duplicates, such as `dup`. Anyway, for now the important point is that if a file descriptor is a duplicate of another, they share the same file offset because they share the same open file description.

If the file is opened with the `O_APPEND` flag set, all writes with the `write` system call are preceded by an implicit `lseek` to the end of the file, so writing occurs at the end, atomically. Even if several processes with the file opened with `O_APPEND` are writing at once, each of their writes will go at the end as it is that instant, and they won't overwrite each other or intermingle their data. You can't do the equivalent thing with `lseek` followed by a `write` (`O_APPEND` not set) because as we've seen in other situations, there's a gap between the two system calls that could result in this:

- Process A seeks its file offset to the end (position 1000, say).
- Process B seeks its file offset to the end (also position 1000).
- Process B writes 200 bytes (at position 1000).
- Process A writes 200 bytes (at position 1000—overwriting B). Ouch!

We could use a lock (Section 2.4.3) to fix this, but there's a much better way: If `O_APPEND` was set when process A and B opened the file, you are guaranteed to get this:

- Process A seeks its file offset to the end (position 1000, say) and writes.
- Process B seeks its file offset to the end (position 1200) and writes.

So `O_APPEND` is perfect for log files or other situations when you want to accumulate output from several processes.

You can also read and write by just specifying the position in the system call itself, without first calling `lseek`; that’s what *pread* and *pwrite* do (Section 2.14). They don’t use the file offset, and they don’t change it, either.

Since you probably already know pretty much how *read* and *write* work, if you like you can skip to Section 2.13 to read about *lseek* and see some interesting examples and then loop back to Section 2.9 to continue in sequence.

### 2.9 write System Call

`write`—write to file descriptor

```c
#include <unistd.h>

ssize_t write(
    int fd,                /* file descriptor */
    const void *buf,       /* data to write */
    size_t nbytes          /* amount to write */
);
/* Returns number of bytes written or -1 on error (sets errno) */
```

We’ve talked so much about *write*, don’t you think it’s time we got properly introduced?

*write* writes the *nbytes* bytes pointed to by *buf* to the open file represented by *fd*. The write starts at the current position of the file offset, and, after the write, the file offset is incremented by the number of bytes written. The number of bytes written, or $-1$ if there was an error, is returned.

Recall that if the `O_APPEND` flag is set, the file offset is set automatically to the end of the file prior to the write.

*write* is used to write to pipes, special files, and sockets, too, but its semantics are somewhat different in these cases. One important difference is that such writes can block, which means that they’re waiting for some unpredictable event, such as data being available. If a *write* is blocked, it can be interrupted by the arrival of a signal (Section 9.1.4), in which case it returns $-1$ with *errno* set to EINTR. I’ll postpone the rest of the discussion of writes to other than regular files until Chapters 4, 6, and 8, when I talk about other types of files.

`write` is deceptively simple. It seems that it writes the data and then returns, but a little experimentation will convince you that this is impossible—it’s too fast. It must be cheating!

Indeed, it does cheat. When you issue a write system call, it does not perform the write and then return. It just transfers the data to a buffer cache in the kernel and then returns, claiming nothing more than this:

> I’ve taken note of your request, and rest assured that your file descriptor is OK. I’ve copied your data successfully, and there’s enough disk space. Later, when it’s convenient for me, and if I’m still alive, I’ll try to put your data on the disk where it belongs. If I discover an error then I’ll try to print something on the console, but I won’t tell you about it (indeed, you may have terminated by then). If you, or any other process, tries to read this data before I’ve written it out, I’ll give it to you from the buffer cache, so, if all goes well, you’ll never be able to find out when and if I’ve completed your request. You may ask no further questions. Trust me, and thank me for the speedy reply—I figured that’s all you really cared about.

If all does go well, delayed writing is fantastic. The semantics are the same as if the writing actually took place, but it’s much faster. However, if there is a disk error, or if the kernel stops for any reason, then the game is up. We discover that the data we “wrote” isn’t on the disk at all.

In addition to the uncertainty about when the physical write occurs, there are two other problems with delayed writes. First, a process initiating a write cannot be informed of write errors. Indeed, file system buffers aren’t owned by any single process; if several processes write to the same block of the same file at the same time, their data will be transferred to the same buffer. Of course, one could conceive of a scheme in which a “write error” signal would be sent to every process that wrote a particular buffer, but what is a process supposed to do about it at that late date? And how does the kernel notify processes that have already terminated?

The second problem is that the order of physical writes can’t be controlled. Order often matters. For example, in updating a linked-list structure on a file, it is better to write a new record and then update the pointer to it, rather than the reverse. This is because a record not pointed to is usually less of a problem than a pointer that points nowhere. Even if the write system calls are issued in a particular order, however, that doesn’t mean that the buffers will be physically written to disk in that order. So careful replacement techniques, of which this is but one example, are not as advantageous as they might be. They guard against the process itself terminating at an inopportune time, but not against disk errors or kernel crashes.

Fortunately, you can force synchronized writes, and I'll explain how in Section 2.16.

These problems with $write$ should not be overemphasized. Considering how reliable computers are today, and how reliable UNIX implementations usually are, kernel crashes are quite rare. Most users are pleased to benefit from the quick response provided by the buffer cache and never find out that the kernel is cheating.

Now let’s look once again at the file copy example at the beginning of this chapter. The bug is in the check for a write error:

```c
if (write(tofd, buf, nread) != nread)
    EC_FAIL;
```

It is *not* an error if the count returned by $write$ is less than the requested count. Maybe the count is short because the write is to a pipe that’s momentarily full, or maybe it’s a regular file that’s reached its size limit. It will be the *next* call to write that will produce the error.$^{6}$

So the bug is that the `EC_FAIL` macro will record a meaningless value for $errno$, which is set *only* when the return value is $-1$. We could recode the function to withstand partial writes and to keep trying until a real error occurs:

```c
#define BUFSIZE 512

void copy2(char *from, char *to)
{
    int fromfd = -1, tofd = -1;
    ssize_t nread, nwrite, n;
    char buf[BUFSIZE];

    ec_neg1( fromfd = open(from, O_RDONLY) )
    ec_neg1( tofd = open(to, O_WRONLY | O_CREAT | O_TRUNC,
             S_IRUSR | S_IWUSR) )
    while ((nread = read(fromfd, buf, sizeof(buf))) > 0) {
        nwrite = 0;
        do {
            ec_neg1( n = write(tofd, &buf[nwrite], nread - nwrite) )
            nwrite += n;
        } while (nwrite < nread);
    }
}
```

6. Although, even then, it’s possible that whatever caused the short count, such as being out of space, resolved itself before the next call, so it won’t return an error. That is, there’s no 100% reliable way of finding out why a partial $write$ or $read$ was short.
