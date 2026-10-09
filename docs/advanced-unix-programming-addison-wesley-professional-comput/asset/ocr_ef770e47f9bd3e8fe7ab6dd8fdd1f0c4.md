# Chapter 1: Fundamental Concepts

```
```
struct timespec—structure for time in seconds and nanoseconds
    struct timespec {
        time_t tv_sec;      /* seconds */
        long tv_nsec;       /* nanoseconds */
    };
```
```

There are three primary functions for measuring a time interval, *gettimeofday*, detailed in the previous section, *clock*, and *times*. The latter two and the structure used by *times* are:

```
```
clock—get execution time
    #include <time.h>
    clock_t clock(void);
    /* Returns time in CLOCKS_PER_SEC or -1 on error (errno not defined) */
```
```

```
```
times—get process and child-process execution times
    #include <sys/times.h>
    clock_t times(
        struct tms *buffer  /* returned times */
    );
    /* Returns time in clock ticks or -1 on error (sets errno) */
```
```

```
```
struct tms—structure for times system call
    struct tms {
        clock_t tms_utime;      /* user time */
        clock_t tms_cutime;     /* user time of terminated children */
        clock_t tms_stime;      /* sys time */
        clock_t tms_cstime;     /* sys time of terminated children */
    };
```
```

*times* returns the time elapsed since some point in the past (usually since the system was booted), sometimes called the *wall-clock* or *real* time. This is different from the time returned from the functions in the previous section, which returned the time since the epoch (normally 1-Jan-1970).

*times* uses units of clock ticks; you get the number of clock ticks per second with *sysconf* (Section 1.5.5) like this:

```
```
clock_ticks = sysconf(_SC_CLK_TCK);
```
```

Additionally, *times* loads the *tms* structure with more specific information: