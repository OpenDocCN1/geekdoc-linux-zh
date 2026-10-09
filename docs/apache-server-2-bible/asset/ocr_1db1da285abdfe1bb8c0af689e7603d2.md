If something goes wrong and the child process dies, only a single request is lost. The number of child processes is controlled using a minimum and maximum setting. When the number of requests increases, new child processes are added until the maximum is reached. Similarly, when the requests fall, any extra child processes are killed.

# The threaded MPM

This MPM enables thread support in Apache 2.0. This is like the prefork MPM, but instead of each child process having a single thread, each child process is allowed to have a specified number of threads. Each thread within a child process can service a different request. If Apache starts 30 child processes where each child is allowed to have at maximum 10 threads, than Apache can service 30 × 10 = 300 requests simultaneously.

If something goes wrong with a thread, for example, an experimental module causes the thread to die, then the entire process dies. This means that all the requests being serviced by the threads within the child process will be lost. However, because requests are distributed among threads on separate child processes, it is likely that a child’s death will take down at maximum of 1/$n$ of all the total connection, where $n$ presents the number of all simultaneous connections.

A process is added or removed by monitoring its spare-thread count. For example, if a process has less than the minimum number of spare threads, a new process is added. Similarly, when a process has a maximum number of idle threads, it killed.

All processes run under the same user and group ID assigned to Apache server.

Because threads are more resource efficient than processes, this MPM is very scalable.

# The perchild MPM

This is also new in Apache 2.0. In this MPM model a set number of child processes are started with a specified number of threads. As request load increases the processes add new threads as needed. When request count reduces, processes shrink their thread counts using a minimum and maximum thread count setting.

The key difference between this module and the threaded MPM is that the process count is static and also each process can run using a different user and group ID. This makes it easy to run different virtual Web sites under different user and group IDs. See Chapter 6 for details.

# The winnt MPM

This is the MPM for the Windows platform, including Windows 2000, Windows NT, and Window 9x. It is a multithreaded module. Using this module Apache will create a parent process and a child process. The child process creates all the threads that