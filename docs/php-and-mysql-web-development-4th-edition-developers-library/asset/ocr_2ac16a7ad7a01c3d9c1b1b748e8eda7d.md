+       *   `SECOND(time)`
+           *   Returns the numeric value of the second for the time value `time`, in the range from 0 to 59.
+           *   `SECOND('12:31:58')` `→ 58`
+           *   `SECOND(123158)` `→ 58`

+       *   `SEC_TO_TIME(seconds)`
+           *   Given a number of seconds `seconds`, returns the corresponding time as a `TIME` value in ‘hh:mm:ss’ format.
+           *   `SEC_TO_TIME(29834)` `→ ‘08:17:14’`

+       *   `STR_TO_DATE(str, format_str)`
+           *   Interprets the string argument `str` using the formatting argument `format_str` and returns a `TIME`, `DATE`, or `DATETIME` value, depending on the formatting specifiers present in `format_str`. You can use this function to interpret temporal values in non-ISO format. `STR_TO_DATE()` performs the inverse operation of `DATE_FORMAT()`, and the format specifiers listed in the description of `DATE_FORMAT()` also are legal for `STR_TO_DATE()`. If `str` is illegal or cannot be interpreted using the given format string, the result is `NULL`.
+           *   `STR_TO_DATE('3/16/1960', '%m/%d/%Y')` `→ 1960-03-16`
+           *   `STR_TO_DATE('12.20.32', '%H.%i.%s')` `→ 12:20:32`
+           *   `STR_TO_DATE('3/16/1960 12:20:32', '%m/%d/%Y %H:%i:%s')` `→ 1960-03-16 12:20:32`
+           *   `STR_TO_DATE('3/16/1960', '%m-%d-%Y')` `→ NULL`

+       *   `SUBDATE(date, INTERVAL expr interval)`
+           *   `SUBDATE(date, expr)`
+           *   For the first syntax, `SUBDATE()` takes a date or date and time value `date`, subtracts a temporal interval from it, and returns the result. This is a synonym for `DATE_SUB()`.
+           *   `SUBDATE('2009-12-01', INTERVAL 1 MONTH)` `→ 2009-11-01`
+           *   For the second syntax, `SUBDATE()` takes a date or date and time value `date`, subtracts a temporal value representing number of days from it, and returns the result. This is similar to the corresponding syntax for `ADDDATE()`.
+           *   `SUBDATE('2009-12-01',30)` `→ 2009-11-01`

+       *   `SUBTIME(expr1, expr2)`
+           *   Subtracts the second expression from the first and returns the result. `expr1` should be a time or date and time value, and `expr2` should be a time value. The values can contain a microseconds part.
+           *   `SUBTIME('06:30:00.5','12:30:00.5')` `→ ‘-06:00:00.000000’`
+           *   `SUBTIME('2009-01-01 00:00:00','12:30:00')` `→ ‘2008-12-31 11:30:00’`