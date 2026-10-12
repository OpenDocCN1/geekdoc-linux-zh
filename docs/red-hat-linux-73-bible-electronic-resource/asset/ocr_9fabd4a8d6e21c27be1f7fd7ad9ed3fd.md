# Loading data from a file

Using the LOAD DATA command during a mysql session, you can load a file containing database records into your MySQL database. Here are a few things you need to know about creating a data file to be loaded into MySQL.

+   • You can create the file using any Linux text editor.

+   • Each record, consisting of all the columns in the table, must be on its own line. (A line feed indicates the start of the next record.)

+   • Separate each column by a Tab character.

+   • You can leave a column blank for a particular record by placing a \N in that column for the record.

+   • Any blank lines you leave in the file result in blank lines in the database table.

In this example, the text shown below is added into a plain-text file. The text is in a format that can be loaded into the "names" table created earlier in this chapter. To try it out, type the following text into a file. Make sure that you insert a Tab character between each value (indicated here as multiple spaces).

| Chris Smith | 175 Harrison Street | Gig Harbor | WA | 98999 | | John Jones | 18 Talbot Road NW | Coventry | NJ | 54889 | | Howard Manty | 1515 Broadway | New York | NY | 10028 |

When you are done entering the data, save the text to any accessible filename (for example, `/tmp/mysql_names.txt`). Remember the filename so that you can enter it later. If you are not already connected to a mysql session, type the following command (assuming the mysql user name of root):

```
```sql
# mysql -u root -p
Enter password: ******
mysql>```
```

Next, identify the database (allusers in this example) as the current database by typing the following:

```
```sql
mysql> USE allusers;
Database changed```
```

To actually load the file into the names table in the allusers database, type the following command to load the file (in this case, `/tmp/mysql_names.txt`) from the `mysql>` prompt.

> **NOTE:** Either enter the full path to the file or have it in the directory where the mysql command starts. In the latter case, you can type the filename without indicating its full path.

```
```sql
mysql> LOAD DATA INFILE "/tmp/mysql_names.txt" INTO TABLE names;
Query OK, 3 rows affected (0.02 sec)
Records: 3 Deleted: 0 Skipped: 0 Warnings: 0```
```