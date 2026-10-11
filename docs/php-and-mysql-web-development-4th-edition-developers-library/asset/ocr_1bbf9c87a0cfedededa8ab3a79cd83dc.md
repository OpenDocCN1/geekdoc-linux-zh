+------------+-------------+------------+
| last_name  | first_name  | birth      |
+------------+-------------+------------+
| Harding    | Warren G.   | 1865-11-02 |
| Poik       | James K.    | 1795-11-02 |
+------------+-------------+------------+

Using DAYOFYEAR() rather than the combination of MONTH() and DAYOFMONTH() would result in a simpler query, but it would produce incorrect results when comparing dates from leap years to dates from nonleap years.

Another kind of multiple-table retrieval uses a “subquery,” which is one SELECT nested within another. There are several types of subqueries, and are discussed further in Section 2.9, “Performing Multiple-Table Retrievals with Subqueries.” For now, a couple of examples will do. Suppose that you want to identify those students who have perfect attendance. This is equivalent to determining which students are not represented in the absence table, which can be done like this:

```
mysql> SELECT * FROM student
    -> WHERE student_id NOT IN (SELECT student_id FROM absence);
```

+------+-----+------------+
| name | sex | student_id |
+------+-----+------------+
| Megan  | F   | 1          |
| Joseph | M   | 2          |
| Katie  | F   | 4          |
| Nathan | M   | 6          |
| Liesl  | F   | 7          |
+------+-----+------------+

The nested SELECT determines the set of student_id values that are present in the absence table, and the outer SELECT retrieves student rows that don’t match any of those IDs.

A subquery also provides a single-statement solution to the question asked in Section 1.4.9.8, “Setting and Using User-Defined Variables,” about which presidents were born before Andrew Jackson. The original solution used two statements and a user variable, but it can be done with a subquery as follows:

```
mysql> SELECT last_name, first_name, birth FROM president
    -> WHERE birth < (SELECT birth FROM president
    ->  WHERE last_name = 'Jackson' AND first_name = 'Andrew');
```

+------------+------------+------------+
| last_name  | first_name | birth      |
+------------+------------+------------+
| Washington | George     | 1732-02-22 |
| Adams      | John       | 1735-10-30 |
| Jefferson  | Thomas     | 1743-04-13 |
| Madison    | James      | 1751-03-16 |
| Monroe     | James      | 1758-04-28 |
+------------+------------+------------+