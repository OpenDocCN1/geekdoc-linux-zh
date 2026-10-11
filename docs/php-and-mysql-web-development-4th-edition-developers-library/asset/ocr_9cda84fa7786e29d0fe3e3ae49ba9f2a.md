Table 3.8 **How $M$ Affects the Range of DECIMAL ($M$, $D$)**

| Type Specification | Range |
| :---------------- | :-------------------------------------- |
| DECIMAL(4, 1)     | -999.9 to 999.9                        |
| DECIMAL(5, 1)     | -9999.9 to 9999.9                      |
| DECIMAL(6, 1)     | -99999.9 to 99999.9                    |

Table 3.9 **How $D$ Affects the Range of DECIMAL ($M$, $D$)**

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

# 3.2.4.2 **Approximate-Value Numeric Data Types**

MySQL provides two floating-point types, FLOAT and DOUBLE, that hold approximate-value numbers. DOUBLE PRECISION is a synonym for DOUBLE. The REAL type is a synonym for DOUBLE by default. If the REAL_AS_DISPLAY SQL mode is enabled, REAL is a synonym for FLOAT.

Floating-point types can be defined as UNSIGNED, which eliminates the negative end of the type’s range.

For each floating-point type (just as for DECIMAL), you may specify a maximum number of significant digits $M$ and the number of decimal places $D$. The value of $M$ should be from 1 to 255. The value of $D$ should be from 0 to 30 and no greater than $M$.

For FLOAT and DOUBLE, $M$ and $D$ are optional. If you omit both from the column definition, values are stored to the full precision allowed by your hardware.

FLOAT($P$) syntax also is allowed. However, whereas $P$ stands for the required number of bits of precision in standard SQL, it is treated differently in MySQL. $P$ may range from 0 to 53 and is used only to determine whether the column stores single-precision or double-precision values. For $P$ values from 0 to 24, the column is treated as single