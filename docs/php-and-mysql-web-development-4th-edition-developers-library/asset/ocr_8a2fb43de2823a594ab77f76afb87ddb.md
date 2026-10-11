two digits for month, day, hour, minute, or second values that are less than 10. The following are all equivalent:

```
'2012-02-03 05:04:09'
'2012-2-03 05:04:09'
'2012-2-3 05:04:09'
'2012-2-3 5:04:09'
'2012-2-3 5:04:9'
'2012-2-3 5:4:9'
```

MySQL may interpret values with leading zeros in different ways depending on whether they are specified as strings or numbers. The string `001231` will be seen as a six-digit value and interpreted as `2000-12-31` for a DATE, and as `2000-12-31 00:00:00` for a DATETIME. On the other hand, the number 001231 will be seen as 1231 after the parser gets done with it and then the interpretation becomes problematic. This is a case where it’s best to supply a string value `001231`, or else use a fully qualified value if you are using numbers (that is, 20001231 for DATE and 200012310000 for DATETIME).

In general, you may freely assign values between the DATE, DATETIME, and TIMESTAMP types, although there are certain restrictions to keep in mind:

+   * If you assign a DATETIME or TIMESTAMP value to a DATE, the time part is discarded.

+   * If you assign a DATE value to a DATETIME or TIMESTAMP, the time part of the resulting value is set to zero (`00:00:00`).

+   * The types have different ranges. In particular, TIMESTAMP has a more limited range (1970 to 2038); so, for example, you cannot assign a pre-1970 DATE-time value to a TIMESTAMP and expect reasonable results. Nor can you assign values that are far in the future to a TIMESTAMP.

MySQL provides many functions for working with date and time values. See Appendix C for more information.

# 3.2.6.6 Interpretation of Ambiguous Year Values

For all date and time types that include a year part (DATE, DATETIME, TIMESTAMP, YEAR), MySQL handles values that contain two-digit years by converting them to four-digit years:

+   * Year values from 00 to 69 become 2000 to 2069

+   * Year values from 70 to 99 become 1970 to 1999

You can see the effect of these rules most easily by storing different two-digit values into a YEAR column and then retrieving the results. This also demonstrates something you should take note of:

```
mysql> CREATE TABLE y_table (y YEAR);
mysql> INSERT INTO y_table VALUES(68),(69),(99),(00),('00');
```