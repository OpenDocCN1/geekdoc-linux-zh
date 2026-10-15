
In case it is not yet apparent, the alarm() system call has several different uses. A process can set an alarm prior to starting a long task that might not complete if the input data is unexpectedly large. The alarm will prevent the process from spending too much time on potentially endless tasks. It can also set an alarm to do a task asynchronously after a specific amount of time, perhaps based upon the state of its data.

A system call that is often used with alarms is the pause() call. When a process calls pause(), it is suspended and remains suspended until it receives a signal. Any signal will do to waken it. The prototype of pause() is:

```
#include <unistd.h>
int pause(void);
```

If a process calls pause() without having scheduled an alarm that will expire after the call to pause(), it will most likely never run again¹. For example:

```
#include <unistd.h>
#include <stdio.h>
int main()
{
    pause();
    printf("You will never see this message!\n");
    return 0;
}
```

This program, when run, will stay blocked until either the kernel sends it a signal or a user does, and because there is no handler, it will take the default action on receiving the signal, which is usually to terminate, not ever reaching the printf() statement.

The demos directory contains several different examples to demonstrate the alarm(), signal(), and pause() calls. The snooze.c demo is similar to the UNIX sleep command. The snoozealot.c demo demonstrates how the alarm can be reused, how a signal handler for SIGALRM and for SIGINT can do program cleanup, and how to allow non-blocking user input while in a programmed loop that is counting down an alarm. The following demo is another example that focuses only on alarms but also records the times that they occur.

The program in the listing below, alarmdemo1.c, uses the signal() system call to install signal handlers. There is a second version of this program in the demos directory that does the exact same thing using sigaction() instead. It is useful to compare them.

## Listing 6.10: alarmdemo1.c

```
#include <unistd.h>
#include <stdio.h>
#include <signal.h>
#include <time.h>
#include <stdlib.h>

/* This is the SIGALRM handler. When the SIGALRM is delivered to this */
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

## Explanation

The main program begins by installing a SIGALRM handler using the signal() call:

```
signal(SIGALRM, catchalarm);
```

The catchalarm() handler is unlike the earlier examples. Before it does anything else, it calls signal() to reinstall the handler. This is because signals of the same type will be lost while the process is handling a signal. The only way to catch a SIGALRM while in the handler for SIGALRM is to reissue the signal(). Although this particular program cannot issue another alarm, in general, signal handlers should be designed so that if a second signal of the same type arrives while they
