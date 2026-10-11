Lines 77–84 are indicative of the kinds of complications found in the real world. Here, one particular Unix variant can't handle count values greater than INT_MAX, so lines 83–84 perform two operations at once: reducing the count to below INT_MAX and keeping the amount a multiple of 8192. The latter operation maintains the efficiency of the I/O operations: Doing I/O in multiples of the fundamental disk block size is always more efficient than doing it in odd amounts. As the comment notes, the code maintains the semantics of read() and write(), where the returned count may be less than the requested count.

Note that the count parameter can indeed be greater than INT_MAX, since count is a size_t, which is unsigned. INT_MAX is a plain int, which on all modern systems is signed.

Lines 86–90 are the actual loop, performing the operation repeatedly, as long as it fails with EINTR. The IS_EINTR() macro isn't shown, but it handles the case for systems on which EINTR isn't defined. (There must be at least one out there or the code wouldn't bother setting up the macro; it was probably done for a Unix or POSIX emulation on top of a non-Unix system.)

Here is safe_write.c:

```
1 /* An interface to write that retries after interrupts.
   Copyright (C) 2002 Free Software Foundation, Inc.
17 ... lots of boilerplate stuff omitted ...
18 #define SAFE_WRITE
19 #include "safe-read.c"
```

The #define on line 18 defines SAFE_WRITE; this ties in to lines 57–60 in safe-read.c.

# 10.4.4.2 GLIBC Only: TEMP_FAILURE_RETRY() 

The GLIBC <unistd.h> file defines a macro, TEMP_FAILURE_RETRY(), that you can use to encapsulate any system call that can fail and set errno to EINTR. Its “de-claration” is as follows:

```
#include <unistd.h>                       GLIBC
long int TEMP_FAILURE_RETRY(expression);
```

Here is the macro's definition: