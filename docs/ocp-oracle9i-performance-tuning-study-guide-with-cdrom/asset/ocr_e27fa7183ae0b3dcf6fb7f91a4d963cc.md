# DISABLEING MATERIALIZED VIEWS

Materialized views can be disabled at the instance, session, or statement level by using one of the following four methods:

+   - Set the `init.ora` parameter `QUERY_REWRITE_ENABLED=FALSE` and restart the instance.
+   - Dynamically set the value of `QUERY_REWRITE_ENABLED=FALSE` using the `ALTER SYSTEM` command.
+   - Set `QUERY_REWRITE_ENABLED=FALSE` at the session level using the `ALTER SESSION` command.
+   - At the statement level, use the `NOWRITE` hint in a query.

![](bbox=[0.13, 0.36, 0.2, 0.42])

> Users need the `QUERY REWRITE` or `GLOBAL QUERY REWRITE` system privilege in order to enable and disable the query rewrite functionality on materialized views in their own schema, or another user’s schema, respectively.

# DROPPING MATERIALIZED VIEWS

The following example demonstrates the syntax for dropping a materialized view:

```
SQL> DROP MATERIALIZED VIEW emp_by_district;
Materialized view dropped.
```

![](bbox=[0.13, 0.61, 0.2, 0.67])

> Dropping a materialized view does not affect any of the data in the base tables that the view was built on.

# Minimizing I/O Using Indexes and Clusters

Stored outlines and materialized views aid query performance by reducing the options that the optimizer must consider when developing an execution plan. This section deals with the other half of the query execution equation—the speed with which the data is actually retrieved once the plan is executed. One of the most effective methods for reducing the time it takes for the Oracle Server to find and return rows is achieved through the use of indexes, partitions, and clusters.