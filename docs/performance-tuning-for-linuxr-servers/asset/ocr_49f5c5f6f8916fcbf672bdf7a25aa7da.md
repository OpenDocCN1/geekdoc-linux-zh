# Pipes

Pipes can be shared among multiple readers and writers. Hence, each pipe consists of a FIFO buffer and a list of processes that are blocked to write and read operations. Pipes are not a configurable option in Linux. They are always compiled into the Linux kernel and are implemented as a pseudo-file system. From an application's point of view, pipes are accessed through file descriptors. Hence, the number of pipes that can be created is tied to the number of file descriptors allowed for a process.

Pipes have two important parameters: the pipe buffer size and the size of bytes that can be written atomically.

The pipe buffer size determines how much data can be asynchronous buffered between the writer and the reader. If the pipe buffer is full, data must be read for the writer to continue to write. If operated in blocking mode, writers block.

The pipe buffer size is always fixed to the PAGE_SIZE of the underlying platform. The atomicity is important because pipes can be shared among multiple writers, and guarantees must exist for a writer to send chunks of data as one block. The value is currently set to 4KB or PAGE_SIZE, whichever is smaller.