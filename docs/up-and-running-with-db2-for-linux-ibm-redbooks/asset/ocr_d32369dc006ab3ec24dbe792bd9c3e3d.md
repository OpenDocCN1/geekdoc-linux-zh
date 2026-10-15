Fortunately, DB2 Version 8 has a new feature that checks values of the kernel.semmni, kernel.msgmni, and kernel.shmmax parameters at db2start time, and changes them for you if the current values are not optimal. DB2start does the following:

+   - Changes semmni kernel parameter to 1024
+   - Changes msgmni kernel parameter to 1024
+   - Changes shmmax kernel parameter to 268435456 (32-bit) or 1073741824 (64-bit)

For example, after issuing db2start for the first time, we got the following messages in db2diag.log:

# Example 2-1 db2diag.log entries after starting instance

```
ADM05061 DB2 has automatically updated the "semmni" kernel parameter from "128" to the recommended value "1024".
2002-10-31-16.38.59.074791 Instance:db2inst1
Node:000
PID:15996(db2sysc) TID:8192 Appid:none
base sys utilities sqlesysc_main Probe:9

ADM05061 DB2 has automatically updated the "msgmni" kernel parameter from "16" to the recommended value "1024".
2002-10-31-16.38.59.076916 Instance:db2inst1
Node:000
PID:15996(db2sysc) TID:8192 Appid:none
base sys utilities sqlesysc_main Probe:9

ADM05061 DB2 has automatically updated the "shmmax" kernel parameter from "33554432" to the recommended value "268435456".
2002-10-31-16.39.01.262594 Instance:db2inst1
Node:000
PID:15994(db2star2) TID:8192 Appid:none
base sys utilities startdbm Probe:911

ADM7513W Database manager has started.
```

You may have noticed that db2start did not update the fs.file-max parameter — this is because any kernel at 2.4.18 and higher does this automatically for you.