+   - GNU/Linux follows POSIX, which is similar but not identical to BSD. If no data were transferred, the system call returns -1/EINTR. Otherwise, it returns a count of the amount of data transferred. The BSD “always restart” behavior is available in the sigaction() interface but is not the default.

+   - Signal handlers used with signal() are prone to race conditions. Variables of type volatile sig_atomic_t should be used exclusively inside signal handlers. (For expositional purposes, we did not follow this rule in some of our examples.) Similarly, only the functions in Table 10.2 are safe to call from within a signal handler.

+   - The System V Release 3 signal API (lifted from 4.0 BSD) was an initial attempt at reliable signals. Don’t use it in new code.

+   - The POSIX API has multiple components:
+       - the process signal mask, which lists the currently blocked signals,
+       - the sigset_t type to represent signal masks, and the sigfillset(), sigemptyset(), sigaddset(), sigdelset(), and sigismember() functions for working with it,
+       - the sigprocmask() function to set and retrieve the process signal mask,
+       - the sigpending() function to retrieve the set of pending signals,
+       - the sigaction() API and struct sigaction in all their glory. These facilities together use signal blocking and the process signal mask to provide reliable signals. Furthermore, through various flags, it’s possible to get restartable system calls and a more capable signal handler that receives more information about the reason for a particular signal (the siginfo_t structure).

+   - kill() and killpg() are the POSIX mechanisms for sending signals. These differ from raise() in two ways: (1) one process may send a signal to another process or an entire process group (permissions permitting, of course), and (2) sending signal 0 does not send anything but does do the checking. Thus, these functions provide a way to verify the existence of a particular process or process group, and the ability to send it (them) a signal.

+   - Signals can be used as an IPC mechanism, although such use is a poor way to structure your application and is prone to race conditions. If someone holds a gun