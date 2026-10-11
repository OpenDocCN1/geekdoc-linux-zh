
## C.2 Functions

CONVERT_TZ('2009-02-11 00:00:00','US/Central','US/Eastern') → '2009-02-11 01:00:00'
CONVERT_TZ('2009-02-11','+00:00','-03:00') → '2009-02-10 21:00:00'

### CURDATE()

Returns the current date in the connection time zone as a DATE value in 'YYYY-MM-DD' format.

CURDATE() → '2008-05-01'

### CURRENT_DATE()

This function is a synonym for CURDATE(). The parentheses are optional.

### CURRENT_TIME()

This function is a synonym for CURTIME(). The parentheses are optional.

### CURRENT_TIMESTAMP()

This function is a synonym for NOW(). The parentheses are optional.

### CURTIME()

Returns the current time of day in the connection time zone as a TIME value in 'hh:mm:ss' format.

CURTIME() → '18:32:58'

### DATE(expr)

Returns the date part of expr, which should be a date or date and time expression.

DATE('2008-03-12') → '2008-03-12'
DATE('2008-03-12 16:15:00') → '2008-03-12'

### DATE_ADD(date, INTERVAL expr interval)

Takes a date or date and time value date, adds a temporal interval to it, and returns the result. expr specifies the time value to be added to date (or subtracted, if expr begins with '-'), and interval specifies how to interpret the interval. The result is a DATE value if date is a DATE value and no time-related values are involved in calculating the result. Otherwise, the result is a DATETIME value. The result is NULL if date is not a legal date.

DATE_ADD('2009-12-01', INTERVAL 1 YEAR) → '2010-12-01'
DATE_ADD('2009-12-01', INTERVAL 60 DAY) → '2010-01-30'
DATE_ADD('2009-12-01', INTERVAL -3 MONTH) → '2009-09-01'
DATE_ADD('2009-12-01 08:30:00', INTERVAL 12 HOUR) → '2009-12-01 20:30:00'

The following table shows the allowable interval values, their meanings, and the format in which values for each interval type should be specified. The keyword INTERVAL and the interval specifiers are not case sensitive.

| Interval Type | Meaning | Value Format |
| :--- | :--- | :--- |
| `MICROSECOND` | Microseconds | `uuuuuu` |
| `SECOND` | Seconds | `ss` |
| `SECOND_MICROSECOND` | Seconds and microseconds | `'ss.uuuuuu'` |
| `MINUTE` | Minutes | `mm` |
| `MINUTE_SECOND` | Minutes and seconds | `'mm:ss'` |
| `MINUTE_MICROSECOND` | Minutes and microseconds | `'mm.uuuuuu'` |
| `HOUR` | Hours | `hh` |
| `HOUR_MINUTE` | Hours and minutes | `'hh:mm'` |
| `HOUR_SECOND` | Hours, minutes, and seconds | `'hh:mm:ss'` |
| `HOUR_MICROSECOND` | Hours and microseconds | `'hh.uuuuuu'` |
| `DAY` | Days | `DD` |
| `DAY_HOUR` | Days and hours | `'DD hh'` |
| `DAY_MINUTE` | Days, hours, and minutes | `'DD hh:mm'` |
| `DAY_SECOND` | Days, hours, minutes, and seconds | `'DD hh:mm:ss'` |
| `DAY_MICROSECOND` | Days and microseconds | `'DD.uuuuuu'` |
| `WEEK` | Weeks | `WW` |
| `MONTH` | Months | `MM` |
| `QUARTER` | Quarters | `QQ` |
| `YEAR` | Years | `YY` |
| `YEAR_MONTH` | Years and months | `'YY-MM'` |

The expression *expr* that is added to the date may be specified as a number or as a string, unless it contains non-digit characters, in which case it must be a string. The delimiter characters may be any punctuation character.

DATE_ADD('2005-12-01', INTERVAL '2' YEAR_MONTH) → '2008-03-01'
DATE_ADD('2005-12-01', INTERVAL '2-3' YEAR_MONTH) → '2008-03-01'

The parts of the value of *expr* are matched from right to left against the parts to be expected based on the *interval* specifier. For example, the expected format for `HOUR_SECOND` is '`hh:mm:ss`'. An *expr* value of '`15:21`' is interpreted as '`00:15:21`', not as '`15:21:00`'.

DATE_ADD('2003-12-01 12:00:00', INTERVAL '15:21' HOUR_SECOND) → '2003-12-01 12:15:21'

If interval is YEAR, MONTH, or YEAR_MONTH and the day part of the result is larger than the number of days in the result month, the day is set to the maximum number of days in that month.

DATE_ADD('2003-12-31', INTERVAL 2 MONTH) → '2004-02-29'

An alternative syntax can be used for date addition.

'2003-12-31' + INTERVAL 2 MONTH → '2004-02-29'
INTERVAL 2 MONTH + '2003-12-31' → '2004-02-29'

### DATE_FORMAT(date, format)

Formats a date or date and time value date according to the formatting string format and returns the resulting string. DATE_FORMAT() can be used to reformat date or date and time values from the form MySQL uses to provide any format you want.

DATE_FORMAT('2004-12-01', '%M %e, %Y') → 'December 1, 2004'
DATE_FORMAT('2004-12-01', 'The %d of %M') → 'The 1st of December'

The following table shows the specifiers that are allowed in the formatting string. The ranges shown for the numeric month and day specifiers begin with zero because zero may be produced for dates that are incomplete, such as '2004-00-13' or '1998-12-00'.

The '%' character preceding each format code is required. Characters present in the formatting string that are not listed in the table are copied to the result string literally.

| Specifier | Meaning |
| :--- | :--- |
| %f | Microseconds in six-digit form (000000, 000001, ...) |
| %S, %s | Second in two-digit form (00, 01, ... 59) |
| %i | Minute in two-digit form (00, 01, ... 59) |
| %h | Hour in two-digit form, 24-hour time (00, 01, ... 23) |
| %h, %I | Hour in two-digit form, 12-hour time (01, 02, ... 12) |
| %k | Hour in numeric form, 24-hour time (0, 1, ... 23) |
| %l | Hour in numeric form, 12-hour time (1, 2, ... 12) |
| %T | Time in 24-hour form (hh:mm:ss) |
| %r | Time in 12-hour form (hh:mm:ss AM or hh:mm:ss PM) |
| %p | AM or PM |
| %W | Weekday name (Sunday, Monday, ..., Saturday) |
| %a | Weekday name in abbreviated form (Sun, Mon, ..., Sat) |
| %d | Day of the month in two-digit form (00, 01, ..., 31) |
| %e | Day of the month in numeric form (0, 1, ..., 31) |
| %D | Day of the month with English suffix (0th, 1st, 2nd, 3rd, ...) |
| %w | Day of the week in numeric form (0=Sunday, ..., 6=Saturday) |
| %j | Day of the year in three-digit form (001, 002, ..., 366) |
| %U | Week (00, ..., 53), where Sunday is the first day of the week |
| %u | Week (00, ..., 53), where Monday is the first day of the week |
| %V | Week (01, ..., 53), where Sunday is the first day of the week |
| %v | Week (01, ..., 53), where Monday is the first day of the week |
| %M | Month name (January, February, ..., December) |
| %b | Month name in abbreviated form (Jan, Feb, ..., Dec) |
| %m | Month in two-digit form (00, 01, ..., 12) |
| %c | Month in numeric form (0, 1, ..., 12) |
| %Y | Year in four-digit form |
| %y | Year in two-digit form |
| %X | Year for the week in which Sunday is the first day, four-digit form |
| %x | Year for the week in which Monday is the first day, four-digit form |
| %% | A literal `%` character |

If you refer to time specifiers for a **date** value, the time part of the value is treated as `00:00:00`.

DATE_FORMAT('2004-12-01','%i') → '00'

### DATE_SUB(date, INTERVAL expr interval)

DATE_SUB() performs date arithmetic in the same manner as DATE_ADD(), except that expr is subtracted from the date or date and time value date. See DATE_ADD() for more information.

DATE_SUB('2009-12-01', INTERVAL 1 MONTH) → '2009-11-01'
DATE_SUB('2009-12-01', INTERVAL '13-2' YEAR_MONTH) → '1996-10-01'
DATE_SUB('2009-12-01 04:53:12', INTERVAL '13-2' MINUTE_SECOND) → '2009-12-01 04:40:10'
DATE_SUB('2009-12-01 04:53:12', INTERVAL '13-2' HOUR_MINUTE) → '2009-11-30 15:51:12'

An alternative syntax is supported for date subtraction.

'2009-12-01' - INTERVAL 1 MONTH → '2009-11-01'

Using this syntax, the INTERVAL clause must be on the right side of the subtraction operator, because you cannot subtract a date from an interval.

### DATEDIFF(expr1, expr2)

Returns the difference in number of days between the two expressions, which should be date or date and time values. The result is positive if the first argument is later than the second. Any time part in the values is ignored.

DATEDIFF('1987-01-01','1987-01-08') → -7
DATEDIFF('1987-01-08','1987-01-01') → 7
DATEDIFF('1987-01-01 12:00:00','1987-01-08') → 7
DATEDIFF('1987-01-08','1987-01-01 12:00:00') → 7

### DAY(date)

This function is a synonym for DAYOFMONTH().

### DAYNAME(date)

Returns a string containing the weekday name for the date value *date*, or *NULL* if the name cannot be determined.

DAYNAME('2004-12-01') → 'Wednesday'
DAYNAME('1900-12-01') → 'Saturday'
DAYNAME('1900-12-00') → NULL

### DAYOFMONTH(date)

Returns the numeric value of the day of the month for the date value *date*, in the range from 0 to 31 (0 for partial dates with no day part).

DAYOFMONTH('2002-12-01') → 1
DAYOFMONTH('2002-12-25') → 25
DAYOFMONTH('2002-12-00') → 0

### DAYOFWEEK(date)

Returns the numeric value of the weekday for the date value *date*. Weekday values are in the range from 1 for Sunday to 7 for Saturday, per the ODBC standard. See also the WEEKDAY() function.

DAYOFWEEK('2004-12-05') → 1
DAYNAME('2004-12-05') → 'Sunday'
DAYOFWEEK('2004-12-18') → 7
DAYNAME('2004-12-18') → 'Saturday'
