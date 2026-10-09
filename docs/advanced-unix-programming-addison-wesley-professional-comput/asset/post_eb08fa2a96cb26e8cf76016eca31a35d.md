
- daylight is set to zero (false) if Daylight Savings Time should never be applied to the time zone, and non-zero (true) if it should. The switchover periods are built into the library functions in an implementation-defined way.
- timezone is set to the difference in seconds between UTC and local standard time. (Divide it by 3,600 to get the difference in hours.)
- tzname is an array of two strings, tzname[0] to be used to designate the local time zone during standard time, and tzname[1] for Daylight Savings Time.

The three globals were not in POSIX earlier than POSIX 2002 and are not defined on FreeBSD or Darwin. But usually you don't need to call tzset or interrogate the globals directly. The standard functions do that as needed.

Here's an example anyway:

```c
tzset();
printf("daylight = %d; timezone = %ld hrs.; tzname = %s/%s\n",
       daylight, timezone / 3600, tzname[0], tzname[1]);
```

with this output:

```
daylight = 1; timezone = 7 hrs.; tzname = MST/MCT
```

For all the details of how all the calendar-time functions are used, especially the ones that involve format strings, see [SUS2002] or a good book on Standard C, such as [Har2002]. Here are some miscellaneous points to keep in mind:

- Ignoring the possibility of an error return, ctime(t) is defined as asctime(localtime(t)).
- The tm_sec field of the tm structure can go to 61 (instead of just 59), to allow for occasional leap seconds.
- The tm_year field of the tm structure is an offset from 1900. It's still perfectly Y2K compatible, just strange (2002 is represented as 102).
- Just as strangely, ctime and asctime put a newline at the end of the output string.
- Several functions take a pointer to a time_t, when a call-by-value time_t would work as well. This is a holdover from the earliest days of UNIX when the C language didn't have a long data type and you had to pass in an array of two 16-bit ints.
- The `time_t` pointer argument to `time` is totally unnecessary and should just be `NULL`. It looks like it supplies a buffer for `time` to use, but no buffer is needed, as the returned `time_t` is an arithmetic type.
- All of the functions presented here that return a pointer to a `tm` structure use a static buffer internally on most implementations, so use the buffer or copy it before you call another such function. There are re-entrant forms with an `_r` suffix that you can use in a multithreaded program if you need to.
- The functions that use `formats`, `strftime`, `wcsftime`, `getdate`, and `strptime` are very complicated, but very powerful, and are well worth learning. The first two are in Standard C; the last two are in the SUS. `getdate` is not in FreeBSD or Darwin, although there is a version of it in the GNU C library that you can install if you want.
- Use `getdate` to get dates and times that users type in, and `strptime` or `getdate` when reading data files containing dates. The reason is that `strptime` takes only a single format, which makes it too difficult for users to format the date and time correctly. `getdate` uses a whole list of formats and tries them one-by-one looking for a match.

### 1.7.2 Execution Time

Execution time is used to measure timing intervals and process-execution times, and for accounting records. The kernel automatically records each process’s execution time. Interval times come in various subsecond units ranging from nanoseconds to hundredths of a second.

The execution-time types and functions are just as confusing as those for calendar time. First, here are the principal types:

- `clock_t`, in Standard C, an arithmetic type (typically a `long`, but don’t assume so) which is a time interval in units of `CLOCKS_PER_SEC` or clock ticks
- `struct timeval`, which holds an interval in seconds and microseconds (also used for calendar time, and explained in detail in the previous section)
- `struct timespec`, which holds an interval in seconds and nanoseconds

Here’s the structure for `timespec` (we already showed `timeval`), which is defined in the header `<time.h>`:

```c
struct timespec {
    time_t tv_sec;      /* seconds */
    long tv_nsec;       /* nanoseconds */
};
```

There are three primary functions for measuring a time interval, *gettimeofday*, detailed in the previous section, *clock*, and *times*. The latter two and the structure used by *times* are:

```c
#include <time.h>
clock_t clock(void);
/* Returns time in CLOCKS_PER_SEC or -1 on error (errno not defined) */
```

```c
#include <sys/times.h>
clock_t times(
    struct tms *buffer  /* returned times */
);
/* Returns time in clock ticks or -1 on error (sets errno) */
```

```c
struct tms {
    clock_t tms_utime;      /* user time */
    clock_t tms_cutime;     /* user time of terminated children */
    clock_t tms_stime;      /* sys time */
    clock_t tms_cstime;     /* sys time of terminated children */
};
```

*times* returns the time elapsed since some point in the past (usually since the system was booted), sometimes called the *wall-clock* or *real* time. This is different from the time returned from the functions in the previous section, which returned the time since the epoch (normally 1-Jan-1970).

*times* uses units of clock ticks; you get the number of clock ticks per second with *sysconf* (Section 1.5.5) like this:

```c
clock_ticks = sysconf(_SC_CLK_TCK);
```

Additionally, *times* loads the *tms* structure with more specific information:

- tms_utime (user time) is the time spent executing instructions from the process's user code. It's CPU time only and doesn't include time spent waiting to run.
- tms_stime (system time) is the CPU time spent executing system calls on behalf of the process.
- tms_cutime (child user time) is the total of user CPU times for all the process's child processes that have terminated and for which the parent has issued a wait system call (explained fully in Chapter 5).
- tms_cstime (child system time) is the total of system CPU times for terminated and waited-for child processes.

Although clock returns the same type as times, the value is CPU time used since the process started, not real time, and the units are given by the macro CLOCKS_PER_SEC, not clock ticks. It's equivalent (except for the different units) to tms_utime + tms_stime.

CLOCKS_PER_SEC is defined in the SUS as 1,000,000 (i.e., microseconds), but non-SUS systems may use a different value, so always use the macro. (FreeBSD defines CLOCKS_PER_SEC as 128; Darwin as 100.)

If clock_t is a 32-bit signed integer, which it often is, and uses units of microseconds, it wraps after about 36 minutes, but at least clock starts timing when the process starts. times, operating in clock ticks, can run longer, but it also starts earlier—much earlier if the UNIX system has been running for weeks or months, which is very common. Still, a 32-bit signed clock_t operating in units of ticks won't wrap for about 250 days, so a semiannual reboot, if you can arrange for one, solves the problem.

However, you can't assume that clock_t is a 32-bit signed integer, or that it's signed, or even that it's an integer. It could be an unsigned long, or even a double.

We'll use times throughout this book to time various programs because it gives us the real time and the user and system CPU times all at once. Here are two handy functions that we'll use—one to start timing, and one to stop and print the results:

```c
#include <sys/times.h>

static struct tms tbuf1;
static clock_t real1;
static long clock_ticks;

void timestart(void)
{
    ec_negl( real1 = times(&tbuf1) )
    /* treat all -1 returns as errors */
    ec_negl( clock_ticks = sysconf(_SC_CLK_TCK) )
    return;

EC_CLEANUP_BGN
    EC_FLUSH("timestart");
EC_CLEANUP_END
}

void timestep(char *msg)
{
    struct tms tbuf2;
    clock_t real2;

    ec_negl( real2 = times(&tbuf2) )
    fprintf (stderr,"%s:\n\tTotal (user/sys/real)=%2.2f, %2.2f, %2.2f\n"
             "\t  Child (user/sys)=%2.2f, %2.2f\n", msg,
             ((double)(tbuf2.tms_utime + tbuf2.tms_cutime) -
               (tbuf1.tms_utime + tbuf1.tms_cutime)) / clock_ticks,
             ((double)(tbuf2.tms_stime + tbuf2.tms_cstime) -
               (tbuf1.tms_stime + tbuf1.tms_cstime)) / clock_ticks,
             (double)(real2 - real1) / clock_ticks,
             (double)(tbuf2.tms_cutime - tbuf1.tms_cutime) / clock_ticks,
             (double)(tbuf2.tms_cstime - tbuf1.tms_cstime) / clock_ticks);
    return;

EC_CLEANUP_BGN
    EC_FLUSH("timestep");
EC_CLEANUP_END
}
```

When we want to time something, we just call `timestart` at the beginning of the interval and `timestep` at the end, as in this example, which also includes calls to `gettimeofday` and `clock` for a comparison:

```c
#define REPS 1000000
#define TV_SUBTRACT(t2, t1) \
    ((double)(t2).tv_sec + (t2).tv_usec / 1000000.0 - \
     ((double)(t1).tv_sec + (t1).tv_usec / 1000000.0)

int main(void)
{
    int i;
    char msg[100];
    clock_t c1, c2;
    struct timeval tv1, tv2;
```
