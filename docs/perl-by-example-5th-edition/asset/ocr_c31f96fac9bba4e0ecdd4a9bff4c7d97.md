# EXAMPLE B.39

```
mysql> select CategoryID, SUM(UnitsInStock) as 'Total Units in Stock'
    -> FROM products
    -> GROUP BY CategoryID;
```

| CategoryID | Total Units in Stock |
| :--- | :--- |
| NULL | 0 |
| 1 | 559 |
| 2 | 507 |
| 3 | 386 |
| 4 | 393 |
| 5 | 308 |
| 6 | 165 |
| 7 | 100 |
| 8 | 701 |

9 rows in set (0.00 sec)

# EXAMPLE B.40

```
mysql> select C.CategoryName,
    -> SUM(P.UnitsInStock) AS Units
    -> FROM products AS P
    -> join categories AS C ON C.CategoryID=
    -> P.CategoryID Group By C.CategoryName;
```

| CategoryName | Units |
| :--- | :--- |
| Beverages | 559 |
| Condiments | 507 |
| Confections | 386 |
| Dairy Products | 393 |
| Grains/Cereals | 308 |
| Meat/Poultry | 165 |
| Produce | 100 |
| Seafood | 701 |

8 rows in set (0.00 sec)