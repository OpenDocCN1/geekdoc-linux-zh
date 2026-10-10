As queries come up that take longer than your threshold, you will be able to see them in this log along with information about the query, such as the user who executed it, the query and lock times, how many rows were sent, and how many were examined. You can then use this information to go back to your application, identify where that query originates, and find ways to optimize it.

Another way to identify problem MySQL queries is via the `mysqladmin processlist` command, which lists information about all the currently active MySQL processes. Here's some sample output from a relatively inactive WordPress install that had one client (a local mysql client connection) connected along with this `mysqladmin` command:

```
$ mysqladmin -u root -p processlist
Enter password:
```

```
+----------------------------------------+
| Id | User | Host | db | Command | Time | State | Info |
+----------------------------------------+
| 2663 | root | localhost | wordpress | Sleep | 80 |  |  |
| 2686 | root | localhost |  | Query | 0 |  | show processlist |
+----------------------------------------+
```

You can also add the -i option along with the number of seconds; when you do, this command will execute over and over with that number of seconds gap in between. Then you can monitor commands as they come in and identify any queries that are taking much longer than they should. If you do identify a query that is slowing down the system and you want to kill it, make a note of the process ID in the output of the processlist command, and use the kill command along with that process ID to kill the process. For instance, if you wanted to kill the above connection to the WordPress DB that had been connected for 80 seconds, you would type

```
$ mysqladmin -u root -p kill 2663
```

# PostgresSQL

PostgresSQL gives you the option to log all queries, not just those that are above a certain threshold with the `log_min_duration_statement` setting. If this