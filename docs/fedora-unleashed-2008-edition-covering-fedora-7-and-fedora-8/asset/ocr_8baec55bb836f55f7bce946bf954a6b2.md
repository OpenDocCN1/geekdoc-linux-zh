**NOTE**

MySQL's data locking methods are discussed in more depth at [http://www.mysql.com/doc/en/Internal_locking.html].

You can find more information on PostgreSQL's locking at [http://www.postgresql.org/docs/7.4/interactive/sql-lock.html].

# ## ACID Compliance in Transaction Processing to Protect Data Integrity

Another way MySQL and PostgreSQL differs is in the amount of protection they provide for keeping data from becoming corrupted. The acronym ACID is commonly used to describe several aspects of data protection:

+   * **Atomicity**—This means that several database operations are treated as an indivisible (atomic) unit, often called a *transaction*. In a transaction, either all unit operations are carried out or none of them are. In other words, if any operation in the atomic unit fails, the entire atomic unit is canceled.

+   * **Consistency**—Ensures that no transaction can cause the database to be left in an inconsistent state. Inconsistent states can be caused by database client crashes, network failures, and similar situations. Consistency ensures that, in such a situation, any transaction or partially completed transaction that would cause the database to be left in an inconsistent state is *rolled back*, or undone.

+   * **Isolation**—Ensures that multiple transactions operating on the same data are completely insulated from each other. This prevents data corruption if two users try to write to the same record at the same time. The way isolation is handled can generally be configured by the database programmer. One way that isolation can be handled is through locking, as discussed previously.

+   * **Durability**—Ensures that, after a transaction has been committed to the database, it cannot be lost in the event of a system crash, network failure, or other problem. This is usually accomplished through transaction logs. Durability means, for example, that if the server crashes, the database can examine the logs when it comes back up and it can commit any transactions that were not yet complete into the database.

PostgreSQL is ACID-compliant, but again MySQL gives you the choice of using ACID-compliant tables or not. MyISAM tables are not ACID-compliant, whereas InnoDB tables are. Note that ACID compliance is no easy task: All the extra precautions incur a performance overhead.

# ## SQL Subqueries

Subqueries enable you to combine several operations into one atomic unit, and they enable those operations to access each other's data. By using SQL subqueries, you can