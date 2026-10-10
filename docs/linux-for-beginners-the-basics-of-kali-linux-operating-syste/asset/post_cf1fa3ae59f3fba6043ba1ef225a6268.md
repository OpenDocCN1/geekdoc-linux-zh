
## Resource allocation tables: memory tables, I/O tables, file tables, etc.

-   Process tables and flow tables that provide information about the processes and flows present in systems at a specific point in time

# Managing Process And Flow Blocks

Information about the processes and flows in the system is stored in special data structures, which are called process control blocks and flow control blocks. These structures are very important for the OS because on the basis of their information system manages processes.

Managing power flow (Thread Control Block or TCB) to an active flow, i.e., that which is in a state of readiness, expectation, or execution. This block may contain the following information:

-   Flow identity (usually its unique identifier)
-   Flow processor status: custom processor registers, instruction counter, the stack pointer
-   Flow planning information

Table streams is a list or array of flow control units. It is located in a protected area of the OS memory. The managing unit process (Process Control Block or PCB) corresponds to the process that is present in the system. Such block may contain:

-   Process identity (unique identifier, information about other processes related to the process)
-   Information about the threads that are running in the address space of the process (for example, pointers to their control blocks)
-   Information that allows you to determine the rights of a process to use different resources (for example, the user ID that created the process)
-   Process address allocation information
-   Information about I/O resources and files used by the process

# Process And Flow Images

The totality of the information displayed in the memory process is called the image process, and all information flow is called the thread image. The image process includes:

-   Process control unit
-   User code
-   User data (global program data common to all threads)
-   Process flow pattern information

The user program code, user data, and stream information are loaded into the process address space. The image process is generally not a continuous section of memory; its parts are unloaded to disk. The streaming image includes:

-   Flow control unit
-   Kernel stack (the flow stack used when executing kernel flow code)
-   User stack (stream stack available in user mode)

# Creating and Completing Processes and Threads

The process creation and termination tools allow you to dynamically change the set of applications that are running on the operating system. Thread creation and completion tools are the basis for creating multithreaded applications.

# Creating Processes

## Basic principles of process creation

Processes can be created by the kernel of the system during its initialization. For example, in UNIX-compatible systems, such a process can be the process of initialization of the init system, in Windows XP - the processes of subsystems (Win32 or POSIX). This creation process, however, is the exception, not the rule (fork and exec).

Most often, processes are created when performing other processes. In this case, a process that creates another process is called an ancestor, and the process created by it is called a descendant. New processes can be created while the application is running according to its logic (the compiler can create processes for each compilation step, the web server can handle the incoming requests), or directly at the request of the user (for example, from a command interpreter, graphical shell, or file manager).

## Interactive And Background Processes

There are two types of background processes in terms of their interaction with the user.

-   **Interactive processes** interact with users directly, receiving input from the keyboard, mouse, and more. An example of an interactive process is the process of a text editor or an integrated development environment.
-   **Background processes** do not interact with the user directly. They are usually started at system startup and are waiting for requests from other applications. Some of them (system processes) support the functioning of the system (implement background printing, networking tools, etc.), others exclude specialized tasks (implement web servers, database servers, etc.). Background processes are also called services (in Windows XP systems) or daemons (on UNIX).

## Managing Address Space When Creating Processes

Because the core element of the process is secure address space, it is important to solve the problem of allocating it when creating a new process. Consider two different approaches.

### System Calls Fork() Exec()

In the first approach, the descendant's address space is created as an exact copy of the ancestor's address space. This operation is implemented by a system call, which in POSIX systems is called `fork()`. In this case, not only the address space is copied, but also the counter of the main process commands, so after calling `fork()` the ancestors and descendants will follow the same instruction. The developer must determine which of the two processes should be managed. This can be done based on the differences between the `fork()` return codes for the ancestor and the descendant.

When the creation of a new process occurs by duplicating the ancestral address space, there is a need for special means of loading the code into the address space of the process. Such tools are implemented by a system call, which in POSIX systems is called `exec()`. As an option, to call `exec()`, the full path to the executable program to be loaded into memory must be specified. In `fork()`-based systems, in order to run the program, you must immediately call `exec()` after calling `fork()` (this is called fork + exec technology).

### Run The Application With One System Call

The second approach does not separate address space duplication and code loading - these steps are combined here into one. In this case, the system call triggers the specified application to execute (usually it needs to specify the entire path to the executable file of this application). It is to be divided into two stages of implementation of the system call:

-   Allocation of memory for the new process's address space (with no information from the address space ancestor being copied)
-   Download executable code from the specified file into the highlighted address space

The approach using `fork()` and `exec()` is more flexible, as it allows you to limit yourself to a single step of starting an application if necessary. Modern operating systems mainly implement a combination of the first and second approaches.

## Features Of Process Completion

Consider three options for completing processes. The process **correctly completes** on its own after completing its task (for interactive processes, this is often done at the initiative of a user who, for example, used the appropriate menu item). To do this, the process code must perform a system call to complete the process. This call on POSIX systems is called `exit()`. It can turn the process that caused it.

The process **crashes** due to an error. This output can be provided by the programmer (error when processing a decision that the program cannot continue) and may be due to the generation of interruption (division by zero, access to a secure area of memory, etc.).

The process is **completed by another process** or system kernel. For example, before the OS shutdown, the kernel stops performing all processes. The process can terminate a process through system calls, which in POSIX is called `kill()`.

Once the process completes its work, memory reserved for its address space is freed and can be used for other purposes. All flows of this process also cease to exist. If there are descendants in this process, their work is preferably not terminated after the work of the ancestor. The online processes are usually terminated when the user logs off.

### Synchronous And Asynchronous Execution Of Processes

When the system creates a new process for the old process, there are two basic options:

-   Continue execution in parallel with the new process - this mode of operation is called **asynchronous execution**
-   Suspend execution until the new process is complete - this is called **synchronous execution**. (In this case, they use a special system call, which in POSIX systems is called `wait()`)

The choice of a particular model depends on the specific task. For example, a web server can create descendant processes to handle requests (if the descendant set is not enough to handle that request). In this case, the processing must be asynchronous, as soon as the descendant is created and the ancestor must be ready to receive the next request. A compiler, on the other hand, must wait for the completion of each step before proceeding to the next stage, in which case they use synchronous processing.

### Creating and Completing Streams

#### Features Of Creating Streams

Setting up streams is different, related primarily to the fact that the currents are created within an existing address space (or a particular kernel process). There are several situations that can lead to a new stream.
