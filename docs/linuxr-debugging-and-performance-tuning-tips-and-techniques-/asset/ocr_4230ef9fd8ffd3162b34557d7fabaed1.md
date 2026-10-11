# WN OHANG

If no child has exited, return immediately. That way you can check periodically to see if any children have died. (Such periodic checking is known as *polling* for an event.)

# WNTRACED

Return information about a child process that has stopped but that hasn't exited yet. (For example, with job control.)

# WCONTINUED

(XSI.) Return information about a child process that has continued if the status of the child has not been reported since it changed. This too is for job control. This flag is an XSI extension and is not available under GNU/Linux.

Multiple macros work on the filled-in `*status` value to determine what happened. They tend to come in pairs: one macro to determine if something occurred, and if that macro is true, one or more macros that retrieve the details. The macros are as follows:

# WIFEXITED(status)

This macro is nonzero (true) if the process exited (as opposed to changing state).

# WEXITSTATUS(status)

This macro gives the exit status; it equals the least-significant eight bits of the value passed to `exit()` or returned from `main()`. You should use this macro only if `WIFEXITED(status)` is true.

# WIFSIGNALED(status)

This macro is nonzero if the process suffered death-by-signal.

# WTERMSIG(status)

This macro provides the signal number that terminated the process. You should use this macro only if `WIFSIGNALED(status)` is true.

# WIFSTOPPED(status)

This macro is nonzero if the process was stopped.

# WSTOPSIG(status)

This macro provides the signal number that stopped the process. (Several signals can stop a process.) You should use this macro only if `WIFSTOPPED(status)` is