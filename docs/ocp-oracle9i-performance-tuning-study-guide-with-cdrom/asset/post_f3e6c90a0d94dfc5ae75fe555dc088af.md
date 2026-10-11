
## Data Dictionary Cache

Whenever an SQL or PL/SQL statement is issued, the data dictionary must also be examined to make sure that the tables referenced in the statement exist, that the column names and data types are correct, and that the application user issuing the statement has sufficient privileges on the segments involved. Like the statement itself, this information is also cached in memory in the Shared Pool's *Data Dictionary Cache*. This memory area is also managed using an LRU mechanism.

By using the Data Dictionary Cache, the Oracle Server caches the data dictionary information in a separate memory area than it does the associated SQL statements. This is useful for two reasons:

- The LRU mechanisms for the Library Cache and Data Dictionary Cache work independently. This tends to keep data dictionary information in memory longer.
- Subsequent application users who issue similar, but not identical, statements as previous users benefit from the fact that the data dictionary information associated with the tables in their statement may be in memory—even if the actual statement is not.

## User Global Area

The User Global Area (UGA) is only present in the Shared Pool if the Shared Server option is being used. In the shared server architecture, the *User Global Area* is used to cache application user session information. This information must be in a shared location because the shared server architecture uses several different shared server processes to process SQL and PL/SQL activity against the instance. Since the shared server process that starts a transaction may not be the one that also finishes it, access to this session information must be stored in the UGA. In a non-shared (or dedicated) server situation, this session information is maintained in the application user's private *Process Global Area* (PGA).

> **NOTE**
> 
> See Chapter 6 of this book, “Tuning Other SGA Areas,” for more details on tuning a shared server configuration.

## Measuring the Performance of the Shared Pool

The primary indicator of the performance of the Shared Pool is the cache-hit ratio. High cache-hit ratios indicate that your application users are frequently finding the SQL and PL/SQL statements they are issuing already in memory. *Hit ratios* can be calculated for both the Library Cache and the Data Dictionary Cache.

![](img/832fbc6aca8b6075843ca6f2356c0a8d_250_0.png)

> NOTE
> 
> Oracle recommends tuning the Library Cache to maximize its hit ratio before attempting to tune the Database Buffer Cache because a less-than-optimal cache hit ratio for the Library Cache has a greater impact on performance than does an underperforming cache hit ratio for the Database Buffer Cache.

### Measuring Library Cache Performance

The performance of the Library Cache is measured by calculating its hit ratio. This hit ratio information can be found in four places: the **V$LIBRARYCACHE** dynamic performance view, **STATSPACK** and **REPORT.TXT** output, and the output from the Performance Manager GUI tool.

**Oracle Objective**
Measure and tune the Library Cache hit ratio

### Using V$LIBRARYCACHE to Monitor the Library Cache

A Library Cache miss can occur at either the parse or execute phases of SQL statement processing. The cache hit ratio related to the parse phase is shown in the **GETHITRATIO** column of **V$LIBRARYCACHE**. The cache hit ratio related to the execution phase is shown in the **PINITRATIO** column of **V$LIBRARYCACHE**. The **RELOADS** and **INVALIDATIONS** columns of **V$LIBRARYCACHE** are also useful for Library Cache tuning. A sample query on **V$LIBRARYCACHE** showing these columns is included here in Figure 4.2.

**FIGURE 4.2 Sample query on V$LIBRARYCACHE**

```sql
SQL> SELECT namespace, gethitratio, pinhitratio, reloads, invalidations
  2  FROM v$librarycache
  3  WHERE namespace IN ('SQL AREA',
  4    'TABLE/PROCEDURE',
  5    'BODY',
  6    'TRIGGER');
```

| NAMESPACE | GETHITRATIO | PINHITRATIO | RELOADS | INVALIDATIONS |
| :--- | :--- | :--- | :--- | :--- |
| SQL AREA | .915877437 | .937549722 | 10 | 2 |
| TABLE/PROCEDURE | .799093656 | .807164634 | 0 | 0 |
| BODY | .7 | .625 | 0 | 0 |
| TRIGGER | 1 | 1 | 0 | 0 |

The **NAMESPACE** column in the above figure shows the source of the cached code. Table 4.3 shows the definition of each namespace type.

**TABLE 4.3 Code Source by Namespace Type**

| Namespace | Code Source |
| :--- | :--- |
| SQL AREA | SQL statement |
| TABLE/PROCEDURE | PL/SQL stored procedure or function |
| BODY | PL/SQL package body |
| TRIGGER | PL/SQL trigger |

The other values for **NAMESPACE** found in **V$LIBRARYCACHE** refer to information used to determine dependencies between cached objects and statements. These values are of little value to you in terms of database tuning.

#### GETHITRATIO

In **V$LIBRARYCACHE**, Oracle uses the term *get* to refer to a type of lock, called a *Parse Lock*, that is taken out on an object during the parse phase for the statement that references that object. Each time a statement is parsed, the value for GETS in the **V$LIBRARYCACHE** view is incremented by 1. The column **GETHIT** stores the number of times that the SQL and PL/SQL statements issued by the application found a parsed copy of themselves already in memory. When this occurs, there is no parsing of the statement required. The user’s Server Process just executes the copy already in memory instead. The ratio of parsed statements (GETS) to those that did not require parsing (GETHITS) is calculated in the GETHITRATIO column of V$LIBRARYCACHE. In the sample output in Figure 4.2, our application users are finding the SQL statements they are issuing already in the Library Cache (i.e., GETHITRATIO) 91.5 percent of the time. The higher this number is, the better the application is performing.

> According to Oracle, well-tuned OLTP systems can expect to have GETHITRATIOs of 90 percent or higher for the SQL Area portion of the Library Cache. DSS and data warehouse applications often have lower hit ratios because of the ad hoc nature of the queries against them.

#### PINHITRATIO

PINS, like GETS, are also related to locking. However, while GETS are associated with locks that occur at parse time, PINS are related to locks that occur at execution time. These locks are the short-term locks used when accessing an object. Therefore, each library cache GET also requires an associated PIN, in either Shared or Exclusive mode, before accessing the statement’s referenced objects. Each time a statement is executed, the value for PINS is incremented by 1. The PINHITRATIO column in V$LIBRARYCACHE indicates how frequently executed statements found the associated parsed SQL already in the Library Cache. In the sample output in Figure 4.2, this is occurring 93.7 percent (i.e., PINHITRATIO) of the time.

> Oracle recommends that well-tuned OLTP systems strive for a PINHITRATIO that exceeds 90 percent for the SQL Area portion of the Library Cache. DSS and data warehouse applications will generally be lower.

#### RELOADS

The RELOADS column shows the number of times that an executed statement had to be re-parsed because the Library Cache had aged out or invalidated the parsed version of the statement. Reload activity can be monitored by comparing the number of statements that have been executed (**PINS**) to the number of those statements that required a reload (**RELOADS**):

```sql
SQL> SELECT SUM(reloads)/SUM(pins) "Reload Ratio"
2 FROM v$librarycache;

Reload Ratio
----------
.001506251
```

In this example our Reload Ratio is .0015, or 0.15 percent. This means that we are not re-parsing statements that were previously loaded in the Library Cache very often.

![](img/832fbc6aca8b6075843ca6f2356c0a8d_253_0.png)

#### INVALIDATIONS

Invalidations occur when a cached SQL statement is marked as invalid and therefore forced to parse even though it was already in the Library Cache. Cached statements are marked as invalid whenever the objects they reference are modified in some way. For example, recompiling a view that was used by previously cached SQL statements will cause those cached statements to be marked as invalid. Therefore, any subsequent statements that use this view will need to be parsed even though an exact copy of that statement may already be cached. High values for **INVALIDATIONS** mean additional overhead for the application. Therefore, performing activities that might cause invalidations should be weighed against the expected benefit of those activities.

### Using STATSPACK to Monitor the Library Cache

Much of the information obtained from the preceding queries against V$LIBRARYCACHE is also available in the output from the STATSPACK utility. Library Cache performance statistics are included in the STATSPACK section headed **Instance Efficiency Percentages (Target 100%)**. The STATSPACK output shown in Figure 4.3 shows that the Library Cache hit ratio was 86.11 percent for the database being monitored.
