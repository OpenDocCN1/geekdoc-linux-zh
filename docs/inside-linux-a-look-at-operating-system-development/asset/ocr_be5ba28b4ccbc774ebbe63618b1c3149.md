+   • **MEMORY**
+   
+       – brk,sbrk - Change data segment size
+       – shmtcl - Shared memory control
+       – shmgel - Allocates a shared memory segment
+       – sh mop - Shared memory operations
+       – shmat, shmnd - shared memory operations

+   • **PROCESS**
+   
+       – Create/Destroy
+           * _exit - Terminate the current process
+           * fork,vfork - Create a child process
+           * exeve - Execute program
+           * kill - Send signal to a process
+           * killpg - Send signal to a process group
+       – Execution control
+           * alarml - Set an alarm clock for delivery of a signal
+           * idle - Make process idle
+           * getpriority, setpriority - Get/set program scheduling priority
+           * nice - Change process priority
+           * pause - Wait for signal
+           * semctl - Semaphore control operations
+           * semget - Get a semaphore set identifier
+           * semop - Semaphore operations
+           * sigblock,sigmask - Block signals
+           * signal, sigaction, sigsuspnd, sigpendl, sgetmask, ssetmask - Signal handling functions.
+           * sippause - Atomically release blocked signals and wait for interrapt
+           * sigvec - Software signal facilities
+           * wait, waitpid - Wait for process termination