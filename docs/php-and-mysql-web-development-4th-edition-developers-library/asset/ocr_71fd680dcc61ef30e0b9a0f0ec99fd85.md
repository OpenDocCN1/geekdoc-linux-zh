```
TIMESTAMP('1985-12-14'); → '1985-12-14 00:00:00'
TIMESTAMP('1985-12-14 09:00:00'); → '1985-12-14 09:00:00'
TIMESTAMP('1985-12-14','18:00:00'); → '1985-12-14 18:00:00'
TIMESTAMP('1985-12-14 09:00:00','18:00:00'); → '1985-12-15 03:00:00'
TIMESTAMP('1985-12-14 09:00:00','-18:00:00'); → '1985-12-13 15:00:00'
```

+   - `TIMESTAMPPAD(interval, expr1, expr2)`

Interprets expr1 as an integer number of units given by the interval argument, adds it to the date or date and time value expr2, and returns the result. The allowable interval values are FRAC_SECOND, SECOND, MINUTE, HOUR, DAY, WEEK, MONTH, QUARTER, and YEAR. Any of these values also may be given with a prefix of SQL_TSI_. As of 5.0.60/5.1.24, FRAC_SECOND is deprecated; instead, MICROSECOND is preferred for specifying a unit of microseconds.

```
TIMESTAMPPAD(DAY,12,'1995-07-01') → '1995-07-13'
TIMESTAMPPAD(MONTH,12,'1995-07-01') → '1996-07-01'
TIMESTAMPPAD(SQL_TSI_MONTH,12,'1995-07-01') → '1996-07-01'
```

+   - `TIMESTAMPDIFF(interval, expr1, expr2)`

Calculates the difference between the date or date and time expressions expr1 and expr2, and returns the result in the units given by the interval argument. Allowable interval values are the same as those given in the description for TIMESTAMPPAD().

```
TIMESTAMPDIFF(DAY,'1995-07-01','1995-08-01') → 31
TIMESTAMPDIFF(MONTH,'1995-07-01','1995-08-01') → 1
```

+   - `TO_DAYS(date)`

Returns a numeric value representing the date value date converted to the number of days since the year 0. The return value may be passed to FROM_DAYS() to convert it back to a date.

```
TO_DAYS('2010-12-01') → 734472
FROM_DAYS(734472 - 365) → '2009-12-01'
```

If given a DATETIME or TIMESTAMP value, TO_DAYS() ignores the time part.

```
TO_DAYS('2010-12-01 12:14:37') → 734472
TO_DAYS() is intended only for dates covered by the Gregorian calendar (1582 on).
```

+   - `UNIX_TIMESTAMP()`

+   - `UNIX_TIMESTAMP(date)`

When called with no arguments, returns the number of seconds since the reference date '1970-01-01 00:00:00' UTC. When called with a date-valued argument date, returns the number of seconds between the reference date and the argument. date may be specified several ways: as a DATE, DATETIME, or TIMESTAMP value, or as a number in the format CCCCMMDD or YYMMDD. The server interprets date as a value in