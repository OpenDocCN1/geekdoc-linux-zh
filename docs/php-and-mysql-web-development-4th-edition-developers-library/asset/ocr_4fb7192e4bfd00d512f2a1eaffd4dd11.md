+---------------------+--------+---------------------+
| dt | a | t |
+---------------------+--------+---------------------+
| 2007-09-14 10:26:26 | 2007-09-14 | 10:26:26 |
+---------------------+--------+---------------------+

MySQL treats the time in DATETIME and TIME values slightly different. For DATETIME, the time part represents a time of day and must be in the range from ‘`00:00:00`’ to ‘`23:59:59`’. A TIME value, on the other hand, represents elapsed time—that’s why the range shown in Table 3.13 for TIME columns includes values larger than ‘`23:59:59`’ and negative values.

One thing to watch out when inserting TIME values into a table is that if you use a “short” (not fully qualified) value, it may not be interpreted as you expect. For example, you’ll probably find that if you insert ‘`30`’ and ‘`12:30`’, into a TIME column, one value will be interpreted from right to left and the other from left to right, resulting in stored values of ‘`00:00:30`’ and ‘`12:30:00`’. If you consider ‘`12:30`’ to represent a value of “12 minutes, 30 seconds,” you should specify it in fully qualified form as ‘`00:12:30`’.

# ### 3.2.6.2 The TIMESTAMP Data Type

TIMESTAMP is a temporal data type that stores combined date and time values. (The word “timestamp” might appear to connote time only, but that is not the case.) The TIMESTAMP data type has the special properties noted in the following discussion.

TIMESTAMP columns have a range of values from ‘`1970-01-01 00:00:01`’ to ‘`2038-01-19 03:14:07`’. The range is tied to Unix time, where the first day of 1970 is “day zero,” also known as “the epoch.” Values are stored as a four-byte number of seconds since the epoch. The beginning of 1970 determines the lower end of the TIMESTAMP range. The upper end of the range corresponds to the maximum four-byte value for Unix time.

Values are stored in Universal Coordinated Time (UTC). When you store a TIMESTAMP value, the server converts it from the connection’s time zone to UTC. When you retrieve the value later, the server converts it back from UTC to the connection’s time zone, so you see the same value that you stored. However, if another client connects to the server, uses a different time zone, and retrieves the value, it will see the value adjusted to its own time zone. In fact, you can see this effect within a single connection if you change your own time zone:

```
```sql
mysql> CREATE TABLE t (ts TIMESTAMP);
mysql> SET time_zone = '+00:00';  # set time zone to UTC
mysql> INSERT INTO t VALUES('2000-01-01 00:00:00');
mysql> SELECT ts FROM t;
```

+---------------------+
| ts |
+---------------------+
```