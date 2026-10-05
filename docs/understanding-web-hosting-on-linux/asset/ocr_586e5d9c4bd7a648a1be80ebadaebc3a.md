# Data Types

RDB tables (files) are defined to contain columns of specific data types. Table 8.3 shows the basic RDB data types supported in IBM's DB2 database management system. Note that business applications use the "numerically exact" data types of DECIMAL and NUMBER to store monetary values, since they enable fixed-point decimal precision. The "numerically approximate" data types of FLOAT, REAL, and DOUBLE are often used for scientific applications requiring fixed-point numbers. The charge in the invoice detail table, for instance, would be appropriately treated as a decimal number with a precision of nine and a decimal count of two: DEC(9,2)

# Table 8.3: Basic DB2 SQL Data Types

| Data Type | Description |
|---|---|
| CHAR(n) | A fixed-length string of n characters. |
| DECIMAL(p,s) | A decimal number with precision p and scale s. The total number of digits, and the scale is the total number of digits to the right of the decimal point. |
| NUMERIC(p,s) | A synonym for DECIMAL. |
| INTEGER | A 32-bit integer. |
| SMALLINT | A 16-bit integer. |
| REAL | A 32-bit, single-precision, floating-point number. |
| DOUBLE | A 64-bit, double-precision number. |
| FLOAT | A synonym for DOUBLE. |
| DATE | Stores the year, month, and day. |
| TIME | Stores the hour, minute, and second. |
| TIMESTAMP | Stores the year, month, hour, minute, second, and microsecond. |

# Defining Your Database

Now that you know the basic theory behind relational database design, it's time to create a database. The standard method of designing (as well as manipulating and retrieving) relational data is to use SQL. SQL is a relatively simple language to learn because it uses a relatively small number of commands. To define tables, you use the CREATE TABLE command:

```
CREATE TABLE table name (column name data type [, ?])
```

The following SQL commands create the invoice, invoice detail, and customer databases:

```
CREATE TABLE Invoice (InvoiceNo INT, CustNo INT, InvoiceDate DATE, CloseDate Date)
CREATE TABLE InvoiceDetail (InvoiceNo INT, LineNo INT, Desc CHAR(50), Qty INT, Charge DEC(9,2))
CREATE TABLE customer (CustNo INT, LastName CHAR(20), Street CHAR(20), City CHAR(15), ZipCode INT, State CHAR(2), PhoneNo CHAR(10))
```

Data can be inserted into a table immediately after it is created. However, before you see that, you need to learn how to build SQL indexes on top of SQL tables. An index is a special file that allows the RDB to quickly retrieve rows from a table. It is standard practice to create an index for each database table on