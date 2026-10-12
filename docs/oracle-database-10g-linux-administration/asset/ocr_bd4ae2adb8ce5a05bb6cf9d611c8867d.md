Try to avoid using NOT when referencing indexed columns. For example, ‘NOT `<`’ is the same as ‘`>=`’, ‘NOT `<=`’ is the same as ‘`>`’, ‘NOT `>`’ is the same as ‘`<=`’, and ‘NOT `>=`’ is the same as ‘`<`’.

Using the IN clause is more efficient than multiple WHERE statements interrogating the same column for multiple values. Use EXISTS in the WHERE clause versus DISTINCT in the SELECT clause (DISTINCT is applied after all rows are returned; WHERE clause predicates limit the number of rows returned).

When using the GROUP BY clause, limit the rows with a WHERE clause line versus using a HAVING clause. The WHERE clause will limit the rows coming back, while the HAVING clause will be applied after all rows are returned.

# ## Finding Poorly Performing SQL

There are several methods for finding poorly performing SQL. Oracle supplies several tools that are useful, such as Enterprise Manager’s TOP (which lists the top SQL that matches the selected criteria, such as IO, time, and so on), the Oracle Trace Facility (a.k.a., trace files and TKProf/Trace Analyzer), and Statspack (statics and SQL text collections). There are many scripts written by numerous experts/DBAs/IT staff to drill into Oracle’s dynamic performance views (a.k.a., the V$ tables) to identify specific performance issues.

# ## Using Scripts

The SQL that Oracle runs is easily accessed from a couple of locations. Listing 16-3 illustrates the V_$SQLAREA view. This view shows the SQL and a significant amount of information about the particular SQL statement. SQL can easily be written to view SQL statements that match a variety of conditions. Information from this view can also be combined with other V$ information to find specific SQL causing specific issues.

# ## Listing 16-3: Listing of V_$SQLAREA

```
shotkaun:ORA110g:SYSTEM>desc v_$sqlarea
```
Name                     Null?    Type
---                    -------    ----
SQL_TEXT                 VARCHAR2(1000)
SQL_ID                   VARCHAR2(13)
SHARABLE_MEM             NUMBER
PERSISTENT_MEM           NUMBER
RUNTIME_MEM              NUMBER
SORTS                    NUMBER
VERSION_COUNT            NUMBER
LOADED_VERSIONS          NUMBER
OPEN_VERSIONS            NUMBER
USERS_OPENING            NUMBER
FETCHES                  NUMBER
```
```