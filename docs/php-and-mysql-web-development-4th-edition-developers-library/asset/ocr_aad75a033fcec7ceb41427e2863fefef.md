The need to cooperate with the server arises in connection with several of the administrative tasks discussed in this chapter, from making backups to performing table repairs. Therefore, the next section begins by describing how to keep the server at bay when necessary, and sections following discuss how to prepare for problems, how to make backups, and how to use repair and recovery techniques if necessary.

Under Unix, operations that require you to directly work with table files or other files under the data directory should be performed while you’re logged in as the MySQL administrator so that you have permission to access the files. In this book, the name of that login account is mysql. It’s also possible to access the files as root, but that case, make sure when you’re done that any files you work with have the same mode and ownership as when you began.

For a full listing of the options supported by the SQL statements and programs discussed in this chapter, see Appendix E, “SQL Syntax Reference,” and Appendix F, “MySQL Program Reference.”

# 14.2 Performing Database Maintenance with the Server Running

Some maintenance operations are performed by connecting to the server and telling it what to do. To perform consistency checks or table repairs on a MyISAM table, one way to do so is to issue a CHECK TABLE or REPAIR TABLE statement (or invoke the mysqlcheck program) and let the server do the work. In this case, the server will access the .frm, .MYD, and .MYI files that represent the table. In general, this is the best approach to take if possible: When the server performs the requested maintenance operations, it handles any issues involved in coordinating access to the table so that you need not think about them.

Other maintenance operations are performed by a program external to the server, in which case, you *must* think about issues of table access coordination. For example, another way to check or repair a MyISAM table is to invoke the myisamchk utility, which opens the table files directly without going through the server. While myisamchk accesses the table files, it’s necessary to prevent the server from changing the table at the same time. If you don’t do that, the competing efforts to access the table can damage it and make it unusable. It’s obviously a bad thing for the server and myisamchk both to be writing to the table at the same time, but even having one of them reading while the other program is writing isn’t good, either. The program doing the reading can become confused if the table is being changed by the other program at the same time.

+   - Compressing a MyISAM table with myisampack.
+   - Relocating a MyISAM table’s data file or index file.
+   - Relocating a database.