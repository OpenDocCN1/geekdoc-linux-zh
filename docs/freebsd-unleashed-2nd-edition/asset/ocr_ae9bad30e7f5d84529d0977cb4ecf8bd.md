The additional clarity that this gives you will be invaluable when you find yourself writing really long, complex queries once you've become a SQL expert.

> **NOTE**
> 
> You must enter all these clauses in a specific order. `LIMIT` cannot appear before `ORDER BY`, for instance. The prototypes for all complete SQL commands are available in the online documentation for the various database applications.

That's about it for a basic extraction of data from a single table. You use a similar process to insert data into a table, though it's a little bit more mathematical in its look and feel. You begin with the `INSERT INTO` statement, followed by the table in question; then, in parentheses, you enter the names of the columns into which you're adding data (you can insert into only a few fields if you want to, leaving the rest in that row as `NULL`). You then enter the `VALUES` statement, followed (in parentheses) by the values you want to insert, listed in the same order as the fields were specified:

```
```
INSERT INTO Users (FullName,Email,Age) VALUES ("Sam
Jones","sjones@somewhere.com", "25");
```
```

Updating data in a row (or group of rows) uses syntax that borrows from both the `SELECT` and `INSERT` commands, as in these examples:

```
```
UPDATE Users SET Age="26" WHERE FullName="Sam Jones";
UPDATE Users SET FullName="Somebody Under 18" WHERE Age<"18";
UPDATE Users SET Age=Age+1;
```
```

> **CAUTION**
> 
> The third example shown here has no restrictions (WHERE clauses); therefore, it's a global update that applies to all records. *Be very careful* when using commands like this—they can wipe out your entire database.

Finally, to delete a row from a table, you use a syntax similar to what you've seen already:

```
```
DELETE FROM Users WHERE Age<"13";
DELETE FROM Users;
```
```

The second line in this example will delete all entries from the Users table. Use this command with the same caution with which you would use `rm -rf *`! If you ever find yourself entering a `DELETE` or `UPDATE` query that has no `WHERE` statements in it, double- and triple-check that you're doing what you want to be doing. You'll thank yourself for your caution.