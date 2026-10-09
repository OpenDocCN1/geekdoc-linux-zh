```
    }
    return;

EC_CLEANUP_BGN
    EC_FLUSH("timer_try1")
EC_CLEANUP_END
}

void handler(int signum)
{
    write(STDOUT_FILENO, "\nX\n", 3);
}
```

And this was the output:

```
X
ERROR:  0: tml [/aup/c9/tmr.c:26] 0
    *** EINTR (4: "Interrupted system call") ***
```

What happened was that the first X came out OK, after 2 seconds, but the SIGALRM signal interrupted the read, which was blocked. The fix is to set the SA_RESTART flag so system calls won’t be interrupted:

```
    memset(&act, 0, sizeof(act));
    act.sa_handler = handler;
    act.sa_flags = SA_RESTART;
    ec_neg1( sigaction(SIGALRM, &act, NULL) )
```

Now the output is this, showing that “hello” was typed and then echoed, along with the Xs every 2 seconds:

```
X
x
hello
X
hello
X
...
```

There’s another interval timer system call named ualarm, but it’s obsolete.

# **9.7.5 Realtime Clocks**

All UNIX systems have a basic clock whose value you can read with the time and gettimeofday system calls (Section 1.7.1), but the same Timers option