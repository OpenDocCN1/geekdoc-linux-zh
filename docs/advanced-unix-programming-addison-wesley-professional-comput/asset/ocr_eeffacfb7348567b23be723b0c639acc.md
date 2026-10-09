thread run. AIO also helps with synchronized *writes* but doesn't do much for nonsynchronized *writes*, as the buffer cache already does much the same thing.

Don't confuse asynchronous I/O with nonblocking I/O that you specify by setting the **O_NONBLOCK** flag (Sections 2.4.4 and 4.2.2). Nonblocking means that the call returns if it would block, but it doesn't do the work. ¹⁶ Asynchronous means that it initiates the work and then returns.

The AIO functions are part of the Asynchronous Input and Output option, as represented by the **_POSIX_ASYNCHRONOUS_IO** macro. You can test it at run-time with **pathconf**, and I showed example code that does that in Section 1.5.4.

One system call in this section, **lio_listio**, can be used for either synchronous or asynchronous I/O.

# 3.9.2 AIO Control Block

All of the AIO system calls use a control block to keep track of the state of an operation, and different operations have to use distinct control blocks. When an operation is complete, its control block can be reused, of course.

```
```
struct aio cb—AIO control block
struct aio cb {
  int a_i o_fil des; /* file descriptor */
  off_t a_i o_offset; /* file offset */
  volatile void *a_i o_buf; /* buffer */
  size_t a_i o_nbytes; /* size of transfer */
  int a_i o_reqprio; /* request priority offset */
  struct sigevent a_i o_sigevent; /* signal information */
  int a_i o_opcode; /* operation to be performed */
};
```
```

The first four members are like the ones for **pread** and **pwrite** (Section 2.14). That is, the three arguments that **read** or **write** would take plus a file offset for an implicit **lseek**.

The **sigevent** structure is explained fully in Section 9.5.6. With it, you can arrange for a signal to be generated or a thread to be started when the operation is complete. You can pass an arbitrary integer or pointer value to the signal handler or the thread, and usually this will be a pointer to the control block. If you don't