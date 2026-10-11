```
```
+------------+
| COUNT(*) |
+------------+
|    16 |
+------------+
```
```

However, although that approach works, it’s tedious and not really very well suited for columns that might have several different values. Consider how you’d determine the number of presidents born in each state this way.You’d have to find out which states are represented so as not to miss any (*SELECT DISTINCT state FROM president*), and then run a *SELECT COUNT (*)* query for each state. That is clearly something you don’t want to do.

Fortunately, it’s possible to use a single query to count how many times each distinct value occurs in a column. For the student list, count boys and girls separately using a *GROUP BY* clause:

```
```sql
mysql> SELECT sex, COUNT(*) FROM student GROUP BY sex;
```
```

```
```
+----+----------+
| sex | COUNT(*) |
+----+----------+
| F |    15 |
| M |    16 |
+----+----------+
```
```

The same form of query tells us how many presidents were born in each state:

```
```sql
mysql> SELECT state, COUNT(*) FROM president GROUP BY state;
```
```

```
```
+-------+----------+
| state | COUNT(*) |
+-------+----------+
| AR | 1 |
| CA | 1 |
| CT | 1 |
| GA | 1 |
| IA | 1 |
| IL | 1 |
| KY | 1 |
| MA | 4 |
| MO | 1 |
| NC | 2 |
| NE | 1 |
| NH | 1 |
| NJ | 1 |
| NY | 4 |
| OH | 7 |
| PA | 1 |
| SC | 1 |
| TX | 2 |
| VA | 8 |
+-------+----------+
```
```