```
constraInt fails (‘sampdb’, ‘absence’, CONSTRAINT 'absence_ibfk_1'
FOREIGN KEY ('student_id') REFERENCES student ('student_id'))
```

The error messages show that the constraints are working.

# 1.4.7.2  Adding New Rows from a File

Another method for loading rows into a table is to read them directly from a file. The file can contain INSERT statements or it can contain raw data. For example, the sampdb distribution contains a file named insert_president.sql that contains INSERT statements for adding new rows to the president table. Assuming that you are in the same directory where that file is located, you can execute those statements like this:

```
mysql sampdb < insert_president.sql
```

If you’re already running mysql, you can use a source command to read the file:

```
mysql> source insert_president.sql;
```

If you have the rows stored in a file as raw data values rather than as INSERT statements, you can load them with the LOAD DATA statement or with the mysqlimport client program.

The LOAD DATA statement acts as a bulk loader that reads data from a file. Use it from within mysql:

```
mysql> LOAD DATA LOCAL INFILE 'member.txt' INTO TABLE member;
```

Assuming that the member.txt file is located in your current directory on the client host, this statement reads it and sends its contents to the server to be loaded into the member table. (The member.txt file can be found in the sampdb distribution.)

By default, the LOAD DATA statement assumes that column values are separated by tabs and that lines end with newlines (also known as “linefeeds”). It also assumes that the values are present in the order that columns are stored in the table. It’s possible to read files in other formats or to specify a different column order. See the entry for LOAD DATA in Appendix E, “SQL Syntax Reference,” for details.

The keyword LOCAL in the LOAD DATA statement causes the data file to be read by the client program (in this case mysql) and sent to the server to be loaded. It is possible to omit LOCAL, but then the file must be located on the server host and you need the FILE server access privilege, which most MySQL users don’t have. You should also specify the full pathname to the file so that the server can find it.

If you get the following error with LOAD DATA LOCAL, the LOCAL capability might be disabled by default:

```
ERROR 1148 (42000): The used command was not allowed with this MySQL version
Try again after invoking mysql with the --local-infile option. For example:
mysql --local-infile sampdb
mysql> LOAD DATA LOCAL INFILE 'member.txt' INTO TABLE member;
```

If that doesn’t work, either, the server also needs to be told to allow LOCAL. See Chapter 12 for information on how to do this.