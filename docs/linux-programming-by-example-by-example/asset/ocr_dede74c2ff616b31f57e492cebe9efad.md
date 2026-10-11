# Creating and Opening a Queue

The `msgget` function creates a new queue or opens an existing one. Its prototype is as follows:

```
int msgget(key_t key, int flags);
```

If the call is successful, it returns the queue ID of the new or existing queue corresponding to the value contained in `key`. If `key` is `IPC_PRIVATE`, a new queue is created using a key value that the underlying implementation generates; using `IPC_PRIVATE` is guaranteed to create a new queue if system limits on the number of queues or the total number of bytes in all queues are not exceeded.

Similarly, if `key` is not `IPC_PRIVATE` if `key` does not correspond to an existing queue having the same `key`, and if the `IPC_CREAT` bit is set in the `flags` argument, a new queue is created. Otherwise—that is, if `key` is not `IPC_PRIVATE` and if the `IPC_CREAT` bit is not set in `flags`—`msgget` returns the queue ID of the existing queue associated with `key`. If `msgget` fails, it returns -1 and sets the `errno` error variable.

# Example

![](bbox=[0.045, 0.39, 0.09, 0.44])

# Example

The sample program that follows, `mkcq`, creates a new message queue. If you execute it a second time rather than create the specified queue, it simply opens the existing queue.

```
/**
 * mkcq.c – Create a SysV IPC message queue
 */
#include <sys/types.h>
#include <sys/ipc.h>
#include <sys/msg.h>
#include <stdio.h>
#include <stdlib.h>

int main(int argc, char *argv[]) {
    int qid;         /* The queue identifier */
    key_t key;      /* The queue key */

    key = 123;

    /* Create the queue */
    if((qid == msgget(key, IPC_CREAT | 0666)) < 0) {
```