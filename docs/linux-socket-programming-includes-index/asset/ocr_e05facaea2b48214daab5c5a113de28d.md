select()  
Wait for any I/O status changes from the file descriptor sets. When any of the specified sets changes, the call returns. You have four macros to help construct and manage the file descriptor sets:

+   - FD_CLR Remove a descriptor from the set.  
+   - FD_SET Add a descriptor to a set.  
+   - FD_ISSET Test if specified descriptor is ready for I/O.  
+   - FD_ZERO Initialize the set to empty.

# Prototype

```
```c
#include <sys/time.h>
#include <sys/types.h>
#include <unistd.h>
int select(int hi_fd, fd_set *readfds, fd_set *writefds,
fd_set *exceptfds, struct timeval *timeout);
FD_CLR(int fd, fd_set *set);
FD_ISSET(int fd, fd_set *set);
FD_SET(int fd, fd_set *set);
FD_ZERO(fd_set *set);
```
```

# Return Value

The number of descriptors that have changed states. If an error occurred, the return value is negative. If the timeout expired, the return value is zero.

# Parameters

| Parameter | Description |
| :--- | :--- |
| hi_fd | This is the highest file descriptor number + 1. For example, if you have four files open plus the stdio, your descriptors could be 0, 1, 2, 3, 5, 6, and 8. The highest is 8. If you include fd(8) in your select statement, hi_fd would equal 9. If the highest fd were 5, this parameter would be 6. |
| readfds | The set of descriptors to test for readability. |
| writefds | The set of descriptors to test for writing. |
| exceptfds | The set of descriptors to test for out-of-band data. |
| timeout | The maximum time to wait for data to arrive in microseconds. This is a pointer to a number. If the number is zero (not the pointer), the call returns immediately after checking all the descriptors. If the pointer is NULL (zero), the select's timeout feature is disabled. |
| fd | The file descriptor to add, remove, or test. |
| set | The file descriptor set. |