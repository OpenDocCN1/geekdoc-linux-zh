```
```
+------------------+
mysql> SELECT GROUP_CONCAT(name SEPARATOR ':') FROM t;
+------------------+
| GROUP_CONCAT(name SEPARATOR ':') |
+------------------+
| dog:cat:rat:dog:rat |
+------------------+

mysql> SELECT GROUP_CONCAT(name ORDER BY name DESC) FROM t;
+-------------------------------+
| GROUP_CONCAT(name ORDER BY name DESC) |
+-------------------------------+
| rat,rat,dog,dog,cat        |
+-------------------------------+

mysql> SELECT GROUP_CONCAT(DISTINCT name ORDER BY name) FROM t;
+-------------------------------+
| GROUP_CONCAT(DISTINCT name ORDER BY name) |
+-------------------------------+
| cat,dog,rat                 |
+-------------------------------+
```
```

+   MAX([DISTINCT] expr)
+   
+   Returns the maximum value of *expr* for all non-`NULL` values in the selected rows. Returns `NULL` if there are no non-`NULL` values. MAX() also can be used with strings or temporal values, in which case it returns the lexically or temporally greatest value.

```
```
SELECT MAX(mycol1) FROM mytbl            → 9

DISTINCT causes MAX() to return the maximum of the distinct *expr* values (which
does not change the result).
```
```

+   MIN([DISTINCT] expr)
+   
+   Returns the minimum value of *expr* for all non-`NULL` values in the selected rows. Returns `NULL` if there are no non-`NULL` values. MIN() also may be used with strings or temporal values, in which case it returns the lexically or temporally least value.

```
```
SELECT MIN(mycol1) FROM mytbl            → 1

DISTINCT causes MIN() to return the minimum of the distinct *expr* values (which
does not change the result).
```
```

+   STD(*expr*)
+   
+   STDDEV(*expr*)
+   
+   STDDEV_POP(*expr*)
+   
+   Returns the population standard deviation of *expr* for all non-`NULL` values in the selected rows. Returns `NULL` if there are no non-`NULL` values.

```
```
SELECT STDDEV_POP(mycol) FROM mytbl      → 2.7701
```
```