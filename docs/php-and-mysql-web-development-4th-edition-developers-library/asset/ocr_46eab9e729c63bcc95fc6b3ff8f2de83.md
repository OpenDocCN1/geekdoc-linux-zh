+   • NAME_CONST (name,value)
+   
+   This function is used internally (for example, to write statements to the binary log). It returns value, with a column name of name. Both arguments must be constants. NAME_CONST() was introduced in MySQL 5.0.12.

+   • ROW_COUNT()
+   
+   This function operates as an SQL-level version of the mysql_affected_rows() C API function. It returns the number of rows affected by the previous statement. This is the number of rows inserted, deleted, or updated. A value of −1 indicates that the previous statement was a SELECT statement (or some other statement that returned a result set), or resulted in an error.
+   
+   ROW_COUNT() was introduced in MySQL 5.0.1.

+   • SCHEMA()
+   
+   This is a synonym for DATABASE(), introduced in MySQL 5.0.2.

+   • SESSION_USER()
+   
+   This function is a synonym for USER().

+   • SLEEP (seconds)
+   
+   Pauses for the given number of seconds and returns 0, or returns 1 if it is interrupted. The seconds argument may have a fractional part. SLEEP() was introduced in MySQL 5.0.12.

+   • SYSTEM_USER()
+   
+   This function is a synonym for USER().

+   • USER()
+   
+   Returns a utf8 string representing the username that the client specified when connecting to the MySQL server, and the host from which the client connected. The return value is a string in 'user_name@host_name' format. The value is a utf8 string; take this into account when passing the value to functions that take multiple string arguments to avoid triggering a collation-mismatch error.
+   
+   USER() → 'paul@localhost'
+   SUBSTRING_INDEX(USER(), '@',1) → 'paul'
+   SUBSTRING_INDEX(USER(), '@', -1) → 'localhost'

+   • UUID()
+   
+   Returns a “universal unique identifier.” The intent is that the return value from one call to UUID() should differ from the value from any other call. Uniqueness of the return value is not absolutely guaranteed, but duplicated values should be very unlikely.
+   
+   UUID() → '455088e8-3c1e-1027-9cc8-78fa1f8d4d6b'
+   UUID() → 'cbb9ad76-3d10-1027-8c06-349c716080d3'