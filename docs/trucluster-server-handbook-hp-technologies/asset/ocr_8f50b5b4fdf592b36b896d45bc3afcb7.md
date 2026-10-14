The `on` parameter specifies the on-list, which is the list of one or more cluster member nodenames which are authorized to run the queue-daemon for the spool queue. The format of the on-list string is illustrated by the following examples:

```
on=localhost: \
on=node1: \
on=node1,node2,node3: \
```

If this parameter is not specified, `localhost` is assumed by default.

The order of the nodes in the on-list, from left to right, specifies the priority from highest to lowest which the member-node parent print daemons will use to determine which member-node will run the queue-daemon.

If localhost is specified, all member-nodes will be authorized to run the queue-daemon. Which node will actually run it is determined by the first node that submits a job to the queue while it is empty.

In a cluster, localhost or no value should be specified only for printers that are connected using tcp.

Printers that are connected to a device specified in the /dev/ directory must specify an on-list if the device is connected to a node that is part of a multi-node cluster. It is recommended that an on-list be specified if the cluster only contains one node.

For non-clustered, stand-alone hosts, use of an on-list specifying the local hostname or ‘localhost’ is optional.

Enter a new value, or press RETURN to use the default.

```
Enter a new value for symbol `on`? [molari]  <Enter>
```

There is also a new lock file used to coordinate lpd(8) activities from cluster members. The following is an excerpt from the lpd(8) reference page.

```
/usr/spool/lpd/lpd.lock
    On clustered systems, this transient file is created to contain the
    daemon status. Note that the /usr/spool/lpd directory is a Context
    Dependent Symbolic Link (CDSL) and should not be manually created or
    destroyed.
```

Note that the /usr/spool/lpd directory is a CDSL, so the spooling directory is member-specific. The /usr/spool/lpd/lpd.lock file is used to synchronize activities from the lpd daemons running on each cluster member. The printer’s log file (usually found in /usr/adm/lp0err — or a similar file name) is not a symbolic link, so all cluster members will log print activity to the same file. The reference pages want the lpd does not use its log files, so you may want to monitor their size periodically using a crontab entry (see existing entries under /usr/var/spool/cron/crontabs).

# Chapter 19