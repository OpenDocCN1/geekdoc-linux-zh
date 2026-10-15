```
no external action
deterministic
return
select (salary_new - salary_old) as salary_diff from employee_hist h , employee o
where h.empno = emp
and h.empno = o.empno
and h.chg_date = (select max(chg_date)
from employee_hist
where empno = h.empno)
```

```
db2inst1@db1nx02:~/tpc> db2 "select empno, firstnme, lastname, salary_diff(empno) as salary_diff from employee where empno in ('000110','000070')"
```

| EMPNO | FIRSTNME | LASTNAME | SALARY_DIFF |
| --- | --- | --- | --- |
| 000110 | VINCENZO | LUCCHESSI | -25000.00 |
| 000070 | EVA | PULASKI | 10000.00 |

2 record(s) selected.

> Note: The statement select max(chg_date) is needed, because for each empno there can exist more than one row in employee_hist table, but a UDF can return only one row.

# 8.2.3 Stored procedures

A stored procedure helps to reduce unnecessary data transfer over the network between client and server. The SQL statements and definitions are stored on the database server. The client sends only the necessary data over the network to call the stored procedure and gets the results sent back. This helps to improve the overall performance of client server applications.

The create procedure DDL statement defines a procedure within an application server. There are two types of procedures: external procedures, which are written in a programming language; and SQL procedures, which are written in SQL. In Example 8-4, there is an SQL procedure that calculates the new salary and bonus for an employee. The input is an employee number and rating, and the result is to update the table EMPLOYEE.

> Note: The create procedure statement is explained in more detail in Chapter 5, "Statements" in the "SQL References" (listed in "Other publications" on page 303.