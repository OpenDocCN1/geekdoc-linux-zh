# Table 19-4 (Continued)

| Timeout Events | Waiting for . . . |
|---|---|
| initial | the initial greeting message |
| mail | acknowledgment of the MAIL command |
| misc | acknowledgment of other SMTP commands |
| queuereturn (any priority) | the message delivery to complete (a bounce message will be delivered) |
| queuewarn (any priority) | the message delivery to complete (a warning message will be delivered) |
| quit | acknowledgment of the QUIT command |
| rcpt | acknowledgment of the RCPT command |
| rset | acknowledgment of the RSET command |
| | |

The next lines relate to pruning routes:

```
# should we not prune routes in route-addr syntax addresses?
#O DontPruneRoutes
```

With the DontPruneRoutes option, an address can be specified as a “route address” where an explicit path through a sequence of hosts is indicated. If the option is set to True, this route is followed. Otherwise, the route is pruned. The next lines relate to where messages are stored as they are being delivered:

```
# queue up everything before forking?
O SuperSafe=True
```

If the SuperSafe option is set to False, sendmail reads a message into memory before delivering it. If the machine were to crash at this point, the message would be lost. When the SuperSafe option is set to True, the message always exists on the file system until delivery is completed. No good reason exists for this option to be set to False. The next lines relate to the status file:

```
# status file
O StatusFile=/var/log/sendmail.st
```

The StatusFile option specifies a file where mail delivery statistics can be stored. This file is then parsed by the mailstats program to display the number of messages sent and the size of those messages (in kilobytes), the number of messages received and the size of those messages (also in kilobytes), the number of messages rejected, and the number of messages discarded.