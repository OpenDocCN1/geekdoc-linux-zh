
## TABLE 9.2 Contents of V$WAITSTAT

| Column Name | Description |
| :--- | :--- |
| CLASS | Short description of the type of segment that the block belongs to |
| COUNT | Number of times a wait to access a block occurred |
| TIME | Total time spent waiting for access to blocks |

Non-zero wait statistics for two classes of blocks in particular, `free list` and `segment header`, indicate that Free List contention is occurring in the database. The sample following query on V$WAITSTAT returns the number of Free List waits that have occurred since instance startup:

```sql
SQL> SELECT class, count
2   FROM v$waitstat
3   WHERE class IN ('free list',
4                    'segment header');
```

![](img/832fbc6aca8b6075843ca6f2356c0a8d_517_0.png)

The output from this query indicates that Free List related waits occurred 12 times for segment headers and four times for free lists.

Once you determine that Free List contention is present, you must next determine which segments are experiencing the contention. This can be achieved using a query on V$SESSION_WAIT and DBA_SEGMENTS.

### Using V$SESSION_WAIT and DBA_SEGMENTS to Measure Free List Contention

The V$SESSION_WAIT view, which contains statistics related to the waits experienced by individual sessions, can be joined to the DBA_SEGMENTS view, which contains information about each segment in the database, to determine which segments are experiencing the Free List contention identified in the previous section. The following query shows how you can join these two tables using the P1, P2, HEADER_FILE, and HEADER_BLOCK columns:

```sql
SQL> SELECT s.segment_name, s.segment_type, s.freelists
2 FROM dba_segments s, v$session_wait w
3 WHERE w.p1 = s.header_file
4 AND w.p2 = s.header_block
5 AND w.event = 'buffer busy waits';
```

| SEGMENT_NAME | SEGMENT_TYPE | FREE_LISTS |
|---|---|---|
| EMPLOYEE | TABLE | 1 |

The output from this query indicates that the EMPLOYEE table, which has only one Free List, is a source of Free List contention in the database.

## Tuning Free List Contention

Once the segments experiencing Free List contention have been identified, you have two options for reducing contention. These options include: adding additional Free Lists to the segment or moving the segment to a tablespace that uses automatic segment-space management.

- **Adding Additional Free Lists** A segment can have more than one Free List. However, by default, only one Free List is assigned to a segment at creation. If additional Free Lists need to be added to the segment in order to resolve Free List contention, then the segment can be altered:

```sql
ALTER TABLE hr.employee
STORAGE (FREE_LISTS 5);
```

Using the above syntax, the number of Free Lists assigned to the EMPLOYEE table would be increased to five.

- **Moving Segments to Automatic Segment-space Managed Tablespaces** One way to minimize Free List contention is to eliminate Free Lists from the process of determining which segment locks should be used to store a newly inserted row. This can be accomplished using a new Oracle9i feature called Automatic Segment-space Management. Tablespaces with the automatic segment-space management feature enabled utilize bitmaps in the tablespace's datafile headers, instead of Free Lists, to manage the free block allocations for each segment in that tablespace. To use this feature to manage the free space allocations for the EMPLOYEE table, you must first create a locally managed, automatic segment-space managed tablespace in which to store the EMPLOYEE table:

```sql
CREATE TABLESPACE app1_data
DATAFILE '/u01/oradata/PROD/app1_data01.dbf' SIZE 500M
EXTENT MANAGEMENT LOCAL
SEGMENT SPACE MANAGEMENT AUTO;
```

Then you need to move the EMPLOYEE table to the new tablespace using the MOVE command:

```sql
ALTER TABLE hr.employee MOVE TABLESPACE app1_data;
```

Any additional new segments created in an automatic segment-space managed tablespace will also use bitmaps instead of Free Lists for free block allocations.

![](img/832fbc6aca8b6075843ca6f2356c0a8d_519_0.png)

> Once moved to an Automatic Segment-space Managed tablespace, the segment’s value for the FREELISTS column in DBA_SEGMENTS view will be null.

## Lock Contention

As you have seen, Oracle uses latches to protect access to memory structures. Latches are held for only short periods of time, and waits for busy latches are also very brief.

Oracle’s locking mechanisms are similar to the latching mechanisms, but locks are used to protect access to data, not memory structures. Locks are also less restrictive than latches. In some cases, several users can share a lock on a segment. This is not possible with latches, which are never shared between processes.

Additionally, unlike latches, lock requests can be queued up in the order they are requested and then applied accordingly. This queuing mechanism is referred to as an enqueuer. The enque keeps track of users who are waiting for locks, which lock mode they need, and in what order they asked for their locks.

Lock contention can occur any time two users try to lock the same resource at the same time. Lock contention usually arises when you have many users performing DML on a relatively small number of tables. When two users try modifying the same row in the same table, at the same time, lock contention results.

In general, locks are used to preserve data consistency. This means that the data a user is changing stays consistent within their session, even if other users are also changing it. Oracle's automatic locking processes lock data at the lowest possible level so as not to needlessly restrict access to application data. Since this type of locking model allows many users to access data at the same time, application users achieve a high degree of data concurrency.

Once taken out, a lock is maintained until the locking user issues either a **COMMIT** or a **ROLLBACK** command. Because of this, locks that are too long in duration or too restrictive in nature can adversely affect performance for other application users who need to access the locked data. In most cases, this locking is done at the row level. Using Oracle's default locking mechanism, multiple users can do the following:

- Change different rows in the same table with no locking issues.
- Change the same row in the same table with enqueues determining who will have access to the row and when, and with System Change Numbers (SCN) deciding whose change will be the final one. In addition to the order in which locks were requested, the enqueue mechanism also keeps track of which users are waiting to obtain locks, and what type of lock they want to obtain.

![](img/832fbc6aca8b6075843ca6f2356c0a8d_520_0.png)

By default, the maximum number of enqueues is derived from the value of the SESSIONS parameter in init.ora. This default is generally adequate, but the number of enqueues can also be tuned manually by setting the ENQUEUE_RESOURCES parameter in the init.ora.

Figure 9.6 demonstrates these two locking situations (two users updating different rows and the same row) when two users are updating and querying data in a table called DEPT.

As illustrated in this figure, when Joe issues his UPDATE statement, he locks the row associated with DEPT_ID 20. When Matt issues his UPDATE command, he locks the row associated with the Sales department. Since Joe and Matt are each locking a different row, neither is affected by the other's lock. When Joe queries the DEPT table looking for the Sales department data, Matt's lock will not prevent Joe from seeing the Sales data. However, since Matt has not yet committed his changes, Joe will use the before-image data in Matt's rollback segment entry to build a read consistent view of the Sales data. Finally, when Matt tries to change the Accounting department's name by updating the row whose DEPT_ID is 20, Matt will experience a wait, stuck behind Joe's lock on the same row. Matt's session will continue to wait until Joe issues either a **COMMIT** or a **ROLLBACK**.
