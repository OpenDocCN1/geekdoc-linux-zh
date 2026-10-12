Typing each data item individually can be tedious. As an alternative, you can add your data to a plain-text file and load it into your MySQL database, as described in the following section.

# ### Loading data from a file

Using the LOAD DATA command during a mysql session, you can load a file containing database records into your MySQL database. Here are a few things you need to know about creating a data file to be loaded into MySQL.

+   - You can create the file using any Linux text editor.
+   - Each record, consisting of all of the columns in the table, must be on its own line. (A line feed indicates the start of the next record.)
+   - Separate each column by a Tab character.
+   - You can leave a column blank for a particular record by placing a \N in that column.
+   - Any blank lines you leave in the file result in blank lines in the database table.

In this example, the following text is added into a plain-text file. The text is in a format that can be loaded into the names table created earlier in this chapter. To try it out, type the following text into a file. Make sure that you insert a Tab character between each value.

```
Chris        Smith      175 Harrison Street     Gig Harbor      WA     98999
John          Jones      18 Talbot Road NW        Coventry        NJ     54889
Howard        Mantly     1515 Broadway             New York        NY     10028
```

When you are done entering the data, save the text to any filename that is accessible to the mysql server daemon (for example, /tmp/name.txt). Remember the filename so that you can use it later. If you are not already connected to a mysql session, type the following command (assuming mysql is the user name root):

```
$ mysql -u root -p
Enter password: ********
mysql>
```

Next, identify the database (allusers in this example) as the current database by typing the following:

```
mysql> USE allusers;
Database changed
```

To actually load the file into the names table in the allusers database, type the following command to load the file (in this case, /tmp/name.txt) from the mysql> prompt.

> > **NOTE:** Either enter the full path to the file or have it in the directory where the mysql command starts. In the latter case, you can type the filename without indicating its full path.

```
mysql> LOAD DATA INFILE "/tmp/name.txt" INTO TABLE names;
Query OK,  3 rows affected (0.02 sec)
Records:  3  Deleted:  0  Skipped:  0  Warnings:  0
```