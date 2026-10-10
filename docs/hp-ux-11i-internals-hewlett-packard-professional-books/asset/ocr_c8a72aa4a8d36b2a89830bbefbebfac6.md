The stack frame used for calling the user’s function is set up such that the return address points to the sigcleanup() routine. More specifically, since the signal handler is going to be in user space and sigcleanup() is a kernel routine, the return address points to a stub in libc that handles the callback into the kernel for cleanup.

We also have to manipulate things to actually get into the signal handler. Remember that we’re in the kernel code, and we got here by means of a trap, a sleep, a wakeup, or a system call. Those are the things that cause signal detection. We have a save state, which points back to the user code that sent us into the kernel. (For details on this, see Chapter 4.) We have to modify that save state so that when we leave kernel mode, we go instead to the user’s handler, sendsig_setuphandler() does this by modifying the value of GR 31—the return pointer—in the save state.

sendsig() has sanity checks throughout this process to make sure the user’s stack hasn’t been corrupted. If any utility routine fails because it’s unable to manipulate the user’s stack, the process gets immediately terminated. This is done by one of my favorite routines—sendsig_the_barbarian(). Even kernel engineers have a sense of humor.

# Signal Handler Return

When the user’s signal handler returns, it branches back to the return pointer it was given by sendsig(). This vectors into a routine in libc, which then goes to a system call to the sigcleanup() kernel routine. sigcleanup() has a pretty easy job—it essentially restores the save state that was saved by sendsig() so that when it returns, it will go back to the place the signal occurred. There are some sanity checks to make sure the user hasn’t modified the stack in any way he or she shouldn’t have, and once again sendsig_the_barbarian() is there to cut down any process with an invalid stack.

# Summary

The generation and handling of signals is a complicated process, involving several transitions between user and kernel space. The kernel has to deal with signals that can be caught, ignored, or held. It also has to determine which thread should receive a signal and manage information passed from the sender to the handler.