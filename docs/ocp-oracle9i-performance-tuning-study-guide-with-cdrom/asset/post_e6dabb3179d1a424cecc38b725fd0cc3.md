
The `init.ora` parameters shown in Table 6.1 replace the deprecated Oracle8i parameters MTS_DISPATCHERS, MTS_MAX_DISPATCHERS, MTS_SERVERS, MTS_MAX_SERVERS, and MTS_CIRCUITS.

While the DISPATCHERS and SHARED_SERVERS parameters are used to establish the minimum number of those processes to spawn at instance startup, both components can be adjusted upward to the ceiling values specified by MAX_DISPATCHERS and MAX_SHARED_SERVERS. However, while Dispatcher processes must be explicitly started by the DBA using the ALTER SYSTEM command, Shared Server processes can be dynamically started and stopped by the PMON background process based on the demands placed on those resources by the connected application users.

Determining how many Dispatchers and Shared Servers to spawn at instance startup can be determined by monitoring the performance of the Shared Server environment once it has been initially configured.

Database administrators cannot use Shared Server connections to perform DBA operations like database startups, shutdowns, etc.

## Measuring Shared Server Performance

Once configured the Shared Server option must be monitored and tuned to obtain optimal performance. Just as with the Shared Pool and Database Buffer Cache, several dynamic performance views can be used to monitor the performance of the Shared Server environment. These dynamic performance views are described in Table 6.2.

### TABLE 6.2 Shared Server Dynamic Performance Views

| View Name | Description |
| :--- | :--- |
| V$SHARED_SERVER | Contains detailed statistics about the Shared Server processes, including idle and busy times for each Shared Server process. |
| V$QUEUE | Contains information about contention for Shared Server Request and Response queues. |
| V$SHARED_SERVER_MONITOR | Contains statistics regarding the Shared Server processes, including the Shared Servers that have been dynamically started and terminated by PMON since instance startup. |
| V$DISPATCHER | Contains detailed statistics about the Shared Server Dispatcher processes, including idle and busy times for each Dispatcher process. |
| V$DISPATCHER_RATE | Contains historical and real-time statistics regarding Dispatcher activity. |
| V$CIRCUIT | Contains statistics about the path, or circuit, a User Process has taken through a Dispatcher, Request Queue, Shared Server, Response Queue, and back to the User Process again. |

Each of the above views can be used to monitor the two dynamic components of the Shared Server architecture: Shared Server processes and Dispatcher Processes.

Oracle Objective Diagnose and resolve performance issues with Oracle Shared Server processes

## Monitoring Shared Server Process Performance

One way to monitor the performance of the Shared Server processes is to monitor at what rate the available server processes are servicing database requests. This busy ratio can be calculated using the V$SHARED_SERVER dynamic performance view. Selected columns from this view that are useful for monitoring Shared Server busy ratios are shown in Table 6.3.

Figure 6.2 shows how, by querying these columns, a Shared Server busy ratio can be calculated.

### TABLE 6.3 Selected Columns from V$SHARED_SERVER

| Column Name | Description |
| :--- | :--- |
| NAME | Shared Server process name |
| REQUESTS | Total number of requests that the Shared Server has serviced during the time it was running |
| BUSY | Total amount of time (in 100th of a second) that the Shared Server was busy during the time it was running |
| IDLE | Total amount of time (in 100th of a second) that the Shared Server was idle during the time it was running |

### FIGURE 6.2 Calculating the Shared Server Busy Ratio

```sql
SQL> SELECT name, DECODE(busy+idle, 0, 0,
2    FROM v$shared_server
3         ROUND((busy/(busy+idle))*100,4)) "BUSY_RATE"
4  WHERE status != 'QUIT' ;
```

NAME   BUSY_RATE
-------- ----------
5000   12.34
5001   16.85
5002    9.73

The output from the above query shows that, at most, the Shared Server processes were busy servicing database requests 16.85 percent of the time.

> High or increasing Shared Server busy ratios indicate that additional Shared Server processes may need to be spawned at instance startup.

When User Processes make a database request using a Shared Server, their requests are initially placed in the Request Queue by the *Dispatcher* process. If there are too few Shared Server processes, these requests may experience a delay while waiting to be serviced. These waits for access to a Shared Server process can be monitored using the **V$QUEUE** dynamic performance view. Selected columns from this view that are useful for monitoring contention for Shared Servers are shown in Table 6.4.

### TABLE 6.4 Selected Columns from V$QUEUE

| Column Name | Description |
| :--- | :--- |
| TYPE | Type of queue that the statistics are for, either DISPATCHER or COMMON (Shared Server) |
| TOTALQ | Total number of items placed in the queue |
| WAIT | Total time that all items in the queue spent waiting for access to a Shared Server process, in 100th of a second |

By querying these columns, an average wait time for access to a Shared Server can be calculated. This type of query is shown in Figure 6.3.

### FIGURE 6.3 Calculating average wait times for Shared Servers

```sql
SQL>SELECT DECODE(totalq,0,'TOTALQ IS ZERO',
2
ROUND(SUM(wait)/SUM(totalq),4) "AVG DISPATCHER WAIT"
3
FROM v$queue
4
WHERE type = 'COMMON'
5
GROUP BY totalq;
```

AVG DISPATCHER WAIT
---------------
.0003

The output from the above query shows that, on average, User Processes waited .0003 hundredths of a second for a Shared Server process to service their database requests.

![](img/832fbc6aca8b6075843ca6f2356c0a8d_340_0.png)

High or increasing waits for Shared Server processes may indicate a need to spawn additional Shared Server processes at instance startup.

## Monitoring Dispatcher Performance

Like Shared Servers, the performance of the Dispatcher processes can also be monitored using a "busy ratio." This ratio can be calculated using the V$DISPATCHER dynamic performance view. Selected columns from this view that are useful for monitoring Dispatcher busy ratios are shown in Table 6.5. By querying these columns, a Dispatcher busy ratio can be calculated using the SQL statement shown in Figure 6.4.

### TABLE 6.5 Selected Columns from V$DISPATCHER

| Column Name | Description |
| :--- | :--- |
| NETWORK | Protocol used by the Dispatcher (network address) |
| STATUS | Current status of the Dispatcher. Possible Dispatcher statuses are: WAIT (idle), SEND (sending a message), RECEIVE (receiving a message), CONNECT (establishing connection), DISCONNECT (disconnecting a session), BREAK (performing a break), TERMINATE (terminating a connection), ACCEPT (accepting connections), REFUSE (refusing connection) |
| OWNED | Number of virtual circuits owned by this Dispatcher |
| BUSY | Total time (in 100th of second) that the Dispatcher was busy |
| IDLE | Total time (in 100th of second) that the Dispatcher was idle |

### FIGURE 6.4 Query to determine Dispatcher busy ratio

```sql
SQL> SELECT name "DISPATCHER", network, (ROUND(SUM(busy)/(SUM(busy)+SUM(idle)),4))*100 "BUSY_RATE" FROM v$dispatcher GROUP BY name, network;
```

| DISPATCHER | NETWORK | BUSY_RATE |
| :--- | :--- | :--- |
| D000 | ADDRESS=<PROTOCOL=tcp)(HOST=moderne)(PORT=45280)) | 33.23 |
| D001 | ADDRESS=<PROTOCOL=tcp)(HOST=moderne)(PORT=45282)) | 27.12 |
| D003 | ADDRESS=<PROTOCOL=tcp)(HOST=moderne)(PORT=45283)) | 17.29 |

The output from the above query shows that, at most, the three Dispatcher processes for the TCP/IP network protocol were busy servicing database requests 33.23 percent of the time.

![](img/832fbc6aca8b6075843ca6f2356c0a8d_341_0.png)

Oracle recommends adding additional Dispatcher processes if the Dispatcher busy rate consistently exceeds 50 percent.
