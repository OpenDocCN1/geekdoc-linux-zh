
## 答案与解析

18. D. The first thing to do is run the ut1xplan.sql script. This script creates the PLAN_TABLE that is used to store execution plans. See Chapter 3 for more information.

19. C. Because the insertions of the data into the new table are not logged, the table would not be recoverable until it was backed up with either a hot or cold backup. See Chapter 7 for details.

20. D. V$DB_CACHE is not a valid Dynamic Performance View. All other methods of collection are valid. See Chapter 5 for more details.

21. C. Increasing the number of users that are utilizing the application would constitute a workload change. See Chapter 1 for more information.

22. B, D. The V$SESSSTAT view shows statistics for all sessions that are connected to the instance. The V$SYSSTAT view does not contain any session-specific statistics, only summary statistics for the entire instance. Since the contents of the V$ views are cleared at instance shutdown, no V$ view contains useful statistics right after instance startup. See Chapter 2 for more information.

23. C. CPU utilizations above 90 percent will cause all processes running on the server to suffer poor performance. See Chapter 10 for more information.

24. A, B, and C. All of these are valid reasons for Oracle to cache SQL statements. By caching SQL, Oracle reduces the I/O overhead because it does not have to go to disk to retrieve information from the Data Dictionary. It reduces memory utilization because it does not have to allocate additional memory for identical statements and reduces CPU utilization because it does not have to re-parse the statements. See Chapter 4 for more details.

25. B. The Lock Monitor component of the Oracle Enterprise Manager Diagnostics Pack provides real-time information about the locks being taken by application users. See Chapter 2 for more information.

26. A, C, and E. All areas of the application and database should be monitored when establishing performance benchmarks. These areas include throughput and response times of SQL statements, statistical data on CPU and memory consumption, and information regarding physical I/O. See Chapter 1 for more information.

27. C. The blocks from the REGION table have been allocated to the Keep pool. Generally, these types of tables would be small, no larger than 10 percent of the overall database buffer cache size. See Chapter 5 for more details.

28. A. The ARC0 process would be responsible for moving information from the Online Redo Logs to the archive logs. You can have multiple Archive processes doing this work if one is not sufficient to keep up with the archive load. See Chapter 7 for details.

29. A. Hash partitioning would be the best solution when the goal is to maintain a fairly even distribution of rows among given partitions. Oracle uses a hashing algorithm to distribute the rows among the given partitions based on the partition key value. See Chapter 3 for more information.

30. B. The key to this question is that the DBA needs to see the ENTIRE SQL statement. V$SQL.TEXT would provide the entire text of the SQL. V$SQL only contains the first 1000 characters of the SQL statement. V$SQLAREA also does not display the entire text of the SQL statement and V$SQL_PLAN contains the address of the SQL statement and not the actual text. Remember though, the SQL contained in V$SQLTEXT may be contained in several rows, so when you perform the query you would want to use an ORDER BY clause. See Chapter 4 for more details.

31. B. Using the DBMS_SYSTEM.SET_SQL_TRACE_IN_SESSION packaged procedure is the best method to use to trace another client process's session. You should not set SQL_TRACE to TRUE for the entire instance, for this will generate trace files for all sessions all the time. The ALTER SESSION command will only trace the connected user's session. See Chapter 2 for more information.

32. A, B, C, and D. All of these statements are true regarding performance tuning. See Chapter 1 for more information.

33. A. The V$DB_CACHE_ADVICE dynamic performance view contains statistics about performance of the database buffer cache at varying sizes. This is a tool that is designed to assist the DBA in achieving the optimal size of the database buffer cache. Remember to set the DB_CACHE_ADVICE init.ora parameter equal to ON to begin collection of these statistics. See Chapter 5 for more details.

34. B. Database Writer is not considered part of Oracle's redo mechanisms. The Redo log buffer, Online Redo Logs, checkpoints, Archiver process, and archive logs constitute the components of Oracle redo architecture. See Chapter 7 for details.

35. B. Parallel statements can take advantage of multiple CPUs. The individual parallel processes can be divided among the available CPUs and run simultaneously to perform the overall statement more efficiently. See Chapter 10 for more information.

36. B. The upper boundary of a partitioned table should include a MAXVALUE partition so that no inserted rows fall above the given range of values for the column on which partitioning is being done. See Chapter 3 for more information.

37. C. The Java Pool would be utilized when you are using Server-Side Java. Java Stored Procedures would be an example of Server-Side Java. See Chapter 6 for more details.

38. B. Row-Level locking ensures a high degree of data concurrency. With row-level locking, it is much less likely that two users will affect one another by requesting the same lock on the same row at the same time. This locking does not prevent readers from accessing the data in the locked row and obtaining a read-consistent view of the data. See Chapter 9 for more information.

39. C. Dictionary managed tablespaces use data dictionary tables stored in the SYSTEM tablespace to determine whether space in the tablespace is free or allocated to a segment. Locally managed tablespaces use bitmaps stored in each Datafile's header to determine whether blocks within the tablespace are free or in use. See Chapter 8 for more details.

40. B. P-Code is another name for the compiled version of code that Oracle creates during the parse phase of SQL execution. See Chapter 4 for more details.

41. C. The Cost-Based optimizer analyzes the statistics gathered on the objects in the SQL statement, considers many different execution plans, and then selects the one with the lowest relative execution cost. See Chapter 3 for more information.

42. C. The Optimal Flexible Architecture is a method of directory naming and location settings that enables you to have a common directory tree and naming construct for all critical Oracle software and application components. See Chapter 2 for more information.

43. D. Although increasing SGA_MAX_SIZE and DB_CACHE_SIZE and bouncing the instance would be the method to use if we had enough memory, in this case there is not enough memory available to make the change that we want. See Chapter 5 for more details.

44. C. All of these could indicate a statement needs tuning except reading blocks for the SGA. You would like to have more reads from the SGA and less reads from disk. This would lead to better performance. See Chapter 3 for more information.

45. A. You would use the `ALTER DATABASE DEFAULT TEMPORARY TABLESPACE temp;` command to set the default temporary tablespace for users of the database. This should be done to avoid the use of the SYSTEM tablespace for sorting. See Chapter 8 for more details.

46. B. Automatic segment-space management utilizes bitmaps in the tablespace's datafile headers, instead of Free Lists, to manage the free block allocations for each segment in that tablespace. This reduces the latch problem that can occur with Free Lists in the segment header. See Chapter 9 for more information.

47. C. Dispatchers can service many clients simultaneously. Because of this, you get a better utilization of resources. See Chapter 6 for more details.

48. C. Generally, the innermost operations of the execution plan are the ones that are the first executed. See Chapter 3 for more information.

49. B. You must have at least two Online Redo Logs—one that is the current Online Redo Log and one to switch to if the current one fills up. There is no limit to the number of online logs you can have. See Chapter 7 for details.

50. B. CPU_COUNT is the `init.ora` parameter that tells Oracle the number of CPUs available on the server. See Chapter 10 for more information.

51. D. Transactions must start and end in the same rollback segment. A transaction will attempt to wrap into the next extent of the rollback segment if the extent has no active transactions. If it does have active transactions, a new extent will be added to the rollback segment and the transaction will grow into this extent. See Chapter 8 for more details.

52. B. Grant the PLUSTRACE role to the users that are going to be using the AUTOTRACE utility in SQL*Plus. If they don't belong to the role, they will receive an error if they try to set AUTOTRACE on. See Chapter 3 for more information.
