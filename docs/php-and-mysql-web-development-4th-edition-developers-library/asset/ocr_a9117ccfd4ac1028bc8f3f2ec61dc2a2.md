the column. Default value handling is described in Section 3.2.3, "Configuring Time Zone Support."

If multiple column attributes are present, there are some constraints on the order in which they may appear. In general, you should be safe if you specify data type-specific attributes such as `UNSIGNED` or `ZEROFILL` before general attributes such as `NULL` or `NOT NULL`.

# 3.2.3 Specifying Column Default Values

For all but BLOB and TEXT types, spatial types, or columns with the `AUTO_INCREMENT` attribute, you can specify a `DEFAULT def_value` clause to indicate that a column should be assigned the value `def_value` when a new row is created that does not explicitly specify the column's value. With some limited exceptions for `TIMESTAMP` columns, `def_value` must be a constant. It cannot be an expression or refer to other columns.

If a column definition includes no explicit `DEFAULT` clause and the column can take `NULL` values, its default value is `NULL`. Otherwise, the handling of a missing `DEFAULT` clause is version dependent.

From MySQL 5.0.2 on, the column is created without any `DEFAULT` clause. That is, it has no default value. This affects how the server handles the column if a new row that does not specify a value for the column is inserted into the table:

+   * When strict SQL mode is not in effect, the column is set to the implicit default for its data type. (Implicit defaults are described shortly)

+   * When strict SQL mode is in effect, an error occurs if the table is transactional. The statement aborts and rolls back. For non-transactional tables, an error occurs and the statement aborts if the row is the first row inserted by the statement. If it is not the first row, you can elect to have the statement abort or to have the column set to its implicit default with a warning. The choice depends on which strict mode setting is in effect. See Section 3.3, "How MySQL Handles Invalid Data Values," for details.

Before MySQL 5.0.2, MySQL defines the column with a `DEFAULT` clause that specifies the implicit default value.

The implicit default for a column depends on its data type:

+   * For numeric columns, the default is 0, except for columns that have the `AUTO_INCREMENT` attribute. For `AUTO_INCREMENT`, the default is the next number in the column sequence.

+   * For date and time types except `TIMESTAMP`, the default is the "zero" value for the type (for example, `'0000-00-00'` for DATE). For `TIMESTAMP`, the default is the current date and time for the first `TIMESTAMP` column in a table, and the `"zero"` value for any following `TIMESTAMP` columns. (`TIMESTAMP` defaults actually are more complex and are discussed in Section 3.2.6.2, "The `TIMESTAMP` Data Type.")