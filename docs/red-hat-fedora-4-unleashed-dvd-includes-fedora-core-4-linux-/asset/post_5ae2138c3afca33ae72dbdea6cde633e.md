
## Choosing a Database: MySQL Versus PostgreSQL

In PostgreSQL, the string concatenation function is simply a double pipe (`||`). The following command is the PostgreSQL equivalent of the preceding MySQL command:

```sql
SELECT (genus || ' ' || species || ' ') AS TitleYear FROM cd_collection;
```

Note that the parentheses are optional, but they make the statement easier to read. Once again, the strings in the middle and at the end (note the space between the quotes) are used to insert spacing and parentheses between the title and year.

Of course, more often than not, you do not want a list of every single row in the database. Rather, you only want to find rows that match certain characteristics. For this, you add the WHERE statement to the SELECT statement. For example, suppose you want to find all the CDs in the cd_collection table that have a rating of 5. You would use a statement like the following:

```sql
SELECT * FROM cd_collection WHERE rating = 5;
```

Using the table from Figure 20.2, you can see that this query would return the rows for Trouser Jazz, Life for Rent, and The Two Towers. This is a simple query, and SQL is capable of handling queries much more complex than this. Complex queries can be written using logical AND and logical OR statements. For example, suppose you want to refine the query so it lists only those CDs that were not released in 2003. You would use a query like the following:

```sql
SELECT * FROM cd_collection WHERE rating = 5 AND year != 2003;
```

In SQL, `!=` means "is not equal to." So once again looking at the table from Figure 20.2, you can see that this query returns the rows for Trouser Jazz and The Two Towers but doesn't return the row for Life for Rent because it was released in 2003.

So, what if you want to list all the CDs that have a rating of 3 or 4 except those released in the year 2000? This time, you combine logical AND and logical OR statements:

```sql
SELECT * FROM cd_collection WHERE rating = 3 OR rating = 4 AND year != 2000;
```

This query would return entries for Mind Bomb, Natural Elements, and Combat Rock. However, it wouldn't return entries for Adiemus 4 because it was released in 2000.

# **TIP**

One of the most common errors among new database programmers is confusing logical AND and logical OR. For example, in everyday speech, you might say "Find me all CDs released in 2003 and 2004." At first glance, you might think that if you fed this statement to the database in SQL format, it would return the rows for For All You've Done and Life for Rent. In fact, it would return no rows at all. This is because the database interprets the statement as "Find all rows in which the CD were released in 2003 and was released in 2004." It is, of course, impossible for the same CD to be released twice, so this statement would never return any rows, no matter how many CDs were stored in the table. The correct way to form this statement is with an OR statement instead of an AND statement.

SQL is capable of far more than is demonstrated here. But as mentioned before, this section is not intended to teach you all there is to know about SQL programming; rather, it teaches you the basics so you can be a more effective DBA.

If you are just starting out and learning about using a database with Linux, the first logical step is to research which database will best serve your needs. Many database software packages are available for Linux; some are free, and others cost hundreds of thousands of dollars. Expensive commercial databases, such as Oracle, are beyond the scope of this book. Instead, this chapter focuses on two freely available databases: MySQL and PostgreSQL.

Both of these high-quality databases are included on this book's CD-ROMs and DVD. But just because MySQL and PostgreSQL are free does not mean they lack power. Both of these databases (PostgreSQL in particular) can handle very complex projects. They are used in commercial organizations (like Yahoo!), government agencies (such as NASA), research institutions, and educational institutions.

Both of these databases are quite capable, and either one could probably serve your needs. However, each database has a unique set of features and capabilities that might serve your needs better or make developing database applications easier for you. The following sections look at some of the key features of any database and discuss how those features are implemented in MySQL and PostgreSQL. You should use the information in these sections to compare the two databases so you can choose the one that's right for your project.

### Speed

Until recently, the speed choice was simple: If the speed of performing queries was paramount to your application, you used MySQL. MySQL has a reputation for being an extremely fast database. Until recently, PostgreSQL was quite slow by comparison.

Newer versions of PostgreSQL have improved in terms of speed (when it comes to disk access, sorting, and so on). In certain situations, such as periods of heavy simultaneous access, PostgreSQL can be significantly faster than MySQL, as you will see in the next section. However, MySQL is still extremely fast when compared to many other databases.

### Data Locking

To prevent data corruption, a database needs to put a lock on data while it is being accessed. As long as the lock is on, no other process can access the data until the first process has released the lock. This means that any other processes trying to access the data have to wait until the current process completes. The next process in line then locks the data until it is finished, and the remaining processes have to wait their turn, and so on. Of course, operations on a database generally complete quickly, so in environments with a small number of users simultaneously accessing the database, the locks are usually of such short duration that they do not cause any significant delays. However, in environments in which many people are accessing the database simultaneously, locking can create performance problems as people wait their turn to access the database.

MySQL uses a data-locking method that is fundamentally different from the data-locking method used by PostgreSQL.

Older versions of MySQL lock data at the table level, which can be considered a bottleneck for updates during periods of heavy access. This means that when someone writes a row of data in the table, the entire table is locked so no one else can enter data. If your table has 500,000 rows (or records) in it, all 500,000 rows are locked any time 1 row is accessed. Once again, in environments with a relatively small number of simultaneous users, this doesn't cause serious performance problems because most operations complete so quickly that the lock time is extremely short. However, in environments in which many people are accessing the data simultaneously, MySQL's table-level locking can be a significant performance bottleneck.

PostgreSQL, on the other hand, locks data at the row level. In PostgreSQL, only the row currently being accessed is locked. The rest of the table can be accessed by other users. This row-level locking significantly reduces the performance impact of locking in environments that have a large number of simultaneous users. Therefore, as a general rule, PostgreSQL is better suited for high-load environments than MySQL.

The MySQL release bundled with Fedora Core gives you the choice of using tables with table-level or row-level locking. In MySQL terminology, MyISAM tables use table-level locking and InnoDB tables use row-level locking.

> **NOTE**
>
> MySQL's data locking methods are discussed in more depth at http://www.mysql.com/doc/en/Internal_locking.html.
>
> You can find more information on PostgreSQL's locking at http://www.postgresql.org/docs/index.php?locking-tables.html.

### ACID Compliance in Transaction Processing to Protect Data Integrity

Another way MySQL and PostgreSQL differ is in the amount of protection they provide for keeping data from becoming corrupted. The acronym ACID is commonly used to describe several aspects of data protection:

- **Atomicity** - A term derived from the word atom, which, as you might know, means "indivisible." In the database world, this means that several database operations are treated as an atomic unit, often called a transaction. In a transaction, either all unit operations are carried out or none of them are. In other words, if any operation in the atomic unit fails, the entire atomic unit is canceled.

If you have a power failure or server crash after an original record has been deleted, for example, but before the updated one has been added, you don't lose the record
