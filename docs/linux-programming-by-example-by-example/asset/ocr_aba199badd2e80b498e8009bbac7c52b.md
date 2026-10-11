```
struct sigaction action;

/* Set up the handler */
action.sa_handler = hndl_usr1;
sigemptyset(&action.sa_mask);
action.sa_flags = SA_NOCLDSTOP;

/* Register the handler */
if((sigaction(SIGUSR1, &action, NULL)) < 0)
    err_quit("sigaction");
/* Enough time to send a signal */
sleep(60);

exit(EXIT_SUCCESS);
```

```
void err_quit(char *msg)
{
    perror(msg);
    exit(EXIT_FAILURE);
}
void hndl_usr1(int signum)
{
    if(signum == SIGUSR1)
        puts("caught USR1");
    else
        printf("caught %d\n", signum);
}
```

`hndl_usr1` is a simple signal handler, doing nothing more than reporting the fact that it caught `SIGUSR1`. Since the `sa_mask` member of `action`, the `sigaction` structure, should contain additional signals to block while the signal handler is running, you simply initialize it to an empty set by passing it directly to `sigemptyset`. With the handler set up, `sigaction` registers the handler for `SIGUSR1`. Since you are not interested in the old disposition of the handler, you pass `NULL` as the value for `oset`. Finally, the program sleeps for 60 seconds to give you enough time to send it a signal. Run this program in one window, then send it `SIGUSR1` from another window, as illustrated: