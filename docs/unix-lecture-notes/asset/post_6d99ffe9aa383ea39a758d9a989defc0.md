
are processing the first, they are not caught "by surprise" and possibly killed by the second signal. This handler is just demonstrating that technique.

The handler uses the time() and localtime() system calls to get the current time, convert it to a human readable format, and display it on the console. The main program displays the current time and immediately turns on the alarm by calling

```
alarm(k)
```

where k is the command line argument's numeric value. It then calls pause() to wait for the SIGALRM to be received. If a SIGALRM arrives before any other signal, it will cause catchalarm() to run, which will display the time. If another signal arrives first, the process will probably be killed.

## 6.10 Interval Timers

The time granularity, or resolution, of the alarm() system call is too coarse to be useful for many applications. Furthermore, alarm() must be called repeatedly if an alarm is to go off at regular intervals, such as when a process is timing the progress of some task. (Suppose you wanted to display some sort of speed indicator on the console, where instantaneous speed was measured by the amount of data written in a fixed time interval. You would need a timer of fine resolution and a SIGALRM catcher that would measure the amount of data processed and reinstall itself, but this would be slightly inaccurate because of time lapsed between the start of the handler and the time it took to reinstall itself.)

Interval timers were introduced in later Berkeley distributions of UNIX (4.2BSD) as well as in the SVR4(1170) versions of UNIX as a solution to this problem. An interval timer has two components: an initial delay and a repeat interval. The value of the initial delay is the amount of time the kernel should delay before sending the first signal to the process. The value of the repeat interval is the amount of time the kernel should wait between successive signals sent to the process. In other words, if an interval timer is started at time t0, with initial delay = x and repeat interval y, then it will generate signals at times t0 + x, t0 + x + y, t0 + x + 2y, t0 + x + 3y, t0 + x + 4y, ... until the process terminates.

### 6.10.1 Three kinds of timers: Real, Virtual, and Profile

There are three different types of interval timers. One type of timer ticks during all elapsed time (like the clock on the wall); this is the real timer. The second ticks only when the process is in user mode (like the timer in a sporting event, which stops when play is paused for various reasons); this is the virtual timer. The last ticks when the process is in user mode or in system calls (like the timer in a professional chess game, which is stopped when one person has stopped it and the other has not yet started it); it is called the prof timer. The constants used to define these timers, as you will shortly see in the documentation are:

ITIMER_REAL ticks always and sends a SIGALRM when it expires

> 5 If the two people decide to take a coffee break, the timer is in the off state. You can think of user mode as your time and kernel mode as your opponent's time. Then this analogy fits.

ITIMER_VIRTUAL only ticks when the process is in user mode, i.e., not in system calls. It sends a SIGVTALRM when it expires.

ITIMER_PROF ticks during user mode and in system calls; on expiration sends a SIGPROF signal

The "PROF" in SIGPROF and ITIMER_PROF is short for profile, which is a snapshot of a process's time usage across all user mode and kernel mode activities. From these definitions, it follows that the time the process spends sleeping is its real time less its profile time, and that the time it spends in kernel mode is profile time less virtual time. Our interest is in real interval timers, those that tick like an ordinary alarm clock.

### 6.10.2 The Initial and Repeating Values

An itimer_val structure contains two members: the value of the initial delay, and the value of the repeat interval:

```
struct itimerval {
    struct timeval it_interval; /* next value */
    struct timeval it_value;    /* current value */
};
```

The initial delay is stored in the it_value element and the repeat interval is stored in it_interval. As the timer ticks, the it_value element is decremented; when it reaches zero, a signal is sent to the process and the value of it_interval is copied into it_value.

Each member is of type timeval. A timeval structure represents a time interval using two elements: the number of seconds and the number of microseconds in the interval. There is no milliseconds field:

```
struct timeval {
    long tv_sec;      /* seconds */
    long tv_usec;     /* microseconds */
};
```

As a long integer is usually either 32 or 64 bits, depending upon the implementation, the tv_usec member is large enough to represent any number of microseconds from 0 to one million. Since it is common to work with time in milliseconds, you need to convert a time measured in milliseconds to a timeval with seconds and microseconds units. Mathematically, if t is a time expressed in milliseconds, then

- ⌊t/1000⌋ is the number of whole seconds in t, and
- 1000 · (t mod 1000) is the number of microseconds in t − ⌊t/1000⌋

Therefore, the following C code fragment sets a timeval structure's fields, given an integer number m of milliseconds
