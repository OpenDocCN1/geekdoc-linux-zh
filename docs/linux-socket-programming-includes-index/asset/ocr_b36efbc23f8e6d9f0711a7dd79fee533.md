the same task (as if it were talking to itself). The same message still goes to the child, but the parent sees its own message in the input. Most communication paths are in one direction: the parent telling the child what it should process, so your process closes the unneeded channels. However, if you want true bi-directional communication, you need to call `pipe()` twice—one pipe for each direction (see Figure 7.3).

+   3.  The parent spawns the new task. The process gets an exact copy of everything (including the pipe). The pipe between the parent and child is inherited.
+   4.  The parent communicates with the child using the file descriptor array.
+   5.  The child process redirects its own standard input (this is optional) and communicates with the parent using the open pipe. It also closes the output channel.
+   6.  The parent needs only the output channel of the pipe to communicate with the child, so it closes the input channel.

You cannot redirect the I/O channels in threads because they share the file descriptor tables. This means that if you close the file in one thread, you essentially close it in all other threads of your program. Processes, on the other hand, make a copy of the file descriptor tables, so closing one channel does not affect the other processes in the program.

Figure 7.2 showed you how to create a unidirectional connection between a parent and the child. To create a bi-directional connection, you need to follow Figure 7.3.

Refer to this diagram to help you create pipes and redirection for your programming.

# Signaling a Course Change: Folding

The poker game has few direct, asynchronous controls. A player can fold (step out of the current game) at any time. If the game were held in the Old West, a cheater might meet a sudden, asynchronous termination. In any case, the dealer picks up the dropped cards. Likewise, after you have started a process, you can change its course or your parent task can get notified of termination with signals.

Every task you program should handle all useful signals. There are approximately 30 different kinds of signals (two signals are user-defined). Most signals you can ignore or not capture because the likelihood that they occur is slim or to capture them is not meaningful. Many uncaught signals usually terminate your program, and some of these are important to multi-tasking programs. For example, the system notifies the parent when a child terminates with a `SIGCHLD` signal.