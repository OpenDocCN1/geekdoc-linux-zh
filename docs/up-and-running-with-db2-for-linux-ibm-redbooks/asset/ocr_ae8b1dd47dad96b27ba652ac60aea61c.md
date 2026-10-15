# Administering databases

This chapter contains information regarding some important database maintenance tasks for DB2 UDB on Linux platforms, such as database backup and recovery, table and index reorganization, and data movement via utilities, such as export, import and load, and so on. These topics are discussed:

+   - Database backup and recovery
+   We discuss factors to consider when choosing database and table space recovery methods, including backing up and restoring a database or table space, and using rollforward recovery. We also discuss the utilities' basic usage, for example, BACKUP, RESTORE, ROLLFORWARD, and so on.

+   - Table and index reorganization and statistics collection
+   We discuss the REORG utility, which can be used to defragment the data pages occupied by tables and indexes, and the RUNSTATS utility for statistics collection, as well as the REBIND task to make the latest statistics information applicable to existing packages. We also discuss the different methods that can be used for table reorganization and index reorganization.

+   - Data movement via EXPORT, IMPORT and LOAD
+   We discuss the utilities that can be used to move data between tables or databases, or other desirable formats; for example, exporting data into the format of a spread program or operating system files with the format of ASC, DEL, or IXF, and so on. We also discuss the LOAD utility in this section, especially for the new online load feature which takes locks at the table level only now. These new load features significantly improve the availability of the