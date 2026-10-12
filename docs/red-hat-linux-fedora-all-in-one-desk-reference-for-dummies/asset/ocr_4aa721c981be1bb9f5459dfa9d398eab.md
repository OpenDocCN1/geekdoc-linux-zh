Then, the following MySQL statement loads this information into the books table:

```
INSERT INTO books VALUES
('156884798X', 'Linux SECRETS', 'Naba Barkakati', NULL,
'IDG Books Worldwide', 1996, 900) \g
```

On the other hand, suppose you have the various fields available in a different order (from the order in which the table's attributes are defined by the CREATE TABLE statement). In that case, you can use a different form of the INSERT INTO command to add the row, as shown in the following example:

```
INSERT INTO books (pubyear, author1, author2, title,
pagecount, pubname, isbn) values
(1996, 'Naba Barkakati', NULL, 'Linux SECRETS', 900, 'IDG
Books Worldwide', '156884798X')\g
```

Essentially, you have to specify the list of attributes as well as the values and make sure that the order of the attributes matches that of the values.

If I save all INSERT INTO commands in a file named additems.sql, then I can load the database from the mysql command line by using the source command like this (type mysql books to start the SQL client):

```
mysql> source additems.sql
```

# Querying the database

You can query the database interactively through the mysql monitor. (Of course, you do have to know SQL to do this operation.) For example, to query the books database, I start the SQL client with the following command:

```
mysql books
```

Then I would type SQL commands at the mysql> prompt to look up items from the database. When done, I type quit to exit the mysql program. Here's an example (all of which I typed in a terminal window):

```
mysql> select title from books where pubyear < 2000 \g
+--------------------------------+
| title                          |
+--------------------------------+
| Linux SECRETS                  |
| Red Hat Linux SECRETS, 2nd Edition |
+--------------------------------+
2 rows in set (0.00 sec)
mysql> quit
Bye
```