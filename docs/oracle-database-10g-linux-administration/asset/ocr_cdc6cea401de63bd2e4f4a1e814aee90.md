This technique also works for primary-key constraints. Use CREATE UNIQUE INDEX ... UNUSABLE, then Alter INDEX REBUILD <parallel> UNRECOVERABLE, and then ALTER TABLE ADD CONSTRAINT ... PRIMARY KEY (key column) USING INDEX. Not only does this method build the index very quickly, but it also allows you to name the primary key index.

> NOTE
> *UNRECOVERABLE turns off the Oracle redo journaling that would normally occur. Not incurring this overhead greatly speeds up the index creation process.*

Unique indexes perform better on single-row lookups, since they store a key value and the ROWID together.

Nonunique indexes perform better on range scans, as ROWIDs are stored with each common key value. The commoner the keys, the more ROWIDs that are stored in each leaf block, and the better the range scans perform (for instance, less I/O).

Reverse-key indexes perform better on inserts, especially when the key value is always ascending (for example, when used with a sequence generator), since the locking contention is spread out evenly across the leaf-level structure. These indexes can be used only for single-row lookups, though.

Function-based indexes are useful when it is necessary to include a function in the WHERE clause and where an index would definitely improve performance.

Bitmap indexes are useful when indexing just a few column values in a table with a large number of rows. Use INDEX_COMBINE or INDEX_JOIN hints when the SQL will access two or more bitmap indexes.

Index columns frequently appear in WHERE clauses (which are part of a join between tables) and in foreign keys accessed by primary keys in other tables.
Avoid indexing columns that are frequently updated and only have a few values across a larger table.

Multiple-key (composite) indexes can increase performance, especially if the composite key satisfies the requesting SQL's need for data. Oracle will not read the table if it doesn't have to.

Composite key selection should be based on the frequency that the key columns appear in WHERE clauses. If one of the key values appears more frequently in WHERE clauses than others, then consider making it the leading key field. If the data in a column in the table is in a particular order, and if this column is also frequently used in WHERE clauses, consider putting this column as the leading key in the composite key (see the following section).

Composite key selection, meanwhile, should be as WHERE clauses using the AND operator.
If it is more advantageous to do a full table scan than to access the index, use the FULL or NO_INDEX hints.