+   • Set up scheduled preventive maintenance to perform table checking periodically. Routine table-checking procedures can help you detect and correct minor problems before they become worse.

+   • Set up a database backup schedule. Should the worst occur and you be faced with catastrophic system failure, you'll need the backups to perform recovery operations. Enable your binary log, too, so that you have a record of updates that took place after the backup was made. (See Section 12.5.4, “The Binary Log and the Binary Log Index File.”) Binary logging provides significant advantages for backup and replication and has negligible performance overhead (about 1%), so there is little reason not to enable it.

If table damage or data loss does occur despite your efforts, exercise your options for dealing with such problems:

+   • Check your tables, and then fix any that are found to be corrupt if possible. Minor damage often can be corrected by using MySQL's table repair capabilities.

+   • For circumstances under which table checking and repair isn't sufficient to get you up and running, perform data recovery using your backups and your binary log. Begin by using the backups to restore your tables to their state at the time of the backup. After that, use the log files to re-apply any updates that were made after the backup, to bring your tables to their state when the crash occurred.

The tools at your disposal for carrying out these tasks include the capabilities of the MySQL server itself and also several other utilities included in the MySQL distribution:

+   • When the server starts, transactional storage engines can perform auto-recovery. You can also enable automatic table repair for the MyISAM storage engine. These capabilities are useful when the server restart follows a crash.

+   • Use the mysqldump or mysqlhotcopy program to make backups of your databases, should you need to recover them later.

+   • To tell the server to perform table maintenance operations on demand, use SQL statements such as CHECK TABLE and REPAIR TABLE. For a command-line interface to these statements, use the mysqlcheck program. The mysqlcheck utility also can check tables for problems and perform various corrective actions.

Some of these programs, such as mysqlcheck and mysqlndq, work in cooperation with the server. They connect as clients to the server and issue SQL statements that instruct the server what kind of table maintenance operation to perform. By contrast, mysqlchk is an independent standalone program that operates directly on the files used to represent tables. Because the server also accesses those files while it runs, mysqlchk acts in effect as a competitor to the server. This means that you must take steps to prevent mysqlchk and the server from interfering with each other. For example, if you're repairing a table with mysqlchk, it's necessary to keep the server from trying to write to the table at the same time. Failure to do so can result in much worse problems than those you're trying to correct!