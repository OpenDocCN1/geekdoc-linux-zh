The executable program `011st01` is invoked in line 1 in the output shown. Lines 2 and 3 show that the socket pair was opened on file descriptors 3 and 4. What follows in lines 4 to 20 are the output lines from the `netstat(1)` command that was invoked from the `system(3)` function call, within the program.

Notice lines 14 and 15 in the `netstat(1)` output of Listing 1.2. Looking under the column for “PID/Program name” we can see that our program named `011st01` had a process ID of 662 and had two “unix” sockets open. Although not shown in the output, you will see under the column “State” that the sockets are shown as connected.

Although the program didn’t do anything with the socket pair that it created, it did demonstrate the creation of a socket pair. It also demonstrated that the sockets are allocated to file unit numbers in the same manner that opened files are.

The astute reader also might have noticed that this pair of `AF_LOCAL` sockets are also referred to as “unix” sockets (we saw this in the `netstat(1)` output). In fact, the C macro constant `AF_UNIX` could have been used in place of the macro `AF_LOCAL` for the domain value in the `socketpair(2)` function call. These values are equivalent, although standards efforts are now encouraging the use of `AF_LOCAL` over `AF_UNIX`.

# ## Performing I/O on Sockets

You learned earlier that sockets can be written to and read from just like any opened file. In this section, you are going to demonstrate this firsthand for yourself. For the sake of completeness however, let’s review the function synopsis for the calls `read(2)`, `write(2)`, and `close(2)` before we put them to work:

```
```c
#include <unistd.h>

ssize_t read(int fd, void *buf, size_t count);
ssize_t write(int fd, const void *buf, size_t count);
int close(int fd);
```
```

These are `Linux` input/output functions you should be already familiar with. By way of review, the function `read(2)` returns input that is available from the file descriptor `fd, into your supplied buffer buf` of a maximum size of `count` bytes. The return value represents the number of bytes read. A return count of zero represents `end-of-file`.

The `write(2)` function writes data to your file descriptor `fd, from your supplied buffer buf` for a total of `count` bytes. The returned value represents