where `BLOB` or `TEXT` identifier information stored in a synthetic index column can be useful. You can search that column to determine the row or rows you want and then re-trieve the `BLOB` or `TEXT` values from the qualifying rows.

**Segregate BLOB or TEXT columns into a separate table.** Under some circumstances, it may make sense to move these columns out of a table into a secondary table, if that en-ables you to convert the table to fixed-length row format for the remaining columns. This will reduce fragmentation in the primary table and allow you to take advantage of the performance benefits of having fixed-length rows. It also enables you to run `SELECT *` queries on the primary table without pulling large `BLOB` or `TEXT` values over the network.

# 5.4 Loading Data Efficiently

Most of the time you'll probably be concerned about optimizing `SELECT` statements be-cause they are the most common type of statement and because it's not always straightfor-ward to figure out how to optimize them. By comparison, loading data into your database is straightforward. Nevertheless, there are strategies you can use to improve the efficiency of data-loading operations. The basic principles are these:

+   * Bulk loading is more efficient than single-row loading because the key cache need not be flushed after each input record is loaded. It can be flushed at the end of the batch of records. The more you can reduce key cache flushing, the faster data load-ing will be. (Index modifications are made in the key cache before being written to disk; flushing the cache once rather than many times significantly reduces disk I/O.)

+   * Loading is faster when a table has no indexes than when it is indexed. If there are indexes, not only must the row's contents be added to the table, each index must also be modified to reflect the addition of the new row.

+   * Shorter `SQL` statements are faster than longer statements because they involve less parsing on the part of the server and because they can be sent over the network from the client to the server more quickly.

Some of these factors may seem minor (the last one in particular), but if you're loading a lot of data, even small efficiencies make a difference. From the preceding general princi-ples, several practical conclusions can be drawn about how to load data most quickly.

`LOAD DATA` (all forms) is more efficient than `INSERT` because it loads rows in bulk. The server must parse and interpret only one statement, not several. Also, the index needs flushing only after all rows have been processed, rather than after each row.

`LOAD DATA` is more efficient without `LOCAL` than with it. Without `LOCAL`, the file must be located on the server and you must have the `FILE` privilege, but the server can read the file directly from disk. With `LOAD DATA LOCAL`, the client reads the file and sends it over the network to the server, which is slower.

If you must use `INSERT`, try to use the syntax that specifies multiple rows to be inserted in a single statement: