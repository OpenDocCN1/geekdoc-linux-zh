```
**EXAMPLE B.12**

```
mysql> SELECT CategoryName from categories WHERE CategoryName < 'D';
+-----------+
| CategoryName|
+-----------+
| Beverages  |
| Condiments |
| Confections |
+-----------+
3 rows in set (0.00 sec)
```
```

**The AND and OR Operators.** AND or OR operators are used in a WHERE clause to further qualify what data you want to select from a table. The AND operator tests one or more conditions to see if all the conditions are true; if so, SELECT displays the rows. The OR operator displays a row if only one of the conditions listed is true. The AND operator can be designated by the && symbol, and the OR operator can be designated as ||.

```
**EXAMPLE B.13**

```
mysql> SELECT ContactName FROM Suppliers
       -> WHERE City = 'Montreal' AND Region = 'Quebec';

+--------------+
| ContactName   |
+--------------+
| Jean-Guy Lauzon |
+--------------+
1 row in set (0.03 sec)
```
```

**EXPLANATION**

When using the && (AND) operator, both of the conditions being tested in the WHERE clause must be true; that is, both the City must be Montreal and the Region must be Quebec. If both conditions are true, then SELECT will print the ContactName from the Suppliers database.