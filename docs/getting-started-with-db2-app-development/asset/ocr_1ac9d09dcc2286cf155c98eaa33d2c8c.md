```
EXECUTE IMMEDIATELY SELECT name from EMP where dept = 1
EXECUTE IMMEDIATELY SELECT name FROM EMP where dept = 2
```

# Listing 1.2 - An embedded C dynamic SQL statement using EXECUTE IMMEDIATELY

In many dynamic programming languages such as PHP or Ruby on Rails, where SQL is run dynamically, programmers tend to write the same SQL statements with different field values as follows:

```
SELECT lastname, salary FROM employee where firstnm = 'Raul'
SELECT lastname, salary FROM employee where firstnm = 'Jin'
...
```

In this example, the statements are identical except for the value of the column firstnm. DB2 considers these two dynamic SQL statements as different ones, and therefore at runtime, it prepares and then executes each statement independently. The overhead of preparing the same statement several times can cause performance degradation, therefore prior to DB2 9.7, the recommendation was to code statements as follows:

```
SELECT lastname, salary FROM employee where firstnm = ?
```

The question mark (?) in the statement is known as a parameter marker. Using parameter markers, the program could prepare the statement only once, and then issue EXECUTE statements providing the different values for the parameter marker.

![](bbox=[0.065, 0.525, 0.13, 0.55])

In DB2 9.7, DB2 introduced a technology called statement concentrator where all the statements that are the same except for the field values are automatically lumped together into one single statement with parameter markers, and then EXECUTE statements are performed with the different values. The statement concentrator does have the intelligence to determine when not to lump some statements together; for example, when you purposefully add some clauses to influence the DB2 optimizer.

With respect to performance, static SQL will normally perform better than dynamic SQL since the access plan in static SQL is performed at precompile time and not at runtime. However, for environments where there is a lot of activity such as INSERTs and DELETEs, the statistics calculated at precompile time may not be up-to-date, and therefore, the access plan of the static SQL may not be optimal. In this case, dynamic SQL may be a better choice, assuming a RUNSTATS command is frequently executed to collect current statistics.

> Note:
> Many users think embedded SQL is only static. In reality, it can be both, static or dynamic.

# 1.3.3 CLI and ODBC

Call Level Interface (CLI) was originally developed by the X/Open Company and the SQL Access Group. It was a specification for a callable SQL interface with the purpose of