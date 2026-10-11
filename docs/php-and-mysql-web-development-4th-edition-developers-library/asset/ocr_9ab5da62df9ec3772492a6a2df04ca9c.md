- **--log-error=***file_name***  
Writes warning and error messages to the end of the named file. This option was introduced in MySQL 5.0.42/5.1.18.

- **--master-data=[***value***]**  
This option helps make a backup that can be used to set up a a slave server. With this option, *mysqldump* sends a *SHOW MASTER STATUS* statement to the server to get its current binary log filename and position, and uses the results to write a *CHANGE MASTER* statement to the output that contains the same filename and position. The effect is that when you load the dump file into a slave server, it synchronizes the slave to the proper replication coordinates of the dumped server to begin replicating at the point when the dump was made. This option has no effect unless the server has binary logging enabled.

By default, the *CHANGE MASTER* statement is written in non-commented form. **--master-data** takes an optional value to explicitly control commenting of the statement. A value of 1 produces a non-commented statement, and a value of 2 produces a commented statement.

- **--master-data** requires the *RELOAD* privilege. This option automatically enables **--lock-all-tables** if **--single-transaction** is not given.

- **--no-autocommit*** (boolean)*  
Writes the *INSERT* statements for each table within a transaction. The resulting output can be loaded more efficiently than executing each statement in autocommit mode.

- **--no-create-db, -n*** (boolean)*  
Causes *CREATE DATABASE* statements not to be written. (Normally, these are added to the output automatically when **--databases** or **--all-databases** are used.)

- **--no-create-info, -t*** (boolean)*  
Causes *CREATE TABLE* statements not to be written. This is useful if you want to dump just table data.

- **--no-data, -d*** (boolean)*  
Causes table data not to be written. This is useful if you want to dump just the *CREATE TABLE* statements.

- **--no-tablespaces, -y*** (boolean)*  
Causes tablespaces not to be dumped. This option was introduced in MySQL 5.1.14.

- **--opt**  
Optimizes table dumping speed and writes a dump file that is optimal for reloading speed. This option turns on whichever of the following options are present in your