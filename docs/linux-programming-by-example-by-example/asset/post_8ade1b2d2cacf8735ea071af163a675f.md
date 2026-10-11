
stored the typed response (indicated in bold) directly into the msgstructure declared earlier. If msgsnd completes successfully, it displays a message to that effect. Note that qsnd sets the message type to the calling process's PID. This allows you later to retrieve (using msgrcv) only those messages that this process posted.

## Reading Queued Messages

To pull a message off a queue, use msgrcv, which has the syntax listed here:

```c
int msgrcv(int msqid, void *ptr, size_t nbytes, long type, int flags);
```

If it succeeds, msgrcv removes the returned message from the queue. The arguments are the same as msgsnd accepts, except that msgrcv fills in the ptr structure with the message type and up to nbytes of data. The additional argument, type, corresponds to the msg_type member of the msg structure previously discussed. type's value determines which message is returned, as outlined in the following list:

- If type is 0, the first message in the queue (the topmost message) is returned.
- If type is > 0, the first message whose msg_type equals type is returned.
- If type is < 0, the first message whose msg_type is the lowest value less than or equal to type's absolute value is returned.

The value of flags also controls msgrcv's behavior. If the returned message is larger than nbytes, the message is truncated to nbytes if the MSG_NOERROR bit is set in flags (but no notification that the message has been truncated will be generated). Otherwise, msgrcv returns -1 to indicate an error and sets errno to E2BIG. The message also stays on the queue.

If the IPC_NOWAIT bit is set in flags, msgrcv returns immediately and sets errno to ENOMSG if no message of the specified type is available. Otherwise, msgrcv blocks until one of the same conditions described earlier for msgsnd occurs.

> **NOTE**
> A negative value for the type argument can be used to create a LIFO, or last-in, first-out type of queue, often called a stack. Passing a negative value in enables you to retrieve messages of a given type in the reverse order in which they were placed in the queue.

## Example

![](img/be588b36b489136ce784030a08a1d3d4_398_0.png)

The following program, qrd, reads a message off a previously created and populated queue. The queue ID from which to read is passed as a command-line argument.

```c
/*
 * qrd.c - Read all message from a message queue
 */
#include <sys/types.h>
#include <sys/ipc.h>
#include <sys/msg.h>
#include <stdio.h>
#include <stdlib.h>

#define BFSZ 512

struct msg { /* Message structure */
    long msg_type;
    char msg_text[BFSZ];
};

int main(int argc, char *argv[]) {
    int qid; /* The queue identifier */
    int len; /* Length of message */
    struct msg pmsg; /* Pointer to a message structure */

    /* Expect the queue ID passed on the command-line */
    if (argc != 2) {
        puts("USAGE: qrd <queue ID>");
        exit(EXIT_FAILURE);
    }
    qid = atoi(argv[1]);

    /* Retrieve and display a message from the queue */
    len = msgrcv(qid, &pmsg, BFSZ, 0, 0);
    if (len > 0) {
        printf("reading queue id: %05d\n", qid);
        printf("\tmessage type: %05d\n", pmsg.msg_type);
        printf("\tmessage text: %s\n", pmsg.msg_text);
    } else {
        perror("msgrcv");
        exit(EXIT_FAILURE);
    }

    exit(EXIT_SUCCESS);
}
```

The output from one run of this program follows. As before, it uses the queue ID created by `mkq` and also reads the message posted by the `qsnd` example.

![](img/be588b36b489136ce784030a08a1d3d4_400_0.png)

**Output**

```
$ ./mkq
created queue id = 640
opened queue id = 640
$ ./qsnd 640
Enter message to post:
this is test message number one
message posted

$ ./qrd 640
reading queue id: 00640
message type: 14308
    message text: this is test message number one
```

You can see from the code listing that reading from a message queue is easier than writing to one and requires less code. Of particular interest in the sample program is that it fetches the first message off the top of the queue because it passed a `type` of 0. In this case, because the PID of the message writing process is known or can be easily discovered (`14308`), `qrd` could have passed a `type` of 14308 and fetched the same message from the queue.

## Removing Message Queues

The `msgctl` function provides a certain degree of control over message queues. Its prototype is as follows:

```c
int msgctl(int msqid, int cmd, struct msqid_ds *buf);
```

As usual, `msqid` is the queue ID of an existing queue. `cmd` can be one of the following:

- `IPC_RMID` — Removes the queue `msqid`.
- `IPC_STAT` — Fills `buf` with the queue’s `msqid_ds` structure. `IPC_STAT` enables you to peek into a queue’s contents without removing any messages. Because it is a non-destructive read, you could consider it similar to `msgrcv`.
- `IPC_SET` — Allows you to change the queue's UID, GID, access mode, and the maximum number of bytes allowed on the queue.

## Example

![](img/be588b36b489136ce784030a08a1d3d4_401_0.png)

The program that follows uses the `msgctl` call to remove a queue whose ID is passed on the command line.

```c
/*
 * qctl.c - Remove a message queue
 */
#include <sys/types.h>
#include <sys/ipc.h>
#include <sys/msg.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>

int main(int argc, char *argv[])
{
    int qid;
    struct msqid_ds dsbuf;

    if(argc != 2) {
        puts("USAGE: qctl <qid>");
        exit(EXIT_FAILURE);
    }
    qid = atoi(argv[1]);

    if((msgctl(qid, IPC_RMID, NULL)) < 0) {
        perror("msgctl");
        exit(EXIT_FAILURE);
    }

    printf("queue %d removed\n", qid);
    exit(EXIT_SUCCESS);
}
```

## Output

```
$ ./mkq
created queue_id = 1280
opened queue_id = 1280
$ ipcs -q
------- Message Queues -------
key        msqid   owner perms   used-bytes messages
0x0000007b 1280    kwall 666     0          0

$ ./qctl 1280
queue 1280 removed
$ ipcs -q
------- Message Queues -------
key        msqid   owner perms   used-bytes messages

```

The program output shows that the specified queue was deleted. `mkq` creates the queue. The `ipcs` call confirms that the queue was created. Using the queue ID displayed by `mkq`, `qctl` calls `msgctl`, specifying the `IPC_RMID` flag to delete the queue. Running `ipcs` a second time again confirms that `qctl` removed the queue.

The `ipcs` command, used in several of the sample programs, shows the number and status of all System V IPC structures that exist on your system when it executes. The `ipcrm` command will delete the IPC structure whose type and ID is specified on the command line. See the manual pages for more information. Figure 17.2 shows the output of the `ipcs` command.

![](img/be588b36b489136ce784030a08a1d3d4_402_0.png)

Figure 17.2: `ipcs` shows all System V IPC objects that currently exist.

Figure 17.2 shows that at least one of each type of IPC object exists. Three shared memory segments, one message queue, and two semaphores are currently in use (semaphores are discussed in the next section). Each object's key, identifier, owner/creator, and permissions are clearly listed. Statistics relative to each type of object are shown in the last one or two columns of the output, depending on the type of object.

## Semaphores

Semaphores control access to shared resources. They are quite different from the other means of IPC you have seen so far, in that they do not make information available between processes, but instead synchronize access to shared resources that should not be accessed simultaneously. In this respect, semaphore operations more closely resemble file or record locking, but applied to more resources than just files. This section discusses only the simplest type of semaphore, a binary semaphore. A binary semaphore takes one of two values: 0 when a resource is locked and should not be accessed by other processes, and 1 when the resource is unlocked.

- For more information about file and record locking, see "File Locking," page 182.

Semaphores function much like traffic lights at a busy intersection. When a process needs access to a controlled resource, such as a file, it first checks the semaphore value, just as a driver checks to see if a traffic light is green. If the semaphore has a value of zero, which corresponds to a red light, the resource is in use, so the process blocks until the resource becomes available (that is, the semaphore's value becomes non-zero). In the terminology of System V IPC, this blocking is called a wait. If the semaphore has a positive value, which corresponds to a green light at an intersection, the associated resource is available, so the process decrements the semaphore, performs its operations on the resource, and then increments the semaphore to release the "lock."

## Creating a Semaphore

Naturally, before you can increment or decrement a semaphore, it must exist. The function call for creating a new semaphore or accessing an existing one is semget, prototyped in sys/sem.h as follows (you also must include sys/ipc.h and sys/types.h):

```c
int semget(key_t key, int nsems, int flags);
```

semget returns the semaphore identifier associated with a set of nsems semaphores. A new set of semaphores is created if key is IPC_PRIVATE or if key is not already in use and the IPC_CREAT bit is set in flags. As with shared memory segments and message queues, flags can also be bitwise ORed with permission bits (in octal) to set the access modes for the semaphore. Note, however, that semaphores have read and alter permissions rather than read and write permissions. Semaphores use the notion of alter rather than
