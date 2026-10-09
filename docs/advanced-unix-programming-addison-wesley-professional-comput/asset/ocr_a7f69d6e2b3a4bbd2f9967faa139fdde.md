```
( SIGFPE, "Erroneous arithmetic operation" ),
( SIGILL, "Illegal instruction" ),
( SIGSEGV, "Invalid memory reference" ),
( SIGSYS, "Bad system call" ),
( SIGXCPU, "CPU-time limit exceeded" ),
( SIGXFSZ, "File-size limit exceeded" ),
( 0, NULL )
};

while (true) {
ec_rx( sigwait( sigset_t *)arg, sigsnum) )
clean_up();
for (i = 0; sigmsg[i].snum > 0; i++)
if (sigmsg[i].snum == sigsnum) {
fprintf(stderr, "%s\n", sigmsg[i].msg);
break;
}

_exit(EXIT_FAILURE);
}
return (void *)true; /* never get here */

EC_CLEANUP_BGN
EC_PUSH("sig_thread")
return (void *)false;
EC_CLEANUP_END
}

static void clean_up(void)
{
/*
Clean-up code goes here --
need not be async-signal-safe.
*/
}
```

The advantage of this version over the one in Section 9.1.8 is that, when a signal is returned by sigwait, we're in a thread, not a signal handler, and we're free to use any system calls or functions we like--we're not restricted to the async-signal-safe list. Note that the comment in the clean_up function has been changed accordingly.

The disadvantage of this version is that it doesn't work! There are two reasons why, both serious:

+   * If some other thread gets a SIGSYS, for example, that signal will be sent to that thread, not to the process, and the sigwait in the sig_thread function won't return with it. Indeed, since that signal is blocked in all threads, it