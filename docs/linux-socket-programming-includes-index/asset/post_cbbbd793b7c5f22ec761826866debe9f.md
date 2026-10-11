
# Asynchronous Writes

You program the asynchronous write a bit differently because of the kernel’s buffers. When your program first calls `send()`, it’s likely that the kernel’s buffers can store the entire data block. But it’s also possible that it can’t, and the kernel caches only a part.

So, check the return value of every `write()` to make sure that all the data gets sent. It may even be essential for you to keep all outgoing data for a channel in a single queue. This reduces the code complexity involved with multiple buffers. Still, making the buffering flexible is important as well, so that the queue may grow and shrink as needed.

A database query example serves well in this situation. It generates lots of data that can be processed or gathered while sending the reply, as shown in Listing 8.5.

### LISTING 8.5 Asynchronous Writer Algorithm

```c
/***** Database Query Async Writer Example: process query ***/
/** while generating results. `*/
/*******...*******/
int ready=0, bytes, size=0, pos=0;
...
int sig_io(int sig)
{
    if ( size > 0 )
    {
        bytes = send(client, buffer, size+pos, 0);
        if ( bytes > 0 )
        {
            pos += bytes;
            ready = 1;
        }
    }
}
...
```

### LISTING 8.5 Continued

```c
/**** Enable nonblocking, signal-driven I/O; claim SIGIO ***/
while ( !done )
{
    if ( /*** channel available ***/ )
        /*** Send message, no blocking ***/
    else
        /*** queue message ***/
}
...
```

Every time the channel clears and is ready for more data, the kernel sends the process a SIGIO signal. Use that signal as shown in the previous example to funnel data out in an on-demand way.

# On-Demand Connections

You can create an on-demand connection server (theoretically). Essentially it looks like an on-demand reader, but instead of reading a file, the program calls `accept()`. The handler needs three global variables to communicate with the main loop: the socket acceptor (`sd`), an array of descriptors, and the current number of connections. Any local variable your signal handler creates is lost at the end of the handler.

The handler might look like this:

```c
/***** On-Demand Connection Example:  Make connection in ***/
/*** signal handler.  Main loop cycles through each open ***/
/*** socket for messages. (Excerpt from damedom-accept.c ***/
/*** on CD.)
...
int Connections[MAXCONNECTIONS];
int sd, NumConnections=0;
void sig_io(int sig)
{
    int client;

    /*** Accept connection.  If too many, error & close ***/
    if ( !(client = accept(sd, 0, 0)) > 0 )
    {
        if ( NumConnections < MAXCONNECTIONS )
            Connections[NumConnections++] = client;
        else
        {
            send(client, "Too many connections\n", 22, 0);
            close(client);
        }
    }
    else
        perror("Accept");
}
...
```

While an on-demand server is useful, the clear advantage of multitasking is that it allows you to retain the local variables, and it sets aside a specific task for each connection.

Unless your server is prone to task-overload (the program creates so many processes that the performance drops), using on-demand connections may encumber your programming. For all the effort in designing and implementing an on-demand connection server, you probably won't get the same bang for the buck. It's simply easier to use either the multitasking or polling technique.

## Solving Unwanted I/O Blocking with `poll()` and `select()`

Linux offers two tools to help you work with multiple open channels at the same time. These tools are more efficient (and may be easier to implement) than manual polling. The whole idea behind each tool is that the system call blocks until any channel changes state.

A state change includes conditions such as data being available to read, a channel is clear for writing, or an error occurred. Upon return, one or many of the channels may have changed state. The return value from the call represents the number of channels that changed.

However, the `select()` system call is a little more complex and involves several macros to help manage the descriptor lists:

```c
#include <sys/time.h>
#include <sys/types.h>
#include <unistd.h>
int select(int maxfd, fd_set *to_read, fd_set *to_write, fd_set *except, struct timeval *timeout);

FD_CLR(int fd, fd_set *set);            /* remove fd from set */
FD_ISSET(int fd, fd_set *set);          /* check if fd is in set */
FD_SET(int fd, fd_set *set);            /* add fd to set */
FD_ZERO(fd_set *set);                   /* initialize set for use */
```

The main routine is the `select()` system call. It has several helper macros (`FD_CLR()`, `FD_ISSET()`, `FD_SET()`, `FD_ZERO()`) to manage the descriptor lists. The parameters are defined in Table 8.3.

# The Server Perspective and Load Control

# PART II

### TABLE 8.3 Parameters for the `select()` System Call

| Parameter | Description |
| :--- | :--- |
| *maxfd* | One more than the highest-numbered file descriptor in the set. (See below for more.) |
| *to_read* | The set of descriptors that await reading. This is the set that you want to test for reading. |
| *to_write* | The set of descriptors that await writing. |
| *except* | The set of descriptors that await priority messages. |
| *timeout* | The time in microseconds to wait before giving up. (See below for more details.) |
| *fd* | The file descriptor to add, delete, or test for. |
| *set* | The set of descriptors to manipulate. |

The `maxfd` parameter is the highest-numbered descriptor slot in any of the three sets plus 1. Each task gets a number of I/O descriptor slots (typically 1024). Each I/O channel occupies a slot (`stdin` is 0, `stdout` is 1, and `stderr` is 2). If the sets had descriptors `[3,6]` in `to_read`, `[4,5,6]` in `to_write`, and `[3,4]` in `except`, `maxfd` becomes 6 (the highest descriptor number) plus 1, or 7.

The `timeout` parameter gives you the flexibility of setting a limit to how long the system call waits:

- If `NULL`, wait indefinitely.
- If positive, wait the specified microseconds.
- If zero, return immediately after checking all descriptors once.

For example, if you had three channels open to clients numbered `[3,4,6]`, you could wait for them to send the program data like this:

```c
/*  ************************************  */
/*  Select() Example.              ***  */
/*  ************************************  */
int count;
fd_set set;
struct timeval timeout;
...
FD_ZERO(&set);               /* Clear set */
FD_SET(3, &set);             /* Add client channel #3 */
FD_SET(4, &set);             /* Add client channel #4 */
FD_SET(6, &set);             /* Add client channel #6 */

timeout.tv_sec = 5;          /* Timeout after 5.25 seconds */
timeout.tv_usec = 250000;

/*--- Wait for select() ---*/
if ( (count = select(6+1, &set, 0, 0, &timeout)) > 0 )
    /*** Find the descriptors that changed ****/
else if ( count == 0 )
    fprintf(stderr, "Timed out!");
else
    perror("Select");
...
```

In this example, when the `select()` system call returns with a positive value, one of the three channels has data to read. To find out which channel is ready, add the code nested and read in the data. However, if the return value is zero, the call exceeded the 5.25-second time limit.

The `poll()` system call is similar to `select()` and may be a little easier to manage. It uses an array of structures to define the behavior:

```c
struct pollfd
{
    int fd;        /* the descriptor to test */
    short events;  /* requested events to watch */
    short revents; /* events that fired */
};
```

The first field, `fd`, is the file or socket descriptor. The second and third fields, `events` and `revents`, are bit masks for specific events:

- `POLLERR`: Any error condition. Return if any error occurs on channel.
- `POLLHUP`: Hang-up on other end. Return if peer hangs up.
- `POLLIN`: Incoming data. Return if data ready for reading.
- `POLLINVAL`: `fd` not open. Return if the channel is not an open file or socket.
- `POLLPRI`: Priority messages. Return if a priority message arrives.
- `POLLOUT`: Channel availability. Return if a `write()` won't block.

The system call to `poll()` looks like this:

```c
#include <sys/poll.h>
int poll(struct pollfd *list, unsigned int cnt, int timeout);
```

The program fills an array of `pollfd` structures before it uses this system call. The `cnt` parameter is the number of legal socket descriptors in the array. (Remember to keep these descriptors contiguous; if one closes, compress the array. Not all implementations deal well with an empty slot.) The `timeout` parameter acts like the `select()` timeout but in milliseconds.
