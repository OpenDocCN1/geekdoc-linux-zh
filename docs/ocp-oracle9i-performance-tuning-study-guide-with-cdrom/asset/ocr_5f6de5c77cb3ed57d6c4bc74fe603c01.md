| USERNAME | SQL_TEXT | BLOCKS |
| --- | --- | --- |
| APPS | SELECT customer_id, customer_name FROM customer ORDER BY city, state | 210 |

# Tuning Rollback Segment I/O

One of Oracle's basic tenets is never to allow a user to view the data from another user's uncommitted transaction. In order to meet this objective, Oracle must make use of rollback segments to store the before-image of changed data whenever an application user performs DML activity. Instead of the data contained in the uncommitted dirty buffers in the Buffer Cache, Oracle uses these before-images to display the original version of the modified data when other application users request it. In this manner, rollback segments play a critical role in every database DML transaction. Because of this, rollback segments should be examined for possible performance enhancement. The following section provides additional details on how rollback segments are used to process user transactions.

# Understanding Rollback Segments

When a user starts a DML transaction, the before-image of the changed data is buffered in the Database Buffer Cache in the SGA. Copies of these buffers are also written to a rollback segment, which is stored in a tablespace. This tablespace is in turn made up of one or more physical Datafiles. The before-image data stored in the rollback segment is used for three important purposes:

+   - It can be used to restore the original state of the data if the user performing the DML command issues a ROLLBACK command.
+   - It provides a read-consistent view of the changed data to other users who access the same data prior to the DML user issuing a COMMIT command.
+   - It is used during instance recovery to undo uncommitted transactions that were in progress just prior to an instance failure.