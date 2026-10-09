
# read()

Read buf_len bytes from the fd file descriptor into the buffer. You can use this system call for sockets as well as files, but this call does not provide as much control as the recv() system call.

## Prototype

```c
#include <unistd.h>
int read(int fd, char *buffer, size_t buf_len);
```

## Return Value

The number of bytes actually read.

## Parameters

| Parameter | Description |
| :--- | :--- |
| fd | File (or socket) descriptor |
| buffer | The memory buffer to accept the read data |
| buf_len | The number of bytes to read and the number of legal bytes in the buffer |

## Possible Errors

- **EINTR**: The call was interrupted by a signal before any data was read.
- **EAGAIN**: Non-blocking I/O has been selected using O_NONBLOCK and no data was immediately available for reading.
- **EIO**: I/O error. This will happen when the process is in a background process group, tries to read from its controlling tty, is either ignoring or blocking SIGTTIN, or its process group is orphaned. It can also occur when there is a low-level I/O error while reading from a disk or tape.
- **EISDIR**: fd refers to a directory.
- **EBADF**: fd is not a valid file descriptor or is not open for reading.
- **EINVAL**: fd is attached to an object that is unsuitable for reading.
- **EFAULT**: buf is outside your accessible address space.

## Example

```c
int sockfd;
int bytes_read;
char buffer[1024];
/*---create socket & connect to server---*/
if ( (bytes_read = read(sockfd, buffer, sizeof(buffer))) < 0 )
    perror("read");
```

# select()

Wait for any I/O status changes from the file descriptor sets. When any of the specified sets changes, the call returns. You have four macros to help construct and manage the file descriptor sets:

- **FD_CLR**: Remove a descriptor from the set.
- **FD_SET**: Add a descriptor to a set.
- **FD_ISSET**: Test if specified descriptor is ready for I/O.
- **FD_ZERO**: Initialize the set to empty.

## Prototype

```c
#include <sys/time.h>
#include <sys/types.h>
#include <unistd.h>
int select(int hi_fd, fd_set *readfds, fd_set *writefds, fd_set *exceptfds, struct timeval *timeout);
FD_CLR(int fd, fd_set *set);
FD_ISSET(int fd, fd_set *set);
FD_SET(int fd, fd_set *set);
FD_ZERO(fd_set *set);
```

## Return Value

The number of descriptors that have changed states. If an error occurred, the return value is negative. If the timeout expired, the return value is zero.

## Parameters

| Parameter | Description |
| --- | --- |
| hi_fd | This is the highest file descriptor number + 1. For example, if you have four files open plus the stdio, your descriptors could be 0, 1, 2, 3, 5, 6, and 8. The highest is 8. If you include fd(8) in your select statement, hi_fd would equal 9. If the highest fd was 5, this parameter would be 6. |
| readfds | The set of descriptors to test for readability. |
| writefds | The set of descriptors to test for writing. |
| exceptfds | The set of descriptors to test for out-of-band data. |
| timeout | The maximum time to wait for data to arrive in microseconds. This is a pointer to a number. If the number is zero (not the pointer), the call returns immediately after checking all the descriptors. If the pointer is NULL (zero), the select's timeout feature is disabled. |
| fd | The file descriptor to add, remove, or test. |
| set | The file descriptor set. |

## Possible Errors

- **EBADF**: An invalid file descriptor was given in one of the sets.
- **EINTR**: A non-blocked signal was caught.
- **EINVAL**: n is negative.
- **ENOMEM**: select was unable to allocate memory for internal tables.

## Example

```c
int i, ports[]={ 9001, 9002, 9004, -1};
int sockfd, max=0;
fd_set set;
struct sockaddr_in addr;
struct timeval Timeout={ 2, 500000} ; /* 2.5 sec. */
FD_ZERO(&set);
bzero(&addr, sizeof(addr));
addr.sin_family = AF_INET;
addr.sin_addr.s_addr = INADDR_ANY;
for ( i = 0; ports[i] > 0; i++ )
{
      sockfd = socket(PF_INET, SOCK_STREAM, 0);
      addr.sin_port = htons(ports[i]);
      if ( bind(sockfd, &addr, sizeof(addr)) != 0)
            perror("bind() failed");
      else
      {
            FD_SET(sockfd, &set);
            if ( max < sockfd )
                 max = sockfd;
      }
}
if ( select(max+1, &set, 0, &set, &timeout) > 0 )
{
      for ( i = 0; i <= max; i++ )
            if ( FD_ISSET(i, &set) )
            {
                 int clicant = accept(i, 0, 0);
                 /**** process the client's requests ****/
            }
}
```

# write()

Write `msg_len` bytes to `fd` field descriptor from `buffer`. You can use a socket descriptor as well, but it does not provide you with as much control as the `send()` system call.

## Prototype

```c
#include <unistd.h>
int write(int fd, const void *buffer, size_t msg_len);
```

## Return Value

Number of bytes written. The byte count can be less than `msg_len`. If the call does not succeed in writing all required bytes, you can use a loop for successive writes. If negative, the call stores the error detail in `errno`.

## Parameters

| Parameter | Description |
| :--- | :--- |
| fd | File descriptor (can be a socket descriptor) |
| buffer | The message to write |
| msg_len | The length of the message |

## Possible Errors

- **EBADF**: fd is not a valid file descriptor or is not open for writing.
- **EINVAL**: buf is attached to an object that is unsuitable for writing.
- **EFAULT**: buf is outside your accessible address space.
- **EPIPE**: fd is connected to a pipe or socket whose reading end is closed. When this happens, the writing process will receive a SIGPIPE signal; if it catches, blocks, or ignores the error, EPIPE is returned.
- **EAGAIN**: Non-blocking I/O has been selected using O_NONBLOCK and there was no room in the pipe or socket connected to fd to write the data immediately.
- **EINTR**: The call was interrupted by a signal before any data was written.
- **ENOSPC**: The device containing the file referred to by fd has no room for the data.
- **EIO**: A low-level I/O error occurred while modifying the inode.

## Example

```c
/**** Write a message (TCP, UDP or Raw) ***/
int sockfd;
int bytes, bytes_wrote=0;
/*--- Create socket, connect to server ---*/
while ( (bytes = write(sockfd, buffer, msg_len)) > 0 )
    if ( (bytes_wrote += bytes) >= msg_len )
        break;
if ( bytes < 0 )
    perror("write");
```

# close()

Closes all descriptors (file or socket). If the socket is connected to a server or client, it requests a close(). The channel actually remains active after the close until the channel empties or times out. Every process has a limit to the number of open descriptors it can have. getdtablesize() returns 1024 in Linux 2.2.14, and the /usr/include/linux/limits.h file defines this limit with NR_OPEN. Also, the first three descriptors default to stdin(0), stdout(1), and stderr(2).

## Prototype

```c
#include <unistd.h>
int close(int fd);
```

## Return Value

Zero if everything goes well. If an error occurs, you can find the cause in errno.

## Parameters

| Parameter | Description |
| :--- | :--- |
| fd | The file or socket descriptor |

## Possible Errors

- **EBADF**: `fd` isn't a valid open file descriptor.

## Example

```c
int sockfd;
sockfd = socket(PF_INET, SOCK_RAW, htons(99));
if ( sockfd < 0 )
    PANIC("Raw socket create failed");
...
if ( close(sockfd) != 0 )
    PANIC("Raw socket close failed");
```

# Appendix D. Object Classes

**IN THIS APPENDIX**

- C++ Exceptions
- C++ Support Classes
- C++ Messaging Classes
- C++ Socket Classes
- Java Exceptions
- Java Support Classes
- Java I/O Classes
- Java Socket Classes

This appendix lists the classes defined in the Java API and the custom C++ library described in the book and on this book’s Web site. Each class has one of three designations: *Class* (a normal class that you can instantiate), *Abstract Class* (a class that defines a skeleton for derived classes), and *Superclass* (an instantiable parent class).

## C++ Exceptions

This section describes the classes for exception classes defined in the book. The hierarchy holds to the philosophy of doing as little as possible so as to minimize the potential of catastrophic class creations.

Figure D.1. The C++ exceptions class hierarchy.

![](img/03334662da8fdfb8d95a02f270c522f6_352_0.png)
