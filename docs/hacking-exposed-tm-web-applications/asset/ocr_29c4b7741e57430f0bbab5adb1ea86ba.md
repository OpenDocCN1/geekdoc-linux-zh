# 234 Hacking Exposed Web Applications

+   - Msdb Supports SQL Server Agent for job scheduling.
- Tempdb Used as temporary storage for all jobs.
- Pubs Sample database that should be deleted.

We will define queries of or access the Master database. More importantly, we need to know some techniques to determine the database configuration, the Web application's database and tables, and the Windows environment around the database. This is accomplished by accessing internal variables, stored procedures, and tables.

Default Internal Variables Microsoft SQL Server has several built-in variables that return information about the server. These variables will be available even if the administrators lock access to the extended stored procedures (xp* commands). They also have the advantage of consisting of a single word. They don't require the database name prepended, as in master..xp_cmdshell. Table 9-2 lists the default SQL Server variables.

The procedures in तालिका type return the most useful information. They only return a single datum—this comes handy in some circumstances, as manipulating ODBC error codes that operate on a single variable.

Each of the procedures can also be called with a select statement in the format: SELECT @@@variable.

The Name of the Rows SQL Server contains a small number of stored procedures that users can call without explicit casting to the mer.. database. Consequently, these are

```
@@connections @@max_connections @@servicename
@@cpu_busy @@max_precision @@spid
@@cursor_rows @@microsoftversion @@textsize
@@dbts @@nestlevel @@timeticks
@@error @@options @@total_errors
@@fetch_status @@pack_received @@total_read
@@identity @@pack_sent @@total_write
@@idle @@packet_errors @@trancount
@@io_busy @@proc @@version
@@langid @@rowcount
@@language @@servername
```

| Table 9-2. Default MS SQL Server Variables |