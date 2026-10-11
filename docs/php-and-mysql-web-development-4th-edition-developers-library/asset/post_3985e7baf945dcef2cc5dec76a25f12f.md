
- Set up scheduled preventive maintenance to perform table checking periodically. Routine table-checking procedures can help you detect and correct minor problems before they become worse.

- Set up a database backup schedule. Should the worst occur and you be faced with catastrophic system failure, you'll need the backups to perform recovery operations. Enable your binary log, too, so that you have a record of updates that took place after the backup was made. (See Section 12.5.4, “The Binary Log and the Binary Log Index File.”) Binary logging provides significant advantages for backup and replication and has negligible performance overhead (about 1%), so there is little reason not to enable it.

If table damage or data loss does occur despite your efforts, exercise your options for dealing with such problems:

- Check your tables, and then fix any that are found to be corrupt if possible. Minor damage often can be corrected by using MySQL's table repair capabilities.

- For circumstances under which table checking and repair isn't sufficient to get you up and running, perform data recovery using your backups and your binary log. Begin by using the backups to restore your tables to their state at the time of the backup. After that, use the log files to re-apply any updates that were made after the backup, to bring your tables to their state when the crash occurred.

The tools at your disposal for carrying out these tasks include the capabilities of the MySQL server itself and also several other utilities included in the MySQL distribution:

- When the server starts, transactional storage engines can perform auto-recovery. You can also enable automatic table repair for the MyISAM storage engine. These capabilities are useful when the server restart follows a crash.

- Use the mysqldump or mysqlhotcopy program to make backups of your databases, should you need to recover them later.

- To tell the server to perform table maintenance operations on demand, use SQL statements such as CHECK TABLE and REPAIR TABLE. For a command-line interface to these statements, use the mysqlcheck program. The mysqlcheck utility also can check tables for problems and perform various corrective actions.

Some of these programs, such as mysqlcheck and mysqlchk, work in cooperation with the server. They connect as clients to the server and issue SQL statements that instruct the server what kind of table maintenance operation to perform. By contrast, mysqlchk is an independent standalone program that operates directly on the files used to represent tables. Because the server also accesses those files while it runs, mysqlchk acts in effect as a competitor to the server. This means that you must take steps to prevent mysqlchk and the server from interfering with each other. For example, if you're repairing a table with mysqlchk, it's necessary to keep the server from trying to write to the table at the same time. Failure to do so can result in much worse problems than those you're trying to correct!

The need to cooperate with the server arises in connection with several of the administrative tasks discussed in this chapter, from making backups to performing table repairs. Therefore, the next section begins by describing how to keep the server at bay when necessary, and sections following discuss how to prepare for problems, how to make backups, and how to use repair and recovery techniques if necessary.

Under Unix, operations that require you to directly work with table files or other files under the data directory should be performed while you’re logged in as the MySQL administrator so that you have permission to access the files. In this book, the name of that login account is mysql. It’s also possible to access the files as root, but in that case, make sure when you’re done that any files you work with have the same mode and ownership as when you began.

For a full listing of the options supported by the SQL statements and programs discussed in this chapter, see Appendix E, “SQL Syntax Reference,” and Appendix F, “MySQL Program Reference.”

## 14.2 Performing Database Maintenance with the Server Running

Some maintenance operations are performed by connecting to the server and telling it what to do. To perform consistency checks or table repairs on a MyISAM table, one way to do so is to issue a CHECK TABLE or REPAIR TABLE statement (or invoke the mysqlcheck program) and let the server do the work. In this case, the server will access the .frm, .MYD, and .MYI files that represent the table. In general, this is the best approach to take if possible: When the server performs the requested maintenance operations, it handles any issues involved in coordinating access to the table so that you need not think about them.

Other maintenance operations are performed by a program external to the server, in which case, you *must* think about issues of table access coordination. For example, another way to check or repair a MyISAM table is to invoke the myisamchk utility, which opens the table files directly without going through the server. While myisamchk accesses the table files, it’s necessary to prevent the server from changing the table at the same time. If you don’t do that, the competing efforts to access the table can damage it and make it unusable. It’s obviously a bad thing for the server and myisamchk both to be writing to the table at the same time, but even having one of them reading while the other program is writing isn’t good, either. The program doing the reading can become confused if the table is being changed by the other program at the same time.

- Compressing a MyISAM table with myisampack.
- Relocating a MyISAM table’s data file or index file.
- Relocating a database.
- Some backup techniques involve copying table files. To ensure consistent backup files, it's necessary to keep the server from changing the tables during the backup procedure.
- Some recovery methods are based on replacing damaged tables with good backup copies. While you are replacing the table, you must not allow the server to access it at all.

The most effective way to prevent the server from interfering with you is to shut it down. Clearly, if the server is not running, it can't access the tables you're working with. But administrators are understandably reluctant to take the server completely offline because that makes all databases and tables unavailable, not just those that you want to check or repair.

To avoid stopping the server while at the same time preventing problems of interaction between a running server and operations that you're performing externally to it, coordinate with the server by using a locking protocol. The server has two kinds of locking:

- The server uses internal locking to keep requests from different clients from getting mixed up with each other—for example, to keep one client's *SELECT* query from being interrupted by another client's *UPDATE* statement. But you can also exploit internal locking to prevent clients from accessing a table while you are working with the table externally to the server.
- The server can use external locking to prevent other programs from modifying table files while it's using them. This is based on the locking capabilities available for your operating system at the filesystem level. Normally, the reason the server uses external locking is for cooperation with programs like *myisamchk* during table checking operations. However, external locking doesn't work reliably on some systems. Another limitation is that external locking is useful only for operations that require read-only access to table files, such as table checking. External locking cannot be used for operations that require read/write access, such as table repair. External locking is based on file locking, but repair operations performed by *myisamchk* copy table files to new files as they work, and then use the new files to replace the originals. The server knows nothing of the new files, which renders useless any attempt at coordinating access by means of file locking.

The following discussion covers only the use of internal locking to coordinate with the server for table access. Because external locking is problematic, I discuss it no further.

### 14.2.1 Locking Individual Tables for Read-Only or Read/Write Access

To use the server's internal locking mechanism to prevent it from accessing a table while you work on it, the general idea is that you connect to the server with *mysql* and issue a *LOCK TABLE* statement for the table you want to use. Then, with *mysql* idle (that is, sitting there not doing anything with the table except keeping it locked), you do whatever you need to do with the table files. When you're done, switch back to your *mysql* session and release the lock to tell the server it's okay to use the table again.
