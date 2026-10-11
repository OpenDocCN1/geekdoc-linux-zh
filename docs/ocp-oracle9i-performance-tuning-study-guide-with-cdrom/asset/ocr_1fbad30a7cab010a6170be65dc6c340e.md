![](bbox=[0.14, 0.13, 0.23, 0.19])

A complete description of all the DBA views can be found in Chapter 2, "Static Data Dictionary Views," in the *Oracle9i Database Reference Release 1 (9.0.1)* (Part Number **A90190-01**).

Some of the columns in the DBA views are not populated with data until the table or index the view references has been analyzed using the **ANALYZE TABLE** or **ANALYZE INDEX** commands.

![](bbox=[0.14, 0.3, 0.23, 0.37])

Analyzing tables and indexes is discussed in Chapter 3, "SQL Application Tuning and Design."

# Sample Queries on Views

In order to demonstrate the usefulness of these views for performance tuning, a brief example of each type will be presented here. Each subsequent chapter also contains examples of relevant queries on the **V$** and **DBA** views for the topic addressed in that chapter.

# Sample V$ View Query

When querying the **V$** views, it is not uncommon to join two or more of these views together in order to get all the information you require. For example, querying **V$SESSTAT** will give you detailed statistics about events within a particular user's session, but will not tell you the name of each statistic. To get the meaning of each statistic, you will have to join **V$SESSTAT** to **V$STATNAME**. An example of this type of query is shown in the following code listing. This query would show all the session statistics for a user called Chris.

```
select s.username, n.name, t.value
from v$session s, v$statname n, v$sesstat t
where s.sid=t.sid
and t.statistic#=n.statistic#
and s.username = 'CHRIS';
```