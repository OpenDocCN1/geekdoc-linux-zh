2. With mysql sitting idle, switch to window B so that you can work directly with the table files. For example, you can repair a MyISAM table like this:
`% mysqlcheck --recover tbl_name`

This example is for illustration only. The particular commands you issue will depend on what maintenance operation you’re performing. (It might be prudent to make copies of the table files first, in case something goes wrong.)

3. When you’re done working with the table, switch back to the mysql session in window A, flush the table again, and release the table lock:
`mysql> FLUSH TABLE tbl_name;`
`mysql> UNLOCK TABLE;`

# 14.2.2 Locking All Databases for Read-Only Access

A convenient way to prevent clients from making any changes to any table is to place a read lock on all tables in all databases at once. To do this, issue the following statements:
`mysql> FLUSH TABLES WITH READ LOCK;`
`mysql> SET GLOBAL read_only = ON;`

The FLUSH statement acquires a global read lock, and the SET statement blocks until all other clients release any table locks they have and finish any outstanding transactions. When the statement returns, other clients can read but not change tables.

To allow changes to be made once again, use these statements:
`mysql> SET GLOBAL read_only = OFF;`
`mysql> UNLOCK TABLES;`

While the tables are locked this way, other clients can read from them but cannot make changes. This is a good way to make the server quiescent for operations such as making copies of all your database directories. On the other hand, it’s unfriendly to all clients that need to make updates, so you should hold the server lock no longer than necessary. It is also insufficient for operations such as making a binary backup of all tables managed by a transactional storage engine because the engine might have outstanding transactions pending and only partly flushed to its log files. Operations like that require that you stop the server to make sure everything is flushed and all files are closed.

# 14.3 General Preventative Maintenance

This section outlines some general strategies to help you maintain the integrity of your databases:

+   - Enable the auto-recovery capabilities that the MySQL server provides.
+   - Schedule regular preventative maintenance to check your tables.