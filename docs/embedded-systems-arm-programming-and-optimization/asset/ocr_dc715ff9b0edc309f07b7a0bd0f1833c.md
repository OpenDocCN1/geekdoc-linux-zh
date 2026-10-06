# 5.4 Kernel Workload Distribution

CPUs derive much of performance from their caches, which typically support rich feature sets such as sophisticated replacement policies, victim caches, and coherency with other caches. These features are designed to maximize memory performance for platform agnostic code.

Aggressive multilevel caches also allow CPUs to have small general register files, since compilers use frequent register spilling to exchange register contents with memory without a large performance penalty.

On the other hand, GPUs, FPGAs, and DSPs generally have simple or no caches, relying instead on annotations in the program code that explicitly allocate and manage on-chip memories. These program-controlled on-chip memories are sometimes referred to as scratchpad memory, although GPUs sometimes call them shared memory since they are also used as a mechanism by which intermediate results can be exchanged between work items within a workload.

On a CPU, the contents of any memory address may be stored in multiple levels of the memory hierarchy at any given time. In other words, the physical location of the data stored at a particular address cannot be determined since the on-chip caches are automatically managed by the hardware.

On a GPU, on-chip memory locations have their own special address ranges. This allows the program to specifically address on-chip memory and to explicitly copy data between on-chip and off-chip memory.

Also, GPUs typically have large register files and their compilers do not spill register values to off-chip memory. The registers serve as a item's private memory and must have sufficient capacity to store the highest number of live register values that a workitem will ever need during its execution, multiplied by the number of work-items assigned to the GPU core.

OpenCL supports programming idioms by which these different memories are referenced. Since different devices have on-chip memory structures, OpenCL must define a set of generalized abstractions that can be mapped to different device technologies.

OpenCL defines global memory as memory accessible by all processor cores. Global memory is usually the off-chip RAM. Global memory has the largest capacity, globally accessible to all work-items in the kernel, but has the highest latency. The OpenCL keyword “global” is used as a prefix to specify a pointer that points to global memory.