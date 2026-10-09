This time it kept displaying numbers, and typing Ctrl-c had no effect. We finally terminated it by typing Ctrl-\, which generated a quit signal (SIGQUIT), whose default behavior, which we didn’t modify, is to terminate the process.

Well, so much for the basics. Signals are actually pretty complicated because:

+   - There are lots of different signals, and sometimes the circumstances under which they’re generated and what they mean are complicated.
+   - Arranging the appropriate action for a signal can be complicated.
+   - Handling a signal can be complicated.

I’ll go through the issues step-by-step, and when you’ve finished this chapter all will be clear.

# 9.1.2 A Signal’s Lifecycle

A signal is born when whatever event it’s associated with occurs and *generates* it. Its life ends when it is *delivered*, which means that whatever *action* specified for it has been taken. There are three possible actions:

+   1. Default action (*SIG\_DFL*): terminate, stop, or continue the process, or ignore the signal.
+   2. Ignore the signal (*SIG\_IGN*).
+   3. Catch the signal by executing a signal handler when the signal is delivered.

Most signals can be generated *naturally* by whatever user or system event the signal is associated with. For example, dividing by zero generates a *SIGFPE* event naturally, and termination of a child generates a *SIGCHLD* event naturally. Alternatively, any signal can be generated *synthetically* by one of five system calls: *kill*, *killpg*, *pthread\_kill*, *raise*, or *sigqueue*. The next section, which enumerates all the signals, indicates the natural cause of each signal that has one. Five signals, *SIGKILL*, *SIGSTOP*, *SIGTERM*, *SIGUSR1*, and *SIGUSR2* have no natural cause and exist only to be synthesized, usually with the *kill* system call.

Between generation and delivery a signal is *pending*. If another signal of the same type arrives while a signal is pending, whether multiple signals of the same type are delivered is implementation dependent and should not be assumed in portable programs. There’s more on this subject in Section 9.5.3.