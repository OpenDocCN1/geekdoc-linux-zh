```
mysql> SELECT last_name, first_name FROM president
         -> WHERE last_name='roosevelt' ;
+------------------------------------+
| last_name     | first_name         |
+------------------------------------+
| Roosevelt    | Theodore           |
| Roosevelt    | Franklin D.      |
+------------------------------------+

```

You can look for dates:

```
mysql> SELECT last_name, first_name, birth FROM president
         -> WHERE birth < '1750-1-1';
+--------------------------------------------+
| last_name     | first_name         | birth     |
+--------------------------------------------+
| Washington  | George           | 1732-02-22 |
| Adams       | John             | 1735-10-30 |
| Jefferson   | Thomas           | 1743-04-13 |
+--------------------------------------------+

```

It’s also possible to search for combinations of values:

```
mysql> SELECT last_name, first_name, birth, state FROM president
         -> WHERE birth < '1750-1-1' AND (state='VA' OR state='MA');
+-------------------------------------------------
| last_name     | first_name         | birth      | state |
+-------------------------------------------------
| Washington  | George           | 1732-02-22 | VA    |
| Adams       | John             | 1735-10-30 | MA    |
| Jefferson   | Thomas           | 1743-04-13 | VA    |
+-------------------------------------------------

```

Expressions in `WHERE` clauses can use arithmetic operators (Table 1.1), comparison operators (Table 1.2), and logical operators (Table 1.3). You can also use parentheses to group parts of an expression. Operations can be performed using constants, table columns, and function calls. We will have occasion to use several of MySQL’s functions in statements throughout this tutorial, but there are far too many to show here. See Appendix C, “Operator and Function Reference,” for a complete list.

# Table 1.1    Arithmetic Operators

| Operator | Meaning          |
| :---     | :---             |
| +        | Addition         |
| –        | Subtraction      |