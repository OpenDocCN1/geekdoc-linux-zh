
If you don’t want the signal mask to be saved, and for some reason you don’t want to just set the *save_mask* argument of *sigsetjmp* to zero, you can use yet another pair:

- **\_setjmp**—set jump point

```c
#include <setjmp.h>

int _setjmp(
    jmp_buf loc_info    /* saved location information */
);
/* Returns 0 if called directly, non-zero if from longjmp (no error
   return) */
```

- **\_longjmp**—jump to jump point without restoring signal mask

```c
#include <setjmp.h>

void _longjmp(
    jmp_buf loc_info,     /* saved location information */
    int val               /* value for setjmp to return */
);
```

Of course, *\_longjmp* isn’t async-signal-safe either. Actually, these two underscored functions are just leftovers from an early standard.

## 9.7 Clocks and Timers

This section describes various system clocks and timers that use those clocks to generate a signal, after a preset interval.

### 9.7.1 *alarm* System Call

- **alarm**—schedule an alarm signal

```c
#include <unistd.h>

unsigned alarm(
    unsigned secs     /* seconds until signal */
);
/* Returns seconds left on previous alarm or zero if none (no error
   return) */
```

Every process has one alarm clock set aside for the *alarm* system call. When the alarm goes off, a *SIGALRM* is sent. A child inherits its parent’s alarm clock value, but the actual clock isn’t shared. The alarm clock remains set across an *exec*.

*alarm* sets the clock to the number of seconds given by *secs*. The previous setting is returned; it will be 0 if no time remained on the clock previously or if there was no previous alarm. The previous setting is used to restore the clock to the way it was before *alarm* was called.

If *secs* is 0, the alarm clock is turned off. It's important to remember to do this. For example, let's say you have a blocking system call like *read* and you only want to block for a limited time. You catch *SIGALRM* (with an empty handler), call *alarm* for, say, 5 seconds, and then issue the *read*, which blocks. When the alarm goes off, the *SIGALRM* interrupts the blocking system call, and *read* returns -1 with *errno* set to *EINTR*. But if *read* returns sooner than 5 seconds, and you forget to turn off the alarm, it will go off later—much later, since 5 seconds is a very long time in computer terms—and maybe mysteriously interrupt something else! You'll know something is amiss if you rigorously check error returns, as we do in this book, but, alas, not everyone does.

Here's an example:

```c
int main(void)
{
    struct sigaction act;
    char buf[100];
    ssize_t rtn;

    memset(&act, 0, sizeof(act));
    act.sa_handler = handler;
    ec_neg1( sigaction(SIGALRM, &act, NULL) )
    alarm(5);
    if ((rtn = read(STDIN_FILENO, buf, sizeof(buf) - 1)) == -1) {
        if (errno == EINTR)
            printf("Timed out... type faster next time!\n");
        else
            EC_FAIL
    }
    alarm(0);
    if (rtn == 0)
        printf("Got EOF\n");
    else if (rtn > 0) {
        buf[rtn] = '\0';
        printf("Got %s", buf);
    }
    exit(EXIT_SUCCESS);

EC_CLEANUP_BGN
    exit(EXIT_FAILURE);
EC_CLEANUP_END
}
```

```c
static void handler(int signum)
{
}
```

In the following sample interaction, I didn't type anything after the first execution of *alarm_test*; I typed "faster" after the second:

```text
$ alarm_test
Timed out... type faster next time!
$ alarm_test
faster
Got faster
$
```

Using *alarm* to interrupt a blocking system call is fine in simple cases, like the one I showed, but in more complicated situations you'll probably be blocking in *select* or *poll*, rather than in *read* directly. If you want to time out, use *pselect* if it's available instead of setting an alarm.

A limitation with *alarm* is that there's only one such alarm clock per process. Sections 9.7.4 and 9.7.6 describe timer system calls with more flexibility.

### 9.7.2 *sleep* System Call

*sleep* is a familiar function that we've used throughout this book. It blocks a thread for a specified number of seconds:

- **sleep**—suspend execution for seconds or until signal

```c
#include <unistd.h>

unsigned sleep(
  unsigned secs      /* seconds to sleep */
);
/* Returns unslept amount */
```

The rules for *sleep* in the SUS contain lots of verbage that allows for a *SIGALRM* to interfere with it, specifically so *sleep* can be implemented as a function in terms of *alarm* and *pause*, or better, *alarm* and *sigsuspend*. Here's a simple way to implement *sleep*:

```c
unsigned aup_sleep(unsigned secs)
{
  struct sigaction act;
  unsigned unslept;

  memset(&act, 0, sizeof(act));
  act.sa_handler = sig_handler;
  ec_neg1( sigaction(SIGALRM, &act, NULL) )
  alarm(secs);
  pause();
  unslept = alarm(0);
  return unslept;

  EC_CLEANUP_BGN
    EC_FLUSH("aup_sleep")
    return 0;
  EC_CLEANUP_END
}

static void sig_handler(int signum)
{
}
```

This version works but has some problems:

- If *SIGALRM*s aren’t blocked, the arrival of one before the call to *sigaction* might terminate the process.
- If they are blocked, the function won’t even work.
- If the *alarm* goes off between the calls to *alarm* and *pause*, the *pause* may last forever.
- The old action for *SIGALRM* isn’t restored.
- *alarm* and *sleep* are supposed to be compatible.

The last point means that in a sequence like

```c
alarm(10);
...
sleep(20);
```

the *alarm* going off should interrupt the *sleep* and execute the handler for *SIGALRM*, and in a sequence like

```c
alarm(20);
...
sleep(10);
```

the *alarm* should be set for 10 more seconds after *sleep* returns.

Handling the interaction of *alarm* and *sleep*, preventing an errant *SIGALRM* from terminating the process, preventing an infinite *pause*, and restoring the old action and mask require a lot of tricky code that has to handle the three possible cases:

- No alarm was set when *sleep* was called.
- The remaining alarm time is less than or equal to the requested *sleep* time.
- The remaining alarm time is greater than the requested *sleep* time.

This version works:

```c
unsigned aup_sleep(unsigned secs)
{
    sigset_t set, oset;
    struct sigaction act, oact;
    unsigned prev_alarm, slept, unslept, effective_secs;

    ec_neg1( sigemptyset(&set) )
    ec_neg1( sigaddset(&set, SIGALRM) )
    ec_neg1( sigprocmask(SIG_BLOCK, &set, &oset) )
    prev_alarm = alarm(0);
    if (prev_alarm != 0 && prev_alarm <= secs)
        effective_secs = prev_alarm;
    else {
        memset(&act, 0, sizeof(act));
        act.sa_handler = slp_handler;
        ec_neg1( sigaction(SIGALRM, &act, &oact) )
        effective_secs = secs;
    }
    alarm(effective_secs);
    set = oset;
    ec_neg1( sigdelset(&set, SIGALRM) )
    if (sigsuspend(&set) == -1 && errno != EINTR)
        EC_FAIL
    unslept = alarm(0);
    slept = effective_secs - unslept;
    ec_neg1( sigaction(SIGALRM, &oact, NULL) )
    if (prev_alarm > slept)
        alarm(prev_alarm - slept);
    ec_neg1( sigprocmask(SIG_SETMASK, &oset, NULL) )
    return unslept;

    EC_CLEANUP_BGN
    EC_FLUSH("aup_sleep")
    return 0;
    EC_CLEANUP_END
}

static void slp_handler(int signum)
{
}
```

[^8] Geoff Clare contributed to this version by finding bugs in my original attempt.

Here’s what’s going on, step-by-step:

1. We block *SIGALRM* so we can proceed without worrying about one being delivered. We save the old signal mask in *oset*.
2. We turn off the alarm, in case it’s set, and save the remaining time.
3. We calculate how long to sleep (*effective_secs*, reducing the amount requested if the remaining alarm time was less), and we set an alarm for that time.
4. If no alarm was already set or the sleep time is less than the remaining alarm time, we install the empty handler and save the old action in *oact*.
5. We call *sigsuspend* instead of *pause* so that we can atomically unblock *SIGALRM*. We leave the other bits in the mask the way they were on entry to *aup_sleep*.
6. When *sigsuspend* returns, it is because the alarm went off or because some other signal interrupted it. We don’t especially care which it was. We do need the amount remaining on the alarm, though, which we get when we turn it off.
7. We calculate the amount of time actually slept.
8. We reset the old action for *SIGALRM*.
9. If the time slept is less than the remaining alarm time on entry, we reset the alarm for the new time remaining (some was slept off).
10. We reset the signal mask.
11. We return the unslept time.

If you can understand this function, you’ve mastered 90% of what’s in this chapter and you can give yourself an A. If you find a mistake and mail it to aup@basepath.com, score yourself an A+.

### 9.7.3 Higher-Resolution Sleeping

*sleep* sleeps for some number of seconds, but that’s way too long for many purposes. There are two other calls that sleep for more precise intervals:
