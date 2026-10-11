```
`ON UPDATE CURRENT_TIMESTAMP` `... other columns ...` `);`
```

When you insert a new row, set both `TIMESTAMP` columns to `NULL` to set them to the insertion timestamp. When you update an existing row, leave both columns alone; `t_modified` will be updated automatically to the modification timestamp if any other columns change value.

# 3.2.6.3  The `YEAR` Data Type

`YEAR` is a one-byte data type intended for efficient representation of year values. A `YEAR` column definition may include a specification for a display width *N*, which should be either 4 or 2. If you omit *N* from a `YEAR` definition, the default is 4. `YEAR(4)` has a range of `1901` to `2155`. `YEAR(2)` has a range of `1970` to `2069`, but only the last two digits are displayed. You can use the `YEAR` type when you want to store date information but only need the year part of the date, such as year of birth, year of election to office, and so forth. When you do not require a full date value, `YEAR` is much more space-efficient than other date types.

`TINYINT` has the same storage size as `YEAR` (one byte), but not the same range. To cover the same range of years as `YEAR` by using an integer type, you would need a `SMALLINT`, which takes twice as much space. If the range of years you need to represent coincides with the range of the `YEAR` type, `YEAR` is more space-efficient than `SMALLINT`. Another advantage of `YEAR` over an integer column is that MySQL converts two-digit values into four-digit values for you using MySQL’s usual year-guessing rules. For example, `97` and `14` become `1997` and `2014`. However, be aware that inserting the numeric value `00` into a four-digit `YEAR` column results in the value `0000` being stored, not `2000`. If you want a value of `00` to convert to `2000`, specify it in string form as `'0'` or `'00'`.

# 3.2.6.4  Date and Time Data Type Attributes

The following remarks apply to all temporal types except `TIMESTAMP`:

+   *   The general attributes `NULL` or `NOT NULL` may be specified. If you don’t specify either of them, `NULL` is the default.

+   *   You can also specify a default value using a `DEFAULT` clause. Section 3.2.3, “Specifying Column Default Values,” described the rules that MySQL uses for assigning a default value if a column definition includes no `DEFAULT` clause.

Note that because default values must be constants, you cannot use a function such as `NOW()` to supply a value of “the current date and time” as the default for a `DATETIME` column. To achieve that result, set the column value explicitly to `NOW()` whenever you create a new row, or else consider using a `TIMESTAMP` column instead. Alternatively, set up a trigger that initializes the column to the appropriate value; see Section 4.3, “Triggers.”

`TIMESTAMP` columns are special; the default for the first such column in a table is the current date and time, and the “zero” value for any others. However, the full set of rules