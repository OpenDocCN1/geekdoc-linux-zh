because atomic transactions ensure that the original record isn’t deleted if the update portion of the atomic unit fails.

+   * **Consistency**—Ensures that no transaction can cause the database to be left in an inconsistent state. Inconsistent states can be caused by database client crashes, network failures, and similar situations. Consistency ensures that, in such a situation, any transaction or partially completed transaction that would cause the database to be left in an inconsistent state is *rolled back*, or undone. This prevents, for example, the deletion of one critical field of a database record when all other fields for that record remain (referred to as *orphaned* data). Incomplete transactions are rolled back to maintain consistency.

+   * **Isolation**—Ensures that multiple transactions operating on the same data are completely isolated from each other. This prevents data corruption if two users try to write to the same record at the same time. The way isolation is handled can generally be configured by the database programmer. One way that isolation can be handled is through locking, as discussed previously.

+   * **Durability**—Ensures that, after a transaction has been committed to the database, it cannot be lost in the event of a system crash, network failure, or other problem. This is usually accomplished through transaction logs. Durability means, for example, that if the server crashes, the database can examine the logs when it comes back up and it can commit any transactions that were not yet complete into the database.

PostgreSQL is ACID-compliant, but again MySQL gives you the choice of using ACID-compliant tables or not. MyISAM tables are not ACID-compliant, whereas InnoDB tables are. Note that ACID compliance is no easy task: All the extra precautions incur a performance overhead.

# SQL Subqueries

Subqueries allow you to combine several operations into one atomic unit, and they enable those operations to access each other’s data. By using SQL subqueries, you can perform some extremely complex operations on a database. In addition, using SQL subqueries eliminates the potential problem of data changing between two operations as a result of another user performing some operation on the same set of data. Both PostgreSQL and MySQL have support for subqueries in this release of Fedora, but this was not true in earlier releases. MySQL has only recently implemented the technology.

> **Importing Text Files into Tables**
> 
> In MySQL and PostgreSQL, the SQL statements used to create a database table can be entered directly into the command-line clients. However, doing so introduces a lot of opportunity for error; if you make a mistake, you have to type the entire table again from the beginning. Fortunately, both MySQL and PostgreSQL can read a list of SQL statements from a plain-text file. You could also enter SQL statements into a text editor and save the file with the filename