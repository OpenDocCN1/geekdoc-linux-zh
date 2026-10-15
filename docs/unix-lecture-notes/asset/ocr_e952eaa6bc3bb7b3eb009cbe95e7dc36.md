```
sigset_t sa_mask;                 // pointer to signal handler
                                   // additional signals to block
int sa_flags;                       // during handling of the signal
};                                  // flags that affect behavior
```

In other words, there are two different forms of the sigaction structure. The first one uses the old-style of handler, and the second uses the newer POSIX compliant method. The structs are otherwise identical.

# Notes

In the old-style, the sa_handler member does not have to be a pointer to a function. It can also be one of the two flags SIG_IGN or SIG_DFL. If it is SIG_IGN, the signal is ignored; if SIG_DFL, then the default action is taken. If a pointer to a handler is supplied, that handler will be run. The handler must have a single integer argument.

In the new style, the sa_handler is replaced by a pointer to a function that has three parameters as follows:

+   - An sa_mask, which defines which signals should be blocked while the handler is processing the signal. By default, the signal that caused the handler to run will always be blocked. Adding signals to SA_MASK is a way to block other signals as well.
+   
+   - The sa_flags is a flag set that can be used to control how subsequent signals of the same type as the one that caused the handler to run are handled. For example, if a handler is handling a SIGINT signal and another SIGINT arrives while the process is in the handler, the sa_flags will determine how to dispose of the second SIGINT. It has no effect on other arriving signals. The flags determine how arriving signals are handled after the handler has been invoked. All flags are independent and sa_flags is their bitwise-or. The most important flags are:

SA_RESETHAND  If this bit is set, the signal action is reset to SIG_DFL. This means that as soon as the signal is delivered, the default action will take place. This flag implies the SA_NODEFER flag; signals are not blocked, instead causing the process to take whatever the default action for the type of signal. The intention is to make the handler behave like the old-style signal() handler, since any signal arriving after the first will cause the default behavior.

SA_NODEFER  If this bit is set, the kernel will not automatically block the signal while it is being caught. This means that an arriving signal will cause the handler itself to be interrupted and re-entered with the second signal. This is involuntary recursion.

SA_RESTART  If this bit is set, certain system calls that would otherwise be terminated if a signal were delivered during their execution, will be automatically restarted. This bit allows the BSD style handling.

SA_SIGINFO  If this bit is set, two additional arguments are passed to the signal-catching function. If the second argument is not NULL, it points to a siginfo_t structure containing the reason why the signal was generated; the third argument points to a ucontext_t structure containing the receiving process’s context when the signal was delivered.