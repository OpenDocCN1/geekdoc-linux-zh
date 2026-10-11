# B.4.3 Date and Time Functions

To get the date and time, MySQL provides the functions shown in Table B.6.

**Table B.6 MySQL Date and Time Functions**

| Function | Example |
| :--- | :--- |
| NOW() | `select NOW();` | | `--> 2006-03-23 20:52:58` | | (See Example B.42.) |
| CURDATE() | `select CURDATE();` | | `--> '2006-12-15'` | | (See Example B.42.) |
| CURTIME() | `select CURTIME();` | | `--> '23:50:26'` | | (See Example B.42.) |
| DAYOFYEAR(date) | `select DAYOFYEAR('2006-12-15');` | | `--> 349` |
| DAYOFMONTH(date) | `select DAYOFMONTH('2006-12-15');` | | `--> 15` |
| DAYOFWEEK(date) | `select DAYOFWEEK('2006-12-15');` | | `--> 6` |
| WEEKDAY(date) | `select WEEKDAY('2006-12-15');` | | `--> 4` |
| MONTHNAME(date) | `select MONTHNAME('2006-12-15');` | | `--> December` |
| DAYNAME(date) | `select DAYNAME('2006-12-15');` | | `--> Friday` |
| YEAR(date) | `select YEAR('2006-12-15');` | | `--> 2006` |
| QUARTER(date) | `select QUARTER('2006-12-15');` | | `--> 4` |