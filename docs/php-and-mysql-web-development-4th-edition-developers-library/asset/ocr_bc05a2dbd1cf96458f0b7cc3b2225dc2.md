+   ```
+   Sary_ref = $sth->{SCALE};
+   ```
+   
+   A reference to an array of values indicating the scale of each column. DBI uses “scale” in the ODBC sense, which for MySQL means the number of decimal places for floating-point columns. For other columns where scale is not applicable, the scale is undef.

+   ```
+   $str = $sth->{Statement};
+   ```
+   
+   The text of the statement associated with `$sth`, as seen by `prepare()` before any placeholder substitution takes place.

+   ```
+   Sary_ref = $sth->{TYPE};
+   ```
+   
+   A reference to an array of values indicating the numeric type of each column. This attribute contains portable type numbers. The `mysql_type` attribute may be accessed to obtain MySQL-specific type numbers.

# H.4.5  MySQL-Specific Statement-Handle Attributes

These attributes are specific to the DBI MySQL driver, DBD::mysql. Most of them should be considered read-only and should be accessed after invoking `execute()`. The exception is the `mysql_use_result` attribute, which should be set after `prepare()` but before `execute()`. See the `mysql_use_result` description for an example.

+   ```
+   $rv = $sth->{mysql_insertid};
+   ```
+   
+   The AUTO_INCREMENT value that was most recently generated on the connection associated with `$sth`.

+   ```
+   Sary_ref = $sth->{mysql_is_auto_increment};
+   ```
+   
+   A reference to an array of values indicating whether each column is an AUTO_INCREMENT column.

+   ```
+   Sary_ref = $sth->{mysql_is_blob};
+   ```
+   
+   A reference to an array of values indicating whether each column is a BLOB type. Values in this array are true for the TEXT types as well.

+   ```
+   Sary_ref = $sth->{mysql_is_key};
+   ```
+   
+   A reference to an array of values indicating whether each column is part of a key.

+   ```
+   Sary_ref = $sth->{mysql_is_num};
+   ```
+   
+   A reference to an array of values indicating whether each column is a numeric type.

+   ```
+   Sary_ref = $sth->{mysql_is_pri_key};
+   ```
+   
+   A reference to an array of values indicating whether each column is part of a PRIMARY KEY.