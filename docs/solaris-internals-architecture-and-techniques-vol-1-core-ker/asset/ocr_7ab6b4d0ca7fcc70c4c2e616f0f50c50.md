# 458

# Interprocess Communication

+   - The queue head (mq_headpp), tail (mq_tailpp), and free (mq_freep) points- are set on the message header structure, and mq_init() returns to mq_open(), completing the open process.

Once a queue is established, processes insert and remove messages by using mq_send(3R) and mq_receive(3R).

+   - mq_send(3R) does some up-front tests on the file type (mqd_magic) and tests the mq_notfull semaphore for space on the queue.

+   - If the process's queue flag is set for nonblocking mode, sem_trywait() is called and returns to the semaphore if it is not available, meaning there's no space on the queue.

+   - Otherwise, sem_wait() is called, causing the process to block until space is available.

+   - Once space is available, sem_wait() is called to acquire the mq_exclusive mutex, which protects the queue during insertions and removals.

POSIX message queues offer an interesting feature that is not available with System V message queues: automatic notification to a process or thread when a message has been added to a queue. An mq_notify(3R) interface can be issued by a process that needs to be notified of the arrival of a signal. To continue with the sequence for the next code:

+   - mq_send() checks to determine if a notification has been set up by testing the mq_sigid's an_pid field. If it is non-NULL, the process has requested notification, and a notification signal is sent if no other processes are already blocked, waiting for a message.

+   - Finally, the library's internal mq_putmsg() function is called to locate the next free message block of the free list (mq_freep) and to place the message on the queue.

For receiving messages:

+   - mq_receive() issues a sem_trywait() call on the mq_notempty semaphore.

+   - If the queue is empty and the descriptor is set to non-blocking, sem_trywait() returns with an EAGAIN error to the caller.

+   - Otherwise, the mq_rblocked semaphore is incremented (sem_post), and sem_wait() is called.

+   - Once a message shows up on the queue, the mq_exclusive semaphore is acquired, and the internal mq_getmsg() function is called.

+   - The next message is pulled off the head of the queue, and the pointers are appropriately adjusted.