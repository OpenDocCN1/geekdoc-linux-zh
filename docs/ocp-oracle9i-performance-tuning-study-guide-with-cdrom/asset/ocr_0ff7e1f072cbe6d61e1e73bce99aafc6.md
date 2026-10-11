These views can be used to see which statements application users are actually issuing against the instance, how many times a statement has been issued, and how many disk and buffer reads and sorts a statement did.

![](bbox=[0.13, 0.19, 0.24, 0.25])

The **V$SQLAREA** view contains only the first 80 characters of the SQL or PL/SQL statements that are being issued. The complete text of these SQL or PL/SQL statements can be found in the SQL\_TEXT column of the data dictionary view V$SQLTEXT.

The execution plans that are cached in the Shared Pool can be seen by querying the **V$SQL\_PLAN** dynamic performance view. This view contains most of the columns found in an EXPLAIN\_PLAN table, plus some additional columns used to keep track of which cached SQL statement each execution plan belongs to. These views can even be joined together in order to get a more complete picture of the SQL activity against the database. For example, the query shown in Figure 4.1 displays the username, SQL text, and execution plan of a SQL statement cached in the Library Cache by the user HR.

# **FIGURE 4.1 Examining the contents of the Library Cache**

```
```sql
SELECT p.username, l.sql_text, LPAD('.4*(LEVEL-2))||
       l.operation||' ||
       l.options||'' ||
       o.object_name 'Execution Plan'
FROM (
     select s.username, p.address, p.hash_value, p.operation,
            p.options, p.object_plan, p.p_id, p.p_a
     from v$sql_plan p, v$session s
     where p.address = s.sql_address
        and p.hash_value = s.sql_hash_value
     and s.username = 'HR' p.v$sql')
  WHERE () .address=p.address
  AND l.hash_value=l.hash_value) p, v$sql
  START WITH id = 0
  CONNECT BY PRIOR id = parent_id;
```

USERNAME        SQL_TEXT                                   Execution Plan
----------------- ------------------------------------------ --------------------------------------
HR
                select e.employee_id, e.first_name, SELECT STATEMENT
                e.last_name, d.department
                t_name from employees e, dept
                d where e.department_id
                  = d.department_id

                                      HASH JOIN
                                      TABLE ACCESS FULL EMPLOYEES
                                      TABLE ACCESS FULL DEPARTMENTS
```

If you are only looking for more general information about the types of SQL statements application users are issuing, you can use the **V$SESSION** and V$DB\_OBJECT\_CACHE views.