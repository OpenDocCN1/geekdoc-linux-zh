+   * If it's SUS1, SUS2, or SUS3, define `_XOPEN_SOURCE` (to nothing, to 500, or to 600) and also use the two POSIX symbols with the appropriate numbers.
+   * For SUS1, also define `_XOPEN_SOURCE_EXTENDED` as 1.
+   * Forget about XPG3 (and XPG4, which I haven't even mentioned)—you have enough to worry about already.

It's easy to write a header file that sets the various request symbols based on a single definition that you see before including it. Here's the header `suvreg.h`.[^15] I'll show how it's used in the next section:

```
```
/*
   Header to request specific standard support. Before including it, one
   of the following symbols must be defined (1003.1-1988 isn't supported):

   SUV_POSIX1990    for 1003.1-1990
   SUV_POSIX1993    for 1003.1b-1993 - real-time
   SUV_POSIX1996    for 1003.1-1996
   SUV_SUS1         for Single UNIX Specification, v. 1 (UNIX 95)
   SUV_SUS2         for Single UNIX Specification, v. 2 (UNIX 98)
   SUV_SUS3         for Single UNIX Specification, v. 3 (UNIX 03)
*/

#if defined(SUV_POSIX1990)
#define  _POSIX_SOURCE
#define  _POSIX_C_SOURCE 1

#elif defined(SUV_POSIX1993)
#define  _POSIX_SOURCE
#define  _POSIX_C_SOURCE 199309L

#elif defined(SUV_POSIX1996)
#define  _POSIX_SOURCE
#define  _POSIX_C_SOURCE 199506L

#elif defined(SUV_SUS1)
#define  _POSIX_SOURCE
#define  _POSIX_C_SOURCE 2
#define  _XOPEN_SOURCE
#define  _XOPEN_SOURCE_EXTENDED 1

#elif defined(SUV_SUS2)
#define  _POSIX_SOURCE
#define  _POSIX_C_SOURCE 199506L
#define  _XOPEN_SOURCE 500
#define  _XOPEN_SOURCE_EXTENDED 1
```
```

> 15.  It's pronounced “S-U-V wreck.” SUV is for Standard UNIX Version. What did you think it was?