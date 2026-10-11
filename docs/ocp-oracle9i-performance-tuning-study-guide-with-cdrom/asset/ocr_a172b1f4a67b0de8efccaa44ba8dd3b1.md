+   * Gather table statistics much faster by performing the analysis in parallel.

+   * Automatically gather statistics on highly volatile tables and bypass gathering statistics on static tables.

The following example shows how the DBMS_STATS packages would be used to gather statistics on the EMPLOYEE table in Joe’s schema:
SQL> EXECUTE DBMS_STATS.GATHER_TABLE_STATS ('JOE', 'EMPLOYEE');

Like the DBMS_UTILITY package, the DBMS_STATS package can also be used to analyze indexes, an entire schema, or the whole database using the procedures shown in Table 3.10.

# TABLE 3.10 Procedures within the DBMS_STATS Package

| Procedure Name | Description |
| :--- | :--- |
| GATHER_INDEX_STATS | Used to gather statistics on a specified index |
| GATHER_SCHEMA_STATS | Used to gather statistics on a specified schema |
| GATHER_DATABASE_STATS | Used to gather statistics on an entire database |
| GATHER_SYSTEM_STATS | Used to gather I/O and CPU performance statistics for the server |

Two of the procedures shown in Table 3.10, GATHER_SCHEMA_STATS and GATHER_SYSTEM_STATS, are particularly useful when utilizing the CBO.

# USING THE GATHER_SCHEMA_STATS PROCEDURE

The GATHER_SCHEMA_STATS procedure listed in Table 3.10 is particularly useful for maintaining accurate statistics for the CBO. Using the GATHER option, you can specify one of the three following options for gathering schema statistics:

GATHER STALE Option  Any table in the schema that has been designated as “monitored” using the ALTER TABLE ... MONITORING command will have its statistics gathered.