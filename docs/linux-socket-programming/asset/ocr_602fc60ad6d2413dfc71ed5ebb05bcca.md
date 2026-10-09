# ## Prototype

```
```
#include <sys/poll.h>
int poll(struct pollfd *ufds, unsigned int nfds, int timeout);
```
```

# ## Return Value

If less than zero, an error occurred; a zero returned means that the call timed out. Otherwise, the call returns the number of descriptor records that changed.

# ## Parameters

| ufd s | The following is an array of `pollfd` structures. Each record tracks a different file descriptor. | |
| | `struct pollfd{` | |
| | `int fd; /* file descriptor */` | |
| | `short events; /* requested events */` | |
| | `short revents; /* returned events */` | |
| | `};` | |
| | The `fd` field is the file descriptor to check. The `events` and `revents` fields indicate the events to check and the events that occurred, respectively. The bit-values available are as follows: `POLLIN` There is data to read. `POLLPRI` There is urgent data to read. `POLLOUT` Writing now will not block. `POLLRERR` Error condition. `POLLHUP` Hung up. `POLLNVAL` Invalid request: `fd` not open. `POLLRDNORM` Normal read (Linux only). `POLLRDBAND` Read out-of-band (Linux only). `POLLWRNORM` Normal write (Linux only). `POLLWRBAND` Write out-of-band (Linux only). | |
| nfds | The number of records to check during the call. | |
| timeout | The timeout in milliseconds. If timeout is negative, the call waits forever. | |

# ## Possible Errors

| ENOMEM | There was no space to allocate file descriptor tables. |
| :--- | :--- |
| EFAULT | The array given as argument was not contained in the calling program's address space. |
| EINTR | A signal occurred before any requested event. |

# ## Example

```
```
int fd_count=0;
struct pollfd fds[MAXFDS];
 fds[fd_count].fd = socket(PF_INET, SOCK_STREAM, 0);
 /*** bind() and listen() socket ***/
 fds[fd_count++].events = POLLIN;
for (;;)
{
    if ( poll(fds, fd_count, TIMEOUT_MS) > 0 )
    {
        int i;
        if ( (fds[0].revents & POLLIN) != 0 )
        {
            fds[fd_count].events = POLLIN | POLLHUP;
            fds[fd_count++].fd = accept(fds[0].fd, 0, 0);
        }
        for ( i = 1; i < fd_count; i++ )
        {
```

```