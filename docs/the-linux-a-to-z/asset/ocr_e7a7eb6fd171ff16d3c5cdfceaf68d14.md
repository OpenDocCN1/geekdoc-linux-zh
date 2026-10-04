Once a FIFO file has been created it can be accessed using just the standard open() system call by any process with appropriate permissions. When open(), a FIFO file has the same basic functionality as an anonymous pipe, i.e. read()s block when the pipe is empty, write()s block when the pipe is full and setting the O_NONBLOCK flag with fcntl() will cause read() and write() to return immediately with an EAGAIN error in situations where they would otherwise have blocked.

Because they can be accessed simultaneously by many unrelated processes, FIFOs are useful in applications where there are multiple readers and/or multiple writers. In this situation there needs to be a rule to determine what happens if two writers try to write to the FIFO at the same time. The rule is that a write() of any number of bytes up to the size of the pipe (4096 bytes in Linux) is guaranteed to be atomic. This means that the data from multiple write() operations will not intermingle in the FIFO but will be maintained as separate messages. Exactly the same rule applies to anonymous pipes, but here it is less useful because they are less often used in these types of application.

# 17.4 System V IPC

In order to provide compatibility with other systems, Linux also provides an option to support the three System V IPC mechanisms: shared memory, messages and semaphores. Each of these has approximately the same kind of interface so we'll just briefly look at one of them – shared memory.

The use of pipes and FIFOs still suffers from one disadvantage and that is the amount of data copying and processor context switching that goes on to transfer the data.

Shared memory overcomes this problem by making the same block of memory simultaneously visible in the address spaces of two or more processes. This means that as soon as one process has written some information into the memory, it is immediately available to the other processes which share this memory block without any further copying operations taking place.

Before any process can attach to a shared memory segment it first needs to be created. This is done with the shmget() call, which has the prototype:

```
#include <sys/ipc.h>
#include <sys/shm.h>

int shmget(key_t key, int size, int flags);
```

where size is the number of bytes required (rounded up to the smallest whole number of memory pages), key is a numeric value (which for a shared memory segment has a similar role to a file's name), and flags is a set of bit masks ORed together to specify access permissions and creation flags when a sheared memory segment is created (rather like a combination of the second and third parameters to an open() system call).