# **File Management**

+   *   **lockf** — lock section of file (7.11.3)
+   *   **mkfifo** — make FIFO (7.2.1)
+   *   **mknod** — make file (3.8.2)

# **File System**

+   *   **fstatvfs** — get file system information by file descriptor (3.2.3)
+   *   **mount** — mount file system (nonstandard) (3.2.4)
+   *   **statvfs** — get file system information by path (3.2.3)
+   *   **umount** — unmount file system (nonstandard) (3.2.4)

# **File-Descriptor Set**

+   *   **FD_CLR** — clear fd_set bit (4.2.3)
+   *   **FD_ISSET** — test fd_set bit (4.2.3)
+   *   **FD_SET** — set fd_set bit (4.2.3)
+   *   **FD_ZERO** — clear entire fd_set (4.2.3)

# **IPC—POSIX Message Queue**

+   *   **mq_close** — close message queue (7.7.1)
+   *   **mq_getattr** — get message-queue attributes (7.7.1)
+   *   **mq_notify** — register or unregister for message notification (7.7.1)
+   *   **mq_open** — open message queue (7.7.1)

+   *   **mq_receive** — receive message (7.7.1)
+   *   **mq_send** — send message (7.7.1)
+   *   **mq_setattr** — set message queue attributes (7.7.1)
+   *   **mq_timedreceive** — receive message with timeout (7.7.1)
+   *   **mq_timedsend** — send message with timeout (7.7.1)
+   *   **mq_unlink** — remove message queue (7.7.1)

# **IPC—POSIX Semaphore**

+   *   **sem_close** — close named semaphore (7.10.1)
+   *   **sem_destroy** — destroy unnamed semaphore (7.10.2)
+   *   **sem_getvalue** — get value of semaphore (7.10.1)
+   *   **sem_init** — initialize unnamed semaphore (7.10.2)
+   *   **sem_open** — open named semaphore (7.10.1)
+   *   **sem_post** — increment semaphore (7.10.1)
+   *   **sem_timedwait** — decrement semaphore (7.10.1)
+   *   **sem_trywait** — decrement semaphore if possible (7.10.1)
+   *   **sem_unlink** — remove named semaphore (7.10.1)
+   *   **sem_wait** — decrement semaphore (7.10.1)