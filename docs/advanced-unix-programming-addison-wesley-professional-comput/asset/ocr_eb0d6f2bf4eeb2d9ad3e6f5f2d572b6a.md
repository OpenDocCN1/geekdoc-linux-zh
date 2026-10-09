owner, group, and other bits with the effective user- and group-IDs is that same as with files.

Also, if O_CREAT is specified and a queue is created and the attr argument is non-NULL, two attributes, `mq_maxms g` and `mq_msgsize` are set from the supplied `mq_attr` structure. These are the maximum number of messages that the queue can hold and the maximum size for an individual message. The standard doesn't specify a limit for either attribute, but if there's insufficient space `mq_open` will return -1 with `errno` set to `ENOSPC`. Most implementations will implement the queue with a linked list, so `mq_open` won't run out of space regardless of the numbers because a new queue is empty. If the `attr` argument is `NULL`, the two attributes are set to implementation-defined values.

If your eyes glazed over reading the previous few paragraphs and you go ahead assuming `mq_open` is just like `open`, you'll probably be just fine as long as you don't assume it returns a file descriptor.

You close an open message queue with `mq_close`: 

```
```
# include <mqueue.h>

int mq_close(
   mqd_t mqd                /* message-queue descriptor */
);
/* Returns zero on success or -1 on error (sets errno) */
```
```

As with System V message queues, POSIX message queues persist until they're removed or the kernel is rebooted. You remove a POSIX message queue with a call that's like `unlink`: 

```
```
# include <mqueue.h>

int mq_unlink(
   const char *name          /* POSIX IPC name */
);
/* Returns 0 on success or -1 on error (sets errno) */
```
```

Like `unlink`, `mq_unlink` makes the name disappear right away, but actual destruction of the queue is postponed until all open message-queue descriptors are closed. (Recall that with System V message queues, removing a queue with `msgctl` was immediate and potentially disruptive.) So, if you want to, once all