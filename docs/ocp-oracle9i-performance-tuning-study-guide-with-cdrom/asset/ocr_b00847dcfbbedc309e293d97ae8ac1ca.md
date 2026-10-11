| USERNAME | RESOURCE_CONSUMER_GROUP |
| :--- | :--- |
| DBSNMP | DEFAULT_CONSUMER_GROUP |
| SYSTEM | SYS_GROUP |
| APPS | POWER_USERS |
| BETTY | POWER_USERS |

The output from this query shows that three RCGs are assigned to connected application users: DEFAULT_CONSUMER_GROUP, SYS_GROUP, and POWER_USERS.

# V$RSRC_CONSUMER_GROUP

The V$RSRC_CONSUMER_GROUP dynamic performance view contains details about the resource allocations that have been made to the active resource consumer groups. Table 10.8 describes the contents of this view.

# TABLE 10.8  Contents of the V$RSRC_CONSUMER_GROUP View

| Column | Description |
| :--- | :--- |
| NAME | The name of the resource consumer group |
| ACTIVE_SESSIONS | The number of sessions that are currently assigned to this resource consumer group |
| EXECUTION_WAITERS | The number of sessions assigned to this resource consumer group that are waiting to be allocated resources before they can execute |
| REQUESTS | The total number of database requests that have been executed by users in this resource consumer group |
| CPU_WAIT_TIME | The total time that users in this resource consumer group have had to wait for access to the CPU (in 100<sup>th</sup>s of a second) |
| CPU_WAITS | The total number of times that users in the resource consumer group have waited for access to the CPU |
| CONSUMED_CPU_TIME | The total amount of CPU time that users in this resource consumer group have consumed (in 100<sup>th</sup>s of a second) |
| YIELDS | The number of times users in this resource consumer group have had to yield the CPU to users in other resource consumer groups with greater priority |