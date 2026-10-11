TABLE 6.8 Java-related init.ora Parameters (continued)  
| Parameter Name | Description |
| --- | --- |
| JAVA_MAX_SESSIONSPACE_SIZE | When memory is allocated to a Java process, the amount of memory requested is compared to this limit. If the request exceeds this limit, an out-of-memory error (ORA-29554) occurs. Default value is zero; maximum value is 4GB. |

TIP Oracle recommends setting JAVA_POOL_SIZE to 50MB or higher for large Java applications.

Oracle Objective Control the amount of Java session memory used by a session

Using Java, an application programmer can write and load Java applications inside the database. This level of intimacy between the application code and the database is supported because Java applications cannot interact with the OS to the same degree that an OS-specific application can. This separation allows the Java applications to execute safely within the database, with little concern for OS-related security. However, this closeness between Java and the database can also cause serious performance problems if an errant Java application consumes too many database resources. The JAVA_SOFT_SESSIONSPACE_LIMIT and JAVA_MAX_SESSIONSPACE_SIZE described in Table 6.8 are intended to let you limit the resources that a Java session is allowed to utilize within the database.

# Measuring the Performance of the Java Pool

Once you've configured the Java Pool to take advantage of its ability to enhance the performance of the Java-based database applications, you should monitor its performance so that you can determine whether it is optimally configured. You can use the V$SGASTAT dynamic performance view and STATSPACK output to monitor the performance of the Java Pool.