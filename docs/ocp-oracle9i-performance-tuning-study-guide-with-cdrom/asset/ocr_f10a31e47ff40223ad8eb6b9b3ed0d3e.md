+   * ANALYZE
+   * CREATE INDEX
+   * Joins between tables on columns that are not indexed

Oracle allows each user process to use a specified amount of memory for each sort operation. If a sort operation is smaller than this size, the sort will be performed in memory. If the sort operation is larger than this size, the sort is broken up into chunks called sort runs. Each chunk is then *sorted* individually, with the intermediate sorted chunks being written to the user’s temporary tablespace. Once all the chunks have been sorted, the final, sorted result is created when the separate sorted chunks are merged together and returned to the user.

| *Oracle Objectives* | Describe how sorts are performed |
|---|---|
| | Differentiate between disk and memory sorts |

The amount of memory set aside for each user’s Server Process to perform these sort operations is impacted by the following `init.ora` parameters:

+   * SORT_AREA_SIZE
+   * SORT_AREA_RETAINED_SIZE
+   * PGA_AGGREGATE_TARGET
+   * WORKAREA_SIZE_POLICY

Each of these `init.ora` parameters and their effect on sorting behavior is addressed in the following sections.

# SORT_AREA_SIZE

The default value for SORT_AREA_SIZE is OS-dependent. The minimum size for this parameter is equivalent to six Oracle blocks. The maximum size is OS-dependent. SORT_AREA_SIZE specifies how much memory each user’s Server Process should set aside to perform in-memory sort operations.

The `SORT_AREA_SIZE` parameter can be set in `init.ora`, or by issuing the `ALTER SYSTEM SET SORT_AREA_SIZE=n DEFERRED` command, or by using the `ALTER SESSION SET SORT_AREA_SIZE=n` command.