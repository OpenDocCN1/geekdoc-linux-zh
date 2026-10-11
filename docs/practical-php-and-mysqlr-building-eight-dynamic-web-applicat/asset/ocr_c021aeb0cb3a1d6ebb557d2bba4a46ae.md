```
```php
<?php
}
require("footer.php");
?>
```
```

Figure 5-11 shows the completed page for adding a forum.

![](bbox=[0.16, 0.3, 0.9, 0.64])

# FIGURE 5-11 Adding a forum

# ## Deleting

Deleting content from tables that are related can often be quite a challenge if the relationships are not enforced by the database. When you delete a category, you really want all dependent content, such as the forums and messages, to be deleted also. When referential integrity is not enforced, a series of SQL statements are needed to delete all dependent content.

At the start of the project, you used the InnoDB table type when creating your tables. With this type of table, you can enforce referential integrity, but it is not currently switched on.

To turn on referential integrity, specify the relationships between the tables in SQL. In this project, the intention is to allow all dependent records in other tables to be deleted. This is called a *cascading delete*. Before writing the SQL to do this, take a moment to understand how these relationships are defined: