DML Locks DML or data locks are denoted by TM and are used to lock tables when users are performing INSERT, UPDATE, and DELETE commands. Data locks can either be at the table level or row level. Every user who performs DML on a table actually gets two locks on the table: a share lock at the table level and an exclusive lock at the row level. These two locks are implicit, meaning that Oracle performs the locking actions for the user. Explicit locks can also be taken out when performing DML commands. An explicit lock requires that you manually request a specified lock type. Table 9.3 compares modes used for DML locks.

# TABLE 9.3 Comparison of the Oracle DML Lock Modes

| Kind of Lock | Lock Mode (Lock Symbol) | Command | Description |
| :--- | :--- | :--- | :--- |
| Implicit | Row Exclusive (RX) | INSERT, UPDATE, DELETE | Other users can still perform DML on any other row in the table. |
| Implicit | Table Row Share (RS) | SELECT ... FOR UPDATE | Other users can still perform DML on the rows in the table that were not returned by the SELECT statement. |
| Implicit | Share (S) | UPDATE and DELETE on parent tables with Foreign Key relationships to child tables | Users can still perform DML on any other row in either the parent or child table as long as an index exists on the child table's Foreign Key column. |
| Implicit | Share Row Exclusive (SRX) | DELETE on parent tables with Foreign Key relationships to child tables | Users can still perform DML on any other row in either the parent or child table as long as an index exists on the child table's Foreign Key column.* |
| Explicit | Exclusive (X) | LOCK TABLE ... IN EXCLUSIVE MODE | Others users can only query the table until the locking transaction is either committed or rolled back. |

* In versions prior to 9i, Oracle will take out a more restrictive lock on the child table whenever appropriate indexes on the Foreign Key columns of a child table are not present.