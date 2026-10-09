# 9.1.6 sigaction System Call

You determine the action to be taken when a signal is delivered with the `sigaction` system call, which you call for each signal whose action you want to set:

```
```
int sigaction(int signum,
              const struct sigaction *act,  /* new action */
              struct sigaction *oact)       /* old action */
```
```

The argument `oact` points to a structure that specifies the new action for the whole process—signal actions are not kept for individual threads. If `oact` is non-NULL, the old action is returned to where it points. If all you want is the old action, you can set `oact` to NULL, in which case the action isn't changed. In most of our examples we've set `oact` to NULL, but Section 9.7.2 has an example where it's used to save the old action so it can be restored.

You can't change the action for SIGKILL, which always terminates the process (not just a thread), or SIGSTOP, which always stops a process (not just a thread).

In the `sigaction` structure, `sa_handler` specifies the action with one of these values:

+   - **SIG_DFL**: The signal gets its default action, which depends on the signal, as described in Section 9.1.3, but is always ignore, terminate, stop, or continue. Again, these always apply to the entire process, never to just an individual thread.

+   - **SIG_IGN**: Ignore the signal, so that delivery has no effect. There's also a side-effect when the SIGCHLD signal is set to SIG_IGN, which is the same as the effect of the SA_NOCLDWAIT flag; see below. Confus-