
the following example, the agent has been configured to monitor the one-minute load average with a threshold of 2:

```
load 2
```

Should this limit be reached, the agent's MIB will be updated appropriately:

```
enterprises.ucdavis.loadTable.laEntry.laErrorFlag.1 = 1
enterprises.ucdavis.loadTable.laEntry.laErrorFlag.2 = 1
enterprises.ucdavis.loadTable.laEntry.laErrorFlag.3 = 0
enterprises.ucdavis.loadTable.laEntry.laErrorMessage.1 = "1 min Load Average too high (<= 2.50)"
enterprises.ucdavis.loadTable.laEntry.laErrorMessage.2 = "5 min Load Average too high (<= 2.26)"
enterprises.ucdavis.loadTable.laEntry.laErrorMessage.3 = ""
```

In this case, the MIB shows that both the one- and the five-minute load averages exceeded the 2 limit threshold. The MIB shows three instances of the laErrorFlag and laErrorMessage because the load average is measured in terms of one-, five-, and 15-minute averages. Thus, three separate MIB object instances are created.

The agent also provides access to both the current system load averages and the parameters for the configuration of the load command itself. For example, the following was obtained from the agent when the load was above the 2 mark:

```
enterprises.ucdavis.loadTable.laEntry.laNames.1 = "Load-1"
enterprises.ucdavis.loadTable.laEntry.laNames.2 = "Load-5"
enterprises.ucdavis.loadTable.laEntry.laNames.3 = "Load-15"
enterprises.ucdavis.loadTable.laEntry.laLoad.1 = "2.56" Hex: 32 2E 35 30
enterprises.ucdavis.loadTable.laEntry.laLoad.2 = "2.26" Hex: 32 2E 32 36
enterprises.ucdavis.loadTable.laEntry.laLoad.3 = "1.38" Hex: 31 2E 33 38
enterprises.ucdavis.loadTable.laEntry.laConfig.1 = "2.00" Hex: 32 2E 30 30
enterprises.ucdavis.loadTable.laEntry.laConfig.2 = "2.00" Hex: 32 2E 30 30
enterprises.ucdavis.loadTable.laEntry.laConfig.3 = "2.00" Hex: 32 2E 30 30
```

As you can see, the load averages for one and five minutes are above 2. Also, the laConfig object is set at 2.00 for each load average threshold level. The laNames object is simply a label used to describe each load average window. This information was obtained directly from the agent configuration file.

## Monitoring Disk Space

The agent can monitor disk-space consumption of any mounted file systems with the disk keyword command, using the following syntax:

```
disk [-system [minimum]]
```

The agent will monitor the specified file system and determine if the total disk space available is less than the minimum. If it is, the MIB object *diskErrorFlag* will be set to 1, and the MIB object *diskErrorMsg* will contain a descriptive message. If no minimum is provided, the agent uses the default value of 100K. The minimum value is stored in the *dskMinimum* object and set either to the specified minimum from the configuration file or to the default if no minimum value is found in the configuration file.

By way of example, consider the following agent commands:

```
disk /
disk /usr 1000
```

The first *disk* command will monitor the / (root) file system and compare the minimum value of 100 megabytes (Mb). If no size argument were supplied, a value of 100 kilobytes (the default) would be used. This value is compared to the total disk space that is available. The default value can be overridden. The second command will monitor the /usr file system and compare available space to the minimum value of 1,000 Kb. Because the minimum is in Kb units, we must add three zeros to the end to get the value in bytes. In this case, we get 1,000,000 bytes. Querying the agent returns the following:

```
enterprises.ucdavis.diskTable.diskEntry.diskMinimum.1 = 100000
enterprises.ucdavis.diskTable.diskEntry.diskMinimum.2 = 1000
enterprises.ucdavis.diskTable.diskEntry.diskAvail.1 = 56924
enterprises.ucdavis.diskTable.diskEntry.diskAvail.2 = 32545
enterprises.ucdavis.diskTable.diskEntry.diskErrorFlag.2 = 1
enterprises.ucdavis.diskTable.diskEntry.diskErrorMsg.1 = "/:
less than 100000 free ( - 56924)"
enterprises.ucdavis.diskTable.diskEntry.diskErrorMsg.2 = "**"
```

You will notice that two sets of MIB objects are defined. The first set corresponds to the root (/) file system because it appears first in the agent configuration file. The second set is for the /usr file system because it comes after the first entry within the configuration file.

As you can see, the diskMinimum objects are set accordingly; the diskMinimum.1 instance, which maps to the / file system, is set to 100Mb (100,000,000 bytes), while the second, diskMinimum.2, which maps to the /usr file system, is set to 1Mb (1,000,000 bytes). The agent also stores the available disk space of each monitored file system in the diskAvail object, one for each file system. In this case, the / file system is approximately 36Mb, while the /usr file system is approximately 32Mb. The diskErrorFlag.1 object for the file system is set because the root file system is less than 100Mb and the diskErrorMsg.1 contains more descriptive information. In this case, the diskErrorMsg.2 object does not contain any information. The diskErrorFlag.2 is not set because the /usr file system contains enough space to satisfy the disk space test.

The MIB also contains other information that can be used when monitoring disk space. The information is comparable to the output of the UNIX df (disk free) command. For example, the df -k command includes a summary of the disk space of the mounted file systems. The output below includes a partial list of the file systems reported:

| Filesystem | 1k-blocks | Used | Available | Use% | Mounted on |
| /dev/hdb1 | 82303 | 25286 | 56935 | 31% | / |
| /dev/hdb2 | 232141 | 199364 | 32545 | 86% | /usr |

When the agent is queried, we find the following:

```
enterprises.ucdavis.diskTable.diskEntry.diskPath.1 = "/" Hex: 2F
enterprises.ucdavis.diskTable.diskEntry.diskPath.2 = "/usr" Hex: 2F 75 73 72
enterprises.ucdavis.diskTable.diskEntry.diskDevice.1 = "/dev/hdb1" Hex:
enterprises.ucdavis.diskTable.diskEntry.diskDevice.2 = "/dev/hdb2"
enterprises.ucdavis.diskTable.diskEntry.diskTotal.2 = 232141
enterprises.ucdavis.diskTable.diskEntry.diskAvail.2 = 32545
enterprises.ucdavis.diskTable.diskEntry.diskUsed.1 = 25286
```

```
enterprises.ucdavis.diskTable.diskEntry.diskUsed.2 = 199364
enterprises.ucdavis.diskTable.diskEntry.diskPercent.1 = 31
enterprises.ucdavis.diskTable.diskEntry.diskPercent.2 = 86
```

Notice that the MIB contains all the information that the df command provides. This includes the mount points, file systems, total disk space, available disk space, used disk space, and percent disk space used. This information can be extremely helpful because, for example, it is possible to monitor disk-space usage in percentages instead of raw bytes by using the dskPercent objects. Also, the remaining objects can be used as an automated mechanism for inventory of system storage capacities. The "Linux MIB" section includes more information on these and other agent MIB objects.

### Monitoring System Processes

The proc command can monitor specific application services or standard UNIX processes. The command uses the following syntax:

```
proc process [maximum limit] [minimum limit]
```

This command is followed by a valid process name or command to be monitored by the agent. This directive is used to monitor a critical process or a set of processes that must be running continuously on the system. If the process is not found running on the local system by the agent, an error flag is set in the MIB object procTable.prEntry.prErrorFlag, and a descriptive message is placed in the MIB object procTable.prEntry.prErrorMessage. The agent uses the UNIX ps -e command to search for running processes as specified with the proc command. For instance, the following command can be used to ensure that the mountd process is alive:

```
proc mountd
```

Additionally, a maximum and minimum value can be included to further refine the number of processes that should be running. The maximum indicates how many processes should be running concurrently, while the minimum determines the smallest number that must be running. For example, since it is customary to have multiple mountd processes on a system, the agent can be configured to monitor the exact number. For the sake of discussion, let's
