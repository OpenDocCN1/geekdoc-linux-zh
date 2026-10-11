The output in Figure 2.10 shows that the user JJOHNSON is trying to obtain an exclusive lock on the EMPLOYEES table, but is currently waiting to obtain that lock because the user SYSTEM is blocking his request.

![](bbox=[0.2, 0.19, 0.28, 0.24])

> A complete discussion of performance tuning issues related to locking can be found in Chapter 9, “Tuning Contention.”

# ## Top SQL

Top SQL is designed to help you easily identify which SQL statements are consuming the most system resources. Figure 2.11 shows a sample of the Top SQL screen.

# **FIGURE 2.11** Top SQL screen

![](bbox=[0.3, 0.43, 0.9, 0.76])

The output in Figure 2.11 shows the SQL commands that have consumed the most system resources. Top SQL also allows you to drill down on any of the statements simply by double-clicking on that statement. The drilldown information would include details like the statement's execution plan and detailed statistics about the statements I/O and CPU usage.