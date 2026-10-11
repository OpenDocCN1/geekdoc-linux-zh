$n specifies the number of the placeholder to which the value $value should be bound and should be in the range from 1 to the number of placeholders. To bind a NULL value, $value should be undef.

The \&attr or \&bind_type parameter may be supplied as a hint about the type of the value to be bound. The default is to treat the variable as a VARCHAR, so non-NULL values are quoted when bound to the statement. This is normally sufficient because MySQL converts string values in statements to other data types as necessary, but can cause problems in some contexts. For example, any argument to a LIMIT clause must be an integer. To specify that a value represents an integer, you can invoke bind_param() in either of the following ways:

```
$rv = \$sth->bind_param (\$n, \$value, { TYPE => DBI::SQL_INTEGER });
$rv = \$sth->bind_param (\$n, \$value, DBI::SQL_INTEGER);
```

+   - $rv = \$sth->bind_param_array (\$n, \$values [, \&attr]);
+   - $rv = \$sth->bind_param_array (\$n, \$values [, \$bind_type]);
+   This function is similar to bind_param(), except that it is intended for use with a prepared statement to be executed with execute_array(). The $values argument can be either a reference to an array of values, or a single scalar value. For an array reference, successive values in the array are used for successive executions of the statement. For a scalar, the value is reused for each execution.

+   - $rows = \$sth->dump_results ({\$maxlen
+   [, \$line_sep
+   [, \$field_sep
+   [, \$fh]]}});
+   
+   Fetche all rows from the statement handle $sth, formats them by calling the utility function DBI::neat_list(), and prints them to the given file handle. Returns the number of rows fetched.
+   
+   The defaults for the $maxlen, $line_sep, $field_sep, and $fh parameters are 35, "\n", ", ", and STDOUT.

+   - $rv = \$sth->execute ([@bind_values]);
+   Executes a prepared statement. For SELECT statements, execute() returns true if the statement executed successfully, or undef if an error occurred. For non-SELECT statements, the return value is the number of rows affected, -1 if the number of rows is unknown, and undef if an error occurred. If the number of rows affected is zero, the return value is the string "0E0", which evaluates as zero in numeric contexts but is considered true in boolean contexts.
+   
+   The @bind_values parameter has the same meaning as for the do() method.

+   - $rv = \$sth->execute_array ([\&attr [, @bind_values]]);
+   Executes a prepared statement multiple times. The number of executions is determined by the number of values passed via @bind_values, the values bound to the statement by earlier calls to bind_param_array(), or by the attribute reference.