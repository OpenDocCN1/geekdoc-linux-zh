# 1.4.9.4 Limiting Query Results

When a query returns many rows, but you want to see only a few of them, add a LIMIT clause. *LIMIT* is especially useful in conjunction with *ORDER BY*. MySQL enables you to limit the output of a query to the first *n* rows of the result that otherwise would be returned. The following query selects the five presidents who were born first:

```
```
mysql> SELECT last_name, first_name, birth FROM president
       -> ORDER BY birth LIMIT 5;
+------------+------------+------------+
| last_name | first_name | birth      |
+------------+------------+------------+
| Washington | George     | 1732-02-22 |
| Adams      | John       | 1735-10-30 |
| Jefferson  | Thomas     | 1743-04-13 |
| Madison    | James      | 1751-03-16 |
| Monroe     | James      | 1758-04-28 |
+------------+------------+------------+
```
```

If you sort in reverse order, using *ORDER BY birth DESC*, you get the five most recently born presidents instead:

```
```
mysql> SELECT last_name, first_name, birth FROM president
       -> ORDER BY birth DESC LIMIT 5;
+------------+------------+------------+
| last_name | first_name | birth      |
+------------+------------+------------+
| Clinton   | William J. | 1946-08-19 |
| Bush      | George W.  | 1946-07-06 |
| Carter    | James E.   | 1924-10-01 |
| Bush      | George H.W.| 1924-06-12 |
| Kennedy   | John F.    | 1917-05-29 |
+------------+------------+------------+
```
```

*LIMIT* also enables you to pull a section of rows out of the middle of a result set. To do this, you must specify two values. The first value is the number of rows to skip at the beginning of the result set, and the second is the number of rows to return. The following query is similar to the previous one but returns 5 rows after skipping the first 10:

```
```
mysql> SELECT last_name, first_name, birth FROM president
       -> ORDER BY birth DESC LIMIT 10, 5;
+------------+------------+------------+
| last_name | first_name | birth      |
+------------+------------+------------+
| Truman     | Harry S.   | 1884-05-08 |
| Roosevelt  | Franklin D.| 1882-01-30 |
| Hoover     | Herbert C. | 1874-08-10 |
| Coolidge   | Calvin     | 1872-07-04 |
| Harding    | Warren G.  | 1865-11-02 |
+------------+------------+------------+
```
```