# EXAMPLE B.28

```
mysql> USE northwind;
Database changed
mysql> DESCRIBE categories;
```

| Field | Type | Null | Key | Default | Extra |
| CategoryID | int(11) | | PRI | NULL | auto_increment |
| CategoryName | varchar(15) | | MUL | | |
| Description | longtext | YES | | NULL | |
| Picture | longblob | YES | | NULL | |

4 rows in set (0.09 sec)

# EXPLANATION

The *CategoryID* is the primary key, an integer of up to 11 digits, which will be incremented by 1, initially set to *NULL* (no value). The first time a record is inserted into the database, the value will be 1.

# EXAMPLE B.29

```
mysql> SELECT CategoryID, CategoryName FROM categories;
```

| CategoryID | CategoryName |
| 1 | Beverages |
| 2 | Condiments |
| 3 | Confections |
| 4 | Dairy Products |
| 5 | Grains/Cereals |
| 6 | Meat/Poultry |
| 7 | Produce |
| 8 | Seafood |

8 rows in set (0.16 sec)

# EXPLANATION

The primary key is called *CategoryID*. It is used to uniquely identify the different categories in this table from the *northwind* database. When a new category is added to the table, the *CategoryID* will be automatically incremented by 1.