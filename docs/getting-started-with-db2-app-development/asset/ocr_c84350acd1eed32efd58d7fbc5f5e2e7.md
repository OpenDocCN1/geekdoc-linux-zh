# ### 3.5.2 Table functions

Table functions return a table of rows. You can call them using the FROM clause of a query. Table functions, as opposed to scalar functions, can change the database state; therefore, INSERT, UPDATE, and DELETE statements are allowed. Some built-in table functions are SNAPSHOT_DYN_SQL() and MQREADALL(). Table functions are similar to views, but since they allow for data modification statements (INSERT, UPDATE, and DELETE) they are more powerful. Typically they are used to return a table and keep an audit record.

*Listing 3.10* provides an example of a table function that enumerates a set of department employees:

```
```sql
CREATE FUNCTION getEnumEmployee(p_dept VARCHAR(3))
RETURNS TABLE
   (empno  CHAR(6),
    lastname VARCHAR(15),
    firstname VARCHAR(12))
SPECIFIC getEnumEmployee
RETURN
    SELECT e.empno, e.lastname, e.firstname
    FROM employee e
    WHERE e.workdept=p_dept
```
```

# **Listing 3.10** - An example of a scalar function

To test the above function, try the SELECT statement shown in *Figure 3.13* below.

![](bbox=[0.15, 0.57, 0.68, 0.705])

**Figure 3.13** – Invoking a table function.

As shown in the above figure, a table UDF has to be invoked in the FROM clause of an SQL statement since it returns a table. The special TABLE() function must be applied and an alias must be provide after its invocation.

# ## 3.6 Triggers: The big picture

Triggers are database objects associated with a table that define operations to occur when an INSERT, UPDATE, or DELETE operation is performed on the table. Triggers are