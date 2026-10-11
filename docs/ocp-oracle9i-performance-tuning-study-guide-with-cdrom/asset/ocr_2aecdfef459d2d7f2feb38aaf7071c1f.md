![](bbox=[0.13, 0.12, 0.22, 0.18])

By default, the number of DML locks is derived from the value of the TRANSACTIONS parameter in the init.ora. This default is generally adequate, but the number of DML locks can also be tuned manually by setting the DML_LOCKS parameter in the init.ora.

DDL Locks  DDL or dictionary locks are denoted by TX and are used to lock tables when users are creating, altering, or dropping tables. This type of lock is always at the table level and is designed to prevent two users from modifying a table's structure simultaneously. Table 9.4 shows a comparison of the different modes used for DDL locks.

# TABLE 9.4 Comparison of the Oracle DDL Lock Modes

| Lock Type | Lock Mode | Command | Description |
| :--- | :--- | :--- | :--- |
| Implicit | Exclusive (X) | CREATE, DROP, ALTER | Prevents other users from issuing DML or SELECT statements against the referenced table until after the CREATE, DROP, or ALTER operation is complete |
| Implicit | Shared (S) | CREATE PROCEDURE, AUDIT | Prevents other users from altering or dropping the referenced table until after the CREATE PROCEDURE or AUDIT operation is complete |
| Implicit | Breakable Parse | - | Used by statements cached in the Shared Pool; never prevents any other types of DML, DDL, or SELECT by any user |

# Real World Scenario
The Special Case of Deadlocks

I was once working with an application user who was in the process of training a new employee to use the company's Customer Relationship Management (CRM) system. While they were working together, I overheard the senior employee say, “Every once in a while I get this weird deadlock error. I don't know what it is, but if you see that error, just enter