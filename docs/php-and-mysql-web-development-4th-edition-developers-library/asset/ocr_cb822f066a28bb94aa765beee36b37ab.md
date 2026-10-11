Returns the bitwise exclusive-OR value of *expr* for all non-NULL values in the elected rows. Returns 0 if there are no non-NULL values.

SELECT BIT_XOR(mycol1) FROM mytbl → 5

COUNT(*expr*)
COUNT(*)
COUNT(DISTINCT expr1, expr2, . . . )

With an expression argument, returns a count of the number of non-NULL values in the result set. Returns 0 if there are no non-NULL values. With an argument of '*', returns a count of all rows in the result set, regardless of their contents.

SELECT COUNT(mycol1) FROM mytbl → 7
SELECT COUNT(*) FROM mytbl → 8

For MySQL tables, COUNT(*) with no WHERE clause is optimized to return the number of rows in the table named in the FROM clause very quickly. When more than one table is named, COUNT(*) returns the product of the number of rows in the individual tables.

SELECT COUNT(*) FROM mytbl AS m1 INNER JOIN mytbl AS m2 → 64

COUNT(DISTINCT) can be used to count the number of distinct non-NULL values.

SELECT COUNT(DISTINCT mycol) FROM mytbl → 5
SELECT COUNT(DISTINCT MOD(mycol,3)) FROM mytbl → 3

If multiple expressions are given, COUNT(DISTINCT) counts the number of distinct combinations of non-NULL values.

GROUP_CONCAT([DISTINCT] var_list [ORDER BY . . .] [SEPARATOR *str*])

This function concatenates the non-NULL values in a group of strings and returns the result. It returns NULL if there are no non-NULL values. You can use DISTINCT to remove duplicates, ORDER BY to sort the results, and SEPARATOR to specify the delimiter between strings. By default, GROUP_CONCAT() does not perform duplicate removal or sorting, and separates values by commas.

Values returned by GROUP_CONCAT() are limited in length to the value of the group_concat_max_len system variable. You can change the value of this variable to enable longer values.

mysql> CREATE TABLE t (name CHAR(10));
mysql> INSERT INTO t VALUES('dog'),('cat'),('rat'),('dog'),('rat');
mysql> SELECT GROUP_CONCAT(name) FROM t;
+-------------------+
| GROUP_CONCAT(name)|
+-------------------+
| dog,cat,rat,dog,rat |
+-------------------+