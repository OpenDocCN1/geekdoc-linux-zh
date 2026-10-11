# **EXAMPLE B.15**

```
mysql> SELECT CompanyName, Country FROM Customers
-> WHERE Country LIKE 'Sw%';
+-----------------+-----------+
| CompanyName     | Country   |
+-----------------+-----------+
| Berglunds snabbkop | Sweden    |
| Chop-suey Chinese  | Switzerland  |
| Folk and f HB  | Sweden    |
| Rictor Supemarkt | Switzerland  |
+-----------------+-----------+
4 rows in set (0.00 sec)
```

# **EXPLANATION**

The SELECT returns all the customers who are from countries that start with Sw.

# **EXAMPLE B.16**

```
mysql> SELECT City, Country FROM Suppliers WHERE City LIKE ' %o ';
+----------+-----------+
| City     | Country   |
+----------+-----------+
| Tokyo    | Japan     |
| Oviedo   | Spain     |
| Sao Paulo | Brazil    |
| Salerno  | Italy     |
+----------+-----------+
4 rows in set (0.00 sec)
```

# **EXPLANATION**

The SELECT returns all cities and countries where the % matches any city that ends with a letter o.

# **EXAMPLE B.17**

```
mysql> SELECT CompanyName FROM customers WHERE CompanyName LIKE '%Super';
+---------------+
| CompanyName   |
+---------------+
| LiLa-Supermercado |
| Rictor Supemarkt  |
+---------------+
2 rows in set (0.00 sec)
```

# **EXPLANATION**

The SELECT returns all company names where the % matches any company name that contains the pattern Super.