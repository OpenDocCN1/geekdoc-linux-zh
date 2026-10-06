# Views

The join example above is a pretty useful query for our tables, but due to its complexity it's best executed from a file rather than an ad hoc query. SQL addresses this issue by providing a feature that allows a complex query to be stored in the database and used to produce a virtual table that can be used with simple query commands. In the following example we will create a view using our INNER JOIN query to create a virtual table Stats that we can use as the target of subsequent queries.

```
-- view_demo.sql

DROP VIEW IF EXISTS Stats;
CREATE VIEW Stats
AS
SELECT Package_Descriptions.package_name AS Package,
description AS Description,
count Files,
tot_size AS Size
FROM Package_Descriptions
INNER JOIN Stats
ON Package_Descriptions.package_name =
Package_Stats.package_name
ORDER BY Package;
```

Once we create it, we can treat Stats as just another table in our database even though it does not really exist.

| Description | Files | Size |
|---|---|---|
| 'Anything to PostScript' query and manage user i | 299 | 3455890 |
| Access control list utilities | 19 | 261704 |
| scripts for handling many ACPI event | 11 | 91106 |
| Advanced configuration and Power In | 18 | 86126 |
| admin release notes | 81 | 246658 |
| Adium message style for Ubuntu | 137 | 126759 |
| default icon of GNOME (small | 1127 | 484868 |
| GNOME solitaire card game collectio | 316 | 1890864 |
| ALSA driver configuration files | 42 | 195295 |

To delete a view we use the DROP VIEW statement as follows:

```
sqlite> DROP VIEW Stats;
```

# Indexes

It's been said that the most important features of a database system are "performance, performance, and performance." While this is not exactly true (things like data integrity and reliability are important), complex operations on large databases can get really slow, so it's important to make things as fast as we can. One feature we can take advantage of is indexes.

# SQL