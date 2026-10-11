
## 15.3 Getting Started with MySQL

### EXAMPLE 15.9

```sql
1 mysql> INSERT INTO teams
      -> SET name='Fremont Tigers',
      -> wins=24,
      -> losses=26;
  Query OK, 1 row affected (0.00 sec)

2 mysql> INSERT INTO teams
      -> SET name='Chico Hardhats',
      -> wins=19,
      -> losses=25;
  Query OK, 1 row affected (0.00 sec)

3 mysql> INSERT INTO teams VALUES
      -> ('Bath Warships',32,3);
  Query OK, 1 row affected (0.00 sec)

4 mysql> INSERT INTO teams VALUES
      -> ('Bangor Rams', 22, 24);
  Query OK, 1 row affected (0.00 sec)

5 mysql> SELECT name FROM teams;
  +---------------------+
  | name                |
  +---------------------+
  | Fremont Tigers      |
  | Chico Hardhats      |
  | Bath Warships       |
  | Bangor Rams         |
  +---------------------+
  4 rows in set (0.00 sec)

mysql> INSERT INTO coaches VALUES
      -> ('', 'John Doe', 'Chico Hardhats', 'Head Coach', 20021210);
  Query OK, 1 row affected, 1 warning (0.05 sec)

6 mysql> INSERT INTO coaches VALUES
      -> ('', 'Jack Mattson', 'Chico Hardhats', 'Offensive Coach',
      '20041005');
  Query OK, 1 row affected, 1 warning (0.00 sec)

7 mysql> INSERT INTO coaches(name, team, title, start_date)
      -> VALUES ('Bud Wilkins','Fremont Tigers', 'Head Coach',
      '19990906');
  Query OK, 1 row affected (0.03 sec)

8 mysql> INSERT INTO coaches(name, team, title, start_date)
      -> VALUES ('Joe Hayes', 'Fremont Tigers', 'Defensive Coach',
      '19980616');
  Query OK, 1 row affected (0.02 sec)
```

### EXPLANATION

- 1. The fields and values are assigned using the SET clause within the INSERT statement. For any field not named in the SET, MySQL assigns its default value.
- 2. Again, the fields and values are inserted using the SET clause.
- 3. In this example, the INSERT statement contains a VALUES list where a value for each field is assigned in the order it was specified when the table was created. To see the order, if you are not sure, use the DESCRIBE statement as shown in the previous example.
- 4. The VALUES list is repeated in this example for a new record. Note that the date is inserted in the format yyyy-mm-dd.
- 5. The SELECT statement displays the names of all the teams that have been inserted into the table.
- 6-9 More records are inserted with the VALUES list.

## Selecting Data from Tables—The SELECT Command.

One of the most commonly used SQL commands is SELECT, mandatory when performing a query. The SELECT command is used to retrieve data from a table based on some criteria. It specifies a comma-separated list of fields to be retrieved, and the FROM clause specifies the table(s) to be accessed. The results are stored in a result table known as the result set, just a little table itself. The * symbol can be used to represent all of the fields.

### Selecting by Columns.

In the following examples, data is retrieved for specific columns, each column (field) separated by a comma.

### EXAMPLE 15.10

```sql
1 mysql> SELECT name FROM teams;
| name |
| Fremont Tigers |
| Chico Hardhats |
| Bath Warships |
| Bangor Rams |
4 rows in set (0.00 sec)

2 mysql> SELECT name, wins FROM teams;
| name | wins |
| Bangor Rams | 22 |
| Bath Warships | 32 |
| Fremont Tigers | 24 |
| Chico Hardhats | 19 |
4 rows in set (0.00 sec)
```

![](img/8556abcb353c0991f12099420ec28735_576_0.png)

```sql
3 mysql> SELECT id, name, title FROM coaches;
| id | name            | title          |
+----+-----------------+------------------+
|  1 | John Doe        | Head Coach       |
|  2 | Jack Mattison   | Offensive Coach  |
|  3 | Bud Wilkins     | Head Coach       |
|  4 | Joe Haynes      | Defensive Coach  |
+----+-----------------+------------------+
4 rows in set (0.00 sec)
```

![](img/8556abcb353c0991f12099420ec28735_576_1.png)

- 1. The SELECT statement retrieves all values in the *name* field from the *teams* table.
- 2. The SELECT statement retrieves all values in the *name* field and the *wins* field from the table called *teams*. The list of field names are separated with a comma.
- 3. The SELECT statement retrieves all values in the *id* field, the *name* field, and the *title* field from the *coaches* table.

**Selecting All Columns.** The * is a wildcard that is used to represent all of the columns in a table.

![](img/8556abcb353c0991f12099420ec28735_576_2.png)

```sql
1 mysql> SELECT * FROM teams;
| name            | wins | losses |
+-----------------+------+--------+
| Fremont Tigers  |  24  |   26   |
| Chico Hardhats  |  19  |   25   |
| Bath Warships   |  32  |    3   |
| Bangor Rams     |  22  |   24   |
+-----------------+------+--------+

2 mysql> SELECT * FROM coaches;
| id | name        | team          | title            | start_date |
+----+-------------+---------------+------------------+------------+
|  1 | John Doe    | Chico Hardhats| Head Coach       | 2002-12-10 |
|  2 | Jack Mattison| Chico Hardhats| Off. Coach      | 2004-10-05 |
|  3 | Bud Wilkins | Fremont Tigers| Head Coach       | 1999-09-06 |
|  4 | Joe Haynes  | Fremont Tigers| Def. Coach      | 1998-06-16 |
+----+-------------+---------------+------------------+------------+
4 rows in set (0.00 sec)
```

![](img/8556abcb353c0991f12099420ec28735_576_3.png)

- 1. The SELECT statement retrieves all fields and values from the table called *teams*.
- 2. The SELECT statement retrieves all fields and values from the table called *coaches*.

### The WHERE Clause.

The WHERE clause is optional and specifies which data values or rows will be selected based on some condition, called a selection criterion. SQL provides a set of operators to qualify the condition being set (see Table 15.4).

#### Table 15.4 SQL Operators

| Operator | Description | Example |
|---|---|---|
| = | Equal to | WHERE country = 'Sweden' |
| <>, != | Not equal to* | WHERE country <> 'Sweden' |
| > | Greater than | WHERE salary > 50000 |
| < | Less than | WHERE salary < 50000 |
| >= | Greater than or equal | |
| <= | Less than or equal | |
| IS [NOT] NULL | IS NULL (no value) or NOT NULL | WHERE birth = NULL |
| BETWEEN | Between an inclusive range | WHERE last_name BETWEEN 'Doe' AND 'Hayes' |
| LIKE | Search for value like a pattern | WHERE last_name LIKE 'D%' |
| NOT LIKE | Search for a value not like a pattern | WHERE country NOT LIKE 'Sw%' |
| !, NOT | logical NOT for negation | WHERE status ! is_married. |
| \|\|, OR | logical OR | WHERE order_number > 10 \|\| part_number = 80 |
| &&, AND | logical AND | WHERE age > 12.6 && age < 21 |
| XOR | Exclusive OR | WHERE status = 1 XOR range = 1 |

\* In some versions of SQL, the <> operator may be written as !=

### EXAMPLE 15.12

```sql
1 mysql> SELECT name, wins FROM teams WHERE wins > 25;
+-------------------+-------+
| name              | wins  |
+-------------------+-------+
| Bath Destroyers   | 34    |
| Portland Penguins | 28    |
+-------------------+-------+

2 mysql> SELECT name FROM teams WHERE losses < wins;
+---------------+
| name          |
+---------------+
| Bath Warships |
+---------------+
1 row in set (0.03 sec)
```

```sql
3 mysql> SELECT name, title FROM coaches WHERE team = 'Chico Hardhats';
    +-------------+-----------------+
    | name        | title           |
    +-------------+-----------------+
    | John Doe    | Head Coach      |
    | Jack Mattson| Offensive Coach |
    +-------------+-----------------+
    2 rows in set (0.00 sec)

4 mysql> SELECT name FROM coaches WHERE name LIKE 'J%';
    +-------------+
    | name        |
    +-------------+
    | John Doe    |
    | Jack Mattson|
    | Joe Hayes   |
    +-------------+
    3 rows in set (0.00 sec)

5 mysql> SELECT name FROM teams WHERE wins > 10 && losses < 10;
    +--------------+
    | name         |
    +--------------+
    | Bath Warships |
    +--------------+
    1 row in set (0.00 sec)

6 mysql> SELECT name FROM coaches WHERE id BETWEEN 1 AND 3;
    +-------------+
    | name        |
    +-------------+
    | John Doe    |
    | Jack Mattson|
    | Bud Wilkins  |
    +-------------+
    3 rows in set (0.00 sec)
```

### EXPLANATION

- 1. The *SELECT* statement retrieves the name of teams from the table called *teams* where the number of wins was greater than 25.
- 2. The *SELECT* statement retrieves the name of teams from the table called *teams* where the number of losses was less than the number of wins.
- 3. The *SELECT* statement retrieves the names of coaches and their titles from the table called *coaches* if their team is equal to the string 'Chico Hardhats'. The string must be quoted in either single or double quotes, and the match must be exact.
