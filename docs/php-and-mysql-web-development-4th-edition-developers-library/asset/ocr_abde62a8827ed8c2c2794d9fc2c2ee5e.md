DATE_ADD('2003–12–01 12:00:00', INTERVAL '15:21' HOUR_SECOND)      → '2003–12–01 12:15:21'

If interval is YEAR, MONTH, or YEAR_MONTH and the day part of the result is larger than the number of days in the result month, the day is set to the maximum number of days in that month.

DATE_ADD('2003–12–31', INTERVAL 2 MONTH)      → '2004–02–29'

An alternative syntax can be used for date addition.

'2003–12–31' + INTERVAL 2 MONTH      → '2004–02–29'
INTERVAL 2 MONTH + '2003–12–31'      → '2004–02–29'

+   DATE_FORMAT(date, format)
+   
+   Formats a date or date and time value date according to the formatting string format and returns the resulting string. DATE_FORMAT() can be used to reformat date or date and time values from the form MySQL uses to provide any format you want.

DATE_FORMAT('2004–12–01', '%M %e, %Y')      → 'December 1, 2004'
DATE_FORMAT('2004–12–01', 'The %d of %M')      → 'The 1st of December'

The following table shows the specifiers that are allowed in the formatting string. The ranges shown for the numeric month and day specifiers begin with zero because zero may be produced for dates that are incomplete, such as '2004–00–13' or '1998–12–00'.

The '%‘character preceding each format code is required. Characters present in the formatting string that are not listed in the table are copied to the result string literally.

|Specifier|Meaning|
|--------|--------|
|%f|Microseconds in six-digit form (000000, 000001, ...)|
|%S, %s|Second in two-digit form (00, 01, ... 59)|
|%i|Minute in two-digit form (00, 01, ... 59)|
|%h|Hour in two-digit form, 24-hour time (00, 01, ... 23)|
|%h, %I|Hour in two-digit form, 12-hour time (01, 02, ... 12)|
|%k|Hour in numeric form, 24-hour time (0, 1, ... 23)|
|%l|Hour in numeric form, 12-hour time (1, 2, ... 12)|
|%T|Time in 24-hour form (hh:mm:ss)|
|%r|Time in 12-hour form (hh:mm:ss AM or hh:mm:ss PM)|