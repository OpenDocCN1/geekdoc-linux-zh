
This solves the first problem.

## 2.6.6.2 Displaying Login Time in Human-Readable Form

Solving the second problem requires an understanding of how calendar, or universal, time is represented in UNIX systems and what functions are provided in the API for manipulating time values.

UNIX represents time as the number of seconds elapsed since 12:00 A.M., January 1, 1970, Coordinated Universal Time (UTC), known as the “Epoch”. UTC is essentially like Greenwich Meridian Time except that it includes occasional “leap seconds” to synchronize with the earth’s rotation. UNIX stores time in objects of type time_t, the implementation of which is not standardized. On many systems time_t is a typedef for a 32-bit integer. Such implementations will fail in the year 2038, when it overflows. Representing time as an integer number of seconds since the Epoch makes it easy for the kernel to update times, but not very easy for a human to determine the time.

How can we learn more about UNIX time and the various parts of the API related to it? The answer again is to do a man page search. If you search on the keyword “time” you will find too many man pages that refer to time. A second keyword will be needed to refine the search. Perhaps “convert” or “transform” or something similar, to capture functions that transform time from one form to another. Trying

```sh
$ man -k time | grep transform
```

we will see several functions related to time, including ctime() and localtime(). The man page will also include reference to the header file, <time.h>, which must be included for most of these functions. These functions share a single man page. Reading this page reveals that ctime() converts a time_t time into a human readable string of the form

```text
"Mon Aug 11 23:12:06 2003\n"
```

To be precise, the ctime() function is declared as

```c
char *ctime(const time_t *clock);
```

Observe that the argument is the address of a time_t value, not the value itself. The return value is a pointer to a string consisting of a 3-letter day abbreviation, a 3-letter month abbreviation, the day of the month, the 24-hour time in hours, minutes, and seconds, and the 4-digit year. The string is allocated statically by ctime(), so it might be overwritten by other calls, so it is best to copy it into a local variable if it needs to be available at a later time.

*Note 1.* ctime() is one of many functions that return a pointer to a string that is allocated statically. Make sure that you understand what this means. The string itself is allocated by ctime() and a pointer to that memory is returned to the caller. Subsequent calls to ctime() will overwrite the previously allocated memory. The caller will be unable to retrieve the old value unless it was copied.

¹¹ The abbreviation UTC is a compromise between the English and French abbreviations. In English, it would be CUT and in French, TUC.
¹² The earth’s rotation can vary due to astronomical conditions. UNIX systems are not required by POSIX to represent exact UTC; they are allowed to ignore the leap seconds.

to a local. Also, the caller is not responsible for freeing the memory allocated to the string; that is handled by the library. This is just one of many functions that are not thread-safe, a topic we discuss below.

The localtime() function takes a time_t argument but returns a pointer to a struct tm, which is a structure whose members are the various components of time, such as the day-of-week, the month, day, and year, and so on.

If you read through the man page carefully, which you should, you will find near the end the conformance section. It states:

```
CONFORMING TO
POSIX.1-2001.  C89 and C99 specify asctime(), ctime(), gmtime(), localtime(),
and mktime().  POSIX.1-2008 marks asctime(), asctime_r(), ctime(), and ctime_r()
as obsolete, recommending the use of strftime(3) instead.
```

The ctime() function is disparaged at this point. One should instead use strftime(), whose prototype is

```c
#include <time.h>
size_t strftime(char *s, size_t max, const char *format, const struct tm *tm);
```

This function, unlike ctime(), allows the calling program to specify the format of the character string to be created. It is also safer to use in that the string is passed as an argument to the function, allocated by the caller, instead of allocated statically and returned as the function value. The first argument is a pointer to the string to be filled, the second, the size of the array of chars to fill, the third is a format for the string, and the last is the tm structure containing the broken down time representation.

The format specification is described in great detail in the man page for the function. It is similar to the format for the printf() function in that it is a string literal enclosed in double-quotes, with conversion specifications of the form %x, where x is a character to be replaced. For example, %M represents minutes as a decimal number in the range 00 to 59. and %b is the abbreviation of the month name in the current locale. This phrase, "in the current locale" means that the locale settings of the user are used in deciding the exact string that %b will produce. Every user has a locale in UNIX. The topic of locales will be covered in a later section. The important point now is that strftime(), unlike ctime(), can use locale information in determining the format of the output string. In chapter 3 we will use this function to display time with more control. For our implementation of the who command, we will use ctime().

The who program only displays the date, hours and minutes. For the above example, it would display only "Aug 11 23:12". Our implementation of who must extract this substring from the larger string. In other words, given

```
"Mon Aug 11 23:12:06 2003\n"
```

it needs to print

```
"Aug 11 23:12"
```
