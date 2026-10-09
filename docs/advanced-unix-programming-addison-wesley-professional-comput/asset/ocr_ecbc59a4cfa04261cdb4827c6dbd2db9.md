Note that unlike `_POSIX_SOURCE`, `_POSIX_C_SOURCE` has a value which is normally a long integer formed from the year and month when the standard was approved (June 1995 in the example). The other possible long integer is 200112L. But for POSIX1990, you set it to 1, not to 199009L.¹⁴

If you’re interested in going beyond POSIX into SUS, which you will be if you’re using a commercial UNIX system, there’s a separate symbol for that, `_XOPEN_SOURCE`, and two special numbers for it: 500 for SUS2, and 600 for SUS3. So, if you want to use what’s in a SUS2, UNIX 98-branded system, you do this:

```
```
#define _POSIX_SOURCE
#define _POSIX_C_SOURCE 199506L
#define _XOPEN_SOURCE 500
#include <sys/types.h>
#include <unistd.h>
```
```

For SUS1, you define `_XOPEN_SOURCE` without a value, and also define `_XOPEN_SOURCE_EXTENDED` as 1:

```
```
#define _POSIX_SOURCE
#define _POSIX_C_SOURCE 2
#define _XOPEN_SOURCE
#define _XOPEN_SOURCE_EXTENDED 1
#include <unistd.h>
```
```

Technically, you don’t need to define the first two POSIX symbols if you really have a SUS2 system, since they will be defined automatically. But, the source you’re writing may be used on an older system, and you need to tell it that you want POSIX in terms it will understand. `_POSIX_C_SOURCE` should use 2 when `_XOPEN_SOURCE` is defined with no value, 199506L when it’s 500, and 200112L when it’s 600.

Are you lost? Too bad, because it gets much worse. To help a little, here’s a summary of what to do:

+   - Decide what level of standardization your program is written to expect.
+   - If it’s only POSIX1990, define only `_POSIX_SOURCE`.
+   - If it’s POSIX1993 or POSIX1996, define both `_POSIX_SOURCE` and `_POSIX_C_SOURCE`, and use the appropriate number from Table 1.2 in Section 1.5.1.

¹⁴. Or you can set it to 2 if you also want the C bindings from 1003.2-1992.