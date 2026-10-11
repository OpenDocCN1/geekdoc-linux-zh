# Table 3.15 **Date and Time Type “Zero” Values**

| **Type Specification** | **Zero Value** |
| DATE | '0000-00-00' |
| TIME | '00:00:00' |
| DATETIME | '0000-00-00 00:00:00' |
| TIMESTAMP | '0000-00-00 00:00:00' |
| YEAR | 0000 |

MySQL always represents dates with the year first, in accordance with the standard SQL and ISO 8601 specifications. For example, December 3, 2008, is represented as '2008-12-03'. However, MySQL does allow some leeway in how you can specify input dates. For example, it will convert two-digit year values to four digits, if you need not supply a leading zero digit for month and day values that are less than 10. However, you must specify the year first and the day last. Formats that you may be more used to, such as '12/3/99' or '3/12/99', will not be interpreted as you might intend. In such cases, you might find the STR_TO_DATE( ) function useful for converting strings in non-ISO format to ISO-format dates. Section 3.2.6.5, “Working with Date and Time Values,” further discusses the date interpretation rules that MySQL uses.

For combined date and time values, it is allowable to specify a 'T' character rather than a space between the date and time, for example, '2008-12-31T12:00:00'.

Time or combined date and time values can include a microseconds part following the time, consisting of a decimal point and up to six digits. For example, '12:30:15.5' or '2008-06-15 10:30:12.000045'. However, current support in MySQL for microseconds on values is only partial. Some temporal functions use them, but you cannot store a temporal value that includes a microseconds part in a table; the microseconds part is discarded.

For retrieval, you can display date and time values in a variety of formats by using the DATE_FORMAT( ) and TIME_FORMAT( ) functions.

# 3.2.6.2 **The DATE, TIME, and DATETIME Data Types**

The DATE and TIME types hold date and time values. The DATETIME type holds combined date and time values. The formats for the three types of values are 'CCYY-MM-DD', 'hh:mm:ss' , and 'CCYY-MM-DD hh:mm:ss' , where CC, YY, MM, DD, hh, mm, and ss represent century, year, month, day, hour, minute, and second, respectively.

For the DATETIME type, the date and time parts are both required; if you assign a DATE value to a DATETIME column, MySQL automatically adds a time part of '00:00:00'. Conversions work in the other direction as well. If you assign a DATETIME value to a DATE or TIME column, MySQL discards the part that is irrelevant:

```
```mysql
mysql> CREATE TABLE t (d DATE, d DATE, t TIME);
mysql> INSERT INTO t (d,d,t) VALUES(NOW(), (NOW(), NOW());
mysql> SELECT * FROM t;
```
```