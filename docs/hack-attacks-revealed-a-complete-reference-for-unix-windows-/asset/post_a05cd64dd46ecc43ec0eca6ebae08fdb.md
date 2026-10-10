
Here is a simple implementation of a case-insensitive version of `strstr()`. The function simply makes a copy of the parameter strings, converts those copies to uppercase, then does a standard `strstr()` on the copies. The offset of the target string within the source string will be the same for the copy as the original, and so it can be returned relative to the parameter string:

```c
char *stristr(char *s1, char *s2)
{
    char c1[1000];
    char c2[1000];
    char *p;

    strcpy(c1, s1);
    strcpy(c2, s2);

    strupr(c1);
    strupr(c2);

    p = stristr(c1, c2);
    if (p)
        return s1 + (p - c1);
    return NULL;
}
```

This function scans a string, `s1`, looking for the word held in `s2`. The word must be a complete word, not simply a character pattern, for the function to return TRUE. It makes use of the `stristr()` function described previously:

```c
int word_in(char *s1, char *s2)
{
    /* return non-zero if s2 occurs as a word in s1 */
    char *p;
    char *q;
    int ok;

    ok = 0;
    q = s1;

    do
    {
        /* Locate character occurrence s2 in s1 */
        p = stristr(q, s2);
        if (p)
        {
            /* Found */
            ok = 1;

            if (p > s1)
            {
                /* Check previous character */
                if (*(p - 1) >= 'A' && *(p - 1) <= 'z')
                    ok = 0;
            }

            /* Move p to end of character set */
            p += strlen(s2);

            if (*p)
            {
                /* Check character following */
                if (*p >= 'A' && *p <= 'z')
                    ok = 0;
            }
            q = p;
        }
    } while (p && !ok);
    return ok;
}
```

More useful functions for dealing with text are the following: `truncstr()`, which truncates a string:

```c
void truncstr(char *p, int num)
{
    /* Truncate string by losing last num characters */
    if (num < strlen(p))
        p[strlen(p) - num] = 0;
}
```

`trim()`, which removes trailing spaces from the end of a string:

```c
void trim(char *text)
{
    /* remove trailing spaces */
    char *p;

    p = &text[strlen(text) - 1];
    while (*p == 32 && p >= text)
        *p-- = 0;
}
```

`strlench()`, which changes the length of a string by adding or deleting characters:

```c
void strlench(char *p, int num)
{
    /* Change length of string by adding or deleting characters */

    if (num > 0)
        memmove(p + num, p, strlen(p) + 1);
    else
    {
        num = 0 - num;
        memmove(p, p + num, strlen(p) + 1);
    }
}
```

`strins()`, which inserts a string into another string:

```c
void strins(char *p, char *q)
{
    /* Insert string q into p */
    strlench(p, strlen(q));
    strncpy(p, q, strlen(q));
}
```

and `strchg()`, which replaces all occurrences of one substring with another within a target string:

```c
void strchg(char *data, char *s1, char *s2)
{
    /* Replace all occurrences of s1 with s2 */
    char *p;
    char changed;

    do
    {
        changed = 0;
        p = strstr(data, s1);
        if (p)
        {
            /* Delete original string */
            strlench(p, 0 - strlen(s1));

            /* Insert replacement string */
            strins(p, s2);
            changed = 1;
        }
    } while (changed);
}
```

## Time

C provides the `time()` function to read the computer's system clock and return the system time as a number of seconds since midnight January 1, 1970. This value can be converted to a useful string with the function `ctime()`, as illustrated:

```c
#include <stdio.h>
#include <time.h>

int main()
{
    /* Structure to hold time, as defined in time.h */
    time_t t;

    /* Get system date and time from computer */
    t = time(NULL);
    printf("Today's date and time: %s\n", ctime(&t));
}
```

The string returned by `ctime()` is composed of seven fields:

- Day of the week
- Month of the year
- Date of the day of the month
- Hour
- Minutes
- Seconds
- Century

These are terminated by a newline character and null-terminating byte. Since the fields always occupy the same width, slicing operations can be carried out on the string with ease. The following program defines a structure, `time`, and a function, `gettime()`, which extracts the hours, minutes, and seconds of the current time, and places them in the structure:

```c
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

The ANSI standard on C does provide a function to convert the value returned by `time()` into a structure, as shown in the following snippet. Also note the structure `tm` is defined in `time.h`:

```c
#include <stdio.h>
#include <time.h>

int main()
{
    time_t t;
    struct tm *tb;

    /* Get time into t */
    t = time(NULL);

    /* Convert time value t into structure pointed to by tb */
    tb = localtime(&t);

    printf("\nTime is %02d:%02d:%02d", tb->tm_hour, tb->tm_min, tb->tm_sec);
}

struct tm
{
    int tm_sec;
    int tm_min;
    int tm_hour;
    int tm_mday;
    int tm_mon;
    int tm_year;
    int tm_wday;
    int tm_yday;
    int tm_isdst;
};
```

## Timers

Often a program must determine the date and time from the host computer’s nonvolatile RAM. Several time functions are provided by the ANSI standard on C that enable a program to retrieve the current date and time. First, `time()` returns the number of seconds that have elapsed since midnight on January 1, 1970. It has the prototype:

```c
time_t time(time_t *timer);
```

Here, `time()` fills in the `time_t` variable, sent as a parameter, and returns the same value. You can call `time()` with a NULL parameter and collect the return value, as in:

```c
#include <time.h>

void main()
{
    time_t now;

    now = time(NULL);
}
```

Here, `asctime()` converts a time block to a twenty-six character string of the format. The `asctime()` function has the prototype:

```c
char *asctime(const struct tm *tblock);
```

Next, `ctime()` converts a time value (as returned by `time()`) into a 26-character string of the same format as `asctime()`. For example:

```c
#include <stdio.h>
#include <time.h>

void main()
{
    time_t now;
    char date[30];

    now = time(NULL);
    strcpy(date, ctime(&now));
}
```

Another time function, `difftime()`, returns the difference, in seconds, between two values (as returned by `time()`). This can be useful for testing the elapsed time between two events, the time a function takes to execute, and for creating consistent delays that are extraneous to the host computer. An example delay program would be:

```c
#include <stdio.h>
#include <time.h>

void DELAY(int period)
{
    time_t start;

    start = time(NULL);
    while (time(NULL) < start + period)
        ;
}

void main()
{
    printf("\nStarting delay now... (please wait 5 seconds)");

    DELAY(5);

    puts("\nOkay, I've finished!");
}
```

The `gmtime()` function converts a local time value (as returned by `time()`) to the GMT time, and stores it in a time block. This function depends upon the global variable time zone being set. The time block is a predefined structure (declared in *time.h*) as follows:

```c
struct tm
{
    int tm_sec;
    int tm_min;
    int tm_hour;
    int tm_mday;
    int tm_mon;
    int tm_year;
    int tm_wday;
    int tm_yday;
    int tm_isdst;
};
```

Here, `tm_mday` records the day of the month, ranging from 1 to 31; `tm_wday` is the day of the week, with Sunday being represented by 0; the year is recorded from 1900 on; `tm_isdst` is a flag to show whether daylight savings time is in effect. The actual names of the structure and its elements may vary from compiler to compiler, but the structure should be the same.

The `mktime()` function converts a time block to a calendar format. It follows the prototype:

```c
time_t mktime(struct tm *t);
```

The following example allows entry of a date, and uses `mktime()` to calculate the day of the week appropriate to that date. Only dates from January 1, 1970 to the present are recognizable by the time functions:

```c
#include <stdio.h>
#include <time.h>
#include <string.h>

void main()
{
    struct tm tstruct;
    int okay;
    char data[100];
    char *p;
    char *wday[] = { "Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday",
    "prior to 1970, thus not known" };

    do
    {
        okay = 0;
        printf("\nEnter a date as dd/mm/yy ");
        p = fgets(data, 8, stdin);
        p = strtok(data, "/");

        if (p != NULL)
            tstruct.tm_mday = atoi(p);
        else
            continue;

        p = strtok(NULL, "/");
        if (p != NULL)
            tstruct.tm_mon = atoi(p);
        else
            continue;

        p = strtok(NULL, "/");
    } while (1);
}
```
