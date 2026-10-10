If a table contains fixed data, you can also include other SQL statements (such as INSERT INTO) to load the data into the table right after the table is created.

To execute the SQL statements in the *makedb.sql* file in order to create the *books* table, I run *mysql* as follows:

```
mysql books < makedb.sql
```

Now the *books* database has a table named *books*. (Okay, maybe I should have named them differently, but it seemed convenient to call them by the same name.) I can now begin loading data into the table.

# **Loading data into a table**

One way to load data into the table is to prepare SQL statements in another file and run *mysql* with that file as input. For example, suppose I want to add the following book information into the *books* table:

```
isbn = '0764596152' 
title = 'SUSE Linux 9.3 For Dummies' 
author1 = 'Naba Barkakati' 
author2 = NULL 
publisher = 'Wiley' 
pubyear = 2005 
pagecount = 384
```

Then, the following MySQL statement loads this information into the *books* table:

```
INSERT INTO books VALUES
( '0764596152', 'SUSE Linux 9.3 For Dummies',
'Naba Barkakati', NULL, 'Wiley', 2005, 384) \G
```

On the other hand, suppose you had the various fields available in a different order — an order from one you can define by using the CREATE TABLE statement. In that case, you can use a different form of the INSERT INTO command to add the row in the correct order, as shown in the following example:

```
INSERT INTO books (pubyear, author1, author2, title, pagecount, publisher, isbn) values
(2005, 'Naba Barkakati', NULL, 'SUSE Linux 9.3 For Dummies', 384, 'Wiley', '0764596152')\G
```

Essentially, you have to specify the list of attributes as well as the values and make sure that the order of the attributes matches that of the values.