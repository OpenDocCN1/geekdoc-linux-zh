
INSERT INTO User_Prefs (User_ID, Prefs_ID, Last_mod)
VALUES ('5', '3', '1030745048');

Then, when the user views his page, your code can query the database for the most recent entry in User_Prefs for this user, find the Prefs_ID, and query for the attributes of that Prefs entry in order to generate the page according to those attributes. Here is an example of those queries:

```sql
SELECT Prefs_ID FROM User_Prefs
WHERE User_ID='5'
ORDER BY Last_mod DESC LIMIT 1;
```

```sql
. . . [ Extract the value of Prefs_ID into $Prefs_id, as we will see later ]
```

```sql
SELECT Background_color, Text_color, Show_email FROM Prefs
WHERE Prefs_ID="$Prefs_id";
```

Alternatively, if you're even more adventurous, you can combine these into a single query with a join:

```sql
SELECT Background_color, Text_color, Show_email FROM User_Prefs, Prefs
WHERE User_Prefs.User_ID='5'
AND User_Prefs.Prefs_ID=Prefs.ID
ORDER BY Last_mod DESC LIMIT 1;
```

You can even do a three-way join to get all of a user's information out of the Users table as well as his latest entry in Prefs, as shown here:

```sql
SELECT Fullname, Email, Age, Background_color, Text_color, Show_email
FROM User_Prefs, Users, Prefs
WHERE Users.ID='5'
AND User_Prefs.User_ID=Users.ID
AND User_Prefs.Prefs_ID=Prefs.ID
ORDER BY Last_mod DESC LIMIT 1;
```

Planning out the structure of your tables in this way, before you even begin creating them, will save you a lot of heartache later on when you might otherwise have had to redesign everything from inside a running system.

## Creating Tables

Now that you have a working design in mind for your database, you can begin creating tables. This is done with the CREATE TABLE query command. The syntax for this command is fairly simple, but it does require the knowledge of what kinds of data types are available. The most common of these are shown in Table 28.1, although more types are available as well and are fully documented at the MySQL and PostgreSQL Web sites.

### TABLE 28.1 Commonly Used Column Data Types

| Type Name | Description |
| :--- | :--- |
| INT, INTEGER | A “signed” integer from −2147483648 to 2147483647. This type can have the **UNSIGNED** attribute. |
| FLOAT | A floating-point number. |
| CHAR(n) | A string of n reserved bytes, up to n=255. |
| VARCHAR(n) | Like CHAR, except only as much space as is required to store the string is consumed. This type is preferable to CHAR. You can specify **BINARY** to make string comparisons case sensitive. |
| BLOB | A binary large object, holding text or binary data (such as images), with variable storage (like VARCHAR). The maximum size is 65KB. There are also **TINYBLOB** (256 bytes), **MEDIUMBLOB** (16.7MB), and **LONGBLOB** (4.3GB). |
| TEXT | Same as BLOB, except that string comparisons are case insensitive. There are also **TINYTEXT**, **MEDIUMTEXT**, and **LONGTEXT**. |
| ENUM | A set of permissible strings (for example, "Red", "Green", "Yellow"). |
| BOOLEAN | "True" or "False". Not supported by MySQL |

Let’s create the tables discussed already in the PictureArchive example. The Users table needs to have an integer ID field, text strings for the FullName and Email fields, and another integer for Age. The following code creates that table:

```sql
CREATE TABLE Users (ID INT, FullName VARCHAR(64), Email VARCHAR(32), Age INT);
```

The Prefs table will have an integer ID, six-character text fields for the two color fields (which you will populate with hex values), and an ENUM for Show_email (because MySQL doesn’t have BOOLEAN). This code creates that table:

```sql
CREATE TABLE Prefs
(ID INT, Background_color VARCHAR(6),
Text_color VARCHAR(6), Show_email ENUM("Y","N"));
```

After entering the CREATE TABLE commands, issue a **DESCRIBE Users** command to view your handiwork, as shown here:

```
mysql> DESCRIBE Users;
+-------+--------------+------+-----+-------+---+
| Field | Type         | Null | Key | Default |   |
+-------+--------------+------+-----+-------+---+
| ID    | int(11)      | YES  |     | NULL    |   |
| FullName | varchar(64) | YES  |     | NULL    |   |
| Email | varchar(32)  | YES  |     | NULL    |   |
| Age   | int(11)      | YES  |     | NULL    |   |
+-------+--------------+------+-----+-------+---+
4 rows in set (0.00 sec)
```

After some data has been entered into a table, the output from any queries you make at the command line will be returned in a tabular format, along with the time it took to process the query. If the columns are too wide for your screen, they will wrap rather than truncate; this can lead to a confused-looking display. Being selective in which fields you query for will help keep the output readable.

The following example shows a couple multiline INSERT queries that populate the Users table, followed by the tabular output from a judiciously restricted SELECT query:

```
mysql> INSERT INTO Users (ID,FullName,Email,Age)
   -> VALUES (1,"Joe Smith","jsmith@somewhere.com",22);
mysql> INSERT INTO Users (ID,FullName,Email,Age)
   -> VALUES (2,"Alice Walker","awalker@elsewhere.com",31);
mysql> SELECT ID,FullName,Email,Age FROM Users;
+----+----------+-----------------------+----+
| ID | FullName | Email                 | Age |
+----+----------+-----------------------+----+
|  1 | Joe Smith  | jsmith@somewhere.com | 22 |
|  2 | Alice Walker | awalker@elsewhere.com | 31 |
+----+----------+-----------------------+----+
2 rows in set (0.00 sec)
```

## Indexes and Keys

You now have working tables that can be used in active queries. Setting up a complete database is not quite that simple, however. One other thing to consider when designing your tables is how they will be indexed. Indexing determines the ordering of data within a database and is what allows databases to be as fast as they are. Think about looking up a word in the dictionary; if you were looking for the word sleep, but you didn’t know what “alphabetical order” was, you could literally spend weeks searching linearly through the dictionary until you found it. But because you know where the letter S is in the alphabet, you know how to zero in directly on the word and find it very rapidly.

Computers are the same way. If they have no indexing scheme for which to look up a piece of data, they can only search linearly through the data store for it—although they can do it faster than we can, it’s still an unacceptably slow solution in most high-performance database contexts. Therefore, we have to create appropriate indexes (which for computers are similar to our concept of alphabetical order) and keys (such as the first letter of sleep) to help the database find its way through the data.

All tables of entity data (those that would be depicted with rectangles in an E-R diagram) should have a primary key. This is a column specifically designated to be the value upon which the data in the table should be automatically indexed. Values in this column should be specified as NOT NULL (in other words, they can’t have a NULL value—a blank input value will become 0 for numeric data types and an empty string for text types). All values in the primary key column must also be unique.

This sounds like a role tailor-made for the integer ID columns in our tables. Indeed, the best practices in creating tables often call for the first column in every table to be a numeric ID that's the primary key and that also has the AUTO_INCREMENT attribute specified. This makes the column behave in a special way: If you insert rows into a table with an AUTO_INCREMENT column (which must also be a primary key), you can simply leave the value for that column blank or NULL, and the database will automatically fill in the next unused integer (the highest number in the column plus one) for each new row. This is perfect for the purposes of this chapter: You'll get a new unique ID number for each entry you put into your tables, and you don't even have to calculate it yourself.

Normally, you would specify these attributes at table-creation time:

```sql
CREATE TABLE Users (ID INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
  Fullname VARCHAR(64), Email VARCHAR(32), Age INT);
```

However, because in this case your tables are already created, you can use the ALTER TABLE command to change the ID column to your taste:

```sql
ALTER TABLE Users CHANGE ID ID INT NOT NULL PRIMARY KEY AUTO_INCREMENT;
```

### NOTE

PostgreSQL does not have AUTO_INCREMENT; instead, it has a special data type called SERIAL. The SERIAL data type is not subject to the same keying restrictions as AUTO_INCREMENT, but it acts much the same. Use SERIAL instead of INT to create an autoincrementing ID field.

Note that in PostgreSQL, if you specify NULL (instead of 0) for the ID field in an INSERT operation, NULL will be entered instead of the next available integer, which you would get if you simply didn't provide a value for that field. NULL trumps the SERIAL property in PostgreSQL. MySQL's AUTO_INCREMENT, by contrast, is invoked on any NULL or 0 entry into such a field.

You can specify other keys on other columns in the table by using the KEY attribute after the variable name at table-creation time or by using the ALTER TABLE command. Issuing this command creates an index on each key you specify. You can also create indexes based on multiple columns. This approach is useful when the unique combination of two columns taken together is what's usefully unique in a table. You can create indexes based on multiple columns like so:

```sql
ALTER TABLE Users ADD INDEX (Email,FullName);
```

This code will result in a MUL tag (for "multiple," meaning that the table has multiple indexes) appearing in the Key column of the output of *describe* *Users*.

It's very important to try to anticipate which tables will be accessed a lot and which will have a large amount of data. Indexing these tables properly, with the keys being the columns on which those tables will most frequently be searched, can cause unbelievably dramatic improvements in performance.
