# Table 24-3: Time/Date Data Types for Columns

| Data Type | Description | Space Needed |
|---|---|---|
| DATE | Contains a date between the range of January 1, 1000 (1000-01-01) and December 31, 9999 (9999-12-31). | Uses 3 bytes |
| DATETIME | Contains a combination of date and time between zero hour of January 1, 1000 (1000-01-01 00:00:00) and the last second of December 31, 9999 (9999-12-31 23:59:59). | Uses 8 bytes |
| TIMESTAMP[M] | Contains a timestamp from between zero hour of January 1, 1970 (1970-01-01 00:00:00) and a time in the year 2037. It is stored in the form: YYYYMMDDHHMMSS. Using M, you can reduce the size of the TIMESTAMP displayed to less than the full 14 characters (though the full 4-byte TIMESTAMP is still stored). | Uses 4 bytes |
| TIME | Contains a time between -838:59:59 and 838:59:59. The format of the field is in hours, minutes, and seconds (HH:MM:SS). | Uses 3 bytes |
| YEAR[2|4] | Contains a year, represented by either two or four digits. For a four-digit year, YEAR mean 1901–2155 (0000 is also allowed). For a two-digit year, the digits 70-69 can represent 1970-2069 | Uses 1 byte |

Table 24-4 shows string data types that you can use with MYSQL.

# Table 24-4: String Data Types for Columns

| Data Type | Description | Space Needed |
|---|---|---|
| BLOB | Contains a binary large object (BLOB) that varies in size, based on the actual value of the data, rather than on the maximum allowable size. Searches on a BLOB column are case-sensitive. | Uses up to L+2 bytes, where L is less than or equal to 65535 |