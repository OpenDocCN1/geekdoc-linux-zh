
| student_id | event_id | score |
|---|---|---|
| 8 | 5 | 13 |
| 9 | 5 | 18 |

### 2.13.2 Using Transaction Savepoints

MySQL enables you to perform a partial rollback of a transaction. To do this, issue a SAVEPOINT statement within the transaction to set a marker. To roll back to just that point in the transaction later, use a ROLLBACK statement that names the savepoint. The following statements illustrate how this works:

```
mysql> CREATE TABLE t (i INT) ENGINE = InnoDB;
mysql> START TRANSACTION;
mysql> INSERT INTO t VALUES(1);
mysql> SAVEPOINT my_savepoint;
mysql> INSERT INTO t VALUES(2);
mysql> ROLLBACK TO SAVEPOINT my_savepoint;
mysql> INSERT INTO t VALUES(3);
mysql> COMMIT;
mysql> SELECT * FROM t;
```

| i |
|---|
| 1 |
| 3 |

After executing these statements, the first and third rows have been inserted, but the second one has been canceled by the partial rollback to the my_savepoint savepoint.

### 2.13.3 Transaction Isolation

Because MySQL is a multiple-user database system, different clients can attempt to use any given table at the same time. Storage engines such as MyISAM use table locking to keep clients from modifying a table at the same time, but this does not provide good concurrency performance when there are many updates. The InnoDB storage engine takes a different approach. It uses row-level locking for finer-grained control over table access by clients. One client can modify a row at the same time that another client reads or modifies a different row in the same table. If both clients want to modify a row at the same time, whichever of them acquires a lock on the row gets to modify it first. This provides better concurrency than table locking. However, there is the question about whether one client's transaction should be able to see the changes made by another client's transaction.

InnoDB implements transaction isolation levels to give clients control over what kind of changes made by other transactions they want to see. Different isolation levels allow or prevent the various problems that can occur when different transactions run simultaneously:

- Dirty reads. A dirty read occurs when a change made by one transaction can be seen by other transactions before the transaction has been committed. Another transaction thus might think the row has been changed, even though that will not really be true if the transaction that changed the row later is rolled back.
- Nonrepeatable reads. A nonrepeatable read refers to the failure by a transaction to get the same result for a given `SELECT` statement each time it executes it. This might happen if one transaction performs a `SELECT` twice but another transaction changes some of the rows in between the two executions.
- Phantom rows. A phantom is a row that becomes visible to a transaction when it was not previously. Suppose that a transaction performs a `SELECT` and then another transaction inserts a row. If the first transaction runs the same `SELECT` again and sees the new row, that is a phantom.

To deal with these problems, InnoDB supports four transaction isolation levels. These levels determine which modifications made by one transaction can be seen by other transactions that execute at the same time:

- `READ UNCOMMITTED`
  - A transaction can see row modifications made by other transactions even before they have been committed.
- `READ COMMITTED`
  - A transaction can see row modifications made by other transactions only if they have been committed.
- `REPEATABLE READ`
  - If a transaction performs a given `SELECT` twice, the result is repeatable. That is, it gets the same result each time, even if other transactions have changed or inserted rows in the meantime.
- `SERIALIZABLE`
  - This isolation level is similar to `REPEATABLE READ` but isolates transactions more completely: Rows examined by one transaction cannot be modified by other transactions until the first transaction completes. This enables one transaction to read rows and at the same time prevent them from being modified by other transactions until it is done with them.

Table 2.4 shows for each isolation level whether it allows dirty reads, nonrepeatable reads, or phantom rows. The table is InnoDB-specific in that `REPEATABLE READ` does not allow phantom rows to occur. Some database systems do allow phantoms at the `REPEATABLE READ` isolation level.

### Table 2.4 Problems Allowed by Isolation Levels

| Isolation Level | Dirty Reads | Nonrepeatable Reads | Phantom Rows |
|---|---|---|---|
| READ UNCOMMITTED | Yes | Yes | Yes |
| READ COMMITTED | No | Yes | Yes |
| REPEATABLE READ | No | No | No |
| SERIALIZABLE | No | No | No |

The default InnoDB isolation level is REPEATABLE READ. This can be changed at server startup with the --transaction-isolation option, or at runtime with the SET TRANSACTION statement. The statement has three forms:

```
SET GLOBAL TRANSACTION ISOLATION LEVEL level;
SET SESSION TRANSACTION ISOLATION LEVEL level;
SET TRANSACTION ISOLATION LEVEL level;
```

A client that has the SUPER privilege can use SET TRANSACTION to change the global isolation level, which then applies to any clients that connect thereafter. In addition, any client can change its own transaction isolation level, either for all subsequent transactions within its session with the server (if SESSION is specified) or for its next transaction only (if SESSION is omitted). No special privileges are required for the client-specific levels.

Most of the information in this section also applies to Falcon. Some differences from InnoDB are that Falcon does not support the READ UNCOMMITTED isolation level and currently does not support SERIALIZABLE (although work is in progress to add support for the latter level).

### 2.13.4 Non-Transactional Approaches to Transactional Problems

In a non-transactional environment, some transactional issues can be handled and some cannot. The following discussion covers what can and cannot be achieved without using transactions. You can use this information to determine whether an application can employ the techniques here and avoid the overhead of transaction-safe tables.

First, let's consider how concurrency problems can occur when multiple clients attempt to make changes to a database using operations that each require several statements. Suppose that you're in the garment sales business and your cash register software automatically updates your inventory levels whenever one of your salesman processes a sale. The sequence of events shown here outlines the operations that take place when multiple sales occur. For the example, assume that the initial shirt inventory level is 47.

1. Salesman A sells three shirts and registers the sale. The register software begins to update the database by selecting the current shirt count (47):
   ```
   SELECT quantity FROM inventory WHERE item = 'shirt';
   ```

2. In the meantime, Salesman B has sold two shirts and registered the sale. The software at the second register also begins to update the database:
   ```
   SELECT quantity FROM inventory WHERE item = 'shirt';
   ```

3. The first register computes the new inventory level to be 47-3 = 44 and updates the shirt count accordingly:
   ```
   UPDATE inventory SET quantity = 44 WHERE item = 'shirt';
   ```

4. The second register computes the new inventory level to be 47-2 = 45 and updates the count:
   ```
   UPDATE inventory SET quantity = 45 WHERE item = 'shirt';
   ```

At the end of this sequence of events, you've sold five shirts. That's good. However, the inventory level says 45. That's bad, because it should be 42. The problem is that if you look up the inventory level in one statement and update the value in another statement, you have a multiple-statement operation. The action taken in the second statement is dependent on the value retrieved in the first. If separate multiple-statement operations occur during overlapping time frames, the statements from each operation intertwine and interfere with each other. To solve this problem, it's necessary that the statements for a given operation execute without interference from other operations.

To deal with the concurrency issues inherent in the situation just described, you can take a couple of approaches.

Lock the tables explicitly. You can group statements and execute them as a unit by surrounding them with LOCK TABLES and UNLOCK TABLES statements: Lock all the tables that you need to use, issue your statements, and release the locks. This prevents anyone else from changing the tables while you have them locked. Using table locking, the inventory update scenario might be handled like this:

1. Salesman A sells three shirts and registers the sale. The register software begins the inventory process by acquiring a table lock and retrieving the current shirt count (47):
   ```
   LOCK TABLES inventory WRITE;
   SELECT quantity FROM inventory WHERE item = 'shirt';
   ```

   A WRITE lock is necessary here because the ultimate goal of the operation is to modify the inventory table, which involves writing to it.

2. In the meantime, Salesman B has sold two shirts and registered the sale. The software at the second register also begins to update the database by trying to acquire a lock:
   ```
   LOCK TABLES inventory WRITE;
   ```

   In this case, this statement blocks because Salesman A already holds a lock on the table.
