```
/* process, it resets the handler and displays the current time. */
void catchalarm(int signo)
{
    signal(SIGALRM, catchalarm); /* install handler again */
    time_t t;                     /* time in seconds since the Epoch */
    struct tm *tp;                /* time struct with years, months, days,... */

    time(&t);                     /* get current time as a time_t in t */
    tp = localtime(&t);           /* convert time to a tm struct */
    printf("Caught alarm at %d:%d:%d\n", tp->tm_hour, tp->tm_min ,tp->tm_sec );
}

int main(int argc, char * argv[])
{
    int k, sec;
    struct tm *tp;    /* time struct with years, months, days, etc */
    time_t t;         /* time in seconds since the Epoch */

    /* check proper usage */
    if (2 > argc) {
        printf("Usage: %s \n",argv[0]);
        return -1;
    }

    k = atoi(argv[1]);            /* convert argv[1] to int (no error check) */
    signal(SIGALRM, catchalarm);  /* install catchalarm as the handler */

    time (&t);                    /* store current time in t */
    tp = localtime(&t);           /* store t as day,hours,minutes, etc. */

    /* print time at which alarm is set an how long it is set for */
    printf("Time is %d:%d:%d\n", tp->tm_hour, tp->tm_min ,tp->tm_sec );
    printf("Alarm is set for %d seconds.\n", k);
    sec = alarm(k);               /* set alarm */

    pause();                      /* wait for a signal to arrive */
    return 0;
}
```

# Explanation

The main program begins by installing a SIGALRM handler using the signal() call:

```
signal(SIGALRM, catchalarm);
```

The catchalarm() handler is unlike the earlier examples. Before it does anything else, it calls signal() to reinstall the handler. This is because signals of the same type will be lost while the process is handling a signal. The only way to catch a SIGALRM while in the handler for SIGALRM is to reissue the signal(). Although this particular program cannot issue another alarm, in general, signal handlers should be designed so that if a second signal of the same type arrives while they