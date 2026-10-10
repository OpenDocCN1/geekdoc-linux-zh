```
if (p != NULL)
    tstruct.tm_year = atoi(p);
else
    continue;
okay = 1;
}
while(!okay);

tstruct.tm_hour = 0;

tstruct.tm_min = 0;
tstruct.tm_sec = 1;
tstruct.tm_isdst = -1;

/* Now get day of the week */
if (mktime(&tstruct) == -1)
tstruct.tm_wday = 7;

printf ("That was %s\n",wday[tstruct.tm_wday]);
}
```

The mktime( ) function also makes the necessary adjustments for values out of range. This capability can be utilized for discovering what the date will be in $n$ number of days, as shown here:

```
#include <stdio.h>
#include <time.h>
include <string.h>

void main()
{
    struct tm *tstruct;
    time_t today;
    
    today = time(NULL);
    tstruct = localtime(&today);
    
    tstruct->tm_mday += 10;
    mktime(tstruct);
    
    printf ("In ten days it will be %02d/%02d/%2d\n", tstruct->tm_mday,tstruct->tm_mon + 1,tstruct->tm_year);
}
```

# Header Files

Function prototypes for library functions supplied with the C compiler, and standard macros, are declared in header files. The ANSI standard on the C programming language lists the following header files:

| HEADER | DESCRIPTION |
| :----- | :---------- |
|        |             |