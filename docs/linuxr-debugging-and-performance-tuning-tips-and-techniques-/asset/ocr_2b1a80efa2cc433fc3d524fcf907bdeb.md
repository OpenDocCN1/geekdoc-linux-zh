When run, this program produces output of the form: 'Thu May 22 15:44:21 2003'. The terminating newline is included in the result. To be more precise, the return value points to an array of 26 characters, as shown in Figure 6.1.

![](bbox=[0.09, 0.21, 0.91, 0.27])

**FIGURE 6.1 Return string from ctime() and asctime()**

Much older Unix code relies on the fact that the values have a fixed position in the returned string. When using these routines, remember that they include a trailing newline. Thus, the small example program uses a simple "\%s" format string for printf(), and not "\%s\n", as might be expected.

```
ctime() saves you the step of calling localtime(); it's essentially equivalent to
time_t now;
char *curtime;

time(& now);
curtime = asctime(localtime(& now));
```

# 6.1.3.2 Complex Time Formatting: strftime()

While asctime() and ctime() are often adequate, they are also limited:

+   - The output format is fixed. There's no way to rearrange the order of the elements.
+   - The output does not include time-zone information.
+   - The output uses abbreviated month and day names.
+   - The output assumes English names for the months and days.

For these reasons, C89 introduced the strftime() standard library routine:

```
#include <time.h>

size_t strftime(char *s, size_t max, const char *format,
const struct tm *tm);

strftime() is similar to sprintf(). The arguments are as follows:

char *s
A buffer to hold the formatted string.
```