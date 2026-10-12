+   6. Issue the ALTER DATABASE DROP LOGFILE GROUP command.
+   7. Issue the ALTER DATABASE ADD LOGFILE GROUP command with the desired naming and storage for the initial log member in the group.
+   8. Add other redo log file members to the group as necessary.
+   9. Issue the ALTER DATABASE OPEN command.

# Archived Redo Log Recovery

Loss of an archived redo log file does not affect the current operation of the database, but it can impact the ability to do either full or incomplete (i.e., point-in-time) recovery.

If there is little or no likelihood of needing to perform point-in-time or incomplete recovery, the simplest method of resolving this situation is to perform an immediate full backup. This eliminates the need for the archived redo log files that were created prior to the full backup. This will also allow for full recovery to a time beyond the lost archived redo log from the full backup datafiles.

If there is a possible need to do point-in-time or incomplete recovery, and if a backup of the archived redo log exists on other media (e.g., as a tape backup), restore the lost archived redo log from tape to the archive destination. If no backup copy of the lost archived redo log exists, recovery will only be possible to the point in time of the last complete archived redo log prior to the one lost.

Oracle strongly recommends making a backup copy of the archived redo logs in order to prevent a single point of failure for recovery.

# How Transactions Work

Remember, the term transaction is used to describe a logical group of work. This group of work can consist of one or many SQL statements and must end with a commit or a rollback. Because this example assumes a client/server application, SQL*Net is necessary. The following steps are executed to complete the transaction:

+   The application processes the user input and creates a connection to the server via SQL*Net.

+   The server picks up the connection request and creates a server process on behalf of the user.

+   The user executes a SQL statement and commits the transaction. In this example, the user changes the value of a row in a table.

+   The server process takes this SQL statement and checks the shared pool to see whether there is a shared SQL area that has this identical SQL statement (assuming CURSOR_SHARING=EXACT). If it finds an identical shared SQL area, the server process checks to see whether the user has access privileges