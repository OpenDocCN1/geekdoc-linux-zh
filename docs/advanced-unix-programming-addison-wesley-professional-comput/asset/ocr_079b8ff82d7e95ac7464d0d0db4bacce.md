# **struct tm**—structure for broken-down time

```
```
struct tm {
	int tm_sec;	/* second [0,61] (up to 2 leap seconds) */
	int tm_min;	/* minute [0,59] */
	int tm_hour;	/* hour [0,23] */
	int tm_mday;	/* day of month [1,31] */
	int tm_mon;	/* month [0,11] */
	int tm_year;	/* years since 1900 */
	int tm_wday;	/* day of week [0,6] (0 = Sunday) */
	int tm_yday;	/* day of year [0,365] */
	int tm_isdst;	/* daylight-savings flag */
};
```
```

# **struct timeval**—structure for gettimeofday

```
```
struct timeval {
	time_t tv_sec;	/* seconds */
	useconds_t tv_usec;	/* microseconds */
};
```
```

# **time**—get current date and time as **time_t**

```
```
#include <time.h>

time_t time(
	time_t *t		/* NULL or returned time */
);
/* Returns time or -1 on error (errno not defined) */
```
```

# **gettimeofday**—get current date and time as **timeval**

```
```
#include <sys/time.h>

int gettimeofday(
	struct timeval *tvalbuf,	/* returned time */
	void *dummy		/* always NULL */
);
/* Returns 0 on success or -1 (maybe) on error (may set errno) */
```
```

# **localtime**—convert **time_t** to local broken-down time

```
```
#include <time.h>

struct tm *localtime(
	const time_t *t		/* time */
);
/* Returns broken-down time or NULL on error (sets errno) */
```
```

# **gmtime**—convert **time_t** to UTC broken-down time

```
```
#include <time.h>

struct tm *gmtime(
	const time_t *t		/* time */
);
/* Returns broken-down time or NULL on error (sets errno) */
```
```