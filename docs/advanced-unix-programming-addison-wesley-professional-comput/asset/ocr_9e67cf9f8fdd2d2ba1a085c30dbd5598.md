In the next two system calls, the which argument must be one of the three listed macros:

| **getitimer** —get value of interval timer |
|---|
| #include <sys/time.h> |
| int getitimer( |
| 	int which,	/* timer to get */ |
| 	struct itimerval *val	/* returned value */ |
| ); |
| /* Returns 0 on success or -1 on error (sets errno) */ |

| **setitimer** —set value of interval timer |
|---|
| #include <sys/time.h> |
| int setitimer( |
| 	int which,	/* timer to set */ |
| 	const struct itimerval *val,	/* value to set */ |
| 	struct itimerval *oval	/* returned old value */ |
| ); |
| /* Returns 0 on success or -1 on error (sets errno) */ |

| **struct itimerval** —structure for getitimer and setitimer |
|---|
| struct itimerval { |
| 	struct timeval it_interval;	/* reset value */ |
| 	struct timeval it_value;	/* current value */ |
| }; |

In an itimerval structure, it_interval is the time to reset the timer to when it expires, and it_value is the value of the current interval. That is, unlike alarm, which goes off only once, these timers can automatically reset themselves when they go off. If you call setitimer with an it_value member of zero, it stops the timer immediately. If you call setitimer with an it_interval member of zero, it stops the timer after the current interval expires. A timeval structure, defined in Section 1.7.1, has two members: tv_sec for seconds, and tv_usec for microseconds.

If the oval argument to setitimer is non-NULL, it gets the old value. Some examples:

```
```
/* 3.5 sec. timer, one time only */
itv.it_interval.tv_sec = 0;
itv.it_interval.tv_usec = 0;
itv.it_value.tv_sec = 3;
itv.it_value.tv_usec = 500000;
ec_negl( setitimer(TIMER_REAL, &itv, NULL) )
```
```