```
```mysql> SELECT @count := COUNT(*) FROM member;
+-------------------------+
| @count := COUNT(*) |
+-------------------------+
|                   102 |
+-------------------------+```
```

User variables can be assigned integer, decimal, floating-point, string, or NULL values, and can be assigned from arbitrary expressions, including those that refer to other variables. If you access a user variable that has not yet been assigned a value explicitly, its value is NULL.

User variable values do not persist across sessions with the server. That is, values are lost when a connection terminates.

In SELECT statements that return multiple rows, variable assignments are performed for each row. The final value is the value assigned for the last row.

String-valued user variables have the same character set and collation as those of the value they are assigned:

```
```mysql> SET @s = CONVERT('abc' USING latin2) COLLATE latin2_czech_cs;
mysql> SELECT CHARSET(@s), COLLATION(@s);
+------------+------------------+ 
| CHARSET(@s) | COLLATION(@s) | 
+------------+------------------+ 
| latin2     | latin2_czech_cs| 
+------------+------------------+```
```