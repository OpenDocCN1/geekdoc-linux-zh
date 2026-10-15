long. As stated in Table 20.2, the following macros are used to manipulate descriptor sets: FD_ZERO(), FD_SET(), FD_CLR(), and FD_ISSET(). Table 20.21 gives the syntax and semantics of these macros. The behavior of these macros is undefined if fd is greater than FD_SETSIZE or less than 0.

The amount of time that select() monitors the descriptor sets is dependent on the value of the timeout argument, as shown in Table 20.22.

The timeval structure is defined in the /usr/include/sys/time.h file as shown next. Thus, a variable of the timeval structure may be used to specify time with microsecond granularity.

```
struct timeval {
    time_t      tv_sec;    /* seconds */
    suseconds_t tv_usec;   /* microseconds */
};
```

The select() call may fail for several reasons. Table 20.23 lists some of the reasons why the accept() call may fail.

The following program illustrates the semantics of the select() system call.
Figure 20.29 shows the algorithm for a single-process connection-oriented concurrent server using the select() system call. Note that this server serves one client request at a time and then moves to serve the request from the next client.

We now discuss the single-process connectionless concurrent server for the TIME and ECHO services using the select() system call. The following session contains the code

# TABLE 20.21 Macros for Manipulating Descriptor Sets

| Macro | Purpose |
|---|---|
| FD_ZERO(fdset) | Initializes the fdset descriptor set to the null set (i.e., all zeros) |
| FD_SET(fd, &fdset) | Includes the given descriptor in the set (i.e., sets the relevant numbered bit to 1) |
| FD_CLR(fd, &fdset) | Excludes the given descriptor from the set (i.e., sets the relevant numbered bit to 0) |
| FD_ISSET(fd, &fdset) | Tests if fd in fdset has a value of 0 or 1. Returns 0 if fd is not set in fdset, nonzero otherwise. It is usually used after the select() call has returned to see if the given descriptor is ready for I/O or exception |

# TABLE 20.22 The Value of the timeout Argument and Its Effect