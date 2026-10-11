+   ▪ \*\_allowed\_packet
+   The maximum size of the buffer used for communication between the server and the client. The default value is 24MB and the maximum is 1GB.

+   ▪ \_buffer\_length
+   The initial size of the buffer used for communication between the server and the client. This buffer may be expanded up to \*\_allowed\_packet bytes long. The default value is slightly less than 1MB.

# F.16 mysqlhotcopy

The \_hotcopy performs efficient backups of databases and tables. It works only for MyISAM and ARCHIVE tables. \_hotcopy is a Perl script. It requires that you have DBI support installed (not surprising, given that it was originally written by Tim Bunce, one of the creators of DBI). \_hotcopy works on Unix and NetWare, but not Windows.

\_hotcopy connects to the server on the local host. It sends table flushing and locking statements to the server for each table to be copied, and then copies the table files to another location to make a backup. This ensures that outstanding table modifications have been flushed to disk and that the server won't try to further modify the table while it is being copied. (Essentially, \_hotcopy implements the protocol described in Section 14.1, “Performing Database Maintenance with the Server Running.” This protocol serves to tell the server to leave the designated tables alone while you're working directly with the table files.)

This program can be invoked in a number of ways. The general invocation syntax is as follows:

```
mysqlhotcopy [options] db_name[,/regex/] [new_db_name | dir_name]
```

For example, to make a copy of the database \_name named \_name\_copy under the data directory, use this command:

```
% mysqlhotcopy [options] db_name
```

To copy the \_name database to a directory named \_name under the /tmp directory instead, do this:

```
% mysqlhotcopy [options] db_name /tmp
```

More examples are provided in the online documentation, available with this command:

```
% perldoc mysqlhotcopy
```