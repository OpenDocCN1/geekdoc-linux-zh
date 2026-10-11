102 Chapter 3 · SQL Application Tuning and Design

# ## The AUTOTRACE Utility

The Oracle *Autotrace* utility combines elements of both the TKPROF utility and the EXPLAIN PLAN FOR facility. Unlike TKPROF, AUTOTRACE does not require you to format a trace file to get resource usage information. This information is automatically included in the AUTOTRACE output along with the execution plan of the SQL statement that was issued. No separate query on the PLAN_TABLE is required. However, unlike the EXPLAIN PLAN FOR facility, AUTOTRACE actually executes the statement being examined before generating an execution plan.

Some preliminary configuration operations must be performed before the AUTOTRACE utility can be utilized to examine SQL execution paths. These requisite configuration steps and subsequent techniques for using the AUTOTRACE utility are described in the following sections.

# ### Preparing to Use AUTOTRACE

Before using the AUTOTRACE utility, you must first perform several initial setup operations. These operations are performed only once.

First, each user who wishes to use the AUTOTRACE utility will need a PLAN_TABLE table in their schema. This table can be created using the ut1xplan.sql script found in %ORACLE_HOME%\rdbms\admin on Unix systems or %ORACLE_HOME%\rdbms\admin on Windows 2000 systems. Unlike EXPLAIN PLAN FOR, AUTOTRACE will automatically clean out the contents of the PLAN_TABLE between executions.

Second, you will then need to create a database role called PLustrace by running an Oracle-supplied script called plustrc.sql while logged on as the user SYS. This script is located in %ORACLE_HOME%\sqlplus\admin on Unix systems or %ORACLE_HOME%\sqlplus\admin on Windows 2000 systems.

Finally, you will have to grant the new PLUstrace role to every user who will be using the AUTOTRACE utility.

# ### Using AUTOTRACE

The AUTOTRACE utility is only available from within a SQL*Plus session. AUTOTRACE can be activated in a SQL*Plus session by issuing the SET AUTOTRACE ON command. The following example demonstrates the output of the AUTOTRACE utility:

```
```
SQL> set autotrace on
SQL> SELECT dist.distributor_id 'ID',
2  dist.city,
```
```

Copyright ©2002 SYBEX, Inc., Alameda, CA www.sybex.com