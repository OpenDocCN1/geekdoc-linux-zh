# # Process Context and Interrupt Context

The kernel accomplishes useful work using a combination of process contexts and interrupt contexts. Kernel code that services system calls issued by user applications runs on behalf of the corresponding application processes and is said to execute in process context. Interrupt handlers, on the other hand, run asynchronously in interrupt context. Processes contexts are not tied to any interrupt context and vice versa.

Kernel code running in process context is *preemptible*. An interrupt context, however, always runs to completion and is not *preemptible*. Because of this, there are restrictions on what can be done from interrupt context. Code executing from interrupt context cannot do the following:

+   - Go to sleep or relinquish the processor
+   - Acquire a mutex
+   - Perform time-consuming tasks
+   - Access user space virtual memory

Look at section "Interrupt Handling" in Chapter 4 for a full discussion of the interrupt context.