Records: 0 Duplicates: 0 Warnings: 0
INSERT INTO ... VALUES (...),(...),...
Records: 0 Duplicates: 0 Warnings: 0
LOAD DATA ...
Records: 0 Deleted: 0 Skipped: 0 Warnings: 0
UPDATE ...
Rows matched: 0 Changed: 0 Warnings: 0

The numbers will vary according to the particular statement you've executed, of course.

*mysql_info()* returns non-NULL for *INSERT* INTO ...*VALUES* only if the statement contains more than one value list. For statements not shown in the preceding list, *mysql_info()* always returns *NULL*.

The string returned by *mysql_info()* is in the language used by the server, so you can't necessarily count on being able to parse it by looking for certain words.

+   * const char *
+   *mysql_stat* (MYSQL *\*conn);

Returns a null-terminated string containing server status information, or *NULL* if an error occurred. The format of the string is subject to change. Currently it looks something like this:

Uptime: 2153150 Threads: 6 Questions: 1306220 Slow queries: 271 Opens: 1260
Flush tables: 1 Open tables: 64 Queries per second avg: 6.007

These values may be interpreted as follows:

+      * *Uptime* is the number of seconds the server has been running.
+      * *Threads* is the number of threads currently running in the server.
+      * *Questions* is the number of statements the server has executed.
+      * *Slow queries* is the number of statements that took longer to process than the time indicated by the server's *long_query_time* variable.
+      * *Opens* is the number of tables the server has opened.
+      * *Flush tables* is the number of *FLUSH*, *REFRESH*, and *RELOAD* statements that have been executed.
+      * *Open tables* is the number of tables the server currently has open.
+      * *Queries per second* is the ratio of *Questions* to *Uptime*.

Not coincidentally, the information returned by the *mysql_stat()* function is the same as that reported by the *mysqladmin status* command. (*mysqladmin* itself invokes this function to get the information.)