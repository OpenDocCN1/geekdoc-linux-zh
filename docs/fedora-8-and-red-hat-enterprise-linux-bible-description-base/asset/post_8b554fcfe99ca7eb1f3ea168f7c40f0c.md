
## Databases and Tables Overview

The databases shown here are named **information_schema**, **allusers**, **mysql**, and **test**. The **information_schema** database contains metadata about information in other databases on your server (such as the types of data, columns, or tables used in each). The **allusers** database is the one created in the previous step. The **mysql** database contains user access data. The **test** database is created automatically for creating test **mysql** databases.

### Working with the Current Database

1. To work with the database you just created (**allusers**), you need to make **allusers** your current database. To do that, type the following at the **mysql>** command prompt:

```sql
mysql> USE allusers;
Database changed
```

2. Creating a table for your database requires some planning and understanding of table syntax. You can type in the following commands and column information to try out creating a table. For more detailed information on creating tables and using different data types, refer to the section “Understanding MySQL Tables” later in this chapter.

To create a table called name, use the following **CREATE TABLE** command at the **mysql>** prompt:

```sql
mysql> CREATE TABLE name (
   ->  firstname     varchar(20)   not null,
   ->  lastname      varchar(20)   not null,
   ->  streetaddr    varchar(30)   not null,
   ->  city          varchar(20)   not null,
   ->  state         varchar(20)   not null,
   ->  zipcode       varchar(10)   not null
   ->  );
Query OK, 0 rows affected (0.00 sec)
```

You have now created a table called name for a database named allusers. It contains columns called **firstname**, **lastname**, **streetaddr**, **city**, **state**, and **zipcode**. Each column allows record lengths of between 10 and 30 characters. Although MySQL supports several different database formats, because none is specified here, the default MyISAM database type is used.

With a database and one table created, you can now add data to the table.

## Adding data to a MySQL database table

After the database is created and the structure of a database table is in place, you can begin working with the database. You can add data to your MySQL database by manually entering each record during a **mysql** session or by adding the data into a plain-text file and loading that file into the database.

**NOTE:** While you are in a *mysql* session, keep in mind that you can use the up arrow key to retrieve and change previous commands. This is particularly useful if you are manually entering database records that contain similar information.

### Manually entering data

To do the procedure in this section, I assume you have an open interactive *mysql* session and that you have created a database and table as described in the previous section. If you are not already connected to a *mysql* session, type the following command (assuming the *mysql* user name of root):

```bash
$ mysql -u root -p
Enter password: ********
mysql>
```

To add data to an existing MySQL database, the following procedure describes how to view the available tables and load data into those tables manually. The next section describes how to create a plain-text file containing database data and how to load that file into your database.

1. To make the database you want to use your current database (in this case, allusers), type the following command from the *mysql>* prompt:

```sql
mysql> USE allusers;
Database changed
```

2. To see the tables that are associated with the current database, type the following command from the *mysql>* prompt:

```sql
mysql> SHOW tables;
+-------------------+
| Tables_in_allusers |
+-------------------+
| name             |
+-------------------+
1 row in set (0.00 sec)
```

You can see that the only table defined so far for the allusers database is the one called name.

3. To display the format of the name table, type the following command at the *mysql>* prompt:

```sql
mysql> DESCRIBE name;
+------------+----------+------+-----+-------+-------+
| Field      | Type     | Null | Key | Default| Extra |
+------------+----------+------+-----+-------+-------+
| firstname  | varchar(20)| NO |     |       |       |
| lastname   | varchar(20)| NO |     |       |       |
| streetaddr | varchar(30)| NO |     |       |       |
| city       | varchar(20)| NO |     |       |       |
| state      | varchar(20)| NO |     |       |       |
| zipcode    | varchar(10)| NO |     |       |       |
+------------+----------+------+-----+-------+-------+
```

4. To add data to the new table, you can use the `INSERT INTO` command from the `mysql>` prompt. Here is an example of how to add a person’s name and address to the new table:

```sql
mysql> INSERT INTO name
    -> VALUES ('Jerry','Wingnut','167 E Street',
    -> 'Roy','UT','84103');
```

In this example, the `INSERT INTO` command identifies the *name* table. Then it indicates that values for a record in that table include the name Jerry Wingnut at the address 167 E Street, Roy, UT 84103.

5. To check that the data has been properly entered into the new table, type the following command from the `mysql>` prompt:

```sql
mysql> SELECT * FROM name;

+-----------+-----------+--------------+-------+--------+--------+
| firstname | lastname  | streetaddr   | city  | state  | zipcode|
+-----------+-----------+--------------+-------+--------+--------+
| Jerry     | Wingnut   | 167 E Street  | Roy   | UT     | 84103  |
+-----------+-----------+--------------+-------+--------+--------+
```

The resulting output shows the data you just entered, displayed in the columns you defined for the name table. If you like, you can continue adding data in this way.

Typing each data item individually can be tedious. As an alternative, you can add your data to a plain-text file and load it into your MySQL database, as described in the following section.

### Loading data from a file

Using the `LOAD DATA` command during a `mysql` session, you can load a file containing database records into your MySQL database. Here are a few things you need to know about creating a data file to be loaded into MySQL:

- You can create the file using any Linux text editor.
- Each record, consisting of all the columns in the table, must be on its own line. (A line feed indicates the start of the next record.)
- Separate each column by a Tab character.
- You can leave a column blank for a particular record by placing a `\N` in that column.
- Any blank lines you leave in the file result in blank lines in the database table.

In this example, the following text is added into a plain-text file. The text is in a format that can be loaded into the *name* table created earlier in this chapter. To try it out, type the following text into a file. Make sure that you insert a Tab character between each value.

```text
Chris Smith 175 Harrison Street Gig Harbor WA 98999
John Jones 18 Talbot Road NW Coventry NJ 54889
Howard Manty 1515 Broadway New York NY 10028
```

When you are done entering the data, save the text to any file name that is accessible to the mysql server daemon (for example, `/tmp/name.txt`). Remember the filename so that you can use it later. If you are not already connected to a `mysql` session, type the following command (assuming `mysql` is the user name root):

```bash
$ mysql -u root -p
Enter password: ********
mysql>
```

Next, identify the database (allusers in this example) as the current database by typing the following:

```sql
mysql> USE allusers;
Database changed
```

To actually load the file into the name table in the allusers database, type the following command to load the file (in this case, `/tmp/name.txt`) from the `mysql>` prompt.

> **NOTE:** Either enter the full path to the file or have it in the directory where the `mysql` command starts. In the latter case, you can type the filename without indicating its full path.

```sql
mysql> LOAD DATA INFILE "/tmp/name.txt" INTO TABLE name;
Query OK, 3 rows affected (0.02 sec)
Records: 3 Deleted: 0 Skipped: 0 Warnings: 0
```

Type the following at the `mysql>` prompt to make sure that the records have been added correctly:

```sql
mysql> SELECT * FROM name;
+----------+----------+-----------------+-----------+------+---------+
| firstname| lastname | streetaddr      | city      | state| zipcode |
+----------+----------+-----------------+-----------+------+---------+
| Chris    | Smith    | 175 Harrison Street|Gig Harbor| WA   | 98999  |
| John     | Jones    | 18 Talbot Road NW|Coventry  | NJ   | 54889  |
| Howard   | Manty    | 1515 Broadway   | New York  | NY   | 10028  |
+----------+----------+-----------------+-----------+------+---------+
```

At this point, you have a database that includes some data that you can begin working with. If something went wrong, refer to the “Updating and deleting MySQL records” section later in this chapter. If you find you need more information than is provided in this chapter, refer to the MySQL documentation at `http://dev.mysql.com/doc`.

Although MySQL doesn’t support all of SQL, it does contain enough features for most users. If you find that MySQL doesn’t meet your needs, you can try the PostgreSQL object-relational
