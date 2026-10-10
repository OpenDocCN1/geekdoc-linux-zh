+   * Day of the week
+   * Month of the year
+   * Date of the day of the month
+   * Hour
+   * Minutes
+   * Seconds
+   * Century

These are terminated by a newline character and null-terminating byte. Since the fields always occupy the same width, slicing operations can be carried out on the string with ease. The following program defines a structure, time, and a function, gettime(), which extracts the hours, minutes, and seconds of the current time, and places them in the structure:

```
```
#include <stdio.h>
#include <time.h>

struct time
{
    int ti_min;      /* Minutes */
    int ti_hour;     /* Hours */
    int ti_sec;      /* Seconds */
};

void gettime(struct time *now)
{
    time_t t;
    char temp[26];
    char *ts;

    /* Get system date and time from computer */
    t = time(NULL);

    /* Translate date and time into a string */
    strcpy(temp, ctime(&t));

    /* Copy out just time part of string */
    temp[19] = 0;

    ts = &temp[11];

    /* Scan time string and copy into time structure */
    sscanf(ts, "%2d:%2d:%2d", &now->ti_hour, &now->ti_min, &now->ti_sec);
}

int main()
{
    struct time now;

    gettime(&now);

    printf("\nThe time is %02d:%02d:%02d",
           now.ti_hour, now.ti_min, now.ti_sec);
}
```
```