# **Table B.7** *Date_Format()* and *Time_Format()* (continued)

| Parameter | What It Means |
| :--- | :--- |
| \%r | Time, 12-hour (hh:mm:ss followed by AM or PM) |
| \%S | Seconds (00..59) |
| \%s | Seconds (00..59) |
| \%T | Time, 24-hour (hh:mm:ss) |
| \%U | Week (00..53) starting with Sunday |
| \%u | Week (00..53) starting with Monday |
| \%v | Week (01..53) starting with Monday |
| \%V | Week (01..53) starting with Sunday |
| \%W | Weekday (Sunday, Monday, etc.) |
| \%w | Day of the week (0 = Sunday, 6 = Saturday) |
| \%Y | Year (1999, 2007) |
| \%y | Two-digit year (99, 07) |
| \%$ | A literal \% character |

**The MySQL EXTRACT Command.** The EXTRACT command is an example of a MySQL extension, not described in the SQL standard. It allows you to extract different parts of a date or time, as shown in Table B.8.

# **Table B.8** Date and Time Parts

| Type | Format |
| :--- | :--- |
| SECOND | SECONDS |
| MINUTE | MINUTES |
| HOUR | HOURS |
| DAY | DAYS |
| MONTH | MONTHS |
| YEAR | YEARS (see Example B.44) |
| MINUTE_SECOND | "MINUTES.SECONDS" |
| HOUR_MINUTE | "HOURS.MINUTES" |

*(continued)*