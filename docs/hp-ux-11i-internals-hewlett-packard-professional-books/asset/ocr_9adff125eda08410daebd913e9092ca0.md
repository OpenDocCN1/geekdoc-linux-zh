# C H A P T E R   1 3

# Kernel Services

In addition to managing the system hardware and scheduling processes, the kernel provides a variety of services to both user applications and kernel subsystems. The services we most commonly associate with the kernel—the system calls—are covered in Chapter 4, “Programs, Processes, and Threads.” The kernel also provides a variety of services to other subsystems within the kernel. In this chapter, we look at what some of those services are and how they are handled.

# The Callout Table

The kernel sometimes needs to be able to schedule events to happen in the future. For example, a driver might want a timeout on an I/O operation. The driver starts an I/O and is interrupted by the I/O system when the I/O completes, but if for some reason the I/O doesn’t complete, the driver needs to know about that too. The driver sets a callout for some number of ticks in the future, specifying a routine to be called at that time. If the I/O completes successfully, then the callout is cancelled. If the callout routine gets called, then the driver knows something went wrong.

# Interface

The basic function for setting a timeout is called `timeout()`. It takes three arguments: a pointer to a function to call, a `void*` argument to pass to the function, and an integer representing the number of ticks in the future at which the function should be called. There are also a few other variations on this routine, including `timeout_on_spu()`, which allows the caller to specify on which system processor unit (SPU) the timeout function should run.