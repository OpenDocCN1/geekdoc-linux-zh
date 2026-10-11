# **EXAMPLE 15.12 (CONTINUED)**

```
3  mysql> SELECT name, title FROM coaches WHERE team = 'Chico Hardhats';
    +-------------+-----------------+
    | name        | title           |
    +-------------+-----------------+
    | John Doe    | Head Coach      |
    | Jack Mattsone | Offensive Coach |
    +-------------+-----------------+
    2 rows in set (0.00 sec)

```

```
4  mysql> SELECT name FROM coaches WHERE name LIKE 'J%';
    +-------------+
    | name        |
    +-------------+
    | John Doe    |
    | Jack Mattsone |
    | Joe Hayes   |
    +-------------+
    3 rows in set (0.00 sec)

```

```
5  mysql> SELECT name FROM teams WHERE wins > 10 && losses < 10;
    +--------------+
    | name         |
    +--------------+
    | Bath Warships |
    +--------------+
    1 row in set (0.00 sec)

```

```
6  mysql> SELECT name FROM coaches WHERE id BETWEEN 1 AND 3;
    +-------------+
    | name        |
    +-------------+
    | John Doe    |
    | Jack Mattsone |
    | Bud Wilkins  |
    +-------------+
    3 rows in set (0.00 sec)

```

# **EXPLANATION**

+   1. The *SELECT* statement retrieves the name of teams from the table called *teams* where the number of wins was greater than 25.
+   2. The *SELECT* statement retrieves the name of teams from the table called *teams* where the number of losses was less than the number of wins.
+   3. The *SELECT* statement retrieves the names of coaches and their titles from the table called *coaches* if their team is equal to the string 'Chico Hardhats'. The string must be quoted in either single or double quotes, and the match must be exact.
+