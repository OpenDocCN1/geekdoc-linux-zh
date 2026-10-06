# 762 VI ♦ Programming in Linux

+   * Shared memory —Shared memory is just set aside for what the name suggests: a region or segment of memory specifically set for use by multiple processes. Because shared memory is never paged out to disk, it is an extremely fast for two processes to exchange data.

+   * Semaphores—Semaphores, briefly mentioned in the “Preemptive Multitasking” section, as flags that indicate a condition controlling the behavior of processes. For example, one process can set a semaphore to indicate a specific file is in. Before other processes attempt to access that file, they check the semaphore’s status and (or shouldn’t) attempt to access the file if the flag is set.

+   * Message queues — Message queues are first-in-first-out (FIFO) data structures that make it possible for processes to exchange short messages in a structure, ordered manner.

Message queues are not necessarily accessed. System V UNIX-style message queues are, but POSIX message queues enable readers to pull messages out of a queue in an arbitrary order.

Shared memory, semaphores, and message queues are idiomatic in the Linux development environment. They solve three distinct domains of problems that arise when multiple processes need to exchange data or share resources without having to resort to slow disks files. All of which is to say that you don’t always need IPC, but it sure is nice to have when you do need it.

# The Building Blocks Philosophy

The building blocks philosophy characterizes the Linux development expressed as a series of rules or principles:

+   * Do one thing very well.
* Whenever possible, accept input data from standard input and send output data to standard output.
* Keep individual programs as self-contained as possible.
* Remember that someone will use your program in ways you didn’t intend and for purposes that you never imagined.

The first rule means that programs should not try to be all things to people: a text editor doesn’t need to be able to send e-mails and a drawing program doesn’t also need to be able to function as a browser. Although it is less true today than it used to be, the best Linux programs don’t have every imaginable feature (also known as featuris). Rather, developers spend time perfecting the program’s intended purpose and making it possible for programs to interoperate.