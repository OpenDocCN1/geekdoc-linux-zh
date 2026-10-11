+   **13. D.** While Oracle does take out a share lock at the table level, an exclusive lock on the data being changed is only taken out at the row level.

+   **14. C.** The SELECT FOR UPDATE command takes out a table row share lock, preventing other users from performing DML on the selected rows.

+   **15. A.** An exclusive lock is the most restrictive type, allowing other users to perform only SELECT statements until the lock is released.

+   **16. B.** Performing DDL on a table requires that an exclusive lock be taken out on that table.

+   **17. A.** By querying **DBA_BLOCKERS** joined to **V$SESSION**, we can tell that Joe has obtained and is holding a lock on an object that another session is requesting. Joe is the blocker preventing the other session from obtaining the lock.

+   **18. B.** Free List contention can become a problem because many resources are trying to obtain information from the segment header as to which blocks are available to store newly inserted rows. The Free List in the segment header contains this information.

+   **19. D.** The values for **SID** and **SERIAL#** must be enclosed in single quotes and separated by commas when killing a session with the ALTER SYSTEM command.

+   **20. C.** The user whose session detects the deadlock and has their transaction rolled back will generate a trace file in the **USER_DUMP_DEST** location specified in `init.ora`.