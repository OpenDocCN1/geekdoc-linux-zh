# TABLE 9.3 Common SQL data type

| Data Type Name | Purpose |
| --- | --- |
| INTEGER (aka INT) | 4-byte integer value |
| SMALLINT | 2-byte integer value |
| DECIMAL | Precision storage of decimal values |
| NUMERIC | Precision storage of decimal values |
| FLOAT | Floating-point number |
| DOUBLE PRECISION | Floating-point number stored with twice the precision of FLOAT |
| DATETIME | A date and time |
| DATE | A date |
| TIME | A time, in HH:MM:SS format; may be a time of day or a period of time |
| CHAR | One or more characters |
| VARCHAR | A variable number of small, medium, or large |
| ENUM | An enumerated list, as such as one of the set |
| SET | Data that may have zero or more values, as in any one of the set of nuts, sprinkles, fudge, and cherry for ice cream toppings |

Additional data types exist; Table 9.3 is intended to give you a feel for what's available and to list some of the data types you're likely to encounter. Some implementations support data types, too. Each of these data types has its own features. For instance, the numeric data types (INTEGER, DECIMAL, and so on) can be manipulated by mathematical operators.

# Using MySQL

To learn about SQL, you should have access to a SQL database. For purposes of demonstration, I'm using MySQL as a reference. Other SQL implementations are similar to what I describe here, but some details differ. One of these details is how to start the database. In the case of MySQL, your distribution should include a SysV or startup script for the SQL server. This server may also need to be configured with its own root password.