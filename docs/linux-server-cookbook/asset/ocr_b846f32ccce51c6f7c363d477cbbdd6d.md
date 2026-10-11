```
*restore
Automatically selected Catalog: MyCatalog
Using Catalog "MyCatalog"

First you select one or more JobIds that contain files to be restored. You will be presented several methods of specifying the JobIds. Then you will be allowed to select which files from those JobIds are to be restored.

To select the JobIds, you have the following choices:

1: List last 20 Jobs run
2: List Jobs where a given File is saved
3: Enter list of comma separated JobIds to select
4: Enter SQL list command
5: Select the most recent backup for a client
6: Select backup for a client before a specified time
7: Enter a list of files to restore
8: Enter a list of files to restore before a specified time
9: Find the JobIds of the most recent backup for a client
10: Find the JobIds for a backup for a client before a specified time
11: Enter a list of directories to restore for found JobIds
12: Select full restore to a specified Job date
13: Select object to restore
14: Cancel
Select item: (1-14): 5
Defined Clients:
1: bacula-fd
2: rhel-fd
Select the Client (1-2): 2
Automatically selected FileSet: OnlyEtc
```

+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| JobId | Level | JobFiles | JobBytes | StartTime | VolumeName |
+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| 13 | F | 1,003 | 21,126,497 | 2022-11-12 20:14:54 | Vol-0001 |
+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

You have selected the following JobId: 13

*Figure 14.9: Example restoring files with the command bconsole*

After the latest **Backup** is selected automatically for the client specified, a command line to specify the files to restore (using the keyword **add**) is available. When the defined files to recover are finished, the command **done** will perform the restoration. *Figure 14.10* shows an example: