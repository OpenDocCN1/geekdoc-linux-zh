specified that denies access to the file to all processes except the current one.

The allocation of processor time between processes is necessary because the processor executes instructions one by one (ie, at a particular time, only one process can physically execute on it), and for the user, the processes should appear as sequences of instructions executed in parallel. To achieve this effect, the OS provides the processor with each process for a short time, after which it switches the processor to another process; in this case, the execution of the processes resume from the place where they were interrupted.

In a *multiprocessor system*, processes can run in parallel on different processors.

Modern operating systems in addition to processes can support multitasking, which provides in the process, the presence of several sequences of instructions (*threads*), which run in parallel to the user, like most processes in the OS. Unlike processes, threads do not provide resource protection (for example, they share the address space of their process).

# ## Memory Management

While executing the code, the processor takes instructions and data from the computer's (main) memory. This memory is displayed as an array of bytes, each of which has an address.

As mentioned, the main memory is a type of resource between processes. OS is responsible for the allocation of memory. The address space is protected during the process and released only after the execution process is completed. The amount of memory available to the process can vary in the course of the distribution of memory.

OS must be capable of programs, individually or in the aggregate amount available for the main memory. To this end, virtual memory technology must be realized. This technology allows placing in the