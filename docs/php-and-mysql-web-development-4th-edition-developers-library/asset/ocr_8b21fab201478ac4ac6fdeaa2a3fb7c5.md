If mode is missing, the value of the default_week_format system variable is used.

```
WEEK('2003-12-08')												→ 49
WEEK('2003-12-08',0)											→ 49
WEEK('2003-12-08',1)											→ 50
```

A WEEK() value of 0 indicates that the date occurs prior to the first instance of the week starting day (Sunday or Monday, depending on the mode value).

```
WEEK('2005-01-01')												→ 0
DAYNAME('2005-01-01')											→ 'Saturday'
WEEK('2006-01-01',1)											→ 0
DAYNAME('2006-01-01')											→ 'Sunday'
```

+   - WEEKDAY(*date*)

Returns the numeric value of the weekday for the date value date, or NULL if the name cannot be determined. Weekday values are in the range from 0 for Monday to 6 for Sunday; see also the DAYOFWEEK() function.

```
WEEKDAY('2002-12-08')										→ 6
DAYNAME('2002-12-08')										→ 'Sunday'
WEEKDAY('2002-12-16')										→ 0
DAYNAME('2002-12-16')										→ 'Monday'
WEEKDAY('2002-12-00')										→ NULL
```

+   - WEEKOFYEAR(*date*)

This is the same as WEEK(date,3).

+   - YEAR(*date*)

Returns the numeric value of the year for the date value date.

```
YEAR('2002-12-01')											→ 2002
YEAR(20021201)												→ 2002
```

+   - YEARWEEK(*date*[,*mode*])

Returns a number in the format CYYYYWN representing the year and week of the year for the date value date. The mode argument, if given, is the same as for the WEEK() function.

```
YEARWEEK('2006-01-01')									→ 200601
YEARWEEK('2006-01-01',0)								→ 200601
YEARWEEK('2006-01-01',1)								→ 200552
```

The year for the result may differ from the year in the argument for the first or last week of the year.

```
WEEK('2008-01-01')											→ 0
YEARWEEK('2008-01-01')									→ 200752
```