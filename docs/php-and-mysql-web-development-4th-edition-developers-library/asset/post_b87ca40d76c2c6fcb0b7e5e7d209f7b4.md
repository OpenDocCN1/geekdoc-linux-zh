
- For string types other than ENUM, the default is the empty string. For ENUM, the default is the first enumeration element. For SET, the default when the column cannot contain NULL actually is the empty set, but that is equivalent to the empty string.

You can use the `SHOW CREATE TABLE` statement to see which columns have a `DEFAULT` clause and what the default value is for those columns that have one.

### 3.2.4 Numeric Data Types

MySQL's numeric data types group into three groups:

- Exact-value types, which include the integer types and DECIMAL. Integer types are used for numbers that have no fractional part, such as 43, -3, 0, or -798432. You can use integer columns for data represented by whole numbers, such as weight to the nearest pound, height to the nearest inch, number of stars in a galaxy, number of people in a household, or number of bacteria in a petri dish. The DECIMAL type stores exact values that may have a fractional part, such as 3.14159, -.00273, or -4.78. This is a good data type for information such as monetary values. Integer and DECIMAL values are stored exactly as specified without rounding when possible, and calculations are exact.
- The floating-point types are available in single precision (FLOAT) and double precision (DOUBLE). These types, like DECIMAL, are used for numbers that may have a fractional part, but they hold approximate-value numbers such as 3.9E4F or -.01E-100 that are subject to rounding. They can be used when exact precision is not required or for values that are so large that DECIMAL cannot represent them. Some types of data you might represent as floating-point values are average crop yield, distances, or unemployment rates.
- The BIT type is used for storing bit-field values.

Values with a fractional part can be assigned to integer columns, but will be rounded using the “round half up” rule: If the fractional part is .5 or greater, the value is rounded away from zero to the next integer (up for positive values, down for negative values.) Conversely, integer values may be assigned to types that allow a fractional part. They are treated as having a fractional part of zero.

When you specify a number, you should not include commas as a separator. For example, 12345678.90 is legal, but 12,345,678.90 is not.

Table 3.6 shows the name and range of each numeric type, and Table 3.7 shows the amount of storage required for values of each type. M represents the maximum display width for integer types, the precision (number of significant digits) for floating-point and decimal types, and the number of bits for BIT. D represents the scale (number of digits following the decimal point) for types that have a fractional part; this is also known as the scale.

Storage for DECIMAL values depends on the number of digits on the left and right sides of the decimal point. For each side, 4 bytes are required for each multiple of nine digits, plus 1 to 4 bytes if there are any remaining digits. Storage per value is the sum of the left and right side storage.

A BIT(M) value requires approximately (M +7)/8 bytes.

Table 3.6 **Numeric Data Type Ranges**

| **Type Specification** | **Range** |
| :--- | :--- |
| TINYINT [ ( M ) ] | Signed values: -128 to 127 (-2⁷ to 2⁷-1); Unsigned values: 0 to 255 (0 to 2⁸-1) |
| SMALLINT [ ( M ) ] | Signed values: -32768 to 32767 (-2¹⁵ to 2¹⁵-1); Unsigned values: 0 to 65535 (0 to 2¹⁶-1) |
| MEDIUMINT [ ( M ) ] | Signed values: -8388608 to 8388607 (-2²³ to 2²³-1); Unsigned values: 0 to 16777215 (0 to 2²⁴-1) |
| INT [ ( M ) ] | Signed values: -2147483648 to 2147483647 (-2³¹ to 2³¹-1); Unsigned values: 0 to 4294967295 (0 to 2³²-1) |
| BIGINT [ ( M ) ] | Signed values: -9223372036854775808 to 9223372036854775807 (-2⁶³ to 2⁶³-1); Unsigned values: 0 to 18446744073709551615 (0 to 2⁶⁴-1) |
| DECIMAL ( ( M , D ) ) | Varies depending on M and D |
| FLOAT [ ( M , D ) ] | Minimum non-zero values: ±1.1759454351E-38; Maximum non-zero values: ±3.402823466E+38 |
| DOUBLE [ ( M , D ) ] | Minimum non-zero values: ±2.2250738585072014E-308; Maximum non-zero values: ±1.7976931348623157E+308 |
| BIT [ ( M ) ] | 0 to 2ᴹ-1 |

Table 3.7 **Numeric Data Type Storage Requirements**

| **Type Specification** | **Storage Required** |
| :--- | :--- |
| TINYINT [ ( M ) ] | 1 byte |
| SMALLINT [ ( M ) ] | 2 bytes |
| MEDIUMINT [ ( M ) ] | 3 bytes |
| INT [ ( M ) ] | 4 bytes |
| BIGINT [ ( M ) ] | 8 bytes |
| DECIMAL ( ( M , D ) ) | Varies depending on M, D |
| FLOAT [ ( M , D ) ] | 4 bytes |
| DOUBLE [ ( M , D ) ] | 8 bytes |
| BIT [ ( M ) ] | Varies depending on M |

### 3.2.4.1 Exact-Value Numeric Data Types

The exact-value data types include the integer types and the fixed-point DECIMAL type.

The integer types in MySQL are TINYINT, SMALLINT, MEDIUMINT, INT, and BIGINT. INTEGER is a synonym for INT. These types vary in the range of values they can represent and in the amount of storage space they require. (The larger the range, the more storage is required.) Integer columns can be defined as UNSIGNED to disallow negative values; this shifts the range for the column upward to begin at 0.

When you define an integer column, you can specify an optional display size M. If given, M should be an integer from 1 to 255. It represents the number of characters used to display values for the column. For example, MEDIUMINT(4) specifies a MEDIUMINT column with a display width of 4. If you define an integer column without an explicit width, a default width is assigned. The defaults are the lengths of the "longest" values for each type. Note that displayed values are not chopped to fit within M characters. If the printable representation of a particular value requires more than M characters, MySQL displays the full value.

The display size M for an integer column relates only to the number of characters used to display column values. It has nothing to do with the number of bytes of storage space required. For example, BIGINT values require 8 bytes of storage regardless of the display width. It is not possible to magically cut the required storage space for a BIGINT column in half by defining it as a BIGINT(4). Nor does M have anything to do with the range of values allowed. If you define a column as INT(3), that doesn't restrict it to a maximum value of 999.

DECIMAL is a fixed-point type: Values have a fixed number of decimals. The significance of this fact is that DECIMAL values are not subject to roundoff error the way that floating-point values are—a property that makes DECIMAL especially applicable for storing currency values.

NUMERIC and FIXED are synonyms for DECIMAL.

DECIMAL columns can be defined as UNSIGNED. Unlike the integer types, defining a DECIMAL type as UNSIGNED does not shift the type's range upward, it merely eliminates the negative end.

For a DECIMAL column, you may specify a maximum number of significant digits M and the number of decimal places D. These correspond to the concepts of "precision" and "scale" with which you may be familiar. The value of M should be from 1 to 65. The value of D should be from 0 to 30 and no greater than M.

M and D are optional. If D is omitted, it defaults to 0. If M is omitted as well, it defaults to 10. In other words, the following equivalences hold:

```
DECIMAL = DECIMAL(10) = DECIMAL(10,0)
DECIMAL(n) = DECIMAL(n,0)
```

The maximum possible range for DECIMAL is determined by the values of M and D. If you vary M and hold D fixed, the range becomes larger as M becomes larger (Table 3.8). If you hold M fixed and vary D, the range becomes smaller as D becomes larger (Table 3.9).

Table 3.8 **How M Affects the Range of DECIMAL (M, D)**

| Type Specification | Range |
| :---------------- | :-------------------------------------- |
| DECIMAL(4, 1)     | -999.9 to 999.9                        |
| DECIMAL(5, 1)     | -9999.9 to 9999.9                      |
| DECIMAL(6, 1)     | -99999.9 to 99999.9                    |

Table 3.9 **How D Affects the Range of DECIMAL (M, D)**

| Type Specification | Range |
| :---------------- | :-------------------------------------- |
| DECIMAL(4, 0)     | -9999 to 9999                          |
| DECIMAL(4, 1)     | -999.9 to 999.9                        |
| DECIMAL(4, 2)     | -99.99 to 99.99                        |

**Note**

Before MySQL 5.0.3, DECIMAL values are stored as strings and have somewhat different properties from those of the current representation. See the MySQL Reference Manual for details. To convert DECIMAL columns in an old table to the current format, dump it with mysqldump and then reload the dump file:

```text
% mysqldump db_name tbl_name > file_name
% mysql db_name < file_name
```

### 3.2.4.2 Approximate-Value Numeric Data Types

MySQL provides two floating-point types, FLOAT and DOUBLE, that hold approximate-value numbers. DOUBLE PRECISION is a synonym for DOUBLE. The REAL type is a synonym for DOUBLE by default. If the REAL_AS_DISPLAY SQL mode is enabled, REAL is a synonym for FLOAT.

Floating-point types can be defined as UNSIGNED, which eliminates the negative end of the type’s range.

For each floating-point type (just as for DECIMAL), you may specify a maximum number of significant digits M and the number of decimal places D. The value of M should be from 1 to 255. The value of D should be from 0 to 30 and no greater than M.

For FLOAT and DOUBLE, M and D are optional. If you omit both from the column definition, values are stored to the full precision allowed by your hardware.

FLOAT(P) syntax also is allowed. However, whereas P stands for the required number of bits of precision in standard SQL, it is treated differently in MySQL. P may range from 0 to 53 and is used only to determine whether the column stores single-precision or double-precision values. For P values from 0 to 24, the column is treated as single precision.
