# **2.6.2.7 Using FEDERATED Tables**

The FEDERATED storage engine enables you to access tables from one MySQL server that actually are managed by another server.

Suppose that there is no *sampdb* database on your local server, but there is one available from the MySQL server running on the host *corn.snake.net* and that you have an account for accessing that server. That account can be used by the local server through the FEDERATED storage engine to make the *sampdb* tables available on the local server. For each table that you want to access this way, create a FEDERATED table that has the same columns as the remote table, but include a connection string that indicates to the local server how to connect to the remote server.

Suppose that the *student* table on the remote server has this definition:

```
CREATE TABLE student
(
  name        VARCHAR(20) NOT NULL,
  sex         ENUM('F','M') NOT NULL,
  student_id  INT UNSIGNED NOT NULL AUTO_INCREMENT,
  PRIMARY KEY (student_id)
) ENGINE = InnoDB;
```

To create a FEDERATED table on the local server, use the same definition, except that the *ENGINE* option should be FEDERATED and a CONNECTION table option should be given that provides connection information. (Prior to MySQL 5.0.13, use the COMMENT option instead of CONNECTION.) The following definition creates a table named *federated_student* that accesses the *student* table on *corn.snake.net*:

```
CREATE TABLE federated_student
(
  name        VARCHAR(20) NOT NULL,
  sex         ENUM('F','M') NOT NULL,
  student_id  INT UNSIGNED NOT NULL AUTO_INCREMENT,
  PRIMARY KEY (student_id)
) ENGINE = FEDERATED
CONNECTION = 'mysql://sampadm:secret@corn.snake.net/sampdb/student';
```

The connection string in the CONNECTION value indicates that the username and password of the MySQL account on the remote server are *sampadm* and *secret*. The general connection string syntax is as follows, where square brackets indicate optional information:

```
mysql://user_name[:password]@host_name[:port_num]/db_name/[tbl_name]
```

After you create the *federated_student* table, you can select from it to access the remote *student* table. You can also INSERT, UPDATE, and DELETE with *federated_student* to modify the contents of the *student* table.

Note that the entire CONNECTION string (including the username and password) is visible to anyone who can use SHOW CREATE TABLE or similar statements for the FEDERATED table. As of MySQL 5.1.15, you can avoid this problem: Create a stored server definition using the CREATE SERVER statement (this requires the SUPER privilege) and refer