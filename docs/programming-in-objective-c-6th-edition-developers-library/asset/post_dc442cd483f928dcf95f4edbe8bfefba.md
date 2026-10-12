
### 代码示例：计算明天的日期与闰年判断

```c
}
else {
            // end of month
	tomorrow.day = 1;
	tomorrow.month = today.month + 1;
	tomorrow.year = today.year;
}

printf ("Tomorrow's date is %i/%i/%.2i.\n",tomorrow.month,
	tomorrow.day, tomorrow.year % 100);

return 0;
}
```

```c
// Function to find the number of days in a month

int numberOfDays (struct date d)
{
	int	days;
	bool isLeapYear (struct date d);
	const int daysPerMonth[12] =
	{ 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31 };

	if ( isLeapYear (d) == true && d.month == 2 )
		days = 29;
	else
		days = daysPerMonth[d.month - 1];

	return days;
}
```

```c
// Function to determine if it's a leap year

bool isLeapYear (struct date d)
{
	bool leapYearFlag;

	if ( (d.year % 4 == 0 && d.year % 100 != 0) ||
		d.year % 400 == 0 )
		leapYearFlag = true; // It's a leap year
	else
		leapYearFlag = false; // Not a leap year

	return leapYearFlag;
}
```

**输出示例：**

Enter today's date (mm dd yyyy): 2 28 2016  
Tomorrow's date is 2/29/16.

Enter today's date (mm dd yyyy): 2 28 2014  
Tomorrow's date is 3/1/14.

```c
int numberOfDays (struct date d);
```

```c
if ( today.day != numberOfDays (today) )
```

```c
int numberOfDays (struct date d)
```

```c
if ( isLeapYear (d) == true && d.month == 2 )
```

### 完整程序：确定明天的日期

```c
// Program to determine tomorrow's date
#include <stdio.h>
#include <stdbool.h>

struct date
{
int month;
int day;
int year;
};

// Function to calculate tomorrow's date
struct date dateUpdate (struct date today)
{
struct date tomorrow;
int numberOfDays (struct date d);

if ( today.day != numberOfDays (today)) {
tomorrow.day = today.day + 1;
tomorrow.month = today.month;
tomorrow.year = today.year;
}
else if ( today.month == 12 ) { // end of year
tomorrow.day = 1;
tomorrow.month = 1;
tomorrow.year = today.year + 1;
}
else {                        // end of month
	tomorrow.day = 1;
	tomorrow.month = today.month + 1;
	tomorrow.year = today.year;
}

	return tomorrow;
}

// Function to find the number of days in a month

int numberOfDays (struct date d)
{
	int days;
	bool isLeapYear (struct date d);
	const int daysPerMonth[12] =
		{ 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31 };

	if ( isLeapYear (d) && d.month == 2 )
		days = 29;
	else
		days = daysPerMonth[d.month - 1];

	return days;
}

// Function to determine if it's a leap year

bool isLeapYear (struct date d)
{
	bool leapYearFlag;

	if ((d.year % 4 == 0 && d.year % 100 != 0) ||
      d.year % 400 == 0 )
  leapYearFlag = true;   // It's a leap year
else
  leapYearFlag = false;  // Not a leap year

return leapYearFlag;
}

int main (void)
{
  struct date  dateUpdate (struct date  today);
  struct date  thisDay, nextDay;

  printf ("Enter today's date (mm dd yyyy): ");
  scanf ("%i%i%i", &thisDay.month, &thisDay.day,
              &thisDay.year);

  nextDay = dateUpdate (thisDay);

  printf ("Tomorrow's date is %i/%i/%.2i.\n",nextDay.month,
     nextDay.day, nextDay.year % 100);

  return 0;
}
```

**输出示例：**

Enter today's date (mm dd yyyy): **2 28 2016**  
Tomorrow's date is 2/29/16.

Enter today's date (mm dd yyyy): 2 22 2015  
Tomorrow's date is 2/23/15.

```c
next_date = dateUpdate (thisDay);
```

### 代码示例：更新时间一秒

```c
// Program to update the time by one second

#include <stdio.h>

struct time
{
        int hour;
        int minutes;
        int seconds;
};

int main (void)
{
        struct time  timeUpdate (struct time  now);
        struct time  currentTime, nextTime;

        printf ("Enter the time (hh:mm:ss): ");
        scanf ("%i:%i:%i", &currentTime.hour,
                        &currentTime.minutes, &currentTime.seconds);

        nextTime = timeUpdate (currentTime);

        printf ("Updated time is %.2i:%.2i:%.2i\n", nextTime.hour,
                        nextTime.minutes, nextTime.seconds );

        return 0;
}
```

```c
// Function to update the time by one second

struct time timeUpdate (struct time now)
{
	++now.seconds;

	if ( now.seconds == 60 ) {		// next minute
		now.seconds = 0;
		++now.minutes;

		if ( now.minutes == 60 ) { // next hour
			now.minutes = 0;
			++now.hour;

			if ( now.hour == 24 ) // midnight
				now.hour = 0;
		}
	}

	return now;
}
```

**输出示例：**

Enter the time (hh:mm:ss): **12:23:55**  
Updated time is 12:23:56

Enter the time (hh:mm:ss): 16:12:59  
Updated time is 16:13:00

Enter the time (hh:mm:ss): **23:59:59**  
Updated time is 00:00:00

### 结构体初始化示例

```c
struct date  today = { 7, 2, 2015 };
```

```c
struct time this_time = { 3, 29, 55 };
```

```c
struct time time1 = { 12, 10 };
```

```c
struct time time1 = { .hour = 12, .minutes = 10 };
```

```c
struct date today = { .year = 2015 };
```

```c
today = (struct date) { 9, 25, 2015 };
```

```c
today = (struct date) { .month = 9, .day = 25, .year = 2015 };
```

### 使用复合字面量计算明天的日期

```c
// Function to calculate tomorrow's date - using compound literals

struct date dateUpdate (struct date today)
{
    struct date tomorrow;
    int numberOfDays (struct date d);

    if (today.day != numberOfDays (today))
        tomorrow = (struct date) { today.month, today.day + 1, today.year };
    else if (today.month == 12)        // end of year
        tomorrow = (struct date) { 1, 1, today.year + 1 };
    else                                // end of month
        tomorrow = (struct date) { today.month + 1, 1, today.year };

    return tomorrow;
}
```

```c
nextDay = dateUpdate ((struct date) { 5, 11, 2004 });
```

### 结构体数组示例

```c
struct time experiments[10];
```

```c
birthdays[1].month = 8;
birthdays[1].day = 8;
birthdays[1].year = 1986;
```

```c
void checkTime (struct time  t0)
{
.
.
.
}
```

**结构体数组初始化：**

```c
struct time runTime [5] =
{
{12, 0, 0}, {12, 30, 0}, {13, 15, 0};
}
```

```c
struct time runTime[5] =
{ 12, 0, 0, 12, 30, 0, 13, 15, 0 };
```

```c
static struct time runTime[5] = { [1].hour = 12, [1].minutes = 30 };
```

### 完整程序：结构体数组演示

```c
// Program to illustrate arrays of structures

#include <stdio.h>

struct time
{
	int hour;
	int minutes;
	int seconds;
};

int main (void)
{
	struct time timeUpdate (struct time now);
	struct time testTimes[5] =
		{ { 11, 59, 59 }, { 12, 0, 0 }, { 1, 29, 59 },
		{ 23, 59, 59 }, { 19, 12, 27 }};
	int i;

	for ( i = 0; i < 5; ++i ) {
		printf ("Time is %.2i:%.2i:%.2i", testTimes[i].hour,
			testTimes[i].minutes, testTimes[i].seconds);

		testTimes[i] = timeUpdate (testTimes[i]);

		printf (" ...one second later it's %.2i:%.2i:%.2i\n",
			testTimes[i].hour, testTimes[i].minutes, testTimes[i].seconds);
	}
	return 0;
}
```

```c
struct time timeUpdate (struct time now)
{
    ++now.seconds;
    if ( now.seconds == 60 ) { // next minute
        now.seconds = 0;
        ++now.minutes;
        if ( now.minutes == 60 ) { // next hour
            now.minutes = 0;
            ++now.hour;
            if ( now.hour == 24 ) // midnight
                now.hour = 0;
        }
    }
    return now;
}
```

**输出示例：**

Time is 11:59:59 ...one second later it's 12:00:00  
Time is 12:00:00 ...one second later it's 12:00:01  
Time is 01:29:59 ...one second later it's 01:30:00  
Time is 23:59:59 ...one second later it's 00:00:00  
Time is 19:12:27 ...one second later it's 19:12:28

### 嵌套结构体与更新操作

```c
event.sdate = dateUpdate (event.sdate);
```

```c
event.stime = timeUpdate (event.stime);
```

**嵌套结构体初始化示例：**

```c
struct dateAndTime  event =
{
{
 2,
 1,
 2015
},
{
 3,
 30,
 0
}
};
```

```c
struct dateAndTime event =
{
{
.month = 2,
.day = 1,
.year = 2015 },
{
.hour = 3,
.minutes = 30, .seconds = 0 }
};
```

```c
struct dateAndTime  events[100];
```

```c
events[i].sdate = dateUpdate (events[i].sdate);
```

```c
events[0].stime.hour     = 12;
events[0].stime.minutes  = 0;
events[0].stime.seconds  = 0;
```

```c
aMonth.numberOfDays = 31;
aMonth.name[0] = 'J';
aMonth.name[1] = 'a';
aMonth.name[2] = 'n';
```
