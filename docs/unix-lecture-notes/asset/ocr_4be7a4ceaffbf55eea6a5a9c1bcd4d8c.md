```
write(1, &s, s_len);\nwrite(1, &x, n+1);\nprintf("\\n");\n}\n}\n} // while\nreturn 0;\n}\n\nvoid interrupt_handler (int signo, siginfo_t *info, void *context)\n{\n    int     localid;      /* stores a number to uniquely identify signal */\n    time_t  timenow;      /* current time -- used to generate id */\n    static  int ticker = 0; /* used for id also */\n    struct tm *tp;\n\n    time(&timenow);\n    tp = localtime(&timenow);\n    localid = 36000*tp->tm_hour + 600*tp->tm_min + 10*tp->tm_sec +\n              ticker++ % 10;\n    printf("Entered handler: sig = %d \\tid = %d\\n",\n           info->si_signo, localid);\n    sleep(3);\n    printf("Leaving handler: sig = %d \\tid = %d\\n",\n           info->si_signo, localid);\n}
```

The while loop in the main program exists just to demonstrate that the system calls to perform I/O are restarted when the interrupts occur. You can run this program with any combination of SA_RESTART, SA_RESETHAND, and SA_NODEFER to see the combined effect of the flags. You can add any signal to the blocked set, but you will only be able to send SIGINT and SIGQUIT unless you open a separate window and use the kill command to send arbitrary signals to the process. You can try this – put signal 4 in the blocked set and issue kill -4 with the process id from a second window while the process is handling a Ctrl-C. You will see that signal 4 is blocked until interrupt_handler() finishes.

The while loop is designed so that you do not have to kill this program to terminate it. If you type "quit" it will terminate.

# 5.3.13  Creating Signal Mask Sets

There are four functions that modify signal mask sets:

```
sigemptyset(sigset_t *set);\nsigfillset(sigset_t *set);\nsigaddset(sigset_t *set, int signum);\nsigdelset(sigset_t *set, int signum);
```

The first two create empty and full mask sets respectively. The next two add or delete specific signals from the specified sets. You can either create an empty mask and add to it, or create a full mask and delete from it. If you plan on having more than half of the signals in it, then do the latter, otherwise do the former.