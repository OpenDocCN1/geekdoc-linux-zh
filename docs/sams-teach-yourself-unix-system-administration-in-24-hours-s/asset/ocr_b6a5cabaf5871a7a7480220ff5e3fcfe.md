```
service telnet
{
    flags         = REUSE
    socket_type   = stream
    wait          = no
    user          = root
    server        = /usr/sbin/in.telnetd
    log_on_failure += USERID
    disable       = yes
}
```

Most of the specific flags should be familiar from the format of the inetd.conf file, including socket_type, wait, user, and server. flags lets you specify one of a wide variety of different low-level network options. In this case, REUSE means that this service has a specific reuse-address flag set (see the xinetd.conf(5) man page for more details. Beware, it's very low-level!).

There's a wonderful feature demonstrated in the log_on_failure parameter in this service definition. Notice that it's using +=, which means that in addition to the default values logged on failure, the telnet service will additionally log USERID. Table 19.1 lists the parameters that can be logged upon the success or failure of a given connection.

TABLE 19.1 Information Logged from xinetd

| Value | Used When | Explanation |
|---|---|---|
| ATTEMPT | Failure | Logs the fact that a failed attempt was made |
| DURATION | Success | Logs the duration of a service session |
| EXIT | Success | Logs when the server quits |
| HOST | Success or Failure | The remote host address |
| PID | Success | The process ID of the server application |
| RECORD | Failure | Records as much information as possible from the remote end |
| USERID | Success or Failure | The user id of the remote host, if available |

Finally, the last line in the telnet configuration listing is perhaps the most important. The disable parameter can be yes or no. If it's yes, the service cannot be started by xinetd and connection attempts will fail. If it's set to no, the service is enabled.

+   3. The use of the disable parameter leads to the greatest problem with xinetd—it's rather difficult to figure out what services are enabled and which are disabled.