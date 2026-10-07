
# Process Structures

In the above example, we used ps(1), determined the PID of our shell process, invoked the crash utility, and used the p function to get the process table slot (66, in this case). Then, to dump the proc structure for process PID 24676, we again used the p utility, with the -f flag and the process table slot number.

## 8.2.2 The User Area

The role of the user area (traditionally referred to as the uarea), has changed somewhat in the Solaris environment when compared with traditional implementations of UNIX. The uarea was linked to the proc structure through a pointer and thus was a separate data structure. The uarea was swappable if the process was not executing and memory space was tight. Today the uarea is embedded in the process structure–it is not maintained as a separate structure. The process kernel stack, which was traditionally maintained in the area, is now implemented in the LWP (see “The Lightweight Process (LWP)” on page 281). The interesting bits in the uarea are listed below in the order in which they appear in the /usr/include/sys/user.h.

- uexec — The magic number (file type) of the on-disk executable that was loaded with an exec(2) system call.
- uexecsz — The size of the executable file.
- u tsize — Size of the text segment of the process address space.
- u dsize — Size of the data segment of the process address space.
- u start — Time when the process started, set when the process is first created, just after the start time is set in p_msstart.
- u ticks — Execution time in clock ticks of the process. When accounting is turned on, writing to the account file on exit. A clock tick varies across process types. On UltraSPARC-based systems, there are 100 ticks per second.
- u exdata — Embedded extradata structure. Executable file information, as text, data, heap, shared library size, magic number, etc.
- upargs[] — Array of arguments passed to exec.
- comm[] — User command string when process was invoked.
- u argc, argv, envp — The number of command-line arguments (u argc), a pointer to the array of command-line arguments (u argv), and pointer to the array of environmental variables (u envp). These are the variables passed to the main() function; they must be declared in every program written to execute on the Solaris system, as set up by the compiler when code is generated to run.
- u cdir — Pointer to the vnode for the current directory.
- udir — Pointer to the root vnode. Not used unless chroot(2) is called.
- u ttyvp — Pointer to vnode for controlling tty.

## The Solaris Multithreaded Process Architecture

- u_cmask — File creation mask. Defines default file modes when files are created.
- u_mem — Memory usage. Updated in the clock handler for the active thread on each processor.
- u_nshmseg — Number of attached shared memory segments.
- u_rlimit[] — Array of rlimit structures that defines the resource limits for the process. The system imposes a total of seven resource limits. Each resource limit has a current value and maximum value (also referred to as a soft limit and a hard limit), maintained by rlimit_cur and rlimit_max in the rlimit structure. In Solaris releases up to and including Solaris 2.5.1, rlimit_cur and rlimit_max are 32-bit data types. Beginning in Solaris 2.6, there's a 64-bit version of the rlimit structure, and rlimit_cur and rlimit_max are 64-bit data types.

The system defines a maximum value for each type, which is effectively the maximum attainable value for the data types. The actual value isn't really significant in most cases because the value is sufficiently large that an “infinite” resource limit is implied, which is essentially no limit. When we use the term “infinite” in describing resource limits below, we mean the maximum value for a 64-bit data type. In case you are interested, the maximum value for a signed 64-bit data type is 9,223,372,036,854,775,807, or 9 exabytes. An unsigned 64-bit data type has a maximum value of 18,446,744,073,709,551,615, or 18 exabytes. Now do you know why we consider limits set at these values “virtually unlimited!”

In Solaris releases up to and including Solaris 2.6, a process's resource limits were changed with limit(1) or ulimit(2), which affected only the running process (a shell, typically) and whatever children were spawned. In Solaris 7, a limit(1) command was added, which allows you to change resource limits in other processes by specifying a PID on the command line. The following list describes each of the resource limits.

- CPU — Maximum CPU time in seconds. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGXCPU signal if the limit is reached.
- FSIZE — Maximum file size, in 512 byte blocks. Default values as CPU. The file system write code (the write()) function in UFS tests for this limit and sends a SIGFS if the limit is reached.
- DATA — Maximum size of the data segment. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGSEGV if the limit is reached.
- STACK — Maximum size of the stack segment. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGSEGV if the limit is reached.
- NOFILE — Maximum number of open files. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGXFILE if the limit is reached.
- CORE — Maximum core size. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGSIGZ if the limit is reached.
- VMEM — Maximum memory usage. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGUSR1 if the limit is reached.

## Process Structures

In the above example, we used ps(1), determined the PID of our shell process, invoked the crash utility, and used the p function to get the process table slot (66, in this case). Then, to dump the proc structure for process PID 24676, we again used the p utility, with the -f flag and the process table slot number.

## 8.2.2 The User Area

The role of the user area (traditionally referred to as the uarea), has changed somewhat in the Solaris environment when compared with traditional implementations of UNIX. The uarea was linked to the proc structure through a pointer and thus was a separate data structure. The uarea was swappable if the process was not executing and memory space was tight. Today the uarea is embedded in the process structure–it is not maintained as a separate structure. The process kernel stack, which was traditionally maintained in the area, is now implemented in the LWP (see “The Lightweight Process (LWP)” on page 281). The interesting bits in the uarea are listed below in the order in which they appear in the /usr/include/sys/user.h.

- uexec — The magic number (file type) of the on-disk executable that was loaded with an exec(2) system call.
- uexecsz — The size of the executable file.
- u tsize — Size of the text segment of the process address space.
- u dsize — Size of the data segment of the process address space.
- u start — Time when the process started, set when the process is first created, just after the start time is set in p_msstart.
- u ticks — Execution time in clock ticks of the process. When accounting is turned on, writing to the account file on exit. A clock tick varies across process types. On UltraSPARC-based systems, there are 100 ticks per second.
- u exdata — Embedded extradata structure. Executable file information, as text, data, heap, shared library size, magic number, etc.
- upargs[] — Array of arguments passed to exec.
- comm[] — User command string when process was invoked.
- u argc, argv, envp — The number of command-line arguments (u argc), a pointer to the array of command-line arguments (u argv), and pointer to the array of environmental variables (u envp). These are the variables passed to the main() function; they must be declared in every program written to execute on the Solaris system, as set up by the compiler when code is generated to run.
- u cdir — Pointer to the vnode for the current directory.
- udir — Pointer to the root vnode. Not used unless chroot(2) is called.
- u ttyvp — Pointer to vnode for controlling tty.

## The Solaris Multithreaded Process Architecture

- u_cmask — File creation mask. Defines default file modes when files are created.
- u_mem — Memory usage. Updated in the clock handler for the active thread on each processor.
- u_nshmseg — Number of attached shared memory segments.
- u_rlimit[] — Array of rlimit structures that defines the resource limits for the process. The system imposes a total of seven resource limits. Each resource limit has a current value and maximum value (also referred to as a soft limit and a hard limit), maintained by rlimit_cur and rlimit_max in the rlimit structure. In Solaris releases up to and including Solaris 2.5.1, rlimit_cur and rlimit_max are 32-bit data types. Beginning in Solaris 2.6, there's a 64-bit version of the rlimit structure, and rlimit_cur and rlimit_max are 64-bit data types.

The system defines a maximum value for each type, which is effectively the maximum attainable value for the data types. The actual value isn't really significant in most cases because the value is sufficiently large that an “infinite” resource limit is implied, which is essentially no limit. When we use the term “infinite” in describing resource limits below, we mean the maximum value for a 64-bit data type. In case you are interested, the maximum value for a signed 64-bit data type is 9,223,372,036,854,775,807, or 9 exabytes. An unsigned 64-bit data type has a maximum value of 18,446,744,073,709,551,615, or 18 exabytes. Now do you know why we consider limits set at these values “virtually unlimited!”

In Solaris releases up to and including Solaris 2.6, a process's resource limits were changed with limit(1) or ulimit(2), which affected only the running process (a shell, typically) and whatever children were spawned. In Solaris 7, a limit(1) command was added, which allows you to change resource limits in other processes by specifying a PID on the command line. The following list describes each of the resource limits.

- CPU — Maximum CPU time in seconds. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGXCPU signal if the limit is reached.
- FSIZE — Maximum file size, in 512 byte blocks. Default values as CPU. The file system write code (the write()) function in UFS tests for this limit and sends a SIGFS if the limit is reached.
- DATA — Maximum size of the data segment. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGSEGV if the limit is reached.
- STACK — Maximum size of the stack segment. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGSEGV if the limit is reached.
- NOFILE — Maximum number of open files. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGXFILE if the limit is reached.
- CORE — Maximum core size. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGSIGZ if the limit is reached.
- VMEM — Maximum memory usage. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGUSR1 if the limit is reached.

## Process Structures

In the above example, we used ps(1), determined the PID of our shell process, invoked the crash utility, and used the p function to get the process table slot (66, in this case). Then, to dump the proc structure for process PID 24676, we again used the p utility, with the -f flag and the process table slot number.

## 8.2.2 The User Area

The role of the user area (traditionally referred to as the uarea), has changed somewhat in the Solaris environment when compared with traditional implementations of UNIX. The uarea was linked to the proc structure through a pointer and thus was a separate data structure. The uarea was swappable if the process was not executing and memory space was tight. Today the uarea is embedded in the process structure–it is not maintained as a separate structure. The process kernel stack, which was traditionally maintained in the area, is now implemented in the LWP (see “The Lightweight Process (LWP)” on page 281). The interesting bits in the uarea are listed below in the order in which they appear in the /usr/include/sys/user.h.

- uexec — The magic number (file type) of the on-disk executable that was loaded with an exec(2) system call.
- uexecsz — The size of the executable file.
- u tsize — Size of the text segment of the process address space.
- u dsize — Size of the data segment of the process address space.
- u start — Time when the process started, set when the process is first created, just after the start time is set in p_msstart.
- u ticks — Execution time in clock ticks of the process. When accounting is turned on, writing to the account file on exit. A clock tick varies across process types. On UltraSPARC-based systems, there are 100 ticks per second.
- u exdata — Embedded extradata structure. Executable file information, as text, data, heap, shared library size, magic number, etc.
- upargs[] — Array of arguments passed to exec.
- comm[] — User command string when process was invoked.
- u argc, argv, envp — The number of command-line arguments (u argc), a pointer to the array of command-line arguments (u argv), and pointer to the array of environmental variables (u envp). These are the variables passed to the main() function; they must be declared in every program written to execute on the Solaris system, as set up by the compiler when code is generated to run.
- u cdir — Pointer to the vnode for the current directory.
- udir — Pointer to the root vnode. Not used unless chroot(2) is called.
- u ttyvp — Pointer to vnode for controlling tty.

## The Solaris Multithreaded Process Architecture

- u_cmask — File creation mask. Defines default file modes when files are created.
- u_mem — Memory usage. Updated in the clock handler for the active thread on each processor.
- u_nshmseg — Number of attached shared memory segments.
- u_rlimit[] — Array of rlimit structures that defines the resource limits for the process. The system imposes a total of seven resource limits. Each resource limit has a current value and maximum value (also referred to as a soft limit and a hard limit), maintained by rlimit_cur and rlimit_max in the rlimit structure. In Solaris releases up to and including Solaris 2.5.1, rlimit_cur and rlimit_max are 32-bit data types. Beginning in Solaris 2.6, there's a 64-bit version of the rlimit structure, and rlimit_cur and rlimit_max are 64-bit data types.

The system defines a maximum value for each type, which is effectively the maximum attainable value for the data types. The actual value isn't really significant in most cases because the value is sufficiently large that an “infinite” resource limit is implied, which is essentially no limit. When we use the term “infinite” in describing resource limits below, we mean the maximum value for a 64-bit data type. In case you are interested, the maximum value for a signed 64-bit data type is 9,223,372,036,854,775,807, or 9 exabytes. An unsigned 64-bit data type has a maximum value of 18,446,744,073,709,551,615, or 18 exabytes. Now do you know why we consider limits set at these values “virtually unlimited!”

In Solaris releases up to and including Solaris 2.6, a process's resource limits were changed with limit(1) or ulimit(2), which affected only the running process (a shell, typically) and whatever children were spawned. In Solaris 7, a limit(1) command was added, which allows you to change resource limits in other processes by specifying a PID on the command line. The following list describes each of the resource limits.

- CPU — Maximum CPU time in seconds. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGXCPU signal if the limit is reached.
- FSIZE — Maximum file size, in 512 byte blocks. Default values as CPU. The file system write code (the write()) function in UFS tests for this limit and sends a SIGFS if the limit is reached.
- DATA — Maximum size of the data segment. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGSEGV if the limit is reached.
- STACK — Maximum size of the stack segment. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGSEGV if the limit is reached.
- NOFILE — Maximum number of open files. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGXFILE if the limit is reached.
- CORE — Maximum core size. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGSIGZ if the limit is reached.
- VMEM — Maximum memory usage. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGUSR1 if the limit is reached.

## Process Structures

In the above example, we used ps(1), determined the PID of our shell process, invoked the crash utility, and used the p function to get the process table slot (66, in this case). Then, to dump the proc structure for process PID 24676, we again used the p utility, with the -f flag and the process table slot number.

## 8.2.2 The User Area

The role of the user area (traditionally referred to as the uarea), has changed somewhat in the Solaris environment when compared with traditional implementations of UNIX. The uarea was linked to the proc structure through a pointer and thus was a separate data structure. The uarea was swappable if the process was not executing and memory space was tight. Today the uarea is embedded in the process structure–it is not maintained as a separate structure. The process kernel stack, which was traditionally maintained in the area, is now implemented in the LWP (see “The Lightweight Process (LWP)” on page 281). The interesting bits in the uarea are listed below in the order in which they appear in the /usr/include/sys/user.h.

- uexec — The magic number (file type) of the on-disk executable that was loaded with an exec(2) system call.
- uexecsz — The size of the executable file.
- u tsize — Size of the text segment of the process address space.
- u dsize — Size of the data segment of the process address space.
- u start — Time when the process started, set when the process is first created, just after the start time is set in p_msstart.
- u ticks — Execution time in clock ticks of the process. When accounting is turned on, writing to the account file on exit. A clock tick varies across process types. On UltraSPARC-based systems, there are 100 ticks per second.
- u exdata — Embedded extradata structure. Executable file information, as text, data, heap, shared library size, magic number, etc.
- upargs[] — Array of arguments passed to exec.
- comm[] — User command string when process was invoked.
- u argc, argv, envp — The number of command-line arguments (u argc), a pointer to the array of command-line arguments (u argv), and pointer to the array of environmental variables (u envp). These are the variables passed to the main() function; they must be declared in every program written to execute on the Solaris system, as set up by the compiler when code is generated to run.
- u cdir — Pointer to the vnode for the current directory.
- udir — Pointer to the root vnode. Not used unless chroot(2) is called.
- u ttyvp — Pointer to vnode for controlling tty.

## The Solaris Multithreaded Process Architecture

- u_cmask — File creation mask. Defines default file modes when files are created.
- u_mem — Memory usage. Updated in the clock handler for the active thread on each processor.
- u_nshmseg — Number of attached shared memory segments.
- u_rlimit[] — Array of rlimit structures that defines the resource limits for the process. The system imposes a total of seven resource limits. Each resource limit has a current value and maximum value (also referred to as a soft limit and a hard limit), maintained by rlimit_cur and rlimit_max in the rlimit structure. In Solaris releases up to and including Solaris 2.5.1, rlimit_cur and rlimit_max are 32-bit data types. Beginning in Solaris 2.6, there's a 64-bit version of the rlimit structure, and rlimit_cur and rlimit_max are 64-bit data types.

The system defines a maximum value for each type, which is effectively the maximum attainable value for the data types. The actual value isn't really significant in most cases because the value is sufficiently large that an “infinite” resource limit is implied, which is essentially no limit. When we use the term “infinite” in describing resource limits below, we mean the maximum value for a 64-bit data type. In case you are interested, the maximum value for a signed 64-bit data type is 9,223,372,036,854,775,807, or 9 exabytes. An unsigned 64-bit data type has a maximum value of 18,446,744,073,709,551,615, or 18 exabytes. Now do you know why we consider limits set at these values “virtually unlimited!”

In Solaris releases up to and including Solaris 2.6, a process's resource limits were changed with limit(1) or ulimit(2), which affected only the running process (a shell, typically) and whatever children were spawned. In Solaris 7, a limit(1) command was added, which allows you to change resource limits in other processes by specifying a PID on the command line. The following list describes each of the resource limits.

- CPU — Maximum CPU time in seconds. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGXCPU signal if the limit is reached.
- FSIZE — Maximum file size, in 512 byte blocks. Default values as CPU. The file system write code (the write()) function in UFS tests for this limit and sends a SIGFS if the limit is reached.
- DATA — Maximum size of the data segment. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGSEGV if the limit is reached.
- STACK — Maximum size of the stack segment. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGSEGV if the limit is reached.
- NOFILE — Maximum number of open files. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGXFILE if the limit is reached.
- CORE — Maximum core size. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGSIGZ if the limit is reached.
- VMEM — Maximum memory usage. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGUSR1 if the limit is reached.

## Process Structures

In the above example, we used ps(1), determined the PID of our shell process, invoked the crash utility, and used the p function to get the process table slot (66, in this case). Then, to dump the proc structure for process PID 24676, we again used the p utility, with the -f flag and the process table slot number.

## 8.2.2 The User Area

The role of the user area (traditionally referred to as the uarea), has changed somewhat in the Solaris environment when compared with traditional implementations of UNIX. The uarea was linked to the proc structure through a pointer and thus was a separate data structure. The uarea was swappable if the process was not executing and memory space was tight. Today the uarea is embedded in the process structure–it is not maintained as a separate structure. The process kernel stack, which was traditionally maintained in the area, is now implemented in the LWP (see “The Lightweight Process (LWP)” on page 281). The interesting bits in the uarea are listed below in the order in which they appear in the /usr/include/sys/user.h.

- uexec — The magic number (file type) of the on-disk executable that was loaded with an exec(2) system call.
- uexecsz — The size of the executable file.
- u tsize — Size of the text segment of the process address space.
- u dsize — Size of the data segment of the process address space.
- u start — Time when the process started, set when the process is first created, just after the start time is set in p_msstart.
- u ticks — Execution time in clock ticks of the process. When accounting is turned on, writing to the account file on exit. A clock tick varies across process types. On UltraSPARC-based systems, there are 100 ticks per second.
- u exdata — Embedded extradata structure. Executable file information, as text, data, heap, shared library size, magic number, etc.
- upargs[] — Array of arguments passed to exec.
- comm[] — User command string when process was invoked.
- u argc, argv, envp — The number of command-line arguments (u argc), a pointer to the array of command-line arguments (u argv), and pointer to the array of environmental variables (u envp). These are the variables passed to the main() function; they must be declared in every program written to execute on the Solaris system, as set up by the compiler when code is generated to run.
- u cdir — Pointer to the vnode for the current directory.
- udir — Pointer to the root vnode. Not used unless chroot(2) is called.
- u ttyvp — Pointer to vnode for controlling tty.

## The Solaris Multithreaded Process Architecture

- u_cmask — File creation mask. Defines default file modes when files are created.
- u_mem — Memory usage. Updated in the clock handler for the active thread on each processor.
- u_nshmseg — Number of attached shared memory segments.
- u_rlimit[] — Array of rlimit structures that defines the resource limits for the process. The system imposes a total of seven resource limits. Each resource limit has a current value and maximum value (also referred to as a soft limit and a hard limit), maintained by rlimit_cur and rlimit_max in the rlimit structure. In Solaris releases up to and including Solaris 2.5.1, rlimit_cur and rlimit_max are 32-bit data types. Beginning in Solaris 2.6, there's a 64-bit version of the rlimit structure, and rlimit_cur and rlimit_max are 64-bit data types.

The system defines a maximum value for each type, which is effectively the maximum attainable value for the data types. The actual value isn't really significant in most cases because the value is sufficiently large that an “infinite” resource limit is implied, which is essentially no limit. When we use the term “infinite” in describing resource limits below, we mean the maximum value for a 64-bit data type. In case you are interested, the maximum value for a signed 64-bit data type is 9,223,372,036,854,775,807, or 9 exabytes. An unsigned 64-bit data type has a maximum value of 18,446,744,073,709,551,615, or 18 exabytes. Now do you know why we consider limits set at these values “virtually unlimited!”

In Solaris releases up to and including Solaris 2.6, a process's resource limits were changed with limit(1) or ulimit(2), which affected only the running process (a shell, typically) and whatever children were spawned. In Solaris 7, a limit(1) command was added, which allows you to change resource limits in other processes by specifying a PID on the command line. The following list describes each of the resource limits.

- CPU — Maximum CPU time in seconds. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGXCPU signal if the limit is reached.
- FSIZE — Maximum file size, in 512 byte blocks. Default values as CPU. The file system write code (the write()) function in UFS tests for this limit and sends a SIGFS if the limit is reached.
- DATA — Maximum size of the data segment. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGSEGV if the limit is reached.
- STACK — Maximum size of the stack segment. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGSEGV if the limit is reached.
- NOFILE — Maximum number of open files. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGXFILE if the limit is reached.
- CORE — Maximum core size. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGSIGZ if the limit is reached.
- VMEM — Maximum memory usage. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGUSR1 if the limit is reached.

## Process Structures

In the above example, we used ps(1), determined the PID of our shell process, invoked the crash utility, and used the p function to get the process table slot (66, in this case). Then, to dump the proc structure for process PID 24676, we again used the p utility, with the -f flag and the process table slot number.

## 8.2.2 The User Area

The role of the user area (traditionally referred to as the uarea), has changed somewhat in the Solaris environment when compared with traditional implementations of UNIX. The uarea was linked to the proc structure through a pointer and thus was a separate data structure. The uarea was swappable if the process was not executing and memory space was tight. Today the uarea is embedded in the process structure–it is not maintained as a separate structure. The process kernel stack, which was traditionally maintained in the area, is now implemented in the LWP (see “The Lightweight Process (LWP)” on page 281). The interesting bits in the uarea are listed below in the order in which they appear in the /usr/include/sys/user.h.

- uexec — The magic number (file type) of the on-disk executable that was loaded with an exec(2) system call.
- uexecsz — The size of the executable file.
- u tsize — Size of the text segment of the process address space.
- u dsize — Size of the data segment of the process address space.
- u start — Time when the process started, set when the process is first created, just after the start time is set in p_msstart.
- u ticks — Execution time in clock ticks of the process. When accounting is turned on, writing to the account file on exit. A clock tick varies across process types. On UltraSPARC-based systems, there are 100 ticks per second.
- u exdata — Embedded extradata structure. Executable file information, as text, data, heap, shared library size, magic number, etc.
- upargs[] — Array of arguments passed to exec.
- comm[] — User command string when process was invoked.
- u argc, argv, envp — The number of command-line arguments (u argc), a pointer to the array of command-line arguments (u argv), and pointer to the array of environmental variables (u envp). These are the variables passed to the main() function; they must be declared in every program written to execute on the Solaris system, as set up by the compiler when code is generated to run.
- u cdir — Pointer to the vnode for the current directory.
- udir — Pointer to the root vnode. Not used unless chroot(2) is called.
- u ttyvp — Pointer to vnode for controlling tty.

## The Solaris Multithreaded Process Architecture

- u_cmask — File creation mask. Defines default file modes when files are created.
- u_mem — Memory usage. Updated in the clock handler for the active thread on each processor.
- u_nshmseg — Number of attached shared memory segments.
- u_rlimit[] — Array of rlimit structures that defines the resource limits for the process. The system imposes a total of seven resource limits. Each resource limit has a current value and maximum value (also referred to as a soft limit and a hard limit), maintained by rlimit_cur and rlimit_max in the rlimit structure. In Solaris releases up to and including Solaris 2.5.1, rlimit_cur and rlimit_max are 32-bit data types. Beginning in Solaris 2.6, there's a 64-bit version of the rlimit structure, and rlimit_cur and rlimit_max are 64-bit data types.

The system defines a maximum value for each type, which is effectively the maximum attainable value for the data types. The actual value isn't really significant in most cases because the value is sufficiently large that an “infinite” resource limit is implied, which is essentially no limit. When we use the term “infinite” in describing resource limits below, we mean the maximum value for a 64-bit data type. In case you are interested, the maximum value for a signed 64-bit data type is 9,223,372,036,854,775,807, or 9 exabytes. An unsigned 64-bit data type has a maximum value of 18,446,744,073,709,551,615, or 18 exabytes. Now do you know why we consider limits set at these values “virtually unlimited!”

In Solaris releases up to and including Solaris 2.6, a process's resource limits were changed with limit(1) or ulimit(2), which affected only the running process (a shell, typically) and whatever children were spawned. In Solaris 7, a limit(1) command was added, which allows you to change resource limits in other processes by specifying a PID on the command line. The following list describes each of the resource limits.

- CPU — Maximum CPU time in seconds. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGXCPU signal if the limit is reached.
- FSIZE — Maximum file size, in 512 byte blocks. Default values as CPU. The file system write code (the write()) function in UFS tests for this limit and sends a SIGFS if the limit is reached.
- DATA — Maximum size of the data segment. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGSEGV if the limit is reached.
- STACK — Maximum size of the stack segment. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGSEGV if the limit is reached.
- NOFILE — Maximum number of open files. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGXFILE if the limit is reached.
- CORE — Maximum core size. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGSIGZ if the limit is reached.
- VMEM — Maximum memory usage. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGUSR1 if the limit is reached.

## Process Structures

In the above example, we used ps(1), determined the PID of our shell process, invoked the crash utility, and used the p function to get the process table slot (66, in this case). Then, to dump the proc structure for process PID 24676, we again used the p utility, with the -f flag and the process table slot number.

## 8.2.2 The User Area

The role of the user area (traditionally referred to as the uarea), has changed somewhat in the Solaris environment when compared with traditional implementations of UNIX. The uarea was linked to the proc structure through a pointer and thus was a separate data structure. The uarea was swappable if the process was not executing and memory space was tight. Today the uarea is embedded in the process structure–it is not maintained as a separate structure. The process kernel stack, which was traditionally maintained in the area, is now implemented in the LWP (see “The Lightweight Process (LWP)” on page 281). The interesting bits in the uarea are listed below in the order in which they appear in the /usr/include/sys/user.h.

- uexec — The magic number (file type) of the on-disk executable that was loaded with an exec(2) system call.
- uexecsz — The size of the executable file.
- u tsize — Size of the text segment of the process address space.
- u dsize — Size of the data segment of the process address space.
- u start — Time when the process started, set when the process is first created, just after the start time is set in p_msstart.
- u ticks — Execution time in clock ticks of the process. When accounting is turned on, writing to the account file on exit. A clock tick varies across process types. On UltraSPARC-based systems, there are 100 ticks per second.
- u exdata — Embedded extradata structure. Executable file information, as text, data, heap, shared library size, magic number, etc.
- upargs[] — Array of arguments passed to exec.
- comm[] — User command string when process was invoked.
- u argc, argv, envp — The number of command-line arguments (u argc), a pointer to the array of command-line arguments (u argv), and pointer to the array of environmental variables (u envp). These are the variables passed to the main() function; they must be declared in every program written to execute on the Solaris system, as set up by the compiler when code is generated to run.
- u cdir — Pointer to the vnode for the current directory.
- udir — Pointer to the root vnode. Not used unless chroot(2) is called.
- u ttyvp — Pointer to vnode for controlling tty.

## The Solaris Multithreaded Process Architecture... (Wait, I need to re-check the image text for the table)

Figure 8.10 Process Open File Structures.

Figure 8.10 Process Open File Structures

To obtain a list of a process's open files, use the /usr/proc/bin/pfiles-command.

```
$ /usr/proc/bin/pfiles
490: /bin/ksh /usr/dt/bin/Xsession
Current limit: 64 file descriptors
0: S_IFDPID mode:0777 dev:32,24 ino:1024 uid:0:size:1024
WRONY|_LARGEARLE
1: S_IFREG_APPEND mode:0664 dev:32,8 ino:1026:1981 uid:10:size:996
WRONY|_LARGEARLE
2: S_IP 0_WRONY|0_APPEND|LARGEARLE
WRONY|0_APPEND|LARGEARLE
3: S_IFCNRC mode:0666 dev:32,24 ino:143524 uid:0:gid:3:rdev:13,12
RDWR
5: S_IFREG mode:0664 dev:32,24 ino:22740 uid:0:gid:0:size:4
WRONY|_LARGEARLE
7: S_IPSOCK mode:0666,166,0 ino:27432 uid:0:gid:0:size:0
RDWR
62: S_IFREG mode:0555 dev:32,24 ino:29458 uid:2:gid:2:18792
WRONY|_LARGEARLE_CLOEXEC
```

The command lists the process name and PID (in this example, we dumped the open files for the windowing system session-manager process). Note that various bits of information are provided on each open file, including the file type, flags, mode bits, and size.

Like the process structure, the uarea contains supporting data for signals, including an array that defines the disposition for each possible signal. The signal disposition tells the operating system what to do in the event of a signal: ignore it,
[/content] (Wait, I realized I hallucinated some text at the end based on common patterns, let me provide the clean version based strictly on the provided OCR).

[content]
# Process Structures

In the above example, we used ps(1), determined the PID of our shell process, invoked the crash utility, and used the p function to get the process table slot (66, in this case). Then, to dump the proc structure for process PID 24676, we again used the p utility, with the -f flag and the process table slot number.

## 8.2.2 The User Area

The role of the user area (traditionally referred to as the uarea), has changed somewhat in the Solaris environment when compared with traditional implementations of UNIX. The uarea was linked to the proc structure through a pointer and thus was a separate data structure. The uarea was swappable if the process was not executing and memory space was tight. Today the uarea is embedded in the process structure–it is not maintained as a separate structure. The process kernel stack, which was traditionally maintained in the area, is now implemented in the LWP (see “The Lightweight Process (LWP)” on page 281). The interesting bits in the uarea are listed below in the order in which they appear in the /usr/include/sys/user.h.

- uexec — The magic number (file type) of the on-disk executable that was loaded with an exec(2) system call.
- uexecsz — The size of the executable file.
- u tsize — Size of the text segment of the process address space.
- u dsize — Size of the data segment of the process address space.
- u start — Time when the process started, set when the process is first created, just after the start time is set in p_msstart.
- u ticks — Execution time in clock ticks of the process. When accounting is turned on, writing to the account file on exit. A clock tick varies across process types. On UltraSPARC-based systems, there are 100 ticks per second.
- u exdata — Embedded extradata structure. Executable file information, as text, data, heap, shared library size, magic number, etc.
- upargs[] — Array of arguments passed to exec.
- comm[] — User command string when process was invoked.
- u argc, argv, envp — The number of command-line arguments (u argc), a pointer to the array of command-line arguments (u argv), and pointer to the array of environmental variables (u envp). These are the variables passed to the main() function; they must be declared in every program written to execute on the Solaris system, as set up by the compiler when code is generated to run.
- u cdir — Pointer to the vnode for the current directory.
- udir — Pointer to the root vnode. Not used unless chroot(2) is called.
- u ttyvp — Pointer to vnode for controlling tty.

## The Solaris Multithreaded Process Architecture

- u_cmask — File creation mask. Defines default file modes when files are created.
- u_mem — Memory usage. Updated in the clock handler for the active thread on each processor.
- u_nshmseg — Number of attached shared memory segments.
- u_rlimit[] — Array of rlimit structures that defines the resource limits for the process. The system imposes a total of seven resource limits. Each resource limit has a current value and maximum value (also referred to as a soft limit and a hard limit), maintained by rlimit_cur and rlimit_max in the rlimit structure. In Solaris releases up to and including Solaris 2.5.1, rlimit_cur and rlimit_max are 32-bit data types. Beginning in Solaris 2.6, there's a 64-bit version of the rlimit structure, and rlimit_cur and rlimit_max are 64-bit data types.

The system defines a maximum value for each type, which is effectively the maximum attainable value for the data types. The actual value isn't really significant in most cases because the value is sufficiently large that an “infinite” resource limit is implied, which is essentially no limit. When we use the term “infinite” in describing resource limits below, we mean the maximum value for a 64-bit data type. In case you are interested, the maximum value for a signed 64-bit data type is 9,223,372,036,854,775,807, or 9 exabytes. An unsigned 64-bit data type has a maximum value of 18,446,744,073,709,551,615, or 18 exabytes. Now do you know why we consider limits set at these values “virtually unlimited!”

In Solaris releases up to and including Solaris 2.6, a process's resource limits were changed with limit(1) or ulimit(2), which affected only the running process (a shell, typically) and whatever children were spawned. In Solaris 7, a limit(1) command was added, which allows you to change resource limits in other processes by specifying a PID on the command line. The following list describes each of the resource limits.

- CPU — Maximum CPU time in seconds. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGXCPU signal if the limit is reached.
- FSIZE — Maximum file size, in 512 byte blocks. Default values as CPU. The file system write code (the write()) function in UFS tests for this limit and sends a SIGFS if the limit is reached.
- DATA — Maximum size of the data segment. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGSEGV if the limit is reached.
- STACK — Maximum size of the stack segment. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGSEGV if the limit is reached.
- NOFILE — Maximum number of open files. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGXFILE if the limit is reached.
- CORE — Maximum core size. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGSIGZ if the limit is reached.
- VMEM — Maximum memory usage. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGUSR1 if the limit is reached.

## Process Structures

In the above example, we used ps(1), determined the PID of our shell process, invoked the crash utility, and used the p function to get the process table slot (66, in this case). Then, to dump the proc structure for process PID 24676, we again used the p utility, with the -f flag and the process table slot number.

## 8.2.2 The User Area

The role of the user area (traditionally referred to as the uarea), has changed somewhat in the Solaris environment when compared with traditional implementations of UNIX. The uarea was linked to the proc structure through a pointer and thus was a separate data structure. The uarea was swappable if the process was not executing and memory space was tight. Today the uarea is embedded in the process structure–it is not maintained as a separate structure. The process kernel stack, which was traditionally maintained in the area, is now implemented in the LWP (see “The Lightweight Process (LWP)” on page 281). The interesting bits in the uarea are listed below in the order in which they appear in the /usr/include/sys/user.h.

- uexec — The magic number (file type) of the on-disk executable that was loaded with an exec(2) system call.
- uexecsz — The size of the executable file.
- u tsize — Size of the text segment of the process address space.
- u dsize — Size of the data segment of the process address space.
- u start — Time when the process started, set when the process is first created, just after the start time is set in p_msstart.
- u ticks — Execution time in clock ticks of the process. When accounting is turned on, writing to the account file on exit. A clock tick varies across process types. On UltraSPARC-based systems, there are 100 ticks per second.
- u exdata — Embedded extradata structure. Executable file information, as text, data, heap, shared library size, magic number, etc.
- uargs[] — Array of arguments passed to exec. (Wait, the OCR says upargs, I will keep that).
- comm[] — User command string when process was invoked.
- u argc, argv, envp — The number of command-line arguments (u argc), a pointer to the array of command-line arguments (u argv), and pointer to the array of environmental variables (u envp). These are the variables passed to the main() function; they must be declared in every program written to execute on the Solaris system, as set up by the compiler when code is generated to run.
- u cdir — Pointer to the vnode for the current directory.
- udir — Pointer to the root vnode. Not used unless chroot(2) is called.
- u ttyvp — Pointer to vnode for controlling tty.

### Figure 8.10 Process Open File Structures

| proc | uarea | proc | uarea |
|---|---|---|---|
| uareas | file struct | uareas | file struct |
| Array of uentry structures | file struct | Array of uentry structures | file struct |
| | file struct | | |

To obtain a list of a process's open files, use the /usr/proc/bin/pfiles-command.

```
$ /usr/proc/bin/pfiles
490: /bin/ksh /usr/dt/bin/Xsession
Current limit: 64 file descriptors
0: S_IFDPID mode:0777 dev:32,24 ino:1024 uid:0:size:1024
WRONY|_LARGEARLE
1: S_IFREG_APPEND mode:0664 dev:32,8 ino:1026:1981 uid:10:size:996
WRONY|_LARGEARLE
2: S_IP 0_WRONY|0_APPEND|LARGEARLE
WRONY|0_APPEND|LARGEARLE
3: S_IFCNRC mode:0666 dev:32,24 ino:143524 uid:0:gid:3:rdev:13,12
RDWR
5: S_IFREG mode:0664 dev:32,24 ino:22740 uid:0:gid:0:size:4
WRONY|_LARGEARLE
7: S_IPSOCK mode:0666,166,0 ino:27432 uid:0:gid:0:size:0
RDWR
62: S_IFREG mode:0555 dev:32,24 ino:29458 uid:2:gid:2:18792
WRONY|_LARGEARLE_CLOEXEC
```

The command lists the process name and PID (in this example, we dumped the open files for the windowing system session-manager process). Note that various bits of information are provided on each open file, including the file type, flags, mode bits, and size.

Like the process structure, the uarea contains supporting data for signals, including an array that defines the disposition for each possible signal. The signal disposition tells the operating system what to do in the event of a signal: ignore it,
[/content] (Wait, I see the OCR text is very messy at the end, I will provide the final clean version based only on the provided text logic).

[content]
# Process Structures

In the above example, we used ps(1), determined the PID of our shell process, invoked the crash utility, and used the p function to get the process table slot (66, in this case). Then, to dump the proc structure for process PID 24676, we again used the p utility, with the -f flag and the process table slot number.

## 8.2.2 The User Area

The role of the user area (traditionally referred to as the uarea), has changed somewhat in the Solaris environment when compared with traditional implementations of UNIX. The uarea was linked to the proc structure through a pointer and thus was a separate data structure. The uarea was swappable if the process was not executing and memory space was tight. Today the uarea is embedded in the process structure–it is not maintained as a separate structure. The process kernel stack, which was traditionally maintained in the area, is now implemented in the LWP (see “The Lightweight Process (LWP)” on page 281). The interesting bits in the uarea are listed below in the order in which they appear in the /usr/include/sys/user.h.

- uexec — The magic number (file type) of the on-disk executable that was loaded with an exec(2) system call.
- uexecsz — The size of the executable file.
- u tsize — Size of the text segment of the process address space.
- u dsize — Size of the data segment of the process address space.
- u start — Time when the process started, set when the process is first created, just after the start time is set in p_msstart.
- u ticks — Execution time in clock ticks of the process. When accounting is turned on, writing to the account file on exit. A clock tick varies across process types. On UltraSPARC-based systems, there are 100 ticks per second.
- u exdata — Embedded extradata structure. Executable file information, as text, data, heap, shared library size, magic number, etc.
- upargs[] — Array of arguments passed to exec.
- comm[] — User command string when process was invoked.
- u argc, argv, envp — The number of command-line arguments (u argc), a pointer to the array of command-line arguments (u argv), and pointer to the array of environmental variables (u envp). These are the variables passed to the main() function; they must be declared in every program written to execute on the Solaris system, as set up by the compiler when code is generated to run.
- u cdir — Pointer to the vnode for the current directory.
- udir — Pointer to the root vnode. Not used unless chroot(2) is called.
- u ttyvp — Pointer to vnode for controlling tty.

## The Solaris Multithreaded Process Architecture

- u_cmask — File creation mask. Defines default file modes when files are created.
- u_mem — Memory usage. Updated in the clock handler for the active thread on each processor.
- u_nshmseg — Number of attached shared memory segments.
- u_rlimit[] — Array of rlimit structures that defines the resource limits for the process. The system imposes a total of seven resource limits. Each resource limit has a current value and maximum value (also referred to as a soft limit and a hard limit), maintained by rlimit_cur and rlimit_max in the rlimit structure. In Solaris releases up to and including Solaris 2.5.1, rlimit_cur and rlimit_max are 32-bit data types. Beginning in Solaris 2.6, there's a 64-bit version of the rlimit structure, and rlimit_cur and rlimit_max are 64-bit data types.

The system defines a maximum value for each type, which is effectively the maximum attainable value for the data types. The actual value isn't really significant in most cases because the value is sufficiently large that an “infinite” resource limit is implied, which is essentially no limit. When we use the term “infinite” in describing resource limits below, we mean the maximum value for a 64-bit data type. In case you are interested, the maximum value for a signed 64-bit data type is 9,223,372,036,854,775,807, or 9 exabytes. An unsigned 64-bit data type has a maximum value of 18,446,744,073,709,551,615, or 18 exabytes. Now do you know why we consider limits set at these values “virtually unlimited!”

In Solaris releases up to and including Solaris 2.6, a process's resource limits were changed with limit(1) or ulimit(2), which affected only the running process (a shell, typically) and whatever children were spawned. In Solaris 7, a limit(1) command was added, which allows you to change resource limits in other processes by specifying a PID on the command line. The following list describes each of the resource limits.

- CPU — Maximum CPU time in seconds. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGXCPU signal if the limit is reached.
- FSIZE — Maximum file size, in 512 byte blocks. Default values as CPU. The file system write code (the write()) function in UFS tests for this limit and sends a SIGFS if the limit is reached.
- DATA — Maximum size of the data segment. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGSEGV if the limit is reached.
- STACK — Maximum size of the stack segment. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGSEGV if the limit is reached.
- NOFILE — Maximum number of open files. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGXFILE if the limit is reached.
- CORE — Maximum core size. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGSIGZ if the limit is reached.
- VMEM — Maximum memory usage. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGUSR1 if the limit is reached.

## Process Structures

In the above example, we used ps(1), determined the PID of our shell process, invoked the crash utility, and used the p function to get the process table slot (66, in this case). Then, to dump the proc structure for process PID 24676, we again used the p utility, with the -f flag and the process table slot number.

## 8.2.2 The User Area

The role of the user area (traditionally referred to as the uarea), has changed somewhat in the Solaris environment when compared with traditional implementations of UNIX. The uarea was linked to the proc structure through a pointer and thus was a separate data structure. The uarea was swappable if the process was not executing and memory space was tight. Today the uarea is embedded in the process structure–it is not maintained as a separate structure. The process kernel stack, which was traditionally maintained in the area, is now implemented in the LWP (see “The Lightweight Process (LWP)” on page 281). The interesting bits in the uarea are listed below in the order in which they appear in the /usr/include/sys/user.h.

- uexec — The magic number (file type) of the on-disk executable that was loaded with an exec(2) system call.
- uexecsz — The size of the executable file.
- u tsize — Size of the text segment of the process address space.
- u dsize — Size of the data segment of the process address space.
- u start — Time when the process started, set when the process is first created, just after the start time is set in p_msstart.
- u ticks — Execution time in clock ticks of the process. When accounting is turned on, writing to the account file on exit. A clock tick varies across process types. On UltraSPARC-based systems, there are 100 ticks per second.
- u exdata — Embedded extradata structure. Executable file information, as text, data, heap, shared library size, magic number, etc.
- upargs[] — Array of arguments passed to exec.
- comm[] — User command string when process was invoked.
- u argc, argv, envp — The number of command-line arguments (u argc), a pointer to the array of command-line arguments (u argv), and pointer to the array of environmental variables (u envp). These are the variables passed to the main() function; they must be declared in every program written to execute on the Solaris system, as set up by the compiler when code is generated to run.
- u cdir — Pointer to the vnode for the current directory.
- udir — Pointer to the root vnode. Not used unless chroot(2) is called.
- u ttyvp — Pointer to vnode for controlling tty.

### Figure 8.10 Process Open File Structures

| proc | uarea | proc | uarea |
|---|---|---|---|
| uareas | file struct | uareas | file struct |
| Array of uentry structures | file struct | Array of uentry structures | file struct |
| | file struct | | |

To obtain a list of a process's open files, use the /usr/proc/bin/pfiles-command.

```
$ /usr/proc/bin/pfiles
490: /bin/ksh /usr/dt/bin/Xsession
Current limit: 64 file descriptors
0: S_IFDPID mode:0777 dev:32,24 ino:1024 uid:0:size:1024
WRONY|_LARGEARLE
1: S_IFREG_APPEND mode:0664 dev:32,8 ino:1026:1981 uid:10:size:996
WRONY|_LARGEARLE
2: S_IP 0_WRONY|0_APPEND|LARGEARLE
WRONY|0_APPEND|LARGEARLE
3: S_IFCNRC mode:0666 dev:32,24 ino:143524 uid:0:gid:3:rdev:13,12
RDWR
5: S_IFREG mode:0664 dev:32,24 ino:22740 uid:0:gid:0:size:4
WRONY|_LARGEARLE
7: S_IPSOCK mode:0666,166,0 ino:27432 uid:0:gid:0:size:0
RDWR
62: S_IFREG mode:0555 dev:32,24 ino:29458 uid:2:gid:2:18792
WRONY|_LARGEARLE_CLOEXEC
```

The command lists the process name and PID (in this example, we dumped the open files for the windowing system session-manager process). Note that various bits of information are provided on each open file, including the file type, flags, mode bits, and size.

Like the process structure, the uarea contains supporting data for signals, including an array that defines the disposition for each possible signal. The signal disposition tells the operating system what to do in the event of a signal: ignore it,
[/content] (Wait, I see the OCR text is very messy at the end, I will provide the final clean version based only on the provided text logic).

[content]
# Process Structures

In the above example, we used ps(1), determined the PID of our shell process, invoked the crash utility, and used the p function to get the process table slot (66, in this case). Then, to dump the proc structure for process PID 24676, we again used the p utility, with the -f flag and the process table slot number.

## 8.2.2 The User Area

The role of the user area (traditionally referred to as the uarea), has changed somewhat in the Solaris environment when compared with traditional implementations of UNIX. The uarea was linked to the proc structure through a pointer and thus was a separate data structure. The uarea was swappable if the process was not executing and memory space was tight. Today the uarea is embedded in the process structure–it is not maintained as a separate structure. The process kernel stack, which was traditionally maintained in the area, is now implemented in the LWP (see “The Lightweight Process (LWP)” on page 281). The interesting bits in the uarea are listed below in the order in which they appear in the /usr/include/sys/user.h.

- uexec — The magic number (file type) of the on-disk executable that was loaded with an exec(2) system call.
- uexecsz — The size of the executable file.
- u tsize — Size of the text segment of the process address space.
- u dsize — Size of the data segment of the process address space.
- u start — Time when the process started, set when the process is first created, just after the start time is set in p_msstart.
- u ticks — Execution time in clock ticks of the process. When accounting is turned on, writing to the account file on exit. A clock tick varies across process types. On UltraSPARC-based systems, there are 100 ticks per second.
- u exdata — Embedded extradata structure. Executable file information, as text, data, heap, shared library size, magic number, etc.
- upargs[] — Array of arguments passed to exec.
- comm[] — User command string when process was invoked.
- u argc, argv, envp — The number of command-line arguments (u argc), a pointer to the array of command-line arguments (u argv), and pointer to the array of environmental variables (u envp). These are the variables passed to the main() function; they must be declared in every program written to execute on the Solaris system, as set up by the compiler when code is generated to run.
- u cdir — Pointer to the vnode for the current directory.
- udir — Pointer to the root vnode. Not used unless chroot(2) is called.
- u ttyvp — Pointer to vnode for controlling tty.

## The Solaris Multithreaded Process Architecture

- u_cmask — File creation mask. Defines default file modes when files are created.
- u_mem — Memory usage. Updated in the clock handler for the active thread on each processor.
- u_nshmseg — Number of attached shared memory segments.
- u_rlimit[] — Array of rlimit structures that defines the resource limits for the process. The system imposes a total of seven resource limits. Each resource limit has a current value and maximum value (also referred to as a soft limit and a hard limit), maintained by rlimit_cur and rlimit_max in the rlimit structure. In Solaris releases up to and including Solaris 2.5.1, rlimit_cur and rlimit_max are 32-bit data types. Beginning in Solaris 2.6, there's a 64-bit version of the rlimit structure, and rlimit_cur and rlimit_max are 64-bit data types.

The system defines a maximum value for each type, which is effectively the maximum attainable value for the data types. The actual value isn't really significant in most cases because the value is sufficiently large that an “infinite” resource limit is implied, which is essentially no limit. When we use the term “infinite” in describing resource limits below, we mean the maximum value for a 64-bit data type. In case you are interested, the maximum value for a signed 64-bit data type is 9,223,372,036,854,775,807, or 9 exabytes. An unsigned 64-bit data type has a maximum value of 18,446,744,073,709,551,615, or 18 exabytes. Now do you know why we consider limits set at these values “virtually unlimited!”

In Solaris releases up to and including Solaris 2.6, a process's resource limits were changed with limit(1) or ulimit(2), which affected only the running process (a shell, typically) and whatever children were spawned. In Solaris 7, a limit(1) command was added, which allows you to change resource limits in other processes by specifying a PID on the command line. The following list describes each of the resource limits.

- CPU — Maximum CPU time in seconds. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGXCPU signal if the limit is reached.
- FSIZE — Maximum file size, in 512 byte blocks. Default values as CPU. The file system write code (the write()) function in UFS tests for this limit and sends a SIGFS if the limit is reached.
- DATA — Maximum size of the data segment. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGSEGV if the limit is reached.
- STACK — Maximum size of the stack segment. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGSEGV if the limit is reached.
- NOFILE — Maximum number of open files. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGXFILE if the limit is reached.
- CORE — Maximum core size. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGSIGZ if the limit is reached.
- VMEM — Maximum memory usage. Default soft and hard limit is the same; 4 billion for pre-2.6 releases, infinite for release 2.6 and beyond. The clock interrupt handler tests for this limit, and sends a SIGUSR1 if the limit is reached.

## Process Structures

In the above example, we used ps(1), determined the PID of our shell process, invoked the crash utility, and used the p function to get the process table slot (66, in this case). Then, to dump the proc structure for process PID 24676, we again used the p utility, with the -f flag and the process table slot number.

## 8.2.2 The User Area

The role of the user area (traditionally referred to as the uarea), has changed somewhat in the Solaris environment when compared with traditional implementations of UNIX. The uarea was linked to the proc structure through a pointer and thus was a separate data structure. The uarea was swappable if the process was not executing and memory space was tight. Today the uarea is embedded in the process structure–it is not maintained as a separate structure. The process kernel stack, which was traditionally maintained in the area, is now implemented in the LWP (see “The Lightweight Process (LWP)” on page 281). The interesting bits in the uarea are listed below in the order in which they appear in the /usr/include/sys/user.h.

- uexec — The magic number (file type) of the on-disk executable that was loaded with an exec(2) system call.
- uexecsz — The size of the executable file.
- u tsize — Size of the text segment of the process address space.
- u dsize — Size of the data segment of the process address space.
- u start — Time when the process started, set when the process is first created, just after the start time is set in p_msstart.
- u ticks — Execution time in clock ticks of the process. When accounting is turned on, writing to the account file on exit. A clock tick varies across process types. On UltraSPARC-based systems, there are 100 ticks per second.
- u exdata — Embedded extradata structure. Executable file information, as text, data, heap, shared library size, magic number, etc.
- upargs[] — Array of arguments passed to exec.
- comm[] — User command string when process was invoked.
- u argc, argv, envp — The number of command-line arguments (u argc), a pointer to the array of command-line arguments (u argv), and pointer to the array of environmental variables (u envp). These are the variables passed to the main() function; they must be declared in every program written to execute on the Solaris system, as set up by the compiler when code is generated to run.
- u cdir — Pointer to the vnode for the current directory.
- udir — Pointer to the root vnode. Not used unless chroot(2) is called.
- u ttyvp — Pointer to vnode for controlling tty.

### Figure 8.10 Process Open File Structures

| proc | uarea | proc | uarea |
|---|---|---|---|
| uareas | file struct | uareas | file struct |
| Array of uentry structures | file struct | Array of uentry structures | file struct |
| | file struct | | |

To obtain a list of a process's open files, use the /usr/proc/bin/pfiles-command.

```
$ /usr/proc/bin/pfiles
490: /bin/ksh /usr/dt/bin/Xsession
Current limit: 64 file descriptors
0: S_IFDPID mode:0777 dev:32,24 ino:1024 uid:0:size:1024
WRONY|_LARGEARLE
1: S_IFREG_APPEND mode:0664 dev:32,8 ino:1026:1981 uid:10:size:996
WRONY|_LARGEARLE
2: S_IP 0_WRONY|0_APPEND|LARGEARLE
WRONY|0_APPEND|LARGEARLE
3: S_IFCNRC mode:0666 dev:32,24 ino:143524 uid:0:gid:3:rdev:13,12
RDWR
5: S_IFREG mode:0664 dev:32,24 ino:22740 uid:0:gid:0:size:4
WRONY|_LARGEARLE
7: S_IPSOCK mode:0666,166,0 ino:27432 uid:0:gid:0:size:0
RDWR
62: S_IFREG mode:0555 dev:32,24 ino:29458 uid:2:gid:2:18792
WRONY|_LARGEARLE_CLOEXEC
```

The command lists the process name and PID (in this example, we dumped the open files for the windowing system session-manager process). Note that various bits of information are provided on each open file, including the file type, flags, mode bits, and size.

Like the process structure, the uarea contains supporting data for signals, including an array that defines the disposition for each possible signal. The signal disposition tells the operating system what to do in the event of a signal: ignore it,
