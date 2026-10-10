```
		
	    newtm->tm_yday); 
    printf("   Daylight time=%d\n", 
            newtm->tm_isdst); 
    printf("   Offset from GMT=%d\n", 
            newtm->tm_gmtoff / 3600); 
    printf("   Time zone=%s\n", 
            newtm->tm_zone); 
    printf("\n"); 
    binarytime = INT_MIN; 
    printf("minimum=%s", ctime(&binarytime)); 
    binarytime = INT_MAX; 
    printf("maximum=%s", ctime(&binarytime)); 
}
```

The call to the function `time()` returns the 32-bit integer representing the current time. This is a convenient form because it is easy to adjust by addition and subtraction, and it only requires four bytes for storage. The call to `ctime()` converts the time into a string that is always 25 characters long— the 24 visible characters with a newline character at the end.

Another storage format for time data is the `tm` struct. In this example, the call to `localtime()` converts the binary time into a `tm` struct. The struct has one field for each piece of information:

```
struct tm
{
    int tm_sec;      /* Seconds [0-60] (1 leap second) */
    int tm_min;      /* Minutes [0-59] */
    int tm_hour;     /* Hours [0-23] */
    int tm_mday;     /* Day [1-31] */
    int tm_mon;      /* Month [0-11] */
    int tm_year;     /* Year - 1900. */
    int tm_wday;     /* Day of week [0-6] */
    int tm_yday;     /* Days in year [0-365]      */
    int tm_isdst;    /* Daylight time [-1/0/1]*/
    long int tm_gmtoff; /* Seconds east of UTC. */
    const char *tm_zone; /* Timezone abbreviation. */
};
```

The months of the year are numbered 0 through 11, with January being the 0 month. The year is stored by subtracting 1900 from the actual year value (this is left over from an earlier version of `tm` in which each field was a single byte). The days of the week are numbered beginning with Sunday as 0, Monday as 1, and so on. The daylight time indicator is set to 1 if daylight time is in effect, 0 if it is not, and -1 if it cannot be determined. The offset from *UTC (Universal Time Coordinate)*, or *Greenwich Mean Time*, is in seconds because there are places that adjust local times by amounts smaller than an hour. The time zone is specified as an ASCII string.