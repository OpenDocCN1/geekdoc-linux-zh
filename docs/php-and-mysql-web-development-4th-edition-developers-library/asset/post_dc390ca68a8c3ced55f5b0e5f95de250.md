
## 3.2.1 Overview of Data Types

MySQL has numeric data types for integer, fixed-point, floating-point, and bit values, as shown in Table 3.2. Numeric types other than `BIT` can be signed or unsigned. A special attribute enables sequential integer or floating-point column values to be generated automatically, which is useful in applications that require a series of unique identification numbers.

**Table 3.2 Numeric Data Types**

| Type Name | Meaning |
| --- | --- |
| TINYINT | A very small integer |
| SMALLINT | A small integer |
| MEDIUMINT | A medium-sized integer |
| INT | A standard integer |
| BIGINT | A large integer |
| DECIMAL | A fixed-point number |
| FLOAT | A single-precision floating-point number |
| DOUBLE | A double-precision floating-point number |
| BIT | A bit field |

Table 3.3 shows the MySQL string data types. Strings can hold anything, even arbitrary binary data such as images or sounds. Strings can be compared according to whether they are case sensitive. In addition, you can perform pattern matching on strings. (Actually, in MySQL, you can even perform pattern matching on numeric types, but it’s more commonly done with string types.)

**Table 3.3 String Data Types**

| Type Name | Meaning |
| --- | --- |
| CHAR | A fixed-length non-binary (character) string |
| VARCHAR | A variable-length non-binary string |
| BINARY | A fixed-length binary string |
| VARBINARY | A variable-length binary string |
| TINYBLOB | A very small BLOB (binary large object) |
| BLOB | A small BLOB |
| MEDIUMBLOB | A medium-sized BLOB |
| LONGBLOB | A large BLOB |
| TINYTEXT | A very small non-binary string |
| TEXT | A small non-binary string |
| MEDIUMTEXT | A medium-sized non-binary string |
| LONGTEXT | A large non-binary string |
| ENUM | An enumeration; each column value may be assigned one enumeration member |
| SET | A set; each column value may be assigned zero or more set members |

Table 3.4 shows the MySQL date and time data types, where $CC$, $YY$, $MM$, $DD$, $hh$, $mm$, and $ss$ represent century, year, month, day of the month, hour, minute, and second, respectively. For temporal values, MySQL provides types for dates and times (either combined or separate) and timestamps (a special type that enables you to track when changes were last made to a row). There is also a type for efficiently representing year values when you don't need an entire date.

**Table 3.4 Date and Time Data Types**

| Type Name | Meaning |
| --- | --- |
| DATE | A date value, in 'CCYY-MM-DD' format |
| TIME | A time value, in 'hh:mm:ss' format |
| DATETIME | A date and time value, in 'CCYY-MM-DD hh:mm:ss' format |
| TIMESTAMP | A timestamp value, in 'CCYY-MM-DD hh:mm:ss' format |
| YEAR | A year value, in CCYY or YY format |

Table 3.5 shows the MySQL spatial data types. These represent various kinds of geometrical or geographical values.

**Table 3.5 Spatial Data Types**

| Type Name | Meaning |
| --- | --- |
| GEOMETRY | A spatial value of any type |
| POINT | A point (a pair of X,Y coordinates) |
| LINESTRING | A curve (one or more POINT values) |
| POLYGON | A polygon |
| GEOMETRYCOLLECTION | A collection of GEOMETRY values |
| MULTILINESTRING | A collection of LINESTRING values |
| MULTIPOINT | A collection of POINT values |
| MULTIPOLYGON | A collection of POLYGON values |

## 3.2.2 Specifying Column Types in Table Definitions

To create a table, issue a CREATE TABLE statement that includes a list of the columns in the table. Here’s an example that creates a table named mytbl with three columns named f, c, and i:

```sql
CREATE TABLE mytbl
(
    f FLOAT(10,4),
    c CHAR(15) NOT NULL DEFAULT 'none',
    i TINYINT UNSIGNED NULL
);
```

Each column has a name and a type, and attributes can be associated with the type. The syntax for defining a column is as follows:

```sql
col_name col_type [type_attributes] [general_attributes]
```

The name of the column, `col_name`, is always first in the definition and must be a legal identifier. The precise rules for identifier syntax are given in Section 2.2, “MySQL Identifier Syntax and Naming Rules.” Briefly summarized, column identifiers may be up to 64 characters long, and may consist of alphanumeric characters from the system character set, as well as the underscore and dollar sign characters (“_” and “$”). Keywords such as SELECT, DELETE, and CREATE normally are reserved and cannot be used. However, you can include other characters within an identifier or use a reserved word as an identifier if you are willing to put up with the bother of quoting it whenever you refer to it. To quote an identifier, enclose it within backtick (“`”) characters. If the ANSI_QUOTES SQL mode is enabled, it is allowable to quote identifiers within double quote (“\"”) characters instead. `col_type` indicates the column data type; that is, the specific kind of values the column can hold. Some type specifiers indicate the maximum length of the values you store in the column. For others, the length is implied by the type name. For example, `CHAR(10)` specifies an explicit length of 10 characters, whereas `TINYTEXT` values have an implicit maximum length of 255 characters. Some of the type specifiers allow you to indicate a maximum display width (how many characters to use for displaying values). For fixed-point and floating-point types, you can specify the number of significant digits and number of decimal places.

Following the column’s data type, you may specify optional type-specific attributes as well as more general attributes. These attributes function as type modifiers. They cause MySQL to change the way it treats column values in some way:

-   The type-specific attributes that are allowable depend on the data type you choose. For example, `UNSIGNED` and `ZEROFILL` are allowable only for numeric types, and `CHARACTER SET` and `COLLATE` are allowable only for non-binary string types.
-   The general attributes may be given for any data type, with a few exceptions. You may specify `NULL` or `NOT NULL` to indicate whether a column can hold NULL values. For most data types, you can specify a `DEFAULT` clause to define a default value for the column. Default value handling is described in Section 3.2.3, "Configuring Time Zone Support."

If multiple column attributes are present, there are some constraints on the order in which they may appear. In general, you should be safe if you specify data type-specific attributes such as `UNSIGNED` or `ZEROFILL` before general attributes such as `NULL` or `NOT NULL`.

## 3.2.3 Specifying Column Default Values

For all but BLOB and TEXT types, spatial types, or columns with the `AUTO_INCREMENT` attribute, you can specify a `DEFAULT def_value` clause to indicate that a column should be assigned the value `def_value` when a new row is created that does not explicitly specify the column's value. With some limited exceptions for `TIMESTAMP` columns, `def_value` must be a constant. It cannot be an expression or refer to other columns.

If a column definition includes no explicit `DEFAULT` clause and the column can take `NULL` values, its default value is `NULL`. Otherwise, the handling of a missing `DEFAULT` clause is version dependent.

From MySQL 5.0.2 on, the column is created without any `DEFAULT` clause. That is, it has no default value. This affects how the server handles the column if a new row that does not specify a value for the column is inserted into the table:

-   When strict SQL mode is not in effect, the column is set to the implicit default for its data type. (Implicit defaults are described shortly)
-   When strict SQL mode is in effect, an error occurs if the table is transactional. The statement aborts and rolls back. For non-transactional tables, an error occurs and the statement aborts if the row is the first row inserted by the statement. If it is not the first row, you can elect to have the statement abort or to have the column set to its implicit default with a warning. The choice depends on which strict mode setting is in effect. See Section 3.3, "How MySQL Handles Invalid Data Values," for details.

Before MySQL 5.0.2, MySQL defines the column with a `DEFAULT` clause that specifies the implicit default value.

The implicit default for a column depends on its data type:

-   For numeric columns, the default is 0, except for columns that have the `AUTO_INCREMENT` attribute. For `AUTO_INCREMENT`, the default is the next number in the column sequence.
-   For date and time types except `TIMESTAMP`, the default is the "zero" value for the type (for example, `'0000-00-00'` for DATE). For `TIMESTAMP`, the default is the current date and time for the first `TIMESTAMP` column in a table, and the `"zero"` value for any following `TIMESTAMP` columns. (`TIMESTAMP` defaults actually are more complex and are discussed in Section 3.2.6.2, "The `TIMESTAMP` Data Type.")
