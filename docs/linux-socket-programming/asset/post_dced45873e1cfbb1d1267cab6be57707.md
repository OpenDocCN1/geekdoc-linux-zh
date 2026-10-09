
## Select() Example

```c
/*****************************************/
/***  Select() Example.             ***/
/*****************************************/
int count;
fd_set set;
struct timeval timeout;


FD_ZERO(&set);                          /*  Clear set  */
FD_SET(3, &set);                        /*  Add client channel #3  */
FD_SET(4, &set);                        /*  Add client channel #4  */
FD_SET(6, &set);                        /*  Add client channel #6  */
timeout.tv_sec = 5;                     /*  Timeout after 5.25 seconds  */
timeout.tv_usec = 250000;
/****  Wait for select()  ----*/
if ( (count = select(6+1, &set, 0, 0, &timeout)) > 0 )
    /****  Find the descriptors that changed ****/
else if ( count == 0 )
      fprintf(stderr, "Timed out!");
else
      perror("Select");
...
```

In this example, when the `select()` system call returns with a positive value, one of the three channels has data to read. To find out which channel is ready, add the code needed and read in the data. However, if the return value is zero, the call exceeded the 5.25-second time limit.

The `poll()` system call is similar to `select()` and may be a little easier to manage. It uses an array of structures to define the behavior:

```c
struct pollfd
{
    int fd;          /*  the descriptor to test  */
    short events;   /*  requested events to watch  */
    short revents;  /*  events that fired  */
} ;
```

The first field, `fd`, is the file or socket descriptor. The second and third fields, `events` and `revents`, are bit masks for specific events:

-   `POLLERR` Any error condition. Return if any error occurs on channel.
-   `POLLHUP` Hang-up on other end. Return if peer hangs up.
-   `POLLIN` Incoming data. Return if data ready for reading.
-   `POLLNVAL` `fd` not open. Return if the channel is not an open file or socket.
-   `POLLPRI` Priority messages. Return if a priority message arrives.
-   `POLLOUT` Channel availability. Return if a `write()` won't block.

The system call to `poll()` looks like this:

```c
#include <sys/poll.h>
int poll(struct pollfd *list, unsigned int cnt, int timeout);
```

The program fills an array of `pollfd` structures before it uses this system call. The `cnt` parameter is the number of legal socket descriptors in the array. (Remember to keep these descriptors contiguous; if one closes, compress the array. Not all implementations deal well with an empty slot.) The `timeout` parameter acts like the `select()` timeout but in milliseconds.

Either the `select()` or the `poll()` system calls provide the power to monitor several channels at the same time. With good planning, you can avoid some of the overhead problems multitasking encounters.

## Implementing Timeouts

A simple alternative to polling I/O channels is to tell the operating system that you do not want to wait longer than a specified time. The Linux system calls do not provide a direct way of doing this. Consider using these ways to implement timeouts:

-   With the timeout in the `select()` or `poll()` system call
-   With a signal (`SIGALRM`) to wake up the task

### NOTE

Linux Socket Timeout Support

The socket options include timeouts for sending (`SO_SNDTIMEO`) and receiving (`SO_RCVTIMEO`). Unfortunately, these parameters are read-only for now; on Linux, they default to `OFF`. If you try to port some code that uses these parameters, you may have to use the other two methods.

The `select()` and `poll()` system calls (described previously) supply a timeout parameter in microseconds. Using these system calls is perhaps the easiest way to implement timeouts, but the timeouts apply to all channels in the call.

This situation can be a problem: Suppose you have three channels, and one of them is not very responsive. Using just these system calls, you cannot detect that the failing channel should have timed out and closed. You can manually keep individual times for each channel, resetting the time with each response. Still, that may be a lot of unnecessary checking and logging.

You can use an alternative instead: an `alarm` signal. An `alarm` is a clock that runs in the kernel. When the `alarm` goes off, the kernel sends a `wakeup` call to the task in the form of a `signal`. If the task is waiting in a `system` call, the `signal` interrupts the call, the task enters the `signal` handler, and then the `system` call returns with an `EINTR` error.

Every task can send itself a `signal`, but the task needs to know what to do with the `signal`. On some systems, the `sleep` library call uses the `alarm()` system call, first setting up the task to capture the `SIGALRM` `signal`. Please look at the following `example`:

```c
/********************************************************************/
/** Example: Timeout example using the alarm() system **/
/** call. (Except from echo-timeout.c on CD.) **/
/********************************************************************/
...
int sig_alarm(int sig)
{ /** do nothing **/}
...
void reader()
{    struct sigaction act;
/*--- Initialize signal structure; reset to default ---*/
 bzero(&act, sizeof(act));
 act.sa_handler = sig_alarm;
 act.sa_flags = SA_ONESHOT;
 /*--- Set the signal handler ---*/
 if ( sigaction(SIGALRM, &act, 0) != 0 )
       perror("Could not set up timeout");
 else
   /*--- If signal handler installed, set timer ---*/
   alarm(TIMEOUT_SEC);
 /*--- Call the I/O that might timeout ---*/
 if ( recv(sd, buffer, sizeof(buffer), 0) < 0 )
   {
       if ( errno == EINTR )
           perror("Timed-out!");
   }
}
```

The example shown sets up the signal handler, sets the timer, and calls the I/O. If `recv()` gets no data by the time the timer expires, the task gets a signal. The signal interrupts the `recv()` system call, and the system call returns with an error (`EINTR`).

To get this behavior, leave off the `SA_RESTART` option from the `sa_flags` field. Chapter 7 advises you to include this option with signals. In that case, omit this option for the timeout timer to work.

One final note: Avoid using the `alarm()` system call with `sleep()`, because it can cause problems in your program. Instead, use the Linux `SIGALRM` signal or use `sleep()` – don’t mix them.

## Summary: Choosing the I/O Techniques

The network program interacts with other programs through the network. Since the performance and response times vary from machine to machine and network to network, it’s important to know when and how to use nonblocking I/O to improve the I/O management in your clients and servers.

Used carefully and properly balanced, blocking and nonblocking I/O increases your client’s and server’s responsiveness to the user.

This chapter covered several topics on blocking (what it is, when it’s useful, why it’s used) and nonblocking (what are the different types, when to use them, how to use them). It discussed the main tool to select nonblocking I/O: the `fcntl()` system call.

The two primary nonblocking tools are polling and asynchronous I/O. Polling repeatedly tries to use an I/O system call. Asynchronous (or signal-driven) I/O places the burden on the kernel to determine when a channel is free. Polling focuses on the I/O, while signal-driven I/O focuses on local processing.

Another tool to manage blocking is a timeout. You can deploy timeouts in the `select()` or `poll()` system call or use a timer signal that wakes up the process when a call takes too long.

## Chapter 9. Breaking Performance Barriers

### IN THIS CHAPTER

- Creating the Servlets Before the Client Arrives
- Extending Control with a Smart Select
- Delving Deeper into Socket Control
- Recovering the Socket Descriptor
- Sending Before Received: Message Interleave
- Noting File I/O Problems
- Using Demand-Based I/O to Recover CPU Time
- Sending High-Priority Messages
- Summary: Pulling Together Performance Features

How do you get everything out of your server or client? Linux has several tools in the Sockets API that make this process relatively straightforward. However, you have to look at the programming problem from several angles at the same time, because each aspect touches on and affects another.

Your network program has three distinct aspects: the task, the connection, and the messages. You work with each one of these in the course of the program. The task involves working with all related processes, or threads. The connection is the socket itself and its behavior, and the messages interact with the I/O processing that receives and sends messages. To get the most out of your network program, you have to balance the tasks with the messaging. The socket enables you to specialize the connection to meet your needs.

This chapter takes you through several ideas and best practices that address the task, connection and messaging. You need to know the concepts presented in previous chapters to fully use these algorithms.

## Creating the Servlets Before the Client Arrives

To this point you have seen how to create a server, implement multitasking, and control I/O blocking. Each of these building blocks helps you interact with your clients and control the throughput. Chapter 7, "Dividing the Load: Multitasking," showed you how to delegate the task of accepting and serving incoming connections, creating child processes as you need them.

On some systems, however, creating a new task each time consumes time and resources. Also, you may not want to dedicate the entire computer resources to just serving network clients. (On the other hand, you may want to do just that, but there are logical and effective limits you must place on server access to ensure performance.) You may have other programs that need to execute on a regular basis, or even local/remote logins. In any form, you need to control the growth of your server program. And, controlling the number of connections requires extra programming.

### Placing a Cap on the Number of Client Connections

If you recall from the previous chapters, the server creates a new child process as soon as the client connects. Your program has to change here to incorporate the control over too many processes (once called rabbit processes because they multiply too quickly to control). The standard algorithm that follows does just that.

```c
/***********************/
```
