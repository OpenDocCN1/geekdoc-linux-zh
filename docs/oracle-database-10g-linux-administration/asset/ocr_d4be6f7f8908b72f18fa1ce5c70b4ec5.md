it cannot be undone without performing an additional operation to manually change the data back. The COMMIT operation makes sure that the entire transaction has completed successfully before the COMMIT statement returns success to the user. In order for this COMMIT operation to complete, several steps must occur.

+   1.  The unique System Change Number (SCN) for the transaction is written into the transaction table in the undo tablespace.
+   2.  The Log Writer (LGWR) writes out the redo log information and the SCN to the redo log file. Until this has actually been written out, the transaction cannot complete. This is why the performance of the redo log files and the LGWR is very important.
+   3.  Locks are released.
+   4.  The COMMIT statement returns a successful return code to the user process.

The COMMIT operation is very important both to the stability of the data, and to the performance of the system. In order to facilitate in transactions, the savepoint operation has been introduced.

# Savepoints

The savepoint allows you to save your work several times during a long and complex transaction. By creating several savepoints, you can roll back to a specific savepoint without having to roll back to the beginning of the transaction. This allows you to correct data problems in a long transaction without having to start over.

A transaction can be rolled back to any savepoint within the transaction; however, all SQL statements that have occurred since that savepoint will be rolled back as well. Take the following example:

+   1.  Transaction begins
+   2.  SQL
+   3.  Savepoint A
+   4.  SQL
+   5.  Savepoint B
+   6.  SQL
+   7.  Savepoint C
+   8.  SQL