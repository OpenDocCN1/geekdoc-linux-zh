+   • An exception is main(), for which you can use return if you wish. Our own style is generally to use exit() when there are problems and ‘return 0’ at the end of main() if everything has gone well.
+   • Use _exit() or Exit() in a child process if exec() fails.

# 9.1.6 Recovering a Child’s Exit Status

When a process dies, the normal course of action is for the kernel to release all its resources. The kernel does retain the dead process’s exit status, as well as information about the resources it used during its lifetime, and the PID continues to be counted as being in use. Such a dead process is termed a zombie.

The parent process, be it the original parent or init, can recover the child’s exit status. Or, by use of BSD functions that aren’t standardized by POSIX, the exit status together with the resource usage information can be recovered. Status recovery is done by waiting for the process to die: This is also known as reaping the process.²

There is considerable interaction between the mechanisms that wait for children to die and the signal mechanisms we haven’t described yet. Which one to describe first is a bit of a chicken-and-egg problem; we’ve chosen to talk about the child-waiting mechanisms first, and Chapter 10, “Signals,” page 347, provides the full story on signals.

For now, it’s enough to understand that a signal is a way to notify a process that some event has occurred. Processes can generate signals that get sent to themselves, or signals can be sent externally by other processes or by a user at a terminal. For example, CTRL-C sends an “interrupt” signal, and CTRL-Z sends a job control “stop” signal.

By default, many signals, such as the interrupt signal, cause the receiving process to die. Others, such as the job control signals, cause it to change state. The child waiting mechanisms can determine whether a process suffered death-by-signal, and, if so, which signal it was. The same is true for processes stopping and, on some systems, when a process continues.