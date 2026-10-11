for a long time. Changing the priorities can also ensure that particular kinds of queries are processed more quickly. This section looks at MySQL's default scheduling policy and the options that are available to you for influencing this policy. It also describes the use of concurrent inserts and the effect that storage engine locking levels have on concurrency among clients. For the purposes of this discussion, a client performing a retrieval (a *SELECT*) is a reader. A client performing an operation that modifies a table (*DELETE*, *INSERT*, *REPLACE*, or *UPDATE*) is a writer.

MySQL's default scheduling policy can be summarized like this:

+   Writes have higher priority than reads.
+   Writes to a table must occur one at a time, and write requests are processed in the order in which they arrive.
+   Multiple reads from a table can be processed simultaneously.

The *MyISAM*, *MERGE*, and *MEMORY* storage engines implement this scheduling policy with the aid of table locks. Whenever a client accesses a table, a lock for it must be acquired first. When the client is finished with a table, the lock on it can be released. It's possible to acquire and release locks explicitly by issuing *LOCK TABLES* and *UNLOCK TABLES* statements, but normally the server's lock manager automatically acquires locks as necessary and releases them when they no longer need be needed. The type of lock required depends on whether a client is writing or reading.

A client performing a write to a table must have a lock for exclusive table access. The table is in an inconsistent state while the operation is in progress because the data row is being deleted, added, or changed, and any indexes on the table may need to be updated to match. Allowing other clients to access the table while the table is in flux would cause problems. It's clearly a bad thing to allow two clients to write to the table at the same time because that would quickly corrupt the table into an unusable mess. But it's not good to allow a client to read from an in-flux table, either, because the table might be changing at the location being read, and the results would be inaccurate.

A client performing a read from a table must have a lock to prevent other clients from writing to the table and changing it during the read. The lock need not be for exclusive access, however. Reading doesn't change the table, so there is no reason one reader should prevent another from accessing the table. Therefore, a read lock enables other clients to read the table at the same time.

MySQL provides several statement modifiers that allow you to influence its scheduling policy:

+   The *LOW_PRIORITY* keyword applies to *DELETE*, *INSERT*, *LOAD DATA*, *REPLACE*, and *UPDATE* statements.
+   The *HIGH_PRIORITY* keyword applies to *SELECT* and *INSERT* statements.
+   The *DELAYED* keyword applies to *INSERT* and *REPLACE* statements.