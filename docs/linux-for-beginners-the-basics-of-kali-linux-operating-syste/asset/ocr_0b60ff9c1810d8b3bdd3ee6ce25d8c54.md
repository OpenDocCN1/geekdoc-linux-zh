If a process is created by a fork () system call, flow is automatically created after the distribution of the address space within that process (often the main application flow). You can create streams from the user code with an appropriate system call.

Many operating systems have special threads that create the kernel of the system (the kernel code can also be executed in threads). When creating a stream, the system must follow these steps.

+   1. Create data structures that reflect the flow in the OS
+   2. Select city at the stack of flow
+   3. Set the processor command counter to the beginning of the code to be executed in the thread;

this code is called a stream procedure or function, and the ng pointer is referred to as a stream call or system call.

Note that when creating flows, as opposed to the creation process, there is no need to allocate memory for the new address space, so usually flows are created faster and with lesser resources.

# Features Completion Streams

At the end of the stream, its resources are released (first of all, the folder); this operation is usually faster than completing the process. The flow may be completed when the control reaches the end of the flow procedure; there are also special system calls intended for early termination of flows.

Like processes, threads can be executed synchronously and asynchronously. A thread that created another thread may pause its execution until it is completed. This expectation is called joining streams (thread joining). Upon completion of the attached thread,