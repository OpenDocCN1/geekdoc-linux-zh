
# 456

# Interprocess Communication

![](img/a86367b95bf21add858c99948ac951c6_501_0.png)

**Figure 10.5** POSIX Message Queue Structures

A POSIX message queue is described by a message queue header, a data structure created and initialized when the message queue is first created. The message queue header contains information on the message queue, as the total size in bytes (mq_totsize), maximum size of each message (mq_maxsz), maximum number of messages allowed on the queue (mq_maxsq), current number of threads waiting to receive messages (mq_waiters), and the current message priority (mq_curmaxprio).

Some attributes are tunable with mq_setattr(3R). The library code sets default values of 128 for the maximum number of messages, 1024 for the maximum size of a single message, and 32 for maximum number of message priorities. If necessary, you can increase the message size and number of messages using mq_setattr(3R), or you can increase them initially when the queue is created, by populating an attributes structure and passing it to the mq_open(3R) call.

The message pointers, mq_headpp and mq_tailpp, in the header do not point directly to the messages on the linked list. They do not contain the address of the message headers. Since the shared mapping can result in the different processes referencing the message queue so that each has a different virtual address within the mapping, mq_headpp and mq_tailpp are implemented as offsets in the shared region.

A message descriptor maintains additional information about the queue, as the file permission flags (read-only or read/write), and the magic number identifying the type of POSIX named object. A structure (mq_dn) maintains per-process flags on the message, allowing different processes to specify either blocking or nonblocking behavior on the message queue files. This is analogous to regular file flags, where a file descriptor for an open file is maintained at the process level, and different processes can have different flags on the same file. (For example, one process could have the file opened for read/write and another process could have the same file opened read-only).

With the big picture in place (Figure 10.5), let's take a look at what happens when a message queue is created and opened.

- When `mq_open()` is entered, it creates the lock file and acquires a file lock. All the message queue uses the `/tmp` directory and follow a file name convention similar to that described in the semaphore section. That is, file names with a prefix—MQD (data file), MQL (lock file), MQP (permission file), or .MQN (file file)—end with the appended file name passed as an argument to `mq_open(3R)` minus the slash character.
- If a new message queue is being created, the maximum message size and messages per queue sizes are set, either with the default values or from a passed attributes to the `mq_open(3R)` call.
    - The permission file is opened, permissions are verified, and the file is closed.
    - The total amount of space needed for messages, based on the limits and structure size, is calculated, and the data file is created, opened, and set to the appropriate size with `ftruncate(3C)`.
- If a new message queue is not being created, an existing queue is being opened, in which case the permission test is done and the queue data file is tested to ensure the queue has been initialized.

The steps described next apply to a new or existing message queue; the latter case is a queue being opened by another process.

- Space for a message queue descriptor is `malloc`d(`mqdes_t`), and the data file is `mmap`d into a shared address space, setting the `mqhp` pointer (Figure 10.5) as the return address from the `mmap(2)` call.
- The message queue descriptor file is created, opened, `mmap`d (also into a shared address space), and closed.
- For new message queues, the `mq_init()` function (not part of the API) is called to complete the initialization process. Each message header has several semaphores (not shown in Figure 10.5) used to synchronize access to the messages, the header structure, and other areas of the queue infrastructure.
- `mq_init()` initializes the semaphores with calls to `sem_init()`, which is part of the libposix4.so library.

- The queue head (mq_headpp), tail (mq_tailpp), and free (mq_freep) points are set on the message header structure, and mq_init() returns to mq_open(), completing the open process.

Once a queue is established, processes insert and remove messages by using mq_send(3R) and mq_receive(3R).

- mq_send(3R) does some up-front tests on the file type (mqd_magic) and tests the mq_notfull semaphore for space on the queue.
- If the process's queue flag is set for nonblocking mode, sem_trywait() is called and returns to the semaphore if it is not available, meaning there's no space on the queue.
- Otherwise, sem_trywait() is called, causing the process to block until space is available.
- Once space is available, the mq_exclusive mutex is acquired, and the mutex protects the queue during insertions and removals.

- POSIX message queues offer an interesting feature not available with System V queues: automatic notification when a message is added. The use of priority mechanism is well documented in the manual pages. Messages with better priorities (larger values) are inserted into the queue before messages of lower priority, so higher-priority messages are kept at the front and will be removed first.

- For receiving messages:
    - mq_receive(3R) issues a sem_trywait() on the mqempty semaphore.
    - If the queue is empty and the descriptor is set to nonblocking, sem_trywait() returns an EAGAIN error to the caller.
    - Otherwise, the mq_blocked semaphore is incremented, and sem_wait() is called. The next message is pulled off the head of the queue, and the pointers are appropriately adjusted.

# 458

# Interprocess Communication

# Solaris Doors

Our description omits some subtle details, mostly around the priority mechanism available for POSIX message queues. Message priority can be specified in the mq_send(3R) and mq_receive(3R) calls. The use and behavior of message priority are well documented in Steven's UNIX Programming—Interprocess Communication [25].

# 10.6 Solaris Doors

Doors provide a facility for systems to issue procedure calls to functions in other processes. Using the APIs, a process can become a door server, exporting a function through a door it creates using the door_create(3X) interface. Other processes can invoke the procedure by issuing a door_call(3X), specifying the door descriptor. Our goal is not to provide a programmer's guide to doors but rather focus on the kernel implementation, data structures, and algorithms. Some discussion of the APIs is, of course, necessary to keep things in context, but we suggest that you refer to the manual pages and Steven's book [25] to understand how to develop applications with doors.

The door APIs were available in Solaris 2.5.1 but not documented and, at that point, subject to change. Solaris 2.6 was the first Solaris release that included a relatively stable set of interfaces (stable in the sense that they were less likely to change). The Solaris kernel ships with a shared object library, libdoor.so, that must be linked to applications using the doors APIs. Table 10-10 describes the door APIs available in Solaris 2.6 and Solaris 7. During the course of our coverage of doors, we refer to the interfaces as necessary for clarity.

Table 10-10 Solaris Doors Interfaces

| Interface | Description |
|---||---|
| door_create(3X) | Creates a door. Called from a door server to associate a procedure within the program with a door descriptor. The door descriptor, returned by door_create(3X), is used by client programs that wish to invoke the procedure. |
| door_revoke(3X) | Revokes access to the door. Can only be called by the server. |
| door_call(3X) | Invokes a function exported as a door. Called from a client process. |
