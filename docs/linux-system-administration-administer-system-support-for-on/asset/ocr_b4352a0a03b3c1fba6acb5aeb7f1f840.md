# itimer.c

An *interval timer* (itimer.c) helps set the system clock and other Linux timing functions, as shown in Listing 6–8.

# **Listing 6–8: Using itimer.c**

```
```
/*
 * linux/kernel/itimer.c
 *
 * Copyright (C) 1992 Darren Senn
 */

/* These are all the functions necessary to implement itimers */

#include <linux/signal.h>
#include <linux/sched.h>
#include <linux/string.h>
#include <linux/errno.h>
#include <linux/time.h>
#include <linux/mm.h>

#include <asm/segment.h>

/*
 * change timeval to jiffies, trying to avoid the
 * most obvious overflows..
 *
 * The tv_sec values are signed, but nothing seems to
 * indicate whether we really should use them as signed values
 * when doing itimers. POSIX doesn't mention this (but if
 * alarm() uses itimers without checking, we have to use unsigned
 * arithmetic).
 */

static unsigned long tvo2jiffies(struct timeval *value)
{
   unsigned long sec = (unsigned) value->tv_sec;
   unsigned long usec = (unsigned) value->tv_usec;

   if (sec > (ULONG_MAX / HZ))
      return ULONG_MAX;
   usec += 1000000 / HZ - 1;
   usec /= 1000000 / HZ;
   return HZ*sec+usec;
}
```
```