```
ADM5500W DB2 is performing lock escalation. The total number of locks currently held is "11382", and the target number of locks to hold is "5691".
^^
2002-11-01-12.15.23.114660  Instance:db2inst2 Node:000
PID:15683(db2agent (SAMPLE))  TID:1024  Appid:*LOCAL.db2inst2.041A71201519
data management  sqlDEscalateLocks Probe:3  Database:SAMPLE

ADM5502W The escalation of "11373" locks on table "DB2INST2.EMP" to lock intent "X" was successful.
```

# 6.2.2 DB2 diagnostic log (db2diag.log)

Besides the notify log, you can also use the DB2 diagnostic log to help identify the cause of a problem that you are having with your Linux-based system. Once the data is collected, it can be examined by someone who is familiar with the problem, or provided to DB2 Customer Support staff for analysis, because sometimes this log file is not intuitive to understand — it may contain dumps or cryptic messages.

The file db2diag.log is located under the directory which is specified by the database manager configuration parameter DIAGPATH. Another instance level parameter DIAGLEVEL is used to specify which type of diagnostic errors will be recorded in the db2diag.log. The following are valid values:

+   0: No diagnostic data captured
+   1: Severe errors only
+   2: All errors
+   3: All errors and warnings
+   4: All errors, warnings and informational messages

You may want to increase the value of this parameter to gather additional problem determination data to help resolve a problem. The default value of DIAGLEVEL is 3. If you changed it to 4 for some reason, please remember to change it back to 3 or a lower value once the problem is resolved or the required information has been captured, because keeping DIAGLEVEL on a level of 4 will impact the system performance to a certain extent and the file system can fill up quickly.

The following log messages (Example 6-7) are extracted from db2diag.log. They are written into the log file when running the DB2 CLP command as below:

```
db2 update db cfg for sample using newlogpath /db2log
```

The part of db2diag.log shows that DB2 is trying to create a directory name /db2log/NODE0000 under /db2log, but the operating system prohibits DB2 from doing that and returned an error number "0d". It means permission denied (you can get the meaning of error number from errno.h include file). In our example, it